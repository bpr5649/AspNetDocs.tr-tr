---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama (3/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484703"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama (3/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide, varlıkların temel CRUD işlemleri için bir dizi Web sayfası uyguladık `Student` . Bu öğreticide, **öğrenciler** dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliği ekleyeceksiniz. Ayrıca basit gruplandırma yapan bir sayfa oluşturacaksınız.

Aşağıdaki çizimde, işiniz bittiğinde sayfanın nasıl görüneceği gösterilmektedir. Sütun başlıkları, kullanıcının sütuna göre sıralamak için tıkladığı bağlantılardır. Sütun başlığına tıklanması artan ve azalan sıralama düzeni arasında sürekli olarak geçiş yapar.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>Öğrenciler dizin sayfasına sütun sıralama bağlantıları Ekle

Öğrenci dizini sayfasına sıralama eklemek için `Index` denetleyicinin yöntemini değiştirecek `Student` ve `Student` Dizin görünümüne kod ekleyeceksiniz.

### <a name="add-sorting-functionality-to-the-index-method"></a>Dizin yöntemine sıralama Işlevi ekleme

*Controllers\studentcontroller.cs*içinde, `Index` yöntemi aşağıdaki kodla değiştirin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Bu kod `sortOrder` , URL 'deki sorgu dizesinden bir parametre alır. Sorgu dizesi değeri, ASP.NET MVC tarafından eylem yöntemine bir parametre olarak sağlanır. Parametresi, "Name" veya "Date" adlı bir dize, isteğe bağlı olarak bir alt çizgi ve azalan sıralama belirtmek için "desc" dizesi olacaktır. Varsayılan sıralama düzeni artan.

Dizin sayfası ilk kez istendiğinde sorgu dizesi yoktur. Öğrenciler, `LastName` bildiriminde, bildirimde bulunan durum ile belirlenen varsayılan değer olan artan sırada görüntülenir `switch` . Kullanıcı bir sütun başlığı köprüsüne tıkladığında, `sortOrder` sorgu dizesinde uygun değer sağlanır.

İki `ViewBag` değişken, görünümün sütun başlığı köprülerini uygun sorgu dizesi değerleriyle yapılandırabilmesi için kullanılır:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Bunlar Üçlü ifadelerdir. Birincisi, `sortOrder` parametre null veya boş ise `ViewBag.NameSortParm` "ad desc" olarak ayarlanması gerektiğini belirtir \_ ; Aksi takdirde, boş bir dizeye ayarlanmalıdır. Bu iki deyim, görünümün sütun başlığı köprülerini şu şekilde ayarlamaya olanak tanır:

| Geçerli sıralama düzeni | Son ad Köprüsü | Tarih Köprüsü |
| --- | --- | --- |
| Artan son ad | descending | ascending |
| Azalan son ad | ascending | ascending |
| Artan Tarih | ascending | descending |
| Azalan Tarih | ascending | ascending |

Yöntemi, sıralama yapılacak sütunu belirtmek için [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) kullanır. Kod, deyimden önce bir [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) değişkeni oluşturur `switch` , `switch` deyimde değiştirir ve `ToList` deyimden sonra yöntemi çağırır `switch` . Değişkenleri oluşturup değiştirirken `IQueryable` veritabanına hiçbir sorgu gönderilmez. Sorgu, `IQueryable` gibi bir yöntemi çağırarak nesne bir koleksiyona dönüştürülene kadar yürütülmez `ToList` . Bu nedenle, bu kod, ifadeye kadar Yürütülmeyen tek bir sorgu ile sonuçlanır `return View` .

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Öğrenci dizini görünümüne sütun başlığı köprüleri ekleme

*Views\student\ındex.cshtml*içinde, `<tr>` `<th>` başlık satırı için ve öğelerini vurgulanan kodla değiştirin:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

Bu kod, `ViewBag` uygun sorgu dizesi değerleriyle köprüler ayarlamak için özelliklerindeki bilgileri kullanır.

Sıralamayı doğrulamak için sayfayı çalıştırın ve **son ad** ve **kayıt tarihi** sütun başlıklarına tıklayın.

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

**Son ad** başlığına tıkladıktan sonra, öğrenciler azalan son ad sırasıyla görüntülenir.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>Öğrenciler dizin sayfasına bir arama kutusu ekleyin

Öğrenciler dizin sayfasına filtre eklemek için, görünüme bir metin kutusu ve Gönder düğmesi ekleyeceksiniz ve yöntemde ilgili değişiklikleri yapmanız gerekir `Index` . Metin kutusu, ilk adı ve soyadı alanlarını aramak için bir dize girmenizi sağlar.

### <a name="add-filtering-functionality-to-the-index-method"></a>Dizin yöntemine filtreleme Işlevi ekleme

*Controllers\studentcontroller.cs*içinde, `Index` yöntemi aşağıdaki kodla değiştirin (değişiklikler vurgulanır):

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Yöntemine bir parametre eklediniz `searchString` `Index` . Ayrıca, `where` yalnızca adı veya soyadı arama dizesini içeren öğrencileri seçen LINQ deyimi a yan tümcesine de eklendiniz. Arama dizesi değeri, dizin görünümüne ekleyeceğiniz bir metin kutusundan alınır. [WHERE](https://msdn.microsoft.com/library/bb535040.aspx) yan tümcesini ekleyen deyimi, yalnızca aranacak bir değer varsa yürütülür.

> [!NOTE]
> Çoğu durumda, bir Entity Framework varlık kümesinde veya bir bellek içi koleksiyonda uzantı yöntemi olarak aynı yöntemi çağırabilirsiniz. Sonuçlar normalde aynıdır, ancak bazı durumlarda farklı olabilir. Örneğin, yöntemin .NET Framework uygulanması `Contains` boş bir dize geçirdiğinizde tüm satırları döndürür, ancak SQL Server Compact 4,0 Entity Framework sağlayıcısı boş dizeler için sıfır satır döndürür. Bu nedenle örnekteki kod (deyimin `Where` içinde deyimin yerleştirilmesi `if` ) tüm SQL Server sürümleri için aynı sonuçları almanızı sağlar. Ayrıca, yöntemi .NET Framework uygulama `Contains` Varsayılan olarak büyük/küçük harfe duyarlı bir karşılaştırma gerçekleştirir, ancak Entity Framework SQL Server sağlayıcılar varsayılan olarak büyük/küçük harfe duyarsız karşılaştırmalar yapar. Bu nedenle, `ToUpper` testi açık büyük/küçük harfe duyarsız hale getirmek için yöntemini çağırmak, daha sonra kodu bir nesne yerine bir koleksiyon döndürecek şekilde değiştirdiğinizde sonuçların değişmemesini sağlar `IEnumerable` `IQueryable` . ( `Contains` Bir koleksiyonda yöntemini çağırdığınızda `IEnumerable` .NET Framework uygulamasını alırsınız; bir nesne üzerinde çağırdığınızda `IQueryable` , veritabanı sağlayıcısı uygulamasını alırsınız.)

### <a name="add-a-search-box-to-the-student-index-view"></a>Öğrenci dizini görünümüne arama kutusu ekleme

*Views\student\ındex.cshtml*içinde, `table` bir başlık, metin kutusu ve bir **arama** düğmesi oluşturmak için, açılan etiketten hemen önce vurgulanan kodu ekleyin.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

Sayfayı çalıştırın, bir arama dizesi girin ve filtreleme 'nin çalıştığını doğrulamak için **Ara** ' ya tıklayın.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

URL 'nin "bir" arama dizesi içermediğini, yani bu sayfaya yer işareti eklerseniz, yer işaretini kullandığınızda filtrelenmiş listeyi almadığına dikkat edin. **Arama** düğmesini daha sonra öğreticide daha sonra filtre ölçütlerine yönelik Sorgu dizelerini kullanacak şekilde değiştirirsiniz.

## <a name="add-paging-to-the-students-index-page"></a>Öğrenciler dizin sayfasına sayfalama ekleme

Öğrenciler dizin sayfasına sayfalama eklemek için **Pagedlist. Mvc** NuGet paketini yükleyerek başlayacaksınız. Daha sonra, yöntemde ek değişiklikler yapar `Index` ve görünüme sayfalama bağlantıları ekleyebilirsiniz `Index` . **Pagedlist. Mvc** , ASP.NET MVC için çok iyi sayfalama ve sıralama paketlerinden biridir ve burada kullanılması, diğer seçeneklerin bir önerisi olarak değil yalnızca örnek olarak tasarlanmıştır. Aşağıdaki çizimde sayfalama bağlantıları gösterilmektedir.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList. MVC NuGet paketini yükler

NuGet **pagedlist. Mvc** paketi, **pagedlist** paketini otomatik olarak bir bağımlılık olarak yüklüyor. **Pagedlist** paketi, `PagedList` ve koleksiyonları için bir koleksiyon türü ve uzantı yöntemleri yüklüyor `IQueryable` `IEnumerable` . Uzantı yöntemleri, veya dışında bir koleksiyondaki verilerin tek bir sayfasını oluşturur `PagedList` `IQueryable` `IEnumerable` ve `PagedList` koleksiyon, sayfalama işlemini kolaylaştıran çeşitli özellikler ve yöntemler sağlar. **Pagedlist. Mvc** paketi, sayfalama düğmelerini görüntüleyen bir sayfalama Yardımcısı yüklüyor.

**Araçlar** menüsünde, **NuGet Paket Yöneticisi** ' ni ve ardından **çözüm için NuGet Paketlerini Yönet**' i seçin.

**NuGet Paketlerini Yönet** iletişim kutusunda, sol taraftaki **çevrimiçi** sekmesine tıklayın ve ardından arama kutusuna "Sayfalanmış" yazın. **Pagedlist. Mvc** paketini gördüğünüzde, **yükler**' e tıklayın.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

**Projeleri Seç** kutusunda **Tamam**' a tıklayın.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>Dizin yöntemine sayfalama Işlevselliği ekleme

*Controllers\studentcontroller.cs*içinde, `using` ad alanı için bir ifade ekleyin `PagedList` :

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` yöntemini aşağıdaki kod ile değiştirin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Bu kod, `page` burada gösterildiği gibi bir parametre, geçerli bir sıralama düzeni parametresi ve Yöntem imzasına geçerli bir filtre parametresi ekler:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Sayfa ilk kez görüntülenirken veya Kullanıcı bir sayfalama veya sıralama bağlantısına tıklamamışsa, tüm parametreler null olur. Bir sayfalama bağlantısına tıklandıysanız, `page` değişken görüntülenecek sayfa numarasını içerir.

`A ViewBag`özelliği geçerli sıralama düzeni ile görünüm sağlar, çünkü bu sıralama sırasını sayfalama sırasında aynı tutmak için disk belleği bağlantılarına dahil edilmesi gerekir:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Başka bir özellik, `ViewBag.CurrentFilter` geçerli filtre dizesiyle görünüm sağlar. Bu değer, disk belleği sırasında filtre ayarlarını korumak için disk belleği bağlantılarına dahil olmalıdır ve sayfa yeniden görüntülenirken metin kutusuna geri yüklenmesi gerekir. Arama dizesi sayfalama sırasında değiştirilmişse, yeni filtre farklı verilerin görüntülenmesini sağladığından sayfanın 1 olarak sıfırlanması gerekir. Metin kutusuna bir değer girildiğinde ve Gönder düğmesine basıldığında arama dizesi değişir. Bu durumda, `searchString` parametre null değil.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Yöntemin sonunda, `ToPagedList` öğrenciler nesnesindeki genişletme yöntemi `IQueryable` öğrenci sorgusunu, sayfalama destekleyen bir koleksiyon türünde tek bir öğrenciye dönüştürür. Bu tek bir öğrenci sayfası daha sonra görünüme geçirilir:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList`Yöntemi bir sayfa numarası alır. İki soru işareti, [null birleşim işlecini](https://msdn.microsoft.com/library/ms173224.aspx)temsil eder. Null birleşim işleci, Nullable bir tür için varsayılan değeri tanımlar; ifade `(page ?? 1)` `page` bir değer içeriyorsa değerini döndürür veya null ise 1 döndürür `page` .

### <a name="add-paging-links-to-the-student-index-view"></a>Öğrenci dizini görünümüne sayfalama bağlantıları ekleme

*Views\student\ındex.cshtml*içinde, mevcut kodu şu kodla değiştirin:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

`@model`Sayfanın üst kısmındaki ifade, görünümün artık nesne yerine bir nesne aldığından emin olarak belirtir `PagedList` `List` .

`using`İçin deyimleri, `PagedList.Mvc` SAYFALAMA düğmelerinin MVC Yardımcısı 'na erişim sağlar.

Kod, bir [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) aşırı yüklemesi kullanarak [FormMethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)belirlemesine izin verir.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

Varsayılan [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) , form VERILERINI bir gönderiyle gönderir, yani Parametreler, URL 'de sorgu dizeleri olarak değil http ileti gövdesinde geçirilir. HTTP GET belirttiğinizde, form verileri URL 'ye sorgu dizeleri olarak geçirilir ve bu da kullanıcıların URL 'ye yer işareti eklemesini sağlar. [Http get kullanımı Için W3C yönergeleri](http://www.w3.org/2001/tag/doc/whenToUseGet.html) , eylem bir güncelleştirme ile sonuçlanmayan Get ' i kullanmanız gerektiğini belirtir.

Metin kutusu geçerli arama dizesiyle başlatılır, böylece yeni bir sayfaya tıkladığınızda geçerli arama dizesini görebilirsiniz.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

Sütun üst bilgisi bağlantıları, kullanıcının filtre sonuçları içinde sıralama yapabilmesi için geçerli arama dizesini denetleyiciye geçirmek için sorgu dizesini kullanır:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

Geçerli sayfa ve toplam sayfa sayısı görüntülenir.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

Görüntülenecek sayfa yoksa, "sayfa 0/0" görüntülenir. (Bu durumda, 1 olan ve 0 olduğu için sayfa numarası sayfa sayısından daha büyük olur `Model.PageNumber` `Model.PageCount` .)

Sayfalama düğmeleri yardımcı tarafından görüntülenir `PagedListPager` :

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`Yardımcı, URL 'ler ve stil oluşturma da dahil olmak üzere özelleştirebilmeniz gereken birkaç seçenek sağlar. Daha fazla bilgi için GitHub sitesindeki [Troyıgocode/PagedList](https://github.com/TroyGoode/PagedList) bölümüne bakın.

Sayfayı çalıştırın.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Disk belleğinin çalıştığından emin olmak için farklı sıralama emirlerindeki disk belleği bağlantılarına tıklayın. Daha sonra bir arama dizesi girin ve sayfalama ve filtreleme ile doğru şekilde çalıştığını doğrulamak için sayfalama işlemi yeniden deneyin.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>Öğrenci Istatistiklerini gösteren bir hakkında sayfa oluşturun

Contoso Üniversitesi web sitesinin hakkında sayfasında, her bir kayıt tarihi için kaç öğrenciye kaydolduğunu görüntüleyeceksiniz. Bu, gruplar üzerinde gruplandırma ve basit hesaplamalar gerektirir. Bunu gerçekleştirmek için aşağıdakileri yapmanız gerekir:

- Görünüme geçirmeniz gereken veriler için bir görünüm modeli sınıfı oluşturun.
- `About`Denetleyicisindeki yöntemi değiştirin `Home` .
- Görünümü değiştirin `About` .

### <a name="create-the-view-model"></a>Görünüm modeli oluşturma

*Viewmodeller* klasörü oluşturun. Bu klasörde, *EnrollmentDateGroup.cs* bir sınıf dosyası ekleyin ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Ana denetleyiciyi değiştirme

*HomeController.cs*' de, `using` dosyanın en üstüne aşağıdaki deyimleri ekleyin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Sınıf için açma küme ayracından hemen sonra veritabanı bağlamı için bir sınıf değişkeni ekleyin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

`About` yöntemini aşağıdaki kod ile değiştirin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ beyanı, öğrenci varlıklarını kayıt tarihine göre gruplandırır, her bir gruptaki varlıkların sayısını hesaplar ve sonuçları bir `EnrollmentDateGroup` görünüm modeli nesneleri koleksiyonunda depolar.

Bir `Dispose` Yöntem ekleyin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Hakkında görünümünü değiştirme

*Views\home\about.exe* dosyasındaki kodu aşağıdaki kodla değiştirin:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

Uygulamayı çalıştırın ve **hakkında** bağlantısına tıklayın. Her kayıt tarihi için öğrenci sayısı bir tabloda görüntülenir.

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>İsteğe bağlı: uygulamayı Microsoft Azure 'a dağıtma

Bu nedenle, uygulamanız geliştirme bilgisayarınızda IIS Express yerel olarak çalışıyor. Diğer kişilerin Internet üzerinden kullanmasını sağlamak için, bir Web barındırma sağlayıcısına dağıtmanız gerekir. Öğreticinin isteğe bağlı bu bölümünde, Windows Azure Web sitesine dağıtırsınız.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Veritabanını dağıtmak için Code First Migrations kullanma

Veritabanını dağıtmak için Code First Migrations kullanırsınız. Visual Studio 'dan dağıtma ayarlarını yapılandırmak için kullandığınız yayımlama profilini oluşturduğunuzda, yürütme Code First Migrations etiketli bir onay kutusunu **(uygulama başlatıldığında çalışır)** seçersiniz. Bu ayar dağıtım işleminin, Code First Başlatıcı sınıfını kullanması için hedef sunucudaki uygulama *Web.config* dosyasını otomatik olarak yapılandırmasına neden olur `MigrateDatabaseToLatestVersion` .

Visual Studio, dağıtım işlemi sırasında veritabanıyla hiçbir şey yapmaz. Dağıtılan uygulama dağıtımdan sonra veritabanına ilk kez eriştiğinde, Code First otomatik olarak veritabanını oluşturur veya veritabanı şemasını en son sürüme güncelleştirir. Uygulama bir geçişler yöntemi uygularsa `Seed` , yöntem veritabanı oluşturulduktan sonra veya şema güncelleştirildikten sonra çalışır.

Geçişler `Seed` yönteminiz test verileri ekler. Bir üretim ortamına dağıtım yapıyorsanız, `Seed` yöntemi yalnızca üretim veritabanınıza eklemek istediğiniz verileri içerecek şekilde değiştirmeniz gerekir. Örneğin, geçerli veri modelinizde gerçek kurslar olmasını, ancak geliştirme veritabanında öğrenci öğrencilerine sahip olmak isteyebilirsiniz. `Seed`Geliştirme sırasında her ikisini de yüklemek için bir yöntem yazabilir ve ardından üretime dağıtmadan önce kurgusal öğrencileri açıklama olarak girebilirsiniz. Ya da `Seed` yalnızca kursları yüklemek için bir yöntem yazabilir ve uygulamanın kullanıcı arabirimini kullanarak test veritabanına kurgusal öğrencileri el ile girebilirsiniz.

### <a name="get-a-windows-azure-account"></a>Bir Windows Azure hesabı alın

Bir Windows Azure hesabınız olması gerekir. Henüz bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [Windows Azure Ücretsiz deneme](https://azure.microsoft.com/free/dotnet/).

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Microsoft Azure 'da bir Web sitesi ve SQL veritabanı oluşturma

Windows Azure Web siteniz, paylaşılan bir barındırma ortamında çalışacak ve bu, diğer Windows Azure istemcileriyle paylaşılan sanal makinelerde (VM) çalıştığı anlamına gelir. Paylaşılan barındırma ortamı, buluta başlamak için düşük maliyetli bir yoldur. Daha sonra, Web trafiğiniz arttıkça, uygulama adanmış VM 'lerde çalışırken ihtiyacı karşılayacak şekilde ölçeklendirebilir. Daha karmaşık bir mimariye ihtiyacınız varsa, bir Windows Azure bulut hizmetine geçiş yapabilirsiniz. Bulut Hizmetleri, gereksinimlerinize göre yapılandırabileceğiniz adanmış VM 'lerde çalışır.

Microsoft Azure SQL veritabanı, SQL Server teknolojileri üzerinde geliştirilen bulut tabanlı bir ilişkisel veritabanı hizmetidir. SQL Server ile birlikte çalışan araçlar ve uygulamalar SQL veritabanı ile de çalışır.

1. [Windows Azure yönetim portalı](https://manage.windowsazure.com/)sol sekmedeki **Web siteleri** ' ne ve ardından **Yeni**' ye tıklayın.

    ![Yönetim Portalı yeni düğme](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. **Özel oluştur**' a tıklayın.

    ![Yönetim Portalı veritabanı bağlantısıyla oluştur](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **Yeni Web sitesi-özel oluşturma** Sihirbazı açılır.
3. Sihirbazın **Yeni Web sitesi** adımında, **URL** kutusuna uygulamanızın benzersiz URL 'si olarak kullanılacak bir dize girin. URL 'nin tamamı buraya girdiklerinize ve metin kutusunun yanında gördüğünüz sonekine sahip olacaktır. Çizimde "ConU" gösterilir, ancak bu URL büyük olasılıkla başka bir tane seçmeniz gerekir.

    ![Yönetim Portalı veritabanı bağlantısıyla oluştur](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. **Bölge** açılan listesinde, size yakın bir bölge seçin. Bu ayar, Web sitenizin çalışacağı veri merkezini belirtir.
5. **Veritabanı** açılan listesinde, **ÜCRETSIZ 20 MB SQL veritabanı oluştur**' u seçin.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. **DB bağlantı DIZESI adı**alanına *SchoolContext*girin.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. Kutunun altındaki sağ tarafına işaret eden oka tıklayın. Sihirbaz **veritabanı ayarları** adımına ilerletir.
8. **Ad** kutusuna *Contosoevrensıtydb*yazın.
9. **Sunucu** kutusunda **Yeni SQL veritabanı sunucusu**' nu seçin. Alternatif olarak, daha önce bir sunucu oluşturduysanız, bu sunucuyu açılan listeden seçebilirsiniz.
10. Yönetici **oturum açma adı** ve **parolası**girin. **Yeni SQL Veritabanı sunucusu** öğesini seçtiyseniz buraya mevcut bir ad ve parola girmezsiniz, daha sonra veritabanına eriştiğinizde kullanmak üzere şimdi tanımlayacağınız yeni adı ve parolayı girersiniz. Daha önce oluşturduğunuz bir sunucu seçtiyseniz, bu sunucunun kimlik bilgilerini girersiniz. Bu öğreticide, ***Gelişmiş*** onay kutusunu seçemezsiniz. ***Gelişmiş*** seçenekler veritabanı [harmanlamasını](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)ayarlamanıza olanak sağlar.
11. Web sitesi için seçtiğiniz **bölgeyi** seçin.
12. Bittiğini göstermek için kutunun sağ alt kısmındaki onay işaretine tıklayın.   
  
    ![Yeni Web sitesinin veritabanı ayarları adımı-veritabanı ile oluşturma Sihirbazı](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    Aşağıdaki görüntüde, mevcut bir SQL Server ve oturum açmanın kullanılması gösterilmektedir.   
  
    ![Yeni Web sitesinin veritabanı ayarları adımı-veritabanı ile oluşturma Sihirbazı](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    Yönetim Portalı Web siteleri sayfasına döner ve **durum** sütunu sitenin oluşturulduğunu gösterir. Bir süre sonra (genellikle bir dakikadan kısa), **durum** sütunu sitenin başarıyla oluşturulduğunu gösterir. Sol taraftaki Gezinti çubuğunda, hesabınızda bulunan sitelerin sayısı **Web siteleri** simgesinin yanında görünür ve **SQL veritabanları** simgesinin yanında veritabanı sayısı görüntülenir.

## <a name="deploy-the-application-to-windows-azure"></a>Uygulamayı Windows Azure 'a dağıtma

1. Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.  
  
    ![Projede Yayımla bağlam menüsü](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. **Web 'ı Yayımla** sihirbazının **profil** sekmesinde **içeri aktar**' a tıklayın.  
  
    ![Yayımlama ayarlarını içeri aktar](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. Microsoft Azure aboneliğinizi Visual Studio 'Ya daha önce eklemediyseniz, aşağıdaki adımları uygulayın. Bu adımlarda, **bir Windows Azure Web sitesinden Içeri aktarma** bölümündeki açılır listenin Web sitenizi içermesini sağlamak için aboneliğinizi eklersiniz.

    a. **Yayımlama profilini Içeri aktar** iletişim kutusunda, **bir Windows Azure Web sitesinden içeri aktar ' a**tıklayın ve ardından **Windows Azure aboneliği Ekle**' ye tıklayın.

    ![Windows Azure aboneliği Ekle](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. **Windows Azure aboneliklerini Içeri aktar** iletişim kutusunda **abonelik dosyasını indir**' e tıklayın.

    ![abonelik dosyasını indir](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. Tarayıcı pencerenizde *. publishsettings* dosyasını kaydedin.

    ![. publishsettings dosyasını indirin](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > Güvenlik- *publishsettings* dosyası, Windows Azure aboneliklerinizi ve hizmetlerinizi yönetmek için kullanılan kimlik bilgilerinizi (Kodlanmamış) içerir. Bu dosya için en iyi güvenlik uygulaması, kaynak dizinlerinizin dışında (örneğin, *Kütüphanaries\belgeler* klasöründe) geçici olarak depolanması ve içeri aktarma tamamlandıktan sonra onu silmektir. Dosyaya erişimi olan kötü niyetli bir Kullanıcı `.publishsettings` , Windows Azure hizmetlerinizi düzenleyebilir, oluşturabilir ve silebilir.

    d. **Windows Azure aboneliklerini Içeri aktar** iletişim kutusunda, **Araştır** ' a tıklayın ve *. publishsettings* dosyasına gidin.

    ![İndir alt](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. **İçeri Aktar**’a tıklayın.

    ![içeri aktar](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. **Yayımlama profilini Içeri aktar** iletişim kutusunda, **bir Windows Azure Web sitesinden içeri aktar**' ı seçin, açılan listeden Web sitenizi seçin ve ardından **Tamam**' a tıklayın.  
  
    ![Yayımlama profilini içeri aktar](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. **Bağlantı** sekmesinde, ayarların doğru olduğundan emin olmak Için **bağlantıyı doğrula** ' ya tıklayın.  
  
    ![Bağlantıyı doğrula](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. Bağlantı doğrulandıktan sonra **bağlantıyı doğrula** düğmesinin yanında yeşil bir onay işareti görüntülenir. **İleri**’ye tıklayın.  
  
    ![Bağlantı başarıyla onaylandı](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. **SchoolContext** altındaki **uzak bağlantı dizesi** açılan listesini açın ve oluşturduğunuz veritabanı için bağlantı dizesini seçin.
8. **Code First Migrations Yürüt ' ü seçin (uygulama başlatma üzerinde çalışır)**.
9. Bu uygulama üyelik veritabanını kullanmıyor olduğundan, bu bağlantı dizesini **UserContext (DefaultConnection)** için **çalışma zamanında kullan** seçeneğinin işaretini kaldırın.   
  
    ![Ayarlar sekmesi](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. **İleri**’ye tıklayın.
11. **Önizleme** sekmesinde **önizlemeyi Başlat**' a tıklayın.  
  
    ![Önizleme sekmesinde StartPreview düğmesi](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    Bu sekmede, sunucuya kopyalanacak dosyaların bir listesi görüntülenir. Önizleme görüntüleme, uygulamayı yayımlamak için gerekli değildir, ancak farkında olmak üzere yararlı bir işlevdir. Bu durumda, görüntülenen dosyaların listesiyle herhangi bir şey yapmanız gerekmez. Bu uygulamayı bir daha dağıttığınızda, yalnızca değiştirilen dosyalar bu listede yer alacak.  
  
    ![StartPreview dosyası çıkışı](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. **Yayımla**’ta tıklayın.  
    Visual Studio, dosyaları Microsoft Azure sunucusuna kopyalama işlemini başlatır.
13. **Çıkış** penceresinde hangi dağıtım eylemlerinin alındığı ve dağıtımın başarılı bir şekilde tamamlandığını raporlayan görüntülenir.  
  
    ![Çıkış penceresi başarılı dağıtımı bildiriyor](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. Dağıtım başarılı olduğunda, varsayılan tarayıcı otomatik olarak dağıtılan Web sitesinin URL 'SI olarak açılır.  
    Oluşturduğunuz uygulama artık bulutta çalışmaktadır. Öğrenciler sekmesine tıklayın.  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

Bu noktada, **Execute Code First Migrations (uygulama başlangıcında çalışır) '** yi seçtiğinizden *SchoolContext* veritabanınız Windows Azure SQL veritabanında oluşturulmuştur. Dağıtılan Web sitesindeki *Web.config* dosyası, kodlarınızın veritabanına veri okuması veya yazması ( **öğrenciler** sekmesini seçtiğinizde meydana gelir) Için, [Migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) başlatıcısı 'nın ilk kez çalışmasını sağlayacak şekilde değiştirilmiştir:

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

Dağıtım işlemi ayrıca, veritabanı şemasını güncelleştirmek ve veritabanını dengeli yapmak için Code First Migrations için yeni bir bağlantı dizesi *(SchoolContext \_ databasepublish*) oluşturmuştur.

![Database_Publish bağlantı dizesi](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection* bağlantı dizesi, üyelik veritabanına (Bu öğreticide kullanmadığınız) yöneliktir. *SchoolContext* bağlantı dizesi contosouniversity veritabanı içindir.

Web.config dosyanın dağıtılan sürümünü *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*kendi bilgisayarınızda bulabilirsiniz. Dağıtılan *Web.config* dosyasına FTP kullanarak erişebilirsiniz. Yönergeler için bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı: kod güncelleştirme dağıtma](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). "FTP aracını kullanmak Için" ile başlayan yönergeleri izleyin: FTP URL 'SI, Kullanıcı adı ve parola. "

> [!NOTE]
> Web uygulaması güvenlik uygulamaz, böylece URL 'YI bulan herkes verileri değiştirebilir. Web sitesinin güvenliğini sağlama hakkında yönergeler için bkz. Membership, [OAuth ve SQL veritabanı Ile güvenli bir ASP.NET MVC uygulamasını Windows Azure Web sitesine dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Siteyi durdurmak için Microsoft Azure Yönetim Portalı veya Visual Studio 'da **Sunucu Gezgini** kullanarak diğer kişilerin siteyi kullanmasını engelleyebilirsiniz.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First başlatıcıları

Dağıtım bölümünde, kullanılmakta olan [Migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) başlatıcısı 'nı gördünüz. Code First Ayrıca, [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (varsayılan), [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) ve [dropcreatedatabaseher zaman](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)dahil olmak üzere kullanabileceğiniz diğer başlatıcıları da sağlar. `DropCreateAlways`Başlatıcı, birim testlerine yönelik koşulları ayarlamak için yararlı olabilir. Ayrıca kendi başlatıcılarınızı yazabilir ve uygulamanın veritabanından okuma veya veritabanına yazma işlemlerini beklemek istemiyorsanız bir başlatıcıyı açıkça çağırabilirsiniz. Başlatıcılar hakkında kapsamlı bir açıklama için, bkz. Bölüm 6, kitap [programlama Entity Framework:](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman ve Rowan Miller tarafından Code First.

## <a name="summary"></a>Özet

Bu öğreticide, bir veri modeli oluşturmayı ve temel CRUD, sıralama, filtreleme, sayfalama ve gruplama işlevlerini nasıl uygulayacağınızı gördünüz. Sonraki öğreticide, veri modelini genişleterek daha gelişmiş konulara bakmaya başlayacaksınız.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md) 
>  [Sonraki](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
