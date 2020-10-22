---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 'SI içinde yönlendirme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345202"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="6d15e-102">ASP.NET Web API 'de yönlendirme</span><span class="sxs-lookup"><span data-stu-id="6d15e-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="6d15e-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6d15e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6d15e-104">Bu makalede, ASP.NET Web API 'SI, HTTP isteklerini denetleyicilere nasıl yönlendirdiğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="6d15e-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="6d15e-105">ASP.NET MVC hakkında bilgi sahibiyseniz, Web API yönlendirmesi MVC yönlendirmeye çok benzer.</span><span class="sxs-lookup"><span data-stu-id="6d15e-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="6d15e-106">Temel fark, Web API 'sinin eylemi seçmek için URI yolunu değil HTTP fiilini kullanması gerektiğidir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="6d15e-107">Ayrıca, Web API 'sinde MVC stili yönlendirmeyi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d15e-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="6d15e-108">Bu makalede, ASP.NET MVC hakkında herhangi bir bilgi varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="6d15e-109">Yönlendirme tabloları</span><span class="sxs-lookup"><span data-stu-id="6d15e-109">Routing Tables</span></span>

<span data-ttu-id="6d15e-110">ASP.NET Web API 'sinde, *DENETLEYICI* http isteklerini işleyen bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="6d15e-111">Denetleyicinin genel yöntemlerine *eylem yöntemleri* veya yalnızca *Eylemler*denir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="6d15e-112">Web API çerçevesi bir istek aldığında, isteği bir eyleme yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="6d15e-113">Hangi eylemin çalıştırılacağını öğrenmek için Framework bir *yönlendirme tablosu*kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="6d15e-114">Web API 'SI için Visual Studio proje şablonu varsayılan bir yol oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6d15e-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="6d15e-115">Bu yol, *uygulama \_ Başlangıç* dizinine yerleştirilmiş *WebApiConfig.cs* dosyasında tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6d15e-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="6d15e-116">Sınıfı hakkında daha fazla bilgi için `WebApiConfig` bkz. [ASP.NET Web API 'sini yapılandırma](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="6d15e-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="6d15e-117">Web API 'sini Self barındırdıysanız, yönlendirme tablosunu doğrudan nesne üzerinde ayarlamanız gerekir `HttpSelfHostConfiguration` .</span><span class="sxs-lookup"><span data-stu-id="6d15e-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="6d15e-118">Daha fazla bilgi için bkz. [kendi kendine konak bir Web API 'si](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="6d15e-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="6d15e-119">Yönlendirme tablosundaki her giriş bir *yol şablonu*içerir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="6d15e-120">Web API 'si için varsayılan yol şablonu, &quot; API/{Controller}/{id} &quot; .</span><span class="sxs-lookup"><span data-stu-id="6d15e-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="6d15e-121">Bu şablonda, &quot; API &quot; bir sabit yol segmenti ve {Controller} ve {id} yer tutucu değişkenleridir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="6d15e-122">Web API çerçevesi bir HTTP isteği aldığında, URI 'yi yönlendirme tablosundaki yol şablonlarından biriyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="6d15e-123">Hiçbir yol eşleşirse, istemci bir 404 hatası alır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="6d15e-124">Örneğin, aşağıdaki URI 'Ler varsayılan yol ile eşleşir:</span><span class="sxs-lookup"><span data-stu-id="6d15e-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="6d15e-125">/api/Contacts</span><span class="sxs-lookup"><span data-stu-id="6d15e-125">/api/contacts</span></span>
- <span data-ttu-id="6d15e-126">/api/Contacts/1</span><span class="sxs-lookup"><span data-stu-id="6d15e-126">/api/contacts/1</span></span>
- <span data-ttu-id="6d15e-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="6d15e-127">/api/products/gizmo1</span></span>

<span data-ttu-id="6d15e-128">Ancak, &quot; API segmentine sahip olmadığı için AŞAĞıDAKI URI eşleşmez &quot; :</span><span class="sxs-lookup"><span data-stu-id="6d15e-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="6d15e-129">/Contacts/1</span><span class="sxs-lookup"><span data-stu-id="6d15e-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="6d15e-130">Yol içinde "API" kullanmanın nedeni ASP.NET MVC yönlendirme ile çarpışmalardan kaçınmaktır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="6d15e-131">Bu şekilde, &quot; /Contacts &quot; bir MVC denetleyicisine gidebilir ve &quot; /api/Contacts &quot; bir Web API denetleyicisine gider.</span><span class="sxs-lookup"><span data-stu-id="6d15e-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="6d15e-132">Kuşkusuz, bu kuralı beğenmezseniz varsayılan yol tablosunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d15e-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="6d15e-133">Eşleşen bir yol bulunduğunda Web API 'SI denetleyiciyi ve eylemi seçer:</span><span class="sxs-lookup"><span data-stu-id="6d15e-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="6d15e-134">Denetleyiciyi bulmak için Web API 'SI, &quot; denetleyiciyi &quot; *{Controller}* değişkeninin değerine ekler.</span><span class="sxs-lookup"><span data-stu-id="6d15e-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="6d15e-135">Eylemi bulmak için Web API 'SI HTTP fiiline bakar ve sonra adı bu HTTP fiili adıyla başlayan bir eylem arar.</span><span class="sxs-lookup"><span data-stu-id="6d15e-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="6d15e-136">Örneğin, GET isteği ile Web API 'SI &quot; &quot; , &quot; GetContact &quot; veya &quot; getallcontacts gibi get ile önekli bir eyleme bakar &quot; .</span><span class="sxs-lookup"><span data-stu-id="6d15e-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="6d15e-137">Bu kural yalnızca GET, POST, PUT, DELETE, HEAD, OPTIONS ve PATCH fiilleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="6d15e-138">Denetleyicinizdeki öznitelikleri kullanarak diğer HTTP fiillerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d15e-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="6d15e-139">Daha sonra bir örnek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6d15e-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="6d15e-140">Yol şablonundaki *{ID}* gibi diğer yer tutucu değişkenleri eylem parametreleriyle eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="6d15e-141">Bir örneğe göz atalım.</span><span class="sxs-lookup"><span data-stu-id="6d15e-141">Let's look at an example.</span></span> <span data-ttu-id="6d15e-142">Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:</span><span class="sxs-lookup"><span data-stu-id="6d15e-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="6d15e-143">İşte, her biri için çağrılan eylem ile birlikte bazı olası HTTP istekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6d15e-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="6d15e-144">HTTP fiili</span><span class="sxs-lookup"><span data-stu-id="6d15e-144">HTTP Verb</span></span> | <span data-ttu-id="6d15e-145">URI yolu</span><span class="sxs-lookup"><span data-stu-id="6d15e-145">URI Path</span></span> | <span data-ttu-id="6d15e-146">Eylem</span><span class="sxs-lookup"><span data-stu-id="6d15e-146">Action</span></span> | <span data-ttu-id="6d15e-147">Parametre</span><span class="sxs-lookup"><span data-stu-id="6d15e-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6d15e-148">GET</span><span class="sxs-lookup"><span data-stu-id="6d15e-148">GET</span></span> | <span data-ttu-id="6d15e-149">API/ürünler</span><span class="sxs-lookup"><span data-stu-id="6d15e-149">api/products</span></span> | <span data-ttu-id="6d15e-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="6d15e-150">GetAllProducts</span></span> | <span data-ttu-id="6d15e-151">*seçim*</span><span class="sxs-lookup"><span data-stu-id="6d15e-151">*(none)*</span></span> |
| <span data-ttu-id="6d15e-152">GET</span><span class="sxs-lookup"><span data-stu-id="6d15e-152">GET</span></span> | <span data-ttu-id="6d15e-153">API/ürünler/4</span><span class="sxs-lookup"><span data-stu-id="6d15e-153">api/products/4</span></span> | <span data-ttu-id="6d15e-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="6d15e-154">GetProductById</span></span> | <span data-ttu-id="6d15e-155">4</span><span class="sxs-lookup"><span data-stu-id="6d15e-155">4</span></span> |
| <span data-ttu-id="6d15e-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="6d15e-156">DELETE</span></span> | <span data-ttu-id="6d15e-157">API/ürünler/4</span><span class="sxs-lookup"><span data-stu-id="6d15e-157">api/products/4</span></span> | <span data-ttu-id="6d15e-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="6d15e-158">DeleteProduct</span></span> | <span data-ttu-id="6d15e-159">4</span><span class="sxs-lookup"><span data-stu-id="6d15e-159">4</span></span> |
| <span data-ttu-id="6d15e-160">POST</span><span class="sxs-lookup"><span data-stu-id="6d15e-160">POST</span></span> | <span data-ttu-id="6d15e-161">API/ürünler</span><span class="sxs-lookup"><span data-stu-id="6d15e-161">api/products</span></span> | <span data-ttu-id="6d15e-162">*(eşleşme yok)*</span><span class="sxs-lookup"><span data-stu-id="6d15e-162">*(no match)*</span></span> |  |

<span data-ttu-id="6d15e-163">Varsa URI 'nin *{id}* segmentinin, eylemin *kimlik* parametresine eşlendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6d15e-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="6d15e-164">Bu örnekte, denetleyici bir *ID* parametresi ve biri parametresi olmayan iki GET yöntemini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6d15e-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="6d15e-165">Ayrıca, denetleyici bir &quot; Post... yöntemi tanımlamadığı IÇIN POST isteğinin başarısız olacağını unutmayın &quot; .</span><span class="sxs-lookup"><span data-stu-id="6d15e-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="6d15e-166">Yönlendirme çeşitlemeleri</span><span class="sxs-lookup"><span data-stu-id="6d15e-166">Routing Variations</span></span>

<span data-ttu-id="6d15e-167">Önceki bölümde ASP.NET Web API 'SI için temel yönlendirme mekanizması açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="6d15e-168">Bu bölümde bazı Çeşitlemeler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="6d15e-169">HTTP fiilleri</span><span class="sxs-lookup"><span data-stu-id="6d15e-169">HTTP verbs</span></span>

<span data-ttu-id="6d15e-170">HTTP fiilleri için adlandırma kuralını kullanmak yerine, eylem yöntemini aşağıdaki özniteliklerden biriyle dekoratarak bir eylem için HTTP fiilini açık bir şekilde belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d15e-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="6d15e-171">Aşağıdaki örnekte, `FindProduct` YÖNTEMI get istekleri ile eşlenir:</span><span class="sxs-lookup"><span data-stu-id="6d15e-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="6d15e-172">Bir eylem için birden çok HTTP fiillerine izin vermek veya GET, PUT, POST, DELETE, HEAD, OPTIONS ve PATCH dışındaki HTTP fiillerine izin vermek için, `[AcceptVerbs]` http fiillerinin bir listesini alan özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d15e-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="6d15e-173">Eylem adına göre yönlendirme</span><span class="sxs-lookup"><span data-stu-id="6d15e-173">Routing by Action Name</span></span>

<span data-ttu-id="6d15e-174">Varsayılan yönlendirme şablonuyla, Web API 'SI eylemi seçmek için HTTP fiilini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="6d15e-175">Bununla birlikte, işlem adının URI 'ye dahil edildiği bir yol da oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d15e-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="6d15e-176">Bu yol şablonunda, *{Action}* parametresi denetleyicisindeki eylem yöntemini adlandırır.</span><span class="sxs-lookup"><span data-stu-id="6d15e-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="6d15e-177">Bu yönlendirme stili ile, izin verilen HTTP fiillerini belirtmek için özniteliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d15e-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="6d15e-178">Örneğin, denetleyicinizin aşağıdaki yöntemi olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="6d15e-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="6d15e-179">Bu durumda, "API/ürünler/Ayrıntılar/1" için bir GET isteği `Details` yöntemine eşlenir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="6d15e-180">Bu yönlendirme stili ASP.NET MVC ile benzerdir ve bir RPC stili API 'SI için uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="6d15e-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="6d15e-181">Özniteliğini kullanarak eylem adını geçersiz kılabilirsiniz `[ActionName]` .</span><span class="sxs-lookup"><span data-stu-id="6d15e-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="6d15e-182">Aşağıdaki örnekte, &quot; API/ürünler/küçük resim/*kimlik*ile eşlenen iki eylem vardır. Bunlardan biri GET 'i destekler ve diğeri GÖNDERISINI destekler:</span><span class="sxs-lookup"><span data-stu-id="6d15e-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="6d15e-183">Eylem dışı</span><span class="sxs-lookup"><span data-stu-id="6d15e-183">Non-Actions</span></span>

<span data-ttu-id="6d15e-184">Bir yöntemin eylem olarak çağrılmasını engellemek için `[NonAction]` özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d15e-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="6d15e-185">Bu, başka bir işlem yönlendirme kurallarıyla eşleşse bile, yöntemin bir eylem olmadığı çerçeveye işaret eder.</span><span class="sxs-lookup"><span data-stu-id="6d15e-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="6d15e-186">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="6d15e-186">Further Reading</span></span>

<span data-ttu-id="6d15e-187">Bu konu, yönlendirmenin üst düzey bir görünümünü sağladı.</span><span class="sxs-lookup"><span data-stu-id="6d15e-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="6d15e-188">Daha fazla ayrıntı için bkz. [Yönlendirme ve eylem seçimi](routing-and-action-selection.md); bu, ÇERÇEVENIN bir URI ile bir yol ile nasıl eşleştiğini açıklar, bir denetleyiciyi seçer ve ardından çağrılacak eylemi seçer.</span><span class="sxs-lookup"><span data-stu-id="6d15e-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
