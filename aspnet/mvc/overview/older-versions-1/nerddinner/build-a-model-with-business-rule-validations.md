---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: İş Kuralı Doğrulamaları ile Model Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 3, NerdDinner uygulamamız için veritabanını hem sorgulamak hem de güncelleştirmek için kullanabileceğimiz bir modeli nasıl oluşturabileceğimizi gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541643"
---
# <a name="build-a-model-with-business-rule-validations"></a>İş Kuralı Doğrulamaları ile Model Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 3 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 3, NerdDinner uygulamamız için veritabanını hem sorgulamak hem de güncelleştirmek için kullanabileceğimiz bir modeli nasıl oluşturabileceğimizi gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner Adım 3: Model Oluşturma

Model görünümü denetleyicisi çerçevesinde "model" terimi, uygulamanın verilerini temsil eden nesnelerin yanı sıra doğrulama ve iş kurallarını onunla tümleştiren ilgili etki alanı mantığını ifade eder. Model birçok yönden bir MVC tabanlı uygulamanın "kalp" ve daha sonra göreceğiz temelde davranışını sürücüler.

ASP.NET MVC çerçevesi herhangi bir veri erişim teknolojisini kullanarak destekler ve geliştiriciler çeşitli zengin .NET veri seçenekleri arasından aralarında modellerini uygulayabilirler: LINQ'dan Varlıklara, LINQ'dan SQL'e, NHibernate'den SQL'e, NHibernate'den LLBLGen Pro'ya, SubSonic, WilsonORM veya yalnızca ham ADO.NET DataReaders veya DataSets.

NerdDinner uygulamamız için, veritabanı tasarımımıza oldukça yakın ve bazı özel doğrulama mantığı ve iş kuralları ekleyen basit bir model oluşturmak için LINQ'dan SQL'e kullanacağız. Daha sonra, veri kalıcılığı uygulamasının geri kalanından soyut olarak uzak olmasına yardımcı olan ve bunu kolayca birleştirmemizi sağlayan bir depo sınıfı uygulayacağız.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL ,NET 3.5'in bir parçası olarak giden bir ORM 'dur (nesne ilişkisel mapper).

LINQ'dan SQL'e veritabanı tablolarını karşı kodlayabildiğimiz .NET sınıflarına eşlemenin kolay bir yolu sağlar. NerdDinner uygulamamız için veritabanımızdaki Dinners ve RSVP tablolarını Dinner ve RSVP sınıflarına göre haritalamak için kullanacağız. Dinners ve RSVP tablolarının sütunları Akşam Yemeği ve RSVP sınıflarında yer alan özelliklere karşılık gelecektir. Her Akşam Yemeği ve RSVP nesnesi, veritabanındaki Akşam Yemekleri veya RSVP tabloları içinde ayrı bir satırı temsil eder.

LINQ'dan SQL'e, Akşam Yemeği ve RSVP nesnelerini veritabanı verileriyle almak ve güncellemek için SQL deyimlerini el ile oluşturmak zorunda kalmamızı sağlar. Bunun yerine, Akşam Yemeği ve RSVP sınıflarını, veritabanına nasıl eşlediklerini ve aralarındaki ilişkileri tanımlarız. LINQ'dan SQL'e, etkileşimde olduğumuz da ve bunları kullandığımız da çalışma zamanında kullanmak üzere uygun SQL yürütme mantığını oluşturmayı halledecektir.

VB ve C# içindeki LINQ dil desteğini kullanarak Veritabanından Akşam Yemeği ve RSVP nesnelerini alan anlamlı sorgular yazabiliriz. Bu, yazmamız gereken veri kodu miktarını en aza indirir ve gerçekten temiz uygulamalar oluşturmamıza olanak tanır.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Projemize SQL Sınıflarına LINQ Ekleme

Projemizdeki "Modeller" klasörüne sağ tıklayarak başlayacağız ve **Ekle-&gt;Yeni Öğe** menüsü komutunu seçeceğiz:

![](build-a-model-with-business-rule-validations/_static/image1.png)

Bu, "Yeni Öğe Ekle" iletişim kutusunu gündeme getirir. "Veri" kategorisine göre filtre uygulayacağız ve içindeki "LINQ to SQL Classes" şablonuna göre seçeceğiz:

![](build-a-model-with-business-rule-validations/_static/image2.png)

Öğeye "NerdDinner" adını vereceğiz ve "Ekle" düğmesine tıklayacağız. Visual Studio bizim \Models dizininin altına bir NerdDinner.dbml dosyası ekler ve sonra LINQ'u SQL nesnesi ilişkisel tasarımcıya açar:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ ile SQL'e Veri Modeli Sınıfları Oluşturma

LINQ'dan SQL'e, varolan veritabanı şemasından hızlı bir şekilde veri modeli sınıfları oluşturmamızı sağlar. Bunu yapmak için Sunucu Gezgini'nde NerdDinner veritabanını açacağız ve içinde modellemek istediğimiz Tabloları seçeceğiz:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Daha sonra tabloları LINQ'dan SQL tasarımcı yüzeyine sürükleyebiliriz. Bunu yaptığımızda SQL'e LINQ, tabloların şemasını kullanarak (veritabanı tablo sütunlarına eşleyen sınıf özellikleriyle) akşam yemeği ve RSVP sınıflarını otomatik olarak oluşturur:

![](build-a-model-with-business-rule-validations/_static/image5.png)

Varsayılan olarak, BIR veritabanı şemasına dayalı sınıflar oluşturduğunda LINQ -SQL tasarımcısı otomatik olarak tablo ve sütun adlarını "çoğullaştırır". Örneğin: Yukarıdaki örneğimizde yer alan "Akşam Yemekleri" tablosu "Akşam Yemeği" sınıfı ile sonuçlandı. Bu sınıf adlandırma bizim modelleri .NET adlandırma kuralları ile tutarlı hale yardımcı olur ve ben genellikle tasarımcı (özellikle tablolar çok eklerken) bu kadar düzeltmek zorunda bulabilirsiniz. Tasarımcının oluşturduğu bir sınıfın veya özelliğin adını beğenmezseniz, her zaman geçersiz kılınabilir ve istediğiniz ada değiştirebilirsiniz. Bunu, tasarımcı içindeki varlık/özellik adını satır satır düzenleyerek veya özellik ızgarası üzerinden değiştirerek yapabilirsiniz.

Varsayılan olarak LINQ'dan SQL tasarımcısına kadar olan temel anahtar/yabancı anahtar ilişkileri de inceler ve bunlara göre oluşturduğu farklı model sınıfları arasında otomatik olarak varsayılan "ilişki ilişkileri" oluşturulur. Örneğin, Dinners ve RSVP tablolarını LINQ'dan SQL tasarımcısına sürüklediğimizde, rsvp tablosunun Dinners tablosuna yabancı bir anahtarı olduğu gerçeğine dayanarak ikisi arasındaki bire bir ilişki ilişkisi ilişkisi çıkarılarak çıkarıladüzenlenmiştir (bu, tasarımcıdaki okla gösterilir):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Yukarıdaki ilişkilendirme, LINQ'un SQL'e geliştiricilerin belirli bir RSVP ile ilişkili Akşam Yemeği'ne erişmek için kullanabilecekleri RSVP sınıfına güçlü bir şekilde yazılan bir "Akşam Yemeği" özelliği eklemesine neden olur. Ayrıca, Akşam Yemeği sınıfının geliştiricilerin belirli bir Akşam Yemeği ile ilişkili RSVP nesnelerini almasına ve güncelleştirmesine olanak tanıyan bir "RSVP" toplama özelliğine sahip olmasına neden olur.

Aşağıda visual studio içinde yeni bir RSVP nesne oluşturmak ve bir Akşam YEMEĞI RSVPs koleksiyonuna eklemek intellisense bir örnek görebilirsiniz. LINQ'dan SQL'e nasıl otomatik olarak "RSVP" koleksiyonu eklendi:

![](build-a-model-with-business-rule-validations/_static/image7.png)

