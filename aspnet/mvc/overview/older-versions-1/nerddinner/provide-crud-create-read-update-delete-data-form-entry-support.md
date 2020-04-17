---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (Oluşturma, Oku, Güncelleme, Silme) Veri Formu Giriş Desteği Sağlayın | Microsoft Dokümanlar
author: rick-anderson
description: Adım 5, Dinners'ı düzenleme, oluşturma ve silme desteği sağlayarak DinnersController sınıfımızı nasıl daha ileriye götüreceğimizi gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542631"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD (Oluşturma, Okuma, Güncelleştirme, Silme) Veri Formu Giriş Desteği Sağlama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 5 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 5, Dinners'ı düzenleme, oluşturma ve silme desteği sağlayarak DinnersController sınıfımızı nasıl daha ileriye götüreceğimizi gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner Adım 5: Form Senaryoları Oluşturma, Güncelleme, Silme

Denetleyicileri ve görünümleri tanıttık ve bunları akşam yemekleri için sitede bir listeleme/ayrıntı deneyimi uygulamak için nasıl kullanacağımızı ele aldık. Bir sonraki adımımız DinnersController sınıfımızı daha da ileri götürmek ve akşam yemeklerini düzenleme, oluşturma ve silme desteği sağlamak olacaktır.

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController tarafından işlenen URL'ler

Daha önce DinnersController'a iki URL için destek uygulayan eylem yöntemleri ekledik: */Dinners* and */Dinners/Details/[id]*.

| **URL** | **Fiil** | **Amaç** |
| --- | --- | --- |
| */Akşam Yemekleri/* | GET | Yaklaşan akşam yemeklerinin HTML listesini görüntüleyin. |
| */Akşam Yemekleri/Ayrıntılar/[id]* | GET | Belirli bir akşam yemeği yle ilgili ayrıntıları görüntüleyin. |

Şimdi üç ek URL uygulamak için eylem yöntemleri ekleyeceğiz: */Dinners/Edit/[id]*, */Dinners/Create*, ve */Dinners/Delete/[id]*. Bu URL'ler, mevcut Akşam Yemekleri'nin düzenlenmesi, yeni Akşam Yemekleri nin oluşturulması ve Akşam Yemeklerinin silmesi için destek sağlayacaktır.

Bu yeni URL'lerle hem HTTP GET hem de HTTP POST fiil etkileşimlerini destekleyeceğiz. Bu URL'lere http GET istekleri verilerin ilk HTML görünümünü görüntüler ("düzenle", "oluştur" durumunda boş bir form ve "silme" durumunda silme onay ekranı durumunda Akşam Yemeği verileriyle doldurulan bir form). Bu URL'lere http POST istekleri DinnerRepository (ve oradan veritabanına) Akşam Yemeği verilerini kaydeder/günceller/siler.

| **URL** | **Fiil** | **Amaç** |
| --- | --- | --- |
| */Akşam Yemekleri/Edit/[id]* | GET | Akşam Yemeği verileriyle doldurulan bir editable HTML formu görüntüleyin. |
| POST | Form değişikliklerini belirli bir Akşam Yemeği için veritabanına kaydedin. |
| */Akşam Yemekleri/Oluştur* | GET | Kullanıcıların yeni Akşam Yemekleri tanımlamasına olanak tanıyan boş bir HTML formu görüntüleyin. |
| POST | Yeni bir Akşam Yemeği oluşturun ve veritabanına kaydedin. |
| */Akşam Yemekleri/Sil/[id]* | GET | Silme onay ekranını görüntüleyin. |
| POST | Belirtilen akşam yemeğini veritabanından siler. |

### <a name="edit-support"></a>Desteği Edit

"Düzenleme" senaryosunu uygulayarak başlayalım.

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET Edit Eylem Yöntemi

Düzenleme eylem yöntemimizin HTTP "GET" davranışını uygulayarak başlayacağız. */Dinners/Edit/[id]* URL'si istendiğinde bu yöntem çağrılacaktır. Uygulamamız şu şekilde görünecektir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

Yukarıdaki kod, Dinner nesnesini almak için DinnerRepository'yi kullanır. Daha sonra Akşam Yemeği nesnesini kullanarak bir Görünüm şablonu işler. Bir şablon adını *Görünüm()* yardımcı yöntemine açıkça geçirmediğimiz için, görünüm şablonu: /Views/Dinners/Edit.aspx'i çözmek için kuraltabanlı varsayılan yolu kullanır.

Şimdi bu görünüm şablonu oluşturalım. Bunu, Düzenleme yöntemi içinde sağ tıklayarak ve "Görünüm Ekle" bağlam ı menüsü komutunu seçerek yapacağız:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"Görünüm Ekle" iletişim kutusunda, bir Akşam Yemeği nesnesini modeli olarak görünüm şablonumuza aktardığımızı belirteceğiz ve bir "Edit" şablonunu otomatik olarak oluşturmayı seçeceğiz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizinine bizim için yeni bir "Edit.aspx" görünüm şablon dosyası ekleyecektir. Ayrıca kod düzenleyicisi içinde yeni "Edit.aspx" görünüm şablonu açılacaktır – aşağıdaki gibi bir ilk "Edit" iskele uygulaması ile doldurulur:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Oluşturulan varsayılan "edit" iskelesi için birkaç değişiklik yapalım ve aşağıdaki içeriğe sahip olacak şekilde görünüm edin şablonuna güncelleştirelim (bu da ortaya çıkarmak istemediğimiz özelliklerden birkaçını kaldırır):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Uygulamayı çalıştırdığımızda ve *"/Dinners/Edit/1"* URL'sini istediğimizde aşağıdaki sayfayı görürsünüz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

