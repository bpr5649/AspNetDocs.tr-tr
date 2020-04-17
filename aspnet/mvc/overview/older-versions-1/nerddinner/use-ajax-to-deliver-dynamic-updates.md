---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Dinamik Güncellemeler Sunmak için AJAX'ı kullanın | Microsoft Dokümanlar
author: rick-anderson
description: Adım 10, akşam yemeği detaylarına entegre edilmiş Ajax tabanlı bir yaklaşım kullanarak, bir akşam yemeğine katılmak la ilgilendikleri RSVP'ye giriş yaptırıcı kullanıcılar için destek uygular...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541253"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX Kullanarak Dinamik Güncelleştirmeler Sunma

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 10 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 10, akşam yemeği ayrıntıları sayfasına entegre edilmiş Ajax tabanlı bir yaklaşım kullanarak, bir akşam yemeğine katılmakla ilgilendikleri RSVP'ye giriş yaptırıcı kullanıcılar için destek uygular.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner Adım 10: AJAX Etkinleştirme RSVPs Kabul

Şimdi, bir akşam yemeğine katılmakla ilgilendikleri RSVP'ye giriş yapmış kullanıcılar için destek uygulayalım. Bunu, akşam yemeği detayları sayfasına entegre edilmiş AJAX tabanlı bir yaklaşım la etkinleştireceğiz.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Kullanıcının RSVP'd olup olmadığını gösteren

Kullanıcılar belirli bir akşam yemeği yle ilgili ayrıntıları görmek için */Dinners/Details/[id*] URL'sini ziyaret edebilirler:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Ayrıntılar() eylem yöntemi aşağıdaki gibi uygulanır:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP desteğini uygulamak için ilk adımımız, Akşam Yemeği nesnemize (daha önce oluşturduğumuz Dinner.cs kısmi sınıf içinde) bir "IsUserRegistered(kullanıcı adı)" yardımcı yöntemi eklemek olacaktır. Bu yardımcı yöntem, kullanıcının akşam yemeği için şu anda RSVP'd olup olmadığına bağlı olarak doğru veya yanlış döndürür:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Daha sonra, kullanıcının olay için kayıtlı olup olmadığını belirten uygun bir ileti görüntülemek için Ayrıntılar.aspx görünüm şablonumuza aşağıdaki kodu ekleyebiliriz:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

Ve şimdi bir kullanıcı kayıtlı olduğu bir Akşam Yemeği ziyaret ettiğinde bu mesajı görürsünüz:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

Ve bir Akşam Yemeği'ni ziyaret ettiklerinde kayıtlı olmadıkları nda aşağıdaki mesajı görürler:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Kayıt Eylem Yönteminin Uygulanması

Şimdi, kullanıcıların ayrıntılar sayfasından bir akşam yemeği için RSVP'ye kabul etmelerini sağlamak için gerekli işlevselliği ekleyelim.

Bunu uygulamak için, \Controllers dizinine sağ tıklayarak ve Ekle-Denetleyici&gt;menü komutunu seçerek yeni bir "RSVPController" sınıfı oluştururuz.

Yeni RSVPController sınıfında bir "Kaydol" eylem yöntemi uygulayacağız, bir akşam yemeği için bir id alır, uygun Akşam Yemeği nesnesini alır, oturum açmış kullanıcının şu anda kayıt yaptıran kullanıcılar listesinde olup olmadığını kontrol eder ve onlar için bir RSVP nesnesi ekleyip eklenmediğini kontrol edeceğiz:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Eylem yönteminin çıktısı olarak basit bir dizeyi nasıl döndürdettiğimize yukarıda dikkat edin. Bu iletiyi bir görünüm şablonuna gömebilirdik – ancak çok küçük olduğu için denetleyici taban sınıfında İçerik() yardımcı yöntemini kullanacağız ve yukarıdaki gibi bir dize iletisi döndüreceğiz.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX kullanarak RSVPForEvent Eylem Yöntemi arama

