---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188917"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="d81cd-102">ASP.NET Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma</span><span class="sxs-lookup"><span data-stu-id="d81cd-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="d81cd-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d81cd-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d81cd-104">Web API 2 ' de *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="d81cd-105">Öznitelik yönlendirmeye genel bir bakış için bkz. [Web API 2 ' de öznitelik yönlendirme](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="d81cd-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="d81cd-106">Bu öğreticide, bir kitap koleksiyonu için REST API oluşturmak üzere öznitelik yönlendirmeyi kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d81cd-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="d81cd-107">API aşağıdaki eylemleri destekler:</span><span class="sxs-lookup"><span data-stu-id="d81cd-107">The API will support the following actions:</span></span>

| <span data-ttu-id="d81cd-108">Eylem</span><span class="sxs-lookup"><span data-stu-id="d81cd-108">Action</span></span> | <span data-ttu-id="d81cd-109">Örnek URI</span><span class="sxs-lookup"><span data-stu-id="d81cd-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="d81cd-110">Tüm kitapların bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-110">Get a list of all books.</span></span> | <span data-ttu-id="d81cd-111">/api/Books</span><span class="sxs-lookup"><span data-stu-id="d81cd-111">/api/books</span></span> |
| <span data-ttu-id="d81cd-112">KIMLIĞE göre bir kitap alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-112">Get a book by ID.</span></span> | <span data-ttu-id="d81cd-113">/api/Books/1</span><span class="sxs-lookup"><span data-stu-id="d81cd-113">/api/books/1</span></span> |
| <span data-ttu-id="d81cd-114">Bir kitabın ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-114">Get the details of a book.</span></span> | <span data-ttu-id="d81cd-115">/api/Books/1/details</span><span class="sxs-lookup"><span data-stu-id="d81cd-115">/api/books/1/details</span></span> |
| <span data-ttu-id="d81cd-116">Türe göre kitap listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-116">Get a list of books by genre.</span></span> | <span data-ttu-id="d81cd-117">/api/Books/fantei</span><span class="sxs-lookup"><span data-stu-id="d81cd-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="d81cd-118">Yayın tarihine göre Kitaplar listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="d81cd-119">/api/Books/Date/2013-02-16/api/Books/Date/2013/02/16 (alternatif form)</span><span class="sxs-lookup"><span data-stu-id="d81cd-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="d81cd-120">Belirli bir yazarın kitap listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="d81cd-121">/api/Authors/1/Books</span><span class="sxs-lookup"><span data-stu-id="d81cd-121">/api/authors/1/books</span></span> |

<span data-ttu-id="d81cd-122">Tüm yöntemler salt okunurdur (HTTP GET istekleri).</span><span class="sxs-lookup"><span data-stu-id="d81cd-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="d81cd-123">Veri katmanı için Entity Framework kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d81cd-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="d81cd-124">Kitap kayıtları aşağıdaki alanlara sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="d81cd-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="d81cd-125">ID</span><span class="sxs-lookup"><span data-stu-id="d81cd-125">ID</span></span>
- <span data-ttu-id="d81cd-126">Title</span><span class="sxs-lookup"><span data-stu-id="d81cd-126">Title</span></span>
- <span data-ttu-id="d81cd-127">Tarzı</span><span class="sxs-lookup"><span data-stu-id="d81cd-127">Genre</span></span>
- <span data-ttu-id="d81cd-128">Yayın tarihi</span><span class="sxs-lookup"><span data-stu-id="d81cd-128">Publication date</span></span>
- <span data-ttu-id="d81cd-129">Fiyat</span><span class="sxs-lookup"><span data-stu-id="d81cd-129">Price</span></span>
- <span data-ttu-id="d81cd-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d81cd-130">Description</span></span>
- <span data-ttu-id="d81cd-131">AuthorId (bir yazarlar tablosuna yabancı anahtar)</span><span class="sxs-lookup"><span data-stu-id="d81cd-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="d81cd-132">Ancak, çoğu istek için, API bu verilerin bir alt kümesini döndürür (başlık, yazar ve tarz).</span><span class="sxs-lookup"><span data-stu-id="d81cd-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="d81cd-133">Tüm kayıtları almak için istemci istekleri `/api/books/{id}/details` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d81cd-134">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d81cd-134">Prerequisites</span></span>

<span data-ttu-id="d81cd-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="d81cd-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="d81cd-136">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d81cd-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="d81cd-137">Visual Studio 'Yu çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-137">Start by running Visual Studio.</span></span> <span data-ttu-id="d81cd-138">**Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="d81cd-139">**Yüklü**  >  **Visual C#** kategorisini genişletin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="d81cd-140">**Visual C#** altında **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="d81cd-141">Proje şablonları listesinde **ASP.NET Web uygulaması (.NET Framework)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="d81cd-142">Projeyi &quot; booksapı olarak adlandırın &quot; .</span><span class="sxs-lookup"><span data-stu-id="d81cd-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="d81cd-143">**Yeni ASP.NET Web uygulaması** Iletişim kutusunda **boş** şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="d81cd-144">"Klasör ve çekirdek başvuruları Ekle" altında **Web API** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="d81cd-145">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="d81cd-146">Bu, Web API işlevselliği için yapılandırılmış bir iskelet projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d81cd-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="d81cd-147">Etki alanı modelleri</span><span class="sxs-lookup"><span data-stu-id="d81cd-147">Domain Models</span></span>

<span data-ttu-id="d81cd-148">Daha sonra, etki alanı modelleri için sınıflar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-148">Next, add classes for domain models.</span></span> <span data-ttu-id="d81cd-149">Çözüm Gezgini modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="d81cd-150">**Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="d81cd-151">Sınıfı adlandırın `Author` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="d81cd-152">Author.cs içindeki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d81cd-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="d81cd-153">Şimdi adlı başka bir sınıf ekleyin `Book` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="d81cd-154">Web API denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="d81cd-154">Add a Web API Controller</span></span>

<span data-ttu-id="d81cd-155">Bu adımda, veri katmanı olarak Entity Framework kullanan bir Web API denetleyicisi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="d81cd-156">Projeyi oluşturmak için CTRL+SHIFT+B tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="d81cd-157">Entity Framework, modellerin özelliklerini saptamak için yansıma kullanır, bu nedenle veritabanı şemasını oluşturmak için derlenmiş bir bütünleştirilmiş kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="d81cd-158">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="d81cd-159">**Ekle**' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="d81cd-160">**Yapı Iskelesi Ekle** iletişim kutusunda, **ENTITY Framework kullanarak Web API 2 denetleyiciyi eylemlerle '** yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="d81cd-161">**Denetleyici Ekle** iletişim kutusunda, **Denetleyici adı**için, &quot; bookscontroller yazın &quot; .</span><span class="sxs-lookup"><span data-stu-id="d81cd-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="d81cd-162">&quot;Zaman uyumsuz denetleyici eylemlerini kullan &quot; onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="d81cd-163">**Model sınıfı**için kitap ' ı seçin &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="d81cd-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="d81cd-164">( `Book` Açılan listede sınıfı görmüyorsanız, projeyi derlediğinizden emin olun.) Ardından "+" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="d81cd-165">**Yeni veri bağlamı** Iletişim kutusunda **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="d81cd-166">**Denetleyici Ekle** Iletişim kutusunda **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="d81cd-167">Scafkatlama, API denetleyicisini tanımlayan adlı bir sınıf ekler `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="d81cd-168">Ayrıca `BooksAPIContext` , Entity Framework için veri bağlamını tanımlayan modeller klasörüne adlı bir sınıfı ekler.</span><span class="sxs-lookup"><span data-stu-id="d81cd-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="d81cd-169">Veritabanının Çekirdeğini Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d81cd-169">Seed the Database</span></span>

<span data-ttu-id="d81cd-170">Araçlar menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="d81cd-171">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="d81cd-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="d81cd-172">Bu komut bir geçişler klasörü oluşturur ve Configuration.cs adlı yeni bir kod dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="d81cd-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="d81cd-173">Bu dosyayı açın ve yöntemine aşağıdaki kodu ekleyin `Configuration.Seed` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="d81cd-174">Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="d81cd-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="d81cd-175">Bu komutlar yerel bir veritabanı oluşturur ve veritabanını doldurmak için çekirdek yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="d81cd-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="d81cd-176">DTO sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="d81cd-176">Add DTO Classes</span></span>

<span data-ttu-id="d81cd-177">Uygulamayı şimdi çalıştırırsanız ve/api/Books/1 öğesine bir GET isteği gönderirseniz, yanıt aşağıdakine benzer şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="d81cd-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="d81cd-178">(Okunabilirlik için girinti ekledim.)</span><span class="sxs-lookup"><span data-stu-id="d81cd-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="d81cd-179">Bunun yerine, bu isteğin, alanların bir alt kümesini döndürmesini istiyorum.</span><span class="sxs-lookup"><span data-stu-id="d81cd-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="d81cd-180">Ayrıca, yazar KIMLIĞI yerine yazarın adını döndürmesini istiyorum.</span><span class="sxs-lookup"><span data-stu-id="d81cd-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="d81cd-181">Bunu gerçekleştirmek için, denetleyici yöntemlerini EF modeli yerine bir *veri aktarımı nesnesi* (DTO) döndürecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="d81cd-182">Bir DTO yalnızca verileri taşımak için tasarlanan bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="d81cd-183">Çözüm Gezgini, projeye sağ tıklayın ve **Add**  |  **Yeni klasör**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="d81cd-184">&quot;DTOS klasörünü adlandırın &quot; .</span><span class="sxs-lookup"><span data-stu-id="d81cd-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="d81cd-185">`BookDto`Aşağıdaki tanıma sahip DTOs klasörüne adlı bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d81cd-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="d81cd-186">Adlı başka bir sınıf ekleyin `BookDetailDto` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="d81cd-187">Sonra, `BooksController` örnekleri döndürecek şekilde sınıfı güncelleştirin `BookDto` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="d81cd-188">Örneklere örnek olarak proje örnekleri eklemek için [sorgulanabilir. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) yöntemini kullanacağız `Book` `BookDto` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="d81cd-189">Controller sınıfının güncelleştirilmiş kodu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="d81cd-190">`PutBook`, `PostBook` Ve yöntemlerini sildim, `DeleteBook` çünkü bu öğretici için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="d81cd-191">Şimdi uygulamayı çalıştırırsanız ve/api/Books/1 isteğinde bulunursa yanıt gövdesi şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d81cd-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="d81cd-192">Rota öznitelikleri Ekle</span><span class="sxs-lookup"><span data-stu-id="d81cd-192">Add Route Attributes</span></span>

<span data-ttu-id="d81cd-193">Ardından, denetleyiciyi öznitelik yönlendirmeyi kullanacak şekilde dönüştürüyoruz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="d81cd-194">İlk olarak, denetleyiciye bir **Routeprefix** özniteliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="d81cd-195">Bu öznitelik, bu denetleyicideki tüm yöntemler için ilk URI segmentlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d81cd-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="d81cd-196">Ardından aşağıdaki gibi, denetleyici eylemlerine **[Route]** öznitelikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d81cd-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="d81cd-197">Her bir Controller yöntemi için yol şablonu, önek artı **yol** özniteliğinde belirtilen dizedir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="d81cd-198">Yöntemi için `GetBook` yol şablonu, &quot; &quot; URI segmentinin bir tamsayı değer içermesi durumunda eşleşen parametre parametreli {ID: int} dizesini içerir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="d81cd-199">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d81cd-199">Method</span></span> | <span data-ttu-id="d81cd-200">Rota şablonu</span><span class="sxs-lookup"><span data-stu-id="d81cd-200">Route Template</span></span> | <span data-ttu-id="d81cd-201">Örnek URI</span><span class="sxs-lookup"><span data-stu-id="d81cd-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="d81cd-202">"API/Kitaplar"</span><span class="sxs-lookup"><span data-stu-id="d81cd-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="d81cd-203">"API/kitaplar/{id: int}"</span><span class="sxs-lookup"><span data-stu-id="d81cd-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="d81cd-204">Kitap ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="d81cd-204">Get Book Details</span></span>

<span data-ttu-id="d81cd-205">Kitap ayrıntılarını almak için, istemci öğesine bir GET isteği gönderir `/api/books/{id}/details` ; burada *{id}* , kitabın kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="d81cd-206">Sınıfına aşağıdaki yöntemi ekleyin `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="d81cd-207">İstek yaptıysanız `/api/books/1/details` Yanıt şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d81cd-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="d81cd-208">Türe göre kitap al</span><span class="sxs-lookup"><span data-stu-id="d81cd-208">Get Books By Genre</span></span>

<span data-ttu-id="d81cd-209">Belirli bir tarz kitap listesini almak için, istemci öğesine bir GET isteği gönderir `/api/books/genre` , burada *tarz* tarz adıdır.</span><span class="sxs-lookup"><span data-stu-id="d81cd-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="d81cd-210">(Örneğin, `/api/books/fantasy` .)</span><span class="sxs-lookup"><span data-stu-id="d81cd-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="d81cd-211">Aşağıdaki yöntemi öğesine ekleyin `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="d81cd-212">Burada URI şablonunda bir {tarzı} parametresi içeren bir yol tanımlanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="d81cd-213">Web API 'sinin bu iki URI 'yi ayırt edebildiğine ve bunları farklı yöntemlere yönlendirdiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d81cd-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="d81cd-214">Bunun nedeni, `GetBook` yöntemi "ID" segmentinin bir tamsayı değeri olması gereken bir kısıtlama içerir:</span><span class="sxs-lookup"><span data-stu-id="d81cd-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="d81cd-215">/Api/Books/FI isteğinde karşılaşırsanız, yanıt şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d81cd-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="d81cd-216">Yazara göre kitaplar alın</span><span class="sxs-lookup"><span data-stu-id="d81cd-216">Get Books By Author</span></span>

<span data-ttu-id="d81cd-217">Belirli bir yazarın kitaplarının listesini almak için, istemci öğesine bir GET isteği gönderir `/api/authors/id/books` ; burada *KIMLIK* yazarın kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="d81cd-218">Aşağıdaki yöntemi öğesine ekleyin `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="d81cd-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="d81cd-219">Bu örnek, &quot; kitaplar &quot; yazarların bir alt kaynağını kabul ettiğinden ilgi çekici bir örnektir &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="d81cd-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="d81cd-220">Bu model, yeniden gerçekleştirilen API 'lerde oldukça yaygındır.</span><span class="sxs-lookup"><span data-stu-id="d81cd-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="d81cd-221">Yol şablonundaki tilde (~), **routeprefix** özniteliğinde rota önekini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="d81cd-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="d81cd-222">Yayın tarihine göre kitap al</span><span class="sxs-lookup"><span data-stu-id="d81cd-222">Get Books By Publication Date</span></span>

<span data-ttu-id="d81cd-223">Yayın tarihine göre Kitaplar listesini almak için, istemci öğesine bir GET isteği gönderir `/api/books/date/yyyy-mm-dd` ; burada *yyyy-aa-gg* tarih olur.</span><span class="sxs-lookup"><span data-stu-id="d81cd-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="d81cd-224">Bunu yapmanın bir yolu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d81cd-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="d81cd-225">`{pubdate:datetime}`Parametresi bir **Tarih saat** değeriyle eşleşecek şekilde kısıtlanıyor.</span><span class="sxs-lookup"><span data-stu-id="d81cd-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="d81cd-226">Bu işe yarar, ancak beğenmekten daha fazla izin veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="d81cd-227">Örneğin, bu URI 'Ler rotayla de eşleşir:</span><span class="sxs-lookup"><span data-stu-id="d81cd-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="d81cd-228">Bu URI 'Lere izin veren bir sorun yok.</span><span class="sxs-lookup"><span data-stu-id="d81cd-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="d81cd-229">Ancak, yol şablonuna normal ifade kısıtlaması ekleyerek yolu belirli bir biçimle kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d81cd-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="d81cd-230">Şimdi yalnızca &quot; YYYY-AA-GG biçiminde olan tarihler &quot; eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="d81cd-231">Gerçek bir tarih olduğunu doğrulamak için Regex kullandığımıza dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d81cd-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="d81cd-232">Web API 'SI, URI segmentini bir **DateTime** örneğine dönüştürmeye çalıştığında işlenir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="d81cd-233">' 2012-47-99 ' gibi geçersiz bir tarih dönüştürülemeyecek ve istemci 404 hatası alacak.</span><span class="sxs-lookup"><span data-stu-id="d81cd-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="d81cd-234">Ayrıca, `/api/books/date/yyyy/mm/dd` farklı bir Regex ile başka bir **[Route]** özniteliği ekleyerek eğik çizgi ayırıcısını () de destekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d81cd-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="d81cd-235">Burada hafif ancak önemli bir ayrıntı vardır.</span><span class="sxs-lookup"><span data-stu-id="d81cd-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="d81cd-236">İkinci yol şablonunda \* {pubdate} parametresinin başlangıcında bir joker karakter () vardır:</span><span class="sxs-lookup"><span data-stu-id="d81cd-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="d81cd-237">Bu, yönlendirme altyapısına {pubdate} uygulamasının URI 'nin geri kalanı ile eşleştiğinden emin olduğunu söyler.</span><span class="sxs-lookup"><span data-stu-id="d81cd-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="d81cd-238">Varsayılan olarak, bir şablon parametresi tek bir URI segmentiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="d81cd-239">Bu durumda, {pubdate} ' nin birkaç URI kesimini yaymasına istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="d81cd-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="d81cd-240">Denetleyici kodu</span><span class="sxs-lookup"><span data-stu-id="d81cd-240">Controller Code</span></span>

<span data-ttu-id="d81cd-241">BooksController sınıfının tüm kodu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d81cd-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="d81cd-242">Özet</span><span class="sxs-lookup"><span data-stu-id="d81cd-242">Summary</span></span>

<span data-ttu-id="d81cd-243">Öznitelik yönlendirme API 'niz için URI 'Leri tasarlarken daha fazla denetim ve daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d81cd-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
