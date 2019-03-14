---
title: ASP.NET Core Razor sayfalar giriş
author: Rick-Anderson
description: Nasıl ASP.NET Core Razor sayfalar kodlama sayfa odaklı senaryolar daha kolay ve MVC kullanmaktan daha üretken hale getirdiğini öğrenin.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/12/2018
uid: razor-pages/index
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="c504b-103">ASP.NET Core Razor sayfalar giriş</span><span class="sxs-lookup"><span data-stu-id="c504b-103">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="c504b-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT) ve [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="c504b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="c504b-105">Razor sayfaları, ASP.NET Core MVC sayfası odaklı senaryolar daha kolay ve daha üretken kodlama sağlayan yeni bir yönü olur.</span><span class="sxs-lookup"><span data-stu-id="c504b-105">Razor Pages is a new aspect of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="c504b-106">Model-View-Controller yaklaşım kullanan bir öğretici için arıyorsanız bkz [ASP.NET Core MVC ile çalışmaya başlama](xref:tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="c504b-106">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Get started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="c504b-107">Bu belge, Razor sayfaları için bir giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="c504b-107">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="c504b-108">Bir adım adım öğretici değil.</span><span class="sxs-lookup"><span data-stu-id="c504b-108">It's not a step by step tutorial.</span></span> <span data-ttu-id="c504b-109">Bazı bölümlerinin çok Gelişmiş bulma olmadığını [Razor sayfaları kullanmaya başlama](xref:tutorials/razor-pages/razor-pages-start).</span><span class="sxs-lookup"><span data-stu-id="c504b-109">If you find some of the sections too advanced, see [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="c504b-110">ASP.NET Core genel bakış için bkz. [ASP.NET Core'a giriş](xref:index).</span><span class="sxs-lookup"><span data-stu-id="c504b-110">For an overview of ASP.NET Core, see the [Introduction to ASP.NET Core](xref:index).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c504b-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c504b-111">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

<a name="rpvs17"></a>

## <a name="create-a-razor-pages-project"></a><span data-ttu-id="c504b-112">Razor sayfaları proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="c504b-112">Create a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="c504b-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c504b-113">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="c504b-114">Bkz: [Razor sayfaları kullanmaya başlama](xref:tutorials/razor-pages/razor-pages-start) Razor sayfaları proje oluşturma konusunda ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="c504b-114">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="c504b-115">Mac için Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c504b-115">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="c504b-116">Çalıştırma `dotnet new webapp` komut satırından.</span><span class="sxs-lookup"><span data-stu-id="c504b-116">Run `dotnet new webapp` from the command line.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c504b-117">Çalıştırma `dotnet new razor` komut satırından.</span><span class="sxs-lookup"><span data-stu-id="c504b-117">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

<span data-ttu-id="c504b-118">Oluşturulan açın *.csproj* Mac için Visual Studio'dan dosyası</span><span class="sxs-lookup"><span data-stu-id="c504b-118">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="c504b-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c504b-119">Visual Studio Code</span></span>](#tab/visual-studio-code)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="c504b-120">Çalıştırma `dotnet new webapp` komut satırından.</span><span class="sxs-lookup"><span data-stu-id="c504b-120">Run `dotnet new webapp` from the command line.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c504b-121">Çalıştırma `dotnet new razor` komut satırından.</span><span class="sxs-lookup"><span data-stu-id="c504b-121">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

---

## <a name="razor-pages"></a><span data-ttu-id="c504b-122">Razor Pages</span><span class="sxs-lookup"><span data-stu-id="c504b-122">Razor Pages</span></span>

<span data-ttu-id="c504b-123">Razor sayfaları etkin *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="c504b-123">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="c504b-124">Temel sayfa göz önünde bulundurun: <a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="c504b-124">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="c504b-125">Yukarıdaki kod, çok Razor görünüm dosyası gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="c504b-125">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="c504b-126">Neler farklı kılan unsurdur `@page` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="c504b-126">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="c504b-127">`@page` Dosya, istekleri doğrudan bir denetleyici geçmeden işleme anlamına gelir ve MVC eyleme - yapar.</span><span class="sxs-lookup"><span data-stu-id="c504b-127">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="c504b-128">`@page` ilk Razor yönergesi bir sayfa üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-128">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="c504b-129">`@page` diğer Razor yapıları davranışını etkiler.</span><span class="sxs-lookup"><span data-stu-id="c504b-129">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="c504b-130">Benzer bir sayfa, kullanarak bir `PageModel` sınıfında, aşağıdaki iki dosyada gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-130">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="c504b-131">*Pages/Index2.cshtml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="c504b-131">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="c504b-132">*Pages/Index2.cshtml.cs* sayfa modeli:</span><span class="sxs-lookup"><span data-stu-id="c504b-132">The *Pages/Index2.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="c504b-133">Kural olarak, `PageModel` sınıf dosyası Razor sayfası dosyası ile aynı ada sahip *.cs* eklenir.</span><span class="sxs-lookup"><span data-stu-id="c504b-133">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="c504b-134">Örneğin, önceki Razor sayfa *Pages/Index2.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c504b-134">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="c504b-135">Dosyayı içeren `PageModel` sınıf adlı *Pages/Index2.cshtml.cs*.</span><span class="sxs-lookup"><span data-stu-id="c504b-135">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="c504b-136">URL yolu sayfalara ilişkilendirmelerini dosya sisteminde sayfanın konuma göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="c504b-136">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="c504b-137">Aşağıdaki tabloda bir Razor sayfası ile eşleşen bir URL gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c504b-137">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="c504b-138">Dosya adı ve yolu</span><span class="sxs-lookup"><span data-stu-id="c504b-138">File name and path</span></span>               | <span data-ttu-id="c504b-139">URL eşleştirme</span><span class="sxs-lookup"><span data-stu-id="c504b-139">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="c504b-140">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-140">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="c504b-141">`/` veya `/Index`</span><span class="sxs-lookup"><span data-stu-id="c504b-141">`/` or `/Index`</span></span> |
| <span data-ttu-id="c504b-142">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-142">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="c504b-143">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-143">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="c504b-144">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-144">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="c504b-145">`/Store` veya `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="c504b-145">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="c504b-146">Notlar:</span><span class="sxs-lookup"><span data-stu-id="c504b-146">Notes:</span></span>

