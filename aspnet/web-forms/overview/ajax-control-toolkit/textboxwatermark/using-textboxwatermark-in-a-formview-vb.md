---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: FormView 'da Textboxfiligran kullanma (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Bir Kullanıcı, kutuya tıkladığında ben...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627108"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a>Bir FormView’da TextBoxWatermark Kullanma (VB)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> AJAX denetim araç setinde Textboxfiligran denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Kullanıcı, kutuya tıkladığında boşaltılır. Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir. Bu bir FormView denetimi içinde de mümkündür.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde `TextBoxWatermark` denetimi metin kutusunu genişleterek metin kutusu içinde görüntülenir. Kullanıcı, kutuya tıkladığında boşaltılır. Kullanıcı metin girmeden kutudan ayrılsa, önceden doldurulmuş metin yeniden görüntülenir. Bu, bir `FormView` denetimi içinde de mümkündür.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.

Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

Ardından, sayfaya `DELETE`, `INSERT` ve `UPDATE` SQL deyimlerini destekleyen bir veri kaynağı ekleyin. Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın. Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

`FormView` denetiminin `DataSourceID` özelliğinde kullanılacağınızdan, veri kaynağının adını (`ID`) unutmayın. `FormView` `<InsertItemTemplate>` bölümü `TextBoxWatermarkExtender` denetimi tarafından genişletilen bir TextBox içerir. Extender 'ın dışında olmadığından, şablonun içinde bulunduğundan emin olun.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

Artık Kullanıcı `FormView` denetimin ekleme moduna değiştirdiğinde, yeni satıcının metin alanı, `TextBoxWatermarkExtender` denetimi için teşekkürler. TextBox içindeki bir tıklama, dolgu metninin kaybolmasına izin verir.

[alandaki sınır ![genişleticinizden geliyor](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

Alandaki filigran genişleticinizden gelir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Önceki](using-textboxwatermark-with-validation-controls-cs.md)
> [İleri](using-textboxwatermark-with-validation-controls-vb.md)
