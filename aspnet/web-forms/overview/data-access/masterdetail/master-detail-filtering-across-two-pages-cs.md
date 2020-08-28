---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: Iki sayfada ana/ayrıntı filtreleme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, bir görüntüle içerir...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c7391c1ea7ef33febd4c2344cb40ac788a56034
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045032"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>İki Sayfada Ana/Ayrıntı Filtreleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe) veya [PDF 'yi indirin](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, tıklatıldığında, kullanıcıyı seçili tedarikçi için bu ürünleri listeleyen ayrı bir sayfaya alacak bir görünüm ürünleri bağlantısı içerir.

## <a name="introduction"></a>Giriş

Önceki iki öğreticilerde, "Ayrıntılar" göstermek için ["ana" kayıtları ve bir GridView ya da DetailsView denetimini göstermek](master-detail-filtering-with-two-dropdownlists-cs.md) üzere [dropdownlists kullanarak ana/ayrıntı raporlarının tek bir Web sayfasında nasıl görüntüleneceğini](master-detail-filtering-with-a-dropdownlist-cs.md) gördük. Ana/ayrıntı raporlarında kullanılan diğer yaygın bir düzende, bir Web sayfasında ana kayıtlar ve başka bir sayfada gösterilen ayrıntılar yer alır. [ASP.net forumları](https://forums.asp.net/)gibi bir Forum Web sitesi, uygulamada bu düzenin harika bir örneğidir. ASP.NET forumları, daha fazla Forum, Web Forms, veri sunum denetimleri ve benzeri bir deyişle oluşur. Her Forum birçok iş parçacığından oluşur ve her iş parçacığı bir dizi gönderilerinden oluşur. ASP.NET forumları giriş sayfasında, Forumlar listelenir. Bir foruma tıkladığınızda `ShowForum.aspx` , bu forum için iş parçacıklarını listeleyen bir sayfaya gidin. Benzer şekilde, bir iş parçacığına tıkladığınızda `ShowPost.aspx` tıklamış olan iş parçacığının gönderilerini görüntüleyen ' a gidersiniz.

Bu öğreticide, veritabanındaki tedarikçileri listelemek için GridView kullanarak bu kalıbı uygulayacağız. GridView 'daki her bir tedarikçi satırı, tıklatıldığında, kullanıcıyı seçili tedarikçi için bu ürünleri listeleyen ayrı bir sayfaya alacak bir görünüm ürünleri bağlantısı içerir.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>1. Adım: `SupplierListMaster.aspx` klasöre ekleme ve `ProductsForSupplierDetails.aspx` sayfa `Filtering` ekleme

Üçüncü öğreticide sayfa düzeni tanımlarken,, ve klasörlerinde birkaç "başlangıç" sayfası ekledik `BasicReporting` `Filtering` `CustomFormatting` . Bununla birlikte, bu öğreticide Bu öğreticiye yönelik bir başlangıç sayfası eklemediğimiz için şu anda klasöre iki yeni sayfa eklemek için bir zaman ayırın `Filtering` : `SupplierListMaster.aspx` ve `ProductsForSupplierDetails.aspx` . `SupplierListMaster.aspx` "ana" kayıtları (tedarikçiler), `ProductsForSupplierDetails.aspx` Seçili tedarikçinin ürünlerini görüntüleyecek şekilde listelecektir.

Bu iki yeni sayfanın oluşturulması, bunları ana sayfayla ilişkilendirmeye yönelik olarak `Site.master` .

![Filtre klasörüne SupplierListMaster. aspx ve ProductsForSupplierDetails. aspx sayfalarını ekleyin](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**Şekil 1**: `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` klasöre ve sayfalarına `Filtering` ekleme

Ayrıca, projeye yeni sayfalar eklerken, site eşleme dosyasını uygun şekilde güncelleştirdiğinizden emin olun `Web.sitemap` . Bu öğreticide, `SupplierListMaster.aspx` filtreleme raporları öğesinin bir alt öğesi olarak AŞAĞıDAKI XML içeriğini kullanarak sayfayı site haritasına eklemek yeterlidir `<siteMapNode>` :

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> [K. Scott Allen](http://odetocode.com/Blogs/scott/)'ın ücretsiz Visual Studio [site haritası makrosunu](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)kullanarak yeni ASP.NET sayfaları eklerken site haritası dosyasını güncelleştirme işlemini otomatikleştirmenize yardımcı olabilirsiniz.

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>2. Adım: tedarikçi listesini görüntüleme`SupplierListMaster.aspx`

`SupplierListMaster.aspx`Ve `ProductsForSupplierDetails.aspx` sayfaları oluşturulduktan sonra, bir sonraki adımınız ' de tedarikçilerin GridView 'u oluşturmaktır `SupplierListMaster.aspx` . Sayfaya bir GridView ekleyin ve bunu yeni bir ObjectDataSource 'a bağlayın. Bu ObjectDataSource, `SuppliersBLL` `GetSuppliers()` tüm tedarikçileri döndürmek için sınıfın yöntemini kullanmalıdır.

[![SuppliersBLL sınıfını seçin](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**Şekil 2**: sınıfı seçin `SuppliersBLL` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image4.png))

[![ObjectDataSource 'ı GetSuppliers () metodunu kullanacak şekilde yapılandırma](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**Şekil 3**: bir yöntemi kullanmak için ObjectDataSource 'ı yapılandırma `GetSuppliers()` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image7.png))

Tıklandığı zaman, Kullanıcı `ProductsForSupplierDetails.aspx` QueryString aracılığıyla seçili satırın değerini geçirmekten geçen her GridView satırına görünüm ürünleri başlıklı bir bağlantı içermesi gerekir `SupplierID` . Örneğin, Kullanıcı Tokyo Traders tedarikçinin (4 değerine sahiptir) ürünleri görüntüle bağlantısına tıklasa `SupplierID` , bunlara gönderilmesi gerekir `ProductsForSupplierDetails.aspx?SupplierID=4` .

Bunu gerçekleştirmek için GridView 'a bir [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) ekleyin ve bu, her GridView satırına bir köprü ekler. GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayarak başlayın. Ardından, sol üst taraftaki listeden Hyperlinkalanını seçin ve Ekle ' ye tıklayarak GridView 'un alan listesine Hyperlinkalanını ekleyin.

[![GridView 'a HyperLinkField ekleyin](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**Şekil 4**: GridView 'A HyperLinkField ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image10.png))

Hyperlinkalanı her bir GridView satırındaki bağlantıyla aynı metin veya URL değerlerini kullanacak şekilde yapılandırılabilir veya bu değerleri belirli bir satıra bağlı veri değerlerinde temel alabilir. Tüm satırlarda statik bir değer belirtmek için Hyperlinkalanının `Text` veya `NavigateUrl` özelliklerinin kullanın. Bağlantı metninin tüm satırlar için aynı olmasını Istediğimize göre, HyperLinkField 'ın `Text` özelliğini ürünleri görüntülemek için ayarlayın.

[![Metinleri görüntülemek için Hyperlinkalanının Text özelliğini ayarlayın](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**Şekil 5**: HyperLinkField 'ın `Text` özelliğini ürünleri görüntülemek için ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image13.png))

Metin veya URL değerlerini GridView satırına bağlı temel veriye göre olacak şekilde ayarlamak için, veya özelliklerinden metin veya URL değerlerinin çekilmesi gereken veri alanlarını belirtin `DataTextField` `DataNavigateUrlFields` . `DataTextField` yalnızca tek bir veri alanına ayarlanabilir; `DataNavigateUrlFields`ancak, virgülle ayrılmış bir veri alanları listesine ayarlanabilir. Genellikle metin veya URL 'YI geçerli satırın veri alanı değerinin bir birleşimine ve bazı statik biçimlendirmeye dayandırıyoruz. Bu öğreticide, örneğin, `ProductsForSupplierDetails.aspx?SupplierID=supplierID` *`supplierID`* her GridView 'un row's değeri olduğu gibi, HyperLinkField BAĞLANTıLARıNıN URL 'sinin olmasını istiyoruz `SupplierID` . Burada hem statik hem de veri tabanlı değerlere ihtiyacımız olduğuna dikkat edin: `ProductsForSupplierDetails.aspx?SupplierID=` bağlantı URL 'sinin kısmı statiktir, ancak bu *`supplierID`* bölüm değeri her satırın kendi değeri olan veri odaklı olur `SupplierID` .

Statik ve veri tabanlı değerlerin bir birleşimini göstermek için, `DataTextFormatString` ve `DataNavigateUrlFormatString` özelliklerini kullanın. Bu özelliklerde, gerekirse statik biçimlendirmeyi girin ve ardından `{0}` veya özelliklerinde belirtilen alanın değerinin görünmesini istediğiniz işaretçiyi kullanın `DataTextField` `DataNavigateUrlFields` . `DataNavigateUrlFields`Özellikte birden çok alan belirtilmişse `{0}` , `{1}` ikinci alan değeri için, ilk alan değerinin eklenmesini istediğiniz yeri kullanın.

Bunu öğreticimize uygulayarak `DataNavigateUrlFields` özelliği, `SupplierID` değeri her satır temelinde özelleştirmeniz gereken veri alanı ve `DataNavigateUrlFormatString` özelliği olarak ' i olarak ayarlamanız gerekir `ProductsForSupplierDetails.aspx?SupplierID={0}` .

[![Bağla alanını, TedarikçiKimliği 'e dayalı doğru bağlantı URL 'sini Içerecek şekilde yapılandırın](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**Şekil 6**: hyperlinkalanını `SupplierID` ([tam boyutlu görüntüyü görüntülemek Için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image16.png)) üzerine doğru bağlantı URL 'sini içerecek şekilde yapılandırın

Hyperlinkalanını ekledikten sonra GridView 'un alanlarını özelleştirmek ve yeniden sıralamak ücretsizdir. Aşağıdaki biçimlendirme, bazı küçük alan düzeyi özelleştirmeler yaptıktan sonra GridView 'ı gösterir.

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

Sayfayı bir tarayıcıdan görüntülemek için bir dakikanızı ayırın `SupplierListMaster.aspx` . Şekil 7 ' de gösterildiği gibi, sayfa şu anda ürünleri görüntüle bağlantısı dahil olmak üzere tüm tedarikçilerini listeler. Ürünleri görüntüle bağlantısına tıkladığınızda, bu işlem size `ProductsForSupplierDetails.aspx` , tedarikçinin QueryString içinde geçen bir işlem yapılır `SupplierID` .

[![Her tedarikçi satırında bir görünüm ürünleri bağlantısı bulunur](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**Şekil 7**: her tedarikçi satırı bir görünüm ürünleri bağlantısını içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image19.png))

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>3. Adım: tedarikçinin ürünlerini ' de listeleme`ProductsForSupplierDetails.aspx`

Bu noktada `SupplierListMaster.aspx` , sayfa Kullanıcı gönderiyor ve `ProductsForSupplierDetails.aspx` Seçilen tedarikçiyi `SupplierID` QueryString 'de geçiyor. Öğreticinin son adımı, bu ürünlerin `ProductsForSupplierDetails.aspx` `SupplierID` QueryString aracılığıyla geçilen bir GridView içinde gösterilmesi `SupplierID` . Bu başlatmayı başarmak için `ProductsForSupplierDetails.aspx` , `ProductsBySupplierDataSource` sınıftan yöntemi çağıran adlı yeni bir ObjectDataSource denetimi kullanarak sayfaya bir GridView ekleyin `GetProductsBySupplierID(supplierID)` `ProductsBLL` .

[![ProductsBySupplierDataSource adlı yeni bir ObjectDataSource ekleyin](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**Şekil 8**: adlı yeni bir ObjectDataSource ekleme `ProductsBySupplierDataSource` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image22.png))

[![ProductsBLL sınıfını seçin](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**Şekil 9**: sınıfı seçin `ProductsBLL` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image25.png))

[![ObjectDataSource 'un Getproductsbysupplierıd (SupplierID) metodunu çağırmasını sağlamak](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**Şekil 10**: ObjectDataSource 'un `GetProductsBySupplierID(supplierID)` yöntemi çağırmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image28.png))

Veri kaynağını yapılandırma sihirbazının son adımı, yöntemin parametresinin kaynağını sağlamamızı ister `GetProductsBySupplierID(supplierID)` *`supplierID`* . QueryString değerini kullanmak için, parametre kaynağını QueryString olarak ayarlayın ve QueryStringField metin kutusunda () kullanmak üzere QueryString değeri adını girin `SupplierID` .

[![SupplierID parametre değerini SupplierID QueryString değerinden doldur](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**Şekil 11**: *`supplierID`* parametre değerini `SupplierID` QueryString değerinden doldur ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image31.png))

İşte bu kadar! Şekil 12 ' de `ProductsForSupplierDetails.aspx` ziyaret edildiğinde, ' den Tokyo Traders bağlantısına tıklanarak sayfa gösterilir `SupplierListMaster.aspx` .

[![Tokyo Traders tarafından sağlanan ürünler gösteriliyor](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**Şekil 12**: Tokyo Traders tarafından sağlanan ürünler gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image34.png))

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Tedarikçi bilgilerini görüntüleme`ProductsForSupplierDetails.aspx`

Şekil 12 ' de gösterildiği gibi, `ProductsForSupplierDetails.aspx` sayfa sorgu dizesinde belirtilen ürünleri yalnızca listeler `SupplierID` . Ancak bu sayfaya doğrudan gönderilen birisi, Şekil 12 ' nin Tokyo Traders ürünlerini gösterdiği olduğunu bilmez. Bu sorunu gidermek için, bu sayfada Tedarikçi bilgilerini de görüntüleriz.

GridView ürünlerinin üzerine bir FormView ekleyerek başlayın. `SuppliersDataSource`Sınıfın yöntemini çağıran adlı yeni bir ObjectDataSource denetimi oluşturun `SuppliersBLL` `GetSupplierBySupplierID(supplierID)` .

[![SuppliersBLL sınıfını seçin](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**Şekil 13**: sınıfı seçin `SuppliersBLL` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image37.png))

[![ObjectDataSource 'un Getsupplierbysupplierıd (SupplierID) metodunu çağırmasını sağlamak](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**Şekil 14**: ObjectDataSource 'un `GetSupplierBySupplierID(supplierID)` yöntemi çağırmasına[izin vermek (tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image40.png))

' De olduğu gibi `ProductsBySupplierDataSource` , *`supplierID`* parametresine `SupplierID` QueryString değeri değeri atanır.

[![SupplierID parametre değerini SupplierID QueryString değerinden doldur](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**Şekil 15**: *`supplierID`* parametre değerini `SupplierID` QueryString değerinden doldur ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image43.png))

FormView, Tasarım görünümü ObjectDataSource 'a bağlarken, Visual Studio otomatik olarak FormView 'un `ItemTemplate` , `InsertItemTemplate` , ve `EditItemTemplate` ObjectDataSource tarafından döndürülen her veri alanı Için etiket ve metin kutusu Web denetimleriyle oluşturur. Yalnızca üretici bilgilerini `InsertItemTemplate` ve ve ' i kaldırmak için ücretsiz olarak göstermek istiyoruz `EditItemTemplate` . Daha sonra, bir öğe içinde tedarikçinin şirket adını `<h3>` ve şirket adının altındaki Adres, şehir, ülke ve telefon numarasını görüntüleyecek şekilde ItemTemplate 'i düzenleyin. Alternatif olarak, `DataSourceID` `ItemTemplate` "[ObjectDataSource ile verileri görüntüleme](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" öğreticisine geri döndüğünüzde FormView 'u el ile ayarlayabilir ve işaretlemeyi oluşturabilirsiniz.

Bu düzenlemeleriniz sonrasında, FormView 'un bildirim temelli işaretleme aşağıdakine benzer görünmelidir:

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

Şekil 16, `ProductsForSupplierDetails.aspx` Yukarıdaki tedarikçi bilgileri eklendikten sonra sayfanın ekran görüntüsünü gösterir.

[![Ürünlerin listesi, tedarikçiyle Ilgili bir Özet Içerir](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**Şekil 16**: ürünlerin listesi, tedarikçi hakkında bir Özet içerir ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-across-two-pages-cs/_static/image46.png))

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Kullanıcı arabirimine son dokunmayı uygulama `ProductsForSupplierDetails.aspx`

Bu rapora yönelik kullanıcı deneyimini geliştirmek için, sayfada yapmanız yeterli olan birkaç ekleme vardır `ProductsForSupplierDetails.aspx` . Şu anda, bir kullanıcının sayfadan yeniden üretici listesine gidebilmeleri, `ProductsForSupplierDetails.aspx` tarayıcının geri düğmesine tıklamanız içindir. Daha sonra, `ProductsForSupplierDetails.aspx` `SupplierListMaster.aspx` kullanıcının ana listeye dönmesi için başka bir yol sunarak, geri bağlantı sağlayan sayfaya bir köprü denetimi ekleyelim.

[![Kullanıcıyı SupplierListMaster. aspx öğesine geri çekmek için bir köprü denetimi ekleyin](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**Şekil 17**: kullanıcıyı geri çekmek Için bir köprü denetimi ekleyin `SupplierListMaster.aspx` ([tam boyutlu görüntüyü görüntülemek için tıklayın](master-detail-filtering-across-two-pages-cs/_static/image49.png))

Kullanıcı herhangi bir ürüne sahip olmayan bir tedarikçi için ürünleri görüntüle bağlantısına tıklasa, `ProductsBySupplierDataSource` içindeki ObjectDataSource `ProductsForSupplierDetails.aspx` hiçbir sonuç döndürmez. ObjectDataSource 'a bağlı GridView, kullanıcının tarayıcısında sayfada boş bir bölgeye neden olan herhangi bir biçimlendirmeyi işlemez. Seçili tedarikçi ile ilişkili hiçbir ürün olmadığından, kullanıcıya daha net bir şekilde iletişim kurmak için GridView 'un `EmptyDataText` özelliğini, böyle bir durum ortaya çıkarsa görüntülenmesini istediğimiz iletiyle ayarlayabiliriz. Bu özelliği "Bu tedarikçi tarafından sunulan ürün yok" olarak ayarladı

Varsayılan olarak, Northwinds veritabanındaki tüm tedarikçiler en az bir ürün sağlar. Bununla birlikte, bu öğretici için tabloyu el ile değiştirdim ve bu da `Products` tedarikçinin escargots nouveaux, artık hiçbir ürünle ilişkili değil. Şekil 18, bu değişiklik yapıldıktan sonra escargots nouveaux için Ayrıntılar sayfasını gösterir.

[![Kullanıcılara, tedarikçinin hiçbir ürün Sağlamadiğini bilgilendirilir](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**Şekil 18**: kullanıcılara tedarikçinin hiçbir ürün sağlamadığını bilgilendirilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](master-detail-filtering-across-two-pages-cs/_static/image52.png))

## <a name="summary"></a>Özet

Ana/ayrıntı raporları hem ana hem de ayrıntı kayıtlarını tek bir sayfada görüntüleyebilir, ancak birçok Web sitesinde iki Web sayfasında ayrılır. Bu öğreticide, "ana" Web sayfasındaki bir GridView 'da listelenen tedarikçilere ve "Ayrıntılar" sayfasında listelenen ilişkili ürünlere sahip olarak böyle bir Master/Detail raporunun nasıl uygulanacağını inceledik. Ana Web sayfasındaki her bir tedarikçi satırı, satır değerinin yanında geçen Ayrıntılar sayfasının bağlantısını içerir `SupplierID` . Bu tür satıra özgü bağlantılar, GridView 'un Hyperlinkalanı kullanılarak kolayca eklenebilir.

Ayrıntılar sayfasında belirtilen tedarikçi için bu ürünlerin alınması, `ProductsBLL` sınıfın yöntemi çağrılarak gerçekleştirildi `GetProductsBySupplierID(supplierID)` . *`supplierID`* Parametre değeri, parametre kaynağı olarak QueryString kullanılarak bildirimli olarak belirtildi. Ayrıca, ayrıntılar sayfasında bir FormView kullanarak tedarikçi ayrıntılarının nasıl görüntüleneceğini de inceledik.

[Sonraki öğreticimiz](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) ana/ayrıntı raporlarında son bir deneyimdir. Bir GridView 'da, her satırda bir Seç düğmesi bulunan ürünlerin listesini görüntüleme bölümüne bakacağız. Seç düğmesine tıkladığınızda bu ürünün ayrıntıları aynı sayfada bir DetailsView denetiminde görüntülenir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [4GuysFromRolla.com](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Adresinden erişilebilir [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla bulunabilir [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, bana bir satır bırakın [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](master-detail-filtering-with-two-dropdownlists-cs.md) 
>  [Sonraki](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
