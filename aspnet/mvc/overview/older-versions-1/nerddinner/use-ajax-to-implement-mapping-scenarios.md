---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Haritalama Senaryolarını Uygulamak için AJAX'ı kullanın | Microsoft Dokümanlar
author: rick-anderson
description: Adım 11, AJAX haritalama desteğinin NerdDinner uygulamamıza nasıl entegre edilebildiğini göstererek, akşam yemeklerini oluşturan, düzenleyen veya görüntüleyen kullanıcıların l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542592"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX Kullanarak Eşleme Senaryoları Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 11 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 11, AJAX haritalama desteğinin NerdDinner uygulamamıza nasıl entegre edilebildiğini ve akşam yemeklerini oluşturan, düzenleyen veya görüntüleyen kullanıcıların akşam yemeğinin yerini grafik olarak görmelerini sağlar.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner Adım 11: Bir AJAX Haritası Entegre

Şimdi AJAX haritalama desteğini entegre ederek uygulamamızı görsel olarak biraz daha heyecan verici hale getireceğiz. Bu, akşam yemeği oluşturan, düzenleyen veya görüntüleyen kullanıcıların yemeğin yerini grafik olarak görmelerini sağlar.

### <a name="creating-a-map-partial-view"></a>Harita Kısmi Görünüm Oluşturma

Uygulamamız dahilinde çeşitli yerlerde haritalama işlevini kullanacağız. Kodumuzu KURU tutmak için, birden çok denetleyici eylemi ve görünümü nde yeniden kullanabileceğimiz tek bir kısmi şablon içinde ortak harita işlevini kapsülleriz. Bu kısmi görünümü "map.ascx" olarak adlandıracağız ve \Görünümler\Akşam Yemekleri dizininde oluşturacağız.

\Views\Dinners dizinine sağ tıklayarak ve Ekle-Görüntüle&gt;menüsü komutunu seçerek map.ascx'i kısmi olarak oluşturabiliriz. "Map.ascx" görünümüne "Map.ascx" adını vereceğiz, kısmi bir görünüm olarak kontrol edeceğiz ve güçlü bir şekilde yazılan "Akşam Yemeği" model sınıfından geçeceğimizi belirteceğiz:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

"Ekle" düğmesine tıkladığımızda kısmi şablonumuz oluşturulacaktır. Daha sonra map.ascx dosyasını aşağıdaki içeriğe sahip olacak şekilde güncelleriz:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

İlk &lt;komut&gt; dosyası başvurusu, Microsoft Virtual Earth 6.2 eşleme kitaplığını işaret ediyor. İkinci &lt;komut&gt; dosyası başvurusu, kısa süre içinde oluşturabileceğimiz ve ortak Javascript haritalama mantığımızı saklayacak bir map.js dosyasına işaret eder. Div &lt;id="theMap"&gt; öğesi, Sanal Dünya'nın haritayı barındırmak için kullanacağı HTML kapsayıcısIdur.

Daha sonra bu &lt;&gt; görünüme özgü iki JavaScript işlevi içeren gömülü bir komut dosyası bloğumuz vardır. İlk işlev, sayfa istemci tarafı komut dosyasını çalıştırmaya hazır olduğunda çalıştıran bir işlevi kablolamak için jQuery kullanır. Sanal dünya haritası denetimini yüklemek için Map.js komut dosyasında tanımladığımız loadmap() yardımcı işlevini çağırır. İkinci işlev, haritaya bir konumu tanımlayan bir pin ekleyen bir geri arama olay işleyicisidir.

JavaScript'e haritalamak istediğimiz &lt;Akşam&gt; Yemeği'nin enlem ve boylamını yerleştirmek için istemci tarafındaki komut dosyası bloğunda sunucu tarafı %= % bloğu kullandığımıza dikkat edin. Bu, istemci tarafı komut dosyası tarafından kullanılabilecek dinamik değerleri çıktılamak için kullanışlı bir tekniktir (değerleri almak için sunucuya ayrı bir AJAX çağrısı gerektirmeden – bu da daha hızlı olmasını sağlar). %= &lt;%&gt; blokları görünüm sunucuda görüntülendiğinde yürütülür ve böylece HTML çıktısı gömülü JavaScript değerleriyle sonuçlanır (örneğin: var enlem = 47.64312;).

### <a name="creating-a-mapjs-utility-library"></a>Map.js yardımcı kitaplık oluşturma

