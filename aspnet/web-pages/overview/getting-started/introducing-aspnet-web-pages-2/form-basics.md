---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: ASP.NET Web Sayfaları Tanıtımı - HTML Form Temelleri | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu öğretici, bir giriş formu oluşturmanın ve web sayfalarını (Ustura) ASP.NET kullandığınızda kullanıcının girdisini nasıl işleyeceğiniz le ilgili temel bilgileri gösterir. Ve şimdi sen ...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676330"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Web Sayfalarından ASP.NET Tanıtımı - HTML Form Temelleri

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> Bu öğretici, bir giriş formu oluşturmanın ve web sayfalarını (Ustura) ASP.NET kullandığınızda kullanıcının girdisini nasıl işleyeceğiniz le ilgili temel bilgileri gösterir. Artık bir veritabanınız olduğuna göre, kullanıcıların veritabanındaki belirli filmleri bulmasına izin vermek için form becerilerinizi kullanacaksınız. [Web Sayfalarını kullanarak Veri Görüntülemeye Giriş](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)yoluyla seriyi tamamladığınızı varsayar ASP.NET.
> 
> Öğrenecekleriniz:
> 
> - Standart HTML öğelerini kullanarak form oluşturma.
> - Nasıl bir formda kullanıcının giriş okumak için.
> - Kullanıcının sağladığı bir arama terimini kullanarak seçici olarak veri alan bir SQL sorgusu nasıl oluşturulur?
> - Sayfada alanların kullanıcının ne girişettiğini "unutma" sağlay
>   
> 
> Tartışılan özellikler/teknolojiler:
> 
> - `Request` nesnesi.
> - SQL `Where` yan tümcesi.

## <a name="what-youll-build"></a>Ne İnşa Edeceksiniz

Önceki öğreticide, bir veritabanı oluşturdunuz, veritabanına veri `WebGrid` eklediniz ve sonra da verileri görüntülemek için yardımcıyı kullandınız. Bu öğreticide, belirli bir türün filmlerini bulmanıza olanak tanıyan veya başlığı girdiğiniz sözcüğü içeren bir arama kutusu eklersiniz. (Örneğin, türü "Aksiyon" olan veya başlığı "Harry" veya "Macera" içeren tüm filmleri bulabilirsiniz.)

Bu öğretici ile bittiğinde, bu gibi bir sayfa olacak:

![Tür ve Başlık araması yapılan filmler sayfası](form-basics/_static/image1.png)

Sayfanın listeleme bölümü, son öğretici &mdash; ızgaradakiyle aynıdır. Aradaki fark, ızgaranın yalnızca aradığınız filmleri göstermesi olacaktır.

## <a name="about-html-forms"></a>HTML Formları Hakkında

(HTML formları oluşturma ve arasındaki `GET` fark ile ilgili `POST`deneyime sahipseniz, bu bölümü atlayabilirsiniz.)

Formda kullanıcı giriş &mdash; öğeleri metin kutuları, düğmeler, radyo düğmeleri, onay kutuları, açılır listeler ve benzeri öğeler vardır. Kullanıcılar bu denetimleri doldurur veya seçim yapar ve bir düğmeyi tıklatarak formu gönderir.

Bir formun temel HTML sözdizimi şu örnekte gösterilmiştir:

[!code-html[Main](form-basics/samples/sample1.html)]

Bu biçimlendirme bir sayfada çalıştığında, bu çizime benzeyen basit bir form oluşturur:

![Tarayıcıda işlenen temel HTML formu](form-basics/_static/image2.png)

