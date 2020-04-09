---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hub'ları API Kılavuzu - .NET İstemci (C#) | Microsoft Dokümanlar
author: bradygaster
description: Bu belge, Windows Mağazası (WinRT), WPF, Silverlight ve eksileri gibi .NET istemcilerinde SignalR sürüm 2 için Hubs API'sını kullanmaya giriş sağlar...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676337"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="31b01-103">ASP.NET SignalR Hub'ları API Kılavuzu - .NET İstemci (C#)</span><span class="sxs-lookup"><span data-stu-id="31b01-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="31b01-104">Bu belge, Windows Mağazası (WinRT), WPF, Silverlight ve konsol uygulamaları gibi .NET istemcilerinde SignalR sürüm 2 için Hubs API'sinin kullanılmasına giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="31b01-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="31b01-105">SignalR Hub'ları API, bir sunucudan bağlı istemcilere ve istemcilerden sunucuya uzaktan yordam aramaları (RPC' ler) yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="31b01-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="31b01-106">Sunucu kodunda, istemciler tarafından çağrılabilen yöntemleri tanımlarsınız ve istemcide çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="31b01-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="31b01-107">İstemci kodunda, sunucudan çağrılabilen yöntemler tanımlarsınız ve sunucuda çalışan yöntemleri çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="31b01-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="31b01-108">SignalR sizin için istemciden sunucuya tüm sıhhi tesisat ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="31b01-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="31b01-109">SignalR ayrıca Kalıcı Bağlantılar adı verilen daha düşük düzeyli bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="31b01-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="31b01-110">SignalR, Hub'lar ve Kalıcı Bağlantılar'a giriş yapmak veya tam bir SignalR uygulamasının nasıl yapılacağını gösteren bir öğretici için [SignalR - Başlarken'](../getting-started/index.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="31b01-111">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="31b01-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="31b01-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="31b01-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="31b01-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="31b01-113">.NET 4.5</span></span>
> - <span data-ttu-id="31b01-114">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="31b01-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="31b01-115">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="31b01-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="31b01-116">SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="31b01-117">Sorular ve yorumlar</span><span class="sxs-lookup"><span data-stu-id="31b01-117">Questions and comments</span></span>
>
> <span data-ttu-id="31b01-118">Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="31b01-119">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b01-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="31b01-120">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="31b01-120">Overview</span></span>

<span data-ttu-id="31b01-121">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="31b01-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="31b01-122">İstemci Kurulumu</span><span class="sxs-lookup"><span data-stu-id="31b01-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="31b01-123">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="31b01-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="31b01-124">Silverlight istemcilerinden etki alanı bağlantıları</span><span class="sxs-lookup"><span data-stu-id="31b01-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="31b01-125">Bağlantı nasıl yapılandırılabilen</span><span class="sxs-lookup"><span data-stu-id="31b01-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="31b01-126">WPF istemcilerinde en fazla eşzamanlı bağlantı sayısı nasıl ayarlanır?</span><span class="sxs-lookup"><span data-stu-id="31b01-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="31b01-127">Sorgu dize parametreleri nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="31b01-128">Taşıma yöntemi nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="31b01-129">HTTP üstbilgi belirtme</span><span class="sxs-lookup"><span data-stu-id="31b01-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="31b01-130">İstemci sertifikaları nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="31b01-131">Hub proxy'si nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="31b01-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="31b01-132">Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="31b01-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="31b01-133">Parametreleri olmayan yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="31b01-134">Parametre türlerini belirleyen parametrelerle ilgili yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="31b01-135">Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="31b01-136">Işleyici nasıl kaldırılır?</span><span class="sxs-lookup"><span data-stu-id="31b01-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="31b01-137">İstemciden sunucu yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="31b01-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="31b01-138">Bağlantı ömrü olayları nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="31b01-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="31b01-139">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="31b01-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="31b01-140">İstemci tarafı günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="31b01-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="31b01-141">Sunucunun çağırabileceği istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="31b01-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="31b01-142">Örnek .NET istemci projeleri için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="31b01-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="31b01-143">[gustavo-armenta / SignalR-Örnekleri](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT, Silverlight, konsol uygulaması örnekleri).</span><span class="sxs-lookup"><span data-stu-id="31b01-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="31b01-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com (WPF örnek).</span><span class="sxs-lookup"><span data-stu-id="31b01-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="31b01-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Konsol uygulaması örneği).</span><span class="sxs-lookup"><span data-stu-id="31b01-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="31b01-146">Sunucu veya JavaScript istemcilerinin nasıl programlanır, aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="31b01-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="31b01-147">SignalR Hub'lar API Kılavuzu - Sunucu</span><span class="sxs-lookup"><span data-stu-id="31b01-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="31b01-148">SignalR Hubs API Kılavuzu - JavaScript İstemci</span><span class="sxs-lookup"><span data-stu-id="31b01-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="31b01-149">API Başvuru konularına bağlantılar, API'nin .NET 4.5 sürümüne bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="31b01-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="31b01-150">.NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="31b01-151">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="31b01-151">Client setup</span></span>

