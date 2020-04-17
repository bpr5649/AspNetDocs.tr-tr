---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX Kontrol Araç Kiti Kontrolve Kontrol Genişleticileri Kullanma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET sayfalarınıza AJAX Control Toolkit denetimlerini ve genişleticileri nasıl ekleyeceğinizi öğrenin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 129d6841bc4db62ecbe5f26c4830d1ce2f199bff
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540018"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>AJAX Denetim Araç Seti Denetimlerini ve Denetim Genişleticilerini Kullanma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET sayfalarınıza AJAX Control Toolkit denetimlerini ve genişleticileri nasıl ekleyeceğinizi öğrenin.

AJAX Control Toolkit bir dizi kontrol ve kontrol genişletici içerir. Bu kısa öğreticide, ASP.NET sayfasına hem denetimhem de denetim genişleticileri eklemeyi öğrenirsiniz.

> [!NOTE] 
> 
> AJAX Control Toolkit'in yüklenmesi ve Visual Studio/Visual Web Developer araç kutusuna AJAX Control Toolkit'in eklenmesi yle ilgili talimatlar için, [ajax Control Toolkit ile başlayın](get-started-with-the-ajax-control-toolkit-vb.md)öğreticiye bakın.

## <a name="using-ajax-control-toolkit-controls"></a>AJAX Kontrol Araç Seti Kontrollerini Kullanma

Ajax Control Toolkit kontrolü normal bir ASP.NET kontrolü gibi çalışır. Denetimi araç kutusundan ASP.NET bir sayfaya sürükleyebilirsiniz. Denetimi sayfaya Tasarım görünümü veya Kaynak görünümünde ekleyebilirsiniz.

AJAX Control Toolkit'in kontrollerini kullanırken özel bir gereksinim vardır. Sayfa bir ScriptManager denetimi içermelidir. ScriptManager denetimi, AJAX Control Toolkit denetimleri tarafından gerekli olan tüm gerekli JavaScript'i de dahil etmekle yükümlüdür.

Örneğin, AJAX Denetim Araç Kiti sekmesi Düzenleyici denetimi adlı bir denetim içerir. Bu denetim zengin bir HTML düzenleyicisi görüntüler. Editör denetimini bir sayfaya eklemek için aşağıdaki adımları izleyin:

1. ShowEditor.aspx adlı yeni bir ASP.NET sayfası oluşturma
2. Araç kutusundaki AJAX Uzantıları sekmesinin altından ScriptManager denetimini seçin ve denetimi sayfaya sürükleyin.
3. Araç kutusundaki AJAX Control Toolkit sekmesinin altından Düzenleyici denetimini seçin ve denetimi sayfaya sürükleyin (Bkz. Şekil 1). Tasarımcı Şekil 2 gibi görünmelidir.
4. Menü seçeneğini seçerek web sitesini çalıştırın **Hata Ayıklama, Hata Ayıklamaya Başla** veya F5 tuşuna basarak.
5. Sayfayı Şekil 3'te görmelisiniz.

[![HTML Düzenleyici denetimini seçme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Şekil 01**: HTML Düzenleyicisi denetimini seçme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))

[![ScriptManager ve Edit denetimi ile Visual Studio Designer](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Şekil 02**: Visual Studio Designer ile ScriptManager ve Edit control[(Tam boyutlu görüntüyü görüntülemek için tıklayınız)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)

[![DisplayEditor.aspx sayfası](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Şekil 03**: DisplayEditor.aspx sayfası([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX Kontrol Araç Seti Kontrol Genişleticiler kullanma

AJAX Control Toolkit ayrıca kontrol genişleticiler içerir. Adından da anlaşılacağı gibi, bir denetim genişletici varolan bir denetimişlevselliğini genişletir. Örneğin, ConfirmButton denetim genişletici standart ASP.NET Düğme denetimini genişletir. Genişletici, Düğme denetiminin davranışını değiştirir, böylece Düğme'yi tıklattığınızda bir onay iletişim kutusu görüntüler.

Bir kontrol genişletici, bir AJAX Control Toolkit kontrolü gibi, bir ScriptManager denetimi gerektirir. Sayfadaki denetim genişleticilerini kullanmaya başlamadan önce bir sayfaya ScriptManager denetimi eklemeniz gerekir.

ConfirmButton denetim genişleticisini kullanmak için aşağıdaki adımları izleyin:

1. ShowConfirmButton.aspx adlı yeni bir ASP.NET sayfası oluşturma
2. Denetimi AJAX Uzantıları sekmesinin altından sayfaya sürükleyerek sayfaya bir ScriptManager denetimi ekleyin.
3. Düğmeyi araç kutusundaki Standart sekmesinin altından Tasarımcı yüzeyine sürükleyerek sayfaya standart bir Düğme denetimi ekleyin.
4. **Genişletici Ekle** görev seçeneğini tıklatın (Bkz. Şekil 4).
5. Genişletici'yi seç iletişim kutusunda, Onayla Düğme Genişletici'yi seçin (Şekil 5'e bakın) ve Tamam düğmesini tıklatın.
6. Tasarımcı'daki Düğme denetimini seçin ve Genişleticiler'i genişletin, Button1\_ConfirmButtonExtender düğümünü Özellikler penceresinde (Bkz. Şekil 6). Değeri *ConfirmText* özelliğine gerçekten atayın.
7. Menü seçeneğini seçerek sayfayı çalıştırın **Hata Ayıklama, Hata Ayıklama başlat** ın veya F5 tuşuna basın.

[![Genişletici Ekle görev seçeneği](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Şekil 04**: Genişletici Ekle görev seçeneği([Tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))

[![Onay düğmesi kontrol genişleticisini seçme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**Şekil 05**: ConfirmButton kontrol genişleticisini seçme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))

[![ConfirmButton özelliğini ayarlama](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Şekil 06**: ConfirmButton özelliğinin ayarlanması([Tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))

Sayfa açıldığında, bir düğme görmeniz gerekir. Düğmeyi tıklattığınızda, Şekil 7'deki onay iletişim kutusunu alırsınız.

[![Onay iletişim kutusunu görüntüleme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**Şekil 07**: Onay iletişim kutusunugörüntüleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))

Normalde bir denetim genişleticisini bir sayfaya sürüklemediğinize dikkat edin. Bunun yerine, sayfaya zaten eklediğiniz bir denetime genişletici eklemek için **Genişletici Ekle** görev seçeneğini kullanırsınız. Ayrıca, denetim inanış süresini uzatmak için özellik sayfasını açarak denetim genişletici özelliklerini ayarladığınıza dikkat edin.

Tek bir ASP.NET denetimi birden çok kontrol genişletici tarafından genişletilebilir. Genişletilmiş denetim için özellik sayfası, denetimle ilişkili tüm denetim genişleticilerini listeler.

> [!div class="step-by-step"]
> [Önceki](get-started-with-the-ajax-control-toolkit-vb.md)
> [Sonraki](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
