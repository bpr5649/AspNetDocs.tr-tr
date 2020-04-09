---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: İzleme ve Telemetri (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma) | Microsoft Dokümanlar
author: MikeWasson
description: Azure e-kitaplı Building Real World Cloud Apps, Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bu 13 desen ve uygulamaları açıklar ki o olabilir ...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676036"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>İzleme ve Telemetri (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)

Mike [Wasson](https://github.com/MikeWasson)tarafından , [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya Download [E-kitap indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-kitaplı **Building Real World Cloud Apps,** Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bulut için web uygulamalarını geliştirmekte başarılı olmanıza yardımcı olabilecek 13 model ve uygulamayı açıklar. E-kitap hakkında bilgi için [ilk bölüme](introduction.md)bakın.

Birçok kişi, uygulamalarının ne zaman kapanacağını bildirmek için müşterilere güvenir. Bu gerçekten her yerde en iyi uygulama değil, özellikle bulut. Hızlı bildirim garantisi yoktur ve size haber verildiğinde, genellikle ne olduğu hakkında en az veya yanıltıcı veri alırsınız. İyi telemetri ve günlük sistemleri ile uygulamanızda neler olup bittiğinin farkında olabilirsiniz ve bir şeyler ters gittiğinde hemen öğrenir ve yardımcı sorun giderme bilgilerine sahip olabilirsiniz.

## <a name="buy-or-rent-a-telemetry-solution"></a>Bir telemetri çözümü satın alın veya kiralayın

> [!NOTE]
> Bu [makale, Application Insights](/azure/application-insights/app-insights-overview) yayımlanmadan önce yazılmıştır. Application Insights, Azure'daki telemetri çözümleri için tercih edilen bir yaklaşımdır. Daha fazla bilgi [için ASP.NET web siteniz için Uygulama Öngörüleri Ayarla'ya](/azure/application-insights/app-insights-asp-net) bakın.

Bulut ortamının en güzel yanlarından biri de zafere giden yolu satın almanın veya kiralamanın gerçekten kolay olmasıdır. Telemetri bir örnektir. Çok fazla çaba sarf etmeden gerçekten iyi bir telemetri sistemi kurup çalışır, çok uygun maliyetli. Azure ile entegre olan bir grup harika iş ortağı vardır ve bazıları nın ücretsiz katmanları vardır , böylece temel telemetriyi boşuna alabilirsiniz. Şu anda Azure'da kullanılabilenlerden yalnızca birkaçı şunlardır:

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) izleme özellikleri de içerir.

Bir telemetri sistemi kullanmanın ne kadar kolay olabileceğini göstermek için Yeni Emanet'i kurmayı çabucak yürüyeceğiz.

Azure yönetim portalında hizmete kaydolun. **Yeni'yi**tıklatın ve ardından **Depola'yı**tıklatın. Eklenti iletişim kutusu **seç** görüntülenir. Aşağı kaydırın ve **Yeni Emanet'e**tıklayın.

![Eklenti Seçin](monitoring-and-telemetry/_static/image1.png)

Sağ ok'u tıklatın ve istediğiniz servis katmanını seçin. Bu demo için ücretsiz katmanı kullanacağız.

![Eklentiyi kişiselleştirin](monitoring-and-telemetry/_static/image2.png)

Sağ ok'u tıklatın, "satın alma"yı onaylayın ve Yeni Emanet şimdi portalda Eklenti olarak gösterilmektedir.

![Satın alma işlemini gözden geçirme](monitoring-and-telemetry/_static/image3.png)

![Yönetim portalında yeni Emanet eklentisi](monitoring-and-telemetry/_static/image4.png)

**Bağlantı Bilgileri'ni**tıklatın ve lisans anahtarını kopyalayın.

![Bağlantı bilgileri](monitoring-and-telemetry/_static/image5.png)

