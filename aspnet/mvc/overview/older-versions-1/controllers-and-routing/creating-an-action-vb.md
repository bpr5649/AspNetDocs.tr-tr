---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Eylem Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin. Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542254"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="20815-104">Eylem Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="20815-104">Creating an Action (VB)</span></span>

<span data-ttu-id="20815-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="20815-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="20815-106">ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="20815-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="20815-107">Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="20815-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="20815-108">Bu öğreticinin amacı, yeni bir denetleyici eylemi nasıl oluşturabileceğinizi açıklamaktır.</span><span class="sxs-lookup"><span data-stu-id="20815-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="20815-109">Bir eylem yönteminin gereksinimleri hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20815-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="20815-110">Ayrıca, bir yöntemin bir eylem olarak açığa çıkarMasını nasıl önleyeceğinizi de öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20815-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="20815-111">Denetleyiciye Eylem Ekleme</span><span class="sxs-lookup"><span data-stu-id="20815-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="20815-112">Denetleyiciye yeni bir yöntem ekleyerek denetleyiciye yeni bir eylem eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="20815-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="20815-113">Örneğin, Listeleme 1'deki denetleyici, Index() adlı bir eylem ve SayHello() adlı bir eylem içerir.</span><span class="sxs-lookup"><span data-stu-id="20815-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="20815-114">Her iki yöntem de eylem olarak ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="20815-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="20815-115">**Listeleme 1 - Denetleyiciler\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="20815-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="20815-116">Bir eylem olarak evrene maruz kalmak için, bir yöntem belirli gereksinimleri karşılamak gerekir:</span><span class="sxs-lookup"><span data-stu-id="20815-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="20815-117">Yöntem herkese açık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20815-117">The method must be public.</span></span>
- <span data-ttu-id="20815-118">Yöntem statik bir yöntem olamaz.</span><span class="sxs-lookup"><span data-stu-id="20815-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="20815-119">Yöntem bir uzantı yöntemi olamaz.</span><span class="sxs-lookup"><span data-stu-id="20815-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="20815-120">Yöntem bir oluşturucu, getter veya ayarlayıcı olamaz.</span><span class="sxs-lookup"><span data-stu-id="20815-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="20815-121">Yöntem, açık genel türleri olamaz.</span><span class="sxs-lookup"><span data-stu-id="20815-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="20815-122">Yöntem denetleyici taban sınıfının bir yöntemi değildir.</span><span class="sxs-lookup"><span data-stu-id="20815-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="20815-123">Yöntem **ref** veya **çıkış** parametreleri içeremez.</span><span class="sxs-lookup"><span data-stu-id="20815-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="20815-124">Denetleyici eyleminin dönüş türünde herhangi bir kısıtlama bulunmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="20815-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="20815-125">Denetleyici eylem bir dize, DateTime, Rasgele sınıfın bir örneği veya geçersiz döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="20815-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="20815-126">ASP.NET MVC çerçevesi, eylem sonucu olmayan herhangi bir iade türünü bir dize ye dönüştürür ve dizeyi tarayıcıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="20815-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="20815-127">Denetleyiciye bu gereksinimleri ihlal etmeyen herhangi bir yöntem eklediğinizde, yöntem denetleyici eylemi olarak ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="20815-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="20815-128">Burada dikkatli ol.</span><span class="sxs-lookup"><span data-stu-id="20815-128">Be careful here.</span></span> <span data-ttu-id="20815-129">Denetleyici eylemi, Internet'e bağlı herkes tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="20815-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="20815-130">Örneğin, bir DeleteMyWebsite() denetleyici eylemi oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="20815-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="20815-131">Genel Yöntemin Çağrılmasını Önleme</span><span class="sxs-lookup"><span data-stu-id="20815-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="20815-132">Denetleyici sınıfında ortak bir yöntem oluşturmanız gerekiyorsa ve yöntemi denetleyici eylemi olarak ortaya çıkarmak istemiyorsanız, yöntemin &lt;Eylem&gt; Dışı özniteliğini kullanarak çağrılmasını engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20815-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="20815-133">Örneğin, Listeleme 2'deki denetleyici, Eylem &lt;&gt; Dışı özniteliğiyle dekore edilmiş CompanySecrets() adlı genel bir yöntem içerir.</span><span class="sxs-lookup"><span data-stu-id="20815-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="20815-134">**Listeleme 2 - Denetleyiciler\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="20815-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="20815-135">/Work/CompanySecrets yazıp /İş/ŞirketSırları'nı tarayıcınızın adres çubuğuna yazarak CompanySecrets() denetleyici eylemini çağırmaya çalışırsanız, hata iletisini Şekil 1'de alırsınız.</span><span class="sxs-lookup"><span data-stu-id="20815-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="20815-136">[![Eylemsizlik yöntemini çağırmak](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="20815-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="20815-137">**Şekil 01**: Eylemsizlik yöntemini çağırmak([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="20815-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20815-138">[Önceki](creating-a-controller-vb.md)
> [Sonraki](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="20815-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
