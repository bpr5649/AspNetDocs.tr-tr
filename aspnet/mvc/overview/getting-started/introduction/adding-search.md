---
uid: mvc/overview/getting-started/introduction/adding-search
title: Ara | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211470"
---
# <a name="search"></a><span data-ttu-id="b4cc3-102">Arama</span><span class="sxs-lookup"><span data-stu-id="b4cc3-102">Search</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="b4cc3-103">Arama yöntemi ve arama görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="b4cc3-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="b4cc3-104">Bu bölümde, `Index` bir türe veya ada göre filmlere göre arama yapmanızı sağlayan eylem yöntemine arama özelliği ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4cc3-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b4cc3-105">Prerequisites</span></span>

<span data-ttu-id="b4cc3-106">Bu bölümün ekran görüntülerini eşleştirmek için, uygulamayı (F5) çalıştırmanız ve aşağıdaki filmleri veritabanına eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="b4cc3-107">Title</span><span class="sxs-lookup"><span data-stu-id="b4cc3-107">Title</span></span> | <span data-ttu-id="b4cc3-108">Yayın Tarihi</span><span class="sxs-lookup"><span data-stu-id="b4cc3-108">Release Date</span></span> | <span data-ttu-id="b4cc3-109">Tarzı</span><span class="sxs-lookup"><span data-stu-id="b4cc3-109">Genre</span></span> | <span data-ttu-id="b4cc3-110">Fiyat</span><span class="sxs-lookup"><span data-stu-id="b4cc3-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="b4cc3-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="b4cc3-111">Ghostbusters</span></span> | <span data-ttu-id="b4cc3-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="b4cc3-112">6/8/1984</span></span> | <span data-ttu-id="b4cc3-113">Komedi</span><span class="sxs-lookup"><span data-stu-id="b4cc3-113">Comedy</span></span> | <span data-ttu-id="b4cc3-114">6,99</span><span class="sxs-lookup"><span data-stu-id="b4cc3-114">6.99</span></span> |
| <span data-ttu-id="b4cc3-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="b4cc3-115">Ghostbusters II</span></span> | <span data-ttu-id="b4cc3-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="b4cc3-116">6/16/1989</span></span> | <span data-ttu-id="b4cc3-117">Komedi</span><span class="sxs-lookup"><span data-stu-id="b4cc3-117">Comedy</span></span> | <span data-ttu-id="b4cc3-118">6,99</span><span class="sxs-lookup"><span data-stu-id="b4cc3-118">6.99</span></span> |
| <span data-ttu-id="b4cc3-119">Apes 'nin Planet</span><span class="sxs-lookup"><span data-stu-id="b4cc3-119">Planet of the Apes</span></span> | <span data-ttu-id="b4cc3-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="b4cc3-120">3/27/1986</span></span> | <span data-ttu-id="b4cc3-121">Eylem</span><span class="sxs-lookup"><span data-stu-id="b4cc3-121">Action</span></span> | <span data-ttu-id="b4cc3-122">5,99</span><span class="sxs-lookup"><span data-stu-id="b4cc3-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="b4cc3-123">Dizin formunu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b4cc3-123">Updating the Index Form</span></span>

