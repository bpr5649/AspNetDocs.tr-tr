---
title: ASP.NET Core MVC için ASP.NET MVC ' geçiş
author: ardalis
description: Bir ASP.NET MVC projesi için ASP.NET Core MVC geçişini kullanmaya nasıl başlayacağınızı öğrenin.
ms.author: riande
ms.date: 02/13/2019
uid: migration/mvc
ms.openlocfilehash: 2ca51a145243444722ad8081fd8cdbb65d72b53a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074268"
---
# <a name="migrate-from-aspnet-mvc-to-aspnet-core-mvc"></a><span data-ttu-id="b33c6-103">ASP.NET Core MVC için ASP.NET MVC ' geçiş</span><span class="sxs-lookup"><span data-stu-id="b33c6-103">Migrate from ASP.NET MVC to ASP.NET Core MVC</span></span>

<span data-ttu-id="b33c6-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), [Steve Smith](https://ardalis.com/), ve [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="b33c6-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), [Steve Smith](https://ardalis.com/), and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="b33c6-105">Bu makalede, bir ASP.NET MVC projesini geçişini kullanmaya başlamak gösterilmektedir [ASP.NET Core MVC](../mvc/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b33c6-105">This article shows how to get started migrating an ASP.NET MVC project to [ASP.NET Core MVC](../mvc/overview.md).</span></span> <span data-ttu-id="b33c6-106">İşlem sırasında ASP.NET MVC değişmiş olan şeyleri çoğunu vurgulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-106">In the process, it highlights many of the things that have changed from ASP.NET MVC.</span></span> <span data-ttu-id="b33c6-107">Birden çok adımlı bir işlemin, ASP.NET MVC ' geçişi ve bu makalede, ilk Kurulum, temel denetleyicileri ve görünümleri, statik içerik ve istemci tarafı bağımlılıkları yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-107">Migrating from ASP.NET MVC is a multiple step process and this article covers the initial setup, basic controllers and views, static content, and client-side dependencies.</span></span> <span data-ttu-id="b33c6-108">Diğer makaleler geçirme yapılandırma ve birçok ASP.NET MVC projesinde bulunan bir kimlik kodu kapsar.</span><span class="sxs-lookup"><span data-stu-id="b33c6-108">Additional articles cover migrating configuration and identity code found in many ASP.NET MVC projects.</span></span>

> [!NOTE]
> <span data-ttu-id="b33c6-109">Sürüm numaraları örneklerdeki geçerli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-109">The version numbers in the samples might not be current.</span></span> <span data-ttu-id="b33c6-110">Projelerinizi uygun şekilde güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-110">You may need to update your projects accordingly.</span></span>

## <a name="create-the-starter-aspnet-mvc-project"></a><span data-ttu-id="b33c6-111">Başlangıç ASP.NET MVC projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b33c6-111">Create the starter ASP.NET MVC project</span></span>

<span data-ttu-id="b33c6-112">Yükseltme göstermek için bir ASP.NET MVC uygulaması oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="b33c6-112">To demonstrate the upgrade, we'll start by creating a ASP.NET MVC app.</span></span> <span data-ttu-id="b33c6-113">Adlı oluşturun *WebApp1* ad sonraki adımda oluşturacağız ASP.NET Core projesi eşleşecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="b33c6-113">Create it with the name *WebApp1* so the namespace matches the ASP.NET Core project we create in the next step.</span></span>

![Visual Studio yeni proje iletişim kutusu](mvc/_static/new-project.png)

![Yeni Web uygulaması iletişim kutusu: ASP.NET şablonları panelinde seçili MVC proje şablonu](mvc/_static/new-project-select-mvc-template.png)

<span data-ttu-id="b33c6-116">*İsteğe bağlı:* Çözüm adını değiştirmek *WebApp1* için *Mvc5*.</span><span class="sxs-lookup"><span data-stu-id="b33c6-116">*Optional:* Change the name of the Solution from *WebApp1* to *Mvc5*.</span></span> <span data-ttu-id="b33c6-117">Visual Studio yeni çözüm adını görüntüler (*Mvc5*), kolaylaştırır bu projeyi bir sonraki projenizde söylemek.</span><span class="sxs-lookup"><span data-stu-id="b33c6-117">Visual Studio displays the new solution name (*Mvc5*), which makes it easier to tell this project from the next project.</span></span>

## <a name="create-the-aspnet-core-project"></a><span data-ttu-id="b33c6-118">ASP.NET Core projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b33c6-118">Create the ASP.NET Core project</span></span>

<span data-ttu-id="b33c6-119">Yeni bir *boş* önceki projeyle aynı ada sahip bir ASP.NET Core web uygulaması (*WebApp1*) iki proje alanlarında eşleşecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="b33c6-119">Create a new *empty* ASP.NET Core web app with the same name as the previous project (*WebApp1*) so the namespaces in the two projects match.</span></span> <span data-ttu-id="b33c6-120">Aynı ad alanına sahip iki proje arasında kod kopyalamak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-120">Having the same namespace makes it easier to copy code between the two projects.</span></span> <span data-ttu-id="b33c6-121">Aynı adı kullanmak için önceki projeyi farklı bir dizine içinde bu proje oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-121">You'll have to create this project in a different directory than the previous project to use the same name.</span></span>

![Yeni Proje iletişim kutusu](mvc/_static/new_core.png)

![Yeni ASP.NET Web uygulaması iletişim kutusu: ASP.NET Core şablonları panelinde seçili boş proje şablonu](mvc/_static/new-project-select-empty-aspnet5-template.png)

* <span data-ttu-id="b33c6-124">*İsteğe bağlı:* Yeni bir ASP.NET Core uygulamasını kullanarak oluşturma *Web uygulaması* proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="b33c6-124">*Optional:* Create a new ASP.NET Core app using the *Web Application* project template.</span></span> <span data-ttu-id="b33c6-125">Projeyi adlandırın *WebApp1*ve bir kimlik doğrulama seçeneği işaretleyin **bireysel kullanıcı hesapları**.</span><span class="sxs-lookup"><span data-stu-id="b33c6-125">Name the project *WebApp1*, and select an authentication option of **Individual User Accounts**.</span></span> <span data-ttu-id="b33c6-126">Bu uygulamayı yeniden adlandır *FullAspNetCore*.</span><span class="sxs-lookup"><span data-stu-id="b33c6-126">Rename this app to *FullAspNetCore*.</span></span> <span data-ttu-id="b33c6-127">Size zaman kazandırır proje dönüştürme oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="b33c6-127">Creating this project saves you time in the conversion.</span></span> <span data-ttu-id="b33c6-128">Şablon tarafından oluşturulan kodu sonuç görmek için veya dönüştürme projeye kodu kopyalamak göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-128">You can look at the template-generated code to see the end result or to copy code to the conversion project.</span></span> <span data-ttu-id="b33c6-129">Şablon tarafından oluşturulan proje ile karşılaştırılacak bir dönüştürme adımında takılı kalarak olduğunda da yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-129">It's also helpful when you get stuck on a conversion step to compare with the template-generated project.</span></span>

## <a name="configure-the-site-to-use-mvc"></a><span data-ttu-id="b33c6-130">Siteyi MVC kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b33c6-130">Configure the site to use MVC</span></span>

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="b33c6-131">.NET Core hedeflenirken [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) varsayılan olarak başvurulur.</span><span class="sxs-lookup"><span data-stu-id="b33c6-131">When targeting .NET Core, the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) is referenced by default.</span></span> <span data-ttu-id="b33c6-132">Bu paket, MVC uygulamaları tarafından yaygın olarak kullanılan paketler paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-132">This package contains packages commonly used packages by MVC apps.</span></span> <span data-ttu-id="b33c6-133">.NET Framework'ü hedefleyen, paket başvuruları ayrı ayrı proje dosyasında listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-133">If targeting .NET Framework, package references must be listed individually in the project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <span data-ttu-id="b33c6-134">.NET Core hedeflenirken [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) varsayılan olarak başvurulur.</span><span class="sxs-lookup"><span data-stu-id="b33c6-134">When targeting .NET Core, the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) is referenced by default.</span></span> <span data-ttu-id="b33c6-135">Bu paket, MVC uygulamaları tarafından yaygın olarak kullanılan paketler paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-135">This package contains packages commonly used packages by MVC apps.</span></span> <span data-ttu-id="b33c6-136">.NET Framework'ü hedefleyen, paket başvuruları ayrı ayrı proje dosyasında listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-136">If targeting .NET Framework, package references must be listed individually in the project file.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

