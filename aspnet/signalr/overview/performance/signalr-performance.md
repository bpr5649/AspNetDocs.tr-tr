---
uid: signalr/overview/performance/signalr-performance
title: SignalR performansı | Microsoft Docs
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345272"
---
# <a name="signalr-performance"></a>SignalR Performansı

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, bir SignalR uygulamasındaki performansı nasıl tasarlayacağınızı, ölçecek ve artırabileceğinizi açıklamaktadır.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

SignalR performansı ve ölçeklendirmeyle ilgili son bir sunum için bkz. [ASP.NET SignalR Ile gerçek zamanlı web 'ı ölçeklendirme](https://channel9.msdn.com/Events/Build/2013/3-502).

Bu konu aşağıdaki bölümleri içermektedir:

- [Tasarım konusunda dikkat edilmesi gerekenler](#design)
- [SignalR sunucunuzu performans için ayarlama](#tuning)
- [Performans sorunlarını giderme](#troubleshooting)
- [SignalR performans sayaçlarını kullanma](#perfcounters)
- [Diğer performans sayaçlarını kullanma](#othercounters)
- [Diğer kaynaklar](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Tasarım konusunda dikkat edilmesi gerekenler

Bu bölüm, bir SignalR uygulamasının tasarımı sırasında uygulanabilecek desenleri açıklar. Bu, performansın gereksiz ağ trafiği oluşturarak dengelenmemiş olmasını sağlar.

### <a name="throttling-message-frequency"></a>Daraltma iletisi sıklığı

Büyük bir sıklıkta (gerçek zamanlı bir oyun uygulaması gibi) ileti gönderen bir uygulamada bile, çoğu uygulamanın bir saniyede birkaç ileti göndermesi gerekmez. Her bir istemcinin ürettiği trafik miktarını azaltmak için, kuyrukların (Bu zaman aralığında gönderilecek iletiler varsa, belirli bir sayıda iletiye kadar) daha sık gönderileceğini ve iletileri göndermesi için bir ileti döngüsü uygulanabilir. İletileri belirli bir hıza (hem istemciden hem de sunucudan) uygulayan örnek bir uygulama için bkz. [SignalR Ile yüksek frekanslı gerçek zamanlı](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>İleti boyutunu küçültme

Seri hale getirilmiş nesnelerinizin boyutunu azaltarak bir SignalR iletisinin boyutunu azaltabilirsiniz. Sunucu kodunda, aktarılmaları gerekmeyen özellikleri içeren bir nesne gönderiyorsanız, bu özelliklerin özniteliği kullanılarak serileştirilmesi önlenir `JsonIgnore` . Özelliklerin adları da iletide depolanır; özelliklerinin adları, özniteliği kullanılarak kısaltılarak yapılabilir `JsonProperty` . Aşağıdaki kod örneği, bir özelliğin istemciye gönderilme şeklini ve özellik adlarının nasıl kısaltılanmasını göstermektedir:

**Verilerin istemciye gönderilmesini hariç tutmak için Jsonıgnore özniteliğini ve ileti boyutunu azaltmak için JsonProperty özniteliğini gösteren .NET Server kodu**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

İstemci kodunda okunabilirlik/bakım korumasını sürdürmek için, kısaltılmış Özellik adları, ileti alındıktan sonra insanla kolay adlarla yeniden eşlenir. Aşağıdaki kod örneğinde, kısaltılmış adları daha uzun bir süre yeniden eşleştirmenin, bir ileti sözleşmesi tanımlayarak (eşleme) ve `reMap` sözleşmeyi iyileştirilmiş ileti sınıfına uygulamak için işlevini kullanarak olası bir yolu gösterilmektedir:

**Kısaltılmış özellik adlarını insan tarafından okunabilen adlara yeniden eşleyen istemci tarafı JavaScript kodu**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Adlar istemciden sunucuya, aynı yöntemi kullanarak da kısaltılarak çalıştırılabilir.

İleti nesnesinin bellek parmak izini (ileti için kullanılan bellek miktarı) azaltmada ayrıca performans de iyileştirebilirler. Örneğin, tam aralığı `int` gerekmiyorsa, `short` `byte` bunun yerine veya kullanılabilir.

İletiler, sunucu belleğindeki ileti veri yolunda depolandığından, ileti boyutunu azaltmak sunucu belleği sorunlarını da ele alabilir.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>SignalR sunucunuzu performans için ayarlama

Aşağıdaki yapılandırma ayarları, sunucunuzu bir SignalR uygulamasında daha iyi performans için ayarlamak üzere kullanılabilir. ASP.NET uygulamasında performansı geliştirme hakkında genel bilgi için bkz. [ASP.net performansını geliştirme](https://msdn.microsoft.com/library/ff647787.aspx).

**SignalR yapılandırma ayarları**

- **Defaultmessagebuffersize**: SignalR, bağlantı başına her hub 'da 1000 ileti tutar. Büyük iletiler kullanılıyorsa, bu değer azaltılarak alleviated olabilen bellek sorunları oluşturabilir. Bu ayar `Application_Start` , bir ASP.NET uygulamasındaki olay işleyicisinde veya `Configuration` Şirket içinde barındırılan bir uygulamadaki owın başlangıç sınıfının yönteminde ayarlanabilir. Aşağıdaki örnek, kullanılan sunucu belleği miktarını azaltmak için uygulamanızın bellek parmak izini azaltmak üzere bu değerin nasıl azaltılacağı gösterilmektedir:

    **Varsayılan ileti arabelleği boyutunu azaltmak için Startup.cs içindeki .NET Server kodu**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS yapılandırma ayarları**

- **Uygulama başına en fazla eşzamanlı istek**sayısı: eşzamanlı IIS isteklerinin sayısını artırmak, istek sunmak için kullanılabilir sunucu kaynaklarını arttırır. Varsayılan değer 5000 ' dir; Bu ayarı artırmak için, yükseltilmiş bir komut isteminde aşağıdaki komutları yürütün:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: uygulama havuzu için sıraya Http.sys en fazla istek sayısıdır. Sıra dolduğunda, yeni istekler 503 "hizmet kullanılamıyor" yanıtını alır. Varsayılan değer 1000'dir.

    Uygulamanızı barındıran uygulama havuzundaki çalışan işlemin sıra uzunluğu kısaltaştırın, bellek kaynaklarını tasarrufu sağlayacaktır. Daha fazla bilgi için bkz. [uygulama havuzlarını yönetme, ayarlama ve yapılandırma](https://technet.microsoft.com/library/cc745955.aspx).

**ASP.NET yapılandırma ayarları**

Bu bölüm, dosyasında ayarlankullanılabilecek yapılandırma ayarlarını içerir `aspnet.config` . Bu dosya, platforma bağlı olarak iki konumdan birinde bulunur:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

ASP.NET, SignalR performansını iyileştirebilecek ayarlar şunlardır:

- **CPU başına en fazla eşzamanlı istek sayısı**: Bu ayarın artırılması, performans sorunlarını hafifedebilir. Bu ayarı artırmak için aşağıdaki yapılandırma ayarını `aspnet.config` dosyasına ekleyin:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Istek sırası sınırı**: Toplam bağlantı sayısı `maxConcurrentRequestsPerCPU` ayarı aşarsa, ASP.net, bir kuyruğu kullanarak istekleri azaltmayı başlatır. Kuyruğun boyutunu artırmak için `requestQueueLimit` ayarı artırabilirsiniz. Bunu yapmak için aşağıdaki yapılandırma ayarını `processModel` içindeki düğümüne ekleyin `config/machine.config` (yerine `aspnet.config` ):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Performans sorunlarını giderme

Bu bölümde, uygulamanızda performans sorunlarını bulmanın yolları açıklanmaktadır.

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket 'in kullanılmakta olduğu doğrulanıyor

SignalR, istemci ve sunucu arasındaki iletişim için çeşitli aktarımlar kullanabilir, ancak WebSocket önemli bir performans avantajı sunar ve istemci ve sunucu bunu destekliyorsa kullanılmalıdır. İstemci ve sunucunuzun WebSocket gereksinimlerini karşılayıp karşılamadığını öğrenmek için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports). Uygulamanızda hangi taşımanın kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanabilir ve bağlantı için hangi taşımanın kullanıldığını görmek üzere günlükleri inceleyebilirsiniz. Internet Explorer ve Chrome 'daki tarayıcı geliştirme araçlarını kullanma hakkında daha fazla bilgi için bkz. [aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR performans sayaçlarını kullanma

Bu bölümde, pakette bulunan SignalR performans sayaçlarının nasıl etkinleştirileceği ve kullanılacağı açıklanmaktadır `Microsoft.AspNet.SignalR.Utils` .

### <a name="installing-signalrexe"></a>signalr.exe yükleniyor

Performans sayaçları, SignalR.exe adlı bir yardımcı program kullanılarak sunucuya eklenebilir. Bu yardımcı programı yüklemek için şu adımları izleyin:

1. Visual Studio 'da **Araçlar**  >  **NuGet Paket Yöneticisi**  >  **çözüm için NuGet Paketlerini Yönet** ' i seçin.
2. **SignalR. utils**araması yapın ve yüklemeyi seçin.

    ![](signalr-performance/_static/image1.png)
3. Paketi yüklemek için lisans sözleşmesini kabul edin.
4. SignalR.exe, ' ye yüklenir `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools` .

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe ile performans sayaçlarını yükleme

SignalR performans sayaçlarını yüklemek için aşağıdaki parametreyle SignalR.exe yükseltilmiş bir komut isteminde çalıştırın:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR performans sayaçlarını kaldırmak için, aşağıdaki parametreyle SignalR.exe yükseltilmiş bir komut isteminde çalıştırın:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR performans sayaçları

Yardımcı programlar paketi aşağıdaki performans sayaçlarını yükleme. "Toplam" sayacı, son uygulama havuzunun veya sunucu yeniden başlatılmasından bu yana olayların sayısını ölçer.

**Bağlantı ölçümleri**

Aşağıdaki ölçümler, gerçekleşen bağlantı ömrü olaylarını ölçer. Daha fazla bilgi için bkz. [bağlantı ömrü olaylarını anlama ve işleme](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Bağlı bağlantılar**
- **Bağlantılar yeniden bağlandı**
- **Bağlantı kesilen bağlantılar**
- **Geçerli bağlantı sayısı**

**İleti ölçümleri**

Aşağıdaki ölçümler, SignalR tarafından oluşturulan ileti trafiğini ölçer.

- **Alınan bağlantı Iletileri toplamı**
- **Gönderilen bağlantı Iletileri toplamı**
- **Alınan bağlantı Iletisi/sn**
- **Gönderilen bağlantı Iletisi/sn**

**İleti veri yolu ölçümleri**

Aşağıdaki ölçümler, gelen ve giden SignalR iletilerinin yerleştirildiği sıra, iç SignalR ileti veri yolu üzerinden trafiği ölçer. İleti gönderildiğinde veya **yayımlandığında yayınlanır** . Bu bağlamdaki bir **abone** , ileti veri yolundaki bir aboneliğiniz; Bu, istemci sayısına ve sunucunun kendine eşit olmalıdır. **Ayrılmış çalışan** , etkin bağlantılara veri gönderen bir bileşendir; Meşgul bir çalışan, etkin bir şekilde ileti gönderen bir **çalışandır** .

- **Alınan ileti veri yolu Iletileri toplamı**
- **Alınan ileti veri yolu iletisi/sn**
- **İleti veri yolu Iletileri yayımlandı toplamı**
- **Yayınlanan ileti veri yolu iletisi/sn**
- **İleti veri yolu aboneleri geçerli**
- **İleti veri yolu aboneleri toplamı**
- **İleti veri yolu aboneleri/sn**
- **İleti veri yolu ayrılmış çalışanları**
- **İleti veri yolu meşgul çalışanları**
- **İleti veri yolu konuları geçerli**

**Hata ölçümleri**

Aşağıdaki ölçümler, SignalR ileti trafiği tarafından oluşturulan hataları ölçer. Hub veya hub yöntemi çözümlenemiyorsa **Merkez çözümleme** hataları oluşur. Hub **çağrısı** hataları, bir hub yöntemi çağrılırken oluşturulan özel durumlardır. **Aktarım** hataları, bir http isteği veya yanıtı sırasında oluşturulan bağlantı hatalardır.

- **Hatalar: tüm toplam**
- **Hatalar: tümü/sn**
- **Hatalar: Merkez çözümleme toplamı**
- **Hatalar: hub çözümleme/sn**
- **Hatalar: hub çağrısı toplamı**
- **Hatalar: hub çağrı/sn**
- **Hatalar: aktarım toplamı**
- **Hatalar: aktarım/sn**

<a id="scaleout_metrics"></a>

**Genişleme ölçümleri**

Aşağıdaki ölçümler, genişleme sağlayıcısı tarafından oluşturulan trafiği ve hataları ölçer. Bu bağlamdaki bir **akış** , genişleme sağlayıcısı tarafından kullanılan bir ölçek birimidir; SQL Server kullanılırsa bu bir tablodur, Service Bus kullanılıyorsa bir konu ve redin kullanılıyorsa bir abonelik. Her akış, sıralı okuma ve yazma işlemlerini sağlar; tek bir akış olası bir ölçeklendirme tıkanıkıdır, bu nedenle bu performans sorununu azaltmaya yardımcı olmak için akış sayısı artırılabilir. Birden çok akış kullanılıyorsa, SignalR, belirli bir bağlantıdan gönderilen iletilerin sırada olmasını sağlamak üzere bu akışlarda iletileri otomatik olarak dağıtır (parça).

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) ayarı, SignalR tarafından tutulan genişleme gönderme sırasının uzunluğunu denetler. Bu değeri 0 ' dan büyük bir değere ayarlamak, bir gönderme sırasındaki tüm iletilerin aynı anda yapılandırılmış mesajlaşma biriktirme düzlemine gönderilmesini sağlar. Kuyruğun boyutu yapılandırılan uzunluğun üzerine gittiğinde, sıradaki ileti sayısı tekrar ayarından daha az olana kadar sonraki Gönder çağrıları bir [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ile hemen başarısız olur. Uygulanan arka düzlemler genellikle kendi sıraya alma veya akış denetimine sahip olduğundan sıraya alma varsayılan olarak devre dışıdır. SQL Server durumda, bağlantı havuzu her seferinde gönderilen gönderme sayısını etkin bir şekilde kısıtlar.

Varsayılan olarak, SQL Server ve redin için yalnızca bir akış kullanılır, Service Bus için beş akış kullanılır ve sıraya alma devre dışıdır, ancak bu ayarlar SQL Server ve Service Bus yapılandırması aracılığıyla değiştirilebilir:

**SQL Server backdüzlemi için tablo sayısını ve sıra uzunluğunu yapılandırmaya yönelik .NET sunucu kodu**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Service Bus backdüzlemi için konu sayısını ve sıra uzunluğunu yapılandırmaya yönelik .NET sunucu kodu**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**Arabelleğe alma** akışı, hatalı bir duruma girmiş bir durumdur; akış hatalı durumdaysa, akış artık hatalı olana kadar geri düzleme gönderilen tüm iletiler hemen başarısız olur. **Gönderme sırası uzunluğu** , gönderilen ancak henüz gönderilmemiş olan iletilerin sayısıdır.

- **Alınan genişleme Ileti veri yolu Iletisi/sn**
- **Ölçek Genişletme akışı toplamı**
- **Ölçek Genişletme akışları açık**
- **Genişleme akışları arabelleğe alma**
- **Ölçek Genişletme hataları toplamı**
- **Genişleme hatası/sn**
- **Genişleme gönderme sırası uzunluğu**

Bu sayaçların ölçüm hakkında daha fazla bilgi için bkz. [Azure Service Bus Ile SignalR ölçeği](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Diğer performans sayaçlarını kullanma

Aşağıdaki performans sayaçları, uygulamanızın performansını izlemek için de yararlı olabilir.

**Bellek**

- .NET CLR bellek sayısı \\ Tüm yığınlardaki bayt (W3wp için)

**ASP.NET**

- ASP. NET\Requests geçerli
- ASP. NET\Queued
- ASP. NET\Rejected

**CPU**

- İşlemci Bilgileri\işlemci zamanı

**TCP/IP**

- TCPv6/bağlantı kurdu
- TCPv4/bağlantı kurdu

**Web hizmeti**

- Web hizmeti \ geçerli bağlantılar
- Web hizmeti \ en fazla bağlantı sayısı

**İş Parçacığı Oluşturma**

- .NET CLR kilitleri ve Iş parçacıkları \\ geçerli mantıksal Iş parçacıklarının sayısı
- .NET CLR kilitleri ve Iş parçacıkları \\ geçerli fiziksel Iş parçacığı sayısı

<a id="otherresources"></a>

## <a name="other-resources"></a>Diğer Kaynaklar

ASP.NET performans izleme ve ayarlama hakkında daha fazla bilgi için aşağıdaki konulara bakın:

- [ASP.NET performansına genel bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [ASP.NET Iş parçacığı kullanımı IIS 7,5, IIS 7,0 ve IIS 6,0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool &gt; öğesi (Web ayarları)](https://msdn.microsoft.com/library/dd560842.aspx)
