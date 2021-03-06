---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: UpdatePanel Ile bir açılan denetimden geri göndermeler işleme (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Özel dikkatli olunmalıdır...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612933"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>UpdatePanel ile Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir açılan pencerede geri gönderme gerçekleşirken özel dikkatli olunmalıdır.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde PopupControl genişletici, başka bir denetim etkinleştirildiğinde açılan pencereyi tetiklemenin kolay bir yolunu sunar. Bu tür bir açılan pencerede geri gönderme gerçekleşirken özel dikkatli olunmalıdır.

## <a name="steps"></a>Adımlar

Geri göndermede bir `PopupControl` kullanırken, bir `UpdatePanel` geri gönderme nedeniyle oluşan sayfa yenilemeyi engelleyebilir. Aşağıdaki biçimlendirme birkaç önemli öğeyi tanımlar:

- ASP.NET AJAX denetim araç seti 'nin çalışması için `ScriptManager` denetimi
- Her ikisinin de bir açılan pencereyi tetikleyeceği iki `TextBox` denetimi
- Açılan pencere olarak kullanılacak `Panel` denetimi
- Panel içinde, bir `Calendar` denetimi bir `UpdatePanel` denetimine katıştırılır
- Paneli metin kutularına atayan iki `PopupControlExtender` denetimi

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

`Calendar` denetiminin `OnSelectionChanged` özniteliğinin ayarlandığını unutmayın. Böylece Kullanıcı Takvim içinde bir tarih seçtiğinde, bir geri gönderme gerçekleşir ve sunucu tarafı yöntemi `c1_SelectionChanged()` yürütülür. Bu yöntemde, geçerli tarih alınmalıdır ve metin kutusuna geri yazılır.

Bunun sözdizimi şöyledir: Ilki, sayfada `PopupControlExtender` için bir proxy nesnesi oluşturulmalıdır. ASP.NET AJAX denetim araç seti `GetProxyForCurrentPopup()` yöntemini sunar. Bu yöntemin döndürdüğü nesne, açılan pencereyi tetikleyen denetime bir değer gönderen `Commit()` yöntemini destekler (yöntem çağrısını tetikleyen denetim değil!). Aşağıdaki kod, `Commit()` yönteminin bağımsız değişkeni olarak seçilen tarihi sağlar ve kodun seçili tarihi tekrar metin kutusuna yazmasına neden olur:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

Artık Takvim tarihine tıkladığınızda, ilişkili metin kutusunda seçilen tarih görüntülenir, bu, şu anda birçok Web sitesinde bulunan bir tarih seçici denetimi oluşturur.

[![Takvim Kullanıcı metin kutusuna tıkladığında görüntülenir](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

Takvim, Kullanıcı metin kutusuna tıkladığında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklatın](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))

[bir tarihe tıklamak ![metin kutusuna koyar](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

Bir tarihe tıklamak, metin kutusuna koyar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](using-multiple-popup-controls-cs.md)
> [İleri](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
