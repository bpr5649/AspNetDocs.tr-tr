---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC web uygulaması için gelişmiş Entity Framework senaryoları (10/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85dd59016d904a9f654c438db977b5ae2c0187d2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045058"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>MVC web uygulaması için gelişmiş Entity Framework senaryoları (10/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide depo ve iş deseni birimi uyguladık. Bu öğreticide aşağıdaki konular ele alınmaktadır:

- Ham SQL sorguları gerçekleştiriliyor.
- Hiçbir izleme sorgusu gerçekleştiriliyor.
- Veritabanına gönderilen sorgular inceleniyor.
- Proxy sınıflarıyla çalışma.
- Değişikliklerin otomatik algılanması devre dışı bırakılıyor.
- Değişiklikler kaydedilirken doğrulama devre dışı bırakılıyor.
- [Hatalar ve Iş arounds](#errors)

Bu konuların çoğu için, zaten oluşturduğunuz sayfalarla çalışacaksınız. Ham SQL 'i toplu güncelleştirmeler yapmak üzere kullanmak için, veritabanındaki tüm kursların kredi sayısını güncelleştiren yeni bir sayfa oluşturacaksınız:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Ve hiçbir izleme sorgusu kullanmak için departman düzenleme sayfasına yeni doğrulama mantığı ekleyeceksiniz:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>Ham SQL sorguları gerçekleştirme

Entity Framework Code First API 'SI, SQL komutlarını doğrudan veritabanına geçirmenize olanak sağlayan yöntemleri içerir. Aşağıdaki seçenekler mevcuttur:

- `DbSet.SqlQuery`Varlık türleri döndüren sorgular için yöntemini kullanın. Döndürülen nesneler nesne tarafından beklenen türde olmalıdır `DbSet` ve izlemeyi kapatmadığınız takdirde veritabanı bağlamı tarafından otomatik olarak izlenir. (Yöntemiyle ilgili aşağıdaki bölüme bakın `AsNoTracking` .)
- Varlık olmayan `Database.SqlQuery` türleri döndüren sorgular için yöntemini kullanın. Döndürülen veriler, varlık türlerini almak için bu yöntemi kullanıyor olsanız bile veritabanı bağlamı tarafından izlenmez.
- Sorgu olmayan komutlar için [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) kullanın.

Entity Framework kullanmanın avantajlarından biri, kodunuzun veri depolarken belirli bir yönteme çok benzemesidir. Bunu sizin için SQL sorguları ve komutları oluşturarak yapar, bu da sizi kendiniz yazmak zorunda kalmaktan kurtarır. Ancak, el ile oluşturduğunuz belirli SQL sorgularını çalıştırmanız gerektiğinde olağanüstü senaryolar vardır ve bu yöntemler bu tür özel durumları idare etmek için bu yöntemleri mümkün kılar.

Her zaman doğru olduğu gibi, bir Web uygulamasında SQL komutları yürüttüğünüzde, sitenizi SQL ekleme saldırılarına karşı korumak için önlemler almalısınız. Bunu yapmanın bir yolu, bir Web sayfası tarafından gönderilen dizelerin SQL komutları olarak yorumlanamadığından emin olmak için parametreli sorgular kullanmaktır. Bu öğreticide Kullanıcı girişini bir sorguyla tümleştirdiğinizde parametreli sorgular kullanacaksınız.

### <a name="calling-a-query-that-returns-entities"></a>Varlıkları döndüren bir sorgu çağırma

`GenericRepository`Sınıfın, ek yöntemlerle türetilmiş bir sınıf oluşturmanıza gerek kalmadan ek filtreleme ve sıralama esnekliği sağlamasını istediğinizi varsayalım. Bunu yapmanın bir yolu, bir SQL sorgusunu kabul eden bir yöntem eklemektir. Daha sonra, denetleyicide istediğiniz filtre veya sıralama türlerini ( `Where` bir birleşimlere veya alt verilere bağlı bir yan tümce gibi) belirtebilirsiniz. Bu bölümde, böyle bir yöntemi nasıl uygulayacağınızı göreceksiniz.

`GetWithRawSql` *GenericRepository.cs*öğesine aşağıdaki kodu ekleyerek yöntemi oluşturun:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

*CourseController.cs*' de, `Details` Aşağıdaki örnekte gösterildiği gibi, yönteminden yeni yöntemi çağırın:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

Bu durumda, yöntemini kullandınız `GetByID` , ancak yöntemin `GetWithRawSql` çalıştığını doğrulamak için yöntemini kullanıyorsunuz `GetWithRawSQL` .

Seçme sorgusunun çalıştığını doğrulamak için Ayrıntılar sayfasını çalıştırın ( **Kurs** sekmesini ve ardından bir kurs için **ayrıntıları** seçin).

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Diğer nesne türlerini döndüren bir sorgu çağırma

Daha önce, yaklaşık bir kayıt tarihi için öğrenci sayısını gösteren hakkında sayfasında bir öğrenci istatistikleri Kılavuzu oluşturdunuz. *HomeController.cs* içinde bunu yapan kod LINQ kullanır:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

LINQ kullanmak yerine, bu verileri doğrudan SQL 'de alan kodu yazmak istediğinizi varsayalım. Bunu yapmak için, varlık nesneleri dışında bir şey döndüren bir sorgu çalıştırmanız gerekir, bu da yöntemini kullanmanız gereken anlamına gelir `Database.SqlQuery` .

*HomeController.cs*' de, yöntemindeki LINQ ifadesini `About` aşağıdaki kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Hakkında sayfasını çalıştırın. Daha önce yaptığımız verileri görüntüler.

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>Güncelleştirme sorgusu çağırma

Contoso Üniversitesi yöneticilerinin veritabanında toplu değişiklikler gerçekleştirebilmesini istediğini varsayalım (her kurs için kredilerin sayısını değiştirme gibi). Üniversitenin çok sayıda kursu varsa, bunların tümünü varlıklar olarak almak ve tek tek değiştirmek verimsiz olur. Bu bölümde, kullanıcının tüm kurslar için kredi sayısını değiştirecek bir faktör belirtmesini sağlayan bir Web sayfası uygulayacaksınız ve bir SQL ifadesini yürüterek değişikliği yaparsınız `UPDATE` . Web sayfası aşağıdaki çizimde gösterildiği gibi görünür:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

Önceki öğreticide, denetleyicideki varlıkları okumak ve güncelleştirmek için genel depoyu kullandınız `Course` `Course` . Bu toplu güncelleştirme işlemi için genel depoda olmayan yeni bir depo yöntemi oluşturmanız gerekir. Bunu yapmak için, `CourseRepository` sınıfından türetilen ayrılmış bir sınıf oluşturacaksınız `GenericRepository` .

*Dal* klasöründe *CourseRepository.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

*UnitOfWork.cs*' de, `Course` Depo türünü olarak değiştirin `GenericRepository<Course>``CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

*CourseController.cs*içinde bir yöntem ekleyin `UpdateCourseCredits` :

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

Bu yöntem, ve için kullanılacaktır `HttpGet` `HttpPost` . `HttpGet` `UpdateCourseCredits` Yöntem çalıştığında, `multiplier` değişken null olur ve görünüm, önceki çizimde gösterildiği gibi boş bir metin kutusu ve bir Gönder düğmesi görüntüler.

**Güncelleştirme** düğmesine tıklandığında ve `HttpPost` yöntemi çalıştırıldığında, `multiplier` metin kutusuna girilen değer olacaktır. Kod daha sonra, `UpdateCourseCredits` etkilenen satırların sayısını döndüren depo yöntemini çağırır ve bu değer `ViewBag` nesnede saklanır. Görünüm nesnedeki etkilenen satırların sayısını aldığında `ViewBag` , aşağıdaki çizimde gösterildiği gibi metin kutusu ve Gönder düğmesi yerine bu numarayı görüntüler:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

Kurs kredilerini Güncelleştir sayfasının *Views\kurs* klasöründe bir görünüm oluşturun:

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

*Views\course\updatecoursecredıts.exe*' de, şablon kodunu şu kodla değiştirin:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

`UpdateCourseCredits` **Kurs** sekmesini seçerek yöntemi çalıştırın, sonra TARAYıCıNıN adres çubuğundaki URL 'nin sonuna "/UpdateCourseCredits" ekleyin (örneğin: `http://localhost:50205/Course/UpdateCourseCredits` ). Metin kutusuna bir sayı girin:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

**Güncelleştir**’e tıklayın. Etkilenen satır sayısını görürsünüz:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

Düzeltilen kredi sayısına sahip kurslar listesini görmek için **listeye geri** ' ye tıklayın.

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

Ham SQL sorguları hakkında daha fazla bilgi için Entity Framework ekip bloguna [Ham SQL sorguları](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) konusuna bakın.

## <a name="no-tracking-queries"></a>Izleme sorguları yok

Bir veritabanı bağlamı veritabanı satırlarını aldığında ve bunları temsil eden varlık nesneleri oluşturduğunda, varsayılan olarak, bellekteki varlıkların veritabanında bulunan verilerle eşitlenmiş olup olmadığını izler. Bellekteki veriler önbellek olarak davranır ve bir varlığı güncelleştirdiğinizde kullanılır. Bağlam örnekleri genellikle kısa süreli olduğundan (her istek için yeni bir tane oluşturulup bırakıldığı) ve bir varlığı okuyan bağlam genellikle bu varlık yeniden kullanılmadan önce atıldığından, bu önbelleğe alma işlemi bir Web uygulamasında genellikle gereksizdir.

Bağlamını kullanarak bir sorgu için varlık nesnelerini izleyip izlemediğini belirtebilirsiniz `AsNoTracking` . Bunu yapmak isteyebileceğiniz tipik senaryolar şunlardır:

- Sorgu, izlemeyi kapatan büyük miktarda veriyi alır, performansı önemli ölçüde artırabilir.
- Bir varlığı güncelleştirmek için eklemek istiyorsunuz, ancak daha önce aynı varlığı farklı bir amaç için elde edersiniz. Varlık veritabanı bağlamı tarafından zaten izlenmekte olduğundan, değiştirmek istediğiniz varlığı iliştiremiyoruz. Bunun oluşmasını önlemenin bir yolu, `AsNoTracking` önceki sorguyla birlikte seçeneğini kullanmaktır.

Bu bölümde, bu senaryoların ikinci kısmını gösteren iş mantığını uygulayacaksınız. Özellikle, bir eğitmenin birden fazla departmanın yöneticisi olmadığını belirten bir iş kuralı zorlayacaksınız.

*DepartmentController.cs*' de, `Edit` `Create` iki bölümün aynı yöneticiye sahip olmadığından emin olmak için ve yöntemlerinden çağırabilmeniz gereken yeni bir yöntem ekleyin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

`try` `HttpPost` `Edit` Doğrulama hatası yoksa, bu yeni yöntemi çağırmak için yönteminin bloğundaki kodu ekleyin. `try`Bloğu şimdi aşağıdaki örneğe benzer şekilde görünür:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

Departman düzenleme sayfasını çalıştırın ve bir departmanın yöneticisini, zaten farklı bir departmanın yöneticisi olan bir eğitmene değiştirmeyi deneyin. Beklenen hata iletisini alırsınız:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Şimdi departman düzenleme sayfasını yeniden çalıştırın ve bu kez **Bütçe** miktarını değiştirin. **Kaydet**' e tıkladığınızda bir hata sayfası görürsünüz:

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

Özel durum hata iletisi, `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` aşağıdaki olaylar dizisi nedeniyle gerçekleşti:

- `Edit`Yöntemi, `ValidateOneAdministratorAssignmentPerInstructor` yönetici olarak Kim Abercrombie olan tüm departmanları alan yöntemini çağırır. Bu, Ingilizce departmanın okunmasına neden olur. Bu departman düzenlendiğinden, hiçbir hata bildirilmemiştir. Ancak, bu okuma işleminin sonucu olarak, veritabanından okunan Ingilizce departman varlığı artık veritabanı bağlamı tarafından izlenir.
- `Edit`Yöntemi, `Modified` MVC model Ciltçi tarafından oluşturulan İngilizce Bölüm varlığındaki bayrağı ayarlamaya çalışır, ancak bağlam İngilizce departmanı için bir varlığı zaten izliyor olduğundan bu başarısız olur.

Bu soruna yönelik bir çözüm, içeriğin doğrulama sorgusu tarafından alınan bellek içi departman varlıklarını izlemesini sağlar. Bunu yapmanın bir dezavantajı yoktur, çünkü bu varlığı güncellemeden veya bellekte önbelleğe alınmasından faydalanabilir bir şekilde tekrar okuyamayacağız.

*DepartmentController.cs*' de, `ValidateOneAdministratorAssignmentPerInstructor` yönteminde, aşağıda gösterildiği gibi, izleme yok ' u belirtin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

Bir departmanın **Bütçe** miktarını düzenleme denemesinden tekrarlayın. Bu kez işlem başarılı olur ve site, düzeltilen bütçe değerini gösteren departmanlar dizin sayfasına beklenen şekilde geri döner.

## <a name="examining-queries-sent-to-the-database"></a>Veritabanına gönderilen sorgular inceleniyor

Bazen veritabanına gönderilen gerçek SQL sorgularını görmeniz yararlı olabilir. Bunu yapmak için, hata ayıklayıcıda bir sorgu değişkenini inceleyebilir veya sorgunun `ToString` metodunu çağırabilirsiniz. Bunu denemek için, basit bir sorguya bakacaksınız ve sonra yükleme, filtreleme ve sıralama gibi seçenekleri eklerken ne olacağı hakkında bilgi edineceksiniz.

*Denetleyiciler/CourseController*içinde, `Index` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

Şimdi ve içindeki *GenericRepository.cs* içinde bir kesme noktası ayarlayın `return query.ToList();` `return orderBy(query).ToList();` `Get` . Projeyi hata ayıklama modunda çalıştırın ve kurs dizini sayfasını seçin. Kod kesme noktasına ulaştığında, `query` değişkeni inceleyin. SQL Server gönderilen sorguyu görürsünüz. Bu basit bir `Select` ifadedir:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.sql)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

Sorgular, Visual Studio 'da hata ayıklama penceresinde görüntülenemeyecek kadar uzun olabilir. Sorgunun tamamını görmek için değişken değerini kopyalayabilir ve bir metin düzenleyicisine yapıştırabilirsiniz:

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

Şimdi, kullanıcıların belirli bir departmanı filtreleyebilmesi için kurs dizini sayfasına açılan bir liste ekleyeceksiniz. Kursları başlığa göre sıralarsınız ve gezinti özelliği için bir Eager yüklemesi belirlersiniz `Department` . *CourseController.cs*içinde, `Index` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

Yöntemi, parametresindeki açılan listenin seçili değerini alır `SelectedDepartment` . Hiçbir şey seçilmezse, bu parametre null olur.

`SelectList`Tüm departmanları içeren bir koleksiyon, açılan listenin görünümüne geçirilir. Oluşturucuya geçirilen parametreler `SelectList` değer alanı adını, metin alanı adını ve seçilen öğeyi belirtin.

`Get`Deponun yöntemi için kod, `Course` gezinti özelliği için bir filtre ifadesi, bir sıralama düzeni ve bir Eager yüklemesi belirtir `Department` . Filtre ifadesi her zaman, `true` açılan listede hiçbir şey seçilmezse (yani, null) ' i döndürür `SelectedDepartment` .

*Views\course\ındex.cshtml*içinde, açılış etiketinden hemen önce, `table` açılan listeyi ve bir Gönder düğmesini oluşturmak için aşağıdaki kodu ekleyin:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

Kesme noktaları sınıfta hala ayarlandığında `GenericRepository` , kurs dizini sayfasını çalıştırın. Sayfanın tarayıcıda görüntülenebilmesi için, kodun bir kesme noktasıyla karşılaşabilmesi için ilk iki kez devam edin. Aşağı açılan listeden bir departman seçin ve **Filtrele**' ye tıklayın:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

Bu kez, ilk kesme noktası, açılan liste için departmanlar sorgusu olacaktır. Bu sorguyu atlayın ve bir `query` sonraki kod, şimdi sorgunun nasıl göründüğünü görmek için kesme noktasına bir sonraki sefer ulaştığında değişkeni görüntüleyin `Course` . Aşağıdakine benzer bir şey göreceksiniz:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.sql)]