Portaldaki web uygulamanız için **Yapılandır sekmesine** gidin, **Performans İzlemeyi** **Eklenti**olarak ayarlayın ve **Eklenti** açılır listesini **Yeni Emanet**olarak ayarlayın. Daha sonra **Kaydet**'e tıklayın.

![Yapılandırma sekmesinde Yeni Emanet](monitoring-and-telemetry/_static/image6.png)

Visual Studio'da Yeni Emanet NuGet paketini uygulamanızda yükleyin.

![Yapılandırma sekmesinde geliştirici analitiği](monitoring-and-telemetry/_static/image7.png)

Uygulamayı Azure'a dağıtın ve kullanmaya başlayın. Yeni Emanet'in izlemesi için bazı etkinlikler sağlamak için birkaç Fix It görevi oluşturun.

Ardından portalın **Eklentiler** sekmesindeki **Yeni Emanet** sayfasına geri dön ve **Yönet'i**tıklatın. Portal, kimlik bilgilerinizi yeniden girmek zorunda kalmamanız için kimlik doğrulama için tek oturum açma kullanarak sizi Yeni Emanet yönetim portalına gönderir. Genel Bakış sayfası çeşitli performans istatistikleri sunar. (Genel bakış sayfasını tam boyutlu görmek için resmi tıklatın.)

