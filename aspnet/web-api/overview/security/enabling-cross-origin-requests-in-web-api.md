---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2 ' de çapraz kaynak Isteklerini etkinleştirme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde, çıkış noktaları arası kaynak paylaşımı 'nı (CORS) nasıl desteklemenin gösterir.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555708"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="4e548-103">ASP.NET Web API 2 ' de çapraz kaynak isteklerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4e548-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="4e548-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4e548-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="4e548-105">Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller.</span><span class="sxs-lookup"><span data-stu-id="4e548-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="4e548-106">Bu kısıtlamaya *aynı-Origin ilkesi*adı verilir ve kötü amaçlı bir sitenin başka bir siteden hassas verileri okumasını önler.</span><span class="sxs-lookup"><span data-stu-id="4e548-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="4e548-107">Ancak, bazen diğer sitelerin Web API 'nizi çağırmasını sağlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="4e548-108">[Çapraz kaynak kaynak paylaşımı](http://www.w3.org/TR/cors/) (CORS), bir sunucunun aynı kaynak ilkeyi rahat bir şekilde sağlamasına olanak tanıyan bir W3C standardıdır.</span><span class="sxs-lookup"><span data-stu-id="4e548-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="4e548-109">CORS kullanarak, bir sunucu bazı çapraz kaynak isteklerine, diğerlerini reddetirken açık bir şekilde izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="4e548-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="4e548-110">CORS, [JSONP](http://en.wikipedia.org/wiki/JSONP)gibi önceki tekniklerin daha güvenli ve daha esnektir.</span><span class="sxs-lookup"><span data-stu-id="4e548-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="4e548-111">Bu öğreticide, Web API uygulamanızda CORS 'nin nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4e548-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="4e548-112">Öğreticide kullanılan yazılım</span><span class="sxs-lookup"><span data-stu-id="4e548-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="4e548-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e548-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="4e548-114">Web API 2,2</span><span class="sxs-lookup"><span data-stu-id="4e548-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="4e548-115">Giriş</span><span class="sxs-lookup"><span data-stu-id="4e548-115">Introduction</span></span>

<span data-ttu-id="4e548-116">Bu öğreticide, ASP.NET Web API 'sinde CORS desteği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4e548-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="4e548-117">Bir Web API denetleyicisi barındıran "WebService" adlı, diğeri de WebService 'yi çağıran "WebClient" adlı iki ASP.NET projesi oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="4e548-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="4e548-118">İki uygulama farklı etki alanlarında barındırıldığından, WebClient 'dan WebService 'a yönelik bir AJAX isteği bir çapraz kaynak isteği olur.</span><span class="sxs-lookup"><span data-stu-id="4e548-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="4e548-119">"Aynı kaynak" nedir?</span><span class="sxs-lookup"><span data-stu-id="4e548-119">What is "same origin"?</span></span>

