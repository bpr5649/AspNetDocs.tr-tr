---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: İçinde başka bir denetimi (VB) animasyon tetikleme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Genellikle, başlatma bir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: b390ebfaec695a1c2565a91acaa38dbcc10a8959
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425801"
---
<a name="triggering-an-animation-in-another-control-vb"></a>Başka bir Denetimde Animasyon Tetikleme (VB)
====================
tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Bir animasyonu başlatmak, aynı denetimi ile kullanıcı etkileşimi tarafından genel olarak, tetiklenir. Ancak aynı zamanda başka bir denetimde bir denetimi ve sonra animasyon ile etkileşim kurmak mümkün.


## <a name="overview"></a>Genel Bakış

ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Bir animasyonu başlatmak, aynı denetimi ile kullanıcı etkileşimi tarafından genel olarak, tetiklenir. Ancak aynı zamanda başka bir denetimde bir denetimi ve sonra animasyon ile etkileşim kurmak mümkün.

## <a name="steps"></a>Adımlar

İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Animasyonun bir panel şuna benzer metin uygulanır:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Panel animasyonu başlatmak için bir HTML düğmesi kullanılır. Unutmayın `<input type="button" />` üzerinden favoured `<asp:Button />` beri kullanıcı bu düğmeye tıkladığında bir geri gönderme istiyoruz değil.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server"`. Ayarlamak önemlidir `TargetControlID` kimliğine (öğesi animasyonun tetiklenmesi), düğmenin paneli (animasyon uygulanan öğesi) kimliği için

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

İçinde `<Animations>` düğümü, her zamanki şekilde Yerleştir animasyonları. Bunları değiştirmek panelin kolaylaştırmak için düğmesini ayarlayın `AnimationTarget` her animasyon öğesi içinde özniteliği `AnimationExtender`. Değeri `AnimationTarget` paneli Elbette kimliğidir. Bu şekilde, animasyon tetikleme düğmesiyle değil paneli ile gerçekleşir. İşte `AnimationExtender` biçimlendirme bu senaryo için:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Tek tek animasyonları göründüğü özel sıra unutmayın. İlk olarak, animasyon çalıştırıldıktan sonra düğme devre dışı. Olduğundan hiçbir `AnimationTarget` özniteliğini `<EnableAction>` öğesi, animasyon, kaynak denetimine uygulanır: düğme. Sonraki iki animasyon adımlar paralel olarak gerçekleştirilebilmesi (`<Parallel>` öğesi). Her ikisi de kendi `AnimationTarget` öznitelikleri kümesine `"Panel1"`, bu nedenle panelini düğme animasyon ekleme.


[![Bir fare tıklaması düğmesine panelinde animasyonun başlatır](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Bir fare tıklaması düğmesine panelinde animasyonun başlar ([tam boyutlu görüntüyü görmek için tıklatın](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](disabling-actions-during-animation-vb.md)
> [İleri](modifying-animations-from-the-server-side-vb.md)
