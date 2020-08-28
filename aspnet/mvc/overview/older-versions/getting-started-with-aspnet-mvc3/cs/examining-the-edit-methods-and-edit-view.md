---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: Düzenleme yöntemlerini ve düzenleme görünümünü İnceleme (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: baa300c66bfae9fe602a8fe597e21b0abbaf3a63
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044993"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>Düzenleme Metotlarını ve Düzenleme Görünümünü İnceleme (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.
> 
> 
> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> C# kaynak koduna sahip bir Visual Web Developer projesi, bu konuyla birlikte kullanılabilecek. [C# sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.

Bu bölümde, film denetleyicisi için oluşturulan eylem yöntemlerini ve görünümlerini inceleyeceksiniz. Ardından özel bir arama sayfası ekleyeceksiniz.

Uygulamayı çalıştırın ve `Movies` tarayıcınızın adres ÇUBUĞUNDAKI URL 'ye */filmler* ekleyerek denetleyiciye gidin. Bağlantı yaptığı URL 'yi görmek için fare işaretçisini bir **düzenleme** bağlantısı üzerine tutun.

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Düzenleme** bağlantısı, `Html.ActionLink` *Views\Movies\Index.cshtml* görünümündeki yöntemi tarafından oluşturulmuştur:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html`Nesnesi, temel sınıftaki bir özellik kullanılarak ortaya çıkarılan bir yardımcıdır `WebViewPage` . `ActionLink`Yardımcı yöntemi, denetleyicilerde eylem yöntemlerine bağlantı sağlayan HTML köprülerini dinamik olarak oluşturmayı kolaylaştırır. Yöntemin ilk bağımsız değişkeni, `ActionLink` işlenecek bağlantı metindir (örneğin, `<a>Edit Me</a>` ). İkinci bağımsız değişken çağrılacak eylem yönteminin adıdır. Son bağımsız değişken, yol verilerini üreten [anonim bir nesnedir](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (Bu durumda, 4 ' ün kimliği).

Önceki görüntüde gösterilen oluşturulan bağlantı `http://localhost:xxxxx/Movies/Edit/4` . Varsayılan yol URL modelini alır `{controller}/{action}/{id}` . Bu nedenle, ASP.NET, `http://localhost:xxxxx/Movies/Edit/4` `Edit` denetleyicinin Action metoduna 4 ' e eşit olan bir isteğe çevirir `Movies` `ID` .

Ayrıca, bir sorgu dizesi kullanarak eylem yöntemi parametrelerini geçirebilirsiniz. Örneğin, URL `http://localhost:xxxxx/Movies/Edit?ID=4` Ayrıca `ID` 4 parametresini `Edit` denetleyicinin Action yöntemine geçirir `Movies` .

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

Denetleyiciyi açın `Movies` . İki `Edit` eylem yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

İkinci `Edit` eylem yönteminin önünde özniteliği olduğuna dikkat edin `HttpPost` . Bu öznitelik, yöntemin aşırı yüklemesinin `Edit` yalnızca post istekleri için çağrılabileceğini belirtir. `HttpGet`Özniteliği ilk düzenleme yöntemine uygulayabilirsiniz, ancak varsayılan değer olduğundan bu gerekli değildir. (Özniteliği Yöntem olarak örtük olarak atanmış eylem yöntemlerine başvuracağız `HttpGet` `HttpGet` .)

`HttpGet` `Edit` Yöntemi, film kimliği parametresini alır, Entity Framework yöntemini kullanarak filmi arar `Find` ve seçili filmi düzenleme görünümüne döndürür. Scafkatlama sistemi düzenleme görünümü oluştururken, sınıfını ve `Movie` `<label>` `<input>` sınıfının her bir özelliği için işlenecek kodu ve öğelerini inceledi. Aşağıdaki örnek, oluşturulan düzenleme görünümünü göstermektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

Görünüm şablonunun dosyanın en üstünde bir ifadeye sahip olduğuna dikkat edin `@model MvcMovie.Models.Movie` ; Bu, görünümün görünüm şablonu için modelin tür olmasını beklediğini belirtir `Movie` .

Scafkatlanmış kod, HTML işaretlemesini kolaylaştırmak için çeşitli *yardımcı yöntemler* kullanır. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Yardımcı, alanın adını ("title", "ReleaseDate", "tarz" veya "Price") görüntüler. [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Yardımcı, BIR HTML `<input>` öğesi görüntüler. [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Yardımcı, bu özellikle ilişkili tüm doğrulama iletilerini görüntüler.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bir **düzenleme** bağlantısına tıklayın. Tarayıcıda, sayfanın kaynağını görüntüleyin. Sayfadaki HTML aşağıdaki örneğe benzer şekilde görünür. (Menü biçimlendirme açıklık için dışlandı.)

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

`<input>`Öğeleri `<form>` `action` özniteliği */movies/Edit* URL 'SINE postala olarak ayarlanmış bir HTML öğesi. Form verileri, **Düzenle** düğmesine tıklandığında sunucuya gönderilir.

## <a name="processing-the-post-request"></a>POST Isteği işleniyor

Aşağıdaki listede `HttpPost` `Edit` eylem yönteminin sürümü gösterilmektedir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

ASP.NET Framework model Ciltçi, postalanan form değerlerini alır ve `Movie` parametresi olarak geçirilmiş bir nesne oluşturur `movie` . `ModelState.IsValid`Koddaki denetim, formda gönderilen verilerin bir nesneyi değiştirmek için kullanılabileceğini doğrular `Movie` . Veriler geçerliyse kod, film verilerini `Movies` örnek koleksiyonuna kaydeder `MovieDBContext` . Daha sonra kod, `SaveChanges` `MovieDBContext` veritabanında değişiklik devam eden yöntemini çağırarak yeni film verilerini veritabanına kaydeder. Veriler kaydedildikten sonra, kod, kullanıcıyı `Index` sınıfının Action yöntemine yönlendirir `MoviesController` , bu da güncelleştirilmiş filmin film listesinde görüntülenmesine neden olur.

Postalanan değerler geçerli değilse, formda yeniden görüntülenir. `Html.ValidationMessageFor` *Edit. cshtml* görünüm şablonundaki yardımcılar, uygun hata iletilerini görüntülemeyi dikkate alır.

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **Yerel ayarlar hakkında** Normalde Ingilizce dışındaki bir yerel ayarda çalışıyorsanız bkz [. Ingilizce olmayan yerel ayarlarda ASP.NET MVC 3 doğrulamasını destekleme.](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)

## <a name="making-the-edit-method-more-robust"></a>Düzenleme yöntemini daha sağlam hale getirme

`HttpGet` `Edit` Yapı iskelesi sistemi tarafından oluşturulan yöntem, kendısıne geçirilen kimliğin geçerli olduğunu denetlemez. Bir Kullanıcı KIMLIK kesimini URL 'den () kaldırırsa `http://localhost:xxxxx/Movies/Edit` aşağıdaki hata görüntülenir:

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

Bir Kullanıcı, veritabanında mevcut olmayan bir KIMLIĞI de geçirebilir (gibi) `http://localhost:xxxxx/Movies/Edit/1234` . `HttpGet` `Edit` Bu kısıtlamayı gidermek için eylem yönteminde iki değişiklik yapabilirsiniz. İlk olarak, `ID` BIR kimlik açıkça geçirilmediğinde parametreyi varsayılan değeri sıfır olacak şekilde değiştirin. Ayrıca, `Find` bir film nesnesini görünüm şablonuna döndürmeden önce metodun gerçekten bir filmi bulduğundan emin olabilirsiniz. Updated `Edit` yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

Hiçbir film bulunamazsa `HttpNotFound` yöntem çağrılır.

Tüm `HttpGet` Yöntemler benzer bir düzene uyar. Bir film nesnesi (veya bunun durumunda nesne listesi `Index` ) alır ve modeli görünüme iletir. `Create`Yöntemi, oluşturma görünümüne boş bir film nesnesi geçirir. Verileri oluşturan, düzenleme, silme veya başka bir şekilde değiştiren tüm yöntemler `HttpPost` , yönteminin aşırı yüküne neden olacak. HTTP GET yöntemindeki verileri değiştirmek, Web günlüğü gönderi girişi [ASP.NET MVC ipucu #46 – güvenlik delikleri oluşturdukları Için silme bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET yöntemindeki verileri değiştirmek, HTTP en iyi uygulamalarını ve bu GET isteklerinin uygulamanızın durumunu değiştirmemelidir. Diğer bir deyişle, bir GET işleminin gerçekleştirilmesi, yan etkileri olmayan bir güvenli işlem olmalıdır.

## <a name="adding-a-search-method-and-search-view"></a>Arama yöntemi ve arama görünümü ekleme

Bu bölümde, `SearchIndex` film tarzında veya ada göre arama yapmanızı sağlayan bir eylem yöntemi ekleyeceksiniz. Bu, */movies/SearchIndex* URL 'si kullanılarak kullanılabilir. İstek, bir kullanıcının filmi aramak için dolduracağı giriş öğelerini içeren bir HTML formu görüntüler. Bir Kullanıcı formu gönderdiğinde, eylem yöntemi kullanıcı tarafından gönderilen arama değerlerini alır ve bu verileri veritabanında aramak için kullanır.

## <a name="displaying-the-searchindex-form"></a>Searchındex formunu görüntüleme

`SearchIndex`Varolan sınıfa bir eylem yöntemi ekleyerek başlayın `MoviesController` . Yöntemi, HTML formu içeren bir görünüm döndürür. Kod şu şekildedir:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

Yöntemin ilk satırı, `SearchIndex` filmleri seçmek için aşağıdaki [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgusunu oluşturur:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

Sorgu bu noktada tanımlandı, ancak henüz veri deposunda çalıştırılmadı.

`searchString`Parametresi bir dize içeriyorsa, filmler sorgusu, aşağıdaki kodu kullanarak arama dizesinin değerine göre filtreleyecek şekilde değiştirilir:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

LINQ sorguları tanımlandıklarında veya veya gibi bir yöntem çağırarak değiştirildiklerinde yürütülmez `Where` `OrderBy` . Bunun yerine, sorgu yürütmesi ertelenir, bu da bir ifadenin değerlendirmesinin, gerçekleştirilmiş değeri gerçekten üzerinde yinelenene veya yöntem çağrılana kadar gecikildiği anlamına gelir [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `SearchIndex`Örnekte, sorgu Searchındex görünümünde yürütülür. Ertelenmiş sorgu yürütme hakkında daha fazla bilgi için bkz. [sorgu yürütme](https://msdn.microsoft.com/library/bb738633.aspx).

Artık `SearchIndex` formu kullanıcıya görüntüleyecek görünümü uygulayabilirsiniz. Metodun içine sağ tıklayın `SearchIndex` ve ardından **Görünüm Ekle**' ye tıklayın. **Görünüm Ekle** iletişim kutusunda, bir `Movie` nesneyi model sınıfı olarak görünüm şablonuna geçileyeceksiniz. **Scaffold şablonu** listesinde **liste**' yi seçin ve ardından **Ekle**' ye tıklayın.

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

**Ekle** düğmesine tıkladığınızda, *Views\Movies\SearchIndex.cshtml* View şablonu oluşturulur. **Yapı iskelesi şablon** listesinde **liste** ' yi seçtiğiniz Için, Visual Web Developer, görünümdeki bazı varsayılan içerikleri otomatik olarak oluşturdu (scafkatlamalı). Scafkatlama bir HTML formu oluşturdu. Sınıfı inceledi `Movie` ve `<label>` sınıfın her özelliği için öğeleri işlemek üzere kod oluşturdu. Aşağıdaki listede, oluşturulan oluşturma görünümü gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Uygulamayı çalıştırın ve */movies/SearchIndex*adresine gidin. URL 'ye gibi bir sorgu dizesi ekleyin `?searchString=ghost` . Filtrelenmiş filmler görüntülenir.

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

`SearchIndex`Yönteminin imzasını adlı bir parametreye sahip olacak şekilde değiştirirseniz `id` , `id` parametresi `{id}` *Global. asax* dosyasında ayarlanan varsayılan yolların yer tutucusuyla eşleşir.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

Değiştirilen `SearchIndex` Yöntem şöyle görünür:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

Artık arama başlığını sorgu dizesi değeri yerine rota verileri (bir URL segmenti) olarak geçirebilirsiniz.

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

Ancak, kullanıcıların bir filmi her arayışınızda URL 'YI değiştirmesini beklemeniz gerekmez. Böylece, filmlerin filtrelemesine yardımcı olmak için Kullanıcı arabirimi ekleyeceğiz. `SearchIndex`Yol ile bağlantılı kimlik parametresinin nasıl geçirileceğini test etmek için yönteminin imzasını değiştirdiyseniz, `SearchIndex` yönteminizin adlı bir dize parametresi alması için geri değiştirin `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

*Views\Movies\SearchIndex.cshtml* dosyasını açın ve hemen sonra `@Html.ActionLink("Create New", "Create")` aşağıdakileri ekleyin:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

Aşağıdaki örnek, eklenen filtreleme işaretlemesi ile *Views\Movies\SearchIndex.cshtml* dosyasının bir bölümünü gösterir.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

`Html.BeginForm`Yardımcı, bir açılış `<form>` etiketi oluşturur. `Html.BeginForm`Yardımcı, Kullanıcı **filtre** düğmesine tıklayarak formu gönderdiğinde formun kendine göndermesine neden olur.

Uygulamayı çalıştırın ve bir filmi aramayı deneyin.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

`HttpPost`Metodun aşırı yüklemesi yoktur `SearchIndex` . Bunun için gerekli değildir çünkü yöntem uygulamanın durumunu değiştirmediğinden verileri filtrelememeniz yeterlidir.

Aşağıdaki `HttpPost SearchIndex` yöntemi ekleyebilirsiniz. Bu durumda, çalıştırılan eylem `HttpPost SearchIndex` yöntemiyle eşleşir ve `HttpPost SearchIndex` yöntemi aşağıdaki görüntüde gösterildiği gibi çalışır.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![Searchposthayalet](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

Ancak, bu yöntemin bu sürümünü eklemeseniz bile `HttpPost` `SearchIndex` , tümünün nasıl uygulandığını gösteren bir sınırlama vardır. Belirli bir arama için yer işareti koymak istediğinizi veya aynı film filtrelenmiş listesini görmek için onlara tıklabilecekleri bir bağlantı göndermek istediğinizi düşünün. HTTP POST isteğinin URL 'SI GET isteğinin URL 'siyle (localhost: xxxxx/filmler/Searchındex) aynı olduğunu ve URL 'de arama bilgisi olmadığını unutmayın. Şu anda arama dizesi bilgileri sunucuya form alanı değeri olarak gönderilir. Bu, arama bilgilerini bir URL 'de yer işaretine veya arkadaşlara göndermek için yakalayamazsınız.

Çözüm, `BeginForm` Post ISTEĞININ URL 'ye arama bilgilerini eklemesi gerektiğini ve yöntemin HttpGet sürümüne yönlendirildiğini belirten bir aşırı yüklemesi kullanmaktır `SearchIndex` . Mevcut parametresiz `BeginForm` yöntemi aşağıdaki kodla değiştirin:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

Artık bir arama gönderdiğinizde URL bir arama sorgu dizesi içerir. `HttpGet SearchIndex`Bir yönteminiz olsa da, arama eylem yöntemine de gidecektir `HttpPost SearchIndex` .

[![Searchındexwithgeturl](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>Türe göre arama ekleme

`HttpPost`Yöntemin sürümünü eklediyseniz `SearchIndex` , şimdi silin.

Daha sonra, kullanıcıların film tarza göre aramasını sağlamak için bir özellik ekleyeceksiniz. `SearchIndex` yöntemini aşağıdaki kod ile değiştirin:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

Yöntemin bu sürümü `SearchIndex` ek bir parametre alır, yani `movieGenre` . İlk birkaç kod satırı, `List` veritabanından film tarzları tutacak bir nesne oluşturur.

Aşağıdaki kod, veritabanından tüm tarzları alan bir LINQ sorgusudur.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

Kod, `AddRange` `List` tüm benzersiz tarzları listeye eklemek için genel koleksiyonun yöntemini kullanır. (Değiştirici olmadan `Distinct` yinelenen tarzlar eklenir — Örneğin, örneğimizde komedi iki kez eklenir). Daha sonra kod, nesne içindeki tarzların listesini depolar `ViewBag` .

Aşağıdaki kod, parametresinin nasıl kontrol alınacağını gösterir `movieGenre` . Boş değilse kod, film sorgusunun seçili filmleri belirtilen tarzya sınırlamak için daha fazla kısıtlar.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Tarza göre aramayı desteklemek için Searchındex görünümüne biçimlendirme ekleme

`Html.DropDownList` *Views\Movies\SearchIndex.cshtml* dosyasına yardımcı olan bir yardımcı ekleyin `TextBox` . Tamamlanan biçimlendirme aşağıda gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

Uygulamayı çalıştırın ve */movies/SearchIndex*konumuna gidin. Türe göre, film adına ve her iki ölçüte göre arama yapmayı deneyin.

Bu bölümde, çerçeve tarafından oluşturulan CRUD eylem yöntemlerini ve görünümlerini inceledi. Kullanıcıların film başlığına ve tarzına göre arama yapmasına izin veren bir arama eylemi yöntemi ve görünümü oluşturdunuz. Sonraki bölümde, modele nasıl özellik ekleneceğini `Movie` ve otomatik olarak bir test veritabanı oluşturacak Başlatıcı nasıl ekleneceğini inceleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](accessing-your-models-data-from-a-controller.md) 
>  [Sonraki](adding-a-new-field.md)
