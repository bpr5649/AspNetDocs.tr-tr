---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2'de öznitelik yönlendirme ile REST API oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 18a44c280e6df1603837938d24d7d639d8c87cc2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075216"
---
<a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="717f1-102">ASP.NET Web API 2 yönlendirme özniteliğine sahip bir REST API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="717f1-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="717f1-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="717f1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="717f1-104">Web API 2 destekleyen yeni bir tür adı yönlendirme *öznitelik yönlendirme*.</span><span class="sxs-lookup"><span data-stu-id="717f1-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="717f1-105">Öznitelik yönlendirme genel bakış için bkz: [Web API 2'de öznitelik yönlendirme](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="717f1-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="717f1-106">Bu öğreticide, öznitelik yönlendirme books koleksiyonu için bir REST API oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="717f1-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="717f1-107">API aşağıdaki eylemleri destekler:</span><span class="sxs-lookup"><span data-stu-id="717f1-107">The API will support the following actions:</span></span>

| <span data-ttu-id="717f1-108">Eylem</span><span class="sxs-lookup"><span data-stu-id="717f1-108">Action</span></span> | <span data-ttu-id="717f1-109">Örnek URI</span><span class="sxs-lookup"><span data-stu-id="717f1-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="717f1-110">Tüm Kitaplar bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="717f1-110">Get a list of all books.</span></span> | <span data-ttu-id="717f1-111">/ api/kitaplar</span><span class="sxs-lookup"><span data-stu-id="717f1-111">/api/books</span></span> |
| <span data-ttu-id="717f1-112">Bir kitap kimliğe göre Al</span><span class="sxs-lookup"><span data-stu-id="717f1-112">Get a book by ID.</span></span> | <span data-ttu-id="717f1-113">/api/Books/1</span><span class="sxs-lookup"><span data-stu-id="717f1-113">/api/books/1</span></span> |
| <span data-ttu-id="717f1-114">Bir kitap ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="717f1-114">Get the details of a book.</span></span> | <span data-ttu-id="717f1-115">/api/Books/1/details</span><span class="sxs-lookup"><span data-stu-id="717f1-115">/api/books/1/details</span></span> |
| <span data-ttu-id="717f1-116">Kitap listesi türe göre alın.</span><span class="sxs-lookup"><span data-stu-id="717f1-116">Get a list of books by genre.</span></span> | <span data-ttu-id="717f1-117">/api/Books/fantasy</span><span class="sxs-lookup"><span data-stu-id="717f1-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="717f1-118">Kitap listesi, yayın tarihe göre alın.</span><span class="sxs-lookup"><span data-stu-id="717f1-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="717f1-119">/api/Books/Date/2013-02-16 /api/books/date/2013/02/16 (alternatif formu)</span><span class="sxs-lookup"><span data-stu-id="717f1-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="717f1-120">Belirli bir yazar tarafından books bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="717f1-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="717f1-121">/api/Authors/1/Books</span><span class="sxs-lookup"><span data-stu-id="717f1-121">/api/authors/1/books</span></span> |

<span data-ttu-id="717f1-122">Salt okunur (HTTP GET isteklerini) tüm yöntemlerdir.</span><span class="sxs-lookup"><span data-stu-id="717f1-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="717f1-123">Entity Framework veri katmanı için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="717f1-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="717f1-124">Kitap kayıtlarını, aşağıdaki alanları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="717f1-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="717f1-125">Kimlik</span><span class="sxs-lookup"><span data-stu-id="717f1-125">ID</span></span>
- <span data-ttu-id="717f1-126">Başlık</span><span class="sxs-lookup"><span data-stu-id="717f1-126">Title</span></span>
- <span data-ttu-id="717f1-127">Tarzı</span><span class="sxs-lookup"><span data-stu-id="717f1-127">Genre</span></span>
- <span data-ttu-id="717f1-128">Yayın tarihi</span><span class="sxs-lookup"><span data-stu-id="717f1-128">Publication date</span></span>
- <span data-ttu-id="717f1-129">Fiyat</span><span class="sxs-lookup"><span data-stu-id="717f1-129">Price</span></span>
- <span data-ttu-id="717f1-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="717f1-130">Description</span></span>
- <span data-ttu-id="717f1-131">AuthorID (yazarlar tabloya yabancı anahtar)</span><span class="sxs-lookup"><span data-stu-id="717f1-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="717f1-132">İsteklerin çoğuna ancak API (başlık, yazar ve Tarz) bu verilerin bir alt kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="717f1-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="717f1-133">Tam kayıt, istemci isteklerini almak için `/api/books/{id}/details`.</span><span class="sxs-lookup"><span data-stu-id="717f1-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="717f1-134">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="717f1-134">Prerequisites</span></span>

<span data-ttu-id="717f1-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="717f1-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="717f1-136">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="717f1-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="717f1-137">Visual Studio çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="717f1-137">Start by running Visual Studio.</span></span> <span data-ttu-id="717f1-138">Gelen **dosya** menüsünde **yeni** seçip **proje**.</span><span class="sxs-lookup"><span data-stu-id="717f1-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="717f1-139">Genişletin **yüklü** > **Visual C#** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="717f1-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="717f1-140">Altında **Visual C#** seçin **Web**.</span><span class="sxs-lookup"><span data-stu-id="717f1-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="717f1-141">Proje şablonları listesinde seçin **ASP.NET Web uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="717f1-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="717f1-142">Projeyi adlandırın &quot;BooksAPI&quot;.</span><span class="sxs-lookup"><span data-stu-id="717f1-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="717f1-143">İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda **boş** şablonu.</span><span class="sxs-lookup"><span data-stu-id="717f1-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="717f1-144">"Klasör eklemek ve çekirdek başvuruları için" altında seçin **Web API** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="717f1-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="717f1-145">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="717f1-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="717f1-146">Bu, Web API işlevleri için yapılandırılmış bir çatı projesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="717f1-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="717f1-147">Etki alanı modelleri</span><span class="sxs-lookup"><span data-stu-id="717f1-147">Domain Models</span></span>

<span data-ttu-id="717f1-148">Ardından, etki alanı modelleri sınıfları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="717f1-148">Next, add classes for domain models.</span></span> <span data-ttu-id="717f1-149">Çözüm Gezgini'nde modeller klasörü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="717f1-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="717f1-150">Seçin **Ekle**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="717f1-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="717f1-151">Sınıf adını `Author`.</span><span class="sxs-lookup"><span data-stu-id="717f1-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="717f1-152">Author.cs kodu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="717f1-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="717f1-153">Şimdi adlı başka bir sınıf ekleyin `Book`.</span><span class="sxs-lookup"><span data-stu-id="717f1-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="717f1-154">Web API denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="717f1-154">Add a Web API Controller</span></span>

<span data-ttu-id="717f1-155">Bu adımda, veri katmanı olarak Entity Framework kullanan bir Web API denetleyicisi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="717f1-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="717f1-156">Projeyi oluşturmak için CTRL+SHIFT+B tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="717f1-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="717f1-157">Entity Framework veritabanı şeması oluşturmak derlenmiş bir bütünleştirilmiş kod gerektirir böylece modellerinin özelliklerini bulmak için yansıtma kullanır.</span><span class="sxs-lookup"><span data-stu-id="717f1-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="717f1-158">Çözüm Gezgini'nde denetleyicileri klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="717f1-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="717f1-159">Seçin **Ekle**, ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="717f1-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="717f1-160">İçinde **İskele Ekle** iletişim kutusunda **Web API 2 denetleyici Entity Framework kullanarak Eylemler ile**.</span><span class="sxs-lookup"><span data-stu-id="717f1-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="717f1-161">İçinde **denetleyici Ekle** iletişim için **Denetleyici adı**, girin &quot;BooksController&quot;.</span><span class="sxs-lookup"><span data-stu-id="717f1-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="717f1-162">Seçin &quot;zaman uyumsuz denetleyici eylemlerini kullanmak&quot; onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="717f1-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="717f1-163">İçin **Model sınıfı**seçin &quot;kitap&quot;.</span><span class="sxs-lookup"><span data-stu-id="717f1-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="717f1-164">(Görmüyorsanız `Book` sınıfı listelenen açılır menüde, proje oluşturulan emin olun.) Ardından, "+" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="717f1-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="717f1-165">Tıklayın **Ekle** içinde **yeni veri bağlamı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="717f1-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="717f1-166">Tıklayın **Ekle** içinde **denetleyici Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="717f1-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="717f1-167">Yapı iskelesi adlı bir sınıf ekler `BooksController` tanımlayan bir API denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="717f1-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="717f1-168">Ayrıca adlı bir sınıf ekler `BooksAPIContext` için Entity Framework veri bağlamı tanımlar modelleri klasöründe.</span><span class="sxs-lookup"><span data-stu-id="717f1-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="717f1-169">Veritabanının Çekirdeğini Oluşturma</span><span class="sxs-lookup"><span data-stu-id="717f1-169">Seed the Database</span></span>

<span data-ttu-id="717f1-170">Araçlar menüsü'nden seçin **NuGet Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="717f1-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="717f1-171">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="717f1-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="717f1-172">Bu komut, geçişler klasörü oluşturur ve Configuration.cs adlı yeni bir kod dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="717f1-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="717f1-173">Bu dosyayı açın ve aşağıdaki kodu ekleyin `Configuration.Seed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="717f1-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="717f1-174">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="717f1-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="717f1-175">Bu komutlar, yerel bir veritabanı oluşturun ve veritabanını doldurmak için Seed yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="717f1-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="717f1-176">DTO sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="717f1-176">Add DTO Classes</span></span>

<span data-ttu-id="717f1-177">Şimdi uygulamayı çalıştırın ve bir GET isteği göndermek için /api/books/1, yanıtı aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="717f1-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="717f1-178">(Okunabilirlik için Girintileme ekledim.)</span><span class="sxs-lookup"><span data-stu-id="717f1-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="717f1-179">Bunun yerine, alanların bir alt kümesini döndürmek için bu istek için istiyorum.</span><span class="sxs-lookup"><span data-stu-id="717f1-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="717f1-180">Ayrıca, Yazar Kimliği yerine, yazarın adı döndürülecek istediğim</span><span class="sxs-lookup"><span data-stu-id="717f1-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="717f1-181">Bunu yapmak için biz döndürülecek denetleyicisi yöntemi değiştireceksiniz bir *veri aktarımı nesnesi* (DTO) yerine EF modeli.</span><span class="sxs-lookup"><span data-stu-id="717f1-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="717f1-182">Bir DTO, yalnızca veri taşımak üzere tasarlanmış bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="717f1-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="717f1-183">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle** | **yeni klasör**.</span><span class="sxs-lookup"><span data-stu-id="717f1-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="717f1-184">Klasör adı &quot;Dto'lar&quot;.</span><span class="sxs-lookup"><span data-stu-id="717f1-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="717f1-185">Adlı bir sınıf ekleyin `BookDto` Dto'lar klasörüne aşağıdaki tanımıyla:</span><span class="sxs-lookup"><span data-stu-id="717f1-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="717f1-186">Adlı başka bir sınıf ekleyin `BookDetailDto`.</span><span class="sxs-lookup"><span data-stu-id="717f1-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="717f1-187">Ardından, güncelleştirme `BooksController` döndürülecek sınıfı `BookDto` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="717f1-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="717f1-188">Kullanacağız [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) projesine yöntemi `Book` için örnekler `BookDto` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="717f1-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="717f1-189">Denetleyici sınıfı için güncelleştirilmiş kod aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="717f1-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="717f1-190">Sildim `PutBook`, `PostBook`, ve `DeleteBook` yöntemleri, çünkü bu öğretici için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="717f1-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>


<span data-ttu-id="717f1-191">Şimdi uygulamayı çalıştırabilir ve /api/books/1 istek, yanıt gövdesi şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="717f1-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="717f1-192">Rota özniteliklerini ekleme</span><span class="sxs-lookup"><span data-stu-id="717f1-192">Add Route Attributes</span></span>

<span data-ttu-id="717f1-193">Ardından, biz özniteliği yönlendirmeyi kullanmak için denetleyici dönüştürmeniz.</span><span class="sxs-lookup"><span data-stu-id="717f1-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="717f1-194">İlk olarak, ekleme bir **routeprefix öğesi** özniteliği denetleyiciye.</span><span class="sxs-lookup"><span data-stu-id="717f1-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="717f1-195">Bu öznitelik, bu denetleyici üzerinde tüm yöntemleri için başlangıç URI kesimleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="717f1-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="717f1-196">Ardından Ekle **[yol]** denetleyici eylemleri için aşağıdaki gibi öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="717f1-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="717f1-197">Her denetleyici yöntemi için rota şablonu önekidir ve dizeyi belirtilen **rota** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="717f1-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="717f1-198">İçin `GetBook` parametreli dizeyi includes yöntemi, rota şablonu &quot;{kimliği: int}&quot;, URI segmenti bir tamsayı değeri içeriyorsa eşleşir.</span><span class="sxs-lookup"><span data-stu-id="717f1-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="717f1-199">Yöntem</span><span class="sxs-lookup"><span data-stu-id="717f1-199">Method</span></span> | <span data-ttu-id="717f1-200">Rota şablonu</span><span class="sxs-lookup"><span data-stu-id="717f1-200">Route Template</span></span> | <span data-ttu-id="717f1-201">Örnek URI</span><span class="sxs-lookup"><span data-stu-id="717f1-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="717f1-202">"API/books"</span><span class="sxs-lookup"><span data-stu-id="717f1-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="717f1-203">"api/books/{id:int}"</span><span class="sxs-lookup"><span data-stu-id="717f1-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="717f1-204">Kitap ayrıntılarını Al</span><span class="sxs-lookup"><span data-stu-id="717f1-204">Get Book Details</span></span>

<span data-ttu-id="717f1-205">Kitap ayrıntıları almak için istemci, bir GET isteği gönderir `/api/books/{id}/details`burada *{id}* kitabın kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="717f1-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="717f1-206">Aşağıdaki yöntemi ekleyin `BooksController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="717f1-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="717f1-207">Eğer istenmişse `/api/books/1/details`, yanıt şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="717f1-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="717f1-208">Türe göre kitap alma</span><span class="sxs-lookup"><span data-stu-id="717f1-208">Get Books By Genre</span></span>

<span data-ttu-id="717f1-209">Belirli bir tarzında books listesini almak için istemci, bir GET isteği gönderir `/api/books/genre`burada *Tarz* Tarz adıdır.</span><span class="sxs-lookup"><span data-stu-id="717f1-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="717f1-210">(Örneğin, `/api/books/fantasy`.)</span><span class="sxs-lookup"><span data-stu-id="717f1-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="717f1-211">Aşağıdaki yöntemi ekleyin `BooksController`.</span><span class="sxs-lookup"><span data-stu-id="717f1-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="717f1-212">Biz bir URI şablonu {Tarz} parametresi içeren bir yol burada tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="717f1-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="717f1-213">Web API'si bu iki bir URI'leri ayırmak ve bunları farklı yöntemleri için yol olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="717f1-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="717f1-214">Çünkü `GetBook` yöntemi içeren bir kısıtlama "id" segment bir tamsayı değeri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="717f1-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="717f1-215">/Api/books/fantasy istek, yanıt şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="717f1-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="717f1-216">Yazara göre kitapları alın</span><span class="sxs-lookup"><span data-stu-id="717f1-216">Get Books By Author</span></span>

<span data-ttu-id="717f1-217">Belirli bir yazar için bir kitap listesi almak için istemci, bir GET isteği gönderir `/api/authors/id/books`burada *kimliği* Yazar kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="717f1-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="717f1-218">Aşağıdaki yöntemi ekleyin `BooksController`.</span><span class="sxs-lookup"><span data-stu-id="717f1-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="717f1-219">Bu örnekte ilginç, çünkü &quot;books&quot; olan bir alt kaynağın kabul &quot;yazarlar&quot;.</span><span class="sxs-lookup"><span data-stu-id="717f1-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="717f1-220">Bu düzen, RESTful API'leri oldukça yaygındır.</span><span class="sxs-lookup"><span data-stu-id="717f1-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="717f1-221">Yol şablonunda tilde (~) yol ön eki geçersiz kılmalar **routeprefix öğesi** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="717f1-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="717f1-222">Kitap Yayını tarihe göre Al</span><span class="sxs-lookup"><span data-stu-id="717f1-222">Get Books By Publication Date</span></span>

<span data-ttu-id="717f1-223">Yayın tarihe göre kitap listesi almak için istemci, bir GET isteği gönderir `/api/books/date/yyyy-mm-dd`burada *yyyy-aa-gg* tarihtir.</span><span class="sxs-lookup"><span data-stu-id="717f1-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="717f1-224">Bunu yapmanın bir yolu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="717f1-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="717f1-225">`{pubdate:datetime}` Eşleştirilecek parametresi kısıtlı bir **DateTime** değeri.</span><span class="sxs-lookup"><span data-stu-id="717f1-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="717f1-226">Bu çalışır, ancak çok isteriz gerçekten daha fazla izin veremez.</span><span class="sxs-lookup"><span data-stu-id="717f1-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="717f1-227">Örneğin, bu bir URI'leri rota eşleşir:</span><span class="sxs-lookup"><span data-stu-id="717f1-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="717f1-228">Bu bir URI'leri vermekle yanlış bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="717f1-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="717f1-229">Ancak bir normal ifade kısıtlaması için rota şablonu ekleyerek belirli bir biçime rota kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="717f1-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="717f1-230">Artık yalnızca tarih biçiminde &quot;yyyy-aa-gg&quot; eşleşir.</span><span class="sxs-lookup"><span data-stu-id="717f1-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="717f1-231">Biz regex gerçek tarih yapılandırdığımıza doğrulamak için kullanmayın dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="717f1-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="717f1-232">Web API uygulamasına URI segmenti Dönüştür çalıştığında işlenen bir **DateTime** örneği.</span><span class="sxs-lookup"><span data-stu-id="717f1-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="717f1-233">Geçersiz bir tarih gibi ' 2012-47-99' başarısız olur dönüştürülecek ve istemci bir 404 hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="717f1-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="717f1-234">Bir eğik çizgi ayırıcı de destekleyebilir (`/api/books/date/yyyy/mm/dd`) diğerine ekleyerek **[yol]** farklı bir regex ile özniteliği.</span><span class="sxs-lookup"><span data-stu-id="717f1-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="717f1-235">Burada küçük ancak önemli ayrıntı yok.</span><span class="sxs-lookup"><span data-stu-id="717f1-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="717f1-236">İkinci rota şablonu olan bir joker karakter (\*) {pubdate} parametresi başlangıcı:</span><span class="sxs-lookup"><span data-stu-id="717f1-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="717f1-237">Bu, yönlendirme altyapısını {pubdate} URI'ın geri kalan eşleşmelidir bildirir.</span><span class="sxs-lookup"><span data-stu-id="717f1-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="717f1-238">Varsayılan olarak, bir şablon parametresi, tek bir URI segmenti eşleşir.</span><span class="sxs-lookup"><span data-stu-id="717f1-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="717f1-239">Bu durumda, {pubdate} birkaç URI segmentleri span istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="717f1-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="717f1-240">Denetleyici kodlarının</span><span class="sxs-lookup"><span data-stu-id="717f1-240">Controller Code</span></span>

<span data-ttu-id="717f1-241">BooksController sınıf için tam kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="717f1-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="717f1-242">Özet</span><span class="sxs-lookup"><span data-stu-id="717f1-242">Summary</span></span>

<span data-ttu-id="717f1-243">Öznitelik yönlendirme, daha fazla denetim ve esneklik, API'niz için bir URI'leri tasarlarken sunar.</span><span class="sxs-lookup"><span data-stu-id="717f1-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
