---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: (C#) verileri temel alan özel biçimlendirme | Microsoft Docs
author: rick-anderson
description: Birden çok yolla biçimi GridView, DetailsView veya kendisine veriye dayalı FormView ayarlayarak gerçekleştirilebilir. Bu öğreticide l geçeriz...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: ee9cdf19769ea63388fd9dd18a82bb2b4dcdef87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066819"
---
<a name="custom-formatting-based-upon-data-c"></a>Verileri Temel Alan Özel Biçimlendirme (C#)
====================
tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) veya [PDF olarak indirin](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)

> Birden çok yolla biçimi GridView, DetailsView veya kendisine veriye dayalı FormView ayarlayarak gerçekleştirilebilir. Bu öğreticide veri bağlama kullanarak veri bağlama ve RowDataBound olay işleyicileri biçimlendirme gerçekleştirmek nasıl şu konuları inceleyeceğiz.


## <a name="introduction"></a>Giriş

FormView GridView ve DetailsView denetimlerini görünümünü stil özellikleri çok özelleştirilebilir. Özellikleri gibi `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, ve `Height`, diğerleriyle birlikte, genel görünümünü işlenen denetimi gerektirir. Özellikler dahil olmak üzere `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, ve diğerleri belirli bölümlerine uygulanacak aynı bu stilini ayarlar sağlar. Benzer şekilde, bu stil ayarları alan düzeyinde uygulanabilir.

Pek çok senaryoda biçimlendirme gereksinimleri görüntülenen verileri değerinin yine de bağlıdır. Örneğin, / ürünleri hisse senedi için dikkat çekmek için ürün bilgileri listeleyen bir rapor bu ürünler için ayarlanmış sarı arka plan rengini ayarlayabilirsiniz `UnitsInStock` ve `UnitsOnOrder` alanları her ikisi de 0'a eşit. Daha pahalı ürünleri vurgulamak için Biz bu ürünlerin birden fazla $75.00 kalın yazı tipinde maliyeti fiyatları görüntülemek isteyebilirsiniz.

Birden çok yolla biçimi GridView, DetailsView veya kendisine veriye dayalı FormView ayarlayarak gerçekleştirilebilir. Bu öğreticide ilişkili veri kullanımının biçimlendirme gerçekleştirmek nasıl inceleyeceğiz `DataBound` ve `RowDataBound` olay işleyicileri. Sonraki öğreticide, alternatif bir yaklaşım şunları keşfedeceğiz.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView denetimin kullanarak`DataBound`olay işleyicisi

Ne zaman veri bağlı bir DetailsView için verileri kaynak denetiminden veya program aracılığıyla veri denetimin atama aracılığıyla `DataSource` özelliği ve arama kendi `DataBind()` yöntemi, aşağıdaki adımlar dizisini oluşur:

1. Veri Web denetimi `DataBinding` olay harekete geçirilir.
2. Veri Web denetimi verilere bağlıdır.
3. Veri Web denetimi `DataBound` olay harekete geçirilir.

Adım 1 ve 3 olay işleyicisi ile hemen sonra özel mantığı yerleştirilebilir. Bir olay işleyicisi için oluşturarak `DataBound` olay biz programlı olarak belirleyebilir yapılmış veriler veri Web denetime bağlı ve biçimlendirmesini gereken şekilde ayarlayın. Bunu şimdi göstermek için bir ürünle ilgili genel bilgiler listelenir, ancak görüntüleyecek bir DetailsView oluşturma `UnitPrice` değerini bir ***kalın, italik yazı tipi*** $75.00 aşarsa.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>1. Adım: Bir DetailsView ürün bilgilerini görüntüleme

Açık `CustomColors.aspx` sayfasını `CustomFormatting` klasörü, tasarımcı araç kutusundan bir DetailsView denetimi sürükleyin, ayarla, `ID` özellik değerini `ExpensiveProductsPriceInBoldItalic`ve çağıran yeni bir ObjectDataSource denetimine bağlama `ProductsBLL` sınıfın `GetProducts()` yöntemi. Biz bunları önceki öğreticilerdeki ayrıntılı olarak incelenir olduğundan bu işlemi gerçekleştirmek için ayrıntılı adımlar burada uzatmamak için göz ardı edilir.

ObjectDataSource için DetailsView bağladınız sonra alan listesini değiştirmek için bir dakikanızı ayırın. Kaldırma bıraktınız `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, ve `Discontinued` BoundFields ve yeniden adlandırılabilir ve kalan BoundFields yeniden biçimlendirildi. Ben ayrıca temizlenmiş `Width` ve `Height` ayarları. DetailsView yalnızca tek bir kaydı görüntüler olduğundan, disk belleği tüm ürünleri görüntülemek son kullanıcı izin vermek için etkinleştirmeniz gerekir. DetailsView'ın akıllı etiket sayfalama etkinleştir onay kutusunu işaretleyerek bunu yapar.


[![DetailsView'ın akıllı etiket etkin disk belleği onay kutusunu işaretleyin](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)

**Şekil 1**: Etkinleştirme sayfalama DetailsView'ın akıllı etiketinde onay ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image3.png))


Bu değişikliklerden sonra DetailsView biçimlendirme olacaktır:


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

Bu sayfası tarayıcınızda test etmek için bir dakikanızı ayırın.


[![DetailsView denetiminde bir ürün teker teker gösterir.](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)

**Şekil 2**: DetailsView denetimi görüntüler bir ürün birer birer ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image6.png))


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>2. Adım: Program aracılığıyla veri DataBound olay işleyicisinde değerini belirleme

Bu ürünler için kalın, italik yazı tipinde fiyat görüntülemek için `UnitPrice` değerini aşan $75.00, ilk program aracılığıyla belirlemek mümkün olması için ihtiyacımız `UnitPrice` değeri. DetailsView için bu içinde gerçekleştirilebilir `DataBound` olay işleyicisi. Olay oluşturmak için işleyici DetailsView Tasarımcısı'nda tıklatın ardından özellikleri penceresine gidin. Görünür veya Görünüm menüsü Git değilse, getirecek için F4 tuşuna basın ve Özellikler penceresinde menü seçeneğini belirleyin. Özellikler penceresinden DetailsView'ın olaylarını listelemek için ışık Şimşek simgesine tıklayın. Ardından, ya da çift `DataBound` olay veya olay işleyicisi oluşturmak istediğiniz adını yazın.


![Veriye bağlı olayı için olay işleyicisi oluşturun](custom-formatting-based-upon-data-cs/_static/image7.png)

**Şekil 3**: İçin bir olay işleyicisi oluşturun `DataBound` olay


Bunun yapılması otomatik olarak olay işleyicisi oluşturun ve burada eklenmiş kod bölümüne katılın. Bu noktada görürsünüz:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

DetailsView için veriye erişilebilir `DataItem` özelliği. Bizim denetimleri kesin türü belirtilmiş DataRow örneklerinin bir koleksiyonunu oluşan bir kesin türü belirtilmiş DataTable öğesine, bağlıyorsanız geri çağırma. DataTable DetailsView için bağlı olduğunda, ilk DataRow DataTable DetailsView için 's atanır `DataItem` özelliği. Özellikle, `DataItem` özelliği atandığında bir `DataRowView` nesne. Kullanabiliriz `DataRowView`'s `Row` özelliği erişmek için kullanılan temel alınan DataRow nesne, aslında bir `ProductsRow` örneği. Biz bunu aldıktan sonra `ProductsRow` biz yapabilir karar nesnenin özellik değerlerini inceleyerek örneği.

Aşağıdaki kod nasıl belirleneceğini göstermektedir olmadığını `UnitPrice` DetailsView denetime bağlı değeri 75.00 büyük:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> Bu yana `UnitPrice` olabilir bir `NULL` değer veritabanında ilk kontrol ediyoruz ile ilgilenemezsiniz emin olmak için bir `NULL` erişmeden önce değer `ProductsRow`'s `UnitPrice` özelliği. Bu onay önemlidir çünkü erişmeye çalışırsanız `UnitPrice` özelliğine sahip bir `NULL` değer `ProductsRow` nesnesi oluşturur bir [StrongTypingException özel durum](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>3. Adım: DetailsView UnitPrice değerini biçimlendirme

Bu noktada belirleyebiliriz olmadığını `UnitPrice` DetailsView için bağlı değerini aşan $75.00 değerine sahip, ancak henüz DetailsView programlama yoluyla ayarlama konusunda görmek için uygun şekilde formatını yaptıklarımız. DetailsView tüm bir satırda biçimini değiştirmek için program aracılığıyla satır erişebileceğiniz `DetailsViewID.Rows[index]`; belirli bir hücre değiştirmek için kullandığı erişimi `DetailsViewID.Rows[index].Cells[index]`. Satır veya hücre bir başvuru sahibiz sonra stil özelliklerini ayarlayarak biz ardından görünümünü ayarlayabilirsiniz.

Bir satır program aracılığıyla erişme, sıranın dizini, 0'da başlar bilmeniz gerekir. `UnitPrice` Satırdır 4 dizinini ayırabilir ve programlı olarak erişilebilir yaparak DetailsView beşinci satırda kullanarak `ExpensiveProductsPriceInBoldItalic.Rows[4]`. Bu noktada size aşağıdaki kodu kullanarak kalın, italik yazı tipiyle gösterilen tüm sıranın içeriğe sahip:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

Ancak, bu yapacak *hem* (Fiyat) etiketi ve değerini kalın ve italik. Biz sadece biz bunu uygulamanız gerekiyorsa, aşağıdaki kullanılarak gerçekleştirilebilir satırın ikinci hücresinde biçimlendirme değer kalın ve italik hale getirmek isterseniz:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

Öğreticilerimizden şimdiye kadarki bilgi stil ve biçimlendirmenin arasında NET bir ayrım sağlamak için stil sayfaları kullanmış olduğundan, yukarıda şimdi bunun yerine gösterildiği gibi belirli stil özelliklerini ayarlama yerine bir CSS sınıfını kullanın. Açık `Styles.css` stil sayfası ve adlı yeni bir CSS sınıfı Ekle `ExpensivePriceEmphasis` aşağıdaki tanımıyla:


[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

Ardından `DataBound` olay işleyicisi, hücre kümesi `CssClass` özelliğini `ExpensivePriceEmphasis`. Aşağıdaki kodda gösterildiği `DataBound` izlediğimizi olay işleyicisi:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

Küçüktür $75.00 maliyetleri, Chai, görüntülerken fiyatı normal bir yazı tipi görüntülenir (bkz: Şekil 4). Ancak, $97.00 fiyatı olan Mishi Kobe Niku görüntülerken fiyat kalın, italik yazı tipinde görüntülenir (bkz: Şekil 5).


[![Normal yazı tipinde $75.00 sayısından az fiyatları görüntülenir](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)

**Şekil 4**: Normal yazı tipinde $75.00 sayısından az fiyatları görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image10.png))


[![Pahalı ürünleri fiyatları bir kalın, italik yazı tipi görüntülenir](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)

**Şekil 5**: Pahalı ürünleri fiyatları bir kalın, italik yazı tipi görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image13.png))


## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView denetimin kullanarak`DataBound`olay işleyicisi

Bir DetailsView oluşturmanız için bir FormView'da bağlı temel alınan verileri belirlemek için adımları aynıdır bir `DataBound` olay işleyicisi cast `DataItem` uygun nesne türü özelliğine denetime bağlı ve devam etmek belirleme. FormView ve DetailsView, ancak kendi kullanıcı arabiriminin görünümünü nasıl güncelleştirileceğini farklı.

FormView herhangi BoundFields içermiyor ve bu nedenle eksik `Rows` koleksiyonu. Bir FormView'da statik HTML bir karışımını içerebilir, şablonlar bunun yerine, oluşan Web denetimleri ve veri bağlama söz dizimi. Bir FormView'da stilini genellikle ayarlama, bir veya daha fazla Web denetimleri FormView şablonları içinde stilini ayarlama içerir.

Bunu göstermek için şimdi bir FormView'da ürünleri listeler için önceki örnekte, ancak bu kez şimdi gibi kullanın yalnızca ürün adı ve birimler 10'a eşit veya daha az ise kırmızı bir yazı tipinde görüntülenen stoktaki birimleri ile stoktaki.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>4. Adım: Bir FormView'da ürün bilgilerini görüntüleme

Bir FormView'da için ekleme `CustomColors.aspx` sayfa kümesi ve DetailsView altında kendi `ID` özelliğini `LowStockedProductsInRed`. FormView ObjectDataSource Denetimi önceki adımda oluşturulan bağlayın. Bu oluşturacak bir `ItemTemplate`, `EditItemTemplate`, ve `InsertItemTemplate` FormView için. Kaldırma `EditItemTemplate` ve `InsertItemTemplate` ve basitleştirmek `ItemTemplate` içerecek şekilde yalnızca `ProductName` ve `UnitsInStock` değerleri, her biri kendi uygun şekilde adlı etiket denetimleri. DetailsView gibi önceki örnekte ile başka bir işlem de FormView akıllı etiketinde sayfalama etkinleştir onay kutusunu işaretleyin.

Sonra bu düzenlemeler, FormView biçimlendirme aşağıdakine benzer görünmelidir:


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

Unutmayın `ItemTemplate` içerir:

- **Statik HTML** metni "Ürün:" ve "stoktaki birimler:" ile birlikte `<br />` ve `<b>` öğeleri.
- **Web denetimleri** iki etiket denetimleri `ProductNameLabel` ve `UnitsInStockLabel`.
- **Veri bağlama söz dizimi** `<%# Bind("ProductName") %>` ve `<%# Bind("UnitsInStock") %>` değerlerini bu alanlardan etiket denetimlerine atar. söz dizimi `Text` özellikleri.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>5. Adım: Program aracılığıyla veri DataBound olay işleyicisinde değerini belirleme

Tam FormView biçimlendirme ile programlı olarak belirlemek için sonraki adım olan `UnitsInStock` değer 10 küçüktür veya eşittir. DetailsView ile olduğu gibi bu FormView ile tam olarak aynı şekilde gerçekleştirilir. FormView için bir olay işleyicisi oluşturarak başlayın `DataBound` olay.


![Veri bağlama olay işleyicisi oluşturun](custom-formatting-based-upon-data-cs/_static/image14.png)

**Şekil 6**: Oluşturma `DataBound` olay işleyicisi


Olay işleyicisi FormView cast `DataItem` özelliğini bir `ProductsRow` belirlemek ve örnek olup olmadığını `UnitsInPrice` değerdir kırmızı bir yazı tipinde görüntülenecek ihtiyacımız olacak şekilde.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>6. Adım: FormView ItemTemplate UnitsInStockLabel etiket denetiminde biçimlendirme

Görüntülenen biçimlendirmek için son adımdır `UnitsInStock` değer 10 veya daha az ise kırmızı bir yazı tipinde değeri. Bu program aracılığıyla erişmek için ihtiyacımız gerçekleştirmek için `UnitsInStockLabel` denetim `ItemTemplate` ve metin kırmızı renkte gösterilir böylece stil özelliklerini ayarlayın. Bir Web Denetim şablonunda erişmek için `FindControl("controlID")` şöyle yöntemi:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

Bizim örneğimizde istediğimiz bir etiket erişmek için ayarlanmış denetim `ID` değer `UnitsInStockLabel`, kullanmanız gerekir:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

Biz Web denetimi için bir programlama başvurusu oluşturduktan sonra biz stil özelliklerini gerektiği gibi değiştirebilirsiniz. Önceki örnekte, bir CSS sınıfı oluşturduğum gibi `Styles.css` adlı `LowUnitsInStockEmphasis`. Bu stil etiketi Web denetime uygulamak için ayarlanmış kendi `CssClass` özelliği uygun şekilde.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> Bir şablon kullanarak Web denetimi program aracılığıyla erişme biçimlendirme sözdizimi `FindControl("controlID")` ve ardından stil özelliklerini ayarlayarak da kullanılabilir kullanırken [TemplateField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView veya GridView denetimler. Sonraki müşterilerimize öğreticide TemplateField inceleyeceğiz.


Şekil 7, bir ürün görüntülerken FormView gösterir, `UnitsInStock` Şekil 8'deki ürün 10 küçüktür değerine sahipken değer 10'dan büyük.


[![Ürünleri ile bir yeterince büyük stoktaki için özel biçimlendirme yok uygulanır](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)

**Şekil 7**: Ürünleri ile bir yeterince büyük stoktaki için özel biçimlendirme yok uygulanır ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image17.png))


[![Hisse senedi numarası birimlerinde bu ürünleri ile değerleri için 10 veya daha az kırmızı renkte gösterilir](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)

**Şekil 8**: Hisse senedi numarası birimlerinde bu ürünleri ile değerleri için 10 veya daha az kırmızı renkte gösterilir ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image20.png))


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>GridView'ile ın biçimlendirme`RowDataBound`olay

