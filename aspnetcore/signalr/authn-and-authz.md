---
title: Kimlik doğrulama ve yetkilendirme ASP.NET Core SignalR
author: bradygaster
description: Kimlik doğrulama ve yetkilendirme ASP.NET Core SignalR kullanmayı öğrenin.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 01/31/2019
uid: signalr/authn-and-authz
ms.openlocfilehash: 5d4574775606b4354ec099b6b32e05294d9f0e45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071769"
---
# <a name="authentication-and-authorization-in-aspnet-core-signalr"></a><span data-ttu-id="a7847-103">Kimlik doğrulama ve yetkilendirme ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="a7847-103">Authentication and authorization in ASP.NET Core SignalR</span></span>

<span data-ttu-id="a7847-104">Tarafından [Andrew Stanton-Nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="a7847-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="a7847-105">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(karşıdan yükleme)](xref:index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="a7847-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(how to download)](xref:index#how-to-download-a-sample)</span></span>

## <a name="authenticate-users-connecting-to-a-signalr-hub"></a><span data-ttu-id="a7847-106">Bir SignalR hub'ına bağlanan kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7847-106">Authenticate users connecting to a SignalR hub</span></span>

<span data-ttu-id="a7847-107">SignalR ile kullanılabilir [ASP.NET Core kimlik doğrulaması](xref:security/authentication/identity) kullanıcının her bağlantı ile ilişkilendirilecek.</span><span class="sxs-lookup"><span data-stu-id="a7847-107">SignalR can be used with [ASP.NET Core authentication](xref:security/authentication/identity) to associate a user with each connection.</span></span> <span data-ttu-id="a7847-108">Bir hub, kimlik doğrulama verilerini erişilebilir [ `HubConnectionContext.User` ](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) özelliği.</span><span class="sxs-lookup"><span data-stu-id="a7847-108">In a hub, authentication data can be accessed from the [`HubConnectionContext.User`](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) property.</span></span> <span data-ttu-id="a7847-109">Kimlik doğrulaması, bir kullanıcıyla ilişkili tüm bağlantıları yöntemleri çağırmak hub sağlar (bkz [yönetme SignalR öğesindeki kullanıcılar ve gruplar](xref:signalr/groups) daha fazla bilgi için).</span><span class="sxs-lookup"><span data-stu-id="a7847-109">Authentication allows the hub to call methods on all connections associated with a user (See [Manage users and groups in SignalR](xref:signalr/groups) for more information).</span></span> <span data-ttu-id="a7847-110">Birden çok bağlantı tek bir kullanıcıyla ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7847-110">Multiple connections may be associated with a single user.</span></span>

### <a name="cookie-authentication"></a><span data-ttu-id="a7847-111">Tanımlama bilgisi kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7847-111">Cookie authentication</span></span>

<span data-ttu-id="a7847-112">Tarayıcı tabanlı bir uygulama, SignalR bağlantıları için otomatik olarak akış için mevcut kullanıcı kimlik bilgilerinizi tanımlama bilgisi kimlik doğrulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7847-112">In a browser-based app, cookie authentication allows your existing user credentials to automatically flow to SignalR connections.</span></span> <span data-ttu-id="a7847-113">Tarayıcı istemcisi kullanılırken, hiçbir ek yapılandırma gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a7847-113">When using the browser client, no additional configuration is needed.</span></span> <span data-ttu-id="a7847-114">SignalR bağlantı, otomatik olarak kullanıcı uygulamanızda oturum açtıysa, bu kimlik doğrulaması devralır.</span><span class="sxs-lookup"><span data-stu-id="a7847-114">If the user is logged in to your app, the SignalR connection automatically inherits this authentication.</span></span>

<span data-ttu-id="a7847-115">Tanımlama bilgileri için erişim belirteçleri göndermek için tarayıcı özel yol olsa da, tarayıcı olmayan istemciler, bunları gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7847-115">Cookies are a browser-specific way to send access tokens, but non-browser clients can send them.</span></span> <span data-ttu-id="a7847-116">Kullanırken [.NET istemci](xref:signalr/dotnet-client), `Cookies` özelliği yapılandırılabilir `.WithUrl` çağrısı bir tanımlama bilgisi sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a7847-116">When using the [.NET Client](xref:signalr/dotnet-client), the `Cookies` property can be configured in the `.WithUrl` call in order to provide a cookie.</span></span> <span data-ttu-id="a7847-117">Ancak, .NET istemci tanımlama bilgisi kimlik doğrulamasını kullanarak kimlik doğrulama verilerini bir tanımlama bilgisi gönderip almak için bir API sağlamak için uygulama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a7847-117">However, using cookie authentication from the .NET Client requires the app to provide an API to exchange authentication data for a cookie.</span></span>

### <a name="bearer-token-authentication"></a><span data-ttu-id="a7847-118">Taşıyıcı belirteç kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7847-118">Bearer token authentication</span></span>

<span data-ttu-id="a7847-119">İstemci, bir tanımlama bilgisi kullanmak yerine bir erişim belirteci sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7847-119">The client can provide an access token instead of using a cookie.</span></span> <span data-ttu-id="a7847-120">Sunucu belirteci doğrular ve kullanıcıyı tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7847-120">The server validates the token and uses it to identify the user.</span></span> <span data-ttu-id="a7847-121">Bağlantı kurulduğunda bu doğrulama gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a7847-121">This validation is done only when the connection is established.</span></span> <span data-ttu-id="a7847-122">Bağlantının ömrünü sırasında sunucunun otomatik olarak için belirteç iptali denetlemek için düzeltin değil.</span><span class="sxs-lookup"><span data-stu-id="a7847-122">During the life of the connection, the server doesn't automatically revalidate to check for token revocation.</span></span>

<span data-ttu-id="a7847-123">Sunucuda, taşıyıcı belirteci kimlik doğrulaması kullanılarak yapılandırılan [JWT taşıyıcı ara yazılımı](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer).</span><span class="sxs-lookup"><span data-stu-id="a7847-123">On the server, bearer token authentication is configured using the [JWT Bearer middleware](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer).</span></span>

<span data-ttu-id="a7847-124">JavaScript istemci kullanarak belirteci sağlanabilir [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a7847-124">In the JavaScript client, the token can be provided using the [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) option.</span></span>

[!code-typescript[Configure Access Token](authn-and-authz/sample/wwwroot/js/chat.ts?range=63-65)]

<span data-ttu-id="a7847-125">.NET istemci yoktur benzer [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) belirteç yapılandırmak için kullanılan özelliği:</span><span class="sxs-lookup"><span data-stu-id="a7847-125">In the .NET client, there is a similar [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) property that can be used to configure the token:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    { 
        options.AccessTokenProvider = () => Task.FromResult(_myAccessToken);
    })
    .Build();
```

> [!NOTE]
> <span data-ttu-id="a7847-126">Sağladığınız bir erişim belirteci işlev önce çağrılır **her** SignalR tarafından yapılan HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="a7847-126">The access token function you provide is called before **every** HTTP request made by SignalR.</span></span> <span data-ttu-id="a7847-127">(Bağlantı sırasında dolabilir nedeniyle) bağlantının etkin kalması için belirteci yenilemek ihtiyacınız varsa, bu işlev gelen bunu ve güncelleştirilmiş bir belirteci döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7847-127">If you need to renew the token in order to keep the connection active (because it may expire during the connection), do so from within this function and return the updated token.</span></span>

<span data-ttu-id="a7847-128">Standart web API'leri bir HTTP üst bilgisinde taşıyıcı belirteçleri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="a7847-128">In standard web APIs, bearer tokens are sent in an HTTP header.</span></span> <span data-ttu-id="a7847-129">Ancak, SignalR bazı taşımalar kullanırken tarayıcılarda bu üstbilgileri ayarlanacak silemiyor.</span><span class="sxs-lookup"><span data-stu-id="a7847-129">However, SignalR is unable to set these headers in browsers when using some transports.</span></span> <span data-ttu-id="a7847-130">WebSockets ve Server-Sent olaylarını kullanarak belirteci bir sorgu dizesi parametresi iletilir.</span><span class="sxs-lookup"><span data-stu-id="a7847-130">When using WebSockets and Server-Sent Events, the token is transmitted as a query string parameter.</span></span> <span data-ttu-id="a7847-131">Bu sunucuda desteklemek için ek yapılandırma gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="a7847-131">In order to support this on the server, additional configuration is required:</span></span>

[!code-csharp[Configure Server to accept access token from Query String](authn-and-authz/sample/Startup.cs?name=snippet)]

### <a name="cookies-vs-bearer-tokens"></a><span data-ttu-id="a7847-132">Taşıyıcı belirteçleri ve tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="a7847-132">Cookies vs. bearer tokens</span></span> 

<span data-ttu-id="a7847-133">Tanımlama bilgilerini tarayıcılar belirli olduğundan, diğer istemciler türlerindeki göndererek taşıyıcı belirteçleri göndermeyi karşılaştırıldığında karmaşıklığı ekler.</span><span class="sxs-lookup"><span data-stu-id="a7847-133">Because cookies are specific to browsers, sending them from other kinds of clients adds complexity compared to sending bearer tokens.</span></span> <span data-ttu-id="a7847-134">Tarayıcı istemcisi kullanıcıların kimliğini doğrulamak uygulamayı yalnızca gerekmedikçe, bu nedenle, tanımlama bilgisi kimlik doğrulamasını önerilmez.</span><span class="sxs-lookup"><span data-stu-id="a7847-134">For this reason, cookie authentication isn't recommended unless the app only needs to authenticate users from the browser client.</span></span> <span data-ttu-id="a7847-135">Taşıyıcı belirteci kimlik doğrulaması için önerilen tarayıcı istemci dışındaki istemcilerin kullanırken yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="a7847-135">Bearer token authentication is the recommended approach when using clients other than the browser client.</span></span>

### <a name="windows-authentication"></a><span data-ttu-id="a7847-136">Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7847-136">Windows authentication</span></span>

<span data-ttu-id="a7847-137">Varsa [Windows kimlik doğrulaması](xref:security/authentication/windowsauth) yapılandırılmış uygulamanızda, hub'ı güvenli hale getirmek için bu kimlik SignalR kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7847-137">If [Windows authentication](xref:security/authentication/windowsauth) is configured in your app, SignalR can use that identity to secure hubs.</span></span> <span data-ttu-id="a7847-138">Ancak, bireysel kullanıcılar için ileti göndermek için özel bir kullanıcı kimliği Sağlayıcı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7847-138">However, in order to send messages to individual users, you need to add a custom User ID provider.</span></span> <span data-ttu-id="a7847-139">Windows kimlik doğrulama sistemi kullanıcı adını belirlemek için SignalR kullanır "Ad tanımlayıcı" talep sağlamaz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a7847-139">This is because the Windows authentication system doesn't provide the "Name Identifier" claim that SignalR uses to determine the user name.</span></span>

<span data-ttu-id="a7847-140">Uygulayan bir yeni sınıf ekleyin `IUserIdProvider` ve taleplerinden biri tanımlayıcı olarak kullanılacak kullanıcı almak.</span><span class="sxs-lookup"><span data-stu-id="a7847-140">Add a new class that implements `IUserIdProvider` and retrieve one of the claims from the user to use as the identifier.</span></span> <span data-ttu-id="a7847-141">Örneğin, "Name" talep kullanmak için (Windows kullanıcı adı biçiminde olduğu `[Domain]\[Username]`), aşağıdaki sınıfı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a7847-141">For example, to use the "Name" claim (which is the Windows username in the form `[Domain]\[Username]`), create the following class:</span></span>

[!code-csharp[Name based provider](authn-and-authz/sample/nameuseridprovider.cs?name=NameUserIdProvider)]

<span data-ttu-id="a7847-142">Yerine `ClaimTypes.Name`, herhangi bir değer kullanabilirsiniz `User` (Windows SID tanımlayıcı gibi vb.).</span><span class="sxs-lookup"><span data-stu-id="a7847-142">Rather than `ClaimTypes.Name`, you can use any value from the `User` (such as the Windows SID identifier, etc.).</span></span>

> [!NOTE]
> <span data-ttu-id="a7847-143">Seçtiğiniz değer sisteminizdeki tüm kullanıcılar arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7847-143">The value you choose must be unique among all the users in your system.</span></span> <span data-ttu-id="a7847-144">Aksi takdirde, bir kullanıcıya yönelik bir ileti için farklı bir kullanıcı daha son.</span><span class="sxs-lookup"><span data-stu-id="a7847-144">Otherwise, a message intended for one user could end up going to a different user.</span></span>

<span data-ttu-id="a7847-145">Bu bileşen, kaydetme, `Startup.ConfigureServices` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a7847-145">Register this component in your `Startup.ConfigureServices` method.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // ... other services ...

    services.AddSignalR();
    services.AddSingleton<IUserIdProvider, NameUserIdProvider>();
}
```

<span data-ttu-id="a7847-146">.NET istemci ayarlayarak Windows kimlik doğrulaması etkinleştirilmelidir [UseDefaultCredentials](/dotnet/api/microsoft.aspnetcore.http.connections.client.httpconnectionoptions.usedefaultcredentials) özelliği:</span><span class="sxs-lookup"><span data-stu-id="a7847-146">In the .NET Client, Windows Authentication must be enabled by setting the [UseDefaultCredentials](/dotnet/api/microsoft.aspnetcore.http.connections.client.httpconnectionoptions.usedefaultcredentials) property:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    {
        options.UseDefaultCredentials = true;
    })
    .Build();
