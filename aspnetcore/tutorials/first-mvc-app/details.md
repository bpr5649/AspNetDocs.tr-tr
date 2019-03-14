---
title: Ayrıntılarını inceleyin ve Delete metotlarını bir ASP.NET Core uygulaması
author: rick-anderson
description: Ayrıntıları denetleyicisi yöntem hakkında bilgi edinin ve temel bir ASP.NET Core MVC uygulamasında görüntüleyebilirsiniz.
ms.author: riande
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/details
ms.openlocfilehash: f674ca1761f85ce127121603286c97d5936f6716
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071661"
---
# <a name="examine-the-details-and-delete-methods-of-an-aspnet-core-app"></a><span data-ttu-id="769ab-103">Ayrıntılarını inceleyin ve Delete metotlarını bir ASP.NET Core uygulaması</span><span class="sxs-lookup"><span data-stu-id="769ab-103">Examine the Details and Delete methods of an ASP.NET Core app</span></span>

<span data-ttu-id="769ab-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="769ab-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="769ab-105">Film denetleyicisi açın ve incelemek `Details` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="769ab-105">Open the Movie controller and examine the `Details` method:</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_details)]

<span data-ttu-id="769ab-106">Bu eylem yöntemine oluşturulan MVC yapı iskelesi altyapısı yöntemi çağıran bir HTTP isteği gösteren bir yorum ekler.</span><span class="sxs-lookup"><span data-stu-id="769ab-106">The MVC scaffolding engine that created this action method adds a comment showing an HTTP request that invokes the method.</span></span> <span data-ttu-id="769ab-107">Bu durumda, üç URL kesimleri ile bir GET isteği, `Movies` denetleyicisi `Details` yöntemi ve bir `id` değeri.</span><span class="sxs-lookup"><span data-stu-id="769ab-107">In this case it's a GET request with three URL segments, the `Movies` controller, the `Details` method, and an `id` value.</span></span> <span data-ttu-id="769ab-108">Bu kesimler tanımlanmış geri çağırma *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="769ab-108">Recall these segments are defined in *Startup.cs*.</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

<span data-ttu-id="769ab-109">EF kullanarak verileri için arama yapmayı kolaylaştırır `FirstOrDefaultAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="769ab-109">EF makes it easy to search for data using the `FirstOrDefaultAsync` method.</span></span> <span data-ttu-id="769ab-110">Yönteme yerleşik bir önemli güvenlik kod arama yöntemi şey denemeden önce bir filmi buldu doğrular özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="769ab-110">An important security feature built into the method is that the code verifies that the search method has found a movie before it tries to do anything with it.</span></span> <span data-ttu-id="769ab-111">Örneğin, bir bilgisayar korsanının hataları siteye bağlantılardan tarafından oluşturulan URL değiştirerek neden olabilirdi `http://localhost:xxxx/Movies/Details/1` gibi bir şey `http://localhost:xxxx/Movies/Details/12345` (veya gerçek bir film temsil etmez başka bir değer).</span><span class="sxs-lookup"><span data-stu-id="769ab-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like  `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="769ab-112">Null film denetlemedi, uygulama bir özel durumlar oluşturan.</span><span class="sxs-lookup"><span data-stu-id="769ab-112">If you didn't check for a null movie, the app would throw an exception.</span></span>

<span data-ttu-id="769ab-113">İnceleme `Delete` ve `DeleteConfirmed` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="769ab-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_delete)]