Dinner'ın RSVPs koleksiyonuna RSVP nesnesini ekleyerek, linq'e SQL'e, Akşam Yemeği ile veritabanımızdaki RSVP satırı arasında yabancı anahtar lı bir ilişkiyi ilişkilendirmelerini söylüyoruz:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Tasarımcının bir tablo ilişkilendirmesini modelleme veya adlarını beğenmezseniz, bunu geçersiz kılabilirsiniz. Tasarımcının içindeki ilişkilendirme okunu tıklattığınızda özelliklerine yeniden adlandırmak, silmek veya değiştirmek için özellik ızgarası üzerinden erişmeniz yeterlidir. NerdDinner uygulamamız için olsa da, varsayılan ilişkilendirme kuralları oluşturmakta olduğumuz veri modeli sınıfları için iyi çalışır ve varsayılan davranışı kullanabiliriz.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext Sınıf

Visual Studio, LINQ'dan SQL tasarımcısına tanımlanan modelleri ve veritabanı ilişkilerini temsil eden .NET sınıflarını otomatik olarak oluşturur. Çözüme eklenen her LINQ-SQL tasarımcı dosyası için bir LINQ-SQL DataContext sınıfı da oluşturulur. LINQ'mizi SQL sınıf öğesine "NerdDinner" olarak adlandırdığımız için oluşturulan DataContext sınıfı "NerdDinnerDataContext" olarak adlandırılacaktır. Bu NerdDinnerDataContext sınıfı, veritabanıyla etkileşim kurmanın birincil yoludur.

NerdDinnerDataContext sınıfımız veritabanında modellediğimiz iki tabloyu temsil eden "Dinners" ve "RSVR" olmak gibi iki özelliği ortaya çıkarır. Akşam Yemeği ve RSVP nesnelerini veritabanından sorgulamak ve almak için bu özelliklere karşı LINQ sorguları yazmak için C# kullanabiliriz.

Aşağıdaki kod, bir NerdDinnerDataContext nesnesinin anlık olarak nasıl anında gerçekleştirildiğini ve gelecekte gerçekleşecek bir Akşam Yemeği dizisi elde etmek için ona karşı bir LINQ sorgusu nasıl gerçekleştirildiğini gösterir. Visual Studio, LINQ sorgusunu yazarken tam bir intellisense sağlar ve ondan döndürülen nesneler güçlü bir şekilde yazılır ve aynı zamanda intellisense'i destekler:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Bir NerdDinnerDataContext, Akşam Yemeği ve RSVP nesnelerini sorgulamamıza izin vermenin yanı sıra, daha sonra aldığımız Akşam Yemeği ve RSVP nesnelerinde yaptığımız değişiklikleri de otomatik olarak izler. Bu işlevi, açık SQL güncelleştirme kodu yazmak zorunda kalmadan değişiklikleri kolayca veritabanına kaydetmek için kullanabiliriz.

Örneğin, aşağıdaki kod, veritabanından tek bir Akşam Yemeği nesnesini almak, Akşam Yemeği özelliklerinden ikisini güncelleştirmek ve değişiklikleri veritabanına kaydetmek için LINQ sorgusunun nasıl kullanılacağını gösterir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Yukarıdaki koddaki NerdDinnerDataContext nesnesi, ondan aldığımız Akşam Yemeği nesnesinde yapılan özellik değişikliklerini otomatik olarak izler. "Değişiklikleri Gönder()" yöntemini adlandırdığımızda, güncelleştirilmiş değerleri geri kalıcı hale getirmek için veritabanına uygun bir SQL "UPDATE" deyimi uygular.

### <a name="creating-a-dinnerrepository-class"></a>DinnerRepository Class oluşturma

Küçük uygulamalar için, Denetleyicilerin doğrudan BIR LINQ'dan SQL DataContext sınıfına karşı çalışması ve Denetleyiciler içinde LINQ sorguları gömmesi bazen iyi olabilir. Uygulamalar büyüdükçe, ancak, bu yaklaşım korumak ve test etmek hantal olur. Aynı zamanda aynı LINQ sorgularını birden çok yerde çoğaltmamıza da yol açabilir.

