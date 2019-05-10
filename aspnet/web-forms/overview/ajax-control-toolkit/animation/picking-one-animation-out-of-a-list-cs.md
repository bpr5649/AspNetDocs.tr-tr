---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: Bir liste (C#) animasyon seçme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Framework ayrıca ver...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: dd22d80775ebe3571fcf9d3225135766669ef85b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128712"
---
# <a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="a57a6-104">Bir Listeden Animasyon Seçme (C#)</span><span class="sxs-lookup"><span data-stu-id="a57a6-104">Picking One Animation Out Of a List (C#)</span></span>

<span data-ttu-id="a57a6-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a57a6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a57a6-106">[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a57a6-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="a57a6-107">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="a57a6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a57a6-108">Framework, bir listeden animasyon animasyon, bazı JavaScript kodları değerlendirmesine bağlı olarak çekmek Programcı de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a57a6-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="a57a6-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a57a6-109">Overview</span></span>

<span data-ttu-id="a57a6-110">ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil.</span><span class="sxs-lookup"><span data-stu-id="a57a6-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a57a6-111">Framework, bir listeden animasyon animasyon, bazı JavaScript kodları değerlendirmesine bağlı olarak çekmek Programcı de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a57a6-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="a57a6-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a57a6-112">Steps</span></span>

<span data-ttu-id="a57a6-113">İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:</span><span class="sxs-lookup"><span data-stu-id="a57a6-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="a57a6-114">Animasyonun bir panel şuna benzer metin uygulanır:</span><span class="sxs-lookup"><span data-stu-id="a57a6-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="a57a6-115">İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a57a6-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="a57a6-116">Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="a57a6-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="a57a6-117">İçinde `<Animations>` düğümü, kullanım `<OnLoad>` animasyonları sayfanın tam yüklü silindikten sonra çalıştırılacak.</span><span class="sxs-lookup"><span data-stu-id="a57a6-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="a57a6-118">Normal animasyonları birini yerine `<Case>` öğesi oyuna gelir.</span><span class="sxs-lookup"><span data-stu-id="a57a6-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="a57a6-119">Kendi SelectScript özniteliğinin değerini değerlendirilir; dönüş değeri sayısal olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a57a6-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="a57a6-120">Bu sayı, içinde subanimations birine bağlı olarak &lt;çalışması&gt; yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a57a6-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="a57a6-121">Denetim Araç Seti SelectScript 2 olarak değerlendirilirse, üçüncü animasyon içinde örneği için çalışan &lt;çalışması&gt; (sayım 0 başlar).</span><span class="sxs-lookup"><span data-stu-id="a57a6-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="a57a6-122">Aşağıdaki biçimlendirmede üç subanimations tanımlar: Genişlik, yükseklik yeniden boyutlandırma ve netleştirme yeniden boyutlandırma. JavaScript kodu (`Math.floor(3 * Math.random())`) üç animasyonları birini çalıştırın, ardından 0. ve 2 arasında bir sayı seçer:</span><span class="sxs-lookup"><span data-stu-id="a57a6-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

<span data-ttu-id="a57a6-123">[![Olası üç animasyonları biri: Panel geniş alır](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a57a6-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="a57a6-124">Olası üç animasyonları biri: Panel geniş alır ([tam boyutlu görüntüyü görmek için tıklatın](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a57a6-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a57a6-125">[Önceki](animation-depending-on-a-condition-cs.md)
> [İleri](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a57a6-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>
