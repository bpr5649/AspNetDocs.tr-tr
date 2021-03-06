---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
title: GridView 'a düğme ekleme ve bu düğmeye yanıt verme (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle de biz...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 06c6bbd2-4bdc-435b-87a3-df2c868f4baa
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
msc.type: authoredcontent
ms.openlocfilehash: 8727d8faead02340d223c75845bf29f63d1a0834
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78549478"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-vb"></a>GridView’a Düğme Ekleme ve Bunları Yanıtlama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_VB.exe) veya [PDF 'yi indirin](adding-and-responding-to-buttons-to-a-gridview-vb/_static/datatutorial28vb1.pdf)

> Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle, kullanıcının tedarikçilerle sayfa oluşturmasını sağlayan bir FormView içeren bir arabirim oluşturacağız.

## <a name="introduction"></a>Giriş

Birçok raporlama senaryosu rapor verilerine salt okuma erişimi içerirken, bu, raporların, görüntülenecek verilere göre eylemleri gerçekleştirme yeteneğini içermesi için sık görülen bir durumdur. Genellikle bu, tıklatıldığında raporda görüntülenen her kayıtla birlikte bir Button, LinkButton veya ImageButton Web denetimi eklemeyi, tıklandığı zaman geri göndermeye neden olur ve bazı sunucu tarafı kodları çağırır. Kayda göre kayıt temelinde verileri düzenlemenin ve silmenin en yaygın örneği vardır. Aslında, veri öğreticisini [ekleme, güncelleştirme ve silmeye Ilişkin genel bakışın](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) yanı sıra, düzenlemenin ve silmenin yanı sıra GridView, DetailsView ve FormView denetimlerinin tek bir kod satırı yazmak zorunda kalmadan bu işlevselliği destekleyebilmesi yaygın bir çalışmadır.

Düzenle ve Sil düğmelerine ek olarak, GridView, DetailsView ve FormView denetimleri, tıklandığı sırada bazı özel sunucu tarafı mantığlarını, LinkButtons 'ı veya görüntü düğmelerini de içerebilir. Bu öğreticide, hem bir şablon hem de bir GridView veya DetailsView denetiminin alanları için özel düğmeler ekleme bölümüne bakacağız. Özellikle, kullanıcının tedarikçilerle sayfa oluşturmasını sağlayan bir FormView içeren bir arabirim oluşturacağız. Belirli bir tedarikçi için, FormView, bir düğme web denetimiyle birlikte tedarikçi hakkındaki bilgileri gösterir ve tıklandıklarında ilişkili tüm ürünlerini kullanımdan kaldırıldı olarak işaretleyebilir. Ek olarak, bir GridView, seçili tedarikçi tarafından sunulan bu ürünleri, tıklanmış olması halinde, ürün s `UnitPrice` %10 ' u (bkz. Şekil 1) yükseltir veya azalttığını belirten fiyat ve Indirim fiyatı düğmelerini içerir.

[FormView ve GridView 'un her Ikisi de ![özel eylemleri gerçekleştiren düğmeler Içerir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image1.png)

**Şekil 1**: hem FormView hem de GridView özel eylemleri gerçekleştiren düğmeler içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image3.png))

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>1\. Adım: düğme öğreticisi Web sayfalarını ekleme

Özel düğmeler eklemeye bakmadan önce, bu öğreticide ihtiyaç duyduğumuz Web sitesi projemizdeki ASP.NET sayfalarını oluşturmak için ilk olarak bir süre sürdük. `CustomButtons`adlı yeni bir klasör ekleyerek başlayın. Sonra, her bir sayfayı `Site.master` ana sayfayla ilişkilendirdiğinizden emin olmak için, aşağıdaki iki ASP.NET sayfasını bu klasöre ekleyin:

- `Default.aspx`
- `CustomButtons.aspx`

![Özel düğmelerle Ilgili öğreticiler için ASP.NET sayfaları ekleyin](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image4.png)

**Şekil 2**: özel düğmelerle ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `CustomButtons` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image5.png)

**Şekil 3**: `Default.aspx` `SectionLevelTutorialListing.ascx` Kullanıcı denetimini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image7.png))