Şimdi haritamız için JavaScript işlevini kapsüllemek için kullanabileceğimiz Map.js dosyasını oluşturalım (ve yukarıdaki LoadMap ve LoadPin yöntemlerini uygulayalım). Bunu projemizdeki \Scripts dizinine sağ tıklayarak yapabiliriz ve ardından "Ekle-&gt;Yeni Öğe" menüsü komutunu seçebilir, JScript öğesini seçebilir ve adını "Map.js" olarak adlandırabiliriz.

Haritamızı görüntülemek ve akşam yemeklerimiz için yer pinleri eklemek için Sanal Dünya ile etkileşime girecek Map.js dosyasına ekleyeceğimiz JavaScript kodu aşağıdadır:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Oluşturma ve Formları Ediyiyle Haritayı Tümleştirme

Şimdi Harita desteğini mevcut Oluştur ve Edit senaryolarımızla bütünleştireceğiz. İyi haber, bu oldukça kolay yapmak ve bize herhangi bir Denetleyici kodu değiştirmek gerektirmez. Form Arabirimi'ni uygulamak için Ortak bir "DinnerForm" kısmi görünümü paylaştığından, haritayı tek bir yerde ekleyebilir ve hem Oluştur hem de Edit senaryolarımızın kullanmasını sağlayabiliriz.

Yapmamız gereken tek şey \Views\Dinners\DinnerForm.ascx kısmi görünümü açmak ve yeni haritakısmi içerecek şekilde güncellemektir. Aşağıda, harita eklendikten sonra güncellenen DinnerForm'un nasıl görüneceği yer almaktadır (not: HTML form öğeleri kısaltma için aşağıdaki kod parçacığından atlanmıştır):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

