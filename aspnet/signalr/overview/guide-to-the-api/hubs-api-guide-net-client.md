---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hub'ları API Kılavuzu - .NET İstemci (C#) | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, Windows Mağazası (WinRT), WPF, Silverlight ve eksileri gibi .NET istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676337"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR Hub'ları API Kılavuzu - .NET İstemci (C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belge, Windows Mağazası (WinRT), WPF, Silverlight ve konsol uygulamaları gibi .NET istemcilerinde SignalR sürüm 2 için Hubs API'sinin kullanılmasına giriş sağlar.
>
> SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar. Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız. İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız. SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.
>
> SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar. SignalR, Hub'lar ve Kalıcı Bağlantılar'a giriş yapmak veya tam bir SignalR uygulamasının nasıl yapılacağını gösteren bir öğretici için [SignalR - Başlarken'](../getting-started/index.md)e bakın.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.
>
> ## <a name="questions-and-comments"></a>Sorular ve yorumlar
>
> Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.

## <a name="overview"></a>Genel Bakış

Bu belgede aşağıdaki bölümler yer alır:

- [İstemci Kurulumu](#clientsetup)
- [Bağlantı kurma](#establishconnection)

    - [Silverlight istemcilerinden etki alanı bağlantıları](#slcrossdomain)
- [Bağlantı nasıl yapılandırılabilen](#configureconnection)

    - [WPF istemcilerinde en fazla eşzamanlı bağlantı sayısı nasıl ayarlanır?](#maxconnections)
    - [Sorgu dize parametreleri nasıl belirtilir?](#querystring)
    - [Taşıma yöntemi nasıl belirtilir?](#transport)
    - [HTTP üstbilgi belirtme](#httpheaders)
    - [İstemci sertifikaları nasıl belirtilir?](#clientcertificate)
- [Hub proxy'si nasıl oluşturulur?](#proxy)
- [Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?](#callclient)

    - [Parametreleri olmayan yöntemler](#clientmethodswithoutparms)
    - [Parametre türlerini belirleyen parametrelerle ilgili yöntemler](#clientmethodswithparmtypes)
    - [Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler](#clientmethodswithdynamparms)
    - [Işleyici nasıl kaldırılır?](#removehandler)
- [İstemciden sunucu yöntemleri nasıl çağrılır?](#callserver)
- [Bağlantı ömrü olayları nasıl işler?](#connectionlifetime)
- [Hataları işleme](#handleerrors)
- [İstemci tarafı günlüğe kaydetmeyi etkinleştirme](#logging)
- [Sunucunun çağırabileceği istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri](#wpfsl)

Örnek .NET istemci projeleri için aşağıdaki kaynaklara bakın:

- [gustavo-armenta / SignalR-Örnekleri](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT, Silverlight, konsol uygulaması örnekleri).
- [DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com (WPF örnek).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Konsol uygulaması örneği).

Sunucu veya JavaScript istemcilerinin nasıl programlanır, aşağıdaki kaynaklara bakın:

- [SignalR Hub'lar API Kılavuzu - Sunucu](hubs-api-guide-server.md)
- [SignalR Hubs API Kılavuzu - JavaScript İstemci](hubs-api-guide-javascript-client.md)

API Başvuru konularına bağlantılar, API'nin .NET 4.5 sürümüne bağlantılardır. .NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.

<a id="clientsetup"></a>

## <a name="client-setup"></a>İstemci kurulumu

[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet paketini yükleyin [(Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) paketi değil). Bu paket, winrt, Silverlight, WPF, konsol uygulaması ve Windows Phone istemcilerini hem .NET 4 hem de .NET 4.5 için destekler.

İstemcide olan SignalR sürümü sunucudaki sürümden farklıysa, SignalR genellikle farka uyum sağlayabilir. Örneğin, SignalR sürüm 2'yi çalıştıran bir sunucu, 1.1.x yüklü istemcilerin yanı sıra sürüm 2 yüklü istemcileri destekler. Sunucudaki sürüm ile istemcideki sürüm arasındaki fark çok büyükse veya istemci sunucudan daha yeniyse, `InvalidOperationException` istemci bağlantı kurmaya çalıştığında SignalR bir özel durum oluşturur. Hata iletisi`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" ".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Bağlantı kurma

Bir bağlantı kuramadan önce, bir `HubConnection` nesne oluşturmanız ve bir proxy oluşturmanız gerekir. Bağlantıyı kurmak `Start` `HubConnection` için, nesne üzerindeki yöntemi arayın.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> JavaScript istemcileri için bağlantıyı kurmak için `Start` yöntemi aramadan önce en az bir olay işleyicisi kaydetmeniz gerekir. Bu .NET istemcileri için gerekli değildir. JavaScript istemcileri için oluşturulan proxy kodu, sunucuda bulunan tüm Hub'lar için otomatik olarak proxy oluşturur ve işleyici kaydetmek, istemcinizin hangi Hub'ları kullanmak istediğini nasıl belirtirsiniz. Ancak bir .NET istemcisi için Hub proxy'lerini el ile oluşturursunuz, bu nedenle SignalR proxy oluşturduğunuz herhangi bir Hub'ı kullandığınızı varsayar.

Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır. Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.

Yöntem `Start` eşsenkronize yürütülür. Sonraki kod satırlarının bağlantı kurulana kadar yürütülmediğinden emin `await` olmak için, ASP.NET 4,5 asynchronous yönteminde veya `.Wait()` senkron yöntemle kullanın. WinRT istemcisinde kullanmayın. `.Wait()`

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight istemcilerinden etki alanı bağlantıları

Silverlight istemcilerinden etki alanı bağlantılarının nasıl etkinleştirilen hakkında bilgi için [bkz.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Bağlantı nasıl yapılandırılabilen

Bağlantı kurmadan önce, aşağıdaki seçeneklerden herhangi birini belirtebilirsiniz:

- Eşzamanlı bağlantılar sınırı.
- Dize parametrelerini sorgula.
- Taşıma yöntemi.
- HTTP üstbilgi.
- İstemci sertifikaları.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF istemcilerinde en fazla eşzamanlı bağlantı sayısı nasıl ayarlanır?

WPF istemcilerinde, varsayılan değeri olan 2'den en fazla eşzamanlı bağlantı sayısını artırmanız gerekebilir. Önerilen değer 10'dur.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Daha fazla bilgi için [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)'e bakın.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Sorgu dize parametreleri nasıl belirtilir?

İstemci bağlandığında sunucuya veri göndermek istiyorsanız, sorgu dize parametrelerini bağlantı nesnesine ekleyebilirsiniz. Aşağıdaki örnekte, istemci kodunda sorgu dize parametresi nasıl ayarlanır gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

Aşağıdaki örnekte, sunucu kodunda sorgu dize parametresi nasıl okunulup okunulduğu gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Taşıma yöntemi nasıl belirtilir?

Bağlanma işleminin bir parçası olarak, bir SignalR istemcisi normalde sunucu ile hem sunucu hem de istemci tarafından desteklenen en iyi aktarım belirlemek için görüşür. Hangi taşımayı kullanmak istediğinizi zaten biliyorsanız, bu müzakere işlemini atlayabilirsiniz. Aktarım yöntemini belirtmek için, bir aktarım nesnesi içinde Başlat yöntemine geçirin. Aşağıdaki örnek, istemci kodunda aktarım yönteminin nasıl belirtilen gösteriş olduğunu gösterir.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) ad alanı, aktarım durumunu belirtmek için kullanabileceğiniz aşağıdaki sınıfları içerir.

- [LongPollingUlaşım](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Yalnızca sunucu ve istemci .NET 4.5 kullandığında kullanılabilir.)
- [Otomatik Taşıma](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Otomatik olarak hem istemci hem de sunucu tarafından desteklenen en iyi aktarım seçer. Bu varsayılan aktarımdır. Bunu yönteme `Start` aktarmak, hiçbir şeyde geçmamak ile aynı etkiye sahiptir.)

Yalnızca tarayıcılar tarafından kullanıldığından ForeverFrame aktarımbu listeye dahil edilmez.

Sunucu kodunda aktarım yöntemini nasıl kontrol edeceğimiz hakkında bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Bağlam özelliğinden istemci hakkında nasıl bilgi alınır.](hubs-api-guide-server.md#contextproperty) Taşımalar ve geri dönüşler hakkında daha fazla bilgi için [SignalR'a Giriş - Taşımalar ve Geri Dönüşler'](../getting-started/introduction-to-signalr.md#transports)e bakın.

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP üstbilgi belirtme

HTTP üstbilgilerini ayarlamak `Headers` için bağlantı nesnesi üzerindeki özelliği kullanın. Aşağıdaki örnekte, http üstbilginin nasıl eklenilebildiğini gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>İstemci sertifikaları nasıl belirtilir?

İstemci sertifikaları eklemek `AddClientCertificate` için bağlantı nesnesi üzerindeki yöntemi kullanın.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Hub proxy'si nasıl oluşturulur?

Hub'ın sunucudan çağırabileceği istemcide yöntemleri tanımlamak ve sunucudaki bir Hub'da yöntemleri çağırmak için bağlantı `CreateHubProxy` nesnesini çağırarak Hub için bir proxy oluşturun. Geçtiğiniz dize `CreateHubProxy` Hub sınıfınızın adı veya sunucuda kullanıldıysa `HubName` öznitelik tarafından belirtilen addır. Ad eşleştirme büyük/küçük harf duyarsız.

**Sunucuda hub sınıfı**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Hub sınıfı için istemci proxy'si oluşturma**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Hub sınıfınızı bir `HubName` öznitelikle dekore ederseniz, bu adı kullanın.

**Sunucuda hub sınıfı**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Hub sınıfı için istemci proxy'si oluşturma**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Aynı `HubConnection.CreateHubProxy` `hubName`ile birden çok kez ararsanız, aynı `IHubProxy` önbelleğe alınmış nesneyi alırsınız.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?

Sunucunun çağırabileceği bir yöntem tanımlamak için, `On` bir olay işleyicisi kaydetmek için proxy yöntemini kullanın.

Yöntem adı eşleştirme büyük/küçük harf duyarsız. Örneğin, `Clients.All.UpdateStockPrice` sunucuda , `updateStockPrice` `updatestockprice`veya `UpdateStockPrice` istemci üzerinde yürütülür.

Farklı istemci platformları, Kullanıcı Arabirimi'ni güncelleştirmek için yöntem kodunu yazma şekliniz için farklı gereksinimlere sahiptir. Gösterilen örnekler WinRT (Windows Mağazası .NET) istemcileri içindir. WPF, Silverlight ve konsol uygulama örnekleri [daha sonra bu konuda ayrı bir bölümde](#wpfsl)verilmiştir.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Parametreleri olmayan yöntemler

İşlediğiniz yöntemin parametreleri yoksa, `On` yöntemin genel olmayan aşırı yükünü kullanın:

**Parametreleri olmadan sunucu kodu arama istemci yöntemi**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Parametreleri olmadan sunucudan çağrılan yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Parametre türlerini belirleyen parametrelerle ilgili yöntemler

İşlediğiniz yöntemin parametreleri varsa, yöntemin genel türleri olarak `On` parametrelerin türlerini belirtin. En fazla 8 parametre (Windows Phone 7'de 4) belirtmenizi sağlayan `On` yöntemin genel aşırı yüklemeleri vardır. Aşağıdaki örnekte, `UpdateStockPrice` yönteme bir parametre gönderilir.

**Bir parametre ile sunucu kodu arama istemci yöntemi**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Parametre için kullanılan Stok sınıfı**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**Parametreli sunucudan çağrılan bir yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler

Parametreleri yöntemin `On` genel türleri olarak belirtmeye alternatif olarak, parametreleri dinamik nesneler olarak belirtebilirsiniz:

**Bir parametre ile sunucu kodu arama istemci yöntemi**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Parametre için kullanılan Stok sınıfı**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**Parametre için dinamik bir nesne kullanarak, parametre ile sunucudan çağrılan bir yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Işleyici nasıl kaldırılır?

Bir işleyiciyi kaldırmak `Dispose` için yöntemini arayın.

**Sunucudan çağrılan bir yöntem için istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**İşleyiciyi kaldırmak için istemci kodu**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>İstemciden sunucu yöntemleri nasıl çağrılır?

Sunucuda bir yöntem çağırmak için `Invoke` Hub proxy'deki yöntemi kullanın.

Sunucu yönteminin iade değeri yoksa, `Invoke` yöntemin genel olmayan aşırı yükünü kullanın.

**İade değeri olmayan bir yöntemiçin sunucu kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**İade değeri olmayan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Sunucu yönteminin iade değeri varsa, yöntemin genel türü `Invoke` olarak iade türünü belirtin.

**İade değeri olan ve karmaşık bir tür parametresi alan bir yöntemiçin sunucu kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Parametre ve iade değeri için kullanılan Stok sınıfı**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Bir ASP.NET 4,5 async yönteminde, geri dönüş değeri olan ve karmaşık bir tür parametresi alan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Eşdönme değeri olan ve eşzamanlı bir yöntemde karmaşık bir tür parametresi alan bir yöntemi çağıran istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Yöntem `Invoke` eşsenkronize yürütülür ve `Task` bir nesneyi döndürür. Belirtmezseniz `await` veya, `.Wait()`çağırdığınız yöntem yürütme tamamlanmadan önce bir sonraki kod satırı yürütülür.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Bağlantı ömrü olayları nasıl işler?

SignalR işleyebilir aşağıdaki bağlantı ömrü olayları sağlar:

- `Received`: Bağlantıdan herhangi bir veri alındığı zaman yükseltilir. Alınan verileri sağlar.
- `ConnectionSlow`: İstemci yavaş veya sık sık bırakarak bağlantı algıladığında yükseltilir.
- `Reconnecting`: Altta yatan aktarım yeniden bağlanmaya başladığında yükseltilir.
- `Reconnected`: Temel taşıma yeniden bağlandığında yükseltilir.
- `StateChanged`: Bağlantı durumu değiştiğinde yükseltilir. Eski durumu ve yeni durumu sağlar. Bağlantı durumu değerleri hakkında bilgi için Bkz. [ConnectionState Numaralandırma.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)
- `Closed`: Bağlantı kesildiğinde yükseltilir.

Örneğin, önemli olmayan ancak bağlantının yavaşlığı veya sık sık düşmesi gibi aralıklı bağlantı sorunlarına neden olan `ConnectionSlow` hatalar için uyarı iletileri görüntülemek istiyorsanız, olayı işleyin.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Hataları işleme

Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, SignalR'ın hatadan sonra döndürdİğİ özel durum nesnesi hata hakkında en az bilgi içerir. Örneğin, bir çağrı `newContosoChatMessage` başarısız olursa, hata nesnesindeki`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`hata iletisi " " Üretimdeki istemcilere ayrıntılı hata iletileri göndermek güvenlik nedenleriyle önerilmez, ancak sorun giderme amacıyla ayrıntılı hata iletilerini etkinleştirmek istiyorsanız, sunucudaki aşağıdaki kodu kullanın.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR'ın kaldırdığı hataları işlemek için bağlantı `Error` nesnesindeki olay için bir işleyici ekleyebilirsiniz.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Yöntem çağrılarından gelen hataları işlemek için kodu try-catch bloğuna sarın.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>İstemci tarafı günlüğe kaydetmeyi etkinleştirme

İstemci tarafı günlüğe `TraceLevel` kaydetmeyi etkinleştirmek için bağlantı nesnesi üzerindeki ve `TraceWriter` özelliklerini ayarlayın.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Sunucunun çağırabileceği istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri

Sunucunun çağırabileceği istemci yöntemlerini tanımlamak için daha önce gösterilen kod örnekleri WinRT istemcilerine uygulanır. Aşağıdaki örnekler WPF, Silverlight ve konsol uygulama istemcileri için eşdeğer kodu gösterir.

### <a name="methods-without-parameters"></a>Parametreleri olmayan yöntemler

**Parametreleri olmadan sunucudan çağrılan yöntem için WPF istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Parametreleri olmadan sunucudan çağrılan yöntem için Silverlight istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Parametreleri olmadan sunucudan çağrılan yöntem için konsol uygulaması istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Parametre türlerini belirleyen parametrelerle ilgili yöntemler

**Parametreli sunucudan çağrılan bir yöntem için WPF istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Parametreli sunucudan çağrılan bir yöntem için Silverlight istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Parametreli sunucudan çağrılan bir yöntem için konsol uygulaması istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler

**Parametre için dinamik bir nesne kullanarak, parametreile sunucudan çağrılan bir yöntem için WPF istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Parametre için dinamik bir nesne kullanarak, parametreile sunucudan çağrılan bir yöntem için Silverlight istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Parametre için dinamik bir nesne kullanarak, parametre ile sunucudan çağrılan bir yöntem için konsol uygulama istemci kodu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
