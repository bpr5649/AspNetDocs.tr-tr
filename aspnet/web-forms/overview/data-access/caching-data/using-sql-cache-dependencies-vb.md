---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: SQL önbellek bağımlılıklarını kullanma (VB) | Microsoft Docs
author: rick-anderson
description: En basit önbelleğe alma stratejisi, önbelleğe alınan verilerin belirli bir süre sonra dolmasına izin verecektir. Ancak bu basit yaklaşım, önbelleğe alınan verilerin bakımı olduğu anlamına gelir...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 175169772ba04376e1bd1cb143b13a200652a9bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044798"
---
# <a name="using-sql-cache-dependencies-vb"></a>SQL Önbellek Bağımlılıklarını Kullanma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip) veya [PDF 'yi indirin](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> En basit önbelleğe alma stratejisi, önbelleğe alınan verilerin belirli bir süre sonra dolmasına izin verecektir. Ancak bu basit yaklaşım, önbelleğe alınmış verilerin temel alınan veri kaynağıyla hiçbir ilişki olmadığı anlamına gelir. Bu, çok uzun tutulan eski veriler veya çok yakında zaman aşımına uğradı. Daha iyi bir yaklaşım, SqlCacheDependency sınıfını temel alınan veriler SQL veritabanında değiştirilene kadar önbelleğe kalacak şekilde kullanmaktır. Bu öğreticide nasıl yapılacağı gösterilmektedir.

## <a name="introduction"></a>Giriş

[Mimari](caching-data-in-the-architecture-vb.md) öğreticilerde [önbelleğe alma verilerinde](caching-data-with-the-objectdatasource-vb.md) incelenen önbelleğe alma teknikleri, verileri belirli bir süre geçtikten sonra önbellekten çıkarmak için zamana dayalı bir süre sonu kullandı. Bu yaklaşım, veri açısından önbelleğe almanın performans kazançlarını dengelemek için en kolay yoldur. Bir sayfa geliştiricisi *x* saniyelik zaman aşımı süresini seçerek, yalnızca *x* saniye boyunca önbelleğe alma işleminin performans avantajlarından faydalanmayı gizlemektir, ancak verilerin en fazla *x* saniyeden daha uzun bir süre daha fazla olmadığı kadar kolay bir şekilde kalmaz. Kuşkusuz, statik veriler için *x* , [uygulama başlangıç öğreticisindeki önbelleğe alma verilerinde](caching-data-at-application-startup-vb.md) incelenen gibi Web uygulamasının kullanım ömrüne genişletilebilir.

Veritabanı verilerini önbelleğe alırken, zaman tabanlı süre sonu genellikle kullanım kolaylığı için seçilir, ancak genellikle yetersiz bir çözümdür. İdeal olarak, veritabanı verileri, temel alınan veriler veritabanında değiştirilene kadar önbellekte kalır; yalnızca önbellek çıkarılmalıdır. Bu yaklaşım, önbelleğe almanın performans avantajlarını en üst düzeye çıkarır ve eski verilerin süresini en aza indirir. Bununla birlikte, bu avantajlardan faydalanmak için, temel alınan veritabanı verilerinin ne zaman değiştirildiğini bilen ve ilgili öğeleri önbellekten çıkarmanın bir sistem olması gerekir. ASP.NET 2,0 ' den önce, sayfa geliştiricileri bu sistemi uygulamaktan sorumludur.

ASP.NET 2,0, karşılık gelen önbelleğe alınmış öğelerin çıkarılenebilmesi için veritabanında bir değişikliğin ne zaman gerçekleştiğini belirlemede bir [ `SqlCacheDependency` sınıf](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) ve gerekli altyapıyı sağlar. Temel alınan verilerin ne zaman değiştiğini belirlemek için iki teknik vardır: bildirim ve yoklama. Bildirim ve yoklamayla arasındaki farkları tartışdıktan sonra, yoklamayı desteklemek için gereken altyapıyı oluşturacağız ve ardından `SqlCacheDependency` sınıfın bildirime dayalı ve program aracılığıyla senaryolarında nasıl kullanılacağını keşfedebilirsiniz.

## <a name="understanding-notification-and-polling"></a>Bildirim ve yoklamayı anlama

Bir veritabanındaki verilerin ne zaman değiştirildiğini tespit etmek için kullanılabilecek iki teknik vardır: bildirim ve yoklama. Bildirim ile, sorgu en son çalıştırılmasından bu yana belirli bir sorgunun sonuçları değiştirildiğinde veritabanı otomatik olarak ASP.NET çalışma zamanını uyarır. bu noktada sorguyla ilişkili olan önbelleğe alınan öğeler çıkarılmıştır. Yoklama ile veritabanı sunucusu, belirli tabloların en son ne zaman güncelleştirildiği hakkında bilgileri saklar. ASP.NET çalışma zamanı, önbelleğe girildiklerinden beri hangi tabloların değiştiğini denetlemek için veritabanını düzenli aralıklarla yoklar. Verilerin değiştirildiği tablolarda ilişkili önbellek öğeleri çıkarıldı.

