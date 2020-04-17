---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR Sorun Giderme (SignalR 1.x) | Microsoft Dokümanlar
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirme ile ilgili yaygın sorunlar açıklanmaktadır.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543099"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="052df-103">SignalR Sorunlarını Giderme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="052df-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="052df-104">tarafından [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="052df-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="052df-105">Bu belge, SignalR ile sık karşılaşılan sorun giderme sorunlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="052df-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="052df-106">Bu belge aşağıdaki bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="052df-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="052df-107">İstemci ve sunucu arasındaki arama yöntemleri sessizce başarısız olur</span><span class="sxs-lookup"><span data-stu-id="052df-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="052df-108">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="052df-109">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="052df-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="052df-110">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="052df-111">İnternet Bilgi Hizmetleri sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="052df-112">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="052df-113">İstemci ve sunucu arasındaki arama yöntemleri sessizce başarısız olur</span><span class="sxs-lookup"><span data-stu-id="052df-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="052df-114">Bu bölümde, istemci ve sunucu arasındaki yöntem çağrısının anlamlı bir hata iletisi olmadan başarısız olmasının olası nedenleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="052df-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="052df-115">SignalR uygulamasında, sunucunun istemcinin uyguladığı yöntemler hakkında hiçbir bilgisi yoktur; sunucu bir istemci yöntemi çağırdığında, yöntem adı ve parametre verileri istemciye gönderilir ve yöntem yalnızca sunucunun belirttiği biçimde varsa yürütülür.</span><span class="sxs-lookup"><span data-stu-id="052df-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="052df-116">İstemcide eşleşen bir yöntem bulunmazsa, hiçbir şey olmaz ve sunucuda hata iletisi yükseltilmez.</span><span class="sxs-lookup"><span data-stu-id="052df-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="052df-117">İstemci yöntemlerinin çağrılmadığını daha fazla araştırmak için, sunucudan hangi çağrıların geldiğini görmek için hub'daki başlangıç yöntemini aramadan önce günlüğe kaydetmeyi açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="052df-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="052df-118">JavaScript uygulamasında günlüğe kaydetmeyi etkinleştirmek [için istemci tarafı günlüğe kaydetmeyi (JavaScript istemci sürümü) nasıl etkinleştirin.](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="052df-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="052df-119">.NET istemci uygulamasında günlüğe kaydetmeyi etkinleştirmek [için istemci tarafı günlüğe kaydetmeyi (.NET İstemci sürümü) nasıl etkinleştirin.](../guide-to-the-api/hubs-api-guide-net-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="052df-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="052df-120">Yanlış yazılmış yöntem, yanlış yöntem imzası veya yanlış hub adı</span><span class="sxs-lookup"><span data-stu-id="052df-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="052df-121">Çağrılan bir yöntemin adı veya imzası istemcide uygun bir yöntemle tam olarak eşleşmiyorsa, arama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="052df-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="052df-122">Sunucu tarafından çağrılan yöntem adının istemcideki yöntemin adıyla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="052df-123">Ayrıca, SignalR JavaScript uygun olarak deve kasalı yöntemleri kullanarak hub proxy `SendMessage` oluşturur, bu nedenle `sendMessage` sunucuda çağrılan bir yöntem istemci proxy çağrılır.</span><span class="sxs-lookup"><span data-stu-id="052df-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="052df-124">Sunucu tarafındaki `HubName` kodunuzda özniteliği kullanırsanız, kullanılan adın istemcide hub'ı oluşturmak için kullanılan adla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="052df-125">Özniteliği kullanmıyorsanız, `HubName` JavaScript istemcisindeki hub'ın adının ChatHub yerine chatHub gibi deve kasası olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="052df-126">İstemciüzerinde yinelenen yöntem adı</span><span class="sxs-lookup"><span data-stu-id="052df-126">Duplicate method name on client</span></span>

<span data-ttu-id="052df-127">İstemcide yalnızca duruma göre farklılık gösteren bir yinelenen yönteminiz olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="052df-128">İstemci uygulamanızda adı `sendMessage`verilen bir yöntem varsa, aynı `SendMessage` zamanda çağrılan bir yöntem de olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="052df-129">Müşteri üzerinde Eksik JSON parser</span><span class="sxs-lookup"><span data-stu-id="052df-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="052df-130">SignalR, sunucu ve istemci arasındaki aramaları seri hale getirmek için bir JSON araleyicisinin bulunmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="052df-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="052df-131">İstemcinizin yerleşik bir JSON parer'i yoksa (Internet Explorer 7 gibi), uygulamanıza bir tane eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="052df-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="052df-132">[Burada](http://nuget.org/packages/json2)JSON parser indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="052df-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="052df-133">Karıştırma Hub ve PersistentConnection sözdizimi</span><span class="sxs-lookup"><span data-stu-id="052df-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="052df-134">SignalR iki iletişim modeli kullanır: Hub'lar ve Kalıcı Bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="052df-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="052df-135">Bu iki iletişim modelini arama sözdizimi istemci kodunda farklıdır.</span><span class="sxs-lookup"><span data-stu-id="052df-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="052df-136">Sunucu kodunuza bir hub eklediyseniz, istemci kodunun tamamının uygun hub sözdizimini kullandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="052df-137">**JavaScript istemcisinde Kalıcı Bağlantı oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="052df-138">**Javascript istemcisinde Hub Proxy oluşturan JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="052df-139">**Bir rotayı PersistentConnection'a eşleyen C# sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="052df-140">**Birden çok uygulamanız varsa, bir hub'a veya birden çok hub'a rota lar oluşturan C# sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="052df-141">Abonelikler eklenmeden önce bağlantı başlatıldı</span><span class="sxs-lookup"><span data-stu-id="052df-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="052df-142">Sunucudan çağrılabilen yöntemler proxy'ye eklenmeden Hub bağlantısı başlatılırsa, iletiler alınmaz.</span><span class="sxs-lookup"><span data-stu-id="052df-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="052df-143">Aşağıdaki JavaScript kodu hub'ı düzgün bir şekilde başlatmaz:</span><span class="sxs-lookup"><span data-stu-id="052df-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="052df-144">**Hubs iletilerinin alınmasına izin vermeyecek yanlış JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="052df-145">Bunun yerine, Başlat'ı aramadan önce yöntem aboneliklerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="052df-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="052df-146">**Bir hub'a abonelikleri doğru bir şekilde ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="052df-147">Hub proxy'de eksik yöntem adı</span><span class="sxs-lookup"><span data-stu-id="052df-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="052df-148">Sunucuda tanımlanan yöntemin istemcide abone olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="052df-149">Sunucu yöntemi tanımlasa da, yine de istemci proxy'ye eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="052df-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="052df-150">Yöntemler istemci proxy'ye aşağıdaki yollarla eklenebilir (Yöntemin doğrudan `client` hub'a değil, hub üyesine eklandığını unutmayın):</span><span class="sxs-lookup"><span data-stu-id="052df-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="052df-151">**Hub proxy'ye yöntem ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="052df-152">Genel olarak bildirilmemiş hub veya hub yöntemleri</span><span class="sxs-lookup"><span data-stu-id="052df-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="052df-153">İstemci üzerinde görünür olması için hub uygulaması `public`ve yöntemleri .</span><span class="sxs-lookup"><span data-stu-id="052df-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="052df-154">Hub'a farklı bir uygulamadan erişim</span><span class="sxs-lookup"><span data-stu-id="052df-154">Accessing hub from a different application</span></span>

<span data-ttu-id="052df-155">SignalR Hub'larına yalnızca SignalR istemcilerini uygulayan uygulamalar aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="052df-156">SignalR diğer iletişim kitaplıklarıyla (SOAP veya WCF web hizmetleri gibi) birlikte çalışamaz. Hedef platformunuz için kullanılabilir sinyalr istemcisi yoksa, sunucunun bitiş noktasına doğrudan erişemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="052df-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="052df-157">Verileri el ile serileştirme</span><span class="sxs-lookup"><span data-stu-id="052df-157">Manually serializing data</span></span>

<span data-ttu-id="052df-158">SignalR, yöntem parametrelerinizi seri hale getirmek için Otomatik olarak JSON'u kullanır- bunu kendiniz yapmanıza gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="052df-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="052df-159">Uzaktan Hub yöntemi OnDisconnected işlevinde istemcide yürütülmedi</span><span class="sxs-lookup"><span data-stu-id="052df-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="052df-160">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-160">This behavior is by design.</span></span> <span data-ttu-id="052df-161">Çağrıldığında, `OnDisconnected` hub zaten `Disconnected` daha fazla hub yöntemlerinin çağrılmasını izin vermez duruma girmiştir.</span><span class="sxs-lookup"><span data-stu-id="052df-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="052df-162">**OnDisconnected olayında kodu doğru şekilde yürüten C# sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="052df-163">Bağlantı sınırına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="052df-163">Connection limit reached</span></span>

<span data-ttu-id="052df-164">IIS'nin tam sürümünü Windows 7 gibi bir istemci işletim sisteminde kullanırken, 10 bağlantı sınırı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="052df-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="052df-165">İstemci işletim sistemi kullanırken, bu sınırdan kaçınmak için Bunun yerine IIS Express'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="052df-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="052df-166">Etki alanı bağlantısı düzgün ayarlanmamıştır</span><span class="sxs-lookup"><span data-stu-id="052df-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="052df-167">Bir etki alanı bağlantısı (SignalR URL'sinin barındırma sayfasıyla aynı etki alanında olmadığı bir bağlantı) doğru şekilde ayarlanmazsa, bağlantı hata iletisi olmadan başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="052df-168">Etki alanları arası iletişimi etkinleştirme hakkında bilgi için, [etki alanları arası bağlantının nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)öğrenin.</span><span class="sxs-lookup"><span data-stu-id="052df-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="052df-169">.NET istemcisinde çalışmayan NTLM (Active Directory) kullanarak bağlantı</span><span class="sxs-lookup"><span data-stu-id="052df-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="052df-170">Bağlantı düzgün yapılandırılmamışsa, Etki Alanı güvenliğini kullanan bir .NET istemci uygulamasındaki bağlantı başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="052df-171">SignalR'i etki alanı ortamında kullanmak için gerekli bağlantı özelliğini aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="052df-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="052df-172">**Bağlantı kimlik bilgilerini uygulayan C# istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="052df-173">Diğer bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-173">Other connection issues</span></span>

<span data-ttu-id="052df-174">Bu bölümde, bağlantı sırasında oluşan belirli belirtiler veya hata iletileri için nedenler ve çözümler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="052df-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="052df-175">"Veriler gönderilmeden önce Başlat çağrılmalı" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="052df-176">Bu hata genellikle bağlantı başlatılmadan önce signalr nesnelerine başvuruyorsa görülür.</span><span class="sxs-lookup"><span data-stu-id="052df-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="052df-177">Bağlantı tamamlandıktan sonra sunucuda tanımlanan yöntemleri çağıracak işleyiciler ve benzeri için wireup eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="052df-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="052df-178">Çağrının eşzamanlı `Start` olduğunu unutmayın, bu nedenle arama tamamlandıktan sonra kod yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="052df-179">Bağlantı tamamen başladıktan sonra işleyicileri eklemenin en iyi yolu, bunları başlangıç yöntemine parametre olarak geçirilen bir geri arama işlevine koymaktır:</span><span class="sxs-lookup"><span data-stu-id="052df-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="052df-180">**SignalR nesnelerine başvuran olay işleyicilerini doğru bir şekilde ekleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="052df-181">SignalR nesneleri hala başvurulmaktayken bir bağlantı durursa bu hata da görülür.</span><span class="sxs-lookup"><span data-stu-id="052df-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="052df-182">"301 Kalıcı Olarak Taşınmış" veya "302 Geçici Olarak Taşınmış" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="052df-183">Proje, otomatik olarak oluşturulan proxy'yi engelleyecek SignalR adlı bir klasör içeriyorsa bu hata görülebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="052df-184">Bu hatayı önlemek için, uygulamanızda `SignalR` adı geçen bir klasör kullanmayın veya otomatik proxy oluşturmayı kapatın.</span><span class="sxs-lookup"><span data-stu-id="052df-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="052df-185">[Oluşturulan Proxy'ye ve](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) daha fazla ayrıntı için sizin için neler yaptığını görün.</span><span class="sxs-lookup"><span data-stu-id="052df-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="052df-186">.NET veya Silverlight istemcisinde "403 Yasak" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="052df-187">Bu hata, etki alanları arası iletişimin düzgün şekilde etkinleştirilen olmadığı etki alanları arası ortamlarda oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="052df-188">Etki alanları arası iletişimi etkinleştirme hakkında bilgi için, [etki alanları arası bağlantının nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)öğrenin.</span><span class="sxs-lookup"><span data-stu-id="052df-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="052df-189">Silverlight istemcisinde etki alanı bağlantısı kurmak için [Silverlight istemcilerinden çapraz etki alanı bağlantılarına](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="052df-190">"404 Bulunamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-190">"404 Not Found" error</span></span>

<span data-ttu-id="052df-191">Bu sorunun çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="052df-191">There are several causes for this issue.</span></span> <span data-ttu-id="052df-192">Aşağıdakilerin tümlerini doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="052df-192">Verify all of the following:</span></span>

- <span data-ttu-id="052df-193">**Hub proxy adresi başvurusu doğru biçimlendirilmemiş:** Oluşturulan hub proxy adresine başvuru doğru biçimlendirme değilse, bu hata genellikle görülür.</span><span class="sxs-lookup"><span data-stu-id="052df-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="052df-194">Hub adresine yapılan başvurunun doğru yapıldığından doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="052df-195">Ayrıntılar için [dinamik olarak oluşturulan proxy'ye nasıl başvurulsağlayacağına](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="052df-196">**Hub rotasını eklemeden önce uygulamaya yol ekleme:** Uygulamanız başka yollar kullanıyorsa, `MapHubs`eklenen ilk rotanın .</span><span class="sxs-lookup"><span data-stu-id="052df-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="052df-197">"500 Dahili Sunucu Hatası"</span><span class="sxs-lookup"><span data-stu-id="052df-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="052df-198">Bu nedenleri geniş bir yelpazede olabilir çok genel bir hatadır.</span><span class="sxs-lookup"><span data-stu-id="052df-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="052df-199">Hatanın ayrıntıları sunucunun olay günlüğünde görünmelidir veya sunucunun hata ayıklama yoluyla bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="052df-200">Sunucudaki ayrıntılı hataları açarak daha ayrıntılı hata bilgileri elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="052df-201">Daha fazla bilgi için [Hub sınıfındaki hataları nasıl işlersin.](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)</span><span class="sxs-lookup"><span data-stu-id="052df-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="052df-202">"TypeError: &lt;hubType&gt; tanımsız" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="052df-203">Arama düzgün yapılmazsa `MapHubs` bu hata ortaya çıkacaktır.</span><span class="sxs-lookup"><span data-stu-id="052df-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="052df-204">[SinyalR rotasını nasıl kaydedin ve](../guide-to-the-api/hubs-api-guide-server.md#route) daha fazla bilgi için SignalR seçeneklerini yapılandırmaya bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="052df-205">JsonSerializationException kullanıcı kodu tarafından işlenmemiş oldu</span><span class="sxs-lookup"><span data-stu-id="052df-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="052df-206">Yöntemlerinize gönderdiğiniz parametrelerin seri olarak izlenebilir olmayan türleri (dosya tutamaçları veya veritabanı bağlantıları gibi) içermediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="052df-207">İstemciye gönderilmek istemediğiniz sunucu tarafındaki bir nesnede (güvenlik için veya serileştirme nedeniyle) üye kullanmanız `JSONIgnore` gerekiyorsa, özniteliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="052df-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="052df-208">"Protokol hatası: Bilinmeyen aktarım" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="052df-209">İstemci SignalR'ın kullandığı aktarımları desteklemiyorsa bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="052df-210">SignalR ile hangi tarayıcıların kullanılabileceğini bilgi için [Transports ve Fallbacks'e](../getting-started/introduction-to-signalr.md#transports) bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="052df-211">"JavaScript Hub proxy oluşturma devre dışı bırakıldı."</span><span class="sxs-lookup"><span data-stu-id="052df-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="052df-212">Dinamik olarak oluşturulan `DisableJavaScriptProxies` proxy'ye bir başvuru da dahil edilirken `signalr/hubs`ayarlanırsa bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="052df-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="052df-213">Proxy'yi el ile oluşturma hakkında daha fazla bilgi için [oluşturulan proxy'ye ve sizin için neler yaptığına](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="052df-214">"Bağlantı kimliği yanlış biçimde" veya "Etkin bir SinyalR bağlantısı sırasında kullanıcı kimliği değiştirilemez" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="052df-215">Kimlik doğrulaması kullanılıyorsa ve bağlantı durdurulmadan önce istemci oturumu kapatılırsa bu hata görülebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="052df-216">Çözüm, istemciyi oturumu açmadan önce SignalR bağlantısını durdurmaktır.</span><span class="sxs-lookup"><span data-stu-id="052df-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="052df-217">"Yakalanmayan Hata: SignalR: jQuery bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="052df-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="052df-218">Lütfen SignalR.js dosyasından önce jQuery'ye başvuruldığından emin olun" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="052df-219">SignalR JavaScript istemcisi jQuery'nin çalışmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="052df-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="052df-220">jQuery başvurunuzun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery'ye yapılan başvurunun SignalR'a başvurudan önce olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="052df-221">"Caught TypeError: Tanımlanmamış&lt;özellik&gt;' özelliği ' okuyamıyorum" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="052df-222">Bu hata, jQuery veya hub proxy düzgün başvurulan olmaması ndan kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="052df-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="052df-223">jQuery ve hub proxy'ye başvurunuzun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery'ye yapılan başvurunun hub proxy'ye başvurudan önce olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="052df-224">Hub'lar proxy varsayılan başvuru aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="052df-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="052df-225">**Hubs proxy'ye doğru başvuran HTML istemci tarafı kodu**</span><span class="sxs-lookup"><span data-stu-id="052df-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="052df-226">"RuntimeBinderException kullanıcı kodu tarafından işlenmemiş oldu" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="052df-227">Yanlış aşırı yükleme `Hub.On` kullanıldığında bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="052df-228">Yöntemin iade değeri varsa, iade türü genel bir tür parametresi olarak belirtilmelidir:</span><span class="sxs-lookup"><span data-stu-id="052df-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="052df-229">**İstemci üzerinde tanımlanan yöntem (oluşturulan proxy olmadan)**</span><span class="sxs-lookup"><span data-stu-id="052df-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="052df-230">Bağlantı kimliği tutarsız veya sayfa yükleri arasında bağlantı sonu</span><span class="sxs-lookup"><span data-stu-id="052df-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="052df-231">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-231">This behavior is by design.</span></span> <span data-ttu-id="052df-232">Hub nesnesi sayfa nesnesinde barındırıldığından, sayfa yenilendiğinde hub yok edilir.</span><span class="sxs-lookup"><span data-stu-id="052df-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="052df-233">Çok sayfalı bir uygulama, sayfa yükleri arasında tutarlı olacak şekilde kullanıcılar ve bağlantı disleri arasındaki ilişkiyi korumak gerekir.</span><span class="sxs-lookup"><span data-stu-id="052df-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="052df-234">Bağlantı adları sunucuda bir `ConcurrentDictionary` nesne de veya veritabanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="052df-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="052df-235">"Değer null olamaz" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-235">"Value cannot be null" error</span></span>

<span data-ttu-id="052df-236">İsteğe bağlı parametrelere sahip sunucu tarafı yöntemleri şu anda desteklenmez; isteğe bağlı parametre atlanırsa, yöntem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="052df-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="052df-237">Daha fazla bilgi için [Isteğe Bağlı Parametreler'e](https://github.com/SignalR/SignalR/issues/324)bakın.</span><span class="sxs-lookup"><span data-stu-id="052df-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="052df-238">Firebug hata "Firefox &lt;adresinde&gt;sunucuya bir bağlantı kuramaz "</span><span class="sxs-lookup"><span data-stu-id="052df-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="052df-239">WebSocket aktarımının anlaşması başarısız olursa ve bunun yerine başka bir aktarım kullanılırsa, bu hata iletisi Firebug'da görülebilir.</span><span class="sxs-lookup"><span data-stu-id="052df-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="052df-240">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="052df-241">.NET istemci uygulamasında "Uzak sertifika doğrulama prosedürüne göre geçersizdir" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="052df-242">Sunucunuz özel istemci sertifikaları gerektiriyorsa, istek yapılmadan önce bağlantıya x509sertifikası ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="052df-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="052df-243">Kullanarak bağlantıya sertifika `Connection.AddClientCertificate`ekleyin.</span><span class="sxs-lookup"><span data-stu-id="052df-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="052df-244">Kimlik doğrulama süreleri bittikten sonra bağlantı düşer</span><span class="sxs-lookup"><span data-stu-id="052df-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="052df-245">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-245">This behavior is by design.</span></span> <span data-ttu-id="052df-246">Bağlantı etkinken kimlik doğrulama kimlik bilgileri değiştirilemez; kimlik bilgilerini yenilemek için bağlantının durdurulması ve yeniden başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="052df-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="052df-247">OnConnected jQuery Mobile kullanırken iki kez çağrılır</span><span class="sxs-lookup"><span data-stu-id="052df-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="052df-248">jQuery Mobile'ın `initializePage` işlevi, her sayfadaki komut dosyalarını yeniden yürütülmesi için zorlayarak ikinci bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="052df-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="052df-249">Bu soruna yönelik çözümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="052df-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="052df-250">JavaScript dosyanızdan önce jQuery Mobile'a başvuruyu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="052df-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="052df-251">İşlevayarlayarak `initializePage` `$.mobile.autoInitializePage = false`işlevi devre dışı</span><span class="sxs-lookup"><span data-stu-id="052df-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="052df-252">Bağlantıyı başlatmadan önce sayfanın başlatmayı bitirmesini bekleyin.</span><span class="sxs-lookup"><span data-stu-id="052df-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="052df-253">Sunucu Gönderilen Etkinlikler kullanılarak Silverlight uygulamalarında iletiler geciktirilir</span><span class="sxs-lookup"><span data-stu-id="052df-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="052df-254">Silverlight'ta sunucu nun gönderdiği olaylar kullanılarak iletiler gecikiyor.</span><span class="sxs-lookup"><span data-stu-id="052df-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="052df-255">Bunun yerine uzun yoklamanın kullanılmasını zorlamak için bağlantıyı kurarken aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="052df-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="052df-256">Forever Frame protokolünü kullanarak "İzin Reddedildi"</span><span class="sxs-lookup"><span data-stu-id="052df-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="052df-257">Bu bilinen bir konudur, [burada](https://github.com/SignalR/SignalR/issues/1963)açıklanan.</span><span class="sxs-lookup"><span data-stu-id="052df-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="052df-258">Bu belirti en son JQuery kitaplığı kullanılarak görülebilir; geçici çözüm JQuery 1.8.2 için uygulamanızı düşürmek için.</span><span class="sxs-lookup"><span data-stu-id="052df-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="052df-259">Derleme ve sunucu tarafı hataları</span><span class="sxs-lookup"><span data-stu-id="052df-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="052df-260">Aşağıdaki bölümde derleyici ve sunucu tarafı çalışma zamanı hataları için olası çözümler içerir.</span><span class="sxs-lookup"><span data-stu-id="052df-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="052df-261">Hub örneğine başvuru null</span><span class="sxs-lookup"><span data-stu-id="052df-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="052df-262">Her bağlantı için bir hub örneği oluşturulduğundan, kodunuzda kendiniz hub örneği oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="052df-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="052df-263">Hub'ın dışından bir hub'da yöntemleri çağırmak için, hub bağlamına başvuru almak için [hub sınıfının dışından gelen grupları nasıl arayacağınızı ve grupları](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) nasıl yöneteceklerini görün.</span><span class="sxs-lookup"><span data-stu-id="052df-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="052df-264">HTTPContext.Current.Session geçersizdir</span><span class="sxs-lookup"><span data-stu-id="052df-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="052df-265">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-265">This behavior is by design.</span></span> <span data-ttu-id="052df-266">SignalR, oturum durumunu etkinleştirme çift yönlü iletiyi kıracağı için ASP.NET oturum durumunu desteklemez.</span><span class="sxs-lookup"><span data-stu-id="052df-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="052df-267">Geçersiz kılmak için uygun bir yöntem yok</span><span class="sxs-lookup"><span data-stu-id="052df-267">No suitable method to override</span></span>

<span data-ttu-id="052df-268">Eski belgelerden veya bloglardan kod kullanıyorsanız bu hatayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="052df-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="052df-269">Değiştirilen veya amortismana alınmış yöntemlerin adlarını (örneğin) `OnConnectedAsync`başvurmadığınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="052df-270">HostContextExtensions.WebSocketServerUrl null</span><span class="sxs-lookup"><span data-stu-id="052df-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="052df-271">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-271">This behavior is by design.</span></span> <span data-ttu-id="052df-272">Bu üye amortismana sokulmalıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="052df-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="052df-273">"'signalr.hub' adlı bir rota zaten rota koleksiyonunda" hatası</span><span class="sxs-lookup"><span data-stu-id="052df-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="052df-274">Uygulamanız tarafından iki `MapHubs` kez çağrılırsa bu hata görülecektir.</span><span class="sxs-lookup"><span data-stu-id="052df-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="052df-275">Bazı örnek uygulamalar `MapHubs` doğrudan genel uygulama dosyasında arama; diğerleri bir sarmalayıcı sınıfında arama yapmak.</span><span class="sxs-lookup"><span data-stu-id="052df-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="052df-276">Uygulamanızın her ikisini de yapmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="052df-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="052df-277">Visual Studio sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-277">Visual Studio issues</span></span>

<span data-ttu-id="052df-278">Bu bölümde Visual Studio'da karşılaşılan sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="052df-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="052df-279">Komut Dosyası Belgeleri düğümü Çözüm Gezgini'nde görünmüyor</span><span class="sxs-lookup"><span data-stu-id="052df-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="052df-280">Bazı öğreticilerimiz hata ayıklama sırasında sizi Solution Explorer'daki "Komut Dosyası Belgeleri" düğümüne yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="052df-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="052df-281">Bu düğüm JavaScript hata ayıklama tarafından üretilir ve yalnızca Internet Explorer'da tarayıcı istemcilerini hata ayıklarken görünür; Chrome veya Firefox kullanılırsa düğüm görünmez.</span><span class="sxs-lookup"><span data-stu-id="052df-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="052df-282">Silverlight hata ayıklama gibi başka bir istemci hata ayıklama çalışıyorsa JavaScript hata ayıklama da çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="052df-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="052df-283">SignalR Visual Studio 2008 veya daha önce çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="052df-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="052df-284">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="052df-284">This behavior is by design.</span></span> <span data-ttu-id="052df-285">SignalR gerektirir .NET Framework 4 veya daha sonra; bu, SignalR uygulamalarının Visual Studio 2010 veya sonraki yıllarda geliştirilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="052df-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="052df-286">IIS sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-286">IIS issues</span></span>

<span data-ttu-id="052df-287">Bu bölümde Internet Bilgi Hizmetleri ile ilgili sorunlar içerir.</span><span class="sxs-lookup"><span data-stu-id="052df-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="052df-288">MapHubs çağrısından sonra web sitesi çöküyor</span><span class="sxs-lookup"><span data-stu-id="052df-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="052df-289">Bu sorun SignalR'ın en son sürümünde giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="052df-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="052df-290">Yüklemenizi NuGet kullanarak güncelleyerek SignalR'ın en son sürümünden kullandığınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="052df-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="052df-291">Azure sorunları</span><span class="sxs-lookup"><span data-stu-id="052df-291">Azure issues</span></span>

<span data-ttu-id="052df-292">Bu bölümde Microsoft Azure ile ilgili sorunlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="052df-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="052df-293">Konu adlarını değiştirdikten sonra Iletiler Azure arka düzlemi üzerinden alınmaz</span><span class="sxs-lookup"><span data-stu-id="052df-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="052df-294">Azure arka düzlemi tarafından kullanılan konular kullanıcı tarafından yapılandırılabilir olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="052df-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
