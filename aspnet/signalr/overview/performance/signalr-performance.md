---
uid: signalr/overview/performance/signalr-performance
title: SignalR Performans | Microsoft Dokümanlar
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676092"
---
# <a name="signalr-performance"></a>SignalR Performansı

tarafından [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, SignalR uygulamasında performansı nasıl tasarlayabilmek, ölçmek ve geliştirmek için açıklanır.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Görsel Stüdyo 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

SignalR performansı ve ölçekleme ile ilgili yeni bir sunum için, [ASP.NET SignalR ile Gerçek Zamanlı Web ölçekleme](https://channel9.msdn.com/Events/Build/2013/3-502)bakın.

Bu konu aşağıdaki bölümleri içermektedir:

- [Tasarım konusunda dikkat edilmesi gerekenler](#design)
- [Performans için SignalR sunucunuzu ayarla](#tuning)
- [Performans sorunlarını giderme](#troubleshooting)
- [SignalR performans sayaçlarını kullanma](#perfcounters)
- [Diğer performans sayaçlarını kullanma](#othercounters)
- [Diğer kaynaklar](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Tasarım konusunda dikkat edilmesi gerekenler

Bu bölümde, gereksiz ağ trafiği oluşturarak performansın engellenmediğinden emin olmak için SignalR uygulamasının tasarımı sırasında uygulanabilecek desenler açıklanmaktadır.

### <a name="throttling-message-frequency"></a>İleti sıklığını azaltma

Yüksek frekansta (gerçek zamanlı oyun uygulaması gibi) ileti gönderen bir uygulamada bile, çoğu uygulamanın saniyede birkaç iletiden fazlasını göndermesi gerekmez. Her istemcinin oluşturduğu trafik miktarını azaltmak için, sabit bir hızdan daha sık sıraya alınan ve ileti gönderen bir ileti döngüsü uygulanabilir (diğer bir deyişle, gönderilmek üzere bu zaman aralığında iletiler varsa, her saniye belirli sayıda ileti gönderilir). İletileri belirli bir hıza (hem istemciden hem de sunucudan) azaltan örnek bir uygulama için [SignalR ile Yüksek Frekanslı Gerçek Zamanlı'ya](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)bakın.

### <a name="reducing-message-size"></a>İleti boyutunu küçültme

Seri leştirilmiş nesnelerinizin boyutunu azaltarak SignalR iletisinin boyutunu küçültebilirsiniz. Sunucu kodunda, aktarılması gerekmeyen özellikler içeren bir nesne gönderiyorsanız, bu özelliklerin özniteliği kullanarak `JsonIgnore` seri hale getirilmesini engelleyin. Özelliklerin adları da iletide depolanır; özelliklerinin adları öznitelik kullanılarak `JsonProperty` kısaltılabilir. Aşağıdaki kod örneği, bir özelliğin istemciye gönderilmesini nasıl dışlayabildiğini ve özellik adlarının nasıl kısaltılabildiğini gösterir:

**Verilerin istemciye gönderilmesini hariç tutmak için JsonIgnore özniteliğini ve ileti boyutunu küçültmek için JsonProperty özniteliğini gösteren .NET sunucu kodu**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

İstemci kodunda okunabilirliği/ korunabilmeyi korumak için, kısaltılmış özellik adları, ileti alındıktan sonra insan dostu adlara yeniden eklenebilir. Aşağıdaki kod örneği, bir ileti sözleşmesi (eşleme) tanımlayarak ve sözleşmeyi en iyi duruma `reMap` getirin sınıfına uygulamak için işlevi kullanarak kısaltılmış adları daha uzun adlarla yeniden eşlemenin olası bir yolunu gösterir:

**Kısaltılmış özellik adlarını insan tarafından okunabilir adlara yeniden eşleyen istemci tarafı JavaScript kodu**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Aynı yöntem kullanılarak istemciden sunucuya gelen iletilerde adlar da kısaltılabilir.

İleti nesnesinin bellek ayak izini (diğer bir şekilde ileti için kullanılan bellek miktarını) azaltmak da performansı artırabilir. Örneğin, a `int` aralığının tam aralığı gerekli `short` değilse, a veya `byte` bunun yerine kullanılabilir.

İletiler sunucu belleğinde ileti veri tonunda depolandığından, iletilerin boyutunu azaltmak da sunucu bellek sorunlarını giderebilir.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Performans için SignalR sunucunuzu ayarla

Aşağıdaki yapılandırma ayarları, bir SignalR uygulamasında sunucunuzu daha iyi performans için ayarlamak için kullanılabilir. bir ASP.NET uygulamasında performansı nasıl artırılavureceğiniz hakkında genel bilgi [ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx)için bkz.

**SignalR yapılandırma ayarları**

- **DefaultMessageBufferSize**: Varsayılan olarak SignalR, bağlantı başına hub başına bellekte 1000 ileti saklar. Büyük iletiler kullanılıyorsa, bu değer azaltılarak hafifletilebilecek bellek sorunları oluşturabilir. Bu ayar, ASP.NET `Application_Start` bir uygulamada olay işleyicisi `Configuration` veya kendi kendine barındırılan bir uygulamada bir OWIN başlangıç sınıfı nın yönteminde ayarlanabilir. Aşağıdaki örnek, kullanılan sunucu bellek miktarını azaltmak için uygulamanızın bellek ayak izini azaltmak için bu değeri nasıl azalttığınızı gösterir:

    **.NET sunucu kodu, varsayılan ileti arabellek boyutunu azaltmak için Startup.cs**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS yapılandırma ayarları**

- **Uygulama başına maksimum eşzamanlı istekler**: Eşzamanlı IIS isteklerinin sayısının artırılması, isteklerin sunulması için kullanılabilen sunucu kaynaklarını artırır. Varsayılan değer 5000'dir; bu ayarı artırmak için, yükseltilmiş bir komut istemi aşağıdaki komutları yürütmek:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: Bu, uygulama havuzu için Http.sys kuyrukları en fazla istek sayısıdır. Sıra dolduğunda, yeni istekler 503 "Hizmet Kullanılamıyor" yanıtı alır. Varsayılan değer 1000'dir.

    Uygulamanızı barındıran uygulama havuzunda alt işlem için sıra uzunluğunun kısaltılması bellek kaynaklarını korur. Daha fazla bilgi için bkz: [Uygulama Havuzlarını Yönetme, Ayarla ve Yapılandırma.](https://technet.microsoft.com/library/cc745955.aspx)

**yapılandırma ayarlarını ASP.NET**

Bu `aspnet.config` bölüm, dosyada ayarlanabilen yapılandırma ayarlarını içerir. Bu dosya, platforma bağlı olarak iki konumdan birinde bulunur:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR performansını artırabilecek ASP.NET ayarları şunlardır:

- **CPU başına maksimum eşzamanlı istek**: Bu ayarı artırmak performans darboğazlarını hafifletebilir. Bu ayarı artırmak için dosyaya `aspnet.config` aşağıdaki yapılandırma ayarını ekleyin:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **İstek Sırası Sınırı**: Toplam bağlantı sayısı `maxConcurrentRequestsPerCPU` ayarı aştığında, ASP.NET bir sıra kullanarak istekleri azaltmaya başlar. Sıranın boyutunu artırmak için `requestQueueLimit` ayarı artırabilirsiniz. Bunu yapmak için, düğüme aşağıdaki `processModel` yapılandırma `config/machine.config` ayarını `aspnet.config`ekleyin (yerine):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Performans sorunlarını giderme

Bu bölümde, uygulamanızda performans sorunları bulmayolları açıklanmaktadır.

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket'in kullanıldığını doğrulama

SignalR istemci ve sunucu arasındaki iletişim için çeşitli aktarımlar kullanabilir, ancak WebSocket önemli bir performans avantajı sunar ve istemci ve sunucu bunu destekliyorsa kullanılmalıdır. İstemcinizin ve sunucunuzun WebSocket gereksinimlerini karşılayıp karşılamadığını belirlemek için [Taşımalar ve Geri Dönüşler'e](../getting-started/introduction-to-signalr.md#transports)bakın. Uygulamanızda hangi aktarımın kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanabilir ve bağlantı için hangi aktarımın kullanıldığını görmek için günlükleri inceleyebilirsiniz. Internet Explorer ve Chrome'daki tarayıcı geliştirme araçlarını kullanma hakkında daha fazla bilgi için [Taşımalar ve Geri Dönüşler'e](../getting-started/introduction-to-signalr.md#transports)bakın.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR performans sayaçlarını kullanma

Bu bölümde, `Microsoft.AspNet.SignalR.Utils` pakette bulunan SignalR performans sayaçlarının nasıl etkinleştirilip kullanılacağı açıklanmaktadır.

### <a name="installing-signalrexe"></a>signalr.exe kurulumu

Performans sayaçları SignalR.exe adlı bir yardımcı program kullanılarak sunucuya eklenebilir. Bu yardımcı programı yüklemek için aşağıdaki adımları izleyin:

1. Visual Studio'da, **Araçlar** > **NuGet Paket Yöneticisi** > **Çözüm için NuGet Paketlerini Yönet'i** seçin
2. **Signalr.utils'i**arayın ve Yükle'yi seçin.

    ![](signalr-performance/_static/image1.png)
3. Paketi yüklemek için lisans sözleşmesini kabul edin.
4. SignalR.exe'ye `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe ile performans sayaçları yükleme

SignalR performans sayaçlarını yüklemek için SignalR.exe'yi aşağıdaki parametreyle yükseltilmiş bir komut istemiyle çalıştırın:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR performans sayaçlarını kaldırmak için SignalR.exe'yi aşağıdaki parametreyle yükseltilmiş bir komut istemiyle çalıştırın:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR Performans sayaçları

Yardımcı programlar paketi aşağıdaki performans sayaçlarını yükler. "Toplam" sayaçları, son uygulama havuzu veya sunucu yeniden başlatılmasından bu yana olayların sayısını ölçer.

**Bağlantı ölçümleri**

Aşağıdaki ölçümler, oluşan bağlantı ömrü olaylarını ölçer. Daha fazla bilgi için [bkz.](../guide-to-the-api/handling-connection-lifetime-events.md)

- **Bağlı Bağlantılar**
- **Bağlantılar Yeniden Bağlandı**
- **Bağlantıları Kesildi**
- **Bağlantılar Güncel**

**İleti ölçümleri**

Aşağıdaki ölçümler SignalR tarafından oluşturulan ileti trafiğini ölçer.

- **Toplam Alınan Bağlantı İletileri**
- **Toplam Gönderilen Bağlantı İletileri**
- **Alınan Bağlantı İletileri/Sn**
- **Gönderilen Bağlantı İletileri/Sn**

**İleti veri günü ölçümleri**

Aşağıdaki ölçümler, gelen ve giden tüm SignalR iletilerinin yerleştirildiği sıra olan dahili SignalR ileti veri yolundaki trafiği ölçer. İleti gönderildiğinde veya yayınlandığında **yayınlanır.** Bu bağlamda **abone,** ileti veri yolundaki bir aboneliktir; bu istemci sayısı artı sunucunun kendisi eşit olmalıdır. **Ayrılan Çalışan,** etkin bağlantılara veri gönderen bir bileşendir; **Meşgul** İşçisi, etkin olarak ileti gönderen bir çalışandır.

- **İleti Veri Gönderi Mesajları Toplam Alınan**
- **Alınan İleti Veri Gönderi Mesajları/Sn**
- **İleti Veri Günü Mesajları Toplam Yayınlandı**
- **İleti Veri Günü Mesajları Yayınlandı/Sn**
- **Mesaj Veri Günü Aboneleri Güncel**
- **İleti Veri Günü Aboneleri Toplamı**
- **İleti Veri Günü Aboneleri/Sn**
- **İleti Veri Otobüsü Tahsisli İşçiler**
- **Mesaj Otobüs Meşgul İşçiler**
- **İleti Veri Günü Konuları Güncel**

**Hata ölçümleri**

Aşağıdaki ölçümler SignalR ileti trafiği tarafından oluşturulan hataları ölçer. **Hub** veya hub yöntemi çözülemediğinde Hub Çözümü hataları oluşur. **Hub Çağırma** hataları, hub yöntemini çağırırken atılan özel durumlardır. **Aktarım** hataları, http isteği veya yanıtı sırasında atılan bağlantı hatalarıdır.

- **Hatalar: Tüm Toplam**
- **Hatalar: Tümü/Sn**
- **Hatalar: Hub Çözünürlük Toplamı**
- **Hatalar: Hub Çözünürlüğü/Sn**
- **Hatalar: Hub Çağırma Toplamı**
- **Hatalar: Hub Çağırma/Sn**
- **Hatalar: Aktarım Toplamı**
- **Hatalar: Aktarım/Sn**

<a id="scaleout_metrics"></a>

**Ölçeklendirme ölçümleri**

Aşağıdaki ölçümler, ölçeklendirme sağlayıcısı tarafından oluşturulan trafiği ve hataları ölçer. Bu bağlamda bir **Akış** ölçeklendirme sağlayıcısı tarafından kullanılan bir ölçek birimidir; BU tablo, SQL Server kullanılıyorsa, Hizmet Veri Tos'u kullanılıyorsa bir Konu ve Redis kullanılıyorsa Abonelik. Her akış, sipariş edilen okuma ve yazma işlemlerini sağlar; tek bir akış olası bir ölçek darboğaz, bu nedenle akış sayısı bu darboğaz azaltmaya yardımcı olmak için artırılabilir. Birden çok akış kullanılırsa, SignalR iletileri bu akışlar arasında belirli bir bağlantıdan gönderilen iletilerin sıralı olmasını sağlayacak şekilde otomatik olarak dağıtır (parça) iletileri dağıtır.

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) ayarı SignalR tarafından tutulan ölçekçıkış gönderme sırasının uzunluğunu denetler. 0'dan büyük bir değere ayarlanması, tüm iletileri yapılandırılmış ileti arka düzlemine teker teker gönderilmek üzere gönderme kuyruğuna yerleştirilecektir. Sıranın boyutu yapılandırılan uzunluğun üzerine çıkarsa, sonraki gönderme çağrıları, kuyruktaki ileti sayısı yeniden ayardan daha az olana kadar Geçersiz [İşlem Özel Durum](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ile hemen başarısız olur. Uygulanan arka uçakların genellikle kendi sıraya veya akış denetimi yerinde olduğundan, kuyruk lar varsayılan olarak devre dışı bırakılır. SQL Server durumunda, bağlantı birleştirme, herhangi bir anda devam eden gönderme sayısını etkin bir şekilde sınırlar.

Varsayılan olarak, SQL Server ve Redis için yalnızca bir akış kullanılır, Hizmet Veri Servisi için beş akış kullanılır ve kuyruk devre dışı bırakılır, ancak bu ayarlar SQL Server ve Service Bus'taki yapılandırma yoluyla değiştirilebilir:

**.NET Server Kodu SQL Server backplane için tablo sayısı ve kuyruk uzunluğu yapılandırmak için**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**.NET Sunucu Kodu Servis Veri Yolu backplane için konu sayısı ve kuyruk uzunluğu yapılandırmak için**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**Arabelleğe Alma** akışı, hatalı bir duruma girmiş olan dır; Akış hatalı durumda olduğunda, geri düzleme gönderilen tüm iletiler akış artık hata yapmayana kadar hemen başarısız olur. **Sıra Gönder Uzunluğu,** deftere nakledilen ancak henüz gönderilmemiş ileti lerin sayısıdır.

- **Alınan İleti Veri Gönderi mesajlarını ölçeklendirme/Sn**
- **Ölçeklendirme Akışları Toplamı**
- **Ölçeklendirme Akışları Aç**
- **Ölçeklendirme Akışları Arabelleğe Alma**
- **Ölçeklendirme Hataları Toplamı**
- **Ölçeklendirme Hataları/Sn**
- **Scaleout Sıra Uzunluğu Gönder**

Bu sayaçların neleri ölçtüğü hakkında daha fazla bilgi için Azure [Hizmet Veri Yolunda Sinyal Ölçer](scaleout-with-windows-azure-service-bus.md)'e bakın.

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Diğer performans sayaçlarını kullanma

Aşağıdaki performans sayaçları, uygulamanızın performansını izlemede de yararlı olabilir.

**Bellek**

- .NET CLR\\Bellek # tüm Yığınları bayt (w3wp için)

**ASP.NET**

- ASP.NET\İstekleri Geçerli
- ASP.NET\Sıraya
- ASP.NET\Reddedildi

**CPU**

- İşlemci Bilgileri\İşlemci Süresi

**TCP/IP**

- TCPv6/Bağlantılar Kuruldu
- TCPv4/Bağlantılar Kuruldu

**Web Hizmeti**

- Web Hizmeti\Geçerli Bağlantılar
- Web Hizmeti\Maksimum Bağlantılar

**İş Parçacığı Oluşturma**

- .NET CLR Kilitler\\Ve Konuları # geçerli mantıksal Konuları
- .NET CLR Kilitler\\Ve Konuları # geçerli fiziksel Konuları

<a id="otherresources"></a>

## <a name="other-resources"></a>Diğer Kaynaklar

ASP.NET performans izleme ve aetmehakkında daha fazla bilgi için aşağıdaki konulara bakın:

- [ASP.NET Performansa Genel Bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5, IIS 7.0 ve IIS 6.0'da ASP.NET İş Parçacığı Kullanımı](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; Element (Web Ayarları)](https://msdn.microsoft.com/library/dd560842.aspx)
