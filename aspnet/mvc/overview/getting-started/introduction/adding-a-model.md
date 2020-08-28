---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Model ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045123"
---
# <a name="adding-a-model"></a><span data-ttu-id="d6df4-102">Model Ekleme</span><span class="sxs-lookup"><span data-stu-id="d6df4-102">Adding a Model</span></span>

<span data-ttu-id="d6df4-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="d6df4-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="d6df4-104">Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d6df4-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="d6df4-105">Bu sınıflar, &quot; &quot; ASP.NET MVC uygulamasının model parçası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d6df4-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="d6df4-106">Bu model sınıflarını tanımlamak ve bunlarla çalışmak için [Entity Framework](https://docs.microsoft.com/ef/) olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d6df4-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="d6df4-107">Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d6df4-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="d6df4-108">Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6df4-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="d6df4-109">(Bunlar ayrıca, düz eski CLR nesnelerinden POCO sınıfları olarak da bilinir &quot; . &quot; ) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6df4-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="d6df4-110">Önce veritabanını oluşturmanız gerekiyorsa, MVC ve EF uygulama geliştirme hakkında bilgi edinmek için bu öğreticiyi izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6df4-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="d6df4-111">Daha sonra veritabanı ilk yaklaşımını kapsayan Tom Fizmakens [ASP.net Scafkatlama](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) öğreticisini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6df4-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="d6df4-112">Model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="d6df4-112">Adding Model Classes</span></span>

<span data-ttu-id="d6df4-113">**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d6df4-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="d6df4-114">Film *sınıfı* adını girin &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="d6df4-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="d6df4-115">Sınıfına aşağıdaki beş özelliği ekleyin `Movie` :</span><span class="sxs-lookup"><span data-stu-id="d6df4-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="d6df4-116">`Movie`Bir veritabanındaki filmleri göstermek için sınıfını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d6df4-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="d6df4-117">Bir nesnenin her örneği `Movie` , bir veritabanı tablosundaki bir satıra karşılık gelir ve sınıfın her özelliği `Movie` tablodaki bir sütunla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d6df4-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="d6df4-118">Note: System. Data. Entity ve ilgili sınıfı kullanabilmek için [Entity Framework NuGet paketini](https://www.nuget.org/packages/EntityFramework/)yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6df4-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="d6df4-119">Daha fazla yönerge için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="d6df4-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="d6df4-120">Aynı dosyada, aşağıdaki `MovieDBContext` sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d6df4-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="d6df4-121">`MovieDBContext`Sınıfı, `Movie` bir veritabanında sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d6df4-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="d6df4-122">, `MovieDBContext` `DbContext` Entity Framework tarafından belirtilen temel sınıftan türetilir.</span><span class="sxs-lookup"><span data-stu-id="d6df4-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="d6df4-123">Ve ' nin başvurabilebilmesi için `DbContext` `DbSet` `using` dosyanın en üstüne aşağıdaki ifadeyi eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6df4-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="d6df4-124">Bunu, using ifadesini el ile ekleyerek yapabilir veya kırmızı dalgalı çizgilerin üzerine geldiğinizde `Show potential fixes` , ' ye tıklayıp `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="d6df4-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="d6df4-125">Note: birkaç kullanılmamış `using` deyim kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d6df4-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="d6df4-126">Visual Studio, kullanılmayan bağımlılıkları gri olarak gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="d6df4-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="d6df4-127">Kullanılmayan bağımlılıkları gri bağımlılıkların üzerine gelerek kaldırabilirsiniz ve kullanılmayan kullanımları Kaldır ' a tıklayın `Show potential fixes` **.**</span><span class="sxs-lookup"><span data-stu-id="d6df4-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="d6df4-128">Son olarak bir model ekledik (MVC 'de d).</span><span class="sxs-lookup"><span data-stu-id="d6df4-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="d6df4-129">Sonraki bölümde, veritabanı bağlantı dizesiyle çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d6df4-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d6df4-130">[Önceki](adding-a-view.md) 
>  [Sonraki](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="d6df4-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
