---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: 'Yineleme #1 – Uygulama Oluştur (C#) | Microsoft Dokümanlar'
author: rick-anderson
description: "İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve D..."
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: ecc3c1201c784e20c6b2601735bee3d4ce721f22
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542553"
---
# <a name="iteration-1--create-the-application-c"></a>1. Yineleme – Uygulamayı oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (VB)

Öğreticiler bu dizi, biz baştan sona tüm Bir İletişim Yönetimi uygulaması oluşturmak. İletişim Yöneticisi uygulaması, kişi listesi için kişi bilgilerini (adlar, telefon numaraları ve e-posta adresleri) depolamanızı sağlar.

Uygulamayı birden çok yineleme üzerine oluşturuyoruz. Her yineleme ile, yavaş yavaş uygulama geliştirmek. Bu çoklu yineleme yaklaşımının amacı, her değişikliğin nedenini anlamanızı sağlamaktır.

- Yineleme #1 - Uygulamayı oluşturun. İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

- Yineleme #2 - Uygulama güzel görünmesini sağlamak. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

- Yineleme #3 - Form doğrulama ekleyin. Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

- Yineleme #4 - Uygulamayı gevşek bir şekilde biraraya getirin. Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

- Yineleme #5 - Birim testleri oluşturun. Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

- Yineleme #6 - Test odaklı geliştirme yi kullanın. Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

- Yineleme #7 - Ajax işlevselliği ekleyin. Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="this-iteration"></a>Bu Yineleme

Bu ilk yinelemede, temel uygulamayı oluştururuz. Amaç, Kişi Yöneticisi'ni mümkün olan en hızlı ve en basit şekilde oluşturmaktır. Daha sonraki yinelemelerde, uygulamanın tasarımını geliştiririz.

Contact Manager uygulaması temel bir veritabanı tabanlı uygulamadır. Uygulamayı yeni kişiler oluşturmak, varolan kişileri düzenlemek ve kişileri silmek için kullanabilirsiniz.

Bu yinelemede, aşağıdaki adımları tamamlıyoruz:

1. ASP.NET MVC uygulaması
2. Kişilerimizi depolamak için bir veritabanı oluşturma
3. Microsoft Entity Framework ile veritabanımız için bir model sınıfı oluşturma
4. Veritabanındaki tüm kişileri listelamamızı sağlayan bir denetleyici eylemi ve görünümü oluşturma
5. Denetleyici eylemleri ve veritabanında yeni bir kişi oluşturmamızı sağlayan bir görünüm oluşturma
6. Denetleyici eylemleri ve veritabanındaki varolan bir kişi yi yeniden oluşturmamızı sağlayan bir görünüm oluşturma
7. Denetleyici eylemleri ve veritabanındaki varolan bir kişi silmek için bize olanak sağlayan bir görünüm oluşturma

## <a name="software-prerequisites"></a>Yazılım Ön koşulları

MVC uygulamaları ASP.NET, ya Visual Studio 2008 veya Visual Web Developer 2008 bilgisayarınızda yüklü olmalıdır (Visual Web Developer Visual Studio tüm gelişmiş özellikleri içermez Visual Studio ücretsiz bir sürümüdür). Visual Studio 2008 veya Visual Web Developer'ın deneme sürümünü aşağıdaki adresten indirebilirsiniz:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer ile ASP.NET MVC uygulamaları için Visual Web Developer Service Pack 1 yüklü olmalıdır. Hizmet Paketi 1 olmadan Web Uygulama Projeleri oluşturamazsınız.

ASP.NET MVC çerçevesi. mvc ASP.NET çerçevesini aşağıdaki adresten indirebilirsiniz:

