---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
title: Bir (VB) ayrıntılar Detailview'u ile seçilebilir bir ana GridView kullanan ana/ayrıntı | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, satırları seçme düğmesi yanı sıra her ürünün fiyatını ve adını içeren bir GridView sahip olur. Bir particu seçme düğmesi...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1d1a7c93-971d-4690-9c5e-dac0e5014a09
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
msc.type: authoredcontent
ms.openlocfilehash: 4130b1016d716877bad909d5f7959e519c5d106e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419996"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-vb"></a>Ayrıntılar DetailView’u ile Seçilebilir Bir Ana GridView Kullanan Ana/Ayrıntı (VB)

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_10_VB.exe) veya [PDF olarak indirin](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/datatutorial10vb1.pdf)

> Bu öğreticide, satırları seçme düğmesi yanı sıra her ürünün fiyatını ve adını içeren bir GridView sahip olur. Belirli bir ürün için Seç düğmesini tıklatarak bir DetailsView denetimi aynı sayfada görüntülenecek tam ayrıntılarını neden olur.


## <a name="introduction"></a>Giriş

İçinde [önceki öğreticide](master-detail-filtering-across-two-pages-vb.md) iki web sayfalarını kullanarak ana/ayrıntı rapor oluşturma gördüğümüz: içinden biz görüntülenen tedarikçileri; listesinde "ana" web sayfası ve seçili tarafından sağlanan bu ürünlerin listelenen "details" web sayfası Sağlayıcı. Bu iki sayfa rapor biçimi bir sayfaya sıkıştırılmış. Bu öğreticide, satırları seçme düğmesi yanı sıra her ürünün fiyatını ve adını içeren bir GridView sahip olur. Belirli bir ürün için Seç düğmesini tıklatarak bir DetailsView denetimi aynı sayfada görüntülenecek tam ayrıntılarını neden olur.


[![Select düğmeye tıklandığında ürün ayrıntıları görüntüler.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image1.png)

**Şekil 1**: Ürünün ayrıntılarını görüntüler için Seç düğmesini ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image3.png))


## <a name="step-1-creating-a-selectable-gridview"></a>1. Adım: Seçilebilir GridView oluşturma

Her ana kayıt köprü dahil rapor veren iki sayfalık ana/ayrıntılı geri çağırma, tıklandığında, kullanıcı tıklandı sıranın geçirme ayrıntıları sayfasına gönderilen `SupplierID` sorgu dizesi değeri. Gibi bir köprüyü bir HyperLinkField kullanarak her GridView satır eklendi. Sayfada ana/ayrıntılar raporu için ihtiyacımız her GridView satır, tıklandığında, bir düğme ayrıntılarını gösterir. GridView denetiminde geri göndermeye neden olur ve bu satırın GridView ın işaretler her satır için seçme düğmesi içerecek şekilde yapılandırılabilir [SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx).

Başlamak için bir GridView denetimi ekleyerek `DetailsBySelecting.aspx` sayfasını `Filtering` ayarlama klasörü kendi `ID` özelliğini `ProductsGrid`. Adlı yeni bir ObjectDataSource ekleyeceğimize `AllProductsDataSource` , çağıran `ProductsBLL` sınıfın `GetProducts()` yöntemi.


[![AllProductsDataSource adlı bir ObjectDataSource oluşturma](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image4.png)

**Şekil 2**: Adlı bir ObjectDataSource oluşturma `AllProductsDataSource` ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image6.png))


[![ProductsBLL sınıfı kullanın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image7.png)

**Şekil 3**: Kullanım `ProductsBLL` sınıfı ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image9.png))


[![ObjectDataSource GetProducts() yöntemini çağırmak için yapılandırma](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image10.png)

**Şekil 4**: ObjectDataSource çağırma yapılandırma `GetProducts()` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image12.png))


GridView'ın alanları kaldırma düzenleme dışındaki tüm `ProductName` ve `UnitPrice` BoundFields. Ayrıca, bu BoundFields biçimlendirme gibi gerektiği şekilde özelleştirme rahatça `UnitPrice` BoundField bir para birimi olarak değiştirerek `HeaderText` BoundFields özellikleri. GridView'ın akıllı etiket sütunları Düzenle bağlantıyı tıklatarak ya da bildirim temelli söz dizimi el ile yapılandırma adımları grafik gerçekleştirilebilir.


[![Tüm ProductName ve UnitPrice BoundFields Kaldır](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image13.png)

**Şekil 5**: Tümünü Kaldır ancak `ProductName` ve `UnitPrice` BoundFields ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image15.png))


