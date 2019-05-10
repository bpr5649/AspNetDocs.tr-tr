---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: Ana/ayrıntı filtreleme (VB) ile bir DropDownList | Microsoft Docs
author: rick-anderson
description: Bu öğreticide bir DropDownList denetimi ve seçilen liste öğesinin GridView ayrıntılarını ana kayıtları görüntülemek nasıl göreceğiz.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 665acdc303b97d393b714f0b2605ee65b27e0feb
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124239"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Bir DropDownList ile Ana/Ayrıntı Filtreleme (VB)

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) veya [PDF olarak indirin](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)

> Bu öğreticide bir DropDownList denetimi ve seçilen liste öğesinin GridView ayrıntılarını ana kayıtları görüntülemek nasıl göreceğiz.

## <a name="introduction"></a>Giriş

Rapor ortak bir tür *ana/ayrıntı raporu*, içindeki bazı "ana" kayıt kümesini göstererek raporu başlar. Kullanıcı daha sonra bir ana kayıtlar, böylece ana kayıt "ayrıntılarını." görüntüleme detaya gidebilirsiniz Ana/ayrıntı olan bir rapor gibi bire çok ilişkileri görselleştirmek için ideal seçim kategorilerin tümünü gösterir ve ardından belirli bir kategori seçin ve onun ilişkili ürünleri görüntülemek bir kullanıcı bildirir. Ayrıca, ana/ayrıntı raporları, "geniş" özellikle tabloları (olanları çok sütun) öğesinden ayrıntılı bilgiler görüntülemek için yararlıdır. Örneğin, ana/ayrıntı raporu "ana" düzeyini, yalnızca ürün adını ve birim fiyatına ürünleri veritabanında gösterebilir ve belirli bir ürün şeklinde detaya ek ürün alanları gösterir (kategori, tedarikçi, birim başına miktar ve vb.).

İle ana/ayrıntı raporu uygulanabilir birçok yolu vardır. Bu ve sonraki üç öğreticiler ana/ayrıntı raporları çeşitli inceleyeceğiz. Bu öğreticide ana kayıtları görüntülemek nasıl görüyoruz bir [DropDownList denetimi](https://msdn.microsoft.com/library/dtx91y0z.aspx) ve seçili liste öğesini GridView ayrıntıları. Özellikle, bu öğreticinin ana/ayrıntı rapor kategorisi ve ürün bilgilerini listeler.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>1. Adım: Bir DropDownList içinde kategorilerini görüntüleme

Bir DropDownList kategorileri görüntülenen seçili liste öğesinin ürünleri ile ana/ayrıntı raporumuzun listeler GridView sayfasında daha ilerisine. Ardından bize önce ilk görev bir DropDownList içinde görüntülenen kategorileri sağlamaktır. Açık `FilterByDropDownList.aspx` sayfasını `Filtering` klasörü üzerinde bir DropDownList sayfanın Tasarımcısı araç kutusundan sürükleyin ve ayarlayın, `ID` özelliğini `Categories`. Ardından, akıllı etiket DropDownList'ın veri kaynağı Seç bağlantıdan tıklayın. Bu veri kaynağı Yapılandırma Sihirbazı'nı görüntüler.

[![DropDownList'ın veri kaynağını belirtin](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)

**Şekil 1**: DropDownList'ın veri kaynağını belirtin ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))

Adlı yeni bir ObjectDataSource eklemek için `CategoriesDataSource` , çağıran `CategoriesBLL` sınıfın `GetCategories()` yöntemi.

[![CategoriesDataSource adlı yeni bir ObjectDataSource Ekle](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)

**Şekil 2**: Adlı yeni bir ObjectDataSource ekleme `CategoriesDataSource` ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))

[![CategoriesBLL sınıfını kullanmak seçin](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)

**Şekil 3**: Use yöntemine seçin `CategoriesBLL` sınıfı ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png))

[![ObjectDataSource GetCategories() yöntemi kullanmak üzere yapılandırma](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)

**Şekil 4**: ObjectDataSource kullanılacak yapılandırma `GetCategories()` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))

Biz yine de hangi veri kaynağı alanı DropDownList içinde görüntülenmesi gerekir ve hangi belirtmenize gerek ObjectDataSource yapılandırdıktan sonra bir liste öğesi için bir değer olarak ilişkili olmalıdır. Sahip `CategoryName` görüntü olarak alan ve `CategoryID` değeri her liste öğesi olarak.

