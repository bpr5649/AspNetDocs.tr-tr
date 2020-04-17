---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ ile SQL (C#) ile Model Sınıfları Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı, ASP.NET bir MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu öğreticide, nasıl model c oluşturmak için öğrenmek ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: eac6fec3a4cfd833b810378d946874a246d9a2c3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542735"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL ile Model Sınıfları Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> Bu öğreticinin amacı, ASP.NET bir MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu eğitimde, Microsoft LINQ'dan SQL'e yararlanarak model sınıfları oluşturmayı ve veritabanı erişimi gerçekleştirmeyi öğrenirsiniz.

Bu öğreticinin amacı, ASP.NET bir MVC uygulaması için model sınıfları oluşturma yöntemini açıklamaktır. Bu eğitimde, Microsoft LINQ'dan SQL'e yararlanarak model sınıfları oluşturmayı ve veritabanı erişimi gerçekleştirmeyi öğreniyorsunuz.

Bu öğreticide, temel bir Film veritabanı uygulaması oluşturuyoruz. Film veritabanı uygulamasını mümkün olan en hızlı ve en kolay şekilde oluşturarak başlıyoruz. Tüm veri erişimlerimizi doğrudan denetleyici eylemlerimizden gerçekleştiririz.

Ardından, Depo desenini nasıl kullanacağınızı öğreneceksiniz. Depo deseni kullanmak biraz daha fazla çalışma gerektirir. Ancak, bu deseni benimsemenin avantajı, değiştirilebilen ve kolayca sınanabilen uygulamalar oluşturmanıza olanak sağlamasıdır.

## <a name="what-is-a-model-class"></a>Model Sınıfı nedir?

Bir MVC modeli, MVC görünümünde veya MVC denetleyicisinde yer alan tüm uygulama mantığını içerir. Özellikle, bir MVC modeli tüm uygulama iş ve veri erişim mantığı içerir.

Veri erişim mantığınızı uygulamak için çeşitli teknolojiler kullanabilirsiniz. Örneğin, Microsoft Entity Framework, NHibernate, Subsonic veya ADO.NET sınıflarını kullanarak veri erişim sınıflarınızı oluşturabilirsiniz.

Bu öğreticide, veritabanını sorgulamak ve güncelleştirmek için LINQ'dan SQL'e kullanıyorum. LINQ'dan SQL'e microsoft SQL Server veritabanıile etkileşim kurmanın çok kolay bir yöntemini sağlar. Ancak, ASP.NET MVC çerçevesinin linq'e sql'e herhangi bir şekilde bağlı olmadığını anlamak önemlidir. ASP.NET MVC herhangi bir veri erişim teknolojisi ile uyumludur.

## <a name="create-a-movie-database"></a>Film Veritabanı Oluşturma

Bu öğreticide -- model sınıflarını nasıl oluşturabileceğinizi göstermek için -- basit bir Film veritabanı uygulaması oluşturuyoruz. İlk adım yeni bir veritabanı oluşturmaktır. Çözüm Gezgini\_penceresindeki Uygulama Verileri klasörüne sağ tıklayın ve **Ekle, Yeni Öğe**seçeneğini seçin. SQL **Server Veritabanı** şablonu seçin, ona MoviesDB.mdf adını verin ve **Ekle** düğmesini tıklatın (Bkz. Şekil 1).

[![Yeni bir SQL Server Veritabanı Ekleme](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Şekil 01**: Yeni bir SQL Server Veritabanı Ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))

Yeni veritabanını oluşturduktan sonra, App\_Data klasöründeki MoviesDB.mdf dosyasını çift tıklatarak veritabanını açabilirsiniz. MoviesDB.mdf dosyasına çift tıklayarak Sunucu Gezgini penceresini açar (Bkz. Şekil 2).

Sunucu Gezgini penceresi, Visual Web Developer'ı kullanırken Veritabanı Gezgini penceresi olarak adlandırılır.

[![Sunucu Gezgini penceresini kullanma](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Şekil 02**: Sunucu Gezgini penceresini kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))

Filmlerimizi temsil eden veritabanımıza bir tablo eklemeliyiz. Tablolar klasörüne sağ tıklayın ve **menü**seçeneğini yeni tablo ekle seçeneğini seçin. Bu menü seçeneğini seçmek tablo tasarımcısını açar (Bkz. Şekil 3).

[![Sunucu Gezgini penceresini kullanma](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Şekil 03**: Tablo Tasarımcısı ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))

Veritabanı tablomuza aşağıdaki sütunları eklememiz gerekir:

| **Sütun Adı** | **Veri Türü** | **Nulls'a İzin Ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar(200) | False |
| Yönetmen | Nvarchar(50) | False |

Kimlik sütununa iki özel şey yapmanız gerekir. İlk olarak, Tablo Tasarımcısı'ndaki sütunu seçip bir anahtarın simgesini tıklatarak Id sütununu birincil anahtar sütunu olarak işaretlemeniz gerekir. LINQ'dan SQL'e, veritabanına karşı ekler veya güncelleştirmeler gerçekleştirirken birincil anahtar sütunlarınızı belirtmenizi gerektirir.

Ardından, Evet değerini **Is Identity** özelliğine atayarak Kimlik sütununa Kimlik sütunu olarak işaretlemeniz gerekir (Bkz. Şekil 3). Kimlik sütunu, tabloya yeni bir veri satırı eklediğinizde otomatik olarak yeni bir sayı atanan sütundur.

## <a name="create-linq-to-sql-classes"></a>SQL Sınıflarına LINQ oluşturma

MVC modelimiz, tblMovie veritabanı tablosunu temsil eden LINQ-SQL sınıflarını içerir. Bu LINQ'dan SQL sınıflarına doğru oluşturmanın en kolay yolu Modeller klasörüne sağ tıklamak, **Ekle, Yeni Öğe'yi**seçmek, LINQ'dan SQL Sınıflara şablonu seçmek, sınıflara Movie.dbml adını vermek ve **Ekle** düğmesini tıklamaktır (Şekil 4'e bakın).

