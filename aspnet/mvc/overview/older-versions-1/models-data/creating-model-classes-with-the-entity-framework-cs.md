---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Varlık Çerçevesi (C#) ile Model Sınıfları Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Bu eğitimde, Microsoft Entity Framework ile ASP.NET MVC'yi nasıl kullanacağınızı öğrenirsiniz. Varlık Sihirbazı'nı ADO.NET Bir Varlık Da oluşturmak için nasıl kullanacağınızı öğrenirsiniz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542670"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Entity Framework ile Model Sınıfları Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Bu eğitimde, Microsoft Entity Framework ile ASP.NET MVC'yi nasıl kullanacağınızı öğrenirsiniz. ADO.NET varlık veri modeli oluşturmak için Varlık Sihirbazı'nı nasıl kullanacağınızı öğrenirsiniz. Bu öğretici boyunca, Varlık Çerçevesi'ni kullanarak veritabanı verilerinin nasıl seçil, eklen, güncelleştirilip silinileceklerini gösteren bir web uygulaması oluşturuyoruz.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması oluştururken Microsoft Entity Framework'ü kullanarak veri erişim sınıflarını nasıl oluşturabileceğinizi açıklamaktır. Bu öğretici, Microsoft Entity Framework hakkında daha önce hiçbir bilgi edinmez. Bu öğreticinin sonunda, veritabanı kayıtlarını seçmek, eklemek, güncelleştirmek ve silmek için Varlık Çerçevesi'ni nasıl kullanacağınızı anlamış olursunuz.

Microsoft Entity Framework, veritabanından otomatik olarak veri erişim katmanı oluşturmanıza olanak tanıyan bir Nesne İlişkisel Eşleme (O/RM) aracıdır. Varlık Çerçevesi, veri erişim sınıflarınızı elle oluşturma zahmetli çalışmalarından kaçınmanızı sağlar.

Microsoft Entity Framework'ASP.NET MVC ile nasıl kullanabileceğinizi göstermek için basit bir örnek uygulama oluşturacağız. Film veritabanı kayıtlarını görüntülemenizi ve görüntülemenizi sağlayan bir Film Veritabanı uygulaması oluştururuz.

Bu öğretici, Service Pack 1 ile Visual Studio 2008 veya Visual Web Developer 2008 sahip olduğunu varsayar. Varlık Çerçevesini kullanmak için Servis Paketi 1'e ihtiyacınız var. Visual Studio 2008 Service Pack 1 veya Visual Web Developer'ı Service Pack 1 ile aşağıdaki adresten indirebilirsiniz:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC ile Microsoft Entity Framework arasında önemli bir bağlantı yoktur. Varlık Çerçevesi'nin ASP.NET MVC ile kullanabileceğiniz çeşitli alternatifler vardır. Örneğin, MVC Model sınıflarınızı Microsoft LINQ to SQL, NHibernate veya SubSonic gibi diğer O/RM araçlarını kullanarak oluşturabilirsiniz.

## <a name="creating-the-movie-sample-database"></a>Film Örnek Veritabanı oluşturma

Film Veritabanı uygulaması, aşağıdaki sütunları içeren Filmler adlı bir veritabanı tablosu kullanır:

| Sütun Adı | Veri Türü | Nulls'a izin mi ver? | Birincil Anahtar mı? |
| --- | --- | --- | --- |
| Kimlik | int | False | True |
| Başlık | nvarchar(100) | False | False |
| Yönetmen | nvarchar(100) | False | False |

Aşağıdaki adımları izleyerek bu tabloyu ASP.NET bir MVC projesine ekleyebilirsiniz:

1. Çözüm Gezgini\_penceresindeki Uygulama Verileri klasörüne sağ tıklayın ve **Ekle, Yeni Öğe** seçeneğini seçin.
2. Yeni **Öğe Ekle** iletişim kutusundan **SQL Server Database'i**seçin, veritabanına MoviesDB.mdf adını verin ve **Ekle** düğmesini tıklatın.
3. Server Explorer/Database Explorer penceresini açmak için MoviesDB.mdf dosyasını çift tıklatın.
4. MoviesDB.mdf veritabanı bağlantısını genişletin, Tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**seçeneğini seçin.
5. Tablo Tasarımcısı'na Kimlik, Başlık ve Yönetmen sütunlarını ekleyin.
6. Filmler adlı yeni tabloyu kaydetmek için **Kaydet** düğmesini (disket simgesi vardır) tıklatın.

Filmler veritabanı tablosunu oluşturduktan sonra, tabloya bazı örnek veriler eklemeniz gerekir. Filmler tablosuna sağ tıklayın ve **Tablo Verilerini Göster**menüsü seçeneğini seçin. Görünen ızgaraya sahte film verileri girebilirsiniz.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET Varlık Veri Modeli oluşturma

Varlık Çerçevesini kullanmak için bir Varlık Veri Modeli oluşturmanız gerekir. Bir veritabanından otomatik olarak bir Varlık Veri Modeli oluşturmak için Visual Studio *Entity Data Model Wizard'dan* yararlanabilirsiniz.

Şu adımları uygulayın:

1. Çözüm Gezgini penceresindeki Modeller klasörüne sağ tıklayın ve **Ekle, Yeni Öğe**seçeneğini seçin.
2. Yeni **Öğe Ekle** iletişim kutusunda, Veri kategorisini seçin (Bkz. Şekil 1).
3. ADO.NET **Varlık Veri Modeli** şablonunu seçin, Varlık Veri Modeli'ne MoviesDBModel.edmx adını verin ve **Ekle** düğmesini tıklatın. **Ekle** düğmesini tıklattığınızda Veri Modeli Sihirbazı başlatın.
4. Model **İçeriği Seç** adımında, **veritabanından Oluştur** seçeneğini seçin ve **Sonraki** düğmesini tıklatın (Bkz. Şekil 2).
5. Veri **Bağlantınızı Seçin** adımda, MoviesDB.mdf veritabanı bağlantısını seçin, varlıklar bağlantı ayarları adı MoviesDBEntities'ı girin ve **Sonraki** düğmesini tıklatın (Bkz. Şekil 3).
6. Veritabanı **Nesnelerinizi Seç** adımında, Film veritabanı tablosunu seçin ve **Finish** düğmesini tıklatın (Bkz. Şekil 4).

Bu adımları tamamladıktan sonra, varlık veri modeli tasarımcısı (Entity Designer) ADO.NET açılır.

**Şekil 1 – Yeni Bir Varlık Veri Modeli Oluşturma**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**Şekil 2 – Model İçerikleri Adım Seçin**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**Şekil 3 – Veri Bağlantınızı Seçin**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**Şekil 4 – Veritabanı Nesnelerinizi Seçin**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET Varlık Veri Modelinin Değiştirilmesi

Bir Varlık Veri Modeli oluşturduktan sonra, Varlık Tasarımcısı'ndan yararlanarak modeli değiştirebilirsiniz (Bkz. Şekil 5). Çözüm Gezgini penceresindeki Modeller klasöründe yer alan MoviesDBModel.edmx dosyasını çift tıklatarak Varlık Tasarımcısı'nı istediğiniz zaman açabilirsiniz.

**Şekil 5 – ADO.NET Varlık Veri Modeli Tasarımcısı**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

Örneğin, Varlık Modeli Veri Sihirbazı'nın oluşturduğu sınıfların adlarını değiştirmek için Varlık Tasarımcısı'nı kullanabilirsiniz. Sihirbaz, Filmler adlı yeni bir veri erişim sınıfı oluşturdu. Başka bir deyişle, Sihirbaz sınıfa veritabanı tablosuyla aynı adı verdi. Bu sınıfı belirli bir Film örneğini temsil etmek için kullanacağımızdan, sınıfı Filmler'den Filme yeniden adlandırmalıyız.

Bir varlık sınıfını yeniden adlandırmak istiyorsanız, Varlık Tasarımcısı'ndaki sınıf adını çift tıklatıp yeni bir ad girebilirsiniz (Bkz. Şekil 6). Alternatif olarak, Varlık Tasarımcısı'nda bir varlık seçtikten sonra Özellikler penceresindeki bir varlığın adını değiştirebilirsiniz.

**Şekil 6 – Varlık adını değiştirme**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

Kaydet düğmesini (disketsimgesi) tıklatarak bir değişiklik yaptıktan sonra Varlık Veri Modelinizi kaydetmeyi unutmayın. Arka planda, Varlık Tasarımcısı c# sınıfları kümesi oluşturur. Çözüm Gezgini penceresinden MoviesDBModel.Designer.cs dosyasını açarak bu sınıfları görüntüleyebilirsiniz.

Değişiklikleriniz Varlık Tasarımcısı'nı bir sonraki kullanımınızda üzerine yazılanınacağı için Designer.cs dosyasındaki kodu değiştirmeyin. Designer.cs dosyasında tanımlanan varlık sınıflarının işlevselliğini genişletmek istiyorsanız, ayrı dosyalarda *kısmi sınıflar* oluşturabilirsiniz.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Varlık Çerçevesi ile Veritabanı Kayıtlarını Seçme

Film kayıtlarının listesini görüntüleyen bir sayfa oluşturarak Film Veritabanı uygulamamızı oluşturmaya başlayalım. Listeleme 1'deki Ev denetleyicisi Index() adlı bir eylemi ortaya çıkarır. Index() eylemi, Varlık Çerçevesi'nden yararlanarak film veritabanı tablosundaki tüm film kayıtlarını döndürür.

**Listeleme 1 – Denetleyiciler\HomeController.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

Listeleme 1'deki denetleyicinin bir oluşturucu içerdiğine dikkat edin. Oluşturucu db adlı sınıf düzeyinde \_bir alan başlatılmasını. db alanı, \_Microsoft Entity Framework tarafından oluşturulan veritabanı varlıklarını temsil eder. \_db alanı, Entity Designer tarafından oluşturulan MoviesDBEntities sınıfının bir örneğidir.

TheMoviesDBEntities sınıfını Ana Sayfa denetleyicisinde kullanmak için MovieEntityApp.Models ad alanını *(MVCProjectName)* almanız gerekir. Modeller).