<span data-ttu-id="b4cc3-124">`Index`Eylem yöntemini mevcut sınıfa güncelleştirerek başlayın `MoviesController` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="b4cc3-125">Kod şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="b4cc3-126">Yöntemin ilk satırı, `Index` filmleri seçmek için aşağıdaki [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgusunu oluşturur:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="b4cc3-127">Sorgu bu noktada tanımlandı, ancak henüz veritabanında çalıştırılmadı.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="b4cc3-128">`searchString`Parametresi bir dize içeriyorsa, filmler sorgusu, aşağıdaki kodu kullanarak arama dizesinin değerine göre filtreleyecek şekilde değiştirilir:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="b4cc3-129">`s => s.Title`Yukarıdaki kod bir [lambda ifadesidir](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc3-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="b4cc3-130">Lambdalar, yukarıdaki kodda kullanılan [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) yöntemi gibi standart sorgu işleci yöntemlerine bağımsız değişkenler olarak Yöntem tabanlı [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) sorgularında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="b4cc3-131">LINQ sorguları tanımlandıklarında veya veya gibi bir yöntem çağırarak değiştirildiklerinde yürütülmez `Where` `OrderBy` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="b4cc3-132">Bunun yerine, sorgu yürütmesi ertelenir, bu da bir ifadenin değerlendirmesinin, gerçekleştirilmiş değeri gerçekten üzerinde yinelenene veya yöntem çağrılana kadar gecikildiği anlamına gelir [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="b4cc3-133">`Search`Örnekte, sorgu *Index. cshtml* görünümünde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="b4cc3-134">Ertelenmiş sorgu yürütme hakkında daha fazla bilgi için bkz. [sorgu yürütme](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc3-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b4cc3-135">[Contains](https://msdn.microsoft.com/library/bb155125.aspx) yöntemi, yukarıdaki c# kodu değil, veritabanında çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="b4cc3-136">Veritabanında [SQL gibi](https://msdn.microsoft.com/library/ms179859.aspx)eşlemeler [içerir](https://msdn.microsoft.com/library/bb155125.aspx) , büyük/küçük harfe duyarsız olur.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="b4cc3-137">Artık `Index` formu kullanıcıya görüntüleyecek görünümü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="b4cc3-138">Uygulamayı çalıştırın ve */movies/Index*adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="b4cc3-139">URL 'ye gibi bir sorgu dizesi ekleyin `?searchString=ghost` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="b4cc3-140">Filtrelenmiş filmler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="b4cc3-142">`Index`Yönteminin imzasını adlı bir parametreye sahip olacak şekilde değiştirirseniz `id` , `id` parametresi `{id}` *App \_ start\routeconfig.cs* dosyasında ayarlanan varsayılan yolların yer tutucusuyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="b4cc3-143">Özgün `Index` Yöntem şöyle görünür::</span><span class="sxs-lookup"><span data-stu-id="b4cc3-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="b4cc3-144">Değiştirilen `Index` Yöntem şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="b4cc3-145">Artık arama başlığını sorgu dizesi değeri yerine rota verileri (bir URL segmenti) olarak geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="b4cc3-146">Ancak, kullanıcıların bir filmi her arayışınızda URL 'YI değiştirmesini beklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="b4cc3-147">Böylece, filmlerin filtrelemesine yardımcı olmak için Kullanıcı arabirimi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="b4cc3-148">`Index`Yol ile bağlantılı kimlik parametresinin nasıl geçirileceğini test etmek için yönteminin imzasını değiştirdiyseniz, `Index` yönteminizin adlı bir dize parametresi alması için geri değiştirin `searchString` :</span><span class="sxs-lookup"><span data-stu-id="b4cc3-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="b4cc3-149">*Views\Movies\Index.cshtml* dosyasını açın ve hemen sonra `@Html.ActionLink("Create New", "Create")` vurgulanan form işaretlemesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="b4cc3-150">`Html.BeginForm`Yardımcı, bir açılış `<form>` etiketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="b4cc3-151">`Html.BeginForm`Yardımcı, Kullanıcı **filtre** düğmesine tıklayarak formu gönderdiğinde formun kendine göndermesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="b4cc3-152">Visual Studio 2013, görüntüleme dosyalarını görüntülerken ve düzenlenirken iyi bir iyileştirmedir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="b4cc3-153">Uygulamayı bir görünüm dosyası açıkken çalıştırdığınızda Visual Studio 2013, görünümü görüntülemek için doğru denetleyici eylemi yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="b4cc3-154">Visual Studio 'da (yukarıdaki görüntüde gösterildiği gibi) dizin görünümü açık olduğunda, uygulamayı çalıştırmak için Mrk F5 veya F5 ' e dokunun ve ardından bir filmi aramayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="b4cc3-155">`HttpPost`Metodun aşırı yüklemesi yoktur `Index` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="b4cc3-156">Bunun için gerekli değildir çünkü yöntem uygulamanın durumunu değiştirmediğinden verileri filtrelememeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="b4cc3-157">Aşağıdaki `HttpPost Index` yöntemi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="b4cc3-158">Bu durumda, çalıştırılan eylem `HttpPost Index` yöntemiyle eşleşir ve `HttpPost Index` yöntemi aşağıdaki görüntüde gösterildiği gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![Searchposthayalet](adding-search/_static/image5.png)

<span data-ttu-id="b4cc3-160">Ancak, bu yöntemin bu sürümünü eklemeseniz bile `HttpPost` `Index` , tümünün nasıl uygulandığını gösteren bir sınırlama vardır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="b4cc3-161">Belirli bir arama için yer işareti koymak istediğinizi veya aynı film filtrelenmiş listesini görmek için onlara tıklabilecekleri bir bağlantı göndermek istediğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="b4cc3-162">HTTP POST isteğinin URL 'SI GET isteğinin URL 'siyle (localhost: xxxxx/filmler/dizin) aynı olduğunu ve URL 'de arama bilgisi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="b4cc3-163">Şu anda arama dizesi bilgileri sunucuya form alanı değeri olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="b4cc3-164">Bu, arama bilgilerini bir URL 'de yer işaretine veya arkadaşlara göndermek için yakalayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="b4cc3-165">Çözüm, `BeginForm` Post ISTEĞININ URL 'ye arama bilgilerini eklemesi gerektiğini ve yöntemin sürümüne yönlendirilmesini belirten bir aşırı yüklemesi kullanmaktır `HttpGet` `Index` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="b4cc3-166">Mevcut parametresiz `BeginForm` yöntemi aşağıdaki biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="b4cc3-168">Artık bir arama gönderdiğinizde URL bir arama sorgu dizesi içerir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="b4cc3-169">`HttpGet Index`Bir yönteminiz olsa da, arama eylem yöntemine de gidecektir `HttpPost Index` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![Indexwithgeturl](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="b4cc3-171">Türe göre arama ekleme</span><span class="sxs-lookup"><span data-stu-id="b4cc3-171">Adding Search by Genre</span></span>

<span data-ttu-id="b4cc3-172">`HttpPost`Yöntemin sürümünü eklediyseniz `Index` , şimdi silin.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="b4cc3-173">Daha sonra, kullanıcıların film tarza göre aramasını sağlamak için bir özellik ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="b4cc3-174">`Index` yöntemini aşağıdaki kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="b4cc3-175">Yöntemin bu sürümü `Index` ek bir parametre alır, yani `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="b4cc3-176">İlk birkaç kod satırı, `List` veritabanından film tarzları tutacak bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="b4cc3-177">Aşağıdaki kod, veritabanından tüm tarzları alan bir LINQ sorgusudur.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="b4cc3-178">Kod, `AddRange` `List` tüm benzersiz tarzları listeye eklemek için genel koleksiyonun yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="b4cc3-179">(Değiştirici olmadan `Distinct` yinelenen tarzlar eklenir — Örneğin, örneğimizde komedi iki kez eklenir).</span><span class="sxs-lookup"><span data-stu-id="b4cc3-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="b4cc3-180">Daha sonra kod, nesne içindeki tarzların listesini depolar `ViewBag.MovieGenre` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="b4cc3-181">Kategori verilerini (film tarzları) içinde bir [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) nesnesi olarak depolama `ViewBag` , sonra bir açılan liste kutusunda Kategori VERILERINE erişme, MVC uygulamaları için tipik bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="b4cc3-182">Aşağıdaki kod, parametresinin nasıl kontrol alınacağını gösterir `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="b4cc3-183">Boş değilse, kod, seçili filmleri belirtilen tarzya sınırlamak için film sorgusunu daha da kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="b4cc3-184">Daha önce belirtildiği gibi, bir sorgu, film listesi üzerinde yinelenene kadar (görünümde, eylem yöntemi döndürüldüğünde gerçekleşen) veritabanı üzerinde çalışmaz `Index` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="b4cc3-185">Türe göre aramayı desteklemek için dizin görünümüne biçimlendirme ekleme</span><span class="sxs-lookup"><span data-stu-id="b4cc3-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="b4cc3-186">`Html.DropDownList` *Views\Movies\Index.cshtml* dosyasına yardımcı olan bir yardımcı ekleyin `TextBox` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="b4cc3-187">Tamamlanan biçimlendirme aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="b4cc3-188">Aşağıdaki kodda:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="b4cc3-189">"Movietarz" parametresi `DropDownList` , içinde bir içinde bulunacak yardımcı için anahtar sağlar `IEnumerable<SelectListItem>` `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="b4cc3-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="b4cc3-190">`ViewBag`Eylem yönteminde doldurulmıştı:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="b4cc3-191">"All" parametresi bir seçenek etiketi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="b4cc3-192">Bu seçimi tarayıcınızda inceleyebilirsiniz, "Value" özniteliğinin boş olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="b4cc3-193">Denetleyicimiz yalnızca dizeyi filtreleyerek `if` `null` veya boş olduğundan, için boş bir değer gönderilmesi `movieGenre` Tüm tarzları gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="b4cc3-194">Ayrıca, varsayılan olarak seçilecek bir seçenek de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="b4cc3-195">Varsayılan seçenek olarak "komedi" isterseniz, denetleyicideki kodu şöyle değiştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4cc3-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="b4cc3-196">Uygulamayı çalıştırın ve */movies/Index*konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="b4cc3-197">Türe göre, film adına ve her iki ölçüte göre arama yapmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="b4cc3-198">Bu bölümde, kullanıcıların film başlığına ve tarzya göre arama yapmasına izin veren bir arama eylemi yöntemi ve görünümü oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="b4cc3-199">Sonraki bölümde, modele nasıl özellik ekleneceğini `Movie` ve otomatik olarak bir test veritabanı oluşturacak Başlatıcı nasıl ekleneceğini inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="b4cc3-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b4cc3-200">[Önceki](examining-the-edit-methods-and-edit-view.md) 
>  [Sonraki](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="b4cc3-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
