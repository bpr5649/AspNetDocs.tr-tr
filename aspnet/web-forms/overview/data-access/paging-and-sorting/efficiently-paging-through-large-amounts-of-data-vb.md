---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: Büyük miktarda veri aracılığıyla verimli disk belleği oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Veri sunumu denetiminin varsayılan sayfalama seçeneği, temel alınan veri kaynağı denetimi retriev olarak büyük miktarlarda verilerle çalışırken uygun değildir...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d1c49e076e1c78e584f91fe2357a98da321f4260
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045110"
---
# <a name="efficiently-paging-through-large-amounts-of-data-vb"></a>Büyük Miktarlı Verileri Etkili Bir Şekilde Sayfalama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe) veya [PDF 'yi indirin](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> Veri sunumu denetiminin varsayılan sayfalama seçeneği, büyük miktarlarda verilerle çalışırken uygun değildir, çünkü temel alınan veri kaynağı denetimi tüm kayıtları alır, ancak yalnızca bir veri alt kümesi görüntülense bile. Bu tür durumlarda, özel disk belleği ' i açmanız gerekir.

## <a name="introduction"></a>Giriş

Önceki öğreticide anlatıldığı gibi, sayfalama iki şekilde de uygulanabilir:

- **Varsayılan sayfalama** yalnızca veri Web denetimi s akıllı etiketinde sayfalama etkinleştir seçeneği denetlenerek uygulanabilir. Ancak, bir veri sayfasını her görüntülerken, sayfada yalnızca bir alt kümesi görüntülenmese de, ObjectDataSource *Tüm* kayıtları alır
- **Özel sayfalama** , yalnızca Kullanıcı tarafından istenen verilerin belirli bir sayfası için görüntülenmesi gereken veritabanından alınan kayıtları alarak varsayılan sayfalama performansını geliştirir; Bununla birlikte, özel disk belleği, varsayılan sayfalamaktan daha fazla çaba gerektirir

Uygulama kolaylığına bağlı olarak yalnızca bir onay kutusunu işaretleyip yeniden yapmanız gerekir! Varsayılan disk belleği etkileyici bir seçenektir. Tüm kayıtları alırken Naïve yaklaşımı, çok büyük miktarlarda veri veya çok sayıda eşzamanlı kullanıcı içeren sitelerde sayfalama yaparken, bunu kesin bir seçenek yapar. Bu gibi durumlarda, yanıt veren bir sistem sağlamak için özel disk belleği ' i açmanız gerekir.

Özel sayfalama zorluğu, belirli bir veri sayfası için gereken tam kayıt kümesini döndüren bir sorgu yazamayacak. Neyse ki Microsoft SQL Server 2005, sonuçları derecelendirme için yeni bir anahtar sözcük sağlar ve bu da kayıtların uygun alt kümesini etkin bir şekilde alan bir sorgu yazmanızı sağlar. Bu öğreticide, bir GridView denetiminde özel sayfalama uygulamak için bu yeni SQL Server 2005 anahtar sözcüğünü nasıl kullanacağınızı inceleyeceğiz. Özel disk belleği için Kullanıcı arabirimi varsayılan sayfalama ile aynı olsa da, özel sayfalama kullanarak bir sayfadan sonrakine geçmek varsayılan sayfalamadan daha hızlı bir şekilde çok daha hızlı olabilir.

> [!NOTE]
> Özel disk belleği tarafından ele alınan tam performans kazancı, üzerinden disk belleğine alınan toplam kayıt sayısına ve yük veritabanı sunucusuna yerleştirilmesine bağlıdır. Bu öğreticinin sonunda, özel sayfalama yoluyla elde edilen performanstan faydalanan bazı kaba ölçümlere bakacağız.

## <a name="step-1-understanding-the-custom-paging-process"></a>Adım 1: özel sayfalama Işlemini anlama

Veriler üzerinden sayfalama yaparken, bir sayfada görünen kesin kayıtlar, istenen verilerin sayfasına ve sayfa başına gösterilecek kayıt sayısına bağlıdır. Örneğin, sayfa başına 10 ürün görüntüleyen 81 ürün aracılığıyla sayfa eklemek istediğimize göz lıyoruz. İlk sayfa görüntülenirken, 1 ' den 10 ' a kadar ürünlerin olmasını istiyoruz. ikinci sayfayı görüntülerken, 10 ile 20 arasındaki ürünlerle ilgilentik ve bu şekilde devam eder.

Hangi kayıtların alınması gerektiğini ve sayfalama arabiriminin nasıl işleneceğini belirten üç değişken vardır:

- **Başlangıç satırı dizini** görüntülenecek veriler sayfasındaki ilk satırın dizini. Bu dizin, sayfa dizinini, sayfa başına görüntülenecek ve bir tane eklenecek kayıtlarla çarpılarak hesaplanabilir. Örneğin, ilk sayfa (sayfa dizini 0 olan) için tek seferde 10 kayıt sırasında sayfalama sırasında, başlangıç satırı dizini 0 \* 10 + 1 veya 1; ikinci sayfa için (sayfa dizini 1), başlangıç satırı dizini 1 \* 10 + 1 veya 11 ' dir.
- **En fazla satır** sayısı, sayfa başına görüntülenecek en fazla kayıt sayısıdır. Bu değişken son sayfa için bu yana en fazla satır olarak adlandırılır, sayfa boyutundan daha az kayıt döndürülür. Örneğin, sayfa başına 81 ürün 10 kayıt sırasında sayfalama yaparken, dokuzuncu ve nihai sayfada yalnızca bir kayıt olur. Ancak sayfa olmadığından, en fazla satır değerinden daha fazla kayıt gösterilecektir.
- **Toplam kayıt** sayısı ile disk belleğine alınan toplam kayıt sayısı. Bu değişken, belirli bir sayfa için alınacak kayıtları belirlemek için gerekli olsa da, sayfalama arabirimini de dikte etmez. Örneğin, sayfalanmakta olan 81 ürün varsa sayfalama arabirimi, sayfalama Kullanıcı arabiriminde dokuz sayfa numarasını görüntülemeyi bilir.

