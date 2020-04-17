---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: IIS (VB) Farklı Sürümleri ile ASP.NET MVC kullanma | Microsoft Dokümanlar
author: rick-anderson
description: Bu eğitimde, Internet Bilgi Hizmetleri'nin farklı sürümleriyle ASP.NET MVC ve URL Yönlendirme'yi nasıl kullanacağınızı öğreneceksiniz. Farklı stratejiler öğreniyorsunuz...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542007"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>ASP.NET MVC’yi Farklı IIS Sürümleriyle Kullanma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Bu eğitimde, Internet Bilgi Hizmetleri'nin farklı sürümleriyle ASP.NET MVC ve URL Yönlendirme'yi nasıl kullanacağınızı öğreneceksiniz. IIS 7.0 (klasik mod), IIS 6.0 ve IIS'nin önceki sürümleriyle ASP.NET MVC'yi kullanmak için farklı stratejiler öğrenirsiniz.

ASP.NET MVC çerçevesi, tarayıcı isteklerini denetleyici eylemlere yönlendirmek için yönlendirme ASP.NET yönlendirmesine bağlıdır. yönlendirmeASP.NET yararlanmak için web sunucunuzda ek yapılandırma adımları gerçekleştirmeniz gerekebilir. Her şey Internet Information Services (IIS) sürümüne ve uygulamanız için istek işleme moduna bağlıdır.

IIS'nin farklı sürümlerinin bir özeti aşağıda veda edebilirsiniz:

- IIS 7.0 (entegre mod) - ASP.NET Yönlendirme'yi kullanmak için özel bir yapılandırma gerekmez.
- IIS 7.0 (klasik mod) - Yönlendirme ASP.NET kullanmak için özel yapılandırma yapmanız gerekir.
- IIS 6.0 veya altında - ASP.NET Yönlendirme'yi kullanmak için özel yapılandırma yapmanız gerekir.

IIS en son sürümü sürüm 7.5 (Win7) olduğunu. IIS 7 IIS Windows Server 2008 VE VISTA/SP1 ve üstü ile birlikte verilir. Ayrıca IIS 7.0'ı Home Basic dışında Vista işletim sisteminin [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)herhangi bir sürümüne yükleyebilirsiniz (bkz.

IIS 7.0, istekleri işlemek için iki modu destekler. Tümleşik modu veya klasik modu kullanabilirsiniz. Entegre modunda IIS 7.0 kullanırken özel yapılandırma adımları gerçekleştirmeniz gerekmez. Ancak, iis 7.0'ı klasik modda kullanırken ek yapılandırma gerçekleştirmeniz gerekir.

Microsoft Windows Server 2003 IIS 6.0 içerir. Windows Server 2003 işletim sistemini kullanırken IIS 6.0'ı IIS 7.0'a yükseltemezsiniz. IIS 6.0 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

Microsoft Windows XP Professional, IIS 5.1 içerir. IIS 5.1 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

Son olarak, Microsoft Windows 2000 ve Microsoft Windows 2000 Professional IIS 5.0 içerir. IIS 5.0 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

## <a name="integrated-versus-classic-mode"></a>Entegre karşı Klasik Mod

IIS 7.0, iki farklı istek işleme modunu kullanarak istekleri işleyebilir: tümleşik ve klasik. Tümleşik mod daha iyi performans ve daha fazla özellik sağlar. Klasik mod, IIS'nin önceki sürümleriyle geriye dönük uyumluluk için dahildir.

İstek işleme modu uygulama havuzu tarafından belirlenir. Uygulamayla ilişkili uygulama havuzunu belirleyerek belirli bir web uygulaması tarafından hangi işlem modunun kullanıldığını belirleyebilirsiniz. Şu adımları uygulayın:

1. İnternet Bilgi Hizmetleri Yöneticisi'ni Başlatın
2. Bağlantılar penceresinde, bir uygulama seçin
3. Eylemler penceresinde, Uygulamayı Edit iletişim kutusunu açmak için **Temel Ayarlar** bağlantısını tıklatın (Bkz. Şekil 1)
4. Seçilen Uygulama havuzuna dikkat edin.

Varsayılan olarak, IIS iki uygulama havuzudesteklemek için yapılandırılmıştır: **DefaultAppPool** ve **Classic .NET AppPool**. DefaultAppPool seçilirse, uygulamanız tümleşik istek işleme modunda çalışır. Klasik .NET AppPool seçilirse, uygulamanız klasik istek işleme modunda çalışır.

