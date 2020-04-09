---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma (C#) ile MVC 5 Uygulaması Oluşturun | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu öğretici, kullanıcıların Harici bir authenti kimlik bilgileri ile OAuth 2.0 kullanarak oturum açmanızı sağlayan bir ASP.NET MVC 5 web uygulaması oluşturmak için nasıl gösterir ...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676323"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma Özellikli Bir ASP.NET MVC 5 Uygulaması Oluşturma (C#)

tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

> Bu öğretici, kullanıcıların Facebook, Twitter, LinkedIn, Microsoft veya Google gibi harici bir kimlik doğrulama sağlayıcısının kimlik bilgileriyle [OAuth 2.0](http://oauth.net/2/) kullanarak oturum açmalarını sağlayan bir ASP.NET MVC 5 web uygulaması oluşturmanızı gösterir. Basitlik için, bu öğretici Facebook ve Google'ın kimlik bilgileri ile çalışmaya odaklanır.
> 
> Milyonlarca kullanıcının bu dış sağlayıcılarla zaten hesapları olduğundan, bu kimlik bilgilerini web sitelerinizde etkinleştirmek önemli bir avantaj sağlar. Bu kullanıcılar, yeni bir kimlik bilgileri kümesi oluşturmak ve hatırlamak zorunda değillerse sitenize kaydolmaya daha meyilli olabilir.
> 
> Ayrıca [sms ve e-posta İki Faktörlü Kimlik Doğrulama ile MVC 5 uygulaması ASP.NET](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)bakın.
> 
> Öğretici ayrıca kullanıcı için profil verilerinin nasıl ekleyeceğini ve rol eklemek için Üyelik API'sinin nasıl kullanılacağını da gösterir. Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır ( [@RickAndMSFT](https://twitter.com/RickAndMSFT) Twitter beni takip edin: ).

<a id="start"></a>
## <a name="getting-started"></a>Başlarken

Web veya [Visual Studio 2013 için Visual Studio Express 2013'u](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyerek ve çalıştırarak başlayın. [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üzeri yükleyin. Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, ve daha fazlası ile ilgili yardım için bu [örnek projeye](https://github.com/matthewdunsdon/oauthforaspnet)bakın.

> [!NOTE]
> Google OAuth 2'yi kullanmak ve SSL uyarıları olmadan yerel hata ayıklamak için Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üzeri ni yüklemeniz gerekir.

**Başlat** sayfasından **Yeni Proje'yi** tıklatın veya menüyü kullanabilirsiniz ve **Dosya'yı**ve ardından **Yeni Proje'yi**seçebilirsiniz.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>İlk Uygulamanızı Oluşturma

**Yeni Proje'yi**tıklatın, ardından soldaki **Visual C#** seçeneğini, ardından **Web'i** ve ardından **ASP.NET Web Uygulamasını**seçin. Projenizi "MvcAuth" olarak adlandırın ve **ardından Tamam'ı**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

Yeni **ASP.NET Projesi** iletişim kutusunda **MVC'yi**tıklatın. Kimlik Doğrulama Bireysel **Kullanıcı Hesapları**değilse, **Kimlik Doğrulamayı Değiştir** düğmesini tıklatın ve Bireysel Kullanıcı **Hesapları'nı**seçin. **Bulutta Host'u**kontrol ederek, uygulamayı Azure'da barındırmak çok kolay olacaktır.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

**Bulutta Ana Bilgisayar'ı**seçtiyseniz, yapıla iletişim kutusunu tamamlayın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>En son OWIN ara yazılımlarına güncellemek için NuGet'i kullanın

[OWIN ara yazılımını](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)güncellemek için NuGet paket yöneticisini kullanın. Sol menüde **Güncelleştirmeler'i** seçin. **Tümlerini Güncelleştir** düğmesine tıklayabilir veya yalnızca OWIN paketlerini arayabilirsiniz (bir sonraki resimde gösterilmiştir):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

Aşağıdaki resimde yalnızca OWIN paketleri gösterilmiştir:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

Paket Yöneticisi Konsolu'ndan (PMC) `Update-Package` tüm paketleri güncelleştiren komutu girebilirsiniz.

Uygulamayı çalıştırmak için **F5** veya **Ctrl+F5** tuşuna basın. Aşağıdaki resimde bağlantı noktası numarası 1234'dür. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.

Tarayıcı pencerenizin boyutuna bağlı olarak, **Ana Sayfa** **,** **İletişim**, **Kayıt** ve **Giriş** bağlantılarını görmek için gezinti simgesini tıklatmanız gerekebilir.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Projede SSL Kurulumu

Google ve Facebook gibi kimlik doğrulama sağlayıcılarına bağlanmak için SSL'yi kullanmak üzere IIS-Express'i ayarlamanız gerekir. Oturum açtıktan sonra SSL kullanmaya devam etmek ve HTTP'ye geri düşmemek önemlidir, giriş çereziniz de kullanıcı adınız ve şifreniz kadar gizlidir ve SSL kullanmadan tel boyunca açık metin olarak gönderirsiniz. Ayrıca, MVC ardışık hattı çalıştırılmadan önce el sıkışmayı gerçekleştirmek ve kanalı (HTTPS'yi HTTP'den daha yavaş yapan şeyin büyük bir kısmı dır) güvenli hale getirmek için zaman aldınız, bu nedenle oturum açtıktan sonra HTTP'ye yönlendirmek mevcut isteği veya gelecekteki istekleri çok daha hızlı yapmaz.

1. **Çözüm Gezgini'nde** **MvcAuth** projesini tıklatın.
2. Proje özelliklerini göstermek için F4 tuşuna basın. Alternatif olarak, **Görünüm** menüsünden **Özellikler Penceresi'ni**seçebilirsiniz.
3. **SSL Etkin'i** True'ya Değiştirin.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL'sini kopyalayın `https://localhost:44300/` (diğer SSL projeleri oluşturmadığınız sürece olacaktır).
5. **Çözüm Gezgini'nde,** **MvcAuth** projesine sağ tıklayın ve **Özellikler'i**seçin.
6. **Web** sekmesini seçin ve ardından SSL URL'sini **Project Url** kutusuna yapıştırın. Dosyayı kaydedin (Ctl+S). Facebook ve Google kimlik doğrulama uygulamalarını yapılandırmak için bu URL'ye ihtiyacınız olacaktır.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Tüm [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) istekleri gerektiren `Home` denetleyiciye Zorunlu Https özniteliğini ekleyin HTTPS kullanmanız gerekir. Daha güvenli bir yaklaşım uygulamaya [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtresi eklemektir. Eğitimimde &quot;Uygulamayı SSL ile koruyun ve&quot; Yetkilendirme Özniteliği ile koruyun bölümüne bakın [Auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve Azure Uygulama Hizmeti'ne dağıtın.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) Ev denetleyicisinin bir bölümü aşağıda gösterilmiştir.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Uygulamayı çalıştırmak için CTRL+F5'e basın. Sertifikayı geçmişte yüklediyseniz, bu bölümün geri kalanını atlayabilir ve [OAuth 2 için bir Google uygulaması oluşturmaya ve uygulamayı projeye bağlayarak](#goog)atlayabilirsiniz , aksi takdirde, IIS Express'in oluşturduğu kendi imzalı sertifikaya güvenme yönergelerini uygulayabilirsiniz.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Güvenlik **Uyarısı** iletişim kutusunu okuyun ve localhost'u temsil eden sertifikayı yüklemek istiyorsanız **Evet'i** tıklatın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE *Ana* sayfayı gösterir ve hiçbir SSL uyarıları vardır.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome da sertifikayı kabul eder ve bir uyarı olmadan HTTPS içeriğini gösterir. Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler. Uygulamamız için Riskleri **Anlıyorum'a**güvenle tıklayabilirsiniz.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2 için bir Google uygulaması oluşturma ve uygulamayı projeye bağlama

> [!WARNING]
> Geçerli Google OAuth yönergeleri için, [ASP.NET Core'da Google kimlik doğrulamasını yapılandırmaya](/aspnet/core/security/authentication/social/google-logins)bakın.

1. [Google Geliştiriciler Konsolu'na](https://console.developers.google.com/)gidin.
2. Daha önce bir proje oluşturmadıysanız, sol sekmede **Kimlik Bilgileri'ni** seçin ve ardından **Oluştur'u**seçin.
3. Sol sekmesinde Kimlik **Bilgileri'ni**tıklatın.
4. **Kimlik bilgileri oluştur'u** ve **Ardından OAuth istemci kimliğini**tıklatın. 

    1. **İstemci Kimliği Oluştur** iletişim kutusunda, uygulama türü için varsayılan **Web uygulamasını** saklayın.
    2. Yetkili **JavaScript** menşelerini yukarıda kullandığınız SSL URL'sine ayarlama (başka`https://localhost:44300/` SSL projeleri oluşturmadığınız sürece)
    3. Yetkili **uri yönlendirmeyi** şu şekilde ayarlayın:  
         `https://localhost:44300/signin-google`
5. OAuth Consent ekran menü öğesini tıklatın, ardından e-posta adresinizi ve ürün adınızı ayarlayın. Formu tamamladığınızda **Kaydet'i**tıklatın.
6. Kütüphane menü öğesini tıklatın, **Google+ API'yi**arayın, üzerine tıklayın ve etkinleştir'e basın.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   Aşağıdaki resimde etkin API'ler gösterilmektedir.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google API'ler API Yöneticisi'nden, **Müşteri Kimliğini**almak için **Kimlik Bilgileri** sekmesini ziyaret edin. Uygulama sırları ile bir JSON dosyasını kaydetmek için indirin. **ClientId** ve **ClientSecret'ı** App_Start `UseGoogleAuthentication` klasöründeki *Startup.Auth.cs* dosyasında *App_Start* bulunan yönteme kopyalayıp yapıştırın. Aşağıda gösterilen **ClientId** ve **ClientSecret** değerleri örneklerdir ve çalışmıyor.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Güvenlik - Hassas verileri asla kaynak kodunuzda depolamayın. Örneği basit tutmak için yukarıdaki koda hesap ve kimlik bilgileri eklenir. [Parolaları ve diğer hassas verileri ASP.NET ve Azure Uygulama Hizmetine dağıtmaya](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)yönelik en iyi uygulamalara bakın.
8. Uygulamayı oluşturmak ve çalıştırmak için **CTRL+F5** tuşuna basın. Giriş **Yap** bağlantısını tıklayın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. Oturum **açmak için başka bir hizmeti kullan**, **Google'ı**tıklatın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Yukarıdaki adımlardan herhangi birini kaçırırsanız HTTP 401 hatası alırsınız. Yukarıdaki adımlarınızı yeniden kontrol edin. Gerekli ayarı (örneğin **ürün adı)** kaçırırsanız, eksik öğeyi ekleyin ve kaydedin; kimlik doğrulamanın çalışması birkaç dakika sürebilir.
10. Kimlik bilgilerinizi gireceğiniz Google sitesine yönlendirilirsiniz.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz web uygulamasına izin vermeniz istenir:
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. **Kabul et**'e tıklayın. Artık Google hesabınızı kaydedebilirsiniz MvcAuth uygulamasının **Kayıt** sayfasına geri yönlendirilir. Gmail hesabınız için kullanılan yerel e-posta kaydı adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta takma adını (diğer bir şekilde kimlik doğrulama için kullandığınız e-posta) tutmak istersiniz. **Kaydol'u**tıklatın.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Uygulamayı Facebook'ta oluşturma ve uygulamayı projeye bağlama

> [!WARNING]
> Geçerli Facebook OAuth2 kimlik doğrulama yönergeleri için Bkz. [Facebook kimlik doğrulamayı yapılandırma](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Üyelik Verilerini İnceleyin

**Görünüm** menüsünde **Sunucu Gezgini'ni**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

**Varsayılan Bağlantıyı Genişlet (MvcAuth)**, **Tabloları**genişlet, **AspNetUsers** sağ tıklatın ve **Tablo Verilerini Göster'i**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers tablo verileri](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Kullanıcı Sınıfına Profil Verileri Ekleme

Bu bölümde, aşağıdaki resimde gösterildiği gibi, kayıt sırasında kullanıcı verilerine doğum tarihi ve memleket eklersiniz.

![ev şehir ve Bday ile reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

*Modeller\IdentityModels.cs* dosyasını açın ve doğum tarihi ve şehir özellikleri ekleyin:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

*Modelleri\AccountViewModels.cs* dosyasını ve ayarlanan doğum tarihini `ExternalLoginConfirmationViewModel`ve şehir merkezi özelliklerini .

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

*Denetleyiciler\AccountController.cs* dosyasını açın ve gösterildiği gibi `ExternalLoginConfirmation` eylem yönteminde doğum tarihi ve memleketi için kod ekleyin:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

*Görünümler\Hesap\ExternalLoginConfirmation.cshtml* dosyasına doğum tarihi ve şehir ekle:

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Facebook hesabınızı tekrar başvurunuzla kaydedebilmeniz ve yeni doğum tarihi ve şehir merkezi profil bilgilerini ekleyebileceğinizdoğrulayabilirsiniz diye üyelik veritabanını silin.

**Çözüm Gezgini'nden**Tüm **Dosyaları Göster** simgesini tıklatın, ardından *Veriyi Ekle\aspnet-MvcAuth-\_&lt;dateStamp&gt;.mdf'yi* tıklatın ve **Sil'i**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

**Araçlar** menüsünden **NuGet Paket Yöneticisi'ni**tıklatın, ardından Paket **Yöneticisi Konsolu'nu** (PMC) tıklatın. PMC'de aşağıdaki komutları girin.

1. Geçişleri Etkinleştir
2. Ekle-Geçiş Eklentisi
3. Güncelleme-Veritabanı

Uygulamayı çalıştırın ve bazı kullanıcılara giriş yapmak ve kayıt yaptırmak için FaceBook ve Google'ı kullanın.

## <a name="examine-the-membership-data"></a>Üyelik Verilerini İnceleyin

**Görünüm** menüsünde **Sunucu Gezgini'ni**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

**AspNetUsers'ı** sağ tıklatın ve **Tablo Verilerini Göster'i**tıklatın.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Ve `HomeTown` `BirthDate` alanlar aşağıda gösterilmiştir.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Uygulamanızdan Oturum Açma ve Başka Bir Hesapla Giriş

Facebook ile uygulamanızda oturum açar ve oturumunuzu başka bir Facebook hesabıyla (aynı tarayıcıyı kullanarak) yeniden oturum açmaya çalışırsanız, kullandığınız önceki Facebook hesabına hemen giriş yaparsınız. Başka bir hesap kullanmak için Facebook'a gidip Facebook'ta oturum açmanız gerekir. Aynı kural diğer üçüncü taraf kimlik doğrulama sağlayıcısı için de geçerlidir. Alternatif olarak, farklı bir tarayıcı kullanarak başka bir hesapla oturum açabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar

Bkz. Yahoo ve LinkedIn talimatları için Jerrie Pelser tarafından OWIN için Yahoo ve [LinkedIn OAuth güvenlik sağlayıcıları tanıtımı.](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Sosyal giriş düğmelerini etkinleştirmek için ASP.NET MVC 5 için Jerrie'nin Pretty sosyal giriş düğmelerine bakın.

Öğreticimi takip edin [Auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bu öğreticidevam eden ve aşağıdakileri gösteren Azure Uygulama Hizmeti'ne dağıtın:

1. Uygulamanızı Azure'a nasıl dağıtılayınız.
2. Nasıl rolleri ile uygulama güvenli.
3. [Zorunlu Https](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) ve [Yetkilendirme](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtreleri ile uygulamanızın güvenliğini sağlama.
4. Kullanıcı ve roller eklemek için üyelik API'sinin nasıl kullanılacağı.

Lütfen bu öğreticiyi nasıl beğendiğiniz ve neler geliştirebileceğimiz hakkında geri bildirimde bırakın. Ayrıca [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)adresinden yeni konular da isteyebilirsiniz. Hatta ASP.NET eklenecek yeni özellikleri isteyebilir ve oylayabilirsiniz. Örneğin, [kullanıcıları ve rolleri oluşturmak ve yönetmek](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use) için bir araca oy verebilirsiniz.

ASP.NET Dış Kimlik Doğrulama Hizmetlerinin nasıl çalıştığına ilişkin iyi bir açıklama için Robert McMurray'in [Dış Kimlik Doğrulama Hizmetleri](https://asp.net/web-api/overview/security/external-authentication-services)bölümüne bakın. Robert'ın makalesi, Microsoft ve Twitter kimlik doğrulamasını etkinleştirmede de ayrıntılı olarak yer alıyor. Tom Dykstra'nın mükemmel [EF/MVC öğreticisi](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework ile nasıl çalışılabildiğini gösterir.