```

<span data-ttu-id="a7847-147">Windows kimlik doğrulaması, yalnızca Microsoft Internet Explorer veya Microsoft Edge kullanırken tarayıcı istemci tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a7847-147">Windows Authentication is only supported by the browser client when using Microsoft Internet Explorer or Microsoft Edge.</span></span>

### <a name="use-claims-to-customize-identity-handling"></a><span data-ttu-id="a7847-148">Kimlik işleme özelleştirmek için talep kullanın</span><span class="sxs-lookup"><span data-stu-id="a7847-148">Use claims to customize identity handling</span></span>

<span data-ttu-id="a7847-149">Bir uygulama kullanıcılarının kimliğini doğrulayan SignalR kullanıcı kimlikleri gelen kullanıcı talepleri türetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7847-149">An app that authenticates users can derive SignalR user IDs from user claims.</span></span> <span data-ttu-id="a7847-150">SignalR, kullanıcı kimliklerini nasıl oluşturur? belirtmek için uygulama `IUserIdProvider` ve uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a7847-150">To specify how SignalR creates user IDs, implement `IUserIdProvider` and register the implementation.</span></span>

<span data-ttu-id="a7847-151">Örnek kod, kullanıcının e-posta adresi tanımlayıcı bir özelliği seçmek için talep nasıl kullanacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a7847-151">The sample code demonstrates how you would use claims to select the user's email address as the identifying property.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7847-152">Seçtiğiniz değer sisteminizdeki tüm kullanıcılar arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7847-152">The value you choose must be unique among all the users in your system.</span></span> <span data-ttu-id="a7847-153">Aksi takdirde, bir kullanıcıya yönelik bir ileti için farklı bir kullanıcı daha son.</span><span class="sxs-lookup"><span data-stu-id="a7847-153">Otherwise, a message intended for one user could end up going to a different user.</span></span>

[!code-csharp[Email provider](authn-and-authz/sample/EmailBasedUserIdProvider.cs?name=EmailBasedUserIdProvider)]

<span data-ttu-id="a7847-154">Hesap kaydı türüyle bir talep ekler `ClaimsTypes.Email` ASP.NET kimlik veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a7847-154">The account registration adds a claim with type `ClaimsTypes.Email` to the ASP.NET identity database.</span></span>

[!code-csharp[Adding the email to the ASP.NET identity claims](authn-and-authz/sample/pages/account/Register.cshtml.cs?name=AddEmailClaim)]

<span data-ttu-id="a7847-155">Bu bileşen, kaydetme, `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="a7847-155">Register this component in your `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSingleton<IUserIdProvider, EmailBasedUserIdProvider>();
```