Son olarak, sayfaları `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, sayfalama ve sıralama `<siteMapNode>`sonrasında aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample1.xml)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık özel düğmeler öğreticisi için girişi Içerir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image8.png)

**Şekil 4**: site haritası artık özel düğmeler öğreticisi Için girişi içerir

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>2\. Adım: tedarikçileri listeleyen bir FormView ekleme

Tedarikçileri listeleyen FormView ekleyerek bu öğreticiyi kullanmaya başlayın. Bu FormView, giriş bölümünde anlatıldığı gibi, bir GridView 'da tedarikçi tarafından sunulan ürünleri göstererek kullanıcının tedarikçilerle sayfa eklemesine izin verir. Ayrıca, bu FormView, tıklandığında tedarikçinin tüm ürünlerini kullanımdan kaldırıldı olarak işaretleyecek bir düğme içerecektir. Kendimize 'e özel düğme ekleme konusunda sorun yapmadan önce, ilk olarak yalnızca FormView 'u Tedarikçi bilgilerini görüntüleyecek şekilde oluşturalım.

`CustomButtons` klasöründeki `CustomButtons.aspx` sayfasını açarak başlayın. Araç kutusundan Tasarımcı üzerine sürükleyerek sayfaya bir FormView ekleyin ve `ID` özelliğini `Suppliers`olarak ayarlayın. FormView s akıllı etiketinden `SuppliersDataSource`adlı yeni bir ObjectDataSource oluşturmayı tercih edin.

[SuppliersDataSource adlı yeni bir ObjectDataSource oluşturma ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image9.png)

**Şekil 5**: `SuppliersDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image11.png))

`SuppliersBLL` sınıf s `GetSuppliers()` yönteminden (bkz. Şekil 6) sorgulamalarını sağlayan bu yeni ObjectDataSource 'ı yapılandırın. Bu FormView, tedarikçi bilgilerini güncelleştirmek için bir arabirim sağlamadığından, GÜNCELLEŞTIR sekmesindeki aşağı açılan listeden (hiçbiri) seçeneğini belirleyin.

[Veri kaynağını SuppliersBLL Class s GetSuppliers () metodunu kullanacak şekilde yapılandırmak ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image12.png)

**Şekil 6**: veri kaynağını `SuppliersBLL` Class s `GetSuppliers()` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image14.png))

ObjectDataSource yapılandırıldıktan sonra, Visual Studio FormView için bir `InsertItemTemplate`, `EditItemTemplate`ve `ItemTemplate` oluşturur. `InsertItemTemplate` ve `EditItemTemplate` kaldırın ve `ItemTemplate` yalnızca tedarikçinin şirket adını ve telefon numarasını görüntüleyecek şekilde değiştirin. Son olarak, akıllı etiketinden sayfalama etkinleştir onay kutusunu işaretleyerek (veya `AllowPaging` özelliğini `True`olarak ayarlayarak FormView için sayfalama desteğini açın). Bu değişikliklerden sonra sayfanızın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample2.aspx)]

Şekil 7 ' de bir tarayıcıdan görüntülendiklerinde CustomButtons. aspx sayfası gösterilir.

[FormView ![Şu anda seçili olan tedarikçiden CompanyName ve telefon alanlarını listeler](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image15.png)

**Şekil 7**: FormView, şu anda seçili olan tedarikçiden `CompanyName` ve `Phone` alanlarını listeler ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image17.png))

## <a name="step-3-adding-a-gridview-that-lists-the-selected-supplier-s-products"></a>3\. Adım: seçili tedarikçinin ürünlerini listeleyen bir GridView ekleme

Tüm ürünleri Durdur düğmesini FormView s şablonuna eklemeden önce, ilk olarak seçili tedarikçi tarafından sunulan ürünleri listeleyen FormView 'un altına bir GridView ekleyelim. Bunu gerçekleştirmek için, sayfaya bir GridView ekleyin, `ID` özelliğini `SuppliersProducts`olarak ayarlayın ve `SuppliersProductsDataSource`adlı yeni bir ObjectDataSource ekleyin.

[SuppliersProductsDataSource adlı yeni bir ObjectDataSource oluşturma ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image18.png)