Sorgunun artık verileri verilerle `JOIN` birlikte yükleyen bir sorgu olduğunu `Department` `Course` ve bir `WHERE` yan tümce içerdiğine bakabilirsiniz.

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>Proxy sınıflarıyla çalışma

Entity Framework varlık örnekleri oluşturduğunda (örneğin, bir sorgu yürüttüğünüzde), bu, genellikle varlık için proxy görevi gören dinamik olarak oluşturulan türetilmiş türün örnekleri olarak oluşturulur. Bu proxy, özellik erişildiği zaman otomatik olarak eylem gerçekleştirmeye yönelik kancalar eklemek için varlığın bazı sanal özelliklerini geçersiz kılar. Örneğin, bu mekanizma ilişkilerin geç yüklemesini desteklemek için kullanılır.

Çoğu zaman, bu proxy kullanımını bilmeniz gerekmez, ancak özel durumlar vardır:

- Bazı senaryolarda Entity Framework proxy örnekleri oluşturmasını engellemek isteyebilirsiniz. Örneğin, proxy olmayan örneklerin serileştirilmesi proxy örneklerinden serileştirilden daha verimli olabilir.
- İşlecini kullanarak bir varlık sınıfını örneklediğinizde `new` , proxy örneği edinmezsiniz. Bu, yavaş yükleme ve otomatik değişiklik izleme gibi işlevleri edinmeyeceğiniz anlamına gelir. Bu genellikle normaldir; Genellikle, veritabanında olmayan yeni bir varlık oluşturmakta olduğunuz ve genellikle varlığı açıkça işaretlemezseniz değişiklik izlemeye ihtiyaç duymadığınızı, genellikle geç yüklemeye gerek kalmaz `Added` . Ancak, geç yüklemeye ihtiyacınız varsa ve değişiklik izlemeye ihtiyacınız varsa, sınıfının yöntemini kullanarak proxy ile yeni varlık örnekleri oluşturabilirsiniz `Create` `DbSet` .
- Bir proxy türünden gerçek bir varlık türü almak isteyebilirsiniz. `GetObjectType` `ObjectContext` Bir proxy türü örneğinin gerçek varlık türünü almak için sınıfının yöntemini kullanabilirsiniz.