[![Yeni Emanet İzleme sekmesi](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Görebileceğiniz istatistiklerden sadece birkaçı şunlardır:

- Günün farklı saatlerinde ortalama yanıt süresi.

    ![Yanıt süresi](monitoring-and-telemetry/_static/image10.png)
- Günün farklı saatlerinde (dakika başına isteklerde) iş mesuliyet oranları.

    ![Aktarım hızı](monitoring-and-telemetry/_static/image11.png)
- Sunucu CPU zaman farklı HTTP istekleriişleme harcanan.

    ![Web İşlem süreleri](monitoring-and-telemetry/_static/image12.png)
- Uygulama kodunun farklı bölümlerinde harcanan CPU süresi:

    ![İzleme ayrıntıları](monitoring-and-telemetry/_static/image13.png)
- Tarihsel performans istatistikleri.

    ![Tarihsel performans](monitoring-and-telemetry/_static/image14.png)
- Blob hizmeti gibi harici hizmetlere yapılan aramalar ve hizmetin ne kadar güvenilir ve duyarlı olduğu yla ilgili istatistikler.

    ![Dış hizmetler](monitoring-and-telemetry/_static/image15.png)

    ![Dış hizmetler](monitoring-and-telemetry/_static/image16.png)

    ![Dış hizmet](monitoring-and-telemetry/_static/image17.png)
- Dünyanın neresinde veya ABD'de web uygulaması trafiğinin nereden geldiği hakkında bilgi.

    ![Coğrafya](monitoring-and-telemetry/_static/image18.png)

Ayrıca raporlar ve etkinlikler ayarlayabilirsiniz. Örneğin, hataları görmeye başladığınızda, destek personelini soruna karşı uyarmak için bir e-posta gönderebileceğinizi söyleyebilirsiniz.

![Raporlar](monitoring-and-telemetry/_static/image19.png)

Yeni Emanet bir telemetri sisteminin sadece bir örneğidir; tüm bunları diğer servislerden de alabilirsiniz. Bulutun güzelliği, herhangi bir kod yazmak zorunda kalmadan ve en az veya hiç masrafsız, aniden uygulamanızın nasıl kullanıldığı ve müşterilerinizin gerçekte ne yaşadığı hakkında çok daha fazla bilgi alabilirsiniz.

<a id="log"></a>
## <a name="log-for-insight"></a>Kavrayış için günlük

Bir telemetri paketi iyi bir ilk adımdır, ama yine de kendi kod enstrüman var. Telemetri hizmeti size bir sorun olduğunda ve müşterilerin neler yaşadığını söyler, ancak kodunuzda neler olup bittiğini size çok fazla fikir vermeyebilir.

Uygulamanızın ne yaptığını görmek için bir üretim sunucusuna remote yapmak zorunda kalmak istemezsiniz. Bir sunucunuz olduğunda bu pratik olabilir, ancak yüzlerce sunucuya ölçeklediğinizde ve hangilerini uzaktan kumanda etmeniz gerektiğini bilmediğiniz zaman ne olacak? Günlüğe kaydetmeniz, sorunları çözümlemek ve hata ayıklamak için üretim sunucularına uzaktan kumanda etmek zorunda kalmayacağınız yeterli bilgi sağlamalıdır. Sorunları yalnızca günlükler aracılığıyla yalıtabilmeniz için yeterli bilgileri günlüğe kaydetmelisiniz.

### <a name="log-in-production"></a>Üretime giriş yapın

Birçok insan sadece bir sorun olduğunda ve hata ayıklamak istediğinde üretimde izlemeyi açar. Bu, bir sorunun farkında olduğunuz zaman ile bu sorunla ilgili yararlı sorun giderme bilgileri aldığınız zaman arasında önemli bir gecikmeye neden olabilir. Ve aldığınız bilgiler aralıklı hatalar için yararlı olmayabilir.

Depolamanın ucuz olduğu bulut ortamında tavsiye ettiğimiz şey, her zaman üretimde oturum açmayı bırakmanızdır. Bu şekilde hatalar olduğunda, bunları zaten günlüğe kaydetmiş olursunuz ve zaman içinde gelişen veya farklı zamanlarda düzenli olarak meydana gelen sorunları çözümlemenize yardımcı olabilecek geçmiş verilere sahip olursunuz. Eski günlükleri silmek için bir temizleme işlemini otomatikleştirebilirsiniz, ancak böyle bir işlemi ayarlamanın günlükleri tutmaktan daha pahalı olduğunu görebilirsiniz.

Günlük kaydetme nin ek gideri, bir şeyler ters gittiğinde zaten mevcut olan tüm bilgilere sahip olarak tasarruf edebilirsiniz sorun giderme süresi ve para miktarı ile karşılaştırıldığında önemsizdir. Sonra birisi size dün gece 8:00 civarında rastgele bir hata olduğunu söylediğinde, hatayı hatırlamazlarsa sorunun ne olduğunu kolayca öğrenebilirsiniz.

Ayda 4 dolardan daha az bir süre için 50 gigabaytlık günlükleri elinizde tutabilirsiniz ve günlük tutmanın performans etkisi, performans darboğazlarını önlemek için, günlük kitaplığınızın eşzamanlı olduğundan emin olmak için tek bir şeyi aklınızda tutsanız önemsizdir.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>Eylem gerektiren günlüklerden bilgi veren günlükleri ayırt etme

Günlükleri (Bir şey bilmek istiyorum) veya ACT (Ben bir şey yapmak istiyorum) INFORM içindir. Yalnızca bir kişinin veya otomatik bir işlemin harekete geçmesini gerektiren sorunlar için ACT günlükleri yazmaya dikkat edin. Çok fazla ACT günlükleri gerçek sorunları bulmak için tüm üzerinden elemek için çok fazla iş gerektiren, gürültü yaratacaktır. Act günlükleriniz destek personeline e-posta göndermek gibi bazı eylemleri otomatik olarak tetiklerse, bu tür binlerce eylemin tek bir sorun tarafından tetiklenebilmiş olmasını önlemek.

.NET System.Diagnostics izleme, günlükleri Hata, Uyarı, Bilgi ve Hata Ayıklama / Verbose düzeyi atanabilir. ACT günlükleri için Hata düzeyini ayırarak ve INFORM günlükleri için alt düzeyleri kullanarak ACT günlüklerini INFORM günlüklerinden ayırt edebilirsiniz.

![Günlük seviyeleri](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Günlük düzeylerini çalışma zamanında yapılandırma

Her zaman üretimde oturum açmanın değerli olmasına ek olsa da, diğer bir iyi uygulama da, uygulamanızı yeniden dağıtmadan veya yeniden başlatmadan, günlüğe kaydettiğiniz ayrıntı düzeyini çalışma zamanında ayarlamanızı sağlayan bir günlük çerçevesi uygulamaktır. Örneğin izleme tesisini kullandığınızda `System.Diagnostics` Hata, Uyarı, Bilgi ve Hata Ayıklama/Verbose günlükleri oluşturabilirsiniz. Üretimde her zaman Hata, Uyarı ve Bilgi günlüklerini günlüğe kaydetmenizi öneririz ve sorun giderme için hata giderme için debug/Verbose günlüğelerini tek tek dinamik olarak eklemek isteyebilirsiniz.

Azure Uygulama Hizmeti'ndeki Web Apps, `System.Diagnostics` dosya sistemine, Tablo depolamaya veya Blob depolamasına günlük yazmak için yerleşik destek sağlar. Her depolama hedefi için farklı günlük düzeyleri seçebilir ve uygulamanızı yeniden başlatmadan anında günlük düzeyini değiştirebilirsiniz. Blob depolama desteği, [HDInsight'ın](https://docs.microsoft.com/azure/hdinsight/) doğrudan Blob depolama ile nasıl çalışacağını bildiğinden, uygulama günlüklerinizde HDInsight analiz işlerini çalıştırmayı kolaylaştırır.

### <a name="log-exceptions"></a>Özel Durumları Günlüğe Kaydetme

Sadece *istisna koyma. ToString()* günlük kodunuzda. Bu bağlamsal bilgi dışında bırakır. SQL hataları durumunda, SQL hata numarasını dışarıda bırakır. Tüm özel durumlar için, sorun giderme için gereken her şeyi sağladığından emin olmak için bağlam bilgilerini, özel durum kendisini ve iç özel durumları içerir. Örneğin, bağlam bilgileri sunucu adını, bir işlem tanımlayıcısını ve kullanıcı adını (parola yı veya herhangi bir sırlar değil!) içerebilir.

Her geliştiricinin özel durum günlüğe kaydetme yle doğru şeyi yapacağına güveniyorsanız, bazıları bunu yapmaz. Her seferinde doğru şekilde yapıldığından emin olmak için, logger arabiriminize özel durum işleme yi oluşturun: özel durum nesnesini logger sınıfına geçirin ve özel durum verilerini logger sınıfında düzgün bir şekilde günlüğe kaydedin.

### <a name="log-calls-to-services"></a>Hizmetleri günlüğe kaydetme çağrıları

Uygulamanız bir hizmete her çağrıda, ister bir veritabanına, ister REST API'sine veya herhangi bir harici hizmete seslenirse, bir günlük yazmanızı öneririz. Günlüklerinize yalnızca başarı veya başarısızlığın bir göstergesi değil, aynı zamanda her isteğin ne kadar sürdüğünü de ekleyin. Bulut ortamında, kesintileri tamamlamak yerine yavaşlamalarla ilgili sorunlar sık sık görürsünüz. Normalde 10 milisaniye süren bir şey aniden bir saniye almaya başlayabilir. Birisi size uygulamanızın yavaş olduğunu söylediğinde, Yeni Emanet'e veya sahip olduğunuz telemetri hizmetine bakıp deneyimlerini doğrulayabilmek ve sonra da neden yavaş olduğu yla ilgili ayrıntılara dalmak için kendi günlüklerinize bakmak isteyebilirsiniz.

### <a name="use-an-ilogger-interface"></a>ILogger arabirimi kullanma

Bir üretim uygulaması oluştururken yapmanızı tavsiye ettiğimiz şey, basit bir *ILogger* arabirimi oluşturmak ve bazı yöntemleri sokmaktır. Bu, günlüğe kaydetme uygulamasını daha sonra değiştirmenizi ve bunu yapmak için tüm kodunuzu gözden geçirmemenizi kolaylaştırır. Biz Fix It `System.Diagnostics.Trace` uygulaması boyunca sınıf kullanıyor olabilir, ama bunun yerine *iLogger*uygulayan bir günlük sınıfında kapakları altında kullanıyoruz , ve biz uygulama boyunca *ILogger* yöntemi aramaları yapmak.

Bu şekilde, günlüğe kaydetmenizi daha zengin hale [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) getirmek istiyorsanız, istediğiniz günlük mekanizmasını değiştirebilirsiniz. Örneğin, uygulamanız büyüdükçe [NLog](http://nlog-project.org/) veya [Enterprise Library Logging Application Block](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)gibi daha kapsamlı bir günlük paketi kullanmak istediğinize karar verebilirsiniz. ([Log4Net](http://logging.apache.org/log4net/) başka bir popüler günlük çerçevesi ama asynchronous günlük yapmaz.)

NLog gibi bir çerçeve kullanmanın olası nedenlerinden biri, günlük çıktısının ayrı yüksek hacimli ve yüksek değerli veri depolarına bölünmesini kolaylaştırmaktır. Bu, ACT verilerine hızlı erişimi korurken, hızlı sorguları yürütmeniz gerekmeyen büyük hacimli INFORM verilerini verimli bir şekilde depolamanıza yardımcı olur.

### <a name="semantic-logging"></a>Anlamsal Günlük

Daha yararlı tanılama bilgileri üretebilen günlük oluşturmanın nispeten yeni bir yolu [için, Bkz. Kurumsal Kitaplık Anlamsal Günlük Uygulama Bloğu (SLAB).](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/) SLAB, daha yapılandırılmış ve sorgulanabilir günlükler oluşturmanıza olanak sağlamak için .NET 4.5'te [Windows için Olay İzleme](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) ve [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) desteğini kullanır. Günlüğe kaydettiğiniz her olay türü için farklı bir yöntem tanımlarsınız ve bu da yazdığınız bilgileri özelleştirmenize olanak tanır. Örneğin, bir SQL Veritabanı hatasını günlüğe kaydetmek için bir `LogSQLDatabaseError` yöntem çağırabilirsiniz. Bu tür bir özel durum için, önemli bir bilgi parçasının hata numarası olduğunu bilirsiniz, bu nedenle yöntem imzaya bir hata numarası parametresi ekleyebilir ve hata numarasını yazdığınız günlük kaydında ayrı bir alan olarak kaydedebilirsiniz. Sayı ayrı bir alanda olduğundan, hata numarasını bir ileti dizesine dahil ediyorsanız, SQL hata numaralarına dayalı raporları alabileceğinizden daha kolay ve güvenilir bir şekilde alabilirsiniz.

## <a name="logging-in-the-fix-it-app"></a>Fix It uygulamasında oturum açma

### <a name="the-ilogger-interface"></a>ILogger arayüzü

İşte Fix It uygulamasındaki *ILogger* arabirimi.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Bu yöntemler *System.Diagnostics*tarafından desteklenen aynı dört düzeyde günlükleri yazmanızı sağlar. TraceApi yöntemleri, gecikme hakkında bilgi içeren harici servis çağrılarını günlüğe kaydetmeniz içindir. Hata Ayıklama/Verbose düzeyi için bir yöntem kümesi de ekleyebilirsiniz.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger arabiriminin Logger uygulaması

Arayüzün uygulanması gerçekten basittir. Temelde sadece standart *System.Diagnostics* yöntemleri çağırır. Aşağıdaki parçacık, bilgi yöntemlerinin üçünü ve diğerlerinden birini gösterir.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger yöntemlerini arama

Fix It uygulamasındaki her kod bir özel durum yakaladığında, özel durum ayrıntılarını günlüğe kaydetmek için bir *ILogger* yöntemi çağırır. Veritabanına, Blob servisine veya REST API'ye her arama yaptığında, aramadan önce kronometreyi başlatır, hizmet döndüğünde kronometreyi durdurur ve geçen süreyi başarı veya başarısızlık la birlikte kaydeder.

Günlük iletisinin sınıf adını ve yöntem adını içerdiğine dikkat edin. Günlük iletilerinin uygulama kodunun hangi bölümünün bunları yazdığını belirlediğinden emin olmak iyi bir uygulamadır.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Şimdi Fix It uygulaması SQL Veritabanı'nı her aradığında, aramayı, onu çağıran yöntemi ve tam olarak ne kadar zaman aldığını görebilirsiniz.

![Günlüklerde SQL Veritabanı sorgusu](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Günlüklerde gezinmeye giderseniz, veritabanı aramalarının zaman larının değişken olduğunu görebilirsiniz. Bu bilgiler yararlı olabilir: uygulama tüm bunları kaydettiği için veritabanı hizmetinin zaman içinde nasıl performans gösterdiğine dair geçmiş eğilimleri analiz edebilirsiniz. Örneğin, bir hizmet çoğu zaman hızlı olabilir, ancak istekler başarısız olabilir veya yanıtlar günün belirli saatlerinde yavaşlayabilir.

Blob hizmeti için de aynı şeyi yapabilirsiniz – uygulama yeni bir dosya yüklediği her seferde bir günlük vardır ve her dosyayı yüklemenin tam olarak ne kadar sürdüğünü görebilirsiniz.

![Blob yükleme günlüğü](monitoring-and-telemetry/_static/image23.png)

Bir hizmeti her aradığınızda yazmak için fazladan birkaç kod satırı, ve şimdi birisi bir sorunla karşılaştığını söylediğinde, sorunun tam olarak ne olduğunu, bir hata olup olmadığını, ya da sadece yavaş çalışıp çalışmadığını biliyorsunuz. Sorunun kaynağını bir sunucuya uzaktan kumanda etmek zorunda kalmadan saptayabiliyor veya hata olduktan sonra günlüğe kaydetmeyi açabilir ve yeniden oluşturmayı umabilirsiniz.

## <a name="dependency-injection-in-the-fix-it-app"></a>Fix It uygulamasında Bağımlılık Enjeksiyonu

Yukarıdaki örnekte depo oluşturucu sundurma arabirimi uygulamasını nasıl alır merak edebilirsiniz:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Uygulama nın arayüzü ne kadar kabloyla bağdaştırmak için [autofac](http://autofac.org/)ile [bağımlılık enjeksiyonu](http://en.wikipedia.org/wiki/Dependency_injection)(DI) kullanır. DI, kodunuz boyunca birçok yerde arabirara dayalı bir nesneyi kullanmanıza olanak tanır ve arabirim anında kullanıldığında kullanılan uygulamayı tek bir yerde belirtmeniz gerekir. Bu, uygulamayı değiştirmeyi kolaylaştırır: örneğin, System.Diagnostics logger'ını bir NLog logger ile değiştirmek isteyebilirsiniz. Veya otomatik test için logger sahte bir sürümünü değiştirmek isteyebilirsiniz.

Fix It uygulaması tüm depolarda ve tüm denetleyicilerde DI kullanır. Denetleyici sınıflarının oluşturucuları, deponun logger arabirimini aldığı gibi *bir ITaskRepository* arabirimine sahiptir:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

Uygulama otomatik olarak bu oluşturucular için *TaskRepository* ve *Logger* örnekleri sağlamak için AutoFac DI kitaplığını kullanır.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Bu kod temelde her yerde bir yapıcı bir *ILogger* arayüzü ihtiyacı olduğunu söylüyor, *Logger* sınıfının bir örnek geçmek, ve bir *IFixItTaskRepository* arayüzü gerektiğinde, *FixItTaskRepository* sınıf bir örnek geçmek.

[AutoFac](http://autofac.org/) kullanabileceğiniz birçok bağımlılık enjeksiyon çerçeveleri biridir. Başka bir popüler bir [Birlik](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), hangi tavsiye edilir ve Microsoft Patterns ve Uygulamalar tarafından desteklenir.

## <a name="built-in-logging-support-in-azure"></a>Azure'da yerleşik günlük desteği

Azure, [Azure Uygulama Hizmeti'nde Web Uygulamaları için](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)aşağıdaki türde günlük leri destekler:

- System.Diagnostics izleme (siteyi yeniden başlatmadan açıp kapatabilir ve seviyeleri anında ayarlayabilirsiniz).
- Windows Olayları.
- IIS Günlükleri (HTTP/FREB).

Azure, Bulut Hizmetlerinde aşağıdaki [türde günlük leri](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)destekler:

- System.Diagnostics izleme.
- Performans sayaçları.
- Windows Olayları.
- IIS Günlükleri (HTTP/FREB).
- Özel dizin izleme.

Fix It uygulaması System.Diagnostics izleme kullanır. System.Diagnostics'in bir web uygulamasında oturum açmasını etkinleştirmek için tek yapmanız gereken portaldaki bir anahtarı çevirmek veya REST API'yi aramaktır. Portalda, sitenizin **Yapılandırma** sekmesini tıklatın ve Uygulama **Tanılama** bölümünü görmek için aşağı kaydırın. Günlüğe kaydetmeyi açabilir veya kapatabilir ve istediğiniz günlük düzeyini seçebilirsiniz. Azure'a günlükleri dosya sistemine veya bir depolama hesabına yazmasını sağlayabilirsiniz.

![Yapılandırma sekmesinde uygulama tanılama ve site tanılama](monitoring-and-telemetry/_static/image24.png)

Azure'da günlüğe kaydetmeyi etkinleştirdikten sonra, günlükleri oluşturulan Visual Studio Çıktı penceresinde görebilirsiniz.

![Akış günlükleri menüsü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Akış günlükleri menüsü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Ayrıca günlükleri depolama hesabınıza yazılı olabilir ve Bunları Visual Studio'daki **Sunucu Gezgini** veya [Azure Depolama Gezgini](https://azure.microsoft.com/features/storage-explorer/)gibi Azure Depolama Masası hizmetine erişebilecek herhangi bir araçla görüntüleyebilirsiniz.

![Sunucu Gezgini'nde oturum açma](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Özet

Kutudan çıkmış bir telemetri sistemi uygulamak, kendi kodunuzda enstrüman günlüğü uygulamak ve Azure'da günlük işlemlerini yapılandırmak gerçekten çok kolaydır. Ve üretim sorunları varsa, bir telemetri sistemi ve özel günlükleri kombinasyonu müşterileriniz için önemli sorunlar haline gelmeden önce hızlı bir şekilde sorunları çözmek yardımcı olacaktır.

Bir [sonraki bölümde](transient-fault-handling.md) geçici hataların nasıl işleyeceğiniince, araştırmanız gereken üretim sorunları haline gelmezler.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın.

Dokümantasyon ağırlıklı olarak telemetri ile ilgili:

- [Microsoft Desenleri ve Uygulamaları - Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. Enstrümantasyon ve Telemetri kılavuzu, Hizmet Ölçümleme kılavuzu, Sistem Sonu İzleme deseni ve Çalışma Zamanı Yeniden Yapılandırma deseni.
- [Bulutta Penny Pinching: Azure Web Sitelerinde Yeni Emanet Performans İzlemesini Etkinleştirme.](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)
- [Azure Bulut Hizmetlerinde Büyük Ölçekli Hizmetlerin Tasarımı için En İyi Uygulamalar.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) Mark Simms ve Michael Thomassy tarafından beyaz kağıt. Telemetri ve Tanılama bölümüne bakın.
- [Uygulama Öngörüleri ile Yeni Nesil Geliştirme](https://msdn.microsoft.com/magazine/dn683794.aspx). MSDN Dergisi makalesi.

Özellikle günlük le ilgili belgeler:

- [Anlamsal Günlük Uygulama Bloğu (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neil Mackenzie SLAB ile anlamsal günlük için durumda sunar.
- [Anlamsal Günlük ile Yapılandırılmış ve Anlamlı Günlükler Oluşturma](https://channel9.msdn.com/Events/Build/2013/3-336). (Video) Julian Dominguez SLAB ile anlamsal günlük için durumda sunar.
- [EF6 SQL Günlük – Bölüm 1: Basit Günlük .](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/) Arthur Vickers, Varlık Çerçevesi tarafından yürütülen sorguları EF 6'da nasıl günlüğe kaydedin gösterir.
- [ASP.NET Bir MVC Uygulamasında Taraf Çerçevesi ile Bağlantı Esnekliği ve Komut Durdurma](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Dokuz bölümlük bir öğretici serisinin dördüncüsü, Entity Framework tarafından veritabanına gönderilen SQL komutlarını günlüğe kaydetmek için EF 6 komut durdurma özelliğinin nasıl kullanılacağını gösterir.
- [C# 5.0 Arayan Bilgi Özniteliklerini kullanarak Günlüğe Kaydetmeyi Geliştirin.](http://www.dotnetcurry.com/showarticle.aspx?ID=972) Nasıl kolayca okuma içine zor kodlama veya el ile almak için yansıma kullanmadan arama yönteminin adını günlüğe kaydetmeye.

Özellikle sorun giderme ile ilgili dokümantasyon:

- [Azure Sorun &amp; Giderme Hata Ayıklama blogu](https://blogs.msdn.com/b/kwill/).
- [AzureTools – Azure Geliştirici Destek Ekibi tarafından kullanılan Tanılama Yardımcı Programı.](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true) Çok çeşitli tanılama ve izleme araçlarını indirmek ve çalıştırmak için Azure VM'de kullanılabilecek bir araç için indirme bağlantısı sunar ve sağlar. Belirli bir VM'de bir sorunu tanılamanız gerektiğinde yararlıdır.
- [Visual Studio'yu kullanarak Azure Uygulama Hizmeti'ndeki bir web uygulamasının sorun giderme](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)sorunu. System.Diagnostics izleme ve uzaktan hata ayıklama ile başlamak için adım adım öğretici.

Videolar:

- [FailSafe: Ölçeklenebilir, Esnek Bulut Hizmetleri Oluşturma.](https://channel9.msdn.com/Series/FailSafe) Ulrich Homann, Marc Mercuri ve Mark Simms tarafından dokuz bölümlük dizi. Microsoft Müşteri Danışma Ekibi'nin (CAT) gerçek müşterilerle olan deneyiminden alınan hikayelerle, üst düzey kavramları ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Bölüm 4 ve 9 izleme ve telemetri hakkında. Bölüm 9 izleme hizmetleri MetricsHub, AppDynamics, New Relic ve PagerDuty genel bir bakış içerir.
- [Building Big: Azure müşterilerinden alınan dersler - Bölüm II](https://channel9.msdn.com/Events/Build/2012/3-030). Mark Simms başarısızlık için tasarım ve her şeyi enstrümanting hakkında konuşuyor. Failsafe serisine benzer ancak daha fazla nasıl yapIlebilen ayrıntılara girer.

Kod örneği:

- [Azure'da Bulut Hizmeti Temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Microsoft Azure Müşteri Danışma Ekibi tarafından oluşturulan örnek uygulama. Aşağıdaki makalelerde açıklandığı gibi hem telemetri hem de günlük uygulamalarını gösterir. Örnek [NLog](http://nlog-project.org/)kullanarak uygulama günlüğe kaydetme uygular. İlgili belgeler için, [telemetri ve günlük hakkında dört TechNet wiki makalelerin serisine](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)bakın.

> [!div class="step-by-step"]
> [Önceki](design-to-survive-failures.md)
> [Sonraki](transient-fault-handling.md)
