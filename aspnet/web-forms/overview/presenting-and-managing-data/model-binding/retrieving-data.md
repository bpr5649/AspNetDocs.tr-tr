---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Model bağlama ve Web formları ile verileri alma ve görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240745"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="71eb3-104">Model bağlama ve Web formları ile verileri alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="71eb3-105">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="71eb3-106">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="71eb3-107">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="71eb3-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="71eb3-108">Model bağlama modeli, herhangi bir veri erişim teknolojisi ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="71eb3-109">Bu öğreticide Entity Framework kullanacaksınız, ancak size en tanıdık veri erişim teknolojisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="71eb3-110">GridView, ListView, DetailsView veya FormView denetimi gibi bir veri bağlantılı sunucu denetiminden, veri seçme, güncelleştirme, silme ve oluşturma için kullanılacak yöntemlerin adlarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="71eb3-111">Bu öğreticide, SelectMethod için bir değer belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="71eb3-112">Bu yöntemde, verileri alma mantığını sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="71eb3-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="71eb3-113">Sonraki öğreticide, UpdateMethod, DeleteMethod ve InsertMethod değerlerini ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="71eb3-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="71eb3-114">C# veya Visual Basic tüm projeyi [indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=286116) .</span><span class="sxs-lookup"><span data-stu-id="71eb3-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="71eb3-115">İndirilebilir kod, Visual Studio 2012 ve üzeri sürümlerle birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="71eb3-116">Bu öğreticide gösterilen Visual Studio 2017 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="71eb3-117">Öğreticide, uygulamayı Visual Studio 'da çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="71eb3-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="71eb3-118">Ayrıca, uygulamayı bir barındırma sağlayıcısına dağıtabilir ve internet üzerinden kullanılabilir hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="71eb3-119">Microsoft, en fazla 10 Web sitesi için ücretsiz web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="71eb3-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="71eb3-120">[ücretsiz Azure deneme hesabı](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="71eb3-120">[free Azure trial account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="71eb3-121">Azure App Service Web Apps bir Visual Studio Web projesinin nasıl dağıtılacağı hakkında daha fazla bilgi için bkz. [Visual Studio Series kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="71eb3-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="71eb3-122">Bu öğretici Ayrıca, SQL Server veritabanınızı Azure SQL veritabanı 'na dağıtmak için Entity Framework Code First Migrations nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="71eb3-123">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="71eb3-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="71eb3-124">Microsoft Visual Studio 2017 veya Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="71eb3-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="71eb3-125">Bu öğretici Visual Studio 2012 ve Visual Studio 2013 ile de birlikte çalışarak, Kullanıcı arabirimi ve proje şablonunda bazı farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="71eb3-126">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="71eb3-126">What you'll build</span></span>

<span data-ttu-id="71eb3-127">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="71eb3-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="71eb3-128">Kurslara kayıtlı olan öğrencilerle bir University 'i yansıtan veri nesneleri oluşturun</span><span class="sxs-lookup"><span data-stu-id="71eb3-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="71eb3-129">Nesnelerden veritabanı tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="71eb3-129">Build database tables from the objects</span></span>
* <span data-ttu-id="71eb3-130">Veritabanını test verileriyle doldur</span><span class="sxs-lookup"><span data-stu-id="71eb3-130">Populate the database with test data</span></span>
* <span data-ttu-id="71eb3-131">Verileri bir Web formunda görüntüleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="71eb3-132">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="71eb3-132">Create the project</span></span>

1. <span data-ttu-id="71eb3-133">Visual Studio 2017 ' de, **Contosoüniversıtymodelbinding**adlı bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71eb3-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![proje oluştur](retrieving-data/_static/image19.png)

2. <span data-ttu-id="71eb3-135">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-135">Select **OK**.</span></span> <span data-ttu-id="71eb3-136">Bir şablon seçmek için iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-136">The dialog box to select a template appears.</span></span>

   ![Web formları seçin](retrieving-data/_static/image3.png)

