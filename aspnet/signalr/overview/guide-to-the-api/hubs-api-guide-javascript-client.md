---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hub'ları API Kılavuzu - JavaScript İstemci | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, tarayıcılar ve Windows Mağazası (WinJS) aplicat gibi JavaScript istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676085"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hub'ları API Kılavuzu - JavaScript İstemci

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belge, tarayıcılar ve Windows Mağazası (WinJS) uygulamaları gibi JavaScript istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar.
>
> SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar. Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız. İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız. SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.
>
> SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar. SignalR, Hub'lar ve Kalıcı [Bağlantılar'a](../getting-started/introduction-to-signalr.md)giriş için bkz.
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

- [Oluşturulan proxy ve sizin için ne yapar](#genproxy)

    - [Oluşturulan proxy ne zaman kullanılır](#cantusegenproxy)
- [İstemci Kurulumu](#clientsetup)

    - [Dinamik olarak oluşturulan proxy'ye nasıl başvurur?](#dynamicproxy)
    - [SignalR oluşturulan proxy için fiziksel bir dosya oluşturma](#manualproxy)
- [Bağlantı kurma](#establishconnection)

    - [$.connection.hub, $.hubConnection() tarafından yapılan nesnedir](#connequivalence)
    - [Başlangıç yönteminin eşzamanlı yürütmesi](#asyncstart)
- [Etki alanları arası bağlantı nasıl kurulur?](#crossdomain)
- [Bağlantı nasıl yapılandırılabilen](#configureconnection)

    - [Sorgu dize parametreleri nasıl belirtilir?](#querystring)
    - [Taşıma yöntemi nasıl belirtilir?](#transport)
- [Hub sınıfı için proxy nasıl edinilir?](#getproxy)
- [Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?](#callclient)
- [İstemciden sunucu yöntemleri nasıl çağrılır?](#callserver)
- [Bağlantı ömrü olayları nasıl işler?](#connectionlifetime)
- [Hataları işleme](#handleerrors)
- [İstemci tarafı günlüğe kaydetmeyi etkinleştirme](#logging)

Sunucu veya .NET istemcilerinin nasıl programlanır, aşağıdaki kaynaklara bakın:

- [SignalR Hub'lar API Kılavuzu - Sunucu](hubs-api-guide-server.md)
- [SignalR Hub'lar API Kılavuzu - .NET İstemci](hubs-api-guide-net-client.md)

SignalR 2 sunucu bileşeni yalnızca .NET 4.5'te kullanılabilir (ancak SignalR 2 için .NET 4.0'da bir .NET istemcisi vardır).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>Oluşturulan proxy ve sizin için ne yapar

SignalR'ın sizin için ürettiği bir proxy ile veya olmadan bir SignalR hizmetiyle iletişim kurmak için bir JavaScript istemcisini programlayabilirsiniz. Proxy'nin sizin için yaptığı şey, bağlanmak, sunucunun çağırdığı yöntemleri yazmak ve sunucuda arama yöntemlerini kullanmak için kullandığınız kodun sözdizimini basitleştirmektir.

Sunucu yöntemlerini aramak için kod yazdığınızda, oluşturulan proxy, yerel bir işlev icra ediyormuşsunuz gibi `serverMethod(arg1, arg2)` görünen `invoke('serverMethod', arg1, arg2)`sözdizimini kullanmanızı sağlar: yerine yazabilirsiniz. Oluşturulan proxy sözdizimi, bir sunucu yöntemi adını yanlış yazarsanız, anında ve anlaşılır bir istemci tarafı hatası da sağlar. Vekilleri tanımlayan dosyayı el ile oluşturursanız, sunucu yöntemlerini çağıran kod yazmak için IntelliSense desteği de alabilirsiniz.

Örneğin, sunucuda aşağıdaki Hub sınıfına sahip olduğunuzu varsayalım:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Aşağıdaki kod örnekleri, JavaScript kodunun sunucuda `NewContosoChatMessage` yöntemi çağırmak ve yöntemin `addContosoChatMessageToPage` çağrılarını sunucudan almak için nasıl göründüğünü gösterir.

**Oluşturulan proxy ile**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Oluşturulan proxy olmadan**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Oluşturulan proxy ne zaman kullanılır

Sunucunun çağırdığı bir istemci yöntemi için birden çok olay işleyicisi kaydetmek istiyorsanız, oluşturulan proxy'yi kullanamazsınız. Aksi takdirde, oluşturulan proxy'yi kullanmayı veya kodlama tercihinize göre kullanmayı seçebilirsiniz. Kullanmamayı seçerseniz, istemci kodunuzdaki bir `script` öğedeki "sinyal/hub" URL'sine başvurmanız gerekmez.

<a id="clientsetup"></a>

## <a name="client-setup"></a>İstemci kurulumu

Bir JavaScript istemcisi jQuery ve SignalR çekirdek JavaScript dosyasına referanslar gerektirir. jQuery sürümü 1.7.2, 1.8.2 veya 1.9.1 gibi 1.6.4 veya daha sonraki büyük sürümler olmalıdır. Oluşturulan proxy kullanmaya karar verirseniz, ayrıca SignalR oluşturulan proxy JavaScript dosyasına bir başvuru gerekir. Aşağıdaki örnek, oluşturulan proxy'yi kullanan bir HTML sayfasında başvuruların nasıl görünebileceğini gösterir.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

Bu başvurular bu sıraya eklenmelidir: jQuery ilk, SignalR çekirdek bundan sonra, ve SignalR yakınlık son.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Dinamik olarak oluşturulan proxy'ye nasıl başvurur?

Önceki örnekte, SignalR oluşturulan proxy başvuru dinamik olarak oluşturulan JavaScript kodu değil, fiziksel bir dosya için. SignalR anında proxy için JavaScript kodu oluşturur ve "/signalr/hubs" URL'sine yanıt olarak istemciye hizmet eder. Yönteminizle sunucuda SignalR bağlantıları için farklı bir `MapSignalR` temel URL belirttiyseniz, dinamik olarak oluşturulan proxy dosyasının URL'si, "/hub"ların ekildiği özel URL'nizdir.

> [!NOTE]
> Windows 8 (Windows Mağazası) JavaScript istemcileri için, dinamik olarak oluşturulan dosya yerine fiziksel proxy dosyasını kullanın. Daha fazla bilgi için, bu konuda daha sonra [oluşturulan SignalR proxy için fiziksel bir dosya nın nasıl oluşturulabildiğini](#manualproxy) görün.

MVC 4 veya 5 Jilet görünümüASP.NET, proxy dosyası başvurunuzdaki uygulama köküne başvurmak için tilde'yi kullanın:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

SignalR'ı MVC 5'te kullanma hakkında daha fazla bilgi için [SignalR ve MVC 5 ile başlarken](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)bakın.

MVC 3 Jilet görünümünde `Url.Content` ASP.NET, proxy dosya başvurunuz için kullanın:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

bir ASP.NET Web Forms `ResolveClientUrl` uygulamasında, yakınlık dosya başvurunuz için kullanın veya uygulama kökü göreli bir yol kullanarak ScriptManager üzerinden kaydedin (tilde ile başlayarak):

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

Genel bir kural olarak, CSS veya JavaScript dosyaları için kullandığınız "/signalr/hub" URL'sini belirtmek için aynı yöntemi kullanın. Tilde kullanmadan bir URL belirtirseniz, bazı senaryolarda Uygulamanız IIS Express'i kullanarak Visual Studio'da test ettiğinizde doğru çalışır, ancak tam IIS'ye dağıtığınızda 404 hatasıyla başarısız olur. Daha fazla bilgi için, MSDN sitesindeki [Web Projelerini ASP.NET için Visual Studio'daki Web Sunucularında](https://msdn.microsoft.com/library/58wxa9w5.aspx) **Kök Düzeyi Kaynaklara Yapılan Başvuruları Çözme'ye** bakın.

Visual Studio 2017'de hata ayıklama modunda bir web projesi çalıştırdığınızda ve Tarayıcınız olarak Internet Explorer kullanıyorsanız, **Solution Explorer'da** Komut Dosyaları altında proxy **dosyasını**görebilirsiniz.

Dosyanın içeriğini görmek için **hub'ları**çift tıklatın. Visual Studio 2012 veya 2013 ve Internet Explorer kullanmıyorsanız veya hata ayıklama modunda değilseniz, "/signalR/hubs" URL'sine göz atarak dosyanın içeriğini de alabilirsiniz. Örneğin, siteniz de `http://localhost:56699`çalışıyorsa, `http://localhost:56699/SignalR/hubs` tarayıcınıza gidin.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR oluşturulan proxy için fiziksel bir dosya oluşturma

Dinamik olarak oluşturulan proxy'ye alternatif olarak, proxy koduna sahip fiziksel bir dosya oluşturabilir ve bu dosyaya başvuruyapabilirsiniz. Önbelleğe alma veya birleştirme davranışı üzerinde denetim için veya sunucu yöntemleri aramaları kodlarken IntelliSense almak için bunu yapmak isteyebilirsiniz.

Proxy dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:

1. [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet paketini yükleyin.
2. Bir komut istemi açın ve SignalR.exe dosyasını içeren *araçlar* klasörüne göz atın. Araçlar klasörü aşağıdaki konumdadır:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. Aşağıdaki komutu girin:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.dll'nize* giden yol genellikle proje klasörünüzdeki *çöp kutusu* klasörüdür.

    Bu komut *signalr.exe*ile aynı klasörde *server.js* adlı bir dosya oluşturur.
4. *Server.js* dosyasını projenizdeki uygun bir klasöre koyun, uygulamanız için uygun şekilde yeniden adlandırın ve "sinyalci/hub" başvurusu yerine bir referans ekleyin.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Bağlantı kurma

Bağlantı kurmadan önce, bir bağlantı nesnesi oluşturmanız, proxy oluşturmanız ve sunucudan çağrılabilen yöntemler için olay işleyicilerini kaydetmeniz gerekir. Proxy ve olay işleyicileri ayarlandığında, yöntemi arayarak `start` bağlantıyı kurun.

Oluşturulan proxy kullanıyorsanız, oluşturulan proxy kodu sizin için yapar, çünkü kendi kodunda bağlantı nesnesi oluşturmak zorunda değilsiniz.

<a id="nogenconnection"></a>

**Bağlantı kurma (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Bağlantı kurma (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır. Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.

Varsayılan olarak, hub konumu geçerli sunucudur; farklı bir sunucuya bağlanıyorsanız, `start` aşağıdaki örnekte gösterildiği gibi yöntemi aramadan önce URL'yi belirtin:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> Normalde bağlantıyı kurmak için yöntemi çağırmadan `start` önce olay işleyicilerini kaydedersiniz. Bağlantıyı kurduktan sonra bazı olay işleyicilerini kaydetmek istiyorsanız, bunu yapabilirsiniz, ancak `start` yöntemi aramadan önce olay işleyicinizden en az birini kaydetmeniz gerekir. Bunun bir nedeni, bir uygulamada çok sayıda Hub olabilir, ancak yalnızca bunlardan `OnConnected` birini kullanacaksanız, her Hub'da olayı tetiklemek istemezsiniz. Bağlantı kurulduğunda, Bir Hub'ın proxy'sindeki istemci yönteminin `OnConnected` varlığı SignalR'a olayı tetiklemasını söyler. `start` Yöntemi aramadan önce herhangi bir olay işleyicisi kaydetmezseniz, Hub'da yöntemleri çağırabilirsiniz, `OnConnected` ancak Hub'ın yöntemi çağrılmaz ve sunucudan istemci yöntemleri çağrılmaz.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connection.hub, $.hubConnection() tarafından yapılan nesnedir

Örneklerden de görebileceğiniz gibi, oluşturulan proxy'yi kullandığınızda bağlantı `$.connection.hub` nesnesi başvurur. Bu, oluşturulan proxy'yi kullanmadığınızda arayarak `$.hubConnection()` elde ettiğiniz nesneyle aynıdır. Oluşturulan proxy kodu aşağıdaki deyimi çalıştırarak sizin için bağlantı oluşturur:

![Oluşturulan proxy dosyasında bağlantı oluşturma](hubs-api-guide-javascript-client/_static/image3.png)

Oluşturulan proxy'yi kullanırken, oluşturulan proxy'yi kullanmadığınızda bağlantı nesnesiyle yapabileceğiniz her şeyi `$.connection.hub` yapabilirsiniz.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Başlangıç yönteminin eşzamanlı yürütmesi

Yöntem `start` eşsenkronize yürütülür. Bir [jQuery Ertelenmiş nesne](http://api.jquery.com/category/deferred-object/)döndürür , bu da gibi `pipe`arama yöntemleri `done`ekleyerek `fail`geri arama işlevleri ekleyebilirsiniz anlamına gelir , , ve . Bağlantı kurulduktan sonra yürütmek istediğiniz kodunuz (sunucu yöntemine çağrı gibi) varsa, bu kodu geri arama işlevine koyun veya geri arama işlevinden arayın. Geri `.done` arama yöntemi, bağlantı kurulduktan sonra ve sunucudaki olay işleyicisi yönteminizde `OnConnected` bulunan herhangi bir kod dan sonra yürütmeyi tamamlar.

`start` Yöntem çağrısından sonra `.done` (geri aramada değil) sonraki kod satırı olarak önceki örnekteki "Şimdi bağlı" deyimini koyarsanız, `console.log` aşağıdaki örnekte gösterildiği gibi, bağlantı kurulmadan önce satır yürütülür:

![Bağlantı kurulduktan sonra çalışan kod yazmak için yanlış yol](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>Etki alanları arası bağlantı nasıl kurulur?

Genellikle tarayıcı bir sayfa `http://contoso.com`yükler, SinyalR bağlantısı aynı etki alanında, at `http://contoso.com/signalr`. Sayfa, `http://contoso.com` `http://fabrikam.com/signalr`etki alanı arası bağlantıyla bağlantı yapıyorsa. Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışı bırakılır.

SignalR 1.x'te, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağı tarafından denetlendi. Bu bayrak hem JSONP hem de CORS isteklerini denetler. Daha fazla esneklik için, tüm CORS desteği SignalR'ın sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının bunu desteklediği algılanırsa hala KORS'u kullanır) ve bu senaryoları desteklemek için yeni OWIN ara yazılımları kullanıma sunulmuştur.

İstemci üzerinde JSONP gerekiyorsa (eski tarayıcılarda etki alanları arası isteklerini desteklemek için), `EnableJSONP` aşağıda `HubConfiguration` gösterildiği `true`gibi nesne üzerinde ayarlayarak açıkça etkinleştirilmesi gerekir. JSONP, CORS'ten daha az güvenli olduğu için varsayılan olarak devre dışı bırakılır.

**Microsoft.Owin.Cors'un projenize eklenmesi:** Bu kitaplığı yüklemek için Paket Yöneticisi Konsolunda aşağıdaki komutu çalıştırın:

`Install-Package Microsoft.Owin.Cors`

Bu komut, paketin 2.1.0 sürümünü projenize ekler.

### <a name="calling-usecors"></a>UseCors'u Arama

 Aşağıdaki kod snippet SignalR 2'de etki alanları arası bağlantıların nasıl uygulanacağını gösterir.

**SignalR 2'de etki alanları arası isteklerin uygulanması**

Aşağıdaki kod, SignalR 2 projesinde CORS veya JSONP'nin nasıl etkinleştirilen gösteriş olduğunu gösterir. Bu kod `Map` örneği, `RunSignalR` `MapSignalR`CORS ara yazılımının yalnızca CORS desteği gerektiren SignalR istekleri için (belirtilen `MapSignalR`yoldaki tüm trafikler yerine . Harita, tüm uygulama yerine belirli bir URL öneki için çalışması gereken diğer ara yazılımlar için de kullanılabilir.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - Kodunuzda doğru `jQuery.support.cors` şekilde ayarlanma.
>
>     ![jQuery.support.cors'u doğru ayarlamayın](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR, CORS kullanımını yönetir. SignalR'ın tarayıcının CORS'u desteklediğini varsayması nedeniyle JSONP'yi gerçek devre dışı bırakırsa ayar. `jQuery.support.cors`
> - Yerel barındırma URL'sine bağlandığınızda, Internet Explorer 10 bunu etki alanı arası bağlantı olarak kabul etmez, bu nedenle sunucuda etki alanları arası bağlantıları etkinleştirmeseniz bile uygulama IE 10 ile yerel olarak çalışır.
> - Internet Explorer 9 ile etki alanı arası bağlantıları kullanma hakkında bilgi için [bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)bakın.
> - Chrome ile etki alanı arası bağlantıları kullanma hakkında daha fazla bilgi için [bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)bakın.
> - Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır. Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Bağlantı nasıl yapılandırılabilen

Bir bağlantı kurmadan önce, sorgu dize parametrelerini belirtebilir veya aktarım yöntemini belirtebilirsiniz.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Sorgu dize parametreleri nasıl belirtilir?

İstemci bağlandığında sunucuya veri göndermek istiyorsanız, sorgu dize parametrelerini bağlantı nesnesine ekleyebilirsiniz. Aşağıdaki örnekler, istemci kodunda bir sorgu dize parametresi nasıl ayarlanır gösterilmektedir.

**Başlangıç yöntemini çağırmadan önce sorgu dize değeri ayarlama (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Başlangıç yöntemini çağırmadan önce sorgu dize değeri ayarlama (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

Aşağıdaki örnekte, sunucu kodunda sorgu dize parametresi nasıl okunulup okunulduğu gösterilmektedir.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Taşıma yöntemi nasıl belirtilir?

Bağlanma işleminin bir parçası olarak, bir SignalR istemcisi normalde sunucu ile hem sunucu hem de istemci tarafından desteklenen en iyi aktarım belirlemek için görüşür. Hangi aktarımkullanmak istediğinizi zaten biliyorsanız, yöntemi aradığınızda aktarım yöntemini belirterek bu işlem işlemini `start` atlayabilirsiniz.

**Aktarım yöntemini belirten istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**Aktarım yöntemini belirten istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

Alternatif olarak, SignalR'ın denemesini istediğiniz sırada birden çok aktarım yöntemi belirtebilirsiniz:

**Özel bir aktarım geri dönüş düzeni belirten istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Özel bir aktarım geri dönüş düzeni belirten istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Aktarım yöntemini belirtmek için aşağıdaki değerleri kullanabilirsiniz:

- "webSockets"
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

Aşağıdaki örnekler, bağlantı tarafından hangi aktarım yönteminin kullanıldığını nasıl bulabileceğinizi gösterir.

**Bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**Bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

Sunucu kodunda aktarım yöntemini nasıl kontrol edeceğimiz hakkında bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Bağlam özelliğinden istemci hakkında nasıl bilgi alınır.](hubs-api-guide-server.md#contextproperty) Taşımalar ve geri dönüşler hakkında daha fazla bilgi için [SignalR'a Giriş - Taşımalar ve Geri Dönüşler'](../getting-started/introduction-to-signalr.md#transports)e bakın.

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>Hub sınıfı için proxy nasıl edinilir?

Oluşturduğunuz her bağlantı nesnesi, bir veya daha fazla Hub sınıfı içeren bir SignalR hizmetine bağlantı hakkındaki bilgileri kapsüller. Hub sınıfıyla iletişim kurmak için, kendi oluşturduğunuz (oluşturulan proxy'yi kullanmıyorsanız) veya sizin için oluşturulan bir proxy nesnesi kullanırsınız.

İstemci üzerinde proxy adı Hub sınıf adının deve kasalı bir sürümüdür. SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.

**Sunucuda hub sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**Hub için oluşturulan istemci proxy'sine başvuru alma**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**Hub sınıfı için istemci proxy'si oluşturma (oluşturulan proxy olmadan)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

Hub sınıfınızı bir `HubName` öznitelikle dekore ederseniz, büyük/küçük harf değiştirmeden tam adı kullanın.

**HubName özniteliği ile sunucuda Hub sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**Hub için oluşturulan istemci proxy'sine başvuru alma**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**Hub sınıfı için istemci proxy'si oluşturma (oluşturulan proxy olmadan)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?

Sunucunun Hub'dan çağırabileceği bir yöntem tanımlamak için, oluşturulan proxy'nin `client` özelliğini kullanarak Hub proxy'sine bir olay işleyicisi ekleyin veya oluşturulan proxy'yi kullanmıyorsanız `on` yöntemi arayın. Parametreler karmaşık nesneler olabilir.

Bağlantıyı kurmak için yöntemi çağırmadan `start` önce olay işleyicisini ekleyin. (Yöntemi aradıktan sonra olay işleyicileri eklemek istiyorsanız, bu belgede daha önce [bağlantı kurma notu](#establishconnection) na bakın ve oluşturulan proxy'yi kullanmadan bir yöntem tanımlamak için gösterilen sözdizimini kullanın.) `start`

Yöntem adı eşleştirme büyük/küçük harf duyarsız. Örneğin, `Clients.All.addContosoChatMessageToPage` sunucuda , `AddContosoChatMessageToPage` `addContosoChatMessageToPage`veya `addcontosochatmessagetopage` istemci üzerinde yürütülür.

**İstemci üzerinde yöntemi tanımlama (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**İstemci de yöntemi tanımlamak için alternatif yol (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**İstemci üzerinde yöntemi tanımlayın (oluşturulan proxy olmadan veya başlat yöntemini çağırdıktan sonra eklerken)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**İstemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

Aşağıdaki örnekler, yöntem parametresi olarak karmaşık bir nesne içerir.

**Karmaşık bir nesne alan istemcide yöntem tanımlama (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**Karmaşık bir nesne alan istemcide yöntem tanımlama (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**Karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>İstemciden sunucu yöntemleri nasıl çağrılır?

İstemciden sunucu yöntemini çağırmak `server` için, oluşturulan proxy'yi kullanmıyorsanız oluşturulan proxy'nin özelliğini veya Hub proxy'deki `invoke` yöntemi kullanın. İade değeri veya parametreler karmaşık nesneler olabilir.

Hub'daki yöntem adının deve kılıfı sürümünde geçirin. SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.

Aşağıdaki örnekler, iade değeri olmayan bir sunucu yönteminin nasıl çağrılmasını ve iade değeri olan bir sunucu yönteminin nasıl çağrılmasını gösterir.

**HubMethodName özniteliği olmayan sunucu yöntemi**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**Parametrede geçirilen karmaşık nesneyi tanımlayan sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Hub yöntemini bir `HubMethodName` öznitelikle dekore ettiyseniz, büyük/küçük harf değiştirmeden bu adı kullanın.

HubMethodName özniteliği olan **sunucu yöntemi**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

Önceki örnekler, iade değeri olmayan bir sunucu yönteminin nasıl çağrılmasını gösterir. Aşağıdaki örnekler, iade değeri olan bir sunucu yönteminin nasıl çağrılmasını gösterir.

**İade değeri olan bir yöntemiçin sunucu kodu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

İade değeri **için kullanılan Stok sınıfı**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Bağlantı ömrü olayları nasıl işler?

SignalR işleyebilir aşağıdaki bağlantı ömrü olayları sağlar:

- `starting`: Bağlantı üzerinden herhangi bir veri gönderilmeden önce yükseltilir.
- `received`: Bağlantıdan herhangi bir veri alındığı zaman yükseltilir. Alınan verileri sağlar.
- `connectionSlow`: İstemci yavaş veya sık sık bırakarak bağlantı algıladığında yükseltilir.
- `reconnecting`: Altta yatan aktarım yeniden bağlanmaya başladığında yükseltilir.
- `reconnected`: Temel taşıma yeniden bağlandığında yükseltilir.
- `stateChanged`: Bağlantı durumu değiştiğinde yükseltilir. Eski durumu ve yeni durumu (Bağlama, Bağlama, Yeniden Bağlanma veya Bağlantı Kesme) sağlar.
- `disconnected`: Bağlantı kesildiğinde yükseltilir.

Örneğin, fark edilebilir gecikmelere neden olabilecek bağlantı sorunları olduğunda uyarı iletilerini görüntülemek `connectionSlow` istiyorsanız, olayı ele alın.

**Bağlantıyı işlemeSlow olayı (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**Bağlantıyı işlemeSlow olayı (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Hataları işleme

SignalR JavaScript istemcisi için bir işleyici ekleyebileceğiniz bir `error` olay sağlar. Sunucu yöntemi çağırmasından kaynaklanan hatalar için işleyici eklemek için başarısız yöntemini de kullanabilirsiniz.

Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, SignalR'ın hatadan sonra döndürdİğİ özel durum nesnesi hata hakkında en az bilgi içerir. Örneğin, bir çağrı `newContosoChatMessage` başarısız olursa, hata nesnesindeki`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`hata iletisi " " Üretimdeki istemcilere ayrıntılı hata iletileri göndermek güvenlik nedenleriyle önerilmez, ancak sorun giderme amacıyla ayrıntılı hata iletilerini etkinleştirmek istiyorsanız, sunucudaki aşağıdaki kodu kullanın.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

Aşağıdaki örnekte, hata olayı için işleyici nasıl ekleyeceğiniz gösterilmektedir.

**Hata işleyicisi ekleme (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**Hata işleyicisi ekleme (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

Aşağıdaki örnek, bir yöntem çağırma bir hata işlemek için nasıl gösterir.

**Yöntem çağırmadan gelen bir hatayı işleme (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**Yöntem çağırmasından bir hata işleme (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Bir yöntem çağırma başarısız `error` olursa, olay da yükseltilir, `error` bu nedenle yöntem `.fail` işleyicisi ve yöntem geri arama kodu yürütülür.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>İstemci tarafı günlüğe kaydetmeyi etkinleştirme

Bağlantıda istemci tarafı günlüğe kaydetmeyi `logging` etkinleştirmek için, bağlantıyı `start` kurmak için yöntemi çağırmadan önce özelliği bağlantı nesnesi üzerinde ayarlayın.

**Günlüğü etkinleştirme (oluşturulan proxy ile)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**Günlüğü etkinleştirme (oluşturulan proxy olmadan)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Günlükleri görmek için tarayıcınızın geliştirici araçlarını açın ve Konsol sekmesine gidin. Bunu nasıl yapacağını gösteren adım adım yönergeleri ve ekran görüntülerini gösteren bir öğretici için, ASP.NET Signalr ile Sunucu Yayını ' na bakın [- Günlük'u etkinleştirin.](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)
