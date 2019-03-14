---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio kullanarak ASP.NET Web Dağıtımı: Veritabanı güncelleştirmesi dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisinin nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) web uygulamasını Azure App Service Web Apps veya bir üçüncü taraf barındırma sağlayıcı tarafından usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 5c9b0c71e2e0d35645e975e9adb7086e65bcf4c3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066666"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="e95ba-103">Visual Studio kullanarak ASP.NET Web Dağıtımı: Veritabanı Güncelleştirmesi Dağıtma</span><span class="sxs-lookup"><span data-stu-id="e95ba-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>
====================
<span data-ttu-id="e95ba-104">tarafından [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e95ba-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e95ba-105">Başlangıç projesini indirin</span><span class="sxs-lookup"><span data-stu-id="e95ba-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="e95ba-106">Bu öğretici serisinin nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısı, Visual Studio 2012 veya Visual Studio 2010 kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e95ba-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="e95ba-107">Seriyle ilgili daha fazla bilgi için bkz: [serideki ilk öğreticide](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e95ba-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="e95ba-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e95ba-108">Overview</span></span>

<span data-ttu-id="e95ba-109">Bu öğreticide, bir veritabanı değişikliği ve ilgili kod değişiklikleri, yaptığınız değişiklikleri Visual Studio'da Test etmek ve ardından güncelleştirme test, hazırlık ve üretim ortamlarına dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e95ba-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="e95ba-110">Bu öğreticide ilk Code First Migrations tarafından yönetilen bir veritabanını güncelleştirmek gösterilmektedir ve ardından daha sonra dbDacFx sağlayıcısını kullanarak bir veritabanını güncelleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="e95ba-111">Anımsatıcı: Bir hata iletisi alıyorum veya Bu öğreticide ilerlerken bir sorun oluşması durumunda kontrol ettiğinizden emin olun [sorun giderme sayfası](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e95ba-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="e95ba-112">Code First Migrations'ı kullanarak bir veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="e95ba-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="e95ba-113">Bu bölümde, bir doğum tarihi sütun eklemek `Person` için temel sınıf `Student` ve `Instructor` varlıklar.</span><span class="sxs-lookup"><span data-stu-id="e95ba-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="e95ba-114">Ardından yeni bir sütun görüntüler Eğitmen veri görüntüleyen sayfa güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="e95ba-115">Son olarak, değişiklikleri test, hazırlık ve üretim için dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="e95ba-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="e95ba-116">Uygulama veritabanı tablosunda bir sütun ekleyin</span><span class="sxs-lookup"><span data-stu-id="e95ba-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="e95ba-117">İçinde *ContosoUniversity.DAL* projesini açarsanız *Person.cs* ve sonunda aşağıdaki özelliği ekleyin `Person` sınıfı (bulunmamalıdır iki kapatma küme ayraçlarını aşağıdaki):</span><span class="sxs-lookup"><span data-stu-id="e95ba-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="e95ba-118">Ardından, güncelleştirme `Seed` olan yeni bir sütun için bir değer sağlar. böylece yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="e95ba-119">Açık *Migrations\Configuration.cs* ve başlayan kod bloğunu `var instructors = new List<Instructor>` doğum tarihi bilgi içeren aşağıdaki kod bloğu ile:</span><span class="sxs-lookup"><span data-stu-id="e95ba-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="e95ba-120">Çözümü derleyin ve ardından açın **Paket Yöneticisi Konsolu** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="e95ba-121">Olarak ContosoUniversity.DAL hala seçili olduğundan emin olun **varsayılan proje**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="e95ba-122">İçinde **Paket Yöneticisi Konsolu** penceresinde **ContosoUniversity.DAL** olarak **varsayılan proje**ve ardından aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="e95ba-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="e95ba-123">Bu komut tamamlandığında, Visual Studio yeni tanımlayan sınıf dosyasını açar `DbMIgration` sınıfı ve `Up` yöntemi yeni bir sütun oluşturan kodu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e95ba-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="e95ba-124">`Up` Değişiklik uygularken sütunu yöntemi oluşturur ve `Down` yöntemi değişikliği geri olduğunda sütun siler.</span><span class="sxs-lookup"><span data-stu-id="e95ba-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="e95ba-126">Çözümü derleyin ve ardından aşağıdaki komutu girin **Paket Yöneticisi Konsolu** penceresi (ContosoUniversity.DAL proje hala seçili olduğundan emin olun):</span><span class="sxs-lookup"><span data-stu-id="e95ba-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="e95ba-127">Entity Framework çalıştıran `Up` yöntemi ve çalıştırmaları `Seed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="e95ba-128">Görüntü Eğitmenler sayfasında yeni bir sütun</span><span class="sxs-lookup"><span data-stu-id="e95ba-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="e95ba-129">ContosoUniversity projeyi *Instructors.aspx* ve doğum tarihini görüntülemek için yeni bir şablon alan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="e95ba-130">İşe alma tarih ve office atama yönelik olanlar arasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e95ba-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="e95ba-131">(Kod girintilemesinin eşitlenmemiş alırsa, otomatik olarak dosyayı yeniden biçimlendirmek için CTRL-K ve ardından CTRL-D tuşlarına basabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="e95ba-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="e95ba-132">Uygulamayı çalıştırmak ve tıklayın **Eğitmenler** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e95ba-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="e95ba-133">Sayfa yüklendiğinde yeni olduğunu gördüğünüz Doğum Tarihi alanı.</span><span class="sxs-lookup"><span data-stu-id="e95ba-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![Doğum tarihi Eğitmenler sayfası](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="e95ba-135">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="e95ba-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="e95ba-136">Veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="e95ba-136">Deploy the database update</span></span>

1. <span data-ttu-id="e95ba-137">İçinde **Çözüm Gezgini** ContosoUniversity projeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="e95ba-138">İçinde **Web tek tık Yayımla** araç çubuğunda tıklatın **Test** yayımlama profili ve ardından **Web'i Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="e95ba-139">(Araç çubuğunda devre dışı bırakılırsa ContosoUniversity projesinde seçin **Çözüm Gezgini**.)</span><span class="sxs-lookup"><span data-stu-id="e95ba-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="e95ba-140">Visual Studio güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="e95ba-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="e95ba-141">Çalıştırma **Eğitmenler** güncelleştirme başarıyla dağıtıldığını doğrulamak için sayfa.</span><span class="sxs-lookup"><span data-stu-id="e95ba-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="e95ba-142">Uygulama veritabanı için bu sayfaya erişmeye çalıştığında, Code First veritabanı şemasını güncelleştirir ve çalışan `Seed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="e95ba-143">Sayfası görüntülendiğinde, beklenen gördüğünüz **doğum tarihi** içindeki tarihler içeren sütun.</span><span class="sxs-lookup"><span data-stu-id="e95ba-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="e95ba-144">İçinde **Web tek tık Yayımla** araç çubuğunda tıklatın **hazırlama** yayımlama profili ve ardından **Web'i Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="e95ba-145">Çalıştırma **Eğitmenler** sayfa güncelleştirme başarıyla dağıtıldığını doğrulamak için hazırlama.</span><span class="sxs-lookup"><span data-stu-id="e95ba-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="e95ba-146">İçinde **Web tek tık Yayımla** araç çubuğunda tıklatın **üretim** yayımlama profili ve ardından **Web'i Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="e95ba-147">Çalıştırma **Eğitmenler** güncelleştirme başarıyla dağıtıldığını doğrulamak için üretim sayfasında.</span><span class="sxs-lookup"><span data-stu-id="e95ba-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="e95ba-148">Veritabanı değişikliği içeren gerçek üretimde uygulama güncelleştirmesi için genellikle de uygulama dağıtımı sırasında çevrimdışı kullanarak götürecek *uygulama\_offline.htm*, önceki öğreticide gördüğünüz gibi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="e95ba-149">DbDacFx sağlayıcısını kullanarak bir veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="e95ba-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="e95ba-150">Bu bölümde, eklediğiniz bir *açıklamaları* sütuna *kullanıcı* üyelik veritabanında tablo ve görüntüler ve her kullanıcı için açıklamaları Düzenle sağlayan bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e95ba-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="e95ba-151">Ardından, değişikliklerin test, hazırlık ve üretim için dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="e95ba-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="e95ba-152">Üyelik veritabanında bir tabloya bir sütun ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="e95ba-153">Visual Studio'da açın **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="e95ba-154">Genişletin **(localdb) \v11.0**, genişletme **veritabanları**, genişletin **aspnet ContosoUniversity** (değil **aspnet ContosoUniversity Prod**) ve ardından **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="e95ba-155">Görmüyorsanız **(localdb) \v11.0** altında **SQL Server** düğümünü sağ **SQL Server** düğüm ve tıklatın **SQL Server Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="e95ba-156">İçinde **sunucuya Bağlan** iletişim kutusuna *(localdb) \v11.0* olarak **sunucu adı**ve ardından **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="e95ba-157">Görmüyorsanız **aspnet ContosoUniversity**kullanarak oturum açın ve projeyi Çalıştır *yönetici* kimlik bilgilerini (parola *devpwd*) ve ardından yenileyin  **SQL Server Nesne Gezgini** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="e95ba-158">Sağ **kullanıcılar** tablosunu ve ardından **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX Görünüm Tasarımcısı](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="e95ba-160">Tasarımcıda ekleme bir *açıklamaları* sütun ve *nvarchar(128)* ve boş değer atanabilir ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![Comments sütunu ekleme](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="e95ba-162">İçinde **veritabanı güncelleştirmelerini Önizle** kutusunun **veritabanını Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![Veritabanı güncelleştirmelerini Önizle](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="e95ba-164">Görüntülemek ve yeni bir sütun düzenlemek için bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="e95ba-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="e95ba-165">İçinde **Çözüm Gezgini**, sağ **hesabı** ContosoUniversity proje klasörü tıklatın **Ekle**ve ardından **yeni öğe** .</span><span class="sxs-lookup"><span data-stu-id="e95ba-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="e95ba-166">Yeni bir **Web formu kullanarak ana sayfa** ve adlandırın *UserInfo.aspx*.</span><span class="sxs-lookup"><span data-stu-id="e95ba-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="e95ba-167">Varsayılan değerleri kabul *Site.Master* dosyası ana sayfa olarak.</span><span class="sxs-lookup"><span data-stu-id="e95ba-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="e95ba-168">Aşağıdaki biçimlendirmede içine kopyalamak `MainContent` `Content` öğesi (son 3'ün `Content` öğeleri):</span><span class="sxs-lookup"><span data-stu-id="e95ba-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="e95ba-169">Sağ *UserInfo.aspx* sayfasında ve tıklayın **tarayıcıda görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="e95ba-170">Oturum açmada, *yönetici* kullanıcı kimlik bilgilerini (parola *devpwd*) ve sayfayı düzgün çalıştığını doğrulamak için bir kullanıcı için bazı yorumlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![Kullanıcı bilgileri sayfası](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="e95ba-172">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="e95ba-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="e95ba-173">Veritabanı güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="e95ba-173">Deploy the database update</span></span>

<span data-ttu-id="e95ba-174">DbDacFx sağlayıcısını kullanarak dağıtmak için seçilecek yeterlidir **veritabanını Güncelleştir** yayımlama profilini seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e95ba-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="e95ba-175">Bu seçenek kullanıldığında ancak, ilk dağıtım için de bazı ek SQL betiklerini çalıştırmak için yapılandırdığınız: hala profilinde olanlardır ve bunları yeniden çalıştırmasını engellemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="e95ba-176">Açık **Web'i Yayımla** ContosoUniversity projeye sağ tıklayıp'ı tıklatarak Sihirbazı **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="e95ba-177">Seçin **Test** profili.</span><span class="sxs-lookup"><span data-stu-id="e95ba-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="e95ba-178">Tıklayın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="e95ba-179">Altında **DefaultConnection**seçin **veritabanını Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="e95ba-180">Ek betikleri çalıştırmak için ilk dağıtım için yapılandırılmış devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="e95ba-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="e95ba-181">Tıklayın **yapılandırma veritabanı güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="e95ba-182">İçinde **veritabanı güncellemelerini yapılandırma** iletişim kutusu temizleyin onay kutularını yanındaki *Grant.sql* ve *aspnet veri dev.sql*.</span><span class="sxs-lookup"><span data-stu-id="e95ba-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="e95ba-183">**Kapat**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e95ba-183">Click **Close**.</span></span>
6. <span data-ttu-id="e95ba-184">Tıklayın **Önizleme** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e95ba-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="e95ba-185">Altında **veritabanları** ve sağındaki **DefaultConnection**, tıklayın **veritabanı önizlemesi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e95ba-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![Veritabanı önizlemesi](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="e95ba-187">Önizleme penceresini hedef veritabanında eşleşen kaynak veritabanı şeması, veritabanı şemasını yapmak için çalıştırılacak komut dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="e95ba-188">Betik yeni bir sütun ekler. bir ALTER TABLE komutu içerir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="e95ba-189">Kapat **veritabanı önizlemesi** iletişim kutusunu ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e95ba-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="e95ba-190">Visual Studio güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="e95ba-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="e95ba-191">Kullanıcı bilgileri çalıştırırsanız (ekleme *Account/UserInfo.aspx* giriş sayfası URL'si için) güncelleştirme başarıyla dağıtıldığını doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="e95ba-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="e95ba-192">Girerek oturum açması *yönetici* ve *devpwd*.</span><span class="sxs-lookup"><span data-stu-id="e95ba-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="e95ba-193">Tablolardaki verileri varsayılan olarak dağıtılmaz ve geliştirme eklenen açıklama bulmaz şekilde çalıştırmak için bir veri dağıtım betiği yapılandırmadı.</span><span class="sxs-lookup"><span data-stu-id="e95ba-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="e95ba-194">Değişiklik veritabanına dağıtılmıştır ve sayfayı düzgün çalıştığını doğrulamak için hazırlama artık yeni bir açıklama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e95ba-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="e95ba-195">Hazırlama ve üretime dağıtmak için aynı yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="e95ba-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="e95ba-196">Ek betikleri devre dışı bırakmak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e95ba-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="e95ba-197">Hazırlama aşamasında yalnızca tek bir betik devre dışı bırakır ve üretim profilleri yalnızca çalıştırmak için yapılandırılmış olduğundan Test profiline kıyasla tek fark, *aspnet prod data.sql*.</span><span class="sxs-lookup"><span data-stu-id="e95ba-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="e95ba-198">Hazırlama ve üretim için kimlik bilgileri, yönetim ve prodpwd ' dir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="e95ba-199">Veritabanı değişikliği içeren gerçek üretimde uygulama güncelleştirmesi için genellikle de uygulama dağıtımı sırasında çevrimdışı yükleyerek götürecek *uygulama\_offline.htm* yayımlama ve silmeden önce gördüğünüz gibi daha sonra [önceki öğreticide](deploying-a-code-update.md).</span><span class="sxs-lookup"><span data-stu-id="e95ba-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="e95ba-200">Özet</span><span class="sxs-lookup"><span data-stu-id="e95ba-200">Summary</span></span>

<span data-ttu-id="e95ba-201">Artık Code First Migrations'ı hem dbDacFx Sağlayıcısı'nı kullanarak bir veritabanı değişiklik bulunan bir uygulama güncelleştirmesi dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="e95ba-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![Doğum tarihi Eğitmenler sayfası](deploying-a-database-update/_static/image8.png)

![Kullanıcı bilgileri sayfası](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="e95ba-204">Sonraki öğreticiye dağıtımları ve komut satırını kullanarak yürütme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e95ba-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e95ba-205">[Önceki](deploying-a-code-update.md)
> [İleri](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="e95ba-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
