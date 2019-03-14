---
title: ASP.NET Core SignalR Java istemci
author: mikaelm12
description: ASP.NET Core SignalR Java istemcisi kullanmayı öğrenin.
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 11/07/2018
uid: signalr/java-client
ms.openlocfilehash: d0eff38c1f622b896ed1dc3002238aec7b6bfd38
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067635"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="b4b76-103">ASP.NET Core SignalR Java istemci</span><span class="sxs-lookup"><span data-stu-id="b4b76-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="b4b76-104">Tarafından [Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="b4b76-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="b4b76-105">Android uygulamaları dahil olmak üzere Java koddan bir ASP.NET Core SignalR sunucusuna bağlanan Java istemci sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4b76-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="b4b76-106">Gibi [JavaScript istemci](xref:signalr/javascript-client) ve [.NET istemci](xref:signalr/dotnet-client), almak ve gerçek zamanlı bir hub'ına ileti göndermek Java istemcisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4b76-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="b4b76-107">Java istemci, ASP.NET Core 2.2 bulunan ve üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b4b76-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="b4b76-108">Bu makalede bahsedilen örnek Java konsol uygulaması SignalR Java istemcisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4b76-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="b4b76-109">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b4b76-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="b4b76-110">SignalR Java istemci paketini yükle</span><span class="sxs-lookup"><span data-stu-id="b4b76-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="b4b76-111">*Signalr 1.0.0* JAR dosyasını istemcilerin SignalR hub'ları bağlanmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="b4b76-111">The *signalr-1.0.0* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="b4b76-112">JAR dosyası en son sürüm numarasını bulmak için bkz: [Maven arama sonuçları](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span><span class="sxs-lookup"><span data-stu-id="b4b76-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="b4b76-113">Gradle kullanıyorsanız, aşağıdaki satırı ekleyin `dependencies` bölümünü, *build.gradle* dosyası:</span><span class="sxs-lookup"><span data-stu-id="b4b76-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0'
```

<span data-ttu-id="b4b76-114">Maven kullanarak eklerseniz içinde aşağıdaki satırları `<dependencies>` öğesinin, *pom.xml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="b4b76-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="b4b76-115">Bir hub'ına bağlama</span><span class="sxs-lookup"><span data-stu-id="b4b76-115">Connect to a hub</span></span>

<span data-ttu-id="b4b76-116">Kurmak için bir `HubConnection`, `HubConnectionBuilder` kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b4b76-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="b4b76-117">Hub'ı URL'si ve günlük düzeyinde bir bağlantı oluşturulurken yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4b76-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="b4b76-118">Gerekli tüm seçenekler herhangi birini çağırarak yapılandırma `HubConnectionBuilder` yöntemleri önce `build`.</span><span class="sxs-lookup"><span data-stu-id="b4b76-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="b4b76-119">Bağlantıyı başlatmak `start`.</span><span class="sxs-lookup"><span data-stu-id="b4b76-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="b4b76-120">İstemciden hub yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="b4b76-120">Call hub methods from client</span></span>

<span data-ttu-id="b4b76-121">Bir çağrı `send` bir hub yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b4b76-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="b4b76-122">Hub yönteminin adını ve hub yöntemi için tanımlanan herhangi bir bağımsız değişken geçirme `send`.</span><span class="sxs-lookup"><span data-stu-id="b4b76-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="b4b76-123">İstemci hub'ından yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="b4b76-123">Call client methods from hub</span></span>

<span data-ttu-id="b4b76-124">Kullanım `hubConnection.on` hub çağıran istemciye yöntemleri tanımlamak için.</span><span class="sxs-lookup"><span data-stu-id="b4b76-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="b4b76-125">Yapı sonra ancak bağlantı başlatmadan önce yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b4b76-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="b4b76-126">Günlük kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="b4b76-126">Add logging</span></span>

<span data-ttu-id="b4b76-127">SignalR Java istemcinin kullandığı [SLF4J](https://www.slf4j.org/) günlüğe kaydetme için kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="b4b76-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="b4b76-128">Seçtiğiniz kendi özel günlük uygulama özel günlük bağımlılık olarak getirerek kullanıcıların Kitaplığı'nın izin veren bir üst düzey günlüğe kaydetme API'si var.</span><span class="sxs-lookup"><span data-stu-id="b4b76-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="b4b76-129">Aşağıdaki kod parçacığını nasıl kullanılacağını gösterir `java.util.logging` SignalR Java istemcisi ile.</span><span class="sxs-lookup"><span data-stu-id="b4b76-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="b4b76-130">Bağımlılıklarınızı içinde günlüğü yapılandırmazsanız, aşağıdaki uyarı iletisi ile bir varsayılan yok-işlem günlükçü SLF4J yükler:</span><span class="sxs-lookup"><span data-stu-id="b4b76-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="b4b76-131">Bu güvenle yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4b76-131">This can safely be ignored.</span></span>

## <a name="android-development-notes"></a><span data-ttu-id="b4b76-132">Android geliştirme notları</span><span class="sxs-lookup"><span data-stu-id="b4b76-132">Android development notes</span></span>

<span data-ttu-id="b4b76-133">SignalR istemcisi özellikleri için Android SDK'sı uyumluluk bakımından, hedef Android SDK sürümünü belirtmek için aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="b4b76-133">With regards to Android SDK compatibility for the SignalR client features, consider the following items when specifying your target Android SDK version:</span></span>

* <span data-ttu-id="b4b76-134">SignalR Java istemci Android API düzeyi 16 ve daha sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="b4b76-134">The SignalR Java Client will run on Android API Level 16 and later.</span></span>
* <span data-ttu-id="b4b76-135">Azure SignalR hizmeti aracılığıyla bağlanma Android API düzeyi 20 ve sonraki sürümleri gerektirir çünkü [Azure SignalR hizmeti](/azure/azure-signalr/signalr-overview) TLS 1.2 gerektirir ve SHA-1 tabanlı şifre paketleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b4b76-135">Connecting through the Azure SignalR Service will require Android API Level 20 and later because the [Azure SignalR Service](/azure/azure-signalr/signalr-overview) requires TLS 1.2 and doesn't support SHA-1-based cipher suites.</span></span> <span data-ttu-id="b4b76-136">Android [destek SHA-256 (ve üstü) şifre paketleri eklenen](https://developer.android.com/reference/javax/net/ssl/SSLSocket) API düzeyi 20 içinde.</span><span class="sxs-lookup"><span data-stu-id="b4b76-136">Android [added support for SHA-256 (and above) cipher suites](https://developer.android.com/reference/javax/net/ssl/SSLSocket) in API Level 20.</span></span>

## <a name="configure-bearer-token-authentication"></a><span data-ttu-id="b4b76-137">Taşıyıcı belirteci kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4b76-137">Configure bearer token authentication</span></span>

<span data-ttu-id="b4b76-138">SignalR Java istemci, bir "erişim belirteci fabrikası" sağlayarak kimlik doğrulaması için kullanılacak bir taşıyıcı belirteç için yapılandırabilirsiniz [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span><span class="sxs-lookup"><span data-stu-id="b4b76-138">In the SignalR Java client, you can configure a bearer token to use for authentication by providing an "access token factory" to the [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span></span> <span data-ttu-id="b4b76-139">Kullanım [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) sağlamak için bir [RxJava](https://github.com/ReactiveX/RxJava) [tek<String>](http://reactivex.io/documentation/single.html).</span><span class="sxs-lookup"><span data-stu-id="b4b76-139">Use [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) to provide an [RxJava](https://github.com/ReactiveX/RxJava) [Single<String>](http://reactivex.io/documentation/single.html).</span></span> <span data-ttu-id="b4b76-140">Çağrısıyla [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), istemciniz için erişim belirteci üretmek için mantığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4b76-140">With a call to [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), you can write logic to produce access tokens for your client.</span></span>

```java
HubConnection hubConnection = HubConnectionBuilder.create("YOUR HUB URL HERE")
    .withAccessTokenProvider(Single.defer(() -> {
        // Your logic here.
        return Single.just("An Access Token");
    })).build();
```

## <a name="known-limitations"></a><span data-ttu-id="b4b76-141">Bilinen sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b4b76-141">Known limitations</span></span>

* <span data-ttu-id="b4b76-142">Yalnızca JSON Protokolü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b4b76-142">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="b4b76-143">WebSockets taşıma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b4b76-143">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="b4b76-144">Akış henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b4b76-144">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4b76-145">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b4b76-145">Additional resources</span></span>

* [<span data-ttu-id="b4b76-146">Java API'si başvurusu</span><span class="sxs-lookup"><span data-stu-id="b4b76-146">Java API reference</span></span>](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
