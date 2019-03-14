---
title: ASP.NET Core tek sayfalı uygulamalar oluşturmak için JavaScriptServices kullanma
author: scottaddie
description: Bir tek sayfa uygulaması (ASP.NET Core tarafından desteklenen SPA) oluşturmak için JavaScriptServices kullanmanın avantajları hakkında bilgi edinin.
ms.author: scaddie
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
uid: client-side/spa-services
ms.openlocfilehash: ee772e67ef14608bcc6e3498ade00424ff6090e5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077286"
---
# <a name="use-javascriptservices-to-create-single-page-applications-in-aspnet-core"></a>ASP.NET Core tek sayfalı uygulamalar oluşturmak için JavaScriptServices kullanma

Tarafından [Scott Addie](https://github.com/scottaddie) ve [Fiyaz Hasan](http://fiyazhasan.me/)

Tek sayfa uygulama (SPA) web uygulamasının kendi devralınan zengin kullanıcı deneyimi nedeniyle popüler bir türdür. İstemci tarafı SPA çerçeveleri veya kitaplıkları gibi tümleştirme [Angular](https://angular.io/) veya [React](https://facebook.github.io/react/), sunucu tarafı çerçevelerle gibi ASP.NET Core zor olabilir. [JavaScriptServices](https://github.com/aspnet/JavaScriptServices) tümleştirme sürecindeki uyuşmazlıkları azaltmak için geliştirilmiştir. Ancak, farklı istemci ve sunucu teknoloji yığınları arasında sorunsuz bir işlemi etkinleştirir.

<a name="what-is-js-services"></a>

## <a name="what-is-javascriptservices"></a>JavaScriptServices nedir

JavaScriptServices ASP.NET Core için istemci tarafı teknolojilerinin koleksiyonudur. ASP.NET Core geliştiricilerinin Spa'lar oluşturmaya yönelik olarak tercih edilen sunucu tarafı platformu olarak yerleştirmek için hedefi sağlamaktır.

Üç farklı NuGet paketlerini JavaScriptServices oluşur:

* [Microsoft.AspNetCore.NodeServices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)
* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)
* [Microsoft.AspNetCore.SpaTemplates](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)

Bu paketler yararlıdır,:

* Sunucu üzerinde JavaScript çalıştırma
* SPA altyapı veya kitaplığı kullanın
* İstemci tarafı Web varlıklarla oluşturun

Bu makalenin odak çoğunu SpaServices paketini kullanarak yerleştirilir.

<a name="what-is-spa-services"></a>

## <a name="what-is-spaservices"></a>SpaServices nedir

ASP.NET Core geliştiricilerinin Spa'lar oluşturmaya yönelik olarak tercih edilen sunucu tarafı platformu olarak yerleştirmek için SpaServices oluşturulur. SpaServices Spa'lar ASP.NET Core ile geliştirmek için gerekli değildir ve bu belirli istemci altyapısına kilitlemez.

SpaServices gibi kullanışlı bir altyapı sağlar:

* [Sunucu tarafı prerendering](#server-prerendering)
* [Web geliştirme ara yazılımı](#webpack-dev-middleware)
* [Sık erişimli modülü değiştirme](#hot-module-replacement)
* [Yönlendirme Yardımcıları](#routing-helpers)

Toplu olarak, bu altyapı bileşenlerini, hem geliştirme iş akışını hem de çalışma zamanı deneyimi geliştirin. Bileşenleri ayrı ayrı önemsenmeksizin devralınabilir.

<a name="spa-services-prereqs"></a>

## <a name="prerequisites-for-using-spaservices"></a>SpaServices kullanmanın önkoşulları

SpaServices ile çalışmak için aşağıdakileri yükleyin:

* [Node.js](https://nodejs.org/) (sürüm 6 veya sonrası) npm ile
  * Bu bileşenler yüklenir ve bulunabilir doğrulamak için komut satırından aşağıdaki komutu çalıştırın:

    ```console
    node -v && npm -v
    ```

Not: Bir Azure web sitesine dağıtıyorsanız, burada bir şey yapmanız gerekmez &mdash; Node.js yüklü olduğundan ve sunucu ortamlarında kullanılabilir.

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]

  * Visual Studio 2017'yi kullanarak Windows üzerinde kullanıyorsanız, SDK'yı seçerek yüklü **.NET Core çoklu platform geliştirme** iş yükü.

* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet paketi

<a name="server-prerendering"></a>

## <a name="server-side-prerendering"></a>Sunucu tarafı prerendering

Bir evrensel (isomorphic olarak da bilinir) uygulama özellikli olan hem çalışan sunucu ve istemci üzerindeki bir JavaScript uygulamasıdır. Angular, React ve diğer popüler çerçeveleri için bu uygulama geliştirme stili Evrensel bir platform sağlar. İlk Node.js aracılığıyla sunucuda framework bileşenleri oluşturma ve yürütme istemciye daha fazla temsilci olur.

ASP.NET Core [etiket Yardımcıları](xref:mvc/views/tag-helpers/intro) tarafından sağlanan SpaServices server JavaScript işlevleri çağrılarak sunucu tarafı prerendering uygulamasını basitleştirin.

### <a name="prerequisites"></a>Önkoşullar

Aşağıdakileri yükleyin:

* [ASP.NET prerendering](https://www.npmjs.com/package/aspnet-prerendering) npm paketi:

    ```console
    npm i -S aspnet-prerendering
    ```

### <a name="configuration"></a>Yapılandırma

Etiket Yardımcıları projesinin ad kayıt bulunabilir yapılan *_viewımports.cshtml* dosyası:

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]

Bu etiket Yardımcıları hemen bir HTML benzeri sözdizimi Razor görünüm içinde yararlanarak alt düzey API'ler ile doğrudan iletişim ayrıntılı olarak incelenmektedir soyut:

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]

### <a name="the-asp-prerender-module-tag-helper"></a>`asp-prerender-module` Etiketi Yardımcısı

`asp-prerender-module` Etiketi Yardımcısı, önceki kod örneğinde kullanılan yürütür *ClientApp/dist/main-server.js* Node.js aracılığıyla sunucuda. Açıklık'ın çok için *ana server.js* dosyasıdır TypeScript JavaScript transpilation görevin bir yapıt [Web](http://webpack.github.io/) derleme işlemi. Web tanımlayan bir giriş noktası diğer `main-server`; ve bu diğer adı için bağımlılık grafiği geçişini başlar *ClientApp/önyükleme-server.ts* dosyası:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]

Aşağıdaki Angular örnekte *ClientApp/önyükleme-server.ts* dosya kullanır `createServerRenderer` işlevi ve `RenderResult` tür `aspnet-prerendering` npm paketi, sunucu işleme Node.js aracılığıyla yapılandırılır. Kesin türü belirtilmiş bir JavaScript içinde sarmalanmış bir Çözümle işlev çağrısı için sunucu tarafı işleme geçirilen hedefleyen bir HTML biçimlendirmesi `Promise` nesne. `Promise` Nesnenin önemi olan, zaman uyumsuz olarak DOM'ın yer tutucu öğesi yerleştirmeye sayfasına HTML biçimlendirme sağlar.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]

### <a name="the-asp-prerender-data-tag-helper"></a>`asp-prerender-data` Etiketi Yardımcısı

İle birlikte zaman `asp-prerender-module` etiketi Yardımcısı `asp-prerender-data` etiketi Yardımcısı, bağlamsal bilgiler için sunucu tarafı JavaScript Razor görünümden geçirmek için kullanılabilir. Örneğin, kullanıcı verilerini aşağıdaki biçimlendirme geçirir `main-server` Modülü:

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]

Alınan `UserName` bağımsız değişkeni yerleşik JSON serileştirici kullanılarak serileştirilmiş ve depolanan `params.data` nesne. Angular aşağıdaki örnekte veri içinde kişiselleştirilmiş bir karşılama oluşturmak için kullanılan bir `h1` öğesi:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]

Not: Etiket Yardımcıları içinde geçirilen özellik adları ile temsil edilir **PascalCase** gösterimi. Burada aynı özellik adları ile gösterilir, JavaScript, Karşıtlık **camelCase**. Bu fark için varsayılan JSON seri hale getirme yapılandırması sorumludur.

Yukarıdaki kod örneğinde genişletmek için verileri sunucudan görünüme hydrating tarafından geçirilebilir `globals` özelliği için sağlanan `resolve` işlevi:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]

`postList` İçinde tanımlanan bir dizi `globals` nesne bağlı tarayıcının genel `window` nesne. Bu değişken hoisting genel kapsam için aynı verileri bir kez sunucuda ve istemcinin yeniden yüklenmesi için özellikle ilgili olarak çaba, çoğaltma ortadan kaldırır.

![Pencere nesnesi bağlı genel postList değişkeni](spa-services/_static/global_variable.png)

<a name="webpack-dev-middleware"></a>

## <a name="webpack-dev-middleware"></a>Web geliştirme ara yazılımı

[Web geliştirme ara yazılım](https://webpack.github.io/docs/webpack-dev-middleware.html) yapabildiği Web yapılar kaynakları isteğe bağlı olarak Basitleştirilmiş geliştirme iş akışı sunar. Ara yazılım, otomatik olarak derler ve bir sayfa tarayıcıya yeniden yüklendiğinde istemci-tarafı kaynaklar sunar. Başka bir üçüncü taraf bağımlılığı veya özel kod değiştiğinde Web projenin npm derleme betiği aracılığıyla el ile başlatmak için yaklaşımdır. Bir npm derleme betiği *package.json* dosya, aşağıdaki örnekte gösterilmiştir:

```json
"build": "npm run build:vendor && npm run build:custom",
```

### <a name="prerequisites"></a>Önkoşullar

Aşağıdakileri yükleyin:

* [ASP.NET Web](https://www.npmjs.com/package/aspnet-webpack) npm paketi:

    ```console
    npm i -D aspnet-webpack
    ```

### <a name="configuration"></a>Yapılandırma

HTTP istek işlem hattı aşağıdaki kod aracılığıyla içine kayıtlı Web geliştirme ara yazılım *Startup.cs* dosyanın `Configure` yöntemi:

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=snippet_WebpackMiddlewareRegistration&highlight=4)]

`UseWebpackDevMiddleware` Genişletme yöntemi çağrıldığında, önce [statik dosya barındırma kaydetme](xref:fundamentals/static-files) aracılığıyla `UseStaticFiles` genişletme yöntemi. Uygulama geliştirme modunda çalıştırıldığında güvenlik nedenleriyle, ara yazılım kaydedin.

*Webpack.config.js* dosyanın `output.publicPath` özelliği söyler izlemek için bir ara yazılım `dist` klasördeki değişiklikleri:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]