<span data-ttu-id="769ab-114">Unutmayın `HTTP GET Delete` yöntemi belirtilen film silme değil, film bir görünümünü (HttpPost) gönderebileceği silme işlemi geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="769ab-114">Note that the `HTTP GET Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (HttpPost) the deletion.</span></span> <span data-ttu-id="769ab-115">Bir GET'e yanıt olarak bir silme işlemi gerçekleştirme isteği (veya bir düzenleme işlemini gerçekleştirirken bu konular için işlem veya veriler değiştiğinde başka bir işlem oluşturun) bir güvenlik boşluğu açılır.</span><span class="sxs-lookup"><span data-stu-id="769ab-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span>

<span data-ttu-id="769ab-116">`[HttpPost]` Verilerini siler yöntemi adlı `DeleteConfirmed` HTTP POST yöntemi için benzersiz bir imza veya ad vermek için.</span><span class="sxs-lookup"><span data-stu-id="769ab-116">The `[HttpPost]` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="769ab-117">İki yöntem imzaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="769ab-117">The two method signatures are shown below:</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete2)]

[!code-csharp[](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete3)]

<span data-ttu-id="769ab-118">Ortak dil çalışma zamanı (CLR) aşırı yüklenmiş yöntemler benzersiz parametre imzası (yöntemi aynı ada ancak farklı parametre listesi) olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="769ab-118">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="769ab-119">Bununla birlikte, burada iki gerekir `Delete` --Get--diğeri POST yöntemleri her ikisi de aynı parametre imzasına sahip.</span><span class="sxs-lookup"><span data-stu-id="769ab-119">However, here you need two `Delete` methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="769ab-120">(Her ikisi de tek bir tamsayı bir parametre olarak kabul etmeniz gerekir.)</span><span class="sxs-lookup"><span data-stu-id="769ab-120">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="769ab-121">Bu sorunun iki yaklaşım vardır, yöntemleri farklı adlar vermek için biridir.</span><span class="sxs-lookup"><span data-stu-id="769ab-121">There are two approaches to this problem, one is to give the methods different names.</span></span> <span data-ttu-id="769ab-122">Önceki örnekte yapı iskelesi mekanizması ne yaptığını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="769ab-122">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="769ab-123">Bununla birlikte, küçük bir sorunla sunar: ASP.NET bir URL kesimleri eylem yöntemleri adıyla eşler ve bir yöntem yeniden adlandırırsanız, normal olarak Yönlendirme bu yöntem bulmak saptayamazdınız.</span><span class="sxs-lookup"><span data-stu-id="769ab-123">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="769ab-124">Eklenecek olan örnekte gördüğünüz çözümüdür `ActionName("Delete")` özniteliğini `DeleteConfirmed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="769ab-124">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="769ab-125">Bu öznitelik bir POST isteği için /Delete/ içeren bir URL bulabilirsiniz, böylece eşleme için yönlendirme sistem gerçekleştirir. `DeleteConfirmed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="769ab-125">That attribute performs mapping for the routing system so that a URL that includes /Delete/ for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="769ab-126">Bir ek eklemek için POST yöntemini imzası yapay olarak değiştirmek için başka bir yaygın geçici aynı adlara ve imzaları olan yöntemler için olan (kullanılmayan) parametre.</span><span class="sxs-lookup"><span data-stu-id="769ab-126">Another common work around for methods that have identical names and signatures is to artificially change the signature of the POST method to include an extra (unused) parameter.</span></span> <span data-ttu-id="769ab-127">Eklediğimiz olduğunda ne önceki gönderide yaptığımız olan `notUsed` parametresi.</span><span class="sxs-lookup"><span data-stu-id="769ab-127">That's what we did in a previous post when we added the `notUsed` parameter.</span></span> <span data-ttu-id="769ab-128">Aynı şeyi burada yapabilirsiniz `[HttpPost] Delete` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="769ab-128">You could do the same thing here for the `[HttpPost] Delete` method:</span></span>

```csharp
// POST: Movies/Delete/6
[ValidateAntiForgeryToken]
public async Task<IActionResult> Delete(int id, bool notUsed)
```

### <a name="publish-to-azure"></a><span data-ttu-id="769ab-129">Azure'a Yayımlama</span><span class="sxs-lookup"><span data-stu-id="769ab-129">Publish to Azure</span></span>

<span data-ttu-id="769ab-130">Azure'a dağıtma hakkında daha fazla bilgi için bkz. [Öğreticisi: Azure App Service'te .NET Core ve SQL veritabanı web uygulaması derleme](/azure/app-service/app-service-web-tutorial-dotnetcore-sqldb).</span><span class="sxs-lookup"><span data-stu-id="769ab-130">For information on deploying to Azure, see [Tutorial: Build a .NET Core and SQL Database web app in Azure App Service](/azure/app-service/app-service-web-tutorial-dotnetcore-sqldb).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="769ab-131">Önceki</span><span class="sxs-lookup"><span data-stu-id="769ab-131">Previous</span></span>](validation.md)