Daha önce size bir dizi adımdan DetailsView incelendi ve FormView veri bağlama sırasında ilerlemeyi denetler. Üzerinde aşağıdaki adımları yine Yenileyici bakalım.

1. Veri Web denetimi `DataBinding` olay harekete geçirilir.
2. Veri Web denetimi verilere bağlıdır.
3. Veri Web denetimi `DataBound` olay harekete geçirilir.

Bunlar tek bir kayıt görüntülemek için aşağıdaki üç basit adımda DetailsView ve FormView için yeterlidir. GridView için görüntüleyen *tüm* bağlı kayıtları kendisine (yalnızca ilk), 2. adım biraz daha karmaşıktır.

GridView veri kaynağı numaralandırır ve her bir kayıt oluşturur. 2. adımda bir `GridViewRow` örneği ve geçerli kayıt bağlar. Her `GridViewRow` GridView'a eklendi, iki olaylar oluşturulur:

- **`RowCreated`** sonra ateşlenir `GridViewRow` oluşturuldu
- **`RowDataBound`** Geçerli kayıt için bağlı sonra ateşlenir `GridViewRow`.

GridView için daha sonra veri bağlama daha doğru bir şekilde aşağıdaki adımlar dizisini açıklanmaktadır:

1. GridView'ın `DataBinding` olay harekete geçirilir.
2. Veri GridView'a bağlıdır.   
  
   Her kayıt için veri kaynağı 

    1. Oluşturma bir `GridViewRow` nesnesi
    2. Ateş `RowCreated` olay
    3. Kaydına bağlama `GridViewRow`
    4. Ateş `RowDataBound` olay
    5. Ekleme `GridViewRow` için `Rows` koleksiyonu
