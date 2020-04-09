---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API'de Yönlendirme | Microsoft Dokümanlar
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676134"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="e8af6-102">ASP.NET Web API'sinde yönlendirme</span><span class="sxs-lookup"><span data-stu-id="e8af6-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="e8af6-103">Mike [Wasson](https://github.com/MikeWasson) tarafından</span><span class="sxs-lookup"><span data-stu-id="e8af6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e8af6-104">Bu makalede, web API ASP.NET http isteklerini denetleyicilere nasıl yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="e8af6-105">MVC ASP.NET aşinaysanız, Web API yönlendirmesi MVC yönlendirmesine çok benzer.</span><span class="sxs-lookup"><span data-stu-id="e8af6-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="e8af6-106">Temel fark, Web API'nin eylemi seçmek için URI yolunu değil, HTTP fiilini kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="e8af6-107">Web API'de MVC tarzı yönlendirmeyi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="e8af6-108">Bu makalede, ASP.NET MVC herhangi bir bilgi kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="e8af6-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="e8af6-109">Yönlendirme Tabloları</span><span class="sxs-lookup"><span data-stu-id="e8af6-109">Routing Tables</span></span>

<span data-ttu-id="e8af6-110">Web APIASP.NET denetleyici, HTTP isteklerini işleyen bir *sınıftır.*</span><span class="sxs-lookup"><span data-stu-id="e8af6-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="e8af6-111">Denetleyicinin genel *yöntemlerine eylem yöntemleri* veya basitçe *eylemler*denir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="e8af6-112">Web API çerçevesi bir istek aldığında, isteği bir eyleme yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="e8af6-113">Hangi eylemi çağıracaklarını belirlemek için, çerçeve bir *yönlendirme tablosu*kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="e8af6-114">Web API için Visual Studio proje şablonu varsayılan bir rota oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e8af6-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="e8af6-115">Bu yol, *\_App Start* dizinine yerleştirilen *WebApiConfig.cs* dosyasında tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="e8af6-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="e8af6-116">`WebApiConfig` Sınıf hakkında daha fazla bilgi için, [Web APIASP.NET Yapılandırma'ya](../advanced/configuring-aspnet-web-api.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="e8af6-117">Web API'sini kendi kendine barındırıyorsanız, yönlendirme tablosunu `HttpSelfHostConfiguration` doğrudan nesnenin üzerine ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="e8af6-118">Daha fazla bilgi için, [Bir Web API Self-Host](../older-versions/self-host-a-web-api.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="e8af6-119">Yönlendirme tablosundaki her giriş bir *rota şablonu*içerir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="e8af6-120">Web API için varsayılan &quot;rota şablonu api/{controller}/{id}&quot;olur.</span><span class="sxs-lookup"><span data-stu-id="e8af6-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="e8af6-121">Bu şablonda &quot;api&quot; gerçek bir yol kesimidir ve {controller} ve {id} yer tutucu değişkenlerdir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="e8af6-122">Web API çerçevesi bir HTTP isteği aldığında, URI'yi yönlendirme tablosundaki rota şablonlarından biriyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="e8af6-123">Rota eşleşmezse, istemci 404 hatası alır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="e8af6-124">Örneğin, aşağıdaki URI'ler varsayılan rotayla eşleşir:</span><span class="sxs-lookup"><span data-stu-id="e8af6-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="e8af6-125">/api/kişiler</span><span class="sxs-lookup"><span data-stu-id="e8af6-125">/api/contacts</span></span>
- <span data-ttu-id="e8af6-126">/api/kişiler/1</span><span class="sxs-lookup"><span data-stu-id="e8af6-126">/api/contacts/1</span></span>
- <span data-ttu-id="e8af6-127">/api/ürünler/gizmo1</span><span class="sxs-lookup"><span data-stu-id="e8af6-127">/api/products/gizmo1</span></span>

<span data-ttu-id="e8af6-128">Ancak, &quot;api&quot; segmenti yoksun olduğundan, aşağıdaki URI eşleşmez:</span><span class="sxs-lookup"><span data-stu-id="e8af6-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="e8af6-129">/kişiler/1</span><span class="sxs-lookup"><span data-stu-id="e8af6-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="e8af6-130">Rotada "api" kullanmanın nedeni, ASP.NET MVC yönlendirmesiyle çarpışmaları önlemektir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="e8af6-131">&quot;Bu şekilde, /kişileri&quot; bir MVC denetleyicisine, &quot;/api/kişiler&quot; bir Web API denetleyicisine gitmenizi sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="e8af6-132">Elbette, bu kuralı beğenmezseniz, varsayılan rota tablosunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="e8af6-133">Eşleşen bir rota bulunduğunda, Web API denetleyiciyi ve eylemi seçer:</span><span class="sxs-lookup"><span data-stu-id="e8af6-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="e8af6-134">Denetleyiciyi bulmak için Web &quot;API,&quot; *{controller}* değişkeninin değerine Denetleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="e8af6-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="e8af6-135">Eylemi bulmak için, Web API HTTP fiiline bakar ve sonra adı bu HTTP fiil adı ile başlayan bir eylem arar.</span><span class="sxs-lookup"><span data-stu-id="e8af6-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="e8af6-136">Örneğin, GET isteğiyle, Web API Get &quot;ile önceden&quot;belirlenmiş &quot;bir&quot; eylem &quot;arar&quot;, Örneğin GetContact veya GetAllContacts.</span><span class="sxs-lookup"><span data-stu-id="e8af6-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="e8af6-137">Bu sözleşme yalnızca GET, POST, PUT, DELETE, HEAD, OPTIONS ve PATCH fiilleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="e8af6-138">Denetleyicinizdeki öznitelikleri kullanarak diğer HTTP fiillerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="e8af6-139">Bunun bir örneğini daha sonra göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="e8af6-140">Rota şablonundaki *{id}* gibi diğer yer tutucu değişkenler eylem parametrelerine eşlenir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="e8af6-141">Şimdi örneği inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="e8af6-141">Let's look at an example.</span></span> <span data-ttu-id="e8af6-142">Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:</span><span class="sxs-lookup"><span data-stu-id="e8af6-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="e8af6-143">Olası BAZı HTTP istekleri ve her biri için çağrılan eylem şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e8af6-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="e8af6-144">HTTP Fiil</span><span class="sxs-lookup"><span data-stu-id="e8af6-144">HTTP Verb</span></span> | <span data-ttu-id="e8af6-145">URI Yolu</span><span class="sxs-lookup"><span data-stu-id="e8af6-145">URI Path</span></span> | <span data-ttu-id="e8af6-146">Eylem</span><span class="sxs-lookup"><span data-stu-id="e8af6-146">Action</span></span> | <span data-ttu-id="e8af6-147">Parametre</span><span class="sxs-lookup"><span data-stu-id="e8af6-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e8af6-148">GET</span><span class="sxs-lookup"><span data-stu-id="e8af6-148">GET</span></span> | <span data-ttu-id="e8af6-149">api/ürünler</span><span class="sxs-lookup"><span data-stu-id="e8af6-149">api/products</span></span> | <span data-ttu-id="e8af6-150">GetAllÜrünler</span><span class="sxs-lookup"><span data-stu-id="e8af6-150">GetAllProducts</span></span> | <span data-ttu-id="e8af6-151">*(yok)*</span><span class="sxs-lookup"><span data-stu-id="e8af6-151">*(none)*</span></span> |
| <span data-ttu-id="e8af6-152">GET</span><span class="sxs-lookup"><span data-stu-id="e8af6-152">GET</span></span> | <span data-ttu-id="e8af6-153">api/ürünler/4</span><span class="sxs-lookup"><span data-stu-id="e8af6-153">api/products/4</span></span> | <span data-ttu-id="e8af6-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="e8af6-154">GetProductById</span></span> | <span data-ttu-id="e8af6-155">4</span><span class="sxs-lookup"><span data-stu-id="e8af6-155">4</span></span> |
| <span data-ttu-id="e8af6-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="e8af6-156">DELETE</span></span> | <span data-ttu-id="e8af6-157">api/ürünler/4</span><span class="sxs-lookup"><span data-stu-id="e8af6-157">api/products/4</span></span> | <span data-ttu-id="e8af6-158">Ürünü Silme</span><span class="sxs-lookup"><span data-stu-id="e8af6-158">DeleteProduct</span></span> | <span data-ttu-id="e8af6-159">4</span><span class="sxs-lookup"><span data-stu-id="e8af6-159">4</span></span> |
| <span data-ttu-id="e8af6-160">POST</span><span class="sxs-lookup"><span data-stu-id="e8af6-160">POST</span></span> | <span data-ttu-id="e8af6-161">api/ürünler</span><span class="sxs-lookup"><span data-stu-id="e8af6-161">api/products</span></span> | <span data-ttu-id="e8af6-162">*(eşleşme yok)*</span><span class="sxs-lookup"><span data-stu-id="e8af6-162">*(no match)*</span></span> |  |

<span data-ttu-id="e8af6-163">Varsa URI'nin *{id}* kesiminin eylemin *kimlik* parametresine eşlenediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="e8af6-164">Bu örnekte, denetleyici iki GET yöntemi, bir *id* parametresi ve bir parametre ile tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e8af6-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="e8af6-165">Ayrıca, denetleyici bir &quot;Post tanımlamadığından POST isteğinin başarısız olacağını unutmayın... &quot; yöntemini belirtin.</span><span class="sxs-lookup"><span data-stu-id="e8af6-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="e8af6-166">Yönlendirme Varyasyonları</span><span class="sxs-lookup"><span data-stu-id="e8af6-166">Routing Variations</span></span>

<span data-ttu-id="e8af6-167">Önceki bölümde, ASP.NET Web API için temel yönlendirme mekanizması açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="e8af6-168">Bu bölümde bazı varyasyonlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="e8af6-169">HTTP fiiller</span><span class="sxs-lookup"><span data-stu-id="e8af6-169">HTTP verbs</span></span>

<span data-ttu-id="e8af6-170">HTTP fiilleri için adlandırma kuralını kullanmak yerine, eylem yöntemini aşağıdaki özniteliklerden biriyle süsleyerek eylem için HTTP fiilini açıkça belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8af6-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="e8af6-171">Aşağıdaki örnekte, `FindProduct` yöntem GET istekleri eşlenir:</span><span class="sxs-lookup"><span data-stu-id="e8af6-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="e8af6-172">Bir eylem için birden çok HTTP fiiline izin vermek veya GET, PUT, POST, DELETE, HEAD, `[AcceptVerbs]` OPTIONS ve PATCH dışındaki HTTP fiillerine izin vermek için, HTTP fiillerinin listesini alan özniteliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="e8af6-173">Eylem Adına Göre Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="e8af6-173">Routing by Action Name</span></span>

<span data-ttu-id="e8af6-174">Varsayılan yönlendirme şablonuyla, Web API eylemi seçmek için HTTP fiilini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="e8af6-175">Ancak, eylem adının URI'ye dahil edildiği bir rota da oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8af6-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="e8af6-176">Bu yol şablonunda, *{action}* parametresi denetleyicideki eylem yöntemini adlandırır.</span><span class="sxs-lookup"><span data-stu-id="e8af6-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="e8af6-177">Bu yönlendirme stiliyle, izin verilen HTTP fiillerini belirtmek için öznitelikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="e8af6-178">Örneğin, denetleyicinizin aşağıdaki yönteme sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="e8af6-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="e8af6-179">Bu durumda, "api/products/details/1" için get isteği `Details` yöntemle eşlenecektir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="e8af6-180">Bu yönlendirme stili ASP.NET MVC'ye benzer ve RPC tarzı bir API için uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="e8af6-181">Özniteliği kullanarak `[ActionName]` eylem adını geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8af6-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="e8af6-182">Aşağıdaki örnekte, api/products/thumbnail/ &quot;*id*ile eşleyen iki eylem vardır. Biri GET'i, diğeri post'u destekler:</span><span class="sxs-lookup"><span data-stu-id="e8af6-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="e8af6-183">Eylem Dışı</span><span class="sxs-lookup"><span data-stu-id="e8af6-183">Non-Actions</span></span>

<span data-ttu-id="e8af6-184">Bir yöntemin `[NonAction]` eylem olarak çağrılmasını önlemek için özniteliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="e8af6-185">Bu, yönlendirme kurallarına uyacak olsa bile, yöntemin bir eylem olmadığını çerçeveye bildirir.</span><span class="sxs-lookup"><span data-stu-id="e8af6-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="e8af6-186">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="e8af6-186">Further Reading</span></span>

<span data-ttu-id="e8af6-187">Bu konu yönlendirme nin üst düzey bir görünümünü sağladı.</span><span class="sxs-lookup"><span data-stu-id="e8af6-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="e8af6-188">Daha fazla ayrıntı için, çerçevenin URI ile bir rotayla tam olarak nasıl eşleştiğini açıklayan, bir denetleyici seçen ve sonra çağırmak için eylemi seçen [Yönlendirme ve Eylem Seçimi'ne](routing-and-action-selection.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e8af6-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