GridView için son biçimlendirmesi şöyledir:


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample1.aspx)]

Ardından, her satır için Seç düğmesini ekler GridView seçilebilir, olarak işaretlemek ihtiyacımız var. Bunu gerçekleştirmek için GridView'ın akıllı etiket Seçimi Etkinleştir onay kutusunu işaretleyerek.


[![GridView'ın satır seçilebilir olun](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image16.png)

**Şekil 6**: GridView'ın satır seçilebilir olun ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image18.png))


Seçimi etkinleştirme seçeneğini işaretlemek için bir CommandField ekler `ProductsGrid` GridView ile kendi `ShowSelectButton` özelliği True olarak ayarlayın. Şekil 6 gösterildiği gibi bu GridView her satır için bir seçim düğmesini sonuçlanır. Varsayılan olarak, Select düğmeleri LinkButtons işlenir, ancak düğmeler veya ImageButtons bunun yerine CommandField kişinin kullanabileceğiniz `ButtonType` özelliği.


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample2.aspx)]

Bir GridView sıranın Seç düğmesine tıklandığında bir geri gönderme ensues ve GridView'ın `SelectedRow` özellik güncelleştirilir. Ek olarak `SelectedRow` GridView özelliği sağlar [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx), ve [SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) özellikleri. `SelectedIndex` Özelliği ise seçilen sıranın dizinini döndürür `SelectedValue` ve `SelectedDataKey` dönüş değerleri GridView ' ın temel özellikleri [DataKeyNames özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx).

`DataKeyNames` Özelliği bir ilişkilendirmek için kullanılan veya daha fazla veri alanı değerlerini ve her satır ve temel alınan verileri her GridView satır benzersiz olarak tanımlayan bilgiler özniteliği için yaygın olarak kullanılır. `SelectedValue` Özelliği ilk değerini döndürür `DataKeyNames` seçili satır için veri alanı olarak nerede `SelectedDataKey` özelliği döndürür seçilen sıranın `DataKey` tüm için belirtilen veri anahtar alanları için değerleri içeren nesne Bu satır.

`DataKeyNames` GridView, DetailsView veya FormView Tasarımcısı aracılığıyla bir veri kaynağına bağlandığınızda özellik için benzersiz olarak tanımlayan veri alanları otomatik olarak ayarlanır. Bu özellik bizim için otomatik olarak önceki öğreticilerdeki ayarlanmamışken, örnekler olmadan hakkında deneyimli olduğunuzu `DataKeyNames` özelliği belirtilmelidir. Sonraki öğreticiler, biz İnceleme ekleme, güncelleştirme, silme, yanı sıra, ancak bu öğreticide seçilebilir GridView için `DataKeyNames` özelliği düzgün şekilde ayarlanmalıdır. GridView'ın emin olmak için birkaç dakikanızı `DataKeyNames` özelliği `ProductID`.

Şimdi bugüne kadarki tarayıcısından ilerlememizin görüntüleyin. GridView adını ve tüm ürünleri seçin bir LinkButton birlikte fiyatı listelediğine dikkat edin. Select düğmeye tıklandığında geri göndermeye neden olur. 2. adımda seçilen ürünün ayrıntılarını görüntülerken bir DetailsView yanıt bu geri göndermenin ne göreceğiz.


[![Her ürün satır seçin LinkButton içerir](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image19.png)

**Şekil 7**: Her ürün satır seçin bir LinkButton içerir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image21.png))


## <a name="highlighting-the-selected-row"></a>Seçili satır vurgulama

`ProductsGrid` GridView sahip bir `SelectedRowStyle` seçili satır için görsel stil dikte için kullanılan özellik. Düzgün kullanıldığında, bu kullanıcı deneyimini daha net bir şekilde GridView öğesinin hangi satırının seçili göstererek artırabilir. Bu öğreticide, şimdi sarı bir arka plan ile vurgulanmış olmalıdır seçili bir satır vardır.

Öğreticilerimizden önceki gibi CSS sınıfları tanımlanan estetik ilgili ayarlarını korumak şimdi çabalar. Bu nedenle, yeni bir CSS sınıfı içinde oluşturma `Styles.css` adlı `SelectedRowStyle`.


[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample3.css)]

Bu CSS sınıfı için uygulanacak `SelectedRowStyle` özelliği *tüm* GridViews öğretici serimizin Düzenle `GridView.skin` içinde kaplama `DataWebControls` içerecek şekilde tema `SelectedRowStyle` aşağıda gösterildiği gibi ayarları:


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample4.aspx)]

Bu eklenmesiyle, seçili GridView satır, sarı arka plan rengiyle artık vurgulanır.


