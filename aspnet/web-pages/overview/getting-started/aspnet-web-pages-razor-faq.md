---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web Sayfaları (Razor) SSS | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu makalede, web sayfaları (Razor) ve WebMatrix ASP.NET hakkında sık sorulan bazı sorular listelenir. Web Sayfaları ASP.NET (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543710"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web Sayfaları (Razor) SSS

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix artık ASP.NET Web Sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) veya Visual [Studio Code](https://code.visualstudio.com/)kullanın.
>
> Bu makalede, web sayfaları (Razor) ve WebMatrix ASP.NET hakkında sık sorulan bazı sorular listelenir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web Sayfaları (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Bu öğretici ayrıca web sayfaları 2, WebMatrix 2 ve Visual Studio 2012 ASP.NET ile de çalışır.

- [web sayfaları, ASP.NET Web Formları ASP.NET ve ASP.NET MVC arasındaki fark nedir?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Web Sayfaları ile çalışmak için WebMatrix'e ihtiyacım var mı?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Web Sayfaları sayfasında ASP.NET Web Formları denetimlerini kullanabilir miyim?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix kullanmadan ASP.NET bir Web Sayfası sitesini dağıtabilir miyim?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Girişleri desteklemek için WebSecurity yardımcısını kullanmam gerekiyor mu?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET Web Sayfaları HTML5'i destekliyor mu?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Web Sayfaları ile JavaScript ve jQuery kullanabilir miyim?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Ek Kaynaklar](#AdditionalResources)

Hatalar ve diğer sorunlarla ilgili sorularınız için [Web Sayfaları (Jilet) Sorun Giderme Kılavuzu'ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253001)bakın.

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>web sayfaları, ASP.NET Web Formları ASP.NET ve ASP.NET MVC arasındaki fark nedir?

Her üç dinamik web uygulamaları oluşturmak için ASP.NET teknolojiler şunlardır:

- ASP.NET Web Sayfaları, HTML sayfalarına dinamik (sunucu tarafı) kod ve veritabanı erişimi eklemeye odaklanır ve basit ve hafif sözdizimine sahiptir.
- ASP.NET Web Formları bir sayfa nesnesi modeli ve geleneksel pencere türü denetimleri (düğmeler, listeler, vb) dayanmaktadır. Web Formları, istemci tabanlı (Windows formları) geliştirme ile çalışmış olanlara tanıdık olay tabanlı bir model kullanır.
- ASP.NET MVC, ASP.NET için model görünümü denetleyicisi deseni uygular. Vurgu "endişelerin ayrılması" (işleme, veri ve UI katmanları) üzerindedir.

Her üç çerçeve de tam olarak desteklenir ve ASP.NET ekibi tarafından geliştirilmeye devam etmektedir. Genel olarak, hangi çerçevenin kullanılacağının seçimi, geçmişinize ve ASP.NET deneyiminize bağlıdır.

Özellikle web sayfalarını ASP.NET, HTML'yi zaten bilen kişilerin sayfalarına sunucu işleme eklemelerini kolaylaştırmak için tasarlanmıştır. Bu öğrenciler, hobi, programlama yeni genel insanlar için iyi bir seçimdir. Ayrıca non-ASP.NET web teknolojileri ile deneyime sahip geliştiriciler için iyi bir seçim olabilir.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Web Sayfaları ile çalışmak için WebMatrix'e ihtiyacım var mı?

Hayır. WebMatrix artık ASP.NET Web Sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) veya Visual [Studio Code](https://code.visualstudio.com/)kullanın.

Visual Studio veya Visual Studio Code'u kullanmak istemiyorsanız, bileşen ürünlerini [Microsoft Web Platform Installer'ı](https://www.microsoft.com/web/downloads/platform.aspx)kullanarak tek tek yükleyebilirsiniz. Aşağıdaki ürünlere ihtiyacınız var:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (ASP.NET Web Sayfaları çerçevesini de yükler)
- IIS Express (web sunucusu)
- Microsoft SQL Server Compact 4.0 (veritabanı)

*.cshtml* (veya *.vbhtml)* sayfalarını yeniden yapmak için metin düzenleyicisi kullanabilirsiniz.

SQL Server Compact veritabanlarını *(.sdf* dosyaları) bir araç olmadan yönetmek biraz daha zordur. Visual Studio *,sdf* veritabanlarını yönetmek için araçlar içerir. Ayrıca, birçok SQL Server yönetim görevini gerçekleştirmek için KODDA SQL komutlarını çalıştırabilirsiniz.

*.cshtml* sayfalarını tümleşik bir geliştirme ortamı (IDE) kullanmadan sınamak için, bunları canlı bir sunucuya dağıtabilirsiniz. [(Bkz. WebMatrix kullanmadan ASP.NET bir Web Sayfası sitesini dağıtabilir miyim?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>IDE kullanmadan IIS Express'i çalıştırma

IIS Express'i bilgisayarınıza bir web sunucusu olarak yüklerseniz, bunu sayfaları sınamak için kullanabilirsiniz. IIS Express'i komut satırından çalıştırabilir ve belirli bir bağlantı noktası numarasıyla ilişkilendirebilirsiniz. Daha sonra tarayıcınızda *.cshtml* dosyaları istediğinizde bu bağlantı noktasını belirtirsiniz.

Windows'da, yönetici ayrıcalıkları içeren bir komut istemi açın ve *C:\Program Files\IIS Express* olarak değiştirin. (64 bit sistemler için *C:\Program Files (x86)\IIS Express* klasörünü kullanın.) Ardından sitenize giden gerçek yolu kullanarak aşağıdaki komutu girin:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Başka bir işlem tarafından zaten rezerve edilmiş herhangi bir bağlantı noktası numarasını kullanabilirsiniz. (1024'ün üzerindeki bağlantı noktası numaraları genellikle ücretsizdir.) `path` Değer için *.cshtml* dosyalarının bulunduğu web sitesi klasörünün yolunu kullanın.

Sayfalarınıza hizmet vermek üzere IIS Express'i kurmak için bu komutu çalıştırdıktan sonra, bir tarayıcı açabilir ve *.cshtml* dosyasına göz atabilirsiniz. Aşağıdaki gibi bir URL kullanın:

`http://localhost:35896/default.cshtml`

IIS Express komut satırı seçenekleriyle `iisexpress.exe /?` ilgili yardım için komut satırına girin.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Web Sayfaları sayfasında ASP.NET Web Formları denetimlerini kullanabilir miyim?

Hayır. Web Formlar [Denetimi,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) doğrulama [denetimleri](https://msdn.microsoft.com/library/bwd43d0x)ve [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) denetimi gibi denetimler yalnızca Web Forms sayfalarında *(.aspx* dosyaları) çalışır. Bu denetimler, Web Formları sayfa çerçevesini gerektirir.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix kullanmadan ASP.NET bir Web Sayfası sitesini dağıtabilir miyim?

Evet. Web sitesi dosyalarını bir sunucuya el ile kopyalayabilirsiniz (genellikle FTP kullanarak). El ile kopya yaparsanız, SQL Server Compact'ı (veritabanı) destekleyen dosyaları da kopyalamanız gerekir. Ayrıntılar için, web [sayfaları uygulamalarını aracı olmadan dağıtan](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)blog girişine bakın.

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Girişleri desteklemek için WebSecurity yardımcısını kullanmam gerekiyor mu?

Hayır. ASP.NET `SimpleMembership` Web Sayfalarının bir parçası olan sağlayıcı bir seçenektir. ASP.NET bir parçası olan (Web Formlarında çalışmaya alışık olabileceğiniz) güvenlik sağlayıcıları da kullanılabilir. Örneğin, formların kimlik doğrulamasını web formlarında olduğu gibi ASP.NET Web Sayfalarında da kullanabilirsiniz. Form kimlik doğrulamasının nasıl kullanılacağına bir örnek olarak, [C#.NET kullanarak ASP.NET Uygulamanızda Form Tabanlı Kimlik Doğrulamanasıl Uygulanır](https://support.microsoft.com/kb/301240)Microsoft Destek makalesine bakın. Basit bir örneği indirmek için ["Giriş &amp; Parolası"nın ASP.NET sürümüne](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)bakın.

Windows kimlik doğrulamasının nasıl kullanılacağı hakkında bilgi için, [ASP.NET Web Sayfalarında Windows kimlik doğrulamasını kullanma](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)blog gönderisine bakın.

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET Web Sayfaları HTML5'i destekliyor mu?

Evet. ASP.NET Web Sayfaları *(.cshtml* veya *.vbhtml* sayfaları) ile oluşturduğunuz sayfalar, sayfa işlenmeden önce sunucuda çalışan kodlar da içeren HTML sayfalarıdır. Kullanıcının tarayıcısı HTML5'i desteklediği sürece, *.cshtml* veya *.vbhtml* sayfasında HTML5 öğelerini kullanabilirsiniz.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Web Sayfaları ile JavaScript ve jQuery kullanabilir miyim?

Kesinlikle. ASP.NET Web Sayfaları *(.cshtml* veya *.vbhtml* sayfaları) ile oluşturduğunuz sayfalar, içinde sunucu kodu bulunan sadece HTML sayfalarıdır. Bu nedenle, javascript veya jQuery kullanarak normal bir HTML sayfasında yapabileceğiniz her şeyi de bir *.cshtml* veya *.vbhtml* sayfasında yapabilirsiniz.

WebMatrix'teki **Başlangıç Sitesi** şablonu bir dizi jQuery kitaplığı içerir. Bu şablonu kullanarak bir site oluşturursanız, *Scripts* klasöründe jQuery çekirdek kitaplığı *(jquery-1.6.2.js)* ve jQuery doğrulama için kitaplıklar *(jquery.validate.js,* vb.) bulunur.

Burada ASP.NET Web Sayfaları ile jQuery kullanmayollarını gösteren bazı blog gönderileri şunlardır:

- Rachel Appel tarafından [WebMatrix kullanarak ASP.NET Web Sayfaları için jQuery İyilik ekleme](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)
- [5 dakika: WebMatrix + jQuery UI + json + jQuery şablonları](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Jonas Eriksson tarafından
- Mike Brind tarafından [WebMatrix Ve jQuery Formları](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web Sayfaları (Razor) Sorun Giderme Kılavuzu](https://go.microsoft.com/fwlink/?LinkId=253001)

web ASP.NET web sitesinde [WebMatrix ve ASP.NET Web Sayfaları forumu](https://forums.asp.net/1224.aspx/1?WebMatrix)