* <span data-ttu-id="b33c6-137">.NET Core veya .NET Framework hedefleme, MVC uygulamaları tarafından yaygın olarak kullanılan paketler paketlerini ayrı ayrı proje dosyasında listelenir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-137">When targeting .NET Core or .NET Framework, packages commonly used packages by MVC apps are listed individually in the project file.</span></span>

::: moniker-end

<span data-ttu-id="b33c6-138">`Microsoft.AspNetCore.Mvc` ASP.NET Core MVC çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-138">`Microsoft.AspNetCore.Mvc` is the ASP.NET Core MVC framework.</span></span> <span data-ttu-id="b33c6-139">`Microsoft.AspNetCore.StaticFiles` statik dosya işleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-139">`Microsoft.AspNetCore.StaticFiles` is the static file handler.</span></span> <span data-ttu-id="b33c6-140">ASP.NET Core çalışma zamanı, modüler ve siz açıkça statik dosyaları işleme kabul etmek gerekir (bkz [statik dosyalar](xref:fundamentals/static-files)).</span><span class="sxs-lookup"><span data-stu-id="b33c6-140">The ASP.NET Core runtime is modular, and you must explicitly opt in to serve static files (see [Static files](xref:fundamentals/static-files)).</span></span>

* <span data-ttu-id="b33c6-141">Açık *Startup.cs* dosya ve kodu aşağıdaki ile eşleşecek şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b33c6-141">Open the *Startup.cs* file and change the code to match the following:</span></span>

  [!code-csharp[](mvc/sample/Startup.cs?highlight=13,26-31)]

