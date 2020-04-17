---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET Web Sayfaları (Razor) ile Grafikte Veri Görüntüleme | Microsoft Dokümanlar
author: rick-anderson
description: Bu bölümde, grafikte verilerin nasıl görüntüleneneaçıklanmaktadır. Önceki bölümlerde, verileri el ile ve ızgarada görüntülemeyi öğrendiniz. Bu bölüm açıklar ...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542891"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>ASP.NET Web Sayfalarıyla Grafikte Veri Görüntüleme (Jilet)

[Microsoft](https://github.com/microsoft) tarafından

> Bu makalede, `Chart` yardımcıyı kullanarak ASP.NET bir Web Sayfaları (Jilet) web sitesinde verileri görüntülemek için grafiğin nasıl kullanılacağı açıklanmaktadır.
> 
> **Ne öğreneceksiniz:**
> 
> - Grafikte veri görüntüleme.
> - Yerleşik temaları kullanarak grafikleri stile şekillendirme.
> - Grafiklerin nasıl kaydedilen ve daha iyi performans için nasıl önbelleğe kazanılabildiği.
> 
> Bu makalede tanıtılan ASP.NET programlama özellikleri şunlardır:
> 
> - `Chart` Yardımcı.
> 
> > [!NOTE]
> > Bu makaledeki bilgiler ASP.NET Web Sayfaları 1.0 ve Web Sayfaları 2 için geçerlidir.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Grafik Yardımcısı

Verilerinizi grafik biçiminde görüntülemek istediğinizde, yardımcıyı `Chart` kullanabilirsiniz. Yardımcı, `Chart` çeşitli grafik türlerinde veri görüntüleyen bir görüntü işleyebilir. Biçimlendirme ve etiketleme için birçok seçeneği destekler. Yardımcı, `Chart` Microsoft Excel veya diğer araçlardan aşina olabileceğiniz tüm grafik türleri, alan grafikleri, çubuk grafikler, sütun grafikleri, satır grafikleri ve pasta grafikleri &#8212; ve stok grafikleri gibi daha özel grafikler de dahil olmak üzere 30'dan fazla grafik türünü işleyebilir.

| **Alan grafiği** ![Açıklaması: Alan grafiği tipinin resmi](7-displaying-data-in-a-chart/_static/image1.jpg) | **Çubuk grafik** ![Açıklama: Çubuk grafik türünün resmi](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Sütun grafiği** ![Açıklama: Sütun grafik türünün resmi](7-displaying-data-in-a-chart/_static/image3.jpg) | **Çizgi grafiği** ![Açıklama: Çizgi grafiği türünün resmi](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Pasta grafiği** ![Açıklama: Pasta grafik türünün resmi](7-displaying-data-in-a-chart/_static/image5.jpg) | **Stok grafiği** ![Açıklaması: Stok grafiği türünün resmi](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Grafik Öğeleri

Grafikler verileri ve göstergeler, eksenler, seriler ve benzeri ek öğeleri gösterir. Aşağıdaki resim, yardımcıyı kullandığınızda özelleştirebileceğiniz grafik öğelerinin `Chart` çoğunu gösterir. Bu makalede, bu öğelerin bazılarını (tümü değil) nasıl ayarlayabileceğinizgösterilmektedir.

![Açıklama: Grafik öğelerini gösteren resim](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Verilerden Grafik Oluşturma

Grafikte görüntülediğiniz veriler bir diziden, veritabanından döndürülen sonuçlardan veya XML dosyasındaki verilerden olabilir.

### <a name="using-an-array"></a>Dizi Kullanma

ASP.NET Web Sayfaları Programlamaya Giriş'te açıklandığı gibi, [Jilet Sözdizimini kullanarak](https://go.microsoft.com/fwlink/?LinkId=202890)bir dizi benzer öğelerin bir koleksiyonunu tek bir değişkende depolamanızı sağlar. Dizileri, grafiğinize eklemek istediğiniz verileri içerecek şekilde kullanabilirsiniz.

Bu yordam, varsayılan grafik türünü kullanarak diziler halindeki verilerden nasıl grafik oluşturabileceğinizi gösterir. Ayrıca, sayfa içinde grafiğin nasıl görüntülenebildiğini de gösterir.

1. *ChartArrayBasic.cshtml*adlı yeni bir dosya oluşturun.
2. Varolan içeriği aşağıdakilerle değiştirin: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Kod önce yeni bir grafik oluşturur ve genişliğini ve yüksekliğini ayarlar. Yöntemi kullanarak grafik başlığını `AddTitle` belirtirsiniz. Veri eklemek için `AddSeries` yöntemi kullanırsınız. Bu örnekte, `name`yöntemin `xValue`, `yValues` , `AddSeries` ve parametrelerini kullanırsınız. `name` Parametre grafik göstergesinde görüntülenir. Parametre, `xValue` grafiğin yatay ekseni boyunca görüntülenen bir veri dizisi içerir. Parametre, `yValues` grafiğin dikey noktalarını çizmek için kullanılan bir veri dizisi içerir.

    Yöntem `Write` aslında grafiği işler. Bu durumda, bir grafik türü belirtmediğiniz `Chart` için, yardımcı varsayılan grafiği işler, bu da bir sütun grafiğidir.
3. Sayfayı tarayıcıda çalıştırın. Tarayıcı grafiği görüntüler. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Grafik Verileri için Veritabanı Sorgusu Kullanma

Grafik oluşturmak istediğiniz bilgiler bir veritabanındaysa, bir veritabanı sorgusu çalıştırabilir ve ardından grafiği oluşturmak için sonuçlardan gelen verileri kullanabilirsiniz. Bu yordam, web sayfaları sitelerinde bir [Veritabanı ile çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=202893)makalesinde oluşturulan veritabanından verileri nasıl okuyup görüntüleyebilirASP.NET.

1. Klasör zaten yoksa, web sitesinin köküne bir *Uygulama\_Veri* klasörü ekleyin.
2. *Uygulama\_Verileri* klasörüne, [ASP.NET Web Sayfaları Sitelerinde Veritabanıyla Çalışmaya Giriş'te](https://go.microsoft.com/fwlink/?LinkId=202893)açıklanan *SmallBakery.sdf* adlı veritabanı dosyasını ekleyin.
3. *ChartDataQuery.cshtml*adında yeni bir dosya oluşturun.
4. Varolan içeriği aşağıdakilerle değiştirin:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Kod ilk Olarak SmallBakery veritabanını açar ve `db`onu . Bu değişken, `Database` veritabanından okumak ve yazmak için kullanılabilecek bir nesneyi temsil eder. Ardından, kod her ürünün adını ve fiyatını almak için bir SQL sorgusu çalıştırın. Kod yeni bir grafik oluşturur ve grafik `DataBindTable` yöntemini çağırarak veritabanı sorgusunu ona geçirir. Bu yöntem iki parametre alır: `dataSource` parametre sorgudaki veriler `xField` içindir ve parametre grafiğin x ekseni için hangi veri sütununun kullanılacağını ayarlamanızı sağlar.

    `DataBindTable` Yöntemi kullanmaya alternatif olarak, yardımcının `AddSeries` yöntemini `Chart` kullanabilirsiniz. Yöntem, `AddSeries` parametreleri `xValue` ve `yValues` parametreleri ayarlamanızı sağlar. Örneğin, aşağıdaki gibi `DataBindTable` yöntemi kullanmak yerine:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Bu yöntemi `AddSeries` kullanabilirsiniz:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Her ikisi de aynı sonuçları verir. Grafik `AddSeries` türünü ve verilerini daha açık bir şekilde belirtebildiğiniz `DataBindTable` için yöntem daha esnektir, ancak ekstra esnekliğe ihtiyacınız yoksa yöntem daha kolaydır.
5. Sayfayı tarayıcıda çalıştırın. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML Verilerini Kullanma

Grafik için üçüncü seçenek grafik için veri olarak bir XML dosyası kullanmaktır. Bu, XML dosyasının XML yapısını açıklayan bir şema dosyası *(.xsd* dosyası) da bulunmasını gerektirir. Bu yordam, bir XML dosyasından verileri nasıl okuyabileceğinizi gösterir.

1. *\_App Data* klasöründe *data.xml*adında yeni bir XML dosyası oluşturun.
2. Varolan XML'i, kurgusal bir şirketteki çalışanlar la ilgili bazı XML verileri olan aşağıdakilerle değiştirin. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. *App\_Data* klasöründe *data.xsd*adında yeni bir XML dosyası oluşturun. (Bu süre uzantısı *.xsd*olduğunu unutmayın .)
4. Varolan XML'i aşağıdakilerle değiştirin: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. Web sitesinin kökünde *ChartDataXML.cshtml*adında yeni bir dosya oluşturun.
6. Varolan içeriği aşağıdakilerle değiştirin: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Kod önce bir `DataSet` nesne oluşturur. Bu nesne, XML dosyasından okunan verileri yönetmek ve şema dosyasındaki bilgilere göre düzenlemek için kullanılır. (Kodun üst kısmında ifadenin `using SystemData`yer aldığına dikkat edin. Bu `DataSet` nesne ile çalışabilmek için gereklidir. Daha fazla bilgi için, bu makalenin ilerleyen saatlerinde [ &quot;Ifadeleri ve Tam Nitelikli Adları&quot; Kullanma'ya](#SB_UsingStatements) bakın.)

    Ardından, kod veri `DataView` kümesini temel alan bir nesne oluşturur. Veri görünümü, grafiğin &#8212; bağlayabileceği, okunan ve çizilebilen bir nesne sağlar. Grafik, dizi verilerini grafikyaparken `AddSeries` daha önce gördüğünüz gibi, bu kez `xValue` `yValues` parametrenin `DataView` nesneye ayarlanması dışında, yöntemi kullanarak verilere bağlanır.

    Bu örnek, belirli bir grafik türünü nasıl belirtdiğinizi de gösterir. `AddSeries` Yönteme veri eklendiğinde, `chartType` parametre de bir pasta grafiği görüntülemek üzere ayarlanır.
7. Sayfayı tarayıcıda çalıştırın. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Kullanma" Deyimleri ve Tam Nitelikli İsimler
> 
> Web Sayfalarını Jilet sözdizimi ile ASP.NET .NET Framework binlerce bileşenden (sınıf) oluşur. Tüm bu sınıflarla çalışmayı yönetilebilir hale getirmek için, bir şekilde kitaplıklar gibi *ad boşlukları*halinde düzenlenirler. Örneğin, `System.Web` ad alanı tarayıcı/sunucu iletişimini destekleyen `System.Xml` sınıflar içerir, ad alanı XML dosyaları oluşturmak `System.Data` ve okumak için kullanılan sınıfları içerir ve ad alanı verilerle çalışmanıza izin veren sınıflar içerir.
> 
> .NET Framework'de belirli bir sınıfa erişmek için kodun sadece sınıf adını değil, sınıfın içinde bulunduğu ad alanını da bilmesi gerekir. Örneğin, `Chart` yardımcıyı kullanabilmek için kodun ad `System.Web.Helpers.Chart` alanını (`System.Web.Helpers``Chart`) sınıf adı yla birleştiren sınıfı bulması gerekir. Bu, sınıfın *tam nitelikli* adı &#8212; .NET Framework'ün enginliği içinde tam ve net konumu olarak bilinir. Kod olarak, bu aşağıdaki gibi görünür:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Ancak, bir sınıfa veya yardımcıya başvurmak istediğiniz her seferinde bu uzun, tam nitelikli adları kullanmak zorunda olmak hantal (ve hataya yatkındır). Bu nedenle, sınıf adlarını kullanmayı kolaylaştırmak için, ilgilendiğiniz ad alanlarını *içe aktarabilirsiniz,* ki bu genellikle .NET Framework'deki birçok ad alanı arasından sadece bir avuç tır. Bir ad alanı aldıysanız, tam nitelikli ad (`Chart``System.Web.Helpers.Chart`) yerine sadece bir sınıf adı kullanabilirsiniz. Kodunuz çalıştığında ve bir sınıf adıile karşılaştığında, o sınıfı bulmak için içe aktardığınız ad alanlarına bakabilir.
> 
> Web sayfalarını oluşturmak için ASP.NET Web Sayfalarını Razor sözdizimi ile kullandığınızda, genellikle `WebPage` sınıf, çeşitli yardımcılar ve benzeri dahil olmak üzere her seferinde aynı sınıf kümesini kullanırsınız. Bir web sitesi oluşturduğunuzher zaman ilgili ad alanlarını alma işini size kazandırmak için, ASP.NET yapılandırılır, böylece her web sitesi için bir dizi temel ad alanı otomatik olarak içeri aktarılır. Bu yüzden isim alanları yla uğraşmak veya bugüne kadar içe aktarma yapmak zorunda kalmadınız; Birlikte çalıştığınız tüm sınıflar, sizin için zaten alınmış olan ad alanlarındadır.
> 
> Ancak, bazen sizin için otomatik olarak alınan bir ad alanında olmayan bir sınıfla çalışmanız gerekir. Bu durumda, bu sınıfın tam nitelikli adını kullanabilir veya sınıfı içeren ad alanını el ile içe aktarabilirsiniz. Bir ad alanı almak için, `using` `import` makalenin önceki bir örneğinde gördüğünüz gibi deyimi (Visual Basic'te) kullanırsınız.
> 
> Örneğin, `DataSet` sınıf `System.Data` ad alanındadır. Ad `System.Data` alanı, ASP.NET Razor sayfalarında otomatik olarak kullanılamaz. Bu nedenle, `DataSet` sınıfla tam nitelikli adını kullanarak çalışmak için aşağıdaki gibi kod kullanabilirsiniz:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> `DataSet` Sınıfı tekrar tekrar kullanmanız gerekiyorsa, böyle bir ad alanını içe aktarabilir ve ardından kodda sadece sınıf adını kullanabilirsiniz:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Başvurmak istediğiniz `using` diğer .NET Framework ad alanları için ekstreler ekleyebilirsiniz. Ancak, birlikte çalışacağınız sınıfların çoğu *.cshtml* ve *.vbhtml* sayfalarında kullanılmak üzere ASP.NET tarafından otomatik olarak içe aktarılan ad alanlarında olduğundan, bunu sık sık yapmanız gerekmez.

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Web Sayfası İçinde Grafikleri Görüntüleme

Şimdiye kadar gördüğünüz örneklerde, bir grafik oluşturursunuz ve grafik doğrudan tarayıcıya grafik olarak işlenir. Ancak, çoğu durumda, bir grafiği yalnızca tarayıcıda tek başına değil, bir sayfanın parçası olarak görüntülemek istersiniz. Bunu yapmak için iki adımlı bir işlem gerektirir. İlk adım, daha önce gördüğünüz gibi grafiği oluşturan bir sayfa oluşturmaktır.

İkinci adım, elde edilen görüntüyü başka bir sayfada görüntülemektir. Görüntüyü görüntülemek için, herhangi `<img>` bir görüntüyü görüntülemek için yaptığınız gibi bir HTML öğesi kullanırsınız. Ancak, *bir .jpg* veya *.png* dosyasına `<img>` başvurmak yerine, öğe grafiği oluşturan `Chart` yardımcıyı içeren *.cshtml* dosyasına başvurur. Görüntü sayfası çalıştığında, `<img>` öğe `Chart` yardımcının çıktısını alır ve grafiği işler.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. *ShowChart.cshtml*adlı bir dosya oluşturun.
2. Varolan içeriği aşağıdakilerle değiştirin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Kod, `<img>` *ChartArrayBasic.cshtml* dosyasında daha önce oluşturduğunuz grafiği görüntülemek için öğeyi kullanır.
3. Web sayfasını tarayıcıda çalıştırın. *ShowChart.cshtml* dosyası, *ChartArrayBasic.cshtml* dosyasında bulunan kodu temel alan grafik görüntüsünü görüntüler.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Grafik Oluşturma

Yardımcı, `Chart` grafiğin görünümünü özelleştirmenize izin veren çok sayıda seçeneği destekler. Renkleri, yazı tiplerini, kenarlıkları ve benzerlerini ayarlayabilirsiniz. Grafiğin görünümünü özelleştirmenin kolay bir yolu bir *tema*kullanmaktır. Temalar, yazı tipleri, renkler, etiketler, paletler, kenarlıklar ve efektler kullanarak grafiğin nasıl işlendirilebildiğini belirten bilgi koleksiyonlarıdır. (Grafiğin stilinin grafik türünü belirtmediğini unutmayın.)

Aşağıdaki tabloda yerleşik temalar listelenir.

| Tema | Açıklama |
| --- | --- |
| `Vanilla` | Beyaz arka planda kırmızı sütunlar görüntüler. |
| `Blue` | Mavi degrade arka planda mavi sütunları görüntüler. |
| `Green` | Yeşil degrade arka planda mavi sütunları görüntüler. |
| `Yellow` | Turuncu sütunları sarı degrade arka planda görüntüler. |
| `Vanilla3D` | Beyaz arka planda 3 B'lik kırmızı sütunlar görüntüler. |

Yeni bir grafik oluştururken kullanılacak temayı belirtebilirsiniz.

1. *ChartStyleGreen.cshtml*adlı yeni bir dosya oluşturun.
2. Sayfadaki varolan içeriği aşağıdakilerle değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Bu kod, veri veritabanını kullanan önceki örnekle aynıdır, `theme` ancak `Chart` nesneyi oluştururken parametreyi ekler. Değiştirilen kod aşağıda gösterilmektedir:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Sayfayı tarayıcıda çalıştırın. Öncekiyle aynı verileri görüyorsunuz, ancak grafik daha parlak görünüyor: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Grafik Kaydetme

Bu makalede `Chart` şimdiye kadar gördüğünüz yardımcıyı kullandığınızda, yardımcı her çağrıldığında grafiği sıfırdan yeniden oluşturur. Gerekirse, grafiğin kodu da veritabanını yeniden sorgular veya verileri almak için XML dosyasını yeniden okur. Bazı durumlarda, sorguladığınız veritabanı büyükse veya XML dosyası çok fazla veri içeriyorsa, bunu yapmak karmaşık bir işlem olabilir. Grafik çok fazla veri içermese bile, dinamik olarak görüntü oluşturma işlemi sunucu kaynaklarını kaplar ve birçok kişi grafiği görüntüleyen sayfa veya sayfaları isterse, web sitenizin performansı üzerinde bir etki olabilir.

Grafik oluşturmanın olası performans etkisini azaltmanıza yardımcı olmak için, ilk ihtiyacınız olduğunda bir grafik oluşturabilir ve ardından kaydedebilirsiniz. Grafik yeniden gerekli olduğunda, yeniden oluşturmak yerine, sadece kaydedilen sürümü almak ve bu render.

Bir grafiği şu şekilde kaydedebilirsiniz:

- Grafiği bilgisayar belleğinde (sunucuda) önbelleğe getirin.
- Grafiği görüntü dosyası olarak kaydedin.
- Grafiği XML dosyası olarak kaydedin. Bu seçenek, grafiği kaydetmeden önce değiştirmenize olanak tanır.

### <a name="caching-a-chart"></a>Grafiği Önbelleğe Alma

Bir grafik oluşturduktan sonra, grafiği önbelleğe alabilirsiniz. Grafiği önbelleğe almak, yeniden görüntülenmesi gerekiyorsa yeniden oluşturulması gerekmediği anlamına gelir. Önbelleğe bir grafik kaydettiğinizde, bu grafiğe özgü olması gereken bir anahtar verirsiniz.

Sunucunun belleği az alıyorsa önbelleğe kaydedilen grafikler kaldırılabilir. Ayrıca, uygulamanız herhangi bir nedenle yeniden başlatılırsa önbellek temizlenir. Bu nedenle, önbelleğe alınmış bir grafikle çalışmanın standart yolu, her zaman önce önbellekte kullanılabilir olup olmadığını denetlemek, değilse de oluşturmak veya yeniden oluşturmaktır.

1. Web sitenizin *kökünde, ShowCachedChart.cshtml*adlı bir dosya oluşturun.
2. Varolan içeriği aşağıdakilerle değiştirin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    Etiket, `<img>` `src` *ChartSaveToCache.cshtml* dosyasına işaret eden ve sayfaya bir anahtarı sorgu dizesi olarak aktaran bir öznitelik içerir. Anahtar myChartKey &quot;&quot;değerini içerir. *ChartSaveToCache.cshtml* dosyası, `Chart` grafiği oluşturan yardımcıyı içerir. Bu sayfayı birazdan oluşturacaksınız.

    Sayfanın sonunda *ClearCache.cshtml*adlı bir sayfanın bağlantısı var. Bu, kısa süre içinde oluşturacağınız bir sayfadır. Önbelleğe alma yalnızca bu örnek için önbelleğe alma test etmek için *ClearCache.cshtml* gerekir - önbelleğe alınmış grafiklerle çalışırken normalde dahil edeceğiniz bir bağlantı veya sayfa değildir.
3. Web sitenizin kökünde *ChartSaveToCache.cshtml*adlı yeni bir dosya oluşturun.
4. Varolan içeriği aşağıdakilerle değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Kod ilk olarak sorgu dizesinde anahtar değer olarak bir şey geçirilip geçirilemediğini denetler. Bu nedenle, kod `GetFromCache` yöntemi çağırarak ve anahtarı geçirerek önbellek dışında bir grafik okumaya çalışır. Önbellekte bu anahtarın altında hiçbir şey olmadığı ortaya çıkarsa (grafik ilk kez istendiğinde olur), kod grafiği her zamanki gibi oluşturur. Grafik tamamlandığında, kod çağırarak `SaveToCache`önbelleğe kaydeder. Bu yöntem bir anahtar (böylece grafik daha sonra istenebilir) ve grafik önbellekte kaydedilmesi gereken süre gerektirir. (Bir grafiği tam olarak önbelleğe aldığınız süre, temsil ettiği verilerin ne sıklıkta değişebileceğini düşündüğünüze bağlıdır.) Yöntem, `SaveToCache` bu `slidingExpiration` doğru ayarlanmışsa &#8212; bir parametre gerektirir, zaman çizelgesi sayacı grafiğe her erişinde sıfırlanır. Bu durumda, geçerli olarak, grafiğin önbellek girişinin, birisi grafiğe en son eriştikten 2 dakika sonra sona erdiği anlamına gelir. (Sürgülü son kullanma süresinin alternatifi mutlak son kullanma süresidir, yani önbellek girişi ne sıklıkta erişilmiş olursa olsun, önbelleğe alındıktan tam 2 dakika sonra sona erer.)

    Son olarak, kod `WriteFromCache` önbellekten grafiği getirmek ve işlemek için yöntemi kullanır. Bu yöntemin `if` önbelleği denetleyen bloğun dışında olduğunu unutmayın, çünkü grafiğin başlangıçta orada olup olmadığını veya oluşturulup önbelleğe kaydedilmesi gerekip gerekmediğini önbellekten alır.

    Örnekte, yöntembir `AddTitle` zaman damgası içerir dikkat edin. (Geçerli tarih ve saati `DateTime.Now` &#8212; &#8212; başlığa ekler.)
5. *ClearCache.cshtml* adında yeni bir sayfa oluşturun ve içeriğini aşağıdakilerle değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Bu sayfa, `WebCache` *ChartSaveToCache.cshtml*önbelleğe alınmış grafiği kaldırmak için yardımcı kullanır. Daha önce belirtildiği gibi, normalde böyle bir sayfa olması zorunda değilsiniz. Önbelleğe alma testini kolaylaştırmak için burada yaratıyorsun.
6. *ShowCachedChart.cshtml* web sayfasını tarayıcıda çalıştırın. Sayfa, *ChartSaveToCache.cshtml* dosyasında bulunan kodu temel alan grafik görüntüsünü görüntüler. Zaman damgasının grafik başlığında ne yazdığına dikkat edin. 

    ![Açıklama: Grafik başlığında zaman damgası olan temel grafiğin resmi](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Tarayıcıyı kapatın.
8. *ShowCachedChart.cshtml'i* yeniden çalıştırın. Zaman damgasının öncekiyle aynı olduğuna dikkat edin, bu da grafiğin yeniden oluşturulmadığını, bunun yerine önbellekten okunduğunu gösterir.
9. *ShowCachedChart.cshtml'de* **önbelleği temizle** bağlantısını tıklatın. Bu, önbelleğin temizlendiğini bildiren *ClearCache.cshtml'e*götürür.
10. **ShowCachedChart.cshtml bağlantısını döndür'e** veya WebMatrix'ten *ShowCachedChart.cshtml'i* yeniden çalıştırmayı tıklatın. Önbellek temizlenmiş olduğundan, bu kez zaman damgasının değiştiğine dikkat edin. Bu nedenle, kodun grafiği yeniden oluşturması ve önbelleğe geri koyması gerekiyordu.

### <a name="saving-a-chart-as-an-image-file"></a>Grafiği Görüntü Dosyası Olarak Kaydetme

Ayrıca, bir grafiği sunucuya görüntü dosyası (örneğin, *.jpg* dosyası olarak) olarak kaydedebilirsiniz. Daha sonra görüntü dosyasını herhangi bir görüntü gibi kullanabilirsiniz. Avantajı, dosyanın geçici bir önbelleğe kaydedilen yerine depolanmasıdır. Yeni bir grafik görüntüsünü farklı zamanlarda (örneğin, her saat) kaydedebilir ve zaman içinde meydana gelen değişikliklerin kalıcı bir kaydını tutabilirsiniz. Web uygulamanızın görüntü dosyasını koymak istediğiniz sunucudaki klasöre bir dosya yı kaydetme izniolduğundan emin olmalısınız.

1. Web sitenizin kökünde, zaten yoksa * \_ChartFiles* adında bir klasör oluşturun.
2. Web sitenizin kökünde *ChartSave.cshtml*adında yeni bir dosya oluşturun.
3. Varolan içeriği aşağıdakilerle değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Kod ilk `File.Exists` olarak *.jpg* dosyasının yöntemi arayarak var olup olmadığını denetler. Dosya yoksa, kod bir diziden yeni `Chart` bir dosya oluşturur. Bu kez, kod `Save` yöntemi çağırır `path` ve dosya yolunu ve grafiği nitaz dosya adını belirtmek için parametreyi geçer. Sayfanın gövdesinde, bir `<img>` öğe *.jpg* dosyasını görüntülemek için işaret etmek için yolu kullanır.
4. *ChartSave.cshtml* dosyasını çalıştırın.
5. WebMatrix'e geri dön. *Chart01.jpg* adlı bir resim dosyasının * \_ChartFiles* klasörüne kaydedildiğine dikkat edin.

### <a name="saving-a-chart-as-an-xml-file"></a>Grafiği XML Dosyası Olarak Kaydetme

Son olarak, bir grafiği sunucuya XML dosyası olarak kaydedebilirsiniz. Bu yöntemi grafiği önbelleğe almak veya grafiği bir dosyaya kaydetmek yerine kullanmanın bir avantajı, isterseniz grafiği görüntülemeden önce XML'i değiştirebilmektir. Uygulamanız, görüntü dosyasını koymak istediğiniz sunucudaki klasör için okuma/yazma izinleri olması gerekir.

1. Web sitenizin kökünde *ChartSaveXml.cshtml*adında yeni bir dosya oluşturun.
2. Varolan içeriği aşağıdakilerle değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Bu kod, xml dosyası kullanması dışında önbellekte bir grafik depolamak için daha önce gördüğünüz koda benzer. Kod, `File.Exists` önce Yöntem'i arayarak XML dosyasının var olup olmadığını denetlemek için denetler. Dosya varsa, kod yeni `Chart` bir nesne oluşturur ve `themePath` dosya adını parametre olarak geçirir. Bu, XML dosyasında ne varsa grafiği oluşturur. XML dosyası zaten yoksa, kod normal gibi bir grafik oluşturur `SaveXml` ve sonra kaydetmek için çağırır. Grafik, daha önce `Write` gördüğünüz gibi yöntem kullanılarak işlenir.

    Önbelleğe alma gösteren sayfada olduğu gibi, bu kod grafik başlığında bir zaman damgası içerir.
3. *ChartDisplayXMLChart.cshtml* adında yeni bir sayfa oluşturun ve aşağıdaki işaretlemeyi ekleyin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. *ChartDisplayXMLChart.cshtml* sayfasını çalıştırın. Grafik görüntülenir. Grafiğin başlığındaki zaman damgasını dikkate alın.
5. Tarayıcıyı kapatın.
6. WebMatrix'te * \_ChartFiles* klasörünü sağ tıklatın, **Yenile'yi**tıklatın ve ardından klasörü açın. Bu klasördeki *XMLChart.xml* dosyası `Chart` yardımcı tarafından oluşturuldu. 

    ![Açıklama: Grafik yardımcısı tarafından oluşturulan XMLChart.xml dosyasını gösteren _ChartFiles klasörü.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. *ChartDisplayXMLChart.cshtml* sayfasını yeniden çalıştırın. Grafik, sayfayı ilk çalıştırdığınız da aynı zaman damgasını gösterir. Bunun nedeni, grafiğin daha önce kaydettiğiniz XML'den oluşturulmasıdır.
8. WebMatrix'te * \_ChartFiles* klasörünü açın ve *XMLChart.xml* dosyasını silin.
9. *ChartDisplayXMLChart.cshtml* sayfasını bir kez daha çalıştırın. `Chart` Bu kez, yardımcıxXML dosyasını yeniden oluşturmak zorunda olduğundan, zaman damgası güncelleştirilir. İstersen, * \_ChartFiles* klasörünü kontrol edin ve XML dosyasının geri döndüğünü fark edin.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Web Sayfaları Sitelerinde Veritabanı ile Çalışmaya Giriş](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Performansı Artırmak için ASP.NET Web Sayfaları Sitelerinde Önbelleğe Alma Kullanma](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Grafik Sınıfı](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (MSDN'de Web Sayfaları API başvurusu ASP.NET)