Bizim görünümümüzde oluşturulan HTML biçimlendirmesi aşağıdaki gibi görünür. Standart HTML'dir – &lt;&gt; "Kaydet" giriş türü="gönder" &lt;düğmesine&gt; basıldığında */Dinners/Edit/1* URL'sine HTTP POST gerçekleştiren bir form öğesi ile. Her &lt;bir editable özellik&gt; için bir HTML giriş türü="text"/ öğesi çıktı olmuştur:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() ve Html.TextBox() Html Yardımcı Yöntemleri

"Edit.aspx" görünüm şablonumuz birkaç "Html Helper" yöntemini kullanıyor: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox() ve Html.ValidationMessage(). Bu yardımcı yöntemleri, bizim için HTML biçimlendirmesi oluşturmanın yanı sıra yerleşik hata işleme ve doğrulama desteği sağlar.

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() yardımcı yöntemi

Html.BeginForm() yardımcı yöntemi, biçimlendirmemizdeki HTML &lt;form&gt; öğesinin çıktısi. Edit.aspx görünüm şablonumuzda bu yöntemi kullanırken C# "using" deyimi uyguladığımızı fark edeceksiniz. Açık kıvırcık ayraç form &lt;&gt; içeriğinin başlangıcını gösterir ve kapanış kıvırcık &lt;ayracı /form&gt; öğesinin sonunu gösterir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Alternatif olarak, böyle bir senaryo için "kullanma" deyimi yaklaşımını doğal bulmazsanız, html.BeginForm() ve Html.EndForm() kombinasyonunu (aynı şeyi yapan) kullanabilirsiniz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Html.BeginForm() 'yi herhangi bir parametre olmadan aramak, geçerli isteğin URL'sine HTTP-POST yapan bir form öğesi nin çıkışına neden olur. Bu nedenle Edit görünümümüz bir * &lt;form eylemi="/Dinners/Edit/1" method="post"&gt; * öğesi oluşturur. Farklı bir URL'ye göndermek isteseydik, açık parametreleri alternatif olarak Html.BeginForm'a() aktarabilirdik.

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() yardımcı yöntemi

Edit.aspx görünümü, giriş türü="text"/ &lt;&gt; öğeleri ni zedeleklemek için Html.TextBox() yardımcı yöntemini kullanır:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

Yukarıdaki Html.TextBox() yöntemi tek bir parametre alır – giriş türü="metin"/ &lt;&gt; öğenin hem kimlik/ad özniteliklerini hem de textbox değerini doldurmak için model özelliğini belirtmek için kullanılır. Örneğin, Edit görünümüne aktardığımız Akşam Yemeği nesnesinin ".NET Futures" özelliğinin "Başlık" özellik değeri vardı ve bu nedenle Html.TextBox("Başlık") metod çağrı çıktısı: * &lt;giriş id="Başlık" adı="Başlık" type="text" value=".NET Futures" /&gt;*.

Alternatif olarak, öğenin kimliğini/adını belirtmek için ilk Html.TextBox() parametresini kullanabilir ve ikinci bir parametre olarak kullanmak üzere değeri açıkça geçirebiliriz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Genellikle çıktı değeri üzerinde özel biçimlendirme gerçekleştirmek isteriz. String.Format() statik yöntemi yerleşik .NET bu senaryolar için yararlıdır. Edit.aspx görünüm şablonumuz, olay tarihi değerini (DateTime türünden) biçimlendirmek için bunu kullanır, böylece saniyeleri zamanında göstermez:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html.TextBox() için üçüncü bir parametre isteğe bağlı olarak ek HTML öznitelikleri çıktısı için kullanılabilir. Aşağıdaki kod-snippet, giriş türü="text"/ &lt;&gt; öğesi üzerinde ek bir boyut="30" özniteliği ve bir sınıf="mycssclass" özniteliğinin nasıl işlendiğini gösterir. "Sınıf"@" character because "kullanarak sınıf özniteliğinin adından nasıl kaçtığımızı not edin C#'da ayrılmış bir anahtar kelime:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP-POST Edit Eylem Yönteminin Uygulanması

Şimdi, Edit eylem yöntemimizin HTTP-GET sürümüne sahibiz. Bir kullanıcı */Dinners/Edit/1* URL'sini istediğinde aşağıdaki gibi bir HTML sayfası alır:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"Kaydet" düğmesine basıldığında */Dinners/Edit/1* URL'sine bir form &lt;gönderisi neden olur ve HTTP POST fiilini kullanarak HTML giriş&gt; formu değerlerini gönderir. Şimdi bizim edit eylem yöntemihttp POST davranışı uygulayalım - hangi Akşam yemeği kaydetme ele alacak.

