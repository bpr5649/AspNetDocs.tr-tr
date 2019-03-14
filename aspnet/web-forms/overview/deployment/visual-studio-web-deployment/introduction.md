---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'Visual Studio kullanarak ASP.NET Web Dağıtımı: Giriş | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisinin nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısı, uygulama tarafından web V kullanarak...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: a227f6564607ed9e909fc4d6297d7370f8fb62b5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075960"
---
<a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio kullanarak ASP.NET Web Dağıtımı: Giriş
====================
tarafından [Tom Dykstra](https://github.com/tdykstra)

[Başlangıç projesini indirin](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisinin nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) web göre uygulamayı Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısı, .NET için Azure SDK'sı ile Visual Studio 2012 kullanarak. Visual Studio 2013 için yordamlar çoğu benzerdir.
> 
> Internet üzerinden kişiler kullanılabilir hale getirmek için bir web uygulaması geliştirme. Ancak, sağ, geliştirme bilgisayarınızda çalışan bir şey nasıl gösterileceğini sonra web programlama öğreticiler genellikle durdurun. Bu öğretici serisinde, diğerleri nereden bırakın başlar: bir web uygulaması yerleşik, test ve kullanıma hazır. Sırada ne var? Bu öğreticiler nasıl test etmek için yerel geliştirme bilgisayarınızda IIS ve Azure'a veya bir üçüncü taraf barındırma sağlayıcısı hazırlama ve üretim için ilk dağıtılacağı gösterir. Entity Framework, SQL Server ve ASP.NET üyelik sistemini kullanan bir web uygulaması projesi dağıtacağınıza örnek uygulamanın var. ASP.NET Web Forms örnek uygulama kullanır, ancak gösterilen yordamları ASP.NET MVC ve Web API için de geçerlidir.
> 
> Bu öğreticiler Visual Studio'da ASP.NET ile nasıl çalışılacağını bildiğiniz varsayılır. Aksi takdirde, başlatmak için iyi bir yerdir bir [temel ASP.NET Web Forms Öğreticisi](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) veya [temel ASP.NET MVC Öğreticisi](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).
> 
> Öğretici için doğrudan ilgili olmayan sorularınız varsa, bunları gönderebilir [ASP.NET dağıtımı Forumu](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) veya [StackOverflow](http://stackoverflow.com).
> 
> Bu içerik ücretsiz bir e-kitap olarak da kullanılabilir [TechNet E-kitap Galerisi](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio).


## <a name="overview"></a>Genel Bakış

Bu öğreticileri aracılığıyla SQL Server veritabanlarını içeren bir ASP.NET web uygulaması Dağıtma Kılavuzu. Öncelikle, test etmek için yerel geliştirme bilgisayarınızda IIS ve Web uygulamalarında Azure App Service ve hazırlama ve üretim için Azure SQL veritabanı dağıtacaksınız. Tek tıklamayla yayımlama Visual Studio kullanarak dağıtma konusunu ele alacağız ve komut satırı kullanarak dağıtma konusunu ele alacağız.

Öğreticiler sayısı göz korkutucu görünen dağıtım işlemi yapabilirsiniz. Aslında, temel yordamlar basittir. Ancak, gerçek durumlarda, genellikle ek dağıtım görevlerini gerçekleştirmeniz gereken — Örneğin, hedef sunucuda klasör izinlerini ayarlama. Biz bu ek görevleri öğreticileri gerçek bir uygulamada başarıyla dağıtması engel olabilecek bilgi bırakmayın umuduyla bazı gösterilen.

Öğreticiler sırayla çalışmak üzere tasarlanmış ve önceki bölümün her bölümü oluşturur. Kendi durumunuza uygun olmayan bölümleri atlayabilirsiniz, ancak ardından sonraki öğreticilerde yordamları ayarlamanız gerekebilir.

## <a name="intended-audience"></a>Hedef kitle

Öğreticiler ortamlarda çalışan ASP.NET geliştiricilerine yönelik burada:

- Üretim ortamı, Azure App Service Web Apps ya da üçüncü taraf barındırma sağlayıcısına alır.
- Dağıtım için bir sürekli tümleştirme işlem sınırlı değildir ve doğrudan Visual Studio'dan yapılabilir.

Dağıtımdan [kaynak denetimi](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) kullanarak bir [sürekli teslim](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) işlemi komut satırından dağıtmak nasıl oluşturulduğunu gösteren bir öğretici dışında bu öğreticilerdeki dahil değildir. Sürekli teslim hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Sürekli tümleştirme ve sürekli teslim (Windows Azure'la gerçek hayatta kullanılan bulut uygulamaları oluşturma)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure App Service'te bir web uygulaması dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [Kurumsal senaryolarda Web uygulamaları dağıtma](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (bir eski kümesi yine de Kurumsal ortamlar için kullanışlı bilgilere sahip Visual Studio 2010 için yazılan öğreticiler.)

## <a name="using-a-third-party-hosting-provider"></a>Bir üçüncü taraf barındırma sağlayıcısı'nı kullanma

Öğreticilerini bir Azure hesabının ayarlanması ve hazırlama ve üretim için Azure App Service'te Web uygulamaları için uygulama dağıtma işlemi kullanın. Ancak, seçtiğiniz üçüncü taraf barındırma sağlayıcısını dağıtmak için aynı temel yordamları kullanabilirsiniz. Öğreticiler işlemleri benzersiz Azure'a gidin. burada biçimde açıklayan ve bir üçüncü taraf barındırma sağlayıcısında beklediğiniz hangi farklar öneri.

## <a name="deploying-web-app-projects"></a>Web Uygulama projeleri dağıtma

Karşıdan yüklemek ve dağıtmak için bu öğreticileri örnek uygulamanın bir Visual Studio web uygulama projesidir. Ancak, en son yüklerseniz [için Visual Studio Web yayımlama güncelleştirmesi](https://msdn.microsoft.com/tr-tr/library/jj161045.aspx), web uygulama projeleri için araçları ve aynı dağıtım yöntemlerini kullanabilirsiniz.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC projeleri dağıtma

Örnek uygulama, bir ASP.NET Web formları projesi olmakla birlikte her şeyi yapma hakkında bilgi de ASP.NET MVC için geçerlidir. Visual Studio MVC proje web uygulaması projesi başka bir biçimidir. ASP.NET MVC ya da, hedef sürümünü desteklemeyen bir barındırma sağlayıcısına dağıtıyorsanız, uygun yüklediğinizden emin olmanız gerekir, tek fark, ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0), [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0) veya [MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) NuGet paketini projenize.

## <a name="programming-language"></a>Programlama dili

Örnek uygulama C# kullanır ancak öğreticileri C# bilgisi gerektirmez ve Eğitmenler tarafından gösterilen dağıtım teknikleri dile özgü değildir.

## <a name="database-deployment-methods"></a>Veritabanı dağıtım yöntemleri

Visual Studio web dağıtımı ile birlikte bir SQL Server veritabanı dağıtma üç yolu vardır:

- Entity Framework Code First geçişleri
- DbDacFx Web dağıtımı sağlayıcısı
- Web dağıtımı dbFullSql sağlayıcısı

Bu öğreticide ilk iki bu yöntemlerden birini kullanın. Web dağıtımı dbFullSql sağlayıcı bundan böyle SQL Server Compact'dan SQL Server'a geçirmeyi gibi bazı belirli senaryolar dışında önerilir eski bir yöntemdir.

Bu öğreticide gösterilen yöntemleri için SQL Server veritabanları, olmayan SQL Server Compact değildir. SQL Server Compact veritabanı dağıtma hakkında daha fazla bilgi için bkz: [Visual Studio Web dağıtımı ile SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md).

Bu öğreticide gösterilen yöntemleri, Web dağıtımı kullanmanızı gerektiren yayımlama yöntemi. Yöntemi, FTP, dosya sistemi veya FPSE, gibi farklı bir yayımlama tercih ediyorsanız bkz [web uygulama dağıtım veritabanından ayrı olarak dağıtma](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) Visual Studio ve ASP.NET için Web dağıtımı içerik haritası'nda.

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First geçişleri

Entity Framework sürümü 4.3, Microsoft Code First Migrations kullanıma sunmuştur. Code First geçişleri bir veri modeline artımlı değişiklikler ve bu değişiklikleri veritabanına yayma işlemini otomatikleştirir. ' Code First'ün önceki sürümlerinde, genellikle bırakın ve veritabanı veri modeli değiştirdiğiniz her durumda yeniden oluşturma içindeki varlık çerçevesi sağlar. Bu sorunun geliştirme, test verileri kolayca yeniden oluşturulur, ancak üretim ortamında genellikle veritabanı şemasına veritabanı bırakmadan güncelleştirmek istediğiniz değildir. Bırakma ve yeniden oluşturulmadan veritabanını güncellemek Code First geçişleri özelliği sağlar. Code First gerekli şema değişiklikleri yapma otomatik olarak karar verebilirsiniz ve değişiklikleri özelleştirir kod yazabilirsiniz. Code First Migrations giriş için bkz: [Code First Migrations](https://msdn.microsoft.com/library/hh770484.aspx).

Bir web projesini dağıtırken, Visual Studio Code First Migrations tarafından yönetilen bir veritabanı dağıtma işlemini otomatik hale getirebilirsiniz. Yayımlama profili oluşturduğunuzda, yürütme Code First Migrations (uygulama başlatılırken çalışır) etiketli onay kutusunu seçin. Bu ayar, uygulamanın Web.config dosyasını hedef sunucuya Code First kullanmasını sağlayacak şekilde otomatik olarak yapılandırmak dağıtım işlemine neden olur `MigrateDatabaseToLatestVersion` Başlatıcı sınıfı.

Visual Studio dağıtım işlemi sırasında veritabanı ile herhangi bir şey yapmaz. Dağıtılan uygulamayı ilk kez dağıtımdan sonra veritabanına eriştiğinde, Code First otomatik olarak veritabanı oluşturur veya veritabanı şeması en son sürüme güncelleştirir. Uygulamaya geçişlerini Seed yöntemi uygularsa, yöntem veritabanı oluşturulur veya şema güncelleştirildikten sonra çalışır.

Bu öğreticide, uygulama veritabanını dağıtmak için Code First Migrations'ı kullanacaksınız.

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web dağıtımı sağlayıcısı

Entity Framework Code First tarafından yönetilmediği durumlarda bir SQL Server veritabanı için yayımlama profili yapılandırdığınızda, veritabanını güncelleştir etiketli onay kutusunu seçebilirsiniz. İlk dağıtım sırasında dbDacFx sağlayıcısı hedef veritabanını kaynak veritabanıyla eşleşmesi için tabloları ve diğer veritabanı nesnelerini oluşturur. Sonraki dağıtımlarda sağlayıcısı nedir kaynak ve hedef veritabanları arasında belirler ve kaynak veritabanıyla eşleşmesi için hedef veritabanı şemasını güncelleştirir. Varsayılan olarak, sağlayıcı bir tabloyu veya sütunu kesildiğinde gibi veri kaybına neden herhangi bir değişiklik yapmaz.

Bu yöntem veritabanı tablolarındaki veriler dağıtımını otomatik hale değil, ancak bunları dağıtım sırasında çalıştırmak için Visual Studio'yu yapılandırma ve bunun için komut dosyaları oluşturabilirsiniz. Dağıtım sırasında komut dosyalarını çalıştırmak için başka bir nedeni, veri kaybına neden olacağından, otomatik olarak yapılan şema değişiklikleri olmasını sağlamaktır.

Bu öğreticide, ASP.NET üyelik veritabanını dağıtmak için dbDacFx Sağlayıcısı'nı kullanacaksınız.

## <a name="troubleshooting-during-this-tutorial"></a>Bu öğretici sırasında sorun giderme

Dağıtım sırasında bir hata meydana geldiğinde veya dağıtılan sitenin düzgün çalışmıyorsa, hata iletileri her zaman açık bir çözüm sunmaz. Bazı yaygın sorun senaryoları ile yardımcı olacak bir [sorun giderme başvuru sayfası](troubleshooting.md) kullanılabilir. Şu öğreticileri gibi bir sorun oluşması veya bir hata iletisi alırsanız, sorun giderme sayfasını kontrol etmeyi unutmayın.

## <a name="comments-welcome"></a>Açıklamalar Hoş Geldiniz

Öğreticileri hakkında yorum davetlidir ve hesap düzeltmeleri veya öğretici açıklamalarda sağlanan geliştirmeleri için öneriler almak için öğreticiyi güncelleştirildiğinde her türlü çabayı yapılacaktır.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Önkoşullar

Bu öğreticide, aşağıdaki ürünler için yazılmıştır:

- Windows 8 veya Windows 7.
- Visual Studio 2012 veya Visual Studio 2012 Express ile Web için [en son güncelleştirmeyi](https://go.microsoft.com/fwlink/?LinkId=272486).
- [Visual Studio 2012 için Azure SDK](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio 2010 SP1 veya Visual Studio 2013 kullanarak öğreticiyi izleyebilirsiniz, ancak bazı ekran görüntüleri farklı olacaktır ve bazı özellikler farklı olacaktır.

Visual Studio 2013 kullanıyorsanız, yükleme [Visual Studio 2013 için Azure SDK'sı](https://go.microsoft.com/fwlink/?LinkID=324322).

Visual Studio 2010 SP1 kullanıyorsanız, aşağıdaki yazılımları yükleyin:

- [Visual Studio 2010 için Azure SDK'sı](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server veri Araçları](https://msdn.microsoft.com/library/hh500335.aspx).

Bulunan SDK bağımlılığı sayısına makinenizde zaten bağlı olarak, Azure SDK'sı yüklenmesi birkaç dakikadan yarım saate uzanacak bir uzun sürebilir. Planladığınız bile yerine üçüncü taraf barındırma sağlayıcısına azure'a yayımlama, SDK, Visual Studio web en son güncelleştirmeleri içerdiğinden özellikleri yayımlamak Azure SDK'sı gerekir.

> [!NOTE]
> Bu öğreticide, Azure SDK'sının 1.8.1 sürümle yazılmıştır. Bu tarihten sonra ek özellikleri yeni sürümleriyle yayımlanmıştır. Öğreticiler, bu özellikler ve bunlar hakkında daha fazla bilgi olan kaynaklara bağlantı bahsetmek için güncelleştirilmiştir.


Yönergeler ve ekran görüntüleri Windows 8'de bağlıdır, ancak öğreticileri, Windows 7 için farkları açıklamaktadır.

Bu öğreticiyi tamamlamak için bazı diğer yazılımlar gereklidir, ancak henüz yüklü olması gerekmez. Öğretici, ihtiyacınız olduğunda, yükleme adımlarında size yol gösterir.

## <a name="download-the-sample-application"></a>Örnek uygulamayı indirin

Dağıtacağınıza uygulama Contoso University adlı ve sizin için zaten oluşturuldu. Açıklanan Contoso University uygulamanın gevşek bağlı bir university web sitesinin basitleştirilmiş bir sürüm olduğu [Entity Framework öğreticileri ASP.NET sitesinde](https://asp.net/entity-framework/tutorials).

Önkoşulların yüklü olduğunda indirme [Contoso University web uygulaması](https://go.microsoft.com/fwlink/p/?LinkId=282627). *.Zip* dosyası proje birden çok sürümünü içerir. Bu öğreticideki adımları ile çalışmak için C# klasöründe bulunan proje başlayın. Proje öğreticileri sonunda nasıl göründüğünü görmek için projeyi ContosoUniversity uç klasöründe açın.

Proje çalışma öğretici adımlarını hazırlamak için aşağıdaki adımları gerçekleştirin:

1. Visual Studio projeleriyle çalışmak için kullandığınız herhangi bir klasörde ContosoUniversity adlı bir klasörde C# klasöründen ContosoUniversity çözüm dosyalarını kaydedin.

    Varsayılan olarak bu Visual Studio 2012 için şu klasörü.

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (Bu öğreticideki ekran görüntüleri için proje klasörünün kök dizininde bulunur `C`: sürücü.)
2. Visual Studio'yu başlatın ve projeyi açın.
3. İçinde **Çözüm Gezgini**, çözüme sağ tıklayın ve tıklayın **EnableNuGet paketi geri yüklemeyi**.
4. Çözümü oluşturun.
5. El ile derleme hataları alırsanız, NuGet paketlerini geri yükleyin:

    1. İçinde **Çözüm Gezgini**, çözüme sağ tıklayın ve ardından **çözüm için NuGet paketlerini Yönet**.
    2. Üst kısmındaki **NuGet paketlerini Yönet** iletişim kutusunu göreceksiniz **bazı NuGet paketlerini bu çözümü eksik. Geri yüklemek için tıklayın.** Tıklayın **geri** düğmesi.
    3. Çözümü yeniden derleyin.
6. Uygulamayı çalıştırmak için CTRL-F5 tuşuna basın.

    Uygulama, Contoso University giriş sayfası açılır.

    ![Giriş sayfası geliştirme](introduction/_static/image1.png)

    (Visual Studio, SQL Server Express LocalDB örneğini başlatılırken bir bekleme süresi olabilir ve bir zaman aşımı hatası varsa, işlem çok uzun sürer alırsınız. Bu durumda yalnızca projeyi yeniden başlatın.)

Web sitesi sayfalarını, menü çubuğundan erişilebilir olduğundan ve şu işlevleri gerçekleştirmesini sağlar:

- Öğrenci istatistikleri (hakkında sayfası) görüntüler.
- Görüntüle, Düzenle, Sil ve öğrencileri ekleme.
- Görüntüleme ve düzenleme kurslar.
- Görüntüleme ve Eğitmenler düzenleyin.
- Görüntüleme ve düzenleme bölümler.

Birkaç temsili sayfaların ekran görüntüsü aşağıda verilmiştir.

![Öğrenciler sayfa geliştirme](introduction/_static/image2.png)

![Öğrenciler sayfa geliştirme Ekle](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>Dağıtım etkileyen uygulama özellikleri gözden geçirin

Uygulama aşağıdaki özellikleri, dağıttığınız nasıl veya ne bunu dağıtmak için yapmanız gereken etkiler. Aşağıdaki öğreticilerde serisindeki her birini daha ayrıntılı olarak açıklanmıştır.

- Contoso University Öğrenci ve Eğitmen adları gibi uygulama verilerini depolamak için bir SQL Server veritabanı kullanır. Veritabanı test verileri ve üretim verilerinin bir karışımını içerir ve üretime dağıtırken test verileri dışlamak gerekir.
- Uygulama, kullanıcı hesabı bilgilerini bir SQL Server veritabanında depolayan ASP.NET üyelik sistemini kullanır. Uygulama kısıtlı bazı bilgilere erişimi olan bir yönetici kullanıcının tanımlar. Üyelik veritabanı olmadan test hesapları, ancak bir yönetici hesabıyla dağıtmanız gerekebilir.
- Uygulama, bir üçüncü taraf hatası günlüğe kaydetme ve raporlama yardımcı programını kullanır. Bu yardımcı programı, uygulama ile dağıtılan bir derlemede sağlanır.
- Hata günlüğü yardımcı programı, dosya XML dosyalarında hata bilgilerini yazar. Dağıtılan sitede ASP.NET altında çalıştığı hesabın bu klasöre yazmak için izne sahip ve bu klasör dağıtımdan dışlama gerek emin olmalısınız. (Aksi halde hata günlük verilerini test ortamından üretim ortamına dağıtılmış olabilir ve/veya üretim hata günlük dosyalarını silinmiş olabilir.)
- Uygulama değiştirmesi gereken bazı ayarları içerir, dağıtılan *Web.config* hedef ortamı (test, hazırlama veya üretim) ve derleme bağlı olarak değiştirmesi gereken diğer ayarlarına bağlı olarak dosya (hata ayıklama veya sürüm) yapılandırması.
- Visual Studio çözüm, bir sınıf kitaplığı projesi içerir. Yalnızca bu projenin oluşturduğu derleme dağıtılması gerektiğini, proje kendisi değil.

## <a name="summary"></a>Özet

Serinin bu ilk öğreticide, örnek Visual Studio Proje indirilir ve uygulama dağıtımı etkileyen site özellikleri gözden. Aşağıdaki öğreticilerde, bazı otomatik olarak işlenmek üzere bunları ayarlayarak dağıtımı için hazırlayın. Diğerleri, el ile ilgileniriz.

> [!div class="step-by-step"]
> [Next](preparing-databases.md)
