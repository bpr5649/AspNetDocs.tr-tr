---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Bir parola (C#) Güçlülüğünü test etme | Microsoft Docs
author: wenz
description: Parolalar, neredeyse her yerden, böylece yavaş kullanıcıları ayırmak kolay olan basit parolalar seçmesini eğilimindedir gereklidir. ASP PasswordStrength denetimi. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: d8ac50874d0325ed9583a16e1b4e19b3becabb99
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59391526"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="3be6a-104">Bir Parolanın Güçlülüğünü Test Etme (C#)</span><span class="sxs-lookup"><span data-stu-id="3be6a-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="3be6a-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3be6a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3be6a-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3be6a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="3be6a-107">Parolalar, neredeyse her yerden, böylece yavaş kullanıcıları ayırmak kolay olan basit parolalar seçmesini eğilimindedir gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3be6a-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="3be6a-108">ASP.NET AJAX Denetim Araç Seti PasswordStrength denetiminde ne kadar iyi bir paroladır kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3be6a-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="3be6a-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3be6a-109">Overview</span></span>

<span data-ttu-id="3be6a-110">Parolalar, neredeyse her yerden, böylece yavaş kullanıcıları ayırmak kolay olan basit parolalar seçmesini eğilimindedir gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3be6a-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="3be6a-111">`PasswordStrength` ASP.NET AJAX Denetim Araç Seti denetiminde ne kadar iyi bir paroladır kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3be6a-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="3be6a-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="3be6a-112">Steps</span></span>

<span data-ttu-id="3be6a-113">`PasswordStrength` Denetimi bir metin kutusu genişletir ve Parolada yeterince iyi olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="3be6a-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="3be6a-114">Bu, çok sayıda öznitelik aracılığıyla seçenekleri sunar. bunları yalnızca bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3be6a-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="3be6a-115">`MinimumNumericCharacters` en düşük Parolada bulunması gereken karakter sayısı</span><span class="sxs-lookup"><span data-stu-id="3be6a-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="3be6a-116">`MinimumSymbolCharacters` gereken en düşük rakam Parolada bulunması gereken simge karakterleri (harfler ve sayılar değil)</span><span class="sxs-lookup"><span data-stu-id="3be6a-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="3be6a-117">`PreferredPasswordLength` Minimum parola uzunluğu</span><span class="sxs-lookup"><span data-stu-id="3be6a-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="3be6a-118">`RequiresUpperAndLowerCaseCharacters` olup büyük ve küçük harf karakterler kullanmak parola gerekir</span><span class="sxs-lookup"><span data-stu-id="3be6a-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="3be6a-119">`StrengthIndicatorType` Metin olarak bir parolanın güçlülüğünü sunma hakkında bilgi sağlar (değer `"Text"`) veya bir ilerleme çubuğu tür olarak (değer `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="3be6a-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="3be6a-120">İçinde `DisplayPosition` özniteliği, yapılandırdığınız bilgiler burada görünür.</span><span class="sxs-lookup"><span data-stu-id="3be6a-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="3be6a-121">ASP.NET AJAX da dahil olmak üzere, tam bir örnek aşağıdadır `ScriptManager` denetimi `PasswordStrength` denetimi ve Elbette kullanıcı girdiğiniz yere bir parola metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3be6a-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="3be6a-122">Geliştirme sırasında yazmakta olduğunuz görebilmeniz için gösterim amacıyla, ikinci formu alan bir normal metin alanı ve parola alanı olur.</span><span class="sxs-lookup"><span data-stu-id="3be6a-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="3be6a-123">Sayfayı çalıştırın ve hemen yazın: Parola yalnızca küçük harfler, büyük harfler, rakamlar ve semboller girdikten sonra kesilemeyen olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="3be6a-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="3be6a-124">[![Artık parola (oldukça) iyi değil](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3be6a-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="3be6a-125">Parola (oldukça) iyi artık ([tam boyutlu görüntüyü görmek için tıklatın](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3be6a-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3be6a-126">Next</span><span class="sxs-lookup"><span data-stu-id="3be6a-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
