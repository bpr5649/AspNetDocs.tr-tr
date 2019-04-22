---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: İstemci tarafı kod (C#) kullanarak bir animasyonu değiştirme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Ayrıca animasyon...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bdee58aa04e1c8217c2a727b96aa8b239fe1aca
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395614"
---
# <a name="changing-an-animation-using-client-side-code-c"></a>İstemci Tarafı Kod Kullanarak Bir Animasyonu Değiştirme (C#)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Animasyon, özel istemci tarafı JavaScript kodu kullanarak da değiştirilebilir.


## <a name="overview"></a>Genel Bakış

ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Animasyon, özel istemci tarafı JavaScript kodu kullanarak da değiştirilebilir.

## <a name="steps"></a>Adımlar

İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

Animasyonun bir panel şuna benzer metin uygulanır:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

Gerçek animasyon tarafından bir HTML düğmesi başlatılır:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server"`:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

Unutmayın hiçbir `<Animations>` düğümünde `AnimationExtender` denetimi. Özel bir JavaScript kodu denetimiyle kullanılacak animasyonları sağlamak için kullanılır.

Sunucunun API ile `AnimationExtender`, animasyon için genişletici henüz atamak için kolay bir yolu yoktur. Ancak genişletici okuma ve yazma animasyonları çeşitli yöntemleri açığa kaydedilen çeşitli olayları (`OnClick`, `OnLoad`, vb.). Bazı örnekler şunlardır:

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

Dönüş değeri biçimi `get_*()` işlevler için bağımsız değişken biçimlerinin ve kimliklerinin `set_*()` işlevleri, bir nesne temsili, XML işaretlemesini ne olacağını sağlayan bir JSON dizesi. Şu anda, nesneyi geçirmek için bir yolu yoktur, ancak belirli bir animasyon bir nesne okumak mümkündür (`get_OnXXXBehavior()` yöntemleri).

Bir JSON dizesi İşte (sınırlandırma tırnak işaretleri olmadan düzgün şekilde biçimlendirilmiş) düğmesi tarafından tetiklenen animasyon temsil eden, ancak yeniden boyutlandırdıktan ve aynı anda yavaş çıkış panelinde animasyon ekleme:

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

İçin bu JSON descripting aşağıdaki JavaScript kodunu atar `OnClick` geçerli genişletici animasyon ve çalıştırır:

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]


[![Fare tıklatın olmadan (ve çok az biçimlendirme) animasyon hemen çalışır](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

Fare tıklatın olmadan (ve çok az biçimlendirme ile) animasyon hemen çalışır ([tam boyutlu görüntüyü görmek için tıklatın](changing-an-animation-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](executing-animations-using-client-side-code-cs.md)
> [İleri](animating-an-updatepanel-control-cs.md)
