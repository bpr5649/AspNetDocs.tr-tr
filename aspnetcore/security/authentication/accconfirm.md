---
title: Hesap onaylama ve parola kurtarma ASP.NET Core
author: rick-anderson
description: E-posta onayı ve parola sıfırlama ile ASP.NET Core uygulaması oluşturmayı öğrenin.
ms.author: riande
ms.date: 2/11/2019
uid: security/authentication/accconfirm
ms.openlocfilehash: 77d7b209d57f9ee44f158798ff780ce85c87aaf2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070164"
---
# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a>Hesap onaylama ve parola kurtarma ASP.NET Core

::: moniker range="<= aspnetcore-2.0"

Bkz: [bu PDF dosyası](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core 1.1 ve 2.1 sürümü için.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT) ve [ALi Audette](https://twitter.com/joeaudette)

Bu öğretici, e-posta onayı ve parola sıfırlama ile ASP.NET Core uygulaması oluşturma işlemi gösterilmektedir. Bu öğretici **değil** başına konu. Sahibi olmalısınız:

* [ASP.NET Core](xref:tutorials/razor-pages/razor-pages-start)
* [Kimlik Doğrulaması](xref:security/authentication/identity)
* [Entity Framework Core](xref:data/ef-mvc/intro)

<!-- see C:/Dropbox/wrk/Code/SendGridConsole/Program.cs -->

## <a name="prerequisites"></a>Önkoşullar

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-web--app-and-scaffold-identity"></a>Bir web uygulaması oluşturma ve kimlik iskelesini

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

* Visual Studio'da yeni bir oluşturma **Web uygulaması** adlı proje **WebPWrecover**.
* Seçin **ASP.NET Core 2.1**.
* Varsayılan tutun **kimlik doğrulaması** kümesine **kimlik doğrulaması yok**. Kimlik doğrulaması, bir sonraki adımda eklenir.

Sonraki adımda:

* Düzen sayfası kümesine *~/Pages/Shared/_Layout.cshtml*
* Seçin *hesabı/kaydı*
* Yeni bir **veri bağlamı sınıfı**

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```console
dotnet new webapp -o WebPWrecover
cd WebPWrecover
dotnet tool install -g dotnet-aspnet-codegenerator
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -fi Account.Register -dc WebPWrecover.Models.WebPWrecoverContext
dotnet ef migrations add CreateIdentitySchema
dotnet ef database drop -f
dotnet ef database update
dotnet build
```

Çalıştırma `dotnet aspnet-codegenerator identity --help` yapı iskelesi aracın Yardım almak için.

------

Bölümündeki yönergeleri [kimlik doğrulamasını etkinleştirme](xref:security/authentication/scaffold-identity#useauthentication):

* Ekleme `app.UseAuthentication();` için `Startup.Configure`
* Ekleme `<partial name="_LoginPartial" />` Düzen dosyası için.

## <a name="test-new-user-registration"></a>Test yeni kullanıcı kaydı

Uygulamayı çalıştırın, seçin **kaydetme** bağlamak ve bir kullanıcı kaydı. Yalnızca e-posta doğrulamasını bu noktada, olan [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) özniteliği. Kayıt gönderdikten sonra uygulamaya günlüğe kaydedilir. Yeni kullanıcıların e-postasına doğrulanır kadar oturum açamazsınız için öğreticinin sonraki bölümlerinde kod güncelleştirilir.

[!INCLUDE[](~/includes/view-identity-db.md)]

Tablonun Not `EmailConfirmed` alandır `False`.

Bu e-posta uygulaması bir onay e-posta gönderdiğinde, yeniden sonraki adımda kullanmak isteyebilirsiniz. Sağ tıklatın ve satır **Sil**. E-posta diğer adı silmek, aşağıdaki adımlarda kolaylaştırır.

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a>E-posta onayı gerektir

Yeni bir kullanıcı kaydı e-postayı onaylamak için iyi bir uygulamadır. E-posta, bunlar değil kimliğe bürünerek başka birisi doğrulamak için onay yardımcı olur (diğer bir deyişle, bunlar başka birinin e-posta ile kayıtlı olmayabilirsiniz). Tartışma Forumu var ve bu önlemek istediğinizi varsayalım "yli@example.com"olarak kaydetme"Kimdennolivetto@contoso.com". E-posta onayı olmadan "nolivetto@contoso.com" istenmeyen e-posta uygulamanızdan alabilir. Kullanıcı olarak yanlışlıkla kayıtlı varsayalım "ylo@example.com" ve "yli", yazım hatası fark yüklediniz. Parola kurtarma uygulamayı doğru e-postasına olmadığından bunlar saptayamazdınız. E-posta onayı robotlar sınırlı koruma sağlar. E-posta onayı, çok sayıda e-posta hesaplarına sahip kötü niyetli kullanıcıların koruma sağlamaz.

Genellikle, yeni kullanıcıların onaylanan e-posta sahip oldukları önce web sitenizi herhangi bir veri gönderme engellemek istiyorsunuz.

Güncelleştirme *Areas/Identity/IdentityHostingStartup.cs* onaylanan e-posta gerektirmek için:

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/IdentityHostingStartup.cs?name=snippet1&highlight=10-13)]