* <span data-ttu-id="c504b-147">Razor sayfaları dosyalarında çalışma zamanı arar *sayfaları* varsayılan klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-147">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="c504b-148">`Index` bir URL bir sayfa içermediğinde varsayılan sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-148">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="write-a-basic-form"></a><span data-ttu-id="c504b-149">Temel bir form yazma</span><span class="sxs-lookup"><span data-stu-id="c504b-149">Write a basic form</span></span>

<span data-ttu-id="c504b-150">Razor sayfaları web tarayıcıları ile kolay bir uygulama oluştururken uygulamak için kullanılan ortak desenler hale getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c504b-150">Razor Pages is designed to make common patterns used with web browsers easy to implement when building an app.</span></span> <span data-ttu-id="c504b-151">[Model bağlama](xref:mvc/models/model-binding), [etiket Yardımcıları](xref:mvc/views/tag-helpers/intro)ve HTML yardımcılarını tüm *yalnızca iş* bir Razor sayfası sınıfta tanımlanan özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="c504b-151">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="c504b-152">"Bize başvurun" oluşturmak için temel bir uygulayan bir sayfa göz önünde bulundurun `Contact` modeli:</span><span class="sxs-lookup"><span data-stu-id="c504b-152">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="c504b-153">Bu belgedeki örnekler için `DbContext` içinde başlatılan [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) dosya.</span><span class="sxs-lookup"><span data-stu-id="c504b-153">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="c504b-154">Veri modeli:</span><span class="sxs-lookup"><span data-stu-id="c504b-154">The data model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="c504b-155">Db bağlamı:</span><span class="sxs-lookup"><span data-stu-id="c504b-155">The db context:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="c504b-156">*Pages/Create.cshtml* dosyasını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="c504b-156">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="c504b-157">*Pages/Create.cshtml.cs* sayfa modeli:</span><span class="sxs-lookup"><span data-stu-id="c504b-157">The *Pages/Create.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="c504b-158">Kural olarak, `PageModel` sınıfı çağrıldığında `<PageName>Model` ve aynı ad alanında sayfası.</span><span class="sxs-lookup"><span data-stu-id="c504b-158">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="c504b-159">`PageModel` Sınıf kendi sunudan sayfasının mantığının ayrımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c504b-159">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="c504b-160">Bu sayfa işleyicileri sayfasına gönderilen istekleri ve sayfayı oluşturmak için kullanılan verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c504b-160">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="c504b-161">Bu ayırma sayfasında bağımlılıkları üzerinden yönetmenizi sağlar [bağımlılık ekleme](xref:fundamentals/dependency-injection) ve [birim testi](xref:test/razor-pages-tests) sayfaları.</span><span class="sxs-lookup"><span data-stu-id="c504b-161">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:test/razor-pages-tests) the pages.</span></span>

<span data-ttu-id="c504b-162">Sayfanın bir `OnPostAsync` *işleyicisi yöntemi*, üzerinde çalıştığı `POST` ister (kullanıcı formu gönderdiğinde).</span><span class="sxs-lookup"><span data-stu-id="c504b-162">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="c504b-163">Herhangi bir HTTP fiil için işleyici yöntemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c504b-163">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="c504b-164">En yaygın işleyicileri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c504b-164">The most common handlers are:</span></span>

