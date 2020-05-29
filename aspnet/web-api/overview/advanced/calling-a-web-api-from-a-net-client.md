---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET Istemcisinden bir Web API 'SI çağırma (C#)-ASP.NET 4. x
author: MikeWasson
description: Bu öğreticide, bir .NET 4. x uygulamasından bir Web API 'sinin nasıl çağrılacağını gösterilmektedir.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172945"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="307a5-103">.NET Istemcisinden Web API 'SI çağırma (C#)</span><span class="sxs-lookup"><span data-stu-id="307a5-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="307a5-104">, [Mike, son](https://github.com/MikeWasson) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="307a5-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="307a5-105">[Tamamlanmış projeyi indirin](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="307a5-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="307a5-106">[Yönergeleri indirin](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="307a5-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="307a5-107">Bu öğreticide, [System .net. http. HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) kullanılarak .NET uygulamasından BIR Web API 'sinin nasıl çağrılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="307a5-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="307a5-108">Bu öğreticide, aşağıdaki Web API 'sini tüketen bir istemci uygulaması yazılmıştır:</span><span class="sxs-lookup"><span data-stu-id="307a5-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="307a5-109">Eylem</span><span class="sxs-lookup"><span data-stu-id="307a5-109">Action</span></span> | <span data-ttu-id="307a5-110">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="307a5-110">HTTP method</span></span> | <span data-ttu-id="307a5-111">Göreli URI</span><span class="sxs-lookup"><span data-stu-id="307a5-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="307a5-112">KIMLIĞE göre ürün al</span><span class="sxs-lookup"><span data-stu-id="307a5-112">Get a product by ID</span></span> | <span data-ttu-id="307a5-113">GET</span><span class="sxs-lookup"><span data-stu-id="307a5-113">GET</span></span> | <span data-ttu-id="307a5-114">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="307a5-114">/api/products/*id*</span></span> |
| <span data-ttu-id="307a5-115">Yeni ürün oluştur</span><span class="sxs-lookup"><span data-stu-id="307a5-115">Create a new product</span></span> | <span data-ttu-id="307a5-116">POST</span><span class="sxs-lookup"><span data-stu-id="307a5-116">POST</span></span> | <span data-ttu-id="307a5-117">/api/Products</span><span class="sxs-lookup"><span data-stu-id="307a5-117">/api/products</span></span> |
| <span data-ttu-id="307a5-118">Bir ürünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="307a5-118">Update a product</span></span> | <span data-ttu-id="307a5-119">PUT</span><span class="sxs-lookup"><span data-stu-id="307a5-119">PUT</span></span> | <span data-ttu-id="307a5-120">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="307a5-120">/api/products/*id*</span></span> |
| <span data-ttu-id="307a5-121">Bir ürünü silme</span><span class="sxs-lookup"><span data-stu-id="307a5-121">Delete a product</span></span> | <span data-ttu-id="307a5-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="307a5-122">DELETE</span></span> | <span data-ttu-id="307a5-123">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="307a5-123">/api/products/*id*</span></span> |

<span data-ttu-id="307a5-124">Bu API 'yi ASP.NET Web API 'SI ile nasıl uygulayacağınızı öğrenmek için bkz. [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="307a5-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="307a5-125">Kolaylık olması için, bu öğreticideki istemci uygulaması bir Windows konsol uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="307a5-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="307a5-126">**HttpClient** , Windows Phone ve Windows Mağazası uygulamaları için de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="307a5-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="307a5-127">Daha fazla bilgi için bkz. [Taşınabilir kitaplıkları kullanarak birden çok platform Için Web API Istemci kodu yazma](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="307a5-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<span data-ttu-id="307a5-128">**Note:** Temel URL 'Leri ve göreli URI 'Leri sabit kodlanmış değerler olarak geçirirseniz, API 'yi kullanmak için kuralların en az olması gerekir `HttpClient` .</span><span class="sxs-lookup"><span data-stu-id="307a5-128">**NOTE:** If you pass base URLs and relative URIs as hard-coded values, be mindful of the rules for utilizing the `HttpClient` API.</span></span> <span data-ttu-id="307a5-129">`HttpClient.BaseAddress`Özelliği sondaki eğik çizgi () içeren bir adrese ayarlanmalıdır `/` .</span><span class="sxs-lookup"><span data-stu-id="307a5-129">The `HttpClient.BaseAddress` property should be set to an address with a trailing forward slash (`/`).</span></span> <span data-ttu-id="307a5-130">Örneğin, sabit kodlanmış kaynak URI 'Lerini `HttpClient.GetAsync` yönteme geçirirken önünde eğik çizgi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="307a5-130">For example, when passing hard-coded resource URIs to the `HttpClient.GetAsync` method, don't include a leading forward slash.</span></span> <span data-ttu-id="307a5-131">`Product`Kimliğe göre almak için:</span><span class="sxs-lookup"><span data-stu-id="307a5-131">To get a `Product` by ID:</span></span>

1. <span data-ttu-id="307a5-132">Kurmak`client.BaseAddress = new Uri("https://localhost:5001/");`</span><span class="sxs-lookup"><span data-stu-id="307a5-132">Set `client.BaseAddress = new Uri("https://localhost:5001/");`</span></span>
1. <span data-ttu-id="307a5-133">İstek a `Product` .</span><span class="sxs-lookup"><span data-stu-id="307a5-133">Request a `Product`.</span></span> <span data-ttu-id="307a5-134">Örneğin, `client.GetAsync<Product>("api/products/4");`.</span><span class="sxs-lookup"><span data-stu-id="307a5-134">For example, `client.GetAsync<Product>("api/products/4");`.</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="307a5-135">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="307a5-135">Create the Console Application</span></span>

<span data-ttu-id="307a5-136">Visual Studio 'da **Httpclientsample** adlı yeni bir Windows konsol uygulaması oluşturun ve aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="307a5-136">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="307a5-137">Yukarıdaki kod, tüm istemci uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="307a5-137">The preceding code is the complete client app.</span></span>

<span data-ttu-id="307a5-138">`RunAsync`çalışır ve tamamlanana kadar engeller.</span><span class="sxs-lookup"><span data-stu-id="307a5-138">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="307a5-139">Ağ g/ç gerçekleştirdiklerinden, çoğu **HttpClient** yöntemi zaman uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="307a5-139">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="307a5-140">Tüm zaman uyumsuz görevler içinde yapılır `RunAsync` .</span><span class="sxs-lookup"><span data-stu-id="307a5-140">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="307a5-141">Normalde bir uygulama ana iş parçacığını engellemez, ancak bu uygulama hiçbir etkileşime izin vermez.</span><span class="sxs-lookup"><span data-stu-id="307a5-141">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="307a5-142">Web API Istemci kitaplıklarını yükler</span><span class="sxs-lookup"><span data-stu-id="307a5-142">Install the Web API Client Libraries</span></span>

<span data-ttu-id="307a5-143">Web API Istemci kitaplıkları paketini yüklemek için NuGet Paket Yöneticisi 'Ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="307a5-143">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="307a5-144">**Araçlar** menüsünde **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="307a5-144">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="307a5-145">Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="307a5-145">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="307a5-146">Yukarıdaki komut, projeye aşağıdaki NuGet paketlerini ekler:</span><span class="sxs-lookup"><span data-stu-id="307a5-146">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="307a5-147">Microsoft. AspNet. WebApi. Client</span><span class="sxs-lookup"><span data-stu-id="307a5-147">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="307a5-148">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="307a5-148">Newtonsoft.Json</span></span>

<span data-ttu-id="307a5-149">Netmerak Soft. JSON (Json.NET olarak da bilinir), .NET için popüler bir yüksek performanslı JSON çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="307a5-149">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="307a5-150">Model sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="307a5-150">Add a Model Class</span></span>

<span data-ttu-id="307a5-151">Sınıfı inceleyin `Product` :</span><span class="sxs-lookup"><span data-stu-id="307a5-151">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="307a5-152">Bu sınıf, Web API 'SI tarafından kullanılan veri modeliyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="307a5-152">This class matches the data model used by the web API.</span></span> <span data-ttu-id="307a5-153">Bir uygulama, HTTP yanıtından bir örnek okumak için **HttpClient** kullanabilir `Product` .</span><span class="sxs-lookup"><span data-stu-id="307a5-153">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="307a5-154">Uygulamanın seri durumdan çıkarma kodu yazmak zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="307a5-154">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="307a5-155">HttpClient oluşturma ve başlatma</span><span class="sxs-lookup"><span data-stu-id="307a5-155">Create and Initialize HttpClient</span></span>

<span data-ttu-id="307a5-156">Statik **HttpClient** özelliğini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="307a5-156">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="307a5-157">**HttpClient** uygulamasının bir kez oluşturulması ve bir uygulamanın ömrü boyunca yeniden kullanılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="307a5-157">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="307a5-158">Aşağıdaki koşullar, **SocketException** hatalarına neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="307a5-158">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="307a5-159">İstek başına yeni bir **HttpClient** örneği oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="307a5-159">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="307a5-160">Sunucu ağır yük altında.</span><span class="sxs-lookup"><span data-stu-id="307a5-160">Server under heavy load.</span></span>

<span data-ttu-id="307a5-161">Her istek için yeni bir **HttpClient** örneği oluşturulması, kullanılabilir yuvaları tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="307a5-161">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="307a5-162">Aşağıdaki kod, **HttpClient** örneğini başlatır:</span><span class="sxs-lookup"><span data-stu-id="307a5-162">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="307a5-163">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="307a5-163">The preceding code:</span></span>

* <span data-ttu-id="307a5-164">HTTP istekleri için temel URI 'yi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="307a5-164">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="307a5-165">Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="307a5-165">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="307a5-166">Sunucu uygulaması için bağlantı noktası kullanılmadığı takdirde uygulama çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="307a5-166">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="307a5-167">Accept üst bilgisini "Application/JSON" olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="307a5-167">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="307a5-168">Bu üst bilgiyi ayarlamak, sunucuya verileri JSON biçiminde göndermesini söyler.</span><span class="sxs-lookup"><span data-stu-id="307a5-168">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="307a5-169">Kaynak almak için GET isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="307a5-169">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="307a5-170">Aşağıdaki kod, bir ürün için GET isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="307a5-170">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="307a5-171">**GetAsync** YÖNTEMI http get isteğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="307a5-171">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="307a5-172">Yöntem tamamlandığında, HTTP yanıtını içeren bir **HttpResponseMessage** döndürür.</span><span class="sxs-lookup"><span data-stu-id="307a5-172">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="307a5-173">Yanıttaki durum kodu bir başarı kodu ise, yanıt gövdesi bir ürünün JSON gösterimini içerir.</span><span class="sxs-lookup"><span data-stu-id="307a5-173">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="307a5-174">JSON yükünün bir örneğe serisini kaldırmak için **Readasasync** çağrısı yapın `Product` .</span><span class="sxs-lookup"><span data-stu-id="307a5-174">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="307a5-175">Yanıt gövdesi çok büyük olabileceğinden **Readasasync** yöntemi zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="307a5-175">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="307a5-176">HTTP yanıtı bir hata kodu içerdiğinde **HttpClient** bir özel durum oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="307a5-176">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="307a5-177">Bunun yerine, durum bir hata kodu ise **IsSuccessStatusCode** özelliği **false 'tur** .</span><span class="sxs-lookup"><span data-stu-id="307a5-177">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="307a5-178">HTTP hata kodlarını özel durumlar olarak kabul etmek isterseniz, yanıt nesnesinde [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="307a5-178">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="307a5-179">`EnsureSuccessStatusCode`durum kodu 200 299 aralığının dışında kalırsa bir özel durum oluşturur &ndash; .</span><span class="sxs-lookup"><span data-stu-id="307a5-179">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="307a5-180">**HttpClient** &mdash; , istek zaman aşımına uğrarsa diğer nedenlerle özel durumlar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="307a5-180">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="307a5-181">Seri durumdan çıkarılacak medya türü Formatlayıcıları</span><span class="sxs-lookup"><span data-stu-id="307a5-181">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="307a5-182">**Readasasync** parametresi olmadan çağrıldığında, yanıt gövdesini okumak için varsayılan *medya formatlayıcıları* kümesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="307a5-182">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="307a5-183">Varsayılan biçim JSON, XML ve form-URL kodlamalı verileri destekler.</span><span class="sxs-lookup"><span data-stu-id="307a5-183">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="307a5-184">Varsayılan biçimleri kullanmak yerine, **Readasasync** yöntemine bir formatınters listesi sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="307a5-184">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="307a5-185">Özel bir medya türü biçimlendirici varsa, bir biçim listesinin kullanılması yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="307a5-185">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="307a5-186">Daha fazla bilgi için bkz. [ASP.NET Web API 2 ' de medya biçimleri](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="307a5-186">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="307a5-187">Kaynak oluşturmak için POST Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="307a5-187">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="307a5-188">Aşağıdaki kod, JSON biçiminde bir örnek içeren bir POST isteği gönderir `Product` :</span><span class="sxs-lookup"><span data-stu-id="307a5-188">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="307a5-189">**Postasjsonasync** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="307a5-189">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="307a5-190">Bir nesneyi JSON 'a dizleştirir.</span><span class="sxs-lookup"><span data-stu-id="307a5-190">Serializes an object to JSON.</span></span>
* <span data-ttu-id="307a5-191">JSON yükünü bir POST isteğinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="307a5-191">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="307a5-192">İstek başarılı olursa:</span><span class="sxs-lookup"><span data-stu-id="307a5-192">If the request succeeds:</span></span>

* <span data-ttu-id="307a5-193">Bu, 201 (oluşturulan) yanıtı döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="307a5-193">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="307a5-194">Yanıt, konum üstbilgisindeki oluşturulan kaynakların URL 'sini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="307a5-194">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="307a5-195">Bir kaynağı güncelleştirmek için PUT Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="307a5-195">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="307a5-196">Aşağıdaki kod bir ürünü güncelleştirmek için bir PUT isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="307a5-196">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="307a5-197">**Putasjsonasync** yöntemi, post yerıne bir PUT isteği göndermesi dışında, **postasjsonasync**yöntemi gibi çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="307a5-197">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="307a5-198">Bir kaynağı silmek için SILME Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="307a5-198">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="307a5-199">Aşağıdaki kod, bir ürünü silmek için bir SILME isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="307a5-199">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="307a5-200">GET gibi, bir DELETE isteğinin bir istek gövdesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="307a5-200">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="307a5-201">DELETE ile JSON veya XML biçimi belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="307a5-201">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="307a5-202">Örneği test etme</span><span class="sxs-lookup"><span data-stu-id="307a5-202">Test the sample</span></span>

<span data-ttu-id="307a5-203">İstemci uygulamasını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="307a5-203">To test the client app:</span></span>

1. <span data-ttu-id="307a5-204">Sunucu uygulamasını [indirip](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="307a5-204">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="307a5-205">[Yönergeleri indirin](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="307a5-205">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="307a5-206">Sunucu uygulamasının çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="307a5-206">Verify the server app is working.</span></span> <span data-ttu-id="307a5-207">Örneğin, `http://localhost:64195/api/products` ürünlerin bir listesini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="307a5-207">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="307a5-208">HTTP istekleri için temel URI 'yi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="307a5-208">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="307a5-209">Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="307a5-209">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="307a5-210">İstemci uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="307a5-210">Run the client app.</span></span> <span data-ttu-id="307a5-211">Aşağıdaki çıktı üretilir:</span><span class="sxs-lookup"><span data-stu-id="307a5-211">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
