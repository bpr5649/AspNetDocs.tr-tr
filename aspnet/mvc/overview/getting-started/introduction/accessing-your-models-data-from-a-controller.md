---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045175"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="82b1a-102">Bir Denetleyiciden Modelinizin Verilerine Erişme</span><span class="sxs-lookup"><span data-stu-id="82b1a-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="82b1a-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="82b1a-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="82b1a-104">Bu bölümde, yeni bir `MoviesController` sınıf oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen bir kod yazacak.</span><span class="sxs-lookup"><span data-stu-id="82b1a-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="82b1a-105">Sonraki adıma geçmeden önce **uygulamayı derleyin** .</span><span class="sxs-lookup"><span data-stu-id="82b1a-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="82b1a-106">Uygulamayı dermezseniz, denetleyici eklenirken bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="82b1a-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="82b1a-107">Çözüm Gezgini, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="82b1a-108">**Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici**' ye tıklayın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="82b1a-109">Model sınıfı için **filmi (MvcMovie. modeller)** seçin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="82b1a-110">Veri bağlamı sınıfı için **Moviedbcontext (MvcMovie. modeller)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="82b1a-111">Denetleyici adı için **MoviesController**girin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="82b1a-112">Aşağıdaki görüntüde tamamlanan iletişim kutusu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="82b1a-113">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-113">Click **Add**.</span></span> <span data-ttu-id="82b1a-114">(Bir hata alırsanız, denetleyiciyi eklemeye başlamadan önce uygulamayı derlemeniz olasıdır.) Visual Studio aşağıdaki dosyaları ve klasörleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="82b1a-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="82b1a-115">*Controllers* klasöründeki *bir MoviesController.cs* dosyası.</span><span class="sxs-lookup"><span data-stu-id="82b1a-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="82b1a-116">*Views\filmler* klasörü.</span><span class="sxs-lookup"><span data-stu-id="82b1a-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="82b1a-117">Yeni *Views\filmlerini* klasöründeki *. cshtml, delete. cshtml, details. cshtml, Edit. cshtml*ve *Index. cshtml* oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82b1a-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="82b1a-118">Visual Studio [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini sizin için otomatik olarak oluşturdu (CRUD eylem yöntemlerinin ve görünümlerinin otomatik olarak oluşturulması, yapı iskelesi olarak bilinir).</span><span class="sxs-lookup"><span data-stu-id="82b1a-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="82b1a-119">Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.</span><span class="sxs-lookup"><span data-stu-id="82b1a-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="82b1a-120">Uygulamayı çalıştırın ve **MVC film** bağlantısına tıklayın (veya `Movies` TARAYıCıNıN adres çubuğundaki URL 'ye */filmler* ekleyerek denetleyiciye gidin).</span><span class="sxs-lookup"><span data-stu-id="82b1a-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="82b1a-121">Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *App \_ Start\routeconfig.cs* dosyasında tanımlanan), tarayıcı isteği `http://localhost:xxxxx/Movies` `Index` denetleyicinin varsayılan eylem yöntemine yönlendirilir `Movies` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="82b1a-122">Diğer bir deyişle, tarayıcı isteği `http://localhost:xxxxx/Movies` tarayıcı isteğiyle aynı şekilde aynıdır `http://localhost:xxxxx/Movies/Index` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="82b1a-123">Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="82b1a-124">Film oluşturma</span><span class="sxs-lookup"><span data-stu-id="82b1a-124">Creating a Movie</span></span>

<span data-ttu-id="82b1a-125">**Yeni oluştur** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-125">Select the **Create New** link.</span></span> <span data-ttu-id="82b1a-126">Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="82b1a-127">Fiyat alanına ondalık nokta veya virgül giremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="82b1a-128">&quot;Ondalık bir nokta ve ABD İngilizcesi olmayan tarih biçimleri için virgül (,) kullanan İngilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için &quot; , *globalize.js* ve belirli *kültürleri/globalize.cultures.js* dosyanızı (Kimden [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve kullanılacak JavaScript 'i dahil etmeniz gerekir `Globalize.parseFloat` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="82b1a-129">Bunu bir sonraki öğreticide nasıl yapacağım.</span><span class="sxs-lookup"><span data-stu-id="82b1a-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="82b1a-130">Şimdilik, yalnızca 10 gibi tüm sayıları girmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="82b1a-131">**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="82b1a-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="82b1a-132">Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="82b1a-133">Birkaç film girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82b1a-133">Create a couple more movie entries.</span></span> <span data-ttu-id="82b1a-134">Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="82b1a-135">Oluşturulan kodu İnceleme</span><span class="sxs-lookup"><span data-stu-id="82b1a-135">Examining the Generated Code</span></span>