[https://www.asp.net/mvc](../../../index.md)

Bu öğreticide, bir veritabanına erişmek için Microsoft Entity Framework'i kullanırız. Varlık Çerçevesi .NET Framework 3.5 Hizmet Paketi 1 ile birlikte verilir. Bu hizmet paketini aşağıdaki konumdan indirebilirsiniz:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=tr](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Bu indirmelerin her birini tek tek gerçekleştirmeye alternatif olarak, Web Platformu Yükleyici'den (Web PI) yararlanabilirsiniz. Web PI'yi aşağıdaki adresten indirebilirsiniz:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC Projesi

ASP.NET MVC Web Uygulama Projesi. Visual Studio'yu başlatın ve menü seçeneği **Dosya, Yeni Proje'yi**seçin. **Yeni Proje** iletişim kutusu görüntülenir (Bkz. Şekil 1). **Web** proje türünü ve **ASP.NET MVC Web Uygulaması** şablonu seçin. Yeni projenize *ContactManager* adını ve Tamam düğmesini tıklayın.

**Yeni Proje** iletişim kutusunun sağ üst kısmındaki açılır listeden .NET Framework 3.5 seçildiğinden emin olun. Aksi takdirde, ASP.NET MVC Web Uygulaması şablonu görünmez.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**Şekil 01**: Yeni Proje iletişim kutusu([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image2.png))

MVC uygulamasından ASP.NET Birim **Test Projesi Oluştur** iletişim kutusu görüntülenir. Bu iletişim kutusunu, ASP.NET MVC uygulamanızı oluştururken çözümünüzü oluşturmak ve bir birim test projesi eklemek istediğinizi belirtmek için kullanabilirsiniz. Bu yinelemede birim testleri oluşturmayacak olsak da, daha sonraki bir yinelemede birim testleri eklemeyi planladığımız için Evet seçeneğini **seçmelisiniz, birim test projesi oluşturmalısınız.** Yeni bir ASP.NET MVC projesi oluşturduğunuzda test projesi eklemek, ASP.NET MVC projesi oluşturulduktan sonra bir Test projesi eklemekten çok daha kolaydır.

> [!NOTE] 
> 
> Visual Web Developer Test projelerini desteklemediği için, Visual Web Developer'ı kullanırken Birim Testi Projesi Oluştur iletişim kutusunu alamazsınız.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**Şekil 02**: Birim Test Projesi Oluştur iletişim kutusu ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image4.png))

ASP.NET MVC uygulaması Visual Studio Solution Explorer penceresinde görünür (Bkz. Şekil 3). Çözüm Gezgini penceresini görmüyorsanız, bu pencereyi menü seçeneği **View, Solution Explorer'ı**seçerek açabilirsiniz. Çözümün iki proje içerdiğine dikkat edin: ASP.NET MVC projesi ve Test projesi. ASP.NET MVC projesinin adı ContactManager ve Test projesinin adı ContactManager.Tests'tir.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**Şekil 03**: Çözüm Gezgini penceresi ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>Proje Örnek Dosyaları Silme

mvc proje şablonu ASP.NET denetleyicileri ve görünümleri için örnek dosyaları içerir. Yeni bir ASP.NET MVC uygulaması oluşturmadan önce, bu dosyaları silmeniz gerekir. Çözüm Gezgini penceresindeki dosya ve klasörleri bir dosya veya klasöre sağ tıklayarak ve menü **seçeneğini**seçerek sil seçeneğini silile ile silebilirsiniz.

ASP.NET MVC projesinden aşağıdaki dosyaları silmeniz gerekir:

- \Controllers\HomeController.cs

- \Görünümler\Ana Sayfa\About.aspx

- \Görünümler\Ana Sayfa\Index.aspx

Ayrıca, Test projesinden aşağıdaki dosyayı silmeniz gerekir:

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>Veritabanı oluşturma

Contact Manager uygulaması veritabanı tarafından yönlendirilen bir web uygulamasıdır. İletişim bilgilerini depolamak için bir veritabanı kullanıyoruz.

Microsoft SQL Server, Oracle, MySQL ve IBM DB2 veritabanları da dahil olmak üzere herhangi bir modern veritabanı ile ASP.NET MVC çerçevesi. Bu öğreticide, bir Microsoft SQL Server veritabanı kullanıyoruz. Visual Studio'yu yüklediğinizde, Microsoft SQL Server veritabanının ücretsiz bir sürümü olan Microsoft SQL Server Express'i yükleme seçeneği yle birlikte verilir.

Çözüm Gezgini penceresindeki Uygulama\_Verileri klasörüne sağ tıklayarak ve **Ekle, Yeni Öğe**seçeneğini seçerek yeni bir veritabanı oluşturun. Yeni **Öğe Ekle** iletişim **kutusunda, Veri** kategorisi ve **SQL Server Veritabanı** şablonu (Bkz. Şekil 4) seçeneğini belirleyin. Yeni veritabanı ContactManagerDB.mdf'yi adlandırın ve Tamam düğmesini tıklatın.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**Şekil 04**: Yeni bir Microsoft SQL Server Express veritabanı oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image8.png))

Yeni veritabanını oluşturduktan sonra, veritabanı Çözüm\_Gezgini penceresindeki Uygulama Verileri klasöründe görünür. Server Explorer penceresini açmak ve veritabanına bağlanmak için ContactManager.mdf dosyasına çift tıklayın.

> [!NOTE] 
> 
> Sunucu Gezgini penceresi, Microsoft Visual Web Developer durumunda Veritabanı Gezgini penceresi olarak adlandırılır.

Veritabanı tabloları, görünümler, tetikleyiciler ve depolanmış yordamlar gibi yeni veritabanı nesneleri oluşturmak için Sunucu Gezgini penceresini kullanabilirsiniz. Tablolar klasörüne sağ tıklayın ve **menü**seçeneğini yeni tablo ekle seçeneğini seçin. Veritabanı Tablo Tasarımcısı görüntülenir (bkz. Şekil 5).

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**Şekil 05**: Veritabanı Tablo Tasarımcısı ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image10.png))