3. GridView'ın `DataBound` olay harekete geçirilir.

GridView'ın tek tek kayıtlar biçimini özelleştirmek için daha sonra bir olay işleyicisi oluşturmak ihtiyacımız `RowDataBound` olay. Bunu açıklamak üzere; GridView'a ekleyelim `CustomColors.aspx` ad, kategori ve fiyatı olan küçüktür $10,00 sarı arka plan rengiyle bu ürünlere vurgulama, her ürünün fiyatını listeleyen sayfası.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>7. Adım: GridView ürün bilgilerini görüntüleme

Önceki örnekte FormView altındaki GridView ekleme ve kendi `ID` özelliğini `HighlightCheapProducts`. Sayfada tüm ürünleri döndüren bir ObjectDataSource biz zaten olduğundan, GridView olarak bağlayın. Son olarak, GridView'ın BoundFields yalnızca ürünlerin adlarını, kategoriler ve fiyatlar içerecek şekilde düzenleyin. Sonra bu düzenlemeler GridView'ın biçimlendirme gibi görünmelidir:


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

Şekil 9 bir tarayıcıdan görüntülendiğinde bu noktaya ilerleme gösterir.


[![GridView ad, kategori ve her ürün için fiyat listeleri](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)

**Şekil 9**: GridView ad, kategori ve her ürün için fiyat listeleri ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image23.png))


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>8. Adım: Program aracılığıyla veri RowDataBound olay işleyicisinde değerini belirleme

