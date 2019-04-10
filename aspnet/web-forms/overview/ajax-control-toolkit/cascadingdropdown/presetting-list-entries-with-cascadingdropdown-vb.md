---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: (VB) CascadingDropDown ile liste girişlerini önceden ayarlama | Microsoft Docs
author: wenz
description: Bir DropDownList yükleri değişiklikleri anoth değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e685d599e3dbc095631e3c28a603ac9c38f799c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385897"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="24082-103">CascadingDropDown ile Liste Girişlerini Önceden Ayarlama (VB)</span><span class="sxs-lookup"><span data-stu-id="24082-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="24082-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="24082-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="24082-105">[Kodu indir](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="24082-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="24082-106">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="24082-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="24082-107">Biraz kod ile verileri dinamik olarak yüklendikten sonra bir liste öğesinin seçilmiş mümkündür.</span><span class="sxs-lookup"><span data-stu-id="24082-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>


## <a name="overview"></a><span data-ttu-id="24082-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="24082-108">Overview</span></span>

<span data-ttu-id="24082-109">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="24082-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="24082-110">(Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Biraz kod ile verileri dinamik olarak yüklendikten sonra bir liste öğesinin seçilmiş mümkündür.</span><span class="sxs-lookup"><span data-stu-id="24082-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="24082-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="24082-111">Steps</span></span>

<span data-ttu-id="24082-112">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde `<form>` öğesi):</span><span class="sxs-lookup"><span data-stu-id="24082-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="24082-113">Ardından, bir DropDownList denetimi gereklidir:</span><span class="sxs-lookup"><span data-stu-id="24082-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="24082-114">Bu liste için web hizmeti URL'sini ve yöntemi bilgilerini sağlama CascadingDropDown genişletici eklenir:</span><span class="sxs-lookup"><span data-stu-id="24082-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="24082-115">CascadingDropDown genişletici daha sonra bir web hizmeti aşağıdaki yöntem imzasını ile zaman uyumsuz olarak çağırır:</span><span class="sxs-lookup"><span data-stu-id="24082-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="24082-116">Yöntem CascadingDropDown değer türünde bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="24082-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="24082-117">Liste girişin açıklamalı alt yazı ve değer türün yapıcı ilk bekliyor (HTML `value` özniteliği).</span><span class="sxs-lookup"><span data-stu-id="24082-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="24082-118">Üçüncü bağımsız değişkeni ayarlanmışsa true olarak liste öğesi tarayıcıda otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="24082-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="24082-119">Tarayıcı sayfa yükleme üç satıcılarla açılan listede seçilmiş ikinci bir doldurur.</span><span class="sxs-lookup"><span data-stu-id="24082-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>


[![T<span data-ttu-id="24082-120">He listesi doldurulur ve otomatik olarak seçilmiş]</span><span class="sxs-lookup"><span data-stu-id="24082-120">he list is filled and preselected automatically]</span></span>(presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

<span data-ttu-id="24082-121">Liste doldurulmuş ve otomatik olarak seçilmiş ([tam boyutlu görüntüyü görmek için tıklatın](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="24082-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="24082-122">[Önceki](using-cascadingdropdown-with-a-database-vb.md)
> [İleri](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="24082-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