## <a name="authorize-users-to-access-hubs-and-hub-methods"></a><span data-ttu-id="a7847-156">Erişim hub'lar ve hub yöntemleri için kullanıcıları yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a7847-156">Authorize users to access hubs and hub methods</span></span>

<span data-ttu-id="a7847-157">Varsayılan olarak, bir hub'ındaki tüm yöntemler, kimliği doğrulanmamış bir kullanıcı tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7847-157">By default, all methods in a hub can be called by an unauthenticated user.</span></span> <span data-ttu-id="a7847-158">Kimlik doğrulaması gerektiren için uygulamanız [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) özniteliği hub'ına:</span><span class="sxs-lookup"><span data-stu-id="a7847-158">In order to require authentication, apply the [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) attribute to the hub:</span></span>

[!code-csharp[Restrict a hub to only authorized users](authn-and-authz/sample/Hubs/ChatHub.cs?range=8-10,32)]

<span data-ttu-id="a7847-159">Oluşturucu bağımsız değişkenleri ve özellikleri kullanabileceğinizi `[Authorize]` belirli eşleşen yalnızca kullanıcılar için erişimi kısıtlamak için özniteliği [Yetkilendirme İlkeleri](xref:security/authorization/policies).</span><span class="sxs-lookup"><span data-stu-id="a7847-159">You can use the constructor arguments and properties of the `[Authorize]` attribute to restrict access to only users matching specific [authorization policies](xref:security/authorization/policies).</span></span> <span data-ttu-id="a7847-160">Örneğin, adında özel yetkilendirme ilkesi varsa `MyAuthorizationPolicy` yalnızca bu ilkeyle eşleşen kullanıcılar hub'ı aşağıdaki kodu kullanarak erişebildiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="a7847-160">For example, if you have a custom authorization policy called `MyAuthorizationPolicy` you can ensure that only users matching that policy can access the hub using the following code:</span></span>

