---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Listeleme/Ayrıntı Kullanıcı UI'ı Uygulamak için Denetleyicileri ve Görünümleri Kullanma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 4, kullanıcılara veri kaydı/ayrıntılı gezinme deneyimi sağlamak için modelden yararlanan uygulamaya nasıl bir Denetleyici ekleyeceğinigösterir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541318"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Denetleyicileri ve Görünümleri Kullanarak Listeleme/Ayrıntılar Kullanıcı Arabirimi Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 4 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 4, kullanıcılara NerdDinner sitemizdeakşam yemekleri için veri kaydı/detay navigasyon deneyimi sunmak için modelden yararlanan uygulamaya nasıl bir Denetleyici ekleyeceğinizi gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner Adım 4: Denetleyicileri ve Görünümler

Geleneksel web çerçeveleri (klasik ASP, PHP, ASP.NET Web Formları, vb. ile gelen URL'ler genellikle diskteki dosyalara eşlenir. Örneğin: "/Products.aspx" veya "/Products.php" gibi bir URL isteği "Products.aspx" veya "Products.php" dosyası yla işlenebilir.

Web tabanlı MVC çerçeveleri URL'leri sunucu koduyla biraz daha farklı bir şekilde eşler. Gelen URL'leri dosyalarla eşlemek yerine, URL'leri sınıflardaki yöntemlerle eşlerler. Bu sınıflara "Denetleyiciler" adı verilir ve gelen HTTP isteklerini işlemekten, kullanıcı girdilerini işlemekten, veri almakve kaydetmekten ve istemciye geri göndermek için yanıtı belirlemekten (HTML görüntülemek, dosya yı indirme, farklı bir URL'ye yönlendirme vb.) sorumludurlar.

Şimdi bizim NerdDinner uygulaması için temel bir model inşa ettik, bir sonraki adım sitemizde Akşam Yemekleri için bir veri listeleme / ayrıntılar navigasyon deneyimi ile kullanıcılara sunmak için yararlanır uygulamaya bir Denetleyici eklemek olacaktır.

### <a name="adding-a-dinnerscontroller-controller"></a>DinnersController DenetleyiciSi Ekleme

Web projemizdeki "Denetleyiciler" klasörüne sağ tıklayarak başlayacağız ve ardından **Ekle-Denetleyici&gt;** menüsü komutunu seçeceğiz (Ctrl-M, Ctrl-C yazarak da bu komutu uygulayabilirsiniz):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Bu, "Denetleyici Ekle" iletişim kutusunu gündeme getirir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

Yeni kumandaya "DinnersController" adını vereceğiz ve "Ekle" düğmesine tıklayacağız. Visual Studio daha sonra \Controllers dizini altında bir DinnersController.cs dosyası ekleyecektir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Ayrıca kod düzenleyici içinde yeni DinnersController sınıf açılacaktır.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>DinnersController Sınıfına Dizin() ve Ayrıntılar() Eylem Yöntemleri Ekleme

Yaklaşan akşam yemeklerinin listesine göz atmak için uygulamamızı kullanan ziyaretçilere olanak sağlamak ve bu konuda ki belirli ayrıntıları görmek için listedeki herhangi bir Akşam Yemeği'ni tıklamalarına izin vermek istiyoruz. Bunu, uygulamamızdan aşağıdaki URL'leri yayınlayarak yapacağız:

| **URL** | **Amaç** |
| --- | --- |
| */Akşam Yemekleri/* | Yaklaşan akşam yemeklerinin HTML listesini görüntüleme |
| */Akşam Yemekleri/Ayrıntılar/[id]* | URL'ye gömülü bir "id" parametresi ile gösterilen ve veritabanındaki akşam yemeğinin DinnerID'si ile eşleşen belirli bir akşam yemeğiyle ilgili ayrıntıları görüntüleyin. Örneğin: /Dinners/Details/2, DinnerID değeri 2 olan Akşam Yemeği hakkında ayrıntıları içeren bir HTML sayfası görüntüler. |

Bu URL'lerin ilk uygulamalarını, aşağıdaki gibi DinnersController sınıfımıza iki genel "eylem yöntemi" ekleyerek yayınlayacağız:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Daha sonra NerdDinner uygulamasını çalıştıracağız ve tarayıcımızı kullanarak onları çağıracağız. *"/Dinners/"* URL'sini yazmak *Index()* yöntemimizin çalışmasına neden olur ve aşağıdaki yanıtı geri gönderir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

