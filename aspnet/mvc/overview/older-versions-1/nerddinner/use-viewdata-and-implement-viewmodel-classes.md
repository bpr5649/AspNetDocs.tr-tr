---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData'yı kullanın ve ViewModel Sınıflarını Uygulayın | Microsoft Dokümanlar
author: rick-anderson
description: Adım 6, daha zengin biçim düzenleme senaryoları için desteği nasıl etkinleştirdiğini gösterir ve denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşımı da tartışır:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541110"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData Kullanma ve ViewModel Sınıfları Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 6 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 6, daha zengin biçim düzenleme senaryoları için desteği nasıl etkinleştirdiğini gösterir ve denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşımı da tartışır: ViewData ve ViewModel.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner Adım 6: ViewData ve ViewModel

Bir dizi form sonrası senaryoyu ele aldık ve oluşturma, güncelleştirme ve silme (CRUD) desteğinin nasıl uygulanacağını tartıştık. Şimdi DinnersController uygulamamızı daha da ileriye götüreceğiz ve daha zengin form düzenleme senaryoları için destek sağlayacağız. Bunu yaparken denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşımı tartışacağız: ViewData ve ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Denetleyicilerden Görünüm Şablonlarına Veri Aktarma

MVC deseninin tanımlayıcı özelliklerinden biri, bir uygulamanın farklı bileşenleri arasında uygulanmasına yardımcı olan katı "endişelerin ayrılması"dır. Modeller, Denetleyiciler ve Görünümler her biri iyi tanımlanmış rolleri ve sorumlulukları var ve onlar iyi tanımlanmış şekillerde birbirleri arasında iletişim. Bu, test edilebilirliği ve kodun yeniden kullanımını desteklemeye yardımcı olur.

Denetleyici sınıfı bir HTML yanıtını istemciye geri vermeye karar verdiğinde, yanıtı işlemek için gereken tüm verilerin görünüm şablonuna açıkça geçirilmesinden sorumludur. Görünüm şablonları hiçbir zaman veri alma veya uygulama mantığı gerçekleştirmemelidir ve bunun yerine kendilerini yalnızca denetleyici tarafından ona aktarılan model/verilerden uzaklaştırılabilen işleme koduyla sınırlandırmalıdır.

Şu anda DinnersController sınıfımız tarafından görünüm şablonlarımıza geçirilen model verileri basit ve doğrudan – Index() durumunda Akşam Yemeği nesnelerinin bir listesi ve Ayrıntılar(), Düzenle(), Oluştur() ve Sil() durumunda tek bir Akşam Yemeği nesnesi. Uygulamamıza daha fazla Kullanıcı Arabirimi özelliği ekledikçe, görünüm şablonlarımız içinde HTML yanıtlarını işlemek için genellikle bu verilerden daha fazlasını aktarmamız gerekecektir. Örneğin, Edit'imiziçindeki "Ülke" alanını değiştirmek ve HTML textbox'ından açılır listeye görünüm ler oluşturmak isteyebiliriz. Görünüm şablonundaki ülke adlarının açılır listesini sabit kodlamak yerine, dinamik olarak dolduran desteklenen ülkeler listesinden oluşturmak isteyebiliriz. Hem Akşam Yemeği nesnesini *hem* de desteklenen ülkelerin listesini denetleyicimizden görünüm şablonlarımıza geçirmenin bir yolunu bulmalıyız.

Bunu başarmanın iki yolunu inceleyelim.

### <a name="using-the-viewdata-dictionary"></a>ViewData Sözlüğü'nün kullanılması

Denetleyici taban sınıfı, Denetleyicilerden Görünümlere ek veri öğeleri aktarmak için kullanılabilecek bir "ViewData" sözlük özelliğini ortaya çıkarır.

Örneğin, Edit görünümümüzdeki "Ülke" textbox'ını HTML textbox'ı açılır listeye değiştirmek istediğimiz senaryoyu desteklemek için, bir ülke açılır listesinin modeli olarak kullanılabilecek bir SelectList nesnesini geçmek için Edit() eylem yöntemimizi güncelleştirebiliriz.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

Yukarıdaki SelectList'in oluşturucusu, açılır listeyi ve şu anda seçili değeri doldurmak için bir ilçe listesini kabul etmektedir.

Daha sonra daha önce kullandığımız Html.TextBox() yardımcı yöntemi yerine Html.DropDownList() yardımcı yöntemini kullanmak için Edit.aspx görünüm şablonumuzu güncelleyebiliriz:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

Yukarıdaki Html.DropDownList() yardımcı yöntemi iki parametre alır. İlk çıktı için HTML form öğesinin adıdır. İkincisi, ViewData sözlüğünden geçen "SelectList" modelidir. Sözlükteki türü SelectList olarak kullanmak için C# "as" anahtar sözcüklerini kullanıyoruz.

Ve şimdi uygulamamızı çalıştırdığımızda ve tarayıcımızdaki */Dinners/Edit/1* URL'sine eriştiğımızda, çevrimiçi Kullanıcı Arabirimi'mizin textbox yerine ülkelerin açılır listesini görüntülemek üzere güncellendiğini göreceğiz:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

HTTP-POST Edit yönteminden (hatalar oluştuğusenaryolarda) Edit görünüm şablonu da işlettiğimiziçin, görünüm şablonu hata senaryolarında işlendiğinde SelectList'i ViewData'ya eklemek için bu yöntemi de güncellediğimizden emin olmak isteriz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

Ve şimdi bizim DinnersController edit senaryo bir DropDownList destekler.

### <a name="using-a-viewmodel-pattern"></a>Görünüm Model Deseni Kullanma

