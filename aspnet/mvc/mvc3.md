---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (Nisan 2011 Araçları Güncelleştirmesi içerir) ASP.NET MVC 3, köklü tasarım deseni kullanarak ölçeklenebilir, standartlara dayalı web uygulamaları oluşturmak için bir çerçevedir...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675134"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(Nisan 2011 Araçları Güncelleştirmesi içerir)*
> 
> ASP.NET MVC 3, köklü tasarım kalıpları ve ASP.NET ve .NET Framework'ün gücünü kullanarak ölçeklenebilir, standartlara dayalı web uygulamaları oluşturmak için bir çerçevedir.
> 
> Bu ASP.NET MVC 2 ile yan yana yükler, bu yüzden bugün kullanmaya başlayın!
> 
> [Yükleyiciyi buradan](https://microsoft.com/download/details.aspx?id=4211) indirin

## <a name="top-features"></a>En İyi Özellikler

- NuGet ile genişletilebilir entegre İskele sistemi
- HTML 5 etkin proje şablonları
- Yeni Razor View Engine dahil Etkileyici Görünümler
- Bağımlılık Enjeksiyonu ve Küresel İşlem Filtreleri ile güçlü kancalar
- Göze çarpmadan JavaScript, jQuery Doğrulama ve JSON bağlama ile zengin JavaScript desteği
- *[Aşağıdaki](#overview) tam özellik listesini okuyun*

## <a name="top-links"></a>En İyi Linkler

ASP.NET MVC 3'te Yenilikler

- Phil Haack: [ASP.NET MVC 3 Çıktı](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express ve Orchard yayınlandı - Microsoft Ocak Web Yayını Bağlamında](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [mvc 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix ASP.NET yayın Duyurusu](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [mvc 3 ASP.NET için Yayın Notları](../whitepapers/mvc3-release-notes.md)

Kurulum ve Yardım

- [Web Platform Yükleyicisini](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3) kullanarak MVC 3 ASP.NET yükleyin (önerilir)
- [Yükleyici çalıştırılabilir](https://go.microsoft.com/fwlink/?LinkID=208140) kullanarak mvc 3 ASP.NET yükleyin
- [Visual Studio 11 Geliştirici Önizleme için MVC 3 ASP.NET](https://go.microsoft.com/fwlink/?LinkID=208140) yükleyin
- [MVC 3 öğretici ASP.NET Intro](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) okuyun
- Yardım alın ve [forumlarda](https://forums.asp.net/1146.aspx) MVC 3 ASP.NET tartışın

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Genel Bakış

ASP.NET MVC 3, hem kodunuzu basitleştiren hem de daha derin genişletilebilirlik sağlayan harika özellikler ekleyerek mvc 1 ve 2'ASP.NET oluşturur. Bu konu, aşağıdaki bölümlerde düzenlenen bu sürümde yer alan yeni özelliklerin birçoğuna genel bir bakış sağlar:

- [MvcScaffold entegrasyonu ile Genişletilebilir İskele](#BM_MvcScaffolding)
- [HTML 5 etkin proje şablonları](#BM_HTML5)
- [Jilet Görünümü Motoru](#BM_TheRazorViewEngine)
- [Çoklu Görünüm Motorları için Destek](#BM_Support_for_Multiple_View_Engines)
- [Denetleyici Geliştirmeleri](#BM_Controller_Improvements)
- [JavaScript ve Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Model Doğrulama Geliştirmeleri](#BM_Model_Validation_Improvements)
- [Bağımlılık Enjeksiyon Iyileştirmeler](#BM_Dependency_Injection_Improvements)
- [Diğer Yeni Özellikler](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold entegrasyonu ile Genişletilebilir İskele

Yeni İskele sistemi, çerçevede tamamen yeniyseniz, hızlı bir şekilde ele alıp verimli bir şekilde kullanmaya başlamanızı ve deneyimliyseniz ve ne yaptığınızı zaten biliyorsanız ortak geliştirme görevlerini otomatikleştirmenizi kolaylaştırır.

Bu **MvcScaffolding**denilen yeni NuGet *iskele* paketi tarafından desteklenir. "İskele" terimi birçok yazılım teknolojisi tarafından "yazılımınızın daha sonra düzenlenebildiğiniz ve özelleştirebileceğiniz temel bir anahat oluşturma" anlamına gelir. MVC ASP.NET için oluşturduğumuz iskele paketi çeşitli senaryolarda büyük ölçüde yararlıdır:

- **MVC'ASP.NET ilk kez öğreniyorsanız,** çünkü size yararlı, çalışma kodu almak için hızlı bir yol sunar, bu da gereksinimlerinize göre edinebilir ve uyarlayabilirsiniz. Bu boş bir sayfaya bakarak ve nereden başlayacağınızı hiçbir fikrim yok travma sizi kurtarır!
- **MVCASP.NET iyi biliyorsanız ve şimdi** nesne ilişkisisel haritalayıcı, görünüm motoru, test kütüphanesi, vb. gibi yeni bir eklenti teknolojisini keşfediyorsanız, çünkü bu teknolojinin yaratıcısı da bunun için bir iskele paketi oluşturmuş olabilir.
- **Çalışmanız sürekli olarak benzer sınıflar veya bir tür dosya oluşturmayı**içeriyorsa, test fikstürlerini, dağıtım komut dosyalarını veya ihtiyacınız olan her şeyi oluşturan özel iskele klasörleri oluşturabilirsiniz. Ekibinizdeki herkes özel iskelelerinizi de kullanabilir.

MvcScaffolding diğer özellikleri şunlardır:

- C# ve VB projeleri için destek
- Razor ve ASPX görünüm motorları için destek
- ASP.NET MVC alanlarına iskeleyi destekler ve özel görüş düzenleri/ustaları kullanır
- T4 şablonlarını düzenleyerek çıktıyı kolayca özelleştirebilirsiniz
- Özel PowerShell mantığı ve özel T4 şablonları kullanarak tamamen yeni iskeleler ekleyebilirsiniz. Bunlar (ve bunları vermiş olduğunuz özel parametreler) otomatik olarak konsol sekmesi tamamlama listesinde görünür.
- Farklı teknolojiler için ek iskeleler içeren NuGet paketlerini alabilir (örneğin, LINQ'dan SQL'e bir kanıtı nız vardır) ve bunları karıştırıp eşleştirebilirsiniz.

mvc 3 Tools Güncellemesi ASP.NET, aşağıdakiler gibi bu iskele sistemi için harika Visual Studio desteği içerir:

- Denetleyici Ekle İletişim Kutusu artık denetleyici eylemleri ve ilgili görünümleri oluştur, oku, güncelleştir ve sil'in tam otomatik iskelesini destekler. Varsayılan olarak, bu iskele önce EF Code First'i kullanarak veri erişim kodunu kullanır.
- Denetleyici Dialog ekle, *MvcScaffolding*gibi NuGet paketleri aracılığıyla *genişletilebilir iskeleleri* destekler. Bu, bu kadar eğimli iseniz ODBCDirect ile NHibernate ve hatta JET gibi diğer veri erişim teknolojileri için iskeleler oluşturmak için izin verecek iletişim içine özel iskeletakmanızı sağlar!

MVC 3'teki İskele ASP.NET hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- Steve Sanderson sonrası serisi, dahil: 

    1. [Giriş: MvcScaffolding paketi ile ASP.NET MVC 3 proje iskele](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Standart kullanım: Tipik kullanım örnekleri ve seçenekleri](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Bir-Çok İlişkiler](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [İskele İşlemleri ve Birim Testleri](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 şablonlarını geçersiz kılma](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Bu yazı: Özel iskele oluşturma](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman sonrası onun PDC 2010 oturumu [Microsoft "Web Love İsimsiz Paketi" ile bir blog Oluşturma](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 Yayın Notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 Proje Şablonları

Yeni Proje iletişim kutusu, proje şablonlarının HTML 5 sürümlerini etkinleştiren bir onay kutusu içerir. Bu şablonlar, alt düzey tarayıcılarda HTML 5 ve CSS 3 için uyumluluk desteği sağlamak için Modernizr 1.7'den yararlanır.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Jilet Görünümü Motoru

ASP.NET MVC 3 aşağıdaki avantajları sunan Razor adlı yeni bir görünüm motoru ile birlikte gelir:

- Jilet sözdizimi temiz ve özlüdür ve en az sayıda tuş vuruşu gerektirir.
- Razor'ı öğrenmek kolaydır, çünkü kısmen C# ve Visual Basic gibi mevcut dillere dayanır.
- Visual Studio, IntelliSense ve Razor sözdizimi için kod renklendirmesini içerir.
- Razor görünümleri, uygulamayı çalıştırmanız veya bir web sunucusu başlatmanız gerekmeden birim test edilebilir.

Bazı yeni Razor özellikleri şunlardır:

- `@model`görünüme geçirilen türü belirtmek için sözdizimi.
- `@* *@`yorum sözdizimi.
- Tüm site için varsayılanları `layoutpage`(örneğin) bir kez belirtme yeteneği.
- HTML `Html.Raw` kodlamaolmadan metin görüntüleme yöntemi.
- Birden çok görünüm*\_(viewstart.cshtml veya* * \_viewstart.vbhtml* dosyaları) arasında kod paylaşımı desteği.

Razor, aşağıdakiler gibi yeni HTML yardımcıları da içerir:

- `Chart`. ASP.NET 4'teki grafik denetimiyle aynı özellikleri sunan bir grafik işler.
- `WebGrid`. Sayfalama ve sıralama işleviyle birlikte bir veri ızgarası işler.
- `Crypto`. Düzgün tuzlanmış ve karma parolalar oluşturmak için karma algoritmalar kullanır.
- `WebImage`. Görüntü işler.
- `WebMail`. Bir e-posta iletisi gönderir.

Razor hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Scott Guthrie's blog yazısı Razor tanıtan](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie's blog yazısı @model anahtar kelime tanıtan](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie's blog yazısı Razor düzenleri tanıtan](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API Hızlı Başvuru](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 Yayın Notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Çoklu Görünüm Motorları için Destek

MVC 3'ASP.NET **Görünüm Ekle** iletişim kutusu, çalışmak istediğiniz görünüm altyapısını seçmenize olanak tanır ve **Yeni Proje** iletişim kutusu bir proje için varsayılan görünüm altyapısını belirtmenizi sağlar. Web Formları görünüm motoru (ASPX), Razor veya [Spark,](http://sparkviewengine.com/) [NHaml](https://code.google.com/p/nhaml/)veya [NDjango](http://ndjango.org/)gibi açık kaynak kodlu bir görünüm motorseçebilirsiniz.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Denetleyici Geliştirmeleri

### <a name="global-action-filters"></a>Genel İşlem Filtreleri

Bazen bir eylem yöntemi çalıştırmadan önce veya bir eylem yöntemi çalıştırdıktan sonra mantık gerçekleştirmek istersiniz. Bunu desteklemek için, mvc 2 ASP.NET işlem filtreleri sağladı. Eylem filtreleri, belirli denetleyici eylem yöntemlerine eylem öncesi ve eylem sonrası davranış eklemek için bildirimsel araçlar sağlayan özel özniteliklerdir. Ancak, bazı durumlarda tüm eylem yöntemleri için geçerli olan eylem öncesi veya eylem sonrası davranışı belirtmek isteyebilirsiniz. MVC 3, `GlobalFilters` genel filtreleri koleksiyona ekleyerek belirtmenizi sağlar. Genel eylem filtreleri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [MVC 3 Önizleme Scott Guthrie günlüğü](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [mvc ASP.NET filtreleme](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Yeni "ViewBag" Özelliği

MVC 2 denetleyicileri, geç bağlanmış sözlük `ViewData` API'sini kullanarak verileri görünüm şablonuna aktarmanızı sağlayan bir özelliği destekler. MVC 3'te, aynı amacı gerçekleştirmek için `ViewBag` özelliği yle birlikte biraz daha basit sözdizimini de kullanabilirsiniz. Örneğin, yazmak `ViewData["Message"]="text"`yerine, yazabilirsiniz. `ViewBag.Message="text"` Özelliği kullanmak için güçlü bir şekilde yazılan sınıfları `ViewBag` tanımlamanız gerekmez. Dinamik bir özellik olduğundan, bunun yerine sadece alabilirsiniz veya özellikleri ayarlamak ve çalışma zamanında dinamik olarak bunları çözecektir. Dahili `ViewBag` olarak, özellikler `ViewData` sözlükte ad/değer çiftleri olarak depolanır. (Not: MVC 3'ün en ön `ViewBag` sürüm sürümlerinde, `ViewModel` özellik özellik olarak adlandırılmıştır.)

### <a name="new-actionresult-types"></a>Yeni "ActionResult" türleri

Aşağıdaki `ActionResult` türleri ve ilgili yardımcı yöntemleri yeni veya MVC 3 geliştirilmiştir:

- [httpnotfoundresult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). İstemciye 404 HTTP durum kodu verir.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Boolean parametreye bağlı olarak geçici bir yeniden yönlendirme (HTTP 302 durum kodu) veya kalıcı bir yeniden yönlendirme (HTTP 301 durum kodu) verir. Bu değişiklikle birlikte, [Denetleyici](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) sınıfının artık kalıcı yönlendirmeler `RedirectPermanent`gerçekleştirmek `RedirectToRoutePermanent`için `RedirectToActionPermanent`üç yöntemi vardır: , , ve . Bu yöntemler, `RedirectResult` `Permanent` özellik olarak ayarlanmış `true`bir örneğini döndürün.
- [httpstatuscoderesult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Kullanıcı tarafından belirtilen bir HTTP durum kodunu döndürür.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript ve Ajax Geliştirmeleri

Varsayılan olarak, Ajax ve Doğrulama yardımcıları MVC 3 göze batan bir JavaScript yaklaşımı kullanın. Göze batmaz JavaScript, HTML'ye satır içinde JavaScript enjekte etmekten kaçınır. Bu, HTML'nizi daha küçük ve daha az karmaşık hale getirir ve JavaScript kitaplıklarını değiştirmeyi veya özelleştirmeyi kolaylaştırır. MVC 3'teki doğrulama yardımcıları `jQueryValidate` da eklentiyi varsayılan olarak kullanır. MVC 2 davranışı istiyorsanız, *bir web.config* dosya ayarını kullanarak göze batmaz JavaScript'i devre dışı kullanabilirsiniz. JavaScript ve Ajax geliştirmeleri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Vikipedi sitesinde göze batmaz JavaScript temel giriş](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson's Unobtrusive JavaScript Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson'S Unobtrusive JavaScript Doğrulama Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Jilet ve Göze batmaz JavaScript ile Bir MVC 3 Uygulama oluşturma](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (ASP.NET sitesinde öğretici)
- [MVC 3 Yayın Notları](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Varsayılan Olarak İstemci Tarafı Doğrulama

MVC'nin önceki sürümlerinde, istemci tarafı `Html.EnableClientValidation` doğrulaması etkinleştirmek için yöntemi açıkça bir görünümden aramanız gerekir. MVC 3'te istemci tarafı doğrulaması varsayılan olarak etkinleştirildiğinden artık bu gerekli değildir. (Bunu *web.config* dosyasındaki bir ayarı kullanarak devre dışı kullanabilirsiniz.)

İstemci tarafı doğrulamanın işe yaraması için, sitenizdeki uygun jQuery ve jQuery Doğrulama kitaplıklarına başvurmanız gerekir. Bu kitaplıkları kendi sunucunuzda barındırabilir veya Microsoft veya Google'ın CDN'leri gibi bir içerik dağıtım ağınızdan (CDN) başvuruyapabilirsiniz.

### <a name="remote-validator"></a>Uzaktan Doğrulayıcı

ASP.NET MVC 3, jQuery Doğrulama eklentisinin uzaktan doğrulayıcı desteğinden yararlanmanızı sağlayan yeni [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) sınıfını destekler. Bu, istemci tarafı doğrulama kitaplığı, yalnızca sunucu tarafında yapılabilecek doğrulama mantığını gerçekleştirmek için sunucuda tanımladığınız özel bir yöntemi otomatik olarak aramasını sağlar.

Aşağıdaki `Remote` örnekte, öznitelik istemci doğrulama `UserNameAvailable` `UsersController` `UserName` alanı doğrulamak için sınıfta adlı bir eylem çağıracağını belirtir.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

Aşağıdaki örnekte karşılık gelen denetleyici gösterilmektedir.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Öznitelik nasıl kullanılacağı `Remote` hakkında daha fazla bilgi için bkz: MSDN kitaplığında [mvc ASP.NET Uzaktan Doğrulama uygulama.](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)

### <a name="json-binding-support"></a>JSON Bağlayıcı Destek

ASP.NET MVC 3, eylem yöntemlerinin JSON kodlanmış verileri almasını ve eylem yöntemi parametrelerine model bağlamasını sağlayan yerleşik JSON bağlama desteğini içerir. Bu özellik, istemci şablonları ve veri bağlama içeren senaryolarda yararlıdır. (İstemci şablonları, istemcide çalıştırılabilen şablonları kullanarak tek bir veri öğesini veya veri öğesi kümesini biçimlendirmenizi ve görüntülemenizi sağlar.) MVC 3, JSON verilerini gönderen ve alan sunucudaki eylem yöntemleriyle istemci şablonlarını kolayca bağlamanızı sağlar. JSON bağlayıcı destek hakkında daha fazla bilgi için, [Scott Guthrie's MVC 3 Önizleme blog yazısı](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript ve AJAX Geliştirmeler** bölümüne bakın.

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Model Doğrulama Geliştirmeleri

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" Meta veri öznitelikleri

ASP.NET MVC `DataAnnotations` 3 gibi `DisplayAttribute`meta veri özniteliklerini destekler.

### <a name="validationattribute-class"></a>"DoğrulamaÖznitelik" Sınıfı

Sınıf, `ValidationAttribute` geçerli doğrulama bağlamı hakkında hangi `IsValid` nesnenin doğrulandığı gibi daha fazla bilgi sağlayan yeni bir aşırı yükü desteklemek için .NET Framework 4'te geliştirilmiştir. Bu, modelin başka bir özelliğine göre geçerli değeri doğrulayabilirsiniz daha zengin senaryolar sağlar. Örneğin, yeni `CompareAttribute` öznitelik bir modelin iki özelliğinin değerlerini karşılaştırmanızı sağlar. Aşağıdaki örnekte, `ComparePassword` özelliğin geçerli `Password` olabilmesi için alanla eşleşmesi gerekir.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Doğrulama Arabirimleri

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) arabirimi, model düzeyinde doğrulama gerçekleştirmenize olanak tanır ve genel modelin durumuna özgü doğrulama hatası iletileri veya model içindeki iki özellik arasında sağlamanızı sağlar. MVC 3 şimdi model `IValidatableObject` bağlama zaman arabirimden hataları alır ve otomatik olarak bayraklar veya yerleşik HTML formu yardımcıları kullanarak bir görünüm içinde etkilenen alanları vurgulamaktadır.

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) arabirimi, ASP.NET MVC'nin bir doğrulayıcının istemci doğrulama desteğine sahip olup olmadığını çalışma zamanında keşfetmesini sağlar. Bu arabirim, çeşitli doğrulama çerçeveleriyle tümleşik olacak şekilde tasarlanmıştır.

Doğrulama arabirimleri hakkında daha fazla bilgi için Scott [Guthrie'nin MVC 3 Önizleme blog yazısının](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **Model Doğrulama Geliştirmeleri** bölümüne bakın. (Ancak, blogdaki "IValidateObject" için başvuru "IValidatableObject" olması gerektiğini unutmayın.)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Bağımlılık Enjeksiyon Iyileştirmeler

ASP.NET MVC 3 Bağımlılık Enjeksiyonu (DI) uygulamak ve Bağımlılık Enjeksiyonu veya Kontrol Ters (IOC) kapları ile entegre için daha iyi destek sağlar. DI desteği aşağıdaki alanlarda eklenmiştir:

- Denetleyiciler (kayıt ve enjekte kontrolörleri, enjekte kontrolörleri).
- Görünümler (görünüm motorlarını kaydetme ve enjekte etme, görünüm sayfalarına bağımlılıkenjekte etme).
- İşlem filtreleri (filtreleri bulma ve enjekte etme).
- Model bağlayıcıları (kayıt ve enjekte).
- Model doğrulama sağlayıcıları (kayıt ve enjekte etme).
- Meta veri sağlayıcılarını (kayıt ve enjekte etme) modelle.
- Değer sağlayıcılar (kayıt ve enjekte etme).

MVC [3, Ortak Hizmet Bulucu](https://github.com/unitycontainer/commonservicelocator) kitaplığını ve bu kitaplığın `IServiceLocator` arabirimini destekleyen herhangi bir DI kapsayıcısını destekler. Ayrıca, DI `IDependencyResolver` çerçevelerinin tümleştirilen kolaylaşmasını sağlayan yeni bir arabirimi de destekler.

MVC 3'teki DI hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Brad Wilson'ın Hizmet Yeri'ndeki blog gönderileri serisi](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 Yayın Notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Diğer Yeni Özellikler

### <a name="nuget-integration"></a>NuGet Entegrasyonu

ASP.NET MVC 3, kurulumunun bir parçası olarak NuGet'i otomatik olarak yükler ve etkinleştirirken. NuGet, projelerinizde .NET kitaplıklarını ve araçlarını bulmayı, yüklemeyi ve kullanmayı kolaylaştıran ücretsiz bir açık kaynak paket yöneticisidir. Tüm Visual Studio proje türleri (ASP.NET Web Formları ve ASP.NET MVC dahil) ile çalışır.

NuGet, açık kaynak projeleri (örneğin, Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks ve Elmah gibi projeler) koruyan geliştiricilerin kitaplıklarını paketlemelerine ve çevrimiçi bir galeriye kaydettirmelerine olanak tanır. Paketi bulmak ve üzerinde çalıştıkları projelere yüklemek için bu kitaplıklardan birini kullanmak isteyen .NET geliştiricileri için daha kolaydır.

ASP.NET 3 Tools Update ile proje şablonları, Önceden yüklenmiş NuGet paketlerini JavaScript kitaplıklarını içerir, böylece NuGet üzerinden güncellenebilir. Varlık Çerçeve Kodu İlk de bir NuGet paketi olarak önceden yüklenir.

NuGet hakkında daha fazla bilgi için [NuGet belgelerine](https://docs.microsoft.com/nuget/)bakın.

### <a name="partial-page-output-caching"></a>Kısmi Sayfa Çıkış Önbelleğe Alma

ASP.NET MVC, sürüm 1'den bu yana tam sayfa yanıtlarının önbelleğe alınmış çıkışını desteklemiştir. MVC 3 ayrıca, bölgeleri veya yanıt parçalarını kolayca önbelleğe almanızı sağlayan kısmi sayfa çıkış önbelleğe almanızı da destekler. Önbelleğe alma hakkında daha fazla bilgi için, MVC 3 sürüm adayı ve [MVC 3 Sürüm Notları](../whitepapers/mvc3-release-notes.md) **Çocuk Eylem Çıkış Önbelleğe alma** bölümünde Scott [Guthrie's blog yazısı](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) Kısmi Sayfa Çıkış **Önbelleğe alma** bölümüne bakın.

### <a name="granular-control-over-request-validation"></a>İstek Doğrulama üzerinde taneli denetim

ASP.NET MVC, XSS ve HTML enjeksiyon saldırılarına karşı otomatik olarak korunmaya yardımcı olan yerleşik istek doğrulamasına sahiptir. Ancak, bazen kullanıcıların HTML içeriği yayınlamasına izin vermek gibi (örneğin, blog girişlerinde veya CMS içeriğinde) istek doğrulamasını açıkça devre dışı bırakmak istersiniz. Artık model bağlama sırasında her mülk için istek doğrulamasını devre dışı bırakmaamaçlı modellere [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) özniteliği ekleyebilirsiniz. İstek doğrulaması hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [MVC 3 sürüm adayı Scott Guthrie's blog yazısı](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) **Unobtrusive JavaScript ve Doğrulama** bölümü .
- [MVC 3 Yayın Notları](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Genişletilebilir "Yeni Proje" İletişim Kutusu

MVC 3 ASP.NET **yeni proje** iletişim kutusuna proje şablonları, görünüm motorları ve birim test proje çerçeveleri ekleyebilirsiniz.

### <a name="template-scaffolding-improvements"></a>Şablon İskele Geliştirmeleri

ASP.NET MVC 3 iskele şablonları, modellerdeki birincil anahtar özelliklerini belirleme ve bunları MVC'nin önceki sürümlerine göre uygun şekilde işleme konusunda daha iyi bir iş yapar. (Örneğin, iskele şablonları artık birincil anahtarın kullanılabilir form alanı olarak İskele oluşturmadığından emin olun.)

Varsayılan olarak, Oluştur ve Düzenlediği İskeleleri artık `Html.EditorFor` yardımcı yerine `Html.TextBoxFor` yardımcıyı kullanır. Bu, **Görünüm Ekle** iletişim kutusu bir görünüm oluşturduğunda, modeldeki meta veriler için veri ek açıklama öznitelikleri şeklindeki desteği artırır.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.LabelFor" ve "Html.LabelForModel" için yeni aşırı yüklemeler

Yeni yöntem aşırı yüklemeleri `LabelFor` ve `LabelForModel` yardımcı yöntemler için eklenmiştir. Yeni aşırı yüklemeler, etiket metnini belirtmenize veya geçersiz kılmanıza olanak tanır.

### <a name="sessionless-controller-support"></a>Oturumsuz Denetleyici Desteği

MVC 3ASP.NET oturum durumunu kullanmak için bir denetleyici sınıfı isteyip istemediğinizi ve eğer öyleyse oturum durumunun okunması/yazması mı yoksa salt okunur mu gerektiğini belirtebilirsiniz. Oturumsuz denetleyici desteği hakkında daha fazla bilgi için [MVC 3 Sürüm Notları'na](../whitepapers/mvc3-release-notes.md)bakın.

### <a name="new-additionalmetadataattribute-class"></a>Yeni "EkMetadataAttribute" Sınıfı

Bir model özelliği için `ModelMetadata.AdditionalValues` sözlüğü doldurmak için [EkMetaveri](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) özniteliğini kullanabilirsiniz. Örneğin, bir görünüm modelinde yalnızca bir yöneticiye görüntülenmesi gereken bir özellik varsa, bu özelliği aşağıdaki örnekte gösterildiği gibi açıklama ekleyebilirsiniz:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Bu meta veriler, bir ürün görünümü modeli işlendiğinde herhangi bir görüntü veya düzenleyici şablonu için kullanılabilir hale getirilir. Meta veri bilgilerini yorumlamak size kalmış.

### <a name="accountcontroller-improvements"></a>AccountController iyileştirmeleri

Internet proje şablonundaki Hesap Denetleyicisi büyük ölçüde geliştirildi.

### <a name="new-intranet-project-template"></a>Yeni Intranet Proje Şablonu

Windows Kimlik Doğrulaması'nı etkinleştiren ve Hesap Kontrolörü'nu kaldıran yeni bir Intranet Proje Şablonu dahildir.
