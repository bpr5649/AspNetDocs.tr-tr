---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: Derecelendirme denetimi (VB) oluşturma | Microsoft Docs
author: wenz
description: E-ticaret topluluk sitelerine, birçok Web sitesi kullanıcılarının oranı makaleler veya öğeleri sunar. Bu genellikle bazı bir kodlama çabası gerektirir, ancak sahibiz...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 91523180501f1d1eb67586bf97649ad6226ec565
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59413236"
---
# <a name="creating-a-rating-control-vb"></a><span data-ttu-id="5b6fe-104">Derecelendirme Denetimi Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="5b6fe-104">Creating a Rating Control (VB)</span></span>

<span data-ttu-id="5b6fe-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5b6fe-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5b6fe-106">[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5b6fe-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)</span></span>

> <span data-ttu-id="5b6fe-107">E-ticaret topluluk sitelerine, birçok Web sitesi kullanıcılarının oranı makaleler veya öğeleri sunar.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="5b6fe-108">Bu genellikle bazı bir kodlama çabası gerektirir, ancak Denetim Araç Seti için sunduğumuz elden sahibiz.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="5b6fe-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5b6fe-109">Overview</span></span>

<span data-ttu-id="5b6fe-110">E-ticaret topluluk sitelerine, birçok Web sitesi kullanıcılarının oranı makaleler veya öğeleri sunar.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="5b6fe-111">Bu genellikle bazı bir kodlama çabası gerektirir, ancak Denetim Araç Seti için sunduğumuz elden sahibiz.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="5b6fe-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="5b6fe-112">Steps</span></span>

<span data-ttu-id="5b6fe-113">Öncelikle, görüntüleri (en az) iki tür ihtiyacınız: bir doldurulmuş bir derecelendirme öğesi ve boş derecelendirme öğenin bir.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="5b6fe-114">Bir derecelendirme genellikle bir yıldız veya bir gülen öğesidir.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="5b6fe-115">Bu senaryo için üç dosyaları, smiley.png ve empty.png ve gülen done.png Bu öğretici için kaynak kodu indirmeleri bir parçası olarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="5b6fe-116">Ardından, yeni bir ASP.NET dosyası oluşturun ve ekleyerek başlayın bir `ScriptManager` denetimi:</span><span class="sxs-lookup"><span data-stu-id="5b6fe-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

<span data-ttu-id="5b6fe-117">Ardından, ekleme `Rating` ASP.NET AJAX Denetim Araç Seti denetim.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="5b6fe-118">Aşağıdaki öznitelikler için bu örneği ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b6fe-118">The following attributes need to be set for this example:</span></span>

- `CurrentRating` <span data-ttu-id="5b6fe-119">kullanılacak ilk derecelendirme</span><span class="sxs-lookup"><span data-stu-id="5b6fe-119">the initial rating to be used</span></span>
- `MaxRating` <span data-ttu-id="5b6fe-120">en yüksek derecelendirme</span><span class="sxs-lookup"><span data-stu-id="5b6fe-120">the maximum rating</span></span>
- `EmptyStarCssClass` <span data-ttu-id="5b6fe-121">CSS sınıfının bir derecelendirme öğesi (star) boş olduğunda kullanın</span><span class="sxs-lookup"><span data-stu-id="5b6fe-121">the CSS class to use when a rating item ( star ) is empty</span></span>
- `FilledStarCssClass` <span data-ttu-id="5b6fe-122">bir derecelendirme öğesi (star) doldurulurken kullanmak için CSS sınıfı</span><span class="sxs-lookup"><span data-stu-id="5b6fe-122">the CSS class to use when a rating item ( star ) is filled out</span></span>
- `StarCssClass` <span data-ttu-id="5b6fe-123">görünür bir durum için kullanılacak bir CSS sınıfı</span><span class="sxs-lookup"><span data-stu-id="5b6fe-123">the CSS class to use for a visible stat</span></span>
- `WaitingStarCssClass` <span data-ttu-id="5b6fe-124">Yıldız derecelendirmesi sunucuya geri gönderilirken kullanılacak CSS sınıfı</span><span class="sxs-lookup"><span data-stu-id="5b6fe-124">the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="5b6fe-125">Ve derecelendirme denetimi ile beşinci oluşturan biçimlendirmesi şöyledir hangi none doldurulan başlangıçta öğeleri (smileys):</span><span class="sxs-lookup"><span data-stu-id="5b6fe-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

<span data-ttu-id="5b6fe-126">Üç başvurulan CSS sınıfları artık uygun görüntü dosyaları göstermek, CSS kullanarak yapmak kolaydır gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b6fe-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

<span data-ttu-id="5b6fe-127">Üç görüntü yüksekliğini ve genişliğini sağlarsanız, görüntüyü oluşturan bir bit messed boyutlandırılabilecek emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="5b6fe-128">Son olarak, derecelendirme sonucunu kullanıcıya görüntüleneceğini (veya, en az bir veritabanında kayıtlı).</span><span class="sxs-lookup"><span data-stu-id="5b6fe-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="5b6fe-129">Bu nedenle sunucu derecelendirme forma geri göndermek için bir kısa mesaj ve bir Gönder düğmesi çıktısı için bir etiket ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5b6fe-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

<span data-ttu-id="5b6fe-130">Sunucu tarafı kodunda erişim derecelendirme denetimi aracılığıyla kendi `ID` ve ardından erişim kendi `CurrentRating` örneğimizde 0 ile 5 arasında bir değer seçili derecelendirme öğe sayısı olan özelliği.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

<span data-ttu-id="5b6fe-131">Sayfayı kaydedin ve tarayıcınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="5b6fe-132">(Başlangıçta boş) derecelendirmesi öğelerin üzerine geldiğinizde, bir JavaScript etkisi oluşur: Derecelendirme değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="5b6fe-133">Yıldızlar kümesini temel tıkladığınızda, geçerli derecelendirme korunur.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="5b6fe-134">Son olarak, formu gönderdiğinde, sunucu tarafı kodu seçili derecelendirme çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5b6fe-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


[![C<span data-ttu-id="5b6fe-135">bir derecelendirme sistemi olabildiğince az kodla reating]</span><span class="sxs-lookup"><span data-stu-id="5b6fe-135">reating a rating system with minimal code]</span></span>(creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

<span data-ttu-id="5b6fe-136">En az kodla derecelendirme sistemi oluşturma ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-rating-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5b6fe-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5b6fe-137">Önceki</span><span class="sxs-lookup"><span data-stu-id="5b6fe-137">Previous</span></span>](creating-a-rating-control-cs.md)
