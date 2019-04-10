---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: (VB) veritabanı verilerinin tablosunu görüntüleme | Microsoft Docs
author: microsoft
description: Bu öğreticide, ı veritabanı kayıt kümesini görüntülemek için iki yöntem göstermektedir. Ben bir HTML veritabanı kayıt kümesini veri biçimlendirme için iki yöntem göster...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: c33812ab9d758c3155a2f75f59bfb63c55487dc7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59396414"
---
# <a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="3e10e-104">Veritabanı Verilerinin Tablosunu Görüntüleme (VB)</span><span class="sxs-lookup"><span data-stu-id="3e10e-104">Displaying a Table of Database Data (VB)</span></span>

<span data-ttu-id="3e10e-105">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3e10e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3e10e-106">PDF'yi indirin</span><span class="sxs-lookup"><span data-stu-id="3e10e-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="3e10e-107">Bu öğreticide, ı veritabanı kayıt kümesini görüntülemek için iki yöntem göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="3e10e-108">Ben bir HTML tablosu veritabanı kayıtları bir dizi biçimlendirme için iki yöntem gösterir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="3e10e-109">İlk olarak, doğrudan bir görünüm içindeki veritabanı kayıtlarını nasıl biçimlendirebilirsiniz ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="3e10e-110">Ardından, ben nasıl veritabanı kayıtlarını biçimlendirilirken kısmi avantajlarından yararlanabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>


<span data-ttu-id="3e10e-111">Bu öğreticide bir ASP.NET MVC uygulamasındaki HTML tablosu veritabanı verilerinin nasıl görüntüleyebilir açıklamak için hedefidir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="3e10e-112">İlk olarak, bir kayıt kümesi otomatik olarak görüntüleyen bir görünüm oluşturmak için Visual Studio'ya dahil olan yapı iskelesi araçları kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="3e10e-113">Ardından, kısmi bir şablon olarak veritabanı kayıtlarını biçimlendirilirken kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="3e10e-114">Model sınıfları oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e10e-114">Create the Model Classes</span></span>

<span data-ttu-id="3e10e-115">Film veritabanı tablosundan kayıt kümesini görüntülemek için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3e10e-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="3e10e-116">Film veritabanı tablo şu sütunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3e10e-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>


| **<span data-ttu-id="3e10e-117">Sütun adı</span><span class="sxs-lookup"><span data-stu-id="3e10e-117">Column Name</span></span>** | **<span data-ttu-id="3e10e-118">Veri Türü</span><span class="sxs-lookup"><span data-stu-id="3e10e-118">Data Type</span></span>** | **<span data-ttu-id="3e10e-119">Null değerlere izin ver</span><span class="sxs-lookup"><span data-stu-id="3e10e-119">Allow Nulls</span></span>** |
| --- | --- | --- |
| <span data-ttu-id="3e10e-120">Kimliği</span><span class="sxs-lookup"><span data-stu-id="3e10e-120">Id</span></span> | <span data-ttu-id="3e10e-121">int</span><span class="sxs-lookup"><span data-stu-id="3e10e-121">Int</span></span> | <span data-ttu-id="3e10e-122">False</span><span class="sxs-lookup"><span data-stu-id="3e10e-122">False</span></span> |
| <span data-ttu-id="3e10e-123">Başlık</span><span class="sxs-lookup"><span data-stu-id="3e10e-123">Title</span></span> | <span data-ttu-id="3e10e-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="3e10e-124">Nvarchar(200)</span></span> | <span data-ttu-id="3e10e-125">False</span><span class="sxs-lookup"><span data-stu-id="3e10e-125">False</span></span> |
| <span data-ttu-id="3e10e-126">Direktörü</span><span class="sxs-lookup"><span data-stu-id="3e10e-126">Director</span></span> | <span data-ttu-id="3e10e-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="3e10e-127">NVarchar(50)</span></span> | <span data-ttu-id="3e10e-128">False</span><span class="sxs-lookup"><span data-stu-id="3e10e-128">False</span></span> |
| <span data-ttu-id="3e10e-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="3e10e-129">DateReleased</span></span> | <span data-ttu-id="3e10e-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="3e10e-130">DateTime</span></span> | <span data-ttu-id="3e10e-131">False</span><span class="sxs-lookup"><span data-stu-id="3e10e-131">False</span></span> |


<span data-ttu-id="3e10e-132">ASP.NET MVC uygulamamıza filmler tablosunda göstermek için bir model sınıfı oluşturmak ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="3e10e-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="3e10e-133">Bu öğreticide, bizim model sınıfları oluşturmak için Microsoft Entity Framework kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e10e-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3e10e-134">Bu öğreticide, Microsoft Entity Framework kullanırız.</span><span class="sxs-lookup"><span data-stu-id="3e10e-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="3e10e-135">Ancak, bir veritabanından LINQ to SQL veya NHibernate ADO.NET dahil olmak üzere bir ASP.NET MVC uygulaması ile etkileşim kurmak için çeşitli farklı teknolojiler kullanabileceğinizi anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>


