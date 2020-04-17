---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio için ASP.NET ve Web Araçları 2013.2 Yayın Notları | Microsoft Dokümanlar
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543632"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013 için ASP.NET and Web Tools 2013.2 Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

## <a name="installation-notes"></a>Kurulum Notları

Visual Studio 2013.2 için ASP.NET ve Web Araçları ana yükleyici de paketlenmiş ve [Visual Studio 2013 Güncelleme 2](https://go.microsoft.com/fwlink/?LinkId=390521)bir parçası olarak indirilebilir .

## <a name="documentation"></a>Belgeler

Öğreticiler ve Visual Studio 2013.2 için ASP.NET ve Web Araçları hakkında diğer bilgiler [ASP.NET web sitesinden](https://www.asp.net/)edinilebilir.

## <a name="software-requirements"></a>Yazılım Gereksinimleri

Visual Studio 2013.2 için ASP.NET ve Web Araçları Visual Studio 2013 gerektirir.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio için ASP.NET ve Web Araçlarında Yeni Özellikler 2013.2

Aşağıdaki bölümlerde sürümde tanıtılan özellikler açıklanmıştır.

- [Bir ASP.NET Proje Şablonları](#oneaspnet)
- [IIS Express'te Web Uygulamaları başlatılırken SSL'yi destekleyin](#ssl)
- [Visual Studio Web Editörü Geliştirmeleri](#vswebeditor)
- [Tarayıcı Bağlantısı](#browserlink)
- [Visual Studio'da Azure App Service Web Apps desteği](#waws)
- [Yeni bir Web projesi oluştururken uzak Azure kaynakları oluşturma](#AzureResources)
- [Web Yayımlama Geliştirmeleri](#webpublish)
- [ASP.NET İskele](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET Web Sayfaları 3.1.2](#webpages)
- [Varlık Çerçevesi 6.1](#ef)
- [ASP.NET Kimliği 2.0.0](#identity)
- [Microsoft OWIN bileşenleri](#owin)
- [ASP.NET Sinyalci 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Bir ASP.NET Proje Şablonları

- Hesap onayı ve Parola Sıfırlama'yı desteklemek için proje şablonlarını ASP.NET güncelleştirmeleri.
- Şirket Içi Kuruluş Hesaplarını kullanarak kimlik doğrulamayı desteklemek için web API şablonunu ASP.NET güncelleştirin.
- ASP.NET SPA şablonu artık MVC ve sunucu yan görünümlerini temel alan kimlik doğrulaması içerir. Şablonda yalnızca kimlik doğrulaması yapılan kullanıcılar tarafından erişilebilen bir WebAPI denetleyicisi vardır.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express'te Web Uygulamaları başlatılırken SSL'yi destekleyin

Localhost'ta HTTPS'ye göz atarken ve hata ayıklarken güvenlik uyarısını ortadan kaldırmak için, Internet Explorer ve Chrome'un kendi imzaladığı IIS express SSL sertifikasına güvenmesine olanak tanıyan bir iletişim kutusu ekledik.

Örneğin, bir web proje özelliği SSL kullanmak için ayarlanabilir. Özellikler iletişim kutusunu açmak için F4'e tıklayın. **SSL'yi** değiştirin Etkin true. SSL URL'sini kopyalayın.

![SSL Etkin Özellik](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS tabanlı URL'yi kullanacak şekilde web projesi özelliği sayfası web `https://localhost:44300/` sekmesini ayarlayın (SSL WEB Sitelerini daha önce oluşturmadığınız sürece SSL URL'si olacaktır.)

![Proje URL'si (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Uygulamayı çalıştırmak için CTRL+F5'e basın. IIS Express'in oluşturduğu kendi imzalı sertifikaya güvenmek için yönergeleri izleyin.

![SSL Uyarısı](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Güvenlik **Uyarısı** iletişim kutusunu okuyun ve localhost'u temsil eden sertifikayı yüklemek istiyorsanız **Evet'i** tıklatın.

![Güvenlik Uyarısı](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Site, tarayıcıda sertifika uyarısı olmadan IE veya Chrome'da gösterilir.

![Uyarı olmadan HTTPS sayfası](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web Editörü Geliştirmeleri

- **Yeni JSON proje öğesi ve editörü**: Visual Studio'ya bir JSON proje öğesi ve editörü ekledik. Geçerli JSON düzenleyici özellikleri renklendirme, sözdizimi doğrulama, ayraç tamamlama, anahat, araçlar seçeneği ayarı ve daha fazlasını içerir.

    ![JSON Editörü](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense şimdi [JSON Schema](http://json-schema.org/) v3 ve v4 destekler. Varolan şemaları seçmek, yerel şema yolunu düzenlemesi veya göreli yolu almak için bir proje JSON dosyasını sürükleyin.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON Schema editörü](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Yeni Sass (SCSS) editörü**: VS2013 RTM'ye DAHA AZ ekledik ve şimdi bir Sass proje öğesi ve editörüvar. Sass düzenleyici özellikleri LESS düzenleyici karşılaştırılabilir ve renklendirme, değişken ve Mixins IntelliSense, yorum / uncomment, hızlı bilgi, biçimlendirme, sözdizimi doğrulama, anahat, goto tanımı, renk seçici, araçlar seçenek ayarı vb içerir.

    ![Yeni Öğe Ekle: SCSS Stil Sayfası](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Stil sayfası düzenleyicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML, Razor, CSS, LESS ve Sass belgelerinde yeni URL Seçici:** VS 2013, Web Formları sayfaları dışında URL seçici olmadan gönderilir. HTML, Razor, CSS, LESS ve Sass editörleri için yeni URL seçici anlayan bir iletişim ücretsiz, akıcı yazma seçici '..' ve img etiketleri ve bağlantıları için uygun dosya listelerini filtreler.

    ![Resim etiketi için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Görünümler için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Daha fazla özellik ekleyerek LESS düzenleyicisine güncelleştirmeler**
- **Knockout Intellisense Yükseltme**: Biz VS intelliSense için standart olmayan knockout sözdizimi eklendi, "ko-vs-editor viewModel:" sözdizimi. Formdaki yorumları kullanarak bir sayfadaki birden çok görüntüleme modeline bağlamak için kullanılabilir:

    ![Nakavt Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    İç içe görünüm Görünümü IntelliSense için destek de ekledik, böylece ViewModel'de derin iç içe olmuş nesneleri delebilirsiniz.

    `<div data-bind="text: foo.bar.baz.etc" />`

    Görüntülenen IntelliSense, JavaScript Nesnesinin tam IntelliSense'idir.

    ![Tam JavaScript nesnesi gösteren Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML, Razor, CSS, LESS ve Sass belgelerinde yeni URL Seçici**: VS 2013, Web Formları sayfaları dışında URL seçici olmadan gönderilir. HTML, Razor, CSS, LESS ve Sass editörleri için yeni URL seçici anlayan bir iletişim ücretsiz, akıcı yazma seçici '..' ve img etiketleri ve bağlantıları için uygun dosya listelerini filtreler.

    ![Resim etiketi için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Görünümler için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS için URL Seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Tarayıcı Bağlantısı

- Tarayıcı Bağlantısı artık HTTPS bağlantılarını destekler ve sertifika tarayıcı tarafından güvenilen sürece panoda diğer bağlantılarla birlikte bunu listeleyecektir.
- Statik HTML kaynak eşleme
- Veri eşleme için SPA desteği
- Haritalama verilerini otomatik güncelleştirme

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio'da Azure App Service Web Apps desteği

- **Azure oturum aç'ı destekleyin.**
- **Web uygulamaları için uzaktan hata ayıklama ve Uzaktan Görünüm**: Azure [Uygulama Hizmeti'ndeki web uygulamaları için uzaktan hata ayıklama](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) ve sunucu gezginindeki web uygulaması içerik dosyalarının uzaktan görünümünü destekliyoruz.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Yeni bir Web projesi oluştururken uzak Azure kaynakları oluşturma

Yeni web uygulaması iletişim kutusuna bir Azure ["Uzak Kaynaklar Oluştur"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) onay kutusu ekledik. Bunu seçerek, yeni bir web uygulaması oluşturma, Azure yayımlama sitesini sınama için ayarlama ve birkaç basit adımda yayımlama profili oluşturma deneyimini entegre edebilirsiniz.

![Azure kaynaklarıyla Yeni Proje](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure’da yayımlama](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web Yayımlama Geliştirmeleri

- Yayımlama için Kullanıcı deneyimini geliştirin.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET İskele

- **Enum desteği:** Modeliniz Enums kullanıyorsa, MVC İskelesi Enum için açılır bırakma oluşturur. Bu, MVC'deki Enum yardımcılarını kullanır.
- **Bootstrap desteği**: Bootstrap sınıflarını kullanmaları için MVC İskelesi'ndeki EditorFor şablonlarını güncelledi.
- **Paket desteği**: MVC ve Web API İskeleleri MVC ve Web API'leri için 5,1 paket ekleyecektir

Aşağıdaki ekran görüntüleri iskele modellerini göstermektedir.

- Model kodu:

     ![Model kodu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Model kodunu derleyin, sağ tıklatın ve **Ekle**, **Yeni İskele Öğesi'ni**seçin.

     ![Yeni İskele Öğesi Ekle](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **Entity Framework'u kullanarak görünümli MVC5 Denetleyicisini**seçin:

     ![Görünümli yeni MVC5 denetleyicisi ekleme](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- Modeli kullanarak **Denetleyici Ekle:**

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Oluşturulan kodu kontrol edin, örneğin Görünümler/WeekdayModels/Edit.cshtml içerir `@Html.EnumDropDownListFor`: ![EnumDropDownListFor içeren görünüm](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- Oluşturulan enum combobox görmek için sayfayı çalıştırın, bir değer null olabilir, boş bir dize açılan kutusu için seçilebilir unutmayın. Örneğin, **Oluştur** sayfası aşağıdakileri gösterir:

    ![Boş dize izin açılan kutu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM Nisan 2014'te piyasaya sürülecek. Burada sürüm notları göze çarpan noktaları, ancak bu değişiklikler hakkında daha fazla bilgi için [tam sürüm notları](http://docs.nuget.org/docs/release-notes/nuget-2.8) kontrol edin.

- **Hedef Windows Phone 8.1 Uygulamaları**: NuGet 2.8.1 artık windows phone 8.1 uygulamalarını hedeflemeyi destekler, hedef çerçeve monikers 'WindowsPhoneApp', 'WPA', 'WindowsPhoneApp81', ve 'WPA81'.

- **Bağımlılıklar için Yama Çözümü**: Paket bağımlılıklarını çözerken, NuGet tarihsel olarak pakete olan bağımlılıkları karşılayan en düşük ana ve küçük paket sürümünü seçme stratejisini uygulamıştır. Ancak, büyük ve küçük sürümün aksine, yama sürümü her zaman en yüksek sürüme göre çözüldü. Davranış iyi niyetli olmasına rağmen, bağımlılıkları olan paketleri yüklemek için determinizm eksikliği yarattı.
- **DependencyVersion Switch**: NuGet 2.8 bağımlılıkları çözmek için *varsayılan* davranışı değiştirse de, paket yöneticisi konsolundaki -DependencyVersion anahtarı aracılığıyla bağımlılık çözümlemesi işlemi üzerinde daha hassas denetim ekler. Anahtar, olası en düşük sürüme (varsayılan davranış), mümkün olan en yüksek sürümveya en yüksek küçük veya yama sürümüne olan bağımlılıkları çözmeyi sağlar. Bu anahtar yalnızca powershell komutundaki yükleme paketi için çalışır.
- **DependencyVersion Özniteliği**: Yukarıda ayrıntılı olarak ayrıntılı -DependencyVersion anahtarına ek olarak, NuGet, yükleme paketinin bir çağrısında -DependencyVersion anahtarı belirtilmemişse, varsayılan değerin ne olduğunu tanımlayan nuget.config dosyasında yeni bir öznitelik ayarlama olanağıda da izin ver. Bu değer, herhangi bir yükleme paketi işlemleri için NuGet Paket Yöneticisi İletişim Kutusu tarafından da saygı duyulacaktır. Bu değeri ayarlamak için nuget.config dosyanıza aşağıdaki özniteliği ekleyin:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Önizleme NuGet İşlemleri Ile -WhatIf**: Bazı NuGet paketleri derin bağımlılık grafikleri olabilir ve bu nedenle, ilk olarak ne olacağını görmek için bir yükleme, kaldırma veya güncelleştirme işlemi sırasında yararlı olabilir. NuGet 2.8 standart PowerShell ekler -ya yükleme paketi, kaldır-paket ve güncelleme paketi komutları geçiş komutu uygulanacak paketlerin tüm kapatma görselleştirme sağlamak için.
- **Downgrade Paketi**: Yeni özellikleri araştırmak ve daha sonra son kararlı sürüme geri dönmeye karar vermek için bir paketin yayın öncesi sürümünü yüklemek nadir değildir. NuGet 2.8'den önce, bu, yayın öncesi paketi ve bağımlılıklarını kaldırma ve önceki sürümü yükleme çok adımlı bir işlemdi. Ancak NuGet 2.8 ile güncelleştirme paketi artık tüm paket kapanışını (örn. paketin bağımlılık ağacı) önceki sürüme geri alacaktır.
- **Geliştirme Bağımlılıkları**: Geliştirme sürecini optimize etmek için kullanılan araçlar da dahil olmak üzere, NuGet paketleri olarak birçok farklı türde yetenek teslim edilebilir. Bu bileşenler, yeni bir paket geliştirmede etkili olsalar da, daha sonra yayımlandığında yeni paketin bağımlılığı olarak kabul edilmemelidir. NuGet 2.8, bir paketin .nuspec dosyasında kendisini geliştirmeBağımlılık olarak tanımlamasını sağlar. Yüklendiğinde, bu meta veriler paketin yüklendiği projenin packages.config dosyasına da eklenir. Bu packages.config dosyası daha sonra nuget.exe paketi sırasında NuGet bağımlılıkları için analiz edildiğinde, geliştirme bağımlılıkları olarak işaretlenmiş bu bağımlılıkları hariç tutar.
- **Farklı Platformlar için Tek tek paketler.config Files**: Birden çok hedef platform için uygulama geliştirirken, ilgili yapı ortamlarının her biri için farklı proje dosyaları olması yaygındır. Paketler farklı platformlar için farklı düzeyde destek düzeyleri olduğundan, farklı proje dosyalarında farklı NuGet paketleri tüketmek de yaygındır. NuGet 2.8 farklı platforma özgü proje dosyaları için farklı paketler.config dosyaları oluşturarak bu senaryo için geliştirilmiş destek sağlar.
- **Yerel Önbelleğe Geri Dönüş**: NuGet paketleri genellikle ağ bağlantısı kullanarak [NuGet galerisi](http://www.nuget.org) gibi uzak bir galeriden tüketilse de, istemcinin bağlı olmadığı birçok senaryo vardır. Ağ bağlantısı olmadan, NuGet istemcisi paketleri yerel NuGet önbelleğinde müşterinin makinesinde olsa bile başarılı bir şekilde yükleyemedi. NuGet 2.8, paket yöneticisi konsoluna otomatik önbellek geri dönüşünü ekler.

    Önbellek geri dönüş özelliği belirli bir komut bağımsız değişkeni gerektirmez. Ayrıca, önbellek geri dönüş şu anda yalnızca paket yöneticisi konsolunda çalışır - davranış şu anda paket yöneticisi iletişim kutusunda çalışmıyor.
- **Hata Düzeltmeleri**: Yapılan en önemli hata düzeltmelerinden biri, güncelleştirme paketi yeniden yükleme komutundaki performans iyileştirmesiydi.

    Bu özelliklere ve söz konusu performans düzeltmesine ek olarak, NuGet'in bu sürümü diğer birçok hata düzeltmesini de içerir. Sürümde ele alınacak toplam 181 sorun vardı. NuGet 2.8'de sabitlenmiş iş öğelerinin tam listesi için lütfen bu sürüm için [NuGet Issue Tracker'ı](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) görüntüleyin.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web Formları şablonları artık ASP.NET Kimlik için Hesap Onayı ve Parola Sıfırlama'nın nasıl yapılacağını gösterir.
- Varlık Veri Kaynağı denetimi ve Varlık Çerçevesi 6 için Dinamik Veri Sağlayıcısı. Daha fazla bilgi için lütfen aşağıdaki MSDN bloguna bakın: [Dinamik Veri sağlayıcısı ve Entity Framework 6 için EntityDataSource denetimi.](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Öznitelik Yönlendirme Geliştirmeleri](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Editör şablonları için Bootstrap desteği](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Görünümlerde Enum desteği](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [MinLength/ MaxLength öznitelikleri için göze batmaz destek](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Mütevazı Ajax'ta 'bu' bağlamı desteklemek](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [Genel hata işleme](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Öznitelik yönlendirme geliştirmeleri](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Yardım sayfası geliştirmeleri](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [Route desteğini Yoksay](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON ortam tipi formatter](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Async filtreler için daha iyi destek](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [İstemci biçimlendirme kitaplığı için ayrıştma sorgusu](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Sayfaları 3.1.2

- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Varlık Çerçevesi 6.1

Varlık Çerçevesi, hem çalışma zamanı hem de takım için sürüm 6.1 olarak güncelleştirildi. Varlık Çerçevesi (EF) 6.1, Entity Framework 6 için küçük bir güncelleştirmedir ve bir dizi hata düzeltmesi ve yeni özellikler içerir. EF6.1 hakkında, yeni özellikler için belgelere bağlantılar da dahil olmak üzere ayrıntılı bilgi için Entity [Framework Version History'ye](https://msdn.microsoft.com/data/jj574253)bakın. Bu sürümdeki yeni özellikler şunlardır:

- **Takım birleştirme konsolidasyonu,** yeni bir EF modeli oluşturmak için tutarlı bir yol sağlar. Bu özellik, varolan bir veritabanından ters mühendislik de dahil olmak üzere Code First modellerini oluşturmayı desteklemek için ADO.NET Varlık Veri Modeli sihirbazını genişletir. Bu özellikler daha önce EF Power Tools'ta Beta kalitesinde mevcuttü.
- **İşlem commit hatalarının işlenmesi,** yeni tanıtılan işlem işlemlerini engelleme yeteneğinden yararlanan yeni [System.Data.Entity.Infrastructure.CommitFailureHandler'ı](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) sağlar. **CommitFailureHandler,** bir işlem yaparken bağlantı hatalarından otomatik olarak kurtarma sağlar.
- **IndexAttribute,** Code First modelinizdeki bir özellik (veya özellik) üzerine bir öznitelik yerleştirerek dizinlerin belirtilmesine olanak tanır. Önce Kod Veritabanında karşılık gelen bir dizin oluşturur.
- **Genel eşleme API'si,** EF'nin özelliklerin ve türlerin veritabanındaki sütunlara ve tablolara nasıl eşlendirildiklerine ilişkin bilgilere erişim sağlar. Geçmiş sürümlerde bu API dahili oldu.
- **App/Web.config dosyası üzerinden önleyicileri yapılandırabilme**(uygulama yeniden derlemeden engelleyicilerin eklenmesine izin verme).
- **DatabaseLogger,** tüm veritabanı işlemlerini bir dosyaya kaydetmeyi kolaylaştıran yeni bir engelleyicidir. Önceki özellik ile birlikte, bu kolayca yeniden derlemek gerek kalmadan, dağıtılan bir uygulama için veritabanı işlemleri günlüğe geçiş yapmanızı sağlar.
- **Geçişler modeli değişikliği algılaması,** iskeleli geçişlerin daha doğru olması için geliştirilmiştir; değişim algılama sürecinin performansı da büyük ölçüde artırılmıştır.
- Başlatma sırasında azaltılmış veritabanı işlemleri, LINQ sorgularında null eşitlik karşılaştırması için optimizasyonlar, daha fazla senaryoda daha hızlı görünüm oluşturma (model oluşturma) ve birden çok ilişkilendirme ile izlenen varlıkların daha verimli somutlaştırılması dahil performans **geliştirmeleri.**

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Kimliği 2.0.0

- **İki faktörlü kimlik doğrulama:** ASP.NET Identity artık iki faktörlü kimlik doğrulamasını destekler. İki faktörlü kimlik doğrulama, parolanızın ele geçirildiği durumlarda kullanıcı hesaplarınız için ek bir güvenlik katmanı sağlar. Ayrıca iki faktör koduna karşı kaba kuvvet saldırıları için koruma vardır.
- **Hesap Kilitleme:** Kullanıcı parolasını veya iki faktörlü kodlarını yanlış girerse, kullanıcıyı kilitlemenin bir yolunu sağlar. Geçersiz deneme sayısı ve kullanıcıların kilitlenme zaman ları yapılandırılabilir. Bir geliştirici, ihtiyaç duyulması halinde belirli kullanıcı hesapları için Hesap Kilitleme'yi isteğe bağlı olarak kapatabilir.
- **Hesap Onayı:** kimlik ASP.NET artık Hesap Onayı'nı destekler. Bu, web sitesinde yeni bir hesap için kayıt olduğunuzda, web sitesinde bir şey yapmadan önce e-posta onaylamak için gerekli olan çoğu web sitelerinde bugün oldukça yaygın bir senaryodur. Sahte hesapların oluşturulmasını önlediği için e-posta onayı yararlıdır. Bu, e-postayı forum siteleri, bankacılık, e-ticaret veya sosyal web siteleri gibi web sitenizin kullanıcılarıyla iletişim kurma yöntemi olarak kullanıyorsanız son derece yararlıdır.
- **Parola Sıfırlama:** Parola Sıfırlama, kullanıcının parolalarını unuttuğu nda parolalarını sıfırlayabildiği bir özelliktir.
- **Güvenlik Damgası (Her yerde oturum açın):** Kullanıcı'nın parolasını değiştirdiği durumlarda veya ilişkili bir girişi kaldırma gibi güvenlikle ilgili diğer bilgilerde (Facebook, Google, Microsoft Hesabı vb.) Kullanıcı için Güvenlik Belirteci'ni yeniden oluşturmanın bir yolunu destekler. Bu, eski parolayla oluşturulan belirteçlerin geçersiz kılındığından emin olmak için gereklidir. Örnek projede, kullanıcının parolasını değiştirirseniz, kullanıcı için yeni bir belirteç oluşturulur ve önceki belirteçler geçersiz kılınır. Bu özellik, parolanızı değiştirdiğinizde, bu uygulamaya giriş yaptığınız her yerden (diğer tüm tarayıcılardan) oturumunuz kapatılacağınızdan, uygulamanız için ek bir güvenlik katmanı sağlar.
- **Birincil Anahtar türünü Kullanıcılar ve Roller için genişletilebilir hale getirin**: kimlik 1.0 ASP.NET, tablo Kullanıcıları ve Roller için birincil anahtar türü dizeleri oldu. Bu, ASP.NET Kimlik sistemi ENTITY Framework kullanılarak SQL Server'da kalıcı olduğunda nvarchar kullandığımız anlamına gelir. Stack Overflow'daki bu varsayılan uygulama yla ilgili ve gelen geri bildirimlere dayalı birçok tartışma vardı. Kullanıcı ve Roller tablonuzun birincil anahtarının ne olması gerektiğini belirtebileceğiniz bir genişletilebilirlik kancası sağladık. Bu genişletilebilirlik kancası özellikle uygulamanızı geçiriyorsanız ve uygulama UserId'leri depolarken GUI veya ints'si yseniz kullanışlıdır.
- **Kullanıcılar ve Roller Üzerinde Destek IQueryable**: UsersStore ve RolesStore iQueryable için destek eklendi, kolayca Kullanıcı ve Roller listesini alabilirsiniz.
- **UserManager aracılığıyla Destek Silme işlemi**
- **Kullanıcı Adı Üzerinde Dizin Oluşturma**: ASP.NET Kimlik Varlık Çerçevesi uygulamasında, EF 6.1.0'daki yeni IndexAtöz özniteliğini kullanarak Kullanıcı Adına benzersiz bir dizin ekledik. Bu, Kullanıcı Adlarının her zaman benzersiz olmasını ve yinelenen kullanıcı adlarıyla sonuçlanabileceğiniz bir yarış koşulu olmadığından emin olmasını sağlar.
- **Geliştirilmiş Şifre Doğrulayıcısı:** kimlik 1.0 ASP.NET gönderilen parola doğrulayıcısı, yalnızca minimum uzunluğu doğrulayan oldukça temel bir parola doğrulayıcısıydı. Parolanın karmaşıklığı üzerinde daha fazla denetim sağlayan yeni bir parola doğrulayıcısı vardır. Bu paroladaki tüm ayarları açsanız bile, kullanıcı hesapları için iki faktörlü kimlik doğrulamasını etkinleştirmenizi öneririz.
- **IdentityFactory Middleware/ CreatePerOwinContext**:

    - **Kullanıcı Yöneticisi**: OWIN bağlamından UserManager'ın bir örneğini almak için Fabrika uygulamasını kullanabilirsiniz. Bu desen, SignIn ve SignOut için OWIN bağlamından AuthenticationManager almak için kullandığımız benzer. Bu, uygulama isteği başına UserManager'ın bir örneğini almanın önerilen bir yoludur.
    - **DbContextFactory**: ASP.NET Identity, SQL Server'da Kimlik sistemini sürdürmek için Entity Framework'ü kullanır. Bunu yapmak için Kimlik Sistemi ApplicationDbContext bir referans vardır. DbContextFactory Middleware, uygulamanızda kullanabileceğiniz istek başına ApplicationDbContext'ın bir örneğini döndürür.
- **ASP.NET Kimlik Örnekleri NuGet paketi**: Örnekler NuGet paketi, ASP.NET Kimlik için numunelerin yüklenmesini ve çalıştırmasını ve en iyi uygulamaları takip etmesini kolaylaştırabilir. Bu, MVC uygulaması ASP.NET bir örnektir. Bunu üretime dağıtmadan önce lütfen kodu uygulamanıza uyacak şekilde değiştirin. Örnek boş bir ASP.NET uygulamasına yüklenmelidir. Paket hakkında daha fazla bilgi için aşağıdaki blog yazısına gidin: [ASP.NET Identity 2.0.0 RTM duyurusu](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN bileşenleri

Bu sürümde düzeltilen bir sürü hata vardı. Daha ayrıntılı bilgi [için lütfen 2.1.0 sürümü için sürüm notlarına](https://katanaproject.codeplex.com/releases/view/113281) bakın.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET Sinyalci 2.0.2

Bu sürümde düzeltilen bir sürü hata vardı. Daha ayrıntılı bilgi [için lütfen 2.0.2 sürümü için sürüm notlarına](https://github.com/SignalR/SignalR/releases/tag/2.0.2) bakın.