Bildirim seçeneği yoklamaya göre daha az kurulum gerektirir ve tablo düzeyi yerine sorgu düzeyindeki değişiklikleri izlediğinden daha ayrıntılı bir hale gelir. Ne yazık ki, bildirimler yalnızca Microsoft SQL Server 2005 ' in (yani Express olmayan sürümler) tüm sürümlerinde kullanılabilir. Ancak yoklama seçeneği 7,0 ' dan 2005 ' e kadar tüm Microsoft SQL Server sürümleri için kullanılabilir. Bu öğreticiler SQL Server 2005 ' nin Express sürümünü kullandığından yoklama seçeneğini ayarlamaya ve kullanmaya odaklanacağız. SQL Server 2005 s bildirim özellikleri hakkında daha fazla kaynak için Bu öğreticinin sonundaki daha fazla okuma bölümüne bakın.

Yoklamayla, veritabanının üç sütunu olan adlı bir tablo (,, ve) içerecek şekilde yapılandırılması gerekir `AspNet_SqlCacheTablesForChangeNotification` `tableName` `notificationCreated` `changeId` . Bu tablo, Web uygulamasında bir SQL önbellek bağımlılığında kullanılması gerekebilecek verilerin bulunduğu her tablo için bir satır içerir. `tableName`Sütun, `notificationCreated` satırın tabloya eklendiği tarihi ve saati gösteren tablonun adını belirtir. `changeId`Sütun türündedir `int` ve ilk değeri 0 ' dır. Değeri, tablodaki her değişiklikle artırılır.

Tablonun yanı sıra `AspNet_SqlCacheTablesForChangeNotification` , veritabanının BIR SQL önbellek bağımlılığında görünebilen her bir tabloya tetikleyici eklemesi de gerekir. Bu Tetikleyiciler, bir satır eklendiğinde, güncelleştirildiğinde veya silindiğinde ve içindeki tablo değeri artında yürütülür `changeId` `AspNet_SqlCacheTablesForChangeNotification` .

ASP.NET çalışma zamanı, `changeId` bir nesneyi kullanarak verileri önbelleğe alırken bir tablonun geçerli olduğunu izler `SqlCacheDependency` . Veritabanı düzenli aralıklarla denetlenir ve `SqlCacheDependency` `changeId` farklı bir `changeId` değer, veri önbellekinden bu yana tabloda değişiklik yapıldığını gösterdiği için, veritabanındaki değerden farklı olan herhangi bir nesne çıkarılmıştır.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>Adım 1: `aspnet_regsql.exe` komut satırı programını keşfetme

Yoklama yaklaşımıyla, veritabanının yukarıda açıklanan altyapıyı içerecek şekilde kurulması gerekir: önceden tanımlanmış bir tablo ( `AspNet_SqlCacheTablesForChangeNotification` ), bir dizi saklı yordam ve Web UYGULAMASıNDAKI SQL önbellek bağımlılıklarında kullanılabilecek her tablo üzerinde Tetikleyiciler. Bu tablolar, saklı yordamlar ve Tetikleyiciler, klasöründe bulunan komut satırı programı aracılığıyla oluşturulabilir `aspnet_regsql.exe` `$WINDOWS$\Microsoft.NET\Framework\version` . `AspNet_SqlCacheTablesForChangeNotification`Tabloyu ve ilişkili saklı yordamları oluşturmak için komut satırından aşağıdakileri çalıştırın:

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> Bu komutları yürütmek için belirtilen veritabanı oturum açma adı [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) ve [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) rolleri olmalıdır. Komut satırı programı tarafından veritabanına gönderilen T-SQL `aspnet_regsql.exe` ' i incelemek için, [Bu Blog girdisine](http://scottonwriting.net/sowblog/posts/10709.aspx)bakın.

Örneğin, yoklamaya yönelik altyapıyı `pubs` Windows kimlik doğrulaması kullanarak adlı bir veritabanı sunucusunda adlı bir Microsoft SQL Server veritabanına eklemek için `ScottsServer` , uygun dizine gidin ve komut satırından, şunu girin:

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

Veritabanı düzeyi altyapısı eklendikten sonra, Tetikleyicileri SQL önbellek bağımlılıklarında kullanılacak olan tablolara eklememiz gerekir. `aspnet_regsql.exe`Komut satırı programını yeniden kullanın, ancak anahtar kullanımını kullanmak yerine anahtarı kullanarak tablo adını belirtin `-t` `-ed` `-et` , örneğin:

[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

Tetikleyicileri içindeki `authors` veritabanına ve tablolarına eklemek için `titles` `pubs` `ScottsServer` şunu kullanın:

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

Bu öğretici için Tetikleyicileri `Products` , `Categories` , ve `Suppliers` tablolarına ekleyin. Adım 3 ' te belirli komut satırı sözdizimine bakacağız.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>2. Adım: Microsoft SQL Server 2005 Express Edition veritabanına başvurma`App_Data`

`aspnet_regsql.exe`Komut satırı programı, gerekli yoklama altyapısını eklemek için veritabanı ve sunucu adını gerektirir. Ancak klasörde yer alan Microsoft SQL Server 2005 Express veritabanı için veritabanı ve sunucu adı nedir `App_Data` ? Veritabanı ve sunucu adlarının ne olduğunu keşfetmesi yerine, en basit yaklaşımın veritabanını `localhost\SQLExpress` veritabanı örneğine eklemek ve [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)kullanarak verileri yeniden adlandırmak için olduğunu buldum. Makinenizde yüklü olan SQL Server 2005 ' nin tam sürümlerinden birine sahipseniz, büyük olasılıkla bilgisayarınızda zaten SQL Server Management Studio yüklü olmalıdır. Yalnızca Express Edition kullanıyorsanız, ücretsiz [Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)'ı indirebilirsiniz.

Visual Studio 'Yu kapatarak başlayın. Sonra, SQL Server Management Studio açın ve `localhost\SQLExpress` Windows kimlik doğrulaması kullanarak sunucuya bağlanmayı seçin.

![Localhost\SQLExpress sunucusuna Ekle](using-sql-cache-dependencies-vb/_static/image1.gif)

**Şekil 1**: `localhost\SQLExpress` sunucuya iliştirme

Sunucuya bağlandıktan sonra, Management Studio sunucuyu gösterir ve veritabanları, güvenlik ve diğerleri için alt klasörlere sahip olur. Veritabanları klasörüne sağ tıklayın ve Ekle seçeneğini belirleyin. Bu işlem veritabanlarını Ekle iletişim kutusunu getirir (bkz. Şekil 2). Ekle düğmesine tıklayın ve `NORTHWND.MDF` Web uygulaması klasörünüzdeki veritabanı klasörünü seçin `App_Data` .

[![Kuzey WND 'i ekleyin. App_Data klasöründen MDF veritabanı](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**Şekil 2**: `NORTHWND.MDF` veritabanını `App_Data` klasörden iliştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image2.png))

Bu, veritabanını veritabanları klasörüne ekler. Veritabanı adı, veritabanı dosyasının tam yolu olabilir veya tam yol bir [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)ile sona erer. ASPNETregsql.exe komut satırı aracını kullanırken bu uzun veritabanı adını yazmak zorunda kalmamak için \_ , yeni eklenen veritabanına sağ tıklayıp Yeniden Adlandır ' ı seçerek veritabanını daha fazla insan dostu bir adla yeniden adlandırın. Veritabanımı Dataöğreticiler olarak yeniden adlandırdım.

![Eklenmiş veritabanını daha kolay bir adla yeniden adlandırın](using-sql-cache-dependencies-vb/_static/image3.gif)

**Şekil 3**: ekli veritabanını daha kolay bir adla yeniden adlandırma

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>3. Adım: yoklama altyapısını Northwind veritabanına ekleme

Artık veritabanını klasöründen eklediğimiz için `NORTHWND.MDF` `App_Data` , yoklama altyapısını eklemeye hazırız. Veritabanını Dataöğreticileri olarak yeniden adlandırdığınız varsayılarak, aşağıdaki dört komutu çalıştırın:

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

Bu dört komutu çalıştırdıktan sonra, Management Studio veritabanı adına sağ tıklayın, görevler alt menüsüne gidin ve ayır ' ı seçin. Sonra Management Studio kapatın ve Visual Studio 'Yu yeniden açın.

Visual Studio yeniden açıldıktan sonra, Sunucu Gezgini aracılığıyla veritabanına detaya gidin. Yeni tabloya ( `AspNet_SqlCacheTablesForChangeNotification` ), yeni saklı yordamlara ve `Products` ,, `Categories` ve tablolarındaki tetikleyicilere göz önünde bulunmaktadır `Suppliers` .

![Veritabanı artık gerekli yoklama altyapısını Içerir](using-sql-cache-dependencies-vb/_static/image4.gif)

**Şekil 4**: veritabanı artık gerekli yoklama altyapısını içerir

## <a name="step-4-configuring-the-polling-service"></a>4. Adım: yoklama hizmetini yapılandırma

Veritabanında gerekli tabloları, Tetikleyicileri ve saklı yordamları oluşturduktan sonra, son adım, `Web.config` kullanılacak veritabanları belirtilerek ve yoklama sıklığı milisaniye olarak belirtilerek gerçekleştirilen yoklama hizmetini yapılandırmaktır. Aşağıdaki biçimlendirme, her saniye bir kez Northwind veritabanını yoklar.

[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

`name` `<add>` Öğedeki değer (northwinddb), okunabilir bir adı belirli bir veritabanıyla ilişkilendirir. SQL önbellek bağımlılıklarıyla çalışırken, burada tanımlanan veritabanı adına ve önbelleğe alınan verilerin dayandığı tabloya başvurmaları gerekir. `SqlCacheDependency`SQL önbellek bağımlılıklarını adım 6 ' da önbelleğe alınmış verilerle programlı bir şekilde ilişkilendirmek için sınıfını nasıl kullanacağınızı inceleyeceğiz.

SQL önbellek bağımlılığı kurulduktan sonra, yoklama sistemi, öğelerde tanımlanan veritabanlarına `<databases>` her `pollTime` milisaniyeye bağlanır ve `AspNet_SqlCachePollingStoredProcedure` saklı yordamı yürütür. Komut satırı aracını kullanarak adım 3 ' te geri eklenen bu saklı yordam `aspnet_regsql.exe` , `tableName` `changeId` içindeki her bir kayıt için ve değerlerini döndürür `AspNet_SqlCacheTablesForChangeNotification` . Güncel olmayan SQL önbelleği bağımlılıkları önbellekten çıkarıldı.

Bu `pollTime` ayar performans ve veri kullanımı arasında bir zorunluluğunu getirir sunar. Küçük bir `pollTime` değer, veritabanının istek sayısını artırır, ancak eski verileri önbellekten daha hızlı bir şekilde çıkarır. Daha büyük bir `pollTime` değer, veritabanı isteklerinin sayısını azaltır, ancak arka uç verilerinin ne zaman değiştiği ve ilgili önbellek öğelerinin ne zaman çıkarıldığı arasındaki gecikmeyi arttırır. Neyse ki veritabanı isteği basit ve hafif bir tablodan yalnızca birkaç satır döndüren basit bir saklı yordam yürütüyor. Ancak, `pollTime` veritabanı erişimi ile uygulamanızın veri kullanımı arasında ideal bir denge bulmak için farklı değerlerle denemeler yapın. `pollTime`İzin verilen en küçük değer 500 ' dir.

> [!NOTE]
> Yukarıdaki örnek, öğesinde tek bir `pollTime` değer sağlar `<sqlCacheDependency>` , ancak isteğe bağlı olarak `pollTime` , öğesinde değeri belirtebilirsiniz `<add>` . Bu, birden çok veritabanınız varsa ve veritabanı başına yoklama sıklığını özelleştirmek istiyorsanız yararlıdır.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>5. Adım: bildirimli olarak SQL önbellek bağımlılıklarıyla çalışma

1 ile 4 arasındaki adımlarda, gerekli veritabanı altyapısını ayarlama ve yoklama sistemini yapılandırma hakkında baktık. Bu altyapıda, artık programlı veya bildirime dayalı teknikler kullanarak ilişkili bir SQL önbellek bağımlılığı ile veri önbelleğine öğe ekleyebiliriz. Bu adımda, SQL önbellek bağımlılıklarıyla bildirimli olarak nasıl çalışacağımız anlatılmaktadır. Adım 6 ' da programlama yaklaşımına bakacağız.

[ObjectDataSource Ile önbelleğe alma verileri](caching-data-with-the-objectdatasource-vb.md) , ObjectDataSource 'un bildirime dayalı önbelleğe alma yeteneklerini araştırın. Yalnızca `EnableCaching` özelliğini `True` ve `CacheDuration` özelliğini bir zaman aralığına ayarlayarak, ObjectDataSource, belirtilen Aralık için temel alınan nesnesinden döndürülen verileri otomatik olarak önbelleğe alınır. ObjectDataSource bir veya daha fazla SQL önbellek bağımlılığı da kullanabilir.

SQL önbellek bağımlılıklarını bildirimli olarak kullanmayı göstermek için, `SqlCacheDependencies.aspx` sayfada sayfayı açın `Caching` ve araç kutusundan bir GridView 'u tasarımcı üzerine sürükleyin. GridView 'u `ID` `ProductsDeclarative` akıllı etiketiyle ve adlı yeni bir ObjectDataSource ile bağlamayı seçin `ProductsDataSourceDeclarative` .

[![Productsdatasourcebildirime adlı yeni bir ObjectDataSource oluşturun](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**Şekil 5**: adlı yeni bir ObjectDataSource oluşturun `ProductsDataSourceDeclarative` ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image4.png))

ObjectDataSource 'ı sınıfını kullanacak şekilde yapılandırın `ProductsBLL` ve seçim sekmesindeki açılan listeyi olarak ayarlayın `GetProducts()` . GÜNCELLEŞTIRME sekmesinde, `UpdateProduct` üç giriş parametresi olan aşırı yüklemeyi seçin- `productName` , `unitPrice` , ve `productID` . Ekle ve SIL sekmelerinde açılan listeleri (yok) olarak ayarlayın.

[![UpdateProduct Overload ' i üç giriş parametresiyle kullanın](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**Şekil 6**: üç giriş parametresiyle UpdateProduct Overload kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image6.png))

[![INSERT ve DELETE sekmeleri için açılan listeyi (yok) olarak ayarlayın](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**Şekil 7**: ekleme ve silme sekmeleri Için açılan listeyi (yok) olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image8.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, veri alanlarının her biri için GridView 'da BoundFields ve CheckBoxFields oluşturur. Tüm alanları,, ve ' ı kaldırın `ProductName` `CategoryName` `UnitPrice` ve bu alanları uygun gördüğünüz şekilde biçimlendirin. GridView s akıllı etiketinde, Sayfalamayı Etkinleştir, sıralamayı etkinleştir ve Düzenle onay kutularını etkinleştir ' i işaretleyin. Visual Studio, ObjectDataSource `OldValuesParameterFormatString` 'un özelliğini olarak ayarlar `original_{0}` . GridView s düzenleme özelliğinin düzgün çalışması için, bu özelliği tamamen bildirime dayalı sözdiziminden kaldırın ya da varsayılan değerine geri ayarlayın `{0}` .

Son olarak, GridView 'un üzerine bir etiket Web denetimi ekleyin ve `ID` özelliğini `ODSEvents` ve `EnableViewState` özelliğini olarak ayarlayın `False` . Bu değişiklikleri yaptıktan sonra, sayfanın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir. SQL önbellek bağımlılığı işlevini göstermek için gerekli olmayan GridView alanlarında çok sayıda Aesthetic Characteristics özelleştirmesi yaptık.

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

Ardından, ObjectDataSource için olay işleyicisi oluşturun `Selecting` ve içinde aşağıdaki kodu ekleyin:

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

ObjectDataSource 'un `Selecting` olayının yalnızca temel alınan nesnesinden veri alırken harekete geçirilir. ObjectDataSource, verilere kendi önbelleğinden eriştiğinde bu olay tetiklenmez.

Şimdi bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Henüz herhangi bir önbelleğe alma işlemi gerçekleştirdiğimiz için, kılavuza her sayfa, sıralama veya düzenleme yaparken sayfada, Şekil 8 ' i gösterdiği şekilde, "olay tetiklendi" metnini görüntülemesi gerekir.

[![GridView, her Sayfalanışında, düzenlendiğinde veya sıralandığında olay seçen ObjectDataSource ateşlenir](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**Şekil 8**: bir `Selecting` GridView her Sayfalanışında, düzenlendiğinde veya sıralandığında ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-sql-cache-dependencies-vb/_static/image10.png)), ObjectDataSource s olayı ateşlenir

[ObjectDataSource Ile verileri önbelleğe alma](caching-data-with-the-objectdatasource-vb.md) bölümünde gördüğünüz gibi, özelliği olarak ayarlamak, `EnableCaching` ObjectDataSource 'un `True` verilerini özelliği tarafından belirtilen süre için önbelleğe almasına neden olur `CacheDuration` . ObjectDataSource Ayrıca, bir veya daha fazla SQL önbellek bağımlılıklarını, bu model kullanılarak önbelleğe alınmış verilere ekleyen bir [ `SqlCacheDependency` özelliğine](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)sahiptir:

[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

Burada *DatabaseName* , içindeki öğesinin özniteliğinde belirtildiği gibi veritabanının adıdır `name` `<add>` `Web.config` ve *TableName* veritabanı tablosunun adıdır. Örneğin, Northwind s tablosuna karşı bir SQL önbellek bağımlılığı temelinde verileri süresiz olarak önbelleğe alan bir ObjectDataSource oluşturmak için `Products` , ObjectDataSource s `EnableCaching` özelliğini `True` ve `SqlCacheDependency` özelliğini northwinddb: Products olarak ayarlayın.

> [!NOTE]
> *and* `EnableCaching` `True` ' I, `CacheDuration` zaman aralığı ' nı ve `SqlCacheDependency` VERITABANı ve tablo adlarını ayarlayarak bir SQL önbellek bağımlılığı ve zaman tabanlı süre sonu kullanabilirsiniz. Zaman tabanlı süre sonuna ulaşıldığında veya yoklama sistemi temeldeki veritabanı verilerinin değiştiğini, hangisi önce gerçekleştiğine bağlı olarak, ObjectDataSource bu verileri çıkarır.

İçindeki GridView, `SqlCacheDependencies.aspx` iki tablodaki verileri görüntüler `Products` ve `Categories` (ürün `CategoryName` alanı bir üzerinde bir ile alınır `JOIN` `Categories` ). Bu nedenle, iki SQL önbellek bağımlılığı belirtmek istiyoruz: NorthwindDB: Products; NorthwindDB: Kategoriler.

[![Ürün ve kategorilerdeki SQL önbellek bağımlılıklarını kullanarak önbelleğe almayı desteklemek için ObjectDataSource 'u yapılandırma](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**Şekil 9**: ve üzerinde SQL önbellek bağımlılıklarını kullanarak önbelleğe almayı desteklemek için ObjectDataSource 'u yapılandırma `Products` `Categories` ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image12.png))

Önbelleğe almayı desteklemek için ObjectDataSource 'u yapılandırdıktan sonra, sayfayı bir tarayıcı aracılığıyla geri ziyaret edin. Yine, ' seçme olayı tetiklendi ' metni ilk sayfada görünmelidir, ancak sayfalama, sıralama veya Düzenle ya da Iptal düğmelerine tıklanması gerekir. Bunun nedeni, veriler ObjectDataSource s önbelleğine yüklendikten sonra, `Products` veya `Categories` tabloları değiştirilene veya veriler GridView aracılığıyla güncelleştirilene kadar kalır.

Kılavuz aracılığıyla hata ettikten ve ' olay harekete geçen metnin eksik olduğunu belirterek, yeni bir tarayıcı penceresi açın ve Düzenle, ekleme ve silme bölümünde temel bilgiler öğreticisine gidin ( `~/EditInsertDelete/Basics.aspx` ). Bir ürünün adını veya fiyatını güncelleştirin. Ardından, ilk tarayıcı penceresine, farklı bir veri sayfası görüntüleyin, Kılavuzu sıralayın veya bir satır s Düzenle düğmesine tıklayın. Bu kez, temel alınan veritabanı verileri değiştirildiğinden ' seçme olayı yeniden görünür olmalıdır (bkz. Şekil 10). Metin görünmezse, birkaç dakika bekleyip yeniden deneyin. Yoklama hizmetinin tabloda her milisaniyeye yönelik değişiklikleri denetleyeceğini unutmayın `Products` . bu `pollTime` nedenle, temeldeki verilerin ne zaman güncelleştirildiği ve önbelleğe alınan verilerin çıkarılma sıklığı arasında bir gecikme vardır.

[![Ürün tablosunu değiştirme, önbelleğe alınmış ürün verilerini Çıkarşır](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**Şekil 10**: ürün tablosunu değiştirme, önbelleğe alınmış ürün verilerini çıkarma ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-sql-cache-dependencies-vb/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>6. Adım: program aracılığıyla `SqlCacheDependency` sınıfla çalışma

Mimari öğreticisindeki [önbelleğe alma verileri](caching-data-in-the-architecture-vb.md) ,, ObjectDataSource ile ön belleğe sıkı bir şekilde eşlenmesinin aksine, mimaride ayrı bir önbelleğe alma katmanı kullanmanın avantajlarından bakıyordu. Bu öğreticide `ProductsCL` , veri önbelleğiyle programlı bir şekilde çalıştığını göstermek için bir sınıf oluşturduk. Önbelleğe alma katmanında SQL önbellek bağımlılıklarını kullanmak için `SqlCacheDependency` sınıfını kullanın.

Yoklama sistemiyle, bir `SqlCacheDependency` nesne belirli bir veritabanı ve tablo çifti ile ilişkilendirilmelidir. Aşağıdaki kod, örneğin, `SqlCacheDependency` Northwind veritabanı tablosunu temel alan bir nesne oluşturur `Products` :

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

S yapıcısına yönelik iki giriş parametresi `SqlCacheDependency` sırasıyla veritabanı ve tablo adlarıdır. ObjectDataSource 'lar `SqlCacheDependency` özelliği gibi, kullanılan veritabanı adı `name` içindeki öğesinin özniteliğinde belirtilen değerle aynıdır `<add>` `Web.config` . Tablo adı, veritabanı tablosunun gerçek adıdır.

Bir `SqlCacheDependency` öğesini veri önbelleğine eklenen bir öğeyle ilişkilendirmek için, `Insert` bağımlılığı kabul eden yöntem aşırı yüklemelerinin birini kullanın. Aşağıdaki kod, tanımsız bir süre için veri önbelleğine *değer* ekler, ancak tablodaki ile ilişkilendirir `SqlCacheDependency` `Products` . Kısacası, *value* bellek kısıtlamaları nedeniyle veya yoklama sistemi `Products` tablonun önbelleğe alındığı zamandan sonra değiştiğini algıladığından, değer önbellekte kalır.

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

Önbelleğe alma katmanı s `ProductsCL` sınıfı şu anda `Products` tablodaki verileri 60 saniyelik zaman tabanlı süre sonu ile önbelleğe alır. Bunun yerine SQL önbellek bağımlılıklarını kullanması için bu sınıfı güncelleştirmesine izin verin. `ProductsCL` `AddCacheItem` Verileri önbelleğe eklemekten sorumlu olan sınıf s yöntemi şu anda aşağıdaki kodu içerir:

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

Bu kodu `SqlCacheDependency` , önbellek bağımlılığı yerine bir nesne kullanacak şekilde güncelleştirin `MasterCacheKeyArray` :

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

Bu işlevi test etmek için, varolan GridView 'un altındaki sayfaya bir GridView ekleyin `ProductsDeclarative` . Bu yeni GridView `ID` `ProductsProgrammatic` öğesini akıllı etiketiyle ve olarak ayarlayın, adlı yeni bir ObjectDataSource 'a bağlayın `ProductsDataSourceProgrammatic` . , `ProductsCL` Select ve Update sekmelerindeki açılan listeleri sırasıyla ve olarak ayarlayarak, bu sınıfı kullanmak Için ObjectDataSource 'u yapılandırın `GetProducts` `UpdateProduct` .

[![ObjectDataSource 'ı ProductsCL sınıfını kullanacak şekilde yapılandırma](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**Şekil 11**: bir sınıfı kullanmak için ObjectDataSource 'ı yapılandırma `ProductsCL` ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image16.png))

[![SELECT Tab s açılır listesinden GetProducts yöntemini seçin](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**Şekil 12**: `GetProducts` seçme sekmesi seç açılan listesinden yöntemi seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image18.png))

[![GÜNCELLEŞTIRME sekmesi açılan listesinden UpdateProduct yöntemini seçin](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**Şekil 13**: güncelleştirme sekmesi açılan listesinden UpdateProduct yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-sql-cache-dependencies-vb/_static/image20.png))

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra Visual Studio, veri alanlarının her biri için GridView 'da BoundFields ve CheckBoxFields oluşturur. Bu sayfaya eklenen ilk GridView gibi, tüm alanları,, ve ' ı `ProductName` kaldırın `CategoryName` `UnitPrice` ve bu alanları uygun gördüğünüz şekilde biçimlendirin. GridView s akıllı etiketinde, Sayfalamayı Etkinleştir, sıralamayı etkinleştir ve Düzenle onay kutularını etkinleştir ' i işaretleyin. ObjectDataSource ile birlikte `ProductsDataSourceDeclarative` , Visual Studio `ProductsDataSourceProgrammatic` ObjectDataSource `OldValuesParameterFormatString` 'un özelliğini olarak ayarlar `original_{0}` . GridView s düzenleme özelliğinin düzgün çalışması için, bu özelliği olarak ayarlayın `{0}` (veya özellik atamasını bildirim temelli sözdiziminden tamamen kaldırın).

Bu görevleri tamamladıktan sonra elde edilen GridView ve ObjectDataSource bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

Önbelleğe alma katmanında SQL önbellek bağımlılığını test etmek için sınıf s yönteminde bir kesme noktası ayarlayın `ProductCL` `AddCacheItem` ve ardından hata ayıklamayı başlatın. İlk ziyaretinizden `SqlCacheDependencies.aspx` , verilerin ilk kez istendiği ve önbelleğe yerleştirilmesi için kesme noktası isabet etmelidir. Sonra, GridView 'da bir başka sayfaya geçin veya sütunlardan birini sıralayın. Bu, GridView 'un verilerini yeniden kaydetmesine neden olur, ancak `Products` veritabanı tablosu değiştirilmediğinden verilerin önbellekte bulunması gerekir. Veriler önbellekte tekrar tekrarlanmadığından bilgisayarınızda yeterli kullanılabilir bellek olduğundan emin olun ve yeniden deneyin.

GridView 'un birkaç sayfasında sayfaladıktan sonra ikinci bir tarayıcı penceresi açın ve Düzenle, ekleme ve silme bölümünde () temel kavramlar öğreticisine gidin `~/EditInsertDelete/Basics.aspx` . Products tablosundan bir kaydı güncelleştirin ve ardından ilk tarayıcı penceresinden yeni bir sayfa görüntüleyin veya sıralama başlıklarından birine tıklayın.

Bu senaryoda, iki seçenekten birini göreceksiniz: kesme noktası isabet edecek ve bu, önbellekteki verilerin veritabanındaki değişiklik nedeniyle çıkarıldığını belirtir; ya da kesme noktasına isabet edilmez, yani `SqlCacheDependencies.aspx` artık eski veriler gösteriliyor. Kesme noktası isabet ettirilmemişse, büyük olasılıkla yoklama hizmeti, verilerin değiştiği bu yana başlatılmamıştır. Yoklama hizmetinin tabloda her milisaniyeye yönelik değişiklikleri denetleyeceğini unutmayın `Products` . bu `pollTime` nedenle, temeldeki verilerin ne zaman güncelleştirildiği ve önbelleğe alınan verilerin çıkarılma sıklığı arasında bir gecikme vardır.

> [!NOTE]
> Bu gecikmenin, ' deki GridView aracılığıyla ürünlerden birini düzenlediğinizde görünmesi daha olasıdır `SqlCacheDependencies.aspx` . Mimari öğreticideki [önbelleğe alma verilerinde](caching-data-in-the-architecture-vb.md) , `MasterCacheKeyArray` sınıf s yöntemi aracılığıyla düzenlenmekte olan verilerin `ProductsCL` önbellekten çıkarılbildiğinden emin olmak için önbellek bağımlılığını ekledik `UpdateProduct` . Ancak, bu adımda daha önce açıklanan yöntemi değiştirirken bu önbellek bağımlılığını değiştirdik `AddCacheItem` ve bu nedenle, `ProductsCL` yoklama sistemi tabloya yapılan değişikliği notlana kadar sınıf önbelleğe alınmış verileri göstermeye devam edecektir `Products` . `MasterCacheKeyArray`Adım 7 ' de önbellek bağımlılığını yeniden nasıl oluşturacağınız anlatılmaktadır.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>7. Adım: birden çok bağımlılığı önbelleğe alınmış öğeyle Ilişkilendirme

`MasterCacheKeyArray`Önbellek bağımlılığının, onunla ilişkilendirilen tek bir öğe güncelleştirildiği sırada *Tüm* ürünle ilgili verilerin önbellekten çıkarıldığından emin olmak için kullanıldığını unutmayın. Örneğin, `GetProductsByCategoryID(categoryID)` yöntemi `ProductsDataTables` her benzersiz *CategoryID* değeri için örnekleri önbelleğe alır. Bu nesnelerden biri çıkarılmışsa, `MasterCacheKeyArray` önbellek bağımlılığı diğerlerinin de kaldırılmasını sağlar. Bu önbellek bağımlılığı olmadan, önbelleğe alınmış veriler değiştirildiğinde, diğer önbelleğe alınmış ürün verilerinin eski olma olasılığı vardır. Sonuç olarak, `MasterCacheKeyArray` SQL önbellek bağımlılıklarını kullanırken önbellek bağımlılığını koruduğumuz önem taşır. Ancak, veri önbelleği s `Insert` yöntemi yalnızca tek bir bağımlılık nesnesine izin verir.

Ayrıca, SQL önbellek bağımlılıklarıyla çalışırken birden çok veritabanı tablosunu bağımlılıklar olarak ilişkilendirmemiz gerekebilir. Örneğin, `ProductsDataTable` sınıfında önbelleğe alınan, `ProductsCL` her ürün için kategori ve Tedarikçi adlarını içerir, ancak `AddCacheItem` Yöntem yalnızca bir bağımlılığı kullanır `Products` . Bu durumda, Kullanıcı bir kategorinin veya tedarikçinin adını Güncelleştir, önbelleğe alınmış ürün verileri önbellekte kalır ve güncel olmayacaktır. Bu nedenle, önbelleğe alınmış ürün verilerinin yalnızca `Products` tablo değil, `Categories` ve tablolarında de bağımlı olmasını istiyoruz `Suppliers` .

[ `AggregateCacheDependency` Sınıfı](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) , birden çok bağımlılığı bir önbellek öğesiyle ilişkilendirmek için bir yol sağlar. Bir örnek oluşturarak başlayın `AggregateCacheDependency` . Ardından, s metodunu kullanarak bağımlılıklar kümesini ekleyin `AggregateCacheDependency` `Add` . Öğesi bundan sonra veri önbelleğine eklenirken `AggregateCacheDependency` örneği geçirin. *any* `AggregateCacheDependency` Örnek s bağımlılıklarından herhangi biri değiştiğinde, önbelleğe alınmış öğe kaldırılır.

Aşağıda sınıf s yöntemi için güncelleştirilmiş kod gösterilmektedir `ProductsCL` `AddCacheItem` . Yöntemi `MasterCacheKeyArray` `SqlCacheDependency` ,, `Products` `Categories` ve tablolarının nesneleriyle birlikte önbellek bağımlılığı oluşturur `Suppliers` . Bunların hepsi adlı bir nesnede birleştirilir `AggregateCacheDependency` `aggregateDependencies` ve daha sonra `Insert` yöntemine geçirilir.

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

Bu yeni kodu test edin. Şimdi `Products` , `Categories` veya tablolarında yapılan değişiklikler `Suppliers` önbelleğe alınmış verilerin çıkarılmasına neden olur. Üstelik, `ProductsCL` `UpdateProduct` GridView aracılığıyla bir ürün düzenlenirken çağrılan sınıf s yöntemi, `MasterCacheKeyArray` önbelleğe alınmış `ProductsDataTable` ve çıkarılan verilerin bir sonraki istekte yeniden alınmasına neden olan önbellek bağımlılığını çıkarır.

> [!NOTE]
> SQL önbellek bağımlılıkları, [çıktı önbelleği](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)ile de kullanılabilir. Bu işlevselliğin bir gösterimi için bkz. [SQL Server ile ASP.net çıktı önbelleği kullanma](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx).

## <a name="summary"></a>Özet

Veritabanı verilerini önbelleğe alırken, veriler veritabanında değiştirilene kadar önbellekte kalır. ASP.NET 2,0 ile SQL önbellek bağımlılıkları hem bildirim temelli hem de programlı senaryolarda oluşturulabilir ve kullanılabilir. Bu yaklaşımla ilgili güçlüklerden biri, verilerin değiştirildiği zaman keşfederdir. Microsoft SQL Server 2005 ' nin tam sürümleri, bir sorgu sonucu değiştiğinde bir uygulamayı uyarabilecek bildirim özellikleri sağlar. SQL Server 2005 ' nin Express sürümü ve SQL Server daha eski sürümleri için bunun yerine bir yoklama sisteminin kullanılması gerekir. Neyse ki, gerekli yoklama altyapısını ayarlama oldukça basittir.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Microsoft SQL Server 2005 ' de sorgu bildirimlerini kullanma](https://msdn.microsoft.com/library/ms175110.aspx)
- [Sorgu bildirimi oluşturma](https://msdn.microsoft.com/library/ms188669.aspx)
- [ASP.NET 'de sınıfıyla önbelleğe alma `SqlCacheDependency`](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server kayıt aracı ( `aspnet_regsql.exe` )](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [Genel Bakış `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [4GuysFromRolla.com](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Adresinden erişilebilir [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla bulunabilir [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Marko Rangel, Teresa Murphy ve Tepton Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, bana bir satır bırakın [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](caching-data-at-application-startup-vb.md)
