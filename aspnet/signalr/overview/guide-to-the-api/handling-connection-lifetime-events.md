---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: SignalR'de Bağlantı ÖmrünüN Boyu Olayları Anlama ve İşleme | Microsoft Dokümanlar
author: bradygaster
description: Bu makalede, Hub'lar API tarafından maruz kalan olayların nasıl kullanılacağı açıklanmaktadır.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676218"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>SignalR’da Bağlantı Ömrü Olaylarını Anlama ve İşleme

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, işleyebilir SinyalR bağlantısı, yeniden bağlantı ve kopukluk olayları ve zaman aşımı ve yapılandırabilirsiniz ayarları canlı tutmak genel bir bakış sağlar.
>
> Makale zaten SignalR ve bağlantı yaşam olayları bazı bilgilere sahip varsayar. SignalR'a giriş için [SignalR'a Giriş 'e](../getting-started/introduction-to-signalr.md)bakın. Bağlantı yaşam boyu olayları nın listeleri için aşağıdaki kaynaklara bakın:
>
> - [Hub sınıfındaki bağlantı ömrü olayları nasıl işleyebilir?](hubs-api-guide-server.md#connectionlifetime)
> - [JavaScript istemcilerinde bağlantı ömrü ndeki olayları nasıl işlersiniz?](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [.NET istemcilerinde bağlantı ömrü olayları nasıl işleyebilir?](hubs-api-guide-net-client.md#connectionlifetime)
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

Bu makalede aşağıdaki bölümler yer alıyor:

- [Bağlantı ömür boyu terminoloji ve senaryolar](#terminology)

    - [SinyalR bağlantıları, aktarım bağlantıları ve fiziksel bağlantılar](#signalrvstransport)
    - [Aktarım kopukluğu senaryoları](#transportdisconnect)
    - [İstemci kopukluk senaryoları](#clientdisconnect)
    - [Sunucu kopukluğu senaryoları](#serverdisconnect)
- [Zaman sonu ve canlı tutma ayarları](#timeoutkeepalive)

    - [Connectiontimeout](#connectiontimeout)
    - [Bağlantıyı KesmeTimeout](#disconnecttimeout)
    - [Keepalive](#keepalive)
    - [Zaman ayarı ve canlı ayarları tutma](#changetimeout)
- [Bağlantı kesilmeleri hakkında kullanıcıya nasıl bilgi verene](#notifydisconnect)
- [Sürekli olarak yeniden bağlanma](#continuousreconnect)
- [Sunucu kodundaki istemci nin bağlantısını kesme](#disconnectclientfromserver)
- [Kopma nedenini algılama](#detectingreasonfordisconnection)

API Başvuru konularına bağlantılar, API'nin .NET 4.5 sürümüne bağlantılardır. .NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Bağlantı ömür boyu terminoloji ve senaryolar

SignalR Hub'daki `OnReconnected` olay işleyicisi, belirli bir istemci için doğrudan sonra `OnConnected` yürütebilir, ancak sonra `OnDisconnected` yürütülemez. Bağlantı kopmadan yeniden bağlantı kuramanın nedeni, SignalR'da "bağlantı" sözcüğünün kullanıldığı çeşitli yollar olmasıdır.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SinyalR bağlantıları, aktarım bağlantıları ve fiziksel bağlantılar

Bu makalede *SinyalR bağlantıları,* *aktarım bağlantıları*ve *fiziksel bağlantılar*arasında ayrım yapılacaktır:

- **SignalR bağlantısı,** SignalR API tarafından korunan ve bir bağlantı kimliğiyle benzersiz olarak tanımlanan bir istemci ve sunucu URL'si arasındaki mantıksal ilişkiyi ifade eder. Bu ilişkiyle ilgili veriler SignalR tarafından korunur ve bir aktarım bağlantısı kurmak için kullanılır. İlişki sona erer ve SignalR, istemci `Stop` yöntemi aradığında veya SignalR kayıp bir aktarım bağlantısını yeniden kurmaya çalışırken bir zaman sonu sınırına ulaşıldığında verileri imha eder.
- **Aktarım bağlantısı,** dört aktarım API'lerinden biri tarafından korunan istemci ve sunucu arasındaki mantıksal ilişkiyi ifade eder: WebSockets, sunucu tarafından gönderilen olaylar, sonsuza kadar çerçeve veya uzun yoklama. SignalR, aktarım bağlantısı oluşturmak için aktarım API'sini kullanır ve aktarım API'si aktarım bağlantısını oluşturmak için fiziksel bir ağ bağlantısının varlığına bağlıdır. Aktarım bağlantısı SignalR sonlandırdığinde veya aktarım API'sı fiziksel bağlantının koptuğunda sona erer.
- **Fiziksel bağlantı,** istemci bilgisayar ile sunucu bilgisayarı arasındaki iletişimi kolaylaştıran fiziksel ağ bağlantılarını (kablolar, kablosuz sinyaller, yönlendiriciler, vb.) ifade eder. Bir aktarım bağlantısı kurmak için fiziksel bağlantı nın bulunması ve SinyalR bağlantısı kurmak için bir aktarım bağlantısı nın kurulması gerekir. Ancak, fiziksel bağlantıyı kırmak, bu konuda daha sonra açıklanacağı gibi, aktarım bağlantısını veya SignalR bağlantısını her zaman hemen sona erdirmez.

Aşağıdaki diyagramda, SignalR bağlantısı Hubs API ve PersistentConnection API SignalR katmanı tarafından temsil edilir, aktarım bağlantısı Aktarımlar katmanı tarafından temsil edilir ve fiziksel bağlantı sunucu ve istemciler arasındaki çizgilerle temsil edilir.

![SignalR mimari diyagramı](handling-connection-lifetime-events/_static/image1.png)

Bir SignalR `Start` istemcisinde yöntemi aradiğinizde, bir sunucuya fiziksel bir bağlantı kurmak için gereken tüm bilgileri sinyalr istemci kodu sağlarsınız. SignalR istemci kodu, bir HTTP isteği nde bulunmak ve dört aktarım yönteminden birini kullanan fiziksel bir bağlantı kurmak için bu bilgileri kullanır. Aktarım bağlantısı başarısız olursa veya sunucu başarısız olursa, istemci aynı SignalR URL'sine otomatik olarak yeni bir aktarım bağlantısı kurmak için gereken bilgilere sahip olduğundan SignalR bağlantısı hemen silinmez. Bu senaryoda, kullanıcı uygulamasından hiçbir müdahale söz konusu değildir ve SignalR istemci kodu yeni bir aktarım bağlantısı kurduğunda, yeni bir SinyalR bağlantısı başlatmaz. SignalR bağlantısının sürekliliği, yöntemi aradığınızda oluşturulan bağlantı kimliğinin `Start` değişmediği gerçeğine yansıtılır.

Hub'daki `OnReconnected` olay işleyicisi, bir aktarım bağlantısı kaybolduktan sonra otomatik olarak yeniden kurulduğunda çalıştırılır. Olay `OnDisconnected` işleyicisi bir SignalR bağlantısının sonunda yürütür. SignalR bağlantısı aşağıdaki yollardan herhangi birinde sona erebilir:

- İstemci `Stop` yöntemi çağırırsa, sunucuya bir durdurma iletisi gönderilir ve hem istemci hem de sunucu SignalR bağlantısını hemen sonlandırır.
- İstemci ve sunucu arasındaki bağlantı kaybolduktan sonra, istemci yeniden bağlanmaya çalışır ve sunucu istemcinin yeniden bağlanmasını bekler. Yeniden bağlanma girişimleri başarısız olursa ve bağlantı kesme zaman sonu süresi sona ererse, hem istemci hem de sunucu SignalR bağlantısını sona erdirin. İstemci yeniden bağlanmaya çalışmayı durdurur ve sunucu SignalR bağlantısının temsilini ortadan kaldırabilir.
- İstemci `Stop` yöntemi arama şansı olmadan çalışmayı durdurursa, sunucu istemcinin yeniden bağlanmasını bekler ve devre son verme süresinin kesilmesinden sonra SinyalR bağlantısını sona erdirer.
- Sunucu çalışmayı durdurursa, istemci yeniden bağlanmaya çalışır (aktarım bağlantısını yeniden oluşturur) ve ardından bağlantı kesme devresi bittikten sonra SinyalR bağlantısını sona erdirer.

Bağlantı sorunu olmadığında ve kullanıcı uygulaması `Stop` yöntemi çağırarak SignalR bağlantısını sona erdirdiğinde, SignalR bağlantısı ve aktarım bağlantısı yaklaşık aynı anda başlar ve biter. Aşağıdaki bölümlerde diğer senaryolar daha ayrıntılı olarak açıklayınız.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Aktarım kopukluğu senaryoları

Fiziksel bağlantılar yavaş olabilir veya bağlantıda kesintiler olabilir. Kesintinin uzunluğu gibi etkenlere bağlı olarak, aktarım bağlantısı kesilebilir. SignalR daha sonra taşıma bağlantısını yeniden kurmaya çalışır. Bazen aktarım bağlantısı API kesintisi algılar ve aktarım bağlantısını düşürür ve SignalR bağlantının kaybolduğunu hemen öğrenir. Diğer senaryolarda, ne aktarım bağlantısı API'si ne de SignalR bağlantının kaybolduğunu hemen fark etmez. Uzun yoklama dışındaki tüm taşımalar için SignalR istemcisi, aktarım API'sinin algılayamadığı bağlantı kaybını kontrol etmek için *canlı tutma* adı verilen bir işlev kullanır. Uzun yoklama bağlantıları hakkında daha fazla bilgi için, bu konunun ilerleyen saatlerinde [Zaman Ekine ve canlı ayarları na](#timeoutkeepalive) bakın.

Bir bağlantı etkin olmadığında, sunucu düzenli aralıklarla istemciye canlı bir paket gönderir. Bu makalenin yazıldığı tarih itibariyle varsayılan sıklık her 10 saniyede bir olur. Bu paketleri dinleyerek, istemciler bir bağlantı sorunu olup olmadığını anlayabilir. Beklenen zamanda bir keepalive paketi alınmazsa, kısa bir süre sonra istemci yavaşlık veya kesinti gibi bağlantı sorunları olduğunu varsayar. Canlı tutma daha uzun bir süre sonra hala alınmazsa, istemci bağlantının bırakıldığını varsayar ve yeniden bağlanmaya çalışır.

Aşağıdaki diyagram, aktarım API'si tarafından hemen tanınmayan fiziksel bağlantıyla ilgili sorunlar olduğunda, tipik bir senaryoda ortaya çıkan istemci ve sunucu olaylarını göstermektedir. Diyagram aşağıdaki durumlar için geçerlidir:

- Aktarım WebSockets, sonsuza kadar çerçeve veya sunucu tarafından gönderilen olaylardır.
- Fiziksel ağ bağlantısında çeşitli kesinti dönemleri vardır.
- Aktarım API'si kesintilerin farkına varmaz, bu nedenle SignalR bunları algılamak için canlı tutma işlevine güvenir.

![Taşıma kopuklukları](handling-connection-lifetime-events/_static/image2.png)

İstemci yeniden bağlanma moduna geçerse ancak bağlantı kesme zaman sınırı içinde bir aktarım bağlantısı kuramazsa, sunucu SignalR bağlantısını sonlandırır. Bu durumda, sunucu Hub'ın `OnDisconnected` yöntemini yürütür ve istemcinin daha sonra bağlanmayı başarması durumunda istemciye göndermek üzere bir bağlantı kesme iletisi sıraya alır. İstemci daha sonra yeniden bağlanırsa, bağlantı `Stop` kesme komutunu alır ve yöntemi çağırır. Bu senaryoda, `OnReconnected` istemci yeniden bağlandığında yürütülmez ve `OnDisconnected` istemci aradığında `Stop`yürütülmez. Aşağıdaki diyagram bu senaryoyu göstermektedir.

![Aktarım kesintileri - sunucu zaman ayarı](handling-connection-lifetime-events/_static/image3.png)

İstemci üzerinde gündeme getirilebilecek SignalR bağlantı yaşam boyu olaylar şunlardır:

- `ConnectionSlow`istemci olay.

    Son iletiden bu yana canlı tutma süresinin önceden ayarlanmış bir oranı geçtiğinde veya ping'i canlı tuttuğunda yükseltilir. Varsayılan tutma zaman dışarısı uyarı süresi, keepalive zaman anının 2/3'üdür. Keepalive zaman dilimi 20 saniyedir, bu nedenle uyarı yaklaşık 13 saniye de gerçekleşir.

    Varsayılan olarak, sunucu her 10 saniyede bir canlı ping gönderir ve istemci her 2 saniyede bir ping'i canlı tutmayı denetler (hayatta kalma zaman ayırma değeri ile keepalive zaman ayırma uyarı değeri arasındaki farkın üçte biri).

    Aktarım API'si bir kopukluk tanhaberdar olursa, signalr sürekli zaman zaman dilimi uyarı süresi geçmeden önce kopukluk hakkında bilgilendirilebilir. Bu durumda, `ConnectionSlow` olay yükseltilmiş olmaz ve SignalR `Reconnecting` doğrudan olay gider.
- `Reconnecting`istemci olay.

    (a) aktarım API'sı bağlantının kaybolduğunu algıladığında veya (b) son iletiden veya keepalive ping'den bu yana geçen zaman diliminde yükseltilir. SignalR istemci kodu yeniden bağlanmaya çalışır. Bir aktarım bağlantısı kaybolduğunda uygulamanızın bazı eylemlerde bulunmasını istiyorsanız, bu olayı işleyebilirsiniz. Varsayılan tutma zaman dışarı sı şu anda 20 saniyedir.

    İstemciniz kodunuz SignalR yeniden bağlanma modundayken Hub yöntemini çağırmaya çalışırsa, SignalR komutu göndermeye çalışır. Çoğu zaman, bu tür girişimler başarısız olur, ancak bazı durumlarda başarılı olabilir. Sunucu tarafından gönderilen olaylar, sonsuza kadar çerçeve ve uzun yoklama aktarımları için SignalR, istemcinin ileti göndermek için kullandığı ve ileti almak için kullandığı iki iletişim kanalı kullanır. Almak için kullanılan kanal kalıcı olarak açık olandır ve fiziksel bağlantı kesildiğinde kapalı olan kanaldır. Göndermek için kullanılan kanal kullanılabilir durumda kalır, bu nedenle fiziksel bağlantı geri yüklenirse, istemciden sunucuya bir yöntem çağrısı, alma kanalı yeniden kurulmadan önce başarılı olabilir. SignalR almak için kullanılan kanalı yeniden açana kadar iade değeri alınmaz.
- `Reconnected`istemci olay.

    Aktarım bağlantısı yeniden kurulduğunda yükseltilir. Hub'daki `OnReconnected` olay işleyicisi yürütülür.
- `Closed`istemci olayı`disconnected` (JavaScript'teki olay).

    SignalR istemci kodu aktarım bağlantısını kaybettikten sonra yeniden bağlanmaya çalışırken bağlantı kesme süresi sona erdiğinde yükseltilir. Varsayılan kesme süresi 30 saniyedir. (Bu olay, `Stop` yöntem çağrıldığında bağlantı sona erdiğinde de yükselir.)

Aktarım API'si tarafından algılanmayan ve sunucudan canlı tutma pinglerinin alımını, canlı tutma zaman aşımı uyarı süresinden daha uzun süre geciktirmeyen aktarım bağlantısı kesintileri, bağlantı ömrü boyunca herhangi bir olayın yükseltilmesine neden olmayabilir.

Bazı ağ ortamları boşta kalan bağlantıları kasıtlı olarak kapatır ve keepalive paketlerinin bir diğer işlevi de bu ağlara SignalR bağlantısının kullanıldığını bildirerek bunu önlemeye yardımcı olmaktır. Ekstrem durumlarda ping'leri canlı tutmanın varsayılan sıklığı kapalı bağlantıları önlemek için yeterli olmayabilir. Bu durumda, keepalive ping'leri daha sık gönderilecek şekilde yapılandırabilirsiniz. Daha fazla bilgi için, bu konuda daha sonra [Timeout ve keepalive ayarları](#timeoutkeepalive) bakın.

> [!NOTE]
>
> **Önemli**: Burada açıklanan olayların sırası garanti edilmez. SignalR, bağlantı ömrü ndeki olayları bu şemaya göre öngörülebilir bir şekilde yükseltmek için her türlü girişimi yapar, ancak ağ olaylarının birçok varyasyonu ve taşıma API'leri gibi temel iletişim çerçevelerinin bunları ele aldığı birçok yöntem vardır. Örneğin, istemci `Reconnected` yeniden bağlandığında olay yükseltilmeyebilir veya `OnConnected` bağlantı kurma girişimi başarısız olduğunda sunucudaki işleyici çalışabilir. Bu konu, yalnızca normalde belirli tipik koşullar tarafından üretilecek etkileri açıklar.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>İstemci kopukluk senaryoları

Tarayıcı istemcisinde, SignalR bağlantısını koruyan SignalR istemci kodu, bir web sayfasının JavaScript bağlamında çalışır. Bu nedenle, bir sayfadan diğerine gezinirken SignalR bağlantısının sona ermesi gerekir ve bu nedenle birden çok tarayıcı penceresinden veya sekmeden bağlanırsanız birden çok bağlantı bağlantısına sahip birden fazla bağlantınız vardır. Kullanıcı bir tarayıcı penceresini veya sekmesini kapattığında veya yeni bir sayfaya gittiğinde veya sayfayı yenilediğinde, SignalR istemci kodu `Stop` bu tarayıcı olayını sizin için işlediği ve yöntemi aradığı için SignalR bağlantısı hemen sona erer. Bu senaryolarda veya `Stop` uygulamanız yöntemi aradığında herhangi bir `OnDisconnected` istemci platformunda, olay işleyicisi `Closed` sunucuda hemen yürütür ve istemci olayı yükseltir (olay JavaScript'te adlandırılır). `disconnected`

Bir istemci uygulaması veya çalışan bilgisayar kilitlenirse veya uyku moduna geçerse (örneğin, kullanıcı dizüstü bilgisayarı kapattığında), sunucuya ne olduğu hakkında bilgi vermez. Sunucunun bildiği kadarıyla, istemcinin kaybı bağlantı kesintisinden kaynaklanıyor olabilir ve istemci yeniden bağlanmaya çalışıyor olabilir. Bu nedenle, bu senaryolarda sunucu istemciye yeniden bağlanma şansı `OnDisconnected` vermek için bekler ve bağlantı kesme süresi dolana kadar (varsayılan olarak yaklaşık 30 saniye) yürütmez. Aşağıdaki diyagram bu senaryoyu göstermektedir.

![İstemci bilgisayar hatası](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Sunucu kopukluğu senaryoları

Bir sunucu çevrimdışı olduğunda -yeniden başlatıldığında, başarısız oluyor, uygulama etki alanı geri dönüşümleri, vb.) sonuç kayıp bir bağlantıya benzer olabilir veya aktarım API'si ve `ConnectionSlow` SignalR sunucunun gittiğini hemen anlayabilir ve SignalR olayı yükseltmeden yeniden bağlanmaya çalışabilir. İstemci yeniden bağlanma moduna geçerse ve sunucu iyileşirse veya yeniden başlatılırsa veya bağlantı kesme süresi dolmadan önce yeni bir sunucu çevrimiçi duruma getirilirse, istemci geri yüklenen veya yeni sunucuya yeniden bağlanır. Bu durumda, Sinyalr bağlantısı istemci üzerinde `Reconnected` devam ediyor ve olay yükseltilir. İlk sunucuda, `OnDisconnected` yürütülmez ve yeni sunucuda, `OnReconnected` `OnConnected` daha önce bu istemci için yürütülmemiş olmasına rağmen yürütülür. (Sunucu önceki bağlantı etkinliği hiçbir bellek olduğu için, istemci yeniden başlatma veya uygulama etki alanı geri dönüşümsonra aynı sunucuya yeniden bağlanır, çünkü etkisi aynıdır.) Aşağıdaki diyagram, aktarım API'sinin kayıp bağlantının hemen `ConnectionSlow` farkına vardığını, bu nedenle olayın yükseltilmediğini varsayar.

![Sunucu hatası ve yeniden bağlantı](handling-connection-lifetime-events/_static/image5.png)

Bir sunucu bağlantı kesme süresi içinde kullanılamıyorsa, SignalR bağlantısı sona erer. Bu senaryoda, `Closed` olay`disconnected` (JavaScript istemcilerinde) istemcide `OnDisconnected` yükseltilir, ancak sunucuda asla çağrılmaz. Aşağıdaki diyagram, aktarım API'sinin kayıp bağlantıdan haberdar olmadığını varsayar, bu nedenle SignalR tarafından algılanır ve `ConnectionSlow` olay yükseltilir.

![Sunucu hatası ve zaman arızası](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Zaman sonu ve canlı tutma ayarları

Varsayılan `ConnectionTimeout`, `DisconnectTimeout`ve `KeepAlive` değerler çoğu senaryo için uygundur, ancak ortamınızın özel gereksinimleri varsa değiştirilebilir. Örneğin, ağ ortamınız boşta kalan bağlantıları 5 saniye liğine kapatıyorsa, canlı kalma değerini azaltmanız gerekebilir.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>Connectiontimeout

Bu ayar, aktarım bağlantısını açık bırakma ve kapatmadan ve yeni bir bağlantı açmadan önce yanıt bekleme süresini gösterir. Varsayılan değer 110 saniyedir.

Bu ayar yalnızca keepalive işlevselliği devre dışı bırakıldığında geçerlidir ve normalde yalnızca uzun yoklama aktarımları için geçerlidir. Aşağıdaki diyagram, bu ayarın uzun bir yoklama aktarım bağlantısı üzerindeki etkisini göstermektedir.

![Uzun yoklama taşıma bağlantısı](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>Bağlantıyı KesmeTimeout

Bu ayar, `Disconnected` olayı yükseltmeden önce aktarım bağlantısı kaybolduktan sonra bekleme süresini gösterir. Varsayılan değer 30 saniyedir. Ayarladığınızda, `DisconnectTimeout` `KeepAlive` otomatik olarak değerin 1/3'ü `DisconnectTimeout` olarak ayarlanır.

<a id="keepalive"></a>

### <a name="keepalive"></a>Keepalive

Bu ayar, boşta kalan bir paketten boşta kalma dan önce bekleme süresini gösterir. Varsayılan değer 10 saniyedir. Bu değer, değerin `DisconnectTimeout` 1/3'ünden fazla olmamalıdır.

Her ikisini `DisconnectTimeout` de ayarlamak `KeepAlive`istiyorsanız `KeepAlive` `DisconnectTimeout`ve sonra ayarlayın. Aksi `KeepAlive` takdirde, zaman ödeme `DisconnectTimeout` değerinin `KeepAlive` 1/3'ü otomatik olarak ayarlandığında ayarınız üzerine yazılır.

Keepalive işlevini devre dışı atmak istiyorsanız, null `KeepAlive` ayarlayın. Keepalive işlevi, uzun yoklama taşıması için otomatik olarak devre dışı bırakılır.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Zaman ayarı ve canlı ayarları tutma

Bu ayarların varsayılan değerlerini değiştirmek için, aşağıdaki örnekte gösterildiği gibi `Application_Start` *Global.asax* dosyanızda ayarlayın. Örnek kodda gösterilen değerler varsayılan değerlerle aynıdır.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Bağlantı kesilmeleri hakkında kullanıcıya nasıl bilgi verene

Bazı uygulamalarda bağlantı sorunları olduğunda kullanıcıya bir ileti görüntülemek isteyebilirsiniz. Bunu nasıl ve ne zaman yapacağınız için çeşitli seçenekleriniz var. Aşağıdaki kod örnekleri, oluşturulan proxy'yi kullanan bir JavaScript istemcisi içindir.

- SignalR `connectionSlow` bağlantı sorunlarının farkına varır varmaz, yeniden bağlanma moduna geçmeden önce bir iletiyi görüntülemek için olayı işleyin.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- SignalR `reconnecting` bir bağlantının kopukluğu ndan haberdar olduğunda ve yeniden bağlanma moduna geçtiğinde, olayı bir iletiyi görüntülemek için işleyin.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Yeniden `disconnected` bağlanma denemesi zaman dolduğunda bir ileti görüntülemek için olayı işleyebilir. Bu senaryoda, sunucuyla yeniden bağlantı kurmanın tek yolu, yeni bir bağlantı kimliği `Start` oluşturacak yöntemi arayarak SignalR bağlantısını yeniden başlatmaktır. Aşağıdaki kod örneği, `Stop` bildirimi yalnızca yeniden bağlanma zaman anından sonra düzenlediğinden emin olmak için bir bayrak kullanır, yöntemi çağırmanın neden olduğu SignalR bağlantısının normal bir sonundan sonra değil.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Sürekli olarak yeniden bağlanma

Bazı uygulamalarda, bağlantı kaybolduktan ve yeniden bağlanma denemesi zaman dolduktan sonra otomatik olarak yeniden bağlantı kurmak isteyebilirsiniz. Bunu yapmak `Start` için, yöntemi olay `Closed` işleyicinizden`disconnected` (JavaScript istemcilerinde olay işleyicisi) arayabilirsiniz. Sunucu veya fiziksel bağlantı kullanılamadığında `Start` bunu çok sık yapmamak için aramadan önce bir süre beklemek isteyebilirsiniz. Aşağıdaki kod örneği, oluşturulan proxy'yi kullanan bir JavaScript istemcisi içindir.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Mobil istemcilerde dikkat edilmesi gereken olası bir sorun, sunucu veya fiziksel bağlantı kullanılamadığında sürekli yeniden bağlantı denemelerinin gereksiz pil indene neden olabilmesidir.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Sunucu kodundaki istemci nin bağlantısını kesme

SignalR sürüm 2 istemcileri kesmek için yerleşik bir sunucu API'si yok. Gelecekte [bu işlevselliği eklemek için planlar](https://github.com/SignalR/SignalR/issues/2101)vardır. Geçerli SignalR sürümünde, istemcinin sunucudan bağlantısını kesmenin en basit yolu istemciye bir bağlantı kesme yöntemi uygulamak ve bu yöntemi sunucudan aramaktır. Aşağıdaki kod örneği, oluşturulan proxy'yi kullanarak bir JavaScript istemcisi için bir bağlantı kesme yöntemini gösterir.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Güvenlik - İstemciler yeniden bağlanabildiği veya ele geçirilen kod `stopClient` yöntemi kaldırabileceğinden veya ne yaptığını değiştirebildiği için, istemcilerin bağlantısını kesmek için ne de önerilen yerleşik API, kötü amaçlı kod çalıştıran istemcilerin senaryosunu ele almaz. Devlet hizmeti reddi (DOS) koruması uygulamak için uygun yer çerçeve veya sunucu katmanı değil, ön uç altyapısıdır.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>Kopma nedenini algılama

SignalR 2.1, sunucu `OnDisconnect` olayına, istemcinin zamanlama yerine kasıtlı olarak bağlantının kesilip kesilmediğini gösteren aşırı yük ekler. İstemci `StopCalled` bağlantıyı açıkça kapattıysa parametre doğrudur. JavaScript'te, bir sunucu hatası istemcinin bağlantısını kesmeye neden olduysa, hata bilgileri istemciye `$.connection.hub.lastError`.

**C# sunucu `stopCalled` kodu: parametre**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript istemci kodu: `lastError` `disconnect` olay erişim.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
