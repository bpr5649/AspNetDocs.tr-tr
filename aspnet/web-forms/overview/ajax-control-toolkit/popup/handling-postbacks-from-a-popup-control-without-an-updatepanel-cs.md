---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: (C#) UpdatePanel olmadan bir açılan denetimden gelen geri göndermeleri işleme | Microsoft Docs
author: wenz
description: AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Su içinde bir geri gönderme gerçekleştiğinde...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 3ad041b3df270e65c1dd39cf0cb6adb28b57880e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069675"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>UpdatePanel Olmadan Bir Açılan Denetimden Gelen Geri Göndermeleri İşleme (C#)
====================
tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Bu panelde bir geri gönderme gerçekleşir ve sayfada birkaç panelleri olduğunda hangi panele tıkladı belirlemek zordur.


## <a name="overview"></a>Genel Bakış

AJAX Denetim Araç Seti, PopupControl genişletici herhangi bir denetimi etkinleştirildiğinde, popup tetiklemek için kolay bir yolunu sunar. Bu panelde bir geri gönderme gerçekleşir ve sayfada birkaç panelleri olduğunda hangi panele tıkladı belirlemek zordur.

## <a name="steps"></a>Adımlar

Kullanırken bir `PopupControl` bir geri gönderme, ancak sahip olmayan bir `UpdatePanel` sayfasında Denetim Araç Seti, hangi istemci öğesi sırayla geri göndermenin neden açılan tetiklediğini belirlemek için bir yol sunmaz. Ancak küçük ipucunu bu senaryo için geçici bir çözüm sağlar.

İlk olarak, temel kurulum şöyledir: her iki aynı açılan, bir Takvim tetikleyicisi iki metin kutuları. İki `PopupControlExtenders` metin kutularını ve açılan bir araya getirin.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

Gizli form alanına eklemek için temel fikirdir &lt; `form` &gt; başlatılan açılan metin kutusuna tutan öğesi:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

Sayfa yüklendiğinde, JavaScript kodu için iki metin kutusuna bir olay işleyicisi ekler: Kullanıcı bir metin kutusunda tıkladığında, adını gizli form alanına yazılır:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

Sunucu tarafı kodunda gizli alan değerini okunması gerekir. Gizli form alanları değiştirmek için Önemsiz olduğundan, gizli değeri doğrulamak için bir beyaz liste yaklaşım gereklidir. Doğru metin kutusunu belirlendikten sonra takvimden tarihi üzerine yazılır.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]


[![Takvim kullanıcı TextBox'a tıkladığında görünür](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

Takvim kullanıcı TextBox'a tıkladığında görünür ([tam boyutlu görüntüyü görmek için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))


[![Bir tarihte tıklayarak metin kutusunda yerleştirir](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

Bir tarihte tıklayarak onu koyar metin kutusu içinde ([tam boyutlu görüntüyü görmek için tıklatın](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [İleri](using-multiple-popup-controls-vb.md)