Aşağıdaki sütunları içeren bir tablo oluşturmamız gerekir:

<a id="0.1_table01"></a>

| **Sütun Adı** | **Veri Türü** | **Nulls'a İzin Ver** |
| --- | --- | --- |
| Kimlik | int | yanlış |
| FirstName | nvarchar(50) | yanlış |
| LastName | nvarchar(50) | yanlış |
| Telefon | nvarchar(50) | yanlış |
| Email | nvarchar(255) | yanlış |

İlk sütun, Id sütunu, özeldir. Kimlik sütununu Kimlik sütunu ve Birincil Anahtar sütunu olarak işaretlemeniz gerekir. Sütun Özelliklerini genişleterek (Şekil 6'nın altına bakarak) ve Kimlik Belirtimi özelliğine aşağı kaydırarak bir sütunun Kimlik sütunu olduğunu belirtirsiniz. **(Kimlik)** özelliğini **Evet**değerine ayarlayın.

Sütunu seçerek ve bir tuşu n simgesiyle düğmeyi tıklatarak bir sütunu Birincil Anahtar sütunu olarak işaretlersiniz. Bir sütun Birincil Anahtar sütunu olarak işaretlendikten sonra, sütunun yanında bir anahtar simgesi görüntülenir (Bkz. Şekil 6).

Tabloyu oluşturmayı bitirdikten sonra, yeni tabloyu kaydetmek için Kaydet düğmesini (disket simgesi olan düğme) tıklatın. Yeni tablonuza *Kişiler*adını verin.

Kişiler veritabanı tablosunu oluşturmayı bitirdikten sonra tabloya bazı kayıtlar eklemeniz gerekir. Sunucu Gezgini penceresindeki Kişiler tablosuna sağ tıklayın ve **Tablo Verilerini Göster**menüsü seçeneğini seçin. Kılavuza görünen bir veya daha fazla kişi girin.

## <a name="creating-the-data-model"></a>Veri Modelini Oluşturma

mvc uygulaması ASP.NET Modeller, Görünümler ve Denetleyicilerden oluşur. Önceki bölümde oluşturduğumuz Kişiler tablosunu temsil eden bir Model sınıfı oluşturarak başlıyoruz.

Bu öğreticide, veritabanından otomatik olarak bir model sınıfı oluşturmak için Microsoft Entity Framework'u kullanırız.

> [!NOTE] 
> 
> ASP.NET MVC çerçevesi hiçbir şekilde Microsoft Entity Framework'e bağlı değildir. NHibernate, LINQ to SQL veya ADO.NET gibi alternatif veritabanı erişim teknolojileri ile ASP.NET MVC kullanabilirsiniz.

Veri modeli sınıflarını oluşturmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresindeki Modeller klasörüne sağ tıklayın ve **Yeni Öğe Ekle'yi**seçin. **Yeni Öğe Ekle** iletişim kutusu görüntülenir (bkz. Şekil 6).
2. **Veri** kategorisini ve **ADO.NET Varlık Veri Modeli** şablonunu seçin. Veri modelinizi *ContactManagerModel.edmx* olarak adlandırın ve **Ekle** düğmesini tıklatın. Varlık Veri Modeli sihirbazı görüntülenir (bkz. Şekil 7).
3. Model **İçeriği Seç** adımında **veritabanından Oluştur'u** seçin (Bkz. Şekil 7).
4. Veri **Bağlantınızı Seç** adımında, ContactManagerDB.mdf veritabanını seçin ve Entity Connection Settings için *ContactManagerDBEntities* adını girin (bkz. Şekil 8).
5. Veritabanı **Nesnelerinizi Seç** adımında, Tablolar etiketli onay kutusunu seçin (Bkz. Şekil 9). Veri modeli veritabanınızda bulunan tüm tabloları içerir (yalnızca bir tane var, Kişiler tablosu). Ad alanı *modellerini*girin. Sihirbazı tamamlamak için Bitir düğmesini tıklatın.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**Şekil 06**: Yeni Öğe Ekle iletişim kutusu ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image12.png))

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**Şekil 07**: Model İçeriklerini Seçin ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image14.png))

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**Şekil 08**: Veri Bağlantınızı Seçin ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image16.png))

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**Şekil 09**: Veritabanı Nesnelerinizi Seçin ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image18.png))

