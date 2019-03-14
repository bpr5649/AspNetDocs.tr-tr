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
# <a name="authentication-and-authorization-in-aspnet-core-signalr"></a>Kimlik doğrulama ve yetkilendirme ASP.NET Core SignalR

Tarafından [Andrew Stanton-Nurse](https://twitter.com/anurse)

[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(karşıdan yükleme)](xref:index#how-to-download-a-sample)

## <a name="authenticate-users-connecting-to-a-signalr-hub"></a>Bir SignalR hub'ına bağlanan kullanıcıların kimlik doğrulaması

SignalR ile kullanılabilir [ASP.NET Core kimlik doğrulaması](xref:security/authentication/identity) kullanıcının her bağlantı ile ilişkilendirilecek. Bir hub, kimlik doğrulama verilerini erişilebilir [ `HubConnectionContext.User` ](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) özelliği. Kimlik doğrulaması, bir kullanıcıyla ilişkili tüm bağlantıları yöntemleri çağırmak hub sağlar (bkz [yönetme SignalR öğesindeki kullanıcılar ve gruplar](xref:signalr/groups) daha fazla bilgi için). Birden çok bağlantı tek bir kullanıcıyla ilişkili olabilir.

### <a name="cookie-authentication"></a>Tanımlama bilgisi kimlik doğrulaması

Tarayıcı tabanlı bir uygulama, SignalR bağlantıları için otomatik olarak akış için mevcut kullanıcı kimlik bilgilerinizi tanımlama bilgisi kimlik doğrulamasını sağlar. Tarayıcı istemcisi kullanılırken, hiçbir ek yapılandırma gerekmez. SignalR bağlantı, otomatik olarak kullanıcı uygulamanızda oturum açtıysa, bu kimlik doğrulaması devralır.

Tanımlama bilgileri için erişim belirteçleri göndermek için tarayıcı özel yol olsa da, tarayıcı olmayan istemciler, bunları gönderebilirsiniz. Kullanırken [.NET istemci](xref:signalr/dotnet-client), `Cookies` özelliği yapılandırılabilir `.WithUrl` çağrısı bir tanımlama bilgisi sağlamak için. Ancak, .NET istemci tanımlama bilgisi kimlik doğrulamasını kullanarak kimlik doğrulama verilerini bir tanımlama bilgisi gönderip almak için bir API sağlamak için uygulama gerektirir.

### <a name="bearer-token-authentication"></a>Taşıyıcı belirteç kimlik doğrulaması

İstemci, bir tanımlama bilgisi kullanmak yerine bir erişim belirteci sağlayabilirsiniz. Sunucu belirteci doğrular ve kullanıcıyı tanımlamak için kullanır. Bağlantı kurulduğunda bu doğrulama gerçekleştirilir. Bağlantının ömrünü sırasında sunucunun otomatik olarak için belirteç iptali denetlemek için düzeltin değil.

Sunucuda, taşıyıcı belirteci kimlik doğrulaması kullanılarak yapılandırılan [JWT taşıyıcı ara yazılımı](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer).

JavaScript istemci kullanarak belirteci sağlanabilir [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) seçeneği.

[!code-typescript[Configure Access Token](authn-and-authz/sample/wwwroot/js/chat.ts?range=63-65)]

.NET istemci yoktur benzer [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) belirteç yapılandırmak için kullanılan özelliği:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    { 
        options.AccessTokenProvider = () => Task.FromResult(_myAccessToken);
    })
    .Build();
```

> [!NOTE]
> Sağladığınız bir erişim belirteci işlev önce çağrılır **her** SignalR tarafından yapılan HTTP isteği. (Bağlantı sırasında dolabilir nedeniyle) bağlantının etkin kalması için belirteci yenilemek ihtiyacınız varsa, bu işlev gelen bunu ve güncelleştirilmiş bir belirteci döndürür.

Standart web API'leri bir HTTP üst bilgisinde taşıyıcı belirteçleri gönderilir. Ancak, SignalR bazı taşımalar kullanırken tarayıcılarda bu üstbilgileri ayarlanacak silemiyor. WebSockets ve Server-Sent olaylarını kullanarak belirteci bir sorgu dizesi parametresi iletilir. Bu sunucuda desteklemek için ek yapılandırma gerekli değildir:

[!code-csharp[Configure Server to accept access token from Query String](authn-and-authz/sample/Startup.cs?name=snippet)]

### <a name="cookies-vs-bearer-tokens"></a>Taşıyıcı belirteçleri ve tanımlama bilgileri 

Tanımlama bilgilerini tarayıcılar belirli olduğundan, diğer istemciler türlerindeki göndererek taşıyıcı belirteçleri göndermeyi karşılaştırıldığında karmaşıklığı ekler. Tarayıcı istemcisi kullanıcıların kimliğini doğrulamak uygulamayı yalnızca gerekmedikçe, bu nedenle, tanımlama bilgisi kimlik doğrulamasını önerilmez. Taşıyıcı belirteci kimlik doğrulaması için önerilen tarayıcı istemci dışındaki istemcilerin kullanırken yaklaşımdır.

### <a name="windows-authentication"></a>Windows kimlik doğrulaması

Varsa [Windows kimlik doğrulaması](xref:security/authentication/windowsauth) yapılandırılmış uygulamanızda, hub'ı güvenli hale getirmek için bu kimlik SignalR kullanabilirsiniz. Ancak, bireysel kullanıcılar için ileti göndermek için özel bir kullanıcı kimliği Sağlayıcı eklemeniz gerekir. Windows kimlik doğrulama sistemi kullanıcı adını belirlemek için SignalR kullanır "Ad tanımlayıcı" talep sağlamaz olmasıdır.

Uygulayan bir yeni sınıf ekleyin `IUserIdProvider` ve taleplerinden biri tanımlayıcı olarak kullanılacak kullanıcı almak. Örneğin, "Name" talep kullanmak için (Windows kullanıcı adı biçiminde olduğu `[Domain]\[Username]`), aşağıdaki sınıfı oluşturun:

[!code-csharp[Name based provider](authn-and-authz/sample/nameuseridprovider.cs?name=NameUserIdProvider)]

Yerine `ClaimTypes.Name`, herhangi bir değer kullanabilirsiniz `User` (Windows SID tanımlayıcı gibi vb.).

> [!NOTE]
> Seçtiğiniz değer sisteminizdeki tüm kullanıcılar arasında benzersiz olması gerekir. Aksi takdirde, bir kullanıcıya yönelik bir ileti için farklı bir kullanıcı daha son.

Bu bileşen, kaydetme, `Startup.ConfigureServices` yöntemi.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // ... other services ...

    services.AddSignalR();
    services.AddSingleton<IUserIdProvider, NameUserIdProvider>();
}
```

.NET istemci ayarlayarak Windows kimlik doğrulaması etkinleştirilmelidir [UseDefaultCredentials](/dotnet/api/microsoft.aspnetcore.http.connections.client.httpconnectionoptions.usedefaultcredentials) özelliği:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    {
        options.UseDefaultCredentials = true;
    })
    .Build();