*"/Dinners/Details/2"* URL'sini yazmak *Ayrıntılar()* yöntemimizin çalışmasına neden olur ve aşağıdaki yanıtı geri gönderir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

Merak ediyor olabilirsiniz - ASP.NET MVC DinnersController sınıfımızı oluşturmayı ve bu yöntemleri nasıl kullanmayı bilip bilip bu yöntemleri kullanmayı biliyor olabilir? Yönlendirmenin nasıl çalıştığına hızlıca bir göz atalım.

### <a name="understanding-aspnet-mvc-routing"></a>MVC YönlendirmeASP.NET anlama

ASP.NET MVC, URL'lerin denetleyici sınıflarına nasıl eşlendirilebildiğini denetlemede çok fazla esneklik sağlayan güçlü bir URL yönlendirme motoru içerir. MVC'ASP.NET hangi denetleyici sınıfı nın oluşturulabileceğini, hangi yöntemi çağırıp çağırabileceğimizi tamamen özelleştirmemize ve değişkenlerin URL/Querystring'ten otomatik olarak ayrıştırılabildiği ve parametre bağımsız değişkenleri olarak yönteme geçirilebildiği farklı şekillerde yapılandırmamıza olanak tanır. Tamamen SEO (arama motoru optimizasyonu) için bir site optimize etmek için esneklik yanı sıra bir uygulamadan istediğiniz herhangi bir URL yapısını yayınlamak sağlar.

Varsayılan olarak, yeni ASP.NET MVC projeleri önceden yapılandırılmış URL yönlendirme kuralları kümesi yle birlikte gelir. Bu, herhangi bir şeyi açıkça yapılandırmamıza gerek kalmadan bir uygulamaya kolayca başlamamızı sağlar. Varsayılan yönlendirme kuralı kayıtları projelerimizin "Uygulama" sınıfında bulunabilir - projemizin kökündeki "Global.asax" dosyasını çift tıklayarak açabiliyoruz:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

Varsayılan ASP.NET MVC yönlendirme kuralları bu sınıfın "RegisterRoutes" yöntemi içinde kaydedilir:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"Rotalar. MapRoute()" yöntemi yukarıdaki çağrı, gelen URL URL'lerini URL biçimini kullanarak denetleyici sınıflarına eşleyen varsayılan bir yönlendirme kuralını kaydeder: "/{controller}/{action}/{id}" – "denetleyici" denetleyici sınıfının anlık adıdır, "eylem" üzerine çağırmak için genel bir yöntemin adıdır ve "id" URL'ye bir argüman olarak aktarılabilen isteğe bağlı bir parametredir. "MapRoute()" yöntem çağrısına geçirilen üçüncü parametre, URL'de bulunmaması durumunda denetleyici/eylem/id değerleri için kullanılacak varsayılan değerler kümesidir (Denetleyici = "Ana Sayfa", Action="Index", Id=").

Aşağıda, çeşitli URL'lerin varsayılan "<em>/{controllers}/{action}/{id}"</em>rota kuralı kullanılarak nasıl eşlendirildiğini gösteren bir tablo yer almaktadır:

| **URL** | **Denetleyici Sınıfı** | **Eylem Yöntemi** | **Geçirilen Parametreler** |
| --- | --- | --- | --- |
| */Akşam Yemekleri/Ayrıntılar/2* | Akşam YemekleriDenetleyici | Ayrıntılar(id) | id=2 |
| */Akşam Yemekleri/Edit/5* | Akşam YemekleriDenetleyici | Edit(id) | id=5 |
| */Akşam Yemekleri/Oluştur* | Akşam YemekleriDenetleyici | Oluştur() | Yok |
| */Akşam Yemekleri* | Akşam YemekleriDenetleyici | Dizin() | Yok |
| */Ana Sayfa* | AnaSayfaDenetleyici | Dizin() | Yok |
| */* | AnaSayfaDenetleyici | Dizin() | Yok |

Son üç satır, kullanılan varsayılan değerleri (Denetleyici = Ev, Eylem = Dizin, Id = "") gösterir. "Dizin" yöntemi belirtilmemişse varsayılan eylem adı olarak kaydolduğundan, "/Dinners" ve "/Home" URL'leri Dizin() eylem yönteminin Denetleyici sınıflarında çağrılmasını sağlar. "Ev" denetleyicisi belirtilmemişse varsayılan denetleyici olarak kaydolduğundan, "/" URL HomeController'ın oluşturulmasına ve üzerindeki Dizin() eylem yönteminin çağrılmasını neden olur.

Bu varsayılan URL yönlendirme kurallarını beğenmiyorsanız, iyi haber, bunların kolayca değiştirilmesidir - bunları yukarıdaki RegisterRoutes yöntemi nde düzenlilatın. Ancak NerdDinner uygulamamız için varsayılan URL yönlendirme kurallarının hiçbirini değiştirmeyeceğiz – bunun yerine bunları olduğu gibi kullanacağız.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>DinnerSController'ımızdan DinnerRepository'u Kullanma

Şimdi DinnersController's Index() ve Details() eylem yöntemlerini modelimizi kullanan uygulamalarla değiştirelim.

Davranışı uygulamak için daha önce oluşturduğumuz DinnerRepository sınıfını kullanacağız. "NerdDinner.Models" ad alanına atıfta bulunan bir "using" deyimi ekleyerek başlayacağız ve daha sonra DinnerRepozitory'mizin bir örneğini DinnerController sınıfımızda bir alan olarak beyan edeceğiz.

Daha sonra bu bölümde biz "Bağımlılık Enjeksiyon" kavramını tanıtmak ve bizim Denetleyicileri için daha iyi birim testi sağlayan bir DinnerRepository bir referans elde etmek için başka bir yol göstereceğiz - ama şu anda sadece aşağıdaki gibi bizim DinnerRepository satırlı bir örnek oluşturacağız.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Şimdi geri bizim alınan veri modeli nesneleri kullanarak bir HTML yanıtı oluşturmak için hazırız.

### <a name="using-views-with-our-controller"></a>Denetleyicimizle Görünümleri Kullanma

HTML'i bir araya getirmek ve ardından *yanıt.write()* yardımcı yöntemini istemciye geri göndermek için kullanmak için eylem yöntemlerimiz içinde kod yazmak mümkün olsa da, bu yaklaşım hızla oldukça hantal hale gelir. Çok daha iyi bir yaklaşım bizim için sadece bizim DinnersController eylem yöntemleri içinde uygulama ve veri mantığı gerçekleştirmek için, ve daha sonra bunun HTML gösterimi outputting sorumlu ayrı bir "görünüm" şablonuna html yanıtı işlemek için gerekli verileri geçmek için. Bir anda göreceğimiz gibi, "görünüm" şablonu genellikle HTML biçimlendirmesi ve gömülü işleme kodunun bir birleşimini içeren bir metin dosyasıdır.

Denetleyici mantığımızı bizim görüşümüzden ayırmak birçok büyük avantaj sağlar. Özellikle, uygulama kodu ve Kullanıcı Arabirimi biçimlendirme/işleme kodu arasında net bir "endişe ayrımı" uygulanmasına yardımcı olur. Bu, kullanıcı arası oluşturma mantığından izole olarak uygulama mantığını birim test etmeyi çok daha kolay hale getirir. Uygulama kodu değişiklikleri yapmak zorunda kalmadan kullanıcı bire-posta oluşturma şablonlarını daha sonra değiştirmeyi kolaylaştırır. Ayrıca, geliştiricilerin ve tasarımcıların projelerde birlikte işbirliği yapmalarını kolaylaştırabilir.

DinnersController sınıfımızı, iki eylem yöntemimizin yöntem imzalarını bir "void" dönüş türüne sahip olmaktan değiştirerek bir HTML Kullanıcı Aracı yanıtı göndermek için bir görünüm şablonu kullanmak istediğimizi belirtmek için güncelleyebiliriz, bunun yerine bir "ActionResult" dönüş türüne sahip olabiliriz. Daha sonra aşağıdaki gibi bir "ViewResult" nesnesini geri döndürmek için Denetleyici taban sınıfındaki *Görünüm()* yardımcı yöntemini çağırabiliriz:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

Yukarıda kullandığımız *View()* yardımcı yönteminin imzası aşağıdaki gibi görünür:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*Görünüm()* yardımcı yönteminin ilk parametresi, HTML yanıtını işlemek için kullanmak istediğimiz görünüm şablondosyasının adıdır. İkinci parametre, GÖRÜNÜM şablonu HTML yanıtını işlemek için gereken verileri içeren bir model nesnesidir.

Index() eylem yöntemimiz içinde *Görünüm()* yardımcı yöntemini çağırıyoruz ve "Index" görünüm şablonu kullanarak akşam yemeklerinin HTML listesini işlemek istediğimizi belirtiyoruz. Görünümü şablonundan, listeyi oluşturmak için bir dizi Akşam Yemeği nesnesi geçiyoruz:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Ayrıntılar() eylem yöntemimiz içinde, URL'de verilen kimliği kullanarak bir Akşam Yemeği nesnesi almaya çalışırız. Geçerli bir Akşam Yemeği bulunursa, alınan Akşam Yemeği nesnesini işlemek için bir "Ayrıntılar" görünüm şablonu kullanmak istediğimizi belirten *Görünüm()* yardımcı yöntemini çağırırız. Geçersiz bir akşam yemeği istenirse, Akşam Yemeğinin "Bulundu Değil" görünüm şablonu (ve yalnızca şablon adını alan *Görünüm()* yardımcı yönteminin aşırı yüklü bir sürümünü kullanarak var olmadığını belirten yararlı bir hata iletisi kullanırız:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Şimdi "Bulundu", "Ayrıntılar" ve "Dizin" görünüm şablonlarını uygulayalım.

### <a name="implementing-the-notfound-view-template"></a>"Bulunamadı" Görünüm Şablonu'nu uygulama

İstenen akşam yemeğinin bulunamadığını belirten dostça bir hata iletisi görüntüleyen "Bulundu" görünüm şablonu uygulayarak başlayacağız.

Metin imlecimizi bir denetleyici eylem yöntemine yerleştirerek yeni bir görünüm şablonu oluşturacağız ve sonra sağ tıklayıp "Görünüm Ekle" menüsü komutunu seçeceğiz (Ctrl-M, Ctrl-V yazarak da bu komutu uygulayabiliriz):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Bu, aşağıdaki gibi bir "Görünüm Ekle" iletişim kutusunu gündeme getirir. Varsayılan olarak iletişim kutusu, imlecin iletişim başlatıldığında bulunduğu eylem yönteminin adıyla eşleşecek şekilde oluşturulacak görünümün adını önceden dolduracaktır (bu durumda "Ayrıntılar"). Önce "Bulundu Değil" şablonuna uygulamak istediğimizden, bu görünüm adını geçersiz kılacağız ve bunun yerine "Bulundu" olarak ayarlayacağız:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizininde bizim için yeni bir "NotFound.aspx" görünüm şablonu oluşturur (dizin zaten yoksa bunu da oluşturur):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Ayrıca kod düzenleyicisi içinde yeni "NotFound.aspx" görünüm şablonu açılır:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

Varsayılan olarak şablonları görüntüleyin, içerik ve kod ekleyebileceğimiz iki "içerik bölgesi" vardır. İlk bize geri gönderilen HTML sayfasının "başlık" özelleştirmek için izin verir. İkinci bize geri gönderilen HTML sayfasının "ana içeriği" özelleştirmek için izin verir.

"Bulundu Değil" görünüm şablonumuzu uygulamak için bazı temel içerik ekleyeceğiz:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Daha sonra tarayıcı içinde deneyebilirsiniz. Bunu yapmak için *"/Dinners/Details/9999"* URL'sini isteyelim. Bu, şu anda veritabanında bulunmayan bir akşam yemeğine atıfta bulunacak ve DinnersController.Details() eylem yöntemimizin "Bulunduama" görünüm şablonumuzu oluşturmasına neden olur:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Yukarıdaki ekran görüntüsünde fark edeceksiniz bir şey, temel görünüm şablonumuz ekrandaki ana içeriği çevreleyen bir grup HTML'yi devralmıştır. Bunun nedeni, görünüm şablonumuz, sitedeki tüm görünümlerde tutarlı bir düzen uygulamamızı sağlayan bir "ana sayfa" şablonu kullanıyor olmasıdır. Bu öğreticinin sonraki bir bölümünde ana sayfaların nasıl daha fazla çalıştığını tartışacağız.

### <a name="implementing-the-details-view-template"></a>"Ayrıntılar" Görünüm Şablonu'nu uygulama

Şimdi tek bir Akşam Yemeği modeli için HTML oluşturacak olan "Ayrıntılar" görünüm şablonu uygulayalım.

Bunu metin imlecimizi Ayrıntılar eylem yöntemine yerleştirerek yapacağız ve sonra sağ tıklayıp "Görünüm Ekle" menüsü komutunu (veya Ctrl-M, Ctrl-V tuşuna basın):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Bu, "Görünüm Ekle" iletişim kutusunu gündeme getirir. Varsayılan görünüm adını ("Ayrıntılar") saklarız. Ayrıca iletişim kutusunda "Güçlü bir şekilde yazılan Görünüm" onay kutusunu seçeriz ve Denetleyici'den Görünüm'e geçmekte olduğumuz model türünün adını (combobox açılır açılır ını kullanarak) seçeriz. Bu görünüm için bir Akşam Yemeği nesnesi geçiyoruz (bu tür için tam nitelikli adı: "NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

"Boş Görünüm" oluşturmayı seçtiğimiz önceki şablonun aksine, bu sefer "Ayrıntılar" şablonu kullanarak görünümü otomatik olarak "iskele" olarak seçeceğiz. Bunu, yukarıdaki iletişim kutusunda "İçeriği Görüntüle" açılır görünümünü değiştirerek gösterebiliriz.

"İskele" biz geçmekte olan Akşam Yemeği nesnedayalı bizim ayrıntıları görünüm şablonu bir ilk uygulama oluşturacaktır. Bu, görünüm şablonu uygulamamıza hızla başlamamız için kolay bir yol sağlar.

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizini içinde bizim için yeni bir "Details.aspx" görünüm şablon dosyası oluşturur:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Ayrıca kod düzenleyicisi içinde yeni "Details.aspx" görünüm şablonumuzu da açacaktır. Bir Akşam Yemeği modeline dayalı bir ayrıntı görünümü bir ilk iskele uygulaması içerecektir. İskele motoru, sınıfa maruz kalan genel özelliklere bakmak için .NET yansımasını kullanır ve bulduğu her türe göre uygun içerik ekler:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

Bu "ayrıntılar" iskele uygulamasının tarayıcıda nasıl göründüğünü görmek için *"/Dinners/Details/1"* URL'sini isteyebiliriz. Bu URL'yi kullanmak, veritabanımızı ilk oluşturduğımızda el ile eklediğimiz akşam yemeklerinden birini görüntüler:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

Bu bizi hızlı bir şekilde çalışır hale alır ve Details.aspx görünümümüzün ilk uygulamasını sağlar. Daha sonra gidip bizim memnuniyeti için UI özelleştirmek için çimdik.

Details.aspx şablonuna daha yakından baktığımızda, statik HTML'nin yanı sıra gömülü işleme kodu içerdiğini görürsünüz. &lt;%&gt; kod külçeleri görünüm şablonu işlendiğinde &lt;kodu&gt; yürütür ve %= % kod külçeleri içlerinde bulunan kodu çalıştırır ve sonucu şablonun çıktı akışına işler.

Güçlü bir şekilde yazılan "Model" özelliğini kullanarak denetleyicimizden geçirilen "Akşam Yemeği" model nesnesine erişen Kodu Görünümümüze yazabiliriz. Visual Studio editör içinde bu "Model" özelliği erişirken tam kod-intellisense bize sağlar:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Son Ayrıntılar görünümü şablonumuzun kaynağının aşağıdaki gibi görünmesi için bazı değişiklikler yapalım:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

*"/Dinners/Details/1"* URL'ye tekrar erişidiğimizde aşağıdaki gibi işlenecektir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>"Dizin" Görünüm Şablonu Uygulama

Şimdi yaklaşan Akşam Yemekleri'nin listesini oluşturacak olan "Index" görünüm şablonuna uygulayalım. Bunu yapmak için metin imlecimizi Dizin eylem yöntemi içinde konumlandıracağız ve sonra sağ tıklayıp "Görünüm Ekle" menüsü komutunu (veya Ctrl-M, Ctrl-V tuşuna basın) seçeceğiz.

"Görünüm Ekle" iletişim kutusunda "Dizin" adlı görünüm şablonunu saklarız ve "Güçlü bir şekilde yazılmış görünüm oluştur" onay kutusunu seçeriz. Bu sefer otomatik olarak bir "Liste" görünüm şablonu oluşturmayı seçeceğiz ve görünüme geçen model türü olarak "NerdDinner.Models.Dinner"ı seçeceğiz (ki biz bir "Liste" iskelesi oluşturduğumuzu belirttiğimiz için, Görünüm Ekle iletişim kutusunu denetleyicimizden Görünüm'e bir dizi akşam yemeği nesnesi geçirdiğimizi varsaymaya neden olacağız):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizini içinde bizim için yeni bir "Index.aspx" görünüm şablon dosyası oluşturur. Bu görünüme geçmek Akşam Yemekleri bir HTML tablo listesi sağlayan içinde bir ilk uygulama "iskele" olacaktır.

Uygulamayı çalıştırdığımızda ve *"/Dinners/"* URL'ye erişirken aşağıdaki gibi akşam yemekleri listemizi işleyecek:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

Yukarıdaki tablo çözümü bize Akşam Yemeği verilerimizin ızgara benzeri bir düzenini verir – ki bu bizim tüketicimiz akşam yemeği listesiyle karşı karşıya için istediğimiz gibi değildir. Index.aspx görünüm şablonu güncelleştirebilir ve daha az veri sütunu listelemek için değiştirebilir ve aşağıdaki kodu kullanarak tablo yerine bunları işlemek için bir &lt;ul&gt; öğesi kullanabiliriz:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Modelimizdeki her akşam yemeğini döngüye sokarak yukarıdaki foreach deyimi içinde "var" anahtar sözcüğümüzü kullanıyoruz. C# 3.0'a aşina olmayanlar "var" kullanmanın yemek nesnesinin geç bağlı olduğu anlamına geldiğini düşünebilirler. Bunun yerine derleyici güçlü bir şekilde yazılan "Model" özelliğine ("Ayrılmaz&lt;Akşam Yemeği"&gt;türünden) karşı tür çıkarımı kullandığı ve yerel "akşam yemeği" değişkenini akşam yemeği türü olarak derlediği anlamına gelir – bu da kod blokları içinde tam intellisense ve derleme zamanı kontrolü yaptığımız anlamına gelir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Tarayıcımızdaki */Dinners* URL'sinde yenile tuşuna bastığımızda güncellenmiş görünümümüz şu şekilde görünür:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

