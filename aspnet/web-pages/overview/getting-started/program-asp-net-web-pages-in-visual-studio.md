---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programlama ASP.NET Web Sayfaları (Razor) Visual Studio kullanma | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu ek, Web Sayfalarını Jilet sözdizimi yle program ASP.NETlamak için Visual Studio 2010 veya Visual Web Developer 2010 Express'i nasıl kullanabileceğinizi açıklar.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542904"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Programlama ASP.NET Web Sayfaları (Razor) Visual Studio kullanma

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> Bu makalede, Web Sayfaları (Razor) web sitelerini ASP.NET programlamak için Visual Studio veya Visual Web Developer Express'i nasıl kullanabileceğiniz açıklanmaktadır.
>
> Öğrenecekleriniz
>
> - Visual Studio sürümünüzdeki ASP.NET Web Sayfaları ile çalışmak için yüklemeniz gerekenler (varsa)
> - Visual Web Developer 2010 Express'e ASP.NET Web Sayfaları için destek nasıl eklenir?
> - IntelliSense ve hata ayıklama dahil olmak üzere ASP.NET Razor sayfaları ile çalışmak için Visual Studio özellikleri nasıl kullanılır.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - ASP.NET Web Sayfaları (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Bu öğretici ayrıca ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010 ve WebMatrix 2 ile birlikte çalışır.

WebMatrix veya diğer birçok kod düzenleyicisini kullanarak Web sayfalarını Razor sözdizimi ile ASP.NET programlayabilirsiniz. Ayrıca, birçok uygulama türü (yalnızca web siteleri değil) oluşturmak için güçlü bir araç kümesi sağlayan tam özellikli tümleşik bir geliştirme ortamı (IDE) olan Microsoft Visual Studio'yu da kullanabilirsiniz. ASP.NET Razor sayfaları ile çalışmak için [Visual Studio 2017'yi](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)kullanabilirsiniz.

Visual Studio'nun ASP.NET Razor web sayfaları yla programlama için sağladığı iki özellikle kullanışlı özellik şunlardır:

- *IntelliSense*. Visual Studio'da yerleşik Olan IntelliSense özelliği, WebMatrix'teki IntelliSense'den daha kapsamlıdır.
- *Hata ayıklama.* Hata ayıklayıcı, bir programı çalışırken durdurarak, değişkenleri inceleyerek ve kod satırına satır satır adım atarak kodunuzu sorun gidermenizi sağlar.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>ASP.NET Web Sayfalarının Farklı Sürümleriyle Visual Studio'nun Kullanılması

Visual Studio 2017'de ASP.NET web uygulamaları geliştirmek için **ASP.NET ve web geliştirme** iş yükünü yükleyin.

