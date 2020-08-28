---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Eşleme senaryolarını uygulamak için AJAX kullanma | Microsoft Docs
author: rick-anderson
description: Adım 11 ' de, AJAX eşleme desteğinin Nerdakşam yemeği uygulamamıza nasıl tümleştirileceği, Dinkim tarafından oluşturulan, düzenleyen veya görüntüleyen kullanıcıların l 'yi görmesini sağlama adımları gösterilmektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 03b3a27d4b761d0417160b95cc6f39a345385065
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044330"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX Kullanarak Eşleme Senaryoları Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 11 ' dir.
> 
> Adım 11 ' de, AJAX eşleme desteğinin Nerdakşam yemeği uygulamamız ile nasıl tümleştirileceği gösterilmektedir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>Nerdakşam yemeği adım 11: AJAX haritasını tümleştirme

Artık, AJAX eşleme desteğini tümleştirerek uygulamamızı daha da etkileyici bir şekilde yapacağız. Bu, akşam yemeği 'nin konumunu oluşturan, düzenleyen veya görüntüleyen kullanıcıların, bir kullanıcı tarafından grafik konumunu görmesini sağlar.

### <a name="creating-a-map-partial-view"></a>Harita kısmi görünümü oluşturma

Uygulama dahilinde birkaç yerde eşleme işlevini kullanacağız. Kod KURUMıZA devam etmek için, birden çok denetleyici eylemi ve görünümünde yeniden kullanabileceğiniz tek bir kısmi şablon içinde ortak harita işlevini kapsülleyeceğiz. Bu kısmi görünümü "Map. ascx" olarak adlandırın ve \Views\dıntik dizininde oluşturun.

\Views\dıntik dizinine sağ tıklayıp Ekle-Görünüm menü komutunu seçerek Map. ascx kısmi ' i de oluşturabilirsiniz &gt; . "Map. ascx" görünümünü adlandıracağız, kısmi bir görünüm olarak kontrol edeceğiz ve bunu kesin yazılmış bir "akşam yemeği" model sınıfı olarak geçireceğiz.

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

Kısmi şablonumuz "Ekle" düğmesine tıkladığımızda oluşturulacak. Ardından Map. ascx dosyasını aşağıdaki içeriğe sahip olacak şekilde güncelleştireceğiz:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

İlk &lt; betik &gt; başvurusu Microsoft Virtual Earth 6,2 eşleme kitaplığını işaret eder. İkinci &lt; betik &gt; başvurusu, kısa bir süre içinde, yaygın JavaScript eşleme mantığımızı kapsülleyen bir map.js dosyasına işaret eder. &lt;Div ID = "themap" &gt; öğesi, Virtual Earth 'ın Haritayı barındırmak IÇIN kullanacağı HTML kapsayıcısıdır.

Daha sonra &lt; &gt; Bu görünüme özgü iki JavaScript işlevi içeren bir katıştırılmış betik bloğu vardır. İlk işlev, sayfa istemci tarafı betiği çalıştırmaya hazırsa yürütülen bir işlevi kurmak için jQuery kullanır. Virtual Earth harita denetimini yüklemek için Map.js betik dosyası içinde tanımlayacağımız bir LoadMap () yardımcı işlevini çağırır. İkinci işlev, bir konumu tanımlayan eşlemeye bir PIN ekleyen bir geri çağırma olay işleyicisidir.

&lt; &gt; JavaScript 'e eşlemek Istediğdiğimiz akşam yemeği 'nin Enlem ve boylamını eklemek için istemci tarafı betik bloğunda sunucu tarafı% =% bloğunu nasıl kullandığınızı fark edin. Bu, istemci tarafı komut dosyası tarafından kullanılabilecek dinamik değerleri (değerleri almak için sunucuya ayrı bir AJAX çağrısı gerektirmeden) çıkarmak için kullanışlı bir tekniktir. Bu, daha hızlı hale gelir. &lt;% =% &gt; Blokları, görünüm sunucuda işlendiğinde yürütülür. bu nedenle, HTML çıktısı yalnızca katıştırılmış JavaScript değerleriyle (örneğin: var enlem = 47,64312;) sona kadar bitecektir.

### <a name="creating-a-mapjs-utility-library"></a>Map.js yardımcı program kitaplığı oluşturma

