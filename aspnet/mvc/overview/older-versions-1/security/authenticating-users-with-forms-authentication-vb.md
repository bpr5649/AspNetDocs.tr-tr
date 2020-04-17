---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: Form Kimlik Doğrulaması (VB) ile Kullanıcıların Kimlik Doğrulaması | Microsoft Dokümanlar
author: rick-anderson
description: MVC uygulamanızdaki belirli sayfaları parola koruma özelliğine [Yetkilendirme] özniteliğini nasıl kullanacağınızı öğrenin. Web Sitesi Yönetimini Nasıl Kullanacağınızı Da Öğreniyorsunuz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540824"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a>Forms Kimlik Doğrulaması ile Kullanıcıların Kimliğini Doğrulama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> MVC uygulamanızdaki belirli sayfaları parola koruma özelliğine [Yetkilendirme] özniteliğini nasıl kullanacağınızı öğrenin. Kullanıcıları ve rolleri oluşturmak ve yönetmek için Web Sitesi Yönetim Aracı'nı nasıl kullanacağınızı öğrenirsiniz. Ayrıca, kullanıcı hesabının ve rol bilgilerinin depolandığı yeri nasıl yapılandıracağınızı da öğrenirsiniz.

Bu öğreticinin amacı, ASP.NET MVC uygulamalarınızdaki görünümleri korumak için Form kimlik doğrulamasını nasıl kullanabileceğinizi açıklamaktır. Kullanıcıları ve rolleri oluşturmak için Web Sitesi Yönetim Aracı'nı nasıl kullanacağınızı öğrenirsiniz. Ayrıca, yetkisiz kullanıcıların denetleyici eylemlerini çalmasını nasıl önleyeceğinizi de öğrenirsiniz. Son olarak, kullanıcı adlarının ve parolaların nerede depolandığını nasıl yapılandıracağınızı öğrenirsiniz.

#### <a name="using-the-web-site-administration-tool"></a>Web Sitesi Yönetim Aracını Kullanma

Başka bir şey yapmadan önce, bazı kullanıcılar ve roller oluşturarak başlamalıdır. Yeni kullanıcılar ve roller oluşturmanın en kolay yolu Visual Studio 2008 Web Sitesi Yönetim Aracı'ndan yararlanmaktır. Bu aracı **Proje, ASP.NET Yapılandırma**menü seçeneğini seçerek başlatabilirsiniz. Alternatif olarak, Çözüm Gezgini penceresinin üst kısmında görünen dünyaya vuran çekicin (biraz korkutucu) simgesine tıklayarak Web Sitesi Yönetim Aracı'nı başlatabilirsiniz (Bkz. Şekil 1).

**Şekil 1 – Web Sitesi Yönetim Aracının Başlatılması**

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