Ayrıntılar görünümümüzden Kayıt eylem yöntemini çağırmak için AJAX'ı kullanacağız. Bunu uygulamak oldukça kolaydır. Önce iki komut dosyası kitaplığı referansı ekleyeceğiz:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

İlk kitaplık, AJAX istemci tarafı komut dosyası kitaplığı ASP.NET temel başvurur. Bu dosya yaklaşık 24k boyutu (sıkıştırılmış) ve çekirdek istemci tarafı AJAX işlevselliği içerir. İkinci kitaplık, mvc'nin dahili AJAX yardımcı yöntemleriyle ASP.NET entegre olan yardımcı program işlevlerini içerir (kısa süre içinde kullanacağız).

Daha sonra daha önce eklediğimiz görünüm şablonu kodunu güncelleştirebiliriz, böylece "Bu olay için kayıtlı değilsiniz" iletisi vermek yerine, itildiğinde RSVP denetleyicimiz ve RSVP kullanıcımız rsvpForEvent eylem yöntemimizi çağıran bir AJAX çağrısı gerçekleştiren bir bağlantı oluşturuyoruz:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

Yukarıda kullanılan Ajax.ActionLink() yardımcı yöntemi yerleşik ASP.NET MVC ve html.ActionLink() yardımcı yöntemine benzer, ancak standart bir navigasyon gerçekleştirmek yerine bağlantı tıklandığında eylem yöntemine AJAX çağrısı yapar. Yukarıda "RSVP" denetleyicisi üzerinde "Kayıt" eylem yöntemi çağırıyoruz ve ona "id" parametresi olarak DinnerID geçen. Geçirdiğimiz son AjaxOptions parametresi, eylem yönteminden döndürülen içeriği almak ve &lt;&gt; kimliği "rsvpmsg" olan sayfadaki HTML div öğesini güncelleştirmek istediğimizi gösterir.

Ve şimdi bir kullanıcı henüz kayıtlı olmayan bir akşam yemeği ne zaman bunun için RSVP için bir bağlantı görürsünüz:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

"Bu olay için RSVP" bağlantısını tıkladıklarında, RSVP denetleyicisindeki Register eylem yöntemine BIR AJAX çağrısı yaparlar ve tamamlandığında aşağıdaki gibi güncelleştirilmiş bir ileti görürler:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

Bu AJAX arama yaparken ilgili ağ bant genişliği ve trafik gerçekten hafiftir. Kullanıcı "Bu olay için RSVP" bağlantısını tıkladığında, telüzerinde aşağıdaki gibi görünen */Dinners/Register/1* URL'sine küçük bir HTTP POST ağ isteği yapılır:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

Ve kayıt eylem yöntemimizden gelen yanıt basitçe:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Bu hafif arama hızlıdır ve yavaş bir ağ üzerinden bile çalışır.

### <a name="adding-a-jquery-animation"></a>jQuery Animasyon ekleme

Uyguladığımız AJAX işlevi iyi ve hızlı çalışır. Bazen o kadar hızlı olabilir ki, bir kullanıcı RSVP bağlantısının yeni metinle değiştirildiğini fark etmeyebilir. Sonucu biraz daha belirgin hale getirmek için güncelleştirme iletisine dikkat çekmek için basit bir animasyon ekleyebiliriz.

Varsayılan ASP.NET MVC proje şablonu jQuery içerir - mükemmel (ve çok popüler) microsoft tarafından desteklenen bir açık kaynak JavaScript kitaplığı. jQuery güzel bir HTML DOM seçimi ve efekt kitaplığı da dahil olmak üzere bir dizi özellik sağlar.

jQuery'yi kullanmak için önce bir komut dosyası referansı ekleyeceğiz. JQuery'yi sitemizdeki çeşitli yerlerde kullanacağımız için, tüm sayfaların kullanabilmesi için Sitemiz.master sayfa dosyasına komut dosyası referansını ekleyeceğiz.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*İpucu: JavaScript dosyaları (jQuery dahil) için daha zengin intellisense desteği sağlayan VS 2008 SP1 için JavaScript intellisense düzeltmesini yüklediğinizden emin olun. Buradan indirebilirsiniz:http://tinyurl.com/vs2008javascripthotfix*

