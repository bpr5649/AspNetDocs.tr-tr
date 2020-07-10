---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: Düzenleme yöntemleri ve düzenleme görünümü inceleniyor | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163059"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Düzenleme Metotlarını ve Düzenleme Görünümünü İnceleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde, film denetleyicisi için oluşturulan eylem yöntemlerini ve görünümlerini inceleyeceksiniz. Ardından özel bir arama sayfası ekleyeceksiniz.

Uygulamayı çalıştırın ve `Movies` tarayıcınızın adres ÇUBUĞUNDAKI URL 'ye */filmler* ekleyerek denetleyiciye gidin. Bağlantı yaptığı URL 'yi görmek için fare işaretçisini bir **düzenleme** bağlantısı üzerine tutun.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Düzenleme** bağlantısı, `Html.ActionLink` *Views\Movies\Index.cshtml* görünümündeki yöntemi tarafından oluşturulmuştur:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`Nesnesi, [System. Web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) temel sınıfında özelliği kullanılarak ortaya çıkarılan bir yardımcıdır. `ActionLink`Yardımcı yöntemi, denetleyicilerde eylem yöntemlerine bağlantı sağlayan HTML köprülerini dinamik olarak oluşturmayı kolaylaştırır. Yöntemin ilk bağımsız değişkeni, `ActionLink` işlenecek bağlantı metindir (örneğin, `<a>Edit Me</a>` ). İkinci bağımsız değişken çağrılacak eylem yönteminin adıdır. Son bağımsız değişken, yol verilerini üreten [anonim bir nesnedir](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (Bu durumda, 4 ' ün kimliği).

Önceki görüntüde gösterilen oluşturulan bağlantı `http://localhost:xxxxx/Movies/Edit/4` . Varsayılan yol ( *App \_ Start\routeconfig.cs*IÇINDE kurulan) URL modelini alır `{controller}/{action}/{id}` . Bu nedenle, ASP.NET, `http://localhost:xxxxx/Movies/Edit/4` `Edit` denetleyicinin Action metoduna 4 ' e eşit olan bir isteğe çevirir `Movies` `ID` . Aşağıdaki kodu *App \_ Start\routeconfig.cs* dosyasından inceleyin.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Ayrıca, bir sorgu dizesi kullanarak eylem yöntemi parametrelerini geçirebilirsiniz. Örneğin, URL `http://localhost:xxxxx/Movies/Edit?ID=4` Ayrıca `ID` 4 parametresini `Edit` denetleyicinin Action yöntemine geçirir `Movies` .

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

Denetleyiciyi açın `Movies` . İki `Edit` eylem yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

İkinci `Edit` eylem yönteminin önünde özniteliği olduğuna dikkat edin `HttpPost` . Bu öznitelik, yöntemin aşırı yüklemesinin `Edit` yalnızca post istekleri için çağrılabileceğini belirtir. `HttpGet`Özniteliği ilk düzenleme yöntemine uygulayabilirsiniz, ancak varsayılan değer olduğundan bu gerekli değildir. (Özniteliği Yöntem olarak örtük olarak atanmış eylem yöntemlerine başvuracağız `HttpGet` `HttpGet` .)

