---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Öğretici: SignalR 2 ile Sunucu yayını | Microsoft Dokümanlar'
author: tdykstra
description: Bu öğretici, sunucu yayını işlevselliğini sağlamak için ASP.NET SignalR 2 kullanan bir web uygulamasının nasıl oluşturulacağını gösterir.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676099"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Öğretici: SignalR 2 ile sunucu yayını

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Bu öğretici, sunucu yayını işlevselliğini sağlamak için ASP.NET SignalR 2 kullanan bir web uygulamasının nasıl oluşturulacağını gösterir. Sunucu yayını, sunucunun istemcilere gönderilen iletişimi başlattığı anlamına gelir.

Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir hisse senedi işaretleyicisini simüle eder. Düzenli olarak, sunucu hisse senedi fiyatlarını rasgele günceller ve güncelleştirmeleri bağlı tüm istemcilere yayınlar. Tarayıcıda, **Değiştir** ve sütunlarda bulunan **%** sayılar ve semboller, sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir. Aynı URL'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.

![Web oluşturma](tutorial-server-broadcast-with-signalr/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Proje oluşturma
> * Sunucu kodunu ayarlama
> * Sunucu kodunu inceleme
> * İstemci kodunu ayarlama
> * İstemci kodunu inceleyin
> * Uygulamayı test etme
> * Günlü kaydını etkinleştir

> [!IMPORTANT]
> Uygulamayı oluşturma adımlarını gözden geçirmek istemiyorsanız, SignalR.Sample paketini yeni bir Boş ASP.NET Web Uygulaması projesine yükleyebilirsiniz. NuGet paketini bu öğreticideki adımları gerçekleştirmeden yüklerseniz, *readme.txt* dosyasındaki yönergeleri izlemeniz gerekir. Paketi çalıştırmak için, yüklenen paketteki `ConfigureSignalR` yöntemi çağıran bir OWIN başlangıç sınıfı eklemeniz gerekir. OWIN başlangıç sınıfını eklemezseniz bir hata alırsınız. Bu [makalenin StockTicker örnek bölümüne yükleyin](#install-the-stockticker-sample) bakın.

## <a name="prerequisites"></a>Ön koşullar

* **ASP.NET ve web geliştirme** iş yüküyle [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).

## <a name="create-the-project"></a>Proje oluşturma

Bu bölümde, boş bir ASP.NET Web Uygulaması oluşturmak için Visual Studio 2017'nin nasıl kullanılacağı gösterilmektedir.

1. Visual Studio'da bir ASP.NET Web Uygulaması oluşturun.

    ![Web oluşturma](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. Yeni **ASP.NET Web Uygulaması - SignalR.StockTicker** penceresinde, **Boş** seçili bırakın ve **Tamam'ı**seçin.

## <a name="set-up-the-server-code"></a>Sunucu kodunu ayarlama

Bu bölümde, sunucuda çalışan kodu ayarlarsınız.

### <a name="create-the-stock-class"></a>Stok sınıfı oluşturma

Stok hakkındaki bilgileri depolamak ve iletmek için kullanacağınız *Stok* modeli sınıfını oluşturarak başlarsınız.

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Sınıf** **Ekle'yi** > seçin.

1. Sınıf *Stok'u* adlandırın ve projeye ekleyin.

1. *Stock.cs* dosyasındaki kodu bu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Hisse senetleri oluştururken ayarladığınız iki `Symbol` özellik (örneğin, Microsoft için `Price`MSFT) ve . Diğer özellikler nasıl ve ne `Price`zaman ayarladığınıza bağlıdır. İlk olarak ayarlağınızda, `Price`değer `DayOpen`' e yayılır. Bundan sonra, ayarladığınızda, `Price`uygulama ve `Change` `PercentChange` arasındaki `Price` farka göre özellik `DayOpen`değerlerini hesaplar.

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>StockTickerHub ve StockTicker sınıflarını oluşturun

Sunucudan istemciye etkileşimi işlemek için SignalR Hub API'sını kullanırsınız. SignalR `StockTickerHub` `Hub` sınıfından türeyen bir sınıf, istemcilerden bağlantı ve yöntem çağrıları alma işlemlerini işler. Ayrıca stok verilerini korumak ve `Timer` bir nesne çalıştırmak gerekir. Nesne, `Timer` istemci bağlantılarından bağımsız olarak düzenli olarak fiyat güncelleştirmelerini tetikler. Hub'lar geçici olduğundan, `Hub` bu işlevleri bir sınıfa koyamazsınız. Uygulama, istemciden `Hub` sunucuya bağlantılar ve aramalar gibi hub'daki her görev için bir sınıf örneği oluşturur. Bu nedenle, stok verilerini tutan, fiyatları güncelleyen ve fiyat güncelleştirmelerini yayınlayan mekanizmanın ayrı bir sınıfta çalışması gerekiyor. Sınıfa `StockTicker`isim vereceksin.

![StockTicker'dan Yayın](tutorial-server-broadcast-with-signalr/_static/image3.png)

`StockTicker` Sınıfın yalnızca bir örneğinin sunucuda çalışmasını istiyorsunuz, bu nedenle her `StockTickerHub` örnekten singleton `StockTicker` örneğine bir başvuru ayarlamanız gerekir. Sınıf, `StockTicker` stok verilerine sahip olduğundan ve güncelleştirmeleri tetiklediği `StockTicker` için istemcilere yayın yapmak zorundadır, ancak bir `Hub` sınıf değildir. Sınıfın `StockTicker` SignalR Hub bağlantı bağlamı nesnesine bir başvuru alması gerekiyor. Daha sonra istemcilere yayın için SignalR bağlantı bağlamı nesnesini kullanabilirsiniz.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs oluşturma

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Yeni Öğe** **Ekle'yi** > seçin.

1. **Yeni Öğe Ekle - SignalR.StockTicker**, **Yüklü** > **Görsel C#** > **Web** > **SignalR'ı** seçin ve ardından **SignalR Hub Sınıfı'nı (v2)** seçin.

1. *StockTickerHub* sınıfının adını ve projeye ekleyin.

    Bu adım, *StockTickerHub.cs* sınıf dosyası oluşturur. Aynı anda, projeye SignalR'ı destekleyen bir dizi komut dosyası dosyası ve derleme başvurusu ekler.

1. *StockTickerHub.cs* dosyasındaki kodu bu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Dosyayı kaydedin.

Uygulama, istemcilerin sunucuda çağırabileceği yöntemleri tanımlamak için [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfını kullanır. Bir yöntem tanımlıyorsunuz: `GetAllStocks()`. Bir istemci başlangıçta sunucuya bağlandığında, geçerli fiyatları ile tüm hisse senetlerinin bir listesini almak için bu yöntemi arayacaktır. Yöntem eşzamanlı olarak çalıştırılabilir `IEnumerable<Stock>` ve bellekten veri döndürdeğinden döndürülebilir.

Yöntem, veritabanı araması veya web hizmeti çağrısı gibi beklemeyi gerektirecek bir şey yaparak verileri `Task<IEnumerable<Stock>>` almak zorunda kaldıysa, eşzamanlı işlemeyi etkinleştirmek için iade değeri olarak belirtirsiniz. Daha fazla bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Ne zaman eşzamanlı olarak yürütülmesi gerektiğini](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)görün.

Öznitelik, `HubName` uygulamanın istemcideki JavaScript kodundaki Hub'a nasıl başvurulacağını belirtir. Bu özniteliği kullanmazsanız istemcideki varsayılan ad, sınıf adının camelCase sürümüdür ve bu durumda `stockTickerHub`.

`StockTicker` Sınıfı oluşturduğunuzda daha sonra göreceğiniz gibi, uygulama statik `Instance` özelliğinde bu sınıfın tek tonluk bir örneğini oluşturur. Bu singleton `StockTicker` örneği, kaç istemci bağlanır veya bağlantıyı keserse bağlansın bellektedir. Bu örnek, `GetAllStocks()` yöntemin geçerli stok bilgilerini döndürmek için kullandığı örnektir.

#### <a name="create-stocktickercs"></a>StockTicker.cs oluştur

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Sınıf** **Ekle'yi** > seçin.

1. *StockTicker* sınıfının adını ve projeye ekleyin.

1. *StockTicker.cs* dosyasındaki kodu bu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Tüm iş parçacıkları StockTicker kodunun aynı örneğini çalıştıracağı için StockTicker sınıfının iş parçacığı açısından güvenli olması gerekir.

### <a name="examine-the-server-code"></a>Sunucu kodunu inceleme

Sunucu kodunu incelerseniz, uygulamanın nasıl çalıştığını anlamanıza yardımcı olur.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Tekton örneğini statik bir alanda depolama

Kod, `Instance` özelliği destekleyen `_instance` statik alanı sınıfın bir örneğiyle birlikte baş harfe döndürer. Oluşturucu özel olduğundan, uygulamanın oluşturabileceği tek örnektir. Uygulama `_instance` alan için [Lazy başlatma](/dotnet/framework/performance/lazy-initialization) kullanır. Performans nedenlerinden dolayı değil. Örnek oluşturmanın iş parçacığı için güvenli olduğundan emin olmak içindir.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

Bir istemci sunucuya her bağlandığında, ayrı bir iş parçacığıiçinde çalışan StockTickerHub sınıfının yeni bir `StockTicker.Instance` örneği, `StockTickerHub` daha önce sınıfta gördüğünüz gibi StockTicker singleton örneğini statik özellikten alır.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Stok verilerinin Eşzamanlı Sözlük'te saklanması

Oluşturucu, koleksiyonu bazı `_stocks` örnek stok verileriyle `GetAllStocks` başolarak alır ve stokları döndürür. Daha önce de gördüğünüz gibi, bu `StockTickerHub.GetAllStocks`hisse senetleri koleksiyonu, `Hub` istemcilerin çağırabileceği sınıftaki bir sunucu yöntemi olan tarafından döndürülür.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Stoktoplama iş parçacığı güvenliği için [EşzamanlıSözlük](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır. Alternatif olarak, [sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve sözlükte değişiklik yaptığınızda sözlüğü açıkça kilitleyebilirsiniz.

Bu örnek uygulama için, uygulama verilerini bellekte depolamak ve uygulama `StockTicker` örneği attığında verileri kaybetmek sorun değil. Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposu yla çalışırsınız.

#### <a name="periodically-updating-stock-prices"></a>Hisse senedi fiyatlarını periyodik olarak güncelleme

Oluşturucu, hisse `Timer` senedi fiyatlarını rasgele güncelleştiren yöntemleri düzenli olarak çağıran bir nesne başlatır.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`aramalar `UpdateStockPrices`, durum parametresi null geçer. Fiyatları güncellemeden önce, uygulama nesneye `_updateStockPricesLock` kilitlenir. Kod, başka bir iş parçacığının fiyatları zaten `TryUpdateStockPrice` güncelleştirip güncellediğini denetler ve ardından listedeki her hisse senedini çağırır. Yöntem, `TryUpdateStockPrice` hisse senedi fiyatını değiştirip değiştirmeyeceğine ve ne kadar değiştireceğinize karar verir. Hisse senedi fiyatı değişirse, uygulama hisse senedi fiyat değişikliğini bağlı tüm istemcilere yayınlamayı çağırır. `BroadcastStockPrice`

İş `_updatingStockPrices` parçacığı güvenli olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak atanan bayrak.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

Gerçek bir uygulamada, `TryUpdateStockPrice` yöntem fiyat aramak için bir web hizmeti çağırır. Bu kodda, uygulama rasgele değişiklik yapmak için rasgele bir sayı üreteci kullanır.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker sınıfının istemcilere yayın yapabilmesi için SignalR bağlamını alma

Fiyat değişiklikleri burada `StockTicker` nesne kaynaklı olduğundan, tüm bağlı istemcilerde bir `updateStockPrice` yöntem çağırmak için gereken nesnedir. Bir `Hub` sınıfta, istemci yöntemlerini aramak için bir `StockTicker` API'niz vardır, ancak `Hub` sınıftan türeyen `Hub` ve herhangi bir nesneye başvurunuz yoktur. Bağlı istemcilere yayın `StockTicker` yapmak için sınıfın sınıf için SignalR bağlam örneğini `StockTickerHub` alması ve istemcilere yönelik yöntemleri aramak için bunu kullanması gerekiyor.

Kod, tekton sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya `Clients` geçirir ve oluşturucu onu özelliğe koyar.

Bağlamı yalnızca bir kez almak istemenizin iki nedeni vardır: bağlamı almak pahalı bir görevdir ve bir kez almak, uygulamanın istemcilere gönderilen iletilerin amaçlanan sırasını koruduğundan emin olur.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Bağlamın `Clients` özelliğini almak ve `StockTickerClient` özelliğine koymak, `Hub` bir sınıfta olduğu gibi görünen istemci yöntemlerini aramak için kod yazmanıza olanak tanır. Örneğin, tüm istemcilere yayın için `Clients.All.updateStockPrice(stock)`yazabilirsiniz.

Aradığınız `updateStockPrice` `BroadcastStockPrice` yöntem henüz yok. İstemci üzerinde çalışan kod yazarken daha sonra eklersiniz. Dinamik `Clients.All` olduğu `updateStockPrice` için buraya başvurabilirsiniz, bu da uygulamanın çalışma zamanında ifadeyi değerlendireceği anlamına gelir. Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve `updateStockPrice`istemcide adlı bir yöntem varsa, uygulama bu yöntemi çağırır ve parametre değerini ona geçirir.

`Clients.All`tüm istemcilere göndermek anlamına gelir. SignalR, hangi istemcilere veya istemci gruplarına gönderilecini belirtmeniz için başka seçenekler sunar. Daha fazla bilgi için [HubConnectionContext'a](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)bakın.

### <a name="register-the-signalr-route"></a>SignalR rotasını kaydedin

Sunucunun hangi URL'yi yakalayıp SignalR'a yönlendirecek olduğunu bilmesi gerekir. Bunu yapmak için bir OWIN başlangıç sınıfı ekleyin:

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Yeni Öğe** **Ekle'yi** > seçin.

1. **Yeni Öğe Ekle - SignalR.StockTicker** **Yüklü** > **Visual C#** > **Web'i** seçin ve ardından **OWIN Başlangıç Sınıfı'nı**seçin.

1. *Sınıf Başlangıç* adını ve **Tamam'ı**seçin.

1. *Startup.cs* dosyasındaki varsayılan kodu bu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Sunucu kodunu ayarlamayı tamamladınız. Bir sonraki bölümde istemciyi ayarla.

## <a name="set-up-the-client-code"></a>İstemci kodunu ayarlama

Bu bölümde, istemci üzerinde çalışan kodu ayarlarsınız.

### <a name="create-the-html-page-and-javascript-file"></a>HTML sayfasını ve JavaScript dosyasını oluşturma

HTML sayfası verileri görüntüler ve JavaScript dosyası verileri düzenler.

#### <a name="create-stocktickerhtml"></a>StockTicker.html oluştur

İlk olarak, HTML istemcisini eklersiniz.

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve**HTML Sayfası** **Ekle'yi** > seçin.

1. *StockTicker* dosyasını adlandırın ve **Tamam'ı**seçin.

1. *StockTicker.html* dosyasındaki varsayılan kodu bu kodla değiştirin:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML, beş sütun, üstbilgi satırı ve beş sütunun tümine yayılan tek bir hücreye sahip bir veri satırı içeren bir tablo oluşturur. Veri satırı "yükleme..." uygulama başladığında anlık olarak. JavaScript kodu bu satırı kaldırır ve sunucudan alınan stok verileriyle yer satırları ekler.

    Komut dosyası etiketleri şunları belirtir:

    * jQuery komut dosyası dosyası.

    * SignalR çekirdek komut dosyası dosyası.

    * SignalR komut dosyası dosyasını vekiller.

    * Daha sonra oluşturacağınız StockTicker komut dosyası dosyası.

    Uygulama dinamik olarak SignalR yakınlık komut dosyası dosyasını oluşturur. "/signalr/hub" URL'sini belirtir ve Hub sınıfındaki yöntemler için `StockTickerHub.GetAllStocks`proxy yöntemleri tanımlar, bu durumda, için. İsterseniz, [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)kullanarak bu JavaScript dosyayı el ile oluşturabilirsiniz. Yöntem çağrısında dinamik dosya oluşturmayı `MapHubs` devre dışı etmeyi unutmayın.

1. **Çözüm Gezgini'nde,** **Komut Dosyalarını**genişletin.

    JQuery ve SignalR için komut dosyası kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket yöneticisi SignalR komut dosyalarının daha sonraki bir sürümünü yükler.

1. Kod bloğundaki komut dosyası başvurularını projedeki komut dosyası dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.

1. **Solution Explorer'da** *StockTicker.html'e*sağ tıklayın ve ardından **Başlangıç Sayfası olarak Ayarla'yı**seçin.

#### <a name="create-stocktickerjs"></a>StockTicker.js oluştur

Şimdi JavaScript dosyasını oluşturun.

1. **Solution Explorer'da**projeyi sağ tıklatın ve**JavaScript Dosyası** **Ekle'yi** > seçin.

1. *StockTicker* dosyasını adlandırın ve **Tamam'ı**seçin.

1. Bu kodu *StockTicker.js* dosyasına ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>İstemci kodunu inceleyin

İstemci kodunu incelerseniz, uygulamanın çalışmasını sağlamak için istemci kodunun sunucu koduyla nasıl etkileşimde olduğunu öğrenmenize yardımcı olur.

#### <a name="starting-the-connection"></a>Bağlantıyı başlatma

`$.connection`SignalR yakınlıklarını ifade eder. Kod `StockTickerHub` sınıf için proxy bir başvuru alır ve `ticker` değişken koyar. Proxy adı öznitelik tarafından `HubName` ayarlanan addır:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Tüm değişkenleri ve işlevleri tanımladıktan sonra, dosyadaki son kod satırı SignalR `start` işlevini çağırarak SignalR bağlantısını açar. İşlev `start` eşsenkronize yürütür ve [bir jQuery Ertelenmiş nesne](http://api.jquery.com/category/deferred-object/)döndürür. Uygulama asynchronous eylemi bittiğinde aranacak işlevi belirtmek için yapılan işlevi arayabilirsiniz.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Tüm hisse senetlerialma

İşlev `init` sunucudaki `getAllStocks` işlevi çağırır ve stok tablosunu güncelleştirmek için sunucunun döndürdettiği bilgileri kullanır. Varsayılan olarak, yöntem adı sunucuda pascal-cased olsa bile istemci üzerinde camelCasing kullanmanız gerektiğine dikkat edin. CamelCasing kuralı sadece yöntemler için geçerlidir, nesneler için değil. Örneğin, başvurur `stock.Symbol` ve `stock.Price`, `stock.symbol` `stock.price`değil veya .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

`init` `formatStock` Yöntemde, uygulama, `stock` nesnenin özelliklerini biçimlendirmek için arayarak sunucudan alınan her stok nesnesi `supplant` için bir tablo `rowTemplate` satırı için `stock` HTML oluşturur ve ardından değişkendeki yer tutucuları nesne özellik değerleriyle değiştirmek için çağrıda bulunur. Elde edilen HTML daha sonra stok tablosuna eklenir.

> [!NOTE]
> Asynchronous `init` `start` işlevi bittikten sonra çalıştırılabilen bir `callback` işlev olarak geçirerek çağırırsınız. Aradıktan `init` sonra ayrı bir JavaScript `start`deyimi olarak adlandırılan , bağlantı kurmayı bitirmek için başlangıç işlevi beklemeden hemen çalışacak çünkü işlev başarısız olur. Bu durumda, `init` işlev, uygulama bir `getAllStocks` sunucu bağlantısı kurmadan önce işlevi çağırmayı dener.

#### <a name="getting-updated-stock-prices"></a>Güncellenmiş hisse senedi fiyatları alma

Sunucu bir hisse senedinin fiyatını değiştirdiğinde, bağlı istemcileri `updateStockPrice` çağırır. Uygulama, sunucudan gelen aramalariçin `stockTicker` kullanılabilir hale getirmek için proxy istemci özelliğine işlevi ekler.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

İşlev, `updateStockPrice` sunucudan alınan stok nesnesini `init` işlevdeki yle aynı şekilde bir tablo satırına biçimlendirir. Satırı tabloya eklemek yerine, tabloda stokun geçerli satırını bulur ve bu satırı yenisiyle değiştirir.

## <a name="test-the-application"></a>Uygulamayı test etme

Çalıştığından emin olmak için uygulamayı test edebilirsiniz. Tüm tarayıcı pencerelerini hisse senedi fiyatları dalgalanan canlı stok tablogörüntülemek görürsünüz.

1. Araç çubuğunda, **Komut Dosyası Hata Ayıklama'yı** açın ve uygulamayı Hata Ayıklama modunda çalıştırmak için oynat düğmesini seçin.

    ![Hata ayıklama modunu ve oynat'ı seçen kullanıcının ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    **Canlı Stok Tablosunu**gösteren bir tarayıcı penceresi açılır. Stok tablosu başlangıçta "yükleme" gösterir. satır, daha sonra, kısa bir süre sonra, uygulama ilk hisse senedi verilerini gösterir ve sonra hisse senedi fiyatları değişmeye başlar.

1. URL'yi tarayıcıdan kopyalayın, diğer iki tarayıcıyı açın ve URL'leri adres çubuklarına yapıştırın.

    İlk stok ekranı ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.

1. Tüm tarayıcıları kapatın, yeni bir tarayıcı açın ve aynı URL'ye gidin.

    StockTicker singleton nesnesi sunucuda çalıştırmaya devam etti. **Canlı Stok Tablosu** hisse senetlerinin değişmeye devam ettiğini göstermektedir. İlk tabloyu sıfır değişiklik rakamlarıyla göremezsin.

1. Tarayıcıyı kapatın.

## <a name="enable-logging"></a>Günlü kaydını etkinleştir

SignalR, istemcinin sorun gidermede yardımcı olmasını etkinleştirebileceğiniz yerleşik bir günlük işlevine sahiptir. Bu bölümde, signalr'in aşağıdaki aktarım yöntemlerinden hangisini kullandığını günlüklerin size nasıl söylediğini gösteren günlük günlüğe kaydetmeyi ve örnekleri görebilirsiniz:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.

* Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar.](http://en.wikipedia.org/wiki/Server-sent_events)

* [Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer tarafından desteklenir.

* [Ajax uzun yoklama,](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)tüm tarayıcılar tarafından desteklenir.

Herhangi bir bağlantı için SignalR, hem sunucunun hem de istemcinin desteklediği en iyi aktarım yöntemini seçer.

1. Açık *StockTicker.js*.

1. Dosyanın sonundaki bağlantıyı açan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bu vurgulanmış kod satırını ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Projeyi çalıştırmak için **F5** tuşuna basın.

1. Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için Konsol'u seçin. SignalR'ın yeni bir bağlantı için aktarım yöntemini müzakere eden günlüklerini görmek için sayfayı yenilemeniz gerekebilir.

    * Windows 8'de (IIS 8) Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **WebSockets'tir.**

    * Windows 7'de (IIS 7.5) Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **iframe'dir.**

    * Windows 8'de Firefox 19 çalıştırıyorsanız (IIS 8), aktarım yöntemi **WebSockets'tir.**

        > [!TIP]
        > Firefox'ta, Konsol penceresi almak için Firebug eklentisini yükleyin.

    * Firefox 19'u Windows 7'de (IIS 7.5) çalıştırıyorsanız, aktarım yöntemi **sunucu tarafından gönderilen** olaylardır.

## <a name="install-the-stockticker-sample"></a>StockTicker örneğini yükleyin

[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker uygulamasını yükler. NuGet paketi, sıfırdan oluşturduğunuz basitleştirilmiş sürümden daha fazla özellik içerir. Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.

> [!IMPORTANT]
> Paketi bu öğreticinin önceki adımlarını gerçekleştirmeden yüklerseniz, projenize bir OWIN başlangıç sınıfı eklemeniz gerekir. NuGet paketi için bu readme.txt dosyası bu adımı açıklar.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR.Sample NuGet paketini yükleyin

1. **Çözüm Gezgini'nde**projeyi sağ tıklatın ve **NuGet Paketlerini Yönet'i**seçin.

1. **NuGet Paket yöneticisi: SignalR.StockTicker**, **Gözat**seçin .

1. **Paket kaynağından**, **nuget.org**seçin.

1. Arama kutusuna *SignalR.Sample* girin ve **Microsoft.AspNet.SignalR.Sample** > **Install'ı**seçin.

1. **Solution Explorer'da** *SignalR.Sample* klasörünü genişletin.

    SignalR.Sample paketinin yüklenmesi klasörü ve içeriğini oluşturdu.

1. *SignalR.Sample* klasöründe *StockTicker.html'e*sağ tıklayın ve ardından **Başlangıç Sayfası Olarak Ayarla'yı**seçin.

    > [!NOTE]
    > SignalR.Sample NuGet paketinin *yüklenmesi, Komut Dosyaları* klasörünüzde bulunan jQuery sürümünü değiştirebilir. Paketin *SignalR.Sample* klasörüne yükleştirdiği yeni *StockTicker.html* dosyası, paketin yükettiği jQuery sürümüyle senkronize olacaktır, ancak orijinal *StockTicker.html* dosyanızı yeniden çalıştırmak istiyorsanız, önce komut dosyası etiketindeki jQuery başvurularını güncelleştirmeniz gerekebilir.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

 İlk uygulamada gördüğünüz tabloyararlı özelliklere sahipti. Tam stok işaretleyici uygulaması yeni özellikler gösterir: hisse senedi verilerini ve yükseldikçe ve düştükçe renk değiştiren hisse senetlerini gösteren yatay kaydırma penceresi.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.

     Uygulamayı ilk kez çalıştırdığınızda, "pazar" "kapalı" dır ve kaydırma olmayan statik bir tablo ve işaretleyici penceresi görürsünüz.

1. **Açık Pazar'ı**seçin.

    ![Canlı işaretleyicinin ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **Canlı Stok Ticker** kutusu yatay olarak kaydırmaya başlar ve sunucu hisse senedi fiyat değişikliklerini düzenli olarak rasgele olarak yayınlamaya başlar.

    * Her zaman bir hisse senedi fiyatı değişir, uygulama hem **Live Stock Table** ve Live **Stock Ticker**günceller.

    * Bir hisse senedinin fiyat değişikliği pozitif olduğunda, uygulama yeşil arka plana sahip hisse senedini gösterir.

    * Değişiklik negatif olduğunda, uygulama kırmızı arka planlı hisse senedini gösterir.

1. **Pazarkapat'ı**seçin.

    * Tablo güncelleştirmeleri durur.

    * İşaretleyici kaydırmayı durdurur.

1. **Sıfırla**’yı seçin.

    * Tüm stok verileri sıfırlanır.

    * Uygulama, fiyat değişiklikleri başlamadan önce ilk durumu geri yüklenir.

1. URL'yi tarayıcıdan kopyalayın, diğer iki tarayıcıyı açın ve URL'leri adres çubuklarına yapıştırın.

1. Her tarayıcıda aynı anda dinamik olarak güncellenen aynı verileri görürsünüz.

1. Denetimlerden herhangi birini seçtiğinizde, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.

### <a name="live-stock-ticker-display"></a>Canlı Hayvan Ticker ekran

**Canlı Stok Ticker** ekranı, CSS `<div>` stilleri tarafından tek bir satıra biçimlendirilmiş bir öğedeki sıralanmamış bir listedir. Uygulama, işaretleyiciyi tabloyla aynı şekilde başolarak algılar ve güncelleştirir: `<li>` bir şablon dizesinde yer tutucuları değiştirerek ve `<li>` öğeleri öğeye `<ul>` dinamik olarak ekleyerek. Uygulama içinde sıralanmamış listenin `animate` kenar boşluğu sol değiştirmek için jQuery işlevini `<div>`kullanarak kaydırma içerir.

#### <a name="signalrsample-stocktickerhtml"></a>SignalR.Sample StockTicker.html

Stok işaretleyici HTML kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR.Sample StockTicker.css

Stok işaretçisi CSS kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR.Sample SignalR.StockTicker.js

Kaydırma yapan jQuery kodu:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>İstemcinin çağırabileceği sunucudaki ek yöntemler

Uygulamaya esneklik eklemek için, uygulamanın çağırabileceği ek yöntemler vardır.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR.Sample StockTickerHub.cs

Sınıf, `StockTickerHub` istemcinin çağırabileceği dört ek yöntem tanımlar:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Uygulama, `OpenMarket`sayfanın `Reset` üst kısmındaki düğmelere yanıt olarak ve çağırır. `CloseMarket` Bunlar, bir istemcinin durumunda bir değişikliği tetikleyen deseni hemen tüm istemcilere yayılır şekilde gösterir. Bu yöntemlerin her `StockTicker` biri, sınıf içinde piyasa durumunun değişmesine neden olan bir yöntem çağırır ve ardından yeni durumu yayınlar.

#### <a name="signalrsample-stocktickercs"></a>SignalR.Sample StockTicker.cs

`StockTicker` Uygulamada, uygulama `MarketState` enum değeri döndüren bir `MarketState` özellik ile piyasanın durumunu korur:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Sınıf iş parçacığı güvenli olması gerekir, çünkü `StockTicker` pazar durumunu değiştirmek yöntemlerin her biri bir kilit bloğu içinde bunu:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Bu kodun iş parçacığı için `_marketState` güvenli olduğundan emin `MarketState` olmak `volatile`için, atanan özelliği destekleyen alan:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

İstemcide `BroadcastMarketStateChange` tanımlanan farklı yöntemleri çağırmaları dışında, yöntemler ve `BroadcastMarketReset` yöntemler, önceden gördüğünüz BroadcastStockPrice yöntemine benzer:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Sunucunun çağırabileceği istemcideki ek işlevler

İşlev `updateStockPrice` şimdi hem tabloyu hem de işaretçi `jQuery.Color` ekranını işler ve kırmızı ve yeşil renkleri yanıp sönmek için kullanır.

*SignalR.StockTicker.js'deki yeni işlevler,* piyasa durumuna göre düğmeleri etkinleştirebilir ve devre dışı eder. Ayrıca Live Stock **Ticker** yatay kaydırma durdurmak veya başlatmak. Birçok fonksiyon eklenmektedir `ticker.client`bu yana, uygulama bunları eklemek için [jQuery genişletmek işlevini](http://api.jquery.com/jQuery.extend/) kullanır.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Bağlantıyı kurduktan sonra ek istemci kurulumu

İstemci bağlantıyı kurduktan sonra, yapması gereken bazı ek işler vardır:

* Uygun `marketOpened` veya `marketClosed` işlevi aramak için piyasanın açık mı kapalı mı yoksa kapalı mı olduğunu öğrenin.

* Sunucu yöntemi çağrılarını düğmelere takın.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Sunucu yöntemleri, uygulama bağlantıyı kurana kadar düğmelere bağlı değildir. Bu, kodun kullanılabilir olmadan önce sunucu yöntemlerini arayamaabilmesi içindir.

## <a name="additional-resources"></a>Ek kaynaklar

Bu eğitimde, sunucudan tüm bağlı istemcilere ileti yayınlayan bir SignalR uygulamasını programlamayı öğrendiniz. Artık iletileri periyodik olarak ve herhangi bir istemciden gelen bildirimlere yanıt olarak yayınlayabilirsiniz. Çok oyunculu çevrimiçi oyun senaryolarında sunucu durumunu korumak için çok iş parçacığı singleton örneği kavramını kullanabilirsiniz. Örneğin, [SignalR tabanlı ShootR oyununa](https://github.com/NTaylorMullen/ShootR)bakın.

Eşler arası iletişim senaryolarını gösteren öğreticiler için [SignalR ile Başlarken](introduction-to-signalr.md) ve [SignalR ile Gerçek Zamanlı Güncelleme](tutorial-high-frequency-realtime-with-signalr.md)bölümüne bakın.

SignalR hakkında daha fazla şey için aşağıdaki kaynaklara bakın:

* [ASP.NET SignalR](../../index.md)
* [SignalR Projesi](http://signalr.net/)
* [Sinyalci GitHub ve Örnekler](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Proje oluşturuldu
> * Sunucu kodunu ayarlama
> * Sunucu kodu incelendi
> * İstemci kodunu ayarlama
> * İstemci kodu incelendi
> * Uygulamayı test etme
> * Etkin günlük

SignalR 2'yi ASP.NET kullanan gerçek zamanlı bir web uygulamasının nasıl oluşturulabildiğini öğrenmek için bir sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [SignalR ile gerçek zamanlı web uygulaması oluşturun](real-time-web-applications-with-signalr.md)
