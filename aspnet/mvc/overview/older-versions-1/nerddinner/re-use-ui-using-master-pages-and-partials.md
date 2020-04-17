---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Ana Sayfaları ve Kısmi Leri Kullanarak UI'yi Yeniden Kullanma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 7, kısmi görünüm şablonlarını ve ana sayfaları kullanarak kod yinelemesini ortadan kaldırmak için görünüm şablonlarımız daki 'DRY İlkesi'ni uygulamanın yollarını arar.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542605"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Ana Sayfaları ve Kısmi Bölümleri Kullanarak Kullanıcı Arabirimini Yeniden Kullanma

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 7 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 7, kısmi görünüm şablonlarını ve ana sayfaları kullanarak kod yinelemesini ortadan kaldırmak için görünüm şablonlarımızdaki "KURU İlke"yi uygulamanın yollarını arar.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner Adım 7: Kısmi ve Ana Sayfalar

MVC'ASP.NET benimsediğinin tasarım felsefelerinden biri de "Kendini Tekrarlama" prensibidir (genellikle "DRY" olarak adlandırılır). DRY tasarımı, kodların ve mantığın çoğaltılmasını ortadan kaldırmaya yardımcı olur ve bu da uygulamaları daha hızlı oluşturmayı ve bakımı daha kolay hale getirir.

İnek Yemeği senaryolarımızın bazılarında DRY prensibinin uygulandığını zaten gördük. Birkaç örnek: doğrulama mantığımız model katmanımızda uygulanmaktadır ve bu da hem düzenleme hem de denetleyicimizde senaryolar oluşturma da sağlar; Düzenle, Ayrıntılar ve Silme eylem yöntemleri arasında "Bulundu" görünüm şablonlarını yeniden kullanıyoruz; görünüm şablonlarımızla birlikte, Görünüm() yardımcı yöntemini adlandırdığımızda adı açıkça belirtme ihtiyacını ortadan kaldıran bir kural oluşturma deseni kullanıyoruz; ve hem Düzenleme hem de Eylem Senaryoları Oluşturma için DinnerFormViewModel sınıfını yeniden kullanıyoruz.

Şimdi de orada kod çoğaltma ortadan kaldırmak için bizim görünüm şablonları içinde "KURU İlke" uygulayabilirsiniz yolları bakalım.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Görünüm Şablonlarımızı Yeniden Oluştur ve Görüntü Oluştur'u Yeniden Ziyaret Edin

Şu anda iki farklı görünüm şablonu kullanıyoruz - "Edit.aspx" ve "Create.aspx" – Akşam Yemeği formu UI'mizi görüntülemek için. Bunların hızlı bir görsel karşılaştırma ne kadar benzer olduğunu vurgulamaktadır. Aşağıda oluşturma formu nasıl görünür:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

Ve burada bizim "Edit" formu gibi görünüyor:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Pek bir fark yok, değil mi? Başlık ve üstbilgi metni dışında, form düzeni ve giriş denetimleri aynıdır.

"Edit.aspx" ve "Create.aspx" görünüm şablonlarını açarsak, aynı form düzeni ve giriş kontrol kodu içerdiğini buluruz. Bu yineleme, yeni bir Akşam Yemeği özelliğini tanıttığımızda veya değiştirdiğimizde iki kez değişiklik yapmak zorunda kaldığımız anlamına gelir ki bu iyi bir şey değildir.

### <a name="using-partial-view-templates"></a>Kısmi Görünüm Şablonlarını Kullanma

ASP.NET MVC, sayfanın bir alt bölümü için görünüm oluşturma mantığını kapsüllemek için kullanılabilecek "kısmi görünüm" şablonlarını tanımlama yeteneğini destekler. "Kısmiler" görünüm işleme mantığını bir kez tanımlamak ve uygulama boyunca birden çok yerde yeniden kullanmak için yararlı bir yol sağlar.

Edit.aspx ve Create.aspx view şablon yinelememizi "KURUtun" olarak "KURUtun" yardımcı olmak için, form düzenini ve her ikisi için de ortak olan giriş öğelerini özetleyen "DinnerForm.ascx" adlı kısmi bir görünüm şablonu oluşturabiliriz. Bunu /Views/Dinners dizinine sağ tıklayarak ve "Ekle-&gt;Görüntüle" menü komutunu seçerek yapacağız:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

Bu, "Görünüm Ekle" iletişim kutusunu görüntüler. "DinnerForm" oluşturmak istediğimiz yeni görünümü adlandıracağız, iletişim kutusundaki "Kısmi görünüm oluşturma" onay kutusunu seçeceğiz ve bir DinnerFormViewModel sınıfından geçeceğimizi belirteceğiz:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizininde bizim için yeni bir "DinnerForm.ascx" görünüm şablonu oluşturacaktır.