Uygulamaların korunmasını ve test edilebilen bir yaklaşım, bir "depo" deseni kullanmaktır. Depo sınıfı, veri sorgulama ve kalıcılık mantığını kapsüllemesine yardımcı olur ve veri kalıcılığının uygulama ayrıntılarını uygulamadan soyutlar. Uygulama kodunu daha temiz hale getirmenin yanı sıra, bir depo deseni kullanmak gelecekte veri depolama uygulamalarını değiştirmeyi kolaylaştırabilir ve gerçek bir veritabanı gerektirmeden birim test ini kolaylaştırabilir.

NerdDinner uygulamamız için aşağıdaki imzayı içeren bir DinnerRepository sınıfını tanımlayacağız:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Not: Bu bölümün ilerleyen bölümlerinde bu sınıftan bir IDinnerRepository arabirimi ayıklayacağız ve denetleyicilerimizde bağımlılık enjeksiyonunu mümkün kılacağız. Başlamak için, olsa da, biz basit başlamak ve sadece doğrudan DinnerRepository sınıf ile çalışmak için gidiyoruz.*

Bu sınıfı uygulamak için "Modeller" klasörümüze sağ tıklayıp **&gt;Yeni Öğe Ekle** menüsü komutunu seçeceğiz. "Yeni Öğe Ekle" iletişim kutusunda "Sınıf" şablonunu seçeceğiz ve dosyaya "DinnerRepository.cs" adını vereceğiz:

![](build-a-model-with-business-rule-validations/_static/image10.png)

Daha sonra aşağıdaki kodu kullanarak DinnerRepository sınıf uygulayabilirsiniz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>DinnerRepository sınıfını kullanarak Alma, Güncelleme, Ekleme ve Silme

Şimdi DinnerRepository sınıfımızı oluşturduğumuza göre, onunla yapabileceğimiz ortak görevleri gösteren birkaç kod örneğine bakalım:

#### <a name="querying-examples"></a>Örnekleri Sorgulama

Aşağıdaki kod, DinnerID değerini kullanarak tek bir Akşam Yemeği alır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Aşağıdaki kod, yaklaşan tüm akşam yemeklerini ve döngüleri üzerlerinden alır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Örnekler Ekle ve Güncelleştir

Aşağıdaki kod iki yeni akşam yemeği eklemeyi göstermektedir. Depodaki eklemeler/değişiklikler, "Kaydet()" yöntemi çağrılana kadar veritabanına bağlanmaz. LINQ to SQL bir veritabanı işlemindeki tüm değişiklikleri otomatik olarak sarar – böylece depomuz kaydederken tüm değişiklikler olur veya bunların hiçbiri olmaz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Aşağıdaki kod varolan bir Akşam Yemeği nesnesini alır ve üzerindeki iki özelliği değiştirir. "Kaydet()" yöntemi depomuzda çağrıldığında değişiklikler veritabanına geri kaydedilir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Aşağıdaki kod bir akşam yemeği alır ve sonra bir RSVP ekler. Bunu, LINQ'dan SQL'in bizim için oluşturduğu Dinner nesnesi üzerindeki RSVP koleksiyonunu kullanarak yapar (çünkü veritabanında ikisi arasında birincil anahtar/yabancı anahtar ilişkisi vardır). Bu değişiklik, depoda "Kaydet()" yöntemi çağrıldığında yeni bir RSVP tablosu satırı olarak veritabanına geri kalıcıdır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Örneği Sil

Aşağıdaki kod varolan bir Akşam Yemeği nesnesini alır ve sonra silinecek şekilde işaretler. Depoda "Kaydet()" yöntemi çağrıldığında silmeyi veritabanına geri alacaktır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Doğrulama ve İş Kuralı Mantığını Model Sınıflarıyla Bütünleştirme

Doğrulama ve iş kuralı mantığı tümleştirme veri ile çalışan herhangi bir uygulamanın önemli bir parçasıdır.

#### <a name="schema-validation"></a>Şema Doğrulama

Linq'den SQL tasarımcısına göre model sınıfları tanımlandığında, veri modeli sınıflarında bulunan özelliklerin veri türleri veritabanı tablosunun veri tiplerine karşılık gelir. Örneğin: Akşam Yemekleri tablosundaki "EventDate" sütunu "datetime" ise, LINQ tarafından SQL'e oluşturulan veri modeli sınıfı "DateTime" (yerleşik bir .NET veri tipi) türünden olacaktır. Bu, koddan bir tamsayı veya boolean atamaya çalışırsanız derleme hataları alacağınız ve çalışma zamanında geçersiz bir dize türünü dolaylı olarak dönüştürmeye çalışırsanız otomatik olarak hata çıkaracağı anlamına gelir.

