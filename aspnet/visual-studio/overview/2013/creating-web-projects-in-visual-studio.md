---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013'te ASP.NET Web Projeleri Oluşturma | Microsoft Dokümanlar
author: tdykstra
description: Bu konu Visual Studio ASP.NET web projeleri oluşturmak için seçenekleri açıklar 2013 Güncelleme ile 2013 İşte web geliştirme c için yeni özelliklerden bazıları ...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676050"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013’te ASP.NET Web Projeleri Oluşturma

tarafından [Tom Dykstra](https://github.com/tdykstra)

> Bu konu, Visual Studio 2013'te Güncelleme 3 ile ASP.NET web projeleri oluşturma seçeneklerini açıklar
> 
> Burada Visual Studio önceki sürümleri ile karşılaştırıldığında web geliştirme için yeni özelliklerden bazıları şunlardır:
> 
> - [Birden çok ASP.NET çerçevesi](#add) (Web Forms, MVC ve Web API) için destek sunan projeler oluşturmak için basit bir kullanıcı arabirimi.
> - [ASP.NET Kimlik,](#indauth)tüm ASP.NET çerçevelerinde aynı şekilde çalışan ve IIS dışındaki web barındırma yazılımı ile çalışan yeni bir ASP.NET üyelik sistemidir.
> - [Bootstrap'ın](#bootstrap) duyarlı tasarım ve temalı özellikler sağlamak için kullanılması.
> - [Otomatik test proje oluşturma](#testproj) ve [Intranet site şablonu](#winauth)gibi yalnızca MVC için sunulan Web Formları için yeni özellikler.
> 
> Azure Bulut Hizmetleri veya Azure Mobil Hizmetleri için web projeleri oluşturma hakkında bilgi için Azure [Bulut Hizmetleri ve ASP.NET ile Başlayın ve](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) Azure Mobil Hizmetleri [.NET Arka Uç ile Lider Panosu Uygulaması Oluşturma'ya](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)bakın.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Ön koşullar

Bu makale, Visual [Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) için güncelleştirme [3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) yüklü olarak geçerlidir.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web uygulama projeleri karşı web sitesi projeleri

ASP.NET web projeleri iki tür arasında bir seçim verir: *web uygulama projeleri* ve web sitesi *projeleri.* Yeni geliştirme için web uygulama projeleri öneririz ve bu makale yalnızca web uygulama projeleri için geçerlidir. Daha fazla bilgi için, MSDN sitesindeki [Visual Studio'daki Web Uygulama Projeleri ve Web Sitesi Projeleri'ne](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) bakın.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web uygulaması proje oluşturmaya genel bakış

Aşağıdaki adımlar, bir web projesinin nasıl oluşturulacak olduğunu gösterir:

1. **Başlat** sayfasında veya **Dosya** menüsünde **Yeni Proje'yi** tıklatın.
2. Yeni **Proje** iletişim kutusunda, sol bölmede **Web'i** ve orta bölmede **Web Uygulaması'nı ASP.NET** tıklatın.

    ![Yeni Proje iletişim kutusu](creating-web-projects-in-visual-studio/_static/image1.png)

    [Bir Azure Bulut Hizmeti, Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)Mobil [Hizmeti](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)veya [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)oluşturmak için sol bölmede **Bulut'u** seçebilirsiniz. Bu konu bu şablonları kapsamaz.
3. Sağ bölmede, uygulamanız için sistem durumu ve kullanım izlemesini istiyorsanız Proje onay **kutusuna Uygulama Öngörüleri Ekle'yi** tıklatın. Daha fazla bilgi için web [uygulamalarında performansı izleyin'](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)e bakın.
4. Proje **Adı,** **Konum**ve diğer seçenekleri belirtin ve ardından **Tamam'ı**tıklatın.

    **Yeni ASP.NET Projesi** iletişim kutusu görüntülenir.

    ![Yeni Proje iletişim kutusu](creating-web-projects-in-visual-studio/_static/image2.png)
5. Şablonu tıklatın.

    ![Şablon seçin](creating-web-projects-in-visual-studio/_static/image3.png)
6. Şablonda yer almayan ek çerçeveler için destek eklemek istiyorsanız, uygun onay kutusunu tıklatın. (Gösterilen örnekte, Bir Web Forms projesine MVC ve/veya Web API ekleyebilirsiniz.)

    ![Çerçeve ekleme](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Birim test projesi eklemek istiyorsanız, **birim testleri ekle'yi**tıklatın.

    ![Birim testi ekleme](creating-web-projects-in-visual-studio/_static/image5.png)
8. Şablonun varsayılan olarak sağladığından farklı bir kimlik doğrulama yöntemi istiyorsanız, **Kimlik Doğruluğunu Değiştir'i**tıklatın.

    ![Kimlik doğrulama düğmesini yapılandırma](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Kimlik doğrulama iletişim kutusunu yapılandırma](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure'da bir web uygulaması veya sanal makine oluşturma

Visual Studio, web uygulamalarını barındırmak için Azure hizmetleriyle çalışmayı kolaylaştıran özellikler içerir. Örneğin, Visual Studio IDE'den aşağıdaki lerin tümlerini yapabilirsiniz:

- Uygulamanızı Internet üzerinden kullanılabilir hale getiren web uygulamaları veya sanal makineler oluşturun ve yönetin.
- Bulutta çalışırken uygulama tarafından oluşturulan günlükleri görüntüleyin.
- Uygulama bulutta çalışırken hata ayıklama modunda uzaktan çalıştırın.
- SQL veritabanları gibi diğer Azure hizmetlerini görüntüleyin ve yönetin.

Ücretsiz web uygulamaları gibi temel hizmetleri içeren [bir Azure hesabı oluşturabilirsiniz](https://www.windowsazure.com/pricing/free-trial/) ve MSDN abonesiyseniz, ek Azure hizmetlerine yönelik aylık krediler veren [avantajları etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 

Varsayılan olarak **Yeni ASP.NET Projesi** iletişim kutusu, yeni bir web projesi için bir web uygulaması veya sanal makine oluşturmanıza olanak tanır. Yeni bir web uygulaması veya sanal makine oluşturmak istemiyorsanız, Bulut onay kutusunda **Ana Bilgisayar'ı** temizleyin.

![Uzak kaynaklar oluşturma](creating-web-projects-in-visual-studio/_static/image8.png)

Onay kutusu başlığı **bulutta Ana Bilgisayar** veya **Uzak Kaynaklar Oluştur**olabilir ve her iki durumda da etkisi aynıdır. Onay kutusunu seçili bırakırsanız, Visual Studio varsayılan olarak Azure Uygulama Hizmeti'nde bir web uygulaması oluşturur. İsterseniz sanal **makine** olarak değiştirmek için açılır kutusunu kullanabilirsiniz. Azure'da zaten oturum açmış değilseniz, Azure kimlik bilgileri için istenirsiniz. Oturum açtıktan sonra, bir iletişim kutusu Visual Studio'nun projeniz için oluşturacağı kaynakları yapılandırmanızı sağlar. Aşağıdaki resimde bir web uygulaması için iletişim gösterir; sanal bir makine oluşturmayı seçerseniz farklı seçenekler görüntülenir.

![Azure Uygulama Ayarlarını Yapılandırma](creating-web-projects-in-visual-studio/_static/image9.png)

Azure kaynakları oluşturmak için bu işlemi nasıl kullanacağınız hakkında daha fazla bilgi için azure [ve ASP.NET ile başlayın ve](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) Visual [Studio'ya sahip bir web sitesi için sanal makine oluşturma](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)bilgisine bakın.

Bu makalenin geri kalanı, kullanılabilir şablonlar ve seçenekleri hakkında daha fazla bilgi sağlar. Makalede ayrıca Bootstrap, düzen ve şablonlarda kullanılan temalı çerçeve tanıtılır.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web Proje Şablonları

Visual Studio, web projeleri oluşturmak için şablonlar kullanır. Proje şablonu yeni projede dosya ve klasörler oluşturabilir, NuGet paketlerini yükleyebilir ve temel bir çalışma uygulaması için örnek kod sağlayabilir. Şablonlar en son web standartlarını uygular ve ASP.NET teknolojilerinnasıl kullanılacağına ilişkin en iyi uygulamaları göstermek ve kendi uygulamanızı oluşturmanızda size hızlı bir başlangıç sağlamak için tasarlanmıştır.

Visual Studio 2013, .NET çerçevesinin .NET 4.5 veya sonraki sürümlerini hedefleyen projeler için web proje şablonları için aşağıdaki seçenekleri sağlar:

- [Boş şablon](#empty)
- [Web Formları şablonu](#wf)
- [MVC şablonu](#mvc)
- [Web API şablonu](#webapi)
- [Tek Sayfa Uygulama şablonu](#spa)
- [Azure Mobil Hizmet şablonu](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 Şablonları](#vs2012)

Ayrıca, [Facebook şablonu](#facebook)sağlayan bir Visual Studio uzantısı da yükleyebilirsiniz.

.NET 4'e yönelik projelerin nasıl oluşturulabildiğini öğrenmek için visual [studio 2012 Şablonları'na](#vs2012) bakın.

Mobil istemciler için ASP.NET uygulamaları nın nasıl oluşturulabildiğini öğrenmek için [ASP.NET'da Mobil Destek'e](../../../mobile/overview.md)bakın.

<a id="empty"></a>
### <a name="empty-template"></a>Boş Şablon

Boş ASP.NET şablon, proje dosyası (*.csproj* veya .* vbproj*) ve bir *Web.config* dosyası. Klasörekle altındaki onay kutularını ve aşağıdaki etiket için **temel referansları** kullanarak Web Formları, MVC ve/veya Web API desteği ekleyebilirsiniz.

Boş şablon için kimlik doğrulama seçeneği kullanılamaz. Örnek uygulamalarda kimlik doğrulama işlevi uygulanır ve Boş şablon örnek bir uygulama oluşturmaz.

<a id="wf"></a>
### <a name="web-forms-template"></a>Web Formları Şablonu

Web Formları çerçevesi, kullanıcı lık bilgisi ve veri erişim özellikleri açısından zengin web sitelerini hızla yürütmenize izin veren şeni' dir:

- Visual Studio'da wysiwyg tasarımcısı.
- HTML'yi oluşturan ve özellikleri ve stilleri ayarlayarak özelleştirebileceğiniz sunucu denetimleri.
- Veri erişimi ve veri görüntüleme için zengin bir denetim yelpazesi.
- WPF gibi bir istemci uygulamasını programlayacağınız gibi programlayabildiğiniz olayları ortaya çıkaran bir olay modeli.
- HTTP istekleri arasındaki durum (verilerin) otomatik olarak korunması.

Genel olarak, Bir Web Forms uygulaması oluşturmak, ASP.NET MVC çerçevesini kullanarak aynı uygulamayı oluşturmaktan daha az programlama çabası gerektirir. Ancak, Web Formları sadece hızlı uygulama geliştirme için değildir. Web Formları'nın üzerine inşa edilmiş birçok karmaşık ticari uygulama ve çerçeve vardır.

Bir Web Forms sayfası ve sayfadaki denetimler otomatik olarak tarayıcıya gönderilen biçimlendirmenin çoğunu oluşturduğundan, MVC'nin sunduğu ASP.NET HTML üzerinde ince taneli denetime sahip değilsiniz. Sayfaları ve denetimleri yapılandırmak için bildirimsel model, yazmanız gereken kod miktarını en aza indirir, ancak HTML ve HTTP'nin bazı davranışlarını gizler. Örneğin, bir denetim tarafından tam olarak hangi biçimlendirmenin oluşturulabileceğini belirtmek her zaman mümkün değildir.

Web Forms çerçevesi, [test odaklı geliştirme,](http://en.wikipedia.org/wiki/Test-driven_development) [endişelerin ayrılması,](http://en.wikipedia.org/wiki/Separation_of_concerns) [kontrol ters çevrilmesi](http://en.wikipedia.org/wiki/Inversion_of_control)ve [bağımlılık enjeksiyonu](http://en.wikipedia.org/wiki/Dependency_injection)gibi kalıptabanlı geliştirme uygulamalarına MVC ASP.NET kadar kolay bir şekilde kendini ödünç vermez. Bu şekilde çarpana kodu yazmak istiyorsanız, yapabilirsiniz; sadece ASP.NET MVC çerçevesinde olduğu gibi otomatik değil. ASP.NET Web Forms MVP projesi, Web [Formlarının](http://webformsmvp.com/) sunmak üzere inşa edildiği hızlı gelişimi sürdürürken endişelerin ve test edilebilirliğin ayrılmasını kolaylaştıran bir yaklaşım gösterir. Microsoft SharePoint, Web Forms MVP'si üzerine kurulmuştur.

Web Formları şablonu, duyarlı tasarım ve temalı özellikler sağlamak için [Bootstrap](#bootstrap) kullanan örnek bir Web Forms uygulaması oluşturur. Aşağıdaki resimde ana sayfa gösterilmektedir.

![Web Formları şablon uygulaması giriş sayfası](creating-web-projects-in-visual-studio/_static/image10.png)

Web Formları hakkında daha fazla bilgi için [ASP.NET Web Formları'na](https://asp.net/web-forms)bakın. Web Formları şablonu sizin için ne yaptığı hakkında bilgi için Visual [Studio 2013'ün kullanımıyla temel bir Web Formları uygulaması oluşturma](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)'ya bakın.

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC Şablonu

ASP.NET MVC, [test odaklı geliştirme,](http://en.wikipedia.org/wiki/Test-driven_development) [endişelerin ayrılması,](http://en.wikipedia.org/wiki/Separation_of_concerns) [kontrol ters çevrilmesi](http://en.wikipedia.org/wiki/Inversion_of_control)ve bağımlılık [enjeksiyonu](http://en.wikipedia.org/wiki/Dependency_injection)gibi kalıp tabanlı geliştirme uygulamalarını kolaylaştırmak üzere tasarlanmıştır. Çerçeve, bir web uygulamasının iş mantığı katmanını sunum katmanından ayırmayı teşvik eder. Uygulamayı modellere (M), görünümlere (V) ve denetleyicilere (C) bölerek, mvc ASP.NET daha büyük uygulamalarda karmaşıklığı yönetmeyi kolaylaştırabilir.

MVC ASP.NET, Web Formlar'dan daha doğrudan HTML ve HTTP ile çalışırsınız. Örneğin, Web Formları HTTP istekleri arasındaki durumu otomatik olarak koruyabilir, ancak açıkça MVC'de kodlaman gerekir. MVC modelinin avantajı, uygulamanızın tam olarak ne yaptığı ve web ortamında nasıl davrandığı üzerinde tam kontrol edebilmenizi sağlamasıdır. Dezavantajı daha fazla kod yazmak zorunda olmasıdır.

MVC genişletilebilir olacak şekilde tasarlanmıştır, güç geliştiricilerkendi uygulama ihtiyaçları için çerçeve özelleştirmek için yeteneği sağlayan. Buna ek olarak, ASP.NET MVC kaynak kodu bir OSI lisansı altında kullanılabilir.

MVC şablonu, duyarlı tasarım ve temalı özellikler sağlamak için [Bootstrap](#bootstrap) kullanan örnek bir MVC 5 uygulaması oluşturur. Aşağıdaki resimde ana sayfa gösterilmektedir.

![MVC örnek uygulaması](creating-web-projects-in-visual-studio/_static/image11.png)

MVC hakkında daha fazla bilgi için [ASP.NET MVC'ye](https://asp.net/mvc)bakın. MVC 4 şablonu nasıl seçilecek hakkında daha fazla bilgi için bu makalenin ilerleyen saatlerinde [Visual Studio 2012 şablonlarına](#vs2012) bakın.

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API Şablonu

Web API şablonu, MVC'yi temel alan API yardım sayfaları da dahil olmak üzere Web API'sini temel alan örnek bir web hizmeti oluşturur.

ASP.NET Web API, tarayıcılar ve mobil cihazlar da dahil olmak üzere çok çeşitli istemcilere ulaşan HTTP hizmetlerinin oluşturulmasını kolaylaştıran bir çerçevedir. ASP.NET Web API,.NET Framework üzerinde yeni hizmetler oluşturmak için ideal bir platformdur.

Web API şablonu örnek bir web hizmeti oluşturur. Aşağıdaki resimlerörnek yardım sayfalarını gösterir.

![Web API yardım sayfası](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API için Web API yardım sayfası](creating-web-projects-in-visual-studio/_static/image13.png)

Web API hakkında daha fazla bilgi için [ASP.NET Web API'ye](https://asp.net/web-api)bakın.

<a id="spa"></a>
### <a name="single-page-application-template"></a>Tek Sayfa uygulama şablonu

Tek Sayfa uygulaması (SPA) şablonu, istemcide JavaScript, HTML 5 ve [KnockoutJS](http://knockoutjs.com/) kullanan bir örnek uygulama oluşturur ve sunucuda Web API'ASP.NET.

SPA şablonu için tek kimlik doğrulama seçeneği [Bireysel Kullanıcı Hesapları'dır.](#indauth)

Aşağıdaki resimde, SPA şablonunun oluşturduğu örnek uygulamanın ilk durumu gösterilmektedir.

![SPA örnek uygulaması](creating-web-projects-in-visual-studio/_static/image14.png)

SPA şablonunu kullanarak uygulama oluşturma hakkında daha fazla bilgi için [Web API - Dış Kimlik Doğrulama Hizmetleri'ne](../../../web-api/overview/security/external-authentication-services.md)bakın.

ASP.NET Tek Sayfa uygulamaları ve KnockoutJS dışındaki JavaScript çerçevelerini kullanan ek SPA şablonları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET Tek Sayfa Uygulaması](../../../single-page-application/index.md).
- [VS2013 RC için SPA Şablonundaki Güvenlik Özelliklerini Anlama](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Tek Sayfauygulamaları: ASP.NET ile Modern, Duyarlı Web Uygulamaları Oluşturun](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook Şablonu

[Facebook şablonu sağlayan bir Visual Studio uzantısı](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)yükleyebilirsiniz. Bu şablon, Facebook web sitesi içinde çalışacak şekilde tasarlanmış bir örnek uygulama oluşturur. MVC ASP.NET dayanır ve gerçek zamanlı güncelleştirme işlevleri için Web API kullanır.

Facebook uygulamaları Facebook sitesi içinde çalıştığı ve Facebook'un kimlik doğrulamasını güvendiği için Facebook şablonu için kimlik doğrulama seçeneği yoktur.

ASP.NET Facebook uygulamaları hakkında daha fazla bilgi için [MVC Facebook API'sını güncelleştirmeye](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)bakın.

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 Şablonları

Visual Studio 2013 web proje oluşturma iletişim kutusu Visual Studio 2012'de bulunan bazı şablonlara erişim sağlamaz. Bu şablonlardan birini kullanmak istiyorsanız, Visual Studio Yeni Proje iletişim kutusunun sol bölmesinde Visual Studio 2012 düğüm'üne tıklayabilirsiniz.

![Visual Studio 2012 şablonları](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012** düğümü, Visual Studio 2013 için varsayılan şablonlar listesinde erişiminiz olmayan aşağıdaki web şablonlarını seçmenize olanak tanır:

- ASP.NET MVC 4 Web Uygulaması
- ASP.NET Dinamik Veri Varlıkları Web Uygulaması
- ASP.NET AJAX Sunucu Kontrolü
- ASP.NET AJAX Sunucu Kontrol Genişletici
- ASP.NET Sunucu Denetimi

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Görsel Stüdyo 2013 web proje şablonlarında Bootstrap

Visual Studio 2013 proje şablonları [Bootstrap](http://getbootstrap.com/)kullanın , bir düzen ve Twitter tarafından oluşturulan temalı çerçeve. Bootstrap, duyarlı tasarım sağlamak için CSS3 kullanır, bu da düzenlerin farklı tarayıcı pencere boyutlarına dinamik olarak adapte olabileceği anlamına gelir. Örneğin, geniş bir tarayıcı penceresinde Web Formları şablonu tarafından oluşturulan ana sayfa aşağıdaki çizime benzer:

![Web Formları şablon uygulaması giriş sayfası](creating-web-projects-in-visual-studio/_static/image16.png)

Pencereyi daraltın ve yatay olarak düzenlenmiş sütunlar dikey düzenlemeye taşınır:

![Bootstrap dikey kolon düzenlemesi](creating-web-projects-in-visual-studio/_static/image17.png)

Pencereyi biraz daha daraltın ve yatay üst menü dikey olarak yönlendirilmiş bir menüye genişletmek için tıklatabileceğiniz bir simgeye dönüşür:

![Bootstrap menü simgesi](creating-web-projects-in-visual-studio/_static/image18.png)

![Bootstrap dikey menü](creating-web-projects-in-visual-studio/_static/image19.png)

Uygulamanın görünümündeki ve hislerindeki bir değişikliği kolayca etkilemek için Bootstrap'ın temalı özelliğini de kullanabilirsiniz. Örneğin, temayı değiştirmek için aşağıdaki adımları yapabilirsiniz.

1. Tarayıcınızda, bir [http://Bootswatch.com](http://Bootswatch.com)tema seçin ve ardından **İndir'i**tıklatın. (Bu indirir *bootstrap.min.css* varsayılan olarak; CSS kodunu incelemek istiyorsanız, minified sürümü yerine *bootstrap.css* olsun.)
2. İndirilen CSS dosyasının içeriğini kopyalayın.
3. Visual Studio'da, *İçerik* klasöründe *bootstrap-theme.css* adlı yeni bir **Stil Sayfası** dosyası oluşturun ve indirilen CSS kodunu yapıştırın.
4. Açık *\_App Başlat /Bundle.config* ve *bootstrap.css için bootstrap.css* *değiştirin*.

Projeyi yeniden çalıştırın ve uygulama yeni bir görünüme sahip. Aşağıdaki resimde Amelia temasının etkisi gösterilmektedir:

![Bootstrap Amelia teması](creating-web-projects-in-visual-studio/_static/image20.png)

Birçok Bootstrap temalar mevcuttur, hem ücretsiz ve prim sürümleri. Bootstrap ayrıca [açılır bırakma,](http://twitter.github.io/bootstrap/components.html#dropdowns) [düğme grupları](http://twitter.github.io/bootstrap/components.html#buttonGroups)ve [simgeler](http://twitter.github.io/bootstrap/base-css.html#images)gibi çok çeşitli UI bileşenleri sunar. Bootstrap hakkında daha fazla bilgi için [Bootstrap sitesine](http://twitter.github.io/bootstrap/)bakın.

Visual Studio'da Web Forms tasarımcısını kullanıyorsanız, tasarımcının CSS3'ü desteklemediğini, bu nedenle Bootstrap temalarının veya duyarlı düzen değişikliklerinin tüm etkilerini doğru şekilde göstermediğini unutmayın. Ancak, Web Formları sayfaları bir tarayıcıyla görüntülendiğinde doğru şekilde görüntülenir.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Ek Çerçeveler için Destek Ekleme

Bir şablon seçtiğinizde, şablon tarafından kullanılan framework(ler) için onay kutusu otomatik olarak seçilir. Örneğin, **Web Formları** şablonu seçerseniz, Web **Formları** onay kutusu seçilir ve bunu temizleyemezsiniz.

![Şablon seçin](creating-web-projects-in-visual-studio/_static/image21.png)

![Çerçeve ekleme](creating-web-projects-in-visual-studio/_static/image22.png)

Proje oluşturulduğunda bu çerçeve için destek eklemek için şablona dahil olmayan bir çerçeve için onay kutusunu seçebilirsiniz. Örneğin, MVC şablonu seçtiğinizde Web Forms *.aspx* sayfalarının kullanımını etkinleştirmek için **Web Formları** onay kutusunu seçin. Veya Web Formları şablonu kullanırken MVC'yi etkinleştirmek için **MVC** onay kutusunu tıklatın. Bir çerçeve eklemek, tasarım zamanının yanı sıra çalışma zamanı desteği sağlar. Örneğin, bir Web Forms projesine MVC desteği eklerseniz, denetleyicileri ve görünümleri iskeleye göre şekillendirebilirsiniz.

Web Formlarını ve MVC'yi bir projede birleştirir ve Web [Formlarında Dost URL'leri](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) etkinleştirirseniz, bir URL'nin birden çok olası hedefi olduğu beklenmeyen yönlendirme sorunları olabilir. İlk olarak tanımlanan yollar öncelikli olacaktır. Örneğin, `Home` bir denetleyiciniz ve *Home.aspx* sayfanız `http://contoso.com/home` varsa, *RouteConfig.cs*yöntemi ni çağırmadan `MapRoute` `EnableFriendlyUrls` önce yöntemi ararsanız URL *Home.aspx'e* gider veya `Home` daha önce `EnableFriendlyUrls` `MapRoute` ararsanız aynı URL denetleyiciniz için varsayılan görünüme gider.

Çerçeve eklemek herhangi bir örnek uygulama işlevi eklemez. Örneğin, MVC şablonu seçtiğinizde Web Formları desteği eklerseniz, *Varsayılan.aspx* ana sayfa dosyası oluşturulmaz. Yalnızca çerçeveyi desteklemek için gereken klasörler, dosyalar ve başvurular eklenir. Bu nedenle, çerçeve eklemek, şablonlar tarafından oluşturulan örnek uygulamalarda kod tarafından uygulanan kimlik doğrulama seçeneklerini değiştirmez. Örneğin, Boş şablonunu seçip Web Formları veya MVC desteği eklerseniz, **Kimlik Doğrulamayı Yapılandır** düğmesi yine devre dışı bırakılır.

Aşağıdaki bölümlerde her onay kutusunun etkisi kısaca açıklayınız.

### <a name="add-web-forms-support"></a>Web Formları Desteği Ekle

Boş *\_Uygulama Verileri* ve *Modelleri* klasörleri ve *Global.asax* dosyası oluşturur. Bunlar zaten Boş şablon dışındaki tüm şablonlar tarafından oluşturulur, bu nedenle Web Formları onay kutusunu seçmek diğer şablonlar için fark etmez.

Web Formları şablonu varsayılan olarak Ortak URL'lere olanak sağlar, ancak Web Formları onay kutusunu seçerek diğer şablonlara Web Formları desteği eklediğinizde Otomatik olarak etkinleştirilmez.

### <a name="add-mvc-support"></a>MVC Desteği Ekle

MVC, Razor ve WebPages NuGet paketlerini yükler, boş *\_Uygulama Verileri,* *Denetleyiciler,* *Modeller*ve *Görünümklasörleri* oluşturur, *RouteConfig.cs* dosyasıyla *App\_Start* klasörü oluşturur ve *Global.asax* dosyaoluşturur.

### <a name="add-web-api-support"></a>Web API Desteği Ekle

WebApi ve Newtonsoft.Json NuGet paketlerini yükler, boş *\_Uygulama Verileri,* *Denetleyiciler*ve *Modeller* klasörleri oluşturur, *WebApiConfig.cs* dosyasıyla *App\_Start* klasörü oluşturur ve *Global.asax* dosyalarını oluşturur.

<a id="auth"></a>
## <a name="authentication-methods"></a>Kimlik Doğrulaması Yöntemleri

Visual Studio 2013, Web Formları, MVC ve Web API şablonları için çeşitli kimlik doğrulama seçenekleri sunar:

- [Kimlik Doğrulaması Yok](#noauth)
- [Bireysel Kullanıcı Hesapları](#indauth) (ASP.NET Kimliği, eski adıyla ASP.NET üyelik)
- [Kuruluş Hesapları](#orgauth) (Windows Server Etkin Dizini veya Azure Etkin Dizini)
- [Windows Kimlik Doğrulama](#winauth) (Intranet)

![Kimlik doğrulama iletişim kutusunu yapılandırma](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Kimlik Doğrulaması Yok

**Kimlik Doğrulama Yok'u**seçerseniz, örnek uygulama oturum açmak için web sayfası içermez, kimlerin oturum açtığını gösteren kullanıcı arabirimi, üyelik veritabanı için varlık sınıfları ve üyelik veritabanı için bağlantı dizesi içermez.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Bireysel Kullanıcı Hesapları

**Bireysel Kullanıcı Hesapları'nı**seçerseniz, örnek uygulama kullanıcı kimlik doğrulaması için ASP.NET Kimlik (eski adıyla ASP.NET üyelik olarak bilinir) kullanacak şekilde yapılandırılır. ASP.NET Kimlik, kullanıcının sitede bir kullanıcı adı ve parola oluşturarak veya Facebook, Google, Microsoft Hesabı veya Twitter gibi sosyal sağlayıcılarla oturum açarak bir hesap kaydetmesini sağlar. ASP.NET Identity'deki kullanıcı profilleri için varsayılan veri deposu, üretim sitesi için SQL Server veya Azure SQL Veritabanı'na dağıtabileceğiniz bir SQL Server LocalDB veritabanıdır.

Visual Studio 2013'te bu özellikler Visual Studio 2012'dekiyle aynıdır, ancak ASP.NET üyelik sisteminin temel kodu yeniden yazılmıştır. Yeni kod tabanının avantajları şunlardır:

- Yeni üyelik sistemi, formlar kimlik doğrulama modülüASP.NET yerine [OWIN'e](http://owin.org/) dayanmaktadır. Bu, IIS'de Web Formları veya MVC kullanıyor sanız veya Web API veya SignalR'ı kendi kendine barındıran aynı kimlik doğrulama mekanizmasını kullanabileceğiniz anlamına gelir.
- Yeni üyelik veritabanı Önce Varlık Çerçeve Kodu tarafından yönetilir ve tüm tablolar değiştirebileceğiniz varlık sınıfları tarafından temsil edilir. Bu, veritabanı şemasını ve profille ilgili web ui'sini kendi gereksinimlerinize uyacak şekilde kolayca özelleştirebileceğiniz ve güncelleştirmelerinizi Kod İlk Geçişleri'ni kullanarak kolayca dağıtabileceğiniz anlamına gelir.

Yeni üyelik sistemi yeni şablonlarda otomatik olarak uygulanır ve .NET 4.5 veya daha sonrasını hedefleyen herhangi bir projede el ile uygulanabilir.

ASP.NET Kimlik, özellikle dış müşteriler için bir Internet web sitesi oluşturuyorsanız iyi bir seçimdir. Kuruluşunuz Active Directory veya Office 365 kullanıyorsa ve çalışanlar ve iş ortakları için tek oturum açmasağlayan bir proje oluşturmak istiyorsanız, **Kuruluş Hesapları** seçeneği daha iyi bir seçim olabilir.

Bireysel Kullanıcı Hesapları seçeneği hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [www.asp.net/identity.](../../../identity/index.md) ASP.NET web sitesinde ASP.NET Kimliği ile ilgili belgeler.
- [Facebook ve Google OAuth2 ve OpenID Oturum Aç ile ASP.NET Bir MVC 5 Uygulaması oluşturun.](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Ayrıca, kullanıcı profili verilerinin nasıl özelleştirilebildiğini de gösterir.
- [Web API - Dış Kimlik Doğrulama Hizmetleri](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013'te ASP.NET uygulamanıza Harici Giriş Ekleme](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Kuruluş Hesapları

**Kuruluş Hesapları'nı**seçerseniz, örnek uygulama, Azure Active Directory (Azure AD, Office 365) veya Windows Server Active Directory'deki kullanıcı hesaplarına dayalı kimlik doğrulama için Windows Identity Foundation (WIF) kullanacak şekilde yapılandırılır. Daha fazla bilgi için, bu konuda daha sonra [Kuruluş hesabı kimlik doğrulama seçeneklerine](#orgauthoptions) bakın.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows Kimlik Doğrulaması

**Windows Kimlik Doğrulama'yı**seçerseniz, örnek uygulama kimlik doğrulama için Windows Kimlik Doğrulama IIS modülünü kullanacak şekilde yapılandırılır. Uygulama, Windows'a giriş yapılan ancak kullanıcı kaydı veya oturum açma kullanıcı ui içermeyen Etkin dizinin veya yerel makine hesabının etki alanını ve kullanıcı kimliğini görüntüler. Bu seçenek Intranet web siteleri için tasarlanmıştır.

Alternatif olarak, [Kuruluş Hesapları altında Şirket İçi seçeneğini](#orgauthonprem)seçerek AD kimlik doğrulamasını kullanan bir Intranet sitesi oluşturabilirsiniz. Şirket Içi seçeneği, Windows Kimlik Doğrulama modülü yerine Windows Identity Foundation (WIF) kullanır. Şirket İçi seçeneğini ayarlamak için bazı ek adımlar gerekir, ancak WIF, Windows Kimlik Doğrulama modülünde kullanılamayan özellikleri etkinleştirir. Örneğin, WIF ile Etkin Dizin ve sorgu dizini verilerinde uygulama erişimini yapılandırabilirsiniz.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Kuruluş hesabı kimlik doğrulama seçenekleri

**Yapılı Kimlik Doğrulama** iletişim kutusu, Azure Etkin Dizini (Office 365' i i çeken Azure AD) veya Windows Server Active Directory (AD) hesap kimlik doğrulaması için çok sayıda seçenek sunar:

- [Bulut - Tek Kuruluş](#orgauthsingle) (Azure AD veya AD, Azure AD ile dizin tümleştirmesi kullanarak)
- [Bulut - Çoklu Organizasyon](#orgauthmulti) (Azure AD veya AD, Azure AD ile dizin tümleştirmesi kullanarak)
- [Şirket Içi](#orgauthonprem) (AD)

Azure AD seçeneklerinden birini denemek istiyorsanız ancak henüz bir hesabınız yoksa, [Azure AD hesabına kaydolmak için burayı tıklatın.](https://go.microsoft.com/fwlink/?LinkId=309942)

> [!NOTE]
> Azure AD seçeneklerinden birini seçerseniz, projeniz in bir veritabanı gerektirir ve Azure AD kiracınız için genel bir yönetici hesabında oturum açmanız gerekir. Azure AD kiracınız için yönetim izinleri admin@contoso.onmicrosoft.comolan bir kuruluş hesabının adını ve parolasını girin.
> 
> **Oturum açma iletişim kutusuna bir Microsoft contoso@hotmail.comhesabının kimlik bilgilerini (örneğin, ) girmeyin.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Bulut - Tek Kuruluş Kimlik Doğrulama

![Tek Kuruluş Kimlik Doğrulama](creating-web-projects-in-visual-studio/_static/image24.png)

Bir Azure AD [kiracısında](https://technet.microsoft.com/library/jj573650.aspx)tanımlanan kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız bu seçeneği belirleyin. Örneğin, site contoso.com ve contoso.onmicrosoft.com kiracı olan Contoso Şirket çalışanları için kullanılabilir hale getirilecektir. Azure AD'yi diğer kiracılardan kullanıcıların uygulamaya erişmesine izin verecek şekilde yapılandıramazsınız.

#### <a name="domain"></a>Domain

Uygulamayı ayarlamak istediğiniz Azure AD etki alanını girin, örneğin: `contoso.onmicrosoft.com`. Özel bir [etki alanınız](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/) `contoso.com` varsa, `contoso.onmicrosoft.com`bunun yerine, bunu buradan girebilirsiniz.

#### <a name="access-level"></a>Erişim Düzeyi

Uygulamanın Grafik API'sini kullanarak dizin bilgilerini sorgulaması veya güncelleştirmesi gerekiyorsa, **Tek Oturum Açma, Dizin Verilerini Okuma** veya Tek Oturum **Açma, Okuma ve Yazma Dizin Verileri'ni**seçin. Aksi takdirde, **Tek Oturum Açma'yı**seçin. Daha fazla bilgi için, Azure REKLAMını Sorgulamak için [Uygulama Erişim Düzeyleri](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) ve Grafik [API'sini kullanma'ya](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)bakın.

#### <a name="application-id-uri"></a>Uygulama Kimliği URI

Varsayılan olarak, şablon, proje adını Azure AD etki alanına ekleyerek sizin için bir uygulama kimliği URI oluşturur. Örneğin, proje adı ve `Example` etki alanı `contoso.onmicrosoft.com`ise, uygulama `https://contoso.onmicrosoft.com/Example`kimliği URI olur. Uygulama Kimliği URI'yi el ile belirtmek istiyorsanız, **Daha Fazla Seçenek** bölümünü genişletin ve metin kutusuna uygulama kimliği URI'yi girin. Uygulama Kimliği URI ile `https://`başlamalıdır.

Varsayılan olarak, Azure AD'de zaten sağlanan bir uygulama Visual Studio'nun proje için kullandığı uygulama kimliği URI ile aynıysa, proje yeni bir uygulama sağlamak yerine varolan uygulamaya bağlanır. Bu durumda yeni bir uygulamanın sağlanmasını istiyorsanız, **aynı kimlikte olan onay kutusunun** üzerinde yazan uygulama girişini temizleyin.

**Overwrite** onay kutusu temizlenir sa ve Visual Studio aynı uygulama kimliği URI ile varolan bir uygulama bulursa, kullanmak için gidiyordu URI bir numara ekleyerek yeni bir URI oluşturur. Örneğin, proje adının `Example`, metin kutusunu boş bıraktığınız, **Overwrite onay** kutusunu temizlediğinizi ve Azure AD `https://contoso.onmicrosoft.com/Example`kiracısının URI ile zaten bir uygulaması olduğunu varsayalım. Bu durumda, yeni bir uygulama gibi `https://contoso.onmicrosoft.com/Example_20130619330903`bir uygulama Kimliği URI ile sağlanacaktır.

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD'de uygulama nın sağlanması

Uygulamayı Azure AD'de sağlamak veya projeyi varolan bir uygulamaya bağlamak için Visual Studio'nun etki alanı için genel bir yöneticinin kimlik bilgilerine ihtiyacı vardır. **Yapılandırma Kimlik Doğrulama** iletişim kutusunda **Tamam'ı** tıklattığınızda, belirttiğiniz etki alanı için genel bir yöneticinin kullanıcı adı ve parolası istenir. Daha sonra, Yeni ASP.NET **Projesi** iletişim kutusunda **Project Oluştur'u** tıklattığınızda, Visual Studio uygulamayı Azure AD'de karşılar. Bu işlemin bir parçası olarak Visual Studio'nun, oluşturulduktan bir yıl sonra süresi dolan Web.config dosyasına istemci gizli değerlerini yerleştirdiğini unutmayın.

**Bulut - Tek Kuruluş** kimlik doğrulamasını kullanan uygulamaların nasıl oluşturulacagerektiği hakkında bilgi için aşağıdaki kaynaklara bakın:

- [Azure Kimlik Doğrulama](../2012/windows-azure-authentication.md)
- [Azure AD'yi Kullanarak Web Uygulamanıza Oturum Açma Ekleme](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory ile ASP.NET Uygulamaları geliştirme](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD ve Microsoft OWIN Bileşenleri ile Web API ASP.NET güvenli](https://msdn.microsoft.com/magazine/dn463788.aspx)

Eğitimler Visual Studio 2013 için henüz güncellenmedi; bazı öğreticiler el ile yapmak için doğrudan Visual Studio 2013 otomatiktir.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Bulut - Çoklu Organizasyon Kimlik Doğrulaması

![Birden çok kuruluş kimlik doğrulaması](creating-web-projects-in-visual-studio/_static/image25.png)

Birden çok Azure AD [kiracısında](https://technet.microsoft.com/library/jj573650.aspx)tanımlanan kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız bu seçeneği belirleyin. Örneğin, site contoso.com ve contoso.onmicrosoft.com kiracı olan Contoso Şirket çalışanları ve fabrikam.onmicrosoft.com kiracı olan Fabrikam Şirket çalışanları için kullanılabilir hale getirilecektir.

Girdiğiniz ayarlar ve uygulama sağlama adımı [tek bir kuruluş kimlik doğrulaması](#orgauthsingle)benzer.

**Bulut - Çoklu Kuruluş** kimlik doğrulaması kullanan uygulamaların nasıl oluşturulacagerektiği hakkında bilgi için aşağıdaki kaynaklara bakın:

- Active Directory Team blogunda [Azure &amp; Active Directory ile Kolay Web Uygulaması Entegrasyonu, ASP.NET Visual Studio.](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)
- [Azure AD öğreticisiyle Çok Kiracılı Web Uygulamaları Geliştirme.](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) Öğretici henüz Visual Studio 2013 için güncellenmedi; öğreticinin sizi el ile yapmaya yönlendiren bazı öğeleri Visual Studio 2013'te otomatiktir.
- [Oturum Açmadan Önce Kendi Çoklu Kuruluşlarınız ASP.NET Uygulamasına Kaydolabilirsiniz.](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/) Vittorio Bertocci tarafından blog nasıl çok organizasyon kimlik doğrulaması kullanan bir proje oluştururken insanların karşılaştığı ortak bir sorun çözmek için açıklar.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Şirket Içi Kurumsal Kimlik Doğrulama

![Şirket içi kuruluş kimlik doğrulaması](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server Active Directory 'de (AD) tanımlanan kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız ve Azure AD'yi kullanmak istemiyorsanız bu seçeneği belirleyin. Bu seçeneği, bir Intranet sitesi veya Internet sitesi oluşturmak için kullanabilirsiniz. Bir Internet sitesi için, AD'ye erişim sağlamak için Active Directory Federation Services 'ı (ADFS) kullanın. Daha fazla bilgi için Visual [Studio 2013'te ASP.NET ile Şirket İçi Kurumsal Kimlik Doğrulama Seçeneğini (ADFS) Kullanın'a](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)bakın.

Bir Intranet sitesi için alternatif olarak bu seçenek yerine [Windows Kimlik Doğrulama'yı](#winauth) seçebilirsiniz. Windows Kimlik Doğrulama seçeneği için meta veri belge URL'si sağlamanız gerekmez. Ancak, Windows Kimlik Doğrulama, Etkin Dizin'de uygulama erişimini denetleme veya dizin verilerini sorgulama olanağı sağlamaz.

#### <a name="on-premises-authority"></a>Şirket Içi Yetki

Meta veri belgesini işaret eden bir URL girin. Meta veri belgesi otoritenin koordinatlarını içerir. Uygulama web oturum açma akışını yönlendirmek için bu koordinatları kullanır.

#### <a name="application-id-uri"></a>Uygulama Kimliği URI

AD'nin bu uygulamayı tanımlamak için kullanabileceği benzersiz bir URI sağlayın veya Visual Studio'nun bir uygulama oluşturmasına izin vermek için boş bırakın.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Sonraki adımlar

Bu belge Visual Studio 2013'te yeni bir ASP.NET web projesi oluşturmak için bazı temel yardım lar sağlamıştır. Web geliştirme için Visual Studio için kullanma [https://www.asp.net/visual-studio/](../../index.md)hakkında daha fazla bilgi için bkz.