Şimdi haritamız için JavaScript işlevini kapsülleyebilmemiz için kullanabilmemiz gereken Map.js dosyasını oluşturalım (ve daha önce LoadMap ve LoadPin yöntemlerini uygulama). Bu, projemizdeki \ KomutDosyaları dizinine sağ tıklayıp ardından " &gt; Yeni öğe Ekle" menü komutunu seçip, JScript öğesini seçip "Map.js" olarak ad vererek bunu yapabiliriz.

Aşağıda, eşlemenizi göstermek ve dinleyiciler için PIN 'lerimizi eklemek üzere sanal dünya ile etkileşime geçmek üzere Map.js dosyasına ekleyeceğiniz JavaScript kodu verilmiştir:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Eşlemeyi oluşturma ve düzenleme formlarıyla tümleştirme

Artık harita desteğini var olan oluşturma ve düzenleme senaryolarımızla tümleştireceğiz. İyi haber, bu oldukça kolay bir işlemdir ve denetleyici kodumuzu değiştirmemizi gerektirmez. Oluşturma ve düzenleme görünümlerimiz akşam yemeği Formu Kullanıcı arabirimini uygulamak için ortak bir "DinnerForm" kısmi görünümü paylaştığından, Haritayı tek bir yere ekleyebiliyoruz ve hem oluşturma hem de düzenleme senaryolarımızın onu kullanmasına olanak sağlar.

Tüm yapmanız gereken, \Views\Dinners\DinnerForm.ascx kısmi görünümü açmak ve yeni haritamızı kısmi olarak güncelleştirmek için onu güncelleştirmemiz gerekir. Güncelleştirilmiş DinnerForm, eşleme eklendikten sonra şöyle görünür (Note: HTML form öğeleri, kısaltma için aşağıdaki kod parçacığında atlanır):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

Yukarıdaki DinnerForm kısmi, model türü olarak "DinnerFormViewModel" türünde bir nesne alır (hem bir akşam yemeği nesnesi hem de ülkelerin DropDownList değerini doldurmak için bir SelectList gereklidir). Haritamız, yalnızca model türü olarak "akşam yemeği" türünde bir nesneye ihtiyaç duyuyor ve bu nedenle Haritayı kısmen işlerken DinnerFormViewModel 'in yalnızca akşam yemeği alt özelliğini geçiririz:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Kısmi öğesine eklediğimiz JavaScript işlevi, "adres" HTML metin kutusuna bir "bulanıklaştırma" olayı eklemek için jQuery kullanır. Bir Kullanıcı bir metin kutusunda veya sekmeye sekme tıkladığı zaman harekete gelen "odak" olaylarını duydunuz. Bunun tersi, bir Kullanıcı bir metin kutusu çıktığında harekete geçecek bir "bulanıklaştırma" olayıdır. Yukarıdaki olay işleyicisi, bu durumda Latitude ve Boylam metin kutusu değerlerini temizler ve haritalarımızda yeni adres konumunu çizer. map.js dosyasında tanımladığımız bir geri çağırma olayı işleyicisi, yaptığımız adrese göre sanal dünya tarafından döndürülen değerleri kullanarak formumuza ilişkin boylam ve Latitude metin kutularını güncelleştirir.

Şimdi uygulamamızı yeniden çalıştırdığımızda ve "ana bilgisayar akşam yemeği" sekmesine tıkladığınızda standart akşam yemeği form öğelerimiz ile birlikte bir varsayılan eşleme görüyoruz:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Bir adrese yazdığımızda ve sonra sekme uzağa geldiğinde, harita konumu görüntüleyecek şekilde dinamik olarak güncelleştirilecek ve olay işleyicimiz Enlem/Boylam metin kutularını konum değerleriyle dolduracaktır:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Yeni akşam yemeği 'ni kaydedip daha sonra düzenlenmek üzere yeniden açtığınızda, sayfa yüklendiğinde harita konumunun görüntülendiğini öğreneceğiz:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Adres alanı her değiştirildiğinde, eşleme ve enlem/boylam koordinatları güncelleşmeyecektir.

Artık Haritada akşam yemeği konumu görünmediğine göre, enlem ve Boylam form alanlarını gizli öğeler (her bir adres girildiğinde bu, eşleme otomatik olarak güncelleştiriyoruz) olarak görünür metin olarak değiştirebiliriz. Bunu yapmak için HTML. TextBox () HTML Yardımcısını kullanarak HTML. Hidden () yardımcı yöntemini kullanmaya geçiş yapacağız:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

Artık formlarımız, daha kolay bir Kullanıcı dostu ve ham Enlem/Boylam 'yi görüntülemeden (yine de veritabanındaki her akşam yemeği ile depolarken):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Haritayı Ayrıntılar görünümüyle tümleştirme

