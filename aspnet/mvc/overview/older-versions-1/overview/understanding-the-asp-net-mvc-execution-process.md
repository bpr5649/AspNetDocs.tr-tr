---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: MVC Yürütme Sürecinin ASP.NET Anlaşılması | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET MVC çerçevesinin tarayıcı isteğini adım adım nasıl işlediğini öğrenin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541032"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="5b625-103">ASP.NET MVC Yürütme İşlemini Anlama</span><span class="sxs-lookup"><span data-stu-id="5b625-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="5b625-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="5b625-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5b625-105">ASP.NET MVC çerçevesinin tarayıcı isteğini adım adım nasıl işlediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5b625-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="5b625-106">MVC tabanlı bir web uygulaması ASP.NETna yapılan istekler ilk olarak bir HTTP modülü olan **UrlRoutingModule** nesnesi üzerinden geçer.</span><span class="sxs-lookup"><span data-stu-id="5b625-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="5b625-107">Bu modül isteği ayrışdırır ve rota seçimini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5b625-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="5b625-108">**UrlRoutingModule** nesnesi geçerli istekle eşleşen ilk rota nesnesini seçer.</span><span class="sxs-lookup"><span data-stu-id="5b625-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="5b625-109">(Rota nesnesi, **RouteBase'i**uygulayan bir sınıftır ve genellikle **Rota** sınıfının bir örneğidir.) Hiçbir rota eşleşmiyorsa, **UrlRoutingModule** nesnesi hiçbir şey yapmaz ve isteğin normal ASP.NET veya IIS istek işlemesine geri dönmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b625-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="5b625-110">**UrlRoutingModule** nesnesi, seçili **Rota** nesnesinden, **Rota** nesnesiyle ilişkili **IRouteHandler** nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="5b625-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="5b625-111">Genellikle, bir MVC uygulamasında, bu **MvcRouteHandler**bir örneği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5b625-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="5b625-112">**IRouteHandler** örneği bir **IHttpHandler** nesnesi oluşturur ve **ihttpcontext** nesnesini geçirir.</span><span class="sxs-lookup"><span data-stu-id="5b625-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="5b625-113">Varsayılan olarak, MVC için **IHttpHandler** örneği **MvcHandler** nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="5b625-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="5b625-114">**MvcHandler** nesnesi daha sonra isteği sonunda işleyecek denetleyiciyi seçer.</span><span class="sxs-lookup"><span data-stu-id="5b625-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="5b625-115">Bir ASP.NET MVC Web uygulaması IIS 7.0'da çalıştığında, MVC projeleri için dosya adı uzantısı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5b625-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="5b625-116">Ancak, IIS 6.0'da işleyici, .mvc dosya adı uzantısını ASP.NET ISAPI DLL ile eşlenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b625-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="5b625-117">Modül ve işleyici, ASP.NET MVC çerçevesinin giriş noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="5b625-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="5b625-118">Aşağıdaki eylemleri gerçekleştirirler:</span><span class="sxs-lookup"><span data-stu-id="5b625-118">They perform the following actions:</span></span>

- <span data-ttu-id="5b625-119">Bir MVC Web uygulamasında uygun denetleyiciyi seçin.</span><span class="sxs-lookup"><span data-stu-id="5b625-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="5b625-120">Belirli bir denetleyici örneği edinin.</span><span class="sxs-lookup"><span data-stu-id="5b625-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="5b625-121">Denetleyicinin Yürüt **metodunu** arayın.</span><span class="sxs-lookup"><span data-stu-id="5b625-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="5b625-122">Aşağıda, bir MVC Web projesinin yürütme aşamaları listelenebilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5b625-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="5b625-123">Uygulama için ilk isteği alma</span><span class="sxs-lookup"><span data-stu-id="5b625-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="5b625-124">Global.asax **dosyasında, Route** nesneleri **RouteTable** nesnesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="5b625-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="5b625-125">Yönlendirme yapma</span><span class="sxs-lookup"><span data-stu-id="5b625-125">Perform routing</span></span> 

    - <span data-ttu-id="5b625-126">**UrlRoutingModule** modülü, **RouteTable** koleksiyonundaki ilk eşleşen **Route** nesnesini kullanır ve daha sonra **bir İstek Bağlamı** **(IHttpContext)** nesnesi oluşturmak için kullandığı **RouteData** nesnesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b625-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="5b625-127">MVC istek işleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b625-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="5b625-128">**MvcRouteHandler** nesnesi **MvcHandler** sınıfının bir örneğini oluşturur ve **RequestContext** örneğini geçirir.</span><span class="sxs-lookup"><span data-stu-id="5b625-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="5b625-129">Denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b625-129">Create controller</span></span> 

    - <span data-ttu-id="5b625-130">**MvcHandler** nesnesi, **iControllerFactory** nesnesini (genellikle **DefaultControllerFactory** sınıfının bir örneği) tanımlamak için **İstek Bağlamı** örneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5b625-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="5b625-131">Yürütme denetleyicisi - **MvcHandler** örneği denetleyicinin **Execute** yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="5b625-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="5b625-132">Eylemi çağırma</span><span class="sxs-lookup"><span data-stu-id="5b625-132">Invoke action</span></span> 

    - <span data-ttu-id="5b625-133">Denetleyicilerin çoğu **Denetleyici** taban sınıfından devralır.</span><span class="sxs-lookup"><span data-stu-id="5b625-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="5b625-134">Bunu yapan denetleyiciler için, denetleyiciyle ilişkili **ControllerActionInvoker** nesnesi, denetleyici sınıfının hangi eylem yöntemini çağırarak çağıracaklarını belirler ve sonra bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="5b625-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="5b625-135">Sonucu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5b625-135">Execute result</span></span> 

    - <span data-ttu-id="5b625-136">Tipik bir eylem yöntemi kullanıcı girişi alabilir, uygun yanıt verilerini hazırlayabilir ve sonuç türünü döndürerek sonucu çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="5b625-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="5b625-137">Yürütülebilir yerleşik sonuç türleri şunlardır: **ViewResult** (bir görünüm işler ve en sık kullanılan sonuç türüdür), **RedirectToRouteResult**, **ReDirectResult**, **ContentResult**, **JsonResult**, ve **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="5b625-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
