---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hub'ları API Kılavuzu - JavaScript İstemci | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, tarayıcılar ve Windows Mağazası (WinJS) aplicat gibi JavaScript istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676085"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="ac618-103">ASP.NET SignalR Hub'ları API Kılavuzu - JavaScript İstemci</span><span class="sxs-lookup"><span data-stu-id="ac618-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ac618-104">Bu belge, tarayıcılar ve Windows Mağazası (WinJS) uygulamaları gibi JavaScript istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="ac618-105">SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="ac618-106">Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="ac618-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="ac618-107">İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="ac618-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="ac618-108">SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="ac618-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="ac618-109">SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="ac618-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="ac618-110">SignalR, Hub'lar ve Kalıcı [Bağlantılar'a](../getting-started/introduction-to-signalr.md)giriş için bkz.</span><span class="sxs-lookup"><span data-stu-id="ac618-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ac618-111">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="ac618-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ac618-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ac618-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="ac618-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ac618-113">.NET 4.5</span></span>
> - <span data-ttu-id="ac618-114">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="ac618-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ac618-115">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="ac618-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ac618-116">SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ac618-117">Sorular ve yorumlar</span><span class="sxs-lookup"><span data-stu-id="ac618-117">Questions and comments</span></span>
>
> <span data-ttu-id="ac618-118">Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ac618-119">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="ac618-120">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ac618-120">Overview</span></span>

<span data-ttu-id="ac618-121">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="ac618-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="ac618-122">Oluşturulan proxy ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="ac618-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="ac618-123">Oluşturulan proxy ne zaman kullanılır</span><span class="sxs-lookup"><span data-stu-id="ac618-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="ac618-124">İstemci Kurulumu</span><span class="sxs-lookup"><span data-stu-id="ac618-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="ac618-125">Dinamik olarak oluşturulan proxy'ye nasıl başvurur?</span><span class="sxs-lookup"><span data-stu-id="ac618-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="ac618-126">SignalR oluşturulan proxy için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac618-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="ac618-127">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="ac618-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="ac618-128">$.connection.hub, $.hubConnection() tarafından yapılan nesnedir</span><span class="sxs-lookup"><span data-stu-id="ac618-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="ac618-129">Başlangıç yönteminin eşzamanlı yürütmesi</span><span class="sxs-lookup"><span data-stu-id="ac618-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="ac618-130">Etki alanları arası bağlantı nasıl kurulur?</span><span class="sxs-lookup"><span data-stu-id="ac618-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="ac618-131">Bağlantı nasıl yapılandırılabilen</span><span class="sxs-lookup"><span data-stu-id="ac618-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="ac618-132">Sorgu dize parametreleri nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="ac618-133">Taşıma yöntemi nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="ac618-134">Hub sınıfı için proxy nasıl edinilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="ac618-135">Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="ac618-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="ac618-136">İstemciden sunucu yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="ac618-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="ac618-137">Bağlantı ömrü olayları nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="ac618-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="ac618-138">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="ac618-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="ac618-139">İstemci tarafı günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ac618-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="ac618-140">Sunucu veya .NET istemcilerinin nasıl programlanır, aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="ac618-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="ac618-141">SignalR Hub'lar API Kılavuzu - Sunucu</span><span class="sxs-lookup"><span data-stu-id="ac618-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="ac618-142">SignalR Hub'lar API Kılavuzu - .NET İstemci</span><span class="sxs-lookup"><span data-stu-id="ac618-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="ac618-143">SignalR 2 sunucu bileşeni yalnızca .NET 4.5'te kullanılabilir (ancak SignalR 2 için .NET 4.0'da bir .NET istemcisi vardır).</span><span class="sxs-lookup"><span data-stu-id="ac618-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="ac618-144">Oluşturulan proxy ve sizin için ne yapar</span><span class="sxs-lookup"><span data-stu-id="ac618-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="ac618-145">SignalR'ın sizin için ürettiği bir proxy ile veya olmadan bir SignalR hizmetiyle iletişim kurmak için bir JavaScript istemcisini programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="ac618-146">Proxy'nin sizin için yaptığı şey, bağlanmak, sunucunun çağırdığı yöntemleri yazmak ve sunucuda arama yöntemlerini kullanmak için kullandığınız kodun sözdizimini basitleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="ac618-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="ac618-147">Sunucu yöntemlerini aramak için kod yazdığınızda, oluşturulan proxy, yerel bir işlev icra ediyormuşsunuz gibi `serverMethod(arg1, arg2)` görünen `invoke('serverMethod', arg1, arg2)`sözdizimini kullanmanızı sağlar: yerine yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="ac618-148">Oluşturulan proxy sözdizimi, bir sunucu yöntemi adını yanlış yazarsanız, anında ve anlaşılır bir istemci tarafı hatası da sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="ac618-149">Vekilleri tanımlayan dosyayı el ile oluşturursanız, sunucu yöntemlerini çağıran kod yazmak için IntelliSense desteği de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="ac618-150">Örneğin, sunucuda aşağıdaki Hub sınıfına sahip olduğunuzu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="ac618-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="ac618-151">Aşağıdaki kod örnekleri, JavaScript kodunun sunucuda `NewContosoChatMessage` yöntemi çağırmak ve yöntemin `addContosoChatMessageToPage` çağrılarını sunucudan almak için nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="ac618-152">**Oluşturulan proxy ile**</span><span class="sxs-lookup"><span data-stu-id="ac618-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="ac618-153">**Oluşturulan proxy olmadan**</span><span class="sxs-lookup"><span data-stu-id="ac618-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="ac618-154">Oluşturulan proxy ne zaman kullanılır</span><span class="sxs-lookup"><span data-stu-id="ac618-154">When to use the generated proxy</span></span>

