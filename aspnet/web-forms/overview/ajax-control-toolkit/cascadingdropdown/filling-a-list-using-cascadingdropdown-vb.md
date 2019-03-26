---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: (VB) CascadingDropDown kullanarak liste doldurma | Microsoft Docs
author: wenz
description: Bir DropDownList yükleri değişiklikleri anoth değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: b4bbe5c120a6f17a7dca08e6fc855018a2e23797
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421966"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a>CascadingDropDown Kullanarak Liste Doldurma (VB)
====================
tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir. (Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.


## <a name="overview"></a>Genel Bakış

Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir. (Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

Ardından, bir DropDownList denetimi gereklidir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

Bu liste için CascadingDropDown genişletici eklenir. Ardından listede görüntülenecek girişlerinin listesini döndürür bir web hizmetini zaman uyumsuz bir istek gönderir. Bunun işe yaraması için aşağıdaki CascadingDropDown öznitelikleri ayarlanması gerekir:

- `ServicePath`: Liste girişlerini sunan bir web hizmeti URL'si
- `ServiceMethod`: Liste girişlerini sunan web yöntemi
- `TargetControlID`: Aşağı açılan liste kimliği
- `Category`: Web yöntemi çağrıldığında gönderilen kategori bilgileri
- `PromptText`: Zaman uyumsuz olarak sunucudan liste verilerini yüklerken görüntülenecek metin

İçin biçimlendirme şöyledir `CascadingDropDown` öğesi. C# ve VB arasındaki tek fark ilişkili web hizmeti adıdır:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

Gelen JavaScript kodu `CascadingDropDown` genişletici imzayla bir web hizmeti yöntemi çağırır:

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

Önemli bir yönüdür yöntemi türünde bir dizi döndürmek gerekir, bu nedenle `CascadingDropDownNameValue` (ASP.NET AJAX Denetim Araç Seti tarafından tanımlanır). İçinde `CascadingDropDownNameValue` oluşturucusu, liste girdinin metin ve değerini sağlanmalıdır, ilk gibi `<option value="VALUE">NAME</option>` HTML yapabilirsiniz. Bazı örnek veriler şu şekildedir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

Tarayıcı sayfa yükleme üç satıcıları ile doldurulacak liste tetikler.


[![Liste otomatik olarak doldurulur.](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görmek için tıklatın](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-auto-postback-with-cascadingdropdown-cs.md)
> [İleri](using-cascadingdropdown-with-a-database-vb.md)