[![Yeni Proje iletişim kutusu](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**Şekil 1**: İstek işleme modunu algılama ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))

Uygulamayı Edit iletişim kutusundaki istek işleme modunu değiştirebileceğinize dikkat edin. Seç düğmesini tıklatın ve uygulamayla ilişkili uygulama havuzunu değiştirin. bir ASP.NET uygulamasını klasikmoddan tümleşik moduna değiştirirken uyumluluk sorunları olduğunu fark edin. Daha fazla bilgi için aşağıdaki makalelere bakın:

- Windows Vista ve Windows Server 2008'de ASP.NET 1.1'i IIS 7.0'a yükseltme --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- iis 7.0 ile ASP.NET Entegrasyonu -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

ASP.NET bir uygulama DefaultAppPool kullanıyorsa, ASP.NET Yönlendirmesi'ni (ve dolayısıyla MVC'yi ASP.NET) işe almak için ek adımlar gerçekleştirmeniz gerekmez. Ancak, ASP.NET uygulaması Classic .NET AppPool'u kullanacak şekilde yapılandırılırsa okumaya devam edin, yapmanız gereken daha çok iş var.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>IIS'nin Eski Sürümleriyle ASP.NET MVC kullanma

IIS 7.0'dan daha eski bir IIS sürümüyle ASP.NET MVC kullanmanız gerekiyorsa veya Klasik modda IIS 7.0 kullanmanız gerekiyorsa, iki seçeneğiniz var demektir. İlk olarak, dosya uzantılarını kullanmak için rota tablosunu değiştirebilirsiniz. Örneğin, /Store/Details gibi bir URL istemek yerine, /Store.aspx/Details gibi bir URL istersiniz.

İkinci seçenek *joker karakter komut dosyası eşlemi*olarak adlandırılan bir şey oluşturmaktır. Joker karakter komut dosyası eşlemi, her isteği ASP.NET çerçeveye dönüştürmenizi sağlar.

Web sunucunuza erişiminiz yoksa (örneğin, ASP.NET MVC uygulamanız bir Internet Servis Sağlayıcısı tarafından barındırılıyorsa) ilk seçeneği kullanmanız gerekir. URL'lerinizin görünümünü değiştirmek istemiyorsanız ve web sunucunuza erişiminiz varsa, ikinci seçeneği kullanabilirsiniz.

Her seçeneği aşağıdaki bölümlerde ayrıntılı olarak inceleyeceğiz.

## <a name="adding-extensions-to-the-route-table"></a>Rota Tablosuna Uzantı Ekleme

ASP.NET Yönlendirme'yi IIS'nin eski sürümleriyle çalışmaya almanın en kolay yolu, Global.asax dosyasındaki rota tablonuzu değiştirmektir. Listeleme 1'deki varsayılan ve değiştirilmemiş Global.asax dosyası Varsayılan rota adlı bir rotayı yapılandırır.

**Listeleme 1 - Global.asax (değiştirilmemiş)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

Listeleme 1'de yapılandırılan Varsayılan rota, aşağıdaki gibi görünen URL'leri yönlendirmenize olanak tanır:

/Ana Sayfa/Dizin

/Ürün/Ayrıntılar/3

/Ürün

Ne yazık ki, IIS'nin eski sürümleri bu istekleri ASP.NET çerçevesine aktarmaz. Bu nedenle, bu istekler bir denetleyiciye yönlendirilemez. Örneğin, URL /Ev/Dizin için bir tarayıcı isteği nde bulunduysanız, Şekil 2'deki hata sayfasını alırsınız.

[![Yeni Proje iletişim kutusu](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**Şekil 2**: 404 Bulunamadı hatası alma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))

IIS'nin eski sürümleri yalnızca belirli istekleri ASP.NET çerçeveyle eşler. İstek, doğru dosya uzantısına sahip bir URL için olmalıdır. Örneğin, /SomePage.aspx için bir istek ASP.NET çerçevesine eşlenir. Ancak, /SomePage.htm için bir istek yok.

Bu nedenle, ASP.NET Yönlendirme'nin çalışması için Varsayılan rotayı, ASP.NET çerçevesine eşlenen bir dosya uzantısı içerecek şekilde değiştirmemiz gerekir.