Yukarıdaki DinnerForm kısmi modeli türü olarak "DinnerFormViewModel" türünden bir nesne alır (çünkü hem bir Akşam Yemeği nesnesine hem de ülkelerin açılır listesini doldurmak için bir SelectList'e ihtiyaç duyar). Bizim Harita kısmi sadece model türü olarak "Akşam Yemeği" türübir nesne ihtiyacı, ve bu yüzden biz ona DinnerFormViewModel sadece Akşam Yemeği alt özelliği geçiyor kısmi harita render:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Kısmi olarak eklediğimiz JavaScript işlevi, "Adres" HTML textbox'ına bir "bulanıklık" olayı eklemek için jQuery kullanır. Bir kullanıcı bir metin kutusunu tıklattığında veya sekmeyaptığında yanan "odak" olaylarını duymuşolabilirsiniz. Bunun tersi, kullanıcı bir textbox'tan çıktığında ateşleyen bir "bulanıklık" olayıdır. Yukarıdaki olay işleyicisi, bu durumda enlem ve boylam metin kutusu değerlerini temizler ve haritamızdaki yeni adres konumunu çizer. map.js dosyasında tanımladığımız bir geri arama olay işleyicisi, daha sonra verdiğimiz adrese göre sanal dünya tarafından döndürülen değerleri kullanarak formumuzdaki boylam ve enlem metin kutularını günceller.

Ve şimdi uygulamamızı tekrar çalıştırdığımızda ve "Ev Sahibi Yemeği" sekmesine tıkladığımızda, standart Akşam Yemeği formu öğelerimizle birlikte görüntülenen varsayılan bir harita göreceğiz:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Bir adres yazdığımızda ve sonra sekmemizden uzaklaştığımızda, harita konumu görüntülemek için dinamik olarak güncellenir ve olay işleyicimiz enlem/boylam metin kutularını konum değerleriyle dolduracaktır:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Yeni akşam yemeğini kaydedip düzenleme için tekrar açarsak, sayfa yüklendiğinde harita konumunun görüntülendiğini buluruz:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Adres alanı her değiştiğinde, harita ve enlem/boylam koordinatları güncellenir.

Artık harita Akşam Yemeği konumunu gösterdiğine göre, Enlem ve Boylam form alanlarını görünür metin kutularından gizli öğeler e dönüştürü (harita her adres girildiğinde otomatik olarak güncelleştirildiği için) değiştirebiliriz. Bunu yapmak için Html.TextBox() HTML yardımcısını kullanmaktan Html.Hidden() yardımcı yöntemini kullanmaya geçeceğiz:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

Ve şimdi formlarımız biraz daha kullanıcı dostu ve ham enlem / boylam (hala veritabanında her Akşam yemeği ile bunları saklarken) görüntüleme kaçının:

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Haritayı Ayrıntılar Görünümüyle Tümleştirme

Artık haritayı Oluştur ve Edit senaryolarımızla entegre ettiğimize göre, bunu Ayrıntılar senaryomuzla da entegre edelim. Yapmamız gereken tek şey &lt;% Html.RenderPartial("harita"); Ayrıntılar&gt; görünümünde %.

Aşağıda tam Ayrıntılar görünümü (harita tümleştirme ile) kaynak kodu nasıl göründüğüdür:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

Ve şimdi bir kullanıcı bir /Dinners/Details/[id] URL'sine gittiğinde akşam yemeğiyle ilgili ayrıntıları, haritadaki akşam yemeğinin konumunu (akşam yemeğinin başlığını ve adresini gösteren bir itme pimi ile birlikte) görür ler ve bunun için RSVP'ye ajax bağlantısı bulunur:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Veritabanımızda ve Depomuzda Konum Araması Uygulama

AJAX uygulamamızı bitirmek için, uygulamanın ana sayfasına kullanıcıların yakınlarındaki akşam yemeklerini grafikolarak aramalarına olanak tanıyan bir Harita ekleyelim.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Akşam Yemekleri için konum tabanlı yarıçap aramasını verimli bir şekilde gerçekleştirmek için veritabanımız ve veri deposu katmanımızda destek uygulayarak başlayacağız. Bunu uygulamak için [SQL 2008'in yeni jeouzamsal özelliklerini](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) kullanabiliriz, ya da alternatif olarak Gary [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) Dryden'ın burada makalede tartıştığı bir SQL fonksiyonu yaklaşımını kullanabiliriz: ve Rob Conery burada LINQ ile SQL'i kullanmak la ilgili blogged:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Bu tekniği uygulamak için Visual Studio'da "Server Explorer"ı açacağız, NerdDinner veritabanını seçeceğiz ve ardından altındaki "fonksiyonlar" alt düğümüne sağ tıklayıp yeni bir "Skaler değerli işlev" oluşturmayı seçeceğiz:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Daha sonra aşağıdaki DistanceBetween işlevine yapıştırırız:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Daha sonra SQL Server'da "NearestDinners" adını vereceğimiz yeni bir tablo değerinde işlev oluştururuz:

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Bu "NearestDinners" tablosu işlevi, sağladığımız enlem ve boylamın 100 mil içindeki tüm Akşam Yemekleri'ni döndürmek için Mesafe Arasındaki Yardımcı işlevini kullanır:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Bu işlevi aramak için, öncelikle \Models dizini içinde NerdDinner.dbml dosyasına çift tıklayarak LINQ'dan SQL tasarımcısına açılırız:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Daha sonra En Yakın Akşam Yemekleri ve Mesafe Arasındaki işlevleri LINQ'dan SQL tasarımcısına sürükleyeceğiz, bu da linq'de SQL NerdDinnerDataContext sınıfımıza yöntem olarak eklenmesine neden olur:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Daha sonra belirtilen konuma 100 mil içinde yaklaşan Akşam Yemekleri dönmek için NearestDinner işlevini kullanan DinnerRepository sınıfımızda bir "FindByLocation" sorgu yöntemini ortaya çıkarabiliriz:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON tabanlı AJAX Arama Eylem Yöntemi uygulama

Şimdi, bir haritayı doldurmak için kullanılabilecek Akşam Yemeği verilerinin listesini geri döndürmek için yeni FindByLocation() deposu yönteminden yararlanan bir denetleyici eylem yöntemi uygulayacağız. Bu eylem yöntemi, istemcide JavaScript kullanılarak kolayca manipüle edilebilmesi için Akşam Yemeği verilerini JSON (JavaScript Object Notation) biçiminde geri döndürecek.

Bunu uygulamak için, \Controllers dizinine sağ tıklayarak ve Ekle-Denetleyici&gt;menü komutunu seçerek yeni bir "SearchController" sınıfı oluştururuz. Daha sonra aşağıdaki gibi yeni SearchController sınıfı içinde bir "SearchByLocation" eylem yöntemi uygulayacağız:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController'ın SearchByLocation eylem yöntemi, yakındaki akşam yemeklerinin listesini almak için DinnerRepository'deki FindByLocation yöntemini dahili olarak çağırır. Ancak Akşam Yemeği nesnelerini doğrudan istemciye döndürmek yerine JsonDinner nesnelerini döndürür. JsonDinner sınıfı Dinner özelliklerinin bir alt kümesini ortaya çıkarır (örneğin: güvenlik nedenleriyle bir akşam yemeği için RSVP'd'si olan kişilerin adlarını açıklamaz). Ayrıca Akşam Yemeği'nde bulunmayan ve belirli bir akşam yemeğiyle ilişkili RSVP nesnelerinin sayısı sayılarak dinamik olarak hesaplanan bir RSVPCount özelliğini de içerir.

Daha sonra, JSON tabanlı tel formatı kullanarak akşam yemeği sırasını döndürmek için Controller taban sınıfındaki Json() yardımcı yöntemini kullanıyoruz. JSON, basit veri yapılarını temsil eden standart bir metin biçimidir. Aşağıda, eylem yöntemimizden döndürüldüğünde JSON biçimli iki JsonDinner nesnesinin nasıl göründüğüne bir örnek verilmiştir:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery kullanarak JSON tabanlı AJAX yöntemiarama

SearchController'ın SearchByLocation eylem yöntemini kullanmak için NerdDinner uygulamasının ana sayfasını güncellemeye hazırız. Bunu yapmak için , /Views/Home/Index.aspx view şablonunu açarız ve bir textbox, arama düğmesi, &lt;&gt; haritamız ve dinnerList adlı bir div öğesi ne olacaksa güncelleniriz:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Daha sonra sayfaya iki JavaScript işlevi ekleyebilirsiniz:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

İlk JavaScript işlevi, sayfa ilk yüklendiğinde haritayı yükler. İkinci JavaScript işlevi, arama düğmesinde bir JavaScript tıklatma olay işleyicisini bağlar. Düğmeye basıldığında Map.js dosyamıza ekleyeceğimiz FindDinnersGivenLocation() JavaScript işlevini çağırır:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Bu FindDinnersGivenLocation() işlevi eşlemi çağırır. Sanal Dünya Denetimi'nde, girilen konuma ortalamak için bulun() Sanal dünya haritası hizmeti döndüğünde, harita. Find() yöntemi callbackUpdateMapDinners geri arama yöntemi biz son argüman olarak geçti çağırır.

CallbackUpdateMapDinners() yöntemi gerçek iş yapılır. Bu bizim SearchController's SearchByLocation() eylem yöntemi bir AJAX arama gerçekleştirmek için jQuery's $ post() yardımcı yöntemi kullanır - yeni merkezli harita enlem ve boylam geçen. $.post() yardımcı yöntemi tamamlandığında çağrılacak bir satır içi işlev tanımlar ve SearchByLocation() eylem yönteminden döndürülen JSON biçimli akşam yemeği sonuçları "akşam yemekleri" adlı bir değişken kullanılarak geçirilir. Daha sonra her döndürülen akşam yemeği üzerinde bir foreach yapar ve harita üzerinde yeni bir pin eklemek için akşam yemeği enlem ve boylam ve diğer özellikleri kullanır. Ayrıca haritanın sağına HTML yemek listesine bir akşam yemeği girişi ekler. Daha sonra hem piştirmeler hem de HTML listesi için bir gezinme olayını kablolar, böylece bir kullanıcı üzerlerinde gezinirken akşam yemeğiyle ilgili ayrıntılar görüntülenir:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

Ve şimdi uygulamayı çalıştırdığımızda ve ana sayfayı ziyaret ettiğimizde bir harita yla birlikte sunulacaktır. Bir şehrin adını girdiğimizde harita, ona yakın olan akşam yemeklerini görüntüler:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Bir akşam yemeği üzerinde gezinen bu konuda ayrıntıları gösterecektir.

Akşam Yemeği başlığını kabarcıkta veya HTML listesinde sağ tarafta tıklatmak bizi akşam yemeğine yönlendirecektir – ki bu da isteğe bağlı olarak RSVP'ye aşağıdakiler için:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Sonraki Adım

NerdDinner uygulamamızın tüm uygulama işlevlerini hayata geçirdik. Şimdi otomatik birim testini nasıl etkinleştirebileceğimize bakalım.

> [!div class="step-by-step"]
> [Önceki](use-ajax-to-deliver-dynamic-updates.md)
> [Sonraki](enable-automated-unit-testing.md)
