---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 'Bölüm 8: Ajax güncelleştirmeleriyle alışveriş | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır. 8. Bölüm Ajax güncelleştirmeleriyle alışveriş sepeti kapsar.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 2ba210d8c541c6c330dda74706470fa73a81474a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379488"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="a48a7-104">Bölüm 8: Ajax Güncelleştirmeleriyle Alışveriş Sepeti</span><span class="sxs-lookup"><span data-stu-id="a48a7-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="a48a7-105">tarafından [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="a48a7-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="a48a7-106">MVC müzik Store tanıtır ve ASP.NET MVC ve Visual Studio web geliştirme için nasıl kullanılacağını adım adım anlatan bir öğretici uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="a48a7-107">MVC müzik Store müzik albümleri çevrimiçi sattığı ve temel site yönetimi, kullanıcı oturum açma ve alışveriş sepeti işlevselliğini uygulayan bir Basit örnek deposu uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="a48a7-108">Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="a48a7-109">8. Bölüm Ajax güncelleştirmeleriyle alışveriş sepeti kapsar.</span><span class="sxs-lookup"><span data-stu-id="a48a7-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>


<span data-ttu-id="a48a7-110">Kayıt olmadan kendi arabasında albümleri yerleştirmek kullanıcılar izin veriyoruz, ancak bunlar tam kullanıma Konukları olarak kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="a48a7-111">Alışveriş ve kullanıma alma işlemi iki denetleyicilerine ayrılacaktır: anonim olarak öğe için bir sepet ekleme izin veren bir ShoppingCart denetleyicisi ve kullanıma alma işlemi yürüten bir kullanıma alma denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="a48a7-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="a48a7-112">Biz bu bölümdeki alışveriş sepetine ile başlayın, ardından derleme aşağıdaki bölümünde kullanıma alma işlemi.</span><span class="sxs-lookup"><span data-stu-id="a48a7-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="a48a7-113">Sepet, sırası ve OrderDetail model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="a48a7-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="a48a7-114">Bizim alışveriş sepeti ve kullanıma alma işlemleri yapar bazı yeni sınıflarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a48a7-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="a48a7-115">Modeller klasörü sağ tıklatın ve aşağıdaki kod ile sepet sınıfı (Cart.cs) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="a48a7-116">Bu sınıf ana kadar [anahtarı] özniteliği için kayıt kimliği özelliği dışında kullandığımız başkalarına oldukça benzerdir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="a48a7-117">Bizim sepet öğeleri anonim alışveriş izin vermek için CartID adlı bir dize tanımlayıcısına sahip olacaktır, ancak tablo RecordID adlı bir tamsayı birincil anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="a48a7-118">Kural gereği, Entity Framework Code-First, sepet adlı bir tablo için birincil anahtarı CartId veya kimliği olacaktır, ancak biz istiyorsanız biz kolayca, ek açıklamalar veya kod yoluyla kılabilirsiniz bekliyor.</span><span class="sxs-lookup"><span data-stu-id="a48a7-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="a48a7-119">Bu bir örnek bize uygun olduğunda basit kuralları Entity Framework Code-First nasıl kullanabileceğimizi ancak sunulmuyorsa, biz bunları tarafından kısıtlanmış değil.</span><span class="sxs-lookup"><span data-stu-id="a48a7-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="a48a7-120">Ardından, bir sipariş sınıfı (Order.cs) ile aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="a48a7-121">Bu sınıf, bir sipariş için Özet ve teslimat bilgilerini izler.</span><span class="sxs-lookup"><span data-stu-id="a48a7-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="a48a7-122">**Henüz derlenemeyecektir**, henüz oluşturduğumuz henüz bir sınıfa bağlıdır bir OrderDetails gezinti özelliği mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="a48a7-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="a48a7-123">Şimdi artık ekleyerek bir sınıf OrderDetail.cs, aşağıdaki kodu ekleyerek adlandırdığınız düzeltelim.</span><span class="sxs-lookup"><span data-stu-id="a48a7-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="a48a7-124">Ayrıca bir olan DB dahil olmak üzere bu yeni Model sınıfları gösterdiğiniz DbSets içerecek şekilde bizim MusicStoreEntities sınıfı bir son güncelleştirme oluşturacağız&lt;sanatçının&gt;.</span><span class="sxs-lookup"><span data-stu-id="a48a7-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="a48a7-125">Güncelleştirilmiş MusicStoreEntities sınıfı olarak görünür aşağıda.</span><span class="sxs-lookup"><span data-stu-id="a48a7-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="a48a7-126">Alışveriş sepeti iş mantığı yönetme</span><span class="sxs-lookup"><span data-stu-id="a48a7-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="a48a7-127">Ardından, modelleri klasöründe ShoppingCart sınıfı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a48a7-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="a48a7-128">Sepet tablosuna veri erişimi ShoppingCart modeli işler.</span><span class="sxs-lookup"><span data-stu-id="a48a7-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="a48a7-129">Buna ek olarak, ekleme ve alışveriş sepetine öğeleri kaldırma iş mantığı işleyeceği.</span><span class="sxs-lookup"><span data-stu-id="a48a7-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="a48a7-130">Yalnızca öğe, alışveriş sepetine eklemek bir hesap için kaydolun gerektirmek istemiyorsanız bu yana, biz kullanıcıların geçici bir benzersiz tanımlayıcı (GUID veya genel olarak benzersiz tanımlayıcısı kullanılarak) atar alışveriş sepetini eriştiklerinde.</span><span class="sxs-lookup"><span data-stu-id="a48a7-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="a48a7-131">ASP.NET oturum sınıfını kullanarak bu kimliği depolarız.</span><span class="sxs-lookup"><span data-stu-id="a48a7-131">We'll store this ID using the ASP.NET Session class.</span></span>