Varlık Veri Modeli Sihirbazı'nı tamamladıktan sonra Varlık Veri Modeli Tasarımcısı görüntülenir. Tasarımcı, modellenen her tabloya karşılık gelen bir sınıf görüntüler. Kişiler adlı bir sınıf görmeniz gerekir.

Varlık Veri Modeli sihirbazı veritabanı tablo adlarını temel alan sınıf adları oluşturur. Sihirbaz tarafından oluşturulan sınıfın adını hemen hemen her zaman değiştirmeniz gerekir. Tasarımcıdaki Kişiler sınıfına sağ tıklayın ve menü seçeneğini yeniden **adlandır'ı**seçin. Sınıfın adını Kişiler (çoğul) ile Kişi (tekil) olarak değiştirin. Sınıf adını değiştirdikten sonra, sınıf Şekil 10 gibi görünmelidir.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**Şekil 10**: İletişim sınıfı ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image20.png))

Bu noktada, veritabanı modelimizi oluşturduk. İletişim sınıfını veritabanımızda belirli bir kişi kaydını temsil etmek için kullanabiliriz.

## <a name="creating-the-home-controller"></a>Ev Denetleyicisini Oluşturma

Bir sonraki adım Ev denetleyicimizi oluşturmaktır. Ev denetleyicisi, ASP.NET bir MVC uygulamasında çağrılan varsayılan denetleyicidir.

Çözüm Gezgini penceresindeki Denetleyiciler klasörüne sağ tıklayarak ve **Ekle, Denetleyici** seçeneğini seçerek Ev denetleyicisi sınıfını oluşturun (Bkz. Şekil 11). **Oluştur, Güncelleştir ve Ayrıntılar senaryoları için eylem yöntemleri ekle**etiketli onay kutusuna dikkat edin. **Ekle** düğmesini tıklatmadan önce bu onay kutusunun işaretli olduğundan emin olun.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**Şekil 11**: Ana Ekran denetleyicisinin eklenmesi ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image22.png))

Giriş denetleyicisini oluşturduğunuzda, Liste 1'deki sınıfı alırsınız.

**Listeleme 1 - Denetleyiciler\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>Kişileri Listeleme

Kişiler veritabanı tablosundaki kayıtları görüntülemek için bir Dizin() eylemi ve Dizin görünümü oluşturmamız gerekir.

Ev denetleyicisi zaten bir Dizin() eylemi içerir. Bu yöntemi Listeleme 2'ye benzeyecek şekilde değiştirmemiz gerekir.

**Listeleme 2 - Denetleyiciler\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

Listeleme 2'deki Ev denetleyici sınıfının \_varlıklar adlı özel bir alan içerdiğine dikkat edin. Varlıklar \_alanı veri modelinden varlıkları temsil eder. Veritabanıyla \_iletişim kurmak için varlıklar alanını kullanırız.

