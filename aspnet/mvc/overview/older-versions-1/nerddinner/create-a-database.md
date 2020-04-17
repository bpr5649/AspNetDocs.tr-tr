---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Veritabanı Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 2, NerdDinner uygulamamız için tüm akşam yemeği ve RSVP verilerini tutan veritabanını oluşturma adımlarını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541617"
---
# <a name="create-a-database"></a><span data-ttu-id="11794-103">Veritabanı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="11794-103">Create a Database</span></span>

<span data-ttu-id="11794-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="11794-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="11794-105">PDF’yi İndir</span><span class="sxs-lookup"><span data-stu-id="11794-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="11794-106">Bu adım 2 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.</span><span class="sxs-lookup"><span data-stu-id="11794-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="11794-107">Adım 2, NerdDinner uygulamamız için tüm akşam yemeği ve RSVP verilerini tutan veritabanını oluşturma adımlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="11794-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="11794-108">MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.</span><span class="sxs-lookup"><span data-stu-id="11794-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="11794-109">NerdDinner Adım 2: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="11794-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="11794-110">NerdDinner uygulamamız için tüm Akşam Yemeği ve RSVP verilerini depolamak için bir veritabanı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="11794-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="11794-111">Aşağıdaki adımlar, ücretsiz SQL Server Express sürümünü kullanarak veritabanıoluşturmayı gösterir [(Microsoft Web Platform Installer'ın](https://www.microsoft.com/web/downloads/platform.aspx)V2'sini kullanarak kolayca yükleyebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="11794-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="11794-112">Yazacağınız tüm kodlar hem SQL Server Express hem de tam SQL Server ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="11794-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="11794-113">Yeni bir SQL Server Express veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="11794-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="11794-114">Web projemize sağ tıklayarak başlayacağız ve ardından **Ekle-&gt;Yeni Öğe** menüsü komutunu seçeceğiz:</span><span class="sxs-lookup"><span data-stu-id="11794-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="11794-115">Bu, Visual Studio'nun "Yeni Öğe Ekle" iletişim kutusunu gündeme getirecektir.</span><span class="sxs-lookup"><span data-stu-id="11794-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="11794-116">"Veri" kategorisine göre filtre uygulayacağız ve "SQL Server Database" öğe şablonu seçeceğiz:</span><span class="sxs-lookup"><span data-stu-id="11794-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="11794-117">"NerdDinner.mdf" oluşturmak istediğimiz SQL Server Express veritabanına isim vereceğiz ve tamam tuşuna basacağız.</span><span class="sxs-lookup"><span data-stu-id="11794-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="11794-118">Visual Studio daha sonra bu dosyayı \App\_Data dizinine eklemek isteyip istemediğimizi soracaktır (ki bu, güvenlik Aç'larını hem okuyhem de yazabilen bir dizinidir):</span><span class="sxs-lookup"><span data-stu-id="11794-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="11794-119">"Evet"i tıklatacağız ve yeni veritabanımız oluşturulacak ve Çözüm Gezgini'ne eklenecektir:</span><span class="sxs-lookup"><span data-stu-id="11794-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="11794-120">Veritabanımızda Tablo Oluşturma</span><span class="sxs-lookup"><span data-stu-id="11794-120">Creating Tables within our Database</span></span>

<span data-ttu-id="11794-121">Artık yeni bir boş veritabanımız var.</span><span class="sxs-lookup"><span data-stu-id="11794-121">We now have a new empty database.</span></span> <span data-ttu-id="11794-122">Buna birkaç tablo ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="11794-122">Let's add some tables to it.</span></span>

<span data-ttu-id="11794-123">Bunu yapmak için Visual Studio'daki "Server Explorer" sekmesine gideriz ve bu da veritabanlarını ve sunucuları yönetmemizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="11794-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="11794-124">Uygulamamızın \App\_Data klasöründe depolanan SQL Server Express veritabanları otomatik olarak Server Explorer içinde gösterilecek.</span><span class="sxs-lookup"><span data-stu-id="11794-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="11794-125">İsteğe bağlı olarak "Server Explorer" penceresinin üst kısmındaki "Veritabanına Bağlan" simgesini kullanarak listeye ek SQL Server veritabanları (yerel ve uzak) ekleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="11794-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="11794-126">Biz NerdDinner veritabanına iki tablo ekleyeceğiz - biri bizim Dinners saklamak için, ve diğer onlara RSVP kabulleri izlemek için.</span><span class="sxs-lookup"><span data-stu-id="11794-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="11794-127">Veritabanımızdaki "Tablolar" klasörüne sağ tıklayarak ve "Yeni Tablo Ekle" menü komutunu seçerek yeni tablolar oluşturabiliriz:</span><span class="sxs-lookup"><span data-stu-id="11794-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="11794-128">Bu bize tablonun şema yapılandırmak için izin veren bir tablo tasarımcısı açılacaktır.</span><span class="sxs-lookup"><span data-stu-id="11794-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="11794-129">"Akşam Yemekleri" tablomuz için 10 veri sütunu ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="11794-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="11794-130">"DinnerID" sütununun tablo için benzersiz bir birincil anahtar olmasını istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="11794-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="11794-131">Bunu "DinnerID" sütununa sağ tıklayarak ve "Birincil Anahtarı Ayarla" menü öğesini seçerek yapılandırabiliriz:</span><span class="sxs-lookup"><span data-stu-id="11794-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="11794-132">DinnerID'ı birincil anahtar haline getirmenin yanı sıra, yeni veri satırları tabloya eklendikçe değeri otomatik olarak artılan bir "kimlik" sütunu olarak da yapılandırmak isteriz (yani eklenen ilk Akşam Yemeği satırı 1'lik bir DinnerID'ye sahip olacak, ikinci eklenen satırda 2'lik bir DinnerID olacak vb.)</span><span class="sxs-lookup"><span data-stu-id="11794-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="11794-133">Bunu "DinnerID" sütununa seçerek yapabilir izleyebilirsiniz ve sütundaki "(Kimlik)" özelliğini "Evet" olarak ayarlamak için "Sütun Özellikleri" düzenleyicisini kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="11794-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="11794-134">Standart kimlik varsayılanlarını kullanırız (her yeni Akşam Yemeği satırında 1'den başlar ve 1'den başlar):</span><span class="sxs-lookup"><span data-stu-id="11794-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="11794-135">Daha sonra Ctrl-S yazarak veya **Dosya-Kaydet&gt;** menüsü komutunu kullanarak tablomuzu kaydedeceğiz.</span><span class="sxs-lookup"><span data-stu-id="11794-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="11794-136">Bu, tabloya isim vermemizi ister.</span><span class="sxs-lookup"><span data-stu-id="11794-136">This will prompt us to name the table.</span></span> <span data-ttu-id="11794-137">Adını "Akşam Yemekleri" koyacağız:</span><span class="sxs-lookup"><span data-stu-id="11794-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="11794-138">Yeni Akşam Yemekleri tablomuz daha sonra sunucu gezgininde veritabanımızda gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="11794-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="11794-139">Daha sonra yukarıdaki adımları tekraredeceğiz ve bir "RSVP" tablosu oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="11794-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="11794-140">Bu tablo ile 3 sütun var.</span><span class="sxs-lookup"><span data-stu-id="11794-140">This table with have 3 columns.</span></span> <span data-ttu-id="11794-141">RsvpID sütununa birincil anahtar olarak kurulum yapacağız ve ayrıca onu bir kimlik sütunu haline getireceğiz:</span><span class="sxs-lookup"><span data-stu-id="11794-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="11794-142">Onu kurtarAcağız ve ona "RSVP" adını vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="11794-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="11794-143">Tablolar Arasında Yabancı Anahtar İlişkisi Kurma</span><span class="sxs-lookup"><span data-stu-id="11794-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="11794-144">Veritabanımızda iki tablo var.</span><span class="sxs-lookup"><span data-stu-id="11794-144">We now have two tables within our database.</span></span> <span data-ttu-id="11794-145">Son şema tasarım adımımız, bu iki tablo arasında "bir-çok" ilişki kurmak olacaktır – böylece her Akşam Yemeği satırına uygulanan sıfır veya daha fazla RSVP satırıyla ilişkilendirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="11794-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="11794-146">Bunu, RSVP tablosunun "DinnerID" sütununa "DinnerID" tablosundaki "DinnerID" sütununa yabancı anahtar ilişkisi sağlayacak şekilde yapılandırarak yapacağız.</span><span class="sxs-lookup"><span data-stu-id="11794-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="11794-147">Bunu yapmak için, sunucu gezgininde çift tıklayarak tablo tasarımcısı içindeki RSVP tablosunu açarız.</span><span class="sxs-lookup"><span data-stu-id="11794-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="11794-148">Daha sonra içindeki "DinnerID" sütununa sağ tıklayıp "İlişkiler..." seçeneğini seçeceğiz. bağlam menüsü komutu:</span><span class="sxs-lookup"><span data-stu-id="11794-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="11794-149">Bu, tablolar arasındaki ilişkileri kurmak için kullanabileceğimiz bir iletişim kutusunu getirir:</span><span class="sxs-lookup"><span data-stu-id="11794-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="11794-150">İletişim kutusuna yeni bir ilişki eklemek için "Ekle" düğmesini tıklatırız.</span><span class="sxs-lookup"><span data-stu-id="11794-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="11794-151">Bir ilişki eklendikten sonra, özellik ızgarası içindeki "Tablolar ve Sütun Belirtimi" ağaç görünümü düğümünün iletişim kutusunun sağında genişletilir ve sonra "..." seçeneğini tıklarız. düğmesinin sağındaki:</span><span class="sxs-lookup"><span data-stu-id="11794-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="11794-152">"..." seçeneğini tıklattığınızda düğmesi, ilişkiye hangi tabloların ve sütunların dahil olduğunu belirtmemize ve ilişkiye isim vermemize olanak tanıyan başka bir iletişim kutusunu gündeme getirecektir.</span><span class="sxs-lookup"><span data-stu-id="11794-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="11794-153">Birincil Anahtar Tablosunu "Akşam Yemekleri" olarak değiştireceğiz ve birincil anahtar olarak Akşam Yemeği tablosundaki "DinnerID" sütununa seçeceğiz.</span><span class="sxs-lookup"><span data-stu-id="11794-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="11794-154">RSVP tablomuz yabancı anahtar tablosu ve RSVP olacak. DinnerID sütunu yabancı anahtar olarak ilişkilendirilecektir:</span><span class="sxs-lookup"><span data-stu-id="11794-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="11794-155">Şimdi RSVP tablosundaki her satır, Akşam Yemeği tablosundaki bir satırla ilişkilendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="11794-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="11794-156">SQL Server bizim için başvuru bütünlüğünü koruyacak tır ve geçerli bir Akşam Yemeği satırına işaret etmiyorsa yeni bir RSVP satırı eklememizi engeller.</span><span class="sxs-lookup"><span data-stu-id="11794-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="11794-157">Ayrıca, hala buna atıfta bulunan RSVP satırları varsa, akşam yemeği satırLarını silmemizi de engeller.</span><span class="sxs-lookup"><span data-stu-id="11794-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="11794-158">Tablolarımıza Veri Ekleme</span><span class="sxs-lookup"><span data-stu-id="11794-158">Adding Data to our Tables</span></span>

<span data-ttu-id="11794-159">Akşam Yemekleri tablomuza bazı örnek verileri ekleyerek bitirelim.</span><span class="sxs-lookup"><span data-stu-id="11794-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="11794-160">Sunucu Gezgini içinde sağ tıklayarak ve "Tablo Verilerini Göster" komutunu seçerek tabloya veri ekleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="11794-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="11794-161">Uygulamayı uygulamaya başladığımızda daha sonra kullanabileceğimiz birkaç satır Akşam Yemeği verisi ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="11794-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="11794-162">Sonraki Adım</span><span class="sxs-lookup"><span data-stu-id="11794-162">Next Step</span></span>

<span data-ttu-id="11794-163">Veritabanımızı oluşturmayı bitirdik.</span><span class="sxs-lookup"><span data-stu-id="11794-163">We've finished creating our database.</span></span> <span data-ttu-id="11794-164">Şimdi sorgulayıp güncellemek için kullanabileceğimiz model sınıfları oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="11794-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11794-165">[Önceki](create-a-new-aspnet-mvc-project.md)
> [Sonraki](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="11794-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
