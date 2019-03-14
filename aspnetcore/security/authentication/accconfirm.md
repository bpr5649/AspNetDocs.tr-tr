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
# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a><span data-ttu-id="326e3-103">Hesap onaylama ve parola kurtarma ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="326e3-103">Account confirmation and password recovery in ASP.NET Core</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="326e3-104">Bkz: [bu PDF dosyası](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core 1.1 ve 2.1 sürümü için.</span><span class="sxs-lookup"><span data-stu-id="326e3-104">See [this PDF file](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core 1.1 and 2.1 version.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="326e3-105">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT) ve [ALi Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="326e3-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="326e3-106">Bu öğretici, e-posta onayı ve parola sıfırlama ile ASP.NET Core uygulaması oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="326e3-106">This tutorial shows how to build an ASP.NET Core app with email confirmation and password reset.</span></span> <span data-ttu-id="326e3-107">Bu öğretici **değil** başına konu.</span><span class="sxs-lookup"><span data-stu-id="326e3-107">This tutorial is **not** a beginning topic.</span></span> <span data-ttu-id="326e3-108">Sahibi olmalısınız:</span><span class="sxs-lookup"><span data-stu-id="326e3-108">You should be familiar with:</span></span>

* [<span data-ttu-id="326e3-109">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="326e3-109">ASP.NET Core</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="326e3-110">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="326e3-110">Authentication</span></span>](xref:security/authentication/identity)
* [<span data-ttu-id="326e3-111">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="326e3-111">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<!-- see C:/Dropbox/wrk/Code/SendGridConsole/Program.cs -->

## <a name="prerequisites"></a><span data-ttu-id="326e3-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="326e3-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-web--app-and-scaffold-identity"></a><span data-ttu-id="326e3-113">Bir web uygulaması oluşturma ve kimlik iskelesini</span><span class="sxs-lookup"><span data-stu-id="326e3-113">Create a web  app and scaffold Identity</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="326e3-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="326e3-114">Visual Studio</span></span>](#tab/visual-studio) 

* <span data-ttu-id="326e3-115">Visual Studio'da yeni bir oluşturma **Web uygulaması** adlı proje **WebPWrecover**.</span><span class="sxs-lookup"><span data-stu-id="326e3-115">In Visual Studio, create a new **Web Application** project named **WebPWrecover**.</span></span>
* <span data-ttu-id="326e3-116">Seçin **ASP.NET Core 2.1**.</span><span class="sxs-lookup"><span data-stu-id="326e3-116">Select **ASP.NET Core 2.1**.</span></span>
* <span data-ttu-id="326e3-117">Varsayılan tutun **kimlik doğrulaması** kümesine **kimlik doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="326e3-117">Keep the default **Authentication** set to **No Authentication**.</span></span> <span data-ttu-id="326e3-118">Kimlik doğrulaması, bir sonraki adımda eklenir.</span><span class="sxs-lookup"><span data-stu-id="326e3-118">Authentication is added in the next step.</span></span>

<span data-ttu-id="326e3-119">Sonraki adımda:</span><span class="sxs-lookup"><span data-stu-id="326e3-119">In the next step:</span></span>

* <span data-ttu-id="326e3-120">Düzen sayfası kümesine *~/Pages/Shared/_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="326e3-120">Set the layout page to *~/Pages/Shared/_Layout.cshtml*</span></span>
* <span data-ttu-id="326e3-121">Seçin *hesabı/kaydı*</span><span class="sxs-lookup"><span data-stu-id="326e3-121">Select *Account/Register*</span></span>
* <span data-ttu-id="326e3-122">Yeni bir **veri bağlamı sınıfı**</span><span class="sxs-lookup"><span data-stu-id="326e3-122">Create a new **Data context class**</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="326e3-123">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="326e3-123">.NET Core CLI</span></span>](#tab/netcore-cli)

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

<span data-ttu-id="326e3-124">Çalıştırma `dotnet aspnet-codegenerator identity --help` yapı iskelesi aracın Yardım almak için.</span><span class="sxs-lookup"><span data-stu-id="326e3-124">Run `dotnet aspnet-codegenerator identity --help` to get help on the scaffolding tool.</span></span>

------

<span data-ttu-id="326e3-125">Bölümündeki yönergeleri [kimlik doğrulamasını etkinleştirme](xref:security/authentication/scaffold-identity#useauthentication):</span><span class="sxs-lookup"><span data-stu-id="326e3-125">Follow the instructions in [Enable authentication](xref:security/authentication/scaffold-identity#useauthentication):</span></span>

* <span data-ttu-id="326e3-126">Ekleme `app.UseAuthentication();` için `Startup.Configure`</span><span class="sxs-lookup"><span data-stu-id="326e3-126">Add `app.UseAuthentication();` to `Startup.Configure`</span></span>
* <span data-ttu-id="326e3-127">Ekleme `<partial name="_LoginPartial" />` Düzen dosyası için.</span><span class="sxs-lookup"><span data-stu-id="326e3-127">Add `<partial name="_LoginPartial" />` to the layout file.</span></span>

## <a name="test-new-user-registration"></a><span data-ttu-id="326e3-128">Test yeni kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="326e3-128">Test new user registration</span></span>

<span data-ttu-id="326e3-129">Uygulamayı çalıştırın, seçin **kaydetme** bağlamak ve bir kullanıcı kaydı.</span><span class="sxs-lookup"><span data-stu-id="326e3-129">Run the app, select the **Register** link, and register a user.</span></span> <span data-ttu-id="326e3-130">Yalnızca e-posta doğrulamasını bu noktada, olan [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) özniteliği.</span><span class="sxs-lookup"><span data-stu-id="326e3-130">At this point, the only validation on the email is with the [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) attribute.</span></span> <span data-ttu-id="326e3-131">Kayıt gönderdikten sonra uygulamaya günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-131">After submitting the registration, you are logged into the app.</span></span> <span data-ttu-id="326e3-132">Yeni kullanıcıların e-postasına doğrulanır kadar oturum açamazsınız için öğreticinin sonraki bölümlerinde kod güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-132">Later in the tutorial, the code is updated so new users can't sign in until their email is validated.</span></span>

[!INCLUDE[](~/includes/view-identity-db.md)]

<span data-ttu-id="326e3-133">Tablonun Not `EmailConfirmed` alandır `False`.</span><span class="sxs-lookup"><span data-stu-id="326e3-133">Note the table's `EmailConfirmed` field is `False`.</span></span>

<span data-ttu-id="326e3-134">Bu e-posta uygulaması bir onay e-posta gönderdiğinde, yeniden sonraki adımda kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-134">You might want to use this email again in the next step when the app sends a confirmation email.</span></span> <span data-ttu-id="326e3-135">Sağ tıklatın ve satır **Sil**.</span><span class="sxs-lookup"><span data-stu-id="326e3-135">Right-click on the row and select **Delete**.</span></span> <span data-ttu-id="326e3-136">E-posta diğer adı silmek, aşağıdaki adımlarda kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="326e3-136">Deleting the email alias makes it easier in the following steps.</span></span>

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a><span data-ttu-id="326e3-137">E-posta onayı gerektir</span><span class="sxs-lookup"><span data-stu-id="326e3-137">Require email confirmation</span></span>

<span data-ttu-id="326e3-138">Yeni bir kullanıcı kaydı e-postayı onaylamak için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="326e3-138">It's a best practice to confirm the email of a new user registration.</span></span> <span data-ttu-id="326e3-139">E-posta, bunlar değil kimliğe bürünerek başka birisi doğrulamak için onay yardımcı olur (diğer bir deyişle, bunlar başka birinin e-posta ile kayıtlı olmayabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="326e3-139">Email confirmation helps to verify they're not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="326e3-140">Tartışma Forumu var ve bu önlemek istediğinizi varsayalım "yli@example.com"olarak kaydetme"Kimdennolivetto@contoso.com".</span><span class="sxs-lookup"><span data-stu-id="326e3-140">Suppose you had a discussion forum, and you wanted to prevent "yli@example.com" from registering as "nolivetto@contoso.com".</span></span> <span data-ttu-id="326e3-141">E-posta onayı olmadan "nolivetto@contoso.com" istenmeyen e-posta uygulamanızdan alabilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-141">Without email confirmation, "nolivetto@contoso.com" could receive unwanted email from your app.</span></span> <span data-ttu-id="326e3-142">Kullanıcı olarak yanlışlıkla kayıtlı varsayalım "ylo@example.com" ve "yli", yazım hatası fark yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-142">Suppose the user accidentally registered as "ylo@example.com" and hadn't noticed the misspelling of "yli".</span></span> <span data-ttu-id="326e3-143">Parola kurtarma uygulamayı doğru e-postasına olmadığından bunlar saptayamazdınız.</span><span class="sxs-lookup"><span data-stu-id="326e3-143">They wouldn't be able to use password recovery because the app doesn't have their correct email.</span></span> <span data-ttu-id="326e3-144">E-posta onayı robotlar sınırlı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="326e3-144">Email confirmation provides limited protection from bots.</span></span> <span data-ttu-id="326e3-145">E-posta onayı, çok sayıda e-posta hesaplarına sahip kötü niyetli kullanıcıların koruma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="326e3-145">Email confirmation doesn't provide protection from malicious users with many email accounts.</span></span>

<span data-ttu-id="326e3-146">Genellikle, yeni kullanıcıların onaylanan e-posta sahip oldukları önce web sitenizi herhangi bir veri gönderme engellemek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="326e3-146">You generally want to prevent new users from posting any data to your web site before they have a confirmed email.</span></span>

<span data-ttu-id="326e3-147">Güncelleştirme *Areas/Identity/IdentityHostingStartup.cs* onaylanan e-posta gerektirmek için:</span><span class="sxs-lookup"><span data-stu-id="326e3-147">Update *Areas/Identity/IdentityHostingStartup.cs*  to require a confirmed email:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/IdentityHostingStartup.cs?name=snippet1&highlight=10-13)]

