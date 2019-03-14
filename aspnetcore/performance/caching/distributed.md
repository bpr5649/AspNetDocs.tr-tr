---
title: Dağıtılmış önbelleğe alma ASP.NET Core
author: guardrex
description: Uygulama performansı ve ölçeklenebilirlik, özellikle bir Bulutu vea sunucusu grubu ortamında artırmak için bir ASP.NET Core dağıtılmış önbellek kullanmayı öğrenin.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: performance/caching/distributed
ms.openlocfilehash: 7337ee3b823064c942832d8a44e4d4289bc4fd0e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074373"
---
# <a name="distributed-caching-in-aspnet-core"></a><span data-ttu-id="cbe94-103">Dağıtılmış önbelleğe alma ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cbe94-103">Distributed caching in ASP.NET Core</span></span>

<span data-ttu-id="cbe94-104">Tarafından [Steve Smith](https://ardalis.com/) ve [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="cbe94-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="cbe94-105">Dağıtılmış bir önbellek genellikle bir dış hizmete erişebilmesi uygulama sunucularına olarak tutulur, birden çok uygulama sunucular tarafından paylaşılan bir önbellektir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-105">A distributed cache is a cache shared by multiple app servers, typically maintained as an external service to the app servers that access it.</span></span> <span data-ttu-id="cbe94-106">Özellikle uygulama bir bulut hizmeti ya da bir sunucu grubu tarafından barındırıldığında dağıtılmış önbellek ASP.NET Core uygulaması, ölçeklenebilirliğini ve performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-106">A distributed cache can improve the performance and scalability of an ASP.NET Core app, especially when the app is hosted by a cloud service or a server farm.</span></span>

<span data-ttu-id="cbe94-107">Dağıtılmış önbellek tek tek uygulama sunucularında önbelleğe alınan verilerin depolandığı önbelleğe alma diğer senaryolar üzerinden çeşitli avantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-107">A distributed cache has several advantages over other caching scenarios where cached data is stored on individual app servers.</span></span>

<span data-ttu-id="cbe94-108">Önbelleğe alınan verilerin ne zaman dağıtılır, veri:</span><span class="sxs-lookup"><span data-stu-id="cbe94-108">When cached data is distributed, the data:</span></span>

* <span data-ttu-id="cbe94-109">Olan *tutarlı* istekleri birden çok sunucu arasında (tutarlı).</span><span class="sxs-lookup"><span data-stu-id="cbe94-109">Is *coherent* (consistent) across requests to multiple servers.</span></span>
* <span data-ttu-id="cbe94-110">Sunucu yeniden başlatıldıktan ve uygulama dağıtımlarını devam eder.</span><span class="sxs-lookup"><span data-stu-id="cbe94-110">Survives server restarts and app deployments.</span></span>
* <span data-ttu-id="cbe94-111">Yerel bellek kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="cbe94-111">Doesn't use local memory.</span></span>

<span data-ttu-id="cbe94-112">Dağıtılmış önbellek, uygulama belirli yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-112">Distributed cache configuration is implementation specific.</span></span> <span data-ttu-id="cbe94-113">Bu makalede, SQL Server yapılandırma ve dağıtılmış önbellek Redis açıklar.</span><span class="sxs-lookup"><span data-stu-id="cbe94-113">This article describes how to configure SQL Server and Redis distributed caches.</span></span> <span data-ttu-id="cbe94-114">Üçüncü taraf uygulamalarında kullanılabilir olduğu gibi aynı zamanda [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([github'da NCache](https://github.com/Alachisoft/NCache)).</span><span class="sxs-lookup"><span data-stu-id="cbe94-114">Third party implementations are also available, such as [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache)).</span></span> <span data-ttu-id="cbe94-115">Hangi uygulama bağımsız olarak işaretlenirse, uygulama önbellek kullanarak ile etkileşim <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> arabirimi.</span><span class="sxs-lookup"><span data-stu-id="cbe94-115">Regardless of which implementation is selected, the app interacts with the cache using the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface.</span></span>

<span data-ttu-id="cbe94-116">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="cbe94-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbe94-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cbe94-117">Prerequisites</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="cbe94-118">Bir SQL Server kullanmak için Dağıtılmış önbellek, başvuru [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) veya paket başvurusu ekleme [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-118">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="cbe94-119">Dağıtılmış önbellek, başvuru bir Redis kullanılacak [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) ve için bir paket başvurusu ekleme [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-119">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) package.</span></span> <span data-ttu-id="cbe94-120">Redis paket bulunup bulunmadığına `Microsoft.AspNetCore.App` paketlemek için Redis paket proje dosyanızda ayrı olarak başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-120">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="cbe94-121">Bir SQL Server kullanmak için Dağıtılmış önbellek, başvuru [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) veya paket başvurusu ekleme [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-121">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="cbe94-122">Dağıtılmış önbellek, başvuru bir Redis kullanılacak [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) ve için bir paket başvurusu ekleme [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-122">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="cbe94-123">Redis paket bulunup bulunmadığına `Microsoft.AspNetCore.App` paketlemek için Redis paket proje dosyanızda ayrı olarak başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-123">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="cbe94-124">Bir SQL Server kullanmak için Dağıtılmış önbellek, başvuru [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) veya paket başvurusu ekleme [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-124">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="cbe94-125">Dağıtılmış önbellek, başvuru bir Redis kullanılacak [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) veya paket başvurusu ekleme [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-125">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="cbe94-126">Redis paketinde `Microsoft.AspNetCore.All` paketini ayrı olarak proje dosyanızda Redis paket başvurusu yapmak zorunda kalmazsınız.</span><span class="sxs-lookup"><span data-stu-id="cbe94-126">The Redis package is included in `Microsoft.AspNetCore.All` package, so you don't need to reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="cbe94-127">Dağıtılmış önbellek bir SQL Server kullanmak için paket başvurusu ekleme [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-127">To use a SQL Server distributed cache, add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="cbe94-128">Dağıtılmış önbellek bir Redis kullanmak için paket başvurusu ekleme [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) paket.</span><span class="sxs-lookup"><span data-stu-id="cbe94-128">To use a Redis distributed cache, add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span>

::: moniker-end

## <a name="idistributedcache-interface"></a><span data-ttu-id="cbe94-129">IDistributedCache arabirimi</span><span class="sxs-lookup"><span data-stu-id="cbe94-129">IDistributedCache interface</span></span>

<span data-ttu-id="cbe94-130"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> Arabirimi dağıtılmış önbellek uygulamasında öğelerini işlemek için aşağıdaki yöntemleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="cbe94-130">The <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface provides the following methods to manipulate items in the distributed cache implementation:</span></span>

* <span data-ttu-id="cbe94-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Dize anahtarı kabul eder ve önbelleğe alınan öğe olarak alır. bir `byte[]` , dizi önbellekte bulundu.</span><span class="sxs-lookup"><span data-stu-id="cbe94-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Accepts a string key and retrieves a cached item as a `byte[]` array if found in the cache.</span></span>
* <span data-ttu-id="cbe94-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Bir öğe ekler (olarak `byte[]` array) için bir dize anahtarı kullanarak önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="cbe94-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Adds an item (as `byte[]` array) to the cache using a string key.</span></span>
* <span data-ttu-id="cbe94-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Önbelleğinde (varsa), kayan zaman aşımı sıfırlama kendi anahtarını temel alan bir öğeyi yeniler.</span><span class="sxs-lookup"><span data-stu-id="cbe94-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>
* <span data-ttu-id="cbe94-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Önbellek öğesinin temel dize anahtarıyla kaldırır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Removes a cache item based on its string key.</span></span>

## <a name="establish-distributed-caching-services"></a><span data-ttu-id="cbe94-135">Dağıtılmış önbelleğe alma hizmetleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbe94-135">Establish distributed caching services</span></span>

<span data-ttu-id="cbe94-136">Uygulaması kaydetme <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> içinde `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="cbe94-136">Register an implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="cbe94-137">Bu konuda açıklanan framework tarafından sağlanan uygulamaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cbe94-137">Framework-provided implementations described in this topic include:</span></span>

* [<span data-ttu-id="cbe94-138">Dağıtılmış önbellek</span><span class="sxs-lookup"><span data-stu-id="cbe94-138">Distributed Memory Cache</span></span>](#distributed-memory-cache)
* [<span data-ttu-id="cbe94-139">SQL Server dağıtılmış önbellek</span><span class="sxs-lookup"><span data-stu-id="cbe94-139">Distributed SQL Server cache</span></span>](#distributed-sql-server-cache)
* [<span data-ttu-id="cbe94-140">Dağıtılmış bir Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="cbe94-140">Distributed Redis cache</span></span>](#distributed-redis-cache)

### <a name="distributed-memory-cache"></a><span data-ttu-id="cbe94-141">Dağıtılmış önbellek</span><span class="sxs-lookup"><span data-stu-id="cbe94-141">Distributed Memory Cache</span></span>

<span data-ttu-id="cbe94-142">Dağıtılmış önbellek (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) bir framework tarafından sağlanan uygulamasıdır <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> , öğeleri bellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="cbe94-142">The Distributed Memory Cache (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) is a framework-provided implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> that stores items in memory.</span></span> <span data-ttu-id="cbe94-143">Dağıtılmış önbellek gerçek bir dağıtılmış önbellek değildir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-143">The Distributed Memory Cache isn't an actual distributed cache.</span></span> <span data-ttu-id="cbe94-144">Önbelleğe alınmış öğeleri, uygulamanın çalıştığı sunucu üzerinde uygulama örneği tarafından depolanır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-144">Cached items are stored by the app instance on the server where the app is running.</span></span>

<span data-ttu-id="cbe94-145">Dağıtılmış önbellek faydalı bir uygulamadır:</span><span class="sxs-lookup"><span data-stu-id="cbe94-145">The Distributed Memory Cache is a useful implementation:</span></span>

* <span data-ttu-id="cbe94-146">Geliştirme ve test senaryoları.</span><span class="sxs-lookup"><span data-stu-id="cbe94-146">In development and testing scenarios.</span></span>
* <span data-ttu-id="cbe94-147">Tek bir sunucu üretim ve bellek tüketimi kullanıldığında, bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-147">When a single server is used in production and memory consumption isn't an issue.</span></span> <span data-ttu-id="cbe94-148">Dağıtılmış önbellek özetleri uygulama, veri depolama önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="cbe94-148">Implementing the Distributed Memory Cache abstracts cached data storage.</span></span> <span data-ttu-id="cbe94-149">Birden çok düğüm veya hataya dayanıklılık gerekli hale ileride önbelleğe alma çözüme gerçek bir dağıtılmış uygulama için sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbe94-149">It allows for implementing a true distributed caching solution in the future if multiple nodes or fault tolerance become necessary.</span></span>

<span data-ttu-id="cbe94-150">Örnek uygulama, uygulama geliştirme ortamında çalıştırıldığında dağıtılmış bellek önbelleğini kullanma yapar:</span><span class="sxs-lookup"><span data-stu-id="cbe94-150">The sample app makes use of the Distributed Memory Cache when the app is run in the Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=5)]

### <a name="distributed-sql-server-cache"></a><span data-ttu-id="cbe94-151">Dağıtılmış SQL Sunucusu Önbelleği</span><span class="sxs-lookup"><span data-stu-id="cbe94-151">Distributed SQL Server Cache</span></span>

<span data-ttu-id="cbe94-152">Dağıtılmış SQL Server önbellek uygulaması (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>), yedekleme deposu bir SQL Server veritabanını kullanmak dağıtılmış bir önbellek sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbe94-152">The Distributed SQL Server Cache implementation (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>) allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="cbe94-153">Bir SQL Server örneğinde SQL Server önbelleğe alınan öğe tablo oluşturmak için kullanabileceğiniz `sql-cache` aracı.</span><span class="sxs-lookup"><span data-stu-id="cbe94-153">To create a SQL Server cached item table in a SQL Server instance, you can use the `sql-cache` tool.</span></span> <span data-ttu-id="cbe94-154">Aracı adı ve belirttiğiniz şema ile bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cbe94-154">The tool creates a table with the name and schema that you specify.</span></span>

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="cbe94-155">Ekleme `SqlConfig.Tools` için `<ItemGroup>` proje dosyası ve çalışma öğesi `dotnet restore`.</span><span class="sxs-lookup"><span data-stu-id="cbe94-155">Add `SqlConfig.Tools` to the `<ItemGroup>` element of the project file and run `dotnet restore`.</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.Extensions.Caching.SqlConfig.Tools"
                          Version="2.0.2" />
</ItemGroup>
```

::: moniker-end

<span data-ttu-id="cbe94-156">Çalıştırarak SQL Server'da bir tablo oluşturma `sql-cache create` komutu.</span><span class="sxs-lookup"><span data-stu-id="cbe94-156">Create a table in SQL Server by running the `sql-cache create` command.</span></span> <span data-ttu-id="cbe94-157">SQL Server örneği sağlayın (`Data Source`), veritabanı (`Initial Catalog`), şema (örneğin, `dbo`) ve tablo adı (örneğin, `TestCache`):</span><span class="sxs-lookup"><span data-stu-id="cbe94-157">Provide the SQL Server instance (`Data Source`), database (`Initial Catalog`), schema (for example, `dbo`), and table name (for example, `TestCache`):</span></span>

```console
dotnet sql-cache create "Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
```

<span data-ttu-id="cbe94-158">Aracı başarılı olduğunu belirten bir ileti kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="cbe94-158">A message is logged to indicate that the tool was successful:</span></span>

```console
Table and index were created successfully.
```

<span data-ttu-id="cbe94-159">Tarafından oluşturulan tabloyu `sql-cache` aracı aşağıdaki şemayı sahiptir:</span><span class="sxs-lookup"><span data-stu-id="cbe94-159">The table created by the `sql-cache` tool has the following schema:</span></span>

![SqlServer önbelleği tablosu](distributed/_static/SqlServerCacheTable.png)

> [!NOTE]
> <span data-ttu-id="cbe94-161">Bir uygulamanın bir örneğini kullanarak önbellek değerleri değiştirmelisiniz <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>değil bir <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span><span class="sxs-lookup"><span data-stu-id="cbe94-161">An app should manipulate cache values using an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>, not a <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span></span>

<span data-ttu-id="cbe94-162">Örnek uygulama uygular <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> olmayan geliştirme ortamında:</span><span class="sxs-lookup"><span data-stu-id="cbe94-162">The sample app implements <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> in a non-Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=9-15)]

> [!NOTE]
> <span data-ttu-id="cbe94-163">A <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (ve isteğe bağlı olarak <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> ve <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) dışında kaynak denetimine genellikle depolanır (örneğin, tarafından depolanan [gizli dizi Yöneticisi](xref:security/app-secrets) veya *appsettings.json* / *appsettings. {Ortamı} .json* dosyaları).</span><span class="sxs-lookup"><span data-stu-id="cbe94-163">A <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (and optionally, <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> and <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) are typically stored outside of source control (for example, stored by the [Secret Manager](xref:security/app-secrets) or in *appsettings.json*/*appsettings.{Environment}.json* files).</span></span> <span data-ttu-id="cbe94-164">Bağlantı dizesi, kaynak denetimi sistemlerini dışında tutulması gereken kimlik bilgileri içeriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-164">The connection string may contain credentials that should be kept out of source control systems.</span></span>

### <a name="distributed-redis-cache"></a><span data-ttu-id="cbe94-165">Dağıtılmış bir Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="cbe94-165">Distributed Redis Cache</span></span>

<span data-ttu-id="cbe94-166">[Redis](https://redis.io/) dağıtılmış bir önbellek sık kullanılan bir açık kaynak bellek içi veri deposu.</span><span class="sxs-lookup"><span data-stu-id="cbe94-166">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="cbe94-167">Yerel olarak Redis kullanın ve yapılandırabileceğiniz bir [Azure Redis Cache](https://azure.microsoft.com/services/cache/) Azure'da barındırılan ASP.NET Core uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="cbe94-167">You can use Redis locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for an Azure-hosted ASP.NET Core app.</span></span> <span data-ttu-id="cbe94-168">Önbellek uygulamasını kullanarak bir uygulamayı yapılandırır bir <xref:Microsoft.Extensions.Caching.Redis.RedisCache> örneği (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span><span class="sxs-lookup"><span data-stu-id="cbe94-168">An app configures the cache implementation using a <xref:Microsoft.Extensions.Caching.Redis.RedisCache> instance (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span></span>

```csharp
services.AddDistributedRedisCache(options =>
{
    options.Configuration = "localhost";
    options.InstanceName = "SampleInstance";
});
```

<span data-ttu-id="cbe94-169">Yerel makinenizde Redis yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="cbe94-169">To install Redis on your local machine:</span></span>

* <span data-ttu-id="cbe94-170">Yükleme [Chocolatey Redis paket](https://chocolatey.org/packages/redis-64/).</span><span class="sxs-lookup"><span data-stu-id="cbe94-170">Install the [Chocolatey Redis package](https://chocolatey.org/packages/redis-64/).</span></span>
* <span data-ttu-id="cbe94-171">Çalıştırma `redis-server` bir komut isteminden.</span><span class="sxs-lookup"><span data-stu-id="cbe94-171">Run `redis-server` from a command prompt.</span></span>

## <a name="use-the-distributed-cache"></a><span data-ttu-id="cbe94-172">Dağıtılmış önbellek kullanma</span><span class="sxs-lookup"><span data-stu-id="cbe94-172">Use the distributed cache</span></span>

<span data-ttu-id="cbe94-173">Kullanılacak <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> arabirim, örneği istek <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> uygulamadaki herhangi bir oluşturucudan.</span><span class="sxs-lookup"><span data-stu-id="cbe94-173">To use the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface, request an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> from any constructor in the app.</span></span> <span data-ttu-id="cbe94-174">Örneği tarafından sağlanan [bağımlılık ekleme (dı)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="cbe94-174">The instance is provided by [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span>

<span data-ttu-id="cbe94-175">Uygulama başlatıldığında <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> içine eklenen `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="cbe94-175">When the app starts, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is injected into `Startup.Configure`.</span></span> <span data-ttu-id="cbe94-176">Geçerli zamanı kullanarak önbelleğe alınmış <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (daha fazla bilgi için [Web ana bilgisayarı: IApplicationLifetime arabirimi](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span><span class="sxs-lookup"><span data-stu-id="cbe94-176">The current time is cached using <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (for more information, see [Web Host: IApplicationLifetime interface](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_Configure&highlight=10)]

<span data-ttu-id="cbe94-177">Örnek uygulamayı eklediği <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> içine `IndexModel` dizin sayfası tarafından kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="cbe94-177">The sample app injects <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> into the `IndexModel` for use by the Index page.</span></span>

<span data-ttu-id="cbe94-178">Dizin Sayfası yüklendiği her durumda, önbelleğe alınan kez önbellek denetlenir `OnGetAsync`.</span><span class="sxs-lookup"><span data-stu-id="cbe94-178">Each time the Index page is loaded, the cache is checked for the cached time in `OnGetAsync`.</span></span> <span data-ttu-id="cbe94-179">Önbelleğe alınan süresi dolmadığından zaman görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-179">If the cached time hasn't expired, the time is displayed.</span></span> <span data-ttu-id="cbe94-180">Önbelleğe alınan saati (Bu sayfayı yüklenen son saat) erişildi son daraltılmasından 20 saniye geçtikten sayfası görüntüler *önbelleğe alınmış süre doldu*.</span><span class="sxs-lookup"><span data-stu-id="cbe94-180">If 20 seconds have elapsed since the last time the cached time was accessed (the last time this page was loaded), the page displays *Cached Time Expired*.</span></span>

<span data-ttu-id="cbe94-181">Önbelleğe alınan zaman seçerek geçerli saate hemen güncelleştirmek **sıfırlama önbelleğe alınmış süresi** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cbe94-181">Immediately update the cached time to the current time by selecting the **Reset Cached Time** button.</span></span> <span data-ttu-id="cbe94-182">Düğme tetikleyicisi `OnPostResetCachedTime` işleyicisi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="cbe94-182">The button triggers the `OnPostResetCachedTime` handler method.</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Pages/Index.cshtml.cs?name=snippet_IndexModel&highlight=7,14-20,25-29)]

> [!NOTE]
> <span data-ttu-id="cbe94-183">Bir Tekliyi veya kapsamındaki ömrü boyunca kullanılacak gerek yoktur <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> örnekleri (en az yerleşik uygulamalar için).</span><span class="sxs-lookup"><span data-stu-id="cbe94-183">There's no need to use a Singleton or Scoped lifetime for <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instances (at least for the built-in implementations).</span></span>
>
> <span data-ttu-id="cbe94-184">Ayrıca oluşturabilirsiniz bir <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> DI kullanmak yerine gerekebilir, ancak kodda bir örnek oluşturma yapabilir, kodunuzu test etmek daha zor bağlanmayacaktır örnek ve ihlal [açık bağımlılıkları ilkesine](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span><span class="sxs-lookup"><span data-stu-id="cbe94-184">You can also create an <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instance wherever you might need one instead of using DI, but creating an instance in code can make your code harder to test and violates the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span></span>

## <a name="recommendations"></a><span data-ttu-id="cbe94-185">Öneriler</span><span class="sxs-lookup"><span data-stu-id="cbe94-185">Recommendations</span></span>

<span data-ttu-id="cbe94-186">Hangi uygulamasının verirken <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> uygulamanız için en iyisidir aşağıdakileri dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="cbe94-186">When deciding which implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is best for your app, consider the following:</span></span>

* <span data-ttu-id="cbe94-187">Var olan altyapı</span><span class="sxs-lookup"><span data-stu-id="cbe94-187">Existing infrastructure</span></span>
* <span data-ttu-id="cbe94-188">Performans gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="cbe94-188">Performance requirements</span></span>
* <span data-ttu-id="cbe94-189">Maliyet</span><span class="sxs-lookup"><span data-stu-id="cbe94-189">Cost</span></span>
* <span data-ttu-id="cbe94-190">Takım deneyimi</span><span class="sxs-lookup"><span data-stu-id="cbe94-190">Team experience</span></span>

<span data-ttu-id="cbe94-191">Önbelleğe alma çözümleri genellikle önbelleğe alınmış verileri hızlı alınmasını sağlamak için bellek içi depolama alanı kullanır, ancak bellektir sınırlı bir kaynağa ve masraflı genişletin.</span><span class="sxs-lookup"><span data-stu-id="cbe94-191">Caching solutions usually rely on in-memory storage to provide fast retrieval of cached data, but memory is a limited resource and costly to expand.</span></span> <span data-ttu-id="cbe94-192">Bir ön bellekte yaygın olarak kullanılan veri yalnızca depolama.</span><span class="sxs-lookup"><span data-stu-id="cbe94-192">Only store commonly used data in a cache.</span></span>

<span data-ttu-id="cbe94-193">Genellikle, Redis önbelleği, yüksek aktarım hızı ve SQL Server önbelleğe göre daha düşük gecikme süresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbe94-193">Generally, a Redis cache provides higher throughput and lower latency than a SQL Server cache.</span></span> <span data-ttu-id="cbe94-194">Ancak, değerlendirmesi önbelleğe alma stratejilerine performans özelliklerini belirlemek için genellikle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-194">However, benchmarking is usually required to determine the performance characteristics of caching strategies.</span></span>

<span data-ttu-id="cbe94-195">SQL Server dağıtılmış önbellek yedekleme deposu kullanıldığında, önbellek ve uygulamanın normal veri depolama için aynı veritabanını kullanın ve alma, her ikisi de performansı olumsuz yönde etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="cbe94-195">When SQL Server is used as a distributed cache backing store, use of the same database for the cache and the app's ordinary data storage and retrieval can negatively impact the performance of both.</span></span> <span data-ttu-id="cbe94-196">Dağıtılmış önbellek yedekleme deposu için adanmış bir SQL Server örneği kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="cbe94-196">We recommend using a dedicated SQL Server instance for the distributed cache backing store.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbe94-197">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cbe94-197">Additional resources</span></span>

* [<span data-ttu-id="cbe94-198">Redis Cache azure'da</span><span class="sxs-lookup"><span data-stu-id="cbe94-198">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="cbe94-199">Azure'da SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="cbe94-199">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* <span data-ttu-id="cbe94-200">[ASP.NET Core Web gruplarındaki NCache IDistributedCache sağlayıcısı](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([github'da NCache](https://github.com/Alachisoft/NCache))</span><span class="sxs-lookup"><span data-stu-id="cbe94-200">[ASP.NET Core IDistributedCache Provider for NCache in Web Farms](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache))</span></span>
* <xref:performance/caching/memory>
* <xref:fundamentals/change-tokens>
* <xref:performance/caching/response>
* <xref:performance/caching/middleware>
* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper>
* <xref:host-and-deploy/web-farm>
