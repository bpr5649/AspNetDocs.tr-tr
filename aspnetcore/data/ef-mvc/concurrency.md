---
title: 'Öğretici: Eşzamanlılık - EF çekirdekli ASP.NET MVC işleme'
description: Bu öğreticide, birden çok kullanıcı aynı anda aynı varlık güncelleştirdiğinizde çakışmalarına gösterilmektedir.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/05/2019
ms.topic: tutorial
uid: data/ef-mvc/concurrency
ms.openlocfilehash: 7b18927d5d528ec2951087502e26b2b30214f389
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073359"
---
# <a name="tutorial-handle-concurrency---aspnet-mvc-with-ef-core"></a><span data-ttu-id="aed0e-103">Öğretici: Eşzamanlılık - EF çekirdekli ASP.NET MVC işleme</span><span class="sxs-lookup"><span data-stu-id="aed0e-103">Tutorial: Handle concurrency - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="aed0e-104">Önceki öğreticilerde, verileri güncelleştirmek hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-104">In earlier tutorials, you learned how to update data.</span></span> <span data-ttu-id="aed0e-105">Bu öğreticide, birden çok kullanıcı aynı anda aynı varlık güncelleştirdiğinizde çakışmalarına gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-105">This tutorial shows how to handle conflicts when multiple users update the same entity at the same time.</span></span>

<span data-ttu-id="aed0e-106">Departman varlık ile çalışma ve eşzamanlılık hatalarını işleme web sayfaları oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="aed0e-106">You'll create web pages that work with the Department entity and handle concurrency errors.</span></span> <span data-ttu-id="aed0e-107">Aşağıdaki çizimler bir eşzamanlılık çakışması ortaya çıkarsa, gösterilen bazı iletileri de dahil olmak üzere düzenleme ve silme sayfalar gösterir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-107">The following illustrations show the Edit and Delete pages, including some messages that are displayed if a concurrency conflict occurs.</span></span>

![Departman düzenleme sayfası](concurrency/_static/edit-error.png)

![Bölüm silme sayfası](concurrency/_static/delete-error.png)

<span data-ttu-id="aed0e-110">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="aed0e-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed0e-111">Eşzamanlılık çakışmalarını hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="aed0e-111">Learn about concurrency conflicts</span></span>
> * <span data-ttu-id="aed0e-112">İzleme özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="aed0e-112">Add a tracking property</span></span>
> * <span data-ttu-id="aed0e-113">Departmanlar denetleyici ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aed0e-113">Create Departments controller and views</span></span>
> * <span data-ttu-id="aed0e-114">Dizini görünümünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aed0e-114">Update Index view</span></span>
> * <span data-ttu-id="aed0e-115">Düzenleme metotlarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="aed0e-115">Update Edit methods</span></span>
> * <span data-ttu-id="aed0e-116">Güncelleştirme düzenleme görünümü</span><span class="sxs-lookup"><span data-stu-id="aed0e-116">Update Edit view</span></span>
> * <span data-ttu-id="aed0e-117">Test eşzamanlılık çakışmaları</span><span class="sxs-lookup"><span data-stu-id="aed0e-117">Test concurrency conflicts</span></span>
> * <span data-ttu-id="aed0e-118">Silme sayfası</span><span class="sxs-lookup"><span data-stu-id="aed0e-118">Update the Delete page</span></span>
> * <span data-ttu-id="aed0e-119">Güncelleştirme ayrıntıları ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aed0e-119">Update Details and Create views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aed0e-120">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aed0e-120">Prerequisites</span></span>

