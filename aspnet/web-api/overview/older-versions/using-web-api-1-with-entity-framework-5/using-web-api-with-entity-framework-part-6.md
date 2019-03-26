---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 'Bölüm 6: Ürün ve sipariş denetleyicileri oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: 21cfbd0bf691ea033e9a5a873ab49c83507750d5
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425970"
---
<a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="22300-102">Bölüm 6: Ürün ve Sipariş Denetleyicileri Oluşturma</span><span class="sxs-lookup"><span data-stu-id="22300-102">Part 6: Creating Product and Order Controllers</span></span>
====================
<span data-ttu-id="22300-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="22300-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="22300-104">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="22300-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="22300-105">Ürünleri denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="22300-105">Add a Products Controller</span></span>

<span data-ttu-id="22300-106">Yönetici, yönetici ayrıcalıklarına sahip kullanıcılar için denetleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="22300-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="22300-107">Müşteriler, diğer taraftan, ürünleri görüntülemek ancak oluşturulamıyor, güncelleştirme veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22300-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="22300-108">Biz kolayca erişim, Get yöntemleri açık bırakarak Post, Put ve Delete yöntemler ile kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22300-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="22300-109">Ancak, bir ürün için döndürülen veri bakın:</span><span class="sxs-lookup"><span data-stu-id="22300-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="22300-110">`ActualCost` Özelliği müşterilere görünebilir olmamalıdır!</span><span class="sxs-lookup"><span data-stu-id="22300-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="22300-111">Çözüm tanımlamaktır bir *veri aktarımı nesnesi* (DTO) bir alt kümesini müşterilere görünür olması gereken özellikleri içeren.</span><span class="sxs-lookup"><span data-stu-id="22300-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="22300-112">LINQ projenize kullanacağız `Product` için örnekler `ProductDTO` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="22300-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="22300-113">Adlı bir sınıf ekleyin `ProductDTO` modeller klasörü için.</span><span class="sxs-lookup"><span data-stu-id="22300-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="22300-114">Şimdi denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="22300-114">Now add the controller.</span></span> <span data-ttu-id="22300-115">Çözüm Gezgini'nde denetleyicileri klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22300-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="22300-116">Seçin **Ekle**, ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="22300-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="22300-117">İçinde **denetleyici Ekle** iletişim kutusunda, denetleyici adı &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="22300-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="22300-118">Altında **şablon**seçin **boş API denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="22300-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="22300-119">Kaynak dosyadaki her şeyi, aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="22300-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="22300-120">Denetleyici hala kullanıyor `OrdersContext` veritabanını sorgulamak için.</span><span class="sxs-lookup"><span data-stu-id="22300-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="22300-121">Ancak döndürmek yerine `Product` örnekleri doğrudan diyoruz `MapProducts` açtığına projeye `ProductDTO` örnekleri:</span><span class="sxs-lookup"><span data-stu-id="22300-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="22300-122">`MapProducts` Yöntemi döndürür bir **Iqueryable**, biz sonucu diğer sorgu parametreleri ile oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22300-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="22300-123">Bu konuda bkz `GetProduct` ekleyen yöntemi bir **burada** sorgu yan tümcesinin:</span><span class="sxs-lookup"><span data-stu-id="22300-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="22300-124">Orders denetleyicisinin Ekle</span><span class="sxs-lookup"><span data-stu-id="22300-124">Add an Orders Controller</span></span>

