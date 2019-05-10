---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Sahte Entity Framework, birim testi ASP.NET Web API 2 | Microsoft Docs
author: Rick-Anderson
description: Bu kılavuzu ve uygulama Entity Framework kullanan, Web API 2 uygulaması için birim testleri oluşturma işlemini göstermektedir. Nasıl değiştirileceğini gösterir...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108172"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="1d6e6-104">Sahte Entity Framework, birim testi ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="1d6e6-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="1d6e6-105">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1d6e6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="1d6e6-106">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="1d6e6-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="1d6e6-107">Bu kılavuzu ve uygulama Entity Framework kullanan, Web API 2 uygulaması için birim testleri oluşturma işlemini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="1d6e6-108">Bu, Entity Framework ile çalışma testi nesneleri oluşturma ve test etmek için bir bağlam nesnesi geçirerek etkinleştirmek için iskele kurulmuş denetleyicisini değiştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="1d6e6-109">Birim testi ile ASP.NET Web API'si için bir giriş için bkz [ASP.NET Web API 2 birim testiyle](unit-testing-with-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="1d6e6-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="1d6e6-110">Bu öğreticide, ASP.NET Web API ile ilgili temel kavramlar hakkında bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="1d6e6-111">Giriş niteliğindeki bir eğitim için bkz. [ASP.NET Web API 2 ile çalışmaya başlama](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="1d6e6-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1d6e6-112">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="1d6e6-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="1d6e6-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1d6e6-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="1d6e6-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="1d6e6-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="1d6e6-115">Bu konuda</span><span class="sxs-lookup"><span data-stu-id="1d6e6-115">In this topic</span></span>

<span data-ttu-id="1d6e6-116">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="1d6e6-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="1d6e6-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1d6e6-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="1d6e6-118">Kodu indir</span><span class="sxs-lookup"><span data-stu-id="1d6e6-118">Download code</span></span>](#download)
- [<span data-ttu-id="1d6e6-119">Uygulama ile birim testi projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="1d6e6-120">Model sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="1d6e6-121">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="1d6e6-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="1d6e6-122">Bağımlılık ekleme Ekle</span><span class="sxs-lookup"><span data-stu-id="1d6e6-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="1d6e6-123">Test projesinde NuGet paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="1d6e6-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="1d6e6-124">Bu testin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="1d6e6-125">Testleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="1d6e6-126">Testleri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1d6e6-126">Run tests</span></span>](#runtests)

<span data-ttu-id="1d6e6-127">' Ndaki adımları zaten tamamladıysanız [ASP.NET Web API 2 birim testiyle](unit-testing-with-aspnet-web-api.md), bölümüne atlayabilirsiniz [denetleyiciyi ekleme](#controller).</span><span class="sxs-lookup"><span data-stu-id="1d6e6-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="1d6e6-128">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1d6e6-128">Prerequisites</span></span>

<span data-ttu-id="1d6e6-129">Visual Studio 2017 Community, Professional veya Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="1d6e6-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="1d6e6-130">Kodu indir</span><span class="sxs-lookup"><span data-stu-id="1d6e6-130">Download code</span></span>

<span data-ttu-id="1d6e6-131">İndirme [projeyi](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span><span class="sxs-lookup"><span data-stu-id="1d6e6-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="1d6e6-132">Birim testi kodu ve için bu konunun indirilebilir proje içerir [birim testi ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) konu.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="1d6e6-133">Uygulama ile birim testi projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-133">Create application with unit test project</span></span>

<span data-ttu-id="1d6e6-134">Uygulamanızı oluştururken bir birim test projesi oluşturun veya mevcut bir uygulamaya bir birim test projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="1d6e6-135">Bu öğreticide, uygulama oluştururken bir birim testi projesi oluşturma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="1d6e6-136">Adlı yeni bir ASP.NET Web uygulaması oluşturma **StoreApp**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="1d6e6-137">Yeni ASP.NET projesi Windows'da seçin **boş** şablon klasörleri ekleyin ve Web API'si için başvuru çekirdek.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="1d6e6-138">Seçin **birim testleri ekleme** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="1d6e6-139">Birim test projesi otomatik olarak adlandırılır **StoreApp.Tests**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="1d6e6-140">Bu ad tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-140">You can keep this name.</span></span>

![Birim testi projesi oluşturma](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="1d6e6-142">Uygulamayı oluşturduktan sonra iki proje - içerdiği görürsünüz **StoreApp** ve **StoreApp.Tests**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="1d6e6-143">Model sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-143">Create the model class</span></span>

<span data-ttu-id="1d6e6-144">StoreApp projeniz için sınıf dosyası ekleyin **modelleri** adlı klasöre **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="1d6e6-145">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="1d6e6-146">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="1d6e6-147">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="1d6e6-147">Add the controller</span></span>

<span data-ttu-id="1d6e6-148">Denetleyicileri klasörüne sağ tıklayıp **Ekle** ve **yeni iskele kurulmuş öğe**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="1d6e6-149">Entity Framework kullanarak Eylemler ile Web API 2 denetleyicisi seçin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![Yeni denetleyici ekleyin](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="1d6e6-151">Aşağıdaki değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1d6e6-151">Set the following values:</span></span>

- <span data-ttu-id="1d6e6-152">Denetleyici adı: **ProductController**</span><span class="sxs-lookup"><span data-stu-id="1d6e6-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="1d6e6-153">Model sınıfı: **Ürün**</span><span class="sxs-lookup"><span data-stu-id="1d6e6-153">Model class: **Product**</span></span>
- <span data-ttu-id="1d6e6-154">Veri bağlamı sınıfı: [seçin **yeni veri bağlamı** aşağıda görüldüğü değerleri doldurur düğme]</span><span class="sxs-lookup"><span data-stu-id="1d6e6-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![Denetleyici belirtin](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="1d6e6-156">Tıklayın **Ekle** denetleyicisi otomatik olarak oluşturulan kod oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="1d6e6-157">Kod oluşturma, alma, güncelleştirme ve ürün sınıfının örneklerini silme yöntemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="1d6e6-158">Yöntemi aşağıdaki kodda gösterildiği bir ürün eklemek için.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="1d6e6-159">Yöntem örneği döndürdüğüne dikkat edin **Ihttpactionresult**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="1d6e6-160">Web API 2'deki yeni özelliklerin Ihttpactionresult biridir ve birim testi geliştirmenin kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="1d6e6-161">Sonraki bölümde kolaylaştırmak için oluşturulan kodu özelleştireceğim denetleyiciye test nesneleri geçirme.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="1d6e6-162">Bağımlılık ekleme Ekle</span><span class="sxs-lookup"><span data-stu-id="1d6e6-162">Add dependency injection</span></span>

<span data-ttu-id="1d6e6-163">Şu anda ProductController StoreAppContext sınıfının bir örneğini kullanmak için kodlanmış sınıftır.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="1d6e6-164">Uygulamanızı değiştirmeniz ve bu sabit kodlanmış bir bağımlılığı kaldırmak için bağımlılık ekleme adlı bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="1d6e6-165">Bu bağımlılık ayırarak, test ederken sahte bir nesne geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="1d6e6-166">Sağ **modelleri** klasöründe ve adlı yeni bir arabirim ekleme **IStoreAppContext**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="1d6e6-167">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="1d6e6-168">StoreAppContext.cs dosyasını açın ve aşağıdaki vurgulanmış değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="1d6e6-169">Dikkat edilecek önemli değişiklikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1d6e6-169">The important changes to note are:</span></span>

- <span data-ttu-id="1d6e6-170">StoreAppContext sınıfı IStoreAppContext arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="1d6e6-171">Uygulanan MarkAsModified yöntemi</span><span class="sxs-lookup"><span data-stu-id="1d6e6-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="1d6e6-172">ProductController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="1d6e6-173">Varolan kodu vurgulanmış kodu eşleşecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="1d6e6-174">Bu değişiklikler, bağımlılık StoreAppContext üzerinde kesme ve diğer sınıflar farklı bir nesne için bağlam sınıfını geçirmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="1d6e6-175">Bu değişiklik sırasında birim testleri bir test bağlamında geçirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="1d6e6-176">ProductController yapmanız gereken daha fazla değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="1d6e6-177">İçinde **PutProduct** yöntemi, varlık durumu ayarlar satır değiştiren MarkAsModified yöntemi çağrısı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="1d6e6-178">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-178">Build the solution.</span></span>

<span data-ttu-id="1d6e6-179">Şimdi test projesini ayarlarsınız hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="1d6e6-180">Test projesinde NuGet paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="1d6e6-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="1d6e6-181">Bir uygulama oluşturmak için boş şablonu kullandığınızda, birim testi projesi (StoreApp.Tests) yüklü herhangi bir NuGet paketinin içermez.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="1d6e6-182">Web API şablonu gibi diğer şablonları, birim test projesinde NuGet paketlerinden bazıları içerir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="1d6e6-183">Bu öğreticide, Entity Framework paketini ve Microsoft ASP.NET Web API 2 Çekirdek paketini test projesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="1d6e6-184">StoreApp.Tests projeye sağ tıklayıp **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="1d6e6-185">Paketler bu projeye eklemek için StoreApp.Tests proje seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![paketlerini yönetme](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="1d6e6-187">Çevrimiçi paketlerinden bulun ve EntityFramework paketi (sürüm 6.0 veya üzeri) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="1d6e6-188">EntityFramework paket zaten yüklü olduğunu görüntüleniyorsa, StoreApp.Tests proje yerine StoreApp proje seçmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![Entity Framework Ekle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="1d6e6-190">Bulun ve Microsoft ASP.NET Web API 2 Çekirdek paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![Web API çekirdek paketini yükle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="1d6e6-192">NuGet paketlerini Yönet penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="1d6e6-193">Bu testin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-193">Create test context</span></span>

<span data-ttu-id="1d6e6-194">Adlı bir sınıf ekleyin **TestDbSet** test projesi için.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="1d6e6-195">Bu sınıf, test veri kümeniz için temel sınıf olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="1d6e6-196">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="1d6e6-197">Adlı bir sınıf ekleyin **TestProductDbSet** aşağıdaki kodu içeren bir test projesi için.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="1d6e6-198">Adlı bir sınıf ekleyin **TestStoreAppContext** ve varolan kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="1d6e6-199">Testleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-199">Create tests</span></span>

<span data-ttu-id="1d6e6-200">Varsayılan olarak, adlı boş bir test dosyası test projenize içerir **UnitTest1.cs**.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="1d6e6-201">Bu dosya, test yöntemleri oluşturduğunuzda kullandığınız öznitelikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="1d6e6-202">Bu öğretici için yeni bir test sınıfı ekleyeceksiniz çünkü bu dosyayı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="1d6e6-203">Adlı bir sınıf ekleyin **TestProductController** test projesi için.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="1d6e6-204">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="1d6e6-205">Testleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1d6e6-205">Run tests</span></span>

<span data-ttu-id="1d6e6-206">Testleri çalıştırmak artık hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-206">You are now ready to run the tests.</span></span> <span data-ttu-id="1d6e6-207">Tüm ile işaretlenmiş yöntem **TestMethod** özniteliği test edilmiş.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="1d6e6-208">Gelen **Test** menü öğesi, testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-208">From the **Test** menu item, run the tests.</span></span>

![testleri çalıştırma](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="1d6e6-210">Açık **Test Gezgini** penceresinde ve test sonuçlarını dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1d6e6-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![test sonuçları](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
