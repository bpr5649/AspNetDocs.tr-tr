---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR'a Giriş | Microsoft Dokümanlar
author: bradygaster
description: Bu makalede SignalR'ın ne olduğu ve oluşturmak için tasarladığı çözümlerden bazıları açıklanmaktadır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676351"
---
# <a name="introduction-to-signalr"></a>SignalR’a Giriş

tarafından [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede SignalR'ın ne olduğu ve oluşturmak için tasarladığı çözümlerden bazıları açıklanmaktadır. 
> 
> ## <a name="questions-and-comments"></a>Sorular ve yorumlar
> 
> Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)gönderebilirsiniz.

## <a name="what-is-signalr"></a>SignalR nedir?

ASP.NET SignalR, ASP.NET geliştiriciler için, uygulamalara gerçek zamanlı web işlevselliği ekleme işlemini kolaylaştıran bir kitaplıktır. Gerçek zamanlı web işlevi, sunucunun istemcinin yeni veri istemesini beklemesi yerine, sunucu kodunun içeriği kullanılabilir hale geldiğinde bağlı istemcilere anında itme sidir.

SignalR, ASP.NET uygulamanıza her türlü "gerçek zamanlı" web işlevselliği eklemek için kullanılabilir. Sohbet genellikle bir örnek olarak kullanılırken, çok daha fazlasını yapabilirsiniz. Bir kullanıcı yeni verileri görmek için bir web sayfasını yenilese veya sayfa yeni veri almak için [uzun yoklama](http://en.wikipedia.org/wiki/Push_technology#Long_polling) lar uyguladığında, SignalR'ı kullanmaya aday olur. Örnekler arasında panolar ve izleme uygulamaları, ortak uygulamalar (belgelerin eşzamanlı olarak düzenlenmesi gibi), iş ilerleme güncelleştirmeleri ve gerçek zamanlı formlar yer almaktadır.

SignalR ayrıca sunucudan yüksek frekansgüncellemeleri gerektiren tamamen yeni web uygulamaları türlerine de olanak tanır, örneğin gerçek zamanlı oyun.

SignalR, sunucu tarafındaki .NET kodundan istemci tarayıcılarında (ve diğer istemci platformlarında) JavaScript işlevlerini çağıran sunucudan istemciye uzak yordam çağrıları (RPC) oluşturmak için basit bir API sağlar. SignalR ayrıca bağlantı yönetimi (örneğin, bağlantı ve bağlantı bağlantılarını ayırmak) ve bağlantıları gruplandırma için API'yi de içerir.

![SignalR ile çekme yöntemleri](introduction-to-signalr/_static/image1.png)

SignalR, bağlantı yönetimini otomatik olarak işler ve bir sohbet odasında olduğu gibi, iletileri bağlı tüm istemcilere yayınlamanıza olanak tanır. İletileri belirli istemcilere de gönderebilirsiniz. Bağlantının her iletişimde tekrar kurulduğu klasik bir HTTP bağlantısının aksine, istemci ve sunucu arasındaki bağlantı kalıcıdır.

SignalR, sunucu kodunun bugün web'de yaygın olan istek yanıt modeli yerine Uzaktan Yordam Çağrıları (RPC) kullanarak tarayıcıdaki istemci koduna çağrılabildiği "sunucu itme" işlevini destekler.

SignalR uygulamaları, yerleşik ve üçüncü taraf ölçeklendirme sağlayıcılarını kullanarak binlerce istemciye ölçeklenebilir.

Yerleşik sağlayıcılar şunlardır:
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Üçüncü taraf sağlayıcılar şunlardır:
* [NÖnbellek](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR açık kaynak kodludur, [GitHub](https://github.com/signalr)üzerinden erişilebilir.

## <a name="signalr-and-websocket"></a>SignalR ve WebSocket

SignalR, mevcut olduğu yerlerde yeni WebSocket aktarımını kullanır ve gerektiğinde eski taşımaaraçlarına geri döner. Kesinlikle doğrudan WebSocket kullanarak uygulama nızı yazabilirsiniz iken, SignalR kullanarak uygulamak için gereken ekstra işlevsellik bir çok zaten sizin için yapılır anlamına gelir. En önemlisi, bu, eski istemciler için ayrı bir kod yolu oluşturma konusunda endişelenmenize gerek kalmadan uygulamanızı WebSocket'den yararlanmak için kodlayabileceğiniz anlamına gelir. SignalR, uygulamanızın WebSocket sürümleri arasında tutarlı bir arayüz sağlayarak temel aktarımdaki değişiklikleri destekleyecek şekilde güncelleştirilediğinden, SignalR sizi WebSocket'teki güncellemeler hakkında endişelenmenize karşı da koruma sağlar.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Taşımalar ve geri dönüşler

SignalR istemci ve sunucu arasında gerçek zamanlı çalışma yapmak için gerekli olan bazı aktarımlar üzerinde bir soyutlama. SignalR bağlantısı HTTP olarak başlar ve varsa WebSocket bağlantısına yükseltilir. WebSocket SignalR için ideal bir aktarımdır, sunucu belleği en verimli şekilde kullanır, en düşük gecikme ye sahiptir ve en temel özelliklere sahiptir (istemci ve sunucu arasındaki tam çift yönlü iletişim gibi), ancak aynı zamanda en sıkı gereksinimlere sahiptir: WebSocket sunucunun Windows Server 2012 veya Windows 8 ve .NET Framework 4.5'i kullanmasını gerektirir. Bu gereksinimler karşılanmazsa, SignalR bağlantılarını yapmak için diğer aktarımları kullanmaya çalışır.

### <a name="html-5-transports"></a>HTML 5 taşımaları

Bu aktarımlar [HTML 5](http://en.wikipedia.org/wiki/HTML5)desteğine bağlıdır. İstemci tarayıcısı HTML 5 standardını desteklemiyorsa, eski aktarımlar kullanılır.

- **WebSocket** (hem sunucu hem de tarayıcı Websocket'i destekleyebilirlerini gösteriyorsa). WebSocket, istemci ve sunucu arasında kalıcı, iki yönlü gerçek bir bağlantı kuran tek aktarımdır. Ancak, WebSocket da en sıkı gereksinimleri vardır; yalnızca Microsoft Internet Explorer, Google Chrome ve Mozilla Firefox'un en son sürümlerinde tam olarak desteklenir ve opera ve safari gibi diğer tarayıcılarda yalnızca kısmi bir uygulama vardır.
- **Sunucu Gönderilen Olaylar**, ayrıca EventSource olarak bilinen (tarayıcı Temelde Internet Explorer hariç tüm tarayıcılar Sunucu Gönderilen Olaylar, destekliyorsa.)

### <a name="comet-transports"></a>Kuyruklu yıldız taşımaları

Aşağıdaki aktarımlar, bir tarayıcının veya başka bir istemcinin, istemci özellikle istemeden verileri istemciye taşımak için kullanabileceği uzun süreli bir HTTP isteğini koruduğu [Kuyruklu Yıldız](http://en.wikipedia.org/wiki/Comet_(programming)) web uygulama modeline dayanır.

- **Forever Frame** (yalnızca Internet Explorer için). Forever Frame, tamamlanmayan sunucuda bir bitiş noktasına istekte bulunan gizli bir IFrame oluşturur. Sunucu daha sonra komut dosyasını istemciye sürekli olarak gönderir ve bu komut dosyası hemen yürütülür ve sunucudan istemciye tek yönlü gerçek zamanlı bağlantı sağlar. İstemciden sunucuya bağlantı sunucudan istemci bağlantısına ayrı bir bağlantı kullanır ve standart bir HTTP isteği gibi, gönderilmesi gereken her veri parçası için yeni bir bağlantı oluşturulur.
- **Ajax uzun yoklama**. Uzun yoklama kalıcı bir bağlantı oluşturmaz, ancak bunun yerine sunucu yanıt verene kadar açık kalan bir istekle sunucuyu yoklar ve bu noktada bağlantı kapanır ve hemen yeni bir bağlantı istenir. Bu, bağlantı sıfırlanırken bazı gecikme sürelerini başlatabilir.

Hangi aktarımların hangi yapılandırmalar altında desteklendiği hakkında daha fazla bilgi için desteklenen [Platformlar'a](supported-platforms.md)bakın.

### <a name="transport-selection-process"></a>Taşıma seçim süreci

Aşağıdaki liste, SignalR'in hangi aktarımın kullanılacağına karar vermek için kullandığı adımları gösterir.

1. Tarayıcı Internet Explorer 8 veya daha önceyse, Uzun Yoklama kullanılır.
2. JSONP yapılandırılırsa (diğer bir `jsonp` şekilde, parametre bağlantı `true` başlatıldığında ayarlanır), Uzun Yoklama kullanılır.
3. Etki alanları arası bağlantı yapılıyorsa (diğer bir deyişle, SignalR bitiş noktası barındırma sayfasıyla aynı etki alanında değilse), aşağıdaki ölçütler karşılanırsa WebSocket kullanılır:

   - İstemci CORS 'u (Çapraz Kaynak Paylaşımı) destekler. Hangi müşterilerin CORS'u desteklediği ne kadar ayrıntılı bilgi [için, caniuse.com'da CORS'e](http://www.caniuse.com/CORS)bakın.
   - İstemci WebSocket'i destekler
   - Sunucu WebSocket destekler

     Bu ölçütlerden herhangi biri karşılanmazsa, Uzun Yoklama kullanılacaktır. Etki alanları arası bağlantılar hakkında daha fazla bilgi için, [etki alanları arası bağlantı nın nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)öğrenin.
4. JSONP yapılandırılmamışsa ve bağlantı etki alanı arası değilse, hem istemci hem de sunucu destekliyorsa WebSocket kullanılır.
5. İstemci veya sunucu WebSocket'i desteklemiyorsa, varsa Sunucu Gönderilen Olaylar kullanılır.
6. Sunucu Gönderilen Olaylar kullanılamıyorsa, Forever Frame denenir.
7. Forever Frame başarısız olursa, Uzun Yoklama kullanılır.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Taşımaların izlenmesi

Hub'ınızda günlüğe kaydetmeyi etkinleştirerek ve tarayıcınızdaki konsol penceresini açarak uygulamanızın hangi taşımayı kullandığını belirleyebilirsiniz.

Hub'ınızın bir tarayıcıdaki olayları nın günlüğe kaydedilmesini etkinleştirmek için istemci uygulamanıza aşağıdaki komutu ekleyin:

`$.connection.hub.logging = true;`

- Internet Explorer'da F12 tuşuna basarak geliştirici araçlarını açın ve Konsol sekmesini tıklatın.

    ![Microsoft Internet Explorer konsolu](introduction-to-signalr/_static/image2.png)
- Chrome'da Ctrl+Shift+J tuşuna basarak konsolu açın.

    ![Google Chrome'da Konsol](introduction-to-signalr/_static/image3.png)

Konsol açık ve günlüğe kaydetme etkin olduğunda, SignalR tarafından hangi aktarımın kullanıldığını görebilirsiniz.

![Internet Explorer'da WebSocket aktarımLarını gösteren konsol](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Aktarım belirtme

Aktarım üzerinde anlaşma kakma belirli bir süre ve istemci/sunucu kaynakları alır. İstemci yetenekleri biliniyorsa, istemci bağlantısı başlatıldığında bir aktarım belirtilebilir. Aşağıdaki kod snippet, istemcinin başka bir protokolü desteklemediği biliniyorsa, Ajax Uzun Yoklama aktarımını kullanarak bağlantı kurmayı gösterir:

`connection.start({ transport: 'longPolling' });`

İstemci sırayla belirli aktarımları denemek istiyorsanız bir geri dönüş sırası belirtebilirsiniz. Aşağıdaki kod snippet WebSocket çalışırken gösterir, ve başarısız, doğrudan Uzun Yoklama gidiyor.

`connection.start({ transport: ['webSockets','longPolling'] });`

Aktarımları belirtmek için dize sabitleri aşağıdaki gibi tanımlanır:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Bağlantılar ve Hub'lar

SignalR API istemciler ve sunucular arasında iletişim kurmak için iki model içerir: Kalıcı Bağlantılar ve Hub'lar.

Bağlantı, tek alıcı, gruplu veya yayın iletileri göndermek için basit bir bitiş noktasını temsil eder. Kalıcı Bağlantı API'si (PersistentConnection sınıfı tarafından .NET kodunda temsil edilir) geliştiriciye SignalR'ın sunduğu alt düzey iletişim protokolüne doğrudan erişim sağlar. Bağlantılar iletişim modelini kullanmak, Windows Communication Foundation gibi bağlantı tabanlı API'leri kullanan geliştiriciler için tanıdık olacaktır.

Hub, bağlantı API'si üzerine inşa edilmiş ve istemcinizin ve sunucunuzun yöntemleri doğrudan birbirleri üzerinde aramasına olanak tanıyan daha üst düzey bir ardışık sistem dir. SignalR, makine sınırları ötesine, istemcilerin sunucudaki yöntemleri yerel yöntemler kadar kolay aramasına izin vererek, bunun tam tersi gibi, makine sınırları ötesine göndermeyi işler. Hubs iletişim modelini kullanmak, .NET Remoting gibi uzaktan çağırma API'leri kullanan geliştiriciler için tanıdık olacaktır. Hub kullanmak, güçlü bir şekilde yazılan parametreleri yöntemlere geçirmenize olanak sağlayarak model bağlamayı sağlar.

### <a name="architecture-diagram"></a>Mimari diyagramı

Aşağıdaki diyagram, Hub'lar, Kalıcı Bağlantılar ve taşımalar için kullanılan temel teknolojiler arasındaki ilişkiyi gösterir.

![API'leri, taşımaları ve istemcileri gösteren SignalR Mimari Diyagramı](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Hub'lar nasıl çalışır?

Sunucu tarafı kodu istemcide bir yöntem çağırdığında, çağrılacak yöntemin adını ve parametrelerini içeren etkin aktarım boyunca bir paket gönderilir (bir nesne yöntem parametresi olarak gönderildiğinde, JSON kullanılarak seri hale getirilir). İstemci daha sonra yöntem adını istemci tarafı kodunda tanımlanan yöntemlerle eşleşir. Bir eşleşme varsa, istemci yöntemi deserialized parametre verileri kullanılarak yürütülür.

Yöntem çağrısı [Fiddler](http://fiddler2.com/) gibi araçlar kullanılarak izlenebilir. Aşağıdaki resimde, SignalR sunucusundan Fiddler'ın Günlükler bölmesinde bir web tarayıcıistemcisine gönderilen bir yöntem çağrısı gösterilmektedir. Yöntem çağrısı adlı `MoveShapeHub`bir hub'dan gönderiliyor ve çağrılan `updateShape`yönteme denir.

![SignalR trafiğini gösteren Fiddler günlüğünün görünümü](introduction-to-signalr/_static/image6.png)

Bu örnekte, hub adı `H` parametre ile tanımlanır; yöntem adı `M` parametre ile tanımlanır ve yönteme gönderilen veriler `A` parametre ile tanımlanır. Bu iletiyi oluşturan uygulama [Yüksek Frekanslı Gerçek Zamanlı](tutorial-high-frequency-realtime-with-signalr.md) öğreticide oluşturulur.

### <a name="choosing-a-communication-model"></a>İletişim modeli seçme

Çoğu uygulama Hub'lar API kullanmalıdır. Bağlantılar API'si aşağıdaki durumlarda kullanılabilir:

- Gönderilen gerçek iletinin biçiminin belirtilmesi gerekir.
- Geliştirici, uzaktan çağırma modeli yerine bir ileti ve gönderme modeliyle çalışmayı tercih eder.
- SignalR kullanmak için bir ileti modeli kullanan varolan bir uygulama taşınır.
