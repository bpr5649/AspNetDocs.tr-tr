---
title: ASP.NET core'da çıkış noktaları arası istekleri (CORS) etkinleştirme
author: rick-anderson
description: Bilgi nasıl CORS izin verme veya reddetme ASP.NET Core uygulaması çıkış noktaları arası istekleri için standart olarak.
ms.author: riande
ms.custom: mvc
ms.date: 02/08/2019
uid: security/cors
ms.openlocfilehash: bc3a0883043a4d6fa33c1ff76fcb7be457b6b840
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075096"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a><span data-ttu-id="49ecf-103">ASP.NET core'da çıkış noktaları arası istekleri (CORS) etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="49ecf-103">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>

<span data-ttu-id="49ecf-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="49ecf-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="49ecf-105">Bu makalede, bir ASP.NET Core uygulamada CORS'yi etkinleştirme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-105">This article shows how to enable CORS in an ASP.NET Core app.</span></span>

<span data-ttu-id="49ecf-106">Tarayıcı güvenlik, bir web sayfası web sayfada sunulandan daha farklı bir etki alanı istekleri yapmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="49ecf-106">Browser security prevents a web page from making requests to a different domain than the one that served the web page.</span></span> <span data-ttu-id="49ecf-107">Bu kısıtlama adlı *aynı çıkış noktası İlkesi*.</span><span class="sxs-lookup"><span data-stu-id="49ecf-107">This restriction is called the *same-origin policy*.</span></span> <span data-ttu-id="49ecf-108">Aynı kaynak İlkesi, kötü niyetli site başka bir siteden hassas verileri okumasını önler.</span><span class="sxs-lookup"><span data-stu-id="49ecf-108">The same-origin policy prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="49ecf-109">Bazı durumlarda, uygulamanız için diğer sitelere çıkış noktaları arası isteklerde izin vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-109">Sometimes, you might want to allow other sites make cross-origin requests to your app.</span></span> <span data-ttu-id="49ecf-110">Daha fazla bilgi için [Mozilla CORS makale](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).</span><span class="sxs-lookup"><span data-stu-id="49ecf-110">For more information, see the [Mozilla CORS article](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).</span></span>

