---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Ek: Düzeltme Örneği Uygulaması (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma) | Microsoft Dokümanlar'
author: MikeWasson
description: Azure e-kitaplı Building Real World Cloud Apps, Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bu 13 desen ve uygulamaları açıklar ki o olabilir ...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675994"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Ek: Düzeltme Örneği Uygulaması (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)

Mike [Wasson](https://github.com/MikeWasson)tarafından , [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure e-kitaplı **Building Real World Cloud Apps,** Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bulut için web uygulamalarını geliştirmekte başarılı olmanıza yardımcı olabilecek 13 model ve uygulamayı açıklar. E-kitap hakkında bilgi için [ilk bölüme](introduction.md)bakın.

Azure e-kitaplı Bina Gerçek Dünya Bulut Uygulamaları Oluşturma ekinde, indirebileceğiniz Fix It örnek uygulaması hakkında ek bilgi sağlayan aşağıdaki bölümler yer almaktadır:

- [Bilinen sorunlar](#knownissues)
- [En iyi uygulamalar](#bestpractices)
- [Uygulamayı Visual Studio'dan yerel bilgisayarınızda çalıştırma](#run-in-vs)
- [Windows PowerShell komut dosyalarını kullanarak temel uygulamayı Azure App Service Web Apps'a dağıtma](#deploybase)
- [Windows PowerShell komut dosyalarının sorun giderme](#troubleshooting)
- [Sıra işleme yle uygulamayı Azure App Service Web Apps ve Azure Bulut Hizmeti'ne dağıtma](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Bilinen sorunlar

Fix It uygulaması aslında bu e-kitapta sunulan bazı desenleri mümkün olduğunca basit bir şekilde göstermek için geliştirilmiştir. Ancak, e-kitap gerçek dünya uygulamaları oluşturmak la ilgili olduğundan, Fix It kodunu, yayımlanan yazılımlar için yaptığımıza benzer bir inceleme ve test sürecine tabi ledik. Bir takım sorunlar bulduk ve herhangi bir gerçek dünya uygulamasında olduğu gibi, bazılarını düzelttedik ve bazılarını daha sonraki bir yayına erteledik.

Aşağıdaki liste, bir üretim uygulamasında ele alınması gereken sorunları içerir, ancak şu veya bu nedenle Fix It örnek uygulamasının ilk sürümünde ele alınmamaya karar verdik.

### <a name="security"></a>Güvenlik

- Var olmayan bir sahipe görev atayamayacağından emin olun.
- Yalnızca oluşturduğunuz veya size atanmış olan görevleri görüntüleyip değiştirebildiğinizden emin olun.
- Oturum açma sayfaları ve kimlik doğrulama çerezleri için HTTPS'yi kullanın.
- Kimlik doğrulama tanımlama bilgileri için bir zaman sınırı belirtin.

### <a name="input-validation"></a>Giriş doğrulaması

Genel olarak, bir üretim uygulaması Fix It uygulamasından daha fazla giriş doğrulaması yapar. Örneğin, yükleme için izin verilen resim boyutu / resim dosyası boyutu sınırlı olmalıdır.

### <a name="administrator-functionality"></a>Yönetici işlevselliği

Bir yönetici varolan görevlerin sahipliğini değiştirebilmeli. Örneğin, bir görevin oluşturucusu şirketten ayrılarak, yönetim erişimi etkinleştirilmedikçe hiç kimseye görevi sürdürme yetkisi bırakamaz.

### <a name="queue-message-processing"></a>Sıra iletisi işleme

Fix It uygulamasındaki sıra iletisi işleme, en az kod miktarıyla sıra merkezli iş deseni göstermek için basit olacak şekilde tasarlanmıştır. Bu basit kod gerçek bir üretim uygulaması için yeterli olmaz.

- Kod, her sıra iletisinin en fazla bir kez işlenmesini garanti etmez. Kuyruktan bir ileti aldığınızda, iletinin diğer sıra dinleyicileri tarafından görülemeyen bir zaman ası süresi vardır. İleti silinmeden önce zaman aşımı sona ererse, ileti yeniden görünür hale gelir. Bu nedenle, bir alt rol örneği bir iletiyi işlemek için uzun bir zaman harcarsa, teorik olarak aynı iletinin iki kez işlenmesi ve veritabanında yinelenen bir görevle sonuçlanması mümkündür. Bu sorunla ilgili daha fazla bilgi için Azure [Depolama Kuyruklarını Kullanma](https://msdn.microsoft.com/library/ff803365.aspx#sec7)konusuna bakın.
- Sıra yoklama mantığı, ileti alma toplu olarak, daha uygun maliyetli olabilir. [CloudQueue.GetMessageAsync'i](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)her aradığınızda bir işlem maliyeti vardır. Bunun yerine, tek bir işlemde birden çok ileti alan [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (çoğul 's'' nota) arayabilirsiniz. Azure Depolama Kuyrukları için işlem maliyetleri çok düşükolduğundan, çoğu senaryoda maliyetler üzerindeki etkisi önemli değildir.
- Sıra iletiişleme kodundaki sıkı döngü, çok çekirdekli VM'leri verimli bir şekilde kullanmayan CPU yakınlığına neden olur. Daha iyi bir tasarım, birkaç async görevi paralel olarak çalıştırmak için görev paralelliği kullanır.
- Sıra iletiişleme yalnızca temel özel durum işleme vardır. Örneğin, kod [zehirli iletileri](https://msdn.microsoft.com/library/ms789028.aspx)işlemez. (İleti işleme bir özel durum neden olduğunda, hata günlüğe kaydetmeniz ve iletiyi silmeniz gerekir veya alt rol yeniden işlemeye çalışır ve döngü süresiz olarak devam eder.)

### <a name="sql-queries-are-unbounded"></a>SQL sorguları sınırsız

Geçerli Düzeltme Kodu, Dizin sayfaları için sorguların kaç satır dönebileceğine sınırlama getirmaz. Veritabanına büyük miktarda görev girilirse, elde edilen listelerin boyutu performans sorunlarına neden olabilir. Çözüm sayfalama uygulamaktır. Örneğin, ASP.NET [bir MVC Uygulamasında Varlık Çerçevesi ile Sıralama, Filtreleme ve Sayfalama'ya](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)bakın.

### <a name="view-models-recommended"></a>Önerilen modelleri görüntüleme

Fix It uygulaması, denetleyici ve görünüm arasında bilgi aktarmak için FixItTask varlık sınıfını kullanır. En iyi yöntem görünüm modellerini kullanmaktır. Etki alanı modeli (örneğin, FixItTask varlık sınıfı) veri kalıcılığı için gerekenler etrafında tasarlanırken, veri sunumu için bir görünüm modeli tasarlanabilir. Daha fazla bilgi için [12 ASP.NET MVC En İyi Uygulamalar'a](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)bakın.

### <a name="secure-image-blob-recommended"></a>Güvenli görüntü blob önerilir

Fix It uygulaması yüklenen görüntüleri herkese açık olarak saklar, bu da URL'yi bulan herkesin görüntülere erişebileceği anlamına gelir. Görüntüler halka açık değil, güvenli olabilir.

### <a name="no-powershell-automation-scripts-for-queues"></a>Kuyruklar için PowerShell otomasyon komut dosyası yok

Örnek PowerShell otomasyon komut dosyaları yalnızca Tamamen Azure App Service Web Apps'ta çalışan Fix It'in temel sürümü için yazılmıştır. Web uygulamasının yanı sıra sıra sıra işleme için gereken Bulut Hizmeti ortamını kurmak ve dağıtmak için komut dosyaları sağlamadık.

### <a name="special-handling-for-html-codes-in-user-input"></a>Kullanıcı girişindeki HTML kodları için özel işleme

ASP.NET, kötü amaçlı kullanıcıların kullanıcı giriş metin kutularına komut dosyası girerek site ler arası komut dosyası saldırılarını denemesini otomatik olarak önler. Ve görev `DisplayFor` başlıklarını ve notlarını görüntülemek için kullanılan MVC yardımcısı tarayıcıya gönderdiği değerleri otomatik olarak HTML kodlar. Ancak bir üretim uygulamasında ek önlemler almak isteyebilirsiniz. Daha fazla bilgi için [ASP.NET'da İstek Doğrulama'ya](https://msdn.microsoft.com/library/hh882339.aspx)bakın.

<a id="bestpractices"></a>
## <a name="best-practices"></a>En iyi uygulamalar

Aşağıda, Fix It uygulamasının orijinal sürümünün kod incelemesi ve test edilmesinde keşfedildikten sonra düzeltilen bazı sorunlar yer alıyor. Bazıları orijinal kodlayıcının belirli bir en iyi uygulamadan haberdar olmamasından, bazıları nın ise kodun hızlı bir şekilde yazıldığı ve serbest bırakılan yazılımlar için tasarlanmadığından kaynaklanıyordu. Bu incelemeden ve testlerden öğrendiğimiz ve web uygulamaları geliştiren diğer kişiler için de yararlı olabilecek bir şey olması durumunda, sorunları burada sıralıyoruz.

### <a name="dispose-the-database-repository"></a>Veritabanı deposunu elden çıkar

Sınıf, `FixItTaskRepository` Varlık Çerçevesi `DbContext` örneğini imha etmelidir. Bunu `FixItTaskRepository` sınıfta uygulayarak `IDisposable` yaptık:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac'ın `FixItTaskRepository` örneği otomatik olarak imha edeceğini unutmayın, bu nedenle açıkça imha yapmamıza gerek yoktur.

Başka bir seçenek, `DbContext` üye `FixItTaskRepository`değişkeni kaldırmak ve `DbContext` bunun yerine her depo yöntemi `using` içinde bir deyim içinde yerel bir değişken oluşturmaktır. Örneğin:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Di ile singletons gibi kayıt

`PhotoService` Sınıf ve `Logger` sınıfın yalnızca bir örneği gerektiğinden, bu sınıflar *DependenciesConfig.cs*bağımlılık [enjeksiyonu için tek örnek olarak kaydedilmelidir:](https://code.google.com/p/autofac/wiki/InstanceScope)

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Güvenlik: Kullanıcılara hata ayrıntıları gösterme

Orijinal Fix It uygulamasının genel bir hata sayfası yoktu ve tüm özel durumların UI'ye kadar kabarcıklar oluşturmasına izin verin, bu nedenle veritabanı bağlantı hataları gibi bazı özel durumlar tarayıcıya tam bir yığın izlemenin görüntülenmesine neden olabilir. Ayrıntılı hata bilgileri bazen kötü niyetli kullanıcıların saldırılarını kolaylaştırabilir. Çözüm, özel durum ayrıntılarını günlüğe kaydetmek ve kullanıcıya hata ayrıntıları içermeyen bir hata sayfası görüntülemektir. Fix It uygulaması zaten günlüğe kaydediyordu ve bir hata `<customErrors mode=On>` sayfası görüntülemek için Web.config dosyasına ekledik.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Varsayılan olarak bu, *Görünümler\Paylaşılan\Error.cshtml* hataları için görüntülenmesine neden olur. *Error.cshtml'i* özelleştirebilir veya kendi hata sayfa `defaultRedirect` görünümünüzü oluşturabilir ve bir öznitelik ekleyebilirsiniz. Belirli hatalar için farklı hata sayfaları da belirtebilirsiniz.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Güvenlik: yalnızca bir görevin oluşturucusu tarafından düzenlenmesine izin verir

Pano Dizini sayfası yalnızca oturum açmış kullanıcı tarafından oluşturulan görevleri gösterir, ancak kötü amaçlı bir kullanıcı başka bir kullanıcının görevine kimlik içeren bir URL oluşturabilir. Bu durumda bir 404 dönmek için *DashboardController.cs* kodu ekledik:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>İstisnaları yutmayın

Özgün Fix It uygulaması, SQL sorgusundan kaynaklanan bir özel durum kaydettikten sonra geçersiz olarak döndü:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

Bu, sorgu başarılı ama sadece herhangi bir satır döndürmemiş gibi kullanıcıya görünmesini sağlar. Çözüm, yakalama ve günlüğe kaydetme sonrasında özel durumu yeniden atmaktır:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Çalışan rollerindeki tüm özel durumları yakalama

İşçi rolündeki işlenmemiş özel durumlar VM'nin geri dönüştürülmesine neden olur, bu nedenle yaptığınız her şeyi bir try-catch bloğunda sarmak ve tüm özel durumları işlemek istersiniz.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Varlık sınıflarındaki dize özellikleri için uzunluk belirtin

Basit kodu görüntülemek için Fix It uygulamasının özgün sürümü, FixItTask kuruluşunun alanları için uzunlukları belirtmedi ve sonuç olarak veritabanında varchar(max) olarak tanımlandı. Sonuç olarak, UI hemen hemen her miktarda giriş kabul eder. Uzunlukları belirtmek, hem web sayfasındaki kullanıcı girişi hem de veritabanındaki sütun boyutu için geçerli sınırlar belirler:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Özel üyeleri yalnızca değiştirmeleri beklenmiyorsa okuma olarak işaretleyin

Örneğin, `DashboardController` sınıfta bir örnek `FixItTaskRepository` oluşturulur ve değişmesi beklenmediği için onu yalnızca [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)olarak tanımladık.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Listeyi kullan. Liste yerine Any() Sayı() &gt; 0

Tek umursadığınız, bir listedeki bir veya daha fazla öğenin belirtilen ölçütlere uygun olup olmadığıysa, [ölçütlere](https://msdn.microsoft.com/library/bb534972.aspx) `Count` uyan bir öğe bulunur bulunmaz geri döndüğünden, yöntem her zaman her öğeyi yinelemek zorunda olduğundan, Any yöntemini kullanın. Pano *Index.cshtml* dosyasında başlangıçta şu kod vardı:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Bunu şu şekilde değiştirdik:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC yardımcılarını kullanarak MVC görünümlerinde URL'ler oluşturma

Ana sayfadaki **Düzelt düğmesi** için, Fix It uygulaması bir bağlantı öğesini sabit olarak kodlur:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

Bunun gibi Görünüm/Eylem bağlantıları için [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML yardımcısını kullanmak daha iyidir, örneğin:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Thread.Sleep yerine Thread.Delay yerine Görev.Delay'ı kullanma

Yeni proje şablonu, bir alt rol için örnek kodu koyar, `Thread.Sleep` ancak iş parçacığının uyku moduna neden olması iş parçacığı havuzunun ek gereksiz iş parçacıkları oluşturmasına neden olabilir. Bunun yerine [Task.Delay'ı](https://msdn.microsoft.com/library/hh139096.aspx) kullanarak bunu önleyebilirsiniz.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Async boşluğundan kaçının

Bir async yöntemi bir değer döndürmek için gerek `Task` yoksa, `void`yerine bir tür döndürün.

Bu örnek sınıftan: `FixItQueueManager`

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

Yalnızca üst `async void` düzey olay işleyicileri için kullanmalısınız. Bir yöntemi `async void`, arayanın yöntemi ni **bekleyemez** veya yöntemin attığı özel durumları yakalayamaz. Daha fazla bilgi için, [Asynchronous Programming'deki En İyi Uygulamalar'a](https://msdn.microsoft.com/magazine/jj991977.aspx)bakın.

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>İşçi rol döngüsünden kırmak için iptal belirteci kullanma

Genellikle, bir alt rol üzerinde **Çalıştır** yöntemi sonsuz bir döngü içerir. İşçi rolü durduğunda [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) yöntemi çağrılır. **Çalıştır** yöntemi içinde yapılan işi iptal etmek ve düzgün bir şekilde çıkmak için bu yöntemi kullanmalısınız. Aksi takdirde, işlem bir işlemin ortasında sonlandırılabilir.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Otomatik MIME Koklama Prosedürü'nden vazgeçin

Bazı durumlarda, Internet Explorer web sunucusu tarafından belirtilen türden farklı bir MIME türü raporlar. Örneğin, Internet Explorer HTTP yanıt üstbilgisi İçerik Türü: metin/düz ile teslim edilen bir dosyada HTML içeriği bulursa, Internet Explorer içeriğin HTML olarak işlenmesi gerektiğini belirler. Ne yazık ki, bu "MIME koklama" da güvenilmeyen içerik barındıran sunucular için güvenlik sorunlarına yol açabilir. Bu sorunla mücadele etmek için, Internet Explorer 8 MIME türü belirleme kodunda bir dizi değişiklik yaptı ve uygulama geliştiricilerin [MIME-sniffing dışında devre dışı](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)bırakmak için izin verir. *Web.config* dosyasına aşağıdaki kod eklendi.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Donma ve minifikasyonu etkinleştirme

Visual Studio yeni bir web projesi oluşturduğunda, JavaScript dosyalarının donlanması ve donifikasyonu varsayılan olarak etkinleştirmez. BundleConfig.cs bir kod satırı ekledik:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Kimlik doğrulama tanımlama bilgileri için son kullanma süresi ayarlama

Varsayılan olarak, kimlik doğrulama tanımlama bilgilerinin süresi iki hafta içinde sona erer. Daha kısa bir süre daha güvenlidir. Bu ayarı *StartupAuth.cs*olarak değiştirebilirsiniz:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>Uygulamayı Visual Studio'dan yerel bilgisayarınızda çalıştırma

Fix It uygulamasını çalıştırmanın iki yolu vardır:

- Yeni görevler doğrudan SQL veritabanına yazan temel uygulamayı çalıştırın.
- Görevleri oluşturmak için bir kuyruk artı bir arka uç hizmeti kullanarak uygulamayı çalıştırın. Sıra deseni, Sıra [Merkezli Çalışma Deseni](queue-centric-work-pattern.md)bölümünde açıklanmıştır.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Temel uygulamayı çalıştırma

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)'yi yükleyin.
2. Visual [Studio için .NET için Azure SDK'yı](https://azure.microsoft.com/downloads/)yükleyin.
3. .zip dosyasını [MSDN Kod Galerisi'nden](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)indirin.
4. Dosya Gezgini'nde .zip dosyasına sağ tıklayın ve Özellikler penceresinde Engeli Kaldır'ı tıklatın.
5. Dosyanın zip'ini açın.
6. Visual Studio'yu başlatmak için .sln dosyasına çift tıklayın.
7. **Araçlar** menüsünden **NuGet Paket**Yöneticisi'ni, ardından **Paket Yöneticisi Konsolu'nu**tıklatın.
8. Paket Yöneticisi Konsolunda (PMC) Geri Yükle'yi tıklatın.
9. Görsel Stüdyo'dan çıkın.
10. Azure [depolama emülatörü'ni](/azure/storage/common/storage-use-emulator)başlatın.
11. Önceki adımda kapattığınız çözüm dosyasını açabildiğiniz Visual Studio'yu yeniden başlatın.
12. FixIt projesinin başlangıç projesi olarak ayarlandıklarına emin olun ve projeyi çalıştırmak için CTRL+F5 tuşuna basın.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Sıra işleme ile uygulamayı çalıştırma

1. Temel uygulamayı [çalıştır](#runbase)için yönergeleri izleyin ve ardından tarayıcıyı kapatın ve Visual Studio'yu kapatın.
2. Visual Studio'u yönetici ayrıcalıklarıyla başlatın. (Azure işlem emülatörü kullanıyor olacaksınız ve bu yönetici ayrıcalıkları gerektirir.)
3. *MyFixIt* projesindeki (web projesi) uygulama *Web.config* dosyasında, `appSettings/UseQueues` "true" değerini değiştirin:

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Azure [depolama emülatörü](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) hala çalışmıyorsa, yeniden başlatın.
5. FixIt web projesini ve MyFixItCloudService projesini aynı anda çalıştırın.

    Visual Studio kullanma:

   1. FixIt projesini çalıştırmak için **F5** tuşuna basın.
   2. **Solution Explorer'da**MyFixItCloudService projesini sağ tıklatın ve ardından **Hata Ayıklama** > **Yeni Örneği Başlat'ı**tıklatın.

    Web için Visual Studio 2013 Express'i kullanma:

   3. Çözüm Gezgini'nde FixIt çözümüne sağ tıklayın ve **Özellikler'i**seçin.
   4. **Birden Çok Başlangıç Projesi**seçin.
   5. MyFixIt ve MyFixItCloudService altındaki **Eylem** açılır listesinde **Başlat'ı**seçin.
   6. **Tamam**'a tıklayın.
   7. Her iki projeyi de çalıştırmak için **F5**'e basın.

      MyFixItCloudService projesini çalıştırdığınızda, Visual Studio Azure işlem emülatörü'ne başlar. Güvenlik duvarı yapılandırmanıza bağlı olarak, emülatörün güvenlik duvarından geçmesine izin vermeniz gerekebilir.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell komut dosyalarını kullanarak temel uygulamayı Azure App Service Web Apps'a dağıtma

[Her Şeyi Otomatikleştir](automate-everything.md) modelini göstermek için, Fix It uygulaması, Azure'da bir ortam oluşturan ve projeyi yeni ortama dağıtan komut dosyalarıyla birlikte verilir. Aşağıdaki yönergeler komut dosyalarının nasıl kullanılacağını açıklar.

Kuyrukları kullanmadan Azure'da çalışmak istiyorsanız ve değişiklikleri kuyruklarla yerel olarak çalışacak şekilde yaptıysanız, aşağıdaki yönergeleri uygulamadan önce UseQueues uygulaması değerini false olarak ayarladığınızdan emin olun.

Bu yönergeler, Fix It çözümlerini yerel olarak zaten indirdiğinizi ve çalıştırdığınızı ve bir Azure hesabınız veya yönetmeye yetkili olduğunuz bir Azure aboneliğiniz olduğunu varsayar.

1. Azure **PowerShell** konsoluna yükleyin. Talimatlar için Azure [PowerShell'i nasıl yükleyip yapılandıracağınıza](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)bakın.

    Bu özelleştirilmiş konsol, Azure aboneliğinizle çalışacak şekilde yapılandırılmıştır. Azure modülü *Program Dosyaları* dizinine yüklenir ve Azure PowerShell konsolunun her kullanımında otomatik olarak alınır.

    Windows PowerShell ISE gibi farklı bir ana bilgisayar programında çalışmayı tercih ediyorsanız, Azure modülunu almak için [Içe Aktarma-Modül](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet'ini kullandığınızdan veya modülün otomatik olarak içe aktarılmasını tetiklemek için Azure modülünde bir komut kullandığınızdan emin olun.
2. Azure PowerShell'i **yönetici olarak Çalıştır** seçeneğiyle başlatın.
3. Azure PowerShell yürütme ilkesini `RemoteSigned`' ye ayarlamak için [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet'i çalıştırın. İlke değişikliğini tamamlamak için **Y** (Evet için) girin.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Bu ayar, dijital olarak imzalanmış yerel komut dosyalarını çalıştırmanızı sağlar. (Yürütme `Unrestricted`ilkesini, daha sonra engellemeyi kaldırma gereksinimini ortadan kaldıracak şekilde de ayarlayabilirsiniz, ancak bu güvenlik nedenleriyle önerilmez.)
4. PowerShell'i `Add-AzureAccount` hesabınız için kimlik bilgileriyle kurmak için cmdlet'i çalıştırın.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Bu kimlik bilgileri bir süre sonra sona erer `Add-AzureAccount` ve cmdlet yeniden çalıştırmak zorunda. Bu e-kitap yazıldığı için kimlik bilgilerinin süresi dolmadan önceki süre 12 saattir.
5. Birden çok aboneliğiniz varsa, test ortamını oluşturmak istediğiniz aboneliği belirtmek için Select-AzureSubscription cmdlet'ini kullanın.
6. Aynı Azure aboneliği için bir yönetim `Get-AzurePublishSettingsFile` sertifikası `Import-AzurePublishSettingsFile` ve cmdlets kullanarak içeri aktarın. Bu cmdlets ilk bir sertifika dosyası indirir ve ikinci sinde bunu almak için bu dosyanın konumunu belirtin. > [!IMPORTANT]
   > Azure hizmetlerinizi yönetmek için kullanılabilecek bir sertifika içerdiğinden, indirilen dosyayı güvenli bir konumda tutun veya işiniz bittiğinde silin.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    Sertifika, SQL Veritabanı sunucusunda bir güvenlik duvarı kuralı ayarlamak için geliştirme makinesinin IP adresini algılayan bir REST API çağrısı için kullanılır.
7. Komut dosyalarını içeren dizine gitmek için `cd` `chdir` [Ayar-Konum](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet'i çalıştırın (diğer adlar , ve `sl`) (Düzelt çözüm klasöründeki *Otomasyon* klasöründe bulunurlar.) Dizin adlarından herhangi biri boşluk içeriyorsa yolu tırnak içine koyun. Örneğin, dizine `c:\Sample Apps\FixIt\Automation` gitmek için aşağıdaki komutu girebilirsiniz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell'in bu komut dosyalarını çalıştırmasına izin vermek için [Engeli Kaldır](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet'ini kullanın. (Komut dosyaları Internet'ten indirildikleri için engellenir.)

    > [!WARNING]
    > Güvenlik - `Unblock-File` Herhangi bir komut dosyası veya çalıştırılabilir dosyaüzerinde çalıştırmadan önce, Dosyayı Not Defteri'nde açın, komutları inceleyin ve kötü amaçlı kod içermediklerini doğrulayın.

    Örneğin, aşağıdaki komut geçerli `Unblock-File` dizindeki tüm komut dosyaları üzerinde cmdlet çalışır.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Taban için web uygulamasını oluşturmak için (kuyruk işleme yok) Fix It uygulamasını düzeltin, ortam oluşturma komut dosyasını çalıştırın.

    Gerekli `Name` parametre veritabanının adını belirtir ve komut dosyasının oluşturduğu depolama hesabı için de kullanılır. Ad, azurewebsites.net etki alanı içinde genel olarak benzersiz olmalıdır. Fixit veya Test (veya örnekte olduğu gibi fixitdemo) gibi benzersiz olmayan `New-AzureWebsite` bir ad belirtirseniz, cmdlet çakışmayı bildiren bir İç Hata ile başarısız olur. Komut dosyası, web uygulamaları, depolama hesapları ve veritabanları için ad gereksinimlerine uymak için adı tüm küçük harfe dönüştürür.

    Gerekli `SqlDatabasePassword` parametre, SQL Veritabanı için oluşturulacak yönetici hesabının parolasını belirtir. Parolaya özel XML karakterleri eklemeyin&amp; &lt; &gt; (;). Bu, komut dosyalarının yazılma biçiminin bir sınırlamasıdır, Azure'un sınırlaması değildir.

    Örneğin, "fixitdemo" adlı bir web uygulaması oluşturmak ve "Passw0rd1" bir SQL Server yönetici parolası kullanmak istiyorsanız, aşağıdaki komutu girebilirsiniz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Ad azurewebsites.net etki alanında benzersiz olmalıdır ve parola karmaşıklığı için SQL Veritabanı gereksinimlerini karşılamalıdır. (Passw0rd1 örneği gereksinimleri karşılamaktadır.)

    Komutun "" ile başladığını unutmayın. \". Komut dosyalarının kötü amaçlı yürütülmesini önlemeye yardımcı olmak için, Windows PowerShell bir komut dosyası çalıştırdığınızda komut dosyası dosyasına tam nitelikli yolu sağlamanızı gerektirir. Geçerli dizini belirtmek için bir nokta kullanabilirsiniz\"(". ) veya aşağıdakiler gibi tam nitelikli yolu sağlar:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Komut dosyası hakkında daha fazla `Get-Help` bilgi için cmdlet'i kullanın.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    İade edilen `Detailed`yardımı `Full` `Parameters`filtrelemek `Examples` için Yardım Al cmdlet'in , , ve parametrelerini kullanabilirsiniz.

    Komut dosyası başarısız olursa veya "Yeni-AzureWeb Sitesi : Önce Set-AzureAboneliği ve Select-AzureSubscription'ı arayın" gibi hatalar üretirse, Azure PowerShell yapılandırmasını tamamlamamış olabilirsiniz.

    Komut dosyası bittikten sonra, [Her Şeyi Otomatikleştir](automate-everything.md) bölümünde gösterildiği gibi oluşturulan kaynakları görmek için Azure Yönetim Portalı'nı kullanabilirsiniz.
10. FixIt projesini yeni Azure ortamına dağıtmak için *AzureWebsite.ps1* komut dosyasını kullanın. Örneğin:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Dağıtım bittiğinde, tarayıcı Azure'da Fix It ile açılır.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell komut dosyalarının sorun giderme

Bu komut dosyalarını çalıştırırken karşılaşılan en yaygın hatalar izinlerle ilgilidir. Bunu ve `Add-AzureAccount` `Import-AzurePublishSettingsFile` başarılı olduğundan ve bunları aynı Azure aboneliği için kullandığınızdan emin olun. Başarılı `Add-AzureAccount` olsa bile tekrar çalıştırmak zorunda klabilirsiniz. Eklenen izinlerin `Add-AzureAccount` süresi 12 saat içinde doluyor.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>Nesne başvurusu bir nesnenin örneğine ayarlı değil.

Komut dosyası, "Nesne başvurusu bir nesnenin bir örneğine ayarlanmaz" gibi hataları döndürürse, bu da Windows PowerShell'in işleyebileceği bir nesne bulamadığı anlamına gelir (bu geçersiz bir başvuru özel dir), `Add-AzureAccount` cmdlet'i çalıştırın ve komut dosyasını yeniden deneyin.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: Sunucu bir iç hata yla karşılaştı.

Cmdlet, `New-AzureWebsite` ad azurewebsites.net etki alanında benzersiz olmadığında bir iç hata döndürür. Hatayı gidermek için, *Yeni AzureWebsiteEnv.ps1'in*Ad parametresi olan ad için farklı bir değer kullanın.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Komut dosyasını yeniden başlatma

"Komut Dosyası tamamlandı" iletisini yazdırmadan önce başarısız olduğu için *Yeni AzureWebsiteEnv.ps1* komut dosyasını yeniden başlatmanız gerekiyorsa, komut dosyasının durdurulmadan önce oluşturduğu kaynakları silmek isteyebilirsiniz. Örneğin, komut dosyası Zaten ContosoFixItDemo web uygulaması oluşturdu ve aynı adla komut dosyası yeniden çalıştırın, ad kullanımda olduğu için komut dosyası başarısız olur.

Komut dosyasının durdurulmadan önce hangi kaynakları oluşturduğunu belirlemek için aşağıdaki cmdlets'i kullanın:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Bu cmdlet çalıştırmak için, `Get-AzureSqlDatabase`boru veritabanı sunucu adı:`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

Bu kaynakları silmek için aşağıdaki komutları kullanın. Veritabanı sunucusunu silerseniz, sunucuyla ilişkili veritabanlarını otomatik olarak sildiğinizi unutmayın.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Sıra işleme yle uygulamayı Azure App Service Web Apps ve Azure Bulut Hizmeti'ne dağıtma

Kuyrukları etkinleştirmek için MyFixIt\Web.config dosyasında aşağıdaki değişikliği yapın. Altında `appSettings`, "true" değerini değiştirin: `UseQueues`

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Daha [önce](#deploybase)açıklandığı gibi MVC uygulamasını Azure App Service'deki bir web uygulamasına dağıtın.

Ardından, yeni bir Azure bulut hizmeti oluşturun. Fix It uygulamasında yer alan komut dosyaları bulut hizmeti oluşturmaz veya dağıtmaz, bu nedenle bunun için Azure portalını kullanmanız gerekir. Portalda, **Yeni** -- **Bilgi İşlem** - Bulut **Hizmeti** -- **Hızlı Oluştur'u**tıklatın ve ardından bir URL ve veri merkezi konumu girin. Web uygulamasını dağıttığınız aynı veri merkezini kullanın.

![](the-fix-it-sample-application/_static/image1.png)

Bulut hizmetini dağıtmadan önce yapılandırma dosyalarından bazılarını güncelleştirmeniz gerekir.

MyFixIt.WorkerRole\app.config'de, `connectionStrings`bağlantı dizesinin `appdb` değerini SQL Veritabanı için gerçek bağlantı dizesi ile değiştirin. Bağlantı dizesini portaldan alabilirsiniz. Portalda,**ADO .Net, ODBC, PHP ve JDBC için** **SQL Databases** - **appdb** - View SQL Database bağlantı dizelerini tıklatın. ADO.NET bağlantı dizesini kopyalayın ve değeri app.config dosyasına yapıştırın. Veritabanı parolanızla\_\_"{parolanızı burada}" olarak değiştirin. (MVC uygulamasını dağıtmak için komut dosyalarını kullandığınızı varsayarsak, `SqlDatabasePassword` komut dosyası parametresinde veritabanı parolasını belirttiniz.)

Sonuç aşağıdaki gibi görünmelidir:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

Aynı MyFixIt.WorkerRole\app.config dosyasında, `appSettings`Azure depolama hesabı için iki yer tutucu değerini değiştirin.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Erişim anahtarını portaldan alabilirsiniz. [Depolama Hesaplarını Nasıl Yönetirene](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)Bakın.

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg'de Azure depolama hesabı için aynı iki yer tutucu değerini değiştirin.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Artık bulut hizmetini dağıtmaya hazırsınız. Solution Explore'ta MyFixItCloudService projesine sağ tıklayın ve **Yayımla'yı**seçin. Daha fazla bilgi için, [bu öğreticinin](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2.[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)

> [!div class="step-by-step"]
> [Önceki](more-patterns-and-guidance.md)
