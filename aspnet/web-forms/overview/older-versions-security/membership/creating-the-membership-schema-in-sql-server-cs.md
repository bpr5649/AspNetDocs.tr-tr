---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: SQL Server üyelik şeması oluşturma (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, SqlMembershipProvider kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar. Bunu izleyerek Wi...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 8160c422d7a20b7c6954f960e73d5d59f7b90a5f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044746"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>SQL Server’da Üyelik Şeması Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> Bu öğretici, SqlMembershipProvider kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar. Bunu izleyerek, şemadaki anahtar tabloları inceleyecek ve amaçlarını ve önemini tartışacağız. Bu öğretici, üyelik çerçevesinin hangi sağlayıcıya kullanması gerektiğini bir ASP.NET uygulamasına nasıl söyleyeceğinizi gösteren bir görünüm ile sonlanır.

## <a name="introduction"></a>Giriş

Web sitesi ziyaretçilerinin tanımlanması için form kimlik doğrulaması kullanılarak incelenen önceki iki öğretici. Forms kimlik doğrulama çerçevesi, geliştiricilerin bir kullanıcıyı bir Web sitesine oturum açmasını ve kimlik doğrulama biletleri aracılığıyla sayfa ziyaretlerinin tamamında hatırlamasını kolaylaştırır. `FormsAuthentication`Sınıfı, Bilet oluşturma ve ziyaretçi tanımlama bilgilerine ekleme yöntemlerini içerir. `FormsAuthenticationModule`Tüm gelen istekleri inceler ve geçerli bir kimlik doğrulama biletine sahip olanlar için `GenericPrincipal` geçerli istek ile bir ve bir nesnesi oluşturur ve ilişkilendirir `FormsIdentity` . Forms kimlik doğrulaması yalnızca bir ziyaretçi için oturum açarken ve sonraki isteklerde, kullanıcının kimliğini belirlemede bu bileti ayrıştırmaya yönelik bir kimlik doğrulama bileti veren bir mekanizmadır. Bir Web uygulamasının Kullanıcı hesaplarını desteklemesi için yine de bir kullanıcı deposu uygulamanız ve kimlik bilgilerini doğrulamak, yeni kullanıcıları kaydettirmek ve Kullanıcı hesabı ile ilgili diğer görevlerin sayısız ' i için işlevsellik eklemeniz gerekir.

ASP.NET 2,0 ' den önce, geliştiriciler Kullanıcı hesabı ile ilgili tüm görevleri uygulamaya yönelik kanca üzerinde vardı. Neyse ki ASP.NET ekibi bu eksiklikleri kabul ederse ve üyelik çerçevesini ASP.NET 2,0 ile kullanıma sunmuştur. Üyelik çerçevesi, ana Kullanıcı hesabı ile ilgili görevleri yerine getirmeye yönelik bir programlama arabirimi sağlayan .NET Framework bir sınıf kümesidir. Bu çerçeve, geliştiricilerin standartlaştırılmış bir API 'ye özelleştirilmiş bir uygulama takmasını sağlayan [Sağlayıcı modeli](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)oluşturulmuştur.

<a id="Tutorial1"></a> [*Güvenlik temelleri ve ASP.NET Destek*](../introduction/security-basics-and-asp-net-support-cs.md) öğreticisinde açıklandığı gibi .NET Framework, iki yerleşik üyelik sağlayıcısıyla birlikte gelir: [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) ve [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) . Adından da anlaşılacağı gibi, `SqlMembershipProvider` Kullanıcı Mağazası olarak bir Microsoft SQL Server veritabanı kullanır. Bu sağlayıcıyı bir uygulamada kullanabilmeniz için sağlayıcıya mağaza olarak hangi veritabanının kullanılacağını söylememiz gerekir. Imagine olabileceğiniz gibi, `SqlMembershipProvider` Kullanıcı Mağazası veritabanının belirli veritabanı tablolarının, görünümlerinin ve saklı yordamların olmasını bekler. Bu beklenen şemayı seçili veritabanına eklememiz gerekiyor.

Bu öğretici, ' i kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar `SqlMembershipProvider` . Bunu izleyerek, şemadaki anahtar tabloları inceleyecek ve amaçlarını ve önemini tartışacağız. Bu öğretici, üyelik çerçevesinin hangi sağlayıcıya kullanması gerektiğini bir ASP.NET uygulamasına nasıl söyleyeceğinizi gösteren bir görünüm ile sonlanır.

Haydi başlayalım!

## <a name="step-1-deciding-where-to-place-the-user-store"></a>1. Adım: Kullanıcı mağazasının yerleştirileceği yere karar verme

Bir ASP.NET uygulamasının verileri genellikle veritabanında bir dizi tabloda depolanır. `SqlMembershipProvider`Veritabanı şemasını uygularken, üyelik şemasının uygulama verileriyle aynı veritabanına mı yoksa alternatif bir veritabanında mı yerleştirileceğini karar vermelidir.

Aşağıdaki nedenlerden dolayı uygulama verileriyle aynı veritabanında üyelik şemasını bulma öneriyorum:

- **Bakımma** ' verileri bir veritabanında kapsüllendiği bir uygulama, iki ayrı veritabanına sahip bir uygulamadan daha kolay anlaşılır, bakım ve dağıtım işlemlerini kolaylaştırır.
- **Ilişkisel bütünlük** ' üyelikle ilgili tabloları uygulama tablolarıyla aynı veritabanında bularak, üyelikle ilgili tablolardaki birincil anahtarlar ve ilgili uygulama tablolarında [yabancı anahtar kısıtlamaları](http://en.wikipedia.org/wiki/Foreign_key) kurmak mümkündür.

Kullanıcı mağazalarının ve uygulama verilerinin ayrı veritabanlarına ayrılması yalnızca, her birinin ayrı veritabanları kullandığı, ancak ortak bir kullanıcı deposu paylaşması gereken birden çok uygulamanız varsa anlamlıdır.

### <a name="creating-a-database"></a>Veritabanı Oluşturma

İkinci öğreticide henüz bir veritabanına ihtiyaç duyulmadığından oluşturmakta olduğumuz uygulama. Ancak, kullanıcı deposu için şimdi bir tane gerekir. Şimdi bir tane oluşturup sağlayıcı için gereken şemayı ekleyin `SqlMembershipProvider` (bkz. 2. adım).

> [!NOTE]
> Bu öğretici serisinin tamamında uygulama tablolarımızı ve şemayı depolamak için bir [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) veritabanı kullanacağız `SqlMembershipProvider` . Bu karar, iki nedenden dolayı yapılmıştır: ilk olarak, maliyet-ücretsiz-Express sürümü, SQL Server 2005 ' in en fazla erişilebilir sürümüdür; İkinci olarak, SQL Server 2005 Express Sürüm veritabanları doğrudan Web uygulamasının `App_Data` klasörüne yerleştirilebilir, bu da veritabanını ve Web uygulamasını BIR ZIP dosyasında birlikte paketleyip, özel kurulum yönergeleri veya yapılandırma seçenekleri olmadan yeniden dağıtmak için bir geçiş yapar. SQL Server Express olmayan bir sürüm sürümünü kullanarak izlemeyi tercih ediyorsanız, ücretsiz olarak kullanabilirsiniz. Adımlar neredeyse aynıdır. `SqlMembershipProvider`Şema Microsoft SQL Server 2000 ve üzerinde herhangi bir sürümle çalışır.

Çözüm Gezgini, klasöre sağ tıklayın `App_Data` ve yeni öğe Ekle ' yi seçin. ( `App_Data` Projenizde bir klasör görmüyorsanız, Çözüm Gezgini projeye sağ tıklayın, ASP.NET klasörü Ekle ve Seç ' i seçin `App_Data` .) Yeni öğe Ekle iletişim kutusunda adlı yeni bir SQL veritabanı eklemeyi seçin `SecurityTutorials.mdf` . Bu öğreticide `SqlMembershipProvider` şemayı bu veritabanına ekleyeceğiz. sonraki öğreticilerde, uygulama verilerimizi yakalamak için ek tablolar oluşturacağız.

