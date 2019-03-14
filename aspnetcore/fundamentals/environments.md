---
title: ASP.NET Core birden çok ortam kullanma
author: rick-anderson
description: ASP.NET Core uygulamaları birden fazla ortam arasında uygulama davranışını denetleme konusunda bilgi edinin.
ms.author: riande
ms.date: 01/22/2019
uid: fundamentals/environments
ms.openlocfilehash: 39e1b48481832a6d76de605b37410fe2e16dcd88
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069294"
---
# <a name="use-multiple-environments-in-aspnet-core"></a><span data-ttu-id="828d4-103">ASP.NET Core birden çok ortam kullanma</span><span class="sxs-lookup"><span data-stu-id="828d4-103">Use multiple environments in ASP.NET Core</span></span>

<span data-ttu-id="828d4-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="828d4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="828d4-105">ASP.NET Core, bir ortam değişkeni kullanarak çalışma zamanı ortama göre uygulama davranışını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="828d4-105">ASP.NET Core configures app behavior based on the runtime environment using an environment variable.</span></span>

<span data-ttu-id="828d4-106">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="828d4-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="828d4-107">Ortamlar</span><span class="sxs-lookup"><span data-stu-id="828d4-107">Environments</span></span>

<span data-ttu-id="828d4-108">ASP.NET Core ortam değişkenini okur `ASPNETCORE_ENVIRONMENT` uygulamanın başlangıcında ve değeri depolar [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname).</span><span class="sxs-lookup"><span data-stu-id="828d4-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at app startup and stores the value in [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname).</span></span> <span data-ttu-id="828d4-109">Ayarlayabileceğiniz `ASPNETCORE_ENVIRONMENT` herhangi bir değere ancak [üç değerden](/dotnet/api/microsoft.aspnetcore.hosting.environmentname) framework tarafından desteklenir: [Geliştirme](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [hazırlama](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging), ve [üretim](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production).</span><span class="sxs-lookup"><span data-stu-id="828d4-109">You can set `ASPNETCORE_ENVIRONMENT` to any value, but [three values](/dotnet/api/microsoft.aspnetcore.hosting.environmentname) are supported by the framework: [Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [Staging](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging), and [Production](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production).</span></span> <span data-ttu-id="828d4-110">Varsa `ASPNETCORE_ENVIRONMENT` değil, varsayılan olarak, belirlenen `Production`.</span><span class="sxs-lookup"><span data-stu-id="828d4-110">If `ASPNETCORE_ENVIRONMENT` isn't set, it defaults to `Production`.</span></span>

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet)]

<span data-ttu-id="828d4-111">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="828d4-111">The preceding code:</span></span>

