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
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="2187f-103">AJAX Kullanarak Dinamik Güncelleştirmeler Sunma</span><span class="sxs-lookup"><span data-stu-id="2187f-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="2187f-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="2187f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2187f-105">PDF’yi İndir</span><span class="sxs-lookup"><span data-stu-id="2187f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2187f-106">Bu adım 10 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.</span><span class="sxs-lookup"><span data-stu-id="2187f-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2187f-107">Adım 10, akşam yemeği ayrıntıları sayfasına entegre edilmiş Ajax tabanlı bir yaklaşım kullanarak, bir akşam yemeğine katılmakla ilgilendikleri RSVP'ye giriş yaptırıcı kullanıcılar için destek uygular.</span><span class="sxs-lookup"><span data-stu-id="2187f-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="2187f-108">MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.</span><span class="sxs-lookup"><span data-stu-id="2187f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="2187f-109">NerdDinner Adım 10: AJAX Etkinleştirme RSVPs Kabul</span><span class="sxs-lookup"><span data-stu-id="2187f-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="2187f-110">Şimdi, bir akşam yemeğine katılmakla ilgilendikleri RSVP'ye giriş yapmış kullanıcılar için destek uygulayalım.</span><span class="sxs-lookup"><span data-stu-id="2187f-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="2187f-111">Bunu, akşam yemeği detayları sayfasına entegre edilmiş AJAX tabanlı bir yaklaşım la etkinleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="2187f-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="2187f-112">Kullanıcının RSVP'd olup olmadığını gösteren</span><span class="sxs-lookup"><span data-stu-id="2187f-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="2187f-113">Kullanıcılar belirli bir akşam yemeği yle ilgili ayrıntıları görmek için */Dinners/Details/[id*] URL'sini ziyaret edebilirler:</span><span class="sxs-lookup"><span data-stu-id="2187f-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="2187f-114">Ayrıntılar() eylem yöntemi aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="2187f-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="2187f-115">RSVP desteğini uygulamak için ilk adımımız, Akşam Yemeği nesnemize (daha önce oluşturduğumuz Dinner.cs kısmi sınıf içinde) bir "IsUserRegistered(kullanıcı adı)" yardımcı yöntemi eklemek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2187f-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="2187f-116">Bu yardımcı yöntem, kullanıcının akşam yemeği için şu anda RSVP'd olup olmadığına bağlı olarak doğru veya yanlış döndürür:</span><span class="sxs-lookup"><span data-stu-id="2187f-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="2187f-117">Daha sonra, kullanıcının olay için kayıtlı olup olmadığını belirten uygun bir ileti görüntülemek için Ayrıntılar.aspx görünüm şablonumuza aşağıdaki kodu ekleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="2187f-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="2187f-118">Ve şimdi bir kullanıcı kayıtlı olduğu bir Akşam Yemeği ziyaret ettiğinde bu mesajı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2187f-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="2187f-119">Ve bir Akşam Yemeği'ni ziyaret ettiklerinde kayıtlı olmadıkları nda aşağıdaki mesajı görürler:</span><span class="sxs-lookup"><span data-stu-id="2187f-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="2187f-120">Kayıt Eylem Yönteminin Uygulanması</span><span class="sxs-lookup"><span data-stu-id="2187f-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="2187f-121">Şimdi, kullanıcıların ayrıntılar sayfasından bir akşam yemeği için RSVP'ye kabul etmelerini sağlamak için gerekli işlevselliği ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="2187f-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="2187f-122">Bunu uygulamak için, \Controllers dizinine sağ tıklayarak ve Ekle-Denetleyici&gt;menü komutunu seçerek yeni bir "RSVPController" sınıfı oluştururuz.</span><span class="sxs-lookup"><span data-stu-id="2187f-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="2187f-123">Yeni RSVPController sınıfında bir "Kaydol" eylem yöntemi uygulayacağız, bir akşam yemeği için bir id alır, uygun Akşam Yemeği nesnesini alır, oturum açmış kullanıcının şu anda kayıt yaptıran kullanıcılar listesinde olup olmadığını kontrol eder ve onlar için bir RSVP nesnesi ekleyip eklenmediğini kontrol edeceğiz:</span><span class="sxs-lookup"><span data-stu-id="2187f-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="2187f-124">Eylem yönteminin çıktısı olarak basit bir dizeyi nasıl döndürdettiğimize yukarıda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2187f-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="2187f-125">Bu iletiyi bir görünüm şablonuna gömebilirdik – ancak çok küçük olduğu için denetleyici taban sınıfında İçerik() yardımcı yöntemini kullanacağız ve yukarıdaki gibi bir dize iletisi döndüreceğiz.</span><span class="sxs-lookup"><span data-stu-id="2187f-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="2187f-126">AJAX kullanarak RSVPForEvent Eylem Yöntemi arama</span><span class="sxs-lookup"><span data-stu-id="2187f-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="2187f-127">Ayrıntılar görünümümüzden Kayıt eylem yöntemini çağırmak için AJAX'ı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="2187f-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="2187f-128">Bunu uygulamak oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="2187f-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="2187f-129">Önce iki komut dosyası kitaplığı referansı ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="2187f-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="2187f-130">İlk kitaplık, AJAX istemci tarafı komut dosyası kitaplığı ASP.NET temel başvurur.</span><span class="sxs-lookup"><span data-stu-id="2187f-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="2187f-131">Bu dosya yaklaşık 24k boyutu (sıkıştırılmış) ve çekirdek istemci tarafı AJAX işlevselliği içerir.</span><span class="sxs-lookup"><span data-stu-id="2187f-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="2187f-132">İkinci kitaplık, mvc'nin dahili AJAX yardımcı yöntemleriyle ASP.NET entegre olan yardımcı program işlevlerini içerir (kısa süre içinde kullanacağız).</span><span class="sxs-lookup"><span data-stu-id="2187f-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="2187f-133">Daha sonra daha önce eklediğimiz görünüm şablonu kodunu güncelleştirebiliriz, böylece "Bu olay için kayıtlı değilsiniz" iletisi vermek yerine, itildiğinde RSVP denetleyicimiz ve RSVP kullanıcımız rsvpForEvent eylem yöntemimizi çağıran bir AJAX çağrısı gerçekleştiren bir bağlantı oluşturuyoruz:</span><span class="sxs-lookup"><span data-stu-id="2187f-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="2187f-134">Yukarıda kullanılan Ajax.ActionLink() yardımcı yöntemi yerleşik ASP.NET MVC ve html.ActionLink() yardımcı yöntemine benzer, ancak standart bir navigasyon gerçekleştirmek yerine bağlantı tıklandığında eylem yöntemine AJAX çağrısı yapar.</span><span class="sxs-lookup"><span data-stu-id="2187f-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="2187f-135">Yukarıda "RSVP" denetleyicisi üzerinde "Kayıt" eylem yöntemi çağırıyoruz ve ona "id" parametresi olarak DinnerID geçen.</span><span class="sxs-lookup"><span data-stu-id="2187f-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="2187f-136">Geçirdiğimiz son AjaxOptions parametresi, eylem yönteminden döndürülen içeriği almak ve &lt;&gt; kimliği "rsvpmsg" olan sayfadaki HTML div öğesini güncelleştirmek istediğimizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="2187f-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="2187f-137">Ve şimdi bir kullanıcı henüz kayıtlı olmayan bir akşam yemeği ne zaman bunun için RSVP için bir bağlantı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2187f-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="2187f-138">"Bu olay için RSVP" bağlantısını tıkladıklarında, RSVP denetleyicisindeki Register eylem yöntemine BIR AJAX çağrısı yaparlar ve tamamlandığında aşağıdaki gibi güncelleştirilmiş bir ileti görürler:</span><span class="sxs-lookup"><span data-stu-id="2187f-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="2187f-139">Bu AJAX arama yaparken ilgili ağ bant genişliği ve trafik gerçekten hafiftir.</span><span class="sxs-lookup"><span data-stu-id="2187f-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="2187f-140">Kullanıcı "Bu olay için RSVP" bağlantısını tıkladığında, telüzerinde aşağıdaki gibi görünen */Dinners/Register/1* URL'sine küçük bir HTTP POST ağ isteği yapılır:</span><span class="sxs-lookup"><span data-stu-id="2187f-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="2187f-141">Ve kayıt eylem yöntemimizden gelen yanıt basitçe:</span><span class="sxs-lookup"><span data-stu-id="2187f-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="2187f-142">Bu hafif arama hızlıdır ve yavaş bir ağ üzerinden bile çalışır.</span><span class="sxs-lookup"><span data-stu-id="2187f-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="2187f-143">jQuery Animasyon ekleme</span><span class="sxs-lookup"><span data-stu-id="2187f-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="2187f-144">Uyguladığımız AJAX işlevi iyi ve hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="2187f-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="2187f-145">Bazen o kadar hızlı olabilir ki, bir kullanıcı RSVP bağlantısının yeni metinle değiştirildiğini fark etmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="2187f-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="2187f-146">Sonucu biraz daha belirgin hale getirmek için güncelleştirme iletisine dikkat çekmek için basit bir animasyon ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="2187f-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="2187f-147">Varsayılan ASP.NET MVC proje şablonu jQuery içerir - mükemmel (ve çok popüler) microsoft tarafından desteklenen bir açık kaynak JavaScript kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="2187f-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="2187f-148">jQuery güzel bir HTML DOM seçimi ve efekt kitaplığı da dahil olmak üzere bir dizi özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="2187f-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="2187f-149">jQuery'yi kullanmak için önce bir komut dosyası referansı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="2187f-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="2187f-150">JQuery'yi sitemizdeki çeşitli yerlerde kullanacağımız için, tüm sayfaların kullanabilmesi için Sitemiz.master sayfa dosyasına komut dosyası referansını ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="2187f-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="2187f-151">*İpucu: JavaScript dosyaları (jQuery dahil) için daha zengin intellisense desteği sağlayan VS 2008 SP1 için JavaScript intellisense düzeltmesini yüklediğinizden emin olun. Buradan indirebilirsiniz:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="2187f-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="2187f-152">JQuery kullanılarak yazılan kod genellikle bir CSS seçici kullanarak bir veya daha fazla HTML öğesini alan genel bir "$()" JavaScript yöntemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="2187f-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="2187f-153">Örneğin, *$(#rsvpmsg")* rsvpmsg kimliğine sahip herhangi bir HTML öğesini seçerken, *$(".something")* "bir şey" CSS sınıf adı olan tüm öğeleri seçer.</span><span class="sxs-lookup"><span data-stu-id="2187f-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="2187f-154">Ayrıca "kontrol edilen tüm radyo düğmelerini iade et" gibi daha gelişmiş sorgular da yazabilirsiniz: *$("giriş[@type=radyo][]")@checked*gibi bir seçici sorgusu.</span><span class="sxs-lookup"><span data-stu-id="2187f-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="2187f-155">Öğeleri seçtikten sonra, bunları gizlemek gibi eylemde bulunmaları için yöntemleri arayabilirsiniz: *$("#rsvpmsg").hide();*</span><span class="sxs-lookup"><span data-stu-id="2187f-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="2187f-156">RSVP senaryomuz için, "rsvpmsg" &lt;divini&gt; seçen ve metin içeriğinin boyutunu animasyona reanimasyonhaline getiren "AnimateRSVPMessage" adlı basit bir JavaScript işlevi tanımlarız.</span><span class="sxs-lookup"><span data-stu-id="2187f-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="2187f-157">Aşağıdaki kod metni küçük olarak başlatır ve ardından metnin 400 milisaniyelik bir zaman diliminde artmasına neden olur:</span><span class="sxs-lookup"><span data-stu-id="2187f-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="2187f-158">Daha sonra ajax çağrımızdan sonra çağrılacak bu JavaScript işlevini Ajax.ActionLink() yardımcı metodumuza (AjaxOptions "OnSuccess" olay özelliği üzerinden) geçirerek tamamlayabiliriz:</span><span class="sxs-lookup"><span data-stu-id="2187f-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="2187f-159">Ve şimdi "bu olay için RSVP" bağlantısı tıklandığında ve AJAX çağrımız başarıyla tamamlandığında, geri gönderilen içerik iletisi animasyona dönüşecek ve büyüyecek:</span><span class="sxs-lookup"><span data-stu-id="2187f-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="2187f-160">"OnSuccess" olayı sağlamanın yanı sıra, AjaxOptions nesnesi OnBegin, OnFailure ve Işlaşabileceğiniz OnComplete olayları (çeşitli diğer özellikler ve kullanışlı seçeneklerle birlikte) ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="2187f-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="2187f-161">Temizleme - RSVP Kısmi Görünümü Yeniden Düzenleme</span><span class="sxs-lookup"><span data-stu-id="2187f-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="2187f-162">Ayrıntılar görünüm şablonumuz biraz uzamaya başlıyor ve bu da fazla mesainin anlaşılmasını biraz zorlaştıracak.</span><span class="sxs-lookup"><span data-stu-id="2187f-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="2187f-163">Kod okunabilirliğini geliştirmeye yardımcı olmak için, Ayrıntılar sayfamızdaki tüm RSVP görünüm kodunu özetleyen kısmi bir görünüm olan RSVPStatus.ascx'i oluşturarak bitirelim.</span><span class="sxs-lookup"><span data-stu-id="2187f-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="2187f-164">Bunu \Views\Dinners klasörüne sağ tıklayıp Ekle-Görüntüle&gt;menüsü komutunu seçerek yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="2187f-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="2187f-165">Biz onun güçlü bir şekilde bürünen ViewModel olarak bir Akşam Yemeği nesne almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2187f-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="2187f-166">Daha sonra RsVP içeriğini Details.aspx görünümümüzden kopyalayabilir/yapıştırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="2187f-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="2187f-167">Bunu yaptıktan sonra, düzenle ve bağlantı görünümü kodumuzu silen başka bir kısmi görünüm oluşturalım - EditAndDeleteLinks.ascx - bu görünüm kodumuzu düzenle ve sil.</span><span class="sxs-lookup"><span data-stu-id="2187f-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="2187f-168">Ayrıca, güçlü bir şekilde yazılan ViewModel olarak bir Akşam Yemeği nesnesi almasını ve Ayrıntılar.aspx görünümümüzden Düzenle ve Sil mantığını kopyala/yapıştırmayı da sağlayacağız.</span><span class="sxs-lookup"><span data-stu-id="2187f-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="2187f-169">Ayrıntıları görüntüleme şablonumuz daha sonra en altta iki Html.RenderPartial() yöntem çağrısı içerebilir:</span><span class="sxs-lookup"><span data-stu-id="2187f-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="2187f-170">Bu, kodu okumak ve korumak için daha temiz hale getirir.</span><span class="sxs-lookup"><span data-stu-id="2187f-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="2187f-171">Sonraki Adım</span><span class="sxs-lookup"><span data-stu-id="2187f-171">Next Step</span></span>

<span data-ttu-id="2187f-172">Şimdi AJAX'ı nasıl daha fazla kullanabileceğimize bakalım ve uygulamamıza etkileşimli harita desteği ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="2187f-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2187f-173">[Önceki](secure-applications-using-authentication-and-authorization.md)
> [Sonraki](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="2187f-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
