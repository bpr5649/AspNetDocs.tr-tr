---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 'Bölüm 4: Ürünleri listeleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 4. Bölüm GridView Sözl ile ürünleri listeleme kapsayan...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131013"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="d3187-104">Bölüm 4: Ürünleri Listeleme</span><span class="sxs-lookup"><span data-stu-id="d3187-104">Part 4: Listing Products</span></span>

<span data-ttu-id="d3187-105">tarafından [ALi Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d3187-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="d3187-106">Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3187-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="d3187-107">Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3187-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="d3187-108">Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3187-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="d3187-109">4. Bölüm GridView denetimi ile ürünleri listeleme kapsar.</span><span class="sxs-lookup"><span data-stu-id="d3187-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a>  <span data-ttu-id="d3187-110">GridView denetimi ile ürünleri listeleme</span><span class="sxs-lookup"><span data-stu-id="d3187-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="d3187-111">"Sağ tıklayarak" ProductsList.aspx sayfamızı uygulama Çözümümüzü ve "Ekle" ve "Yeni öğe" seçerek başlayalım.</span><span class="sxs-lookup"><span data-stu-id="d3187-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="d3187-112">"Web formu kullanarak ana sayfa" öğesini seçin ve ProductsList.aspx sayfa adını".</span><span class="sxs-lookup"><span data-stu-id="d3187-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="d3187-113">"Ekle" ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d3187-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="d3187-114">Sonraki biz Site.Master sayfanın nereye yerleştirileceğini "Stilleri" klasörü seçin ve "Klasörünün içeriğini" penceresinden seçin.</span><span class="sxs-lookup"><span data-stu-id="d3187-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="d3187-115">Sayfayı oluşturmak için "Tamam"'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d3187-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="d3187-116">Veritabanımızdaki aşağıda görüldüğü gibi ürün verilerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="d3187-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="d3187-117">Sayfamızı oluşturulduktan sonra yeniden bir varlık veri kaynağı bu ürün verilere erişmek için kullanacağız ancak bu örnekte ürün varlıkları seçmeliyiz ve yalnızca seçilen kategori için döndürülen öğeleri sınırlamak gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="d3187-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="d3187-118">Bunu gerçekleştirmek için otomatik oluşturmak için EntityDataSource WHERE yan tümcesi anlatılır ve biz WhereParameter belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3187-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="d3187-119">Bizim "ürün kategorisi menüde" menü öğelerini oluşturduğumuz zaman dinamik olarak bağlantı CategoryID her bağlantı için sorgu dizesini ekleyerek oluşturduk, Hatırlayacağınız.</span><span class="sxs-lookup"><span data-stu-id="d3187-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="d3187-120">Biz bu QueryString parametresi nerede parametresi türetmek için varlık veri kaynağını bildirir.</span><span class="sxs-lookup"><span data-stu-id="d3187-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="d3187-121">Ardından, ürünlerin listesini görüntülemek için ListView denetimi yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="d3187-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="d3187-122">En iyi bir alışveriş deneyimi oluşturmak için sizi birkaç kısa özellik bizim ListVew içinde gösterilen her bir ürün düzenlenecek.</span><span class="sxs-lookup"><span data-stu-id="d3187-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="d3187-123">Ürün adı, ürün ayrıntılı görünüm bağlantısı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d3187-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="d3187-124">Ürünün fiyatını görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d3187-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="d3187-125">Ürün görüntüsü görüntülenir ve dinamik olarak görüntüyü bir katalog görüntüleri dizinden uygulamamız içinde seçeneğini belirleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d3187-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="d3187-126">Biz, hemen ürününün alışveriş sepetine eklemek için bir bağlantı bulunur.</span><span class="sxs-lookup"><span data-stu-id="d3187-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="d3187-127">Bizim ListView denetimi örneği için biçimlendirme şöyledir.</span><span class="sxs-lookup"><span data-stu-id="d3187-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="d3187-128">Biz, dinamik olarak görüntülenen her ürün için çeşitli bağlantılar oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="d3187-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="d3187-129">Ayrıca, kendi yeni sayfa test ederiz önce ürün için dizin yapısına şu şekilde Kataloğu görüntüleri oluşturmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3187-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="d3187-130">Ürün görüntülerimizi erişilebilir olduğunda, ürün listesi sayfamızı sınayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="d3187-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="d3187-131">Sitenin giriş sayfasından, kategori listesi bağlantılardan birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d3187-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="d3187-132">Artık ProductDetails.aspx sayfası ve AddToCart işlevselliği uygulamak ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="d3187-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="d3187-133">Dosya - kullanma&gt;yeni bir sayfa adı daha önce yaptığımız gibi sitenin ana sayfasını kullanarak ProductDetails.aspx oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d3187-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="d3187-134">Biz yeniden EntityDataSource denetimi veritabanında belirli bir ürün kaydı erişmek için kullanacağı ve ASP.NET FormView denetimi gibi ürün verilerini görüntülemek için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d3187-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="d3187-135">Biçimlendirme bir bit size komik olmadıysa endişelenmeyin.</span><span class="sxs-lookup"><span data-stu-id="d3187-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="d3187-136">Ekran düzenini odada birkaç biz daha sonra uygulayacaksınız özellikleri için yukarıdaki biçimlendirme bırakır.</span><span class="sxs-lookup"><span data-stu-id="d3187-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="d3187-137">Alışveriş sepeti uygulamamızı daha karmaşık mantık temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d3187-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="d3187-138">Başlamak için dosya - kullanma&gt;MyShoppingCart.aspx adlı bir sayfa oluşturmak için yeni.</span><span class="sxs-lookup"><span data-stu-id="d3187-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="d3187-139">Biz ShoppingCart.aspx adı almadığınızdan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d3187-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="d3187-140">Veritabanımızdaki "ShoppingCart" adında bir tablo içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d3187-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="d3187-141">Biz oluşturulan bir varlık veri modeli, veritabanındaki her tablo için bir sınıf oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d3187-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="d3187-142">Bu nedenle, varlık veri modeli "ShoppingCart" adında bir varlık sınıfı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d3187-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="d3187-143">Modeli böylece biz alışveriş sepeti kararlılığımızın için bu adı kullanın veya ilişkin genişletmek ancak biz yalnızca çakışma kaçınır bir ad seçmek için bunun yerine benimseyeceksiniz düzenlemek.</span><span class="sxs-lookup"><span data-stu-id="d3187-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="d3187-144">Ayrıca biz basit bir alışveriş sepeti oluşturacağınız belirterek ve alışveriş sepeti mantığı ile alışveriş sepetini görüntüleme katıştırma değer olur.</span><span class="sxs-lookup"><span data-stu-id="d3187-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="d3187-145">Biz de tamamen ayrı bir iş katmanında alışveriş sepetimizi uygulamak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3187-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d3187-146">[Önceki](tailspin-spyworks-part-3.md)
> [İleri](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="d3187-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