*<span data-ttu-id="a48a7-132">Not: ASP.NET oturum, bunlar site ayrıldıktan sonra süresi dolacak kullanıcıya özgü bilgileri depolamak için kullanışlı bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-132">Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site.</span></span> <span data-ttu-id="a48a7-133">Oturum durumu b.internet performans etkilerinin daha büyük sitelerinde olabilse de tanıtım amacıyla ışık kullanma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-133">While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.</span></span>*

<span data-ttu-id="a48a7-134">ShoppingCart sınıfı aşağıdaki yöntemi kullanıma sunar:</span><span class="sxs-lookup"><span data-stu-id="a48a7-134">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="a48a7-135">**AddToCart** albüm bir parametre olarak alır ve kullanıcının sepetine ekler.</span><span class="sxs-lookup"><span data-stu-id="a48a7-135">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="a48a7-136">Sepet tablonun her albüm miktarını izler olduğundan, gerekirse yeni bir satır oluşturun veya kullanıcı zaten bir kopyasını albümü sipariş yalnızca miktarını artırmak için mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-136">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="a48a7-137">**RemoveFromCart** albüm kimliği alır ve kullanıcının sepetinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-137">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="a48a7-138">Kullanıcı kendi arabasında yalnızca bir kopyasını albümü olsaydı, satır kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-138">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="a48a7-139">**EmptyCart** kullanıcının alışveriş sepetini tüm öğeleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-139">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="a48a7-140">**GetCartItems** görüntüleme veya işleme için CartItems listesini alır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-140">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="a48a7-141">**GetCount** alır bir albümleri bir kullanıcının sahip, alışveriş sepetine içinde toplam sayısı.</span><span class="sxs-lookup"><span data-stu-id="a48a7-141">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="a48a7-142">**GetTotal** sepetteki tüm öğelerin toplam maliyeti hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a48a7-142">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="a48a7-143">**CreateOrder** alışveriş sepetini sipariş kullanıma alma aşamasında dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="a48a7-143">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="a48a7-144">**GetCart** Sepeti nesne elde etmek üzere bizim denetleyicileri sağlayan statik bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-144">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="a48a7-145">Kullandığı **GetCartId** kullanıcının oturumunu CartId okuma işlemek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a48a7-145">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="a48a7-146">Kullanıcının oturumunu kullanıcı CartId okuyabilirsiniz GetCartId yöntemi httpcontextbase öğesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-146">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="a48a7-147">İşte tam **ShoppingCart sınıfı**:</span><span class="sxs-lookup"><span data-stu-id="a48a7-147">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="a48a7-148">Viewmodel'lar</span><span class="sxs-lookup"><span data-stu-id="a48a7-148">ViewModels</span></span>

