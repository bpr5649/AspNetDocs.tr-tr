---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET ve Web Araçları 2012.2 Yayın Notları | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET ve Web Araçları 2012.2 için sürüm notları.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676309"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET and Web Tools 2012.2 Sürüm Notları

> Bu belge, ASP.NET ve Web Araçları 2012.2 sürümü açıklanır. Bu Visual Studio Web Tooling ve ASP.NET için bir güncelleştirmedir.

- [Kurulum Notları](#_Installation)
- [Belgeler](#_Documentation)
- [Destek](#_Support)
- [Yazılım Gereksinimleri](#_Software_Requirements)
- [ASP.NET ve Web Araçlarında Yeni Özellikler 2012.2](#_New_Features_in)

    - [Araçlar](#_Tooling)
    - [Web Yayıncılık](#_Web_Publishing)
    - [ASP.NET MVC Şablonları](#_Templates)
    - [ASP.NET Web API'si](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET Dostu URL'ler](#_ASP.NET_Friendly_URLs)
- [Bilinen Sorunlar ve Son Dakika Değişiklikleri](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Kurulum Notları

ASP.NET ve Web Araçları 2012.2 Visual Studio 2012 web [platformu yükleyici](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)kullanılarak yüklenebilir. Bu gerekli web için Visual Studio 2012 veya Visual Studio Express 2012 için bir güncelleştirmedir. Visual Studio yüklü yoksa, Web için Visual Studio Express 2012 yüklenir.

ayrıca ASP.NET ve Web Araçları 2012.2'yi el ile de yükleyebilirsiniz. Web için Visual Studio 2012 veya Visual Studio Express 2012 yüklü olmalıdır. Ardından aşağıdaki talimatları kullanın: 

1. [Download Center'dan ASP.NET ve Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) yükleyiciindir.
2. İstendiğinde Çalıştır'ı tıklatın. Dosyayı daha sonra çalıştırmak için de kaydedebilirsiniz.
3. Güncellediğiniz Visual Studio sürümünü doğrulayın. Bunu güncellemek istediğiniz Visual Studio'yu başlatarak yapabilirsiniz. Ardından Yardım menüsü öğesini tıklatın.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Web&quot; için Microsoft &quot;Visual Studio 2012 hakkında menü öğesini görürseniz, Web [Geliştirici Araçları 2012.2 - Visual Studio Express 2012 web için](https://go.microsoft.com/fwlink/?LinkID=282228)indirin. Aksi takdirde [Web Geliştirici Araçları indir 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. İstendiğinde Çalıştır'ı tıklatın. Dosyayı daha sonra çalıştırmak için de kaydedebilirsiniz.

> [!NOTE]
> ASP.NET ve Web Tools 2012.2 sürümü SQL Server Veri Araçları içermez. SQL Server ve Windows Azure SQL Veritabanları, çevrimdışı proje destekli geliştirme, şema karşılaştırması ve gelişmiş veritabanı dağıtım özellikleri de dahil olmak üzere daha zengin bir veritabanı aracı kümesi sağlar. Daha fazla bilgi için veya SQL [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)Server Veri Araçları yüklemek için ziyaret edin.

<a id="_Documentation"></a>
## <a name="documentation"></a>Belgeler

Eğitimler ve ASP.NET ve Web Araçları 2012.2 hakkında diğer https://www.asp.net)bilgiler ASP.NET web sitesinden edinilebilir ( .

<a id="_Support"></a>
## <a name="support"></a>Destek

ASP.NET ve Web Araçları 2012.2 resmi olarak yayımlanır ve desteklenir. Normal destek kanalınızı kullanabilirsiniz. Ayrıca, ASP.NET topluluğunun üyelerinin sık[https://forums.asp.net/](https://forums.asp.net/)sık gayri resmi destek sağlayabilecekleri ASP.NET forumlarına da soru gönderebilirsiniz.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

ASP.NET ve Web Araçları 2012.2 Web için Visual Studio 2012 veya Visual Studio Express 2012 gerektirir.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET ve Web Araçlarında Yeni Özellikler 2012.2

Bu bölümde, ASP.NET ve Web Araçları 2012.2 sürümünde tanıtılan özellikler açıklanmaktadır.

<a id="_Tooling"></a>
### <a name="tooling"></a>Araçlar

- Sayfa Denetçisi 

    - Sayfa Denetçisi'nin sayfaya dinamik olarak eklenen öğeleri ilgili JavaScript koduna geri eşlemesine olanak tanıyan JavaScript seçim eşlemenliğini destekleyin.
    - CSS güncellemelerini gerçek zamanlı olarak görebilme özelliği.
    - Daha fazla bilgi için [Sayfa Denetçisi CSS Otomatik Eşitleme ve JavaScript Seçim Eşlemesi'ni](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)okuyun.
- Düzenleyici 

    - CoffeeScript, Bıyık, Gidon ve JsRender için sözdizimini vurgulamayı destekleyin.
    - HTML düzenleyicisi Knockout ciltleri için Intellisense sağlar.
    - DAHA AZ kullanarak dinamik CSS oluşturmayı sağlamak için daha az düzenleme ve derleyici desteği.
    - JSON'u .NET sınıfı olarak yapıştırın. JSON'u c# veya VB.NET kod dosyasına yapıştırmak için bu Özel Yapıştır komutunu kullanarak Visual Studio, JSON'dan çıkarılan .NET sınıflarını otomatik olarak oluşturur.
- Mobil Emülatör desteği, üçüncü taraf emülatörlerin VSIX olarak yüklenebileceği şekilde genişletilebilirlik kancaları ekler. Yüklü emülatörleri F5 açılır açılır durumda görünür, böylece geliştiriciler web sitelerini çeşitli mobil cihazlarda önizleyebilirler. [Visual Studio ile yeni BrowserStack entegrasyonu](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)Scott Hanselman günlüğü bu özellik hakkında daha fazla bilgi edinin.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web Yayıncılık

- Web sitesi projeleri artık Windows Azure Web Sitelerine yayımlama da dahil olmak üzere Web Uygulaması projeleri ile aynı yayımlama deneyimine sahiptir.
- Bir veya daha fazla dosya için seçici yayımlama &#8211; aşağıdaki eylemleri gerçekleştirebilirsiniz (Web Dağıtım bitiş noktasına yayımladıktan sonra): 

    - Seçili dosyaları yayımlayın.
    - Yerel bir dosya ile uzak dosya arasındaki farkı görün.
    - Uzak dosyayla yerel dosyayı güncelleştirin veya uzak dosyayı yerel dosyayla güncelleştirin.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC Şablonları

- Yeni Facebook Uygulaması şablonu, Facebook Canvas uygulamalarını yazmayı kolaylaştırır. Birkaç basit adımda, oturum açmış bir kullanıcıdan veri alan ve arkadaşlarıyla tümleştiren bir Facebook uygulaması oluşturabilirsiniz. Şablon, kimlik doğrulama, izinler, Facebook verilerine erişim ve daha fazlası dahil olmak üzere bir Facebook uygulaması nın oluşturulmasında yer alan tüm tesisatlarla ilgilenmek için yeni bir kütüphane içerir. Facebook Uygulama şablonu kullanma hakkında [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)daha fazla bilgi için bkz.
- Yeni bir Tek Sayfa Uygulama MVC şablonu geliştiriciler html 5, CSS 3 ve popüler Knockout ve jQuery JavaScript kitaplıkları kullanarak etkileşimli istemci tarafı web uygulamaları oluşturmak için izin verir, ASP.NET Web API üstüne. Şablon, yeniden bir sunucu API'si kullanan bir JavaScript HTML5 uygulaması oluşturmak için yaygın uygulamaları gösteren bir "todo" listesi uygulaması içerir. Daha fazla bilgi [https://www.asp.net/single-page-application](../../../single-page-application/index.md)edinebilirsiniz .
- Artık ASP.NET MVC Yeni Proje iletişim kutusuna yeni şablonlar ekleyen bir VSIX oluşturabilirsiniz. Nasıl yapılacağını buradan öğrenin:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- MVC proje şablonları &#8211; FixedDisplayModes paketi, MVC 4'teki bir hata için geçici çözüm içeren yeni 'FixedDisplayModes' NuGet paketini içerecek şekilde güncelleştirildi. Pakette yer alan düzeltme hakkında daha fazla bilgi[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)için, MVC ekibinden bu blog gönderisine bakın.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API'si

ASP.NET Web API birkaç yeni özellik ile geliştirilmiştir:

- ASP.NET Web API OData
- ASP.NET Web API İzleme
- ASP.NET Web API Yardım Sayfası

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData size herhangi bir veri kaynağı üzerinde zengin iş mantığı ile OData uç noktaları oluşturmak için gereken esneklik sağlar. ASP.NET Web API OData ile ortaya çıkarmak istediğiniz OData semantik miktarını denetlersiniz. ASP.NET Web API OData ASP.NET MVC 4 proje şablonları ile birlikte[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)ve nuget () de mevcuttur.

ASP.NET Web API OData şu anda aşağıdaki özellikleri destekler:

- [Sorgulanabilir] özniteliğini uygulayarak OData sorgusu semantiklerini etkinleştirin.
- OData sorgularını kolayca doğrulayın ve desteklenen sorgu seçenekleri, işleçler ve işlevler kümesini kısıtlayın.
- Parametre, sorgunun daha sonra doğrulanabilen ve IQueryable veya IEnumerable'a uygulanabilen soyut bir sözdizimi ağacı temsilini almak için doğrudan ODataQueryOptions'a bağlanır.
- [Sorgulanabilir] özniteliğinde sonuç sınırları belirterek hizmet odaklı sayfalama ve sonraki sayfa bağlantı oluşturmayı etkinleştirin.
- $inlinecount kullanarak eşleşen toplam kaynak sayısının sıralı bir sayısını isteyin.
- Null yayılımı kontrol edin.
- $filter'daki tüm operatörler.
- Bir varlık veri modelini sözleşmeye göre çıkarveya bir modeli Varlık Çerçeve Kodu-İlk'e benzer şekilde açıkça özelleştirin.
- EntitySetController'dan türeerek varlık kümelerini açığa çıkar.
- Navigasyon özelliklerini açığa çıkarmak, bağlantıları işlemek ve OData eylemlerini uygulamak için basit, özelleştirilebilir kurallar.
- MapODataRoute uzantı yöntemini kullanarak basitleştirilmiş yönlendirme.
- Birden çok EDM modelini teşhir ederek sürüm oluşturma desteği.
- Web API'nız için istemciler (.NET, Windows Phone, Windows Mağazası, vb.) oluşturabilmeniz için hizmet belgesini ve $metadata ortaya çıkar.
- OData Atom, JSON ve JSON ayrıntılı biçimleri için destek.
- Varlıkları oluşturun, güncelleyin, kısmen güncelleştirin (PATCH) ve silin.
- Varlıklar arasındaki ilişkileri sorgula ve işleme.
- Rotalarınıza kabloyla bağlanan ilişki bağlantıları oluşturun.
- Karmaşık türleri.
- Varlık Türü Devralma.
- Toplama özellikleri.
- Numaralandırmalar.
- OData eylemleri.
- WCF Veri Hizmetleri, yani ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)) ile aynı temel üzerine inşa edilmiştir.

ASP.NET Web API OData hakkında [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)daha fazla bilgi için bkz.

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API İzleme

ASP.NET Web API İzleme, web API'lerinizdeki verilerin izlenmesini .NET İzleme ile tümleştirir. Artık Web API proje şablonunda varsayılan olarak etkinleştirilir. Web API'lerinizin verilerinin izlenmesi Çıktı penceresine gönderilir ve IntelliTrace aracılığıyla kullanıma sunulmuştur. ASP.NET Web API İzleme, Windows Azure'da barındırıldığında Windows [Azure'da barındırılan](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)Web API'nizle ilgili bilgileri Windows Azure Tanılama ile tümleştirme yoluyla izlemenize olanak tanır. Ayrıca, ASP.NET Web API İzleme NuGet paketini kullanarak herhangi bir uygulamada Web[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)API İzlemesini ASP.NET web API İzlemesini yükleyebilir ve etkinleştirebilirsiniz.

Web API İzleme ASP.NET yapılandırma ve kullanma [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)hakkında daha fazla bilgi için bkz.

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API Yardım Sayfası

ASP.NET Web API Yardım Sayfası artık varsayılan olarak Web API proje şablonuna dahildir. ASP.NET Web API Yardım Sayfası, HTTP uç noktaları, desteklenen HTTP yöntemleri, parametreler ve örnek istek ve yanıt iletisi yüklerini içeren web API'leri için otomatik olarak belgeler oluşturur. Belgeler, kodunuzdaki yorumlardan otomatik olarak çıkarılır. Ayrıca ASP.NET Web API Yardım Sayfası NuGet paketini kullanarak herhangi bir uygulamaya[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)ASP.NET Web API Yardım Sayfası ekleyebilirsiniz .

Web API Yardım Sayfasının kurulumu ve ASP.NET özellemi hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR, varsa WebSockets'i kullanarak ASP.NET uygulamanıza gerçek zamanlı web özellikleri eklemeyi ve olmadığında otomatik olarak diğer tekniklere geri dönmeyi kolaylaştırır.

SignalR ASP.NET kullanımı hakkında [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)daha fazla bilgi için bkz.

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Dostu URL'ler

ASP.NET FriendlyURLs web formları geliştiricileri için çok kolay temiz görünümlü URL'ler (.aspx uzantısı olmadan) oluşturmak için yapar. Çok az veya hiç yapılandırma gerektirir ve mevcut ASP.NET v4.0 uygulamaları ile kullanılabilir. FriendlyURLs özelliği, geliştiricilerin masaüstü ve mobil görünümler arasında geçişi destekleyerek uygulamalarına mobil destek eklemelerini de kolaylaştırır.

ASP.NET Friendly URL'leri yükleme ve kullanma [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)hakkında daha fazla bilgi için bkz.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen Sorunlar ve Son Dakika Değişiklikleri

Bu bölümde, ASP.NET ve Web Araçları 2012.2 sürümünde yer alan bilinen sorunları ve kesme değişiklikleri açıklanmaktadır.

### <a name="installation-issues"></a>Yükleme Sorunları

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Out of order Visual Studio 2012 yükler

ASP.NET ve Web Tools 2012.2'yi yükledikten sonra Visual Studio 2012'nin ek bir SKU'su nun yüklenmesi için onarım işlemi gerekir. Aşağıdaki sırayı göz önünde bulundurun:

1. Web için Visual Studio 2012 Express yükle
2. ASP.NET ve Web Araçları 2012.2'yi yükleyin
3. Visual Studio 2012 Profesyonel, Premium veya Ultimate yükleyin

Adım 2 yalnızca Web için Express güncelleştirmeleri yüklemeyle sonuçlanır. Adım 3 sırasında yüklenen ek SKU'nun, yüklenen son SKU güncelleştirmelerini yüklemek için ASP.NET ve Web Araçları 2012.2'yi onarmanız gereken güncelleştirmeyi içerdiğinden emin olmak için. Bu, Adım 1 ve 3'teki SNU'lar tersine çevrildiğinde de geçerlidir.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio açıldığında Microsoft ASP.NET ve Web Araçları 2012.2'yi yükleme

Microsoft ASP.NET ve Web Tools 2012.2'nin yüklenmesi sırasında VS açıksa, Visual Studio kötü bir duruma baçabilir. Kullanıcıların yüklemeişlemine geçmeden önce Visual Studio'nun tüm örneklerini kapatmaları önerilir.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Yüklemenin ortasında ASP.NET ve Web Araçları 2012.2 kurulumunu iptal etme

yüklemenin ortasında ASP.NET ve Web Araçları 2012.2 kurulumiptal kötü bir durumda Visual Studio bırakacaktır. Bu sorunu gidermek için aşağıdaki adımları izleyin: 

- Programları Kaldır Ekle'ye Git
- Varsa Microsoft ASP.NET ve Web Araçları 2012.2'yi kaldırın.
- Microsoft ASP.NET ve Web Araçları 2012.2'yi yeniden yükleme

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET ve Web Araçları 2012.2'yi yükledikten sonra ASP.NET MVC 4 şablonları ve Razor v2 Web Sitesi şablonları eksik

ASP.NET ve Web Araçları 2012.2'nin yüklenmesi, Visual Studio 2012'deki ASP.NET MVC 4 ve Razor v2 Web Sitesi şablonlarının tümünün yüklenmesini sağlar.

Geçici çözüm, MVC 4 ve Razor v2 Web Sitesi şablonlarını ASP.NET yeniden yüklemek için Visual Studio 2012 yüklemenizi onarmaktır.

### <a name="tooling-issues"></a>Araç Sorunları

#### <a name="nuget-error-reported-during-project-creation"></a>Proje oluşturma sırasında bildirilen NuGet hatası

ASP.NET ve Web Araçları 2012.2'yi yükledikten sonra bir MVC 4 projesi oluştururken aşağıdaki hatayı görebilirsiniz

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET ve Web Tools 2012.2 gemi NuGet 2.1 ve Visual Studio 2012 uzantısı yükseltecektir. Bazı durumlarda, VSIX yükleyicidoğru VSIX güncelleştirmek için başarısız olur. Aşağıdaki adımlar, bu sorunu gidermenize olanak sağlar:

1. Visual Studio 2012'yi Yönetici Olarak Başlat
2. Araçlar-&gt;Uzantılar ve Güncellemeler'e gidin ve NuGet'i kaldırın.
3. Visual Studio’yu kapatın
4. ASP.NET ve Web Araçları 2012.2 yükleme klasörüne gidin:

    1. Visual Studio 2012 için: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**
    2. Web için Visual Studio 2012 Express için: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 Web için**
5. NuGet'i yeniden yüklemek için NuGet.Tools.vsix'e çift tıklayın

### <a name="web-api-issues"></a>Web API Sorunları

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filter ve DateTime literatüründeki sorunları ayrıştma

OData URI parser kısmi datetime literals düzgün ayrıştırmak için başarısız olur. Örneğin, $filter=başlangıç eq datetime'2012-12-31T12:00' düzgün ayrışma başarısız olur. Bir geçici çözüm tam edebi kullanmaktır, $filter=başlangıç eq datetime'2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData, büyük/küçük harf duyarlı özellik adlarını desteklemez.

OData, OData sorgularında ve odata yolunda ki büyük/küçük harf duyarlı özellik adlarını desteklemez. Bkz. çalışma öğeleri:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Kullanıcılar javascript istemci tarafında ve sunucu tarafında farklı kasa varsa, büyük olasılıkla bu sorunla karşılaşacak. Bu sorun odata protokolünde tasarım gereğidir. Ancak, birçok kullanıcı bu sorunu bildirir. Bu geçici çözüm için, kullanıcıların url'deki servis taleplerini düzeltmeleri gerekir.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Varsayılan OData yönlendirme kuralları, gezinme özelliğindeki POST/PUT'u desteklemez.

Varsayılan OData yönlendirme kuralları, gezinme özelliğindeki POST/PUT'u desteklemez. Bkz. [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)iş öğesi. Varsayılan sözleşmelerde sık kullanılan bu kuralı kaçırıyoruz.

Bu geçici çözüm için, kullanıcıların bunu desteklemek için yeni yönlendirme kuralını genişletmeleri gerekir.

### <a name="facebook-template-issues"></a>Facebook Şablon Sorunları

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook Uygulama şablonu yalnızca .NET 4.5 kullanarak çalışır

ASP.NET MVC 4'teki Facebook Uygulama şablonunu görmek için Yeni Proje iletişim kutusundaki çerçeve açılır listesinde .NET 4.5'i seçmeniz gerekir.

#### <a name="real-time-update-controller"></a>Gerçek zamanlı Güncelleme Denetleyicisi

Facebook Uygulama şablonu, kullanıcının Facebook'tan gelen gerçek zamanlı güncellemeleri işlemek için kolayca bir Web API Denetleyicisi oluşturmasına olanak tanır. Geliştirme makineniz NAT'nin arkasındaysa, Denetleyiciniz daha fazla ağ yapılandırması olmadan çalışmayabilir. Ayrıntılar için buraya bakın:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Sorgu dize değerleri Facebook OAuth parametreleri ile çakışması

Aşağıdaki alanlar, Facebook OAuth iletişim kutusunun geri arama URL'si ile çakışıyor. Kod, hata, hata\_açıklaması, hata\_nedeni: aşağıdaki adlarla kendi sorgu dize değerleri eklemeyin.

#### <a name="using-page-inspector-with-facebook-template"></a>Facebook Şablonuyla Sayfa Denetçisi Kullanma

Visual Studio 2012'deki Sayfa Denetçisi özelliğini, Facebook Uygulamanızı hata ayıklarken kullanamazsınız. Sayfa Denetçisi şu anda iframe'leri desteklemiyor.

### <a name="single-page-application-template-issues"></a>Tek Sayfauygulama Şablonu Sorunları

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/Knockout 2.2.1 güncellemesi ile varsayılan MVC SPA projesini çalıştırırken, yeni todo öğesi düzenlemesi enter focus olayı düzgün şekilde işlenmez.

JQuery 1.9/Knockout 2.2.1 güncellemesi ile, varsayılan MVC SPA projesini çalıştırırken, yeni todo öğesi düzenlemesi girin artık yeni todo öğesini todo listesine girdikten sonra yeni todo öğesi düzenlemesi kutusuna odaklanmayın.

Başvuruyu [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)geçici olarak çözmek ve aşağıdaki örnek koda benzer düzeltmeler yapmak için:

Dosya todo.model.js  
 fonksiyon todolist(veri), aşağıdakileri ekleyin:  
 **self.isSelected = ko.observable(yanlış);**

fonksiyon todoList.prototype.addTodo, aşağıdaki karartılmış metin ekleyin:  
 **self.isSelected(doğru);**  
 self.newTodoTitle(&quot;&quot;);

Dosya index.cshtml, aşağıdaki karartılmış metin ekleyin:  
 &lt;form data-bind=&quot;gönderin: addTodo&quot;&gt;  
 &lt;&quot;input class= addTodo&quot; type=&quot;text&quot; &quot;data-bind= value: newTodoTitle, yer tutucu: 'Buraya eklemek için yazın', blurOnEnter: true, **hasfocus: isSelected**, olay: { blur: addTodo }&quot; /&gt;  
 &lt;/form&gt;