<span data-ttu-id="326e3-148">`config.SignIn.RequireConfirmedEmail = true;` kayıtlı kullanıcıların e-postasına onaylanana kadar oturum açma engeller.</span><span class="sxs-lookup"><span data-stu-id="326e3-148">`config.SignIn.RequireConfirmedEmail = true;` prevents registered users from logging in until their email is confirmed.</span></span>

### <a name="configure-email-provider"></a><span data-ttu-id="326e3-149">E-posta sağlayıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="326e3-149">Configure email provider</span></span>

<span data-ttu-id="326e3-150">Bu öğreticide [SendGrid](https://sendgrid.com) e-posta göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="326e3-150">In this tutorial, [SendGrid](https://sendgrid.com) is used to send email.</span></span> <span data-ttu-id="326e3-151">SendGrid hesabı ve e-posta göndermek için anahtar ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="326e3-151">You need a SendGrid account and key to send email.</span></span> <span data-ttu-id="326e3-152">Diğer e-posta sağlayıcılarının kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-152">You can use other email providers.</span></span> <span data-ttu-id="326e3-153">ASP.NET Core 2.x içerir `System.Net.Mail`, uygulamanızdan e-posta göndermenize olanak tanıyan.</span><span class="sxs-lookup"><span data-stu-id="326e3-153">ASP.NET Core 2.x includes `System.Net.Mail`, which allows you to send email from your app.</span></span> <span data-ttu-id="326e3-154">E-posta göndermek için SendGrid veya başka bir e-posta hizmeti kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="326e3-154">We recommend you use SendGrid or another email service to send email.</span></span> <span data-ttu-id="326e3-155">SMTP güvenli ve doğru bir şekilde ayarlamak zordur.</span><span class="sxs-lookup"><span data-stu-id="326e3-155">SMTP is difficult to secure and set up correctly.</span></span>

<span data-ttu-id="326e3-156">Güvenli e-posta anahtarı almak için bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="326e3-156">Create a class to fetch the secure email key.</span></span> <span data-ttu-id="326e3-157">Bu örnek için oluşturma *Services/AuthMessageSenderOptions.cs*:</span><span class="sxs-lookup"><span data-stu-id="326e3-157">For this sample, create *Services/AuthMessageSenderOptions.cs*:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/AuthMessageSenderOptions.cs?name=snippet1)]

