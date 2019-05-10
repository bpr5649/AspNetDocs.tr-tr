---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Kaydırıcı denetimi otomatik geri gönderme ile (C#) kullanma | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti kaydırıcı denetimi fareyle denetlenebilir bir grafik kaydırıcı sağlar. Kaydırıcı autopost yapmak mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b1e7c2e62438876343987917ffc8f792c755186
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124630"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="f5275-104">Kaydırıcı denetimi otomatik geri gönderme ile (C#) kullanma</span><span class="sxs-lookup"><span data-stu-id="f5275-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="f5275-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f5275-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f5275-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5275-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="f5275-107">AJAX Denetim Araç Seti kaydırıcı denetimi fareyle denetlenebilir bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5275-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="f5275-108">Kaydırıcı autopostback değeri değiştiğinde bir kez yapmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f5275-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="f5275-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f5275-109">Overview</span></span>

<span data-ttu-id="f5275-110">AJAX Denetim Araç Seti kaydırıcı denetimi fareyle denetlenebilir bir grafik kaydırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5275-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="f5275-111">Kaydırıcı autopostback değeri değiştiğinde bir kez yapmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f5275-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="f5275-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="f5275-112">Steps</span></span>

<span data-ttu-id="f5275-113">Kaydırıcı otomatik olarak geri gönderme sırasında bir değişiklik yapmak için iki metin kutusuna öznitelik gerekiyor `AutoPostBack="true"`: Kaydırıcı olacak metin kutusu ve kaydırıcının konumunu içeren metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f5275-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="f5275-114">Söz konusu gerekli biçimlendirmesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f5275-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="f5275-115">`SliderExtender` ASP.NET AJAX Denetim Araç Seti denetiminden iki metin kutuları kaydırıcı işlevi atar:</span><span class="sxs-lookup"><span data-stu-id="f5275-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="f5275-116">Bir ek label öğesini, daha sonra bir geri gönderme kullanıcıya bildirmek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="f5275-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="f5275-117">Son olarak, `ScriptManager` Denetim ASP.NET AJAX Denetim Araç Seti çalışması için gerekli JavaScript yükler:</span><span class="sxs-lookup"><span data-stu-id="f5275-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="f5275-118">Kaydırıcı geri gönderen artık; Sunucu tarafında bu olay yakalandı ve izlemede:</span><span class="sxs-lookup"><span data-stu-id="f5275-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="f5275-119">[![Bir geri gönderme kaydırıcıyı hareket tetikler](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f5275-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="f5275-120">Kaydırıcıyı hareket, bir geri gönderme tetikler ([tam boyutlu görüntüyü görmek için tıklatın](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f5275-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="f5275-121">[![Daha sonra bu değişiklik tarihini etikette yazılır](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f5275-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="f5275-122">Daha sonra bu değişiklik tarihini etikette yazılır ([tam boyutlu görüntüyü görmek için tıklatın](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f5275-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f5275-123">Next</span><span class="sxs-lookup"><span data-stu-id="f5275-123">Next</span></span>](databinding-the-slider-control-cs.md)