<span data-ttu-id="a48a7-149">Bizim alışveriş sepeti denetleyicisi bizim Model nesneleri için düzgün bir şekilde eşlemiyor karmaşık bazı bilgileri görünümlerini için iletişim kurması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-149">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="a48a7-150">Bizim modelleri, görünümleri uyacak şekilde değiştirmek istemediğiniz; Etki alanımızda, kullanıcı arabiriminde model sınıfları temsil etmelidir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-150">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="a48a7-151">Store Yöneticisi açılır bilgilerle yaptığımız, ancak birçok bilgi geçirme ViewBag yönetmek zor alır ViewBag sınıfı kullanarak bizim görünümleri için bilgi geçirmek için bir çözüm olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-151">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="a48a7-152">Bu çözüme kullanmaktır *ViewModel* deseni.</span><span class="sxs-lookup"><span data-stu-id="a48a7-152">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="a48a7-153">Bu model kullanılırken, bizim belirli görünüm senaryolar için iyileştirilen ve hangi özellikleri görünümü şablonlarımızı gerekli dinamik değerler/içerik üzerinden kullanıma sunacaksınız kesin türü belirtilmiş sınıfları oluştururuz.</span><span class="sxs-lookup"><span data-stu-id="a48a7-153">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="a48a7-154">Bizim denetleyici sınıflarına doldurun ve kullanmak üzere bizim görünüm şablonu bu görünüm için iyileştirilmiş sınıfların geçirin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-154">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="a48a7-155">Bu tür güvenliği, derleme zamanı denetimi ve Düzenleyicisi IntelliSense içinde görüntüleme şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a48a7-155">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="a48a7-156">Bizim alışveriş sepeti denetleyicisi kullanmak için iki görünüm modeli oluşturacağız: ShoppingCartViewModel kullanıcının alışveriş sepeti içeriğini tutacak ve ShoppingCartRemoveViewModel bir kullanıcının bir şey kaldırdığında onay bilgileri görüntülemek için kullanılacak kendi sepetinden.</span><span class="sxs-lookup"><span data-stu-id="a48a7-156">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="a48a7-157">Yeni bir Viewmodel'lar klasör düzenli tutmak için proje kök dizininde oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="a48a7-157">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="a48a7-158">Projeyi sağ tıklatın, Ekle'yi seçin / yeni bir klasör.</span><span class="sxs-lookup"><span data-stu-id="a48a7-158">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="a48a7-159">Viewmodel'lar klasörün adı.</span><span class="sxs-lookup"><span data-stu-id="a48a7-159">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="a48a7-160">Ardından, ShoppingCartViewModel sınıfı Viewmodel'lar klasöre ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-160">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="a48a7-161">İki özelliğe sahiptir: alışveriş sepetini öğeleri ve tüm öğeleri toplam fiyatı arabasına tutacak bir ondalık değer listesi.</span><span class="sxs-lookup"><span data-stu-id="a48a7-161">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="a48a7-162">Şimdi aşağıdaki dört özelliklerle Viewmodel'lar klasörüne ShoppingCartRemoveViewModel ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-162">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="a48a7-163">Alışveriş sepeti denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="a48a7-163">The Shopping Cart Controller</span></span>

<span data-ttu-id="a48a7-164">Alışveriş sepeti denetleyicisi üç temel amacı vardır: öğe için bir sepet ekleme, sepetinden öğeleri kaldırma ve arabasında öğeler görüntüleniyor.</span><span class="sxs-lookup"><span data-stu-id="a48a7-164">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="a48a7-165">Kullanan üç sınıfları ki hale getirecek yeni oluşturduğunuz: ShoppingCartViewModel ShoppingCartRemoveViewModel ve ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="a48a7-165">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="a48a7-166">StoreController ve StoreManagerController olduğu gibi MusicStoreEntities örneğini tutacak bir alan ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="a48a7-166">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="a48a7-167">Yeni bir alışveriş sepeti denetleyicisi boş denetleyici şablon kullanılarak projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48a7-167">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="a48a7-168">Tam ShoppingCart denetleyicisi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-168">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="a48a7-169">Dizin ve denetleyici Ekle eylemleri tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-169">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="a48a7-170">Remove ve CartSummary denetleyici eylemleri aşağıdaki bölümde açıklayacağız iki özel durumları işler.</span><span class="sxs-lookup"><span data-stu-id="a48a7-170">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="a48a7-171">JQuery AJAX güncelleştirmeleriyle</span><span class="sxs-lookup"><span data-stu-id="a48a7-171">Ajax Updates with jQuery</span></span>

