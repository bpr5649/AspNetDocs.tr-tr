---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 Öznitelik Yönlendirme | Microsoft Dokümanlar
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675380"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="58b46-102">ASP.NET Web API 2'de Öznitelik Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="58b46-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="58b46-103">Mike [Wasson](https://github.com/MikeWasson) tarafından</span><span class="sxs-lookup"><span data-stu-id="58b46-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="58b46-104">*Yönlendirme,* Web API'nin bir EYLEMle URI ile eşleştiğinin şeklidir.</span><span class="sxs-lookup"><span data-stu-id="58b46-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="58b46-105">Web API 2, *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türünü destekler.</span><span class="sxs-lookup"><span data-stu-id="58b46-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="58b46-106">Adından da anlaşılacağı gibi, öznitelik yönlendirme yolları tanımlamak için öznitelikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="58b46-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="58b46-107">Öznitelik yönlendirme, web API'nizdeki URI'ler üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="58b46-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="58b46-108">Örneğin, kaynak hiyerarşilerini açıklayan UR'leri kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="58b46-109">Kongre tabanlı yönlendirme olarak adlandırılan daha önceki yönlendirme stili hala tam olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="58b46-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="58b46-110">Aslında, aynı projede her iki tekniği birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="58b46-111">Bu konu öznitelik yönlendirmesini nasıl etkinleştireceklerini gösterir ve öznitelik yönlendirmesi için çeşitli seçenekleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="58b46-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="58b46-112">Öznitelik yönlendirmesini kullanan uçtan uca bir öğretici için [bkz.](create-a-rest-api-with-attribute-routing.md)</span><span class="sxs-lookup"><span data-stu-id="58b46-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58b46-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58b46-113">Prerequisites</span></span>

<span data-ttu-id="58b46-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Topluluk, Profesyonel veya Kurumsal sürüm</span><span class="sxs-lookup"><span data-stu-id="58b46-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="58b46-115">Alternatif olarak, gerekli paketleri yüklemek için NuGet Package Manager'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="58b46-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="58b46-116">Visual Studio'daki **Araçlar** menüsünden **NuGet Package Manager'ı**seçin, ardından **Paket Yöneticisi Konsolu'nu**seçin.</span><span class="sxs-lookup"><span data-stu-id="58b46-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="58b46-117">Paket Yöneticisi Konsolu penceresine aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="58b46-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="58b46-118">Neden Öznitelik Yönlendirme?</span><span class="sxs-lookup"><span data-stu-id="58b46-118">Why Attribute Routing?</span></span>

<span data-ttu-id="58b46-119">Web API'nin ilk *sürümünde kural tabanlı* yönlendirme kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="58b46-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="58b46-120">Bu yönlendirme türünde, temelde parametrelendirilmiş dizeleri olan bir veya daha fazla rota şablonu tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="58b46-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="58b46-121">Çerçeve bir istek aldığında, uri ile rota şablonuyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="58b46-122">Kongre tabanlı yönlendirme hakkında daha fazla bilgi için, [ASP.NET Web API'de Yönlendirme'ye](routing-in-aspnet-web-api.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="58b46-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="58b46-123">Kural tabanlı yönlendirmenin bir avantajı, şablonların tek bir yerde tanımlanması ve yönlendirme kurallarının tüm denetleyicilere tutarlı bir şekilde uygulanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="58b46-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="58b46-124">Ne yazık ki, kongre tabanlı yönlendirme zor RESTful API'larda yaygın olan bazı URI desenleri desteklemek için yapar.</span><span class="sxs-lookup"><span data-stu-id="58b46-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="58b46-125">Örneğin, kaynaklar genellikle alt kaynaklar içerir: Müşterilerin siparişleri vardır, filmlerin aktörleri vardır, kitapların yazarları vardır, vb.</span><span class="sxs-lookup"><span data-stu-id="58b46-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="58b46-126">Bu ilişkileri yansıtan URI'ler oluşturmak doğaldır:</span><span class="sxs-lookup"><span data-stu-id="58b46-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="58b46-127">Uri Bu tür kural tabanlı yönlendirme kullanarak oluşturmak zordur.</span><span class="sxs-lookup"><span data-stu-id="58b46-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="58b46-128">Yapılsa da, çok sayıda denetleyiciniz veya kaynak türünüz varsa sonuçlar iyi ölçeklendirilmez.</span><span class="sxs-lookup"><span data-stu-id="58b46-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="58b46-129">Öznitelik yönlendirmesi ile, bu URI için bir rota tanımlamak için önemsiz.</span><span class="sxs-lookup"><span data-stu-id="58b46-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="58b46-130">Denetleyici eylemine bir öznitelik eklemeniz yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="58b46-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="58b46-131">Yönlendirmenin kolaylaştırdığı diğer desenler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="58b46-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="58b46-132">**API sürüm**</span><span class="sxs-lookup"><span data-stu-id="58b46-132">**API versioning**</span></span>

<span data-ttu-id="58b46-133">Bu örnekte, "/api/v1/products" "/api/v2/products" daha farklı bir denetleyiciye yönlendirildirilebilir.</span><span class="sxs-lookup"><span data-stu-id="58b46-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="58b46-134">**Aşırı yüklenmiş URI segmentleri**</span><span class="sxs-lookup"><span data-stu-id="58b46-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="58b46-135">Bu örnekte, "1" bir sipariş numarasıdır, ancak bir koleksiyona "beklemede" eşler.</span><span class="sxs-lookup"><span data-stu-id="58b46-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="58b46-136">**Birden çok parametre türü**</span><span class="sxs-lookup"><span data-stu-id="58b46-136">**Multiple parameter types**</span></span>

<span data-ttu-id="58b46-137">Bu örnekte, "1" bir sipariş numarasıdır, ancak "2013/06/16" bir tarih belirtir.</span><span class="sxs-lookup"><span data-stu-id="58b46-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="58b46-138">Öznitelik Yönlendirmesini Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="58b46-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="58b46-139">Öznitelik yönlendirmesini etkinleştirmek için yapılandırma sırasında **MapHttpAttributeRoutes'u** arayın.</span><span class="sxs-lookup"><span data-stu-id="58b46-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="58b46-140">Bu uzantı yöntemi **System.Web.Http.HttpConfigurationExtensions** sınıfında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="58b46-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="58b46-141">Öznitelik [yönlendirme, kural tabanlı](routing-in-aspnet-web-api.md) yönlendirme ile birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="58b46-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="58b46-142">Kongre tabanlı rotalar tanımlamak için **MapHttpRoute** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="58b46-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="58b46-143">Web API'yi yapılandırma hakkında daha fazla bilgi için bkz. [ASP.NET Yapılandırma Web API 2.](../advanced/configuring-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="58b46-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="58b46-144">Not: Web API'sinden Geçiş 1</span><span class="sxs-lookup"><span data-stu-id="58b46-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="58b46-145">Web API 2'den önce, Web API proje şablonları aşağıdaki gibi kod lar oluşturmaktadır:</span><span class="sxs-lookup"><span data-stu-id="58b46-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="58b46-146">Öznitelik yönlendirmesi etkinleştirilmişse, bu kod bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58b46-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="58b46-147">Öznitelik yönlendirmesini kullanmak üzere varolan bir Web API projesini yükseltirseniz, bu yapılandırma kodunu aşağıdakilere güncelleştirmeyi unutmayın:</span><span class="sxs-lookup"><span data-stu-id="58b46-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="58b46-148">Daha fazla bilgi için, [web API'yi ASP.NET Barındırma ile Yapılandırma'ya](../advanced/configuring-aspnet-web-api.md#webhost)bakın.</span><span class="sxs-lookup"><span data-stu-id="58b46-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="58b46-149">Rota Öznitelikleri Ekleme</span><span class="sxs-lookup"><span data-stu-id="58b46-149">Adding Route Attributes</span></span>

<span data-ttu-id="58b46-150">Burada bir öznitelik kullanılarak tanımlanan bir rota örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="58b46-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="58b46-151">String &quot;customers/{customerId}/orders,&quot; rota için URI şablonudur.</span><span class="sxs-lookup"><span data-stu-id="58b46-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="58b46-152">Web API, istek URI'yi şablonla eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="58b46-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="58b46-153">Bu örnekte, "müşteriler" ve "siparişler" gerçek segmentlerdir ve "{customerId}" değişken bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="58b46-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="58b46-154">Aşağıdaki URI'ler bu şablonla eşleşir:</span><span class="sxs-lookup"><span data-stu-id="58b46-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="58b46-155">Bu konuda daha sonra açıklanan [kısıtlamaları](#constraints)kullanarak eşleştirmeyi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="58b46-156">Rota şablonundaki &quot;{customerId}&quot; parametresinin yöntemdeki *customerId* parametresinin adıyla eşleştiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="58b46-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="58b46-157">Web API denetleyici eylemini çağırdığında, rota parametrelerini bağlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="58b46-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="58b46-158">Örneğin, URI ise, `http://example.com/customers/1/orders`Web API eylemi *customerId* parametre "1" değerini bağlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="58b46-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="58b46-159">URI şablonunda çeşitli parametreler olabilir:</span><span class="sxs-lookup"><span data-stu-id="58b46-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="58b46-160">Rota özniteliği olmayan tüm denetleyici yöntemleri kural tabanlı yönlendirme kullanır.</span><span class="sxs-lookup"><span data-stu-id="58b46-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="58b46-161">Bu şekilde, aynı projede her iki yönlendirme türünü birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="58b46-162">HTTP Yöntemleri</span><span class="sxs-lookup"><span data-stu-id="58b46-162">HTTP Methods</span></span>

<span data-ttu-id="58b46-163">Web API ayrıca isteğin HTTP yöntemine (GET, POST, vb) dayalı eylemleri seçer.</span><span class="sxs-lookup"><span data-stu-id="58b46-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="58b46-164">Varsayılan olarak, Web API denetleyici yöntemi adının başlangıcı ile bir büyük/küçük harf duyarsız eşleşme arar.</span><span class="sxs-lookup"><span data-stu-id="58b46-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="58b46-165">Örneğin, adlı `PutCustomers` bir denetleyici yöntemi bir HTTP PUT isteğiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="58b46-166">Yöntemi aşağıdaki özniteliklerle süsleyerek bu kuralı geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="58b46-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="58b46-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="58b46-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="58b46-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="58b46-168">**[HttpGet]**</span></span>
- <span data-ttu-id="58b46-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="58b46-169">**[HttpHead]**</span></span>
- <span data-ttu-id="58b46-170">**[Seçenekler]**</span><span class="sxs-lookup"><span data-stu-id="58b46-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="58b46-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="58b46-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="58b46-172">**[Posta]**</span><span class="sxs-lookup"><span data-stu-id="58b46-172">**[HttpPost]**</span></span>
- <span data-ttu-id="58b46-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="58b46-173">**[HttpPut]**</span></span>

<span data-ttu-id="58b46-174">Aşağıdaki örnek, CreateBook yöntemini HTTP POST istekleriyle eşler.</span><span class="sxs-lookup"><span data-stu-id="58b46-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="58b46-175">Standart olmayan yöntemler de dahil olmak üzere diğer tüm HTTP yöntemleri için, HTTP yöntemlerinin bir listesini alan **AcceptVerbs** özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="58b46-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="58b46-176">Rota Önekleri</span><span class="sxs-lookup"><span data-stu-id="58b46-176">Route Prefixes</span></span>

<span data-ttu-id="58b46-177">Genellikle, denetleyicideki yolların tümü aynı önek ile başlar.</span><span class="sxs-lookup"><span data-stu-id="58b46-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="58b46-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="58b46-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="58b46-179">**[RoutePrefix]** özniteliğini kullanarak tüm denetleyici için ortak bir önek ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="58b46-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="58b46-180">Rota önekini geçersiz kılmak için yöntem özniteliğiüzerinde bir tilde (~) kullanın:</span><span class="sxs-lookup"><span data-stu-id="58b46-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="58b46-181">Rota öneki parametreleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="58b46-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="58b46-182">Rota Kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="58b46-182">Route Constraints</span></span>

<span data-ttu-id="58b46-183">Rota kısıtlamaları, rota şablonundaki parametrelerin nasıl eşleşip eşleşip eşleştirildiğini kısıtlamanıza izin sağlar.</span><span class="sxs-lookup"><span data-stu-id="58b46-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="58b46-184">Genel sözdizimi &quot;{parametre:constraint}&quot;'dur.</span><span class="sxs-lookup"><span data-stu-id="58b46-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="58b46-185">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="58b46-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="58b46-186">Burada, ilk rota yalnızca &quot;URI'nin&quot; kimlik bölümü bir sondaysa seçilecektir.</span><span class="sxs-lookup"><span data-stu-id="58b46-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="58b46-187">Aksi takdirde, ikinci rota seçilir.</span><span class="sxs-lookup"><span data-stu-id="58b46-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="58b46-188">Aşağıdaki tabloda desteklenen kısıtlamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="58b46-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="58b46-189">Kısıtlama</span><span class="sxs-lookup"><span data-stu-id="58b46-189">Constraint</span></span> | <span data-ttu-id="58b46-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="58b46-190">Description</span></span> | <span data-ttu-id="58b46-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="58b46-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58b46-192">alfa</span><span class="sxs-lookup"><span data-stu-id="58b46-192">alpha</span></span> | <span data-ttu-id="58b46-193">Büyük veya küçük Latin alfabesi karakterleri (a-z, A-Z) eşleşir</span><span class="sxs-lookup"><span data-stu-id="58b46-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="58b46-194">{x:alfa}</span><span class="sxs-lookup"><span data-stu-id="58b46-194">{x:alpha}</span></span> |
| <span data-ttu-id="58b46-195">bool</span><span class="sxs-lookup"><span data-stu-id="58b46-195">bool</span></span> | <span data-ttu-id="58b46-196">Boolean değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-196">Matches a Boolean value.</span></span> | <span data-ttu-id="58b46-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="58b46-197">{x:bool}</span></span> |
| <span data-ttu-id="58b46-198">datetime</span><span class="sxs-lookup"><span data-stu-id="58b46-198">datetime</span></span> | <span data-ttu-id="58b46-199">**DateTime** değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="58b46-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="58b46-200">{x:datetime}</span></span> |
| <span data-ttu-id="58b46-201">decimal</span><span class="sxs-lookup"><span data-stu-id="58b46-201">decimal</span></span> | <span data-ttu-id="58b46-202">Ondalık değerle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-202">Matches a decimal value.</span></span> | <span data-ttu-id="58b46-203">{x:ondalık}</span><span class="sxs-lookup"><span data-stu-id="58b46-203">{x:decimal}</span></span> |
| <span data-ttu-id="58b46-204">double</span><span class="sxs-lookup"><span data-stu-id="58b46-204">double</span></span> | <span data-ttu-id="58b46-205">64 bit kayan nokta değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="58b46-206">{x:çift}</span><span class="sxs-lookup"><span data-stu-id="58b46-206">{x:double}</span></span> |
| <span data-ttu-id="58b46-207">float</span><span class="sxs-lookup"><span data-stu-id="58b46-207">float</span></span> | <span data-ttu-id="58b46-208">32 bit kayan nokta değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="58b46-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="58b46-209">{x:float}</span></span> |
| <span data-ttu-id="58b46-210">Guıd</span><span class="sxs-lookup"><span data-stu-id="58b46-210">guid</span></span> | <span data-ttu-id="58b46-211">GUID değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-211">Matches a GUID value.</span></span> | <span data-ttu-id="58b46-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="58b46-212">{x:guid}</span></span> |
| <span data-ttu-id="58b46-213">int</span><span class="sxs-lookup"><span data-stu-id="58b46-213">int</span></span> | <span data-ttu-id="58b46-214">32 bit tamsayı değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="58b46-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="58b46-215">{x:int}</span></span> |
| <span data-ttu-id="58b46-216">length</span><span class="sxs-lookup"><span data-stu-id="58b46-216">length</span></span> | <span data-ttu-id="58b46-217">Bir dize belirtilen uzunlukta veya belirli bir uzunluk aralığında eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="58b46-218">{x:uzunluk(6)} {x:uzunluk(1,20)}</span><span class="sxs-lookup"><span data-stu-id="58b46-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="58b46-219">long</span><span class="sxs-lookup"><span data-stu-id="58b46-219">long</span></span> | <span data-ttu-id="58b46-220">64 bit tamsayı değeriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="58b46-221">{x:uzun}</span><span class="sxs-lookup"><span data-stu-id="58b46-221">{x:long}</span></span> |
| <span data-ttu-id="58b46-222">max</span><span class="sxs-lookup"><span data-stu-id="58b46-222">max</span></span> | <span data-ttu-id="58b46-223">En yüksek değere sahip bir tamsayıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="58b46-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="58b46-224">{x:max(10)}</span></span> |
| <span data-ttu-id="58b46-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="58b46-225">maxlength</span></span> | <span data-ttu-id="58b46-226">Bir dize maksimum uzunlukta eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="58b46-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="58b46-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="58b46-228">min</span><span class="sxs-lookup"><span data-stu-id="58b46-228">min</span></span> | <span data-ttu-id="58b46-229">En az değere sahip bir tamsayıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="58b46-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="58b46-230">{x:min(10)}</span></span> |
| <span data-ttu-id="58b46-231">Minlength</span><span class="sxs-lookup"><span data-stu-id="58b46-231">minlength</span></span> | <span data-ttu-id="58b46-232">En az uzunlukta bir dize eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="58b46-233">{x:minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="58b46-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="58b46-234">aralık</span><span class="sxs-lookup"><span data-stu-id="58b46-234">range</span></span> | <span data-ttu-id="58b46-235">Bir tamsede, çeşitli değerler içinde eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="58b46-236">{x:aralığı(10,50)}</span><span class="sxs-lookup"><span data-stu-id="58b46-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="58b46-237">Regex</span><span class="sxs-lookup"><span data-stu-id="58b46-237">regex</span></span> | <span data-ttu-id="58b46-238">Normal bir ifadeyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="58b46-238">Matches a regular expression.</span></span> | <span data-ttu-id="58b46-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="58b46-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="58b46-240">Min &quot;&quot;gibi bazı kısıtlamaların parantez içinde bağımsız değişkenler aldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="58b46-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="58b46-241">Bir üst nokta ile ayrılmış bir parametreye birden çok kısıtlama uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="58b46-242">Özel Rota Kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="58b46-242">Custom Route Constraints</span></span>

<span data-ttu-id="58b46-243">**IHttpRouteConstraint** arabirimini uygulayarak özel rota kısıtlamaları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="58b46-244">Örneğin, aşağıdaki kısıtlama bir parametreyi sıfır olmayan bir tamsayı değeriyle sınırlandırmaz.</span><span class="sxs-lookup"><span data-stu-id="58b46-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="58b46-245">Aşağıdaki kod kısıtlamanın nasıl kaydedilen gösteriş olduğunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="58b46-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="58b46-246">Artık kısıtlamaları rotalarınızda uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="58b46-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="58b46-247">**Ayrıca IInlineConstraintResolver** arabirimini uygulayarak tüm **DefaultInlineConstraintResolver** sınıfını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="58b46-248">Bunu yapmak, **IInlineConstraintResolver** uygulamanız özellikle bunları eklmediği sürece, yerleşik kısıtlamaların tümünün yerini alacaktır.</span><span class="sxs-lookup"><span data-stu-id="58b46-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="58b46-249">İsteğe Bağlı URI Parametreleri ve Varsayılan Değerler</span><span class="sxs-lookup"><span data-stu-id="58b46-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="58b46-250">Rota parametresine soru işareti ekleyerek URI parametresini isteğe bağlı hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="58b46-251">Bir rota parametresi isteğe bağlıysa, yöntem parametresi için varsayılan değer tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58b46-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="58b46-252">Bu örnekte `/api/books/locale/1033` `/api/books/locale` ve aynı kaynağı döndürün.</span><span class="sxs-lookup"><span data-stu-id="58b46-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="58b46-253">Alternatif olarak, rota şablonu içinde aşağıdaki gibi varsayılan bir değer belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="58b46-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="58b46-254">Bu, önceki örnekle hemen hemen aynıdır, ancak varsayılan değer uygulandığında hafif bir davranış farkı vardır.</span><span class="sxs-lookup"><span data-stu-id="58b46-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="58b46-255">İlk örnekte ("{lcid:int?}"), 1033 varsayılan değeri doğrudan yöntem parametresine atanır, böylece parametre tam olarak bu değere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="58b46-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="58b46-256">İkinci örnekte ("{lcid:int=1033}"), "1033"ün varsayılan değeri model bağlama işleminden geçer.</span><span class="sxs-lookup"><span data-stu-id="58b46-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="58b46-257">Varsayılan model bağlayıcısı "1033"ü sayısal değer 1033'e dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="58b46-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="58b46-258">Ancak, farklı bir şey yapabilir özel bir model bağlayıcı, takabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b46-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="58b46-259">(Çoğu durumda, ardışık ardışık nızda özel model bağlayıcıları yoksa, iki form eşdeğer olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="58b46-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="58b46-260">Rota Adları</span><span class="sxs-lookup"><span data-stu-id="58b46-260">Route Names</span></span>

<span data-ttu-id="58b46-261">Web API'sinde her rotanın bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="58b46-261">In Web API, every route has a name.</span></span> <span data-ttu-id="58b46-262">Rota adları, http yanıtına bir bağlantı ekleyebilmeniz için bağlantı oluşturmak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="58b46-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="58b46-263">Rota adını belirtmek için, öznitelik üzerinde **Ad** özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58b46-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="58b46-264">Aşağıdaki örnek, rota adının nasıl ayarlanır ve bağlantı oluştururken rota adının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="58b46-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="58b46-265">Rota Siparişi</span><span class="sxs-lookup"><span data-stu-id="58b46-265">Route Order</span></span>

<span data-ttu-id="58b46-266">Çerçeve bir URI'yi bir rotayla eşleştirmeye çalıştığında, yolları belirli bir sırada değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="58b46-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="58b46-267">Siparişi belirtmek için, rota özniteliği üzerinde **Sipariş** özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58b46-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="58b46-268">Önce daha düşük değerler değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="58b46-268">Lower values are evaluated first.</span></span> <span data-ttu-id="58b46-269">Varsayılan sipariş değeri sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="58b46-269">The default order value is zero.</span></span>

<span data-ttu-id="58b46-270">Toplam sıralama nın nasıl belirlendiği aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="58b46-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="58b46-271">Rota özniteliğinin **Sipariş** özelliğini karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="58b46-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="58b46-272">Rota şablonundaki her URI bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="58b46-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="58b46-273">Her kesim için aşağıdaki gibi sipariş:</span><span class="sxs-lookup"><span data-stu-id="58b46-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="58b46-274">Gerçek bölümler.</span><span class="sxs-lookup"><span data-stu-id="58b46-274">Literal segments.</span></span>
    2. <span data-ttu-id="58b46-275">Kısıtlarla rota parametreleri.</span><span class="sxs-lookup"><span data-stu-id="58b46-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="58b46-276">Kısıtlama olmadan rota parametreleri.</span><span class="sxs-lookup"><span data-stu-id="58b46-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="58b46-277">Joker karakter parametresi kısıtlamaları içeren segmentler.</span><span class="sxs-lookup"><span data-stu-id="58b46-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="58b46-278">Joker karakter parametresi kısıtlama olmadan segmentler.</span><span class="sxs-lookup"><span data-stu-id="58b46-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="58b46-279">Bir kravat durumunda, rotalar rota şablonunun duyarsız bir ordinal dize karşılaştırması[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)tarafından sıralanır.</span><span class="sxs-lookup"><span data-stu-id="58b46-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="58b46-280">Aşağıda bir örnek vardır.</span><span class="sxs-lookup"><span data-stu-id="58b46-280">Here is an example.</span></span> <span data-ttu-id="58b46-281">Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:</span><span class="sxs-lookup"><span data-stu-id="58b46-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="58b46-282">Bu güzergahlar aşağıdaki gibi sıralanır.</span><span class="sxs-lookup"><span data-stu-id="58b46-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="58b46-283">siparişler/ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="58b46-283">orders/details</span></span>
2. <span data-ttu-id="58b46-284">siparişler/{id}</span><span class="sxs-lookup"><span data-stu-id="58b46-284">orders/{id}</span></span>
3. <span data-ttu-id="58b46-285">siparişler/{customerName}</span><span class="sxs-lookup"><span data-stu-id="58b46-285">orders/{customerName}</span></span>
4. <span data-ttu-id="58b46-286">siparişler/{\*tarih}</span><span class="sxs-lookup"><span data-stu-id="58b46-286">orders/{\*date}</span></span>
5. <span data-ttu-id="58b46-287">siparişler/beklemede</span><span class="sxs-lookup"><span data-stu-id="58b46-287">orders/pending</span></span>

<span data-ttu-id="58b46-288">"Ayrıntılar"ın gerçek bir kesim olduğuna ve "{id}" harfinin önünde göründüğüne, ancak **Sipariş** özelliği 1 olduğundan "beklemede" olarak en son göründüğüne dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="58b46-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="58b46-289">(Bu örnek, "ayrıntılar" veya "beklemede" adlı müşteri olmadığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="58b46-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="58b46-290">Genel olarak, belirsiz yolları önlemek için deneyin.</span><span class="sxs-lookup"><span data-stu-id="58b46-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="58b46-291">Bu örnekte, daha iyi `GetByCustomer` bir rota şablonu için "customers/{customerName}" (</span><span class="sxs-lookup"><span data-stu-id="58b46-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