`config.SignIn.RequireConfirmedEmail = true;` kayıtlı kullanıcıların e-postasına onaylanana kadar oturum açma engeller.

### <a name="configure-email-provider"></a>E-posta sağlayıcısı yapılandırma

Bu öğreticide [SendGrid](https://sendgrid.com) e-posta göndermek için kullanılır. SendGrid hesabı ve e-posta göndermek için anahtar ihtiyacınız var. Diğer e-posta sağlayıcılarının kullanabilirsiniz. ASP.NET Core 2.x içerir `System.Net.Mail`, uygulamanızdan e-posta göndermenize olanak tanıyan. E-posta göndermek için SendGrid veya başka bir e-posta hizmeti kullanmanızı öneririz. SMTP güvenli ve doğru bir şekilde ayarlamak zordur.

Güvenli e-posta anahtarı almak için bir sınıf oluşturun. Bu örnek için oluşturma *Services/AuthMessageSenderOptions.cs*:

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/AuthMessageSenderOptions.cs?name=snippet1)]

#### <a name="configure-sendgrid-user-secrets"></a>SendGrid kullanıcı parolaları yapılandırın

Benzersiz bir ekleme `<UserSecretsId>` değerini `<PropertyGroup>` proje dosyasının öğe:

[!code-xml[](accconfirm/sample/WebPWrecover21/WebPWrecover.csproj?highlight=5)]

Ayarlama `SendGridUser` ve `SendGridKey` ile [gizli dizi Yöneticisi aracını](xref:security/app-secrets). Örneğin:

```console
C:/WebAppl>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

Windows üzerinde gizli dizi Yöneticisi'ni anahtar/değer çiftleri olarak depolar. bir *secrets.json* dosyası `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` dizin.

İçeriğini *secrets.json* olmayan dosya şifrelenmiş. *Secrets.json* aşağıda gösterilmektedir dosyanın ( `SendGridKey` değer kaldırıldı.)

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```
 
Daha fazla bilgi için [seçenekleri deseni](xref:fundamentals/configuration/options) ve [yapılandırma](xref:fundamentals/configuration/index).

### <a name="install-sendgrid"></a>SendGrid yükleyin