* [<span data-ttu-id="aed0e-121">Bir ASP.NET Core MVC web uygulamasında EF Core ile ilgili verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aed0e-121">Update related data with EF Core in an ASP.NET Core MVC web app</span></span>](update-related-data.md)

## <a name="concurrency-conflicts"></a><span data-ttu-id="aed0e-122">Eşzamanlılık çakışmaları</span><span class="sxs-lookup"><span data-stu-id="aed0e-122">Concurrency conflicts</span></span>

<span data-ttu-id="aed0e-123">Düzenlemek için bir kullanıcı bir varlığın verilerini görüntüler ve ilk kullanıcının değişiklik veritabanına yazılmadan önce başka bir kullanıcı aynı varlığın veri güncelleştirmeleri bir eşzamanlılık çakışması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-123">A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates the same entity's data before the first user's change is written to the database.</span></span> <span data-ttu-id="aed0e-124">Böyle bir çakışma algılanması etkinleştirmezseniz, kişi veritabanını güncelleştiren son diğer kullanıcının yaptığı değişikliklerin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-124">If you don't enable the detection of such conflicts, whoever updates the database last overwrites the other user's changes.</span></span> <span data-ttu-id="aed0e-125">Birçok uygulamada, bu riski kabul edilebilir: Bazı kullanıcılara veya birkaç güncelleştirmeleri varsa veya bazı değişikliklerin üzerine yazılır, programlama için eşzamanlılık maliyeti gereksinimlerine ağır bastığı avantajı gerçekten önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-125">In many applications, this risk is acceptable: if there are few users, or few updates, or if isn't really critical if some changes are overwritten, the cost of programming for concurrency might outweigh the benefit.</span></span> <span data-ttu-id="aed0e-126">Bu durumda, eşzamanlılık çakışmalarını işleme için uygulamayı yapılandırmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aed0e-126">In that case, you don't have to configure the application to handle concurrency conflicts.</span></span>

### <a name="pessimistic-concurrency-locking"></a><span data-ttu-id="aed0e-127">Kötümser eşzamanlılık (kilitleme)</span><span class="sxs-lookup"><span data-stu-id="aed0e-127">Pessimistic concurrency (locking)</span></span>

<span data-ttu-id="aed0e-128">Uygulamanızı eşzamanlılık senaryolarda yanlışlıkla veri kaybı önleme ihtiyacınız varsa, bunu yapmanın bir yolu veritabanı kilitlerini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-128">If your application does need to prevent accidental data loss in concurrency scenarios, one way to do that is to use database locks.</span></span> <span data-ttu-id="aed0e-129">Bu, eşzamanlılık çağrılır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-129">This is called pessimistic concurrency.</span></span> <span data-ttu-id="aed0e-130">Örneğin, bir veritabanından satır okumadan önce kilit isteği salt okunur veya güncelleştirme erişim için.</span><span class="sxs-lookup"><span data-stu-id="aed0e-130">For example, before you read a row from a database, you request a lock for read-only or for update access.</span></span> <span data-ttu-id="aed0e-131">Güncelleştirme erişimi için bir satır kilitlerseniz, başka hiçbir kullanıcı için ya da satırın kilitlemek için izin salt okunur veya değiştirilen sürecinde olan verilerin bir kopyasını elde edecekleri çünkü erişim güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-131">If you lock a row for update access, no other users are allowed to lock the row either for read-only or update access, because they would get a copy of data that's in the process of being changed.</span></span> <span data-ttu-id="aed0e-132">Salt okunur erişim için bir satır kilitlerseniz, diğerleri de salt okunur erişim için kullanılabilir ancak güncelleştirme kilitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-132">If you lock a row for read-only access, others can also lock it for read-only access but not for update.</span></span>

<span data-ttu-id="aed0e-133">Kilitleri yönetmek dezavantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-133">Managing locks has disadvantages.</span></span> <span data-ttu-id="aed0e-134">Programa karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-134">It can be complex to program.</span></span> <span data-ttu-id="aed0e-135">Önemli bir veritabanı yönetim kaynakları gerektirir ve bu uygulamanın kullanıcı sayısı performans sorunlarına neden olabilir artırır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-135">It requires significant database management resources, and it can cause performance problems as the number of users of an application increases.</span></span> <span data-ttu-id="aed0e-136">Bu nedenle, tüm veritabanı yönetim sistemleri kötümser eşzamanlılık destekler.</span><span class="sxs-lookup"><span data-stu-id="aed0e-136">For these reasons, not all database management systems support pessimistic concurrency.</span></span> <span data-ttu-id="aed0e-137">Entity Framework Core yerleşik desteği yok sağlar ve Bu öğreticide nasıl göstermez.</span><span class="sxs-lookup"><span data-stu-id="aed0e-137">Entity Framework Core provides no built-in support for it, and this tutorial doesn't show you how to implement it.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="aed0e-138">İyimser eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="aed0e-138">Optimistic Concurrency</span></span>

<span data-ttu-id="aed0e-139">İyimser eşzamanlılık kötümser eşzamanlılık alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-139">The alternative to pessimistic concurrency is optimistic concurrency.</span></span> <span data-ttu-id="aed0e-140">İyimser eşzamanlılık, eşzamanlılık çakışmalarını olmasını sağlar ve eğer uygun şekilde tepki anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-140">Optimistic concurrency means allowing concurrency conflicts to happen, and then reacting appropriately if they do.</span></span> <span data-ttu-id="aed0e-141">Örneğin, Jane departmanı Düzen sayfasını ziyaret ve bütçe tutar İngilizce bölümü için 350,000.00 $0,00 değiştirir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-141">For example, Jane visits the Department Edit page and changes the Budget amount for the English department from $350,000.00 to $0.00.</span></span>

![Bütçe 0 olarak değiştirme](concurrency/_static/change-budget.png)

<span data-ttu-id="aed0e-143">Jane tıkladığında önce **Kaydet**, John aynı sayfayı ziyaret eder ve alanın başlangıç tarihi 1/9/2013 1/9/2007'deki değiştirir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-143">Before Jane clicks **Save**, John visits the same page and changes the Start Date field from 9/1/2007 to 9/1/2013.</span></span>

![2013'e başlangıç tarihini değiştirme](concurrency/_static/change-date.png)

<span data-ttu-id="aed0e-145">Jane tıkladığında **Kaydet** ilk ve her tarayıcı dizin sayfasına geri döndüğünde değiştirme görür.</span><span class="sxs-lookup"><span data-stu-id="aed0e-145">Jane clicks **Save** first and sees her change when the browser returns to the Index page.</span></span>

![Bütçe sıfır olarak değiştirildi](concurrency/_static/budget-zero.png)

<span data-ttu-id="aed0e-147">John tıklattığında **Kaydet** yine de bir bütçe $350,000.00 birini gösteren bir Düzenle sayfasında.</span><span class="sxs-lookup"><span data-stu-id="aed0e-147">Then John clicks **Save** on an Edit page that still shows a budget of $350,000.00.</span></span> <span data-ttu-id="aed0e-148">Sonraki işlemin ne eşzamanlılık çakışmalarını nasıl ele tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-148">What happens next is determined by how you handle concurrency conflicts.</span></span>

<span data-ttu-id="aed0e-149">Bazı seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aed0e-149">Some of the options include the following:</span></span>

* <span data-ttu-id="aed0e-150">Bir kullanıcı değiştirmiş hangi özelliğinin izlemek ve yalnızca ilgili sütunları veritabanında güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-150">You can keep track of which property a user has modified and update only the corresponding columns in the database.</span></span>

     <span data-ttu-id="aed0e-151">Farklı özellikleri iki kullanıcı tarafından güncelleştirildiği için yer alan örnek senaryoda, veri kaybı, olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-151">In the example scenario, no data would be lost, because different properties were updated by the two users.</span></span> <span data-ttu-id="aed0e-152">Gamze'nin hem Can'ın değişiklikleri--başlangıç tarihi 1/9/2013 / ve sıfır dolarlık bir bütçe biri İngilizce, departman gözatar sonraki açışınızda görürler.</span><span class="sxs-lookup"><span data-stu-id="aed0e-152">The next time someone browses the English department, they will see both Jane's and John's changes -- a start date of 9/1/2013 and a budget of zero dollars.</span></span> <span data-ttu-id="aed0e-153">Bu güncelleştirme yöntemini veri kaybına neden olabilecek çakışmaları sayısını azaltabilir, ancak bir varlığın aynı özelliğe rakip bir değişiklik yaptıysanız, veri kaybını önlemek olamaz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-153">This method of updating can reduce the number of conflicts that could result in data loss, but it can't avoid data loss if competing changes are made to the same property of an entity.</span></span> <span data-ttu-id="aed0e-154">Varlık Çerçevesi'Bu şekilde çalışıp çalışmadığını güncelleştirme kodunuzu nasıl uygulayacağınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-154">Whether the Entity Framework works this way depends on how you implement your update code.</span></span> <span data-ttu-id="aed0e-155">Bir varlığın özgün tüm özellik değerlerini yanı sıra yeni değerleri izlemek için büyük miktarlarda durumu bakımını gerektirebilir içinde bir web uygulaması pratik değildir, çünkü genellikle.</span><span class="sxs-lookup"><span data-stu-id="aed0e-155">It's often not practical in a web application, because it can require that you maintain large amounts of state in order to keep track of all original property values for an entity as well as new values.</span></span> <span data-ttu-id="aed0e-156">Koruma durumu büyük miktarlarda uygulama performansı etkileyebilir sunucu kaynaklarını gerektirir ya da web sayfasında kendisi (örneğin, gizli alanlar) dahil edilmesi için veya bir tanımlama bilgisinde.</span><span class="sxs-lookup"><span data-stu-id="aed0e-156">Maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself (for example, in hidden fields) or in a cookie.</span></span>

* <span data-ttu-id="aed0e-157">Gamze'nin değişikliğinin üzerine Can'ın değişiklik sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-157">You can let John's change overwrite Jane's change.</span></span>

     <span data-ttu-id="aed0e-158">Sonraki biri İngilizce departmanı gözatar, 1/9/2013 görürler ve geri yüklenen $350,000.00 değeri.</span><span class="sxs-lookup"><span data-stu-id="aed0e-158">The next time someone browses the English department, they will see 9/1/2013 and the restored $350,000.00 value.</span></span> <span data-ttu-id="aed0e-159">Bu adlı bir *istemci WINS* veya *WINS'te son* senaryo.</span><span class="sxs-lookup"><span data-stu-id="aed0e-159">This is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="aed0e-160">(Tüm istemci değerlerinden veri deposunda nedir üzerinde önceliklidir.) Bu bölüm için giriş eşzamanlılık işleme için kodlama yapmazsanız belirtildiği gibi bu otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-160">(All values from the client take precedence over what's in the data store.) As noted in the introduction to this section, if you don't do any coding for concurrency handling, this will happen automatically.</span></span>

* <span data-ttu-id="aed0e-161">Veritabanında güncelleştirilen Can'ın değişiklik engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-161">You can prevent John's change from being updated in the database.</span></span>

     <span data-ttu-id="aed0e-162">Genellikle, bir hata iletisi görüntüler, ona verilerin geçerli durumunu gösterir ve yine de bunları yapmak istediği, peter'in değişikliklerini uygulamak kendisine izin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-162">Typically, you would display an error message, show him the current state of the data, and allow him to reapply his changes if he still wants to make them.</span></span> <span data-ttu-id="aed0e-163">Bu adlı bir *Store WINS* senaryo.</span><span class="sxs-lookup"><span data-stu-id="aed0e-163">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="aed0e-164">(Veri deposu değerlerini istemci tarafından gönderilen değerler önceliklidir.) Bu öğreticide Store WINS senaryo uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="aed0e-164">(The data-store values take precedence over the values submitted by the client.) You'll implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="aed0e-165">Bu yöntem, neler olduğunu için uyarı bir kullanıcı olmaksızın herhangi bir değişiklik kılınmamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-165">This method ensures that no changes are overwritten without a user being alerted to what's happening.</span></span>

### <a name="detecting-concurrency-conflicts"></a><span data-ttu-id="aed0e-166">Eşzamanlılık çakışmaları algılama</span><span class="sxs-lookup"><span data-stu-id="aed0e-166">Detecting concurrency conflicts</span></span>

<span data-ttu-id="aed0e-167">İşleyerek çakışmalarını çözebilirsiniz `DbConcurrencyException` Entity Framework oluşturduğu özel durumları.</span><span class="sxs-lookup"><span data-stu-id="aed0e-167">You can resolve conflicts by handling `DbConcurrencyException` exceptions that the Entity Framework throws.</span></span> <span data-ttu-id="aed0e-168">Bu özel durumlar ne zaman öğrenmek için Entity Framework algılayamayabilir çakışmalar olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-168">In order to know when to throw these exceptions, the Entity Framework must be able to detect conflicts.</span></span> <span data-ttu-id="aed0e-169">Bu nedenle, veritabanı ve veri modeline uygun şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-169">Therefore, you must configure the database and the data model appropriately.</span></span> <span data-ttu-id="aed0e-170">Çakışma algılamasını etkinleştirmek için bazı seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aed0e-170">Some options for enabling conflict detection include the following:</span></span>

* <span data-ttu-id="aed0e-171">Veritabanı tablosunda bir satıra değiştirildiğinde belirlemek için kullanılan bir izleme sütunu içerir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-171">In the database table, include a tracking column that can be used to determine when a row has been changed.</span></span> <span data-ttu-id="aed0e-172">Daha sonra bu sütun nerede eklemek için Entity Framework yapılandırabilirsiniz SQL güncelleştirme veya silme komutlarını yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-172">You can then configure the Entity Framework to include that column in the Where clause of SQL Update or Delete commands.</span></span>

     <span data-ttu-id="aed0e-173">İzleme sütunun veri türü genellikle `rowversion`.</span><span class="sxs-lookup"><span data-stu-id="aed0e-173">The data type of the tracking column is typically `rowversion`.</span></span> <span data-ttu-id="aed0e-174">`rowversion` Satır güncelleştirilir her zaman artan sıralı bir sayı değeridir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-174">The `rowversion` value is a sequential number that's incremented each time the row is updated.</span></span> <span data-ttu-id="aed0e-175">Bir Update veya Delete komutu, Where yan tümcesi izleme sütunu (özgün satır sürümü) özgün değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-175">In an Update or Delete command, the Where clause includes the original value of the tracking column (the original row version) .</span></span> <span data-ttu-id="aed0e-176">Güncelleştirilen satır değeri başka bir kullanıcı tarafından değiştirildiyse `rowversion` Update veya Delete deyiminin Where nedeniyle güncelleştirilecek satırın bulmanız sütun özgün değerinden farklı yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-176">If the row being updated has been changed by another user, the value in the `rowversion` column is different than the original value, so the Update or Delete statement can't find the row to update because of the Where clause.</span></span> <span data-ttu-id="aed0e-177">Update veya Delete tarafından hiçbir satırın güncelleştirilmediği Entity Framework bulur (diğer bir deyişle, etkilenen satır sayısı sıfır olduğunda) komut olduğunda, bir eşzamanlılık çakışması yorumlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-177">When the Entity Framework finds that no rows have been updated by the Update or Delete command (that is, when the number of affected rows is zero), it interprets that as a concurrency conflict.</span></span>

* <span data-ttu-id="aed0e-178">Where tablosunda her sütun öğesinin özgün değerleri eklemek için Entity Framework yapılandırma Update ve Delete komutlarını yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-178">Configure the Entity Framework to include the original values of every column in the table in the Where clause of Update and Delete commands.</span></span>

     <span data-ttu-id="aed0e-179">İlk seçenek satırın ilk okunuşundan bu yana, sıradaki herhangi bir şey değiştiyse, olduğu gibi Where yan tümcesi bir satırı güncelleştirmek için iade kalmaz, Entity Framework bir eşzamanlılık çakışması yorumlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-179">As in the first option, if anything in the row has changed since the row was first read, the Where clause won't return a row to update, which the Entity Framework interprets as a concurrency conflict.</span></span> <span data-ttu-id="aed0e-180">Birçok sütunları olan veritabanı tabloları için bu yaklaşım çok büyük nerede sonuçlanabilir yan tümcesi ve büyük miktarlarda durumu bakımını gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-180">For database tables that have many columns, this approach can result in very large Where clauses, and can require that you maintain large amounts of state.</span></span> <span data-ttu-id="aed0e-181">Daha önce belirtildiği gibi büyük miktarlarda durumu bakımını yapma, uygulama performansını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-181">As noted earlier, maintaining large amounts of state can affect application performance.</span></span> <span data-ttu-id="aed0e-182">Bu nedenle bu yaklaşım genellikle önerilmez ve Bu öğreticide kullanılan yöntem değildir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-182">Therefore this approach is generally not recommended, and it isn't the method used in this tutorial.</span></span>

     <span data-ttu-id="aed0e-183">Eşzamanlılık için bu yaklaşımı uygulamak istiyorsanız, tüm birincil anahtar özellikleri ekleyerek eşzamanlılık için izlemek istediğiniz varlık işaretlemek sahip `ConcurrencyCheck` öznitelik.</span><span class="sxs-lookup"><span data-stu-id="aed0e-183">If you do want to implement this approach to concurrency, you have to mark all non-primary-key properties in the entity you want to track concurrency for by adding the `ConcurrencyCheck` attribute to them.</span></span> <span data-ttu-id="aed0e-184">Bu değişiklik tüm sütunları SQL Where yan tümcesinde Update ve Delete deyimleri dahil etmek Entity Framework sağlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-184">That change enables the Entity Framework to include all columns in the SQL Where clause of Update and Delete statements.</span></span>

<span data-ttu-id="aed0e-185">Bu öğreticinin geri kalanında, ekleyeceksiniz bir `rowversion` özelliği departmanı varlık izleme, bir denetleyici ve Görünüm ve her şeyin düzgün çalıştığını doğrulamak için sınama.</span><span class="sxs-lookup"><span data-stu-id="aed0e-185">In the remainder of this tutorial you'll add a `rowversion` tracking property to the Department entity, create a controller and views, and test to verify that everything works correctly.</span></span>

## <a name="add-a-tracking-property"></a><span data-ttu-id="aed0e-186">İzleme özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="aed0e-186">Add a tracking property</span></span>

<span data-ttu-id="aed0e-187">İçinde *Models/Department.cs*, RowVersion adlı izleme özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aed0e-187">In *Models/Department.cs*, add a tracking property named RowVersion:</span></span>

[!code-csharp[](intro/samples/cu/Models/Department.cs?name=snippet_Final&highlight=26,27)]

<span data-ttu-id="aed0e-188">`Timestamp` Özniteliği, bu sütun dahil olacağını belirtir Where yan tümcesi, Update ve Delete komutlarını veritabanına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-188">The `Timestamp` attribute specifies that this column will be included in the Where clause of Update and Delete commands sent to the database.</span></span> <span data-ttu-id="aed0e-189">Adlandırılan öznitelik `Timestamp` bir SQL SQL Server'ın önceki sürümlerinde kullanılan çünkü `timestamp` veri türü SQL önce `rowversion` değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-189">The attribute is called `Timestamp` because previous versions of SQL Server used a SQL `timestamp` data type before the SQL `rowversion` replaced it.</span></span> <span data-ttu-id="aed0e-190">.NET türü `rowversion` bir bayt dizisidir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-190">The .NET type for `rowversion` is a byte array.</span></span>

<span data-ttu-id="aed0e-191">Fluent API'sini kullanmayı tercih ederseniz kullanabilirsiniz `IsConcurrencyToken` yöntemi (içinde *Data/SchoolContext.cs*) aşağıdaki örnekte gösterildiği gibi izleme özelliği belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="aed0e-191">If you prefer to use the fluent API, you can use the `IsConcurrencyToken` method (in *Data/SchoolContext.cs*) to specify the tracking property, as shown in the following example:</span></span>

```csharp
modelBuilder.Entity<Department>()
    .Property(p => p.RowVersion).IsConcurrencyToken();
```

<span data-ttu-id="aed0e-192">Başka bir geçiş gerçekleştirmeniz gereken şekilde bir özellik ekleyerek veritabanı modeli değişti.</span><span class="sxs-lookup"><span data-stu-id="aed0e-192">By adding a property you changed the database model, so you need to do another migration.</span></span>

<span data-ttu-id="aed0e-193">Yaptığınız değişiklikleri kaydedin ve projeyi oluşturun ve sonra komut penceresinde aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="aed0e-193">Save your changes and build the project, and then enter the following commands in the command window:</span></span>

```console
dotnet ef migrations add RowVersion
```

```console
dotnet ef database update
```

## <a name="create-departments-controller-and-views"></a><span data-ttu-id="aed0e-194">Departmanlar denetleyici ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aed0e-194">Create Departments controller and views</span></span>

<span data-ttu-id="aed0e-195">Öğrenciler, kurslara ve Eğitmenler için daha önce yaptığınız gibi Departmanlar denetleyici ve görünüm iskelesini.</span><span class="sxs-lookup"><span data-stu-id="aed0e-195">Scaffold a Departments controller and views as you did earlier for Students, Courses, and Instructors.</span></span>

![İskele departmanı](concurrency/_static/add-departments-controller.png)

<span data-ttu-id="aed0e-197">İçinde *DepartmentsController.cs* dosya, departman Yöneticisi açılır listede Eğitmen tam adı yerine yalnızca son adını içerecek şekilde "tam"adı "FirstMidName" dört tüm oluşumlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-197">In the *DepartmentsController.cs* file, change all four occurrences of "FirstMidName" to "FullName" so that the department administrator drop-down lists will contain the full name of the instructor rather than just the last name.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_Dropdown)]

## <a name="update-index-view"></a><span data-ttu-id="aed0e-198">Dizini görünümünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aed0e-198">Update Index view</span></span>

<span data-ttu-id="aed0e-199">Yapı iskelesi altyapısı RowVersion sütun dizini Görünümü'nde oluşturulur, ancak bu alan görüntülenen olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-199">The scaffolding engine created a RowVersion column in the Index view, but that field shouldn't be displayed.</span></span>

<span data-ttu-id="aed0e-200">Değiştirin *Views/Departments/Index.cshtml* aşağıdaki kod ile.</span><span class="sxs-lookup"><span data-stu-id="aed0e-200">Replace the code in *Views/Departments/Index.cshtml* with the following code.</span></span>

[!code-html[](intro/samples/cu/Views/Departments/Index.cshtml?highlight=4,7,44)]

<span data-ttu-id="aed0e-201">Bu "Bölümler" başlığı değiştirir, RowVersion sütun siler ve yönetici için tam adı ad yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-201">This changes the heading to "Departments", deletes the RowVersion column, and shows full name instead of first name for the administrator.</span></span>

## <a name="update-edit-methods"></a><span data-ttu-id="aed0e-202">Düzenleme metotlarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="aed0e-202">Update Edit methods</span></span>

<span data-ttu-id="aed0e-203">Her iki HttpGet içinde `Edit` yöntemi ve `Details` yöntemi ekleme `AsNoTracking`.</span><span class="sxs-lookup"><span data-stu-id="aed0e-203">In both the HttpGet `Edit` method and the `Details` method, add `AsNoTracking`.</span></span> <span data-ttu-id="aed0e-204">İçinde HttpGet `Edit` yöntemi istekli yükleme için yönetici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-204">In the HttpGet `Edit` method, add eager loading for the Administrator.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_EagerLoading&highlight=2,3)]

<span data-ttu-id="aed0e-205">HttpPost için mevcut kodu değiştirin `Edit` yöntemini aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="aed0e-205">Replace the existing code for the HttpPost `Edit` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_EditPost)]