<a name="hot-module-replacement"></a>

## <a name="hot-module-replacement"></a>Sık erişimli modülü değiştirme

Web'ın düşünebilirsiniz [sık erişimli modülü değiştirme](https://webpack.js.org/concepts/hot-module-replacement/) (HMR) özelliği'nın Gelişmiş hali olarak [Web geliştirme ara yazılım](#webpack-dev-middleware). HMR aynı avantajları sunar, ancak otomatik olarak değişiklikleri derledikten sonra sayfa içeriği güncelleştirerek daha fazla geliştirme iş akışı kolaylaştırır. Bu, geçerli bellek içi durumu ve hata ayıklama oturumu SPA ile neden tarayıcı yenileme ile karıştırmayın. Web geliştirme ara yazılım hizmeti ve değişiklikleri tarayıcıya gönderilmesini anlamına gelir tarayıcı arasında canlı bir bağlantı yoktur.

### <a name="prerequisites"></a>Önkoşullar

Aşağıdakileri yükleyin:

* [Web hot Ara](https://www.npmjs.com/package/webpack-hot-middleware) npm paketi:

    ```console
    npm i -D webpack-hot-middleware
    ```

### <a name="configuration"></a>Yapılandırma

HMR bileşen MVC'nin HTTP istek işlem hattı, kaydedilmesi gerekir `Configure` yöntemi:

```csharp
app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
    HotModuleReplacement = true
});
```

İle doğru olarak [Web geliştirme ara yazılım](#webpack-dev-middleware), `UseWebpackDevMiddleware` genişletme yöntemi çağrıldığında, önce `UseStaticFiles` genişletme yöntemi. Uygulama geliştirme modunda çalıştırıldığında güvenlik nedenleriyle, ara yazılım kaydedin.

*Webpack.config.js* dosya tanımlamalıdır bir `plugins` dizi bile boş bırakılır:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]

Uygulamayı tarayıcıda yüklendikten sonra geliştirici araçları konsol sekmesi HMR Etkinleştirme Onayı sağlar:

![Sık erişimli modülü değiştirme bağlı ileti](spa-services/_static/hmr_connected.png)

<a name="routing-helpers"></a>

## <a name="routing-helpers"></a>Yönlendirme Yardımcıları

Çoğu ASP.NET Core tabanlı Spa'lar içinde sunucu tarafı ek olarak istemci tarafı yönlendirmesi istersiniz. SPA ve MVC yönlendirme sistemleri girişim bağımsız olarak çalışabilir. Yoktur, ancak bir kenar büyük/küçük harf taşıyor sorunlarını: HTTP 404 yanıtları tanımlayan.

Senaryoyu göz önünde bulundurun uzantısız bir yolu `/some/page` kullanılır. İstek deseni-sunucu tarafı rota match değil, ancak desenine bir istemci-tarafı rota ile eşleşmekte varsayılır. Şimdi gelen bir istek için göz önünde bulundurun `/images/user-512.png`, hangi genellikle bekliyor sunucudaki bir görüntü dosyası bulunamıyor. Bu istenen kaynak yolu herhangi bir sunucu tarafı rota veya statik dosya eşleşmiyorsa, istemci-tarafı uygulaması, işlemek olası — genellikle bir 404 HTTP durum kodu iade etmek istediğiniz.

### <a name="prerequisites"></a>Önkoşullar

Aşağıdakileri yükleyin:

* İstemci tarafı yönlendirme npm paket. Angular örnek olarak kullanıp:

    ```console
    npm i -S @angular/router
    ```

### <a name="configuration"></a>Yapılandırma

Adlı bir genişletme yöntemi `MapSpaFallbackRoute` kullanılır `Configure` yöntemi:

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=snippet_MvcRoutingTable&highlight=7-9)]