DB alanı, \_Filmler veritabanı tablosundaki kayıtları almak için Index() eylemi içinde kullanılır. Db \_ifadesi. MovieSet, Filmler veritabanı tablosundaki tüm kayıtları temsil eder. ToList() yöntemi, film kümesini film nesnelerinin genel bir koleksiyonuna&lt;&gt;dönüştürmek için kullanılır (List Movie).

Film kayıtları LINQ'dan Varlıklara yardımıyla alınır. Listeleme 1'deki Dizin() eylemi, veritabanı kayıtları kümesini almak için LINQ *yöntemi sözdizimini* kullanır. İsterseniz, bunun yerine LINQ *sorgu sözdizimini* kullanabilirsiniz. Aşağıdaki iki ifadeler çok aynı şeyi yapmak:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

En sezgisel bulduğunuz linq sözdizimini (yöntem sözdizimi veya sorgu sözdizimi) hangisinde kullanın. İki yaklaşım arasında performans farkı yoktur – tek fark stildir.

Listeleme 2'deki görünüm film kayıtlarını görüntülemek için kullanılır.

**Listeleme 2 – Görünümler\Ana Sayfa\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

Listeleme 2'deki görünüm, her film kaydında yineleyen ve film kaydının Başlık ve Yönetmen özelliklerinin değerlerini görüntüleyen **bir foreach** döngüsü içerir. Her kaydın yanında bir Düzenle ve Sil bağlantısının görüntülendiğine dikkat edin. Ayrıca, görünümün alt kısmında Film Ekle bağlantısı görünür (Bkz. Şekil 7).