<span data-ttu-id="aed0e-206">Kod, güncelleştirilecek departman okumaya çalışarak başlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-206">The code begins by trying to read the department to be updated.</span></span> <span data-ttu-id="aed0e-207">Varsa `SingleOrDefaultAsync` yöntemi null değerini döndürür, departman, başka bir kullanıcı tarafından silindi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-207">If the `SingleOrDefaultAsync` method returns null, the department was deleted by another user.</span></span> <span data-ttu-id="aed0e-208">Bu durumda kod düzenleme sayfası, bir hata iletisi ile yeniden, böylece bir departman varlık oluşturmak için gönderilen form değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-208">In that case the code uses the posted form values to create a department entity so that the Edit page can be redisplayed with an error message.</span></span> <span data-ttu-id="aed0e-209">Alternatif olarak, departman alanları yeniden görüntüleme olmadan yalnızca bir hata iletisi görüntüler, departman varlık yeniden oluşturmak zorunda mıydı.</span><span class="sxs-lookup"><span data-stu-id="aed0e-209">As an alternative, you wouldn't have to re-create the department entity if you display only an error message without redisplaying the department fields.</span></span>

<span data-ttu-id="aed0e-210">Görünümün özgün depolar `RowVersion` değerini gizli bir alan ve bu yöntem değeri alan `rowVersion` parametresi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-210">The view stores the original `RowVersion` value in a hidden field, and this method receives that value in the `rowVersion` parameter.</span></span> <span data-ttu-id="aed0e-211">Çağırmadan önce `SaveChanges`, özgün moduna sahip `RowVersion` özellik değeri `OriginalValues` varlık için koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="aed0e-211">Before you call `SaveChanges`, you have to put that original `RowVersion` property value in the `OriginalValues` collection for the entity.</span></span>

