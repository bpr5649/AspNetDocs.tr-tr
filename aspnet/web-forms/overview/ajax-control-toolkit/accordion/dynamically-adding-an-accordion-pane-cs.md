---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Dinamik olarak Accordion bölmesi bir (C#) ekleme | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir. Paneller genellikle w bildirilen...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: ea526ce8abdf6f7013e8dd832824c21448878e0b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416850"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="38098-104">Dinamik olarak Accordion bölmesi bir (C#) ekleme</span><span class="sxs-lookup"><span data-stu-id="38098-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="38098-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="38098-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="38098-106">[Kodu indir](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="38098-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="38098-107">AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir.</span><span class="sxs-lookup"><span data-stu-id="38098-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="38098-108">Paneller genellikle sayfa içinde bildirilen, ancak sunucu tarafı kod aynı sonucu elde etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38098-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="38098-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="38098-109">Overview</span></span>

<span data-ttu-id="38098-110">AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir.</span><span class="sxs-lookup"><span data-stu-id="38098-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="38098-111">Paneller genellikle sayfa içinde bildirilen, ancak sunucu tarafı kod aynı sonucu elde etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38098-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="38098-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="38098-112">Steps</span></span>

<span data-ttu-id="38098-113">Accordion denetimi, sunucu tarafı kodu tüm önemli özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="38098-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="38098-114">Başka şeylerin yanında `Panes` özelliği Accordion olun bölmelerin koleksiyonunu erişim verir.</span><span class="sxs-lookup"><span data-stu-id="38098-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="38098-115">Türü her bölmesinde `AccordionPane`.</span><span class="sxs-lookup"><span data-stu-id="38098-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="38098-116">Bu nedenle, böyle bir bölme oluşturmak için Önemsiz:</span><span class="sxs-lookup"><span data-stu-id="38098-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="38098-117">`HeaderContainer` Özelliği `AccordionPane` ; bölmesinin üst bilgisi bölümü içinde ASP.NET denetimleri için erişim sağlayan `ContentContainer` özelliği `AccordionPane` bölmesinin içerik bölümü için aynı yapar.</span><span class="sxs-lookup"><span data-stu-id="38098-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="38098-118">Bu içeriği bölmelerini eklemek ASP.NET kodu sağlar:</span><span class="sxs-lookup"><span data-stu-id="38098-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="38098-119">Son olarak, pane(s) eklenmeli `Panes` Accordion koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="38098-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="38098-120">İki bölme için bir Accordion denetimi ekler tam bir sunucu tarafı kod şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="38098-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="38098-121">Tek eksik öğe ASP.NET varlığını temel bağımlı Accordion kendisi ise `ScriptManager` denetimi:</span><span class="sxs-lookup"><span data-stu-id="38098-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="38098-122">Örneği tamamlamak için tarayıcı için stil bilgilerini Accordion denetimi başvurulan iki CSS sınıfları sağlar:</span><span class="sxs-lookup"><span data-stu-id="38098-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


[![T<span data-ttu-id="38098-123">He bir accordion'a veri, sunucu tarafı kodu tarafından dinamik olarak eklendi]</span><span class="sxs-lookup"><span data-stu-id="38098-123">he data in the accordion was dynamically added by server-side code]</span></span>(dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

<span data-ttu-id="38098-124">Sunucu tarafı kodu tarafından dinamik olarak accordion verileri eklendikten sonra ([tam boyutlu görüntüyü görmek için tıklatın](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="38098-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38098-125">[Önceki](databinding-to-an-accordion-cs.md)
> [İleri](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="38098-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
