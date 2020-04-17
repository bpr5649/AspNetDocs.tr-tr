---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: Veritabanı Verileri Tablosunu Görüntüleme (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticide, veritabanı kayıtları kümesini görüntülemenin iki yöntemini gösteriyorum. Ben bir HTML ta veritabanı kayıtları kümesi biçimlendirme iki yöntem göstermek ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541903"
---
# <a name="displaying-a-table-of-database-data-vb"></a>Veritabanı Verilerinin Tablosunu Görüntüleme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> Bu öğreticide, veritabanı kayıtları kümesini görüntülemenin iki yöntemini gösteriyorum. Html tablosunda veritabanı kayıtları kümesini biçimlendirmek için iki yöntem gösteriyorum. İlk olarak, veritabanı kayıtlarını doğrudan bir görünüm içinde nasıl biçimlendirebileceğinizi gösteririm. Daha sonra, veritabanı kayıtlarını biçimlendirirken kısmi lerden nasıl yararlanabileceğinizi gösteririm.

Bu öğreticinin amacı, ASP.NET bir MVC uygulamasında veritabanı verilerinin HTML tablosunu nasıl görüntüleyebileceğinizi açıklamaktır. İlk olarak, bir kayıt kümesini otomatik olarak görüntüleyen bir görünüm oluşturmak için Visual Studio'da bulunan iskele araçlarını nasıl kullanacağınızı öğrenirsiniz. Ardından, veritabanı kayıtlarını biçimlendirirken kısmi bir şablon olarak nasıl kullanılacağını öğrenirsiniz.

## <a name="create-the-model-classes"></a>Model Sınıfları Oluşturma

Filmler veritabanı tablosundaki kayıt kümesini göstereceğiz. Filmler veritabanı tablosu aşağıdaki sütunları içerir:

<a id="0.4_table01"></a>

| **Sütun Adı** | **Veri Türü** | **Nulls'a İzin Ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar(200) | False |
| Yönetmen | NVarchar(50) | False |
| TarihYayınlandı | DateTime | False |

ASP.NET MVC uygulamamızda Filmler tablosunu temsil edebilmek için bir model sınıfı oluşturmamız gerekir. Bu öğreticide, model sınıflarımızı oluşturmak için Microsoft Entity Framework'u kullanırız.

> [!NOTE] 
> 
> Bu öğreticide, Microsoft Entity Framework'u kullanıyoruz. Ancak, LINQ'dan SQL'e, NHibernate'ye veya ADO.NET kadar ASP.NET bir MVC uygulamasından bir veritabanıyla etkileşim de dahil olmak üzere çeşitli teknolojiler kullanabileceğinizi anlamak önemlidir.

Varlık Veri Modeli Sihirbazı'nı başlatmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresindeki Modeller klasörüne sağ tıklayın ve menü seçeneğini seçin **Ekle, Yeni Öğe.**
2. **Veri** kategorisini seçin ve varlık veri modeli şablonu **ADO.NET** seçin.
3. Veri modelinize *MoviesDBModel.edmx* adını verin ve **Ekle** düğmesini tıklayın.

Ekle düğmesini tıklattıktan sonra Varlık Veri Modeli Sihirbazı görüntülenir (Bkz. Şekil 1). Sihirbazı tamamlamak için aşağıdaki adımları izleyin:

1. Model **İçeriği Seç** adımında **veritabanından Oluştur** seçeneğini belirleyin.
2. Veri **Bağlantınızı Seç** adımda, bağlantı ayarları için *MoviesDB.mdf* veri bağlantısını ve *MoviesDBEntities* adını kullanın. **İleri** düğmesini tıklatın.
3. Veritabanı **Nesneleri'ni seç** adımda, Tablolar düğümünü genişletin, Filmler tablosunu seçin. Ad alanı *modellerini* girin ve **Bitiş** düğmesini tıklatın.

[![SQL sınıflarına LINQ oluşturma](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**Şekil 01**: SQL sınıflarına LINQ oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](displaying-a-table-of-database-data-vb/_static/image2.png))

Varlık Veri Modeli Sihirbazı'nı tamamladıktan sonra Varlık Veri Modeli Tasarımcısı açılır. Tasarımcı Filmler varlığını göstermelidir (Bkz. Şekil 2).

[![Varlık Veri Modeli Tasarımcısı](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**Şekil 02**: Varlık Veri Modeli Tasarımcısı ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](displaying-a-table-of-database-data-vb/_static/image4.png))

Devam etmeden önce bir değişiklik yapmalıyız. Varlık Veri Sihirbazı, Filmler veritabanı tablosunu temsil eden *Filmler* adlı bir model sınıfı oluşturur. Belirli bir filmi temsil etmek için Filmler sınıfını kullanacağımız için, sınıfın adını *Film* yerine *Film* olarak değiştirmemiz gerekir (çoğul yerine tekil).

Tasarımcı yüzeyindeki sınıfın adını çift tıklatın ve sınıfın adını Filmler'den Filme değiştirin. Bu değişikliği yaptıktan sonra Film sınıfını oluşturmak için **Kaydet** düğmesini (disket simgesi) tıklatın.

## <a name="create-the-movies-controller"></a>Film Denetleyicisini Oluşturma

Artık veritabanı kayıtlarımızı temsil etmenin bir yolu olduğuna göre, film koleksiyonunu döndüren bir denetleyici oluşturabiliriz. Visual Studio Solution Explorer penceresinde, Denetleyiciler klasörüne sağ tıklayın ve **Ekle, Denetleyici** seçeneğini seçin (Bkz. Şekil 3).

[![Denetleyici Ekle Menüsü](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**Şekil 03**: Denetleyici Ekle Menüsü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](displaying-a-table-of-database-data-vb/_static/image6.png))

Denetleyici **Ekle** iletişim kutusu göründüğünde, denetleyici adı MovieController'ı girin (Bkz. Şekil 4). Yeni denetleyiciyi eklemek için **Ekle** düğmesini tıklatın.

[![Denetleyici Ekle iletişim kutusu](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**Şekil 04**: Denetleyici Ekle iletişim kutusu([Tam boyutlu görüntüyü görüntülemek için tıklayınız](displaying-a-table-of-database-data-vb/_static/image8.png))

Film denetleyicisi tarafından maruz kalan dizin eylemini veritabanı kayıtları kümesini döndürecek şekilde değiştirmemiz gerekir. Denetleyiciyi Listeleme 1'deki denetleyiciye benzeyerek değiştirin.

**Listeleme 1 – Denetleyiciler\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

Listeleme 1'de, MoviesDBntities sınıfı MoviesDB veritabanını temsil etmek için kullanılır. İfade *varlıkları. MovieSet.ToList()* Filmler veritabanı tablosundaki tüm filmlerin kümesini döndürür.

## <a name="create-the-view"></a>Görünümü Oluştur

Bir HTML tablosunda veritabanı kayıtları kümesini görüntülemenin en kolay yolu Visual Studio tarafından sağlanan iskeleden yararlanmaktır.

Menü seçeneğini seçerek uygulamanızı oluşturun **Çözüm Oluştur.** **Görünüm Ekle** iletişim kutusunu açmadan önce uygulamanızı oluşturmanız gerekir veya veri sınıflarınız iletişim kutusunda görünmez.

Index() eylemine sağ tıklayın ve **Görünüm Ekle** menü seçeneğini seçin (Bkz. Şekil 5).

[![Görünüm ekleme](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**Şekil 05**: Görünüm ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-vb/_static/image10.png))

Görünüm **Ekle** iletişim kutusunda, güçlü bir **şekilde yazılan görünüm oluşturma**etiketli onay kutusunu işaretleyin. **Görünüm veri sınıfı**olarak Film sınıfını seçin. **Görünüm içeriği** olarak *Liste'yi* seçin (bkz. Şekil 6). Bu seçenekleri seçmek, filmlerin listesini görüntüleyen güçlü bir şekilde yazılan bir görünüm oluşturur.

[![Görünüm Ekle iletişim kutusu](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**Şekil 06**: Görünüm Ekle iletişim kutusu([Tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-vb/_static/image12.png))

**Ekle** düğmesini tıklattıktan sonra, Listeleme 2'deki görünüm otomatik olarak oluşturulur. Bu görünüm, film koleksiyonu nda yinelemek ve bir filmin özelliklerini görüntülemek için gereken kodu içerir.

**Listeleme 2 – Görünümler\Film\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

Menü seçeneği **Hata Ayıklama, Baş Hata Ayıklama** (veya F5 tuşuna basarak) seçerek uygulamayı çalıştırabilirsiniz. Uygulamayı çalıştıran Internet Explorer başlattı. /Film URL'sine giderseniz, sayfayı Şekil 7'de görürsünüz.

[![Bir film tablosu](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**Şekil 07**: Bir film tablosu([Tam boyutlu görüntüyü görüntülemek için tıklayınız](displaying-a-table-of-database-data-vb/_static/image14.png))

Şekil 7'deki veritabanı kayıtlarının ızgarasının görünümüyle ilgili herhangi bir şey beğenmezseniz, dizin görünümünü değiştirebilirsiniz. Örneğin, Dizin görünümünü değiştirerek *DateReleased* üstbilgisini *Çıkış Tarihi* olarak değiştirebilirsiniz.

## <a name="create-a-template-with-a-partial"></a>Kısmi Şablon Oluşturma

Bir görünüm çok karmaşık hale geldiğinde, görünümü kısmi olarak bölmeye başlamak iyi bir fikirdir. Kısmi görünümlerin kullanılması, görünümlerinizin anlaşılmasını ve bakımını kolaylaştırır. Film veritabanı kayıtlarının her birini biçimlendirmek için şablon olarak kullanabileceğimiz bir kısmi oluştururuz.

Kısmi oluşturmak için aşağıdaki adımları izleyin:

1. Görünümler\Film klasörüne sağ tıklayın ve **Görünüm Ekle**seçeneğini seçin.
2. *Kısmi görünüm (.ascx)* olarak etiketlenmiş onay kutusunu işaretleyin.
3. Kısmi *MovieTemplate'i*adlandırın.
4. Etiketli onay kutusunu işaretleyin **Güçlü bir şekilde yazılan görünüm oluşturun.**
5. Görünüm veri *sınıfı*olarak Film'i seçin.
6. *Görünüm içeriği*olarak Boş'u seçin.
7. Kısmi yi projenize eklemek için **Ekle** düğmesini tıklatın.

Bu adımları tamamladıktan sonra MovieTemplate'u listeleme 3'e benzer şekilde kısmi olarak değiştirin.

**Listeleme 3 – Görünümler\Film\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

Listeleme 3'teki kısmi, tek bir kayıt satırı için şablon içerir.

Listeleme 4'teki değiştirilmiş Dizin görünümü, MovieTemplate'u kısmi olarak kullanır.

**Listeleme 4 – İzlenme\Film\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

Listeleme 4'teki görünüm, tüm filmlerde her şeyi yineleyen bir For Each döngüsü içerir. Her film için, MovieTemplate kısmi film biçimlendirmek için kullanılır. MovieTemplate, RenderPartial() yardımcı yöntemini arayarak işlenir.

Değiştirilen Dizin görünümü veritabanı kayıtlarının çok aynı HTML tablosunu işler. Ancak, görünüm büyük ölçüde basitleştirilmiştir.

RenderPartial() yöntemi, bir dize döndürmediği için diğer yardımcı yöntemlerin çoğundan farklıdır. Bu &lt;nedenle,&gt; &lt;% Html.RenderPartial() % yerine % = Html.RenderPartial() %&gt;kullanarak RenderPartial() yöntemini aramalısınız.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, bir HTML tablosunda veritabanı kayıtları kümesini nasıl görüntüleyebileceğinizi açıklamaktır. İlk olarak, Microsoft Entity Framework'den yararlanarak bir denetleyici eyleminden veritabanı kayıtları kümesini döndürmeyi öğrendiniz. Ardından, otomatik olarak bir öğe koleksiyonu görüntüleyen bir görünüm oluşturmak için Visual Studio iskelesini nasıl kullanacağınızı öğrendiniz. Son olarak, kısmi bir yararlanarak görünümü basitleştirmek için nasıl öğrendim. Her veritabanı kaydını biçimlendirebilmek için kısmi şablon olarak nasıl kullanılacağını öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](creating-model-classes-with-linq-to-sql-vb.md)
> [Sonraki](performing-simple-validation-vb.md)
