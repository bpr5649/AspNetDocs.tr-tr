---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: (C#) görünüm ana sayfalarıyla sayfa düzenleri oluşturma | Microsoft Docs
author: microsoft
description: Bu öğreticide, görünüm ana sayfalarına yararlanarak uygulamanızda ortak bir sayfa düzeni için birden çok sayfa oluşturma konusunda bilgi edinin. Kullanabileceğiniz bir...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d09a38c2bea9e8beb91e322ed7e4a9d337fa0843
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412638"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="de392-104">Görünüm Ana Sayfalarıyla Sayfa Düzenleri Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="de392-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="de392-105">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="de392-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="de392-106">PDF'yi indirin</span><span class="sxs-lookup"><span data-stu-id="de392-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="de392-107">Bu öğreticide, görünüm ana sayfalarına yararlanarak uygulamanızda ortak bir sayfa düzeni için birden çok sayfa oluşturma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="de392-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="de392-108">Örneğin, iki sütunlu sayfa düzeni tanımlamak ve web uygulamanızda tüm sayfalar için iki sütunlu düzeni kullanmak için ana görünüm sayfası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>


## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="de392-109">Görünüm ana sayfalarıyla sayfa düzenleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="de392-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="de392-110">Bu öğreticide, görünüm ana sayfalarına yararlanarak uygulamanızda ortak bir sayfa düzeni için birden çok sayfa oluşturma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="de392-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="de392-111">Örneğin, iki sütunlu sayfa düzeni tanımlamak ve web uygulamanızda tüm sayfalar için iki sütunlu düzeni kullanmak için ana görünüm sayfası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="de392-112">Ayrıca görünümün birden çok sayfada uygulamanızda ortak içerik paylaşmak için ana sayfalar yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="de392-113">Örneğin, bir görünüm ana sayfaya, Web sitesi logosu, gezinti bağlantılarının ve başlık reklamları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="de392-114">Bu şekilde, uygulamanızdaki her sayfada bu içerik otomatik olarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="de392-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="de392-115">Bu öğreticide, yeni bir görünüm ana sayfası oluşturun ve ana sayfasını temel alan yeni bir görünüm içerik sayfası oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="de392-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="de392-116">Görünüm ana sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="de392-116">Creating a View Master Page</span></span>

<span data-ttu-id="de392-117">İki sütunlu düzeni tanımlayan bir görünümü ana sayfası oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="de392-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="de392-118">Yeni bir görünüm ana sayfası bir MVC projesi için görünümler/paylaşılan klasörünü sağ tıklayarak menü seçeneğini belirleyerek eklediğiniz **Ekle, yeni öğe**, seçerek **MVC görünüm ana sayfa** şablonu (bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="de392-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>


[![A<span data-ttu-id="de392-119">Görünüm ana sayfası dding]</span><span class="sxs-lookup"><span data-stu-id="de392-119">dding a view master page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

<span data-ttu-id="de392-120">**Şekil 01**: Görünüm ana sayfası ekleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="de392-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="de392-121">Bir uygulamada birden fazla ana görünüm sayfası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="de392-122">Her görünüm ana sayfası farklı sayfa düzeni tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="de392-123">Örneğin, iki sütunlu düzeni için belirli sayfaları ve diğer sayfalara üç sütunlu düzeni isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="de392-124">Görünüm ana sayfası gibi standart bir ASP.NET MVC görünüm çok arar.</span><span class="sxs-lookup"><span data-stu-id="de392-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="de392-125">Ancak, normal görünümünden farklı olarak, bir veya daha fazla görünüm ana sayfası içeren `<asp:ContentPlaceHolder>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="de392-126">`<contentplaceholder>` Etiketler tek tek bir içerik sayfasındaki geçersiz kılınabilir ana sayfa alanlarının işaretlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de392-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="de392-127">Örneğin, iki sütunlu düzeni listeleme 1 görünüm ana sayfasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="de392-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="de392-128">İki tane `<contentplaceholder>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="de392-129">Bir `<ContentPlaceHolder>` her sütun için.</span><span class="sxs-lookup"><span data-stu-id="de392-129">One `<ContentPlaceHolder>` for each column.</span></span>

**<span data-ttu-id="de392-130">Kod 1 –</span><span class="sxs-lookup"><span data-stu-id="de392-130">Listing 1 –</span></span> `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="de392-131">Ana sayfa 1 listeleme içeren iki görünüm gövdesi `<div>` iki sütunlara karşılık gelen etiketleri.</span><span class="sxs-lookup"><span data-stu-id="de392-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="de392-132">Geçişli stil sayfası sütun sınıf her ikisi de uygulanır `<div>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="de392-133">Bu sınıf ana sayfanın en üstündeki bildirilen stil sayfası içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="de392-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="de392-134">Tasarım görünümüne geçerek görünüm ana sayfasını nasıl işlenir önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="de392-135">Kaynak kod düzenleyicisinin alt sol tasarım sekmesine tıklayın (bkz: Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="de392-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>


[![P<span data-ttu-id="de392-136">bir ana sayfa tasarımcıyı gözden geçirme]</span><span class="sxs-lookup"><span data-stu-id="de392-136">reviewing a master page in the designer]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

<span data-ttu-id="de392-137">**Şekil 02**: Bir ana sayfa tasarımcıyı Önizleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="de392-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>


### <a name="creating-a-view-content-page"></a><span data-ttu-id="de392-138">Bir görünüm içerik sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="de392-138">Creating a View Content Page</span></span>

<span data-ttu-id="de392-139">Görünüm ana sayfası oluşturduktan sonra içerik sayfalarının görünüm ana sayfasını temel alan bir veya daha fazla görünüm oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="de392-140">Görünümler/giriş klasörünü sağ tıklayarak dizini bir görünüm içerik sayfası için giriş denetleyicisine gibi oluşturabilirsiniz seçerek **Ekle, yeni öğe**u seçerek **MVC görünüm içerik sayfası** girme şablonu ' % s'adı, Index.aspx tıklayıp **Ekle** (bkz: Şekil 3) düğmesini.</span><span class="sxs-lookup"><span data-stu-id="de392-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>


[![A<span data-ttu-id="de392-141">bir görünüm içerik sayfası dding]</span><span class="sxs-lookup"><span data-stu-id="de392-141">dding a view content page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

<span data-ttu-id="de392-142">**Şekil 03**: Bir görünüm içerik sayfası ekleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="de392-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>


<span data-ttu-id="de392-143">Ekle düğmesine tıkladıktan sonra Görünüm içerik sayfası ile ilişkilendirmek için bir ana görünüm sayfası seçmenize olanak sağlayan yeni bir iletişim kutusu görünür (bkz: Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="de392-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="de392-144">Önceki bölümde oluşturduğumuz Site.master görünüm ana sayfasına gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>


[![S<span data-ttu-id="de392-145">ana sayfa seçme]</span><span class="sxs-lookup"><span data-stu-id="de392-145">electing a master page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

<span data-ttu-id="de392-146">**Şekil 04**: Ana sayfa seçme ([tam boyutlu görüntüyü görmek için tıklatın](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="de392-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>


<span data-ttu-id="de392-147">Site.master ana sayfasını temel alan yeni bir görünüm içerik sayfası oluşturduktan sonra 2 listeleme dosyasında alın.</span><span class="sxs-lookup"><span data-stu-id="de392-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

**<span data-ttu-id="de392-148">Kod 2 –</span><span class="sxs-lookup"><span data-stu-id="de392-148">Listing 2 –</span></span> `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="de392-149">Bu görünüm içeren bildirimi bir `<asp:Content>` her biri için karşılık gelen etiket `<asp:ContentPlaceHolder>` görünüm ana sayfasındaki etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="de392-150">Her `<asp:Content>` etiketi içeren belirli işaret eden bir ContentPlaceHolderID özniteliği `<asp:ContentPlaceHolder>` , onu geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="de392-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="de392-151">Ayrıca, içerik görünümü sayfası listeleme 2 normal açılış ve kapanış HTML etiketleri herhangi birini içermediğinden emin dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="de392-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="de392-152">Örneğin, bu açılış ve kapanış içermiyor `<html>` veya `<head>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="de392-153">Normal açılış ve kapanış etiketlerinin tümünün görünüm ana sayfada yer alır.</span><span class="sxs-lookup"><span data-stu-id="de392-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="de392-154">Bir görünüm içerik sayfası görüntülemek istediğiniz herhangi bir içerik içinde yerleştirilmelidir bir `<asp:Content>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="de392-155">Herhangi bir HTML veya bu etiketleri dışında diğer içerik yerleştirirseniz, sayfayı görüntülemeye çalıştığınızda bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="de392-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="de392-156">Geçersiz kılma gerekmez her `<asp:ContentPlaceHolder>` bir ana sayfa içerik görünümü sayfasında etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="de392-157">Yalnızca geçersiz kılmak gereken bir `<asp:ContentPlaceHolder>` etiketi ile belirli bir içeriğe etiket değiştirmek istediğinizde.</span><span class="sxs-lookup"><span data-stu-id="de392-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="de392-158">Örneğin, yalnızca iki listeleme 3'te değiştirilmiş Index görünümünü içerir `<asp:Content>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="de392-159">Her biri `<asp:Content>` etiketleri, bazı metinleri içerir.</span><span class="sxs-lookup"><span data-stu-id="de392-159">Each of the `<asp:Content>` tags includes some text.</span></span>

**<span data-ttu-id="de392-160">Kod 3 –</span><span class="sxs-lookup"><span data-stu-id="de392-160">Listing 3 –</span></span> `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="de392-161">3 liste görünümünde istendiğinde, Şekil 5'te sayfasını işler.</span><span class="sxs-lookup"><span data-stu-id="de392-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="de392-162">Görünüm iki sütuna sahip bir sayfa işler dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="de392-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="de392-163">Ayrıca, içerik görünümü içerik sayfasından ana görünüm sayfası içerikle birleştirilir fark</span><span class="sxs-lookup"><span data-stu-id="de392-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>


[![T<span data-ttu-id="de392-164">He dizin görünüm içerik sayfası]</span><span class="sxs-lookup"><span data-stu-id="de392-164">he Index view content page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

<span data-ttu-id="de392-165">**Şekil 05**: Dizin görünüm içerik sayfası ([tam boyutlu görüntüyü görmek için tıklatın](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="de392-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>


### <a name="modifying-view-master-page-content"></a><span data-ttu-id="de392-166">Görünüm ana sayfa içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="de392-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="de392-167">Neredeyse karşılaştığınız bir sorun, farklı bir görünüm içerik sayfalarını istendiğinde görünüm ana sayfa içeriği değiştirme sorununu hemen görünüm ana sayfalarıyla çalışırken.</span><span class="sxs-lookup"><span data-stu-id="de392-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="de392-168">Örneğin, her sayfada web uygulamanıza benzersiz bir başlık olmasını istersiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="de392-169">Ancak, ana sayfa görünümü ve görünüm içerik sayfası başlığı bildirilir.</span><span class="sxs-lookup"><span data-stu-id="de392-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="de392-170">Bu nedenle, nasıl sayfa başlığının her görünüm içerik sayfası için özelleştirdiğiniz?</span><span class="sxs-lookup"><span data-stu-id="de392-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="de392-171">Görünüm içerik sayfası tarafından gördüğü başlık değiştirebileceğiniz iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="de392-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="de392-172">İlk olarak, bir sayfa başlığı başlık özniteliğiyle atayabilirsiniz `<%@ page %>` yönergesi bildirilen bir görünüm içerik sayfası üstünde.</span><span class="sxs-lookup"><span data-stu-id="de392-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="de392-173">Örneğin, dizin görünümü sayfa başlığı "Süper harika Web sitesi" atamak istiyorsanız, aşağıdaki yönerge Index görünümünü üst kısmındaki şunları içerebilir:</span><span class="sxs-lookup"><span data-stu-id="de392-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="de392-174">Dizin görünümünün tarayıcıya işlendiğinde, istenen başlık tarayıcının başlık çubuğunda görünür:</span><span class="sxs-lookup"><span data-stu-id="de392-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>


[![B<span data-ttu-id="de392-175">Tarayıcıdan başlık çubuğu]</span><span class="sxs-lookup"><span data-stu-id="de392-175">rowser title bar]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)


<span data-ttu-id="de392-176">Bir ana görünüm sayfası, sırayla çalışmak üzere title özniteliği için karşılaması gereken önemli bir gereksinim yoktur.</span><span class="sxs-lookup"><span data-stu-id="de392-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="de392-177">Görünüm ana sayfası içermelidir bir `<head runat="server">` yerine normal bir etiket `<head>` üstbilgisi etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="de392-178">Varsa `<head>` etiketi runat içermez başlığı görünmez sonra = "server" özniteliği.</span><span class="sxs-lookup"><span data-stu-id="de392-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="de392-179">Ana sayfa içerir gerekli varsayılan görünüm `<head runat="server">` etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="de392-180">Tek görünüm içerik sayfasından ana sayfa içeriği değiştirme için alternatif bir yaklaşım sarmaktır değiştirmek için istediğiniz bölgede bir `<asp:ContentPlaceHolder>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="de392-181">Örneğin, yalnızca başlığı, aynı zamanda bir ana görünüm sayfası tarafından oluşturulan meta etiketleri değiştirmek istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="de392-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="de392-182">Ana görünüm sayfası 4 listesi içeren bir `<asp:ContentPlaceHolder>` içinde etiketi kendi `<head>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="de392-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

**<span data-ttu-id="de392-183">4 listeleme –</span><span class="sxs-lookup"><span data-stu-id="de392-183">Listing 4 –</span></span> `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="de392-184">Dikkat `<asp:ContentPlaceHolder>` listeleme 4'te etiketi varsayılan içerik içerir: varsayılan başlık ve varsayılan meta etiketler.</span><span class="sxs-lookup"><span data-stu-id="de392-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="de392-185">Bu geçersiz kılmazsanız `<asp:ContentPlaceHolder>` varsayılan içerik görüntülenecek sonra tek tek görünüm içerik sayfası etiketleyin.</span><span class="sxs-lookup"><span data-stu-id="de392-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="de392-186">Geçersiz kılmaları listeleme 5'teki içerik görünümü sayfası `<asp:ContentPlaceHolder>` özel bir başlık ve özel meta etiketler görüntülemek için etiket.</span><span class="sxs-lookup"><span data-stu-id="de392-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

**<span data-ttu-id="de392-187">5 listeleme –</span><span class="sxs-lookup"><span data-stu-id="de392-187">Listing 5 –</span></span> `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="de392-188">Özet</span><span class="sxs-lookup"><span data-stu-id="de392-188">Summary</span></span>

<span data-ttu-id="de392-189">Bu öğreticide, ana sayfalar ve içerik sayfalarını görüntülemek için temel bir giriş sağlanan.</span><span class="sxs-lookup"><span data-stu-id="de392-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="de392-190">Ana sayfalar yeni görünüm oluşturma ve bunları temel alan içerik sayfalarını görüntüleme oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="de392-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="de392-191">Ayrıca belirli görünüm içerik sayfası görünüm ana sayfadan içerik nasıl değiştirebileceğiniz incelenir.</span><span class="sxs-lookup"><span data-stu-id="de392-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="de392-192">[Önceki](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [İleri](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="de392-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
