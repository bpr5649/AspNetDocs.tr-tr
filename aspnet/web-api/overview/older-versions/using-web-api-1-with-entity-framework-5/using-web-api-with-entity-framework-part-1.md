---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'Bölüm 1: Genel bakış ve projeyi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0e4021402e8deccd2395f23b6b512679b5e9d281
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073809"
---
<a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="13db5-102">Bölüm 1: Genel Bakış ve Projeyi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="13db5-102">Part 1: Overview and Creating the Project</span></span>
====================
<span data-ttu-id="13db5-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="13db5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="13db5-104">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="13db5-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="13db5-105">Entity Framework, bir nesne/ilişkisel eşleme çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="13db5-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="13db5-106">Kodunuzda etki alanı nesnelerini ilişkisel bir veritabanındaki varlıkları eşlenir.</span><span class="sxs-lookup"><span data-stu-id="13db5-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="13db5-107">Çoğunlukla, Entity Framework bunu sizin için üstlenir çünkü veritabanı katmanı hakkında endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="13db5-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="13db5-108">Kodunuzu nesneleri yönetir ve bir veritabanına değişiklikleri kalıcı.</span><span class="sxs-lookup"><span data-stu-id="13db5-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="13db5-109">Öğretici</span><span class="sxs-lookup"><span data-stu-id="13db5-109">About the Tutorial</span></span>

<span data-ttu-id="13db5-110">Bu öğreticide, bir basit depolama uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="13db5-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="13db5-111">Uygulama için iki ana bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="13db5-111">There are two main parts to the application.</span></span> <span data-ttu-id="13db5-112">Normal kullanıcıların ürünleri görüntüleyip sipariş oluşturur:</span><span class="sxs-lookup"><span data-stu-id="13db5-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="13db5-113">Yöneticiler oluşturamaz, silemez veya ürünleri Düzenle:</span><span class="sxs-lookup"><span data-stu-id="13db5-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="13db5-114">Beceriler hakkında bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="13db5-114">Skills You'll Learn</span></span>

<span data-ttu-id="13db5-115">Öğrenecekleriniz aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="13db5-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="13db5-116">Entity Framework ile ASP.NET Web API kullanma</span><span class="sxs-lookup"><span data-stu-id="13db5-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="13db5-117">Knockout.js dinamik istemci kullanıcı Arabirimi oluşturmak için kullanma</span><span class="sxs-lookup"><span data-stu-id="13db5-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="13db5-118">Form kimlik doğrulaması, kullanıcıların kimliklerini doğrulamak için Web API'si ile kullanma</span><span class="sxs-lookup"><span data-stu-id="13db5-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="13db5-119">Bu öğreticiyi kendi içinde olsa da, aşağıdaki öğreticilerde ilk okumak isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13db5-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="13db5-120">İlk ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="13db5-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="13db5-121">CRUD işlemleri destekleyen bir Web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="13db5-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="13db5-122">Bazı bilgisine [ASP.NET MVC](../../../../mvc/index.md) da yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="13db5-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="13db5-123">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="13db5-123">Overview</span></span>

<span data-ttu-id="13db5-124">Yüksek düzeyde, uygulama mimarisinden şöyledir:</span><span class="sxs-lookup"><span data-stu-id="13db5-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="13db5-125">ASP.NET MVC HTML sayfaları için istemci bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13db5-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="13db5-126">ASP.NET Web API (ürünler ve siparişler) veri CRUD işlemleri sunar.</span><span class="sxs-lookup"><span data-stu-id="13db5-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="13db5-127">Varlık çerçevesi veritabanı varlıklarını Web API'si tarafından kullanılan C# modelleri çevirir.</span><span class="sxs-lookup"><span data-stu-id="13db5-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="13db5-128">Aşağıdaki diyagramda, etki alanı nesnelerini uygulamasının çeşitli katmanına nasıl temsil edildiğini gösterir: Veritabanı katmanı, nesne modeli ve son olarak istemci HTTP üzerinden veri iletmek için kullanılan gönderme biçimini.</span><span class="sxs-lookup"><span data-stu-id="13db5-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="13db5-129">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="13db5-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="13db5-130">Visual Web Developer Express veya tam Visual Studio sürümünü kullanarak öğretici projesinin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13db5-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="13db5-131">Gelen **Başlat** sayfasında **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="13db5-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="13db5-132">İçinde **şablonları** bölmesinde **yüklü şablonlar** genişletin **Visual C#** düğümü.</span><span class="sxs-lookup"><span data-stu-id="13db5-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="13db5-133">Altında **Visual C#** seçin **Web**.</span><span class="sxs-lookup"><span data-stu-id="13db5-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="13db5-134">Proje şablonları listesinde seçin **ASP.NET MVC 4 Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="13db5-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="13db5-135">"ProductStore" Projeyi adlandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13db5-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="13db5-136">İçinde **yeni ASP.NET MVC 4 proje** iletişim kutusunda **Internet uygulaması** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13db5-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="13db5-137">"Internet uygulama" şablonu, forms kimlik doğrulamasını destekleyen bir ASP.NET MVC uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13db5-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="13db5-138">Uygulamayı şimdi çalıştırırsanız, zaten bazı özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="13db5-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="13db5-139">Yeni kullanıcılar, sağ üst köşedeki "Register" bağlantısına tıklayarak kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="13db5-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="13db5-140">Kayıtlı kullanıcılar "Oturum Aç" bağlantısına tıklayarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="13db5-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="13db5-141">Üyelik bilgileri otomatik olarak oluşturulan bir veritabanında kalıcı hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="13db5-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="13db5-142">ASP.NET mvc'de form kimlik doğrulaması hakkında daha fazla bilgi için bkz: [izlenecek yol: ASP.NET MVC'de form kimlik doğrulaması kullanarak](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="13db5-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="13db5-143">CSS dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="13db5-143">Update the CSS File</span></span>

<span data-ttu-id="13db5-144">Bu adım yüzeysel, ancak önceki ekran görüntüleri gibi işleme sayfaları hale getirir.</span><span class="sxs-lookup"><span data-stu-id="13db5-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="13db5-145">Çözüm Gezgini'nde içerik klasörünü genişletin ve Site.css adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="13db5-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="13db5-146">Aşağıdaki CSS stilleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="13db5-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="13db5-147">Next</span><span class="sxs-lookup"><span data-stu-id="13db5-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)