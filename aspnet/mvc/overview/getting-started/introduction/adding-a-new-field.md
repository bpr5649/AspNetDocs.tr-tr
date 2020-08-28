---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: Yeni alan ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045149"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="b4d9e-102">Yeni Alan Ekleme</span><span class="sxs-lookup"><span data-stu-id="b4d9e-102">Adding a New Field</span></span>

<span data-ttu-id="b4d9e-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="b4d9e-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="b4d9e-104">Bu bölümde, değişikliğin veritabanına uygulanması için model sınıflarında bazı değişiklikleri geçirmek üzere Entity Framework Code First Migrations kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="b4d9e-105">Varsayılan olarak, bu öğreticide yaptığınız gibi, otomatik olarak bir veritabanı oluşturmak için Entity Framework Code First kullandığınızda Code First veritabanının şemasının oluşturulduğu model sınıflarıyla eşitlenmiş olup olmadığını izlemeye yardımcı olmak üzere veritabanına tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="b4d9e-106">Eşitlenmiyorsa Entity Framework bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="b4d9e-107">Bu durum, çalışma zamanında yalnızca (hataları gizleyerek) bulabileceğiniz geliştirme zamanında sorunları izlemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="b4d9e-108">Model değişiklikleri için Code First Migrations ayarlama</span><span class="sxs-lookup"><span data-stu-id="b4d9e-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="b4d9e-109">Çözüm Gezgini gidin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="b4d9e-110">Filmler veritabanını kaldırmak için *filmler. mdf* dosyasına sağ tıklayın ve **Sil** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="b4d9e-111">*Filmler. mdf* dosyasını görmüyorsanız, kırmızı anahatta aşağıda gösterilen **tüm dosyaları göster** simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="b4d9e-112">Hata olmadığından emin olmak için uygulamayı derleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="b4d9e-113">**Araçlar** menüsünden **NuGet Paket Yöneticisi**’ne ve ardından **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Paket Man 'ı Ekle](adding-a-new-field/_static/image2.png)