Bu öğretici, e-posta bildirimleri aracılığıyla ekleneceği gösterilmiştir [SendGrid](https://sendgrid.com/), ancak e-posta SMTP veya başka mekanizmalar kullanılarak gönderebilirsiniz.

Yükleme `SendGrid` NuGet paketi:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Paket Yöneticisi konsolundan aşağıdaki komutu girin:

``` PMC
Install-Package SendGrid
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Konsolundan aşağıdaki komutu girin:

```cli
dotnet add package SendGrid
```

------

Bkz: [SendGrid ile ücretsiz olarak kullanmaya başlayın](https://sendgrid.com/free/) ücretsiz SendGrid hesabı kaydedilecek.
### <a name="implement-iemailsender"></a>IEmailSender uygulayın

Uygulama için `IEmailSender`, oluşturma *Services/EmailSender.cs* kodu aşağıdakine benzer:

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/EmailSender.cs)]

### <a name="configure-startup-to-support-email"></a>Başlangıç e-posta destekleyecek şekilde yapılandırma

Aşağıdaki kodu ekleyin `ConfigureServices` yönteminde *Startup.cs* dosyası:

* Ekleme `EmailSender` geçici bir hizmet olarak.
* Kayıt `AuthMessageSenderOptions` yapılandırma örneği.

[!code-csharp[](accconfirm/sample/WebPWrecover21/Startup.cs?name=snippet2&highlight=12-99)]

## <a name="enable-account-confirmation-and-password-recovery"></a>Hesap onaylama ve parola kurtarmayı etkinleştir

Şablon hesap onaylama ve parola kurtarma kodu var. Bulma `OnPostAsync` yönteminde *Areas/Identity/Pages/Account/Register.cshtml.cs*.

Yeni kaydettiğiniz kullanıcıların otomatik olarak aşağıdaki satırı açıklama satırı yaparak oturum engellemek:

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

Vurgulanmış satır ile tam yöntemi gösterilir:

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/Pages/Account/Register.cshtml.cs?highlight=22&name=snippet_Register)]

## <a name="register-confirm-email-and-reset-password"></a>Kaydetme, e-posta onayı ve parola sıfırlama

Web uygulamasını çalıştırın ve hesap onaylama ve parola kurtarma akışı test edin.

* Uygulamayı çalıştırın ve yeni bir kullanıcı kaydı

  ![Web uygulaması görünümü hesabı Kaydet](accconfirm/_static/loginaccconfirm1.png)

* Hesap onay bağlantısı için e-postanızı kontrol edin. Bkz: [hata ayıklama, e-posta](#debug) e-posta alırsanız yok.
* E-postanızı doğrulamak için bağlantıya tıklayın.
* E-postanıza ve parola ile oturum açın.
* Oturumu kapatın.

### <a name="view-the-manage-page"></a>Yönet sayfasını görüntüle

Tarayıcıda kullanıcı adınızı seçin: ![tarayıcı penceresi ile kullanıcı adı](accconfirm/_static/un.png)

Kullanıcı adı görmek için Gezinti genişletmeniz gerekebilir.

![navbar](accconfirm/_static/x.png)

İle Yönet sayfasında görüntülenen **profili** sekmesi seçili. **E-posta** e-posta belirten bir onay kutusu onaylanan gösterir.

### <a name="test-password-reset"></a>Test parola sıfırlama

* Oturum açmadıysanız, seçin **oturum kapatma**.
* Seçin **oturum** seçin ve bağlama **parolanızı mı unuttunuz?** bağlantı.
* Hesap kaydolmak için kullandığınız e-posta girin.
* Parolanızı sıfırlamak için bir bağlantı içeren bir e-posta gönderilir. E-postanızı kontrol edin ve parolanızı sıfırlamak için bağlantıya tıklayın. Parolanızı başarıyla sıfırladıktan sonra e-posta ve yeni bir parola ile oturum açabilirsiniz.

<a name="debug"></a>

### <a name="debug-email"></a>E-posta hata ayıklama

E-posta çalışma erişemiyorsanız:

* Bir kesim noktası `EmailSender.Execute` doğrulamak için `SendGridClient.SendEmailAsync` çağrılır.
* Oluşturma bir [e-posta göndermek için konsol uygulaması](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html) benzer bir kod kullanarak `EmailSender.Execute`.
* Gözden geçirme [e-posta etkinlik](https://sendgrid.com/docs/User_Guide/email_activity.html) sayfası.
* İstenmeyen posta klasörünüzü kontrol edin.
* Farklı bir e-posta sağlayıcısı (Microsoft, Yahoo, Gmail, vb.) başka bir e-posta diğer adı deneyin
* Farklı bir e-posta hesaplarına göndermeyi deneyin.

**En iyi güvenlik uygulaması** için **değil** test ve geliştirme üretim gizli dizileri kullanın. Uygulamayı Azure'a yayımlama, Web uygulamasını Azure Portalı'nda Uygulama ayarları olarak SendGrid parolaları ayarlayabilirsiniz. Yapılandırma sistemi ortam değişkenlerinden anahtarları okumak için ayarlanır.

## <a name="combine-social-and-local-login-accounts"></a>Sosyal ve yerel oturum açma hesabını birleştirin

Bu bölümde tamamlamak için önce bir dış kimlik doğrulama sağlayıcısı etkinleştirmeniz gerekir. Bkz: [Facebook, Google ve dış sağlayıcı kimlik doğrulaması](xref:security/authentication/social/index).

Yerel hem de sosyal hesaplar, e-posta bağlantısına tıklayarak birleştirebilirsiniz. Aşağıdaki sırayla "RickAndMSFT@gmail.com" ilk olarak bir yerel oturum açın; oluşturulur ancak, bir sosyal oturum açma ilk hesap oluşturun, sonra bir yerel oturum açma ekleme.

![Web uygulaması: RickAndMSFT@gmail.com kimliği doğrulanmış kullanıcı](accconfirm/_static/rick.png)

Tıklayarak **Yönet** bağlantı. Bu hesapla ilişkili 0 dış (sosyal oturum açma bilgileri) unutmayın.

![Görünümü yönetme](accconfirm/_static/manage.png)

Başka bir oturum açma hizmeti bağlantısını tıklayın ve uygulama isteklerini kabul etmek. Aşağıdaki görüntüde, Facebook Dış kimlik doğrulama sağlayıcısı'dır:

![Facebook listeleme görünümünüzü harici oturum açmaları yönetme](accconfirm/_static/fb.png)

İki hesap birleştirilmiştir. Her iki hesabıyla oturum açabilir. Kullanıcılarınızın kendi sosyal oturum açma kimlik doğrulama hizmeti çalışmıyor veya bunlar sosyal hesaplarına erişim daha büyük bir olasılıkla kaybettiğinizde durumunda yerel hesaplar eklemek isteyebilirsiniz.

## <a name="enable-account-confirmation-after-a-site-has-users"></a>Kullanıcılar bir siteye sahip olduktan sonra hesap onaylama etkinleştir

Var olan tüm kullanıcıları etkinleştirme hesap onaylama sitesinde kullanıcılarla kilitler. Varolan kullanıcı hesaplarını onaylanan değildir çünkü kilitlidir. Mevcut kullanıcı kilitlemesinin geçici olarak çözmek için aşağıdaki yaklaşımlardan birini kullanın:

* Tüm mevcut kullanıcılar onaylanıp olarak işaretlemek için veritabanı güncelleştirin.
* Mevcut kullanıcıları onaylayın. Örneğin, batch onay bağlantılarının ile e-posta gönderme.

::: moniker-end