[![SQL sınıflarına LINQ oluşturma](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Şekil 04**: SQL sınıflarına LINQ oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))

Movie LINQ to SQL Classes'ı oluşturduktan hemen sonra Object Relational Designer görüntülenir. Belirli veritabanı tablolarını temsil eden SQL Sınıfları IÇIN LINQ oluşturmak için Veritabanı tablolarını Sunucu Gezgini penceresinden Object İlişkisel Tasarımcı'ya sürükleyebilirsiniz. TblMovie veritabanı tablosunu Object İlişkisel Tasarımcı'ya eklememiz gerekir (bkz. Şekil 5).

[![Nesne İlişkisel Tasarımcıyı Kullanma](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Şekil 05**: Nesne İlişkisel Tasarımcısı nı Kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))

Varsayılan olarak, Nesne İlişkisel Tasarımcısı, Tasarımcı'ya sürüklediğiniz veritabanı tablosuyla aynı ada sahip bir sınıf oluşturur. Ancak, sınıfımızı `tblMovie`aramak istemiyoruz. Bu nedenle, Tasarımcı'daki sınıfın adını tıklatın ve sınıfın adını Film olarak değiştirin.

Son olarak, LINQ'yi SQL Sınıflarına kaydetmek için **Kaydet** düğmesini (disketin resmi) tıklatmayı unutmayın. Aksi takdirde, LINQ to SQL Sınıfları Object İlişkisel Tasarımcı tarafından oluşturulamaz.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Denetleyici Eyleminde LINQ'dan SQL'e KULLANMA

Artık LINQ'dan SQL'e sınıflarımız olduğuna göre, veritabanından veri almak için bu sınıfları kullanabiliriz. Bu bölümde, doğrudan bir denetleyici eylem içinde SQL sınıfları LINQ nasıl kullanılacağını öğrenirler. TBLMovies veritabanı tablosundaki filmlerin listesini MVC görünümünde görüntüleyeceğiz.

İlk olarak, HomeController sınıfını değiştirmemiz gerekiyor. Bu sınıf, uygulamanızın Denetleyicileri klasöründe bulunabilir. Liste 1'deki sınıfa benzeyerek sınıfı değiştirin.

**İlan 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

Listeleme 1'deki eylem, `Index()` `MovieDataContext` `MoviesDB` veritabanını temsil etmek için BIR LINQ-SQL DataContext sınıfı (the) kullanır. Sınıf `MoveDataContext` Visual Studio Object İlişkisel Tasarımcı tarafından oluşturuldu.

Tüm filmleri `tblMovies` veritabanı tablosundan almak için DataContext'a karşı bir LINQ sorgusu gerçekleştirilir. Film listesi adlı `movies`yerel bir değişkene atanır. Son olarak, film listesi görünüm verileri aracılığıyla görünüme aktarılır.

