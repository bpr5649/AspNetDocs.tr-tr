---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR hub 'Ları API Kılavuzu-.NET Istemcisi (C#) | Microsoft Docs
author: bradygaster
description: Bu belge, .NET istemcilerindeki SignalR sürüm 2 için Windows Mağazası (WinRT), WPF, Silverlight ve dezavantajlar gibi hub API 'leri kullanma hakkında bir giriş sağlar.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345548"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="6eccc-103">ASP.NET SignalR hub 'Ları API Kılavuzu-.NET Istemcisi (C#)</span><span class="sxs-lookup"><span data-stu-id="6eccc-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="6eccc-104">Bu belge, .NET istemcilerindeki SignalR sürüm 2 için Windows Mağazası (WinRT), WPF, Silverlight ve konsol uygulamaları gibi hub API 'leri kullanma hakkında bir giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="6eccc-105">SignalR hub 'Ları API 'SI, uzak yordam çağrılarını (RPC) bir sunucudan, istemcilerden ve istemcilerden sunucuya bağlı hale getirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="6eccc-106">Sunucu kodu ' nda, istemciler tarafından çağrılabilen Yöntemler tanımlar ve istemcide çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eccc-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="6eccc-107">İstemci kodunda, sunucudan çağrılabilen yöntemleri tanımlayabilir ve sunucuda çalışan yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eccc-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="6eccc-108">SignalR, sizin için istemciden sunucuya sıhhi kını ele alır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="6eccc-109">SignalR Ayrıca kalıcı bağlantılar adlı alt düzey bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="6eccc-110">SignalR, hub 'Lar ve sürekli bağlantılara giriş veya tam bir SignalR uygulamasının nasıl oluşturulduğunu gösteren bir öğretici için bkz. [SignalR-Başlarken](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="6eccc-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="6eccc-111">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="6eccc-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="6eccc-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6eccc-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="6eccc-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6eccc-113">.NET 4.5</span></span>
> - <span data-ttu-id="6eccc-114">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="6eccc-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="6eccc-115">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="6eccc-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="6eccc-116">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="6eccc-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="6eccc-117">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6eccc-117">Questions and comments</span></span>
>
> <span data-ttu-id="6eccc-118">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="6eccc-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6eccc-119">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eccc-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="6eccc-120">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6eccc-120">Overview</span></span>

<span data-ttu-id="6eccc-121">Bu belgede aşağıdaki bölümler yer alır:</span><span class="sxs-lookup"><span data-stu-id="6eccc-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="6eccc-122">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="6eccc-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="6eccc-123">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="6eccc-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="6eccc-124">Silverlight istemcilerinden etki alanları arası bağlantılar</span><span class="sxs-lookup"><span data-stu-id="6eccc-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="6eccc-125">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="6eccc-126">WPF istemcilerinde en fazla eşzamanlı bağlantı sayısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="6eccc-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="6eccc-127">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="6eccc-128">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="6eccc-129">HTTP üst bilgilerini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="6eccc-130">İstemci sertifikalarını belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="6eccc-131">Merkez proxy oluşturma</span><span class="sxs-lookup"><span data-stu-id="6eccc-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="6eccc-132">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="6eccc-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="6eccc-133">Parametreleri olmayan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="6eccc-134">Parametre türlerini belirterek parametreleri olan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="6eccc-135">Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="6eccc-136">Bir işleyiciyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="6eccc-137">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="6eccc-138">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="6eccc-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="6eccc-139">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="6eccc-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="6eccc-140">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6eccc-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="6eccc-141">Sunucunun çağıra, istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="6eccc-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="6eccc-142">Örnek bir .NET istemci projeleri için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="6eccc-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="6eccc-143">[Gustavo-Ermenistan ta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT, Silverlight, konsol uygulama örnekleri) üzerinde örnekler.</span><span class="sxs-lookup"><span data-stu-id="6eccc-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="6eccc-144">GitHub.com üzerinde [Dadmıanedödüller/SignalR-MoveShapeDemo/MoveShape. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF örneği).</span><span class="sxs-lookup"><span data-stu-id="6eccc-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="6eccc-145">[SignalR/Microsoft. Aspnet. SignalR. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (konsol uygulaması örneği).</span><span class="sxs-lookup"><span data-stu-id="6eccc-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="6eccc-146">Sunucu veya JavaScript istemcilerini programmaya yönelik belgeler için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="6eccc-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="6eccc-147">SignalR hub 'Ları API Kılavuzu-sunucu</span><span class="sxs-lookup"><span data-stu-id="6eccc-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="6eccc-148">SignalR hub 'Ları API Kılavuzu-JavaScript Istemcisi</span><span class="sxs-lookup"><span data-stu-id="6eccc-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="6eccc-149">API başvuru konularına bağlantılar, API 'nin .NET 4,5 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="6eccc-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="6eccc-150">.NET 4 kullanıyorsanız, [API konularının .NET 4 sürümüne](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="6eccc-151">İstemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="6eccc-151">Client setup</span></span>

<span data-ttu-id="6eccc-152">[Microsoft. Aspnet. SignalR. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet paketini ( [Microsoft. Aspnet. SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) paketini değil) yükler.</span><span class="sxs-lookup"><span data-stu-id="6eccc-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="6eccc-153">Bu paket, .NET 4 ve .NET 4,5 için WinRT, Silverlight, WPF, konsol uygulaması ve Windows Phone istemcilerini destekler.</span><span class="sxs-lookup"><span data-stu-id="6eccc-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="6eccc-154">İstemci üzerindeki SignalR sürümü, sunucuda sahip olduğunuz sürümden farklıysa, SignalR genellikle farka uyum sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="6eccc-155">Örneğin, SignalR sürüm 2 çalıştıran bir sunucu, 1.1. x yüklü olan istemcileri ve sürüm 2 ' nin yüklü olduğu İstemcileri destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="6eccc-156">Sunucu üzerindeki sürüm ile istemcideki sürüm arasındaki fark çok harika ise veya istemci sunucudan daha yeniyse, `InvalidOperationException` istemci bir bağlantı kurmaya çalıştığında SignalR bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6eccc-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="6eccc-157">Hata iletisi " `You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X` ".</span><span class="sxs-lookup"><span data-stu-id="6eccc-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="6eccc-158">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="6eccc-158">How to establish a connection</span></span>

<span data-ttu-id="6eccc-159">Bir bağlantı kurmadan önce bir `HubConnection` nesnesi oluşturmanız ve proxy oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="6eccc-160">Bağlantıyı kurmak için `Start` nesnesi üzerinde yöntemini çağırın `HubConnection` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="6eccc-161">JavaScript istemcileri için, `Start` bağlantıyı kurmak üzere yöntemini çağırmadan önce en az bir olay işleyicisini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="6eccc-162">.NET istemcileri için bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="6eccc-163">JavaScript istemcileri için, oluşturulan proxy kodu, sunucuda var olan tüm Hub 'Lar için otomatik olarak proxy oluşturur ve bir işleyiciyi kaydetmek, istemcinizin hangi hub 'Ları kullandığını belirtebilmeniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="6eccc-164">Ancak, bir .NET istemcisi için hub proxy 'leri el ile oluşturursunuz. SignalR, için proxy oluşturduğunuz herhangi bir hub kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="6eccc-165">Örnek kod, SignalR hizmetinize bağlanmak için varsayılan "/SignalR" URL 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="6eccc-166">Farklı bir temel URL belirtme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-/SignalR URL 'si](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="6eccc-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="6eccc-167">`Start`Yöntemi zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="6eccc-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="6eccc-168">Sonraki kod satırlarının bağlantı kurulana kadar yürütülmediği için, `await` ASP.NET 4,5 zaman uyumsuz bir yöntemde veya `.Wait()` zaman uyumlu bir yöntemde kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="6eccc-169">`.Wait()`Bir WinRT istemcisinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="6eccc-170">Silverlight istemcilerinden etki alanları arası bağlantılar</span><span class="sxs-lookup"><span data-stu-id="6eccc-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="6eccc-171">Silverlight istemcilerinden etki alanları arası bağlantıları etkinleştirme hakkında daha fazla bilgi için bkz. [bir hizmeti etki alanı sınırları genelinde kullanılabilir hale getirme](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="6eccc-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="6eccc-172">Bağlantıyı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-172">How to configure the connection</span></span>

<span data-ttu-id="6eccc-173">Bir bağlantı kurmadan önce, aşağıdaki seçeneklerden herhangi birini belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6eccc-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="6eccc-174">Eşzamanlı bağlantı sınırı.</span><span class="sxs-lookup"><span data-stu-id="6eccc-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="6eccc-175">Sorgu dizesi parametreleri.</span><span class="sxs-lookup"><span data-stu-id="6eccc-175">Query string parameters.</span></span>
- <span data-ttu-id="6eccc-176">Taşıma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6eccc-176">The transport method.</span></span>
- <span data-ttu-id="6eccc-177">HTTP üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="6eccc-177">HTTP headers.</span></span>
- <span data-ttu-id="6eccc-178">İstemci sertifikaları.</span><span class="sxs-lookup"><span data-stu-id="6eccc-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="6eccc-179">WPF istemcilerinde en fazla eşzamanlı bağlantı sayısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="6eccc-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="6eccc-180">WPF istemcilerinde, en fazla eş zamanlı bağlantı sayısını varsayılan 2 değerinden artırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="6eccc-181">Önerilen değer 10 ' dur.</span><span class="sxs-lookup"><span data-stu-id="6eccc-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="6eccc-182">Daha fazla bilgi için bkz. [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eccc-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="6eccc-183">Sorgu dizesi parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-183">How to specify query string parameters</span></span>

<span data-ttu-id="6eccc-184">İstemci bağlandığı zaman sunucuya veri göndermek istiyorsanız, bağlantı nesnesine sorgu dizesi parametreleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eccc-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="6eccc-185">Aşağıdaki örnekte, istemci kodunda bir sorgu dizesi parametresinin nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="6eccc-186">Aşağıdaki örnek, sunucu kodundaki bir sorgu dizesi parametresinin nasıl okunacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="6eccc-187">Taşıma yöntemini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-187">How to specify the transport method</span></span>

<span data-ttu-id="6eccc-188">Bağlantı sürecinin bir parçası olarak, bir SignalR istemcisi normalde sunucu ve istemci tarafından desteklenen en iyi aktarımı tespit etmek üzere sunucuyla görüşür.</span><span class="sxs-lookup"><span data-stu-id="6eccc-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="6eccc-189">Kullanmak istediğiniz taşımayı zaten biliyorsanız, bu anlaşma işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eccc-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="6eccc-190">Taşıma yöntemini belirtmek için, başlangıç yöntemine bir taşıma nesnesi geçirin.</span><span class="sxs-lookup"><span data-stu-id="6eccc-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="6eccc-191">Aşağıdaki örnek, istemci kodunda taşıma yönteminin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="6eccc-192">[Microsoft. Aspnet. SignalR. Client. taşımalar](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) ad alanı, taşımayı belirtmek için kullanabileceğiniz aşağıdaki sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="6eccc-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="6eccc-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="6eccc-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="6eccc-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="6eccc-195">[Websockettransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (yalnızca hem sunucu hem de istemci .NET 4,5 ' i kullanırken kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="6eccc-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="6eccc-196">Otomatik [Aktarım](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (hem istemci hem de sunucu tarafından desteklenen en iyi aktarımı otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="6eccc-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="6eccc-197">Bu, varsayılan aktarımdır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-197">This is the default transport.</span></span> <span data-ttu-id="6eccc-198">Bunu yöntemine geçirmek, `Start` hiçbir şeyi geçirmeyen aynı etkiye sahiptir.)</span><span class="sxs-lookup"><span data-stu-id="6eccc-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="6eccc-199">Yalnızca tarayıcılar tarafından kullanıldığından, ForeverFrame taşıması bu listeye dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="6eccc-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="6eccc-200">Sunucu kodundaki aktarım yöntemini denetleme hakkında daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-bağlam özelliğinden istemci hakkında bilgi alma](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="6eccc-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="6eccc-201">Aktarımlar ve geri göndermeler hakkında daha fazla bilgi için bkz. [SignalR 'ye giriş-aktarımlar ve geri göndermeler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="6eccc-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="6eccc-202">HTTP üst bilgilerini belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-202">How to specify HTTP headers</span></span>

<span data-ttu-id="6eccc-203">HTTP üst bilgilerini ayarlamak için `Headers` bağlantı nesnesindeki özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="6eccc-204">Aşağıdaki örnek, bir HTTP üst bilgisinin nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="6eccc-205">İstemci sertifikalarını belirtme</span><span class="sxs-lookup"><span data-stu-id="6eccc-205">How to specify client certificates</span></span>

<span data-ttu-id="6eccc-206">İstemci sertifikaları eklemek için `AddClientCertificate` bağlantı nesnesindeki yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="6eccc-207">Merkez proxy oluşturma</span><span class="sxs-lookup"><span data-stu-id="6eccc-207">How to create the Hub proxy</span></span>

<span data-ttu-id="6eccc-208">İstemcideki bir hub 'ın sunucudan çağırabildiği ve sunucudaki bir hub 'da Yöntemler çağırabileceği yöntemleri tanımlamak için, bağlantı nesnesini çağırarak Hub için bir ara sunucu oluşturun `CreateHubProxy` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="6eccc-209">' A geçirdiğiniz dize, `CreateHubProxy` hub sınıfınızın adı veya `HubName` bir sunucu üzerinde kullanılmışsa öznitelik tarafından belirtilen addır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="6eccc-210">Ad eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="6eccc-211">**Sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="6eccc-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="6eccc-212">**Hub sınıfı için istemci ara sunucusu oluşturma**</span><span class="sxs-lookup"><span data-stu-id="6eccc-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="6eccc-213">Hub sınıfınızı bir özniteliğiyle süslemek istiyorsanız `HubName` , bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="6eccc-214">**Sunucudaki hub sınıfı**</span><span class="sxs-lookup"><span data-stu-id="6eccc-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="6eccc-215">**Hub sınıfı için istemci ara sunucusu oluşturma**</span><span class="sxs-lookup"><span data-stu-id="6eccc-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="6eccc-216">`HubConnection.CreateHubProxy`Aynı ile birden çok kez çağrı yaparsanız `hubName` , aynı önbelleğe alınmış `IHubProxy` nesneyi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6eccc-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="6eccc-217">İstemcide sunucunun çağırabir yöntemi tanımlama</span><span class="sxs-lookup"><span data-stu-id="6eccc-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="6eccc-218">Sunucunun çağırabir yöntemi tanımlamak için, `On` bir olay işleyicisini kaydetmek üzere proxy 'nin metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="6eccc-219">Yöntem adı eşleştirme, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="6eccc-220">Örneğin, `Clients.All.UpdateStockPrice` sunucusunda, `updateStockPrice` `updatestockprice` veya istemcisinde yürütülür `UpdateStockPrice` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="6eccc-221">Farklı istemci platformları, Kullanıcı arabirimini güncelleştirmek için yöntem kodu yazma konusunda farklı gereksinimlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="6eccc-222">Gösterilen örnekler, WinRT (Windows Mağazası .NET) istemcileri içindir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="6eccc-223">WPF, Silverlight ve konsol uygulaması örnekleri, [Bu konunun ilerleyen kısımlarında ayrı bir bölümde](#wpfsl)sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6eccc-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="6eccc-224">Parametreleri olmayan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-224">Methods without parameters</span></span>

<span data-ttu-id="6eccc-225">İşlemekte olduğunuz yöntemin parametreleri yoksa, yöntemin genel olmayan aşırı yüklemesini kullanın `On` :</span><span class="sxs-lookup"><span data-stu-id="6eccc-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="6eccc-226">**Parametre olmadan istemci yöntemini çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="6eccc-227">**Parametresiz sunucudan çağrılan yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında bulunan WPF ve Silverlight örneklerine bakın](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="6eccc-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="6eccc-228">Parametre türlerini belirterek parametreleri olan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="6eccc-229">İşlemekte olduğunuz yöntemin parametreleri varsa, yöntemin genel türleri olarak parametre türlerini belirtin `On` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="6eccc-230">`On`8 ' e kadar parametre belirtmenizi sağlayan metodun genel aşırı yüklemeleri vardır (Windows Phone 7 üzerinde 4).</span><span class="sxs-lookup"><span data-stu-id="6eccc-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="6eccc-231">Aşağıdaki örnekte yöntemine bir parametre gönderilir `UpdateStockPrice` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="6eccc-232">**İstemci yöntemini bir parametre ile çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="6eccc-233">**Parametresi için kullanılan hisse senedi sınıfı**</span><span class="sxs-lookup"><span data-stu-id="6eccc-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="6eccc-234">**Parametresi ile sunucudan çağrılan bir yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında yer alarak WPF ve Silverlight örneklerine bakın](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="6eccc-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="6eccc-235">Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="6eccc-236">Yöntemin genel türleri olarak parametre belirtmeye alternatif olarak `On` , parametreleri dinamik nesneler olarak belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6eccc-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="6eccc-237">**İstemci yöntemini bir parametre ile çağıran sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="6eccc-238">**Parametresi için kullanılan hisse senedi sınıfı**</span><span class="sxs-lookup"><span data-stu-id="6eccc-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="6eccc-239">**Parametresi için dinamik bir nesne kullanan ve parametresi için bir parametre içeren sunucudan çağrılan bir yöntem için WinRT Istemci kodu ([Bu konunun ilerleyen kısımlarında yer almaktadır WPF ve Silverlight örnekleri](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="6eccc-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="6eccc-240">Bir işleyiciyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-240">How to remove a handler</span></span>

<span data-ttu-id="6eccc-241">Bir işleyiciyi kaldırmak için `Dispose` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="6eccc-242">**Sunucudan çağrılan bir yöntem için istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="6eccc-243">**İşleyiciyi kaldırmak için istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="6eccc-244">İstemciden sunucu yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="6eccc-244">How to call server methods from the client</span></span>

<span data-ttu-id="6eccc-245">Sunucuda bir yöntemi çağırmak için `Invoke` hub proxy üzerinde yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="6eccc-246">Sunucu yönteminin dönüş değeri yoksa, yöntemin genel olmayan aşırı yüklemesini kullanın `Invoke` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="6eccc-247">**Dönüş değeri olmayan bir yöntem için sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="6eccc-248">**Dönüş değeri olmayan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="6eccc-249">Sunucu yönteminin bir dönüş değeri varsa, dönüş türünü metodun genel türü olarak belirtin `Invoke` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="6eccc-250">**Dönüş değerine sahip ve karmaşık bir tür parametresi alan bir yöntem için sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="6eccc-251">**Parametre ve dönüş değeri için kullanılan hisse senedi sınıfı**</span><span class="sxs-lookup"><span data-stu-id="6eccc-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="6eccc-252">**Bir ASP.NET 4,5 zaman uyumsuz yönteminde dönüş değeri olan ve karmaşık tür parametresi alan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="6eccc-253">**Bir dönüş değeri olan ve bir karmaşık tür parametresi alan ve bir zaman uyumlu yöntemde olan bir yöntemi çağıran istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="6eccc-254">`Invoke`Yöntemi zaman uyumsuz olarak yürütülür ve bir `Task` nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="6eccc-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="6eccc-255">`await`Ya da belirtmezseniz `.Wait()` , bir sonraki kod satırı, çağırabileceğiniz yöntemin yürütmeyi bitirinceye kadar yürütülür.</span><span class="sxs-lookup"><span data-stu-id="6eccc-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="6eccc-256">Bağlantı ömrü olaylarını işleme</span><span class="sxs-lookup"><span data-stu-id="6eccc-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="6eccc-257">SignalR, işleyebilmeniz için aşağıdaki bağlantı ömrü olaylarını sağlar:</span><span class="sxs-lookup"><span data-stu-id="6eccc-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="6eccc-258">`Received`: Bağlantıda herhangi bir veri alındığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="6eccc-259">Alınan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-259">Provides the received data.</span></span>
- <span data-ttu-id="6eccc-260">`ConnectionSlow`: İstemci yavaş veya sık bırakma bağlantısı algıladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="6eccc-261">`Reconnecting`: Temeldeki aktarım yeniden bağlanmaya başladığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="6eccc-262">`Reconnected`: Temeldeki aktarım yeniden bağlandığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="6eccc-263">`StateChanged`: Bağlantı durumu değiştiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="6eccc-264">Eski durumu ve yeni durumu sağlar.</span><span class="sxs-lookup"><span data-stu-id="6eccc-264">Provides the old state and the new state.</span></span> <span data-ttu-id="6eccc-265">Bağlantı durumu değerleri hakkında daha fazla bilgi için bkz. [ConnectionState numaralandırması](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="6eccc-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="6eccc-266">`Closed`: Bağlantının bağlantısı kesildiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="6eccc-267">Örneğin, önemli olmayan hatalar için uyarı iletileri göstermek istiyorsanız, ancak bağlantının yavaşlılığını veya sık olarak düşürülmesi gibi aralıklı bağlantı sorunlarına neden olursa `ConnectionSlow` olayı işleyin.</span><span class="sxs-lookup"><span data-stu-id="6eccc-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="6eccc-268">Daha fazla bilgi için bkz. [SignalR 'de bağlantı ömrü olaylarını anlama ve işleme](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="6eccc-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="6eccc-269">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="6eccc-269">How to handle errors</span></span>

<span data-ttu-id="6eccc-270">Sunucuda ayrıntılı hata iletilerini açıkça etkinleştirmezseniz, bir hatadan sonra SignalR 'nin döndürdüğü özel durum nesnesi hata hakkında en az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="6eccc-271">Örneğin, bir çağrı `newContosoChatMessage` başarısız olursa, hata nesnesindeki hata iletisi, `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` Güvenlik nedenleriyle, üretimde istemcilere ayrıntılı hata iletileri gönderilmesi önerilmez, ancak sorun giderme amacıyla ayrıntılı hata iletileri etkinleştirmek istiyorsanız, sunucuda aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="6eccc-272">SignalR 'nin yükselten hataları işlemek için bağlantı nesnesine olay için bir işleyici ekleyebilirsiniz `Error` .</span><span class="sxs-lookup"><span data-stu-id="6eccc-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="6eccc-273">Yöntem etkinleştirmeleri içindeki hataları işlemek için, kodu bir try-catch bloğunda sarın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="6eccc-274">İstemci tarafı günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6eccc-274">How to enable client-side logging</span></span>

<span data-ttu-id="6eccc-275">İstemci tarafı günlük kaydını etkinleştirmek için, `TraceLevel` `TraceWriter` bağlantı nesnesindeki ve özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6eccc-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="6eccc-276">Sunucunun çağıra, istemci yöntemleri için WPF, Silverlight ve konsol uygulama kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="6eccc-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="6eccc-277">Daha önce sunucunun, WinRT istemcilerine uygulama çağırabilecek istemci yöntemleri tanımlamak için gösterilen kod örnekleri.</span><span class="sxs-lookup"><span data-stu-id="6eccc-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="6eccc-278">Aşağıdaki örnekler WPF, Silverlight ve konsol uygulama istemcileri için eşdeğer kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6eccc-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="6eccc-279">Parametreleri olmayan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-279">Methods without parameters</span></span>

<span data-ttu-id="6eccc-280">**Parametre olmadan sunucudan çağrılan yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="6eccc-281">**Parametresiz sunucudan çağrılan yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="6eccc-282">**Parametre olmadan sunucudan çağrılan yöntem için konsol uygulaması istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="6eccc-283">Parametre türlerini belirterek parametreleri olan Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="6eccc-284">**Bir parametre ile sunucudan çağrılan bir yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="6eccc-285">**Bir parametre ile sunucudan çağrılan bir yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="6eccc-286">**Bir parametre ile sunucudan çağrılan bir yöntem için konsol uygulaması istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="6eccc-287">Parametreleri için dinamik nesneler belirten parametrelere sahip Yöntemler</span><span class="sxs-lookup"><span data-stu-id="6eccc-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="6eccc-288">**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntem için WPF istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="6eccc-289">**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntem için Silverlight istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="6eccc-290">**Parametresi için dinamik bir nesne kullanarak, bir parametresiyle sunucudan çağrılan bir yöntemin konsol uygulama istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="6eccc-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