```

Windows kimlik doğrulaması, yalnızca Microsoft Internet Explorer veya Microsoft Edge kullanırken tarayıcı istemci tarafından desteklenir.

### <a name="use-claims-to-customize-identity-handling"></a>Kimlik işleme özelleştirmek için talep kullanın

Bir uygulama kullanıcılarının kimliğini doğrulayan SignalR kullanıcı kimlikleri gelen kullanıcı talepleri türetebilirsiniz. SignalR, kullanıcı kimliklerini nasıl oluşturur? belirtmek için uygulama `IUserIdProvider` ve uygulama kaydedin.

Örnek kod, kullanıcının e-posta adresi tanımlayıcı bir özelliği seçmek için talep nasıl kullanacağınız gösterilmektedir. 

> [!NOTE]
> Seçtiğiniz değer sisteminizdeki tüm kullanıcılar arasında benzersiz olması gerekir. Aksi takdirde, bir kullanıcıya yönelik bir ileti için farklı bir kullanıcı daha son.

[!code-csharp[Email provider](authn-and-authz/sample/EmailBasedUserIdProvider.cs?name=EmailBasedUserIdProvider)]

Hesap kaydı türüyle bir talep ekler `ClaimsTypes.Email` ASP.NET kimlik veritabanı.

[!code-csharp[Adding the email to the ASP.NET identity claims](authn-and-authz/sample/pages/account/Register.cshtml.cs?name=AddEmailClaim)]

Bu bileşen, kaydetme, `Startup.ConfigureServices`.

```csharp
services.AddSingleton<IUserIdProvider, EmailBasedUserIdProvider>();
```

## <a name="authorize-users-to-access-hubs-and-hub-methods"></a>Erişim hub'lar ve hub yöntemleri için kullanıcıları yetkilendirme

Varsayılan olarak, bir hub'ındaki tüm yöntemler, kimliği doğrulanmamış bir kullanıcı tarafından çağrılabilir. Kimlik doğrulaması gerektiren için uygulamanız [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) özniteliği hub'ına:

[!code-csharp[Restrict a hub to only authorized users](authn-and-authz/sample/Hubs/ChatHub.cs?range=8-10,32)]

Oluşturucu bağımsız değişkenleri ve özellikleri kullanabileceğinizi `[Authorize]` belirli eşleşen yalnızca kullanıcılar için erişimi kısıtlamak için özniteliği [Yetkilendirme İlkeleri](xref:security/authorization/policies). Örneğin, adında özel yetkilendirme ilkesi varsa `MyAuthorizationPolicy` yalnızca bu ilkeyle eşleşen kullanıcılar hub'ı aşağıdaki kodu kullanarak erişebildiğinizden emin olun:

```csharp
[Authorize("MyAuthorizationPolicy")]
public class ChatHub: Hub
{
}
```

Tek hub yöntemleri olabilir `[Authorize]` özniteliği de uygulandı. Geçerli kullanıcının yönteme uygulanmış olan ilkenin eşleşmiyorsa, bir hata çağırana döndürülür:

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

## <a name="additional-resources"></a>Ek kaynaklar

* [ASP.NET core'da taşıyıcı belirteci kimlik doğrulaması](https://blogs.msdn.microsoft.com/webdev/2016/10/27/bearer-token-authentication-in-asp-net-core/)
