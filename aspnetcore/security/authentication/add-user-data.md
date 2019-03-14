---
title: Ekleme, indirmek ve bir ASP.NET Core projesi kimliği için kullanıcı verilerini silme
author: rick-anderson
description: Bir ASP.NET Core projesi içinde kimlik için özel kullanıcı veri eklemeyi öğrenin. GDPR başına verileri silin.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 6/16/2018
ms.custom: seodec18
uid: security/authentication/add-user-data
ms.openlocfilehash: 5465117e5db880e8298e6c2075a27699e4081894
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075852"
---
# <a name="add-download-and-delete-custom-user-data-to-identity-in-an-aspnet-core-project"></a><span data-ttu-id="34ad0-104">Ekleme, indirmek ve kimlik için bir ASP.NET Core projesi özel kullanıcı verilerini silme</span><span class="sxs-lookup"><span data-stu-id="34ad0-104">Add, download, and delete custom user data to Identity in an ASP.NET Core project</span></span>

<span data-ttu-id="34ad0-105">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="34ad0-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="34ad0-106">Bu makale nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="34ad0-106">This article shows how to:</span></span>

* <span data-ttu-id="34ad0-107">ASP.NET Core web uygulaması için özel kullanıcı verilerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34ad0-107">Add custom user data to an ASP.NET Core web app.</span></span>
* <span data-ttu-id="34ad0-108">Özel kullanıcı veri modeli ile donatmak [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) indirme ve silme için otomatik olarak kullanılabilir olacak şekilde özniteliği.</span><span class="sxs-lookup"><span data-stu-id="34ad0-108">Decorate the custom user data model with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute so it's automatically available for download and deletion.</span></span> <span data-ttu-id="34ad0-109">Verileri silinir ve indirilen mümkün hale yardımcı karşılamak [GDPR](xref:security/gdpr) gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="34ad0-109">Making the data able to be downloaded and deleted helps meet [GDPR](xref:security/gdpr) requirements.</span></span>

