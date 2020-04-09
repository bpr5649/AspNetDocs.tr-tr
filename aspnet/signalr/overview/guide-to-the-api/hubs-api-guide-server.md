---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hub'ları API Kılavuzu - Sunucu (C#) | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, SignalR sürüm 2 için SignalR Hub'ASP.NET sunucu tarafıprogramlamaiçin bir giriş sağlar, kod örnekleri gösteren ile ...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676190"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR Hub'ları API Kılavuzu - Sunucu (C#)

Patrick [Fletcher](https://github.com/pfletcher)tarafından , [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belge, SignalR sürüm 2 için signalr hub'ASP.NET sunucu tarafını programlamaya giriş sağlar ve kod örnekleri ortak seçenekleri gösterir.
> 
> SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar. Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız. İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız. SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.
> 
> SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar. SignalR, Hub'lar ve Kalıcı [Bağlantılar'a](../getting-started/introduction-to-signalr.md)giriş için bkz.
> 
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
> 
> 
> - [Görsel Stüdyo 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR sürüm 2
>   
> 
> 
> ## <a name="topic-versions"></a>Konu sürümleri
> 
> SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.
> 
> ## <a name="questions-and-comments"></a>Sorular ve yorumlar
> 
> Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.

## <a name="overview"></a>Genel Bakış

Bu belgede aşağıdaki bölümler yer alır:

- [SignalR ara yazılımnasıl kaydedilir?](#route)

    - [/sinyalci URL'si](#signalrurl)
    - [SignalR seçeneklerini yapılandırma](#options)
- [Hub sınıfları oluşturma ve kullanma](#hubclass)

    - [Hub nesnesi yaşam süresi](#transience)
    - [JavaScript istemcilerinde Hub adlarının deve kaplaması](#hubnames)
    - [Birden Çok Hub](#multiplehubs)
    - [Güçlü Bir Şekilde Yazılan Hub'lar](#stronglytypedhubs)
- [Hub sınıfında istemcilerin çağırabileceği yöntemler nasıl tanımlanır?](#hubmethods)

    - [JavaScript istemcilerinde yöntem adlarının deve kaplaması](#methodnames)
    - [Eşsenkronize olarak ne zaman yürütülecek?](#asyncmethods)
    - [Aşırı yüklemeleri tanımlama](#overloads)
    - [Hub yöntemi çağrılarından ilerlemeyi bildirme](#progress)
- [Hub sınıfından istemci yöntemleri nasıl çağrılır?](#callfromhub)

    - [Hangi istemcilerin RPC'yi alacağını seçme](#selectingclients)
    - [Yöntem adları için derleme zamanı doğrulaması yok](#dynamicmethodnames)
    - [Büyük/küçük harf duyarsız yöntem adı eşleştirme](#caseinsensitive)
    - [Eşkron yürütme](#asyncclient)
- [Hub sınıfından grup üyeliği nasıl yönetilir?](#groupsfromhub)

    - [Ekle ve Kaldır yöntemlerinin eşzamanlı yürütmesi](#asyncgroupmethods)
    - [Grup üyeliği kalıcılığı](#grouppersistence)
    - [Tek kullanıcılı gruplar](#singleusergroups)
- [Hub sınıfındaki bağlantı ömrü olayları nasıl işleyebilir?](#connectionlifetime)

    - [OnConnected, OnDisconnected ve OnReconnected çağrıldığında](#onreconnected)
    - [Arayan durumu doldurulmamada](#nocallerstate)
- [Bağlam özelliğinden istemci hakkında bilgi alma](#contextproperty)
- [İstemciler ve Hub sınıfı arasında durum nasıl geçirilir?](#passstate)
- [Hub sınıfındaki hatalar nasıl işler?](#handleErrors)
- [İstemci yöntemlerini arama ve Hub sınıfı dışından grupları yönetme](#callfromoutsidehub)

    - [İstemci yöntemlerini arama](#callingclientsoutsidehub)
    - [Grup üyeliğini yönetme](#managinggroupsoutsidehub)
- [İzlemeyi etkinleştirme](#tracing)
- [Hubs ardışık hattı özelleştirme](#hubpipeline)

İstemcilerin nasıl programlanacak programlayacağına ilişkin belgeler için aşağıdaki kaynaklara bakın

- [SignalR Hubs API Kılavuzu - JavaScript İstemci](hubs-api-guide-javascript-client.md)
- [SignalR Hub'lar API Kılavuzu - .NET İstemci](hubs-api-guide-net-client.md)

SignalR 2'nin sunucu bileşenleri yalnızca .NET 4.5'te kullanılabilir. .NET 4.0 çalıştıran sunucular SignalR v1.x kullanmalıdır.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>SignalR ara yazılımnasıl kaydedilir?

İstemcilerin Hub'ınıza bağlanmak için kullanacağı `MapSignalR` yolu tanımlamak için uygulama başladığında yöntemi arayın. `MapSignalR`sınıf için bir [uzantı yöntemidir.](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` Aşağıdaki örnekte, OWIN başlangıç sınıfını kullanarak SignalR Hub'ları rotasının nasıl tanımlanılışgösterilmektedir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

ASP.NET bir MVC uygulamasına SignalR işlevselliği ekliyorsanız, SignalR rotasının diğer rotalardan önce eklenmiştir. Daha fazla bilgi için [Bkz. Öğretici: SignalR 2 ve MVC 5 ile Başlarken.](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/sinyalci URL'si

Varsayılan olarak, istemcilerin Hub'ınıza bağlanmak için kullanacağı rota URL'si "/signalr"dir. (Bu URL'yi otomatik olarak oluşturulan JavaScript dosyası için olan "/signalr/hubs" URL'si ile karıştırmayın. Oluşturulan proxy hakkında daha fazla bilgi için [SignalR Hub'lar API Kılavuzu - JavaScript İstemci - Oluşturulan proxy ve sizin için ne yaptığını](hubs-api-guide-javascript-client.md#genproxy)bakın .)

Bu temel URL'yi SignalR için kullanılabilir hale getiren olağanüstü durumlar olabilir; örneğin, projenizde *signalr* adında bir klasör var ve adı değiştirmek istemiyorsun. Bu durumda, aşağıdaki örneklerde gösterildiği gibi temel URL'yi değiştirebilirsiniz (örnek koddaki "/sinyal"i istediğiniz URL ile değiştirin).

**URL'yi belirten sunucu kodu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**URL'yi belirten JavaScript istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**URL'yi belirten JavaScript istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL'yi belirten .NET istemci kodu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>Sinyal Seçeneklerinin Yapılandırılması

`MapSignalR` Yöntemin aşırı yükleri özel bir URL, özel bağımlılık çözümleyicisi ve aşağıdaki seçenekleri belirtmenize olanak tanır:

- Tarayıcı istemcilerinden CORS veya JSONP kullanarak etki alanları arası aramaları etkinleştirin.

    Genellikle tarayıcı bir sayfa `http://contoso.com`yükler, SinyalR bağlantısı aynı etki alanında, at `http://contoso.com/signalr`. Sayfa, `http://contoso.com` `http://fabrikam.com/signalr`etki alanı arası bağlantıyla bağlantı yapıyorsa. Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışı bırakılır. Daha fazla bilgi için [signalr hub'lar API Kılavuzu ASP.NET - JavaScript Client - Nasıl bir çapraz etki alanı bağlantısı kurmak için bkz.](hubs-api-guide-javascript-client.md#crossdomain)
- Ayrıntılı hata iletilerini etkinleştirin.

    Hatalar oluştuğunda, SignalR'In varsayılan davranışı istemcilere ne olduğu hakkında ayrıntılı bilgi olmadan bir bildirim iletisi göndermektir. Kötü niyetli kullanıcılar bu bilgileri uygulamanıza yönelik saldırılarda kullanabileceğinden, müşterilere ayrıntılı hata bilgileri gönderilmesi üretimde önerilmez. Sorun giderme için, geçici olarak daha bilgilendirici hata raporlaması etkinleştirmek için bu seçeneği kullanabilirsiniz.
- Otomatik olarak oluşturulan JavaScript proxy dosyalarını devre dışı kalın.

    Varsayılan olarak, Hub sınıflarınız için ek sa'ların yer aldığı bir JavaScript dosyası, URL "/signalr/hub"a yanıt olarak oluşturulur. JavaScript proxy'lerini kullanmak istemiyorsanız veya bu dosyayı el ile oluşturmak ve istemcilerinizde fiziksel bir dosyaya başvurmak istiyorsanız, proxy oluşturmayı devre dışı kullanabilirsiniz. Daha fazla bilgi için [SignalR Hubs API Kılavuzu - JavaScript Client - SignalR oluşturulan proxy için fiziksel bir dosya oluşturmak için nasıl](hubs-api-guide-javascript-client.md#manualproxy)bakın.

Aşağıdaki örnekte, SignalR bağlantı URL'sinin nasıl belirtililir `MapSignalR` ve bu seçenekler yönteme yapılan bir çağrıda gösterilmektedir. Özel bir URL belirtmek için, örnekteki "/sinyal"i kullanmak istediğiniz URL ile değiştirin.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Hub sınıfları oluşturma ve kullanma

Hub oluşturmak için [Microsoft.Aspnet.Signalr.Hub'dan](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)türetilen bir sınıf oluşturun. Aşağıdaki örnekte, sohbet uygulaması için basit bir Hub sınıfı gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

Bu örnekte, bağlı bir `NewContosoChatMessage` istemci yöntemi arayabilir ve bu yöntem olduğunda, alınan veriler tüm bağlı istemcilere yayınlanır.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Hub nesnesi yaşam süresi

Hub sınıfını anında atamazsın veya yöntemlerini sunucuda kendi kodunuzdan aramazsınız; tüm bunlar SignalR Hub'lar boru hattı tarafından sizin için yapılır. SignalR, istemcinin sunucuya bağlanması, bağlantısını kesmesi veya bir yöntem çağrısı yapması gibi hub işlemini işlemesi gerektiğinde Hub sınıfınızın yeni bir örneğini oluşturur.

Hub sınıfının örnekleri geçici olduğundan, durumları bir yöntem çağrısından diğerine korumak için bunları kullanamazsınız. Sunucu her istemciden yöntem çağrısı aldığında, Hub sınıfınızın yeni bir örneği iletiyi işler. Birden çok bağlantı ve yöntem çağrıları aracılığıyla durumu korumak için, veritabanı veya Hub sınıfında statik bir değişken veya türetilmeyen farklı bir sınıf gibi başka bir yöntem `Hub`kullanın. Hub sınıfındastatik değişken gibi bir yöntem kullanarak bellekte verileri kalıcı olarak kullanırsanız, uygulama etki alanı geri dönüştürdüğünde veriler kaybolur.

Hub sınıfının dışında çalışan kendi kodunuzdan istemcilere ileti göndermek istiyorsanız, hub sınıfı örneğini anında anlayarak bunu yapamazsınız, ancak Hub sınıfınız için SignalR bağlam nesnesine bir başvuru alarak bunu yapabilirsiniz. Daha fazla bilgi için, bu konuda daha sonra [Hub sınıfı dışından istemci yöntemlerini nasıl çağırıp grupları nasıl yöneteceklerini](#callfromoutsidehub) öğrenin.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript istemcilerinde Hub adlarının deve kaplaması

Varsayılan olarak, JavaScript istemcileri sınıf adının deve kasalı bir sürümünü kullanarak Hub'lara başvurur. SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar. Önceki örnek JavaScript kodunda olarak `contosoChatHub` adlandırılır.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

İstemciler için farklı bir ad belirtmek `HubName` istiyorsanız, özniteliği ekleyin. Bir `HubName` öznitelik kullandığınızda, JavaScript istemcilerinde deve durumunda ad değişikliği yoktur.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Birden Çok Hub

Bir uygulamada birden çok Hub sınıfı tanımlayabilirsiniz. Bunu yaptığınızda, bağlantı paylaşılır, ancak gruplar ayrıdır:

- Tüm istemciler, hizmetinizle ("/signalr" veya belirttiğiniz özel URL'nizde) bir SignalR bağlantısı kurmak için aynı URL'yi kullanır ve bu bağlantı hizmet tarafından tanımlanan tüm Hub'lar için kullanılır.

    Tek bir sınıftaki tüm Hub işlevlerini tanımlamayla karşılaştırıldığında birden çok Hub için performans farkı yoktur.
- Tüm Hub'lar aynı HTTP istek bilgilerini alır.

    Tüm Hub'lar aynı bağlantıyı paylaştığından, sunucunun aldığı tek HTTP isteği bilgisi SignalR bağlantısını kuran orijinal HTTP isteğinde ne gelir. Bir sorgu dizesi belirterek istemciden sunucuya bilgi aktarmak için bağlantı isteğini kullanırsanız, farklı Hub'lara farklı sorgu dizeleri sağlayamazsınız. Tüm Hub'lar aynı bilgileri alır.
- Oluşturulan JavaScript yakınlık dosyası, tek bir dosyadaki tüm Hub'lar için yakınlıklar içerir.

    JavaScript proxy'leri hakkında bilgi için [SignalR Hub'lar API Kılavuzu - JavaScript Client - Oluşturulan proxy ve sizin için ne yaptığına](hubs-api-guide-javascript-client.md#genproxy)bakın.
- Gruplar Hub'lar içinde tanımlanır.

    SignalR'da bağlı istemcialt kümelerine yayın yapacak adlandırılmış grupları tanımlayabilirsiniz. Gruplar her Hub için ayrı ayrı tutulur. Örneğin, "Yöneticiler" adlı bir grup, sınıfınız `ContosoChatHub` için bir istemci kümesi içerir ve aynı grup adı `StockTickerHub` sınıfınız için farklı bir istemci kümesine başvurur.

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Güçlü Bir Şekilde Yazılan Hub'lar

Müşterinizin başvuruedebileceği hub yöntemleriniz için bir arayüz tanımlamak (ve hub yöntemlerinizde Intellisense'i etkinleştirin), `Hub<T>` hub'ınızı `Hub`(SignalR 2.1'de tanıtılan) yerine türetin:

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Hub sınıfında istemcilerin çağırabileceği yöntemler nasıl tanımlanır?

İstemciden çağrılmasını istediğiniz hub'da bir yöntemi ortaya çıkarmak için, aşağıdaki örneklerde gösterildiği gibi ortak bir yöntem bildirin.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Herhangi bir C# yönteminde olduğu gibi, karmaşık türler ve diziler de dahil olmak üzere bir iade türü ve parametreleri belirtebilirsiniz. Parametrelerde aldığınız veya arayana geri döndüğünüz tüm veriler JSON kullanılarak istemci ve sunucu arasında iletilir ve SignalR karmaşık nesnelerin ve nesnelerin dizilerinin bağlanmasını otomatik olarak işler.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript istemcilerinde yöntem adlarının deve kaplaması

Varsayılan olarak, JavaScript istemcileri yöntem adının deve kasalı bir sürümünü kullanarak Hub yöntemlerine başvurur. SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

İstemciler için farklı bir ad belirtmek `HubMethodName` istiyorsanız, özniteliği ekleyin.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Eşsenkronize olarak ne zaman yürütülecek?

Yöntem uzun süreli olacaksa veya veritabanı araması veya web hizmeti çağrısı gibi beklemeyi içeren işler yapmak zorundaysa, [Görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) `void` `T` (iade yerine) veya [Görev&lt;&gt; T](https://msdn.microsoft.com/library/dd321424.aspx) nesnesini (iade türü yerine) döndürerek Hub yöntemini eş zamanlı hale getirin. Yöntemden bir `Task` nesne döndürdüğünde, SignalR `Task` tamamlanmasını bekler ve ardından paketlenmemiş sonucu istemciye geri gönderir, bu nedenle istemcideki yöntem çağrısını nasıl kodladığınız konusunda bir fark yoktur.

Hub yöntemini eşkron yapma, WebSocket aktarımını kullandığında bağlantıyı engellemeyi önler. Hub yöntemi eşzamanlı olarak yürütülür ve aktarım WebSocket olduğunda, Hub yöntemi tamamlanana kadar hub'daki yöntemlerin sonraki çağrıları aynı istemciden engellenir.

Aşağıdaki örnek, eşzamanlı veya eşsenkronize çalıştırmak için kodlanmış aynı yöntemi gösterir ve ardından her iki sürümü de aramak için çalışan JavaScript istemci kodu gelir.

**Zaman uyumlu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**Zaman uyumsuz**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5'te eşzamanlı yöntemlerin nasıl kullanılacağı hakkında daha fazla bilgi için, [ASP.NET MVC 4'te Asynchronous Yöntemleri kullanma'ya](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)bakın.

<a id="overloads"></a>

### <a name="defining-overloads"></a>Aşırı yüklemeleri tanımlama

Bir yöntem için aşırı yüklemeleri tanımlamak istiyorsanız, her aşırı yükteki parametre sayısı farklı olmalıdır. Bir aşırı yükü sadece farklı parametre türleri belirterek farklılaştırırsanız, Hub sınıfınız derlenir, ancak istemciler aşırı yüklerden birini çağırmaya çalıştıklarında SignalR hizmeti çalışma zamanında bir özel durum oluşturur.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>Hub yöntemi çağrılarından ilerlemeyi bildirme

SignalR 2.1,.NET 4.5'te tanıtılan [ilerleme raporlama deseni](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) için destek ekler. İlerleme raporlaması uygulamak `IProgress<T>` için, istemcinizin erişebileceği hub yönteminiz için bir parametre tanımlayın:

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

Uzun soluklu bir sunucu yöntemi yazarken, hub iş parçacığı engelleme yerine Async / Await gibi bir eşzamanlı programlama deseni kullanmak önemlidir.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Hub sınıfından istemci yöntemleri nasıl çağrılır?

Sunucudan istemci yöntemlerini çağırmak `Clients` için Hub sınıfınızdaki bir yöntemde özelliği kullanın. Aşağıdaki örnek, bağlı tüm `addNewMessageToPage` istemcileri çağıran sunucu kodunu ve JavaScript istemcisinde yöntemi tanımlayan istemci kodunu gösterir.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

İstemci yöntemini çağırmak eşzamanlı bir işlemdir `Task`ve bir . Kullanım `await`Tarihi :

* İletinin hatasız gönderilmesini sağlamak için. 
* Try-catch bloğunda hataların yakalanmasını ve işlenmesini etkinleştirmek için.

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

İstemci yönteminden iade değeri alamazsınız; gibi `int x = Clients.All.add(1,1)` sözdizimi çalışmıyor.

Parametreler için karmaşık türleri ve dizileri belirtebilirsiniz. Aşağıdaki örnek, yöntem parametresinde istemciye karmaşık bir tür geçer.

**Karmaşık bir nesne kullanarak istemci yöntemi çağıran sunucu kodu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**Karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Hangi istemcilerin RPC'yi alacağını seçme

İstemciler özelliği, hangi istemcilerin RPC'yi alacağını belirtmek için çeşitli seçenekler sağlayan bir [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) nesnesi döndürür:

- Tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- Sadece arayan müşteri.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- Arayan istemci hariç tüm müşteriler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- Bağlantı kimliğiyle tanımlanan belirli bir istemci.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    Bu örnek, çağıran istemciyi çağırır `addContosoChatMessageToPage` ve `Clients.Caller`'yi kullanmakla aynı etkiye sahiptir.
- Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- Belirli bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında belirli bir gruptaki tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- Çağıran istemci dışında belirli bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- UserId tarafından tanımlanan belirli bir kullanıcı.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    Varsayılan olarak, `IPrincipal.Identity.Name`bu , ancak bu [küresel ana bilgisayar ile IUserIdProvider bir uygulama kaydedilerek](mapping-users-to-connections.md#IUserIdProvider)değiştirilebilir.
- Bağlantı t.c. listesindeki tüm istemciler ve gruplar.

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- Grupların listesi.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- Ada göre bir kullanıcı.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- Kullanıcı adlarının listesi (SignalR 2.1'de tanıtıldı).

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Yöntem adları için derleme zamanı doğrulaması yok

Belirttiğiniz yöntem adı dinamik bir nesne olarak yorumlanır, bu da IntelliSense veya derleme zamanı doğrulaması olmadığı anlamına gelir. İfade çalışma zamanında değerlendirilir. Yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerlerini istemciye gönderir ve istemcide ada uyan bir yöntem varsa, bu yöntem çağrılır ve parametre değerleri ona aktarılır. İstemcide eşleşen bir yöntem bulunmazsa, hata yapılmaz. İstemci yöntemini aradiğinizde SignalR'ın istemciye aktardığı verilerin biçimi hakkında bilgi için [signalr'e giriş bölümüne](../getting-started/introduction-to-signalr.md)bakın.

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Büyük/küçük harf duyarsız yöntem adı eşleştirme

Yöntem adı eşleştirme büyük/küçük harf duyarsız. Örneğin, `Clients.All.addContosoChatMessageToPage` sunucuda , `AddContosoChatMessageToPage` `addcontosochatmessagetopage`veya `addContosoChatMessageToPage` istemci üzerinde yürütülür.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Eşkron yürütme

Dediğiniz yöntem eşsenkronize olarak yürütülür. İstemciye bir yöntem çağrısından sonra gelen herhangi bir kod, sonraki kod satırlarının yöntemin tamamlanmasını beklemesi gerektiğini belirtmediğiniz sürece SignalR'ın istemcilere veri iletimini bitirmesini beklemeden hemen yürütülür. Aşağıdaki kod örneği, iki istemci yönteminin sırayla nasıl yürütüleceklerini gösterir.

**Await kullanma (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

İstemci `await` yöntemi nin bir sonraki kod satırı yürütülmeden önce tamamlanmasını beklerseniz, bu istemcilerin bir sonraki kod satırı yürütülmeden önce iletiyi gerçekten alacağı anlamına gelmez. İstemci yöntemi çağrısının "tamamlanması" yalnızca SignalR'In iletiyi göndermek için gereken her şeyi yaptığı anlamına gelir. İstenilenlerin iletiyi aldığını doğrulamanız gerekiyorsa, bu mekanizmayı kendiniz programlamanız gerekir. Örneğin, Hub'da `MessageReceived` bir yöntem kodlayabilir ve `addContosoChatMessageToPage` istemcideki yöntemde `MessageReceived` istemci üzerinde yapmanız gereken her türlü işi yaptıktan sonra arayabilirsiniz. Hub'da, `MessageReceived` gerçek istemci alımına ve özgün yöntem çağrısının işlenmesine bağlı olarak ne iş yaparsanız yapabilirsiniz.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Yöntem adı olarak bir dize değişkeni nasıl kullanılır?

Yöntem adı olarak bir dize değişkeni kullanarak bir istemci `Clients.All` yöntemi `Clients.Others` `Clients.Caller`çağırmak istiyorsanız, `IClientProxy` döküm (veya , , vb) ve sonra [Invoke (methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)diyoruz.

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Hub sınıfından grup üyeliği nasıl yönetilir?

SignalR'deki gruplar, iletileri bağlı istemcilerin belirtilen alt kümelerine yayınlamak için bir yöntem sağlar. Bir grubun herhangi bir sayıda istemcisi olabilir ve istemci herhangi bir sayıda grubun üyesi olabilir.

Grup üyeliğini yönetmek için Hub sınıfının `Groups` özelliği tarafından sağlanan [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) ve [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini kullanın. Aşağıdaki örnek, `Groups.Add` hub `Groups.Remove` yöntemlerinde istemci kodu tarafından çağrılan yöntemleri ve yöntemleri gösterir ve ardından onları çağıran JavaScript istemci kodu nu gösterir.

**Sunucu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**Oluşturulan proxy kullanarak JavaScript istemcisi**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

Açıkça grup oluşturmanız gerekmemektedir. Sonuç olarak, bir grup, bir çağrıda `Groups.Add`adını ilk kez belirttiğiniz de otomatik olarak oluşturulur ve son bağlantıyı üyelikten kaldırdığınızda silinir.

Grup üyelik listesi veya grupların listesini almak için API yoktur. SignalR istemcilere ve gruplara bir [pub/alt modele](http://en.wikipedia.org/wiki/Publish/subscribe)dayalı iletigönderir ve sunucu grup veya grup üyeliklerinin listesini tutmaz. Bu ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur, çünkü bir web çiftliğine düğüm eklediğinizde, SignalR'In koruduğu herhangi bir durum yeni düğüme yayılması gerekir.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Ekle ve Kaldır yöntemlerinin eşzamanlı yürütmesi

Ve `Groups.Add` `Groups.Remove` yöntemler eşsenkronize yürütülür. Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen bir ileti göndermek istiyorsanız, `Groups.Add` önce yöntemin sona erdiğinden emin olmalısınız. Aşağıdaki kod örneği, bunun nasıl yapılacağını gösterir.

**Bir gruba istemci ekleme ve sonra o istemciile mesajlaşma**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Grup üyeliği kalıcılığı

SignalR bağlantıları izler, kullanıcıları değil, bu nedenle bir kullanıcının her bağlantı kurduğunda aynı grupta olmasını `Groups.Add` istiyorsanız, kullanıcı yeni bir bağlantı kurduğunda her aramanız gerekir.

Geçici bir bağlantı kaybından sonra, bazen SignalR bağlantıyı otomatik olarak geri yükleyebilir. Bu durumda SignalR aynı bağlantıyı geri yükleniyor, yeni bir bağlantı kurmuyor ve böylece istemcinin grup üyeliği otomatik olarak geri yükleniyor. Grup üyelikleri de dahil olmak üzere her istemci için bağlantı durumu istemciye çift yönlü olarak takıldıklarından, geçici ara sunucu yeniden başlatma veya hata nın sonucu olsa bile bu mümkündür. Bir sunucu kapanıp bağlantı süreleri dolmadan yeni bir sunucu yla değiştirilirse, istemci yeni sunucuya otomatik olarak yeniden bağlanabilir ve üyesi olduğu gruplara yeniden kaydolabilir.

Bağlantı kaybından sonra bir bağlantı otomatik olarak geri yüklenemediğinde veya bağlantı zaman ları kesildiğinde veya istemci bağlantı kesildiğinde (örneğin, bir tarayıcı yeni bir sayfaya gittiğinde), grup üyelikleri kaybolur. Kullanıcı bir sonraki bağlanında yeni bir bağlantı olacaktır. Aynı kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini korumak için, uygulamanızın kullanıcılar ve gruplar arasındaki ilişkileri izlemesi ve bir kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini geri yüklemesi vardır.

Bağlantılar ve yeniden bağlantılar hakkında daha fazla bilgi için hub [sınıfındaki bağlantı ömrü olaylarının bu konuda nasıl işleyeceğiniz](#connectionlifetime) konusuna bakın.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Tek kullanıcılı gruplar

SignalR kullanan uygulamalar, hangi kullanıcının ileti gönderdiğini ve hangi kullanıcının ileti alması gerektiğini bilmek için genellikle kullanıcılar ve bağlantılar arasındaki ilişkileri izlemek zorundadır. Gruplar bunu yapmak için kullanılan iki desenden birinde kullanılır.

- Tek kullanıcılı gruplar.

    Kullanıcı adını grup adı olarak belirtebilir ve kullanıcı her bağlandığında veya yeniden bağlanınher bağlanında gruba geçerli bağlantı kimliğini ekleyebilirsiniz. Gruba gönderdiğiniz kullanıcıya ileti göndermek için. Bu yöntemin bir dezavantajı, grubun size kullanıcının çevrimiçi veya çevrimdışı olup olmadığını öğrenmeniz için bir yol sağlamamasıdır.
- Kullanıcı adları ve bağlantı adları arasındaki ilişkileri izleyin.

    Her kullanıcı adı ile bir veya daha fazla bağlantı bağlantısı disi arasındaki ilişkilendirmeyi bir sözlükveya veritabanında depolayabilir ve kullanıcı her bağlandığında veya bağlantı kestiğinde depolanan verileri güncelleştirebilirsiniz. Kullanıcıya ileti göndermek için bağlantı bağlantı larını belirtirsiniz. Bu yöntemin bir dezavantajı daha fazla bellek alır olmasıdır.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Hub sınıfındaki bağlantı ömrü olayları nasıl işleyebilir?

Bağlantı yaşam boyu olayları işlemeiçin tipik nedenler, bir kullanıcının bağlı olup olmadığını izlemek ve kullanıcı adları ve bağlantı adları arasındaki ilişkilendirme izlemektir. İstemciler bağlandığında veya bağlantılarını kestiğinde `OnConnected` `OnDisconnected`kendi `OnReconnected` kodunuzu çalıştırmak için, aşağıdaki örnekte gösterildiği gibi Hub sınıfının ,, ve sanal yöntemlerini geçersiz kılın.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected, OnDisconnected ve OnReconnected çağrıldığında

Bir tarayıcı yeni bir sayfaya her yönlendirilse, yeni bir bağlantı kurulmalıdır, bu da SignalR'In `OnDisconnected` `OnConnected` yöntemi uygulayacağı anlamına gelir. SignalR, yeni bir bağlantı kurulduğunda her zaman yeni bir bağlantı kimliği oluşturur.

Bu `OnReconnected` yöntem, SignalR'in bağlantı süreleri kesilmeden önce kablonun geçici olarak bağlantısının kesilmesi ve yeniden bağlanması gibi otomatik olarak kurtarabileceği geçici bir bağlantı sonu olduğunda çağrılır. İstemcinin `OnDisconnected` bağlantısı kesildiğinde ve Tarayıcı yeni bir sayfaya gittiğinde olduğu gibi SignalR otomatik olarak yeniden bağlanadığında yöntem çağrılır. Bu nedenle, belirli bir istemci için `OnConnected` `OnReconnected`olası `OnDisconnected`bir olay dizisi , , , ; veya `OnConnected` `OnDisconnected`, . Belirli bir bağlantı `OnConnected` `OnDisconnected` `OnReconnected` için sırayı görmezsiniz.

Yöntem, `OnDisconnected` sunucunun çöktüğü veya Uygulama Etki Alanı'nın geri dönüştürülderken olduğu gibi bazı senaryolarda çağrılmaz. Başka bir sunucu devreye girdiğinde veya App Domain geri dönüşümünü tamamladığında, bazı `OnReconnected` istemciler olayı yeniden bağlayıp ateşleyebilir.

Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Arayan durumu doldurulmamada

Bağlantı ömrü nes'i olay işleyicisi yöntemleri sunucudan çağrılır, bu da istemcideki `state` nesneye koyduğunuz herhangi bir durum için sunucudaki `Caller` özellikte doldurulmayacağı anlamına gelir. Nesne ve `state` `Caller` özellik hakkında bilgi için, bu konunun ilerleyen saatlerinde [istemciler ve Hub sınıfı arasında durum geçişini nasıl](#passstate) göreceğiz.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Bağlam özelliğinden istemci hakkında bilgi alma

İstemci hakkında bilgi almak `Context` için Hub sınıfının özelliğini kullanın. Özellik, `Context` aşağıdaki bilgilere erişim sağlayan bir [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) nesnesini döndürür:

- Arayan istemcinin bağlantı kimliği.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    Bağlantı kimliği SignalR tarafından atanan bir GUID'dir (kendi kodunuzdaki değeri belirtemezsiniz). Her bağlantı için bir bağlantı kimliği vardır ve uygulamanızda birden çok Hub varsa aynı bağlantı kimliği tüm Hub'lar tarafından kullanılır.
- HTTP üstbilgi verileri.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    Ayrıca HTTP başlıkları `Context.Headers`alabilirsiniz. Aynı şey `Context.Headers` için birden çok başvuruiçin nedeni, `Context.Request` ilk oluşturulan, özellik `Context.Headers` daha sonra eklendi ve geriye dönük uyumluluk için tutuldu.
- Dize verilerini sorgula.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    Ayrıca sorgu dize verileri `Context.QueryString`de alabilirsiniz.

    Bu özellikte aldığınız sorgu dizesi, SignalR bağlantısını kuran HTTP isteğiyle kullanılan dizedir. İstemci hakkındaki verileri istemciden sunucuya aktarmanın kullanışlı bir yolu olan bağlantıyı yapılandırarak istemciye sorgu dize parametreleri ekleyebilirsiniz. Aşağıdaki örnek, oluşturulan proxy'yi kullandığınızda JavaScript istemcisine sorgu dizesi eklemenin bir yolunu gösterir.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    Sorgu dize parametrelerini ayarlama hakkında daha fazla bilgi için [JavaScript](hubs-api-guide-javascript-client.md) ve [.NET](hubs-api-guide-net-client.md) istemcileri için API kılavuzlarına bakın.

    SignalR tarafından dahili olarak kullanılan diğer bazı değerlerle birlikte sorgu dize verilerinde bağlantı için kullanılan aktarım yöntemini bulabilirsiniz:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    Değeri "webSockets", "serverSentEvents", "foreverFrame" veya "longPolling" `transportMethod` olacaktır. `OnConnected` Olay işleyicisi yönteminde bu değeri denetlerseniz, bazı senaryolarda başlangıçta bağlantı için son anlaşmalı aktarım yöntemi olmayan bir aktarım değeri alabileceğinizi unutmayın. Bu durumda yöntem bir özel durum oluşturur ve son aktarım yöntemi oluşturulduğunda daha sonra tekrar çağrılacaktır.
- Kurabiye.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    Ayrıca çerezleri `Context.RequestCookies`de .
- Kullanıcı bilgileri.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- İstek için HttpContext nesnesi:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    SinyalR bağlantısı için `HttpContext.Current` `HttpContext` nesneyi almak yerine bu yöntemi kullanın.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>İstemciler ve Hub sınıfı arasında durum nasıl geçirilir?

İstemci proxy, sunucuya aktarılmasını istediğiniz verileri her yöntem çağrısıyla depolayabildiğiniz bir `state` nesne sağlar. Sunucuda, istemciler tarafından çağrılan `Clients.Caller` Hub yöntemleriyle bu verilere özellikte erişebilirsiniz. Özellik `Clients.Caller` bağlantı ömrü olay işleyiciyöntemleri `OnConnected`için doldurulur değil , `OnDisconnected`, ve `OnReconnected`.

`state` Nesnede veri oluşturma veya güncelleştirme `Clients.Caller` özelliği her iki yönde de çalışır. Sunucudaki değerleri güncelleştirebilirsiniz ve bunlar istemciye geri aktarılır.

Aşağıdaki örnek, her yöntem çağrısıyla sunucuya iletim için durum depolayan JavaScript istemci kodunu gösterir.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

Aşağıdaki örnekte bir .NET istemcisinde eşdeğer kod gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

Hub sınıfınızda, bu verilere özellikte `Clients.Caller` erişebilirsiniz. Aşağıdaki örnek, önceki örnekte belirtilen durumu alan kodu gösterir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> Kalıcı durum için bu mekanizma büyük miktarda veri için tasarlanmamıştır, çünkü içine `state` koyduğunuz veya `Clients.Caller` özelliğinize koyduğunuz her şey her yöntem çağırmasıyla birlikte tökezler. Kullanıcı adları veya sayaçlar gibi daha küçük öğeler için kullanışlıdır.

VB.NET veya güçlü bir şekilde yazılan hub'da, arayan durum nesnesine `Clients.Caller`erişilemez; bunun yerine, kullanın `Clients.CallerState` (SignalR 2.1 tanıtıldı):

**C'de CallerState'i kullanma #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**Visual Basic'te CallerState'i kullanma**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Hub sınıfındaki hatalar nasıl işler?

Hub sınıfı yöntemlerinizde oluşan hataları işlemek için, öncelikle async işlemlerinden (istemci yöntemleriçağırmak gibi) özel `await`durumları kullanarak "gözlemlediğinizden" emin olun. Ardından aşağıdaki yöntemlerden birini veya birkaçını kullanın:

- Yöntem kodunuzu try-catch bloklarında sarın ve özel durum nesnesini günlüğe kaydedin. Hata ayıklama amacıyla istemciye özel durum gönderebilirsiniz, ancak güvenlik nedenleriyle üretimdeki istemcilere ayrıntılı bilgi gönderilmesi önerilmez.
- [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) yöntemini işleyen bir Hubs ardışık modül oluşturun. Aşağıdaki örnekte, hataları günlüğe kaydeden bir ardışık hatlar modülü, ardından modülü Hubs ardışık hattına enjekte eden Startup.cs kod gösterilmektedir.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- `HubException` Sınıfı kullanın (SignalR 2'de tanıtıldı). Bu hata herhangi bir hub çağırma atılabilir. Oluşturucu `HubError` bir dize iletisi ve ek hata verileri depolamak için bir nesne alır. SignalR özel durumu otomatik olarak serihale getirir ve hub yöntemi çağırmasını reddetmek veya başarısız olmak için kullanılacak istemciye gönderir.

    Aşağıdaki kod örnekleri, Hub `HubException` çağırma sırasında nasıl atılacağını ve JavaScript ve .NET istemcilerinde özel durum nasıl işleyeceğini gösterir.

    **HubException sınıfını gösteren sunucu kodu**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **Hub'a HubException atmaya yanıt gösteren JavaScript istemci kodu**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **.NET istemci kodu hub'a HubException atma yanıtı gösteren**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

Hub ardışık işlem hattı modülleri hakkında daha fazla bilgi için hub'lar ardışık hattını bu konuda nasıl [özelleştirileştirin.](#hubpipeline)

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>İzlemeyi etkinleştirme

Sunucu tarafı izlemeyi etkinleştirmek için, bu örnekte gösterildiği gibi Web.config dosyanıza bir system.diagnostics öğesi ekleyin:

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Uygulamayı Visual Studio'da çalıştırdığınızda, **Çıkış** penceresindeki günlükleri görüntüleyebilirsiniz.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>İstemci yöntemlerini arama ve Hub sınıfı dışından grupları yönetme

Hub sınıfınızdan farklı bir sınıftan istemci yöntemlerini çağırmak için Hub için SignalR bağlam nesnesine bir başvuru alın ve bunu istemcideki yöntemleri çağırmak veya grupları yönetmek için kullanın.

Aşağıdaki örnek `StockTicker` sınıf bağlam nesnesini alır, sınıfın bir örneğinde depolar, sınıf örneğini statik bir özellikte depolar ve `updateStockPrice` singleton sınıf örneğindeki `StockTickerHub`bağlamı kullanır, adlı hub'a bağlı istemcilerde yöntemi aramak için .

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

Bağlamı uzun ömürlü bir nesnede birden çok kez kullanmanız gerekiyorsa, başvuruyu bir kez alın ve her seferinde yeniden almak yerine kaydedin. Bağlamı bir kez almak, SignalR'ın istemcilere Hub yöntemlerinizin istemci yöntemi çağrıları yaptığı aynı sırayla ileti göndermesini sağlar. Hub için SignalR bağlamını nasıl kullanacağımı gösteren bir öğretici için, [ASP.NET SignalR içeren Sunucu Yayını'na](../getting-started/tutorial-server-broadcast-with-signalr.md)bakın.

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>İstemci yöntemlerini arama

Hangi istemcilerin RPC'yi alacağını belirtebilirsiniz, ancak Hub sınıfından arama yaptığınızdan daha az seçeneğiniz vardır. Bunun nedeni, bağlamın bir istemciden gelen belirli bir aramayla ilişkili olmamasıdır, bu nedenle geçerli `Clients.Others`bağlantı `Clients.Caller`kimliği `Clients.OthersInGroup`hakkında bilgi gerektiren yöntemler (örneğin, veya , veya , ) kullanılamaz. Aşağıdaki seçenekler mevcuttur:

- Tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- Bağlantı kimliğiyle tanımlanan belirli bir istemci.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- Belirli bir gruptaki tüm bağlı istemciler.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında belirli bir gruptaki tüm bağlı istemciler.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

Hub sınıfınızdaki yöntemlerden Hub olmayan sınıfınızı çağırıyorsanız, geçerli bağlantı kimliğini geçirebilir ve `Clients.Client`bunu `Clients.AllExcept`, `Clients.Group` veya `Clients.Caller` `Clients.Others`simüle `Clients.OthersInGroup`etmek için , veya . Aşağıdaki örnekte, `MoveShapeHub` `Broadcaster` sınıf sınıf simüle `Clients.Others` `Broadcaster` böylece sınıfa bağlantı kimliği geçer.

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Grup üyeliğini yönetme

Grupları yönetmek için Hub sınıfındakiyle aynı seçeneklere sahipsiniz.

- Gruba istemci ekleme

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- İstemciyi gruptan kaldırma

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Hubs ardışık hattı özelleştirme

SignalR, Hub ardışık hattına kendi kodunuzu enjekte etmenizi sağlar. Aşağıdaki örnek, istemciden alınan her gelen yöntem çağrısını ve istemciye çağrılan giden yöntem çağrısını kaydeden özel bir Hub ardışık nokta modülü gösterir:

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs* dosyasındaki aşağıdaki kod, Hub ardışık alanında çalışacak modülü kaydeder:

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

Geçersiz kılabileceğiniz birçok farklı yöntem vardır. Tam liste için [HubPipelineModule Yöntemleri'ne](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)bakın.
