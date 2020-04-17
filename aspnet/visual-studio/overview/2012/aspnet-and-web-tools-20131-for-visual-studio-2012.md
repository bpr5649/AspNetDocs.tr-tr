---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET ve Web Araçları için Yayın Notları 2013.1 Visual Studio 2012 | Microsoft Dokümanlar
author: rick-anderson
description: Bu belge, Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1 sürümü açıklanmaktadır.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543580"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 için ASP.NET and Web Tools 2013.1 Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

> Bu belge, Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1 sürümü açıklanmaktadır.

## <a name="contents"></a>İçindekiler

- [Kurulum Notları](#install)
- [Yazılım Gereksinimleri](#requirements)
- Visual Studio 2012 için ASP.NET ve Web Araçlarında Yeni Özellikler 2013.1

    - [Bootstrap](#bootstrap)
    - [Şablonlar](#templates)

        - [ASP.NET MVC 5 şablonu](#mvc5template)
        - [ASP.NET Web API 2 şablonu](#apitemplate)
        - [Öğe Şablonları](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET İskele](#scaffold)
    - [Razor Editörü](#razor)
    - [NuGet 2.7](#nuget)
- Bilinen Sorunlar ve Son Dakika Değişiklikleri

    - [ASP.NET İskele](#issuescaffolding)

        - [MVC ve Web API İskele - HTTP 404, Bulunamadı hatası](#404issue)
        - [Web için Visual Studio Express 2012, iskeleye bağlı bir öğe ekledikten sonra çalışmayı durdurur](#expressissue)
    - [ASP.NET Jilet 3](#issuerazor)

        - [Cshtml dosyasInI Gözat veya F5 ile görüntülemek sunucu hatasına neden olur](#browseissue)
        - [Url Yeniden Yazma ve Tilde(~)](#rewriteissue)
    - [Şablonlar](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Kurulum Notları

[Yükle](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1.

<a id="requirements"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

Web için Visual Studio 2012 veya Visual Studio Express 2012'ye sahip olmalısınız.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 için ASP.NET ve Web Araçlarında Yeni Özellikler 2013.1

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

MVC 5 denetleyicilerini ve görünümlerini iskeleye aldığınızda, görünümlerin biçimlendirmesi [Bootstrap'ı](http://getbootstrap.com/)kullanır.

<a id="templates"></a>
### <a name="templates"></a>Şablonlar

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 şablonu

Yeni bir MVC 5 şablonu ekledik. En son MVC 5 NuGet paketlerine atıfta bulunur ve denetleyiciler ve görünümler eklemek için iskeleyi kullanabilirsiniz.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 şablonu

Yeni bir Web API 2 şablonu ekledik. En son Web API 2 NuGet paketlerine başvurur ve denetleyiciler ve görünümler eklemek için iskeleyi kullanabilirsiniz.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Öğe Şablonları

MVC 5 görünümleri, Web Sayfaları (Razor 3) ve Web API 2 denetleyicileri için yeni öğe şablonları ekledik. Yeni öğeler eklerken ilgili NuGet paketlerini projeye yüklerler.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Varlık Çerçevesi'ni kullanarak bir MVC veya Web API denetleyicisi satın aldığınızda, Framework 6'yı kullanırız. Varlık Çerçevesi hakkında daha fazla bilgi için [Entity Framework Version History'ye](https://msdn.com/data/jj574253)bakın.

Ayrıca Visual Studio 2012 için Entity Framework 6 Tools'u indirip yükleyebilirsiniz. Varlık [Çerçevesini Al'a](https://msdn.com/data/ee712906#tooling)bakın.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET İskele

ASP.NET İskele, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Projenize bir veri modeliyle etkileşimde bulunarak ortak kod eklemeyi kolaylaştırır.

Visual Studio'nun önceki sürümlerinde, iskele ASP.NET MVC projeleri ile sınırlıydı. Bu güncelleştirmeyle, artık Web Formlar da dahil olmak üzere herhangi bir ASP.NET projesi için iskele kullanabilirsiniz. Bu güncelleştirme, bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Formları ile iskeleyi kullanmaya devam edebilirsiniz. Web Formları için sayfa oluşturma desteği gelecekteki bir güncelleştirmede eklenir.

İskele kullanırken, gerekli tüm bağımlılıkların projeye yüklenmesini sağlıyoruz. Örneğin, bir web formları projesi ASP.NETyle başlayıp web API Denetleyicisi eklemek için iskele kullanırsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.

Bir Web Forms projesine MVC iskelesi eklemek için **Yeni İskele Öğesi** ekleyin ve iletişim penceresinde **MVC 5 Bağımlılıkları'nı** seçin. İskele MVC için iki seçenek vardır; Minimal ve Tam. Minimal'i seçerseniz, projenize yalnızca ASP.NET MVC için NuGet paketleri ve referansları eklenir. Tam seçeneği seçerseniz, Bir MVC projesi için gerekli içerik dosyalarının yanı sıra Minimal bağımlılıklar eklenir.

İskele async denetleyicileri desteği, Entity Framework 6'nın yeni async özelliklerini kullanır.

Daha fazla bilgi ve öğreticiler için, [ASP.NET İskele Genel bakınız.](../2013/aspnet-scaffolding-overview.md) Bu öğreticiler Visual Studio 2013 ile iskele göstermek, ama aynı zamanda Visual Studio 2012 için ASP.NET ve Web Tools 2013.1 için de geçerlidir.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor Editörü

Bu güncelleme ile Visual Studio 2012 artık Razor 3 araç/düzenlemeyi destekliyor.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7, [NuGet 2.7 Sürüm Notları'nda](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir yeni özellik kümesini içerir.

NuGet'in bu sürümü, kullanıcıların NuGet'in eksik paketleri geri yüklemesine açıkça izin verme gereğini ortadan kaldırır. NuGet 2.7'yi yüklerken, kullanıcılar eksik paketleri otomatik olarak geri yüklemeyi dolaylı olarak kabul eder. Kullanıcılar Visual Studio'daki NuGet ayarları aracılığıyla paket geri yüklemesini açıkça devre dışı edebilirler. Bu değişiklik, paket geri yüklemenin nasıl çalıştığını basitleştirir.

## <a name="known-issues-and-breaking-changes"></a>Bilinen Sorunlar ve Son Dakika Değişiklikleri

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET İskele

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC ve Web API İskele - HTTP 404, Bulunamadı hatası

Bir projeye iskeleye ayrılmış bir öğe eklerken bir hatayla karşılaşırsanız, projenizin tutarsız bir durumda kalması mümkündür. İskele olarak yapılan değişikliklerin bazıları geri alınır, ancak yüklenen NuGet paketleri gibi diğer değişiklikler geri alınmaz. Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar iskeledeki öğelerde gezinirken bir HTTP 404 hatası alır.

MVC için bu hatayı düzeltmek için yeni bir iskele öğesi ekleyin ve MVC 5 Bağımlılıkları 'nı (Minimal veya Tam) seçin. Bu işlem, projenize gerekli tüm değişiklikleri ekler.

Web API için bu hatayı düzeltmek için:

1. Projenize aşağıdaki WebApiConfig sınıfını ekleyin.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Global.asax'ta Uygulama\_Başlangıç yönteminde WebApiConfig.Register'ı aşağıdaki şekilde yapılandırın:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Web için Visual Studio Express 2012, iskeleye bağlı bir öğe ekledikten sonra çalışmayı durdurur

Web için Visual Studio Express 2012, Entity Framework ile (Entity Framework kullanarak web API 2 Controller gibi) İskeleli öğe ekledikten sonra çalışmayı durdurursa, Visual Studio Express'in System.Web.Extensions'a bağlı bir derlemenin yerel görüntüsünü yüklememesi mümkündür.

Bu sorunu gidermek için Visual Studio Express'i System.Web.Extensions'ın MSIL görüntüsüyle çalışacak şekilde yapılandırın:

1. Yönetici modunda Komut İstem'i açın.
2. %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE veya %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (64 bit Windows için) gidin.
3. Bir metin editöründe VWDExpress.exe.config'i açın.
4. Yapılandırma&lt;&gt; &lt;&gt;/çalışma zamanı öğesinin altına aşağıdaki satırı ekleyin:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Web için Visual Studio Express 2012'yi yeniden başlatın.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Jilet 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Cshtml dosyasInI Gözat veya F5 ile görüntülemek sunucu hatasına neden olur

Visual Studio 2012'de bir MVC 5 projesi oluşturduğunuzda (veya Visual Studio 2012'de açılan bir MVC 5 projesi 2013'te oluşturulduğunda) ve Gözat ile veya F5 kullanarak bir cshtml dosyasını görüntülemeye çalıştığınızda, bir hata alırsınız - **Sunucu Hatası '/' Uygulamasında**. Sunucu gezinmek için çalışır`http://localhost:XXXX/Views/../XXXX.cshtml`

Bu sorunu gidermek için, projenizdeki **Başlangıç Eylemi** ayarını **Belirli Sayfa**olarak değiştirin. Sayfa için bir değer sağlamanız gerekmez.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Bu değişikliği yaptıktan sonra, F5'i seçerek uygulamanızın köküne doğru iletin (`http://localhost:XXXX`). Bu davranış, **Geçerli Sayfa** ayarının açık sayfayı başlattığı Visual Studio 2013'teki MVC 5 projelerinin davranışıyla aynı değildir.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url Yeniden Yazma ve Tilde(~)

ASP.NET Razor 3 veya ASP.NET MVC 5'e yükselttikten sonra, URL yeniden yazmalarını kullanıyorsanız tilde(~) gösterimi artık doğru çalışmayabilir. URL &lt;yeniden yazma, A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;gibi HTML öğelerindeki tilde(~) gösterimini etkiler ve sonuç olarak tilde artık kök diziniyle eşlenmez.

Örneğin, **asp.net** **için asp.net/content** isteklerini yeniden yazarsanız, A &lt;href="~/content/"/&gt; adresindeki href özniteliği **/**/ **içerik/içerik/** yerine giderir. Bu değişikliği bastırmak için, **IIS\_WasUrlRewritten** bağlamını her Web Sayfasında veya Global.asax'taki **Application\_BeginRequest'de** false olarak ayarlayabilirsiniz.

<a id="templateissue"></a>
### <a name="templates"></a>Şablonlar

Visual Studio 2012 ile Windows 8.1 veya Windows Server 2012 R2'de ASP.NET MVC projeleri oluşturduğunuzda, Visual Studio "ASP.NET 4,5 için Web [url]'yi yapılandırma" belirten bir hata iletisi görüntüler.

![yapılandırma hatası](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Visual Studio 2012, Windows'un bu sürümlerine yüklendiğinde ASP.NET 4.5 özelliğini etkinleştirmediği için bu hatayı görürsünüz. 4,5 ASP.NET etkinleştirmek için Windows özelliklerini aç veya kapat'ta açıklanan adımları [gerçekleştirin.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)

![Windows özelliklerini açma veya kapatma](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Alternatif olarak, komut satırı üzerinden 4,5 ASP.NET etkinleştirebilirsiniz.

1. Yönetici modunda Komut İstem'i açın.
2. 4,5 ASP.NET sağlamak için aşağıdaki komutu çalıştırın.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