```csharp
_context.Entry(departmentToUpdate).Property("RowVersion").OriginalValue = rowVersion;
```

<span data-ttu-id="aed0e-212">Entity Framework SQL güncelleştirme komut oluşturduğunda, bu komut, özgün sahip bir satır için görünen bir WHERE yan tümcesi içerecektir sonra `RowVersion` değeri.</span><span class="sxs-lookup"><span data-stu-id="aed0e-212">Then when the Entity Framework creates a SQL UPDATE command, that command will include a WHERE clause that looks for a row that has the original `RowVersion` value.</span></span> <span data-ttu-id="aed0e-213">Hiçbir satır güncelleştirme komutu tarafından etkileniyorsanız (hiçbir satır özgün sahip `RowVersion` değer), Entity Framework oluşturur bir `DbUpdateConcurrencyException` özel durum.</span><span class="sxs-lookup"><span data-stu-id="aed0e-213">If no rows are affected by the UPDATE command (no rows have the original `RowVersion` value),  the Entity Framework throws a `DbUpdateConcurrencyException` exception.</span></span>

<span data-ttu-id="aed0e-214">Bu özel durum için catch bloğu içindeki kod güncelleştirilmiş değerleri olan etkilenen departmanı varlık alır `Entries` özelliği özel durum nesnesi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-214">The code in the catch block for that exception gets the affected Department entity that has the updated values from the `Entries` property on the exception object.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?range=164)]

