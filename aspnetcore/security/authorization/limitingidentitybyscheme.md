---
title: ASP.NET core'da belirli bir düzeni ile yetkilendirme
author: rick-anderson
description: Bu makalede, birden çok kimlik doğrulama yöntemleri ile çalışırken, belirli bir düzen kimliğini sınırlamak açıklanmaktadır.
ms.author: riande
ms.date: 10/22/2018
uid: security/authorization/limitingidentitybyscheme
ms.openlocfilehash: 778bb61f472ab2e76f85da5999d3c79238188f19
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076503"
---
# <a name="authorize-with-a-specific-scheme-in-aspnet-core"></a><span data-ttu-id="b9759-103">ASP.NET core'da belirli bir düzeni ile yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b9759-103">Authorize with a specific scheme in ASP.NET Core</span></span>

<span data-ttu-id="b9759-104">Tek sayfa uygulamaları (Spa'lar) gibi bazı senaryolarda birden çok kimlik doğrulama yöntemleri kullanan yaygındır.</span><span class="sxs-lookup"><span data-stu-id="b9759-104">In some scenarios, such as Single Page Applications (SPAs), it's common to use multiple authentication methods.</span></span> <span data-ttu-id="b9759-105">Örneğin, uygulama oturum açma tanımlama bilgisi tabanlı kimlik doğrulaması ve JWT taşıyıcı kimlik doğrulaması için JavaScript istekleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b9759-105">For example, the app may use cookie-based authentication to log in and JWT bearer authentication for JavaScript requests.</span></span> <span data-ttu-id="b9759-106">Bazı durumlarda, uygulama birden fazla örneğini bir kimlik doğrulama işleyicisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9759-106">In some cases, the app may have multiple instances of an authentication handler.</span></span> <span data-ttu-id="b9759-107">Örneğin, iki tanımlama bilgisi işleyicileri burada temel bir kimlik içerir ve bir oluşturulduğunda bir multi-Factor authentication (MFA) tetiklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="b9759-107">For example, two cookie handlers where one contains a basic identity and one is created when a multi-factor authentication (MFA) has been triggered.</span></span> <span data-ttu-id="b9759-108">Kullanıcıya ek güvenlik gerektiren bir işlem istediğinden MFA tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b9759-108">MFA may be triggered because the user requested an operation that requires extra security.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b9759-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b9759-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b9759-110">Kimlik doğrulaması sırasında kimlik doğrulama hizmeti tarafından yapılandırıldığında bir kimlik doğrulama düzeni olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b9759-110">An authentication scheme is named when the authentication service is configured during authentication.</span></span> <span data-ttu-id="b9759-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b9759-111">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication()
        .AddCookie(options => {
            options.LoginPath = "/Account/Unauthorized/";
            options.AccessDeniedPath = "/Account/Forbidden/";
        })
        .AddJwtBearer(options => {
            options.Audience = "http://localhost:5001/";
            options.Authority = "http://localhost:5000/";
        });
```

<span data-ttu-id="b9759-112">Önceki kodda, iki kimlik doğrulaması işleyici eklendi: biri tanımlama bilgileri, diğeri taşıyıcı için.</span><span class="sxs-lookup"><span data-stu-id="b9759-112">In the preceding code, two authentication handlers have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="b9759-113">Varsayılan düzenini belirten sonuçlanıyor `HttpContext.User` kimliğe ayarlanan özelliği.</span><span class="sxs-lookup"><span data-stu-id="b9759-113">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="b9759-114">Bu davranışı gerekli değildir, parametresiz derleyeceği harekete geçirerek devre dışı `AddAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="b9759-114">If that behavior isn't desired, disable it by invoking the parameterless form of `AddAuthentication`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b9759-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b9759-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b9759-116">Kimlik doğrulaması sırasında kimlik doğrulaması middlewares yapılandırıldığında kimlik doğrulama düzeni olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b9759-116">Authentication schemes are named when authentication middlewares are configured during authentication.</span></span> <span data-ttu-id="b9759-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b9759-117">For example:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // Code omitted for brevity

    app.UseCookieAuthentication(new CookieAuthenticationOptions()
    {
        AuthenticationScheme = "Cookie",
        LoginPath = "/Account/Unauthorized/",
        AccessDeniedPath = "/Account/Forbidden/",
        AutomaticAuthenticate = false
    });
    
    app.UseJwtBearerAuthentication(new JwtBearerOptions()
    {
        AuthenticationScheme = "Bearer",
        AutomaticAuthenticate = false,
        Audience = "http://localhost:5001/",
        Authority = "http://localhost:5000/",
        RequireHttpsMetadata = false
    });
```

<span data-ttu-id="b9759-118">Önceki kodda, iki kimlik doğrulaması middlewares eklenmiştir: biri tanımlama bilgileri, diğeri taşıyıcı için.</span><span class="sxs-lookup"><span data-stu-id="b9759-118">In the preceding code, two authentication middlewares have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="b9759-119">Varsayılan düzenini belirten sonuçlanıyor `HttpContext.User` kimliğe ayarlanan özelliği.</span><span class="sxs-lookup"><span data-stu-id="b9759-119">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="b9759-120">Bu davranışı gerekli değildir, ayarı devre dışı `AuthenticationOptions.AutomaticAuthenticate` özelliğini `false`.</span><span class="sxs-lookup"><span data-stu-id="b9759-120">If that behavior isn't desired, disable it by setting the `AuthenticationOptions.AutomaticAuthenticate` property to `false`.</span></span>

---

## <a name="selecting-the-scheme-with-the-authorize-attribute"></a><span data-ttu-id="b9759-121">Authorize özniteliği düzeni seçme</span><span class="sxs-lookup"><span data-stu-id="b9759-121">Selecting the scheme with the Authorize attribute</span></span>

<span data-ttu-id="b9759-122">Yetkilendirme noktasında kullanılacak işleyici uygulamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9759-122">At the point of authorization, the app indicates the handler to be used.</span></span> <span data-ttu-id="b9759-123">Uygulama ile yetkilendirmek için kimlik doğrulama düzenleri, virgülle ayrılmış listesini geçirerek işleyiciyi seçin `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="b9759-123">Select the handler with which the app will authorize by passing a comma-delimited list of authentication schemes to `[Authorize]`.</span></span> <span data-ttu-id="b9759-124">`[Authorize]` Kimlik doğrulama düzeni veya düzenleri varsayılan yapılandırılmış bağımsız olarak kullanılacak özniteliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="b9759-124">The `[Authorize]` attribute specifies the authentication scheme or schemes to use regardless of whether a default is configured.</span></span> <span data-ttu-id="b9759-125">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b9759-125">For example:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b9759-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b9759-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b9759-127">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b9759-127">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

---

<span data-ttu-id="b9759-128">Yukarıdaki örnekte tanımlama bilgisi ve taşıyıcı işleyicileri çalıştırın ve oluşturun ve geçerli kullanıcı için bir kimlik eklenecek şansına sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9759-128">In the preceding example, both the cookie and bearer handlers run and have a chance to create and append an identity for the current user.</span></span> <span data-ttu-id="b9759-129">Yalnızca tek bir düzen belirterek, karşılık gelen işleyici çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b9759-129">By specifying a single scheme only, the corresponding handler runs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b9759-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b9759-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b9759-131">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b9759-131">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

---

<span data-ttu-id="b9759-132">Önceki kodda; yalnızca işleyici "Bearer" düzeni ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9759-132">In the preceding code, only the handler with the "Bearer" scheme runs.</span></span> <span data-ttu-id="b9759-133">Tanımlama bilgisi tabanlı hiç kimlik yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="b9759-133">Any cookie-based identities are ignored.</span></span>

## <a name="selecting-the-scheme-with-policies"></a><span data-ttu-id="b9759-134">İlkeleriyle düzenini seçme</span><span class="sxs-lookup"><span data-stu-id="b9759-134">Selecting the scheme with policies</span></span>

<span data-ttu-id="b9759-135">İstenen düzenleri belirtmek istiyorsanız [ilke](xref:security/authorization/policies), ayarlayabileceğiniz `AuthenticationSchemes` ilkenizi eklerken koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="b9759-135">If you prefer to specify the desired schemes in [policy](xref:security/authorization/policies), you can set the `AuthenticationSchemes` collection when adding your policy:</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("Over18", policy =>
    {
        policy.AuthenticationSchemes.Add(JwtBearerDefaults.AuthenticationScheme);
        policy.RequireAuthenticatedUser();
        policy.Requirements.Add(new MinimumAgeRequirement());
    });
});
```

<span data-ttu-id="b9759-136">Önceki örnekte, "Over18" ilke karşı "Bearer" işleyicisi tarafından oluşturulan kimlik yalnızca çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9759-136">In the preceding example, the "Over18" policy only runs against the identity created by the "Bearer" handler.</span></span> <span data-ttu-id="b9759-137">Bir ilke ayarlayarak kullanın `[Authorize]` özniteliğin `Policy` özelliği:</span><span class="sxs-lookup"><span data-stu-id="b9759-137">Use the policy by setting the `[Authorize]` attribute's `Policy` property:</span></span>

```csharp
[Authorize(Policy = "Over18")]
public class RegistrationController : Controller
```

::: moniker range=">= aspnetcore-2.0"

## <a name="use-multiple-authentication-schemes"></a><span data-ttu-id="b9759-138">Birden fazla kimlik doğrulama şeması kullanma</span><span class="sxs-lookup"><span data-stu-id="b9759-138">Use multiple authentication schemes</span></span>

<span data-ttu-id="b9759-139">Bazı uygulamalar birden çok kimlik doğrulama türlerini desteklemek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b9759-139">Some apps may need to support multiple types of authentication.</span></span> <span data-ttu-id="b9759-140">Örneğin, uygulamanız kullanıcıların Azure Active Directory'den ve kullanıcıların veritabanından kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b9759-140">For example, your app might authenticate users from Azure Active Directory and from a users database.</span></span> <span data-ttu-id="b9759-141">Başka bir örnek, hem Active Directory Federasyon Hizmetleri, hem de Azure Active Directory B2C kullanıcılarının kimliğini doğrulayan bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="b9759-141">Another example is an app that authenticates users from both Active Directory Federation Services and Azure Active Directory B2C.</span></span> <span data-ttu-id="b9759-142">Bu durumda, uygulama, JWT taşıyıcı belirtecinden birkaç verenler kabul etmelidir.</span><span class="sxs-lookup"><span data-stu-id="b9759-142">In this case, the app should accept a JWT bearer token from several issuers.</span></span>

<span data-ttu-id="b9759-143">Kabul etmek istediğiniz tüm kimlik doğrulama düzenleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9759-143">Add all authentication schemes you'd like to accept.</span></span> <span data-ttu-id="b9759-144">Aşağıdaki örnek, kod `Startup.ConfigureServices` farklı verenler ile iki JWT taşıyıcı kimlik doğrulama düzenleri ekler:</span><span class="sxs-lookup"><span data-stu-id="b9759-144">For example, the following code in `Startup.ConfigureServices` adds two JWT bearer authentication schemes with different issuers:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.Audience = "https://localhost:5000/";
            options.Authority = "https://localhost:5000/identity/";
        })
        .AddJwtBearer("AzureAD", options =>
        {
            options.Audience = "https://localhost:5000/";
            options.Authority = "https://login.microsoftonline.com/eb971100-6f99-4bdc-8611-1bc8edd7f436/";
        });
}
```