<span data-ttu-id="b33c6-142">`UseStaticFiles` Genişletme yöntemi statik dosya işleyicisi ekler.</span><span class="sxs-lookup"><span data-stu-id="b33c6-142">The `UseStaticFiles` extension method adds the static file handler.</span></span> <span data-ttu-id="b33c6-143">Daha önce belirtildiği gibi ASP.NET çalışma zamanı modüler ve siz açıkça statik dosyaları işleme kabul etmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-143">As mentioned previously, the ASP.NET runtime is modular, and you must explicitly opt in to serve static files.</span></span> <span data-ttu-id="b33c6-144">`UseMvc` Uzantı yöntemi, yönlendirme ekler.</span><span class="sxs-lookup"><span data-stu-id="b33c6-144">The `UseMvc` extension method adds routing.</span></span> <span data-ttu-id="b33c6-145">Daha fazla bilgi için [uygulama başlatma](xref:fundamentals/startup) ve [yönlendirme](xref:fundamentals/routing).</span><span class="sxs-lookup"><span data-stu-id="b33c6-145">For more information, see [Application Startup](xref:fundamentals/startup) and [Routing](xref:fundamentals/routing).</span></span>

## <a name="add-a-controller-and-view"></a><span data-ttu-id="b33c6-146">Bir denetleyici ve Görünüm Ekle</span><span class="sxs-lookup"><span data-stu-id="b33c6-146">Add a controller and view</span></span>

<span data-ttu-id="b33c6-147">Bu bölümde, bir en az bir denetleyici ve ASP.NET MVC denetleyicisi için yer tutucu olarak görev yapacak görünümü ve sonraki bölümde geçiş görünümü ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-147">In this section, you'll add a minimal controller and view to serve as placeholders for the ASP.NET MVC controller and views you'll migrate in the next section.</span></span>

* <span data-ttu-id="b33c6-148">Ekleme bir *denetleyicileri* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-148">Add a *Controllers* folder.</span></span>

* <span data-ttu-id="b33c6-149">Ekleme bir **denetleyici sınıfı** adlı *HomeController.cs* için *denetleyicileri* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-149">Add a **Controller Class** named *HomeController.cs* to the *Controllers* folder.</span></span>

