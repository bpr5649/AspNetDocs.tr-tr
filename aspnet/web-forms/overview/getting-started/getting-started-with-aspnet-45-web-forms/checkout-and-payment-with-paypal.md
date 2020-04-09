---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: PayPal ile Ödeme ve Ödeme | Microsoft Dokümanlar
author: Erikre
description: Bu öğretici ASP.NET serisi, 4.5 ASP.NET ve Microsoft Visual Studio Express 2013 for We...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676057"
---
# <a name="checkout-and-payment-with-paypal"></a>PayPal ile Kasa İşlemleri ve Ödeme

tarafından [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys Örnek Proje (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) İndir veya [E-kitap İndir (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici seri, web için ASP.NET 4.5 ve Web için Microsoft Visual Studio Express 2013 kullanarak ASP.NET bir Web Forms uygulaması oluşturmanın temellerini öğretecektir. [C# kaynak kodu ile](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) bir Visual Studio 2013 proje bu öğretici serisi eşlik etmek için kullanılabilir.

Bu öğretici, PayPal kullanarak kullanıcı yetkilendirme, kayıt ve ödeme içerecek şekilde Wingtip Toys örnek uygulamasını nasıl değiştirebilirsiniz açıklar. Yalnızca oturum açan kullanıcılar ürün satın alma yetkisine sahip olacaktır. ASP.NET 4.5 Web Forms proje şablonunun yerleşik kullanıcı kaydı işlevselliği zaten ihtiyacınız olan ın çoğunu içerir. PayPal Express Ödeme işlevini eklersiniz. Bu eğitimde PayPal geliştirici test ortamını kullanıyorsunuz, böylece gerçek para aktarılmaz. Eğitimin sonunda, alışveriş sepetine eklenecek ürünleri seçerek, ödeme düğmesini tıklatarak ve verileri PayPal test web sitesine aktararak uygulamayı test edeyim. PayPal test web sitesinde, gönderi ve ödeme bilgilerinizi onaylayacak ve satın alma işlemini onaylamak ve tamamlamak için yerel Wingtip Toys örnek uygulamasına geri döneceksiniz.

Ölçeklenebilirlik ve güvenliği ele alan çevrimiçi alışverişte uzmanlaşmış birkaç deneyimli üçüncü taraf ödeme işlemcisi vardır. ASP.NET geliştiricilerbir alışveriş ve satın alma çözümü uygulamadan önce bir üçüncü taraf ödeme çözümü kullanmanın avantajlarını göz önünde bulundurmalıdır.

> [!NOTE] 
> 
> Wingtip Toys örnek uygulaması, web geliştiricileri ASP.NET belirli ASP.NET kavram ve özellikleri gösterilecek şekilde tasarlanmıştır. Bu örnek uygulama ölçeklenebilirlik ve güvenlik açısından tüm olası durumlar için optimize edilmedi.

## <a name="what-youll-learn"></a>Öğrenecekleriniz:

- Bir klasördeki belirli sayfalara erişimi kısıtlama.
- Anonim bir alışveriş sepetinden bilinen bir alışveriş sepeti nasıl oluşturulur.
- Proje için SSL nasıl etkinleştirilir.
- Projeye bir OAuth sağlayıcısı nasıl eklenir?
- PayPal test ortamını kullanarak ürün satın almak için PayPal nasıl kullanılır?
- PayPal'daki ayrıntıları **DetailsView** denetiminde görüntüleme.
- PayPal'dan elde edilen ayrıntılarla Wingtip Toys uygulamasının veritabanını nasıl güncellenir?

## <a name="adding-order-tracking"></a>Sipariş İzleme Ekleme

Bu eğitimde, bir kullanıcının oluşturduğu siparişteki verileri izlemek için iki yeni sınıf oluşturursunuz. Sınıflar, sevkiyat bilgileri, satın alma toplamı ve ödeme onayı ile ilgili verileri izler.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Sipariş ve SiparişDetay Model Sınıfları ekle

Bu `Category`öğretici serinin başlarında, *Modeller* klasöründe , ve `Product` `CartItem` sınıflar oluşturarak kategoriler, ürünler ve alışveriş sepeti öğeleri için şema tanımlamıştır. Şimdi ürün siparişi ve sipariş ayrıntıları için şema tanımlamak için iki yeni sınıflar eklersiniz.

1. **Modeller** klasörüne *Order.cs*adlı yeni bir sınıf ekleyin.   
   Yeni sınıf dosyası düzenleyicide görüntülenir.
2. Varsayılan kodu aşağıdakilerle değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *Modeller* klasörüne *OrderDetail.cs* bir sınıf ekleyin.
4. Varsayılan kodu aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

Ve `Order` `OrderDetail` sınıflar satın alma ve sevkiyat için kullanılan sipariş bilgilerini tanımlamak için şema içerir.

Ayrıca, varlık sınıflarını yöneten ve veritabanına veri erişimi sağlayan veritabanı bağlam ı sınıfını güncelleştirmeniz gerekir. Bunu yapmak için, yeni oluşturulan Sipariş `OrderDetail` ve `ProductContext` model sınıflarını sınıfa eklersiniz.

1. **Çözüm Gezgini'nde** *ProductContext.cs* dosyasını bulun ve açın.
2. Vurgulanan kodu ProductContext.cs *dosyasına* aşağıda gösterildiği gibi ekleyin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Bu öğretici seride daha önce de belirtildiği *ProductContext.cs* gibi, `System.Data.Entity` ProductContext.cs dosyasındaki kod ad alanını ekler, böylece Entity Framework'ün tüm temel işlevlerine erişebilirsiniz. Bu işlevsellik, güçlü bir şekilde yazılan nesnelerle çalışarak verileri sorgulama, ekleme, güncelleştirme ve silme özelliğini içerir. Sınıftaki `ProductContext` yukarıdaki kod, yeni eklenen `Order` ve `OrderDetail` sınıflara Entity Framework erişimi ekler.

## <a name="adding-checkout-access"></a>Ödeme Erişimi Ekleme

Wingtip Toys örnek uygulaması, anonim kullanıcıların bir alışveriş sepetini incelemesine ve eklemesine olanak tanır. Ancak, anonim kullanıcılar alışveriş sepetine ekledikleri ürünleri satın almayı seçtiklerinde, sitede oturum açmaları gerekir. Oturum açtıktan sonra, ödeme ve satın alma işlemini işleyen Web uygulamasının kısıtlı sayfalarına erişebilirler. Bu kısıtlı sayfalar, uygulamanın *Kullanıma Para* klasöründe bulunur.

### <a name="add-a-checkout-folder-and-pages"></a>Ödeme Klasörü ve Sayfa Ekleme

Şimdi *Ödeme* klasörünü ve müşterinin ödeme işlemi sırasında göreceği sayfaları oluşturursunuz. Bu sayfaları daha sonra bu öğreticide güncelleştireceksiniz.

1. **Solution Explorer'da** proje adını **(Wingtip Toys)** sağ tıklatın ve **Yeni Klasör Ekle'yi**seçin. 

    ![PayPal ile Ödeme ve Ödeme - Yeni Klasör](checkout-and-payment-with-paypal/_static/image1.png)
2. Yeni *klasöre Ödeme*adını vereb'i adlandırın.
3. *Ödeme* klasörüne sağ tıklayın ve ardından**Yeni Öğe** **Ekle'yi**-&gt;seçin. 

    ![PayPal ile Ödeme ve Ödeme - Yeni Ürün](checkout-and-payment-with-paypal/_static/image2.png)
4. **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
5. Soldaki **Visual C#**  - &gt; **Web** şablonları grubunu seçin. Daha sonra, orta bölmeden, **Ana Sayfa ile Web Formu'nu**seçin ve *checkoutStart.aspx*adını koyun. 

    ![PayPal ile Ödeme ve Ödeme - Yeni Öğe Ekle İletişim Kutusu](checkout-and-payment-with-paypal/_static/image3.png)
6. Daha önce olduğu gibi, ana sayfa olarak *Site.Master* dosyasını seçin.
7. Yukarıdaki adımları kullanarak *Ödeme* klasörüne aşağıdaki ek sayfaları ekleyin:   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Web.config Dosyası Ekleme

*Ödeme* klasörüne yeni bir *Web.config* dosyası ekleyerek, klasörde bulunan tüm sayfalara erişimi kısıtlayabilirsiniz.

1. *Ödeme* klasörüne sağ tıklayın ve **Yeni Öğe** **Ekle'yi**  - &gt; seçin.  
   **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
2. Soldaki **Visual C#**  - &gt; **Web** şablonları grubunu seçin. Daha sonra, orta bölmeden **Web Yapılandırma Dosyası'nı**seçin, *Web.config*varsayılan adını kabul edin ve sonra **Ekle'yi**seçin.
3. *Web.config* dosyasındaki mevcut XML içeriğini aşağıdakilerle değiştirin:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web.config* dosyasını kaydedin.

*Web.config* dosyası, Web uygulamasının bilinmeyen tüm kullanıcılarının *Ödeme* klasöründe bulunan sayfalara erişiminin engellenmesi gerektiğini belirtir. Ancak, kullanıcı bir hesap kaydetmişse ve oturum açmışsa, bilinen bir kullanıcı dır ve *Ödeme* klasöründeki sayfalara erişebilir.

yapılandırmaASP.NET her *Web.config* dosyasının yapılandırma ayarlarını bulunduğu klasöre ve altındaki tüm alt dizinlere uyguladığı bir hiyerarşi izlediğini unutmayın.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Proje için SSL'yi etkinleştirme

 Secure Sockets Layer (SSL), Web sunucularının ve Web istemcilerinin şifreleme kullanımı yoluyla daha güvenli bir şekilde iletişim kurmasına olanak sağlamak için tanımlanan bir protokoldür. SSL kullanılmadığında, istemci ve sunucu arasında gönderilen veriler ağa fiziksel erişimi olan herkes tarafından paket koklamaya açıktır. Ayrıca, birkaç yaygın kimlik doğrulama düzenleri düz HTTP üzerinde güvenli değildir. Özellikle, Temel kimlik doğrulama ve formkimlik doğrulaması şifrelenmemiş kimlik bilgileri gönderir. Güvenli olması için bu kimlik doğrulama şemaları SSL kullanmalıdır. 

1. **Solution Explorer'da** **WingtipToys** projesini tıklatın ve ardından **Özellikler** penceresini görüntülemek için **F4** tuşuna basın.
2. `true` **SSL'yi Değiştir.**
3. **SSL URL'sini** kopyalayın, böylece daha sonra kullanabilirsiniz.   
 SSL URL'si daha önce SSL Web Siteleri oluşturmadığınız sürece olacaktır `https://localhost:44300/` (aşağıda gösterildiği gibi).   
    ![Proje Özellikleri](checkout-and-payment-with-paypal/_static/image4.png)
4. **Solution Explorer'da** **WingtipToys** projesini sağ tıklatın ve **Özellikler'i**tıklatın.
5. Sol sekmede **Web'i**tıklatın.
6. Daha önce kaydettiğiniz **SSL URL'sini** kullanmak için **Proje Url'sini** değiştirin.   
    ![Proje Web Özellikleri](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL+S**tuşuna basarak sayfayı kaydedin.
8. Uygulamayı çalıştırmak için **Ctrl+F5** tuşuna basın. Visual Studio, SSL uyarılarından kaçınmanızı sağlayacak bir seçenek görüntüler.
9. IIS Express SSL sertifikasına güvenmek ve devam etmek için **Evet'i** tıklatın.   
    ![IIS Express SSL sertifika detayları](checkout-and-payment-with-paypal/_static/image6.png)  
 Güvenlik Uyarısı görüntülenir.
10. Sertifikayı yerel host'unuza yüklemek için **Evet'i** tıklatın.   
    ![Güvenlik Uyarısı iletişim kutusu](checkout-and-payment-with-paypal/_static/image7.png)  
 Tarayıcı penceresi görüntülenir.

Artık SSL kullanarak Web uygulamanızı yerel olarak kolayca test edebilirsiniz.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 Sağlayıcı Ekle

ASP.NET Web Formları üyelik ve kimlik doğrulama için gelişmiş seçenekler sunar. Bu geliştirmeler OAuth içerir. OAuth web, mobil ve masaüstü uygulamalarından basit ve standart bir yöntemle güvenli yetkilendirme sağlayan açık bir protokoldür. ASP.NET Web Formları şablonu, Facebook, Twitter, Google ve Microsoft'u kimlik doğrulama sağlayıcısı olarak ortaya çıkarmak için OAuth'u kullanır. Bu öğretici kimlik doğrulama sağlayıcısı olarak yalnızca Google'ı kullansa da, kodu sağlayıcılardan herhangi birini kullanacak şekilde kolayca değiştirebilirsiniz. Diğer sağlayıcıları uygulamak için adımlar bu öğreticide göreceğiniz adımlara çok benzer.

Kimlik doğrulamaya ek olarak, öğretici yetkilendirmeyi uygulamak için rolleri de kullanır. Yalnızca `canEdit` role eklediğiniz kullanıcılar verileri değiştirebilir (kişileri oluşturabilir, düzenleyebilir veya silebilir).

> [!NOTE] 
> 
> Windows Live uygulamaları yalnızca çalışan bir web sitesi için canlı bir URL kabul eder, bu nedenle girişleri test etmek için yerel bir web sitesi URL'si kullanamazsınız.

Aşağıdaki adımlar, bir Google kimlik doğrulama sağlayıcısı eklemenize olanak sağlar.

1. *\_App Start\Startup.Auth.cs* dosyasını açın.
2. Yöntem aşağıdaki gibi görünecek `app.UseGoogleAuthentication()` şekilde yorum karakterleri yöntemden kaldırın: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google Geliştiriciler Konsolu'na](https://console.developers.google.com/)gidin. Ayrıca Google geliştirici e-posta hesabınızla (gmail.com) oturum açmanız gerekir. Google hesabınız **yoksa, hesap oluştur** bağlantısını seçin.   
   Ardından, Google Geliştiriciler **Konsolu'nu**görürsünüz.   
    ![Google Geliştiriciler Konsolu](checkout-and-payment-with-paypal/_static/image8.png)
4. Proje **Oluştur** düğmesini tıklatın ve bir proje adı ve kimliği girin (varsayılan değerleri kullanabilirsiniz). Ardından, **anlaşma onay kutusunu** ve **Oluştur** düğmesini tıklatın.  

    ![Google - Yeni Proje](checkout-and-payment-with-paypal/_static/image9.png)

   Birkaç saniye içinde yeni proje oluşturulacak ve tarayıcınız yeni projeler sayfasını görüntüleyecek.
5. Sol sekmesinde, **API'ler &amp; auth'u**tıklatın ve ardından **Kimlik Bilgileri'ni**tıklatın.
6. **OAuth**altında **Yeni İstemci Kimliği Oluştur'u** tıklatın.   
   **İstemci Kimliği Oluştur** iletişim kutusu görüntülenir.   
    ![Google - Müşteri Kimliği Oluşturma](checkout-and-payment-with-paypal/_static/image10.png)
7. **İstemci Kimliği Oluştur** iletişim kutusunda, uygulama türü için varsayılan **Web uygulamasını** saklayın.
8. Yetkili **JavaScript Origins'i** bu öğreticide daha önce kullandığınız`https://localhost:44300/` SSL URL'sine ayarlayın (başka SSL projeleri oluşturmadığınız sürece).   
   Bu URL, başvurunuzun kaynağıdır. Bu örnek için yalnızca localhost test URL'sini girersiniz. Ancak, yerel barındırma ve üretim için hesaba katılmak için birden çok URL girebilirsiniz.
9. Yetkili **Yeniden Yönlendirme URI'yi** aşağıdakilere ayarlayın: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Bu değer, OAuth kullanıcılarının google OAuth sunucusuyla iletişim kurmalarını ASP.NET URI'dir. Yukarıda kullandığınız SSL URL'sini hatırlayın (başka `https://localhost:44300/` SSL projeleri oluşturmadığınız sürece).
10. **İstemci Kimliği Oluştur** düğmesini tıklatın.
11. Google Geliştiriciler Konsolu'nun sol **menüsünde, Onay ekranı** menüsü öğesini tıklatın ve ardından e-posta adresinizi ve ürün adınızı ayarlayın. Formu tamamladığınızda **Kaydet'i**tıklatın.
12. **API'ler** menü öğesini tıklatın, aşağı kaydırın ve **Google+ API'nin**yanındaki **kapatma** düğmesini tıklatın.   
    Bu seçeneği kabul etmek Google+ API'yi etkinleştirecektir.
13. **Microsoft.Owin** NuGet paketini sürüm 3.0.0 olarak da güncelleştirmeniz gerekir.   
    **Araçlar** menüsünden **NuGet Paket Yöneticisi'ni** seçin ve ardından Çözüm için **Paketleri Yönet'i**seçin.  
    **NuGet Paketlerini Yönet** penceresinden **Microsoft.Owin** paketini bulup sürüm 3.0.0'a güncelleyin.
14. Visual Studio'da, `UseGoogleAuthentication` Istemci kimliğini ve **İstemci Sırrı'nı** kopyalayıp yönteme yapıştırarak **Client ID** *Startup.Auth.cs* sayfasının yöntemini güncelleştirin. Aşağıda gösterilen **İstemci Kimliği** ve **İstemci Gizli** değerleri örneklerdir ve çalışmaz. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Uygulamayı oluşturmak ve çalıştırmak için **CTRL+F5** tuşuna basın. Giriş **Yap** bağlantısını tıklayın.
16. Oturum **açmak için başka bir hizmeti kullan**, **Google'ı**tıklatın.  
    ![Oturum açma](checkout-and-payment-with-paypal/_static/image11.png)
17. Kimlik bilgilerinizi girmeniz gerekiyorsa, kimlik bilgilerinizi gireceğiniz google sitesine yönlendirilirsiniz.  
    ![Google - Oturum aç](checkout-and-payment-with-paypal/_static/image12.png)
18. Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz web uygulamasına izin vermeniz istenir.  
    ![Proje Varsayılan Hizmet Hesabı](checkout-and-payment-with-paypal/_static/image13.png)
19. **Kabul et**'e tıklayın. Artık Google hesabınızı kaydedebilirsiniz **WingtipToys** uygulamasının **Kayıt** sayfasına yönlendirilir.  
    ![Google Hesabınıza kaydolun](checkout-and-payment-with-paypal/_static/image14.png)
20. Gmail hesabınız için kullanılan yerel e-posta kaydı adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta takma adını (diğer bir şekilde kimlik doğrulama için kullandığınız e-posta) tutmak istersiniz. Yukarıda gösterildiği gibi **Giriş** Yap'ı tıklatın.

### <a name="modifying-login-functionality"></a>Giriş İşlevselliğini Değiştirme

Bu öğretici seride daha önce de belirtildiği gibi, kullanıcı kaydı işlevinin çoğu varsayılan olarak ASP.NET Web Formları şablonuna eklenmiştir. Şimdi `MigrateCart` varsayılan *Login.aspx* ve *Register.aspx* sayfalarını değiştirerek yöntemi aramalısınız. Yöntem, `MigrateCart` yeni oturum açmış bir kullanıcıyı anonim bir alışveriş sepetiyle ilişkilendirer. Wingtip Toys örnek uygulaması, kullanıcıyı ve alışveriş sepetini ilişkilendirerek, ziyaretler arasında kullanıcının alışveriş sepetini koruyabilecektir.

1. **Çözüm Gezgini'nde** *Hesap* klasörünü bulun ve açın.
2. Aşağıdaki gibi görünecek şekilde, sarı olarak vurgulanan kodu içerecek şekilde *Login.aspx.cs* adlı kod arkası sayfasını değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs* dosyasını kaydedin.

Şimdilik, `MigrateCart` yöntem için bir tanım olmadığı uyarısını yok sayabilirsiniz. Bu öğretici biraz daha sonra ekleyerek olacaktır.

*Login.aspx.cs* kod arkası dosyası bir Giriş yöntemini destekler. Login.aspx sayfasını inceleyerek, bu sayfada tıklandığında kod arkasındaki işleyiciyi `LogIn` tetikleyen bir "Oturum Aç" düğmesi olduğunu görürsünüz.

*Login.aspx.cs* `Login` yöntemi çağrıldığında, adlı `usersShoppingCart` alışveriş sepetinin yeni bir örneği oluşturulur. Alışveriş sepetinin kimliği (GUID) alınır ve `cartId` değişkene ayarlanır. Daha sonra, bu `MigrateCart` yöntem, `cartId` oturum açmış kullanıcının hem de adının bu yönteme geçirilmesiyle çağrılır. Alışveriş sepeti geçirildiğinde, anonim alışveriş sepetini tanımlamak için kullanılan GUID kullanıcı adı ile değiştirilir.

Kullanıcı oturum açarken alışveriş sepetini geçirmek için *Login.aspx.cs* kod arkası dosyasını değiştirmenin yanı sıra, kullanıcı yeni bir hesap oluşturup oturum açtıklarında alışveriş sepetini geçirmek için *Register.aspx.cs kod arkası dosyasını* da değiştirmeniz gerekir.

1. *Hesap* klasöründe, *Register.aspx.cs*adlı kod arkası dosyasını açın.
2. Kodu sarıya ekleyerek kodun arkası dosyasını değiştirin, böylece aşağıdaki gibi görünür:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs* dosyasını kaydedin. Bir kez daha, `MigrateCart` yöntem hakkında uyarı yoksay.

Olay işleyicisinde `CreateUser_Click` kullandığınız kodun `LogIn` yöntemde kullandığınız koda çok benzediğini unutmayın. Kullanıcı siteye kaydolduğunda veya siteye giriş yaptığında, `MigrateCart` yönteme bir çağrı yapılır.

## <a name="migrating-the-shopping-cart"></a>Alışveriş Sepetini Geçirme

Artık oturum açma ve kayıt işlemini güncelleştirdiğinizde, `MigrateCart` yöntemi kullanarak alışveriş sepetini geçirmek için kodu ekleyebilirsiniz.

1. **Çözüm Gezgini'nde,** *Mantık* klasörünü bulun ve *ShoppingCartActions.cs* sınıf dosyasını açın.
2. *ShoppingCartActions.cs* dosyasındaki kod aşağıdaki gibi görünsin, böylece *ShoppingCartActions.cs* dosyasındaki varolan koda sarı renkle vurgulanan kodu ekleyin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

Yöntem, `MigrateCart` kullanıcının alışveriş sepetini bulmak için varolan cartId'i kullanır. Ardından, kod tüm alışveriş sepeti öğeleri ni döngüler ve `CartId` özelliği `CartItem` (şema tarafından belirtildiği gibi) oturum açmış kullanıcı adı ile değiştirir.

### <a name="updating-the-database-connection"></a>Veritabanı Bağlantısını Güncelleme

**Önceden oluşturulmuş** Wingtip Toys örnek uygulamasını kullanarak bu öğreticiyi takip ediyorsanız, varsayılan üyelik veritabanını yeniden oluşturmanız gerekir. Varsayılan bağlantı dizesini değiştirerek, uygulama bir sonraki çalıştığında üyelik veritabanı oluşturulur.

1. *Web.config* dosyasını projenin kökünden açın.
2. Varsayılan bağlantı dizesini aşağıdaki gibi görünecek şekilde güncelleştirin:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>PayPal'ı Entegre Etme

PayPal, çevrimiçi satıcıların ödemelerini kabul eden web tabanlı bir faturalandırma platformudur. Bu öğretici, daha sonra PayPal'ın Express Checkout işlevini uygulamanız içine nasıl entegre ediletacağınızı açıklar. Ekspres Ödeme, müşterilerinizin alışveriş sepetine ekledikleri öğelerin ücretini ödemek için PayPal'ı kullanmasına olanak tanır.

### <a name="create-paypal-test-accounts"></a>PayPal Test Hesapları Oluşturma

PayPal test ortamını kullanmak için bir geliştirici test hesabı oluşturmanız ve doğrulamanız gerekir. Geliştirici test hesabını bir alıcı test hesabı ve satıcı test hesabı oluşturmak için kullanırsınız. Geliştirici test hesabı kimlik bilgileri, Wingtip Toys örnek uygulamasının PayPal test ortamına erişmesine de olanak sağlar.

1. Tarayıcıda PayPal geliştirici test sitesine gidin:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal geliştirici hesabınız yoksa, **Kaydol'u**tıklayarak ve kaydolma adımlarını izleyerek yeni bir hesap oluşturun. Mevcut bir PayPal geliştirici hesabınız **varsa, Giriş Yap'ı**tıklayarak oturum açın. Wingtip Toys örnek uygulamasını daha sonra bu eğitimde test etmek için PayPal geliştirici hesabınızın olması gerekir.
3. PayPal geliştirici hesabınıza yeni kaydolduysanız, PayPal geliştirici hesabınızı PayPal ile doğrulamanız gerekebilir. PayPal'ın e-posta hesabınıza gönderdiği adımları izleyerek hesabınızı doğrulayabilirsiniz. PayPal geliştirici hesabınızı doğruladıktan sonra PayPal geliştirici test sitesine tekrar giriş yapın.
4. PayPal geliştirici hesabınızla PayPal geliştirici sitesine giriş yaptıktan sonra, zaten hesabınız yoksa bir PayPal alıcı test hesabı oluşturmanız gerekir. Bir alıcı test hesabı oluşturmak için PayPal sitesinde **Uygulamalar** sekmesini tıklatın ve ardından **Sandbox hesaplarını**tıklatın.   
 **Sandbox test hesapları** sayfası gösterilir.   

    > [!NOTE] 
    > 
    > PayPal Geliştirici sitesi zaten bir satıcı test hesabı sağlar.

    ![PayPal ile Ödeme ve Ödeme - Sandbox test hesapları](checkout-and-payment-with-paypal/_static/image15.png)
5. Sandbox test hesapları sayfasında **Hesap Oluştur'u**tıklatın.
6. Test **hesabı oluştur** sayfasında, seçtiğiniz bir alıcı test hesabı e-postası ve parolasını seçin.   

    > [!NOTE] 
    > 
    > Bu eğitimin sonunda Wingtip Toys örnek uygulamasını test etmek için alıcı nın e-posta adreslerine ve şifresine ihtiyacınız olacaktır.

    ![PayPal ile Ödeme ve Ödeme - Sandbox test hesapları](checkout-and-payment-with-paypal/_static/image16.png)
7. **Hesap Oluştur** düğmesini tıklatarak alıcı test hesabını oluşturun.  
 **Sandbox Test hesapları** sayfası görüntülenir. 

    ![PayPal ile Ödeme ve Ödeme - PayPal Hesapları](checkout-and-payment-with-paypal/_static/image17.png)
8. **Sandbox test hesapları** sayfasında **kolaylaştırıcı** e-posta hesabını tıklatın.  
    **Profil** ve **Bildirim** seçenekleri görüntülenir.
9. **Profil** seçeneğini seçin ve satıcı test hesabı için API kimlik bilgilerinizi görüntülemek için **API kimlik bilgilerini** tıklatın.
10. TEST API kimlik bilgilerini not defterine kopyalayın.

Wingtip Toys örnek uygulamasından PayPal test ortamına API aramaları yapmak için görüntülenen Klasik TEST API kimlik bilgilerinize (Kullanıcı Adı, Parola ve İmza) ihtiyacınız olacaktır. Bir sonraki adımda kimlik bilgilerini eklersiniz.

### <a name="add-paypal-class-and-api-credentials"></a>PayPal Sınıfı ve API Kimlik Bilgileri Ekleme

PayPal kodunun çoğunluğunu tek bir sınıfa yerleştireceksiniz. Bu sınıf PayPal ile iletişim kurmak için kullanılan yöntemleri içerir. Ayrıca, PayPal kimlik bilgilerinizi bu sınıfa eklersiniz.

1. Visual Studio içindeki Wingtip Toys örnek uygulamasında **Mantık** klasörüne sağ tıklayın ve **ardından Yeni Öğe** **Ekle'yi**  - &gt; seçin.   
   **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
2. Soldaki **Yüklü** bölmeden **Visual C#** altında **Kod'u**seçin.
3. Orta bölmeden **Sınıf'ı**seçin. Bu yeni sınıf **PayPalFunctions.cs.**
4. **Ekle**’ye tıklayın.  
   Yeni sınıf dosyası düzenleyicide görüntülenir.
5. Varsayılan kodu aşağıdaki kodla değiştirin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. PayPal test ortamına işlev çağrıları yapabilmeniz için bu eğitimde daha önce görüntülediğiniz Merchant API kimlik bilgilerini (Kullanıcı adı, Parola ve İmza) ekleyin.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> Bu örnek uygulamada sadece bir C# dosyasına (.cs) kimlik bilgileri ekliyorsunuz. Ancak, uygulanan bir çözümde, kimlik bilgilerinizi yapılandırma dosyasında şifrelemeyi düşünmelisiniz.

NVPAPICaller sınıfı PayPal işlevselliğinin çoğunluğunu içerir. Sınıftaki kod, PayPal test ortamından bir test satın alma işlemi yapmak için gereken yöntemleri sağlar. Aşağıdaki üç PayPal işlevi satın alma işlemleri yapmak için kullanılır:

- `SetExpressCheckout`Işlev
- `GetExpressCheckoutDetails`Işlev
- `DoExpressCheckoutPayment`Işlev

Yöntem, `ShortcutExpressCheckout` alışveriş sepetinden test satın alma bilgilerini ve `SetExpressCheckout` ürün bilgilerini toplar ve PayPal işlevini çağırır. Yöntem, `GetCheckoutDetails` satın alma ayrıntılarını `GetExpressCheckoutDetails` onaylar ve test satın alma işlemini yapmadan önce PayPal işlevini çağırır. Yöntem, `DoCheckoutPayment` PayPal işlevini arayarak test ortamından test satın alımını `DoExpressCheckoutPayment` tamamlar. Kalan kod, dizeleri kodlama, dizeleri çözme, dizileri işleme ve kimlik bilgilerini belirleme gibi PayPal yöntemlerini ve işlemini destekler.

> [!NOTE] 
> 
> PayPal, [PayPal'ın API belirtimine](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)göre isteğe bağlı satın alma ayrıntılarını eklemenize olanak tanır. Wingtip Toys örnek uygulamasında kodu genişleterek, yerelleştirme ayrıntılarını, ürün açıklamalarını, vergiyi, müşteri hizmetleri numarasını ve diğer birçok isteğe bağlı alanı ekleyebilirsiniz.

**KısayolExpressCheckout** yönteminde belirtilen iade ve iptal URL'lerinin bir bağlantı noktası numarası kullandığına dikkat edin.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web Developer SSL kullanarak bir web projesi çalıştırdığında, genellikle 44300 bağlantı noktası web sunucusu için kullanılır. Yukarıda gösterildiği gibi, bağlantı noktası numarası 44300'dür. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görebilirsiniz. Bu eğitimin sonunda Wingtip Toys örnek uygulamasını başarılı bir şekilde çalıştırabilmeniz için bağlantı noktası numaranızın kodda doğru şekilde ayarlanması gerekir. Bu öğreticinin bir sonraki bölümünde, yerel ana bağlantı noktası numarasının nasıl alınıp PayPal sınıfının güncelleştirilen nasıl güncelleştirilen açıklanmaktadır.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal Sınıfındaki LocalHost Bağlantı Noktası Numarasını Güncelleştir

Wingtip Toys örnek uygulaması, PayPal test sahasına gidip Wingtip Toys örnek uygulamasının yerel örneğine geri dönerek ürünleri satın alır. PayPal'ın doğru URL'ye geri dönmesi için, yukarıda belirtilen PayPal kodunda yerel olarak çalışan örnek uygulamanın bağlantı noktası numarasını belirtmeniz gerekir.

1. **Solution Explorer'da** proje adını **(WingtipToys)** sağ tıklatın ve **Özellikler'i**seçin.
2. Sol sütunda **Web** sekmesini seçin.
3. **Proje Url** kutusundan bağlantı noktası numarasını alın.
4. Gerekirse, web `returnURL` uygulamanızın bağlantı noktası`NVPAPICaller`numarasını kullanmak için *PayPalFunctions.cs* dosyasındaki Ve PayPal sınıfını güncelleyin: `cancelURL`   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Artık eklediğiniz kod, yerel Web uygulamanız için beklenen bağlantı noktasıyla eşleşecek. PayPal yerel makinenizdeki doğru URL'ye geri dönebilir.

### <a name="add-the-paypal-checkout-button"></a>PayPal Ödeme Düğmesini Ekle

Örnek uygulamaya birincil PayPal işlevleri eklendiğiniz için, bu işlevleri çağırmak için gereken biçimlendirmeyi ve kodu eklemeye başlayabilirsiniz. İlk olarak, kullanıcının alışveriş sepeti sayfasında göreceği ödeme düğmesini eklemeniz gerekir.

1. *ShoppingCart.aspx* dosyasını açın.
2. Dosyanın altına gidin ve `<!--Checkout Placeholder -->` yorumu bulun.
3. İşaretlemenin aşağıdaki `ImageButton` gibi değiştirilmesi için yorumu bir denetimle değiştirin:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs* dosyasında, dosyanın `UpdateBtn_Click` sonuna yakın olay işleyicisi `CheckOutBtn_Click` sonra, olay işleyicisi ekleyin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. Ayrıca *ShoppingCart.aspx.cs* dosyasında, yeni resim `CheckoutBtn`düğmesine aşağıdaki gibi başvurulan , bir referans ekleyin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Değişikliklerinizi hem *ShoppingCart.aspx* dosyasına hem de *ShoppingCart.aspx.cs* dosyasına kaydedin.
7. Menüden Hata **Ayıklama**-&gt;**WingtipToys'u**seçin.  
   Proje, yeni eklenen **ImageButton** denetimi yle yeniden oluşturulacaktır.

### <a name="send-purchase-details-to-paypal"></a>Satın Alma Ayrıntılarını PayPal'a Gönder

Kullanıcı alışveriş sepeti sayfasındaki **Ödeme** düğmesini *(ShoppingCart.aspx)* tıklattığında, satın alma işlemine başlar. Aşağıdaki kod, ürünleri satın almak için gereken ilk PayPal işlevini çağırır.

1. *Ödeme* klasöründen, *CheckoutStart.aspx.cs*adlı kod arkası dosyasını açın.   
   Kod arkasındaki dosyayı açtığından emin olun.
2. Varolan kodu aşağıdakilerle değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Uygulamanın kullanıcısı alışveriş sepeti **sayfasındaki Ödeme** düğmesini tıklattığında, tarayıcı *CheckoutStart.aspx* sayfasına yönlendirilir. *CheckoutStart.aspx* sayfası `ShortcutExpressCheckout` yüklendiğinde, yöntem çağrılır. Bu noktada, kullanıcı PayPal test web sitesine aktarılır. PayPal sitesinde, kullanıcı PayPal kimlik bilgilerini girer, satın alma ayrıntılarını inceler, PayPal sözleşmesini kabul eder `ShortcutExpressCheckout` ve yöntemin tamamlandığı Wingtip Toys örnek uygulamasına geri döner. Yöntem tamamlandığında, kullanıcıyı `ShortcutExpressCheckout` yöntemde belirtilen *CheckoutReview.aspx* sayfasına yönlendirir. `ShortcutExpressCheckout` Bu, kullanıcının Wingtip Toys örnek uygulamasından sipariş ayrıntılarını gözden geçirmesine olanak tanır.

### <a name="review-order-details"></a>Sipariş Ayrıntılarını İncele

PayPal döndükten sonra, Wingtip Toys örnek uygulamanın *CheckoutReview.aspx* sayfası sipariş ayrıntılarını görüntüler. Bu sayfa, kullanıcının ürünleri satın almadan önce sipariş ayrıntılarını gözden geçirmesine olanak tanır. *CheckoutReview.aspx* sayfası aşağıdaki gibi oluşturulmalıdır:

1. *Ödeme* klasöründe *CheckoutReview.aspx*adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdakilerle değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. *CheckoutReview.aspx.cs* adlı kod arkasındaki sayfayı açın ve varolan kodu aşağıdakilerle değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView** denetimi, PayPal'dan döndürülen sipariş ayrıntılarını görüntülemek için kullanılır. Ayrıca, yukarıdaki kod sipariş ayrıntılarını Wingtip Toys veritabanına `OrderDetail` nesne olarak kaydeder. Kullanıcı **Tam Sipariş** düğmesini tıklattığında, *CheckoutComplete.aspx* sayfasına yönlendirilir.

> [!NOTE] 
> 
> **İpucu**
> 
> *CheckoutReview.aspx* sayfasının biçimlendirmesinde, etiketin `<ItemStyle>` sayfanın alt **kısmındaki DetailsView** denetimindeki öğelerin stilini değiştirmek için kullanıldığını unutmayın. Sayfayı Tasarım **Görünümü'nde** görüntüleyerek (Visual Studio'nun sol alt köşesinde **Tasarım'ı** seçerek), **ardından DetailsView** denetimini seçerek ve **Smart Tag'i** (denetimin sağ üst köşesindeki ok simgesi) seçerek **DetailsView Görevleri'ni**görebilirsiniz.
> 
> ![PayPal ile Ödeme ve Ödeme - Alanları Edin](checkout-and-payment-with-paypal/_static/image18.png)
> 
> **Alanları Edit'i**seçerek, **Alanlar** iletişim kutusu görüntülenir. Bu iletişim **kutusunda, DetailsView** denetiminin **ItemStyle**, gibi görsel özelliklerini kolayca denetleyebilirsiniz.
> 
> ![PayPal ile Ödeme ve Ödeme - Alanlar İletişim](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Satın Alma'yı Tamamla

*CheckoutComplete.aspx* sayfası PayPal'dan satın alma işlemini yapar. Yukarıda belirtildiği gibi, uygulama *Nın CheckoutComplete.aspx* sayfasına gitmeden önce kullanıcının **Sipariş'i Tamamla** düğmesine tıklaması gerekir.

1. *Ödeme* klasöründe *CheckoutComplete.aspx*adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdakilerle değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs* adlı kod arkası sayfasını açın ve varolan kodu aşağıdakilerle değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

*CheckoutComplete.aspx* sayfası `DoCheckoutPayment` yüklendiğinde, yöntem çağrılır. Daha önce de `DoCheckoutPayment` belirtildiği gibi, yöntem PayPal test ortamından satın alma tamamlar. PayPal siparişin satın alımını tamamladıktan *sonra, CheckoutComplete.aspx* sayfası alıcıya bir ödeme hareketi `ID` görüntüler.

### <a name="handle-cancel-purchase"></a>Satın Almayı İptal Et

Kullanıcı satın almayı iptal etmeye karar verirse, siparişlerinin iptal edildiğini görecekleri *CheckoutCancel.aspx* sayfasına yönlendirilir.

1. *CheckoutCancel.aspx* adlı sayfayı *Ödeme* klasöründe açın.
2. Varolan biçimlendirmeyi aşağıdakilerle değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Satınalma Hatalarını Işleme

Satın alma işlemi sırasındaki hatalar *CheckoutError.aspx* sayfası tarafından işlenir. *CheckoutStart.aspx* sayfasının, *CheckoutReview.aspx* sayfasının ve *CheckoutComplete.aspx* sayfasının kod arkası, bir hata oluşursa *CheckoutError.aspx* sayfasına yönlendirecektir.

1. *Ödeme* klasöründe *CheckoutError.aspx* adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdakilerle değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*Ödeme Hatası.aspx* sayfası, ödeme işlemi sırasında bir hata oluştuğunda hata ayrıntılarıyla birlikte görüntülenir.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Ürünleri nasıl satın alsüreceğiniziçin uygulamayı çalıştırın. PayPal test ortamında çalışacağınızı unutmayın. Gerçek para değiş tokuş edilsin.

1. Tüm dosyalarınızın Visual Studio'ya kaydolduğundan emin olun.
2. Bir Web tarayıcısı [https://developer.paypal.com](https://developer.paypal.com/)açın ve 'ye gidin.
3. Bu eğitimde daha önce oluşturduğunuz PayPal geliştirici hesabınızla giriş yapın.  
   PayPal'ın geliştirici sandbox'ı için, ekspres [https://developer.paypal.com](https://developer.paypal.com/) ödemeyi test etmek için oturum açmanız gerekir. Bu yalnızca PayPal'ın sandbox testi için geçerlidir, PayPal'ın canlı ortamı için değil.
4. Visual Studio'da Wingtip Toys örnek uygulamasını çalıştırmak için **F5** tuşuna basın.  
   Veritabanı yeniden oluşturulduktan sonra, tarayıcı açılır ve *Varsayılan.aspx* sayfasını gösterir.
5. "Arabalar" gibi ürün kategorisini seçip her ürünün yanındaki **Sepete Ekle'yi** tıklatarak alışveriş sepetine üç farklı ürün ekleyin.  
   Alışveriş sepeti seçtiğiniz ürünü görüntüler.
6. Ödeme yapmak için **PayPal** düğmesini tıklatın. 

    ![PayPal ile Ödeme ve Ödeme - Sepet](checkout-and-payment-with-paypal/_static/image20.png)

   Check-out, Wingtip Toys örnek uygulaması için bir kullanıcı hesabınız olması gerekir.
7. Mevcut bir gmail.com e-posta hesabıyla oturum açmak için sayfanın sağındaki **Google** bağlantısını tıklayın.  
   gmail.com bir hesabınız yoksa, [www.gmail.com'da](https://www.gmail.com/)test amacıyla bir hesap oluşturabilirsiniz. "Kaydol"u tıklatarak standart bir yerel hesap da kullanabilirsiniz. 

    ![PayPal ile Ödeme ve Ödeme - Giriş Yap](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail hesabınız ve şifrenizle oturum açın. 

    ![PayPal ile Ödeme ve Ödeme - Gmail Oturum Aç](checkout-and-payment-with-paypal/_static/image22.png)
9. Gmail hesabınızı Wingtip Toys örnek uygulama kullanıcı adınıza kaydetmek için **Giriş** Yap düğmesini tıklayın. 

    ![PayPal ile Ödeme ve Ödeme - Register Hesabı](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal test sitesinde, bu eğitimde daha önce oluşturduğunuz **alıcı** e-posta adresinizi ve parolanızı ekleyin ve ardından **Giriş Yap** düğmesini tıklatın. 

    ![PayPal ile Ödeme ve Ödeme - PayPal Oturum Aç](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal politikasını kabul edin ve **Kabul et ve Devam et** düğmesini tıklayın.  
    Bu sayfanın yalnızca bu PayPal hesabını ilk kez kullandığınızda görüntülendiğini unutmayın. Yine bu bir test hesabı olduğunu unutmayın, hiçbir gerçek para alışverişi olduğunu. 

    ![PayPal ile Ödeme ve Ödeme - PayPal Politikası](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal test ortamı inceleme sayfasındaki sipariş bilgilerini inceleyin ve **Devam et'i**tıklatın. 

    ![PayPal ile Ödeme ve Ödeme - İnceleme Bilgileri](checkout-and-payment-with-paypal/_static/image26.png)
13. *CheckoutReview.aspx* sayfasında, sipariş miktarını doğrulayın ve oluşturulan sevkiyat adresini görüntüleyin. Ardından **Siparişi Tamamla** düğmesini tıklatın. 

    ![PayPal ile Ödeme ve Ödeme - Sipariş İnceleme](checkout-and-payment-with-paypal/_static/image27.png)
14. **CheckoutComplete.aspx** sayfası ödeme işlem kimliğiyle görüntülenir. 

    ![PayPal ile Ödeme ve Ödeme - Checkout Tamamlandı](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Veritabanını Gözden Geçirme

Uygulamayı çalıştırdıktan sonra Wingtip Toys örnek uygulama veritabanında güncellenen verileri inceleyerek, uygulamanın ürünlerin satın alımını başarıyla kaydettiğini görebilirsiniz.

*Wingtiptoys.mdf* veritabanı dosyasında yer alan verileri, bu öğretici seride daha önce yaptığınız gibi **Veritabanı Gezgini** penceresini (Visual Studio'daki**Server Explorer** penceresi) kullanarak inceleyebilirsiniz.

1. Hala açıksa tarayıcı penceresini kapatın.
2. Visual Studio'da, **Uygulama\_Verileri** klasörünü genişletmenize olanak sağlamak için **Solution Explorer'ın** üst kısmındaki Tüm **Dosyaları Göster** simgesini seçin.
3. **Uygulama\_Verileri** klasörünü genişletin.  
 Klasör için Tüm **Dosyaları Göster** simgesini seçmeniz gerekebilir.
4. *Wingtiptoys.mdf* veritabanı dosyasına sağ tıklayın ve **Aç'ı**seçin.  
    **Sunucu Gezgini** görüntülenir.
5. **Tablolar** klasörünü genişletin.
6. **Siparişler**tablosuna sağ tıklayın ve **Tablo Verilerini Göster'i**seçin.  
 **Siparişler** tablosu görüntülenir.
7. Başarılı işlemleri onaylamak için **PaymentTransactionID** sütununa inceleyin. 

    ![PayPal ile Ödeme ve Ödeme - Veritabanını İncele](checkout-and-payment-with-paypal/_static/image29.png)
8. **Siparişler** tablosu penceresini kapatın.
9. Sunucu Gezgini'nde, **OrderDetails** tablosunu sağ tıklatın ve **Tablo Verilerini Göster'i**seçin.
10. **OrderDetails** `Username` tablosundaki `OrderId` ve değerleri gözden geçirin. Bu değerlerin **Siparişler** `OrderId` tablosunda yer alan değerlerle `Username` eşleşip tamamlanadığını unutmayın.
11. **OrderDetails** tablosu penceresini kapatın.
12. Wingtip Toys veritabanı dosyasına *(Wingtiptoys.mdf)* sağ tıklayın ve **Bağlantıyı Kapat'ı**seçin.
13. **Çözüm Gezgini** penceresini görmüyorsanız, Çözüm Gezgini'ni yeniden göstermek için **Solution Explorer** Sunucu Gezgini penceresinin altındaki **Çözüm Gezgini'ni** tıklatın. **Server Explorer**

## <a name="summary"></a>Özet

Bu öğreticide, ürün satın alımını izlemek için sipariş ve sipariş detay şemalarını eklediniz. Ayrıca PayPal işlevini Wingtip Toys örnek uygulamasına entegre ettiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Yapılandırmaya Genel Bakış](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Üyelik, OAuth ve SQL Veritabanı ile Güvenli ASP.NET Web Formları Uygulamasını Azure Uygulama Hizmetine Dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure - Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Disclaimer

Bu öğretici örnek kod içerir. Bu tür örnek kod herhangi bir garanti olmadan "olduğu gibi" sağlanır. Buna göre, Microsoft örnek kodun doğruluğunu, bütünlüğünü veya kalitesini garanti etmez. Örnek kodu kendi riskinizle kullanmayı kabul edersiniz. Microsoft, herhangi bir örnek kodun kullanımı sonucunda ortaya çıkan herhangi bir örnek kod, içerik veya herhangi bir kayıp veya hasar da dahil ancak bunlarla sınırlı olmamak üzere hiçbir şekilde size karşı sorumlu olmayacaktır. Burada size tebliğ edilmiş ve microsoft'u, burada ifade edilen görüşler dahil, ilettiğiniz, kullandığınız veya bunlarla sınırlı olmamak üzere yayınladığınız, ilettiğiniz, kullandığınız veya bunlarla sınırlı olmamak üzere, bunlarla sınırlı olmamak kaydıyla, bunlarla sınırlı olmamak kaydıyla, her türlü kayıp, kayıp, yaralanma veya hasardan zarar görme, zarar ve zarara karşı tazmin etmeyi, kaydetmeyi ve bunlara karşı tutmayı kabul edeyimsiniz.

> [!div class="step-by-step"]
> [Önceki](shopping-cart.md)
> [Sonraki](membership-and-administration.md)
