---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Model bağlama ve Web formları ile verileri alma ve görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240745"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>Model bağlama ve Web formları ile verileri alma ve görüntüleme

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Model bağlama modeli, herhangi bir veri erişim teknolojisi ile birlikte kullanılır. Bu öğreticide Entity Framework kullanacaksınız, ancak size en tanıdık veri erişim teknolojisini kullanabilirsiniz. GridView, ListView, DetailsView veya FormView denetimi gibi bir veri bağlantılı sunucu denetiminden, veri seçme, güncelleştirme, silme ve oluşturma için kullanılacak yöntemlerin adlarını belirtirsiniz. Bu öğreticide, SelectMethod için bir değer belirtirsiniz. 
> 
> Bu yöntemde, verileri alma mantığını sağlarsınız. Sonraki öğreticide, UpdateMethod, DeleteMethod ve InsertMethod değerlerini ayarlayacaksınız.
>
> C# veya Visual Basic tüm projeyi [indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=286116) . İndirilebilir kod, Visual Studio 2012 ve üzeri sürümlerle birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2017 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.
> 
> Öğreticide, uygulamayı Visual Studio 'da çalıştırırsınız. Ayrıca, uygulamayı bir barındırma sağlayıcısına dağıtabilir ve internet üzerinden kullanılabilir hale getirebilirsiniz. Microsoft, en fazla 10 Web sitesi için ücretsiz web barındırma hizmeti sunar.  
> [ücretsiz Azure deneme hesabı](https://azure.microsoft.com/free/dotnet/). Azure App Service Web Apps bir Visual Studio Web projesinin nasıl dağıtılacağı hakkında daha fazla bilgi için bkz. [Visual Studio Series kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md) . Bu öğretici Ayrıca, SQL Server veritabanınızı Azure SQL veritabanı 'na dağıtmak için Entity Framework Code First Migrations nasıl kullanacağınızı gösterir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> - Microsoft Visual Studio 2017 veya Microsoft Visual Studio Community 2017
>   
> Bu öğretici Visual Studio 2012 ve Visual Studio 2013 ile de birlikte çalışarak, Kullanıcı arabirimi ve proje şablonunda bazı farklılıklar vardır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide şunları yapmanız gerekir:

* Kurslara kayıtlı olan öğrencilerle bir University 'i yansıtan veri nesneleri oluşturun
* Nesnelerden veritabanı tabloları oluşturma
* Veritabanını test verileriyle doldur
* Verileri bir Web formunda görüntüleme

## <a name="create-the-project"></a>Proje oluşturma

1. Visual Studio 2017 ' de, **Contosoüniversıtymodelbinding**adlı bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun.

   ![proje oluştur](retrieving-data/_static/image19.png)

2. **Tamam**’ı seçin. Bir şablon seçmek için iletişim kutusu görüntülenir.

   ![Web formları seçin](retrieving-data/_static/image3.png)

3. **Web Forms** şablonunu seçin. 

4. Gerekirse, kimlik doğrulamasını **bireysel kullanıcı hesaplarıyla**değiştirin. 

5. Projeyi oluşturmak için **Tamam**'ı seçin.

## <a name="modify-site-appearance"></a>Site görünümünü değiştirme

   Site görünümünü özelleştirmek için birkaç değişiklik yapın. 
   
   1. Site. Master dosyasını açın.
   
   2. Başlığı, **ASP.NET uygulamamın**değil **Contoso Üniversitesi** görüntülenecek şekilde değiştirin.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. Üst bilgi metnini **uygulama adından** **Contoso Üniversitesi**olarak değiştirin.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. Gezinti üst bilgisi bağlantılarını siteyle ilgili olanlarla değiştirin. 
   
      **Hakkında** ve **iletişim kurulacak** bağlantıları kaldırın ve bunun yerine oluşturacağınız bir **öğrenciler** sayfasına bağlanın.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. Site. Master öğesini kaydedin.

## <a name="add-a-web-form-to-display-student-data"></a>Öğrenci verilerini göstermek için Web formu ekleme

   1. **Çözüm Gezgini**, projenize sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe**' yi seçin. 
   
   2. **Yeni öğe Ekle** iletişim kutusunda, **Ana sayfa şablonuyla Web formu** ' nu seçin ve bunu **öğrenciler. aspx**olarak adlandırın.

      ![sayfa oluştur](retrieving-data/_static/image5.png)

   3. **Ekle**'yi seçin.
   
   4. Web formunun ana sayfasında, **site. Master**' u seçin.
   
   5. **Tamam**’ı seçin.

## <a name="add-the-data-model"></a>Veri modelini ekleme

**Modeller** klasöründe, **UniversityModels.cs**adlı bir sınıf ekleyin.

   1. **Modeller**' e sağ tıklayın, **Ekle**' yi ve ardından **Yeni öğe**' yi seçin. **Yeni Öğe Ekle** iletişim kutusu görünür.

   2. Sol gezinti menüsünde, **kod**' u ve ardından **sınıf**' ı seçin.

      ![model sınıfı oluştur](retrieving-data/_static/image20.png)

   3. Sınıfı **UniversityModels.cs** olarak adlandırın ve **Ekle**' yi seçin.

      Bu dosyada,,, `SchoolContext` `Student` `Enrollment` ve `Course` sınıflarını aşağıdaki gibi tanımlayın:

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext`Sınıfı, `DbContext` veritabanı bağlantısını ve verilerdeki değişiklikleri yöneten öğesinden türetilir.

      Sınıfında,, `Student` ve özelliklerine uygulanan özniteliklere dikkat edin `FirstName` `LastName` `Year` . Bu öğretici, veri doğrulama için bu öznitelikleri kullanır. Kodu basitleştirmek için, yalnızca bu özellikler veri doğrulama öznitelikleriyle işaretlenir. Gerçek bir projede, doğrulama gerektiren tüm özelliklere doğrulama öznitelikleri uygularsınız.

   4. UniversityModels.cs Kaydet.

## <a name="set-up-the-database-based-on-classes"></a>Sınıfları temel alarak veritabanını ayarlama

Bu öğretici, nesne ve veritabanı tabloları oluşturmak için [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) kullanır. Bu tablolar, öğrenciler ve kurslarıyla ilgili bilgileri depolar.

   1. **Araçlar**  >  **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu**' nu seçin.

   2. **Paket Yöneticisi konsolu**'nda şu komutu çalıştırın:  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      Komut başarıyla tamamlanırsa, geçişleri belirten bir ileti görüntülenir.

      ![geçişleri etkinleştir](retrieving-data/_static/image8.png)

      *Configuration.cs* adlı bir dosyanın oluşturulduğunu unutmayın. `Configuration`Sınıfı bir yöntemine sahiptir `Seed` ve bu, veritabanı tablolarını test verileriyle önceden doldurabilir.

## <a name="pre-populate-the-database"></a>Veritabanını önceden doldur

   1. Configuration.cs 'i açın.
   
   2. `Seed` yöntemine aşağıdaki kodu ekleyin. Ayrıca, `using` ad alanı için bir ifade ekleyin `ContosoUniversityModelBinding. Models` .

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. Configuration.cs Kaydet.

   4. Paket Yöneticisi konsolunda, **ilk komut ekle-geçiş**' i çalıştırın.

   5. **Update-Database**komutunu çalıştırın.

      Bu komutu çalıştırırken bir özel durum alırsanız, `StudentID` ve `CourseID` değerleri `Seed` Yöntem değerlerinden farklı olabilir. Bu veritabanı tablolarını açın ve ve için varolan değerleri `StudentID` bulun `CourseID` . Bu değerleri tablo için sağlama koduna ekleyin `Enrollments` .

## <a name="add-a-gridview-control"></a>GridView denetimi ekleme

Doldurulmuş veritabanı verileriyle, artık bu verileri almaya ve görüntülemeye hazır olursunuz. 

1. Öğrenciler. aspx ' i açın.

2. `MainContent`Yer tutucuyu bulun. Bu yer tutucunun içinde, bu kodu içeren bir **GridView** denetimi ekleyin.

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   Dikkat edilmesi gerekenler:
   * GridView öğesinde özelliği için ayarlanan değere dikkat edin `SelectMethod` . Bu değer, bir sonraki adımda oluşturduğunuz GridView verilerini almak için kullanılan yöntemi belirtir. 
   
   * `ItemType`Özelliği `Student` daha önce oluşturulan sınıfa ayarlanır. Bu ayar, İşaretlemede Sınıf özelliklerine başvurmasına olanak tanır. Örneğin, `Student` sınıfında adlı bir koleksiyon vardır `Enrollments` . `Item.Enrollments`Bu koleksiyonu almak için öğesini kullanabilir ve ardından her öğrencinin kayıtlı kredilerinin toplamını almak Için [LINQ sözdizimini](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) kullanabilirsiniz.
   
3. Öğrenciler. aspx ' i kaydedin.

## <a name="add-code-to-retrieve-data"></a>Verileri almak için kod ekleme

   Öğrenciler. aspx arka plan kod dosyasında, değer için belirtilen yöntemi ekleyin `SelectMethod` . 
   
   1. Students.aspx.cs 'i açın.
   
   2. `using` `ContosoUniversityModelBinding. Models` Ve ad alanları için deyimler ekleyin `System.Data.Entity` .

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. Belirttiğiniz yöntemi ekleyin `SelectMethod` :

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include`Yan tümce sorgu performansını geliştirir, ancak gerekli değildir. `Include`Yan tümcesi olmadan veriler, ilgili verilerin alındığı her seferinde veritabanına ayrı bir sorgu göndermeyi içeren [*yavaş yükleme*](https://en.wikipedia.org/wiki/Lazy_loading)kullanılarak alınır. `Include`Yan tümcesiyle, veriler *Eager yüklemesi*kullanılarak alınır, yani tek bir veritabanı sorgusu ilgili tüm verileri alır. İlgili veriler kullanılmıyorsa, daha fazla veri alındığından Eager yüklemesi daha az verimlidir. Ancak, bu durumda, her bir kayıt için ilgili veriler görüntülendiğinden, Eager yüklemesi size en iyi performansı sağlar.

      İlgili verileri yüklerken performans konuları hakkında daha fazla bilgi için, [ASP.NET MVC uygulamasındaki Entity Framework Ile ilgili verileri okuma](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) bölümünde Ilgili **verileri geç, Eager ve açık yükleme** bölümüne bakın.

      Varsayılan olarak, veriler anahtar olarak işaretlenen özelliğin değerlerine göre sıralanır. `OrderBy`Farklı bir sıralama değeri belirtmek için bir yan tümce ekleyebilirsiniz. Bu örnekte, `StudentID` sıralama için varsayılan özellik kullanılır. [Sıralama, sayfalama ve verileri filtreleme](sorting-paging-and-filtering-data.md) makalesinde, kullanıcı sıralama için bir sütun seçmek üzere etkinleştirilir.
 
   4. Students.aspx.cs Kaydet.

## <a name="run-your-application"></a>Uygulamanızı çalıştırma 

Web uygulamanızı çalıştırın (**F5**) ve aşağıdakiler görüntülenen **öğrenciler** sayfasına gidin:

   ![verileri göster](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>Model bağlama yöntemlerinin otomatik nesli

Bu öğretici serisi ile çalışırken öğreticiden projenize yalnızca kodu kopyalamanız yeterlidir. Ancak, bu yaklaşımın bir dezavantajı, Visual Studio tarafından model bağlama yöntemlerine yönelik kodu otomatik olarak oluşturmak için sunulan özelliği bilmeyebilirsiniz. Kendi projeleriniz üzerinde çalışırken, otomatik kod üretimi size zaman kazandırabilir ve bir işlemin nasıl uygulanacağını anladığınızda size yardımcı olabilir. Bu bölümde otomatik kod oluşturma özelliği açıklanmaktadır. Bu bölüm yalnızca bilgilendirme amaçlıdır ve projenizde uygulamanız gereken herhangi bir kod içermez. 

`SelectMethod`Biçimlendirme kodundaki,, veya özellikleri için bir değer ayarlarken `UpdateMethod` `InsertMethod` `DeleteMethod` **Yeni Yöntem Oluştur** seçeneğini belirleyebilirsiniz.

![Yöntem oluşturma](retrieving-data/_static/image18.png)

Visual Studio, doğru imzayla kodda arka planda bir yöntem oluşturmaz, ancak işlemi gerçekleştirmek için uygulama kodu da oluşturur. İlk `ItemType` olarak özelliği otomatik kod oluşturma özelliğini kullanmadan önce ayarlarsanız, oluşturulan kod işlemler için bu türü kullanır. Örneğin, `UpdateMethod` özelliği ayarlarken aşağıdaki kod otomatik olarak oluşturulur:

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

Yine, bu kodun projenize eklenmesi gerekmez. Sonraki öğreticide, güncelleştirme, silme ve yeni veri ekleme yöntemlerini uygulayacaksınız.

## <a name="summary"></a>Özet

Bu öğreticide, veri modeli sınıfları oluşturdunuz ve bu sınıflardan bir veritabanı oluşturmuş olursunuz. Veritabanı tablolarını test verileriyle doldurmuş olursunuz. Veritabanından veri almak için model bağlama 'yı kullandınız ve sonra verileri bir GridView 'da görüntülen.

Bu serinin sonraki [öğreticide](updating-deleting-and-creating-data.md) , güncelleştirme, silme ve veri oluşturmayı etkinleştireceksiniz.

> [!div class="step-by-step"]
> [Sonraki](updating-deleting-and-creating-data.md)
