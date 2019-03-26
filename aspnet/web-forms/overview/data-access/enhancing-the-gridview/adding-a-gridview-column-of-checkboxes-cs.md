---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: Onay kutularından (C#) oluşan GridView sütunu ekleme | Microsoft Docs
author: rick-anderson
description: Bu öğretici, kullanıcı G. birden çok satır seçme kullanımı kolay bir yol sağlamak üzere bir GridView denetimi için onay kutuları içeren bir sütun ekleme bakan...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: b78e87d7bd6a05b790203808a9be52af8e8aad1e
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58422980"
---
<a name="adding-a-gridview-column-of-checkboxes-c"></a>Onay Kutularından Oluşan GridView Sütunu Ekleme (C#)
====================
tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe) veya [PDF olarak indirin](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> Bu öğretici, kullanıcı birden çok satır GridView'ın seçilmesi, kullanımı kolay bir yol sağlamak üzere bir GridView denetimi için onay kutuları içeren bir sütun ekleme bakar.


## <a name="introduction"></a>Giriş

Önceki öğreticide size belirli bir kayıt seçmek amacıyla GridView radyo düğmelerinden oluşan bir sütun eklemek nasıl incelenir. Kullanıcı kılavuzundan en fazla bir öğe seçmek için sınırlı olduğunda radyo düğmelerinden oluşan bir sütunu uygun kullanıcı arabirimidir. Bazen, ancak biz kılavuzdan öğeleri tercihe bağlı sayıda kullanıcının izin vermek isteyebilirsiniz. Web tabanlı e-posta istemcileri, örneğin, genellikle onay kutularından oluşan bir sütun ile iletilerinin listesini görüntüler. Kullanıcı, iletileri rastgele bir sayıdan seçin ve ardından başka bir klasöre e-postaları taşıma veya silme gibi bazı eylemleri gerçekleştirin.

Bu öğreticide onay kutularından oluşan bir sütun eklemek nasıl ve hangi onay kutularını geri göndermede denetlenen belirleme göreceğiz. Özellikle, web tabanlı e-posta istemcisi kullanıcı arabirimi yakından taklit eden bir örnek oluşturacağız. Bizim örneğimizde ürünleri listeleme disk belleğine alınan GridView içerecektir `Products` bir onay kutusu her veritabanı tablosu satır (bkz. Şekil 1). Tıklandığında, seçili ürünlerin Sil düğmesini seçili bu ürünlerin silinmesine neden olur.


[![Bir onay kutusu her bir ürün satır içerir](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**Şekil 1**: Bir onay kutusu her bir ürün satır içerir ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png))


## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>1. Adım: Ürün bilgileri listeleyen bir disk belleğine alınan GridView ekleme

Onay kutularından oluşan bir sütun ekleme hakkında endişe önce disk belleği destekleyen GridView ürünleri listeleme s ilk odaklanmasına olanak tanır. Başlangıç açarak `CheckBoxField.aspx` sayfasını `EnhancedGridView` klasörü ve ayar Tasarımcısı araç kutusundan sürükleyip GridView kendi `ID` için `Products`. Ardından, GridView adlı yeni bir ObjectDataSource bağlamak seçin `ProductsDataSource`. ObjectDataSource kullanmak için yapılandırma `ProductsBLL` çağırma, sınıf `GetProducts()` verileri döndürmek için yöntemi. Bu GridView salt okunur olacağından, güncelleştirme, ekleme, açılan listeler ayarlayın ve sekme (hiçbiri) SİLİN.


[![ProductsDataSource adlı yeni bir ObjectDataSource oluşturma](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**Şekil 2**: Adlı yeni bir ObjectDataSource oluşturma `ProductsDataSource` ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))


[![ObjectDataSource GetProducts() yöntemi kullanarak verileri almak için yapılandırma](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**Şekil 3**: ObjectDataSource kullanarak verileri almak için yapılandırma `GetProducts()` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))


[![Güncelleştirme, ekleme, açılan listeler ayarlayın ve sekmeleri (hiçbiri) silme](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**Şekil 4**: Aşağı açılan listeler güncelleştirme, ekleme ve silme sekmeler (hiçbiri) ayarlayın ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))


Veri Kaynağı Yapılandırma Sihirbazı'nı tamamladıktan sonra BoundColumns ve ürünle ilgili veri alanları için bir CheckBoxColumn otomatik olarak Visual Studio oluşturur. Önceki öğreticide yaptığımız gibi Kaldır dışındaki tüm `ProductName`, `CategoryName`, ve `UnitPrice` BoundFields, değiştirip `HeaderText` ürün, kategori ve fiyat özellikler. Yapılandırma `UnitPrice` BoundField böylece değerini para birimi olarak biçimlendirilir. GridView'ın akıllı etiket sayfalama etkinleştir onay kontrol ederek disk belleği desteği de yapılandırın.

Ayrıca seçili ürünlerin silmek için kullanıcı arabirimi ekleme s olanak tanır. Ayarı GridView altındaki bir düğme Web denetimi ekleyin, `ID` için `DeleteSelectedProducts` ve kendi `Text` özelliğini Sil ürün seçildi. Ürün veritabanından gerçekten silmek yerine, bu örnek için yalnızca, silinmiş ürünleri bildiren bir ileti görüntüleyeceğiz. Bunu yapabilmek için bir etiket Web denetimi düğmenin altına ekleyin. Kimliğine ayarlayın `DeleteResults`kullanıma temizleyin, `Text` özelliği ve kümesi kendi `Visible` ve `EnableViewState` özelliklerine `false`.

Bu değişiklikleri yaptıktan sonra GridView, ObjectDataSource, düğme ve etiket s bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

Sayfasını bir tarayıcıda görüntülemek için bir dakikanızı ayırın (bkz: Şekil 5). Bu noktada ad, kategori ve fiyat ilk on ürün görmeniz gerekir.


[![Ad, kategori ve ilk on ürün fiyatı listelenir.](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**Şekil 5**: Ad, kategori ve ilk on ürün fiyatı listelenir ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png))


## <a name="step-2-adding-a-column-of-checkboxes"></a>2. Adım: Onay kutularından oluşan bir sütun ekleme

ASP.NET 2.0 bir CheckBoxField içerdiğinden, biri, bir sütun onay kutularından oluşan GridView için eklemek için kullanılabilir düşünebilirsiniz. CheckBoxField Boole veri alanı ile çalışmak için tasarlandığı gibi ne yazık ki bu durumda değil. Diğer bir deyişle, CheckBoxField kullanmak için şu değeri işlenmiş onay kutusunun işaretli olup olmadığını belirlemek için alınmadığında temel alınan veri alanını belirtmeniz gerekir. Yalnızca işaretli onay kutularından oluşan bir sütun eklemek için biz CheckBoxField kullanamazsınız.

Bunun yerine, biz bir TemplateField ekleyin ve bir onay kutusu Web denetimi için eklemeniz gerekir, `ItemTemplate`. Bir tane eklemek için bir TemplateField `Products` GridView ve ilk (en sol) alanı kolaylaştırır. GridView s akıllı etiket Şablonları Düzenle bağlantısına tıklayın ve ardından araç kutusundan bir onay kutusu Web denetimi sürükleyin `ItemTemplate`. Bu onay kutusu s ayarlamak `ID` özelliğini `ProductSelector`.


[![ProductSelector TemplateField s ItemTemplate için adlı bir onay kutusu Web denetimi ekleme](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**Şekil 6**: Bir onay kutusu Web denetimi adlı ekleme `ProductSelector` TemplateField s `ItemTemplate` ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png))


Eklenen TemplateField ve onay kutusu Web denetimi ile her satır bir onay kutusu artık içerir. Şekil 7, onay kutusunu ve TemplateField eklendikten sonra bir tarayıcıdan görüntülendiğinde bu sayfayı gösterir.


[![Her ürün satır bir onay kutusu artık içerir.](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**Şekil 7**: Her ürün satır bir onay kutusu artık içerir ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png))


## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>3. Adım: Hangi onay kutularını belirleme geri göndermede iade

Bu noktada bir onay kutularını ancak hiçbir şekilde geri göndermede hangi onay kutularını denetlenen belirlenemiyor sütununun sahibiz. Ancak, seçili ürünlerin Sil düğmesine tıklandığında, biz hangi onay kutularını bu ürünlerin silinmesi için denetlenen bilmeniz gerekir.

GridView s [ `Rows` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) GridView veri satırlarına erişim sağlar. Biz bu satırlara yineleme onay kutusu denetimi programlı olarak erişmek ve ardından başvurun, `Checked` onay kutusunun seçili olup olmadığını belirlemek için özellik.

İçin bir olay işleyicisi oluşturun `DeleteSelectedProducts` düğmesi Web denetimi s `Click` olay ve aşağıdaki kodu ekleyin:


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

`Rows` Özellik koleksiyonunu döndürür `GridViewRow` GridView s veri satırları, düzenini örnekler. `foreach` Döngü burada bu koleksiyon numaralandırır. Her `GridViewRow` nesnesi, satır s onay kutusu, kullanarak program aracılığıyla erişildiğinde `row.FindControl("controlID")`. Onay kutusu işaretli değilse, ilgili satır s `ProductID` değer alınır `DataKeys` koleksiyonu. Bu alıştırmada, yalnızca bilgilendirici iletisinde görüntüleriz `DeleteResults` içinde çalışan bir uygulama d biz bunun yerine çağrı yapmak olsa da, etiket `ProductsBLL` s sınıfı `DeleteProduct(productID)` yöntemi.

Bu olay işleyicisi'nın eklenmesiyle, seçili ürünlerin silme artık düğmesi görüntüler `ProductID` seçili ürünlerin s.


[![Seçili ürün ProductIDs Sil Seçili ürünleri düğmesine tıklandığında listelenir](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**Şekil 8**: Ne zaman Sil Seçili ürünleri düğmesine tıklandığında ürün seçildi `ProductID` s listelenir ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png))


## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>4. Adım: Ekleme tüm denetler ve tüm düğmeler işaretini kaldırın

Bir kullanıcı geçerli sayfadaki tüm ürünleri silme istiyorsa, bunlar her on onay kutularını işaretlemeniz gerekir. Bir kontrol tüm ekleyerek bu işlemi hızlandırmak yardımcı olabiliriz, düğmesine tıklandığında, tüm onay kutularını kılavuzda seçer. Bir onay kutusunu temizleyin tüm düğmesi eşit yardımcı olacaktır.

Bunları GridView yerleştirme sayfasına iki düğme Web denetimi ekleyin. İlk s ayarlamak `ID` için `CheckAll` ve kendi `Text` özelliğini denetle; ikinci bir s kümesi `ID` için `UncheckAll` ve kendi `Text` özelliğini tüm işaretini kaldırın.


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

Ardından, arka plan kod sınıfı adlı bir yöntem oluşturma `ToggleCheckState(checkState)` , çağrıldığında numaralandırır `Products` GridView s `Rows` koleksiyonu ve her onay kutusu s ayarlar `Checked` geçirilen değere içinde *checkState*  parametresi.


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

Ardından, oluşturma `Click` için olay işleyicileri `CheckAll` ve `UncheckAll` düğmeleri. İçinde `CheckAll` s olay işleyicisi, yalnızca çağrı `ToggleCheckState(true)`; `UncheckAll`, çağrı `ToggleCheckState(false)`.


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

Bu kod denetle düğmesine tıklayarak geri göndermeye neden olur ve tüm onay kutularını GridView de denetler. Benzer şekilde, tüm onay kutularının işaretini kaldırın tüm tıklayarak seçili olanları kaldırdığında. Şekil 9, denetle düğmesine kaydedildikten sonra ekranı gösterilir.


[![Tüm düğme denetimi tıklayarak tüm onay kutularının seçer](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**Şekil 9**: Denetleme tüm düğmesini seçer tüm onay kutularını tıklayarak ([tam boyutlu görüntüyü görmek için tıklatın](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png))


> [!NOTE]
> Onay kutusunu seçerek veya onay kutularını tümünün seçimini için bir yaklaşım bir sütunu görüntüleme için başlık satırındaki onay kutusu aracılığıyla olduğunda. Ayrıca, geçerli tüm denetleyin / işaretini kaldırın tüm uygulama bir geri gönderme gerektirir. Onay kutularını, ancak işaretli veya işaretsiz, böylece snappier bir kullanıcı deneyimi sağlayan tamamen istemci tarafı komut dosyası, olabilir. Bir üst bilgi satırı onay kutusuna, istemci tarafı teknikleri kullanma hakkında bir tartışma yanı sıra ayrıntılı denetle ve tüm işaretini kaldırın kullanarak keşfetmek için kullanıma [denetimi tüm onay kutularının GridView kullanarak istemci tarafı komut dosyası ve bir onay tüm kutusu](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx).


## <a name="summary"></a>Özet

Devam etmeden önce GridView satır rastgele bir sayıdan arasından kullanıcıların gerek duyduğunuz senaryolara durumda onay kutularından oluşan bir sütun ekleyerek bir seçenektir. Bu öğreticide gördüğümüz gibi GridView içinde onay kutularından oluşan bir sütun içeren bir onay kutusu Web denetimi ile bir TemplateField ekleme kapsar. Bir Web denetimi (biz önceki öğreticide yaptığınız gibi karşı biçimlendirme şablonuna doğrudan ekleme) kullanarak ASP.NET otomatik olarak hatırlar ne onay kutularını olan ve geri gönderme arasında işaretli değil. Biz, onay kutularını kodda belirli bir onay kutusunun işaretli olup olmadığını belirlemek için ya da işaretli durumu değiştirmek için program aracılığıyla da erişebilirsiniz.

Bu öğretici ve sonuncu GridView'a satır seçici sütun ekleme sırasında arıyordu. Sonraki müşterilerimize öğreticide nasıl ile biraz iş ekleme özellikleri GridView'a ekleyebiliriz inceleyeceğiz.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Önceki](adding-a-gridview-column-of-radio-buttons-cs.md)
> [İleri](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
