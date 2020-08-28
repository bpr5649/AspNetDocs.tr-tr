---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: Yönetilen kod ile saklı yordamlar ve Kullanıcı tanımlı Işlevler oluşturma (C#) | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005, geliştiricilerin yönetilen kod aracılığıyla veritabanı nesneleri oluşturmalarına olanak tanımak için .NET ortak dil çalışma zamanına tümleştirilir. Bu öğretici...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c1882d019d9dfde2dc4f960cae65aa8268c97a51
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045305"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>Yönetilen Kod ile Saklı Yordamlar ve Kullanıcı Tanımlı İşlevler Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) veya [PDF 'yi indirin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005, geliştiricilerin yönetilen kod aracılığıyla veritabanı nesneleri oluşturmalarına olanak tanımak için .NET ortak dil çalışma zamanına tümleştirilir. Bu öğreticide, Visual Basic veya C# kodunuzla yönetilen saklı yordamların ve yönetilen Kullanıcı tanımlı işlevlerin nasıl oluşturulacağı gösterilmektedir. Ayrıca, Visual Studio 'nun bu sürümlerinin bu tür yönetilen veritabanı nesnelerinin hatalarını ayıklamanıza nasıl izin veririz.

## <a name="introduction"></a>Giriş

Microsoft s SQL Server 2005 gibi veritabanları veri ekleme, değiştirme ve alma için [Transact-yapılandırılmış sorgu dili (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) kullanır. Çoğu veritabanı sisteminde, daha sonra tek, yeniden kullanılabilir bir birim olarak yürütülebilecek bir dizi SQL deyimini gruplandırmak için yapılar bulunur. Saklı yordamlar bir örnektir. Diğer bir deyişle, adım 9 ' da daha ayrıntılı olarak inceleyeceği bir yapı olan *Kullanıcı tanımlı işlevler*(UDF 'ler).

SQL, temel olarak veri kümeleriyle çalışmak üzere tasarlanmıştır. `SELECT`, `UPDATE` , Ve `DELETE` deyimleri, karşılık gelen tablodaki tüm kayıtlar için geçerlidir ve yalnızca `WHERE` yan tümceleriyle sınırlandırılır. Ancak, tek seferde bir kayıt ile çalışmak ve skaler verileri değiştirmek için tasarlanan birçok dil özelliği vardır. [ `CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) bir kayıt kümesinin tek seferde bir kez döngüye eklenmesine izin verir. , Ve gibi dize işleme işlevleri, `LEFT` `CHARINDEX` ve `PATINDEX` skaler verilerle çalışır. SQL Ayrıca ve gibi denetim akışı deyimlerini `IF` içerir `WHILE` .

Microsoft SQL Server 2005 ' den önce, saklı yordamlar ve UDF 'ler yalnızca bir T-SQL deyimleri koleksiyonu olarak tanımlanabilir. Ancak, SQL Server 2005, tüm .NET derlemeleri tarafından kullanılan çalışma zamanı olan [ortak dil çalışma zamanı (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)ile tümleştirme sağlamak üzere tasarlanmıştır. Sonuç olarak, bir SQL Server 2005 veritabanındaki saklı yordamlar ve UDF 'ler, yönetilen kod kullanılarak oluşturulabilir. Diğer bir deyişle, bir C# sınıfında bir yöntem olarak bir saklı yordam veya UDF oluşturabilirsiniz. Bu, bu saklı yordamların ve UDF 'ların .NET Framework ve kendi özel sınıflarınızda işlevselliği kullanmasına olanak sağlar.

Bu öğreticide, yönetilen saklı yordamlar ve Kullanıcı tanımlı Işlevler oluşturmayı ve bunları Northwind veritabanımızla nasıl tümleştirileceğini inceleyeceğiz. Haydi başlayın!

> [!NOTE]
> Yönetilen veritabanı nesneleri, SQL karşılıkları üzerinde bazı avantajlar sunar. Dil zenginliği ve açıklık ve mevcut kodu ve mantığı yeniden kullanma olanağı ana avantajlardır. Ancak, yönetilen veritabanı nesnelerinin çok yordamsal mantığı içermeyen veri kümeleriyle çalışırken daha az verimli olması olasıdır. Yönetilen kod kullanmanın avantajları hakkında daha kapsamlı bir tartışma için, [veritabanı nesneleri oluşturmak üzere yönetilen kod kullanmanın avantajlarını](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)inceleyin.

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>1. Adım: Northwind veritabanını taşıma`App_Data`

Bu nedenle tüm öğreticilerimiz, Web uygulaması s klasöründe bir Microsoft SQL Server 2005 Express Edition veritabanı dosyası kullandık `App_Data` . Veritabanını `App_Data` basit bir biçimde dağıtmak ve çalıştırmak, tüm dosyalar bir dizinde bulunduğundan ve öğreticiyi test etmek için başka bir yapılandırma adımı gerekmediği için Bu öğreticilerin basitleştirilmesi ve çalıştırılması.

Bununla birlikte, bu öğretici için Northwind veritabanını ' dan dışarı taşıyıp `App_Data` SQL Server 2005 Express sürüm veritabanı örneğiyle birlikte doğrudan kaydetlim. Bu öğreticide, klasöründeki veritabanıyla ilgili adımları gerçekleştirebilmemiz de `App_Data` , veritabanını SQL Server 2005 Express sürüm veritabanı örneğiyle açıkça kaydederek birçok adım daha basit hale getirilir.

Bu öğreticinin indirilmesi, iki veritabanı dosyasına sahiptir `NORTHWND.MDF` ve `NORTHWND_log.LDF` adlı bir klasöre yerleştirilir `DataFiles` . Kendi öğreticilerinin uygulanınızla birlikte takip ediyorsanız, Visual Studio 'Yu kapatın ve `NORTHWND.MDF` ve `NORTHWND_log.LDF` dosyalarını web sitesi `App_Data` klasöründeki Web sitesi dışındaki bir klasöre taşıyın. Veritabanı dosyaları başka bir klasöre taşındıktan sonra Northwind veritabanını SQL Server 2005 Express Sürüm veritabanı örneğiyle kaydetmeniz gerekir. Bu, SQL Server Management Studio yapılabilir. Bilgisayarınızda SQL Server 2005 ' nin Express olmayan bir sürümüne sahipseniz, büyük olasılıkla Management Studio zaten yüklü. Bilgisayarınızda yalnızca SQL Server 2005 Express Sürüm varsa [Microsoft SQL Server Management Studio Express 'i](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)indirip yüklemek için biraz zaman ayırın.

SQL Server Management Studio'yu başlatın. Şekil 1 ' de gösterildiği gibi, Management Studio sunucuya hangi sunucudan bağlanılacağını sorar. Sunucu adı için localhost\SQLExpress girin, kimlik doğrulaması açılır listesinden Windows kimlik doğrulaması ' nı seçin ve Bağlan ' a tıklayın.

![Uygun veritabanı örneğine bağlanma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**Şekil 1**: uygun veritabanı örneğine bağlanma

Bağlandıktan sonra, Nesne Gezgini penceresinde veritabanları, güvenlik bilgileri, yönetim seçenekleri gibi SQL Server 2005 Express Sürüm veritabanı örneğiyle ilgili bilgiler listelenir.

Northwind veritabanını `DataFiles` klasöre (veya taşıdığınız yere) SQL Server 2005 Express sürüm veritabanı örneğine iliştirmemiz gerekir. Veritabanları klasörüne sağ tıklayın ve bağlam menüsünden Ekle seçeneğini belirleyin. Bu işlem veritabanlarını Ekle iletişim kutusunu getirir. Ekle düğmesine tıklayın, uygun dosyanın detayına gidin `NORTHWND.MDF` ve Tamam ' a tıklayın. Bu noktada, ekranınızda Şekil 2 ' ye benzer görünmelidir.

[![Uygun veritabanı örneğine bağlanma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**Şekil 2**: uygun veritabanı örneğine bağlanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))

> [!NOTE]
> SQL Server 2005 Express Sürüm Management Studio örneğine bağlanırken veritabanları Iliştirme iletişim kutusu, Belgelerim gibi Kullanıcı profili dizinlerinde ayrıntıya geçmenize izin vermez. Bu nedenle, `NORTHWND.MDF` ve `NORTHWND_log.LDF` dosyalarını Kullanıcı profili olmayan bir dizine yerleştirdiğinizden emin olun.

Veritabanını eklemek için Tamam düğmesine tıklayın. Veritabanları Iliştir iletişim kutusu kapanır ve Nesne Gezgini artık tam olarak eklenmiş veritabanını listelemelidir. Northwind veritabanının benzer bir adı vardır `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` . Veritabanına sağ tıklayıp Yeniden Adlandır ' ı seçerek veritabanını Northwind olarak yeniden adlandırın.

![Veritabanını Northwind olarak yeniden adlandırma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**Şekil 3**: veritabanını Northwind olarak yeniden adlandırma

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>2. Adım: Visual Studio 'da yeni bir çözüm ve SQL Server projesi oluşturma

SQL Server 2005 ' de yönetilen saklı yordamlar veya UDF 'ler oluşturmak için, saklı yordamı ve UDF mantığını bir sınıfta C# kodu olarak yazacak. Kod yazıldıktan sonra, bu sınıfı bir derlemede derlemek (bir `.dll` dosyası), derlemeyi SQL Server veritabanına kaydetmeniz ve sonra veritabanında ilgili yönteme işaret eden bir saklı yordam ya da UDF nesnesi oluşturmanız gerekecektir. Bu adımların tümü el ile gerçekleştirilebilir. Kodu herhangi bir metin düzenleyicisinde oluşturabilir, C# derleyicisini kullanarak komut satırından derleyebiliriz ( [`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx) ), [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) komutu veya Management Studio kullanarak veritabanına kaydedebilir ve saklı yordamı ya da UDF nesnesini benzer yollarla ekleyebilirsiniz. Neyse ki, Visual Studio 'nun profesyonel ve Team Systems sürümleri, bu görevleri otomatikleştiren SQL Server bir proje türü içerir. Bu öğreticide, yönetilen bir saklı yordam ve UDF oluşturmak için SQL Server proje türünü kullanarak izlenecek yol göstereceğiz.