```csharp
[Authorize("MyAuthorizationPolicy")]
public class ChatHub: Hub
{
}
```

<span data-ttu-id="a7847-161">Tek hub yöntemleri olabilir `[Authorize]` özniteliği de uygulandı.</span><span class="sxs-lookup"><span data-stu-id="a7847-161">Individual hub methods can have the `[Authorize]` attribute applied as well.</span></span> <span data-ttu-id="a7847-162">Geçerli kullanıcının yönteme uygulanmış olan ilkenin eşleşmiyorsa, bir hata çağırana döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a7847-162">If the current user doesn't match the policy applied to the method, an error is returned to the caller:</span></span>

```csharp
[Authorize]
public class ChatHub: Hub
{
    public async Task Send(string message)
    {
        // ... send a message to all users ...
    }

    [Authorize("Administrators")]
    public void BanUser(string userName)
    {
        // ... ban a user from the chat room (something only Administrators can do) ...
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="a7847-163">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a7847-163">Additional resources</span></span>

* [<span data-ttu-id="a7847-164">ASP.NET core'da taşıyıcı belirteci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7847-164">Bearer Token Authentication in ASP.NET Core</span></span>](https://blogs.msdn.microsoft.com/webdev/2016/10/27/bearer-token-authentication-in-asp-net-core/)