Artık harita oluşturma ve düzenleme senaryolarımızla tümleşik olduğunu öğrendiğimiz için, bunu Ayrıntılar senaryomızla de tümleştireceğiz. Tüm yapmanız gereken, &lt; Ayrıntılar görünümü içinde% HTML. RenderPartial ("map");% öğesini çağırıyoruz &gt; .

Aşağıda, tüm ayrıntılar görünümüne kaynak kodu (eşleme tümleştirmesi ile) şöyle görünür:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

Artık bir Kullanıcı/Dinners/Details/[ID] URL 'sine gittiğinde, akşam yemeği hakkındaki ayrıntıları, Haritada akşam yemeği 'nin konumunu (üzerinde gezindiği zaman bir itme PIN 'i ile birlikte) ve bunun için bir AJAX bağlantısı olduğunu görürsünüz:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Veritabanı ve deponuzda konum arama uygulama

AJAX uygulamamızı devre dışı bırakmak için, uygulamanın ana sayfasına, kullanıcıların yakın dinleleri grafik olarak aramasına imkan tanıyan bir harita ekleyelim.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Dinleler için konum tabanlı bir RADIUS aramasını verimli bir şekilde gerçekleştirmek üzere veritabanımızda ve veri havuzu katmanımız desteği uygulayarak başlayacağız. Bunu uygulamak için [sql 2008 ' in yeni Jeo uzamsal özelliklerini](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) kullanabiliriz veya alternatif olarak, burada makalesinde açıklanan Gary Dryden açıklanılan bir SQL işlevi yaklaşımı kullanabiliriz: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) ile ilgili olarak LINQ to SQL: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Bu tekniği uygulamak için, Visual Studio içinde "Sunucu Gezgini" öğesini açıp Nerdakşam yemeği veritabanını seçin ve ardından altındaki "işlevler" alt düğümüne sağ tıklayıp yeni "skaler değerli bir işlev" oluşturmayı seçin:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Daha sonra aşağıdaki DistanceBetween işlevini yapıştıracağız:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Daha sonra, SQL Server "Nearestdıntik" çağıracağımız yeni bir tablo değerli işlev oluşturacağız:

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Bu "Nearestdıntik" tablosu işlevi, DistanceBetween yardımcı işlevini kullanarak Enlem ve boyladığımız 100 mil içindeki tüm Dinlayıcıları döndürür:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Bu işlevi çağırmak için, önce \Modeller dizinimizin içindeki Nerdakşam. dbml dosyasına çift tıklayarak LINQ to SQL tasarımcısını açacağız:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Daha sonra Nearestdıntik ve DistanceBetween işlevlerini LINQ to SQL tasarımcı üzerine sürükleyeceğiz ve bu, LINQ to SQL NerdDinnerDataContext sınıfımızda yöntemler olarak eklenmesine neden olacak:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Daha sonra, belirtilen konumun 100 mil dahilinde olan gelecek iadeleri döndürmek için Nearestakşam yemeği işlevini kullanan DinnerRepository sınıfımızda bir "FindByLocation" sorgu yöntemi kullanıma sunabiliriz:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON tabanlı AJAX arama eylemi yöntemi uygulama

Şimdi, bir Haritayı doldurmak için kullanılabilecek akşam yemeği verilerinin bir listesini geri döndürmek için yeni FindByLocation () depo yönteminden faydalanan bir denetleyici eylemi yöntemi uygulayacağız. Bu eylem yöntemi, istemci üzerindeki JavaScript kullanılarak kolayca işlenebilmesi için akşam yemeği verilerini JSON (JavaScript Nesne Gösterimi) biçiminde geri döndüreceğiz.

Bunu uygulamak için, \Controllers dizinine sağ tıklayıp add-Controller menü komutunu seçerek yeni bir "SearchController" sınıfı oluşturacağız &gt; . Daha sonra aşağıdaki gibi yeni SearchController sınıfında bir "SearchByLocation" eylem yöntemi uygulayacağız:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 'ın SearchByLocation eylem yöntemi, yakındaki dinde bir liste almak için DinnerRepository üzerindeki FindByLocation metodunu dahili olarak çağırır. Bunun yerine, akşam yemeği nesnelerini doğrudan istemciye döndürmek yerine, Jsonakşam yemeği nesnelerini döndürür. Jsonakşam yemeği sınıfı, akşam yemeği özelliklerinin bir alt kümesini sunar (örneğin: güvenlik nedenleriyle, bir akşam yemeği için RSVP 'e sahip kişilerin adlarını açıklamaz). Ayrıca, akşam yemeği üzerinde mevcut olmayan ve belirli bir akşam yemeği ile ilişkili RSVP nesnelerinin sayısı sayarak dinamik olarak hesaplanan bir RSVPCount özelliği de içerir.

Daha sonra, JSON tabanlı bir Tel biçimi kullanarak dinetlerin sırasını döndürmek için denetleyici temel sınıfında JSON () yardımcı yöntemini kullanıyoruz. JSON, basit veri yapılarını temsil eden standart bir metin biçimidir. Aşağıda, iki Jsonakşam yemeği nesnesinin JSON ile biçimlendirilen listesinin, eylem yöntemızdan döndürüldüğünde nasıl göründüğü hakkında bir örnek verilmiştir:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.txt)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery kullanarak JSON tabanlı AJAX metodunu çağırma