**Şekil 8**: `SuppliersProductsDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image20.png))

Bu ObjectDataSource 'ı ProductsBLL sınıfı s `GetProductsBySupplierID(supplierID)` yöntemini kullanacak şekilde yapılandırın (bkz. Şekil 9). Bu GridView bir ürün fiyatı ayarlanmasına izin vermekle kalmaz, GridView 'daki yerleşik Düzenle veya silme özelliklerini kullanmayacaktır. Bu nedenle, ObjectDataSource için GÜNCELLEŞTIRME, ekleme ve SILME sekmeleri için açılan listeyi (yok) olarak ayarlayabiliriz.

[![veri kaynağını ProductsBLL sınıfı s Getproductsbysupplierıd (SupplierID) metodunu kullanacak şekilde yapılandırın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image21.png)

**Şekil 9**: veri kaynağını `ProductsBLL` Class s `GetProductsBySupplierID(supplierID)` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image23.png))

`GetProductsBySupplierID(supplierID)` yöntemi bir giriş parametresini kabul ettiğinden, ObjectDataSource Sihirbazı bize bu parametre değerinin kaynağını sorar. FormView 'dan `SupplierID` değerini geçirmek için, parametre kaynağı açılır listesini kontrol ve ControlID açılan listesini `Suppliers` (adım 2 ' de oluşturulan FormView 'un KIMLIĞI) olarak ayarlayın.

[![SupplierID parametresinin Suppliers FormView denetiminden gelmesi gerektiğini belirtir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image24.png)

**Şekil 10**: *`supplierID`* parametresinin `Suppliers` FormView denetiminden gelmesi gerektiğini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image26.png))

ObjectDataSource Sihirbazı tamamlandıktan sonra GridView, her ürün veri alanı için bir BoundField veya CheckBoxField içerecektir. `Discontinued` CheckBoxField ile birlikte yalnızca `ProductName` ve `UnitPrice` BoundFields alanlarını göstermek için bunu kırpalım; Ayrıca, metnin bir para birimi olarak biçimlendirilmesi için `UnitPrice` BoundField biçimine izin verin. GridView ve `SuppliersProductsDataSource` ObjectDataSource 'lar bildirim temelli biçimlendirme aşağıdaki biçimlendirmeye benzer olmalıdır:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample3.aspx)]

Bu noktada, öğreticimiz ana/ayrıntı raporunu görüntüleyerek kullanıcının en üstteki FormView 'dan bir tedarikçi seçmesini ve alttaki GridView aracılığıyla söz konusu tedarikçi tarafından sunulan ürünleri görüntülemesini sağlar. Şekil 11 ' den bu sayfanın bir ekran görüntüsünü, FormView 'dan Tokyo Traders tedarikçisine seçerken gösterir.

[![seçili tedarikçinin ürünleri GridView 'da görüntülenir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image27.png)

**Şekil 11**: seçili tedarikçinin ürünleri GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image29.png))

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>4\. Adım: bir tedarikçiye yönelik tüm ürünleri sona erdirmek için DAL ve BLL yöntemleri oluşturma

FormView 'a bir düğme ekleyebilmemiz için, tıkladıklarında, tedarikçinin tüm ürünlerini tamamen devam ettirir, önce bu eylemi gerçekleştiren DAL ve BLL 'e bir yöntem eklememiz gerekir. Özellikle, bu yöntem `DiscontinueAllProductsForSupplier(supplierID)`olarak adlandırılır. FormView s düğmesine tıklandığında, bu yöntemi Iş mantığı katmanında, seçili tedarikçinin s `SupplierID`geçirerek çağıracağız; BLL daha sonra karşılık gelen veri erişim katmanı yöntemine geri çağrı yapılır, bu da belirtilen Tedarikçi s ürünlerini sürekli olarak devam eden veritabanında `UPDATE` bir bildirim sağlar.

Önceki öğreticilerimizde yaptığımız gibi, DAL yöntemi oluşturmaya, sonra BLL yöntemine ve son olarak ASP.NET sayfasındaki işlevselliği uygulamaya göre aşağıdan yukarıya bir yaklaşım kullanacağız. `App_Code/DAL` klasöründe `Northwind.xsd` türü belirtilmiş veri kümesini açın ve `ProductsTableAdapter` yeni bir yöntem ekleyin (`ProductsTableAdapter` sağ tıklayın ve sorgu Ekle ' yi seçin). Bunun yapılması, yeni yöntemi ekleme sürecinde bize yol gösteren TableAdapter sorgu Yapılandırma Sihirbazı 'nı getirir. DAL yönteminizin bir geçici SQL ifadesini kullandığını belirterek başlayın.

[![geçici bir SQL Ifadesini kullanarak DAL yöntemi oluşturma](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image30.png)

**Şekil 12**: GEÇICI bir SQL IFADESINI kullanarak dal yöntemi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image32.png))

Daha sonra sihirbaz, oluşturulacak sorgu türünü bizimle uyarır. `DiscontinueAllProductsForSupplier(supplierID)` yönteminin `Products` veritabanı tablosunu güncelleştirmesi gerekir, çünkü `Discontinued` alanı belirtilen *`supplierID`* tarafından sunulan tüm ürünler için 1 olarak ayarlandığında, verileri güncelleştiren bir sorgu oluşturmanız gerekir.

[![GÜNCELLEŞTIRME sorgu türünü seçin](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image33.png)

**Şekil 13**: güncelleştirme sorgu türünü seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image35.png))

Sonraki sihirbaz ekranı, `Products` DataTable 'da tanımlanan her bir alanı güncelleştiren TableAdapter s Existing `UPDATE` ifadesini sağlar. Bu sorgu metnini aşağıdaki ifadeyle değiştirin:

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample4.sql)]

Bu sorguyu girdikten ve Ileri 'ye tıkladıktan sonra, son sihirbaz ekranı yeni yöntem adı `DiscontinueAllProductsForSupplier`kullanımını ister. Son düğmesine tıklayarak Sihirbazı doldurun. Veri kümesi tasarımcısına döndükten sonra, `ProductsTableAdapter` adlı `DiscontinueAllProductsForSupplier(@SupplierID)`yeni bir yöntem görmeniz gerekir.

[yeni dal yönteminin adını ![adı allproductsfortedarikç](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image36.png)

**Şekil 14**: yeni dal yöntemini adlandırın `DiscontinueAllProductsForSupplier` ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image38.png))

Veri erişim katmanında oluşturulan `DiscontinueAllProductsForSupplier(supplierID)` yöntemi ile, sonraki göreviniz Iş mantığı katmanında `DiscontinueAllProductsForSupplier(supplierID)` yöntemini oluşturmaktır. Bunu gerçekleştirmek için `ProductsBLL` sınıf dosyasını açın ve aşağıdakileri ekleyin:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample5.vb)]

Bu yöntem, yalnızca DAL içindeki `DiscontinueAllProductsForSupplier(supplierID)` yöntemine çağrı yaparak, belirtilen *`supplierID`* parametre değerini geçirerek. Yalnızca bir tedarikçi ürünlerinin belirli koşullar altında kullanımdan bulunmasına izin verilen iş kuralları varsa, bu kuralların BLL 'de burada uygulanması gerekir.

> [!NOTE]
> `ProductsBLL` sınıfındaki `UpdateProduct` aşırı yüklemelerin aksine `DiscontinueAllProductsForSupplier(supplierID)` Yöntem imzası `DataObjectMethodAttribute` özniteliğini (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`) içermez. Bu, `DiscontinueAllProductsForSupplier(supplierID)` yöntemini, GÜNCELLEŞTIRME sekmesindeki veri kaynağı Yapılandırma Sihirbazı ' nın açılan listesi ' nden daha fazla düşürüler. Bu özniteliği, ASP.NET sayfamızda doğrudan bir olay işleyicisinden `DiscontinueAllProductsForSupplier(supplierID)` yöntemi çağırmak yaptığımız için atlıyorum.

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>5\. Adım: FormView 'a tüm ürünleri durdur düğmesi ekleme