> [!NOTE]
> Visual Web Developer veya Visual Studio Standard Edition kullanıyorsanız, bunun yerine el ile yaklaşımı kullanmanız gerekir. 13. adım, bu adımları el ile gerçekleştirmeye yönelik ayrıntılı yönergeler sağlar. Bu adımlar, kullanmakta olduğunuz Visual Studio sürümü ne olursa olsun, uygulanması gereken önemli SQL Server yapılandırma yönergelerini içerdiğinden, adım 13 ' i okumadan önce 2 ile 12 arasındaki adımları okumanızı öneririz.

Visual Studio 'Yu açarak başlayın. Yeni proje iletişim kutusunu görüntülemek için Dosya menüsünden Yeni proje ' yi seçin (bkz. Şekil 4). Veritabanı projesi türünün detayına gidin ve sağ tarafta listelenen şablonlardan yeni bir SQL Server projesi oluşturmayı seçin. Bu projeyi adlandırma `ManagedDatabaseConstructs` ve adlı bir çözüm içine yerleştirdim `Tutorial75` .

[![Yeni bir SQL Server projesi oluştur](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**Şekil 4**: yeni bir SQL Server projesi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))

Çözüm ve SQL Server proje oluşturmak için yeni proje iletişim kutusundaki Tamam düğmesine tıklayın.

Bir SQL Server projesi belirli bir veritabanına bağlıdır. Sonuç olarak, yeni SQL Server projesi oluşturduktan sonra bu bilgileri hemen belirtmemiz istenir. Şekil 5 ' te, 1. adımda SQL Server 2005 Express Sürüm veritabanı örneğine Kaydolduğumuz Northwind veritabanına işaret etmek üzere doldurulmuş yeni veritabanı başvurusu iletişim kutusu gösterilir.

![SQL Server projesini Northwind veritabanıyla ilişkilendir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**Şekil 5**: SQL Server projesini Northwind veritabanıyla ilişkilendirme

Bu proje içinde oluşturduğumuz yönetilen saklı yordamları ve UDF 'Leri hata ayıklaması yapmak için, bağlantı için SQL/CLR hata ayıklama desteğini etkinleştirmemiz gerekiyor. Bir SQL Server projesini yeni bir veritabanıyla ilişkilendirirken (Şekil 5 ' te yaptığımız gibi), Visual Studio, bağlantıda SQL/CLR hata ayıklamayı etkinleştirmek isteyip istemediğinizi sorar (bkz. Şekil 6). Evet'e tıklayın.