İpucu: Rotalar yapılandırılmış sırada değerlendirilir. Sonuç olarak, `default` rota önceki kod örneğinde kullanılan ilk desen eşleştirmesi için.

<a name="new-project-creation"></a>

## <a name="creating-a-new-project"></a>Yeni proje oluşturma

JavaScriptServices önceden yapılandırılmış uygulama şablonları sağlar. SpaServices bu şablonları farklı çerçeveler ve kitaplıklar gibi Angular, React ve Redux ile birlikte kullanılır.

Bu şablonlar, aşağıdaki komutu çalıştırarak, .NET Core CLI yüklenebilir:

```console
dotnet new --install Microsoft.AspNetCore.SpaTemplates::*
```

Kullanılabilir SPA şablonlar listesi görüntülenir:

| Şablonlar                                 | Kısa Ad | Dil | Etiketler        |
|:------------------------------------------|:-----------|:---------|:------------|
| Angular ile ASP.NET Core MVC             | Angular    | [C#]     | MVC/Web/SPA |
| React.js ile ASP.NET Core MVC            | react      | [C#]     | MVC/Web/SPA |
| ASP.NET Core MVC React.js ve Redux  | açarken kilitlenmesi | [C#]     | MVC/Web/SPA |

SPA şablonlardan birini kullanarak yeni bir proje oluşturmak için dahil **kısa ad** şablonda, [yeni dotnet](/dotnet/core/tools/dotnet-new) komutu. Aşağıdaki komut, sunucu tarafı için yapılandırılan ASP.NET Core MVC ile Angular bir uygulama oluşturur:

```console
dotnet new angular
```

<a name="runtime-config-mode"></a>

### <a name="set-the-runtime-configuration-mode"></a>Çalışma zamanı yapılandırma modunu ayarlayın

Birincil çalışma zamanı yapılandırma için iki mod vardır:

* **Geliştirme**:
  * Hata ayıklamayı kolaylaştırmak için kaynak eşlemeleri içerir.
  * İstemci tarafı kod performans için en iyi duruma değil.
* **Üretim**:
  * Kaynak eşlemeleri dışlar.
  * İstemci tarafı kod paketleme ve küçültme ile en iyi duruma getirir.

ASP.NET Core kullanan adlı bir ortam değişkeni `ASPNETCORE_ENVIRONMENT` yapılandırma modunu depolamak için. Bkz: **[ortamı](xref:fundamentals/environments#set-the-environment)** daha fazla bilgi için.

### <a name="running-with-net-core-cli"></a>.NET Core CLI ile çalıştırma

Proje kök dizininde aşağıdaki komutu çalıştırarak gerekli NuGet ve npm paketlerini geri yükleyin:

```console
dotnet restore && npm i
```

Derleme ve uygulamayı çalıştırın:

```console
dotnet run
```

Şunlara göre localhost üzerinde uygulama başladığında [çalışma zamanı yapılandırma modunu](#runtime-config-mode). Gezinme `http://localhost:5000` tarayıcısında giriş sayfası görüntüler.

### <a name="running-with-visual-studio-2017"></a>Visual Studio 2017 ile çalıştırma

Açık *.csproj* tarafından oluşturulan dosya [yeni dotnet](/dotnet/core/tools/dotnet-new) komutu. Gerekli NuGet ve npm paketleri proje üzerinde otomatik olarak geri yüklenir. Bu geri yükleme işlemi birkaç dakika sürebilir ve tamamlandığında çalıştırmaya hazır bir uygulamadır. Yeşil çalıştırma düğmesine veya tuşuna tıklayın `Ctrl + F5`, ve tarayıcıda uygulama giriş sayfası açılır. Uygulama ayarına göre localhost üzerinde çalışır [çalışma zamanı yapılandırma modunu](#runtime-config-mode).

<a name="app-testing"></a>

## <a name="testing-the-app"></a>Uygulamayı test etme

SpaServices şablonları kullanarak istemci tarafı testleri çalıştırmak için önceden yapılandırılmış [Karma](https://karma-runner.github.io/1.0/index.html) ve [Jasmine](https://jasmine.github.io/). Test Çalıştırıcısı bu testler için karma bilgileriyse jasmine bir popüler birim testi çerçevesi için JavaScript, ' dir. Karma çalışmak üzere yapılandırılmış [Web geliştirme ara yazılım](#webpack-dev-middleware) sağlayacak şekilde Geliştirici durdurmak ve değişiklikler her zaman test çalıştırması için gerekli değildir. Test çalışması veya test çalışması karşı çalışan kod olup olmadığını test otomatik olarak çalıştırılır.

Angular uygulamasını örnek olarak kullanıp, Jasmine iki test çalışmaları zaten için sağlanan `CounterComponent` içinde *counter.component.spec.ts* dosyası:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]

Komut istemi açın *ClientApp* dizin. Şu komutu çalıştırın:

```console
npm test
```

Komut dosyası içinde tanımlanan ayarlarını okur Karma test Çalıştırıcısı başlatır *karma.conf.js* dosya. Diğer ayarlar arasında *karma.conf.js* aracılığıyla yürütülecek test dosyalarını tanımlar, `files` dizi:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]

<a name="app-publishing"></a>

## <a name="publishing-the-application"></a>Uygulama yayımlama

Oluşturulan istemci-tarafı varlıkları ve yayımlanan ASP.NET Core yapıları dağıtmak için hazır bir pakete birleştiren çok uğraşmayı gerektirebilir. Ne SpaServices adlı özel bir MSBuild hedefi ile tüm yayın işlem düzenler `RunWebpack`:

[!code-xml[](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]

MSBuild hedefi aşağıdaki sorumluluklara sahiptir:

1. Npm paketlerini geri yükle
1. Üçüncü taraf, istemci tarafı varlıkların üretim sınıfı oluşturma
1. Özel istemci tarafı varlıkların üretim sınıfı oluşturma
1. Web oluşturulan varlıkları publish klasörüne kopyalayın.

MSBuild hedefi çalıştırılırken çağrılır:

```console
dotnet publish -c Release
```

## <a name="additional-resources"></a>Ek kaynaklar

* [Angular belgeleri](https://angular.io/docs)