Web Sitesi Yönetimi Aracı içinde, Güvenlik sekmesini seçerek yeni kullanıcılar ve roller oluşturursunuz. Stephen adında yeni bir kullanıcı oluşturmak için **kullanıcı oluştur** bağlantısını tıklatın (Şekil 2'ye bakın). Stephen kullanıcısına istediğiniz parolayı sağlayın (örneğin, *gizli).*

**Şekil 2 – Yeni bir kullanıcı oluşturma**

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

Önce rolleri etkinleştirerek ve bir veya daha fazla rolü tanımlayarak yeni roller oluşturursunuz. **Rolleri Etkinleştir** bağlantısını tıklatarak rolleri etkinleştirin. Ardından, **rol Oluştur veya Yönet** bağlantısını tıklatarak *Yöneticiler* adlı bir rol oluşturun (Bkz. Şekil 3).

**Şekil 3 – Yeni bir rol oluşturma**

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

Son olarak, Sally adında yeni bir kullanıcı oluşturun ve Sally'yi Oluştur Kullanıcı bağlantısını tıklayarak ve Sally oluştururken Yöneticiler'i seçerek Yöneticiler rolüyle ilişkilendirin (Bkz. Şekil 4).

**Şekil 4 – Bir role kullanıcı ekleme**

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

Ne zaman tüm söylenir ve yapılır, Stephen ve Sally adlı iki yeni kullanıcılar olmalıdır. Ayrıca Yöneticiler adlı yeni bir rol olmalıdır. Sally Yöneticiler rolü bir üyesi ve Stephen değildir.

#### <a name="requiring-authorization"></a>Yetkilendirme Gerektiren

Kullanıcı eyleme [Authorize] özniteliği ekleyerek bir denetleyici eylemi çağırmadan önce bir kullanıcının kimliğinin doğrulamasını gerektirebilirsiniz. [Authorize] özniteliğini tek bir denetleyici eylemine uygulayabilir veya bu özniteliği tüm denetleyici sınıfına uygulayabilirsiniz.

Örneğin, Listeleme 1'deki denetleyici, CompanySecrets() adlı bir eylemi ortaya çıkarır. Bu eylem [Authorize] özniteliği ile dekore edilmiş olduğundan, kullanıcı kimliği doğrulanmıyorsa bu eylem çağrılamaz.

**Listeleme 1 – Denetleyiciler\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

Tarayıcınızın adres çubuğuna URL /Home/CompanySecrets'ı girerek CompanySecrets() eylemini çağırırsanız ve kimliği doğrulanmış bir kullanıcı değilseniz, otomatik olarak Giriş görünümüne yönlendirilirsiniz (Bkz. Şekil 5).

**Şekil 5 – Giriş görünümü**

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

Kullanıcı adınızı ve şifrenizi girmek için Giriş görünümünü kullanabilirsiniz. Kayıtlı bir kullanıcı değilseniz, Kayıt görünümüne gitmek için **kayıt** bağlantısını tıklatabilirsiniz (Bkz. Şekil 6). Yeni bir kullanıcı hesabı oluşturmak için Kayıt görünümü'ni kullanabilirsiniz.

**Şekil 6 – Kayıt görünümü**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

Başarılı bir şekilde giriş yaptıktan sonra CompanySecrets görünümünü görebilirsiniz (Bkz. Şekil 7). Varsayılan olarak, tarayıcı pencerenizi kapatana kadar oturum açmaya devam eceksiniz.

**Şekil 7 – CompanySecrets görünümü**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Kullanıcı Adı veya Kullanıcı Rolüne Göre Yetkilendirme

Denetleyici eylemine erişimi belirli bir kullanıcı kümesiyle veya belirli bir kullanıcı rolü kümesiyle kısıtlamak için [Yetkilendirme] özniteliğini kullanabilirsiniz. Örneğin, Listeleme 2'deki değiştirilmiş Ev denetleyicisi StephenSecrets() ve AdministratorSecrets() adlı iki yeni eylem içerir.

**Listeleme 2 – Denetleyiciler\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

Yalnızca Stephen kullanıcı adına sahip bir kullanıcı StephenSecrets() eylemini çağırabilir. Diğer tüm kullanıcılar Giriş görünümüne yönlendirilir. Kullanıcılar özelliği, kullanıcı hesabı adlarının virgülle ayrılmış listesini kabul eder.

Yalnızca Yöneticiler rolündeki kullanıcılar AdministratorSecrets() eylemini çağırabilir. Örneğin, Sally Yöneticiler grubunun bir üyesi olduğundan, AdministratorSecrets() eylemini çağırabilir. Diğer tüm kullanıcılar Giriş görünümüne yönlendirilir. Roller özelliği, rol adlarının virgülle ayrılmış listesini kabul eder.

#### <a name="configuring-authentication"></a>Kimlik Doğrulamayı Yapılandırma

Bu noktada, kullanıcı hesabının ve rol bilgilerinin nerede depolandığını merak ediyor olabilirsiniz. Varsayılan olarak, bilgiler MVC uygulamanızın Uygulama\_Verileri klasöründe bulunan ASPNETDB.mdf adlı (RANU) SQL Express veritabanında depolanır. Bu veritabanı, üyeliği kullanmaya başladığınızda otomatik olarak ASP.NET çerçevesi tarafından oluşturulur.

Çözüm Gezgini penceresinde ASPNETDB.mdf veritabanını görmek için öncelikle Tüm Dosyaları Göster menüsü seçeneğini seçmeniz gerekir.

Varsayılan SQL Express veritabanını kullanmak, bir uygulama geliştirirken iyidir. Ancak büyük olasılıkla, bir üretim uygulaması için varsayılan ASPNETDB.mdf veritabanını kullanmak istemeyebilirsiniz. Bu durumda, aşağıdaki iki adımı tamamlayarak kullanıcı hesabı bilgilerinin depolandığı yeri değiştirebilirsiniz:

1. Uygulama Hizmetleri veritabanı nesnelerini üretim veritabanınıza ekleyin - Uygulama bağlantı dizenizi üretim veritabanınızı işaret etmek üzere değiştirin

İlk adım, üretim veritabanınıza gerekli tüm veritabanı nesnelerini (tablolar ve depolanan yordamlar) eklemektir. Bu nesneleri yeni bir veritabanına eklemenin en kolay yolu ASP.NET SQL Server Kurulum Sihirbazı'ndan yararlanmaktır (Bkz. Şekil 8). Bu aracı Microsoft Visual Studio 2008 program grubundan Visual Studio 2008 Komut Komut Istemi'ni açarak ve komut isteminden aşağıdaki komutu çalıştırarak başlatabilirsiniz:

aspnet\_regsql

**Şekil 8 – sql server kurulum sihirbazı ASP.NET**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL Server Kurulum Sihirbazı, ağınızda bir SQL Server veritabanı seçmenize ve ASP.NET uygulama hizmetlerinin gerektirdiği tüm veritabanı nesnelerini yüklemenize olanak tanır. Veritabanı sunucusunun yerel makinenizde bulunması gerekmez.

> [!NOTE]
> SQL Server Setup Sihirbazı'ASP.NET kullanmak istemiyorsanız, uygulama hizmetleri veritabanı nesnelerini aşağıdaki klasöre eklemek için SQL komut dosyalarını bulabilirsiniz:
> 
> 
> C:\Windows\Microsoft.NET\Framework\v2.0.50727

Gerekli veritabanı nesnelerini oluşturduktan sonra, MVC uygulamanız tarafından kullanılan veritabanı bağlantısını değiştirmeniz gerekir. Web yapılandırma (web.config) dosyanızdaki ApplicationServices bağlantı dizesini üretim veritabanını işaret edecek şekilde değiştirin. Örneğin, Listeleme'deki değiştirilmiş bağlantı MyProductionDB adlı bir veritabanına 3 nokta (özgün ApplicationServices bağlantı dizesi yorumlandı).

**Listeleme 3 – Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Veritabanı İzinlerini Yapılandırma

Veritabanınıza bağlanmak için Tümleşik Güvenlik'i kullanıyorsanız, veritabanınıza giriş olarak doğru Windows kullanıcı hesabını eklemeniz gerekir. Doğru hesap, ASP.NET Geliştirme Sunucusu'nu veya Internet Bilgi Hizmetlerini web sunucunuz olarak kullanıp kullanmadığınıza bağlıdır. Doğru kullanıcı hesabı da işletim sisteminize bağlıdır.

ASP.NET Geliştirme Sunucusu'nu (Visual Studio tarafından kullanılan varsayılan web sunucusu) kullanıyorsanız, uygulamanız Windows kullanıcı hesabınızın bağlamında yürütülür. Bu durumda, Windows kullanıcı hesabınızı veritabanı sunucusu girişi olarak eklemeniz gerekir.

Alternatif olarak, Internet Bilgi Hizmetleri kullanıyorsanız, veritabanı sunucusu girişi olarak ASPNET hesabını veya NT AUTHORITY/NETWORK SERVICE hesabını eklemeniz gerekir. Windows XP kullanıyorsanız, ASPNET hesabını veritabanınıza giriş olarak ekleyin. Windows Vista veya Windows Server 2008 gibi daha yeni bir işletim sistemi kullanıyorsanız, veritabanı girişi olarak NT AUTHORITY/NETWORK SERVICE hesabını ekleyin.

Microsoft SQL Server Management Studio'u kullanarak veritabanınıza yeni bir kullanıcı hesabı ekleyebilirsiniz (Bkz. Şekil 9).

**Şekil 9 - Yeni bir Microsoft SQL Server girişi oluşturma**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

Gerekli girişi oluşturduktan sonra, oturum açmanın doğru veritabanı rolleriyle bir veritabanı kullanıcısıyla eşlemesi gerekir. Girişe çift tıklayın ve Kullanıcı Eşleme sekmesini seçin. Bir veya daha fazla uygulama hizmetleri veritabanı rolü seçin. Örneğin, kullanıcıların kimliğini doğrulamak için aspnet\_Membership\_BasicAccess veritabanı rolünü etkinleştirmeniz gerekir. Yeni kullanıcılar oluşturmak için aspnet\_Membership\_FullAccess veritabanı rolünü etkinleştirmeniz gerekir (Bkz. Şekil 10).

**Şekil 10 - Uygulama Hizmetleri veritabanı rollerinin eklenmesi**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>Özet

Bu eğitimde, bir ASP.NET MVC uygulaması oluştururken Formkimlik doğrulamasını nasıl kullanacağınızı öğrendiniz. İlk olarak, Web Sitesi Yönetim Aracı'ndan yararlanarak yeni kullanıcılar ve roller oluşturmayı öğrendiniz. Ardından, yetkisiz kullanıcıların denetleyici eylemlerini çalmasını önlemek için [Authorize] özniteliğini nasıl kullanacağınızı öğrendiniz. Son olarak, MVC uygulamanızı kullanıcı ve rol bilgilerini bir üretim veritabanında depolamak için nasıl yapılandırabileceğinizi öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](preventing-javascript-injection-attacks-cs.md)
> [Sonraki](authenticating-users-with-windows-authentication-vb.md)