![SQL/CLR hata ayıklamayı etkinleştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**Şekil 6**: SQL/CLR hata ayıklamayı etkinleştir

Bu noktada yeni SQL Server projesi çözüme eklenmiştir. `Test Scripts` `Test.sql` Projede oluşturulan yönetilen veritabanı nesnelerinde hata ayıklamak için kullanılan adlı bir dosyayla adlı bir klasör içerir. Adım 12 ' de hata ayıklamaya bakacağız.

Artık bu projeye yeni yönetilen saklı yordamlar ve UDF 'ler ekleyebiliriz, ancak ilk olarak çözümde mevcut Web uygulamamıza izin vermeden önce Dosya menüsünden Ekle seçeneğini belirleyin ve mevcut Web sitesi ' ni seçin. Uygun Web sitesi klasörüne gidin ve Tamam ' a tıklayın. Şekil 7 ' de gösterildiği gibi bu, çözümü iki proje içerecek şekilde güncelleştirecektir: Web sitesi ve `ManagedDatabaseConstructs` SQL Server projesi.

![Çözüm Gezgini artık Iki proje Içeriyor](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**Şekil 7**: Çözüm Gezgini Şu anda Iki proje içeriyor

`NORTHWNDConnectionString`İçindeki değeri `Web.config` Şu anda `NORTHWND.MDF` klasöründeki dosyaya başvuruyor `App_Data` . Bu veritabanını ' dan kaldırdık `App_Data` ve SQL Server 2005 Express sürüm veritabanı örneğinde açıkça kaydettiğimiz için, değeri güncelleştirmeniz gerekir `NORTHWNDConnectionString` . `Web.config`Web sitesinde dosyasını açın ve `NORTHWNDConnectionString` bağlantı dizesinin şunu okuması için değeri değiştirin: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` . Bu değişiklikten sonra, `<connectionStrings>` bölümündeki bölümünün `Web.config` aşağıdakine benzer şekilde görünmesi gerekir:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> [Önceki öğreticide](debugging-stored-procedures-cs.md)açıklandığı gibi, bir istemci uygulamasından bir ASP.NET Web sitesi gibi SQL Server nesnesinde hata ayıklarken bağlantı havuzunu devre dışı bıraktık. Yukarıda gösterilen bağlantı dizesi bağlantı kuyruğunu devre dışı bırakır ( `Pooling=false` ). Yönetilen saklı yordamlar ve UDF 'ler ASP.NET Web sitesinden hata ayıklamayı planlamıyorsanız bağlantı havuzunu etkinleştirin.

## <a name="step-3-creating-a-managed-stored-procedure"></a>3. Adım: yönetilen saklı yordam oluşturma

Bir yönetilen saklı yordamı Northwind veritabanına eklemek için ilk olarak SQL Server projesinde saklı yordamı bir yöntem olarak oluşturmanız gerekir. Çözüm Gezgini, `ManagedDatabaseConstructs` proje adına sağ tıklayın ve yeni bir öğe eklemeyi seçin. Bu işlem, projeye eklenebilen yönetilen veritabanı nesnelerinin türlerini listeleyen yeni öğe Ekle iletişim kutusunu görüntüler. Şekil 8 ' de gösterildiği gibi, bunlar arasında saklı yordamlar ve Kullanıcı tanımlı Işlevler de dahildir.

Yalnızca, artık durdurulmuş olan tüm ürünleri döndüren bir saklı yordam ekleyerek başlayalım. Yeni saklı yordam dosyasını adlandırın `GetDiscontinuedProducts.cs` .

[![GetDiscontinuedProducts.cs adlı yeni bir saklı yordam ekleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**Şekil 8**: adlı yeni bir saklı yordam ekleyin `GetDiscontinuedProducts.cs` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))

Bu, aşağıdaki içeriğe sahip yeni bir C# sınıf dosyası oluşturur:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

Saklı yordamın `static` adlı bir sınıf dosyası içinde bir yöntem olarak uygulandığını unutmayın `partial` `StoredProcedures` . Üstelik, yöntemi, `GetDiscontinuedProducts` `SqlProcedure attribute` yöntemi saklı yordam olarak işaretleyen ile birlikte tasarlanmıştır.

Aşağıdaki kod, bir `SqlCommand` nesnesi oluşturur ve değerini, `CommandText` alanı 1 ' e `SELECT` `Products` eşit olan ürünler için tablodaki tüm sütunları döndüren bir sorgu olarak ayarlar `Discontinued` . Daha sonra komutu yürütür ve sonuçları istemci uygulamasına geri gönderir. Bu kodu `GetDiscontinuedProducts` yöntemine ekleyin.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

Tüm yönetilen veritabanı nesneleri, çağıranın bağlamını temsil eden bir [ `SqlContext` nesneye](https://msdn.microsoft.com/library/ms131108.aspx) erişebilir. , `SqlContext` [ `Pipe` Özelliği](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)aracılığıyla bir [ `SqlPipe` nesneye](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) erişim sağlar. Bu `SqlPipe` nesne SQL Server veritabanı ile çağıran uygulama arasında bilgi almak için kullanılır. Adından da anlaşılacağı gibi, [ `ExecuteAndSend` yöntemi](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) bir geçirilen `SqlCommand` nesneyi yürütür ve sonuçları istemci uygulamasına geri gönderir.

> [!NOTE]
> Yönetilen veritabanı nesneleri, küme tabanlı mantık yerine yordamsal mantığı kullanan saklı yordamlar ve UDF 'ler için idealdir. Yordamsal mantık, satır satır temelinde veri kümeleriyle çalışmayı veya skaler verilerle çalışmayı içerir. `GetDiscontinuedProducts`Ancak yeni oluşturduğumuz yöntem hiçbir yordam mantığını içermez. Bu nedenle, ideal olarak T-SQL saklı yordamı olarak uygulanmalıdır. Yönetilen saklı yordamlar oluşturmak ve dağıtmak için gereken adımları göstermek üzere yönetilen bir saklı yordam olarak uygulanır.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>4. Adım: yönetilen saklı yordamı dağıtma

Bu kod tamamlandıktan sonra Northwind veritabanına dağıtmaya hazırız. SQL Server bir projeyi dağıtmak, kodu bir derlemeye derler, derlemeyi veritabanına kaydeder ve veritabanında ilgili nesneleri oluşturur ve bu nesneleri derlemede uygun yöntemlere ilişkilendirir. Dağıtım seçeneği tarafından gerçekleştirilen görevlerin tam bir kümesi 13. adımda daha hassas bir şekilde yazılmaktır. `ManagedDatabaseConstructs`Çözüm Gezgini proje adına sağ tıklayın ve Dağıt seçeneğini belirleyin. Ancak, dağıtım şu hata ile başarısız olur: ' EXTERNAL ' yakınında yanlış sözdizimi. Bu özelliği etkinleştirmek için geçerli veritabanının uyumluluk düzeyini daha yüksek bir değere ayarlamanız gerekebilir. Saklı yordam için yardıma bakın `sp_dbcmptlevel` .

Derlemeyi Northwind veritabanıyla kaydetmeye çalışırken bu hata iletisi oluşur. Bir derlemeyi SQL Server 2005 veritabanı ile kaydetmek için veritabanının uyumluluk düzeyi 90 olarak ayarlanmalıdır. Varsayılan olarak, yeni SQL Server 2005 veritabanlarının uyumluluk düzeyi 90 ' dir. Ancak, Microsoft SQL Server 2000 kullanılarak oluşturulan veritabanlarının varsayılan uyumluluk düzeyi 80 ' dir. Northwind veritabanı başlangıçta Microsoft SQL Server 2000 veritabanı olduğundan, uyumluluk düzeyi Şu anda 80 olarak ayarlanmıştır ve bu nedenle yönetilen veritabanı nesnelerini kaydettirmek için 90.

Veritabanı s uyumluluk düzeyini güncelleştirmek için Management Studio yeni bir sorgu penceresi açın ve şunu girin:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

Yukarıdaki sorguyu çalıştırmak için araç çubuğundaki yürütme simgesine tıklayın.

[![Northwind veritabanı uyumluluk düzeyini güncelleştirme](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**Şekil 9**: Northwind veritabanı uyumluluk düzeyini güncelleştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))

Uyumluluk düzeyini güncelleştirdikten sonra SQL Server projeyi yeniden dağıtın. Bu sefer dağıtım hatasız tamamlanmalıdır.

SQL Server Management Studio dönün, Nesne Gezgini Northwind veritabanına sağ tıklayın ve Yenile ' yi seçin. Daha sonra, programlama klasörü detayına gidin ve ardından derlemeler klasörünü genişletin. Şekil 10 ' da gösterildiği gibi, Northwind veritabanı artık proje tarafından oluşturulan derlemeyi içerir `ManagedDatabaseConstructs` .

![ManagedDatabaseConstructs derlemesi artık Northwind veritabanına kayıtlı](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**Şekil 10**: `ManagedDatabaseConstructs` derleme artık Northwind veritabanına kayıtlı

Ayrıca, saklı yordamlar klasörünü genişletin. Adlı bir saklı yordam görürsünüz `GetDiscontinuedProducts` . Bu saklı yordam, dağıtım işlemi tarafından oluşturulmuştur ve derlemedeki yöntemine işaret eder `GetDiscontinuedProducts` `ManagedDatabaseConstructs` . `GetDiscontinuedProducts`Saklı yordam yürütüldüğünde, bu, sırasıyla `GetDiscontinuedProducts` yöntemini yürütür. Bu yönetilen bir saklı yordam olduğundan, Management Studio ile düzenlenemez (Bu nedenle, saklı yordam adının yanındaki kilit simgesi).

![GetDiscontinuedProducts saklı yordamı saklı yordamlar klasöründe listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**Şekil 11**: `GetDiscontinuedProducts` saklı yordam saklı yordamlar klasöründe listelenir

Yönetilen saklı yordamı çağırabilmemiz için aşmamız gereken bir daha aceye sahip olmaya devam ediyoruz: veritabanı yönetilen kodun yürütülmesini engelleyecek şekilde yapılandırılmıştır. Yeni bir sorgu penceresi açıp saklı yordamı yürüterek bunu doğrulayın `GetDiscontinuedProducts` . Şu hata iletisini alırsınız: .NET Framework Kullanıcı kodu yürütme devre dışı bırakıldı. ' CLR etkin yapılandırma seçeneğini etkinleştirin.

Northwind veritabanı yapılandırma bilgilerini incelemek için, komutu sorgu penceresinde girin ve yürütün `exec sp_configure` . Bu, clr etkin ayarının Şu anda 0 olarak ayarlandığını gösterir.

[![Clr etkin ayarı şu anda 0 olarak ayarlanmış](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**Şekil 12**: clr etkin ayarı şu anda 0 olarak ayarlanmıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))

Şekil 12 ' deki her yapılandırma ayarının, ile listelenmiş dört değeri olduğunu unutmayın: en düşük ve en yüksek değerler ve yapılandırma ve çalıştırma değerleri. Clr etkin ayarının yapılandırma değerini güncelleştirmek için aşağıdaki komutu yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

Yeniden çalıştırırsanız `exec sp_configure` Yukarıdaki deyimin clr özellikli ayar s yapılandırma değerini 1 olarak güncelleştirildiğini, ancak çalıştırma değerinin hala 0 olarak ayarlandığını görürsünüz. Bu yapılandırma değişikliğinin etkili olması için, [ `RECONFIGURE` komutu](https://msdn.microsoft.com/library/ms176069.aspx)yürütmemiz gerekir, bu, Run değerini geçerli yapılandırma değerine ayarlar. `RECONFIGURE`Sorgu penceresine girmeniz yeterlidir ve araç çubuğundaki yürütme simgesine tıklayın. `exec sp_configure`Şimdi çalıştırırsanız, clr özellikli ayar s yapılandırması ve çalıştırma değerleri için 1 değerini görmeniz gerekir.

Clr etkinleştirilmiş yapılandırma tamamlandıktan sonra, yönetilen saklı yordamı çalıştırmaya hazırız `GetDiscontinuedProducts` . Sorgu penceresinde komutunu girip yürütün `exec` `GetDiscontinuedProducts` . Saklı yordamı çağırmak, yönteminde karşılık gelen yönetilen kodun yürütülmesine neden olur `GetDiscontinuedProducts` . Bu kod, `SELECT` kullanımdan kaldırılmıştır ve bu verileri bu örnekteki SQL Server Management Studio çağıran uygulamaya döndüren bir sorgu yayınlar. Management Studio bu sonuçları alır ve sonuçlar penceresinde görüntüler.

[![GetDiscontinuedProducts saklı yordamı, tüm Discontinued ürünlerini döndürür](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**Şekil 13**: `GetDiscontinuedProducts` saklı yordam, tüm durdurulmuş ürünleri döndürür ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>5. Adım: giriş parametrelerini kabul eden yönetilen saklı yordamlar oluşturma

Bu öğreticiler genelinde oluşturduğumuz sorguların ve saklı yordamların birçoğu, kullanılan *parametreleri*içerir. Örneğin, [yazılan veri kümesi s TableAdapters öğreticisi Için yeni saklı yordamlar oluşturma](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) bölümünde `GetProductsByCategoryID` adlı bir giriş parametresi kabul eden adlı bir saklı yordam oluşturduk `@CategoryID` . Daha sonra saklı yordam, `CategoryID` alanı sağlanan parametrenin değeri ile eşleşen tüm ürünleri geri döndürür `@CategoryID` .

Giriş parametrelerini kabul eden bir yönetilen saklı yordam oluşturmak için, bu parametreleri yöntem s tanımında belirtmeniz yeterlidir. Bunu göstermek için, ' ın adlı projeye başka bir yönetilen saklı yordam eklemesine izin verin `ManagedDatabaseConstructs` `GetProductsWithPriceLessThan` . Bu yönetilen saklı yordam, bir fiyat belirten giriş parametresini kabul eder ve alanı parametre değerinden küçük olan tüm ürünleri döndürür `UnitPrice` .

Projeye yeni bir saklı yordam eklemek için `ManagedDatabaseConstructs` proje adına sağ tıklayın ve yeni bir saklı yordam eklemeyi seçin. Dosyayı `GetProductsWithPriceLessThan.cs` olarak adlandırın. Adım 3 ' te gördüğümüz gibi, bu, sınıfının içine yerleştirilmiş adlı bir yöntemle yeni bir C# sınıf dosyası oluşturur `GetProductsWithPriceLessThan` `partial` `StoredProcedures` .

`GetProductsWithPriceLessThan`Yöntem tanımları ' nı adlı bir giriş parametresi kabul edecek şekilde güncelleştirin [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) `price` ve yürütülecek kodu yazın ve sorgu sonuçlarını döndürün:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

`GetProductsWithPriceLessThan`Yöntem tanımı ve kodu, `GetDiscontinuedProducts` Adım 3 ' te oluşturulan metodun tanımına ve koduna benzer. Tek fark, `GetProductsWithPriceLessThan` yöntemin giriş parametresi olarak kabul ettesidir () `price` , `SqlCommand` s sorgusu bir parametre () içerir `@MaxPrice` ve bir parametre `SqlCommand` s koleksiyonuna eklenir `Parameters` ve değişkenin değeri atanır `price` .

Bu kodu ekledikten sonra SQL Server projesini yeniden dağıtın. Sonra, SQL Server Management Studio ' a dönüp saklı yordamlar klasörünü yenileyin. Yeni bir giriş görmeniz gerekir `GetProductsWithPriceLessThan` . Sorgu penceresinde, `exec GetProductsWithPriceLessThan 25` Şekil 14 ' ün gösterdiği gibi, $25 ' den küçük tüm ürünleri listelendirilecektir ve komutunu girin ve yürütün.

[![$25 altındaki ürünler görüntülenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**Şekil 14**: $25 altındaki ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>6. Adım: yönetilen saklı yordamı veri erişim katmanından çağırma

Bu noktada, `GetDiscontinuedProducts` ve `GetProductsWithPriceLessThan` yönetilen saklı yordamları `ManagedDatabaseConstructs` projeye ekledik ve bunları Northwind SQL Server veritabanına kaydettiniz. Ayrıca, bu yönetilen saklı yordamları SQL Server Management Studio 'tan de çağırdık (bkz. Şekil s 13 ve 14). Ancak, ASP.NET uygulamamız tarafından yönetilen bu saklı yordamları kullanabilmesi için, bunları mimarideki veri erişimi ve Iş mantığı katmanlarına eklememiz gerekir. Bu adımda, türü belirtilmiş DataSet `ProductsTableAdapter` `NorthwindWithSprocs` [s TableAdapters öğreticisi Için başlangıçta yeni saklı yordamlar oluşturmak Için](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) oluşturulmuş olan veri kümesindeki içine iki yeni yöntem ekleyeceğiz. Adım 7 ' de, BLL 'ye karşılık gelen yöntemleri ekleyeceğiz.

`NorthwindWithSprocs`Visual Studio 'da türü belirtilmiş veri kümesini açın ve adlı yeni bir yöntem ekleyerek başlayın `ProductsTableAdapter` `GetDiscontinuedProducts` . TableAdapter 'a yeni bir yöntem eklemek için, tasarımcıda TableAdapter s adına sağ tıklayın ve bağlam menüsünden sorgu Ekle seçeneğini belirleyin.

> [!NOTE]
> Northwind veritabanını `App_Data` klasörden SQL Server 2005 Express sürüm veritabanı örneğine taşıdığımız için, Web.config içindeki karşılık gelen bağlantı dizesinin bu değişikliği yansıtacak şekilde güncellenmesi zorunludur. 2 `NORTHWNDConnectionString` . adımda ' de değeri güncelleştirme yaptık `Web.config` . Bu güncelleştirmeyi yapmayı unuttuysanız, sorgu ekleme başarısız oldu iletisini görürsünüz. `NORTHWNDConnectionString` `Web.config` TableAdapter 'a yeni bir yöntem eklenmeye çalışılırken bir iletişim kutusunda nesne bağlantısı bulunamıyor. Bu hatayı çözmek için, Tamam ' a tıklayın ve ardından `Web.config` `NORTHWNDConnectionString` 2. adımda anlatıldığı gibi değere gidin ve değeri güncelleştirin. Ardından, yöntemi TableAdapter 'a yeniden eklemeyi deneyin. Bu süre hatasız çalışmalıdır.

Yeni bir yöntem eklendiğinde, eski öğreticilerde birçok kez kullandığımız TableAdapter sorgu Yapılandırma Sihirbazı başlatılır. İlk adım, TableAdapter 'ın veritabanına nasıl erişmesi gerektiğini belirtmesini ister: geçici bir SQL ifadesiyle veya yeni veya mevcut bir saklı yordam aracılığıyla. Yönetilen saklı yordamı veritabanıyla zaten oluşturup kaydettiğimiz `GetDiscontinuedProducts` için, mevcut saklı yordamı kullan seçeneğini belirleyin ve sonraki düğmesine basın.

[![Mevcut saklı yordamı kullan seçeneğini belirleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**Şekil 15**: mevcut saklı yordamı kullan seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))

Sonraki ekranda, yöntemin çağıracağı saklı yordam için bizi uyarır. `GetDiscontinuedProducts`Açılan listeden yönetilen saklı yordamı seçin ve ileri ' ye tıklayın.

[![GetDiscontinuedProducts yönetilen saklı yordamını seçin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**Şekil 16**: `GetDiscontinuedProducts` yönetilen saklı yordamı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))

Daha sonra, saklı yordamın satırları, tek bir değeri veya herhangi bir şey döndürüp döndürmeyeceğini belirtmemiz istenir. `GetDiscontinuedProducts`, Discontinued ürün satırları kümesini döndürdüğünden, ilk seçeneği (tablosal veri) seçin ve ileri ' ye tıklayın.

[![Tablo verisi seçeneğini belirleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**Şekil 17**: tablo verisi seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))

Son sihirbaz ekranı, kullanılan veri erişim desenlerini ve elde edilen yöntemlerin adlarını belirtmemizi sağlar. Her iki onay kutusu işaretli bırakın ve yöntemleri `FillByDiscontinued` ve olarak adlandırın `GetDiscontinuedProducts` . Sihirbazı tamamlamak için Son’a tıklayın.

[![Metotları FillByDiscontinued ve GetDiscontinuedProducts olarak adlandırın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**Şekil 18**: yöntemleri `FillByDiscontinued` ve `GetDiscontinuedProducts` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))

`FillByPriceLessThan` `GetProductsWithPriceLessThan` `ProductsTableAdapter` Yönetilen saklı yordamda için ve içinde adlı yöntemleri oluşturmak için bu adımları tekrarlayın `GetProductsWithPriceLessThan` .

Şekil 19, `ProductsTableAdapter` `GetDiscontinuedProducts` ve yönetilen saklı yordamlar için yöntemleri eklendikten sonra veri kümesi tasarımcısının ekran görüntüsünü gösterir `GetProductsWithPriceLessThan` .

[![ProductsTableAdapter, bu adımda eklenen yeni yöntemleri Içerir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**Şekil 19**: `ProductsTableAdapter` Bu adımda eklenen yeni yöntemleri içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png))

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>7. Adım: Ilgili yöntemleri Iş mantığı katmanına ekleme

Artık, 4 ve 5. adımlarda eklenen yönetilen saklı yordamları çağırmaya yönelik yöntemler eklemek için veri erişim katmanını güncelleştirdik. Iş mantığı katmanına ilgili yöntemleri eklememiz gerekiyor. Aşağıdaki iki yöntemi `ProductsBLLWithSprocs` sınıfına ekleyin:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

Her iki yöntem de karşılık gelen DAL yöntemini çağırır ve `ProductsDataTable` örneği döndürüyor. `DataObjectMethodAttribute`Her yöntemin üzerindeki biçimlendirme bu yöntemlerin, ObjectDataSource s veri kaynağını yapılandırma SIHIRBAZıNıN seçim sekmesinde yer alan açılan listede yer almasına neden olur.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>8. Adım: yönetilen saklı yordamları sunum katmanından çağırma

Iş mantığı ve veri erişimi katmanları, `GetDiscontinuedProducts` ve yönetilen saklı yordamları çağırma desteğini kapsayacak şekilde `GetProductsWithPriceLessThan` genişletiyorsa, artık bu saklı yordam sonuçlarını bir ASP.NET sayfası aracılığıyla görüntüleriz.

`ManagedFunctionsAndSprocs.aspx` `AdvancedDAL` Klasörü klasöründe açın ve araç kutusundan Tasarımcı üzerine bir GridView sürükleyin. GridView s `ID` özelliğini `DiscontinuedProducts` ve akıllı etiketinden, adlı yeni bir ObjectDataSource 'a bağlamak için olarak ayarlayın `DiscontinuedProductsDataSource` . Veri kaynaklarını sınıf s yönteminden çekmek için ObjectDataSource 'ı yapılandırın `ProductsBLLWithSprocs` `GetDiscontinuedProducts` .

[![ObjectDataSource 'ı ProductsBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**Şekil 20**: bir sınıfı kullanmak için ObjectDataSource 'ı yapılandırma `ProductsBLLWithSprocs` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))

[![Seç sekmesindeki açılan listeden GetDiscontinuedProducts yöntemini seçin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**Şekil 21**: `GetDiscontinuedProducts` Seç sekmesindeki açılan listeden yöntemi seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))

Bu kılavuz yalnızca ürün bilgilerini göstermek için kullanılacak olduğundan, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerini (yok) ve ardından son ' a tıklayarak açılan listeleri ayarlayın.

Sihirbaz tamamlandıktan sonra Visual Studio, içindeki her bir veri alanı için otomatik olarak bir BoundField veya CheckBoxField ekler `ProductsDataTable` . Ve hariç olmak üzere tüm bu alanları kaldırmak için bir dakikanızı `ProductName` ayırın `Discontinued` ve bu noktada, GridView ve ObjectDataSource 'un bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı ayırın. Sayfa ziyaret edildiğinde, ObjectDataSource `ProductsBLLWithSprocs` sınıf s `GetDiscontinuedProducts` yöntemini çağırır. Adım 7 ' de gördüğünüz gibi, bu yöntem, `ProductsDataTable` `GetDiscontinuedProducts` saklı yordamı çağıran dal s sınıf s yöntemine çağrı yapılır `GetDiscontinuedProducts` . Bu saklı yordam yönetilen bir saklı yordamdır ve 3. adımda oluşturduğumuz kodu yürüterek, Discontinued ürünlerini döndürür.

Yönetilen saklı yordam tarafından döndürülen sonuçlar `ProductsDataTable` , dal tarafından bir olarak paketlenir ve sonra BLL 'ye döndürülür. Bu, daha sonra bunları GridView 'a bağlandıkları ve görüntülenen sunum katmanına geri döndürür. Beklenen şekilde, kılavuz bu ürünleri kaldırılmıştır.

[![Üretimi durdurulmuş ürünler listelenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**Şekil 22**: Discontinued ürünleri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))

Daha fazla uygulama için, sayfaya bir TextBox ve başka bir GridView ekleyin. Bu GridView 'un, sınıf s metodunu çağırarak TextBox 'a girilen miktardan daha az ürün göstermesini sağlayabilirsiniz `ProductsBLLWithSprocs` `GetProductsWithPriceLessThan` .

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>9. Adım: T-SQL UDF 'Leri oluşturma ve çağırma

Kullanıcı tanımlı Işlevler veya UDF 'ler, veritabanı nesneleridir ve programlama dillerinde işlevlerin semantiğini yakından taklit eder. C# ' deki bir işlev gibi, UDF 'ler değişken sayıda giriş parametresi içerebilir ve belirli bir türün değerini döndürebilir. UDF, skaler veri döndürebilir; bir dize, bir tamsayı, vb. ya da tablo verileri. Skaler bir veri türü döndüren bir UDF ile başlayan her iki tür UDF öğesine hızlıca göz atalım.

Aşağıdaki UDF belirli bir ürünün envanterinin tahmini değerini hesaplar. Bu, `UnitPrice` belirli bir ürün için, ve değerleri olmak üzere üç giriş parametresi gerçekleştirerek, `UnitsInStock` `Discontinued` ve türünde bir değer döndürür `money` . İle çarpılarak envanterin tahmini değerini hesaplar `UnitPrice` `UnitsInStock` . Üretimi durdurulmuş öğeler için bu değer yarıya iner.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

Bu UDF veritabanına eklendikten sonra, Programlanabilirlik klasörünü genişleterek, Işlevler ve sonra skaler değer Işlevleri Management Studio aracılığıyla bulunabilir. Bu, şöyle bir sorguda kullanılabilir `SELECT` :

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

`udf_ComputeInventoryValue`Udf 'Yi Northwind veritabanına ekledim; Şekil 23, `SELECT` Management Studio aracılığıyla görüntülendiğinde yukarıdaki sorgunun çıkışını gösterir. Ayrıca, UDF 'nin Nesne Gezgini skaler değer Işlevleri klasörünün altında listelendiğini unutmayın.

[![Her ürün stok değeri listelenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**Şekil 23**: her ürün stok değeri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))

UDF 'ler tablo verilerini de döndürebilir. Örneğin, belirli bir kategoriye ait ürünleri döndüren bir UDF oluşturuyoruz:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID`Udf bir `@CategoryID` giriş parametresini kabul eder ve belirtilen sorgunun sonuçlarını döndürür `SELECT` . Oluşturulduktan sonra, bu UDF `FROM` `JOIN` bir sorgunun (veya) yan tümcesinde başvurulabilir `SELECT` . Aşağıdaki örnek, `ProductID` `ProductName` `CategoryID` her bir içecek için, ve değerlerini döndürür.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

`udf_GetProductsByCategoryID`Udf 'Yi Northwind veritabanına ekledim; Şekil 24 ' `SELECT` Management Studio aracılığıyla görüntülendiğinde yukarıdaki sorgunun çıkışını gösterir. Tablo verileri döndüren UDF 'ler Nesne Gezgini s tablo-değer Işlevleri klasöründe bulunabilir.

[![ProductID, ProductName ve CategoryID her bir Içecek için listelenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**Şekil 24**:, `ProductID` `ProductName` ve her bir `CategoryID` beiçecek için listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png))

> [!NOTE]
> UDF 'ler oluşturma ve kullanma hakkında daha fazla bilgi için, [Kullanıcı tanımlı IŞLEVLERE giriş](http://www.sqlteam.com/item.asp?ItemID=1955)konusuna bakın. Ayrıca, [Kullanıcı tanımlı Işlevlerin olumlu ve dezavantajlarına](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)göz atın.

## <a name="step-10-creating-a-managed-udf"></a>10. Adım: yönetilen UDF oluşturma

`udf_ComputeInventoryValue` `udf_GetProductsByCategoryID` Yukarıdaki örneklerde oluşturulan ve UDF 'ler T-SQL veritabanı nesneleridir. SQL Server 2005 Ayrıca, `ManagedDatabaseConstructs` Adım 3 ve 5 ' ten yönetilen saklı yordamlar gibi, projeye eklenebilen yönetilen UDF 'leri de destekler. Bu adım için, `udf_ComputeInventoryValue` yönetilen kodda UDF 'yi uygulayalım.

Projeye yönetilen bir UDF eklemek için `ManagedDatabaseConstructs` Çözüm Gezgini proje adına sağ tıklayın ve yeni bir öğe eklemeyi seçin. Yeni öğe Ekle iletişim kutusundan Kullanıcı tanımlı şablon ' u seçin ve yeni UDF dosyasını adlandırın `udf_ComputeInventoryValue_Managed.cs` .

[![ManagedDatabaseConstructs projesine yeni bir yönetilen UDF ekleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**Şekil 25**: projeye yeni BIR yönetilen UDF ekleme `ManagedDatabaseConstructs` ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))

Kullanıcı tanımlı Işlev şablonu, `partial` `UserDefinedFunctions` adı sınıf dosya adı (Bu örnekte) ile aynı olan bir yöntemle adlı bir sınıf oluşturur `udf_ComputeInventoryValue_Managed` . Bu yöntem, yöntemi yönetilen bir UDF olarak işaret eden [ `SqlFunction` özniteliği](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)kullanılarak donatılmalıdır.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue`Yöntemi şu anda bir [ `SqlString` nesne](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) döndürüyor ve herhangi bir giriş parametresi kabul etmiyor. Yöntem tanımını,, `UnitPrice` ve-olmak üzere üç giriş parametresi kabul edecek şekilde güncelleştirmemiz gerekir `UnitsInStock` `Discontinued` `SqlMoney` . Envanter değerini hesaplama mantığı T-SQL UDF ' deki ile aynıdır `udf_ComputeInventoryValue` .

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

UDF yöntemi giriş parametrelerinin karşılık gelen SQL türleriyle olduğunu unutmayın: alanı için ve için `SqlMoney` `UnitPrice` [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) `UnitsInStock` [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) `Discontinued` . Bu veri türleri tabloda tanımlanan türleri yansıtır `Products` : `UnitPrice` sütun türü `money` , `UnitsInStock` türü sütunu `smallint` ve `Discontinued` türünün sütunu `bit` .

Kod, `SqlMoney` 0 değeri atanmış adlı bir örnek oluşturarak başlar `inventoryValue` . `Products`Tablo `NULL` , ve sütunlarındaki veritabanı değerlerine izin verir `UnitsInPrice` `UnitsInStock` . Bu nedenle, önce bu değerlerin `NULL` `SqlMoney` nesne s [ `IsNull` özelliğinden](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)yaptığımız olup olmadığını kontrol etmemiz gerekir. Her ikisi `UnitPrice` de `UnitsInStock` `NULL` değer olmayan değerler içeriyorsa, `inventoryValue` iki ürünün ürünü olarak ' i hesapladık. Ardından, `Discontinued` true ise değeri halliyoruz.

> [!NOTE]
> `SqlMoney`Nesne yalnızca iki `SqlMoney` örneğe birlikte çarpılmasına izin verir. Örneğin, bir `SqlMoney` Örneğin sabit bir kayan noktalı sayı ile çarpılmasına izin vermez. Bu nedenle, bunu bırakmak için `inventoryValue` `SqlMoney` 0,5 değerine sahip yeni bir örnekle çarpıyoruz.

## <a name="step-11-deploying-the-managed-udf"></a>11. Adım: yönetilen UDF dağıtma

Artık yönetilen UDF oluşturuldığına göre, bunu Northwind veritabanına dağıtmaya hazır hale gelmiştir. 4. adımda gördüğünüz gibi, bir SQL Server projesindeki yönetilen nesneler, Çözüm Gezgini proje adına sağ tıklayıp bağlam menüsünden dağıt seçeneği belirlenerek dağıtılır.

Projeyi dağıttıktan sonra, SQL Server Management Studio döndürün ve skaler değerli Işlevler klasörünü yenileyin. Şimdi iki giriş görmeniz gerekir:

- `dbo.udf_ComputeInventoryValue` -9. adımda oluşturulan T-SQL UDF ve
- `dbo.udf ComputeInventoryValue_Managed` -10. adımda oluşturulan yönetilen UDF, yeni dağıtıldı.

Bu yönetilen UDF 'yi test etmek için Management Studio içinden aşağıdaki sorguyu yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

Bu komut `udf ComputeInventoryValue_Managed` T-SQL UDF yerine yönetilen UDF kullanır `udf_ComputeInventoryValue` , ancak çıktı aynıdır. UDF s çıkışının ekran görüntüsünü görmek için Şekil 23 ' e geri bakın.

## <a name="step-12-debugging-the-managed-database-objects"></a>12. Adım: yönetilen veritabanı nesnelerinde hata ayıklama

[Saklı yordamlar hata ayıklaması](debugging-stored-procedures-cs.md) öğreticisinde, Visual Studio aracılığıyla SQL Server hata ayıklama için üç seçenekten bahsettik: doğrudan veritabanı hata ayıklaması, uygulama hata ayıklaması ve bir SQL Server projesinden hata ayıklama. Yönetilen veritabanı nesnelerine doğrudan veritabanı hata ayıklaması aracılığıyla hata ayıklanamaz, ancak bir istemci uygulamasından ve doğrudan SQL Server projesinden hata ayıklanabilir. Ancak, hata ayıklamanın çalışması için SQL Server 2005 veritabanı SQL/CLR hata ayıklamasına izin vermelidir. Visual Studio 'Yu ilk oluşturduğumuz, `ManagedDatabaseConstructs` SQL/CLR hata ayıklamayı etkinleştirmek isteyip istediğimiz konusunda sizi geri çekin (adım 2 ' de Şekil 6 ' ya bakın). Bu ayar, Sunucu Gezgini penceresinden veritabanına sağ tıklanarak değiştirilebilir.

![Veritabanının SQL/CLR hata ayıklamasına Izin verdiğinden emin olun](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**Şekil 26**: veritabanının SQL/CLR hata ayıklamasına izin verdiğinden emin olun

Yönetilen saklı yordamda hata ayıklamak istediğinizi düşünün `GetProductsWithPriceLessThan` . Yöntemin kodu içinde bir kesme noktası ayarlayarak başlayacağız `GetProductsWithPriceLessThan` .

[![GetProductsWithPriceLessThan yönteminde bir kesme noktası ayarlayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**Şekil 27**: yöntemde bir kesme noktası ayarlayın `GetProductsWithPriceLessThan` ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))

SQL Server projesinden yönetilen veritabanı nesnelerinde hata ayıklamaya ilk göz atalım. Çözümünüz iki proje içerdiğinden, `ManagedDatabaseConstructs` SQL Server projesi, Web sitemizden ve hata ayıklamaya başladığımızda, Visual Studio 'yu `ManagedDatabaseConstructs` SQL Server projeyi başlatmasını bildirmek için gereken SQL Server projeden `ManagedDatabaseConstructs`Çözüm Gezgini ' de projeye sağ tıklayın ve bağlam menüsünden başlangıç projesi olarak ayarla seçeneğini belirleyin.

`ManagedDatabaseConstructs`Proje hata ayıklayıcıdan başlatıldığında `Test.sql` , dosyasında, KLASÖRÜNDE bulunan SQL deyimlerini yürütür `Test Scripts` . Örneğin, yönetilen saklı yordamı test etmek için, `GetProductsWithPriceLessThan` mevcut `Test.sql` dosya içeriğini aşağıdaki ifadesiyle değiştirin ve bu, `GetProductsWithPriceLessThan` 14,95 değerini geçirerek yönetilen saklı yordamı çağırır `@CategoryID` :

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

Yukarıdaki betiği içine girdikten sonra hata ayıklama `Test.sql` menüsüne gidip hata ayıklamayı Başlat ' ı ya da araç çubuğundaki yeşil oynat simgesini seçerek hata ayıklamayı başlatın. Bu işlem, çözüm içinde projeleri oluşturur, yönetilen veritabanı nesnelerini Northwind veritabanına dağıtır ve ardından `Test.sql` betiği yürütür. Bu noktada, kesme noktası isabet eder ve yöntemin içinde ilerleyebileceğiniz `GetProductsWithPriceLessThan` , giriş parametrelerinin değerlerini inceleyebileceğiniz vb.

[![GetProductsWithPriceLessThan yöntemindeki kesme noktası Isabet ediyor](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**Şekil 28**: yöntemdeki kesme noktası `GetProductsWithPriceLessThan` isabet ediyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))

Bir SQL veritabanı nesnesinin hata ayıklaması için bir istemci uygulama aracılığıyla ayıklanmak üzere, veritabanının uygulama hata ayıklamasını destekleyecek şekilde yapılandırılması zorunludur. Sunucu Gezgini veritabanında veritabanına sağ tıklayın ve uygulama hata ayıklama seçeneğinin işaretli olduğundan emin olun. Ayrıca, ASP.NET uygulamasını SQL hata ayıklayıcıyla tümleştirilecek ve bağlantı havuzunu devre dışı bırakacak şekilde yapılandırmamız gerekir. Bu adımlar, [saklı yordamlar](debugging-stored-procedures-cs.md) öğreticisinin adım 2 ' de ayrıntılı olarak açıklanmaktadır.

ASP.NET uygulamasını ve veritabanını yapılandırdıktan sonra, ASP.NET Web sitesini başlangıç projesi olarak ayarlayın ve hata ayıklamayı başlatın. Kesme noktası olan yönetilen nesnelerden birini çağıran bir sayfayı ziyaret ederseniz, uygulama durabilir ve denetim hata ayıklayıcıya açılır; burada Şekil 28 ' de gösterildiği gibi kodda adım adım gezinebilirsiniz.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>13. Adım: yönetilen veritabanı nesnelerini El Ile derleme ve dağıtma

SQL Server projeler, yönetilen veritabanı nesneleri oluşturmayı, derlemeyi ve dağıtmayı kolaylaştırır. Ne yazık ki SQL Server projeler yalnızca Visual Studio 'nun Professional ve Team Systems sürümlerinde kullanılabilir. Visual Web Developer veya Visual Studio 'nun standart sürümünü kullanıyorsanız ve yönetilen veritabanı nesnelerini kullanmak istiyorsanız, bunları el ile oluşturmanız ve dağıtmanız gerekir. Bu dört adımdan oluşur:

1. Yönetilen veritabanı nesnesi için kaynak kodunu içeren bir dosya oluşturun,
2. Nesneyi bir derlemede derleyin,
3. Derlemeyi SQL Server 2005 veritabanı ile kaydedin ve
4. SQL Server, derlemede uygun yöntemi işaret eden bir veritabanı nesnesi oluşturun.

Bu görevleri göstermek için, `UnitPrice` belirli bir değerden daha büyük olan ürünleri döndüren yeni bir yönetilen saklı yordam oluşturalım. Bilgisayarınızda adlı yeni bir dosya oluşturun `GetProductsWithPriceGreaterThan.cs` ve dosyaya aşağıdaki kodu girin (bunu gerçekleştirmek Için Visual Studio, Not defteri veya herhangi bir metin düzenleyicisini kullanabilirsiniz):

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

Bu kod, `GetProductsWithPriceLessThan` 5. adımda oluşturulan yöntemden neredeyse aynıdır. Tek farklar, sorguda kullanılan yöntem adları, `WHERE` yan tümce ve parametre adıdır. Yöntemine geri dönün `GetProductsWithPriceLessThan` , `WHERE` yan tümcesini okuyun: `WHERE UnitPrice < @MaxPrice` . Burada, ' de `GetProductsWithPriceGreaterThan` şunu kullanıyoruz: `WHERE UnitPrice > @MinPrice` .

Şimdi bu sınıfı bir derlemede derlemeniz gerekir. Komut satırından, dosyayı kaydettiğiniz dizine gidin `GetProductsWithPriceGreaterThan.cs` ve `csc.exe` sınıf dosyasını bir derlemede derlemek Için C# derleyicisini () kullanın:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

Sistemde bulunmayan ' de içeren klasör, `csc.exe` `PATH` yoluna tam olarak başvurmanız gerekecektir, `%WINDOWS%\Microsoft.NET\Framework\version\` Örneğin:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[![GetProductsWithPriceGreaterThan.cs derleme](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**Şekil 29**: `GetProductsWithPriceGreaterThan.cs` bir derlemeye derleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))

`/t`Bayrak, C# sınıf dosyasının BIR DLL (yürütülebilir değil) olarak derlenmesi gerektiğini belirtir. `/out`Bayrak, sonuçta elde edilen derlemenin adını belirtir.

> [!NOTE]
> `GetProductsWithPriceGreaterThan.cs`Sınıf dosyasını komut satırından derlemek yerine, alternatif olarak [Visual C# Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) 'ı kullanabilir veya Visual Studio Standard Edition 'Da ayrı bir sınıf kitaplığı projesi oluşturabilirsiniz. S Ren Jacob Lauritsen, `GetProductsWithPriceGreaterThan` saklı yordam kodu ve 3, 5 ve 10. adımlarda oluşturulan iki yönetilen saklı yordam ve UDF ile birlikte bir Visual C# Express Edition projesi sağlamıştır. Ayrıca, ilgili veritabanı nesnelerini eklemek için gereken T-SQL komutlarını içeren s Ren Project.

Bir derlemeye derlenen kodla, derlemeyi SQL Server 2005 veritabanı içine kaydetmeye hazırız. Bu, komutunu kullanarak veya SQL Server Management Studio aracılığıyla T-SQL üzerinden gerçekleştirilebilir `CREATE ASSEMBLY` . Management Studio kullanmaya odaklanalım.

Management Studio, Northwind veritabanındaki programlama klasörünü genişletin. Alt klasörlerinden biri derlemelerdir. Veritabanına yeni bir derlemeyi el ile eklemek için derlemeler klasörüne sağ tıklayın ve bağlam menüsünden Yeni derleme ' yi seçin. Bu, yeni derleme iletişim kutusunu görüntüler (bkz. Şekil 30). Araştır düğmesine tıklayın, `ManuallyCreatedDBObjects.dll` Yeni derduğumuz derlemeyi seçin ve ardından derlemeyi veritabanına eklemek için Tamam ' a tıklayın. `ManuallyCreatedDBObjects.dll`Derlemeyi Nesne Gezgini görmemelisiniz.

[![Veritabanına ManuallyCreatedDBObjects.dll derlemeyi ekleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**Şekil 30**: `ManuallyCreatedDBObjects.dll` derlemeyi veritabanına ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))

![ManuallyCreatedDBObjects.dll Nesne Gezgini listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**Şekil 31**: `ManuallyCreatedDBObjects.dll` Nesne Gezgini listede listelenir

Derlemeyi Northwind veritabanına ekledik, ancak bir saklı yordamı `GetProductsWithPriceGreaterThan` derlemedeki yöntemiyle ilişkilendirdik. Bunu gerçekleştirmek için yeni bir sorgu penceresi açın ve aşağıdaki betiği yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

Bu, Northwind veritabanında adlı yeni bir saklı yordam oluşturur `GetProductsWithPriceGreaterThan` ve onu yönetilen yöntemle ilişkilendirir `GetProductsWithPriceGreaterThan` (derlemede bulunan sınıfında `StoredProcedures` `ManuallyCreatedDBObjects` ).

Yukarıdaki betiği yürüttükten sonra, Nesne Gezgini saklı yordamlar klasörünü yenileyin. Yanında bir kilit simgesi olan yeni bir saklı yordam girişi görmeniz gerekir `GetProductsWithPriceGreaterThan` . Bu saklı yordamı test etmek için sorgu penceresine aşağıdaki betiği girin ve yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

Şekil 32 gösterdiği gibi, yukarıdaki komut $24,95 ' ten büyük olan bu ürünlerin bilgilerini görüntüler `UnitPrice` .

[![ManuallyCreatedDBObjects.dll Nesne Gezgini listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**Şekil 32**: `ManuallyCreatedDBObjects.dll` Nesne Gezgini listelenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))

## <a name="summary"></a>Özet

Microsoft SQL Server 2005, yönetilen kod kullanılarak veritabanı nesnelerinin oluşturulmasına izin veren ortak dil çalışma zamanı (CLR) ile tümleştirme sağlar. Daha önce bu veritabanı nesneleri yalnızca T-SQL kullanılarak oluşturulabilir, ancak artık C# gibi .NET programlama dillerini kullanarak bu nesneleri oluşturmuyoruz. Bu öğreticide, yönetilen iki saklı yordam ve yönetilen Kullanıcı tanımlı bir Işlev oluşturduk.

Visual Studio s SQL Server proje türü, yönetilen veritabanı nesneleri oluşturmayı, derlemeyi ve dağıtılmasını kolaylaştırır. Üstelik, zengin hata ayıklama desteği sunar. Ancak SQL Server proje türleri yalnızca Visual Studio 'nun Professional ve Team Systems sürümlerinde kullanılabilir. Visual Web Developer veya Visual Studio 'nun standart sürümünü kullanan kişiler için, 13. adımda gördüğünüz gibi oluşturma, derleme ve dağıtım adımlarının el ile gerçekleştirilmesi gerekir.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kullanıcı tanımlı Işlevlerin avantajları ve dezavantajları](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Yönetilen kodda SQL Server 2005 nesneleri oluşturma](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005 ' de yönetilen kod kullanarak Tetikleyiciler oluşturma](http://www.15seconds.com/issue/041006.htm)
- [Nasıl yapılır: CLR SQL Server saklı yordamı oluşturma ve çalıştırma](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Nasıl yapılır: bir CLR SQL Server Kullanıcı tanımlı Işlev oluşturma ve çalıştırma](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Nasıl yapılır: `Test.sql` SQL nesnelerini çalıştırmak için betiği düzenleme](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Kullanıcı tanımlı IŞLEVLERE giriş](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Yönetilen kod ve SQL Server 2005 (video)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-SQL başvurusu](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [İzlenecek yol: yönetilen kodda saklı yordam oluşturma](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [4GuysFromRolla.com](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Adresinden erişilebilir [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla bulunabilir [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, S. Bu makaleyi gözden geçirmenin yanı sıra, Ayrıca, yönetilen veritabanı nesnelerini el ile derlemek için bu makalede yer alan Visual C# Express Edition projesi de oluşturulmuştur. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, bana bir satır bırakın [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](debugging-stored-procedures-cs.md) 
>  [Sonraki](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
