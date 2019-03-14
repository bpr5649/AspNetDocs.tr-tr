---
uid: signalr/overview/older-versions/signalr-performance
title: SignalR performansı (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: SignalR Performansı
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 4158cb055088f3da752020e577007ffe80856b60
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075450"
---
<a name="signalr-performance-signalr-1x"></a><span data-ttu-id="c89e3-103">SignalR Performansı (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="c89e3-103">SignalR Performance (SignalR 1.x)</span></span>
====================
<span data-ttu-id="c89e3-104">tarafından [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="c89e3-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c89e3-105">Bu konuda, SignalR uygulama performansını artırmak için tasarlayın ve ölçmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="c89e3-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>


<span data-ttu-id="c89e3-106">SignalR performans ve ölçeklendirme hakkında son sunumu için bkz [ASP.NET SignalR ile gerçek zamanlı Web ölçeklendirme](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="c89e3-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="c89e3-107">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="c89e3-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="c89e3-108">Tasarım konuları</span><span class="sxs-lookup"><span data-stu-id="c89e3-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="c89e3-109">SignalR sunucunuz için performans ayarlama</span><span class="sxs-lookup"><span data-stu-id="c89e3-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="c89e3-110">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c89e3-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="c89e3-111">SignalR performans sayaçları kullanma</span><span class="sxs-lookup"><span data-stu-id="c89e3-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="c89e3-112">Diğer performans sayaçları kullanma</span><span class="sxs-lookup"><span data-stu-id="c89e3-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="c89e3-113">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c89e3-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="c89e3-114">Tasarım konuları</span><span class="sxs-lookup"><span data-stu-id="c89e3-114">Design considerations</span></span>

<span data-ttu-id="c89e3-115">Bu bölümde performans gereksiz ağ trafiğini oluşturarak engelliyordu değil emin olmak için bir SignalR uygulamasının Tasarım sırasında uygulanan desenler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="c89e3-116">İleti sıklığı azaltma</span><span class="sxs-lookup"><span data-stu-id="c89e3-116">Throttling message frequency</span></span>

<span data-ttu-id="c89e3-117">(Örneğin, gerçek zamanlı oyun uygulaması) bir yüksek sıklıkta ileti gönderen bile bir uygulamada, çoğu uygulama, ikinci bir fazla sayıda ileti göndermek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c89e3-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="c89e3-118">Her istemci ürettiği trafik miktarını azaltmak için bir ileti döngüsü kuyruklar ve göndereceğini sık en fazla sabit bir ücrete iletileri uygulanabilir (süre içerisinde iletileri ise diğer bir deyişle, belirli sayıda ileti kadar her saniye gönderilir gönderilecek oluşturma aralığı).</span><span class="sxs-lookup"><span data-stu-id="c89e3-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="c89e3-119">İletiler (hem istemci ve sunucu) için belirli bir fiyatı kısıtlar örnek bir uygulama için bkz. [SignalR ile yüksek sıklıkta gerçek zamanlı](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="c89e3-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="c89e3-120">İleti boyutu azaltma</span><span class="sxs-lookup"><span data-stu-id="c89e3-120">Reducing message size</span></span>

<span data-ttu-id="c89e3-121">SignalR ileti boyutu, serileştirilmiş nesneler boyutunu azaltarak azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="c89e3-122">Aktarılması gerekmez özellikleri içeren bir nesne gönderiyorsanız, sunucu kodunda bu özellikleri kullanarak serileştirilen öğesinden önlemek `JsonIgnore` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c89e3-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="c89e3-123">Özellik adlarını da iletide depolanır; Özellik adlarını kullanarak kısalttık `JsonProperty` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c89e3-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="c89e3-124">Aşağıdaki kod örneği, nasıl istemciye gönderilen bir özelliği dışarıda ve özellik adlarını kısaltmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="c89e3-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="c89e3-125">**İstemciye gönderilen veri dışlanacak JsonIgnore öznitelik ve ileti boyutunu küçültmek için Item özniteliğini gösterir .NET sunucu kodu**</span><span class="sxs-lookup"><span data-stu-id="c89e3-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="c89e3-126">Okunabilirliğini korumak için / bakım istemci kodu içinde kısaltılmış özellik adları olabilir İnsan dostu uri'lerini adları ileti alındıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="c89e3-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="c89e3-127">Aşağıdaki kod örneği bir ileti anlaşması (eşleme) tanımlayarak uzun olanlara, kısaltılmış adı yeniden eşleme, olası bir yol gösterir ve kullanarak `reMap` işlevi en iyi duruma getirilmiş ileti sınıfı için sözleşme uygulamak için:</span><span class="sxs-lookup"><span data-stu-id="c89e3-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="c89e3-128">**Özellik adlarının okunabilir adlarına yeniden eşleyen bir istemci tarafı JavaScript kodu kısalttık**</span><span class="sxs-lookup"><span data-stu-id="c89e3-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="c89e3-129">Adları iletilerinde istemci aynı zamanda sunucu için aynı yöntemi kullanarak kısaltılması.</span><span class="sxs-lookup"><span data-stu-id="c89e3-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="c89e3-130">(Diğer bir deyişle, ileti için kullanılan bellek miktarı) bellek kullanım alanını azaltmaya ileti nesne performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="c89e3-131">Örneğin, tam aralığının bir `int` gerekli değildir, bir `short` veya `byte` bunun yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="c89e3-132">İletileri ileti veri yolunda iletileri boyutunu azaltma, sunucu belleği depolandığından sunucu bellek sorunlarını gidermek de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89e3-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="c89e3-133">SignalR sunucunuz için performans ayarlama</span><span class="sxs-lookup"><span data-stu-id="c89e3-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="c89e3-134">Aşağıdaki yapılandırma ayarları, SignalR uygulamada daha iyi performans için sunucunuzu ayarlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="c89e3-135">Bir ASP.NET uygulamasında performansını artırma hakkında genel bilgi için bkz. [ASP.NET performans geliştirme](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="c89e3-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="c89e3-136">**SignalR yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="c89e3-137">**DefaultMessageBufferSize**: Varsayılan olarak, SignalR hub'ı bağlantı başına başına bellek 1000 iletilerinde korur.</span><span class="sxs-lookup"><span data-stu-id="c89e3-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="c89e3-138">Büyük iletileri kullanılıyorsa, bu, bu değer azaltarak alleviated bellek sorunlarını oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="c89e3-139">Bu ayar ayarlanabilir `Application_Start` olay işleyicisi bir ASP.NET uygulaması ya da `Configuration` yöntemi OWIN başlangıç sınıfı şirket içinde barındırılan bir uygulamada.</span><span class="sxs-lookup"><span data-stu-id="c89e3-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="c89e3-140">Aşağıdaki örnek, kullanılan sunucu bellek miktarını azaltmak için uygulamanızın bellek ayak izini azaltmak için bu değeri azaltmanız gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c89e3-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="c89e3-141">**Varsayılan ileti arabellek boyutunu azaltmak için .NET sunucu kodunda Global.asax**</span><span class="sxs-lookup"><span data-stu-id="c89e3-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="c89e3-142">**IIS yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="c89e3-143">**Uygulama başına en fazla eş zamanlı istek**: Eş zamanlı IIS sayısının artırılması, istekleri isteklerine hizmet için kullanılabilir sunucu kaynaklarına artacaktır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="c89e3-144">Varsayılan değer 5000'dir; Bu ayar artırmak için yükseltilmiş bir komut isteminde aşağıdaki komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="c89e3-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="c89e3-145">**ASP.NET yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="c89e3-146">Bu bölümü, ayarlanabilen yapılandırma ayarlarını içerir `aspnet.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="c89e3-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="c89e3-147">Bu dosya, platforma bağlı olarak iki konumlardan birinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="c89e3-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="c89e3-148">SignalR performansı iyileştirebilir ASP.NET ayarları aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="c89e3-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="c89e3-149">**CPU başına en fazla eş zamanlı istek**: Bu ayar artan performans sorunlarını giderebilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="c89e3-150">Bu ayar artırmak için aşağıdaki yapılandırma ayarı ekleme `aspnet.config` dosyası:</span><span class="sxs-lookup"><span data-stu-id="c89e3-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="c89e3-151">**Sıra sınırı iste**: Toplam bağlantı sayısını aştığında `maxConcurrentRequestsPerCPU` ayarlama, ASP.NET bir kuyruk kullanma istekleri azaltma başlar.</span><span class="sxs-lookup"><span data-stu-id="c89e3-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="c89e3-152">Sıranın boyutunu artırmak için artırabilirsiniz `requestQueueLimit` ayarı.</span><span class="sxs-lookup"><span data-stu-id="c89e3-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="c89e3-153">Bunu yapmak için aşağıdaki yapılandırma ayarı ekleme `processModel` düğümünde `config/machine.config` (yerine `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="c89e3-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="c89e3-154">Performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c89e3-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="c89e3-155">Bu bölümde, uygulamanızda performans sorunlarını bulmak için yolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="c89e3-156">WebSocket kullanılmakta olduğunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="c89e3-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="c89e3-157">SignalR istemci ve sunucu arasındaki iletişim için taşımalar çeşitli kullanabilirsiniz, ancak WebSocket önemli performans avantajı sunar ve istemci ve sunucu destekliyorsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="c89e3-158">İstemci ve sunucu WebSocket gereksinimlerini karşılayıp karşılamadığını belirlemek için bkz: [aktarım ve geri dönüşler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="c89e3-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="c89e3-159">Hangi aktarım uygulamanızda kullanıldığını belirlemek için tarayıcı geliştirici araçlarını kullanın ve aktarım bağlantı için kullanıldığını görmek için günlüklerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="c89e3-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="c89e3-160">Internet Explorer ve Chrome tarayıcı geliştirme araçları kullanma hakkında daha fazla bilgi için bkz. [aktarım ve geri dönüşler](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="c89e3-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="c89e3-161">SignalR performans sayaçları kullanma</span><span class="sxs-lookup"><span data-stu-id="c89e3-161">Using SignalR performance counters</span></span>

<span data-ttu-id="c89e3-162">Bu bölümde, etkinleştirmek ve kullanmak SignalR performans sayaçları açıklanmaktadır bulunan `Microsoft.AspNet.SignalR.Utils` paket.</span><span class="sxs-lookup"><span data-stu-id="c89e3-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="c89e3-163">Signalr.exe yükleme</span><span class="sxs-lookup"><span data-stu-id="c89e3-163">Installing signalr.exe</span></span>

<span data-ttu-id="c89e3-164">Performans sayaçları SignalR.exe adlı bir yardımcı program kullanarak sunucuya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-164">Peformance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="c89e3-165">Bu yardımcı programını yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c89e3-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="c89e3-166">Visual Studio'da **Araçları** > **NuGet Paket Yöneticisi** > **çözüm için NuGet paketlerini Yönet**</span><span class="sxs-lookup"><span data-stu-id="c89e3-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="c89e3-167">Arama **signalr.utils**ve yükleme seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c89e3-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="c89e3-168">Paketi yüklemek için lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c89e3-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="c89e3-169">SignalR.exe için yüklenecek `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="c89e3-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="c89e3-170">Performans sayaçları ile SignalR.exe yükleniyor</span><span class="sxs-lookup"><span data-stu-id="c89e3-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="c89e3-171">SignalR performans sayaçlarını yüklemek için yükseltilmiş bir komut istemi aşağıdaki parametresiyle SignalR.exe çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c89e3-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="c89e3-172">SignalR performans sayaçları kaldırmak için yükseltilmiş bir komut istemi aşağıdaki parametresiyle SignalR.exe çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c89e3-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="c89e3-173">SignalR performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="c89e3-173">SignalR Performance counters</span></span>

<span data-ttu-id="c89e3-174">Aşağıdaki performans sayaçları yardımcı programlar paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="c89e3-174">The utilites package installs the following performance counters.</span></span> <span data-ttu-id="c89e3-175">Son uygulama havuzunu veya sunucu yeniden başlatıldığından beri "Toplam" sayaçları, olay sayısını ölçer.</span><span class="sxs-lookup"><span data-stu-id="c89e3-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="c89e3-176">**Bağlantı ölçümü**</span><span class="sxs-lookup"><span data-stu-id="c89e3-176">**Connection metrics**</span></span>

<span data-ttu-id="c89e3-177">Aşağıdaki ölçümler gerçekleşen bağlantı ömrü olaylarını ölçün.</span><span class="sxs-lookup"><span data-stu-id="c89e3-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="c89e3-178">Daha fazla bilgi için [anlama ve işleme bağlantı ömrü olaylarını](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="c89e3-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="c89e3-179">**Bağlı bağlantıları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-179">**Connections Connected**</span></span>
- <span data-ttu-id="c89e3-180">**Bağlantıları yeniden bağlantı kuruldu**</span><span class="sxs-lookup"><span data-stu-id="c89e3-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="c89e3-181">**Bağlantıları Disonnected**</span><span class="sxs-lookup"><span data-stu-id="c89e3-181">**Connections Disonnected**</span></span>
- <span data-ttu-id="c89e3-182">**Bağlantılar-geçerli**</span><span class="sxs-lookup"><span data-stu-id="c89e3-182">**Connections Current**</span></span>

<span data-ttu-id="c89e3-183">**İleti ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-183">**Message metrics**</span></span>

<span data-ttu-id="c89e3-184">Aşağıdaki ölçümler SignalR tarafından oluşturulan ileti trafiği ölçer.</span><span class="sxs-lookup"><span data-stu-id="c89e3-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="c89e3-185">**Alınan toplam bağlantı iletisi**</span><span class="sxs-lookup"><span data-stu-id="c89e3-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="c89e3-186">**Toplam gönderilen bağlantısı iletileri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="c89e3-187">**Bağlantı alınan ileti sayısı/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="c89e3-188">**Bağlantı gönderilen ileti sayısı/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="c89e3-189">**Message bus ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-189">**Message bus metrics**</span></span>

<span data-ttu-id="c89e3-190">Aşağıdaki ölçümler, iç SignalR ileti veri, tüm gelen ve giden SignalR iletileri yerleştirilir kuyruk üzerinden geçen trafik ölçün.</span><span class="sxs-lookup"><span data-stu-id="c89e3-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="c89e3-191">Bir ileti **yayımlanan** zaman bunu gönderilir ya da yayın.</span><span class="sxs-lookup"><span data-stu-id="c89e3-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="c89e3-192">A **abone** bu bağlamda bir ileti veri yoluna abonelikte; bu istemciler ve sunucu sayısına eşit.</span><span class="sxs-lookup"><span data-stu-id="c89e3-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="c89e3-193">Bir **ayrılmış çalışan** veri gönderen etkin bağlantılar için; bir bileşeni bir **meşgul çalışan** , etkin bir ileti gönderen bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="c89e3-194">**Alınan toplam ileti veri yoluna iletileri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="c89e3-195">**İleti veri yoluna iletileri/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="c89e3-196">**Toplam ileti veri yoluna yayımlanan**</span><span class="sxs-lookup"><span data-stu-id="c89e3-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="c89e3-197">**İleti veri yoluna iletileri yayımlanan/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="c89e3-198">**İleti veri yoluna abone geçerli**</span><span class="sxs-lookup"><span data-stu-id="c89e3-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="c89e3-199">**İleti veri yoluna abone toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="c89e3-200">**İleti veri yoluna abone/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="c89e3-201">**İleti veri yoluna ayrılan çalışanları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="c89e3-202">**İleti veri yolu meşgul çalışanların**</span><span class="sxs-lookup"><span data-stu-id="c89e3-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="c89e3-203">**İleti veri yolu konuları geçerli**</span><span class="sxs-lookup"><span data-stu-id="c89e3-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="c89e3-204">**Hata ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-204">**Error metrics**</span></span>

<span data-ttu-id="c89e3-205">SignalR ileti trafiği tarafından oluşturulan hatalar aşağıdaki ölçümleri ölçün.</span><span class="sxs-lookup"><span data-stu-id="c89e3-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="c89e3-206">**Hub çözümleme** hataları bir hub veya hub'yöntemini çözümlenemiyor olduğunda oluşur.</span><span class="sxs-lookup"><span data-stu-id="c89e3-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="c89e3-207">**Hub çağırma** hataları olan bir hub yöntemi çağrılırken oluşan özel durum.</span><span class="sxs-lookup"><span data-stu-id="c89e3-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="c89e3-208">**Aktarım** bir HTTP isteği veya yanıtı sırasında oluşturulan bağlantı hataları hatalardır.</span><span class="sxs-lookup"><span data-stu-id="c89e3-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="c89e3-209">**Hataları: Tüm toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-209">**Errors: All Total**</span></span>
- <span data-ttu-id="c89e3-210">**Hataları: All/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="c89e3-211">**Hataları: Hub çözümleme toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="c89e3-212">**Hataları: Hub çözümleme/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="c89e3-213">**Hataları: Hub çağırma toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="c89e3-214">**Hataları: Hub çağırma/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="c89e3-215">**Hataları: Aktarım toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="c89e3-216">**Hataları: Aktarım/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="c89e3-217">**Genişletme ölçümleri**</span><span class="sxs-lookup"><span data-stu-id="c89e3-217">**Scaleout metrics**</span></span>

<span data-ttu-id="c89e3-218">Aşağıdaki ölçümler, trafik ve genişletme sağlayıcı tarafından oluşturulan hatalar ölçün.</span><span class="sxs-lookup"><span data-stu-id="c89e3-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="c89e3-219">A **Stream** bu bağlamda bir ölçek birimi genişletme sağlayıcı tarafından kullanılan; SQL Server kullandıysanız bir tablo, Service Bus kullanılırsa, bir konu ve abonelik Redis kullandıysanız budur.</span><span class="sxs-lookup"><span data-stu-id="c89e3-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="c89e3-220">Varsayılan olarak, yalnızca bir akış kullanılır, ancak bu yapılandırma, SQL Server ve Service Bus aracılığıyla artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="c89e3-221">A **arabelleği** stream, hatalı bir duruma geçtiğini; akış hatalı bir durumda olduğunda hemen akış artık hatalı kadar devre kartına gönderilen tüm iletilerin başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c89e3-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="c89e3-222">**Gönderme sırası uzunluğu** gönderilen, ancak henüz gönderilen iletilerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="c89e3-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="c89e3-223">**Genişletme ileti veri yoluna iletileri/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="c89e3-224">**Genişletme akışları toplam**</span><span class="sxs-lookup"><span data-stu-id="c89e3-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="c89e3-225">**Genişletme açık akışları**</span><span class="sxs-lookup"><span data-stu-id="c89e3-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="c89e3-226">**Genişletme akışları arabelleğe alma**</span><span class="sxs-lookup"><span data-stu-id="c89e3-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="c89e3-227">**Genişletme hataları toplamı**</span><span class="sxs-lookup"><span data-stu-id="c89e3-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="c89e3-228">**Genişletme Hatası/sn**</span><span class="sxs-lookup"><span data-stu-id="c89e3-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="c89e3-229">**Genişletme gönderme sırası uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="c89e3-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="c89e3-230">Ne Bu sayaçlar ölçme ile ilgili daha fazla bilgi için bkz: [Azure Service Bus ile SignalR ölçeğini genişletme](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="c89e3-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="c89e3-231">Diğer performans sayaçları kullanma</span><span class="sxs-lookup"><span data-stu-id="c89e3-231">Using other performance counters</span></span>

<span data-ttu-id="c89e3-232">Aşağıdaki performans sayaçları, uygulamanızın performansını izlemek için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e3-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="c89e3-233">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="c89e3-233">**Memory**</span></span>

- <span data-ttu-id="c89e3-234">.NET CLR bellek # bayt cinsinden tüm yığınlardaki (w3wp)</span><span class="sxs-lookup"><span data-stu-id="c89e3-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="c89e3-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="c89e3-235">**ASP.NET**</span></span>

- <span data-ttu-id="c89e3-236">ASP.NET\Requests geçerli</span><span class="sxs-lookup"><span data-stu-id="c89e3-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="c89e3-237">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="c89e3-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="c89e3-238">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="c89e3-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="c89e3-239">**CPU**</span><span class="sxs-lookup"><span data-stu-id="c89e3-239">**CPU**</span></span>

- <span data-ttu-id="c89e3-240">İşlemci Information\Processor zamanı</span><span class="sxs-lookup"><span data-stu-id="c89e3-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="c89e3-241">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="c89e3-241">**TCP/IP**</span></span>

- <span data-ttu-id="c89e3-242">TCPv6/kurulan bağlantılar</span><span class="sxs-lookup"><span data-stu-id="c89e3-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="c89e3-243">TCPv4/kurulan bağlantılar</span><span class="sxs-lookup"><span data-stu-id="c89e3-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="c89e3-244">**Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="c89e3-244">**Web Service**</span></span>

- <span data-ttu-id="c89e3-245">Web Service\Current bağlantıları</span><span class="sxs-lookup"><span data-stu-id="c89e3-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="c89e3-246">Web Service\Maximum bağlantıları</span><span class="sxs-lookup"><span data-stu-id="c89e3-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="c89e3-247">**İş parçacığı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="c89e3-247">**Threading**</span></span>

- <span data-ttu-id="c89e3-248">.NET CLR LocksAndThreads\# geçerli mantıksal iş parçacığı sayısı</span><span class="sxs-lookup"><span data-stu-id="c89e3-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="c89e3-249">.NET CLR LocksAnd iş parçacıkları\# geçerli fiziksel iş parçacığı sayısı</span><span class="sxs-lookup"><span data-stu-id="c89e3-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="c89e3-250">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c89e3-250">Other Resources</span></span>

<span data-ttu-id="c89e3-251">ASP.NET Performans izleme ve ayarlama hakkında daha fazla bilgi için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="c89e3-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="c89e3-252">[ASP.NET performansa genel bakış](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="c89e3-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="c89e3-253">IIS 6.0 IIS 7.5 ve IIS 7.0 üzerinde ASP.NET iş parçacığı kullanımı</span><span class="sxs-lookup"><span data-stu-id="c89e3-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="c89e3-254">&lt;applicationPool&gt; öğesi (Web Ayarları)</span><span class="sxs-lookup"><span data-stu-id="c89e3-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