Index() yöntemi, Kişiler veritabanı tablosundaki tüm kişileri temsil eden bir görünüm döndürür. İfade \_varlıkları. ContactSet.ToList() genel bir liste olarak kişilerin listesini döndürür.

Dizin denetleyicisini oluşturduğumuza göre, bir sonraki dizin görünümünü oluşturmamız gerekir. Dizin görünümünü oluşturmadan önce, çözüm **oluştur, ekle**seçeneği ekle seçeneğini seçerek uygulamanızı derleyin. **Görünüm Ekle** iletişim kutusunda görüntülenecek model sınıfları listesi için bir görünüm eklemeden önce her zaman projenizi derlemeniz gerekir.

Index() yöntemini sağ tıklatarak ve **Görünüm Ekle** seçeneğini seçerek Dizin görünümünü oluşturursunuz (Bkz. Şekil 12). Bu menü seçeneğini seçmek, **Görünüm Ekle** iletişim kutusunu açar (Bkz. Şekil 13).

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**Şekil 12**: Dizin görünümünü ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image24.png))

Görünüm **Ekle** iletişim kutusunda, güçlü bir **şekilde yazılan görünüm oluşturma**etiketli onay kutusunu işaretleyin. Veri sınıfı ContactManager.Models.Contact ve View content List'i seçin. Bu seçenekleri seçmek, Kişi kayıtlarının listesini görüntüleyen bir görünüm oluşturur.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**Şekil 13**: Görünüm Ekle iletişim kutusu ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image26.png))

**Ekle** düğmesini tıklattığınızda, Listeleme 3'teki Dizin görünümü oluşturulur. Dosyanın &lt;üst kısmında&gt; görünen %@ Sayfa % yönergesi'ne dikkat edin. Dizin&lt;görünümü ViewPage Ayrılmaz&lt;ContactManager.Models.Contact&gt; &gt; sınıfından devralır. Başka bir deyişle, görünümdeki Model sınıfı İlgili kişilerin listesini temsil eder.

Dizin görünümünün gövdesi, Model sınıfı tarafından temsil edilen kişilerin her biri aracılığıyla yineleyen bir foreach döngüsü içerir. İlgili Kişi sınıfının her özelliğinin değeri bir HTML tablosunda görüntülenir.

**Listeleme 3 - Görünümler\Ana Sayfa\Index.aspx (değiştirilmemiş)**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

Dizin görünümünde bir değişiklik yapmamız gerekiyor. Ayrıntılar görünümü oluşturmadığımız için Ayrıntılar bağlantısını kaldırabiliriz. Dizin görünümünden aşağıdaki kodu bulun ve kaldırın:

{ id=öğe. Id })%&gt;

Dizin görünümünü değiştirdikten sonra, İletişim Yöneticisi uygulamasını çalıştırabilirsiniz. Menü seçeneğini seçin Hata Ayıklama, Baş Hata Ayıklama veya sadece F5 tuşuna basın. Uygulamayı ilk çalıştırdığınızda, iletişim kutusunu Şekil 14'te alırsınız. **Hata ayıklamayı etkinleştirmek için Web.config dosyasını değiştir** seçeneğini seçin ve Tamam düğmesini tıklatın.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**Şekil 14**: Hata ayıklamayı etkinleştirme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image28.png))

Dizin görünümü varsayılan olarak döndürülür. Bu görünüm, Kişiler veritabanı tablosundaki tüm verileri listeler (bkz. Şekil 15).

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**Şekil 15**: Dizin görünümü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image30.png))

Dizin görünümünün görünümün alt kısmında Yeni Oluştur etiketli bir bağlantı içerdiğine dikkat edin. Sonraki bölümde, yeni kişiler oluşturmayı öğrenirsiniz.

## <a name="creating-new-contacts"></a>Yeni Kişiler Oluşturma

Kullanıcıların yeni kişiler oluşturmasına olanak sağlamak için, Ana Sayfa denetleyicisine iki Oluşturma eylemi eklememiz gerekir. Yeni bir kişi oluşturmak için HTML formunu döndüren bir Create() eylemi oluşturmamız gerekir. Yeni ilgili kişi gerçek veritabanı eklemek gerçekleştiren ikinci bir Create() eylem oluşturmanız gerekir.

