---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: Details ve Delete metotlarını İnceleme | Microsoft Docs
author: Rick-Anderson
description: 'Not: Bu öğreticide güncelleştirilmiş bir sürümünü burada ASP.NET MVC 5 ve Visual Studio 2013 kullanan kullanılabilir. Bu, daha güvenli ve izleyin ve tanıtım çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 1e23189fe927a5145647baa1f8886c4aed057b78
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077634"
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="ce65f-104">Details ve Delete Metotlarını inceleme</span><span class="sxs-lookup"><span data-stu-id="ce65f-104">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="ce65f-105">Tarafından [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="ce65f-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="ce65f-106">Bu öğreticide güncelleştirilmiş bir sürümü kullanılabilir [burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013'ü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ce65f-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="ce65f-107">Bu, daha güvenli ve izlemek çok daha kolay ve daha fazla özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce65f-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="ce65f-108">Öğreticinin bu bölümünde, otomatik olarak oluşturulan inceleyeceğiz `Details` ve `Delete` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ce65f-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="ce65f-109">Details ve Delete Metotlarını inceleme</span><span class="sxs-lookup"><span data-stu-id="ce65f-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="ce65f-110">Açık `Movie` denetleyicisi ve incelemek `Details` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ce65f-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="ce65f-111">Bu eylem yöntemine oluşturulan MVC yapı iskelesi altyapısı yöntemi çağıran bir HTTP isteği gösteren bir yorum ekler.</span><span class="sxs-lookup"><span data-stu-id="ce65f-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="ce65f-112">Bu durumda, bir `GET` üç URL kesimleri, istekle `Movies` denetleyicisi `Details` yöntemi ve bir `ID` değeri.</span><span class="sxs-lookup"><span data-stu-id="ce65f-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="ce65f-113">Kod ilk kullanarak verileri için arama yapmayı kolaylaştırır `Find` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ce65f-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="ce65f-114">Kod doğrular yönteme yerleşik bir önemli güvenlik özelliği olduğu `Find` yöntemi kod şey denemeden önce bir filmi buldu.</span><span class="sxs-lookup"><span data-stu-id="ce65f-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="ce65f-115">Örneğin, bir bilgisayar korsanının hataları siteye bağlantılardan tarafından oluşturulan URL değiştirerek neden olabilirdi `http://localhost:xxxx/Movies/Details/1` gibi bir şey `http://localhost:xxxx/Movies/Details/12345` (veya gerçek bir film temsil etmez başka bir değer).</span><span class="sxs-lookup"><span data-stu-id="ce65f-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="ce65f-116">Null film işaretlemediyseniz null film bir veritabanı hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="ce65f-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="ce65f-117">İnceleme `Delete` ve `DeleteConfirmed` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ce65f-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="ce65f-118">Unutmayın `HTTP Get``Delete` yöntemi belirtilen film silme değil, size gönderebileceği bir filmi görünümünü döndürür (`HttpPost`) silme...</span><span class="sxs-lookup"><span data-stu-id="ce65f-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="ce65f-119">Bir GET'e yanıt olarak bir silme işlemi gerçekleştirme isteği (veya bir düzenleme işlemini gerçekleştirirken bu konular için işlem veya veriler değiştiğinde başka bir işlem oluşturun) bir güvenlik boşluğu açılır.</span><span class="sxs-lookup"><span data-stu-id="ce65f-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="ce65f-120">Bu konu hakkında daha fazla bilgi için Stephen Walther'ın blog girişine bakın [ASP.NET MVC ipucu #46; bunlar güvenlik açıkları oluşturduğundan Sil bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce65f-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="ce65f-121">`HttpPost` Verilerini siler yöntemi adlı `DeleteConfirmed` HTTP POST yöntemi için benzersiz bir imza veya ad vermek için.</span><span class="sxs-lookup"><span data-stu-id="ce65f-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="ce65f-122">İki yöntem imzaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ce65f-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="ce65f-123">Ortak dil çalışma zamanı (CLR) aşırı yüklenmiş yöntemler benzersiz parametre imzası (yöntemi aynı ada ancak farklı parametre listesi) olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ce65f-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="ce65f-124">Bununla birlikte, burada her ikisi de aynı parametre imzasına sahip iki silme yöntemleri--bir get--ve sonrası için gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce65f-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="ce65f-125">(Her ikisi de tek bir tamsayı bir parametre olarak kabul etmeniz gerekir.)</span><span class="sxs-lookup"><span data-stu-id="ce65f-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="ce65f-126">Bu sıralamak için birkaç şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce65f-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="ce65f-127">Yöntemleri farklı adlar vermek için biridir.</span><span class="sxs-lookup"><span data-stu-id="ce65f-127">One is to give the methods different names.</span></span> <span data-ttu-id="ce65f-128">Önceki örnekte yapı iskelesi mekanizması ne yaptığını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ce65f-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="ce65f-129">Bununla birlikte, küçük bir sorunla sunar: ASP.NET bir URL kesimleri eylem yöntemleri adıyla eşler ve bir yöntem yeniden adlandırırsanız, normal olarak Yönlendirme bu yöntem bulmak saptayamazdınız.</span><span class="sxs-lookup"><span data-stu-id="ce65f-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="ce65f-130">Eklenecek olan örnekte gördüğünüz çözümüdür `ActionName("Delete")` özniteliğini `DeleteConfirmed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ce65f-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="ce65f-131">Böylece içeren bir URL bu etkili bir şekilde yönlendirme sistemi eşleme gerçekleştirir <em>/Delete/</em>için bir POST isteği bulabilirsiniz `DeleteConfirmed` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ce65f-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="ce65f-132">Aynı adlara ve imzaları olan yöntemleri ile ilgili bir sorun önlemek için başka bir yaygın yapay olarak kullanılmayan bir parametre eklemek için POST yöntemini imzasını değiştirmek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="ce65f-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="ce65f-133">Örneğin, bazı geliştiriciler bir parametre türü ekleyin `FormCollection` POST yöntemine geçirilir ve ardından yalnızca parametresini kullanmayın:</span><span class="sxs-lookup"><span data-stu-id="ce65f-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="ce65f-134">Özet</span><span class="sxs-lookup"><span data-stu-id="ce65f-134">Summary</span></span>

<span data-ttu-id="ce65f-135">Şimdi yerel bir DB veritabanına veri depolayan tam bir ASP.NET MVC Uygulamam var.</span><span class="sxs-lookup"><span data-stu-id="ce65f-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="ce65f-136">Oluşturma, okuma, güncelleştirme, silme ve filmler için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="ce65f-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="ce65f-137">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ce65f-137">Next Steps</span></span>

<span data-ttu-id="ce65f-138">Oluşturulan ve bir web uygulamasını test sonra sonraki adım, Internet üzerinden kullanmak için diğer kişilerin kullanımına sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ce65f-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="ce65f-139">Bunu yapmak için bir web barındırma sağlayıcısına dağıtmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="ce65f-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="ce65f-140">Microsoft'un sunduğu en fazla 10 web siteleri için ücretsiz bir web barındırma bir [ücretsiz deneme hesabınızı Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="ce65f-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="ce65f-141">My öğreticinin sonraki izleyin ı önerin [bir Windows Azure Web sitesine bir üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET MVC uygulaması dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="ce65f-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ce65f-142">Tom Dykstra'nın orta düzey mükemmel bir öğreticidir [bir ASP.NET MVC uygulaması için bir Entity Framework veri modeli oluşturma](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="ce65f-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="ce65f-143">[StackOverflow](http://stackoverflow.com/help) ve [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx) olan soru sormak için harika bir yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="ce65f-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="ce65f-144">İzleyin [bana](https://twitter.com/RickAndMSFT) my en yeni öğreticiler güncelleştirmeleri alabilmeniz için Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="ce65f-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="ce65f-145">Geri bildirim Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="ce65f-145">Feedback is welcome.</span></span>

<span data-ttu-id="ce65f-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ce65f-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="ce65f-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="ce65f-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ce65f-148">Önceki</span><span class="sxs-lookup"><span data-stu-id="ce65f-148">Previous</span></span>](adding-validation-to-the-model.md)