<span data-ttu-id="49ecf-111">[Çıkış noktaları arası kaynak paylaşımı](https://www.w3.org/TR/cors/) (CORS):</span><span class="sxs-lookup"><span data-stu-id="49ecf-111">[Cross Origin Resource Sharing](https://www.w3.org/TR/cors/) (CORS):</span></span>

* <span data-ttu-id="49ecf-112">Gevşek bir aynı çıkış noktası İlkesi bir sunucu izin veren bir W3C standarttır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-112">Is a W3C standard that allows a server to relax the same-origin policy.</span></span>
* <span data-ttu-id="49ecf-113">Olan **değil** CORS bir güvenlik özelliği güvenlik rahatlatır;.</span><span class="sxs-lookup"><span data-stu-id="49ecf-113">Is **not** a security feature, CORS relaxes security.</span></span> <span data-ttu-id="49ecf-114">API CORS tanıyarak güvenli değil</span><span class="sxs-lookup"><span data-stu-id="49ecf-114">An API is not safer by allowing CORS.</span></span> <span data-ttu-id="49ecf-115">Daha fazla bilgi için [CORS nasıl çalıştığını](#how-cors).</span><span class="sxs-lookup"><span data-stu-id="49ecf-115">For more information, see [How CORS works](#how-cors).</span></span>
* <span data-ttu-id="49ecf-116">Açıkça bazı çıkış noktaları arası istekleri izin verirken diğerlerini sunucuya sağlar.</span><span class="sxs-lookup"><span data-stu-id="49ecf-116">Allows a server to explicitly allow some cross-origin requests while rejecting others.</span></span>
* <span data-ttu-id="49ecf-117">Güvenli ve önceki teknikleri, daha esnek olduğu gibi [JSONP](/dotnet/framework/wcf/samples/jsonp).</span><span class="sxs-lookup"><span data-stu-id="49ecf-117">Is safer and more flexible than earlier techniques, such as [JSONP](/dotnet/framework/wcf/samples/jsonp).</span></span>

<span data-ttu-id="49ecf-118">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/2.2-stage-samples) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="49ecf-118">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/2.2-stage-samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="same-origin"></a><span data-ttu-id="49ecf-119">Aynı kaynak</span><span class="sxs-lookup"><span data-stu-id="49ecf-119">Same origin</span></span>

<span data-ttu-id="49ecf-120">İki URL aynı düzenleri, konaklar ve bağlantı noktaları varsa aynı kaynağa sahip ([RFC 6454](https://tools.ietf.org/html/rfc6454)).</span><span class="sxs-lookup"><span data-stu-id="49ecf-120">Two URLs have the same origin if they have identical schemes, hosts, and ports ([RFC 6454](https://tools.ietf.org/html/rfc6454)).</span></span>

<span data-ttu-id="49ecf-121">Bu iki URL aynı kaynağa sahip:</span><span class="sxs-lookup"><span data-stu-id="49ecf-121">These two URLs have the same origin:</span></span>

* `https://example.com/foo.html`
* `https://example.com/bar.html`

<span data-ttu-id="49ecf-122">Bu URL'ler, önceki iki URL değerinden farklı çıkış noktaları vardır:</span><span class="sxs-lookup"><span data-stu-id="49ecf-122">These URLs have different origins than the previous two URLs:</span></span>

* <span data-ttu-id="49ecf-123">`https://example.net` &ndash; Farklı bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="49ecf-123">`https://example.net` &ndash; Different domain</span></span>
* <span data-ttu-id="49ecf-124">`https://www.example.com/foo.html` &ndash; Farklı alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="49ecf-124">`https://www.example.com/foo.html` &ndash; Different subdomain</span></span>
* <span data-ttu-id="49ecf-125">`http://example.com/foo.html` &ndash; Farklı düzeni</span><span class="sxs-lookup"><span data-stu-id="49ecf-125">`http://example.com/foo.html` &ndash; Different scheme</span></span>
* <span data-ttu-id="49ecf-126">`https://example.com:9000/foo.html` &ndash; Farklı bir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="49ecf-126">`https://example.com:9000/foo.html` &ndash; Different port</span></span>

<span data-ttu-id="49ecf-127">Internet Explorer kaynakları karşılaştırılırken, bağlantı noktası dikkate almaz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-127">Internet Explorer doesn't consider the port when comparing origins.</span></span>

## <a name="cors-with-named-policy-and-middleware"></a><span data-ttu-id="49ecf-128">CORS adlandırılmış ilke ve ara yazılım</span><span class="sxs-lookup"><span data-stu-id="49ecf-128">CORS with named policy and middleware</span></span>

<span data-ttu-id="49ecf-129">CORS Ara çıkış noktaları arası istekleri işler.</span><span class="sxs-lookup"><span data-stu-id="49ecf-129">CORS Middleware handles cross-origin requests.</span></span> <span data-ttu-id="49ecf-130">Aşağıdaki kod, uygulamanın tamamında ile belirtilen kaynak için CORS sağlar:</span><span class="sxs-lookup"><span data-stu-id="49ecf-130">The following code enables CORS for the entire app with the specified origin:</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/Startup.cs?name=snippet&highlight=8,14-23,38)]

<span data-ttu-id="49ecf-131">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="49ecf-131">The preceding code:</span></span>

* <span data-ttu-id="49ecf-132">İlke adı "_myAllowSpecificOrigins" olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="49ecf-132">Sets the policy name to "_myAllowSpecificOrigins".</span></span> <span data-ttu-id="49ecf-133">İlke adı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-133">The policy name is arbitrary.</span></span>
* <span data-ttu-id="49ecf-134">Çağrıları <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> çekirdek sağlayan genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="49ecf-134">Calls the <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> extension method, which enables cores.</span></span>
* <span data-ttu-id="49ecf-135">Çağrıları <xref:Microsoft.Extensions.DependencyInjection.CorsServiceCollectionExtensions.AddCors*> ile bir [lambda ifadesi](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="49ecf-135">Calls <xref:Microsoft.Extensions.DependencyInjection.CorsServiceCollectionExtensions.AddCors*> with a [lambda expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="49ecf-136">Lambda alan bir <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> nesne.</span><span class="sxs-lookup"><span data-stu-id="49ecf-136">The lambda takes a <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> object.</span></span> <span data-ttu-id="49ecf-137">[Yapılandırma seçenekleri](#cors-policy-options), gibi `WithOrigins`, bu makalenin sonraki bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-137">[Configuration options](#cors-policy-options), such as `WithOrigins`, are described later in this article.</span></span>

<span data-ttu-id="49ecf-138"><xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> Yöntem çağrısının CORS Hizmetleri uygulamanın hizmet kapsayıcıya ekler:</span><span class="sxs-lookup"><span data-stu-id="49ecf-138">The <xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> method call adds CORS services to the app's service container:</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/Startup.cs?name=snippet2)]

<span data-ttu-id="49ecf-139">Daha fazla bilgi için [CORS ilkesi seçenekleri](#cpo) bu belgedeki.</span><span class="sxs-lookup"><span data-stu-id="49ecf-139">For more information, see [CORS policy options](#cpo) in this document .</span></span>

<span data-ttu-id="49ecf-140"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> Yöntemi aşağıdaki kodda gösterildiği gibi yöntemleri, zincir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-140">The <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> method can chain methods, as shown in the following code:</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/Startup2.cs?name=snippet2)]

<span data-ttu-id="49ecf-141">Aşağıdaki vurgulanmış kodu tüm uygulamaları uç noktalar için CORS ilkelerini uygular [CORS ara yazılımı](#enable-cors-with-cors-middleware):</span><span class="sxs-lookup"><span data-stu-id="49ecf-141">The following highlighted code applies CORS policies to all the apps endpoints via [CORS Middleware](#enable-cors-with-cors-middleware):</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/Startup.cs?name=snippet3&highlight=12)]

<span data-ttu-id="49ecf-142">Bkz: [Razor sayfaları, denetleyiciler ve eylem yöntemlerine CORS'yi etkinleştirme](#ecors) CORS ilkesini denetleyicisi/sayfa/eylemi düzeyinde uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="49ecf-142">See [Enable CORS in Razor Pages, controllers, and action methods](#ecors) to apply CORS policy at the page/controller/action level.</span></span>

<span data-ttu-id="49ecf-143">Not:</span><span class="sxs-lookup"><span data-stu-id="49ecf-143">Note:</span></span>

* <span data-ttu-id="49ecf-144">`UseCors` önce çağrılmalıdır `UseMvc`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-144">`UseCors` must be called before `UseMvc`.</span></span>
* <span data-ttu-id="49ecf-145">URL gerekir **değil** sonunda eğik çizgi içermelidir (`/`).</span><span class="sxs-lookup"><span data-stu-id="49ecf-145">The URL must **not** contain a trailing slash (`/`).</span></span> <span data-ttu-id="49ecf-146">URL ile sona ererse `/`, karşılaştırma döndürür `false` ve üst bilgi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="49ecf-146">If the URL terminates with `/`, the comparison returns `false` and no header is returned.</span></span>

<span data-ttu-id="49ecf-147">Bkz: [Test CORS](#test) yönergeler için yukarıdaki kod test etme.</span><span class="sxs-lookup"><span data-stu-id="49ecf-147">See [Test CORS](#test) for instructions on testing the preceding code.</span></span>

<a name="ecors"></a>

## <a name="enable-cors-with-attributes"></a><span data-ttu-id="49ecf-148">Özniteliklerle CORS'yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="49ecf-148">Enable CORS with attributes</span></span>

<span data-ttu-id="49ecf-149">[ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) öznitelik CORS genel uygulama için bir alternatif sağlar.</span><span class="sxs-lookup"><span data-stu-id="49ecf-149">The [&lbrack;EnableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) attribute provides an alternative to applying CORS globally.</span></span> <span data-ttu-id="49ecf-150">`[EnableCors]` Özniteliği, tüm uç noktaları yerine seçili uç noktaları için CORS sağlar.</span><span class="sxs-lookup"><span data-stu-id="49ecf-150">The `[EnableCors]` attribute enables CORS for selected end points, rather than all end points.</span></span>

<span data-ttu-id="49ecf-151">Kullanım `[EnableCors]` varsayılan ilkesi belirlemek ve `[EnableCors("{Policy String}")]` ilke belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="49ecf-151">Use `[EnableCors]` to specify the default policy and `[EnableCors("{Policy String}")]` to specify a policy.</span></span>

<span data-ttu-id="49ecf-152">`[EnableCors]` Özniteliği uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-152">The `[EnableCors]` attribute can be applied to:</span></span>

* <span data-ttu-id="49ecf-153">Razor sayfası `PageModel`</span><span class="sxs-lookup"><span data-stu-id="49ecf-153">Razor Page `PageModel`</span></span>
* <span data-ttu-id="49ecf-154">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="49ecf-154">Controller</span></span>
* <span data-ttu-id="49ecf-155">Denetleyici eylem yöntemi</span><span class="sxs-lookup"><span data-stu-id="49ecf-155">Controller action method</span></span>

<span data-ttu-id="49ecf-156">Denetleyici/sayfası-model/eylem ile farklı ilkeler uygulayabilirsiniz `[EnableCors]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="49ecf-156">You can apply different policies to controller/page-model/action with the  `[EnableCors]` attribute.</span></span> <span data-ttu-id="49ecf-157">Zaman `[EnableCors]` özniteliği denetleyicileri/sayfası-model/eylem yöntemine uygulanan ve CORS Ara yazılımında etkin, her iki ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-157">When the `[EnableCors]` attribute is applied to a controllers/page-model/action method, and CORS is enabled in middleware, both policies are applied.</span></span> <span data-ttu-id="49ecf-158">İlkeleri birleştirme karşı öneririz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-158">We recommend against combining policies.</span></span> <span data-ttu-id="49ecf-159">Kullanım `[EnableCors]` özniteliği veya her ikisini birden aynı uygulama ara yazılım.</span><span class="sxs-lookup"><span data-stu-id="49ecf-159">Use the `[EnableCors]` attribute or middleware, not both in the same app.</span></span>

<span data-ttu-id="49ecf-160">Aşağıdaki kod, farklı bir ilke her yönteme uygulanır:</span><span class="sxs-lookup"><span data-stu-id="49ecf-160">The following code applies a different policy to each method:</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/Controllers/WidgetController.cs?name=snippet&highlight=6,14)]

<span data-ttu-id="49ecf-161">Aşağıdaki kod bir CORS varsayılan ilkesi ve adlı bir ilke oluşturur `"AnotherPolicy"`:</span><span class="sxs-lookup"><span data-stu-id="49ecf-161">The following code creates a CORS default policy and a policy named `"AnotherPolicy"`:</span></span>

[!code-csharp[](cors/sample/Cors/WebAPI/StartupMultiPolicy.cs?name=snippet&highlight=12-28)]

### <a name="disable-cors"></a><span data-ttu-id="49ecf-162">CORS devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="49ecf-162">Disable CORS</span></span>

<span data-ttu-id="49ecf-163">[ &lbrack;DisableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) özniteliği devre dışı bırakır CORS denetleyicisi/sayfası-model/için eylem.</span><span class="sxs-lookup"><span data-stu-id="49ecf-163">The [&lbrack;DisableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) attribute disables CORS for the controller/page-model/action.</span></span>

<a name="cpo"></a>

## <a name="cors-policy-options"></a><span data-ttu-id="49ecf-164">CORS ilkesi seçenekleri</span><span class="sxs-lookup"><span data-stu-id="49ecf-164">CORS policy options</span></span>

<span data-ttu-id="49ecf-165">Bu bölümde, CORS ilke ayarlanabilir çeşitli seçenekler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="49ecf-165">This section describes the various options that can be set in a CORS policy:</span></span>

* [<span data-ttu-id="49ecf-166">İzin verilen çıkış noktaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="49ecf-166">Set the allowed origins</span></span>](#set-the-allowed-origins)
* [<span data-ttu-id="49ecf-167">İzin verilen HTTP yöntemleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-167">Set the allowed HTTP methods</span></span>](#set-the-allowed-http-methods)
* [<span data-ttu-id="49ecf-168">İzin verilen istek üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-168">Set the allowed request headers</span></span>](#set-the-allowed-request-headers)
* [<span data-ttu-id="49ecf-169">İfşa edilen yanıt üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-169">Set the exposed response headers</span></span>](#set-the-exposed-response-headers)
* [<span data-ttu-id="49ecf-170">Çıkış noktaları arası istekleri kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="49ecf-170">Credentials in cross-origin requests</span></span>](#credentials-in-cross-origin-requests)
* [<span data-ttu-id="49ecf-171">Denetim öncesi sona erme saati ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-171">Set the preflight expiration time</span></span>](#set-the-preflight-expiration-time)

 <span data-ttu-id="49ecf-172"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsOptions.AddPolicy*> çağrılma yeri `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-172"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsOptions.AddPolicy*> is called in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="49ecf-173">Bazı seçenekleri okumak yardımcı olabilecek [CORS nasıl çalıştığını](#how-cors) ilk bölümü.</span><span class="sxs-lookup"><span data-stu-id="49ecf-173">For some options, it may be helpful to read the [How CORS works](#how-cors) section first.</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="49ecf-174">İzin verilen çıkış noktaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="49ecf-174">Set the allowed origins</span></span>

<span data-ttu-id="49ecf-175"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*> &ndash; CORS istekleri herhangi şeması ile tüm kaynaklara izin verir (`http` veya `https`).</span><span class="sxs-lookup"><span data-stu-id="49ecf-175"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*> &ndash; Allows CORS requests from all origins with any scheme (`http` or `https`).</span></span> <span data-ttu-id="49ecf-176">`AllowAnyOrigin` güvenli değil çünkü *herhangi bir Web sitesinde* çıkış noktaları arası istekleri için uygulama yapabilir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-176">`AllowAnyOrigin` is insecure because *any website* can make cross-origin requests to the app.</span></span>

  ::: moniker range=">= aspnetcore-2.2"

  > [!NOTE]
  > <span data-ttu-id="49ecf-177">Belirtme `AllowAnyOrigin` ve `AllowCredentials` güvensiz bir yapılandırmadır ve siteler arası istek sahteciliğini neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-177">Specifying `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration and can result in cross-site request forgery.</span></span> <span data-ttu-id="49ecf-178">Bir uygulamanın her iki yöntemde de yapılandırıldığında CORS hizmeti geçersiz bir CORS yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="49ecf-178">The CORS service returns an invalid CORS response when an app is configured with both methods.</span></span>

  ::: moniker-end

  ::: moniker range="< aspnetcore-2.2"

  > [!NOTE]
  > <span data-ttu-id="49ecf-179">Belirtme `AllowAnyOrigin` ve `AllowCredentials` güvensiz bir yapılandırmadır ve siteler arası istek sahteciliğini neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-179">Specifying `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration and can result in cross-site request forgery.</span></span> <span data-ttu-id="49ecf-180">İstemci sunucu kaynaklarına erişmek için yetkilendirmeniz gerekiyorsa güvenli bir uygulama için başlangıç noktaları tam bir listesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="49ecf-180">For a secure app, specify an exact list of origins if the client must authorize itself to access server resources.</span></span>

  ::: moniker-end

<!-- REVIEW required
I changed from
Specifying `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration. **This** setting affects preflight requests and the ...
to
**`AllowAnyOrigin`** affects preflight requests and the

to remove the ambiguous **This**. 
-->

  <span data-ttu-id="49ecf-181">`AllowAnyOrigin` etkiler ön kontrol istekleri ve `Access-Control-Allow-Origin` başlığı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-181">`AllowAnyOrigin` affects preflight requests and the `Access-Control-Allow-Origin` header.</span></span> <span data-ttu-id="49ecf-182">Daha fazla bilgi için [öncesi istekleri](#preflight-requests) bölümü.</span><span class="sxs-lookup"><span data-stu-id="49ecf-182">For more information, see the [Preflight requests](#preflight-requests) section.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="49ecf-183"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetIsOriginAllowedToAllowWildcardSubdomains*> &ndash; Kümeleri <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.IsOriginAllowed*> yapılandırılmış joker karakter etki alanı kaynağını izin verilip verilmediğini değerlendirirken eşleşecek şekilde kaynakları sağlayan bir işlevi ilkesinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="49ecf-183"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetIsOriginAllowedToAllowWildcardSubdomains*> &ndash; Sets the <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.IsOriginAllowed*> property of the policy to be a function that allows origins to match a configured wildcard domain when evaluating if the origin is allowed.</span></span>

  [!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=100-104&highlight=4)]

::: moniker-end

### <a name="set-the-allowed-http-methods"></a><span data-ttu-id="49ecf-184">İzin verilen HTTP yöntemleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-184">Set the allowed HTTP methods</span></span>

<span data-ttu-id="49ecf-185"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-185"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span></span>

* <span data-ttu-id="49ecf-186">Herhangi bir HTTP yöntemini sağlar:</span><span class="sxs-lookup"><span data-stu-id="49ecf-186">Allows any HTTP method:</span></span>
* <span data-ttu-id="49ecf-187">Etkiler ön kontrol istekleri ve `Access-Control-Allow-Methods` başlığı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-187">Affects preflight requests and the `Access-Control-Allow-Methods` header.</span></span> <span data-ttu-id="49ecf-188">Daha fazla bilgi için [öncesi istekleri](#preflight-requests) bölümü.</span><span class="sxs-lookup"><span data-stu-id="49ecf-188">For more information, see the [Preflight requests](#preflight-requests) section.</span></span>

### <a name="set-the-allowed-request-headers"></a><span data-ttu-id="49ecf-189">İzin verilen istek üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-189">Set the allowed request headers</span></span>

<span data-ttu-id="49ecf-190">Adlı bir CORS isteğinde gönderilecek belirli üstbilgilere izin için *yazar, istek üst bilgilerini*, çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> ve izin verilen üstbilgileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="49ecf-190">To allow specific headers to be sent in a CORS request, called *author request headers*, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> and specify the allowed headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=55-60&highlight=5)]

<span data-ttu-id="49ecf-191">Tüm istek üstbilgilerini Yazar izin vermek için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-191">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=64-69&highlight=5)]

<span data-ttu-id="49ecf-192">Bu ayar Denetim öncesi isteği etkiler ve `Access-Control-Request-Headers` başlığı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-192">This setting affects preflight requests and the `Access-Control-Request-Headers` header.</span></span> <span data-ttu-id="49ecf-193">Daha fazla bilgi için [öncesi istekleri](#preflight-requests) bölümü.</span><span class="sxs-lookup"><span data-stu-id="49ecf-193">For more information, see the [Preflight requests](#preflight-requests) section.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="49ecf-194">CORS ara yazılımı ilke eşleşmesi için belirli üst bilgileri tarafından belirtilen `WithHeaders` gönderilen üst bilgiler, yalnızca mümkündür `Access-Control-Request-Headers` belirtilen üst bilgilerin tam olarak eşleşmesi `WithHeaders`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-194">A CORS Middleware policy match to specific headers specified by `WithHeaders` is only possible when the headers sent in `Access-Control-Request-Headers` exactly match the headers stated in `WithHeaders`.</span></span>

<span data-ttu-id="49ecf-195">Örneğin, şu şekilde yapılandırılmış bir uygulama göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="49ecf-195">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="49ecf-196">CORS ara yazılımı, çünkü bir denetim öncesi isteği şu istek üst bilgisi ile azalma `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage)) içinde listelenmiyor `WithHeaders`:</span><span class="sxs-lookup"><span data-stu-id="49ecf-196">CORS Middleware declines a preflight request with the following request header because `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage)) isn't listed in `WithHeaders`:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

<span data-ttu-id="49ecf-197">Uygulama döndürür bir *200 Tamam* yanıt geri CORS üst bilgileri göndermez ancak.</span><span class="sxs-lookup"><span data-stu-id="49ecf-197">The app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="49ecf-198">Bu nedenle, tarayıcının çıkış noktaları arası istek çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-198">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="49ecf-199">CORS ara yazılımı, her zaman dört üst bilgilerinde sağlar `Access-Control-Request-Headers` CorsPolicy.Headers içinde yapılandırılan değerlere bakılmaksızın gönderilecek.</span><span class="sxs-lookup"><span data-stu-id="49ecf-199">CORS Middleware always allows four headers in the `Access-Control-Request-Headers` to be sent regardless of the values configured in CorsPolicy.Headers.</span></span> <span data-ttu-id="49ecf-200">Üst bilgi bu liste aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-200">This list of headers includes:</span></span>

* `Accept`
* `Accept-Language`
* `Content-Language`
* `Origin`

<span data-ttu-id="49ecf-201">Örneğin, şu şekilde yapılandırılmış bir uygulama göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="49ecf-201">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="49ecf-202">CORS ara yazılımın yanıt başarıyla bir denetim öncesi isteği şu istek üst bilgisi için çünkü `Content-Language` her zaman izin verilenler listesinde olur:</span><span class="sxs-lookup"><span data-stu-id="49ecf-202">CORS Middleware responds successfully to a preflight request with the following request header because `Content-Language` is always whitelisted:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

::: moniker-end

### <a name="set-the-exposed-response-headers"></a><span data-ttu-id="49ecf-203">İfşa edilen yanıt üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-203">Set the exposed response headers</span></span>

<span data-ttu-id="49ecf-204">Varsayılan olarak, tüm yanıt üstbilgilerini uygulamaya tarayıcı ortaya çıkarmıyor.</span><span class="sxs-lookup"><span data-stu-id="49ecf-204">By default, the browser doesn't expose all of the response headers to the app.</span></span> <span data-ttu-id="49ecf-205">Daha fazla bilgi için [W3C çıkış noktaları arası kaynak paylaşımı (terminolojisi): Basit bir yanıt üstbilgisi](https://www.w3.org/TR/cors/#simple-response-header).</span><span class="sxs-lookup"><span data-stu-id="49ecf-205">For more information, see [W3C Cross-Origin Resource Sharing (Terminology): Simple Response Header](https://www.w3.org/TR/cors/#simple-response-header).</span></span>

<span data-ttu-id="49ecf-206">Varsayılan olarak kullanılabilir olan yanıt üstbilgilerini şunlardır:</span><span class="sxs-lookup"><span data-stu-id="49ecf-206">The response headers that are available by default are:</span></span>

* `Cache-Control`
* `Content-Language`
* `Content-Type`
* `Expires`
* `Last-Modified`
* `Pragma`

<span data-ttu-id="49ecf-207">Bu üst CORS belirtimi çağırır *basit yanıt üstbilgilerini*.</span><span class="sxs-lookup"><span data-stu-id="49ecf-207">The CORS specification calls these headers *simple response headers*.</span></span> <span data-ttu-id="49ecf-208">Diğer üst bilgileri uygulama için kullanılabilir hale getirmek için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-208">To make other headers available to the app, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=73-78&highlight=5)]

### <a name="credentials-in-cross-origin-requests"></a><span data-ttu-id="49ecf-209">Çıkış noktaları arası istekleri kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="49ecf-209">Credentials in cross-origin requests</span></span>

<span data-ttu-id="49ecf-210">Özel işleme bir CORS isteğinde kimlik bilgilerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-210">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="49ecf-211">Varsayılan olarak, tarayıcının çıkış noktaları arası istek ile kimlik bilgileri göndermez.</span><span class="sxs-lookup"><span data-stu-id="49ecf-211">By default, the browser doesn't send credentials with a cross-origin request.</span></span> <span data-ttu-id="49ecf-212">Tanımlama bilgileri ve kimlik doğrulama düzeni HTTP kimlik bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-212">Credentials include cookies and HTTP authentication schemes.</span></span> <span data-ttu-id="49ecf-213">İstemci kimlik bilgileriyle bir çıkış noktaları arası istek göndermek için ayarlamalısınız `XMLHttpRequest.withCredentials` için `true`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-213">To send credentials with a cross-origin request, the client must set `XMLHttpRequest.withCredentials` to `true`.</span></span>

<span data-ttu-id="49ecf-214">Kullanarak `XMLHttpRequest` doğrudan:</span><span class="sxs-lookup"><span data-stu-id="49ecf-214">Using `XMLHttpRequest` directly:</span></span>

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'https://www.example.com/api/test');
xhr.withCredentials = true;
```

<span data-ttu-id="49ecf-215">JQuery kullanarak:</span><span class="sxs-lookup"><span data-stu-id="49ecf-215">Using jQuery:</span></span>

```javascript
$.ajax({
  type: 'get',
  url: 'https://www.example.com/api/test',
  xhrFields: {
    withCredentials: true
  }
});
```

<span data-ttu-id="49ecf-216">Kullanarak [Fetch API'sini](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API):</span><span class="sxs-lookup"><span data-stu-id="49ecf-216">Using the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API):</span></span>

```javascript
fetch('https://www.example.com/api/test', {
    credentials: 'include'
});
```

<span data-ttu-id="49ecf-217">Sunucu kimlik bilgilerine izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-217">The server must allow the credentials.</span></span> <span data-ttu-id="49ecf-218">Çıkış noktaları arası kimlik bilgilerini sağlamak için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-218">To allow cross-origin credentials, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=82-87&highlight=5)]

<span data-ttu-id="49ecf-219">HTTP yanıtı içeren bir `Access-Control-Allow-Credentials` sunucu çıkış noktaları arası istek için kimlik bilgilerini sağlayan tarayıcı söyler. başlığı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-219">The HTTP response includes an `Access-Control-Allow-Credentials` header, which tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="49ecf-220">Tarayıcı bilgilerini gönderir, ancak yanıt geçerli bir içermez `Access-Control-Allow-Credentials` üst bilgi, tarayıcı olmayan uygulama yanıtı kullanımına sunun ve çıkış noktaları arası istek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="49ecf-220">If the browser sends credentials but the response doesn't include a valid `Access-Control-Allow-Credentials` header, the browser doesn't expose the response to the app, and the cross-origin request fails.</span></span>

<span data-ttu-id="49ecf-221">Çıkış noktaları arası kimlik bilgilerini sağlayan bir güvenlik riski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="49ecf-221">Allowing cross-origin credentials is a security risk.</span></span> <span data-ttu-id="49ecf-222">Başka bir etki alanındaki bir Web sitesi kullanıcı bilgisi olmadan kullanıcı adına uygulamasında oturum açmış kullanıcının kimlik bilgilerini gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-222">A website at another domain can send a signed-in user's credentials to the app on the user's behalf without the user's knowledge.</span></span> <!-- TODO Review: When using `AllowCredentials`, all CORS enabled domains must be trusted.
I don't like "all CORS enabled domains must be trusted", because it implies that if you're not using  `AllowCredentials`, domains don't need to be trusted. -->

<span data-ttu-id="49ecf-223">CORS belirtimi Ayrıca bu ayar durumları için kaynakları `"*"` (tüm kaynaklar) geçersiz, `Access-Control-Allow-Credentials` başlığı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-223">The CORS specification also states that setting origins to `"*"` (all origins) is invalid if the `Access-Control-Allow-Credentials` header is present.</span></span>

### <a name="preflight-requests"></a><span data-ttu-id="49ecf-224">Denetim öncesi isteği</span><span class="sxs-lookup"><span data-stu-id="49ecf-224">Preflight requests</span></span>

<span data-ttu-id="49ecf-225">Bazı CORS istekleri için tarayıcı, gerçek isteği yapmadan önce ek bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-225">For some CORS requests, the browser sends an additional request before making the actual request.</span></span> <span data-ttu-id="49ecf-226">Bu istek adında bir *denetim öncesi isteği*.</span><span class="sxs-lookup"><span data-stu-id="49ecf-226">This request is called a *preflight request*.</span></span> <span data-ttu-id="49ecf-227">Aşağıdaki koşullar doğruysa, tarayıcının denetim öncesi isteği atlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49ecf-227">The browser can skip the preflight request if the following conditions are true:</span></span>

* <span data-ttu-id="49ecf-228">İstek yöntemini GET, HEAD veya POST ' dir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-228">The request method is GET, HEAD, or POST.</span></span>
* <span data-ttu-id="49ecf-229">Uygulama dışında istek üst bilgilerini ayarlayıp ayarlamadığını `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, veya `Last-Event-ID`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-229">The app doesn't set request headers other than `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, or `Last-Event-ID`.</span></span>
* <span data-ttu-id="49ecf-230">`Content-Type` Üst bilgi, ayarla, aşağıdaki değerlerden birine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-230">The `Content-Type` header, if set, has one of the following values:</span></span>
  * `application/x-www-form-urlencoded`
  * `multipart/form-data`
  * `text/plain`

<span data-ttu-id="49ecf-231">İstek üstbilgileri kural kümesi çağırarak uygulama ayarlar üst bilgileri istemci isteği uygulandığı için `setRequestHeader` üzerinde `XMLHttpRequest` nesne.</span><span class="sxs-lookup"><span data-stu-id="49ecf-231">The rule on request headers set for the client request applies to headers that the app sets by calling `setRequestHeader` on the `XMLHttpRequest` object.</span></span> <span data-ttu-id="49ecf-232">Bu üst CORS belirtimi çağırır *yazar, istek üst bilgilerini*.</span><span class="sxs-lookup"><span data-stu-id="49ecf-232">The CORS specification calls these headers *author request headers*.</span></span> <span data-ttu-id="49ecf-233">Tarayıcı ayarlayabilir, gibi üstbilgileri kuralı uygulanmaz `User-Agent`, `Host`, veya `Content-Length`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-233">The rule doesn't apply to headers the browser can set, such as `User-Agent`, `Host`, or `Content-Length`.</span></span>

<span data-ttu-id="49ecf-234">Denetim öncesi isteğinin bir örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-234">The following is an example of a preflight request:</span></span>

```
OPTIONS https://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: https://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

<span data-ttu-id="49ecf-235">Uçuş öncesi isteğinin HTTP OPTIONS yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-235">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="49ecf-236">Bu, iki özel üst bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-236">It includes two special headers:</span></span>

* <span data-ttu-id="49ecf-237">`Access-Control-Request-Method`: Fiili istek için kullanılacak HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="49ecf-237">`Access-Control-Request-Method`: The HTTP method that will be used for the actual request.</span></span>
* <span data-ttu-id="49ecf-238">`Access-Control-Request-Headers`: Uygulamayı gerçek istekte ayarlar istek üst bilgilerini içeren bir liste.</span><span class="sxs-lookup"><span data-stu-id="49ecf-238">`Access-Control-Request-Headers`: A list of request headers that the app sets on the actual request.</span></span> <span data-ttu-id="49ecf-239">Daha önce belirtildiği gibi bu tarayıcı ayarlar, aşağıdaki gibi üst bilgiler içermez `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-239">As stated earlier, this doesn't include headers that the browser sets, such as `User-Agent`.</span></span>

<span data-ttu-id="49ecf-240">CORS denetim öncesi isteği içerebilir bir `Access-Control-Request-Headers` üst bilgi sunucuya gerçek isteğiyle gönderilen üst bilgiler gösterir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-240">A CORS preflight request might include an `Access-Control-Request-Headers` header, which indicates to the server the headers that are sent with the actual request.</span></span>

<span data-ttu-id="49ecf-241">Özel üst bilgiler izin vermek için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-241">To allow specific headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=55-60&highlight=5)]

<span data-ttu-id="49ecf-242">Tüm istek üstbilgilerini Yazar izin vermek için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-242">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=64-69&highlight=5)]

<span data-ttu-id="49ecf-243">Bunlar nasıl kümesinde tamamen tutarlı olmayan tarayıcıları `Access-Control-Request-Headers`.</span><span class="sxs-lookup"><span data-stu-id="49ecf-243">Browsers aren't entirely consistent in how they set `Access-Control-Request-Headers`.</span></span> <span data-ttu-id="49ecf-244">Üst bilgileri için herhangi bir şey dışında ayarlarsanız `"*"` (veya <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>), en az içermelidir `Accept`, `Content-Type`, ve `Origin`, artı, desteklemek istediğiniz tüm özel üst.</span><span class="sxs-lookup"><span data-stu-id="49ecf-244">If you set headers to anything other than `"*"` (or use <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>), you should include at least `Accept`, `Content-Type`, and `Origin`, plus any custom headers that you want to support.</span></span>

<span data-ttu-id="49ecf-245">(Sunucu isteği izin varsayılarak) denetim öncesi isteği için bir örnek yanıt aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-245">The following is an example response to the preflight request (assuming that the server allows the request):</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

<span data-ttu-id="49ecf-246">Yanıt içeren bir `Access-Control-Allow-Methods` izin verilen yöntemleri listeleyen üst bilgi ve isteğe bağlı olarak bir `Access-Control-Allow-Headers` izin verilen üstbilgileri listeleyen üst bilgisi.</span><span class="sxs-lookup"><span data-stu-id="49ecf-246">The response includes an `Access-Control-Allow-Methods` header that lists the allowed methods and optionally an `Access-Control-Allow-Headers` header, which lists the allowed headers.</span></span> <span data-ttu-id="49ecf-247">Denetim öncesi isteği başarıyla sonuçlanırsa, tarayıcı gerçek isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-247">If the preflight request succeeds, the browser sends the actual request.</span></span>

<span data-ttu-id="49ecf-248">Denetim öncesi isteği reddedilirse, uygulamayı döndürür bir *200 Tamam* yanıt geri CORS üst bilgileri göndermez ancak.</span><span class="sxs-lookup"><span data-stu-id="49ecf-248">If the preflight request is denied, the app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="49ecf-249">Bu nedenle, tarayıcının çıkış noktaları arası istek çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-249">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

### <a name="set-the-preflight-expiration-time"></a><span data-ttu-id="49ecf-250">Denetim öncesi sona erme saati ayarla</span><span class="sxs-lookup"><span data-stu-id="49ecf-250">Set the preflight expiration time</span></span>

<span data-ttu-id="49ecf-251">`Access-Control-Max-Age` Üstbilgisini belirtir ne kadar süreyle denetim öncesi isteğin yanıtını önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-251">The `Access-Control-Max-Age` header specifies how long the response to the preflight request can be cached.</span></span> <span data-ttu-id="49ecf-252">Bu başlık ayarlamak için çağrı <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span><span class="sxs-lookup"><span data-stu-id="49ecf-252">To set this header, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=91-96&highlight=5)]

<a name="how-cors"></a>

## <a name="how-cors-works"></a><span data-ttu-id="49ecf-253">CORS nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="49ecf-253">How CORS works</span></span>

<span data-ttu-id="49ecf-254">Bu bölümde, ne açıklar bir [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) HTTP iletileri düzeyinde istek.</span><span class="sxs-lookup"><span data-stu-id="49ecf-254">This section describes what happens in a [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) request at the level of the HTTP messages.</span></span>

* <span data-ttu-id="49ecf-255">CORS olduğu **değil** bir güvenlik özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-255">CORS is **not** a security feature.</span></span> <span data-ttu-id="49ecf-256">CORS bir sunucunun gevşek bir aynı çıkış noktası İlkesi olanak W3C standart ' dir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-256">CORS is a W3C standard that allows a server to relax the same-origin policy.</span></span>
  * <span data-ttu-id="49ecf-257">Örneğin, kötü amaçlı bir aktör kullanabilirsiniz [önlemek siteler arası betik (XSS)](xref:security/cross-site-scripting) sitenize karşı ve bilgilerini çalmak için siteler arası istek kendi CORS etkin siteye yürütün.</span><span class="sxs-lookup"><span data-stu-id="49ecf-257">For example, a malicious actor could use [Prevent Cross-Site Scripting (XSS)](xref:security/cross-site-scripting) against your site and execute a cross-site request to their CORS enabled site to steal information.</span></span>
* <span data-ttu-id="49ecf-258">CORS vererek özelliği API'nizi güvenli değil.</span><span class="sxs-lookup"><span data-stu-id="49ecf-258">Your API is not safer by allowing CORS.</span></span>
  * <span data-ttu-id="49ecf-259">İstemci (tarayıcı) CORS zorunlu aittir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-259">It's up to the client (browser) to enforce CORS.</span></span> <span data-ttu-id="49ecf-260">Sunucusu isteği yürütür ve yanıtı döndürür, hata ve blokları yanıtı döndürür istemcidir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-260">The server executes the request and returns the response, it's the client that returns an error and blocks the response.</span></span> <span data-ttu-id="49ecf-261">Örneğin, aşağıdaki araçlardan herhangi birini sunucu yanıtı görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-261">For example, any of the following tools will display the server response:</span></span>
     * [<span data-ttu-id="49ecf-262">Fiddler</span><span class="sxs-lookup"><span data-stu-id="49ecf-262">Fiddler</span></span>](https://www.telerik.com/fiddler)
     * [<span data-ttu-id="49ecf-263">Postman</span><span class="sxs-lookup"><span data-stu-id="49ecf-263">Postman</span></span>](https://www.getpostman.com/)
     * [<span data-ttu-id="49ecf-264">.NET HttpClient</span><span class="sxs-lookup"><span data-stu-id="49ecf-264">.NET HttpClient</span></span>](/dotnet/csharp/tutorials/console-webapiclient)
     * <span data-ttu-id="49ecf-265">Adres çubuğuna URL'yi girerek bir web tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-265">A web browser by entering the URL in the address bar.</span></span>
* <span data-ttu-id="49ecf-266">Bir çıkış noktaları arası yürütmek için bir yol tarayıcılar izin vermek bir sunucu için olan [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) veya [Fetch API'sini](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) aksi alınamaz istek.</span><span class="sxs-lookup"><span data-stu-id="49ecf-266">It's a way for a server to allow browsers to execute a cross-origin [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) or [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) request that otherwise would be forbidden.</span></span>
  * <span data-ttu-id="49ecf-267">Çıkış noktaları arası istekleri (CORS) olmayan tarayıcıları yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="49ecf-267">Browsers (without CORS) can't do cross-origin requests.</span></span> <span data-ttu-id="49ecf-268">CORS önce [JSONP](https://www.w3schools.com/js/js_json_jsonp.asp) bu kısıtlama aşmak için kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="49ecf-268">Before CORS, [JSONP](https://www.w3schools.com/js/js_json_jsonp.asp) was used to circumvent this restriction.</span></span> <span data-ttu-id="49ecf-269">JSONP XHR kullanmaz, kullandığı `<script>` yanıtını almak için etiket.</span><span class="sxs-lookup"><span data-stu-id="49ecf-269">JSONP doesn't use XHR, it uses the `<script>` tag to receive the response.</span></span> <span data-ttu-id="49ecf-270">Betikleri yüklenen çıkış noktaları arası izin verilir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-270">Scripts are allowed to be loaded cross-origin.</span></span>

<span data-ttu-id="49ecf-271">[CORS belirtimi]() çıkış noktaları arası istekleri etkinleştirme birkaç yeni HTTP üstbilgileri sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="49ecf-271">The [CORS specification]() introduced several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="49ecf-272">Bir tarayıcı CORS destekliyorsa, bu üstbilgileri çıkış noktaları arası istekleri için otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="49ecf-272">If a browser supports CORS, it sets these headers automatically for cross-origin requests.</span></span> <span data-ttu-id="49ecf-273">Özel JavaScript kodu, CORS'yi etkinleştirmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-273">Custom JavaScript code isn't required to enable CORS.</span></span>

<span data-ttu-id="49ecf-274">Çıkış noktaları arası isteğinin bir örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="49ecf-274">The following is an example of a cross-origin request.</span></span> <span data-ttu-id="49ecf-275">`Origin` Üst bilgi isteği yapan site etki alanı sağlar:</span><span class="sxs-lookup"><span data-stu-id="49ecf-275">The `Origin` header provides the domain of the site that's making the request:</span></span>

```
GET https://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: https://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: https://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

<span data-ttu-id="49ecf-276">Sunucu isteği izin veriyorsa, bu ayarlar `Access-Control-Allow-Origin` yanıt üst bilgisi.</span><span class="sxs-lookup"><span data-stu-id="49ecf-276">If the server allows the request, it sets the `Access-Control-Allow-Origin` header in the response.</span></span> <span data-ttu-id="49ecf-277">Bu üst bilgi değeri ya da eşleşen `Origin` istekteki üstbilgi veya joker karakter değeri `"*"`, yani her türlü kaynağa izin verilir:</span><span class="sxs-lookup"><span data-stu-id="49ecf-277">The value of this header either matches the `Origin` header from the request or is the wildcard value `"*"`, meaning that any origin is allowed:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

<span data-ttu-id="49ecf-278">Yanıt içermiyorsa `Access-Control-Allow-Origin` üst bilgi çıkış noktaları arası istek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="49ecf-278">If the response doesn't include the `Access-Control-Allow-Origin` header, the cross-origin request fails.</span></span> <span data-ttu-id="49ecf-279">Özellikle, tarayıcının isteği izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="49ecf-279">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="49ecf-280">Sunucunun başarılı bir yanıt döndürürse bile, tarayıcı yanıtı istemci uygulamasının kullanımına yapmaz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-280">Even if the server returns a successful response, the browser doesn't make the response available to the client app.</span></span>

<a name="test"></a>

## <a name="test-cors"></a><span data-ttu-id="49ecf-281">CORS'yi test etme</span><span class="sxs-lookup"><span data-stu-id="49ecf-281">Test CORS</span></span>

<span data-ttu-id="49ecf-282">CORS test etmek için:</span><span class="sxs-lookup"><span data-stu-id="49ecf-282">To test CORS:</span></span>

1. <span data-ttu-id="49ecf-283">[Bir API projesi oluşturma](xref:tutorials/first-web-api).</span><span class="sxs-lookup"><span data-stu-id="49ecf-283">[Create an API project](xref:tutorials/first-web-api).</span></span> <span data-ttu-id="49ecf-284">Alternatif olarak, [örneği indirin](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cors/sample/Cors).</span><span class="sxs-lookup"><span data-stu-id="49ecf-284">Alternatively, you can [download the sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cors/sample/Cors).</span></span>
1. <span data-ttu-id="49ecf-285">Yaklaşımlardan biri bu belgeyi kullanarak CORS'yi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="49ecf-285">Enable CORS using one of the approaches in this document.</span></span> <span data-ttu-id="49ecf-286">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49ecf-286">For example:</span></span>

  [!code-csharp[](cors/sample/Cors/WebAPI/StartupTest.cs?name=snippet2&highlight=13-18)]
  
  > [!WARNING]
  > <span data-ttu-id="49ecf-287">`WithOrigins("https://localhost:<port>");` benzer şekilde bir örnek uygulamayı test etmek için yalnızca kullanılmalıdır [örnek kodu indirdikten](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/cors/sample/Cors).</span><span class="sxs-lookup"><span data-stu-id="49ecf-287">`WithOrigins("https://localhost:<port>");` should only be used for testing a sample app similar to the [download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/cors/sample/Cors).</span></span>

1. <span data-ttu-id="49ecf-288">(Razor sayfaları veya MVC) bir web uygulaması projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49ecf-288">Create a web app project (Razor Pages or MVC).</span></span> <span data-ttu-id="49ecf-289">Razor sayfaları örnek kullanır.</span><span class="sxs-lookup"><span data-stu-id="49ecf-289">The sample uses Razor Pages.</span></span> <span data-ttu-id="49ecf-290">API projesi olarak aynı çözüm içindeki web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-290">You can create the web app in the same solution as the API project.</span></span>
1. <span data-ttu-id="49ecf-291">Aşağıdaki vurgulanmış kodu ekleyin *Index.cshtml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="49ecf-291">Add the following highlighted code to the *Index.cshtml* file:</span></span>

  [!code-csharp[](cors/sample/Cors/ClientApp/Pages/Index2.cshtml?highlight=7-99)]

1. <span data-ttu-id="49ecf-292">Önceki kod içinde `url: 'https://<web app>.azurewebsites.net/api/values/1',` dağıtılan uygulamanın URL'siyle.</span><span class="sxs-lookup"><span data-stu-id="49ecf-292">In the preceding code, replace `url: 'https://<web app>.azurewebsites.net/api/values/1',` with the URL to the deployed app.</span></span>
1. <span data-ttu-id="49ecf-293">API projesini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="49ecf-293">Deploy the API project.</span></span> <span data-ttu-id="49ecf-294">Örneğin, [Azure'a dağıtma](xref:host-and-deploy/azure-apps/index).</span><span class="sxs-lookup"><span data-stu-id="49ecf-294">For example, [deploy to Azure](xref:host-and-deploy/azure-apps/index).</span></span>
1. <span data-ttu-id="49ecf-295">Masaüstünden Razor sayfaları veya MVC uygulamayı çalıştırın ve tıklayarak **Test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="49ecf-295">Run the Razor Pages or MVC app from the desktop and click on the **Test** button.</span></span> <span data-ttu-id="49ecf-296">Hata iletilerini gözden geçirmek için F12 araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="49ecf-296">Use the F12 tools to review error messages.</span></span>
1. <span data-ttu-id="49ecf-297">Localhost merkezinden kaldırın `WithOrigins` ve uygulamayı dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="49ecf-297">Remove the localhost origin from `WithOrigins` and deploy the app.</span></span> <span data-ttu-id="49ecf-298">Alternatif olarak, farklı bir bağlantı noktası ile istemci uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="49ecf-298">Alternatively, run the client app with a different port.</span></span> <span data-ttu-id="49ecf-299">Örneğin, Visual Studio'dan çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="49ecf-299">For example, run from Visual Studio.</span></span>
1. <span data-ttu-id="49ecf-300">İstemci uygulaması ile test edin.</span><span class="sxs-lookup"><span data-stu-id="49ecf-300">Test with the client app.</span></span> <span data-ttu-id="49ecf-301">CORS hatalarını hata döndürür, ancak hata iletisi, JavaScript için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="49ecf-301">CORS failures return an error, but the error message isn't available to JavaScript.</span></span> <span data-ttu-id="49ecf-302">Konsolu sekmesine, hatayı görmek için F12 araçlarındaki kullanın.</span><span class="sxs-lookup"><span data-stu-id="49ecf-302">Use the console tab in the F12 tools to see the error.</span></span> <span data-ttu-id="49ecf-303">Tarayıcıya bağlı olarak, bir hata (F12 araçları konsolunu) aşağıdakine benzer da alın:</span><span class="sxs-lookup"><span data-stu-id="49ecf-303">Depending on the browser, you get an error (in the F12 tools console) similar to the following:</span></span>

  * <span data-ttu-id="49ecf-304">Microsoft Edge kullanarak:</span><span class="sxs-lookup"><span data-stu-id="49ecf-304">Using Microsoft Edge:</span></span>

    <span data-ttu-id="49ecf-305">**SEC7120: [CORS] kaynağını 'https://localhost:44375'değil buldunuz mu'https://localhost:44375'Access-Control-Allow-Origin yanıtı üstbilgisi çıkış noktaları arası kaynak için' ın https://webapi.azurewebsites.net/api/values/1'.**</span><span class="sxs-lookup"><span data-stu-id="49ecf-305">**SEC7120: [CORS] The origin 'https://localhost:44375' did not find 'https://localhost:44375' in the Access-Control-Allow-Origin response header for cross-origin  resource at 'https://webapi.azurewebsites.net/api/values/1'.**</span></span>

  * <span data-ttu-id="49ecf-306">Chrome kullanarak:</span><span class="sxs-lookup"><span data-stu-id="49ecf-306">Using Chrome:</span></span>

    <span data-ttu-id="49ecf-307">**Erişim sırasında XMLHttpRequest 'https://webapi.azurewebsites.net/api/values/1'kaynaktan'https://localhost:44375' CORS İlkesi tarafından engellendi: İstenen kaynak üzerinde 'Access-Control-Allow-Origin' üst bilgi yok.**</span><span class="sxs-lookup"><span data-stu-id="49ecf-307">**Access to XMLHttpRequest at 'https://webapi.azurewebsites.net/api/values/1' from origin 'https://localhost:44375' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49ecf-308">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="49ecf-308">Additional resources</span></span>

* [<span data-ttu-id="49ecf-309">Çıkış noktaları arası kaynak paylaşımı (CORS)</span><span class="sxs-lookup"><span data-stu-id="49ecf-309">Cross-Origin Resource Sharing (CORS)</span></span>](https://developer.mozilla.org/docs/Web/HTTP/CORS)