<span data-ttu-id="aed0e-215">`Entries` Koleksiyon yalnızca bir tane olacaktır `EntityEntry` nesne.</span><span class="sxs-lookup"><span data-stu-id="aed0e-215">The `Entries` collection will have just one `EntityEntry` object.</span></span>  <span data-ttu-id="aed0e-216">Bu nesne, kullanıcı tarafından girilen yeni değerler ve geçerli veritabanı değerlerini almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-216">You can use that object to get the new values entered by the user and the current database values.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?range=165-166)]

<span data-ttu-id="aed0e-217">Özel hata iletisi düzenleme girilen kullanıcı sayfasında veritabanı değerleri farklı olan her sütun için kod ekler (yalnızca bir alan burada gösterilmiştir kısa tutmak için).</span><span class="sxs-lookup"><span data-stu-id="aed0e-217">The code adds a custom error message for each column that has database values different from what the user entered on the Edit page (only one field is shown here for brevity).</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?range=174-178)]

<span data-ttu-id="aed0e-218">Son olarak, kod ayarlar `RowVersion` değerini `departmentToUpdate` yeni değere veritabanından alınır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-218">Finally, the code sets the `RowVersion` value of the `departmentToUpdate` to the new value retrieved from the database.</span></span> <span data-ttu-id="aed0e-219">Bu yeni `RowVersion` değeri depolanan gizli alanı sayfasını yeniden düzenleme ve sonraki kullanıcı çalıştırdığında **Kaydet**, yeniden düzenleme sayfası, yakalanan bu yana gerçekleşen eşzamanlılık hataları.</span><span class="sxs-lookup"><span data-stu-id="aed0e-219">This new `RowVersion` value will be stored in the hidden field when the Edit page is redisplayed, and the next time the user clicks **Save**, only concurrency errors that happen since the redisplay of the Edit page will be caught.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?range=199-200)]