DinnersController'ımıza, http POST senaryolarını işlediğini gösteren "AcceptVerbs" özelliği olan aşırı yüklü bir "Edit" eylem yöntemi ekleyerek başlayacağız:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

[AcceptVerbs] özniteliği aşırı yüklenen eylem yöntemlerine uygulandığında, ASP.NET MVC gelen HTTP fiiline bağlı olarak istekleri ni uygun eylem yöntemine otomatik olarak işleme eder. HTTP POST istekleri */Dinners/Edit/[id]* URL'leri yukarıdaki Edit yöntemine giderken, diğer tüm HTTP fiil istekleri */Dinners/Edit/[id]* URL'leri uyguladığımız ilk `[AcceptVerbs]` Edit yöntemine (özniteliği olmayan) gider.

| **Yan Konu: Neden HTTP fiiller aracılığıyla ayırt?** |
| --- |
| Sorabilirsiniz - neden tek bir URL kullanıyoruz ve http fiili ile davranışını farklılatıyoruz? Neden yükleme ve tasarruf değişiklikleri işlemek için sadece iki ayrı URL'si yok? Örneğin: /Dinners/Edit/[id] ilk formu görüntülemek ve /Dinners/Save/[id] formu kaydetmek için formu işlemek için? İki ayrı URL yayımlamanın dezavantajı, /Dinners/Save/2 adresine gönderdiğimiz ve daha sonra bir giriş hatası nedeniyle HTML formunu yeniden görüntülememiz gereken durumlarda, son kullanıcının tarayıcılarının adres çubuğunda /Dinners/Save/2 URL'sine sahip olmasıdır (çünkü formun gönderdiği URL'dir). Son kullanıcı yeniden görüntülenen bu sayfayı tarayıcı sık kullanılanlar listesine yer imleri gösterirse veya URL'yi kopyalayıp yapıştırırve bir arkadaşınıza e-postalarsa, gelecekte çalışmayan bir URL kaydederler (bu URL gönderi değerlerine bağlı olduğundan). Tek bir URL (örneğin: /Dinners/Edit/[id]) ortaya çıkararak ve bunun işlenmesini HTTP fiili ile ayırt ederek, son kullanıcıların düzenleme sayfasını yer imi ne kadar güvenli hale getirmek ve/veya URL'yi başkalarına göndermek güvenlidir. |

#### <a name="retrieving-form-post-values"></a>Form Sonrası Değerleri Alma

HTTP POST "Edit" yöntemimiz içinde gönderilen form parametrelerine erişmenin çeşitli yolları vardır. Basit bir yaklaşım, form koleksiyonuna erişmek ve deftere nakledilen değerleri doğrudan almak için Denetleyici taban sınıfındaki İstek özelliğini kullanmaktır:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

Yukarıdaki yaklaşım biraz ayrıntılı olsa da, özellikle bir kez hata işleme mantığı ekleyin.

Bu senaryo için daha iyi bir yaklaşım, Denetleyici taban sınıfında yerleşik *UpdateModel()* yardımcı yönteminden yararlanmaktır. Gelen form parametrelerini kullanarak aktardığımız bir nesnenin özelliklerini güncelleştirmeyi destekler. Nesnedeki özellik adlarını belirlemek için yansımayı kullanır ve ardından istemci tarafından gönderilen giriş değerlerini temel alarak değerleri otomatik olarak dönüştürür ve bunlara atar.

Bu kodu kullanarak HTTP-POST Düzenleme Eylemimizi basitleştirmek için UpdateModel() yöntemini kullanabiliriz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Artık */Dinners/Edit/1* URL'sini ziyaret edebilir ve Akşam Yemeğimizin başlığını değiştirebiliriz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"Kaydet" düğmesini tıklattığımızda, Edit eylemimizde bir form gönderisi gerçekleştireceğiz ve güncelleştirilmiş değerler veritabanında kalıcı hale gelecektir. Daha sonra Akşam Yemeği için Ayrıntılar URL'sine yönlendiriliriz (yeni kaydedilen değerleri görüntüler):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Düzeltme Hatalarını İşleme

Mevcut HTTP-POST uygulamamız iyi çalışır – hatalar olmadığı durumlar dışında.

Bir kullanıcı bir formu düzenleyerek hata yaptığında, formun düzeltmeleri için onlara yol gösteren bilgilendirici bir hata iletisiyle yeniden görüntülendiğinden emin olmamız gerekir. Buna, son kullanıcının yanlış giriş (örneğin: biçimsiz tarih dizesi) gönderdiği durumlar ve giriş biçiminin geçerli olduğu ancak iş kuralı ihlali olduğu durumlar dahildir. Hatalar oluştuğunda, form, kullanıcının ilk olarak girdiği giriş verilerini korumalıdır, böylece değişikliklerini el ile doldurmak zorunda kalmamalıdır. Bu işlem, form başarıyla tamamlanana kadar gerektiği kadar tekrarlanmalıdır.

ASP.NET MVC hata işleme ve form yeniden görüntüleme kolay yapmak bazı güzel yerleşik özellikler içerir. Bu özellikleri iş başında görmek için Eylem Edit yöntemimizi aşağıdaki kodla güncelleyelim:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

Yukarıdaki kod önceki uygulamamıza benzer – ancak artık çalışmalarımızın etrafında bir try/catch hata işleme bloğunu sarıyoruz. UpdateModel() () çağrısında bulunurken veya DinnerRepository'yi kaydetmeye çalıştığımızda (kaydetmeye çalıştığımız Akşam Yemeği nesnesi modelimizdeki bir kural ihlali nedeniyle geçersiz sayıldıysa) bir özel durum oluşursa, yakalama hatası işleme bloğumuz yürütülür. İçinde, Akşam Yemeği nesnesinde bulunan kural ihlallerinin üzerinden döngü ve bunları bir ModelState nesnesine ekliyoruz (kısa bir süre içinde tartışacağız). Daha sonra görünümü yeniden görüntüleriz.

Bu çalışmayı görmek için uygulamayı yeniden çalıştıralım, akşam yemeğini düzenledirelim ve boş bir Başlık, "BOGUS" Etkinlik Tarihi olacak şekilde değiştirelim ve ABD ülke değerine sahip bir Birleşik Krallık telefon numarası kullanın. "Kaydet" düğmesine bastığımızda HTTP POST Edit yöntemimiz Akşam Yemeği'ni kaydedemeyecek (çünkü hatalar var) ve formu yeniden görüntülenecektir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Uygulamamız iyi bir hata deneyimine sahiptir. Geçersiz girişi olan metin öğeleri kırmızı yla vurgulanır ve doğrulama hatası iletileri son kullanıcıya bunlar hakkında görüntülenir. Form ayrıca, kullanıcının başlangıçta girdiği giriş verilerini de korur, böylece hiçbir şeyi yeniden doldurmak zorunda kalmaz.

Bu nasıl oldu diye sorabilirsiniz. Başlık, EventDate ve ContactPhone textbox'lar kendilerini kırmızı yla nasıl vurgulamıştır ve başlangıçta girilen kullanıcı değerlerini çıktıolarak nasıl bilir? Peki hata iletileri en üstteki listede nasıl görüntülendi? İyi haber, bu sihirli tarafından meydana gelmedi - bunun yerine bazı giriş doğrulama ve hata işleme senaryoları kolaylaştırmak yerleşik ASP.NET MVC özellikleri nin kullanılan çünkü.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelDurumunu ve Doğrulama HTML Yardımcı Yöntemlerini Anlama

Denetleyici sınıfları, Görünüm'e geçirilen bir model nesnesi ile hataların var olduğunu gösteren bir yol sağlayan bir "ModelState" özellik koleksiyonuna sahiptir. ModelState koleksiyonundaki hata girişleri, model özelliğinin adını sorunla birlikte tanımlar (örneğin: "Başlık", "EventDate" veya "ContactPhone") ve insan dostu bir hata iletisinin belirtilmesine izin verir (örneğin: "Başlık gereklidir").

*UpdateModel()* yardımcı yöntemi, model nesnesindeki özelliklere form değerleri atamaya çalışırken hatalarla karşılaştığında ModelState koleksiyonunu otomatik olarak doldurar. Örneğin, Akşam Yemeği nesnemizin EventDate özelliği DateTime türündendir. UpdateModel() yöntemi yukarıdaki senaryoda "BOGUS" dize değerini atayamayınca, UpdateModel() yöntemi ModelState koleksiyonuna bu özellikte bir atama hatası oluştuğunu belirten bir giriş ekledi.

Geliştiriciler ayrıca, ModelState koleksiyonuna, Akşam Yemeği nesnesindeki etkin Kural İhlallerine dayalı girişlerle modelstate koleksiyonunu dolduran "catch" hata işleme bloğumuzda yaptığımız gibi açıkça hata girişleri eklemek için kod yazabilirler:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>ModelState ile Html Yardımcı Tümleştirmesi

HTML yardımcı yöntemleri - Html.TextBox() gibi - çıktıyı işlerken ModelState koleksiyonunu kontrol edin. Öğe için bir hata varsa, kullanıcı girilen değeri ve CSS hata sınıfını işlerler.

Örneğin, "Edit" görünümümüzde, Akşam Yemeği nesnemizin Olay Tarihini işlemek için Html.TextBox() yardımcı yöntemini kullanıyoruz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Görünüm hata senaryosunda işlendiğinde, Html.TextBox() yöntemi, Akşam Yemeği nesnemizin "EventDate" özelliğiyle ilişkili herhangi bir hata olup olmadığını görmek için ModelState koleksiyonunu işaretledi. Bir hata olduğunu belirlediğinde gönderilen kullanıcı girdisini ("BOGUS") değer olarak işledi ve oluşturduğu giriş &lt;türüne css hata&gt; sınıfı ekledi="textbox"/ biçimlendirme:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

CSS hata sınıfının görünümünü istediğiniz şekilde bakmak için özelleştirebilirsiniz. Varsayılan CSS hata sınıfı – "giriş-doğrulama-hata" – *\content\site.css* stylesheet'te tanımlanır ve aşağıdaki gibi görünür:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Bu CSS kuralı, geçersiz giriş öğelerimizin aşağıdaki gibi vurgulanmasına neden olan şeydir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() Yardımcı Yöntemi

Html.ValidationMessage() yardımcı yöntemi, belirli bir model özelliğiyle ilişkili ModelState hata iletisini çıktılamak için kullanılabilir:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

Yukarıdaki kod çıktıları: * &lt;span class="alan&gt; doğrulama-hatası" 'BOGUS' değeri&lt;geçersiz /span&gt;*

Html.ValidationMessage() yardımcı yöntemi, geliştiricilerin görüntülenen hata metin iletisini geçersiz kılmasına olanak tanıyan ikinci bir parametreyi de destekler:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

Yukarıdaki kod çıkışları: EventDate özelliği için bir hata olduğunda varsayılan hata metni yerine * &lt;span&gt;\*&lt;class="alan doğrulama-hatası" /span.&gt; *

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() Yardımcı Yöntemi

Html.ValidationSummary() yardımcı yöntemi, ModelState koleksiyonundaki tüm ayrıntılı hata &lt;iletilerinin&gt;&lt;bir&gt; ul&gt;&lt;li/ /ul listesi eşliğinde bir özet hata iletisi işlemek için kullanılabilir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.ValidationSummary() yardımcı yöntemi isteğe bağlı bir dize parametresi alır – ayrıntılı hatalar listesinin üzerinde görüntülemek için bir özet hata iletisi tanımlar:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

Hata listesinin nasıl göründüğünü geçersiz kılmak için isteğe bağlı olarak CSS kullanabilirsiniz.

#### <a name="using-a-addruleviolations-helper-method"></a>AddRuleViolations Helper Yöntemini Kullanma

İlk HTTP-POST Düzenleme uygulamamız, Akşam Yemeği nesnesinin Kural İhlalleri üzerinde döngü ve denetleyicinin ModelState koleksiyonuna eklemek için catch bloğu içinde foreach deyimi ni kullandı:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Bu kodu, NerdDinner projesine bir "ControllerHelpers" sınıfı ekleyerek biraz daha temiz yapabilir ve içinde ASP.NET mvc modelStateDictionary sınıfına yardımcı bir yöntem ekleyen bir "AddRuleViolations" uzantı yöntemi uygulayabiliriz. Bu uzantı yöntemi, ModelStateDictionary'yi RuleViolation hatalarının bir listesiyle doldurmak için gereken mantığı özetleyebilir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Daha sonra, ModelState koleksiyonunu Akşam Yemeği Kuralı İhlallerimizle doldurmak için bu uzantı yöntemini kullanmak için HTTP-POST Düzenleme eylem yöntemimizi güncelleyebiliriz.

#### <a name="complete-edit-action-method-implementations"></a>Eylem Yöntemini Tamamla

Aşağıdaki kod, Edit senaryomuz için gerekli tüm denetleyici mantığını uygular:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

Düzenleme uygulamamız la ilgili güzel olan şey, ne Denetleyici sınıfımızın ne de Görünüm şablonumuz, Akşam Yemeği modelimiz tarafından uygulanan belirli doğrulama veya iş kuralları hakkında hiçbir şey bilmesi gerekmemektedir. Gelecekte modelimize ek kurallar ekleyebiliriz ve bunların desteklenmesi için denetleyicimizde veya görünümümüzde herhangi bir kod değişikliği yapmamız gerekmez. Bu, bize gelecekte en az kod değişikliğiyle uygulama gereksinimlerimizi kolayca geliştirme esnekliği sağlar.

### <a name="create-support"></a>Destek Oluştur

DinnersController sınıfımızın "Edit" davranışını uygulamayı bitirdik. Şimdi kullanıcıların yeni akşam yemekleri eklemesini sağlayacak olan "Oluştur" desteğini uygulamaya geçelim.

#### <a name="the-http-get-create-action-method"></a>HTTP-GET Oluşturma Eylem Yöntemi

Eylem oluşturma yöntemimizin HTTP "GET" davranışını uygulayarak başlayacağız. Birisi */Dinners/Create* URL'sini ziyaret ettiğinde bu yöntem çağrılacaktır. Uygulamamız şu şekilde görünür:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

Yukarıdaki kod yeni bir Akşam Yemeği nesnesi oluşturur ve EventDate özelliğini gelecekte bir hafta olarak atar. Daha sonra yeni Akşam Yemeği nesnesini temel alan bir Görünüm işler. *Görünüm()* yardımcı yöntemine açıkça bir ad geçirmediğimiz için, görünüm şablonu: /Views/Dinners/Create.aspx'i çözmek için kuraltabanlı varsayılan yolu kullanır.

Şimdi bu görünüm şablonu oluşturalım. Bunu, eylem oluştur yöntemi içinde sağ tıklayarak ve "Görünüm Ekle" bağlam ı menüsü komutunu seçerek yapabiliriz. "Görünüm Ekle" iletişim kutusunda, bir Akşam Yemeği nesnesini görünüm şablonuna aktardığımızı belirteceğiz ve otomatik olarak bir "Oluştur" şablonu oluşturmayı seçeceğiz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizinine yeni bir iskele tabanlı "Create.aspx" görünümünü kaydeder ve IDE içinde açar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Bizim için oluşturulan varsayılan "oluşturma" iskele dosyasında birkaç değişiklik yapalım ve aşağıdaki gibi görünecek şekilde değiştirelim:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

Ve şimdi uygulamamızı çalıştırdığımızda ve tarayıcıdaki *"/Dinners/Create"* URL'sine eriştiğımızda, eylem oluştur uygulamamızdan aşağıdaki gibi Kullanıcı Arabirimi'ni işletecektir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP-POST Oluşturma Eylem Yöntemini Uygulama

Eylem Oluştur yöntemimizin HTTP-GET sürümünü uyguladık. Bir kullanıcı "Kaydet" düğmesini tıklattığında */Dinners/Create* URL'sine bir form &lt;gönderisi gerçekleştirir ve HTTP POST fiilini kullanarak HTML giriş&gt; formu değerlerini gönderir.

Şimdi eylem yöntemimiz deki HTTP POST davranışını uygulayalım. DinnersController'ımıza, http POST senaryolarını işlediğini gösteren "AcceptVerbs" özelliği olan aşırı yüklü bir "Oluştur" eylem yöntemi ekleyerek başlayacağız:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP-POST etkin "Oluştur" yöntemimiz içinde gönderilen form parametrelerine erişmenin çeşitli yolları vardır.

Bir yaklaşım, yeni bir Akşam Yemeği nesnesi oluşturmak ve ardından *updatemodel()* yardımcı yöntemini (Edit eyleminde yaptığımız gibi) kullanarak onu gönderilen form değerleriyle doldurmaktır. Daha sonra DinnerRepository'mize ekleyebilir, veritabanında devam edebilir ve kullanıcıyı aşağıdaki kodu kullanarak yeni oluşturulan Akşam Yemeği'ni göstermek için Ayrıntılar eylemimize yönlendirebiliriz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternatif olarak, Create() eylem yöntemimizin bir Akşam Yemeği nesnesi nesnesi alma yöntemini yöntem parametresi olarak aldığı bir yaklaşım kullanabiliriz. ASP.NET MVC daha sonra otomatik olarak bizim için yeni bir Akşam Yemeği nesnesi anında, form girişlerini kullanarak özelliklerini doldurmak ve eylem yöntemine aktarmak:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Yukarıdaki eylem yöntemimiz, Dinner nesnesinin ModelState.IsValid özelliğini işaretleyerek form sonrası değerleriyle başarıyla dolduruldugUnu doğrular. Giriş dönüştürme sorunları varsa (örneğin: EventDate özelliği için "BOGUS" dizisi) ve eylem yöntemimiz formu yeniden görüntülerherhangi bir sorun varsa bu yanlış döndürecektir.

Giriş değerleri geçerliyse, eylem yöntemi yeni Akşam Yemeği'ni DinnerRepository'a eklemeye ve kaydetmeye çalışır. Bu çalışmayı bir try/catch bloğu içinde sarar ve herhangi bir iş kuralı ihlali varsa formu yeniden görüntüler (bu da bir istisna oluşturmak için dinnerRepository.Save() yöntemine neden olur).

Bu hata işleme davranışını iş başında görmek *için/Akşam Yemekleri/Url Oluştur'u* isteyebilir ve yeni bir Akşam Yemeği yle ilgili ayrıntıları doldurabiliriz. Yanlış giriş veya değerler, aşağıdaki gibi vurgulanan hatalarla oluşturma formunun yeniden görüntülenmesine neden olur:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Oluştur formuzun, Edit formumuzla aynı doğrulama ve iş kurallarını nasıl onurlandırdığını fark edin. Bunun nedeni, doğrulama ve iş kurallarımızın modelde tanımlanmış olması ve kullanıcı arabirimi veya uygulama denetleyicisine katıştırılmış olmamasıdır. Bu, daha sonra doğrulama veya iş kurallarımızı tek bir yerde değiştirebileceğimiz/geliştirebileceğimiz ve uygulamamız boyunca uygulanmasını sağlayabiliriz anlamına gelir. Mevcut kurallara veya değişikliklere otomatik olarak uymak için Edit veya Create eylem yöntemlerimiz içinde herhangi bir kodu değiştirmek zorunda kalmayız.

Giriş değerlerini düzeltip tekrar "Kaydet" düğmesine tıkladığımızda, DinnerRepository'ye eklememiz başarılı olacak ve veritabanına yeni bir Akşam Yemeği eklenecektir. Daha sonra */Dinners/Details/[id]* URL'sine yönlendirileceğiz – burada yeni oluşturulan Akşam Yemeği hakkında ayrıntılı bilgi verilecektir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Desteği Sil

Şimdi DinnersController'ımıza "Sil" desteği ekleyelim.

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET Silme Eylem Yöntemi

Silme eylem yöntemimizin HTTP GET davranışını uygulayarak başlayacağız. Birisi */Dinners/Delete/[id]* URL'sini ziyaret ettiğinde bu yöntem çağrılır. Aşağıda uygulama:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

Eylem yöntemi, Akşam Yemeği'ni silinmek üzere almaya çalışır. Akşam Yemeği varsa, Akşam Yemeği nesnesini temel alan bir Görünüm işler. Nesne yoksa (veya zaten silinmişse), "Ayrıntılar" eylem yöntemimiz için daha önce oluşturduğumuz "Bulunan Yok" görünüm şablonu oluşturan bir Görünüm döndürür.

"Sil" görünüm şablonunu, Delete eylem yöntemi içinde sağ tıklayarak ve "Görünüm Ekle" bağlam menüsü komutunu seçerek oluşturabiliriz. "Görünüm Ekle" iletişim kutusunda, bir Akşam Yemeği nesnesini modeli olarak görünüm şablonumuza aktardığımızı belirteceğiz ve boş bir şablon oluşturmayı seçeceğiz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"Ekle" düğmesini tıklattığımızda Visual Studio, "\Views\Dinners" dizini içinde bizim için yeni bir "Delete.aspx" görünüm şablon dosyası ekleyecektir. Aşağıdaki gibi bir silme onay ekranı uygulamak için şablona bazı HTML ve kod ekleyeceğiz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

Yukarıdaki kod, silinecek Akşam Yemeği'nin başlığını &lt;görüntüler&gt; ve son kullanıcı içindeki "Sil" düğmesini tıklatarsa /Dinners/Delete/[id] URL'sine GÖNDERI yapan bir form öğesi çıkar.

Uygulamamızı çalıştırdığımızda ve geçerli bir Akşam Yemeği nesnesi için *"/Dinners/Delete/[id]"* URL'sine eriştiğımızda aşağıdaki gibi Kullanıcı Arabirimi'ni işler:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Yan Konu: Neden bir POST yapıyoruz?** |
| --- |
| Sorabilirsiniz – neden Sil onay ekranımızda &lt;&gt; bir form oluşturma çabasından geçtik? Neden gerçek silme işlemini yapan bir eylem yöntemine bağlanmak için standart bir köprü kullanmıyoruz? Bunun nedeni, url'lerimizi keşfeden ve bağlantıları takip ettiklerinde yanlışlıkla verilerin silinmesine neden olan web tarayıcılarına ve arama motorlarına karşı dikkatli olmak istememizdir. HTTP-GET tabanlı URL'ler erişim /tarama için "güvenli" olarak kabul edilir ve http-POST olanları takip etmek gerekiyordu. İyi bir kural, http-POST isteklerinin arkasına her zaman yıkıcı veya veri değiştirme işlemleri koyduğunuzdan emin olmaktır. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP-POST Silme Eylem Yöntemini Uygulama

Şimdi bir silme onay ekranı görüntüler bizim Silme eylem yöntemi nin HTTP-GET sürümü vardır. Son kullanıcı "Sil" düğmesini tıklattığında */Dinners/Dinner/[id]* URL'sine bir form gönderisi gerçekleştirecektir.

Şimdi aşağıdaki kodu kullanarak silme eylem yönteminin HTTP "POST" davranışını uygulayalım:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Silme eylem yöntemimizin HTTP-POST sürümü, silmek için akşam yemeği nesnesini almaya çalışır. Bulamıyorsa (zaten silindiği için) "Bulundu Malandı" şablonumuzu işler. Akşam Yemeği'ni bulursa, DinnerRepository'den siler. Daha sonra bir "Silinmiş" şablonu işler.

"Silinen" şablonuna uygulamak için eylem yöntemine sağ tıklayıp "Görünüm Ekle" bağlam menüsünü seçeceğiz. Görünümümüze "Silinmiş" adını vereceğiz ve boş bir şablon olmasını sağlayacağız (ve güçlü bir şekilde yazılan bir model nesnesini almayalım). Daha sonra bazı HTML içeriği ekleyeceğiz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

Ve şimdi uygulamamızı çalıştırdığımızda ve geçerli bir Akşam Yemeği nesnesi için *"/Dinners/Delete/[id]"* URL'sine eriştiğımızda, aşağıdaki gibi Akşam Yemeği silme onay ekranımızı işleyecek:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"Sil" düğmesini *tıklattığımızda/Yemek/Sil/[id]* URL'sine bir HTTP-POST gerçekleştirecek ve bu url'yi veritabanımızdan silecek ve "Silinmiş" görünüm şablonumuzu görüntüleyecek:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Model Bağlama Güvenliği

mvc'nin yerleşik model bağlama özelliklerini kullanmanın iki farklı yolunu tartıştık ASP.NET. İlk güncelleştirme modeli() yöntemini kullanarak varolan bir model nesnesi üzerindeki özellikleri güncelleştirmek için, ikincisi ise ASP.NET MVC'nin model nesnelerini eylem yöntemi parametreleri olarak aktarmak için desteğini kullanır. Bu tekniklerin her ikisi de çok güçlü ve son derece yararlıdır.

Bu güç de beraberinde sorumluluk getirir. Herhangi bir kullanıcı girişi kabul ederken her zaman güvenlik hakkında paranoyak olmak önemlidir ve bu da nesneleri giriş oluşturmak için bağlama zaman da geçerlidir. HTML ve JavaScript enjeksiyon saldırılarından kaçınmak için kullanıcı tarafından girilen değerleri her zaman HTML kodlamaya ve SQL enjeksiyon saldırılarına dikkat etmelisiniz (not: Bu tür saldırıları önlemek için parametreleri otomatik olarak kodlayan uygulamamız için LINQ'u SQL'e kullanıyoruz). Yalnızca istemci tarafı doğrulamasına asla güvenmemelisiniz ve size sahte değerler göndermeye çalışan bilgisayar korsanlarına karşı korunmak için her zaman sunucu tarafı doğrulamasını kullanmamalısınız.

ASP.NET MVC'nin bağlama özelliklerini kullanırken düşündüğünüzden emin olmak için ek bir güvenlik öğesi, bağladiğiniz nesnelerin kapsamıdır. Özellikle, bağlanmasına izin verdiğiniz özelliklerin güvenlik etkilerini anladığınızdan emin olmak ve yalnızca son kullanıcı tarafından güncelleştirilebilen bu özelliklerin güncelleştirilebilmesine izin verdiğinden emin olmak istersiniz.

Varsayılan olarak, UpdateModel() yöntemi gelen form parametre değerleri eşleşen model nesnesi üzerindeki tüm özellikleri güncelleştirmeyi çalışır. Aynı şekilde, eylem yöntemi parametreleri olarak geçirilen nesneler de varsayılan olarak tüm özelliklerini form parametreleri üzerinden ayarlayabilir.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Kullanım başına bağlamayı kilitleme

Bağlaç ilkesini, güncelleştirilebilen özelliklerin açık bir "dahil listesi" sağlayarak kullanım başına kilitleyebilirsiniz. Bu, aşağıdaki gibi UpdateModel() yöntemine fazladan bir dize dizi parametresi geçirilerek yapılabilir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Eylem yöntemi parametreleri olarak geçirilen nesneler, izin verilen özelliklerin "dahil listesinin" aşağıda belirtildiği bir [Bağlayıcı] özniteliğini de destekler:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Tür bazında bağlamayı kilitleme

Bağlama kurallarını her türü için ayrı ayrı da kilitleyebilirsiniz. Bu, bağlama kurallarını bir kez belirtmenize ve tüm denetleyiciler ve eylem yöntemleri boyunca tüm senaryolarda (Hem UpdateModel hem de eylem yöntemi parametre senaryoları dahil) uygulanmasını sağlar.

Bir türe [Bind] özniteliği ekleyerek veya uygulamanın Global.asax dosyasına kaydederek (türe sahip olmadığınız senaryolar için yararlıdır) türü başına bağlama kurallarını özelleştirebilirsiniz. Daha sonra, belirli sınıf veya arabirim için hangi özelliklerin bağlanabilir olduğunu denetlemek için Bind özniteliğinin Ekle ve Hariç tutma özelliklerini kullanabilirsiniz.

Bu tekniği NerdDinner uygulamamızda Akşam Yemeği sınıfı için kullanacağız ve bağlanabilen özellikler listesini aşağıdakilerle sınırlayan bir [Bind] özniteliği ekleyeceğiz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

RsVP koleksiyonunun bağlayıcı lıkla manipüle edilmesine izin vermememiz ve DinnerID veya HostedBy özelliklerinin bağlama yoluyla ayarlanmasına izin vermediğimizi unutmayın. Güvenlik nedenleriyle, bunun yerine bu özel özellikleri yalnızca eylem yöntemlerimiz içinde açık kodu kullanarak manipüle edeceğiz.

### <a name="crud-wrap-up"></a>CRUD Sarma

ASP.NET MVC, form gönderme senaryolarının uygulanmasına yardımcı olan bir dizi yerleşik özellik içerir. DinnerRepository'mizin üzerine CRUD UI desteği sağlamak için bu özelliklerin çeşitlilerini kullandık.

Uygulamamızı uygulamak için model odaklı bir yaklaşım kullanıyoruz. Bu, tüm doğrulama ve iş kuralı mantığımızın, denetleyicilerimiz veya görünümlerimiz içinde değil, model katmanımızda tanımlandığı anlamına gelir. Ne Denetleyici sınıfımız ne de Görünüm şablonlarımız, Dinner model sınıfımız tarafından uygulanan belirli iş kuralları hakkında hiçbir şey bilmez.

Bu, uygulama mimarimizi temiz tutacak ve test etmeyi kolaylaştıracaktır. Gelecekte model katmanımıza ek iş kuralları ekleyebiliriz ve bunların desteklenmesi için Denetleyicimiz veya Görünümümüzde *herhangi bir kod değişikliği yapmak zorunda kalmamalıyız.* Bu bize gelecekte uygulamamızı geliştirmek ve değiştirmek için büyük bir çeviklik sağlayacaktır.

DinnersController artık Akşam Yemeği girişlerini/ayrıntılarını ve destek oluşturmalarını, düzenlemesini ve silmesini sağlar. Sınıfın tam kodunu aşağıda bulabilirsiniz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Sonraki Adım

Şimdi dinnersController sınıfımızda temel CRUD (Oluştur, Oku, Güncelle ve Sil) desteği ne var?

Şimdi formlarımızda daha da zengin uI sağlamak için ViewData ve ViewModel sınıflarını nasıl kullanabileceğimize bakalım.

> [!div class="step-by-step"]
> [Önceki](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [Sonraki](use-viewdata-and-implement-viewmodel-classes.md)
