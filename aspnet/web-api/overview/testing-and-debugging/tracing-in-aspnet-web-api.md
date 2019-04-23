---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2'de izleme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API'de izlemenin nasıl etkinleştirileceği gösterilmektedir.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59405904"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="fdcbc-103">ASP.NET Web API 2'de izleme</span><span class="sxs-lookup"><span data-stu-id="fdcbc-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="fdcbc-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fdcbc-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="fdcbc-105">Web tabanlı bir uygulamanın hatalarını ayıklama çalışırken izleme günlüklerini iyi bir dizi için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="fdcbc-106">Bu öğreticide, ASP.NET Web API'de izlemenin nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="fdcbc-107">Bu özellik, Web API çerçevesi önce ve sonra denetleyiciyi çağıran yaptığı izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="fdcbc-108">Kendi kodunuzu izlemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fdcbc-109">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="fdcbc-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="fdcbc-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (Visual Studio 2015 ile de çalışır)</span><span class="sxs-lookup"><span data-stu-id="fdcbc-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="fdcbc-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="fdcbc-111">Web API 2</span></span>
> - [<span data-ttu-id="fdcbc-112">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="fdcbc-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="fdcbc-113">Web API'si izleme System.Diagnostics etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fdcbc-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="fdcbc-114">İlk olarak, yeni bir ASP.NET Web uygulaması projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="fdcbc-115">Visual Studio'da gelen **dosya** menüsünde **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="fdcbc-116">Altında **şablonları**, **Web**seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="fdcbc-117">Web API proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="fdcbc-118">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **paket yönetme Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="fdcbc-119">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="fdcbc-120">İlk komut, en son Web API'sini izleme paketini yükler.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="fdcbc-121">Ayrıca, core Web API'si paketleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="fdcbc-122">İkinci komut, en son sürüme WebApi.WebHost paketini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="fdcbc-123">Belirli bir Web API sürümünü hedeflemek istiyorsanız, kullanma izleme paketi yüklediğinizde sürüm bayrağı.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="fdcbc-124">Uygulamada WebApiConfig.cs dosya açma\_başlangıç klasörü.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="fdcbc-125">Aşağıdaki kodu ekleyin **kaydetme** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="fdcbc-126">Bu kod ekler [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) Web API ardışık düzeni için sınıf.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="fdcbc-127">**SystemDiagnosticsTraceWriter** sınıfı Yazar izlemelere [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span><span class="sxs-lookup"><span data-stu-id="fdcbc-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="fdcbc-128">İzlemelerini görmek için hata ayıklayıcıda uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="fdcbc-129">Tarayıcıda gidin `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="fdcbc-130">İzleme Deyimleri Visual Studio çıktı penceresinde yazılır.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="fdcbc-131">(Gelen **görünümü** menüsünde **çıkış**).</span><span class="sxs-lookup"><span data-stu-id="fdcbc-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="fdcbc-132">Çünkü **SystemDiagnosticsTraceWriter** izlemeleri için Yazar **System.Diagnostics.Trace**, ek izleme dinleyicileri kaydedebilirsiniz; Örneğin, yazma için izler bir günlük dosyasına.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="fdcbc-133">İzleme yazıcılar hakkında daha fazla bilgi için bkz. [izleme dinleyicilerine](https://msdn.microsoft.com/library/4y5y10s7.aspx) MSDN'de konu.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="fdcbc-134">SystemDiagnosticsTraceWriter yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fdcbc-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="fdcbc-135">Aşağıdaki kod, izleme yazıcısı yapılandırma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="fdcbc-136">Denetleyebileceğiniz iki ayarı vardır:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="fdcbc-137">IsVerbose: False ise, her izleme en düşük miktarda bilgiyi içerir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="fdcbc-138">TRUE ise izlemeleri daha fazla bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-138">If true, traces include more information.</span></span>
- <span data-ttu-id="fdcbc-139">MinimumLevel: Minimum izleme düzeyini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="fdcbc-140">İzleme düzeylerini, sırasıyla, hata ayıklama, bilgi, uyarı, hata ve önemli olan.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="fdcbc-141">Web API uygulamanızı izlemeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fdcbc-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="fdcbc-142">Bir izleme yazıcısı ekleme Web API ardışık düzeni tarafından oluşturulan izlemeleri anında erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="fdcbc-143">Kendi kodunuzu izlemek için izleme yazıcısı de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="fdcbc-144">İzleme yazıcısı almak için arama **HttpConfiguration.Services.GetTraceWriter**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="fdcbc-145">Bu yöntem bir denetleyiciden üzerinden erişilebilir **ApiController.Configuration** özelliği.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="fdcbc-146">Bir izleme yazmak için çağırabilirsiniz **ITraceWriter.Trace** yöntemi doğrudan, ancak [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) sınıfı daha kolay olan bazı genişletme yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="fdcbc-147">Örneğin, **bilgisi** yukarıda gösterilen yöntemi oluşturur bir izleme ile izleme düzeyini **bilgisi**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="fdcbc-148">Web API izleme altyapısı</span><span class="sxs-lookup"><span data-stu-id="fdcbc-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="fdcbc-149">Bu bölümde, bir Web API'si için özel izleme yazıcısı yazma açıklar.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="fdcbc-150">Web API'de daha genel bir izleme altyapısının en üstünde Microsoft.AspNet.WebApi.Tracing paket oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="fdcbc-151">Microsoft.AspNet.WebApi.Tracing kullanmak yerine, ayrıca bazı diğer izleme/günlüğünü Kitaplığı'nda, aşağıdaki gibi takabilirsiniz [NLog](http://nlog-project.org/) veya [log4net](http://logging.apache.org/log4net/).</span><span class="sxs-lookup"><span data-stu-id="fdcbc-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="fdcbc-152">İzlemeleri toplamak için uygulama **ITraceWriter** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="fdcbc-153">Basit bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="fdcbc-154">**ITraceWriter.Trace** yöntemi, bir izleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="fdcbc-155">Arayan bir kategori ve izleme düzeyini belirtir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="fdcbc-156">Kategori herhangi bir kullanıcı tanımlı dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-156">The category can be any user-defined string.</span></span> <span data-ttu-id="fdcbc-157">Uygulamanıza **izleme** aşağıdakileri yapmalıdır:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="fdcbc-158">Yeni bir **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="fdcbc-159">Bu istek, kategori ve izleme düzeyi ile gösterildiği gibi başlatın.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="fdcbc-160">Bu değerler, çağıran tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="fdcbc-161">Çağırma *traceAction* temsilci.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="fdcbc-162">Bu temsilci içinde çağırana geri kalanında doldurması beklenir **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="fdcbc-163">Yazma **TraceRecord**, istediğiniz herhangi bir günlük teknik kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="fdcbc-164">İçine burada gösterilen örnek yalnızca yapılan çağrılar **System.Diagnostics.Trace**.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="fdcbc-165">İzleme yazıcısı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fdcbc-165">Setting the Trace Writer</span></span>

<span data-ttu-id="fdcbc-166">İzlemeyi etkinleştirmek için Web API'ı kullanmak için yapılandırmanız gerekir, **ITraceWriter** uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="fdcbc-167">Bunu aracılığıyla **HttpConfiguration** nesne, aşağıdaki kodda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="fdcbc-168">Yalnızca bir izleme yazıcısı etkin olabilir.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-168">Only one trace writer can be active.</span></span> <span data-ttu-id="fdcbc-169">Varsayılan olarak, Web API kümelerini bir &quot;İşlemsiz&quot; hiçbir şey yapmaz İzleyici.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="fdcbc-170">( &quot;İşlemsiz&quot; İzleyici mevcut izleme yazıcısı olup olmadığını denetlemek izleme kodu yok böylece **null** izleme yazmadan önce.)</span><span class="sxs-lookup"><span data-stu-id="fdcbc-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="fdcbc-171">Nasıl çalıştığını izleme API Web</span><span class="sxs-lookup"><span data-stu-id="fdcbc-171">How Web API Tracing Works</span></span>

<span data-ttu-id="fdcbc-172">Web API izleme kullanan bir *cephe* Desen: İzleme etkin olduğunda, Web API'sini izleme çağrıları gerçekleştirmek sınıflarla istek ardışık düzenini çeşitli bölümlerini sarmalar.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="fdcbc-173">Örneğin, bir denetleyici seçerken, işlem hattı kullanır **IHttpControllerSelector** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="fdcbc-174">Etkin izleme ile işlem hattı uygulayan bir sınıf ekler **IHttpControllerSelector** ancak çağrıları üzerinden gerçek uygulama:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API izlemesi cephe deseni kullanır.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="fdcbc-176">Bu tasarım avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-176">The benefits of this design include:</span></span>

- <span data-ttu-id="fdcbc-177">İzleme yazıcısı eklemezseniz izleme bileşenleri değil örneği oluşturulur ve performansını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="fdcbc-178">Varsayılan hizmetler gibi değiştirirseniz **IHttpControllerSelector** izleme sarmalayıcısı nesne tarafından yapıldığı için kendi özel uygulamasıyla izleme etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="fdcbc-179">Varsayılan değiştirerek kendi özel framework ile tüm Web API izleme çerçevesini değiştirebilirsiniz **ITraceManager** hizmeti:</span><span class="sxs-lookup"><span data-stu-id="fdcbc-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="fdcbc-180">Uygulama **ITraceManager.Initialize** izleme sisteminizi başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="fdcbc-181">Bu değiştirir unutmayın *tüm* tüm Web API'sine yerleşik izleme kodu da dahil olmak üzere, izleme framework.</span><span class="sxs-lookup"><span data-stu-id="fdcbc-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
