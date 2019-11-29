---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel animasyonlarını dinamik olarak denetleme (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir. Bir... öğesinin içeriği için
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 97a52bd75fdf63ad62282afd9df772f0a9e4f931
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599711"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="e7970-104">UpdatePanel Animasyonlarını Dinamik Olarak Denetleme (VB)</span><span class="sxs-lookup"><span data-stu-id="e7970-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="e7970-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="e7970-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e7970-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e7970-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="e7970-107">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="e7970-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e7970-108">Bir UpdatePanel 'ın içeriği için animasyon çerçevesinde yoğun bir şekilde yararlanan özel bir genişletici vardır: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="e7970-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="e7970-109">Ayrıca, UpdatePanel tetikleyicilerle birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="e7970-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="e7970-110">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e7970-110">Overview</span></span>

<span data-ttu-id="e7970-111">ASP.NET AJAX denetim araç setinde animasyon denetimi yalnızca bir denetim değildir ancak bir denetime animasyon eklemek için bir bütün çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="e7970-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e7970-112">Bir `UpdatePanel`içeriği için animasyon çerçevesine yoğun bir şekilde dayanan özel bir genişletici vardır: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="e7970-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="e7970-113">Ayrıca, `UpdatePanel` tetikleyicilerle birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="e7970-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="e7970-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="e7970-114">Steps</span></span>

<span data-ttu-id="e7970-115">İlk adım, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için sayfaya `ScriptManager` dahil etmek için her zamanki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e7970-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="e7970-116">Bu senaryodaki animasyon geçerli saatin görüntüsüne uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e7970-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="e7970-117">Bu bilgiler `Page_Load()` yöntemi kullanılarak bir etikete yazılabilir veya (basitlik sağlamak için) aşağıdaki satır içi kod kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e7970-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="e7970-118">Ayrıca, zaman güncellemenin tetiklenmesi için bir düğme oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="e7970-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="e7970-119">Bu kod daha sonra bir `UpdatePanel` öğesinin `<ContentTemplate>` bölümüne konur.</span><span class="sxs-lookup"><span data-stu-id="e7970-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="e7970-120">Panelin `UpdateMode` özniteliği `"Conditional"`olarak ayarlanmalıdır, çünkü yalnızca Tetikleyiciler panelin içeriğini güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="e7970-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="e7970-121">`UpdatePanel``<Triggers>` bölümünde, zaman uyumsuz bir geri gönderme tetikleyicisi oluşturulur ve düğmenin `Click` olayına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e7970-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="e7970-122">Bu nedenle, Kullanıcı düğmeye tıkladığında `UpdatePanel` yenilenir.</span><span class="sxs-lookup"><span data-stu-id="e7970-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="e7970-123">`UpdatePanel` denetimi için biçimlendirme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e7970-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="e7970-124">Son olarak, `UpdatePanelAnimationExtender` yapılandırılması gerekir: `TargetControlID` özniteliğini panelin KIMLIĞI olarak ayarlayın ve Extender içinde bir animasyon tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e7970-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="e7970-125">' Deki soldurma, güncelleştirilmiş sürede iyi bir görsel vurgu oluşturan anlamda anlamlı hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e7970-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="e7970-126">Daha sonra genişletici biçimlerinizin şöyle görünebiliriz:</span><span class="sxs-lookup"><span data-stu-id="e7970-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="e7970-127">Dosyayı tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7970-127">Run the file in the browser.</span></span> <span data-ttu-id="e7970-128">Düğmeye tıkladığınızda, geçerli saat panelde gösterilir, her zaman bir saniye boyunca geçişi yapılır.</span><span class="sxs-lookup"><span data-stu-id="e7970-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="e7970-129">[geçerli zaman ![](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e7970-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="e7970-130">Şu anki Saat Soldurma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e7970-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e7970-131">Öncekini</span><span class="sxs-lookup"><span data-stu-id="e7970-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