LINQ'dan SQL'e, dizeleri kullanırken sizin için sql değerlerinden kaçan değerleri otomatik olarak işler ve bu da kullanırken SQL enjeksiyon saldırılarına karşı korunmanıza yardımcı olur.

#### <a name="validation-and-business-rule-logic"></a>Doğrulama ve İş Kuralı Mantığı

Şema doğrulama ilk adım olarak yararlıdır, ancak nadiren yeterlidir. Çoğu gerçek dünya senaryosu, birden çok özelliği kapsayabilen, kodu yürütebilen ve genellikle bir modelin durumu hakkında farkında olan daha zengin doğrulama mantığı belirtmeyi gerektirir (örneğin: oluşturuluyor/güncelleniyor/silinmiş veya "arşivlenmiş" gibi etki alanına özgü bir durum içinde mi dir). Doğrulama kurallarını model sınıflarına tanımlamak ve uygulamak için kullanılabilecek çeşitli desenler ve çerçeveler vardır ve bu sınıfa yardımcı olmak için kullanılabilecek birkaç .NET tabanlı çerçeve vardır. ASP.NET MVC uygulamaları içinde hemen hemen herhangi birini kullanabilirsiniz.

NerdDinner uygulamamızın amaçları doğrultusunda, Bir IsValid özelliğini ve Dinner model nesnemizde getruleviolations() yöntemini ortaya çıkardığımız nispeten basit ve düz ileri desen kullanacağız. Geçerli özellik, doğrulama ve iş kurallarının geçerli olup olmadığına bağlı olarak doğru veya yanlış döndürecektir. GetRuleViolations() yöntemi kural hatalarının listesini döndürür.

