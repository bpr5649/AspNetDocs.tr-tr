---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Öğretici: SignalR 2 ile sunucu yayını | Microsoft Docs'
author: tdykstra
description: Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345603"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Öğretici: SignalR 2 ile sunucu yayını

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Sunucu yayını, sunucunun istemcilere gönderilen iletişimleri başlattığı anlamına gelir.

Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir stok Ticker benzetimini yapar. Düzenli aralıklarla, sunucu stok fiyatlarını rastgele güncelleştirir ve güncelleştirmeleri tüm bağlı istemcilere yayınlar. Tarayıcıda, **değişiklik** ve sütunlardaki sayılar ve semboller, **%** sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir. Aynı URL 'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.

![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Proje oluşturma
> * Sunucu kodunu ayarlama
> * Sunucu kodunu inceleyin
> * İstemci kodunu ayarlama
> * İstemci kodunu inceleme
> * Uygulamayı test edin
> * Günlü kaydını etkinleştir

> [!IMPORTANT]
> Uygulamayı oluşturma adımları boyunca çalışmak istemiyorsanız, SignalR. Sample paketini yeni bir boş ASP.NET Web uygulaması projesine yükleyebilirsiniz. NuGet paketini bu öğreticideki adımları uygulamadan yüklerseniz, *readme.txt* dosyadaki yönergeleri izlemelisiniz. Paketi çalıştırmak için, yüklü paketteki yöntemi çağıran bir OWıN başlangıç sınıfı eklemeniz gerekir `ConfigureSignalR` . OWıN başlangıç sınıfını eklememanız durumunda bir hata alırsınız. Bu makalenin [StockTicker örneğini Install](#install-the-stockticker-sample) bölümüne bakın.

## <a name="prerequisites"></a>Ön koşullar

* **ASP.NET ve web geliştirme** iş yüküyle [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).

## <a name="create-the-project"></a>Proje oluşturma

Bu bölümde, Visual Studio 2017 ' ın boş bir ASP.NET Web uygulaması oluşturmak için nasıl kullanılacağı gösterilmektedir.

1. Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.

    ![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. **Yeni ASP.NET Web uygulaması-SignalR. StockTicker** penceresinde **boş** bırakın ve **Tamam**' ı seçin.

## <a name="set-up-the-server-code"></a>Sunucu kodunu ayarlama

Bu bölümde, sunucuda çalışan kodu ayarlarsınız.

### <a name="create-the-stock-class"></a>Hisse senedi sınıfını oluşturma

Bir hisse senedi hakkındaki bilgileri depolamak ve aktarmak için kullanacağınız *Stok* modeli sınıfını oluşturarak başlarsınız.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**.

1. Sınıfı *stoğa* adlandırın ve projeye ekleyin.

1. *Stock.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Hisse senetleri oluştururken ayarlayacağımız iki özellik `Symbol` (örneğin, Microsoft IÇIN MSFT) ve `Price` . Diğer özellikler, nasıl ve ne zaman ayarlandığınıza bağlıdır `Price` . İlk kez ayarlandığında `Price` değer değerine yayılır `DayOpen` . Bundan sonra uygulama, ve `Price` `Change` `PercentChange` özellik değerlerini ve arasındaki farka göre hesaplar `Price` `DayOpen` .

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>StockTickerHub ve StockTicker sınıfları oluşturma

Sunucudan istemciye etkileşimi işlemek için SignalR hub API 'sini kullanırsınız. `StockTickerHub`SignalR sınıfından türetilen bir sınıf, `Hub` istemcilerden gelen bağlantıları ve Yöntem çağrılarını almayı işleymeyecektir. Ayrıca, stok verilerini korumanız ve bir nesnesi çalıştırmanız gerekir `Timer` . `Timer`Nesne, istemci bağlantılarından bağımsız olarak fiyat güncelleştirmelerini tetikleyecektir. `Hub`Hub 'lar geçici olduğundan bu işlevleri bir sınıfa koyamazsınız. Uygulama, `Hub` hub üzerindeki her görev için, istemcilerden sunucuya bağlantılar ve çağrılar gibi bir sınıf örneği oluşturur. Bu nedenle, stok verilerini tutan, fiyatları güncelleştiren ve fiyat güncelleştirmelerinin yayınlarından oluşan mekanizmanın ayrı bir sınıfta çalışması gerekir. Sınıfını adlandırın `StockTicker` .

![StockTicker 'den yayımlama](tutorial-server-broadcast-with-signalr/_static/image3.png)

Yalnızca bir sınıfın bir örneğinin `StockTicker` sunucuda çalıştırılmasını istiyorsunuz, bu nedenle her örnekten tek örneğe bir başvuru ayarlamanız gerekir `StockTickerHub` `StockTicker` . `StockTicker`Hisse senedi verileri olduğundan ve güncelleştirmeleri tetiklediği, ancak `StockTicker` bir sınıf olmadığı için, sınıfı istemcilere yayınlayacak `Hub` . `StockTicker`Sınıfı, SignalR hub bağlantı bağlamı nesnesine bir başvuru almak için sahiptir. Daha sonra, istemcilere yayımlamak için SignalR bağlantı bağlamı nesnesini kullanabilir.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs oluştur

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin.

1. **Add New Item-SignalR. StockTicker**' da, **yüklü**  >  **Visual C#**  >  **Web**  >  **SignalR** ' yi seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.

1. Sınıfı *StockTickerHub* olarak adlandırın ve projeye ekleyin.

    Bu adım *StockTickerHub.cs* sınıf dosyasını oluşturur. Aynı anda, bir dizi betik dosyası ve proje için SignalR 'yi destekleyen derleme başvuruları ekler.

1. *StockTickerHub.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Dosyayı kaydedin.

Uygulama, istemcilerin sunucuda çağırabilmesine yönelik yöntemleri tanımlamak için [hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfını kullanır. Bir yöntem tanımlanıyor: `GetAllStocks()` . Bir istemci sunucuya ilk kez bağlandığında, geçerli fiyatlarına sahip tüm hisse senetleri listesini almak için bu yöntemi çağırır. Yöntemi zaman uyumlu olarak çalışabilir ve bellekten veri döndürdüğü için döndürebilir `IEnumerable<Stock>` .

Bir veritabanı araması veya bir Web hizmeti çağrısı gibi beklenmek üzere, yöntemin verileri alması gerekiyorsa, `Task<IEnumerable<Stock>>` zaman uyumsuz işlemeyi etkinleştirmek için dönüş değeri olarak belirtmeniz gerekir. Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-zaman uyumsuz olarak yürütülecektir](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

`HubName`Özniteliği, uygulamanın, Istemcideki JavaScript kodunda hub 'a nasıl başvurulacağını belirtir. İstemci üzerindeki varsayılan ad bu özniteliği kullanmıyorsanız, sınıf adının bir camelCase sürümüdür ve bu durumda olacaktır `stockTickerHub` .

Daha sonra `StockTicker` sınıfı oluşturduğunuzda, uygulama statik özelliğinde bu sınıfın tek bir örneğini oluşturur `Instance` . Bu tek örneği `StockTicker` , kaç istemcinin bağlanıp bağlantısı kesildiğine bakılmaksızın bellekte bulunur. Bu örnek, `GetAllStocks()` yöntemin geçerli stok bilgilerini döndürmek için kullandığı şeydir.

#### <a name="create-stocktickercs"></a>StockTicker.cs oluştur

1. **Çözüm Gezgini**, projeye sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**.

1. Sınıfı *StockTicker* olarak adlandırın ve projeye ekleyin.

1. *StockTicker.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Tüm iş parçacıkları StockTicker Code 'un aynı örneğini çalıştırdığından, StockTicker sınıfının iş parçacığı açısından güvenli olması gerekir.

### <a name="examine-the-server-code"></a>Sunucu kodunu inceleyin

Sunucu kodunu incelerseniz, uygulamanın nasıl çalıştığını anlamanıza yardımcı olur.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Tek örneği statik bir alanda depolama

Kod, `_instance` `Instance` özelliği sınıfın bir örneğiyle yedekleyen statik alanı başlatır. Oluşturucu özel olduğundan, sınıfın, uygulamanın oluşturabileceğinden tek örneğidir. Uygulama, alan için [yavaş başlatma](/dotnet/framework/performance/lazy-initialization) kullanır `_instance` . Performans nedenleriyle bu değildir. Örnek oluşturmanın iş parçacığı açısından güvenli olduğundan emin olmak.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

İstemci sunucuya her bağlanışında, ayrı bir iş parçacığında çalışan StockTickerHub sınıfının yeni bir örneği, `StockTicker.Instance` sınıfında daha önce gördüğünüz gibi, static özelliğinden StockTicker Singleton örneğini alır `StockTickerHub` .

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Bir ConcurrentDictionary içinde hisse senedi verilerini depolama

Oluşturucu, `_stocks` koleksiyonu bazı örnek hisse senedi verileri ile başlatır ve `GetAllStocks` hisse senetleri döndürür. Daha önce gördüğünüz gibi, bu hisse senedi koleksiyonu tarafından `StockTickerHub.GetAllStocks` , `Hub` istemcilerin çağırabileceği sınıfta bir sunucu yöntemi olan tarafından döndürülür.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Hisse senetleri koleksiyonu, iş parçacığı güvenliği için bir [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır. Alternatif olarak, bir [Sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve üzerinde değişiklik yaptığınızda sözlüğü açıkça kilitleyemezsiniz.

Bu örnek uygulama için uygulama verilerini bellekte depolamak ve uygulama örneği olmadığında verileri kaybetmek için Tamam  `StockTicker` . Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposuyla çalışırsınız.

#### <a name="periodically-updating-stock-prices"></a>Stok fiyatlarını düzenli olarak güncelleştirme

Oluşturucu, `Timer` stok fiyatlarını rastgele olarak güncelleştiren yöntemleri düzenli aralıklarla çağıran bir nesne başlatır.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer``UpdateStockPrices`durum parametresinde null değeri geçen çağrılar. Fiyatlar güncelleştirilmeden önce uygulama, nesne üzerinde bir kilit alır `_updateStockPricesLock` . Kod, başka bir iş parçacığının fiyatları güncelleştirme olup olmadığını denetler ve ardından `TryUpdateStockPrice` listedeki her bir stoğa çağrı yapılır. `TryUpdateStockPrice`Yöntemi, stok fiyatının değiştirilip değişmeyeceğine ve ne kadarının değiştirileceğini belirler. Stok fiyatı değişirse, uygulama `BroadcastStockPrice` Stok fiyatı değişikliğini tüm bağlı istemcilere yayınlamak için çağırır.

`_updatingStockPrices`Bu bayrak, iş parçacığı açısından güvenli olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak belirlenmiş.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

Gerçek bir uygulamada, `TryUpdateStockPrice` yöntemi fiyatı aramak için bir Web hizmeti çağırır. Bu kodda, uygulama, değişiklikleri rastgele yapmak için rastgele bir sayı Oluşturucu kullanır.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker sınıfının istemcilere yayınlanabilmesi için SignalR bağlamı alma

Fiyat değişiklikleri nesnede yer aldığı için `StockTicker` , bu, `updateStockPrice` tüm bağlı istemcilerde bir yöntemi çağırması gereken nesnedir. Bir `Hub` sınıfında, istemci yöntemlerini çağırmak için BIR API 'si vardır, ancak `StockTicker` sınıfından türemez `Hub` ve herhangi bir nesneye başvuruya sahip olmaz `Hub` . Bağlı istemcilere yayımlamak için, sınıfın, `StockTicker` sınıfa yönelik SignalR bağlam örneğini alması `StockTickerHub` ve istemcileri üzerinde yöntemleri çağırmak için kullanması gerekir.

Kod, tek sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya geçirir ve Oluşturucu onu `Clients` özelliğine koyar.

Bağlamı yalnızca bir kez almak istediğiniz iki neden vardır: bağlamı almak pahalı bir görevdir ve bir kez alınması, uygulamanın istemcilere gönderilen iletilerin amaçlanan sırasını koruyabilmesine olanak sağlar.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

`Clients`Bağlam özelliğinin alınması ve özelliğe yerleştirilmesi, `StockTickerClient` bir sınıfta olduğu gibi görünen istemci yöntemlerini çağırmak için kod yazmanıza olanak tanır `Hub` . Örneğin, yazabileceğiniz tüm istemcilere yayımlamak için `Clients.All.updateStockPrice(stock)` .

`updateStockPrice`İçinde aradığınız Yöntem `BroadcastStockPrice` henüz yok. Daha sonra, istemcide çalışan bir kod yazdığınızda eklersiniz. `updateStockPrice` `Clients.All` Dinamik olduğundan, uygulamanın, çalışma zamanında ifadeyi değerlendileceğini gösterdiği için buraya başvurabilirsiniz. Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve istemcinin adlı bir yöntemi varsa `updateStockPrice` , uygulama bu yöntemi çağırır ve parametre değerini bu yönteme iletir.

`Clients.All` tüm istemcilere gönderme anlamına gelir. SignalR, hangi istemcileri veya istemci gruplarını gönderileceğini belirtmek için size diğer seçenekler sağlar. Daha fazla bilgi için bkz. [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>SignalR rotasını kaydetme

Sunucunun hangi URL 'yi ele geçirip SignalR 'ye yönlendireceğimizi bilmeleri gerekir. Bunu yapmak için bir OWıN başlangıç sınıfı ekleyin:

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin.

1. **Yeni öğe Ekle-SignalR. StockTicker** **yüklü**  >  **Visual C#**  >  **Web** ' i seçin ve ardından **owın başlangıç sınıfı**' nı seçin.

1. Sınıfın *başlangıcını* adlandırın ve **Tamam**' ı seçin.

1. *Startup.cs* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Artık sunucu kodunu ayarlamayı tamamladınız. Sonraki bölümde, istemcisini ayarlayacaksınız.

## <a name="set-up-the-client-code"></a>İstemci kodunu ayarlama

Bu bölümde, istemcisinde çalışan kodu ayarlarsınız.

### <a name="create-the-html-page-and-javascript-file"></a>HTML sayfası ve JavaScript dosyası oluşturma

HTML sayfasında veriler görüntülenir ve JavaScript dosyası verileri düzenler.

#### <a name="create-stocktickerhtml"></a>StockTicker.html oluştur

İlk olarak, HTML istemcisini eklersiniz.

1. **Çözüm Gezgini**' de projeye sağ tıklayın ve **Add**  >  **HTML sayfası**Ekle ' yi seçin.

1. Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.

1. *StockTicker.html* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML, beş sütun, üst bilgi satırı ve beş sütuna yayılan tek bir hücre içeren bir veri satırı içeren bir tablo oluşturur. Veri satırında "yükleniyor..." görüntülenir uygulama başladığında anlık olarak. JavaScript kodu, bu satırı kaldırır ve kendi yerleştirme satırlarına sunucudan alınan stok verilerini ekler.

    Komut dosyası etiketleri şunları belirtir:

    * JQuery betik dosyası.

    * SignalR çekirdek betik dosyası.

    * SignalR proxy 'leri betik dosyası.

    * Daha sonra oluşturacağınız bir StockTicker betik dosyası.

    Uygulama, SignalR proxy 'leri betik dosyasını dinamik olarak oluşturur. "/SignalR/hub 'ları" URL 'sini belirtir ve bu örnekte, için hub sınıfındaki yöntemler için proxy yöntemlerini tanımlar `StockTickerHub.GetAllStocks` . İsterseniz, [SignalR yardımcı programlarını](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)kullanarak bu JavaScript dosyasını el ile oluşturabilirsiniz. Yöntem çağrısında dinamik dosya oluşturmayı devre dışı bırakmayı unutmayın `MapHubs` .

1. **Çözüm Gezgini**' de **betikler**' ı genişletin.

    JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yükler.

1. Kod bloğundaki betik başvurularını projedeki betik dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.

1. **Çözüm Gezgini**' de, *StockTicker.html*öğesine sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.

#### <a name="create-stocktickerjs"></a>StockTicker.js oluştur

Şimdi JavaScript dosyasını oluşturun.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **JavaScript dosyası**Ekle ' yi seçin.

1. Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.

1. Bu kodu *StockTicker.js* dosyasına ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>İstemci kodunu inceleme

İstemci kodunu incelerseniz, istemci kodunun, uygulamayı çalışır hale getirmek için sunucu koduyla nasıl etkileşime gireceğini öğrenirsiniz.

#### <a name="starting-the-connection"></a>Bağlantı başlatılıyor

`$.connection` SignalR proxy 'leri anlamına gelir. Kod, sınıf için proxy 'ye bir başvuru alır `StockTickerHub` ve `ticker` değişkenine koyar. Proxy adı, öznitelik tarafından ayarlanan addır `HubName` :

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Tüm değişkenleri ve işlevleri tanımladıktan sonra, dosyadaki kodun son satırı, SignalR işlevini çağırarak SignalR bağlantısını başlatır `start` . `start`İşlev zaman uyumsuz olarak yürütülür ve [jQuery ertelenmiş nesnesini](http://api.jquery.com/category/deferred-object/)döndürür. Uygulama zaman uyumsuz eylemi bitirdiğinde çağrılacak işlevi belirtmek için bitti işlevini çağırabilirsiniz.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Tüm stokları alma

`init`İşlevi, `getAllStocks` sunucuda işlevini çağırır ve sunucunun stok tablosunu güncelleştirmek için döndürdüğü bilgileri kullanır. Varsayılan olarak, yöntem adı sunucuda Pascal-cased olsa da, istemci üzerinde Camelbüyük harfleri kullanmanız gerektiğini unutmayın. Camelphı kuralı yalnızca yöntemlere uygulanır, nesneleri değil. Örneğin, `stock.Symbol` ve ' a başvurursunuz `stock.Price` `stock.symbol` `stock.price` .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

`init`Yönteminde, uygulama, `formatStock` nesnenin özelliklerini biçimlendirme ' ye çağırarak `stock` ve sonra `supplant` `rowTemplate` değişkendeki yer tutucuları nesne özelliği değerleriyle değiştirmek için çağırarak, `stock` sunucudan alınan her bir stok NESNESI için bir tablo satırı için HTML oluşturur. Elde edilen HTML daha sonra hisse senedi tablosuna eklenir.

> [!NOTE]
> Öğesini `init` `callback` zaman uyumsuz işlev bittikten sonra yürüten bir işlev olarak geçirerek çağırın `start` . Çağrıldıktan `init` sonra ayrı bir JavaScript açıklaması olarak çağrılırsa `start` , başlangıç işlevinin bağlantıyı kurmayı bitirmesini beklemeden hemen çalıştırılacağından işlev başarısız olur. Bu durumda, işlev, `init` `getAllStocks` uygulama bir sunucu bağlantısı oluşturmadan önce işlevi çağırmaya çalışır.

#### <a name="getting-updated-stock-prices"></a>Güncelleştirilmiş Stok fiyatları alma

Sunucu bir hisse senedi fiyatını değiştirdiğinde, `updateStockPrice` bağlı istemcileri çağırır. Uygulama, `stockTicker` sunucudan çağrılarla kullanılabilir hale getirmek için, işlevini proxy 'nin istemci özelliğine ekler.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice`İşlevi, sunucudan alınan bir stok nesnesini, işlevle aynı şekilde bir tablo satırına biçimlendirir `init` . Satırı tabloya eklemek yerine, stoktaki geçerli satırını bulur ve bu satırı yeni bir satır ile değiştirir.

## <a name="test-the-application"></a>Uygulamayı test edin

Çalıştığından emin olmak için uygulamayı test edebilirsiniz. Tüm tarayıcı pencerelerinin, hisse senedi fiyatları dalgalanarak canlı hisse senedi tablosunu görüntülemesini görürsünüz.

1. Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından uygulamayı hata ayıklama modunda çalıştırmak için Yürüt düğmesini seçin.

    ![Kullanıcı hata ayıklama modunu açıp oynat 'ı seçen kullanıcının ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    **Canlı hisse senedi tablosunu**görüntüleyen bir tarayıcı penceresi açılacaktır. Hisse senedi tablosu başlangıçta "yükleniyor..." ardından, kısa bir süre sonra, uygulama ilk stok verilerini gösterir ve stok fiyatları değişme başlar.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

    İlk stok görüntüsü ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.

1. Tüm tarayıcıları kapatın, yeni bir tarayıcı açın ve aynı URL 'ye gidin.

    StockTicker Singleton nesnesi sunucuda çalışmaya devam ediyor. **Canlı hisse senedi tablosu** , hisse senedinin değişmeye devam etseyi gösterir. Sıfır değişiklik rakamlarını içeren ilk tabloyu görmezsiniz.

1. Tarayıcıyı kapatın.

## <a name="enable-logging"></a>Günlü kaydını etkinleştir

SignalR 'de, sorun gidermeye yardımcı olmak için istemcisinde etkinleştirebilmeniz gereken yerleşik bir günlüğe kaydetme işlevi vardır. Bu bölümde, günlüğe kaydetmeyi etkinleştirir ve günlüklerin, SignalR aşağıdaki taşıma yöntemlerinden hangisini kullandığını nasıl söyletiğini gösteren örneklere bakabilirsiniz:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.

* Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar](http://en.wikipedia.org/wiki/Server-sent_events).

* Internet Explorer tarafından desteklenen [süresiz çerçeve](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe).

* Tüm tarayıcılar tarafından desteklenen [Ajax uzun yoklama](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).

Verilen herhangi bir bağlantı için, SignalR hem sunucu hem de istemci tarafından desteklenen en iyi taşıma yöntemini seçer.

1. *StockTicker.js*açın.

1. Dosyanın sonunda bağlantıyı başlatan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bu vurgulanmış kod satırını ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Projeyi çalıştırmak için **F5** tuşuna basın.

1. Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için konsolu seçin. Yeni bir bağlantı için taşıma yöntemiyle ilgili olarak, SignalR 'nin işlem için anlaşmasının günlüklerini görmek üzere sayfayı yenilemeniz gerekebilir.

    * Windows 8 (IIS 8) üzerinde Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.

    * Windows 7 ' de (IIS 7,5) Internet Explorer 10 çalıştırıyorsanız, taşıma yöntemi **iframe**'dir.

    * Windows 8 (IIS 8) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.

        > [!TIP]
        > Firefox 'ta, bir konsol penceresi almak için Firebug eklentisini yüklersiniz.

    * Windows 7 (IIS 7,5) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **sunucu tarafından gönderilen** olaylardır.

## <a name="install-the-stockticker-sample"></a>StockTicker örneğini yükler

[Microsoft. Aspnet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) , StockTicker uygulamasını yüklüyor. NuGet paketi sıfırdan oluşturduğunuz Basitleştirilmiş sürümden daha fazla özellik içerir. Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.

> [!IMPORTANT]
> Bu öğreticinin önceki adımlarını gerçekleştirmeden paketi yüklerseniz, projenize bir OWıN başlangıç sınıfı eklemeniz gerekir. NuGet paketi için bu readme.txt dosyası bu adımı açıklamaktadır.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR. Sample NuGet paketini yükler

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.

1. **NuGet Paket Yöneticisi: SignalR. StockTicker**' de, **Araştır**' ı seçin.

1. **Paket kaynağından** **NuGet.org**öğesini seçin.

1. Arama kutusuna *SignalR. Sample* girin ve **Microsoft. Aspnet. SignalR. Sample**  >  **Install**' ı seçin.

1. **Çözüm Gezgini**, *SignalR. Sample* klasörünü genişletin.

    SignalR. Sample paketini yükleme, klasörü ve içeriğini oluşturdu.

1. *SignalR. Sample* klasöründe, *StockTicker.html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.

    > [!NOTE]
    > SignalR. Sample NuGet paketini yükleme, *Scripts* klasörünüzdeki jQuery sürümünü değiştirebilir. Paketin *SignalR. Sample* klasörüne yüklediği yeni *StockTicker.html* dosyası, paketin yüklediği jQuery sürümüyle eşitlenmiş olacaktır, ancak özgün *StockTicker.html* dosyanızı yeniden çalıştırmak Istiyorsanız, önce komut dosyası etiketinde jQuery başvurusunu güncelleştirmeniz gerekebilir.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

 İlk uygulamada gördüğünüz tablo yararlı özelliklere sahipti. Tam hisse senedi oluşturma uygulaması yeni özellikleri gösterir: bir yatay kaydırma penceresi, renkleri arttığında ve düşecek şekilde değişen hisse senedi verilerini ve stokları gösterir.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.

     Uygulamayı ilk kez çalıştırdığınızda, "Pazar" "kapalı" olur ve kaydırılmayan bir statik tablo ve bir Ticker penceresi görürsünüz.

1. **Açık Pazar**' ı seçin.

    ![Canlı Ticker 'ın ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **Canlı hisse senedi bandı** , yatay olarak kaydırmaya başlar ve sunucu düzenli olarak stok fiyatı değişikliklerini rastgele bir şekilde yayınlar.

    * Bir stok fiyatı her değiştiğinde uygulama hem **canlı hisse senedi tablosunu** hem de **canlı hisse senedi bandı**' ni güncelleştirir.

    * Bir hisse senedinin fiyat değişikliği pozitif olduğunda, uygulama stoku yeşil bir arka plana gösterir.

    * Değişiklik negatifse, uygulama, stoku kırmızı bir arka plana gösterir.

1. **Pazara kapat**' ı seçin.

    * Tablo güncelleştirmeleri durdu.

    * Ticker, kaydırmayı durduruyor.

1. **Sıfırla**’yı seçin.

    * Tüm hisse senedi verileri sıfırlanır.

    * Uygulama, Fiyat değişikliklerinin başlatılmasından önce ilk durumu geri yükler.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

1. Aynı verileri her bir tarayıcıda dinamik olarak güncelleştirilmiş şekilde görürsünüz.

1. Denetimlerden herhangi birini seçtiğinizde, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.

### <a name="live-stock-ticker-display"></a>Canlı hisse şeridi görüntüleme

**Canlı hisse senedi bandı** EKRANı, `<div>` CSS stilleriyle tek bir satıra biçimlendirilen bir öğe içinde sıralanmamış bir listesidir. Uygulama başlatılır ve Ticker 'ı tabloyla aynı şekilde güncelleştirir: bir şablon dizesindeki yer tutucuları değiştirerek `<li>` ve öğeleri dinamik olarak `<li>` öğesine ekler `<ul>` . Uygulama `animate` , içindeki sıralanmamış listenin sol kenar boşluğunu değiştirmek Için jQuery işlevini kullanarak kaydırma içerir `<div>` .

#### <a name="signalrsample-stocktickerhtml"></a>SignalR. örnek StockTicker.html

Stock Ticker HTML kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR. Sample StockTicker. css

Hisse senedi bandı CSS kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR. Sample SignalR.StockTicker.js

Kaydırma yapan jQuery kodu:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Sunucuda istemcinin çağıra, ek Yöntemler

Uygulamaya esneklik eklemek için, uygulamanın çağırabilmesine ek yöntemler vardır.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR. Sample StockTickerHub.cs

`StockTickerHub`Sınıfı, istemcinin çağırabileceğini dört ek yöntem tanımlar:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Uygulama, `OpenMarket` `CloseMarket` , ve `Reset` sayfanın en üstündeki düğmelere yanıt olarak çağırır. Tüm istemcilere anında yayılmış durumdaki bir değişikliği tetikleyen bir istemcinin modelini gösterir. Bu yöntemlerin her biri, bir `StockTicker` sınıf içinde piyasa durumu değişikliğine neden olan bir yöntemi çağırır ve sonra yeni durumu yayınlar.

#### <a name="signalrsample-stocktickercs"></a>SignalR. Sample StockTicker.cs

`StockTicker`Sınıfında, uygulama `MarketState` bir sabit listesi değeri döndüren bir özellik ile Pazar durumunu korur `MarketState` :

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Pazar durumunu değiştiren yöntemlerin her biri, `StockTicker` sınıfın iş parçacığı açısından güvenli olması gerektiğinden bir kilit bloğunun içinde olur:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Bu kodun iş parçacığı açısından güvenli olduğundan emin olmak için, `_marketState` belirtilen özelliği yedekleyen alan `MarketState` `volatile` :

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`Ve `BroadcastMarketReset` yöntemleri, zaten gördüğünüz BroadcastStockPrice yöntemine benzerdir, ancak istemcide tanımlı farklı Yöntemler çağırır:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>İstemcinin çağıra, istemci üzerinde ek işlevler

`updateStockPrice`İşlev artık hem tabloyu hem de Ticker görüntüsünü işler ve `jQuery.Color` kırmızı ve yeşil renkleri Flash için kullanır.

*SignalR.StockTicker.js* yeni işlevler, Pazar durumuna göre düğmeleri etkinleştirir ve devre dışı bırakır. Ayrıca **canlı hisse senedi bandı** yatay kaydırmayı da durdurur veya başlatır. Uygulamasına birçok işlev eklendiğinden `ticker.client` , uygulama bunları eklemek Için [jQuery genişletme işlevini](http://api.jquery.com/jQuery.extend/) kullanır.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Bağlantı kurulduktan sonra ek istemci kurulumu

İstemci bağlantıyı belirledikten sonra, yapılacak bazı ek işler de vardır:

* Uygun veya işlevi çağırmak için pazar açık veya kapalı olduğunu öğrenin `marketOpened` `marketClosed` .

* Düğmelerine sunucu yöntemi çağrılarını ekleyin.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Sunucu yöntemleri, uygulama bağlantıyı yapana kadar düğmelere bağlı değildir. Bu, kodun kullanılabilir hale gelmeden önce sunucu yöntemlerine çağrı yapamıyor.

## <a name="additional-resources"></a>Ek kaynaklar

Bu öğreticide, sunucudan bağlı olan tüm istemcilere ileti veren bir SignalR uygulamasını nasıl programlayabilirsiniz. Artık iletileri düzenli aralıklarla ve herhangi bir istemciden gelen bildirimlere yanıt olarak yayınlayabilirsiniz. Çoklu iş parçacıklı tekil örnek kavramını kullanarak, çok oyunculu çevrimiçi oyun senaryolarında sunucu durumunu koruyabilirsiniz. Bir örnek için bkz. [SignalR tabanlı ShootR oyunu](https://github.com/NTaylorMullen/ShootR).

Eşler arası iletişim senaryolarını gösteren öğreticiler için bkz. [SignalR Ile çalışmaya](introduction-to-signalr.md) başlama ve [SignalR Ile gerçek zamanlı güncelleştirme](tutorial-high-frequency-realtime-with-signalr.md).

SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [ASP.NET SignalR](../../index.md)
* [SignalR projesi](http://signalr.net/)
* [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
* [SignalR wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Proje oluşturuldu
> * Sunucu kodunu ayarlama
> * Sunucu kodu incelendi
> * İstemci kodunu ayarlama
> * İstemci kodu incelendi
> * Uygulamayı test etme
> * Etkin günlük kaydı

ASP.NET SignalR 2 kullanan gerçek zamanlı bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [SignalR ile gerçek zamanlı web uygulaması oluşturma](real-time-web-applications-with-signalr.md)
