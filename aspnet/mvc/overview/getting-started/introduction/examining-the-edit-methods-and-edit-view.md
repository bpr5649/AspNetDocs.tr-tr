---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Düzenleme yöntemleri ve düzenleme görünümü inceleniyor | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045214"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Düzenleme Metotlarını ve Düzenleme Görünümünü İnceleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu bölümde, `Edit` film denetleyicisi için oluşturulan eylem yöntemlerini ve görünümlerini inceleyeceksiniz. Ancak ilk olarak yayın tarihinin daha iyi görünmesini sağlamak için kısa bir göz atalım. *Models\movie.cs* dosyasını açın ve vurgulanan satırları aşağıda gösterildiği gibi ekleyin:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

Ayrıca, tarih kültürünü aşağıdakine benzer hale getirebilirsiniz:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

Sonraki öğreticide [veri ek açıklamalarını](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ele alacağız. [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) özniteliği bir alanın adı için (Bu durumda "ReleaseDate" yerine "Yayın tarihi") görüntüleneceğini belirtir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği verilerin türünü belirtir, bu durumda bir tarih olur, bu nedenle alanda depolanan zaman bilgileri görüntülenmez. Chrome tarayıcısında, tarih biçimlerini yanlış işleyen bir hata için [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliği gereklidir.

Uygulamayı çalıştırın ve `Movies` denetleyiciye gidin. Bağlantı yaptığı URL 'yi görmek için fare işaretçisini bir **düzenleme** bağlantısı üzerine tutun.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Düzenleme** bağlantısı, `Html.ActionLink` *Views\Movies\Index.cshtml* görünümündeki yöntemi tarafından oluşturulmuştur:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`Nesnesi, [System. Web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) temel sınıfında özelliği kullanılarak ortaya çıkarılan bir yardımcıdır. `ActionLink`Yardımcı yöntemi, denetleyicilerde eylem yöntemlerine bağlantı sağlayan HTML köprülerini dinamik olarak oluşturmayı kolaylaştırır. Yöntemin ilk bağımsız değişkeni, `ActionLink` işlenecek bağlantı metindir (örneğin, `<a>Edit Me</a>` ). İkinci bağımsız değişken çağrılacak eylem yönteminin adıdır (Bu durumda `Edit` eylem). Son bağımsız değişken, yol verilerini üreten [anonim bir nesnedir](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (Bu durumda, 4 ' ün kimliği).

Önceki görüntüde gösterilen oluşturulan bağlantı `http://localhost:1234/Movies/Edit/4` . Varsayılan yol ( *App \_ Start\routeconfig.cs*IÇINDE kurulan) URL modelini alır `{controller}/{action}/{id}` . Bu nedenle, ASP.NET, `http://localhost:1234/Movies/Edit/4` `Edit` denetleyicinin Action metoduna 4 ' e eşit olan bir isteğe çevirir `Movies` `ID` . Aşağıdaki kodu *App \_ Start\routeconfig.cs* dosyasından inceleyin. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) YÖNTEMI, http isteklerini doğru denetleyiciye ve eylem yöntemine yönlendirmek ve Isteğe bağlı ID parametresini sağlamak için kullanılır. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) yöntemi, [HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) `ActionLink` Denetleyici, eylem yöntemi ve rota verileri verilen URL 'Leri oluşturmak için gibi htmlyardımcılar tarafından da kullanılır.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

Ayrıca, bir sorgu dizesi kullanarak eylem yöntemi parametrelerini geçirebilirsiniz. Örneğin, URL `http://localhost:1234/Movies/Edit?ID=3` Ayrıca `ID` 3 parametresini `Edit` denetleyicinin Action yöntemine geçirir `Movies` .

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

Denetleyiciyi açın `Movies` . İki `Edit` eylem yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

İkinci `Edit` eylem yönteminin önünde özniteliği olduğuna dikkat edin `HttpPost` . Bu öznitelik, yönteminin aşırı yüklemesinin `Edit` yalnızca post istekleri için çağrılabileceğini belirtir. `HttpGet`Özniteliği ilk düzenleme yöntemine uygulayabilirsiniz, ancak varsayılan değer olduğundan bu gerekli değildir. (Özniteliği Yöntem olarak örtük olarak atanmış eylem yöntemlerine başvuracağız `HttpGet` `HttpGet` .) [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) özniteliği, korsanların modelinize veri gönderme işlemini daha fazla tutan başka önemli bir güvenlik mekanizmasıdır. Yalnızca, değiştirmek istediğiniz bağlama özniteliğinde özellikleri eklemeniz gerekir. Fazla deftere nakil ve bağlama özniteliği hakkında bilgi edinmek için bkz. [fazla nakil güvenlik notum](https://go.microsoft.com/fwlink/?LinkId=317598). Bu öğreticide kullanılan basit modelde, modeldeki tüm verileri bağlamamız gerekir. [Validateantiforgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği bir isteğin kullanımını engellemek için kullanılır ve `@Html.AntiForgeryToken()` düzenleme görünümü dosyasında (*Views\Movies\Edit.cshtml*) eşleştirilmiştir, aşağıda bir bölüm gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` denetleyicinin yöntemiyle eşleşmesi gereken gizli form Anti-forma belirteci oluşturur `Edit` `Movies` . MVC 'de öğreticide, siteler arası istek (XSRF veya CSRF olarak da bilinir) hakkında daha fazla bilgi edinmek için bkz. [MVC/CSRF önleme](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).

`HttpGet` `Edit` Yöntemi, film kimliği parametresini alır, Entity Framework yöntemini kullanarak filmi arar `Find` ve seçili filmi düzenleme görünümüne döndürür. Bir film bulunamazsa, [Httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) döndürülür. Scafkatlama sistemi düzenleme görünümü oluştururken, sınıfını ve `Movie` `<label>` `<input>` sınıfının her bir özelliği için işlenecek kodu ve öğelerini inceledi. Aşağıdaki örnekte, Visual Studio scafkatlama sistemi tarafından oluşturulan düzenleme görünümü gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Görünüm şablonunun dosyanın en üstünde bir ifadeye sahip olduğuna dikkat edin `@model MvcMovie.Models.Movie` ; Bu, görünümün görünüm şablonu için modelin tür olmasını beklediğini belirtir `Movie` .

Scafkatlanmış kod, HTML işaretlemesini kolaylaştırmak için çeşitli *yardımcı yöntemler* kullanır. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Yardımcı, alanın adını ( &quot; başlık &quot; , &quot; ReleaseDate &quot; , &quot; tarz &quot; veya &quot; Fiyat) görüntüler &quot; . [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Yardımcı BIR HTML öğesi işler `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Yardımcı, bu özellikle ilişkili tüm doğrulama iletilerini görüntüler.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bir **düzenleme** bağlantısına tıklayın. Tarayıcıda, sayfanın kaynağını görüntüleyin. Form öğesi için HTML aşağıda gösterilmiştir.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>`Öğeleri `<form>` `action` özniteliği */movies/Edit* URL 'SINE postala olarak ayarlanmış bir HTML öğesi. **Kaydet** düğmesine tıklandığında form verileri sunucuya gönderilir. İkinci satır, çağrı tarafından oluşturulan gizli [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) belirtecini gösterir `@Html.AntiForgeryToken()` .

## <a name="processing-the-post-request"></a>POST Isteği işleniyor

Aşağıdaki listede `HttpPost` `Edit` eylem yönteminin sürümü gösterilmektedir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[Validateantiforgerrivtoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği, görünümdeki çağrı tarafından oluşturulan [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) belirtecini doğrular `@Html.AntiForgeryToken()` .

[ASP.NET MVC model Ciltçi](https://msdn.microsoft.com/library/dd410405.aspx) , postalanan form değerlerini alır ve `Movie` parametresi olarak geçirilmiş bir nesne oluşturur `movie` . , `ModelState.IsValid` Formda gönderilen verilerin bir nesneyi değiştirmek (düzenlemek veya güncelleştirmek) için kullanılabileceğini doğrular `Movie` . Veriler geçerliyse, film verileri `Movies` `db` ( `MovieDBContext` örnek) koleksiyonuna kaydedilir. Yeni film verileri, yöntemi çağırarak veritabanına kaydedilir `SaveChanges` `MovieDBContext` . Veriler kaydedildikten sonra kod, kullanıcıyı, `Index` `MoviesController` Yeni yapılan değişiklikler dahil olmak üzere, film koleksiyonunu görüntüleyen sınıfının Action yöntemine yönlendirir.

İstemci tarafı doğrulaması bir alanın değerini belirler almaz, bir hata iletisi görüntülenir. JavaScript devre dışıysa, istemci tarafı doğrulaması devre dışı bırakılır. Ancak, sunucu, gönderilen değerleri geçerli değil olarak algılar ve form değerleri hata iletileriyle birlikte görüntülenir.

Doğrulama Öğreticinin ilerleyen kısımlarında daha ayrıntılı olarak incelendi.

`Html.ValidationMessageFor` *Edit. cshtml* görünüm şablonundaki yardımcılar, uygun hata iletilerini görüntülemeyi dikkate alır.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

Tüm `HttpGet` Yöntemler benzer bir düzene uyar. Bir film nesnesi (veya bunun durumunda nesne listesi `Index` ) alır ve modeli görünüme iletir. `Create`Yöntemi, oluşturma görünümüne boş bir film nesnesi geçirir. Verileri oluşturan, düzenleme, silme veya başka bir şekilde değiştiren tüm yöntemler `HttpPost` , yönteminin aşırı yüküne neden olacak. HTTP GET yöntemindeki verileri değiştirmek, Web günlüğü gönderi girişi [ASP.NET MVC ipucu #46 – güvenlik delikleri oluşturdukları Için silme bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET yöntemindeki verileri değiştirmek, HTTP en iyi uygulamalarını ve bu GET isteklerinin uygulamanızın [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) durumunu değiştirmemelidir. Diğer bir deyişle, bir GET işleminin gerçekleştirilmesi, yan etkileri olmayan ve kalıcı verilerinizi değiştirmeyen bir güvenli işlem olmalıdır.

## <a name="jquery-validation-for-non-english-locales"></a>Ingilizce olmayan yerel ayarlarda jQuery doğrulaması

ABD Ingilizcesi bilgisayar kullanıyorsanız, bu bölümü atlayabilir ve sonraki öğreticiye gidebilirsiniz. Bu öğreticinin globalize sürümünü [buradan](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)indirebilirsiniz. Uluslararası duruma getirme için harika iki bölüm öğreticisi için bkz. [Nadeem 'ın ASP.NET MVC 5 Uluslararası duruma getirme](http://afana.me/post/aspnet-mvc-internationalization.aspx).

> [!NOTE]
> &quot;ondalık bir nokta ve ABD İngilizcesi olmayan tarih biçimleri için virgül (,) kullanan İngilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için &quot; , *globalize.js* ve belirli *kültürleri/globalize.cultures.js* dosyanızı (Kimden [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve kullanılacak JavaScript 'i dahil etmeniz gerekir `Globalize.parseFloat` . NuGet 'ten Ingilizce olmayan jQuery doğrulamasını alabilirsiniz. (Ingilizce yerel ayar kullanıyorsanız globalize ' yi yüklemeyin.)

1. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne tıklayın ve ardından **çözüm için NuGet Paketlerini Yönet**' e tıklayın.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. Sol bölmede, Araştır ' ı <strong>seçin *.</strong> * (Aşağıdaki resme bakın.)
3. Giriş kutusuna * globalize * * yazın.

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) Seç `jQuery.Validation.Globalize` ' i seçin `MvcMovie` ve **ardından Install**' a tıklayın. *Scripts\jquery.globalize\globalize.js* dosyası projenize eklenecektir. * Scripts\jquerypst Globalize\kültürleri \* klasörü birçok kültür JavaScript dosyası içerir. Bu paketin yüklenmesi beş dakika sürebilir.

   Aşağıdaki kod Views\Movies\Edit.cshtml dosyasındaki değişiklikleri gösterir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Her düzenleme görünümünde bu kodun yinelenmesinden kaçınmak için, düzen dosyasına taşıyabilirsiniz. Betik indirmeyi iyileştirmek için bkz. öğretici [paketme ve küçültmeye](../../performance/bundling-and-minification.md)yönelik.

Daha fazla bilgi için bkz. [ASP.NET MVC 3 Uluslararası duruma getirme](http://afana.me/post/aspnet-mvc-internationalization.aspx) ve [ASP.NET MVC 3 Uluslararası duruma getirme-Bölüm 2 (nerdakşam yemeği)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).

Geçici bir düzeltme olarak, doğrulamanız için yerel ayarda çalışmayı alamazsanız bilgisayarınızı ABD Ingilizcesi 'ni kullanmaya zorlayabilir veya tarayıcınızda JavaScript 'ı devre dışı bırakabilirsiniz. Bilgisayarınızı ABD Ingilizcesi kullanmaya zorlamak için, proje kök *web.config* dosyasına Genelleştirme öğesini ekleyebilirsiniz. Aşağıdaki kod, kültürü Birleşik Devletler Ingilizce olarak ayarlanan Genelleştirme öğesini gösterir.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> Sonraki öğreticide, arama işlevi uygulayacağız.

> [!div class="step-by-step"]
> [Önceki](accessing-your-models-data-from-a-controller.md) 
>  [Sonraki](adding-search.md)