![Yeni öğe iletişim kutusu Ekle](mvc/_static/add_mvc_ctl.png)

* <span data-ttu-id="b33c6-151">Ekleme bir *görünümleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-151">Add a *Views* folder.</span></span>

* <span data-ttu-id="b33c6-152">Ekleme bir *görünümler/giriş* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-152">Add a *Views/Home* folder.</span></span>

* <span data-ttu-id="b33c6-153">Ekleme bir **Razor Görünüm** adlı *Index.cshtml* için *görünümler/giriş* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-153">Add a **Razor View** named *Index.cshtml* to the *Views/Home* folder.</span></span>

![Yeni öğe iletişim kutusu Ekle](mvc/_static/view.png)

<span data-ttu-id="b33c6-155">Proje yapısını aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b33c6-155">The project structure is shown below:</span></span>

![Dosya ve klasörleri WebApp1 gösteren Çözüm Gezgini](mvc/_static/project-structure-controller-view.png)

<span data-ttu-id="b33c6-157">Öğesinin içeriğini değiştirin *Views/Home/Index.cshtml* aşağıdaki dosya:</span><span class="sxs-lookup"><span data-stu-id="b33c6-157">Replace the contents of the *Views/Home/Index.cshtml* file with the following:</span></span>

```html
<h1>Hello world!</h1>
```

<span data-ttu-id="b33c6-158">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b33c6-158">Run the app.</span></span>

