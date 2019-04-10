---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Model bağlama ve web formlarını kullanan bir proje için iş mantığı katmanı ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisinde, model bağlama kullanarak bir ASP.NET Web formları projesi ile temel yönlerini gösterir. Model bağlama veri etkileşimi daha fazla düz - sağlar...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a229ebd71c913f3fe086892786988d0b3e42ec88
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59411585"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="01606-104">Model bağlama ve web formlarını kullanan bir proje için iş mantığı katmanı ekleme</span><span class="sxs-lookup"><span data-stu-id="01606-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="01606-105">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="01606-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="01606-106">Bu öğretici serisinde, model bağlama kullanarak bir ASP.NET Web formları projesi ile temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="01606-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="01606-107">Model bağlama, daha doğru verilerle ilgili kaynak nesne (örneğin, ObjectDataSource veya SqlDataSource) daha veri etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="01606-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="01606-108">Bu seri, tanıtım malzemeleri ile başlar ve sonraki öğreticilerde için daha gelişmiş kavramlar taşır.</span><span class="sxs-lookup"><span data-stu-id="01606-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="01606-109">Bu öğreticide, model bağlama iş mantığı katmanı ile kullanmak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="01606-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="01606-110">Geçerli sayfanın dışında bir nesne veri yöntemleri çağırmak için kullanıldığını belirtmek için OnCallingDataMethods üye ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="01606-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="01606-111">Bu öğreticide oluşturulan proje geliştirir [önceki](retrieving-data.md) dizisinin bölümleri.</span><span class="sxs-lookup"><span data-stu-id="01606-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="01606-112">Yapabilecekleriniz [indirme](https://go.microsoft.com/fwlink/?LinkId=286116) tam projeyi C# veya vb</span><span class="sxs-lookup"><span data-stu-id="01606-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="01606-113">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="01606-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="01606-114">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklıdır Visual Studio 2012 şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="01606-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="01606-115">Derleme</span><span class="sxs-lookup"><span data-stu-id="01606-115">What you'll build</span></span>

<span data-ttu-id="01606-116">Model bağlama, veri etkileşimi kodunuzu bir web sayfası için arka plan kod dosyasında veya ayrı iş mantığı sınıfı yerleştirilmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="01606-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="01606-117">Önceki öğreticilerde, arka plan kod dosyaları için veri etkileşim kodu kullanma göstermiştir.</span><span class="sxs-lookup"><span data-stu-id="01606-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="01606-118">Bu yaklaşım küçük siteler için çalışır ancak büyük bir site bakımı yapılırken kod yinelemesi ve büyük zorluk açabilir.</span><span class="sxs-lookup"><span data-stu-id="01606-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="01606-119">Ayrıca programlı olarak Soyutlama Katmanı olduğundan, arka plan kod dosyalarını bulunan kodu test etmek oldukça zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="01606-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="01606-120">Veri etkileşim kodu merkezileştirmek için tüm verilerle etkileşim kurmak için mantığı içeren bir iş mantığı katmanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01606-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="01606-121">Ardından web sayfalarınızdan iş mantığı katmanı çağırın.</span><span class="sxs-lookup"><span data-stu-id="01606-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="01606-122">Bu öğreticide, tüm iş mantığı katmanı içine önceki öğreticilerde yazdığınız kodun taşıyın ve sonra bu kodu sayfalarından gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="01606-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="01606-123">Bu öğreticide, gerekir:</span><span class="sxs-lookup"><span data-stu-id="01606-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="01606-124">Kod, iş mantığı katmanı için arka plan kod dosyaları Taşı</span><span class="sxs-lookup"><span data-stu-id="01606-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="01606-125">Değişiklik iş mantığı katmanı yöntemleri çağırmak için veri bağlama denetimleri</span><span class="sxs-lookup"><span data-stu-id="01606-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="01606-126">İş mantığı katmanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="01606-126">Create business logic layer</span></span>

<span data-ttu-id="01606-127">Şimdi web sayfalarından adlı bir sınıf oluşturur.</span><span class="sxs-lookup"><span data-stu-id="01606-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="01606-128">Bu sınıftaki yöntemlerin önceki öğreticilerdeki kullanılan yöntemlere benzer ve değer sağlayıcısı özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="01606-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="01606-129">İlk olarak, adlı yeni bir klasör ekleyin **BLL**.</span><span class="sxs-lookup"><span data-stu-id="01606-129">First, add a new folder called **BLL**.</span></span>