<span data-ttu-id="3e10e-136">Varlık veri modeli Sihirbazı başlatmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3e10e-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="3e10e-137">Çözüm Gezgini penceresinde ve menü seçeneğini seçin modelleri klasörünü sağ tıklatın **Ekle, yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="3e10e-138">Seçin **veri** kategori seçip alt **ADO.NET varlık veri modeli** şablonu.</span><span class="sxs-lookup"><span data-stu-id="3e10e-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="3e10e-139">Veri modelinizi adını verin *MoviesDBModel.edmx* tıklatıp **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e10e-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="3e10e-140">Ekle düğmesine tıkladıktan sonra (bkz. Şekil 1) varlık veri modeli Sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="3e10e-141">Sihirbazı tamamlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3e10e-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="3e10e-142">İçinde **Choose Model Contents** adım, select **veritabanından Oluştur** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3e10e-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="3e10e-143">İçinde **veri bağlantınızı seçin** adım, kullanın *MoviesDB.mdf* veri bağlantısı ve ad *MoviesDBEntities* bağlantı ayarları için.</span><span class="sxs-lookup"><span data-stu-id="3e10e-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="3e10e-144">Tıklayın **sonraki** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e10e-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="3e10e-145">İçinde **veritabanı nesnelerinizi seçin** adım, tablolar düğümünü genişletin, filmler tabloyu seçin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="3e10e-146">Ad alanı girin *modelleri* tıklatıp **son** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e10e-146">Enter the namespace *Models* and click the **Finish** button.</span></span>


