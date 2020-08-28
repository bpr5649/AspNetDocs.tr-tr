---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX denetim araç seti denetimlerini ve denetim Genişleticilerini kullanma (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET sayfalarınıza AJAX denetim araç seti denetimleri ve Extender 'ların nasıl ekleneceğini öğrenin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 416ee0d4931a3850c1e9bb4ba28db43f5e1647bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044369"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>AJAX Denetim Araç Seti Denetimlerini ve Denetim Genişleticilerini Kullanma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET sayfalarınıza AJAX denetim araç seti denetimleri ve Extender 'ların nasıl ekleneceğini öğrenin.

AJAX denetim araç seti bir denetimler kümesi ve denetim Genişleticileri içerir. Bu kısa öğreticide, bir ASP.NET sayfasına hem denetimleri hem de denetim Genişleticilerini nasıl ekleyeceğinizi öğreneceksiniz.

> [!NOTE] 
> 
> AJAX denetim araç setini yükleme ve AJAX denetim araç setini Visual Studio/Visual Web Developer araç kutusu 'na ekleme hakkında yönergeler için bkz. [AJAX denetim araç seti Ile çalışmaya başlama](get-started-with-the-ajax-control-toolkit-vb.md)öğreticisi.

## <a name="using-ajax-control-toolkit-controls"></a>AJAX denetim araç seti denetimlerini kullanma

AJAX denetim araç seti denetimi normal bir ASP.NET denetimi gibi çalışmaktadır. Denetimi araç kutusundan bir ASP.NET sayfasına sürükleyebilirsiniz. Denetimi sayfaya Tasarım görünümü veya kaynak görünümünde ekleyebilirsiniz.

AJAX denetim araç setinde denetimleri kullanırken bir özel gereksinim vardır. Sayfa bir ScriptManager denetimi içermelidir. ScriptManager Denetim araç seti denetimleri için gerekli tüm JavaScript 'ı dahil etmek için ScriptManager denetimi sorumludur.

Örneğin, AJAX denetim araç seti sekmesi, düzenleyici denetimi adında bir denetim içerir. Bu denetim zengin bir HTML Düzenleyicisi görüntüler. Bir sayfaya düzenleyici denetimi eklemek için aşağıdaki adımları izleyin:

1. Showweditor. aspx adlı yeni bir ASP.NET sayfası oluşturun
2. Araç kutusundaki AJAX Uzantıları sekmesinin altında bulunan ScriptManager denetimini seçin ve denetimi sayfaya sürükleyin.
3. Araç kutusundaki AJAX denetim araç seti sekmesinin altındaki düzenleyici denetimini seçin ve denetimi sayfaya sürükleyin (bkz. Şekil 1). Tasarımcı Şekil 2 gibi görünmelidir.
4. Web sitesini **Hata Ayıkla, hata ayıklamayı Başlat** veya F5 tuşuna basarak menü seçeneğini belirleyerek çalıştırın.
5. Şekil 3 ' te sayfayı görmeniz gerekir.

[![HTML düzenleyici denetimini seçme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Şekil 01**: HTML düzenleyici denetimini seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))

[![ScriptManager ve düzenleme denetimiyle Visual Studio Tasarımcısı](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Şekil 02**: ScriptManager Ile Visual Studio Tasarımcısı ve düzenleme denetimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))

[![DisplayEditor. aspx sayfası](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Şekil 03**: displayeditor. aspx sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX denetim araç seti denetim Genişleticilerini kullanma

AJAX denetim araç seti ayrıca denetim Genişleticilerini içerir. Adından da anlaşılacağı gibi, bir denetim genişletici var olan bir denetimin işlevselliğini genişletir. Örneğin, ConfirmButton denetim genişletici standart ASP.NET düğme denetimini genişletir. Genişletici düğme denetiminin davranışını değiştirir, böylece düğme, düğmesine tıkladığınızda bir onay iletişim kutusu görüntüler.

AJAX denetim araç seti denetiminde olduğu gibi bir denetim Genişleticisi, ScriptManager denetimi gerektirir. Sayfada denetim Genişleticilerini kullanmaya başlamadan önce sayfaya bir ScriptManager denetimi eklemeniz gerekir.

ConfirmButton denetim genişletici 'i kullanmak için şu adımları izleyin:

1. ShowConfirmButton. aspx adlı yeni bir ASP.NET sayfası oluşturun
2. Denetimi, AJAX Uzantıları sekmesinin altındaki sayfaya sürükleyerek sayfaya bir ScriptManager denetimi ekleyin.
3. Araç kutusundaki Standart Sekmenin altındaki düğmeyi tasarımcı yüzeyine sürükleyerek sayfaya standart düğme denetimi ekleyin.
4. Genişletici görevi **Ekle** seçeneğine tıklayın (bkz. Şekil 4).
5. Genişletici Seç iletişim kutusunda ConfirmButtonExtender (Şekil 5 ' e bakın) öğesini seçin ve Tamam düğmesine tıklayın.
6. Tasarımcıda düğme denetimini seçin ve Özellikler penceresi genişleticiler, Button1 \_ ConfirmButtonExtender düğümünü genişletin (bkz. Şekil 6). *' Gerçekten? '* değerini ata ConfirmText özelliğine.
7. **Hata Ayıkla, hata ayıklamayı Başlat** veya F5 tuşuna basın menü seçeneğini belirleyerek sayfayı çalıştırın.

[![Genişletici görevi Ekle seçeneği](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Şekil 04**: Genişletici görevi Ekle seçeneği ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))

[![ConfirmButton denetim genişletici 'i seçme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**Şekil 05**: ConfirmButton Control genişletici seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))

[![ConfirmButton özelliğini ayarlama](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Şekil 06**: ConfirmButton özelliğini ayarlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))

Sayfa açıldığında bir düğme görmeniz gerekir. Düğmeye tıkladığınızda, Şekil 7 ' de onay iletişim kutusunu alırsınız.

[![Onay iletişim kutusunu görüntüleme](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**Şekil 07**: onay iletişim kutusunu görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))

Normalde bir denetim genişleticisini bir sayfaya sürükleytiğine dikkat edin. Bunun yerine, bir sayfaya daha önce eklediğiniz bir denetime genişletici eklemek için **genişletici görevi Ekle** seçeneğini kullanın. Ayrıca, denetim Genişletici özelliklerini genişletmekte olan denetimin özellik sayfasını açarak ayarlayabildiğinize de dikkat edin.

Tek bir ASP.NET denetimi, birden çok denetim Genişleticileri tarafından genişletilebilir. Genişletilmekte olan denetimin özellik sayfası denetimle ilişkili tüm denetim Genişleticilerini listeler.

> [!div class="step-by-step"]
> [Önceki](get-started-with-the-ajax-control-toolkit-vb.md) 
>  [Sonraki](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