<span data-ttu-id="34ad0-110">Bir Razor sayfaları web uygulaması proje örneği oluşturulur, ancak yönergeleri ASP.NET Core MVC web uygulaması için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="34ad0-110">The project sample is created from a Razor Pages web app, but the instructions are similar for a ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="34ad0-111">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="34ad0-111">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34ad0-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34ad0-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="34ad0-113">Razor web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="34ad0-113">Create a Razor web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="34ad0-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34ad0-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="34ad0-115">Visual Studio'dan **dosya** menüsünde **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-115">From the Visual Studio **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="34ad0-116">Projeyi adlandırın **WebApp1** için istiyorsanız ad alanı eşleşen [örneği indirin](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) kod.</span><span class="sxs-lookup"><span data-stu-id="34ad0-116">Name the project **WebApp1** if you want to it match the namespace of the [download sample](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) code.</span></span>
* <span data-ttu-id="34ad0-117">Seçin **ASP.NET Core Web uygulaması** > **Tamam**</span><span class="sxs-lookup"><span data-stu-id="34ad0-117">Select **ASP.NET Core Web Application** > **OK**</span></span>
* <span data-ttu-id="34ad0-118">Seçin **ASP.NET Core 2.1** açılır</span><span class="sxs-lookup"><span data-stu-id="34ad0-118">Select **ASP.NET Core 2.1** in the dropdown</span></span>
* <span data-ttu-id="34ad0-119">Seçin **Web uygulaması**  > **Tamam**</span><span class="sxs-lookup"><span data-stu-id="34ad0-119">Select **Web Application**  > **OK**</span></span>
* <span data-ttu-id="34ad0-120">Derleme ve projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34ad0-120">Build and run the project.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="34ad0-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="34ad0-121">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp -o WebApp1
```

---

## <a name="run-the-identity-scaffolder"></a><span data-ttu-id="34ad0-122">Kimlik iskele kurucu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="34ad0-122">Run the Identity scaffolder</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="34ad0-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34ad0-123">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="34ad0-124">Gelen **Çözüm Gezgini**, projeye sağ tıklayın > **Ekle** > **yeni iskele kurulmuş öğe**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-124">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="34ad0-125">Sol bölmeden **İskele Ekle** iletişim kutusunda **kimlik** > **ekleme**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-125">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="34ad0-126">İçinde **ADD kimliğini** iletişim kutusunda, aşağıdaki seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="34ad0-126">In the **ADD Identity** dialog, the following options:</span></span>
  * <span data-ttu-id="34ad0-127">Varolan bir düzen dosyası seçin *~/Pages/Shared/_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="34ad0-127">Select the existing layout  file  *~/Pages/Shared/_Layout.cshtml*</span></span>
  * <span data-ttu-id="34ad0-128">Aşağıdaki dosyalar geçersiz kılmak için seçin:</span><span class="sxs-lookup"><span data-stu-id="34ad0-128">Select the following files to override:</span></span>
    * <span data-ttu-id="34ad0-129">**Hesabı/kaydı**</span><span class="sxs-lookup"><span data-stu-id="34ad0-129">**Account/Register**</span></span>
    * <span data-ttu-id="34ad0-130">**Hesabı/yönetmek/dizin**</span><span class="sxs-lookup"><span data-stu-id="34ad0-130">**Account/Manage/Index**</span></span>
  * <span data-ttu-id="34ad0-131">Seçin **+** yeni bir düğme **veri bağlamı sınıfının**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-131">Select the **+** button to create a new **Data context class**.</span></span> <span data-ttu-id="34ad0-132">Tür kabul et (**WebApp1.Models.WebApp1Context** proje adlandırılmışsa **WebApp1**).</span><span class="sxs-lookup"><span data-stu-id="34ad0-132">Accept the type (**WebApp1.Models.WebApp1Context** if the project is named **WebApp1**).</span></span>
  * <span data-ttu-id="34ad0-133">Seçin **+** yeni bir düğme **kullanıcı sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-133">Select the **+** button to create a new **User class**.</span></span> <span data-ttu-id="34ad0-134">Tür kabul et (**WebApp1User** proje adlandırılmışsa **WebApp1**) > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-134">Accept the type (**WebApp1User** if the project is named **WebApp1**) > **Add**.</span></span>
* <span data-ttu-id="34ad0-135">Seçin **ekleme**.</span><span class="sxs-lookup"><span data-stu-id="34ad0-135">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="34ad0-136">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="34ad0-136">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="34ad0-137">ASP.NET Core iskele kurucu daha önce yüklemediyseniz şimdi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="34ad0-137">If you have not previously installed the ASP.NET Core scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="34ad0-138">Paket başvurusu ekleme [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) proje (.csproj) dosyasına.</span><span class="sxs-lookup"><span data-stu-id="34ad0-138">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (.csproj) file.</span></span> <span data-ttu-id="34ad0-139">Proje dizininde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34ad0-139">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="34ad0-140">Kimlik destek seçeneklerini listelemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34ad0-140">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="34ad0-141">Proje klasöründe kimlik iskele kurucu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34ad0-141">In the project folder, run the Identity scaffolder:</span></span>

```cli
dotnet aspnet-codegenerator identity -u WebApp1User -fi Account.Register;Account.Manage.Index
```

-------------

<span data-ttu-id="34ad0-142">Verilen yönergeleri izleyin [düzeni geçişleri ve UseAuthentication](xref:security/authentication/scaffold-identity#efm) aşağıdaki adımları gerçekleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="34ad0-142">Follow the instruction in [Migrations, UseAuthentication, and layout](xref:security/authentication/scaffold-identity#efm) to perform the following steps:</span></span>

* <span data-ttu-id="34ad0-143">Bir geçiş oluşturmak ve veritabanı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="34ad0-143">Create a migration and update the database.</span></span>
* <span data-ttu-id="34ad0-144">Add `UseAuthentication` to `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="34ad0-144">Add `UseAuthentication` to `Startup.Configure`.</span></span>
* <span data-ttu-id="34ad0-145">Ekleme `<partial name="_LoginPartial" />` Düzen dosyası için.</span><span class="sxs-lookup"><span data-stu-id="34ad0-145">Add `<partial name="_LoginPartial" />` to the layout file.</span></span>
* <span data-ttu-id="34ad0-146">Uygulamayı test edin:</span><span class="sxs-lookup"><span data-stu-id="34ad0-146">Test the app:</span></span>
  * <span data-ttu-id="34ad0-147">Bir kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="34ad0-147">Register a user</span></span>
  * <span data-ttu-id="34ad0-148">Yeni kullanıcı adını seçin (yanındaki **oturum kapatma** bağlantı).</span><span class="sxs-lookup"><span data-stu-id="34ad0-148">Select the new user name (next to the **Logout** link).</span></span> <span data-ttu-id="34ad0-149">Penceresini genişletin veya kullanıcı adı ve diğer bağlantıları göstermek için gezinti çubuğu simgesini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="34ad0-149">You might need to expand the window or select the navigation bar icon to show the user name and other links.</span></span>
  * <span data-ttu-id="34ad0-150">Seçin **kişisel verileri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="34ad0-150">Select the **Personal Data** tab.</span></span>
  * <span data-ttu-id="34ad0-151">Seçin **indirme** düğmesine tıklayın ve denetlenen *PersonalData.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="34ad0-151">Select the **Download** button and examined the *PersonalData.json* file.</span></span>
  * <span data-ttu-id="34ad0-152">Test **Sil** düğmesi, oturum açmış kullanıcıyı siler.</span><span class="sxs-lookup"><span data-stu-id="34ad0-152">Test the **Delete** button, which deletes the logged on user.</span></span>

## <a name="add-custom-user-data-to-the-identity-db"></a><span data-ttu-id="34ad0-153">Özel kullanıcı verilerini kimlik Veritabanına Ekle</span><span class="sxs-lookup"><span data-stu-id="34ad0-153">Add custom user data to the Identity DB</span></span>