BLL ve DAL `DiscontinueAllProductsForSupplier(supplierID)` yöntemi tamamlandıktan sonra, seçili tedarikçiye yönelik tüm ürünleri sona erdirme özelliği eklemek için son adım, FormView s `ItemTemplate`bir düğme web denetimi eklemektir. Düğme metniyle, tedarikçinin s telefon numarasının altına böyle bir düğme ekleyelim, tüm ürünleri ve `DiscontinueAllProductsForSupplier``ID` özellik değerini durdur. Bu düğme web denetimini, FormView 'un akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayarak (Şekil 15 ' i) veya doğrudan bildirime dayalı sözdizimi aracılığıyla ekleyebilirsiniz.

[![tüm ürünleri Durdur düğme web denetimi ile FormView 'e](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image39.png)

**Şekil 15**: FormView s `ItemTemplate` tüm ürünleri Durdur düğme web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image41.png))

Düğmeye sayfayı ziyaret eden bir kullanıcı tarafından tıklandığında, bir geri gönderme işlemi ve FormView [`ItemCommand` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) ateşlenir. Bu düğmeye tıklanmakta olan bu düğmeye yanıt olarak özel kod yürütmek için, bu olay için bir olay işleyicisi oluşturarız. Bu durumda, *her* düğme, LinkButton veya ImageButton Web denetimine FormView içinde tıklandığında `ItemCommand` olayının tetiklendiğine anlayın. Diğer bir deyişle, Kullanıcı FormView 'da bir sayfadan diğerine taşınırsa, `ItemCommand` olayı ateşlenir; Kullanıcı ekleme, güncelleştirme veya silmeyi destekleyen bir FormView 'da yeni, Düzenle veya Sil ' i tıklattığında aynı şey.

