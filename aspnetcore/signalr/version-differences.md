---
title: SignalR ve ASP.NET Core SignalR arasındaki farklar
author: bradygaster
description: SignalR ve ASP.NET Core SignalR arasındaki farklar
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.date: 11/14/2018
uid: signalr/version-differences
ms.openlocfilehash: 091fc44fccf820a394e7c6f775700c85bebc9101
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072714"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="e6ee7-103">ASP.NET SignalR ile ASP.NET Core SignalR arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-103">Differences between ASP.NET SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="e6ee7-104">ASP.NET Core SignalR istemciler veya sunucular için ASP.NET SignalR ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-104">ASP.NET Core SignalR isn't compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="e6ee7-105">Bu makalede, kaldırılmış veya ASP.NET Core SignalR öğesinde değiştirilen özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-105">This article details features which have been removed or changed in ASP.NET Core SignalR.</span></span>

## <a name="how-to-identify-the-signalr-version"></a><span data-ttu-id="e6ee7-106">SignalR sürüm belirleme</span><span class="sxs-lookup"><span data-stu-id="e6ee7-106">How to identify the SignalR version</span></span>

|                      | <span data-ttu-id="e6ee7-107">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="e6ee7-107">ASP.NET SignalR</span></span> | <span data-ttu-id="e6ee7-108">ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="e6ee7-108">ASP.NET Core SignalR</span></span> |
| -------------------- | --------------- | -------------------- |
| <span data-ttu-id="e6ee7-109">Sunucu NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="e6ee7-109">Server NuGet Package</span></span> | [<span data-ttu-id="e6ee7-110">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="e6ee7-110">Microsoft.AspNet.SignalR</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | <span data-ttu-id="e6ee7-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="e6ee7-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span></span><br><span data-ttu-id="e6ee7-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="e6ee7-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span></span> |
| <span data-ttu-id="e6ee7-113">İstemci NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="e6ee7-113">Client NuGet Packages</span></span> | [<span data-ttu-id="e6ee7-114">Microsoft.AspNet.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="e6ee7-114">Microsoft.AspNet.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[<span data-ttu-id="e6ee7-115">Microsoft.AspNet.SignalR.JS</span><span class="sxs-lookup"><span data-stu-id="e6ee7-115">Microsoft.AspNet.SignalR.JS</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [<span data-ttu-id="e6ee7-116">Microsoft.AspNetCore.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="e6ee7-116">Microsoft.AspNetCore.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| <span data-ttu-id="e6ee7-117">İstemci npm paket</span><span class="sxs-lookup"><span data-stu-id="e6ee7-117">Client npm Package</span></span> | [<span data-ttu-id="e6ee7-118">signalr</span><span class="sxs-lookup"><span data-stu-id="e6ee7-118">signalr</span></span>](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| <span data-ttu-id="e6ee7-119">Java istemci</span><span class="sxs-lookup"><span data-stu-id="e6ee7-119">Java Client</span></span> | <span data-ttu-id="e6ee7-120">[GitHub deposu](https://github.com/SignalR/java-client) (kullanım dışı)</span><span class="sxs-lookup"><span data-stu-id="e6ee7-120">[GitHub Repository](https://github.com/SignalR/java-client) (deprecated)</span></span>  | <span data-ttu-id="e6ee7-121">Maven paket [com.microsoft.signalr](https://search.maven.org/artifact/com.microsoft.signalr/signalr)</span><span class="sxs-lookup"><span data-stu-id="e6ee7-121">Maven package [com.microsoft.signalr](https://search.maven.org/artifact/com.microsoft.signalr/signalr)</span></span> |
| <span data-ttu-id="e6ee7-122">Sunucu uygulama türü</span><span class="sxs-lookup"><span data-stu-id="e6ee7-122">Server App Type</span></span> | <span data-ttu-id="e6ee7-123">ASP.NET (System.Web) veya OWIN barındırma</span><span class="sxs-lookup"><span data-stu-id="e6ee7-123">ASP.NET (System.Web) or OWIN Self-Host</span></span> | <span data-ttu-id="e6ee7-124">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e6ee7-124">ASP.NET Core</span></span> |
| <span data-ttu-id="e6ee7-125">Desteklenen sunucu platformları</span><span class="sxs-lookup"><span data-stu-id="e6ee7-125">Supported Server Platforms</span></span> | <span data-ttu-id="e6ee7-126">.NET framework 4.5 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="e6ee7-126">.NET Framework 4.5 or later</span></span> | <span data-ttu-id="e6ee7-127">.NET framework 4.6.1 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="e6ee7-127">.NET Framework 4.6.1 or later</span></span><br><span data-ttu-id="e6ee7-128">.NET core 2.1 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="e6ee7-128">.NET Core 2.1 or later</span></span> |

## <a name="feature-differences"></a><span data-ttu-id="e6ee7-129">Özellik farkları</span><span class="sxs-lookup"><span data-stu-id="e6ee7-129">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="e6ee7-130">Otomatik yeniden bağlantılar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-130">Automatic reconnects</span></span>

<span data-ttu-id="e6ee7-131">ASP.NET Core SignalR öğesinde otomatik yeniden bağlantılar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-131">Automatic reconnects aren't supported in ASP.NET Core SignalR.</span></span> <span data-ttu-id="e6ee7-132">İstemci bağlantısı kesilmişse, kullanıcı yeniden bağlamak isterseniz yeni bir bağlantı açıkça başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-132">If the client is disconnected, the user must explicitly start a new connection if they want to reconnect.</span></span> <span data-ttu-id="e6ee7-133">ASP.NET SignalR SignalR bağlantısı kesilirse, sunucuya yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-133">In ASP.NET SignalR, SignalR attempts to reconnect to the server if the connection is dropped.</span></span> 

### <a name="protocol-support"></a><span data-ttu-id="e6ee7-134">Protokol desteği</span><span class="sxs-lookup"><span data-stu-id="e6ee7-134">Protocol support</span></span>

<span data-ttu-id="e6ee7-135">ASP.NET Core Signalr'yi destekleyen dayalı yeni bir ikili Protokolü yanı sıra JSON [MessagePack](xref:signalr/messagepackhubprotocol).</span><span class="sxs-lookup"><span data-stu-id="e6ee7-135">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="e6ee7-136">Ayrıca, özel protokoller oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-136">Additionally, custom protocols can be created.</span></span>

### <a name="transports"></a><span data-ttu-id="e6ee7-137">Taşımalar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-137">Transports</span></span>

<span data-ttu-id="e6ee7-138">ASP.NET Core SignalR öğesinde sonsuza kadar çerçeve taşıma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-138">The Forever Frame transport is not supported in ASP.NET Core SignalR.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="e6ee7-139">Sunucuda farkları</span><span class="sxs-lookup"><span data-stu-id="e6ee7-139">Differences on the server</span></span>

<span data-ttu-id="e6ee7-140">ASP.NET Core SignalR sunucu tarafı kitaplıklar dahil [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) parçası olan paket **ASP.NET Core Web uygulaması** Razor hem MVC şablonu projeleri.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-140">The ASP.NET Core SignalR server-side libraries are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) package that's part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="e6ee7-141">ASP.NET Core SignalR çağırarak yapılandırılmalıdır bir ASP.NET Core ara yazılımını olduğundan [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) içinde `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-141">ASP.NET Core SignalR is an ASP.NET Core middleware, so it must be configured by calling [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR()
```

<span data-ttu-id="e6ee7-142">Yönlendirmeyi yapılandırmak için eşleme rotaları hub içinde [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) yöntem çağrısı `Startup.Configure` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-142">To configure routing, map routes to hubs inside the [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a><span data-ttu-id="e6ee7-143">Yapışkan oturumlar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-143">Sticky sessions</span></span>

<span data-ttu-id="e6ee7-144">ASP.NET SignalR ölçeğini genişletme modeli yeniden ve gruptaki herhangi bir sunucuya ileti gönderme etmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-144">The scaleout model for ASP.NET SignalR allows clients to reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="e6ee7-145">ASP.NET Core SignalR öğesinde, istemci ile aynı sunucuya bağlantı süresi boyunca etkileşim kurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-145">In ASP.NET Core SignalR, the client must interact with the same server for the duration of the connection.</span></span> <span data-ttu-id="e6ee7-146">Redis kullanarak genişletme için Yapışkan oturumlar gerekli olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-146">For scaleout using Redis, that means sticky sessions are required.</span></span> <span data-ttu-id="e6ee7-147">Genişletme kullanma [Azure SignalR hizmeti](/azure/azure-signalr/), Yapışkan oturumlar bulunmamaktır hizmet bağlantıları istemcilere hallettiğinden.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-147">For scaleout using [Azure SignalR Service](/azure/azure-signalr/), sticky sessions are not required because the service handles connections to clients.</span></span> 

### <a name="single-hub-per-connection"></a><span data-ttu-id="e6ee7-148">Bağlantı başına tek bir hub</span><span class="sxs-lookup"><span data-stu-id="e6ee7-148">Single hub per connection</span></span>

<span data-ttu-id="e6ee7-149">ASP.NET Core SignalR öğesinde bağlantı modeli basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-149">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="e6ee7-150">Bağlantıları, doğrudan erişim birden çok hub'a paylaşmak için kullanılan tek bir bağlantı yerine tek bir hub için gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-150">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="e6ee7-151">Akış</span><span class="sxs-lookup"><span data-stu-id="e6ee7-151">Streaming</span></span>

<span data-ttu-id="e6ee7-152">ASP.NET Core SignalR destekler [akış verileri](xref:signalr/streaming) istemciye hub'ından.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-152">ASP.NET Core SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="e6ee7-153">Durum</span><span class="sxs-lookup"><span data-stu-id="e6ee7-153">State</span></span>

<span data-ttu-id="e6ee7-154">İlerleme durumu iletileri için destek yanı sıra hub'ı (HubState olarak da adlandırılır) ve istemciler arasında rastgele bir durum geçirme özelliği kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-154">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="e6ee7-155">Şu anda hiçbir hub proxy karşılığı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-155">There is no counterpart of hub proxies at the moment.</span></span>

### <a name="persistentconnection-removal"></a><span data-ttu-id="e6ee7-156">PersistentConnection kaldırma</span><span class="sxs-lookup"><span data-stu-id="e6ee7-156">PersistentConnection removal</span></span>

<span data-ttu-id="e6ee7-157">ASP.NET Core signalr'da [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118)) sınıfı kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-157">In ASP.NET Core SignalR, the [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118)) class has been removed.</span></span> 

### <a name="globalhost"></a><span data-ttu-id="e6ee7-158">GlobalHost</span><span class="sxs-lookup"><span data-stu-id="e6ee7-158">GlobalHost</span></span>

<span data-ttu-id="e6ee7-159">ASP.NET Core Framework'e yerleşik bağımlılık ekleme (dı) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-159">ASP.NET Core has dependency injection (DI) built into the framework.</span></span> <span data-ttu-id="e6ee7-160">Hizmetleri DI erişmek için kullanabileceğiniz [HubContext](xref:signalr/hubcontext).</span><span class="sxs-lookup"><span data-stu-id="e6ee7-160">Services can use DI to access the [HubContext](xref:signalr/hubcontext).</span></span> <span data-ttu-id="e6ee7-161">`GlobalHost` ASP.NET SignalR öğesinde almak için kullanılan nesne bir `HubContext` ASP.NET Core SignalR öğesinde yok.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-161">The `GlobalHost` object that is used in ASP.NET SignalR to get a `HubContext` doesn't exist in ASP.NET Core SignalR.</span></span>

### <a name="hubpipeline"></a><span data-ttu-id="e6ee7-162">HubPipeline</span><span class="sxs-lookup"><span data-stu-id="e6ee7-162">HubPipeline</span></span>

<span data-ttu-id="e6ee7-163">ASP.NET Core SignalR için destek yok `HubPipeline` modüller.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-163">ASP.NET Core SignalR doesn't have support for `HubPipeline` modules.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="e6ee7-164">İstemci üzerinde farkları</span><span class="sxs-lookup"><span data-stu-id="e6ee7-164">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="e6ee7-165">TypeScript</span><span class="sxs-lookup"><span data-stu-id="e6ee7-165">TypeScript</span></span>

<span data-ttu-id="e6ee7-166">ASP.NET Core SignalR istemci yazıldığı [TypeScript](https://www.typescriptlang.org/).</span><span class="sxs-lookup"><span data-stu-id="e6ee7-166">The ASP.NET Core SignalR client is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="e6ee7-167">JavaScript veya TypeScript kullanırken yazabileceğiniz [JavaScript istemci](xref:signalr/javascript-client).</span><span class="sxs-lookup"><span data-stu-id="e6ee7-167">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="e6ee7-168">JavaScript istemcisi, barındırılan [npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="e6ee7-168">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="e6ee7-169">Önceki sürümlerde, Visual Studio'da bir NuGet paketi aracılığıyla JavaScript istemci alındı.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-169">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="e6ee7-170">Çekirdek sürümleri için [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm paket JavaScript kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-170">For the Core versions, the [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm package contains the JavaScript libraries.</span></span> <span data-ttu-id="e6ee7-171">Bu paket bulunup bulunmadığına **ASP.NET Core Web uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-171">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="e6ee7-172">Elde etmek ve yüklemek için npm kullanın `@aspnet/signalr` npm paketi.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-172">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="e6ee7-173">jQuery</span><span class="sxs-lookup"><span data-stu-id="e6ee7-173">jQuery</span></span>

<span data-ttu-id="e6ee7-174">JQuery bağımlı projeler jQuery kullanmaya devam edebilirsiniz ancak kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-174">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="internet-explorer-support"></a><span data-ttu-id="e6ee7-175">Internet Explorer desteği</span><span class="sxs-lookup"><span data-stu-id="e6ee7-175">Internet Explorer support</span></span>

<span data-ttu-id="e6ee7-176">ASP.NET Core SignalR (ASP.NET SignalR, Microsoft Internet Explorer 8 ve üzeri desteklenir) Microsoft Internet Explorer 11 veya üstü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-176">ASP.NET Core SignalR requires Microsoft Internet Explorer 11 or later (ASP.NET SignalR supported Microsoft Internet Explorer 8 and later).</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="e6ee7-177">JavaScript istemci yöntem sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e6ee7-177">JavaScript client method syntax</span></span>

<span data-ttu-id="e6ee7-178">JavaScript sözdizimi SignalR önceki sürümünden değişmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-178">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="e6ee7-179">Yerine `$connection` nesne, bir bağlantı kullanarak oluşturduğunuz [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-179">Rather than using the `$connection` object, create a connection using the [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="e6ee7-180">Kullanım [üzerinde](/javascript/api/@aspnet/signalr/HubConnection#on) hub çağırabilirsiniz istemci yöntemlerini belirtmek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-180">Use the [on](/javascript/api/@aspnet/signalr/HubConnection#on) method to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="e6ee7-181">İstemci yöntemi oluşturduktan sonra hub Bağlantısı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-181">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="e6ee7-182">Zincir bir [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) oturum veya hataları işlemek için bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-182">Chain a [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="e6ee7-183">Hub proxy</span><span class="sxs-lookup"><span data-stu-id="e6ee7-183">Hub proxies</span></span>

<span data-ttu-id="e6ee7-184">Hub proxy artık otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-184">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="e6ee7-185">Bunun yerine, yöntem adı yöntemlere geçirilen [çağırma](/javascript/api/%40aspnet/signalr/hubconnection#invoke) dize olarak API.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-185">Instead, the method name is passed into the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="e6ee7-186">.NET ve diğer istemciler</span><span class="sxs-lookup"><span data-stu-id="e6ee7-186">.NET and other clients</span></span>

<span data-ttu-id="e6ee7-187">`Microsoft.AspNetCore.SignalR.Client` NuGet paketi, ASP.NET Core SignalR için .NET istemci kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-187">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="e6ee7-188">Kullanım [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) ve hub'ına bağlantı örneğini oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-188">Use the [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a><span data-ttu-id="e6ee7-189">Genişletme farkları</span><span class="sxs-lookup"><span data-stu-id="e6ee7-189">Scaleout differences</span></span>

<span data-ttu-id="e6ee7-190">ASP.NET SignalR, SQL Server ve Redis destekler.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-190">ASP.NET SignalR supports SQL Server and Redis.</span></span> <span data-ttu-id="e6ee7-191">Azure SignalR hizmeti ve Redis ASP.NET Core SignalR destekler.</span><span class="sxs-lookup"><span data-stu-id="e6ee7-191">ASP.NET Core SignalR supports Azure SignalR Service and Redis.</span></span>

### <a name="aspnet"></a><span data-ttu-id="e6ee7-192">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e6ee7-192">ASP.NET</span></span>

* [<span data-ttu-id="e6ee7-193">Azure Service Bus ile SignalR ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="e6ee7-193">SignalR scaleout with Azure Service Bus</span></span>](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [<span data-ttu-id="e6ee7-194">Redis ile SignalR ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="e6ee7-194">SignalR scaleout with Redis</span></span>](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [<span data-ttu-id="e6ee7-195">SQL Server ile SignalR ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="e6ee7-195">SignalR scaleout with SQL Server</span></span>](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a><span data-ttu-id="e6ee7-196">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e6ee7-196">ASP.NET Core</span></span>

* [<span data-ttu-id="e6ee7-197">Azure SignalR Hizmeti</span><span class="sxs-lookup"><span data-stu-id="e6ee7-197">Azure SignalR Service</span></span>](/azure/azure-signalr/)

## <a name="additional-resources"></a><span data-ttu-id="e6ee7-198">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-198">Additional resources</span></span>

* [<span data-ttu-id="e6ee7-199">Merkezler</span><span class="sxs-lookup"><span data-stu-id="e6ee7-199">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="e6ee7-200">JavaScript istemcisi</span><span class="sxs-lookup"><span data-stu-id="e6ee7-200">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="e6ee7-201">.NET istemcisi</span><span class="sxs-lookup"><span data-stu-id="e6ee7-201">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="e6ee7-202">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="e6ee7-202">Supported platforms</span></span>](xref:signalr/supported-platforms)