**Şekil 7 – Endeks görünümü**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

Dizin görünümü *yazılı*bir görünümdür. Dizin görünümü, &lt;Model özelliğini film nesnelerinin güçlü bir şekilde yazılan genel Liste koleksiyonuna (Film Listesi)&lt;atan *bir Devralma* özniteliğine sahip %@ Sayfa %&gt; yönergesi içerir.

## <a name="inserting-database-records-with-the-entity-framework"></a>Veritabanı Kayıtlarını Varlık Çerçevesine Ekleme

Veritabanı tablosuna yeni kayıtlar eklemeyi kolaylaştırmak için Varlık Çerçevesi'ni kullanabilirsiniz. Listeleme 3, Film veritabanı tablosuna yeni kayıtlar eklemek için kullanabileceğiniz Ev denetleyicisi sınıfına eklenen iki yeni eylem içerir.

**Listeleme 3 – Denetleyiciler\HomeController.cs (Yöntem ekle)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

İlk Ekle() eylemi yalnızca bir görünümü döndürür. Görünüm, yeni bir film veritabanı kaydı eklemek için bir form içerir (Bkz. Şekil 8). Formu gönderdiğiniz zaman, ikinci Add() eylemi çağrılır.

İkinci Add() eyleminin AcceptVerbs özniteliği yle süslenmiş olduğuna dikkat edin. Bu eylem yalnızca bir HTTP POST işlemi gerçekleştirirken çağrılabilir. Başka bir deyişle, bu eylem yalnızca bir HTML formu gönderirken çağrılabilir.

İkinci Add() eylemi, ASP.NET MVC TryUpdateModel() yöntemi yardımıyla Entity Framework Movie sınıfının yeni bir örneğini oluşturur. TryUpdateModel() yöntemi, FormCollection'daki alanları Add() yöntemine aktarAn alanları alır ve bu HTML form alanlarının değerlerini Film sınıfına atar.

Varlık Çerçevesi'ni kullanırken, bir varlık sınıfının özelliklerini güncelleştirmek için TryUpdateModel veya UpdateModel yöntemlerini kullanırken özelliklerin bir "beyaz listesini" sağlamanız gerekir.

