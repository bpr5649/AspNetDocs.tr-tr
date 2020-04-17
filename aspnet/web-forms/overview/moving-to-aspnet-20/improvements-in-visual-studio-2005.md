---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005'te Gelişmeler | Microsoft Dokümanlar
author: rick-anderson
description: Visual Studio 2005, Web uygulama geliştiricileri, Web projelerinde yapılan iyileştirmeler ve geliştirmelerin uzun bir listesini sağlar.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542995"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005’teki Geliştirmeler

[Microsoft](https://github.com/microsoft) tarafından

> Visual Studio 2005, Web uygulama geliştiricileri, Web projelerinde yapılan iyileştirmeler ve geliştirmelerin uzun bir listesini sağlar.

Visual Studio 2005, Web uygulama geliştiricileri, Web projelerinde yapılan iyileştirmeler ve geliştirmelerin uzun bir listesini sağlar. Visual Studio .NET 2002 ve 2003 kadar güçlü, Web projeleri ele şekilde birçok şikayet vardı. Visual Studio 2005, bu şikayetleri gidermek için önemli sayıda yeni özellik ekler. Visual Studio .NET 2003 web uygulamalarının derlemesini ele alış şeklini tercih edenler için [Web Uygulama Projeleri](https://go.microsoft.com/fwlink/?LinkId=57870)bölümüne bakın.

Bu modülde, Web proje oluşturma, yönetimi ve geliştirme deki geliştirmeleri iyi kaplar. Daha sonraki bir modülde, Web projeleri oluşturma ve dağıtma daki gelişmeleri iyi bir şekilde kapsar.

## <a name="frontpage-server-extensions"></a>FrontPage Sunucu Uzantıları

Visual Studio .NET 2002 ve 2003, Web projeleri oluşturmak veya oluşturmak için kutunun üzerinde FrontPage Server Uzantıları gerekti. Geliştiricilerin iki farklı erişim modu (FrontPage Server Uzantıları veya Dosya erişim modu) arasında bir seçim vardı, her ikisi de IIS, vb uygulama kökü ayarı gibi görevleri gerçekleştirmek için FrontPage Server Uzantıları kullanılır.

Visual Studio 2005, yerel projeler için FrontPage Sunucu Uzantılarına olan güveni ortadan kaldırır. Visual Studio 2005 artık FrontPage Server Uzantılarını kullanmak yerine doğrudan IIS metatabanına erişebiliyor. Visual Studio 2005 ayrıca FrontPage Server Uzantıları gerektirmeden uzaktan proje erişimi ne olanak sağlar FTP için destek ekler.

Projelerinde FrontPage Server Uzantılarını kullanmak isteyen geliştiriciler için seçenek hala kullanılabilir. Ancak, ASP.NET geliştirici topluluğundan gelen güçlü geri bildirimlere dayanarak, bu bir gereklilik değildir.

> [!NOTE]
> FrontPage Sunucu Uzantıları hala uzak proje oluşturma, açılış, vb için gereklidir.

## <a name="aspnet-development-server"></a>ASP.NET Geliştirme Sunucusu

Visual Studio 2005, ASP.NET Development Server adlı yeni bir Web sunucusuyla birlikte çalışıyor. (Bu Web sunucusu daha önce Cassini olarak biliniyordu.)

ASP.NET Geliştirme Sunucusu'nun çeşitli avantajları vardır.

- Artık Yönetici olmayanların bir Web sunucusuna karşı hata ayıklama geliştirmesi ve hata ayıklama ları artık mümkündür.
- ASP.NET Geliştirme Sunucusu, sanal dizinleri dosya sistemindeki herhangi bir konuma dinamik olarak eşleyerek esnek proje konumları sağlar.
- Windows XP Professional'da zaten IIS kullanan kullanıcılar artık IIS'deki Varsayılan Web Sitelerinin dosya veya klasör yapısını etkilemeyecek yeni Web uygulamaları oluşturabilecektir.

ASP.NET Geliştirme Sunucusu'ndan yararlanmak için özel bir yapılandırma gerekmez. Dosya sisteminde barındırılan bir Web projesi debugged veya göz atıldığında, Visual Studio 2005 otomatik olarak isteği hizmet için rasgele bir bağlantı noktasında ASP.NET Geliştirme Sunucusu bir örnek başlatacak.

Daha fazla bilgi daha sonra bu modülde ASP.NET Geliştirme Sunucusu'nda ele alınacaktır.

## <a name="improved-file-management"></a>Geliştirilmiş Dosya Yönetimi

Visual Studio 2002 ve 2003'te, bir proje dosyası (VB.NET için vbproj ve C#için .csproj) Web uygulamasındaki tüm dosyalarda bilgi depolatılır. Çözüm Gezgini ekranı proje dosyasındaki dosya bilgilerine dayanır. Bu nedenle, Solution Explorer genellikle dış düzenleyicilerin kullanıldığı durumlarda yanlış bilgiler görüntüler. Visual Studio 2002 ve 2003 genellikle dosya değişikliklerinin üzerine yazar veya dosyaların en son sürümünü görüntülemez.

Visual Studio 2005 proje dosyasını ortadan kaldırıyor. Bunun yerine, dosya ve klasör bilgilerini doğrudan diskten okur ve projenizdeki dosyaların doğru bir şekilde görüntülenmesini sağlar. Visual Studio 2002 ve 2003'teki Başvurular klasörü Web uygulamanızda gerçek bir klasörü temsil etmediğinden, Visual Studio 2005 de Çözüm Gezgini'nden Başvurular klasörünü kaldırır. Visual Studio 2005'te projenizin referanslarına erişmek için proje için Özellik sayfalarını kullanmanız gerekir.

## <a name="creating-web-projects"></a>Web Projeleri Oluşturma

Web geliştiricileri Visual Studio 2005 proje oluşturma için birçok yeni seçenek var. Web siteleri artık dosya sisteminin herhangi bir yerinde oluşturulabilir ve daha sonra yeni ASP.NET Geliştirme Sunucusu kullanılarak debugged veya göz atılabilir. Geliştiriciler ftp kullanarak yeni Web siteleri de oluşturabilir.

Visual Studio 2005'te Web projeleri oluşturmanın video walkthrough'ünü görüntülemek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Tam Ekran Video Aç](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Dosya Sistemi Projeleri

Video izbinde gördüğünüz gibi, dosya sisteminde yerel makinede veya dosya paylaşımı yoluyla uzak bir konumda Web siteleri oluşturmayı seçebilirsiniz. Dosya sisteminde oluşturulan web sitelerine ASP.NET Geliştirme Sunucusu kullanılarak göz lenir ve debugged.

> [!NOTE]
> ASP.NET Geliştirme Sunucusu müşteriler için bazı karışıklığa neden olabilir. IISs dizin yapısında (c:/inetpub/wwwroot) dosya sisteminde bir Web projesi oluşturulursa, Visual Studio 2005'ten başlatıldığında Web sitesine ASP.NET Geliştirme Sunucusu üzerinden göz atılır. Bu nedenle, herhangi bir IIS yapılandırması (yani kimlik doğrulama yöntemleri) geçerli değildir.

Varsayılan web projesi, yalnızca default.aspx sayfası, default.cs dosyası ve app/_Data klasörü ekleyerek ek yükün çoğunu da kaldırır. Web.config ve özel klasörler (yani app/_code) gerektiğinde eklenir. Web projeniz yalnızca ihtiyacınız olan dosya ve klasörleri içerir.

### <a name="http-projects"></a>HTTP Projeleri

HTTP projeleri, yerel bir IIS Web sitesinde veya uzak bir Web sitesinde oluşturulan projeler olabilir. Varsayılan proje `http://localhost`konumu. Gözat düğmesini tıklattığınızda, iki HTTP seçeneği vardır: Yerel IIS ve Uzak Site. Bu iki seçenekteki temel fark, web sitesi bilgilerinin Konum Seç iletişim kutusunda görüntülenme yöntemi ve dosyaların Web sunucusuna nasıl kopyalandığıdır.

Yerel IIS seçeneği, yerel makinedeki metatabandaki site bilgilerini okur ve dosyalar dosya sistemi kullanılarak kopyalanır. Uzak Site seçeneği FrontPage Server Uzantıları kullanır ve site bilgileri ve dosyaları HTTP ve FrontPage Server Extensions RPC çağrıları kullanılarak kopyalanır.

> [!NOTE]
> vs##//_tmp.htm dosyası ve get/_aspx/_ver.aspx artık sürüm bilgilerini belirlemek için kullanılmaz.

Varsayılan HTTP seçeneği Yerel IIS'dir. Bu seçenek, hangi sitelerin kullanılabilip içerik oluşturulabilmek için hangi konumda olduğunu belirlemek için IIS Metabase'i okur. Ağaç görünümünde seçerek farklı bir klasör veya sanal dizin seçebilirsiniz. Ayrıca yeni bir sanal dizin oluşturabilir, klasörleri uygulama olarak işaretleyebilir ve varolan sanal dizinleri bu iletişim kutusundan silebilirsiniz.

![Konum Seç İletişim Kutusu](improvements-in-visual-studio-2005/_static/image1.gif)

**Şekil 1**: Konum Seç iletişim kutusu

Visual Studio'nun önceki sürümlerinden farklı olarak, **Güvenli Soketler Katmanı Nı Kullan** onay kutusunu kontrol ederseniz ve SSL sertifikası göz attığınız URL ile eşleşmiyorsa, size devam etmek isteyip istemediğiniz konusunda size bir Güvenlik Uyarısı iletişim kutusu sunulur. Visual Studio .NET 2003'ün kullanımı, sertifika eşleşen bir sertifika değilse, proje oluşturma başarısız olur.

![SSL Sertifikası ile ilgili güvenlik uyarısı](improvements-in-visual-studio-2005/_static/image2.gif)

**Şekil 2**: SSL Sertifikasına İlişkin Güvenlik Uyarısı

### <a name="note-on-host-headers"></a>Ev Sahibi Üstenler hakkında not

Belirli bir IP'ye bağlı bir sitede bir Web uygulaması oluşturuyorsanız, ana bilgisayar üstbilginin yapılandırıldığından emin olmanız gerekir. Aksi takdirde, Visual Studio `http://localhost`siteyi ,, ancak sitenin IDE içinden tsıçrıldığında veya debugged olduğunda IP adresi doğru şekilde çözülmez.

Uzak Site seçeneğini belirlerseniz, iletişim kutusu yeni Web sitesinin hedef URL'sini girmenize olanak sağlayacak şekilde değişir. Bu URL, FrontPage Sunucu Uzantıları etkinleştirilmiş bir sunucuda olmalıdır. FrontPage Sunucu Uzantılarını kullanarak yerel Web sunucunuzla çalışmak istiyorsanız, Uzak Site seçeneğini kullanabilir ve yerel bir URL belirtebilirsiniz.

![Uzak Sunucuda Web Sitesi Oluşturma](improvements-in-visual-studio-2005/_static/image1.jpg)

**Şekil 3**: Uzak Sunucuda Web Sitesi Oluşturma

SSL üzerinden uzak bir sitede uygulama oluştururken, SSL sertifikası eşleşmiyorsa, onay iletişim kutusu Yerel IIS seçeneğini kullanırken görüntülenen iletişim kutusundan biraz farklıdır.

![Uzak Site Güvenlik Uyarısı](improvements-in-visual-studio-2005/_static/image3.gif)

**Şekil 4**: Uzak Site Güvenlik Uyarısı

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 FTP üzerinden Web siteleri oluşturma seçeneğini sunar. Bu seçeneği kullandığınızda, IDE dosyaları kullanıcılar geçici klasöründe yerel olarak oluşturur ve dosyaları FTP konumuna taşımak için FTP kullanır.

> [!NOTE]
> Geçici klasör konumu c:/Belgeler ve&lt;&gt;Ayarlar/ Kullanıcı /Yerel Ayarlar/Geçici/VWDWebÖnbellek/&lt;Sunucu&gt;/_&lt;uygulama adıdır&gt;

FTP seçeneğini kullanırken, size konum seç iletişim kutusu sunulur. Bu iletişim kutusuna gerekli FTP bağlantı bilgilerini aşağıda gösterildiği gibi girersiniz.

![FTP için Konum Seç İletişim Kutusu](improvements-in-visual-studio-2005/_static/image2.jpg)

**Şekil 5**: FTP için Konum Seç İletişim Kutusu

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Laboratuvar: FTP sitesini kurulum ve proje oluşturma

Aşağıdaki adımlar, ftp sitesini, kullanıcının yalnızca FTP üzerinden yükleyebileceği bir konuma sahip olması için yapılandırır.

### <a name="install-the-ftp-service"></a>FTP Hizmetini Yükleyin

1. Programları Kaldır'ı Aç, Windows Bileşenleri Ekle/Kaldır'ı seçin
2. Internet Information Services 'i (Windows 2003'te Uygulama Sunucusu) seçin ve **Ayrıntılar'ı**tıklatın.
3. **Dosya Aktarım Protokolü (FTP) Hizmetini** denetleyin ve **Tamam'ı**tıklatın.
4. FTP hizmetini yüklemek için **İleri'yi** tıklatın.

### <a name="create-a-new-folder-for-content"></a>İçerik için Yeni Bir Klasör Oluşturma

1. Windows Gezgini'nde, c:/inetpub/wwwroot içinde **User1** adında yeni bir klasör oluşturun.

#### <a name="configure-folders-and-permissions-on-folders"></a>Klasörleri ve izinleri klasörlerde yapılandırın.

1. İdari Araçlar'dan Internet Bilgi Hizmetleri'ni açın. Artık bilgisayar adı düğümü altında bir FTP Siteleri klasörüne sahip olacak.
2. **FTP Sitelerini**Genişletin.
3. **Varsayılan FTP Sitesini**sağ tıklatın, **Yeni'yi**seçin , sonra **Sanal Dizin**, sonra **İleri'yi**tıklatın.
4. Sanal dizin adı için **User1'i** girin ve **İleri'yi**tıklatın.
5. Yol için **c:/inetpub/wwwroot/User1'i** girin ve **İleri'yi**tıklatın.
6. **Sihirbazı** tamamlamak için İleri ve Sonra **Bitir'i** tıklatın.
7. Varsayılan FTP Sitesi altında **User1** sanal dizinine sağ tıklayın ve **Özellikler'i**seçin.
8. **Yaz** onay kutusunu işaretleyin ve iletişim kutusunu kapatmak için **Tamam'ı** tıklatın.
9. **Varsayılan FTP Sitesini** sağ tıklatın ve **Özellikler'i**seçin.
10. Güvenlik **Hesapları** sekmesinde, **Anonim Bağlantılara İzin Ver'in**işaretlerini kaldırın.
11. Devam etmek isteyip istemediğinisoran iletişim kutusunda **Evet'i** tıklatın.
12. İletişim kutusunu kapatmak için **Tamam'ı** tıklatın.
13. Varsayılan **Web Sitesini** **Web Siteleri** düğümü altında genişletin.
14. **User1** dizinine sağ tıklayın ve **Özellikler'i** seçin
15. Uygulama **Ayarları** bölümünde, klasörü uygulama olarak işaretlemek için **Oluştur'u** tıklatın.
16. İletişim kutusunu kapatmak için **Tamam'ı** tıklatın.
17. Internet Bilgi Hizmetleri'ni kapatın.

### <a name="create-web-project"></a>Web projesi oluşturma

1. Açık Görsel Studio 2005.
2. **Dosya** menüsünden **Yeni Web Sitesi'ni**seçin.
3. **Konum** açılır düşüşünde **FTP'yi**seçin.
4. **Gözat**’a tıklayın.
5. **Sunucu** metin kutusuna **localhost** girin.
6. Dizin metin kutusuna **User1'i** girin.
7. **Aç**'a tıklayın. FTP konumu Yeni Web Sitesi iletişim kutusuna girilir.
8. **Tamam**'a tıklayın.
9. FTP Oturum Açma iletişim kutusunda **Anonim oturum** açma nın işaretlerini kaldırın, kimlik bilgilerinizi girin ve **Tamam'ı**tıklatın.
10. Projenin URL'si nedir? (Projenin URL'si Çözüm Gezgini'nde görüntülenir.)
11. **Yapı** menüsünden Web Sitesi Oluştur veya **Çözüm Oluştur'u**seçin. **Build Web Site**
12. Solution Explorer'da Default.aspx'e sağ tıklayın ve **Tarayıcıda Görüntüle'yi**seçin.
13. Web Sitesi URL Gerekli iletişim `http://localhost/user1` kutusunda, URL için girin ve **Tamam'ı**tıklatın.

> [!NOTE]
> Tür /_Default yüklenemediğini belirten bir hata alırsanız, önceki bir sürüm yerine Web sitenizde 2.0'ASP.NET çalıştırdığınızdan emin olun. Bunu Internet Bilgi Hizmetleri'ndeki ASP.NET sekmesinden yapabilirsiniz.

## <a name="opening-web-projects"></a>Web Projeleri Açma

Web projelerini açmak, proje oluşturmaya benzer. Aşağıdaki bölümlerde IDE içinde çalışırken dikkat edilebis alanlar aforme. Ayrıca HTTP ve FTP kullanarak Web projeleri ile çalışmayı kapsar.

Bir Web projesi açmak için Dosya menüsünden Web Sitesini Aç'ı seçin. Daha önce kapsanan aynı Konum Seç iletişim kutusunda sizden istenir ve kullanabileceğiniz aynı dört seçenek vardır: Dosya Sistemi, Yerel IIS, FTP ve Uzak Site.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Dosya Sistemi

Bu modülde daha önce belirtildiği gibi, Visual Studio artık bir proje dosyası kullanmaz. Bu nedenle, dosya sisteminden bir Web sitesi açmayı seçerseniz, seçtiğiniz klasör başlangıçta Visual Studio'da bir Web projesi olarak oluşturulmasa bile istediğiniz klasörü seçme seçeneğiniz vardır. Örneğin, Belgelerim klasörünü Bir Web sitesi olarak açmayı seçebilirsiniz ve Visual Studio bu klasörü mutlu bir şekilde açar ve dosyalarınızı aşağıda gösterildiği gibi görüntüler.

![Web Sitesi Olarak Açılan Belgelerim](improvements-in-visual-studio-2005/_static/image3.jpg)

**Şekil 6**: Web Sitesi Olarak Açılan *Belgelerim*

Visual Studio yalnızca gerektiğinde ek dosya ve klasörler oluşturduğundan, açtığınız konuma ek dosya veya klasör eklenmez. Bu mimarinin bir yan etkisi, dosya sisteminde Web sitelerini iç içe geçmenizi engellemesidir. Örneğin, aşağıdaki dizin yapısını göz önünde bulundurun.

C:/MyWebSite'de Web projesi

C:/MyWebSite/Nested'de başka bir web projesi

Web sitesini c:/MyWebSite adresinde açtığınızda, İç Içe klasör bu uygulamanın bir alt klasörü olarak görünür.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

WEB sitelerini HTTP üzerinden açarken ayarlar IIS metatabanından (Yerel IIS) veya FrontPage Server Uzantıları (Uzak Site) kullanılarak okunur. İç içe web uygulamaları varsa, bunlar da onları bir uygulama olarak tanımlayan bir simgeyle görüntülenir. FrontPage'deki web uygulamalarıyla çalışmaya aşinaysanız, Visual Studio 2005'teki davranış benzerdir.

Visual Studio, Şu anda IDE içinde açılan uygulamanın altında iç içe olan uygulamalar için bir simge gösterse de, içeriklerini görmek için genişletmenize izin vermez. Ancak, bunları açmak için onlara çift tıklayabilirsiniz. Bunu yaptığınızda, web uygulamasını açmanızı (ve şu anda açık olan çözümü değiştirmenizi) veya Web uygulamasını geçerli çözümünüzün yerine eklemenizi isteyen bir iletişim kutusu sunulur.

![İç içe geçen bir uygulama simgesini çift tıklatma nız size bu iletişim kutusunu sunar](improvements-in-visual-studio-2005/_static/image4.jpg)

**Şekil 7**: İç içe geçen bir uygulama simgesine çift tıklayarak bu iletişim kutusunu sunar

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP Sitesi

FTP ile bir siteyi açtığınızda, dosyaların tümü geçici klasörünüze yerel olarak kopyalanır. Yerel depolama konumu için tam yol proje için Özellikler bölmesinde görüntülenir ve aşağıdaki biçim kullanılarak oluşturulur.

C:/Belgeler ve&lt;Ayarlar/ Kullanıcı&gt;/Yerel Ayarlar/Geçici/VWDWebÖnbellek/&lt;Sunucu&gt;/_&lt;uygulama adı&gt;

FTP kullanırken Visual Studio'nun projenizin temel URL'sini belirterek aşağıda gösterildiği gibi göz atabilmeniz gerekir. Temel URL belirtmezseniz, Visual Studio web sitesindeki bir sayfaya ilk kez göz atmagirişiminde sizden bunu ister.

![FTP Siteleri için Temel URL belirtme](improvements-in-visual-studio-2005/_static/image5.jpg)

**Şekil 8**: FTP Siteleri için Temel URL belirtme

## <a name="improvements-in-compilation"></a>Derlemede Geliştirmeler

Visual Studio 2005'teki Web uygulamalarıyla çalışmak önceki sürümlere göre belirgin derecede daha hızlıdır. Bunun nedeni derleme mimarisindeki değişikliklerdir.

Visual Studio 2002 ve 2003'te, Web uygulamaları /bin klasöründe bulunan tek bir birincil derleme de derlenmiştir. Visual Studio 2005'te bir App/_Code klasörü eklendi. Sınıflar ve Diğer Kullanıcı Arabirimi kodu App/_Code klasörüne eklenir. Visual Studio projeyi oluşturduğunda, App/_Code klasöründeki tüm dosyalar tek bir App/_Code.dll dosyasında derlenir. Bu değişikliğin sonucu, sonraki yapılar önceki sürümlere göre çok daha hızlı olmasıdır.

> [!NOTE]
> MSBuild komut satırı yardımcı programı, web uygulamaları ASP.NET oluşturmak için de kullanılabilir. Bu alet modül 9'da ele alınacaktır.

Başka bir derleme geliştirme, Yapı menüsündeki yeni Yapı Sayfası seçeneğidir. Bu özellik, değişikliklerin daha hızlı derlenebilmeleri için bir geliştiricinin yalnızca geçerli sayfayı (elbette ve bağımlılıklarla birlikte) yeniden oluşturmasına olanak tanır. C# IntelliSense, vb güncelleme amacıyla arka plan derleme sunmuyor çünkü intelliSense sadece tek bir sayfa yı kalarak hızlı bir şekilde güncellenmesine olanak sağlayacak, çünkü bu özellikten son derece yararlanacaktır.

Projenin Yapı özellikleri, başlangıç sayfası yürütülmeden önce oluşan yapı türünü yapılandırmanıza olanak sağlar. Geliştiriciler, Visual Studio'nun kod değişikliklerinden sonra uygulamaları daha hızlı bir şekilde hata ayıklamaya başlayabilmeleri için geçerli sayfayı oluşturmayı seçebilir.

![Yapı Sayfası Başlatma Eylemi](improvements-in-visual-studio-2005/_static/image6.jpg)

**Şekil 9**: Yapı Sayfası Başlatma Eylemi

Visual Studio ve ASP.NET mimarisi için başka büyük geliştirme edit ve devam alanında. Visual Studio 2005'te, geliştiriciler bir projeyi hata ayıklamaya başlayabilir ve hata ayıklayıcıyı ayırmadan projede kod değişiklikleri yapabilir. Aslında, kelimenin tam anlamıyla bir proje hata ayıklama başlayabilir, yeni bir sınıf eklemek, bu sınıfa kod eklemek, bu sınıfın yeni bir örnek oluşturur ve sınıfın bir yöntem yürütmek sayfanıza kod eklemek, tüm hata ayıklayıcı ayırmadan. Yeni kodu yürütmek tarayıcıyı yenilemek kadar kolaydır!

Visual Studio 2005'te yapılan editin video walkthrough'ını görmek ve devam etmek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Tam Ekran Video Aç](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 ve Visual Studio 2005'teki sağlam ve devam işlevselliği, ASP.NET uygulamaları için mimari bir değişiklikten kaynaklanmaktadır. 1.xASP.NET Visual Studio 2002/2003'te oluşturulan uygulamalar /bin klasöründe depolanan bir birincil derleme de derlenmiştir. Uygulama için tüm sınıflar, sayfalar, vb bu bir DLL içine derlenmiştir. Daha sonra çalışma zamanında, ASP.NET tüm denetimleri, işaretlemeyi ve ASP.NET kodu sayfalar içinde derler ve bu DL'leri ASP.NET geçici klasörüne kopyalar.

Visual Studio 2005'te ASP.NET 2.0 kullanılarak, yukarıda ana hatolan iki derleme modeli (biri Visual Studio için, diğeri çalışma zamanında ASP.NET için) ortak bir derleme modelinde birleştirilmiştir. Bu, tüm derleme sorunlarının artık çalışma zamanı yerine geliştirme aşamasında yakalandığı anlamına gelir. Ayrıca, kullanıcı denetimleri ve ana sayfalar gibi özellikler için tasarımcı ve IntelliSense desteğine de olanak tanır.

Kullanıcı denetimleri için tasarımcı desteğinin video walkthrough görmek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Tam Ekran Video Aç](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Bir kullanıcı denetimi bir sayfadan @Register kaldırıldığında, kullanıcı denetimi Web sitesinden silinirse ayrıştırıcı hatalarını önlemek için yönerge biçimlendirmede kalır ve el ile kaldırılmalıdır.

Visual Studio derleme modelindeki bir diğer gelişme de Web Sitesini Yayımla özelliğidir. Yayımlama özelliği Web sitesini önceden derlediği için, geliştiriciler isteğe bağlı olarak hiçbir şey derlemek zorunda kalmamanın ek performansından yararlanabilir. Ayrıca, kaynak kodunun dağıtılması gerekmesin diye App/_Code klasöründeki tüm kaynak kodlarını dll olarak önceden derler.

![Web Sitesi Yayımla İletişim](improvements-in-visual-studio-2005/_static/image7.jpg)

**Şekil 10**: Web Sitesi Yayınla Iletişim Kutusu

> [!NOTE]
> aspnet/_compile.exe yardımcı programı, ASP.NET bir Web uygulamasını önceden derlemek için de kullanılabilir. Bu alet modül 9'da ele alınacaktır.

Bir Web sitesi yayımladığınızda, önceden derlenmiş dosyalar aşağıda gösterildiği gibi Geçici ASP.NET Dosyaları klasöründe depolanır. *.derlenmiş* dosya uzantısı olan dosyalar, belirli DL'ler için bağımlılıkları tanımlayan XML dosyalarıdır. Herhangi bir Webform veya kullanıcı denetimleri App / *_Web/_* ile başlayan rasgele DLs içine derlenir.

*Önceden derlenmiş bu siteyi güncellenebilir* onay kutusu olarak bırakırsanız, Webformlarınızın ve kullanıcı denetimlerinizin içindeki biçimlendirme, dağıtımdan sonra değişiklik yapmanıza olanak tanıyan bir DLL'ye önceden derlenmez. Dağıtılan içeriğe izin verilmemesi için işaretlemeyi kilitlemeyi tercih ederseniz, bu kutunun işaretini kaldırın.

*Sabit adlandırma ve tek sayfa derlemelerini kullan* onay kutusu, her sayfanın sabit adlandırılmış bir derlemede derlenmesine olanak sağlayacak toplu toplu derlemeyi devre dışı bırakmanızı sağlar. Bu kutuyu işaretsiz bırakmak toplu toplu derlemeden yararlanmanızı sağlar.

Önceden derlenmiş derlemeler onay kutusunda *güçlü adlandırmayı etkinleştir,* önceden derlenmiş derlemelerinizi güçlü bir şekilde adlandırmanızı sağlar.

> [!NOTE]
> 1.xASP.NET, güçlü adlandırılmış derlemelerin Küresel Derleme Önbelleğine (GAC) yüklenmesi gerekiyordu. 2.0ASP.NET, GAC'ye güçlü adlandırılmış derlemeler yüklemeniz gerekmez.

![Bir ASP.NET Uygulamaları Önceden Derlenmiş Dosyalar](improvements-in-visual-studio-2005/_static/image8.jpg)

**Şekil 11**: Bir ASP.NET Uygulamaları Önceden Derlenmiş Dosyalar

> [!NOTE]
> Yukarıdaki uygulamada, hiçbir web.config dosyası vardı. Olsaydı, Web sitesi yayınlama işleminden sonra *PrecompiledApp.config* olarak adlandırılacaktı.

## <a name="improvements-in-deployment"></a>Dağıtımdaki Geliştirmeler

Visual Studio 2002 ve 2003'te olduğu gibi Visual Studio 2005, Copy Project özelliği ni sunuyor. Ancak, özellik Visual Studio 2005 yılında güçlendirilmiş ve şimdi Copy Web Sitesi denir.

Web Sitesini Kopyala iletişim kutusu sol çerçeveye ve sağ çerçeveye bölünür. Sol çerçeveye Kaynak Web Sitesi, sağ çerçeveye uzak web sitesi denir. Bazı geliştiricilerin kafasını karıştırabilecek bir şey, doğru çerçevede görüntülenen sitenin mutlaka uzak bir site olmamasıdır. Yerel dosya sisteminde veya IIS'nin yerel örneğinde bir site olabilir. Ayrıca, iletişim kutusu uzak Web *sitesinden* kaynak Web sitesine yayımlamanızı sağladığından, sol çerçevede görüntülenen site mutlaka kaynak Web sitesi değildir.

Bir projeyi uzak bir Web sitesine kopyalıyorsanız, bu sitenin üzerinde FrontPage Server Uzantıları yüklü olmalıdır. Değilse, FTP kullanarak bağlanmanız gerekir. Diğer taraftan, bir projeyi yerel IIS örneğine kopyalıyorsanız, FrontPage Sunucu Uzantıları gerekmez.

> [!NOTE]
> Yerel IIS örneğinde yeni bir Web sitesi oluşturmaya çalışırsanız ve FrontPage 2002 Sunucu Uzantıları yüklenirse, Web sitesi oluşturmanın Bir SharePoint sunucusunda desteklenmediğini belirten bir hata iletisi alırsınız. Bu durumda, FrontPage 2000 Sunucu Uzantılarını yükleme veya FrontPage Sunucu Uzantılarını kaldırma seçeneğiniz vardır.

Web Sitesini Kopyala özelliğinin video bölümü için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Tam Ekran Video Aç](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Hata Ayıklamada Geliştirmeler

Visual Studio 2005'te hata ayıklamada dört önemli gelişme vardır.

- Yönetici olmayan biri olarak yerel olarak hata ayıklama kutudan çıkmak mümkündür.
- Derleme öğesi için Hata Ayıklama özniteliği artık varsayılan olarak yanlıştır.
- Uzaktan hata ayıklama kurulumu ve yapılandırması eskisinden daha kolaydır.
- Artık FTP konumu üzerinden açılan bir Web sitesini hata ayıklayabilirsiniz.

## <a name="debugging-as-a-non-administrator"></a>Yönetici Olmayan Olarak Hata Ayıklama

ASP.NET Geliştirme Sunucusu'nun eklenmesi, yönetici olmayanların ASP.NET uygulamaları kolayca kutudan çıkarmalarına olanak tanır. Yerel dosya sisteminde çalışan bir ASP.NET uygulaması debugged olduğunda, Visual Studio oturum açmış kullanıcı bağlamında ASP.NET Geliştirme Sunucusu başlattı. Bu kullanıcı daha sonra herhangi bir ek yapılandırma olmadan bu uygulamayı hata ayıklama olabilir.

## <a name="debug-is-false-by-default"></a>Hata Ayıklama Varsayılan Olarak False

1.xASP.NETde, web.config dosyasının *derleme* öğesindeki *hata ayıklama* özniteliği varsayılan olarak *doğru* olarak ayarlanmıştır. Geliştiricilerin bir uygulamayı üretime dağıtmadan önce bu özniteliği *yanlış* olarak ayarlamaları her zaman önerilmiştir, ancak çoğu geliştirici hata ayıklama özniteliğini doğru bırakmanın sonuçlarını tam olarak anlamadığından, yalnızca olduğu gibi bıraktılar.

Hata ayıklama özniteliğinin doğru olarak ayarlanmasındaki en ciddi sorun, ASP.NETs toplu derleme modelini devre dışı bırakmasın. Bu nedenle, her sayfa ayrı bir DLL içine derlenir. Bir Web uygulaması binlerce sayfadan oluşuyorsa (hiçbir şekilde duyulmamış değil), bu uygulama tarafından birkaç bin küçük LL'nin oluşturulacağı anlamına gelir. Bu DL'ler boyutu küçük olsa da, bellekte belirli bir konuma yüklenmez. Bu nedenle, sistem belleğinde parçalanmaya neden olur lar ve OutOfMemoryException oluşumlarına katkıda bulunabilirler.

2.0ASP.NET hata ayıklama özniteliği varsayılan olarak false olarak ayarlanır. Daha önce de gördüğünüz gibi, bir geliştirici Visual Studio 2005'te bir ASP.NET uygulamasını bozduğunda, hata ayıklama etkin leştirilmiş bir web.config dosyası eklemeleri istenir. Bunu yapmak, ASP.NET 1.x'te bulunan aynı sakıncalara neden olur, ancak şimdi geliştirici, uygulamayı üretime taşımadan önce özniteliğin yanlışa sıfırlandığı konusunda açıkça uyarılır.

## <a name="remote-debugging-setup-and-configuration"></a>Uzaktan Hata Ayıklama Kurulumu ve Yapılandırması

Visual Studio 2002/2003'te uzaktan hata ayıklama Makine Hata Ayıklama Yöneticisi (mdm.exe) ve vs7jit.exe sürecine dayanıyordu. Bu nedenle, uzaktan hata ayıklama sorunları sorun giderme genellikle müşteriler için bir kara kutu oldu ve genellikle PSS için çok daha iyi değildi.

Visual Studio 2005 mdm.exe ve vs7jit.exe süreçlerine olan güveni ortadan kaldırır. Bunun yerine, şimdi Uzaktan Hata Ayıklama Monitörü hizmetini kullanır (msvsmon.exe.)

Visual Studio 2005'te hata ayıklama gereksinimi oldukça basittir. Hata ayıklama dan önce uzak sunucuda msvsmon.exe çalıştırmak gerekir. Uzaktan Hata Ayıklama Monitörünü Visual Studio CD'sinden yükleyebilir veya Web sunucusuna hiçbir şey yüklemeden msvsmon.exe'yi bir paylaşımdan çalıştırabilirsiniz.

msvsmon.exe çalıştırdığınızda, uzak hata ayıklama için bloke olan bağlantı noktaları hakkında şikayet olasıdır. Neyse ki, aşağıda gösterildiği gibi uyarı iletişim kutusundaki bağlantı noktalarını kolayca kaldırabilirsiniz.

![Windows Güvenlik Duvarı'nın Uzaktan Hata Ayıklama'yı Engellediğini Bildiren Bildirim](improvements-in-visual-studio-2005/_static/image9.jpg)

**Şekil 12**: Windows Güvenlik Duvarı'nın Uzaktan Hata Ayıklama'yı EngellediğiniN Bildirilmesi

Hata ayıklama için gerekli bağlantı noktalarını kaldırdıktan sonra, aşağıda gösterildiği gibi Uzaktan Hata Ayıklama Monitörü'nün de liğini görürsünüz. Bu arabirimden bağlantıları izleyebilir ve hata ayıklama izinlerini kolayca değiştirebilirsiniz.

![Uzaktan Hata Ayıklama Monitörü](improvements-in-visual-studio-2005/_static/image10.jpg)

**Şekil 13**: Uzaktan Hata Ayıklama Monitörü

FTP üzerinden açılan bir Web uygulamasını uzaktan hata ayıklamak da mümkündür. Adımlar, daha önce kapsananlarla aynıdır. Ancak, ftp projesinde daha önce belirtildiği gibi göz atmak için bir temel URL belirtmeniz gerekir.

## <a name="lab-2"></a>Laboratuvar 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Visual Studio 2005 ile Uzaktan Hata Ayıklama

Bu laboratuvar Visual Studio 2005 ile uzaktan hata ayıklama size yol verecektir.

Bu laboratuvarın video bölümü için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Tam Ekran Video Aç](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

Bu laboratuvar, biri Visual Studio 2005'i, diğeri de IIS 5 veya daha büyük çalışan iki makineye sahip olmayı gerektirir.

1. Visual Studio 2005'i açın ve uzak sunucuda yeni bir Web sitesi oluşturun.

> [!NOTE]
> Web sitesini uzak bir IIS örneğinde veya FTP aracılığıyla oluşturabilirsiniz.

1. Uzak Web sunucusundan, bir UNC yolunu kullanarak geliştirme makinesinde msvsmon.exe'yi bulun ve çalıştırın.  
 msvsmon.exe için varsayılan konum //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86'dır.
2. Uzaktan hata ayıklama için bağlantı noktalarının engelini kaldırması istenirse, bunu yapın.
3. Geliştirme makinesinden Default.aspx için kodu niçin açın ve Sayfa/_Load yönteminde bir kesme noktası ayarlayın.
4. Geliştirme makinesinden hata ayıklamaya başlayın.

Beklendiği gibi kırılma noktasına ulaşmalısın.

## <a name="aspnet-development-server"></a>ASP.NET Geliştirme Sunucusu

Daha önce de tartıştığımız gibi, Visual Studio 2005 ASP.NET Development Server adlı bir Web sunucusu ile gemi. (ASP.NET Geliştirme Sunucusu bazen Cassini olarak adlandırılır.) Bu Web sunucusu, dosya sisteminde çalışan Web uygulamalarına göz atmak ve hata ayıklamak için kullanışlı bir araçtır.

ASP.NET Geliştirme Sunucusu kısıtlı bir Web sunucusudur. Uzaktan bağlantılara izin vermez, Web sunucusunu başlatan kullanıcı dışında herhangi bir kullanıcıdan gelen isteklere izin vermez. Ayrıca ASP sayfaları sunma özelliğine de sahip değildir. Yalnızca ASP.NET kaynakları ve HTML kaynakları (resimler, CSS dosyaları, vb. dahil) sunulmaktadır.

ASP.NET Geliştirme Sunucusu komut satırı üzerinden c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/*adresinde bulunan WebDev.WebServer.exe dosyasını çalıştırarak başlatılabilir. Aşağıdaki iletişim kutusu, kullanılabilir parametreleri görüntüler.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Şekil 14**

> [!NOTE]
> ASP.NET Geliştirme Sunucusu komut satırı üzerinden açıkça başlatıldığında desteklenmez.
