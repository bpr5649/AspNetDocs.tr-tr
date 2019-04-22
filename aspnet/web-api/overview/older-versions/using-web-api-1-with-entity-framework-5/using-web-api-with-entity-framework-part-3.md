---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'Bölüm 3: Yönetim denetleyicisi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: de4bb063d2a6c1bdb4aeffdadb161ef19efd2b78
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59390954"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="a520b-102">Bölüm 3: Yönetim Denetleyicisi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="a520b-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="a520b-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a520b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a520b-104">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="a520b-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="a520b-105">Yönetim Denetleyicisi Ekle</span><span class="sxs-lookup"><span data-stu-id="a520b-105">Add an Admin Controller</span></span>

<span data-ttu-id="a520b-106">Bu bölümde, CRUD destekleyen bir Web API denetleyicisi ekleyeceğiz (oluşturma, okuma, güncelleştirme ve silme) ürünleri işlemleri.</span><span class="sxs-lookup"><span data-stu-id="a520b-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="a520b-107">Denetleyici, Entity Framework veritabanı katmanı ile iletişim kurmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a520b-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="a520b-108">Yalnızca Yöneticiler bu denetleyici kullanmanız mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a520b-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="a520b-109">Müşteriler, ürünler başka bir denetleyici erişir.</span><span class="sxs-lookup"><span data-stu-id="a520b-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="a520b-110">Çözüm Gezgini'nde denetleyicileri klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a520b-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="a520b-111">Seçin **ekleme** ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="a520b-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="a520b-112">İçinde **denetleyici Ekle** iletişim kutusunda, denetleyici adı `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="a520b-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="a520b-113">Altında **şablon**seçin &quot;Entity Framework kullanarak okuma/yazma eylemleri olan API denetleyicisi&quot;.</span><span class="sxs-lookup"><span data-stu-id="a520b-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="a520b-114">Altında **Model sınıfı**, "Ürün (ProductStore.Models)" seçin.</span><span class="sxs-lookup"><span data-stu-id="a520b-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="a520b-115">Altında **veri bağlamı**seçin "&lt;yeni veri bağlamı&gt;".</span><span class="sxs-lookup"><span data-stu-id="a520b-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="a520b-116">Varsa **Model sınıfı** açılan göstermiyor herhangi bir model sınıfları, projeye derlenmiş olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a520b-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="a520b-117">Entity Framework, yansıma, kullanır, bu nedenle derlenmiş bütünleştirilmiş kodu gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a520b-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>