Bu, ". `registermvc.wsf` Bu ASP.NET MVC 1 sürümü ile `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`dahil edildi , ama ASP.NET 2 bu komut dosyası [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)ASP.NET Futures taşındı, kullanılabilir .

Bu komut dosyasının yürütülmesi IIS ile yeni bir .mvc uzantısı kaydeder. .mvc uzantısını kaydettikten sonra, global.asax dosyasındaki rotalarınızı değiştirerek yolların .mvc uzantısını kullanmasını sağlayabilirsiniz.

Listeleme 2'deki değiştirilmiş Global.asax dosyası IIS'nin eski sürümleriyle çalışır.

**Listeleme 2 - Global.asax (uzantılarla değiştirilmiş)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

Önemli: Global.asax dosyasını değiştirdikten sonra ASP.NET MVC Uygulamanızı yeniden oluşturmayı unutmayın.

Listeleme 2'de Global.asax dosyasında iki önemli değişiklik vardır. Global.asax'ta tanımlanmış iki güzergah var. Varsayılan rotanın URL deseni, ilk rota şimdi aşağıdaki gibi görünüyor:

{controller}.mvc/{action}/{id}

.mvc uzantısının eklenmesi, ASP.NET Yönlendirme modülünün engellenebilen dosya türünü değiştirir. Bu değişiklikle, ASP.NET MVC uygulaması artık aşağıdaki gibi istekleri yönlendirir:

/Home.mvc/Index/

/Product.mvc/Ayrıntılar/3

/Ürün.mvc/

İkinci rota, Kök rotası, yeni. Kök rotası için bu URL deseni boş bir dizedir. Bu yol, uygulamanızın köküne göre yapılan istekleri eşleştirmek için gereklidir. Örneğin, Kök yolu aşağıdaki gibi görünen bir istekle eşleşir:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Rota tablonuzda bu değişiklikleri yaptıktan sonra, uygulamanızdaki tüm bağlantıların bu yeni URL desenleri ile uyumlu olduğundan emin olmanız gerekir. Başka bir deyişle, tüm bağlantılarınızın .mvc uzantısını içerdiğinden emin olun. Bağlantılarınızı oluşturmak için Html.ActionLink() yardımcı yöntemini kullanıyorsanız, herhangi bir değişiklik yapmanız gerekmez.

Registermvc.wcf komut dosyasını kullanmak yerine, IIS'ye ASP.NET çerçevesine elle eşlenen yeni bir uzantı ekleyebilirsiniz. Kendiniz yeni bir uzantı eklerken, **dosyanın var olduğunu doğrula** etiketli onay kutusunun işaretlenmediğinden emin olun.

## <a name="hosted-server"></a>Barındırılan Sunucu

Web sunucunuza her zaman erişiminiz yoktur. Örneğin, bir Internet Barındırma Sağlayıcısı kullanarak ASP.NET MVC uygulamanızı barındırırsanız, IIS'ye mutlaka erişiminiz gerekmez.

Bu durumda, ASP.NET çerçevesine eşlenen varolan dosya uzantılarından birini kullanmanız gerekir. ASP.NET eşlenen dosya uzantılarına örnek olarak .aspx, .axd ve .ashx uzantıları verilebilir.

Örneğin, Listeleme 3'teki değiştirilmiş Global.asax dosyası .mvc uzantısı yerine .aspx uzantısını kullanır.

**Listeleme 3 - Global.asax (.aspx uzantıları ile değiştirildi)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

Listeleme 3'teki Global.asax dosyası, .mvc uzantısı yerine .aspx uzantısını kullanması dışında önceki Global.asax dosyasıyla tamamen aynıdır. .aspx uzantısını kullanmak için uzak web sunucunuzda herhangi bir kurulum gerçekleştirmeniz gerekmez.

## <a name="creating-a-wildcard-script-map"></a>Joker Karakter Komut Dosyası Haritası Oluşturma

URL'leri ASP.NET MVC uygulamanız için değiştirmek istemiyorsanız ve web sunucunuza erişiminiz varsa, ek bir seçeneğiniz vardır. Web sunucusundaki tüm istekleri ASP.NET çerçeveyle eşleyen bir joker karakter komut dosyası eşlenebebilirsiniz. Bu şekilde, Varsayılan ASP.NET MVC rota tablosunu IIS 7.0 (klasik modda) veya IIS 6.0 ile kullanabilirsiniz.