Varsayılan sayfalama ile, başlangıç satırı dizini sayfa dizininin ürünü ve sayfa boyutu ile birlikte hesaplanır, ancak en fazla satır yalnızca sayfa boyutudur. Varsayılan sayfalama, herhangi bir veri sayfasını işlerken veritabanındaki tüm kayıtları gönderdiğinden, her bir satırın dizini bilindiğinden, bu nedenle başlangıç satırı Dizin satırına büyük bir görev gönderilir. Ayrıca, toplam kayıt sayısı, yalnızca DataTable içindeki kayıt sayısı (veya veritabanı sonuçlarını tutmak için kullanılan nesne) olarak hazır hale gelir.

Başlangıç satırı dizini ve en fazla satır değişkenleri verildiğinde, özel bir sayfalama uygulamasının yalnızca başlangıç satırı dizininden başlayarak kayıtların kesin alt kümesini döndürmesi ve bundan sonra en fazla satır sayısına dönmesi gerekir. Özel disk belleği iki zorluk sağlar:

- Belirtilen başlangıç satırı dizininde kayıtları döndürmeye başlayabilmemiz için, bir satır dizinini tüm verilerin sayfalandırılmış her bir satırla verimli bir şekilde ilişkilendirebilmelidir
- Disk belleğine alınan toplam kayıt sayısını sağlamamız gerekir

Sonraki iki adımda, bu iki güçlüğe yanıt vermek için gereken SQL betiğini inceleyeceğiz. SQL betiğine ek olarak, DAL ve BLL 'de yöntemler de uygulamamız gerekir.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>2. Adım: disk belleğine alınan toplam kayıt sayısını döndürme

