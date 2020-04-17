---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Botların ASP.NET Web Razor) Sitenizi Kullanmasını Önlemek için CAPTCHA Kullanma | Microsoft Dokümanlar
author: rick-anderson
description: Bu makalede, otomatik programların (botların) ASP.NET bir Web Sayfasında (Razor) görevleri yerine getirmesini önlemek için ReCaptcha'nın (güvenlik önlemi) nasıl kullanılacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543762"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="ae7fd-103">Botların ASP.NET Web Razor) Sitenizi Kullanmasını Önlemek için CAPTCHA Kullanma</span><span class="sxs-lookup"><span data-stu-id="ae7fd-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="ae7fd-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="ae7fd-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ae7fd-105">Bu makalede, otomatik programların (botların) ASP.NET web sayfaları (Jilet) web sitesinde görevleri yerine getirmesini önlemek için ReCaptcha (güvenlik önlemi) nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="ae7fd-106">**Ne öğreneceksiniz:**</span><span class="sxs-lookup"><span data-stu-id="ae7fd-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="ae7fd-107">Sitenize captcha testi nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="ae7fd-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="ae7fd-108">Bu makalede tanıtılan ASP.NET özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ae7fd-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="ae7fd-109">`ReCaptcha` Yardımcı.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="ae7fd-110">Bu makaledeki bilgiler ASP.NET Web Sayfaları 1.0 ve Web Sayfaları 2 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="ae7fd-111">CAPTCHAs Hakkında</span><span class="sxs-lookup"><span data-stu-id="ae7fd-111">About CAPTCHAs</span></span>

<span data-ttu-id="ae7fd-112">İnsanların sitenize kaydolmasına izin verdiğinizde, hatta sadece bir ad ve URL girdiğinizde (blog yorumu gibi), sahte adlar selebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="ae7fd-113">Bunlar genellikle bulabilecekleri her web sitesinde URL'leri bırakmaya çalışan otomatik programlar (botlar) tarafından bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="ae7fd-114">(Ortak bir motivasyon satılık ürünlerin URL'leri göndermektir.)</span><span class="sxs-lookup"><span data-stu-id="ae7fd-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="ae7fd-115">Kullanıcının adlarını ve sitesini kaydettiklerinde veya başka bir şekilde girdiklerini doğrulamak için bir *CAPTCHA* kullanarak bir kullanıcının bilgisayar programı değil, gerçek kişi olduğundan emin olmanıza yardımcı olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="ae7fd-116">CAPTCHA, Bilgisayarlara ve İnsanlara Ayrı Söylemek Için Tamamen Otomatik Leştirilmiş Turing testinin kısaltmasI.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="ae7fd-117">CAPTCHA, kullanıcıdan bir kişinin yapması kolay ama otomatik bir programın yapması zor olan bir şey yapması istenen bir *meydan okuma yanıtı* testidir.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="ae7fd-118">CAPTCHA'nın en yaygın türü, bazı bozuk harfler gördüğünüz ve bunları yazmanız istendiği bir türdür.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="ae7fd-119">(Distorsiyon zor botlar için harfleri deşifre etmek için yapmak gerekiyordu.)</span><span class="sxs-lookup"><span data-stu-id="ae7fd-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="ae7fd-120">ReCaptcha Testi Ekleme</span><span class="sxs-lookup"><span data-stu-id="ae7fd-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="ae7fd-121">ASP.NET sayfalarda, `ReCaptcha` recaptcha hizmetini temel alan bir CAPTCHA testi işlemek için[http://recaptcha.net](http://recaptcha.net)yardımcıyı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="ae7fd-122">Yardımcı, `ReCaptcha` sayfa doğrulanmadan önce kullanıcıların doğru şekilde girmeleri gereken iki bozuk sözcük resmi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="ae7fd-123">Kullanıcı yanıtı ReCaptcha.Net hizmeti tarafından doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="ae7fd-124">Web sitenizi ReCaptcha.Net[http://recaptcha.net](http://recaptcha.net)' de kaydedin ( ).</span><span class="sxs-lookup"><span data-stu-id="ae7fd-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="ae7fd-125">Kaydı tamamladığınızda, ortak bir anahtar ve özel bir anahtar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="ae7fd-126">Web Yardımcıları Kitaplığı'ASP.NET, [ASP.NET bir Web Sayfası Sitesine Yardımcı Yükleme'de](https://go.microsoft.com/fwlink/?LinkId=252372)açıklandığı şekilde web sitenize ekleyin .</span><span class="sxs-lookup"><span data-stu-id="ae7fd-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="ae7fd-127">Zaten bir \* \_AppStart.cshtml\* dosyanız yoksa, bir web sitesinin kök klasöründe \* \_AppStart.cshtml\*adında bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="ae7fd-128">`Recaptcha` \* \_AppStart.cshtml\* dosyasına aşağıdaki yardımcı ayarlarını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae7fd-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="ae7fd-129">Kendi `PublicKey` ortak `PrivateKey` ve özel anahtarlarınızı kullanarak özellikleri ve özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="ae7fd-130">\* \_AppStart.cshtml\* dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="ae7fd-131">Bir web sitesinin kök klasöründe, *Recaptcha.cshtml*adlı yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="ae7fd-132">Varolan içeriği aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ae7fd-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="ae7fd-133">*Recaptcha.cshtml* sayfasını tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="ae7fd-134">`PrivateKey` Değer geçerliyse, sayfa ReCaptcha denetimini ve bir düğmeyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="ae7fd-135">Eğer appstart.html genel olarak anahtarları ayarlamamış olsaydı, sayfa bir hata görüntülerdi. \* \_\*</span><span class="sxs-lookup"><span data-stu-id="ae7fd-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="ae7fd-136">Test için sözcükleri girin.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-136">Enter the words for the test.</span></span> <span data-ttu-id="ae7fd-137">ReCaptcha testini geçerseniz, bu yönde bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="ae7fd-138">Aksi takdirde bir hata iletisi görürsünüz ve ReCaptcha denetimi yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7fd-139">Bilgisayarınız proxy sunucusu kullanan bir etki alanındaysa, `defaultproxy` *Web.config* dosyasının öğesini yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="ae7fd-140">Aşağıdaki örnekte, ReCaptcha hizmetinin çalışmasını sağlayacak şekilde yapılandırılan öğeye `defaultproxy` sahip bir *Web.config* dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ae7fd-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ae7fd-141">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ae7fd-141">Additional Resources</span></span>

- [<span data-ttu-id="ae7fd-142">ASP.NET Web Sayfaları Siteleri için Site Genelinde Davranışı Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="ae7fd-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="ae7fd-143">ReCaptcha sitesi</span><span class="sxs-lookup"><span data-stu-id="ae7fd-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