> [!NOTE]
> <span data-ttu-id="b9759-145">Yalnızca bir JWT taşıyıcı kimlik doğrulaması varsayılan kimlik doğrulama düzeni kayıtlı `JwtBearerDefaults.AuthenticationScheme`.</span><span class="sxs-lookup"><span data-stu-id="b9759-145">Only one JWT bearer authentication is registered with the default authentication scheme `JwtBearerDefaults.AuthenticationScheme`.</span></span> <span data-ttu-id="b9759-146">Ek kimlik doğrulama bir benzersiz kimlik doğrulama düzeni ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9759-146">Additional authentication has to be registered with a unique authentication scheme.</span></span>

<span data-ttu-id="b9759-147">Sonraki adım her iki kimlik doğrulama düzenleri kabul etmek için varsayılan yetkilendirme ilkesi güncelleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="b9759-147">The next step is to update the default authorization policy to accept both authentication schemes.</span></span> <span data-ttu-id="b9759-148">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b9759-148">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthorization(options =>
    {
        var defaultAuthorizationPolicyBuilder = new AuthorizationPolicyBuilder(
            JwtBearerDefaults.AuthenticationScheme,
            "AzureAD");
        defaultAuthorizationPolicyBuilder = 
            defaultAuthorizationPolicyBuilder.RequireAuthenticatedUser();
        options.DefaultPolicy = defaultAuthorizationPolicyBuilder.Build();
    });
}
```

<span data-ttu-id="b9759-149">Varsayılan yetkilendirme ilkesi geçersiz kılınan gibi kullanmak mümkün mü `[Authorize]` denetleyicileri özniteliği.</span><span class="sxs-lookup"><span data-stu-id="b9759-149">As the default authorization policy is overridden, it's possible to use the `[Authorize]` attribute in controllers.</span></span> <span data-ttu-id="b9759-150">Denetleyici ardından istekleri ile ilk veya ikinci veren tarafından verilen JWT kabul eder.</span><span class="sxs-lookup"><span data-stu-id="b9759-150">The controller then accepts requests with JWT issued by the first or second issuer.</span></span>

::: moniker-end