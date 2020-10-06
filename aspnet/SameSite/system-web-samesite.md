---
title: ASP.NET içinde SameSite tanımlama bilgileriyle çalışma
author: rick-anderson
description: ASP.NET içindeki site tanımlama bilgilerini nasıl kullanacağınızı öğrenin
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 2a39663dcbfa97ae441edd9a9768172cafbaab03
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763462"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET içinde SameSite tanımlama bilgileriyle çalışma

Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite, siteler arası istek sahteciliği (CSRF) saldırılarına karşı bir koruma sağlamak için tasarlanmış bir [IETF](https://ietf.org/about/) taslak standardıdır. [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)içinde orijinal drafted, taslak standart [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)' de güncelleştirildi. Güncelleştirilmiş standart, önceki standartlarla geriye dönük olarak uyumlu değildir ve aşağıdakiler en belirgin farklılıklardır:

* SameSite üst bilgisi olmayan tanımlama bilgileri varsayılan olarak kabul edilir `SameSite=Lax` .
* `SameSite=None` siteler arası tanımlama bilgisi kullanımına izin vermek için kullanılmalıdır.
* Onaylama bilgilerinin `SameSite=None` de olarak işaretlenmesi gerekir `Secure` .
* Kullanan uygulamalar [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) `sameSite=Lax` `sameSite=Strict` `<iframe>` , siteler arası senaryolar olarak değerlendirildiğinden veya tanımlama bilgileriyle ilgili sorunlar yaşayabilir.
* Değerin `SameSite=None` [2016 standart](https://tools.ietf.org/html/draft-west-first-party-cookies-07) tarafından yapılmasına izin verilmez ve bazı uygulamaların bu tür tanımlama bilgilerini olarak ele alınmasına neden olur `SameSite=Strict` . Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

`SameSite=Lax`Ayar çoğu uygulama tanımlama bilgisi için geçerlidir. [OpenID Connect](https://openid.net/connect/) (OIDC) ve [WS-Federation](https://auth0.com/docs/protocols/ws-fed) gibi bazı kimlik doğrulama biçimlerinden bırı, temel yönlendirmeye gönderi sağlar. POST tabanlı yeniden yönlendirmeler, SameSite tarayıcı korumalarının tetiklenmesi, bu nedenle bu bileşenler için SameSite devre dışı bırakıldı. Çoğu [OAuth](https://oauth.net/) oturum açma, istek akışının farklılığı nedeniyle etkilenmez.

Tanımlama bilgilerini veren her ASP.NET bileşeni, SameSite ' ın uygun olup olmadığına karar vermeniz gerekir.

2019 .net SameSite güncelleştirmelerini yükledikten sonra uygulamalarla ilgili sorunların [bilinen sorunları](#known) bölümüne bakın.

## <a name="using-samesite-in-aspnet-472-and-48"></a>ASP.NET 4.7.2 ve 4,8 ' de SameSite kullanma

.NET 4.7.2 ve 4,8 Aralık 2019 ' de güncelleştirmelerin yayımlanmasından bu yana SameSite için [2019 taslak standardını](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) destekler. Geliştiriciler [HttpCookie. SameSite özelliğini](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)kullanarak SameSite üst bilgisinin değerini programlı bir şekilde denetleyebilir. `SameSite`Özelliği `Strict` , `Lax` , veya, `None` tanımlama bilgisi ile ağda yazılmakta olan değerleri, veya olarak ayarlama. Eşittir ayarı `(SameSiteMode)(-1)` , ağa tanımlama bilgisiyle hiçbir SameSite üstbilgisinin dahil edilip edilmediğini gösterir. [HttpCookie. Secure özelliği](/dotnet/api/system.web.httpcookie.secure)veya yapılandırma dosyalarındaki ' RequireSSL ', tanımlama bilgisini olarak işaretlemek için kullanılabilir `Secure` .

Yeni `HttpCookie` örnekler varsayılan olarak `SameSite=(SameSiteMode)(-1)` ve olur `Secure=false` . Bu varsayılanlar `system.web/httpCookies` yapılandırma bölümünde geçersiz kılınabilir, burada dize, `"Unspecified"` için yalnızca kolay bir yapılandırma sözdizimidir `(SameSiteMode)(-1)` :

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net Ayrıca, bu özellikler için kendi kendine özgü dört tanımlama bilgisi verir: anonim kimlik doğrulaması, Forms kimlik doğrulaması, oturum durumu ve rol yönetimi. Çalışma zamanında elde edilen bu tanımlama bilgilerinin örnekleri, `SameSite` `Secure` diğer tüm HttpCookie örnekleri gibi ve özellikleri kullanılarak yönetilebilir. Ancak, aynı site standardının sürecinizin ortaya çıktı nedeniyle, bu dört özellik tanımlama bilgilerine yönelik yapılandırma seçenekleri tutarsız olur. İlgili yapılandırma bölümleri ve öznitelikler, varsayılan olarak aşağıda gösterilmiştir. `SameSite` `Secure` Bir özellik için veya ilgili özniteliği yoksa, bu özellik yukarıda açıklanan bölümde yapılandırılan varsayılanlara geri döner `system.web/httpCookies` .

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Note**: ' belirtilmemiş ' yalnızca şu anda kullanılabilir `system.web/httpCookies@sameSite` . Gelecekteki güncelleştirmelerde daha önce gösterilen tanımlama bilgisi Esamesite özniteliklerine benzer bir sözdizimi eklemenizi umuyoruz. `(SameSiteMode)(-1)`Kod ayarı bu tanımlama bilgilerinin örneklerinde hala geçerlidir. *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>.NET uygulamalarını yeniden hedefle

.NET 4.7.2 veya üstünü hedeflemek için:

* *web.config* aşağıdakileri içerdiğinden emin olun:  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  [.Net geçiş kılavuzunda](/dotnet/framework/migration-guide/) daha fazla ayrıntı vardır.

* Projedeki NuGet paketlerinin doğru çerçeve sürümüne hedeflenmiş olduğunu doğrulayın. *packages.config* dosyasını inceleyerek doğru Framework sürümünü doğrulayabilirsiniz, örneğin:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  Yukarıdaki *packages.config* dosyasında `Microsoft.ApplicationInsights` paket:
    * , .NET 4.5.1 'e yöneliktir.
    * `targetFramework` `net472` Çerçeve hedefini hedefleyen güncelleştirilmiş bir paket varsa, özniteliği ' e güncelleştirilmiş olmalıdır.

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>4.7.2 'den önceki .NET sürümleri

Microsoft, aynı-site tanımlama bilgisi özniteliğini yazmak için 4.7.2 'in daha düşük .NET sürümlerini desteklemez. Şunları yapmak için güvenilir bir yol bulduk:

* Özniteliğin tarayıcı sürümüne bağlı olarak doğru yazıldığından emin olun.
* Daha eski çerçeve sürümlerindeki kimlik doğrulama ve oturum tanımlama bilgilerini durdurur ve ayarlar.

### <a name="december-patch-behavior-changes"></a>Aralık düzeltme eki davranış değişiklikleri

.NET Framework için belirli davranış değişikliği `SameSite` özelliğin `None` değeri yorumlaması:

* Düzeltme ekinin bir değeri `None` :
  * Özniteliği hiçbir şekilde gösterme.
* Düzeltme ekiyle sonra:
  * Bunun bir değeri, `None` "özniteliği değeri Ile yay" anlamına gelir `None` .
  * Bir `SameSite` değeri `(SameSiteMode)(-1)` özniteliğin yayınlanmasına neden olur.

Form kimlik doğrulaması ve oturum durumu tanımlama bilgileri için varsayılan SameSite değeri, ' dan ' a değiştirilmiştir `None` `Lax` .

### <a name="summary-of-change-impact-on-browsers"></a>Tarayıcılarda değişiklik etkisinin Özeti

Düzeltme ekini yükler ve ile bir tanımlama bilgisi verirseniz `SameSite.None` , iki işlemlerden biri gerçekleşir:
* Chrome V80, bu tanımlama bilgisini yeni uygulamaya göre değerlendirir ve tanımlama bilgisinde aynı site kısıtlamalarını zorlamayacaktır.
* Yeni uygulamayı destekleyecek şekilde güncelleştirilmemiş herhangi bir tarayıcı eski uygulamayı takip edecektir. Eski uygulama şöyle diyor:
  * Anladığınızı bir değer görürseniz, bunu yoksayın ve katı aynı site kısıtlamalarına geçiş yapın.

Böylece uygulama Chrome 'da kesilir veya çok sayıda başka yerde de kesintiye uğratır.

## <a name="history-and-changes"></a>Geçmiş ve değişiklikler

SameSite desteği ilk olarak .NET 4.7.2 'de [2016 taslak standardı](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)kullanılarak uygulanmıştır.

19 Kasım 2019, 2016 standardı ile 2019 standardına kadar, Windows için Kasım ' i güncelleştirme. Diğer Windows sürümlerine ek güncelleştirmeler geliyor. Daha fazla bilgi için bkz. <xref:samesite/kbs-samesite>.

 SameSite belirtiminin 2019 taslağı:

* , 2016 taslağı ile geriye dönük olarak uyumlu **değildir** . Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.
* Tanımlama bilgilerinin varsayılan olarak değerlendirilip değerlendirilmediğini belirtir `SameSite=Lax` .
* `SameSite=None`Siteler arası teslimin etkinleştirilmesi için açıkça onay veren tanımlama bilgilerini belirtir `Secure` .
* Yukarıda listelenen BB 'de açıklandığı şekilde verilen düzeltme ekleri tarafından desteklenir.
* , [Şubat 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)' de varsayılan olarak [Chrome](https://chromestatus.com/feature/5088147346030592) tarafından etkinleştirilmek üzere zamanlanır. Tarayıcılar 2019 içinde bu standarda geçmeyi başlattı.

<a name="known"></a>

## <a name="known-issues"></a>Bilinen Sorunlar

2016 ve 2019 taslak belirtimleri uyumlu olmadığından, Kasım 2019 .NET Framework güncelleştirmesi, kırılmaya neden olabilecek bazı değişiklikler sunar.

* Oturum durumu ve Forms kimlik doğrulama tanımlama bilgileri artık `Lax` , belirtilmemiş yerine ağa yazılır.
  * Çoğu uygulama tanımlama bilgileriyle çalışırken `SameSite=Lax` , ' yi kullanan siteler veya uygulamalar arasında gönderi yapan uygulamalar, `iframe` oturum durumu veya form yetkilendirme tanımlama bilgilerinin beklendiği gibi kullanılmadığını fark edebilir. Bu sorunu gidermek için, `cookieSameSite` daha önce anlatıldığı gibi uygun yapılandırma bölümündeki değeri değiştirin.
* Kod veya yapılandırmada açıkça ayarlanan HttpCookies `SameSite=None` artık bu değeri, daha önce atlandığı halde tanımlama bilgisiyle yazılmış. Bu, yalnızca 2016 taslak standardını destekleyen eski tarayıcılarla ilgili sorunlara neden olabilir.
  * Tarayıcıları tanımlama bilgileriyle 2019 taslak standardını destekleyen bir şekilde hedeflerken `SameSite=None` , bunları da işaretlemeniz gerektiğini unutmayın `Secure` .
  * Yazma değil 2016 davranışına dönmek için `SameSite=None` uygulama ayarını kullanın `aspnet:SupressSameSiteNone=true` . Bunun, uygulamadaki tüm HttpCookies için uygulanacağını unutmayın.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite tanımlama bilgisi işleme

Azure App Service .NET 4.7.2 uygulamalarında SameSite davranışlarını yapılandırma hakkında bilgi için bkz. [Azure App Service — SameSite tanımlama bilgisi işleme ve .NET Framework 4.7.2 Patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Eski tarayıcıları destekleme

2016 SameSite Standard uygulanan, bilinmeyen değerlerin değer olarak değerlendirilmelidir `SameSite=Strict` . 2016 SameSite standardını destekleyen eski tarayıcılardan erişilen uygulamalar, bir değeri olan bir SameSite özelliği edindiklerinde kesintiye uğramayabilir `None` . Web uygulamaları, eski tarayıcıları desteklemek istiyorlarsa, tarayıcı algılaması gerçekleştirmelidir. ASP.NET tarayıcı algılamayı uygulamaz; çünkü kullanıcı aracıları değerleri yüksek ölçüde geçici ve sık sık değiştirilir.

Microsoft 'un sorunu çözme yaklaşımı, tarayıcıyı `sameSite=None` desteklemez olarak bilindiğinde özniteliği tanımlama bilgilerinden atmak için tarayıcı algılama bileşenleri uygulamanıza yardımcı olur. Google 'ın önerisi, biri yeni özniteliğiyle, diğeri de özniteliği olmayan çift tanımlama bilgileri veriliydi. Bununla birlikte, Google 'ın öner, sınırlı olduğunu düşüntik. Bazı tarayıcılar, özellikle de mobil tarayıcılar bir sitenin tanımlama bilgisi sayısı veya bir etki alanı adı için çok küçük sınırlara sahiptir. Birden çok tanımlama bilgisi gönderdiğinizde, özellikle kimlik doğrulama tanımlama bilgileri gibi büyük tanımlama bilgileri mobil tarayıcı sınırına çok hızlı ulaşabilir ve bu da tanılama ve düzeltilmesi zor olan uygulama arızalarına yol açabilir. Framework 'ün yanı sıra, bir çift tanımlama bilgisi yaklaşımı kullanmak üzere güncelleştirilemeyebilir üçüncü taraf kodu ve bileşenleri büyük bir ekosistemi vardır.

[Bu GitHub deposundaki]() örnek projelerde kullanılan tarayıcı algılama kodu iki dosyada bulunuyor

* [C# SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

Bu algılamalar, 2016 standardını desteklediğimiz ve özniteliği tamamen kaldırılması gereken en yaygın tarayıcı aracısıdır. Bu, tamamen uygulama olarak tasarlanmamıştır:

* Uygulamanız, test sitemizdeki tarayıcıları görebilir.
* Ortamınız için gereken algılamaları eklemeye hazır olmanız gerekir.

Algılama işleminin nasıl yapılacağı, .NET ve kullanmakta olduğunuz Web çerçevesinin sürümüne göre farklılık gösterir. Aşağıdaki kod [HttpCookie](/dotnet/api/system.web.httpcookie) çağrı sitesinde çağrılabilir:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

Aşağıdaki ASP.NET 4.7.2 SameSite tanımlama bilgisi konularına bakın:

* [C# MVC](xref:samesite/csMVC)
* [C# WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>Sitenizin HTTPS 'ye yönlendirilmesini sağlama

ASP.NET 4. x, WebForms ve MVC için [IIS 'nın URL yeniden yazma](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) özelliği tüm istekleri https 'ye yönlendirmek için kullanılabilir. Aşağıdaki XML örnek bir kural göstermektedir:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

[IIS URL yeniden yazma](https://www.iis.net/downloads/microsoft/url-rewrite) 'nin şirket içi yüklemelerinde, yüklenmesi gerekebilecek isteğe bağlı bir özelliktir.

## <a name="test-apps-for-samesite-problems"></a>SameSite sorunları için test uygulamaları

Uygulamanızı, destekettiğiniz tarayıcılarla test etmeniz ve tanımlama bilgilerini içeren senaryolarınız üzerinden gitmeniz gerekir. Tanımlama bilgisi senaryoları genellikle şunları içerir

* Oturum açma formları
* Facebook, Azure AD, OAuth ve OıDC gibi dış oturum açma mekanizmaları
* Diğer sitelerden gelen istekleri kabul eden sayfalar
* Uygulamanızdaki iframe 'lere katıştırılacak şekilde tasarlanan sayfalar

Tanımlama bilgilerinin uygulamanızda oluşturulduğunu, kalıcı olduğunu ve doğru şekilde silindiğini denetlemeniz gerekir.

Üçüncü taraf oturum açma bilgileri gibi uzak sitelerle etkileşim kuran uygulamalar şunlar gerekir:

* Etkileşimi birden çok tarayıcıda test edin.
* [Tarayıcı algılamasını ve](#sob) bu belgede açıklanan risk azaltma işlemini uygulayın.

Yeni SameSite davranışını kabul edebilir bir istemci sürümünü kullanarak Web uygulamalarını test edin. Chrome, Firefox ve Kmıum Edge tümünde test için kullanılabilecek yeni bir katılım özelliği bayrakları vardır. Uygulamanız SameSite düzeltme eklerini uyguladıktan sonra, daha eski istemci sürümleriyle test edin, özellikle Safari. Daha fazla bilgi için bu belgede [eski tarayıcıları destekleme](#sob) bölümüne bakın.

### <a name="test-with-chrome"></a>Chrome ile test etme

Chrome 78 + bir yerde geçici bir risk azaltma yaptığından yanıltıcı sonuçlar verir. Chrome 78 + geçici risk azaltma, iki dakikadan daha eski tanımlama bilgilerine izin verir. Uygun test bayraklarıyla etkin olan Chrome 76 veya 77 daha doğru sonuçlar sağlar. Yeni bir SameSite davranışını test etmek için `chrome://flags/#same-site-by-default-cookies` **etkin**olarak değiştirin. Chrome 'un (75 ve üzeri) eski sürümleri, yeni ayar ile başarısız olarak bildirilir `None` . Bkz. bu belgede [eski tarayıcıları destekleme](#sob) .

Google, eski Chrome sürümlerini kullanılabilir hale getirir. Chrome 'un eski sürümlerini test etmek için [Kmıum indirme](https://www.chromium.org/getting-involved/download-chromium) bölümündeki yönergeleri izleyin. Chrome 'un eski sürümlerini arayarak sunulan bağlantılardan **Chrome indirmeyin** .

* [Kmıum 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Kmıum 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* Windows 'un 64 bit sürümünü kullanmıyorsanız, [Kmahaproxy görüntüleyicisini](https://omahaproxy.appspot.com/) kullanarak kmıum dalının, [küzum tarafından sunulan yönergeleri](https://www.chromium.org/getting-involved/download-chromium)kullanarak Chrome 74 ' e (v 74.0.3729.108) karşılık geldiğini arayabilirsiniz.

Canary sürümünden itibaren `80.0.3975.0` , LAX + GEÇICI sonrası risk azaltma, `--enable-features=SameSiteDefaultChecksMethodRigorously` azaltma 'nın kaldırıldığı özelliğin son bitiş durumunda siteler ve hizmetlerin test edilmesine izin vermek için yeni bayrağını kullanarak test amacıyla devre dışı bırakılabilir. Daha fazla bilgi için, bkz. Kmıum projeleri [SameSite Updates](https://www.chromium.org/updates/same-site)

#### <a name="test-with-chrome-80"></a>Chrome ile test 80 +

Yeni özniteliğini destekleyen Chrome 'un bir sürümünü [indirin](https://www.google.com/chrome/) . Yazma sırasında, geçerli sürüm Chrome 80 ' dir. Chrome 80 ' in `chrome://flags/#same-site-by-default-cookies` yeni davranışı kullanması için etkin olması gerekir. Aynı zamanda, bir `chrome://flags/#cookies-without-same-site-must-be-secure` sameSite özniteliği etkin olmayan tanımlama bilgileri için yaklaşan davranışı test etmek üzere () öğesini etkinleştirmeniz gerekir. Chrome 80, anahtarın özniteliği olmadan tanımlama bilgilerini ele almasını sağlamak için gereklidir `SameSite=Lax` , belirli istekler için zaman aşımına uğramış bir yetkisiz kullanım süresi ile birlikte. Her zaman yetkisiz kullanım süresini devre dışı bırakmak için Chrome 80 aşağıdaki komut satırı bağımsız değişkeniyle başlatılabilir:

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80, tarayıcı konsolunda eksik olan sameSite öznitelikleri hakkında uyarı iletileri içerir. Tarayıcı konsolunu açmak için F12 kullanın.

### <a name="test-with-safari"></a>Safari ile test etme

Safari 12, önceki taslağı kesin olarak uyguladık ve yeni `None` değer bir tanımlama bilgisinde olduğunda başarısız olur. `None` Bu belgede [eski tarayıcıları destekleyen](#sob) tarayıcı algılama kodu aracılığıyla kaçınılmaz. MSAL, ADAL veya kullandığınız herhangi bir kitaplığı kullanarak Safari 12, Safari 13 ve WebKit tabanlı işletim sistemi stili oturum açma stilini test edin. Sorun, temel alınan işletim sistemi sürümüne bağımlıdır. OSX Mojave (10,14) ve iOS 12 ' nin yeni SameSite davranışıyla uyumluluk sorunlarına sahip olduğu bilinmektedir. İşletim sistemini OSX Catalina (10,15) veya iOS 13 ' e yükseltmek sorunu düzeltir. Safari 'nin şu anda yeni belirtim davranışını test etmek için bir katılım bayrağı yoktur.

### <a name="test-with-firefox"></a>Firefox ile test etme

Yeni standart için Firefox desteği, `about:config` sayfada özellik bayrağıyla birlikte seçilerek, 68 + sürümünde test edilebilir `network.cookie.sameSite.laxByDefault` . Daha eski Firefox sürümleriyle uyumluluk sorunları hakkında rapor yoktu.

### <a name="test-with-edge-legacy-browser"></a>Edge (eski) tarayıcıyla test etme

Edge, eski SameSite standardını destekler. Edge sürümü 44 +, yeni standart ile bilinen uyumluluk sorunlarına sahip değildir.

### <a name="test-with-edge-chromium"></a>Edge ile test (Kmıum)

Sayfada SameSite bayrakları ayarlanır `edge://flags/#same-site-by-default-cookies` . Edge Kmıum ile hiçbir uyumluluk sorunu bulunmadı.

### <a name="test-with-electron"></a>Elektron ile test

Elektron sürümleri, daha eski bir Kmıum sürümlerini içerir. Örneğin, takımlar tarafından kullanılan elektron sürümü, eski davranışı gösteren Kmıum 66 ' dir. Ürününüzün kullandığı elektron sürümüyle kendi uyumluluk testinizi gerçekleştirmeniz gerekir. Bkz. [eski tarayıcıları destekleme](#sob).

## <a name="reverting-samesite-patches"></a>SameSite yamaları geri alınıyor

.NET Framework uygulamalarında güncelleştirilmiş sameSite davranışını, sameSite özniteliğinin değeri için yayılmayan önceki davranışına geri döndürebilir `None` ve değeri yaymayan kimlik doğrulama ve oturum tanımlama bilgilerini geri döndürmenize olanak sağlar. Bu, *son derece geçici bir çözüm*olarak görüntülenmelidir, çünkü Chrome değişiklikleri, standart değişiklikleri destekleyen tarayıcıları kullanan kullanıcılar için tüm dış post isteklerini veya kimlik doğrulamasını bozacaktır.

### <a name="reverting-net-472-behavior"></a>.NET 4.7.2 davranışını geri alma

*web.config* aşağıdaki yapılandırma ayarlarını içerecek şekilde güncelleştirin:

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>Ek kaynaklar

* [ASP.NET ve ASP.NET Core yaklaşan SameSite tanımlama bilgisi değişiklikleri](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Aynı-varsayılan ve "SameSite = none;. Güvenli "tanımlama bilgileri](https://www.chromium.org/updates/same-site/test-debug)
* [Kmıum blogu: geliştiriciler: yeni SameSite için hazırlanın = yok; Güvenli tanımlama bilgisi ayarları](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Aynı şekilde açıklanan SameSite tanımlama bilgileri](https://web.dev/samesite-cookies-explained/)
* [Chrome güncelleştirmeleri](https://www.chromium.org/updates/same-site)
* [.NET SameSite yamaları](/aspnet/samesite/kbs-samesite)
* [Azure Web uygulamaları aynı site bilgileri](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure ActiveDirectory aynı site bilgileri](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