<span data-ttu-id="31b01-152">[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet paketini yükleyin [(Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) paketi değil).</span><span class="sxs-lookup"><span data-stu-id="31b01-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="31b01-153">Bu paket, winrt, Silverlight, WPF, konsol uygulaması ve Windows Phone istemcilerini hem .NET 4 hem de .NET 4.5 için destekler.</span><span class="sxs-lookup"><span data-stu-id="31b01-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="31b01-154">İstemcide olan SignalR sürümü sunucudaki sürümden farklıysa, SignalR genellikle farka uyum sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="31b01-155">Örneğin, SignalR sürüm 2'yi çalıştıran bir sunucu, 1.1.x yüklü istemcilerin yanı sıra sürüm 2 yüklü istemcileri destekler.</span><span class="sxs-lookup"><span data-stu-id="31b01-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="31b01-156">Sunucudaki sürüm ile istemcideki sürüm arasındaki fark çok büyükse veya istemci sunucudan daha yeniyse, `InvalidOperationException` istemci bağlantı kurmaya çalıştığında SignalR bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="31b01-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="31b01-157">Hata iletisi`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" ".</span><span class="sxs-lookup"><span data-stu-id="31b01-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="31b01-158">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="31b01-158">How to establish a connection</span></span>

<span data-ttu-id="31b01-159">Bir bağlantı kuramadan önce, bir `HubConnection` nesne oluşturmanız ve bir proxy oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="31b01-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="31b01-160">Bağlantıyı kurmak `Start` `HubConnection` için, nesne üzerindeki yöntemi arayın.</span><span class="sxs-lookup"><span data-stu-id="31b01-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="31b01-161">JavaScript istemcileri için bağlantıyı kurmak için `Start` yöntemi aramadan önce en az bir olay işleyicisi kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31b01-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="31b01-162">Bu .NET istemcileri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="31b01-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="31b01-163">JavaScript istemcileri için oluşturulan proxy kodu, sunucuda bulunan tüm Hub'lar için otomatik olarak proxy oluşturur ve işleyici kaydetmek, istemcinizin hangi Hub'ları kullanmak istediğini nasıl belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b01-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="31b01-164">Ancak bir .NET istemcisi için Hub proxy'lerini el ile oluşturursunuz, bu nedenle SignalR proxy oluşturduğunuz herhangi bir Hub'ı kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="31b01-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="31b01-165">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/signalr" URL'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="31b01-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="31b01-166">Farklı bir temel URL'nin nasıl belirtilen hakkında bilgi için [signalr hub'ASP.NET API Kılavuzu - Sunucu - /signalr URL'ye](hubs-api-guide-server.md#signalrurl)bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="31b01-167">Yöntem `Start` eşsenkronize yürütülür.</span><span class="sxs-lookup"><span data-stu-id="31b01-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="31b01-168">Sonraki kod satırlarının bağlantı kurulana kadar yürütülmediğinden emin `await` olmak için, ASP.NET 4,5 asynchronous yönteminde veya `.Wait()` senkron yöntemle kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="31b01-169">WinRT istemcisinde kullanmayın. `.Wait()`</span><span class="sxs-lookup"><span data-stu-id="31b01-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="31b01-170">Silverlight istemcilerinden etki alanı bağlantıları</span><span class="sxs-lookup"><span data-stu-id="31b01-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="31b01-171">Silverlight istemcilerinden etki alanı bağlantılarının nasıl etkinleştirilen hakkında bilgi için [bkz.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="31b01-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="31b01-172">Bağlantı nasıl yapılandırılabilen</span><span class="sxs-lookup"><span data-stu-id="31b01-172">How to configure the connection</span></span>

<span data-ttu-id="31b01-173">Bağlantı kurmadan önce, aşağıdaki seçeneklerden herhangi birini belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31b01-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="31b01-174">Eşzamanlı bağlantılar sınırı.</span><span class="sxs-lookup"><span data-stu-id="31b01-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="31b01-175">Dize parametrelerini sorgula.</span><span class="sxs-lookup"><span data-stu-id="31b01-175">Query string parameters.</span></span>
- <span data-ttu-id="31b01-176">Taşıma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="31b01-176">The transport method.</span></span>
- <span data-ttu-id="31b01-177">HTTP üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="31b01-177">HTTP headers.</span></span>
- <span data-ttu-id="31b01-178">İstemci sertifikaları.</span><span class="sxs-lookup"><span data-stu-id="31b01-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="31b01-179">WPF istemcilerinde en fazla eşzamanlı bağlantı sayısı nasıl ayarlanır?</span><span class="sxs-lookup"><span data-stu-id="31b01-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="31b01-180">WPF istemcilerinde, varsayılan değeri olan 2'den en fazla eşzamanlı bağlantı sayısını artırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="31b01-181">Önerilen değer 10'dur.</span><span class="sxs-lookup"><span data-stu-id="31b01-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="31b01-182">Daha fazla bilgi için [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)'e bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="31b01-183">Sorgu dize parametreleri nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-183">How to specify query string parameters</span></span>

<span data-ttu-id="31b01-184">İstemci bağlandığında sunucuya veri göndermek istiyorsanız, sorgu dize parametrelerini bağlantı nesnesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b01-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="31b01-185">Aşağıdaki örnekte, istemci kodunda sorgu dize parametresi nasıl ayarlanır gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="31b01-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="31b01-186">Aşağıdaki örnekte, sunucu kodunda sorgu dize parametresi nasıl okunulup okunulduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="31b01-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="31b01-187">Taşıma yöntemi nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-187">How to specify the transport method</span></span>

<span data-ttu-id="31b01-188">Bağlanma işleminin bir parçası olarak, bir SignalR istemcisi normalde sunucu ile hem sunucu hem de istemci tarafından desteklenen en iyi aktarım belirlemek için görüşür.</span><span class="sxs-lookup"><span data-stu-id="31b01-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="31b01-189">Hangi taşımayı kullanmak istediğinizi zaten biliyorsanız, bu müzakere işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b01-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="31b01-190">Aktarım yöntemini belirtmek için, bir aktarım nesnesi içinde Başlat yöntemine geçirin.</span><span class="sxs-lookup"><span data-stu-id="31b01-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="31b01-191">Aşağıdaki örnek, istemci kodunda aktarım yönteminin nasıl belirtilen gösteriş olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="31b01-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="31b01-192">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) ad alanı, aktarım durumunu belirtmek için kullanabileceğiniz aşağıdaki sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="31b01-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="31b01-193">[LongPollingUlaşım](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="31b01-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="31b01-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="31b01-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="31b01-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Yalnızca sunucu ve istemci .NET 4.5 kullandığında kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="31b01-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="31b01-196">[Otomatik Taşıma](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Otomatik olarak hem istemci hem de sunucu tarafından desteklenen en iyi aktarım seçer.</span><span class="sxs-lookup"><span data-stu-id="31b01-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="31b01-197">Bu varsayılan aktarımdır.</span><span class="sxs-lookup"><span data-stu-id="31b01-197">This is the default transport.</span></span> <span data-ttu-id="31b01-198">Bunu yönteme `Start` aktarmak, hiçbir şeyde geçmamak ile aynı etkiye sahiptir.)</span><span class="sxs-lookup"><span data-stu-id="31b01-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="31b01-199">Yalnızca tarayıcılar tarafından kullanıldığından ForeverFrame aktarımbu listeye dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="31b01-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="31b01-200">Sunucu kodunda aktarım yöntemini nasıl kontrol edeceğimiz hakkında bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Bağlam özelliğinden istemci hakkında nasıl bilgi alınır.](hubs-api-guide-server.md#contextproperty)</span><span class="sxs-lookup"><span data-stu-id="31b01-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="31b01-201">Taşımalar ve geri dönüşler hakkında daha fazla bilgi için [SignalR'a Giriş - Taşımalar ve Geri Dönüşler'](../getting-started/introduction-to-signalr.md#transports)e bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="31b01-202">HTTP üstbilgi belirtme</span><span class="sxs-lookup"><span data-stu-id="31b01-202">How to specify HTTP headers</span></span>

<span data-ttu-id="31b01-203">HTTP üstbilgilerini ayarlamak `Headers` için bağlantı nesnesi üzerindeki özelliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="31b01-204">Aşağıdaki örnekte, http üstbilginin nasıl eklenilebildiğini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="31b01-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="31b01-205">İstemci sertifikaları nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="31b01-205">How to specify client certificates</span></span>

<span data-ttu-id="31b01-206">İstemci sertifikaları eklemek `AddClientCertificate` için bağlantı nesnesi üzerindeki yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="31b01-207">Hub proxy'si nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="31b01-207">How to create the Hub proxy</span></span>

<span data-ttu-id="31b01-208">Hub'ın sunucudan çağırabileceği istemcide yöntemleri tanımlamak ve sunucudaki bir Hub'da yöntemleri çağırmak için bağlantı `CreateHubProxy` nesnesini çağırarak Hub için bir proxy oluşturun.</span><span class="sxs-lookup"><span data-stu-id="31b01-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="31b01-209">Geçtiğiniz dize `CreateHubProxy` Hub sınıfınızın adı veya sunucuda kullanıldıysa `HubName` öznitelik tarafından belirtilen addır.</span><span class="sxs-lookup"><span data-stu-id="31b01-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="31b01-210">Ad eşleştirme büyük/küçük harf duyarsız.</span><span class="sxs-lookup"><span data-stu-id="31b01-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="31b01-211">**Sunucuda hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="31b01-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="31b01-212">**Hub sınıfı için istemci proxy'si oluşturma**</span><span class="sxs-lookup"><span data-stu-id="31b01-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="31b01-213">Hub sınıfınızı bir `HubName` öznitelikle dekore ederseniz, bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="31b01-214">**Sunucuda hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="31b01-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="31b01-215">**Hub sınıfı için istemci proxy'si oluşturma**</span><span class="sxs-lookup"><span data-stu-id="31b01-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="31b01-216">Aynı `HubConnection.CreateHubProxy` `hubName`ile birden çok kez ararsanız, aynı `IHubProxy` önbelleğe alınmış nesneyi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="31b01-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="31b01-217">Sunucunun çağırabileceği istemcide yöntemler nasıl tanımlanır?</span><span class="sxs-lookup"><span data-stu-id="31b01-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="31b01-218">Sunucunun çağırabileceği bir yöntem tanımlamak için, `On` bir olay işleyicisi kaydetmek için proxy yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="31b01-219">Yöntem adı eşleştirme büyük/küçük harf duyarsız.</span><span class="sxs-lookup"><span data-stu-id="31b01-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="31b01-220">Örneğin, `Clients.All.UpdateStockPrice` sunucuda , `updateStockPrice` `updatestockprice`veya `UpdateStockPrice` istemci üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="31b01-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="31b01-221">Farklı istemci platformları, Kullanıcı Arabirimi'ni güncelleştirmek için yöntem kodunu yazma şekliniz için farklı gereksinimlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="31b01-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="31b01-222">Gösterilen örnekler WinRT (Windows Mağazası .NET) istemcileri içindir.</span><span class="sxs-lookup"><span data-stu-id="31b01-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="31b01-223">WPF, Silverlight ve konsol uygulama örnekleri [daha sonra bu konuda ayrı bir bölümde](#wpfsl)verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="31b01-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="31b01-224">Parametreleri olmayan yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-224">Methods without parameters</span></span>

<span data-ttu-id="31b01-225">İşlediğiniz yöntemin parametreleri yoksa, `On` yöntemin genel olmayan aşırı yükünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="31b01-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="31b01-226">**Parametreleri olmadan sunucu kodu arama istemci yöntemi**</span><span class="sxs-lookup"><span data-stu-id="31b01-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="31b01-227">**Parametreleri olmadan sunucudan çağrılan yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="31b01-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="31b01-228">Parametre türlerini belirleyen parametrelerle ilgili yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="31b01-229">İşlediğiniz yöntemin parametreleri varsa, yöntemin genel türleri olarak `On` parametrelerin türlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="31b01-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="31b01-230">En fazla 8 parametre (Windows Phone 7'de 4) belirtmenizi sağlayan `On` yöntemin genel aşırı yüklemeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="31b01-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="31b01-231">Aşağıdaki örnekte, `UpdateStockPrice` yönteme bir parametre gönderilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="31b01-232">**Bir parametre ile sunucu kodu arama istemci yöntemi**</span><span class="sxs-lookup"><span data-stu-id="31b01-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="31b01-233">**Parametre için kullanılan Stok sınıfı**</span><span class="sxs-lookup"><span data-stu-id="31b01-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="31b01-234">**Parametreli sunucudan çağrılan bir yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="31b01-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="31b01-235">Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="31b01-236">Parametreleri yöntemin `On` genel türleri olarak belirtmeye alternatif olarak, parametreleri dinamik nesneler olarak belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31b01-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="31b01-237">**Bir parametre ile sunucu kodu arama istemci yöntemi**</span><span class="sxs-lookup"><span data-stu-id="31b01-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="31b01-238">**Parametre için kullanılan Stok sınıfı**</span><span class="sxs-lookup"><span data-stu-id="31b01-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="31b01-239">**Parametre için dinamik bir nesne kullanarak, parametre ile sunucudan çağrılan bir yöntem için WinRT İstemci kodu ([bu konuda daha sonra WPF ve Silverlight örneklerine bakın](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="31b01-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="31b01-240">Işleyici nasıl kaldırılır?</span><span class="sxs-lookup"><span data-stu-id="31b01-240">How to remove a handler</span></span>

<span data-ttu-id="31b01-241">Bir işleyiciyi kaldırmak `Dispose` için yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="31b01-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="31b01-242">**Sunucudan çağrılan bir yöntem için istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="31b01-243">**İşleyiciyi kaldırmak için istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="31b01-244">İstemciden sunucu yöntemleri nasıl çağrılır?</span><span class="sxs-lookup"><span data-stu-id="31b01-244">How to call server methods from the client</span></span>

<span data-ttu-id="31b01-245">Sunucuda bir yöntem çağırmak için `Invoke` Hub proxy'deki yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="31b01-246">Sunucu yönteminin iade değeri yoksa, `Invoke` yöntemin genel olmayan aşırı yükünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="31b01-247">**İade değeri olmayan bir yöntemiçin sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="31b01-248">**İade değeri olmayan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="31b01-249">Sunucu yönteminin iade değeri varsa, yöntemin genel türü `Invoke` olarak iade türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="31b01-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="31b01-250">**İade değeri olan ve karmaşık bir tür parametresi alan bir yöntemiçin sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="31b01-251">**Parametre ve iade değeri için kullanılan Stok sınıfı**</span><span class="sxs-lookup"><span data-stu-id="31b01-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="31b01-252">**Bir ASP.NET 4,5 async yönteminde, geri dönüş değeri olan ve karmaşık bir tür parametresi alan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="31b01-253">**Eşdönme değeri olan ve eşzamanlı bir yöntemde karmaşık bir tür parametresi alan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="31b01-254">Yöntem `Invoke` eşsenkronize yürütülür ve `Task` bir nesneyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="31b01-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="31b01-255">Belirtmezseniz `await` veya, `.Wait()`çağırdığınız yöntem yürütme tamamlanmadan önce bir sonraki kod satırı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="31b01-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="31b01-256">Bağlantı ömrü olayları nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="31b01-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="31b01-257">SignalR işleyebilir aşağıdaki bağlantı ömrü olayları sağlar:</span><span class="sxs-lookup"><span data-stu-id="31b01-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="31b01-258">`Received`: Bağlantıdan herhangi bir veri alındığı zaman yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="31b01-259">Alınan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="31b01-259">Provides the received data.</span></span>
- <span data-ttu-id="31b01-260">`ConnectionSlow`: İstemci yavaş veya sık sık bırakarak bağlantı algıladığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="31b01-261">`Reconnecting`: Altta yatan aktarım yeniden bağlanmaya başladığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="31b01-262">`Reconnected`: Temel taşıma yeniden bağlandığında yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="31b01-263">`StateChanged`: Bağlantı durumu değiştiğinde yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="31b01-264">Eski durumu ve yeni durumu sağlar.</span><span class="sxs-lookup"><span data-stu-id="31b01-264">Provides the old state and the new state.</span></span> <span data-ttu-id="31b01-265">Bağlantı durumu değerleri hakkında bilgi için Bkz. [ConnectionState Numaralandırma.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="31b01-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="31b01-266">`Closed`: Bağlantı kesildiğinde yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="31b01-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="31b01-267">Örneğin, önemli olmayan ancak bağlantının yavaşlığı veya sık sık düşmesi gibi aralıklı bağlantı sorunlarına neden olan `ConnectionSlow` hatalar için uyarı iletileri görüntülemek istiyorsanız, olayı işleyin.</span><span class="sxs-lookup"><span data-stu-id="31b01-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="31b01-268">Daha fazla bilgi için [SignalR'deki Bağlantı Yaşam Boyu Olayları Anlama ve İşleme'ye](handling-connection-lifetime-events.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="31b01-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="31b01-269">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="31b01-269">How to handle errors</span></span>

<span data-ttu-id="31b01-270">Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, SignalR'ın hatadan sonra döndürdİğİ özel durum nesnesi hata hakkında en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="31b01-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="31b01-271">Örneğin, bir çağrı `newContosoChatMessage` başarısız olursa, hata nesnesindeki`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`hata iletisi " " Üretimdeki istemcilere ayrıntılı hata iletileri göndermek güvenlik nedenleriyle önerilmez, ancak sorun giderme amacıyla ayrıntılı hata iletilerini etkinleştirmek istiyorsanız, sunucudaki aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="31b01-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="31b01-272">SignalR'ın kaldırdığı hataları işlemek için bağlantı `Error` nesnesindeki olay için bir işleyici ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b01-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="31b01-273">Yöntem çağrılarından gelen hataları işlemek için kodu try-catch bloğuna sarın.</span><span class="sxs-lookup"><span data-stu-id="31b01-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="31b01-274">İstemci tarafı günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="31b01-274">How to enable client-side logging</span></span>

<span data-ttu-id="31b01-275">İstemci tarafı günlüğe `TraceLevel` kaydetmeyi etkinleştirmek için bağlantı nesnesi üzerindeki ve `TraceWriter` özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="31b01-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="31b01-276">Sunucunun çağırabileceği istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="31b01-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="31b01-277">Sunucunun çağırabileceği istemci yöntemlerini tanımlamak için daha önce gösterilen kod örnekleri WinRT istemcilerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="31b01-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="31b01-278">Aşağıdaki örnekler WPF, Silverlight ve konsol uygulama istemcileri için eşdeğer kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="31b01-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="31b01-279">Parametreleri olmayan yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-279">Methods without parameters</span></span>

<span data-ttu-id="31b01-280">**Parametreleri olmadan sunucudan çağrılan yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="31b01-281">**Parametreleri olmadan sunucudan çağrılan yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="31b01-282">**Parametreleri olmadan sunucudan çağrılan yöntem için konsol uygulaması istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="31b01-283">Parametre türlerini belirleyen parametrelerle ilgili yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="31b01-284">**Parametreli sunucudan çağrılan bir yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="31b01-285">**Parametreli sunucudan çağrılan bir yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="31b01-286">**Parametreli sunucudan çağrılan bir yöntem için konsol uygulaması istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="31b01-287">Parametreler için dinamik nesneleri belirleyen parametreleri içeren yöntemler</span><span class="sxs-lookup"><span data-stu-id="31b01-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="31b01-288">**Parametre için dinamik bir nesne kullanarak, parametreile sunucudan çağrılan bir yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="31b01-289">**Parametre için dinamik bir nesne kullanarak, parametreile sunucudan çağrılan bir yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="31b01-290">**Parametre için dinamik bir nesne kullanarak, parametre ile sunucudan çağrılan bir yöntem için konsol uygulama istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="31b01-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
