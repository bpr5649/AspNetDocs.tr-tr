---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Eylem (VB) oluşturma | Microsoft Docs
author: microsoft
description: ASP.NET MVC denetleyicisi için yeni bir eylem eklemeyi öğrenin. Bir eylem için bir yöntem gereksinimleri hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123445"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="9d248-104">Eylem Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="9d248-104">Creating an Action (VB)</span></span>

<span data-ttu-id="9d248-105">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9d248-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9d248-106">ASP.NET MVC denetleyicisi için yeni bir eylem eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9d248-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="9d248-107">Bir eylem için bir yöntem gereksinimleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9d248-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="9d248-108">Bu öğreticinin amacı, yeni bir denetleyici eylemi nasıl oluşturacağınızı açıklar sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="9d248-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="9d248-109">Bir eylem yönteminin gereksinimleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9d248-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="9d248-110">Ayrıca bir yöntem bir eylem olarak açıklanmasını önlemenize öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9d248-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="9d248-111">Denetleyici için eylem ekleme</span><span class="sxs-lookup"><span data-stu-id="9d248-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="9d248-112">Bir denetleyici için yeni bir yöntem denetleyiciye ekleyerek yeni bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9d248-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="9d248-113">Örneğin, denetleyici 1 listeleme İNDİS() adlı bir eylem ve SayHello() adlı bir eylem içerir.</span><span class="sxs-lookup"><span data-stu-id="9d248-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="9d248-114">Her iki yöntem de eylem olarak kullanıma sunulur.</span><span class="sxs-lookup"><span data-stu-id="9d248-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="9d248-115">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="9d248-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="9d248-116">Bir eylem olarak evreni maruz kalabilir için bir yöntem belirli gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="9d248-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="9d248-117">Yöntemi, ortak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9d248-117">The method must be public.</span></span>
- <span data-ttu-id="9d248-118">Yöntem statik bir yöntemi olamaz.</span><span class="sxs-lookup"><span data-stu-id="9d248-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="9d248-119">Yöntemin bir genişletme yöntemi olamaz.</span><span class="sxs-lookup"><span data-stu-id="9d248-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="9d248-120">Bir oluşturucu, alıcı veya ayarlayıcı yöntemi olamaz.</span><span class="sxs-lookup"><span data-stu-id="9d248-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="9d248-121">Yöntemi, açık genel türler sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="9d248-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="9d248-122">Yöntemi denetleyici temel sınıfın bir yöntem değil.</span><span class="sxs-lookup"><span data-stu-id="9d248-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="9d248-123">Bir yöntemi içeremez **ref** veya **kullanıma** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="9d248-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="9d248-124">Bir denetleyici eylemi dönüş türüne hiçbir kısıtlama olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9d248-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="9d248-125">Bir denetleyici eylemi bir dize bir DateTime Random sınıfını veya void örneği döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="9d248-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="9d248-126">ASP.NET MVC çerçevesi bir eylem sonucu bir dizeye değil herhangi bir dönüş türü dönüştürmek ve tarayıcıya dize işleme.</span><span class="sxs-lookup"><span data-stu-id="9d248-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="9d248-127">Bu gereksinimleri denetleyicisi ihlal etmemesini herhangi bir yöntemi eklediğinizde, yöntem bir denetleyici eylemi kullanıma sunulur.</span><span class="sxs-lookup"><span data-stu-id="9d248-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="9d248-128">Burada dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="9d248-128">Be careful here.</span></span> <span data-ttu-id="9d248-129">Bir denetleyici eylemi, Internet'e bağlı herhangi bir kişi tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d248-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="9d248-130">Örneğin, bir DeleteMyWebsite() denetleyici eylemi oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="9d248-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="9d248-131">Genel bir yöntem çağrılmakta olan önleme</span><span class="sxs-lookup"><span data-stu-id="9d248-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="9d248-132">Genel bir yöntem bir controller sınıfında oluşturmanız gerekir ve yöntemi bir denetleyici eylemi olarak göstermek istemediğiniz sonra yöntemi kullanarak çağrılmasını engelleyebilir &lt;NonAction&gt; özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9d248-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="9d248-133">Örneğin, denetleyici listeleme 2 ile donatılmış CompanySecrets() adlı bir genel yöntem içerir &lt;NonAction&gt; özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9d248-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="9d248-134">**Listing 2 - Controllers\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="9d248-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="9d248-135">Tarayıcınızın adres çubuğuna /Work/CompanySecrets yazarak CompanySecrets() denetleyici eylemini çağırma denerseniz, Şekil 1'de hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9d248-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="9d248-136">[![NonAction yöntemi çağırma](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9d248-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="9d248-137">**Şekil 01**: NonAction yöntemi çağırma ([tam boyutlu görüntüyü görmek için tıklatın](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9d248-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d248-138">[Önceki](creating-a-controller-vb.md)
> [İleri](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9d248-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
