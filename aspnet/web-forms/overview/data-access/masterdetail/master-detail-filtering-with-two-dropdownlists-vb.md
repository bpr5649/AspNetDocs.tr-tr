---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: Ana/ayrıntı filtreleme (VB) iki DropDownList ile | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, istenen üst ve doya recor seçmek için iki DropDownList denetimi kullanarak, bir üçüncü katman eklemek için ana/ayrıntı ilişkisi genişletir...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: a9a76a960952b34138424bff1735a4ea93d2bfa2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65109193"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>İki DropDownList ile Ana/Ayrıntı Filtreleme (VB)

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe) veya [PDF olarak indirin](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> Bu öğreticide, istenen üst ve doya kayıtları seçmek için iki DropDownList denetimi kullanarak, bir üçüncü katman eklemek için ana/ayrıntı ilişkisi genişletir.

## <a name="introduction"></a>Giriş

İçinde [önceki öğreticide](master-detail-filtering-with-a-dropdownlist-vb.md) biz kategorileri ve seçilen bir kategoriye ait bu ürünlerin gösteren GridView doldurulmuş tek bir DropDownList kullanarak bir basit ana/ayrıntılar raporu görüntülemek nasıl incelenir. Bu rapor düzeni, bire çok ilişkisi vardır ve birden çok-çok ilişkileri içeren senaryolar için çalışmak için kolayca genişletilebilir kayıtları görüntülenirken iyi çalışır. Örneğin, bir sipariş girişi sistemi müşteri, sipariş ve sipariş satır öğesi için karşılık gelen bir tablo gerekir. Belirli bir müşteri, birden çok öğelerinden oluşan her sipariş birden çok siparişler olabilir. Bu tür veriler, kullanıcıya iki DropDownList ve GridView sunulabilir. İlk DropDownList ikinci veritabanındaki her müşteri için bir liste öğesi olur birinin içeriği Seçilen müşteri tarafından yerleştirilen siparişler oluşturuluyor. GridView satır öğeleri seçili siparişi listesi.

Northwind veritabanı içerirken kurallı müşteri / / sipariş ayrıntıları bilgilerinde kendi `Customers`, `Orders`, ve `Order Details` tablolar, bu tablolar mimarimiz içinde yakalanan değildir. Öte yandan, size iki bağımlı DropDownList kullanarak yine de gösterebilirsiniz. İlk DropDownList kategorileri ve ikinci Seçili kategoriye ait olan ürünleri listeler. Bir DetailsView sonra seçili ürün ayrıntılarını listeler.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>1. Adım: Oluşturma ve kategorilere DropDownList doldurma

İlk Hedefimiz kategorileri listeler DropDownList eklemektir. Bu adımlar önceki öğreticide ayrıntılı olarak incelenir, ancak bütünlük açısından buraya özetlenmiştir.

Açık `MasterDetailsDetails.aspx` sayfasını `Filtering` sayfasına bir DropDownList ekleme klasörü ayarlayın, `ID` özelliğini `Categories`ve ardından akıllı etiketinde veri kaynağı yapılandırma bağlantıya tıklayın. Yeni bir veri kaynağı eklemek veri kaynağı Yapılandırma Sihirbazı'nı seçin.

[![Bir DropDownList için yeni bir veri kaynağı Ekle](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**Şekil 1**: Yeni bir veri kaynağı için DropDownList ekleyin ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png))

Doğal olarak, yeni veri kaynağı bir ObjectDataSource olmalıdır. Bu yeni ObjectDataSource ad `CategoriesDataSource` ve çağırma `CategoriesBLL` nesnenin `GetCategories()` yöntemi.

[![CategoriesBLL sınıfını kullanmak seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**Şekil 2**: Use yöntemine seçin `CategoriesBLL` sınıfı ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png))

[![ObjectDataSource GetCategories() yöntemi kullanmak üzere yapılandırma](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**Şekil 3**: ObjectDataSource kullanılacak yapılandırma `GetCategories()` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png))

ObjectDataSource yapılandırdıktan sonra hala hangi veri kaynağı alanın görüntüleneceğini belirtmek ihtiyacımız `Categories` DropDownList ve hangisinin liste öğesi için bir değer olarak yapılandırılması gerekir. Ayarlama `CategoryName` görüntü olarak alan ve `CategoryID` değeri her liste öğesi olarak.

[![CategoryName alan ve kullanım CategoryID DropDownList görünen değere sahip](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**Şekil 4**: DropDownList görüntülemesi `CategoryName` alan ve kullanım `CategoryID` değeri ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png))

Bir DropDownList denetimi bu noktada sahibiz (`Categories`) kayıtları ile doldurulmuş `Categories` tablo. Kullanıcı DropDownList'e yeni kategori seçtiğinde biz biz 2. adımda oluşturacağız DropDownList ürün yenilemek için gerçekleşecek bir geri gönderme istersiniz. Bu nedenle, AutoPostBack Etkinleştir seçeneği denetleyin `categories` DropDownList'ın akıllı etiket.

[![Povolit vlastnost AutoPostBack için kategorileri DropDownList](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**Şekil 5**: Povolit vlastnost AutoPostBack için `Categories` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>2. Adım: Seçilen kategorinin ürün içinde ikinci bir DropDownList görüntüleme

İle `Categories` DropDownList tamamlandı, sonraki adımımız, seçilen kategoriye ait olan ürünlerin bir DropDownList görüntülemektir. Bunu gerçekleştirmek için başka bir DropDownList adlı sayfasına ekleme `ProductsByCategory`. Olduğu gibi `Categories` DropDownList, oluşturmak için yeni bir ObjectDataSource `ProductsByCategory` adlı DropDownList `ProductsByCategoryDataSource`.

[![Yeni veri kaynağı için ProductsByCategory DropDownList Ekle](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**Şekil 6**: İçin yeni bir veri kaynağı Ekle `ProductsByCategory` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png))

[![ProductsByCategoryDataSource adlı yeni bir ObjectDataSource oluşturma](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**Şekil 7**: Adlı yeni bir ObjectDataSource oluşturma `ProductsByCategoryDataSource` ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png))

Bu yana `ProductsByCategory` Seçili kategoriye ait yalnızca ürünleri görüntülemek üzere DropDownList ihtiyaçları olan çağırma ObjectDataSource `GetProductsByCategoryID(categoryID)` yönteminden `ProductsBLL` nesne.

[![ProductsBLL sınıfını kullanmak seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**Şekil 8**: Use yöntemine seçin `ProductsBLL` sınıfı ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png))

[![ObjectDataSource GetProductsByCategoryID(categoryID) yöntemi kullanmak üzere yapılandırma](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**Şekil 9**: ObjectDataSource kullanılacak yapılandırma `GetProductsByCategoryID(categoryID)` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png))

Değeri belirtmek ihtiyacımız sihirbazının son adımı *`categoryID`* parametresi. Bu parametre, seçili öğenin atayın `Categories` DropDownList.

[![Parametre değeri CategoryID kategorileri DropDownList çekme](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**Şekil 10**: Çekme *`categoryID`* parametresi değerinden `Categories` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png))

ObjectDataSource ile yapılandırılmış kalan tek şey görünen ve DropDownList'ın öğe değerini için hangi veri kaynağı alanları kullanılan belirtmek için. Görüntü `ProductName` kullanın ve alan `ProductID` değeri alanı.

[![DropDownList'ın ListItems metin ve değer özellikleri için kullanılan veri kaynağı alanları belirtin](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**Şekil 11**: Veri kaynağı alanları kullanılan DropDownList için 's belirtin `ListItem` s' `Text` ve `Value` özellikleri ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png))

ObjectDataSource ile ve `ProductsByCategory` DropDownList sayfamızı yapılandırılmış iki DropDownList görüntülenir: ikinci Seçili kategoriye ait olan bu ürünlerin listeler sırasında ilk kategorilerin tümünü listeler. Kullanıcı ilk DropDownList'e yeni kategori seçtiğinde, bir geri gönderme ardından ve ikinci DropDownList, yeni seçilen kategoriye ait bu ürünlerin gösteren DataSet'e. Şekil 12 ve 13 show `MasterDetailsDetails.aspx` uygulamada bir tarayıcı üzerinden görüntülenebilir.

[![Sayfa ilk ziyaret edildiğinde, İçecekler kategorisindeki seçili](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**Şekil 12**: Sayfa ilk ziyaret edildiğinde, İçecekler kategorisindeki seçilir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png))

[![Farklı bir kategori seçerek yeni kategori ürünleri görüntüler](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**Şekil 13**: Farklı bir kategori görüntüler yeni kategorinin ürün seçme ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png))

Şu anda `productsByCategory` değiştirildiğinde DropDownList mu *değil* bir geri göndermeye neden olur. Ancak, (3. adım) seçili ürünün ayrıntılarını görüntülemek için bir DetailsView eklediğimiz sonra gerçekleşecek bir geri gönderme istiyoruz. Bu nedenle, etkinleştirme AutoPostBack gelen onay `productsByCategory` DropDownList'ın akıllı etiket.

[![DropDownList productsByCategory AutoPostBack özelliğini etkinleştir](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**Şekil 14**: Vlastnost AutoPostBack özelliğini etkinleştirme `productsByCategory` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>3. Adım: Seçili ürün için ayrıntıları görüntülemek için bir DetailsView kullanma

Son adım, bir DetailsView içinde seçili ürün ayrıntılarını görüntülemektir. Bunu başarmak eklemek için bir DetailsView sayfasına ayarlayın, `ID` özelliğini `ProductDetails`ve yeni ObjectDataSource oluşturun. Kendi verileri çekmek için bu ObjectDataSource yapılandırma `ProductsBLL` sınıfın `GetProductByProductID(productID)` seçili değerini kullanarak yöntemini `ProductsByCategory` DropDownList değerini *`productID`* parametresi.

[![ProductsBLL sınıfını kullanmak seçin](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**Şekil 15**: Use yöntemine seçin `ProductsBLL` sınıfı ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png))

[![ObjectDataSource GetProductByProductID(productID) yöntemi kullanmak üzere yapılandırma](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**Şekil 16**: ObjectDataSource kullanılacak yapılandırma `GetProductByProductID(productID)` yöntemi ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png))

[![Parametre değeri ProductID ProductsByCategory DropDownList çekme](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**Şekil 17**: Çekme *`productID`* parametresi değerinden `ProductsByCategory` DropDownList ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png))

Herhangi bir kullanılabilir alanları görüntülemek seçebileceğiniz `ProductDetails` DetailsView. Kaldırma bıraktınız `ProductID`, `SupplierID`, ve `CategoryID` alanları ve yeniden geri kalan alanları biçimlendirilmiş. Ayrıca, ı DetailsView ait temizlenmiş `Height` ve `Width` DetailsView verilerini yerine belirtilen boyutu kısıtlı genişliği en iyi görüntü için gereken şekilde genişletmek izin verme özellikler. Aşağıda, tam biçimlendirme görünür:

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

Denemek için birkaç dakikanızı `MasterDetailsDetails.aspx` sayfasını bir tarayıcıda. İlk bakışta her şeyin istendiği gibi çalıştığından, ancak ince bir sorun olduğu görünebilir. Yeni bir kategori seçtiğinizde `ProductsByCategory` DropDownList, seçilen kategori için bu ürünlerin içerecek şekilde güncelleştirilir ancak `ProductDetails` DetailsView devamı olan önceki ürün bilgileri gösterecek şekilde. DetailsView, seçilen kategori için farklı bir ürünü seçerken güncelleştirilir. Yeterince baştan sona test edin, sürekli olarak yeni bir kategori seçerseniz Ayrıca, bulabilirsiniz (gelen İçecekler seçme gibi `Categories` DropDownList sonra Çeşniler, ardından Confections) her bir kategori seçimi neden`ProductDetails`DetailsView yenilenecek.

Bu sorunu concretize yardımcı olmak için belirli bir örneğe bakalım. Sayfa ilk ziyaret edildiğinde İçecekler kategorisindeki seçilir ve ilgili ürünler yüklenen `ProductsByCategory` DropDownList. Chai seçili ürün ve ayrıntılarını görüntülenen `ProductDetails` Şekil 18'de gösterildiği gibi DetailsView.

[![Bir DetailsView içinde seçili ürün ayrıntıları görüntülenir](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**Şekil 18**: Bir DetailsView içinde seçili ürün ayrıntıları görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png))

Çeşniler için İçecekler kategori seçimi değiştirirseniz, bir geri gönderme gerçekleşir ve `ProductsByCategory` DropDownList buna uygun olarak güncelleştirilir ancak DetailsView ayrıntılarını hala ayrıntılarını görüntüler.

[![Daha önce seçilen ürün uygulamasının Ayrıntılar hala görüntülenir](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**Şekil 19**: Daha önce seçilen ürün uygulamasının Ayrıntılar hala görüntülenir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png))

Yeni ürün listesinden çekme DetailsView beklendiği gibi yeniler. Ürün değiştirdikten sonra yeni bir kategori seçerseniz DetailsView tekrar yenileyin olmaz. Ancak, yeni bir ürün seçmek yerine yeni bir kategori seçtiyseniz, DetailsView yeniler. Dünyadaki ne anlama geliyor?

Sorun sayfa yaşam döngüsü bir zamanlama sorunundan kaynaklanır. Her bir sayfa birkaç adım olarak, işleme üzerinden geçer istenir. ObjectDataSource varsa denetleyin denetleyen aşağıdaki adımlardan birini kendi `SelectParameters` değerleri değişti. Veri Web denetimi bu nedenle, bağlı değilse ObjectDataSource görünümünü yenilemek gerektiğini biliyor. Örneğin, yeni bir kategori seçildiğinde, `ProductsByCategoryDataSource` ObjectDataSource parametre değerlerini değiştiğini algılar ve `ProductsByCategory` DropDownList rebinds kendisi için seçilen kategori ürünleri alma.

Bu durumda ortaya ObjectDataSources değiştirilen parametrelerini denetleyin. sayfa yaşam döngüsü noktasında oluştuğunu sorunudur *önce* ilişkili veri Web denetimleri yeniden bağlama. Bu nedenle, yeni bir kategori seçerken `ProductsByCategoryDataSource` ObjectDataSource, parametrenin değeri bir değişikliği algılar. Tarafından kullanılan ObjectDataSource `ProductDetails` DetailsView, ancak değil unutmayın herhangi bir değişiklik nedeniyle `ProductsByCategory` DropDownList olması henüz DataSet'e. Yaşam döngüsü devamındaki `ProductsByCategory` DropDownList rebinds ürünleri yeni seçilen kategori için kapmasını, kendi ObjectDataSource için. Sırada `ProductsByCategory` DropDownList'ın değeri değişti, `ProductDetails` DetailsView'ın ObjectDataSource parametre değeri onay zaten yapmış; bu nedenle, DetailsView önceki sonuçları görüntüler. Bu etkileşimi Şekil 20 gösterilir.

[![Değişiklikleri tazelemek DetailsView'ın ObjectDataSource denendikten sonra ProductsByCategory DropDownList değeri değiştirir.](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**Şekil 20**: `ProductsByCategory` DropDownList değeri değişiklikleri sonra `ProductDetails` değişiklikleri DetailsView'ın ObjectDataSource denetler ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png))

İhtiyacımız açıkça yeniden bağlamak için bu sorunu gidermek için `ProductDetails` DetailsView sonra `ProductsByCategory` DropDownList bağlı. Biz çağırarak gerçekleştirebilirsiniz `ProductDetails` DetailsView'ın `DataBind()` yöntemi zaman `ProductsByCategory` DropDownList'ın `DataBound` olay harekete geçirilir. Aşağıdaki olay işleyici kodu `MasterDetailsDetails.aspx` sayfa arka plan kod sınıfı (başvurun "[ObjectDataSource parametre değerlerini programlı olarak ayarlama](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" bir olay işleyicisi ekleme hakkında bir tartışma için):

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

Bu açık çağrı sonra `ProductDetails` DetailsView'ın `DataBind()` yöntemi eklendi, öğreticiyi beklendiği gibi çalışır. Şekil 21 vurgular nasıl bu değiştirilen bizim önceki sorun gidererek.

[![Tazelemek DetailsView olduğunu açıkça yenilenir olduğunda ProductsByCategory DropDownList's DataBound olay harekete geçirilir](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**Şekil 21**: `ProductDetails` DetailsView olduğunu açıkça yenilendiğinde `ProductsByCategory` DropDownList'ın `DataBound` olay harekete geçirilir ([tam boyutlu görüntüyü görmek için tıklatın](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png))

## <a name="summary"></a>Özet

Ana/ayrıntı raporlar için ideal bir kullanıcı arabirimi öğesi DropDownList Hizmet Yöneticisi ve ayrıntılı kayıtlar arasında bire çok ilişkisi olduğu. Önceki öğreticide seçilen kategoriye göre görüntülenen ürünleri filtrelemek için tek bir DropDownList kullanmayı gördük. Bu öğreticide sunuyoruz GridView ürünlerinin bir DropDownList ile değiştirildi ve bir DetailsView seçili ürün ayrıntılarını görüntülemek için kullanılır. Bu öğreticide açıklanan kavramlar, müşteriler ve siparişler öğeleri sıralama gibi birden çok-çok ilişkileri içeren veri modelleri için kolayca genişletilebilir. Genel olarak, her bir-çok ilişkilerde yer "bir" varlığı için her zaman bir DropDownList ekleyebilirsiniz.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğretici için müşteri adayı İnceleme Hilton Giesenow oluştu. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-with-a-dropdownlist-vb.md)
> [İleri](master-detail-filtering-across-two-pages-vb.md)
