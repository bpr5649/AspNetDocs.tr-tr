---
title: Razor bileşenlerine giriş
author: guardrex
description: 'ASP.NET Core Razor bileşenleri, etkileşimli istemci tarafı web kullanıcı Arabirimi ile .NET, ASP.NET Core uygulaması oluşturmak için bir yöntem keşfedin.'
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/12/2019
uid: razor-components/index
---
# <a name="introduction-to-razor-components"></a><span data-ttu-id="16211-103">Razor bileşenlerine giriş</span><span class="sxs-lookup"><span data-stu-id="16211-103">Introduction to Razor Components</span></span>

<span data-ttu-id="16211-104">Tarafından [Daniel Roth](https://github.com/danroth27) ve [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="16211-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="16211-105">*Razor bileşenleri* etkileşimli istemci tarafı web kullanıcı Arabirimi ile .NET derleme yolu:</span><span class="sxs-lookup"><span data-stu-id="16211-105">*Razor Components* is a way to build interactive client-side web UI with .NET:</span></span>

* <span data-ttu-id="16211-106">Kullanarak zengin etkileşimli kullanıcı arabirimleri oluşturun C# JavaScript yerine.</span><span class="sxs-lookup"><span data-stu-id="16211-106">Build rich interactive UIs using C# instead of JavaScript.</span></span>
* <span data-ttu-id="16211-107">.NET ile yazılan tüm sunucu tarafı ve istemci tarafı uygulama mantığı paylaşın.</span><span class="sxs-lookup"><span data-stu-id="16211-107">Share server-side and client-side app logic all written with .NET.</span></span>
* <span data-ttu-id="16211-108">HTML ve CSS olarak UI mobil tarayıcılar dahil olmak üzere geniş tarayıcı desteği işleyin.</span><span class="sxs-lookup"><span data-stu-id="16211-108">Render the UI as HTML and CSS for wide browser support, including mobile browsers.</span></span>

<span data-ttu-id="16211-109">Razor bileşenleri dahil olmak üzere çoğu uygulama tarafından gereken çekirdek özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="16211-109">Razor Components supports core facilities required by most apps, including:</span></span>

* <span data-ttu-id="16211-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="16211-110">Parameters</span></span>
* <span data-ttu-id="16211-111">Olay işleme</span><span class="sxs-lookup"><span data-stu-id="16211-111">Event handling</span></span>
* <span data-ttu-id="16211-112">Veri bağlama</span><span class="sxs-lookup"><span data-stu-id="16211-112">Data binding</span></span>
* <span data-ttu-id="16211-113">Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="16211-113">Routing</span></span>
* <span data-ttu-id="16211-114">Bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="16211-114">Dependency injection</span></span>
* <span data-ttu-id="16211-115">Düzenler</span><span class="sxs-lookup"><span data-stu-id="16211-115">Layouts</span></span>
* <span data-ttu-id="16211-116">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="16211-116">Templating</span></span>
* <span data-ttu-id="16211-117">Basamaklı değerler</span><span class="sxs-lookup"><span data-stu-id="16211-117">Cascading values</span></span>

<span data-ttu-id="16211-118">Kullanıcı Arabirimi güncelleştirmeleri nasıl uygulanacağını gelen bileşeni işleme mantığı Razor bileşeni birbirinden ayırır.</span><span class="sxs-lookup"><span data-stu-id="16211-118">Razor Components decouples component rendering logic from how UI updates are applied.</span></span> <span data-ttu-id="16211-119">ASP.NET Core Razor bileşenleri .NET Core 3. 0'ı ASP.NET Core uygulaması sunucusunda Razor bileşenlerini barındırma desteği ekler.</span><span class="sxs-lookup"><span data-stu-id="16211-119">ASP.NET Core Razor Components in .NET Core 3.0 adds support for hosting Razor Components on the server in an ASP.NET Core app.</span></span> <span data-ttu-id="16211-120">Kullanıcı Arabirimi güncelleştirmeleri SignalR bağlantısı üzerinden işlenir.</span><span class="sxs-lookup"><span data-stu-id="16211-120">UI updates are handled over a SignalR connection.</span></span>

<span data-ttu-id="16211-121">Çalışma zamanı:</span><span class="sxs-lookup"><span data-stu-id="16211-121">The runtime:</span></span>

* <span data-ttu-id="16211-122">UI olayları tarayıcıdan sunucuya gönderme işler.</span><span class="sxs-lookup"><span data-stu-id="16211-122">Handles sending UI events from the browser to the server.</span></span>
* <span data-ttu-id="16211-123">Geçerli kullanıcı Arabirimi güncelleştirmeleri sunucu tarafından gönderilen bileşenleri çalıştırdıktan sonra tarayıcıya geri.</span><span class="sxs-lookup"><span data-stu-id="16211-123">Applies UI updates sent by the server back to the browser after running the components.</span></span>

<span data-ttu-id="16211-124">Tarayıcı ile iletişim kurmak için Razor bileşenleri tarafından kullanılan bağlantı JavaScript birlikte çalışma çağrıları işlemek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="16211-124">The connection used by Razor Components to communicate with the browser is also used to handle JavaScript interop calls.</span></span>

![Razor bileşenleri .NET kod sunucu üzerinde çalışır ve belge nesne modeli istemcide bir SignalR bağlantısı üzerinden etkileşim](index/_static/aspnet-core-razor-components.png)

<span data-ttu-id="16211-126">Daha fazla bilgi için bkz. <xref:razor-components/hosting-models#server-side-hosting-model>.</span><span class="sxs-lookup"><span data-stu-id="16211-126">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span>

<span data-ttu-id="16211-127">*Blazor* Razor bileşenlerinin Deneysel istemci-tarafı barındırma modeli.</span><span class="sxs-lookup"><span data-stu-id="16211-127">*Blazor* is the experimental client-side hosting model of Razor Components.</span></span> <span data-ttu-id="16211-128">Blazor transpilation eklentileri veya kod olmadan açık web standartları kullanarak tarayıcıda .NET üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="16211-128">Blazor runs on .NET in the browser using open web standards without plugins or code transpilation.</span></span> <span data-ttu-id="16211-129">Daha fazla bilgi için bkz. <xref:razor-components/hosting-models#client-side-hosting-model>.</span><span class="sxs-lookup"><span data-stu-id="16211-129">For more information, see <xref:razor-components/hosting-models#client-side-hosting-model>.</span></span>

## <a name="components"></a><span data-ttu-id="16211-130">Bileşenler</span><span class="sxs-lookup"><span data-stu-id="16211-130">Components</span></span>

<span data-ttu-id="16211-131">A *Razor bileşen* bir kullanıcı Arabirimi, bir sayfa, iletişim kutusu veya veri girişi formuna gibi parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="16211-131">A *Razor Component* is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="16211-132">Bileşenleri kullanıcı olayları işlemek ve esnek UI işleme mantığı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="16211-132">Components handle user events and define flexible UI rendering logic.</span></span> <span data-ttu-id="16211-133">Bileşenleri iç içe geçmiş ve yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="16211-133">Components can be nested and reused.</span></span>

<span data-ttu-id="16211-134">.NET sınıf paylaşılabilir ve NuGet paketleri olarak dağıtılmış .NET derlemelerini yerleşik bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="16211-134">Components are .NET classes built into .NET assemblies that can be shared and distributed as NuGet packages.</span></span> <span data-ttu-id="16211-135">Sınıf ya da bir Razor biçimlendirme sayfası biçiminde yazılabilir (*.cshtml*) veya farklı bir C# sınıfı (*.cs*).</span><span class="sxs-lookup"><span data-stu-id="16211-135">The class can either be written in the form of a Razor markup page (*.cshtml*) or as a C# class (*.cs*).</span></span>

<span data-ttu-id="16211-136">[Razor](xref:mvc/views/razor) HTML biçimlendirmesi ile birleştiren bir söz dizimi C# kod.</span><span class="sxs-lookup"><span data-stu-id="16211-136">[Razor](xref:mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="16211-137">Razor Geliştirici üretkenliği, biçimlendirme arasında geçiş yapmak Geliştirici izin vermek için tasarlanmıştır ve C# ile aynı dosyada [IntelliSense](/visualstudio/ide/using-intellisense) destekler.</span><span class="sxs-lookup"><span data-stu-id="16211-137">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="16211-138">Razor sayfaları ve MVC görünümleri de Razor kullanın.</span><span class="sxs-lookup"><span data-stu-id="16211-138">Razor Pages and MVC views also use Razor.</span></span> <span data-ttu-id="16211-139">Razor sayfaları ve istek/yanıt modeli çevresinde kurulan MVC görünümleri, bileşenleri özellikle kullanıcı Arabirimi oluşturma işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="16211-139">Unlike Razor Pages and MVC views, which are built around a request/response model, components are used specifically for handling UI composition.</span></span> <span data-ttu-id="16211-140">Razor bileşenleri, özellikle istemci tarafı UI mantığı ve birleştirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="16211-140">Razor Components can be used specifically for client-side UI logic and composition.</span></span>

<span data-ttu-id="16211-141">Aşağıdaki biçimlendirme bir Razor dosyasında özel iletişim bileşeninin örneğidir (*DialogComponent.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="16211-141">The following markup is an example of a custom dialog component in a Razor file (*DialogComponent.cshtml*):</span></span>

```cshtml
<div>
    <h2>@Title</h2>
    @BodyContent
    <button onclick=@OnOK>OK</button>
</div>

@functions {
    public string Title { get; set; }
    public RenderFragment BodyContent { get; set; }
    public Action OnOK { get; set; }
}
```

<span data-ttu-id="16211-142">Bu bileşen, uygulamada başka bir yerde kullanıldığında, IntelliSense tamamlama söz dizimi ve parametre ile geliştirme hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="16211-142">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="16211-143">Bileşenleri oluşturma DOM adlı tarayıcı bellek içi gösterimine bir *ağaç işleme* , ardından UI esnek ve verimli bir şekilde güncelleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="16211-143">Components render into an in-memory representation of the browser DOM called a *render tree* that can then be used to update the UI in a flexible and efficient way.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="16211-144">JavaScript ile birlikte çalışma</span><span class="sxs-lookup"><span data-stu-id="16211-144">JavaScript interop</span></span>

<span data-ttu-id="16211-145">Üçüncü taraf JavaScript kitaplıklarını ve API'lerini tarayıcı gerektiren uygulamalar için bileşenleri JavaScript ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="16211-145">For apps that require third-party JavaScript libraries and browser APIs, components interoperate with JavaScript.</span></span> <span data-ttu-id="16211-146">Herhangi bir kitaplığı veya JavaScript kullanabilmek için API kullanma yeteneği bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="16211-146">Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="16211-147">C#kod, JavaScript kodu çağırabilir ve JavaScript kod içine çağırabilir C# kod.</span><span class="sxs-lookup"><span data-stu-id="16211-147">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="16211-148">Daha fazla bilgi için [JavaScript birlikte çalışma](xref:razor-components/javascript-interop).</span><span class="sxs-lookup"><span data-stu-id="16211-148">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16211-149">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="16211-149">Additional resources</span></span>

* <xref:spa/blazor/index>
* [<span data-ttu-id="16211-150">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="16211-150">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="16211-151">C# Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="16211-151">C# Guide</span></span>](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [<span data-ttu-id="16211-152">HTML</span><span class="sxs-lookup"><span data-stu-id="16211-152">HTML</span></span>](https://www.w3.org/html/)
