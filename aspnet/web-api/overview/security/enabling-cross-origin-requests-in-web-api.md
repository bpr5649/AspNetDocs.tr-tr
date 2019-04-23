---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2'de kaynaklar arası istekleri etkinleştirme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API'de çıkış noktaları arası kaynak paylaşımı (CORS) destekleyecek şekilde gösterilmektedir.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59403837"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="d0756-103">ASP.NET Web API 2'de kaynaklar arası istekleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d0756-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="d0756-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d0756-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="d0756-105">Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller.</span><span class="sxs-lookup"><span data-stu-id="d0756-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="d0756-106">Bu kısıtlama adlı *aynı çıkış noktası İlkesi*ve kötü amaçlı bir siteyi başka bir siteden hassas verileri okumasını önler.</span><span class="sxs-lookup"><span data-stu-id="d0756-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="d0756-107">Ancak, bazen, web API'si çağırma diğer sitelere izin vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0756-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="d0756-108">[Kaynağın kaynak paylaşımını çapraz](http://www.w3.org/TR/cors/) (CORS) olan gevşek bir aynı çıkış noktası ilkesi izin veren bir W3C standart.</span><span class="sxs-lookup"><span data-stu-id="d0756-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="d0756-109">CORS kullanarak, bir sunucu açıkça bazı çıkış noktaları arası istekleri izin verirken diğerlerini.</span><span class="sxs-lookup"><span data-stu-id="d0756-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="d0756-110">CORS güvenli ve önceki teknikler daha esnek gibi [JSONP](http://en.wikipedia.org/wiki/JSONP).</span><span class="sxs-lookup"><span data-stu-id="d0756-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="d0756-111">Bu öğreticide, Web API uygulamanıza CORS'yi etkinleştirme işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0756-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="d0756-112">Bu öğreticide kullanılan yazılım</span><span class="sxs-lookup"><span data-stu-id="d0756-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="d0756-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0756-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="d0756-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="d0756-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="d0756-115">Giriş</span><span class="sxs-lookup"><span data-stu-id="d0756-115">Introduction</span></span>

<span data-ttu-id="d0756-116">Bu öğreticide, ASP.NET Web API CORS desteği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0756-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="d0756-117">– "Web API denetleyicisi barındıran, bir çağrılan Web hizmetini" ve "Web hizmetini çağıran diğer adlı WebClient", iki ASP.NET projesi oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="d0756-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="d0756-118">İki uygulama farklı etki alanlarında barındırıldığından, WebClient bir AJAX isteği WebService çıkış noktaları arası isteğidir.</span><span class="sxs-lookup"><span data-stu-id="d0756-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="d0756-119">"Aynı kaynak" nedir?</span><span class="sxs-lookup"><span data-stu-id="d0756-119">What is "same origin"?</span></span>