<span data-ttu-id="82b1a-136">*Controllers\MoviesController.cs* dosyasını açın ve oluşturulan `Index` yöntemi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="82b1a-137">Aşağıdaki yöntemi içeren film denetleyicisinin bir bölümü `Index` aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="82b1a-138">Denetleyiciye yönelik bir istek `Movies` tablodaki tüm girişleri döndürür `Movies` ve sonra sonuçları `Index` görünüme geçirir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="82b1a-139">Sınıfından aşağıdaki satır `MoviesController` , daha önce açıklandığı gibi bir film veritabanı bağlamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82b1a-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="82b1a-140">Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="82b1a-141">Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="82b1a-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="82b1a-142">Bu öğreticide daha önce, bir denetleyicinin nesneyi kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="82b1a-143">, `ViewBag` Bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="82b1a-144">MVC Ayrıca, *türü kesin* belirlenmiş nesneleri bir görünüm şablonuna geçirebilme olanağı da sağlar.</span><span class="sxs-lookup"><span data-stu-id="82b1a-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="82b1a-145">Bu kesin türü belirtilmiş yaklaşım, Visual Studio düzenleyicisinde kodunuzun ve daha zengin [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 'in derleme zamanı denetimini daha iyi bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="82b1a-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="82b1a-146">Visual Studio 'daki scafkatlama mekanizması, bu yaklaşımı (yani, *türü kesin* belirlenmiş bir model geçirerek), `MoviesController` Yöntem ve görünümleri oluştururken sınıfla ve görüntüleme şablonlarına kullandı.</span><span class="sxs-lookup"><span data-stu-id="82b1a-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="82b1a-147">*Controllers\MoviesController.cs* dosyasında, oluşturulan `Details` yöntemi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="82b1a-148">`Details`Yöntemi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="82b1a-149">`id`Parametre genellikle rota verileri olarak geçirilir. Örneğin, `http://localhost:1234/movies/details/1` denetleyiciyi film denetleyicisine, eylemini öğesine ve ile 1 ' e ayarlar `details` `id` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="82b1a-150">Ayrıca kimliği bir sorgu dizesi ile aşağıdaki gibi geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82b1a-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="82b1a-151">Bir `Movie` bulunursa, modelin bir örneği `Movie` `Details` görünüme geçirilir:</span><span class="sxs-lookup"><span data-stu-id="82b1a-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="82b1a-152">*Views\Movies\Details.cshtml* dosyasının içeriğini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="82b1a-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="82b1a-153">`@model`Görünüm şablonu dosyasının üst kısmına bir ifade ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="82b1a-154">Film denetleyicisini oluştururken, Visual Studio `@model` *details. cshtml* dosyasının en üstüne aşağıdaki ifadeyi otomatik olarak dahil edin:</span><span class="sxs-lookup"><span data-stu-id="82b1a-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="82b1a-155">Bu `@model` yönerge, kesin olarak belirlenmiş bir nesne kullanarak denetleyicinin görünüme geçirildiği filme erişmenizi sağlar `Model` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="82b1a-156">Örneğin, *details. cshtml* şablonunda, kod her bir film alanını, `DisplayNameFor` türü kesin belirlenmiş nesne olan HTML Yardımcıları [için ve displayto](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) öğesine geçirir `Model` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="82b1a-157">`Create`Ve `Edit` yöntemleri ve Görünüm şablonları da bir film modeli nesnesi iletir.</span><span class="sxs-lookup"><span data-stu-id="82b1a-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="82b1a-158">*Index. cshtml* görünüm şablonunu ve `Index` *MoviesController.cs* dosyasındaki yöntemi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="82b1a-159">[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` Eylem yönteminde yardımcı yöntemini çağırdığında kodun bir nesne nasıl oluşturduğunu fark edin `Index` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="82b1a-160">Kod daha sonra bu `Movies` listeyi `Index` eylem yönteminden görünüme geçirir:</span><span class="sxs-lookup"><span data-stu-id="82b1a-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="82b1a-161">Film denetleyicisini oluştururken, Visual Studio `@model` *Index. cshtml* dosyasının en üstüne aşağıdaki ifadeyi otomatik olarak dahil edin:</span><span class="sxs-lookup"><span data-stu-id="82b1a-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="82b1a-162">Bu `@model` yönerge, kesin olarak belirlenmiş bir nesne kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar `Model` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="82b1a-163">Örneğin, *Index. cshtml* şablonunda, kod, `foreach` türü kesin belirlenmiş nesne üzerinde bir ekstre yaparak filmlerle döngü yapılır `Model` :</span><span class="sxs-lookup"><span data-stu-id="82b1a-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="82b1a-164">`Model`Nesne türü kesin belirlenmiş olduğundan (bir nesne olarak `IEnumerable<Movie>` ), `item` döngüdeki her bir nesne olarak yazılır `Movie` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="82b1a-165">Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="82b1a-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="82b1a-167">SQL Server Yerel Veritabanı ile çalışma</span><span class="sxs-lookup"><span data-stu-id="82b1a-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="82b1a-168">Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin `Movies` henüz mevcut olmayan bir veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First.</span><span class="sxs-lookup"><span data-stu-id="82b1a-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="82b1a-169">*Uygulamanın \_ veri* klasörüne bakarak oluşturulduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="82b1a-170">*Filmler. mdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama \_ verileri* klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="82b1a-171">*Film. mdf* ' ye çift TıKLAYARAK **Sunucu Gezgini**'Ni açın ve ardından Filmler tablosunu görmek için **Tablolar** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="82b1a-172">ID ' ın yanındaki anahtar simgesine göz önünde.</span><span class="sxs-lookup"><span data-stu-id="82b1a-172">Note the key icon next to ID.</span></span> <span data-ttu-id="82b1a-173">Varsayılan olarak, EF, birincil anahtar adlı bir özellik oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="82b1a-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="82b1a-174">EF ve MVC hakkında daha fazla bilgi için, bkz. Tom Dykstra 'ın [MVC ve EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)hakkında harika bir öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="82b1a-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="82b1a-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="82b1a-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="82b1a-176">Tabloya sağ tıklayıp `Movies` **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="82b1a-177">Tabloya sağ tıklayıp tablo `Movies` **tanımını aç** ' ı seçerek Entity Framework Code First sizin için oluşturduğu tablo yapısını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="82b1a-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="82b1a-178">Tablo şemasının, `Movies` `Movie` daha önce oluşturduğunuz sınıfa nasıl eşlendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="82b1a-179">Entity Framework Code First, bu şemayı sınıfınıza göre sizin için otomatik olarak oluşturdu `Movie` .</span><span class="sxs-lookup"><span data-stu-id="82b1a-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="82b1a-180">İşiniz bittiğinde, *Moviedbcontext* ' i sağ tıklatıp **Bağlantıyı kapat**' ı seçerek bağlantıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="82b1a-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="82b1a-181">(Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="82b1a-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="82b1a-182">Artık veri görüntüleme, düzenleme, güncelleştirme ve silme için bir veritabanınız ve sayfalarınız vardır.</span><span class="sxs-lookup"><span data-stu-id="82b1a-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="82b1a-183">Sonraki öğreticide, yapı iskelesi kodunun geri kalanını inceleyeceğiz ve `SearchIndex` `SearchIndex` Bu veritabanında film aramanıza olanak tanıyan bir yöntem ve bir görünüm ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="82b1a-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="82b1a-184">MVC ile Entity Framework kullanma hakkında daha fazla bilgi için, bkz. [ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="82b1a-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="82b1a-185">[Önceki](creating-a-connection-string.md) 
>  [Sonraki](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="82b1a-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
