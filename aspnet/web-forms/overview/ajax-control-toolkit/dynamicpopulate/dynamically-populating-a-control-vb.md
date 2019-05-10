---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: Bir denetimi (VB) dinamik olarak doldurma | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti DynamicPopulate denetimi web hizmetini (veya sayfa yöntemi) çağırır ve t hedef denetime sonuç değerini doldurur...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 369beea703f84bb787ec132a357f016c2a74e6bd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131218"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="825c0-103">Bir Denetimi Dinamik Olarak Doldurma (VB)</span><span class="sxs-lookup"><span data-stu-id="825c0-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="825c0-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="825c0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="825c0-105">[Kodu indir](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="825c0-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="825c0-106">ASP.NET AJAX Denetim Araç Seti DynamicPopulate denetimi, bir web hizmeti (veya sayfa yöntemi) çağırır ve bir hedef denetimine sayfasında, bir sayfa yenileme olmadan sonuç değerini doldurur.</span><span class="sxs-lookup"><span data-stu-id="825c0-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="825c0-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="825c0-107">Overview</span></span>

<span data-ttu-id="825c0-108">`DynamicPopulate` ASP.NET AJAX Denetim Araç Seti denetiminde bir web hizmeti (veya sayfa yöntemi) çağırır ve bir hedef denetimine sayfasında, bir sayfa yenileme olmadan sonuç değerini doldurur.</span><span class="sxs-lookup"><span data-stu-id="825c0-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="825c0-109">Bu öğretici, bu ayarlama işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="825c0-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="825c0-110">Adımlar</span><span class="sxs-lookup"><span data-stu-id="825c0-110">Steps</span></span>

<span data-ttu-id="825c0-111">İlk olarak bir ASP.NET Web hizmeti çağrılacak yöntemin uygulayan ihtiyacınız `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="825c0-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="825c0-112">Web hizmeti sınıfı gerektirir `ScriptService` içinde tanımlanan öznitelik `Microsoft.Web.Script.Services`; Aksi takdirde, ASP.NET AJAX sırayla tarafından gerekli olan web hizmeti için istemci tarafı JavaScript proxy'si oluşturulamıyor `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="825c0-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="825c0-113">Web yöntemi adı verilen dize türünde bir bağımsız değişken bekler gerekir `contextKey`, bu yana `DynamicPopulate` denetim bağlam bilgilerini tek bir parçası olan her web hizmeti çağrısı gönderir.</span><span class="sxs-lookup"><span data-stu-id="825c0-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="825c0-114">Aşağıdaki web hizmeti tarafından temsil edilen bir biçiminde geçerli tarihi döndürür `contextKey` bağımsız değişkeni:</span><span class="sxs-lookup"><span data-stu-id="825c0-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="825c0-115">Web hizmeti olarak kaydedilir `DynamicPopulate.vb.asmx`.</span><span class="sxs-lookup"><span data-stu-id="825c0-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="825c0-116">Alternatif olarak, uygulayabileceğine `getDate()` yöntemi ile gerçek ASP.NET sayfası içinde bir sayfa yöntemi olarak `DynamicPopulate` denetimi.</span><span class="sxs-lookup"><span data-stu-id="825c0-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="825c0-117">Sonraki adımda, yeni bir ASP.NET dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="825c0-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="825c0-118">Her zaman ilk adımı eklemek için olduğundan `ScriptManager` geçerli sayfadaki ASP.NET AJAX Kitaplığı'nı yüklemek için ve Denetim Araç Seti çalışmasını sağlamak için:</span><span class="sxs-lookup"><span data-stu-id="825c0-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="825c0-119">Ardından, bir etiket denetimi ekleyin (örneğin aynı ada sahip bir HTML denetimini kullanarak veya &lt; `asp:Label`  / &gt; web denetimi), daha sonra gösterir web hizmeti çağrısı sonucunu.</span><span class="sxs-lookup"><span data-stu-id="825c0-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="825c0-120">Bir HTML düğmesi (olarak beri bir geri gönderme sunucuya gerektirmeyen bir HTML denetimini), ardından dinamik popülasyon tetiklemek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="825c0-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="825c0-121">Son olarak, ihtiyacımız `DynamicPopulateExtender` kablo işlemleri için denetim.</span><span class="sxs-lookup"><span data-stu-id="825c0-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="825c0-122">Aşağıdaki öznitelikler ayarlayın (belirgin olanlar dışında `ID` ve `runat` = `"server"`):</span><span class="sxs-lookup"><span data-stu-id="825c0-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="825c0-123">`TargetControlID` web hizmeti çağrısından sonucu yerleştirileceği yeri</span><span class="sxs-lookup"><span data-stu-id="825c0-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="825c0-124">`ServicePath` web hizmetinin yolunu (sayfası yöntemi kullanmak istiyorsanız atla)</span><span class="sxs-lookup"><span data-stu-id="825c0-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="825c0-125">`ServiceMethod` web yöntemi veya sayfası yöntemi adı</span><span class="sxs-lookup"><span data-stu-id="825c0-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="825c0-126">`ContextKey` web hizmetine gönderilmesini bağlam bilgileri.</span><span class="sxs-lookup"><span data-stu-id="825c0-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="825c0-127">`PopulateTriggerControlID` web hizmeti çağrısı tetikleyen öğesi</span><span class="sxs-lookup"><span data-stu-id="825c0-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="825c0-128">`ClearContentsDuringUpdate` web hizmeti çağrısı sırasında hedef öğe boş verilip verilmeyeceğini</span><span class="sxs-lookup"><span data-stu-id="825c0-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="825c0-129">Gördüğünüz gibi denetimi bazı bilgiler gerektirir ancak her şeyi yere koymak oldukça rahatça.</span><span class="sxs-lookup"><span data-stu-id="825c0-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="825c0-130">İçin biçimlendirme şöyledir `DynamicPopulateExtender` denetimi Geçerli senaryoda:</span><span class="sxs-lookup"><span data-stu-id="825c0-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="825c0-131">ASP.NET sayfasını tarayıcıda çalıştırın ve düğmesine tıklayın. ay gün yıl biçiminde geçerli tarihi alır.</span><span class="sxs-lookup"><span data-stu-id="825c0-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="825c0-132">[![Düğmenin click sunucudan tarihi alır.](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="825c0-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="825c0-133">Düğmenin click sunucudan tarihi alır ([tam boyutlu görüntüyü görmek için tıklatın](dynamically-populating-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="825c0-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="825c0-134">[Önceki](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [İleri](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="825c0-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
