---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: Okunabilir URL'ler oluşturma ASP.NET Web sayfaları (Razor) siteler | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, bir ASP.NET Web sayfaları (Razor) Web sitesi ve bu daha okunabilir ve SEO için daha iyi URL'leri kullanmanıza nasıl sağladığını yönlendirme açıklanır. Gerekir...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131764"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="50aef-104">ASP.NET Web sayfaları (Razor) sitelerinde okunabilir URL'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="50aef-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="50aef-105">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="50aef-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="50aef-106">Bu makalede, bir ASP.NET Web sayfaları (Razor) Web sitesi ve bu daha okunabilir ve SEO için daha iyi URL'leri kullanmanıza nasıl sağladığını yönlendirme açıklanır.</span><span class="sxs-lookup"><span data-stu-id="50aef-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="50aef-107">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="50aef-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="50aef-108">Nasıl ASP.NET yönlendirmesi daha okunabilir ve aranabilir URL'lere kullanmanıza izin vermek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="50aef-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="50aef-109">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="50aef-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="50aef-110">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="50aef-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="50aef-111">Bu öğreticide, ASP.NET Web Pages 2 ile de çalışır.</span><span class="sxs-lookup"><span data-stu-id="50aef-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="50aef-112">Yönlendirme hakkında</span><span class="sxs-lookup"><span data-stu-id="50aef-112">About Routing</span></span>

<span data-ttu-id="50aef-113">Sitenizde sayfaları için URL'leri site ne kadar iyi çalıştığı bir etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="50aef-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="50aef-114">Bir URL bu &quot;kolay&quot; sitesini kullanmak üzere kişiler için daha kolay yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50aef-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="50aef-115">Site için arama motoru iyileştirmesi (SEO) ile de yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="50aef-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="50aef-116">ASP.NET Web sitesini kolay URL'leri otomatik olarak kullanma yeteneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="50aef-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="50aef-117">ASP.NET yerine yalnızca bir dosya sunucusuna işaret eden kullanıcı eylemleri açıklayan anlamlı URL'ler oluşturmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="50aef-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="50aef-118">Bu URL'ler için kurgusal bir blog göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="50aef-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="50aef-119">Bu URL'leri aşağıdaki karşılaştırma:</span><span class="sxs-lookup"><span data-stu-id="50aef-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="50aef-120">İlk çiftini, bir kullanıcı blog kullanarak görüntülendiğini bilmesi gerekir *blog.cshtml* sayfasında ve doğru bir kategori veya tarih aralığını alır bir sorgu dizesi oluşturmak sahip.</span><span class="sxs-lookup"><span data-stu-id="50aef-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="50aef-121">İkinci bir örnekler kümesini kavrama ve oluşturmak çok daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="50aef-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="50aef-122">İlk örnek için URL'leri ayrıca doğrudan belirli bir dosyaya işaret (*blog.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="50aef-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="50aef-123">Herhangi bir nedenden dolayı sunucuda başka bir klasöre blog taşınan veya blog farklı bir sayfayı kullanmak için yazılan, bağlantıları yanlış olur.</span><span class="sxs-lookup"><span data-stu-id="50aef-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="50aef-124">İkinci Küme URL'leri belirli bir sayfaya işaret etmiyor da blog uygulanması veya konum değişirse, URL'leri yine de geçerli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="50aef-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="50aef-125">ASP.NET Web sayfaları, ASP.NET kullandığından bu Yukarıdaki örneklerde gibi daha kolay URL'leri oluşturabilirsiniz *yönlendirme*.</span><span class="sxs-lookup"><span data-stu-id="50aef-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="50aef-126">Yönlendirme isteği gerçekleştirmek bir URL'den bir sayfayı (veya sayfaları) için mantıksal eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="50aef-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="50aef-127">Eşleme mantıksal olduğu için (fiziksel, belirli bir dosyaya), yönlendirme URL'leri siteniz için nasıl tanımladığınızı büyük esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="50aef-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="50aef-128">Yönlendirmenin nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="50aef-128">How Routing Works</span></span>

<span data-ttu-id="50aef-129">ASP.NET isteği işlerken yönlendirmek nasıl saptamak için URL'ye okur.</span><span class="sxs-lookup"><span data-stu-id="50aef-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="50aef-130">ASP.NET, dosyaları diskte URL'sine soldan sağa doğru giden tek tek bölümleri eşleşmiyor dener.</span><span class="sxs-lookup"><span data-stu-id="50aef-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="50aef-131">Bir eşleşme varsa, URL'yi kalan herhangi bir şey sayfasına geçirilir *yol bilgisi*.</span><span class="sxs-lookup"><span data-stu-id="50aef-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="50aef-132">Birisi bu URL'yi kullanarak bir isteği yapar düşünün:</span><span class="sxs-lookup"><span data-stu-id="50aef-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="50aef-133">Arama şöyle geçer:</span><span class="sxs-lookup"><span data-stu-id="50aef-133">The search goes like this:</span></span>

