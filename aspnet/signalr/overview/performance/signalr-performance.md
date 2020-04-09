---
uid: signalr/overview/performance/signalr-performance
title: SignalR Performans | Microsoft Dokümanlar
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676092"
---
# <a name="signalr-performance"></a><span data-ttu-id="db4d4-103">SignalR Performansı</span><span class="sxs-lookup"><span data-stu-id="db4d4-103">SignalR Performance</span></span>

<span data-ttu-id="db4d4-104">tarafından [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="db4d4-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="db4d4-105">Bu konu, SignalR uygulamasında performansı nasıl tasarlayabilmek, ölçmek ve geliştirmek için açıklanır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="db4d4-106">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="db4d4-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="db4d4-107">Görsel Stüdyo 2013</span><span class="sxs-lookup"><span data-stu-id="db4d4-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="db4d4-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="db4d4-108">.NET 4.5</span></span>
> - <span data-ttu-id="db4d4-109">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="db4d4-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="db4d4-110">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="db4d4-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="db4d4-111">SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="db4d4-112">Sorular ve yorumlar</span><span class="sxs-lookup"><span data-stu-id="db4d4-112">Questions and comments</span></span>
>
> <span data-ttu-id="db4d4-113">Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="db4d4-114">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db4d4-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="db4d4-115">SignalR performansı ve ölçekleme ile ilgili yeni bir sunum için, [ASP.NET SignalR ile Gerçek Zamanlı Web ölçekleme](https://channel9.msdn.com/Events/Build/2013/3-502)bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="db4d4-116">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="db4d4-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="db4d4-117">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="db4d4-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="db4d4-118">Performans için SignalR sunucunuzu ayarla</span><span class="sxs-lookup"><span data-stu-id="db4d4-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="db4d4-119">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="db4d4-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="db4d4-120">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="db4d4-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="db4d4-121">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="db4d4-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="db4d4-122">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="db4d4-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="db4d4-123">Tasarım konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="db4d4-123">Design considerations</span></span>

<span data-ttu-id="db4d4-124">Bu bölümde, gereksiz ağ trafiği oluşturarak performansın engellenmediğinden emin olmak için SignalR uygulamasının tasarımı sırasında uygulanabilecek desenler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="db4d4-125">İleti sıklığını azaltma</span><span class="sxs-lookup"><span data-stu-id="db4d4-125">Throttling message frequency</span></span>

<span data-ttu-id="db4d4-126">Yüksek frekansta (gerçek zamanlı oyun uygulaması gibi) ileti gönderen bir uygulamada bile, çoğu uygulamanın saniyede birkaç iletiden fazlasını göndermesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="db4d4-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="db4d4-127">Her istemcinin oluşturduğu trafik miktarını azaltmak için, sabit bir hızdan daha sık sıraya alınan ve ileti gönderen bir ileti döngüsü uygulanabilir (diğer bir deyişle, gönderilmek üzere bu zaman aralığında iletiler varsa, her saniye belirli sayıda ileti gönderilir).</span><span class="sxs-lookup"><span data-stu-id="db4d4-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="db4d4-128">İletileri belirli bir hıza (hem istemciden hem de sunucudan) azaltan örnek bir uygulama için [SignalR ile Yüksek Frekanslı Gerçek Zamanlı'ya](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="db4d4-129">İleti boyutunu küçültme</span><span class="sxs-lookup"><span data-stu-id="db4d4-129">Reducing message size</span></span>

<span data-ttu-id="db4d4-130">Seri leştirilmiş nesnelerinizin boyutunu azaltarak SignalR iletisinin boyutunu küçültebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db4d4-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="db4d4-131">Sunucu kodunda, aktarılması gerekmeyen özellikler içeren bir nesne gönderiyorsanız, bu özelliklerin özniteliği kullanarak `JsonIgnore` seri hale getirilmesini engelleyin.</span><span class="sxs-lookup"><span data-stu-id="db4d4-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="db4d4-132">Özelliklerin adları da iletide depolanır; özelliklerinin adları öznitelik kullanılarak `JsonProperty` kısaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="db4d4-133">Aşağıdaki kod örneği, bir özelliğin istemciye gönderilmesini nasıl dışlayabildiğini ve özellik adlarının nasıl kısaltılabildiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="db4d4-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="db4d4-134">**Verilerin istemciye gönderilmesini hariç tutmak için JsonIgnore özniteliğini ve ileti boyutunu küçültmek için JsonProperty özniteliğini gösteren .NET sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="db4d4-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="db4d4-135">İstemci kodunda okunabilirliği/ korunabilmeyi korumak için, kısaltılmış özellik adları, ileti alındıktan sonra insan dostu adlara yeniden eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="db4d4-136">Aşağıdaki kod örneği, bir ileti sözleşmesi (eşleme) tanımlayarak ve sözleşmeyi en iyi duruma `reMap` getirin sınıfına uygulamak için işlevi kullanarak kısaltılmış adları daha uzun adlarla yeniden eşlemenin olası bir yolunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="db4d4-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="db4d4-137">**Kısaltılmış özellik adlarını insan tarafından okunabilir adlara yeniden eşleyen istemci tarafı JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="db4d4-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="db4d4-138">Aynı yöntem kullanılarak istemciden sunucuya gelen iletilerde adlar da kısaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="db4d4-139">İleti nesnesinin bellek ayak izini (diğer bir şekilde ileti için kullanılan bellek miktarını) azaltmak da performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="db4d4-140">Örneğin, a `int` aralığının tam aralığı gerekli `short` değilse, a veya `byte` bunun yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="db4d4-141">İletiler sunucu belleğinde ileti veri tonunda depolandığından, iletilerin boyutunu azaltmak da sunucu bellek sorunlarını giderebilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="db4d4-142">Performans için SignalR sunucunuzu ayarla</span><span class="sxs-lookup"><span data-stu-id="db4d4-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="db4d4-143">Aşağıdaki yapılandırma ayarları, bir SignalR uygulamasında sunucunuzu daha iyi performans için ayarlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="db4d4-144">bir ASP.NET uygulamasında performansı nasıl artırılavureceğiniz hakkında genel bilgi [ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx)için bkz.</span><span class="sxs-lookup"><span data-stu-id="db4d4-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="db4d4-145">**SignalR yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="db4d4-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="db4d4-146">**DefaultMessageBufferSize**: Varsayılan olarak SignalR, bağlantı başına hub başına bellekte 1000 ileti saklar.</span><span class="sxs-lookup"><span data-stu-id="db4d4-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="db4d4-147">Büyük iletiler kullanılıyorsa, bu değer azaltılarak hafifletilebilecek bellek sorunları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="db4d4-148">Bu ayar, ASP.NET `Application_Start` bir uygulamada olay işleyicisi `Configuration` veya kendi kendine barındırılan bir uygulamada bir OWIN başlangıç sınıfı nın yönteminde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="db4d4-149">Aşağıdaki örnek, kullanılan sunucu bellek miktarını azaltmak için uygulamanızın bellek ayak izini azaltmak için bu değeri nasıl azalttığınızı gösterir:</span><span class="sxs-lookup"><span data-stu-id="db4d4-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="db4d4-150">**.NET sunucu kodu, varsayılan ileti arabellek boyutunu azaltmak için Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="db4d4-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="db4d4-151">**IIS yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="db4d4-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="db4d4-152">**Uygulama başına maksimum eşzamanlı istekler**: Eşzamanlı IIS isteklerinin sayısının artırılması, isteklerin sunulması için kullanılabilen sunucu kaynaklarını artırır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="db4d4-153">Varsayılan değer 5000'dir; bu ayarı artırmak için, yükseltilmiş bir komut istemi aşağıdaki komutları yürütmek:</span><span class="sxs-lookup"><span data-stu-id="db4d4-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="db4d4-154">**ApplicationPool QueueLength**: Bu, uygulama havuzu için Http.sys kuyrukları en fazla istek sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="db4d4-155">Sıra dolduğunda, yeni istekler 503 "Hizmet Kullanılamıyor" yanıtı alır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="db4d4-156">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-156">The default value is 1000.</span></span>

    <span data-ttu-id="db4d4-157">Uygulamanızı barındıran uygulama havuzunda alt işlem için sıra uzunluğunun kısaltılması bellek kaynaklarını korur.</span><span class="sxs-lookup"><span data-stu-id="db4d4-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="db4d4-158">Daha fazla bilgi için bkz: [Uygulama Havuzlarını Yönetme, Ayarla ve Yapılandırma.](https://technet.microsoft.com/library/cc745955.aspx)</span><span class="sxs-lookup"><span data-stu-id="db4d4-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="db4d4-159">**yapılandırma ayarlarını ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="db4d4-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="db4d4-160">Bu `aspnet.config` bölüm, dosyada ayarlanabilen yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="db4d4-161">Bu dosya, platforma bağlı olarak iki konumdan birinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="db4d4-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="db4d4-162">SignalR performansını artırabilecek ASP.NET ayarları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="db4d4-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="db4d4-163">**CPU başına maksimum eşzamanlı istek**: Bu ayarı artırmak performans darboğazlarını hafifletebilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="db4d4-164">Bu ayarı artırmak için dosyaya `aspnet.config` aşağıdaki yapılandırma ayarını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="db4d4-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="db4d4-165">**İstek Sırası Sınırı**: Toplam bağlantı sayısı `maxConcurrentRequestsPerCPU` ayarı aştığında, ASP.NET bir sıra kullanarak istekleri azaltmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="db4d4-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="db4d4-166">Sıranın boyutunu artırmak için `requestQueueLimit` ayarı artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db4d4-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="db4d4-167">Bunu yapmak için, düğüme aşağıdaki `processModel` yapılandırma `config/machine.config` ayarını `aspnet.config`ekleyin (yerine):</span><span class="sxs-lookup"><span data-stu-id="db4d4-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="db4d4-168">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="db4d4-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="db4d4-169">Bu bölümde, uygulamanızda performans sorunları bulmayolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="db4d4-170">WebSocket'in kullanıldığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="db4d4-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="db4d4-171">SignalR istemci ve sunucu arasındaki iletişim için çeşitli aktarımlar kullanabilir, ancak WebSocket önemli bir performans avantajı sunar ve istemci ve sunucu bunu destekliyorsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="db4d4-172">İstemcinizin ve sunucunuzun WebSocket gereksinimlerini karşılayıp karşılamadığını belirlemek için [Taşımalar ve Geri Dönüşler'e](../getting-started/introduction-to-signalr.md#transports)bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="db4d4-173">Uygulamanızda hangi aktarımın kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanabilir ve bağlantı için hangi aktarımın kullanıldığını görmek için günlükleri inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db4d4-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="db4d4-174">Internet Explorer ve Chrome'daki tarayıcı geliştirme araçlarını kullanma hakkında daha fazla bilgi için [Taşımalar ve Geri Dönüşler'e](../getting-started/introduction-to-signalr.md#transports)bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="db4d4-175">SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="db4d4-175">Using SignalR performance counters</span></span>

<span data-ttu-id="db4d4-176">Bu bölümde, `Microsoft.AspNet.SignalR.Utils` pakette bulunan SignalR performans sayaçlarının nasıl etkinleştirilip kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="db4d4-177">signalr.exe kurulumu</span><span class="sxs-lookup"><span data-stu-id="db4d4-177">Installing signalr.exe</span></span>

<span data-ttu-id="db4d4-178">Performans sayaçları SignalR.exe adlı bir yardımcı program kullanılarak sunucuya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="db4d4-179">Bu yardımcı programı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="db4d4-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="db4d4-180">Visual Studio'da, **Araçlar** > **NuGet Paket Yöneticisi** > **Çözüm için NuGet Paketlerini Yönet'i** seçin</span><span class="sxs-lookup"><span data-stu-id="db4d4-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="db4d4-181">**Signalr.utils'i**arayın ve Yükle'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="db4d4-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="db4d4-182">Paketi yüklemek için lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="db4d4-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="db4d4-183">SignalR.exe'ye `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="db4d4-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="db4d4-184">SignalR.exe ile performans sayaçları yükleme</span><span class="sxs-lookup"><span data-stu-id="db4d4-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="db4d4-185">SignalR performans sayaçlarını yüklemek için SignalR.exe'yi aşağıdaki parametreyle yükseltilmiş bir komut istemiyle çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db4d4-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="db4d4-186">SignalR performans sayaçlarını kaldırmak için SignalR.exe'yi aşağıdaki parametreyle yükseltilmiş bir komut istemiyle çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db4d4-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="db4d4-187">SignalR Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="db4d4-187">SignalR Performance counters</span></span>

<span data-ttu-id="db4d4-188">Yardımcı programlar paketi aşağıdaki performans sayaçlarını yükler.</span><span class="sxs-lookup"><span data-stu-id="db4d4-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="db4d4-189">"Toplam" sayaçları, son uygulama havuzu veya sunucu yeniden başlatılmasından bu yana olayların sayısını ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="db4d4-190">**Bağlantı ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-190">**Connection metrics**</span></span>

<span data-ttu-id="db4d4-191">Aşağıdaki ölçümler, oluşan bağlantı ömrü olaylarını ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="db4d4-192">Daha fazla bilgi için [bkz.](../guide-to-the-api/handling-connection-lifetime-events.md)</span><span class="sxs-lookup"><span data-stu-id="db4d4-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="db4d4-193">**Bağlı Bağlantılar**</span><span class="sxs-lookup"><span data-stu-id="db4d4-193">**Connections Connected**</span></span>
- <span data-ttu-id="db4d4-194">**Bağlantılar Yeniden Bağlandı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="db4d4-195">**Bağlantıları Kesildi**</span><span class="sxs-lookup"><span data-stu-id="db4d4-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="db4d4-196">**Bağlantılar Güncel**</span><span class="sxs-lookup"><span data-stu-id="db4d4-196">**Connections Current**</span></span>

<span data-ttu-id="db4d4-197">**İleti ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-197">**Message metrics**</span></span>

<span data-ttu-id="db4d4-198">Aşağıdaki ölçümler SignalR tarafından oluşturulan ileti trafiğini ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="db4d4-199">**Toplam Alınan Bağlantı İletileri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="db4d4-200">**Toplam Gönderilen Bağlantı İletileri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="db4d4-201">**Alınan Bağlantı İletileri/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="db4d4-202">**Gönderilen Bağlantı İletileri/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="db4d4-203">**İleti veri günü ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-203">**Message bus metrics**</span></span>

<span data-ttu-id="db4d4-204">Aşağıdaki ölçümler, gelen ve giden tüm SignalR iletilerinin yerleştirildiği sıra olan dahili SignalR ileti veri yolundaki trafiği ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="db4d4-205">İleti gönderildiğinde veya yayınlandığında **yayınlanır.**</span><span class="sxs-lookup"><span data-stu-id="db4d4-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="db4d4-206">Bu bağlamda **abone,** ileti veri yolundaki bir aboneliktir; bu istemci sayısı artı sunucunun kendisi eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="db4d4-207">**Ayrılan Çalışan,** etkin bağlantılara veri gönderen bir bileşendir; **Meşgul** İşçisi, etkin olarak ileti gönderen bir çalışandır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="db4d4-208">**İleti Veri Gönderi Mesajları Toplam Alınan**</span><span class="sxs-lookup"><span data-stu-id="db4d4-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="db4d4-209">**Alınan İleti Veri Gönderi Mesajları/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="db4d4-210">**İleti Veri Günü Mesajları Toplam Yayınlandı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="db4d4-211">**İleti Veri Günü Mesajları Yayınlandı/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="db4d4-212">**Mesaj Veri Günü Aboneleri Güncel**</span><span class="sxs-lookup"><span data-stu-id="db4d4-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="db4d4-213">**İleti Veri Günü Aboneleri Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="db4d4-214">**İleti Veri Günü Aboneleri/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="db4d4-215">**İleti Veri Otobüsü Tahsisli İşçiler**</span><span class="sxs-lookup"><span data-stu-id="db4d4-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="db4d4-216">**Mesaj Otobüs Meşgul İşçiler**</span><span class="sxs-lookup"><span data-stu-id="db4d4-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="db4d4-217">**İleti Veri Günü Konuları Güncel**</span><span class="sxs-lookup"><span data-stu-id="db4d4-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="db4d4-218">**Hata ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-218">**Error metrics**</span></span>

<span data-ttu-id="db4d4-219">Aşağıdaki ölçümler SignalR ileti trafiği tarafından oluşturulan hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="db4d4-220">**Hub** veya hub yöntemi çözülemediğinde Hub Çözümü hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="db4d4-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="db4d4-221">**Hub Çağırma** hataları, hub yöntemini çağırırken atılan özel durumlardır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="db4d4-222">**Aktarım** hataları, http isteği veya yanıtı sırasında atılan bağlantı hatalarıdır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="db4d4-223">**Hatalar: Tüm Toplam**</span><span class="sxs-lookup"><span data-stu-id="db4d4-223">**Errors: All Total**</span></span>
- <span data-ttu-id="db4d4-224">**Hatalar: Tümü/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="db4d4-225">**Hatalar: Hub Çözünürlük Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="db4d4-226">**Hatalar: Hub Çözünürlüğü/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="db4d4-227">**Hatalar: Hub Çağırma Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="db4d4-228">**Hatalar: Hub Çağırma/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="db4d4-229">**Hatalar: Aktarım Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="db4d4-230">**Hatalar: Aktarım/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="db4d4-231">**Ölçeklendirme ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="db4d4-231">**Scaleout metrics**</span></span>

<span data-ttu-id="db4d4-232">Aşağıdaki ölçümler, ölçeklendirme sağlayıcısı tarafından oluşturulan trafiği ve hataları ölçer.</span><span class="sxs-lookup"><span data-stu-id="db4d4-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="db4d4-233">Bu bağlamda bir **Akış** ölçeklendirme sağlayıcısı tarafından kullanılan bir ölçek birimidir; BU tablo, SQL Server kullanılıyorsa, Hizmet Veri Tos'u kullanılıyorsa bir Konu ve Redis kullanılıyorsa Abonelik.</span><span class="sxs-lookup"><span data-stu-id="db4d4-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="db4d4-234">Her akış, sipariş edilen okuma ve yazma işlemlerini sağlar; tek bir akış olası bir ölçek darboğaz, bu nedenle akış sayısı bu darboğaz azaltmaya yardımcı olmak için artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="db4d4-235">Birden çok akış kullanılırsa, SignalR iletileri bu akışlar arasında belirli bir bağlantıdan gönderilen iletilerin sıralı olmasını sağlayacak şekilde otomatik olarak dağıtır (parça) iletileri dağıtır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="db4d4-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) ayarı SignalR tarafından tutulan ölçekçıkış gönderme sırasının uzunluğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="db4d4-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="db4d4-237">0'dan büyük bir değere ayarlanması, tüm iletileri yapılandırılmış ileti arka düzlemine teker teker gönderilmek üzere gönderme kuyruğuna yerleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="db4d4-238">Sıranın boyutu yapılandırılan uzunluğun üzerine çıkarsa, sonraki gönderme çağrıları, kuyruktaki ileti sayısı yeniden ayardan daha az olana kadar Geçersiz [İşlem Özel Durum](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ile hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="db4d4-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="db4d4-239">Uygulanan arka uçakların genellikle kendi sıraya veya akış denetimi yerinde olduğundan, kuyruk lar varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="db4d4-240">SQL Server durumunda, bağlantı birleştirme, herhangi bir anda devam eden gönderme sayısını etkin bir şekilde sınırlar.</span><span class="sxs-lookup"><span data-stu-id="db4d4-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="db4d4-241">Varsayılan olarak, SQL Server ve Redis için yalnızca bir akış kullanılır, Hizmet Veri Servisi için beş akış kullanılır ve kuyruk devre dışı bırakılır, ancak bu ayarlar SQL Server ve Service Bus'taki yapılandırma yoluyla değiştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="db4d4-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="db4d4-242">**.NET Server Kodu SQL Server backplane için tablo sayısı ve kuyruk uzunluğu yapılandırmak için**</span><span class="sxs-lookup"><span data-stu-id="db4d4-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="db4d4-243">**.NET Sunucu Kodu Servis Veri Yolu backplane için konu sayısı ve kuyruk uzunluğu yapılandırmak için**</span><span class="sxs-lookup"><span data-stu-id="db4d4-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="db4d4-244">**Arabelleğe Alma** akışı, hatalı bir duruma girmiş olan dır; Akış hatalı durumda olduğunda, geri düzleme gönderilen tüm iletiler akış artık hata yapmayana kadar hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="db4d4-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="db4d4-245">**Sıra Gönder Uzunluğu,** deftere nakledilen ancak henüz gönderilmemiş ileti lerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="db4d4-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="db4d4-246">**Alınan İleti Veri Gönderi mesajlarını ölçeklendirme/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="db4d4-247">**Ölçeklendirme Akışları Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="db4d4-248">**Ölçeklendirme Akışları Aç**</span><span class="sxs-lookup"><span data-stu-id="db4d4-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="db4d4-249">**Ölçeklendirme Akışları Arabelleğe Alma**</span><span class="sxs-lookup"><span data-stu-id="db4d4-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="db4d4-250">**Ölçeklendirme Hataları Toplamı**</span><span class="sxs-lookup"><span data-stu-id="db4d4-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="db4d4-251">**Ölçeklendirme Hataları/Sn**</span><span class="sxs-lookup"><span data-stu-id="db4d4-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="db4d4-252">**Scaleout Sıra Uzunluğu Gönder**</span><span class="sxs-lookup"><span data-stu-id="db4d4-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="db4d4-253">Bu sayaçların neleri ölçtüğü hakkında daha fazla bilgi için Azure [Hizmet Veri Yolunda Sinyal Ölçer](scaleout-with-windows-azure-service-bus.md)'e bakın.</span><span class="sxs-lookup"><span data-stu-id="db4d4-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="db4d4-254">Diğer performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="db4d4-254">Using other performance counters</span></span>

<span data-ttu-id="db4d4-255">Aşağıdaki performans sayaçları, uygulamanızın performansını izlemede de yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="db4d4-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="db4d4-256">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="db4d4-256">**Memory**</span></span>

- <span data-ttu-id="db4d4-257">.NET CLR\\Bellek # tüm Yığınları bayt (w3wp için)</span><span class="sxs-lookup"><span data-stu-id="db4d4-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="db4d4-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="db4d4-258">**ASP.NET**</span></span>

- <span data-ttu-id="db4d4-259">ASP.NET\İstekleri Geçerli</span><span class="sxs-lookup"><span data-stu-id="db4d4-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="db4d4-260">ASP.NET\Sıraya</span><span class="sxs-lookup"><span data-stu-id="db4d4-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="db4d4-261">ASP.NET\Reddedildi</span><span class="sxs-lookup"><span data-stu-id="db4d4-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="db4d4-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="db4d4-262">**CPU**</span></span>

- <span data-ttu-id="db4d4-263">İşlemci Bilgileri\İşlemci Süresi</span><span class="sxs-lookup"><span data-stu-id="db4d4-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="db4d4-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="db4d4-264">**TCP/IP**</span></span>

- <span data-ttu-id="db4d4-265">TCPv6/Bağlantılar Kuruldu</span><span class="sxs-lookup"><span data-stu-id="db4d4-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="db4d4-266">TCPv4/Bağlantılar Kuruldu</span><span class="sxs-lookup"><span data-stu-id="db4d4-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="db4d4-267">**Web Hizmeti**</span><span class="sxs-lookup"><span data-stu-id="db4d4-267">**Web Service**</span></span>

- <span data-ttu-id="db4d4-268">Web Hizmeti\Geçerli Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="db4d4-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="db4d4-269">Web Hizmeti\Maksimum Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="db4d4-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="db4d4-270">**İş Parçacığı Oluşturma**</span><span class="sxs-lookup"><span data-stu-id="db4d4-270">**Threading**</span></span>

- <span data-ttu-id="db4d4-271">.NET CLR Kilitler\\Ve Konuları # geçerli mantıksal Konuları</span><span class="sxs-lookup"><span data-stu-id="db4d4-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="db4d4-272">.NET CLR Kilitler\\Ve Konuları # geçerli fiziksel Konuları</span><span class="sxs-lookup"><span data-stu-id="db4d4-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="db4d4-273">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="db4d4-273">Other Resources</span></span>

<span data-ttu-id="db4d4-274">ASP.NET performans izleme ve aetmehakkında daha fazla bilgi için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="db4d4-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="db4d4-275">[ASP.NET Performansa Genel Bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="db4d4-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="db4d4-276">IIS 7.5, IIS 7.0 ve IIS 6.0'da ASP.NET İş Parçacığı Kullanımı</span><span class="sxs-lookup"><span data-stu-id="db4d4-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="db4d4-277">&lt;applicationPool&gt; Element (Web Ayarları)</span><span class="sxs-lookup"><span data-stu-id="db4d4-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