<span data-ttu-id="4e548-120">Aynı şemalara, konaklara ve bağlantı noktalarına sahip olmaları durumunda iki URL aynı kaynağa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e548-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="4e548-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="4e548-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="4e548-122">Bu iki URL aynı kaynağa sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4e548-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="4e548-123">Bu URL 'Ler, önceki iki değerden farklı kaynaklardan farklıdır:</span><span class="sxs-lookup"><span data-stu-id="4e548-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="4e548-124">`http://example.net`-farklı etki alanı</span><span class="sxs-lookup"><span data-stu-id="4e548-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="4e548-125">`http://example.com:9000/foo.html`-farklı bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="4e548-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="4e548-126">`https://example.com/foo.html`-farklı düzen</span><span class="sxs-lookup"><span data-stu-id="4e548-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="4e548-127">`http://www.example.com/foo.html`-farklı alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="4e548-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="4e548-128">Internet Explorer, kaynakları karşılaştırırken bağlantı noktasını dikkate almaz.</span><span class="sxs-lookup"><span data-stu-id="4e548-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="4e548-129">WebService projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e548-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="4e548-130">Bu bölümde, Web API projeleri oluşturmayı bildiğiniz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4e548-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="4e548-131">Aksi takdirde, bkz. [ASP.NET Web API 'si Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="4e548-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="4e548-132">Visual Studio 'Yu başlatın ve yeni bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e548-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="4e548-133">**Yeni ASP.NET Web uygulaması** Iletişim kutusunda **boş** proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="4e548-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="4e548-134">**Klasör ve temel başvuru Ekle**' nin altında **Web API** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="4e548-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio 'da yeni ASP.NET Project iletişim kutusu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="4e548-136">Aşağıdaki kodla `TestController` adlı bir Web API denetleyicisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4e548-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="4e548-137">Uygulamayı yerel olarak çalıştırabilir veya Azure 'a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="4e548-138">(Bu öğreticideki ekran görüntüleri için, uygulama Azure App Service Web Apps dağıtılır.) Web API 'sinin çalıştığını doğrulamak için, *ana bilgisayar adının* uygulamayı dağıttığınız etki alanı olduğu `http://hostname/api/test/`' a gidin.</span><span class="sxs-lookup"><span data-stu-id="4e548-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="4e548-139">&quot;al: test Iletisi&quot;yanıt metnini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e548-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![Sınama iletisini gösteren Web tarayıcısı](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="4e548-141">WebClient projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e548-141">Create the WebClient project</span></span>

1. <span data-ttu-id="4e548-142">Başka bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun ve **MVC** proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="4e548-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="4e548-143">İsteğe bağlı olarak \*\*, kimlik doğrulaması > \*\* **kimlik doğrulamasını Değiştir** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="4e548-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="4e548-144">Bu öğretici için kimlik doğrulamaya gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="4e548-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio 'da yeni ASP.NET proje iletişim kutusunda MVC şablonu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="4e548-146">**Çözüm Gezgini**' de, *Görünümler/Home/Index. cshtml*dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="4e548-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="4e548-147">Bu dosyadaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4e548-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="4e548-148">*ServiceUrl* değişkeni için WEBSERVICE uygulamasının URI 'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e548-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="4e548-149">WebClient uygulamasını yerel olarak çalıştırın veya başka bir Web sitesinde yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="4e548-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="4e548-150">"Dene" düğmesine tıkladığınızda, Web hizmeti uygulamasına açılan kutuda listelenen HTTP yöntemi kullanılarak bir AJAX isteği gönderilir (GET, POST veya PUT).</span><span class="sxs-lookup"><span data-stu-id="4e548-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="4e548-151">Bu, farklı çapraz kaynak isteklerini incelemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e548-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="4e548-152">Şu anda, Web hizmeti uygulaması CORS 'yi desteklemez, bu nedenle düğmeye tıkladığınızda bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="4e548-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![Tarayıcıda ' deneyin ' hatası](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="4e548-154">HTTP trafiğini [Fiddler](https://www.telerik.com/fiddler)gibi bir araçta izleyebilirsiniz, tarayıcının get isteğini göndereceğini ve isteğin başarılı olduğunu, ancak Ajax çağrısının bir hata döndürdüğünü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4e548-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="4e548-155">Aynı kaynak ilkenin tarayıcının isteği *göndermesini* önleyemediğinden emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4e548-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="4e548-156">Bunun yerine, uygulamanın *yanıtı*görmesini önler.</span><span class="sxs-lookup"><span data-stu-id="4e548-156">Instead, it prevents the application from seeing the *response*.</span></span>