Ardından, Ekle() eylemi bazı basit form doğrulama gerçekleştirir. Eylem, hem Başlık hem de Yönetici özelliklerinin değerleri olduğunu doğrular. Bir doğrulama hatası varsa, ModelState'e bir doğrulama hatası iletisi eklenir.

Doğrulama hatası yoksa, Varlık Çerçevesi yardımıyla Filmler veritabanı tablosuna yeni bir film kaydı eklenir. Yeni kayıt, aşağıdaki iki kod satırıyla veritabanına eklenir:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

Kodun ilk satırı, Varlık Çerçevesi tarafından izlenen film kümesine yeni Film varlığını ekler. İkinci kod satırı, temel veritabanına kadar izlenen Filmler'de yapılan değişikliklerden ne olursa olsun kaydeder.

**Şekil 8 – Görünüm Ekle**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Veritabanı Kayıtlarını Varlık Çerçevesi ile Güncelleştirme

Yeni bir veritabanı kaydı eklemek için izlediğimiz yaklaşım olarak Varlık Çerçevesi ile bir veritabanı kaydını yeniden oluşturmak için hemen hemen aynı yaklaşımı uygulayabilirsiniz. Listeleme 4, Edit() adlı iki yeni denetleyici eylemi içerir. İlk Edit() eylemi, bir film kaydını düzenlemek için bir HTML formu döndürür. İkinci Edit() eylemi veritabanını güncelleştirmeye çalışır.

**Listeleme 4 – Denetleyiciler\HomeController.cs (Edit yöntemleri)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

İkinci Edit() eylemi, düzenlenen filmin kimliğiyle eşleşen veritabanından Film kaydını alarak başlar. Aşağıdaki LINQ to Ntities deyimi, belirli bir Id ile eşleşen ilk veritabanı kaydını kaplar:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

Daha sonra, TryUpdateModel() yöntemi, HTML form alanlarının değerlerini film varlığının özelliklerine atamak için kullanılır. Güncelleştirilen tam özellikleri belirtmek için beyaz bir liste sağlandığına dikkat edin.

Ardından, hem Film Başlığı hem de Yönetmen özelliklerinin değerleri olduğunu doğrulamak için bazı basit doğrulama gerçekleştirilir. Her iki özellikte de bir değer eksikse, ModelState'e bir doğrulama hatası iletisi eklenir ve ModelState.IsValid değeri yanlış döndürür.

Son olarak, doğrulama hatası yoksa, temel Filmler veritabanı tablosu SaveChanges() yöntemini arayarak değişikliklerle güncelleştirilir.

Veritabanı kayıtlarını düzenlerken, düzenlenen kaydın kimliğini veritabanı güncelleştirmesini gerçekleştiren denetleyici eylemine geçirmeniz gerekir. Aksi takdirde, denetleyici eylem altta yatan veritabanında güncelleştirmek için hangi kayıt bilemez. Listeleme 5'te yer alan Düzenle görünümü, düzenlenen veritabanı kaydının Kimliğini temsil eden gizli bir form alanı içerir.

**Listeleme 5 – Görünümler\Ana Sayfa\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Veritabanı Kayıtlarını Varlık Çerçevesi ile Silme

Bu öğreticide ele almamız gereken son veritabanı işlemi veritabanı kayıtlarını siler. Belirli bir veritabanı kaydını silmek için Listeleme 6'daki denetleyici eylemini kullanabilirsiniz.

**Listeleme 6 -- \Controllers\HomeController.cs (Eylemi sil)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Sil() eylemi önce eyleme geçen Id ile eşleşen Film varlığını alır. Daha sonra film, DeleteObject() yöntemini ve ardından SaveChanges() yöntemini arayarak veritabanından silinir. Son olarak, kullanıcı Dizin görünümüne geri yönlendirilir.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, mvc ve Microsoft Entity Framework ASP.NET yararlanarak veritabanı tabanlı web uygulamaları nasıl oluşturabileceğinizi göstermekti. Veritabanı kayıtlarını seçmenizi, eklemenizi, güncelleştirmenizi ve silmenizi sağlayan bir uygulamayı nasıl oluşturabileceğinizi öğrendiniz.

İlk olarak, Visual Studio içinden bir Varlık Veri Modeli oluşturmak için Varlık Veri Modeli Sihirbazı'nı nasıl kullanabileceğinizi tartıştık. Ardından, bir veritabanı tablosundan bir veritabanı kaydı kümesi almak için LINQ to Ntities'ı nasıl kullanacağınızı öğrenirsiniz. Son olarak, veritabanı kayıtlarını eklemek, güncelleştirmek ve silmek için Varlık Çerçevesi'ni kullandık.

> [!div class="step-by-step"]
> [Sonraki](creating-model-classes-with-linq-to-sql-cs.md)
