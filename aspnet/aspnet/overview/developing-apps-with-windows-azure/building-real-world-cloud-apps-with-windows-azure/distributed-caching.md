---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Dağıtılmış Önbelleğe Alma (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma) | Microsoft Dokümanlar
author: MikeWasson
description: Azure e-kitaplı Building Real World Cloud Apps, Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bu 13 desen ve uygulamaları açıklar ki o olabilir ...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676022"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Dağıtılmış Önbelleğe Alma (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)

Mike [Wasson](https://github.com/MikeWasson)tarafından , [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya Download [E-kitap indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-kitaplı **Building Real World Cloud Apps,** Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bulut için web uygulamalarını geliştirmekte başarılı olmanıza yardımcı olabilecek 13 model ve uygulamayı açıklar. E-kitap hakkında bilgi için [ilk bölüme](introduction.md)bakın.

Önceki bölümde geçici hata işleme baktı ve bir devre kesici stratejisi olarak önbelleğe bahsedilen. Bu bölümde, önbelleğe alma hakkında ne zaman kullanılacağı, kullanımı için ortak desenler ve Azure'da nasıl uygulanacağı gibi daha fazla arka plan sağlar.

## <a name="what-is-distributed-caching"></a>Dağıtılmış önbelleğe alma nedir

Önbellek, verileri bellekte depolayarak yaygın olarak erişilen uygulama verilerine yüksek iş ortalığı, düşük gecikme süresi erişimi sağlar. Bir bulut uygulaması için en yararlı önbellek türü, verilerin tek tek web sunucusunun belleğinde değil, diğer bulut kaynaklarında depolandığı ve önbelleğe alınan verilerin bir uygulamanın tüm web sunucuları (veya uygulama tarafından kullanılan diğer bulut Sanal M'leri) için kullanılabilir hale getirildiği anlamına gelir.

![aynı önbellek sunucuları erişen birden çok web sunucusugösteren diyagram](distributed-caching/_static/image1.png)

Uygulama sunucu ekleyerek veya kaldırarak ölçeklendiğinde veya yükseltmeler veya hatalar nedeniyle sunucular değiştirildiğinde, önbelleğe alınan veriler uygulamayı çalıştıran her sunucu için erişilebilir kalır.

Kalıcı bir veri deposunun yüksek gecikmeli veri erişiminden kaçınarak, önbelleğe alma uygulama yanıt verme yeteneğini önemli ölçüde artırabilir. Örneğin, önbellekten veri alma, ilişkisel bir veritabanından almaktan çok daha hızlıdır.

Önbelleğe almanın bir yan yararı, kalıcı veri deposuna olan trafiği azaltır ve bu da kalıcı veri deposu için veri çıkış ücretleri olduğunda daha düşük maliyetlere neden olabilir.

## <a name="when-to-use-distributed-caching"></a>Dağıtılmış önbelleğe alma ne zaman kullanılır

Önbelleğe alma, veri yazmaktan daha fazla okuma yapan uygulama iş yükleri için en iyi sonucu kullanır ve veri modeli önbellekte verileri depolamak ve almak için kullandığınız anahtar/değer organizasyonunu desteklediğinde. Ayrıca, uygulama kullanıcıları çok sayıda ortak veriyi paylaştığında daha kullanışlıdır; örneğin, her kullanıcı genellikle bu kullanıcıya özgü verileri alıyorsa önbellek bu kadar çok avantaj sağlamaz. Önbelleğe almanın çok yararlı olabileceği bir örnek, veriler sık sık değişmediği ve tüm müşteriler aynı verilere baktığından, bir ürün kataloğudur.

Kalıcı veri deposunun iş sonu limitleri ve gecikme gecikmeleri genel uygulama performansında daha fazla bir sınır haline geldikçe, önbelleğe almanın yararı, uygulama ölçeklendikçe giderek daha ölçülebilir hale gelir. Ancak, önbelleğe alma performansının yanı sıra başka nedenlerle de uygulayabilirsiniz. Kullanıcıya gösterildiğinde mükemmel bir şekilde güncel olması gerekmeyen veriler için, önbellek erişimi kalıcı veri deposunun yanıt vermediğinde veya kullanılamadığı nda devre kesici görevi görebilir.

## <a name="popular-cache-population-strategies"></a>Popüler önbellek popülasyon stratejileri

Önbellekten veri alabilmek için önce verileri orada depolamanız gerekir. Önbelleğe ihtiyacınız olan verileri elde etmek için çeşitli stratejiler vardır:

- İsteğe Bağlı / Önbellek Kenara

    Uygulama önbellekten veri almaya çalışır ve önbellekte veri ("miss") olmadığında, uygulama verileri önbellekte saklar ve böylece bir sonraki sefere kullanılabilir olur. Uygulama aynı verileri almaya çalıştığında, önbellekte ("isabet") aradığını bulur. Veritabanında değiştirilen önbelleğe alınmış verileri almak için, veri deposunda değişiklik yaparken önbelleği geçersiz kılınırsınız.
- Arka Plan Veri Push

    Arka plan hizmetleri verileri düzenli bir zamanlamayla önbelleğe iter ve uygulama her zaman önbellekten çekilir. Bu yaklaşım, her zaman en son verileri döndürmenizi gerektirmeyen yüksek gecikme li veri kaynaklarında harika çalışır.
- Devre Kesici

    Uygulama normalde kalıcı veri deposuyla doğrudan iletişim kurar, ancak kalıcı veri deposunda kullanılabilirlik sorunları olduğunda, uygulama önbellekten veri alır. Veriler önbellek bir yana veya arka plan veri itme stratejisi kullanılarak önbelleğe alınmış olabilir. Bu, performans arttırıcı bir stratejiden çok bir hata işleme stratejisidir.

Önbellekteki verileri güncel tutmak için, uygulamanız veri oluşturduğunda, güncellediğinde veya sildiğinde ilgili önbellek girişlerini silebilirsiniz. Uygulamanızın bazen biraz güncel olmayan verileri alması uygunsa, önbellek verilerinin ne kadar eski olabileceğine ilişkin bir sınır belirlemek için yapılandırılabilir bir son kullanma süresine güvenebilirsiniz.

Mutlak son kullanma tarihini (önbellek öğesinin oluşturulmasından bu yana geçen süre) veya kayan son kullanma süresini (önbellek öğesine en son erişilen zamandan bu yana geçen süre) yapılandırabilirsiniz. Verilerin çok bayat olmasını önlemek için önbellek son kullanma mekanizmasına bağlı olduğunuzda mutlak son kullanma süresi kullanılır. Fix It uygulamasında, eski önbellek öğelerini el ile boşaltırız ve en güncel verileri önbellekte tutmak için kaydırma son kullanma süresi kullanırız. Seçtiğiniz son kullanma ilkesinden bağımsız olarak, önbelleğin bellek sınırına ulaşıldığında önbellek en eski (En Son Kullanılan veya LRU) öğeleri otomatik olarak boşaltır.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Fix It uygulaması için örnek önbellek kenara kodu

Aşağıdaki örnek kodda, düzeltme görevini alırken önce önbelleği kontrol ediyoruz. Görev önbellekte bulunursa, iade ediyoruz; bulunamazsa, veritabanından alıp önbellekte saklarız. `FindTaskByIdAsync` Yönteme önbelleğe almak için yapacağınız değişiklikler vurgulanır.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Bir Fix It görevini güncellediğinizde veya sildiğinizde, önbelleğe alınmış görevi geçersiz kılmanız (kaldırmanız) gerekir. Aksi takdirde, bu görevi okumaya yönelik gelecekteki denemeler önbellekten eski verileri almaya devam edecektir.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Bunlar basit önbelleğe alma kodunu göstermek için örneklerdir; önbelleğe alma, indirilebilir Düzeltme It projesinde uygulanmamıştır.

## <a name="azure-caching-services"></a>Azure önbelleğe alma hizmetleri

Azure aşağıdaki önbelleğe alma hizmetlerini sunar: [Azure Redis Önbelleği](https://msdn.microsoft.com/library/dn690523.aspx) ve [Azure Yönetilen Önbellek.](https://msdn.microsoft.com/library/dn386094.aspx) Azure Redis önbelleği popüler [açık kaynak Redis Önbelleğini](http://redis.io/) temel alıntır ve önbelleğe alma senaryolarının çoğu için ilk tercihtir.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>önbellek sağlayıcısı nı kullanarak oturum durumunu ASP.NET

[Web geliştirme en iyi uygulamalar bölümünde](web-development-best-practices.md)belirtildiği gibi, en iyi uygulama oturum durumu kullanmaktan kaçınmaktır. Uygulamanız oturum durumu gerektiriyorsa, bir sonraki en iyi yöntem varsayılan bellek sağlayıcıdan kaçınmaktır, çünkü bu ölçeklendirmeyi etkinleştirmez (web sunucusunun birden çok örneği). ASP.NET SQL Server oturum durumu sağlayıcısı, birden çok web sunucusunda çalışan bir sitenin oturum durumunu kullanmasına olanak tanır, ancak bellek içi sağlayıcıyla karşılaştırıldığında yüksek bir gecikme maliyetine neden olur. Oturum durumunu kullanmanız gerekiyorsa en iyi çözüm, [Azure Önbelleği için Oturum Durumu Sağlayıcısı](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)gibi bir önbellek sağlayıcısı kullanmaktır.

## <a name="summary"></a>Özet

Yanıt süresini ve ölçeklenebilirliği artırmak ve veritabanı kullanılamadığında uygulamanın okuma işlemleri için yanıt vermeye devam etmesini sağlamak için Fix It uygulamasının önbelleğe alma uygulamasını nasıl uygulayabileceğini gördünüz. Bir [sonraki bölümde](queue-centric-work-pattern.md) ölçeklenebilirliği nasıl daha da geliştirebileceğimizi ve uygulamanın yazma işlemleri için yanıt vermeye devam etmesini nasıl sağlayacağız.

## <a name="resources"></a>Kaynaklar

Önbelleğe alma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

Belgeler

- [Azure Önbelleği](https://msdn.microsoft.com/library/gg278356.aspx). Azure'da önbelleğe alma yla ilgili resmi MSDN belgeleri.
- [Microsoft Desenleri ve Uygulamaları - Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. Önbelleğe Alma kılavuzu ve Önbellek-Kenara desen.
- [Failsafe: Esnek Bulut Mimarileri için Kılavuz.](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx) Marc Mercuri, Ulrich Homann ve Andrew Townhill tarafından beyaz kağıt. Caching'deki bölüme bak.
- [Azure Bulut Hizmetlerinde Büyük Ölçekli Hizmetlerin Tasarımı için En İyi Uygulamalar.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) W. Mark Simms ve Michael Thomassy tarafından beyaz kağıt. Dağıtılmış önbelleğe alma bölümüne bakın.
- [Ölçeklenebilirlik Yolunda Dağıtılmış Önbelleğe](https://msdn.microsoft.com/magazine/dd942840.aspx)Alma . Eski bir (2009) MSDN Dergisi makalesi, ancak genel olarak dağıtılmış önbelleğe alma için açıkça yazılmış bir giriş; FailSafe ve En İyi Uygulamalar teknik incelemelerin önbelleğe alma bölümlerinden daha fazla derinliğe gider.

Videolar

- [FailSafe: Ölçeklenebilir, Esnek Bulut Hizmetleri Oluşturma.](https://channel9.msdn.com/Series/FailSafe) Ulrich Homann, Marc Mercuri ve Mark Simms tarafından dokuz bölümlük dizi. Bulut uygulamalarının nasıl tasarlanabildiğini gösteren 400 düzeyli bir görünüm sunar. Bu dizi teori ve nedenleri üzerinde duruluyor; daha fazla nasıl-nasıl ayrıntılar için, Mark Simms tarafından Building Big serisi bakın. 1:24:14'ten başlayan 3.
- [Building Big: Azure müşterilerinden alınan dersler - Bölüm I](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davies 46:00'dan itibaren dağıtılmış önbelleğe alımını tartışıyor. Failsafe serisine benzer ancak daha fazla nasıl yapIlebilen ayrıntılara girer. Sunum 31 Ekim 2012'de sunulduğundan, 2013 yılında tanıtılan Azure Uygulama Hizmeti'ndeki Web Apps önbelleğe alma hizmetini kapsamaz.

Kod örneği

- [Azure'da Bulut Hizmeti Temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Dağıtılmış önbelleğe alma uygulayan örnek uygulama. Aşağıdaki blog gönderisine bakın [Bulut Hizmeti Temelleri – Önbelleğe Alma Temelleri](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Önceki](transient-fault-handling.md)
> [Sonraki](queue-centric-work-pattern.md)