Ana Sayfa denetleyicisine eklememiz gereken yeni Create() yöntemleri Listeleme 4'te bulunur.

**Listeleme 4 - Denetleyiciler\HomeController.cs (Oluşturma yöntemleri ile)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

İkinci Create() yöntemi yalnızca bir HTTP POST tarafından çağrılabilirken, ilk Create() yöntemi BIR HTTP GET ile çağrılabilir. Başka bir deyişle, ikinci Create() yöntemi yalnızca bir HTML formu gönderirken çağrılabilir. İlk Oluşturma() yöntemi, yeni bir kişi oluşturmak için HTML formunu içeren bir görünüm döndürür. İkinci Create() yöntemi çok daha ilginçtir: veritabanına yeni kişi ekler.

İkinci Create() yönteminin İlgili Kişi sınıfının bir örneğini kabul etmek üzere değiştirildiğini unutmayın. HTML formundan gönderilen form değerleri, mvc ASP.NET tarafından otomatik olarak bu İletişim sınıfına bağlanır. HTML Oluştur formundaki her form alanı, İlgili Kişi parametresinin bir özelliğine atanır.

İlgili Kişi parametresinin [Bind] özniteliğiyle dekore edildiğine dikkat edin. [Bind] özniteliği, İlgili Kişi Kimliği özelliğini bağlamayı hariç tutmak için kullanılır. Kimlik özelliği bir Kimlik özelliğini temsil ettiği için, Kimlik özelliğini ayarlamak istemiyoruz.

Create() yönteminin gövdesinde, Varlık Çerçevesi yeni Kişi'yi veritabanına eklemek için kullanılır. Yeni İlgili Kişi varolan Kişiler kümesine eklenir ve SaveChanges() yöntemi, bu değişiklikleri temel veritabanına geri itmek için çağrılır.

İki Create() yönteminden birini sağ tıklatarak ve **Görünüm Ekle** seçeneğini seçerek yeni Kişiler oluşturmak için bir HTML formu oluşturabilirsiniz (Bkz. Şekil 16).

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**Şekil 16**: Oluştur görünümü ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image32.png))

Görünüm **Ekle** iletişim **kutusunda, ContactManager.Models.Contact** sınıfını ve görüntüleme içeriği için **Oluştur** seçeneğini seçin (Bkz. Şekil 17). **Ekle** düğmesini tıklattığınızda, oluştur görünümü otomatik olarak oluşturulur.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**Şekil 17**: Bir sayfanın patladığı nagöre ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image34.png))

Oluştur görünümü, İlgili Kişi sınıfının her özellikleri için form alanları içerir. Create görünümü için kod Listeleme 5'e dahildir.

**Listeleme 5 - Görünümler\Ana Sayfa\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Oluştur() yöntemlerini değiştirip Create görünümünü ekledikten sonra, Contact Manger uygulamasını çalıştırabilir ve yeni kişiler oluşturabilirsiniz. Oluştur görünümüne gitmek için Dizin görünümünde görünen **Yeni Oluştur** bağlantısını tıklatın. Şekil 18'deki görünümü görmelisiniz.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**Şekil 18**: Görünüm Oluştur ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image36.png))

## <a name="editing-contacts"></a>Kişileri Düzenleme

Kişi kaydını düzenlemek için işlevsellik eklemek, yeni kişi kayıtları oluşturmak için işlevselliği eklemeye çok benzer. İlk olarak, Ev denetleyici sınıfına iki yeni Edit yöntemi eklememiz gerekir. Bu yeni Edit() yöntemleri Listeleme 6'da yer almaktadır.

**Listeleme 6 - Denetleyiciler\HomeController.cs (Edit yöntemleri ile)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

İlk Edit() yöntemi bir HTTP GET işlemi tarafından çağrılır. Düzenlenen kişi kaydının Kimliğini temsil eden bu yönteme Bir Kimlik parametresi geçirilir. Varlık Çerçevesi, Kimlikle eşleşen bir ilgilikişi almak için kullanılır. Kaydı düzenlemek için HTML formu içeren bir görünüm döndürülür.