![Microsoft Edge'de açık Web uygulaması](mvc/_static/hello-world.png)

<span data-ttu-id="b33c6-160">Bkz: [denetleyicileri](xref:mvc/controllers/actions) ve [görünümleri](xref:mvc/views/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b33c6-160">See [Controllers](xref:mvc/controllers/actions) and [Views](xref:mvc/views/overview) for more information.</span></span>

<span data-ttu-id="b33c6-161">En az bir çalışan ASP.NET Core projesi sahibiz, biz işlevselliği ASP.NET MVC projeden geçiş başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-161">Now that we have a minimal working ASP.NET Core project, we can start migrating functionality from the ASP.NET MVC project.</span></span> <span data-ttu-id="b33c6-162">Aşağıdaki taşımanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b33c6-162">We need to move the following:</span></span>

* <span data-ttu-id="b33c6-163">istemci tarafı içeriği (CSS, yazı tipleri ve betikler)</span><span class="sxs-lookup"><span data-stu-id="b33c6-163">client-side content (CSS, fonts, and scripts)</span></span>

* <span data-ttu-id="b33c6-164">denetleyiciler</span><span class="sxs-lookup"><span data-stu-id="b33c6-164">controllers</span></span>

* <span data-ttu-id="b33c6-165">görünümler</span><span class="sxs-lookup"><span data-stu-id="b33c6-165">views</span></span>

* <span data-ttu-id="b33c6-166">modeller</span><span class="sxs-lookup"><span data-stu-id="b33c6-166">models</span></span>

* <span data-ttu-id="b33c6-167">Paketleme</span><span class="sxs-lookup"><span data-stu-id="b33c6-167">bundling</span></span>

* <span data-ttu-id="b33c6-168">filtreler</span><span class="sxs-lookup"><span data-stu-id="b33c6-168">filters</span></span>

* <span data-ttu-id="b33c6-169">Giren/çıkan günlüğü, kimlik (Bu, sonraki öğreticide gerçekleştirilir.)</span><span class="sxs-lookup"><span data-stu-id="b33c6-169">Log in/out, Identity (This is done in the next tutorial.)</span></span>

## <a name="controllers-and-views"></a><span data-ttu-id="b33c6-170">Denetleyicileri ve görünümleri</span><span class="sxs-lookup"><span data-stu-id="b33c6-170">Controllers and views</span></span>

* <span data-ttu-id="b33c6-171">ASP.NET MVC yöntemlerinin her birini kopyalayın `HomeController` yeni `HomeController`.</span><span class="sxs-lookup"><span data-stu-id="b33c6-171">Copy each of the methods from the ASP.NET MVC `HomeController` to the new `HomeController`.</span></span> <span data-ttu-id="b33c6-172">ASP.NET MVC'de yerleşik şablonun denetleyici eylem yöntemi dönüş türü olduğunu unutmayın [actionresult öğesini](https://msdn.microsoft.com/library/system.web.mvc.actionresult(v=vs.118).aspx); ASP.NET Core MVC, eylem yöntemleri dönüş `IActionResult` yerine.</span><span class="sxs-lookup"><span data-stu-id="b33c6-172">Note that in ASP.NET MVC, the built-in template's controller action method return type is [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult(v=vs.118).aspx); in ASP.NET Core MVC, the action methods return `IActionResult` instead.</span></span> <span data-ttu-id="b33c6-173">`ActionResult` uygulayan `IActionResult`var. Bu nedenle, eylem yöntemleri dönüş türünü değiştirmenize gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="b33c6-173">`ActionResult` implements `IActionResult`, so there's no need to change the return type of your action methods.</span></span>

* <span data-ttu-id="b33c6-174">Kopyalama *About.cshtml*, *Contact.cshtml*, ve *Index.cshtml* ASP.NET MVC projesi Razor görünüm dosyaları ASP.NET Core projesi.</span><span class="sxs-lookup"><span data-stu-id="b33c6-174">Copy the *About.cshtml*, *Contact.cshtml*, and *Index.cshtml* Razor view files from the ASP.NET MVC project to the ASP.NET Core project.</span></span>

* <span data-ttu-id="b33c6-175">ASP.NET Core uygulaması çalıştırın ve her yöntem test edin.</span><span class="sxs-lookup"><span data-stu-id="b33c6-175">Run the ASP.NET Core app and test each method.</span></span> <span data-ttu-id="b33c6-176">İşlenmiş görünümler yalnızca görünümü dosya içeriklerinde içerir, böylece biz Düzen dosyası ya da stilleri henüz geçişi henüz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-176">We haven't migrated the layout file or styles yet, so the rendered views only contain the content in the view files.</span></span> <span data-ttu-id="b33c6-177">Düzen oluşturulan dosya bağlantılarını olmaz `About` ve `Contact` görünümleri tarayıcıdan çağrılacak gerekir (Değiştir **4492** projenizde kullanılan bağlantı noktası numarası ile).</span><span class="sxs-lookup"><span data-stu-id="b33c6-177">You won't have the layout file generated links for the `About` and `Contact` views, so you'll have to invoke them from the browser (replace **4492** with the port number used in your project).</span></span>

  * `http://localhost:4492/home/about`

  * `http://localhost:4492/home/contact`

![Kişi sayfası](mvc/_static/contact-page.png)

<span data-ttu-id="b33c6-179">Stil ve menü öğeleri eksikliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b33c6-179">Note the lack of styling and menu items.</span></span> <span data-ttu-id="b33c6-180">Sonraki bölümde, gidereceğiz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-180">We'll fix that in the next section.</span></span>

## <a name="static-content"></a><span data-ttu-id="b33c6-181">Statik içerik</span><span class="sxs-lookup"><span data-stu-id="b33c6-181">Static content</span></span>

<span data-ttu-id="b33c6-182">ASP.NET MVC önceki sürümlerinde, statik içerik web projesinin kökünden barındırılan ve sunucu tarafı dosyaları ile karıştırılmış,.</span><span class="sxs-lookup"><span data-stu-id="b33c6-182">In previous versions of ASP.NET MVC, static content was hosted from the root of the web project and was intermixed with server-side files.</span></span> <span data-ttu-id="b33c6-183">ASP.NET Core, statik içerik içinde barındırılan *wwwroot* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-183">In ASP.NET Core, static content is hosted in the *wwwroot* folder.</span></span> <span data-ttu-id="b33c6-184">Eski ASP.NET MVC uygulamanıza statik içeriği kopyalamak istersiniz *wwwroot* ASP.NET Core proje klasöründe.</span><span class="sxs-lookup"><span data-stu-id="b33c6-184">You'll want to copy the static content from your old ASP.NET MVC app to the *wwwroot* folder in your ASP.NET Core project.</span></span> <span data-ttu-id="b33c6-185">Bu örnek dönüştürme:</span><span class="sxs-lookup"><span data-stu-id="b33c6-185">In this sample conversion:</span></span>

* <span data-ttu-id="b33c6-186">Kopyalama *favicon.ico* eski MVC projesini dosyasından *wwwroot* ASP.NET Core projesi klasöründe.</span><span class="sxs-lookup"><span data-stu-id="b33c6-186">Copy the *favicon.ico* file from the old MVC project to the *wwwroot* folder in the ASP.NET Core project.</span></span>

<span data-ttu-id="b33c6-187">ASP.NET MVC eski proje kullandığı [önyükleme](https://getbootstrap.com/) önyükleme dosyaları, stil ve depoları *içerik* ve *betikleri* klasörleri.</span><span class="sxs-lookup"><span data-stu-id="b33c6-187">The old ASP.NET MVC project uses [Bootstrap](https://getbootstrap.com/) for its styling and stores the Bootstrap files in the *Content* and *Scripts* folders.</span></span> <span data-ttu-id="b33c6-188">Eski ASP.NET MVC projesi oluşturulan şablonu Düzen dosyası içinde önyükleme başvuruyor (*Views/Shared/_Layout.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b33c6-188">The template, which generated the old ASP.NET MVC project, references Bootstrap in the layout file (*Views/Shared/_Layout.cshtml*).</span></span> <span data-ttu-id="b33c6-189">Konumuna yüklenemedi *bootstrap.js* ve *bootstrap.css* ASP.NET MVC dosyalarından proje için *wwwroot* klasöründe yeni bir proje.</span><span class="sxs-lookup"><span data-stu-id="b33c6-189">You could copy the *bootstrap.js* and *bootstrap.css* files from the ASP.NET MVC project to the *wwwroot* folder in the new project.</span></span> <span data-ttu-id="b33c6-190">Sonraki bölümde CDN'ler kullanarak Bootstrap için destek (ve diğer istemci tarafı kitaplıkları) bunun yerine, ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-190">Instead, we'll add support for Bootstrap (and other client-side libraries) using CDNs in the next section.</span></span>

## <a name="migrate-the-layout-file"></a><span data-ttu-id="b33c6-191">Düzen dosyası geçirme</span><span class="sxs-lookup"><span data-stu-id="b33c6-191">Migrate the layout file</span></span>

* <span data-ttu-id="b33c6-192">Kopyalama *_ViewStart.cshtml* eski ASP.NET MVC proje dosyasından *görünümleri* ASP.NET Core proje klasörüne *görünümleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-192">Copy the *_ViewStart.cshtml* file from the old ASP.NET MVC project's *Views* folder into the ASP.NET Core project's *Views* folder.</span></span> <span data-ttu-id="b33c6-193">*_ViewStart.cshtml* dosya içinde ASP.NET Core MVC değişmemiştir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-193">The *_ViewStart.cshtml* file has not changed in ASP.NET Core MVC.</span></span>

* <span data-ttu-id="b33c6-194">Oluşturma bir *görünümler/paylaşılan* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-194">Create a *Views/Shared* folder.</span></span>

* <span data-ttu-id="b33c6-195">*İsteğe bağlı:* Kopyalama *_viewımports.cshtml* gelen *FullAspNetCore* MVC projenin *görünümleri* ASP.NET Core proje klasörüne *görünümleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-195">*Optional:* Copy *_ViewImports.cshtml* from the *FullAspNetCore* MVC project's *Views* folder into the ASP.NET Core project's *Views* folder.</span></span> <span data-ttu-id="b33c6-196">Herhangi bir ad alanı bildiriminde kaldırmak *_viewımports.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="b33c6-196">Remove any namespace declaration in the *_ViewImports.cshtml* file.</span></span> <span data-ttu-id="b33c6-197">*_Viewımports.cshtml* dosya ad alanları için tüm görünüm dosyaları sağlar ve getirdiği [etiket Yardımcıları](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="b33c6-197">The *_ViewImports.cshtml* file provides namespaces for all the view files and brings in [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span> <span data-ttu-id="b33c6-198">Etiket Yardımcıları yeni bir düzen dosyasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-198">Tag Helpers are used in the new layout file.</span></span> <span data-ttu-id="b33c6-199">*_Viewımports.cshtml* dosya ASP.NET Core için yenidir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-199">The *_ViewImports.cshtml* file is new for ASP.NET Core.</span></span>

* <span data-ttu-id="b33c6-200">Kopyalama *_Layout.cshtml* eski ASP.NET MVC proje dosyasından *görünümler/paylaşılan* ASP.NET Core proje klasörüne *görünümler/paylaşılan* klasör.</span><span class="sxs-lookup"><span data-stu-id="b33c6-200">Copy the *_Layout.cshtml* file from the old ASP.NET MVC project's *Views/Shared* folder into the ASP.NET Core project's *Views/Shared* folder.</span></span>

<span data-ttu-id="b33c6-201">Açık *_Layout.cshtml* dosya ve (tamamlanan kodu aşağıda gösterilmektedir) aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="b33c6-201">Open *_Layout.cshtml* file and make the following changes (the completed code is shown below):</span></span>

* <span data-ttu-id="b33c6-202">Değiştirin `@Styles.Render("~/Content/css")` ile bir `<link>` yüklenecek öğe *bootstrap.css* (aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="b33c6-202">Replace `@Styles.Render("~/Content/css")` with a `<link>` element to load *bootstrap.css* (see below).</span></span>

* <span data-ttu-id="b33c6-203">Kaldırma `@Scripts.Render("~/bundles/modernizr")`.</span><span class="sxs-lookup"><span data-stu-id="b33c6-203">Remove `@Scripts.Render("~/bundles/modernizr")`.</span></span>

* <span data-ttu-id="b33c6-204">Açıklama `@Html.Partial("_LoginPartial")` satır (satırla çevreleyen `@*...*@`).</span><span class="sxs-lookup"><span data-stu-id="b33c6-204">Comment out the `@Html.Partial("_LoginPartial")` line (surround the line with `@*...*@`).</span></span> <span data-ttu-id="b33c6-205">Daha fazla bilgi için [geçirme kimlik doğrulaması ve kimlik için ASP.NET Core](xref:migration/identity)</span><span class="sxs-lookup"><span data-stu-id="b33c6-205">For more information see [Migrate Authentication and Identity to ASP.NET Core](xref:migration/identity)</span></span>

* <span data-ttu-id="b33c6-206">Değiştirin `@Scripts.Render("~/bundles/jquery")` ile bir `<script>` öğesi (aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="b33c6-206">Replace `@Scripts.Render("~/bundles/jquery")` with a `<script>` element (see below).</span></span>

* <span data-ttu-id="b33c6-207">Değiştirin `@Scripts.Render("~/bundles/bootstrap")` ile bir `<script>` öğesi (aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="b33c6-207">Replace `@Scripts.Render("~/bundles/bootstrap")` with a `<script>` element (see below).</span></span>

<span data-ttu-id="b33c6-208">Değiştirme biçimlendirme önyükleme CSS eklemek için:</span><span class="sxs-lookup"><span data-stu-id="b33c6-208">The replacement markup for Bootstrap CSS inclusion:</span></span>

```html
<link rel="stylesheet"
    href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
    integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u"
    crossorigin="anonymous">
```

<span data-ttu-id="b33c6-209">JQuery ve önyükleme JavaScript ekleme için değiştirme biçimlendirme:</span><span class="sxs-lookup"><span data-stu-id="b33c6-209">The replacement markup for jQuery and Bootstrap JavaScript inclusion:</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"
    integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
```

<span data-ttu-id="b33c6-210">Güncelleştirilmiş *_Layout.cshtml* dosya aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b33c6-210">The updated *_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[](mvc/sample/Views/Shared/_Layout.cshtml?highlight=7-10,29,41-44)]

<span data-ttu-id="b33c6-211">Site tarayıcıda görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="b33c6-211">View the site in the browser.</span></span> <span data-ttu-id="b33c6-212">Bunu artık doğru yerde beklenen stilleri ile yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-212">It should now load correctly, with the expected styles in place.</span></span>

* <span data-ttu-id="b33c6-213">*İsteğe bağlı:* Yeni düzen dosyası kullanarak denemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b33c6-213">*Optional:* You might want to try using the new layout file.</span></span> <span data-ttu-id="b33c6-214">Bu proje için Düzen dosyasından kopyalayabilirsiniz *FullAspNetCore* proje.</span><span class="sxs-lookup"><span data-stu-id="b33c6-214">For this project you can copy the layout file from the *FullAspNetCore* project.</span></span> <span data-ttu-id="b33c6-215">Yeni düzen dosyası kullanan [etiket Yardımcıları](xref:mvc/views/tag-helpers/intro) ve diğer iyileştirmeler yapılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-215">The new layout file uses [Tag Helpers](xref:mvc/views/tag-helpers/intro) and has other improvements.</span></span>

## <a name="configure-bundling-and-minification"></a><span data-ttu-id="b33c6-216">Paketleme ve küçültme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b33c6-216">Configure bundling and minification</span></span>

<span data-ttu-id="b33c6-217">Paketleme ve küçültme yapılandırma hakkında daha fazla bilgi için bkz: [paketleme ve küçültme](../client-side/bundling-and-minification.md).</span><span class="sxs-lookup"><span data-stu-id="b33c6-217">For information about how to configure bundling and minification, see [Bundling and Minification](../client-side/bundling-and-minification.md).</span></span>

## <a name="solve-http-500-errors"></a><span data-ttu-id="b33c6-218">HTTP 500 hataları çözün</span><span class="sxs-lookup"><span data-stu-id="b33c6-218">Solve HTTP 500 errors</span></span>

<span data-ttu-id="b33c6-219">Sorunun kaynağını hakkında hiçbir bilgi içeren bir HTTP 500 hata iletisini neden olabilecek çok sayıda sorunları vardır.</span><span class="sxs-lookup"><span data-stu-id="b33c6-219">There are many problems that can cause a HTTP 500 error message that contain no information on the source of the problem.</span></span> <span data-ttu-id="b33c6-220">Örneğin, varsa *Views/_ViewImports.cshtml* dosya içeriyorsa, projede mevcut bir ad alanı, bir HTTP 500 hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b33c6-220">For example, if the *Views/_ViewImports.cshtml* file contains a namespace that doesn't exist in your project, you'll get a HTTP 500 error.</span></span> <span data-ttu-id="b33c6-221">Varsayılan olarak, ASP.NET Core uygulamalarında `UseDeveloperExceptionPage` uzantısı eklenmiş `IApplicationBuilder` ve yapılandırma olduğunda yürütülen *geliştirme*.</span><span class="sxs-lookup"><span data-stu-id="b33c6-221">By default in ASP.NET Core apps, the `UseDeveloperExceptionPage` extension is added to the `IApplicationBuilder` and executed when the configuration is *Development*.</span></span> <span data-ttu-id="b33c6-222">Bu aşağıdaki kodda ayrıntılı olarak verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b33c6-222">This is detailed in the following code:</span></span>

[!code-csharp[](mvc/sample/Startup.cs?highlight=19-22)]

<span data-ttu-id="b33c6-223">ASP.NET Core web uygulamasında işlenmeyen özel durumları HTTP 500 hata yanıtları dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="b33c6-223">ASP.NET Core converts unhandled exceptions in a web app into HTTP 500 error responses.</span></span> <span data-ttu-id="b33c6-224">Normalde, hata ayrıntıları sunucu ile ilgili potansiyel olarak hassas bilgilerin açığa çıkmasını önlemek için bu yanıtları dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="b33c6-224">Normally, error details aren't included in these responses to prevent disclosure of potentially sensitive information about the server.</span></span> <span data-ttu-id="b33c6-225">Bkz: **Geliştirici özel durumu sayfasını kullanarak** içinde [hataları işlemek](../fundamentals/error-handling.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b33c6-225">See **Using the Developer Exception Page** in [Handle errors](../fundamentals/error-handling.md) for more information.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b33c6-226">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b33c6-226">Additional resources</span></span>

* <xref:razor-components/index>
* <xref:mvc/views/tag-helpers/intro>