![Klasör Ekle](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="01606-131">BLL klasöründe adlı yeni bir sınıf oluşturun **SchoolBL.cs**.</span><span class="sxs-lookup"><span data-stu-id="01606-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="01606-132">Tüm arka plan kod dosyalarında başlangıçta belgeler veri işlemlerini içerecektir.</span><span class="sxs-lookup"><span data-stu-id="01606-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="01606-133">Yöntemleri neredeyse arka plan kod dosyasındaki yöntemleri ile aynıdır, ancak bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="01606-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="01606-134">Artık kod örneği içinde yürütülen dikkat edilecek en önemli bir değişiklik olduğunu **sayfa** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="01606-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="01606-135">Sayfa sınıfını içeren **TryUpdateModel** yöntemi ve **ModelState** özelliği.</span><span class="sxs-lookup"><span data-stu-id="01606-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="01606-136">Bu kod, iş mantığı katmanı için taşındığında, bu üyeleri çağırmak için sayfa sınıfının bir örneği artık yok.</span><span class="sxs-lookup"><span data-stu-id="01606-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="01606-137">Bu sorunu aşmak için eklemelisiniz bir **ModelMethodContext** TryUpdateModel veya ModelState erişen herhangi bir yönteme parametre.</span><span class="sxs-lookup"><span data-stu-id="01606-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="01606-138">TryUpdateModel arayın veya ModelState almak için bu ModelMethodContext parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="01606-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="01606-139">Bu yeni bir parametre için hesap için bu web sayfasında herhangi bir ayarı değiştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="01606-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="01606-140">SchoolBL.cs kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="01606-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="01606-141">İş mantığı katmanından veri almak için var olan sayfaları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="01606-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="01606-142">Son olarak, sorgular kullanarak iş mantığı katmanı kullanarak arka plan kod dosyasında Students.aspx AddStudent.aspx ve Courses.aspx sayfaları dönüştürülecektir.</span><span class="sxs-lookup"><span data-stu-id="01606-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="01606-143">Öğrenciler, AddStudent ve kurslar için arka plan kod dosyalarında silin veya açıklama olarak aşağıdaki sorgu metotları:</span><span class="sxs-lookup"><span data-stu-id="01606-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="01606-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="01606-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="01606-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="01606-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="01606-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="01606-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="01606-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="01606-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="01606-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="01606-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="01606-149">Veri işlemleri ilgili arka plan kod dosyasındaki kod şimdi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="01606-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="01606-150">**OnCallingDataMethods** olay işleyicisi veri yöntemleri için kullanılacak bir nesne belirtmenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="01606-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="01606-151">Students.aspx, bu olay işleyicisi için bir değer ekleyin ve iş mantığı sınıftaki yöntemlerin adlarına veri yöntemlerin adlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="01606-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="01606-152">Students.aspx arka plan kod dosyasında CallingDataMethods olayı için olay işleyicisini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="01606-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="01606-153">Bu olay işleyicisinde veri işlemleri için iş mantığı sınıf belirtin.</span><span class="sxs-lookup"><span data-stu-id="01606-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="01606-154">AddStudent.aspx benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="01606-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="01606-155">Courses.aspx benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="01606-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="01606-156">Uygulamayı çalıştırmak ve daha önce olduğu gibi tüm sayfaları işlev dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="01606-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="01606-157">Doğrulama mantığını ayrıca düzgün çalışır.</span><span class="sxs-lookup"><span data-stu-id="01606-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="01606-158">Sonuç</span><span class="sxs-lookup"><span data-stu-id="01606-158">Conclusion</span></span>

<span data-ttu-id="01606-159">Bu öğreticide, bir veri erişim katmanı ve iş mantığı katmanı kullanmak için uygulamanızı yeniden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="01606-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="01606-160">Belirttiğiniz veri denetimleri veri işlemleri için geçerli sayfa değil bir nesne kullanın.</span><span class="sxs-lookup"><span data-stu-id="01606-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="01606-161">Önceki</span><span class="sxs-lookup"><span data-stu-id="01606-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
