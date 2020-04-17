---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 Yetkilendirme Sunucusu | Microsoft Dokümanlar
author: hongyes
description: Bu öğretici, OWIN OAuth aracını kullanarak Bir OAuth 2.0 Yetkilendirme Sunucusu'nu nasıl uygulayacağınız konusunda size rehberlik edecektir. Bu gelişmiş bir öğretici olduğunu sadece outlin ...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540434"
---
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 Yetkilendirme Sunucusu
====================
Tarafından [Hongye Sun](https://github.com/hongyes) ve [Praburaj Thiagarajan](https://github.com/Praburaj)

> Bu öğretici, OWIN OAuth aracını kullanarak Bir OAuth 2.0 Yetkilendirme Sunucusu'nu nasıl uygulayacağınız konusunda size rehberlik edecektir. Bu, yalnızca Bir OWIN OAuth 2.0 Yetkilendirme Sunucusu oluşturmak için adımları özetleyen gelişmiş bir öğreticidir. Bu adım öğretici bir adım değildir. [Örnek kodu indirin.](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)
>
> > [!NOTE]
> > Bu anahat, güvenli bir üretim uygulaması oluşturmak için kullanılmak üzere tasarlanmamalıdır. Bu öğretici, OWIN OAuth aracını kullanarak bir OAuth 2.0 Yetkilendirme Sunucusunun nasıl uygulanacağı hakkında yalnızca bir anahat sağlamak için tasarlanmıştır.
>
>
> ## <a name="software-versions"></a>Yazılım sürümleri
>
> | **Öğreticide gösterilen** | **Ayrıca ile çalışır** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Görsel Stüdyo 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [Visual Studio 2013 Masaüstü için Express](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 ile en son güncelleme çalışması gerekir, ancak öğretici ile test edilmemiştir ve bazı menü seçimleri ve iletişim kutuları farklıdır. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>Sorular ve Yorumlar
>
> Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [GitHub'daki Katana Projesi'nde](https://github.com/aspnet/AspNetKatana/)yayınlayabilirsiniz. Öğreticinin kendisi yle ilgili soru ve yorumlar için sayfanın altındaki yorumlar bölümüne bakın.


[OAuth 2.0 çerçevesi,](http://tools.ietf.org/html/rfc6749) bir üçüncü taraf uygulamasının bir HTTP hizmetine sınırlı erişim elde etmesini sağlar. İstemci, korumalı bir kaynağa erişmek için kaynak sahibinin kimlik bilgilerini kullanmak yerine, bir erişim belirteci (belirli bir kapsam, yaşam süresi ve diğer erişim özniteliklerini gösteren bir dize) alır. Erişim belirteçleri, kaynak sahibinin onayı ile bir yetkilendirme sunucusu tarafından üçüncü taraf istemcilere verilir.

Bu öğretici kapsayacak:

- Dört yetkilendirme hibe türünü desteklemek ve belirteçleri yenilemek için bir yetkilendirme sunucusu oluşturma:
    - Yetkilendirme kodu hibesi
    - Örtülü Hibe
    - Kaynak Sahibi Şifre Kimlik Bilgileri Hibesi
    - Müşteri Kimlik Bilgileri Hibesi
- Erişim belirteci tarafından korunan bir kaynak sunucusu oluşturma.
- OAuth 2.0 istemcileri oluşturma.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Ön koşullar

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) veya ücretsiz [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), sayfanın üst kısmında **Yazılım Sürümleri** belirtildiği gibi.
- OWIN ile aşinalık. Katana Projesi ve OWIN ve [Katana yeniliklerle](index.md) [başlarken](https://msdn.microsoft.com/magazine/dn451439.aspx) bakın.
- [Roller,](http://tools.ietf.org/html/rfc6749#section-1.1) [Protokol Akışı](http://tools.ietf.org/html/rfc6749#section-1.2)ve [Yetki Lendirme Desteği](http://tools.ietf.org/html/rfc6749#section-1.3)de dahil olmak üzere [OAuth](http://tools.ietf.org/html/rfc6749) terminolojisi ile aşinalık. [OAuth 2.0 giriş](http://tools.ietf.org/html/rfc6749#section-1) iyi bir giriş sağlar.

## <a name="create-an-authorization-server"></a>Yetkilendirme Sunucusu Oluşturma

Bu öğreticide, bir yetkilendirme sunucusu oluşturmak için [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) ve ASP.NET MVC'nin nasıl kullanılacağını kabaca çizeceğiz. Bu öğretici her adımı içermemektedir gibi, yakında tamamlanan örnek için bir indirme sağlamak umuyoruz. İlk olarak, *AuthorizationServer* adında boş bir web uygulaması oluşturun ve aşağıdaki paketleri yükleyin:

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- Microsoft.Owin.Security.Google (Veya Microsoft.Owin.Security.Facebook gibi diğer sosyal giriş paketi)

*Başlangıç*adlı proje kök klasörü altında bir [OWIN Başlangıç sınıfı](owin-startup-class-detection.md) ekleyin.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

Bir *App\_Start* klasörü oluşturun. *App\_Start* klasörünü seçin ve *YetkilendirmeServer\App\_Start\Startup.Auth.cs* dosyasının indirilen sürümünü eklemek için Shift+Alt+A'yı kullanın.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

Yukarıdaki kod, hesapları yönetmek için yetkilendirme sunucusunun kendisi tarafından kullanılan uygulama/dış oturum açma tanımlama bilgileri ve Google kimlik doğrulaması sağlar.

Uzantı `UseOAuthAuthorizationServer` yöntemi yetkilendirme sunucusunu kurmaktır. Kurulum seçenekleri şunlardır:

- `AuthorizeEndpointPath`: İstemci uygulamalarının kullanıcı aracısını yeniden yönlendireceği istek yolu, kullanıcıların bir belirteç veya kod verme izni almasını sağlar. Örneğin,`/Authorize`önde gelen bir kesikle başlamalı.
- `TokenEndpointPath`: İstek yolu istemci uygulamaları doğrudan erişim belirteci elde etmek için iletişim. "/Token" gibi önde gelen bir kesikle başlamalıdır. İstemciye bir [\_istemci sırrı](http://tools.ietf.org/html/rfc6749#appendix-A.2)verilirse, bu uç noktaya sağlanmalıdır.
- `ApplicationCanDisplayErrors`: Web `true` `/Authorize` uygulaması, uç noktadaistemci doğrulama hataları için özel bir hata sayfası oluşturmak isterse ayarlayın. Bu yalnızca tarayıcının istemci uygulamasına geri yönlendirilen olmadığı durumlar için gereklidir, örneğin, tarayıcı yanlış olduğunda `client_id` veya `redirect_uri` yanlışolduğunda. Bitiş `/Authorize` noktası "oauth görmek için bekleyebilirsiniz. Hata", "oauth. Hata Açıklaması", ve "oauth. ErrorUri" özellikleri OWIN ortamına eklenir.

    > [!NOTE]
    > Doğru değilse, yetkilendirme sunucusu hata ayrıntılarıyla birlikte varsayılan bir hata sayfası döndürecektir.
- `AllowInsecureHttp`: Yetki lendirme ve belirteç isteklerinin HTTP URI adreslerine ulaşmasına izin vermek ve gelen `redirect_uri` yetkilendirme isteği parametrelerinin HTTP URI adreslerine sahip olmasını sağlamak için geçerlidir.

    > [!WARNING]
    > Güvenlik - Bu sadece geliştirme içindir.
- `Provider`: Yetkilendirme Sunucusu ara ware tarafından yükseltilen olayları işlemek için uygulama tarafından sağlanan nesne. Uygulama arabirimi tam olarak uygulayabilir veya bu `OAuthAuthorizationServerProvider` sunucunun desteklediği OAuth akışları için gerekli olan temsilcilerin bir örneğini oluşturabilir ve atayabilir.
- `AuthorizationCodeProvider`: İstemci uygulamasına dönmek için tek kullanımlık bir yetkilendirme kodu üretir. OAuth sunucusunun güvenli olması için `AuthorizationCodeProvider` uygulama, `OnCreate/OnCreateAsync` olay tarafından üretilen belirteç için yalnızca bir `OnReceive/OnReceiveAsync`çağrı için geçerli kabul edildiği bir örnek **sağlamalı.**
- `RefreshTokenProvider`: Gerektiğinde yeni bir erişim belirteci üretmek için kullanılabilecek bir yenileme belirteci üretir. Yetkilendirme sunucusu `/Token` sağlanmadıysa, bitiş noktasından yenileme belirteçlerini döndürmez.

## <a name="account-management"></a>Hesap Yönetimi

OAuth, kullanıcı hesabı bilgilerinizi nerede veya nasıl yönettiğinizi umursamaz. Bundan sorumlu olan [ASP.NET kimliktir.](../../../identity/index.md) Bu eğitimde, hesap yönetim kodunu basitleştirecek ve kullanıcının OWIN çerez aracını kullanarak oturum açabilmesini sağlayacağız. Burada basitleştirilmiş örnek `AccountController`kodu:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`kayıtlı yönlendirme URL'si ile istemciyi doğrulamak için kullanılır. `ValidateClientAuthentication`istemcinin kimlik bilgilerini almak için temel şema üstbilgisini ve form gövdesini denetler.

Giriş sayfası aşağıda gösterilmiştir:

![](owin-oauth-20-authorization-server/_static/image1.png)

Şimdi IETF's OAuth 2 [Yetki Kodu Hibe](http://tools.ietf.org/html/rfc6749#section-4.1) bölümünü inceleyin.

**Sağlayıcı** (aşağıdaki tabloda) [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)olduğunu. Sağlayıcı, tüm OAuth sunucu olayları içeren türü, `OAuthAuthorizationServerProvider`dir.

| Yetkilendirme Kodu Hibe bölümünden akış adımları | Örnek indirme şu adımları gerçekleştirir: |
| --- | --- |
|  |  |
| (A) İstemci, kaynak sahibinin kullanıcı aracısını yetkilendirme bitiş noktasına yönlendirerek akışı başlatır. İstemci, istemci tanımlayıcısını, istenen kapsamı, yerel durumu ve yetkilendirme sunucusunun erişim verildikten (veya reddedildikten) sonra kullanıcı aracısını geri göndereceği bir yeniden yönlendirme URI'sini içerir. | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Yetkilendirme sunucusu kaynak sahibinin kimliğini doğrular (kullanıcı aracısı aracılığıyla) ve kaynak sahibinin istemcinin erişim isteğini hibe edip etmediğini veya reddedip etmediğini belirler. | **Kullanıcı erişim izni veriyorsa&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Kaynak sahibinin erişim sağladığını varsayarsak, yetkilendirme sunucusu kullanıcı aracısını daha önce sağlanan yeniden yönlendirme URI'yi kullanarak istemciye geri yönlendirir (istekte veya istemci kaydı sırasında). ... |  |
|  |  |
| (D) İstemci, önceki adımda alınan yetkilendirme kodunu ekleyerek yetkilendirme sunucusunun belirteç bitiş noktasından bir erişim belirteci ister. İstek tevekkül ederken, istemci yetkilendirme sunucusuyla kimlik doğrulaması sağlar. İstemci, doğrulama için yetkilendirme kodunu elde etmek için kullanılan yeniden yönlendirme URI'yi içerir. | Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

Yetkilendirme kodunun `AuthorizationCodeProvider.CreateAsync` `ReceiveAsync` oluşturulması ve doğrulanması için ve denetlemek için örnek bir uygulama aşağıda gösterilmiştir.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

Yukarıdaki kod, kodu ve kimlik biletini depolamak ve kodu aldıktan sonra kimliği geri yüklemek için bellek içi eşzamanlı bir sözlük kullanır. Gerçek bir uygulamada, kalıcı bir veri deposu tarafından değiştirilir. Yetkilendirme bitiş noktası, kaynak sahibinin istemciye erişim izni vermesi içindir. Genellikle, kullanıcının bir düğmeyi tıklatması ve hibeyi onaylaması için bir kullanıcı arabirimine ihtiyacı vardır. OWIN OAuth middleware uygulama kodu yetkilendirme bitiş noktası işlemek için izin verir. Örnek uygulamamızda, onu işlemek için `OAuthController` çağrılan bir MVC denetleyicisi kullanırız. İşte örnek uygulama:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

Eylem `Authorize` ilk olarak kullanıcının yetkilendirme sunucusunda oturum açmış olup olmadığını denetler. Değilse, kimlik doğrulama aracı arayanın "Uygulama" çerezini kullanarak kimliğini doğrulaması için zorlar ve giriş sayfasına yönlendirir. (Bkz. yukarıda vurgulanan kod.) Kullanıcı oturum açmışsa, aşağıda gösterildiği gibi Yetkilendirme görünümünü işleyecektir:

![](owin-oauth-20-authorization-server/_static/image2.png)

**Hibe** düğmesi seçilirse, `Authorize` eylem yeni bir "Taşıyıcı" kimliği oluşturur ve onunla oturum açtır. Bir taşıyıcı belirteci oluşturmak ve JSON yükü ile istemciye geri göndermek için yetkilendirme sunucusu tetikler.

### <a name="implicit-grant"></a>Örtülü Hibe

Şimdi IETF's OAuth 2 [Örtülü Hibe](http://tools.ietf.org/html/rfc6749#section-4.2) bölümüne bakın.

 Şekil 4'te gösterilen [Örtük Hibe](http://tools.ietf.org/html/rfc6749#section-4.2) akışı, OWIN OAuth aracının izlediği akış ve haritalamadır.

| Örtülü Hibe bölümünden akış adımları | Örnek indirme şu adımları gerçekleştirir: |
| --- | --- |
|  |  |
| (A) İstemci, kaynak sahibinin kullanıcı aracısını yetkilendirme bitiş noktasına yönlendirerek akışı başlatır. İstemci, istemci tanımlayıcısını, istenen kapsamı, yerel durumu ve yetkilendirme sunucusunun erişim verildikten (veya reddedildikten) sonra kullanıcı aracısını geri göndereceği bir yeniden yönlendirme URI'sini içerir. | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Yetkilendirme sunucusu kaynak sahibinin kimliğini doğrular (kullanıcı aracısı aracılığıyla) ve kaynak sahibinin istemcinin erişim isteğini hibe edip etmediğini veya reddedip etmediğini belirler. | **Kullanıcı erişim izni veriyorsa&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Kaynak sahibinin erişim sağladığını varsayarsak, yetkilendirme sunucusu kullanıcı aracısını daha önce sağlanan yeniden yönlendirme URI'yi kullanarak istemciye geri yönlendirir (istekte veya istemci kaydı sırasında). ... |  |
|  |  |
| (D) İstemci, önceki adımda alınan yetkilendirme kodunu ekleyerek yetkilendirme sunucusunun belirteç bitiş noktasından bir erişim belirteci ister. İstek tevekkül ederken, istemci yetkilendirme sunucusuyla kimlik doğrulaması sağlar. İstemci, doğrulama için yetkilendirme kodunu elde etmek için kullanılan yeniden yönlendirme URI'yi içerir. |  |

Yetkilendirme kodu hibesi için`OAuthController.Authorize` yetkilendirme bitiş noktasını (eylem) zaten uyguladığımız için, otomatik olarak örtülü akışı da sağlar. Not: `Provider.ValidateClientRedirectUri` dolaylı hibe akışını kötü amaçlı istemcilere[(ortadaki adam saldırısı)](https://www.owasp.org/index.php/Man-in-the-middle_attack)gönderen dolaylı hibe akışını koruyan yeniden yönlendirme URL'si ile istemci kimliğini doğrulamak için kullanılır.

### <a name="resource-owner-password-credentials-grant"></a>Kaynak Sahibi Şifre Kimlik Bilgileri Hibesi

Şimdi IETF's OAuth 2 [Kaynak Sahibi Şifre Kimlik Bilgileri Hibe](http://tools.ietf.org/html/rfc6749#section-4.3) bölümüne bakın.

 Şekil 5'te gösterilen [Kaynak Sahibi Parola Kimlik Bilgileri Hibe](http://tools.ietf.org/html/rfc6749#section-4.3) akışı, OWIN OAuth aracının izlediği akış ve eşlemedir.

| Kaynak Sahibi Parola Kimlik Bilgileri Hibe bölümünden akış adımları | Örnek indirme şu adımları gerçekleştirir: |
| --- | --- |
|  |  |
| (A) Kaynak sahibi istemciye kullanıcı adı ve parolasını verir. |  |
|  |  |
| (B) İstemci, kaynak sahibinden alınan kimlik bilgilerini ekleyerek yetkilendirme sunucusunun belirteç bitiş noktasından bir erişim belirteci ister. İstek tevekkül ederken, istemci yetkilendirme sunucusuyla kimlik doğrulaması sağlar. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) Yetkilendirme sunucusu istemcinin kimliğini doğrular ve kaynak sahibi kimlik bilgilerini doğrular ve geçerliyse, bir erişim belirteci verir. |  |

Burada örnek `Provider.GrantResourceOwnerCredentials`uygulama:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> Yukarıdaki kod öğreticinin bu bölümünü açıklamak için tasarlanmıştır ve güvenli veya üretim uygulamalarında kullanılmamalıdır. Kaynak sahiplerinin kimlik bilgilerini denetlemez. Her kimlik bilgisinin geçerli olduğunu varsayar ve bunun için yeni bir kimlik oluşturur. Yeni kimlik, erişim belirteci oluşturmak ve belirteci yenilemek için kullanılacaktır. Lütfen kodu kendi güvenli hesap yönetim kodunuzla değiştirin.


### <a name="client-credentials-grant"></a>Müşteri Kimlik Bilgileri Hibesi

Şimdi IETF's OAuth 2 [Müşteri Kimlik Bilgileri Hibe](http://tools.ietf.org/html/rfc6749#section-4.4) bölümüne bakın.

 Şekil 6'da gösterilen [İstemci Kimlik Bilgileri Hibe](http://tools.ietf.org/html/rfc6749#section-4.4) akışı, OWIN OAuth aracının izlediği akış ve eşlemedir.

| İstemci Kimlik Bilgileri Hibe bölümünden akış adımları | Örnek indirme şu adımları gerçekleştirir: |
| --- | --- |
|  |  |
| (A) İstemci yetkilendirme sunucusuyla kimlik doğrular ve belirteç bitiş noktasından bir erişim belirteci ister. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) Yetkilendirme sunucusu istemcinin kimliğini doğrular ve geçerliyse, bir erişim belirteci sağlar. |  |

Burada örnek `Provider.GrantClientCredentials`uygulama:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> Yukarıdaki kod öğreticinin bu bölümünü açıklamak için tasarlanmıştır ve güvenli veya üretim uygulamalarında kullanılmamalıdır. Lütfen kodu kendi güvenli istemci yönetim kodunuzla değiştirin.


### <a name="refresh-token"></a>Belirteci Yenile

Şimdi IETF's OAuth 2 [Yenile Token](http://tools.ietf.org/html/rfc6749#section-1.5) bölümüne bakın.

 Şekil 2'de gösterilen [Token'i Yenile](http://tools.ietf.org/html/rfc6749#section-1.5) akışı, OWIN OAuth aracının izlediği akış ve haritalamadır.

| İstemci Kimlik Bilgileri Hibe bölümünden akış adımları | Örnek indirme şu adımları gerçekleştirir: |
| --- | --- |
|  |  |
| (G) İstemci, yetkilendirme sunucusuyla kimlik doğrulaması yaparak ve yenileme belirteci sunarak yeni bir erişim belirteci ister. İstemci kimlik doğrulama gereksinimleri istemci türüne ve yetkilendirme sunucusu ilkelerine dayanır. | Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (H) Yetkilendirme sunucusu istemcinin kimliğini doğrular ve yenileme belirteci doğrular ve geçerliyse, yeni bir erişim belirteci (ve isteğe bağlı olarak yeni bir yenileme belirteci) sorunları. |  |

Burada örnek `Provider.GrantRefreshToken`uygulama:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>Access Token tarafından korunan bir Kaynak Sunucusu Oluşturma

Boş bir web uygulaması projesi oluşturun ve projeye aşağıdaki paketleri yükleyin:

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

Bir başlangıç sınıfı oluşturun ve kimlik doğrulaması ve Web API'sini yapılandırın. Örnek indirmede *YetkilendirmeServer\ResourceServer\Startup.cs'ye* bakın.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

Bkz. Örnek indirmede *\_YetkilendirmeServer\ResourceServer\App Start\Startup.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

Bkz. Örnek indirmede *\_YetkilendirmeServer\ResourceServer\App Start\Startup.WebApi.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`yöntem tüm etki alanları için CORS sağlar.
- `UseOAuthBearerAuthentication`yöntem, istekteki yetkilendirme üstbilgisinden taşıyıcı belirteci belirteci nialını alacak ve doğrulayacak Olan OAuth taşıyıcı belirteç kimlik doğrulaması ara ware'i sağlar.
- `Config.SuppressDefaultHostAuthenticaiton`varsayılan ana bilgisayar ını uygulamadan doğrulanmış ana bilgisayardan bastırır, bu nedenle bu çağrıdan sonra tüm istekler anonim olur.
- `HostAuthenticationFilter`sadece belirtilen kimlik doğrulama türü için kimlik doğrulamasını sağlar. Bu durumda, taşıyıcı kimlik doğrulama türüdür.

Kimlik doğrulaması yapılan kimliği göstermek için, geçerli kullanıcının taleplerini ortaya çıkarmak için bir ApiController oluştururuz.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

Yetkilendirme sunucusu ve kaynak sunucusu aynı bilgisayarda değilse, OAuth aracı erişim belirtecişifrelemek ve şifresini çözmek için farklı makine anahtarlarını kullanır. Her iki proje arasında aynı özel anahtarı paylaşmak `machinekey` için, her iki *web.config* dosyasına da aynı ayarı ekliyoruz.

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>OAuth 2.0 İstemcileri Oluştur

 İstemci kodunu basitleştirmek için [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet paketini kullanıyoruz.

### <a name="authorization-code-grant-client"></a>Yetkilendirme Kodu Hibe İstemci

 Bu istemci bir MVC uygulamasıdır. Arka uçtan erişim belirteci almak için bir yetkilendirme kodu hibe akışını tetikler. Aşağıda gösterildiği gibi tek bir sayfası vardır:

![](owin-oauth-20-authorization-server/_static/image3.png)

- **Yetkilendirme** düğmesi, bu istemciye erişim izni vermek için kaynak sahibine bildirmek için tarayıcıyı yetkilendirme sunucusuna yönlendirir.
- **Yenile** düğmesi, geçerli yenileme belirteci kullanılarak yeni bir erişim belirteci alır ve belirteci yeniler.
- **Access Protected Resource API** düğmesi, geçerli kullanıcının talep verilerini almak ve bunları sayfada göstermek için kaynak sunucusunu arar.

Burada istemcinin `HomeController` örnek kodudur.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`varsayılan olarak SSL gerektirir. Demomuz HTTP kullandığından, config dosyasına aşağıdaki ayarı eklemeniz gerekir:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> Güvenlik - Bir üretim uygulamasında SSL'yi asla devre dışı kmayın. Giriş kimlik bilgileriniz artık tüm kabloüzerinde açık metin olarak gönderiliyor. Yukarıdaki kod sadece yerel örnek hata ayıklama ve keşif içindir.


### <a name="implicit-grant-client"></a>Örtülü Hibe İstemci

Bu istemci:

1. Yeni bir pencere açın ve Yetkilendirme Sunucusu'nun yetkili bitiş noktasına yönlendirin.
2. Yeniden yönlendirildiğinde URL parçalarından erişim belirteci alın.

Aşağıdaki resim bu işlemi gösterir:

![](owin-oauth-20-authorization-server/_static/image4.png)

İstemcinin iki sayfası olmalıdır: biri ana sayfa, diğeri geri arama için. *Index.cshtml* dosyasında bulunan örnek JavaScript kodu aşağıdavelvere veda eder:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

*SignIn.cshtml* dosyasındaki geri arama işleme kodu aşağıdavelvere işlenir:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> En iyi yöntem, JavaScript'i harici bir dosyaya taşımak ve Razor biçimlendirmesiyle katıştırmamaktır. Bu örneği basit tutmak için birleştirilmiştir.


### <a name="resource-owner-password-credentials-grant-client"></a>Kaynak Sahibi Şifre Kimlik Bilgileri Hibe İstemci

Bu istemciyi çıkarmak için bir konsol uygulaması kullanıyoruz. Kod aşağıdaki gibidir:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>İstemci Kimlik Bilgileri Hibe İstemci

Kaynak Sahibi Parola Kimlik Bilgileri Hibebenzer, burada konsol uygulama kodu:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
