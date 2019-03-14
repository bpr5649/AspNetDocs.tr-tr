---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: (VB) bir koşula bağlı animasyon | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Bir animasyon olup...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: be43b68ce77819cdcd09d8e875604db90e8a8d96
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077622"
---
<a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="0db82-104">Bir Koşula Bağlı Animasyon (VB)</span><span class="sxs-lookup"><span data-stu-id="0db82-104">Animation Depending On a Condition (VB)</span></span>
====================
<span data-ttu-id="0db82-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0db82-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0db82-106">[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0db82-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="0db82-107">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="0db82-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0db82-108">Bir animasyon çalışıp ayrıca formunda bazı JavaScript kodunun bir koşul bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0db82-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="0db82-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0db82-109">Overview</span></span>

<span data-ttu-id="0db82-110">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="0db82-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0db82-111">Bir animasyon çalışıp ayrıca formunda bazı JavaScript kodunun bir koşul bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0db82-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="0db82-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="0db82-112">Steps</span></span>

<span data-ttu-id="0db82-113">İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:</span><span class="sxs-lookup"><span data-stu-id="0db82-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="0db82-114">Animasyonun bir panel şuna benzer metin uygulanır:</span><span class="sxs-lookup"><span data-stu-id="0db82-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="0db82-115">İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0db82-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="0db82-116">Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="0db82-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="0db82-117">İçinde `<Animations>` düğümü, kullanım `<OnLoad>` animasyonları sayfanın tam yüklü silindikten sonra çalıştırılacak.</span><span class="sxs-lookup"><span data-stu-id="0db82-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="0db82-118">Normal animasyonları birini yerine `<Condition>` öğesi oyuna gelir.</span><span class="sxs-lookup"><span data-stu-id="0db82-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="0db82-119">Değeri olarak sağlanan JavaScript kodu `ConditionScript` özniteliği, çalışma zamanında yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0db82-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="0db82-120">True olarak değerlendirilirse animasyon, aksi takdirde yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="0db82-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="0db82-121">Her biri %50 rastgele sırasında çalışmalarının yürütülmekte olan iki animasyon aşağıdaki biçimlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="0db82-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="0db82-122">İçinde bir animasyon bulunabilir olduğundan `<OnLoad>`, iki `<Condition>` animasyonları birlikte kullanarak birleştirilir `<Sequence>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="0db82-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="0db82-123">Unutmayın küçüktür işareti (`<`) içinde `ConditionScript` özniteliğinin Atlanan () olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0db82-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="0db82-124">Ne zaman ya da animasyon çalıştırma yok, bu betiği çalıştırın veya bir iki desteklemez veya her ikisini birden yapın.</span><span class="sxs-lookup"><span data-stu-id="0db82-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="0db82-125">[![Birinci ikinci animasyon çalıştırmaların dolayısıyla paneli yeniden boyutlandırma olmadan, yavaş çıkış](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0db82-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span></span>

<span data-ttu-id="0db82-126">Birinci ikinci animasyon çalıştırmaların dolayısıyla paneli yeniden boyutlandırma olmadan, yavaş çıkış ([tam boyutlu görüntüyü görmek için tıklatın](animation-depending-on-a-condition-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0db82-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0db82-127">[Önceki](executing-several-animations-after-each-other-vb.md)
> [İleri](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0db82-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