Bu daha iyi görünüyor - ama tamamen henüz orada değil. Son adımımız, son kullanıcıların listedeki tek tek Akşam Yemekleri'ni tıklatmalarını ve bunlarla ilgili ayrıntıları görmelerini sağlamaktır. Bunu, DinnersController'ımızdaki Ayrıntılar eylem yöntemine bağlantı veren HTML köprü öğelerini oluşturarak uygulayacağız.

Bu köprüleri Index görünümümüzde iki şekilde oluşturabiliriz. Bunlardan &lt;ilki, HTML'yi&gt; el ile aşağıdaki gibi &lt;bir&gt; öğe &lt;oluşturmak&gt; ve bir HTML öğesine % bloklar yerleştirdiğimiz aşağıdaki gibi bir öğe oluşturmaktır:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Kullanabileceğimiz alternatif bir yaklaşım, programlı bir HTML &lt;oluşturmayı destekleyen ASP.NET MVC içindeki yerleşik "Html.ActionLink()"&gt; yardımcı yönteminden yararlanmaktır, denetleyicide başka bir eylem yöntemine bağlantı veren bir öğe:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink() yardımcı yönteminin ilk parametresi, görüntülenecek bağlantı metnidir (bu durumda akşam yemeğinin başlığı), ikinci parametre bağlantı oluşturmak istediğimiz Denetleyici eylem adıdır (bu durumda Ayrıntılar yöntemi) ve üçüncü parametre eyleme gönderilecek bir parametre kümesidir (özellik adı/değerleri olan anonim bir tür olarak uygulanır). Bu durumda bağlantı vermek istediğimiz yemeğin "id" parametresini belirtiriz ve ASP.NET MVC'deki varsayılan URL yönlendirme kuralı "{Controller}/{Action}/{id}" olduğundan Html.ActionLink() yardımcı yöntemi aşağıdaki çıktıyı oluşturur:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Index.aspx görünümüiçin Html.ActionLink() yardımcı yöntemi yaklaşımını kullanacağız ve her akşam yemeğini uygun ayrıntılar URL'sinin liste bağlantısında bulacağız:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

