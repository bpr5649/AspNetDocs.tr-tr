---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: ColorPicker Control Extender (C#) kullanma | Microsoft Dokümanlar
author: rick-anderson
description: ColorPicker bir pop-up kontrolünde Kullanıcı Arası ile istemci tarafı renk toplama işlevselliği sağlayan bir ASP.NET AJAX genişleticidir. Herhangi bir ASP.NET bağlı olabilir ...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 63b6bc58d36fdfcb5ee0a1c97988091e8d35505b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543138"
---
# <a name="using-the-colorpicker-control-extender-c"></a>ColorPicker Kontrol Genişletici (C#) kullanma

[Microsoft](https://github.com/microsoft) tarafından

> ColorPicker bir pop-up kontrolünde Kullanıcı Arası ile istemci tarafı renk toplama işlevselliği sağlayan bir ASP.NET AJAX genişleticidir. Herhangi bir ASP.NET TextBox denetimine eklenebilir. Bu kadar.

Bu öğreticinin amacı, AJAX Control Toolkit ColorPicker kontrol genişleticisini nasıl kullanabileceğinizi açıklamaktır. ColorPicker denetim genişletici, bir renk seçmenize olanak tanıyan bir açılır pencere iletişim kutusu görüntüler. ColorPicker bir kullanıcı için bir renk seçmek için sezgisel bir kullanıcı arayüzü sağlamak istediğinizde yararlıdır.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker Control Extender ile TextBox Denetimini Genişletme

Örneğin, ziyaretçilerin özelleştirilmiş kartvizitler oluşturmasına olanak tanıyan bir web sitesi oluşturmak istediğinizi düşünün. Ziyaretçiler kartvizit için metni girebilir ve rengi seçebilir. Listeleme 1'deki ASP.NET sayfası, txtCardText ve txtCardColor adlı iki TextBox denetimi içerir. Formu gönderdiğiniz zaman, seçili değerler görüntülenir (Bkz. Şekil 1).

[![Kartvizit oluşturmak için basit form](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**Şekil 01**: Kartvizit oluşturmak için basit form ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-the-colorpicker-control-extender-cs/_static/image2.png))

**Listeleme 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

Listeleme 1'deki form çalışır, ancak harika bir kullanıcı deneyimi sağlamaz. Kullanıcımetin kutusuna bir renk yazmak zorundadır. Kullanıcı özel bir renk istiyorsa - örneğin, bezelye yeşilsadece sağ gölge - o zaman kullanıcı herhangi bir yardım olmadan HTML renk kodu anlamaya gerekir.

Daha iyi bir kullanıcı deneyimi oluşturmak için ColorPicker kontrol genişleticisini kullanabilirsiniz. ColorPicker, odağı TextBox denetimine taşıdığınızda bir renk iletişim kutusu görüntüler (Bkz. Şekil 2).

[![ColorPicker Kontrol Genişletici](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**Şekil 02**: ColorPicker Kontrol Genişletici ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-the-colorpicker-control-extender-cs/_static/image4.png))

ColorPicker kontrol genişleticisini Listeleme 1'deki formla kullanmak için iki adımı tamamlamanız gerekir:

1. Sayfaya ScriptManager denetimi ekleme
2. ColorPicker kontrol genişleticisini sayfaya ekleme

ColorPicker'ı kullanabilmek için önce sayfanıza bir ScriptManager eklemeniz gerekir. ScriptManager eklemek için iyi bir yer sağ açılış &lt;&gt; sunucu tarafı form etiketi altındadır. ScriptManager'ı araç kutusundan sayfaya sürükleyebilirsiniz (ScriptManager AJAX Uzantıları sekmesinin altında yer alır). Alternatif olarak, sunucu tarafındaki form etiketinin altındaki Kaynak Görünümü'ne aşağıdaki etiketi yazabilirsiniz:

&lt;asp:ScriptManager ID="ScriptManager1" runat="sunucu" /&gt;

ColorPicker denetim genişleticisini sayfaya eklemenin en kolay yolu Tasarım Görünümü'dür. Farenizi txtCardColor TextBox'ın üzerine sokarsanız, akıllı bir görev seçeneği bir genişletici eklemenize olanak sağlar (Bkz. Şekil 3). Bu seçeneği seçerseniz, Genişletici Sihirbazı görüntülenir (Bkz. Şekil 4).

[![Genişletici ekleme](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**Şekil 03**: Genişletici ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-the-colorpicker-control-extender-cs/_static/image6.png))

[![Genişletici Sihirbazı ile bir kontrol genişletici seçme](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**Şekil 04**: Genişletici Sihirbazı ile bir kontrol genişletici seçme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-cs/_static/image8.png))

ColorPicker genişletici ile txtCardColor TextBox genişletmek için ColorPicker genişletici seçebilirsiniz. İletişim kutusunu kapatmak için Tamam'ı tıklatın.

Bu değişiklikleri yaptıktan sonra, sayfanın kaynağı Listeleme 2'ye benzer.

Listeleme 2 - CreateCard.aspx (ColorPicker ile)

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

Sayfanın artık txtCardColor TextBox denetiminin hemen altında görünen bir ColorPickerExtender denetimi içerdiğine dikkat edin. ColorPickerExtender denetimi txtCardColor denetimini genişletir, böylece renk seçici iletişim kutusunu görüntüler.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Renk Seçici İletişim kutusunu başlatmak için Düğme Kullanma

ColorPicker genişletici aşağıdaki özellikleri destekler:

- PopupButtonId - Sayfadaki renk seçici iletişim kutusunun görünmesine neden olan bir düğmenin kimliği.
- PopupPosition - Renk seçici iletişim kutusunun hedef denetimine göre konum. Olası değerler Mutlak, Merkez, BottomLeft, BottomRight, TopLeft, TopRight, Right ve Left (varsayılan BottomLeft) vardır.
- SampleControlId - Seçili rengi görüntüleyen bir denetimin kimliği.
- SelectedColor - ColorPicker tarafından seçilen ilk renk.

Bu özellikleri, renk seçici iletişim kutusunun nasıl görüntüleneceğini ve seçili rengin nasıl görüntüleneceğini özelleştirmek için kullanabilirsiniz. Listeleme 3'teki sayfa, bu özelliklerden birkaçını nasıl kullanabileceğinizi gösterir.

**Listeleme 3 - CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

Listeleme 3'teki sayfada Renk Seç düğmesi bulunur (Bkz. Şekil 5). Bu düğmeyi tıklattığınızda, TextBox'ın üzerinde renk seçici iletişim kutusu görüntülenir. İletişim kutusundan bir renk seçerseniz, seçili renk lblSample Label denetiminin arka plan rengi olarak görünür.

ColorPicker PopupButtonID özelliği ColorPicker genişletici ile Renk Seç düğmesini ilişkilendirmek için kullanılır. PopupButtonID özelliği için bir değer sağladığınızda, hedef denetim odaklandığında renk seçici iletişim kutusu artık görünmez. İletişim kutusunu görüntülemek için düğmeyi tıklatmanız gerekir.

SampleControlID özelliği, seçili rengi ColorPicker ile görüntüleyen bir denetimi ilişkilendirmek için kullanılır. ColorPicker, bu denetimin arka plan rengini şu anda seçili renge değiştirir.

[![Renk seçici iletişim kutusunu bir düğmeyle görüntüleme](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**Şekil 05**: Renk seçici iletişim kutusunu n için bir düğmeyle görüntüleme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-cs/_static/image10.png))

## <a name="summary"></a>Özet

Bu eğitimde, bir açılır renk seçici iletişim kutusunu görüntülemek için ColorPicker denetim genişleticisini kullanmayı öğrendiniz. İlk olarak, odak TextBox denetimine taşındığında iletişim kutusunu nasıl görüntüleyebilirsiniz inceledik. Ardından, düğme tıklatıldığında renk seçici iletişim kutusunu görüntüleyen bir düğme oluşturmayı öğrendiniz.

> [!div class="step-by-step"]
> [Sonraki](using-the-colorpicker-control-extender-vb.md)
