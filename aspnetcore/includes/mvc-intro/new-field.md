---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069648"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="ba2da-101">Bir ASP.NET Core MVC uygulaması için yeni bir alan ekleyin</span><span class="sxs-lookup"><span data-stu-id="ba2da-101">Add a new field to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="ba2da-102">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ba2da-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ba2da-103">Bu öğretici için yeni bir alan ekleyeceksiniz `Movies` tablo.</span><span class="sxs-lookup"><span data-stu-id="ba2da-103">This tutorial will add a new field to the `Movies` table.</span></span> <span data-ttu-id="ba2da-104">Biz veritabanını bırakıp şema değiştirdiğimizde yeni bir tane oluşturun (yeni bir alan ekleyin).</span><span class="sxs-lookup"><span data-stu-id="ba2da-104">We'll drop the database and create a new one when we change the schema (add a new field).</span></span> <span data-ttu-id="ba2da-105">Biz perserve üretim veri olmadığında bu iş akışı geliştirme erken iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="ba2da-105">This workflow works well early in development when we don't have any production data to perserve.</span></span>

<span data-ttu-id="ba2da-106">Şema değiştirmeniz gerektiğinde perserve için ihtiyacınız olan verilere sahip olduğunuz ve uygulamanız dağıtıldıktan sonra veritabanı bırakılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ba2da-106">Once your app is deployed and you have data that you need to perserve, you can't drop your DB when you need to change the schema.</span></span> <span data-ttu-id="ba2da-107">Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) şemanızı güncelleştirin ve veri kaybı olmadan veritabanını geçirme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ba2da-107">Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) allows you to update your schema and migrate the database without losing data.</span></span> <span data-ttu-id="ba2da-108">Geçişleri bir özelliktir popüler birçok geçiş şema işlemleri SQL Server, ancak SQLlite kullanarak desteklemediğinde bu nedenle yalnızca çok basit geçişleri mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ba2da-108">Migrations is a popular feature when using SQL Server, but SQLlite doesn't support many migration schema operations, so only very simply migrations are possible.</span></span> <span data-ttu-id="ba2da-109">Bkz: [SQLite sınırlamaları](/ef/core/providers/sqlite/limitations) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ba2da-109">See [SQLite Limitations](/ef/core/providers/sqlite/limitations) for more information.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="ba2da-110">Film modeli derecelendirme özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="ba2da-110">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="ba2da-111">Açık *Models/Movie.cs* dosya ve ekleme bir `Rating` özelliği:</span><span class="sxs-lookup"><span data-stu-id="ba2da-111">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

<span data-ttu-id="ba2da-112">Yeni bir alan eklediğiniz çünkü `Movie` sınıfı da gereken bağlama beyaz liste bu yeni özellik dahil edilecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ba2da-112">Because you've added a new field to the `Movie` class, you also need to update the binding whitelist so this new property will be included.</span></span> <span data-ttu-id="ba2da-113">İçinde *MoviesController.cs*, güncelleştirme `[Bind]` özniteliği hem de `Create` ve `Edit` dahil etmek için eylem yöntemleri `Rating` özelliği:</span><span class="sxs-lookup"><span data-stu-id="ba2da-113">In *MoviesController.cs*, update the `[Bind]` attribute for both the `Create` and `Edit` action methods to include the `Rating` property:</span></span>

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

<span data-ttu-id="ba2da-114">Ayrıca görüntülemek için görüntüleme şablonları güncelleştirilecek oluşturabilecek ve yeni `Rating` Tarayıcı Görünümü özelliği.</span><span class="sxs-lookup"><span data-stu-id="ba2da-114">You also need to update the view templates in order to display, create, and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="ba2da-115">Düzen */Views/Movies/Index.cshtml* dosya ve ekleme bir `Rating` alan:</span><span class="sxs-lookup"><span data-stu-id="ba2da-115">Edit the */Views/Movies/Index.cshtml* file and add a `Rating` field:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

<span data-ttu-id="ba2da-116">Güncelleştirme */Views/Movies/Create.cshtml* ile bir `Rating` alan.</span><span class="sxs-lookup"><span data-stu-id="ba2da-116">Update the */Views/Movies/Create.cshtml* with a `Rating` field.</span></span>

