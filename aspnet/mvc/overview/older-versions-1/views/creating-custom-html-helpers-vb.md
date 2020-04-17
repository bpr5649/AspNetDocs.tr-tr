---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Özel HTML Yardımcıları Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Helper'dan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 52f16bf666edc9f1c95c01faf004e303fcb6a0b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542514"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="2c485-104">Özel HTML Yardımcıları Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="2c485-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="2c485-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="2c485-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2c485-106">PDF’yi İndir</span><span class="sxs-lookup"><span data-stu-id="2c485-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="2c485-107">Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir.</span><span class="sxs-lookup"><span data-stu-id="2c485-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="2c485-108">HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="2c485-109">Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir.</span><span class="sxs-lookup"><span data-stu-id="2c485-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="2c485-110">HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="2c485-111">Bu öğreticinin ilk bölümünde, bazı mevcut HTML Yardımcıları ASP.NET MVC çerçeve ile birlikte açıklar.</span><span class="sxs-lookup"><span data-stu-id="2c485-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="2c485-112">Daha sonra, özel HTML Yardımcıları oluşturmanın iki yöntemini açıklıyorum: Paylaşılan bir yöntem oluşturarak ve bir uzantı yöntemi oluşturarak özel HTML Yardımcıları oluşturmanın nasıl yapılacağını açıklıyorum.</span><span class="sxs-lookup"><span data-stu-id="2c485-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="2c485-113">HTML Yardımcılarını Anlama</span><span class="sxs-lookup"><span data-stu-id="2c485-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="2c485-114">HTML Yardımcısı, dize döndüren bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="2c485-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="2c485-115">Dize istediğiniz herhangi bir içerik türünü temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="2c485-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="2c485-116">Örneğin, HTML `<input>` ve `<img>` etiketler gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="2c485-117">Sekme şeridi veya veritabanı verilerinin HTML tablosu gibi daha karmaşık içerik işlemek için HTML Yardımcıları'nı da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="2c485-118">ASP.NET MVC çerçevesi aşağıdaki standart HTML Yardımcıları kümesini içerir (bu tam bir liste değildir):</span><span class="sxs-lookup"><span data-stu-id="2c485-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="2c485-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="2c485-119">Html.ActionLink()</span></span>
- <span data-ttu-id="2c485-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="2c485-120">Html.BeginForm()</span></span>
- <span data-ttu-id="2c485-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="2c485-121">Html.CheckBox()</span></span>
- <span data-ttu-id="2c485-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="2c485-122">Html.DropDownList()</span></span>
- <span data-ttu-id="2c485-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="2c485-123">Html.EndForm()</span></span>
- <span data-ttu-id="2c485-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="2c485-124">Html.Hidden()</span></span>
- <span data-ttu-id="2c485-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="2c485-125">Html.ListBox()</span></span>
- <span data-ttu-id="2c485-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="2c485-126">Html.Password()</span></span>
- <span data-ttu-id="2c485-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="2c485-127">Html.RadioButton()</span></span>
- <span data-ttu-id="2c485-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="2c485-128">Html.TextArea()</span></span>
- <span data-ttu-id="2c485-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="2c485-129">Html.TextBox()</span></span>