İkinci Edit() yöntemi veritabanına gerçek güncelleştirmegerçekleştirir. Bu yöntem, Birleşme sınırının bir çişini parametre olarak kabul eder. ASP.NET MVC çerçevesi form alanlarını Edit formundan bu sınıfa otomatik olarak bağlar. Bir İlgili Kişi'yi düzenlerken [Bind] özniteliğini eklemediğinize dikkat edin (Id özelliğinin değerine ihtiyacımız var).

Varlık Çerçevesi, değiştirilen Kişi'yi veritabanına kaydetmek için kullanılır. Özgün İlgili Kişi önce veritabanından alınmalıdır. Ardından, Entity Framework ApplyPropertyChanges() yöntemi, Kişi'deki değişiklikleri kaydetmek için çağrılır. Son olarak, Varlık Framework SaveChanges() yöntemi, temel veritabanındaki değişiklikleri sürdürmek için çağrılır.

Düzenleme() yöntemini sağ tıklatarak ve Menü Ekle seçeneğini seçerek Düzenleme biçimini içeren görünümü oluşturabilirsiniz. Görünüm Ekle iletişim **kutusunda, ContactManager.Models.Contact** sınıfını ve görünüm içeriğini **edin** (Bkz. Şekil 19'a bakınız).

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**Şekil 19**: Edit Görünümü Ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image38.png))

Ekle düğmesini tıklattığınızda, yeni bir Edit görünümü otomatik olarak oluşturulur. Oluşturulan HTML formu, İlgili Kişi sınıfının her özelliklerine karşılık gelen alanları içerir (bkz.

**Listeleme 7 - Görünümler\Ana Sayfa\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Kişileri Silme

Kişileri silmek istiyorsanız, Ana Sayfa denetleyici sınıfına iki Silme eylemi eklemeniz gerekir. İlk Sil() eylemi bir silme onay formu görüntüler. İkinci Sil() eylemi gerçek silme yi gerçekleştirir.

> [!NOTE] 
> 
> Daha sonra, Yineleme #7, bir adım Ajax silme destekler şekilde İletişim Yöneticisi değiştirin.

İki yeni Sil() yöntemi Listeleme 8'de yer almaktadır.

**Listeleme 8 - Denetleyiciler\HomeController.cs (Silme yöntemleri)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

İlk Silme() yöntemi, kişi kaydını veritabanından silmek için bir onay formu döndürür (Bkz. Şekil20). İkinci Delete() yöntemi veritabanına karşı gerçek silme işlemini gerçekleştirir. Özgün kişi veritabanından alındıktan sonra, Veritabanı silme gerçekleştirmek için Entity Framework DeleteObject() ve SaveChanges() yöntemleri çağrılır.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**Şekil 20**: Silme onay görünümü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image40.png))

Kişi kayıtlarını silen bir bağlantı içerecek şekilde Dizin görünümünü değiştirmemiz gerekir (Bkz. Şekil 21). Edit bağlantısını içeren aynı tablo hücresine aşağıdaki kodu eklemeniz gerekir:

Html.ActionLink( { id=item. Id }) %&gt;

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**Şekil 21**: Edit bağlantısı ile dizin görünümü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image42.png))

Ardından, silme onay görünümünü oluşturmamız gerekir. Ana Sayfa denetleyicisi sınıfında Sil() yöntemine sağ tıklayın ve Görünüm Ekle menü seçeneğini seçin. Görünüm Ekle iletişim kutusu görüntülenir (bkz. Şekil 22).

Görünüm Ekle iletişim kutusu, Liste, Oluştur ve Düzenle görünümlerinin aksine, Sil görünümü oluşturmak için bir seçenek içermez. Bunun **yerine, ContactManager.Models.Contact** veri sınıfını ve **Boş** görünüm içeriğini seçin. Boş görünüm içeriği seçeneğini seçmek, görünümü kendimiz oluşturmamızı gerektirir.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**Şekil 22**: Silme onay görünümünü ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image44.png))

Sil görünümünün içeriği Listeleme 9'da bulunur. Bu görünüm, belirli bir ilgili kişi silmesi gerekip gerekmediğini doğrulayan bir form içerir (Bkz. Şekil 21).

**Listeleme 9 - Görünümler\Ana Sayfa\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Varsayılan Denetleyicinin Adını Değiştirme

