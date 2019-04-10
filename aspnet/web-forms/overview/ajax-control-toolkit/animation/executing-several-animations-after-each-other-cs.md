---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Arkaya (C#) birkaç animasyon yürütme | Microsoft Docs
author: wenz
description: ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Severa çalıştırılacak sağlar...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: 644af2485c1a51f2de209e968ba1b3475350fa47
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59394074"
---
# <a name="executing-several-animations-after-each-other-c"></a>Arka Arkaya Birkaç Animasyon Yürütme (C#)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)

> ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Art arda birkaç animasyon bir çalıştırmayı sağlar.


ASP.NET AJAX Denetim Araç Seti animasyon denetimi yalnızca bir denetim, ancak bir denetime animasyon eklemek için tam bir çerçeve değil. Art arda birkaç animasyon bir çalıştırmayı sağlar.

## <a name="steps"></a>Adımlar

İlk olarak dahil `ScriptManager` sayfasında; ardından, ASP.NET AJAX kitaplığı, Denetim Araç Seti kullanmayı mümkün hale yüklenir:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

Animasyonun bir panel şuna benzer metin uygulanır:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

İlişkili CSS sınıfı paneli için iyi bir arka plan rengi tanımlayın ve ayrıca panelinin sabit genişlikte ayarlayın:

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

Ardından, ekleme `AnimationExtender` sayfasına sağlayan bir `ID`, `TargetControlID` özniteliği ve bömesinde `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

İçinde `<Animations>` düğümü, kullanım `<OnLoad>` animasyonları sayfanın tam yüklü silindikten sonra çalıştırılacak. Genellikle, `<OnLoad>` yalnızca bir animasyon kabul eder. Animasyon çerçevesi bir kullanarak birkaç animasyon katılmaya sağlar `<Sequence>` öğesi. İçindeki tüm animasyonları `<Sequence>` yürütülen art arda olan. İşte için olası bir biçimlendirme `AnimationExtender` ilk geniş paneli yapma ve ardından yükseklik azalan denetimi:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

Bu komut, panel ilk alır ve ardından daha küçük geniş çalıştırıldığında.


[![Fun genişliğini artırılır](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

İlk genişliğini artırılır ([tam boyutlu görüntüyü görmek için tıklatın](executing-several-animations-after-each-other-cs/_static/image3.png))


[![TMIN yüksekliği azalır](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

Yüksekliği azalır sonra ([tam boyutlu görüntüyü görmek için tıklatın](executing-several-animations-after-each-other-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](executing-several-animations-at-the-same-time-cs.md)
> [İleri](animation-depending-on-a-condition-cs.md)
