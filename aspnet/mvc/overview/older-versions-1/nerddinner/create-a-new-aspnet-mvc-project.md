---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Yeni bir ASP.NET MVC Projesi Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 1, temel NerdDinner uygulama yapısını nasıl yerleştirdiğinizi gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541487"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Yeni ASP.NET MVC Projesi Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 1 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 1, temel NerdDinner uygulama yapısını nasıl yerleştirdiğinizi gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner Adım 1:&gt;Dosya- Yeni Proje

Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express içindeki **Dosya-Yeni&gt;Proje** menü öğesini seçerek NerdDinner uygulamamıza başlayacağız.

Bu "Yeni Proje" iletişim kutusunu gündeme getirecektir. Yeni bir ASP.NET MVC uygulaması oluşturmak için, iletişim kutusunun sol tarafındaki "Web" düğümünü ve ardından sağdaki "ASP.NET MVC Web Uygulaması" proje şablonu seçilir:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Önemli: MVC ASP.NET indirdiğinizde ve yüklediğinizden emin olun , aksi takdirde Yeni Proje iletişim kutusunda gösterilmez. Henüz yüklemediyseniz [Microsoft Web Platform Installer'ın](https://www.microsoft.com/web/downloads/platform.aspx) V2'sini kullanabilirsiniz (ASP.NET MVC",&gt;"Web Platformu- Çerçeveler ve Çalışma Saatleri" bölümünde kullanılabilir).*

"NerdDinner" oluşturacağız ve oluşturmak için "ok" düğmesine tıklayacağız.

"Ok" Visual Studio'yu tıklattığımızda, yeni uygulama için de isteğe bağlı olarak bir birim test projesi oluşturmamızı gerektiren ek bir iletişim formu gündeme gelecektir. Bu birim test projesi, uygulamamızın işlevselliğini ve davranışını doğrulayan otomatik testler oluşturmamıza olanak tanır (bu öğreticide daha sonra nasıl yapılacağını ele alacağız).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

Yukarıdaki iletişim kutusundaki "Test çerçevesi" açılır bırakım, makineye yüklenen tüm kullanılabilir ASP.NET MVC birim test proje şablonlarıyla doldurulur. Sürümler NUnit, MBUnit ve XUnit için indirilebilir. Dahili Visual Studio Unit Test çerçevesi de desteklenir.

*Not: Visual Studio Unit Test Framework sadece Visual Studio 2008 Professional ve daha yüksek sürümlerle kullanılabilir. VS 2008 Standard Edition veya Visual Web Developer 2008 Express kullanıyorsanız, bu iletişim kutusunun gösterilebilmesi için ASP.NET MVC için NUnit, MBUnit veya XUnit uzantılarını indirmeniz ve yüklemeniz gerekir. Yüklü herhangi bir test çerçevesi yoksa iletişim kutusu görüntülenmez.*

Oluşturduğumuz test projesi için varsayılan "NerdDinner.Tests" adını ve "Visual Studio Unit Test" çerçeve seçeneğini kullanacağız. "Ok" düğmesine tıkladığımızda Visual Studio bizim için iki proje ile bir çözüm yaratacak - bir web uygulaması ve birim testleri için bir:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>NerdDinner dizin yapısının incelenmesi

Visual Studio ile yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, projeye otomatik olarak bir dizi dosya ve dizin ekler:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET MVC projelerinin varsayılan olarak altı üst düzey dizini bulunmaktadır:

| **Dizin** | **Amaç** |
| --- | --- |
| **/Denetleyiciler** | URL isteklerini işleyen Denetleyici sınıflarını nereye koyduğunuz |
| **/Modeller** | Verileri temsil eden ve işleyen sınıfları koyduğunuz yer |
| **/Görünümler** | Çıktı oluşturmadan sorumlu UI şablon dosyalarını nereye koyduğunuz |
| **/Komut Dosyaları** | JavaScript kitaplık dosyalarını ve komut dosyalarını koyduğunuz yer (.js) |
| **/İçerik** | CSS ve resim dosyalarını ve diğer dinamik olmayan/JavaScript olmayan içeriği koyduğunuz yer |
| **/Uygulama\_Verileri** | Okumak/yazmak istediğiniz veri dosyalarını depoladığınız yer. |

ASP.NET MVC bu yapıyı gerektirmez. Aslında, büyük uygulamalar üzerinde çalışan geliştiriciler genellikle uygulamayı daha yönetilebilir hale getirmek için genellikle birden çok projeye bölümlere ayırır (örneğin: veri modeli sınıfları genellikle web uygulamasından ayrı bir sınıf kitaplığı projesine gider). Ancak varsayılan proje yapısı, uygulama sorunlarımızı temiz tutmak için kullanabileceğimiz hoş bir varsayılan dizin kuralı sağlar.

/Controllers dizinini genişletdiğimizde Visual Studio'nun projeye varsayılan olarak iki denetleyici sınıfı -HomeController ve AccountController- eklediğini göreceğiz:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Görünüm dizini genişlettiğinde, üç alt dizin (/Ana Sayfa, /Hesap ve /Paylaşılan) yanı sıra bunların içinde birkaç şablon dosyası da varsayılan olarak projeye eklenmiştir:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/İçerik ve /Scriptds dizinlerini genişletdiğimizde, sitedeki tüm HTML'leri stillemek için kullanılan bir Site.css dosyasının yanı sıra uygulama içinde ASP.NET AJAX ve jQuery desteğine olanak tanıyan JavaScript kitaplıklarını da buluruz:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

NerdDinner.Tests projesini genişletirken denetleyici sınıflarımız için birim testleri içeren iki sınıf bulacağız:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio tarafından eklenen bu varsayılan dosyalar bize çalışan bir uygulama için temel bir yapı sağlar - ana sayfa, sayfa hakkında, hesap giriş/giriş/kayıt sayfaları ve işlenmemiş bir hata sayfası (hepsi kablolu ve kutunun dışında çalışma) ile birlikte.

### <a name="running-the-nerddinner-application"></a>NerdDinner Uygulamasını Çalıştırma

Hata **Ayıklama başlat veya&gt;Hata Ayıklama-** **&gt;Hata Ayıklama** menüsü öğelerini seçmeden projeyi çalıştırabiliriz:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Bu, Visual Studio ile birlikte gelen yerleşik ASP.NET Web sunucusunu başlatacak ve uygulamamızı çalıştıracaktır:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Yeni projemizin ana sayfası (URL: "/") çalıştığında:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

"Hakkında" sekmesine tıkladığınızda bir sayfa görüntülenir (URL: "/Ana Sayfa/Hakkında"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Sağ üstteki "Oturum Aç" bağlantısına tıkladığınızda giriş sayfası (URL: "/Account/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Giriş hesabımız yoksa, aşağıdakileri oluşturmak için kayıt bağlantısını (URL: "/Account/Register") tıklayabiliriz:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

Yeni projemizi oluşturduğumuzda, yukarıdaki ev, hakkında ve oturum açma/kayıt işlevini uygulamak için kod varsayılan olarak eklendi. Uygulamamızın başlangıç noktası olarak kullanacağız.

### <a name="testing-the-nerddinner-application"></a>NerdDinner Uygulamasını Test Etme

Visual Studio 2008'in Professional Edition veya daha yüksek sürümünü kullanıyorsak, projeyi test etmek için Visual Studio'daki yerleşik birim test IDE desteğini kullanabiliriz:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

Yukarıdaki seçeneklerden birini seçmek IDE içindeki "Test Sonuçları" bölmesini açacak ve yerleşik işlevselliği kapsayan yeni projemizde yer alan 27 birim testinde geçiş/başarısız durumu sağlayacaktır:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Bu öğreticinin ilerleyen saatlerinde otomatik sınama hakkında daha fazla konuşacağız ve uyguladığımız uygulama işlevselliğini kapsayan ek birim testleri ekleyeceğiz.

### <a name="next-step"></a>Sonraki Adım

Şu anda temel bir uygulama yapısına sahiptir. Şimdi uygulama [verilerimizi depolamak için bir veritabanı oluşturalım.](create-a-database.md)

> [!div class="step-by-step"]
> [Önceki](introducing-the-nerddinner-tutorial.md)
> [Sonraki](create-a-database.md)
