---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: Model (VB) ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, Microsoft Visual Web Developer 2010 Express Service Pack, 1, kullanarak bir ASP.NET MVC Web uygulaması oluşturmaya yönelik temel bilgiler sağlanır...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: c2ec1f4cf8f68a426fa4cabfc36c5e7bf928fe32
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130061"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="b0013-103">Model Ekleme (VB)</span><span class="sxs-lookup"><span data-stu-id="b0013-103">Adding a Model (VB)</span></span>

<span data-ttu-id="b0013-104">Tarafından [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="b0013-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="b0013-105">Bu öğreticide, Microsoft Visual Web Developer 2010 Express Service Pack ücretsiz bir Microsoft Visual Studio sürümü olan 1, kullanarak bir ASP.NET MVC Web uygulaması oluşturmaya yönelik temel bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b0013-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="b0013-106">Başlamadan önce aşağıda listelenen ön yüklediğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="b0013-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="b0013-107">Aşağıdaki bağlantıya tıklayarak bunların tümünü yükleyebilirsiniz: [Web Platformu yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="b0013-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="b0013-108">Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0013-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="b0013-109">Visual Studio Web Developer Express SP1 önkoşulları</span><span class="sxs-lookup"><span data-stu-id="b0013-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="b0013-110">ASP.NET MVC 3 araçları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b0013-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="b0013-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçları desteği)</span><span class="sxs-lookup"><span data-stu-id="b0013-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="b0013-112">Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıyı tıklatarak önkoşulları yükleyin: [Visual Studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="b0013-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="b0013-113">Bu konuya eşlik etmek üzere bir Visual Web Developer proje VB.NET kaynak koduyla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0013-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="b0013-114">[VB.NET Eki](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="b0013-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="b0013-115">C# tercih ederseniz, geçiş [C# sürümü](../cs/adding-a-model.md) Bu öğreticinin.</span><span class="sxs-lookup"><span data-stu-id="b0013-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="b0013-116">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="b0013-116">Adding a Model</span></span>

<span data-ttu-id="b0013-117">Bu bölümde, bir veritabanında filmler yönetmek için bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b0013-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="b0013-118">Bu sınıf, ASP.NET MVC uygulamasını "modeli" parçası olacak.</span><span class="sxs-lookup"><span data-stu-id="b0013-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="b0013-119">Entity Framework bilinen bir .NET Framework Veri erişim teknolojisi tanımlayın ve bu model sınıfları ile çalışmak için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b0013-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="b0013-120">Geliştirme paradigma adlı Entity Framework (genellikle EF adlandırılır) destekler *Code First*.</span><span class="sxs-lookup"><span data-stu-id="b0013-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="b0013-121">Kod ilk basit sınıfları yazarak model nesneleri oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0013-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="b0013-122">(Bunlar da POCO sınıflardan "düz eski CLR nesnesi." verilir) Ardından, bir çok temiz ve hızlı geliştirme iş akışını sağlayan çalışma sırasında sınıflardan oluşturduğunuz veritabanına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b0013-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="b0013-123">Model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="b0013-123">Adding Model Classes</span></span>

<span data-ttu-id="b0013-124">İçinde **Çözüm Gezgini**, sağ tıklayın *modelleri* klasörüne **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="b0013-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="b0013-125">"Film" sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="b0013-125">Name the class "Movie".</span></span>

<span data-ttu-id="b0013-126">Aşağıdaki beş özelliği Ekle `Movie` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b0013-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="b0013-127">Kullanacağız `Movie` filmler veritabanındaki temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="b0013-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="b0013-128">Her bir örneği bir `Movie` nesne karşılık gelen bir veritabanı tablosu ve her bir özellik içinde bir satıra `Movie` sınıfı tablosunda bir sütun eşleme.</span><span class="sxs-lookup"><span data-stu-id="b0013-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="b0013-129">Aynı dosyada, aşağıdaki ekleyin `MovieDBContext` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b0013-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="b0013-130">`MovieDBContext` Sınıfı temsil eder, alma, depolama ve güncelleştirme işleme Entity Framework film veritabanı bağlamı `Movie` sınıfı bir veritabanında örnekleri.</span><span class="sxs-lookup"><span data-stu-id="b0013-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="b0013-131">`MovieDBContext` Türetildiği `DbContext` temel Entity Framework tarafından sağlanan sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b0013-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="b0013-132">Hakkında daha fazla bilgi için `DbContext` ve `DbSet`, bkz: [Entity Framework için üretkenlik geliştirmeleri](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="b0013-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="b0013-133">Başvuru yapabilmek için `DbContext` ve `DbSet`, aşağıdaki eklemeniz `imports` deyimini dosyanın üst:</span><span class="sxs-lookup"><span data-stu-id="b0013-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="b0013-134">Tam *Movie.vb* dosya aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b0013-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="b0013-135">Bağlantı dizesi oluşturma ve SQL Server Compact ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b0013-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="b0013-136">`MovieDBContext` Sınıfı, oluşturduğunuz veritabanına bağlanma ve eşleme görevi işler `Movie` veritabanı kayıtlarını nesneleri.</span><span class="sxs-lookup"><span data-stu-id="b0013-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="b0013-137">Bir soru sorabilirsiniz. ancak, listede bağlantı kurulacak veritabanını belirtmek şeklidir.</span><span class="sxs-lookup"><span data-stu-id="b0013-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="b0013-138">Bu bağlantı bilgilerini ekleyerek gerçekleştirirsiniz *Web.config* uygulamanın dosya.</span><span class="sxs-lookup"><span data-stu-id="b0013-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="b0013-139">Uygulama kökü açın *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="b0013-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="b0013-140">(Değil *Web.config* dosyası *görünümleri* klasör.) Aşağıdaki görüntüde göstermek hem de *Web.config* dosyaları; açık *Web.config* dosya kırmızı daire içinde.</span><span class="sxs-lookup"><span data-stu-id="b0013-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="b0013-141">Aşağıdaki bağlantı dizesi Ekle `<connectionStrings>` öğesinde *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="b0013-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="b0013-142">Aşağıdaki örnek bir bölümü gösterilmektedir *Web.config* dosyasıyla eklenen yeni bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="b0013-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="b0013-143">Bu küçük kod ve XML temsil eder ve film verileri bir veritabanında saklamak için yazmanız gereken her şeyi miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="b0013-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="b0013-144">Ardından, yeni bir oluşturacaksınız `MoviesController` film verileri görüntülemek ve kullanıcıların yeni film listeleri oluşturmak için kullanabileceğiniz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b0013-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0013-145">[Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="b0013-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
