---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: (VB) doğrulama denetimleri ile TextBoxWatermark kullanma | Microsoft Docs
author: wenz
description: Bir metin kutusu içinde gösterilir böylece AJAX Denetim Araç Seti TextBoxWatermark denetiminde metin kutusunu genişletir. Bir kullanıcı kutusuna tıkladığında, ben...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: d83fb53ddb40a31013bc724909fa149ce2e4c713
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59387388"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>Doğrulama Denetimleri ile TextBoxWatermark Kullanma (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> Bir metin kutusu içinde gösterilir böylece AJAX Denetim Araç Seti TextBoxWatermark denetiminde metin kutusunu genişletir. Kullanıcı kutusuna tıkladığında boşaltılır. Kullanıcının metin girmeden kutusu ayrılırsa doldurulmuş metni görüntülenir. Bu aynı sayfa üzerinde ASP.NET doğrulama denetimleri ile çakışabilir, ancak bu sorunları gidermek.


## <a name="overview"></a>Genel Bakış

`TextBoxWatermark` AJAX Denetim Araç Seti denetiminde metin kutusuna bir metin kutusu içinde gösterilir böylece genişletir. Kullanıcı kutusuna tıkladığında boşaltılır. Kullanıcının metin girmeden kutusu ayrılırsa doldurulmuş metni görüntülenir. Bu aynı sayfa üzerinde ASP.NET doğrulama denetimleri ile çakışabilir, ancak bu sorunları gidermek.

## <a name="steps"></a>Adımlar

Temel kurulum örnek aşağıda verilmiştir: bir `TextBox` denetimi Filigran kullanarak bir `TextBoxWatermarkExtender` denetimi. Bir düğme, bir geri gönderme tetikler ve daha sonra sayfasında doğrulama denetimlerini tetiklemek için kullanılacaktır. Ayrıca, bir `ScriptManager` denetimi, ASP.NET AJAX başlatmak için gereklidir:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

Şimdi ekleyin bir `RequiredFieldValidator` olup metin alanı form gönderildiğinde denetleyen denetimi. `InitialValue` Doğrulayıcı özelliğini ayarlayın, kullanılan aynı değere `TextBoxWatermarkExtender` denetimi: Form gönderildiğinde, değişmeyen bir metin kutusu içindeki eşik değerini değeridir:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

Ancak bu yaklaşım ile ilgili bir sorun yoktur: JavaScript istemci devre dışı bırakır, metin alanı filigran metni ile bu nedenle doldurulmuş değil `RequiredFieldValidator` bir hata iletisi tetiklemez. Bu nedenle, ikinci `RequiredFieldValidator` denetimi gereklidir, bir boş metin kutusunu denetler (atlama `InitialValue` özniteliği).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

Her iki doğrulayıcıları kullandığından `Display` = `"Dynamic"`, son kullanıcının hangi iki doğrulayıcıları harekete geçirildi görsel görünümünü ayırt edemez; bunun yerine, olduğu gibi yalnızca bunlardan birinin arar.

Son olarak, bir hata iletisi Doğrulayıcı verilen, alandaki metin çıktısını almak için bazı sunucu tarafı kodu ekleyin:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


[![Doğrulayıcı alanı metin olduğunu şeklinde hata verir.](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

Doğrulayıcı alanı metin olduğunu şeklinde hata verir ([tam boyutlu görüntüyü görmek için tıklatın](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-textboxwatermark-in-a-formview-vb.md)
