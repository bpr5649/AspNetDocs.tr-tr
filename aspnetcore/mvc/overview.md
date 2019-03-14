---
title: ASP.NET Core MVC’ye Genel Bakış
author: ardalis
description: ASP.NET Core MVC web uygulamaları oluşturmaya yönelik zengin bir altyapı nasıl olduğunu öğrenin ve API'leri kullanarak Model-View-Controller tasarım deseni.
ms.author: riande
ms.date: 01/08/2018
uid: mvc/overview
ms.openlocfilehash: 205948cb45709b4eb6014aaf4960bf193a20dc30
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072459"
---
# <a name="overview-of-aspnet-core-mvc"></a><span data-ttu-id="4a2c4-103">ASP.NET Core MVC’ye Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4a2c4-103">Overview of ASP.NET Core MVC</span></span>

<span data-ttu-id="4a2c4-104">Tarafından [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="4a2c4-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="4a2c4-105">ASP.NET Core MVC web uygulamaları oluşturmaya yönelik zengin bir altyapı olan ve API'leri kullanarak Model-View-Controller tasarım deseni.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-105">ASP.NET Core MVC is a rich framework for building web apps and APIs using the Model-View-Controller design pattern.</span></span>

## <a name="what-is-the-mvc-pattern"></a><span data-ttu-id="4a2c4-106">MVC düzeni nedir?</span><span class="sxs-lookup"><span data-stu-id="4a2c4-106">What is the MVC pattern?</span></span>

<span data-ttu-id="4a2c4-107">Model-View-Controller (MVC) tasarım örüntüsü, uygulamanın üç ana bileşenleri gruplar halinde ayırır: Modelleri, görünümleri ve denetleyicileri.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-107">The Model-View-Controller (MVC) architectural pattern separates an application into three main groups of components: Models, Views, and Controllers.</span></span> <span data-ttu-id="4a2c4-108">Bu düzen, elde yardımcı olur [görev ayrımı nettir](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-108">This pattern helps to achieve [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns).</span></span> <span data-ttu-id="4a2c4-109">Bu düzeni kullanmak, kullanıcı isteklerini, kullanıcı eylemlerini gerçekleştirmek ve/veya sorguların sonuçlarını almak için modeli ile çalışmak için sorumlu denetleyicisi yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-109">Using this pattern, user requests are routed to a Controller which is responsible for working with the Model to perform user actions and/or retrieve results of queries.</span></span> <span data-ttu-id="4a2c4-110">Denetleyici kullanıcıya görüntülenecek görünüm seçer ve gerektirdiği modeli verilerle sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-110">The Controller chooses the View to display to the user, and provides it with any Model data it requires.</span></span>

<span data-ttu-id="4a2c4-111">Aşağıdaki diyagramda üç ana bileşenleri gösterilmektedir ve hangilerinin diğer başvuru:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-111">The following diagram shows the three main components and which ones reference the others:</span></span>

![MVC düzeni](overview/_static/mvc.png)

<span data-ttu-id="4a2c4-113">Bu kabul edilebilir açıklıkta sorumlulukları karmaşıklık açısından uygulama kodu, hata ayıklama ve sorun (model, görünüm veya denetleyicisi) tek bir iş olan test etmek daha kolay ölçeklendirme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-113">This delineation of responsibilities helps you scale the application in terms of complexity because it's easier to code, debug, and test something (model, view, or controller) that has a single job.</span></span> <span data-ttu-id="4a2c4-114">Bu güncelleştirme, test ve iki veya daha fazlası üç bu alanlar arasında yayılabilir bağımlılıkları olan hata ayıklama kodu daha zordur.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-114">It's more difficult to update, test, and debug code that has dependencies spread across two or more of these three areas.</span></span> <span data-ttu-id="4a2c4-115">Örneğin, kullanıcı arabirimi mantığı, iş mantığı daha sık değiştirmek için eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-115">For example, user interface logic tends to change more frequently than business logic.</span></span> <span data-ttu-id="4a2c4-116">Sunu kod ve iş mantığı tek bir nesnede birleştirildiğinde, kullanıcı arabirimi her değiştiğinde iş mantığı içeren bir nesne değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-116">If presentation code and business logic are combined in a single object, an object containing business logic must be modified every time the user interface is changed.</span></span> <span data-ttu-id="4a2c4-117">Bu genellikle hataları sunar ve iş mantığı her en düşük kullanıcı arabirimi değişiklikten sonra çözülüp gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-117">This often introduces errors and requires the retesting of business logic after every minimal user interface change.</span></span>

> [!NOTE]
> <span data-ttu-id="4a2c4-118">Hem görünümü hem de denetleyicisi modeline bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-118">Both the view and the controller depend on the model.</span></span> <span data-ttu-id="4a2c4-119">Ancak, model, görünüm ne denetleyici bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-119">However, the model depends on neither the view nor the controller.</span></span> <span data-ttu-id="4a2c4-120">Bu, ayrımı başlıca avantajlarından biridir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-120">This is one of the key benefits of the separation.</span></span> <span data-ttu-id="4a2c4-121">Bu ayrım modeli oluşturulan test edilmiş ve görsel sunumunu bağımsız sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-121">This separation allows the model to be built and tested independent of the visual presentation.</span></span>

### <a name="model-responsibilities"></a><span data-ttu-id="4a2c4-122">Model sorumlulukları</span><span class="sxs-lookup"><span data-stu-id="4a2c4-122">Model Responsibilities</span></span>

<span data-ttu-id="4a2c4-123">Bir MVC uygulamasında Model, uygulama ve iş mantığı veya tarafından yapılması gereken işlemlerin durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-123">The Model in an MVC application represents the state of the application and any business logic or operations that should be performed by it.</span></span> <span data-ttu-id="4a2c4-124">İş mantığı modelde, uygulamanın durumunu kalıcı hale getirmeniz için herhangi bir uygulama mantığı ile birlikte kapsüllenmiş.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-124">Business logic should be encapsulated in the model, along with any implementation logic for persisting the state of the application.</span></span> <span data-ttu-id="4a2c4-125">Kesin türü belirtilmiş görünümler, verileri içerecek şekilde tasarlanmış ViewModel türleri genellikle bu görünümde göstermek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-125">Strongly-typed views typically use ViewModel types designed to contain the data to display on that view.</span></span> <span data-ttu-id="4a2c4-126">Denetleyici oluşturur ve bu ViewModel örnekler modelinden doldurur.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-126">The controller creates and populates these ViewModel instances from the model.</span></span>

### <a name="view-responsibilities"></a><span data-ttu-id="4a2c4-127">Görünümünü Sorumluluklar</span><span class="sxs-lookup"><span data-stu-id="4a2c4-127">View Responsibilities</span></span>

<span data-ttu-id="4a2c4-128">Görünümler kullanıcı arabirimi aracılığıyla içerik sunmak için sorumlu olursunuz.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-128">Views are responsible for presenting content through the user interface.</span></span> <span data-ttu-id="4a2c4-129">Kullandıkları [Razor görünüm altyapısı](#razor-view-engine) HTML biçimlendirmesini ekleme .NET kodu için.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-129">They use the [Razor view engine](#razor-view-engine) to embed .NET code in HTML markup.</span></span> <span data-ttu-id="4a2c4-130">Görünümler içinde en az bir mantıksal olmalıdır ve bunlara herhangi bir mantık içerik sunmak için sebeple ilişkili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-130">There should be minimal logic within views, and any logic in them should relate to presenting content.</span></span> <span data-ttu-id="4a2c4-131">Harika bir fırsat mantığı görünümde gerçekleştirmek için gereken dosyaları bir karmaşık modeli verileri görüntülemek için fark ederseniz, kullanmayı bir [görünümü bileşen](views/view-components.md), ViewModel, ya da görünümü basitleştirmek için şablonu görüntüle.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-131">If you find the need to perform a great deal of logic in view files in order to display data from a complex model, consider using a [View Component](views/view-components.md), ViewModel, or view template to simplify the view.</span></span>

### <a name="controller-responsibilities"></a><span data-ttu-id="4a2c4-132">Denetleyici sorumlulukları</span><span class="sxs-lookup"><span data-stu-id="4a2c4-132">Controller Responsibilities</span></span>

<span data-ttu-id="4a2c4-133">Denetleyicileri, kullanıcı etkileşimi işlemek, modelle çalışan ve sonuç olarak işlemek için bir görünüm seçin bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-133">Controllers are the components that handle user interaction, work with the model, and ultimately select a view to render.</span></span> <span data-ttu-id="4a2c4-134">Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; Denetleyici, işler ve kullanıcı girişini ve etkileşimini yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-134">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span> <span data-ttu-id="4a2c4-135">MVC örüntüsü, denetleyici ilk giriş noktasıdır ve hangi modelle çalışmak için türleri ve işlemek için hangi görünümün seçmek için sorumludur (Bu nedenle adını - denetimleri uygulama için belirtilen bir isteğin nasıl yanıt vereceğini).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-135">In the MVC pattern, the controller is the initial entry point, and is responsible for selecting which model types to work with and which view to render (hence its name - it controls how the app responds to a given request).</span></span>

> [!NOTE]
> <span data-ttu-id="4a2c4-136">Denetleyicileri, çok fazla sorumluluklara göre aşırı karmaşık olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-136">Controllers shouldn't be overly complicated by too many responsibilities.</span></span> <span data-ttu-id="4a2c4-137">Fazla karmaşık hale gelmesini denetleyicisi mantıksal tutmak için iş mantığı denetleyicisi dışında ve etki alanı modeline gönderin.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-137">To keep controller logic from becoming overly complex, push business logic out of the controller and into the domain model.</span></span>

>[!TIP]
> <span data-ttu-id="4a2c4-138">Denetleyici eylemleri sık aynı tür eylemler gerçekleştirmek bulursanız, bu ortak Eylemler içine Taşı [filtreleri](#filters).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-138">If you find that your controller actions frequently perform the same kinds of actions, move these common actions into [filters](#filters).</span></span>

## <a name="what-is-aspnet-core-mvc"></a><span data-ttu-id="4a2c4-139">ASP.NET Core MVC nedir</span><span class="sxs-lookup"><span data-stu-id="4a2c4-139">What is ASP.NET Core MVC</span></span>

<span data-ttu-id="4a2c4-140">ASP.NET Core MVC, bir basit, açık kaynaklı bir ASP.NET Core ile kullanılmak için iyileştirilmiş yüksek düzeyde sınanabilir bir sunu çerçevesidir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-140">The ASP.NET Core MVC framework is a lightweight, open source, highly testable presentation framework optimized for use with ASP.NET Core.</span></span>

<span data-ttu-id="4a2c4-141">ASP.NET Core MVC, ilgilenilecek alanların temiz bir biçimde ayrılmasını sağlayan dinamik Web siteleri oluşturmak için desen tabanlı bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-141">ASP.NET Core MVC provides a patterns-based way to build dynamic websites that enables a clean separation of concerns.</span></span> <span data-ttu-id="4a2c4-142">İşaretleme üzerinde tam denetim verir, TDD kullanımı kolay geliştirme destekler ve en son web standartlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-142">It gives you full control over markup, supports TDD-friendly development and uses the latest web standards.</span></span>

## <a name="features"></a><span data-ttu-id="4a2c4-143">Özellikler</span><span class="sxs-lookup"><span data-stu-id="4a2c4-143">Features</span></span>

<span data-ttu-id="4a2c4-144">ASP.NET Core MVC aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-144">ASP.NET Core MVC includes the following:</span></span>

* [<span data-ttu-id="4a2c4-145">Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="4a2c4-145">Routing</span></span>](#routing)
* [<span data-ttu-id="4a2c4-146">Model bağlama</span><span class="sxs-lookup"><span data-stu-id="4a2c4-146">Model binding</span></span>](#model-binding)
* [<span data-ttu-id="4a2c4-147">Model doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4a2c4-147">Model validation</span></span>](#model-validation)
* [<span data-ttu-id="4a2c4-148">Bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="4a2c4-148">Dependency injection</span></span>](../fundamentals/dependency-injection.md)
* [<span data-ttu-id="4a2c4-149">Filtreler</span><span class="sxs-lookup"><span data-stu-id="4a2c4-149">Filters</span></span>](#filters)
* [<span data-ttu-id="4a2c4-150">Alanlar</span><span class="sxs-lookup"><span data-stu-id="4a2c4-150">Areas</span></span>](#areas)
* [<span data-ttu-id="4a2c4-151">Web API'leri</span><span class="sxs-lookup"><span data-stu-id="4a2c4-151">Web APIs</span></span>](#web-apis)
* [<span data-ttu-id="4a2c4-152">Test Edilebilirlik</span><span class="sxs-lookup"><span data-stu-id="4a2c4-152">Testability</span></span>](#testability)
* [<span data-ttu-id="4a2c4-153">Razor görünüm altyapısı</span><span class="sxs-lookup"><span data-stu-id="4a2c4-153">Razor view engine</span></span>](#razor-view-engine)
* [<span data-ttu-id="4a2c4-154">Kesin türü belirtilmiş görünümler</span><span class="sxs-lookup"><span data-stu-id="4a2c4-154">Strongly typed views</span></span>](#strongly-typed-views)
* [<span data-ttu-id="4a2c4-155">Etiket Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="4a2c4-155">Tag Helpers</span></span>](#tag-helpers)
* [<span data-ttu-id="4a2c4-156">Görünüm bileşenleri</span><span class="sxs-lookup"><span data-stu-id="4a2c4-156">View Components</span></span>](#view-components)

### <a name="routing"></a><span data-ttu-id="4a2c4-157">Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="4a2c4-157">Routing</span></span>

<span data-ttu-id="4a2c4-158">ASP.NET Core MVC üzerine kurulmuştur [ASP.NET Core'nın Yönlendirme](../fundamentals/routing.md), olanak tanıyan güçlü bir URL eşlemesi bileşeni, anlaşılabilir ve aranabilir URL'lere sahip uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-158">ASP.NET Core MVC is built on top of [ASP.NET Core's routing](../fundamentals/routing.md), a powerful URL-mapping component that lets you build applications that have comprehensible and searchable URLs.</span></span> <span data-ttu-id="4a2c4-159">Bu, web sunucunuzdaki dosyaları nasıl düzenlendiği için bakmadan bağlantı oluşturma ve arama motoru iyileştirmesi (SEO) için iyi iş uygulamanızın URL adlandırma modelleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-159">This enables you to define your application's URL naming patterns that work well for search engine optimization (SEO) and for link generation, without regard for how the files on your web server are organized.</span></span> <span data-ttu-id="4a2c4-160">Rota değeri kısıtlamaları, Varsayılanları ve isteğe bağlı değerler destekleyen bir kullanışlı bir yol şablonu söz dizimini kullanarak yollarınızı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-160">You can define your routes using a convenient route template syntax that supports route value constraints, defaults and optional values.</span></span>

<span data-ttu-id="4a2c4-161">*Kural tabanlı yönlendirme* genel URL tanımlamanızı biçimleri sağlar, uygulamanızın kabul eder ve her birini nasıl biçimlendirir belirli bir eylem yöntemine üzerinde denetleyici eşler.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-161">*Convention-based routing* enables you to globally define the URL formats that your application accepts and how each of those formats maps to a specific action method on given controller.</span></span> <span data-ttu-id="4a2c4-162">Gelen bir istek alındığında, yönlendirme altyapısını URL ayrıştırır ve tanımlanmış URL biçimlerinden biri kendisine eşleşir ve ardından ilişkili denetleyicinin eylem yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-162">When an incoming request is received, the routing engine parses the URL and matches it to one of the defined URL formats, and then calls the associated controller's action method.</span></span>

```csharp
routes.MapRoute(name: "Default", template: "{controller=Home}/{action=Index}/{id?}");
```

<span data-ttu-id="4a2c4-163">*Öznitelik yönlendirme* denetleyici ve Eylemler, uygulamanızın yollar tanımlayan öznitelikleri ile tasarlayarak yönlendirme bilgilerini belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-163">*Attribute routing* enables you to specify routing information by decorating your controllers and actions with attributes that define your application's routes.</span></span> <span data-ttu-id="4a2c4-164">Başka bir deyişle, denetleyici ve eylem ile ilişkili oldukları yanındaki rota tanımlarınızı yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-164">This means that your route definitions are placed next to the controller and action with which they're associated.</span></span>

```csharp
[Route("api/[controller]")]
public class ProductsController : Controller
{
  [HttpGet("{id}")]
  public IActionResult GetProduct(int id)
  {
    ...
  }
}
```

### <a name="model-binding"></a><span data-ttu-id="4a2c4-165">Model bağlama</span><span class="sxs-lookup"><span data-stu-id="4a2c4-165">Model binding</span></span>

<span data-ttu-id="4a2c4-166">ASP.NET Core MVC [model bağlama](models/model-binding.md) istemci isteği verilerini (form değerleri, rota verileri, sorgu dizesi parametreleri, HTTP üst bilgileri) denetleyicisi işleyebileceği nesnelerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-166">ASP.NET Core MVC [model binding](models/model-binding.md) converts client request data  (form values, route data, query string parameters, HTTP headers) into objects that the controller can handle.</span></span> <span data-ttu-id="4a2c4-167">Sonuç olarak, denetleyici mantığınızı gelen istek verileri başarınızda yapması gerekmez; yalnızca kendi eylem yöntemlerine parametre olarak veri yok.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-167">As a result, your controller logic doesn't have to do the work of figuring out the incoming request data; it simply has the data as parameters to its action methods.</span></span>

```csharp
public async Task<IActionResult> Login(LoginViewModel model, string returnUrl = null) { ... }
   ```

### <a name="model-validation"></a><span data-ttu-id="4a2c4-168">Model doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4a2c4-168">Model validation</span></span>

<span data-ttu-id="4a2c4-169">ASP.NET Core MVC destekler [doğrulama](models/validation.md) modeli nesnenizle veri ek açıklama doğrulama özniteliklerinin dekorasyon olarak.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-169">ASP.NET Core MVC supports [validation](models/validation.md) by decorating your model object with data annotation validation attributes.</span></span> <span data-ttu-id="4a2c4-170">Doğrulama özniteliklerinin değerleri sunucuya gönderilen önce istemci tarafında denetlenir yanı denetleyici eylemini önce sunucu üzerinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-170">The validation attributes are checked on the client side before values are posted to the server, as well as on the server before the controller action is called.</span></span>

```csharp
using System.ComponentModel.DataAnnotations;
public class LoginViewModel
{
    [Required]
    [EmailAddress]
    public string Email { get; set; }

    [Required]
    [DataType(DataType.Password)]
    public string Password { get; set; }

    [Display(Name = "Remember me?")]
    public bool RememberMe { get; set; }
}
```

<span data-ttu-id="4a2c4-171">Bir denetleyici eylemi:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-171">A controller action:</span></span>

```csharp
public async Task<IActionResult> Login(LoginViewModel model, string returnUrl = null)
{
    if (ModelState.IsValid)
    {
      // work with the model
    }
    // At this point, something failed, redisplay form
    return View(model);
}
```

<span data-ttu-id="4a2c4-172">Çerçeve doğrulama isteği verileri istemci ve sunucu işler.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-172">The framework handles validating request data both on the client and on the server.</span></span> <span data-ttu-id="4a2c4-173">Belirtilen model türleri üzerinde doğrulama mantığı işlenmiş görünüm örtük ek açıklamaları olarak eklenir ve tarayıcı ile zorlanır [jQuery doğrulaması](https://jqueryvalidation.org/).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-173">Validation logic specified on model types is added to the rendered views as unobtrusive annotations and is enforced in the browser with [jQuery Validation](https://jqueryvalidation.org/).</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="4a2c4-174">Bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="4a2c4-174">Dependency injection</span></span>

<span data-ttu-id="4a2c4-175">ASP.NET Core için yerleşik desteği vardır [bağımlılık ekleme (dı)](../fundamentals/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-175">ASP.NET Core has built-in support for [dependency injection (DI)](../fundamentals/dependency-injection.md).</span></span> <span data-ttu-id="4a2c4-176">ASP.NET Core MVC, [denetleyicileri](controllers/dependency-injection.md) istek gerekli hizmetleri aracılığıyla bunları izlemek izin verme oluşturucuları, [açık bağımlılıkları ilkesine](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-176">In ASP.NET Core MVC, [controllers](controllers/dependency-injection.md) can request needed services through their constructors, allowing them to follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span></span>

<span data-ttu-id="4a2c4-177">Uygulamanızı kullanabilirsiniz [görünümünde bağımlılık ekleme dosyaları](views/dependency-injection.md)kullanarak `@inject` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-177">Your app can also use [dependency injection in view files](views/dependency-injection.md), using the `@inject` directive:</span></span>

```cshtml
@inject SomeService ServiceName
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ServiceName.GetTitle</title>
</head>
<body>
    <h1>@ServiceName.GetTitle</h1>
</body>
</html>
```

### <a name="filters"></a><span data-ttu-id="4a2c4-178">FilTReleri</span><span class="sxs-lookup"><span data-stu-id="4a2c4-178">Filters</span></span>

<span data-ttu-id="4a2c4-179">[Filtreler](controllers/filters.md) özel durum işleme veya yetkilendirme gibi çapraz kesme konuları kapsülleyen geliştiricilerin yardımcı.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-179">[Filters](controllers/filters.md) help developers encapsulate cross-cutting concerns, like exception handling or authorization.</span></span> <span data-ttu-id="4a2c4-180">Filtreleri eylem yöntemleri için çalışan özel öncesi ve sonrası işleme mantığı etkinleştirmek ve belirli bir istek için yürütme işlem hattı içindeki bazı noktalarda çalıştırmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-180">Filters enable running custom pre- and post-processing logic for action methods, and can be configured to run at certain points within the execution pipeline for a given request.</span></span> <span data-ttu-id="4a2c4-181">Filtreler denetleyicileri veya öznitelikleri eylemleri uygulanabilir (veya genel olarak çalıştırılabilir).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-181">Filters can be applied to controllers or actions as attributes (or can be run globally).</span></span> <span data-ttu-id="4a2c4-182">Birkaç filtreleri (gibi `Authorize`) Framework'e dahil edilen.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-182">Several filters (such as `Authorize`) are included in the framework.</span></span> <span data-ttu-id="4a2c4-183">`[Authorize]` MVC yetkilendirme filtrelerini oluşturmak için kullanılan özniteliğidir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-183">`[Authorize]` is the attribute that is used to create MVC authorization filters.</span></span>

```csharp
[Authorize]
   public class AccountController : Controller
   {
```

### <a name="areas"></a><span data-ttu-id="4a2c4-184">Alanlar</span><span class="sxs-lookup"><span data-stu-id="4a2c4-184">Areas</span></span>

<span data-ttu-id="4a2c4-185">[Alanları](controllers/areas.md) büyük bir ASP.NET Core MVC Web uygulaması işlevsel gruplamalarda daha küçük bölümlere ayırmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-185">[Areas](controllers/areas.md) provide a way to partition a large ASP.NET Core MVC Web app into smaller functional groupings.</span></span> <span data-ttu-id="4a2c4-186">Bir alan, bir uygulama içinde bir MVC yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-186">An area is an MVC structure inside an application.</span></span> <span data-ttu-id="4a2c4-187">Bir MVC projesi mantıksal bileşenler modeli, denetleyici ve görünüm gibi farklı klasörlerde tutulur ve MVC bu bileşenler arasındaki ilişki oluşturmak için adlandırma kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-187">In an MVC project, logical components like Model, Controller, and View are kept in different folders, and MVC uses naming conventions to create the relationship between these components.</span></span> <span data-ttu-id="4a2c4-188">Büyük bir uygulama için ayrı yüksek düzey alanlarına işlev uygulamasını bölümleme için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-188">For a large app, it may be advantageous to partition the app into separate high level areas of functionality.</span></span> <span data-ttu-id="4a2c4-189">Örneğin, bir e-ticaret uygulamayla kullanıma alma ve faturalandırma arama vb. gibi birden çok iş birimleri. Bu birimlerin her biri kendi mantıksal bileşen görünümleri, denetleyicilere ve modelleri sahip.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-189">For instance, an e-commerce app with multiple business units, such as checkout, billing, and search etc. Each of these units have their own logical component views, controllers, and models.</span></span>

### <a name="web-apis"></a><span data-ttu-id="4a2c4-190">Web API'leri</span><span class="sxs-lookup"><span data-stu-id="4a2c4-190">Web APIs</span></span>

<span data-ttu-id="4a2c4-191">ASP.NET Core MVC, web siteleri oluşturmak için harika bir platform olmaya ek olarak, Web API'leri oluşturmaya yönelik harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-191">In addition to being a great platform for building web sites, ASP.NET Core MVC has great support for building Web APIs.</span></span> <span data-ttu-id="4a2c4-192">Bir çeşit tarayıcılar ve mobil cihazlar dahil olmak üzere istemciye ulaşan hizmetler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-192">You can build services that reach a broad range of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="4a2c4-193">HTTP İçerik anlaşma desteği için yerleşik destekle framework içerir [veri biçimlendirme](xref:web-api/advanced/formatting) JSON veya XML.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-193">The framework includes support for HTTP content-negotiation with built-in support to [format data](xref:web-api/advanced/formatting) as JSON or XML.</span></span> <span data-ttu-id="4a2c4-194">Yazma [özel biçimlendiriciler](xref:web-api/advanced/custom-formatters) kendi biçimleri için destek eklemek için.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-194">Write [custom formatters](xref:web-api/advanced/custom-formatters) to add support for your own formats.</span></span>

<span data-ttu-id="4a2c4-195">Bağlantı oluşturma, Hiper medyayı desteğini etkinleştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-195">Use link generation to enable support for hypermedia.</span></span> <span data-ttu-id="4a2c4-196">Kolayca desteğini etkinleştirme [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/) böylece Web API'leri, birden çok Web uygulaması arasında paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-196">Easily enable support for [cross-origin resource sharing (CORS)](http://www.w3.org/TR/cors/) so that your Web APIs can be shared across multiple Web applications.</span></span>

### <a name="testability"></a><span data-ttu-id="4a2c4-197">Test Edilebilirlik</span><span class="sxs-lookup"><span data-stu-id="4a2c4-197">Testability</span></span>

<span data-ttu-id="4a2c4-198">Framework'ün kullanımını arabirimleri ve bağımlılık ekleme kılmaktadır için birim testi ve framework, Özellikler (örneğin, Entity Framework için TestHost ve Inmemory sağlayıcısı) içerir [tümleştirme testleri](xref:test/integration-tests) hızlı ve kolay de.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-198">The framework's use of interfaces and dependency injection make it well-suited to unit testing, and the framework includes features (like a TestHost and InMemory provider for Entity Framework) that make [integration tests](xref:test/integration-tests) quick and easy as well.</span></span> <span data-ttu-id="4a2c4-199">Daha fazla bilgi edinin [denetleyicisi mantıksal test etme](controllers/testing.md).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-199">Learn more about [how to test controller logic](controllers/testing.md).</span></span>

### <a name="razor-view-engine"></a><span data-ttu-id="4a2c4-200">Razor görünüm altyapısı</span><span class="sxs-lookup"><span data-stu-id="4a2c4-200">Razor view engine</span></span>

<span data-ttu-id="4a2c4-201">[ASP.NET Core MVC görünümleri](views/overview.md) kullanın [Razor görünüm altyapısı](views/razor.md) görünüm işlemek için.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-201">[ASP.NET Core MVC views](views/overview.md) use the [Razor view engine](views/razor.md) to render views.</span></span> <span data-ttu-id="4a2c4-202">Razor, katıştırılmış C# kodunu kullanarak görünümlerini tanımlamak için bir compact, ifadesel ve akıcı şablon biçimlendirme dilidir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-202">Razor is a compact, expressive and fluid template markup language for defining views using embedded C# code.</span></span> <span data-ttu-id="4a2c4-203">Razor, web içeriği sunucusundaki dinamik olarak oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-203">Razor is used to dynamically generate web content on the server.</span></span> <span data-ttu-id="4a2c4-204">Sunucu kodu, istemci tarafı içeriği ve kod ile düzgün bir şekilde karıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-204">You can cleanly mix server code with client side content and code.</span></span>

```text
<ul>
  @for (int i = 0; i < 5; i++) {
    <li>List item @i</li>
  }
</ul>
```

<span data-ttu-id="4a2c4-205">Tanımlayabilirsiniz Razor görünüm altyapısı kullanılarak [düzenleri](views/layout.md), [kısmi görünümler](views/partial.md) ve bölümleri değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-205">Using the Razor view engine you can define [layouts](views/layout.md), [partial views](views/partial.md) and replaceable sections.</span></span>

### <a name="strongly-typed-views"></a><span data-ttu-id="4a2c4-206">Kesin türü belirtilmiş görünümler</span><span class="sxs-lookup"><span data-stu-id="4a2c4-206">Strongly typed views</span></span>

<span data-ttu-id="4a2c4-207">MVC Razor görünümleri, modelinize göre türü kesin olarak.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-207">Razor views in MVC can be strongly typed based on your model.</span></span> <span data-ttu-id="4a2c4-208">Denetleyicileri tür denetlemesi ve IntelliSense desteği sağlamak kendi görünümlerinizi etkinleştirme görünüme kesin türü belirtilmiş bir model geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-208">Controllers can pass a strongly typed model to views enabling your views to have type checking and IntelliSense support.</span></span>

<span data-ttu-id="4a2c4-209">Örneğin, bir türü modelin aşağıdaki görünümü işleyen `IEnumerable<Product>`:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-209">For example, the following view renders a model of type `IEnumerable<Product>`:</span></span>

```cshtml
@model IEnumerable<Product>
<ul>
    @foreach (Product p in Model)
    {
        <li>@p.Name</li>
    }
</ul>
```

### <a name="tag-helpers"></a><span data-ttu-id="4a2c4-210">Etiket Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="4a2c4-210">Tag Helpers</span></span>

<span data-ttu-id="4a2c4-211">[Etiket Yardımcıları](views/tag-helpers/intro.md) sunucu tarafı kodu oluşturma ve Razor dosyalarında HTML öğeleri işleme katılmak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-211">[Tag Helpers](views/tag-helpers/intro.md) enable server side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="4a2c4-212">Etiket Yardımcıları özel etiketler tanımlamak için kullanabilirsiniz (örneğin, `<environment>`) veya mevcut olan etiketlerin davranışını değiştirmek için (örneğin, `<label>`).</span><span class="sxs-lookup"><span data-stu-id="4a2c4-212">You can use tag helpers to define custom tags (for example, `<environment>`) or to modify the behavior of existing tags (for example, `<label>`).</span></span> <span data-ttu-id="4a2c4-213">Etiket Yardımcıları öğe adı ve öznitelikleri temel alan belirli öğeleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-213">Tag Helpers bind to specific elements based on the element name and its attributes.</span></span> <span data-ttu-id="4a2c4-214">Bunlar, bir HTML düzenleme deneyimi hala korurken, sunucu tarafı işleme avantajlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-214">They provide the benefits of server-side rendering while still preserving an HTML editing experience.</span></span>

<span data-ttu-id="4a2c4-215">Birçok yerleşik etiket Yardımcıları için formlar, bağlantılar, yükleme varlıklar ve ortak GitHub depoları ve NuGet olarak daha kullanılabilir ve daha fazla - paketleri oluşturma gibi ortak görevler - vardır.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-215">There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.</span></span> <span data-ttu-id="4a2c4-216">Etiket Yardımcıları C# dilinde yazılmış ve öğe adı, öznitelik adı veya üst etiketi dayalı HTML öğeleri hedeflenir.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-216">Tag Helpers are authored in C#, and they target HTML elements based on element name, attribute name, or parent tag.</span></span> <span data-ttu-id="4a2c4-217">Örneğin, LinkTagHelper bağlantısı oluşturmak için kullanılabilir yerleşik `Login` eylemi `AccountsController`:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-217">For example, the built-in LinkTagHelper can be used to create a link to the `Login` action of the `AccountsController`:</span></span>

```cshtml
<p>
    Thank you for confirming your email.
    Please <a asp-controller="Account" asp-action="Login">Click here to Log in</a>.
</p>
```

<span data-ttu-id="4a2c4-218">`EnvironmentTagHelper` Farklı betikler görünümleriniz (örneğin, ham veya küçültülmüş) çalışma zamanı ortamı, geliştirme, hazırlama veya üretim gibi temel dahil etmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4a2c4-218">The `EnvironmentTagHelper` can be used to include different scripts in your views (for example, raw or minified) based on the runtime environment, such as Development, Staging, or Production:</span></span>

```cshtml
<environment names="Development">
    <script src="~/lib/jquery/dist/jquery.js"></script>
</environment>
<environment names="Staging,Production">
    <script src="https://ajax.aspnetcdn.com/ajax/jquery/jquery-2.1.4.min.js"
            asp-fallback-src="~/lib/jquery/dist/jquery.min.js"
            asp-fallback-test="window.jQuery">
    </script>
</environment>
```

<span data-ttu-id="4a2c4-219">Etiket Yardımcıları, bir HTML kullanımı kolay geliştirme deneyimi ve HTML ve Razor biçimlendirme oluşturmak için zengin IntelliSense ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-219">Tag Helpers provide an HTML-friendly development experience and a rich IntelliSense environment for creating HTML and Razor markup.</span></span> <span data-ttu-id="4a2c4-220">Yerleşik etiket Yardımcıları çoğu mevcut HTML öğeleri hedef ve öğe için sunucu tarafı öznitelikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-220">Most of the built-in Tag Helpers target existing HTML elements and provide server-side attributes for the element.</span></span>

### <a name="view-components"></a><span data-ttu-id="4a2c4-221">Görünüm bileşenleri</span><span class="sxs-lookup"><span data-stu-id="4a2c4-221">View Components</span></span>

<span data-ttu-id="4a2c4-222">[Görüntüleme bileşenleri](views/view-components.md) işleme mantığının paketleyin ve uygulamanın tamamında yeniden olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-222">[View Components](views/view-components.md) allow you to package rendering logic and reuse it throughout the application.</span></span> <span data-ttu-id="4a2c4-223">Benzer şekilde oldukları [kısmi görünümler](views/partial.md), ancak ilişkili mantığı.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-223">They're similar to [partial views](views/partial.md), but with associated logic.</span></span>

## <a name="compatibility-version"></a><span data-ttu-id="4a2c4-224">Uyumluluk sürümü</span><span class="sxs-lookup"><span data-stu-id="4a2c4-224">Compatibility version</span></span>

<span data-ttu-id="4a2c4-225"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> Yöntemi kabul etme veya potansiyel olarak davranışı sunulan içinde ASP.NET Core MVC 2.1 veya üzeri bozucu değişiklikler çevirme için bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-225">The <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET Core MVC 2.1 or later.</span></span>

<span data-ttu-id="4a2c4-226">Daha fazla bilgi için bkz. <xref:mvc/compatibility-version>.</span><span class="sxs-lookup"><span data-stu-id="4a2c4-226">For more information, see <xref:mvc/compatibility-version>.</span></span>
