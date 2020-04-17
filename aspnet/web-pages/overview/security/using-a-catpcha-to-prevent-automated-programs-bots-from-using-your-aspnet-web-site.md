---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Botların ASP.NET Web Razor) Sitenizi Kullanmasını Önlemek için CAPTCHA Kullanma | Microsoft Dokümanlar
author: rick-anderson
description: Bu makalede, otomatik programların (botların) ASP.NET bir Web Sayfasında (Razor) görevleri yerine getirmesini önlemek için ReCaptcha'nın (güvenlik önlemi) nasıl kullanılacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543762"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Botların ASP.NET Web Razor) Sitenizi Kullanmasını Önlemek için CAPTCHA Kullanma

[Microsoft](https://github.com/microsoft) tarafından

> Bu makalede, otomatik programların (botların) ASP.NET web sayfaları (Jilet) web sitesinde görevleri yerine getirmesini önlemek için ReCaptcha (güvenlik önlemi) nasıl kullanılacağı açıklanmaktadır.
> 
> **Ne öğreneceksiniz:** 
> 
> - Sitenize captcha testi nasıl eklenir?
> 
> Bu makalede tanıtılan ASP.NET özellikleri şunlardır:
> 
> - `ReCaptcha` Yardımcı.
> 
> > [!NOTE]
> > Bu makaledeki bilgiler ASP.NET Web Sayfaları 1.0 ve Web Sayfaları 2 için geçerlidir.

## <a name="about-captchas"></a>CAPTCHAs Hakkında

İnsanların sitenize kaydolmasına izin verdiğinizde, hatta sadece bir ad ve URL girdiğinizde (blog yorumu gibi), sahte adlar selebilirsiniz. Bunlar genellikle bulabilecekleri her web sitesinde URL'leri bırakmaya çalışan otomatik programlar (botlar) tarafından bırakılır. (Ortak bir motivasyon satılık ürünlerin URL'leri göndermektir.)

Kullanıcının adlarını ve sitesini kaydettiklerinde veya başka bir şekilde girdiklerini doğrulamak için bir *CAPTCHA* kullanarak bir kullanıcının bilgisayar programı değil, gerçek kişi olduğundan emin olmanıza yardımcı olabilirsiniz. CAPTCHA, Bilgisayarlara ve İnsanlara Ayrı Söylemek Için Tamamen Otomatik Leştirilmiş Turing testinin kısaltmasI. CAPTCHA, kullanıcıdan bir kişinin yapması kolay ama otomatik bir programın yapması zor olan bir şey yapması istenen bir *meydan okuma yanıtı* testidir. CAPTCHA'nın en yaygın türü, bazı bozuk harfler gördüğünüz ve bunları yazmanız istendiği bir türdür. (Distorsiyon zor botlar için harfleri deşifre etmek için yapmak gerekiyordu.)

## <a name="adding-a-recaptcha-test"></a>ReCaptcha Testi Ekleme

ASP.NET sayfalarda, `ReCaptcha` recaptcha hizmetini temel alan bir CAPTCHA testi işlemek için[http://recaptcha.net](http://recaptcha.net)yardımcıyı kullanabilirsiniz. Yardımcı, `ReCaptcha` sayfa doğrulanmadan önce kullanıcıların doğru şekilde girmeleri gereken iki bozuk sözcük resmi görüntüler. Kullanıcı yanıtı ReCaptcha.Net hizmeti tarafından doğrulanır.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Web sitenizi ReCaptcha.Net[http://recaptcha.net](http://recaptcha.net)' de kaydedin ( ). Kaydı tamamladığınızda, ortak bir anahtar ve özel bir anahtar alırsınız.
2. Web Yardımcıları Kitaplığı'ASP.NET, [ASP.NET bir Web Sayfası Sitesine Yardımcı Yükleme'de](https://go.microsoft.com/fwlink/?LinkId=252372)açıklandığı şekilde web sitenize ekleyin .
3. Zaten bir * \_AppStart.cshtml* dosyanız yoksa, bir web sitesinin kök klasöründe * \_AppStart.cshtml*adında bir dosya oluşturun.
4. `Recaptcha` * \_AppStart.cshtml* dosyasına aşağıdaki yardımcı ayarlarını ekleyin: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Kendi `PublicKey` ortak `PrivateKey` ve özel anahtarlarınızı kullanarak özellikleri ve özelliklerini ayarlayın.
6. * \_AppStart.cshtml* dosyasını kaydedin ve kapatın.
7. Bir web sitesinin kök klasöründe, *Recaptcha.cshtml*adlı yeni bir sayfa oluşturun.
8. Varolan içeriği aşağıdakilerle değiştirin: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. *Recaptcha.cshtml* sayfasını tarayıcıda çalıştırın. `PrivateKey` Değer geçerliyse, sayfa ReCaptcha denetimini ve bir düğmeyi görüntüler. Eğer appstart.html genel olarak anahtarları ayarlamamış olsaydı, sayfa bir hata görüntülerdi. * \_* 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Test için sözcükleri girin. ReCaptcha testini geçerseniz, bu yönde bir ileti görürsünüz. Aksi takdirde bir hata iletisi görürsünüz ve ReCaptcha denetimi yeniden görüntülenir.

> [!NOTE]
> Bilgisayarınız proxy sunucusu kullanan bir etki alanındaysa, `defaultproxy` *Web.config* dosyasının öğesini yapılandırmanız gerekebilir. Aşağıdaki örnekte, ReCaptcha hizmetinin çalışmasını sağlayacak şekilde yapılandırılan öğeye `defaultproxy` sahip bir *Web.config* dosyası gösterilmektedir.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Web Sayfaları Siteleri için Site Genelinde Davranışı Özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha sitesi](https://www.google.com/recaptcha)