* <span data-ttu-id="828d4-112">Çağrıları [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) olduğunda `ASPNETCORE_ENVIRONMENT` ayarlanır `Development`.</span><span class="sxs-lookup"><span data-stu-id="828d4-112">Calls [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="828d4-113">Çağrıları [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler) zaman değerini `ASPNETCORE_ENVIRONMENT` aşağıdakilerden birine ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="828d4-113">Calls [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="828d4-114">[Ortam etiketi Yardımcısı](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) değerini kullanır `IHostingEnvironment.EnvironmentName` dahil edin veya dışlayın öğesinde bulunan işaretleme:</span><span class="sxs-lookup"><span data-stu-id="828d4-114">The [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-cshtml[](environments/sample-snapshot/EnvironmentsSample/Pages/About.cshtml)]

<span data-ttu-id="828d4-115">Windows ve macOS üzerinde ortam değişkenlerini ve değerleri büyük küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="828d4-115">On Windows and macOS, environment variables and values aren't case sensitive.</span></span> <span data-ttu-id="828d4-116">Linux ortam değişkenlerini ve değerleri **büyük küçük harfe duyarlı** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="828d4-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="828d4-117">Geliştirme</span><span class="sxs-lookup"><span data-stu-id="828d4-117">Development</span></span>

<span data-ttu-id="828d4-118">Geliştirme ortamının, üretim ortamında kullanıma sunulan olmamalıdır özellikleri etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="828d4-118">The development environment can enable features that shouldn't be exposed in production.</span></span> <span data-ttu-id="828d4-119">Örneğin, ASP.NET Core şablonları etkinleştirme [Geliştirici özel durum sayfasında](xref:fundamentals/error-handling#the-developer-exception-page) geliştirme ortamında.</span><span class="sxs-lookup"><span data-stu-id="828d4-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="828d4-120">Yerel makine geliştirme ortamını ayarlanabilir *Properties\launchSettings.json* proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="828d4-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="828d4-121">Ortam değerlerini kümesinde *launchSettings.json* sistemi ortamında ayarlanan değerleri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="828d4-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="828d4-122">Aşağıdaki JSON üç profillerden gösterir bir *launchSettings.json* dosyası:</span><span class="sxs-lookup"><span data-stu-id="828d4-122">The following JSON shows three profiles from a *launchSettings.json* file:</span></span>

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:54339/",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      }
    },
    "EnvironmentsSample": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:54340/"
    },
    "Kestrel Staging": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:51997/"
    }
  }
}
```

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="828d4-123">`applicationUrl` Özelliğinde *launchSettings.json* sunucu URL'lerin bir listesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="828d4-123">The `applicationUrl` property in *launchSettings.json* can specify a list of server URLs.</span></span> <span data-ttu-id="828d4-124">Listedeki URL'leri arasında noktalı virgül kullanın:</span><span class="sxs-lookup"><span data-stu-id="828d4-124">Use a semicolon between the URLs in the list:</span></span>
>
> ```json
> "EnvironmentsSample": {
>    "commandName": "Project",
>    "launchBrowser": true,
>    "applicationUrl": "https://localhost:5001;http://localhost:5000",
>    "environmentVariables": {
>      "ASPNETCORE_ENVIRONMENT": "Development"
>    }
> }
> ```

::: moniker-end

<span data-ttu-id="828d4-125">Ne zaman uygulama başlatıldığında ile [çalıştırma dotnet](/dotnet/core/tools/dotnet-run), ilk profiliyle `"commandName": "Project"` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="828d4-125">When the app is launched with [dotnet run](/dotnet/core/tools/dotnet-run), the first profile with `"commandName": "Project"` is used.</span></span> <span data-ttu-id="828d4-126">Değerini `commandName` başlatmak için web sunucusunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="828d4-126">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="828d4-127">`commandName` aşağıdakilerden herhangi biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="828d4-127">`commandName` can be any one of the following:</span></span>

* `IISExpress`
* `IIS`
* <span data-ttu-id="828d4-128">`Project` (hangi Kestrel başlatır)</span><span class="sxs-lookup"><span data-stu-id="828d4-128">`Project` (which launches Kestrel)</span></span>

<span data-ttu-id="828d4-129">Ne zaman bir uygulama başlatıldığında ile [çalıştırma dotnet](/dotnet/core/tools/dotnet-run):</span><span class="sxs-lookup"><span data-stu-id="828d4-129">When an app is launched with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

* <span data-ttu-id="828d4-130">*launchSettings.json* okunur varsa.</span><span class="sxs-lookup"><span data-stu-id="828d4-130">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="828d4-131">`environmentVariables` ayarlarında *launchSettings.json* ortam değişkenlerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="828d4-131">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="828d4-132">Barındırma ortamı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="828d4-132">The hosting environment is displayed.</span></span>

<span data-ttu-id="828d4-133">Bir uygulama kullanmaya aşağıdaki çıktıyı gösterir [çalıştırma dotnet](/dotnet/core/tools/dotnet-run):</span><span class="sxs-lookup"><span data-stu-id="828d4-133">The following output shows an app started with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

```bash
PS C:\Websites\EnvironmentsSample> dotnet run
Using launch settings from C:\Websites\EnvironmentsSample\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Websites\EnvironmentsSample
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="828d4-134">Visual Studio Proje özelliklerini **hata ayıklama** sekmesi düzenlemek için bir GUI sağlar *launchSettings.json* dosyası:</span><span class="sxs-lookup"><span data-stu-id="828d4-134">The Visual Studio project properties **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![Proje Özellikleri ayarı ortam değişkenleri](environments/_static/project-properties-debug.png)