* <span data-ttu-id="c504b-165">`OnGet` sayfa için gerekli durumu başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="c504b-165">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="c504b-166">[OnGet](#OnGet) örnek.</span><span class="sxs-lookup"><span data-stu-id="c504b-166">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="c504b-167">`OnPost` Form gönderilerini görselleştirip işlemek için.</span><span class="sxs-lookup"><span data-stu-id="c504b-167">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="c504b-168">`Async` Adlandırma soneki isteğe bağlıdır, ancak genellikle kurala göre zaman uyumsuz işlevleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c504b-168">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="c504b-169">`OnPostAsync` Kod önceki örnekte ne, normalde bir denetleyicisi yazmalısınız için benzer görünür.</span><span class="sxs-lookup"><span data-stu-id="c504b-169">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="c504b-170">Yukarıdaki kod, Razor sayfaları için tipik bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="c504b-170">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="c504b-171">MVC temelleri çoğu ister [model bağlama](xref:mvc/models/model-binding), [doğrulama](xref:mvc/models/validation), ve eylem sonuçlarını paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="c504b-171">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="c504b-172">Önceki `OnPostAsync` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="c504b-172">The previous `OnPostAsync` method:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="c504b-173">Temel akışı `OnPostAsync`:</span><span class="sxs-lookup"><span data-stu-id="c504b-173">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="c504b-174">Doğrulama hataları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c504b-174">Check for validation errors.</span></span>

*  <span data-ttu-id="c504b-175">Herhangi bir hata varsa, verileri kaydetmek ve yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="c504b-175">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="c504b-176">Hatalar varsa sayfası yeniden doğrulama iletileri göster.</span><span class="sxs-lookup"><span data-stu-id="c504b-176">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="c504b-177">İstemci tarafı doğrulama geleneksel ASP.NET Core MVC uygulamaları için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-177">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="c504b-178">Çoğu durumda, doğrulama hataları istemcide algılandı ve hiçbir zaman sunucuya teslim.</span><span class="sxs-lookup"><span data-stu-id="c504b-178">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="c504b-179">Verileri başarıyla girildiğinde `OnPostAsync` işleyicisi yöntem çağrılarını `RedirectToPage` örneği döndürmek için yardımcı yöntem `RedirectToPageResult`.</span><span class="sxs-lookup"><span data-stu-id="c504b-179">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="c504b-180">`RedirectToPage` Yeni eylem sonucu, benzer olan `RedirectToAction` veya `RedirectToRoute`, ancak özelleştirilmiş sayfalar için.</span><span class="sxs-lookup"><span data-stu-id="c504b-180">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="c504b-181">İsteğe bağlı olarak önceki örnekte, kök dizin sayfasına yönlendirir (`/Index`).</span><span class="sxs-lookup"><span data-stu-id="c504b-181">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="c504b-182">`RedirectToPage` içinde ayrıntılı [sayfaları için URL üretimi](#url_gen) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c504b-182">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="c504b-183">Gönderilen bir formu, (yani sunucuya geçirilir) doğrulama hataları olduğunda`OnPostAsync` işleyicisi yöntem çağrılarını `Page` yardımcı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c504b-183">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="c504b-184">`Page` örneği döndürür `PageResult`.</span><span class="sxs-lookup"><span data-stu-id="c504b-184">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="c504b-185">Döndüren `Page` denetleyicileri eylemleri nasıl döndürmek için benzer `View`.</span><span class="sxs-lookup"><span data-stu-id="c504b-185">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="c504b-186">`PageResult` Varsayılan değer <!-- Review  --> dönüş türü için bir işleyici yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c504b-186">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="c504b-187">Döndürür bir işleyici yönteminin `void` sayfasını işler.</span><span class="sxs-lookup"><span data-stu-id="c504b-187">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="c504b-188">`Customer` Özelliği kullanan `[BindProperty]` model bağlama için katılım için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c504b-188">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="c504b-189">Razor sayfaları varsayılan olarak, GET olmayan fiilleri yalnızca özelliklerle bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c504b-189">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="c504b-190">Özellikleri bağlama yazmanız gereken kod miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="c504b-190">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="c504b-191">Form alanlarını işlemek için aynı özellik kullanarak kod azaltır bağlama (`<input asp-for="Customer.Name" />`) ve giriş kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c504b-191">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

[!INCLUDE[](~/includes/bind-get.md)]

<span data-ttu-id="c504b-192">Giriş sayfası (*Index.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="c504b-192">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="c504b-193">İlişkili `PageModel` sınıfı (*Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="c504b-193">The associated `PageModel` class (*Index.cshtml.cs*):</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="c504b-194">*Index.cshtml* dosyası her kişi için bir düzenleme bağlantısı oluşturmak için aşağıdaki biçimlendirme içerir:</span><span class="sxs-lookup"><span data-stu-id="c504b-194">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="c504b-195">[Yer işareti etiketi Yardımcısı](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) kullanılan `asp-route-{value}` düzenleme sayfasına giden bir bağlantı oluşturmak için öznitelik.</span><span class="sxs-lookup"><span data-stu-id="c504b-195">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="c504b-196">Rota verilerini kişiyle bağlantısını içeren kimliği</span><span class="sxs-lookup"><span data-stu-id="c504b-196">The link contains route data with the contact ID.</span></span> <span data-ttu-id="c504b-197">Örneğin: `http://localhost:5000/Edit/1`</span><span class="sxs-lookup"><span data-stu-id="c504b-197">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="c504b-198">*Pages/Edit.cshtml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="c504b-198">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="c504b-199">İlk satırında `@page "{id:int}"` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="c504b-199">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="c504b-200">Yönlendirme kısıtlaması`"{id:int}"` sayfasına içeren isteklerini kabul etmek için sayfayı söyler `int` rota verileri.</span><span class="sxs-lookup"><span data-stu-id="c504b-200">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="c504b-201">Sayfasına bir istek dönüştürülebilir rota verilerini içermiyorsa, bir `int`, çalışma zamanı HTTP 404 (bulunamadı) hatası döndürür.</span><span class="sxs-lookup"><span data-stu-id="c504b-201">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span> <span data-ttu-id="c504b-202">Kimliği isteğe bağlı yapmak için URL'ye `?` rota kısıtlaması için:</span><span class="sxs-lookup"><span data-stu-id="c504b-202">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

<span data-ttu-id="c504b-203">*Pages/Edit.cshtml.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="c504b-203">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="c504b-204">*Index.cshtml* dosyası ayrıca Sil düğmesini her müşteri iletişim bilgileri için oluşturulacak işaretleme içerir:</span><span class="sxs-lookup"><span data-stu-id="c504b-204">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="c504b-205">Sil düğmesini HTML işlendiğinde, `formaction` parametreleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c504b-205">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="c504b-206">Müşteri Kimliği tarafından belirtilen iletişime `asp-route-id` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c504b-206">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="c504b-207">`handler` Tarafından belirtilen `asp-page-handler` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c504b-207">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="c504b-208">İşte bir müşteri bir işlenen Sil düğmesini bir örnek kimliği başvurun `1`:</span><span class="sxs-lookup"><span data-stu-id="c504b-208">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="c504b-209">Düğme seçildiğinde, bir form `POST` isteği sunucuya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-209">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="c504b-210">Kural gereği, işleyici yönteminin adı değerine göre seçilen `handler` parametre düzeni göre `OnPost[handler]Async`.</span><span class="sxs-lookup"><span data-stu-id="c504b-210">By convention, the name of the handler method is selected based on the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="c504b-211">Çünkü `handler` olduğu `delete` Bu örnekte, `OnPostDeleteAsync` işleyicisi yöntemi kullanılır işleme `POST` isteği.</span><span class="sxs-lookup"><span data-stu-id="c504b-211">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="c504b-212">Varsa `asp-page-handler` gibi farklı bir değere ayarlanmış `remove`, ada sahip bir sayfa işleyicisi yöntemi `OnPostRemoveAsync` seçilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-212">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="c504b-213">`OnPostDeleteAsync` Yöntemi:</span><span class="sxs-lookup"><span data-stu-id="c504b-213">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="c504b-214">Kabul `id` Sorgu dizesinden.</span><span class="sxs-lookup"><span data-stu-id="c504b-214">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="c504b-215">Veritabanı ile müşteri iletişim bilgileri için sorgular `FindAsync`.</span><span class="sxs-lookup"><span data-stu-id="c504b-215">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="c504b-216">Müşteri irtibat bulunursa, müşteri kişiler listesinden kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="c504b-216">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="c504b-217">Veritabanı güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-217">The database is updated.</span></span>
* <span data-ttu-id="c504b-218">Çağrıları `RedirectToPage` kök dizin sayfasına yeniden yönlendirmek için (`/Index`).</span><span class="sxs-lookup"><span data-stu-id="c504b-218">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-as-required"></a><span data-ttu-id="c504b-219">Sayfa özelliklerini gerektiği gibi işaretleme</span><span class="sxs-lookup"><span data-stu-id="c504b-219">Mark page properties as required</span></span>

<span data-ttu-id="c504b-220">Özellikleri bir `PageModel` ile donatılmış [gerekli](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) özniteliği:</span><span class="sxs-lookup"><span data-stu-id="c504b-220">Properties on a `PageModel` can be decorated with the [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) attribute:</span></span>

[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]

<span data-ttu-id="c504b-221">Daha fazla bilgi için [Model doğrulama](xref:mvc/models/validation).</span><span class="sxs-lookup"><span data-stu-id="c504b-221">For more information, see [Model validation](xref:mvc/models/validation).</span></span>

## <a name="manage-head-requests-with-the-onget-handler"></a><span data-ttu-id="c504b-222">HEAD isteklerini OnGet işleyici ile yönetme</span><span class="sxs-lookup"><span data-stu-id="c504b-222">Manage HEAD requests with the OnGet handler</span></span>

<span data-ttu-id="c504b-223">HEAD isteklerini belirli bir kaynak için üstbilgiler almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c504b-223">HEAD requests allow you to retrieve the headers for a specific resource.</span></span> <span data-ttu-id="c504b-224">GET istekleri, yanıt gövdesi HEAD isteklerini döndürmeyin.</span><span class="sxs-lookup"><span data-stu-id="c504b-224">Unlike GET requests, HEAD requests don't return a response body.</span></span>

<span data-ttu-id="c504b-225">Normalde, bir baş işleyici oluşturulur ve HEAD isteklerini çağrılır:</span><span class="sxs-lookup"><span data-stu-id="c504b-225">Ordinarily, a HEAD handler is created and called for HEAD requests:</span></span> 

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

<span data-ttu-id="c504b-226">Hiçbir baş işleyici (`OnHead`) olan tanımlanan, Razor sayfaları geri alma sayfası işleyicisi çağırma için döner (`OnGet`) ASP.NET Core 2.1 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="c504b-226">If no HEAD handler (`OnHead`) is defined, Razor Pages falls back to calling the GET page handler (`OnGet`) in ASP.NET Core 2.1 or later.</span></span> <span data-ttu-id="c504b-227">ASP.NET Core 2.1 ve 2.2 ile bu davranış oluşur [SetCompatibilityVersion](xref:mvc/compatibility-version) içinde `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="c504b-227">In ASP.NET Core 2.1 and 2.2, this behavior occurs with the [SetCompatibilityVersion](xref:mvc/compatibility-version) in `Startup.Configure`:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

<span data-ttu-id="c504b-228">Varsayılan şablon oluşturma `SetCompatibilityVersion` 2.2 ve ASP.NET Core 2.1 ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="c504b-228">The default templates generate the `SetCompatibilityVersion` call in ASP.NET Core 2.1 and 2.2.</span></span>

<span data-ttu-id="c504b-229">`SetCompatibilityVersion` Razor sayfaları seçeneği etkili bir şekilde ayarlar `AllowMappingHeadRequestsToGetHandler` için `true`.</span><span class="sxs-lookup"><span data-stu-id="c504b-229">`SetCompatibilityVersion` effectively sets the Razor Pages option `AllowMappingHeadRequestsToGetHandler` to `true`.</span></span>

<span data-ttu-id="c504b-230">Tüm 2.1 davranışlarla içine edilmesiyle yerine `SetCompatibilityVersion`, siz açıkça özel davranışları için katılımı.</span><span class="sxs-lookup"><span data-stu-id="c504b-230">Rather than opting into all 2.1 behaviors with `SetCompatibilityVersion`, you can explicitly opt-in to specific behaviors.</span></span> <span data-ttu-id="c504b-231">Aşağıdaki kod içine GET işleyicisine eşleme HEAD isteklerini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="c504b-231">The following code opts into the mapping HEAD requests to the GET handler.</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```

::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="c504b-232">XSRF/CSRF ve Razor sayfaları</span><span class="sxs-lookup"><span data-stu-id="c504b-232">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="c504b-233">Herhangi bir kod yazmanıza gerek kalmaz [antiforgery doğrulama](xref:security/anti-request-forgery).</span><span class="sxs-lookup"><span data-stu-id="c504b-233">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="c504b-234">Otomatik olarak antiforgery belirteç oluşturma ve doğrulama Razor sayfaları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-234">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="c504b-235">Razor sayfaları kullanmaya düzenleri, kısmi, şablonları ve etiket yardımcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="c504b-235">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="c504b-236">Sayfaları Razor görüntüleme motorunu tüm özellikleriyle çalışma.</span><span class="sxs-lookup"><span data-stu-id="c504b-236">Pages work with all the capabilities of the Razor view engine.</span></span> <span data-ttu-id="c504b-237">Düzenleri, kısmi, şablonlar, etiket Yardımcıları *_ViewStart.cshtml*, *_viewımports.cshtml* geleneksel Razor görünümleri yaptıkları aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="c504b-237">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="c504b-238">Şimdi bu sayfa, bu özelliklerden bazılarını avantajlarından yararlanarak declutter.</span><span class="sxs-lookup"><span data-stu-id="c504b-238">Let's declutter this page by taking advantage of some of those capabilities.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="c504b-239">Ekleme bir [düzen sayfası](xref:mvc/views/layout) için *Pages/Shared/_Layout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="c504b-239">Add a [layout page](xref:mvc/views/layout) to *Pages/Shared/_Layout.cshtml*:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c504b-240">Ekleme bir [düzen sayfası](xref:mvc/views/layout) için *Pages/_Layout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="c504b-240">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

::: moniker-end

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="c504b-241">[Düzen](xref:mvc/views/layout):</span><span class="sxs-lookup"><span data-stu-id="c504b-241">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="c504b-242">(Sayfa düzeni dışında bölgedeyse sürece) her sayfasının düzenini denetler.</span><span class="sxs-lookup"><span data-stu-id="c504b-242">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="c504b-243">JavaScript ve stil sayfalarını gibi HTML yapıları içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="c504b-243">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="c504b-244">Bkz: [düzen sayfası](xref:mvc/views/layout) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c504b-244">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="c504b-245">[Düzen](xref:mvc/views/layout#specifying-a-layout) özelliği ayarlandığında *Pages/_ViewStart.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="c504b-245">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="c504b-246">Düzen bulunduğu *sayfaları/paylaşılan* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-246">The layout is in the *Pages/Shared* folder.</span></span> <span data-ttu-id="c504b-247">Geçerli sayfa ile aynı klasörde başlangıç sayfaları başka görünümlerini (düzenleri, şablonlar, kısmi) hiyerarşik olarak arayın.</span><span class="sxs-lookup"><span data-stu-id="c504b-247">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="c504b-248">Bir düzende *sayfaları/paylaşılan* klasörü altında herhangi bir Razor sayfadan kullanılabilir *sayfaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-248">A layout in the *Pages/Shared* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="c504b-249">Düzen dosyası gitmesi gereken *sayfaları/paylaşılan* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-249">The layout file should go in the *Pages/Shared* folder.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c504b-250">Düzen bulunduğu *sayfaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-250">The layout is in the *Pages* folder.</span></span> <span data-ttu-id="c504b-251">Geçerli sayfa ile aynı klasörde başlangıç sayfaları başka görünümlerini (düzenleri, şablonlar, kısmi) hiyerarşik olarak arayın.</span><span class="sxs-lookup"><span data-stu-id="c504b-251">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="c504b-252">Bir düzende *sayfaları* klasörü altında herhangi bir Razor sayfadan kullanılabilir *sayfaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-252">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

::: moniker-end

<span data-ttu-id="c504b-253">Öneririz **değil** Düzen dosyası koymak *görünümler/paylaşılan* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-253">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="c504b-254">*Görünümler/paylaşılan* bir MVC görünümleri modelidir.</span><span class="sxs-lookup"><span data-stu-id="c504b-254">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="c504b-255">Razor sayfaları klasör hiyerarşisi, yol kuralları yararlanmayı yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="c504b-255">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="c504b-256">Bir Razor sayfası görünümü aramadan içerir *sayfaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-256">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="c504b-257">Düzenleri, şablonları ve geleneksel Razor görünümleri ile MVC denetleyicileri ile kullanmakta olduğunuz kısmi *yalnızca iş*.</span><span class="sxs-lookup"><span data-stu-id="c504b-257">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="c504b-258">Ekleme bir *Pages/_ViewImports.cshtml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="c504b-258">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="c504b-259">`@namespace` öğreticinin ilerleyen bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c504b-259">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="c504b-260">`@addTagHelper` Yönergesi getirdiği [yerleşik etiket Yardımcıları](xref:mvc/views/tag-helpers/builtin-th/Index) tüm sayfalara *sayfaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-260">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="c504b-261">Zaman `@namespace` yönergesi bir sayfada açıkça kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c504b-261">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="c504b-262">Yönergesi, ad alanı sayfası için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c504b-262">The directive sets the namespace for the page.</span></span> <span data-ttu-id="c504b-263">`@model` Yönergesi ad alanını katmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c504b-263">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="c504b-264">Zaman `@namespace` yönergesi kapsanıyorsa *_viewımports.cshtml*, belirtilen ad alanı içe aktaran sayfasında oluşturulan ad alanı öneki sağlayan `@namespace` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="c504b-264">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="c504b-265">Oluşturulan ad alanı (sonek kısmı) geri kalanı içeren klasörü arasında noktayla ayrılmış göreli yoludur *_viewımports.cshtml* ve sayfayı içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="c504b-265">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="c504b-266">Örneğin, `PageModel` sınıfı *Pages/Customers/Edit.cshtml.cs* ad alanını açıkça ayarlar:</span><span class="sxs-lookup"><span data-stu-id="c504b-266">For example, the `PageModel` class *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="c504b-267">*Pages/_ViewImports.cshtml* dosyasını ayarlar şu ad alanı:</span><span class="sxs-lookup"><span data-stu-id="c504b-267">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="c504b-268">Oluşturulan ad alanı için *Pages/Customers/Edit.cshtml* Razor sayfası aynıdır `PageModel` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c504b-268">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the `PageModel` class.</span></span>

<span data-ttu-id="c504b-269">`@namespace` *Geleneksel Razor görünümleri ile de çalışır.*</span><span class="sxs-lookup"><span data-stu-id="c504b-269">`@namespace` *also works with conventional Razor views.*</span></span>

<span data-ttu-id="c504b-270">Özgün *Pages/Create.cshtml* dosyasını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="c504b-270">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="c504b-271">Güncelleştirilmiş *Pages/Create.cshtml* dosyasını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="c504b-271">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="c504b-272">[Razor sayfaları başlangıç projesini](#rpvs17) içeren *Pages/_ValidationScriptsPartial.cshtml*, istemci tarafı doğrulama kancaları.</span><span class="sxs-lookup"><span data-stu-id="c504b-272">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<span data-ttu-id="c504b-273">Kısmi görünümler hakkında daha fazla bilgi için bkz. <xref:mvc/views/partial>.</span><span class="sxs-lookup"><span data-stu-id="c504b-273">For more information on partial views, see <xref:mvc/views/partial>.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="c504b-274">Sayfaları için URL üretimi</span><span class="sxs-lookup"><span data-stu-id="c504b-274">URL generation for Pages</span></span>

<span data-ttu-id="c504b-275">`Create` Sayfasında, daha önce kullandığı gösterilen `RedirectToPage`:</span><span class="sxs-lookup"><span data-stu-id="c504b-275">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="c504b-276">Uygulama, aşağıdaki dosya/klasör yapısına sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c504b-276">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="c504b-277">*/ Sayfaları*</span><span class="sxs-lookup"><span data-stu-id="c504b-277">*/Pages*</span></span>

  * <span data-ttu-id="c504b-278">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-278">*Index.cshtml*</span></span>
  * <span data-ttu-id="c504b-279">*/ Müşteriler*</span><span class="sxs-lookup"><span data-stu-id="c504b-279">*/Customers*</span></span>

    * <span data-ttu-id="c504b-280">*Create.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-280">*Create.cshtml*</span></span>
    * <span data-ttu-id="c504b-281">*Edit.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-281">*Edit.cshtml*</span></span>
    * <span data-ttu-id="c504b-282">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c504b-282">*Index.cshtml*</span></span>

<span data-ttu-id="c504b-283">*Pages/Customers/Create.cshtml* ve *Pages/Customers/Edit.cshtml* yeniden yönlendirme sayfası *Pages/Index.cshtml* başarılı olduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="c504b-283">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="c504b-284">Dize `/Index` önceki sayfaya erişmek için URI'ın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-284">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="c504b-285">Dize `/Index` için URI oluşturmak için kullanılan *Pages/Index.cshtml* sayfası.</span><span class="sxs-lookup"><span data-stu-id="c504b-285">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="c504b-286">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c504b-286">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="c504b-287">Sayfa adı sayfasına kökünden yoludur */sayfaları* önde gelen dahil olmak üzere klasörü `/` (örneğin, `/Index`).</span><span class="sxs-lookup"><span data-stu-id="c504b-287">The page name is the path to the page from the root */Pages* folder including a leading `/` (for example, `/Index`).</span></span> <span data-ttu-id="c504b-288">Önceki URL oluşturma örnekleri, runbook'a kod bir URL Gelişmiş Seçenekler ve işlevsel yetenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="c504b-288">The preceding URL generation samples offer enhanced options and functional capabilities over hardcoding a URL.</span></span> <span data-ttu-id="c504b-289">URL üretimi kullanan [yönlendirme](xref:mvc/controllers/routing) ve oluşturmak ve parametreleri hedef yolda bir rota nasıl tanımlandığını göre kodlayın.</span><span class="sxs-lookup"><span data-stu-id="c504b-289">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="c504b-290">URL üretimi sayfaları için göreli adlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="c504b-290">URL generation for pages supports relative names.</span></span> <span data-ttu-id="c504b-291">Aşağıdaki tabloda, hangi dizin sayfası ile farklı seçili olduğunu gösterir `RedirectToPage` parametrelerinden *Pages/Customers/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="c504b-291">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="c504b-292">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="c504b-292">RedirectToPage(x)</span></span>| <span data-ttu-id="c504b-293">Sayfa</span><span class="sxs-lookup"><span data-stu-id="c504b-293">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="c504b-294">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="c504b-294">RedirectToPage("/Index")</span></span> | <span data-ttu-id="c504b-295">*Sayfalar/dizin*</span><span class="sxs-lookup"><span data-stu-id="c504b-295">*Pages/Index*</span></span> |
| <span data-ttu-id="c504b-296">RedirectToPage("./Index");</span><span class="sxs-lookup"><span data-stu-id="c504b-296">RedirectToPage("./Index");</span></span> | <span data-ttu-id="c504b-297">*Müşteriler/sayfalar/dizin*</span><span class="sxs-lookup"><span data-stu-id="c504b-297">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="c504b-298">RedirectToPage(".. / Dizin")</span><span class="sxs-lookup"><span data-stu-id="c504b-298">RedirectToPage("../Index")</span></span> | <span data-ttu-id="c504b-299">*Sayfalar/dizin*</span><span class="sxs-lookup"><span data-stu-id="c504b-299">*Pages/Index*</span></span> |
| <span data-ttu-id="c504b-300">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="c504b-300">RedirectToPage("Index")</span></span>  | <span data-ttu-id="c504b-301">*Müşteriler/sayfalar/dizin*</span><span class="sxs-lookup"><span data-stu-id="c504b-301">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="c504b-302">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, ve `RedirectToPage("../Index")` olan <em>göreli adlar</em>.</span><span class="sxs-lookup"><span data-stu-id="c504b-302">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are <em>relative names</em>.</span></span> <span data-ttu-id="c504b-303">`RedirectToPage` Parametresi <em>birleştirilmiş</em> ile hedef sayfanın adını işlem için geçerli sayfasının yolu.</span><span class="sxs-lookup"><span data-stu-id="c504b-303">The `RedirectToPage` parameter is <em>combined</em> with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

<span data-ttu-id="c504b-304">Göreli adı bağlama siteleri karmaşık bir yapısı ile derleme yaparken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-304">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="c504b-305">Bir klasördeki sayfalar arasında bağlamak için göreli adları kullanıyorsa, bu klasörü yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c504b-305">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="c504b-306">(Bunlar klasör adı olmadığından) tüm bağlantıların hala çalıştığından.</span><span class="sxs-lookup"><span data-stu-id="c504b-306">All the links still work (because they didn't include the folder name).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="viewdata-attribute"></a><span data-ttu-id="c504b-307">ViewData özniteliği</span><span class="sxs-lookup"><span data-stu-id="c504b-307">ViewData attribute</span></span>

<span data-ttu-id="c504b-308">Veri içeren bir sayfa geçilebilir [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span><span class="sxs-lookup"><span data-stu-id="c504b-308">Data can be passed to a page with [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="c504b-309">Denetleyicilerde veya modellerde Razor sayfası özelliklerini düzenlenmiş ile `[ViewData]` depolanır ve gelen yüklenen değerlerine sahip [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span><span class="sxs-lookup"><span data-stu-id="c504b-309">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span></span>

<span data-ttu-id="c504b-310">Aşağıdaki örnekte, `AboutModel` içeren bir `Title` özelliği düzenlenmiş ile `[ViewData]`.</span><span class="sxs-lookup"><span data-stu-id="c504b-310">In the following example, the `AboutModel` contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="c504b-311">`Title` Özelliği hakkında sayfasının başlığı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c504b-311">The `Title` property is set to the title of the About page:</span></span>

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

<span data-ttu-id="c504b-312">Hakkında sayfasında erişim `Title` özelliği model özelliği olarak:</span><span class="sxs-lookup"><span data-stu-id="c504b-312">In the About page, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="c504b-313">Düzende dışında ViewData sözlükten başlığını okuyun:</span><span class="sxs-lookup"><span data-stu-id="c504b-313">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

## <a name="tempdata"></a><span data-ttu-id="c504b-314">TempData</span><span class="sxs-lookup"><span data-stu-id="c504b-314">TempData</span></span>

<span data-ttu-id="c504b-315">ASP.NET Core sunan [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) özelliği bir [denetleyicisi](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span><span class="sxs-lookup"><span data-stu-id="c504b-315">ASP.NET Core exposes the [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="c504b-316">Bu özellik, okunur kadar verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="c504b-316">This property stores data until it's read.</span></span> <span data-ttu-id="c504b-317">`Keep` Ve `Peek` yöntemleri silme olmadan verileri incelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c504b-317">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="c504b-318">`TempData` için yeniden yönlendirme, birden çok tek bir istek verileri gerektiğinde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c504b-318">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="c504b-319">`[TempData]` Özniteliği ASP.NET Core 2.0 sürümünde yenidir ve denetleyicileri ve sayfaları desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c504b-319">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="c504b-320">Aşağıdaki kodu değerini ayarlar `Message` kullanarak `TempData`:</span><span class="sxs-lookup"><span data-stu-id="c504b-320">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="c504b-321">Aşağıdaki biçimlendirmede *Pages/Customers/Index.cshtml* dosya değerini görüntülediğine `Message` kullanarak `TempData`.</span><span class="sxs-lookup"><span data-stu-id="c504b-321">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="c504b-322">*Pages/Customers/Index.cshtml.cs* sayfa modeli uygular `[TempData]` özniteliğini `Message` özelliği.</span><span class="sxs-lookup"><span data-stu-id="c504b-322">The *Pages/Customers/Index.cshtml.cs* page model applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="c504b-323">Daha fazla bilgi için [TempData](xref:fundamentals/app-state#tempdata) .</span><span class="sxs-lookup"><span data-stu-id="c504b-323">For more information, see [TempData](xref:fundamentals/app-state#tempdata) .</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="c504b-324">Sayfa başına birden çok işleyicileri</span><span class="sxs-lookup"><span data-stu-id="c504b-324">Multiple handlers per page</span></span>

<span data-ttu-id="c504b-325">İki sayfa kullanarak işleyicileri için şu sayfaya biçimlendirmeleri oluşturur `asp-page-handler` etiketi Yardımcısı:</span><span class="sxs-lookup"><span data-stu-id="c504b-325">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

<span data-ttu-id="c504b-326">Önceki örnekte iki düğmeleri kullanarak her gönderme formundadır `FormActionTagHelper` için farklı bir URL göndermek için.</span><span class="sxs-lookup"><span data-stu-id="c504b-326">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="c504b-327">`asp-page-handler` Özniteliktir na yardımcı olarak `asp-page`.</span><span class="sxs-lookup"><span data-stu-id="c504b-327">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="c504b-328">`asp-page-handler` bir sayfa tarafından tanımlanan işleyici yöntemlerin her biri için gönderme URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c504b-328">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="c504b-329">`asp-page` örnek, geçerli sayfa için bağlama için belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="c504b-329">`asp-page` isn't specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="c504b-330">Sayfa modeli:</span><span class="sxs-lookup"><span data-stu-id="c504b-330">The page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="c504b-331">Önceki kod *işleyici yöntemleri adlı*.</span><span class="sxs-lookup"><span data-stu-id="c504b-331">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="c504b-332">Adlandırılmış işleyici yöntemleri adında sonra metin alarak oluşturulur `On<HTTP Verb>` ve önce `Async` (varsa).</span><span class="sxs-lookup"><span data-stu-id="c504b-332">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="c504b-333">Önceki örnekte OnPost sayfa yöntemlerdir**JoinList**zaman uyumsuz ve OnPost**JoinListUC**zaman uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="c504b-333">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="c504b-334">İle *OnPost* ve *zaman uyumsuz* kaldırıldıysa, işleyici adları olan `JoinList` ve `JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="c504b-334">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="c504b-335">Kod önceki kullanarak, gönderildiği URL yolu `OnPostJoinListAsync` olduğu `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span><span class="sxs-lookup"><span data-stu-id="c504b-335">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="c504b-336">Gönderildiği URL yolu `OnPostJoinListUCAsync` olduğu `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="c504b-336">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>

## <a name="custom-routes"></a><span data-ttu-id="c504b-337">Özel yollar</span><span class="sxs-lookup"><span data-stu-id="c504b-337">Custom routes</span></span>

<span data-ttu-id="c504b-338">Kullanım `@page` yönergesini:</span><span class="sxs-lookup"><span data-stu-id="c504b-338">Use the `@page` directive to:</span></span>

* <span data-ttu-id="c504b-339">Bir sayfa için özel bir yol belirtin.</span><span class="sxs-lookup"><span data-stu-id="c504b-339">Specify a custom route to a page.</span></span> <span data-ttu-id="c504b-340">Rota hakkında sayfasına gibi ayarlanabilir `/Some/Other/Path` ile `@page "/Some/Other/Path"`.</span><span class="sxs-lookup"><span data-stu-id="c504b-340">For example, the route to the About page can be set to `/Some/Other/Path` with `@page "/Some/Other/Path"`.</span></span>
* <span data-ttu-id="c504b-341">Bir sayfanın varsayılan yol kesimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c504b-341">Append segments to a page's default route.</span></span> <span data-ttu-id="c504b-342">Örneğin, bir "Item" segment ile bir sayfanın varsayılan rota eklenebilir `@page "item"`.</span><span class="sxs-lookup"><span data-stu-id="c504b-342">For example, an "item" segment can be added to a page's default route with `@page "item"`.</span></span>
* <span data-ttu-id="c504b-343">Bir sayfanın varsayılan rota için parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c504b-343">Append parameters to a page's default route.</span></span> <span data-ttu-id="c504b-344">Örneğin, bir kimliği parametre `id`, içeren bir sayfa için gerekli olabilir `@page "{id}"`.</span><span class="sxs-lookup"><span data-stu-id="c504b-344">For example, an ID parameter, `id`, can be required for a page with `@page "{id}"`.</span></span>

<span data-ttu-id="c504b-345">Bir tilde işareti tarafından atanan bir köküne göreli yol (`~`) yolunun başında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c504b-345">A root-relative path designated by a tilde (`~`) at the beginning of the path is supported.</span></span> <span data-ttu-id="c504b-346">Örneğin, `@page "~/Some/Other/Path"` aynı `@page "/Some/Other/Path"`.</span><span class="sxs-lookup"><span data-stu-id="c504b-346">For example, `@page "~/Some/Other/Path"` is the same as `@page "/Some/Other/Path"`.</span></span>

<span data-ttu-id="c504b-347">Sorgu dizesi değiştirebilirsiniz `?handler=JoinList` yol kesimi URL'yi `/JoinList` rota şablonu belirterek `@page "{handler?}"`.</span><span class="sxs-lookup"><span data-stu-id="c504b-347">You can change the query string `?handler=JoinList` in the URL to a route segment `/JoinList` by specifying the route template `@page "{handler?}"`.</span></span>

<span data-ttu-id="c504b-348">Sorgu dizesi beğenmezseniz `?handler=JoinList` URL'de, yol işleyicisi adı URL'nin yol kısmı put değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c504b-348">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="c504b-349">Rota sonra çift tırnak içine alınmış bir rota şablonu ekleyerek özelleştirebilirsiniz `@page` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="c504b-349">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="c504b-350">Kod önceki kullanarak, gönderildiği URL yolu `OnPostJoinListAsync` olduğu `http://localhost:5000/Customers/CreateFATH/JoinList`.</span><span class="sxs-lookup"><span data-stu-id="c504b-350">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH/JoinList`.</span></span> <span data-ttu-id="c504b-351">Gönderildiği URL yolu `OnPostJoinListUCAsync` olduğu `http://localhost:5000/Customers/CreateFATH/JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="c504b-351">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH/JoinListUC`.</span></span>

<span data-ttu-id="c504b-352">`?` Aşağıdaki `handler` rota parametresinin isteğe bağlı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c504b-352">The `?` following `handler` means the route parameter is optional.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="c504b-353">Yapılandırma ve ayarlar</span><span class="sxs-lookup"><span data-stu-id="c504b-353">Configuration and settings</span></span>

<span data-ttu-id="c504b-354">Gelişmiş seçeneklerini yapılandırmak için genişletme yöntemini kullanmak `AddRazorPagesOptions` MVC oluşturucu üzerinde:</span><span class="sxs-lookup"><span data-stu-id="c504b-354">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="c504b-355">Şu anda kullanabileceğiniz `RazorPagesOptions` sayfa için kök dizine ayarlayın veya uygulama sayfaları için model kuralları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c504b-355">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="c504b-356">Daha fazla genişletilebilirlik bu şekilde gelecekte etkinleştiririz.</span><span class="sxs-lookup"><span data-stu-id="c504b-356">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="c504b-357">Görünümlerinizi önceden derleme için bkz: [Razor görünüm derlemesi](xref:mvc/views/view-compilation) .</span><span class="sxs-lookup"><span data-stu-id="c504b-357">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="c504b-358">[İndirme veya görüntüleme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="c504b-358">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span></span>

<span data-ttu-id="c504b-359">Bkz: [Razor sayfaları kullanmaya başlama](xref:tutorials/razor-pages/razor-pages-start), ilgili bu girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c504b-359">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="c504b-360">Razor sayfaları içerik kök dizininde olduğunu belirtin</span><span class="sxs-lookup"><span data-stu-id="c504b-360">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="c504b-361">Varsayılan olarak, Razor sayfaları, köklü olmayan */sayfaları* dizin.</span><span class="sxs-lookup"><span data-stu-id="c504b-361">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="c504b-362">Ekleme [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) için [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) , Razor sayfaları içerik kök dizininde olduğunu belirtmek için ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) uygulama:</span><span class="sxs-lookup"><span data-stu-id="c504b-362">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="c504b-363">Razor sayfaları özel kök dizininde olduğunu belirtin</span><span class="sxs-lookup"><span data-stu-id="c504b-363">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="c504b-364">Ekleme [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) için [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) , Razor sayfaları bir uygulamadaki özel kök dizininde olduğunu belirtmek için (göreli bir yol belirtin):</span><span class="sxs-lookup"><span data-stu-id="c504b-364">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="additional-resources"></a><span data-ttu-id="c504b-365">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c504b-365">Additional resources</span></span>

* <xref:index>
* <xref:mvc/views/razor>
* <xref:tutorials/razor-pages/razor-pages-start>
* <xref:security/authorization/razor-pages-authorization>
* <xref:razor-pages/razor-pages-conventions>
* <xref:test/razor-pages-tests>
* <xref:mvc/views/partial>
