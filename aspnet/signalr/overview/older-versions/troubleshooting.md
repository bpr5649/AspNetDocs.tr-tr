---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR sorunlarını giderme (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirme ile yaygın sorunları açıklar.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65116015"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="c7548-103">SignalR Sorunlarını Giderme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="c7548-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="c7548-104">tarafından [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="c7548-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c7548-105">Bu belge, SignalR ile ortak sorun giderme konularını açıklar.</span><span class="sxs-lookup"><span data-stu-id="c7548-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="c7548-106">Bu belge aşağıdaki bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c7548-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="c7548-107">Yöntemleri istemci ve sunucu arasındaki sessizce başarısız çağırma</span><span class="sxs-lookup"><span data-stu-id="c7548-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="c7548-108">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="c7548-109">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="c7548-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="c7548-110">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="c7548-111">Internet Information Services sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="c7548-112">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="c7548-113">Yöntemleri istemci ve sunucu arasındaki sessizce başarısız çağırma</span><span class="sxs-lookup"><span data-stu-id="c7548-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="c7548-114">Bu bölümde, bir yöntem çağrısının başarısız anlamlı bir hata iletisi, istemci ve sunucu arasındaki olası nedenleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c7548-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="c7548-115">Bir SignalR uygulamasında, sunucunun istemci uygulayan yöntemler hakkında bir bilgi bulunmaz; Sunucunun istemci yöntemini çağırdığında, istemciye gönderilen yöntemi adı ve parametre veri ve yalnızca sunucu belirtilen biçimde varsa yöntemi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="c7548-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="c7548-116">Varsa eşleşen hiçbir yöntemi hiçbir şey olmaz, istemcide bulunan ve hiçbir hata iletisi, sunucu üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7548-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="c7548-117">İstemci yöntemleri çağrılmazsa daha fazla araştırmak için başlangıç yöntemin hangi çağrıları görmek için hub'ında, sunucudan geliyor çağırmadan önce günlüğü etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7548-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="c7548-118">Bir JavaScript uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz: [istemci tarafı günlüğe kaydetme (JavaScript istemci sürümü) etkinleştirme](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="c7548-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="c7548-119">Bir .NET istemci uygulamasında günlüğe kaydetmeyi etkinleştirmek için bkz: [istemci tarafı günlüğe kaydetme (.NET istemci sürümü) etkinleştirme](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="c7548-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="c7548-120">Yanlış yazılmış yöntemi, hatalı yöntem imzası veya yanlış hub'ı adı</span><span class="sxs-lookup"><span data-stu-id="c7548-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="c7548-121">İstemci üzerinde uygun bir yöntem adı ya da çağrılan yöntemin imzası tam olarak eşleşmiyor, çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c7548-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="c7548-122">Sunucu tarafından adlandırılan yöntem adını istemcideki yöntemin adı eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="c7548-123">Ayrıca, SignalR hub proxy başlamalıdır yöntemlerle oluşturur JavaScript'te uygun olduğundan, bu nedenle bir yöntem adlı `SendMessage` sunucu üzerinde çağrılır `sendMessage` istemci proxy'de.</span><span class="sxs-lookup"><span data-stu-id="c7548-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="c7548-124">Kullanırsanız `HubName` özniteliği sunucu tarafı kodunuzda, kullanılan adını istemcide hub'ı oluşturmak için kullanılan adı ile eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="c7548-125">Kullanmıyorsanız, `HubName` öznitelik, bir JavaScript istemci hub'ı adını başlamalıdır, chatHub ChatHub yerine gibi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="c7548-126">İstemci üzerinde yinelenen yöntem adı</span><span class="sxs-lookup"><span data-stu-id="c7548-126">Duplicate method name on client</span></span>

<span data-ttu-id="c7548-127">Yinelenen bir yöntem yalnızca büyük küçük harfle farklı istemci üzerinde olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="c7548-128">İstemci uygulamanızın adlı yöntemi varsa `sendMessage`, adında bir yöntem de, hiç doğrulayın `SendMessage` de.</span><span class="sxs-lookup"><span data-stu-id="c7548-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="c7548-129">İstemci üzerinde eksik JSON ayrıştırıcı</span><span class="sxs-lookup"><span data-stu-id="c7548-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="c7548-130">SignalR, bir JSON ayrıştırıcı, sunucu ve istemci arasındaki çağrıların seri hale getirmek için mevcut olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c7548-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="c7548-131">İstemci (örneğin, Internet Explorer 7) yerleşik bir JSON Ayrıştırıcı yoksa, bir uygulama eklemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7548-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="c7548-132">JSON ayrıştırıcının indirebileceğiniz [burada](http://nuget.org/packages/json2).</span><span class="sxs-lookup"><span data-stu-id="c7548-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="c7548-133">Hub ve PersistentConnection sözdiziminin karışık kullanımına</span><span class="sxs-lookup"><span data-stu-id="c7548-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="c7548-134">SignalR iki iletişim modeli kullanır: Hub'ları ve PersistentConnections.</span><span class="sxs-lookup"><span data-stu-id="c7548-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="c7548-135">Bu iki iletişim modeller çağırma söz dizimi, istemci kodu farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c7548-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="c7548-136">Sunucu kodunuzdaki bir hub eklediyseniz, istemci kodunuzun tamamını kullandığını hub'ı uygun söz dizimini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="c7548-137">**JavaScript istemci olarak bir PersistentConnection oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="c7548-138">**Bir Javascript istemci bir Hub Proxy oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="c7548-139">**Bir rota eşleyen bir PersistentConnection için C# sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="c7548-140">**C#birden çok uygulamalarınız varsa, Hub'ına veya birden çok hub'a bir rotayı eşler sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="c7548-141">Abonelikleri eklemeden önce başlatılan bağlantı</span><span class="sxs-lookup"><span data-stu-id="c7548-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="c7548-142">Hub'ın bağlantı için proxy sunucudan çağrılabilir yöntemleri eklenmeden önce başlatılırsa, iletileri alınmaz.</span><span class="sxs-lookup"><span data-stu-id="c7548-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="c7548-143">Aşağıdaki JavaScript kodunu hub düzgün bir şekilde başlar:</span><span class="sxs-lookup"><span data-stu-id="c7548-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="c7548-144">**Alınacak hub'ları iletileri izin vermez yanlış JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="c7548-145">Bunun yerine, başlangıç çağırmadan önce yöntemi abonelik ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c7548-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="c7548-146">**Doğru bir şekilde bir hub'ına abonelikleri ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="c7548-147">Hub proxy yöntemi adı eksik</span><span class="sxs-lookup"><span data-stu-id="c7548-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="c7548-148">Sunucuda tanımlanmış yöntemi istemcide abone olduğu olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="c7548-149">Sunucu yöntemi tanımlar olsa bile, yine de için istemci proxy eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="c7548-150">Yöntemleri eklenebilir istemci Ara sunucuya aşağıdaki yollarla (yöntemi eklenen Not `client` hub'ı değil hub doğrudan üyesi):</span><span class="sxs-lookup"><span data-stu-id="c7548-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="c7548-151">**Hub proxy için yöntemler ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="c7548-152">Hub veya hub yöntemlerine genel olarak bildirilmedi</span><span class="sxs-lookup"><span data-stu-id="c7548-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="c7548-153">İstemcide görünür olması için hub uygulama ve yöntemler olarak bildirilmelidir `public`.</span><span class="sxs-lookup"><span data-stu-id="c7548-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="c7548-154">Hub'ı farklı bir uygulamadan erişme</span><span class="sxs-lookup"><span data-stu-id="c7548-154">Accessing hub from a different application</span></span>

<span data-ttu-id="c7548-155">SignalR hub'ları yalnızca SignalR istemciler kullanan uygulamalar erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="c7548-156">Diğer iletişim kitaplıklarını (örneğin, SOAP ve WCF web hizmetlerini.) ile SignalR işleyemez Hedef platform için kullanılabilir hiçbir SignalR istemcisi varsa, sunucu uç noktası doğrudan erişemez.</span><span class="sxs-lookup"><span data-stu-id="c7548-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="c7548-157">El ile verileri seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="c7548-157">Manually serializing data</span></span>

<span data-ttu-id="c7548-158">SignalR otomatik olarak JSON yönteminizi seri hale getirmek için kendi başınıza parametreleri-burada ait gerek kullanır.</span><span class="sxs-lookup"><span data-stu-id="c7548-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="c7548-159">İstemci OnDisconnected işlevindeki yürütülmedi uzak Hub yöntemi</span><span class="sxs-lookup"><span data-stu-id="c7548-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="c7548-160">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-160">This behavior is by design.</span></span> <span data-ttu-id="c7548-161">Zaman `OnDisconnected` olan çağrılır, hub'ı zaten geçtiğini `Disconnected` hub yöntemlerine yönelik daha fazla izin vermeyen durumu.</span><span class="sxs-lookup"><span data-stu-id="c7548-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="c7548-162">**Doğru OnDisconnected olayda kodu yürüten C# sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="c7548-163">Bağlantı sınırına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="c7548-163">Connection limit reached</span></span>

<span data-ttu-id="c7548-164">Windows 7 gibi bir istemci işletim sisteminde IIS tam sürümünü kullanırken, 10 bağlantı sınırı uygulanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c7548-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="c7548-165">Bir istemci işletim sistemi kullanırken, IIS Express yerine bu sınırı önlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7548-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="c7548-166">Etki alanları arası bağlantı düzgün şekilde ayarlanmamış</span><span class="sxs-lookup"><span data-stu-id="c7548-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="c7548-167">Etki alanları arası bağlantı varsa (bir ağ bağlantısı için SignalR URL değil barındırma sayfası aynı etki alanında) doğru şekilde ayarlanmamışsa, bir hata iletisi bağlantı başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="c7548-168">Etki alanları arası iletişimi etkinleştirme hakkında daha fazla bilgi için bkz: [etki alanları arası bağlantı kurmak nasıl](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="c7548-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="c7548-169">.NET istemci çalışmıyor NTLM (Active Directory) kullanarak sanal ağa bağlantı</span><span class="sxs-lookup"><span data-stu-id="c7548-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="c7548-170">Bağlantının düzgün şekilde yapılandırılmadıysa, etki alanı güvenlik kullanan bir .NET istemci uygulamasındaki bir bağlantı başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="c7548-171">SignalR, bir etki alanı ortamında kullanmak için gerekli bağlantı özelliği şu şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c7548-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="c7548-172">**Bağlantı kimlik bilgilerini uygulayan C# istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="c7548-173">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-173">Other connection issues</span></span>

<span data-ttu-id="c7548-174">Bu bölümde, nedenleri ve çözümleri belirli belirtileri veya bağlantı sırasında oluşan hata iletileri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c7548-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="c7548-175">"Veri gönderilmeden önce başlangıç çağrılmalıdır" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="c7548-176">Kod SignalR nesneleri başvuruyorsa bağlantı başlatılmadan önce bu hatanın yaygın olarak görülür.</span><span class="sxs-lookup"><span data-stu-id="c7548-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="c7548-177">İşleyicileri ve benzeri için iliştirdiği bağlantı tamamlandıktan sonra sunucuda tanımlı yöntemlerini eklenecek gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7548-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="c7548-178">Unutmayın çağrısı `Start` tamamlandıktan sonra önce çağrı çalıştırılabilir kod şekilde uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="c7548-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="c7548-179">Bir bağlantı tamamen başlatıldıktan sonra işleyicileri eklemek için en iyi başlangıç yöntemine bir parametre olarak geçirilen bir geri çağırma işlevini yerleştirmenin yoludur:</span><span class="sxs-lookup"><span data-stu-id="c7548-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="c7548-180">**SignalR nesnelerine başvuru olay işleyicileri doğru ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="c7548-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="c7548-181">Bu hata ayrıca SignalR nesneler hala başvurulmayan ederken bir bağlantı durduğunda görülür.</span><span class="sxs-lookup"><span data-stu-id="c7548-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="c7548-182">"301 kalıcı olarak taşındı" veya "302 geçici olarak taşındı" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="c7548-183">Bu hata, proje ile otomatik olarak oluşturulan proxy müdahale SignalR, adlı bir klasör içeriyorsa görülebilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="c7548-184">Bu hatayı önlemek için adlı bir klasör kullanmayın `SignalR` , uygulama ya da devre dışı bırakma otomatik proxy oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c7548-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="c7548-185">Bkz: [oluşturulan Proxy ve sizin için yaptığı](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="c7548-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="c7548-186">.NET veya Silverlight İstemcisi'nde "403 Yasak" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="c7548-187">Burada etki alanları arası iletişimin düzgün şekilde etkinleştirilmedi etki alanları arası ortamlarda bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="c7548-188">Etki alanları arası iletişimi etkinleştirme hakkında daha fazla bilgi için bkz: [etki alanları arası bağlantı kurmak nasıl](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="c7548-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="c7548-189">Bir Silverlight İstemcisi'nde etki alanları arası bağlantı kurmak için bkz: [Silverlight istemcileri etki alanları arası bağlantılara](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span><span class="sxs-lookup"><span data-stu-id="c7548-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="c7548-190">"404 bulunamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-190">"404 Not Found" error</span></span>

<span data-ttu-id="c7548-191">Bu sorunun çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c7548-191">There are several causes for this issue.</span></span> <span data-ttu-id="c7548-192">Aşağıdakilerin tümü doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="c7548-192">Verify all of the following:</span></span>

- <span data-ttu-id="c7548-193">**Hub proxy adresi başvurusu düzgün biçimlendirilmemiş:** Bu hata, oluşturulan hub proxy adresi başvurusu doğru şekilde biçimlendirilmemiş, yaygın olarak görülür.</span><span class="sxs-lookup"><span data-stu-id="c7548-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="c7548-194">Hub adresine başvuru düzgün yapıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="c7548-195">Bkz: [nasıl dinamik olarak oluşturulan proxy başvuru](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="c7548-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="c7548-196">**Hub rotasını eklemeden önce uygulama için yollar ekleme:** Uygulamanız diğer yollar kullanıyorsa, eklenen ilk rota çağrısı olduğunu doğrulayın `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="c7548-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="c7548-197">"500 İç sunucu hatası"</span><span class="sxs-lookup"><span data-stu-id="c7548-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="c7548-198">Çok çeşitli nedenleri olabilir çok genel bir hatadır.</span><span class="sxs-lookup"><span data-stu-id="c7548-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="c7548-199">Hatanın ayrıntıları sunucunun olay günlüğüne görünmelidir veya sunucunun hata ayıklama aracılığıyla bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="c7548-200">Daha ayrıntılı hata bilgileri, sunucu üzerindeki ayrıntılı hatalar açarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="c7548-201">Daha fazla bilgi için [Hub sınıfına hataları işlemek nasıl](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span><span class="sxs-lookup"><span data-stu-id="c7548-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="c7548-202">"TypeError: &lt;hubType&gt; tanımlanmamış" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="c7548-203">Bu hataya neden olur çağrısı `MapHubs` düzgün yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="c7548-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="c7548-204">Bkz: [SignalR yol kaydetmek ve SignalR seçeneklerini yapılandırmak nasıl](../guide-to-the-api/hubs-api-guide-server.md#route) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c7548-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="c7548-205">JsonSerializationException kullanıcı kodu ile işlenmedi</span><span class="sxs-lookup"><span data-stu-id="c7548-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="c7548-206">Doğrulamak için yöntemlerinizi gönderdiğiniz parametreleri seri hale getirilemeyen türleri (örneğin, dosya tanıtıcıları veya veritabanı bağlantıları) içermez.</span><span class="sxs-lookup"><span data-stu-id="c7548-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="c7548-207">İstemci (veya güvenlik için serileştirme nedeniyle), kullanım gönderilmesini istemiyorsanız bir sunucu tarafı nesne üyeleri kullanmanız gerekiyorsa `JSONIgnore` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c7548-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="c7548-208">"Protokol hatası: Bilinmeyen aktarım"hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="c7548-209">İstemci SignalR kullanan taşımalar desteklemiyorsa bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="c7548-210">Bkz: [aktarım ve geri dönüşler](../getting-started/introduction-to-signalr.md#transports) hangi tarayıcılar kullanılabilir SignalR ile bilgi.</span><span class="sxs-lookup"><span data-stu-id="c7548-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="c7548-211">"JavaScript Hub proxy oluşturma devre dışı bırakıldı."</span><span class="sxs-lookup"><span data-stu-id="c7548-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="c7548-212">Bu hata oluşacaktır `DisableJavaScriptProxies` dinamik olarak oluşturulan proxy için bir başvuru da dahil olmak üzere sırasında ayarlanır `signalr/hubs`.</span><span class="sxs-lookup"><span data-stu-id="c7548-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="c7548-213">Proxy el ile oluşturma hakkında daha fazla bilgi için bkz. [oluşturulan proxy ve sizin için yaptığı](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="c7548-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="c7548-214">"Bağlantı kimliği yanlış biçimde" veya "kullanıcı kimliği etkin bir SignalR bağlantısı sırasında değiştiremezsiniz" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="c7548-215">Bu hata, kimlik doğrulaması kullanılır ve istemci bağlantı durdurulmadan önce kaydedilir görülebilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="c7548-216">İstemci oturumu kapatmak önce SignalR bağlantı durdurma çözümdür.</span><span class="sxs-lookup"><span data-stu-id="c7548-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="c7548-217">"Yakalanmayan hata: SignalR: jQuery nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="c7548-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="c7548-218">JQuery önce SignalR.js dosyasını başvurulduğundan emin olun"hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="c7548-219">SignalR JavaScript istemci çalıştırmak için jQuery gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c7548-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="c7548-220">JQuery yönelik başvurunuz kullanılan yolun geçerli olduğunu ve jQuery başvuru SignalR başvurusu önce olduğunu doğru olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7548-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="c7548-221">"Yakalanmamış TypeError: Özelliği okunamıyor '&lt;özelliği&gt;' undefined'ın "hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="c7548-222">JQuery veya düzgün başvurulan hub proxy kalmamasını değil Bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="c7548-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="c7548-223">Başvurunuz jQuery ve hub proxy için kullanılan yolun geçerli olduğunu ve jQuery başvurusunu başvuru hub proxy için önce olduğunu doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c7548-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="c7548-224">Hub proxy için varsayılan başvuru aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c7548-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="c7548-225">**HTML istemci tarafı hub proxy doğru başvuran bir kod**</span><span class="sxs-lookup"><span data-stu-id="c7548-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="c7548-226">"RuntimeBinderException kullanıcı kodu ile işlenmedi" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="c7548-227">Bu hata oluşabilir, yanlış aşırı yüklemesini `Hub.On` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7548-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="c7548-228">Yöntemin dönüş değeri varsa, dönüş türü bir genel tür parametresi belirtilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c7548-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="c7548-229">**İstemci (olmadan oluşturulan proxy) üzerinde tanımlanan yöntemi**</span><span class="sxs-lookup"><span data-stu-id="c7548-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="c7548-230">Bağlantı kimliği tutarsız veya sayfa yüklemelerinin bağlantıyı keser</span><span class="sxs-lookup"><span data-stu-id="c7548-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="c7548-231">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-231">This behavior is by design.</span></span> <span data-ttu-id="c7548-232">Hub nesnesi sayfa nesnesinde barındırıldığından, Sayfa yenilendiğinde hub yok edilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="c7548-233">Bunlar sayfa yüklemelerinin arasında tutarlı olması kullanıcıların bağlantı kimlikleri arasındaki ilişkiyi korumak çok sayfalı bir uygulamada gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7548-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="c7548-234">Bağlantı kimlikleri ya da sunucuda depolanan bir `ConcurrentDictionary` nesnesi veya bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c7548-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="c7548-235">Hata "Değer null olamaz"</span><span class="sxs-lookup"><span data-stu-id="c7548-235">"Value cannot be null" error</span></span>

<span data-ttu-id="c7548-236">İsteğe bağlı parametreler içeren sunucu tarafı yöntemlerinin şu anda desteklenmiyor; İsteğe bağlı parametresi atlanırsa, yöntem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c7548-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="c7548-237">Daha fazla bilgi için [isteğe bağlı parametreler](https://github.com/SignalR/SignalR/issues/324).</span><span class="sxs-lookup"><span data-stu-id="c7548-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="c7548-238">"Firefox sunucusuna bir bağlantı kuramıyor &lt;adresi&gt;" Firebug hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="c7548-239">Anlaşma WebSocket taşıma başarısız olur ve bunun yerine başka bir aktarım kullanılıyorsa bu hata iletisini Firebug içinde görülebilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="c7548-240">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="c7548-241">.NET istemci uygulamasındaki "doğrulama yordamına göre uzak sertifika geçersiz" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="c7548-242">Sunucunuz, özel bir istemci sertifikası gerektiriyorsa, isteği yapılmadan önce sonra bir x509certificate bağlantı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7548-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="c7548-243">Sertifikayı kullanarak bağlantı eklemek `Connection.AddClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="c7548-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="c7548-244">Bağlantı kimlik doğrulaması zaman aşımına sonra bırakır</span><span class="sxs-lookup"><span data-stu-id="c7548-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="c7548-245">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-245">This behavior is by design.</span></span> <span data-ttu-id="c7548-246">Kimlik doğrulama kimlik bilgileri, bir bağlantı etkin durumdayken değiştirilemez; kimlik bilgilerini yenilemek için bağlantı durdurulup yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7548-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="c7548-247">OnConnected iki kez jQuery Mobile'ı kullanırken uğradığında çağrılır</span><span class="sxs-lookup"><span data-stu-id="c7548-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="c7548-248">jQuery Mobile's `initializePage` işlevi, böylece ikinci bir bağlantı oluşturma betikleri yeniden yürütülmesi için her bir sayfasında zorlar.</span><span class="sxs-lookup"><span data-stu-id="c7548-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="c7548-249">Bu soruna yönelik çözümler içerir:</span><span class="sxs-lookup"><span data-stu-id="c7548-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="c7548-250">JQuery Mobile JavaScript dosyanıza önce başvurusunu içerir.</span><span class="sxs-lookup"><span data-stu-id="c7548-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="c7548-251">Devre dışı `initializePage` ayarlayarak işlevi `$.mobile.autoInitializePage = false`.</span><span class="sxs-lookup"><span data-stu-id="c7548-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="c7548-252">Sayfa başlatma bağlantı başlatmadan önce tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="c7548-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="c7548-253">İletileri sunucu gönderilen olayları kullanarak Silverlight uygulamalarında gecikiyor</span><span class="sxs-lookup"><span data-stu-id="c7548-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="c7548-254">Sunucu kullanarak olayları Silverlight'ın gönderilen iletileri gecikir.</span><span class="sxs-lookup"><span data-stu-id="c7548-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="c7548-255">Uzun yoklama yerine kullanılacak zorlamak için aşağıdaki bağlantı başlatırken kullanın:</span><span class="sxs-lookup"><span data-stu-id="c7548-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="c7548-256">"İzin reddedildi" kullanarak sürekli çerçeve Protokolü</span><span class="sxs-lookup"><span data-stu-id="c7548-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="c7548-257">Açıklanan bilinen bir sorun budur [burada](https://github.com/SignalR/SignalR/issues/1963).</span><span class="sxs-lookup"><span data-stu-id="c7548-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="c7548-258">En son JQuery kitaplığını kullanarak bu belirti görülebilir; JQuery 1.8.2 uygulamanıza düşürmek çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7548-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="c7548-259">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="c7548-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="c7548-260">Aşağıdaki bölümde, derleyici ve sunucu tarafı çalışma zamanı hataları için olası çözümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c7548-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="c7548-261">Hub örneği null başvurudur</span><span class="sxs-lookup"><span data-stu-id="c7548-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="c7548-262">Her bağlantı için hub örneği oluşturulduğundan, hub örneği, kodunuzda oluşturma olamaz.</span><span class="sxs-lookup"><span data-stu-id="c7548-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="c7548-263">Hub dışında aynı hub'da yöntemleri çağırmak için bkz: [istemci yöntemleri çağırmak ve Hub sınıfına dışındaki grupları yönetmek nasıl](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) için hub bağlamını başvuru elde etme.</span><span class="sxs-lookup"><span data-stu-id="c7548-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="c7548-264">HTTPContext.Current.Session null</span><span class="sxs-lookup"><span data-stu-id="c7548-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="c7548-265">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-265">This behavior is by design.</span></span> <span data-ttu-id="c7548-266">Oturum durumunu etkinleştirme çift yönlü Mesajlaşma kesmek beri SignalR ASP.NET oturum durumu desteklemez.</span><span class="sxs-lookup"><span data-stu-id="c7548-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="c7548-267">Geçersiz kılmak için uygun yöntem</span><span class="sxs-lookup"><span data-stu-id="c7548-267">No suitable method to override</span></span>

<span data-ttu-id="c7548-268">Eski belgelere veya blog koddan kullanıyorsanız bu hatayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7548-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="c7548-269">Adları değiştirildi veya kullanım dışı yöntemler başvuran değil doğrulayın (gibi `OnConnectedAsync`).</span><span class="sxs-lookup"><span data-stu-id="c7548-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="c7548-270">HostContextExtensions.WebSocketServerUrl null</span><span class="sxs-lookup"><span data-stu-id="c7548-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="c7548-271">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-271">This behavior is by design.</span></span> <span data-ttu-id="c7548-272">Bu üye, kullanım dışıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c7548-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="c7548-273">"'Signalr.hubs' adlı bir rota rota koleksiyonu içinde zaten" hatası</span><span class="sxs-lookup"><span data-stu-id="c7548-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="c7548-274">Bu hata görülen `MapHubs` iki kez uygulamanız tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c7548-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="c7548-275">Bazı örnek uygulamalar arama `MapHubs` doğrudan genel uygulama dosyasında; başkalarının yaptığı çağrısında bir sarmalayıcı sınıftır.</span><span class="sxs-lookup"><span data-stu-id="c7548-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="c7548-276">Uygulamanızı hem yapmaz emin olun.</span><span class="sxs-lookup"><span data-stu-id="c7548-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="c7548-277">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-277">Visual Studio issues</span></span>

<span data-ttu-id="c7548-278">Bu bölümde, Visual Studio'da karşılaşılan sorunları açıklar.</span><span class="sxs-lookup"><span data-stu-id="c7548-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="c7548-279">Betik Belgeler düğümü, Çözüm Gezgini'nde görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="c7548-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="c7548-280">Öğreticilerimizden bazıları, Çözüm Gezgininde "Betik belgelerini" hata ayıklama sırasında yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="c7548-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="c7548-281">Bu düğüm, JavaScript hata ayıklayıcı tarafından üretilen ve yalnızca tarayıcı istemcilerinin Internet Explorer'da hata ayıklama sırasında görünür; Chrome ya da Firefox kullandıysanız düğümünde görünmez.</span><span class="sxs-lookup"><span data-stu-id="c7548-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="c7548-282">Başka bir istemci hata ayıklayıcı çalışıyorsa, Silverlight hata ayıklayıcı gibi JavaScript hata ayıklayıcı ayrıca çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="c7548-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="c7548-283">Visual Studio 2008 veya daha eski SignalR çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="c7548-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="c7548-284">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c7548-284">This behavior is by design.</span></span> <span data-ttu-id="c7548-285">SignalR, .NET Framework 4 veya sonrasını gerektirir; Bu SignalR uygulamalarını Visual Studio 2010 veya üzeri geliştirilecek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c7548-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="c7548-286">IIS sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-286">IIS issues</span></span>

<span data-ttu-id="c7548-287">Bu bölüm, Internet Information Services ile ilgili sorunları içerir.</span><span class="sxs-lookup"><span data-stu-id="c7548-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="c7548-288">Web sitesi MapHubs çağırdıktan sonra kilitleniyor</span><span class="sxs-lookup"><span data-stu-id="c7548-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="c7548-289">SignalR son sürümünde bu sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7548-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="c7548-290">NuGet kullanarak yüklemenizi güncelleştirerek SignalR ' son yayınlanan sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c7548-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="c7548-291">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="c7548-291">Azure issues</span></span>

<span data-ttu-id="c7548-292">Bu bölüm, Microsoft Azure ile ilgili sorunlar içerir.</span><span class="sxs-lookup"><span data-stu-id="c7548-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="c7548-293">İletiler konu adları değiştirme sonra Azure devre kartına alınmıyor</span><span class="sxs-lookup"><span data-stu-id="c7548-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="c7548-294">Azure devre kartına tarafından kullanılan konular, kullanıcı tarafından yapılandırılabilen olması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c7548-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