Zaman `ProductsDataTable` GridView'a bağlı kendi `ProductsRow` örnekleridir listelenmiş ve her biri için `ProductsRow` bir `GridViewRow` oluşturulur. `GridViewRow`'S `DataItem` özelliği, belirli atandığı `ProductRow`, sonrasında GridView'ın `RowDataBound` olay işleyicisi oluşturulur. Belirlemek için `UnitPrice` GridView'a sınır değeri her ürün için sonra GridView için ait bir olay işleyicisi oluşturmak ihtiyacımız `RowDataBound` olay. Bu olay işleyicisinde biz inceleyebilirsiniz `UnitPrice` için geçerli değer `GridViewRow` ve ilgili satır için biçimlendirme bir karar.

Bu olay işleyicisi DetailsView ve FormView ile aynı dizi adımları kullanarak oluşturulabilir.


![GridView'ın RowDataBound olayı için olay işleyicisi oluşturun](custom-formatting-based-upon-data-cs/_static/image24.png)

**Şekil 10**: GridView için ait bir olay işleyicisi oluşturun `RowDataBound` olay


Bu olay işleyicisi oluşturmak için ASP.NET sayfa kod bölümü otomatik olarak eklenmesi için aşağıdaki kodu neden olur:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

Zaman `RowDataBound` olayı tetiklendiğinde, olay işleyicisine geçirilir, ikinci parametre olarak bir nesne türü `GridViewRowEventArgs`, adlı bir özellik olan `Row`. Bu özellik bir başvuru döndürür `GridViewRow` yalnızca veri bağımlı olduğu. Erişim için `ProductsRow` örneği bağlı `GridViewRow` kullandığımız `DataItem` özelliği şu şekilde:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

İle çalışırken `RowDataBound` GridView satır farklı türde oluşan ve bu olay harekete geçirilen aklınızda bulundurun önemlidir olay işleyicisi *tüm* satır türleri. A `GridViewRow`ın türü tarafından belirlenebilir kendi `RowType` özelliği ve değerlerden biri olabilir:

- `DataRow` bir kayda GridView ' ın bağlı olduğu bir satır `DataSource`
- `EmptyDataRow` görüntülenen satır GridView'ın `DataSource` boş
- `Footer` Alt satır; gösterilen if GridView'ın `ShowFooter` özelliği `true`
- `Header` üst bilgi satırı; GridView'ın ShowHeader özelliği ayarlanırsa gösterilen `true` (varsayılan)
- `Pager` GridView için 's, disk belleği, disk belleği arabirimini görüntüler satır uygulayın.
- `Separator` GridView için kullanılmaz, ancak tarafından kullanılan `RowType` özelliklerini DataList ve Repeater denetimleri, iki veri Web denetimleri ele gelecekte öğreticiler

Bu yana `EmptyDataRow`, `Header`, `Footer`, ve `Pager` satır ile ilişkili olmayan bir `DataSource` kayıt, bunlar her zaman sahip olur bir `null` değerini kendi `DataItem` özelliği. Geçerli çalışma çalışmadan önce bu nedenle `GridViewRow`'s `DataItem` özelliği, biz öncelikle biz ile ilgilenen emin emin olmalısınız bir `DataRow`. Bu kontrol ederek gerçekleştirilebilir `GridViewRow`'s `RowType` özelliği şu şekilde:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>9. Adım: Küçüktür $10,00 olan satır sarı olduğunda UnitPrice değeri vurgulama

Tüm program aracılığıyla vurgulamak için son adımdır `GridViewRow` varsa `UnitPrice` satır küçüktür $10,00 değeri. GridView'ın satır veya hücre erişmek için söz dizimi olarak DetailsView ile aynı olup `GridViewID.Rows[index]` tüm satırı erişmeye `GridViewID.Rows[index].Cells[index]` belirli bir hücre erişmek için. Ancak, `RowDataBound` olay işleyicisi, veri bağlama harekete `GridViewRow` henüz GridView'ın eklenmesi gereken `Rows` koleksiyonu. Geçerli etkinleştirilemez `GridViewRow` gelen örnek `RowDataBound` satır koleksiyonu kullanarak olay işleyicisi.

Yerine `GridViewID.Rows[index]`, biz geçerli başvurabilirsiniz `GridViewRow` örneğini `RowDataBound` kullanarak olay işleyicisi `e.Row`. Geçerli vurgulamak için diğer bir deyişle, giriş sırası `GridViewRow` gelen örnek `RowDataBound` olay işleyicisi kullanırız:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

Yerine ayarlamak `GridViewRow`'s `BackColor` özelliği doğrudan şimdi CSS sınıfları kullanmaya da devam edin. Adlı bir CSS sınıfı oluşturduğum `AffordablePriceEmphasis` sarı arka plan rengini ayarlar. Tamamlanan `RowDataBound` olay işleyicisi izler:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]


[![Sarı vurgulanmış olan en uygun maliyetli ürünler](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)

**Şekil 11**: En uygun maliyetli ürünleri vurgulanmış sarı, ([tam boyutlu görüntüyü görmek için tıklatın](custom-formatting-based-upon-data-cs/_static/image27.png))


## <a name="summary"></a>Özet

Bu öğreticide GridView DetailsView ve FormView denetime bağlı verileri temel alan biçimlendirme gördük. Bir olay işleyicisi için oluşturduğumuz bunu sağlamak için `DataBound` veya `RowDataBound` burada temel alınan verileri incelenirken biçimlendirme bir değişiklikle birlikte, gerekirse olayları. Bir DetailsView veya FormView bağlı verilere erişmek için kullanırız `DataItem` özelliğinde `DataBound` olay işleyicisi, GridView için; her `GridViewRow` örneğinin `DataItem` özelliği içindekullanılabilir,satırbağlıverileriiçerir`RowDataBound` olay işleyicisi.

Veri Web denetimin biçimlendirme programlı olarak ayarlamak için söz dizimi Web denetimi ve Biçimlendirilecek verilerin nasıl görüntüleneceğini bağlıdır. DetailsView ve GridView denetimleri, satır ve hücre bir sıra dizini tarafından erişilebilir. FormView şablonları kullanan için `FindControl("controlID")` yöntemi şablonu içindeki bir Web denetimi bulmak için yaygın olarak kullanılır.

Sonraki öğreticide şablonları GridView ve DetailsView ile nasıl kullanılacağını şu konuları inceleyeceğiz. Ayrıca, temel alınan verileri temel alan biçimlendirme özelleştirmek için başka bir teknik göreceğiz.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğretici için müşteri adayı gözden geçirenler E.R. olan Gilmore, Dennis Patterson ve Can Jagers. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](using-templatefields-in-the-gridview-control-cs.md)