Şimdi SearchController 'ın SearchByLocation eylem yöntemini kullanmak için Nerdakşam yemeği uygulamasının giriş sayfasını güncelleştirmeye hazırsınız. Bunu yapmak için/views/Home/Index.aspx görünüm şablonunu açacak ve onu bir TextBox, Search button, haritamız ve &lt; dinnerList adlı bir div öğesi olacak şekilde güncelleştireceğiz &gt; :

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Sonra sayfaya iki JavaScript işlevi ekleyebiliriz:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

İlk JavaScript işlevi, sayfa ilk yüklendiğinde Haritayı yükler. İkinci JavaScript işlevi arama düğmesinde bir JavaScript 'e tıklama olayı işleyicisi. Düğmeye basıldığında, Map.js dosyasına ekleyeceğiniz FindDinnersGivenLocation () JavaScript işlevini çağırır:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Bu FindDinnersGivenLocation () işlevi eşlemeyi çağırır. Bu denetimi, girilen konumda ortalamak için Virtual Earth denetiminde bulun (). Virtual Earth harita hizmeti, eşlemesini döndürür. Find () yöntemi, en son bağımsız değişken olarak geçirdiğimiz Callbackupdatemapdınanlar geri çağırma yöntemini çağırır.

Callbackupdatemapdınanlar () yöntemi, gerçek işin yapıldığı yerdir. Bu, SearchController 'ın SearchByLocation () eylem yöntemine yönelik bir AJAX çağrısı gerçekleştirmek için jQuery 'in $. Post () yardımcı yöntemini kullanır; bu, yeni ortalanmış haritanın Enlem ve boylamı olur. $. Post () yardımcı yöntemi tamamlandığında ve SearchByLocation () eylem yönteminden döndürülen JSON biçimli akşam yemeği sonuçları, bunu "dinlenebilir" olarak adlandırılan bir değişken kullanılarak geçirilecek bir satır içi işlevi tanımlar. Ardından, döndürülen her akşam yemeği üzerinden bir foreach yapar ve haritadaki yeni bir PIN eklemek için akşam yemeği 'nin Enlem ve boylam ve diğer özelliklerini kullanır. Ayrıca, eşlemenin sağındaki dinde HTML listesine bir akşam yemeği girişi ekler. Ardından, bir kullanıcı üzerlerine geldiğinde akşam yemeği hakkındaki ayrıntıların görüntülenmesi için hem Pushpin 'ler hem de HTML listesi için bir vurgulama olayı arar:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

Şimdi uygulamayı çalıştırdığımızda ve bir harita ile sunulacak olan giriş sayfasını ziyaret ettiğimiz zaman. Bir şehrin adını girdiğimiz zaman, haritada yakında yaklaşan başlayıcıları görüntülenecektir:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Bir akşam yemeği üzerine gelindiğinde, onunla ilgili ayrıntılar görüntülenir.

Akşam yemeği başlığına tıklayarak ya da HTML listesinin sağ tarafında, bize akşam yemeği, daha sonra isteğe bağlı olarak RSVP ile ilgili olarak şu şekilde bir işlem yapabilirsiniz:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Sonraki adım

Şimdi Nerdakşam yemeği uygulamamız için tüm uygulama işlevlerini uyguladık. Şimdi otomatik birim testlerini etkinleştirebilmemiz için bakalım.

> [!div class="step-by-step"]
> [Önceki](use-ajax-to-deliver-dynamic-updates.md) 
>  [Sonraki](enable-automated-unit-testing.md)