Öğe `<form>` gönderilecek HTML öğelerini içine alar. (Kolay bir hata yapmak sayfaya öğeleri eklemek için ama sonra `<form>` bir öğe içine koymak için unutmak. Bu durumda, hiçbir şey sunulmaz.) Öznitelik, `method` tarayıcıya kullanıcı girişinin nasıl gönderilebildiğini söyler. Bunu, sunucuda bir güncelleştirme gerçekleştiriyorsanız veya `post` `get` yalnızca sunucudan veri alıyorsanız ayarlayabilirsiniz.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST ve HTTP Fiil Güvenliği**
> 
> Tarayıcıların ve sunucuların bilgi alışverişinde kullanmak için kullandığı protokol HTTP, temel işlemlerinde son derece basittir. Tarayıcılar sunuculara istekte bulunmak için yalnızca birkaç fiil kullanır. Web için kod yazarken, bu fiilleri ve tarayıcının ve sunucunun bunları nasıl kullandığını anlamak yararlıdır. Uzak ve uzak en sık kullanılan fiiller şunlardır:
> 
> - `GET`. Tarayıcı sunucudan bir şey almak için bu fiili kullanır. Örneğin, tarayıcınıza bir URL yazdığınızda, tarayıcı `GET` istediğiniz sayfayı istemek için bir işlem gerçekleştirir. Sayfa grafikler içeriyorsa, tarayıcı `GET` görüntüleri almak için ek işlemler gerçekleştirir. İşlemin `GET` bilgileri sunucuya aktarması gerekiyorsa, bilgiler sorgu dizesindeki URL'nin bir parçası olarak aktarılır.
> - `POST`. Tarayıcı, sunucuya eklenecek veya değiştirilecek verileri göndermek için bir `POST` istek gönderir. Örneğin, `POST` fiil bir veritabanında kayıt oluşturmak veya varolanları değiştirmek için kullanılır. Çoğu zaman, bir formu doldurup gönder düğmesini tıklattığınızda, `POST` tarayıcı bir işlem gerçekleştirir. Bir `POST` işlemde, sunucuya aktarılan veriler sayfanın gövdesindedir.
> 
> Bu fiiller arasındaki önemli bir `GET` ayrım, bir işlemin sunucudaki hiçbir şeyi değiştirmemesi veya biraz daha `GET` soyut bir şekilde ifade etmesi, bir işlemin sunucuda durum değişikliğine yol açamayan olmasıdır. Aynı kaynaklarda `GET` istediğiniz kadar işlem gerçekleştirebilirsiniz ve bu kaynaklar değişmez. (Bir `GET` işlemin genellikle "güvenli" olduğu veya teknik bir terim kullandığı söylenir, *iktidara gelir.)* Buna karşılık, tabii `POST` ki, bir istek işlemi gerçekleştirmek her zaman sunucuda bir şey değiştirir.
> 
> İki örnek bu ayrımı niçin göstermeme yardımcı olacaktır. Bing veya Google gibi bir motoru kullanarak arama yaptığınızda, bir metin kutusundan oluşan bir form doldurursunuz ve ardından arama düğmesini tıklatırsınız. Tarayıcı, URL'nin bir parçası olarak geçirilen kutuya girdiğiniz değerle bir `GET` işlem gerçekleştirir. Bu `GET` form türü için bir işlem kullanmak iyidir, çünkü bir arama işlemi sunucudaki kaynakları değiştirmez, yalnızca bilgileri getirir.
> 
> Şimdi çevrimiçi bir şey sipariş süreci düşünün. Sipariş ayrıntılarını doldurun ve sonra gönder düğmesini tıklatın. Bu işlem bir `POST` istek olacaktır, çünkü işlem sunucuda yeni bir sipariş kaydı, hesap bilgilerinizde değişiklik ve belki de diğer birçok değişiklik gibi değişikliklere neden olur. İşlemin `GET` aksine, isteğinizi `POST` yineleyemezsiniz — eğer yaptıysa, isteği her yeniden gönderdiğinizde, sunucuda yeni bir sipariş oluşturursunuz. (Bu gibi durumlarda, web siteleri genellikle bir gönder düğmesini birden fazla kez tıklatmamanız konusunda sizi uyarır veya formu yanlışlıkla yeniden göndermemeniz için gönder düğmesini devre dışı kalacaktır.)
> 
> Bu öğretici süresince, HTML formları ile `GET` çalışmak `POST` için hem bir işlem hem de bir işlem kullanırsınız. Her durumda kullandığınız fiilin neden uygun olduğunu açıklayacağız.
> 
> (HTTP fiilleri hakkında daha fazla bilgi edinmek için W3C sitesindeki [Yöntem Tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makalesine bakın.)

Çoğu kullanıcı giriş öğesi `<input>` HTML öğeleridir. Bunlar, `<input type="type" name="name">,` *yazın* istediğiniz kullanıcı giriş denetimi türünü gösterdiği yere benzer. Bu öğeler ortak olanlardır:

- Metin kutusu:`<input type="text">`
- Onay kutusu:`<input type="check">`
- Radyo düğmesi:`<input type="radio">`
- Düğme:`<input type="button">`
- Gönder düğmesi:`<input type="submit">`

Ayrıca, çok `<textarea>` satırlı bir metin kutusu ve `<select>` bir açılır liste veya kaydırılabilir liste oluşturmak için öğe oluşturmak için öğeyi kullanabilirsiniz. (HTML form öğeleri hakkında daha fazla bilgi için W3Schools sitesindeki [HTML Formları ve Giriş'e](http://www.w3schools.com/html/html_forms.asp) bakın.)

Öznitelik `name` çok önemlidir, çünkü ad, kısa bir süre sonra göreceğiniz gibi öğenin değerini daha sonra nasıl alacağınızdır.

İşin ilginç yanı, sayfa geliştiricisi olarak kullanıcının girişiyle ne yaptığınızdır. Bu öğelerle ilişkili yerleşik bir davranış yoktur. Bunun yerine, kullanıcının girdiği veya seçtiği değerleri almanız ve onlarla bir şeyler yapmanız gerekir. Bu öğreticide bunu öğreneceksiniz.

> [!TIP] 
> 
> **HTML5 ve Giriş Formları**
> 
> Bildiğiniz gibi, HTML geçiş ve en son sürümü (HTML5) kullanıcıların bilgi girmek için daha sezgisel yollar için destek içerir. Örneğin, HTML5'te siz (sayfa geliştiricisi) sayfaya kullanıcının bir tarih girmesini istediğinizi söyleyebilirsiniz. Tarayıcı daha sonra, kullanıcının bir tarihi el ile girmesini gerektirmek yerine takvimi otomatik olarak görüntüleyebilir. Ancak, HTML5 yenidir ve henüz tüm tarayıcılarda desteklenmez.
> 
> ASP.NET Web Sayfaları HTML5 girdisini kullanıcının tarayıcısı kadar destekler. HTML5'teki `<input>` öğenin yeni öznitelikleri hakkında bir fikir için W3Schools sitesindeki [HTML &lt;giriş&gt; türü Özniteliği'ne](http://www.w3schools.com/html/html_form_input_types.asp) bakın.

## <a name="creating-the-form"></a>Form Oluşturma

WebMatrix'te, **Dosyalar** çalışma alanında *Movies.cshtml* sayfasını açın.

Kapanış `</h1>` etiketinden sonra ve `<div>` aramanın `grid.GetHtml` açılış etiketinden önce aşağıdaki işaretlemeyi ekleyin:

[!code-html[Main](form-basics/samples/sample2.html)]

Bu biçimlendirme, bir metin kutusu ve `searchGenre` bir gönder düğmesi olan bir form oluşturur. Metin kutusu ve gönder düğmesi, `<form>` özniteliği `method` `get`'' olarak ayarlanmış bir öğeyle çevrilidir. (Metin kutusunu koymazsanız ve düğmeyi bir `<form>` öğenin içine göndermezseniz, düğmeyi tıklattığınızda hiçbir şey gönderilmeyecektir.) `GET` Burada fiili kullanırsınız, çünkü sunucuda herhangi bir değişiklik yapmayan bir form oluşturuyorsunuz — bu sadece bir aramayla sonuçlanır. (Önceki öğreticide, sunucuya `post` değişiklikleri gönderme yöntemini kullandınız. Bunu bir sonraki öğreticide tekrar göreceksiniz.)

Sayfayı çalıştırın. Form için herhangi bir davranış tanımlamamış olsanız da, nasıl göründüğünü görebilirsiniz:

![Tür için arama kutusu ile Filmler sayfası](form-basics/_static/image3.png)

Metin kutusuna "Komedi" gibi bir değer girin. Ardından **Arama Türü'ne**tıklayın.

Sayfanın URL'sini not alın. Öğenin `<form>` `method` özniteliğini `get`, girdiğiniz değer artık URL'deki sorgu dizesinin bir parçası olarak ayarladığınızda, aşağıdaki gibi:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Okuma Formu Değerleri

Sayfa zaten veritabanı verilerini alan ve sonuçları bir ızgarada görüntüleyen bazı kodlar içerir. Şimdi arama terimini içeren bir SQL sorgusu çalıştırabilmeniz için metin kutusunun değerini okuyan bazı kodlar eklemeniz gerekir.

Formun yöntemini `get`, metin kutusuna girilen değeri aşağıdaki gibi kod kullanarak okuyabilirsiniz:

`var searchTerm = Request.QueryString["searchGenre"];`

Nesne `Request.QueryString` `QueryString` `Request` (nesnenin özelliği) `GET` işlemin bir parçası olarak gönderilen öğelerin değerlerini içerir. Özellik, `Request.QueryString` formda gönderilen değerlerin bir *koleksiyonunu* (bir liste) içerir. Herhangi bir bireysel değer almak için, istediğiniz öğenin adını belirtirsiniz. Bu nedenle metin kutusunu oluşturan `name` `<input>` öğe`searchTerm`() öğesi üzerinde bir öznitelik olması gerekir. `Request` (Nesne hakkında daha fazla bilgi için kenar [çubuğuna](#BKMK_TheRequestObject) daha sonra bakın.)

Metin kutusunun değerini okuyacak kadar basit. Ancak kullanıcı metin kutusuna hiçbir şey girmemişse ancak yine de **Ara'yı** tıklattıysa, aranacak bir şey olmadığından bu tıklamayı yok sayabilirsiniz.

Aşağıdaki kod, bu koşulların nasıl uygulanacağını gösteren bir örnektir. (Henüz bu kodu eklemek zorunda değilsiniz; bir dakika içinde bunu yapacağız.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Test bu şekilde bozulur:

- Adlı `Request.QueryString["searchGenre"]` `searchGenre` `<input>` öğeye girilen değeri , yani değeri alın.
- `IsEmpty` Yöntemi kullanarak boş olup olmadığını öğrenin. Bu yöntem, bir şeyin (örneğin, form öğesi) bir değer iyp içermediğini belirlemenin standart yoludur. Ama gerçekten, bu nedenle, boş *değilse* sadece bakım ...
- `IsEmpty` İşleç'i `!` testin önüne ekleyin. (Operatör `!` mantıksal NOT anlamına gelir).

Düz İngilizce, tüm `if` durum aşağıdaki çevirir: *formun searchGenre öğesi boş değilse, o zaman ...*

Bu blok, arama terimini kullanan bir sorgu oluşturmak için sahneyi ayarlar. Bunu bir sonraki bölümde yapacaksın.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **İstek Nesnesi**
> 
> Nesne, `Request` bir sayfa istendiğinde veya gönderildiğinde tarayıcının uygulamanıza gönderdiği tüm bilgileri içerir. Bu nesne, metin kutusu değerleri veya yüklenmesi gereken bir dosya gibi kullanıcının sağladığı tüm bilgileri içerir. Ayrıca, çerezler, URL sorgu dizesindeki değerler (varsa), çalışan sayfanın dosya yolu, kullanıcının kullandığı tarayıcı türü, tarayıcıda ayarlanan dillerin listesi ve çok daha fazlası gibi her türlü ek bilgi içerir.
> 
> Nesne, `Request` değerler *topluluğudur.* Adını belirterek koleksiyondan tek bir değer elde elabilirsiniz:
> 
> `var someValue = Request["name"];`
> 
> Nesne `Request` aslında birkaç alt kümeleri ortaya çıkarır. Örneğin:
> 
> - `Request.Form`istek bir `POST` istekse, `<form>` gönderilen öğeiçindeki öğelerden değerler verir.
> - `Request.QueryString`URL'nin sorgu dizesinde sadece değerleri verir. (URL gibi `http://mysite/myapp/page?searchGenre=action&page=2`bir `?searchGenre=action&page=2` URL'de, URL'nin bölümü sorgu dizesidir.)
> - `Request.Cookies`toplama, tarayıcının gönderdiği çerezlere erişmenizi sağlar.
> 
> Gönderdiğiniz formda olduğunu bildiğiniz bir değeri elde etmek `Request["name"]`için . Alternatif olarak, daha özel sürümleri `Request.Form["name"]` (istekler `Request.QueryString["name"]` için) `GET` `POST` veya (istekler için) kullanabilirsiniz. Tabii ki, *adı* almak için öğenin adıdır.
> 
> Almak istediğiniz öğenin adı, kullanmakta olduğunuz koleksiyonda benzersiz olmalıdır. Bu nedenle `Request` nesne, aşağıdaki gibi `Request.Form` alt `Request.QueryString`kümeleri sağlar. Sayfanızın adlı `userName` bir form öğesi içerdiğini ve `userName` *ayrıca* bir çerez içerdiğini varsayalım. `Request["userName"]`Alırsanız, form değerini mi yoksa çerezi mi istediğiniz belirsizdir. Ancak, hangi `Request.Form["userName"]` değeri `Request.Cookie["userName"]`alacağınız konusunda açık bir şekilde bilgi sahibi oluyorsunuz.
> 
> Belirli olmak ve ilgilendiğiniz alt kümesini `Request` kullanmak iyi bir uygulamadır, `Request.Form` `Request.QueryString`örneğin. Bu öğretici oluşturduğunuz basit sayfalar için, muhtemelen gerçekten herhangi bir fark yaratmaz. Ancak, müstehcen sürümü `Request.Form` kullanarak daha karmaşık sayfalar `Request.QueryString` oluşturduğunuzda veya sayfa bir form (veya birden çok form), tanımlama bilgileri, sorgu dize değerleri vb. içerdiğinde ortaya çıkabilecek sorunları önlemenize yardımcı olabilir.

## <a name="creating-a-query-by-using-a-search-term"></a>Arama Terimi Kullanarak Sorgu Oluşturma

Artık kullanıcının girdiği arama terimini nasıl alacağınızı bildiğinize göre, onu kullanan bir sorgu oluşturabilirsiniz. Tüm film öğelerini veritabanından çıkarmak için şu deyime benzeyen bir SQL sorgusu kullandığınızı unutmayın:

`SELECT * FROM Movies`

Yalnızca belirli filmleri almak için, yan tümce `Where` içeren bir sorgu kullanmanız gerekir. Bu yan tümce, sorgu tarafından satırları döndürülen bir koşul ayarlamanızı sağlar. Bir örneği aşağıda verilmiştir:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Temel biçimi `WHERE column = value`. Aradığınız alete bağlı `=`olarak, sadece , `>` (büyük), (daha az), `<` `<>` (eşit olmayan), `<=` (daha az veya eşit olmayan), vb. dışında farklı işleçler kullanabilirsiniz.

Eğer merak ediyorsanız, SQL deyimleri &mdash; `SELECT` büyük/küçük `Select` harf duyarlı `select`değildir (veya bile) aynıdır. Ancak, insanlar okunmasını kolaylaştırmak için genellikle `SELECT` `WHERE`bir SQL deyimindeki anahtar kelimeleri büyük harfe benzer.

### <a name="passing-the-search-term-as-a-parameter"></a>Arama terimini parametre olarak geçirme

Belirli bir türü aramak yeterince`WHERE Genre = 'Action'`kolaydır (), ancak kullanıcının girdiği herhangi bir türü arayabilmek istersiniz. Bunu yapmak için, arama değeri için bir yer tutucu içeren SQL sorgusu olarak oluşturursunuz. Bu komut gibi görünecektir:

`SELECT * FROM Movies WHERE Genre = @0`

Yer tutucu sıfırın `@` ardından gelen karakterdir. Tahmin edebileceğiniz gibi, bir sorgu birden çok yer tutucu `@0`içerebilir `@1` `@2`ve bu sorgular , , vb. olarak adlandırılır.

Sorguyu ayarlamak ve değeri gerçekten aktarmak için kodu aşağıdaki gibi kullanırsınız:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Bu kod, ızgaradaki verileri görüntülemek için zaten yaptığınız koda benzer. Tek fark:

- Sorgu bir yer tutucu`WHERE Genre = @0"`( ) içerir.
- Sorgu bir değişkene konur (`selectCommand`); önce, sorguyu doğrudan `db.Query` yönteme aktardınız.
- `db.Query` Yöntemi aradiğinizde, hem sorguyu hem de yer tutucu için kullanılacak değeri geçersiniz. (Sorguda birden çok yer tutucusu varsa, hepsini yönteme ayrı değerler olarak geçirirsiniz.)

Tüm bu öğeleri bir araya getirirseniz, aşağıdaki kodu alırsınız:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Önemli!** Değerleri SQL komutuna geçirmek için yer tutucuları (beğen) `@0`kullanmak güvenlik açısından son derece *önemlidir.* Burada gördüğünüz şekilde, değişken veri için yer tutucular, SQL komutları oluşturmanız gereken tek yoldur.
> 
> Kullanıcıdan aldığınız gerçek metin ve değerleri bir araya getirerek (birleşerek) bir SQL deyimi oluşturmayın. Kullanıcı girişini bir SQL deyimine dahil etmek, sitenizi kötü amaçlı bir kullanıcının veritabanınızı hackleyen değerler gönderdiği bir *SQL enjeksiyon saldırısına* açar. (Sen [makaleSQL Enjeksiyon](https://msdn.microsoft.com/library/ms161953.aspx) MSDN web sitesinde daha fazla bilgi edinebilirsiniz.)

## <a name="updating-the-movies-page-with-search-code"></a>Arama Kodu ile Filmler Sayfasını Güncelleme

Artık *Movies.cshtml* dosyasındaki kodu güncelleştirebilirsiniz. Başlamak için, sayfanın üst kısmındaki kod bloğundaki kodu bu kodla değiştirin:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Buradaki fark, sorguyu daha sonra geçeceğiniz `selectCommand` değişkene `db.Query` koymuş olmasıdır. SQL deyimini bir değişkene koymak, aramayı gerçekleştirmek için yapacağınız ifadeyi değiştirmenize olanak tanır.

Daha sonra geri koyacağınız bu iki satırı da kaldırdınız:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Sorguyu henüz çalıştırmak istemiyorsun (diğer bir şey, arama) `db.Query`ve yardımcının `WebGrid` başlatılmasını da henüz istemiyorsunuz. Bunları, hangi SQL deyiminin çalışması gerektiğini bulduktan sonra yaparsınız.

Bu yeniden yazıldı bloktan sonra, aramayı işlemek için yeni mantığı ekleyebilirsiniz. Tamamlanan kod aşağıdaki gibi görünecektir. Sayfanızdaki kodu şu örneğe uygun şekilde güncelleştirin:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Sayfa şimdi bu şekilde çalışıyor. Sayfa her çalıştığında, kod veritabanını açar `selectCommand` ve değişken `Movies` tablodaki tüm kayıtları alan SQL deyimine ayarlanır. Kod ayrıca değişkeni `searchTerm` de başharfe ait hale tir.

Ancak, geçerli istek `searchGenre` öğe için bir değer içeriyorsa, kod farklı bir sorguya ayarlar `selectCommand` - yani, bir tür aramak için yan tümceyi `Where` içeren birine. Ayrıca arama `searchTerm` kutusu (hiçbir şey olabilir) için geçti ne olursa olsun ayarlar.

Hangi SQL deyiminde `selectCommand`olursa olsun, kod `db.Query` sonra sorguyu çalıştırmak için `searchTerm`çağırır, ne olursa olsun geçen . Eğer içinde bir `searchTerm`şey yoksa, önemli değil, çünkü bu durumda zaten değeri geçmek `selectCommand` için hiçbir parametre yok.

Son olarak, kod, `WebGrid` daha önce olduğu gibi sorgu sonuçlarını kullanarak yardımcıyı işe adatandır.

SQL deyimini ve arama terimini değişkenlere koyarak koda esneklik eklediğinizi görebilirsiniz. Bu öğreticide daha sonra göreceğiniz gibi, bu temel çerçeveyi kullanabilir ve farklı arama türleri için mantık eklemeye devam edebilirsiniz.

## <a name="testing-the-search-by-genre-feature"></a>Türe Göre Arama Özelliğini Test Etme

WebMatrix'te *Movies.cshtml* sayfasını çalıştırın. Tür için metin kutusu olan sayfayı görürsünüz.

Test kayıtlarınızdan biri için girdiğiniz bir tür girin ve ardından **Ara'yı**tıklatın. Bu sefer sadece bu tür eşleşen filmlerin bir listesini görmek:

![Tür 'Komediler' aradıktan sonra Filmler sayfa listesi](form-basics/_static/image4.png)

Farklı bir tür girin ve yeniden arama yapın. Aramanın büyük/küçük harf olmadığını görebilmeniz için tüm küçük harfleri veya tüm büyük harfleri kullanarak türgirmeyi deneyin.

## <a name="remembering-what-the-user-entered"></a>Kullanıcının Girdiğini "Hatırlama"

Bir tür girdikten ve **Arama Türünü**tıklattıktan sonra, bu tür için bir liste gördüğünüzün fark etmiş olabilirsiniz. Ancak, arama metin kutusu &mdash; başka bir deyişle boştu, ne girdiğinizi hatırlamıyordu.

Bu davranışın neden oluştuğunu anlamak önemlidir. Bir sayfa gönderdiğinde, tarayıcı web sunucusuna bir istek gönderir. ASP.NET isteği aldığında, sayfanın yepyeni bir örneğini oluşturur, sayfadaki kodu çalıştırır ve sayfayı yeniden tarayıcıya işler. Sonuç olarak, ancak, sayfa sadece kendisi bir önceki sürümü ile çalıştığını bilmiyor. Tek bildiği, içinde bazı form verileri olan bir istek olduğu.

Bir sayfayı &mdash; ilk kez istediğinizde veya göndererek &mdash; her istediğinizde yeni bir sayfa elde esiniz. Web sunucusu, son isteğinizle ilgili hiçbir belleğe sahip değildir. Ne ASP.NET, ne de tarayıcı yok. Sayfanın bu ayrı örnekleri arasındaki tek bağlantı, aralarında ilettiğiniz verilerdir. Örneğin, bir sayfa gönderirseniz, yeni sayfa örneği önceki örnek tarafından gönderilen form verilerini alabilir. (Sayfalar arasında veri aktarmanın başka bir yolu da çerezleri kullanmaktır.)

Bu durumu açıklamak için resmi bir yolu web sayfaları *vatansız*olduğunu söylemektir. Web sunucuları ve sayfaların kendileri ve sayfadaki öğeler, bir sayfanın önceki durumu hakkında herhangi bir bilgi tutmaz. Web bu şekilde tasarlanmıştır, çünkü tek tek istekler için durumu korumak, genellikle saniyede binlerce, belki de yüz binlerce isteği işleyen web sunucularının kaynaklarını hızla tüketir.

Bu yüzden metin kutusu boştu. Sayfayı gönderdikten sonra, ASP.NET sayfanın yeni bir örneğini oluşturdu ve kod ve biçimlendirme de koştu. O kodda ASP.NET metin kutusuna değer biçmelerini söyleyen hiçbir şey yoktu. Yani ASP.NET bir şey yapmadı ve metin kutusu içinde bir değer olmadan işlendi.

Aslında bu sorunu aşmak için kolay bir yolu var. Metin *kutusuna* girdiğiniz tür, içinde bulunduğu &mdash; kodda `Request.QueryString["searchGenre"]`kullanılabilir.

Metin kutusunun biçimlendirmesini, özniteliğin değerini şu `searchTerm`örnekteki gibi alabilmesi `value` için güncelleştirin:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Bu sayfada, bu değişken girdiğiniz türü `searchTerm` de içerdiğinden, değişkene özniteliği de ayarlamış `value` olabilirsiniz. Ancak, `Request` burada gösterildiği `value` gibi özniteliği ayarlamak için nesneyi kullanmak, bu görevi gerçekleştirmenin standart yoludur. (Bazı durumlarda bunu &mdash; yapmak istediğinizi varsayarsak, sayfayı alanlarda değerler *olmadan* işlemek isteyebilirsiniz. Her şey uygulamanızda neler olduğuna bağlıdır.)

> [!NOTE]
> Parolalar için kullanılan bir metin kutusunun değerini "hatırlayamaz". Bu, kişilerin kod kullanarak parola alanını doldurmasına izin veren bir güvenlik açığı olacaktır.

Sayfayı yeniden çalıştırın, bir tür girin ve **Arama Türünü**tıklatın. Bu kez sadece arama sonuçlarını görmekle kalmıyor, metin kutusu da geçen kez girdiğiniz şeyi hatırlıyor:

![Metin kutusunun önceki girişi 'hatırladığını' gösteren sayfa](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Başlıkta Herhangi Bir Sözcük Aranıyor

Artık herhangi bir türü arayabilirsiniz, ancak bir başlık da aramak isteyebilirsiniz. Arama yaparken tam olarak doğru bir başlık almak zordur, bu nedenle bir başlığın içinde herhangi bir yerde görünen bir sözcüğü arayabilirsiniz. Bunu SQL'de yapmak için `LIKE` işleci ve sözdizimini aşağıdaki gibi kullanırsınız:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Bu komut, başlıkları "macera" içeren tüm filmleri alır. İşleç `LIKE` kullandığınızda, arama teriminin `%` bir parçası olarak joker karakter eklersiniz. Arama `LIKE 'adventure%'` "macera' ile başlayan" anlamına gelir. (Teknik olarak, "dize 'macera' bir şey takip anlamına gelir.) Benzer şekilde, arama `LIKE '%adventure'` terimi "'macera' ile biten" demenin başka bir yolu olan "macera" dizesini takip eden her şey anlamına gelir.

Bu nedenle `LIKE '%adventure%'` arama terimi başlığın herhangi bir yerinde "macera" anlamına gelir. (Teknik olarak, "başlık bir şey, 'macera' takip, bir şey takip.")

Öğenin `<form>` içine, tür araması için `</div>` kapanış etiketinin hemen altına aşağıdaki `</form>` biçimlendirmeyi ekleyin (kapanış öğesinden hemen önce):

[!code-html[Main](form-basics/samples/sample10.html)]

Bu aramayı işleyen kod, `LIKE` aramayı birleştirmeniz dışında tür aramasının koduna benzer. Sayfanın üst kısmındaki kod bloğunun `if` içine, tür `if` araması için bloktan hemen sonra bu bloğu ekleyin:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Bu kod, aramanın bir `LIKE` işleç kullanması ve kodun arama`%`teriminden önce ve sonra " olarak koyması dışında, daha önce gördüğünüz mantığı kullanır.

Sayfaya başka bir arama eklemenin ne kadar kolay olduğuna dikkat edin. Tek yapman gereken:

- İlgili `if` arama kutusunun bir değeri olup olmadığını görmek için sınanan bir blok oluşturun.
- Değişkeni `selectCommand` yeni bir SQL deyimine ayarlayın.
- Değişkeni `searchTerm` sorguya geçmek üzere değere ayarlayın.

Başlık araması için yeni mantığı içeren tam kod bloğu aşağıda veda eder:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Bu kodun yaptıklarının bir özeti aşağıda vereb:

- Değişkenler `searchTerm` ve `selectCommand` üst te başharf. Bu değişkenleri, kullanıcının sayfada yaptıklarına göre uygun arama terimine (varsa) ve uygun SQL komutuna göre ayarlayasınız. Varsayılan arama veritabanından tüm filmleri alma basit bir durumdur.
- Için `searchGenre` ve `searchTitle`, kod için `searchTerm` testlerde aramak istediğiniz değere ayarlar. Bu kod blokları `selectCommand` da bu arama için uygun bir SQL komutu ayarlanır.
- Yöntem, `db.Query` SQL komutu ne olursa olsun `selectedCommand` ve hangi değerde `searchTerm`olursa olsun kullanılarak yalnızca bir kez çağrılır. Arama terimi yoksa (tür ve başlık sözcüğü yok), değeri boş bir `searchTerm` dizedir. Ancak, bu durumda sorgu bir parametre gerektirmez, çünkü bu önemli değildir.

## <a name="testing-the-title-search-feature"></a>Başlık Arama Özelliğini Test Etme

Artık tamamlanmış arama sayfanızı test edebilirsiniz. *Filmler.cshtml*çalıştırın.

Bir tür girin ve **Arama Türünü**tıklatın. Izgara, daha önce olduğu gibi, bu türün filmlerini görüntüler.

Bir başlık sözcüğü girin ve **Arama Başlığı'nı**tıklatın. Izgara, başlıkta bu sözcüğü içeren filmleri görüntüler.

![Başlıkta 'The' arandıktan sonra filmler sayfası nın listesi](form-basics/_static/image6.png)

Her iki metin kutularını da boş bırakın ve her iki düğmeye tıklayın. Izgara tüm filmleri görüntüler.

## <a name="combining-the-queries"></a>Sorguları Birleştirme

Gerçekleştirebileceğiniz aramaların özel olduğunu fark edebilirsiniz. Her iki arama kutusuda da değerler olsa bile, başlığı ve türü aynı anda arayamaabilirsiniz. Örneğin, başlığı "Macera" olan tüm aksiyon filmlerini arayamaabilirsiniz. (Sayfa şimdi kodlanmış olduğundan, hem tür hem de başlık için değerler girerseniz, başlık araması öncelikli olur.) Koşulları birleştiren bir arama oluşturmak için, aşağıdaki gibi sözdizimi olan bir SQL sorgusu oluşturmanız gerekir:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

Ve aşağıdaki gibi bir ifade kullanarak sorgu çalıştırmak gerekir (kabaca konuşma):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Gördüğünüz gibi, arama ölçütlerinin birçok permütasyonuna izin verecek mantık oluşturmak biraz karışabilir. Bu yüzden burada duracağız.

## <a name="coming-up-next"></a>Sonraki Geliyor

Bir sonraki öğreticide, kullanıcıların veritabanına film eklemesine izin vermek için form kullanan bir sayfa oluşturursunuz.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Film Sayfası için Tam Listeleme (Arama ile Güncellendi)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Jilet Sözdizimini Kullanarak ASP.NET Web Programlamaya Giriş](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools sitesinde [SQL WHERE Yan tümcesi](http://www.w3schools.com/sql/sql_where.asp)
- W3C sitesinde [Yöntem Tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makale

> [!div class="step-by-step"]
> [Önceki](displaying-data.md)
> [Sonraki](entering-data.md)
