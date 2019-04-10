---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: (C#) Repeater'da ConfirmButton kullanma | Microsoft Docs
author: wenz
description: Evet, AJAX Denetim Araç Seti ConfirmButton genişletici oluşturur/Kullanıcı bir düğmeyi tıkladığında açılır penceresi (LinkButton denetim dahil). Yalnızca Evet ise...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ab979f220c06d22f51931c7c00fc4d273731f85
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59413951"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a><span data-ttu-id="ae89a-104">Repeater’da ConfirmButton Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="ae89a-104">Using a ConfirmButton In a Repeater (C#)</span></span>

<span data-ttu-id="ae89a-105">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ae89a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ae89a-106">[Kodu indir](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ae89a-106">[Download Code](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span></span>

> <span data-ttu-id="ae89a-107">Evet, AJAX Denetim Araç Seti ConfirmButton genişletici oluşturur/Kullanıcı bir düğmeyi tıkladığında açılır penceresi (LinkButton denetim dahil).</span><span class="sxs-lookup"><span data-stu-id="ae89a-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="ae89a-108">Yalnızca Evet tıklandığında, düğmenin eylemi, aksi takdirde iptal yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ae89a-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="ae89a-109">Bu aynı zamanda repeater'da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ae89a-109">This is also possible in a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="ae89a-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ae89a-110">Overview</span></span>

<span data-ttu-id="ae89a-111">Evet, AJAX Denetim Araç Seti ConfirmButton genişletici oluşturur/Kullanıcı bir düğmeyi tıkladığında açılır penceresi (LinkButton denetim dahil).</span><span class="sxs-lookup"><span data-stu-id="ae89a-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="ae89a-112">Yalnızca Evet tıklandığında, düğmenin eylemi, aksi takdirde iptal yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ae89a-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="ae89a-113">Bu aynı zamanda repeater'da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ae89a-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="ae89a-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="ae89a-114">Steps</span></span>

<span data-ttu-id="ae89a-115">İlk olarak bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ae89a-115">First of all, a data source is required.</span></span> <span data-ttu-id="ae89a-116">Bu örnekte, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="ae89a-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="ae89a-117">Veritabanı (express sürüm dahil) bir Visual Studio yüklemesi isteğe bağlı bir parçasıdır ve ayrıca altında ayrı bir indirme olarak kullanılabilir [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="ae89a-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="ae89a-118">AdventureWorks veritabanı SQL Server 2005 örnekleri ve örnek veritabanları parçasıdır (adresinden [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="ae89a-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="ae89a-119">En kolay yolu, veritabanını ayarlamak için Microsoft SQL Server Management Studio Express kullanmaktır ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) ve ekleme `AdventureWorks.mdf` veritabanı dosyası.</span><span class="sxs-lookup"><span data-stu-id="ae89a-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="ae89a-120">Bu örnek için SQL Server 2005 Express Edition örneğini çağrıldığından emin olan varsayıyoruz `SQLEXPRESS` ve web sunucusu; ile aynı makinede bulunan varsayılan kurulumu da budur.</span><span class="sxs-lookup"><span data-stu-id="ae89a-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="ae89a-121">Kurulumunuzu farklıysa, veritabanı için bağlantı bilgilerini uymak zorunda.</span><span class="sxs-lookup"><span data-stu-id="ae89a-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="ae89a-122">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="ae89a-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

<span data-ttu-id="ae89a-123">Ardından, bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ae89a-123">Then, a data source is required.</span></span> <span data-ttu-id="ae89a-124">Basitleştirmek amacıyla, yalnızca ilk beş girişleri satıcıları tablosunda AdventureWorks alınır.</span><span class="sxs-lookup"><span data-stu-id="ae89a-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="ae89a-125">Tablo adı veri kaynağını oluşturmak için Visual Studio Sihirbazı'nı kullanırken dikkat edin (`Vendors`) şu anda doğru ön ekine sahip değil `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="ae89a-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="ae89a-126">Aşağıdaki biçimlendirmede doğru olur:</span><span class="sxs-lookup"><span data-stu-id="ae89a-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

<span data-ttu-id="ae89a-127">Bu veri kaynağı, bir yineleyici içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ae89a-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="ae89a-128">Her zamanki şekilde `DataBinder.Eval()` yöntemi, veri kaynağından veri alır.</span><span class="sxs-lookup"><span data-stu-id="ae89a-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="ae89a-129">`ConfirmButtonExtender` Denetim sonra yerleştirilmelidir içinde `<ItemTemplate>` BT'nin veri kaynağındaki her giriş için görünmesi yineleyicinin bölümü.</span><span class="sxs-lookup"><span data-stu-id="ae89a-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]


[![T<span data-ttu-id="ae89a-130">He onaylayın düğmesinin yanındaki her girdi veri kaynağından]</span><span class="sxs-lookup"><span data-stu-id="ae89a-130">he confirm button appears next to each entry from the data source]</span></span>(using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

<span data-ttu-id="ae89a-131">Her giriş veri kaynağından yanında Onayla düğmesi görünür ([tam boyutlu görüntüyü görmek için tıklatın](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ae89a-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ae89a-132">Next</span><span class="sxs-lookup"><span data-stu-id="ae89a-132">Next</span></span>](using-a-confirmbutton-in-a-repeater-vb.md)