<span data-ttu-id="a48a7-172">Sonraki ShoppingCartViewModel için kesin ve önce olarak aynı yöntemi kullanarak liste görünümü şablonunu kullanan bir alışveriş sepeti dizin sayfa oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a48a7-172">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="a48a7-173">Ancak, bir Html.ActionLink sepetinden öğeleri kaldırmak için kullanmak yerine, jQuery "yukarı RemoveLink HTML sınıfı bu görünümde tüm bağlantılar için tıklama olayı wire için" kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="a48a7-173">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="a48a7-174">Form gönderme yerine bu click olay işleyicisi yalnızca bir AJAX geri çağırma RemoveFromCart denetleyicisi eylemimiz hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-174">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="a48a7-175">Bir seri hale getirilmiş JSON sonuç RemoveFromCart döndürür, bizim jQuery geri çağırma daha sonra ayrıştırır ve jQuery kullanarak sayfasına dört Hızlı güncelleştirmeler yapar:</span><span class="sxs-lookup"><span data-stu-id="a48a7-175">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="a48a7-176">Silinen albümü listeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a48a7-176">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="a48a7-177">Sepet sayısı üst bilgisindeki güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="a48a7-177">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="a48a7-178">Kullanıcı için bir güncelleştirme iletisi görüntüler</span><span class="sxs-lookup"><span data-stu-id="a48a7-178">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="a48a7-179">Sepet toplam fiyat güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="a48a7-179">Updates the cart total price</span></span>

<span data-ttu-id="a48a7-180">Kaldır senaryo dizin görünümündeki bir Ajax geri çağırma tarafından işlenen olduğundan, ek bir görünüm için RemoveFromCart eylem gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a48a7-180">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="a48a7-181">/ShoppingCart/Index görünümü için tam kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a48a7-181">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="a48a7-182">Bu test için öğe, alışveriş sepetimizi eklemek gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a48a7-182">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="a48a7-183">Güncelleştireceğiz bizim **Store ayrıntıları** bir "Sepete Ekle" düğmesi içerecek şekilde görünümü.</span><span class="sxs-lookup"><span data-stu-id="a48a7-183">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="a48a7-184">Biz adresinden iken, bazı ekledik albüm ek bilgiler dahil edebilirsiniz Biz bu görünüm son güncelleştirmenizden sonra: Türe, sanatçının, fiyat ve albüm resmi.</span><span class="sxs-lookup"><span data-stu-id="a48a7-184">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="a48a7-185">Güncelleştirilmiş kodu Store Ayrıntıları Görüntüle, aşağıda gösterildiği gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="a48a7-185">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="a48a7-186">Şimdi biz mağazası aracılığıyla tıklayın ve test ekleme ve albümleri, için ve alışveriş sepetimizi kaldırma.</span><span class="sxs-lookup"><span data-stu-id="a48a7-186">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="a48a7-187">Uygulamayı çalıştırmak ve Store dizinine göz atın.</span><span class="sxs-lookup"><span data-stu-id="a48a7-187">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="a48a7-188">Ardından, Albümler listesini görüntülemek için bir türe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a48a7-188">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="a48a7-189">Artık bir albüm başlığına tıklayarak "Sepete Ekle" düğmesi de dahil olmak üzere güncelleştirilmiş bizim albüm Ayrıntılar görünümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-189">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="a48a7-190">"Sepete Ekle" düğmesine tıklayarak bizim alışveriş sepeti dizini görünümde alışveriş sepeti Özet listesi ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a48a7-190">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="a48a7-191">Alışveriş sepetinize yüklendikten sonra Ajax güncelleştirme, alışveriş sepetine görmek için sepet bağlantısından Kaldır tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a48a7-191">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="a48a7-192">Alışveriş sepeti kaydı kendi sepetine öğe ekleme olanağı tanıyan bir çalışan bir çıkış oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="a48a7-192">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="a48a7-193">Aşağıdaki bölümde, bunları kaydetmek ve kullanıma alma işlemini tamamlamak izin veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="a48a7-193">In the following section, we'll allow them to register and complete the checkout process.</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="a48a7-194">[Önceki](mvc-music-store-part-7.md)
> [İleri](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="a48a7-194">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
