---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: (VB) metin kutusunda yalnızca belirli karakterlere izin verme | Microsoft Docs
author: wenz
description: Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz. Ancak bu yazmaya geçersiz kullanıcılar hala engellemez...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 455d62d97808862f70692c46ae223f47270266f9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59387626"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="97696-104">Bir Metin Kutusunda Yalnızca Belirli Karakterlere İzin Verme (VB)</span><span class="sxs-lookup"><span data-stu-id="97696-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="97696-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="97696-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="97696-106">[Kodu indir](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="97696-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="97696-107">Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97696-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="97696-108">Ancak bu kullanıcıların geçersiz karakterleri yazmaya ve form göndermeye devam engellemez.</span><span class="sxs-lookup"><span data-stu-id="97696-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="97696-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="97696-109">Overview</span></span>

<span data-ttu-id="97696-110">Doğrulama denetimleri ASP.NET uygulamasında kullanıcı girdisi yalnızca belirli karakterlere izin verildiğini emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97696-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="97696-111">Ancak bu kullanıcıların geçersiz karakterleri yazmaya ve form göndermeye devam engellemez.</span><span class="sxs-lookup"><span data-stu-id="97696-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="97696-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="97696-112">Steps</span></span>

<span data-ttu-id="97696-113">ASP.NET AJAX Denetim Araç Seti içeren `FilteredTextBox` genişleten bir metin kutusu denetimi.</span><span class="sxs-lookup"><span data-stu-id="97696-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="97696-114">Sonra yalnızca belirli karakter kümesini alana girilebilir.</span><span class="sxs-lookup"><span data-stu-id="97696-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="97696-115">Bunun işe yaraması için önce her zaman olduğu gibi ASP.NET AJAX ihtiyacımız `ScriptManager` de ASP.NET AJAX Denetim Araç Seti tarafından kullanılan JavaScript kitaplıklarını yükler:</span><span class="sxs-lookup"><span data-stu-id="97696-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="97696-116">Ardından, bir metin kutusu gerekir:</span><span class="sxs-lookup"><span data-stu-id="97696-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="97696-117">Son olarak, `FilteredTextBoxExtender` denetimi, kullanıcı türüne izin verilir karakter kısıtlama üstlenir.</span><span class="sxs-lookup"><span data-stu-id="97696-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="97696-118">İlk olarak ayarlamak `TargetControlID` özniteliğini `ID` , `TextBox` denetimi.</span><span class="sxs-lookup"><span data-stu-id="97696-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="97696-119">Ardından, kullanılabilir birini `FilterType` değerleri:</span><span class="sxs-lookup"><span data-stu-id="97696-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="97696-120">`Custom` Varsayılan olarak; Geçerli karakterler listesini sağlamanız gerekir</span><span class="sxs-lookup"><span data-stu-id="97696-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="97696-121">`LowercaseLetters` yalnızca küçük harfler</span><span class="sxs-lookup"><span data-stu-id="97696-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="97696-122">`Numbers` yalnızca rakam</span><span class="sxs-lookup"><span data-stu-id="97696-122">`Numbers` digits only</span></span>
- <span data-ttu-id="97696-123">`UppercaseLetters` yalnızca büyük harfler</span><span class="sxs-lookup"><span data-stu-id="97696-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="97696-124">Varsa `Custom FilterType` kullanılan `ValidChars` özelliği ayarlanmış olmalıdır ve türü belirtilmiş olmalıdır karakterlerin listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="97696-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="97696-125">Bu arada: metin, metin kutusuna yapıştırın denerseniz, tüm geçersiz karakterleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="97696-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="97696-126">İçin biçimlendirme şöyledir `FilteredTextBoxExtender` basamak yalnızca veren denetiminin (şey de mümkün olacaktı `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="97696-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="97696-127">JavaScript etkinse, bir harf girmeyi deneyin ve sayfa Çalıştır çalışmaz; Basamaklar, ancak sayfada görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="97696-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="97696-128">Ancak, unutmayın koruma `FilteredTextBox` sağlar madde işareti kavram değil: JavaScript etkinse, herhangi bir veri ek doğrulama anlamına gelir, yani ASP kullanmak zorunda metin kutusuna girilebilir. NET doğrulama denetimleri.</span><span class="sxs-lookup"><span data-stu-id="97696-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


<span data-ttu-id="97696-129">[![Yalnızca rakam girilebilir](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="97696-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="97696-130">Yalnızca rakam girilebilir ([tam boyutlu görüntüyü görmek için tıklatın](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="97696-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="97696-131">Önceki</span><span class="sxs-lookup"><span data-stu-id="97696-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)
