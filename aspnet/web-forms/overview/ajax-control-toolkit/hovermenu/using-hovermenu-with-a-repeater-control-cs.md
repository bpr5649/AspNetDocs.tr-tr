---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: (C#) Repeater denetimiyle HoverMenu kullanma | Microsoft Docs
author: wenz
description: 'AJAX Denetim Araç Seti HoverMenu denetiminde basit açılan etkisi sağlar: Fare işaretçisini bir öğenin geldiğinde bir specifi açılır pencere görünür...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 33f65a132ea9f0a939ab70ac249b397ea883ac8c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068328"
---
<a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="0689e-103">Repeater Denetimiyle HoverMenu Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="0689e-103">Using HoverMenu with a Repeater Control (C#)</span></span>
====================
<span data-ttu-id="0689e-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0689e-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0689e-105">[Kodu indir](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0689e-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="0689e-106">AJAX Denetim Araç Seti HoverMenu denetiminde basit açılan etkisi sağlar: Fare işaretçisini bir öğenin geldiğinde, belirtilen konumda bir açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="0689e-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="0689e-107">Repeater'da içindeki bu denetimi kullanmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0689e-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="0689e-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0689e-108">Overview</span></span>

<span data-ttu-id="0689e-109">`HoverMenu` AJAX Denetim Araç Seti denetiminde basit açılan etkisi sağlar: Fare işaretçisini bir öğenin geldiğinde, belirtilen konumda bir açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="0689e-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="0689e-110">Repeater'da içindeki bu denetimi kullanmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0689e-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="0689e-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="0689e-111">Steps</span></span>

<span data-ttu-id="0689e-112">İlk olarak bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0689e-112">First of all, a data source is required.</span></span> <span data-ttu-id="0689e-113">Bu örnekte, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="0689e-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="0689e-114">Veritabanı (express sürüm dahil) bir Visual Studio yüklemesi isteğe bağlı bir parçasıdır ve ayrıca altında ayrı bir indirme olarak kullanılabilir [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="0689e-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="0689e-115">AdventureWorks veritabanı SQL Server 2005 örnekleri ve örnek veritabanları parçasıdır (adresinden [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="0689e-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="0689e-116">En kolay yolu, veritabanını ayarlamak için Microsoft SQL Server Management Studio Express kullanmaktır ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) ve ekleme `AdventureWorks.mdf` veritabanı dosyası.</span><span class="sxs-lookup"><span data-stu-id="0689e-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="0689e-117">Bu örnek için SQL Server 2005 Express Edition örneğini çağrıldığından emin olan varsayıyoruz `SQLEXPRESS` ve web sunucusu; ile aynı makinede bulunan varsayılan kurulumu da budur.</span><span class="sxs-lookup"><span data-stu-id="0689e-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="0689e-118">Kurulumunuzu farklıysa, veritabanı için bağlantı bilgilerini uymak zorunda.</span><span class="sxs-lookup"><span data-stu-id="0689e-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="0689e-119">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="0689e-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="0689e-120">Ardından, bir veri kaynağı sayfasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0689e-120">Then, add a data source to the page.</span></span> <span data-ttu-id="0689e-121">Sınırlı miktarda veri kullanmak için yalnızca ilk beş girişleri AdventureWorks veritabanını Satıcı tablosunda seçiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0689e-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="0689e-122">Veri kaynağı oluşturmak için Visual Studio Yardımcısı'nı kullanıyorsanız, güncel sürümdeki bir hatayı tablo adı öneki değil gerektiğini unutmayın (`Vendor`) ile `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="0689e-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="0689e-123">Aşağıdaki biçimlendirmede doğru sözdizimini gösterir:</span><span class="sxs-lookup"><span data-stu-id="0689e-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="0689e-124">Ardından, kalıcı açılan hizmet veren bir panel ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0689e-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="0689e-125">Şimdi, `HoverMenuExtender` dönüştürülerek.</span><span class="sxs-lookup"><span data-stu-id="0689e-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="0689e-126">Veri kaynağındaki her öğenin kendi açılan alır, böylece yineleyici içinde 's genişletici yerleştirmeniz gerekir `<ItemTemplate>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="0689e-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="0689e-127">Biçimlendirme şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0689e-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="0689e-128">Veri kaynağındaki her öğe sağ tarafta açılır pencere görüntüler artık (`PopupPosition` özniteliği) bir gecikme 50 milisaniye sonra (`PopDelay` özniteliği).</span><span class="sxs-lookup"><span data-stu-id="0689e-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="0689e-129">[![Yineleyicideki her öğenin yanında vurgulu menüsünde görünür](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0689e-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="0689e-130">Yineleyicideki her bir öğenin üzerine gelindiğinde kullanılacak menüsünün yanında ([tam boyutlu görüntüyü görmek için tıklatın](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0689e-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0689e-131">Next</span><span class="sxs-lookup"><span data-stu-id="0689e-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
