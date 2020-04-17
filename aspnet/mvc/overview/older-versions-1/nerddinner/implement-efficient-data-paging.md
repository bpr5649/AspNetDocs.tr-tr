---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Verimli Veri Sayfalama Uygulayın | Microsoft Dokümanlar
author: rick-anderson
description: 8. adım, /Dinners URL'mize nasıl çağrıdesteği ekleyebileceğimizi gösterir, böylece 1000'lerce akşam yemeğini aynı anda görüntülemek yerine, sadece 10 akşam yemeğini...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541331"
---
# <a name="implement-efficient-data-paging"></a>Verimli Veri Sayfalama Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 8 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 8, /Dinners URL'mize nasıl çağrıdesteği ekleyeceğinigösterir, böylece aynı anda 1000'lerce akşam yemeği görüntülemek yerine, aynı anda sadece 10 yaklaşan akşam yemeğini görüntüleriz ve son kullanıcıların tüm listeyi SEO dostu bir şekilde ileri geri yönlendirmelerine olanak sağlarız.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner Adım 8: Paging Destek

Sitemiz başarılı olursa, yaklaşan akşam yemekleri binlerce olacak. Kullanıcı bira bilgisayarlarımızın tüm bu akşam yemeklerini işlemek için ölçeklendirildiklerinden ve kullanıcıların bunlara göz atmasını sağladığından emin olmalıyız. Bunu etkinleştirmek için, */Dinners* URL'mize sayfalama desteği ekleyeceğiz, böylece aynı anda 1000'lerce akşam yemeği görüntülemek yerine, aynı anda sadece 10 yaklaşan akşam yemeğini göstereceğiz ve son kullanıcıların tüm listeyi SEO dostu bir şekilde ileri geri yönlendirmelerine izin vereceğiz.

### <a name="index-action-method-recap"></a>Dizin() Eylem Yöntemi Özeti

DinnersController sınıfımızdaki Index() eylem yöntemi şu anda aşağıdaki gibi görünmaktadır:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

*/Dinners* URL'sine bir istek yapıldığında, yaklaşan tüm akşam yemeklerinin listesini alır ve sonra bunların bir listesini çıkarır:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>IQueryable&lt;T Anlama&gt;

*IQueryable&lt;&gt; T,* .NET 3.5'in bir parçası olarak LINQ ile tanıtılan bir arayüzdür. Bu, çağrılma desteğini uygulamak için yararlanabileceğimiz güçlü "ertelenmiş yürütme" senaryolarına olanak tanır.

DinnerRepository sitemizde FindUpcomingDinners()&lt;&gt; metodumuzdan Bir IQueryable Dinner dizisi geri dönüyoruz:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinner() yöntemimiz tarafından döndürülen IQueryable&lt;Dinner&gt; nesnesi, LINQ'dan SQL'e kullanarak veritabanımızdan Dinner nesnelerini almak için bir sorguyu kapsüller. Daha da önemlisi, sorgudaki verilere erişmeye/tekrarlamaya çalışana veya üzerinde ToList() yöntemini arayana kadar sorguyu veritabanına karşı yürütmez. FindUpcomingDinners() metodumuzu çağıran kod, sorguyu yürütmeden önce Isteğe bağlı olarak&lt;&gt; IQueryable Dinner nesnesine ek "zincirlenmiş" işlemler/filtreler eklemeyi seçebilir. LinQ'dan SQL'e, veriler istendiğinde veritabanına karşı birleştirilmiş sorguyu yürütecek kadar akıllıdır.

Sayfalama mantığını uygulamak için DinnersController'S Index() eylem yöntemimizi güncelleyebiliriz, böylece tolist() çağırmadan&lt;&gt; önce döndürülen IQueryable Dinner dizisine ek "Atla" ve "Al" operatörleri uygular:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

Yukarıdaki kod veritabanında ilk 10 yaklaşan akşam yemekleri atlar ve sonra 20 akşam yemeği geri döndürür. LINQ'dan SQL'e, web sunucusunda değil, SQL veritabanında bu atlama mantığını gerçekleştiren en iyi duruma getirilmiş bir SQL sorgusu oluşturacak kadar akıllıdır. Bu, veritabanında milyonlarca yaklaşan Akşam Yemeği olsa bile, bu isteğin bir parçası olarak yalnızca istediğimiz 10 yemeğin alınacağı anlamına gelir (verimli ve ölçeklenebilir hale getirir).

### <a name="adding-a-page-value-to-the-url"></a>URL'ye "sayfa" değeri ekleme

Belirli bir sayfa aralığını sabit kodlamak yerine, URL'lerimizin bir kullanıcının hangi Akşam Yemeği aralığını istediğini gösteren bir "sayfa" parametresi eklemesini isteriz.

#### <a name="using-a-querystring-value"></a>Querystring değerini kullanma

