---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX Kontrol Araç Seti (VB) ile başlayın | Microsoft Dokümanlar
author: rick-anderson
description: AJAX Control Toolkit'i kullanmaya başlamak için bilmeniz gereken her şeyi öğrenin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543567"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="7c89e-103">AJAX Denetim Araç Seti ile Çalışmaya Başlama (VB)</span><span class="sxs-lookup"><span data-stu-id="7c89e-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="7c89e-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="7c89e-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7c89e-105">AJAX Control Toolkit'i kullanmaya başlamak için bilmeniz gereken her şeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="7c89e-106">AJAX Control Toolkit, ASP.NET uygulamalarınızda kullanabileceğiniz 30'dan fazla ücretsiz denetim içerir.</span><span class="sxs-lookup"><span data-stu-id="7c89e-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="7c89e-107">Bu eğitimde, AJAX Control Toolkit'i nasıl indirdiğinizi ve araç seti denetimlerini Visual Studio/Visual Web Developer Express araç kutunuza nasıl ekleyeceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7c89e-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="7c89e-108">AJAX Kontrol Araç Kiti'ni İndirme</span><span class="sxs-lookup"><span data-stu-id="7c89e-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="7c89e-109">[AJAX Control Toolkit,](http://devexpress.com/act) ASP.NET topluluğu üyeleri ve ASP.NET ekibi tarafından geliştirilen açık kaynak kodlu bir projedir.</span><span class="sxs-lookup"><span data-stu-id="7c89e-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="7c89e-110">[![AJAX Kontrol Araç Kiti'ni İndirme](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7c89e-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="7c89e-111">**Şekil 01**: AJAX Kontrol Araç Kiti'ni indirme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7c89e-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="7c89e-112">Dosyayı indirdikten sonra, dosyanın engelini kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c89e-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="7c89e-113">Dosyayı sağ tıklatın, Özellikler'i seçin ve **Engeli Kaldır** düğmesini tıklatın (Bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="7c89e-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="7c89e-114">[![AJAX Control Toolkit ZIP dosyasının engelini kaldırma](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7c89e-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="7c89e-115">**Şekil 02**: AJAX Control Toolkit ZIP dosyasının engelini kaldırma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7c89e-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="7c89e-116">Dosyanın engelini kaldırdıktan sonra dosyanın zipini kaldırabilirsiniz: Dosyayı sağ tıklatın ve **Tümünü Ayıkla** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="7c89e-117">Şimdi, Visual Studio / Görsel Web Geliştirici araç kutusuna araç eklemek için hazırız.</span><span class="sxs-lookup"><span data-stu-id="7c89e-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="7c89e-118">Ajax Control Toolkit'in Araç Kutusuna Eklenmesi</span><span class="sxs-lookup"><span data-stu-id="7c89e-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="7c89e-119">AJAX Control Toolkit'i kullanmanın en kolay yolu, araç kitini Visual Studio/Visual Web Developer araç kutunuza eklemektir (Bkz. Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="7c89e-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="7c89e-120">Bu şekilde, kullanmak istediğinizde bir araç seti denetimini bir sayfaya sürükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c89e-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="7c89e-121">[![AJAX Control Toolkit araç kutusunda görünür](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7c89e-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="7c89e-122">**Şekil 03**: AJAX Control Toolkit araç kutusunda görünür ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7c89e-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="7c89e-123">İlk olarak, araç kutusuna bir AJAX Control Toolkit sekmesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c89e-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="7c89e-124">Şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-124">Follow these steps.</span></span>

1. <span data-ttu-id="7c89e-125">Yeni Web Sitesi dosyası seçeneği Dosya'yı seçerek yeni bir ASP.NET Web Sitesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c89e-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="7c89e-126">Dosyayı düzenleyicide açmak için Solution Explorer penceresindevarsayılan.aspx'e çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c89e-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="7c89e-127">Genel Sekme'nin altındaki Araç Kutusu'na sağ tıklayın ve **Sekme Ekle** seçeneğini seçin (Bkz. Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="7c89e-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="7c89e-128">AJAX Control Toolkit adlı yeni bir sekme girin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="7c89e-129">[![Yeni bir sekme ekleme](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7c89e-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="7c89e-130">**Şekil 04**: Yeni bir sekme ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklatın](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7c89e-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="7c89e-131">Ardından, AJAX Control Toolkit denetimlerini yeni sekmeye eklemeniz gerekir. Aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7c89e-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="7c89e-132">AJAX Control Toolkit sekmesinin altına sağ tıklayın ve Menü seçeneğini seçin **Öğeleri Seçin (Bkz. Şekil 5).**</span><span class="sxs-lookup"><span data-stu-id="7c89e-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="7c89e-133">AJAX Control Toolkit'in fermuarını açtığınızda bulunduğunuz yere göz atın ve AjaxControlToolkit.dll montajını seçin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="7c89e-134">[![Araç kutusuna eklemek için öğeleri seçme](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7c89e-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="7c89e-135">**Şekil 05**: Araç kutusuna eklemek için öğeleri seçin ([Tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7c89e-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="7c89e-136">Bu adımları tamamladıktan sonra, tüm araç seti denetimleri araç kutunuzda görünür.</span><span class="sxs-lookup"><span data-stu-id="7c89e-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="7c89e-137">Toolkit'in Yeni Sürümüne Yükseltme</span><span class="sxs-lookup"><span data-stu-id="7c89e-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="7c89e-138">Toolkit'in eski bir sürümünü kullanıyorsanız ve şimdi daha sonraki bir sürüme geçmeniz gerekiyorsa önerilen adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7c89e-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="7c89e-139">İkili - Web sitenizbin klasöründen AjaxControlToolkit.dll derlemesinin eski sürümünü silin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="7c89e-140">Araç Kutusu Öğeleri - AJAX Control Toolkit sekmesini silin ve AjaxControlToolkit.dll derlemesinin yeni sürümüyle sekmeyi yeniden oluşturmak için yukarıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7c89e-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7c89e-141">[Önceki](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [Sonraki](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7c89e-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