[![CategoryName alan ve kullanım CategoryID DropDownList görünen değere sahip](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)

**Şekil 5**: DropDownList görüntülemesi `CategoryName` alan ve kullanım `CategoryID` değeri ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png))

Kayıtlardan doldurulur bir DropDownList denetimi bu noktada sahibiz `Categories` tablo (tümü yaklaşık altı saniyeler içinde gerçekleştirilir). Şekil 6 ilerlememizin şimdiye kadarki bir tarayıcıdan görüntülendiğinde gösterir.

[![Bir açılan geçerli kategorileri listeler](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)

**Şekil 6**: Bir açılan listeler geçerli kategorilerin ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png))

## <a name="step-2-adding-the-products-gridview"></a>2. Adım: Ürünleri GridView ekleme

Ana/ayrıntı raporumuzun bu son adımda, seçilen kategori ile ilişkili ürün listesi sağlamaktır. Bunu gerçekleştirmek için GridView sayfaya ekleyin ve adlı yeni bir ObjectDataSource oluşturma `productsDataSource`. Sahip `productsDataSource` denetimi, verilerden cull `ProductsBLL` sınıfın `GetProductsByCategoryID(categoryID)` yöntemi.

[![GetProductsByCategoryID(categoryID) yöntemi seçin](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)

**Şekil 7**: Seçin `GetProductsByCategoryID(categoryID)` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png))

Bu yöntem seçtikten sonra ObjectDataSource Sihirbazı bize değeri için yöntemin ister *`categoryID`* parametresi. Seçili değerini kullanacak şekilde `categories` DropDownList öğesi denetimi ve ControlId için parametre kaynağı ayarla `Categories`.

[![CategoryID parametresi kategorileri DropDownList değerine ayarlayın.](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)

**Şekil 8**: Ayarlama *`categoryID`* parametre değerine `Categories` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png))

Bir tarayıcıda ilerlememizin kullanıma için bir dakikanızı ayırın. İlk sayfasını ziyaret ederek, bu ürünlerin seçilen kategoriye ait (İçecekler), (Şekil 9'da gösterildiği gibi) görüntülenir, ancak DropDownList değiştirme veri güncelleştirilmiyor. GridView güncelleştirmek bir geri gönderme gerçekleşmelidir olmasıdır. Bunu gerçekleştirmek için (hiçbiri, herhangi bir kod yazmadan gerektirir) iki seçenek sunuyoruz:

- **Kategorilerini DropDownList's**[AutoPostBack özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**true.** (Bunu DropDownList'ın akıllı etiket AutoPostBack etkinleştir seçeneğini işaretleyerek gerçekleştirebilirsiniz.) DropDownList'ın seçili olduğunda, bu bir geri gönderme tetikleyecek öğe kullanıcı tarafından değiştirildi. Bu nedenle, kullanıcı DropDownList'e yeni kategori seçtiğinde bir geri gönderme ardından ve yeni seçilen kategori ürünlerle GridView güncelleştirilir. (Bu öğreticide kullanılan yaklaşım budur.)
- **Bir DropDownList yanındaki düğmeyi Web denetimi ekleyin.** Ayarlama, `Text` yenileme özelliğini ya da benzer. Bu yaklaşımda, kullanıcı yeni bir kategori seçin ve ardından düğmesine gerekecektir. Düğmeye tıklandığında geri göndermeye neden ve bu ürünlerin, seçilen kategori listelemek için GridView güncelleştirin.

Şekil 9 ve 10 eylem ana/ayrıntı raporu gösterilmektedir.

[![Sayfa ilk ziyaret edildiğinde, içecek ürünleri görüntülenir](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)

**Şekil 9**: Sayfa ilk ziyaret edildiğinde, içecek ürünleri görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png))

[![Yeni bir ürün (ürün) otomatik olarak seçilmesi GridView güncelleştirme geri göndermenin neden olur](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)

**Şekil 10**: Yeni bir ürün (ürün) otomatik olarak seçilmesi GridView güncelleştiriliyor, bir geri gönderme neden olur ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png))

## <a name="adding-a----choose-a-category----list-item"></a>"--Bir kategori seçin--" liste öğesi ekleme