Bu seçeneğin IIS'nin web sunucusuna karşı yapılan her isteği engellemesine neden olduğunu unutmayın. Buna resimler, klasik ASP sayfaları ve HTML sayfaları istekleri de dahildir. Bu nedenle, ASP.NET için bir joker komut dosyası eşlemi etkinleştirme performans etkileri vardır.

IIS 7.0 için joker karakter komut dosyası haritasını şu şekilde etkinleştirebilirsiniz:

1. Uygulamalar penceresinde uygulamanızı seçin
2. **Özellikler** görünümünün seçildiğinden emin olun
3. **Işleyici Eşlemeler** düğmesini çift tıklatın
4. Joker **Karakter Komut Dosyası Haritası Ekle** bağlantısını tıklayın (Bkz. Şekil 3)
5. aspnet\_isapi.dll dosyasına giden yolu girin (Bu yolu PageHandlerFactory komut dosyası haritasından kopyalayabilirsiniz)
6. MVC adını girin
7. **Tamam** düğmesini tıklatın

[![Yeni Proje iletişim kutusu](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**Şekil 3**: IIS 7.0 ile joker karakter komut dosyası haritası oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))

IIS 6.0 ile joker karakter komut dosyası haritası oluşturmak için aşağıdaki adımları izleyin:

1. Bir web sitesine sağ tıklayın ve Özellikler'i seçin
2. Ana **Dizini** sekmesini seçin
3. **Yapılandırma** düğmesini tıklatın
4. **Eşlemeler** sekmesini seçin
5. **Ekle** düğmesini tıklatın (Bkz. Şekil 4)
6. Yolu aspnet\_isapi.dll'ye yapıştırın (.aspx dosyaları için komut dosyası haritasından bu yolu kopyalayabilirsiniz)
7. Etiketli onay kutusunun işaretli olarak işaretle **nivarı dosyanın var olduğunu doğrula**
8. **Tamam** düğmesini tıklatın

[![Yeni Proje iletişim kutusu](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**Şekil 4**: IIS 6.0 ile joker karakter komut dosyası haritası oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))

Joker karakter komut dosyası eşlemlerini etkinleştirdikten sonra, Global.asax dosyasındaki rota tablosunu Root rotası içerecek şekilde değiştirmeniz gerekir. Aksi takdirde, uygulamanızın kök sayfası için bir istekte bulunduğunuzda Şekil 5'teki hata sayfasını alırsınız. Değiştirilen Global.asax dosyasını Listeleme 4'te kullanabilirsiniz.

[![Yeni Proje iletişim kutusu](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**Şekil 5**: Eksik Kök rota hatası([Tam boyutlu görüntüyü görüntülemek için tıklayınız](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))

**Listeleme 4 - Global.asax (Root rotası ile değiştirildi)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

IIS 7.0 veya IIS 6.0 için joker karakter komut dosyası eşlemesini etkinleştirdikten sonra, varsayılan rota tablosuyla çalışan ve şu gibi görünen isteklerde bulunabilirsiniz:

/

/Ana Sayfa/Dizin

/Ürün/Ayrıntılar/3

/Ürün

## <a name="summary"></a>Özet

Bu öğreticinin amacı, IIS'nin (veya klasik modda IIS 7.0)'in eski bir sürümünü kullanırken ASP.NET MVC'yi nasıl kullanabileceğinizi açıklamaktır. ASP.NET Yönlendirme'yi IIS'nin eski sürümleriyle çalışmaya almanın iki yöntemini tartıştık: Varsayılan rota tablosunu değiştirin veya joker karakter komut dosyası eşlemi oluşturun.

İlk seçenek, ASP.NET MVC uygulamanızda kullanılan URL'leri değiştirmenizi gerektirir. Bu ilk seçeneğin çok önemli bir avantajı, rota tablosunu değiştirmek için bir web sunucusuna erişmenize gerek kalmamasıdır. Bu, bir Internet barındırma şirketi ile ASP.NET MVC uygulama barındırma bile bu ilk seçeneği kullanabilirsiniz anlamına gelir.

İkinci seçenek bir joker komut dosyası eşlemi oluşturmaktır. Bu ikinci seçeneğin avantajı, URL'lerinizi değiştirmeniz gerekmemesidir. Bu ikinci seçeneğin dezavantajı, ASP.NET MVC uygulamanızın performansını etkileyebilir.

> [!div class="step-by-step"]
> [Önceki](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