Daha fazla bilgi için bkz. Entity Framework ekip blogundan [proxy Ile çalışma](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) .

## <a name="disabling-automatic-detection-of-changes"></a>Değişikliklerin otomatik olarak algılanmasını devre dışı bırakma

Entity Framework bir varlığın geçerli değerlerini özgün değerlerle karşılaştırarak bir varlığın nasıl değiştiğini (ve bu nedenle veritabanına gönderilmesi gereken güncelleştirmeleri) belirler. Özgün değerler, varlık sorgulanırken veya eklendiğinde saklanır. Otomatik değişiklik algılamaya neden olan yöntemlerin bazıları şunlardır:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Çok sayıda varlığı izliyorsanız ve bu yöntemlerden birini bir döngüde birçok kez çağırırsanız, otomatik değişiklik algılamayı geçici olarak devre dışı [bırakarak otomatik değişiklik](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) algılamayı el ile kapatarak önemli performans iyileştirmeleri alabilirsiniz. Daha fazla bilgi için bkz. [değişiklikleri otomatik olarak algılama](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).

## <a name="disabling-validation-when-saving-changes"></a>Değişiklikler kaydedilirken doğrulamayı devre dışı bırakma

`SaveChanges`Yöntemini çağırdığınızda, varsayılan olarak Entity Framework, veritabanını güncelleştirmeden önce tüm değiştirilen varlıkların tüm özelliklerindeki verileri doğrular. Çok sayıda varlığı güncelleştirdiyseniz ve verileri zaten doğruladıysanız, bu çalışma gereksizdir ve değişiklikleri kaydetme sürecini geçici olarak doğrulamayı devre dışı bırakarak daha az zaman alabilir. Bunu, [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) özelliğini kullanarak yapabilirsiniz. Daha fazla bilgi için bkz. [doğrulama](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).

