---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Kullanarak Entity Framework 4.0 ve ObjectDataSource Denetimi, 3. Bölüm: Sıralama ve filtreleme | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisinde, kullanmaya başlama Entity Framework 4.0 öğretici serisinin tarafından oluşturulan Contoso University web uygulaması oluşturur. BEN...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 19726a728fc6d94552c315b38315a29c269d97db
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59380424"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="c4fb6-104">Kullanarak Entity Framework 4.0 ve ObjectDataSource Denetimi, 3. Bölüm: Sıralama ve Filtreleme</span><span class="sxs-lookup"><span data-stu-id="c4fb6-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="c4fb6-105">tarafından [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c4fb6-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="c4fb6-106">Bu öğretici serisinde Contoso University web uygulaması tarafından oluşturulan geliştirir [Entity Framework 4.0 ile çalışmaya başlama](https://asp.net/entity-framework/tutorials#Getting%20Started) öğretici serisi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="c4fb6-107">Önceki öğreticilerde tamamlanmadıysa, Bu öğretici için bir başlangıç noktası olarak yapabilecekleriniz [uygulamayı karşıdan](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) oluşturmuş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="c4fb6-108">Ayrıca [uygulamayı karşıdan](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) tam öğretici serisinin tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="c4fb6-109">Öğreticileri hakkında sorularınız varsa, bunları gönderebilir [ASP.NET Entity Framework Forumu](https://forums.asp.net/1227.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4fb6-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="c4fb6-110">Önceki öğreticide Entity Framework kullanan bir n katmanlı web uygulamasında depo deseni uygulanan ve `ObjectDataSource` denetimi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="c4fb6-111">Bu öğreticide, sıralama ve filtreleme yapmak ve ana öğe-ayrıntı senaryoları işlemek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="c4fb6-112">Aşağıdaki gibi iyileştirmeyi ekleyeceksiniz *Departments.aspx* sayfası:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="c4fb6-113">Departmanlar adına göre seçmek kullanıcılara izin vermek için metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="c4fb6-114">Kılavuzda gösterilen her departman kursları listesi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="c4fb6-115">Sütun başlıklarını tıklatarak sıralama olanağı.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-115">The ability to sort by clicking column headings.</span></span>

[![I<span data-ttu-id="c4fb6-116">mage01]</span><span class="sxs-lookup"><span data-stu-id="c4fb6-116">mage01]</span></span>(using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="c4fb6-117">GridView Sütun sıralama özelliği ekleme</span><span class="sxs-lookup"><span data-stu-id="c4fb6-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="c4fb6-118">Açık *Departments.aspx* sayfa ve ekleme bir `SortParameterName="sortExpression"` özniteliğini `ObjectDataSource` adlı Denetim `DepartmentsObjectDataSource`.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="c4fb6-119">(Daha sonra oluşturacağınız bir `GetDepartments` adlı bir parametresi alan yöntemi `sortExpression`.) Açılış etiketinde denetimi için biçimlendirme artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="c4fb6-120">Ekleme `AllowSorting="true"` özniteliği öğesinin açılış etiketinde `GridView` denetimi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="c4fb6-121">Açılış etiketinde denetimi için biçimlendirme artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="c4fb6-122">İçinde *Departments.aspx.cs*, çağırarak varsayılan sıralama düzenini ayarlayın `GridView` denetimin `Sort` yönteminden `Page_Load` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="c4fb6-123">İş mantığı sınıfı veya depo sınıfını sıralar veya filtreleri kod ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="c4fb6-124">İş mantığı sınıfı, bunu yaparsanız, veritabanından verilerin alındıktan sonra ile iş mantığı sınıfı çalıştığından sıralama veya filtreleme iş yapılır bir `IEnumerable` deposu tarafından döndürülen nesne.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="c4fb6-125">Sıralama ve filtreleme depo sınıfını kodda ekleyin ve bir LINQ ifadesini önce bunu ya da nesne sorgusu için dönüştürülmüş bir `IEnumerable` komutlarınızı geçirilir aracılığıyla veritabanı, genellikle daha verimli bir işlem için nesne.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="c4fb6-126">Bu öğreticide, sıralama ve filtreleme işlemi veritabanı tarafından yapılacak neden olan bir yolla uygulayacaksınız — diğer bir deyişle, depodaki.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="c4fb6-127">Sıralama özelliği eklemek için depo arabirimi ve depo sınıfları da iş mantığı sınıfı için yeni bir yöntem eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="c4fb6-128">İçinde *ISchoolRepository.cs* dosya, yeni bir `GetDepartments` gereken yöntemini bir `sortExpression` döndürülen bölümleri sıralamak için kullanılacak parametre:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="c4fb6-129">`sortExpression` Sıralanacak sütunu ve sıralama yönünü parametre belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="c4fb6-130">Yeni bir yönteme için kod ekleme *SchoolRepository.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="c4fb6-131">Parametresiz varolan değiştirme `GetDepartments` yeni yöntemini çağırmak için yöntem:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="c4fb6-132">Test projesinde aşağıdaki yeni yöntemi ekleyin *MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="c4fb6-133">Bu metot üzerinde sıralanmış listesini döndüren bir işleve bağımlı herhangi bir birim test oluşturacağınız döndürmeden önce listeyi sıralamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="c4fb6-134">Yöntemi yalnızca bölümlerin Sıralanmamış liste dönebilmeniz testleri gibi Bu öğreticide, oluşturduğunuz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="c4fb6-135">İçinde *SchoolBL.cs* iş mantığı sınıfına aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="c4fb6-136">Bu kod sıralama parametresi depo yönteme geçirir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="c4fb6-137">Çalıştırma *Departments.aspx* sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-137">Run the *Departments.aspx* page.</span></span>

[![I<span data-ttu-id="c4fb6-138">mage02]</span><span class="sxs-lookup"><span data-stu-id="c4fb6-138">mage02]</span></span>(using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

<span data-ttu-id="c4fb6-139">Artık, herhangi bir sütuna göre sıralamak için sütunun başlığına da tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="c4fb6-140">Sütun zaten sıraladıysanız başlığına tıklayarak sıralama yönünü tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="c4fb6-141">Bir arama kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="c4fb6-141">Adding a Search Box</span></span>

<span data-ttu-id="c4fb6-142">Bu bölümde, arama metin kutusu ekleme, gerekir bağlantısına `ObjectDataSource` denetim parametresini kullanarak denetlemek ve Filtrelemeyi desteklemek üzere iş mantığı sınıfına bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="c4fb6-143">Açık *Departments.aspx* sayfasında ve başlık ve ilk arasında aşağıdaki işaretlemeyi ekleyin `ObjectDataSource` denetimi:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="c4fb6-144">İçinde `ObjectDataSource` adlı Denetim `DepartmentsObjectDataSource`, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="c4fb6-145">Ekleme bir `SelectParameters` adlı bir parametre için öğe `nameSearchString` girilen değerin alır `SearchTextBox` denetimi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="c4fb6-146">Değişiklik `SelectMethod` öznitelik değerine `GetDepartmentsByName`.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="c4fb6-147">(Daha sonra bu yöntem oluşturacaksınız.)</span><span class="sxs-lookup"><span data-stu-id="c4fb6-147">(You'll create this method later.)</span></span>

<span data-ttu-id="c4fb6-148">İşaretleme için `ObjectDataSource` denetimi artık aşağıdaki örnekte benzer:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="c4fb6-149">İçinde *ISchoolRepository.cs*, ekleme bir `GetDepartmentsByName` yönteminin hem de alan `sortExpression` ve `nameSearchString` parametreleri:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="c4fb6-150">İçinde *SchoolRepository.cs*, aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="c4fb6-151">Bu kod bir `Where` arama dizesini içeren öğelerini seçmek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="c4fb6-152">Arama dizesi boş ise, tüm kayıtları seçilir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="c4fb6-153">Yöntem çağrıları birlikte böyle bir ifade belirttiğinizde unutmayın (`Include`, ardından `OrderBy`, ardından `Where`), `Where` yöntemi her zaman son olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="c4fb6-154">Varolan değiştirme `GetDepartments` gereken yöntemini bir `sortExpression` parametresini kullanarak yeni yöntemi çağırın:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="c4fb6-155">İçinde *MockSchoolRepository.cs* test projesinde aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="c4fb6-156">İçinde *SchoolBL.cs*, aşağıdaki yeni yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="c4fb6-157">Çalıştırma *Departments.aspx* sayfasında ve seçim mantığını çalıştığından emin olmak için bir arama dizesini girin.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="c4fb6-158">Metin kutusunu boş bırakın ve tüm kayıtlar döndürülür emin olmak için bir arama deneyin.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

[![I<span data-ttu-id="c4fb6-159">mage03]</span><span class="sxs-lookup"><span data-stu-id="c4fb6-159">mage03]</span></span>(using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="c4fb6-160">Ayrıntılar sütunu için her bir ızgara satır ekleme</span><span class="sxs-lookup"><span data-stu-id="c4fb6-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="c4fb6-161">Ardından, tüm kursları kılavuzunun sağ hücrede görüntülenen her departman için görmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="c4fb6-162">Bunu yapmak için iç içe bir kullanacağınız `GridView` denetim ve veri bağlama için verileri `Courses` gezinti özelliği `Department` varlık.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="c4fb6-163">Açık *Departments.aspx* ve için biçimlendirme `GridView` denetimi bir işleyici belirtmek için `RowDataBound` olay.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="c4fb6-164">Açılış etiketinde denetimi için biçimlendirme artık aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="c4fb6-165">Yeni bir `TemplateField` öğeden sonra `Administrator` şablonu:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="c4fb6-166">Bu işaretleme iç içe bir oluşturur `GridView` kurs sayısını ve başlığını kursları listesini gösteren denetimdir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="c4fb6-167">Databind gerekir çünkü bir veri kaynağı belirtmiyor kod içinde `RowDataBound` işleyici.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="c4fb6-168">Açık *Departments.aspx.cs* ve eklemek için aşağıdaki işleyicisi `RowDataBound` olay:</span><span class="sxs-lookup"><span data-stu-id="c4fb6-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="c4fb6-169">Bu kod alır `Department` olay bağımsız değişkenleri varlıktan dönüştürür `Courses` gezinme özelliği için bir `List` koleksiyona ve iç içe databinds `GridView` koleksiyonuna.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="c4fb6-170">Açık *SchoolRepository.cs* istekli yükleme için belirtin ve dosya `Courses` çağırarak gezinti özelliği `Include` oluşturduğunuz nesne sorgusu yönteminde `GetDepartmentsByName` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="c4fb6-171">`return` Deyiminde `GetDepartmentsByName` yöntemi artık aşağıdaki örnekte benzer.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="c4fb6-172">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-172">Run the page.</span></span> <span data-ttu-id="c4fb6-173">Sıralama ve filtreleme, daha önce eklediğiniz özelliği yanı sıra GridView denetiminde artık her departman için iç içe geçmiş kurs ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

[![I<span data-ttu-id="c4fb6-174">mage01]</span><span class="sxs-lookup"><span data-stu-id="c4fb6-174">mage01]</span></span>(using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

<span data-ttu-id="c4fb6-175">Bu sıralama, filtreleme ve ana öğe-ayrıntı senaryoları giriş tamamlar.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="c4fb6-176">Sonraki öğreticide eşzamanlılık nasıl ele alınacağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c4fb6-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4fb6-177">[Önceki](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [İleri](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="c4fb6-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
