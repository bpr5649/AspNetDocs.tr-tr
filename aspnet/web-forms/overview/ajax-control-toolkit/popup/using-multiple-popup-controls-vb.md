---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Birden çok açılan denetim (VB) kullanarak | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. M kullanmak da mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 81b0dbd794d31bc3c55bff4ba8110c590b88b509
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073632"
---
<a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="50231-104">Birden Çok Açılan Denetim Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="50231-104">Using Multiple Popup Controls (VB)</span></span>
====================
<span data-ttu-id="50231-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="50231-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="50231-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="50231-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="50231-107">AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="50231-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="50231-108">Tek bir sayfada birden çok açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="50231-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="50231-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="50231-109">Overview</span></span>

<span data-ttu-id="50231-110">AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="50231-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="50231-111">Tek bir sayfada birden çok açılan denetim kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="50231-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="50231-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="50231-112">Steps</span></span>

<span data-ttu-id="50231-113">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="50231-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="50231-114">Ardından, açılan menüsü hizmet veren bir panel ekleme.</span><span class="sxs-lookup"><span data-stu-id="50231-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="50231-115">Geçerli senaryosunda, panele içeren bir `Calendar` denetimi.</span><span class="sxs-lookup"><span data-stu-id="50231-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="50231-116">Takvimin Geri göndermeler tarafından neden sayfa yenilenir önlemek için panel içinde konur bir `UpdatePanel` denetimi:</span><span class="sxs-lookup"><span data-stu-id="50231-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="50231-117">Sayfa, iki metin kutuları da içerir.</span><span class="sxs-lookup"><span data-stu-id="50231-117">The page also contains two text boxes.</span></span> <span data-ttu-id="50231-118">Metin kutusu etkinleştirildikten sonra her bir metin kutusu için Takvim açılır görünmesi gereken.</span><span class="sxs-lookup"><span data-stu-id="50231-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="50231-119">Her iki metin kutuları artık genişleten bir `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="50231-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="50231-120">`TargetControlID` Öznitelik kimliği için genişletici bağlı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="50231-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="50231-121">`PopupControlID` Özniteliği açılır paneli Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="50231-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="50231-122">Bu durumda, her iki Genişleticileri aynı paneli gösterir, ancak farklı panellerin yanı olasılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="50231-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="50231-123">Artık bir metin alanı içinde tıklattığınızda, bir takvim tarihi seçmenize olanak sağlar alanının altında görünür.</span><span class="sxs-lookup"><span data-stu-id="50231-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="50231-124">(Seçilen tarihten metin kutularına geri alamazsınız. farklı bir öğreticide ele alınacaktır.)</span><span class="sxs-lookup"><span data-stu-id="50231-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="50231-125">[![Takvim kullanıcı TextBox'a tıkladığında görünür](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="50231-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="50231-126">Takvim kullanıcı TextBox'a tıkladığında görünür ([tam boyutlu görüntüyü görmek için tıklatın](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="50231-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50231-127">[Önceki](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [İleri](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="50231-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>