![Web isteklerini gösteren Fiddler Web hata ayıklayıcısı](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="4e548-158">CORS'yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4e548-158">Enable CORS</span></span>

<span data-ttu-id="4e548-159">Şimdi WebService uygulamasında CORS 'yi etkinleştirelim.</span><span class="sxs-lookup"><span data-stu-id="4e548-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="4e548-160">İlk olarak CORS NuGet paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e548-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="4e548-161">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="4e548-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4e548-162">Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="4e548-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="4e548-163">Bu komut, en son paketi yüklenir ve çekirdek Web API kitaplıkları da dahil olmak üzere tüm bağımlılıkları günceller.</span><span class="sxs-lookup"><span data-stu-id="4e548-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="4e548-164">Belirli bir sürümü hedeflemek için `-Version` bayrağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e548-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="4e548-165">CORS paketi için Web API 2,0 veya üzeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e548-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="4e548-166">*Start/WebApiConfig. cs\_dosya uygulamasını*açın.</span><span class="sxs-lookup"><span data-stu-id="4e548-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="4e548-167">**WebApiConfig. Register** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4e548-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="4e548-168">Sonra, `TestController` sınıfına **[Enablecors]** özniteliğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4e548-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="4e548-169">*Kaynakları* parametresi Için, WebClient UYGULAMASıNı dağıttığınız URI 'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e548-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="4e548-170">Bu, aynı zamanda diğer tüm etki alanları arası isteklere izin verdiğinden WebClient kaynaklı çapraz kaynak isteklerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="4e548-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="4e548-171">Daha sonra, **[Enablecors]** parametrelerini daha ayrıntılı olarak açıklayacağım.</span><span class="sxs-lookup"><span data-stu-id="4e548-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="4e548-172">*Çıkış* URL 'sinin sonuna eğik çizgi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="4e548-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="4e548-173">Güncelleştirilmiş Web hizmeti uygulamasını yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4e548-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="4e548-174">WebClient 'ı güncelleştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4e548-174">You don't need to update WebClient.</span></span> <span data-ttu-id="4e548-175">Şimdi WebClient 'daki AJAX isteği başarılı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e548-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="4e548-176">GET, PUT ve POST yöntemlerine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4e548-176">The GET, PUT, and POST methods are all allowed.</span></span>

![Başarılı sınama iletisini gösteren Web tarayıcısı](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="4e548-178">CORS nasıl kullanılır?</span><span class="sxs-lookup"><span data-stu-id="4e548-178">How CORS Works</span></span>

<span data-ttu-id="4e548-179">Bu bölümde, HTTP iletileri düzeyinde bir CORS isteğinde ne olacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4e548-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="4e548-180">CORS 'nin nasıl çalıştığını anlamak önemlidir. böylece, **[Enablecors]** özniteliğini doğru şekilde yapılandırabilir ve her şeyin beklendiği gibi çalışmadığına sorun giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="4e548-181">CORS belirtimi, çıkış noktaları arası istekleri etkinleştiren birkaç yeni HTTP üst bilgisi sunar.</span><span class="sxs-lookup"><span data-stu-id="4e548-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="4e548-182">Bir tarayıcı CORS 'yi destekliyorsa, bu üst bilgileri, çıkış noktaları arası istekler için otomatik olarak ayarlar; JavaScript kodunuzda özel bir şey yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4e548-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="4e548-183">Bir çapraz kaynak isteğine bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4e548-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="4e548-184">"Origin" üstbilgisi, isteği yapan sitenin etki alanını verir.</span><span class="sxs-lookup"><span data-stu-id="4e548-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="4e548-185">Sunucu isteğe izin veriyorsa, erişim-denetim-Izin-kaynak üst bilgisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4e548-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="4e548-186">Bu üstbilginin değeri, kaynak üstbilgisiyle eşleşir veya "\*" joker değeri, yani herhangi bir kaynağa izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4e548-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="4e548-187">Yanıt, erişim-denetim-Izin verme-kaynak üst bilgisini içermiyorsa, AJAX isteği başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4e548-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="4e548-188">Özellikle, tarayıcı isteğe izin vermez.</span><span class="sxs-lookup"><span data-stu-id="4e548-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="4e548-189">Sunucu başarılı bir yanıt döndürse bile tarayıcı, yanıtı istemci uygulaması için kullanılabilir hale getirmez.</span><span class="sxs-lookup"><span data-stu-id="4e548-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="4e548-190">**Ön kontrol Istekleri**</span><span class="sxs-lookup"><span data-stu-id="4e548-190">**Preflight Requests**</span></span>

<span data-ttu-id="4e548-191">Bazı CORS istekleri için, tarayıcı kaynağın gerçek isteğini göndermeden önce "ön kontrol isteği" olarak adlandırılan ek bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="4e548-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="4e548-192">Aşağıdaki koşullar doğruysa tarayıcı, ön kontrol isteğini atlayabilir:</span><span class="sxs-lookup"><span data-stu-id="4e548-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="4e548-193">İstek yöntemi al, HEAD veya POST, *ve*</span><span class="sxs-lookup"><span data-stu-id="4e548-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="4e548-194">Uygulama, kabul etme, kabul etme dili, Içerik-dil, Içerik türü veya son olay KIMLIĞI dışında bir istek üst bilgisi ayarlanmamış *ve*</span><span class="sxs-lookup"><span data-stu-id="4e548-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="4e548-195">Content-Type üst bilgisi (ayarlandıysa) aşağıdakilerden biridir:</span><span class="sxs-lookup"><span data-stu-id="4e548-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="4e548-196">Application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="4e548-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="4e548-197">multipart/form-Data</span><span class="sxs-lookup"><span data-stu-id="4e548-197">multipart/form-data</span></span>
    - <span data-ttu-id="4e548-198">metin/düz</span><span class="sxs-lookup"><span data-stu-id="4e548-198">text/plain</span></span>

<span data-ttu-id="4e548-199">İstek üstbilgileri hakkındaki kural, uygulamanın **setRequestHeader** **XMLHttpRequest** nesnesine çağırarak ayarladığı üst bilgiler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4e548-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="4e548-200">(CORS belirtimi bu "yazar istek üstbilgilerini" çağırır.) Kural, *tarayıcı* tarafından ayarlanan Kullanıcı Aracısı, ana bilgisayar veya içerik uzunluğu gibi üstbilgilere uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="4e548-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="4e548-201">Bir ön kontrol isteğine bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e548-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="4e548-202">Uçuş öncesi isteği HTTP SEÇENEKLERI yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e548-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="4e548-203">İki özel üst bilgi içerir:</span><span class="sxs-lookup"><span data-stu-id="4e548-203">It includes two special headers:</span></span>

- <span data-ttu-id="4e548-204">Access-Control-Request-Method: gerçek istek için kullanılacak HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e548-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="4e548-205">Erişim-denetim-Istek-üstbilgiler: *uygulamanın* gerçek istekte ayarlandığı istek üst bilgilerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="4e548-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="4e548-206">(Yine, bu, tarayıcının ayarladığı üst bilgileri içermez.)</span><span class="sxs-lookup"><span data-stu-id="4e548-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="4e548-207">Sunucunun isteğe izin verdiğini kabul eden örnek bir yanıt aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e548-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="4e548-208">Yanıt, izin verilen yöntemleri ve isteğe bağlı olarak izin verilen üst bilgileri listeleyen bir erişim-denetimi-Izin-üstbilgiler başlığını listeleyen bir Access-Control-Allow-Methods üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="4e548-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="4e548-209">Ön kontrol isteği başarılı olursa, tarayıcı, daha önce açıklandığı gibi gerçek isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="4e548-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="4e548-210">Sık kullanılan araçlar, ön uç noktalarını (örneğin, [Fiddler](https://www.telerik.com/fiddler) ve [Postman](https://www.getpostman.com/)), varsayılan olarak gerekli seçenek üstbilgilerini göndermez.</span><span class="sxs-lookup"><span data-stu-id="4e548-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="4e548-211">`Access-Control-Request-Method` ve `Access-Control-Request-Headers` üst bilgilerinin istekle birlikte gönderildiğini ve seçenekler başlıklarının IIS aracılığıyla uygulamaya ulaşmasını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="4e548-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="4e548-212">IIS 'yi bir ASP.NET uygulamasının seçenek isteklerini almasına ve işlemesine izin verecek şekilde yapılandırmak için, aşağıdaki yapılandırmayı `<system.webServer><handlers>` bölümünde uygulamanın *Web. config* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4e548-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="4e548-213">`OPTIONSVerbHandler` kaldırılması, IIS 'nin seçenek isteklerini işlemesini engeller.</span><span class="sxs-lookup"><span data-stu-id="4e548-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="4e548-214">Varsayılan modül kaydı yalnızca uzantısız URL 'Ler ile alma, baş, POST ve hata ayıklama isteklerine izin verdiğinden, `ExtensionlessUrlHandler-Integrated-4.0` değişimi, SEÇENEKLERE ulaşmak için izin verir.</span><span class="sxs-lookup"><span data-stu-id="4e548-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="4e548-215">[EnableCors] için kapsam kuralları</span><span class="sxs-lookup"><span data-stu-id="4e548-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="4e548-216">Uygulamanızdaki tüm Web API denetleyicileri için işlem başına CORS 'yi, denetleyici başına veya genel olarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="4e548-217">**Eylem başına**</span><span class="sxs-lookup"><span data-stu-id="4e548-217">**Per Action**</span></span>

<span data-ttu-id="4e548-218">CORS 'yi tek bir eylem için etkinleştirmek üzere, eylem yönteminde **[Enablecors]** özniteliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4e548-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="4e548-219">Aşağıdaki örnek, CORS 'yi yalnızca `GetItem` yöntemi için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4e548-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="4e548-220">**Denetleyici başına**</span><span class="sxs-lookup"><span data-stu-id="4e548-220">**Per Controller**</span></span>

<span data-ttu-id="4e548-221">Denetleyici sınıfında **[Enablecors]** ayarlarsanız, denetleyici üzerindeki tüm eylemler için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="4e548-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="4e548-222">Bir eylemde CORS 'yi devre dışı bırakmak için, eyleme **[Disablecors]** özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e548-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="4e548-223">Aşağıdaki örnek, `PutItem`hariç her yöntemde CORS 'yi mümkün.</span><span class="sxs-lookup"><span data-stu-id="4e548-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="4e548-224">**Görünüm**</span><span class="sxs-lookup"><span data-stu-id="4e548-224">**Globally**</span></span>

<span data-ttu-id="4e548-225">Uygulamanızdaki tüm Web API denetleyicileri için CORS 'yi etkinleştirmek üzere **Enablecorsattribute** örneğini **enablecors** yöntemine geçirin:</span><span class="sxs-lookup"><span data-stu-id="4e548-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="4e548-226">Özniteliği birden fazla kapsamda ayarlarsanız, öncelik sırası şu şekilde olur:</span><span class="sxs-lookup"><span data-stu-id="4e548-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="4e548-227">Eylem</span><span class="sxs-lookup"><span data-stu-id="4e548-227">Action</span></span>
2. <span data-ttu-id="4e548-228">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="4e548-228">Controller</span></span>
3. <span data-ttu-id="4e548-229">Global</span><span class="sxs-lookup"><span data-stu-id="4e548-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="4e548-230">İzin verilen kaynakları ayarla</span><span class="sxs-lookup"><span data-stu-id="4e548-230">Set the allowed origins</span></span>

<span data-ttu-id="4e548-231">**[Enablecors]** özniteliğinin *kaynaklar parametresi,* kaynağa hangi kaynakların erişmelerine izin verildiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e548-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="4e548-232">Değer, izin verilen çıkış noktaları için virgülle ayrılmış bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="4e548-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="4e548-233">Tüm kaynaklardan gelen isteklere izin vermek için "\*" joker değerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="4e548-234">Herhangi bir kaynaktan isteklere izin vermeden önce dikkatlice düşünün.</span><span class="sxs-lookup"><span data-stu-id="4e548-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="4e548-235">Bu, tam olarak herhangi bir Web sitesinin Web API 'niz için AJAX çağrıları yapabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4e548-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="4e548-236">İzin verilen HTTP yöntemlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="4e548-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="4e548-237">**[Enablecors]** özniteliğinin *Methods* parametresi, hangi http yöntemlerinin kaynağa erişmelerine izin verileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e548-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="4e548-238">Tüm yöntemlere izin vermek için "\*" joker karakter değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e548-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="4e548-239">Aşağıdaki örnek yalnızca GET ve POST isteklerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="4e548-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="4e548-240">İzin verilen istek üst bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="4e548-240">Set the allowed request headers</span></span>

<span data-ttu-id="4e548-241">Bu makalede, bir ön kontrol isteğinin, uygulama tarafından ayarlanan HTTP üstbilgilerini (yani, "yazar istek üstbilgileri") listeleyerek bir erişim denetimi-Istek-üstbilgiler üst bilgisi nasıl dahil olabileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4e548-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="4e548-242">**[Enablecors]** özniteliğinin *Headers* parametresi hangi yazar istek üst bilgilerine izin verileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e548-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="4e548-243">Tüm üstbilgilere izin vermek için *üst bilgileri* "\*" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4e548-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="4e548-244">Belirli üstbilgileri beyaz listelemek için *üst bilgileri* izin verilen üst bilgilerin virgülle ayrılmış listesine ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4e548-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="4e548-245">Ancak, tarayıcılar erişim-denetim-Istek üst bilgilerini ayarlama konusunda tamamen tutarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4e548-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="4e548-246">Örneğin, Chrome şu anda "Origin" i içerir.</span><span class="sxs-lookup"><span data-stu-id="4e548-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="4e548-247">FireFox, uygulama bunları betikte ayarlarsa bile, "kabul et" gibi standart üstbilgileri içermez.</span><span class="sxs-lookup"><span data-stu-id="4e548-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="4e548-248">*Üst bilgileri* "\*" dışında bir şeye ayarlarsanız, en az "kabul", "içerik türü" ve "kaynak" ve ayrıca desteklemek istediğiniz tüm özel üstbilgileri dahil etmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="4e548-249">İzin verilen yanıt üst bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="4e548-249">Set the allowed response headers</span></span>

<span data-ttu-id="4e548-250">Varsayılan olarak tarayıcı, tüm yanıt üst bilgilerini uygulamaya sunmaz.</span><span class="sxs-lookup"><span data-stu-id="4e548-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="4e548-251">Varsayılan olarak kullanılabilen yanıt üstbilgileri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e548-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="4e548-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="4e548-252">Cache-Control</span></span>
- <span data-ttu-id="4e548-253">İçerik-dil</span><span class="sxs-lookup"><span data-stu-id="4e548-253">Content-Language</span></span>
- <span data-ttu-id="4e548-254">İçerik Türü</span><span class="sxs-lookup"><span data-stu-id="4e548-254">Content-Type</span></span>
- <span data-ttu-id="4e548-255">Süresi Dolacak</span><span class="sxs-lookup"><span data-stu-id="4e548-255">Expires</span></span>
- <span data-ttu-id="4e548-256">Son değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e548-256">Last-Modified</span></span>
- <span data-ttu-id="4e548-257">Prag</span><span class="sxs-lookup"><span data-stu-id="4e548-257">Pragma</span></span>

<span data-ttu-id="4e548-258">CORS belirtimi bu [basit yanıt üstbilgilerini](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)çağırır.</span><span class="sxs-lookup"><span data-stu-id="4e548-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="4e548-259">Diğer üst bilgileri uygulama için kullanılabilir hale getirmek için, **[Enablecors]** *exposedHeaders* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4e548-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="4e548-260">Aşağıdaki örnekte, denetleyicinin `Get` yöntemi ' X-Custom-Header ' adlı bir özel üst bilgi ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="4e548-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="4e548-261">Varsayılan olarak tarayıcı, bu üst bilgiyi bir çapraz kaynak isteğinde kullanıma sunmaz.</span><span class="sxs-lookup"><span data-stu-id="4e548-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="4e548-262">Üstbilgiyi kullanılabilir hale getirmek için, *exposedHeaders*Içine ' X-Custom-Header ' ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e548-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="4e548-263">Kimlik bilgilerini, çıkış noktaları arası isteklere geçirme</span><span class="sxs-lookup"><span data-stu-id="4e548-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="4e548-264">Kimlik bilgileri CORS isteğinde özel işleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4e548-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="4e548-265">Varsayılan olarak tarayıcı, bir çapraz kaynak isteğiyle kimlik bilgileri göndermez.</span><span class="sxs-lookup"><span data-stu-id="4e548-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="4e548-266">Kimlik bilgileri, HTTP kimlik doğrulama düzenlerini de içerir.</span><span class="sxs-lookup"><span data-stu-id="4e548-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="4e548-267">Bir çapraz kaynak isteğiyle kimlik bilgilerini göndermek için, istemcinin **XMLHttpRequest. withcredentials** öğesini true olarak ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e548-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="4e548-268">Doğrudan **XMLHttpRequest** kullanma:</span><span class="sxs-lookup"><span data-stu-id="4e548-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="4e548-269">JQuery içinde:</span><span class="sxs-lookup"><span data-stu-id="4e548-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="4e548-270">Ayrıca, sunucu kimlik bilgilerine izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="4e548-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="4e548-271">Web API 'sinde, çıkış noktaları arası kimlik bilgilerine izin vermek için, **[Enablecors]** özniteliğinde **SupportsCredentials** özelliğini true olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4e548-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="4e548-272">Bu özellik true ise, HTTP yanıtı bir erişim-denetim-Izin-kimlik bilgileri üst bilgisi içerecektir.</span><span class="sxs-lookup"><span data-stu-id="4e548-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="4e548-273">Bu üst bilgi, tarayıcıya sunucunun bir çapraz kaynak isteği için kimlik bilgilerini verdiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="4e548-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="4e548-274">Tarayıcı kimlik bilgilerini gönderirse, ancak yanıt geçerli bir erişim-denetim-Izin-kimlik bilgileri üst bilgisi içermiyorsa, tarayıcı uygulamaya yanıtı kullanıma sunmaz ve AJAX isteği başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4e548-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="4e548-275">**SupportsCredentials** değeri true olarak ayarlanırken, başka bir etki alanındaki bir Web sitesinin kullanıcı adına Kullanıcı adına, oturum açmış bir kullanıcının kimlik bilgilerini, Kullanıcı tarafından farkında olmadan BIR Web API 'nize gönderebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e548-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="4e548-276">CORS belirtimi Ayrıca, **SupportsCredentials** true ise &quot;\*&quot; için *Çıkış* ayarının geçersiz olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e548-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="4e548-277">Özel CORS ilke sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="4e548-277">Custom CORS policy providers</span></span>

<span data-ttu-id="4e548-278">**[Enablecors]** özniteliği **ıcorspolicyprovider** arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="4e548-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="4e548-279">**Özniteliğinden** türetilen ve **ıcorspolicyprovider**uygulayan bir sınıf oluşturarak kendi uygulamanızı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="4e548-280">Artık özniteliği, **[Enablecors]** yerine koyabileceğiniz herhangi bir yerde uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="4e548-281">Örneğin, özel bir CORS ilke sağlayıcısı yapılandırma dosyasından ayarları okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="4e548-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="4e548-282">Öznitelikleri kullanmanın bir alternatifi olarak **ıcorspolicyprovider** nesneleri oluşturan bir **ıcorspolicyproviderfactory** nesnesini kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e548-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="4e548-283">**Icorspolicyproviderfactory**ayarlamak için, başlangıç sırasında **setcorspolicyproviderfactory** genişletme yöntemini aşağıdaki gibi çağırın:</span><span class="sxs-lookup"><span data-stu-id="4e548-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="4e548-284">Tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="4e548-284">Browser support</span></span>

<span data-ttu-id="4e548-285">Web API CORS paketi, sunucu tarafı teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="4e548-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="4e548-286">Kullanıcının tarayıcısının de CORS 'yi desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e548-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="4e548-287">Neyse ki, tüm büyük tarayıcıların geçerli sürümleri [cors desteği](http://caniuse.com/cors)içerir.</span><span class="sxs-lookup"><span data-stu-id="4e548-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
