---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: Birkaç animasyon yürütme (VB) aynı anda | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Severa çalıştırılacak sağlar...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 92191e87ed78d8e549d14412ff4a5a9d8eb4afbb
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58422471"
---
<a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="3a961-104">(VB) aynı anda birkaç animasyon yürütme</span><span class="sxs-lookup"><span data-stu-id="3a961-104">Executing Several Animations at The Same Time (VB)</span></span>
====================
<span data-ttu-id="3a961-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3a961-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3a961-106">[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3a961-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="3a961-107">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="3a961-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3a961-108">Birkaç animasyon paralel bir şekilde çalışmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a961-108">It allows to run several animations in a parallel fashion.</span></span>


## <a name="overview"></a><span data-ttu-id="3a961-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3a961-109">Overview</span></span>

<span data-ttu-id="3a961-110">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="3a961-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3a961-111">Birkaç animasyon paralel bir şekilde çalışmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a961-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="3a961-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="3a961-112">Steps</span></span>

<span data-ttu-id="3a961-113">İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:</span><span class="sxs-lookup"><span data-stu-id="3a961-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="3a961-114">Animasyonun bir panel şuna benzer metin uygulanır:</span><span class="sxs-lookup"><span data-stu-id="3a961-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="3a961-115">İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="3a961-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="3a961-116">Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="3a961-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="3a961-117">İçinde `<Animations>` düğümü, kullanım `<OnLoad>` animasyonları sayfanın tam yüklü silindikten sonra çalıştırılacak.</span><span class="sxs-lookup"><span data-stu-id="3a961-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="3a961-118">Genellikle, `<OnLoad>` yalnızca bir animasyon kabul eder.</span><span class="sxs-lookup"><span data-stu-id="3a961-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="3a961-119">Animasyon çerçevesi bir kullanarak birkaç animasyon katılmaya sağlar `<Parallel>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="3a961-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="3a961-120">İçindeki tüm animasyonları `<Parallel>` aynı zamanda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3a961-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="3a961-121">İşte için olası bir biçimlendirme `AnimationExtender` yavaş çıkış ve aynı anda paneli yeniden boyutlandırma denetimi:</span><span class="sxs-lookup"><span data-stu-id="3a961-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="3a961-122">Ve gerçekten: Bu komut dosyasını çalıştırdığınızda, paneli, ardından (birden fazla genişliğini tripling ve yükseklik halving) yeniden boyutlandırır görüntülenir ve aynı anda silinerek çıkar.</span><span class="sxs-lookup"><span data-stu-id="3a961-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>


<span data-ttu-id="3a961-123">[![Panel yavaş çıkış ve yeniden boyutlandırma (tarayıcının işleme altyapısı sayesinde, içeriği dahil)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3a961-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="3a961-124">Panel yavaş çıkış ve (tarayıcının işleme altyapısı sayesinde, içeriği dahil) yeniden boyutlandırma ([tam boyutlu görüntüyü görmek için tıklatın](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3a961-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3a961-125">[Önceki](adding-animation-to-a-control-vb.md)
> [İleri](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3a961-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