Daha sonra yinelenen form düzenini / giriş kontrol kodunu Edit.aspx/ Create.aspx görünüm şablonlarımızdan yeni "DinnerForm.ascx" kısmi görünüm şablonumuza kopyalayabilir/yapıştırabiliriz:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Daha sonra DinnerForm kısmi şablonunu aramak ve form yinelemesini ortadan kaldırmak için Görünüm Şablonlarımızı Edit ve Oluştur'da güncelleyebiliriz. Bunu, görünüm şablonlarımız dahilinde Html.RenderPartial("DinnerForm") numaralı telefonu arayarak yapabiliriz:

##### <a name="createaspx"></a>Oluştur.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html.RenderPartial'i ararken istediğiniz kısmi şablonun yolunu açıkça nitelendirebilirsiniz (örneğin: ~Görünümler/Akşam Yemekleri/DinnerForm.ascx).) Yukarıdaki kodumuzda, ancak, biz ASP.NET MVC içinde kongre tabanlı adlandırma desen yararlanarak, ve sadece "DinnerForm" kısmi işlemek için adı olarak belirterek. Bunu yaptığımızda ASP.NET MVC ilk olarak kongre tabanlı görünüm dizini (DinnersController için bu /Views/Dinners olacaktır) görünecektir. Orada kısmi şablon bulamazsa o zaman / Görünümler / Paylaşılan dizini arar.

Html.RenderPartial() yalnızca kısmi görünümün adı ile çağrıldığında, ASP.NET MVC arama görünümü şablonu tarafından kullanılan aynı Model ve ViewData sözlük nesnelerini kısmi görünüme geçirir. Alternatif olarak, html.renderpartial() tarafından kullanılan kısmi görünüm için alternatif bir Model nesnesi ve/veya ViewData sözlüğünü geçirmenizi sağlayan aşırı yüklü sürümleri vardır. Bu, yalnızca tam Model/Görünüm Modeli'nin bir alt kümesini geçirmek istediğiniz senaryolar için yararlıdır.