Görüntülenmekte olan sayfa için tam kayıt alt kümesini nasıl alacağınızı incelemeden önce, ilk olarak disk belleğine alınan toplam kayıt sayısını geri döndürmenizi sağlar. Bu bilgiler, sayfalama Kullanıcı arabirimini düzgün bir şekilde yapılandırmak için gereklidir. Belirli bir SQL sorgusu tarafından döndürülen toplam kayıt sayısı, [ `COUNT` toplama işlevi](https://msdn.microsoft.com/library/ms175997.aspx)kullanılarak elde edilebilir. Örneğin, tablodaki toplam kayıt sayısını öğrenmek için `Products` aşağıdaki sorguyu kullanabiliriz:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

Bu bilgileri döndüren DAL için bir yöntem ekleyelim. Özellikle, `TotalNumberOfProducts()` `SELECT` yukarıda gösterilen deyimyi yürüten ADLı bir dal yöntemi oluşturacağız.

`Northwind.xsd`Yazılan veri kümesi dosyasını klasöründe açarak başlayın `App_Code/DAL` . Sonra, tasarımcıda öğesine sağ tıklayın `ProductsTableAdapter` ve sorgu Ekle ' yi seçin. Önceki öğreticilerde gördüğünüze göre, bu, çağrıldığında, belirli bir SQL ifadesini veya saklı yordamı yürütecek olan yeni bir yöntem ekleyebilmemiz için size izin verir. Bu, önceki öğreticilerdeki TableAdapter yöntemlerinde olduğu gibi, bir geçici SQL ifadesini kullanmayı tercih edebilir.

![Geçici bir SQL Ifadesini kullanın](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**Şekil 1**: GEÇICI bir SQL ifadesini kullanın

Sonraki ekranda, oluşturulacak sorgu türünü belirtebilirsiniz. Bu sorgu tek bir skaler değer döndürecek ve tablodaki toplam kayıt sayısı `Products` , `SELECT` bir tek değer seçeneği döndüren öğesini seçer.

![Sorguyu tek bir değer döndüren bir SELECT Ifadesini kullanacak şekilde yapılandırın](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**Şekil 2**: sorguyu tek bir değer döndüren bir SELECT ifadesini kullanacak şekilde yapılandırma

Kullanılacak sorgunun türünü belirttikten sonra sorguyu belirtmemiz gerekir.

![Products sorgusundan SELECT COUNT (*) kullanın](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**Şekil 3**: Ürünler SORGUSUNDAN select count ( \* ) kullanın

Son olarak, yöntemin adını belirtin. Belirtildiği gibi, ' ın kullanımına izin verin `TotalNumberOfProducts` .

![DAL yöntemi TotalNumberOfProducts olarak adlandırın](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**Şekil 4**: dal yöntemi TotalNumberOfProducts olarak adlandırın

Son ' a tıkladıktan sonra sihirbaz, `TotalNumberOfProducts` YÖNTEMI dal 'e ekler. DAL içindeki skaler döndürme yöntemleri, SQL sorgusunun sonucu olması halinde null yapılabilir türler döndürür `NULL` . `COUNT`Ancak sorgumuz her zaman değer olmayan bir `NULL` değer döndürür; ne olursa dal yöntemi null yapılabilir bir tamsayı döndürür.

DAL yöntemine ek olarak BLL 'de de bir metoda ihtiyacımız var. `ProductsBLL`Sınıf dosyasını açın ve `TotalNumberOfProducts` yalnızca dal s yöntemine çağrı yapan bir yöntem ekleyin `TotalNumberOfProducts` :

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

DAL oluşturma `TotalNumberOfProducts` yöntemi null yapılabilen bir tamsayı döndürür; ancak, `ProductsBLL` sınıf s `TotalNumberOfProducts` metodunu standart bir tamsayı döndürmesi için oluşturduk. Bu nedenle, `ProductsBLL` sınıf s `TotalNumberOfProducts` YÖNTEMININ, dal s yöntemi tarafından döndürülen Nullable tamsayının değer bölümünü döndürmesi gerekir `TotalNumberOfProducts` . Çağrısı, varsa `GetValueOrDefault()` Nullable tamsayı değerini döndürür; null atanabilir tamsayı, `null` ancak varsayılan tamsayı değeri olan 0 değerini döndürür.

## <a name="step-3-returning-the-precise-subset-of-records"></a>3. Adım: kayıtların kesin alt kümesini döndürme

Sonraki görevimiz, daha önce tartışılan başlangıç satırı dizinini ve en fazla satır değişkenlerini kabul eden ve uygun kayıtları döndüren DAL ve BLL 'de Yöntemler oluşturmaktır. Bunu yapmadan önce, gereken SQL betiğine ilk göz atalım. Bize bakan zorluk, yalnızca başlangıç satırı dizininden (ve en fazla kayıt numarası kayıt sayısına kadar) başlayarak yalnızca bu kayıtları döndürebilmemiz için tüm sonuçların tamamında disk belleğine alınan her satıra bir dizin atayabilmelidir.

Bu, veritabanı tablosunda bir satır dizini görevi gören bir sütun zaten varsa bir zorluk değildir. İlk bakışta, `Products` `ProductID` ilk ürüne `ProductID` 1, ikincisi 2 vb. sahip olduğu için tablo s alanının yeterli olduğunu düşündük. Ancak, bir ürünün silinmesi dizide bir boşluk bırakır, bu yaklaşım bu yaklaşımla sonuçlanır.

Bir satır dizinini verilerle sayfa ile bir şekilde ilişkilendirmek için kullanılan iki genel teknik vardır ve böylece kayıtların tam alt kümesini elde etmenizi sağlar:

- **SQL Server 2005 s `ROW_NUMBER()` kullanma ** SQL Server 2005 ' den yeni anahtar sözcüğü, `ROW_NUMBER()` anahtar sözcüğü bir sıralamayı, bir sıralama temelinde döndürülen her kayıtla ilişkilendirir. Bu sıralama, her satır için bir satır dizini olarak kullanılabilir.
- **Tablo değişkeni kullanarak ve `SET ROWCOUNT` ** SQL Server s [ `SET ROWCOUNT` deyimleri](https://msdn.microsoft.com/library/ms188774.aspx) , bir sorgunun sonlandırmadan önce kaç tane toplam kayıt tarafından işlenmesi gerektiğini belirtmek için kullanılabilir; [Tablo değişkenleri](http://www.sqlteam.com/item.asp?ItemID=9454) , [geçici tablolara](http://www.sqlteam.com/item.asp?ItemID=2029)aktarılan tablolu verileri tutan yerel T-SQL değişkenleridir. Bu yaklaşım, hem Microsoft SQL Server 2005 hem de 2000 SQL Server (ancak `ROW_NUMBER()` yaklaşım yalnızca SQL Server 2005 ile birlikte çalışarak) ile aynı şekilde çalışacaktır.  
  
  Buradaki fikir, `IDENTITY` verileri sayfalandırılmış olan tablonun birincil anahtarları için bir sütun ve sütun içeren bir tablo değişkeni oluşturmaktır. Daha sonra, verileri Sayfalanmış tablonun içeriği tablo değişkenine dökülür ve bu sayede tablodaki her bir kayıt için sıralı bir satır dizinini (sütun aracılığıyla) ilişkilendirmektir `IDENTITY` . Tablo değişkeni doldurulduktan sonra, `SELECT` tablo değişkeninde, temel tabloyla birleştirilmiş bir ifade, belirli kayıtları çekmek için yürütülebilir. `SET ROWCOUNT`Tablosu, tablo değişkenine döküme gereken kayıt sayısını akıllıca sınırlamak için kullanılır.  
  
  Bu yaklaşım verimlilik, istenen sayfa numarasını temel alır `SET ROWCOUNT` . değer, başlangıç satırı dizininin değeri ve en fazla satır sayısı olarak atanır. Verilerin ilk birkaç sayfası gibi düşük sayılı sayfalarda sayfalama yaparken bu yaklaşım çok verimlidir. Bununla birlikte, son görüntülenen sayfayı alırken varsayılan disk belleği benzeri performansı sergiler.

Bu öğretici, anahtar sözcüğünü kullanarak özel sayfalama uygular `ROW_NUMBER()` . Tablo değişkenini ve tekniği kullanma hakkında daha fazla bilgi için `SET ROWCOUNT` , [büyük sonuç kümelerinde sayfalama Için daha verimli bir yönteme](http://www.4guysfromrolla.com/webtech/042606-1.shtml)bakın.

`ROW_NUMBER()`Aşağıdaki sözdizimini kullanarak belirli bir sıralama üzerinde döndürülen her bir kayıtla birlikte bir derecelendirmeden ilişkilendirilen anahtar sözcük:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` belirtilen sıralamaya göre her bir kayıt için derecelendirmeyi belirten sayısal bir değer döndürür. Örneğin, her bir ürün için en pahalı olandan en az bir sıralama olduğunu görmek için aşağıdaki sorguyu kullanabiliriz:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

Şekil 5 ' te, Visual Studio 'da sorgu penceresi aracılığıyla çalıştırıldığında bu sorgu sonuçları gösterilmektedir. Ürünlerin fiyata göre sıralandığına ve her satır için bir fiyat derecesine sahip olduğuna unutmayın.

![Her döndürülen kayıt için fiyat Sıralaması dahildir](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**Şekil 5**: her döndürülen kayıt Için fiyat Sıralaması dahildir

> [!NOTE]
> `ROW_NUMBER()` SQL Server 2005 ' de bulunan çok sayıda yeni derecelendirme işlevlerinden yalnızca biridir. Diğer derecelendirme işlevleriyle birlikte hakkında daha ayrıntılı bir tartışma için `ROW_NUMBER()` , [Microsoft SQL Server 2005 Ile dereceli sonuçları geri döndürmeyi](http://www.4guysfromrolla.com/webtech/010406-1.shtml)okuyun.

Cümledeki belirtilen sütuna göre sonuçları derecelendirerek `ORDER BY` `OVER` ( `UnitPrice` Yukarıdaki örnekte), SQL Server sonuçları sırmalıdır. Bu, sonuçların tarafından sıralanan sütunlar üzerinde kümelenmiş bir dizin varsa veya kapsayan bir dizin varsa, ancak başka maliyetli bir işlem olduğunda hızlı bir işlemdir. Yeterince büyük sorguların performansını artırmaya yardımcı olmak için, sonuçların sıralandığı sütun için kümelenmemiş bir dizin eklemeyi göz önünde bulundurun. Performans konularına daha ayrıntılı bir bakış için bkz. [SQL Server 2005 ' de derecelendirme işlevleri ve performansı](http://www.sql-server-performance.com/ak_ranking_functions.asp) .

Tarafından döndürülen derecelendirme bilgileri `ROW_NUMBER()` `WHERE` yan tümcesinde doğrudan kullanılamaz. Ancak, bir türetilen tablo, sonuç döndürmek için kullanılabilir ve `ROW_NUMBER()` Bu da `WHERE` yan tümce içinde görünebilir. Örneğin, aşağıdaki sorgu, sonuç olarak ProductName ve BirimFiyat sütunlarını döndürmek için türetilmiş bir tablo kullanır `ROW_NUMBER()` ve ardından `WHERE` yalnızca fiyat derecesi 11 ile 20 arasında olan ürünleri döndürmek için bir yan tümce kullanır:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

Bu kavramı biraz daha uzun bir şekilde genişleterek, istenen başlangıç satırı dizini ve en fazla satır değerleri verilen belirli bir veri sayfasını almak için bu yaklaşımı kullanabilirsiniz:

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> Bu öğreticide daha sonra göreceğiniz gibi, *`StartRowIndex`* ObjectDataSource tarafından sağlanan değer sıfırdan başlayarak dizinlenir, ancak `ROW_NUMBER()` SQL Server 2005 tarafından döndürülen değer 1 ' den başlayarak dizinlenir. Bu nedenle, `WHERE` yan tümce `PriceRank` kesinlikle büyük *`StartRowIndex`* ve küçüktür veya eşittir olan kayıtları döndürür *`StartRowIndex`*  +  *`MaximumRows`* .

Artık `ROW_NUMBER()` Başlangıç satırı dizini ve en fazla satır değerleri verilen belirli bir veri sayfasını almak için nasıl kullanılabileceğinizi anladık. artık bu MANTıĞı dal ve BLL 'de yöntemler olarak uygulamanız gerekir.

Bu sorguyu oluştururken sonuçların derecelendirilir sıralamaya karar vermelidir; ürünlerin adlarını alfabetik sırada sıralamasına izin verin. Diğer bir deyişle, bu öğreticideki özel disk belleği uygulamasının de sıralanamayacak özel bir Sayfalanmış rapor oluşturabileceksiniz. Yine de, bir sonraki öğreticide, bu işlevselliğin nasıl sağlanabileceğiz.

Önceki bölümde, DAL yöntemini geçici bir SQL ifadesiyle oluşturduk. Ne yazık ki, TableAdapter Sihirbazı tarafından kullanılan Visual Studio 'da T-SQL ayrıştırıcısı, `OVER` işlev tarafından kullanılan söz dizimini beğenmez `ROW_NUMBER()` . Bu nedenle, bu DAL metodunu saklı yordam olarak oluşturuyoruz. Görünüm menüsünden Sunucu Gezgini seçin (veya CTRL + ALT + S tuşlarına basın) ve `NORTHWND.MDF` düğümü genişletin. Yeni bir saklı yordam eklemek için saklı yordamlar düğümüne sağ tıklayın ve yeni bir saklı yordam Ekle ' yi seçin (bkz. Şekil 6).

![Ürünler aracılığıyla sayfalama için yeni bir saklı yordam ekleyin](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**Şekil 6**: ürünler aracılığıyla sayfalama için yeni bir saklı yordam ekleyin

Bu saklı yordam iki tamsayı giriş parametresini kabul etmeli ve `@startRowIndex` Bu `@maximumRows` `ROW_NUMBER()` işlevi `ProductName` alan tarafından, yalnızca belirtilen satırdan daha büyük `@startRowIndex` ve şundan küçük veya eşit olan satırları döndürerek kullanır `@startRowIndex`  +  `@maximumRow` . Yeni saklı yordama aşağıdaki betiği girin ve ardından Kaydet simgesine tıklayarak saklı yordamı veritabanına ekleyin.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

Saklı yordamı oluşturduktan sonra, test etmek için bir dakikanızı ayırın. `GetProductsPaged` Sunucu Gezgini saklı yordam adına sağ tıklayın ve Yürüt seçeneğini belirleyin. Ardından, Visual Studio sizden giriş parametrelerini `@startRowIndex` ve `@maximumRow` öğeleri (bkz. Şekil 7) ister. Farklı değerleri deneyin ve sonuçları inceleyin.

![@startRowIndexVe parametreleri için bir değer girin @maximumRows](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>Şekil 7</strong>: @startRowIndex ve parametreleri için bir değer girin @maximumRows

Bu giriş parametreleri değerlerini seçtikten sonra, çıkış penceresinde sonuçlar gösterilir. Şekil 8 ' de hem hem de parametreleri için 10 ' a geçirilirken sonuçlar gösterilmektedir `@startRowIndex` `@maximumRows` .

[![Verilerin Ikinci sayfasında görünecek kayıtlar döndürülür](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**Şekil 8**: verilerin Ikinci sayfasında görünen kayıtlar döndürülür ([tam boyutlu görüntüyü görüntülemek için tıklayın](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png))

Bu saklı yordam oluşturulduktan sonra, yöntemi oluşturmaya hazırız `ProductsTableAdapter` . `Northwind.xsd`Yazılan veri kümesini açın, ' a sağ tıklayın `ProductsTableAdapter` ve sorgu Ekle seçeneğini belirleyin. Geçici bir SQL ifadesini kullanarak sorgu oluşturmak yerine, mevcut bir saklı yordamı kullanarak oluşturun.

![Varolan bir saklı yordamı kullanarak DAL metodunu oluşturma](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**Şekil 9**: varolan bir saklı yordamı kullanarak dal metodunu oluşturma

Ardından, çağrılacak saklı yordamı seçeceğiz. `GetProductsPaged`Açılan listeden saklı yordamı seçin.

![Açılan listeden GetProductsPaged saklı yordamını seçin](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**Şekil 10**: açılan listeden GetProductsPaged saklı yordamını seçin

Ardından, bir sonraki ekranda, saklı yordam tarafından döndürülen veri türünü, tek bir değeri veya değeri olmadığını sorar. `GetProductsPaged`Saklı yordam birden çok kayıt döndürebileceğinizden bu yana tablo verileri döndürdüğünü belirtin.

![Saklı yordamın tablo verilerini döndürdüğünü belirtir](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**Şekil 11**: saklı yordamın tablo verilerini döndürdüğünü belirtin

Son olarak, oluşturulmasını istediğiniz yöntemlerin adlarını belirtin. Önceki öğreticilerimizde olduğu gibi, bir DataTable doldur ve bir DataTable döndüren yöntemleri kullanarak devam edin. İlk yöntemi `FillPaged` ve ikincisini adlandırın `GetProductsPaged` .

![Yöntemleri Filldisk belleğine ve GetProductsPaged olarak adlandırın](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**Şekil 12**: yöntemleri filldisk belleğine ve GetProductsPaged olarak adlandırın

Belirli bir ürün sayfasını döndürmek için bir DAL yöntemi oluşturmalarının yanı sıra, BLL 'de bu işlevleri de sağlamaları gerekir. DAL yöntemi gibi, BLL s GetProductsPaged yöntemi, başlangıç satırı dizinini ve en yüksek satırları belirtmek için iki tamsayı girişi kabul etmelidir ve yalnızca belirtilen aralıkta kalan kayıtları döndürmelidir. Bu tür bir BLL yöntemi oluşturun, örneğin, yalnızca DAL s GetProductsPaged yöntemine çağrı yapan ProductsBLL sınıfında:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

BLL metodu giriş parametreleri için herhangi bir ad kullanabilirsiniz, ancak kısa bir süre sonra da göreceğiniz şekilde, `startRowIndex` `maximumRows` Bu yöntemi kullanmak üzere bir ObjectDataSource 'u yapılandırırken daha fazla çalışma ve ABD 'de tasarruf eteceğiz.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>4. Adım: özel sayfalama kullanmak için ObjectDataSource yapılandırma

Belirli bir kayıt alt kümesine erişim için BLL ve DAL yöntemleriyle, özel sayfalama kullanarak alttaki kayıtları aracılığıyla sayfaları veren bir GridView denetimi oluşturmaya hazırız. `EfficientPaging.aspx` `PagingAndSorting` ' I klasörden açın, sayfaya bir GridView ekleyin ve yeni bir ObjectDataSource denetimi kullanmak üzere yapılandırın. Geçmiş öğreticilerimizde, genellikle sınıf s metodunu kullanacak şekilde yapılandırılmış ObjectDataSource vardı `ProductsBLL` `GetProducts` . Bununla birlikte, yöntemi `GetProductsPaged` veritabanındaki tüm ürünleri döndürdüğünden, bunun yerine yöntemi kullanmak istiyoruz `GetProducts` . bunun yerine *all* `GetProductsPaged` yalnızca belirli bir kayıt alt kümesini döndürür.

![ObjectDataSource 'ı ProductsBLL Class s GetProductsPaged metodunu kullanacak şekilde yapılandırma](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**Şekil 13**: ObjectDataSource 'ı ProductsBLL Class s GetProductsPaged yöntemini kullanacak şekilde yapılandırma

Salt okunurdur bir GridView oluşturuyoruz, INSERT, UPDATE ve DELETE sekmelerinde (None) yöntem açılan listesini ayarlamak için bir dakikanızı ayırın.

Ardından, ObjectDataSource Sihirbazı, `GetProductsPaged` Yöntem `startRowIndex` ve `maximumRows` giriş parametresi değerlerinin kaynaklarını ister. Bu giriş parametreleri aslında GridView tarafından otomatik olarak ayarlanır, bu nedenle kaynak kümesini None olarak bırakıp son ' a tıklayın.

![Giriş parametresi kaynaklarını hiçbiri olarak bırak](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**Şekil 14**: giriş parametre kaynaklarını yok olarak bırakın

ObjectDataSource Sihirbazı 'nı tamamladıktan sonra GridView, ürün verileri alanlarının her biri için bir BoundField veya CheckBoxField içerecektir. GridView s görünümünü uygun gördüğünüz şekilde uyarlayabilirsiniz. Yalnızca,,,, `ProductName` `CategoryName` `SupplierName` `QuantityPerUnit` ve `UnitPrice` boundfields alanlarını görüntülemeyi tercih ediyorum. Ayrıca, GridView 'u akıllı etiketinde sayfalama etkinleştir onay kutusunu işaretleyerek sayfalamayı destekleyecek şekilde yapılandırın. Bu değişikliklerden sonra, GridView ve ObjectDataSource tanımlayıcı biçimlendirme biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

Ancak sayfayı bir tarayıcı aracılığıyla ziyaret ederseniz, GridView nerede bulunur.

![GridView görüntülenmiyor](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**Şekil 15**: GridView görüntülenmiyor

ObjectDataSource, `GetProductsPaged` `startRowIndex` ve giriş parametrelerinin her ikisi için de şu anda 0 kullandığından, GridView yok `maximumRows` . Bu nedenle, ortaya çıkan SQL sorgusu kayıt döndürmüyor ve bu nedenle GridView görüntülenmez.

Bu sorunu gidermek için, ObjectDataSource 'u özel sayfalama kullanacak şekilde yapılandırmamız gerekir. Bu, aşağıdaki adımlarda gerçekleştirilebilir:

1. **ObjectDataSource 'un bu `EnablePaging` `true` özelliği** , iki ek parametreye geçmesi gereken ObjectDataSource olduğunu gösterir `SelectMethod` : biri başlangıç satırı dizinini ( [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) ) ve diğeri ise en fazla satırları () belirtmek için [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) .
2. **ObjectDataSource ve `StartRowIndexParameterName` `MaximumRowsParameterName` özellikleri uygun şekilde ayarlayın** `StartRowIndexParameterName` ve `MaximumRowsParameterName` özellikleri `SelectMethod` Özel sayfalama amacıyla öğesine geçirilen giriş parametrelerinin adlarını belirtir. Varsayılan olarak, bu parametre adları `startIndexRow` ve `maximumRows` , `GetProductsPaged` BLL 'de yöntemi oluştururken giriş parametreleri için bu değerleri kullandım. Ve gibi BLL s yöntemi için farklı parametre adları kullanmayı seçtiyseniz `GetProductsPaged` `startIndex` `maxRows` , örneğin, ObjectDataSource `StartRowIndexParameterName` ve `MaximumRowsParameterName` özellikleri uygun şekilde ayarlamanız gerekir (örneğin, startIndex for `StartRowIndexParameterName` ve MaxRows gibi `MaximumRowsParameterName` ).
3. **ObjectDataSource 'un [ `SelectCountMethod` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) , `TotalNumberOfProducts` ** `ProductsBLL` `TotalNumberOfProducts` bir sorgu yürüten dal yöntemi kullanarak, disk belleğine alınan toplam kayıt sayısını döndüren, (), sınıf s yönteminin toplam kaç kayıt sayısını döndürdüğünü geri çekmek için bir yöntem olarak ayarlayın `SELECT COUNT(*) FROM Products` . Bu bilgiler, disk belleği arabirimini doğru bir şekilde işlemek için ObjectDataSource tarafından gereklidir.
4. Sihirbaz aracılığıyla ObjectDataSource 'u **yapılandırırken, Visual `startRowIndex` `maximumRows` `<asp:Parameter>` ** Studio `<asp:Parameter>` Yöntem giriş parametreleri için otomatik olarak iki öğe ekledi `GetProductsPaged` . Olarak ayarlandığında `EnablePaging` `true` , bu parametreler otomatik olarak geçirilir; bildirim temelli sözdiziminde de görünüyorsa, ObjectDataSource yönteme *dört* parametre `GetProductsPaged` ve yönteme iki parametre geçirmeye çalışacaktır `TotalNumberOfProducts` . Bu öğeleri kaldırmayı unutursanız `<asp:Parameter>` , sayfayı bir tarayıcı aracılığıyla ziyaret ederken şu şekilde bir hata iletisi alırsınız: *' ObjectDataSource1 ' ObjectDataSource, şu parametrelere sahip genel olmayan bir ' TotalNumberOfProducts ' yöntemi bulamadı: StartRowIndex, MaximumRows*.

Bu değişiklikleri yaptıktan sonra, ObjectDataSource 'un bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

`EnablePaging`Ve `SelectCountMethod` özelliklerinin ayarlandığını ve `<asp:Parameter>` öğelerin kaldırıldığını unutmayın. Şekil 16, bu değişiklikler yapıldıktan sonra Özellikler penceresi ekran görüntüsünü gösterir.

![Özel sayfalama kullanmak için, ObjectDataSource denetimini yapılandırın](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**Şekil 16**: özel sayfalama kullanmak Için, ObjectDataSource denetimini yapılandırın

Bu değişiklikleri yaptıktan sonra bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Alfabetik olarak sıralanan 10 ürün listelendiğini görmeniz gerekir. Verileri tek seferde bir sayfada ilerlemek için bir dakikanızı ayırın. Varsayılan sayfalama ve özel sayfalama arasındaki Son Kullanıcı perspektifinden, özel sayfalama, yalnızca belirli bir sayfa için görüntülenmesi gereken kayıtları aldığı için, büyük miktarlarda veri aracılığıyla daha verimli sayfalar sağlar.

[![Ürün adına göre sıralanmış veriler özel sayfalama kullanılarak Sayfalanmalıdır](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**Şekil 17**: ürün adına göre sıralanmış veriler özel sayfalama ([tam boyutlu görüntüyü görüntülemek Için tıklayın](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png)) kullanılarak sayfalanmalıdır.

> [!NOTE]
> Özel sayfalama ile, ObjectDataSource tarafından döndürülen sayfa sayısı değeri `SelectCountMethod` GridView 'un Görünüm durumunda depolanır. ,,, Koleksiyonu ve benzeri diğer GridView değişkenleri, `PageIndex` `EditIndex` `SelectedIndex` `DataKeys` GridView 'un özelliğinin değerine bakılmaksızın kalıcı olan *Denetim durumunda*depolanır `EnableViewState` . `PageCount`Değer Görünüm durumu kullanılarak geri göndermeler arasında kalıcı olduğundan, son sayfaya gidebileceğiniz bir bağlantı içeren bir sayfalama arabirimi kullanılırken, GridView 'un görünüm durumunun etkinleştirilmesi zorunludur. (Sayfalama arabiriminiz son sayfaya doğrudan bir bağlantı içermiyorsa, görünüm durumunu devre dışı bırakabilirsiniz.)

Son sayfa bağlantısına tıkladığınızda geri göndermeye neden olur ve GridView 'un özelliğini güncelleştirmesini sağlar `PageIndex` . Son sayfa bağlantısına tıklandıysanız, GridView kendi özelliğini `PageIndex` özelliğinden daha küçük bir değere atar `PageCount` . Görünüm durumu devre dışı bırakıldığında, `PageCount` değer geri göndermeler arasında kaybedilir ve `PageIndex` bunun yerine en büyük tamsayı değeri atanır. Daha sonra GridView, ve özelliklerini çarparak başlangıç satırı dizinini saptamaya çalışır `PageSize` `PageCount` . Bu `OverflowException` , ürünün izin verilen en büyük tamsayı boyutunu aşması ile sonuçlanır.

## <a name="implement-custom-paging-and-sorting"></a>Özel sayfalama ve sıralama uygulama

Geçerli özel sayfalama uygulamamız, saklı yordam oluştururken verilerin disk belleğine alınan sırasının statik olarak belirtilmesini gerektirir `GetProductsPaged` . Ancak, sayfalama etkinleştir seçeneğinin yanı sıra GridView s akıllı etiketinin sıralamayı etkinleştir onay kutusunu içerdiğini Not alabilirsiniz. Ne yazık ki, geçerli özel sayfalama uygulamamız ile GridView 'a sıralama desteği eklemek, yalnızca şu anda görüntülenen veri sayfasındaki kayıtları sıralayacak. Örneğin, GridView 'u sayfalama 'yi de destekleyecek şekilde yapılandırırsanız, ilk veri sayfasını görüntülerken, ürün adına göre azalan sırada sıralama yaparken, sayfa 1 ' deki ürünlerin sırası tersine alınır. Şekil 18 ' de gösterildiği gibi, geriye doğru alfabetik 71 sırada sıralama yaparken ilk ürün gibi Carnarvon Tiger 'ları gösterir. sıralamada yalnızca ilk sayfadaki kayıtlar göz önünde bulundurululur.

[![Yalnızca geçerli sayfada gösterilen veriler sıralanır](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**Şekil 18**: yalnızca geçerli sayfada gösterilen veriler sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))

Sıralama yalnızca geçerli veri sayfası için geçerlidir çünkü sıralama, veriler BLL yönteminden alındıktan sonra gerçekleştiğinden `GetProductsPaged` ve bu yöntem yalnızca belirli bir sayfa için bu kayıtları döndürüyor. Sıralamayı doğru şekilde uygulamak için sıralama ifadesini yöntemine geçirmemiz gerekir, böylece veriler, `GetProductsPaged` verilerin belirli bir sayfasını döndürmeden önce uygun şekilde derecelendirilir. Bunu bir sonraki öğreticimizde nasıl gerçekleştireceğinizi öğreneceğiz.

## <a name="implementing-custom-paging-and-deleting"></a>Özel sayfalama uygulama ve silme

Özel disk belleği tekniklerini kullanarak verileri sayfalandırılmış bir GridView 'da silme işlevini etkinleştirirseniz, son sayfadan son kayıt silinirken GridView 'un, GridView 'un uygun şekilde azaltılamaması yerine nasıl kaybolduğunu görürsünüz `PageIndex` . Bu hatayı yeniden oluşturmak için, yalnızca yeni oluşturduğumuz öğreticide silmeyi etkinleştirin. Bir kerede 81 ürün, 10 ürün ile sayfalama yaptığımız için tek bir ürün görmeniz gereken son sayfaya (sayfa 9) gidin. Bu ürünü silin.

Son ürünü sildikten sonra, GridView otomatik olarak sekizinci sayfasına *gitmeli* ve bu tür işlevlere varsayılan sayfalama söz konusu olduğunda izin verilir. Ancak, özel sayfalama ile son sayfadaki son ürünü sildikten sonra, GridView yalnızca ekrandan kaybolur. Bunun *tam nedeni, bu* öğreticinin kapsamının ötesinde bir bit olur; Bu sorunun kaynağına göre alt düzey Ayrıntılar için [Özel sayfalama ile bir GridView 'Dan son sayfadaki son kaydı silme](http://scottonwriting.net/sowblog/posts/7326.aspx) bölümüne bakın. Özet içinde, Sil düğmesine tıklandığında GridView tarafından gerçekleştirilen aşağıdaki adım dizisi nedeniyle bu ayrıntıları izleyin:

1. Kaydı silme
2. Belirtilen ve için görüntülenecek uygun kayıtları al `PageIndex``PageSize`
3. `PageIndex`Veri kaynağındaki veri sayfalarının sayısını aşmadığından emin olmak için kontrol edin; varsa, GridView s özelliğini otomatik olarak azaltır `PageIndex`
4. 2. adımda elde edilen kayıtları kullanarak GridView 'a uygun veri sayfasını bağlama

Sorun, adım 2 ' de, `PageIndex` yakalayıp görüntülenecek kayıtlar, `PageIndex` tek kaydı yeni silinen son sayfanın hala bulunduğu durumlarda kullanılır. Bu nedenle, adım 2 ' de, verilerin son sayfası artık hiçbir kayıt bulunmadığından *hiçbir kayıt döndürülmez* . Daha sonra, adım 3 ' te GridView, `PageIndex` özelliğinin veri kaynağındaki toplam sayfa sayısından daha büyük olduğunu (son sayfadaki son kaydı sildiğimiz için) ve bu nedenle `PageIndex` özelliğini azaltır. 4. adımda GridView, adım 2 ' de alınan verilere kendisini bağlamayı dener; Ancak, 2. adımda hiçbir kayıt döndürülmedi, bu nedenle boş bir GridView ile sonuçlanır. Varsayılan sayfalama ile bu sorun, 2. adımdaki *Tüm* kayıtlar veri kaynağından alındığından, bu sorun bir yüzey değildir.

Bunu yapmak için iki seçeneğiniz vardır. Birincisi, `RowDeleted` Yeni silinen sayfada kaç kaydın görüntülendiğini belirleyen GridView s olay işleyicisi için bir olay işleyicisi oluşturmaktır. Yalnızca bir kayıt varsa, yeni silinen kayıt en son bir tane olmalıdır ve GridView 'u azaltmemiz gerekiyor `PageIndex` . Tabii ki, yalnızca `PageIndex` silme işlemi başarılı olduysa, özelliğin olduğundan belirlenebilir olan öğesini güncelleştirmek istiyoruz `e.Exception` `null` .

Bu yaklaşım, `PageIndex` 1. adımdan sonra ancak adım 2 ' den önce güncelleştiğinden işe yarar. Bu nedenle, adım 2 ' de, uygun kayıt kümesi döndürülür. Bunu gerçekleştirmek için aşağıdaki gibi bir kod kullanın:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

Alternatif bir geçici çözüm, ObjectDataSource 'un olayı için bir olay işleyicisi oluşturmak `RowDeleted` ve `AffectedRows` özelliğini 1 değerine ayarlamak içindir. Adım 1 ' deki kayıt silindikten sonra (ancak adım 2 ' deki verileri yeniden almadan önce), GridView, `PageIndex` bir veya daha fazla satır işlemden etkilenirse, özelliğini güncelleştirir. Ancak, `AffectedRows` özelliği ObjectDataSource tarafından ayarlanmadı ve bu nedenle bu adım atlanır. Bu adımın bir yolu, `AffectedRows` silme işlemi başarıyla tamamlanırsa özelliği el ile ayarlamaya yönelik bir yoldur. Bu, aşağıdakiler gibi kod kullanılarak gerçekleştirilebilir:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

Bu olay işleyicilerinin her ikisi için de kod, örneğin arka plan kod sınıfında bulunabilir `EfficientPaging.aspx` .

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>Varsayılan ve özel sayfalama performansını karşılaştırma

Özel sayfalama yalnızca gerekli kayıtları aldığı için, varsayılan sayfalama görüntülenen her sayfanın *Tüm* kayıtlarını döndürdüğünden, özel sayfalama varsayılan sayfalamadan daha etkilidir. Ancak özel sayfalama ne kadar verimli? Varsayılan disk belleğine özel disk belleğine geçerek performans artışı ne şekilde görülebilir?

Ne yazık ki, burada hiç bir boyut tüm yanıta sığar. Performans kazancı, bir dizi etkene bağlıdır, en belirgin ikisi üzerinde disk belleğine alınan kayıt sayısı ve veritabanı sunucusuna ve Web sunucusu ile veritabanı sunucusu arasındaki iletişim kanallarına yerleştirilir. Yalnızca birkaç düzine kayıt içeren küçük tablolar için performans farkı göz ardı edilebilir olmayabilir. Büyük tablolar için, binlerce ila yüzlerce satır, ancak performans farkı ise dar olur.

[SQL Server 2005 ile ASP.NET 2,0 ' de özel sayfalama](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx), bir bir veritabanı 50.000 tablosu aracılığıyla disk belleği ile sayfalama yaparken, bu iki sayfalama tekniği arasındaki performans farklarını sergilediğim bazı performans testlerini içeren bir makale. Bu testlerde, sorgu SQL Server düzeyinde ( [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)kullanarak) ve ASP.NET sayfasında [ASP.net s izleme özelliklerini](https://msdn.microsoft.com/library/y13fw6we.aspx)kullanarak sorguyu yürütmek için her iki zamanı da inceledim. Bu testlerin, tek bir etkin kullanıcıyla geliştirme kutum üzerinde çalıştırıldığını ve bu nedenle bilimsel olduğunu ve tipik web sitesi yükleme düzenlerini benzemeyeceğini göz önünde bulundurun. Ne olursa olsun, sonuçlar yeterince büyük miktarda verilerle çalışırken varsayılan ve özel sayfalama yürütme sürelerindeki göreli farklılıkları gösterir.

|  | **Ort. süre (sn)** | **Okumalar** |
| --- | --- | --- |
| **Varsayılan sayfalama SQL Profiler** | 1,411 | 383 |
| **Özel sayfalama SQL Profiler** | 0,002 | 29 |
| **Varsayılan sayfalama ASP.NET Izleme** | 2,379 | *Yok* |
| **Özel sayfalama ASP.NET Izleme** | 0,029 | *Yok* |

Görebileceğiniz gibi, belirli bir veri sayfasını almak, ortalama olarak 354 daha az okuma ve tamamlanma süresinin bir kesilişinde tamamlanmakta olması gerekir. ASP.NET sayfasında, özel sayfa, varsayılan sayfalama kullanılırken geçen<sup>sürenin 1/100 '</sup> a yakın sürede işleme sağlayamıştı. Bu testleri kendi ortamınızda yeniden oluşturmak için indirebileceğiniz kod ve veritabanıyla birlikte bu sonuçlarla ilgili daha fazla bilgi için [makaleme](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) bakın.

## <a name="summary"></a>Özet

Varsayılan sayfalama, veri Web denetimi 'nin akıllı etiketinde yalnızca Sayfalamayı Etkinleştir onay kutusunu işaretleyin, ancak bu tür kolaylık da performans maliyetine girer. Varsayılan sayfalama ile, bir Kullanıcı herhangi bir veri sayfası istediğinde, yalnızca küçük bir kesri gösterilse bile *Tüm* kayıtlar döndürülür. Bu performans yüküyle mücadele etmek için, ObjectDataSource alternatif bir sayfalama seçeneği özel sayfalama seçeneği sunar.

Özel sayfalama, yalnızca görüntülenmesi gereken kayıtları alarak varsayılan sayfalama performansı sorunları üzerinde gelişirken, özel sayfalama uygulamak daha da dahil olur. İlk olarak, bir sorgu, istenen kayıt alt kümesine doğru şekilde (ve etkili bir şekilde) yazılmalıdır. Bu, çeşitli yollarla gerçekleştirilebilir; Bu öğreticide incelenen tek bir `ROW_NUMBER()` işlev, sonuçları derecelendirmek için SQL Server 2005 s yeni işlevini kullanmak ve ardından yalnızca derecelendirmesi belirtilen bir aralık dahilinde olan sonuçları döndürmek için kullanılır. Ayrıca, üzerinden disk belleğine alınan toplam kayıt sayısını belirlemede bir yol eklememiz gerekir. Bu DAL ve BLL yöntemlerini oluşturduktan sonra Ayrıca, ObjectDataSource 'un kaç toplam kayıt sayfalanmakta olduğunu belirleyebilmesi ve başlangıç satırı dizinini ve en yüksek satır değerlerini BLL 'ye doğru bir şekilde geçebilmesini sağlayacak şekilde yapılandırmamız gerekir.

Özel sayfalama uygulamak için birkaç adım gerekir ve varsayılan disk belleği olarak neredeyse basit değildir. özel sayfalama, yeterince büyük miktarda veri ile sayfalama yaparken bir zorunludur. Sonuçlar incelendiği için, özel sayfalama, ASP.NET sayfa işleme süresinin sonuna kadar bir azalma olabilir ve veritabanı sunucusundaki yükü bir veya daha fazla büyüklük ile açabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [4GuysFromRolla.com](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Adresinden erişilebilir [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla bulunabilir [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

> [!div class="step-by-step"]
> [Önceki](paging-and-sorting-report-data-vb.md) 
>  [Sonraki](sorting-custom-paged-data-vb.md)