JQuery kullanılarak yazılan kod genellikle bir CSS seçici kullanarak bir veya daha fazla HTML öğesini alan genel bir "$()" JavaScript yöntemi kullanır. Örneğin, *$(#rsvpmsg")* rsvpmsg kimliğine sahip herhangi bir HTML öğesini seçerken, *$(".something")* "bir şey" CSS sınıf adı olan tüm öğeleri seçer. Ayrıca "kontrol edilen tüm radyo düğmelerini iade et" gibi daha gelişmiş sorgular da yazabilirsiniz: *$("giriş[@type=radyo][]")@checked*gibi bir seçici sorgusu.

Öğeleri seçtikten sonra, bunları gizlemek gibi eylemde bulunmaları için yöntemleri arayabilirsiniz: *$("#rsvpmsg").hide();*

RSVP senaryomuz için, "rsvpmsg" &lt;divini&gt; seçen ve metin içeriğinin boyutunu animasyona reanimasyonhaline getiren "AnimateRSVPMessage" adlı basit bir JavaScript işlevi tanımlarız. Aşağıdaki kod metni küçük olarak başlatır ve ardından metnin 400 milisaniyelik bir zaman diliminde artmasına neden olur:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Daha sonra ajax çağrımızdan sonra çağrılacak bu JavaScript işlevini Ajax.ActionLink() yardımcı metodumuza (AjaxOptions "OnSuccess" olay özelliği üzerinden) geçirerek tamamlayabiliriz:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

Ve şimdi "bu olay için RSVP" bağlantısı tıklandığında ve AJAX çağrımız başarıyla tamamlandığında, geri gönderilen içerik iletisi animasyona dönüşecek ve büyüyecek:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

"OnSuccess" olayı sağlamanın yanı sıra, AjaxOptions nesnesi OnBegin, OnFailure ve Işlaşabileceğiniz OnComplete olayları (çeşitli diğer özellikler ve kullanışlı seçeneklerle birlikte) ortaya çıkarır.

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Temizleme - RSVP Kısmi Görünümü Yeniden Düzenleme

Ayrıntılar görünüm şablonumuz biraz uzamaya başlıyor ve bu da fazla mesainin anlaşılmasını biraz zorlaştıracak. Kod okunabilirliğini geliştirmeye yardımcı olmak için, Ayrıntılar sayfamızdaki tüm RSVP görünüm kodunu özetleyen kısmi bir görünüm olan RSVPStatus.ascx'i oluşturarak bitirelim.

Bunu \Views\Dinners klasörüne sağ tıklayıp Ekle-Görüntüle&gt;menüsü komutunu seçerek yapabiliriz. Biz onun güçlü bir şekilde bürünen ViewModel olarak bir Akşam Yemeği nesne almak gerekir. Daha sonra RsVP içeriğini Details.aspx görünümümüzden kopyalayabilir/yapıştırabiliriz.

Bunu yaptıktan sonra, düzenle ve bağlantı görünümü kodumuzu silen başka bir kısmi görünüm oluşturalım - EditAndDeleteLinks.ascx - bu görünüm kodumuzu düzenle ve sil. Ayrıca, güçlü bir şekilde yazılan ViewModel olarak bir Akşam Yemeği nesnesi almasını ve Ayrıntılar.aspx görünümümüzden Düzenle ve Sil mantığını kopyala/yapıştırmayı da sağlayacağız.

Ayrıntıları görüntüleme şablonumuz daha sonra en altta iki Html.RenderPartial() yöntem çağrısı içerebilir:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

Bu, kodu okumak ve korumak için daha temiz hale getirir.

### <a name="next-step"></a>Sonraki Adım

Şimdi AJAX'ı nasıl daha fazla kullanabileceğimize bakalım ve uygulamamıza etkileşimli harita desteği ekleyelim.

> [!div class="step-by-step"]
> [Önceki](secure-applications-using-authentication-and-authorization.md)
> [Sonraki](use-ajax-to-implement-mapping-scenarios.md)