`HttpGet` `Edit` Yöntemi, film kimliği parametresini alır, Entity Framework yöntemini kullanarak filmi arar `Find` ve seçili filmi düzenleme görünümüne döndürür. Yöntem parametre olmadan çağrılırsa, ID parametresi [varsayılan değeri](https://msdn.microsoft.com/library/dd264739.aspx) sıfır olarak belirler `Edit` . Bir film bulunamazsa, [Httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) döndürülür. Scafkatlama sistemi düzenleme görünümü oluştururken, sınıfını ve `Movie` `<label>` `<input>` sınıfının her bir özelliği için işlenecek kodu ve öğelerini inceledi. Aşağıdaki örnek, oluşturulan düzenleme görünümünü göstermektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

Görünüm şablonunun dosyanın en üstünde bir ifadeye sahip olduğuna dikkat edin `@model MvcMovie.Models.Movie` ; Bu, görünümün görünüm şablonu için modelin tür olmasını beklediğini belirtir `Movie` .

Scafkatlanmış kod, HTML işaretlemesini kolaylaştırmak için çeşitli *yardımcı yöntemler* kullanır. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Yardımcı, alanın adını ( &quot; başlık &quot; , &quot; ReleaseDate &quot; , &quot; tarz &quot; veya &quot; Fiyat) görüntüler &quot; . [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Yardımcı BIR HTML öğesi işler `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Yardımcı, bu özellikle ilişkili tüm doğrulama iletilerini görüntüler.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bir **düzenleme** bağlantısına tıklayın. Tarayıcıda, sayfanın kaynağını görüntüleyin. Form öğesi için HTML aşağıda gösterilmiştir.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`Öğeleri `<form>` `action` özniteliği */movies/Edit* URL 'SINE postala olarak ayarlanmış bir HTML öğesi. Form verileri, **Düzenle** düğmesine tıklandığında sunucuya gönderilir.

## <a name="processing-the-post-request"></a>POST Isteği işleniyor

Aşağıdaki listede `HttpPost` `Edit` eylem yönteminin sürümü gösterilmektedir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC model Ciltçi](https://msdn.microsoft.com/magazine/hh781022.aspx) , postalanan form değerlerini alır ve `Movie` parametresi olarak geçirilmiş bir nesne oluşturur `movie` . `ModelState.IsValid`Yöntemi, formda gönderilen verilerin bir nesneyi değiştirmek (düzenlemek veya güncelleştirmek) için kullanılabileceğini doğrular `Movie` . Veriler geçerliyse, film verileri `Movies` örnek koleksiyonuna kaydedilir `db(MovieDBContext` ). Yeni film verileri, yöntemi çağırarak veritabanına kaydedilir `SaveChanges` `MovieDBContext` . Veriler kaydedildikten sonra, kod, `Index` `MoviesController` Yeni yapılan değişiklikler dahil olmak üzere film koleksiyonunu görüntüleyen sınıfının Action yöntemine kullanıcıyı yönlendirir.

Postalanan değerler geçerli değilse, formda yeniden görüntülenir. `Html.ValidationMessageFor` *Edit. cshtml* görünüm şablonundaki yardımcılar, uygun hata iletilerini görüntülemeyi dikkate alır.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> ondalık bir nokta için virgül (,) kullanan Ingilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için &quot; &quot; , *globalize.js* ve belirli *kültürlerini/globalize.cultures.js* dosyanızı (Kimden [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve kullanılacak JavaScript 'i dahil etmeniz gerekir `Globalize.parseFloat` . Aşağıdaki kod, &quot; fr-FR kültürü ile çalışmak için Views\Movies\Edit.cshtml dosyasındaki değişiklikleri gösterir &quot; :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Decimal alanı ondalık bir nokta değil virgül gerektirebilir. Geçici bir çözüm olarak, Genelleştirme öğesini projeler kök web.config dosyasına ekleyebilirsiniz. Aşağıdaki kod, kültürü Birleşik Devletler Ingilizce olarak ayarlanan Genelleştirme öğesini gösterir.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

Tüm `HttpGet` Yöntemler benzer bir düzene uyar. Bir film nesnesi (veya bunun durumunda nesne listesi `Index` ) alır ve modeli görünüme iletir. `Create`Yöntemi, oluşturma görünümüne boş bir film nesnesi geçirir. Verileri oluşturan, düzenleme, silme veya başka bir şekilde değiştiren tüm yöntemler `HttpPost` , yönteminin aşırı yüküne neden olacak. HTTP GET yöntemindeki verileri değiştirmek, Web günlüğü gönderi girişi [ASP.NET MVC ipucu #46 – güvenlik delikleri oluşturdukları Için silme bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET yöntemindeki verileri değiştirmek, HTTP en iyi uygulamalarını ve bu GET isteklerinin uygulamanızın [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) durumunu değiştirmemelidir. Diğer bir deyişle, bir GET işleminin gerçekleştirilmesi, yan etkileri olmayan ve kalıcı verilerinizi değiştirmeyen bir güvenli işlem olmalıdır.

## <a name="adding-a-search-method-and-search-view"></a>Arama yöntemi ve arama görünümü ekleme

Bu bölümde, `SearchIndex` film tarzında veya ada göre arama yapmanızı sağlayan bir eylem yöntemi ekleyeceksiniz. Bu, */movies/SearchIndex* URL 'si kullanılarak kullanılabilir. İstek, bir kullanıcının filmi arayacaktır girebileceği giriş öğelerini içeren bir HTML formu görüntüler. Bir Kullanıcı formu gönderdiğinde, eylem yöntemi kullanıcı tarafından gönderilen arama değerlerini alır ve bu verileri veritabanında aramak için kullanır.

## <a name="displaying-the-searchindex-form"></a>Searchındex formunu görüntüleme

`SearchIndex`Varolan sınıfa bir eylem yöntemi ekleyerek başlayın `MoviesController` . Yöntemi, HTML formu içeren bir görünüm döndürür. Kod şu şekildedir:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Yöntemin ilk satırı, `SearchIndex` filmleri seçmek için aşağıdaki [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgusunu oluşturur:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

Sorgu bu noktada tanımlandı, ancak henüz veri deposunda çalıştırılmadı.

`searchString`Parametresi bir dize içeriyorsa, filmler sorgusu, aşağıdaki kodu kullanarak arama dizesinin değerine göre filtreleyecek şekilde değiştirilir:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

`s => s.Title`Yukarıdaki kod bir [lambda ifadesidir](https://msdn.microsoft.com/library/bb397687.aspx). Lambdalar, yukarıdaki kodda kullanılan [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) yöntemi gibi standart sorgu işleci yöntemlerine bağımsız değişkenler olarak Yöntem tabanlı [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgularında kullanılır. LINQ sorguları tanımlandıklarında veya veya gibi bir yöntem çağırarak değiştirildiklerinde yürütülmez `Where` `OrderBy` . Bunun yerine, sorgu yürütmesi ertelenir, bu da bir ifadenin değerlendirmesinin, gerçekleştirilmiş değeri gerçekten üzerinde yinelenene veya yöntem çağrılana kadar gecikildiği anlamına gelir [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `SearchIndex`Örnekte, sorgu Searchındex görünümünde yürütülür. Ertelenmiş sorgu yürütme hakkında daha fazla bilgi için bkz. [sorgu yürütme](https://msdn.microsoft.com/library/bb738633.aspx).

Artık `SearchIndex` formu kullanıcıya görüntüleyecek görünümü uygulayabilirsiniz. Metodun içine sağ tıklayın `SearchIndex` ve ardından **Görünüm Ekle**' ye tıklayın. **Görünüm Ekle** iletişim kutusunda, bir `Movie` nesneyi model sınıfı olarak görünüm şablonuna geçileyeceksiniz. **Scaffold şablonu** listesinde **liste**' yi seçin ve ardından **Ekle**' ye tıklayın.

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

**Ekle** düğmesine tıkladığınızda, *Views\Movies\SearchIndex.cshtml* View şablonu oluşturulur. **Yapı iskelesi şablon** listesinde **liste** ' yi seçtiğiniz için, Visual Studio otomatik olarak (scafkatlamalı) görünümdeki bazı varsayılan biçimlendirmeleri otomatik olarak oluşturdu. Scafkatlama bir HTML formu oluşturdu. Sınıfı inceledi `Movie` ve `<label>` sınıfın her özelliği için öğeleri işlemek üzere kod oluşturdu. Aşağıdaki listede, oluşturulan oluşturma görünümü gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

Uygulamayı çalıştırın ve */movies/SearchIndex*adresine gidin. URL 'ye gibi bir sorgu dizesi ekleyin `?searchString=ghost` . Filtrelenmiş filmler görüntülenir.

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

`SearchIndex`Yönteminin imzasını adlı bir parametreye sahip olacak şekilde değiştirirseniz `id` , `id` parametresi `{id}` *Global. asax* dosyasında ayarlanan varsayılan yolların yer tutucusuyla eşleşir.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

Özgün `SearchIndex` Yöntem şöyle görünür::

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

Değiştirilen `SearchIndex` Yöntem şöyle görünür:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

Artık arama başlığını sorgu dizesi değeri yerine rota verileri (bir URL segmenti) olarak geçirebilirsiniz.

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

Ancak, kullanıcıların bir filmi her arayışınızda URL 'YI değiştirmesini beklemeniz gerekmez. Böylece, filmlerin filtrelemesine yardımcı olmak için Kullanıcı arabirimi ekleyeceğiz. `SearchIndex`Yol ile bağlantılı kimlik parametresinin nasıl geçirileceğini test etmek için yönteminin imzasını değiştirdiyseniz, `SearchIndex` yönteminizin adlı bir dize parametresi alması için geri değiştirin `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

*Views\Movies\SearchIndex.cshtml* dosyasını açın ve hemen sonra `@Html.ActionLink("Create New", "Create")` aşağıdakileri ekleyin:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

Aşağıdaki örnek, eklenen filtreleme işaretlemesi ile *Views\Movies\SearchIndex.cshtml* dosyasının bir bölümünü gösterir.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`Yardımcı, bir açılış `<form>` etiketi oluşturur. `Html.BeginForm`Yardımcı, Kullanıcı **filtre** düğmesine tıklayarak formu gönderdiğinde formun kendine göndermesine neden olur.

Uygulamayı çalıştırın ve bir filmi aramayı deneyin.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

`HttpPost`Metodun aşırı yüklemesi yoktur `SearchIndex` . Bunun için gerekli değildir çünkü yöntem uygulamanın durumunu değiştirmediğinden verileri filtrelememeniz yeterlidir.

Aşağıdaki `HttpPost SearchIndex` yöntemi ekleyebilirsiniz. Bu durumda, çalıştırılan eylem `HttpPost SearchIndex` yöntemiyle eşleşir ve `HttpPost SearchIndex` yöntemi aşağıdaki görüntüde gösterildiği gibi çalışır.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![Searchposthayalet](examining-the-edit-methods-and-edit-view/_static/image9.png)

Ancak, bu yöntemin bu sürümünü eklemeseniz bile `HttpPost` `SearchIndex` , tümünün nasıl uygulandığını gösteren bir sınırlama vardır. Belirli bir arama için yer işareti koymak istediğinizi veya aynı film filtrelenmiş listesini görmek için onlara tıklabilecekleri bir bağlantı göndermek istediğinizi düşünün. HTTP POST isteğinin URL 'SI GET isteğinin URL 'siyle (localhost: xxxxx/filmler/Searchındex) aynı olduğunu ve URL 'de arama bilgisi olmadığını unutmayın. Şu anda arama dizesi bilgileri sunucuya form alanı değeri olarak gönderilir. Bu, arama bilgilerini bir URL 'de yer işaretine veya arkadaşlara göndermek için yakalayamazsınız.

Çözüm, `BeginForm` Post ISTEĞININ URL 'ye arama bilgilerini eklemesi gerektiğini ve yöntemin HttpGet sürümüne yönlendirilmesini belirten bir aşırı yüklemesi kullanmaktır `SearchIndex` . Mevcut parametresiz `BeginForm` yöntemi aşağıdaki kodla değiştirin:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

Artık bir arama gönderdiğinizde URL bir arama sorgu dizesi içerir. `HttpGet SearchIndex`Bir yönteminiz olsa da, arama eylem yöntemine de gidecektir `HttpPost SearchIndex` .

![Searchındexwithgeturl](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>Türe göre arama ekleme

`HttpPost`Yöntemin sürümünü eklediyseniz `SearchIndex` , şimdi silin.

Daha sonra, kullanıcıların film tarza göre aramasını sağlamak için bir özellik ekleyeceksiniz. `SearchIndex` yöntemini aşağıdaki kod ile değiştirin:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

Yöntemin bu sürümü `SearchIndex` ek bir parametre alır, yani `movieGenre` . İlk birkaç kod satırı, `List` veritabanından film tarzları tutacak bir nesne oluşturur.

Aşağıdaki kod, veritabanından tüm tarzları alan bir LINQ sorgusudur.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

Kod, `AddRange` `List` tüm benzersiz tarzları listeye eklemek için genel koleksiyonun yöntemini kullanır. (Değiştirici olmadan `Distinct` yinelenen tarzlar eklenir — Örneğin, örneğimizde komedi iki kez eklenir). Daha sonra kod, nesne içindeki tarzların listesini depolar `ViewBag` .

Aşağıdaki kod, parametresinin nasıl kontrol alınacağını gösterir `movieGenre` . Boş değilse, kod, seçili filmleri belirtilen tarzya sınırlamak için film sorgusunu daha da kısıtlar.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Tarza göre aramayı desteklemek için Searchındex görünümüne biçimlendirme ekleme

`Html.DropDownList` *Views\Movies\SearchIndex.cshtml* dosyasına yardımcı olan bir yardımcı ekleyin `TextBox` . Tamamlanan biçimlendirme aşağıda gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

Uygulamayı çalıştırın ve */movies/SearchIndex*konumuna gidin. Türe göre, film adına ve her iki ölçüte göre arama yapmayı deneyin.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

Bu bölümde, çerçeve tarafından oluşturulan CRUD eylem yöntemlerini ve görünümlerini inceledi. Kullanıcıların film başlığına ve tarzına göre arama yapmasına izin veren bir arama eylemi yöntemi ve görünümü oluşturdunuz. Sonraki bölümde, modele nasıl özellik ekleneceğini `Movie` ve otomatik olarak bir test veritabanı oluşturacak Başlatıcı nasıl ekleneceğini inceleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](accessing-your-models-data-from-a-controller.md) 
>  [Sonraki](adding-a-new-field-to-the-movie-model-and-table.md)
