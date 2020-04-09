---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio kullanarak web dağıtım ASP.NET: Web.config Dosya Dönüşümleri | Microsoft Dokümanlar'
author: tdykstra
description: Bu öğretici seri, ASP.NET bir web uygulamasını Azure App Service Web Apps'a veya bir üçüncü taraf barındırma sağlayıcısına nasıl dağıtabileceğinizi (yayınlayacağınızı) bize gösterir...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676127"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio kullanarak ASP.NET Web Dağıtım: Web.config Dosya Dönüşümleri

tarafından [Tom Dykstra](https://github.com/tdykstra)

[Başlangıç Projesini İndir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici seri, Visual Studio 2012 veya Visual Studio 2010'u kullanarak azure App Service Web Apps'a veya üçüncü taraf barındırma sağlayıcısına ASP.NET bir web uygulamasını nasıl dağıtabileceğinizi (yayımlayacağınızı) gösterir. Seri hakkında daha fazla bilgi için [serinin ilk öğreticisini](introduction.md)görün.

## <a name="overview"></a>Genel Bakış

Bu öğretici, *web.config* dosyasını farklı hedef ortamlara dağıtırken değiştirme işlemini nasıl otomatikleştirdiğinizi gösterir. Çoğu uygulamanın *Web.config* dosyasında, uygulama dağıtıldığında farklı olması gereken ayarlar vardır. Bu değişiklikleri yapma işlemini otomatikleştirmek, her dağıtımıyaptığınızda bunları el ile yapmanıza engel olur ve bu da sıkıcı ve hataya yatkın olur.

Hatırlatma: Bir hata iletisi alırsanız veya öğreticiden geçerken bir şey işe yaramazsa, [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config dönüşümleri ve Web Dağıtım parametreleri

*Web.config* dosya ayarlarını değiştirme işlemini otomatikleştirmenin iki yolu vardır: [Web.config dönüşümleri](https://msdn.microsoft.com/library/dd465326.aspx) ve [Web Dağıtma parametreleri.](https://msdn.microsoft.com/library/ff398068.aspx) *Bir Web.config* dönüştürme dosyası, dağıtıldığında *Web.config* dosyasının nasıl değiştirilebildiğini belirten XML biçimlendirmesi içerir. Belirli yapı yapılandırmaları ve belirli yayımlama profilleri için farklı değişiklikler belirtebilirsiniz. Varsayılan yapı yapılandırmaları Hata Ayıklama ve Sürüm'dir ve özel yapı yapılandırmaları oluşturabilirsiniz. Yayımlama profili genellikle hedef ortama karşılık gelir. (Test Ortamı öğreticisi [olarak IIS'ye Dağıtım'daki](deploying-to-iis.md) profilleri yayımlama hakkında daha fazla bilgi edineceksiniz.)

Web Dağıtım parametreleri, *Web.config* dosyalarında bulunan ayarlar da dahil olmak üzere dağıtım sırasında yapılandırılması gereken birçok farklı türde ayar belirtmek için kullanılabilir. *Web.config* dosya değişikliklerini belirtmek için kullanıldığında, Web Dağıtma parametreleri ayarlanacak daha karmaşıktır, ancak dağıtana kadar ayarlanacak değeri bilmediğiniz zaman kullanışlıdır. Örneğin, bir kuruluş ortamında, bir *dağıtım paketi* oluşturabilir ve bunu üretime yüklenmesi için BT departmanındaki bir kişiye verebilirsiniz ve bu kişinin bilmediğiniz bağlantı dizeleri veya parolaları girebilmesi gerekir.

Bu öğretici serisinin kapsadığı senaryo için, *Web.config* dosyasına yapılması gereken her şeyi önceden biliyorsunuz, bu nedenle Web Dağıtma parametrelerini kullanmanız gerekmez. Kullanılan yapı yapılandırmasına bağlı olarak farklı olan bazı dönüşümleri, kullanılan yayımlama profiline bağlı olarak değişen bazı dönüşümleri yapılandırırsınız.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure'da Web.config ayarlarını belirtme

Değiştirmek istediğiniz *Web.config* dosya ayarları `<connectionStrings>` öğede veya `<appSettings>` öğedeyse ve Azure Uygulama Hizmeti'nde Web Apps'a dağıtıyorsanız, dağıtım sırasında değişiklikleri otomatikleştirmek için başka bir seçeneğiniz vardır. Azure'da etkili olmak istediğiniz ayarları web uygulamanızın yönetim portalı sayfasının **Yapıla** sekmesine girebilirsiniz **(uygulama ayarlarına** ve **bağlantı dizeleri** bölümlerine gidin). Projeyi dağıttığınızda, Azure değişiklikleri otomatik olarak uygular. Daha fazla bilgi için [Windows Azure Web Siteleri: Uygulama Dizeleri ve Bağlantı Dizeleri Nasıl Çalışır.](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)

## <a name="default-transformation-files"></a>Varsayılan dönüştürme dosyaları

**Solution**Explorer'da, iki varsayılan yapı yapılandırması için varsayılan olarak oluşturulan *Web.Debug.config* ve *Web.Release.config* dönüşüm dosyalarını görmek için *Web.config'i* genişletin.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Web.config dosyasına sağ tıklayarak ve bağlam menüsünden **Config Dönüşümleri Ekle'yi** seçerek özel yapı yapılandırmaları için dönüşüm dosyaları oluşturabilirsiniz. Bu öğretici için bunu yapmanız gerekmez ve menü seçeneği devre dışı bırakılır, çünkü herhangi bir özel yapı yapılandırması oluşturmadın.

Daha sonra, test, evreleme ve üretim yayımlama profilleri için birer tane olmak üzere üç dönüşüm dosyası daha oluşturursunuz. Hedef ortama bağlı olduğu için bir yayımlama profili dönüştürme dosyasında işleyeceğiniz ayarın tipik bir örneği, test ve üretim için farklı olan bir WCF bitiş noktasıdır. Birlikte gittikleri yayımlama profillerini oluşturduktan sonra sonraki öğreticilerde yayımlama profil dönüşüm dosyaları oluşturursunuz.

## <a name="disable-debug-mode"></a>Hata ayıklama modunu devre dışı

Hedef ortam yerine yapı yapılandırması na bağlı bir `debug` ayar örneği özniteliktir. Sürüm oluşturma için, genellikle hangi ortama dağıtım yaptığınızdan bağımsız olarak hata ayıklamanın devre dışı bırakılmasını istersiniz. Bu nedenle, varsayılan olarak Visual Studio proje `compilation` şablonları, özniteliği öğeden `debug` kaldıran kodla *Web.Release.config* dönüştürme dosyalarını oluşturur. Burada varsayılan *Web.Release.config:* dışarı yorumlanan bazı örnek dönüşüm kodu ek olarak, özniteliği `compilation` `debug` kaldırır öğesi kodu içerir:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

Öznitelik, `xdt:Transform="RemoveAttributes(debug)"` özniteliğin dağıtılan *Web.config* `system.web/compilation` dosyasındaki öğeden kaldırılmasını istediğinizi `debug` belirtir. Bu, bir Sürüm yapınızı her dağıttığınızda yapılır.

## <a name="limit-error-log-access-to-administrators"></a>Yöneticilere hata günlüğü erişimini sınırlama

Uygulama çalışırken bir hata varsa, uygulama sistem tarafından oluşturulan hata sayfasının yerine genel bir hata sayfası görüntüler ve hata günlüğü ve raporlama için [Elmah NuGet paketini](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) kullanır. Uygulama `customErrors` *Web.config* dosyasındaki öğe hata sayfasını belirtir:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Hata sayfasını görmek için, `mode` öğenin özniteliğini `customErrors` geçici olarak "RemoteOnly"dan "On"a değiştirin ve uygulamayı Visual Studio'dan çalıştırın. *Studentsxxx.aspx*gibi geçersiz bir URL isteyerek hata yayılın. IIS tarafından oluşturulan "Kaynak bulunamıyor" hata sayfası *yerine, GenericErrorPage.aspx* sayfasını görürsünüz.

![Hata sayfası](web-config-transformations/_static/image2.png)

Hata günlüğünü görmek için, bağlantı noktası numarasından sonra URL'deki her şeyi `http://localhost:51130/elmah.axd` *elmah.axd* (örneğin,) ile değiştirin ve Enter tuşuna basın:

![ELMAH sayfası](web-config-transformations/_static/image3.png)

Bittiğinde öğeyi `customErrors` "RemoteOnly" moduna geri ayarlamayı unutmayın.

Geliştirme bilgisayarınızda hata günlüğü sayfasına ücretsiz erişime izin vermek uygundur, ancak üretimde bu bir güvenlik riski oluşturur. Üretim sitesi için, yöneticilere hata günlüğü erişimini kısıtlayan bir yetkilendirme kuralı eklemek ve kısıtlamanın test ve evrelemede de çalıştığından emin olmak istiyorsunuz. Bu nedenle, bir Sürüm yapısını her dağıttyaptığınızda uygulamak istediğiniz ve bu nedenle *Web.Release.config* dosyasına ait olan başka bir değişikliktir.

*Web.Release.config'i* açın `location` ve burada gösterildiği `configuration` gibi kapanış etiketinden hemen önce yeni bir öğe ekleyin.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

"Ekle" `Transform` öznitelik değeri, bu `location` öğenin `location` *Web.config* dosyasındaki varolan öğelere kardeş olarak eklenmesine neden olur. (Kredileri `location` **Güncelleştir** sayfası için yetkilendirme kurallarını belirten bir öğe zaten vardır.)

Artık dönüşümü doğru kodladığınızdan emin olmak için önizleyebilirsiniz.

**Çözüm Gezgini'nde,** *Web.Release.config'e* sağ tıklayın ve **Dönüştür'e Önizleme'yi**tıklatın.

![Dönüştür menüsünü önizleme](web-config-transformations/_static/image4.png)

Soldaki geliştirme *Web.config* dosyasını ve dağıtılan *Web.config* dosyasının sağda nasıl görüneceğini gösteren ve değişiklikler vurgulanan bir sayfa açılır.

![Hata ayıklama dönüşümü önizlemesi](web-config-transformations/_static/image5.png)

![Konum dönüştürmeönizleme](web-config-transformations/_static/image6.png)

( Önizlemede, dönüşümler yazmadığınız bazı ek değişiklikler fark edebilirsiniz: bunlar genellikle işlevselliği etkilemeyen beyaz alanın kaldırılmasını içerir.)

Dağıtımdan sonra siteyi sınadığınızda, yetkilendirme kuralının etkili olduğunu doğrulamak için de test esiniz.

> [!NOTE] 
> 
> **Güvenlik Notu** Bir üretim uygulamasında hata ayrıntılarını asla herkese görüntülemeyin veya bu bilgileri ortak bir konumda depolayın. Saldırganlar, bir sitedeki güvenlik açıklarını keşfetmek için hata bilgilerini kullanabilir. ELMAH'ı kendi uygulamanızda kullanıyorsanız, güvenlik risklerini en aza indirmek için ELMAH'ı yapılandırın. Bu öğreticideki ELMAH örneği önerilen yapılandırma olarak kabul edilmemelidir. Bu, uygulamanın içinde dosya oluşturabilmesi gereken bir klasörün nasıl işleyeceğini göstermek için seçilen bir örnektir. Daha fazla bilgi için [ELMAH bitiş noktasını güvence altına alma](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)konusuna bakın.

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Profil dönüştürme dosyalarında yayımlama da işleyeceğiniz bir ayar

Yaygın bir senaryo, dağıtdığınız her ortamda farklı olması gereken *Web.config* dosya ayarlarına sahip olmaktır. Örneğin, WCF hizmetini çağıran bir uygulamanın test ve üretim ortamlarında farklı bir bitiş noktası gerekebilir. Contoso Üniversitesi uygulaması da bu tür bir ayar içerir. Bu ayar, sitenin sayfalarında geliştirme, test veya üretim gibi hangi ortamda olduğunuzu söyleyen görünür bir göstergeyi denetler. Ayar değeri, uygulamanın *Site.Master* ana sayfasındaki ana başlık için "(Dev)" veya "(Test)" ekleyip ekmeyeceğini belirler:

![Çevre göstergesi](web-config-transformations/_static/image7.png)

Uygulama evreleme veya üretimde çalışırken ortam göstergesi atlanır.

Contoso Üniversitesi web sayfaları, uygulamanın `appSettings` hangi ortamda çalıştığını belirlemek için *Web.config* dosyasında ayarlanan bir değeri okur:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

Değer, test ortamında "Test" ve evreleme ve üretim için "Prod" olmalıdır.

Dönüştürme dosyasındaki aşağıdaki kod bu dönüşümü uygular:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform` Öznitelik değeri "SetÖzler" bu dönüşümün amacının *Web.config* dosyasındaki varolan bir öğenin öznitelik değerlerini değiştirmek olduğunu gösterir. `xdt:Locator` Öznitelik değeri "Match(key)" değiştirilecek öğenin burada belirtilen `key` öznitelikle `key` eşleşen öznitelik olduğunu gösterir. Öğenin `add` diğer tek `value`özniteliği, ve dağıtılan *Web.config* dosyasında değiştirilecek budur. Burada gösterilen kod, `value` öğenin `Environment` `appSettings` bağlı olduğu *Web.config* dosyasında "Test" olarak ayarlanacak özniteliğine neden olur.

Bu dönüştürme, henüz oluşturmadığınız yayımlama profili dönüştürme dosyalarına aittir. Test, evreleme ve üretim ortamları için yayımlama profilleri oluşturduğunuzda, bu değişikliği uygulayan dönüştürme dosyalarını oluşturur ve güncelleştirirsiniz. Bunu [IIS'ye dağıtımda](deploying-to-iis.md) yapar ve üretim öğreticilerine [dağıtabilirsiniz.](deploying-to-production.md)

> [!NOTE]
> Bu ayar `<appSettings>` öğeiçinde olduğundan, Azure Uygulama Hizmeti'nde Web Apps'a dağıtırken dönüşümü belirtmek için başka bir alternatifiniz var. Bu konuda [azure'da Web.config ayarlarını belirtmeye](#watransforms) bakın.

## <a name="setting-connection-strings"></a>Bağlantı dizelerini ayarlama

Varsayılan dönüştürme dosyası bir bağlantı dizesini nasıl güncelleştirebileceğinizi gösteren bir örnek içerse de, yayımlama profilinde bağlantı dizeleri belirtebildiğiniz için çoğu durumda bağlantı dize dönüşümleri ayarlamanız gerekmez. Bunu [IIS'ye dağıtımda](deploying-to-iis.md) yapar ve üretim öğreticilerine [dağıtabilirsiniz.](deploying-to-production.md)

## <a name="summary"></a>Özet

Artık yayımlama profillerini oluşturmadan önce *Web.config* dönüşümleri ile mümkün olduğunca çok şey yaptınız ve dağıtılan Web.config dosyasında neler olacağının bir önizlemesini gördünüz.

![Konum dönüştürmeönizleme](web-config-transformations/_static/image8.png)

Aşağıdaki öğreticide, proje özelliklerini ayarlamayı gerektiren dağıtım ayarlama görevlerini halleceksiniz.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu öğreticinin kapsadığı konular hakkında daha fazla bilgi için, Visual Studio ve ASP.NET için Web Dağıtım İçerik Haritası'nda [dağıtım sırasında hedef Web.config dosyasındaki veya app.config dosyasındaki ayarları değiştirmek için Web.config dönüşümlerini kullanma](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) konusuna bakın.

> [!div class="step-by-step"]
> [Önceki](preparing-databases.md)
> [Sonraki](project-properties.md)
