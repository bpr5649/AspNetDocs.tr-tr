---
uid: mvc/overview/getting-started/introduction/adding-search
title: Ara | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211470"
---
# <a name="search"></a>Arama

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a>Arama yöntemi ve arama görünümü ekleme

Bu bölümde, `Index` bir türe veya ada göre filmlere göre arama yapmanızı sağlayan eylem yöntemine arama özelliği ekleyeceksiniz.

## <a name="prerequisites"></a>Önkoşullar

Bu bölümün ekran görüntülerini eşleştirmek için, uygulamayı (F5) çalıştırmanız ve aşağıdaki filmleri veritabanına eklemeniz gerekir.

| Title | Yayın Tarihi | Tarzı | Fiyat |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | Komedi | 6,99 |
| Ghostbusters II | 6/16/1989 | Komedi | 6,99 |
| Apes 'nin Planet | 3/27/1986 | Eylem | 5,99 |

## <a name="updating-the-index-form"></a>Dizin formunu güncelleştirme

`Index`Eylem yöntemini mevcut sınıfa güncelleştirerek başlayın `MoviesController` . Kod şu şekildedir:

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

Yöntemin ilk satırı, `Index` filmleri seçmek için aşağıdaki [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgusunu oluşturur:

[!code-csharp[Main](adding-search/samples/sample2.cs)]

Sorgu bu noktada tanımlandı, ancak henüz veritabanında çalıştırılmadı.

`searchString`Parametresi bir dize içeriyorsa, filmler sorgusu, aşağıdaki kodu kullanarak arama dizesinin değerine göre filtreleyecek şekilde değiştirilir:

[!code-csharp[Main](adding-search/samples/sample3.cs)]

`s => s.Title`Yukarıdaki kod bir [lambda ifadesidir](https://msdn.microsoft.com/library/bb397687.aspx). Lambdalar, yukarıdaki kodda kullanılan [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) yöntemi gibi standart sorgu işleci yöntemlerine bağımsız değişkenler olarak Yöntem tabanlı [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgularında kullanılır. LINQ sorguları tanımlandıklarında veya veya gibi bir yöntem çağırarak değiştirildiklerinde yürütülmez `Where` `OrderBy` . Bunun yerine, sorgu yürütmesi ertelenir, bu da bir ifadenin değerlendirmesinin, gerçekleştirilmiş değeri gerçekten üzerinde yinelenene veya yöntem çağrılana kadar gecikildiği anlamına gelir [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `Search`Örnekte, sorgu *Index. cshtml* görünümünde yürütülür. Ertelenmiş sorgu yürütme hakkında daha fazla bilgi için bkz. [sorgu yürütme](https://msdn.microsoft.com/library/bb738633.aspx).

> [!NOTE]
> [Contains](https://msdn.microsoft.com/library/bb155125.aspx) yöntemi, yukarıdaki c# kodu değil, veritabanında çalıştırılır. Veritabanında [SQL gibi](https://msdn.microsoft.com/library/ms179859.aspx)eşlemeler [içerir](https://msdn.microsoft.com/library/bb155125.aspx) , büyük/küçük harfe duyarsız olur.

Artık `Index` formu kullanıcıya görüntüleyecek görünümü güncelleştirebilirsiniz.

Uygulamayı çalıştırın ve */movies/Index*adresine gidin. URL 'ye gibi bir sorgu dizesi ekleyin `?searchString=ghost` . Filtrelenmiş filmler görüntülenir.

![SearchQryStr](adding-search/_static/image1.png)

`Index`Yönteminin imzasını adlı bir parametreye sahip olacak şekilde değiştirirseniz `id` , `id` parametresi `{id}` *App \_ start\routeconfig.cs* dosyasında ayarlanan varsayılan yolların yer tutucusuyla eşleşir.

[!code-json[Main](adding-search/samples/sample4.json)]

Özgün `Index` Yöntem şöyle görünür::

[!code-csharp[Main](adding-search/samples/sample5.cs)]

Değiştirilen `Index` Yöntem şöyle görünür:

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

Artık arama başlığını sorgu dizesi değeri yerine rota verileri (bir URL segmenti) olarak geçirebilirsiniz.

![](adding-search/_static/image2.png)

Ancak, kullanıcıların bir filmi her arayışınızda URL 'YI değiştirmesini beklemeniz gerekmez. Böylece, filmlerin filtrelemesine yardımcı olmak için Kullanıcı arabirimi ekleyeceğiz. `Index`Yol ile bağlantılı kimlik parametresinin nasıl geçirileceğini test etmek için yönteminin imzasını değiştirdiyseniz, `Index` yönteminizin adlı bir dize parametresi alması için geri değiştirin `searchString` :

[!code-csharp[Main](adding-search/samples/sample7.cs)]

*Views\Movies\Index.cshtml* dosyasını açın ve hemen sonra `@Html.ActionLink("Create New", "Create")` vurgulanan form işaretlemesini ekleyin:

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

`Html.BeginForm`Yardımcı, bir açılış `<form>` etiketi oluşturur. `Html.BeginForm`Yardımcı, Kullanıcı **filtre** düğmesine tıklayarak formu gönderdiğinde formun kendine göndermesine neden olur.

Visual Studio 2013, görüntüleme dosyalarını görüntülerken ve düzenlenirken iyi bir iyileştirmedir. Uygulamayı bir görünüm dosyası açıkken çalıştırdığınızda Visual Studio 2013, görünümü görüntülemek için doğru denetleyici eylemi yöntemini çağırır.

![](adding-search/_static/image3.png)

Visual Studio 'da (yukarıdaki görüntüde gösterildiği gibi) dizin görünümü açık olduğunda, uygulamayı çalıştırmak için Mrk F5 veya F5 ' e dokunun ve ardından bir filmi aramayı deneyin.

![](adding-search/_static/image4.png)

`HttpPost`Metodun aşırı yüklemesi yoktur `Index` . Bunun için gerekli değildir çünkü yöntem uygulamanın durumunu değiştirmediğinden verileri filtrelememeniz yeterlidir.

Aşağıdaki `HttpPost Index` yöntemi ekleyebilirsiniz. Bu durumda, çalıştırılan eylem `HttpPost Index` yöntemiyle eşleşir ve `HttpPost Index` yöntemi aşağıdaki görüntüde gösterildiği gibi çalışır.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![Searchposthayalet](adding-search/_static/image5.png)

Ancak, bu yöntemin bu sürümünü eklemeseniz bile `HttpPost` `Index` , tümünün nasıl uygulandığını gösteren bir sınırlama vardır. Belirli bir arama için yer işareti koymak istediğinizi veya aynı film filtrelenmiş listesini görmek için onlara tıklabilecekleri bir bağlantı göndermek istediğinizi düşünün. HTTP POST isteğinin URL 'SI GET isteğinin URL 'siyle (localhost: xxxxx/filmler/dizin) aynı olduğunu ve URL 'de arama bilgisi olmadığını unutmayın. Şu anda arama dizesi bilgileri sunucuya form alanı değeri olarak gönderilir. Bu, arama bilgilerini bir URL 'de yer işaretine veya arkadaşlara göndermek için yakalayamazsınız.

Çözüm, `BeginForm` Post ISTEĞININ URL 'ye arama bilgilerini eklemesi gerektiğini ve yöntemin sürümüne yönlendirilmesini belirten bir aşırı yüklemesi kullanmaktır `HttpGet` `Index` . Mevcut parametresiz `BeginForm` yöntemi aşağıdaki biçimlendirme ile değiştirin:

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

Artık bir arama gönderdiğinizde URL bir arama sorgu dizesi içerir. `HttpGet Index`Bir yönteminiz olsa da, arama eylem yöntemine de gidecektir `HttpPost Index` .

![Indexwithgeturl](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>Türe göre arama ekleme

`HttpPost`Yöntemin sürümünü eklediyseniz `Index` , şimdi silin.

Daha sonra, kullanıcıların film tarza göre aramasını sağlamak için bir özellik ekleyeceksiniz. `Index` yöntemini aşağıdaki kod ile değiştirin:

[!code-csharp[Main](adding-search/samples/sample11.cs)]

Yöntemin bu sürümü `Index` ek bir parametre alır, yani `movieGenre` . İlk birkaç kod satırı, `List` veritabanından film tarzları tutacak bir nesne oluşturur.

Aşağıdaki kod, veritabanından tüm tarzları alan bir LINQ sorgusudur.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

Kod, `AddRange` `List` tüm benzersiz tarzları listeye eklemek için genel koleksiyonun yöntemini kullanır. (Değiştirici olmadan `Distinct` yinelenen tarzlar eklenir — Örneğin, örneğimizde komedi iki kez eklenir). Daha sonra kod, nesne içindeki tarzların listesini depolar `ViewBag.MovieGenre` . Kategori verilerini (film tarzları) içinde bir [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) nesnesi olarak depolama `ViewBag` , sonra bir açılan liste kutusunda Kategori VERILERINE erişme, MVC uygulamaları için tipik bir yaklaşımdır.

Aşağıdaki kod, parametresinin nasıl kontrol alınacağını gösterir `movieGenre` . Boş değilse, kod, seçili filmleri belirtilen tarzya sınırlamak için film sorgusunu daha da kısıtlar.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

Daha önce belirtildiği gibi, bir sorgu, film listesi üzerinde yinelenene kadar (görünümde, eylem yöntemi döndürüldüğünde gerçekleşen) veritabanı üzerinde çalışmaz `Index` .

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>Türe göre aramayı desteklemek için dizin görünümüne biçimlendirme ekleme

`Html.DropDownList` *Views\Movies\Index.cshtml* dosyasına yardımcı olan bir yardımcı ekleyin `TextBox` . Tamamlanan biçimlendirme aşağıda gösterilmektedir:

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

Aşağıdaki kodda:

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

"Movietarz" parametresi `DropDownList` , içinde bir içinde bulunacak yardımcı için anahtar sağlar `IEnumerable<SelectListItem>` `ViewBag` . `ViewBag`Eylem yönteminde doldurulmıştı:

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

"All" parametresi bir seçenek etiketi sağlar. Bu seçimi tarayıcınızda inceleyebilirsiniz, "Value" özniteliğinin boş olduğunu görürsünüz. Denetleyicimiz yalnızca dizeyi filtreleyerek `if` `null` veya boş olduğundan, için boş bir değer gönderilmesi `movieGenre` Tüm tarzları gösterir.

Ayrıca, varsayılan olarak seçilecek bir seçenek de ayarlayabilirsiniz. Varsayılan seçenek olarak "komedi" isterseniz, denetleyicideki kodu şöyle değiştirirsiniz:

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

Uygulamayı çalıştırın ve */movies/Index*konumuna gidin. Türe göre, film adına ve her iki ölçüte göre arama yapmayı deneyin.

![](adding-search/_static/image8.png)

Bu bölümde, kullanıcıların film başlığına ve tarzya göre arama yapmasına izin veren bir arama eylemi yöntemi ve görünümü oluşturdunuz. Sonraki bölümde, modele nasıl özellik ekleneceğini `Movie` ve otomatik olarak bir test veritabanı oluşturacak Başlatıcı nasıl ekleneceğini inceleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](examining-the-edit-methods-and-edit-view.md) 
>  [Sonraki](adding-a-new-field.md)
