---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Sunucu kodundan (C#) kalıcı bir açılan pencere başlatılıyor | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar. Ancak bazı senaryolar bu t... gerektirir.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599065"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="3add1-104">Sunucu Kodundan Kalıcı Açılan Pencere Başlatma (C#)</span><span class="sxs-lookup"><span data-stu-id="3add1-104">Launching a Modal Popup Window from Server Code (C#)</span></span>

<span data-ttu-id="3add1-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="3add1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3add1-106">[Kodu indirin](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3add1-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="3add1-107">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="3add1-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="3add1-108">Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3add1-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="3add1-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="3add1-109">Overview</span></span>

<span data-ttu-id="3add1-110">AJAX denetim araç setinde ModalPopup denetimi, istemci tarafı anlamını kullanarak kalıcı bir açılan pencere oluşturmanın basit bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="3add1-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="3add1-111">Ancak bazı senaryolar, sunucu tarafında kalıcı açılan pencerenin açılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3add1-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="3add1-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="3add1-112">Steps</span></span>

<span data-ttu-id="3add1-113">Birincisi, ModalPopup denetiminin nasıl çalıştığını göstermek için bir ASP.NET Button Web denetimi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3add1-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="3add1-114">Yeni bir sayfada &lt;form&gt; öğesi içinde böyle bir düğme ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3add1-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="3add1-115">Ardından, oluşturmak istediğiniz açılan pencere için biçimlendirmenin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3add1-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="3add1-116">Bunu bir `<asp:Panel>` denetimi olarak tanımlayın ve bir düğme denetimi içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3add1-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="3add1-117">ModalPopup denetimi, bu tür bir düğmeyi açılan pencereyi kapatacak şekilde işlevleri sunar; Aksi takdirde, bir yol açmanın kolay bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="3add1-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="3add1-118">Daha sonra, ASP.NET AJAX araç kümesinden ModalPopup denetimini sayfaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3add1-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="3add1-119">Denetimi yükleyen düğme için özellikleri, ortadan kaldırdıkları düğmeyi ve gerçek açılan pencerenin KIMLIĞINI ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3add1-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="3add1-120">ASP.NET AJAX 'ı temel alan tüm Web sayfalarında olduğu gibi Komut dosyası Yöneticisi, farklı hedef tarayıcılar için gerekli JavaScript kitaplıklarını yüklemek üzere gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3add1-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="3add1-121">Örneği tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3add1-121">Run the example in the browser.</span></span> <span data-ttu-id="3add1-122">Düğmeye tıkladığınızda, kalıcı açılan pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="3add1-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="3add1-123">Sunucu tarafı kod kullanarak aynı etkiye ulaşmak için yeni bir düğme gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3add1-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="3add1-124">Gördüğünüz gibi, düğmesine bir tıklama geri gönderme oluşturur ve `ServerButton_Click()` yöntemi sunucuda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3add1-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="3add1-125">Bu yöntemde `launchModal()` adlı bir JavaScript işlevi, sayfa yüklendikten sonra JavaScript işlevi yürütülür:</span><span class="sxs-lookup"><span data-stu-id="3add1-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="3add1-126">`launchModal()` işi ModalPopup görüntülemektir.</span><span class="sxs-lookup"><span data-stu-id="3add1-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="3add1-127">Tüm HTML sayfası yüklendikten sonra `launchModal()` işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3add1-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="3add1-128">Ancak, ASP.NET AJAX Framework henüz tam olarak yüklenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="3add1-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="3add1-129">Bu nedenle, `launchModal()` işlevi yalnızca ModalPopup denetiminin daha sonra gösterilmesi gereken bir değişken ayarlar:</span><span class="sxs-lookup"><span data-stu-id="3add1-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="3add1-130">`pageLoad()` JavaScript işlevi, ASP.NET AJAX tam olarak yüklendikten sonra yürütülen özel bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="3add1-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="3add1-131">Bu nedenle, ModalPopup denetimini göstermek için bu işleve kod ekleyeceğiz, ancak yalnızca `launchModal()` daha önce çağrılırsa:</span><span class="sxs-lookup"><span data-stu-id="3add1-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="3add1-132">`$find()` işlevi sayfada adlandırılmış bir öğe arıyor ve sunucu tarafı KIMLIĞINI parametre olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="3add1-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="3add1-133">Bu nedenle, `$find("mpe")` ModalPopup denetiminin istemci temsilini döndürür; `show()` yöntemi, açılan pencerenin görünmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="3add1-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="3add1-134">[düğme tıklandığında kalıcı açılan pencere ![görünür](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3add1-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="3add1-135">Düğme tıklandığında kalıcı açılan pencere görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3add1-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3add1-136">Next</span><span class="sxs-lookup"><span data-stu-id="3add1-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