[![GridView'ın SelectedRowStyle özelliğini kullanarak seçilen sıranın özelleştirme](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image22.png)

**Şekil 8**: GridView'ın seçilen sıranın görünümünü kullanarak özelleştirme `SelectedRowStyle` özelliği ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image24.png))


## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>2. Adım: Bir DetailsView içinde seçili ürünün ayrıntılarını görüntüleme

İle `ProductsGrid` GridView tamamlandı, tüm kalan tek şey, seçili belirli ürün ilgili bilgileri görüntüleyen bir DetailsView eklemek için. GridView yukarıda bir DetailsView denetimi ekleyin ve adlı yeni bir ObjectDataSource oluşturma `ProductDetailsDataSource`. Seçili ürün hakkındaki belirli bilgileri görüntülemek için bu DetailsView istiyoruz olduğundan, yapılandırma `ProductDetailsDataSource` kullanılacak `ProductsBLL` sınıfın `GetProductByProductID(productID)` yöntemi.


[![ProductsBLL sınıfın GetProductByProductID(productID) yöntemi çağırma](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image25.png)

**Şekil 9**: Çağırma `ProductsBLL` sınıfın `GetProductByProductID(productID)` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image27.png))


Sahip *`productID`* GridView denetimin alınan parametrenin değerini `SelectedValue` özelliği. GridView'ın önceki sürümlerinde, ele aldığımız gibi `SelectedValue` özelliği ilk veri anahtar seçili satır için bir değer döndürür. Bu nedenle, zorunludur, GridView'ın `DataKeyNames` özelliği `ProductID`, böylece seçilen sıranın `ProductID` değer tarafından döndürülür `SelectedValue`.


[![GridView'ın SelectedValue özelliği ProductID parametre kümesi](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image28.png)

**Şekil 10**: Ayarlama *`productID`* GridView'ın parametre `SelectedValue` özelliği ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image30.png))


Bir kez `productDetailsDataSource` ObjectDataSource doğru şekilde yapılandırıldığında ve DetailsView için bağlı, Bu öğretici tamamlandı! Sayfa ilk ziyaret edildiğinde, herhangi bir sütun seçiliyse, böylece GridView'ın `SelectedValue` özelliği döndürür `Nothing`. Hiçbir ürünleriyle olduğundan bir `NULL` `ProductID` değeri, kayıt tarafından döndürülür `GetProductByProductID(productID)` yöntemi DetailsView görüntülenmediğini anlamına gelir (bkz. Şekil 11). Bir GridView sıranın Seç düğmesini tıklatarak, bağlı bir geri gönderme ensues ve DetailsView yenilenir. GridView'ın bu sefer `SelectedValue` özelliği döndürür `ProductID` seçilen satırın `GetProductByProductID(productID)` yöntemi döndürür bir `ProductsDataTable` belirli ürün ve DetailsView hakkında bilgi içeren bu ayrıntıları gösterilir (bkz. Şekil 12).


[![İlk ziyaret yalnızca GridView görüntülendiğinde](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image31.png)

**Şekil 11**: GridView'yalnızca ilk ziyaret edildiğinde görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image33.png))


[![Bir satır seçtikten sonra ürün ayrıntıları görüntülenir](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image34.png)

**Şekil 12**: Bir satır seçtikten sonra ürün ayrıntıları görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image36.png))


## <a name="summary"></a>Özet

Bu ve önceki üç öğreticiler çeşitli teknikler ana/ayrıntı raporları görüntülemek için gördük. Biz incelenirken Bu öğreticide, ana kaydeder ve aynı sayfada seçilen ana kayıt hakkındaki ayrıntıları görüntülemek için bir DetailsView barındırmak için seçilebilir GridView kullanarak. Önceki öğreticilerde DropDownList kullanarak ve bir web sayfası ve ayrıntılı kayıtların başka bir ana kayıtlarını görüntüleme ana/Ayrıntılar raporları görüntülemek nasıl inceledik.

Bu öğreticiyi ana/ayrıntı raporları bizim incelenmesi sonlandırır. Sonraki öğretici ile başlayan GridView DetailsView ve FormView ile özelleştirilmiş biçimlendirme bizim araştırma başlarsınız. Kendisine bağlı verileri temel alan bu denetimlerin görünümünü özelleştirmek nasıl GridView'ın alt verileri özetlemek nasıl ve yüksek düzeyde yerleşimi üzerinde denetim elde etmek için şablonları kullanma göreceğiz.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğretici için müşteri adayı İnceleme Hilton Giesenow oluştu. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-across-two-pages-vb.md)