<span data-ttu-id="aed0e-220">`ModelState.Remove` Deyimi, çünkü gereklidir `ModelState` eski olan `RowVersion` değeri.</span><span class="sxs-lookup"><span data-stu-id="aed0e-220">The `ModelState.Remove` statement is required because `ModelState` has the old `RowVersion` value.</span></span> <span data-ttu-id="aed0e-221">Görünümü'nde `ModelState` değerinin ikisi de mevcut olduğunda alan üzerinde model özellik değerlerini öncelik kazanır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-221">In the view, the `ModelState` value for a field takes precedence over the model property values when both are present.</span></span>

## <a name="update-edit-view"></a><span data-ttu-id="aed0e-222">Güncelleştirme düzenleme görünümü</span><span class="sxs-lookup"><span data-stu-id="aed0e-222">Update Edit view</span></span>

<span data-ttu-id="aed0e-223">İçinde *Views/Departments/Edit.cshtml*, aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="aed0e-223">In *Views/Departments/Edit.cshtml*, make the following changes:</span></span>

* <span data-ttu-id="aed0e-224">Kaydetmek için gizli bir alan ekleme `RowVersion` özellik değeri, gizli bir alan için takip `DepartmentID` özelliği.</span><span class="sxs-lookup"><span data-stu-id="aed0e-224">Add a hidden field to save the `RowVersion` property value, immediately following the hidden field for the `DepartmentID` property.</span></span>

* <span data-ttu-id="aed0e-225">Bir "Yönetici Seç" seçeneği aşağı açılan listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-225">Add a "Select Administrator" option to the drop-down list.</span></span>

[!code-html[](intro/samples/cu/Views/Departments/Edit.cshtml?highlight=16,34-36)]

## <a name="test-concurrency-conflicts"></a><span data-ttu-id="aed0e-226">Test eşzamanlılık çakışmaları</span><span class="sxs-lookup"><span data-stu-id="aed0e-226">Test concurrency conflicts</span></span>

<span data-ttu-id="aed0e-227">Uygulamayı çalıştırın ve Departmanlar dizin sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-227">Run the app and go to the Departments Index page.</span></span> <span data-ttu-id="aed0e-228">Sağ **Düzenle** seçin ve İngilizce departmanı için köprü **yeni sekmede aç**, ardından **Düzenle** İngilizce departmanı için köprü.</span><span class="sxs-lookup"><span data-stu-id="aed0e-228">Right-click the **Edit** hyperlink for the English department and select **Open in new tab**, then click the **Edit** hyperlink for the English department.</span></span> <span data-ttu-id="aed0e-229">İki tarayıcı sekmeleri artık aynı bilgiyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aed0e-229">The two browser tabs now display the same information.</span></span>

<span data-ttu-id="aed0e-230">İlk tarayıcı sekmesine bir alana değiştirin ve tıklatın **Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="aed0e-230">Change a field in the first browser tab and click **Save**.</span></span>

![Departman düzenleme değişikliğinden sonra sayfa 1](concurrency/_static/edit-after-change-1.png)

<span data-ttu-id="aed0e-232">Tarayıcı değişmiş değer ile dizin sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-232">The browser shows the Index page with the changed value.</span></span>

<span data-ttu-id="aed0e-233">İkinci bir tarayıcı sekmesinde bir alanı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-233">Change a field in the second browser tab.</span></span>

![Departman düzenleme değişikliğinden sonra sayfa 2](concurrency/_static/edit-after-change-2.png)

<span data-ttu-id="aed0e-235">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aed0e-235">Click **Save**.</span></span> <span data-ttu-id="aed0e-236">Bir hata iletisi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="aed0e-236">You see an error message:</span></span>

![Departman düzenleme sayfa hata iletisi](concurrency/_static/edit-error.png)

<span data-ttu-id="aed0e-238">Tıklayın **Kaydet** yeniden.</span><span class="sxs-lookup"><span data-stu-id="aed0e-238">Click **Save** again.</span></span> <span data-ttu-id="aed0e-239">İkinci tarayıcı sekmesinde girdiğiniz değer kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-239">The value you entered in the second browser tab is saved.</span></span> <span data-ttu-id="aed0e-240">Dizin Sayfası göründüğünde, kaydedilen değerler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-240">You see the saved values when the Index page appears.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="aed0e-241">Silme sayfası</span><span class="sxs-lookup"><span data-stu-id="aed0e-241">Update the Delete page</span></span>

<span data-ttu-id="aed0e-242">Silme sayfası için Entity Framework, birisi başka benzer bir şekilde bölüm düzenleme nedeni eşzamanlılık çakışmalarını algılar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-242">For the Delete page, the Entity Framework detects concurrency conflicts caused by someone else editing the department in a similar manner.</span></span> <span data-ttu-id="aed0e-243">Zaman HttpGet `Delete` yöntemi görüntüler onay görünümü, görünümün özgün içerir `RowVersion` gizli bir alan değeri.</span><span class="sxs-lookup"><span data-stu-id="aed0e-243">When the HttpGet `Delete` method displays the confirmation view, the view includes the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="aed0e-244">Değer ardından HttpPost için kullanılabilir olduğunu `Delete` kullanıcının silmeyi onaylaması çağrılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="aed0e-244">That value is then available to the HttpPost `Delete` method that's called when the user confirms the deletion.</span></span> <span data-ttu-id="aed0e-245">Entity Framework SQL DELETE komutu oluşturduğunda orijinal bir WHERE yan tümcesi içerdiğinden `RowVersion` değeri.</span><span class="sxs-lookup"><span data-stu-id="aed0e-245">When the Entity Framework creates the SQL DELETE command, it includes a WHERE clause with the original `RowVersion` value.</span></span> <span data-ttu-id="aed0e-246">Sıfır satır komutu sonuçları (satır silme onayı sayfasında görüntülenen sonra değiştirildiği anlamına gelir) etkileniyorsa, bir eşzamanlılık özel durum oluşturulur ve HttpGet `Delete` yöntemi görüntülemek için true olarak hata bayrak kümesi ile çağrılır bir hata iletisiyle onay sayfası.</span><span class="sxs-lookup"><span data-stu-id="aed0e-246">If the command results in zero rows affected (meaning the row was changed after the Delete confirmation page was displayed), a concurrency exception is thrown, and the HttpGet `Delete` method is called with an error flag set to true in order to redisplay the confirmation page with an error message.</span></span> <span data-ttu-id="aed0e-247">Bu durumda, hata iletisi görüntülenir, böylece satırın başka bir kullanıcı tarafından silindiğinden sıfır satır etkilenmiştir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="aed0e-247">It's also possible that zero rows were affected because the row was deleted by another user, so in that case no error message is displayed.</span></span>