`ItemCommand` düğmenin tıklanmasından bağımsız olarak tetiklendiği için, olay işleyicisinde tüm ürünleri Durdur düğmesinin tıklandığını veya başka bir düğme olup olmadığını belirlemek için bir yol gerekir. Bunu gerçekleştirmek için, Button Web Control s `CommandName` özelliğini bir tanımlayıcı değere ayarlayabiliriz. Düğmeye tıklandığında, bu `CommandName` değeri `ItemCommand` olay işleyicisine geçirilir ve tüm ürünleri Durdur düğmesinin tıklanmadığını belirlememize olanak tanır. Tüm ürünler düğmesini durdur `CommandName` özelliği, ürünleri Kaldır ' a ayarlayın.

Son olarak, kullanıcının gerçekten seçili Tedarikçi ürünlerini sona erdirmek istediğinizden emin olmak için bir istemci tarafı onaylama iletişim kutusu kullanalım. Öğreticiyi [silerken Istemci tarafı onaylama ekleme](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb.md) konusunda gördüğünüz gibi, bu, JavaScript bir bit ile gerçekleştirilebilir. Özellikle, düğme web denetimi s OnClientClick özelliğini `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');` olarak ayarlayın

Bu değişiklikleri yaptıktan sonra FormView 'un bildirim temelli sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample6.aspx)]

Ardından, FormView s `ItemCommand` olayı için bir olay işleyicisi oluşturun. Bu olay işleyicisinde, önce tüm ürünleri Durdur düğmesine tıklanmadığını belirlememiz gerekir. Bu durumda, `ProductsBLL` sınıfının bir örneğini oluşturmak ve `DiscontinueAllProductsForSupplier(supplierID)` metodunu, seçili FormView 'un `SupplierID` geçirerek çağırmak istiyoruz:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample7.vb)]

FormView 'daki geçerli seçili tedarikçinin `SupplierID` FormView s [`SelectedValue` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)kullanılarak erişilebilir olduğunu unutmayın. `SelectedValue` özelliği, FormView 'da görüntülenmekte olan kaydın ilk veri anahtarı değerini döndürür. Veri anahtarı değerlerinin alındığı veri alanlarını gösteren FormView s [`DataKeyNames` özelliği](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx), Visual Studio tarafından otomatik olarak `SupplierID` olarak ayarlanmıştır. Bu, ObjectDataSource 'un adım 2 ' de FormView 'e bağlanması sırasında otomatik olarak Visual Studio tarafından olarak ayarlanmıştır.

