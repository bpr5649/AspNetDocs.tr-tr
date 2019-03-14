---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Görünümü (UI) oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: aa0ea68dd83a294e6d6c343887738c60eef595bf
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069072"
---
<a name="create-the-view-ui"></a><span data-ttu-id="6069a-102">Görünümü (Kullanıcı Arabirimi) Oluşturma</span><span class="sxs-lookup"><span data-stu-id="6069a-102">Create the View (UI)</span></span>
====================
<span data-ttu-id="6069a-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6069a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6069a-104">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="6069a-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="6069a-105">Bu bölümde, uygulama için HTML tanımlayın ve HTML ve görünüm modeli arasında veri bağlaması Ekle başlar.</span><span class="sxs-lookup"><span data-stu-id="6069a-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="6069a-106">Views/Home/Index.cshtml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="6069a-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="6069a-107">Bu dosyanın tüm içeriğini aşağıdakiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6069a-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="6069a-108">Çoğu `div` öğeleri bulunduğundan için [önyükleme](http://getbootstrap.com/) stil oluşturma.</span><span class="sxs-lookup"><span data-stu-id="6069a-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="6069a-109">En önemli öğeler `data-bind` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="6069a-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="6069a-110">Bu öznitelik HTML görünümü modeline bağlar.</span><span class="sxs-lookup"><span data-stu-id="6069a-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="6069a-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6069a-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="6069a-112">Bu örnekte, &quot; `text` &quot; nedenler bağlamayı `<p>` değerini gösterilecek öğe `error` özelliğinden görünüm modeli.</span><span class="sxs-lookup"><span data-stu-id="6069a-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="6069a-113">Bu geri çağırma `error` olarak bildirilen bir `ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="6069a-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="6069a-114">Her yeni bir değer atanır `error`, Knockout güncelleştirmeleri metinde `<p>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="6069a-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="6069a-115">`foreach` Bağlama içeriğini döngü Knockout söyler `books` dizisi.</span><span class="sxs-lookup"><span data-stu-id="6069a-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="6069a-116">Knockout dizideki her öğe için yeni bir oluşturur &lt;li&gt; öğesi.</span><span class="sxs-lookup"><span data-stu-id="6069a-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="6069a-117">Bağlama bağlamı içinde `foreach` dizideki özelliklere bakın.</span><span class="sxs-lookup"><span data-stu-id="6069a-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="6069a-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6069a-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="6069a-119">Burada `text` bağlama her kitabın Yazar özelliği okur.</span><span class="sxs-lookup"><span data-stu-id="6069a-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="6069a-120">Uygulamayı şimdi çalıştırırsanız, şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6069a-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="6069a-121">Kitap listesi, Sayfa yüklendikten sonra zaman uyumsuz olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="6069a-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="6069a-122">Şu anda &quot;ayrıntıları&quot; Bağlantılar işlevsel değildir.</span><span class="sxs-lookup"><span data-stu-id="6069a-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="6069a-123">Sonraki bölümde bu işlevselliğini ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="6069a-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6069a-124">[Önceki](part-6.md)
> [İleri](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="6069a-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