<span data-ttu-id="828d4-136">Proje profillere yapılan değişiklikler web sunucu yeniden başlatılana kadar etkili değildir.</span><span class="sxs-lookup"><span data-stu-id="828d4-136">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="828d4-137">Kestrel'i, ortama yapılan değişiklikleri algılayabilir önce başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="828d4-137">Kestrel must be restarted before it can detect changes made to its environment.</span></span>

> [!WARNING]
> <span data-ttu-id="828d4-138">*launchSettings.json* gizli dizileri depolamak olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="828d4-138">*launchSettings.json* shouldn't store secrets.</span></span> <span data-ttu-id="828d4-139">[Gizli dizi Yöneticisi aracını](xref:security/app-secrets) yerel geliştirme için gizli dizileri depolamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="828d4-139">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

<span data-ttu-id="828d4-140">Kullanırken [Visual Studio Code](https://code.visualstudio.com/), ortam değişkenleri ayarlanabilir *.vscode/launch.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="828d4-140">When using [Visual Studio Code](https://code.visualstudio.com/), environment variables can be set in the *.vscode/launch.json* file.</span></span> <span data-ttu-id="828d4-141">Aşağıdaki örnek ortamı ayarlar `Development`:</span><span class="sxs-lookup"><span data-stu-id="828d4-141">The following example sets the environment to `Development`:</span></span>

```json
{
   "version": "0.2.0",
   "configurations": [
        {
            "name": ".NET Core Launch (web)",

            ... additional VS Code configuration settings ...

            "env": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    ]
}
```

<span data-ttu-id="828d4-142">A *.vscode/launch.json* proje dosyasında değil okuma uygulamayı başlatırken `dotnet run` aynı şekilde *Properties/launchSettings.json*.</span><span class="sxs-lookup"><span data-stu-id="828d4-142">A *.vscode/launch.json* file in the project isn't read when starting the app with `dotnet run` in the same way as *Properties/launchSettings.json*.</span></span> <span data-ttu-id="828d4-143">Bir uygulamaya sahip olmayan geliştirme başlatırken bir *launchSettings.json* dosyası ortamında bir ortam değişkeni veya bir komut satırı bağımsız değişkeni ile ayarlanan `dotnet run` komutu.</span><span class="sxs-lookup"><span data-stu-id="828d4-143">When launching an app in development that doesn't have a *launchSettings.json* file, either set the environment with an environment variable or a command-line argument to the `dotnet run` command.</span></span>

### <a name="production"></a><span data-ttu-id="828d4-144">Üretim</span><span class="sxs-lookup"><span data-stu-id="828d4-144">Production</span></span>

<span data-ttu-id="828d4-145">Üretim ortamında, güvenlik, performans ve uygulama sağlamlık en üst düzeye çıkarmak için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="828d4-145">The production environment should be configured to maximize security, performance, and app robustness.</span></span> <span data-ttu-id="828d4-146">Geliştirme farklı bazı ortak ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="828d4-146">Some common settings that differ from development include:</span></span>

* <span data-ttu-id="828d4-147">Önbelleğe alma.</span><span class="sxs-lookup"><span data-stu-id="828d4-147">Caching.</span></span>
* <span data-ttu-id="828d4-148">İstemci tarafı kaynakları küçültülmüş, toplanmış ve potansiyel olarak cdn'den.</span><span class="sxs-lookup"><span data-stu-id="828d4-148">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="828d4-149">Tanılama hata sayfalarını devre dışı.</span><span class="sxs-lookup"><span data-stu-id="828d4-149">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="828d4-150">Kolay hata sayfalarını etkin.</span><span class="sxs-lookup"><span data-stu-id="828d4-150">Friendly error pages enabled.</span></span>
* <span data-ttu-id="828d4-151">Üretim günlüğe kaydetme ve izleme etkin.</span><span class="sxs-lookup"><span data-stu-id="828d4-151">Production logging and monitoring enabled.</span></span> <span data-ttu-id="828d4-152">Örneğin, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span><span class="sxs-lookup"><span data-stu-id="828d4-152">For example, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="set-the-environment"></a><span data-ttu-id="828d4-153">Ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="828d4-153">Set the environment</span></span>

<span data-ttu-id="828d4-154">Genellikle, test etmek için belirli bir ortamı kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="828d4-154">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="828d4-155">Ortam ayarlanmadıysa, varsayılan `Production`, hangi devre dışı bırakır çoğu hata ayıklama özellikleri.</span><span class="sxs-lookup"><span data-stu-id="828d4-155">If the environment isn't set, it defaults to `Production`, which disables most debugging features.</span></span> <span data-ttu-id="828d4-156">Ortamını yöntemi işletim sistemine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="828d4-156">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure-app-service"></a><span data-ttu-id="828d4-157">Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="828d4-157">Azure App Service</span></span>

<span data-ttu-id="828d4-158">Ortamı ayarlamak için [Azure App Service](https://azure.microsoft.com/services/app-service/), aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="828d4-158">To set the environment in [Azure App Service](https://azure.microsoft.com/services/app-service/), perform the following steps:</span></span>

1. <span data-ttu-id="828d4-159">Uygulamadan seçin **uygulama hizmetleri** dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="828d4-159">Select the app from the **App Services** blade.</span></span>
1. <span data-ttu-id="828d4-160">İçinde **ayarları** grubu, select **uygulama ayarları** dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="828d4-160">In the **SETTINGS** group, select the **Application settings** blade.</span></span>
1. <span data-ttu-id="828d4-161">İçinde **uygulama ayarları** alanında **yeni ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="828d4-161">In the **Application settings** area, select **Add new setting**.</span></span>
1. <span data-ttu-id="828d4-162">İçin **bir ad girin**, sağlayan `ASPNETCORE_ENVIRONMENT`.</span><span class="sxs-lookup"><span data-stu-id="828d4-162">For **Enter a name**, provide `ASPNETCORE_ENVIRONMENT`.</span></span> <span data-ttu-id="828d4-163">İçin **bir değer girin**, ortamı sağlayın (örneğin, `Staging`).</span><span class="sxs-lookup"><span data-stu-id="828d4-163">For **Enter a value**, provide the environment (for example, `Staging`).</span></span>
1. <span data-ttu-id="828d4-164">Seçin **yuva ayarı** ortam ayarını, dağıtım yuvaları takas zaman ile geçerli yuvadaki kalmasına istiyorsanız kutuyu.</span><span class="sxs-lookup"><span data-stu-id="828d4-164">Select the **Slot Setting** check box if you wish the environment setting to remain with the current slot when deployment slots are swapped.</span></span> <span data-ttu-id="828d4-165">Daha fazla bilgi için [Azure belgeleri: Hangi ayarların değiştirilir? ](/azure/app-service/web-sites-staged-publishing).</span><span class="sxs-lookup"><span data-stu-id="828d4-165">For more information, see [Azure Documentation: Which settings are swapped?](/azure/app-service/web-sites-staged-publishing).</span></span>
1. <span data-ttu-id="828d4-166">Seçin **Kaydet** dikey penceresinin üstünde.</span><span class="sxs-lookup"><span data-stu-id="828d4-166">Select **Save** at the top of the blade.</span></span>

<span data-ttu-id="828d4-167">Bir uygulama ayarı (ortam değişkeni) eklenmesine, değiştirilmesine veya Azure portalda silinen sonra azure App Service uygulama otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="828d4-167">Azure App Service automatically restarts the app after an app setting (environment variable) is added, changed, or deleted in the Azure portal.</span></span>

### <a name="windows"></a><span data-ttu-id="828d4-168">Windows</span><span class="sxs-lookup"><span data-stu-id="828d4-168">Windows</span></span>

<span data-ttu-id="828d4-169">Ayarlanacak `ASPNETCORE_ENVIRONMENT` uygulama başlatıldığında geçerli oturum için kullanarak [çalıştırma dotnet](/dotnet/core/tools/dotnet-run), aşağıdaki komutları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="828d4-169">To set the `ASPNETCORE_ENVIRONMENT` for the current session when the app is started using [dotnet run](/dotnet/core/tools/dotnet-run), the following commands are used:</span></span>

<span data-ttu-id="828d4-170">**Komut İstemi**</span><span class="sxs-lookup"><span data-stu-id="828d4-170">**Command prompt**</span></span>

```console
set ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="828d4-171">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="828d4-171">**PowerShell**</span></span>

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="828d4-172">Bu komutları yalnızca geçerli pencere için etkili.</span><span class="sxs-lookup"><span data-stu-id="828d4-172">These commands only take effect for the current window.</span></span> <span data-ttu-id="828d4-173">Penceresi kapatıldığında `ASPNETCORE_ENVIRONMENT` ayarı varsayılan ayar veya bir makine değere döner.</span><span class="sxs-lookup"><span data-stu-id="828d4-173">When the window is closed, the `ASPNETCORE_ENVIRONMENT` setting reverts to the default setting or machine value.</span></span>

<span data-ttu-id="828d4-174">Değerini genel olarak Windows içinde ayarlamak için aşağıdaki yaklaşımlardan birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="828d4-174">To set the value globally in Windows, use either of the following approaches:</span></span>

* <span data-ttu-id="828d4-175">Açık **Denetim Masası** > **sistem** > **Gelişmiş Sistem ayarları** ve ekleme veya düzenleme `ASPNETCORE_ENVIRONMENT` değeri:</span><span class="sxs-lookup"><span data-stu-id="828d4-175">Open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value:</span></span>

  ![Sistem Gelişmiş özellikleri](environments/_static/systemsetting_environment.png)

  ![ASP.NET Core ortam değişkeni](environments/_static/windows_aspnetcore_environment.png)

* <span data-ttu-id="828d4-178">Bir yönetici komut istemi açın ve kullanmak `setx` komutu veya bir yönetici PowerShell komut istemi açın ve kullanmak `[Environment]::SetEnvironmentVariable`:</span><span class="sxs-lookup"><span data-stu-id="828d4-178">Open an administrative command prompt and use the `setx` command or open an administrative PowerShell command prompt and use `[Environment]::SetEnvironmentVariable`:</span></span>

  <span data-ttu-id="828d4-179">**Komut İstemi**</span><span class="sxs-lookup"><span data-stu-id="828d4-179">**Command prompt**</span></span>

  ```console
  setx ASPNETCORE_ENVIRONMENT Development /M
  ```

  <span data-ttu-id="828d4-180">`/M` Sistem düzeyinde ortam değişkenini ayarlamak için anahtar belirtir.</span><span class="sxs-lookup"><span data-stu-id="828d4-180">The `/M` switch indicates to set the environment variable at the system level.</span></span> <span data-ttu-id="828d4-181">Varsa `/M` anahtar kullanılmaz, kullanıcı hesabı için ortam değişkeni ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="828d4-181">If the `/M` switch isn't used, the environment variable is set for the user account.</span></span>

  <span data-ttu-id="828d4-182">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="828d4-182">**PowerShell**</span></span>

  ```powershell
  [Environment]::SetEnvironmentVariable("ASPNETCORE_ENVIRONMENT", "Development", "Machine")
  ```

  <span data-ttu-id="828d4-183">`Machine` Sistem düzeyinde ortam değişkenini ayarlamak için seçeneği değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="828d4-183">The `Machine` option value indicates to set the environment variable at the system level.</span></span> <span data-ttu-id="828d4-184">Seçenek değeri değiştirilirse `User`, kullanıcı hesabı için ortam değişkeni ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="828d4-184">If the option value is changed to `User`, the environment variable is set for the user account.</span></span>

<span data-ttu-id="828d4-185">Zaman `ASPNETCORE_ENVIRONMENT` ortam değişkeni genel olarak ayarlandığında, etkili olur `dotnet run` değer ayarlandıktan sonra herhangi bir komut penceresinde açılır.</span><span class="sxs-lookup"><span data-stu-id="828d4-185">When the `ASPNETCORE_ENVIRONMENT` environment variable is set globally, it takes effect for `dotnet run` in any command window opened after the value is set.</span></span>

<span data-ttu-id="828d4-186">**Web.config**</span><span class="sxs-lookup"><span data-stu-id="828d4-186">**web.config**</span></span>

<span data-ttu-id="828d4-187">Ayarlanacak `ASPNETCORE_ENVIRONMENT` ortam değişkeni ile *web.config*, bkz: *ortam değişkenlerini ayarlama* bölümünü <xref:host-and-deploy/aspnet-core-module#setting-environment-variables>.</span><span class="sxs-lookup"><span data-stu-id="828d4-187">To set the `ASPNETCORE_ENVIRONMENT` environment variable with *web.config*, see the *Setting environment variables* section of <xref:host-and-deploy/aspnet-core-module#setting-environment-variables>.</span></span> <span data-ttu-id="828d4-188">Zaman `ASPNETCORE_ENVIRONMENT` ile ortam değişkeninin ayarlı *web.config*, sistem düzeyindeki bir ayarı değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="828d4-188">When the `ASPNETCORE_ENVIRONMENT` environment variable is set with *web.config*, its value overrides a setting at the system level.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="828d4-189">**Proje dosyası veya yayımlama profili**</span><span class="sxs-lookup"><span data-stu-id="828d4-189">**Project file or publish profile**</span></span>

<span data-ttu-id="828d4-190">**Windows IIS dağıtımlar için:** Dahil `<EnvironmentName>` yayımlama profilini özelliğinde (*.pubxml*) ya da proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="828d4-190">**For Windows IIS deployments:** Include the `<EnvironmentName>` property in the publish profile (*.pubxml*) or project file.</span></span> <span data-ttu-id="828d4-191">Bu yaklaşım ortamı ayarlar *web.config* proje yayımlandığında ne zaman:</span><span class="sxs-lookup"><span data-stu-id="828d4-191">This approach sets the environment in *web.config* when the project is published:</span></span>

```xml
<PropertyGroup>
  <EnvironmentName>Development</EnvironmentName>
</PropertyGroup>
```

::: moniker-end

<span data-ttu-id="828d4-192">**IIS uygulama havuzu başına**</span><span class="sxs-lookup"><span data-stu-id="828d4-192">**Per IIS Application Pool**</span></span>

<span data-ttu-id="828d4-193">Ayarlanacak `ASPNETCORE_ENVIRONMENT` bir yalıtılmış uygulama (IIS 10.0 veya sonraki sürümlerde desteklenir) havuzunda, bkz: çalışan bir uygulama için ortam değişkenini *AppCmd.exe komut* bölümünü [ortam değişkenlerini &lt; environmentVariables&gt; ](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) konu.</span><span class="sxs-lookup"><span data-stu-id="828d4-193">To set the `ASPNETCORE_ENVIRONMENT` environment variable for an app running in an isolated Application Pool (supported on IIS 10.0 or later), see the *AppCmd.exe command* section of the [Environment Variables &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span> <span data-ttu-id="828d4-194">Zaman `ASPNETCORE_ENVIRONMENT` ortam değişkeni için bir uygulama havuzu ayarlandığında, sistem düzeyindeki bir ayarı değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="828d4-194">When the `ASPNETCORE_ENVIRONMENT` environment variable is set for an app pool, its value overrides a setting at the system level.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="828d4-195">IIS'de bir uygulamanın barındırma ve ekleme veya değiştirme `ASPNETCORE_ENVIRONMENT` aşağıdakilerden herhangi birini yaklaşıyor uygulamalar tarafından toplanmış yeni değerine sahip olacak şekilde ortam değişkeni kullanın:</span><span class="sxs-lookup"><span data-stu-id="828d4-195">When hosting an app in IIS and adding or changing the `ASPNETCORE_ENVIRONMENT` environment variable, use any one of the following approaches to have the new value picked up by apps:</span></span>
>
> * <span data-ttu-id="828d4-196">Yürütme `net stop was /y` ardından `net start w3svc` bir komut isteminden.</span><span class="sxs-lookup"><span data-stu-id="828d4-196">Execute `net stop was /y` followed by `net start w3svc` from a command prompt.</span></span>
> * <span data-ttu-id="828d4-197">Sunucuyu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="828d4-197">Restart the server.</span></span>

### <a name="macos"></a><span data-ttu-id="828d4-198">macOS</span><span class="sxs-lookup"><span data-stu-id="828d4-198">macOS</span></span>

<span data-ttu-id="828d4-199">MacOS olabilir geçerli ortamı ayarı satır içi uygulamayı çalıştırırken gerçekleştirmiştir:</span><span class="sxs-lookup"><span data-stu-id="828d4-199">Setting the current environment for macOS can be performed in-line when running the app:</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

<span data-ttu-id="828d4-200">Alternatif olarak, ortam kümesi `export` uygulamayı çalıştırmadan önce:</span><span class="sxs-lookup"><span data-stu-id="828d4-200">Alternatively, set the environment with `export` prior to running the app:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="828d4-201">Makine düzeyinde ortam değişkenlerini ayarlanır *.bashrc* veya *.bash_profile* dosya.</span><span class="sxs-lookup"><span data-stu-id="828d4-201">Machine-level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="828d4-202">Herhangi bir metin düzenleyicisi kullanarak dosyayı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="828d4-202">Edit the file using any text editor.</span></span> <span data-ttu-id="828d4-203">Aşağıdaki deyimi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="828d4-203">Add the following statement:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="828d4-204">Linux</span><span class="sxs-lookup"><span data-stu-id="828d4-204">Linux</span></span>

<span data-ttu-id="828d4-205">Linux dağıtımları için kullanmak `export` oturum tabanlı değişken ayarları için bir komut isteminde komutunu ve *bash_profile* makine düzeyinde ortam ayarları dosyası.</span><span class="sxs-lookup"><span data-stu-id="828d4-205">For Linux distros, use the `export` command at a command prompt for session-based variable settings and *bash_profile* file for machine-level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="828d4-206">Ortama göre yapılandırma</span><span class="sxs-lookup"><span data-stu-id="828d4-206">Configuration by environment</span></span>

<span data-ttu-id="828d4-207">Yapılandırma ortamı tarafından yüklenecek öneririz:</span><span class="sxs-lookup"><span data-stu-id="828d4-207">To load configuration by environment, we recommend:</span></span>

* <span data-ttu-id="828d4-208">*appSettings* dosyaları (\* appsettings.&lt; <Environment> &gt;.json).</span><span class="sxs-lookup"><span data-stu-id="828d4-208">*appsettings* files (\*appsettings.&lt;<Environment>&gt;.json).</span></span> <span data-ttu-id="828d4-209">Bkz: [yapılandırma: Dosya yapılandırma sağlayıcısı](xref:fundamentals/configuration/index#file-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="828d4-209">See [Configuration: File configuration provider](xref:fundamentals/configuration/index#file-configuration-provider).</span></span>
* <span data-ttu-id="828d4-210">ortam değişkenleri (her sisteminde uygulamanın barındırıldığı ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="828d4-210">environment variables (set on each system where the app is hosted).</span></span> <span data-ttu-id="828d4-211">Bkz: [yapılandırma: Dosya yapılandırma sağlayıcısı](xref:fundamentals/configuration/index#file-configuration-provider) ve [geliştirmede uygulama gizli anahtarlarının Güvenli Depolama: Ortam değişkenlerini](xref:security/app-secrets#environment-variables).</span><span class="sxs-lookup"><span data-stu-id="828d4-211">See [Configuration: File configuration provider](xref:fundamentals/configuration/index#file-configuration-provider) and [Safe storage of app secrets in development: Environment variables](xref:security/app-secrets#environment-variables).</span></span>
* <span data-ttu-id="828d4-212">Gizli dizi Yöneticisi (geliştirme ortamındaki yalnızca).</span><span class="sxs-lookup"><span data-stu-id="828d4-212">Secret Manager (in the Development environment only).</span></span> <span data-ttu-id="828d4-213">Bkz. <xref:security/app-secrets>.</span><span class="sxs-lookup"><span data-stu-id="828d4-213">See <xref:security/app-secrets>.</span></span>

## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="828d4-214">Ortam tabanlı başlangıç sınıfı ve yöntemleri</span><span class="sxs-lookup"><span data-stu-id="828d4-214">Environment-based Startup class and methods</span></span>

### <a name="startup-class-conventions"></a><span data-ttu-id="828d4-215">Başlangıç sınıfı kuralları</span><span class="sxs-lookup"><span data-stu-id="828d4-215">Startup class conventions</span></span>

<span data-ttu-id="828d4-216">ASP.NET Core uygulaması başladığında [başlangıç sınıfı](xref:fundamentals/startup) uygulama bootstraps.</span><span class="sxs-lookup"><span data-stu-id="828d4-216">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="828d4-217">Uygulamayı ayrı tanımlayabilirsiniz `Startup` sınıflar farklı ortamlar için (örneğin, `StartupDevelopment`) ve uygun `Startup` sınıfı, çalışma zamanında seçilidir.</span><span class="sxs-lookup"><span data-stu-id="828d4-217">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate `Startup` class is selected at runtime.</span></span> <span data-ttu-id="828d4-218">Geçerli ortamı olan adı sonekiyle sınıfı kurtarılmasına öncelik verilir.</span><span class="sxs-lookup"><span data-stu-id="828d4-218">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="828d4-219">Eşleşen bir `Startup{EnvironmentName}` sınıfı değil bulundu, `Startup` sınıfı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="828d4-219">If a matching `Startup{EnvironmentName}` class isn't found, the `Startup` class is used.</span></span>

<span data-ttu-id="828d4-220">Ortam tabanlı uygulamak için `Startup` sınıfları oluşturma bir `Startup{EnvironmentName}` her ortamda kullanın ve bir geri dönüş için sınıf `Startup` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="828d4-220">To implement environment-based `Startup` classes, create a `Startup{EnvironmentName}` class for each environment in use and a fallback `Startup` class:</span></span>

```csharp
// Startup class to use in the Development environment
public class StartupDevelopment
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}

// Startup class to use in the Production environment
public class StartupProduction
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}