<span data-ttu-id="34ad0-154">Güncelleştirme `IdentityUser` türetilmiş sınıf özel özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="34ad0-154">Update the `IdentityUser` derived class with custom properties.</span></span> <span data-ttu-id="34ad0-155">' % S'proje WebApp1 adlı, dosyanın nasıl adlandırıldığı *Areas/Identity/Data/WebApp1User.cs*.</span><span class="sxs-lookup"><span data-stu-id="34ad0-155">If you named the project WebApp1, the file is named *Areas/Identity/Data/WebApp1User.cs*.</span></span> <span data-ttu-id="34ad0-156">Dosya, aşağıdaki kod ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34ad0-156">Update the file with the following code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Data/WebApp1User.cs)]

<span data-ttu-id="34ad0-157">Düzenlenmiş özellikler ile [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) öznitelik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34ad0-157">Properties decorated with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute are:</span></span>

* <span data-ttu-id="34ad0-158">Ne zaman silinmiş *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor sayfası çağırır `UserManager.Delete`.</span><span class="sxs-lookup"><span data-stu-id="34ad0-158">Deleted when the *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor Page calls `UserManager.Delete`.</span></span>
* <span data-ttu-id="34ad0-159">Tarafından yüklenen veriler dahil *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor sayfası.</span><span class="sxs-lookup"><span data-stu-id="34ad0-159">Included in the downloaded data by the *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor Page.</span></span>

### <a name="update-the-accountmanageindexcshtml-page"></a><span data-ttu-id="34ad0-160">Account/Manage/Index.cshtml sayfası</span><span class="sxs-lookup"><span data-stu-id="34ad0-160">Update the Account/Manage/Index.cshtml page</span></span>

<span data-ttu-id="34ad0-161">Güncelleştirme `InputModel` içinde *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* aşağıdaki vurgulanmış kodu:</span><span class="sxs-lookup"><span data-stu-id="34ad0-161">Update the `InputModel` in *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml.cs?name=snippet&highlight=28-36,63-64,87-95,120)]

<span data-ttu-id="34ad0-162">Güncelleştirme *Areas/Identity/Pages/Account/Manage/Index.cshtml* aşağıdaki vurgulanmış biçimlendirmeye sahip:</span><span class="sxs-lookup"><span data-stu-id="34ad0-162">Update the *Areas/Identity/Pages/Account/Manage/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml?highlight=34-41)]

### <a name="update-the-accountregistercshtml-page"></a><span data-ttu-id="34ad0-163">Account/Register.cshtml sayfası</span><span class="sxs-lookup"><span data-stu-id="34ad0-163">Update the Account/Register.cshtml page</span></span>

<span data-ttu-id="34ad0-164">Güncelleştirme `InputModel` içinde *Areas/Identity/Pages/Account/Register.cshtml.cs* aşağıdaki vurgulanmış kodu:</span><span class="sxs-lookup"><span data-stu-id="34ad0-164">Update the `InputModel` in *Areas/Identity/Pages/Account/Register.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=8-16,43,44)]

<span data-ttu-id="34ad0-165">Güncelleştirme *Areas/Identity/Pages/Account/Register.cshtml* aşağıdaki vurgulanmış biçimlendirmeye sahip:</span><span class="sxs-lookup"><span data-stu-id="34ad0-165">Update the *Areas/Identity/Pages/Account/Register.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml?highlight=16-25)]

<span data-ttu-id="34ad0-166">Projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34ad0-166">Build the project.</span></span>

### <a name="add-a-migration-for-the-custom-user-data"></a><span data-ttu-id="34ad0-167">Özel kullanıcı verileri için bir geçiş ekleyin</span><span class="sxs-lookup"><span data-stu-id="34ad0-167">Add a migration for the custom user data</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="34ad0-168">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34ad0-168">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="34ad0-169">Visual Studio **Paket Yöneticisi Konsolu**:</span><span class="sxs-lookup"><span data-stu-id="34ad0-169">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CustomUserData
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="34ad0-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="34ad0-170">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CustomUserData
dotnet ef database update
```

------

## <a name="test-create-view-download-delete-custom-user-data"></a><span data-ttu-id="34ad0-171">Test oluşturun, görüntüleyin, indirin, özel kullanıcı verilerini sil</span><span class="sxs-lookup"><span data-stu-id="34ad0-171">Test create, view, download, delete custom user data</span></span>

<span data-ttu-id="34ad0-172">Uygulamayı test edin:</span><span class="sxs-lookup"><span data-stu-id="34ad0-172">Test the app:</span></span>

* <span data-ttu-id="34ad0-173">Yeni bir kullanıcı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34ad0-173">Register a new user.</span></span>
* <span data-ttu-id="34ad0-174">Özel kullanıcı veri görünümünde `/Identity/Account/Manage` sayfası.</span><span class="sxs-lookup"><span data-stu-id="34ad0-174">View the custom user data on the `/Identity/Account/Manage` page.</span></span>
* <span data-ttu-id="34ad0-175">İndirme ve görüntüleme kullanıcıların kişisel verilerden `/Identity/Account/Manage/PersonalData` sayfası.</span><span class="sxs-lookup"><span data-stu-id="34ad0-175">Download and view the users personal data from the `/Identity/Account/Manage/PersonalData` page.</span></span>