### <a name="update-the-delete-methods-in-the-departments-controller"></a><span data-ttu-id="aed0e-248">Güncelleştirme Departmanlar denetleyicideki silme yöntemleri</span><span class="sxs-lookup"><span data-stu-id="aed0e-248">Update the Delete methods in the Departments controller</span></span>

<span data-ttu-id="aed0e-249">İçinde *DepartmentsController.cs*, HttpGet değiştirin `Delete` yöntemini aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="aed0e-249">In *DepartmentsController.cs*, replace the HttpGet `Delete` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_DeleteGet&highlight=1,10,14-17,21-29)]

<span data-ttu-id="aed0e-250">Yöntemi, bir eşzamanlılık hatası sonra sayfayı yeniden olup olmadığını belirten isteğe bağlı bir parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="aed0e-250">The method accepts an optional parameter that indicates whether the page is being redisplayed after a concurrency error.</span></span> <span data-ttu-id="aed0e-251">Bu bayrağı true olarak ayarlandığında ve artık departman var, başka bir kullanıcı tarafından silinmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-251">If this flag is true and the department specified no longer exists, it was deleted by another user.</span></span> <span data-ttu-id="aed0e-252">Bu durumda, kod dizin sayfasına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-252">In that case, the code redirects to the Index page.</span></span>  <span data-ttu-id="aed0e-253">Bu bayrağı true olarak ayarlandığında ve departman mevcut değilse, başka bir kullanıcı tarafından değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="aed0e-253">If this flag is true and the Department does exist, it was changed by another user.</span></span> <span data-ttu-id="aed0e-254">Bu durumda, kod görünümünü kullanarak bir hata iletisi gönderir `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="aed0e-254">In that case, the code sends an error message to the view using `ViewData`.</span></span>

<span data-ttu-id="aed0e-255">HttpPost değiştirin `Delete` yöntemi (adlı `DeleteConfirmed`) aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="aed0e-255">Replace the code in the HttpPost `Delete` method (named `DeleteConfirmed`) with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_DeletePost&highlight=1,3,5-8,11-18)]

<span data-ttu-id="aed0e-256">Yalnızca değiştirilen iskele kurulmuş kod içinde bu yöntem yalnızca bir kayıt kimliği kabul:</span><span class="sxs-lookup"><span data-stu-id="aed0e-256">In the scaffolded code that you just replaced, this method accepted only a record ID:</span></span>

```csharp
public async Task<IActionResult> DeleteConfirmed(int id)
```

<span data-ttu-id="aed0e-257">Model bağlayıcı tarafından oluşturulan bir bölüm varlık örneği için bu parametreyi değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-257">You've changed this parameter to a Department entity instance created by the model binder.</span></span> <span data-ttu-id="aed0e-258">Bu kayıt anahtarı yanı sıra RowVersion özellik değerinin EF erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-258">This gives EF access to the RowVersion property value in addition to the record key.</span></span>

```csharp
public async Task<IActionResult> Delete(Department department)
```

<span data-ttu-id="aed0e-259">Eylem yöntemi adından de değiştirdiğiniz `DeleteConfirmed` için `Delete`.</span><span class="sxs-lookup"><span data-stu-id="aed0e-259">You have also changed the action method name from `DeleteConfirmed` to `Delete`.</span></span> <span data-ttu-id="aed0e-260">İskele kurulan kodu kullanılan adı `DeleteConfirmed` HttpPost yöntem benzersiz bir imza vermek için.</span><span class="sxs-lookup"><span data-stu-id="aed0e-260">The scaffolded code used the name `DeleteConfirmed` to give the HttpPost method a unique signature.</span></span> <span data-ttu-id="aed0e-261">(CLR'nin farklı yöntem parametreleri sağlamak için aşırı yüklenmiş yöntemler gerektirir.) İmzaları benzersiz, MVC kuralı takılıyor ve HttpPost ve HttpGet silme yöntemleri için aynı adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="aed0e-261">(The CLR requires overloaded methods to have different method parameters.) Now that the signatures are unique, you can stick with the MVC convention and use the same name for the HttpPost and HttpGet delete methods.</span></span>

<span data-ttu-id="aed0e-262">Departman zaten silinmişse `AnyAsync` yöntem false döndürür ve uygulama yalnızca dizin yöntemine döner.</span><span class="sxs-lookup"><span data-stu-id="aed0e-262">If the department is already deleted, the `AnyAsync` method returns false and the application just goes back to the Index method.</span></span>

<span data-ttu-id="aed0e-263">Bir eşzamanlılık hatası yakalanmışsa kod silme onayı sayfası görüntüler ve bunu belirten bir bayrak eşzamanlılık hata iletisi görüntülenmelidir sağlar.</span><span class="sxs-lookup"><span data-stu-id="aed0e-263">If a concurrency error is caught, the code redisplays the Delete confirmation page and provides a flag that indicates it should display a concurrency error message.</span></span>

### <a name="update-the-delete-view"></a><span data-ttu-id="aed0e-264">Delete Görünümü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aed0e-264">Update the Delete view</span></span>

<span data-ttu-id="aed0e-265">İçinde *Views/Departments/Delete.cshtml*, iskele kurulan kodu bir hata iletisi alan ve gizli alanları DepartmentID ve RowVersion özellikleri ekleyen aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-265">In *Views/Departments/Delete.cshtml*, replace the scaffolded code with the following code that adds an error message field and hidden fields for the DepartmentID and RowVersion properties.</span></span> <span data-ttu-id="aed0e-266">Değişiklikler vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-266">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Departments/Delete.cshtml?highlight=9,38,44,45,48)]

<span data-ttu-id="aed0e-267">Bu, aşağıdaki değişiklikleri yapar:</span><span class="sxs-lookup"><span data-stu-id="aed0e-267">This makes the following changes:</span></span>

* <span data-ttu-id="aed0e-268">Bir hata iletisi arasında ekler `h2` ve `h3` başlıkları.</span><span class="sxs-lookup"><span data-stu-id="aed0e-268">Adds an error message between the `h2` and `h3` headings.</span></span>

* <span data-ttu-id="aed0e-269">FullName FirstMidName değiştirir **yönetici** alan.</span><span class="sxs-lookup"><span data-stu-id="aed0e-269">Replaces FirstMidName with FullName in the **Administrator** field.</span></span>

* <span data-ttu-id="aed0e-270">RowVersion alanını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="aed0e-270">Removes the RowVersion field.</span></span>

* <span data-ttu-id="aed0e-271">İçin gizli bir alan ekler `RowVersion` özelliği.</span><span class="sxs-lookup"><span data-stu-id="aed0e-271">Adds a hidden field for the `RowVersion` property.</span></span>

<span data-ttu-id="aed0e-272">Uygulamayı çalıştırın ve Departmanlar dizin sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-272">Run the app and go to the Departments Index page.</span></span> <span data-ttu-id="aed0e-273">Sağ tıklayın **Sil** seçin ve İngilizce departmanı için köprü **yeni sekmede aç**, birinci sekmede ardından **Düzenle** İngilizce departmanı için köprü.</span><span class="sxs-lookup"><span data-stu-id="aed0e-273">Right-click the **Delete** hyperlink for the English department and select **Open in new tab**, then in the first tab click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="aed0e-274">İlk penceresinde değerlerden birini değiştirin ve tıklayın **Kaydet**:</span><span class="sxs-lookup"><span data-stu-id="aed0e-274">In the first window, change one of the values, and click **Save**:</span></span>

![Bölüm silme önce değişiminin düzenleme sayfası](concurrency/_static/edit-after-change-for-delete.png)

<span data-ttu-id="aed0e-276">İkinci sekmesini tıklatın **Sil**.</span><span class="sxs-lookup"><span data-stu-id="aed0e-276">In the second tab, click **Delete**.</span></span> <span data-ttu-id="aed0e-277">Eşzamanlılık hata iletisini görüntüleyin ve departman değerlerini şu anda veritabanında nedir ile yenilenir.</span><span class="sxs-lookup"><span data-stu-id="aed0e-277">You see the concurrency error message, and the Department values are refreshed with what's currently in the database.</span></span>

![Eşzamanlılık hatası ile bölüm silme onay sayfası](concurrency/_static/delete-error.png)

<span data-ttu-id="aed0e-279">Tıklarsanız **Sil** yeniden departman silindiğini gösterir dizin sayfasına yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed0e-279">If you click **Delete** again, you're redirected to the Index page, which shows that the department has been deleted.</span></span>

## <a name="update-details-and-create-views"></a><span data-ttu-id="aed0e-280">Güncelleştirme ayrıntıları ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aed0e-280">Update Details and Create views</span></span>

<span data-ttu-id="aed0e-281">İsteğe bağlı olarak, iskele kurulan kodu ayrıntıları temizlemek ve görünümler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aed0e-281">You can optionally clean up scaffolded code in the Details and Create views.</span></span>

<span data-ttu-id="aed0e-282">Değiştirin *Views/Departments/Details.cshtml* RowVersion sütunu silin ve yöneticinin tam adı.</span><span class="sxs-lookup"><span data-stu-id="aed0e-282">Replace the code in *Views/Departments/Details.cshtml* to delete the RowVersion column and show the full name of the Administrator.</span></span>

[!code-html[](intro/samples/cu/Views/Departments/Details.cshtml?highlight=35)]

<span data-ttu-id="aed0e-283">Değiştirin *Views/Departments/Create.cshtml* Seç seçeneğini aşağı açılan listesine eklenecek.</span><span class="sxs-lookup"><span data-stu-id="aed0e-283">Replace the code in *Views/Departments/Create.cshtml* to add a Select option to the drop-down list.</span></span>

[!code-html[](intro/samples/cu/Views/Departments/Create.cshtml?highlight=32-34)]

## <a name="get-the-code"></a><span data-ttu-id="aed0e-284">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="aed0e-284">Get the code</span></span>

[<span data-ttu-id="aed0e-285">İndirme veya tamamlanmış uygulamanın görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-285">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="additional-resources"></a><span data-ttu-id="aed0e-286">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="aed0e-286">Additional resources</span></span>

 <span data-ttu-id="aed0e-287">EF Core eşzamanlılık nasıl ele alınacağını hakkında daha fazla bilgi için bkz. [eşzamanlılık çakışmalarını](/ef/core/saving/concurrency).</span><span class="sxs-lookup"><span data-stu-id="aed0e-287">For more information about how to handle concurrency in EF Core, see [Concurrency conflicts](/ef/core/saving/concurrency).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aed0e-288">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aed0e-288">Next steps</span></span>

<span data-ttu-id="aed0e-289">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="aed0e-289">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed0e-290">Eşzamanlılık çakışmalarını hakkında bilgi edindiniz</span><span class="sxs-lookup"><span data-stu-id="aed0e-290">Learned about concurrency conflicts</span></span>
> * <span data-ttu-id="aed0e-291">İzleme özelliği eklendi</span><span class="sxs-lookup"><span data-stu-id="aed0e-291">Added a tracking property</span></span>
> * <span data-ttu-id="aed0e-292">Oluşturulan bölümler denetleyici ve Görünüm</span><span class="sxs-lookup"><span data-stu-id="aed0e-292">Created Departments controller and views</span></span>
> * <span data-ttu-id="aed0e-293">Güncelleştirilmiş dizini görünümü</span><span class="sxs-lookup"><span data-stu-id="aed0e-293">Updated Index view</span></span>
> * <span data-ttu-id="aed0e-294">Düzenleme metotlarını güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="aed0e-294">Updated Edit methods</span></span>
> * <span data-ttu-id="aed0e-295">Güncelleştirilmiş düzenleme görünümü</span><span class="sxs-lookup"><span data-stu-id="aed0e-295">Updated Edit view</span></span>
> * <span data-ttu-id="aed0e-296">Test edilen eşzamanlılık çakışmaları</span><span class="sxs-lookup"><span data-stu-id="aed0e-296">Tested concurrency conflicts</span></span>
> * <span data-ttu-id="aed0e-297">Silme sayfası güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="aed0e-297">Updated the Delete page</span></span>
> * <span data-ttu-id="aed0e-298">Güncelleştirilen Ayrıntılar ve görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aed0e-298">Updated Details and Create views</span></span>

<span data-ttu-id="aed0e-299">Tablo başına hiyerarşi devralma Eğitmen ve Öğrenci varlıkların uygulama hakkında bilgi edinmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="aed0e-299">Advance to the next article to learn how to implement table-per-hierarchy inheritance for the Instructor and Student entities.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="aed0e-300">Tablo başına hiyerarşi devralma uygulama</span><span class="sxs-lookup"><span data-stu-id="aed0e-300">Implement table-per-hierarchy inheritance</span></span>](inheritance.md)
