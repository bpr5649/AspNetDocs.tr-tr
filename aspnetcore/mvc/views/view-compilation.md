---
title: ASP.NET Core Razor dosyası derleme
author: rick-anderson
description: Razor dosyaları derleme içinde ASP.NET Core uygulaması nasıl gerçekleştirildiğini öğrenin.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: mvc/views/view-compilation
ms.openlocfilehash: 0b6173a7860f5f1d9d11219fbf3f57f76d703031
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069660"
---
# <a name="razor-file-compilation-in-aspnet-core"></a>ASP.NET Core Razor dosyası derleme

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="= aspnetcore-1.1"

İlişkili bir MVC görünümü çağrıldığında bir Razor dosya çalışma zamanında derlenir. Derleme zamanı Razor dosya yayımlama desteklenmiyor. Razor dosyaları isteğe bağlı olarak derlenmesi sırasında zaman yayımlama ve uygulama ile birlikte dağıtılan&mdash;ön derleme aracını kullanarak.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

İlişkili bir Razor sayfası veya MVC görünümü çağrıldığında bir Razor dosya çalışma zamanında derlenir. Derleme zamanı Razor dosya yayımlama desteklenmiyor. Razor dosyaları isteğe bağlı olarak derlenmesi sırasında zaman yayımlama ve uygulama ile birlikte dağıtılan&mdash;ön derleme aracını kullanarak.

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

İlişkili bir Razor sayfası veya MVC görünümü çağrıldığında bir Razor dosya çalışma zamanında derlenir. Razor dosyaları her iki yapı derlenir ve saat kullanarak yayımlama [Razor SDK](xref:razor-pages/sdk).

::: moniker-end

::: moniker range=">= aspnetcore-3.0"

Razor dosyaları her iki yapı derlenir ve saat kullanarak yayımlama [Razor SDK](xref:razor-pages/sdk). Çalışma zamanı derlemesi isteğe bağlı olarak, uygulamanızın yapılandırarak etkinleştirilebilir

::: moniker-end

## <a name="razor-compilation"></a>Razor derleme

::: moniker range=">= aspnetcore-3.0"
Razor dosyaları derleme ve yayımlama-zamanı derlemesini Razor SDK'sı tarafından varsayılan olarak etkindir. Etkinleştirildiğinde, çalışma zamanı derlemesi tamamlayıcı editied olmaları durumunda güncelleştirilecek Razor dosyaları izin vererek zamanında derleme oluşturacaksınız.

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

Razor dosyaları derleme ve yayımlama-zamanı derlemesini Razor SDK'sı tarafından varsayılan olarak etkindir. Bunlar güncelleştirdikten sonra Razor dosyaları düzenleme, derleme sırasında desteklenir. Varsayılan olarak, yalnızca derlenmiş *Views.dll* ve hiçbir *.cshtml* Razor dosyalarını derlemek için gerekli dosyaları veya başvuru derlemeleri, uygulamanızla birlikte dağıtılır.

> [!IMPORTANT]
> Ön derleme araç kullanım dışı bırakıldı ve ASP.NET Core 3. 0'kaldırılacak. Geçiş öneririz [Razor Sdk](xref:razor-pages/sdk).
>
> Yalnızca proje dosyasında hiçbir ön derleme özgü özellikler ayarlandığında Razor SDK'sı etkili olur. Örneğin, ayarı *.csproj* dosyanın `MvcRazorCompileOnPublish` özelliğini `true` Razor SDK'yı devre dışı bırakır.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