`ItemCommand` olay işleyicisi oluşturulduktan sonra, sayfayı sınamak için bir dakikanızı ayırın. Cogutıva ve Sorgtada ' Las Cabras ' tedarikçisine gidin (benim için FormView 'daki beşinci tedarikçiye göre). Bu Tedarikçi, her ikisi de *artık Discontinued olan* Sorgo Cabrales ve Sorgo Manchego La Pastora olmak üzere iki ürün sunmaktadır.

COOPERATIVA ve Sorgun ' Las Cabras ' öğesinin iş dışı olduğunu ve bu nedenle ürünlerinin sonlandırılmamakta olduğunu düşünün. Tüm ürünleri Durdur düğmesine tıklayın. Bu, istemci tarafı onaylama iletişim kutusunu görüntüler (bkz. Şekil 16).

[![Cooperativa de Sorgtada Las Cabras Iki etkin ürün sağlar](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image42.png)

**Şekil 16**: Cooperativa de Sorgtada Las Cabras Iki etkin ürün sağlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image44.png))

İstemci tarafı onaylama iletişim kutusunda Tamam ' a tıklarsanız, form gönderimi devam eder ve bu da FormView s `ItemCommand` olayının tetikleneceği bir geri göndermeye neden olur. Oluşturduğumuz olay işleyicisi yürütülecektir, `DiscontinueAllProductsForSupplier(supplierID)` yöntemini çağırır ve hem Sorgo Cabrales hem de Sorgo Manchego La Pastora ürünlerinin her ikisi de devam eder.

GridView s görünüm durumunu devre dışı bırakırsanız, GridView her geri göndermede temel alınan veri deposuna yeniden bağlanır ve bu nedenle hemen bu iki ürünün artık devre dışı bırakıldığını yansıtacak şekilde güncelleştirilir (bkz. Şekil 17). Ancak, GridView 'da görünüm durumunu devre dışı bırakıldıysanız, bu değişikliği yaptıktan sonra verileri GridView 'a el ile yeniden bağlamanız gerekir. Bunu gerçekleştirmek için, `DiscontinueAllProductsForSupplier(supplierID)` yöntemini çağırdıktan hemen sonra GridView s `DataBind()` yöntemine bir çağrı yapmanız yeterlidir.

[Tüm ürünleri Durdur düğmesine tıkladıktan sonra, tedarikçinin s ürünleri buna göre güncelleştirilir ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image45.png)

**Şekil 17**: tüm ürünleri Durdur düğmesine tıkladıktan sonra, tedarikçinin s ürünleri uygun şekilde güncelleştirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image47.png))

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-product-s-price"></a>6\. Adım: bir ürün fiyatı ayarlamak için Iş mantığı katmanında UpdateProduct Overload oluşturma

FormView 'daki tüm ürünleri Durdur düğmesinin yanı sıra, GridView 'da bir ürünün fiyatını artırmak ve azaltmak için düğmeler eklemek üzere öncelikle uygun veri erişim katmanını ve Iş mantığı katman yöntemlerini eklememiz gerekir. DAL içinde tek bir ürün satırını güncelleştiren bir metoda zaten sahip olduğumuz için BLL 'deki `UpdateProduct` yöntemi için yeni bir aşırı yükleme oluşturarak bu işlevselliği sağlayabiliriz.

Son `UpdateProduct` aşırı yüklemeleri, ürün alanlarının bazı kombinasyonda skaler giriş değerleri olarak alınmıştır ve daha sonra yalnızca belirtilen ürüne ait bu alanları güncelleştirdi. Bu aşırı yüklemede, bu standarda göre biraz farklılık gösterir ve bunun yerine ürün `ProductID` ve `UnitPrice` ayarlama (yeni, ayarlanmış `UnitPrice` kendi kendine geçirilme aksine). Bu yaklaşım, geçerli ürün `UnitPrice`'yi belirlemekten daha fazla duymak zorunda olduğumuz için ASP.NET sayfa arka plan kodu sınıfına yazılması gereken kodu basitleştirir.

Bu öğretici için `UpdateProduct` aşırı yüklemesi aşağıda gösterilmektedir:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample8.vb)]

Bu aşırı yükleme, DAL s `GetProductByProductID(productID)` yöntemiyle belirtilen ürünle ilgili bilgileri alır. Ardından, ürün `UnitPrice` bir veritabanı `NULL` değeri atanıp atanmadığını görmek için kontrol eder. Bu değer ise, Fiyat değiştirilmemiş olarak kalır. Ancak,`NULL` `UnitPrice` olmayan bir değer varsa, yöntemi belirtilen yüzde (`unitPriceAdjustmentPercent`) tarafından `UnitPrice` ürün güncelleştirmelerini güncelleştirir.

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>7\. Adım: GridView 'a artış ve küçültme düğmelerini ekleme

