---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: (VB) UpdatePanel olmadan bir açılan denetimden gelen geri göndermeleri işleme | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Su içinde bir geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: c46f00c42f9b06d0224bcae03f51be8a73099974
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409349"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="72398-104">UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (VB)</span><span class="sxs-lookup"><span data-stu-id="72398-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="72398-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="72398-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="72398-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="72398-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="72398-107">AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="72398-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="72398-108">Bu panelde bir geri gönderme gerçekleşir ve sayfada birkaç panelleri olduğunda hangi panele tıkladı belirlemek zordur.</span><span class="sxs-lookup"><span data-stu-id="72398-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="72398-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="72398-109">Overview</span></span>

<span data-ttu-id="72398-110">AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="72398-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="72398-111">Bu panelde bir geri gönderme gerçekleşir ve sayfada birkaç panelleri olduğunda hangi panele tıkladı belirlemek zordur.</span><span class="sxs-lookup"><span data-stu-id="72398-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="72398-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="72398-112">Steps</span></span>

<span data-ttu-id="72398-113">Kullanırken bir `PopupControl` bir geri gönderme, ancak sahip olmayan bir `UpdatePanel` sayfasında Denetim Araç Seti, hangi istemci öğesi sırayla geri göndermenin neden açılan tetiklediğini belirlemek için bir yol sunmaz.</span><span class="sxs-lookup"><span data-stu-id="72398-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="72398-114">Ancak küçük ipucunu bu senaryo için geçici bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="72398-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="72398-115">İlk olarak, temel kurulum şöyledir: her iki aynı açılan, bir Takvim tetikleyicisi iki metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="72398-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="72398-116">İki `PopupControlExtenders` metin kutularını ve açılan bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="72398-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="72398-117">Gizli form alanına eklemek için temel fikirdir &lt; `form` &gt; başlatılan açılan metin kutusuna tutan öğesi:</span><span class="sxs-lookup"><span data-stu-id="72398-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="72398-118">Sayfa yüklendiğinde, JavaScript kodu için iki metin kutusuna bir olay işleyicisi ekler: Kullanıcı bir metin kutusunda tıkladığında, adını gizli form alanına yazılır:</span><span class="sxs-lookup"><span data-stu-id="72398-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="72398-119">Sunucu tarafı kodunda gizli alan değerini okunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72398-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="72398-120">Gizli form alanları değiştirmek için Önemsiz olduğundan, gizli değeri doğrulamak için bir beyaz liste yaklaşım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="72398-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="72398-121">Doğru metin kutusunu belirlendikten sonra takvimden tarihi üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="72398-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


[![T<span data-ttu-id="72398-122">Kullanıcı, metin kutusuna tıkladığında kendisinin Takvim görünür]</span><span class="sxs-lookup"><span data-stu-id="72398-122">he Calendar appears when the user clicks into the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

<span data-ttu-id="72398-123">Takvim kullanıcı TextBox'a tıkladığında görünür ([tam boyutlu görüntüyü görmek için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="72398-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>


[![C<span data-ttu-id="72398-124">bir tarihte licking metin kutusunda koyar]</span><span class="sxs-lookup"><span data-stu-id="72398-124">licking on a date puts it in the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

<span data-ttu-id="72398-125">Bir tarihte tıklayarak onu koyar metin kutusu içinde ([tam boyutlu görüntüyü görmek için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="72398-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="72398-126">Önceki</span><span class="sxs-lookup"><span data-stu-id="72398-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
