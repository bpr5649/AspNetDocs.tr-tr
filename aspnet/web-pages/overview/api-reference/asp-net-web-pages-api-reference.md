---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Sayfaları (Razor) API Hızlı Başvuru | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu sayfa, Web Sayfalarını Jilet sözdizimi ile ASP.NET programlamak için en sık kullanılan nesnelerin, özelliklerin ve yöntemlerin kısa örneklerini içeren bir liste içerir.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676246"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web Sayfaları (Razor) API Hızlı Başvuru

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> Bu sayfa, Web Sayfalarını Jilet sözdizimi ile ASP.NET programlamak için en sık kullanılan nesnelerin, özelliklerin ve yöntemlerin kısa örneklerini içeren bir liste içerir.
> 
> "(v2)" ile işaretlenmiş açıklamalar ASP.NET Web Sayfaları sürüm 2'de tanıtıldı.
> 
> API başvuru belgeleri için, MSDN'deki [Web Sayfaları Başvuru Belgeleri ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) bakın.
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> 
> - ASP.NET Web Sayfaları (Razor) 3
>   
> 
> Bu öğretici ayrıca ASP.NET Web Sayfaları 2 ve ASP.NET Web Sayfaları 1.0 ile de çalışır (v2 işaretli özellikler hariç).

Bu sayfa aşağıdakiler için referans bilgileri içerir:

- [Sınıflar](#Classes)
- [Veri](#Data)
- [Yardımcıları](#Helpers)
- [Doğrulama](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Sınıflar

### `AppState[key], AppState[index],App`

Uygulamadaki herhangi bir sayfa tarafından paylaşılabilen verileri içerir. Aşağıdaki örnekte `App` olduğu gibi, aynı verilere erişmek için dinamik özelliği kullanabilirsiniz:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Dize değerini Boolean değerine (true/false) dönüştürür. Dize doğru/yanlışı temsil etmiyorsa false veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Dize değerini tarihe/saate dönüştürür. Dize bir tarihi/saati temsil etmiyorsa, verir `DateTime.MinValue` veya belirtilen değeri verir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Dize değerini ondalık değere dönüştürür. Dize ondalık değeri temsil etmiyorsa 0,0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Dize değerini float'a dönüştürür. Dize ondalık değeri temsil etmiyorsa 0,0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Dize değerini bir tamsayıya dönüştürür. Dize bir karşıcıyı temsil etmiyorsa 0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

İsteğe bağlı ek yol parçalarıyla yerel bir dosya yolundan tarayıcı uyumlu bir URL oluşturur.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

*Değeri* HTML kodlanmış çıktı olarak işlemek yerine HTML biçimlendirmesi olarak işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Değer bir dizeden belirtilen türe dönüştürülebiliyorsa doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Nesne veya değişkenin değeri yoksa doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

İstek bir POST ise doğru döndürür. (İlk istekler genellikle GET'dir.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Bu sayfaya uygulanacak bir düzen sayfasının yolunu belirtir.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Geçerli istekteki sayfa, düzen sayfaları ve kısmi sayfalar arasında paylaşılan verileri içerir. Aşağıdaki örnekte `Page` olduğu gibi, aynı verilere erişmek için dinamik özelliği kullanabilirsiniz:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Düzen sayfaları) Herhangi bir adlandırılmış bölümde olmayan bir içerik sayfasının içeriğini işler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Belirtilen yolu ve isteğe bağlı ek verileri kullanarak bir içerik sayfasını işler. Ekstra parametrelerin değerlerini konuma göre `PageData` (örnek 1) veya anahtardan (örnek 2) alabilirsiniz.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Düzen sayfaları) Adı olan bir içerik bölümü işler. Bir bölümü isteğe bağlı hale getirmek için yanlış olması *için gerekli* ayarlayın.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Bir HTTP çerezinin değerini alır veya ayarlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Geçerli istekte yüklenen dosyaları alır.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Bir formda (dizeleri olarak) deftere nakledilen verileri alır. `Request[key]`hem koleksiyonları `Request.Form` hem `Request.QueryString` de koleksiyonları denetler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL sorgu dizesinde belirtilen verileri alır. `Request[key]`hem koleksiyonları `Request.Form` hem `Request.QueryString` de koleksiyonları denetler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Bir form öğesi, sorgu dize değeri, çerez veya üstbilgi değeri için istek doğrulamayı seçici olarak devre dışı kılabilir. İstek doğrulaması varsayılan olarak etkinleştirilir ve kullanıcıların biçimlendirme veya diğer tehlikeli olabilecek içerikleri deftere nakletmesini engeller.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Yanıta bir HTTP sunucu üstbilgisi ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Sayfa çıktısını belirli bir süre için önbelleğe alır. İsteğe bağlı olarak her sayfa erişiminde zaman alabildiği zaman asımı sıfırlamak için *kaydırMa* ayarlayın ve sayfa isteğindeki her farklı sorgu dizesi için sayfanın farklı sürümlerini önbelleğe almak için *ByParams'ı değiştirin.*

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Tarayıcı isteğini yeni bir konuma yönlendirir.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Tarayıcıya gönderilen HTTP durum kodunu ayarlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

*Verilerin* içeriğini isteğe bağlı MIME türüyle yanıta yazar.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Yanıta bir dosyanın içeriğini yazar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Düzen sayfaları) Adı olan bir içerik bölümü tanımlar.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML kodlanmış bir dize çözme.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML biçimlendirmesinde işleme için bir dize kodlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Belirtilen sanal yol için sunucu fiziksel yolunu döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL'deki metni deşifre eder.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

URL'ye koymak için metni kodlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Kullanıcı tarayıcıyı kapatana kadar var olan bir değeri alır veya ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Nesnenin değerinin dize gösterimini görüntüler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL'den ek veri alır (örneğin, */MyPage/ExtraData).*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Belirtilen kullanıcının parolasını değiştirir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Hesap onay belirteci kullanarak bir hesabı onaylar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Belirtilen kullanıcı adı ve parolaile yeni bir kullanıcı hesabı oluşturur. Bir onay belirteci gerektirmek için, *gerekliConfirmationToken* için doğru geçmek.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Şu anda oturum açmış kullanıcıiçin sonda tanımlayıcısını alır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Şu anda oturum açmış olan kullanıcının adını alır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Kullanıcının parolayı sıfırlayabilmesi için kullanıcıya e-posta yla gönderilebilen parola sıfırlama belirteci oluşturur.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Kullanıcı adından kullanıcı kimliğini verir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Geçerli kullanıcı oturum açmışsa doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Kullanıcı onaylandıysa (örneğin, bir onay e-postası aracılığıyla) doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Geçerli kullanıcının adı belirtilen kullanıcı adıyla eşleşiyorsa doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Çerezde kimlik doğrulama belirteci ayarlayarak kullanıcıyı oturum açar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Kimlik doğrulama belirteci çerezini kaldırarak kullanıcıyı dışarı kaydeder.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Kullanıcı nın kimliği doğrulanmazsa, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Geçerli kullanıcı belirtilen rollerden birinin üyesi değilse, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Geçerli kullanıcı *kullanıcı adı*ile belirtilen kullanıcı değilse, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Parola sıfırlama belirteci geçerliyse, kullanıcının parolasını yeni parolayla değiştirir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Veriler

### `Database.Execute(SQLstatement [,parameters]`

INSERT, DELETE veya UPDATE gibi *SQLstatement* 'ı (isteğe bağlı parametrelerle) yürütür ve etkilenen kayıtların sayısını döndürür.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

En son eklenen satırdaki kimlik sütununa döndürür.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Belirtilen veritabanı dosyasını veya *Web.config* dosyasından adlandırılmış bir bağlantı dizesini kullanarak belirtilen veritabanını açar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Bağlantı dizesini kullanarak bir veritabanı açar. `Database.Open`(Bu, bağlantı dizesi adı kullanan ile tezat.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement* kullanarak veritabanını sorgular (isteğe bağlı parametreleri geçen) ve sonuçları bir koleksiyon olarak döndürür.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

*SQLdeyimi* (isteğe bağlı parametrelerle) yürütür ve tek bir kayıt döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

*SQLdeyimi* (isteğe bağlı parametrelerle) yürütür ve tek bir değer döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Yardımcıları

### `Analytics.GetGoogleHtml(webPropertyId)`

Belirtilen kimlik için Google Analytics JavaScript kodunu işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Belirtilen proje için StatCounter Analytics JavaScript kodunu işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Belirtilen hesap için Yahoo Analytics JavaScript kodunu işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Aramayı Bing'e aktarın. Aranacak siteyi ve arama kutusunun başlığını belirtmek için, bu siteyi `Bing.SiteUrl` ve `Bing.SiteTitle` özelliklerini ayarlayabilirsiniz. Normalde bu özellikleri * \_AppStart* sayfasında ayarlarsınız.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Bir grafiği n için başharfe ait hale.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Grafiğe bir gösterge ekler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Grafiğe bir dizi değer ekler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Belirtilen veriler için karma döndürür. Varsayılan algoritma `sha256`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebook kullanıcılarının sayfalara bağlantı kurmasını sağlar.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Dosya yüklemek için Genel BirA'yı işler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Belirtilen Xbox oyuncu etiketini işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Belirtilen e-posta adresi için Gravatar görüntüsünü işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Bir veri nesnesini JavaScript Nesne Gösterimi (JSON) biçiminde bir dize dönüştürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON kodlu giriş dizesini, üzerinde kopyalayabildiğiniz veya veritabanına ekleyebildiğiniz bir veri nesnesine dönüştürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Belirtilen başlığı ve isteğe bağlı URL'yi kullanarak sosyal ağ bağlantılarını işler.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Hata iletisi form alanıyla ilişkilendirin. Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Hata iletisi ile form ilişkilendirir. Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Doğrulama hatası yoksa doğru döndürür. Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Bir nesnenin ve alt nesnelerin özelliklerini ve değerlerini işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

ReCAPTCHA doğrulama testini işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

ReCAPTCHA hizmeti için ortak ve özel anahtarları ayarlar. Normalde bu özellikleri * \_AppStart* sayfasında ayarlarsınız.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

ReCAPTCHA testinin sonucunu verir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

ASP.NET Web Sayfaları hakkındaki durum bilgilerini işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Belirtilen kullanıcı için bir Twitter akışı işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Belirtilen arama metni için bir Twitter akışı işler.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Belirtilen dosya için isteğe bağlı genişlik ve yüksekliğe sahip bir Flash video oynatıcı işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Belirtilen dosya için isteğe bağlı genişlik ve yüksekliğe sahip bir Windows Media oynatıcısı işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Belirtilen *.xap* dosyası için gerekli genişlik ve yüksekliğe sahip bir Silverlight oynatıcı sıcağa sahiptir.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

*Anahtarla*belirtilen nesneyi döndürür veya nesne bulunmazsa null' u verir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

*Anahtarla* belirtilen nesneyi önbellekten kaldırır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

*Anahtarla*belirtilen ad altında önbelleğe *değer* koyar.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Sorgudaki verileri `WebGrid` kullanarak yeni bir nesne oluşturur.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Verileri HTML tablosunda görüntülemek için biçimlendirme yi işler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Nesne için bir çağrı `WebGrid` cihazı işler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Görüntüyü belirtilen yoldan yükler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Belirtilen görüntüyü filigran olarak ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Belirtilen metni resme ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Görüntüyü yatay veya dikey olarak çevirir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Dosya yüklemesi sırasında bir sayfaya görüntü gönderildiğinde görüntü yükler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Görüntüyü yeniden boyutlandırıyor.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Görüntüyü sola veya sağa döndürür.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Görüntüyü belirtilen yola kaydeder.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP sunucusunun parolasını ayarlar. Normalde bu özelliği * \_AppStart* sayfasında ayarlarsınız.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Bir e-posta iletisi gönderir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP sunucu adını ayarlar. Normalde bu özelliği * \_AppStart* sayfasında ayarlarsınız.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP sunucusunun kullanıcı adını ayarlar. Normalde bu özelliği * \_AppStart* sayfasında ayarlamanız gerekir.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Doğrulama

### `Html.ValidationMessage(field)`

(v2) Belirtilen alan için bir doğrulama hatası iletisi işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) Tüm doğrulama hatalarının listesini görüntüler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) Belirtilen doğrulama türü için bir kullanıcı giriş öğesi kaydeder.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) Doğrulama hata iletilerini biçimlendirebilmeniz için istemci tarafı doğrulaması için CSS sınıf özniteliklerini dinamik olarak işler. (Uygun istemci komut dosyası kitaplıklarına başvurmanızı ve CSS sınıflarını tanımlamanızı gerektirir.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) Kullanıcı giriş alanı için istemci tarafı doğrulamasını sağlar. (Uygun istemci komut dosyası kitaplıkları başvuru gerektirir.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) Doğrulama için kayıt yaptırılan tüm kullanıcı giriş öğeleri geçerli değerler içeriyorsa doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) Kullanıcıların kullanıcı giriş öğesi için bir değer sağlaması gerektiğini belirtir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) Kullanıcıların her kullanıcı giriş öğesi için değerler sağlaması gerektiğini belirtir. Bu yöntem, özel bir hata iletisi belirtmenize izin vermez.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

(v2) `Validation.Add` Yöntemi kullandığınızda bir doğrulama testi belirtir.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
