---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Bir DropShadow 'un Z dizinini ayarlama (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Bununla birlikte, bu gölge bazen diğer denetimlerle çelişmekte...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613885"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a>Bir DropShadow’un Z Dizinini Ayarlama (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Ancak bu gölge bazen diğer denetimlerle (örneğin, ASP.NET menü denetimi) çakışıyor. Bir menü girdisi açıldığında, bu gölge arkasında görüntülenir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde DropShadow denetimi, bir paneli bir alt gölge ile genişletir. Ancak bu gölge bazen diğer denetimlerle (örneğin, ASP.NET menü denetimi) çakışıyor. Bir menü girdisi açıldığında, bu gölge arkasında görüntülenir.

## <a name="steps"></a>Adımlar

Kod, panelin, efektin görünür olması için yeterli metin içermesi için yeterli metin içeren panelin kendisiyle yorum yapar:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

Başka bir panel `panelShadow` panelinden doğrudan yerleştirilir. Menü girişlerinin `dropShadow` panel) üzerinde görünmesi için yatay yönlendirmeye sahip bir menü içerir (veya bunun yerine: altında):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

Sonra, `panelShadow` panelini bir gölge efektiyle genişletmek için `DropShadowExtender` eklenir:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

Son olarak, ASP.NET AJAX `ScriptManager` denetimi denetim araç setinin çalışmasını sağlar:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

Bu betiği çalıştırdığınızda, menü girdileri panelin altında görünür. Ancak menü, öğelerin diğer panelin önünde görünmesini sağlamak için yalnızca iki şey tanımlamanız gereken `panel` CSS sınıfını kullanır:

- Göreli konumlandırma
- Pozitif bir z dizini

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

Daha sonra, `DropShadowExtender` denetimi menü denetimiyle daha uzun bir süre çakışmaz.

[![önce: menü girdisi görünür değil](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

Önce: menü girdisi görünür değil ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))

[![sonra: menü girdisi görüntülenir](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

Sonra: menü girdisi görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Next](manipulating-dropshadow-properties-from-client-code-cs.md)