ViewData sözlük yaklaşımı oldukça hızlı ve uygulaması kolay olmanın avantajına sahiptir. Ancak bazı geliştiriciler dize tabanlı sözlükler kullanmayı sevmezler, çünkü yazım hataları derleme zamanında yakalanmayacak hatalara yol açabilir. Yazılmamış ViewData sözlüğü, görünüm şablonunda C# gibi güçlü bir şekilde yazılan bir dili kullanırken "as" işleci veya döküm kullanmayı da gerektirir.

Kullanabileceğimiz alternatif bir yaklaşım genellikle "ViewModel" deseni olarak adlandırılır. Bu deseni kullanırken, belirli görünüm senaryolarımız için en iyi duruma getirilmiş ve görünüm şablonlarımızın gerektirdiği dinamik değerler/içerik özelliklerini ortaya çıkaran güçlü bir şekilde yazılan sınıflar oluştururuz. Denetleyici sınıflarımız daha sonra bu görünüm için optimize edilmiş sınıfları kullanmak üzere görünüm şablonumuza aktarabilir. Bu, görünüm şablonları içinde tür güvenliği, derleme-zaman denetimi ve düzenleyici intellisense sağlar.

Örneğin, akşam yemeği formu düzenleme senaryolarını etkinleştirmek için aşağıda olduğu gibi güçlü bir şekilde yazılan iki özelliği ortaya çıkaran bir "DinnerFormViewModel" sınıfı oluşturabiliriz: Bir Akşam Yemeği nesnesi ve ülkelerin açılır listesini doldurmak için gereken SelectList modeli:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Daha sonra, depomuzdan aldığımız Akşam Yemeği nesnesini kullanarak DinnerFormViewModel'i oluşturmak için Edit() eylem yöntemimizi güncelleyebilir ve ardından görünüm şablonumuza aktarabiliriz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Daha sonra görünüm şablonumuzu, edit.aspx sayfasının üst kısmındaki "devralır" özniteliğini değiştirerek "Akşam Yemeği" nesnesi yerine "DinnerFormViewModel" bekleyerek güncelleriz:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Bunu yaptıktan sonra, görünüm şablonumuzdaki "Model" özelliğinin intellisense'i, geçtiğimiz DinnerFormViewModel türünün nesne modelini yansıtacak şekilde güncellenecektir:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Daha sonra, çalışma için görünüm kodumuzu güncelleyebiliriz. Oluşturduğumuz giriş öğelerinin adlarını değiştirmediğimizi aşağıdan aşağıya dikkat edin (form öğeleri yine de "Başlık", "Ülke" olarak adlandırılacaktır) – ancak DinnerFormViewModel sınıfını kullanarak değerleri almak için HTML Yardımcı yöntemlerini güncelliyoruz:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Ayrıca, hata oluştururken DinnerFormViewModel sınıfını kullanmak için Düzenleme sonrası yöntemimizi de güncelleriz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Ayrıca, aynı *DinnerFormViewModel* sınıfını yeniden kullanmak için Create() eylem yöntemlerimizi güncelleştirip, bu ülkelerdeki DropDownList'i de etkinleştirebiliriz. Aşağıda HTTP-GET uygulaması:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

Aşağıda HTTP-POST Oluşturma yönteminin uygulanması:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

Ve şimdi hem Edit hem de Oluştur ekranlarımız ülkeyi seçmek için açılır listeleri destekliyor.

### <a name="custom-shaped-viewmodel-classes"></a>Özel şekilli ViewModel sınıfları

Yukarıdaki senaryoda, DinnerFormViewModel sınıfımız, destekleyici selectlist modeli özelliğiyle birlikte Akşam Yemeği modeli nesnesini doğrudan bir özellik olarak ortaya çıkarır. Bu yaklaşım, görünüm şablonumuz içinde oluşturmak istediğimiz HTML UI'sinin etki alanı modeli nesnelerimize nispeten yakın olduğu senaryolar için iyi çalışır.

Bunun böyle olmadığı senaryolarda, kullanabileceğiniz seçeneklerden biri, nesne modeli görünüme göre tüketim için daha iyi duruma getirilmiş ve temel etki alanı modeli nesnesinden tamamen farklı görünebilecek özel şekilli bir ViewModel sınıfı oluşturmaktır. Örneğin, birden çok model nesnesinden toplanan farklı özellik adlarını ve/veya toplu özelliklerini ortaya çıkarabilir.

Özel şekilli ViewModel sınıfları hem denetleyicilerden görüntülenecek görünümlere veri aktarmak hem de denetleyicinin eylem yöntemine geri gönderilen form verilerini işlemek için kullanılabilir. Bu daha sonraki senaryo için, eylem yöntemi form deftere nakledilen verilerle bir ViewModel nesnesini güncelleştirmek ve sonra gerçek bir etki alanı modeli nesnesi eşlemek veya almak için ViewModel örneğini kullanabilirsiniz.

Özel şekilli ViewModel sınıfları büyük bir esneklik sağlayabilir ve görünüm şablonlarınızda görüntüleme kodunu bulduğunuzda veya eylem yöntemleriniz içinde form gönderme kodunu çok karmaşık hale gelmeye başladığınızda araştırabileceğiniz bir şeydir. Bu genellikle etki alanı modellerinizin oluşturmakta olduğunuz Kullanıcı Ara Birimi'ne temiz bir şekilde karşılık olmadığının ve ara özel şekilli ViewModel sınıfının yardımcı olabileceğinin bir işaretidir.

### <a name="next-step"></a>Sonraki Adım

Şimdi uygulamamız genelinde kullanıcı arasını yeniden kullanmak ve paylaşmak için kısmi sayfaları ve ana sayfaları nasıl kullanabileceğimize bakalım.

> [!div class="step-by-step"]
> [Önceki](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [Sonraki](re-use-ui-using-master-pages-and-partials.md)