| **Yan Konu: &lt;Neden&gt; &lt;% yerine&gt;% %= % ?** |
| --- |
| Yukarıdaki kodla fark etmiş olabileceğiniz ince şeylerden biri, Html.RenderPartial() &lt;'yi&gt; ararken %= % bloğu yerine &lt;%&gt; bloğu kullanıyor olmamızdır. &lt;%=&gt; ASP.NET'daki %bloklar, bir geliştiricinin belirli bir &lt;değeri işlemek istediğini&gt; gösterir (örneğin: %= "Merhaba" % "Merhaba" olur). &lt;%&gt; blokları bunun yerine geliştiricinin kod yürütmek istediğini ve bunların içinde işlenen herhangi bir çıktının açıkça yapılması gerektiğini gösterir (örneğin: &lt;% Response.Write("Hello") %&gt;. Yukarıdaki Html.RenderPartial &lt;kodumuzda % blok&gt; kullanmamızın nedeni, Html.RenderPartial() yönteminin bir dize döndürmemesi ve bunun yerine içeriği doğrudan arama görünümü şablonundaki çıkış akışına çıkarmasıdır. Bunu performans verimliliği nedenleriyle yapar ve bunu yaparak (potansiyel olarak çok büyük) geçici bir dize nesnesi oluşturma gereksinimini önler. Bu, bellek kullanımını azaltır ve genel uygulama verime kullanımını artırır. Html.RenderPartial() kullanırken sık karşılaşılan hatalardan &lt;biri, % blok&gt; içinde yken aramanın sonunda bir yarı nokta nokta eklemeyi unutmaktır. Örneğin, bu kod derleyici hatasına &lt;neden olur: % Html.RenderPartial("DinnerForm") %&gt; Bunun yerine yazmanız gerekir: &lt;% Html.RenderPartial("DinnerForm"); %&gt; Bunun &lt;nedeni&gt; % blokların bağımsız kod ekstreleri olması ve C# kod deyimleri kullanırken bir yarı-iki nokta ile sonlandırılması gerekir. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Kodu Netleştirmek için Kısmi Görünüm Şablonlarını Kullanma

Görünümü çoğaltma mantığını birden çok yerde çoğaltmamak için "DinnerForm" kısmi görünüm şablonu oluşturduk. Bu, kısmi görünüm şablonları oluşturmak için en yaygın nedendir.

Bazen, yalnızca tek bir yerde çağrılsalar bile kısmi görünümler oluşturmak yine de mantıklı dır. Çok karmaşık görünüm şablonları genellikle görünüm oluşturma mantığı ayıklandığında ve bir veya daha fazla iyi adlandırılmış kısmi şablonlara bölümlendiğinde okunması çok daha kolay hale gelebilir.

Örneğin, projemizdeki Site.master dosyasından aşağıdaki kod-parçacığı nı göz önünde bulundurun (kısa süre içinde inceleeceğiz). Kod okumak için nispeten düz-ileri - kısmen ekranın sağ üst kısmında bir giriş / logout bağlantı görüntülemek için mantık "LogOnUserControl" kısmi içinde kapsüllenmiş çünkü:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Bir görünüm şablonu içindeki html/kod biçimlendirmesini anlamaya çalışırken kafanızın karıştığını bulduğunuzda, bir kısmının ayıklanıp iyi adlandırılmış kısmi görünümlere yeniden dizilip yeniden dizilseydi daha net olup olmayacağını düşünün.

### <a name="master-pages"></a>Ana Sayfalar

ASP.NET MVC, kısmi görünümleri desteklemenin yanı sıra, bir sitenin ortak düzenini ve üst düzey html'ini tanımlamak için kullanılabilecek "ana sayfa" şablonları oluşturma yeteneğini de destekler. İçerik yer tutucu denetimleri daha sonra, geçersiz kılınabilen veya görünümler tarafından "doldurulabilen" değiştirilebilir bölgeleri belirlemek için ana sayfaya eklenebilir. Bu, bir uygulama arasında ortak bir düzen uygulamak için çok etkili (ve DRY) bir yol sağlar.

Varsayılan olarak, yeni ASP.NET MVC projeleri otomatik olarak eklenen bir ana sayfa şablonu var. Bu ana sayfa "Site.master" olarak adlandırılır ve \Views\Shared\ klasöründe yaşar:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

Varsayılan Site.master dosyası aşağıdaki gibi görünür. Bu üst te gezinme için bir menü ile birlikte, sitenin dış html tanımlar. Biri başlık için, diğeri ise bir sayfanın birincil içeriğinin değiştirilmesi gereken iki değiştirilebilir içerik yer tutucu denetimi içerir:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

NerdDinner uygulamamız için oluşturduğumuz tüm görünüm şablonları ("Liste", "Ayrıntılar", "Edit", "Create", "NotFound", vb.) bu Site.master şablonuna dayanmaktadır. Bu, "Görünüm Ekle" iletişim kutusunu kullanarak görünümlerimizi oluşturduğumuzda &lt;varsayılan olarak&gt; en üst % @ Sayfa % yönergesine eklenen "MasterPageFile" özniteliği ile gösterilir:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

Bunun anlamı, Site.master içeriğini değiştirebileceğimiz ve görünüm şablonlarımızdan herhangi birini işlediğimizde değişikliklerin otomatik olarak uygulanıp kullanılmasını sağlayabiliriz.

Sitemizi güncelleyelim.master üstbilgi bölümü, uygulamamızın üstbilgisinin "MVC Uygulamam" yerine "NerdDinner" olması için güncelleyelim. Navigasyon menümüzü de ilk sekme "Bir Akşam Yemeği Bul" (HomeController's Index() eylem yöntemi yle ele alınabilecek şekilde güncelleyelim ve "Host a Dinner" (DinnersController's Create() eylem yöntemi yle işlenen" adlı yeni bir sekme ekleyelim:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master dosyasını kaydedip tarayıcımızı yenilediğimizde üstbilgi değişikliklerimizin uygulamamızdaki tüm görünümler arasında ortaya çıktığınızı görürsünüz. Örneğin:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

Ve */Dinners/Edit/[id]* URL'si ile:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Sonraki Adım

Kısmi sayfalar ve ana sayfalar, görünümleri temiz bir şekilde düzenlemenizi sağlayan çok esnek seçenekler sunar. Görünüm içeriğini/ kodunu çoğaltmanızı önlemenize ve görünüm şablonlarınızın okunmasını ve bakımını kolaylaştırmanıza yardımcı olduklarını göreceksiniz.

Şimdi daha önce oluşturduğumuz listeleme senaryosunu yeniden gözden geçirelim ve ölçeklenebilir sayfalama desteğietkinleştirelim.

> [!div class="step-by-step"]
> [Önceki](use-viewdata-and-implement-viewmodel-classes.md)
> [Sonraki](implement-efficient-data-paging.md)
