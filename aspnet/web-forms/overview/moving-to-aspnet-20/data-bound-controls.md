---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Veri Bağlama Denetimleri | Microsoft Dokümanlar
author: rick-anderson
description: Çoğu ASP.NET uygulama, bir arka uç veri kaynağından bir dereceye kadar veri sunumuna dayanır. Veriye bağlı denetimler etkileşim w önemli bir parçası olmuştur ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 941e2ed15b3da28991e7b06cbab570eb1b5b8899
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543086"
---
# <a name="data-bound-controls"></a>Veri Sınırı Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> Çoğu ASP.NET uygulama, bir arka uç veri kaynağından bir dereceye kadar veri sunumuna dayanır. Verilere bağlı denetimler, dinamik Web uygulamalarındaki verilerle etkileşimin önemli bir parçası olmuştur. ASP.NET 2.0, yeni bir BaseDataBoundControl sınıfı ve bildirimsel sözdizimi de dahil olmak üzere veriye bağlı denetimlerde bazı önemli iyileştirmeler sunar.

Çoğu ASP.NET uygulama, bir arka uç veri kaynağından bir dereceye kadar veri sunumuna dayanır. Verilere bağlı denetimler, dinamik Web uygulamalarındaki verilerle etkileşimin önemli bir parçası olmuştur. ASP.NET 2.0, yeni bir BaseDataBoundControl sınıfı ve bildirimsel sözdizimi de dahil olmak üzere veriye bağlı denetimlerde bazı önemli iyileştirmeler sunar.

BaseDataBoundControl, DataBoundControl sınıfı ve HiyerarşikDataBoundControl sınıfının taban sınıfı olarak görev eder. Bu modülde, DataBoundControl'den türeyen aşağıdaki sınıfları tartışacağız:

- Adrotator
- Liste denetimleri
- GridView
- Formview
- Detailsview

HiyerarşikDataBoundControl sınıfından türeyen aşağıdaki sınıfları da tartışacağız:

- TreeView
- Menü
- Sitemappath

## <a name="databoundcontrol-class"></a>DataBoundControl Sınıfı

