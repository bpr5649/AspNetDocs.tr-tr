---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Özel HTML Yardımcıları Oluşturma (C#) | Microsoft Dokümanlar
author: microsoft
description: Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Helper'dan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675337"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="c7f59-104">Özel HTML Yardımcıları Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="c7f59-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="c7f59-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="c7f59-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c7f59-106">PDF’yi İndir</span><span class="sxs-lookup"><span data-stu-id="c7f59-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="c7f59-107">Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="c7f59-108">HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="c7f59-109">Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="c7f59-110">HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="c7f59-111">Bu öğreticinin ilk bölümünde, bazı mevcut HTML Yardımcıları ASP.NET MVC çerçeve ile birlikte açıklar.</span><span class="sxs-lookup"><span data-stu-id="c7f59-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="c7f59-112">Daha sonra, özel HTML Yardımcıları oluşturmanın iki yöntemini açıklıyorum: Statik bir yöntem oluşturarak ve bir uzantı yöntemi oluşturarak özel HTML Yardımcıları oluşturmanın nasıl yapılacağını açıklıyorum.</span><span class="sxs-lookup"><span data-stu-id="c7f59-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="c7f59-113">HTML Yardımcılarını Anlama</span><span class="sxs-lookup"><span data-stu-id="c7f59-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="c7f59-114">HTML Yardımcısı, dize döndüren bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="c7f59-115">Dize istediğiniz herhangi bir içerik türünü temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="c7f59-116">Örneğin, HTML `<input>` ve `<img>` etiketler gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="c7f59-117">Sekme şeridi veya veritabanı verilerinin HTML tablosu gibi daha karmaşık içerik işlemek için HTML Yardımcıları'nı da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="c7f59-118">ASP.NET MVC çerçevesi aşağıdaki standart HTML Yardımcıları kümesini içerir (bu tam bir liste değildir):</span><span class="sxs-lookup"><span data-stu-id="c7f59-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="c7f59-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="c7f59-119">Html.ActionLink()</span></span>
- <span data-ttu-id="c7f59-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="c7f59-120">Html.BeginForm()</span></span>
- <span data-ttu-id="c7f59-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="c7f59-121">Html.CheckBox()</span></span>
- <span data-ttu-id="c7f59-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="c7f59-122">Html.DropDownList()</span></span>
- <span data-ttu-id="c7f59-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="c7f59-123">Html.EndForm()</span></span>
- <span data-ttu-id="c7f59-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="c7f59-124">Html.Hidden()</span></span>
- <span data-ttu-id="c7f59-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="c7f59-125">Html.ListBox()</span></span>
- <span data-ttu-id="c7f59-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="c7f59-126">Html.Password()</span></span>
- <span data-ttu-id="c7f59-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="c7f59-127">Html.RadioButton()</span></span>
- <span data-ttu-id="c7f59-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="c7f59-128">Html.TextArea()</span></span>
- <span data-ttu-id="c7f59-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="c7f59-129">Html.TextBox()</span></span>

<span data-ttu-id="c7f59-130">Örneğin, Listeleme 1'deki formu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c7f59-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="c7f59-131">Bu form, standart HTML Yardımcılarından ikisinin yardımıyla işlenir (Bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="c7f59-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="c7f59-132">Bu form, `Html.BeginForm()` `Html.TextBox()` basit bir HTML formu oluşturmak için Yardımcı ve Yardımcı yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="c7f59-133">[![HTML Yardımcıları ile işlenen sayfa](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7f59-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="c7f59-134">**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c7f59-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="c7f59-135">**İlan 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="c7f59-136">HTML.BeginForm() Yardımcı yöntemi, HTML `<form>` etiketlerini açmak ve kapatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="c7f59-137">Yöntemin `Html.BeginForm()` bir using deyimi içinde çağrıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c7f59-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="c7f59-138">Using deyimi, etiketin `<form>` kullanarak bloğun sonunda kapatılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7f59-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="c7f59-139">İsterseniz, bir kullanarak blok oluşturmak yerine, etiketi kapatmak için Html.EndForm() `<form>` Yardımcı yöntemini arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="c7f59-140">Size en sezgisel görünen açılış `<form>` ve kapanış etiketini oluşturmak için hangi yaklaşımı kullanırsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7f59-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="c7f59-141">`Html.TextBox()` Yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için Listeleme 1'de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="c7f59-142">Tarayıcınızda görünüm kaynağını seçerseniz, Listeleme 2'deki HTML kaynağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="c7f59-143">Kaynağın standart HTML etiketleri içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c7f59-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7f59-144">-HTML `Html.TextBox()`Yardımcısının `<%= %>` `<% %>` etiketler yerine etiketlerle işlendirilene dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c7f59-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="c7f59-145">Eşit işareti eklemezseniz, tarayıcıya hiçbir şey işlenmez.</span><span class="sxs-lookup"><span data-stu-id="c7f59-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="c7f59-146">ASP.NET MVC çerçevesi küçük bir yardımcı kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="c7f59-147">Büyük olasılıkla, özel HTML Yardımcıları ile MVC çerçevesini genişletmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="c7f59-148">Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="c7f59-149">**Listeleme 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="c7f59-150">Statik Yöntemlerle HTML Yardımcıları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7f59-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="c7f59-151">Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, dize döndüren statik bir yöntem oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="c7f59-152">Örneğin, html `<label>` etiketi işleyen yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="c7f59-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="c7f59-153">Listeleme 2'deki sınıfı kullanarak `<label>` bir .</span><span class="sxs-lookup"><span data-stu-id="c7f59-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="c7f59-154">**Listeleme 2 –`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="c7f59-155">Listeleme 2'deki sınıfın özel bir özelliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="c7f59-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="c7f59-156">Yöntem `Label()` sadece bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="c7f59-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="c7f59-157">Listeleme 3'teki değiştirilmiş `LabelHelper` Dizin `<label>` görünümü, HTML etiketlerini işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="c7f59-158">Görünümün ad alanını `<%@ imports %>` içeri iten bir yönerge içerdiğine dikkat edin. `Application1.Helpers`</span><span class="sxs-lookup"><span data-stu-id="c7f59-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="c7f59-159">**Listeleme 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="c7f59-160">Uzantı Yöntemleriyle HTML Yardımcıları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7f59-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="c7f59-161">ASP.NET MVC çerçevesine dahil edilen standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="c7f59-162">Uzantı yöntemleri, varolan bir sınıfa yeni yöntemler eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="c7f59-163">BIR HTML Yardımcı yöntemi oluştururken, görünümün Html özelliğiyle temsil edilen HtmlHelper sınıfına yeni yöntemler eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="c7f59-164">Listeleme 3'teki sınıf, adlı `HtmlHelper` `Label()`sınıfa bir uzantı yöntemi ekler.</span><span class="sxs-lookup"><span data-stu-id="c7f59-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="c7f59-165">Bu sınıf hakkında dikkat etmelisiniz birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="c7f59-166">İlk olarak, sınıfın statik bir sınıf olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c7f59-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="c7f59-167">Statik bir sınıfa sahip bir uzantı yöntemi tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="c7f59-168">İkinci olarak, yöntemin `Label()` ilk parametreanahtar kelimesi `this`önce olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c7f59-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="c7f59-169">Uzantı yönteminin ilk parametresi, uzantı yönteminin genişletir sınıfını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="c7f59-170">**İlan 3 –`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="c7f59-171">Bir uzantı yöntemi oluşturduktan ve uygulamanızı başarıyla oluşturduktan sonra, uzantı yöntemi visual studio intellisense'de sınıfın diğer tüm yöntemleri gibi görünür (Bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="c7f59-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="c7f59-172">Tek fark, uzantı yöntemlerinin yanlarında özel bir sembolle (aşağı doğru bir ok simgesi) görünmesidir.</span><span class="sxs-lookup"><span data-stu-id="c7f59-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="c7f59-173">[![Html.Label() uzantı yöntemini kullanma](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c7f59-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="c7f59-174">**Şekil 02**: Html.Label() uzantı yöntemini kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c7f59-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="c7f59-175">Listeleme 4'teki değiştirilmiş Dizin görünümü, tüm etiketlerini işlemek `<label>` için Html.Label() uzantı yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c7f59-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="c7f59-176">**İlan 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c7f59-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="c7f59-177">Özet</span><span class="sxs-lookup"><span data-stu-id="c7f59-177">Summary</span></span>

<span data-ttu-id="c7f59-178">Bu eğitimde, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="c7f59-179">İlk olarak, bir dize `Label()` döndüren statik bir yöntem oluşturarak özel bir HTML Yardımcısı oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="c7f59-180">Ardından, sınıfta bir uzantı `Label()` yöntemi oluşturarak özel bir HTML `HtmlHelper` Yardımcı yöntemi oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="c7f59-181">Bu öğretici, ben son derece basit bir HTML Helper yöntemi bina üzerinde duruldu.</span><span class="sxs-lookup"><span data-stu-id="c7f59-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="c7f59-182">Bir HTML Yardımcısının istediğiniz kadar karmaşık olabileceğini fark edin.</span><span class="sxs-lookup"><span data-stu-id="c7f59-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="c7f59-183">Ağaç görünümleri, menüler veya veritabanı veri tabloları gibi zengin içerik oluşturan HTML Yardımcıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f59-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7f59-184">[Önceki](asp-net-mvc-views-overview-cs.md)
> [Sonraki](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c7f59-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