3. <span data-ttu-id="71eb3-138">**Web Forms** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="71eb3-139">Gerekirse, kimlik doğrulamasını **bireysel kullanıcı hesaplarıyla**değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="71eb3-140">Projeyi oluşturmak için **Tamam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="71eb3-141">Site görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="71eb3-141">Modify site appearance</span></span>

   <span data-ttu-id="71eb3-142">Site görünümünü özelleştirmek için birkaç değişiklik yapın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="71eb3-143">Site. Master dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="71eb3-144">Başlığı, **ASP.NET uygulamamın**değil **Contoso Üniversitesi** görüntülenecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="71eb3-145">Üst bilgi metnini **uygulama adından** **Contoso Üniversitesi**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="71eb3-146">Gezinti üst bilgisi bağlantılarını siteyle ilgili olanlarla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="71eb3-147">**Hakkında** ve **iletişim kurulacak** bağlantıları kaldırın ve bunun yerine oluşturacağınız bir **öğrenciler** sayfasına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="71eb3-148">Site. Master öğesini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="71eb3-149">Öğrenci verilerini göstermek için Web formu ekleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="71eb3-150">**Çözüm Gezgini**, projenize sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="71eb3-151">**Yeni öğe Ekle** iletişim kutusunda, **Ana sayfa şablonuyla Web formu** ' nu seçin ve bunu **öğrenciler. aspx**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![sayfa oluştur](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="71eb3-153">**Ekle**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="71eb3-154">Web formunun ana sayfasında, **site. Master**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="71eb3-155">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="71eb3-156">Veri modelini ekleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-156">Add the data model</span></span>

<span data-ttu-id="71eb3-157">**Modeller** klasöründe, **UniversityModels.cs**adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="71eb3-158">**Modeller**' e sağ tıklayın, **Ekle**' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="71eb3-159">**Yeni Öğe Ekle** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="71eb3-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="71eb3-160">Sol gezinti menüsünde, **kod**' u ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![model sınıfı oluştur](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="71eb3-162">Sınıfı **UniversityModels.cs** olarak adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="71eb3-163">Bu dosyada,,, `SchoolContext` `Student` `Enrollment` ve `Course` sınıflarını aşağıdaki gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="71eb3-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="71eb3-164">`SchoolContext`Sınıfı, `DbContext` veritabanı bağlantısını ve verilerdeki değişiklikleri yöneten öğesinden türetilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="71eb3-165">Sınıfında,, `Student` ve özelliklerine uygulanan özniteliklere dikkat edin `FirstName` `LastName` `Year` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="71eb3-166">Bu öğretici, veri doğrulama için bu öznitelikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="71eb3-167">Kodu basitleştirmek için, yalnızca bu özellikler veri doğrulama öznitelikleriyle işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="71eb3-168">Gerçek bir projede, doğrulama gerektiren tüm özelliklere doğrulama öznitelikleri uygularsınız.</span><span class="sxs-lookup"><span data-stu-id="71eb3-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="71eb3-169">UniversityModels.cs Kaydet.</span><span class="sxs-lookup"><span data-stu-id="71eb3-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="71eb3-170">Sınıfları temel alarak veritabanını ayarlama</span><span class="sxs-lookup"><span data-stu-id="71eb3-170">Set up the database based on classes</span></span>

