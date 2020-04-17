---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Jilet ve Göze batmaz JavaScript ile MVC 3 Uygulaması Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Kullanıcı Listesi örnek web uygulaması, Razor görünüm motorlarını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar basit olduğunu gösterir. Örnek uygulama s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542462"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="9ee56-104">Razor ve Unobtrusive JavaScript ile MVC 3 Uygulaması Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ee56-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="9ee56-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="9ee56-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9ee56-106">Kullanıcı Listesi örnek web uygulaması, Razor görünüm motorlarını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar basit olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="9ee56-107">Örnek uygulama, kullanıcıları oluşturma, görüntüleme, düzenleme ve silme gibi işlevleri içeren kurgusal bir Kullanıcı Listesi web sitesi oluşturmak için ASP.NET MVC sürüm 3 ve Visual Studio 2010 ile yeni Razor görünüm altyapısının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="9ee56-108">Bu öğretici, MVC 3 uygulaması ASP.NET Kullanıcı Listesi örneğini oluşturmak için atılan adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="9ee56-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="9ee56-109">C# ve VB kaynak koduna sahip bir Visual Studio projesi bu konuya eşlik etmek için kullanılabilir: [İndir](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="9ee56-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="9ee56-110">Bu öğretici hakkında sorularınız varsa, [MVC foruma](https://forums.asp.net/1146.aspx)gönderin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="9ee56-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9ee56-111">Overview</span></span>

<span data-ttu-id="9ee56-112">İnşa edeceğimiz uygulama basit bir kullanıcı listesi web sitesidir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="9ee56-113">Kullanıcılar kullanıcı bilgilerini girebilir, görüntüleyebilir ve güncelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-113">Users can enter, view, and update user information.</span></span>

![Örnek site](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="9ee56-115">VB ve C# tamamlanan projeyi [buradan](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="9ee56-116">Web Uygulamasını Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ee56-116">Creating the Web Application</span></span>

<span data-ttu-id="9ee56-117">Öğreticiyi başlatmak için Visual Studio 2010'u açın ve *mvc 3 Web Uygulaması* şablonu ASP.NET kullanarak yeni bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ee56-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="9ee56-118">Uygulama &quot;Mvc3Razor&quot;adı .</span><span class="sxs-lookup"><span data-stu-id="9ee56-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="9ee56-119">[![Yeni MVC 3 projesi](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="9ee56-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="9ee56-120">Yeni **ASP.NET MVC 3 Project** iletişim kutusunda, **Internet Application'ı**seçin, Razor görünüm altyapısını seçin ve ardından **Tamam'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Yeni ASP.NET MVC 3 Proje iletişim kutusu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="9ee56-122">Bu eğitimde ASP.NET üyelik sağlayıcısını kullanmaydığınız için oturum açma ve üyelikle ilişkili tüm dosyaları silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="9ee56-123">**Çözüm Gezgini'nde,** aşağıdaki dosyaları ve dizinleri kaldırın:</span><span class="sxs-lookup"><span data-stu-id="9ee56-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="9ee56-124">*Denetleyiciler\Hesap Kontrolörü*</span><span class="sxs-lookup"><span data-stu-id="9ee56-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="9ee56-125">*Modeller\Hesap Modelleri*</span><span class="sxs-lookup"><span data-stu-id="9ee56-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="9ee56-126">*Görünümler\Paylaşılan\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="9ee56-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="9ee56-127">*Görünümler\Hesap* (ve bu dizindeki tüm dosyalar)</span><span class="sxs-lookup"><span data-stu-id="9ee56-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="9ee56-129"><em> \_Layout.cshtml</em> dosyasını düzenle ve giriş `<div>` devre `logindisplay` dışı&quot;bırakılan <em>&quot;</em>ileti ile adlandırılmış öğenin içindeki biçimlendirmeyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="9ee56-130">Aşağıdaki örnekte yeni biçimlendirme gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="9ee56-131">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="9ee56-131">Adding the Model</span></span>

<span data-ttu-id="9ee56-132">**Çözüm Gezgini'nde,** *Modeller* klasörüne sağ tıklayın, **Ekle'yi**seçin ve ardından **Sınıf'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Yeni Kullanıcı Mdl sınıfı](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="9ee56-134">Sınıfı `UserModel`adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-134">Name the class `UserModel`.</span></span> <span data-ttu-id="9ee56-135">*UserModel* dosyasının içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="9ee56-136">Sınıf `UserModel` kullanıcıları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9ee56-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="9ee56-137">Sınıfın her [üyesi, DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanından [Gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelik ile açıklamalı.</span><span class="sxs-lookup"><span data-stu-id="9ee56-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="9ee56-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki öznitelikler, web uygulamaları için otomatik istemci ve sunucu tarafı doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ee56-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="9ee56-139">Sınıfı `HomeController` açın ve `using` sınıflara `UserModel` erişebilmeniz `Users` için bir yönerge ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="9ee56-140">Bildirimden `HomeController` hemen sonra, aşağıdaki yorumu ve `Users` bir sınıfa başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="9ee56-141">Sınıf, `Users` bu öğreticide kullanacağınız basitleştirilmiş, bellek içi veri deposudur.</span><span class="sxs-lookup"><span data-stu-id="9ee56-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="9ee56-142">Gerçek bir uygulamada, kullanıcı bilgilerini depolamak için bir veritabanı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9ee56-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="9ee56-143">Dosyanın `HomeController` ilk birkaç satırı aşağıdaki örnekte gösterilir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="9ee56-144">Uygulamayı, kullanıcı modelinin bir sonraki adımda iskele sihirbazı tarafından kullanılabileceğini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ee56-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="9ee56-145">Varsayılan Görünümü Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ee56-145">Creating the Default View</span></span>

<span data-ttu-id="9ee56-146">Bir sonraki adım, kullanıcıları görüntülemek için bir eylem yöntemi ve görünüm eklemektir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="9ee56-147">Varolan *Görünümler\Ana Sayfa\Dizin* dosyasını silin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="9ee56-148">Kullanıcıları görüntülemek için yeni bir *Dizin* dosyası oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="9ee56-149">`HomeController` Sınıfta, `Index` yöntemin içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="9ee56-150">Yöntemin `Index` içine sağ tıklayın ve ardından **Görünüm Ekle'yi**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="9ee56-152">Güçlü **bir şekilde yazılmış görünüm** oluştur seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="9ee56-153">**Veri sınıfı görüntüle**için **Mvc3Razor.Models.UserModel'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="9ee56-154">(Veri **sınıfı görünümü** kutusunda **Mvc3Razor.Models.UserModel'i** görmüyorsanız, projeyi oluşturmanız gerekir.) Görünüm motorunun **Razor**olarak ayarlandıklarına emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ee56-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="9ee56-155">İçeriği **Listeye** **Göre'ye** Ayarla ve Ardından **Ekle'yi**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-155">Set **View content** to **List** and then click **Add**.</span></span>

![Dizin Görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="9ee56-157">Yeni görünüm, `Index` görünüme geçirilen kullanıcı verilerini otomatik olarak kalıba biçer.</span><span class="sxs-lookup"><span data-stu-id="9ee56-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="9ee56-158">Yeni oluşturulan *Görünümler\Ana Sayfa\Dizin* dosyasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="9ee56-159">**Yeni Oluştur**, **Düzenle,** **Ayrıntıları**düzenle ve **sil** bağlantıları çalışmıyor, ancak sayfanın geri kalanı işlevsel.</span><span class="sxs-lookup"><span data-stu-id="9ee56-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="9ee56-160">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-160">Run the page.</span></span> <span data-ttu-id="9ee56-161">Kullanıcıların listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-161">You see a list of users.</span></span>

![Dizin Sayfası](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="9ee56-163">*Index.cshtml* dosyasını açın `ActionLink` ve **Düzenle**, **Ayrıntılar**ve **Sil** için biçimlendirmeyi aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="9ee56-164">Kullanıcı adı, **Düzenle**, **Ayrıntılar**ve **Sil** bağlantılarında seçili kaydı bulmak için kimlik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ee56-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="9ee56-165">Ayrıntıları Görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9ee56-165">Creating the Details View</span></span>

<span data-ttu-id="9ee56-166">Bir sonraki adım, `Details` kullanıcı ayrıntılarını görüntülemek için bir eylem yöntemi ve görünüm eklemektir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="9ee56-168">Ev denetleyicisine aşağıdaki `Details` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="9ee56-169">Yöntemin `Details` içine sağ tıklayın ve ardından <strong>Görünüm Ekle'yi</strong>seçin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="9ee56-170"><strong>Veri sınıfı görüntükutusunun</strong> <strong>Mvc3Razor.Models.UserModel</strong>içerdiğini<em>doğrulayın.</em></span><span class="sxs-lookup"><span data-stu-id="9ee56-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="9ee56-171">İçeriği <strong>Ayrıntılara</strong> <strong>Göre Ayarla</strong> ve <strong>Ardından Ekle'yi</strong>tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Ayrıntıları görünüm ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="9ee56-173">Uygulamayı çalıştırın ve ayrıntılar bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-173">Run the application and select a details link.</span></span> <span data-ttu-id="9ee56-174">Otomatik iskele modeldeki her özelliği gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-174">The automatic scaffolding shows each property in the model.</span></span>

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="9ee56-176">Görünüm Edit Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ee56-176">Creating the Edit View</span></span>

<span data-ttu-id="9ee56-177">Ev denetleyicisine aşağıdaki `Edit` yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="9ee56-178">Önceki adımlardaki gibi bir görünüm ekleyin, ancak **Görünümü** **Edit'e**ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="9ee56-180">Uygulamayı çalıştırın ve kullanıcılardan birinin adını ve soyadını edin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="9ee56-181">Sınıfa uygulanan `DataAnnotation` kısıtlamaları ihlal ederseniz, formu gönderdiğiniz zaman sunucu kodu tarafından üretilen doğrulama hatalarını görürsünüz. `UserModel`</span><span class="sxs-lookup"><span data-stu-id="9ee56-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="9ee56-182">Örneğin, formu gönderdiğiniz zaman &quot;ilk&quot; &quot;ad&quot;Ann'i A ile değiştirirseniz, formda aşağıdaki hata görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="9ee56-183">Bu öğreticide, kullanıcı adını birincil anahtar olarak ele alıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="9ee56-184">Bu nedenle, kullanıcı adı özelliği değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9ee56-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="9ee56-185">*Edit.cshtml* dosyasında, deyimden `Html.BeginForm` hemen sonra, kullanıcı adını gizli bir alan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="9ee56-186">Bu, özelliğin modelde geçirilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="9ee56-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="9ee56-187">Aşağıdaki kod parçası deyimin `Hidden` yerleşimini gösterir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="9ee56-188">Kullanıcı `TextBoxFor` adı `ValidationMessageFor` için işaretleme ve işaretlemeyi bir `DisplayFor` çağrıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="9ee56-189">Yöntem, `DisplayFor` özelliği salt okunur öğe olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9ee56-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="9ee56-190">Aşağıdaki örnek, tamamlanan biçimlendirmeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-190">The following example shows the completed markup.</span></span> <span data-ttu-id="9ee56-191">Orijinal `TextBoxFor` ve `ValidationMessageFor` aramalar Razor başlangıç-yorum ve son yorum karakterleri`@* *@`ile yorumlanır ( )</span><span class="sxs-lookup"><span data-stu-id="9ee56-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="9ee56-192">İstemci Tarafı Doğrulamayı Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9ee56-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="9ee56-193">mvc 3 ASP.NET'te istemci tarafı doğrulamayı etkinleştirmek için iki bayrak ayarlamanız ve üç JavaScript dosyası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="9ee56-194">Uygulamanın *Web.config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="9ee56-195">`that ClientValidationEnabled` Doğrulayın `UnobtrusiveJavaScriptEnabled` ve uygulama ayarlarında doğru ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9ee56-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="9ee56-196">Root *Web.config* dosyasından aşağıdaki parça doğru ayarları gösterir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="9ee56-197">Doğru `UnobtrusiveJavaScriptEnabled` ayar, göze batmaz Ajax ve göze batmaz istemci doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ee56-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="9ee56-198">Göze çarpmadan doğrulama kullandığınızda, doğrulama kuralları HTML5 özniteliklerine dönüştürülr.</span><span class="sxs-lookup"><span data-stu-id="9ee56-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="9ee56-199">HTML5 öznitelik adları yalnızca küçük harflerden, sayılardan ve tirelerden oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="9ee56-200">Doğru `ClientValidationEnabled` ayar istemci tarafı doğrulamasağlar.</span><span class="sxs-lookup"><span data-stu-id="9ee56-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="9ee56-201">Bu anahtarları uygulama *Web.config* dosyasında ayarlayarak, tüm uygulama için istemci doğrulamasını ve göze batmaz JavaScript'i etkinleştirmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="9ee56-202">Ayrıca, aşağıdaki kodu kullanarak bu ayarları tek tek görünümlerde veya denetleyici yöntemlerinde etkinleştirebilir veya devre dışı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ee56-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="9ee56-203">Ayrıca, işlenen görünüme birkaç JavaScript dosyası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="9ee56-204">JavaScript'i tüm görünümlere eklemenin kolay bir yolu, bunları *Görünümler\Paylaşılan\\_Layout.cshtml* dosyasına eklemektir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="9ee56-205">Layout.cshtml dosyasının `<head>` öğesini aşağıdaki kodla değiştirin: \* \_\*</span><span class="sxs-lookup"><span data-stu-id="9ee56-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="9ee56-206">İlk iki jQuery komut dosyası Microsoft Ajax İçerik Dağıtım Ağı (CDN) tarafından barındırılır.</span><span class="sxs-lookup"><span data-stu-id="9ee56-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="9ee56-207">Microsoft Ajax CDN'den yararlanarak, uygulamalarınızın ilk hit performansını önemli ölçüde artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="9ee56-208">Uygulamayı çalıştırın ve bir edit bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-208">Run the application and click an edit link.</span></span> <span data-ttu-id="9ee56-209">Sayfanın kaynağını tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-209">View the page's source in the browser.</span></span> <span data-ttu-id="9ee56-210">Tarayıcı kaynağı formun `data-val` birçok özniteliklerini gösterir (veri doğrulama için).</span><span class="sxs-lookup"><span data-stu-id="9ee56-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="9ee56-211">İstemci doğrulama ve göze batmayan JavaScript etkinleştirildiğinde, istemci doğrulama kuralına `data-val="true"` sahip giriş alanları, göze batmayan istemci doğrulaması tetiklemek için öznitelik içerir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="9ee56-212">Örneğin, modeldeki `City` alan [Gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelik ile dekore edilmiştir ve bu da aşağıdaki örnekte gösterilen HTML ile sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="9ee56-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="9ee56-213">Her istemci doğrulama kuralı için, formu `data-val-rulename="message"`olan bir öznitelik eklenir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="9ee56-214">Daha `City` önce gösterilen alan örneğini kullanarak, gerekli istemci `data-val-required` doğrulama kuralı &quot;özniteliği oluşturur&quot;ve Şehir alanının gerekli olduğu ileti.</span><span class="sxs-lookup"><span data-stu-id="9ee56-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="9ee56-215">Uygulamayı çalıştırın, kullanıcılardan birini edin `City` ve alanı temizleyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="9ee56-216">Alanın dışına çıktığınızda, istemci tarafı doğrulama hatası iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ee56-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Şehir gerekli](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="9ee56-218">Benzer şekilde, istemci doğrulama kuralındaki her parametre için, formu `data-val-rulename-paramname=paramvalue`olan bir öznitelik eklenir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="9ee56-219">Örneğin, `FirstName` özellik [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliği ile açıklamalı ve en az 3 uzunluk ve 8 maksimum uzunluk belirtir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="9ee56-220">Adlı `length` veri doğrulama kuralı parametre `max` adı ve parametre değeri 8 vardır.</span><span class="sxs-lookup"><span data-stu-id="9ee56-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="9ee56-221">Aşağıdaki, kullanıcılardan birini yaptığınızda `FirstName` alan için oluşturulan HTML'yi gösterir:</span><span class="sxs-lookup"><span data-stu-id="9ee56-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="9ee56-222">Göze batmaz istemci doğrulaması hakkında daha fazla bilgi için, Brad Wilson'ın blogunda [ASP.NET MVC 3'teki Unobtrusive Müşteri Doğrulama](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) girişine bakın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="9ee56-223">MVC 3 BetaASP.NET bazen istemci tarafı doğrulamayı başlatmak için formu göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="9ee56-224">Bu son sürüm için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="9ee56-225">Görünüm Oluştur</span><span class="sxs-lookup"><span data-stu-id="9ee56-225">Creating the Create View</span></span>

<span data-ttu-id="9ee56-226">Bir sonraki adım, `Create` kullanıcının yeni bir kullanıcı oluşturmasını sağlamak için bir eylem yöntemi ve görünüm eklemektir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="9ee56-227">Ev denetleyicisine aşağıdaki `Create` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="9ee56-228">Önceki adımlardaki gibi bir görünüm ekleyin, ancak **Görünümü** **Oluştur'a**ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Görünüm Oluşturma](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="9ee56-230">Uygulamayı çalıştırın, **Oluştur** bağlantısını seçin ve yeni bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="9ee56-231">Yöntem `Create` otomatik olarak istemci tarafı ve sunucu tarafı doğrulama yararlanır.</span><span class="sxs-lookup"><span data-stu-id="9ee56-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="9ee56-232">Ben X &quot;&quot;gibi beyaz alan içeren bir kullanıcı adı girmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="9ee56-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="9ee56-233">Kullanıcı adı alanının dışına çıktığınızda, istemci tarafı doğrulama`White space is not allowed`hatası ( ) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9ee56-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="9ee56-234">Sil yöntemini ekle</span><span class="sxs-lookup"><span data-stu-id="9ee56-234">Add the Delete method</span></span>

<span data-ttu-id="9ee56-235">Öğreticiyi tamamlamak için ev `Delete` denetleyicisine aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ee56-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="9ee56-236">Önceki `Delete` adımlardaki gibi bir görünüm ekleyin, **Içeriği** **Sil'e**ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ee56-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Görünümü Sil](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="9ee56-238">Şimdi doğrulama ile basit ama tamamen işlevsel ASP.NET MVC 3 uygulama var.</span><span class="sxs-lookup"><span data-stu-id="9ee56-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