DataBoundControl sınıfı, tabular veya liste stili verilerle etkileşimkurmak için kullanılan soyut bir sınıftır (VB'de MustInherit olarak işaretlenmiştir). Aşağıdaki denetimler DataBoundControl türetilen denetimlerden bazılarıdır.

## <a name="adrotator"></a>Adrotator

AdRotator denetimi, belirli bir URL'ye bağlı bir Web sayfasında grafik afiş görüntülemenize olanak tanır. Görüntülenen grafik, denetim özellikleri kullanılarak döndürülür. Bir sayfada belirli bir reklamın görüntülenme sıklığı **Gösterim** özelliği kullanılarak yapılandırılabilir ve reklamlar anahtar kelime filtrelekullanılarak filtrelenebilir.

AdRotator denetimleri, veri için bir veritabanında bir XML dosyası veya tablo kullanır. AdRotator denetimini yapılandırmak için xml dosyalarında aşağıdaki öznitelikler kullanılır.

### <a name="imageurl"></a>ımageurl
Reklam için görüntülenecek resmin URL'si.

### <a name="navigateurl"></a>Navigateurl
Reklam tıklandığında kullanıcının alınması gereken URL. Bu URL kodlanmış olmalıdır.

### <a name="alternatetext"></a>Alternatetext
Araç uçlarında görüntülenen ve ekran okuyucular tarafından okunan alternatif metin. ImageUrl tarafından belirtilen görüntü kullanılamadığında da görüntüler.

### <a name="keyword"></a>Anahtar kelime
Anahtar kelime filtreleme kullanırken kullanılabilecek bir anahtar kelime tanımlar. Belirtilmişse, yalnızca anahtar kelime filtresiyle eşleşen bir anahtar kelimeye sahip reklamlar görüntülenir.

### <a name="impressions"></a>Gösterim
Belirli bir reklamın ne sıklıkta görünebildiğini belirleyen bir ağırlık numarası. Aynı dosyadaki diğer reklamların izlenimine göredir. Bir XML dosyasındaki tüm reklamlar için toplu gösterimlerin maksimum değeri 2.048.000.000 1'dir.

### <a name="height"></a>Height
Reklamın piksel olarak yüksekliği.

### <a name="width"></a>Genişlik
Piksel lerde reklamın genişliği.

> [!NOTE]
> Yükseklik ve Genişlik öznitelikleri, AdRotator denetiminin yüksekliğini ve genişliğini geçersiz kılar.

Tipik bir XML dosyası aşağıdaki gibi görünebilir:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

Yukarıdaki örnekte, Gösterim özniteliğinin değeri nedeniyle Contoso'nun reklamı, ASP.NET Web sitesinin reklamından iki kat daha olasıdır.

Yukarıdaki XML dosyasından reklamlar görüntülemek için bir sayfaya Bir AdRotator denetimi ekleyin ve **AdvertisementFile** özelliğini aşağıda gösterildiği gibi XML dosyasına işaret etmek üzere ayarlayın:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

AdRotator denetiminiz için veri kaynağı olarak bir veritabanı tablosu kullanmayı seçerseniz, öncelikle aşağıdaki şemayı kullanarak bir veritabanı kurmanız gerekir:

| **Sütun adı** | **Veri türü** | **Açıklama** |
| --- | --- | --- |
| Kimlik | int | Birincil anahtar. Bu sütunun herhangi bir adı olabilir. |
| ımageurl | nvarchar (*uzunluk*) | Reklam için görüntülenecek resmin göreli veya mutlak URL'si. |
| Navigateurl | nvarchar (*uzunluk*) | Reklamın hedef URL'si. Bir değer sağlamazsanız, reklam bir köprü değildir. |
| Alternatetext | nvarchar (*uzunluk*) | Görüntü bulunamıyorsa görüntülenen metin. Bazı tarayıcılarda metin Araç İpucu olarak görüntülenir. Alternatif metin, grafiği göremeyen kullanıcıların açıklamasının yüksek sesle okunduğunu duyabilmesi için erişilebilirlik için de kullanılır. |
| Anahtar kelime | nvarchar (*uzunluk*) | Sayfanın filtreleyebileceği reklam için bir kategori. |
| Gösterim | int(4) | Reklamın ne sıklıkta görüntülenme olasılığını gösteren bir sayı. Sayı ne kadar büyükse, reklam o kadar sık görüntülenir. XML dosyasındaki tüm gösterim değerlerinin toplamı 2.048.000.000 - 1'i geçemez. |
| Genişlik | int(4) | Görüntünün piksel genişliği. |
| Height | int(4) | Görüntünün piksel yüksekliği. |

Zaten farklı bir şemaya sahip bir veritabanına sahip olduğunuz durumlarda, AdRotator özniteliklerini varolan veritabanınıza eşlemek için **AlternativeTextField,** **ImageUrlField**ve **NavigateUrlField** özelliklerini kullanabilirsiniz. AdRotator denetiminde veritabanındaki verileri görüntülemek için, sayfaya bir veri kaynağı denetimi ekleyin, veri kaynağı denetimi için bağlantı dizesini veritabanınızı gösterecek şekilde yapılandırın ve AdRotator denetiminin **DataSourceID** özelliğini veri kaynağı denetiminin kimliğine ayarlayın. AdRotator reklamlarını programlı olarak yapılandırmanız gereken durumlarda, AdCreated olayını kullanın. AdCreated olayı iki parametre alır; bir nesne ve diğer AdCreatedEventArgs bir örneği. AdCreatedEventArgs, oluşturulan reklama bir göndermedir.

Aşağıdaki kod parçacığı, programlı bir reklam için ImageUrl, NavigateUrl ve AlternativeText'i ayarlar:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Liste Denetimleri

Liste denetimleri ListBox, DropDownList, CheckBoxList, RadioButtonList ve BulletedList içerir. Bu denetimlerin her biri bir veri kaynağına bağlı veri olabilir. Görüntü metni olarak veri kaynağındaki bir alanı kullanırlar ve isteğe bağlı olarak ikinci bir alanı öğenin değeri olarak kullanabilirler. Öğeler tasarım zamanında statik olarak da eklenebilir ve statik öğeleri ve veri kaynağından eklenen dinamik öğeleri karıştırabilirsiniz.

Bir liste denetimini veri bağlamak için sayfaya bir veri kaynağı denetimi ekleyin. Veri kaynağı denetimi için bir SELECT komutu belirtin ve ardından liste denetiminin DataSourceID özelliğini veri kaynağı denetiminin kimliğine ayarlayın. Görüntü metnini ve denetim in değerini tanımlamak için **DataTextField** ve **DataValueField** özelliklerini kullanın. Ayrıca, aşağıdaki gibi ekran metninin görünümünü denetlemek için **DataTextFormatString** özelliğini kullanabilirsiniz:

| **İfadeler** | **Açıklama** |
| --- | --- |
| Fiyat:{0:C} | Sayısal/ondalık veriler için. "Fiyat:" harfini ve ardından para birimi biçiminde ki sayıları görüntüler. Para birimi biçimi, **Sayfa** yönergesi veya Web.config dosyasında kültür özniteliği belirtilen kültür ayarına bağlıdır. |
| {0:D4} | İnteger verileri için. Ondalık sayılarla kullanılamaz. Tamsayılar, dört karakter genişliğinde sıfır yastıklı bir alanda görüntülenir. |
| {0:N2}% | Sayısal veriler için. Sayıyı 2 ondalık basamak hassasiyetiyle görüntüler ve ardından "%". |
| {0:000.0} | Sayısal/ondalık veriler için. Sayılar bir ondalık basamak ta yuvarlanır. Üç basamaktan küçük sayılar sıfır yastıklıdır. |
| {0:D} | Tarih/saat verileri için. Uzun tarih biçimini görüntüler ("Perşembe, 06 Ağustos 1996"). Tarih biçimi, sayfanın veya Web.config dosyasının kültür ayarına bağlıdır. |
| {0:d} | Tarih/saat verileri için. Kısa tarih biçimini görüntüler ("12/31/99"). |
| {0:yy-MM-dd} | Tarih/saat verileri için. Tarihi sayısal yıl-ay-gün biçiminde görüntüler (96-08-06) |

## <a name="gridview"></a>GridView

GridView denetimi, bildirimsel bir yaklaşım kullanarak tabular veri görüntüleme ve düzenleme sağlar ve DataGrid denetiminin halefidir. Aşağıdaki özellikler GridView denetiminde kullanılabilir.

- SqlDataSource gibi veri kaynağı denetimlerine bağlama.
- Dahili sıralama yetenekleri.
- Yerleşik güncelleme ve silme özellikleri.
- Dahili sayfalama yetenekleri.
- Yerleşik satır seçim yetenekleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek ve benzeri şekilde GridView nesne modeline programlı erişim.
- Birden çok anahtar alanı.
- Köprü sütunları için birden çok veri alanı.
- Temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

**Sütun Alanları**

GridView denetimindeki her sütun bir DataControlField nesnesi tarafından temsil edilir. Varsayılan olarak, AutoGenerateColumns özelliği **gerçek**olarak ayarlanır, bu da veri kaynağındaki her alan için bir AutoGenerateField nesnesi oluşturur. Her alan daha sonra, her alanın veri kaynağında görünmesi sırasına göre GridView denetiminde bir sütun olarak işlenir. Ayrıca, **AutoGenerateColumns** özelliğini **false** olarak ayarlayarak ve sonra kendi sütun alanı koleksiyonunuzu tanımlayarak **GridView** denetiminde hangi sütun alanlarının göründüğünü el ile denetleyebilirsiniz. Farklı sütun alanı türleri denetimdeki sütunların davranışını belirler.

Aşağıdaki tabloda kullanılabilecek farklı sütun alanı türleri listelenilir.

| **Sütun alan türü** | **Açıklama** |
| --- | --- |
| Boundfield | Bir alanın değerini bir veri kaynağında görüntüler. Bu GridView denetiminin varsayılan sütun türüdür. |
| Buttonfield | GridView denetimindeki her öğe için bir komut düğmesi görüntüler. Bu, Ekle veya Kaldır düğmesi gibi özel düğme denetimlerinden oluşan bir sütun oluşturmanıza olanak tanır. |
| Checkboxfield | GridView denetimindeki her öğe için bir onay kutusu görüntüler. Bu sütun alanı türü genellikle Boolean değeri olan alanları görüntülemek için kullanılır. |
| Commandfield | Seçme, düzenleme veya silme işlemlerini gerçekleştirmek için önceden tanımlanmış komut düğmelerini görüntüler. |
| Hyperlinkfield | Veri kaynağındaki bir alanın değerini köprü olarak görüntüler. Bu sütun alanı türü, ikinci bir alanı köprünün URL'sine bağlamanızı sağlar. |
| ımagefield | GridView denetimindeki her öğe için bir görüntü görüntüler. |
| Templatefield | GridView denetimindeki her öğe için kullanıcı tanımlı içeriği belirtilen şablona göre görüntüler. Bu sütun alanı türü, özel bir sütun alanı oluşturmanıza olanak sağlar. |

Bir sütun alanı koleksiyonunu açıklayıcı bir şekilde tanımlamak için, önce GridView denetiminin açılış ve kapanış etiketleri arasına ** &lt;Sütunlar&gt; ** etiketlerini açma ve kapatma ekleyin. Ardından, açılış ve kapanış ** &lt;Sütunları&gt; ** etiketleri arasına eklemek istediğiniz sütun alanlarını listele. Belirtilen sütunlar listelenen sırada Sütunlar koleksiyonuna eklenir. **Sütunlar** koleksiyonu denetimdeki tüm sütun alanlarını depolar ve GridView denetimindeki sütun alanlarını programlı bir şekilde yönetmenize olanak tanır.

Açıkça bildirilen sütun alanları otomatik olarak oluşturulan sütun alanlarıyla birlikte görüntülenebilir. Her ikisi de kullanıldığında, açıkça bildirilen sütun alanları önce işlenir ve ardından otomatik olarak oluşturulan sütun alanları oluşturulur.

## <a name="binding-to-data"></a>Verilere Bağlama

GridView denetimi bir veri kaynağı denetimine **(SqlDataSource,** **ObjectDataSource**vb. gibi) ve System.Collections.Imenumerable arabirimini (System.Data.DataView, System.Collections.ArrayList veya System.Collections.Hashtable gibi) uygulayan herhangi bir veri kaynağına bağlanabilir. GridView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Bir veri kaynağı denetimine bağlamak için GridView denetiminin DataSourceID özelliğini veri kaynağı denetiminin kimlik değerine ayarlayın. GridView denetimi otomatik olarak belirtilen veri kaynağı denetimine bağlanır ve sıralama, güncelleştirme, silme ve arama işlevlerini gerçekleştirmek için veri kaynağı denetiminin özelliklerinden yararlanabilir. Bu, verilere bağlamak için tercih edilen yöntemdir.
- System.Collections.IEnumerable arabirimini uygulayan bir veri kaynağına bağlamak için GridView denetiminin DataSource özelliğini programlı olarak veri kaynağına ayarlayın ve ardından DataBind yöntemini arayın. Bu yöntemi kullanırken, GridView denetimi yerleşik sıralama, güncelleştirme, silme ve sayfalama işlevleri sağlamaz. Bu işlevselliği kendiniz sağlamanız gerekir.

## <a name="data-operations"></a>Veri İşlemleri

GridView denetimi, kullanıcının denetimdeki öğeler aracılığıyla sıralamasına, güncelleştirmesine, silmesine, seçmesine ve sayfaatmasını sağlayan birçok yerleşik özellik sağlar. GridView denetimi bir veri kaynağı denetimine bağlandığında, GridView denetimi veri kaynağı denetiminin özelliklerinden yararlanabilir ve otomatik sıralama, güncelleştirme ve silme işlevleri sağlayabilir.

> [!NOTE]
> GridView denetimi, diğer veri kaynakları türleri ile sıralama, güncelleştirme ve silme desteği sağlayabilir; ancak, bu işlemler için uygulama ile uygun bir olay işleyicisi sağlamanız gerekir.

Sıralama, kullanıcının Sütunun üstbilgisini tıklatarak gridview denetimindeki öğeleri belirli bir sütuna göre sıralamasına olanak tanır. Sıralamayı etkinleştirmek için İzin Sıralaması özelliğini **doğru**olarak ayarlayın.

**ButtonField** veya **TemplateField** sütun alanında sırasıyla "Düzenle", "Sil" ve "Seç" komut adıyla bir düğme tıklatıldığında otomatik güncelleştirme, silme ve seçim işlevleri etkinleştirilir. GridView denetimi, AutoGenerateEditButton, AutoGenerateDeleteButton veya AutoGenerateSelectButton özelliği sırasıyla **doğru**olarak ayarlanmışsa, Bir Edit, Sil veya Seç düğmesi ile otomatik olarak bir **CommandField** sütun alanı ekleyebilirsiniz.

> [!NOTE]
> Veri kaynağına kayıt eklemek GridView denetimi tarafından doğrudan desteklenmez. Ancak, DetailsView veya FormView denetimi ile birlikte GridView denetimini kullanarak kayıtları eklemek mümkündür.

GridView denetimi, tüm kayıtları veri kaynağında aynı anda görüntülemek yerine, kayıtları otomatik olarak sayfalara ayırabilir. Sayfalamayı etkinleştirmek için AllowPaging özelliğini **doğru**olarak ayarlayın.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümleri için stil özelliklerini ayarlayarak GridView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelendir.

| **Stil özelliği** | **Açıklama** |
| --- | --- |
| AlternatifRowStyle | GridView denetiminde alternatif veri satırları için stil ayarları. Bu özellik ayarlandığında, veri satırları RowStyle ayarları ile **AlternatifRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| EditRowStyle | GridView denetiminde düzenlenen satırın stil ayarları. |
| Emptydatarowstyle | Veri kaynağı herhangi bir kayıt içermiyorsa GridView denetiminde görüntülenen boş veri satırının stil ayarları. |
| Footerstyle | GridView denetiminin altbilgi satırının stil ayarları. |
| Headerstyle | GridView denetiminin üstbilgi satırının stil ayarları. |
| Pagerstyle | GridView denetiminin çağrı sırasının stil ayarları. |
| Rowstyle | GridView denetimindeki veri satırlarının stil ayarları. **AlternatingRowStyle** özelliği de ayarlandığında, veri satırları **RowStyle** ayarları ile **AlternatifRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| SelectedRowStyle | GridView denetiminde seçili satırın stil ayarları. |

Denetimin farklı bölümlerini gösterebilir veya gizleyebilirsiniz. Aşağıdaki tabloda, hangi parçaların gösterildiğini veya gizlendiğini denetleyen özellikler listelenir.

| **Özellik** | **Açıklama** |
| --- | --- |
| Showfooter | GridView denetiminin altbilgi bölümünü gösterir veya gizler. |
| Showheader | GridView denetiminin üstbilgi bölümünü gösterir veya gizler. |

### <a name="events"></a>Olaylar

GridView denetimi, karşı programlayabileceğiniz çeşitli olaylar sağlar. Bu, bir olay olduğunda özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda GridView denetimi tarafından desteklenen olaylar listelenmektedir.

| **Olay** | **Açıklama** |
| --- | --- |
| Pageındexchanged | Çağrı cihazı düğmelerinden biri tıklatıldığında oluşur, ancak GridView denetiminden sonra çağrılama işlemi gerçekleşir. Bu olay genellikle, kullanıcı denetimde farklı bir sayfaya gidince görev gerçekleştirmeniz gerektiğinde kullanılır. |
| Pageındexchanging | Çağrı cihazı düğmelerinden biri tıklatıldığında, gridview denetimi sayfalama işlemini işlemeden önce oluşur. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |
| SatırİptalEdit | Bir satırın İptal düğmesi tıklatıldığında, ancak GridView denetimi denetim ediş modundan çıkmadan önce oluşur. Bu olay genellikle iptal işlemini durdurmak için kullanılır. |
| Rowcommand | GridView denetiminde bir düğme tıklatıldığında oluşur. Bu olay genellikle denetimde bir düğme tıklatıldığında bir görevi gerçekleştirmek için kullanılır. |
| Rowcreated | GridView denetiminde yeni bir satır oluşturulduğunda oluşur. Bu olay genellikle satır oluşturulduğunda bir satırın içeriğini değiştirmek için kullanılır. |
| SatırDataBound | GridView denetiminde bir veri satırı verilere bağlandığında oluşur. Bu olay genellikle satır verilere bağlı olduğunda bir satırın içeriğini değiştirmek için kullanılır. |
| Rowdeleted | Bir satırın Sil düğmesi tıklatıldığında oluşur, ancak GridView denetiminden sonra kayıt veri kaynağından silinir. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| Rowdeleting | Bir satırın Sil düğmesi tıklatıldığında, ancak GridView denetimi kaydı veri kaynağından silmeden önce oluşur. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| Rowediting | Bir satırın Edit düğmesi tıklatıldığında, ancak GridView denetimi edit moduna girmeden önce oluşur. Bu olay genellikle düzenleme işlemini iptal etmek için kullanılır. |
| Rowupdated | Bir satırın Güncelleştirme düğmesi tıklatıldığında oluşur, ancak GridView denetiminden sonra satır güncellenir. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| Rowupdating | Bir satırın Güncelleştirme düğmesi tıklatıldığında, ancak GridView denetimi satırı güncelleştirmeden önce oluşur. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| Selectedındexchanged | Bir satırın Seç düğmesi tıklatıldığında oluşur, ancak GridView denetiminden sonra select işlemi işler. Bu olay genellikle denetimde bir satır seçildikten sonra bir görevi gerçekleştirmek için kullanılır. |
| Selectedındexchanging | Bir satırın Seç düğmesi tıklatıldığında, ancak GridView denetimi select işlemini işlemeden önce oluşur. Bu olay genellikle seçim işlemini iptal etmek için kullanılır. |
| Sıra -lanmış | Bir sütunu sıralamak için köprü tıklatıldığında oluşur, ancak GridView denetiminden sonra sıralama işlemini işler. Bu olay genellikle bir sütun sıralamak için bir köprü üzerinde kullanıcı tıkladığı sonra bir görevi gerçekleştirmek için kullanılır. |
| Sıralama | Bir sütunu sıralamak için köprü tıklatıldığında, ancak GridView denetimi sıralama işlemini işlemeden önce oluşur. Bu olay genellikle sıralama işlemini iptal etmek veya özel bir sıralama yordamı gerçekleştirmek için kullanılır. |

## <a name="formview"></a>Formview

FormView denetimi, bir veri kaynağından tek bir kaydı görüntülemek için kullanılır. Satır alanları yerine kullanıcı tanımlı şablonlar görüntülemesi dışında DetailsView denetimine benzer. Kendi şablonlarınızı oluşturmak, verilerin nasıl görüntüleneceğini denetlemede size daha fazla esneklik sağlar. FormView denetimi aşağıdaki özellikleri destekler:

- SqlDataSource ve ObjectDataSource gibi veri kaynağı denetimlerine bağlama.
- Dahili ekleme yetenekleri.
- Yerleşik güncelleme ve silme özellikleri.
- Dahili sayfalama yetenekleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek ve benzeri için FormView nesne modeline programlı erişim.
- Kullanıcı tanımlı şablonlar, temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

## <a name="templates"></a>Şablonlar

FormView denetiminin içeriği görüntülemesi için denetimin farklı bölümleri için şablonlar oluşturmanız gerekir. Çoğu şablon isteğe bağlıdır; ancak, denetimin yapılandırıldığı mod için bir şablon oluşturmanız gerekir. Örneğin, kayıtları eklemeyi destekleyen bir FormView denetiminin bir ekleme öğesi şablonu tanımlanmış olması gerekir. Aşağıdaki tabloda oluşturabileceğiniz farklı şablonlar listelenir.

| **Şablon türü** | **Açıklama** |
| --- | --- |
| Editıtemtemplate | FormView denetimi edit modundayken veri satırının içeriğini tanımlar. Bu şablon genellikle kullanıcının varolan bir kaydı edinebileceği giriş denetimleri ve komut düğmeleri içerir. |
| Emptydatatemplate | FormView denetimi herhangi bir kayıt içermeyen bir veri kaynağına bağlandığında görüntülenen boş veri satırının içeriğini tanımlar. Bu şablon genellikle kullanıcıyı veri kaynağının herhangi bir kayıt içermediği konusunda uyarmak için içerik içerir. |
| Footertemplate | Altbilgi satırının içeriğini tanımlar. Bu şablon genellikle altbilgi satırında görüntülemek istediğiniz ek içeriği içerir. Alternatif olarak, Altbilgi metnini Altbilgi özelliğini ayarlayarak altbilgi satırında görüntülemek üzere belirtebilirsiniz. |
| Headertemplate | Üstbilgi satırının içeriğini tanımlar. Bu şablon genellikle üstbilgi satırında görüntülemek istediğiniz ek içeriği içerir. Alternatif olarak, Üstbilgi Metni özelliğini ayarlayarak üstbilgi satırında görüntülenecek metni belirtmeniz yeterlidir. |
| ıtemtemplate | FormView denetimi salt okunur modundayken veri satırının içeriğini tanımlar. Bu şablon genellikle varolan bir kaydın değerlerini görüntülemek için içerik içerir. |
| ınsertıtemtemplate | FormView denetimi ekleme modundayken veri satırının içeriğini tanımlar. Bu şablon genellikle kullanıcının yeni bir kayıt ekleyebileceği giriş denetimleri ve komut düğmeleri içerir. |
| Pagertemplate | Çağrı özelliği etkinleştirildiğinde görüntülenen çağrı cihazı satırının içeriğini tanımlar (AllowPaging özelliği **doğru**ayarlandığında). Bu şablon genellikle kullanıcının başka bir kayda gidebileceği denetimleri içerir. |

Düzenleme öğesi şablonundaki giriş denetimleri ve madde ekleme şablonu, iki yönlü bağlama ifadesi kullanılarak veri kaynağının alanlarına bağlanabilir. Bu, FormView denetiminin bir güncelleştirme veya ekleme işlemi için giriş denetimideğerlerini otomatik olarak ayıklamasına olanak tanır. İki yönlü bağlama ifadeleri, bir edit öğesi şablonundaki giriş denetimlerinin özgün alan değerlerini otomatik olarak görüntülemesine de olanak sağlar.

### <a name="binding-to-data"></a>Verilere Bağlama

FormView denetimi bir veri kaynağı denetimine **(SqlDataSource, AccessDataSource,** **ObjectDataSource** vb. gibi) veya System.Collections.Imumerable arabirimini (System.DataView, System.Collections.ArrayList ve System.Collections.Hashtable gibi) uygulayan herhangi bir veri kaynağına bağlanabilir. FormView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Veri kaynağı denetimine bağlamak için, FormView denetiminin DataSourceID özelliğini veri kaynağı denetiminin kimlik değerine ayarlayın. FormView denetimi otomatik olarak belirtilen veri kaynağı denetimine bağlanır ve ekleme, güncelleştirme, silme ve arama işlevlerini gerçekleştirmek için veri kaynağı denetiminin özelliklerinden yararlanabilir. Bu, verilere bağlamak için tercih edilen yöntemdir.
- **System.Collections.IEnumerable** arabirimini uygulayan bir veri kaynağına bağlamak için, FormView denetiminin DataSource özelliğini programlı olarak veri kaynağına ayarlayın ve ardından DataBind yöntemini arayın. Bu yöntemi kullanırken, FormView denetimi yerleşik ekleme, güncelleştirme, silme ve sayfalama işlevleri sağlamaz. Uygun olayı kullanarak bu işlevselliği sağlamanız gerekir.

## <a name="data-operations"></a>Veri İşlemleri

FormView denetimi, kullanıcının denetimdeki öğeler aracılığıyla güncelleştirmesine, silmesine, eklemesine ve sayfaya geçmesine olanak tanıyan birçok yerleşik özellik sağlar. FormView denetimi bir veri kaynağı denetimine bağlandığında, FormView denetimi veri kaynağı denetiminin özelliklerinden yararlanabilir ve otomatik güncelleştirme, silme, ekleme ve sayfalama işlevleri sağlayabilir. FormView denetimi, diğer veri kaynakları yla güncelleştirme, silme, ekleme ve sayfalama işlemleri için destek sağlayabilir; ancak, bu işlemler için uygulama ile uygun bir olay işleyicisi sağlamanız gerekir.

FormView denetimi şablonlar kullandığından, güncelleştirme, silme veya ekleme işlemleri gerçekleştirmek için komut düğmelerini otomatik olarak oluşturmanın bir yolunu sağlamaz. Bu komut düğmelerini uygun şablona el ile eklemeniz gerekir. FormView denetimi, **CommandName** özellikleri belirli değerlere ayarlanmış belirli düğmeleri tanır. Aşağıdaki tabloda FormView denetiminin tanıdığı komut düğmeleri listelenistır.

| **Düğme** | **Komut adı değeri** | **Açıklama** |
| --- | --- | --- |
| İptal | "İptal Et" | İşlemi iptal etmek ve kullanıcı tarafından girilen değerleri atmak için işlemleri güncelleştirmeveya eklemede kullanılır. FormView denetimi daha sonra Varsayılan Mod özelliği tarafından belirtilen moda döner. |
| Sil | "Sil" | Görüntülenen kaydı veri kaynağından silmek için silme işlemlerinde kullanılır. ItemDeleting ve ItemDeleted olayları yükseltir. |
| Düzenle | "Edit" | FormView denetimini edit moduna koymak için işlemleri güncelleştirmede kullanılır. **EditItemTemplate** özelliğinde belirtilen içerik veri satırı için görüntülenir. |
| Ekle | "Ekle" | Kullanıcı tarafından sağlanan değerleri kullanarak veri kaynağına yeni bir kayıt eklemeye çalışmak için ekleme işlemleri kullanılır. ItemIning ve ItemInsed olayları yükseltir. |
| Yeni | "Yeni" | FormView denetimini ekleme moduna sokmak için ekleme işlemlerinde kullanılır. **InsertItemTemplate** özelliğinde belirtilen içerik veri satırı için görüntülenir. |
| Sayfa | "Sayfa" | Sayfalama işlemlerinde çağrı lama yapan çağrı cihazı satırındaki bir düğmeyi temsil etmek için kullanılır. Sayfalama işlemini belirtmek için, düğmenin **CommandArgument** özelliğini "Next", "Prev", "First", "Last" veya gezinmek için sayfanın dizinine ayarlayın. PageIndexChanging ve PageIndexChanged olaylarını yükseltir. |
| Güncelleştirme | "Güncelleme" | Veri kaynağında görüntülenen kaydı kullanıcı tarafından sağlanan değerlerle güncelleştirmeye çalışmak için işlemleri güncelleştirmede kullanılır. ItemGüncelleme ve ItemUpdated olayları yükseltir. |

Sil düğmesinin aksine (görüntülenen kaydı hemen siler), Düzenle veya Yeni düğmesine tıklandığında, FormView denetimi sırasıyla düzenle veya ekle moduna geçer. EditItemTemplate özelliğinde bulunan içerik, geçerli veri öğesi için **editItemtemplate** özelliğinde yer alan içerik olarak görüntülenir. Genellikle, edit öğesi şablonu, Edit düğmesinin bir Güncelleştirme ve İptal düğmesiyle değiştirilecek şekilde tanımlanır. Alanın veri türüne (TextBox veya CheckBox denetimi gibi) uygun giriş denetimleri de genellikle kullanıcının değiştirmesi için bir alanın değeriyle görüntülenir. Güncelleştirme düğmesini tıklattığınızda veri kaynağındaki kayıt güncellenirken İptal düğmesini tıklatmak tüm değişiklikleri terk eder.

Aynı şekilde, **InsertItemTemplate** özelliğinde bulunan içerik, denetim ekleme modundayken veri öğesi için görüntülenir. Ekle öğesi şablonu genellikle Yeni düğme bir Ekle ve İptal düğmesi ile değiştirilir ve boş giriş denetimleri kullanıcı için yeni kayıt değerlerini girmek için görüntülenir şekilde tanımlanır. Ekle düğmesine tıkladığınızda, veri kaynağına kayıt eklenir, İptal düğmesini tıklatmak ise değişiklikleri terk eder.

FormView denetimi, kullanıcının veri kaynağındaki diğer kayıtlara gitmesini sağlayan bir sayfalama özelliği sağlar. Etkinleştirildiğinde, sayfa gezinti denetimlerini içeren FormView denetiminde bir çağrı sayfası satırı görüntülenir. Sayfalamayı etkinleştirmek için **AllowPaging** özelliğini **doğru**olarak ayarlayın. PagerStyle ve PagerSettings özelliğinde bulunan nesnelerin özelliklerini ayarlayarak çağrı cihazı satırını özelleştirebilirsiniz. Yerleşik çağrı cihazı satırı ui'sini kullanmak yerine, **PagerTemplate** özelliğini kullanarak kendi UI'nizi oluşturabilirsiniz.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümleri için stil özelliklerini ayarlayarak FormView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelendir.

| **Stil özelliği** | **Açıklama** |
| --- | --- |
| EditRowStyle | FormView denetimi edit modundayken veri satırının stil ayarları. |
| Emptydatarowstyle | Veri kaynağı herhangi bir kayıt içermiyorsa FormView denetiminde görüntülenen boş veri satırının stil ayarları. |
| Footerstyle | FormView denetiminin altbilgi satırının stil ayarları. |
| Headerstyle | FormView denetiminin üstbilgi satırının stil ayarları. |
| InsertRowStyle | FormView denetimi ekleme modundayken veri satırının stil ayarları. |
| Pagerstyle | Çağrı özelliği etkinleştirildiğinde FormView denetiminde görüntülenen çağrı sayfası satırının stil ayarları. |
| Rowstyle | FormView denetimi salt okunur modundayken veri satırının stil ayarları. |

## <a name="events"></a>Olaylar

FormView denetimi, karşı programlayabileceğiniz çeşitli olaylar sağlar. Bu, bir olay olduğunda özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda FormView denetimi tarafından desteklenen olaylar listelenmektedir.

| **Olay** | **Açıklama** |
| --- | --- |
| ıtemcommand | FormView denetimi içindeki bir düğme tıklatıldığında oluşur. Bu olay genellikle denetimde bir düğme tıklatıldığında bir görevi gerçekleştirmek için kullanılır. |
| ıtemcreated | Tüm FormViewRow nesneleri FormView denetiminde oluşturulduktan sonra oluşur. Bu olay genellikle görüntülenmeden önce bir kaydın değerlerini değiştirmek için kullanılır. |
| ıtemdeleted | Sil düğmesi **(CommandName** özelliği "Delete" olarak ayarlandığında) tıklandığında, ancak FormView denetiminden sonra kaydı veri kaynağından sildiği ortaya çıkar. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemdeleting | Sil düğmesi tıklatıldığında oluşur, ancak FormView denetimi kaydı veri kaynağından silmeden önce. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| ıtemınserted | Bir Ekle düğmesi **(CommandName** özelliği "Ekle" olarak ayarlanmış bir düğme) tıklatıldığında, ancak FormView denetimi kaydı ekledikten sonra oluşur. Bu olay genellikle ekleme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemınserting | Bir Ekle düğmesi tıklatıldığında, ancak FormView denetimi kaydı eklemeden önce oluşur. Bu olay genellikle ekleme işlemini iptal etmek için kullanılır. |
| ıtemupdated | Bir Güncelleştirme düğmesi **(CommandName** özelliği "Güncelleştirme" olarak ayarlanmış bir düğme) tıklatıldığında, ancak FormView denetimi satırı güncelleştirdikten sonra oluşur. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemupdating | Bir Güncelleştirme düğmesi tıklatıldığında, ancak FormView denetimi kaydı güncelleştirmeden önce oluşur. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| Modechanged | FormView denetimi modları değiştirdikten sonra oluşur (yalnızca salt okuma modunu edin, eklemek veya salt okunur modu nu oluşturmak için). Bu olay genellikle FormView denetimi modları değiştirdiğinde bir görevi gerçekleştirmek için kullanılır. |
| Modechanging | FormView denetimi modları değiştirmeden önce oluşur (yalnızca salt okuma modunu oluşturmak, eklemek veya salt okunur modu nu oluşturmak için). Bu olay genellikle bir mod değişikliğini iptal etmek için kullanılır. |
| Pageındexchanged | Çağrı cihazı düğmelerinden biri tıklatıldığında oluşur, ancak FormView denetiminden sonra çağrılama işlemi gerçekleşir. Bu olay genellikle, kullanıcı denetimde farklı bir kayda geçtikten sonra bir görevi gerçekleştirmeniz gerektiğinde kullanılır. |
| Pageındexchanging | Çağrı cihazı düğmelerinden biri tıklatıldığında, ancak FormView denetimi çağrı işlemini işlemeden önce oluşur. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |

## <a name="detailsview"></a>Detailsview

DetailsView denetimi, kaydın her alanının tablonun bir satırında görüntülendiği bir tablodaki bir veri kaynağından tek bir kaydı görüntülemek için kullanılır. Ana ayrıntı senaryoları için GridView denetimi ile birlikte kullanılabilir. DetailsView denetimi aşağıdaki özellikleri destekler:

- SqlDataSource gibi veri kaynağı denetimlerine bağlama.
- Dahili ekleme yetenekleri.
- Yerleşik güncelleme ve silme özellikleri.
- Dahili sayfalama yetenekleri.
- Özellikleri dinamik olarak ayarlamak, olayları işlemek ve benzeri için DetailsView nesne modeline programlı erişim.
- Temalar ve stiller aracılığıyla özelleştirilebilir görünüm.

## <a name="row-fields"></a>Satır Alanları

DetailsView denetimindeki her veri satırı bir alan denetimi belirtilerek oluşturulur. Farklı satır alanı türleri denetimdeki satırların davranışını belirler. Alan denetimleri DataControlField'dan türetilmiştir. Aşağıdaki tabloda kullanılabilecek farklı satır alanı türleri listelenilir.

| **Sütun alan türü** | **Açıklama** |
| --- | --- |
| Boundfield | Veri kaynağındaki bir alanın değerini metin olarak görüntüler. |
| Buttonfield | DetailsView denetiminde bir komut düğmesi görüntüler. Bu, Ekle veya Kaldır düğmesi gibi özel bir düğme denetimiyle bir satır görüntülemenize olanak tanır. |
| Checkboxfield | DetailsView denetiminde bir onay kutusu görüntüler. Bu satır alanı türü genellikle Boolean değeri olan alanları görüntülemek için kullanılır. |
| Commandfield | DetailsView denetiminde işlemleri düzenlemek, eklemek veya silmek için yerleşik komut düğmelerini görüntüler. |
| Hyperlinkfield | Veri kaynağındaki bir alanın değerini köprü olarak görüntüler. Bu satır alanı türü, ikinci bir alanı köprünün URL'sine bağlamanızı sağlar. |
| ımagefield | DetailsView denetiminde bir görüntü görüntüler. |
| Templatefield | AyrıntılarGörünümü denetiminde belirtilen şablona göre bir satır için kullanıcı tanımlı içeriği görüntüler. Bu satır alanı türü özel bir satır alanı oluşturmanıza olanak sağlar. |

Varsayılan olarak, AutoGenerateRows özelliği **gerçek**olarak ayarlanır, hangi otomatik olarak veri kaynağında bağlanabilir türünden her alan için bağlı bir satır alanı nesnesi oluşturur. Geçerli bağlanabilir türleri String, DateTime, Ondalık, Guid ve ilkel türleri kümesidir. Her alan daha sonra, her alanın veri kaynağında göründüğü sırada metin olarak bir satırda görüntülenir.

Satırları otomatik olarak oluşturmak, kayıttaki her alanı görüntülemek için hızlı ve kolay bir yol sağlar. Ancak, DetailsView denetiminin gelişmiş özelliklerinden yararlanmak için satır alanlarını DetailsView denetimine dahil etmek üzere açıkça beyan etmelisiniz. Satır alanlarını bildirmek için, önce **AutoGenerateRows** özelliğini **false**olarak ayarlayın. Ardından, DetailsView denetiminin açılış ve kapanış etiketleri arasına ** &lt;Fields&gt; ** etiketlerini açma ve kapatma ekleyin. Son olarak, açılış ve kapatma ** &lt;Alanları&gt; ** etiketleri arasına eklemek istediğiniz satır alanlarını listele. Belirtilen satır alanları listelenen sırada Alanlar koleksiyonuna eklenir. **Alanlar** koleksiyonu, DetailsView denetimindeki satır alanlarını programlı bir şekilde yönetmenize olanak tanır.

> [!NOTE]
> Otomatik olarak oluşturulan satır alanları Alanlar koleksiyonuna eklenmez.

## <a name="binding-to-data"></a>Verilere Bağlama

DetailsView denetimi, **SqlDataSource** veya AccessDataSource gibi bir veri kaynağı denetimine veya System.Data.DataView, System.Collections.ArrayList ve System.Collections.Hashtable gibi System.Collections.Imumerable arabirimini uygulayan herhangi bir veri kaynağına bağlanabilir.

DetailsView denetimini uygun veri kaynağı türüne bağlamak için aşağıdaki yöntemlerden birini kullanın:

- Veri kaynağı denetimine bağlamak için DetailsView denetiminin DataSourceID özelliğini veri kaynağı denetiminin kimlik değerine ayarlayın. DetailsView denetimi otomatik olarak belirtilen veri kaynağı denetimine bağlanır. Bu, verilere bağlamak için tercih edilen yöntemdir.
- **System.Collections.IEnumerable** arabirimini uygulayan bir veri kaynağına bağlamak için, DetailsView denetiminin DataSource özelliğini programlı olarak veri kaynağına ayarlayın ve ardından DataBind yöntemini arayın.

## <a name="security"></a>Güvenlik

Bu denetim, kötü amaçlı istemci komut dosyası içerebilir kullanıcı girişi görüntülemek için kullanılabilir. Uygulamanızda görüntülemeden önce yürütülebilir komut dosyası, SQL deyimleri veya başka bir kod için istemciden gönderilen tüm bilgileri denetleyin. ASP.NET, kullanıcı girişinde komut dosyası ve HTML'yi engellemek için bir giriş isteği doğrulama özelliği sağlar.

## <a name="data-operations"></a>Veri İşlemleri

DetailsView denetimi, kullanıcının denetimdeki öğeler aracılığıyla güncelleştirmesine, silmesine, eklemesine ve sayfaya geçmesine olanak tanıyan yerleşik özellikler sağlar. DetailsView denetimi bir veri kaynağı denetimine bağlandığında, DetailsView denetimi veri kaynağı denetiminin özelliklerinden yararlanabilir ve otomatik güncelleştirme, silme, ekleme ve sayfalama işlevleri sağlayabilir.

DetailsView denetimi, diğer veri kaynaklarıyla güncelleştirme, silme, ekleme ve sayfalama işlemleri için destek sağlayabilir; ancak, bu işlemler için uygulamayı uygun bir olay işleyicisi olarak sağlamanız gerekir.

DetailsView denetimi, AutoGenerateEditButton, AutoGenerateDeleteButton veya AutoGenerateInsertButton özelliklerini **sırasıyla doğru**olarak ayarlayarak otomatik olarak Bir Düzenleme, Silme veya Yeni düğme ile **CommandField** satır alanı ekleyebilirsiniz. Sil düğmesinin aksine (seçili kaydı hemen siler), Düzenle veya Yeni düğmesine tıklandığında, DetailsView denetimi sırasıyla düzenle veya ekle moduna geçer. Edit modunda, Edit düğmesi bir Güncelleştirme ve İptal düğmesiyle değiştirilir. Alanın veri türüne (TextBox veya CheckBox denetimi gibi) uygun giriş denetimleri, kullanıcının değiştirmesi için bir alanın değeriyle görüntülenir. Güncelleştirme düğmesini tıklattığınızda veri kaynağındaki kayıt güncellenirken İptal düğmesini tıklatmak tüm değişiklikleri terk eder. Aynı şekilde, ekle modunda Yeni düğmesi bir Ekle ve İptal düğmesiyle değiştirilir ve kullanıcının yeni kayıt değerlerini girebilmek için boş giriş denetimleri görüntülenir.

DetailsView denetimi, kullanıcının veri kaynağındaki diğer kayıtlara gitmesini sağlayan bir sayfalama özelliği sağlar. Etkinleştirildiğinde, sayfa gezinti denetimleri çağrı cihazı satırında görüntülenir. Sayfalamayı etkinleştirmek için AllowPaging özelliğini **doğru**olarak ayarlayın. Çağrı sayfası satırı PagerStyle ve PagerSettings özellikleri kullanılarak özelleştirilebilir.

## <a name="customizing-the-user-interface"></a>Kullanıcı Arabirimini Özelleştirme

Denetimin farklı bölümleri için stil özelliklerini ayarlayarak DetailsView denetiminin görünümünü özelleştirebilirsiniz. Aşağıdaki tabloda farklı stil özellikleri listelendir.

| **Stil özelliği** | **Açıklama** |
| --- | --- |
| AlternatifRowStyle | DetailsView denetiminde alternatif veri satırlarıiçin stil ayarları. Bu özellik ayarlandığında, veri satırları RowStyle ayarları ile **AlternatifRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| CommandRowStyle | DetailsView denetiminde yerleşik komut düğmelerini içeren satırın stil ayarları. |
| EditRowStyle | DetailsView denetimi edit modundayken veri satırlarının stil ayarları. |
| Emptydatarowstyle | Veri kaynağı herhangi bir kayıt içermiyorsa Ayrıntılar Görünümü denetiminde görüntülenen boş veri satırının stil ayarları. |
| Footerstyle | DetailsView denetiminin altbilgi satırının stil ayarları. |
| Headerstyle | DetailsView denetiminin üstbilgi satırının stil ayarları. |
| InsertRowStyle | DetailsView denetimi ekleme modundayken veri satırlarının stil ayarları. |
| Pagerstyle | DetailsView denetiminin çağrı sayfası satırının stil ayarları. |
| Rowstyle | DetailsView denetimindeki veri satırlarının stil ayarları. **AlternatingRowStyle** özelliği de ayarlandığında, veri satırları **RowStyle** ayarları ile **AlternatifRowStyle** ayarları arasında dönüşümlü olarak görüntülenir. |
| FieldHeaderStyle | DetailsView denetiminin üstbilgi sütununun stil ayarları. |

## <a name="events"></a>Olaylar

DetailsView denetimi, karşı programlayabileceğiniz çeşitli olaylar sağlar. Bu, bir olay olduğunda özel bir yordam çalıştırmanızı sağlar. Aşağıdaki tabloda DetailsView denetimi tarafından desteklenen olaylar listelenmektedir. DetailsView denetimi bu olayları temel sınıflarından da devralır: DataBinding, DataBound, Dispose, Init, Load, PreRender ve Render.

| **Olay** | **Açıklama** |
| --- | --- |
| ıtemcommand | DetailsView denetiminde bir düğme tıklatıldığında oluşur. |
| ıtemcreated | Tüm DetailsViewRow nesneleri DetailsView denetiminde oluşturulduktan sonra oluşur. Bu olay genellikle görüntülenmeden önce bir kaydın değerlerini değiştirmek için kullanılır. |
| ıtemdeleted | Sil düğmesi tıklatıldığında oluşur, ancak DetailsView denetiminden sonra kayıt veri kaynağından silinir. Bu olay genellikle silme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemdeleting | Sil düğmesi tıklatıldığında oluşur, ancak DetailsView denetimi kaydı veri kaynağından silmeden önce. Bu olay genellikle silme işlemini iptal etmek için kullanılır. |
| ıtemınserted | Bir Ekle düğmesi tıklatıldığında oluşur, ancak DetailsView denetimi nden sonra kayıt eklenir. Bu olay genellikle ekleme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemınserting | Bir Ekle düğmesi tıklatıldığında, ancak DetailsView denetimi kaydı eklemeden önce oluşur. Bu olay genellikle ekleme işlemini iptal etmek için kullanılır. |
| ıtemupdated | Bir Güncelleştirme düğmesi tıklatıldığında oluşur, ancak DetailsView denetiminden sonra satır güncellenir. Bu olay genellikle güncelleştirme işleminin sonuçlarını denetlemek için kullanılır. |
| ıtemupdating | Bir Güncelleştirme düğmesi tıklatıldığında, ancak DetailsView denetimi kaydı güncelleştirmeden önce oluşur. Bu olay genellikle güncelleştirme işlemini iptal etmek için kullanılır. |
| Modechanged | DetailsView denetimi modları (edit, ekleme veya salt okunur modu) değiştirdikten sonra oluşur. Bu olay genellikle DetailsView denetimi modları değiştirdiğinde bir görevi gerçekleştirmek için kullanılır. |
| Modechanging | DetailsView denetimi modları değiştirmeden önce oluşur (edit, ekleme veya salt okunur modu). Bu olay genellikle bir mod değişikliğini iptal etmek için kullanılır. |
| Pageındexchanged | Çağrı cihazı düğmelerinden biri tıklatıldığında oluşur, ancak DetailsView denetiminden sonra çağrılama işlemi gerçekleşir. Bu olay genellikle, kullanıcı denetimde farklı bir kayda geçtikten sonra bir görevi gerçekleştirmeniz gerektiğinde kullanılır. |
| Pageındexchanging | Çağrı cihazı düğmelerinden biri tıklatıldığında, ancak DetailsView denetimi sayfalama işlemini işlemeden önce oluşur. Bu olay genellikle sayfalama işlemini iptal etmek için kullanılır. |

## <a name="the-menu-control"></a>Menü Denetimi

ASP.NET 2.0'daki Menü kontrolü tam özellikli bir navigasyon sistemi olacak şekilde tasarlanmıştır. SiteMapDataSource gibi hiyerarşik veri kaynaklarına kolayca veri bağlı olabilir.

Menü denetim yapısı bildirimsel veya dinamik olarak tanımlanabilir ve tek bir kök düğümü ve herhangi bir alt düğüm sayısından oluşur. Aşağıdaki kod bildirimsel olarak Menü denetimi için bir menü tanımlar.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

Yukarıdaki örnekte, Home.aspx düğümü kök düğümüdür. Diğer tüm düğümler çeşitli düzeylerde kök düğümü içinde iç içe.

Menü denetiminin işleyebilir iki tür menü vardır; statik menüler ve dinamik menüler. Statik menüler, her zaman görünür menü öğelerinden oluşur. Dinamik menüler, yalnızca kullanıcı fare yle üzerlerinde gezindiğinde görülebilen menü öğelerinden oluşur. Müşteriler genellikle statik menüleri bildirimsel olarak tanımlanan menülerle ve dinamik menülerle çalışma zamanında veri yle dolu menülerle karıştırabilir. Aslında, dinamik ve statik menüler nüfus yöntemi ile ilgisi yoktur. *Statik* ve *dinamik* terimler yalnızca menünün varsayılan olarak statik olarak görüntülenip görüntülenmediğine veya yalnızca kullanıcı bazı eylemlerde bulunduğunda görüntülenip görüntülenmediğine atıfta bulunur.

**StaticDisplayLevels** özelliği, menünün kaç düzeyinin statik olduğunu ve bu nedenle varsayılan olarak görüntüleneceğini yapılandırmak için kullanılır. Yukarıdaki örnekte, **StaticDisplayLevels** özelliğini 2 değerine ayarlamak, menünün Ana Sayfa düğüm, Müzik düğümü ve Filmler düğümünün statik olarak görüntülenmesine neden olur. Kullanıcı üst düğümün üzerinde gezindiğinde diğer tüm düğümler dinamik olarak görüntülenir.

**MaximumDynamicDisplayLevels** özelliği, menünün görüntülenebildiği maksimum dinamik düzey sayısını yapılandırır. **MaximumDynamicDisplayLevels** özelliği tarafından belirtilen değerden daha yüksek bir düzeydeki dinamik menüler atılır.

> [!NOTE]
> Menülerin MaximumDynamicDisplayLevels özelliği nedeniyle oluşturulmadı gibi görünen durumlarla karşılaşabileceğiniz neredeyse kesindir. Bu gibi durumlarda, özelliğin müşteri menülerinin görüntülenmesine izin verecek şekilde ayarlandığından emin olun.

## <a name="data-binding-the-menu-control"></a>Menü Denetimini Veri Bağlama

Menü denetimi, SiteMapDataSource veya XMLDataSource gibi hiyerarşik veri kaynağına bağlanabilir. SiteMapDataSource, Web.siteharitası dosyasından beslendiği ve şemasını Menü denetimine bilinen bir API sağladığından, Bir Menü denetimine veri bağlama için en yaygın kullanılan yöntemdir. Aşağıdaki liste basit bir Web.site haritası dosyasını gösterir.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Bu durumda, Ev öğesi, sadece bir kök siteMapNode öğesi olduğunu unutmayın. Her site MapNode için çeşitli öznitelikler yapılandırılabilir. En sık kullanılan öznitelikler şunlardır:

- **url** Bir kullanıcı menü öğesini tıklattığında görüntülenecek URL'yi belirtir. Bu öznitelik yoksa, düğüm tıklatıldığında yalnızca geri yayınlanır.
- **başlık** Menü öğesinde görüntülenen metni belirtir.
- **açıklama** Düğüm için belge olarak kullanılır. Ayrıca, fare düğümün üzerinde gezinildiğinde bir araç ucu olarak da görüntülenir.
- **siteMapFile** İç içe site haritaları na izin verir. Bu öznitelik iyi biçimlendirilmiş bir ASP.NET site haritası dosyasına işaret etmelidir.
- **rolleri** Bir düğümün görünümünün ASP.NET güvenlik kırpma tarafından kontrol edilmesine izin verir.

Bu özniteliklerin tümü isteğe bağlı olsa da, belirtilmemişse menünün davranışının beklenen olmayabilir. Örneğin, *url* özniteliği belirtilmişse, ancak *açıklama* özniteliği belirtilmemişse, düğüm görünmez ve belirtilen URL'ye gezinmenin bir yolu yoktur.

## <a name="controlling-a-menus-operation"></a>Menüler İşlemini Denetleme

ASP.NET Menü denetiminin çalışmasını etkileyen çeşitli özellikler vardır; **Yönlendirme** özelliği, **DisappearAfter** özelliği, **StaticItemFormatString** özelliği ve **StaticPopoutImageUrl** özelliği bunlardan sadece birkaçıdır.

- **Yönlendirme** *yatay* veya *dikey* olarak ayarlanabilir ve statik menü öğelerinin yatay olarak bir satırda mı yoksa dikey olarak mı dizilir ve birbirinin üzerine yığılıp yığılıp yığılıp yığılıp yığılmadığını denetler. Bu özellik dinamik menüleri etkilemez.
- **Kaybolduktan Sonra** özelliği, dinamik bir menünün fareden uzaklaştıktan sonra ne kadar görünür kalması gerektiğini yapılandırır. Değer milisaniye cinsinden belirtilir ve varsayılan olarak 500'e ulaşır. Bu özelliği -1 değerine ayarlamak, menünün otomatik olarak asla kaybolmasına neden olur. Bu durumda, menü yalnızca kullanıcı menünün dışına tıkladığında kaybolur.
- **StaticItemFormatString** özelliği, menü sisteminizde tutarlı bir şekilde sabit tutulmasını kolaylaştırır. Bu özellik belirtilirken, *{0}* veri kaynağında görünen açıklamayerine girilmelidir. Örneğin, alıştırma 1'deki menü öğesinin Ürünlerimizi Ziyaret Et Sayfamızı vb. {0} belirtmesi için StaticItemFormatString için Sayfamızı ziyaret et belirtmiş olursunuz. Çalışma saatinde, ASP.NET menü öğesi {0} için doğru açıklama ile herhangi bir olay yerini alacaktır.
- **StaticPopoutImageUrl** özelliği, belirli bir menü düğümünün üzerinde gezinerek erişilebilen alt düğümleri olduğunu belirtmek için kullanılan görüntüyü belirtir. Dinamik menüler varsayılan görüntüyü kullanmaya devam eder.

## <a name="templated-menu-controls"></a>Şablonlanmış Menü Denetimleri

Menü denetimi şablonlanmış bir denetimdir ve iki farklı Öğe Şablonu sağlar; StaticItemTemplate ve DynamicItemTemplate. Bu şablonları kullanarak menülerinize sunucu denetimlerini veya kullanıcı denetimlerini kolayca ekleyebilirsiniz.

Visual Studio .NET'teki şablonları yeniden oluşturmak için menüdeki Akıllı Etiket düğmesini tıklatın ve Şablonları Edin'i seçin. Daha sonra StaticItemTemplate veya DynamicItemTemplate düzenleme arasında seçim yapabilirsiniz.

StaticItemTemplate'e eklenen tüm denetimler, sayfa yüklendiğinde statik menüde görünür. DynamicItemTemplate'e eklenen tüm denetimler tüm açılır menülerde görünür.

## <a name="menu-events"></a>Menü Etkinlikleri

Menü denetiminde ona özgü iki olay vardır; **MenuItemClicked** ve **MenuItemDatabound** olay.

Menü öğesi tıklandığında MenuItemClicked olayı yükseltilir. MenuItemDatabound olayı, bir menü öğesi veri ye bağlı olduğunda yükseltilir. Olay işleyicisine geçirilen **MenuEventArgs,** Öğe özelliği üzerinden menü öğesine erişim sağlar.

## <a name="controlling-a-menus-appearance"></a>Menüler Görünümünü Denetleme

Ayrıca, menüleri biçimlendirmek için kullanılabilen birçok stilden birini veya daha fazlasını kullanarak menü denetiminin görünümünü de etkileyebilirsiniz. Bunlar arasında **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**, ve **DynamicHoverStyle**vardır. Bu özellikler standart bir HTML Stil dizesi kullanılarak yapılandırılır. Örneğin, aşağıdaki dinamik menüler için stili etkileyecektir.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Hover stillerinden herhangi birini kullanıyorsanız, *sunucuya* &lt;ayarlanmış&gt; *runat* öğesi ile sayfaya bir kafa öğesi eklemeniz gerekir.

Menü denetimleri de ASP.NET 2.0 temalarının kullanımını destekler.

## <a name="the-treeview-control"></a>TreeView Denetimi

TreeView denetimi verileri ağaca benzer bir yapıda görüntüler. Menü denetiminde olduğu gibi, SiteMapDataSource gibi hiyerarşik veri kaynağına kolayca veri bağlanabilir.

Müşterilerin ASP.NET 2.0'daki TreeView denetimi hakkında sorması muhtemel ilk soru, 1,ASP.NET için kullanılabilen TreeView IE WebControl ile ilgili olup olmadığıdır. Değil. ASP.NET 2.0 TreeView denetimi sıfırdan yazılmıştır ve daha önce mevcut olan IE TreeView WebControl üzerinde önemli bir gelişme sunar.

Bir TreeView denetiminin menü denetimiyle tam olarak aynı şekilde gerçekleştirildiği için bir site haritasına nasıl bağlanılabildiğim konusunda ayrıntılı bilgi vermem. Ancak, TreeView denetiminin çalışma şekliyle ilgili bazı belirgin farklılıklar vardır.

Varsayılan olarak, bir TreeView denetimi tamamen genişletilmiş görünür. İlk yüklemede genişletme düzeyini değiştirmek için denetimin **ExpandDepth** özelliğini değiştirin. Bu, özellikle TreeView'in belirli düğümleri genişlettikten sonra veri ye bağlı olduğu durumlarda önemlidir.

## <a name="databinding-the-treeview-control"></a>DataBinding TreeView Denetimi

Menü denetiminin aksine, TreeView büyük miktarda veriyi işlemeye iyi gelir. Bu nedenle, bir SiteMapDataSource veya XMLDataSource için veri bağlama ek olarak, TreeView genellikle veri bir DataSet veya diğer ilişkisel verilere bağlı. TreeView denetiminin büyük miktarda veriye bağlı olduğu durumlarda, yalnızca denetimde gerçekte görünen verilere bağlamak en iyisidir. Daha sonra TreeView düğümleri genişletildikçe ek verilere veri bağlayabilirsiniz.

Bu gibi durumlarda, **TreeView'in PopulateOnDemand** özelliği *doğru*olarak ayarlanmalıdır. Daha sonra **TreeNodePopulate** yöntemi için bir uygulama sağlamanız gerekir.

## <a name="data-binding-without-postback"></a>Postback olmadan veri bağlama

Önceki örnekte bir düğümü ilk kez genişletdiğinizde, sayfanın geri gönderiler ve yeniler. Bu örnekte bu bir sorun değil, ancak büyük miktarda veri ile bir üretim ortamında olabileceğini hayal edebilirsiniz. Daha iyi bir senaryo, TreeView'in düğümlerini dinamik olarak doldurmaya devam edeceği, ancak sunucuya geri gönderilmeden bir senaryo olacaktır.

**PopulateNodesFromClient** ve **PopulateOnDemand** özelliklerini doğru ayarlayarak, ASP.NET TreeView denetimi bir yazı geri olmadan düğümleri dinamik olarak dolduracaktır. Üst düğüm genişletildiğinde, istemciden bir XMLHttp isteği yapılır ve OnTreeNodePopulate olayı ateşlenir. Sunucu, daha sonra alt düğümleri bağlamak için kullanılan bir XML veri adası ile yanıt verir.

ASP.NET dinamik olarak bu işlevselliği uygulayan istemci kodu oluşturur. Komut &lt;&gt; dosyası içeren komut dosyası etiketleri bir AXD dosyasına işaret ederek oluşturulur. Örneğin, aşağıdaki liste, XMLHttp isteğini oluşturan komut dosyası kodunun komut dosyası bağlantılarını gösterir.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Tarayıcınızda yukarıdaki AXD dosyasına göz atar ve açarsanız, XMLHttp isteğini uygulayan kodu görürsünüz. Bu yöntem, müşterilerin komut dosyası dosyasını değiştirmesini engeller.

## <a name="controlling-the-operation-of-the-treeview-control"></a>TreeView Denetiminin Çalışmasını Denetleme

TreeView denetimi, denetimin çalışmasını etkileyen çeşitli özelliklere sahiptir. En belirgin özellikleri **ShowCheckBoxes**vardır , **ShowExpandCollapse**, ve **ShowLines**.

**ShowCheckBoxes** özelliği, düğümlerin işlendiğinde bir onay kutusu gösterip görüntülemediğini etkiler. Bu özellik için geçerli değerler **Yok**, **Kök**, **Üst**, **Yaprak**, ve **Tümü**. Bunlar TreeView denetimini aşağıdaki gibi etkiler:

| **Özellik Değeri** | **Etki** |
| --- | --- |
| Hiçbiri | Onay kutuları düğümlerde görüntülenmez. Bu varsayılan ayardır. |
| Root | Onay kutusu yalnızca kök düğümünde görüntülenir. |
| Üst | Yalnızca alt düğümleri olan düğümlerde bir onay kutusu görüntülenir. Bu çocuk düğümleri ebeveyn düğümleri veya yaprak düğümleri olabilir. |
| Yaprak | Yalnızca alt düğümleri olmayan düğümlerde bir onay kutusu görüntülenir. |
| Tümü | Tüm düğümlerde bir onay kutusu görüntülenir. |

Onay kutuları kullanılırken, **CheckedNodes** özelliği, postback'te işaretlenen TreeView düğümleri koleksiyonunu döndürür.

**ShowExpandCollapse** özelliği, kök ve üst düğümlerin yanındaki genişletme/daraltma görüntüsünün görünümünü denetler. Bu özellik **yanlış**olarak ayarlanmışsa, TreeView düğümleri köprü olarak işlenir ve bağlantıya tıklayarak genişletilir/daraltılır.

**ShowLines** özelliği, üst düğümleri alt düğümlere bağlayan çizgilerin görüntülenip görüntülenmediğini denetler. **False** (varsayılan) olduğunda, hiçbir satır görüntülenmez. **Doğru**olduğunda, TreeView denetimi **LineImagesFolder** özelliği tarafından belirtilen klasörde satır görüntüleri kullanır.

TreeView hatlarının görünümünü özelleştirmek için Visual Studio .NET 2005 bir Çizgi Tasarımcısı aracı içerir. Bu araca TreeView denetimindeki Akıllı Etiket düğmesini kullanarak aşağıdaki gibi erişebilirsiniz.

![](data-bound-controls/_static/image1.jpg)

**Şekil 1**

**Satır Görüntülerini Özelleştir** menüsü seçeneğini seçtiğinizde, TreeView satırlarının görünümünü yapılandırmanıza olanak tanıyan Satır Tasarımcısı aracı başlatılır.

## <a name="treeview-events"></a>TreeView Etkinlikleri

TreeView denetimiaşağıdaki benzersiz olaylara sahiptir:

- SelectNodeChanged **SelectAction** özelliğine göre bir düğüm seçildiğinde oluşur.
- Bir düğüm onay kutusu durumu değiştirildiğinde TreeNodeCheckChanged oluşur.
- TreeNodeExpanded **SelectAction** özelliğine göre bir düğüm genişletildiğinde oluşur.
- TreeNodeCollapsed bir düğüm çöktüğünde oluşur.
- TreeNodeDataBound bir düğüm veri bağlı olduğunda oluşur.
- TreeNodePopulate bir düğüm doldurulduğunda oluşur.

**SelectAction** özelliği, düğüm seçildiğinde hangi olayın ateşlendiğine yapılandırmanızı sağlar. SelectAction özelliği aşağıdaki eylemleri sağlar:

- TreeNodeSelectAction.Expand düğüm seçildiğinde TreeNodeExpand yükseltir.
- TreeNodeSelectAction.None düğüm seçildiğinde hiçbir olay yükseltir.
- TreeNodeSelectAction.Select düğüm seçildiğinde SelectedNodeChanged olayını yükseltir.
- TreeNodeSelectAction.SelectExpand düğüm seçildiğinde hem SelectedNodeChanged olayını hem de TreeNodeExpand olayını yükseltir.

## <a name="controlling-appearance-with-styles"></a>Stilleri ile Görünüm Kontrol

TreeView denetimi, denetimin stilleriyle görünümünü denetlemek için birçok özellik sağlar. Aşağıdaki özellikler kullanılabilir.

| **Özellik Adı** | **Denetimler** |
| --- | --- |
| Hovernodestyle | Fare üzerlerine geldiğinde düğümlerin stilini denetler. |
| LeafNodeStyle | Yaprak düğümlerinin stilini kontrol eder. |
| Nodestyle | Tüm düğümlerin stilini denetler. Belirli düğüm stilleri (LeafNodeStyle gibi) bu stili geçersiz kılar. |
| Parentnodestyle | Tüm üst düğümlerin stilini denetler. |
| RootNodeStyle | Kök düğümün stilini denetler. |
| SelectedNodeStyle | Seçili düğümün stilini denetler. |

Bu özelliklerin her biri salt okunur. Ancak, her biri bir **TreeNodeStyle** nesnesini döndürür ve bu nesnenin özellikleri *özellik alt özelliği* biçimi kullanılarak değiştirilebilir. Örneğin, **SelectedNodeStyle'ın** **ForeColor** özelliğini ayarlamak için aşağıdaki sözdizimini kullanırsınız:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Yukarıdaki etiketin kapalı olmadığını unutmayın. Bunun nedeni, burada gösterilen bildirimsel sözdizimini kullanırken, HTML koduna TreeViews düğümlerini de eklemenizdir.

Stil *özellikleri, property.subproperty* biçimini kullanarak kodolarak da belirtilebilir. Örneğin, **RootNodeStyle'ın** **ForeColor** özelliğini kodolarak ayarlamak için aşağıdaki sözdizimini kullanırsınız:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Farklı stil özelliklerinin kapsamlı bir listesi için TreeNodeStyle nesnesindeki MSDN belgelerine bakın.

## <a name="the-sitemappath-control"></a>SiteMapPath Denetimi

SiteMapPath denetimi, ASP.NET geliştiricileri için ekmek kırıntısı gezinme denetimi sağlar. Diğer navigasyon denetimleri gibi, kolayca SiteMapDataSource veya XmlDataSource gibi hiyerarşik veri kaynaklarına bağlı veri olabilir.

SiteMapPath denetimi, SiteMapNodeItem nesnelerinden oluşur. Üç tür düğüm vardır; Kök düğümü, Üst düğüm ve Geçerli düğüm. Kök düğüm hiyerarşik yapının üst kısmındaki düğümdür. Geçerli düğüm geçerli sayfayı temsil eder. Diğer tüm düğümler ana düğümlerdir.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>SiteMapPath Denetiminin Çalışmasını Denetleme

SiteMapPath denetiminin çalışmasını kontrol eden özellikler aşağıdaki gibidir:

| **Özellik** | **Mülkiyet açıklaması** |
| --- | --- |
| Görüntülenen Üst Düzeyler | Kaç üst düğümün görüntüleneceğini denetler. Varsayılan değer -1'dir ve görüntülenen üst düğüm sayısına herhangi bir kısıtlama getirmez. |
| Yol Yönü | SiteMapPath yönünü denetler. Geçerli değerler RootToCurrent (varsayılan) ve CurrentToRoot'dur. |
| Pathseparator | SiteMapPath denetiminde düğümleri ayıran karakteri kontrol eden bir dize. Varsayılan değer :. |
| RenderCurrentNodeAsLink | Geçerli düğümün bağlantı olarak işlenip işlenmediğini kontrol eden boolean değeri. Varsayılan, False'dur. |
| Skiplinktext | Sayfa ekran okuyucular tarafından görüntülendiğinde erişilebilirlik konusunda yardımcı olur. Bu özellik, ekran okuyucuların SiteMapPath denetimini atlamasına olanak tanır. Bu özelliği devre dışı bırakabilmek için özelliği String.Empty olarak ayarlayın. |

## <a name="templated-sitemappath-controls"></a>Şablonlanmış SiteMapPath Denetimleri

SiteMapControl şablonlanmış bir denetimdir ve bu nedenle, denetimi görüntülemede kullanmak üzere farklı şablonlar tanımlayabilirsiniz. SiteMapPath denetiminde şablonları yeniden görüntülemek için denetimdeki Akıllı Etiket düğmesini tıklatın ve menüden Şablonları Edin'i seçin. Bu, mevcut farklı şablonlar arasında seçim yapabileceğiniz SiteMapTasks menüsünü aşağıda gösterildiği gibi görüntüler.

![](data-bound-controls/_static/image2.jpg)

**Şekil 2**

**Düğüm Şablonu** şablonu SiteMapPath'teki herhangi bir düğümü ifade eder. Düğüm bir kök düğümveya geçerli düğüm ve **RootNodeTemplate** veya **CurrentNodeTemplate** yapılandırılırsa, Düğüm Şablonu geçersiz kılındı.

## <a name="sitemappath-events"></a>SiteMapPath Olaylar

SiteMapPath denetiminde Denetim sınıfından türetilmiş olmayan iki olay vardır; **ItemCreated** olayı ve **ItemDataBound** olayı. SiteMapPath öğesi oluşturulduğunda ItemCreated olayı yükseltilir. Bir SiteMapPath düğümünün veri bağlaması sırasında DataBind yöntemi çağrıldığında ItemDataBound yükseltilir. Bir **SiteMapNodeItemEventArgs** nesnesi, Öğe özelliği üzerinden belirli SiteMapNodeItem'e erişim sağlar.

## <a name="controlling-appearance-with-styles"></a>Stilleri ile Görünüm Kontrol

Aşağıdaki stilleri bir SiteMapPath denetimi biçimlendirme kindirilebilir.

| **Özellik Adı** | **Denetimler** |
| --- | --- |
| CurrentNodeStyle | Geçerli düğüm için metnin stilini denetler. |
| RootNodeStyle | Kök düğümü için metnin stilini denetler. |
| Nodestyle | CurrentNodeStyle veya RootNodeStyle'ın geçerli olmadığını varsayarak tüm düğümler için metnin stilini denetler. |

NodeStyle özelliği CurrentNodeStyle veya RootNodeStyle tarafından geçersiz kılınan özelliktir. Bu özelliklerin her biri salt okunur ve **stil** nesnesi döndürür. Bu özelliklerden birini kullanarak düğümün görünümünü etkilemek için döndürülen Stil nesnesinin özelliklerini ayarlamanız gerekir. Örneğin, aşağıdaki kod geçerli düğümün ön renkli özelliğini değiştirir.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

Özellik de aşağıdaki gibi programlı olarak uygulanabilir:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Şablon uygulanırsa, stil uygulanmaz.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Laboratuvar 1: ASP.NET Menü Denetiminin Yapılandırılması

1. Yeni bir Web sitesi oluşturun.
2. Dosya şablonları listesinden Dosya, Yeni, Dosya ve Site Haritası'nı seçerek Bir Site Haritası dosyası ekleyin.
3. Site haritasını (Varsayılan olarak Web.site eşlemi) açın ve aşağıdaki listegibi olacak şekilde değiştirin. Site haritası dosyasına bağladığınız sayfalar gerçekten yok, ancak bu alıştırma için bir sorun olmayacaktır.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Tasarım görünümünde varsayılan Web formunu açın.
5. Araç Kutusu'nun Gezinti bölümünden sayfaya yeni bir Menü denetimi ekleyin.
6. Toolbox'ın Veri bölümünden yeni bir SiteMapDataSource ekleyin. SiteMapDataSource sitenizdeki Web.site haritası dosyasını otomatik olarak kullanır. (Web.site haritası dosyası sitenin kök klasöründe *olmalıdır.)*
7. Menü Denetimi'ni tıklatın ve ardından Menü Görevleri iletişim kutusunu görüntülemek için Akıllı Etiket düğmesini tıklatın.
8. Veri Kaynağı açılır bilgisini seç'te SiteMapDataSource1'i seçin.
9. Otomatik Biçim bağlantısını tıklayın ve Menü için bir biçim seçin.
10. Özellikler bölmesinde **StaticDisplayLevels** özelliğini 2 olarak ayarlayın. Menü denetimi artık Tasarımcı'da Ev, Ürünler ve Hizmetler düğümlerini görüntülemelidir.
11. Menüyü kullanmak için tarayıcınızdaki sayfaya göz atın. (Site haritasına eklediğiniz sayfalar gerçekte bulunmadığından, bunlara göz atmaya çalıştığınızda bir hata görürsünüz.)

StaticDisplayLevels ve MaximumDynamicDisplayLevels özelliklerini değiştirmeyi deneyin ve bunların menünün nasıl işlendiğini nasıl etkilediğini görün.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Laboratuvar 2: Bir TreeView Denetimini Dinamik Olarak Bağlama

Bu alıştırma, SQL Server'ın yerel olarak çalıştığını ve Northwind veritabanının SQL Server örneğinde mevcut olduğunu varsayar. Bu koşullar yerine getirilmezse, lütfen örnekteki bağlantı dizesini değiştirin. Güvenilir bir bağlantı yerine SQL Server kimlik doğrulaması belirtmeniz gerekebileceğini de unutmayın.

1. Yeni bir Web sitesi oluşturun.
2. Varsayılan.aspx için Kod görünümüne geçin ve tüm kodu aşağıda listelenen kodla değiştirin. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Sayfayı treeview.aspx olarak kaydedin.
4. Sayfaya göz atın.
5. Sayfa ilk görüntülendiğinde, tarayıcınızdaki sayfanın kaynağını görüntüleyin. İstemciye yalnızca görünür düğümlerin gönderildiğini unutmayın.
6. Herhangi bir düğümün yanındaki artı işaretini tıklatın.
7. Sayfadaki kaynağı yeniden görüntüleyin. Yeni görüntülenen düğümlerin artık mevcut olduğuna dikkat edin.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Laboratuvar 3: GridView ve DetailsView kullanarak Verileri Görüntüle ve Düzenleme Ayrıntıları

1. Yeni bir Web sitesi oluşturun.
2. Web sitesine yeni bir web.config ekleyin.
3. Aşağıda gösterildiği gibi web.config dosyasına bir bağlantı dizesi ekleyin: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > Ortamınıza bağlı olarak bağlantı dizesini değiştirmeniz gerekebilir.
4. Web.config dosyasını kaydedin ve kapatın.
5. Default.aspx'i açın ve yeni bir SqlDataSource denetimi ekleyin.
6. SqlDataSource denetiminin kimliğini **Ürünlerle**değiştirin.
7. **SqlDataSource Görevler** menüsünde **Veri Kaynağını Yapılandır'ı**tıklatın.
8. Bağlantı açılır açılır ayında **Northwind'i** seçin ve İleri'yi tıklatın.
9. **Ad** açılır tarihinden **Ürünleri** seçin ve aşağıda gösterildiği gibi **ProductID,** **ProductName**, **UnitPrice**ve **UnitsInStock** onay kutularını kontrol edin. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. **İleri**’ye tıklayın.
11. **Son**'a tıklayın.
12. Kaynak görünümüne geçin ve oluşturulan kodu inceleyin. SqlDataSource denetimine eklenen **SelectCommand,** **DeleteCommand,** **InsertCommand**ve **UpdateCommand'a** dikkat edin. Ayrıca eklenen parametrelere de dikkat edin.
13. Tasarım görünümüne geçin ve sayfaya yeni bir GridView denetimi ekleyin.
14. Veri Kaynağı açılır giyi **seç'ten** **Ürünler'i** seçin.
15. Aşağıda gösterildiği gibi **Sayfalama** yı etkinleştir ve **Seçimi Etkinleştir'i** denetleyin. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. **Sütunları Edit** bağlantısını tıklatın ve **Otomatik oluşturma alanlarının** denetlendiğinden emin olun.
17. **Tamam**'a tıklayın.
18. GridView denetimi seçili olduğu için, Özellikler bölmesinde **DataKeyNames** özelliğinin yanındaki düğmeyi tıklatın.
19. **Kullanılabilir veri alanları** listesinden **&gt;** **ProductID'yi** seçin ve eklemek için düğmeyi tıklatın.
20. Tamam'a tıklayın.
21. Sayfaya yeni bir SqlDataSource denetimi ekleyin.
22. SqlDataSource denetiminin kimliğini **Ayrıntılar**olarak değiştirin.
23. SqlDataSource Görevler menüsünden **Veri Kaynağını Yapılandır'ı**seçin.
24. Açılır açılır yerden **Northwind'i** seçin ve **İleri'yi**tıklatın.
25. <strong>Ad</strong> açılır listesinden <strong> \< <strong>Ürünler'i</strong> seçin ve <strong>Sütunlar</strong> liste kutusundaki /güçlü>* onay kutusunu işaretleyin.
26. **WHERE** düğmesini tıklatın.
27. **Sütun** açılır tarafından **ProductID'yi** seçin.
28. Operatör **=** açılır açılır arasında seçin.
29. **Kaynak** açılır tarafından **Denetim'i** seçin.
30. **Denetim Kimliği** açılır tarafından **GridView1'i** seçin.
31. WHERE yan tümcesini eklemek için **Ekle** düğmesini tıklatın.
32. **Tamam**'a tıklayın.
33. **Gelişmiş** düğmesini tıklatın ve **InSERT Oluştur, GÜNCELLE ve DELETE ifadelerini** onay kutusunu işaretleyin.
34. **Tamam**'a tıklayın.
35. **İleri'yi** tıklatın ve **Bitir'i**tıklatın.
36. Sayfaya DetailsView denetimi ekleyin.
37. Veri Kaynağı açılır **ayininde** **Ayrıntılar'ı**seçin.
38. Aşağıda gösterildiği gibi **Düzenlemeyi Etkinleştir** onay kutusunu işaretleyin. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Sayfayı kaydedin ve Varsayılan.aspx'e göz atın.
40. DetailsView güncelleştirmesini otomatik olarak görmek için farklı kayıtların yanındaki **Seç** bağlantısını tıklatın.
41. DetailsView denetiminde **Edit** bağlantısını tıklatın.
42. Kayıtta değişiklik yapın ve **Güncelleştir'i**tıklatın.
