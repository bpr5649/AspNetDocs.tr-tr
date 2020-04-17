---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Özel Rotalar Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Bir MVC uygulamasına özel rotalar eklemeyi öğrenin. Bu eğitimde, Global.asax dosyasındaki varsayılan rota tablosunu nasıl değiştirdiğinizi öğrenirsiniz.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542748"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="b0080-104">Özel Rotalar Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="b0080-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="b0080-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="b0080-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b0080-106">ASP.NET Bir MVC uygulamasına özel rotalar eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b0080-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="b0080-107">Bu eğitimde, Global.asax dosyasındaki varsayılan rota tablosunu nasıl değiştirdiğinizi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="b0080-108">Bu öğreticide, ASP.NET bir MVC uygulamasına özel bir rota eklemeyi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="b0080-109">Global.asax dosyasındaki varsayılan rota tablosunu özel bir rotayla nasıl değiştirebilirsiniz öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b0080-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="b0080-110">MVC uygulamalarında ASP.NET, varsayılan rota tablosu gayet iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="b0080-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="b0080-111">Ancak, özel yönlendirme gereksinimleriniz olduğunu keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="b0080-112">Bu durumda, özel bir rota oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="b0080-113">Örneğin, bir blog uygulaması oluşturuyorolduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="b0080-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="b0080-114">Şuna benzeyen gelen istekleri işlemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0080-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="b0080-115">/Arşiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="b0080-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="b0080-116">Bir kullanıcı bu isteği girdiğinde, 25/12/2009 tarihine karşılık gelen blog girişini iade etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="b0080-117">Bu tür bir isteği işlemek için özel bir rota oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0080-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="b0080-118">Listeleme 1'deki Global.asax dosyası, /Arşiv/*giriş tarihine*benzeyen istekleri işleyen Blog adlı yeni bir özel rota içerir.</span><span class="sxs-lookup"><span data-stu-id="b0080-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="b0080-119">**Listeleme 1 - Global.asax (özel rota ile)**</span><span class="sxs-lookup"><span data-stu-id="b0080-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="b0080-120">Rota tablosuna eklediğiniz yolların sırası önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b0080-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="b0080-121">Yeni özel Blog rotamız, varolan Varsayılan rotadan önce eklenir.</span><span class="sxs-lookup"><span data-stu-id="b0080-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="b0080-122">Siparişi tersine çevirdiyseniz, Varsayılan yol her zaman özel rota yerine çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b0080-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="b0080-123">Özel Blog rotası / Arşiv/ ile başlayan herhangi bir istek eşleşir.</span><span class="sxs-lookup"><span data-stu-id="b0080-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="b0080-124">Bu nedenle, aşağıdaki URL'lerin tümüyle eşleşir:</span><span class="sxs-lookup"><span data-stu-id="b0080-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="b0080-125">/Arşiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="b0080-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="b0080-126">/Arşiv/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="b0080-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="b0080-127">/Arşiv/elma</span><span class="sxs-lookup"><span data-stu-id="b0080-127">/Archive/apple</span></span>

<span data-ttu-id="b0080-128">Özel rota, gelen isteği Arşiv adlı bir denetleyiciyle eşler ve Giriş() eylemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b0080-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="b0080-129">Giriş() yöntemi çağrıldığında, giriş tarihi entryDate adlı bir parametre olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="b0080-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="b0080-130">Listeleme 2'deki denetleyiciile Blog özel rotasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="b0080-131">**Listeleme 2 - ArchiveController.vb**</span><span class="sxs-lookup"><span data-stu-id="b0080-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="b0080-132">Listeleme 2'deki Giriş() yönteminin DateTime türünden bir parametreyi kabul ettiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b0080-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="b0080-133">MVC çerçevesi, giriş tarihini URL'den otomatik olarak DateTime değerine dönüştürecek kadar akıllıdır.</span><span class="sxs-lookup"><span data-stu-id="b0080-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="b0080-134">URL'den giriş tarihi parametresi DateTime'a dönüştürülemiyorsa, bir hata yükseltilir (Bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="b0080-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="b0080-135">**Şekil 1 - Parametre dönüştürme hatası**</span><span class="sxs-lookup"><span data-stu-id="b0080-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="b0080-136">[![Yeni Proje iletişim kutusu](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b0080-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="b0080-137">**Şekil 01**: Parametredönüştürme hatası ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b0080-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="b0080-138">Özet</span><span class="sxs-lookup"><span data-stu-id="b0080-138">Summary</span></span>

<span data-ttu-id="b0080-139">Bu öğreticinin amacı, özel bir rotayı nasıl oluşturabileceğinizi göstermekti.</span><span class="sxs-lookup"><span data-stu-id="b0080-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="b0080-140">Blog girişlerini temsil eden Global.asax dosyasındaki rota tablosuna özel bir rota eklemeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b0080-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="b0080-141">Blog girişleri isteklerini ArchiveController adlı bir denetleyiciye ve Entry() adlı bir denetleyici eylemine nasıl eşlendirebileceğimizi tartıştık.</span><span class="sxs-lookup"><span data-stu-id="b0080-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0080-142">[Önceki](asp-net-mvc-controller-overview-vb.md)
> [Sonraki](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b0080-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