GridView (ve DetailsView), her ikisi de bir alan koleksiyonundan oluşur. BoundFields, CheckBoxFields ve TemplateFields 'e ek olarak, ASP.NET, adından da anlaşılacağı gibi, her satır için bir Button, LinkButton veya ImageButton içeren bir sütun olarak işleyen ButtonField 'ı içerir. FormView 'a benzer şekilde, GridView sayfalama düğmeleri içindeki *herhangi bir* düğmeye tıklamak, düğmeleri düzenleme veya silme, düğmeleri sıralama ve benzeri bir geri gönderme işlemine neden olur ve gridview s [`RowCommand` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)başlatır.

ButtonField, her düğme `CommandName` için belirtilen değeri atayan bir `CommandName` özelliğine sahiptir. FormView ile benzer şekilde, hangi düğmenin tıklandığını belirleyen `CommandName` değeri `RowCommand` olay işleyicisi tarafından kullanılır.

Bir düğme metin fiyatı + %10 ve diğeri fiyat-%10 ' a sahip olmak üzere GridView 'a iki yeni Buttonalanı ekleyelim. Bu ButtonFields alanlarını eklemek için GridView s akıllı etiketinden sütunları düzenle bağlantısına tıklayın, sol üstteki listeden ButtonField alan türünü seçin ve Ekle düğmesine tıklayın.

![GridView 'a Iki ButtonField ekleyin](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image48.png)

**Şekil 18**: GridView 'A Iki buttonalanı ekleme

İki ButtonField öğesini ilk iki GridView alanı olarak görünecek şekilde taşıyın. Ardından, bu iki ButtonFields `Text` özelliklerini Price + %10 ve Price-10 ' a ve `CommandName` özelliklerini sırasıyla ıncreaseprice ve DecreasePrice olarak ayarlayın. Varsayılan olarak, bir ButtonField, düğme sütununu LinkButtons olarak işler. Ancak, ButtonField s [`ButtonType` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)aracılığıyla bu değiştirilebilir. Bu iki ButtonField ' ın düzenli basma düğmeleri olarak işlenmiş olmasına izin ver. Bu nedenle, `ButtonType` özelliğini `Button`olarak ayarlayın. Şekil 19, bu değişiklikler yapıldıktan sonra alanlar iletişim kutusunu gösterir; Aşağıda, GridView s bildirim temelli biçimlendirme bu şekilde yapılır.

![ButtonFields metin, CommandName ve ButtonType özelliklerini yapılandırın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image49.png)

**Şekil 19**: buttonfields `Text`, `CommandName`ve `ButtonType` özelliklerini yapılandırma

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample9.aspx)]

Bu ButtonFields 'ler oluşturulduktan sonra, son adım GridView s `RowCommand` olayı için bir olay işleyicisi oluşturmaktır. Bu olay işleyicisi, Fiyat + %10 veya fiyat-10% düğmelerine tıklandığı için tetiklense, düğme tıklandığı satırın `ProductID` belirlenmesi ve sonra uygun `UnitPrice` yüzde ayarlamasını `ProductID`ile geçirerek `ProductsBLL` sınıf s `UpdateProduct` yöntemini çağırmaları gerekir. Aşağıdaki kod bu görevleri gerçekleştirir:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample10.vb)]

Fiyatı + %10 veya fiyat-10% düğmesine tıklanmış olan satırın `ProductID` belirleyebilmek için, GridView s `DataKeys` koleksiyonuna başvurmalısınız. Bu koleksiyon, her GridView satırı için `DataKeyNames` özelliğinde belirtilen alanların değerlerini barındırır. GridView s `DataKeyNames` özelliği, ObjectDataSource 'u GridView 'a bağlarken Visual Studio tarafından ProductID olarak ayarlandığı için, `DataKeys(rowIndex).Value` belirtilen *RowIndex*için `ProductID` sağlar.