// Fallback Startup class
// Selected if the environment doesn't match a Startup{EnvironmentName} class
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}
```

<span data-ttu-id="828d4-221">Kullanım [UseStartup (IWebHostBuilder, String)](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usestartup) bir derleme adı kabul eden aşırı yükleme:</span><span class="sxs-lookup"><span data-stu-id="828d4-221">Use the [UseStartup(IWebHostBuilder, String)](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usestartup) overload that accepts an assembly name:</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
public static void Main(string[] args)
{
    CreateWebHostBuilder(args).Build().Run();
}

public static IWebHostBuilder CreateWebHostBuilder(string[] args)
{
    var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

    return WebHost.CreateDefaultBuilder(args)
        .UseStartup(assemblyName);
}
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
public static void Main(string[] args)
{
    CreateWebHost(args).Run();
}

public static IWebHost CreateWebHost(string[] args)
{
    var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

    return WebHost.CreateDefaultBuilder(args)
        .UseStartup(assemblyName)
        .Build();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

        var host = new WebHostBuilder()
            .UseStartup(assemblyName)
            .Build();

        host.Run();
    }
}
```

::: moniker-end

### <a name="startup-method-conventions"></a><span data-ttu-id="828d4-222">Başlangıç yöntem kuralları</span><span class="sxs-lookup"><span data-stu-id="828d4-222">Startup method conventions</span></span>

<span data-ttu-id="828d4-223">[Yapılandırma](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) ve [Createservicereplicalisteners()](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) formun ortama özgü sürümlerini destekleyen `Configure<EnvironmentName>` ve `Configure<EnvironmentName>Services`:</span><span class="sxs-lookup"><span data-stu-id="828d4-223">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) support environment-specific versions of the form `Configure<EnvironmentName>` and `Configure<EnvironmentName>Services`:</span></span>

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet_all&highlight=15,51)]

## <a name="additional-resources"></a><span data-ttu-id="828d4-224">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="828d4-224">Additional resources</span></span>

* <xref:fundamentals/startup>
* <xref:fundamentals/configuration/index>
* [<span data-ttu-id="828d4-225">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="828d4-225">IHostingEnvironment.EnvironmentName</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)