<span data-ttu-id="ac618-155">Sunucunun çağırdığı bir istemci yöntemi için birden çok olay işleyicisi kaydetmek istiyorsanız, oluşturulan proxy'yi kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ac618-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="ac618-156">Aksi takdirde, oluşturulan proxy'yi kullanmayı veya kodlama tercihinize göre kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="ac618-157">Kullanmamayı seçerseniz, istemci kodunuzdaki bir `script` öğedeki "sinyal/hub" URL'sine başvurmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ac618-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="ac618-158">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="ac618-158">Client setup</span></span>

<span data-ttu-id="ac618-159">Bir JavaScript istemcisi jQuery ve SignalR çekirdek JavaScript dosyasına referanslar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ac618-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="ac618-160">jQuery sürümü 1.7.2, 1.8.2 veya 1.9.1 gibi 1.6.4 veya daha sonraki büyük sürümler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac618-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="ac618-161">Oluşturulan proxy kullanmaya karar verirseniz, ayrıca SignalR oluşturulan proxy JavaScript dosyasına bir başvuru gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac618-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="ac618-162">Aşağıdaki örnek, oluşturulan proxy'yi kullanan bir HTML sayfasında başvuruların nasıl görünebileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="ac618-163">Bu başvurular bu sıraya eklenmelidir: jQuery ilk, SignalR çekirdek bundan sonra, ve SignalR yakınlık son.</span><span class="sxs-lookup"><span data-stu-id="ac618-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="ac618-164">Dinamik olarak oluşturulan proxy'ye nasıl başvurur?</span><span class="sxs-lookup"><span data-stu-id="ac618-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="ac618-165">Önceki örnekte, SignalR oluşturulan proxy başvuru dinamik olarak oluşturulan JavaScript kodu değil, fiziksel bir dosya için.</span><span class="sxs-lookup"><span data-stu-id="ac618-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="ac618-166">SignalR anında proxy için JavaScript kodu oluşturur ve "/signalr/hubs" URL'sine yanıt olarak istemciye hizmet eder.</span><span class="sxs-lookup"><span data-stu-id="ac618-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="ac618-167">Yönteminizle sunucuda SignalR bağlantıları için farklı bir `MapSignalR` temel URL belirttiyseniz, dinamik olarak oluşturulan proxy dosyasının URL'si, "/hub"ların ekildiği özel URL'nizdir.</span><span class="sxs-lookup"><span data-stu-id="ac618-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="ac618-168">Windows 8 (Windows Mağazası) JavaScript istemcileri için, dinamik olarak oluşturulan dosya yerine fiziksel proxy dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="ac618-169">Daha fazla bilgi için, bu konuda daha sonra [oluşturulan SignalR proxy için fiziksel bir dosya nın nasıl oluşturulabildiğini](#manualproxy) görün.</span><span class="sxs-lookup"><span data-stu-id="ac618-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="ac618-170">MVC 4 veya 5 Jilet görünümüASP.NET, proxy dosyası başvurunuzdaki uygulama köküne başvurmak için tilde'yi kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac618-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="ac618-171">SignalR'ı MVC 5'te kullanma hakkında daha fazla bilgi için [SignalR ve MVC 5 ile başlarken](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="ac618-172">MVC 3 Jilet görünümünde `Url.Content` ASP.NET, proxy dosya başvurunuz için kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac618-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="ac618-173">bir ASP.NET Web Forms `ResolveClientUrl` uygulamasında, yakınlık dosya başvurunuz için kullanın veya uygulama kökü göreli bir yol kullanarak ScriptManager üzerinden kaydedin (tilde ile başlayarak):</span><span class="sxs-lookup"><span data-stu-id="ac618-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="ac618-174">Genel bir kural olarak, CSS veya JavaScript dosyaları için kullandığınız "/signalr/hub" URL'sini belirtmek için aynı yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="ac618-175">Tilde kullanmadan bir URL belirtirseniz, bazı senaryolarda Uygulamanız IIS Express'i kullanarak Visual Studio'da test ettiğinizde doğru çalışır, ancak tam IIS'ye dağıtığınızda 404 hatasıyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ac618-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="ac618-176">Daha fazla bilgi için, MSDN sitesindeki [Web Projelerini ASP.NET için Visual Studio'daki Web Sunucularında](https://msdn.microsoft.com/library/58wxa9w5.aspx) **Kök Düzeyi Kaynaklara Yapılan Başvuruları Çözme'ye** bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="ac618-177">Visual Studio 2017'de hata ayıklama modunda bir web projesi çalıştırdığınızda ve Tarayıcınız olarak Internet Explorer kullanıyorsanız, **Solution Explorer'da** Komut Dosyaları altında proxy **dosyasını**görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="ac618-178">Dosyanın içeriğini görmek için **hub'ları**çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ac618-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="ac618-179">Visual Studio 2012 veya 2013 ve Internet Explorer kullanmıyorsanız veya hata ayıklama modunda değilseniz, "/signalR/hubs" URL'sine göz atarak dosyanın içeriğini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="ac618-180">Örneğin, siteniz de `http://localhost:56699`çalışıyorsa, `http://localhost:56699/SignalR/hubs` tarayıcınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="ac618-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="ac618-181">SignalR oluşturulan proxy için fiziksel bir dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac618-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="ac618-182">Dinamik olarak oluşturulan proxy'ye alternatif olarak, proxy koduna sahip fiziksel bir dosya oluşturabilir ve bu dosyaya başvuruyapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="ac618-183">Önbelleğe alma veya birleştirme davranışı üzerinde denetim için veya sunucu yöntemleri aramaları kodlarken IntelliSense almak için bunu yapmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="ac618-184">Proxy dosyası oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ac618-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="ac618-185">[Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ac618-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="ac618-186">Bir komut istemi açın ve SignalR.exe dosyasını içeren *araçlar* klasörüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="ac618-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="ac618-187">Araçlar klasörü aşağıdaki konumdadır:</span><span class="sxs-lookup"><span data-stu-id="ac618-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="ac618-188">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ac618-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="ac618-189">*.dll'nize* giden yol genellikle proje klasörünüzdeki *çöp kutusu* klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="ac618-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="ac618-190">Bu komut *signalr.exe*ile aynı klasörde *server.js* adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ac618-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="ac618-191">*Server.js* dosyasını projenizdeki uygun bir klasöre koyun, uygulamanız için uygun şekilde yeniden adlandırın ve "sinyalci/hub" başvurusu yerine bir referans ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac618-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="ac618-192">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="ac618-192">How to establish a connection</span></span>

<span data-ttu-id="ac618-193">Bağlantı kurmadan önce, bir bağlantı nesnesi oluşturmanız, proxy oluşturmanız ve sunucudan çağrılabilen yöntemler için olay işleyicilerini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac618-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="ac618-194">Proxy ve olay işleyicileri ayarlandığında, yöntemi arayarak `start` bağlantıyı kurun.</span><span class="sxs-lookup"><span data-stu-id="ac618-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="ac618-195">Oluşturulan proxy kullanıyorsanız, oluşturulan proxy kodu sizin için yapar, çünkü kendi kodunda bağlantı nesnesi oluşturmak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="ac618-196">**Bağlantı kurma (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="ac618-197">**Bağlantı kurma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="ac618-198">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ac618-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="ac618-199">Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="ac618-200">Varsayılan olarak, hub konumu geçerli sunucudur; farklı bir sunucuya bağlanıyorsanız, `start` aşağıdaki örnekte gösterildiği gibi yöntemi aramadan önce URL'yi belirtin:</span><span class="sxs-lookup"><span data-stu-id="ac618-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="ac618-201">Normalde bağlantıyı kurmak için yöntemi çağırmadan `start` önce olay işleyicilerini kaydedersiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="ac618-202">Bağlantıyı kurduktan sonra bazı olay işleyicilerini kaydetmek istiyorsanız, bunu yapabilirsiniz, ancak `start` yöntemi aramadan önce olay işleyicinizden en az birini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac618-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="ac618-203">Bunun bir nedeni, bir uygulamada çok sayıda Hub olabilir, ancak yalnızca bunlardan `OnConnected` birini kullanacaksanız, her Hub'da olayı tetiklemek istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="ac618-204">Bağlantı kurulduğunda, Bir Hub'ın proxy'sindeki istemci yönteminin `OnConnected` varlığı SignalR'a olayı tetiklemasını söyler.</span><span class="sxs-lookup"><span data-stu-id="ac618-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="ac618-205">`start` Yöntemi aramadan önce herhangi bir olay işleyicisi kaydetmezseniz, Hub'da yöntemleri çağırabilirsiniz, `OnConnected` ancak Hub'ın yöntemi çağrılmaz ve sunucudan istemci yöntemleri çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="ac618-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="ac618-206">$.connection.hub, $.hubConnection() tarafından yapılan nesnedir</span><span class="sxs-lookup"><span data-stu-id="ac618-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="ac618-207">Örneklerden de görebileceğiniz gibi, oluşturulan proxy'yi kullandığınızda bağlantı `$.connection.hub` nesnesi başvurur.</span><span class="sxs-lookup"><span data-stu-id="ac618-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="ac618-208">Bu, oluşturulan proxy'yi kullanmadığınızda arayarak `$.hubConnection()` elde ettiğiniz nesneyle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ac618-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="ac618-209">Oluşturulan proxy kodu aşağıdaki deyimi çalıştırarak sizin için bağlantı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ac618-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Oluşturulan proxy dosyasında bağlantı oluşturma](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="ac618-211">Oluşturulan proxy'yi kullanırken, oluşturulan proxy'yi kullanmadığınızda bağlantı nesnesiyle yapabileceğiniz her şeyi `$.connection.hub` yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="ac618-212">Başlangıç yönteminin eşzamanlı yürütmesi</span><span class="sxs-lookup"><span data-stu-id="ac618-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="ac618-213">Yöntem `start` eşsenkronize yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ac618-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="ac618-214">Bir [jQuery Ertelenmiş nesne](http://api.jquery.com/category/deferred-object/)döndürür , bu da gibi `pipe`arama yöntemleri `done`ekleyerek `fail`geri arama işlevleri ekleyebilirsiniz anlamına gelir , , ve .</span><span class="sxs-lookup"><span data-stu-id="ac618-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="ac618-215">Bağlantı kurulduktan sonra yürütmek istediğiniz kodunuz (sunucu yöntemine çağrı gibi) varsa, bu kodu geri arama işlevine koyun veya geri arama işlevinden arayın.</span><span class="sxs-lookup"><span data-stu-id="ac618-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="ac618-216">Geri `.done` arama yöntemi, bağlantı kurulduktan sonra ve sunucudaki olay işleyicisi yönteminizde `OnConnected` bulunan herhangi bir kod dan sonra yürütmeyi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="ac618-217">`start` Yöntem çağrısından sonra `.done` (geri aramada değil) sonraki kod satırı olarak önceki örnekteki "Şimdi bağlı" deyimini koyarsanız, `console.log` aşağıdaki örnekte gösterildiği gibi, bağlantı kurulmadan önce satır yürütülür:</span><span class="sxs-lookup"><span data-stu-id="ac618-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Bağlantı kurulduktan sonra çalışan kod yazmak için yanlış yol](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="ac618-219">Etki alanları arası bağlantı nasıl kurulur?</span><span class="sxs-lookup"><span data-stu-id="ac618-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="ac618-220">Genellikle tarayıcı bir sayfa `http://contoso.com`yükler, SinyalR bağlantısı aynı etki alanında, at `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="ac618-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="ac618-221">Sayfa, `http://contoso.com` `http://fabrikam.com/signalr`etki alanı arası bağlantıyla bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="ac618-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="ac618-222">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ac618-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="ac618-223">SignalR 1.x'te, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağı tarafından denetlendi.</span><span class="sxs-lookup"><span data-stu-id="ac618-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="ac618-224">Bu bayrak hem JSONP hem de CORS isteklerini denetler.</span><span class="sxs-lookup"><span data-stu-id="ac618-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="ac618-225">Daha fazla esneklik için, tüm CORS desteği SignalR'ın sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının bunu desteklediği algılanırsa hala KORS'u kullanır) ve bu senaryoları desteklemek için yeni OWIN ara yazılımları kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ac618-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="ac618-226">İstemci üzerinde JSONP gerekiyorsa (eski tarayıcılarda etki alanları arası isteklerini desteklemek için), `EnableJSONP` aşağıda `HubConfiguration` gösterildiği `true`gibi nesne üzerinde ayarlayarak açıkça etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac618-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="ac618-227">JSONP, CORS'ten daha az güvenli olduğu için varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ac618-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="ac618-228">**Microsoft.Owin.Cors'un projenize eklenmesi:** Bu kitaplığı yüklemek için Paket Yöneticisi Konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ac618-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="ac618-229">Bu komut, paketin 2.1.0 sürümünü projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="ac618-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="ac618-230">UseCors'u Arama</span><span class="sxs-lookup"><span data-stu-id="ac618-230">Calling UseCors</span></span>

 <span data-ttu-id="ac618-231">Aşağıdaki kod snippet SignalR 2'de etki alanları arası bağlantıların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="ac618-232">**SignalR 2'de etki alanları arası isteklerin uygulanması**</span><span class="sxs-lookup"><span data-stu-id="ac618-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="ac618-233">Aşağıdaki kod, SignalR 2 projesinde CORS veya JSONP'nin nasıl etkinleştirilen gösteriş olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="ac618-234">Bu kod `Map` örneği, `RunSignalR` `MapSignalR`CORS ara yazılımının yalnızca CORS desteği gerektiren SignalR istekleri için (belirtilen `MapSignalR`yoldaki tüm trafikler yerine . Harita, tüm uygulama yerine belirli bir URL öneki için çalışması gereken diğer ara yazılımlar için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="ac618-235">Kodunuzda doğru `jQuery.support.cors` şekilde ayarlanma.</span><span class="sxs-lookup"><span data-stu-id="ac618-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![jQuery.support.cors'u doğru ayarlamayın](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="ac618-237">SignalR, CORS kullanımını yönetir.</span><span class="sxs-lookup"><span data-stu-id="ac618-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="ac618-238">SignalR'ın tarayıcının CORS'u desteklediğini varsayması nedeniyle JSONP'yi gerçek devre dışı bırakırsa ayar. `jQuery.support.cors`</span><span class="sxs-lookup"><span data-stu-id="ac618-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="ac618-239">Yerel barındırma URL'sine bağlandığınızda, Internet Explorer 10 bunu etki alanı arası bağlantı olarak kabul etmez, bu nedenle sunucuda etki alanları arası bağlantıları etkinleştirmeseniz bile uygulama IE 10 ile yerel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="ac618-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="ac618-240">Internet Explorer 9 ile etki alanı arası bağlantıları kullanma hakkında bilgi için [bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="ac618-241">Chrome ile etki alanı arası bağlantıları kullanma hakkında daha fazla bilgi için [bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="ac618-242">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ac618-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="ac618-243">Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="ac618-244">Bağlantı nasıl yapılandırılabilen</span><span class="sxs-lookup"><span data-stu-id="ac618-244">How to configure the connection</span></span>

<span data-ttu-id="ac618-245">Bir bağlantı kurmadan önce, sorgu dize parametrelerini belirtebilir veya aktarım yöntemini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="ac618-246">Sorgu dize parametreleri nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-246">How to specify query string parameters</span></span>

<span data-ttu-id="ac618-247">İstemci bağlandığında sunucuya veri göndermek istiyorsanız, sorgu dize parametrelerini bağlantı nesnesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="ac618-248">Aşağıdaki örnekler, istemci kodunda bir sorgu dize parametresi nasıl ayarlanır gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac618-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="ac618-249">**Başlangıç yöntemini çağırmadan önce sorgu dize değeri ayarlama (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="ac618-250">**Başlangıç yöntemini çağırmadan önce sorgu dize değeri ayarlama (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="ac618-251">Aşağıdaki örnekte, sunucu kodunda sorgu dize parametresi nasıl okunulup okunulduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac618-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="ac618-252">Taşıma yöntemi nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-252">How to specify the transport method</span></span>

<span data-ttu-id="ac618-253">Bağlanma işleminin bir parçası olarak, bir SignalR istemcisi normalde sunucu ile hem sunucu hem de istemci tarafından desteklenen en iyi aktarım belirlemek için görüşür.</span><span class="sxs-lookup"><span data-stu-id="ac618-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="ac618-254">Hangi aktarımkullanmak istediğinizi zaten biliyorsanız, yöntemi aradığınızda aktarım yöntemini belirterek bu işlem işlemini `start` atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="ac618-255">**Aktarım yöntemini belirten istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="ac618-256">**Aktarım yöntemini belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="ac618-257">Alternatif olarak, SignalR'ın denemesini istediğiniz sırada birden çok aktarım yöntemi belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac618-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="ac618-258">**Özel bir aktarım geri dönüş düzeni belirten istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="ac618-259">**Özel bir aktarım geri dönüş düzeni belirten istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="ac618-260">Aktarım yöntemini belirtmek için aşağıdaki değerleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac618-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="ac618-261">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="ac618-261">"webSockets"</span></span>
- <span data-ttu-id="ac618-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="ac618-262">"foreverFrame"</span></span>
- <span data-ttu-id="ac618-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="ac618-263">"serverSentEvents"</span></span>
- <span data-ttu-id="ac618-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="ac618-264">"longPolling"</span></span>

<span data-ttu-id="ac618-265">Aşağıdaki örnekler, bağlantı tarafından hangi aktarım yönteminin kullanıldığını nasıl bulabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="ac618-266">**Bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="ac618-267">**Bağlantı tarafından kullanılan aktarım yöntemini görüntüleyen istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="ac618-268">Sunucu kodunda aktarım yöntemini nasıl kontrol edeceğimiz hakkında bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Bağlam özelliğinden istemci hakkında nasıl bilgi alınır.](hubs-api-guide-server.md#contextproperty)</span><span class="sxs-lookup"><span data-stu-id="ac618-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="ac618-269">Taşımalar ve geri dönüşler hakkında daha fazla bilgi için [SignalR'a Giriş - Taşımalar ve Geri Dönüşler'](../getting-started/introduction-to-signalr.md#transports)e bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="ac618-270">Hub sınıfı için proxy nasıl edinilir?</span><span class="sxs-lookup"><span data-stu-id="ac618-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="ac618-271">Oluşturduğunuz her bağlantı nesnesi, bir veya daha fazla Hub sınıfı içeren bir SignalR hizmetine bağlantı hakkındaki bilgileri kapsüller.</span><span class="sxs-lookup"><span data-stu-id="ac618-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="ac618-272">Hub sınıfıyla iletişim kurmak için, kendi oluşturduğunuz (oluşturulan proxy'yi kullanmıyorsanız) veya sizin için oluşturulan bir proxy nesnesi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ac618-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="ac618-273">İstemci üzerinde proxy adı Hub sınıf adının deve kasalı bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="ac618-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="ac618-274">SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="ac618-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="ac618-275">**Sunucuda hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="ac618-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="ac618-276">**Hub için oluşturulan istemci proxy'sine başvuru alma**</span><span class="sxs-lookup"><span data-stu-id="ac618-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="ac618-277">**Hub sınıfı için istemci proxy'si oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="ac618-278">Hub sınıfınızı bir `HubName` öznitelikle dekore ederseniz, büyük/küçük harf değiştirmeden tam adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="ac618-279">**HubName özniteliği ile sunucuda Hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="ac618-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="ac618-280">**Hub için oluşturulan istemci proxy'sine başvuru alma**</span><span class="sxs-lookup"><span data-stu-id="ac618-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="ac618-281">**Hub sınıfı için istemci proxy'si oluşturma (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="ac618-282">Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="ac618-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="ac618-283">Sunucunun Hub'dan çağırabileceği bir yöntem tanımlamak için, oluşturulan proxy'nin `client` özelliğini kullanarak Hub proxy'sine bir olay işleyicisi ekleyin veya oluşturulan proxy'yi kullanmıyorsanız `on` yöntemi arayın.</span><span class="sxs-lookup"><span data-stu-id="ac618-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="ac618-284">Parametreler karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="ac618-285">Bağlantıyı kurmak için yöntemi çağırmadan `start` önce olay işleyicisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac618-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="ac618-286">(Yöntemi aradıktan sonra olay işleyicileri eklemek istiyorsanız, bu belgede daha önce [bağlantı kurma notu](#establishconnection) na bakın ve oluşturulan proxy'yi kullanmadan bir yöntem tanımlamak için gösterilen sözdizimini kullanın.) `start`</span><span class="sxs-lookup"><span data-stu-id="ac618-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="ac618-287">Yöntem adı eşleştirme büyük/küçük harf duyarsız.</span><span class="sxs-lookup"><span data-stu-id="ac618-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="ac618-288">Örneğin, `Clients.All.addContosoChatMessageToPage` sunucuda , `AddContosoChatMessageToPage` `addContosoChatMessageToPage`veya `addcontosochatmessagetopage` istemci üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ac618-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="ac618-289">**İstemci üzerinde yöntemi tanımlama (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="ac618-290">**İstemci de yöntemi tanımlamak için alternatif yol (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="ac618-291">**İstemci üzerinde yöntemi tanımlayın (oluşturulan proxy olmadan veya başlat yöntemini çağırdıktan sonra eklerken)**</span><span class="sxs-lookup"><span data-stu-id="ac618-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="ac618-292">**İstemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="ac618-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="ac618-293">Aşağıdaki örnekler, yöntem parametresi olarak karmaşık bir nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="ac618-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="ac618-294">**Karmaşık bir nesne alan istemcide yöntem tanımlama (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="ac618-295">**Karmaşık bir nesne alan istemcide yöntem tanımlama (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="ac618-296">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="ac618-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="ac618-297">**Karmaşık bir nesne kullanarak istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="ac618-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="ac618-298">İstemciden sunucu yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="ac618-298">How to call server methods from the client</span></span>

<span data-ttu-id="ac618-299">İstemciden sunucu yöntemini çağırmak `server` için, oluşturulan proxy'yi kullanmıyorsanız oluşturulan proxy'nin özelliğini veya Hub proxy'deki `invoke` yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="ac618-300">İade değeri veya parametreler karmaşık nesneler olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="ac618-301">Hub'daki yöntem adının deve kılıfı sürümünde geçirin.</span><span class="sxs-lookup"><span data-stu-id="ac618-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="ac618-302">SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="ac618-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="ac618-303">Aşağıdaki örnekler, iade değeri olmayan bir sunucu yönteminin nasıl çağrılmasını ve iade değeri olan bir sunucu yönteminin nasıl çağrılmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="ac618-304">**HubMethodName özniteliği olmayan sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="ac618-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="ac618-305">**Parametrede geçirilen karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="ac618-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="ac618-306">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="ac618-307">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="ac618-308">Hub yöntemini bir `HubMethodName` öznitelikle dekore ettiyseniz, büyük/küçük harf değiştirmeden bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="ac618-309">HubMethodName özniteliği olan **sunucu yöntemi**</span><span class="sxs-lookup"><span data-stu-id="ac618-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="ac618-310">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="ac618-311">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="ac618-312">Önceki örnekler, iade değeri olmayan bir sunucu yönteminin nasıl çağrılmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="ac618-313">Aşağıdaki örnekler, iade değeri olan bir sunucu yönteminin nasıl çağrılmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="ac618-314">**İade değeri olan bir yöntemiçin sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="ac618-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="ac618-315">İade değeri **için kullanılan Stok sınıfı**</span><span class="sxs-lookup"><span data-stu-id="ac618-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="ac618-316">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="ac618-317">**Sunucu yöntemini çağıran istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="ac618-318">Bağlantı ömrü olayları nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="ac618-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="ac618-319">SignalR işleyebilir aşağıdaki bağlantı ömrü olayları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ac618-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="ac618-320">`starting`: Bağlantı üzerinden herhangi bir veri gönderilmeden önce yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="ac618-321">`received`: Bağlantıdan herhangi bir veri alındığı zaman yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="ac618-322">Alınan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-322">Provides the received data.</span></span>
- <span data-ttu-id="ac618-323">`connectionSlow`: İstemci yavaş veya sık sık bırakarak bağlantı algıladığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="ac618-324">`reconnecting`: Altta yatan aktarım yeniden bağlanmaya başladığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="ac618-325">`reconnected`: Temel taşıma yeniden bağlandığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="ac618-326">`stateChanged`: Bağlantı durumu değiştiğinde yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="ac618-327">Eski durumu ve yeni durumu (Bağlama, Bağlama, Yeniden Bağlanma veya Bağlantı Kesme) sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="ac618-328">`disconnected`: Bağlantı kesildiğinde yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="ac618-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="ac618-329">Örneğin, fark edilebilir gecikmelere neden olabilecek bağlantı sorunları olduğunda uyarı iletilerini görüntülemek `connectionSlow` istiyorsanız, olayı ele alın.</span><span class="sxs-lookup"><span data-stu-id="ac618-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="ac618-330">**Bağlantıyı işlemeSlow olayı (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="ac618-331">**Bağlantıyı işlemeSlow olayı (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="ac618-332">Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="ac618-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="ac618-333">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="ac618-333">How to handle errors</span></span>

<span data-ttu-id="ac618-334">SignalR JavaScript istemcisi için bir işleyici ekleyebileceğiniz bir `error` olay sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac618-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="ac618-335">Sunucu yöntemi çağırmasından kaynaklanan hatalar için işleyici eklemek için başarısız yöntemini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac618-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="ac618-336">Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, SignalR'ın hatadan sonra döndürdİğİ özel durum nesnesi hata hakkında en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="ac618-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="ac618-337">Örneğin, bir çağrı `newContosoChatMessage` başarısız olursa, hata nesnesindeki`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`hata iletisi " " Üretimdeki istemcilere ayrıntılı hata iletileri göndermek güvenlik nedenleriyle önerilmez, ancak sorun giderme amacıyla ayrıntılı hata iletilerini etkinleştirmek istiyorsanız, sunucudaki aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac618-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="ac618-338">Aşağıdaki örnekte, hata olayı için işleyici nasıl ekleyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac618-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="ac618-339">**Hata işleyicisi ekleme (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="ac618-340">**Hata işleyicisi ekleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="ac618-341">Aşağıdaki örnek, bir yöntem çağırma bir hata işlemek için nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac618-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="ac618-342">**Yöntem çağırmadan gelen bir hatayı işleme (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="ac618-343">**Yöntem çağırmasından bir hata işleme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="ac618-344">Bir yöntem çağırma başarısız `error` olursa, olay da yükseltilir, `error` bu nedenle yöntem `.fail` işleyicisi ve yöntem geri arama kodu yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ac618-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="ac618-345">İstemci tarafı günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ac618-345">How to enable client-side logging</span></span>

<span data-ttu-id="ac618-346">Bağlantıda istemci tarafı günlüğe kaydetmeyi `logging` etkinleştirmek için, bağlantıyı `start` kurmak için yöntemi çağırmadan önce özelliği bağlantı nesnesi üzerinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ac618-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="ac618-347">**Günlüğü etkinleştirme (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="ac618-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="ac618-348">**Günlüğü etkinleştirme (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="ac618-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="ac618-349">Günlükleri görmek için tarayıcınızın geliştirici araçlarını açın ve Konsol sekmesine gidin. Bunu nasıl yapacağını gösteren adım adım yönergeleri ve ekran görüntülerini gösteren bir öğretici için, ASP.NET Signalr ile Sunucu Yayını ' na bakın [- Günlük'u etkinleştirin.](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)</span><span class="sxs-lookup"><span data-stu-id="ac618-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