Filmleri göstermek için, bir sonraki Dizin görünümünü değiştirmemiz gerekir. Klasörde `Views\Home\` Dizin görünümünü bulabilirsiniz. Liste 2'deki görünüme benzer şekilde Dizin görünümünü güncelleştirin.

**Listeleme 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Değiştirilen Dizin görünümü, `<%@ import namespace %>` görünümün üst kısmında bir yönerge içerir dikkat edin. Bu yönerge, `MvcApplication1.Models namespace`'. Görünümdeki `model` sınıflarla - özellikle de `Movie` sınıfla - çalışabilmek için bu ad alanına ihtiyacımız var.

Listeleme 2'deki `foreach` görünüm, `ViewData.Model` özellik tarafından temsil edilen tüm öğeler arasında yineleyen bir döngü içerir. Özelliğin `Title` değeri her `movie`biri için görüntülenir.

`ViewData.Model` Özelliğin değerinin bir `IEnumerable`. Bu, içeriğini döngü için `ViewData.Model`gereklidir. Başka bir seçenek burada güçlü bir `view`şekilde yazılmış oluşturmaktır. Güçlü bir şekilde yazılan bir `view`özellik oluşturduğunuzda, `ViewData.Model` özelliği görünümün kod arkası sınıfında belirli bir türe atarsınız.

`HomeController` Uygulamayı sınıfı ve Dizin görünümünü değiştirdikten sonra çalıştırırsanız, boş bir sayfa alırsınız. `tblMovies` Veritabanı tablosunda film kaydı olmadığından boş bir sayfa alırsınız.

`tblMovies` Veritabanı tablosuna kayıt eklemek için, Server `tblMovies` Explorer penceresindeki veritabanı tablosuna (Visual Web Developer'da Veritabanı Gezgini penceresi) sağ tıklayın ve Tablo Verilerini Göster menüsü seçeneğini seçin. Görünen ızgarayı `movie` kullanarak kayıtları ekleyebilirsiniz (Bkz. Şekil 6).

[![Film ekleme](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Şekil 06**: Film ekleme([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))

`tblMovies` Tabloya bazı veritabanı kayıtları ekledikten ve uygulamayı çalıştırdıktan sonra, sayfayı Şekil 7'de görürsünüz. Tüm film veritabanı kayıtları madde işaretli listede görüntülenir.

[![Dizin görünümüyle film görüntüleme](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Şekil 07**: Dizin görünümünde film görüntüleme([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Depo Deseni Kullanma

Önceki bölümde, doğrudan bir denetleyici eylem içinde SQL sınıfları LINQ kullanılır. `MovieDataContext` Sınıfı doğrudan denetleyici eyleminden kullandık. `Index()` Basit bir uygulama durumunda bunu yapmanın yanlış bir şey yoktur. Ancak, denetleyici sınıfında doğrudan LINQ'dan SQL'e çalışmak, daha karmaşık bir uygulama oluşturmanız gerektiğinde sorunlar oluşturur.

Bir denetleyici sınıfı içinde LINQ'dan SQL'e kullanmak, gelecekte veri erişim teknolojilerinde geçiş yapmayı zorlaştırır. Örneğin, Microsoft LINQ'yi kullanmaktan SQL'e, veri erişim teknolojiniz olarak Microsoft Entity Framework'e geçmeye karar verebilirsiniz. Bu durumda, uygulamanızdaki veritabanına erişen tüm denetleyicileri yeniden yazmanız gerekir.

Denetleyici sınıfı içinde LINQ'dan SQL'e kullanmak, uygulamanız için birim testleri oluşturmayı da zorlaştırır. Normalde, birim testleri gerçekleştirirken bir veritabanı ile etkileşim kurmak istemiyorum. Veritabanı sunucunuzu değil, uygulama mantığınızı sınamak için birim testlerinizi kullanmak istiyorsunuz.

Gelecekteki değişime daha uygun ve daha kolay sınanabilecek bir MVC uygulaması oluşturmak için Depo deseni kullanmayı düşünmelisiniz. Depo deseni kullandığınızda, tüm veritabanı erişim mantığınızı içeren ayrı bir depo sınıfı oluşturursunuz.

Depo sınıfını oluşturduğunuzda, depo sınıfı tarafından kullanılan tüm yöntemleri temsil eden bir arabirim oluşturursunuz. Denetleyicilerinizde, kodunuzu depo yerine arabiriyine yazarsınız. Bu şekilde, gelecekte farklı veri erişim teknolojilerini kullanarak depoyu uygulayabilirsiniz.

Listeleme 3'teki `IMovieRepository` arabirim adlandırılmış ve `ListAll()`..

**İlan 3 –`Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