<span data-ttu-id="a520b-118">Seçme "&lt;yeni veri bağlamı&gt;" açılır **yeni veri bağlamı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a520b-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="a520b-119">Veri bağlamının adı `ProductStore.Models.OrdersContext`.</span><span class="sxs-lookup"><span data-stu-id="a520b-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="a520b-120">Tıklayın **Tamam** kapatmak için **yeni veri bağlamı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a520b-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="a520b-121">İçinde **denetleyici Ekle** iletişim kutusunda, tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a520b-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="a520b-122">Projeye eklenen aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a520b-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="a520b-123">Adlı bir sınıf `OrdersContext` türetilen **DbContext**.</span><span class="sxs-lookup"><span data-stu-id="a520b-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="a520b-124">Bu sınıf, bağlantılı POCO modelleri ve veritabanı arasındaki sağlar.</span><span class="sxs-lookup"><span data-stu-id="a520b-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="a520b-125">Adlı bir Web API denetleyicisi `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="a520b-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="a520b-126">Bu denetleyici üzerinde CRUD işlemleri destekleyen `Product` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="a520b-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="a520b-127">Kullandığı `OrdersContext` Entity Framework ile iletişim kurmak için sınıf.</span><span class="sxs-lookup"><span data-stu-id="a520b-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="a520b-128">Web.config dosyasında yeni bir veritabanı bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="a520b-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="a520b-129">OrdersContext.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a520b-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="a520b-130">Bildirim oluşturucu veritabanı bağlantı dizesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a520b-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="a520b-131">Bu ad, bağlantı dizesini Web.config dosyasına eklenen ifade eder.</span><span class="sxs-lookup"><span data-stu-id="a520b-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="a520b-132">Aşağıdaki özellikleri `OrdersContext` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="a520b-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="a520b-133">A **olan DB** sorgulanabilir varlık kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a520b-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="a520b-134">Tam liste için işte `OrdersContext` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="a520b-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="a520b-135">`AdminController` Sınıfı, temel CRUD işlevselliği uygulamak beş yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a520b-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="a520b-136">Her yöntem istemci çağırabileceği bir URI karşılık gelmektedir:</span><span class="sxs-lookup"><span data-stu-id="a520b-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="a520b-137">Denetleyici yöntemi</span><span class="sxs-lookup"><span data-stu-id="a520b-137">Controller Method</span></span> | <span data-ttu-id="a520b-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a520b-138">Description</span></span> | <span data-ttu-id="a520b-139">URI</span><span class="sxs-lookup"><span data-stu-id="a520b-139">URI</span></span> | <span data-ttu-id="a520b-140">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="a520b-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a520b-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="a520b-141">GetProducts</span></span> | <span data-ttu-id="a520b-142">Tüm ürünler alır.</span><span class="sxs-lookup"><span data-stu-id="a520b-142">Gets all products.</span></span> | <span data-ttu-id="a520b-143">API/ürünleri</span><span class="sxs-lookup"><span data-stu-id="a520b-143">api/products</span></span> | <span data-ttu-id="a520b-144">GET</span><span class="sxs-lookup"><span data-stu-id="a520b-144">GET</span></span> |
| <span data-ttu-id="a520b-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="a520b-145">GetProduct</span></span> | <span data-ttu-id="a520b-146">Bir ürün kimliğine göre bulur</span><span class="sxs-lookup"><span data-stu-id="a520b-146">Finds a product by ID.</span></span> | <span data-ttu-id="a520b-147">API/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="a520b-147">api/products/*id*</span></span> | <span data-ttu-id="a520b-148">GET</span><span class="sxs-lookup"><span data-stu-id="a520b-148">GET</span></span> |
| <span data-ttu-id="a520b-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="a520b-149">PutProduct</span></span> | <span data-ttu-id="a520b-150">Bir ürün güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a520b-150">Updates a product.</span></span> | <span data-ttu-id="a520b-151">API/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="a520b-151">api/products/*id*</span></span> | <span data-ttu-id="a520b-152">PUT</span><span class="sxs-lookup"><span data-stu-id="a520b-152">PUT</span></span> |
| <span data-ttu-id="a520b-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="a520b-153">PostProduct</span></span> | <span data-ttu-id="a520b-154">Yeni bir ürün oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a520b-154">Creates a new product.</span></span> | <span data-ttu-id="a520b-155">API/ürünleri</span><span class="sxs-lookup"><span data-stu-id="a520b-155">api/products</span></span> | <span data-ttu-id="a520b-156">POST</span><span class="sxs-lookup"><span data-stu-id="a520b-156">POST</span></span> |
| <span data-ttu-id="a520b-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="a520b-157">DeleteProduct</span></span> | <span data-ttu-id="a520b-158">Bir ürün siler.</span><span class="sxs-lookup"><span data-stu-id="a520b-158">Deletes a product.</span></span> | <span data-ttu-id="a520b-159">API/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="a520b-159">api/products/*id*</span></span> | <span data-ttu-id="a520b-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="a520b-160">DELETE</span></span> |

<span data-ttu-id="a520b-161">Her yöntem içine yapılan çağrılar `OrdersContext` veritabanını sorgulamak için.</span><span class="sxs-lookup"><span data-stu-id="a520b-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="a520b-162">Koleksiyon (PUT, POST ve DELETE) değiştirme yöntemlerini çağıran `db.SaveChanges` veritabanına değişiklikleri kalıcı hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="a520b-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="a520b-163">Denetleyicileri HTTP istek başına oluşturulan ve atıldı, bir yöntem döndürmeden önce değişiklikleri kalıcı hale getirmek için gerekli olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="a520b-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="a520b-164">Bir veritabanı Başlatıcı Ekle</span><span class="sxs-lookup"><span data-stu-id="a520b-164">Add a Database Initializer</span></span>

<span data-ttu-id="a520b-165">Entity Framework başlangıçta veritabanını doldurmak ve modelleri değiştirdiğinizde veritabanını otomatik olarak yeniden olanak tanıyan kullanışlı bir özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a520b-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="a520b-166">Modelleri değiştirseniz bile bazı test verilerini her zaman sahip olduğundan bu geliştirme sırasında yararlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="a520b-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="a520b-167">Çözüm Gezgini'nde, modeller klasörü sağ tıklatın ve adlı yeni bir sınıf oluşturun `OrdersContextInitializer`.</span><span class="sxs-lookup"><span data-stu-id="a520b-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="a520b-168">Aşağıdaki uygulama içinde yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="a520b-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="a520b-169">Öğesinden devralan tarafından **DropCreateDatabaseIfModelChanges** sınıfı, biz söyleyen model sınıfları ki değiştirme her veritabanını bırakmak için Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="a520b-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="a520b-170">Entity Framework oluşturur (veya yeniden oluşturur) veritabanı, onu çağırır **çekirdek** tablolarını doldurmak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a520b-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="a520b-171">Kullandığımız **çekirdek** bazı örnek ürünlerinin yanı sıra örnek sipariş eklemek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a520b-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="a520b-172">Bu özelliği test etmek için harika bir deneyimdir ancak kullanmayın **DropCreateDatabaseIfModelChanges** sınıfı üretim ortamında, çünkü birisi bir model sınıfı değişirse, veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a520b-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="a520b-173">Ardından, Global.asax açın ve aşağıdaki kodu ekleyin **uygulama\_Başlat** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a520b-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="a520b-174">Denetleyici için bir istek gönderin</span><span class="sxs-lookup"><span data-stu-id="a520b-174">Send a Request to the Controller</span></span>

<span data-ttu-id="a520b-175">Bu noktada, biz herhangi bir istemci kodu yazmadınız, ancak bir web tarayıcısı ya da bir HTTP hata ayıklama kullanarak API aracı gibi web çağırabilirsiniz [Fiddler](http://www.fiddler2.com/fiddler2/).</span><span class="sxs-lookup"><span data-stu-id="a520b-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="a520b-176">Visual Studio'da hata ayıklamayı başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a520b-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="a520b-177">Web tarayıcınızda açılacak `http://localhost:*portnum*/`burada *portnum* bazı bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="a520b-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="a520b-178">Bir HTTP isteği Gönder "`http://localhost:*portnum*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="a520b-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="a520b-179">Entity Framework oluşturun ve veritabanının çekirdeğini oluşturma gerektiğinden ilk istek tamamlanmak için yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="a520b-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="a520b-180">Yanıt, aşağıdakine benzer bir şey gerekir:</span><span class="sxs-lookup"><span data-stu-id="a520b-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="a520b-181">[Önceki](using-web-api-with-entity-framework-part-2.md)
> [İleri](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="a520b-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
