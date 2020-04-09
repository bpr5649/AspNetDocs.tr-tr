---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hub'ları API Kılavuzu - Sunucu (C#) | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, SignalR sürüm 2 için SignalR Hub'ASP.NET sunucu tarafıprogramlamaiçin bir giriş sağlar, kod örnekleri gösteren ile ...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676190"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="0f233-103">ASP.NET SignalR Hub'ları API Kılavuzu - Sunucu (C#)</span><span class="sxs-lookup"><span data-stu-id="0f233-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="0f233-104">Patrick [Fletcher](https://github.com/pfletcher)tarafından , [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0f233-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="0f233-105">Bu belge, SignalR sürüm 2 için signalr hub'ASP.NET sunucu tarafını programlamaya giriş sağlar ve kod örnekleri ortak seçenekleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="0f233-106">SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f233-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="0f233-107">Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="0f233-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="0f233-108">İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="0f233-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="0f233-109">SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="0f233-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="0f233-110">SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="0f233-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="0f233-111">SignalR, Hub'lar ve Kalıcı [Bağlantılar'a](../getting-started/introduction-to-signalr.md)giriş için bkz.</span><span class="sxs-lookup"><span data-stu-id="0f233-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="0f233-112">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="0f233-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="0f233-113">Görsel Stüdyo 2013</span><span class="sxs-lookup"><span data-stu-id="0f233-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="0f233-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="0f233-114">.NET 4.5</span></span>
> - <span data-ttu-id="0f233-115">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="0f233-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="0f233-116">Konu sürümleri</span><span class="sxs-lookup"><span data-stu-id="0f233-116">Topic versions</span></span>
> 
> <span data-ttu-id="0f233-117">SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="0f233-118">Sorular ve yorumlar</span><span class="sxs-lookup"><span data-stu-id="0f233-118">Questions and comments</span></span>
> 
> <span data-ttu-id="0f233-119">Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="0f233-120">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="0f233-121">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0f233-121">Overview</span></span>

<span data-ttu-id="0f233-122">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="0f233-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="0f233-123">SignalR ara yazılımnasıl kaydedilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="0f233-124">/sinyalci URL'si</span><span class="sxs-lookup"><span data-stu-id="0f233-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="0f233-125">SignalR seçeneklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f233-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="0f233-126">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="0f233-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="0f233-127">Hub nesnesi yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="0f233-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="0f233-128">JavaScript istemcilerinde Hub adlarının deve kaplaması</span><span class="sxs-lookup"><span data-stu-id="0f233-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="0f233-129">Birden Çok Hub</span><span class="sxs-lookup"><span data-stu-id="0f233-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="0f233-130">Güçlü Bir Şekilde Yazılan Hub'lar</span><span class="sxs-lookup"><span data-stu-id="0f233-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="0f233-131">Hub sınıfında istemcilerin çağırabileceği yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="0f233-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="0f233-132">JavaScript istemcilerinde yöntem adlarının deve kaplaması</span><span class="sxs-lookup"><span data-stu-id="0f233-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="0f233-133">Eşsenkronize olarak ne zaman yürütülecek?</span><span class="sxs-lookup"><span data-stu-id="0f233-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="0f233-134">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="0f233-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="0f233-135">Hub yöntemi çağrılarından ilerlemeyi bildirme</span><span class="sxs-lookup"><span data-stu-id="0f233-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="0f233-136">Hub sınıfından istemci yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="0f233-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="0f233-137">Hangi istemcilerin RPC'yi alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="0f233-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="0f233-138">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="0f233-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="0f233-139">Büyük/küçük harf duyarsız yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="0f233-140">Eşkron yürütme</span><span class="sxs-lookup"><span data-stu-id="0f233-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="0f233-141">Hub sınıfından grup üyeliği nasıl yönetilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="0f233-142">Ekle ve Kaldır yöntemlerinin eşzamanlı yürütmesi</span><span class="sxs-lookup"><span data-stu-id="0f233-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="0f233-143">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="0f233-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="0f233-144">Tek kullanıcılı gruplar</span><span class="sxs-lookup"><span data-stu-id="0f233-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="0f233-145">Hub sınıfındaki bağlantı ömrü olayları nasıl işleyebilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="0f233-146">OnConnected, OnDisconnected ve OnReconnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="0f233-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="0f233-147">Arayan durumu doldurulmamada</span><span class="sxs-lookup"><span data-stu-id="0f233-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="0f233-148">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="0f233-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="0f233-149">İstemciler ve Hub sınıfı arasında durum nasıl geçirilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="0f233-150">Hub sınıfındaki hatalar nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="0f233-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="0f233-151">İstemci yöntemlerini arama ve Hub sınıfı dışından grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="0f233-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="0f233-152">İstemci yöntemlerini arama</span><span class="sxs-lookup"><span data-stu-id="0f233-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="0f233-153">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="0f233-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="0f233-154">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="0f233-155">Hubs ardışık hattı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="0f233-156">İstemcilerin nasıl programlanacak programlayacağına ilişkin belgeler için aşağıdaki kaynaklara bakın</span><span class="sxs-lookup"><span data-stu-id="0f233-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="0f233-157">SignalR Hubs API Kılavuzu - JavaScript İstemci</span><span class="sxs-lookup"><span data-stu-id="0f233-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="0f233-158">SignalR Hub'lar API Kılavuzu - .NET İstemci</span><span class="sxs-lookup"><span data-stu-id="0f233-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="0f233-159">SignalR 2'nin sunucu bileşenleri yalnızca .NET 4.5'te kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="0f233-160">.NET 4.0 çalıştıran sunucular SignalR v1.x kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0f233-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="0f233-161">SignalR ara yazılımnasıl kaydedilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-161">How to register SignalR middleware</span></span>

<span data-ttu-id="0f233-162">İstemcilerin Hub'ınıza bağlanmak için kullanacağı `MapSignalR` yolu tanımlamak için uygulama başladığında yöntemi arayın.</span><span class="sxs-lookup"><span data-stu-id="0f233-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="0f233-163">`MapSignalR`sınıf için bir [uzantı yöntemidir.](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions`</span><span class="sxs-lookup"><span data-stu-id="0f233-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="0f233-164">Aşağıdaki örnekte, OWIN başlangıç sınıfını kullanarak SignalR Hub'ları rotasının nasıl tanımlanılışgösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="0f233-165">ASP.NET bir MVC uygulamasına SignalR işlevselliği ekliyorsanız, SignalR rotasının diğer rotalardan önce eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f233-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="0f233-166">Daha fazla bilgi için [Bkz. Öğretici: SignalR 2 ve MVC 5 ile Başlarken.](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="0f233-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="0f233-167">/sinyalci URL'si</span><span class="sxs-lookup"><span data-stu-id="0f233-167">The /signalr URL</span></span>

<span data-ttu-id="0f233-168">Varsayılan olarak, istemcilerin Hub'ınıza bağlanmak için kullanacağı rota URL'si "/signalr"dir.</span><span class="sxs-lookup"><span data-stu-id="0f233-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="0f233-169">(Bu URL'yi otomatik olarak oluşturulan JavaScript dosyası için olan "/signalr/hubs" URL'si ile karıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="0f233-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="0f233-170">Oluşturulan proxy hakkında daha fazla bilgi için [SignalR Hub'lar API Kılavuzu - JavaScript İstemci - Oluşturulan proxy ve sizin için ne yaptığını](hubs-api-guide-javascript-client.md#genproxy)bakın .)</span><span class="sxs-lookup"><span data-stu-id="0f233-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="0f233-171">Bu temel URL'yi SignalR için kullanılabilir hale getiren olağanüstü durumlar olabilir; örneğin, projenizde *signalr* adında bir klasör var ve adı değiştirmek istemiyorsun.</span><span class="sxs-lookup"><span data-stu-id="0f233-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="0f233-172">Bu durumda, aşağıdaki örneklerde gösterildiği gibi temel URL'yi değiştirebilirsiniz (örnek koddaki "/sinyal"i istediğiniz URL ile değiştirin).</span><span class="sxs-lookup"><span data-stu-id="0f233-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="0f233-173">**URL'yi belirten sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="0f233-174">**URL'yi belirten JavaScript istemci kodu (oluşturulan proxy ile)**</span><span class="sxs-lookup"><span data-stu-id="0f233-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="0f233-175">**URL'yi belirten JavaScript istemci kodu (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="0f233-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="0f233-176">**URL'yi belirten .NET istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="0f233-177">Sinyal Seçeneklerinin Yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="0f233-177">Configuring SignalR Options</span></span>

<span data-ttu-id="0f233-178">`MapSignalR` Yöntemin aşırı yükleri özel bir URL, özel bağımlılık çözümleyicisi ve aşağıdaki seçenekleri belirtmenize olanak tanır:</span><span class="sxs-lookup"><span data-stu-id="0f233-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="0f233-179">Tarayıcı istemcilerinden CORS veya JSONP kullanarak etki alanları arası aramaları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f233-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="0f233-180">Genellikle tarayıcı bir sayfa `http://contoso.com`yükler, SinyalR bağlantısı aynı etki alanında, at `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="0f233-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="0f233-181">Sayfa, `http://contoso.com` `http://fabrikam.com/signalr`etki alanı arası bağlantıyla bağlantı yapıyorsa.</span><span class="sxs-lookup"><span data-stu-id="0f233-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="0f233-182">Güvenlik nedenleriyle, etki alanları arası bağlantılar varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="0f233-183">Daha fazla bilgi için [signalr hub'lar API Kılavuzu ASP.NET - JavaScript Client - Nasıl bir çapraz etki alanı bağlantısı kurmak için bkz.](hubs-api-guide-javascript-client.md#crossdomain)</span><span class="sxs-lookup"><span data-stu-id="0f233-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="0f233-184">Ayrıntılı hata iletilerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f233-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="0f233-185">Hatalar oluştuğunda, SignalR'In varsayılan davranışı istemcilere ne olduğu hakkında ayrıntılı bilgi olmadan bir bildirim iletisi göndermektir.</span><span class="sxs-lookup"><span data-stu-id="0f233-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="0f233-186">Kötü niyetli kullanıcılar bu bilgileri uygulamanıza yönelik saldırılarda kullanabileceğinden, müşterilere ayrıntılı hata bilgileri gönderilmesi üretimde önerilmez.</span><span class="sxs-lookup"><span data-stu-id="0f233-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="0f233-187">Sorun giderme için, geçici olarak daha bilgilendirici hata raporlaması etkinleştirmek için bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="0f233-188">Otomatik olarak oluşturulan JavaScript proxy dosyalarını devre dışı kalın.</span><span class="sxs-lookup"><span data-stu-id="0f233-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="0f233-189">Varsayılan olarak, Hub sınıflarınız için ek sa'ların yer aldığı bir JavaScript dosyası, URL "/signalr/hub"a yanıt olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0f233-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="0f233-190">JavaScript proxy'lerini kullanmak istemiyorsanız veya bu dosyayı el ile oluşturmak ve istemcilerinizde fiziksel bir dosyaya başvurmak istiyorsanız, proxy oluşturmayı devre dışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="0f233-191">Daha fazla bilgi için [SignalR Hubs API Kılavuzu - JavaScript Client - SignalR oluşturulan proxy için fiziksel bir dosya oluşturmak için nasıl](hubs-api-guide-javascript-client.md#manualproxy)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="0f233-192">Aşağıdaki örnekte, SignalR bağlantı URL'sinin nasıl belirtililir `MapSignalR` ve bu seçenekler yönteme yapılan bir çağrıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="0f233-193">Özel bir URL belirtmek için, örnekteki "/sinyal"i kullanmak istediğiniz URL ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0f233-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="0f233-194">Hub sınıfları oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="0f233-194">How to create and use Hub classes</span></span>

<span data-ttu-id="0f233-195">Hub oluşturmak için [Microsoft.Aspnet.Signalr.Hub'dan](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)türetilen bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f233-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="0f233-196">Aşağıdaki örnekte, sohbet uygulaması için basit bir Hub sınıfı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="0f233-197">Bu örnekte, bağlı bir `NewContosoChatMessage` istemci yöntemi arayabilir ve bu yöntem olduğunda, alınan veriler tüm bağlı istemcilere yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="0f233-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="0f233-198">Hub nesnesi yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="0f233-198">Hub object lifetime</span></span>

<span data-ttu-id="0f233-199">Hub sınıfını anında atamazsın veya yöntemlerini sunucuda kendi kodunuzdan aramazsınız; tüm bunlar SignalR Hub'lar boru hattı tarafından sizin için yapılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="0f233-200">SignalR, istemcinin sunucuya bağlanması, bağlantısını kesmesi veya bir yöntem çağrısı yapması gibi hub işlemini işlemesi gerektiğinde Hub sınıfınızın yeni bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f233-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="0f233-201">Hub sınıfının örnekleri geçici olduğundan, durumları bir yöntem çağrısından diğerine korumak için bunları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0f233-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="0f233-202">Sunucu her istemciden yöntem çağrısı aldığında, Hub sınıfınızın yeni bir örneği iletiyi işler.</span><span class="sxs-lookup"><span data-stu-id="0f233-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="0f233-203">Birden çok bağlantı ve yöntem çağrıları aracılığıyla durumu korumak için, veritabanı veya Hub sınıfında statik bir değişken veya türetilmeyen farklı bir sınıf gibi başka bir yöntem `Hub`kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="0f233-204">Hub sınıfındastatik değişken gibi bir yöntem kullanarak bellekte verileri kalıcı olarak kullanırsanız, uygulama etki alanı geri dönüştürdüğünde veriler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="0f233-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="0f233-205">Hub sınıfının dışında çalışan kendi kodunuzdan istemcilere ileti göndermek istiyorsanız, hub sınıfı örneğini anında anlayarak bunu yapamazsınız, ancak Hub sınıfınız için SignalR bağlam nesnesine bir başvuru alarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="0f233-206">Daha fazla bilgi için, bu konuda daha sonra [Hub sınıfı dışından istemci yöntemlerini nasıl çağırıp grupları nasıl yöneteceklerini](#callfromoutsidehub) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f233-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="0f233-207">JavaScript istemcilerinde Hub adlarının deve kaplaması</span><span class="sxs-lookup"><span data-stu-id="0f233-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="0f233-208">Varsayılan olarak, JavaScript istemcileri sınıf adının deve kasalı bir sürümünü kullanarak Hub'lara başvurur.</span><span class="sxs-lookup"><span data-stu-id="0f233-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="0f233-209">SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="0f233-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="0f233-210">Önceki örnek JavaScript kodunda olarak `contosoChatHub` adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="0f233-211">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="0f233-212">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="0f233-213">İstemciler için farklı bir ad belirtmek `HubName` istiyorsanız, özniteliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f233-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="0f233-214">Bir `HubName` öznitelik kullandığınızda, JavaScript istemcilerinde deve durumunda ad değişikliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="0f233-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="0f233-215">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="0f233-216">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="0f233-217">Birden Çok Hub</span><span class="sxs-lookup"><span data-stu-id="0f233-217">Multiple Hubs</span></span>

<span data-ttu-id="0f233-218">Bir uygulamada birden çok Hub sınıfı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="0f233-219">Bunu yaptığınızda, bağlantı paylaşılır, ancak gruplar ayrıdır:</span><span class="sxs-lookup"><span data-stu-id="0f233-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="0f233-220">Tüm istemciler, hizmetinizle ("/signalr" veya belirttiğiniz özel URL'nizde) bir SignalR bağlantısı kurmak için aynı URL'yi kullanır ve bu bağlantı hizmet tarafından tanımlanan tüm Hub'lar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="0f233-221">Tek bir sınıftaki tüm Hub işlevlerini tanımlamayla karşılaştırıldığında birden çok Hub için performans farkı yoktur.</span><span class="sxs-lookup"><span data-stu-id="0f233-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="0f233-222">Tüm Hub'lar aynı HTTP istek bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="0f233-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="0f233-223">Tüm Hub'lar aynı bağlantıyı paylaştığından, sunucunun aldığı tek HTTP isteği bilgisi SignalR bağlantısını kuran orijinal HTTP isteğinde ne gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="0f233-224">Bir sorgu dizesi belirterek istemciden sunucuya bilgi aktarmak için bağlantı isteğini kullanırsanız, farklı Hub'lara farklı sorgu dizeleri sağlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0f233-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="0f233-225">Tüm Hub'lar aynı bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="0f233-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="0f233-226">Oluşturulan JavaScript yakınlık dosyası, tek bir dosyadaki tüm Hub'lar için yakınlıklar içerir.</span><span class="sxs-lookup"><span data-stu-id="0f233-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="0f233-227">JavaScript proxy'leri hakkında bilgi için [SignalR Hub'lar API Kılavuzu - JavaScript Client - Oluşturulan proxy ve sizin için ne yaptığına](hubs-api-guide-javascript-client.md#genproxy)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="0f233-228">Gruplar Hub'lar içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0f233-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="0f233-229">SignalR'da bağlı istemcialt kümelerine yayın yapacak adlandırılmış grupları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="0f233-230">Gruplar her Hub için ayrı ayrı tutulur.</span><span class="sxs-lookup"><span data-stu-id="0f233-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="0f233-231">Örneğin, "Yöneticiler" adlı bir grup, sınıfınız `ContosoChatHub` için bir istemci kümesi içerir ve aynı grup adı `StockTickerHub` sınıfınız için farklı bir istemci kümesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="0f233-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="0f233-232">Güçlü Bir Şekilde Yazılan Hub'lar</span><span class="sxs-lookup"><span data-stu-id="0f233-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="0f233-233">Müşterinizin başvuruedebileceği hub yöntemleriniz için bir arayüz tanımlamak (ve hub yöntemlerinizde Intellisense'i etkinleştirin), `Hub<T>` hub'ınızı `Hub`(SignalR 2.1'de tanıtılan) yerine türetin:</span><span class="sxs-lookup"><span data-stu-id="0f233-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="0f233-234">Hub sınıfında istemcilerin çağırabileceği yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="0f233-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="0f233-235">İstemciden çağrılmasını istediğiniz hub'da bir yöntemi ortaya çıkarmak için, aşağıdaki örneklerde gösterildiği gibi ortak bir yöntem bildirin.</span><span class="sxs-lookup"><span data-stu-id="0f233-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="0f233-236">Herhangi bir C# yönteminde olduğu gibi, karmaşık türler ve diziler de dahil olmak üzere bir iade türü ve parametreleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="0f233-237">Parametrelerde aldığınız veya arayana geri döndüğünüz tüm veriler JSON kullanılarak istemci ve sunucu arasında iletilir ve SignalR karmaşık nesnelerin ve nesnelerin dizilerinin bağlanmasını otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="0f233-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="0f233-238">JavaScript istemcilerinde yöntem adlarının deve kaplaması</span><span class="sxs-lookup"><span data-stu-id="0f233-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="0f233-239">Varsayılan olarak, JavaScript istemcileri yöntem adının deve kasalı bir sürümünü kullanarak Hub yöntemlerine başvurur.</span><span class="sxs-lookup"><span data-stu-id="0f233-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="0f233-240">SignalR, JavaScript kodunun JavaScript kurallarına uygun olması için bu değişikliği otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="0f233-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="0f233-241">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="0f233-242">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="0f233-243">İstemciler için farklı bir ad belirtmek `HubMethodName` istiyorsanız, özniteliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f233-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="0f233-244">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="0f233-245">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="0f233-246">Eşsenkronize olarak ne zaman yürütülecek?</span><span class="sxs-lookup"><span data-stu-id="0f233-246">When to execute asynchronously</span></span>

<span data-ttu-id="0f233-247">Yöntem uzun süreli olacaksa veya veritabanı araması veya web hizmeti çağrısı gibi beklemeyi içeren işler yapmak zorundaysa, [Görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) `void` `T` (iade yerine) veya [Görev&lt;&gt; T](https://msdn.microsoft.com/library/dd321424.aspx) nesnesini (iade türü yerine) döndürerek Hub yöntemini eş zamanlı hale getirin.</span><span class="sxs-lookup"><span data-stu-id="0f233-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="0f233-248">Yöntemden bir `Task` nesne döndürdüğünde, SignalR `Task` tamamlanmasını bekler ve ardından paketlenmemiş sonucu istemciye geri gönderir, bu nedenle istemcideki yöntem çağrısını nasıl kodladığınız konusunda bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="0f233-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="0f233-249">Hub yöntemini eşkron yapma, WebSocket aktarımını kullandığında bağlantıyı engellemeyi önler.</span><span class="sxs-lookup"><span data-stu-id="0f233-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="0f233-250">Hub yöntemi eşzamanlı olarak yürütülür ve aktarım WebSocket olduğunda, Hub yöntemi tamamlanana kadar hub'daki yöntemlerin sonraki çağrıları aynı istemciden engellenir.</span><span class="sxs-lookup"><span data-stu-id="0f233-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="0f233-251">Aşağıdaki örnek, eşzamanlı veya eşsenkronize çalıştırmak için kodlanmış aynı yöntemi gösterir ve ardından her iki sürümü de aramak için çalışan JavaScript istemci kodu gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="0f233-252">**Zaman uyumlu**</span><span class="sxs-lookup"><span data-stu-id="0f233-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="0f233-253">**Zaman uyumsuz**</span><span class="sxs-lookup"><span data-stu-id="0f233-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="0f233-254">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="0f233-255">ASP.NET 4.5'te eşzamanlı yöntemlerin nasıl kullanılacağı hakkında daha fazla bilgi için, [ASP.NET MVC 4'te Asynchronous Yöntemleri kullanma'ya](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="0f233-256">Aşırı yüklemeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="0f233-256">Defining Overloads</span></span>

<span data-ttu-id="0f233-257">Bir yöntem için aşırı yüklemeleri tanımlamak istiyorsanız, her aşırı yükteki parametre sayısı farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0f233-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="0f233-258">Bir aşırı yükü sadece farklı parametre türleri belirterek farklılaştırırsanız, Hub sınıfınız derlenir, ancak istemciler aşırı yüklerden birini çağırmaya çalıştıklarında SignalR hizmeti çalışma zamanında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f233-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="0f233-259">Hub yöntemi çağrılarından ilerlemeyi bildirme</span><span class="sxs-lookup"><span data-stu-id="0f233-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="0f233-260">SignalR 2.1,.NET 4.5'te tanıtılan [ilerleme raporlama deseni](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="0f233-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="0f233-261">İlerleme raporlaması uygulamak `IProgress<T>` için, istemcinizin erişebileceği hub yönteminiz için bir parametre tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="0f233-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="0f233-262">Uzun soluklu bir sunucu yöntemi yazarken, hub iş parçacığı engelleme yerine Async / Await gibi bir eşzamanlı programlama deseni kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0f233-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="0f233-263">Hub sınıfından istemci yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="0f233-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="0f233-264">Sunucudan istemci yöntemlerini çağırmak `Clients` için Hub sınıfınızdaki bir yöntemde özelliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="0f233-265">Aşağıdaki örnek, bağlı tüm `addNewMessageToPage` istemcileri çağıran sunucu kodunu ve JavaScript istemcisinde yöntemi tanımlayan istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="0f233-266">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="0f233-267">İstemci yöntemini çağırmak eşzamanlı bir işlemdir `Task`ve bir .</span><span class="sxs-lookup"><span data-stu-id="0f233-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="0f233-268">Kullanım `await`Tarihi :</span><span class="sxs-lookup"><span data-stu-id="0f233-268">Use `await`:</span></span>

* <span data-ttu-id="0f233-269">İletinin hatasız gönderilmesini sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="0f233-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="0f233-270">Try-catch bloğunda hataların yakalanmasını ve işlenmesini etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0f233-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="0f233-271">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="0f233-272">İstemci yönteminden iade değeri alamazsınız; gibi `int x = Clients.All.add(1,1)` sözdizimi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="0f233-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="0f233-273">Parametreler için karmaşık türleri ve dizileri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="0f233-274">Aşağıdaki örnek, yöntem parametresinde istemciye karmaşık bir tür geçer.</span><span class="sxs-lookup"><span data-stu-id="0f233-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="0f233-275">**Karmaşık bir nesne kullanarak istemci yöntemi çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="0f233-276">**Karmaşık nesneyi tanımlayan sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="0f233-277">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="0f233-278">Hangi istemcilerin RPC'yi alacağını seçme</span><span class="sxs-lookup"><span data-stu-id="0f233-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="0f233-279">İstemciler özelliği, hangi istemcilerin RPC'yi alacağını belirtmek için çeşitli seçenekler sağlayan bir [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="0f233-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="0f233-280">Tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="0f233-281">Sadece arayan müşteri.</span><span class="sxs-lookup"><span data-stu-id="0f233-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="0f233-282">Arayan istemci hariç tüm müşteriler.</span><span class="sxs-lookup"><span data-stu-id="0f233-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="0f233-283">Bağlantı kimliğiyle tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="0f233-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="0f233-284">Bu örnek, çağıran istemciyi çağırır `addContosoChatMessageToPage` ve `Clients.Caller`'yi kullanmakla aynı etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0f233-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="0f233-285">Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="0f233-286">Belirli bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="0f233-287">Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında belirli bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="0f233-288">Çağıran istemci dışında belirli bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="0f233-289">UserId tarafından tanımlanan belirli bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0f233-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="0f233-290">Varsayılan olarak, `IPrincipal.Identity.Name`bu , ancak bu [küresel ana bilgisayar ile IUserIdProvider bir uygulama kaydedilerek](mapping-users-to-connections.md#IUserIdProvider)değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="0f233-291">Bağlantı t.c. listesindeki tüm istemciler ve gruplar.</span><span class="sxs-lookup"><span data-stu-id="0f233-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="0f233-292">Grupların listesi.</span><span class="sxs-lookup"><span data-stu-id="0f233-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="0f233-293">Ada göre bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0f233-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="0f233-294">Kullanıcı adlarının listesi (SignalR 2.1'de tanıtıldı).</span><span class="sxs-lookup"><span data-stu-id="0f233-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="0f233-295">Yöntem adları için derleme zamanı doğrulaması yok</span><span class="sxs-lookup"><span data-stu-id="0f233-295">No compile-time validation for method names</span></span>

<span data-ttu-id="0f233-296">Belirttiğiniz yöntem adı dinamik bir nesne olarak yorumlanır, bu da IntelliSense veya derleme zamanı doğrulaması olmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="0f233-297">İfade çalışma zamanında değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="0f233-298">Yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerlerini istemciye gönderir ve istemcide ada uyan bir yöntem varsa, bu yöntem çağrılır ve parametre değerleri ona aktarılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="0f233-299">İstemcide eşleşen bir yöntem bulunmazsa, hata yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="0f233-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="0f233-300">İstemci yöntemini aradiğinizde SignalR'ın istemciye aktardığı verilerin biçimi hakkında bilgi için [signalr'e giriş bölümüne](../getting-started/introduction-to-signalr.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="0f233-301">Büyük/küçük harf duyarsız yöntem adı eşleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="0f233-302">Yöntem adı eşleştirme büyük/küçük harf duyarsız.</span><span class="sxs-lookup"><span data-stu-id="0f233-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="0f233-303">Örneğin, `Clients.All.addContosoChatMessageToPage` sunucuda , `AddContosoChatMessageToPage` `addcontosochatmessagetopage`veya `addContosoChatMessageToPage` istemci üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0f233-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="0f233-304">Eşkron yürütme</span><span class="sxs-lookup"><span data-stu-id="0f233-304">Asynchronous execution</span></span>

<span data-ttu-id="0f233-305">Dediğiniz yöntem eşsenkronize olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0f233-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="0f233-306">İstemciye bir yöntem çağrısından sonra gelen herhangi bir kod, sonraki kod satırlarının yöntemin tamamlanmasını beklemesi gerektiğini belirtmediğiniz sürece SignalR'ın istemcilere veri iletimini bitirmesini beklemeden hemen yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0f233-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="0f233-307">Aşağıdaki kod örneği, iki istemci yönteminin sırayla nasıl yürütüleceklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="0f233-308">**Await kullanma (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="0f233-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="0f233-309">İstemci `await` yöntemi nin bir sonraki kod satırı yürütülmeden önce tamamlanmasını beklerseniz, bu istemcilerin bir sonraki kod satırı yürütülmeden önce iletiyi gerçekten alacağı anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="0f233-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="0f233-310">İstemci yöntemi çağrısının "tamamlanması" yalnızca SignalR'In iletiyi göndermek için gereken her şeyi yaptığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="0f233-311">İstenilenlerin iletiyi aldığını doğrulamanız gerekiyorsa, bu mekanizmayı kendiniz programlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f233-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="0f233-312">Örneğin, Hub'da `MessageReceived` bir yöntem kodlayabilir ve `addContosoChatMessageToPage` istemcideki yöntemde `MessageReceived` istemci üzerinde yapmanız gereken her türlü işi yaptıktan sonra arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="0f233-313">Hub'da, `MessageReceived` gerçek istemci alımına ve özgün yöntem çağrısının işlenmesine bağlı olarak ne iş yaparsanız yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="0f233-314">Yöntem adı olarak bir dize değişkeni nasıl kullanılır?</span><span class="sxs-lookup"><span data-stu-id="0f233-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="0f233-315">Yöntem adı olarak bir dize değişkeni kullanarak bir istemci `Clients.All` yöntemi `Clients.Others` `Clients.Caller`çağırmak istiyorsanız, `IClientProxy` döküm (veya , , vb) ve sonra [Invoke (methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)diyoruz.</span><span class="sxs-lookup"><span data-stu-id="0f233-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="0f233-316">Hub sınıfından grup üyeliği nasıl yönetilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="0f233-317">SignalR'deki gruplar, iletileri bağlı istemcilerin belirtilen alt kümelerine yayınlamak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f233-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="0f233-318">Bir grubun herhangi bir sayıda istemcisi olabilir ve istemci herhangi bir sayıda grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="0f233-319">Grup üyeliğini yönetmek için Hub sınıfının `Groups` özelliği tarafından sağlanan [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) ve [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="0f233-320">Aşağıdaki örnek, `Groups.Add` hub `Groups.Remove` yöntemlerinde istemci kodu tarafından çağrılan yöntemleri ve yöntemleri gösterir ve ardından onları çağıran JavaScript istemci kodu nu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="0f233-321">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="0f233-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="0f233-322">**Oluşturulan proxy kullanarak JavaScript istemcisi**</span><span class="sxs-lookup"><span data-stu-id="0f233-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="0f233-323">Açıkça grup oluşturmanız gerekmemektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="0f233-324">Sonuç olarak, bir grup, bir çağrıda `Groups.Add`adını ilk kez belirttiğiniz de otomatik olarak oluşturulur ve son bağlantıyı üyelikten kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="0f233-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="0f233-325">Grup üyelik listesi veya grupların listesini almak için API yoktur.</span><span class="sxs-lookup"><span data-stu-id="0f233-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="0f233-326">SignalR istemcilere ve gruplara bir [pub/alt modele](http://en.wikipedia.org/wiki/Publish/subscribe)dayalı iletigönderir ve sunucu grup veya grup üyeliklerinin listesini tutmaz.</span><span class="sxs-lookup"><span data-stu-id="0f233-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="0f233-327">Bu ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur, çünkü bir web çiftliğine düğüm eklediğinizde, SignalR'In koruduğu herhangi bir durum yeni düğüme yayılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f233-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="0f233-328">Ekle ve Kaldır yöntemlerinin eşzamanlı yürütmesi</span><span class="sxs-lookup"><span data-stu-id="0f233-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="0f233-329">Ve `Groups.Add` `Groups.Remove` yöntemler eşsenkronize yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0f233-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="0f233-330">Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen bir ileti göndermek istiyorsanız, `Groups.Add` önce yöntemin sona erdiğinden emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="0f233-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="0f233-331">Aşağıdaki kod örneği, bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="0f233-332">**Bir gruba istemci ekleme ve sonra o istemciile mesajlaşma**</span><span class="sxs-lookup"><span data-stu-id="0f233-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="0f233-333">Grup üyeliği kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="0f233-333">Group membership persistence</span></span>

<span data-ttu-id="0f233-334">SignalR bağlantıları izler, kullanıcıları değil, bu nedenle bir kullanıcının her bağlantı kurduğunda aynı grupta olmasını `Groups.Add` istiyorsanız, kullanıcı yeni bir bağlantı kurduğunda her aramanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f233-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="0f233-335">Geçici bir bağlantı kaybından sonra, bazen SignalR bağlantıyı otomatik olarak geri yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="0f233-336">Bu durumda SignalR aynı bağlantıyı geri yükleniyor, yeni bir bağlantı kurmuyor ve böylece istemcinin grup üyeliği otomatik olarak geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="0f233-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="0f233-337">Grup üyelikleri de dahil olmak üzere her istemci için bağlantı durumu istemciye çift yönlü olarak takıldıklarından, geçici ara sunucu yeniden başlatma veya hata nın sonucu olsa bile bu mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0f233-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="0f233-338">Bir sunucu kapanıp bağlantı süreleri dolmadan yeni bir sunucu yla değiştirilirse, istemci yeni sunucuya otomatik olarak yeniden bağlanabilir ve üyesi olduğu gruplara yeniden kaydolabilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="0f233-339">Bağlantı kaybından sonra bir bağlantı otomatik olarak geri yüklenemediğinde veya bağlantı zaman ları kesildiğinde veya istemci bağlantı kesildiğinde (örneğin, bir tarayıcı yeni bir sayfaya gittiğinde), grup üyelikleri kaybolur.</span><span class="sxs-lookup"><span data-stu-id="0f233-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="0f233-340">Kullanıcı bir sonraki bağlanında yeni bir bağlantı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f233-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="0f233-341">Aynı kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini korumak için, uygulamanızın kullanıcılar ve gruplar arasındaki ilişkileri izlemesi ve bir kullanıcı yeni bir bağlantı kurduğunda grup üyeliklerini geri yüklemesi vardır.</span><span class="sxs-lookup"><span data-stu-id="0f233-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="0f233-342">Bağlantılar ve yeniden bağlantılar hakkında daha fazla bilgi için hub [sınıfındaki bağlantı ömrü olaylarının bu konuda nasıl işleyeceğiniz](#connectionlifetime) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="0f233-343">Tek kullanıcılı gruplar</span><span class="sxs-lookup"><span data-stu-id="0f233-343">Single-user groups</span></span>

<span data-ttu-id="0f233-344">SignalR kullanan uygulamalar, hangi kullanıcının ileti gönderdiğini ve hangi kullanıcının ileti alması gerektiğini bilmek için genellikle kullanıcılar ve bağlantılar arasındaki ilişkileri izlemek zorundadır.</span><span class="sxs-lookup"><span data-stu-id="0f233-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="0f233-345">Gruplar bunu yapmak için kullanılan iki desenden birinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="0f233-346">Tek kullanıcılı gruplar.</span><span class="sxs-lookup"><span data-stu-id="0f233-346">Single-user groups.</span></span>

    <span data-ttu-id="0f233-347">Kullanıcı adını grup adı olarak belirtebilir ve kullanıcı her bağlandığında veya yeniden bağlanınher bağlanında gruba geçerli bağlantı kimliğini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="0f233-348">Gruba gönderdiğiniz kullanıcıya ileti göndermek için.</span><span class="sxs-lookup"><span data-stu-id="0f233-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="0f233-349">Bu yöntemin bir dezavantajı, grubun size kullanıcının çevrimiçi veya çevrimdışı olup olmadığını öğrenmeniz için bir yol sağlamamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0f233-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="0f233-350">Kullanıcı adları ve bağlantı adları arasındaki ilişkileri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0f233-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="0f233-351">Her kullanıcı adı ile bir veya daha fazla bağlantı bağlantısı disi arasındaki ilişkilendirmeyi bir sözlükveya veritabanında depolayabilir ve kullanıcı her bağlandığında veya bağlantı kestiğinde depolanan verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="0f233-352">Kullanıcıya ileti göndermek için bağlantı bağlantı larını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="0f233-353">Bu yöntemin bir dezavantajı daha fazla bellek alır olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0f233-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="0f233-354">Hub sınıfındaki bağlantı ömrü olayları nasıl işleyebilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="0f233-355">Bağlantı yaşam boyu olayları işlemeiçin tipik nedenler, bir kullanıcının bağlı olup olmadığını izlemek ve kullanıcı adları ve bağlantı adları arasındaki ilişkilendirme izlemektir.</span><span class="sxs-lookup"><span data-stu-id="0f233-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="0f233-356">İstemciler bağlandığında veya bağlantılarını kestiğinde `OnConnected` `OnDisconnected`kendi `OnReconnected` kodunuzu çalıştırmak için, aşağıdaki örnekte gösterildiği gibi Hub sınıfının ,, ve sanal yöntemlerini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="0f233-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="0f233-357">OnConnected, OnDisconnected ve OnReconnected çağrıldığında</span><span class="sxs-lookup"><span data-stu-id="0f233-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="0f233-358">Bir tarayıcı yeni bir sayfaya her yönlendirilse, yeni bir bağlantı kurulmalıdır, bu da SignalR'In `OnDisconnected` `OnConnected` yöntemi uygulayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="0f233-359">SignalR, yeni bir bağlantı kurulduğunda her zaman yeni bir bağlantı kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f233-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="0f233-360">Bu `OnReconnected` yöntem, SignalR'in bağlantı süreleri kesilmeden önce kablonun geçici olarak bağlantısının kesilmesi ve yeniden bağlanması gibi otomatik olarak kurtarabileceği geçici bir bağlantı sonu olduğunda çağrılır. İstemcinin `OnDisconnected` bağlantısı kesildiğinde ve Tarayıcı yeni bir sayfaya gittiğinde olduğu gibi SignalR otomatik olarak yeniden bağlanadığında yöntem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="0f233-361">Bu nedenle, belirli bir istemci için `OnConnected` `OnReconnected`olası `OnDisconnected`bir olay dizisi , , , ; veya `OnConnected` `OnDisconnected`, .</span><span class="sxs-lookup"><span data-stu-id="0f233-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="0f233-362">Belirli bir bağlantı `OnConnected` `OnDisconnected` `OnReconnected` için sırayı görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="0f233-363">Yöntem, `OnDisconnected` sunucunun çöktüğü veya Uygulama Etki Alanı'nın geri dönüştürülderken olduğu gibi bazı senaryolarda çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="0f233-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="0f233-364">Başka bir sunucu devreye girdiğinde veya App Domain geri dönüşümünü tamamladığında, bazı `OnReconnected` istemciler olayı yeniden bağlayıp ateşleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="0f233-365">Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="0f233-366">Arayan durumu doldurulmamada</span><span class="sxs-lookup"><span data-stu-id="0f233-366">Caller state not populated</span></span>

<span data-ttu-id="0f233-367">Bağlantı ömrü nes'i olay işleyicisi yöntemleri sunucudan çağrılır, bu da istemcideki `state` nesneye koyduğunuz herhangi bir durum için sunucudaki `Caller` özellikte doldurulmayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f233-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="0f233-368">Nesne ve `state` `Caller` özellik hakkında bilgi için, bu konunun ilerleyen saatlerinde [istemciler ve Hub sınıfı arasında durum geçişini nasıl](#passstate) göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="0f233-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="0f233-369">Bağlam özelliğinden istemci hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="0f233-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="0f233-370">İstemci hakkında bilgi almak `Context` için Hub sınıfının özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="0f233-371">Özellik, `Context` aşağıdaki bilgilere erişim sağlayan bir [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) nesnesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="0f233-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="0f233-372">Arayan istemcinin bağlantı kimliği.</span><span class="sxs-lookup"><span data-stu-id="0f233-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="0f233-373">Bağlantı kimliği SignalR tarafından atanan bir GUID'dir (kendi kodunuzdaki değeri belirtemezsiniz).</span><span class="sxs-lookup"><span data-stu-id="0f233-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="0f233-374">Her bağlantı için bir bağlantı kimliği vardır ve uygulamanızda birden çok Hub varsa aynı bağlantı kimliği tüm Hub'lar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="0f233-375">HTTP üstbilgi verileri.</span><span class="sxs-lookup"><span data-stu-id="0f233-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="0f233-376">Ayrıca HTTP başlıkları `Context.Headers`alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="0f233-377">Aynı şey `Context.Headers` için birden çok başvuruiçin nedeni, `Context.Request` ilk oluşturulan, özellik `Context.Headers` daha sonra eklendi ve geriye dönük uyumluluk için tutuldu.</span><span class="sxs-lookup"><span data-stu-id="0f233-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="0f233-378">Dize verilerini sorgula.</span><span class="sxs-lookup"><span data-stu-id="0f233-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="0f233-379">Ayrıca sorgu dize verileri `Context.QueryString`de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="0f233-380">Bu özellikte aldığınız sorgu dizesi, SignalR bağlantısını kuran HTTP isteğiyle kullanılan dizedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="0f233-381">İstemci hakkındaki verileri istemciden sunucuya aktarmanın kullanışlı bir yolu olan bağlantıyı yapılandırarak istemciye sorgu dize parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="0f233-382">Aşağıdaki örnek, oluşturulan proxy'yi kullandığınızda JavaScript istemcisine sorgu dizesi eklemenin bir yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="0f233-383">Sorgu dize parametrelerini ayarlama hakkında daha fazla bilgi için [JavaScript](hubs-api-guide-javascript-client.md) ve [.NET](hubs-api-guide-net-client.md) istemcileri için API kılavuzlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="0f233-384">SignalR tarafından dahili olarak kullanılan diğer bazı değerlerle birlikte sorgu dize verilerinde bağlantı için kullanılan aktarım yöntemini bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0f233-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="0f233-385">Değeri "webSockets", "serverSentEvents", "foreverFrame" veya "longPolling" `transportMethod` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f233-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="0f233-386">`OnConnected` Olay işleyicisi yönteminde bu değeri denetlerseniz, bazı senaryolarda başlangıçta bağlantı için son anlaşmalı aktarım yöntemi olmayan bir aktarım değeri alabileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0f233-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="0f233-387">Bu durumda yöntem bir özel durum oluşturur ve son aktarım yöntemi oluşturulduğunda daha sonra tekrar çağrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f233-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="0f233-388">Kurabiye.</span><span class="sxs-lookup"><span data-stu-id="0f233-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="0f233-389">Ayrıca çerezleri `Context.RequestCookies`de .</span><span class="sxs-lookup"><span data-stu-id="0f233-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="0f233-390">Kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f233-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="0f233-391">İstek için HttpContext nesnesi:</span><span class="sxs-lookup"><span data-stu-id="0f233-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="0f233-392">SinyalR bağlantısı için `HttpContext.Current` `HttpContext` nesneyi almak yerine bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="0f233-393">İstemciler ve Hub sınıfı arasında durum nasıl geçirilir?</span><span class="sxs-lookup"><span data-stu-id="0f233-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="0f233-394">İstemci proxy, sunucuya aktarılmasını istediğiniz verileri her yöntem çağrısıyla depolayabildiğiniz bir `state` nesne sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f233-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="0f233-395">Sunucuda, istemciler tarafından çağrılan `Clients.Caller` Hub yöntemleriyle bu verilere özellikte erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="0f233-396">Özellik `Clients.Caller` bağlantı ömrü olay işleyiciyöntemleri `OnConnected`için doldurulur değil , `OnDisconnected`, ve `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="0f233-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="0f233-397">`state` Nesnede veri oluşturma veya güncelleştirme `Clients.Caller` özelliği her iki yönde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="0f233-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="0f233-398">Sunucudaki değerleri güncelleştirebilirsiniz ve bunlar istemciye geri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="0f233-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="0f233-399">Aşağıdaki örnek, her yöntem çağrısıyla sunucuya iletim için durum depolayan JavaScript istemci kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="0f233-400">Aşağıdaki örnekte bir .NET istemcisinde eşdeğer kod gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="0f233-401">Hub sınıfınızda, bu verilere özellikte `Clients.Caller` erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="0f233-402">Aşağıdaki örnek, önceki örnekte belirtilen durumu alan kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="0f233-403">Kalıcı durum için bu mekanizma büyük miktarda veri için tasarlanmamıştır, çünkü içine `state` koyduğunuz veya `Clients.Caller` özelliğinize koyduğunuz her şey her yöntem çağırmasıyla birlikte tökezler.</span><span class="sxs-lookup"><span data-stu-id="0f233-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="0f233-404">Kullanıcı adları veya sayaçlar gibi daha küçük öğeler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="0f233-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="0f233-405">VB.NET veya güçlü bir şekilde yazılan hub'da, arayan durum nesnesine `Clients.Caller`erişilemez; bunun yerine, kullanın `Clients.CallerState` (SignalR 2.1 tanıtıldı):</span><span class="sxs-lookup"><span data-stu-id="0f233-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="0f233-406">**C'de CallerState'i kullanma #**</span><span class="sxs-lookup"><span data-stu-id="0f233-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="0f233-407">**Visual Basic'te CallerState'i kullanma**</span><span class="sxs-lookup"><span data-stu-id="0f233-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="0f233-408">Hub sınıfındaki hatalar nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="0f233-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="0f233-409">Hub sınıfı yöntemlerinizde oluşan hataları işlemek için, öncelikle async işlemlerinden (istemci yöntemleriçağırmak gibi) özel `await`durumları kullanarak "gözlemlediğinizden" emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f233-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="0f233-410">Ardından aşağıdaki yöntemlerden birini veya birkaçını kullanın:</span><span class="sxs-lookup"><span data-stu-id="0f233-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="0f233-411">Yöntem kodunuzu try-catch bloklarında sarın ve özel durum nesnesini günlüğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f233-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="0f233-412">Hata ayıklama amacıyla istemciye özel durum gönderebilirsiniz, ancak güvenlik nedenleriyle üretimdeki istemcilere ayrıntılı bilgi gönderilmesi önerilmez.</span><span class="sxs-lookup"><span data-stu-id="0f233-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="0f233-413">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) yöntemini işleyen bir Hubs ardışık modül oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f233-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="0f233-414">Aşağıdaki örnekte, hataları günlüğe kaydeden bir ardışık hatlar modülü, ardından modülü Hubs ardışık hattına enjekte eden Startup.cs kod gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f233-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="0f233-415">`HubException` Sınıfı kullanın (SignalR 2'de tanıtıldı).</span><span class="sxs-lookup"><span data-stu-id="0f233-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="0f233-416">Bu hata herhangi bir hub çağırma atılabilir.</span><span class="sxs-lookup"><span data-stu-id="0f233-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="0f233-417">Oluşturucu `HubError` bir dize iletisi ve ek hata verileri depolamak için bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="0f233-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="0f233-418">SignalR özel durumu otomatik olarak serihale getirir ve hub yöntemi çağırmasını reddetmek veya başarısız olmak için kullanılacak istemciye gönderir.</span><span class="sxs-lookup"><span data-stu-id="0f233-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="0f233-419">Aşağıdaki kod örnekleri, Hub `HubException` çağırma sırasında nasıl atılacağını ve JavaScript ve .NET istemcilerinde özel durum nasıl işleyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f233-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="0f233-420">**HubException sınıfını gösteren sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="0f233-421">**Hub'a HubException atmaya yanıt gösteren JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="0f233-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="0f233-422">**.NET istemci kodu hub'a HubException atma yanıtı gösteren**</span><span class="sxs-lookup"><span data-stu-id="0f233-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="0f233-423">Hub ardışık işlem hattı modülleri hakkında daha fazla bilgi için hub'lar ardışık hattını bu konuda nasıl [özelleştirileştirin.](#hubpipeline)</span><span class="sxs-lookup"><span data-stu-id="0f233-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="0f233-424">İzlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-424">How to enable tracing</span></span>

<span data-ttu-id="0f233-425">Sunucu tarafı izlemeyi etkinleştirmek için, bu örnekte gösterildiği gibi Web.config dosyanıza bir system.diagnostics öğesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0f233-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="0f233-426">Uygulamayı Visual Studio'da çalıştırdığınızda, **Çıkış** penceresindeki günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="0f233-427">İstemci yöntemlerini arama ve Hub sınıfı dışından grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="0f233-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="0f233-428">Hub sınıfınızdan farklı bir sınıftan istemci yöntemlerini çağırmak için Hub için SignalR bağlam nesnesine bir başvuru alın ve bunu istemcideki yöntemleri çağırmak veya grupları yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f233-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="0f233-429">Aşağıdaki örnek `StockTicker` sınıf bağlam nesnesini alır, sınıfın bir örneğinde depolar, sınıf örneğini statik bir özellikte depolar ve `updateStockPrice` singleton sınıf örneğindeki `StockTickerHub`bağlamı kullanır, adlı hub'a bağlı istemcilerde yöntemi aramak için .</span><span class="sxs-lookup"><span data-stu-id="0f233-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="0f233-430">Bağlamı uzun ömürlü bir nesnede birden çok kez kullanmanız gerekiyorsa, başvuruyu bir kez alın ve her seferinde yeniden almak yerine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f233-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="0f233-431">Bağlamı bir kez almak, SignalR'ın istemcilere Hub yöntemlerinizin istemci yöntemi çağrıları yaptığı aynı sırayla ileti göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f233-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="0f233-432">Hub için SignalR bağlamını nasıl kullanacağımı gösteren bir öğretici için, [ASP.NET SignalR içeren Sunucu Yayını'na](../getting-started/tutorial-server-broadcast-with-signalr.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="0f233-433">İstemci yöntemlerini arama</span><span class="sxs-lookup"><span data-stu-id="0f233-433">Calling client methods</span></span>

<span data-ttu-id="0f233-434">Hangi istemcilerin RPC'yi alacağını belirtebilirsiniz, ancak Hub sınıfından arama yaptığınızdan daha az seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="0f233-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="0f233-435">Bunun nedeni, bağlamın bir istemciden gelen belirli bir aramayla ilişkili olmamasıdır, bu nedenle geçerli `Clients.Others`bağlantı `Clients.Caller`kimliği `Clients.OthersInGroup`hakkında bilgi gerektiren yöntemler (örneğin, veya , veya , ) kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0f233-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="0f233-436">Aşağıdaki seçenekler mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="0f233-436">The following options are available:</span></span>

- <span data-ttu-id="0f233-437">Tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="0f233-438">Bağlantı kimliğiyle tanımlanan belirli bir istemci.</span><span class="sxs-lookup"><span data-stu-id="0f233-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="0f233-439">Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="0f233-440">Belirli bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="0f233-441">Bağlantı kimliğiyle tanımlanan belirtilen istemciler dışında belirli bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="0f233-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="0f233-442">Hub sınıfınızdaki yöntemlerden Hub olmayan sınıfınızı çağırıyorsanız, geçerli bağlantı kimliğini geçirebilir ve `Clients.Client`bunu `Clients.AllExcept`, `Clients.Group` veya `Clients.Caller` `Clients.Others`simüle `Clients.OthersInGroup`etmek için , veya .</span><span class="sxs-lookup"><span data-stu-id="0f233-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="0f233-443">Aşağıdaki örnekte, `MoveShapeHub` `Broadcaster` sınıf sınıf simüle `Clients.Others` `Broadcaster` böylece sınıfa bağlantı kimliği geçer.</span><span class="sxs-lookup"><span data-stu-id="0f233-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="0f233-444">Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="0f233-444">Managing group membership</span></span>

<span data-ttu-id="0f233-445">Grupları yönetmek için Hub sınıfındakiyle aynı seçeneklere sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f233-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="0f233-446">Gruba istemci ekleme</span><span class="sxs-lookup"><span data-stu-id="0f233-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="0f233-447">İstemciyi gruptan kaldırma</span><span class="sxs-lookup"><span data-stu-id="0f233-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="0f233-448">Hubs ardışık hattı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0f233-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="0f233-449">SignalR, Hub ardışık hattına kendi kodunuzu enjekte etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f233-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="0f233-450">Aşağıdaki örnek, istemciden alınan her gelen yöntem çağrısını ve istemciye çağrılan giden yöntem çağrısını kaydeden özel bir Hub ardışık nokta modülü gösterir:</span><span class="sxs-lookup"><span data-stu-id="0f233-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="0f233-451">*Startup.cs* dosyasındaki aşağıdaki kod, Hub ardışık alanında çalışacak modülü kaydeder:</span><span class="sxs-lookup"><span data-stu-id="0f233-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="0f233-452">Geçersiz kılabileceğiniz birçok farklı yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="0f233-452">There are many different methods that you can override.</span></span> <span data-ttu-id="0f233-453">Tam liste için [HubPipelineModule Yöntemleri'ne](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="0f233-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