[![App_Data klasöre Securityöğreticileri. mdf veritabanı adlı yeni bir SQL veritabanı ekleyin](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**Şekil 1**: klasöre yenı bir SQL veritabanı ekleme `SecurityTutorials.mdf` `App_Data` ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-the-membership-schema-in-sql-server-cs/_static/image3.png))

`App_Data`Klasöre otomatik olarak bir veritabanı eklemek, veritabanı Gezgini görünümünde onu otomatik olarak ekler. (Visual Studio 'nun Express sürümü olmayan sürümünde, Veritabanı Gezgini Sunucu Gezgini olarak adlandırılır.) Veritabanı Gezgini gidin ve hemen eklenen `SecurityTutorials` veritabanını genişletin. Ekranda Veritabanı Gezgini görmüyorsanız, Görünüm menüsüne gidin ve Veritabanı Gezgini ' i seçin veya CTRL + ALT + S tuşlarına basın. Şekil 2 ' de gösterildiği gibi, `SecurityTutorials` veritabanı boştur; hiç tablo yok, hiçbir görünüm ve saklı yordam içermez.

[![Securityöğreticileri veritabanı şu anda boş](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**Şekil 2**: `SecurityTutorials` veritabanı şu anda boş ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-the-membership-schema-in-sql-server-cs/_static/image6.png))

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>2. Adım: `SqlMembershipProvider` Şemayı veritabanına ekleme

, `SqlMembershipProvider` Kullanıcı Mağazası veritabanına yüklenecek belirli bir tablo, görünüm ve saklı yordam kümesi gerektirir. Bu önkoşul veritabanı nesneleri [ `aspnet_regsql.exe` araç](https://msdn.microsoft.com/library/ms229862.aspx)kullanılarak eklenebilir. Bu dosya `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` klasöründe bulunur.

> [!NOTE]
> `aspnet_regsql.exe`Araç hem komut satırı işlevselliği hem de bir grafik kullanıcı arabirimi sunar. Grafik arabirimi daha kolay ve bu öğreticide inceleyeceğiz. Komut satırı arabirimi, `SqlMembershipProvider` derleme betikleri veya otomatikleştirilmiş test senaryolarında olduğu gibi, şemanın eklenmesi gerektiğinde faydalıdır.

`aspnet_regsql.exe`Araç, *ASP.NET uygulama hizmetlerini* belirtilen bir SQL Server veritabanına eklemek veya kaldırmak için kullanılır. ASP.NET uygulama hizmetleri, ve için şemaları, `SqlMembershipProvider` `SqlRoleProvider` diğer ASP.NET 2,0 çerçeveleri IÇIN de SQL tabanlı sağlayıcılara yönelik şemalarla birlikte. Araca iki bit bilgi sağlamamız gerekir `aspnet_regsql.exe` :

- Uygulama hizmetlerini eklemek mi yoksa kaldırmak mı istediğinizi ve
- Uygulama Hizmetleri şemasının ekleneceği veya kaldırılacağı veritabanı

Veritabanının kullanması istenmeden, araç, veritabanının `aspnet_regsql.exe` bulunduğu sunucunun adını, veritabanına bağlanmak için kullanılan güvenlik kimlik bilgilerini ve veritabanı adını sağlamamızı ister. SQL Server Express olmayan sürümünü kullanıyorsanız, bir ASP.NET Web sayfası aracılığıyla veritabanıyla çalışırken bir bağlantı dizesi aracılığıyla sağlamanız gereken bilgilerle aynı olduğundan bu bilgileri zaten bilmelisiniz. Ancak, klasörde bir SQL Server 2005 Express Sürüm veritabanı kullanılırken sunucu ve veritabanı adını belirleme, `App_Data` biraz daha karmaşıktır.

Aşağıdaki bölümde, klasöründeki bir SQL Server 2005 Express Sürüm veritabanı için sunucu ve veritabanı adını belirtmenin kolay bir yolu incelenir `App_Data` . SQL Server 2005 Express Sürüm kullanmıyorsanız Uygulama Hizmetleri bölümünü yüklemeye devam edebilirsiniz.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>Klasördeki bir SQL Server 2005 Express Sürüm veritabanı için sunucu ve veritabanı adını belirleme `App_Data`

Aracı kullanabilmeniz için `aspnet_regsql.exe` sunucu ve veritabanı adlarını bilmemiz gerekir. Sunucu adı `localhost\InstanceName` . Büyük olasılıkla, *InstanceName* `SQLExpress` . Ancak, SQL Server 2005 Express Sürüm el ile yüklediyseniz (yani, Visual Studio 'Yu yüklerken onu otomatik olarak yüklememediyseniz), farklı bir örnek adı seçmiş olmanız mümkündür.

Veritabanı adı, tespit edilecek bir bit kankidır. `App_Data`Klasördeki veritabanları genellikle veritabanı dosyasının yoluyla birlikte [genel olarak benzersiz bir tanımlayıcı](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) içeren bir veritabanı adına sahiptir. Uygulama Hizmetleri şemasını aracılığıyla eklemek için bu veritabanı adını belirlememiz gerekir `aspnet_regsql.exe` .

Veritabanı adını belirlemek için en kolay yol SQL Server Management Studio aracılığıyla incelemektir. SQL Server Management Studio, SQL Server 2005 veritabanlarının yönetilmesine yönelik grafik bir arabirim sağlar, ancak SQL Server 2005 ' nin Express Edition ile birlikte gelmez. İyi haber, SQL Server Management Studio Ücretsiz Express sürümünü [indirebileceğiniz](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) yerdir.

> [!NOTE]
> Masaüstünüzde SQL Server 2005 ' nin Express sürümü olmayan bir sürümüne sahipseniz, Management Studio tam sürümü büyük olasılıkla yüklüdür. Aşağıdaki, Express Edition için aşağıda özetlenen adımları izleyerek veritabanı adını tespit etmek üzere tam sürümü kullanabilirsiniz.

Veritabanı dosyasındaki Visual Studio tarafından uygulanan kilitlerin kapalı olduğundan emin olmak için Visual Studio 'Yu kapatarak başlayın. Sonra, SQL Server Management Studio başlatın ve `localhost\InstanceName` SQL Server 2005 Express sürüm veritabanına bağlanın. Daha önce belirtildiği gibi, örnek adı da olur `SQLExpress` . Kimlik doğrulama seçeneği için Windows kimlik doğrulaması ' nı seçin.

[![SQL Server 2005 Express Sürüm örneğine bağlanma](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**Şekil 3**: SQL Server 2005 Express sürüm örneğine bağlanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image9.png))

SQL Server 2005 Express Sürüm örneğine bağlandıktan sonra, Management Studio veritabanları, güvenlik ayarları, sunucu nesneleri vb. için klasörleri görüntüler. Veritabanları sekmesini genişletirseniz veritabanının `SecurityTutorials.mdf` veritabanı örneğine *kaydedilmediğini* görürsünüz. önce veritabanını iliştirmemiz gerekir.

Veritabanları klasörüne sağ tıklayın ve bağlam menüsünden Ekle ' yi seçin. Bu, veritabanları Ekle iletişim kutusunu görüntüler. Buradan Ekle düğmesine tıklayın, `SecurityTutorials.mdf` veritabanına gidin ve Tamam ' a tıklayın. Şekil 4 ' te, veritabanı seçildikten sonra veritabanlarını Ekle iletişim kutusu gösterilir `SecurityTutorials.mdf` . Şekil 5 ' te, veritabanı başarıyla eklendikten sonra Nesne Gezgini Management Studio gösterilmektedir.

[![Securityöğreticileri. mdf veritabanını ekleyin](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**Şekil 4**: veritabanını iliştirme `SecurityTutorials.mdf` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image12.png))

[![Securityöğreticileri. mdf veritabanı veritabanları klasöründe görüntülenir](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**Şekil 5**: `SecurityTutorials.mdf` veritabanı veritabanları klasöründe görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image15.png))

Şekil 5 ' i gösterdiği gibi, `SecurityTutorials.mdf` veritabanının bir tercih eden abstruse adı vardır. Bunu daha kolay bir şekilde (ve yazmak daha kolay) değiştirelim. Veritabanına sağ tıklayın, bağlam menüsünden Yeniden Adlandır ' ı seçin ve yeniden adlandırın `SecurityTutorialsDatabase` . Bu dosya adını değiştirmez, yalnızca veritabanının kendisini SQL Server için tanımlamak üzere kullandığı adı.

[![Veritabanını SecurityTutorialsDatabase olarak yeniden adlandırma](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**Şekil 6**: veritabanını olarak yeniden adlandırma `SecurityTutorialsDatabase` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))

Bu noktada, veritabanı dosyası için sunucu ve veritabanı adlarını (sırasıyla) biliyoruz `SecurityTutorials.mdf` `localhost\InstanceName` `SecurityTutorialsDatabase` . Artık uygulama hizmetlerini araç aracılığıyla yüklemeye hazırsınız `aspnet_regsql.exe` .

### <a name="installing-the-application-services"></a>Uygulama Hizmetleri yükleme

Aracı başlatmak için `aspnet_regsql.exe` Başlat menüsüne gidin ve Çalıştır ' ı seçin. `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`Metin kutusuna girip Tamam ' a tıklayın. Alternatif olarak, uygun klasöre gitmek ve dosyayı çift tıklamak için Windows Gezgini 'ni kullanabilirsiniz `aspnet_regsql.exe` . Her iki yaklaşım da aynı sonuçlara neden olur.

`aspnet_regsql.exe`Aracı herhangi bir komut satırı bağımsız değişkeni olmadan çalıştırmak, ASP.NET SQL Server Kurulum Sihirbazı grafik kullanıcı arabirimini başlatır. Sihirbaz, ASP.NET uygulama hizmetlerinin belirtilen bir veritabanına eklenmesini veya kaldırılmasını kolaylaştırır. Sihirbazın ilk ekranı, Şekil 7 ' de gösterildiği gibi, aracın amacını açıklamaktadır.

[![Üyelik şeması eklemek için ASP.NET SQL Server Kurulum Sihirbazı 'Nı kullanın](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**Şekil 7**: ASP.NET SQL Server Kurulum Sihirbazı üyelik şemasını eklemek için kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image21.png))

Sihirbazdaki ikinci adım, uygulama hizmetlerini eklemek mi yoksa kaldırmak mı istediğinizi sorar. İçin gereken tabloları, görünümleri ve saklı yordamları eklemek istiyoruz çünkü, `SqlMembershipProvider` uygulama hizmetleri için SQL Server Yapılandır seçeneğini belirleyin. Daha sonra, bu şemayı veritabanınızdan kaldırmak istiyorsanız, bu Sihirbazı yeniden çalıştırın, bunun yerine var olan bir veritabanından uygulama hizmetleri bilgilerini Kaldır seçeneğini belirleyin.

[![Uygulama Hizmetleri için SQL Server Yapılandır seçeneğini belirleyin](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**Şekil 8**: Uygulama Hizmetleri Için SQL Server Yapılandır seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image24.png))

Üçüncü adım veritabanı bilgilerini ister: sunucu adı, kimlik doğrulama bilgileri ve veritabanı adı. Bu öğreticiyle birlikte takip ediyorsanız ve veritabanını ' ye eklemişse, Bu öğreticiye eklediniz `SecurityTutorials.mdf` `App_Data` `localhost\InstanceName` ve olarak yeniden adlandırdıysanız, `SecurityTutorialsDatabase` aşağıdaki değerleri kullanın:

- Server `localhost\InstanceName`
- Windows kimlik doğrulaması
- Veritabanınızı `SecurityTutorialsDatabase`

[![Veritabanı bilgilerini girin](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**Şekil 9**: veritabanı bilgilerini girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image27.png))

Veritabanı bilgilerini girdikten sonra Ileri ' ye tıklayın. Son adım, gerçekleştirilecek adımları özetler. Uygulama hizmetlerini yüklemek için Ileri ' ye tıklayın ve Sihirbazı tamamladıktan sonra işlemi doldurun.

> [!NOTE]
> Veritabanını iliştirmek ve veritabanı dosyasını yeniden adlandırmak için Management Studio kullandıysanız, Visual Studio 'Yu yeniden açmadan önce veritabanını kullanımdan çıkarmayı ve Management Studio kapatmayı unutmayın. Veritabanını ayırmak için `SecurityTutorialsDatabase` veritabanı adına sağ tıklayın ve görevler menüsünde Ayır ' ı seçin.

Sihirbaz tamamlandıktan sonra Visual Studio 'ya dönün ve Veritabanı Gezgini gidin. Tablolar klasörünü genişletin. Adları önekiyle başlayan bir tablo dizisi görmeniz gerekir `aspnet_` . Benzer şekilde, görünümler ve saklı yordamlar klasörlerinin çeşitli görünümleri ve saklı yordamları bulabilirsiniz. Bu veritabanı nesneleri uygulama Hizmetleri şemasını yapar. 3. adımda üyelik ve role özgü veritabanı nesnelerini inceleyeceğiz.

[![Veritabanına çeşitli tablolar, görünümler ve saklı yordamlar eklenmiştir](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**Şekil 10**: veritabanına çeşitli tablolar, görünümler ve saklı yordamlar eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-cs/_static/image30.png))

> [!NOTE]
> `aspnet_regsql.exe`Aracın grafik kullanıcı arabirimi, tüm uygulama Hizmetleri şemasını kurar. Ancak `aspnet_regsql.exe` komut satırından yürütürken, hangi uygulama Hizmetleri bileşenlerinin yükleneceğini (veya kaldırabileceklerini) belirtebilirsiniz. Bu nedenle, ve sağlayıcıları için gereken tabloları, görünümleri ve saklı yordamları eklemek istiyorsanız `SqlMembershipProvider` `SqlRoleProvider` , `aspnet_regsql.exe` komut satırından komutunu çalıştırın. Alternatif olarak, tarafından kullanılan T-SQL oluşturma betikleri 'nin uygun alt kümesini el ile çalıştırabilirsiniz `aspnet_regsql.exe` . Bu betikler,,,, `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` ve gibi adlara sahip klasörde bulunur `InstallCommon.sql` `InstallMembership.sql` `InstallRoles.sql` `InstallProfile.sql` `InstallSqlState.sql` .

Bu noktada, için gereken veritabanı nesnelerini oluşturduk `SqlMembershipProvider` . Bununla birlikte, üyelik çerçevesini `SqlMembershipProvider` (buna karşılık, deyin,) kullanması gerektiğini `ActiveDirectoryMembershipProvider` ve `SqlMembershipProvider` veritabanını kullanması gerektiğini de söylememiz gerekir `SecurityTutorials` . Hangi sağlayıcının kullanılacağını ve 4. adımda seçilen sağlayıcının ayarlarını nasıl özelleştireceğinizi inceleyeceğiz. Ancak ilk olarak, yeni oluşturulan veritabanı nesnelerine daha derin bir göz atalım.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>3. Adım: şemanın temel tablolarına bakış

Bir ASP.NET uygulamasında üyelik ve rol çerçeveleri ile çalışırken, uygulama ayrıntıları sağlayıcı tarafından kapsüllenir. Gelecek öğreticilerde, bu çerçeveleri .NET Framework ve sınıfları aracılığıyla arayüzle göndereceğiz `Membership` `Roles` . Bu üst düzey API 'Leri kullanırken, hangi sorguların yürütüldüğü veya ve tarafından hangi tabloların değiştirildiği gibi alt düzey ayrıntılarla kendimize ilgilenmenize gerek yoktur `SqlMembershipProvider` `SqlRoleProvider` .

Bu şekilde, 1. adımda oluşturulan veritabanı şemasını araştırmadan üyelik ve rol çerçevelerini güvenle kullanabiliriz. Ancak, uygulama verilerini depolamak için tablolar oluştururken, kullanıcılar veya rollerle ilgili varlıklar oluşturmanız gerekebilir. `SqlMembershipProvider` `SqlRoleProvider` Uygulama veri tabloları ve adım 2 ' de oluşturulan tablolar arasında yabancı anahtar kısıtlamaları oluştururken ve şemaları hakkında bir benzerlik sağlanmasına yardımcı olur. Üstelik, bazı nadir durumlarda, Kullanıcı ve rol depolarıyla doğrudan veritabanı düzeyinde Arabirim (veya sınıfları yerine) ile arabirim oluşturmanız gerekebilir `Membership` `Roles` .

### <a name="partitioning-the-user-store-into-applications"></a>Kullanıcı mağazasını uygulamalara bölümleme

Üyelik ve rol çerçeveleri, tek bir Kullanıcı ve rol mağazasının birçok farklı uygulama arasında paylaşılabilmesi için tasarlanmıştır. Üyeliği veya rolleri kullanan bir ASP.NET uygulamasının kullanılacak uygulama bölümünü belirtmesi gerekir. Kısacası, birden çok Web uygulaması aynı kullanıcı ve rol mağazalarını kullanabilir. Şekil 11 ' de üç uygulamada bölümlenen Kullanıcı ve rol depoları gösterilmektedir: HRSite, CustomerSite ve SalesSite. Bu üç Web uygulamasının kendine ait benzersiz kullanıcıları ve rolleri vardır, ancak bunların hepsi, Kullanıcı hesabını ve rol bilgilerini aynı veritabanı tablolarında fiziksel olarak depolar.

[![Kullanıcı hesapları birden çok uygulama arasında bölümlenmiş olabilir](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**Şekil 11**: Kullanıcı hesapları birden çok uygulama arasında bölümlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-the-membership-schema-in-sql-server-cs/_static/image33.png))

`aspnet_Applications`Tablo, bu bölümleri tanımlar. Kullanıcı hesabı bilgilerini depolamak için veritabanını kullanan her uygulama, bu tablodaki bir satırla temsil edilir. `aspnet_Applications`Tabloda dört sütun vardır: `ApplicationId` ,, `ApplicationName` `LoweredApplicationName` , ve `Description` . `ApplicationId` türündedir [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) ve tablonun birincil anahtarıdır; `ApplicationName` her bir uygulama için benzersiz bir insan dostu ad sağlar.

Diğer üyelik ve rolle ilgili tablolar `ApplicationId` içindeki alana geri bağlanır `aspnet_Applications` . Örneğin, `aspnet_Users` her kullanıcı hesabı için bir kayıt içeren tablo, `ApplicationId` yabancı anahtar alanına sahiptir; tablo için Ditto `aspnet_Roles` . `ApplicationId`Bu tablolardaki alan, Kullanıcı hesabının veya rolün ait olduğu uygulama bölümünü belirtir.

### <a name="storing-user-account-information"></a>Kullanıcı hesabı bilgilerini depolama

Kullanıcı hesabı bilgileri iki tabloda barındırıdık: `aspnet_Users` ve `aspnet_Membership` . `aspnet_Users`Tablo, önemli Kullanıcı hesabı bilgilerini tutan alanları içerir. En önemli üç sütun şunlardır:

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` birincil anahtardır (ve türünde `uniqueidentifier` ). `UserName` , `nvarchar(256)` ve parolasıyla birlikte kullanıcının kimlik bilgilerini oluşturur. (Kullanıcının parolası `aspnet_Membership` tabloda depolanır.) `ApplicationId` Kullanıcı hesabını ' de belirli bir uygulamayla bağlantılandırır `aspnet_Applications` . Ve sütunlarında bileşik bir [ `UNIQUE` kısıtlama](https://msdn.microsoft.com/library/ms191166.aspx) vardır `UserName` `ApplicationId` . Bu, belirli bir uygulamada her kullanıcı adının benzersiz olmasını, ancak aynı `UserName` şekilde farklı uygulamalarda kullanılmasına izin verilmesini sağlar.

`aspnet_Membership`Tablo, kullanıcının parolası, e-posta adresi, son oturum açma tarihi ve saati gibi ek kullanıcı hesabı bilgilerini içerir ve bu şekilde devam eder. Ve tablolarındaki kayıtlar arasında bire bir yazışmalar vardır `aspnet_Users` `aspnet_Membership` . Bu ilişki `UserId` , ' deki alanı tarafından `aspnet_Membership` , tablonun birincil anahtarı olarak işlev gören bir değer tarafından sağlanır. Tablo gibi `aspnet_Users` , `aspnet_Membership` `ApplicationId` Bu bilgileri belirli bir uygulama bölümüne bağlayan bir alan içerir.

### <a name="securing-passwords"></a>Parolaların güvenliğini sağlama

Parola bilgileri `aspnet_Membership` tabloda depolanır. , `SqlMembershipProvider` Aşağıdaki üç teknikten biri kullanılarak parolaların veritabanında depolanmasını sağlar:

- **Temizle** -parola veritabanında düz metin olarak depolanır. Bu seçeneği kullanmayı kesinlikle önleyin. Veritabanı tehlikeye atılırsa, veritabanı erişimi olan bir arka kapı veya disgruntled çalışanı bulan bir bilgisayar korsanının olması-her tek kullanıcının kimlik bilgileri almak için orada bulunur.
- **Karma hale getirilmiş** parolalar tek yönlü bir karma algoritması ve rastgele oluşturulmuş bir anahtar değeri kullanılarak karma hale getirilir. Bu karma değer (güvenlik ile birlikte) veritabanında depolanır.
- **Şifrelenmiş** -parolanın şifrelenmiş bir sürümü veritabanında depolanır.

Kullanılan parola depolama tekniği, `SqlMembershipProvider` içinde belirtilen ayarlara bağlıdır `Web.config` . `SqlMembershipProvider`4. adımdaki ayarları özelleştirmeye bakacağız. Varsayılan davranış parolanın karmasını deposıdır.

Parolanın depolanmasından sorumlu sütunlar `Password` , ve ' dir `PasswordFormat` `PasswordSalt` . `PasswordFormat``int`değeri, parolayı depolamak için kullanılan tekniği belirten bir tür alanıdır: Clear için 0; karma için 1, şifreli için 2. `PasswordSalt` kullanılan parola depolama tekniğinden bağımsız olarak rastgele oluşturulmuş bir dize atanır; değeri `PasswordSalt` yalnızca parolanın karması hesaplanırken kullanılır. Son olarak, `Password` sütunda gerçek parola verileri, düz metin parola, Parola karması veya şifrelenmiş parola bulunur.

Tablo 1, parolayı saklarken çeşitli depolama teknikleri için bu üç sütunun nasıl görünebileceğini gösterir! .

| **Depolama tekniği &lt; \_ o3a \_ p/&gt;** | **Parola &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **Passwordanahtar &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Temizle | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| Haline | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| Şifreli | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/AA/oqAXGLHJNBw = = |

**Tablo 1**: parolayı saklarken parola Ile ilgili alanlar Için örnek değerler MySecret!

> [!NOTE]
> Tarafından kullanılan özel şifreleme veya karma algoritması, `SqlMembershipProvider` öğesindeki ayarlara göre belirlenir `<machineKey>` . Bu yapılandırma öğesi, <a id="Tutorial3"></a> [*Forms kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) öğreticisinin 3. adımında anlatıldık.

### <a name="storing-roles-and-role-associations"></a>Rolleri ve rol Ilişkilendirmelerini depolama

Rol çerçevesi, geliştiricilerin bir rol kümesi tanımlamasına ve hangi kullanıcıların hangi rollere ait olduğunu belirlemesine izin verir. Bu bilgiler veritabanında iki tablo aracılığıyla yakalanır: `aspnet_Roles` ve `aspnet_UsersInRoles` . Tablodaki her kayıt, `aspnet_Roles` belirli bir uygulama için bir rolü temsil eder. Tabloya benzer şekilde `aspnet_Users` , `aspnet_Roles` tabloda Tartışmayla ilgili üç sütun vardır:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` birincil anahtardır (ve türünde `uniqueidentifier` ). `RoleName` türündedir `nvarchar(256)` . Ve `ApplicationId` Kullanıcı hesabını ' de belirli bir uygulamayla bağlantılandırır `aspnet_Applications` . `UNIQUE` `RoleName` Ve `ApplicationId` sütunlarında, belirli bir uygulamada her bir rol adının benzersiz olmasını sağlayan bir bileşik kısıtlama vardır.

`aspnet_UsersInRoles`Tablo, kullanıcılar ve roller arasında bir eşleme görevi görür. Yalnızca iki sütun vardır ve `UserId` `RoleId` bir bileşik birincil anahtar oluşturun.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>4. Adım: sağlayıcıyı belirtme ve ayarlarını özelleştirme

Üyelik ve rol çerçeveleri gibi sağlayıcı modelini destekleyen tüm çerçeveler-uygulama ayrıntılarının olmaması ve bunun yerine bu sorumluluğu bir sağlayıcı sınıfına devretmek. Üyelik çerçevesi söz konusu olduğunda, `Membership` sınıfı kullanıcı hesaplarını yönetmek IÇIN API 'yi tanımlar, ancak herhangi bir Kullanıcı deposuyla doğrudan etkileşime almaz. Bunun yerine, `Membership` sınıfının yöntemleri, yapılandırılan sağlayıcıya yönelik istekleri devre dışı bırakır `SqlMembershipProvider` . Sınıftaki yöntemlerden birini çağırdığımızda `Membership` , üyelik çerçevesi ' ne çağrıyı devretmek için nasıl bilir `SqlMembershipProvider` ?

`Membership`Sınıfı, üyelik çerçevesi tarafından kullanılabilecek tüm kayıtlı sağlayıcı sınıflarının başvurusunu içeren bir [ `Providers` özelliğe](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) sahiptir. Kayıtlı her sağlayıcının ilişkili bir adı ve türü vardır. Ad, `Providers` sağlayıcı sınıfını tanımladığından, koleksiyonda belirli bir sağlayıcıya başvurmak için kolay bir yol sunar. Üstelik, her kayıtlı sağlayıcı yapılandırma ayarlarını içerebilir. Üyelik çerçevesi için yapılandırma ayarları `passwordFormat` `requiresUniqueEmail` , diğer birçok, ve arasında bulunur. Tarafından kullanılan yapılandırma ayarlarının tüm listesi için bkz. Tablo 2 `SqlMembershipProvider` .

`Providers`Özelliğin içeriği, Web uygulamasının yapılandırma ayarları aracılığıyla belirtilir. Varsayılan olarak, tüm Web uygulamalarının türünde adlı bir sağlayıcısı vardır `AspNetSqlMembershipProvider` `SqlMembershipProvider` . Bu varsayılan üyelik sağlayıcısı ' de kaydedilir `machine.config` (şurada bulunur `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)` :

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

Yukarıdaki biçimlendirme gösterildiği gibi, [ `<membership>` öğesi](https://msdn.microsoft.com/library/1b9hw62f.aspx) , [ `<providers>` alt öğe](https://msdn.microsoft.com/library/6d4936ht.aspx) kayıtlı sağlayıcıları belirttiğinde üyelik çerçevesinin yapılandırma ayarlarını tanımlar. Sağlayıcılar veya öğeleri kullanılarak eklenebilir veya kaldırılabilir [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) ; [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) Şu anda kayıtlı olan tüm sağlayıcıları kaldırmak için öğesini kullanın. Yukarıdaki biçimlendirme gösterildiği gibi, `machine.config` türünde adlı bir sağlayıcı ekler `AspNetSqlMembershipProvider` `SqlMembershipProvider` .

Ve özniteliklerine ek olarak `name` `type` öğesi, `<add>` çeşitli yapılandırma ayarlarının değerlerini tanımlayan öznitelikler içerir. Tablo 2 `SqlMembershipProvider` , kullanılabilir yapılandırma ayarlarını, her birinin açıklamasıyla birlikte listeler.

> [!NOTE]
> Tablo 2 ' de belirtilen varsayılan değerler, sınıfında tanımlanan varsayılan değerlere başvurur `SqlMembershipProvider` . İçindeki yapılandırma ayarlarının tümünün, `AspNetSqlMembershipProvider` sınıfının varsayılan değerlerine karşılık geldiğini unutmayın `SqlMembershipProvider` . Örneğin, bir üyelik sağlayıcısında belirtilmemişse, `requiresUniqueEmail` ayar varsayılan olarak true değerini alır. Ancak, `AspNetSqlMembershipProvider` açıkça bir değeri belirterek bu varsayılan değeri geçersiz kılar `false` .

| **&lt; \_ O3a \_ p/ayarlama&gt;** | **Açıklama &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | Üyelik çerçevesinin, tek bir Kullanıcı deposunun birden çok uygulama arasında bölümlenmesi için izin verdiğini hatırlayın. Bu ayar, üyelik sağlayıcısı tarafından kullanılan uygulama bölümünün adını gösterir. Bu değer açıkça belirtilmemişse, çalışma zamanında, uygulamanın sanal kök yolu değerine ayarlanır. |
| `commandTimeout` | SQL komut zaman aşımı değerini (saniye cinsinden) belirtir. Varsayılan değer 30’dur. |
| `connectionStringName` | `<connectionStrings>`Kullanıcı deposu veritabanına bağlanmak için kullanılacak öğedeki bağlantı dizesinin adı. Bu değer gereklidir. |
| `description` | Kayıtlı sağlayıcının insanın kolay bir açıklamasını sağlar. |
| `enablePasswordRetrieval` | Kullanıcıların unutulan parolalarını alıp almamadığını belirtir. Varsayılan değer: `false`. |
| `enablePasswordReset` | Kullanıcıların parolalarını sıfırlamasına izin verilip verilmeyeceğini belirtir. Varsayılan olarak olur `true` . |
| `maxInvalidPasswordAttempts` | Kullanıcı kilitlenmesinden önce belirtilen kullanıcı için ortaya çıkabilecek başarısız oturum açma girişimi sayısı üst sınırı `passwordAttemptWindow` . Varsayılan değer 5 ' tir. |
| `minRequiredNonalphanumericCharacters` | Kullanıcı parolada görünmesi gereken en az alfasayısal olmayan karakter sayısı. Bu değer 0 ile 128 arasında olmalıdır; Varsayılan değer 1 ' dir. |
| `minRequiredPasswordLength` | Bir parolada gereken en az karakter sayısı. Bu değer 0 ile 128 arasında olmalıdır; Varsayılan değer 7 ' dir. |
| `name` | Kayıtlı sağlayıcının adı. Bu değer gereklidir. |
| `passwordAttemptWindow` | Başarısız oturum açma girişimlerinin izlendiği dakika sayısı. Bir Kullanıcı belirtilen bu pencerede geçersiz oturum açma kimlik bilgileri `maxInvalidPasswordAttempts` süreleri sağlarsa, bunlar kilitlenir. Varsayılan değer 10 ' dur. |
| `PasswordFormat` | Parola depolama biçimi: `Clear` , `Hashed` , veya `Encrypted` . Varsayılan değer: `Hashed`. |
| `passwordStrengthRegularExpression` | Sağlanmışsa, bu normal ifade, yeni bir hesap oluştururken veya parolalarını değiştirirken kullanıcının seçili parolasının gücünü değerlendirmek için kullanılır. Varsayılan değer boş bir dizedir. |
| `requiresQuestionAndAnswer` | Kullanıcının parolasını alırken veya sıfırlarken güvenlik sorusuna yanıt vermesi gerekip gerekmediğini belirtir. Varsayılan değer: `true`. |
| `requiresUniqueEmail` | Belirli bir uygulama bölümündeki tüm Kullanıcı hesaplarının benzersiz bir e-posta adresine sahip olup olmadığını gösterir. Varsayılan değer: `true`. |
| `type` | Sağlayıcının türünü belirtir. Bu değer gereklidir. |

**Tablo 2**: Üyelik ve `SqlMembershipProvider` yapılandırma ayarları

Buna ek olarak `AspNetSqlMembershipProvider` , diğer üyelik sağlayıcıları, dosyaya benzer biçimlendirme eklenerek uygulama temelinde da kaydedilebilir `Web.config` .

> [!NOTE]
> Rol çerçevesi çok aynı şekilde çalışıyor: ' de varsayılan bir kayıtlı rol sağlayıcısı vardır `machine.config` ve kayıtlı sağlayıcılar ' de uygulama temelinde bir uygulamayla özelleştirilebilir `Web.config` . Daha sonraki bir öğreticide, roller çerçevesini ve yapılandırma işaretlemesini ayrıntılı olarak inceleyeceğiz.

### <a name="customizing-thesqlmembershipprovidersettings"></a>Ayarları özelleştirme `SqlMembershipProvider`

Default `SqlMembershipProvider` ( `AspNetSqlMembershipProvider` ) `connectionStringName` özniteliği olarak ayarlanır `LocalSqlServer` . Sağlayıcı gibi `AspNetSqlMembershipProvider` , bağlantı dizesi adı da `LocalSqlServer` tanımlanmıştır `machine.config` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

Görebileceğiniz gibi, bu bağlantı dizesi | konumunda bulunan bir SQL 2005 Express Edition veritabanını tanımlar. DataDirectory | aspnetdb. mdf '. Dize | Veri dizini | çalışma zamanında, dizine işaret etmek için çevrilir `~/App_Data/` , bu nedenle veritabanı yolu | DataDirectory | aspnetdb. mdf "öğesine çevrilir `~/App_Data` / `aspnet.mdf` .

Uygulama dosyasında herhangi bir üyelik sağlayıcısı bilgisi belirtmediyseniz, `Web.config` uygulama varsayılan kayıtlı üyelik sağlayıcısını kullanır `AspNetSqlMembershipProvider` . `~/App_Data/aspnet.mdf`Veritabanı yoksa, ASP.NET çalışma zamanı otomatik olarak oluşturulur ve uygulama Hizmetleri şemasını ekler. Ancak, veritabanını kullanmak istememiz gerekmez `aspnet.mdf` ; bunun yerine `SecurityTutorials.mdf` 2. adımda oluşturduğumuz veritabanını kullanmak istiyoruz. Bu değişiklik, iki şekilde gerçekleştirilebilir:

- İçin bir değer <strong>belirtin</strong> <strong>`LocalSqlServer`</strong> içindeki bağlantı dizesi <strong>adı</strong> <strong>`Web.config`</strong> <strong>.</strong> `LocalSqlServer`İçindeki bağlantı dizesi adı değerinin üzerine yazarak `Web.config` , varsayılan kayıtlı üyelik sağlayıcısını ( `AspNetSqlMembershipProvider` ) kullanabilir ve veritabanıyla doğru bir şekilde çalışmasını sağlayabilirsiniz `SecurityTutorials.mdf` . Bu yaklaşım, tarafından belirtilen yapılandırma ayarlarıyla içeriğiniz varsa uygundur `AspNetSqlMembershipProvider` . Bu teknik hakkında daha fazla bilgi için bkz. [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog gönderisi, [SQL Server 2000 veya SQL Server 2005 kullanmak için ASP.NET 2,0 uygulama hizmetleri yapılandırma](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>Yeni bir kayıtlı sağlayıcı türü ekleyin</strong> <strong>`SqlMembershipProvider`</strong> <strong>ve yapılandırma</strong> <strong>`connectionStringName`</strong> öğesine işaret eden <strong>ayar</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>veritabanı.</strong> Bu yaklaşım, veritabanı bağlantı dizesine ek olarak diğer yapılandırma özelliklerini özelleştirmek istediğiniz senaryolarda yararlıdır. Kendi projelerimde bu yaklaşımı esneklik ve okunabilirlik nedeniyle her zaman kullandım.

Veritabanına başvuran yeni bir kayıtlı sağlayıcı ekleyebilmek `SecurityTutorials.mdf` için önce içindeki bölümüne uygun bir bağlantı dizesi değeri eklememiz gerekir `<connectionStrings>` `Web.config` . Aşağıdaki biçimlendirme, `SecurityTutorialsConnectionString` klasöründeki SQL Server 2005 Express sürüm veritabanına başvuran adlı yeni bir bağlantı dizesi ekler `SecurityTutorials.mdf` `App_Data` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> Alternatif bir veritabanı dosyası kullanıyorsanız, bağlantı dizesini gerektiği şekilde güncelleştirin. Doğru bağlantı dizesinin nasıl oluşabileceği hakkında daha fazla bilgi için bkz. [connectionStrings.com](http://www.connectionstrings.com/).

Ardından, aşağıdaki Üyelik yapılandırma işaretlemesini `Web.config` dosyaya ekleyin. Bu biçimlendirme adlı yeni bir sağlayıcı kaydeder `SecurityTutorialsSqlMembershipProvider` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

Sağlayıcıyı kaydetmenin yanı sıra, `SecurityTutorialsSqlMembershipProvider` Yukarıdaki biçimlendirme `SecurityTutorialsSqlMembershipProvider` varsayılan sağlayıcıyı ( `defaultProvider` öğesindeki özniteliği aracılığıyla `<membership>` ) tanımlar. Üyelik çerçevesinin birden çok kayıtlı sağlayıcısı olabilir. , `AspNetSqlMembershipProvider` İçinde ilk sağlayıcı olarak kaydedildiğinden `machine.config` , aksini belirtmediğiniz sürece varsayılan sağlayıcı olarak görev yapar.

Şu anda uygulamamız iki kayıtlı sağlayıcıya sahiptir: `AspNetSqlMembershipProvider` ve `SecurityTutorialsSqlMembershipProvider` . Ancak, `SecurityTutorialsSqlMembershipProvider` sağlayıcıyı kaydetmeden önce, öğesinden hemen önce bir [ `<clear />` öğe](https://msdn.microsoft.com/library/t062y6yc.aspx) ekleyerek daha önce kayıtlı olan tüm sağlayıcıları temizlemiş olabilir `<add>` . Bu, `AspNetSqlMembershipProvider` kayıtlı sağlayıcılar listesinden, yani `SecurityTutorialsSqlMembershipProvider` yalnızca kayıtlı üyelik sağlayıcısı olacak şekilde Temizlenebileceği anlamına gelir. Bu yaklaşımı kullandığımızda, `SecurityTutorialsSqlMembershipProvider` kayıtlı tek üyelik sağlayıcısı olduğundan, varsayılan sağlayıcı olarak işaretlemenize gerek kalmaz. Kullanma hakkında daha fazla bilgi için `<clear />` bkz [. `<clear />` sağlayıcılar eklenirken kullanma](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx).

`SecurityTutorialsSqlMembershipProvider`Öğesinin `connectionStringName` ayarının `SecurityTutorialsConnectionString` , tam olarak eklenen bağlantı dizesi adına Başvurdığına ve `applicationName` ayarının securityöğreticiler değeri olarak ayarlandığını unutmayın. Ayrıca, `requiresUniqueEmail` ayar olarak ayarlanmıştır `true` . Diğer tüm yapılandırma seçenekleri, içindeki değerlerle aynıdır `AspNetSqlMembershipProvider` . İsterseniz, burada herhangi bir yapılandırma değişikliği yapabilirsiniz. Örneğin, bir tane yerine iki alfasayısal olmayan karakter gerektirerek veya parola uzunluğunu yedi yerine sekiz karakter ile artırarak parola gücünü güçleyerek artırabilirsiniz.

> [!NOTE]
> Üyelik çerçevesinin, tek bir Kullanıcı deposunun birden çok uygulama arasında bölümlenmesi için izin verdiğini hatırlayın. Üyelik sağlayıcısının ayarı, `applicationName` sağlayıcının kullanıcı deposuyla çalışırken hangi uygulamayı kullanacağını gösterir. Açıkça ayarlanmamışsa, bir yapılandırma ayarı için bir değer ayarlamanız önemlidir `applicationName` , çünkü açık bir şekilde `applicationName` ayarlanmamışsa, çalışma zamanında Web uygulamasının sanal kök yoluna atanır. Bu, uygulamanın sanal kök yolu değişmeyeceği ve uygulamayı farklı bir yola taşıdığınız sürece bu kadar iyi çalışır `applicationName` . Bu durumda, üyelik sağlayıcısı daha önce kullanılandan farklı bir uygulama bölümüyle çalışmaya başlayacaktır. Taşıma işleminden önce oluşturulan kullanıcı hesapları farklı bir uygulama bölümünde kalacak ve bu kullanıcılar artık sitede oturum açamaz. Bu konuyla ilgili daha ayrıntılı bir tartışma için bkz. [ `applicationName` ASP.NET 2,0 üyeliğini ve diğer sağlayıcıları yapılandırırken her zaman özelliği ayarla](https://weblogs.asp.net/scottgu/443634).

## <a name="summary"></a>Özet

Bu noktada, yapılandırılmış uygulama hizmetleri () ile bir veritabanı vardır `SecurityTutorials.mdf` ve üyelik çerçevesinin yeni Kaydolduğumuz sağlayıcıyı kullanması için Web uygulamamızı yapılandırdık `SecurityTutorialsSqlMembershipProvider` . Bu kayıtlı sağlayıcı türündedir `SqlMembershipProvider` ve `connectionStringName` uygun bağlantı dizesi ( `SecurityTutorialsConnectionString` ) ve `applicationName` değeri açıkça ayarlanmış olarak ayarlanır.

Artık uygulamamızda üyelik çerçevesini kullanmaya hazırsınız. Sonraki öğreticide, Yeni Kullanıcı hesapları oluşturmayı inceleyeceğiz. Aşağıdaki, Kullanıcı tabanlı yetkilendirme gerçekleştirerek ve Kullanıcı ile ilgili ek bilgileri veritabanında depolarız.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [`applicationName`ASP.NET 2,0 üyeliğini ve diğer sağlayıcıları yapılandırırken her zaman özelliği ayarlayın](https://weblogs.asp.net/scottgu/443634)
- [SQL Server 2000 veya SQL Server 2005 kullanmak için ASP.NET 2,0 Uygulama Hizmetleri yapılandırma](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [SQL Server Management Studio Express Edition 'ı indirin](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>`Üyelik sağlayıcıları için öğesi](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>`Öğe](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>`Üyelik öğesi](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [`<clear />`Sağlayıcılar eklenirken kullanma](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [Doğrudan ile çalışma `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Bu öğreticide bulunan konularda video eğitimi

- [ASP.NET Üyeliklerini Anlama](../../../videos/authentication/understanding-aspnet-memberships.md)
- [SQL’yi Üyelik Şemalarıyla Çalışacak Biçimde Yapılandırma](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [Varsayılan Üyelik Şemasında Üyelik Ayarlarını Değiştirme](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott, [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) konumundaki blogundan veya üzerinden erişilebilir [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Alicja Maziarz. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, bana bir satır bırakın [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [Sonraki](creating-user-accounts-cs.md)
