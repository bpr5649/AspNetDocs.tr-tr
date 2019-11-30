---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: Sunucu tarafında animasyonları değiştirme (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Animasyonlar de olabilir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575168"
---
# <a name="modifying-animations-from-the-server-side-c"></a><span data-ttu-id="330a6-104">Sunucu tarafı (C#) animasyonlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="330a6-104">Modifying Animations From The Server Side (C#)</span></span>

<span data-ttu-id="330a6-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="330a6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="330a6-106">[Kodu indirin](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="330a6-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span></span>

> <span data-ttu-id="330a6-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="330a6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="330a6-108">Animasyonlar Ayrıca sunucu tarafında değişebilir</span><span class="sxs-lookup"><span data-stu-id="330a6-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="330a6-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="330a6-109">Overview</span></span>

<span data-ttu-id="330a6-110">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="330a6-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="330a6-111">Animasyonlar Ayrıca sunucu tarafında değişebilir</span><span class="sxs-lookup"><span data-stu-id="330a6-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="330a6-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="330a6-112">Steps</span></span>

<span data-ttu-id="330a6-113">Birincisi, sayfaya `ScriptManager` ekleyin; ardından, ASP.NET AJAX kitaplığı yüklenir ve Denetim araç setini kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="330a6-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

<span data-ttu-id="330a6-114">Animasyon, şunun gibi görünen bir metin paneline uygulanır:</span><span class="sxs-lookup"><span data-stu-id="330a6-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

<span data-ttu-id="330a6-115">Panelin ilişkili CSS sınıfında, iyi bir arka plan rengi tanımlayın ve panel için sabit bir genişlik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="330a6-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

<span data-ttu-id="330a6-116">Kodun geri kalanı sunucu tarafında çalışır ve biçimlendirme kullanmaz; Bunun yerine, `AnimationExtender` denetimini oluşturmak için kodu kullanır:</span><span class="sxs-lookup"><span data-stu-id="330a6-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

<span data-ttu-id="330a6-117">Ancak, Denetim araç seti Şu anda bireysel animasyonları oluşturmak için bir API erişimi sağlamıyor.</span><span class="sxs-lookup"><span data-stu-id="330a6-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="330a6-118">Ancak, `AnimationExtender`animasyonları özelliğini, animasyonları bildirimli olarak atarken kullanılan XML işaretlemesini içeren bir dizeye ayarlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="330a6-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="330a6-119">`<Animations>` öğesi içermemesi gereken XML oluşturmak için, .NET Framework XML desteğini veya aşağıdaki kodda olduğu gibi, yalnızca dizeyi sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="330a6-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

<span data-ttu-id="330a6-120">Son olarak, `<form runat="server">` öğesi içindeki geçerli sayfaya `AnimationExtender` denetimini ekleyin, böylece animasyon dahil edildiğinden ve çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="330a6-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

<span data-ttu-id="330a6-121">[![animasyonu, sunucu tarafı C#/vb kodu kullanılarak oluşturulur](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="330a6-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span></span>

<span data-ttu-id="330a6-122">Animasyon, sunucu tarafı C#/vb kodu kullanılarak oluşturulur ([tam boyutlu görüntüyü görüntülemek için tıklayın](modifying-animations-from-the-server-side-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="330a6-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="330a6-123">[Önceki](triggering-an-animation-in-another-control-cs.md)
> [İleri](executing-animations-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="330a6-123">[Previous](triggering-an-animation-in-another-control-cs.md)
[Next](executing-animations-using-client-side-code-cs.md)</span></span>
