---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: ASP.NET Web sayfalarına giriş-HTML form temelleri | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda bir giriş formu oluşturma ve kullanıcının girişini işleme hakkında temel bilgiler gösterilmektedir. Şimdi...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345462"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>ASP.NET Web sayfalarına giriş-HTML form temelleri

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda bir giriş formu oluşturma ve kullanıcının girişini işleme hakkında temel bilgiler gösterilmektedir. Artık bir veritabanınız olduğuna göre, kullanıcıların veritabanında belirli filmleri bulmasına izin vermek için form becerilerinizi kullanacaksınız. [ASP.NET Web sayfalarını kullanarak verileri görüntülemeye giriş](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)ile seriyi tamamlamış olduğunu varsayar.
> 
> Öğrenecekleriniz:
> 
> - Standart HTML öğelerini kullanarak form oluşturma.
> - Kullanıcının bir formdaki girişini okuma.
> - Kullanıcının sağladığı bir arama terimini kullanarak verileri seçmeli olarak alan bir SQL sorgusu oluşturma.
> - "Kullanıcının ne girdiği" konusunda "hatırlama" sayfasında alan
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - `Request` nesnesi.
> - SQL `Where` yan tümcesi.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Önceki öğreticide, bir veritabanı oluşturdunuz, ona veri ekledi ve sonra `WebGrid` verileri göstermek için yardımcı 'yı kullandınız. Bu öğreticide, belirli bir tarzın filmlerini bulmanıza veya başlığında girdiğiniz herhangi bir sözcük içeren bir arama kutusu ekleyeceksiniz. (Örneğin, tarzı "Action" olan veya başlığı "Harry" veya "Adventure" içeren tüm filmleri bulabilirsiniz.

Bu öğreticiyi tamamladığınızda, şöyle bir sayfanız olacaktır:

![Tarz ve başlık arama içeren filmler sayfası](form-basics/_static/image1.png)

Sayfanın listeleme bölümü, bir kılavuzun son öğreticisiyle aynıdır &mdash; . Fark, kılavuzun yalnızca aradığınız filmleri gösterecektir.

## <a name="about-html-forms"></a>HTML formları hakkında

(HTML formları oluşturma ve ile arasındaki fark ile ilgili deneyiminiz varsa `GET` `POST` , bu bölümü atlayabilirsiniz.)

Bir formda Kullanıcı giriş öğeleri &mdash; metin kutuları, düğmeler, radyo düğmeleri, onay kutuları, açılan listeler vb. bulunur. Kullanıcılar bu denetimleri doldurur veya seçimler yapar ve ardından bir düğmeye tıklayarak formu gönderir.

Bir formun temel HTML sözdizimi bu örneğe göre gösterilmiştir:

[!code-html[Main](form-basics/samples/sample1.html)]

Bu biçimlendirme bir sayfada çalıştığında, bu çizimi şöyle görünen basit bir form oluşturur:

![Tarayıcıda işlenmiş şekilde temel HTML formu](form-basics/_static/image2.png)