<span data-ttu-id="2c485-130">Örneğin, Listeleme 1'deki formu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2c485-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="2c485-131">Bu form, standart HTML Yardımcılarından ikisinin yardımıyla işlenir (Bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="2c485-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="2c485-132">Bu form `Html.BeginForm()` ve `Html.TextBox()` Yardımcı yöntemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2c485-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="2c485-133">[![HTML Yardımcıları ile işlenen sayfa](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2c485-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="2c485-134">**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2c485-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="2c485-135">**İlan 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2c485-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="2c485-136">`Html.BeginForm()` Yardımcı yöntemi, HTML `<form>` etiketlerini açmak ve kapatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2c485-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="2c485-137">Yöntemin `Html.BeginForm()` bir using deyimi içinde çağrıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="2c485-138">Using deyimi, etiketin `<form>` kullanarak bloğun sonunda kapatılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c485-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="2c485-139">İsterseniz, bir kullanarak blok oluşturmak yerine, etiketi kapatmak için Html.EndForm() `<form>` Yardımcı yöntemini arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="2c485-140">Size en sezgisel görünen açılış `<form>` ve kapanış etiketini oluşturmak için hangi yaklaşımı kullanırsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c485-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="2c485-141">`Html.TextBox()` Yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için Listeleme 1'de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2c485-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="2c485-142">Tarayıcınızda görünüm kaynağını seçerseniz, Listeleme 2'deki HTML kaynağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2c485-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="2c485-143">Kaynağın standart HTML etiketleri içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c485-144">-HTML `Html.TextBox()`Yardımcısının `<%= %>` `<% %>` etiketler yerine etiketlerle işlendirilene dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="2c485-145">Eşit işareti eklemezseniz, tarayıcıya hiçbir şey işlenmez.</span><span class="sxs-lookup"><span data-stu-id="2c485-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="2c485-146">ASP.NET MVC çerçevesi küçük bir yardımcı kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="2c485-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="2c485-147">Büyük olasılıkla, özel HTML Yardımcıları ile MVC çerçevesini genişletmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c485-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="2c485-148">Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="2c485-149">**Listeleme 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="2c485-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="2c485-150">Paylaşılan Yöntemlerle HTML Yardımcıları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c485-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="2c485-151">Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren paylaşılan bir yöntem oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2c485-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="2c485-152">Örneğin, html `<label>` etiketi işleyen yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="2c485-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="2c485-153">Listeleme 2'deki sınıfı kullanarak `<label>`bir .</span><span class="sxs-lookup"><span data-stu-id="2c485-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="2c485-154">**Listeleme 2 –`Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="2c485-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="2c485-155">Listeleme 2'deki sınıfın özel bir özelliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="2c485-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="2c485-156">Yöntem `Label()` sadece bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="2c485-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="2c485-157">Listeleme 3'teki değiştirilmiş `LabelHelper` Dizin `<label>` görünümü, HTML etiketlerini işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2c485-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="2c485-158">Görünümün Application1.Helpers ad alanını içeri iten bir `<%@ imports %>` yönerge içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="2c485-159">**Listeleme 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2c485-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="2c485-160">Uzantı Yöntemleriyle HTML Yardımcıları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c485-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="2c485-161">ASP.NET MVC çerçevesine dahil edilen standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c485-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="2c485-162">Uzantı yöntemleri, varolan bir sınıfa yeni yöntemler eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2c485-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="2c485-163">BIR HTML Yardımcısı yöntemi oluştururken, görünümün `HtmlHelper` Html özelliğiyle temsil edilen sınıfa yeni yöntemler eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="2c485-164">Listeleme 3'teki Visual Basic `Label()` `HtmlHelper` modülü, sınıfa adlandırılmış bir uzantı yöntemi ekler.</span><span class="sxs-lookup"><span data-stu-id="2c485-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="2c485-165">Bu modül hakkında dikkat etmelisiniz birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="2c485-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="2c485-166">İlk olarak, modülün öznitelik `<Extension()>` ile dekore edilmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2c485-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="2c485-167">Bu özniteliği kullanmak `System.Runtime.CompilerServices` için, ad alanını almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="2c485-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="2c485-168">İkinci olarak, yöntemin ilk `Label()` parametresinin `HtmlHelper` sınıfı temsil ettiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="2c485-169">Uzantı yönteminin ilk parametresi, uzantı yönteminin genişletir sınıfını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2c485-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="2c485-170">**İlan 3 –`Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="2c485-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="2c485-171">Bir uzantı yöntemi oluşturduktan ve uygulamanızı başarıyla oluşturduktan sonra, uzantı yöntemi visual studio intellisense'de sınıfın diğer tüm yöntemleri gibi görünür (Bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="2c485-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="2c485-172">Tek fark, uzantı yöntemlerinin yanlarında özel bir sembolle (aşağı doğru bir ok simgesi) görünmesidir.</span><span class="sxs-lookup"><span data-stu-id="2c485-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="2c485-173">[![Html.Label() uzantı yöntemini kullanma](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="2c485-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="2c485-174">**Şekil 02**: Html.Label() uzantı yöntemini kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2c485-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="2c485-175">Listeleme 4'teki değiştirilmiş Dizin görünümü, tüm etiket &lt;&gt; etiketlerini işlemek için Html.Label() uzantı yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2c485-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="2c485-176">**İlan 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2c485-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="2c485-177">Özet</span><span class="sxs-lookup"><span data-stu-id="2c485-177">Summary</span></span>

<span data-ttu-id="2c485-178">Bu eğitimde, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="2c485-179">İlk olarak, bir dize `Label()` döndüren paylaşılan bir yöntem oluşturarak özel bir HTML Yardımcısı oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="2c485-180">Ardından, sınıfta bir uzantı `Label()` yöntemi oluşturarak özel bir HTML `HtmlHelper` Yardımcı yöntemi oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="2c485-181">Bu öğretici, ben son derece basit bir HTML Helper yöntemi bina üzerinde duruldu.</span><span class="sxs-lookup"><span data-stu-id="2c485-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="2c485-182">Bir HTML Yardımcısının istediğiniz kadar karmaşık olabileceğini fark edin.</span><span class="sxs-lookup"><span data-stu-id="2c485-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="2c485-183">Ağaç görünümleri, menüler veya veritabanı veri tabloları gibi zengin içerik oluşturan HTML Yardımcıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c485-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2c485-184">[Önceki](asp-net-mvc-views-overview-vb.md)
> [Sonraki](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2c485-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