#### <a name="configure-sendgrid-user-secrets"></a><span data-ttu-id="326e3-158">SendGrid kullanıcı parolaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="326e3-158">Configure SendGrid user secrets</span></span>

<span data-ttu-id="326e3-159">Benzersiz bir ekleme `<UserSecretsId>` değerini `<PropertyGroup>` proje dosyasının öğe:</span><span class="sxs-lookup"><span data-stu-id="326e3-159">Add a unique `<UserSecretsId>` value to the `<PropertyGroup>` element of the project file:</span></span>

[!code-xml[](accconfirm/sample/WebPWrecover21/WebPWrecover.csproj?highlight=5)]

<span data-ttu-id="326e3-160">Ayarlama `SendGridUser` ve `SendGridKey` ile [gizli dizi Yöneticisi aracını](xref:security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="326e3-160">Set the `SendGridUser` and `SendGridKey` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="326e3-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="326e3-161">For example:</span></span>

```console
C:/WebAppl>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

<span data-ttu-id="326e3-162">Windows üzerinde gizli dizi Yöneticisi'ni anahtar/değer çiftleri olarak depolar. bir *secrets.json* dosyası `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` dizin.</span><span class="sxs-lookup"><span data-stu-id="326e3-162">On Windows, Secret Manager stores keys/value pairs in a *secrets.json* file in the `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` directory.</span></span>

<span data-ttu-id="326e3-163">İçeriğini *secrets.json* olmayan dosya şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="326e3-163">The contents of the *secrets.json* file aren't encrypted.</span></span> <span data-ttu-id="326e3-164">*Secrets.json* aşağıda gösterilmektedir dosyanın ( `SendGridKey` değer kaldırıldı.)</span><span class="sxs-lookup"><span data-stu-id="326e3-164">The *secrets.json* file is shown below (the `SendGridKey` value has been removed.)</span></span>

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```
 
<span data-ttu-id="326e3-165">Daha fazla bilgi için [seçenekleri deseni](xref:fundamentals/configuration/options) ve [yapılandırma](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="326e3-165">For more information, see the [Options pattern](xref:fundamentals/configuration/options) and [configuration](xref:fundamentals/configuration/index).</span></span>

### <a name="install-sendgrid"></a><span data-ttu-id="326e3-166">SendGrid yükleyin</span><span class="sxs-lookup"><span data-stu-id="326e3-166">Install SendGrid</span></span>

<span data-ttu-id="326e3-167">Bu öğretici, e-posta bildirimleri aracılığıyla ekleneceği gösterilmiştir [SendGrid](https://sendgrid.com/), ancak e-posta SMTP veya başka mekanizmalar kullanılarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-167">This tutorial shows how to add email notifications through [SendGrid](https://sendgrid.com/), but you can send email using SMTP and other mechanisms.</span></span>

<span data-ttu-id="326e3-168">Yükleme `SendGrid` NuGet paketi:</span><span class="sxs-lookup"><span data-stu-id="326e3-168">Install the `SendGrid` NuGet package:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="326e3-169">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="326e3-169">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="326e3-170">Paket Yöneticisi konsolundan aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="326e3-170">From the Package Manager Console, enter the following command:</span></span>

``` PMC
Install-Package SendGrid
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="326e3-171">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="326e3-171">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="326e3-172">Konsolundan aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="326e3-172">From the console, enter the following command:</span></span>

```cli
dotnet add package SendGrid
```

------

<span data-ttu-id="326e3-173">Bkz: [SendGrid ile ücretsiz olarak kullanmaya başlayın](https://sendgrid.com/free/) ücretsiz SendGrid hesabı kaydedilecek.</span><span class="sxs-lookup"><span data-stu-id="326e3-173">See [Get Started with SendGrid for Free](https://sendgrid.com/free/) to register for a free SendGrid account.</span></span>
### <a name="implement-iemailsender"></a><span data-ttu-id="326e3-174">IEmailSender uygulayın</span><span class="sxs-lookup"><span data-stu-id="326e3-174">Implement IEmailSender</span></span>

<span data-ttu-id="326e3-175">Uygulama için `IEmailSender`, oluşturma *Services/EmailSender.cs* kodu aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="326e3-175">To Implement `IEmailSender`, create *Services/EmailSender.cs* with code similar to the following:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/EmailSender.cs)]

### <a name="configure-startup-to-support-email"></a><span data-ttu-id="326e3-176">Başlangıç e-posta destekleyecek şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="326e3-176">Configure startup to support email</span></span>

<span data-ttu-id="326e3-177">Aşağıdaki kodu ekleyin `ConfigureServices` yönteminde *Startup.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="326e3-177">Add the following code to the `ConfigureServices` method in the *Startup.cs* file:</span></span>

* <span data-ttu-id="326e3-178">Ekleme `EmailSender` geçici bir hizmet olarak.</span><span class="sxs-lookup"><span data-stu-id="326e3-178">Add `EmailSender` as a transient service.</span></span>
* <span data-ttu-id="326e3-179">Kayıt `AuthMessageSenderOptions` yapılandırma örneği.</span><span class="sxs-lookup"><span data-stu-id="326e3-179">Register the `AuthMessageSenderOptions` configuration instance.</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Startup.cs?name=snippet2&highlight=12-99)]

## <a name="enable-account-confirmation-and-password-recovery"></a><span data-ttu-id="326e3-180">Hesap onaylama ve parola kurtarmayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="326e3-180">Enable account confirmation and password recovery</span></span>

<span data-ttu-id="326e3-181">Şablon hesap onaylama ve parola kurtarma kodu var.</span><span class="sxs-lookup"><span data-stu-id="326e3-181">The template has the code for account confirmation and password recovery.</span></span> <span data-ttu-id="326e3-182">Bulma `OnPostAsync` yönteminde *Areas/Identity/Pages/Account/Register.cshtml.cs*.</span><span class="sxs-lookup"><span data-stu-id="326e3-182">Find the `OnPostAsync` method in *Areas/Identity/Pages/Account/Register.cshtml.cs*.</span></span>

<span data-ttu-id="326e3-183">Yeni kaydettiğiniz kullanıcıların otomatik olarak aşağıdaki satırı açıklama satırı yaparak oturum engellemek:</span><span class="sxs-lookup"><span data-stu-id="326e3-183">Prevent newly registered users from being automatically logged on by commenting out the following line:</span></span>

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

<span data-ttu-id="326e3-184">Vurgulanmış satır ile tam yöntemi gösterilir:</span><span class="sxs-lookup"><span data-stu-id="326e3-184">The complete method is shown with the changed line highlighted:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/Pages/Account/Register.cshtml.cs?highlight=22&name=snippet_Register)]

## <a name="register-confirm-email-and-reset-password"></a><span data-ttu-id="326e3-185">Kaydetme, e-posta onayı ve parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="326e3-185">Register, confirm email, and reset password</span></span>

<span data-ttu-id="326e3-186">Web uygulamasını çalıştırın ve hesap onaylama ve parola kurtarma akışı test edin.</span><span class="sxs-lookup"><span data-stu-id="326e3-186">Run the web app, and test the account confirmation and password recovery flow.</span></span>

* <span data-ttu-id="326e3-187">Uygulamayı çalıştırın ve yeni bir kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="326e3-187">Run the app and register a new user</span></span>

  ![Web uygulaması görünümü hesabı Kaydet](accconfirm/_static/loginaccconfirm1.png)

* <span data-ttu-id="326e3-189">Hesap onay bağlantısı için e-postanızı kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="326e3-189">Check your email for the account confirmation link.</span></span> <span data-ttu-id="326e3-190">Bkz: [hata ayıklama, e-posta](#debug) e-posta alırsanız yok.</span><span class="sxs-lookup"><span data-stu-id="326e3-190">See [Debug email](#debug) if you don't get the email.</span></span>
* <span data-ttu-id="326e3-191">E-postanızı doğrulamak için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="326e3-191">Click the link to confirm your email.</span></span>
* <span data-ttu-id="326e3-192">E-postanıza ve parola ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="326e3-192">Sign in with your email and password.</span></span>
* <span data-ttu-id="326e3-193">Oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="326e3-193">Sign out.</span></span>

### <a name="view-the-manage-page"></a><span data-ttu-id="326e3-194">Yönet sayfasını görüntüle</span><span class="sxs-lookup"><span data-stu-id="326e3-194">View the manage page</span></span>

<span data-ttu-id="326e3-195">Tarayıcıda kullanıcı adınızı seçin: ![tarayıcı penceresi ile kullanıcı adı](accconfirm/_static/un.png)</span><span class="sxs-lookup"><span data-stu-id="326e3-195">Select your user name in the browser: ![browser window with user name](accconfirm/_static/un.png)</span></span>

<span data-ttu-id="326e3-196">Kullanıcı adı görmek için Gezinti genişletmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-196">You might need to expand the navbar to see user name.</span></span>

![navbar](accconfirm/_static/x.png)

<span data-ttu-id="326e3-198">İle Yönet sayfasında görüntülenen **profili** sekmesi seçili.</span><span class="sxs-lookup"><span data-stu-id="326e3-198">The manage page is displayed with the **Profile** tab selected.</span></span> <span data-ttu-id="326e3-199">**E-posta** e-posta belirten bir onay kutusu onaylanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="326e3-199">The **Email** shows a check box indicating the email has been confirmed.</span></span>

### <a name="test-password-reset"></a><span data-ttu-id="326e3-200">Test parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="326e3-200">Test password reset</span></span>

* <span data-ttu-id="326e3-201">Oturum açmadıysanız, seçin **oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="326e3-201">If you're logged in, select **Logout**.</span></span>
* <span data-ttu-id="326e3-202">Seçin **oturum** seçin ve bağlama **parolanızı mı unuttunuz?** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="326e3-202">Select the **Log in** link and select the **Forgot your password?** link.</span></span>
* <span data-ttu-id="326e3-203">Hesap kaydolmak için kullandığınız e-posta girin.</span><span class="sxs-lookup"><span data-stu-id="326e3-203">Enter the email you used to register the account.</span></span>
* <span data-ttu-id="326e3-204">Parolanızı sıfırlamak için bir bağlantı içeren bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-204">An email with a link to reset your password is sent.</span></span> <span data-ttu-id="326e3-205">E-postanızı kontrol edin ve parolanızı sıfırlamak için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="326e3-205">Check your email and click the link to reset your password.</span></span> <span data-ttu-id="326e3-206">Parolanızı başarıyla sıfırladıktan sonra e-posta ve yeni bir parola ile oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-206">After your password has been successfully reset, you can sign in with your email and new password.</span></span>

<a name="debug"></a>

### <a name="debug-email"></a><span data-ttu-id="326e3-207">E-posta hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="326e3-207">Debug email</span></span>

<span data-ttu-id="326e3-208">E-posta çalışma erişemiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="326e3-208">If you can't get email working:</span></span>

* <span data-ttu-id="326e3-209">Bir kesim noktası `EmailSender.Execute` doğrulamak için `SendGridClient.SendEmailAsync` çağrılır.</span><span class="sxs-lookup"><span data-stu-id="326e3-209">Set a breakpoint in `EmailSender.Execute` to verify `SendGridClient.SendEmailAsync` is called.</span></span>
* <span data-ttu-id="326e3-210">Oluşturma bir [e-posta göndermek için konsol uygulaması](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html) benzer bir kod kullanarak `EmailSender.Execute`.</span><span class="sxs-lookup"><span data-stu-id="326e3-210">Create a [console app to send email](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html) using similar code to `EmailSender.Execute`.</span></span>
* <span data-ttu-id="326e3-211">Gözden geçirme [e-posta etkinlik](https://sendgrid.com/docs/User_Guide/email_activity.html) sayfası.</span><span class="sxs-lookup"><span data-stu-id="326e3-211">Review the [Email Activity](https://sendgrid.com/docs/User_Guide/email_activity.html) page.</span></span>
* <span data-ttu-id="326e3-212">İstenmeyen posta klasörünüzü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="326e3-212">Check your spam folder.</span></span>
* <span data-ttu-id="326e3-213">Farklı bir e-posta sağlayıcısı (Microsoft, Yahoo, Gmail, vb.) başka bir e-posta diğer adı deneyin</span><span class="sxs-lookup"><span data-stu-id="326e3-213">Try another email alias on a different email provider (Microsoft, Yahoo, Gmail, etc.)</span></span>
* <span data-ttu-id="326e3-214">Farklı bir e-posta hesaplarına göndermeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="326e3-214">Try sending to different email accounts.</span></span>

<span data-ttu-id="326e3-215">**En iyi güvenlik uygulaması** için **değil** test ve geliştirme üretim gizli dizileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="326e3-215">**A security best practice** is to **not** use production secrets in test and development.</span></span> <span data-ttu-id="326e3-216">Uygulamayı Azure'a yayımlama, Web uygulamasını Azure Portalı'nda Uygulama ayarları olarak SendGrid parolaları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-216">If you publish the app to Azure, you can set the SendGrid secrets as application settings in the Azure Web App portal.</span></span> <span data-ttu-id="326e3-217">Yapılandırma sistemi ortam değişkenlerinden anahtarları okumak için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="326e3-217">The configuration system is set up to read keys from environment variables.</span></span>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="326e3-218">Sosyal ve yerel oturum açma hesabını birleştirin</span><span class="sxs-lookup"><span data-stu-id="326e3-218">Combine social and local login accounts</span></span>

<span data-ttu-id="326e3-219">Bu bölümde tamamlamak için önce bir dış kimlik doğrulama sağlayıcısı etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="326e3-219">To complete this section, you must first enable an external authentication provider.</span></span> <span data-ttu-id="326e3-220">Bkz: [Facebook, Google ve dış sağlayıcı kimlik doğrulaması](xref:security/authentication/social/index).</span><span class="sxs-lookup"><span data-stu-id="326e3-220">See [Facebook, Google, and external provider authentication](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="326e3-221">Yerel hem de sosyal hesaplar, e-posta bağlantısına tıklayarak birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-221">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="326e3-222">Aşağıdaki sırayla "RickAndMSFT@gmail.com" ilk olarak bir yerel oturum açın; oluşturulur ancak, bir sosyal oturum açma ilk hesap oluşturun, sonra bir yerel oturum açma ekleme.</span><span class="sxs-lookup"><span data-stu-id="326e3-222">In the following sequence, "RickAndMSFT@gmail.com" is first created as a local login; however, you can create the account as a social login first, then add a local login.</span></span>

![Web uygulaması: RickAndMSFT@gmail.com kimliği doğrulanmış kullanıcı](accconfirm/_static/rick.png)

<span data-ttu-id="326e3-224">Tıklayarak **Yönet** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="326e3-224">Click on the **Manage** link.</span></span> <span data-ttu-id="326e3-225">Bu hesapla ilişkili 0 dış (sosyal oturum açma bilgileri) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="326e3-225">Note the 0 external (social logins) associated with this account.</span></span>

![Görünümü yönetme](accconfirm/_static/manage.png)

<span data-ttu-id="326e3-227">Başka bir oturum açma hizmeti bağlantısını tıklayın ve uygulama isteklerini kabul etmek.</span><span class="sxs-lookup"><span data-stu-id="326e3-227">Click the link to another login service and accept the app requests.</span></span> <span data-ttu-id="326e3-228">Aşağıdaki görüntüde, Facebook Dış kimlik doğrulama sağlayıcısı'dır:</span><span class="sxs-lookup"><span data-stu-id="326e3-228">In the following image, Facebook is the external authentication provider:</span></span>

![Facebook listeleme görünümünüzü harici oturum açmaları yönetme](accconfirm/_static/fb.png)

<span data-ttu-id="326e3-230">İki hesap birleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="326e3-230">The two accounts have been combined.</span></span> <span data-ttu-id="326e3-231">Her iki hesabıyla oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="326e3-231">You are able to sign in with either account.</span></span> <span data-ttu-id="326e3-232">Kullanıcılarınızın kendi sosyal oturum açma kimlik doğrulama hizmeti çalışmıyor veya bunlar sosyal hesaplarına erişim daha büyük bir olasılıkla kaybettiğinizde durumunda yerel hesaplar eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326e3-232">You might want your users to add local accounts in case their social login authentication service is down, or more likely they've lost access to their social account.</span></span>

## <a name="enable-account-confirmation-after-a-site-has-users"></a><span data-ttu-id="326e3-233">Kullanıcılar bir siteye sahip olduktan sonra hesap onaylama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="326e3-233">Enable account confirmation after a site has users</span></span>

<span data-ttu-id="326e3-234">Var olan tüm kullanıcıları etkinleştirme hesap onaylama sitesinde kullanıcılarla kilitler.</span><span class="sxs-lookup"><span data-stu-id="326e3-234">Enabling account confirmation on a site with users locks out all the existing users.</span></span> <span data-ttu-id="326e3-235">Varolan kullanıcı hesaplarını onaylanan değildir çünkü kilitlidir.</span><span class="sxs-lookup"><span data-stu-id="326e3-235">Existing users are locked out because their accounts aren't confirmed.</span></span> <span data-ttu-id="326e3-236">Mevcut kullanıcı kilitlemesinin geçici olarak çözmek için aşağıdaki yaklaşımlardan birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="326e3-236">To work around existing user lockout, use one of the following approaches:</span></span>

* <span data-ttu-id="326e3-237">Tüm mevcut kullanıcılar onaylanıp olarak işaretlemek için veritabanı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="326e3-237">Update the database to mark all existing users as being confirmed.</span></span>
* <span data-ttu-id="326e3-238">Mevcut kullanıcıları onaylayın.</span><span class="sxs-lookup"><span data-stu-id="326e3-238">Confirm existing users.</span></span> <span data-ttu-id="326e3-239">Örneğin, batch onay bağlantılarının ile e-posta gönderme.</span><span class="sxs-lookup"><span data-stu-id="326e3-239">For example, batch-send emails with confirmation links.</span></span>

::: moniker-end