ButtonField, düğme `e.CommandArgument` parametresi aracılığıyla tıklandığı olan satırın *RowIndex* öğesinde otomatik olarak geçer. Bu nedenle, fiyatı + %10 veya fiyat-10% düğmesine tıklandığı satırın `ProductID` belirlenmesi için şunu kullanırız: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`.

Tüm ürünleri Durdur düğmesinin bulunduğu gibi, GridView s görünüm durumunu devre dışı bırakırsanız, GridView her geri göndermede temel alınan veri deposuna yeniden bağlanır ve bu nedenle, tıklanarak oluşan bir fiyat değişikliğini yansıtacak şekilde hemen güncelleştirilir. düğmelerden birini kullanabilirsiniz. Ancak, GridView 'da görünüm durumunu devre dışı bırakıldıysanız, bu değişikliği yaptıktan sonra verileri GridView 'a el ile yeniden bağlamanız gerekir. Bunu gerçekleştirmek için, `UpdateProduct` yöntemini çağırdıktan hemen sonra GridView s `DataBind()` yöntemine bir çağrı yapmanız yeterlidir.

Şekil 20, Grandma Kelly 'in Homestead tarafından sunulan ürünleri görüntülerken sayfayı gösterir. Şekil 21, Grandma 'nın boyuna yayıldığı ve Kuzey Woods Cranbraz Sauce için fiyat-10% düğmesi bir kez tıklandıktan sonra, Fiyat + %10 ' dan sonra sonuçları gösterir.

[GridView ![Price + %10 ve Price-10% düğmelerini Içerir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image50.png)

**Şekil 20**: GridView, Price + %10 ve Price-10% düğmelerini içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image52.png))

[![birinci ve üçüncü ürün için fiyatlar, Fiyat + %10 ve fiyat-10% düğmeleri aracılığıyla güncelleştirilmiştir](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image53.png)

**Şekil 21**: birinci ve üçüncü ürünün fiyatları, Fiyat + %10 ve fiyat-10% düğmeleriyle güncelleştirilmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image55.png))

> [!NOTE]
> GridView (ve DetailsView), TemplateFields öğesine eklenen düğmeler, LinkButtons veya ımagebuttons da içerebilir. BoundField 'da olduğu gibi, tıklandığı sırada bu düğmeler, GridView s `RowCommand` olayını oluşturacak şekilde bir geri gönderme işlemiyle gönderilir. Ancak, bir TemplateField öğesine düğme eklenirken düğme s `CommandArgument`, ButtonFields kullanılırken olduğu gibi otomatik olarak satır dizinine ayarlanır. `RowCommand` olay işleyicisi içinde tıklanan düğmenin satır dizinini belirlemeniz gerekiyorsa, aşağıdaki gibi bir kod kullanarak TemplateField içindeki bildirime dayalı sözdiziminde düğme s `CommandArgument` özelliğini el ile ayarlamanız gerekir:  
> `<asp:Button runat="server" ... CommandArgument='<%# CType(Container, GridViewRow).RowIndex %>' />`.

## <a name="summary"></a>Özet

GridView, DetailsView ve FormView denetimleri hepsi, düğme, LinkButtons veya ımagebuttons içerebilir. Bu tür düğmeler tıklandığında, geri göndermeye neden olur ve FormView ve DetailsView denetimlerinde `ItemCommand` olayı ve GridView 'daki `RowCommand` olayını yükseltir. Bu veri Web denetimlerinde, kayıtları silme veya düzenlemeyle ilgili yaygın komutla ilgili eylemleri işlemek için yerleşik işlevlere sahiptir. Ancak, tıklandığı zaman kendi özel kodumuzu yürütme ile yanıt veren düğmeleri de kullanabiliriz.

Bunu gerçekleştirmek için `ItemCommand` veya `RowCommand` olayı için bir olay işleyicisi oluşturmanız gerekir. Bu olay işleyicisinde, hangi düğmenin tıklandığını belirleyip ardından uygun özel eylemi ele almak için ilk olarak gelen `CommandName` değerini denetliyoruz. Bu öğreticide, belirli bir tedarikçiye yönelik tüm ürünleri sona erdirmek veya belirli bir ürünün fiyatını %10 oranında artırmak veya azaltmak için düğmeler ve Buttonalanlarını nasıl kullanacağınızı gördünüz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](adding-and-responding-to-buttons-to-a-gridview-cs.md)