<span data-ttu-id="71eb3-171">Bu öğretici, nesne ve veritabanı tabloları oluşturmak için [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="71eb3-172">Bu tablolar, öğrenciler ve kurslarıyla ilgili bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="71eb3-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="71eb3-173">**Araçlar**  >  **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="71eb3-174">**Paket Yöneticisi konsolu**'nda şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="71eb3-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="71eb3-175">Komut başarıyla tamamlanırsa, geçişleri belirten bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![geçişleri etkinleştir](retrieving-data/_static/image8.png)

      <span data-ttu-id="71eb3-177">*Configuration.cs* adlı bir dosyanın oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="71eb3-178">`Configuration`Sınıfı bir yöntemine sahiptir `Seed` ve bu, veritabanı tablolarını test verileriyle önceden doldurabilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="71eb3-179">Veritabanını önceden doldur</span><span class="sxs-lookup"><span data-stu-id="71eb3-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="71eb3-180">Configuration.cs 'i açın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="71eb3-181">`Seed` yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="71eb3-182">Ayrıca, `using` ad alanı için bir ifade ekleyin `ContosoUniversityModelBinding. Models` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="71eb3-183">Configuration.cs Kaydet.</span><span class="sxs-lookup"><span data-stu-id="71eb3-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="71eb3-184">Paket Yöneticisi konsolunda, **ilk komut ekle-geçiş**' i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="71eb3-185">**Update-Database**komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="71eb3-186">Bu komutu çalıştırırken bir özel durum alırsanız, `StudentID` ve `CourseID` değerleri `Seed` Yöntem değerlerinden farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="71eb3-187">Bu veritabanı tablolarını açın ve ve için varolan değerleri `StudentID` bulun `CourseID` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="71eb3-188">Bu değerleri tablo için sağlama koduna ekleyin `Enrollments` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="71eb3-189">GridView denetimi ekleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-189">Add a GridView control</span></span>

<span data-ttu-id="71eb3-190">Doldurulmuş veritabanı verileriyle, artık bu verileri almaya ve görüntülemeye hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="71eb3-191">Öğrenciler. aspx ' i açın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="71eb3-192">`MainContent`Yer tutucuyu bulun.</span><span class="sxs-lookup"><span data-stu-id="71eb3-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="71eb3-193">Bu yer tutucunun içinde, bu kodu içeren bir **GridView** denetimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="71eb3-194">Dikkat edilmesi gerekenler:</span><span class="sxs-lookup"><span data-stu-id="71eb3-194">Things to note:</span></span>
   * <span data-ttu-id="71eb3-195">GridView öğesinde özelliği için ayarlanan değere dikkat edin `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="71eb3-196">Bu değer, bir sonraki adımda oluşturduğunuz GridView verilerini almak için kullanılan yöntemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="71eb3-197">`ItemType`Özelliği `Student` daha önce oluşturulan sınıfa ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="71eb3-198">Bu ayar, İşaretlemede Sınıf özelliklerine başvurmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="71eb3-199">Örneğin, `Student` sınıfında adlı bir koleksiyon vardır `Enrollments` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="71eb3-200">`Item.Enrollments`Bu koleksiyonu almak için öğesini kullanabilir ve ardından her öğrencinin kayıtlı kredilerinin toplamını almak Için [LINQ sözdizimini](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="71eb3-201">Öğrenciler. aspx ' i kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71eb3-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="71eb3-202">Verileri almak için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="71eb3-202">Add code to retrieve data</span></span>

   <span data-ttu-id="71eb3-203">Öğrenciler. aspx arka plan kod dosyasında, değer için belirtilen yöntemi ekleyin `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="71eb3-204">Students.aspx.cs 'i açın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="71eb3-205">`using` `ContosoUniversityModelBinding. Models` Ve ad alanları için deyimler ekleyin `System.Data.Entity` .</span><span class="sxs-lookup"><span data-stu-id="71eb3-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="71eb3-206">Belirttiğiniz yöntemi ekleyin `SelectMethod` :</span><span class="sxs-lookup"><span data-stu-id="71eb3-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="71eb3-207">`Include`Yan tümce sorgu performansını geliştirir, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="71eb3-208">`Include`Yan tümcesi olmadan veriler, ilgili verilerin alındığı her seferinde veritabanına ayrı bir sorgu göndermeyi içeren [*yavaş yükleme*](https://en.wikipedia.org/wiki/Lazy_loading)kullanılarak alınır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="71eb3-209">`Include`Yan tümcesiyle, veriler *Eager yüklemesi*kullanılarak alınır, yani tek bir veritabanı sorgusu ilgili tüm verileri alır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="71eb3-210">İlgili veriler kullanılmıyorsa, daha fazla veri alındığından Eager yüklemesi daha az verimlidir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="71eb3-211">Ancak, bu durumda, her bir kayıt için ilgili veriler görüntülendiğinden, Eager yüklemesi size en iyi performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="71eb3-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="71eb3-212">İlgili verileri yüklerken performans konuları hakkında daha fazla bilgi için, [ASP.NET MVC uygulamasındaki Entity Framework Ile ilgili verileri okuma](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) bölümünde Ilgili **verileri geç, Eager ve açık yükleme** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="71eb3-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="71eb3-213">Varsayılan olarak, veriler anahtar olarak işaretlenen özelliğin değerlerine göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="71eb3-214">`OrderBy`Farklı bir sıralama değeri belirtmek için bir yan tümce ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="71eb3-215">Bu örnekte, `StudentID` sıralama için varsayılan özellik kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="71eb3-216">[Sıralama, sayfalama ve verileri filtreleme](sorting-paging-and-filtering-data.md) makalesinde, kullanıcı sıralama için bir sütun seçmek üzere etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="71eb3-217">Students.aspx.cs Kaydet.</span><span class="sxs-lookup"><span data-stu-id="71eb3-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="71eb3-218">Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="71eb3-218">Run your application</span></span> 

<span data-ttu-id="71eb3-219">Web uygulamanızı çalıştırın (**F5**) ve aşağıdakiler görüntülenen **öğrenciler** sayfasına gidin:</span><span class="sxs-lookup"><span data-stu-id="71eb3-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![verileri göster](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="71eb3-221">Model bağlama yöntemlerinin otomatik nesli</span><span class="sxs-lookup"><span data-stu-id="71eb3-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="71eb3-222">Bu öğretici serisi ile çalışırken öğreticiden projenize yalnızca kodu kopyalamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="71eb3-223">Ancak, bu yaklaşımın bir dezavantajı, Visual Studio tarafından model bağlama yöntemlerine yönelik kodu otomatik olarak oluşturmak için sunulan özelliği bilmeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="71eb3-224">Kendi projeleriniz üzerinde çalışırken, otomatik kod üretimi size zaman kazandırabilir ve bir işlemin nasıl uygulanacağını anladığınızda size yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="71eb3-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="71eb3-225">Bu bölümde otomatik kod oluşturma özelliği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="71eb3-226">Bu bölüm yalnızca bilgilendirme amaçlıdır ve projenizde uygulamanız gereken herhangi bir kod içermez.</span><span class="sxs-lookup"><span data-stu-id="71eb3-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="71eb3-227">`SelectMethod`Biçimlendirme kodundaki,, veya özellikleri için bir değer ayarlarken `UpdateMethod` `InsertMethod` `DeleteMethod` **Yeni Yöntem Oluştur** seçeneğini belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![Yöntem oluşturma](retrieving-data/_static/image18.png)

<span data-ttu-id="71eb3-229">Visual Studio, doğru imzayla kodda arka planda bir yöntem oluşturmaz, ancak işlemi gerçekleştirmek için uygulama kodu da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71eb3-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="71eb3-230">İlk `ItemType` olarak özelliği otomatik kod oluşturma özelliğini kullanmadan önce ayarlarsanız, oluşturulan kod işlemler için bu türü kullanır.</span><span class="sxs-lookup"><span data-stu-id="71eb3-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="71eb3-231">Örneğin, `UpdateMethod` özelliği ayarlarken aşağıdaki kod otomatik olarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="71eb3-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="71eb3-232">Yine, bu kodun projenize eklenmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="71eb3-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="71eb3-233">Sonraki öğreticide, güncelleştirme, silme ve yeni veri ekleme yöntemlerini uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="71eb3-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="71eb3-234">Özet</span><span class="sxs-lookup"><span data-stu-id="71eb3-234">Summary</span></span>

<span data-ttu-id="71eb3-235">Bu öğreticide, veri modeli sınıfları oluşturdunuz ve bu sınıflardan bir veritabanı oluşturmuş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="71eb3-236">Veritabanı tablolarını test verileriyle doldurmuş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-236">You filled the database tables with test data.</span></span> <span data-ttu-id="71eb3-237">Veritabanından veri almak için model bağlama 'yı kullandınız ve sonra verileri bir GridView 'da görüntülen.</span><span class="sxs-lookup"><span data-stu-id="71eb3-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="71eb3-238">Bu serinin sonraki [öğreticide](updating-deleting-and-creating-data.md) , güncelleştirme, silme ve veri oluşturmayı etkinleştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="71eb3-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="71eb3-239">Sonraki</span><span class="sxs-lookup"><span data-stu-id="71eb3-239">Next</span></span>](updating-deleting-and-creating-data.md)