Aşağıdaki kod, bir querystring parametresini desteklemek ve */Dinners?page=2*gibi URL'leri etkinleştirmek için Index() eylem yöntemimizi nasıl güncelleştirebileceğimizi göstermektedir:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

Yukarıdaki Dizin eylem yönteminde "sayfa" adlı bir parametre vardır. Parametre nullable tamsayı olarak bildirilir (yani int? gösterir). Bu, */Dinners?page=2* URL'nin parametre değeri olarak "2" değerinin geçirilmesine neden olacağı anlamına gelir. */Dinners* URL (sorgu dize değeri olmadan) null bir değer geçirilmesine neden olur.

Kaç akşam yemeği atlayabileceğimizi belirlemek için sayfa değerini sayfa boyutuna (bu durumda 10 satır) çarpıyoruz. Biz nullable türleri ile uğraşırken yararlı [c# null "coalescing" işleci (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) kullanıyoruz. Yukarıdaki kod, sayfa parametresi null ise sayfaya 0 değerini atar.

#### <a name="using-embedded-url-values"></a>Gömülü URL değerlerini kullanma

Sorgu dize değeri kullanmanın alternatifi, sayfa parametresini gerçek URL'nin içine katıştırmaktır. Örneğin: */Akşam Yemekleri/Sayfa/2* veya */Akşam Yemekleri/2*. ASP.NET MVC, bu gibi senaryoları desteklemeyi kolaylaştıran güçlü bir URL yönlendirme motoru içerir.

Gelen URL veya URL biçimlerini istediğimiz herhangi bir denetleyici sınıfına veya eylem yöntemine eşleyen özel yönlendirme kuralları kaydedebiliriz. Tek yapmamız gereken projemiz dahilinde Global.asax dosyasını açmak:

![](implement-efficient-data-paging/_static/image2.png)

Ardından, routelara yapılan ilk arama gibi MapRoute() yardımcı yöntemini kullanarak yeni bir eşleme kuralı kaydedin. MapRoute() aşağıda:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Yukarıda "Yaklaşan Akşam Yemekleri" adlı yeni bir yönlendirme kuralı kaydediyoruz. {sayfa} URL'nin içine katıştırılmış bir parametre değeri olan "Akşam Yemekleri/Sayfa/{sayfa}" URL biçimine sahip olduğunu gösteriyoruz. MapRoute() yönteminin üçüncü parametresi, bu biçimi DinnersController sınıfındaki Index() eylem yöntemiyle eşleşen URL'leri eşleştirmemiz gerektiğini belirtir.

Querystring senaryomuzda daha önce sahip olduğumuz index() kodunu kullanabiliriz – ancak artık "sayfa" parametremiz querystring'ten değil URL'den gelecektir:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

Ve şimdi biz uygulama çalıştırmak ve */ Akşam Yemeği* yazın biz ilk 10 yaklaşan akşam yemekleri görürsünüz:

![](implement-efficient-data-paging/_static/image3.png)

*/Dinners/Page/1* yazdığımızda akşam yemeklerinin bir sonraki sayfasını göreceğiz:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Sayfa gezintisi UI ekleme

Sayfalama senaryomuzu tamamlamak için son adım, kullanıcıların Akşam Yemeği verilerini kolayca atlayabilmeleri için görünüm şablonumuz içinde "sonraki" ve "önceki" gezinti Kullanıcı Arabirimi'ni uygulamak olacaktır.

Bunu doğru bir şekilde uygulamak için, veritabanındaki toplam Akşam Yemeği sayısını ve bunun kaç sayfaya çevrildiği ni bilmemiz gerekir. Daha sonra, şu anda istenen "sayfa" değerinin verilerin başında mı yoksa sonunda mı olduğunu hesaplamamız ve "önceki" ve "sonraki" UI'yi buna göre göstermemiz veya gizlememiz gerekir. Bu mantığı Index() eylem yöntemimiz içinde uygulayabiliriz. Alternatif olarak, projemize bu mantığı daha yeniden kullanılabilir bir şekilde saklayan bir yardımcı sınıf ekleyebiliriz.

Aşağıda,.NET Framework'de yerleşik T&lt;&gt; koleksiyonu listesinden türeyen basit bir "PaginatedList" yardımcı sınıfı yer almaktadır. Herhangi bir IQueryable veri dizisini paginate için kullanılabilecek yeniden kullanılabilir bir toplama sınıfı uygular. Bizim&lt;NerdDinner uygulamada biz IQueryable Akşam Yemeği&gt; sonuçları üzerinde çalışmak gerekir, ama sadece&lt;kolayca&gt; diğer uygulama senaryolarında IQueryable Ürün veya IQueryable&lt;Müşteri&gt; sonuçlarına karşı kullanılabilir:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

"PageIndex", "PageSize", "TotalCount" ve "TotalPages" gibi özellikleri nasıl hesaplayıp sonra ortaya çıkardığına dikkat edin. Ayrıca, koleksiyondaki veri sayfasının özgün dizinin başında mı yoksa sonunda mı olduğunu gösteren iki yardımcı özelliği "HasPreviousPage" ve "HasNextPage" olarak da gösterir. Yukarıdaki kod iki SQL sorgusunun çalıştırılmasına neden olur - ilkolarak toplam Akşam Yemeği nesnesi sayısının sayısını almak için (bu nesneleri döndürmez – daha çok bir tamsayı döndüren bir "SELECT COUNT" deyimi gerçekleştirir) ve ikincisi de geçerli veri sayfası için veritabanımızdan yalnızca ihtiyacımız olan veri satırlarını almak için kullanılır.

Daha sonra DinnersController.Index() yardımcı yöntemimizi güncelleştirerek DinnerRepository.FindUpcomingDinners() sonuçlarımızdan pajinedList&lt;akşam yemeği&gt; oluşturabilir ve görünüm şablonumuza aktarabiliriz:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Daha sonra ViewPage IndDinner.Helpers.PaginatedList&lt;&lt;&gt; &gt; &lt;&lt;Dinner yerine ViewPage IndDinner.PaginatedList Dinner'dan&gt;&gt;devralmak üzere \Views\Dinners\Index.aspx görünüm şablonunu güncelleyebilir ve ardından sonraki ve önceki gezinti UI'sını göstermek veya gizlemek için görünüm şablonumuzun altına aşağıdaki kodu ekleyebiliriz:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Köprülerimizi oluşturmak için Html.RouteLink() yardımcı yöntemini nasıl kullandığımıza dikkat edin. Bu yöntem, daha önce kullandığımız Html.ActionLink() yardımcı yöntemine benzer. Aradaki fark, Global.asax dosyamızda kurduğumuz "Yaklaşan Dinners" yönlendirme kuralını kullanarak URL'yi oluşturuyor olmamızdır. Bu, {sayfa} değerinin geçerli PageIndex'e göre yukarıda sağladığımız bir değişken olduğu */Dinners/Page/{page}* biçimine sahip Dizin eylem yöntemimize URL'ler oluşturmamızı sağlar.

Ve şimdi uygulamamızı tekrar çalıştırdığımızda tarayıcımızda aynı anda 10 akşam yemeği göreceğiz:

![](implement-efficient-data-paging/_static/image5.png)

Ayrıca, &lt; &lt; &lt; arama &gt; &gt; motoru erişilebilir URL'leri kullanarak verilerimiz üzerinden ileri ve geri atlamamızı sağlayan sayfanın alt kısmında kullanıcı arabirimi var ve &gt; navigasyon ui:

![](implement-efficient-data-paging/_static/image6.png)

| **Yan Konu: IQueryable&lt;T etkileri anlama&gt;** |
| --- |
| IQueryable&lt;&gt; T ilginç ertelenmiş yürütme senaryoları çeşitli sağlayan çok güçlü bir özelliktir (sayfalama ve kompozisyon tabanlı sorgular gibi). Tüm güçlü özellikleri olduğu gibi, nasıl kullandığınıza dikkat etmek ve kötüye olmadığından emin olmak istiyorum. Deponuzdan bir IQueryable&lt;T&gt; sonucunu döndürmenin, arama kodunun zincirlenmiş işleç yöntemlerine eklemesini ve böylece nihai sorgu yürütmesine katılmasını sağladığını kabul etmek önemlidir. Arama kodu bu yeteneği sağlamak istemiyorsanız, o zaman&lt;iList&gt; T veya ImEnumerable&lt;T&gt; sonuçları geri dönmelisiniz - zaten yürütülmüş bir sorgu sonuçlarını içeren. Pagination senaryoları için bu, gerçek veri pagination mantığını çağrılan depo yöntemine itmenizi gerektirir. Bu senaryoda findUpcomingDinners() bulucu yöntemimizi, paginatedList'i döndüren bir imzaya&lt; &gt; sahip olmak için güncelleyebiliriz: PaginatedList Dinner FindUpcomingDinners(int pageIndex, int pageSize) { } Veya bir&lt;IList Akşam Yemeği'ni&gt;geri döndürebilir ve bir "totalCount" out param kullanarak Akşam Yemeği toplam sayısını iade edebilir: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageIndex, int pageSize, outt), } |

### <a name="next-step"></a>Sonraki Adım

Şimdi uygulamamıza kimlik doğrulama ve yetkilendirme desteğini nasıl ekleyebileceğimize bakalım.

> [!div class="step-by-step"]
> [Önceki](re-use-ui-using-master-pages-and-partials.md)
> [Sonraki](secure-applications-using-authentication-and-authorization.md)