<span data-ttu-id="b4d9e-115">**Paket Yöneticisi konsol** penceresinde, `PM>` isteminde şunu girin:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="b4d9e-116">Enable-geçişler-ContextTypeName MvcMovie. modeller. MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="b4d9e-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="b4d9e-117">**Enable-geçişler** komutu (yukarıda gösterilmiştir) yeni bir *geçişler* klasöründe bir *Configuration.cs* dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="b4d9e-118">Visual Studio, *Configuration.cs* dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="b4d9e-119">`Seed` *Configuration.cs* dosyasındaki yöntemi aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="b4d9e-120">Altındaki kırmızı dalgalı çizginin üzerine gelin `Movie` ve `Show Potential Fixes` ardından **Mvcmovie. modellerini** **kullanma** ' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="b4d9e-121">Bunun yapılması Aşağıdaki using ifadesini ekler:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="b4d9e-122">Code First Migrations `Seed` her geçişten sonra (yani, Package Manager konsolunda **Update-Database** ' i çağırarak) yöntemi çağırır ve bu yöntem zaten eklenmiş olan satırları güncelleştirir veya henüz yoksa onları ekler.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="b4d9e-123">Aşağıdaki koddaki [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemi "upsert" bir işlem gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="b4d9e-124">[Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemi her geçişte çalıştığı için, eklemeye çalıştığınız satırlar veritabanını oluşturan ilk geçişten sonra zaten mevcut olacağı için yalnızca verileri ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="b4d9e-125">"[Upsert](http://en.wikipedia.org/wiki/Upsert)" işlemi, zaten var olan bir satır eklemeye çalışırsanız, ancak uygulamayı test ederken yapmış olduğunuz verilerde yapılan değişiklikleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="b4d9e-126">Bazı tablolardaki test verileri ile bu durum oluşmasını istemeyebilirsiniz: bazı durumlarda verileri değiştirirken değişiklikler veritabanı güncelleştirmelerinden sonra kalmasını istiyor.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="b4d9e-127">Bu durumda, bir koşullu ekleme işlemi yapmak istiyorsanız, yalnızca mevcut değilse bir satır ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="b4d9e-128">[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) metoduna geçirilen ilk parametre, bir satırın zaten var olup olmadığını denetlemek için kullanılacak özelliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="b4d9e-129">Sağlanan test filmi verileri için, `Title` listedeki her bir başlık benzersiz olduğundan bu amaçla özellik kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="b4d9e-130">Bu kod, başlıkların benzersiz olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="b4d9e-131">El ile yinelenen bir başlık eklerseniz, bir sonraki sefer geçiş işlemi yaptığınızda aşağıdaki özel durumu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="b4d9e-132">*Sıra birden fazla öğe içeriyor*</span><span class="sxs-lookup"><span data-stu-id="b4d9e-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="b4d9e-133">[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemi hakkında daha fazla bilgi için, bkz. [EF 4,3 AddOrUpdate yöntemiyle dikkatli](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)olmak.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="b4d9e-134">**Projeyi derlemek IÇIN CTRL-SHIFT-B tuşlarına basın.** (Bu noktada derleme yapmazsanız aşağıdaki adımlar başarısız olur.)</span><span class="sxs-lookup"><span data-stu-id="b4d9e-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="b4d9e-135">Sonraki adım, `DbMigration` ilk geçiş için bir sınıf oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="b4d9e-136">Bu geçiş yeni bir veritabanı oluşturur. bu nedenle, önceki bir adımda bulunan *Movie. mdf* dosyasını silmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="b4d9e-137">**Paket Yöneticisi konsolu** penceresinde, `add-migration Initial` ilk geçişi oluşturmak için komutunu girin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="b4d9e-138">"Initial" adı rasgele olur ve oluşturulan geçiş dosyasını adlandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="b4d9e-139">Code First Migrations *geçişler* klasöründe başka bir sınıf dosyası oluşturur ( *{datestamp} \_ Initial.cs* adıyla) ve bu sınıf veritabanı şemasını oluşturan kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="b4d9e-140">Geçiş dosya adı, sıralamaya yardımcı olması için zaman damgasıyla önceden düzeltilir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="b4d9e-141">*{DateStamp} \_ Initial.cs* dosyasını Inceleyerek, `Movies` film DB için tablo oluşturma yönergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="b4d9e-142">Aşağıdaki yönergelerdeki veritabanını güncelleştirdiğinizde, bu *{dateStamp} \_ Initial.cs* dosyası çalışacaktır ve DB şemasını oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="b4d9e-143">Ardından, VERITABANıNı test verileriyle doldurmak için **çekirdek** yöntemi çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="b4d9e-144">**Paket Yöneticisi konsolunda**, `update-database` veritabanını oluşturmak ve metodunu çalıştırmak için komutunu girin `Seed` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="b4d9e-145">Bir tablonun zaten var olduğunu ve oluşturulamayabileceğini belirten bir hata alırsanız, veritabanını sildikten ve çalıştırmadan önce uygulamayı çalıştırmanızdan kaynaklanıyor olabilirsiniz `update-database` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="b4d9e-146">Bu durumda, *filmler. mdf* dosyasını yeniden silin ve komutu yeniden deneyin `update-database` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="b4d9e-147">Yine de bir hata alırsanız, geçişler klasörünü ve içeriğini silin ve ardından bu sayfanın üst kısmındaki yönergelerden başlayın (yani, *filmler. mdf* dosyasını silin ve ardından geçişlere devam edin).</span><span class="sxs-lookup"><span data-stu-id="b4d9e-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="b4d9e-148">Hala bir hata alırsanız, SQL Server Nesne Gezgini açın ve veritabanını listeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="b4d9e-149">Uygulamayı çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="b4d9e-150">Çekirdek veriler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="b4d9e-151">Film modeline bir derecelendirme özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="b4d9e-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="b4d9e-152">Yeni bir `Rating` özelliği var olan sınıfa ekleyerek başlayın `Movie` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="b4d9e-153">*Models\movie.cs* dosyasını açın ve `Rating` Şu şekilde bir özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="b4d9e-154">Tüm `Movie` sınıf artık aşağıdaki kod gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="b4d9e-155">Uygulamayı derleyin (Ctrl + Shift + B).</span><span class="sxs-lookup"><span data-stu-id="b4d9e-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="b4d9e-156">Sınıfa yeni bir alan eklediyseniz `Movie` , bu yeni özelliğin dahil edilmesini sağlamak için bağlama *beyaz listesini* de güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="b4d9e-157">`bind` `Create` Ve eylem yöntemlerine ait özniteliği `Edit` Özelliği içerecek şekilde güncelleştirin `Rating` :</span><span class="sxs-lookup"><span data-stu-id="b4d9e-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="b4d9e-158">Ayrıca, tarayıcı görünümündeki yeni özelliği görüntülemek, oluşturmak ve düzenlemek için görünüm şablonlarını güncelleştirmeniz gerekir `Rating` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="b4d9e-159">*\Views\Movies\Index.cshtml* dosyasını açın ve `<th>Rating</th>` **Fiyat** sütunundan hemen sonra bir sütun başlığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="b4d9e-160">Sonra `<td>` değeri işlemek için şablonun sonuna yakın bir sütun ekleyin `@item.Rating` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="b4d9e-161">Güncelleştirilmiş *Index. cshtml* görünüm şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="b4d9e-162">Sonra, *\Views\Movies\Create.cshtml* dosyasını açın ve `Rating` aşağıdaki vurgulanmış işaretlerle alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="b4d9e-163">Bu, yeni bir film oluşturulduğunda bir derecelendirme belirleyebilmeniz için bir metin kutusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="b4d9e-164">Artık yeni özelliği desteklemek için uygulama kodunu güncelleştirdiniz `Rating` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="b4d9e-165">Uygulamayı çalıştırın ve */filmler* URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="b4d9e-166">Bunu yaptığınızda, aşağıdaki hatalardan birini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="b4d9e-167">' MovieDBContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="b4d9e-168">Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün ( https://go.microsoft.com/fwlink/?LinkId=238269) .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="b4d9e-169">Bu hatayı `Movie` , uygulamadaki güncelleştirilmiş model sınıfı artık mevcut veritabanının tablosunun şemasından farklı olduğu için görüyorsunuz `Movie` .</span><span class="sxs-lookup"><span data-stu-id="b4d9e-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="b4d9e-170">( `Rating` Veritabanı tablosunda sütun yok.)</span><span class="sxs-lookup"><span data-stu-id="b4d9e-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="b4d9e-171">Hatayı çözmek için birkaç yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="b4d9e-172">Entity Framework yeni model sınıfı şemasına göre otomatik olarak veritabanını bırakıp yeniden oluşturmayı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="b4d9e-173">Bu yaklaşım, bir test veritabanı üzerinde etkin geliştirme yaparken geliştirme döngüsünün başlarında çok daha kolay. modeli ve veritabanı şemasını birlikte hızla gelişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="b4d9e-174">Bunun yanında, bu yaklaşımı bir üretim veritabanında *kullanmak istemezsiniz,* ancak bu, veritabanında var olan verileri kaybetmeniz olur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="b4d9e-175">Bir veritabanının test verileriyle otomatik olarak çekirdeği oluşturmak için bir başlatıcı kullanılması, genellikle bir uygulama geliştirmenin üretken bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="b4d9e-176">Entity Framework veritabanı başlatıcıları hakkında daha fazla bilgi için bkz. [ASP.NET MVC/Entity Framework öğreticisi](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="b4d9e-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="b4d9e-177">Mevcut veritabanının şemasını model sınıflarıyla eşleşecek şekilde açıkça değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="b4d9e-178">Bu yaklaşımın avantajı, verilerinizi tutmanızı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="b4d9e-179">Bu değişikliği el ile ya da bir veritabanı değişiklik betiği oluşturarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="b4d9e-180">Veritabanı şemasını güncelleştirmek için Code First Migrations kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="b4d9e-181">Bu öğretici için Code First Migrations kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="b4d9e-182">Çekirdek yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="b4d9e-183">Migrations\Configuration.cs dosyasını açın ve her bir film nesnesine bir derecelendirme alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="b4d9e-184">Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="b4d9e-185">Bu `add-migration` komut, geçiş çerçevesinin geçerli film modelini geçerli fılm DB şemasıyla incelemesini ve veritabanını yeni modele geçirmek için gerekli kodu oluşturmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="b4d9e-186">Ad *derecelendirmesi* rasgele ve geçiş dosyasını adlandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="b4d9e-187">Geçiş adımı için anlamlı bir ad kullanılması yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="b4d9e-188">Bu komut tamamlandığında, Visual Studio yeni türetilmiş sınıfı tanımlayan sınıf dosyasını açar `DbMigration` ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="b4d9e-189">Çözümü oluşturun ve ardından `update-database` **Paket Yöneticisi konsolu** penceresine komutu girin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="b4d9e-190">Aşağıdaki görüntüde, **Paket Yöneticisi konsol** penceresinde çıkış gösterilmektedir (Tarih damgası ön bekleyen *Derecelendirme* farklı olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="b4d9e-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="b4d9e-191">Uygulamayı yeniden çalıştırın ve/filmler URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="b4d9e-192">Yeni derecelendirme alanını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="b4d9e-193">Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="b4d9e-194">Bir derecelendirme ekleyebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="b4d9e-196">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-196">Click **Create**.</span></span> <span data-ttu-id="b4d9e-197">Yeni film, derecelendirme de dahil, artık filmler listesinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="b4d9e-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="b4d9e-199">Artık proje geçişleri kullanıyor olduğuna göre, yeni bir alan eklediğinizde veya şemayı güncelleştirdiğinizde veritabanını bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="b4d9e-200">Sonraki bölümde, daha fazla şema değişikliği yapacağız ve veritabanını güncelleştirmek için geçişleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="b4d9e-201">Ayrıca `Rating` alanı düzenleme, Ayrıntılar ve Sil görünüm şablonlarına de eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="b4d9e-202">**Paket Yöneticisi konsol** penceresinde "Güncelleştir-veritabanı" komutunu tekrar girebilir ve şema modelle eşleştiğinden geçiş kodu çalıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="b4d9e-203">Bununla birlikte, "Update-Database" çalıştırmak `Seed` yöntemi yeniden çalıştırır ve çekirdek verilerinden herhangi birini değiştirdiyseniz, bu değişiklikler kaybedilir çünkü bu `Seed` Yöntem verileri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="b4d9e-204">`Seed`Tom Dykstra 'in popüler [ASP.NET MVC/Entity Framework öğreticisindeki](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)yöntemi hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="b4d9e-205">Bu bölümde, model nesnelerini nasıl değiştirebileceğiniz ve veritabanını değişikliklerle eşitlenmiş halde tutan bir şekilde gördünüz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="b4d9e-206">Ayrıca, senaryoları deneyebilmeniz için yeni oluşturulan bir veritabanını örnek verilerle doldurmanın bir yolunu öğrenmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="b4d9e-207">Bu yalnızca Code First hızlı bir giriştir, konu hakkında daha kapsamlı bir öğretici için [ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="b4d9e-208">Daha sonra model sınıflarına daha zengin doğrulama mantığı ekleme ve bazı iş kurallarının uygulanmasını sağlama konusuna bakalım.</span><span class="sxs-lookup"><span data-stu-id="b4d9e-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b4d9e-209">[Önceki](adding-search.md) 
>  [Sonraki](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="b4d9e-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
