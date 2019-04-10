---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: (VB) bir Accordion'a veri bağlama | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir. Paneller genellikle w bildirilen...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: dde3d60f82bb5f32fdd8b6b5cf8a0e1accebd1a7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408933"
---
# <a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="6ca74-104">Bir Accordion’a Veri Bağlama (VB)</span><span class="sxs-lookup"><span data-stu-id="6ca74-104">Databinding to an Accordion (VB)</span></span>

<span data-ttu-id="6ca74-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6ca74-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6ca74-106">[Kodu indir](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6ca74-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="6ca74-107">AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir.</span><span class="sxs-lookup"><span data-stu-id="6ca74-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6ca74-108">Paneller genellikle sayfa içinde bildirilen, ancak bir veri kaynağına bağlama daha fazla esneklik sunar.</span><span class="sxs-lookup"><span data-stu-id="6ca74-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="6ca74-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6ca74-109">Overview</span></span>

<span data-ttu-id="6ca74-110">AJAX Denetim Araç Seti Accordion denetimi birden fazla bölme sağlar ve bunlardan biri aynı anda görüntüleme izin verir.</span><span class="sxs-lookup"><span data-stu-id="6ca74-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6ca74-111">Paneller genellikle sayfa içinde bildirilen, ancak bir veri kaynağına bağlama daha fazla esneklik sunar.</span><span class="sxs-lookup"><span data-stu-id="6ca74-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="6ca74-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="6ca74-112">Steps</span></span>

<span data-ttu-id="6ca74-113">İlk olarak bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6ca74-113">First of all, a data source is required.</span></span> <span data-ttu-id="6ca74-114">Bu örnekte, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ca74-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6ca74-115">Veritabanı (express sürüm dahil) bir Visual Studio yüklemesi isteğe bağlı bir parçasıdır ve ayrıca altında ayrı bir indirme olarak kullanılabilir [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="6ca74-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6ca74-116">AdventureWorks veritabanı SQL Server 2005 örnekleri ve örnek veritabanları parçasıdır (adresinden [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="6ca74-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6ca74-117">En kolay yolu, veritabanını ayarlamak için Microsoft SQL Server Management Studio Express kullanmaktır ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) ve ekleme `AdventureWorks.mdf` veritabanı dosyası.</span><span class="sxs-lookup"><span data-stu-id="6ca74-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6ca74-118">Bu örnek için SQL Server 2005 Express Edition örneğini çağrıldığından emin olan varsayıyoruz `SQLEXPRESS` ve web sunucusu; ile aynı makinede bulunan varsayılan kurulumu da budur.</span><span class="sxs-lookup"><span data-stu-id="6ca74-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6ca74-119">Kurulumunuzu farklıysa, veritabanı için bağlantı bilgilerini uymak zorunda.</span><span class="sxs-lookup"><span data-stu-id="6ca74-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6ca74-120">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="6ca74-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="6ca74-121">Ardından, bir veri kaynağı sayfasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ca74-121">Then, add a data source to the page.</span></span> <span data-ttu-id="6ca74-122">Sınırlı miktarda veri kullanmak için yalnızca ilk beş girişleri AdventureWorks veritabanını Satıcı tablosunda seçiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ca74-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="6ca74-123">Veri kaynağı oluşturmak için Visual Studio Yardımcısı'nı kullanıyorsanız, güncel sürümdeki bir hatayı tablo adı öneki değil gerektiğini unutmayın (`Vendor`) ile `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="6ca74-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="6ca74-124">Aşağıdaki biçimlendirmede doğru sözdizimini gösterir:</span><span class="sxs-lookup"><span data-stu-id="6ca74-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="6ca74-125">Veri kaynağı adı (ID) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6ca74-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="6ca74-126">Bu çok kimliği daha sonra kullanılmalıdır `DataSourceID` Accordion denetimi özelliği:</span><span class="sxs-lookup"><span data-stu-id="6ca74-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="6ca74-127">Accordion denetimi içinde denetimi üst bilgisi dahil olmak üzere çeşitli bölümlerini şablonları sağlayabilirsiniz (`<HeaderTemplate>`) ve içeriği (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="6ca74-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="6ca74-128">Bu öğeleri içinde yalnızca veri verileri çıktı kullanarak kaynak `DataBinder.Eval()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="6ca74-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="6ca74-129">Sayfa yüklendiğinde, bu sunucu tarafı kodu ile bir accordion'a veri kaynağı bağlı olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6ca74-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="6ca74-130">Bu örnek sonuçlandırmak için başvurulan iki CSS sınıfları Accordion denetimi tanımlamanız gerekir (özelliklerinde `HeaderCssClass` ve `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="6ca74-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="6ca74-131">Aşağıdaki biçimlendirmede koymak `<head>` sayfasının bölümünde:</span><span class="sxs-lookup"><span data-stu-id="6ca74-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]


[![T<span data-ttu-id="6ca74-132">He accordion verileri doğrudan veri kaynağından gelen]</span><span class="sxs-lookup"><span data-stu-id="6ca74-132">he data in the accordion comes directly from the data source]</span></span>(databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

<span data-ttu-id="6ca74-133">Accordion verileri doğrudan veri kaynağından gelir ([tam boyutlu görüntüyü görmek için tıklatın](databinding-to-an-accordion-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6ca74-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6ca74-134">[Önceki](dynamically-adding-an-accordion-pane-cs.md)
> [İleri](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6ca74-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
