---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: Ana sayfadan içerik sayfası (VB) ile etkileşim kurma | Microsoft Docs
author: rick-anderson
description: Yöntemleri çağırmak için içerik sayfasındaki kod özellikleri ana sayfanın vb. kümeden nasıl inceler.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 04642dbcd62fe24d4e0fa379b90cbf4122c57066
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65134070"
---
# <a name="interacting-with-the-master-page-from-the-content-page-vb"></a>Ana Sayfadan İçerik Sayfası ile Etkileşim Kurma (VB)

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Kodu indir](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> Yöntemleri çağırmak için içerik sayfasındaki kod özellikleri ana sayfanın vb. kümeden nasıl inceler.

## <a name="introduction"></a>Giriş

Ana sayfa oluşturma, içerik bölgeleri tanımlamak, ASP.NET sayfaları için bir ana sayfa bağlamak ve sayfaya özel içeriği tanımlayan nasıl en son beş eğitim kursunda incelemiştik. Ziyaretçi belirli bir içerik sayfa istediğinde, içerik ve ana sayfalar biçimlendirme zamanında birleştirilmiş denetim hiyerarşisi işlemede elde edilen çarpım. Bu nedenle, zaten bir yoludur, ana sayfa ve içerik sayfalarını biri etkileşim kurabilir gördük: içerik sayfası ana sayfanın ContentPlaceHolder denetimlere transfuse için biçimlendirme harfe dönüştüren.

Ne incelemek henüz nasıl ana sayfa ve içerik sayfası program aracılığıyla etkileşim kurabilir olur. Ana sayfanın ContentPlaceHolder denetimleri için biçimlendirme tanımlanmasına ek olarak, bir içerik sayfasının kendi ana sayfanın genel özelliklerine değerler atamanıza da genel metotlarını çağırır. Benzer şekilde, bir ana sayfa içerik sayfalarını ile etkileşimde bulunabilir. Bir ana ve içerik sayfası arasında program tabanlı etkileşimlerin, bildirim temelli işaretlerini arasındaki etkileşimi daha az yaygın olsa da, bu tür bir program tabanlı etkileşimlerin gerekmesi halinde birçok senaryo vardır.

Bu öğreticide nasıl bir içerik sayfasının program aracılığıyla kendi ana sayfası ile etkileşim kurabilir inceleyin; sonraki öğreticide nasıl ana sayfaya benzer şekilde, içerik sayfalarıyla etkileşim kurabilir görünecektir.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>İçerik sayfası ile onun ana sayfa arasındaki program tabanlı etkileşimlerin örnekleri

Belirli bir bölge sayfasının bir sayfa sayfa olarak yapılandırılması gerekir, ContentPlaceHolder denetimi kullanırız. Ancak burada sayfalarını çoğunu gereken belirli bir çıkış, ancak küçük bir dizi sayfa yaymak için durumlar konusunda başka bir göstermek için özelleştirmeniz gerekir? Biz de incelenirken bir tür örneği [ *birden çok ContentPlaceHolder ve varsayılan içerik* ](multiple-contentplaceholders-and-default-content-vb.md) öğreticide içeren her sayfada bir oturum açma arabirimine görüntüleme. Çoğu sayfaları bir oturum açma arabirimine içermelidir, ancak, birkaç sayfa sayısı gibi atlanması: ana oturum açma sayfasını (`Login.aspx`); hesap oluşturma sayfasına; ve yalnızca kimliği doğrulanmış kullanıcıların erişimine açık olan diğer sayfaları. [ *Birden çok ContentPlaceHolder ve varsayılan içerik* ](multiple-contentplaceholders-and-default-content-vb.md) öğretici gösterilen varsayılan içeriği için ana sayfasında bir ContentPlaceHolder tanımlama ve ardından içinde geçersiz kılma sayfalar yeri Varsayılan içerik istiyordu değil.

Genel özellik veya yöntem göstermek veya gizlemek için oturum açma arabirimini gösteren ana sayfa içindeki başka bir seçenek oluşturmaktır. Örneğin, ana sayfa adlı ortak bir özelliği içerebilir `ShowLoginUI` değeri ayarlamak için kullanılan `Visible` ana sayfasındaki oturum açma denetimi özelliği. Bu içerik sayfalarını burada oturum açma kullanıcı arabirimi gizlenen ardından programlı olarak ayarlayabilirsiniz `ShowLoginUI` özelliğini `False`.

Ana sayfa içerik sayfasındaki bazı eylemleri ortaya çıkan sonra yenilenmesi gerekiyor veri görüntülenen belki de en yaygın örnek içerik ve ana sayfa etkileşim meydana gelir. En son beş görüntüleyen GridView içeren bir ana sayfa eklenen belirli veritabanı tablosundan kayıtları göz önünde bulundurun ve içerik sayfalarını birinin aynı tabloya yeni bir kayıt eklemek için bir arabirimi içerir.

Bir kullanıcı yeni bir kayıt eklemek için sayfayı ziyaret ettiğinde, en son eklediğiniz beş ana sayfasında görüntülenen kayıt görür. Yeni bir kaydın sütun değerlerini doldurduktan sonra Filiz formu gönderir. Ana sayfada GridView sahip varsayarak, `EnableViewState` (varsayılan) True olarak ayarlanan özelliği, içeriği görüntüle durumundan yeniden yüklendikten ve, daha yeni bir kayıt yalnızca veritabanına eklenmiş olsa da sonuç olarak, beş aynı kayıt gösterilir. Bu kullanıcı karışıklığa neden olabilir.

> [!NOTE]
> Böylece kendi temel alınan veri kaynağına her geri gönderme üzerinde rebinds GridView'ın görünüm durumu devre dışı bırakırsanız, verileri yeni kayıt için datab eklendiğinde daha önceki sayfa yaşam döngüsü içinde GridView bağlı olduğundan, yine de tam eklediği kayıt gösterilmez ase.

Böylece yeni eklenen bir kaydın ana sayfasında görüntülenen bu sorunu gidermek için kullanıcının GridView ihtiyacımız kendi veri kaynağına yeniden bağlamaya GridView istemek için bir geri gönderme üzerinde *sonra* veritabanına yeni kayıt eklendi. Yeni kayıt (ve kendi olay işleyicileri) içerik sayfası ancak yenilenmesi gerekiyor GridView Koleksiyonlar'a arabirimi ana sayfasında olduğundan bu ana sayfalar ve içeriği arasındaki etkileşimi gerektirir.

Olay işleyicisinde içerik sayfası ana sayfanın görüntüden yenileme içeriği ve ana sayfa etkileşimi en yaygın gereksinimlerini biri olduğu için bu konuyu daha ayrıntılı bir şekilde araştıralım. Bu öğretici için indirme adlı bir Microsoft SQL Server 2005 Express Edition veritabanı içerir `NORTHWIND.MDF` Web sitesinin içinde `App_Data` klasör. Ürün, çalışan ve satış bilgi kurgusal bir şirkette, Northwind Traders için Northwind veritabanına depolar.

En son beş görüntüleme aracılığıyla 1. adım Yürüyüşü ürünleri GridView ana sayfasına eklenen. 2. adım, yeni ürün eklemek için bir içerik sayfası oluşturur. Ana sayfada ortak özellikler ve yöntemler oluşturma 3. adım bakar ve 4. adım, program aracılığıyla bu özellikleri ve yöntemleri içerik sayfasından ile arabirim oluşturmak verilmektedir.

> [!NOTE]
> Bu öğreticide ASP.NET verilerle çalışmaya özelliklerini içine delve değil. Veri ve veri ekleme için içerik sayfasını görüntülemek ana sayfası ayarlama adımları şunlardır: tam, henüz breezy. SqlDataSource ile GridView denetimleri görüntüleme ve veri ekleme ve kullanma daha derinlemesine bir bakış için bu öğreticinin sonunda başka okumalar bölümdeki kaynaklar başvurun.

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>1. Adım: Beş görüntüleme en son ürün ana sayfada eklendi

Site.master ana sayfasını açın ve bir etiket için bir GridView denetimi ekleyip `leftContent` `<div>`. Etiketin Temizle `Text` özelliği ayarlamak, `EnableViewState` özelliğini `False`ve onun `ID` özelliğini `GridMessage`; GridView'ın ayarlamak `ID` özelliğini `RecentProducts`. Ardından, Tasarımcısından GridView'ın akıllı etiket genişletin ve yeni bir veri kaynağına bağlamak seçin. Bu veri kaynağı Yapılandırma Sihirbazı'nı başlatır. Northwind veritabanı içinde `App_Data` klasördür bir Microsoft SQL Server veritabanı (bkz. Şekil 1) seçerek bir SqlDataSource oluşturulacağını seçin; SqlDataSource ad `RecentProductsDataSource`.

[![GridView RecentProductsDataSource adlı bir SqlDataSource denetimi bağlama](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**Şekil 01**: GridView SqlDataSource adlı Denetim bağlama `RecentProductsDataSource` ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png))

Sonraki adım bize ne bağlanmak için veritabanı belirtmenizi ister. Seçin `NORTHWIND.MDF` veritabanı dosyasının aşağı açılan listeden ve İleri'ye tıklayın. Bu, size bu veritabanına kullandığınız ilk kez olduğu için sihirbaz bağlantı dizesinde depolamak sunacaktır `Web.config`. Sahip adı kullanarak bağlantı dizesini depolama `NorthwindConnectionString`.

[![Northwind veritabanı'na bağlanma](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**Şekil 02**: Northwind veritabanına bağlanma ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png))

Veri Kaynağı Yapılandırma Sihirbazı'nı, biz verileri almak için kullanılan bir sorgu belirtin iki yöntem sunar:

- Özel bir SQL deyimi veya saklı yordam belirterek veya
- Bir tablo veya Görünüm çekme ve ardından döndürülecek olan sütunları belirtme

Yalnızca beş ürünleri en son eklenen döndürülecek istediğimizden, size özel bir SQL deyimi belirtmeniz gerekir. Aşağıdaki `SELECT` sorgu:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` Anahtar sözcüğü, sorgunun yalnızca ilk beş kaydı döndürür. `Products` Tablonun birincil anahtarı `ProductID`, olan bir `IDENTITY` bize tabloya eklenen her yeni ürün önceki giriş daha büyük bir değere sahip olacağını garantiler sütunu. Bu nedenle, sonuçlarına göre sıralama `ProductID` ile en son oluşturulan olanları başlangıç ürünleri azalan sırada döndürür.

[![Beş en son eklenen ürün döndürür](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**Şekil 03**: Beş en son eklenen ürün döndürür ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png))

Sihirbazı tamamladıktan sonra Visual Studio için görüntülenecek GridView iki BoundFields oluşturur `ProductName` ve `UnitPrice` veritabanından döndürülen alanlar. Bu noktada bildirim temelli biçimlendirme ana sayfanın aşağıdakine benzer bir biçimlendirme içermelidir:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

Gördüğünüz gibi biçimlendirme içeriyor: Etiket Web denetimi (`GridMessage`); GridView `RecentProducts`iki BoundFields; ve beş en son eklenen ürünleri döndüren SqlDataSource denetimi ile.

Bu GridView oluşturulan ve yapılandırılan SqlDataSource denetimi ile bir tarayıcı aracılığıyla bir Web sitesini ziyaret edin. Şekil 4'te gösterildiği gibi ürünleri en son beş listeleyen sol alt köşesinde bir kılavuzda eklenen görürsünüz.

[![GridView beş en son eklenen ürünleri görüntüler.](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**Şekil 04**: GridView beş en son eklenen ürünleri görüntüler ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png))

> [!NOTE]
> GridView görünümünü oluşturan temiz çekinmeyin. Görüntülenen biçimlendirme bazı öneriler şunlardır `UnitPrice` değeri olarak bir para birimi ve kılavuz görünümü geliştirmek için arka plan renklerini ve yazı tiplerini kullanma.

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>2. Adım: Yeni ürün eklemek için bir içerik sayfası oluşturma

Bizim sıradaki görev, bir kullanıcı için yeni bir ürün ekleyebilirsiniz bir içerik sayfasının oluşturmaktır `Products` tablo. Yeni bir içerik sayfasına ekleme `Admin` adlı klasöre `AddProduct.aspx`ettiğinizden emin olmak için bağlama `Site.master` ana sayfa. Bu sayfa Web sitesine eklendikten sonra Çözüm Gezgini Şekil 5 gösterir.

[![Yönetici klasöre yeni bir ASP.NET sayfası ekleyin](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**Şekil 05**: Yeni bir ASP.NET sayfasına ekleme `Admin` klasörü ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png))

Geri çağırma [ *ana sayfada başlık, Meta etiketler ve diğer HTML üst bilgilerini belirtme* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) adlı bir özel taban sayfası sınıfı oluşturduk öğretici `BasePage` , oluşturulan başlığı yazılmışsa açıkça ayarlayın. Git `AddProduct.aspx` sayfa arka plan kod sınıfı ve varsa, türetilen `BasePage` (yerine gelen `System.Web.UI.Page`).

Son olarak, güncelleştirme `Web.sitemap` bu ders için bir giriş eklemek için dosya. Altında aşağıdaki işaretlemeyi ekleyin `<siteMapNode>` denetim kimliği adlandırma sorunları ders için:

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

Bu ek Şekil 6'da gösterildiği gibi `<siteMapNode>` öğesi dersleri listesinde yansıtılır.

Geri dönüp `AddProduct.aspx`. İçerik denetimi için `MainContent` ContentPlaceHolder, bir DetailsView denetimi ekleyin ve adlandırın `NewProduct`. Adlı yeni bir SqlDataSource denetimi DetailsView bağlamak `NewProductDataSource`. Gibi Northwind veritabanı kullanan Sihirbazı 1. adımında SqlDataSource ile yapılandırın ve özel bir SQL deyimi belirtmek seçin. DetailsView öğeleri eklemek için kullanılacağından, her ikisini de belirtmek ihtiyacımız bir `SELECT` ifadesi ve bir `INSERT` deyimi. Aşağıdaki `SELECT` sorgu:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

Ardından, aşağıdaki Ekle sekmesinden ekleyin `INSERT` deyimi:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

Sihirbazı tamamladıktan sonra DetailsView'ın akıllı etiket için gidin ve "ekleme etkinleştir" onay kutusunu işaretleyin. Bu bir CommandField DetailsView ekler, `ShowInsertButton` özelliği True olarak ayarlayın. DetailsView'ın bu DetailsView yalnızca veri ekleme için kullanılacağından ayarlamak `DefaultMode` özelliğini `Insert`.

İşte bu kadar kolay! Şimdi bu sayfayı test edin. Ziyaret `AddProduct.aspx` bir tarayıcıdan bir ad ve Fiyat (bkz. Şekil 6) girin.

[![Veritabanına yeni ürün ekleme](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**Şekil 06**: Veritabanına yeni ürün ekleme ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png))

Yeni ürün için fiyat ve adını yazarak sonra Ekle düğmesine tıklayın. Bu, geri gönderme formun neden olur. Geri gönderme, SqlDataSource denetimi 's üzerinde `INSERT` deyimi yürütülür; iki parametrelerini DetailsView'ın iki TextBox kullanıcı tarafından girilen değerlerle doldurulur. Ne yazık ki, bir ekleme oluştu hiçbir görsel geri bildirim yoktur. Yeni bir kayıt eklendiğini onaylayan görüntülenen bir ileti olup iyi olurdu. Ben bunu bir alıştırma olarak için okuyucu bırakın. Ayrıca, yeni bir kayıt DetailsView ekledikten sonra GridView ana sayfasında önce aynı beş kayıtları olarak görüntülenmeye devam eder; Yeni eklenen bir kaydın içermez. Sonraki adımlarda bu sorunu gidermek nasıl inceleyeceğiz.

> [!NOTE]
> Ekleme başarılı oldu görsel geri bildirim çeşit eklemenin yanı sıra, ayrıca DetailsView'ın ekleme arabirimi doğrulamasını içerecek şekilde güncelleştirmek için öneriyoruz. Şu anda doğrulama yoktur. Bir kullanıcı için geçersiz bir değer girerse `UnitPrice` alan olduğu gibi "çok pahalı" içinde bir ondalık sayı, dize dönüştürmek sistem girişiminde bulunduğunda geri göndermede bir özel durum oluşturulur. Ekleme özelleştirme hakkında daha fazla bilgi için arabirim, başvurmak [ *veri değişikliği arabirimini özelleştirme* öğretici](https://asp.net/learn/data-access/tutorial-20-vb.aspx) gelen my [veri öğretici serisininileçalışma](../../data-access/index.md).

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>3. Adım: Ana sayfada ortak özellikler ve yöntemler oluşturma

1. adımda eklediğimiz adlı bir etiket Web denetimi `GridMessage` yukarıda ana sayfasında GridView. Bu etiket, isteğe bağlı olarak bir ileti görüntülemek için tasarlanmıştır. Yeni bir kayda ekledikten sonra Örneğin `Products` tablo istiyoruz okuyan bir ileti görüntülemek: "*ProductName* veritabanına eklenen." İletinin içerik sayfası tarafından özelleştirilebilir sabit kodlamak yerine bu etikette ana sayfa için metin, istiyoruz.

Etiket denetimi, bir korumalı üye değişkeni ana sayfada uygulandığından içerik sayfalarını doğrudan erişilemez. Etiketi içinde bir ana sayfa içerik sayfasından (ya da sorgunuzun, ana sayfa içindeki herhangi bir Web Denetimi) ile çalışması için ortak bir özellik tarafından özelliklerinden biri olabilen bir proxy olarak hizmet veren ya da Web denetimi sunan ana sayfasında için oluşturmamız gerekir  erişilebilir. Etiketin kullanıma sunmak için ana sayfa arka plan kod sınıfına aşağıdaki söz dizimini ekleyin `Text` özelliği:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

İçin yeni bir kayıt eklendiğinde `Products` içerik sayfası tablosundan `RecentProducts` GridView ana sayfasında, temel alınan veri kaynağına yeniden bağlamanız gerekir. GridView çağrı yeniden bağlamak için kendi `DataBind` yöntemi. Ana sayfada GridView içerik sayfalarına programlı olarak erişilebilir olmadığı için biz genel bir yöntem ana sayfasında, çağrıldığında oluşturmanız gerekir, GridView verileri rebinds. Ana sayfa arka plan kod sınıfına aşağıdaki yöntemi ekleyin:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

İle `GridMessageText` özelliği ve `RefreshRecentProductsGrid` yöntemi yerinde herhangi bir içerik sayfayı programlı olarak ayarlamak veya değerini okumak `GridMessage` etiketin `Text` özelliği veya verileri yeniden bağlamanız `RecentProducts` GridView. 4. adım, içerik sayfasından ana sayfa genel özelliklerini ve yöntemlerini nasıl inceler.

> [!NOTE]
> Ana sayfanın özellikleri ve yöntemleri olarak işaretlemek unutmayın `Public`. Siz açıkça bu özellikler ve yöntemler olarak belirtmek değil, `Public`, bunlar içerik sayfasından erişilebilir olmaz.

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>4. Adım: İçerik sayfasından ana sayfa genel üyeleri çağırma

Ana sayfaya gerekli genel özellikleri ve yöntemleri vardır, bu özellikleri ve yöntemleri çağırmak hazırız `AddProduct.aspx` içerik sayfası. Özellikle, ana sayfanın ayarlamak ihtiyacımız `GridMessageText` özelliği ve çağrı kendi `RefreshRecentProductsGrid` yeni ürünü veritabanına eklendikten sonra yöntemi. Hemen önce ve önce veya sonra görev programlı bazı işlemler yapması sayfa geliştiriciler için kolaylaştıran çeşitli görevleri tamamladıktan sonra tüm ASP.NET veri Web denetimleri olaylarını başlatmak. Son kullanıcı DetailsView'ın Ekle düğmesine tıkladığında, örneğin, üzerinde DetailsView harekete geçirirse geri gönderme kendi `ItemInserting` ekleme iş akışı başlamadan önce olay. Ardından kayıt veritabanına ekler. DetailsView oluşturur, kendi `ItemInserted` olay. Bu nedenle, yeni ürün eklendikten sonra ana sayfayla çalışması için DetailsView için ait bir olay işleyicisi oluşturun `ItemInserted` olay.

İçerik sayfası, program aracılığıyla kendi ana sayfası ile arabirim oluşturmasını iki yolu vardır:

- Kullanarak `Page.Master` ana sayfaya geniş yazılmış bir başvuru döndürür, özelliği veya
- Aracılığıyla sayfanın ana sayfa türü veya dosya yolu belirtin. bir `@MasterType` yönergesi; bu otomatik olarak ekler kesin türü belirtilmiş bir özellik sayfası için `Master`.

Her iki yaklaşım inceleyelim.

### <a name="using-the-loosely-typedpagemasterproperty"></a>Geniş yazılmış kullanarak`Page.Master`özelliği

Tüm ASP.NET web sayfaları öğesinden türetilmelidir `Page` bulunan sınıf `System.Web.UI` ad alanı. `Page` Sınıfı içeren bir [ `Master` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) , sayfanın ana sayfa için bir başvuru döndürür. Sayfanın bir ana sayfa yoksa `Master` döndürür `Nothing`.

`Master` Özellik türü bir nesne döndürür [ `MasterPage` ](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) (bulunan `System.Web.UI` ad alanı) tüm ana sayfalar türetilen temel türü. Bu nedenle, genel özellikleri kullanın veya gerekir cast bizim Web sitesinin ana sayfasında tanımlanan yöntemleri için `MasterPage` döndürülen nesne `Master` özelliğini uygun bir tür. Size sunduğumuz ana sayfa dosyası adlı `Site.master`, arka plan kod sınıfı olarak adlandırılan `Site`. Bu nedenle, aşağıdaki atamalardan kod `Page.Master` örneğine özellik `Site` sınıfı.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

Şimdi, Integer sahibiz geniş yazılmış `Page.Master` özelliği Site türü için şu özellikleri ve yöntemleri siteye belirli başvurabilirsiniz. Şekil 7 gösterildiği gibi genel özelliğin `GridMessageText` IntelliSense açılan menü görüntülenir.

[![IntelliSense bizim ana sayfanın genel özellikleri ve yöntemleri gösterilmektedir.](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**Şekil 07**: IntelliSense, bizim ana sayfanın genel özellikleri ve yöntemleri gösterilmektedir ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png))

> [!NOTE]
> Ana sayfa dosyanız adlı `MasterPage.master` ana sayfa arka plan kod sınıfı adı ise `MasterPage`. Bu türden atama olduğunda belirsiz kodlara neden olabilir `System.Web.UI.MasterPage` için `MasterPage` sınıfı. Kısacası, Web sitesi projesi modeli kullanılırken biraz karmaşık olabilen tür için atama tam olarak nitelemek gerekir. Ya da ana sayfanıza oluşturduğunuzda dışında bir ad olduğunu emin olmak için önerim olacaktır `MasterPage.master` veya ana sayfayı kesin türü belirtilmiş bir başvuru daha da iyi oluşturun.

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>Kesin türü belirtilmiş bir başvuruyla oluşturma`@MasterType`yönergesi

Yakından baktığımızda bir ASP.NET sayfasının arka plan kod sınıfı kısmi bir sınıf olduğunu görebilirsiniz (Not `Partial` sınıf tanımında anahtar sözcüğü). Kısmi sınıflar, C# ve Visual Basic with.NET Framework 2.0 içinde tanıtılan ve birden çok dosyaya tanımlanacak bir sınıfın üyeleri de koysalar sağlar. Arka plan kod sınıfı dosyası - `AddProduct.aspx.vb`, örneğin - oluşturuyoruz, sayfa geliştirici kodu içerir. Kodumuzu, ek olarak ASP.NET altyapısının özelliklere sahip ayrı bir sınıf dosyası otomatik olarak oluşturulur. ve olay işleyicileri, bildirim temelli biçimlendirme sayfanın sınıfı hiyerarşiye çevir.

Bir ASP.NET sayfası olduğunda oluşan otomatik kod oluşturma için bazı çok ilginç ve yararlı olanaklar niteliğindedir. Biz ne ana sayfa içerik sayfamızı tarafından kullanılan ASP.NET altyapısı bildirirseniz ana sayfaları söz konusu olduğunda, türü kesin belirlenmiş bir ürettiği `Master` bizim için özellik.

Kullanım [ `@MasterType` yönergesi](https://msdn.microsoft.com/library/ms228274.aspx) ASP.NET altyapısı içerik sayfasının ana sayfa türünde bildirmeniz. `@MasterType` Ana sayfa türü adı veya dosya yoluna yönergesi kabul edebilir. Belirtmek için `AddProduct.aspx` sayfasında kullandığı `Site.master` kendi ana sayfa olarak aşağıdaki yönergesi üst kısmına ekleyin. `AddProduct.aspx`:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

Bu yönerge bildirir adlandırılmış bir özelliği aracılığıyla ana sayfaya kesin türü belirtilmiş bir başvuru eklemek için ASP.NET altyapısı `Master`. İle `@MasterType` yerinde yönergesi, biz çağırabilirsiniz `Site.master` ana sayfanın genel özellikleri ve yöntemleri yoluyla `Master` tüm atamaları olmadan özelliği.

> [!NOTE]
> Atlarsanız `@MasterType` yönergesi, sözdizimi `Page.Master` ve `Master` aynı şeyi döndürür: sayfa ana sayfasına geniş yazılmış bir nesne. Eklerseniz `@MasterType` ardından yönergesi `Master` belirtilen ana sayfayı kesin türü belirtilmiş bir başvuru döndürür. `Page.Master`, ancak yine de geniş yazılmış bir başvuru döndürür. Neden daha kapsamlı göz atmak için bu durum geçerlidir ve nasıl `Master` özelliği oluşturulur, `@MasterType` yönergesi dahildir, bkz: [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx)'s blog girişine [ `@MasterType` ASP.NET 2. 0'ı](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx).

### <a name="updating-the-master-page-after-adding-a-new-product"></a>Yeni ürün ekledikten sonra ana sayfa güncelleştiriliyor

Bir ana sayfanın genel özellikleri ve yöntemleri içerik sayfasından çağırmak nasıl biliyoruz, güncelleştirilecek hazırız `AddProduct.aspx` yeni ürün ekledikten sonra ana sayfa yenilenir, böylece sayfa. 4. adım başında oluşturduğumuz DetailsView denetim için bir olay işleyicisi `ItemInserting` hemen yeni ürünü veritabanına eklendikten sonra yürütür olayı. Bu olay işleyicisine aşağıdaki kodu ekleyin:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

Yukarıdaki kod, her iki geniş yazılmış kullanır `Page.Master` özelliği ve kesin tür belirtilmiş `Master` özelliği. Unutmayın `GridMessageText` özelliği "*ProductName* ... eklenen" Yeni eklenen ürün değerler üzerinden erişilebilir `e.Values` koleksiyonu; görebileceğiniz gibi yeni eklenen `ProductName` değer aracılığıyla erişilen `e.Values("ProductName")`.

Şekil 8 gösterir `AddProduct.aspx` sayfası - Scott'ın Soda - yeni bir ürün hemen sonra veritabanına eklendi. Yeni eklenen ürün adını ana sayfanın etiketi içinde belirtilir ve GridView ürün ile fiyatı içerecek şekilde yenilendi unutmayın.

[![Ana sayfanın etiket ve GridView yeni eklenen ürün Göster](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**Şekil 08**: Ana sayfanın etiket ve GridView Just-Added ürün Göster ([tam boyutlu görüntüyü görmek için tıklatın](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png))

## <a name="summary"></a>Özet

İdeal olarak, bir ana sayfa ve içerik sayfalarını birbirlerinden tamamen ayrı ve etkileşimi yok düzeyini gerektirir. Ana sayfalar ve içerik sayfaları ile bu hedefe aklınızda tasarlanmalıdır vardır birkaç senaryoyu içerik sayfası, ana sayfayla arabirimi gerekir. En yaygın nedenlerinden biri, belirli bir içerik sayfasındaki ilkelerinden bazı eylemleri göre ana sayfa görüntüleme kısmını güncelleştirme etrafında ortalar.

Güzel bir haberimiz var program aracılığıyla kendi ana sayfası ile etkileşim bir içerik sayfasının olması oldukça basit olmasıdır. İçerik sayfası tarafından çağrılması gerekir işlevi kapsülleyen ana sayfasında genel özellikleri veya yöntemleri oluşturarak başlayın. Ardından, içerik sayfasındaki ana sayfanın özelliklerini ve yöntemlerini geniş yazılmış erişim `Page.Master` özelliği veya kullanım `@MasterType` ana sayfaya kesin türü belirtilmiş bir başvuru oluşturmak için yönergesi.

Sonraki öğreticide programlama yoluyla içerik sayfalarını biri ile etkileşim ana sayfaya nasıl inceleyeceğiz.

Mutlu programlama!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Erişim ve ASP.NET'te verileri güncelleştirme](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET ana sayfaları: İpuçları, püf noktalarını ve tuzakları](http://www.odetocode.com/articles/450.aspx)
- [`@MasterType` ASP.NET 2.0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [İçerik ve ana sayfalar arasında bilgi geçirme](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET Öğreticilerde verilerle çalışma](../../data-access/index.md)

### <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar 1998'de bu yana birden çok ASP/ASP.NET books ve poshbeauty.com sitesinin 4GuysFromRolla.com, Microsoft Web teknolojileri ile çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 3.5 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott, konumunda ulaşılabilir [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) veya kendi blog'da aracılığıyla [ http://ScottOnWriting.NET ](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğretici için müşteri adayı İnceleme Zack Jones oluştu. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](control-id-naming-in-content-pages-vb.md)
> [İleri](interacting-with-the-content-page-from-the-master-page-vb.md)
