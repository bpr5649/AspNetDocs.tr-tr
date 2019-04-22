---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Birden çok açılan denetim (VB) kullanarak | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. M kullanmak da mümkündür...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: ee66e166d24bb80008671c84f6512d5c54707fcf
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389823"
---
# <a name="using-multiple-popup-controls-vb"></a>Birden Çok Açılan Denetim Kullanma (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Tek bir sayfada birden çok açılan denetim kullanmak da mümkündür.


## <a name="overview"></a>Genel Bakış

AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Tek bir sayfada birden çok açılan denetim kullanmak da mümkündür.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

Ardından, açılan menüsü hizmet veren bir panel ekleme. Geçerli senaryosunda, panele içeren bir `Calendar` denetimi. Takvimin Geri göndermeler tarafından neden sayfa yenilenir önlemek için panel içinde konur bir `UpdatePanel` denetimi:

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

Sayfa, iki metin kutuları da içerir. Metin kutusu etkinleştirildikten sonra her bir metin kutusu için Takvim açılır görünmesi gereken.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

Her iki metin kutuları artık genişleten bir `PopupControlExtender`. `TargetControlID` Öznitelik kimliği için genişletici bağlı denetim sağlar. `PopupControlID` Özniteliği açılır paneli Kimliğini içerir. Bu durumda, her iki Genişleticileri aynı paneli gösterir, ancak farklı panellerin yanı olasılığı vardır.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

Artık bir metin alanı içinde tıklattığınızda, bir takvim tarihi seçmenize olanak sağlar alanının altında görünür. (Seçilen tarihten metin kutularına geri alamazsınız. farklı bir öğreticide ele alınacaktır.)


[![Takvim kullanıcı TextBox'a tıkladığında görünür](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

Takvim kullanıcı TextBox'a tıkladığında görünür ([tam boyutlu görüntüyü görmek için tıklatın](using-multiple-popup-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [İleri](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
