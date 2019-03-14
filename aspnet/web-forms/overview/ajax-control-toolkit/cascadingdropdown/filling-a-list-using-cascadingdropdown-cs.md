---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: (C#) CascadingDropDown kullanarak liste doldurma | Microsoft Docs
author: wenz
description: Bir DropDownList yükleri değişiklikleri anoth değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 795b2a2ee80d3d2bed6f752887d5f9d974151a56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070650"
---
<a name="filling-a-list-using-cascadingdropdown-c"></a>CascadingDropDown Kullanarak Liste Doldurma (C#)
====================
tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir. (Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.


## <a name="overview"></a>Genel Bakış

Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir. (Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Çözmek için ilk testten bu denetimi kullanarak bir açılan listedeki gerçekten doldurmaktır.

## <a name="steps"></a>Adımlar

ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

Ardından, bir DropDownList denetimi gereklidir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

Bu liste için CascadingDropDown genişletici eklenir. Ardından listede görüntülenecek girişlerinin listesini döndürür bir web hizmetini zaman uyumsuz bir istek gönderir. Bunun işe yaraması için aşağıdaki CascadingDropDown öznitelikleri ayarlanması gerekir:

- `ServicePath`: Liste girişlerini sunan bir web hizmeti URL'si
- `ServiceMethod`: Liste girişlerini sunan web yöntemi
- `TargetControlID`: Aşağı açılan liste kimliği
- `Category`: Web yöntemi çağrıldığında gönderilen kategori bilgileri
- `PromptText`: Zaman uyumsuz olarak sunucudan liste verilerini yüklerken görüntülenecek metin

İçin biçimlendirme şöyledir `CascadingDropDown` öğesi. C# ve VB arasındaki tek fark ilişkili web hizmeti adıdır:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

Gelen JavaScript kodu `CascadingDropDown` genişletici imzayla bir web hizmeti yöntemi çağırır:

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

Önemli bir yönüdür yöntemi türünde bir dizi döndürmek gerekir, bu nedenle `CascadingDropDownNameValue` (ASP.NET AJAX Denetim Araç Seti tarafından tanımlanır). İçinde `CascadingDropDownNameValue` Oluşturucu, ilk liste girdinin metin ve değerini sağlanmalıdır, gibi `<option value="VALUE">NAME</option>` HTML yapabilirsiniz. Bazı örnek veriler şu şekildedir:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

Tarayıcı sayfa yükleme üç satıcıları ile doldurulacak liste tetikler.


[![Liste otomatik olarak doldurulur.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

Liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görmek için tıklatın](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](using-cascadingdropdown-with-a-database-cs.md)