<span data-ttu-id="d0756-120">Aynı düzeni, konaklar ve bağlantı noktaları varsa iki URL aynı kaynağa sahip.</span><span class="sxs-lookup"><span data-stu-id="d0756-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="d0756-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="d0756-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="d0756-122">Bu iki URL aynı kaynağa sahip:</span><span class="sxs-lookup"><span data-stu-id="d0756-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="d0756-123">Bu URL'ler önceki değerinden farklı kaynakları iki vardır:</span><span class="sxs-lookup"><span data-stu-id="d0756-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="d0756-124">`http://example.net` -Farklı bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="d0756-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="d0756-125">`http://example.com:9000/foo.html` -Farklı bir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="d0756-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="d0756-126">`https://example.com/foo.html` -Farklı düzeni</span><span class="sxs-lookup"><span data-stu-id="d0756-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="d0756-127">`http://www.example.com/foo.html` -Farklı bir alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="d0756-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="d0756-128">Internet Explorer bağlantı noktası kaynakları karşılaştırılırken göz önünde bulundurmaz.</span><span class="sxs-lookup"><span data-stu-id="d0756-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="d0756-129">Web hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0756-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="d0756-130">Bu bölümde, Web API projeleri oluşturma bildiğiniz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="d0756-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="d0756-131">Aksi takdirde bkz [ASP.NET Web API'si ile çalışmaya başlama](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="d0756-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="d0756-132">Visual Studio'yu başlatın ve yeni bir **ASP.NET Web uygulaması (.NET Framework)** proje.</span><span class="sxs-lookup"><span data-stu-id="d0756-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="d0756-133">İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda **boş** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="d0756-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="d0756-134">Altında **klasörleri ekleyin ve çekirdek başvuruları**seçin **Web API** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0756-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio'da yeni ASP.NET projesi iletişim kutusu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="d0756-136">Adlı bir Web API denetleyicisi ekleme `TestController` aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="d0756-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="d0756-137">Uygulamayı yerel olarak çalıştırmak veya Azure'a dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d0756-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="d0756-138">(Ekran görüntüleri için Bu öğreticide, Azure App Service Web Apps için uygulamayı dağıtır.) Web API'si çalıştığını doğrulamak için gidin `http://hostname/api/test/`burada *hostname* uygulamanın dağıtıldığı etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="d0756-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="d0756-139">Yanıt metni görmelisiniz &quot;alın: Sınama iletisi&quot;.</span><span class="sxs-lookup"><span data-stu-id="d0756-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![Web tarayıcı gösteren sınama iletisi](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="d0756-141">WebClient projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0756-141">Create the WebClient project</span></span>

1. <span data-ttu-id="d0756-142">Hesaplanmış sütun oluşturabiliriz **ASP.NET Web uygulaması (.NET Framework)** seçin ve proje **MVC** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="d0756-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="d0756-143">İsteğe bağlı olarak **kimlik doğrulamayı Değiştir** > **kimlik doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="d0756-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="d0756-144">Bu öğretici için kimlik doğrulaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0756-144">You don't need authentication for this tutorial.</span></span>

   ![Yeni ASP.NET projesi iletişim kutusunda Visual Studio'da MVC şablonu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="d0756-146">İçinde **Çözüm Gezgini**, dosyayı açma *Views/Home/Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d0756-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="d0756-147">Bu dosyadaki kodu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d0756-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="d0756-148">İçin *serviceUrl* değişkeni, Web hizmeti uygulama URI'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0756-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="d0756-149">WebClient uygulamayı yerel olarak çalıştırmak veya başka bir Web sitesine yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0756-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="d0756-150">"Try It" düğmesine tıkladığınızda, listelenen HTTP yöntemini kullanarak Web hizmeti uygulaması için bir AJAX isteği gönderilir açılan kutuda (GET, POST veya PUT).</span><span class="sxs-lookup"><span data-stu-id="d0756-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="d0756-151">Bu farklı çıkış noktaları arası istekleri incelemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="d0756-152">Şu anda düğmesine tıklarsanız bir hata alırsınız. Bu nedenle Web hizmeti uygulama CORS desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d0756-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![Tarayıcı 'try' hatası](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="d0756-154">Bir aracının HTTP trafiğini izleme hoşlanıyorsanız [Fiddler](https://www.telerik.com/fiddler), tarayıcı GET isteği gönderir ve isteğin başarılı ancak AJAX çağrısı bir hata döndürür görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d0756-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="d0756-155">Aynı çıkış noktası İlkesi tarayıcıdan engellemez anlaşılması önemlidir *gönderme* istek.</span><span class="sxs-lookup"><span data-stu-id="d0756-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="d0756-156">Bunun yerine, uygulama görmesini engeller *yanıt*.</span><span class="sxs-lookup"><span data-stu-id="d0756-156">Instead, it prevents the application from seeing the *response*.</span></span>

![Fiddler'ı web hata ayıklayıcısı Web istekleri gösteriliyor](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="d0756-158">CORS'yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d0756-158">Enable CORS</span></span>

<span data-ttu-id="d0756-159">Şimdi github'dan WebService uygulamada CORS'yi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="d0756-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="d0756-160">İlk olarak, CORS NuGet paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0756-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="d0756-161">Visual Studio'da gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="d0756-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d0756-162">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d0756-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="d0756-163">Bu komut, en son paketini yükler ve çekirdek Web API kitaplıkları dahil olmak üzere tüm bağımlılıkları güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d0756-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="d0756-164">Kullanım `-Version` belirli bir sürümü hedeflemek için bayrak.</span><span class="sxs-lookup"><span data-stu-id="d0756-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="d0756-165">CORS paketi, Web API 2.0 veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d0756-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="d0756-166">Dosyayı açmak *uygulama\_Start/WebApiConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="d0756-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="d0756-167">Aşağıdaki kodu ekleyin **WebApiConfig.Register** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d0756-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="d0756-168">Ardından, ekleme **[EnableCors]** özniteliğini `TestController` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="d0756-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="d0756-169">İçin *kaynakları* parametresi WebClient uygulamanın dağıtıldığı bir URI kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0756-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="d0756-170">Bu çıkış noktaları arası istekleri WebClient tüm diğer etki alanları arası istekleri engelleyerek hala çalışırken sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="d0756-171">Daha sonra parametrelerini açıklayacağız **[EnableCors]** daha ayrıntılı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="d0756-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="d0756-172">Sonunda eğik çizgi içermez *kaynakları* URL'si.</span><span class="sxs-lookup"><span data-stu-id="d0756-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="d0756-173">Güncelleştirilmiş WebService uygulamayı yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d0756-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="d0756-174">WebClient güncelleştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0756-174">You don't need to update WebClient.</span></span> <span data-ttu-id="d0756-175">WebClient AJAX isteği başarılı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0756-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="d0756-176">GET, PUT ve POST yöntemleri tüm izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-176">The GET, PUT, and POST methods are all allowed.</span></span>

![Web tarayıcı gösteren başarılı bir sınama iletisi](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="d0756-178">CORS nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d0756-178">How CORS Works</span></span>

<span data-ttu-id="d0756-179">Bu bölümde, HTTP iletileri düzeyinde bir CORS isteğinde ne açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0756-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="d0756-180">Böylece yapılandırabileceğiniz CORS nasıl çalıştığını anlamak önemlidir **[EnableCors]** doğru öznitelik ve beklediğiniz gibi şeyler çalışmazsa sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="d0756-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="d0756-181">CORS belirtimi çıkış noktaları arası istekleri etkinleştirme birkaç yeni HTTP üst bilgilerini ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d0756-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="d0756-182">Bir tarayıcı CORS destekliyorsa, bu üstbilgileri çıkış noktaları arası istekleri için otomatik olarak ayarlar; JavaScript kodunuza özel herhangi bir şey yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0756-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="d0756-183">Çıkış noktaları arası isteğinin bir örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0756-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="d0756-184">"Kaynak" üst bilgisi istekte site etki alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="d0756-185">Sunucu isteği izin veriyorsa, Access-Control-Allow-Origin üst bilgi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="d0756-186">Bu üst bilgi değeri ile eşleşen kaynak üst bilgisi ya da joker karakter değeri "\*", yani her türlü kaynağa izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="d0756-187">Access-Control-Allow-Origin üst bilgi yanıtı içermez AJAX isteği başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d0756-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="d0756-188">Özellikle, tarayıcının isteği izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="d0756-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="d0756-189">Tarayıcı yanıt, sunucunun başarılı bir yanıt döndürürse bile, istemci uygulama tarafından kullanılabilir yapmaz.</span><span class="sxs-lookup"><span data-stu-id="d0756-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="d0756-190">**Denetim öncesi isteği**</span><span class="sxs-lookup"><span data-stu-id="d0756-190">**Preflight Requests**</span></span>

<span data-ttu-id="d0756-191">Bazı CORS istekleri için tarayıcı kaynak gerçek isteği göndermeden önce bir "Denetim öncesi isteği" adlı ek bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0756-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="d0756-192">Aşağıdaki koşullar doğruysa, tarayıcının denetim öncesi isteği atlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0756-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="d0756-193">İstek yöntemini GET, HEAD veya sonrası, olan *ve*</span><span class="sxs-lookup"><span data-stu-id="d0756-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="d0756-194">Uygulama dışındaki içeriği kabul et, Accept-Language, dil, herhangi bir istek üst ayarlamaz Content-Type veya son-Event-ID *ve*</span><span class="sxs-lookup"><span data-stu-id="d0756-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="d0756-195">Content-Type üst bilgisi (varsa ayarlayın) aşağıdakilerden biridir:</span><span class="sxs-lookup"><span data-stu-id="d0756-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="d0756-196">Application/x-www-form-urlencoded işlemek</span><span class="sxs-lookup"><span data-stu-id="d0756-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="d0756-197">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="d0756-197">multipart/form-data</span></span>
    - <span data-ttu-id="d0756-198">metin/düz</span><span class="sxs-lookup"><span data-stu-id="d0756-198">text/plain</span></span>

<span data-ttu-id="d0756-199">Uygulama çağırarak ayarlar üst istek üst bilgileri hakkında kuralın uygulanacağı **setRequestHeader** üzerinde **XMLHttpRequest** nesne.</span><span class="sxs-lookup"><span data-stu-id="d0756-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="d0756-200">(Bu "Yazar istek üstbilgilerini" CORS belirtimi çağırır.) Kural üstbilgileri uygulanmaz *tarayıcı* kullanıcı aracısı, konak veya Content-Length gibi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0756-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="d0756-201">Denetim öncesi isteğinin bir örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0756-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="d0756-202">Uçuş öncesi isteğinin HTTP OPTIONS yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0756-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="d0756-203">Bu, iki özel üst bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="d0756-203">It includes two special headers:</span></span>

- <span data-ttu-id="d0756-204">Erişim-Control-Request-Method: Fiili istek için kullanılacak HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d0756-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="d0756-205">Access-Control-Request-Headers: İstek üst bilgilerinin bir listesi, *uygulama* gerçek istek üzerinde ayarlanan.</span><span class="sxs-lookup"><span data-stu-id="d0756-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="d0756-206">(Yeniden, bu tarayıcı ayarlar üst bilgileri içermez.)</span><span class="sxs-lookup"><span data-stu-id="d0756-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="d0756-207">Sunucunun isteği izin varsayılarak bir yanıt örneği, şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="d0756-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="d0756-208">Yanıt, izin verilen yöntemleri listeleyen bir erişim-denetim-Allow-Methods üst bilgisi ve isteğe bağlı olarak izin verilen üstbilgileri listeleyen bir Access-Control-izin ver-Headers üstbilgisi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d0756-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="d0756-209">Denetim öncesi isteği başarıyla sonuçlanırsa, tarayıcı daha önce açıklandığı gibi gerçek bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0756-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="d0756-210">Uç nokta denetim öncesi OPTIONS istekleri ile test etmek için yaygın olarak kullanılan araçlar (örneğin, [Fiddler](https://www.telerik.com/fiddler) ve [Postman](https://www.getpostman.com/)) varsayılan olarak gerekli seçenekleri üst bilgileri gönderme.</span><span class="sxs-lookup"><span data-stu-id="d0756-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="d0756-211">Onaylayın `Access-Control-Request-Method` ve `Access-Control-Request-Headers` üstbilgileri, istekle birlikte gönderilir ve Seçenekler üst bilgileri uygulama IIS üzerinden ulaşın.</span><span class="sxs-lookup"><span data-stu-id="d0756-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="d0756-212">IIS almak ve seçeneği isteklerini işlemek bir ASP.NET uygulaması izin verecek şekilde yapılandırmak için aşağıdaki yapılandırma uygulamanın ekleme *web.config* dosyası `<system.webServer><handlers>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="d0756-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="d0756-213">Kaldırılmasını `OPTIONSVerbHandler` IIS OPTIONS istekleri işleme öğesinden engeller.</span><span class="sxs-lookup"><span data-stu-id="d0756-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="d0756-214">Adlandırılan `ExtensionlessUrlHandler-Integrated-4.0` OPTIONS istekleri varsayılan modülün kaydını yalnızca GET, HEAD, POST ve hata ayıklama isteği uzantısız URL'lerle izin verdiğinden, uygulamanıza ulaşmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="d0756-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="d0756-215">Kapsam kuralları [EnableCors] için</span><span class="sxs-lookup"><span data-stu-id="d0756-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="d0756-216">Uygulamanızdaki her eylem, denetleyici başına veya genel olarak tüm Web APİ'si denetleyicilerinin için CORS etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0756-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="d0756-217">**Eylem başına**</span><span class="sxs-lookup"><span data-stu-id="d0756-217">**Per Action**</span></span>

<span data-ttu-id="d0756-218">Tek bir eylem için CORS etkinleştirmek için ayarlayın **[EnableCors]** özniteliği eylem yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d0756-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="d0756-219">Aşağıdaki örnek için CORS `GetItem` yalnızca yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d0756-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="d0756-220">**Denetleyici**</span><span class="sxs-lookup"><span data-stu-id="d0756-220">**Per Controller**</span></span>

<span data-ttu-id="d0756-221">Ayarlarsanız **[EnableCors]** denetleyici sınıfı üzerinde denetleyicinin tüm eylemleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0756-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="d0756-222">Bir eylem için CORS devre dışı bırakmak için ekleme **[DisableCors]** eyleme özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d0756-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="d0756-223">Aşağıdaki örnek her yöntemi dışında için CORS sağlar `PutItem`.</span><span class="sxs-lookup"><span data-stu-id="d0756-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="d0756-224">**Genel olarak**</span><span class="sxs-lookup"><span data-stu-id="d0756-224">**Globally**</span></span>

<span data-ttu-id="d0756-225">Uygulamanızdaki tüm Web APİ'si denetleyicilerinin CORS'yi etkinleştirmek için geçirmek bir **EnableCorsAttribute** için örnek **EnableCors** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d0756-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="d0756-226">Birden fazla kapsamda öznitelik ayarlanırsa, öncelik sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d0756-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="d0756-227">Eylem</span><span class="sxs-lookup"><span data-stu-id="d0756-227">Action</span></span>
2. <span data-ttu-id="d0756-228">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="d0756-228">Controller</span></span>
3. <span data-ttu-id="d0756-229">Global</span><span class="sxs-lookup"><span data-stu-id="d0756-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="d0756-230">İzin verilen çıkış noktaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0756-230">Set the allowed origins</span></span>

<span data-ttu-id="d0756-231">*Kaynakları* parametresinin **[EnableCors]** özniteliği belirtir kaynağa erişmek için hangi çıkış noktaları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="d0756-232">İzin verilen çıkış noktaları, virgülle ayrılmış listesini değerdir.</span><span class="sxs-lookup"><span data-stu-id="d0756-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="d0756-233">Joker karakter değeri de kullanabilirsiniz "\*" tüm kaynaklar gelen isteklere izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="d0756-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="d0756-234">Her türlü kaynağa gelen isteklere izin vermeden önce dikkatlice düşünün.</span><span class="sxs-lookup"><span data-stu-id="d0756-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="d0756-235">Bu, tam anlamıyla herhangi bir Web sitesinde Web API AJAX çağrıları yapabileceğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d0756-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="d0756-236">İzin verilen HTTP yöntemleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="d0756-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="d0756-237">*Yöntemleri* parametresinin **[EnableCors]** özniteliği belirtir kaynağa erişmek için hangi HTTP yöntemlerine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="d0756-238">Tüm yöntemlere izin için joker karakter değeri kullanın. "\*".</span><span class="sxs-lookup"><span data-stu-id="d0756-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="d0756-239">Aşağıdaki örnek yalnızca GET ve POST istekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="d0756-240">İzin verilen istek üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="d0756-240">Set the allowed request headers</span></span>

<span data-ttu-id="d0756-241">Daha önce nasıl bir denetim öncesi isteği uygulama tarafından ayarlanıp HTTP üst bilgileri listeleyen bir Access-Control-Request-Headers üstbilgisi içeriyor olabilir, bu makalede açıklanan (Malum "yazar, istek üst bilgileri").</span><span class="sxs-lookup"><span data-stu-id="d0756-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="d0756-242">*Üstbilgileri* parametresinin **[EnableCors]** özniteliği belirtir hangi yazar istek üst bilgiye izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="d0756-243">Üst bilgileri izin verecek şekilde ayarlanmış *üstbilgileri* için "\*".</span><span class="sxs-lookup"><span data-stu-id="d0756-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="d0756-244">Beyaz liste belirli üstbilgileri için ayarlanmış *üstbilgileri* izin verilen üstbilgileri virgülle ayrılmış bir listesi için:</span><span class="sxs-lookup"><span data-stu-id="d0756-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="d0756-245">Ancak, tarayıcılar nasıl bunlar Access-Control-Request-Headers kümesinde tamamen tutarlı değil.</span><span class="sxs-lookup"><span data-stu-id="d0756-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="d0756-246">Örneğin, Chrome, şu anda "Başlangıç" içerir.</span><span class="sxs-lookup"><span data-stu-id="d0756-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="d0756-247">Bile uygulama bunları betikte ayarladığında FireFox "Kabul et" gibi standart başlıklarını içermez.</span><span class="sxs-lookup"><span data-stu-id="d0756-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="d0756-248">Ayarlarsanız *üstbilgileri* dışında herhangi bir şey için "\*", "kabul", "content-type" ve "Başlangıç" yanı sıra, desteklemek istediğiniz tüm özel üst en az içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d0756-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="d0756-249">İzin verilen yanıt üstbilgilerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="d0756-249">Set the allowed response headers</span></span>

<span data-ttu-id="d0756-250">Varsayılan olarak, tarayıcı tüm yanıt üstbilgilerini uygulamaya kullanıma sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="d0756-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="d0756-251">Varsayılan olarak kullanılabilir olan yanıt üstbilgilerini şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d0756-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="d0756-252">Önbellek denetimi</span><span class="sxs-lookup"><span data-stu-id="d0756-252">Cache-Control</span></span>
- <span data-ttu-id="d0756-253">İçerik dili</span><span class="sxs-lookup"><span data-stu-id="d0756-253">Content-Language</span></span>
- <span data-ttu-id="d0756-254">İçerik Türü</span><span class="sxs-lookup"><span data-stu-id="d0756-254">Content-Type</span></span>
- <span data-ttu-id="d0756-255">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="d0756-255">Expires</span></span>
- <span data-ttu-id="d0756-256">Son değiştirilme</span><span class="sxs-lookup"><span data-stu-id="d0756-256">Last-Modified</span></span>
- <span data-ttu-id="d0756-257">Pragma</span><span class="sxs-lookup"><span data-stu-id="d0756-257">Pragma</span></span>

<span data-ttu-id="d0756-258">CORS spec bu çağrıları [basit yanıt üstbilgilerini](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span><span class="sxs-lookup"><span data-stu-id="d0756-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="d0756-259">Diğer üst bilgileri uygulama için kullanılabilir hale getirmek için ayarlanmış *exposedHeaders* parametresinin **[EnableCors]**.</span><span class="sxs-lookup"><span data-stu-id="d0756-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="d0756-260">Aşağıdaki örnekte, denetleyici 's `Get` yöntemi 'X-Custom-Header' adlı bir özel üst bilgi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0756-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="d0756-261">Varsayılan olarak, tarayıcı bu çıkış noktaları arası istek üstbilgisinde açığa çıkarmamak.</span><span class="sxs-lookup"><span data-stu-id="d0756-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="d0756-262">Üst bilgi kullanılabilir hale getirmek için 'X-Custom-Header' dahil *exposedHeaders*.</span><span class="sxs-lookup"><span data-stu-id="d0756-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="d0756-263">Çıkış noktaları arası istekleri Pass kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="d0756-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="d0756-264">Özel işleme bir CORS isteğinde kimlik bilgilerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d0756-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="d0756-265">Varsayılan olarak, tarayıcının çıkış noktaları arası istek ile herhangi bir kimlik bilgisi göndermez.</span><span class="sxs-lookup"><span data-stu-id="d0756-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="d0756-266">Kimlik bilgileri, tanımlama bilgilerinin yanı sıra HTTP kimlik doğrulama düzenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d0756-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="d0756-267">İstemci kimlik bilgileriyle bir çıkış noktaları arası istek göndermek için ayarlamalısınız **XMLHttpRequest.withCredentials** true.</span><span class="sxs-lookup"><span data-stu-id="d0756-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="d0756-268">Kullanarak **XMLHttpRequest** doğrudan:</span><span class="sxs-lookup"><span data-stu-id="d0756-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="d0756-269">JQuery içinde:</span><span class="sxs-lookup"><span data-stu-id="d0756-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="d0756-270">Ayrıca, sunucunun kimlik bilgilerini izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0756-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="d0756-271">Web API'de çıkış noktaları arası kimlik bilgileri'izin verecek şekilde ayarlanmış **SupportsCredentials** özelliğini true olarak **[EnableCors]** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="d0756-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="d0756-272">Bu özellik true ise, HTTP yanıtı erişim-denetim-Allow-Credentials üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="d0756-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="d0756-273">Bu üst bilgi, tarayıcı sunucunun bir çıkış noktaları arası istek için kimlik bilgilerini sağlar söyler.</span><span class="sxs-lookup"><span data-stu-id="d0756-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="d0756-274">Tarayıcı bilgilerini gönderir, ancak yanıt, geçerli bir erişim-denetim-Allow-Credentials üst bilgisi içermez, tarayıcı uygulamaya yanıt açığa çıkarmamak ve AJAX isteği başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d0756-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="d0756-275">Ayar hakkında dikkatli olun **SupportsCredentials** başka bir etki alanındaki bir Web sitesi gönderebilir bir oturum açmış kullanıcı kimlik bilgilerini kullanıcının adına, Web API'niz için farkına varmadan kullanıcı anlamına geldiğinden, true.</span><span class="sxs-lookup"><span data-stu-id="d0756-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="d0756-276">CORS spec Ayrıca bu ayar durumları *kaynakları* için &quot; \* &quot; geçersiz olursa **SupportsCredentials** geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0756-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="d0756-277">CORS ilkesini sağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="d0756-277">Custom CORS policy providers</span></span>

<span data-ttu-id="d0756-278">**[EnableCors]** özniteliğini uygular **ICorsPolicyProvider** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="d0756-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="d0756-279">Türetilen bir sınıf oluşturarak kendi uygulamanız sağlayabilir **özniteliği** ve uygulayan **ICorsPolicyProvider**.</span><span class="sxs-lookup"><span data-stu-id="d0756-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="d0756-280">Artık tüm yerleştirme, koyabilirsiniz öznitelik uygulayabilirsiniz **[EnableCors]**.</span><span class="sxs-lookup"><span data-stu-id="d0756-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="d0756-281">Örneğin, özel bir CORS ilke sağlayıcısı, ayarlar yapılandırma dosyasından okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="d0756-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="d0756-282">Öznitelikleri kullanarak alternatif olarak, kaydedebileceğiniz bir **ICorsPolicyProviderFactory** oluşturan nesne **ICorsPolicyProvider** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="d0756-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="d0756-283">Ayarlanacak **ICorsPolicyProviderFactory**, çağrı **SetCorsPolicyProviderFactory** genişletme yöntemi aşağıdaki gibi başlangıçta:</span><span class="sxs-lookup"><span data-stu-id="d0756-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="d0756-284">Tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="d0756-284">Browser support</span></span>

<span data-ttu-id="d0756-285">Web API CORS, bir sunucu tarafı teknoloji paketidir.</span><span class="sxs-lookup"><span data-stu-id="d0756-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="d0756-286">Ayrıca kullanıcının tarayıcı CORS desteği gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0756-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="d0756-287">Neyse ki, tüm temel tarayıcılarda geçerli sürümleri dahil [desteklemek için CORS](http://caniuse.com/cors).</span><span class="sxs-lookup"><span data-stu-id="d0756-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
