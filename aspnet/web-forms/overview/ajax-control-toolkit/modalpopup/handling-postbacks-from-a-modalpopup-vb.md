---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: Bir ModalPopup (VB) gelen geri göndermeleri işleme | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti ModalPopup denetiminde istemci-tarafı yollardan kalıcı açılan pencere oluşturmak için basit bir yol sunar. Bir pos olduğunda özel dikkatli olunması gerekir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: add305855d876b5033bbd7921ad24b5e840b9acc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386404"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a>ModalPopup’tan Gelen Geri Göndermeleri İşleme (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> AJAX Denetim Araç Seti ModalPopup denetiminde istemci-tarafı yollardan kalıcı açılan pencere oluşturmak için basit bir yol sunar. Bir geri gönderme içinde açılan oluşturulduğunda, özel dikkatli olunması gerekir.


## <a name="overview"></a>Genel Bakış

AJAX Denetim Araç Seti ModalPopup denetiminde istemci-tarafı yollardan kalıcı açılan pencere oluşturmak için basit bir yol sunar. Bir geri gönderme içinde açılan oluşturulduğunda, özel dikkatli olunması gerekir.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

Ardından, kalıcı açılan hizmet veren bir panel ekleme. Burada, kullanıcı bir ad ve e-posta adresini girebilirsiniz. Bir düğme, açılan kapatın ve bilgileri kaydetmek için kullanılır. Unutmayın `OnClick` özniteliği, bu düğmeye tıklandığında bir geri gönderme gerçekleşmesi ayarlanır:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

Sayfa için tam olarak aynı bilgilerin iki etiket oluşur: ad ve e-posta adresi. Bir düğme kalıcı açılan tetiklemek için kullanılır:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

Açılan pencere görünür hale getirmek için ekleme `ModalPopupExtender` denetimi. Ayarlama `PopupControlID` özniteliği bölmenin Kimliğine ve `TargetControlID` düğmenin kimliği:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

Artık her `Save` içinde kalıcı açılan düğmesine tıklandığında, sunucu tarafı `SaveData()` yöntemi yürütülür. Burada, girilen verileri bir veri deposunda tasarruf sağlayabilirsiniz. Basitleştirmek amacıyla, yeni verilerin yalnızca etikette çıktı:

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

Ayrıca, textbox denetimi içinde kalıcı açılan geçerli bir ad ve e-posta ile doldurulması gerekir. Hiçbir geri gönderme gerçekleştiğinde Ancak bu yalnızca gereklidir. Bir geri gönderme varsa, ASP.NET viewstate özellik metin kutuları uygun değerlerle otomatik olarak doldurur.

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]


[![Kalıcı açılan geri göndermeye neden olur.](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

Kalıcı açılan geri göndermeye neden olur ([tam boyutlu görüntüyü görmek için tıklatın](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-modalpopup-with-a-repeater-control-vb.md)
> [İleri](positioning-a-modalpopup-vb.md)