Kişilerle çalışmak için denetleyici sınıfımızın adının HomeController sınıfı olarak adlandırılması sizi rahatsız edebilir. Denetleyicinin ContactController olarak adlandırılması gerekmez mi?

Bu sorunu gidermek için yeterince kolaydır. İlk olarak, Ev denetleyicisinin adını yeniden düzenlememiz gerekiyor. Visual Studio Code Editor'da HomeController sınıfını açın, sınıfın adını sağ tıklatın ve menü seçeneğini seçin **Refactor, Rename**. Bu menü seçeneğini seçmek, Yeniden Adlandır iletişim kutusunu açar.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**Şekil 23**: Denetleyici adını yeniden düzenleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image46.png))

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**Şekil 24**: Yeniden Adlandırma iletişim kutusunu kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image48.png))

Denetleyici sınıfınızı yeniden adsanız, Visual Studio Görünümler klasöründeki klasörün adını da günceller. Visual Studio \Views\Home klasörünü \Görünümler\Kişi klasörüne yeniden adlendirecek.

Bu değişikliği yaptıktan sonra, uygulamanızda artık bir Ev denetleyicisi olmayacak. Uygulamanızı çalıştırdığınızda, Şekil 25'teki hata sayfasını alırsınız.

[![Yeni Proje iletişim kutusu](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**Şekil 25**: Varsayılan denetleyici yok ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-1-create-the-application-cs/_static/image50.png))

Ana Sayfa denetleyicisi yerine İletişim denetleyicisini kullanmak için Global.asax dosyasındaki varsayılan rotayı güncelleştirmemiz gerekir. Global.asax dosyasını açın ve varsayılan rota tarafından kullanılan varsayılan denetleyiciyi değiştirin (bkz.

**İlan 10 - Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

Bu değişiklikleri yaptıktan sonra, İlgili Kişi Yöneticisi doğru çalışacaktır. Şimdi, varsayılan denetleyici olarak Contact denetleyicisi sınıfını kullanır.

## <a name="summary"></a>Özet

Bu ilk yinelemede, mümkün olan en hızlı şekilde temel bir Contact Manager uygulaması oluşturduk. Denetleyicilerimiz ve görünümlerimiz için ilk kodu otomatik olarak oluşturmak için Visual Studio'dan yararlandık. Veritabanı modeli sınıflarımızı otomatik olarak oluşturmak için Varlık Çerçevesi'nden de yararlandık.

Şu anda, Kişi Yöneticisi uygulamasıyla kişi kayıtlarını listeleyebilir, oluşturabilir, düzenleyebilir ve silebiliriz. Başka bir deyişle, veritabanı tabanlı bir web uygulaması tarafından gerekli tüm temel veritabanı işlemleri gerçekleştirebilirsiniz.

Ne yazık ki, uygulamamız bazı sorunlar vardır. İlk ve ben bu itiraf tereddüt, İletişim Yöneticisi uygulaması en cazip uygulama değildir. Biraz tasarım çalışması gerekiyor. Bir sonraki yinelemede, uygulamanın görünümünü iyileştirmek için varsayılan görünüm ana sayfasını ve basamaklı stil sayfasını nasıl değiştirebileceğimize bakacağız.

İkinci olarak, herhangi bir form doğrulama uygulamadık. Örneğin, form alanlarının herhangi biri için değerler girmeden kişi oluştur formunu göndermenizi engelleyecek hiçbir şey yoktur. Ayrıca, geçersiz telefon numaraları ve e-posta adresleri girebilirsiniz. #3 yinelemede form doğrulama sorununu çözmeye başlıyoruz.

Son olarak, ve en önemlisi, İletişim Yöneticisi uygulamasının geçerli yinelemekolayca değiştirilemez veya sürdürülemez. Örneğin, veritabanı erişim mantığı denetleyici eylemleri içine doğru pişmiş. Bu, denetleyicilerimizi değiştirmeden veri erişim kodumuzu değiştiremeyeceğimiz anlamına gelir. Daha sonraki yinelemelerde, İletişim Yöneticisi'ni değişime karşı daha esnek hale getirmek için uygulayabileceğimiz yazılım tasarım modellerini inceleriz.

> [!div class="step-by-step"]
> [Sonraki](iteration-2-make-the-application-look-nice-cs.md)