Projeniz .NET Framework hedefliyorsa, yükleme [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet paketi:

[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]

.NET Core projenizi olmasını istiyorsanız, hiçbir değişiklik gereklidir.

ASP.NET Core 2.x proje şablonları örtük olarak ayarlanır `MvcRazorCompileOnPublish` özelliğini `true` varsayılan olarak. Sonuç olarak, bu öğe güvenli bir şekilde alanından kaldırılabilir *.csproj* dosya.

> [!IMPORTANT]
> Ön derleme araç kullanım dışı bırakıldı ve ASP.NET Core 3. 0'kaldırılacak. Geçiş öneririz [Razor Sdk](xref:razor-pages/sdk).
>
> Razor dosyası ön derleme, gerçekleştirirken kullanılamıyorsa bir [müstakil dağıtım (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) ASP.NET Core 2.0.

::: moniker-end

::: moniker range="= aspnetcore-1.1"

Ayarlama `MvcRazorCompileOnPublish` özelliğini `true`, yükleyip [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet paketi. Aşağıdaki *.csproj* örnek bu ayarları vurgular:

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

Uygulama için hazırlama bir [framework bağımlı dağıtım](/dotnet/core/deploying/#framework-dependent-deployments-fdd) ile [.NET Core CLI komutu yayımlama](/dotnet/core/tools/dotnet-publish). Örneğin, proje kök dizinini aşağıdaki komutu yürütün:

```console
dotnet publish -c Release
```

A *< project_name >. PrecompiledViews.dll* derlenmiş Razor dosyalarını içeren dosya, bir ön derleme başarılı olduğunda oluşturulur. Örneğin, aşağıdaki ekran içeriğini gösterir *Index.cshtml* içinde *WebApplication1.PrecompiledViews.dll*:

![DLL içindeki Razor görünümleri](view-compilation/_static/razor-views-in-dll.png)

::: moniker-end

## <a name="runtime-compilation"></a>Çalışma zamanı derlemesi

::: moniker range="= aspnetcore-2.1"

Derleme zamanında derleme Razor dosyaları çalışma zamanı derlemesi tarafından desteklenir. ASP.NET Core MVC yeniden derleyin Razor ne zaman dosya içeriğini bir *.cshtml* dosya değişikliği.

::: moniker-end

::: moniker range="= aspnetcore-2.2"

Derleme zamanında derleme Razor dosyaları çalışma zamanı derlemesi tarafından desteklenir. <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions> <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> Razor dosyaları (Razor görünümleri ve Razor sayfaları) ve yeniden derlenen dosyalar diskte değiştirirseniz güncelleştirilmiş belirleyen bir değer alır veya ayarlar.

Varsayılan değer `true` için:

* Cihazın uyumluluk sürümü ayarlanırsa <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1> veya önceki sürümleri
* Cihazın uyumluluk sürümü çok kümesi ayarlanmış olup olmadığını <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_2> veya üzeri ve uygulama geliştirme ortamında <xref:Microsoft.AspNetCore.Hosting.HostingEnvironmentExtensions.IsDevelopment*>. Diğer bir deyişle, Razor dosyaları olmayan geliştirme ortamında sürece yeniden derlemeniz değil <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> açıkça ayarlayın.

Yönergeler ve cihazın uyumluluk sürümü ayarlama örnekleri için bkz. <xref:mvc/compatibility-version>.

::: moniker-end

::: moniker range=">= aspnetcore-3.0"

Çalışma zamanı derlemesi kullanarak etkin `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` paket. Çalışma zamanı derlemesi etkinleştirmek için uygulamaları gerekir.

* Yükleme [Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/) NuGet paketi.
* Uygulamanın güncelleştirme `ConfigureServices` çağrısı içerecek şekilde `AddMvcRazorRuntimeCompilation`:

```csharp
services
    .AddMvc()
    .AddMvcRazorRuntimeCompilation()
```

Çalışma zamanı derlemesi dağıtıldığında çalışacak şekilde ayarlamak için proje dosyaları ayrıca uygulamaları değiştirmelisiniz `PreserveCompilationReferences` için `true`.
[!code-xml[](view-compilation/sample/RuntimeCompilation.csproj?highlight=3)]

::: moniker-end

## <a name="additional-resources"></a>Ek kaynaklar

::: moniker range="= aspnetcore-1.1"

* <xref:mvc/views/overview>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>
* <xref:razor-pages/sdk>

::: moniker-end
