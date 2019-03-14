---
title: ASP.NET Core Modülü
author: guardrex
description: ASP.NET Core uygulamaları barındırmak için gereken ASP.NET Core modülü yapılandırmayı öğrenin.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 302cfb00127c223aeb5e51e4d0a9ef3cb69b10eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067581"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="f31d8-103">ASP.NET Core Modülü</span><span class="sxs-lookup"><span data-stu-id="f31d8-103">ASP.NET Core Module</span></span>

<span data-ttu-id="f31d8-104">Tarafından [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [ Justin Kotalik](https://github.com/jkotalik), ve [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="f31d8-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [Justin Kotalik](https://github.com/jkotalik), and [Luke Latham](https://github.com/guardrex)</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-105">ASP.NET Core modülü ya da IIS kanala takılan yerel bir IIS modülüdür:</span><span class="sxs-lookup"><span data-stu-id="f31d8-105">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to either:</span></span>

* <span data-ttu-id="f31d8-106">IIS çalışan işlemi içinde ASP.NET Core uygulaması ana bilgisayar (`w3wp.exe`) adlı [işlem içi barındırma modeli](#in-process-hosting-model).</span><span class="sxs-lookup"><span data-stu-id="f31d8-106">Host an ASP.NET Core app inside of the IIS worker process (`w3wp.exe`), called the [in-process hosting model](#in-process-hosting-model).</span></span>
* <span data-ttu-id="f31d8-107">Arka uç, çalışan bir ASP.NET Core uygulaması için web istekleri iletmek [Kestrel sunucu](xref:fundamentals/servers/kestrel)adlı [işlem dışı barındırma modeli](#out-of-process-hosting-model).</span><span class="sxs-lookup"><span data-stu-id="f31d8-107">Forward web requests to a backend ASP.NET Core app running the [Kestrel server](xref:fundamentals/servers/kestrel), called the [out-of-process hosting model](#out-of-process-hosting-model).</span></span>

<span data-ttu-id="f31d8-108">Desteklenen Windows sürümleri:</span><span class="sxs-lookup"><span data-stu-id="f31d8-108">Supported Windows versions:</span></span>

* <span data-ttu-id="f31d8-109">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="f31d8-109">Windows 7 or later</span></span>
* <span data-ttu-id="f31d8-110">Windows Server 2008 R2 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="f31d8-110">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="f31d8-111">İşlem içi barındırırken modülü bir işlem sunucusu uygulama IIS HTTP sunucusu olarak adlandırılır, IIS için kullanır. (`IISHttpServer`).</span><span class="sxs-lookup"><span data-stu-id="f31d8-111">When hosting in-process, the module uses an in-process server implementation for IIS, called IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="f31d8-112">İşlem dışı barındırırken, modülü yalnızca Kestrel ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-112">When hosting out-of-process, the module only works with Kestrel.</span></span> <span data-ttu-id="f31d8-113">Uyumlu bir modüldür [HTTP.sys](xref:fundamentals/servers/httpsys).</span><span class="sxs-lookup"><span data-stu-id="f31d8-113">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

## <a name="hosting-models"></a><span data-ttu-id="f31d8-114">Barındırma modelleri</span><span class="sxs-lookup"><span data-stu-id="f31d8-114">Hosting models</span></span>

### <a name="in-process-hosting-model"></a><span data-ttu-id="f31d8-115">İşlem içi barındırma modeli</span><span class="sxs-lookup"><span data-stu-id="f31d8-115">In-process hosting model</span></span>

<span data-ttu-id="f31d8-116">İşlem içi barındırmak için bir uygulamayı yapılandırmak için Ekle `<AspNetCoreHostingModel>` özellik değerini içeren uygulamanın proje dosyasına `InProcess` (işlem dışı barındırma ile ayarlanır `OutOfProcess`):</span><span class="sxs-lookup"><span data-stu-id="f31d8-116">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file with a value of `InProcess` (out-of-process hosting is set with `OutOfProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>InProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="f31d8-117">İşlem içi barındırma modeli, .NET Framework'ü hedefleyen ASP.NET Core uygulamaları için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-117">The in-process hosting model isn't supported for ASP.NET Core apps that target the .NET Framework.</span></span>

<span data-ttu-id="f31d8-118">Varsa `<AspNetCoreHostingModel>` özelliği dosyasında mevcut değilse, varsayılan değer `OutOfProcess`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-118">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>

<span data-ttu-id="f31d8-119">Aşağıdaki özellikler, işlem içi barındırırken geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="f31d8-119">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="f31d8-120">IIS HTTP sunucusu (`IISHttpServer`) yerine kullanılan [Kestrel](xref:fundamentals/servers/kestrel) sunucusu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-120">IIS HTTP Server (`IISHttpServer`) is used instead of [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span> <span data-ttu-id="f31d8-121">İşlem içinde için [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) çağrıları <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIIS*> için:</span><span class="sxs-lookup"><span data-stu-id="f31d8-121">For in-process, [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) calls <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIIS*> to:</span></span>

  * <span data-ttu-id="f31d8-122">Kayıt `IISHttpServer`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-122">Register the `IISHttpServer`.</span></span>
  * <span data-ttu-id="f31d8-123">Sunucu, ASP.NET Core modülü çalıştırırken dinleyecek temel yolu ve bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-123">Configure the port and base path the server should listen on when running behind the ASP.NET Core Module.</span></span>
  * <span data-ttu-id="f31d8-124">Başlatma hataları yakalamak için ana yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-124">Configure the host to capture startup errors.</span></span>

* <span data-ttu-id="f31d8-125">[RequestTimeout özniteliği](#attributes-of-the-aspnetcore-element) işlem içi barındırmak için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-125">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="f31d8-126">Uygulamalar arasında bir uygulama havuzu paylaşımı desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f31d8-126">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="f31d8-127">Uygulama başına bir uygulama havuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-127">Use one app pool per app.</span></span>

* <span data-ttu-id="f31d8-128">Kullanırken [Web dağıtımı](/iis/publish/using-web-deploy/introduction-to-web-deploy) veya el ile yerleştirme bir [app_offline.htm dosyasını dağıtımdaki](xref:host-and-deploy/iis/index#locked-deployment-files), açık bir bağlantı varsa uygulamayı hemen kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="f31d8-128">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="f31d8-129">Örneğin, bir websocket bağlantısı uygulama kapatma gecikmeye neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-129">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="f31d8-130">Yüklü çalışma zamanı (x64 veya x86) ve uygulama mimarisi (bit) uygulama havuzu mimarisiyle gerekir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-130">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="f31d8-131">El ile uygulamanın ana bilgisayar ayarlıyorsanız `WebHostBuilder` (kullanmayan [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) ve uygulama çağrı hiç olmadığı kadar (şirket içinde barındırılan) doğrudan Kestrel sunucuda çalıştırıldığında `UseKestrel` çağırmadan önce `UseIISIntegration`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-131">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="f31d8-132">Sıra ters çevrilir ana bilgisayarı başlatmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-132">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="f31d8-133">İstemci bağlantısını keser algılanır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-133">Client disconnects are detected.</span></span> <span data-ttu-id="f31d8-134">[HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) istemci kestiğinde iptal belirteci iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="f31d8-134">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="f31d8-135">ASP.NET core'da 2.2.1 veya daha önce <xref:System.IO.Directory.GetCurrentDirectory*> uygulamanın dizinine yerine IIS tarafından başlatılan işlem alt dizinini döndürür (örneğin, *C:\Windows\System32\inetsrv* için *w3wp.exe*) .</span><span class="sxs-lookup"><span data-stu-id="f31d8-135">In ASP.NET Core 2.2.1 or earlier, <xref:System.IO.Directory.GetCurrentDirectory*> returns the worker directory of the process started by IIS rather than the app's directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

  <span data-ttu-id="f31d8-136">Uygulamanın geçerli dizin ayarlar örnek kod için bkz: [CurrentDirectoryHelpers sınıfı](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs).</span><span class="sxs-lookup"><span data-stu-id="f31d8-136">For sample code that sets the app's current directory, see the [CurrentDirectoryHelpers class](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs).</span></span> <span data-ttu-id="f31d8-137">Çağrı `SetCurrentDirectory` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f31d8-137">Call the `SetCurrentDirectory` method.</span></span> <span data-ttu-id="f31d8-138">Yapılan sonraki çağrılar <xref:System.IO.Directory.GetCurrentDirectory*> uygulamanın dizinine sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-138">Subsequent calls to <xref:System.IO.Directory.GetCurrentDirectory*> provide the app's directory.</span></span>
  
* <span data-ttu-id="f31d8-139">İşlem içinde barındırırken <xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*> dahili olarak bir kullanıcı başlatmak için çağırılır değil.</span><span class="sxs-lookup"><span data-stu-id="f31d8-139">When hosting in-process, <xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*> isn't called internally to initialize a user.</span></span> <span data-ttu-id="f31d8-140">Bu nedenle, bir <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> her kimlik doğrulaması varsayılan olarak etkinleştirilmez sonra talepleri dönüştürmek için kullanılan uygulama.</span><span class="sxs-lookup"><span data-stu-id="f31d8-140">Therefore, an <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> implementation used to transform claims after every authentication isn't activated by default.</span></span> <span data-ttu-id="f31d8-141">Talepleri ile dönüştürülürken bir <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> uygulaması, çağrı <xref:Microsoft.Extensions.DependencyInjection.AuthenticationServiceCollectionExtensions.AddAuthentication*> kimlik doğrulama hizmetlerini eklemek için:</span><span class="sxs-lookup"><span data-stu-id="f31d8-141">When transforming claims with an <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> implementation, call <xref:Microsoft.Extensions.DependencyInjection.AuthenticationServiceCollectionExtensions.AddAuthentication*> to add authentication services:</span></span>

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddTransient<IClaimsTransformation, ClaimsTransformer>();
      services.AddAuthentication(IISServerDefaults.AuthenticationScheme);
  }
  
  public void Configure(IApplicationBuilder app)
  {
      app.UseAuthentication();
  }
  ```

### <a name="out-of-process-hosting-model"></a><span data-ttu-id="f31d8-142">İşlem dışı barındırma modeli</span><span class="sxs-lookup"><span data-stu-id="f31d8-142">Out-of-process hosting model</span></span>

<span data-ttu-id="f31d8-143">İşlem dışı barındırmak için bir uygulamayı yapılandırmak için proje dosyasında aşağıdaki yaklaşımlardan birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="f31d8-143">To configure an app for out-of-process hosting, use either of the following approaches in the project file:</span></span>

* <span data-ttu-id="f31d8-144">Belirtmeyin `<AspNetCoreHostingModel>` özelliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-144">Don't specify the `<AspNetCoreHostingModel>` property.</span></span> <span data-ttu-id="f31d8-145">Varsa `<AspNetCoreHostingModel>` özelliği dosyasında mevcut değilse, varsayılan değer `OutOfProcess`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-145">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>
* <span data-ttu-id="f31d8-146">Değerini `<AspNetCoreHostingModel>` özelliğini `OutOfProcess` (işlem içi barındırma ile ayarlanır `InProcess`):</span><span class="sxs-lookup"><span data-stu-id="f31d8-146">Set the value of the `<AspNetCoreHostingModel>` property to `OutOfProcess` (in-process hosting is set with `InProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>OutOfProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="f31d8-147">[Kestrel'i](xref:fundamentals/servers/kestrel) sunucusu yerine IIS HTTP sunucusu kullanılır (`IISHttpServer`).</span><span class="sxs-lookup"><span data-stu-id="f31d8-147">[Kestrel](xref:fundamentals/servers/kestrel) server is used instead of IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="f31d8-148">Çıkış işlemini için [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) çağrıları <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> için:</span><span class="sxs-lookup"><span data-stu-id="f31d8-148">For out-of-process, [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) calls <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> to:</span></span>

* <span data-ttu-id="f31d8-149">Sunucu, ASP.NET Core modülü çalıştırırken dinleyecek temel yolu ve bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-149">Configure the port and base path the server should listen on when running behind the ASP.NET Core Module.</span></span>
* <span data-ttu-id="f31d8-150">Başlatma hataları yakalamak için ana yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-150">Configure the host to capture startup errors.</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="f31d8-151">Barındırma modeli değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="f31d8-151">Hosting model changes</span></span>

<span data-ttu-id="f31d8-152">Varsa `hostingModel` ayar değiştirildiğinde *web.config* dosya (açıklandığı [web.config yapılandırmasıyla](#configuration-with-webconfig) bölümü), modülü için IIS çalışan işlemi geri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-152">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="f31d8-153">Modülü, IIS Express için çalışan işlemi geri dönüşüm değil ancak bunun yerine geçerli IIS Express işlemi normal şekilde kapatılmasını tetikler.</span><span class="sxs-lookup"><span data-stu-id="f31d8-153">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="f31d8-154">Uygulamanın sonraki isteği, IIS Express'in yeni bir işlem olarak çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-154">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="f31d8-155">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="f31d8-155">Process name</span></span>

<span data-ttu-id="f31d8-156">`Process.GetCurrentProcess().ProcessName` raporları `w3wp` / `iisexpress` (işlem içi) veya `dotnet` (giden işlem).</span><span class="sxs-lookup"><span data-stu-id="f31d8-156">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f31d8-157">ASP.NET Core modülü, uygulama arka ucu ASP.NET Core web isteklerini iletmek için IIS ardışık düzende takılan yerel bir IIS modülüdür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-157">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to forward web requests to backend ASP.NET Core apps.</span></span>

<span data-ttu-id="f31d8-158">Desteklenen Windows sürümleri:</span><span class="sxs-lookup"><span data-stu-id="f31d8-158">Supported Windows versions:</span></span>

* <span data-ttu-id="f31d8-159">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="f31d8-159">Windows 7 or later</span></span>
* <span data-ttu-id="f31d8-160">Windows Server 2008 R2 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="f31d8-160">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="f31d8-161">Modül yalnızca Kestrel ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-161">The module only works with Kestrel.</span></span> <span data-ttu-id="f31d8-162">Uyumlu bir modüldür [HTTP.sys](xref:fundamentals/servers/httpsys).</span><span class="sxs-lookup"><span data-stu-id="f31d8-162">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

<span data-ttu-id="f31d8-163">Bir işlem içinde çalıştırmak, ASP.NET Core uygulamaları IIS çalışan işleminden ayrı olduğundan, modül işlem yönetimi da işler.</span><span class="sxs-lookup"><span data-stu-id="f31d8-163">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="f31d8-164">İlk istek ulaştığında ve onu bir çökme gerçekleşirse, uygulama yeniden başlatmalarını modülü ASP.NET Core uygulaması için bir işlem başlar.</span><span class="sxs-lookup"><span data-stu-id="f31d8-164">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="f31d8-165">Bu aslında aynı işlemde çalışan ASP.NET 4.x uygulamalar ile görüldüğü gibi davranıştır tarafından yönetildiği IIS'de [Windows İşlem Etkinleştirme Hizmeti (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span><span class="sxs-lookup"><span data-stu-id="f31d8-165">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="f31d8-166">Aşağıdaki diyagramda, IIS, ASP.NET Core modülü ve uygulama arasındaki ilişki gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f31d8-166">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app:</span></span>

![ASP.NET Core Modülü](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="f31d8-168">İstekleri için çekirdek modu HTTP.sys sürücüsünü Web'den ulaşır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-168">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="f31d8-169">Sürücü istekler IIS Web sitesinin yapılandırılan bağlantı noktası, genellikle 80 (HTTP) veya 443 (HTTPS) üzerinde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-169">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="f31d8-170">Modül Kestrel rastgele bağlantı noktası için 80 veya 443 bağlantı noktası olmadığından uygulama isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-170">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80 or 443.</span></span>

<span data-ttu-id="f31d8-171">Modülü başlatma sırasında bir ortam değişkeni aracılığıyla bağlantı noktasını belirtir ve IIS tümleştirme ara yazılımı üzerinde dinlemek üzere yapılandırır `http://localhost:{port}`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-171">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="f31d8-172">Ek denetimler gerçekleştirilir ve modülünden değilsiniz kaynaklı istekler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-172">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="f31d8-173">İstekler HTTP üzerinden HTTPS üzerinden IIS tarafından alınan bile iletilir modülü HTTPS iletmeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-173">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="f31d8-174">Modül istekten Kestrel seçer sonra ASP.NET Core ara yazılım ardışık düzende isteği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-174">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="f31d8-175">Ara yazılım ardışık düzenini isteği işler ve olarak geçirir bir `HttpContext` örneği uygulama mantığına.</span><span class="sxs-lookup"><span data-stu-id="f31d8-175">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="f31d8-176">IIS tümleştirme tarafından eklenen bir ara yazılım istek için Kestrel iletmek için hesap için şema, uzak IP ve pathbase güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-176">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="f31d8-177">Uygulamanın yanıt IIS, yeniden istek başlatılan HTTP istemcisi için hangi bildirim geçirilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-177">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

<span data-ttu-id="f31d8-178">Windows kimlik doğrulaması gibi birçok yerel modül etkin kalır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-178">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="f31d8-179">ASP.NET Core modülü içeren etkin IIS modülleri hakkında daha fazla bilgi için bkz: <xref:host-and-deploy/iis/modules>.</span><span class="sxs-lookup"><span data-stu-id="f31d8-179">To learn more about IIS modules active with the ASP.NET Core Module, see <xref:host-and-deploy/iis/modules>.</span></span>

<span data-ttu-id="f31d8-180">ASP.NET Core modülü de yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f31d8-180">The ASP.NET Core Module can also:</span></span>

* <span data-ttu-id="f31d8-181">Çalışan işlemi için ortam değişkenlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-181">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="f31d8-182">Çıkış başlatma sorunlarını gidermek için dosya depolama için stdout'u günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f31d8-182">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="f31d8-183">Windows kimlik doğrulama belirteçlerinizi iletin.</span><span class="sxs-lookup"><span data-stu-id="f31d8-183">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="f31d8-184">Yükleme ve ASP.NET Core modülü kullanın</span><span class="sxs-lookup"><span data-stu-id="f31d8-184">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="f31d8-185">Yükleme ve ASP.NET Core modülü kullanma hakkında yönergeler için bkz. <xref:host-and-deploy/iis/index>.</span><span class="sxs-lookup"><span data-stu-id="f31d8-185">For instructions on how to install and use the ASP.NET Core Module, see <xref:host-and-deploy/iis/index>.</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="f31d8-186">Web.config ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f31d8-186">Configuration with web.config</span></span>

<span data-ttu-id="f31d8-187">ASP.NET Core modülü ile yapılandırılmış `aspNetCore` bölümünü `system.webServer` sitenin düğümünde *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="f31d8-187">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="f31d8-188">Aşağıdaki *web.config* dosya için yayınlanmış bir [framework bağımlı dağıtım](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) ve site isteklerini işlemek için gereken ASP.NET Core modülü yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="f31d8-188">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" 
                  arguments=".\MyApp.dll" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" 
                arguments=".\MyApp.dll" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="f31d8-189">Aşağıdaki *web.config* için yayımlanan bir [müstakil dağıtım](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span><span class="sxs-lookup"><span data-stu-id="f31d8-189">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

<span data-ttu-id="f31d8-190"><xref:System.Configuration.SectionInformation.InheritInChildApplications*> Özelliği `false` ayarları içinde belirtilen belirtmek için [ \<konum >](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) öğesi olmayan uygulamanın bir alt dizinde bulunan uygulamalar tarafından devralınan.</span><span class="sxs-lookup"><span data-stu-id="f31d8-190">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the app.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="f31d8-191">Ne zaman bir uygulamanın dağıtıldığı [Azure App Service](https://azure.microsoft.com/services/app-service/), `stdoutLogFile` yolunu ayarlamak `\\?\%home%\LogFiles\stdout`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-191">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="f31d8-192">Yol stdout günlüklerine kaydeder *LogFiles* klasörü, bir konumdur otomatik olarak oluşturulan hizmet tarafından.</span><span class="sxs-lookup"><span data-stu-id="f31d8-192">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="f31d8-193">IIS alt uygulama yapılandırma hakkında daha fazla bilgi için bkz: <xref:host-and-deploy/iis/index#sub-applications>.</span><span class="sxs-lookup"><span data-stu-id="f31d8-193">For information on IIS sub-application configuration, see <xref:host-and-deploy/iis/index#sub-applications>.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="f31d8-194">AspNetCore öğenin öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="f31d8-194">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="f31d8-195">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f31d8-195">Attribute</span></span> | <span data-ttu-id="f31d8-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f31d8-196">Description</span></span> | <span data-ttu-id="f31d8-197">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="f31d8-197">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f31d8-198">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-198">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-199">Belirtilen yürütülebilir dosya için bağımsız değişkenler **processPath**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-199">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f31d8-200">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-200">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-201">TRUE ise **502.5 - işlem hatası** sayfa geçersiz kılınır ve 502 durumu kod sayfası yapılandırılan *web.config* önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-201">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f31d8-202">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-202">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-203">TRUE ise, istek başına 'MS-ASPNETCORE-WINAUTHTOKEN' üst bilgi olarak ASPNETCORE_PORT % üzerinde dinleme alt işlem belirteci iletilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-203">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f31d8-204">İstek başına Bu belirteci CloseHandle çağırmak için işlemin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-204">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="f31d8-205">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-205">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-206">Barındırma modeli işlemdeki belirtir (`InProcess`) veya işlem dışı (`OutOfProcess`).</span><span class="sxs-lookup"><span data-stu-id="f31d8-206">Specifies the hosting model as in-process (`InProcess`) or out-of-process (`OutOfProcess`).</span></span></p> | `OutOfProcess` |
| `processesPerApplication` | <p><span data-ttu-id="f31d8-207">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-207">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-208">Belirtilen işlem örneklerinin sayısını belirtir **processPath** ayarı hazırladık yedekleme uygulama.</span><span class="sxs-lookup"><span data-stu-id="f31d8-208">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="f31d8-209">&dagger;İşlem içi barındırmak için değer sınırlı olan `1`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-209">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p><p><span data-ttu-id="f31d8-210">Ayar `processesPerApplication` önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-210">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="f31d8-211">Bu öznitelik, gelecekteki bir sürümde kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="f31d8-211">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="f31d8-212">Varsayılan: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-212">Default: `1`</span></span><br><span data-ttu-id="f31d8-213">En küçük: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-213">Min: `1`</span></span><br><span data-ttu-id="f31d8-214">En fazla: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="f31d8-214">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="f31d8-215">Gerekli dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-215">Required string attribute.</span></span></p><p><span data-ttu-id="f31d8-216">HTTP istekleri için dinleme işlemini başlatan yürütülebilir dosya yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-216">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f31d8-217">Göreli yollar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-217">Relative paths are supported.</span></span> <span data-ttu-id="f31d8-218">Yol ile başlıyorsa `.`, yolun site köküne göreli olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-218">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f31d8-219">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-219">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-220">Belirtilen işlem sayısını belirtir **processPath** dakika başına kilitlenme izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-220">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f31d8-221">Bu sınır aşılırsa, dakikanın geri kalanı için işlem başlatılırken modülü durdurur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-221">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="f31d8-222">İşlem içi barındırma ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-222">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="f31d8-223">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-223">Default: `10`</span></span><br><span data-ttu-id="f31d8-224">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-224">Min: `0`</span></span><br><span data-ttu-id="f31d8-225">En fazla: `100`</span><span class="sxs-lookup"><span data-stu-id="f31d8-225">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f31d8-226">İsteğe bağlı timespan özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-226">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f31d8-227">ASP.NET Core modülü ASPNETCORE_PORT % üzerinde dinleme işleminden yanıt almayı bekleyeceği süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-227">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f31d8-228">ASP.NET Core 2.1 veya daha sonra sürüm ile birlikte gelen ASP.NET Core modülü sürümlerinde `requestTimeout` saat, dakika ve saniye olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-228">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="f31d8-229">İşlem içi barındırmak için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-229">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="f31d8-230">İşlem içi barındırmak için modülü isteği işlemek için uygulamada bekler.</span><span class="sxs-lookup"><span data-stu-id="f31d8-230">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="f31d8-231">Varsayılan: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-231">Default: `00:02:00`</span></span><br><span data-ttu-id="f31d8-232">En küçük: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-232">Min: `00:00:00`</span></span><br><span data-ttu-id="f31d8-233">En fazla: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-233">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f31d8-234">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-234">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-235">Modül düzgün biçimde kapatma çalıştırılabiliri için bekleyeceği saniye cinsinden zaman *app_offline.htm* dosyası algılandı.</span><span class="sxs-lookup"><span data-stu-id="f31d8-235">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f31d8-236">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-236">Default: `10`</span></span><br><span data-ttu-id="f31d8-237">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-237">Min: `0`</span></span><br><span data-ttu-id="f31d8-238">En fazla: `600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-238">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f31d8-239">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-239">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-240">Modül için yürütülebilir dosya bağlantı noktası üzerinde dinleme işlemini başlatmasını bekleyeceği saniye cinsinden süre.</span><span class="sxs-lookup"><span data-stu-id="f31d8-240">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f31d8-241">Bu süre aşılırsa, modül işlemi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-241">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f31d8-242">Yeni bir istek alırsa ve uygulamayı başlatmak tarayamaz hale gelen sonraki istekleri işlemi yeniden denemek devam ediyor, işlemi yeniden başlatın dener modülün **rapidFailsPerMinute** son kez sayısı sıralı dakika.</span><span class="sxs-lookup"><span data-stu-id="f31d8-242">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="f31d8-243">0 (sıfır) değeri **değil** sonsuz zaman aşımını kabul.</span><span class="sxs-lookup"><span data-stu-id="f31d8-243">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="f31d8-244">Varsayılan: `120`</span><span class="sxs-lookup"><span data-stu-id="f31d8-244">Default: `120`</span></span><br><span data-ttu-id="f31d8-245">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-245">Min: `0`</span></span><br><span data-ttu-id="f31d8-246">En fazla: `3600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-246">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f31d8-247">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-247">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-248">TRUE ise **stdout** ve **stderr** belirtilen işlem için **processPath** belirtilen dosyaya yeniden yönlendirilen **stdoutLogFile**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-248">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f31d8-249">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-249">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-250">Kendisi için göreli veya mutlak dosya yolunu belirtir **stdout** ve **stderr** belirtilen işlemden **processPath** kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-250">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f31d8-251">Site köküne göreli yollardır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-251">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f31d8-252">İle başlayan herhangi bir yola `.` olan göreli site kök ve diğer tüm yolları mutlak yollar olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-252">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f31d8-253">Günlük dosyası oluşturulduğunda yolunda sağlanan herhangi bir klasörde modülü tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-253">Any folders provided in the path are created by the module when the log file is created.</span></span> <span data-ttu-id="f31d8-254">Alt çizgi sınırlayıcıları, bir zaman damgası, işlem kimliği ve dosya uzantısı kullanarak (*.log*) son segmenti eklenen **stdoutLogFile** yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-254">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f31d8-255">Varsa `.\logs\stdout` sağlanan bir değer olarak, bir örnek stdout günlük olarak kaydedilir *stdout_20180205194132_1934.log* içinde *günlükleri* 2/5/2018'de, bir işlem kimliğine sahip 1934 19:41:32 kaydedildiğinde klasör.</span><span class="sxs-lookup"><span data-stu-id="f31d8-255">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="f31d8-256">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f31d8-256">Attribute</span></span> | <span data-ttu-id="f31d8-257">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f31d8-257">Description</span></span> | <span data-ttu-id="f31d8-258">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="f31d8-258">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f31d8-259">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-259">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-260">Belirtilen yürütülebilir dosya için bağımsız değişkenler **processPath**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-260">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f31d8-261">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-261">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-262">TRUE ise **502.5 - işlem hatası** sayfa geçersiz kılınır ve 502 durumu kod sayfası yapılandırılan *web.config* önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-262">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f31d8-263">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-263">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-264">TRUE ise, istek başına 'MS-ASPNETCORE-WINAUTHTOKEN' üst bilgi olarak ASPNETCORE_PORT % üzerinde dinleme alt işlem belirteci iletilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-264">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f31d8-265">İstek başına Bu belirteci CloseHandle çağırmak için işlemin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-265">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="f31d8-266">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-266">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-267">Belirtilen işlem örneklerinin sayısını belirtir **processPath** ayarı hazırladık yedekleme uygulama.</span><span class="sxs-lookup"><span data-stu-id="f31d8-267">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="f31d8-268">Ayar `processesPerApplication` önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-268">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="f31d8-269">Bu öznitelik, gelecekteki bir sürümde kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="f31d8-269">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="f31d8-270">Varsayılan: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-270">Default: `1`</span></span><br><span data-ttu-id="f31d8-271">En küçük: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-271">Min: `1`</span></span><br><span data-ttu-id="f31d8-272">En fazla: `100`</span><span class="sxs-lookup"><span data-stu-id="f31d8-272">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="f31d8-273">Gerekli dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-273">Required string attribute.</span></span></p><p><span data-ttu-id="f31d8-274">HTTP istekleri için dinleme işlemini başlatan yürütülebilir dosya yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-274">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f31d8-275">Göreli yollar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-275">Relative paths are supported.</span></span> <span data-ttu-id="f31d8-276">Yol ile başlıyorsa `.`, yolun site köküne göreli olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-276">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f31d8-277">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-277">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-278">Belirtilen işlem sayısını belirtir **processPath** dakika başına kilitlenme izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-278">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f31d8-279">Bu sınır aşılırsa, dakikanın geri kalanı için işlem başlatılırken modülü durdurur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-279">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="f31d8-280">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-280">Default: `10`</span></span><br><span data-ttu-id="f31d8-281">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-281">Min: `0`</span></span><br><span data-ttu-id="f31d8-282">En fazla: `100`</span><span class="sxs-lookup"><span data-stu-id="f31d8-282">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f31d8-283">İsteğe bağlı timespan özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-283">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f31d8-284">ASP.NET Core modülü ASPNETCORE_PORT % üzerinde dinleme işleminden yanıt almayı bekleyeceği süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-284">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f31d8-285">ASP.NET Core 2.1 veya daha sonra sürüm ile birlikte gelen ASP.NET Core modülü sürümlerinde `requestTimeout` saat, dakika ve saniye olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-285">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="f31d8-286">Varsayılan: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-286">Default: `00:02:00`</span></span><br><span data-ttu-id="f31d8-287">En küçük: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-287">Min: `00:00:00`</span></span><br><span data-ttu-id="f31d8-288">En fazla: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-288">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f31d8-289">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-289">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-290">Modül düzgün biçimde kapatma çalıştırılabiliri için bekleyeceği saniye cinsinden zaman *app_offline.htm* dosyası algılandı.</span><span class="sxs-lookup"><span data-stu-id="f31d8-290">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f31d8-291">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-291">Default: `10`</span></span><br><span data-ttu-id="f31d8-292">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-292">Min: `0`</span></span><br><span data-ttu-id="f31d8-293">En fazla: `600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-293">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f31d8-294">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-294">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-295">Modül için yürütülebilir dosya bağlantı noktası üzerinde dinleme işlemini başlatmasını bekleyeceği saniye cinsinden süre.</span><span class="sxs-lookup"><span data-stu-id="f31d8-295">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f31d8-296">Bu süre aşılırsa, modül işlemi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-296">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f31d8-297">Yeni bir istek alırsa ve uygulamayı başlatmak tarayamaz hale gelen sonraki istekleri işlemi yeniden denemek devam ediyor, işlemi yeniden başlatın dener modülün **rapidFailsPerMinute** son kez sayısı sıralı dakika.</span><span class="sxs-lookup"><span data-stu-id="f31d8-297">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="f31d8-298">0 (sıfır) değeri **değil** sonsuz zaman aşımını kabul.</span><span class="sxs-lookup"><span data-stu-id="f31d8-298">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="f31d8-299">Varsayılan: `120`</span><span class="sxs-lookup"><span data-stu-id="f31d8-299">Default: `120`</span></span><br><span data-ttu-id="f31d8-300">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-300">Min: `0`</span></span><br><span data-ttu-id="f31d8-301">En fazla: `3600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-301">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f31d8-302">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-302">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-303">TRUE ise **stdout** ve **stderr** belirtilen işlem için **processPath** belirtilen dosyaya yeniden yönlendirilen **stdoutLogFile**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-303">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f31d8-304">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-304">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-305">Kendisi için göreli veya mutlak dosya yolunu belirtir **stdout** ve **stderr** belirtilen işlemden **processPath** kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-305">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f31d8-306">Site köküne göreli yollardır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-306">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f31d8-307">İle başlayan herhangi bir yola `.` olan göreli site kök ve diğer tüm yolları mutlak yollar olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-307">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f31d8-308">Modül bir günlük dosyası oluşturmak için sırayla yolunda sağlanan herhangi bir klasörde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-308">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f31d8-309">Alt çizgi sınırlayıcıları, bir zaman damgası, işlem kimliği ve dosya uzantısı kullanarak (*.log*) son segmenti eklenen **stdoutLogFile** yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-309">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f31d8-310">Varsa `.\logs\stdout` sağlanan bir değer olarak, bir örnek stdout günlük olarak kaydedilir *stdout_20180205194132_1934.log* içinde *günlükleri* 2/5/2018'de, bir işlem kimliğine sahip 1934 19:41:32 kaydedildiğinde klasör.</span><span class="sxs-lookup"><span data-stu-id="f31d8-310">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="f31d8-311">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f31d8-311">Attribute</span></span> | <span data-ttu-id="f31d8-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f31d8-312">Description</span></span> | <span data-ttu-id="f31d8-313">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="f31d8-313">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f31d8-314">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-314">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-315">Belirtilen yürütülebilir dosya için bağımsız değişkenler **processPath**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-315">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f31d8-316">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-316">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-317">TRUE ise **502.5 - işlem hatası** sayfa geçersiz kılınır ve 502 durumu kod sayfası yapılandırılan *web.config* önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-317">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f31d8-318">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-318">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-319">TRUE ise, istek başına 'MS-ASPNETCORE-WINAUTHTOKEN' üst bilgi olarak ASPNETCORE_PORT % üzerinde dinleme alt işlem belirteci iletilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-319">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f31d8-320">İstek başına Bu belirteci CloseHandle çağırmak için işlemin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-320">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="f31d8-321">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-321">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-322">Belirtilen işlem örneklerinin sayısını belirtir **processPath** ayarı hazırladık yedekleme uygulama.</span><span class="sxs-lookup"><span data-stu-id="f31d8-322">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="f31d8-323">Ayar `processesPerApplication` önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-323">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="f31d8-324">Bu öznitelik, gelecekteki bir sürümde kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="f31d8-324">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="f31d8-325">Varsayılan: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-325">Default: `1`</span></span><br><span data-ttu-id="f31d8-326">En küçük: `1`</span><span class="sxs-lookup"><span data-stu-id="f31d8-326">Min: `1`</span></span><br><span data-ttu-id="f31d8-327">En fazla: `100`</span><span class="sxs-lookup"><span data-stu-id="f31d8-327">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="f31d8-328">Gerekli dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-328">Required string attribute.</span></span></p><p><span data-ttu-id="f31d8-329">HTTP istekleri için dinleme işlemini başlatan yürütülebilir dosya yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-329">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f31d8-330">Göreli yollar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-330">Relative paths are supported.</span></span> <span data-ttu-id="f31d8-331">Yol ile başlıyorsa `.`, yolun site köküne göreli olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-331">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f31d8-332">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-332">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-333">Belirtilen işlem sayısını belirtir **processPath** dakika başına kilitlenme izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="f31d8-333">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f31d8-334">Bu sınır aşılırsa, dakikanın geri kalanı için işlem başlatılırken modülü durdurur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-334">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="f31d8-335">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-335">Default: `10`</span></span><br><span data-ttu-id="f31d8-336">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-336">Min: `0`</span></span><br><span data-ttu-id="f31d8-337">En fazla: `100`</span><span class="sxs-lookup"><span data-stu-id="f31d8-337">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f31d8-338">İsteğe bağlı timespan özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-338">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f31d8-339">ASP.NET Core modülü ASPNETCORE_PORT % üzerinde dinleme işleminden yanıt almayı bekleyeceği süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-339">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f31d8-340">ASP.NET Core 2.0 veya daha önceki sürüm ile birlikte gelen ASP.NET Core modülü sürümlerinde `requestTimeout` yalnızca tam dakikalar içinde aksi 2 dakika için varsayılan olarak belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-340">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="f31d8-341">Varsayılan: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-341">Default: `00:02:00`</span></span><br><span data-ttu-id="f31d8-342">En küçük: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-342">Min: `00:00:00`</span></span><br><span data-ttu-id="f31d8-343">En fazla: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f31d8-343">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f31d8-344">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-344">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-345">Modül düzgün biçimde kapatma çalıştırılabiliri için bekleyeceği saniye cinsinden zaman *app_offline.htm* dosyası algılandı.</span><span class="sxs-lookup"><span data-stu-id="f31d8-345">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f31d8-346">Varsayılan: `10`</span><span class="sxs-lookup"><span data-stu-id="f31d8-346">Default: `10`</span></span><br><span data-ttu-id="f31d8-347">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-347">Min: `0`</span></span><br><span data-ttu-id="f31d8-348">En fazla: `600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-348">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f31d8-349">İsteğe bağlı tamsayı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-349">Optional integer attribute.</span></span></p><p><span data-ttu-id="f31d8-350">Modül için yürütülebilir dosya bağlantı noktası üzerinde dinleme işlemini başlatmasını bekleyeceği saniye cinsinden süre.</span><span class="sxs-lookup"><span data-stu-id="f31d8-350">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f31d8-351">Bu süre aşılırsa, modül işlemi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-351">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f31d8-352">Yeni bir istek alırsa ve uygulamayı başlatmak tarayamaz hale gelen sonraki istekleri işlemi yeniden denemek devam ediyor, işlemi yeniden başlatın dener modülün **rapidFailsPerMinute** son kez sayısı sıralı dakika.</span><span class="sxs-lookup"><span data-stu-id="f31d8-352">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="f31d8-353">Varsayılan: `120`</span><span class="sxs-lookup"><span data-stu-id="f31d8-353">Default: `120`</span></span><br><span data-ttu-id="f31d8-354">En küçük: `0`</span><span class="sxs-lookup"><span data-stu-id="f31d8-354">Min: `0`</span></span><br><span data-ttu-id="f31d8-355">En fazla: `3600`</span><span class="sxs-lookup"><span data-stu-id="f31d8-355">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f31d8-356">İsteğe bağlı Boolean özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-356">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f31d8-357">TRUE ise **stdout** ve **stderr** belirtilen işlem için **processPath** belirtilen dosyaya yeniden yönlendirilen **stdoutLogFile**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-357">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f31d8-358">İsteğe bağlı dize özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-358">Optional string attribute.</span></span></p><p><span data-ttu-id="f31d8-359">Kendisi için göreli veya mutlak dosya yolunu belirtir **stdout** ve **stderr** belirtilen işlemden **processPath** kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-359">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f31d8-360">Site köküne göreli yollardır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-360">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f31d8-361">İle başlayan herhangi bir yola `.` olan göreli site kök ve diğer tüm yolları mutlak yollar olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-361">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f31d8-362">Modül bir günlük dosyası oluşturmak için sırayla yolunda sağlanan herhangi bir klasörde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-362">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f31d8-363">Alt çizgi sınırlayıcıları, bir zaman damgası, işlem kimliği ve dosya uzantısı kullanarak (*.log*) son segmenti eklenen **stdoutLogFile** yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-363">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f31d8-364">Varsa `.\logs\stdout` sağlanan bir değer olarak, bir örnek stdout günlük olarak kaydedilir *stdout_20180205194132_1934.log* içinde *günlükleri* 2/5/2018'de, bir işlem kimliğine sahip 1934 19:41:32 kaydedildiğinde klasör.</span><span class="sxs-lookup"><span data-stu-id="f31d8-364">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="f31d8-365">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="f31d8-365">Setting environment variables</span></span>

::: moniker range=">= aspnetcore-3.0"

<span data-ttu-id="f31d8-366">Ortam değişkenleri, işlem için belirtilebilir `processPath` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-366">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="f31d8-367">Bir ortam değişkeni ile belirtin `<environmentVariable>` alt öğesi bir `<environmentVariables>` koleksiyon öğesi.</span><span class="sxs-lookup"><span data-stu-id="f31d8-367">Specify an environment variable with the `<environmentVariable>` child element of an `<environmentVariables>` collection element.</span></span> <span data-ttu-id="f31d8-368">Ortam değişkenleri bu bölümünde ortam değişkenlerini sistem üzerinde önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-368">Environment variables set in this section take precedence over system environment variables.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-3.0"

<span data-ttu-id="f31d8-369">Ortam değişkenleri, işlem için belirtilebilir `processPath` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-369">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="f31d8-370">Bir ortam değişkeni ile belirtin `<environmentVariable>` alt öğesi bir `<environmentVariables>` koleksiyon öğesi.</span><span class="sxs-lookup"><span data-stu-id="f31d8-370">Specify an environment variable with the `<environmentVariable>` child element of an `<environmentVariables>` collection element.</span></span>

> [!WARNING]
> <span data-ttu-id="f31d8-371">Aynı ada sahip bu bölümde çakışma sistem ortam değişkenlerini ayarlamak ortam değişkenlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-371">Environment variables set in this section conflict with system environment variables set with the same name.</span></span> <span data-ttu-id="f31d8-372">Hem de bir ortam değişkenine ayarlanmışsa *web.config* dosya ve sistem düzeyi, Windows, değerinden *web.config* dosya sistemi ortam değişken değerini (eklenmiş olur Örneğin, `ASPNETCORE_ENVIRONMENT: Development;Development`), önleyen uygulamanın başlatılmasını.</span><span class="sxs-lookup"><span data-stu-id="f31d8-372">If an environment variable is set in both the *web.config* file and at the system level in Windows, the value from the *web.config* file becomes appended to the system environment variable value (for example, `ASPNETCORE_ENVIRONMENT: Development;Development`), which prevents the app from starting.</span></span>

::: moniker-end

<span data-ttu-id="f31d8-373">Aşağıdaki örnek, iki ortam değişkenlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f31d8-373">The following example sets two environment variables.</span></span> <span data-ttu-id="f31d8-374">`ASPNETCORE_ENVIRONMENT` uygulamanın ortamı yapılandırır `Development`.</span><span class="sxs-lookup"><span data-stu-id="f31d8-374">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="f31d8-375">Bir geliştirici geçici olarak bu değer ayarlayabilir *web.config* zorlamak için dosya [Geliştirici özel durum sayfasında](xref:fundamentals/error-handling) uygulama özel durum hata ayıklama sırasında yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="f31d8-375">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="f31d8-376">`CONFIG_DIR` bir kullanıcı tarafından tanımlanan ortam değişkeni Geliştirici uygulamanın yapılandırma dosyası yükleme için bir yol oluşturmak için başlangıç değeri okuyan kod burada yazmıştır örneğidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-376">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="InProcess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="f31d8-377">Doğrudan bir ortam ayarını bir alternatif *web.config* eklemektir `<EnvironmentName>` yayımlama profilini özelliğinde (*.pubxml*) ya da proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="f31d8-377">An alternative to setting the environment directly in *web.config* is to include the `<EnvironmentName>` property in the publish profile (*.pubxml*) or project file.</span></span> <span data-ttu-id="f31d8-378">Bu yaklaşım ortamı ayarlar *web.config* proje yayımlandığında ne zaman:</span><span class="sxs-lookup"><span data-stu-id="f31d8-378">This approach sets the environment in *web.config* when the project is published:</span></span>
>
> ```xml
> <PropertyGroup>
>   <EnvironmentName>Development</EnvironmentName>
> </PropertyGroup>
> ```

::: moniker-end

> [!WARNING]
> <span data-ttu-id="f31d8-379">Yalnızca `ASPNETCORE_ENVIRONMENT` ortam değişkenine `Development` Internet gibi güvenilmeyen ağlara erişilemez sunucularını test etme ve hazırlama.</span><span class="sxs-lookup"><span data-stu-id="f31d8-379">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="f31d8-380">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="f31d8-380">app_offline.htm</span></span>

<span data-ttu-id="f31d8-381">Bir dosya varsa adıyla *app_offline.htm* algılandığında, uygulama kök dizininde ASP.NET Core modülü gelen istekleri işlemeyi durdur ve uygulama düzgün bir şekilde kapatmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-381">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="f31d8-382">Uygulama içinde tanımlanan saniye sonra hala çalışıyorsa `shutdownTimeLimit`, ASP.NET Core modülü çalışan işlemi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-382">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="f31d8-383">Sırada *app_offline.htm* dosya varsa, ASP.NET Core modülü isteklerine içeriği yeniden göndererek yanıt *app_offline.htm* dosya.</span><span class="sxs-lookup"><span data-stu-id="f31d8-383">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="f31d8-384">Zaman *app_offline.htm* dosya kaldırılır, uygulamanın sonraki isteği başlatır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-384">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-385">Açık bir bağlantı varsa işlem dışı barındırma modeli kullanılırken, uygulamayı hemen kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="f31d8-385">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="f31d8-386">Örneğin, bir websocket bağlantısı uygulama kapatma gecikmeye neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-386">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="f31d8-387">Başlangıç hata sayfası</span><span class="sxs-lookup"><span data-stu-id="f31d8-387">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-388">İşlem içi ve dışı işlem uygulamayı başlatmak başarısız olduğunda ürettiği özel hata sayfaları barındırma.</span><span class="sxs-lookup"><span data-stu-id="f31d8-388">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="f31d8-389">Her iki işlem veya işlem dışı istek işleyicisi, bulmak gereken ASP.NET Core modülü başarısız olursa bir *500.0 - içindeki işlem/Out-işlem işleyicisi yükleme hatası* durumu kod sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-389">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="f31d8-390">Uygulamayı başlatmak gereken ASP.NET Core modülü başarısız olursa, işlem içi barındırma için bir *500.30 - başlangıç hatası* durumu kod sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-390">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="f31d8-391">Arka uç işlemi veya arka uç işlemi başlar ancak yapılandırılmış bağlantı noktasında dinleyecek biçimde başarısız başlatmak gereken ASP.NET Core modülü başarısız olursa, barındırma işlemi çıkış için bir *502.5 - işlem hatası* durumu kod sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-391">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="f31d8-392">Bu sayfayı gösterme ve varsayılan IIS 5xx durum kod sayfasına geri dönmek için kullandığınız `disableStartUpErrorPage` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-392">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="f31d8-393">Özel hata iletileri yapılandırma hakkında daha fazla bilgi için bkz. [HTTP hataları \<httpErrors >](/iis/configuration/system.webServer/httpErrors/).</span><span class="sxs-lookup"><span data-stu-id="f31d8-393">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f31d8-394">Arka uç işlemi veya arka uç işlemi başlar ancak yapılandırılmış bağlantı noktasında dinleyecek biçimde başarısız başlatmak gereken ASP.NET Core modülü başarısız olursa bir *502.5 - işlem hatası* durumu kod sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="f31d8-394">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="f31d8-395">Bu sayfayı gösterme ve varsayılan IIS 502 durumu kod sayfasına geri dönmek için kullandığınız `disableStartUpErrorPage` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f31d8-395">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="f31d8-396">Özel hata iletileri yapılandırma hakkında daha fazla bilgi için bkz. [HTTP hataları \<httpErrors >](/iis/configuration/system.webServer/httpErrors/).</span><span class="sxs-lookup"><span data-stu-id="f31d8-396">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 işlem hatası durum kodu sayfası](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="f31d8-398">Günlük oluşturma ve yönlendirme</span><span class="sxs-lookup"><span data-stu-id="f31d8-398">Log creation and redirection</span></span>

<span data-ttu-id="f31d8-399">ASP.NET Core modülü, stdout ve stderr konsol çıktısı diske yönlendirir `stdoutLogEnabled` ve `stdoutLogFile` özniteliklerini `aspNetCore` öğesi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-399">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="f31d8-400">Herhangi bir klasörde `stdoutLogFile` günlük dosyası oluşturulduğunda, yol modülü tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-400">Any folders in the `stdoutLogFile` path are created by the module when the log file is created.</span></span> <span data-ttu-id="f31d8-401">Uygulama havuzu günlükleri yazıldığı konumuna yazma erişimi olması gerekir (kullanın `IIS AppPool\<app_pool_name>` yazma izni sağlamak için).</span><span class="sxs-lookup"><span data-stu-id="f31d8-401">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="f31d8-402">Günlükleri Döndürülmüş değildir, bu işlem geri dönüştürme/yeniden başlatma gerçekleşmediği sürece.</span><span class="sxs-lookup"><span data-stu-id="f31d8-402">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="f31d8-403">Barındırma sağlayıcının günlüklerini kullanma disk alanını sınırla sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-403">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="f31d8-404">Stdout günlüğü kullanarak uygulama başlatma sorunlarını gidermek için yalnızca önerilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-404">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="f31d8-405">Stdout günlük genel uygulama günlüğe kaydetme amacıyla kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-405">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="f31d8-406">ASP.NET Core uygulamanızı rutin günlüğü için günlük dosyası boyutunu sınırlar ve günlükleri döndürür bir günlük kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-406">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="f31d8-407">Daha fazla bilgi için [üçüncü taraf günlük sağlayıcıları](xref:fundamentals/logging/index#third-party-logging-providers).</span><span class="sxs-lookup"><span data-stu-id="f31d8-407">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="f31d8-408">Bir zaman damgası ve dosya uzantısı günlük dosyası oluşturulduğunda otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-408">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="f31d8-409">Günlük dosyası adı zaman damgası, işlem kimliği ve dosya uzantısı ekleyerek oluşur (*.log*) son segmenti için `stdoutLogFile` yolu (genellikle *stdout*) alt çizgi ile ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="f31d8-409">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="f31d8-410">Varsa `stdoutLogFile` yolu ile sona erer *stdout*, bir PID 19:42:32 2/5/2018'de oluşturulan 1934 ile bir uygulama için bir günlük dosyası adına sahip *stdout_20180205194132_1934.log*.</span><span class="sxs-lookup"><span data-stu-id="f31d8-410">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-411">Varsa `stdoutLogEnabled` uygulama başlatma sırasında oluşan hatalar yakalanır ve olay günlüğüne yayılan false ise 30 KB'a kadar.</span><span class="sxs-lookup"><span data-stu-id="f31d8-411">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="f31d8-412">Başlatma işleminden sonra tüm ek günlükler atılır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-412">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="f31d8-413">Aşağıdaki örnek `aspNetCore` öğesi stdout günlük kaydı için Azure App Service'te barındırılan bir uygulamayı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-413">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="f31d8-414">Bir yerel yol ya da ağ paylaşımı yolu yerel günlüğe kaydetme için kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-414">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="f31d8-415">Uygulama havuzu kullanıcı kimliği sağlanan yol için yazma izni olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-415">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="f31d8-416">Gelişmiş tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="f31d8-416">Enhanced diagnostic logs</span></span>

<span data-ttu-id="f31d8-417">ASP.NET Core modülü Gelişmiş tanılama günlükleri sağlamak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-417">The ASP.NET Core Module is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="f31d8-418">Ekleme `<handlerSettings>` öğesine `<aspNetCore>` öğesinde *web.config*. Ayarı `debugLevel` için `TRACE` tanılama bilgileri daha yüksek bir aslına uygunluk sunar:</span><span class="sxs-lookup"><span data-stu-id="f31d8-418">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="f31d8-419">Hata ayıklama düzeyini (`debugLevel`) hem düzeyine hem de konum değerleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-419">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="f31d8-420">Düzeyleri (en az sırası için en ayrıntılı):</span><span class="sxs-lookup"><span data-stu-id="f31d8-420">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="f31d8-421">HATA</span><span class="sxs-lookup"><span data-stu-id="f31d8-421">ERROR</span></span>
* <span data-ttu-id="f31d8-422">UYARI</span><span class="sxs-lookup"><span data-stu-id="f31d8-422">WARNING</span></span>
* <span data-ttu-id="f31d8-423">BİLGİLERİ</span><span class="sxs-lookup"><span data-stu-id="f31d8-423">INFO</span></span>
* <span data-ttu-id="f31d8-424">TRACE</span><span class="sxs-lookup"><span data-stu-id="f31d8-424">TRACE</span></span>

<span data-ttu-id="f31d8-425">(Birden fazla konumda izin verilir) konumları:</span><span class="sxs-lookup"><span data-stu-id="f31d8-425">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="f31d8-426">KONSOLU</span><span class="sxs-lookup"><span data-stu-id="f31d8-426">CONSOLE</span></span>
* <span data-ttu-id="f31d8-427">OLAY GÜNLÜĞÜ</span><span class="sxs-lookup"><span data-stu-id="f31d8-427">EVENTLOG</span></span>
* <span data-ttu-id="f31d8-428">DOSYA</span><span class="sxs-lookup"><span data-stu-id="f31d8-428">FILE</span></span>

<span data-ttu-id="f31d8-429">İşleyici ayarları ortam değişkenlerini de sağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="f31d8-429">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="f31d8-430">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Hata ayıklama günlük dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-430">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="f31d8-431">(Varsayılan: *aspnetcore debug.log*)</span><span class="sxs-lookup"><span data-stu-id="f31d8-431">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="f31d8-432">`ASPNETCORE_MODULE_DEBUG` &ndash; Hata ayıklama düzeyi ayarı.</span><span class="sxs-lookup"><span data-stu-id="f31d8-432">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="f31d8-433">Yapmak **değil** hata ayıklama günlüğü dağıtımı için sorun gidermek için gereken süreden etkin bırakın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-433">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="f31d8-434">Günlüğünün boyutu sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-434">The size of the log isn't limited.</span></span> <span data-ttu-id="f31d8-435">Etkin hata ayıklama günlüğünü bırakarak, kullanılabilir disk alanı tüketebilir ve sunucu veya app service kilitlenme.</span><span class="sxs-lookup"><span data-stu-id="f31d8-435">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="f31d8-436">Bkz: [web.config yapılandırmasıyla](#configuration-with-webconfig) ilişkin bir örnek `aspNetCore` öğesinde *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="f31d8-436">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="f31d8-437">HTTP protokolü ve eşleştirme simgesi Ara sunucu yapılandırmasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-437">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-438">*Yalnızca işlem dışı barındırmak için geçerlidir.*</span><span class="sxs-lookup"><span data-stu-id="f31d8-438">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="f31d8-439">Kestrel ve ASP.NET Core modülü arasında oluşturulan proxy, HTTP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-439">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="f31d8-440">HTTP bir performans iyileştirme Kestrel ve modül arasındaki trafik bir geri döngü adresine ağ arabiriminin dışına gerçekleştiği kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-440">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="f31d8-441">Sunucu oturumunu bir konumdan Kestrel ve modül arasındaki trafik gizlice, riski yoktur.</span><span class="sxs-lookup"><span data-stu-id="f31d8-441">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="f31d8-442">Eşleşme bir belirteç Kestrel tarafından alınan isteklerden IIS tarafından proxy ve başka bir kaynaktan gelmemiştir güvence altına almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f31d8-442">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="f31d8-443">Eşleştirme belirteç oluşturulur ve bir ortam değişkeninde ayarlayın (`ASPNETCORE_TOKEN`) modülü tarafından.</span><span class="sxs-lookup"><span data-stu-id="f31d8-443">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="f31d8-444">Eşleştirme belirteç de bir üstbilgisine ayarlanır (`MS-ASPNETCORE-TOKEN`) proxy kullanan her istekte.</span><span class="sxs-lookup"><span data-stu-id="f31d8-444">The pairing token is also set into a header (`MS-ASPNETCORE-TOKEN`) on every proxied request.</span></span> <span data-ttu-id="f31d8-445">IIS ara yazılım denetimleri eşleştirme belirteci üstbilgi değeri ortam değişken değerini eşleştiğini doğrulamak için aldığı istek.</span><span class="sxs-lookup"><span data-stu-id="f31d8-445">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="f31d8-446">Belirteç değerleri eşleşirse, isteği günlüğe ve reddedildi.</span><span class="sxs-lookup"><span data-stu-id="f31d8-446">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="f31d8-447">Eşleştirme belirteci ortam değişkeni ve Kestrel ve modül arasındaki trafik bir konumdan sunucu dışına erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="f31d8-447">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="f31d8-448">Eşleştirme belirteç değeri farkında olmadan bir saldırgan IIS Ara yazılımında denetimini atla istekleri gönderemiyor.</span><span class="sxs-lookup"><span data-stu-id="f31d8-448">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="f31d8-449">Bir IIS ile ASP.NET Core modülü paylaşılan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f31d8-449">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="f31d8-450">ASP.NET Core modülü yükleyiciyi ayrıcalıklarıyla çalıştırır **TrustedInstaller** hesabı.</span><span class="sxs-lookup"><span data-stu-id="f31d8-450">The ASP.NET Core Module installer runs with the privileges of the **TrustedInstaller** account.</span></span> <span data-ttu-id="f31d8-451">IIS paylaşılan yapılandırması tarafından kullanılan paylaşımı yol için izne sahip yerel sistem hesabı olmayan değiştirme çünkü Yükleyici bir erişim reddedildi hatası modül ayarlarını yapılandırılmaya çalışılırken oluşturur *applicationHost.config*  Dosya paylaşımındaki.</span><span class="sxs-lookup"><span data-stu-id="f31d8-451">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer throws an access denied error when attempting to configure the module settings in the *applicationHost.config* file on the share.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f31d8-452">IIS paylaşılan yapılandırmaya, IIS yüklemesi ile aynı makinede kullanırken, ASP.NET Core barındırma Paket Yükleyici ile çalıştırma `OPT_NO_SHARED_CONFIG_CHECK` parametresini `1`:</span><span class="sxs-lookup"><span data-stu-id="f31d8-452">When using an IIS Shared Configuration on the same machine as the IIS installation, run the ASP.NET Core Hosting Bundle installer with the `OPT_NO_SHARED_CONFIG_CHECK` parameter set to `1`:</span></span>

```console
dotnet-hosting-{VERSION}.exe OPT_NO_SHARED_CONFIG_CHECK=1
```

<span data-ttu-id="f31d8-453">Paylaşılan yapılandırma yolu IIS yüklemesi ile aynı makinede olmadığı durumlarda, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f31d8-453">When the path to the shared configuration isn't on the same machine as the IIS installation, follow these steps:</span></span>

1. <span data-ttu-id="f31d8-454">IIS paylaşılan yapılandırması devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-454">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="f31d8-455">Yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-455">Run the installer.</span></span>
1. <span data-ttu-id="f31d8-456">Güncelleştirilmiş dışarı *applicationHost.config* dosya paylaşımına.</span><span class="sxs-lookup"><span data-stu-id="f31d8-456">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="f31d8-457">IIS paylaşılan yapılandırması yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f31d8-457">Re-enable the IIS Shared Configuration.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f31d8-458">IIS paylaşılan yapılandırmaya kullanırken, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f31d8-458">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="f31d8-459">IIS paylaşılan yapılandırması devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-459">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="f31d8-460">Yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f31d8-460">Run the installer.</span></span>
1. <span data-ttu-id="f31d8-461">Güncelleştirilmiş dışarı *applicationHost.config* dosya paylaşımına.</span><span class="sxs-lookup"><span data-stu-id="f31d8-461">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="f31d8-462">IIS paylaşılan yapılandırması yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f31d8-462">Re-enable the IIS Shared Configuration.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="application-initialization"></a><span data-ttu-id="f31d8-463">Uygulama başlatma</span><span class="sxs-lookup"><span data-stu-id="f31d8-463">Application Initialization</span></span>

<span data-ttu-id="f31d8-464">[IIS uygulama başlatma](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization) uygulama havuzunu başlatır veya geri dönüştürüldüğünde, uygulamaya bir HTTP isteği gönderir, bir IIS özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-464">[IIS Application Initialization](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization) is an IIS feature that sends an HTTP request to the app when the app pool starts or is recycled.</span></span> <span data-ttu-id="f31d8-465">İstek, uygulamanın başlatılması tetikler.</span><span class="sxs-lookup"><span data-stu-id="f31d8-465">The request triggers the app to start.</span></span> <span data-ttu-id="f31d8-466">Uygulama başlatma her ikisi için de kullanılabilir [işlem içi barındırma modeli](xref:fundamentals/servers/index#in-process-hosting-model) ve [işlem dışı barındırma modeli](xref:fundamentals/servers/index#out-of-process-hosting-model) ile ASP.NET Core modülü sürüm 2.</span><span class="sxs-lookup"><span data-stu-id="f31d8-466">Application Initialization can be used by both the [in-process hosting model](xref:fundamentals/servers/index#in-process-hosting-model) and [out-of-process hosting model](xref:fundamentals/servers/index#out-of-process-hosting-model) with the ASP.NET Core Module version 2.</span></span>

<span data-ttu-id="f31d8-467">Uygulama başlatma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="f31d8-467">To enable Application Initialization:</span></span>

1. <span data-ttu-id="f31d8-468">IIS uygulama başlatma rolü özelliği etkin olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="f31d8-468">Confirm that the IIS Application Initialization role feature in enabled:</span></span>
   * <span data-ttu-id="f31d8-469">Windows 7 veya sonraki sürümlerde: Gidin **Denetim Masası** > **programlar** > **programlar ve Özellikler** > **kapatma Windows özellikleri hakkında ya da kapalı** (ekranın sol).</span><span class="sxs-lookup"><span data-stu-id="f31d8-469">On Windows 7 or later: Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="f31d8-470">Açık **Internet Information Services** > **World Wide Web Hizmetleri** > **uygulama geliştirme özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-470">Open **Internet Information Services** > **World Wide Web Services** > **Application Development Features**.</span></span> <span data-ttu-id="f31d8-471">Onay kutusunu seçin **uygulama başlatma**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-471">Select the check box for **Application Initialization**.</span></span>
   * <span data-ttu-id="f31d8-472">Windows Server 2008 R2 veya sonraki sürümlerde, açık **Ekle roller ve Özellikler Sihirbazı**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-472">On Windows Server 2008 R2 or later, open the **Add Roles and Features Wizard**.</span></span> <span data-ttu-id="f31d8-473">Ulaştığınızda **rol hizmetlerini seçin** paneli, açık **uygulama geliştirme** düğümünü seçip alt **uygulama başlatma** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="f31d8-473">When you reach the **Select role services** panel, open the **Application Development** node and select the **Application Initialization** check box.</span></span>
1. <span data-ttu-id="f31d8-474">IIS Yöneticisi'nde **uygulama havuzları** içinde **bağlantıları** paneli.</span><span class="sxs-lookup"><span data-stu-id="f31d8-474">In IIS Manager, select **Application Pools** in the **Connections** panel.</span></span>
1. <span data-ttu-id="f31d8-475">Listede uygulamanın uygulama havuzunu seçin.</span><span class="sxs-lookup"><span data-stu-id="f31d8-475">Select the app's app pool in the list.</span></span>
1. <span data-ttu-id="f31d8-476">Seçin **Gelişmiş ayarlar** altında **uygulama havuzunu Düzenle** içinde **eylemleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="f31d8-476">Select **Advanced Settings** under **Edit Application Pool** in the **Actions** panel.</span></span>
1. <span data-ttu-id="f31d8-477">Ayarlama **başlangıç modu** için **AlwaysRunning**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-477">Set **Start Mode** to **AlwaysRunning**.</span></span>
1. <span data-ttu-id="f31d8-478">Açık **siteleri** düğümünde **bağlantıları** paneli.</span><span class="sxs-lookup"><span data-stu-id="f31d8-478">Open the **Sites** node in the **Connections** panel.</span></span>
1. <span data-ttu-id="f31d8-479">Uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="f31d8-479">Select the app.</span></span>
1. <span data-ttu-id="f31d8-480">Seçin **Gelişmiş ayarlar** altında **Web sitesini Yönet** içinde **eylemleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="f31d8-480">Select **Advanced Settings** under **Manage Website** in the **Actions** panel.</span></span>
1. <span data-ttu-id="f31d8-481">Ayarlama **önceden yükleme etkin** için **True**.</span><span class="sxs-lookup"><span data-stu-id="f31d8-481">Set **Preload Enabled** to **True**.</span></span>

<span data-ttu-id="f31d8-482">Daha fazla bilgi için [IIS 8.0 uygulama başlatma](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization).</span><span class="sxs-lookup"><span data-stu-id="f31d8-482">For more information, see [IIS 8.0 Application Initialization](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization).</span></span>

<span data-ttu-id="f31d8-483">Kullanan uygulamalar [işlem dışı barındırma modeli](xref:fundamentals/servers/index#out-of-process-hosting-model) uygulamanın çalışmasını sağlamak için düzenli aralıklarla ping göndermek için bir dış hizmet kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f31d8-483">Apps that use the [out-of-process hosting model](xref:fundamentals/servers/index#out-of-process-hosting-model) must use an external service to periodically ping the app in order to keep it running.</span></span>

::: moniker-end

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="f31d8-484">Modül sürümü ve paket barındırma yükleyici günlükleri</span><span class="sxs-lookup"><span data-stu-id="f31d8-484">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="f31d8-485">Yüklü ASP.NET Core modülü sürümünü belirlemek için:</span><span class="sxs-lookup"><span data-stu-id="f31d8-485">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="f31d8-486">Barındıran sistemde gidin *%windir%\System32\inetsrv*.</span><span class="sxs-lookup"><span data-stu-id="f31d8-486">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="f31d8-487">Bulun *aspnetcore.dll* dosya.</span><span class="sxs-lookup"><span data-stu-id="f31d8-487">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="f31d8-488">Dosyaya sağ tıklayıp **özellikleri** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="f31d8-488">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="f31d8-489">Seçin **ayrıntıları** sekmesi. **Dosya sürümü** ve **ürün sürümü** modülünün yüklü sürümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f31d8-489">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="f31d8-490">Barındırma Paket Yükleyici günlükleri modülü için adresten *C:\\kullanıcılar\\% UserName %\\AppData\\yerel\\Temp*. Dosyanın nasıl adlandırıldığı *dd_DotNetCoreWinSvrHosting__\<zaman damgası > _000_AspNetCoreModule_x64.log*.</span><span class="sxs-lookup"><span data-stu-id="f31d8-490">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="f31d8-491">Modül, şema ve yapılandırma dosyası konumları</span><span class="sxs-lookup"><span data-stu-id="f31d8-491">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="f31d8-492">Modül</span><span class="sxs-lookup"><span data-stu-id="f31d8-492">Module</span></span>

<span data-ttu-id="f31d8-493">**IIS (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="f31d8-493">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="f31d8-494">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-494">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="f31d8-495">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-495">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f31d8-496">%ProgramFiles%\IIS\Asp.NET çekirdek Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-496">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="f31d8-497">% ProgramFiles (x86) %\IIS\Asp.Net çekirdek Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-497">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="f31d8-498">**IIS Express (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="f31d8-498">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="f31d8-499">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-499">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="f31d8-500">% ProgramFiles (x86) %\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-500">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f31d8-501">%ProgramFiles%\IIS Express\Asp.Net çekirdek Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-501">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="f31d8-502">% ProgramFiles (x86) %\IIS Express\Asp.Net çekirdek Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f31d8-502">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="f31d8-503">Şema</span><span class="sxs-lookup"><span data-stu-id="f31d8-503">Schema</span></span>

<span data-ttu-id="f31d8-504">**IIS**</span><span class="sxs-lookup"><span data-stu-id="f31d8-504">**IIS**</span></span>

   * <span data-ttu-id="f31d8-505">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.XML</span><span class="sxs-lookup"><span data-stu-id="f31d8-505">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f31d8-506">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.XML</span><span class="sxs-lookup"><span data-stu-id="f31d8-506">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="f31d8-507">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="f31d8-507">**IIS Express**</span></span>

   * <span data-ttu-id="f31d8-508">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="f31d8-508">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f31d8-509">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="f31d8-509">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="f31d8-510">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f31d8-510">Configuration</span></span>

<span data-ttu-id="f31d8-511">**IIS**</span><span class="sxs-lookup"><span data-stu-id="f31d8-511">**IIS**</span></span>

   * <span data-ttu-id="f31d8-512">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="f31d8-512">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="f31d8-513">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="f31d8-513">**IIS Express**</span></span>

   * <span data-ttu-id="f31d8-514">Visual Studio: {Uygulama KÖKÜ}\\.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="f31d8-514">Visual Studio: {APPLICATION ROOT}\\.vs\config\applicationHost.config</span></span>
   
   * <span data-ttu-id="f31d8-515">*iisexpress.exe* CLI: %USERPROFILE%\Documents\IISExpress\config\applicationhost.config</span><span class="sxs-lookup"><span data-stu-id="f31d8-515">*iisexpress.exe* CLI: %USERPROFILE%\Documents\IISExpress\config\applicationhost.config</span></span>

<span data-ttu-id="f31d8-516">Dosyalar için arama yaparak bulunabilir *aspnetcore* içinde *applicationHost.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="f31d8-516">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f31d8-517">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f31d8-517">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* [<span data-ttu-id="f31d8-518">ASP.NET Core modülü GitHub deposu (başvuru kaynağı)</span><span class="sxs-lookup"><span data-stu-id="f31d8-518">ASP.NET Core Module GitHub repository (reference source)</span></span>](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