Ve şimdi biz */ Dinners* URL bizim akşam yemeği listesi vurmak aşağıdaki gibi görünüyor:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Listedeki Akşam Yemekleri'nden herhangi birini tıklattığımızda, bu sayfayla ilgili ayrıntıları görmek için gideriz:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Kural tabanlı adlandırma ve \Görünümler dizini yapısı

ASP.NET MVC uygulamaları varsayılan olarak görünüm şablonlarını çözerken kural tabanlı dizin adlandırma yapısı kullanır. Bu, geliştiricilerin denetleyici sınıfının görünümlerine başvururken bir konum yolunu tam olarak nitelemek zorunda kalmamalarını sağlar. Varsayılan olarak ASP.NET MVC, uygulamanın altındaki *\Views\[ControllerName]\* dizinindeki görünüm şablonu dosyasını arar.

Örneğin, "Index", "Details" ve "NotFound" olmak üzere üç görünüm şablonuna açıkça atıfta bulunan DinnersController sınıfı üzerinde çalışıyoruz. ASP.NET MVC varsayılan olarak uygulama kök dizini altında *\Views\Dinners* dizininde bu görünümleri arar:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Proje içinde şu anda üç denetleyici sınıfı (DinnersController, HomeController ve AccountController – projeyi oluşturduğumuzda varsayılan olarak son ikisi eklendi) ve \Görünümler dizininde üç alt dizin (her bir denetleyici için bir tane) vardır.