1. <span data-ttu-id="50aef-134">Bir dosya yolu ve adı yok */a/b/c.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="50aef-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="50aef-135">Bu durumda, bu sayfayı çalıştırın ve hiçbir bilgi geçirin.</span><span class="sxs-lookup"><span data-stu-id="50aef-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="50aef-136">Aksi takdirde...</span><span class="sxs-lookup"><span data-stu-id="50aef-136">Otherwise ...</span></span>
2. <span data-ttu-id="50aef-137">Bir dosya yolu ve adı yok */a/b.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="50aef-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="50aef-138">Bu nedenle, bu sayfayı çalıştırın ve değeri geçirin `c` ona.</span><span class="sxs-lookup"><span data-stu-id="50aef-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="50aef-139">Aksi takdirde...</span><span class="sxs-lookup"><span data-stu-id="50aef-139">Otherwise …</span></span>
3. <span data-ttu-id="50aef-140">Bir dosya yolu ve adı yok */a.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="50aef-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="50aef-141">Bu nedenle, bu sayfayı çalıştırın ve değeri geçirin `b/c` ona.</span><span class="sxs-lookup"><span data-stu-id="50aef-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="50aef-142">Hayır tam bulunan arama için eşleşiyorsa *.cshtml* belirtilen klasörlerine dosyaları ASP.NET devam bu dosyalar sırayla aranıyor:</span><span class="sxs-lookup"><span data-stu-id="50aef-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="50aef-143">*/a/b/c/default.cshtml* (hiçbir yol bilgisi).</span><span class="sxs-lookup"><span data-stu-id="50aef-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="50aef-144">*/a/b/c/index.cshtml* (hiçbir yol bilgisi).</span><span class="sxs-lookup"><span data-stu-id="50aef-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="50aef-145">Açık olması için belirli bir sayfa istekleri (diğer bir deyişle, içeren istekleri *.cshtml* dosya adı uzantısı) yalnızca beklediğiniz gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="50aef-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="50aef-146">Bir isteği ister `http://www.contoso.com/a/b.cshtml` sayfasının çalışacağı *b.cshtml* düzgün.</span><span class="sxs-lookup"><span data-stu-id="50aef-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="50aef-147">Bir sayfa içinde sayfa aracılığıyla yolu bilgi edinebilirsiniz `UrlData` bir sözlük özelliği.</span><span class="sxs-lookup"><span data-stu-id="50aef-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="50aef-148">Adlı bir dosyaya sahip olduğunuzu düşünün *ViewCustomers.cshtml* ve bu istek, sitenizi alır:</span><span class="sxs-lookup"><span data-stu-id="50aef-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="50aef-149">Yukarıdaki kuralları açıklandığı gibi istek sayfanıza geçer.</span><span class="sxs-lookup"><span data-stu-id="50aef-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="50aef-150">İçinde sayfasında, aşağıdaki gibi bir kod almak ve yol bilgilerini görüntülemek için kullanabilirsiniz (Bu durumda, değer &quot;1000&quot;):</span><span class="sxs-lookup"><span data-stu-id="50aef-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="50aef-151">Yönlendirme tam dosya adları içermeyen çünkü olabilir belirsizlik aynı sayfaları varsa ad ancak farklı bir dosya adı uzantıları (örneğin, *MyPage.cshtml* ve *MyPage.html*) .</span><span class="sxs-lookup"><span data-stu-id="50aef-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="50aef-152">Yönlendirme sorunlarını önlemek için sitenizde kendi uzantı yalnızca, adları farklı sayfaları yoksa emin olmak idealdir.</span><span class="sxs-lookup"><span data-stu-id="50aef-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="50aef-153">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="50aef-153">Additional Resources</span></span>

<span data-ttu-id="50aef-154">[WebMatrix - URL'leri, UrlData ve SEO için yönlendirme](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span><span class="sxs-lookup"><span data-stu-id="50aef-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="50aef-155">Bu blog girişi Mike Brind tarafından ASP.NET Web Pages'de yönlendirmenin nasıl çalıştığıyla ilgili bazı ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="50aef-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
