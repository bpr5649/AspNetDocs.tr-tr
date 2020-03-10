---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: '3\. kısım: düzen ve kategori menüsü | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 3\. bölüm, düzen ve kategori menüsü eklemeyi içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639120"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="97a14-104">3\. Bölüm: Düzen ve Kategori Menüsü</span><span class="sxs-lookup"><span data-stu-id="97a14-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="97a14-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="97a14-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="97a14-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a14-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="97a14-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a14-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="97a14-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="97a14-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="97a14-109">3\. bölüm, düzen ve kategori menüsü eklemeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="97a14-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="97a14-110">Bazı düzen ve kategori menüsü ekleme</span><span class="sxs-lookup"><span data-stu-id="97a14-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="97a14-111">Site ana sayfamızda, sol taraftaki sütun için, ürün kategorisi menüsünü içerecek bir div ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="97a14-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="97a14-112">İstenen hizalama ve diğer biçimlendirmeler Style. css dosyanıza eklediğimiz CSS sınıfı tarafından sağlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="97a14-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="97a14-113">Ürün kategorisi menüsü, mevcut ürün kategorileri için ticaret veritabanını sorgulayarak ve menü öğeleri ve karşılık gelen bağlantılar oluşturarak çalışma zamanında dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="97a14-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="97a14-114">Bunu gerçekleştirmek için, iki ASP. NET ' in güçlü veri denetimleri.</span><span class="sxs-lookup"><span data-stu-id="97a14-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="97a14-115">"Varlık veri kaynağı" denetimi ve "ListView" denetimi.</span><span class="sxs-lookup"><span data-stu-id="97a14-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="97a14-116">"Tasarım görünümüne" geçelim ve denetimlerinizi yapılandırmak için yardımcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a14-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="97a14-117">EntityDataSource ID özelliğini EDS\_category\_Menu olarak ayarlayalim ve "veri kaynağını Yapılandır" seçeneğine tıklaalım.</span><span class="sxs-lookup"><span data-stu-id="97a14-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="97a14-118">Ticaret veritabanımız için varlık veri kaynağı modelini oluşturduğumuzda ve "Ileri" ye tıkladığımızda bizim için oluşturulan CommerceEntities bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="97a14-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="97a14-119">"Kategoriler" varlık kümesi adını seçin ve diğer seçenekleri varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="97a14-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="97a14-120">"Son" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97a14-120">Click "Finish".</span></span>

<span data-ttu-id="97a14-121">Şimdi sayfamıza yerleştirdiğimiz ListView denetim örneğinin ID özelliğini bir ListView\_ProductsMenu olarak ayarlayalım ve yardımcı ' i etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="97a14-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="97a14-122">Veri öğesi görüntüleme ve biçimlendirmesini biçimlendirmek için denetim seçeneklerini kullanabiliriz; ancak, bu kodu kaynak görünümüne girebilmemiz için menü oluşturma yalnızca basit biçimlendirme gerektireceğiz.</span><span class="sxs-lookup"><span data-stu-id="97a14-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="97a14-123">Lütfen "eval" ekstresini unutmayın: &lt;% # eval ("CategoryName")%&gt;</span><span class="sxs-lookup"><span data-stu-id="97a14-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="97a14-124">ASP.NET sözdizimi &lt;% #%&gt;, çalışma zamanının içinde yer aldığı her şeyi yürütmesini ve sonuçları "satır" olarak çıktısını veren bir toplu kuraldır.</span><span class="sxs-lookup"><span data-stu-id="97a14-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="97a14-125">İfade eval ("CategoryName"), veri öğelerinin bağlantılı koleksiyonundaki geçerli giriş için "CategoryName" varlık modeli öğe adlarının değerini getiren bildirir.</span><span class="sxs-lookup"><span data-stu-id="97a14-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="97a14-126">Bu, çok güçlü bir özellik için kısa bir sözdizimidir.</span><span class="sxs-lookup"><span data-stu-id="97a14-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="97a14-127">Uygulamayı şimdi çalıştırmaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="97a14-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="97a14-128">Ürün kategorisi menümüzün görüntülendiğini ve kategori menü öğelerinden birinin üzerine geldiğinizde, menü öğesi bağlantı noktalarını yalnızca adlandırılmış ProductsList. aspx ' i uygulamamız ve bir dinamik sorgu dizesi bağımsız değişkeni (  kategori kimliği.</span><span class="sxs-lookup"><span data-stu-id="97a14-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="97a14-129">[Önceki](tailspin-spyworks-part-2.md)
> [İleri](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="97a14-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
