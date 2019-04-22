---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: (C#) bir dropshadow'un Z dizinini ayarlama | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir. Ancak bu gölge bazen diğer denetimlerle yükleme konumu için çakışan...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: cc9407ba15474f58437817c9536d6040e0ea2e84
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59381462"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="98709-104">Bir DropShadow’un Z Dizinini Ayarlama (C#)</span><span class="sxs-lookup"><span data-stu-id="98709-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>

<span data-ttu-id="98709-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="98709-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="98709-106">[Kodu indir](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="98709-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="98709-107">AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir.</span><span class="sxs-lookup"><span data-stu-id="98709-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="98709-108">Ancak bu gölge, örneğin ASP.NET menü denetimi diğer denetimlerle çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="98709-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="98709-109">Ne zaman menüsü girişi, gölge görünür açılır.</span><span class="sxs-lookup"><span data-stu-id="98709-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="98709-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="98709-110">Overview</span></span>

<span data-ttu-id="98709-111">AJAX Denetim Araç Seti DropShadow denetiminde gölge paneliyle genişletir.</span><span class="sxs-lookup"><span data-stu-id="98709-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="98709-112">Ancak bu gölge, örneğin ASP.NET menü denetimi diğer denetimlerle çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="98709-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="98709-113">Ne zaman menüsü girişi, gölge görünür açılır.</span><span class="sxs-lookup"><span data-stu-id="98709-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="98709-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="98709-114">Steps</span></span>

<span data-ttu-id="98709-115">Kod paneli görünür olmasını etkisi için yeterli metni içeren yeterli metin içeren Panel'i kendisi ile başlar:</span><span class="sxs-lookup"><span data-stu-id="98709-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="98709-116">Başka bir panel hemen öncesine yerleştirilir `panelShadow` paneli.</span><span class="sxs-lookup"><span data-stu-id="98709-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="98709-117">Yatay yönlendirme sahip bir menüyü menü girişlerini üzerinde görünmesini sağlayacak şekilde içerdiği (veya bunun yerine: altında) `dropShadow` paneli):</span><span class="sxs-lookup"><span data-stu-id="98709-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="98709-118">Ardından, `DropShadowExtender` genişletmek için eklenen `panelShadow` panel gölge etkisi ile:</span><span class="sxs-lookup"><span data-stu-id="98709-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="98709-119">Son olarak, ASP.NET AJAX `ScriptManager` denetimi çalışmak Denetim Araç Seti sağlar:</span><span class="sxs-lookup"><span data-stu-id="98709-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="98709-120">Bu komut dosyasını çalıştırdığınızda, menü girişlerini bölmenin altında görünür.</span><span class="sxs-lookup"><span data-stu-id="98709-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="98709-121">Ancak menü CSS sınıfı kullanır `panel` yalnızca sahip olduğunuz öğeleri diğer panel önünde görünür yapmak için iki şey tanımlamak:</span><span class="sxs-lookup"><span data-stu-id="98709-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="98709-122">Göreli konum</span><span class="sxs-lookup"><span data-stu-id="98709-122">Relative positioning</span></span>
- <span data-ttu-id="98709-123">Bir pozitif z dizinini ayarlama</span><span class="sxs-lookup"><span data-stu-id="98709-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="98709-124">Ardından, `DropShadowExtender` denetimi değil çakışan artık ile menü denetimi.</span><span class="sxs-lookup"><span data-stu-id="98709-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


<span data-ttu-id="98709-125">[![Önce: Menü girdisi görünür değil](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98709-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="98709-126">Sonra: Menü girdisi görünür değil ([tam boyutlu görüntüyü görmek için tıklatın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="98709-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>


<span data-ttu-id="98709-127">[![Sonra: Menü giriş görüntülenir.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="98709-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="98709-128">Sonra: Menü girdisi görünür ([tam boyutlu görüntüyü görmek için tıklatın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="98709-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="98709-129">Next</span><span class="sxs-lookup"><span data-stu-id="98709-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
