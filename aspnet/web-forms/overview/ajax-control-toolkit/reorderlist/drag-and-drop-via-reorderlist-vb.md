---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: Sürükleme ve bırakma (VB) ReorderList aracılığıyla | Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 72c697bc2a2005d3ff116cf2f73d80e23bb526dd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124913"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a>ReorderList Aracılığıyla Sürükle ve Bırak (VB)

tarafından [Christian Wenz](https://github.com/wenz)

[Kodu indir](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)

> AJAX Denetim Araç Seti ReorderList denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listenin geçerli sırasını sunucuda kalıcı hale.

## <a name="overview"></a>Genel Bakış

`ReorderList` AJAX Denetim Araç Seti denetimi sürükle ve bırak kullanıcı tarafından sıralanabilir bir liste sağlar. Listenin geçerli sırasını sunucuda kalıcı hale.

## <a name="steps"></a>Adımlar

`ReorderList` Denetim listesi veritabanından veri bağlamayı destekler. Hepsinden önemlisi, sıra liste öğesi için veri deposuna yazma değişiklikleri de destekler.

Bu örnek, Microsoft SQL Server 2005 Express Edition veri deposu olarak kullanır. Veritabanı express sürüm dahil olmak üzere Visual Studio yüklemesi isteğe bağlı (ve boş) bir parçasıdır. Altında ayrı bir indirme olarak kullanılabilir [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Bu örnek için SQL Server 2005 Express Edition örneğini çağrıldığından emin olan varsayıyoruz `SQLEXPRESS` ve web sunucusu; ile aynı makinede bulunan varsayılan kurulumu da budur. Kurulumunuzu farklıysa, veritabanı için bağlantı bilgilerini uymak zorunda.

Microsoft SQL Server Management Studio Express kullanmak için veritabanı ayarlamak için en kolay yolu olan ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). Sunucuya, çift tıklayarak `Databases` ve yeni bir veritabanı oluşturun (sağ tıklatın ve seçin `New Database`) olarak adlandırılan `Tutorials`.

Bu veritabanında adlı yeni bir tablo oluşturma `AJAX` aşağıdaki dört sütun ile:

- `id` (NULL olmayan birincil anahtar, tamsayı, kimlik)
- `char` (char(1), NULL)
- `description` (varchar(50), NULL)
- `position` (int, NULL)

[![AJAX Tablo düzeni](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)

AJAX tablo düzenini ([tam boyutlu görüntüyü görmek için tıklatın](drag-and-drop-via-reorderlist-vb/_static/image3.png))

Ardından, tabloda değerlerin birkaç ile doldurun. Unutmayın `position` sütun öğelerin sıralama düzenini tutar.

[![AJAX tablosundaki ilk veri](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)

AJAX tablosundaki ilk veri ([tam boyutlu görüntüyü görmek için tıklatın](drag-and-drop-via-reorderlist-vb/_static/image6.png))

Oluşturulacak sonraki adım gerektirir bir `SqlDataSource` , tablo ve yeni veritabanı ile iletişim kurmak için denetim. Veri kaynağı desteklemelidir `SELECT` ve `UPDATE` SQL komutları. Daha sonra liste öğelerini sırası değiştirildiğinde, `ReorderList` denetimi otomatik olarak gönderir veri kaynağı için iki değer `Update` komut: yeni konumunu ve öğesinin kimliği. Bu nedenle, gereksinimleri veri kaynağının bir `<UpdateParameters>` bölümü bu iki değer için:

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

`ReorderList` Aşağıdaki öznitelikleri ayarlamak denetim gerekir:

- `AllowReorder`: Liste öğeleri düzenlenebilir olup olmadığı
- `DataSourceID`: Veri kaynağı kimliği
- `DataKeyField`: Birincil anahtar sütunu veri kaynağındaki adı
- `SortOrderField`: Liste öğeleri için sıralama düzeni sağlayan veri kaynak sütunu

İçinde `<DragHandleTemplate>` ve `<ItemTemplate>` bölümleri, liste düzeninin göre ayarlanabilir. Ayrıca, veri bağlama mümkündür kullanarak `Eval()` yöntemi, burada görüldüğü gibi:

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

Aşağıdaki CSS stil bilgileri (bulunulan `<DragHandleTemplate>` bölümünü `ReorderList` denetimi) sürükleme tutamacı geldiğinde fare işaretçisi uygun şekilde değiştirir emin olur:

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

Son olarak, bir `ScriptManager` denetim sayfa için ASP.NET AJAX başlatır:

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

Bu örnekte tarayıcıda çalıştırın ve liste öğeleri biraz yeniden düzenleyebilirsiniz. Daha sonra sayfayı yeniden yükleyin ve/veya veritabanı bir bakalım. Değiştirilen konumları tutulmuş ve değerler tarafından yansıtılır `position` sütun veritabanı ve tüm herhangi bir kod yalnızca işaretleme kullanarak.

[![Veritabanı değişiklikleri yeni liste öğesi sırasına göre verileri](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)

Veritabanı değişiklikleri yeni listesine göre verileri öğe sırasını ([tam boyutlu görüntüyü görmek için tıklatın](drag-and-drop-via-reorderlist-vb/_static/image9.png))

> [!div class="step-by-step"]
> [Önceki](using-postbacks-with-reorderlist-vb.md)
