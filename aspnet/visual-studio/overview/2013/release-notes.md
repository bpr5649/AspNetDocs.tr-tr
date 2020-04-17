---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio için ASP.NET ve Web Araçları 2013 Yayın Notları | Microsoft Dokümanlar
author: rick-anderson
description: Bu belge, Visual Studio 2013 için ASP.NET ve Web Araçları'nın yayımlanmasından açıklanmaktadır.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543502"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013 için ASP.NET and Web Tools Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

> Bu belge, Visual Studio 2013 için ASP.NET ve Web Araçları'nın yayımlanmasından açıklanmaktadır.

## <a name="contents"></a>İçindekiler

- [Kurulum Notları](#TOC1)
- [Belgeler](#TOC2)
- [Yazılım Gereksinimleri](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio için ASP.NET ve Web Araçlarında Yeni Özellikler 2013

- [Bir ASP.NET](#TOC6)
- [Yeni Web Proje Deneyimi](#newproj)
- [ASP.NET İskele](#scaffold)
- [Tarayıcı Bağlantısı](#browser-link)
- [Visual Studio Web Editörü Geliştirmeleri](#web-editor)
- [Visual Studio'da Azure App Service Web Apps Desteği](#waws)
- [Web Yayımlama Geliştirmeleri](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Kimlik](#TOC8)
- [Microsoft OWIN Bileşenleri](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Jilet 3](#TOC14)
- [ASP.NET Uygulama Askıya Alma](#TOC15)
- [Bilinen Sorunlar ve Son Dakika Değişiklikleri](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Kurulum Notları

Visual Studio 2013 için ASP.NET ve Web Araçları ana yükleyici de paketlenmiş ve [buradan](https://www.asp.net/downloads)indirebilirsiniz.

<a id="TOC2"></a>
## <a name="documentation"></a>Belgeler

Eğitimler ve Visual Studio 2013 için ASP.NET ve Web Araçları hakkında diğer bilgiler [ASP.NET web sitesinden](https://www.asp.net/)edinilebilir.

<a id="TOC4"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

ASP.NET ve Web Araçları Visual Studio 2013 gerektirir.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio için ASP.NET ve Web Araçlarında Yeni Özellikler 2013

Aşağıdaki bölümlerde sürümde tanıtılan özellikler açıklanmıştır.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Bir ASP.NET

Visual Studio 2013'ün piyasaya sürülmesiyle, ASP.NET teknolojilerini kullanma deneyimini birleştirme yolunda bir adım attık, böylece istediğiniz teknolojileri kolayca karıştırıp eşleştirebilesiniz. Örneğin, MVC kullanarak bir proje başlatabilir ve daha sonra projeye Web Formları sayfalarını kolayca ekleyebilir veya Web Formları projesinde Web API'lerini iskeleye alabilirsiniz. Bir ASP.NET, bir geliştirici olarak sevdiğiniz şeyleri ASP.NET daha kolay hale getirmektir. Hangi teknolojiyi seçerseniz seçin, One ASP.NET'nin güvenilir temel çerçevesi üzerinde inşa ettiğinize güvenebilirsiniz.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Yeni Web Proje Deneyimi

Visual Studio 2013'te yeni web projeleri oluşturma deneyimini artırdık. Yeni **ASP.NET Web Projesi** iletişim kutusunda istediğiniz proje türünü seçebilir, herhangi bir teknoloji birleşimini (Web Forms, MVC, Web API) yapılandırabilir, kimlik doğrulama seçeneklerini yapılandırabilir ve birim test projesi ekleyebilirsiniz.

![Yeni ASP.NET Projesi](release-notes/_static/image1.png)

Yeni iletişim kutusu, şablonların çoğu için varsayılan kimlik doğrulama seçeneklerini değiştirmenizi sağlar. Örneğin, bir ASP.NET Web Formları projesi oluşturduğunuzda aşağıdaki seçeneklerden birini seçebilirsiniz:

- Kimlik Doğrulaması Yok
- Bireysel Kullanıcı Hesapları (ASP.NET üyelik veya sosyal sağlayıcı girişi)
- Kurumsal Hesaplar (Bir internet uygulamasında Aktif Dizin)
- Windows Kimlik Doğrulama (Intranet uygulamasında Etkin Dizin)

![Kimlik doğrulaması seçenekleri](release-notes/_static/image2.png)

Web projeleri oluşturmak için yeni süreç hakkında daha fazla bilgi için Visual [Studio 2013'te ASP.NET Web Projeleri Oluşturma'ya](creating-web-projects-in-visual-studio.md)bakın. Yeni kimlik doğrulama seçenekleri hakkında daha fazla bilgi için, bu belgede daha sonra [ASP.NET Kimliği'ne](#TOC8) bakın.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET İskele

ASP.NET İskele, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Projenize bir veri modeliyle etkileşimde bulunarak ortak kod eklemeyi kolaylaştırır.

Visual Studio'nun önceki sürümlerinde, iskele ASP.NET MVC projeleri ile sınırlıydı. Visual Studio 2013 ile artık Web Formlar da dahil olmak üzere herhangi bir ASP.NET projesi için iskele kullanabilirsiniz. Visual Studio 2013 şu anda bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Formları ile iskeleyi kullanmaya devam edebilirsiniz. Web Formları için sayfa oluşturma desteği gelecekteki bir güncelleştirmede eklenir.

İskele kullanırken, gerekli tüm bağımlılıkların projeye yüklenmesini sağlıyoruz. Örneğin, bir web formları projesi ASP.NETyle başlayıp web API Denetleyicisi eklemek için iskele kullanırsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.

Bir Web Forms projesine MVC iskelesi eklemek için **Yeni İskele Öğesi** ekleyin ve iletişim penceresinde **MVC 5 Bağımlılıkları'nı** seçin. İskele MVC için iki seçenek vardır; Minimal ve Tam. Minimal'i seçerseniz, projenize yalnızca ASP.NET MVC için NuGet paketleri ve referansları eklenir. Tam seçeneği seçerseniz, Bir MVC projesi için gerekli içerik dosyalarının yanı sıra Minimal bağımlılıklar eklenir.

İskele async denetleyicileri desteği, Entity Framework 6'nın yeni async özelliklerini kullanır.

Daha fazla bilgi ve öğreticiler için, [ASP.NET İskele Genel bakınız.](aspnet-scaffolding-overview.md)

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Tarayıcı Bağlantısı – Tarayıcı ve Visual Studio arasındaki SignalR kanalı

Yeni [Tarayıcı Bağlantısı](using-browser-link.md) özelliği, birden fazla tarayıcıyı Visual Studio'ya bağlamanızı ve araç çubuğundaki bir düğmeyi tıklatarak hepsini yenilemenizi sağlar. Mobil emülatörler de dahil olmak üzere geliştirme sitenize birden fazla tarayıcı bağlayabilir ve tüm tarayıcıları aynı anda yenilemek için yenile'yi tıklatabilirsiniz. Browser Link ayrıca geliştiricilerin Tarayıcı Bağlantısı uzantıları nı yazabilmeleri için bir API'yi de ortaya çıkarır.

![](release-notes/_static/image3.png)

Geliştiricilerin Tarayıcı Bağlantısı API'si'nden yararlanmasını sağlayarak, Visual Studio ile bağlı herhangi bir tarayıcı arasındaki sınırları aşan çok gelişmiş senaryolar oluşturmak mümkün olur. Web Essentials, Visual Studio ve tarayıcının geliştirici araçları, mobil emülatörleri uzaktan kontrol etme ve çok daha fazlası arasında entegre bir deneyim oluşturmak için API'den yararlanır.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web Editörü Geliştirmeleri

Visual Studio 2013 web uygulamalarında Razor dosyaları ve HTML dosyaları için yeni bir HTML düzenleyicisi içerir. Yeni HTML düzenleyicisi HTML5 tabanlı tek bir birleşik şema sağlar. Otomatik ayraç tamamlama, jQuery UI ve AngularJS öznitelik IntelliSense, öznitelik IntelliSense Gruplama, KIMLIK ve sınıf adı Intellisense ve daha iyi performans, biçimlendirme ve SmartTags dahil olmak üzere diğer iyileştirmeler vardır.

Aşağıdaki ekran görüntüsü, HTML düzenleyicisinde Bootstrap özniteliği IntelliSense'in kullanılmasını gösterir.

![INtellisense IN HTML düzenleyicisi](release-notes/_static/image4.png)

Visual Studio 2013, hem CoffeeScript hem de DAHA AZ editörler dahili olarak da gelir. LESS editörü CSS editörütüm serin özellikleri ile birlikte gelir ve @import zincirdeki tüm AZ belgeler arasında değişkenler ve mixins için özel Intellisense vardır.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio'da Azure App Service Web Apps Desteği

.NET 2.2 için Azure SDK ile Visual Studio 2013'te, uzak web uygulamalarınızla doğrudan etkileşim kurmak için **Server Explorer'ı** kullanabilirsiniz. Azure hesabınızda oturum açabilir, yeni web uygulamaları oluşturabilir, uygulamaları yapılandırabilir, gerçek zamanlı günlükleri görüntüleyebilirsiniz ve daha fazlasını yapabilirsiniz. SDK 2.2 yayımlandıktan kısa bir süre sonra Azure'da hata ayıklama modunda uzaktan çalıştırabilirsiniz. Azure App Service Web Apps'ın yeni özelliklerinin çoğu, .NET için Azure SDK'nın geçerli sürümüne yüklediğinizde Visual Studio 2012'de de çalışır.

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Azure Uygulama Hizmeti'nde ASP.NET bir web uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio'yu kullanarak Azure Uygulama Hizmeti'ndeki bir web uygulamasını sorun giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web Yayımlama Geliştirmeleri

Visual Studio 2013 yeni ve gelişmiş Web Yayımlama özellikleri içerir. Bunlardan birkaçı şunlardır:

- [Web.config dosya şifrelemeyi](https://go.microsoft.com/fwlink/?LinkId=325529)kolayca otomatikleştirin. (Bu bağlantı ve 10/17 günün geç saatlerine kadar mevcut olmayabilir MSDN belgeleri için aşağıdaki iki nokta.)
- Dağıtım sırasında uygulamayı çevrimdışı naalarak kolayca [otomatikleştirin.](https://go.microsoft.com/fwlink/?LinkId=325530)
- Hangi dosyaların sunucuya kopyalanmasını gerektiğini belirlemek için [son değiştirilen tarih yerine dosya denetimi kullanmak](https://go.microsoft.com/fwlink/?LinkId=325531) üzere Web Dağıtımı'nı yapılandırın.
- FTP veya dosya sistemi yayımlama yöntemlerini kullanırken ve Web Dağıtımı'nda seçili dosyaları (Web.config dahil) hızla yayımlayın.

ASP.NET web dağıtımı hakkında daha fazla bilgi için [ASP.NET sitesine](https://go.microsoft.com/fwlink/?LinkId=322027)bakın.

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7, [NuGet 2.7 Sürüm Notları'nda](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir yeni özellik kümesini içerir.

NuGet'in bu sürümü, Paketleri indirmek için NuGet'in paket geri yükleme özelliği için açık onay sağlama gereksinimini de ortadan kaldırır. NuGet'in kurulumu ile onay (ve NuGet'in tercihleri iletişim kutusundaki ilişkili onay kutusu) verilir. Şimdi paket geri yükleme sadece varsayılan olarak çalışır.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>Bir ASP.NET

Web Formları proje şablonları, yeni One ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir. Web Formları projenize MVC ve Web API desteği ekleyebilir ve One ASP.NET proje oluşturma sihirbazını kullanarak kimlik doğrulamasını yapılandırabilirsiniz. Daha fazla bilgi için Visual [Studio 2013'te ASP.NET Web Projeleri Oluşturma'ya](creating-web-projects-in-visual-studio.md)bakın.

### <a name="aspnet-identity"></a>ASP.NET Kimlik

Web Formları proje şablonları yeni ASP.NET Kimlik çerçevesini destekler. Buna ek olarak, şablonlar artık bir Web Forms intranet projesinin oluşturulmasını destekler. Daha fazla bilgi için Visual **Studio 2013'te ASP.NET Web Projeleri Oluşturmada** [Kimlik Doğrulama Yöntemleri'ne](creating-web-projects-in-visual-studio.md#auth) bakın.

### <a name="bootstrap"></a>Bootstrap

Web Formları şablonları, şık ve duyarlı bir görünüm sağlamak ve kolayca özelleştirebileceğinizi hissetmek için [Bootstrap'ı](http://twitter.github.io/bootstrap/) kullanır. Daha fazla bilgi için [Visual Studio 2013 web proje şablonlarında Bootstrap'a](creating-web-projects-in-visual-studio.md#bootstrap)bakın.

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Bir ASP.NET

Web MVC proje şablonları, yeni One ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir. One ASP.NET proje oluşturma sihirbazını kullanarak MVC projenizi özelleştirebilir ve kimlik doğrulamasını yapılandırabilirsiniz. MVC 5'i ASP.NET için bir giriş eğitimi, [MVC 5'ASP.NET başlarken](../../../mvc/overview/getting-started/introduction/getting-started.md)bulunabilir.

MVC 4 projelerini MVC 5'e yükseltme hakkında bilgi için, [MVC 5 ve Web API 2'yi ASP.NET için ASP.NET MVC 4 ve Web API Projesi'ni nasıl yükseltilir'](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)e bakın.

### <a name="aspnet-identity"></a>ASP.NET Kimlik

MVC proje şablonları kimlik doğrulama ve kimlik yönetimi için kimlik ASP.NET kullanmak üzere güncelleştirildi. Facebook ve Google kimlik doğrulama ve yeni üyelik API içeren bir öğretici [Facebook ve Google OAuth2 ve OpenID Oturum](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) açma ile ASP.NET bir MVC 5 App oluşturun ve [auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve Azure App Service dağıtmak](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)bulunabilir.

### <a name="bootstrap"></a>Bootstrap

MVC proje şablonu, şık ve duyarlı bir görünüm sağlamak ve kolayca özelleştirebileceğinizi hissetmek için [Bootstrap'ı](http://getbootstrap.com/) kullanacak şekilde güncellendi. Daha fazla bilgi için [Visual Studio 2013 web proje şablonlarında Bootstrap'a](creating-web-projects-in-visual-studio.md#bootstrap)bakın.

### <a name="authentication-filters"></a>Kimlik doğrulama filtreleri

Kimlik doğrulama filtreleri, ASP.NET MVC ardışık etki alanında yetkilendirme filtrelerinden önce çalışan ve tüm denetleyiciler için eylem başına, denetleyici başına veya genel olarak kimlik doğrulama mantığı belirtmenize olanak tanıyan ASP.NET MVC'deki yeni bir filtre türüdür. Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve ilgili bir anapara sağlar. Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları da ekleyebilir.

### <a name="filter-overrides"></a>Filtre geçersiz kılar

Artık bir geçersiz kılma filtresi belirterek, belirli bir eylem yöntemine veya denetleyicisine hangi filtrelerin uygulandığını geçersiz kılabilirsiniz. Geçersiz kılma filtreleri, belirli bir kapsam (eylem veya denetleyici) için çalıştırılmaması gereken bir filtre türü kümesi belirtir. Bu, genel olarak uygulanan filtreleri yapılandırmanıza, ancak daha sonra belirli genel filtrelerin belirli eylemlere veya denetleyicilere uygulanmasını hariç tutmanıza olanak tanır.

### <a name="attribute-routing"></a>Öznitelik yönlendirme

ASP.NET MVC şimdi öznitelik yönlendirme destekler, Tim McCall, yazarı [http://attributerouting.net](http://attributerouting.net)tarafından bir katkı sayesinde . Öznitelik yönlendirmesi ile eylemlerinizi ve denetleyicilerinizi açıklamayaparak yollarınızı belirtebilirsiniz.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>Öznitelik yönlendirme

ASP.NET Web API şimdi öznitelik yönlendirme destekler, Tim McCall, yazarı [http://attributerouting.net](http://attributerouting.net)tarafından bir katkı sayesinde . Öznitelik yönlendirmesi ile eylemlerinizi ve denetleyicilerinizi şu şekilde ekleyerek Web API rotalarınızı belirtebilirsiniz:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

Öznitelik yönlendirme, web API'nizdeki URI'ler üzerinde daha fazla denetim sağlar. Örneğin, tek bir API denetleyicisi kullanarak bir kaynak hiyerarşisi kolayca tanımlayabilirsiniz:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

Öznitelik yönlendirme, isteğe bağlı parametreleri, varsayılan değerleri ve rota kısıtlamalarını belirtmek için kullanışlı bir sözdizimi de sağlar:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Öznitelik yönlendirmesi hakkında daha fazla bilgi [için, Web API 2'de Öznitelik Yönlendirme'ye](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)bakın.

### <a name="oauth-20"></a>OAuth 2.0

Web API ve Tek Sayfa uygulaması proje şablonları artık OAuth 2.0 kullanarak yetkilendirmeyi destekliyor. OAuth 2.0, istemcinin korunan kaynaklara erişimini yetkilendirmek için bir çerçevedir. Tarayıcılar ve mobil cihazlar da dahil olmak üzere çeşitli istemciler için çalışır.

OAuth 2.0 desteği, taşıyıcı kimlik doğrulaması ve yetkilendirme sunucusu rolünün uygulanması için Microsoft OWIN Bileşenleri tarafından sağlanan yeni güvenlik ara yazılımlarını temel almaktadır. Alternatif olarak, istemciler Windows Server 2012 R2'de Azure Active Directory veya ADFS gibi bir kuruluş yetkilendirme sunucusu kullanılarak yetkilendirilebilir.

### <a name="odata-improvements"></a>OData Geliştirmeleri

**$select, $expand, $batch ve $value desteği**

ASP.NET Web API OData artık $select, $expand ve $value için tam desteğe sahiptir. Değişiklik kümelerinin istek toplu işlemesi ve işlenmesi için $batch da kullanabilirsiniz.

$select ve $expand seçenekleri, OData bitiş noktasından döndürülen verilerin şeklini değiştirmenize sağlar. Daha fazla bilgi için, [Web API OData'da $select ve $expand desteği tanıtma'ya](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)bakın.

**Geliştirilmiş genişletilebilirlik**

OData formatters artık genişletilebilir. Atom girişi meta verilerini, adı geçen akışı ve medya bağlantısı girişlerini destekleyebilir, örnek ek açıklamalar ekleyebilir ve bağlantıların nasıl oluşturulduğunu özelleştirebilirsiniz.

**Türüz destek**

Artık varlık türleri için CLR türlerini tanımlamaya gerek kalmadan OData hizmetleri oluşturabilirsiniz. Bunun yerine, OData denetleyicileriniz, OData'nın serihale/deserialize edilmesine neden olan **IEdmObject**örneklerini alabilir veya döndürebilir.

**Varolan bir modeli yeniden kullanma**

Zaten varolan bir varlık veri modeli (EDM) varsa, artık yeni bir tane oluşturmak zorunda yerine doğrudan yeniden kullanabilirsiniz. Örneğin, Varlık Çerçevesi kullanıyorsanız, EF'nin sizin için oluşturduğu EDM'yi kullanabilirsiniz.

### <a name="request-batching"></a>İstek Toplu İşlemi

İstek toplu işlemi, ağ trafiğini azaltmak ve daha sorunsuz, daha az geveze bir kullanıcı arabirimi sağlamak için birden çok işlemi tek bir HTTP POST isteğinde birleştirir. ASP.NET Web API şimdi toplu talep için çeşitli stratejileri destekler:

- Bir OData hizmetinin $batch bitiş noktasını kullanın.
- Birden çok isteği tek bir MIME çok parçalı istekte paketle.
- Özel bir toplu işlem biçimi kullanın.

İstek toplu çalışmasını etkinleştirmek için, Web API yapılandırmanıza toplu işleyiciiçeren bir rota eklemeniz yeterlidir:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Ayrıca, isteklerin sırayla mı yoksa herhangi bir sırada mı yürütülmeyeceğini de denetleyebilirsiniz.

### <a name="portable-aspnet-web-api-client"></a>Taşınabilir ASP.NET Web API İstemci

Artık Windows Mağazası ve Windows Phone 8 uygulamalarınızda çalışan taşınabilir sınıf kitaplıkları oluşturmak için ASP.NET Web API İstemcisini kullanabilirsiniz. Ayrıca istemci ve sunucu arasında paylaşılabilir taşınabilir formatters oluşturabilirsiniz.

### <a name="improved-testability"></a>Geliştirilmiş Test Edilebilirlik

Web API 2, API denetleyicilerinizi birleştirmeyi çok daha kolay hale getirir. Api denetleyicinizi istek mesajınız ve yapılandırmanızla anında anında belirtin ve test etmek istediğiniz eylem yöntemini arayın. Bağlantı oluşturma gerçekleştiren eylem yöntemleri için **UrlHelper** sınıfıyla alay etmek de kolaydır.

### <a name="ihttpactionresult"></a>ihttpactionresult

Artık Web API eylem yöntemlerinizin sonucunu kapsüllemek için IHttpActionResult uygulayabilirsiniz. Bir Web API eylem yönteminden döndürülen bir IHttpActionResult, ortaya çıkan yanıt iletisini oluşturmak için ASP.NET Web API çalışma zamanı tarafından yürütülür. Web API uygulamanızın birim testini basitleştirmek için herhangi bir Web API eyleminden bir IHttpActionResult döndürülebilir. Kolaylık sağlamak için, belirli durum kodlarını, biçimlendirilmiş içeriği veya içerik leilgili yanıtları döndürmeye ilişkin sonuçlar da dahil olmak üzere kutunun dışında bir dizi IHttpActionResult uygulaması sağlanır.

### <a name="httprequestcontext"></a>httpRequestContext

Yeni **HttpRequestContext,** isteğe bağlı olan ancak istekten hemen kullanılamayan herhangi bir durumu izler. Örneğin, rota verilerini, istekle ilişkili asıl kaynağı, istemci sertifikasını, **UrlHelper'ı** ve sanal yol kökünü almak için **HttpRequestContext'ı** kullanabilirsiniz. Birim sınama amacıyla kolayca bir **HttpRequestContext** oluşturabilirsiniz.

İsteğin asıllığı **Thread.CurrentPrincipal'a**güvenmek yerine istekle birlikte aktığı ndan, asıl, web API ardışık ardışık ardışık ardışık olduğunda isteğin ömrü boyunca kullanılabilir.

### <a name="cors"></a>CORS

Brock Allen başka bir büyük katkı sayesinde, ASP.NET şimdi tamamen Cross Origin İstek Paylaşımı (CORS) destekler.

Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller. [CORS,](http://www.w3.org/TR/cors/) bir sunucunun aynı orijin ilkesini gevşetmesine olanak tanıyan bir W3C standardıdır. CORS'i kullanan sunucu, diğerlerini reddederken bazı kişiler arası isteklere açıkça izin verebilir.

Web API 2 artık ön kontrol isteklerinin otomatik olarak işlenmesi de dahil olmak üzere CORS'u destekler. Daha fazla bilgi için bkz: [ASP.NET Web API'sinde Başlangıç Lar Arası İstekleri Etkinleştirme.](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)

### <a name="authentication-filters"></a>Kimlik Doğrulama Filtreleri

Kimlik doğrulama filtreleri, ASP.NET Web API ardışık alt etki alanında yetkilendirme filtrelerinden önce çalışan ve tüm denetleyiciler için eylem başına, denetleyici başına veya genel olarak kimlik doğrulama mantığı belirtmenize olanak tanıyan ASP.NET Web API'sinde yeni bir tür filtredir. Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve ilgili bir anapara sağlar. Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları da ekleyebilir.

### <a name="filter-overrides"></a>Filtre Geçersiz Kılar

Artık bir geçersiz kılma filtresi belirterek, belirli bir eylem yöntemine veya denetleyicisine hangi filtrelerin uygulandığını geçersiz kılabilirsiniz. Geçersiz kılma filtreleri, belirli bir kapsam (eylem veya denetleyici) için çalışmaması gereken bir filtre türü kümesi belirtir. Bu, genel filtreler eklemenize olanak tanır, ancak daha sonra bazılarını belirli eylemlerden veya denetleyicilerden hariç tutmanıza olanak tanır.

### <a name="owin-integration"></a>OWIN Entegrasyonu

ASP.NET Web API şimdi tam Olarak OWIN destekler ve herhangi bir OWIN yetenekli ana bilgisayarda çalıştırılabilir. Ayrıca, OWIN kimlik doğrulama sistemiyle tümleştirme sağlayan bir **HostAuthenticationFiltresi** de dahildir.

OWIN tümleştirmesi ile, SignalR gibi diğer OWIN ara yazılımlarıyla birlikte kendi sürecinizde Web API'yi kendi ev sahipliğiyapabilirsiniz. Daha fazla bilgi için, [Web API'ASP.NET Self-Host için OWIN'i kullanın'](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)a bakın.

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET Sinyalci 2.0

Aşağıdaki bölümlerde SignalR 2.0'ın özellikleri açıklayınız.

- [OWIN üzerine inşa edilmiştir](#builtonowin)
- [MapHubs ve MapConnection artık MapSignalR vardır](#MapSignalR)
- [Etki Alanı Arası Destek](#crossdomain)
- [MonoTouch ve MonoDroid ile iOS ve Android desteği](#mobile)
- [Taşınabilir .NET İstemci](#portable)
- [Yeni Self-Host Paketi](#selfhost)
- [Geriye uyumlu sunucu desteği](#backwardcompat)
- [.NET 4.0 için kaldırılan sunucu desteği](#remove40)
- [İstemci ve gruplar listesine ileti gönderme](#messagelist)
- [Belirli bir kullanıcıya ileti gönderme](#sendtouser)
- [Daha iyi hata işleme desteği](#errorhandling)
- [Hub'ların daha kolay birim testi](#unittesting)
- [JavaScript hata işleme](#javascripterror)

Varolan bir 1.x projeyi SignalR 2.0'a yükseltme nin bir örneği için [bkz.](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN üzerine inşa edilmiştir

SignalR 2.0 tamamen [OWIN (.NET için Açık Web Arabirimi)](http://owin.org/)üzerine inşa edilmiştir. Bu değişiklik, SignalR için kurulum işlemini web tarafından barındırılan ve kendi kendine barındırılan SignalR uygulamaları arasında çok daha tutarlı hale getirir, ancak bir dizi API değişikliği de gerektirilmiştir.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs ve MapConnection artık MapSignalR vardır

OWIN standartlarıyla uyumluluk için bu yöntemler in `MapSignalR`adı 'na yeniden verilmiştir. `MapSignalR`parametrelerolmadan adlandırılan tüm hub'lar `MapHubs` (sürüm 1.x'te olduğu gibi) eşlenecektir; tek tek **PersistentConnection** nesnelerini eşlemek için, bağlantı türünü tür parametresi olarak ve bağlantının URL uzantısını ilk bağımsız değişken olarak belirtin.

Yöntem, `MapSignalR` Owin başlangıç sınıfında çağrılır. Visual Studio 2013, Owin başlangıç sınıfı için yeni bir şablon içerir; bu şablonu kullanmak için aşağıdakileri yapın:

1. Projeye sağ tıklayın
2. **Ekle**, **Yeni Öğe'yi seçin...**
3. **Owin Başlangıç sınıf'ı**seçin. Yeni sınıf **Startup.cs.**

Bir **Web uygulamasında,** `MapSignalR` yöntemi içeren Owin başlangıç sınıfı, aşağıda gösterildiği gibi Web.Config dosyasının uygulama ayarları düğümünde bir giriş kullanılarak Owin'in başlangıç sürecine eklenir.

Kendi **kendine barındırılan**bir uygulamada, Başlangıç sınıfı `WebApp.Start` yöntemin tür parametresi olarak geçirilir.

**SignalR 1.x'teki hub'ları ve bağlantıları (bir web uygulamasındaki genel uygulama dosyasından):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2.0'daki hub'ları ve bağlantıları eşleme (Owin Başlangıç sınıfı dosyasından):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

Kendi **kendine barındırılan**bir uygulamada, Başlangıç sınıfı aşağıda `WebApp.Start` gösterildiği gibi yöntemin tür parametresi olarak geçirilir.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Etki Alanı Arası Destek

SignalR 1.x'te, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağı tarafından denetlendi. Bu bayrak hem JSONP hem de CORS isteklerini denetler. Daha fazla esneklik için, tüm CORS desteği SignalR'ın sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının bunu desteklediği algılanırsa hala KORS'u kullanır) ve bu senaryoları desteklemek için yeni OWIN ara yazılımları kullanıma sunulmuştur.

SignalR 2.0'da, istemcide JSONP gerekiyorsa (eski tarayıcılarda etki alanları arası isteklerini desteklemek için), `EnableJSONP` aşağıda `HubConfiguration` gösterildiği `true`gibi nesneüzerinde ayarlayarak açıkça etkinleştirilmesi gerekir. JSONP, CORS'ten daha az güvenli olduğu için varsayılan olarak devre dışı bırakılır.

SignalR 2.0'a yeni CORS ara yazılımını eklemek `Microsoft.Owin.Cors` için, `UseCors` aşağıdaki bölümde gösterildiği gibi kitaplığı projenize ekleyin ve SignalR ara yazılımınızdan önce arayın.

**Projenize Microsoft.Owin.Cors ekleme**: Bu kitaplığı yüklemek için Paket Yöneticisi Konsolunda aşağıdaki komutu çalıştırın:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Bu komut, paketin 2.0.0 sürümünü projenize ekler.

**UseCors'u Arama**

Aşağıdaki kod parçacıkları SignalR 1.x ve 2.0'da etki alanları arası bağlantıların nasıl uygulanacağını gösterir.

**SignalR 1.x'te (genel uygulama dosyasından) etki alanları arası isteklerin uygulanması**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2.0'da etki alanları arası isteklerin uygulanması (C# kod dosyasından)**

Aşağıdaki kod, SignalR 2.0 projesinde CORS veya JSONP'nin nasıl etkinleştirilen gösteriş olduğunu gösterir. Bu kod `Map` örneği, `RunSignalR` `MapSignalR`CORS ara yazılımının yalnızca CORS desteği gerektiren SignalR istekleri için (belirtilen `MapSignalR`yoldaki tüm trafikler yerine . `Map` tüm uygulama yerine belirli bir URL öneki için çalışması gereken diğer ara yazılımlar için de kullanılabilir.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>MonoTouch ve MonoDroid ile iOS ve Android desteği

[Xamarin kütüphanesinden](https://xamarin.com/)MonoTouch ve MonoDroid bileşenleri kullanan iOS ve Android istemcileri için destek eklendi. Bunların nasıl kullanılacağı hakkında daha fazla bilgi için Bkz. [Xamarin Bileşenlerini Kullanma.](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln) SignalR RTW sürümü kullanılabilir olduğunda bu bileşenler [Xamarin Mağazası'nda](https://store.xamarin.com/) kullanılabilir olacaktır.

<a id="portable"></a>### Taşınabilir .NET istemcisi

Platformlar arası geliştirmeyi daha iyi kolaylaştırmak için Silverlight, WinRT ve Windows Phone istemcileri aşağıdaki platformları destekleyen tek bir taşınabilir .NET istemcisiyle değiştirildi:

- NET 4,5
- Silverlight 5
- WinRT (Windows Mağazası Uygulamaları için.NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Yeni Self-Host Paketi

Artık SignalR Self-Host (bir web sunucusunda barındırılmak yerine bir işlem veya başka bir uygulamada barındırılan SignalR uygulamaları) ile başlamayı kolaylaştıran bir NuGet paketi vardır. SignalR 1.x ile oluşturulmuş bir kendi kendine barındıran projeyi yükseltmek için Microsoft.AspNet.SignalR.Owin paketini kaldırın ve Microsoft.AspNet.SignalR.SelfHost paketini ekleyin. Self-host paketi ile başlamak hakkında daha fazla bilgi için, [Bkz. Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Geriye uyumlu sunucu desteği

SignalR'ın önceki sürümlerinde, istemcide ve sunucuda kullanılan SignalR paketinin sürümlerinin aynı olması gerekiyordu. Güncellemesi zor olan kalın istemci uygulamalarını desteklemek için SignalR 2.0 artık eski bir istemciye sahip daha yeni bir sunucu sürümünü kullanmayı destekliyor. **Not: SignalR 2.0, eski sürümlerle oluşturulmuş sunucuları yeni istemcilerle desteklemez.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0 için kaldırılan sunucu desteği

SignalR 2.0,.NET 4.0 ile sunucu birlikte çalışabilirliği için destek düştü. .NET 4.5 SignalR 2.0 sunucuları ile kullanılmalıdır. SignalR 2.0 için bir .NET 4.0 istemcisi hala vardır.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>İstemci ve gruplar listesine ileti gönderme

SignalR 2.0'da, istemci ve grup dislerinin listesini kullanarak ileti göndermek mümkündür. Aşağıdaki kod parçacıkları bunun nasıl yapılacağını gösterir.

**PersistentConnection'ı kullanan istemciler ve gruplar listesine ileti gönderme**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Hub'ları kullanan istemciler ve gruplar listesine ileti gönderme**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Belirli bir kullanıcıya ileti gönderme

Bu özellik, kullanıcıların yeni bir arayüz iUserIdProvider üzerinden bir IRequest'e dayalı kullanıcı Kimliği'nin ne olduğunu belirtmelerine olanak tanır:

**IUserIdProvider arabirimi**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Varsayılan olarak, kullanıcı adı olarak kullanıcının IPrincipal.Identity.Name kullanan bir uygulama olacaktır.

Hub'larda, bu kullanıcılara yeni bir API aracılığıyla ileti gönderebilirsiniz:

**Clients.User API'yi kullanma**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Daha İyi Hata İşleme Desteği

Kullanıcılar artık **hubexception'ı** herhangi bir hub çağırmasından atabilir. **HubException'ın** oluşturucusu bir dize iletisi ve nesne ekstra hata verileri alabilir. SignalR özel durumu otomatik olarak serihale getirir ve hub yöntemi çağırmasını reddetmek/başarısız yapmak için kullanılacağı istemciye gönderir.

**Ayrıntılı hub özel durumları ayarı,** **HubException'ın** istemciye geri gönderilmesi veya gönderilmemesi ile ilgili bir etkiye sahip değildir; her zaman gönderilir.

**İstemciye HubException göndermeyi gösteren sunucu tarafı kodu**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**JavaScript istemci kodu sunucudan gönderilen bir HubException yanıt gösteren**

[!code-html[Main](release-notes/samples/sample16.html)]

**Sunucudan gönderilen HubException'a yanıt veren .NET istemci kodu**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Hub'ların daha kolay birim testi

SignalR 2.0, Hub'larda sahte `IHubCallerConnectionContext` istemci tarafı çağrıları oluşturmayı kolaylaştıran bir arabirim içerir. Aşağıdaki kod parçacıkları popüler test koşumları [xUnit.net](https://github.com/xunit/xunit) ve [moq](https://code.google.com/p/moq/)ile bu arayüzü kullanarak göstermek.

**xUnit.net ile Unit test SignalR**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Birim test SignalR ile moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript hata işleme

SignalR 2.0'da, tüm JavaScript hata işleme geri aramaları ham dizeleri yerine JavaScript hata nesnelerini döndürer. Bu, SignalR'ın hata işleyicilerinize daha zengin bilgiler akışını sağlar. Hata özelliğinden `source` iç özel durum alabilirsiniz.

**Başlat.Başarısız özel durumu işleyen JavaScript istemci kodu**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Kimlik

### <a name="new-aspnet-membership-system"></a>Yeni ASP.NET Üyelik Sistemi

ASP.NET Kimlik ASP.NET başvurular için yeni üyelik sistemidir. ASP.NET Kimlik, kullanıcıya özel profil verilerini uygulama verileriyle tümleştirmeyi kolaylaştırır. ASP.NET Kimlik, uygulamanızdaki kullanıcı profilleri için kalıcılık modelini seçmenize de olanak tanır. Verileri, Azure Depolama Tabloları gibi NoSQL veri depoları da dahil olmak üzere bir SQL Server veritabanında veya başka bir veri deposunda depolayabilirsiniz. Daha fazla bilgi için **Visual Studio 2013'te ASP.NET Web Projeleri Oluştururken** [Bireysel Kullanıcı Hesapları'na](creating-web-projects-in-visual-studio.md#indauth) bakın.

### <a name="claims-based-authentication"></a>Beyana dayalı kimlik doğrulama

ASP.NET artık, kullanıcının kimliğinin güvenilir bir verenden gelen bir talep kümesi olarak temsil edildiği taleplere dayalı kimlik doğrulamasını destekler. Kullanıcılar, bir uygulama veritabanında tutulan bir kullanıcı adı ve parola kullanılarak veya sosyal kimlik sağlayıcıları (örneğin: Microsoft Hesapları, Facebook, Google, Twitter) kullanılarak veya Azure Etkin Dizin veya Active Directory Federation Services (ADFS) aracılığıyla kuruluş hesaplarını kullanarak kimlik doğrulaması yapılabilir.

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory ve Windows Server Active Directory ile Tümleştirme

Artık kimlik doğrulaması için Azure Active Directory veya Windows Server Active Directory (AD) kullanan ASP.NET projeler oluşturabilirsiniz. Daha fazla bilgi için **Visual Studio 2013'te ASP.NET Web Projeleri Oluştururken** [Kuruluş Hesapları'na](creating-web-projects-in-visual-studio.md#orgauth) bakın.

### <a name="owin-integration"></a>OWIN Entegrasyonu

ASP.NET kimlik doğrulaması artık herhangi bir OWIN tabanlı ana bilgisayarda kullanılabilen OWIN ara yazılımlarını temel alınr. OWIN hakkında daha fazla bilgi için aşağıdaki [Microsoft OWIN Bileşenleri](#TOC7) bölümüne bakın.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN Bileşenleri

[.NET](http://owin.org/) için Açık Web Arabirimi (OWIN), .NET web sunucuları ve web uygulamaları arasında bir soyutlama tanımlar. OWIN web uygulamasını sunucudan ayırarak web uygulamalarını ana bilgisayar-agnostik hale getirir. Örneğin, IIS'de OWIN tabanlı bir web uygulamasını barındırabilir veya özel bir işlemle kendi kendine barındırabilirsiniz.

Microsoft OWIN bileşenlerinde (Katana projesi olarak da bilinir) tanıtılan değişiklikler, yeni sunucu ve ana bilgisayar bileşenlerini, yeni yardımcı kitaplıkları ve ara yazılımları ve yeni kimlik doğrulama ara yazılımlarını içerir.

OWIN ve Katana hakkında daha fazla bilgi için, [OWIN ve Katana yenilikleri](../../../aspnet/overview/owin-and-katana/index.md)hakkında bilgi.

**Not: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamaları IIS klasik modunda çalıştırılamaz; entegre modda çalıştırılmalıdır.**

**Not: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamaları tam güven içinde çalıştırılmalıdır.**

### <a name="new-servers-and-hosts"></a>Yeni Sunucular ve Ana Bilgisayarlar

Bu sürümle, kendi kendine barındırış senaryolarını etkinleştirmek için yeni bileşenler eklendi. Bu bileşenler aşağıdaki NuGet paketlerini içerir:

- **Microsoft.Owin.Host.HttpListener**. HTTP isteklerini dinlemek ve bunları OWIN ardışık boru hattına yönlendirmek için **HttpListener'ı** kullanan bir OWIN sunucusu sağlar.
- **Microsoft.Owin.Hosting,** konsol uygulaması veya Windows hizmeti gibi özel bir işlemle bir OWIN ardışık hattını kendi kendine barındırmak isteyen geliştiriciler için bir kitaplık sağlar.
- **OwinHost**. Özel bir ana bilgisayar uygulaması `Microsoft.Owin.Hosting` yazmak zorunda kalmadan bir OWIN ardışık hattını saran ve barındırmanızı sağlayan tek başına çalıştırılabilir bir yürütme sağlar.

Buna ek `Microsoft.Owin.Host.SystemWeb` olarak, paket artık middleware **SystemWeb** sunucusuna ipuçları sağlamak için izin, middleware belirli bir ASP.NET boru hattı aşamasında çağrılması gerektiğini belirten sağlar. Bu özellik, özellikle ASP.NET ardışık çalışması gereken kimlik doğrulama ara ware için yararlıdır.

### <a name="helper-libraries-and-middleware"></a>Yardımcı Kütüphaneler ve Middleware

OWIN belirtiminden yalnızca işlev ve tür tanımlarını kullanarak OWIN `Microsoft.Owin` bileşenleri yazabilirsiniz, ancak yeni paket daha kullanıcı dostu bir soyutlama kümesi sağlar. Bu paket, daha önceki birkaç paketi `Owin.Extensions`(örn. , , ) `Owin.Types`diğer OWIN bileşenleri tarafından kolayca kullanılabilen tek ve iyi yapılandırılmış bir nesne modelinde birleştirir. Aslında, Microsoft OWIN bileşenlerinin çoğu artık bu paketi kullanmaktadır.

> [!NOTE]
> [OWIN](http://www.owin.org) uygulamaları IIS klasik modunda çalıştırılamaz; entegre modda çalıştırılmalıdır.

> [!NOTE]
> [OWIN](http://www.owin.org) uygulamaları tam güven içinde çalıştırılmalıdır.

Bu sürüm, çalışan bir OWIN uygulamasını doğrulamak için ara yazılım ların yanı sıra hataları araştırmaya yardımcı olacak hata sayfası ara yazılımını da içeren Microsoft.Owin.Diagnostics paketini de içerir.

### <a name="authentication-components"></a>Kimlik Doğrulama Bileşenleri

Aşağıdaki kimlik doğrulama bileşenleri kullanılabilir.

- **Microsoft.Owin.Security.ActiveDirectory**. Şirket içi veya bulut tabanlı dizin hizmetlerini kullanarak kimlik doğrulamayı etkinleştirin.
- **Microsoft.Owin.Security.Cookies** tanımlama bilgilerini kullanarak kimlik doğrulamasını sağlar. Bu paket daha `Microsoft.Owin.Security.Forms`önce seçildi.
- **Microsoft.Owin.Security.Facebook,** Facebook'un OAuth tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştiri.
- **Microsoft.Owin.Security.Google,** Google'ın OpenID tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştirir.
- **Microsoft.Owin.Security.Jwt** JWT belirteçleri kullanarak kimlik doğrulamasağlar.
- **Microsoft.Owin.Security.MicrosoftAccount** Microsoft hesaplarını kullanarak kimlik doğrulamasını sağlar.
- **Microsoft.Owin.Security.OAuth**. Taşıyıcı belirteçlerinin doğruluğunu doğrulamak için bir OAuth yetkilendirme sunucusunun yanı sıra ara yazılım sağlar.
- **Microsoft.Owin.Security.Twitter,** Twitter'ın OAuth tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştiri.

Bu sürüm, `Microsoft.Owin.Cors` çapraz kökenli HTTP isteklerini işlemek için ara yazılım içeren paketi de içerir.

> [!NOTE]
> Visual Studio 2013'ün son sürümünde JWT imza desteği kaldırıldı.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Varlık Çerçevesi 6'daki yeni özelliklerin ve diğer değişikliklerin listesi için Entity [Framework Version History](https://msdn.com/data/jj574253)bölümüne bakın.

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Jilet 3

ASP.NET Razor 3 aşağıdaki yeni özellikleri içerir:

- Sekme düzenlemesi için destek. Daha önce, Belgeyi **Biçimlendir** komutu, Visual Studio'da otomatik girintisi ve otomatik biçimlendirme **Sekmeleri Tut** seçeneğini kullanırken doğru çalışmadı. Bu değişiklik, sekme biçimlendirmesi için Razor kodu için Visual Studio biçimlendirmesini düzeltir.
- Bağlantılar oluştururken URL Yeniden Yazma kuralları için destek.
- Güvenlik saydam özniteliği kaldırın.
  > [!NOTE]
  > Bu bir kırılma değişikliğidir ve Razor 3'ün MVC4 ve daha öncekilerle uyumsuz olmasına neden olarak, Razor 2 MVC5 veya MVC5'e karşı derlenen derlemelerle uyumsuzdur.

Visual Studio sabit Razor 3 sorunları 2013 ön sürüm [sürümleriburada](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)bulabilirsiniz .

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET Uygulama Askıya Alma

ASP.NET App Suspend, .NET Framework 4.5.1'de çok sayıda ASP.NET siteyi tek bir makinede barındırmak için kullanıcı deneyimini ve ekonomik modeli kökten değiştiren bir oyun değiştirme özelliğidir. Daha fazla bilgi için, ASP.NET App Askıya Alma [– duyarlı paylaşılan .NET web barındırma](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)bakın.

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen Sorunlar ve Son Dakika Değişiklikleri

Bu bölümde, Visual Studio 2013 için ASP.NET ve Web Araçları'ndaki bilinen sorunlar ve kırılma değişiklikleri açıklanmaktadır.

### <a name="nuget"></a>NuGet

- [Yeni paket geri yükleme SLN dosyayı kullanırken Mono çalışmıyor](https://nuget.codeplex.com/workitem/3596) - yaklaşan nuget.exe indirme ve [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleme sabit olacaktır.
- [Yeni paket geri yükleme Wix projeleri ile çalışmıyor](https://nuget.codeplex.com/workitem/3598) - yaklaşan nuget.exe indirme ve [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleme sabit olacaktır.
- [Otomatik Paket geri yüklemesi bir çözüm klasörü altındaki projelerde çalışmaz](https://nuget.codeplex.com/workitem/3625) – NuGet 2.8'de sabitlenir.

### <a name="aspnet-web-api"></a>ASP.NET Web API'si

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`biz destek `IQueryable<T>` `$select` ve ekledi her zaman `$expand`dönmez .

    Bizim önceki `ODataQueryOptions<T>` örnekler için her zaman `ApplyTo` `IQueryable<T>`gelen dönüş değeri attı . Daha önce desteklediğimiz sorgu seçenekleri (`$filter` `$orderby`, `$skip` `$top`, , ) sorgunun şeklini değiştirmediği için bu daha önce çalıştı. Şimdi biz `$select` destek `$expand` ve geri `ApplyTo` dönüş `IQueryable<T>` değeri her zaman olmayacaktır.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Örnek kodu daha önce kullanıyorsanız, istemci göndermezse `$select` çalışmaya devam `$expand`eder ve . Ancak, desteklemek `$select` istiyorsanız ve `$expand` bu kodu değiştirmek zorunda.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request.Url veya RequestContext.Url toplu iş isteği sırasında geçersizdir**

    Bir toplu işlem senaryosunda, **UrlHelper** **Request.Url** veya **RequestContext.Url'den**erişildiğinde geçersizdir.

    Bu sorun şu anda burada izlenir: [BatchRequestContext.Url toplu istek için null .](http://aspnetwebstack.codeplex.com/workitem/1301)

    Bu sorun için geçici çözüm **UrlHelper**yeni bir örnek oluşturmaktır , aşağıdaki örnekte olduğu gibi:

    **UrlHelper'ın yeni bir örneğini oluşturma**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 ve OrgAuth kullanırken, AntiForgerToken doğrulama yapmak görünümlere sahipseniz, görünüme veri deftere naklettiğinizde aşağıdaki hata yla karşılaşabilirsiniz:

    **Hata**:

    *'/' Uygulamasında Sunucu Hatası.*

    <em>' ' veya<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' ' türü iddiası, sağlanan ClaimsIdentity'de mevcut değildi. Talep tabanlı kimlik doğrulamayla sahteciliğe karşı destek sağlamak için, lütfen yapılandırılan talep sağlayıcısının bu taleplerin her ikisini de oluşturduğu ClaimsIdentity örneklerinde sağladığını doğrulayın. Yapılandırılan talep sağlayıcısı bunun yerine benzersiz bir tanımlayıcı olarak farklı bir talep türü kullanıyorsa, statik özellik AntiForgeryConfig.UniqueClaimTypeIdentifier ayarlayarak yapılandırılabilir.</em>

    **Geçici Çözüm**:

    Düzeltmek için Global.asax'a aşağıdaki satırı ekleyin:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Bu, bir sonraki sürüm için düzeltilecektir.
2. Bir MVC4 uygulamasını MVC5'e yükselttikten sonra, çözümü oluşturun ve başlatın. Aşağıdaki hatayı görmeniz gerekir:

    [A] System.Web.WebPages.Razor.Configuration.HostSection [B]System.Web.WebPages.Razor.Configuration.HostSection için döküm olamaz. A türü 'System.Web.WebPages.Razor' adresinden gelir, Sürüm=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' adresindeki 'Varsayılan'\_konumunda 'C:\windows\Microsoft.Net\assembly\GAC MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0\_\_31bf3856ad364e35\System..WebPages.d.d. B türü 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' bağlamında 'Varsayılan' konumunda 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d 05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.

    Yukarıdaki hatayı düzeltmek için, projenizdeki *tüm* Web.config dosyalarını (Görünümler klasöründekiler dahil) açın ve aşağıdakileri yapın:

   1. "System.Web.Mvc"in "4.0.0.0" sürümünün tüm oluşumlarını "5.0.0.0" olarak güncelleştirin.
   2. "System.Web.Helpers", &quot;System.Web.WebPages and&quot; &quot;System.WebPages.Razor&quot; sürümü "2.0.0.0" tüm oluşumları güncelleme "3.0.0.0"

      Örneğin, yukarıdaki değişiklikleri yaptıktan sonra, derleme bağlamaları aşağıdaki gibi görünmelidir:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 projelerini MVC 5'e yükseltme hakkında bilgi için, [MVC 5 ve Web API 2'yi ASP.NET için ASP.NET MVC 4 ve Web API Projesi'ni nasıl yükseltilir'](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)e bakın.
3. jQuery Unobtrusive Doğrulama ile istemci tarafı doğrulama kullanırken, doğrulama iletisi bazen type='number' olan bir HTML giriş öğesi için yanlıştır. Geçersiz bir sayı girildiğinde, gerekli bir değer için doğrulama hatası ("Yaş alanı gereklidir") geçerli bir sayının gerekli olduğu doğru ileti yerine gösterilir.

    Bu sorun genellikle Oluşturma ve Düzenley görünümleri üzerinde bir tamsayı özelliği olan bir model için iskele kodu ile bulunur.

    Bu sorunu çözmek için düzenleyici yardımcıyı aşağıdakilerden değiştirin:

    `@Html.EditorFor(person => person.Age)`

    Hedef:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 artık kısmi güveni desteklemiyor. MVC veya WebAPI ikililerine bağlanan projeler [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) özniteliğini ve [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) özniteliğini kaldırmalıdır. Bu öznitelikleri kaldırmak aşağıdaki gibi derleyici hataları ortadan kaldırır.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Not, bunun bir yan etkisi olarak aynı uygulamada 4.0 ve 5.0 derlemeleri kullanamazsınız. Hepsini 5.0 olarak güncellemeniz gerekir.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Facebook yetkilendirmeli SPA Şablonu, web sitesi intranet bölgesinde barındırılırken IE'de istikrarsızlığa neden olabilir

SPA şablonu Facebook ile harici oturum açma sağlar. Şablonla oluşturulan proje yerel olarak çalışırken, oturum açma IE'nin çökmesine neden olabilir.

Çözüm:

1. Web sitesini internet bölgesinde barındırın; Veya

2. Senaryoyu IE dışındaki bir tarayıcıda test edin.

### <a name="web-forms-scaffolding"></a>Web Formları İskele

Web Forms İskelesi VS2013'ten kaldırıldı ve Visual Studio için gelecekteki bir güncellemede kullanıma sunulacaktır. Ancak, MVC bağımlılıkları ekleyerek ve MVC için iskele oluşturarak bir Web Forms projesi içinde iskele kullanabilirsiniz. Projeniz Web Formları ve MVC'nin bir birleşimini içerir.

Web Formları projenize MVC eklemek için yeni bir iskele öğesi ekleyin ve **MVC 5 Bağımlılıkları'nı**seçin. Komut dosyaları gibi tüm içerik dosyalarına ihtiyacınız olup olmadığına bağlı olarak Minimal veya Tam'ı seçin. Ardından, MVC için, projenizde görünümler ve denetleyici oluşturacak bir iskele öğesi ekleyin.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC ve Web API İskele - HTTP 404, Bulunamadı hatası

Bir projeye iskeleye ayrılmış bir öğe eklerken bir hatayla karşılaşılırsa, projenizin tutarsız bir durumda kalması mümkündür. İskele olarak yapılan değişikliklerin bazıları geri alınır, ancak yüklenen NuGet paketleri gibi diğer değişiklikler geri alınmaz. Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar iskeledeki öğelerde gezinirken bir HTTP 404 hatası alır.

Geçici çözüm:

- MVC için bu hatayı düzeltmek için yeni bir iskele öğesi ekleyin ve MVC 5 Bağımlılıkları 'nı (Minimal veya Tam) seçin. Bu işlem, projenize gerekli tüm değişiklikleri ekler.
- Web API için bu hatayı düzeltmek için:

  1. WebApiConfig sınıfını projenize ekleyin.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. Global.asax'ta Uygulama\_Başlangıç yönteminde WebApiConfig.Register'ı aşağıdaki şekilde yapılandırın:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