## <a name="summary"></a>Özet

Bu, bir ASP.NET MVC uygulamasında Entity Framework kullanma hakkında bu öğretici serisini tamamlar. Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

Web uygulamanızı oluşturduktan sonra dağıtma hakkında daha fazla bilgi için, MSDN Kitaplığı 'nda [ASP.NET dağıtım Içerik Haritası](https://msdn.microsoft.com/library/bb386521.aspx) ' na bakın.

Kimlik doğrulama ve yetkilendirme gibi MVC ile ilgili diğer konular hakkında daha fazla bilgi için bkz. [MVC önerilen kaynaklar](../../getting-started/recommended-resources-for-mvc.md).

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>Teşekkürler

- Tom Dykstra, Bu öğreticinin orijinal sürümünü yazdı ve Microsoft Web platformu ve araçlar Içerik ekibi üzerinde bir kıdemli programlama yazdır.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) bu öğreticiyi yazdı ve en fazla iş bu ÖĞRETICIYI, EF 5 ve MVC 4 için güncelleştirti. Rick, Microsoft 'un Azure ve MVC 'ye odaklanarak bir üst düzey programlama yazdır.
- [Rowa Miller](http://www.romiller.com) ve Entity Framework ekip yardımı 'nın diğer üyeleri kod İncelemeleri Ile ve EF 5 için öğreticiyi güncelleştirtiğimiz sırada çok sayıda sorunu ayıklamanıza yardımcı oldu.

## <a name="vb"></a>VB

Öğretici ilk üretildiğinde, tamamlanan indirme projesinin hem C# hem de VB sürümlerini sağladık. Bu güncelleştirmeyle, her bir bölüm için her yerden çalışmaya daha kolay hale getirmek için C# indirilebilir bir proje sunuyoruz, ancak zaman sınırlamaları ve diğer öncelikler VB. için bunu gerçekleştirmedik. Bu öğreticileri kullanarak VB projesi derleyebilir ve bunları başkalarıyla paylaşmak istiyorsanız lütfen bize bildirin.

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>Hatalar ve geçici çözümler

### <a name="cannot-createshadow-copy"></a>Gölge kopya oluşturulamıyor

Hata İletisi:

*Bu dosya zaten mevcutsa, ' DotNetOpenAuth. OpenID ' kopyası oluşturulamıyor/gölge kopyası oluşturulamıyor.*

Çözüm:

Birkaç saniye bekleyin ve sayfayı yenileyin.

### <a name="update-database-not-recognized"></a>Güncelleştirme-veritabanı tanınmıyor

Hata İletisi:

*' Update-Database ' terimi bir cmdlet, işlev, betik dosyası veya çalıştırılabilir programının adı olarak tanınmıyor. Adın yazımını denetleyin veya bir yol içerilip yolun doğru olduğundan emin olun ve yeniden deneyin.* ( *`Update-Database`* PMC 'deki komuttan)

Çözüm:

Visual Studio 'dan çıkın. Projeyi yeniden açın ve yeniden deneyin.

### <a name="validation-failed"></a>Doğrulama başarısız oldu

Hata İletisi:

*Bir veya daha fazla varlık için doğrulama başarısız oldu. Daha fazla ayrıntı için bkz. ' EntityValidationErrors ' özelliği.* ( *`Update-Database`* PMC 'deki komuttan)

Çözüm:

Yöntem çalışırken bu sorunun bir nedeni doğrulama hatalardır `Seed` . Yöntemi hata ayıklamayla ilgili ipuçları için bkz. [dağıtım ve hata ayıklama Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` .

### <a name="http-50019-error"></a>HTTP 500,19 hatası

Hata İletisi:

*HTTP hatası 500,19-Iç sunucu hatası istenen sayfaya erişilemiyor çünkü sayfa için ilgili yapılandırma verileri geçersiz.*

Çözüm:

Bu hatanın tek bir yolu, her biri aynı bağlantı noktası numarasını kullanarak çözümün birden çok kopyasının olmasını sağlayabilir. Bu sorunu genellikle Visual Studio 'nun tüm örneklerinden çıkıp üzerinde çalıştığınız projeyi yeniden başlatarak çözebilirsiniz. Bu işe yaramazsa, bağlantı noktası numarasını değiştirmeyi deneyin. Proje dosyasına sağ tıklayın ve ardından Özellikler ' e tıklayın. **Web** sekmesini seçin ve ardından **proje URL 'si** metin kutusunda bağlantı noktası numarasını değiştirin.

### <a name="error-locating-sql-server-instance"></a>SQL Server örneği bulunurken hata oluştu

Hata İletisi:

*SQL Server bağlantı kurulurken ağla ilgili veya örneğe özgü bir hata oluştu. Sunucu bulunamadı veya erişilebilir durumda değil. Örnek adının doğru olduğundan ve SQL Server uzak bağlantılara izin verecek şekilde yapılandırıldığından emin olun. (sağlayıcı: SQL ağ arabirimleri, hata: 26-belirtilen sunucu/örnek bulunurken hata oluştu)*

Çözüm:

Bağlantı dizesini denetleyin. Veritabanını el ile sildiyseniz, oluşturulmakta olan dizedeki veritabanının adını değiştirin.

> [!div class="step-by-step"]
> [Önceki](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
>  [Sonraki](building-the-ef5-mvc4-chapter-downloads.md)
