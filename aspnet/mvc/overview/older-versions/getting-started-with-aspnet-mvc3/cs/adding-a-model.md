---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: Model (C#) ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Not: Bu öğreticide güncelleştirilmiş bir sürümünü burada ASP.NET MVC 5 ve Visual Studio 2013 kullanan kullanılabilir. Bu, daha güvenli ve izleyin ve tanıtım çok daha kolay...'
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 8cf8693b71509163860c78a87370c4765414fd5d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130343"
---
# <a name="adding-a-model-c"></a><span data-ttu-id="273e4-104">Model Ekleme (C#)</span><span class="sxs-lookup"><span data-stu-id="273e4-104">Adding a Model (C#)</span></span>

<span data-ttu-id="273e4-105">Tarafından [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="273e4-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="273e4-106">Bu öğreticide, Microsoft Visual Web Developer 2010 Express Service Pack ücretsiz bir Microsoft Visual Studio sürümü olan 1, kullanarak bir ASP.NET MVC Web uygulaması oluşturmaya yönelik temel bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="273e4-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="273e4-107">Başlamadan önce aşağıda listelenen ön yüklediğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="273e4-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="273e4-108">Aşağıdaki bağlantıya tıklayarak bunların tümünü yükleyebilirsiniz: [Web Platformu yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="273e4-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="273e4-109">Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="273e4-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="273e4-110">Visual Studio Web Developer Express SP1 önkoşulları</span><span class="sxs-lookup"><span data-stu-id="273e4-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="273e4-111">ASP.NET MVC 3 araçları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="273e4-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="273e4-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçları desteği)</span><span class="sxs-lookup"><span data-stu-id="273e4-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="273e4-113">Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıyı tıklatarak önkoşulları yükleyin: [Visual Studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="273e4-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="273e4-114">C# kaynak kodu içeren bir Visual Web Developer proje, bu konuya eşlik etmek üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="273e4-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="273e4-115">[C# sürümü indirme](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="273e4-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="273e4-116">Visual Basic tercih ederseniz, geçiş [Visual Basic sürümü](../vb/adding-a-model.md) Bu öğreticinin.</span><span class="sxs-lookup"><span data-stu-id="273e4-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="273e4-117">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="273e4-117">Adding a Model</span></span>

<span data-ttu-id="273e4-118">Bu bölümde, bir veritabanında filmler yönetmek için bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="273e4-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="273e4-119">Bu sınıf, ASP.NET MVC uygulamasını "modeli" parçası olacak.</span><span class="sxs-lookup"><span data-stu-id="273e4-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="273e4-120">Entity Framework bilinen bir .NET Framework Veri erişim teknolojisi tanımlayın ve bu model sınıfları ile çalışmak için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="273e4-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="273e4-121">Geliştirme paradigma adlı Entity Framework (genellikle EF adlandırılır) destekler *Code First*.</span><span class="sxs-lookup"><span data-stu-id="273e4-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="273e4-122">Kod ilk basit sınıfları yazarak model nesneleri oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="273e4-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="273e4-123">(Bunlar da POCO sınıflardan "düz eski CLR nesnesi." verilir) Ardından, bir çok temiz ve hızlı geliştirme iş akışını sağlayan çalışma sırasında sınıflardan oluşturduğunuz veritabanına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="273e4-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="273e4-124">Model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="273e4-124">Adding Model Classes</span></span>

<span data-ttu-id="273e4-125">İçinde **Çözüm Gezgini**, sağ tıklayın *modelleri* klasörüne **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="273e4-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="273e4-126">Adı *sınıfı* "Film".</span><span class="sxs-lookup"><span data-stu-id="273e4-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="273e4-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="273e4-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="273e4-128">Aşağıdaki beş özelliği Ekle `Movie` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="273e4-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="273e4-129">Kullanacağız `Movie` filmler veritabanındaki temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="273e4-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="273e4-130">Her bir örneği bir `Movie` nesne karşılık gelen bir veritabanı tablosu ve her bir özellik içinde bir satıra `Movie` sınıfı tablosunda bir sütun eşleme.</span><span class="sxs-lookup"><span data-stu-id="273e4-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="273e4-131">Aynı dosyada, aşağıdaki ekleyin `MovieDBContext` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="273e4-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="273e4-132">`MovieDBContext` Sınıfı temsil eder, alma, depolama ve güncelleştirme işleme Entity Framework film veritabanı bağlamı `Movie` sınıfı bir veritabanında örnekleri.</span><span class="sxs-lookup"><span data-stu-id="273e4-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="273e4-133">`MovieDBContext` Türetildiği `DbContext` temel Entity Framework tarafından sağlanan sınıfı.</span><span class="sxs-lookup"><span data-stu-id="273e4-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="273e4-134">Hakkında daha fazla bilgi için `DbContext` ve `DbSet`, bkz: [Entity Framework için üretkenlik geliştirmeleri](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="273e4-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="273e4-135">Başvuru yapabilmek için `DbContext` ve `DbSet`, aşağıdaki eklemeniz `using` deyimini dosyanın üst:</span><span class="sxs-lookup"><span data-stu-id="273e4-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="273e4-136">Tam *Movie.cs* dosya aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="273e4-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="273e4-137">Bağlantı dizesi oluşturma ve SQL Server Compact ile çalışma</span><span class="sxs-lookup"><span data-stu-id="273e4-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="273e4-138">`MovieDBContext` Sınıfı, oluşturduğunuz veritabanına bağlanma ve eşleme görevi işler `Movie` veritabanı kayıtlarını nesneleri.</span><span class="sxs-lookup"><span data-stu-id="273e4-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="273e4-139">Bir soru sorabilirsiniz. ancak, listede bağlantı kurulacak veritabanını belirtmek şeklidir.</span><span class="sxs-lookup"><span data-stu-id="273e4-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="273e4-140">Bu bağlantı bilgilerini ekleyerek gerçekleştirirsiniz *Web.config* uygulamanın dosya.</span><span class="sxs-lookup"><span data-stu-id="273e4-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="273e4-141">Uygulama kökü açın *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="273e4-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="273e4-142">(Değil *Web.config* dosyası *görünümleri* klasör.) Aşağıdaki görüntüde göstermek hem de *Web.config* dosyaları; açık *Web.config* dosya kırmızı daire içinde.</span><span class="sxs-lookup"><span data-stu-id="273e4-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

<span data-ttu-id="273e4-143">Aşağıdaki bağlantı dizesi Ekle `<connectionStrings>` öğesinde *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="273e4-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="273e4-144">Aşağıdaki örnek bir bölümü gösterilmektedir *Web.config* dosyasıyla eklenen yeni bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="273e4-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="273e4-145">Bu küçük kod ve XML temsil eder ve film verileri bir veritabanında saklamak için yazmanız gereken her şeyi miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="273e4-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="273e4-146">Ardından, yeni bir oluşturacaksınız `MoviesController` film verileri görüntülemek ve kullanıcıların yeni film listeleri oluşturmak için kullanabileceğiniz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="273e4-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="273e4-147">[Önceki](adding-a-view.md)
> [İleri](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="273e4-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