Projemize "kısmi sınıf" ekleyerek Akşam Yemeği modelimiz için IsValid ve GetRuleViolations() uygulamasını uygulayacağız. Kısmi sınıflar, bir VS tasarımcısı tarafından tutulan sınıflara yöntem/özellik/olay eklemek için kullanılabilir (LINQ'dan SQL tasarımcısına kadar olan Akşam Yemeği sınıfı gibi) ve aracın kodumuzu karıştırmasını önlemeye yardımcı olur. \Modeller klasörüne sağ tıklayarak projemize yeni bir kısmi sınıf ekleyebilir ve ardından "Yeni Öğe Ekle" menüsü komutunu seçebiliriz. Daha sonra "Yeni Öğe Ekle" iletişim kutusundaki "Sınıf" şablonuna yer alabilir ve adını Dinner.cs.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"Ekle" düğmesine tıkladığınızda projemize bir Dinner.cs dosyası eklenir ve IDE içinde açılır. Daha sonra aşağıdaki kodu kullanarak temel bir kural/doğrulama zorlama çerçevesi uygulayabiliriz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Yukarıdaki kod hakkında birkaç notlar:

- Dinner sınıfı "kısmi" bir anahtar kelimeyle önceden ifade edilir – bu da içerdiği kodun LINQ tarafından SQL tasarımcısına oluşturulan/tutulan sınıfla birleştirilip tek bir sınıfa derleneceği anlamına gelir.
- RuleViolation sınıfı, bir kural ihlali hakkında daha fazla ayrıntı sağlamamızı sağlayan projeye ekleyeceğimiz yardımcı sınıftır.
- Dinner.GetRuleViolations() yöntemi doğrulama ve iş kurallarımızın değerlendirilmesine neden olur (bunları kısa süre içinde uygulayacağız). Daha sonra, kural hataları hakkında daha fazla ayrıntı sağlayan bir kural ihlali nesnedizisi döndürür.
- Dinner.IsValid özelliği, Akşam Yemeği nesnesinin etkin Kural Ihlalleri olup olmadığını gösteren kullanışlı bir yardımcı özellik sağlar. Herhangi bir zamanda Dinner nesnesini kullanan bir geliştirici tarafından proaktif olarak denetlenebilir (ve bir özel durum yükseltmez).
- Dinner.OnValidate() kısmi yöntemi, LINQ'dan SQL'e sağladığı ve Akşam Yemeği nesnesinin veritabanında kalıcı olarak devam etmek üzere olduğu her an bize bildirilmesini sağlayan bir kancadır. Yukarıdaki OnValidate() uygulamamız, Akşam Yemeği'nin kaydedilmeden önce Kural Ihlali olmamasını sağlar. Geçersiz bir durumdaysa, linq'in SQL'e işlemi iptal etmesini sağlayacak bir özel durum oluşturur.

Bu yaklaşım, doğrulama ve iş kurallarını entegre edebileceğimiz basit bir çerçeve sağlar. Şimdilik GetRuleViolations() yöntemimize aşağıdaki kuralları ekleyelim:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Herhangi bir Kural Ihlali dizisi döndürmek için C# 'ın "verim getirisi" özelliğini kullanıyoruz. Yukarıdaki ilk altı kural denetimleri sadece bizim Akşam Yemeği üzerinde dize özellikleri null veya boş olamaz zorlamak. Son kural biraz daha ilginçtir ve ContactPhone numarası biçiminin Akşam Yemeği'nin ülkesiyle eşleştiğini doğrulamak için projemize ekleyebileceğimiz bir PhoneValidator.IsValidNumber() yardımcı yöntemini arar.

Biz kullanabilirsiniz. NET'in bu telefon doğrulama desteğini uygulamak için düzenli ifade desteği. Aşağıda, ülkeye özel Regex desen denetimleri eklememizi sağlayan projemize ekleyebileceğimiz basit bir PhoneValidator uygulaması verilmiştir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Kullanım Doğrulama ve İş Mantığı İhlalleri

Artık yukarıdaki doğrulama ve iş kuralı kodunu eklediğimize göre, bir Akşam Yemeği oluşturmaya veya güncellemeye çalıştığımızda, doğrulama mantığı kurallarımız değerlendirilecek ve uygulanacaktır.

Geliştiriciler, akşam yemeği nesnesinin geçerli olup olmadığını proaktif olarak belirlemek için aşağıdaki gibi kod yazabilir ve herhangi bir özel durum çıkarmadan tüm ihlallerin listesini alabilir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Bir Akşam Yemeği'ni geçersiz bir durumda kaydetmeye çalışırsak, DinnerRepository'de Kaydet() yöntemini aradığımız zaman bir özel durum ortaya çıkacaktır. Bunun nedeni, LINQ to SQL'in Dinner.OnValidate() kısmi metodumuzu Akşam Yemeği'nin değişikliklerini kaydetmeden önce otomatik olarak araması ve Akşam Yemeği'nde herhangi bir kural ihlali varsa bir özel durum çıkarmak için Dinner.OnValidate() kodu eklediğimiz için oluşur. Bu özel durumu yakalayabilir ve düzeltmek için ihlallerin bir listesini reaktif olarak alabiliriz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Doğrulama ve iş kurallarımız Kullanıcı Arabirimi katmanımızda değil, model katmanımızda uygulandığından, uygulamamızdaki tüm senaryolarda uygulanacak ve kullanılacaktır. Daha sonra iş kurallarını değiştirebilir veya ekleyebilir ve Dinner nesnelerimizle çalışan tüm kodların onları onurlandırabilir.

Bu değişikliklerin uygulama ve Kullanıcı Yanı mantığı boyunca dalgalanmayaşamadan, iş kurallarını tek bir yerde değiştirme esnekliğine sahip olmak, iyi yazılmış bir uygulamanın ve MVC çerçevesinin teşvik etmeye yardımcı olduğu bir faydanın işaretidir.

### <a name="next-step"></a>Sonraki Adım

Artık veritabanımızı hem sorgulamak hem de güncellemek için kullanabileceğimiz bir modelimiz var.

Şimdi projeye, çevresinde bir HTML UI deneyimi oluşturmak için kullanabileceğimiz bazı denetleyiciler ve görünümler ekleyelim.

> [!div class="step-by-step"]
> [Önceki](create-a-database.md)
> [Sonraki](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