Listeleme 4'teki depo sınıfı `IMovieRepository` arabirimi uygular. Arabirimin gerektirdiği yönteme `ListAll()` karşılık gelen adlandırılmış bir `IMovieRepository` yöntem içerdiğine dikkat edin.

**İlan 4 –`Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Son olarak, Listeleme 5'teki `MoviesController` sınıf Depo deseni kullanır. Artık DOĞRUDAN SQL sınıfları IÇIN LINQ kullanır.

**İlan 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Listeleme `MoviesController` 5'teki sınıfın iki oluşturucusu olduğuna dikkat edin. Uygulamanız çalışırken ilk oluşturucu, parametresiz oluşturucu çağrılır. Bu oluşturucu `MovieRepository` sınıfın bir örneğini oluşturur ve ikinci oluşturucuya geçirir.

İkinci oluşturucunun tek bir parametresi vardır: bir `IMovieRepository` parametre. Bu oluşturucu sadece parametrenin değerini sınıf düzeyinde bir `_repository`alana atar.

Sınıf `MoviesController` Bağımlılık Enjeksiyon deseni olarak adlandırılan bir yazılım tasarım deseni yararlanarak. Özellikle, Yapıcı Bağımlılık Enjeksiyon denilen bir şey kullanıyor. Martin Fowler tarafından aşağıdaki makaleyi okuyarak bu desen hakkında daha fazla bilgi edinebilirsiniz:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

`MoviesController` Sınıftaki tüm kodun (ilk oluşturucu hariç) gerçek `MovieRepository` sınıf yerine `IMovieRepository` arabirimle etkileşime geçtiğine dikkat edin. Kod, arabirimin somut bir uygulaması yerine soyut bir arabirimle etkileşime girer.

Uygulama tarafından kullanılan veri erişim teknolojisini değiştirmek istiyorsanız, `IMovieRepository` arabirimi alternatif veritabanı erişim teknolojisini kullanan bir sınıfla uygulayabilirsiniz. Örneğin, bir `EntityFrameworkMovieRepository` sınıf veya sınıf `SubSonicMovieRepository` oluşturabilirsiniz. Denetleyici sınıfı arabirime karşı programlandığı için, denetleyici `IMovieRepository` sınıfına yeni bir uygulama geçirebilirsiniz ve sınıf çalışmaya devam eder.

Ayrıca, `MoviesController` sınıf test etmek istiyorsanız, o zaman sahte bir film deposu sınıf `HomeController`geçebilir . Sınıfı, veritabanına `IMovieRepository` gerçekte erişmeyen ancak `IMovieRepository` arabirimin gerekli tüm yöntemlerini içeren bir sınıfla uygulayabilirsiniz. Bu şekilde, gerçek bir `MoviesController` veritabanına erişmeden sınıfı birim olarak gerçekleştirebilirsiniz.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, Microsoft LINQ'dan SQL'e yararlanarak MVC model sınıflarını nasıl oluşturabileceğinizi göstermekti. Veritabanı verilerini ASP.NET bir MVC uygulamasında görüntülemek için iki stratejiyi inceledik. İlk olarak, LINQ'dan SQL sınıflarına oluşturduk ve sınıfları doğrudan bir denetleyici eylemi içinde kullandık. Bir denetleyici içinde LINQ'dan SQL sınıflarına doğru kullanmak, veritabanı verilerini bir MVC uygulamasında hızlı ve kolay bir şekilde görüntülemenizi sağlar.

Sonra, veritabanı verilerini görüntülemek için biraz daha zor, ama kesinlikle daha erdemli bir yol araştırdık. Depo deseninden yararlandık ve tüm veritabanı erişim mantığımızı ayrı bir depo sınıfına yerleştirdik. Denetleyicimizde, tüm kodlarımızı somut bir sınıf yerine bir arayüze karşı yazdık. Depo deseninin avantajı, gelecekte veritabanı erişim teknolojilerini kolayca değiştirmemizi ve denetleyici sınıflarımızı kolayca test etmemizi sağlamasıdır.

> [!div class="step-by-step"]
> [Önceki](creating-model-classes-with-the-entity-framework-cs.md)
> [Sonraki](displaying-a-table-of-database-data-cs.md)