[![C<span data-ttu-id="3e10e-147">LINQ to SQL sınıfları reating]</span><span class="sxs-lookup"><span data-stu-id="3e10e-147">reating LINQ to SQL classes]</span></span>(displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

<span data-ttu-id="3e10e-148">**Şekil 01**: SQL sınıflarına LINQ oluşturma ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>


<span data-ttu-id="3e10e-149">Varlık veri modeli Sihirbazı tamamladıktan sonra varlık veri modeli Tasarımcısı açılır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="3e10e-150">Tasarımcı filmler varlık görüntülenmesi gerekir (bkz: Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="3e10e-150">The Designer should display the Movies entity (see Figure 2).</span></span>


[![T<span data-ttu-id="3e10e-151">He varlık veri modeli Tasarımcısı]</span><span class="sxs-lookup"><span data-stu-id="3e10e-151">he Entity Data Model Designer]</span></span>(displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

<span data-ttu-id="3e10e-152">**Şekil 02**: Varlık veri modeli Tasarımcısı ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>


<span data-ttu-id="3e10e-153">Biz devam etmeden önce bir değişiklik yapmak ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="3e10e-153">We need to make one change before we continue.</span></span> <span data-ttu-id="3e10e-154">Varlık veri Sihirbazı adlı bir model sınıfı oluşturur *filmler* film veritabanı tablosunu temsil eden.</span><span class="sxs-lookup"><span data-stu-id="3e10e-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="3e10e-155">Filmler sınıfı belirli bir filmi temsil etmek için kullanacağız çünkü olması için sınıfın adını değiştirmek ihtiyacımız *film* yerine *filmler* (tekil yerine çoğul).</span><span class="sxs-lookup"><span data-stu-id="3e10e-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="3e10e-156">Tasarımcı yüzeyinde sınıf adına çift tıklayın ve sınıfın adını film film değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="3e10e-157">Bu değişikliği yaptıktan sonra tıklayın **Kaydet** (disket simgesi) düğmesine film sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e10e-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="3e10e-158">Denetleyici filmler oluşturun</span><span class="sxs-lookup"><span data-stu-id="3e10e-158">Create the Movies Controller</span></span>

<span data-ttu-id="3e10e-159">Veritabanı Kayıtlarımız temsil etmek için bir yolunu sunuyoruz, bir denetleyici filmler koleksiyonunu döndürür oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="3e10e-160">Visual Studio Çözüm Gezgini penceresinde denetleyicileri klasörü sağ tıklatın ve menü seçeneğini **Ekle, denetleyici** (bkz: Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="3e10e-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>


[![T<span data-ttu-id="3e10e-161">He ekleme denetleyicisi menüsü]</span><span class="sxs-lookup"><span data-stu-id="3e10e-161">he Add Controller Menu]</span></span>(displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

<span data-ttu-id="3e10e-162">**Şekil 03**: Denetleyici menü Ekle ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>


<span data-ttu-id="3e10e-163">Zaman **denetleyici Ekle** iletişim kutusu açılır, denetleyici adı MovieController girin (bkz: Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="3e10e-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="3e10e-164">Tıklayın **Ekle** düğmesini yeni denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-164">Click the **Add** button to add the new controller.</span></span>


[![T<span data-ttu-id="3e10e-165">He denetleyici Ekle iletişim kutusu]</span><span class="sxs-lookup"><span data-stu-id="3e10e-165">he Add Controller dialog]</span></span>(displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

<span data-ttu-id="3e10e-166">**Şekil 04**: Denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>


<span data-ttu-id="3e10e-167">Biz, böylece veritabanı kayıt kümesini döndürür film denetleyici tarafından kullanıma sunulan İNDİS() eylem değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="3e10e-168">Denetleyici Denetleyici 1 listeleme benzer şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

**<span data-ttu-id="3e10e-169">Listing 1 – Controllers\MovieController.vb</span><span class="sxs-lookup"><span data-stu-id="3e10e-169">Listing 1 – Controllers\MovieController.vb</span></span>**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="3e10e-170">Listeleme 1'de MoviesDBEntities sınıfı MoviesDB veritabanı temsil etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="3e10e-171">İfade *varlıklar. MovieSet.ToList()* film veritabanı tablosundan tüm filmlere kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3e10e-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="3e10e-172">Görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e10e-172">Create the View</span></span>

<span data-ttu-id="3e10e-173">HTML tablosu halinde veritabanı kayıt kümesini görüntülemek için en kolay yolu, Visual Studio tarafından sağlanan yapı iskelesi yararlanmak sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="3e10e-174">Menü seçeneği seçerek uygulamanızı **yapı, yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="3e10e-175">Uygulamanızı açmadan önce derlemelidir **Görünüm Ekle** iletişim kutusu veya veri sınıflarınızı iletişim kutusunda görünmez.</span><span class="sxs-lookup"><span data-stu-id="3e10e-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="3e10e-176">Menü seçeneği İNDİS() eylem sağ tıklayıp **Görünüm Ekle** (bkz: Şekil 5).</span><span class="sxs-lookup"><span data-stu-id="3e10e-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>


[![A<span data-ttu-id="3e10e-177">bir görünüm dding]</span><span class="sxs-lookup"><span data-stu-id="3e10e-177">dding a view]</span></span>(displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

<span data-ttu-id="3e10e-178">**Şekil 05**: Görünüm ekleme ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>


<span data-ttu-id="3e10e-179">İçinde **Görünüm Ekle** iletişim kutusunda etiketli onay **kesin türü belirtilmiş görünüm oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="3e10e-180">Film sınıfı olarak seçin **görüntülemek veri sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="3e10e-181">Seçin *listesi* olarak **içeriği görüntüle** (bkz. Şekil 6).</span><span class="sxs-lookup"><span data-stu-id="3e10e-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="3e10e-182">Bu seçenekleri filmler listesini görüntüleyen bir kesin türü belirtilmiş görünüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3e10e-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>


[![T<span data-ttu-id="3e10e-183">He Görünüm Ekle iletişim kutusu]</span><span class="sxs-lookup"><span data-stu-id="3e10e-183">he Add View dialog]</span></span>(displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

<span data-ttu-id="3e10e-184">**Şekil 06**: Görünüm Ekle iletişim kutusu ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>


<span data-ttu-id="3e10e-185">Tıkladıktan sonra **Ekle** 2 liste görünümünde düğme otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3e10e-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="3e10e-186">Bu görünüm, her bir filmi özelliklerini görüntüler ve filmler toplulukta tekrarlama için gerekli kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

**<span data-ttu-id="3e10e-187">2 – Views\Movie\Index.aspx listeleme</span><span class="sxs-lookup"><span data-stu-id="3e10e-187">Listing 2 – Views\Movie\Index.aspx</span></span>**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="3e10e-188">Menü seçeneğini belirleyerek uygulamayı çalıştırabilirsiniz **hata ayıklama, hata ayıklamayı Başlat** (veya F5 tuşuna basarak).</span><span class="sxs-lookup"><span data-stu-id="3e10e-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="3e10e-189">Uygulamayı çalıştıran, Internet Explorer başlatır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="3e10e-190">Ardından /Movie URL'sine gidin, Şekil 7'de bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>


[![A <span data-ttu-id="3e10e-191">Tablo film]</span><span class="sxs-lookup"><span data-stu-id="3e10e-191">table of movies]</span></span>(displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

<span data-ttu-id="3e10e-192">**Şekil 07**: Filmler tablosu ([tam boyutlu görüntüyü görmek için tıklatın](displaying-a-table-of-database-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="3e10e-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>


<span data-ttu-id="3e10e-193">Şekil 7'de veritabanı kayıtlarını kılavuz görünümünü ilgili hiçbir şeyi beğenmezseniz dizin görünümünün yalnızca değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="3e10e-194">Örneğin, değiştirebileceğiniz *DateReleased* başlığına *yayımlanma tarihi* dizin görünümünün değiştirerek.</span><span class="sxs-lookup"><span data-stu-id="3e10e-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="3e10e-195">İle kısmi bir şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e10e-195">Create a Template with a Partial</span></span>

<span data-ttu-id="3e10e-196">Çok karmaşık bir görünümünü alır, kısmi görünüm bozucu başlatmak için iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="3e10e-197">Kısmi bölümleri kullanarak kendi görünümlerinizi anlamak ve sürdürmek daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="3e10e-198">Kısmi, oluşturacağız film veritabanı kayıtların her birinde biçimlendirmek için bir şablon olarak kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="3e10e-199">Kısmi oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3e10e-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="3e10e-200">Views\Movie klasörü sağ tıklatın ve menü seçeneğini **Görünüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="3e10e-201">Etiketli onay *(.ascx) kısmi görünüm oluşturma*.</span><span class="sxs-lookup"><span data-stu-id="3e10e-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="3e10e-202">Kısmi ad *MovieTemplate*.</span><span class="sxs-lookup"><span data-stu-id="3e10e-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="3e10e-203">Etiketli onay **kesin türü belirtilmiş görünüm oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="3e10e-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="3e10e-204">Film olarak seçin *görüntülemek veri sınıfı*.</span><span class="sxs-lookup"><span data-stu-id="3e10e-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="3e10e-205">Boş olarak işaretleyin *içeriği görüntüle*.</span><span class="sxs-lookup"><span data-stu-id="3e10e-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="3e10e-206">Tıklayın **Ekle** düğmesini kısmi projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="3e10e-207">Bu adımları tamamladıktan sonra 3 listeleme gibi aramak için kısmi MovieTemplate değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3e10e-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

**<span data-ttu-id="3e10e-208">3 – Views\Movie\MovieTemplate.ascx listeleme</span><span class="sxs-lookup"><span data-stu-id="3e10e-208">Listing 3 – Views\Movie\MovieTemplate.ascx</span></span>**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="3e10e-209">Kısmi listeleme 3'te kayıt tek bir satır için bir şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="3e10e-210">Listeleme 4'te değiştirilmiş dizini görünümü, kısmi MovieTemplate kullanır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

**<span data-ttu-id="3e10e-211">4 – Views\Movie\Index.aspx listeleme</span><span class="sxs-lookup"><span data-stu-id="3e10e-211">Listing 4 – Views\Movie\Index.aspx</span></span>**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="3e10e-212">4 liste görünümünde bir For içeren tüm film her döngü.</span><span class="sxs-lookup"><span data-stu-id="3e10e-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="3e10e-213">Her bir filmi kısmi MovieTemplate film biçimlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="3e10e-214">MovieTemplate RenderPartial() yardımcı yöntemini çağırarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="3e10e-215">Veritabanı kayıtlarını çok aynı HTML tablosu değiştirilmiş Index görünümünü işler.</span><span class="sxs-lookup"><span data-stu-id="3e10e-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="3e10e-216">Ancak, görünümü önemli ölçüde basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3e10e-216">However, the view has been greatly simplified.</span></span>


<span data-ttu-id="3e10e-217">Bir dize döndürmediğinden RenderPartial() yöntemi diğer yardımcı yöntemlerinin bir çoğu uygulamadan farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3e10e-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="3e10e-218">Bu nedenle, RenderPartial() yöntemi kullanarak çağırmalıdır &lt;Html.RenderPartial() %&gt; yerine &lt;% = Html.RenderPartial() %&gt;.</span><span class="sxs-lookup"><span data-stu-id="3e10e-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>


## <a name="summary"></a><span data-ttu-id="3e10e-219">Özet</span><span class="sxs-lookup"><span data-stu-id="3e10e-219">Summary</span></span>

<span data-ttu-id="3e10e-220">Bu öğreticinin amacı, bir veritabanı kayıt kümesi ile HTML tablosu halinde nasıl görüntüleyebileceğiniz açıklamak için oluştu.</span><span class="sxs-lookup"><span data-stu-id="3e10e-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="3e10e-221">İlk olarak, Microsoft Entity Framework avantajlarından yararlanarak veritabanı kayıt kümesini bir denetleyici eylemi dönüş hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="3e10e-222">Ardından, otomatik olarak öğelerin bir koleksiyonunu görüntüleyen bir görünüm oluşturmak için Visual Studio yapı iskelesi kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="3e10e-223">Son olarak, kısmi avantajlarından yararlanarak görünümü basitleştirmek hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="3e10e-224">Kısmi bir şablon olarak kullanabilir, böylece her veritabanı kaydı biçimlendirebilirsiniz öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3e10e-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e10e-225">[Önceki](creating-model-classes-with-linq-to-sql-vb.md)
> [İleri](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3e10e-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
