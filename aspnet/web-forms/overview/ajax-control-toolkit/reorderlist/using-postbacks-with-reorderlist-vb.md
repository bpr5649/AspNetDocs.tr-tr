---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: (VB) ReorderList ile geri gönderme kullanma | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listeyi yeniden her bir SAS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 1e2124327a36c94db8bafbdf91f767068ac7e834
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066243"
---
<a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="f71b2-104">ReorderList ile Geri Gönderme Kullanma (VB)</span><span class="sxs-lookup"><span data-stu-id="f71b2-104">Using Postbacks with ReorderList (VB)</span></span>
====================
<span data-ttu-id="f71b2-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f71b2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f71b2-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f71b2-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="f71b2-107">AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="f71b2-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f71b2-108">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="f71b2-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="f71b2-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f71b2-109">Overview</span></span>

<span data-ttu-id="f71b2-110">`ReorderList` AJAX Denetim Araç Seti denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="f71b2-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f71b2-111">Listeyi yeniden olduğunda, bir geri gönderme sunucunun değişikliği bildirmek.</span><span class="sxs-lookup"><span data-stu-id="f71b2-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="f71b2-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="f71b2-112">Steps</span></span>

<span data-ttu-id="f71b2-113">Birkaç olası veri kaynağı için `ReorderList` denetimi.</span><span class="sxs-lookup"><span data-stu-id="f71b2-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="f71b2-114">Biridir kullanmak için bir `XmlDataSource` denetimi:</span><span class="sxs-lookup"><span data-stu-id="f71b2-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="f71b2-115">Bu XML bağlamak amacıyla bir `ReorderList` denetimi ve etkinleştirme Geri göndermeler, aşağıdaki öznitelikleri ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="f71b2-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="f71b2-116">`DataSourceID`: Veri kaynağı kimliği</span><span class="sxs-lookup"><span data-stu-id="f71b2-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="f71b2-117">`SortOrderField`: Sıralama ölçütü olarak özelliği</span><span class="sxs-lookup"><span data-stu-id="f71b2-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="f71b2-118">`AllowReorder`: Liste öğeleri yeniden sıralamak kullanıcı izin verilip verilmeyeceğini</span><span class="sxs-lookup"><span data-stu-id="f71b2-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="f71b2-119">`PostBackOnReorder`: Listenin düzenlenmeyecek her bir geri gönderme oluşturulup oluşturulmayacağını</span><span class="sxs-lookup"><span data-stu-id="f71b2-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="f71b2-120">Denetim için uygun biçimlendirmesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f71b2-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="f71b2-121">İçinde `ReorderList` denetimi, veri kaynağındaki belirli veri bağımlı kullanarak `Eval()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="f71b2-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="f71b2-122">Son yeniden sıralama oluştuğunda rastgele bir konumda sayfasında, bilgileri bir etiket tutar:</span><span class="sxs-lookup"><span data-stu-id="f71b2-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="f71b2-123">Bu etiket, metin işleme geri gönderme sunucu tarafı kodu ile doldurulur:</span><span class="sxs-lookup"><span data-stu-id="f71b2-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="f71b2-124">Son olarak, ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` sayfada denetim yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="f71b2-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


<span data-ttu-id="f71b2-125">[![Bir geri gönderme tetikleyen her yeniden sıralama](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f71b2-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="f71b2-126">Bir geri gönderme her sipariş tetikler ([tam boyutlu görüntüyü görmek için tıklatın](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f71b2-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f71b2-127">[Önceki](drag-and-drop-via-reorderlist-cs.md)
> [İleri](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f71b2-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