<span data-ttu-id="22300-125">Ardından, kullanıcıların siparişlerini görüntülemek ve oluşturmalarına olanak tanıyan bir denetleyici ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="22300-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="22300-126">Başka bir DTO ile başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="22300-126">We'll start with another DTO.</span></span> <span data-ttu-id="22300-127">Çözüm Gezgini'nde, modeller klasörü sağ tıklatın ve adlı bir sınıf ekleyin `OrderDTO` aşağıdaki uygulama kullanın:</span><span class="sxs-lookup"><span data-stu-id="22300-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="22300-128">Şimdi denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="22300-128">Now add the controller.</span></span> <span data-ttu-id="22300-129">Çözüm Gezgini'nde denetleyicileri klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22300-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="22300-130">Seçin **Ekle**, ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="22300-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="22300-131">İçinde **denetleyici Ekle** iletişim kutusunda aşağıdaki seçenekleri belirleyin:</span><span class="sxs-lookup"><span data-stu-id="22300-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="22300-132">Altında **Denetleyici adı**, "OrdersController" girin.</span><span class="sxs-lookup"><span data-stu-id="22300-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="22300-133">Altında **şablon**seçin "Entity Framework kullanarak okuma/yazma eylemleri olan API denetleyicisi".</span><span class="sxs-lookup"><span data-stu-id="22300-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="22300-134">Altında **Model sınıfı**seçin &quot;sırası (ProductStore.Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="22300-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="22300-135">Altında **veri bağlamı sınıfının**seçin &quot;OrdersContext (ProductStore.Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="22300-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="22300-136">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22300-136">Click **Add**.</span></span> <span data-ttu-id="22300-137">Bu OrdersController.cs adlı bir dosya ekler.</span><span class="sxs-lookup"><span data-stu-id="22300-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="22300-138">Ardından, varsayılan uygulama denetleyicisinin değiştirileceğini ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="22300-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="22300-139">İlk olarak, Sil `PutOrder` ve `DeleteOrder` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="22300-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="22300-140">Bu örnek için müşterilerin değiştiremez veya mevcut siparişlerin silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="22300-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="22300-141">Gerçek bir uygulamada çok sayıda arka uç mantığının bu durumları idare etmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="22300-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="22300-142">(Örneğin, sipariş zaten sevk?)</span><span class="sxs-lookup"><span data-stu-id="22300-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="22300-143">Değişiklik `GetOrders` yöntemi yalnızca bir kullanıcıya ait siparişlerini döndürmek için:</span><span class="sxs-lookup"><span data-stu-id="22300-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="22300-144">Değişiklik `GetOrder` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="22300-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="22300-145">Biz yönteme yapılan değişiklikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="22300-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="22300-146">Dönüş değeri bir `OrderDTO` örneği yerine bir `Order`.</span><span class="sxs-lookup"><span data-stu-id="22300-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="22300-147">Biz siparişi için veritabanını sorgulama, kullandığımız [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) ilgili getirilecek yöntemi `OrderDetail` ve `Product` varlıklar.</span><span class="sxs-lookup"><span data-stu-id="22300-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="22300-148">Biz, sonucu bir yansıtma kullanarak düzleştirin.</span><span class="sxs-lookup"><span data-stu-id="22300-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="22300-149">HTTP yanıt bir dizi miktarlar ürünleriyle içerir:</span><span class="sxs-lookup"><span data-stu-id="22300-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="22300-150">Bu biçim, iç içe geçmiş varlıkları (sipariş, ayrıntıları ve ürünleri) içeren özgün nesne grafiği, kullanmak istemcileri için kolaydır.</span><span class="sxs-lookup"><span data-stu-id="22300-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="22300-151">Bunu göz önüne almanız gereken son yöntemi `PostOrder`.</span><span class="sxs-lookup"><span data-stu-id="22300-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="22300-152">Şu anda, bu yöntem bir `Order` örneği.</span><span class="sxs-lookup"><span data-stu-id="22300-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="22300-153">Ne olacağını düşünün, ancak bir istemci bir istek gövdesi böyle gönderirse:</span><span class="sxs-lookup"><span data-stu-id="22300-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="22300-154">Bu iyi yapılandırılmış bir siparişi ve Entity Framework sonsuza dek bunun veritabanına ekler.</span><span class="sxs-lookup"><span data-stu-id="22300-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="22300-155">Ancak, önceden var olmayan bir ürün varlığı içerir.</span><span class="sxs-lookup"><span data-stu-id="22300-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="22300-156">İstemci, yalnızca veritabanımızda yer yeni ürün oluşturuldu!</span><span class="sxs-lookup"><span data-stu-id="22300-156">The client just created a new product in our database!</span></span> <span data-ttu-id="22300-157">Bunlar koala ayılarının için sipariş gördüğünüzde Bu siparişi yerine getirme departmanı şaşkınlık olacaktır.</span><span class="sxs-lookup"><span data-stu-id="22300-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="22300-158">Ahlaki, bir POST veya PUT isteği kabul veriler hakkında çok dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="22300-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="22300-159">Bu sorunu önlemek için değiştirme `PostOrder` gerçekleştirilecek yöntemi bir `OrderDTO` örneği.</span><span class="sxs-lookup"><span data-stu-id="22300-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="22300-160">Kullanım `OrderDTO` oluşturmak için `Order`.</span><span class="sxs-lookup"><span data-stu-id="22300-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="22300-161">Kullandığımız bildirimi `ProductID` ve `Quantity` özellikleri ve ürün adı veya fiyat için istemciye gönderilen herhangi bir değeri yoksayın.</span><span class="sxs-lookup"><span data-stu-id="22300-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="22300-162">Ürün Kimliği geçerli değilse, veritabanında yabancı anahtar kısıtlaması ihlal ve gerektiği gibi ekleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="22300-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="22300-163">İşte tam `PostOrder` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="22300-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="22300-164">Son olarak, ekleme **Authorize** özniteliği denetleyiciye:</span><span class="sxs-lookup"><span data-stu-id="22300-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="22300-165">Artık yalnızca kayıtlı kullanıcıların oluşturabilir veya siparişleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="22300-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22300-166">[Önceki](using-web-api-with-entity-framework-part-5.md)
> [İleri](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="22300-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