İlk ziyaret edildiğinde `FilterByDropDownList.aspx` DropDownList'ın ilk liste öğesinin (İçecekler) içecek ürünleri gösteren GridView içinde varsayılan olarak seçili kategorileri sayfa. Bunun yerine bir DropDownList öğesi olmasını isteyebilirsiniz ilk kategori ürünleri gösteren seçili yerine gibi "--bir kategori seçin--" diyor.

DropDownList'e yeni bir liste öğesi eklemek için özellikler penceresine gidin ve içinde üç noktaya tıklayarak `Items` özelliği. İle yeni bir liste öğesi ekleme `Text` "--bir kategori seçin--" ve `Value` `-1`.

[![Ekleme bir--bir kategori--liste öğesini seçin.](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)

**Şekil 11**: Ekleme bir--bir kategori--liste öğesini seçin ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))

Alternatif olarak, aşağıdaki biçimlendirme DropDownList'e ekleyerek liste öğesi ekleyebilirsiniz:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

Ayrıca, DropDownList denetimin ayarlamak ihtiyacımız `AppendDataBoundItems` kategorileri ObjectDataSource DropDownList'e bağlandığında, herhangi bir el ile eklenen liste öğelerini, şunun üzerine yazacağız çünkü true `AppendDataBoundItems` True değil.

![AppendDataBoundItems özelliğini True olarak ayarlayın](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

**Şekil 12**: Ayarlama `AppendDataBoundItems` özelliği true

Bu değişikliklerden sonra sayfa ilk ziyaret edildiğinde "--bir kategori seçin--" seçeneğini seçili olduğundan ve hiçbir ürünleri görüntülenir.

[![İlk sayfa yükü hiçbir ürünleri görüntülenir](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)

**Şekil 13**: İlk sayfa yükü Hayır ürünler hakkında görüntülenen ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png))

Ürün yok "--bir kategori seçin--" liste öğesi seçildiğinden, görüntülenme nedeni değeri olduğundan `-1` ve veritabanında hiçbir ürünü mevcuttur bir `CategoryID` , `-1`. Bu davranıştır bu noktada işiniz sonra isterseniz! Ancak görüntülemek istiyorsanız, *tüm* Kategorilerini "--bir kategori seçin--" liste öğesi seçildiğinde dönmek `ProductsBLL` sınıfı ve özelleştirme `GetProductsByCategoryID(categoryID)` BT'nin çağırır, böylece yöntemi `GetProducts()` yöntemi varsa geçirilen içinde *`categoryID`* parametresi sıfırdan küçük:

[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

Burada kullanılan bir teknik yaklaşım tüm Üreticiler görüntülenecek kullandık benzer geri [bildirim temelli parametreler](../basic-reporting/declarative-parameters-cs.md) öğretici, bu örneğin değerini kullanıyoruz ancak `-1` tüm kayıtları olması gerektiğini belirtmek için öğesine alınan `Nothing`. Bunun nedeni, *`categoryID`* parametresinin `GetProductsByCategoryID(categoryID)` yöntemi, tamsayı değeri geçirilen gibi bildirim temelli parametreler öğreticide biz dizesi giriş parametresi geçirerek ise bekliyor.

Şekil 14 gösteren ekran görüntüsü `FilterByDropDownList.aspx` "--bir kategori seçin--" seçeneği seçildiğinde. Burada, varsayılan olarak tüm ürünleri görüntülenir ve kullanıcının görünen belirli bir kategori seçerek daraltabilirsiniz.

[![Artık listelenen varsayılan olarak tüm ürünleri olan](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)

**Şekil 14**: Artık listelenen varsayılan olarak tüm ürünleri olan ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png))

## <a name="summary"></a>Özet

Hiyerarşik olarak ilgili verileri görüntülerken, bu genellikle, kullanıcı verileri hiyerarşisinin üstünde harcadığı başlatabilir ve aşağı detaylarına ana/ayrıntı raporları kullanarak verileri sunmak için yardımcı olur. Bu öğreticide, seçilen kategori ürünleri gösteren bir basit ana/ayrıntı rapor oluşturmaya incelenir. Bu bir DropDownList kategorileri ve GridView Seçili kategoriye ait olan ürünlerin listesini kullanarak gerçekleştirilebilir.

İçinde [sonraki öğreticiye](master-detail-filtering-with-two-dropdownlists-vb.md) biz DropDownList arabirimi bir adım daha iki DropDownList kullanarak sürer.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Önceki](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [İleri](master-detail-filtering-with-two-dropdownlists-vb.md)
