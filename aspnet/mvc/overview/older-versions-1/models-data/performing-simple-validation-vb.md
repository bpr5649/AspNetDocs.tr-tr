---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: Basit doğrulama (VB) gerçekleştirme | Microsoft Docs
author: StephenWalther
description: Bir ASP.NET MVC uygulamasındaki doğrulama gerçekleştirmeyi öğreneceksiniz. Bu öğreticide, model durumu ve doğrulama HTML Yardımcısı Stephen Walther sunar...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: c7a1b9e82defaae71f0a911e5e4321f6e15ad8bf
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422622"
---
# <a name="performing-simple-validation-vb"></a><span data-ttu-id="43864-104">Basit Doğrulama Gerçekleştirme (VB)</span><span class="sxs-lookup"><span data-stu-id="43864-104">Performing Simple Validation (VB)</span></span>

<span data-ttu-id="43864-105">tarafından [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="43864-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="43864-106">Bir ASP.NET MVC uygulamasındaki doğrulama gerçekleştirmeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="43864-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="43864-107">Bu öğreticide, model durumu ve doğrulama HTML Yardımcıları Stephen Walther tanıtır.</span><span class="sxs-lookup"><span data-stu-id="43864-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>


<span data-ttu-id="43864-108">Bu öğreticide bir ASP.NET MVC uygulaması içindeki doğrulama nasıl gerçekleştirebileceğiniz açıklamak için hedefidir.</span><span class="sxs-lookup"><span data-stu-id="43864-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="43864-109">Örneğin, birisi, gerekli bir alan için bir değer içermeyen bir form göndermesinin önlenmesine hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="43864-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="43864-110">Model durumu ve doğrulama HTML Yardımcıları kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="43864-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="43864-111">Model durumu anlama</span><span class="sxs-lookup"><span data-stu-id="43864-111">Understanding Model State</span></span>

<span data-ttu-id="43864-112">Doğrulama hataları temsil eden bir model durumu - veya daha doğru bir şekilde ve model durumu sözlüğündeki-'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="43864-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="43864-113">Örneğin, ürün sınıfı için bir veritabanı eklemeden önce bir ürün sınıf özelliklerini listeleme 1 Create() eylemi doğrular.</span><span class="sxs-lookup"><span data-stu-id="43864-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>


<span data-ttu-id="43864-114">Ben bir denetleyiciye doğrulama veya veritabanı mantığınızı eklemek öneren değil.</span><span class="sxs-lookup"><span data-stu-id="43864-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="43864-115">Bir denetleyici yalnızca mantık uygulaması akış denetimi ile ilgili içermelidir.</span><span class="sxs-lookup"><span data-stu-id="43864-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="43864-116">Örneği basit tutmak için bir kısayol sürüyor.</span><span class="sxs-lookup"><span data-stu-id="43864-116">We are taking a shortcut to keep things simple.</span></span>


**<span data-ttu-id="43864-117">Listing 1 - Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="43864-117">Listing 1 - Controllers\ProductController.vb</span></span>**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

<span data-ttu-id="43864-118">Listeleme 1'de ürün sınıfın adını, açıklamasını ve unitsInStock özelliklerini doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="43864-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="43864-119">Bu özelliklerin herhangi bir doğrulama testi başarısız olursa bir hata (denetleyici sınıfının ModelState özelliği tarafından gösterilen) model durumu sözlüğüne eklenir.</span><span class="sxs-lookup"><span data-stu-id="43864-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="43864-120">Model durumu hataları varsa ModelState.IsValid özelliği false döndürür.</span><span class="sxs-lookup"><span data-stu-id="43864-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="43864-121">HTML formu yeni bir ürün oluşturmaya yönelik bu durumda görünürler.</span><span class="sxs-lookup"><span data-stu-id="43864-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="43864-122">Aksi takdirde, doğrulama hatası varsa, yeni ürün veritabanına eklenir.</span><span class="sxs-lookup"><span data-stu-id="43864-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="43864-123">Doğrulama yardımcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="43864-123">Using the Validation Helpers</span></span>

<span data-ttu-id="43864-124">ASP.NET MVC çerçevesi iki doğrulama Yardımcıları içerir: Html.ValidationMessage() Yardımcısı ve Html.ValidationSummary() Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="43864-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="43864-125">Doğrulama hatası iletilerini görüntülemek için Görünümü'nde bu iki Yardımcıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="43864-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="43864-126">Html.ValidationMessage() ve Html.ValidationSummary() Yardımcıları, ASP.NET MVC yapı iskelesi tarafından otomatik olarak oluşturulan oluşturma ve düzenleme görünümlerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43864-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="43864-127">Oluştur görünümünün oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43864-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="43864-128">Menü seçeneği ürün denetleyicisi Create() eylemi sağ tıklayıp **Görünüm Ekle** (bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="43864-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="43864-129">İçinde **Görünüm Ekle** iletişim kutusunda etiketli onay **kesin türü belirtilmiş görünüm oluşturmak** (bkz: Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="43864-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="43864-130">Gelen **görüntülemek veri sınıfı** açılan listesinde, ürün sınıfı seçin.</span><span class="sxs-lookup"><span data-stu-id="43864-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="43864-131">Gelen **içeriği görüntüle** açılır listesi, select oluşturma.</span><span class="sxs-lookup"><span data-stu-id="43864-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="43864-132">**Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43864-132">Click the **Add** button.</span></span>


<span data-ttu-id="43864-133">Uygulamanızı bir görünüm eklemeden önce oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="43864-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="43864-134">Sınıf listesi Aksi takdirde görünmez **görüntülemek veri sınıfı** açılır liste.</span><span class="sxs-lookup"><span data-stu-id="43864-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>


[![T<span data-ttu-id="43864-135">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="43864-135">he New Project dialog box]</span></span>(performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

<span data-ttu-id="43864-136">**Şekil 01**: Görünüm ekleme ([tam boyutlu görüntüyü görmek için tıklatın](performing-simple-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="43864-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-vb/_static/image2.png))</span></span>


[![T<span data-ttu-id="43864-137">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="43864-137">he New Project dialog box]</span></span>(performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

<span data-ttu-id="43864-138">**Şekil 02**: Kesin türü belirtilmiş görünüm oluşturmak ([tam boyutlu görüntüyü görmek için tıklatın](performing-simple-validation-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="43864-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-vb/_static/image4.png))</span></span>


<span data-ttu-id="43864-139">Bu adımları tamamladıktan sonra Oluştur görünümünün listeleme 2'de sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="43864-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

**<span data-ttu-id="43864-140">Listing 2 - Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="43864-140">Listing 2 - Views\Product\Create.aspx</span></span>**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

<span data-ttu-id="43864-141">Listeleme 2'de Html.ValidationSummary() Yardımcısı hemen HTML form üzerinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="43864-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="43864-142">Bu yardımcı, doğrulama hata iletilerinin listesini görüntülemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43864-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="43864-143">Bir madde işaretli liste hataları Html.ValidationSummary() Yardımcısı işler.</span><span class="sxs-lookup"><span data-stu-id="43864-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="43864-144">Html.ValidationMessage() Yardımcısı her HTML form alanlarının yanındaki olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="43864-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="43864-145">Bu yardımcı, bir form alanının yanında şu hata iletisi görüntülemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43864-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="43864-146">Bir hata olduğunda listeleme 2 söz konusu olduğunda, bir yıldız işareti Html.ValidationMessage() Yardımcısı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="43864-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="43864-147">Şekil 3'te sayfanın eksik alanlar geçersiz değerler ile form gönderildiğinde, doğrulama Yardımcılar tarafından işlenen hata iletilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="43864-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>


[![T<span data-ttu-id="43864-148">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="43864-148">he New Project dialog box]</span></span>(performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

<span data-ttu-id="43864-149">**Şekil 03**: Oluştur görünümünün sorunları gönderilen ([tam boyutlu görüntüyü görmek için tıklatın](performing-simple-validation-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="43864-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-vb/_static/image6.png))</span></span>


<span data-ttu-id="43864-150">HTML görünümünü bir doğrulama hatası olduğunda alanlar da değiştirilmez giriş dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="43864-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="43864-151">Html.TextBox() yardımcı işleme bir *sınıfı "giriş doğrulama hata" =* Html.TextBox() Yardımcısı tarafından işlenen özelliği ilişkili doğrulama hatası olduğunda özniteliği.</span><span class="sxs-lookup"><span data-stu-id="43864-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="43864-152">Doğrulama hataları görünümünü kontrol etmek için kullanılan üç basamaklı stil sayfası sınıfları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="43864-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="43864-153">Giriş-doğrulama-hata - uygulanan &lt;giriş&gt; Html.TextBox() Yardımcısı tarafından işlenen etiketi.</span><span class="sxs-lookup"><span data-stu-id="43864-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="43864-154">alan-doğrulama-hata - uygulanan &lt;span&gt; Html.ValidationMessage() Yardımcısı tarafından işlenen etiketi.</span><span class="sxs-lookup"><span data-stu-id="43864-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="43864-155">Doğrulama-Özeti-hata - uygulanan &lt;ul&gt; Html.ValidationSummary() Yardımcısı tarafından işlenen etiketi.</span><span class="sxs-lookup"><span data-stu-id="43864-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSummary() helper.</span></span>

<span data-ttu-id="43864-156">Bu geçişli stil sayfası sınıfları değiştirebilir ve bu nedenle içerik klasöründe yer alan Site.css dosyasını değiştirerek doğrulama hatalarını görünümünü değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43864-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="43864-157">CSS ilgili doğrulama adları alınırken HtmlHelper sınıfı salt okunur statik özelliklerini içeren sınıflar.</span><span class="sxs-lookup"><span data-stu-id="43864-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="43864-158">Bu statik özellikleri ValidationInputCssClassName ValidationFieldCssClassName ve ValidationSummaryCssClassName adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="43864-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>


## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="43864-159">Doğrulama ve Postbinding doğrulama prebinding</span><span class="sxs-lookup"><span data-stu-id="43864-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="43864-160">Bir ürün oluşturmaya HTML formu göndermeden ve Fiyat alanının ve unitsInStock alan için hiçbir değer için geçersiz bir değer girin, Şekil 4'te görüntülenen doğrulama iletilerinin elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="43864-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="43864-161">Burada bu doğrulama hata iletileri gelir?</span><span class="sxs-lookup"><span data-stu-id="43864-161">Where do these validation error messages come from?</span></span>


[![T<span data-ttu-id="43864-162">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="43864-162">he New Project dialog box]</span></span>(performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

<span data-ttu-id="43864-163">**Şekil 04**: Doğrulama hataları prebinding ([tam boyutlu görüntüyü görmek için tıklatın](performing-simple-validation-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="43864-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-vb/_static/image8.png))</span></span>


<span data-ttu-id="43864-164">Doğrulama hata iletilerinin - HTML form alanlarını bir sınıfa bağlanır ve form alanlarını sınıfa bağlı sonra bu oluşturulan önce oluşturulanların aslında iki türü vardır.</span><span class="sxs-lookup"><span data-stu-id="43864-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="43864-165">Diğer bir deyişle, vardır prebinding doğrulama hatalarını ve postbinding doğrulama hataları.</span><span class="sxs-lookup"><span data-stu-id="43864-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="43864-166">Listeleme 1 ürün denetleyicisi tarafından kullanıma sunulan Create() eylem ürün sınıfının bir örneği kabul eder.</span><span class="sxs-lookup"><span data-stu-id="43864-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="43864-167">Oluşturma metodun imzası şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="43864-167">The signature of the Create method looks like this:</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

<span data-ttu-id="43864-168">HTML form alanlarını oluşturma formundaki değerlerini bir model bağlayıcı olarak adlandırılan bir şey tarafından productToCreate sınıfa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="43864-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="43864-169">Varsayılan model bağlayıcısını bir hata iletisi model durumuna bir form alanı için bir form özelliği bağlanamıyor olduğunda otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="43864-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="43864-170">Varsayılan model bağlayıcısını, ürün sınıfın fiyat özelliği için dize "apple" bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="43864-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="43864-171">Bir dize ondalık bir özelliğe atanamaz.</span><span class="sxs-lookup"><span data-stu-id="43864-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="43864-172">Bu nedenle, model bağlayıcı hata model durumuna ekler.</span><span class="sxs-lookup"><span data-stu-id="43864-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="43864-173">Varsayılan model bağlayıcısını de değer Nothing değeri hiçbir şey kabul etmeyen bir özelliğe atanamaz.</span><span class="sxs-lookup"><span data-stu-id="43864-173">The default model binder also cannot assign the value Nothing to a property that does not accept the value Nothing.</span></span> <span data-ttu-id="43864-174">Özellikle, model bağlayıcı değeri hiçbir şey unitsInStock özelliğine atama yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="43864-174">In particular, the model binder cannot assign the value Nothing to the UnitsInStock property.</span></span> <span data-ttu-id="43864-175">Bir kez daha, model bağlayıcı Vazgeçmeden ve bir hata iletisini model durumuna ekler.</span><span class="sxs-lookup"><span data-stu-id="43864-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="43864-176">Hata iletileri prebinding bu görünümünü özelleştirmek istiyorsanız, bu iletileri görmek için kaynak dizeleri oluşturmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="43864-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="43864-177">Özet</span><span class="sxs-lookup"><span data-stu-id="43864-177">Summary</span></span>

<span data-ttu-id="43864-178">ASP.NET MVC çerçevesi doğrulama temel mekanikleri açıklamak için bu öğreticinin amacı oluştu.</span><span class="sxs-lookup"><span data-stu-id="43864-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="43864-179">Model durumu ve doğrulama HTML Yardımcıları kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="43864-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="43864-180">Ayrıca prebinding ve doğrulama postbinding arasında ayrım ele almıştık.</span><span class="sxs-lookup"><span data-stu-id="43864-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="43864-181">Diğer öğreticileri, doğrulama kodunuzu denetleyicilerinizi ve model sınıflarınızı içine taşımak için çeşitli stratejileri açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="43864-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="43864-182">[Önceki](displaying-a-table-of-database-data-vb.md)
> [İleri](validating-with-the-idataerrorinfo-interface-vb.md)</span><span class="sxs-lookup"><span data-stu-id="43864-182">[Previous](displaying-a-table-of-database-data-vb.md)
[Next](validating-with-the-idataerrorinfo-interface-vb.md)</span></span>