<span data-ttu-id="ba2da-117">Uygulama, yeni alan eklemek için bir veritabanı güncelleştiriyoruz kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ba2da-117">The app won't work until we update the DB to include the new field.</span></span> <span data-ttu-id="ba2da-118">Şimdi çalıştırırsanız, aşağıdaki elde edecekleriniz `SqliteException`:</span><span class="sxs-lookup"><span data-stu-id="ba2da-118">If you run it now, you'll get the following `SqliteException`:</span></span>

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

<span data-ttu-id="ba2da-119">Güncelleştirilmiş film modeli sınıfı var olan veritabanının film tablonun şeması farklı olduğu için bu hatayı görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ba2da-119">You're seeing this error because the updated Movie model class is different than the schema of the Movie table of the existing database.</span></span> <span data-ttu-id="ba2da-120">(Yok hiçbir `Rating` veritabanı tablosundaki sütun.)</span><span class="sxs-lookup"><span data-stu-id="ba2da-120">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="ba2da-121">Hatayı çözümlemek için birkaç yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="ba2da-121">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="ba2da-122">Veritabanını bırakın ve yeni model sınıfı şemasını temel alan veritabanı otomatik olarak yeniden oluşturma Entity Framework sahip.</span><span class="sxs-lookup"><span data-stu-id="ba2da-122">Drop the database and have the Entity Framework automatically re-create the database based on the new model class schema.</span></span> <span data-ttu-id="ba2da-123">Bu yaklaşımda, veritabanında var olan veri kaybı — üretim veritabanıyla yapamadığı şekilde!</span><span class="sxs-lookup"><span data-stu-id="ba2da-123">With this approach, you lose existing data in the database — so you can't do this with a production database!</span></span> <span data-ttu-id="ba2da-124">Bir başlatıcı bir veritabanı test verileri ile otomatik olarak oluşturmak için genellikle bir uygulama geliştirmek için üretken bir şekilde kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="ba2da-124">Using an initializer to automatically seed a database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="ba2da-125">El ile model sınıfları eşleşecek şekilde var olan veritabanı şeması değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ba2da-125">Manually modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="ba2da-126">Bu yaklaşımın avantajı, verilerinizi korumak olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ba2da-126">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="ba2da-127">Bu değişikliği yapmak ya da el ile veya bir veritabanı oluşturma betiği değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ba2da-127">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="ba2da-128">Veritabanı şemasını güncelleştirmek için Code First Migrations'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba2da-128">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="ba2da-129">Bu öğreticide, biz bırakın ve şema değiştiğinde veritabanını yeniden oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="ba2da-129">For this tutorial, we'll drop and re-create the database when the schema changes.</span></span> <span data-ttu-id="ba2da-130">Bir terminal db bırakmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ba2da-130">Run the following command from a terminal to drop the db:</span></span>

`dotnet ef database drop`

<span data-ttu-id="ba2da-131">Güncelleştirme `SeedData` böylece yeni bir sütun için bir değer sağlar sınıfını.</span><span class="sxs-lookup"><span data-stu-id="ba2da-131">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="ba2da-132">Aşağıda bir örnek değişikliği gösterilmiştir, ancak her biri için bu değişikliği yapmak istersiniz `new Movie`.</span><span class="sxs-lookup"><span data-stu-id="ba2da-132">A sample change is shown below, but you'll want to make this change for each `new Movie`.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

<span data-ttu-id="ba2da-133">Ekleme `Rating` alanı `Edit`, `Details`, ve `Delete` görünümü.</span><span class="sxs-lookup"><span data-stu-id="ba2da-133">Add the `Rating` field to the `Edit`, `Details`, and `Delete` view.</span></span>

<span data-ttu-id="ba2da-134">Uygulamayı çalıştırın ve kontrol edebilirsiniz oluşturma/düzenleme/görüntüleme filmlerle bir `Rating` alan.</span><span class="sxs-lookup"><span data-stu-id="ba2da-134">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="ba2da-135">şablonları.</span><span class="sxs-lookup"><span data-stu-id="ba2da-135">templates.</span></span>
