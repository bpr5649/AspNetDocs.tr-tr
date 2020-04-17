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
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX Denetim Araç Seti ile Çalışmaya Başlama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> AJAX Control Toolkit'i kullanmaya başlamak için bilmeniz gereken her şeyi öğrenin.

AJAX Control Toolkit, ASP.NET uygulamalarınızda kullanabileceğiniz 30'dan fazla ücretsiz denetim içerir. Bu eğitimde, AJAX Control Toolkit'i nasıl indirdiğinizi ve araç seti denetimlerini Visual Studio/Visual Web Developer Express araç kutunuza nasıl ekleyeceğinizi öğreneceksiniz.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX Kontrol Araç Kiti'ni İndirme

[AJAX Control Toolkit,](http://devexpress.com/act) ASP.NET topluluğu üyeleri ve ASP.NET ekibi tarafından geliştirilen açık kaynak kodlu bir projedir.

[![AJAX Kontrol Araç Kiti'ni İndirme](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**Şekil 01**: AJAX Kontrol Araç Kiti'ni indirme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

Dosyayı indirdikten sonra, dosyanın engelini kaldırmanız gerekir. Dosyayı sağ tıklatın, Özellikler'i seçin ve **Engeli Kaldır** düğmesini tıklatın (Bkz. Şekil 2).

[![AJAX Control Toolkit ZIP dosyasının engelini kaldırma](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**Şekil 02**: AJAX Control Toolkit ZIP dosyasının engelini kaldırma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

Dosyanın engelini kaldırdıktan sonra dosyanın zipini kaldırabilirsiniz: Dosyayı sağ tıklatın ve **Tümünü Ayıkla** seçeneğini belirleyin. Şimdi, Visual Studio / Görsel Web Geliştirici araç kutusuna araç eklemek için hazırız.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Ajax Control Toolkit'in Araç Kutusuna Eklenmesi

AJAX Control Toolkit'i kullanmanın en kolay yolu, araç kitini Visual Studio/Visual Web Developer araç kutunuza eklemektir (Bkz. Şekil 3). Bu şekilde, kullanmak istediğinizde bir araç seti denetimini bir sayfaya sürükleyebilirsiniz.

[![AJAX Control Toolkit araç kutusunda görünür](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**Şekil 03**: AJAX Control Toolkit araç kutusunda görünür ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))

İlk olarak, araç kutusuna bir AJAX Control Toolkit sekmesi eklemeniz gerekir. Şu adımları izleyin.

1. Yeni Web Sitesi dosyası seçeneği Dosya'yı seçerek yeni bir ASP.NET Web Sitesi oluşturun. Dosyayı düzenleyicide açmak için Solution Explorer penceresindevarsayılan.aspx'e çift tıklayın.
2. Genel Sekme'nin altındaki Araç Kutusu'na sağ tıklayın ve **Sekme Ekle** seçeneğini seçin (Bkz. Şekil 4).
3. AJAX Control Toolkit adlı yeni bir sekme girin.

[![Yeni bir sekme ekleme](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**Şekil 04**: Yeni bir sekme ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklatın](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

Ardından, AJAX Control Toolkit denetimlerini yeni sekmeye eklemeniz gerekir. Aşağıdaki adımları izleyin:

- AJAX Control Toolkit sekmesinin altına sağ tıklayın ve Menü seçeneğini seçin **Öğeleri Seçin (Bkz. Şekil 5).**
- AJAX Control Toolkit'in fermuarını açtığınızda bulunduğunuz yere göz atın ve AjaxControlToolkit.dll montajını seçin.

[![Araç kutusuna eklemek için öğeleri seçme](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**Şekil 05**: Araç kutusuna eklemek için öğeleri seçin ([Tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

Bu adımları tamamladıktan sonra, tüm araç seti denetimleri araç kutunuzda görünür.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Toolkit'in Yeni Sürümüne Yükseltme

Toolkit'in eski bir sürümünü kullanıyorsanız ve şimdi daha sonraki bir sürüme geçmeniz gerekiyorsa önerilen adımlar şunlardır:

- İkili - Web sitenizbin klasöründen AjaxControlToolkit.dll derlemesinin eski sürümünü silin.
- Araç Kutusu Öğeleri - AJAX Control Toolkit sekmesini silin ve AjaxControlToolkit.dll derlemesinin yeni sürümüyle sekmeyi yeniden oluşturmak için yukarıdaki adımları izleyin.

> [!div class="step-by-step"]
> [Önceki](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [Sonraki](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
