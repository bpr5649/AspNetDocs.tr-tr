---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: ASP.NET Web sayfalarına giriş-WebMatrix kullanarak site yayımlama | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, ASP.NET Web sayfalarını ve Microsoft WebMatrix 'i tanıtan öğretici kümesinde son taksiti. Site t 'nizi yayımlamayı açıklar...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240594"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>ASP.NET Web sayfalarına giriş-WebMatrix kullanarak site yayımlama

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

> Bu öğretici, ASP.NET Web sayfalarını ve Microsoft WebMatrix 'i tanıtan öğretici kümesinde son taksiti. Başkalarının onunla çalışabilmesi için sitenizi Internet 'Te nasıl yayımlayacağınızı ele alır. [ASP.NET Web sayfaları siteleri Için tutarlı bir görünüm oluşturarak](https://go.microsoft.com/fwlink/?LinkId=251585)seriyi tamamladığınız varsayılır.
> 
> Sitenizi kullanarak nasıl yayımlayacağınızı öğreneceksiniz:
> 
> - Microsoft Azure
> - Web barındırma şirketi

## <a name="about-publishing-your-site"></a>Sitenizi yayımlama hakkında

Şimdi, sayfalarınızın sınanması da dahil olmak üzere tüm çalışmalarınızı yerel bir bilgisayarda tamamladınız. <em>. Cshtml</em> sayfalarınızı çalıştırmak Için, WebMatrix içinde yerleşik olan Web sunucusunu kullandınız, yani IIS Express. Ancak kuşkusuz, sizin dışında oluşturduğunuz siteyi hiç kimse göremez. Başkalarının siteniz ile çalışmasına izin vermek için, bunu Internet 'Te yayımlamanız gerekir.

Zaten bir genel Web sunucusuna erişiminiz yoksa, yayımlama, *bulut platformu* veya *barındırma sağlayıcısı*içeren bir hesabınız olması gerektiği anlamına gelir. Microsoft Azure gibi bir bulut platformu, uygulamalarınız için isteğe bağlı altyapı sağlar. Barındırma sağlayıcısı, herkese açık bir Web sunucusuna sahip olan ve siteniz için size alan kiralayabileceği bir şirkettir. Barındırma planları, küçük siteler için ayda birkaç ABD Doları (veya ücretsiz), yüksek hacimli ticari web siteleri için de ayda yüzlerce ABD Doları kadar çalışır.

> [!NOTE]
> Evde Internet hizmetini almak için kullandığınız Internet servis sağlayıcısı (ISS) aracılığıyla bir genel Web sunucusuna erişiminiz olabilir. Ancak, barındırma sağlayıcınız ASP.NET Web sayfalarını desteklemelidir. Birçok ISS yoktur, ancak her zaman kontrol etecektir.

Bu öğreticide yayımlama hakkında genel bakış sunuyoruz. Her şey için tam ayrıntı sağlamak pratik değildir, çünkü işlem her barındırma sağlayıcısı için bir bit 'e göre farklılık gösterir. Ancak işlemin nasıl çalıştığına ilişkin iyi bir fikir alacaksınız.

Bu öğretici dört bölüm içerir:

1. [Varsayılan sayfayı ayarlama](#defaultpage)
2. Yayımlama (aşağıdakilerden birini seçin)  
 a. [Sitenizi Microsoft Azure yayımlama](#azure)  
 b. [Sitenizi bir Web barındırma şirketine yayımlama](#host)
3. [Canlı siteyi güncelleştirme: yeniden yayımlama](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Varsayılan sayfayı ayarlama

Bir Kullanıcı Web sitenizin temel adresine gittiğinde, sitenizin varsayılan sayfası kullanıcıya gösterilir. Örneğin, *Default.htm* ' de site için varsayılan sayfa olarak ayarlandığında, ' ye gidilme ile `www.contoso.com` `www.contoso.com` aynı olur `www.contoso.com/Default.htm` .

Şu anda siteniz varsayılan sayfa olarak **default. cshtml** kullanır. Bu sayfa, varsayılan sayfanız için uygundur, ancak bu öğreticide, boş bir sayfa görüntülemesi için bu sayfaya herhangi bir içerik eklemediniz. Default. cshtml dosyasını açın ve içeriği aşağıdaki kodla değiştirin.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Artık siteniz yayın için hazır. İlk olarak, siteyi Azure 'a dağıtmayı ve sonra bir Web barındırma şirketine dağıtmayı öğreneceksiniz. Her iki seçenek de Web siteniz için geçerlidir ve yalnızca dağıtım seçeneklerinden birini izlemeniz yeterlidir.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Sitenizi Microsoft Azure yayımlama

Bu öğretici öncelikle sitenizin Microsoft Azure nasıl dağıtılacağını gösterir. Microsoft hesabı ile oturum açarak Azure üzerinde en fazla 10 ücretsiz site oluşturabilirsiniz. Bu ücretsiz siteler, sitelerinizi test etmek için kullanışlı bir yol sağlar. Tüm ücretsiz siteleriniz kullanmaktan kaçınmak için, bu örnek siteyi daha sonra her zaman silebilirsiniz. Yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/dotnet/).

WebMatrix şeridinde **Yayımla** düğmesine tıklayın.

![WebMatrix şeridinde ' Yayımla ' düğmesi](publishing/_static/image1.png)

**Sitenizi Yayımla** iletişim kutusu görüntülenir. Microsoft hesabı oturumunuzu açmadıysanız, iletişim kutusunda **Azure ile çalışmaya başlama** bağlantısı bulunur. Bu bağlantıya tıklayın.

![Sitenizi yayımlayın](publishing/_static/image2.png)

Bir Microsoft hesabı oturum açmadıysanız, oturum açma fırsatına yeniden giriş vermiş olursunuz. Sitenizi Azure 'da yayımlamak için bir Microsoft hesabı oturum açmalısınız.

![Oturum Açma](publishing/_static/image3.png)

Microsoft hesabı oturum açtıktan sonra iletişim kutusu, Azure 'da yeni bir site oluşturmak veya Azure 'daki mevcut sitelerinizden birine bağlanmak için bağlantılar içerir.

![Yeni site oluştur](publishing/_static/image4.png)

**Yeni site oluştur**' u seçin.

Projenizi **Webpagesfilmlerini**olarak adlandırdıysanız sitenizin varsayılan adı **webpagesmovies.azurewebsites.net**olacaktır. Bu varsayılan ad, kırmızı ünlem işaretiyle gösterildiği gibi büyük olasılıkla kullanılabilir değildir.

![Varsayılan Web sitesi adı](publishing/_static/image5.png)

Site adını kullanılabilir bir şekilde değiştirin ve konumunuza yakın bir konum seçin.

![değiştirilen site adı](publishing/_static/image6.png)

**Tamam**'a tıklayın.

WebMatrix, sunucunun siteyle uyumlu olup olmadığını belirlemede bir test.

![Uyumluluk testi](publishing/_static/image7.png)

**Devam**’ı seçin.

Uyumluluk testinin sonuçları görüntülenir.

![Uyumluluk sonucu](publishing/_static/image8.png)

**Devam**’ı seçin.

WebMatrix, sitede yayımlanacak dosya ve veritabanlarını görüntüler. Siteyi ilk kez yayımladınız bu yana tüm dosyalar listelenir. Yayımlanmaya hazırlanmayan bir dosyanın işaretini kaldırabilirsiniz. Sonraki yayınlarda yalnızca değiştirilen dosyalar görüntülenir. Bkz. [canlı siteyi güncelleştirme: yeniden yayımlama](#update).

![Önizlemeyi Yayımla](publishing/_static/image9.png)

**Devam**’ı seçin.

Site Azure 'a dağıtıldıktan sonra, dağıtımın tamamlandığını belirten bir ileti görüntülenir.

![Yayımlama Tamam](publishing/_static/image10.png)

Siteniz ve veritabanınız Azure 'da yayımlanmıştır ve artık genel kullanıma sunulmuştur. Yayımlamanın tamamlandığını belirten iletideki bağlantıya tıklayın ve ardından dağıtılan sitenizi görürsünüz. Siz veya Internet erişimi olan herkes veritabanına kayıt ekleyebilir veya kayıtları değiştirebilir.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Sitenizi bir Web barındırma şirketine yayımlama

Azure 'da yayınlanmamaya karar verirseniz, sitenizi bir Web barındırma şirketine yayımlayabilirsiniz.

**Web barındırma 'Yı bul** bağlantısına tıklayın.

![Yayımlama Ayarları iletişim kutusunda ' Web barındırma 'i bul ' düğmesi](publishing/_static/image12.png)

Microsoft sitesinde ASP.NET destekleyen barındırma sağlayıcılarını listeleyen bir sayfaya gidebilirsiniz.

![Microsoft sitesinde barındırma sağlayıcılarını listeleyen sayfa](publishing/_static/image13.png)

Kuşkusuz, artık uzun vadede gerekli olan barındırma özelliklerini tam olarak bilmek zor olabilir. Göz önünde bulundurmanız gereken birkaç nokta aşağıda verilmiştir:

- Webpagesfilmlerini sitesinin amaçları doğrultusunda, SQL Server için ayrı bir eklentiye sahip olmanız gerekmez, bu da genellikle ekstra maliyetlere sahiptir. Sitenizde, kendi içinde olan SQL Server Compact Edition kullanıyorsunuz. Ancak, gelecekteki bazı Web sitesi işleri için SQL Server erişiminizin olması gerekebilir. Bunu düşünüyorsanız, daha sonra SQL Server Özellik ekleyediğinizden emin olun.
- Barındırma sağlayıcısının Web Dağıtımı yayımlama protokolünü destekleyip desteklemediğini denetleyin. FTP protokolünü kullanarak yayımlayabilirsiniz, ancak Web Dağıtımı kullanmak daha uygundur.

Bazı siteler ücretsiz deneme süresi sunmaktadır. Ücretsiz deneme sürümü, WebMatrix ve ASP.NET Web sayfaları ile çalışmaya devam ederken yayımlamayı ve barındırmayı denemeye yönelik iyi bir yoldur.

Dilediğiniz birini seçin. Bu öğretici için, DiscountASP.NET ' yi seçtik, çünkü öğreticiyi oluşturuyoruz, bu şirketin kişilerin bir siteyi birkaç ay boyunca serbest bir şekilde barındırmasına izin veren bir promosyonu vardı.

> [!NOTE]
> Bu öğreticide bir barındırma sağlayıcısı seçemiz, bu şirketin başka bir yerinde bir onay olarak yorumlanmamalıdır. Ancak, bir çizim için bir tane seçmemiz gerekiyordu ve DiscountASP.NET, ASP.NET Web sayfalarını ve yayımlama için Web Dağıtımı protokolünü destekleyen birçok şirketten biridir.

Genellikle, barındırma sağlayıcısına kaydolduktan sonra şirket size Kullanıcı adı ve parola, Web sunucusunun URL 'SI ve benzeri bir e-posta gönderir. Barındırma şirketi Web Dağıtımı protokolünü destekliyorsa, yayımlama ayarları içeren bir dosya gönderebilir veya bir tane indirmenizi sağlayabilirsiniz. Bir yayımlama ayarları dosyası sizin için işlemi basitleştirir.

Kaydolup yayımlamaya hazırsanız, WebMatrix şeridinde **Yayımla** düğmesine tıklayın. **Ayarları Yayımla** iletişim kutusu görüntülenir.

Barındırma sağlayıcısı size bir yayımlama ayarları dosyası gönderdiyse, **Yayımlama ayarlarını Içeri aktar** bağlantısına tıklayın ve dosyayı içeri aktarın. Bir yayımlama ayarları dosyanız yoksa, barındırma şirketinin size e-posta ile gönderdiği değerleri kullanarak alanları girin. İşte **yayınlama ayarları** iletişim kutusu işiniz bittiğinde şöyle görünebilir:

![Yayımlama Ayarları ' ayarları Yayımla ' iletişim kutusunda doldurulmuştur](publishing/_static/image14.png)

**Bağlantıyı doğrula**' ya tıklayın. Her şey tamam ise, iletişim kutusu **başarıyla bağlanır**, bu da barındırma sağlayıcısının sunucusuyla iletişim kurabildiği anlamına gelir.

![Yayımlama ayarları doğruysa başarı iletisi](publishing/_static/image15.png)

Bir sorun varsa, WebMatrix, sorunun ne olduğunu anlatmak için en iyi seçenektir:

![Yayımlama ayarları ile ilgili bir sorun varsa hata iletisi](publishing/_static/image16.png)

Ayarlarınızı kaydetmek için **Kaydet** ' e tıklayın. WebMatrix, barındırma sitesiyle doğru iletişim kurabildiğinden emin olmak için bir test gerçekleştirmeyi önerir:

![Yayımlama işleminin bir testini gerçekleştirmeye yönelik ileti teklifi](publishing/_static/image17.png)

**Evet**' e tıklayın. WebMatrix, bazı örnek dosyaları barındırma sağlayıcısına yükler. Uyumluluk testi tamamlandığında, WebMatrix sonuçları raporlar:

![Yayımlama testinin sonuçları](publishing/_static/image18.png)

Çalışmaya hazırsanız, **devam** ' a tıklayarak yayımlama işlemini gerçek için başlatın. WebMatrix, sitenizde hangi dosyaların olduğunu ve zaten ana bilgisayar sunucusunda (Şu anda, yok) olduğunu ve yayımlama işleminin bir önizlemesini almanızı sağlar:

![Yayınlama işleminin karşıya yükleneceği dosyaların önizlemesi](publishing/_static/image19.png)

Yayımlanacak dosyaların listesi, *filmler. cshtml*gibi oluşturduğunuz Web sayfalarını içerir. Listede ayrıca yüklediğiniz Yardımcılar için dosyalar, veritabanınız için SQL Server Compact Edition çalıştırmak ve benzeri bilgiler de bulunur. Sonuç olarak, ilk yayımlama süreci önemli olabilir.

**Devam**’a tıklayın. WebMatrix, dosyalarınızı barındırma sağlayıcısının sunucusuna kopyalar. İşlem tamamlandığında, sonuçlar durum çubuğunda bildirilir:

![Yayımlama işlemi başarıyla tamamlandığında durum çubuğu iletisi](publishing/_static/image20.png)

Canlı sitenizi görmek için durum çubuğundaki bağlantıya tıklayın. URL 'ye *film* ekleyin ve oluşturduğunuz *filmler. cshtml* dosyasını görürsünüz:

![Filmler sayfasını gösteren canlı site](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Canlı siteyi güncelleştirme: yeniden yayımlama

Sitenizi yayımladıktan sonra (Azure 'a veya bir Web barındırma şirketine), &mdash; bilgisayarınızın sürümü ve Hizmet sağlayıcısındaki sürüm olmak üzere iki kopyası vardır. Büyük olasılıkla siteyi geliştirmeye devam etmek isteyeceksiniz (başka bir şey, bir sonraki öğretici kümesinin parçası olarak). Bunu yaptığınızda, değişiklikleri bilgisayarınızdan hizmet sağlayıcısına kopyalamak için sitenizi yeniden yayımlamanız gerekir. WebMatrix 'teki Yayımla işlemi, sitenizde hangi dosyaların değiştiğini belirleyebilir ve yalnızca bu dosyaları yayımlayabilirler.

Yeniden yayımmadan nasıl çalıştığını görmek için, *filmler. cshtml* sitesini açın, küçük bir değişiklik yapın ve dosyayı kaydedin. Örneğin, başlığını olarak değiştirin `Movies - Updated` .

Şeritteki **Yayımla** düğmesine tıklayın. WebMatrix nelerin değiştirildiğini belirler ve yayımlayacağınız dosyaların önizlemesini gösterir.

![Değiştirilen dosyaları yeniden yayımlamaya yönelik olarak gösteren ' Yayımla ' iletişim kutusu](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> Varsayılan olarak, WebMatrix veritabanını (*. sdf* dosyası) yalnızca siteyi ilk kez yayımladığınızda yayımlar. Siteniz yayımlandığında ve insanlar web sitesiyle etkileştikten sonra, canlı sitedeki veritabanı genellikle sitenin gerçek verileri olur. Bilgisayarınızda genellikle test verilerini içeren *. sdf* dosyası ile canlı veritabanının üzerine yazılmamaya dikkat etmeniz gerekir. Uyarı **yayımlamanın her türlü uzak veritabanının üzerine yazılmasına**neden olduğunu ve *webpagesfilmlerini. sdf* onay kutusunun neden varsayılan olarak temizlendiğinizi görürsünüz.

**Devam**’a tıklayın. WebMatrix, değiştirilen dosyaları yayımlar ve ilk yayımladığında olduğu gibi başarılı bir ileti gösterir.

Canlı siteye gidin (hala gösteriyorsa, başarı iletisindeki bağlantıyı tıklatabilir) ve yaptığınız değişikliğin yayımlandığını doğrulayabilirsiniz.

> [!TIP] 
> 
> **Dosyaları uzaktan Düzenle**
> 
> Sitenizi değiştirmeye ve sonra yeniden yayınlayabilmeniz alternatif olarak, uzak dosyaları doğrudan WebMatrix 'te düzenleyebilirsiniz. Bu senaryoda, hizmet sağlayıcıdaki bir dosyayı açarsınız ve WebMatrix sizin düzenlemeniz için bir kopyasını indirir. Dosyayı her kaydedişinizde, WebMatrix değişiklikleri siteye gönderir.
> 
> Uzaktan Düzenle, canlı sitenizde değişiklik yapmanın kolay bir yoludur. Ancak, bu şekilde yaptığınız değişiklikler yerel sitenizdeki dosyalarla eşitlenmez. Yerel dosyaları uzak siteyle eşleştirmek için uzak dosyaları indirebilirsiniz. Bu işlem, tersi dışında yayımlama gibi işler.
> 
> Burada WebMatrix 'in uzaktan düzenleme ve uzaktan indirme özellikleri hakkında daha fazla bilgi vermeyiz. Birden çok kişinin aynı sitede farklı bilgisayarlarda çalışması gerekiyorsa oldukça yararlı olur. Daha fazla bilgi için bkz. [WebMatrix 2 Beta Ile uzak site yayımlama ve düzenleme](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.net WebMatrix ASP.NET Web sayfaları Forumu](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), sorularınızı göndermek ve yanıt almak için harika bir yerdir.

> [!div class="step-by-step"]
> [Önceki](layouts.md)