`<form>`Öğesi GÖNDERILECEK HTML öğelerini barındırır. (Oluşturmanın kolay bir hata olması, sayfaya öğe eklemek ve ardından bunları bir öğe içine koymayı unutmak olur `<form>` . Bu durumda hiçbir şey gönderilmez.) `method` Özniteliği, tarayıcıya Kullanıcı girişini nasıl gönderebileceklerini bildirir. `post`Sunucuda bir güncelleştirme gerçekleştirmeniz veya `get` sunucudan yalnızca veri getirmeniz durumunda bunu olarak ayarlayın.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST ve HTTP fiil güvenliği**
> 
> Tarayıcı ve sunucuların bilgi alışverişi için kullandığı protokol olan HTTP, temel işlemlerinde daha basit bir işlemdir. Tarayıcılar, sunuculara istek yapmak için yalnızca birkaç fiil kullanır. Web için kod yazdığınızda, bu yüklemleri ve tarayıcının ve sunucunun bunları nasıl kullandığını anlamanız yararlı olur. En yaygın olarak kullanılan fiiller şunlardır:
> 
> - `GET`. Tarayıcı, sunucudan bir şeyi getirmek için bu fiili kullanır. Örneğin, tarayıcınıza bir URL yazdığınızda, tarayıcı `GET` istediğiniz sayfayı istemek için bir işlem gerçekleştirir. Sayfa grafik içeriyorsa, tarayıcı `GET` görüntüleri almak için ek işlemler gerçekleştirir. `GET`İşlemin sunucuya bilgi geçirmesi gerekiyorsa, bilgiler sorgu DIZESINDEKI URL 'nin bir parçası olarak geçirilir.
> - `POST`. Tarayıcı, `POST` sunucuda eklenecek veya değiştirilecek verileri göndermek için bir istek gönderir. Örneğin, `POST` fiil bir veritabanında kayıtlar oluşturmak veya var olanları değiştirmek için kullanılır. Çoğu zaman, bir formu doldururken ve Gönder düğmesine tıkladığınızda tarayıcı bir `POST` işlem gerçekleştirir. Bir `POST` işlemde, sunucuya geçirilmekte olan veriler sayfanın gövdesinde bulunur.
> 
> Bu fiiller arasındaki önemli bir ayrım, bir `GET` işlemin sunucu üzerinde herhangi bir şeyi değiştirmesi veya biraz daha soyut bir şekilde yerleştirmek için beklenmemelidir; bir `GET` işlem, sunucuda durumunda değişikliğe neden olmaz. `GET`Aynı kaynaklar üzerinde dilediğiniz kadar bir işlem yapabilirsiniz ve bu kaynaklar değişmez. (Bir `GET` işlem genellikle "güvenli" olarak ya da teknik bir dönem kullanmak için *ıdempotent*.) Bunun aksine, bir `POST` istek işlemi gerçekleştirdiğiniz her seferinde sunucuda bir şeyi değiştirir.
> 
> Bu ayrımı göstermeye yardımcı olacak iki örnek vardır. Bing veya Google gibi bir altyapıyı kullanarak arama gerçekleştirdiğinizde, tek bir metin kutusundan oluşan bir formu doldurup Ara düğmesine tıklayabilirsiniz. Tarayıcı, `GET` URL 'nin bir parçası olarak geçirilen kutuya girdiğiniz değerle bir işlem gerçekleştirir. `GET`Bu tür bir form için bir işlem kullanmak iyidir, çünkü bir arama işlemi sunucudaki kaynakları değiştirmez, yalnızca bilgi getirir.
> 
> Şimdi bir şeyi çevrimiçi olarak sıralama sürecini göz önünde bulundurun. Sipariş Ayrıntıları ' nı doldurup Gönder düğmesine tıklayabilirsiniz. Bu işlem bir istek olacaktır `POST` , çünkü işlem yeni bir sipariş kaydı, hesap bilgilerinde bir değişiklik ve belki de birçok başka değişiklik gibi sunucu üzerinde değişikliklere neden olur. İşlemin aksine `GET` , isteğinizi tekrarlayükleyemezsiniz `POST` — siz isteği her yeniden yapılandırdığınızda, sunucuda yeni bir sipariş oluşturursunuz. (Bu gibi durumlarda, Web siteleri genellikle bir Gönder düğmesine birden çok kez tıklamamanızı veya formu yanlışlıkla yeniden gönderemeyecek şekilde Gönder düğmesini devre dışı bırakacağını uyarır.)
> 
> Bu öğreticide, `GET` HTML formlarıyla çalışmak için hem işlem hem de bir işlem kullanacaksınız `POST` . Kullandığınız fiilin her durumda uygun bir durum olduğunu açıklayacağız.
> 
> (HTTP fiilleri hakkında daha fazla bilgi için bkz. W3C sitesindeki [Yöntem tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makalesi.)

Çoğu kullanıcı girişi öğesi HTML `<input>` öğeleridir. `<input type="type" name="name">,`Burada *tür* , istediğiniz kullanıcı giriş denetimi türünü gösterir. Bu öğeler yaygın olanlardır:

- Metin kutusu: `<input type="text">`
- Onay kutusu: `<input type="check">`
- Radyo düğmesi: `<input type="radio">`
- Bu `<input type="button">`
- Gönder düğmesi: `<input type="submit">`

Ayrıca, `<textarea>` öğesini kullanarak bir çoklu satır metin kutusu ve `<select>` bir açılan liste veya kaydırılabilir liste oluşturmak için öğesi de kullanabilirsiniz. (HTML form öğeleri hakkında daha fazla bilgi için, bkz. W3Schools sitesinde [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) .)

`name`Özniteliği çok önemlidir, çünkü ad daha sonra göreceğiniz gibi, daha sonra bir öğenin değerini alabilir.

İlginç olan bölüm, sayfa geliştiricisi, kullanıcının girişi ile yapılır. Bu öğelerle ilişkili yerleşik davranış yok. Bunun yerine, kullanıcının girdiği veya seçtiği değerleri almanız ve bunlarla ilgili bir şey yapmanız gerekir. Bu öğreticide öğrenirsiniz.

> [!TIP] 
> 
> **HTML5 ve giriş formları**
> 
> Bildiğiniz gibi, HTML geçiştir ve en son sürüm (HTML5), kullanıcıların bilgi girmesi için daha sezgisel yollar desteği içerir. Örneğin, HTML5 'de, sizin (sayfa geliştiricisi), sayfanın bir tarih girmesini istediğinizi söyleyebilir. Tarayıcı, kullanıcının el ile tarih girmesini gerektirmek yerine otomatik olarak bir takvim görüntüleyebilir. Ancak HTML5 yenidir ve henüz tüm tarayıcılarda desteklenmez.
> 
> ASP.NET Web sayfaları, kullanıcı tarayıcısının bulunduğu ölçüde HTML5 girişini destekler. HTML5 içindeki öğe için yeni öznitelikler hakkında fikir için `<input>` , bkz. w3schools sitesinde [HTML &lt; giriş &gt; türü özniteliği](http://www.w3schools.com/html/html_form_input_types.asp) .

## <a name="creating-the-form"></a>Form Oluşturma

WebMatrix 'te **dosyalar** çalışma alanında, *filmler. cshtml* sayfasını açın.

Kapanış etiketinden sonra `</h1>` ve çağrının açılış etiketinden önce `<div>` `grid.GetHtml` , aşağıdaki biçimlendirmeyi ekleyin:

[!code-html[Main](form-basics/samples/sample2.html)]

Bu biçimlendirme, adlı bir metin kutusu ve Gönder düğmesi içeren bir form oluşturur `searchGenre` . Metin kutusu ve Gönder düğmesi, `<form>` özniteliği olarak ayarlanmış bir öğe içine alınmıştır `method` `get` . (Metin kutusunu ve Gönder düğmesini bir öğesi içine yerleştirmezseniz `<form>` , düğmeye tıkladığınızda hiçbir şey gönderilmeyecektir.) `GET` Burada fiil, sunucuda herhangi bir değişiklik yapmayan bir form oluşturduğunuz için kullanılır; yalnızca bir aramaya neden olur. (Önceki öğreticide, bir `post` yöntemi kullandınız, bu da sunucuya değişiklikleri nasıl gönderirsiniz. Sonraki öğreticide bir daha görürsünüz.)

Sayfayı çalıştırın. Form için herhangi bir davranış tanımlamamış olsanız da, neye benzebileceğinize bakabilirsiniz:

![Tarz için arama kutusu içeren filmler sayfası](form-basics/_static/image3.png)

Metin kutusuna "komedi" gibi bir değer girin. Ardından **Ara tarzı**' ne tıklayın.

Sayfanın URL 'sini bir yere göz atın. `<form>`Öğenin `method` özniteliğini olarak ayarlarsanız `get` , GIRDIĞINIZ değer artık URL 'deki sorgu dizesinin bir parçasıdır, örneğin:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Form değerlerini okuma

Sayfa, veritabanı verilerini alan ve sonuçları bir kılavuzda görüntüleyen bazı kodları zaten içeriyor. Artık, arama terimini içeren bir SQL sorgusunu çalıştırabilmeniz için metin kutusunun değerini okuyan bazı kodlar eklemeniz gerekir.

Formun yöntemini olarak ayarladığınız için `get` , aşağıdaki gibi bir kod kullanarak metin kutusuna girilen değeri okuyabilirsiniz:

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString`Nesnesi ( `QueryString` `Request` nesnesinin özelliği), işlemin bir parçası olarak gönderilen öğelerin değerlerini içerir `GET` . `Request.QueryString`Özelliği, formda gönderilen değerlerin bir *koleksiyonunu* (bir listesini) içerir. Tek bir değer almak için istediğiniz öğenin adını belirtirsiniz. Bu nedenle, `name` `<input>` metin kutusunu oluşturan öğesinde () bir özniteliğe sahip olmanız gerekir `searchTerm` . (Nesne hakkında daha fazla bilgi için, `Request` [kenar çubuğuna](#BKMK_TheRequestObject) daha sonra bakın.)

Metin kutusunun değerini okumak yeterince basittir. Ancak Kullanıcı, metin kutusuna hiç bir şey girmediyse ancak **Ara** ' yı tıklamadığında, arama yapmak için hiçbir şey olmadığından, tıklamayı yoksayabilirsiniz.

Aşağıdaki kod, bu koşulların nasıl uygulanacağını gösteren bir örnektir. (Bu kodu henüz eklemeniz gerekmez; bunu bir süre sonra yapmanız gerekir.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Test şu şekilde aşağı doğru bir şekilde kesilir:

- Değerini `Request.QueryString["searchGenre"]` , adlı öğesine girilen değeri değerini alır `<input>` `searchGenre` .
- Yöntemini kullanarak boş olup olmadığını öğrenin `IsEmpty` . Bu yöntem, bir şeyin (örneğin, form öğesi) bir değer içerip içermediğini belirlemenin standart yoludur. Ancak aslında yalnızca boş *değil* , bu nedenle...
- `!`Testin önüne işleci ekleyin `IsEmpty` . ( `!` İşleç MANTıKSAL değil anlamına gelir).

Düz Ingilizce olarak, tüm `if` koşul aşağıdaki gibi *olur: formun searchtarz öğesi boş değilse.* ..

Bu blok arama terimini kullanan bir sorgu oluşturmak için aşamayı belirler. Bunu bir sonraki bölümde yapacaksınız.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Istek nesnesi**
> 
> `Request`Nesnesi, bir sayfa istendiğinde veya gönderildiğinde tarayıcının uygulamanıza gönderdiği tüm bilgileri içerir. Bu nesne, kullanıcının sağladığı, metin kutusu değerleri veya karşıya yüklenecek bir dosya gibi tüm bilgileri içerir. Ayrıca, tanımlama bilgileri, URL sorgu dizesindeki (varsa), çalışan sayfanın dosya yolu, kullanıcının kullandığı tarayıcı türü, tarayıcıda ayarlanan dillerin listesi ve çok daha fazlası gibi ek bilgilerin tümünü de içerir.
> 
> `Request`Nesne, değerlerin bir *koleksiyon* (liste). Adını belirterek koleksiyondan tek bir değer alırsınız:
> 
> `var someValue = Request["name"];`
> 
> `Request`Nesnesi aslında çeşitli alt kümeler sunar. Örneğin:
> 
> - `Request.Form``<form>`istek bir istek ise, gönderilen öğe içindeki öğelerin değerlerini verir `POST` .
> - `Request.QueryString` size yalnızca URL 'nin sorgu dizesindeki değerleri verir. (Benzer bir URL 'de `http://mysite/myapp/page?searchGenre=action&page=2` , `?searchGenre=action&page=2` URL 'nin bölümü sorgu dizesidir.)
> - `Request.Cookies` koleksiyon, tarayıcının gönderdiği tanımlama bilgilerine erişmenizi sağlar.
> 
> Gönderilen formda olduğunu bildiğiniz bir değer almak için kullanabilirsiniz `Request["name"]` . Alternatif olarak, daha belirli sürümleri `Request.Form["name"]` ( `POST` istekler için) veya `Request.QueryString["name"]` (istekler için) kullanabilirsiniz `GET` . Kuşkusuz, *ad* alınacak öğenin adıdır.
> 
> Almak istediğiniz öğenin adı, kullanmakta olduğunuz koleksiyon içinde benzersiz olmalıdır. Bu nedenle nesne, `Request` ve gibi alt kümeleri sağlar `Request.Form` `Request.QueryString` . Sayfanızın adlı bir form öğesi içerdiğini `userName` ve *Ayrıca* adlı bir tanımlama bilgisi içerdiğini varsayalım `userName` . `Request["userName"]`Bu değeri alırsanız, form değerinin mi yoksa tanımlama bilgisinin mi olmasını istediğinize belirsizdir. Ancak, `Request.Form["userName"]` veya alırsanız `Request.Cookie["userName"]` , hangi değeri alacağınız hakkında açık olursunuz.
> 
> Belirli bir uygulama `Request` , veya gibi ilgilendiğiniz alt kümesini kullanmak iyi bir uygulamadır `Request.Form` `Request.QueryString` . Bu öğreticide oluşturmakta olduğunuz basit sayfalar için büyük olasılıkla herhangi bir farklılık yapmaz. Ancak, daha karmaşık sayfalar oluştururken, açık sürümü kullanarak `Request.Form` veya `Request.QueryString` sayfa bir form (veya birden çok form içerdiğinde), tanımlama bilgileri, sorgu dizesi değerleri vb. içerdiğinde ortaya çıkabilecek sorunları önlemenize yardımcı olabilir.

## <a name="creating-a-query-by-using-a-search-term"></a>Arama terimi kullanarak sorgu oluşturma

Artık kullanıcının girdiği arama teriminin nasıl alınacağını öğrenmiş olduğunuza göre, onu kullanan bir sorgu oluşturabilirsiniz. Tüm film öğelerini veritabanından almak için, bu ifadeye benzeyen bir SQL sorgusu kullandığınızı unutmayın:

`SELECT * FROM Movies`

Yalnızca belirli filmleri almak için, yan tümce içeren bir sorgu kullanmanız gerekir `Where` . Bu yan tümce, sorgu tarafından döndürülen satırları ayarlamanıza olanak sağlar. İşte bir örnek:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Temel biçim `WHERE column = value` . `=` `>` `<` `<>` Ne aradığınıza bağlı olarak, tıpkı (büyüktür), (küçüktür), (eşit değildir), `<=` vb. gibi farklı işleçleri kullanabilirsiniz.

Merak ediyorsanız SQL deyimleri büyük/küçük harfe duyarlı değildir &mdash; `SELECT` `Select` (veya hatta `select` ). Ancak insanlar, daha kolay okunmasını sağlamak için, ve gibi bir SQL deyimindeki anahtar kelimeleri genellikle büyük harfle `SELECT` `WHERE` okur.

### <a name="passing-the-search-term-as-a-parameter"></a>Arama terimi parametre olarak geçiliyor

Belirli bir tarzı aramak yeterince kolay ( `WHERE Genre = 'Action'` ), ancak kullanıcının girdiği tarz için arama yapmak isteyebilirsiniz. Bunu yapmak için, Aranacak değer için bir yer tutucu içeren bir SQL sorgusu oluşturun. Bu komut şöyle görünür:

`SELECT * FROM Movies WHERE Genre = @0`

Yer tutucu, `@` ardından sıfır karakter olur. Tahmin edebildiği gibi, bir sorgu birden fazla yer tutucu içerebilir ve adı,, `@0` `@1` `@2` vb. olarak adlandırılır.

Sorguyu ayarlamak ve bunu gerçekten değeri geçirmek için, aşağıdaki gibi bir kod kullanın:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Bu kod, kılavuzda verileri göstermek için yapmış olduğunuz verilere benzer. Tek farklar şunlardır:

- Sorgu bir yer tutucu ( `WHERE Genre = @0"` ) içeriyor.
- Sorgu bir değişkene ( `selectCommand` ) konur, önce sorguyu doğrudan yöntemine geçirtiniz `db.Query` .
- `db.Query`Yöntemini çağırdığınızda, hem sorguyu hem de yer tutucu için kullanılacak değeri geçitirsiniz. (Sorguda birden fazla yer tutucu varsa, bunları yönteme ayrı değerler olarak geçirirsiniz.)

Tüm bu öğeleri birlikte yerleştirirseniz, aşağıdaki kodu alırsınız:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Önemli!** `@0`SQL komutuna değer geçirmek için yer tutucuları (gibi) kullanmak, güvenlik açısından *son derece önemlidir* . Burada gördüğünüz gibi, değişken veri yertutucuları ile birlikte SQL komutları oluşturmanız gereken tek yoldur.
> 
> Değişmez değer metin ve kullanıcıdan aldığınız değerleri birlikte koyarak bir SQL ifadesini hiçbir şekilde oluşturun. Kullanıcı girişini bir SQL ifadesine bitiştirme, sitenizi kötü niyetli bir kullanıcının sayfanıza bir değer gönderdiği bir *SQL ekleme saldırısında* açar. (MSDN Web sitesini [ekleme](https://msdn.microsoft.com/library/ms161953.aspx) başlıklı makalede daha fazla bilgi edinebilirsiniz.)

## <a name="updating-the-movies-page-with-search-code"></a>Filmler sayfasını arama koduyla güncelleştirme

Artık *film. cshtml* dosyasındaki kodu güncelleştirebilirsiniz. Başlamak için, sayfanın üst kısmındaki kod bloğundaki kodu şu kodla değiştirin:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Buradaki fark, `selectCommand` daha sonra geçirilecek olan değişkenine sorgu koymanızdır `db.Query` . SQL ifadesini bir değişkene koymak, aramayı gerçekleştirmek için yapmanız gereken ifadeyi değiştirmenize olanak sağlar.

Ayrıca, daha sonra geri yerleştirilecek bu iki satırı da kaldırmış olursunuz:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Sorguyu henüz çalıştırmak istemezsiniz (yani çağrısı `db.Query` ) ve yardımcı 'yı henüz başlatmak istemezsiniz `WebGrid` . Bu şeyleri, SQL deyimin çalıştırılacağı iletişime aldıktan sonra gerçekleştirirsiniz.

Bu yeniden yazan bloğundan sonra, aramayı işlemeye yönelik yeni mantığı ekleyebilirsiniz. Tamamlanan kod aşağıdaki gibi görünür. Sayfanızdaki kodu, bu örnekle eşleşecek şekilde güncelleştirin:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Sayfa artık bunun gibi çalışmaktadır. Sayfa her çalıştığında, kod veritabanını açar ve `selectCommand` değişken, tablodaki tüm kayıtları alan SQL ifadesine ayarlanır `Movies` . Kod ayrıca değişkeni de başlatır `searchTerm` .

Ancak, geçerli istek öğesi için bir değer içeriyorsa `searchGenre` , kod `selectCommand` farklı bir sorguya (yani, `Where` bir tarz aramak için yan tümcesini içeren bir) ayarlar. Ayrıca `searchTerm` , arama kutusu için geçirilmiş şekilde ayarlanır (hiçbir şey olmayabilir).

Hangi SQL deyimden bağımsız olarak olursa olsun `selectCommand` , kod daha sonra `db.Query` sorguyu çalıştırmak için ' i çağırır `searchTerm` . İçinde hiçbir şey yoksa `searchTerm` , bu durum büyük değildir, çünkü bu durumda değeri yine de değerine geçirmek için parametre yoktur `selectCommand` .

Son olarak, kod, `WebGrid` daha önce olduğu gibi sorgu sonuçlarını kullanarak yardımcı başlatır.

SQL ifadesini ve arama terimini değişkenlere koyarak koda esneklik eklemişseniz bunu görebilirsiniz. Bu öğreticide daha sonra göreceğiniz gibi, bu temel çerçeveyi kullanabilir ve farklı arama türleri için mantık eklemeyi koruyabilirsiniz.

## <a name="testing-the-search-by-genre-feature"></a>Türe göre arama özelliğini test etme

WebMatrix 'te, *filmler. cshtml* sayfasını çalıştırın. Sayfayı tarz için metin kutusuyla görürsünüz.

Test kayıtlarınız için girmiş olduğunuz bir tarz girin ve **Ara**' ya tıklayın. Bu zaman, yalnızca bu tarz ile eşleşen filmlerle ilgili bir liste görürsünüz:

![' Comedies ' tarzı aranırken filmlere sayfa listeleme](form-basics/_static/image4.png)

Farklı bir tarz girin ve tekrar arama yapın. Aramanın büyük/küçük harfe duyarlı olmadığını görebilmeniz için tüm küçük harfleri veya tüm büyük harfleri kullanarak tarzı girmeyi deneyin.

## <a name="remembering-what-the-user-entered"></a>Kullanıcının girdiği "hatırlama"

Bir tarz girdikten ve **arama tarzında**tıklandıktan sonra, bu tarz için bir liste gördünüz. Ancak, arama metin kutusu &mdash; diğer sözcüklerde boştu, ne girdiğinizi hatıraramamıştı.

Bu davranışın neden oluştuğunu anlamak önemlidir. Bir sayfa gönderdiğinizde, tarayıcı Web sunucusuna bir istek gönderir. ASP.NET isteği aldığında, sayfanın marka-yeni bir örneğini oluşturur, kod içinde çalıştırır ve sonra sayfayı tarayıcıda yeniden oluşturur. Aslında, sayfa yalnızca önceki bir sürümü ile çalıştıbildiğinizi bilmez. Tüm BT, içinde bazı form verileri bulunan bir istek olduğunu bilir.

İlk kez veya gönderdikten sonra bir sayfa istediğinizde &mdash; &mdash; Yeni bir sayfa alıyorsunuz. Web sunucusunda son isteğiniz bellek yok. , ASP.NET yapmaz ve hiçbir ikisini de yapmaz. Sayfanın bu ayrı örnekleri arasındaki tek bağlantı, aralarında iletim yaptığınız herhangi bir veri olur. Örneğin, yeni sayfa örneği, bir sayfa gönderirseniz, önceki örnek tarafından gönderilen form verileri alabilir. (Sayfalar arasında veri geçirmenin diğer bir yolu tanımlama bilgilerini kullanmaktır.)

Bu durumu tanımlamanın resmi bir yolu, Web sayfalarının *durum bilgisiz*olduğu söydir. Web sunucuları ve sayfaları ve sayfadaki öğeler, sayfanın önceki durumu hakkında herhangi bir bilgi bulundurmaz. Web bu şekilde tasarlanmıştır çünkü bireysel isteklerin bakım durumu, genellikle binlerce, hatta yüzlerce binlerce istek (saniyede) işleyen Web sunucularının kaynaklarını hızla tüketti.

Bu nedenle metin kutusunun boş olması neden oldu. Sayfayı gönderdikten sonra, ASP.NET sayfanın yeni bir örneğini oluşturdu ve kod ve biçimlendirme üzerinden çalışır. Bu kodda, metin kutusuna bir değer ASP.NET söylenecek bir şey yok. Bu nedenle ASP.NET hiçbir şey yapmamıştı ve metin kutusu bu değerde bir değer olmadan işlenmiştir.

Bu sorunu geçici olarak yapmanın kolay bir yolu vardır. Metin *kutusuna girdiğiniz tarz,* içinde olduğu kodda sizin için kullanılabilir &mdash; `Request.QueryString["searchGenre"]` .

`value` `searchTerm` Bu örnekte olduğu gibi, özniteliğin değerini aldığından, metin kutusu için biçimlendirmeyi güncelleştirin:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Bu sayfada Ayrıca, `value` `searchTerm` girmiş olduğunuz tarz da içerdiği için özniteliği değişkenine de ayarlayabilirsiniz. Ancak, `Request` `value` Bu görevi gerçekleştirmenin standart yolu aşağıda gösterildiği gibi özniteliğini ayarlamak için nesnesini kullanmaktır. (Bazı durumlarda bunu yapmak istediğiniz varsayılarak &mdash; , bu sayfayı alanlarda değer *olmadan* işlemek isteyebilirsiniz. Hepsi, uygulamanızla ilgili olan yeniliklere bağlıdır.)

> [!NOTE]
> Parolalar için kullanılan bir metin kutusunun değerini "hatırlayamıyorum". Bu, kullanıcıların kod kullanarak bir parola alanını doldurmasına izin veren bir güvenlik deliği olacaktır.

Sayfayı yeniden çalıştırın, bir tarz girin ve **tarz ara**' yı tıklatın. Bu süre yalnızca aramanın sonuçlarını görmemiş, ancak metin kutusu son kez girdiklerinizi anımsar:

![Metin kutusunun önceki girişin ' hatırlanan ' olduğunu gösteren sayfa](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Başlıktaki herhangi bir sözcük aranıyor

Artık herhangi bir tarz için arama yapabilirsiniz, ancak bir başlık aramak da isteyebilirsiniz. Arama yaptığınızda bir başlık tam olarak doğru bir şekilde almak zordur. bunun yerine başlık içinde herhangi bir yerde görünen bir sözcük arayabilirsiniz. Bunu SQL 'de yapmak için `LIKE` aşağıdaki gibi işlecini ve sözdizimini kullanın:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Bu komut, başlıkları "Adventure" içeren tüm filmleri alır. `LIKE`İşlecini kullandığınızda, `%` arama teriminin bir parçası olarak joker karakterini dahil edersiniz. Arama `LIKE 'adventure%'` "' Adventure ' ile başlıyor" anlamına gelir. (Teknik olarak, "Adventure" dizesinin ardından herhangi bir şey olduğu anlamına gelir. ") Benzer şekilde, arama terimi `LIKE '%adventure'` "' Adventure '" dizesi tarafından izlenen "" Adventure "ile biten" söylemenin bir diğer yolu anlamına gelir.

Bu nedenle arama terimi, `LIKE '%adventure%'` "Adventure" başlığında her yerde "Adventure" anlamına gelir. " (Teknik olarak, başlıktaki her şey, ' Adventure ' ve ardından herhangi bir şey). ")

Öğesinin içinde `<form>` , aşağıdaki biçimlendirmeyi, tarz aramasının sağ etiketi altına ekleyin `</div>` (kapanış öğesinden hemen önce `</form>` ):

[!code-html[Main](form-basics/samples/sample10.html)]

Bu aramayı işleme kodu, ara değer arama koduna benzer, ancak aramayı birleştirme yapmanız gerekir `LIKE` . Sayfanın üst kısmındaki kod bloğunun içinde, bu `if` bloğu yalnızca `if` tarz arama bloğundan sonra ekleyin:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Bu kod, daha önce gördüğünüz mantığı kullanır, ancak arama bir `LIKE` işleç kullanır ve kod, `%` arama teriminden önce ve sonra "" koyar.

Sayfada başka bir aramanın nasıl daha kolay bir şekilde ekleneceğini fark edin. Yapmanız gerekdik:

- `if`İlgili arama kutusunun bir değere sahip olup olmadığını görmek için test edilmiş bir blok oluşturun.
- `selectCommand`Değişkeni yeni BIR SQL ifadesine ayarlayın.
- `searchTerm`Değişkeni sorguya geçirilecek değere ayarlayın.

Aşağıda bir başlık araması için yeni mantığı içeren tüm kod bloğu verilmiştir:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Bu kodun ne işe yönelik bir özet aşağıda verilmiştir:

- Değişkenler `searchTerm` ve `selectCommand` en üstte başlatılır. Bu değişkenleri, kullanıcının sayfada ne yaptığını temel alarak uygun arama terimine (varsa) ve uygun SQL komutuna göre ayarlayacağız. Varsayılan arama, tüm filmlerden veritabanından alınması için basit bir durumdur.
- Ve için testlerinde `searchGenre` `searchTitle` , kod, `searchTerm` aramak istediğiniz değere ayarlanır. Bu kod blokları `selectCommand` , bu arama için uygun BIR SQL komutuna de ayarlanır.
- `db.Query`Yöntemi yalnızca bir kez çağrılır, HANGI SQL komutunun içinde olduğu `selectedCommand` ve hangi değerin bulunduğu `searchTerm` . Arama terimi (tarz yok ve başlık sözcüğü yoksa) yoksa, değeri `searchTerm` boş bir dizedir. Ancak, bu nedenle sorgu bir parametre gerektirmediğinden bu durum değildir.

## <a name="testing-the-title-search-feature"></a>Başlık arama özelliğini test etme

Artık tamamlanan arama sayfanızı test edebilirsiniz. *Filmleri. cshtml*'yi çalıştırın.

Bir tarz girin ve **Ara türe**tıklayın. Kılavuz, daha önce olduğu gibi bu tarzın filmlerini görüntüler.

Bir başlık sözcüğü girin ve **başlık ara**' yı tıklatın. Kılavuz, başlığında bu sözcüğe sahip olan filmleri görüntüler.

![Başlıkta ' The ' aranırken filmlere sayfa listeleme](form-basics/_static/image6.png)

Her iki metin kutusunu da boş bırakın ve düğmeye tıklayın. Kılavuzda tüm filmler görüntülenir.

## <a name="combining-the-queries"></a>Sorguları birleştirme

Gerçekleştirebileceğiniz aramaların dışlamalı olduğunu fark edebilirsiniz. Her iki arama kutusunda de değerler olsa bile başlık ve tarzda aynı anda arama yapamazsınız. Örneğin, başlığı "Adventure" içeren tüm eylem filmlerini araymıyorsunuz. (Sayfa şu anda kodlandığında, hem tarz hem de başlık için değer girerseniz, başlık araması önceliklidir.) Koşulları birleştiren bir arama oluşturmak için, aşağıdaki gibi bir sözdizimi içeren bir SQL sorgusu oluşturmanız gerekir:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

Ve aşağıdaki gibi bir ifade kullanarak (kabaca konuşulur) sorguyu çalıştırmanız gerekir:

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Birçok permütasyon arama ölçütünden izin vermek için mantık oluşturma, görebileceğiniz gibi bir bit dahil olabilir. Bu nedenle, burada duracağız.

## <a name="coming-up-next"></a>Sonraki adımda

Sonraki öğreticide, kullanıcıların veritabanına film eklemesine izin vermek için form kullanan bir sayfa oluşturacaksınız.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Film sayfası listesinin tamamını listeleme (aramayla güncelleştirildi)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools sitesinde [SQL WHERE yan tümcesi](http://www.w3schools.com/sql/sql_where.asp)
- W3C sitesindeki [Yöntem tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makalesi

> [!div class="step-by-step"]
> [Önceki](displaying-data.md) 
>  [Sonraki](entering-data.md)
