---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Veritabanı Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 2, NerdDinner uygulamamız için tüm akşam yemeği ve RSVP verilerini tutan veritabanını oluşturma adımlarını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541617"
---
# <a name="create-a-database"></a>Veritabanı Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 2 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 2, NerdDinner uygulamamız için tüm akşam yemeği ve RSVP verilerini tutan veritabanını oluşturma adımlarını gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner Adım 2: Veritabanı oluşturma

NerdDinner uygulamamız için tüm Akşam Yemeği ve RSVP verilerini depolamak için bir veritabanı kullanacağız.

Aşağıdaki adımlar, ücretsiz SQL Server Express sürümünü kullanarak veritabanıoluşturmayı gösterir [(Microsoft Web Platform Installer'ın](https://www.microsoft.com/web/downloads/platform.aspx)V2'sini kullanarak kolayca yükleyebilirsiniz). Yazacağınız tüm kodlar hem SQL Server Express hem de tam SQL Server ile çalışır.

### <a name="creating-a-new-sql-server-express-database"></a>Yeni bir SQL Server Express veritabanı oluşturma

Web projemize sağ tıklayarak başlayacağız ve ardından **Ekle-&gt;Yeni Öğe** menüsü komutunu seçeceğiz:

![](create-a-database/_static/image1.png)

Bu, Visual Studio'nun "Yeni Öğe Ekle" iletişim kutusunu gündeme getirecektir. "Veri" kategorisine göre filtre uygulayacağız ve "SQL Server Database" öğe şablonu seçeceğiz:

![](create-a-database/_static/image2.png)

"NerdDinner.mdf" oluşturmak istediğimiz SQL Server Express veritabanına isim vereceğiz ve tamam tuşuna basacağız. Visual Studio daha sonra bu dosyayı \App\_Data dizinine eklemek isteyip istemediğimizi soracaktır (ki bu, güvenlik Aç'larını hem okuyhem de yazabilen bir dizinidir):

![](create-a-database/_static/image3.png)

"Evet"i tıklatacağız ve yeni veritabanımız oluşturulacak ve Çözüm Gezgini'ne eklenecektir:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Veritabanımızda Tablo Oluşturma

Artık yeni bir boş veritabanımız var. Buna birkaç tablo ekleyelim.

Bunu yapmak için Visual Studio'daki "Server Explorer" sekmesine gideriz ve bu da veritabanlarını ve sunucuları yönetmemizi sağlar. Uygulamamızın \App\_Data klasöründe depolanan SQL Server Express veritabanları otomatik olarak Server Explorer içinde gösterilecek. İsteğe bağlı olarak "Server Explorer" penceresinin üst kısmındaki "Veritabanına Bağlan" simgesini kullanarak listeye ek SQL Server veritabanları (yerel ve uzak) ekleyebiliriz:

![](create-a-database/_static/image5.png)

Biz NerdDinner veritabanına iki tablo ekleyeceğiz - biri bizim Dinners saklamak için, ve diğer onlara RSVP kabulleri izlemek için. Veritabanımızdaki "Tablolar" klasörüne sağ tıklayarak ve "Yeni Tablo Ekle" menü komutunu seçerek yeni tablolar oluşturabiliriz:

![](create-a-database/_static/image6.png)

Bu bize tablonun şema yapılandırmak için izin veren bir tablo tasarımcısı açılacaktır. "Akşam Yemekleri" tablomuz için 10 veri sütunu ekleyeceğiz:

![](create-a-database/_static/image7.png)

"DinnerID" sütununun tablo için benzersiz bir birincil anahtar olmasını istiyoruz. Bunu "DinnerID" sütununa sağ tıklayarak ve "Birincil Anahtarı Ayarla" menü öğesini seçerek yapılandırabiliriz:

![](create-a-database/_static/image8.png)

DinnerID'ı birincil anahtar haline getirmenin yanı sıra, yeni veri satırları tabloya eklendikçe değeri otomatik olarak artılan bir "kimlik" sütunu olarak da yapılandırmak isteriz (yani eklenen ilk Akşam Yemeği satırı 1'lik bir DinnerID'ye sahip olacak, ikinci eklenen satırda 2'lik bir DinnerID olacak vb.)

Bunu "DinnerID" sütununa seçerek yapabilir izleyebilirsiniz ve sütundaki "(Kimlik)" özelliğini "Evet" olarak ayarlamak için "Sütun Özellikleri" düzenleyicisini kullanabiliriz. Standart kimlik varsayılanlarını kullanırız (her yeni Akşam Yemeği satırında 1'den başlar ve 1'den başlar):

![](create-a-database/_static/image9.png)

Daha sonra Ctrl-S yazarak veya **Dosya-Kaydet&gt;** menüsü komutunu kullanarak tablomuzu kaydedeceğiz. Bu, tabloya isim vermemizi ister. Adını "Akşam Yemekleri" koyacağız:

![](create-a-database/_static/image10.png)

Yeni Akşam Yemekleri tablomuz daha sonra sunucu gezgininde veritabanımızda gösterecektir.

Daha sonra yukarıdaki adımları tekraredeceğiz ve bir "RSVP" tablosu oluşturacağız. Bu tablo ile 3 sütun var. RsvpID sütununa birincil anahtar olarak kurulum yapacağız ve ayrıca onu bir kimlik sütunu haline getireceğiz:

![](create-a-database/_static/image11.png)

Onu kurtarAcağız ve ona "RSVP" adını vereceğiz.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Tablolar Arasında Yabancı Anahtar İlişkisi Kurma

Veritabanımızda iki tablo var. Son şema tasarım adımımız, bu iki tablo arasında "bir-çok" ilişki kurmak olacaktır – böylece her Akşam Yemeği satırına uygulanan sıfır veya daha fazla RSVP satırıyla ilişkilendirebiliriz. Bunu, RSVP tablosunun "DinnerID" sütununa "DinnerID" tablosundaki "DinnerID" sütununa yabancı anahtar ilişkisi sağlayacak şekilde yapılandırarak yapacağız.

Bunu yapmak için, sunucu gezgininde çift tıklayarak tablo tasarımcısı içindeki RSVP tablosunu açarız. Daha sonra içindeki "DinnerID" sütununa sağ tıklayıp "İlişkiler..." seçeneğini seçeceğiz. bağlam menüsü komutu:

![](create-a-database/_static/image12.png)

Bu, tablolar arasındaki ilişkileri kurmak için kullanabileceğimiz bir iletişim kutusunu getirir:

![](create-a-database/_static/image13.png)

İletişim kutusuna yeni bir ilişki eklemek için "Ekle" düğmesini tıklatırız. Bir ilişki eklendikten sonra, özellik ızgarası içindeki "Tablolar ve Sütun Belirtimi" ağaç görünümü düğümünün iletişim kutusunun sağında genişletilir ve sonra "..." seçeneğini tıklarız. düğmesinin sağındaki:

![](create-a-database/_static/image14.png)

"..." seçeneğini tıklattığınızda düğmesi, ilişkiye hangi tabloların ve sütunların dahil olduğunu belirtmemize ve ilişkiye isim vermemize olanak tanıyan başka bir iletişim kutusunu gündeme getirecektir.

Birincil Anahtar Tablosunu "Akşam Yemekleri" olarak değiştireceğiz ve birincil anahtar olarak Akşam Yemeği tablosundaki "DinnerID" sütununa seçeceğiz. RSVP tablomuz yabancı anahtar tablosu ve RSVP olacak. DinnerID sütunu yabancı anahtar olarak ilişkilendirilecektir:

![](create-a-database/_static/image15.png)

Şimdi RSVP tablosundaki her satır, Akşam Yemeği tablosundaki bir satırla ilişkilendirilecektir. SQL Server bizim için başvuru bütünlüğünü koruyacak tır ve geçerli bir Akşam Yemeği satırına işaret etmiyorsa yeni bir RSVP satırı eklememizi engeller. Ayrıca, hala buna atıfta bulunan RSVP satırları varsa, akşam yemeği satırLarını silmemizi de engeller.

### <a name="adding-data-to-our-tables"></a>Tablolarımıza Veri Ekleme

Akşam Yemekleri tablomuza bazı örnek verileri ekleyerek bitirelim. Sunucu Gezgini içinde sağ tıklayarak ve "Tablo Verilerini Göster" komutunu seçerek tabloya veri ekleyebiliriz:

![](create-a-database/_static/image16.png)

Uygulamayı uygulamaya başladığımızda daha sonra kullanabileceğimiz birkaç satır Akşam Yemeği verisi ekleyeceğiz:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Sonraki Adım

Veritabanımızı oluşturmayı bitirdik. Şimdi sorgulayıp güncellemek için kullanabileceğimiz model sınıfları oluşturalım.

> [!div class="step-by-step"]
> [Önceki](create-a-new-aspnet-mvc-project.md)
> [Sonraki](build-a-model-with-business-rule-validations.md)