Visual Studio 2012 ve Visual Studio 2013 ASP.NET Web Sayfaları desteğini içerir. (Visual Studio'yu yüklediğinizde web sayfalarını ASP.NET desteklemek için gereken paketler yüklenir.)

Visual Studio 2010, web sayfalarını ASP.NET için varsayılan olarak destek içermez. Visual Studio 2010 ile web sayfalarını ASP.NET kullanmak için ASP.NET MVC paketini yüklemeniz gerekir. Web Sayfalarını 2ASP.NET almak için MVC 4 ASP.NET yüklersiniz.

Aşağıdaki tablo, Visual Studio'nun farklı sürümlerinde ASP.NET Web Sayfaları desteğini özetleyilmiştir.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web Sayfaları 2** | MVC 4 ASP.NET yükleyin | (Dahil) | (Dahil) |
| **ASP.NET Web Sayfaları 3** |  | NuGet ile Web Sayfalarını 3 ASP.NET güncelleme | (Dahil) |

Visual Studio 2010 ile çalışmak için Visual [Studio 2010'da ASP.NET Web Sayfaları için Destek Yükleme'ye](#vs2010support)bakın.

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix'ten Visual Studio'nun başlatılması

WebMatrix'te bir proje başlattıysanız ve Visual Studio'ya geçmek istiyorsanız, WebMatrix projeyi Visual Studio'da kolayca açmak için bir düğme sağlar. Bu düğmenin etkin olabilmesi için bilgisayarınızda Visual Studio yüklü olmalıdır. Aşağıdaki resimde WebMatrix'teki düğme gösterilmektedir.

![Görsel Stüdyo'da başlat](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Düğmeyi tıklattığınızda, proje Visual Studio'da açılır. WebMatrix ve Visual Studio arasında herhangi bir sorun olmadan geçiş yapabilirsiniz. Diğer ortamda herhangi bir dosya değiştiyse ve en son değişiklikleri almak için yeniden yüklenmesi gerekiyorsa size bildirilir.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio'da ASP.NET Jilet Sitesi Oluşturma

Visual Studio'da ASP.NET bir Razor web sitesi oluşturmak için:

1. Visual Studio'yu açın.
2. **Dosya** menüsünde **Yeni Web Sitesi'ni**tıklatın.

    ![yeni web sitesi oluşturmak](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. Yeni **Web Sitesi** iletişim kutusunda kullanılacak dili (Visual C# veya Visual Basic) seçin.
4. web **sitesi (Razor)** şablonu ASP.NET seçin.

    ![jilet sitesi](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **Tamam**'a tıklayın.

Yeni projeniz var ve başlamanıza yardımcı olacak bazı varsayılan web sayfalarıyla doldurulur.

### <a name="using-intellisense"></a>IntelliSense Kullanma

Artık bir site oluşturduğunuza göre, IntelliSense'in Visual Studio'da nasıl çalıştığını görebilirsiniz.

1. Oluşturduğunuz web sitesinde *Varsayılan.cshtml* sayfasını açın.
2. Sayfadaki `<h3>` etiketlerden sonra `@ServerInfo.` ,(nokta dahil) yazın. IntelliSense'in, `ServerInfo` yardımcıiçin kullanılabilir yöntemleri açılır listede nasıl görüntülenebildiğini öğrenin.

    ![ıntellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Listeden `GetHtml` yöntemi seçin ve sonra Enter tuşuna basın. IntelliSense yöntemi otomatik olarak doldurur. (C#'daki herhangi bir yöntemde `()` olduğu gibi, yöntemden sonra karakter eklemeniz gerekir.) `GetHtml` Yöntem için tamamlanan kod aşağıdaki örnek gibi görünür:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Sayfayı çalıştırmak için Ctrl+F5 tuşuna basın. Bir tarayıcıda görüntülendiğinde sayfa aşağıdaki gibidir:

    ![tarayıcıda varsayılan sayfa](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Tarayıcıyı kapatın.

### <a name="using-the-debugger"></a>Hata Ayıklama'yı kullanma

1. *Default.cshtml* sayfasının üst kısmında, ile başlayan `Page.Title`satırdan sonra, aşağıdaki kod satırını ekleyin:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. Kodun solundaki düzenleyicinin gri kenar boşluğunda, *bir kesme noktası*eklemek için bu yeni satırın yanındaki niyazda bulunun. Kesme noktası, hata ayıklayana programı o noktada çalıştırmayı durdurmasını söyleyen bir işaretçidir, böylece neler olduğunu görebilirsiniz.

    ![kesme noktasını ayarlama](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Aramayı yönteme `ServerInfo.GetHtml` kaldırın ve yerine `@myTime` değişkene bir çağrı ekleyin. Bu çağrı, yeni kod satırı tarafından döndürülen geçerli saat değerini görüntüler.
4. Sayfayı hata ayıklamada çalıştırmak için F5 tuşuna basın. Sayfa ayarladığınız kesme noktasında durur. Aşağıdaki resim, sayfanın yazıcıda kesme noktası (sarı renkte) ile nasıl göründüğünü gösterir.

    ![hata ayıklama kesme noktası](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Hata Ayıklama araç çubuğunda, bir sonraki kod satırını çalıştırmak için **Adım adım** düğmesini (veya F11 tuşuna basın) tıklatın. Bu düğmeyi her tıklattığınızda, yürütmeyi bir sonraki kod satırına ilerletin.

    ![Düğmeye bas](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Fare işaretçinizi `myTime` üzerinde tutarak veya **Yerel Halk** ve **Çağrı Yığını** pencerelerinde görüntülenen değerleri inceleyerek değişkenin değerini inceleyin. Visual Studio değişkenin değerini görüntüler.

    ![zaman değerini göster](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Değişkeni incelemeyi ve kodu aşmayı bitirdiğinizde, her satırda durmadan sayfayı çalıştırmaya devam etmek için F5 tuşuna basın. Tüm kodu niçin tamamlamayı tamamladığınızda, tarayıcı sayfayı görüntüler.

Hata ayıklama ve Visual Studio'da kod ayıklama hakkında daha fazla bilgi edinmek [için, Visual Web Developer'da Web Sayfalarını](https://msdn.microsoft.com/library/z9e7w6cs.aspx)Hata Ayıklama bölümüne bakın.

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Visual Studio ile ASP.NET MVC projelerinde Razor kullanma

Razor sözdizimi de ASP.NET MVC projelerinde yaygın olarak kullanılmaktadır. MVC, dinamik web siteleri oluşturmanın güçlü, desen tabanlı bir yoludur. ASP.NET Web Sayfaları sitenizin bakımı zorlaşırsa, siteyi ASP.NET bir MVC uygulamasına dönüştürmeyi düşünebilirsiniz. Bir MVC uygulaması oluşturma örneği için, [ASP.NET MVC 5 ile Başlarken'e](../../../mvc/overview/getting-started/introduction/getting-started.md)bakın.

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010'da ASP.NET Web Sayfaları için Destek Yükleme

Bu bölümde Visual Web Developer Express 2010 ve Visual Studio için ASP.NET Web Sayfaları Araçları nasıl yüklenir gösterilmektedir.

1. Web Platformu Yükleyici'niz zaten yoksa, aşağıdaki URL'den indirin:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Web Platform Yükleyicisini çalıştırın.
3. **Ürünler** sekmesini tıklatın.

    ![WebPI Ürünleri sekmesi](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. **MVC 4 ASP.NET** arayın (ASP.NET Web Sayfaları 2 için) ve sonra **Ekle'yi**tıklatın. Bu ürünler ASP.NET Razor web siteleri oluşturmak için Visual Studio araçları içerir.

    ![WebPi yükleme seçenekleri](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Yüklemeyi tamamlamak için **Yükle'yi** tıklatın.