Ev ve Hesap denetleyicilerinden başvurulan görünümler, görünüm şablonlarını ilgili *\Görünümler\Ev ve \Görünümler\Hesap* dizinlerinden otomatik olarak çözer. *\Views\Account* *\Views\Shared* alt dizini, uygulama içinde birden çok denetleyici arasında yeniden kullanılan görünüm şablonlarını depolamak için bir yol sağlar. ASP.NET MVC bir görünüm şablonu çözmeye çalıştığında, önce *\Views\[Controller]* belirli dizininde denetler ve görünüm şablonu burada bulamazsa *\Views\Shared* dizininin içinde görünecektir.

Tek tek görünüm şablonlarını adlandırma söz konusu olduğunda, önerilen kılavuz, görünüm şablonuna işlenmesine neden olan eylem yöntemiyle aynı adı paylaşmasını sağlamaktır. Örneğin, "Dizin" eylem yöntemimizin üzerinde görünüm sonucunu işlemek için "Dizin" görünümü ve "Ayrıntılar" eylem yöntemi sonuçlarını işlemek için "Ayrıntılar" görünümünü kullanıyor. Bu, her eylemle hangi şablonun ilişkili olduğunu hızlı bir şekilde görmenizi kolaylaştırır.

Görünüm şablonu denetleyicide çağrılan eylem yöntemiyle aynı ada sahipolduğunda, geliştiricilerin görünüm şablonadını açıkça belirtmeleri gerekmez. Bunun yerine model nesnesini "View()" yardımcı yöntemine geçirebiliriz (görünüm adını belirtmeden) ve ASP.NET MVC otomatik olarak *diskteki\[\[\Views ControllerName] ActionName]* görünüm şablonundan kullanmak istediğimizi ortaya çıkaracaktır.

Bu, denetleyici kodumuzu biraz temizlememizi ve kodumuzda adı iki kez çoğaltmaktan kaçınmamızı sağlar:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

Yukarıdaki kod site için güzel bir Akşam Yemeği listesi / ayrıntıları deneyimi uygulamak için gerekli olan tüm.

#### <a name="next-step"></a>Sonraki Adım

Şimdi inşa güzel bir Akşam Yemeği tarama deneyimi var.

Şimdi CRUD (Create, Read, Update, Delete) veri form düzenleme desteğini etkinleştirelim.

> [!div class="step-by-step"]
> [Önceki](build-a-model-with-business-rule-validations.md)
> [Sonraki](provide-crud-create-read-update-delete-data-form-entry-support.md)
