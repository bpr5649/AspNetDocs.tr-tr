---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Üyelik | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Üyelik, Formkimlik doğrulama modelinin ASP.NET 1.x'ten elde edilen başarısını oluşturur. ASP.NET Formlar kimlik doğrulaması incorp için uygun bir yol sağlar ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543775"
---
# <a name="membership"></a>Üyelik

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET Üyelik, Formkimlik doğrulama modelinin ASP.NET 1.x'ten elde edilen başarısını oluşturur. ASP.NET Formlar kimlik doğrulaması, ASP.NET uygulamanıza bir giriş formu dahil etmek ve kullanıcıları bir veritabanı veya başka bir veri deposuna karşı doğrulamak için kullanışlı bir yol sağlar.

ASP.NET Üyelik, Formkimlik doğrulama modelinin ASP.NET 1.x'ten elde edilen başarısını oluşturur. ASP.NET Formlar kimlik doğrulaması, ASP.NET uygulamanıza bir giriş formu dahil etmek ve kullanıcıları bir veritabanı veya başka bir veri deposuna karşı doğrulamak için kullanışlı bir yol sağlar. FormsAuthentication sınıfının üyeleri kimlik doğrulama için tanımlama bilgilerini işlemeyi, geçerli bir girişi kontrol etmeyi, kullanıcıyı oturumu oturum alamasını vb. mümkün kılar. Ancak, ASP.NET 1.x uygulamasında Form kimlik doğrulaması uygulanması adil bir kod miktarı gerektirebilir.

ASP.NET 2.0 üyeliği, formların kimlik doğrulamasını tek başına kullanma konusunda büyük bir ilerlemedir. (Formlar kimlik doğrulaması ile birleştiğinde üyelik en sağlamdır, ancak Formkimlik doğrulaması kullanmak bir gereklilik değildir.) Yakında göreceğiniz gibi, hiç çok kod yazmadan güçlü bir üyelik sistemi uygulamak için ASP.NET 2.0 ASP.NET Üyelik ve giriş kontrolleri kullanabilirsiniz.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2.0'da Üyeliğin Uygulanması

Üyelik dört adım izleyerek uygulanır. Dahil olan birçok alt adımın yanı sıra isteğe bağlı yapılandırmada da uygulanabileceğini unutmayın. Bu adımlar, üyeliği yapılandırmanın büyük resmini göstermek içindir.

1. Üyelik veritabanınızı oluşturun (SQL Server üyelik deposu olarak kullanılıyorsa.)
2. Uygulama yapılandırma dosyalarınızdaki üyelik seçeneklerini belirtin. (Üyelik varsayılan olarak etkinleştirilir.)
3. Kullanmak istediğiniz üyelik deposunun türünü belirleyin. Seçenekler şunlardır: 

    - Microsoft SQL Server (sürüm 7.0 veya sonraki sürüm)
    - Aktif Dizin Mağazası
    - Özel üyelik sağlayıcısı
4. ASP.NET Formlar kimlik doğrulaması için uygulamayı yapılandırın. Üyelik bir kez daha Formkimlik doğrulamadan yararlanmak üzere tasarlanmıştır, ancak Form kimlik doğrulaması kullanmak bir gereklilik değildir.
5. Üyelik için kullanıcı hesaplarını tanımlayın ve istenirse rolleri yapılandırın.

## <a name="creating-the-membership-database"></a>Üyelik Veritabanı oluşturma

SQL Server 7.0 veya daha sonra üyelik mağazanız olarak kullanıyorsanız,\_veritabanınızı yapılandırmak için aspnet regsql yardımcı programını (Visual Studio .NET 2005 Command Prompt'dan en kolay olarak temin edilebilir) kullanabilirsiniz. Aspnet\_regsql yardımcı programı komut istemi aracı olarak veya gui sihirbazı aracılığıyla kullanılabilir. Sihirbaz yöntemi veritabanınızı yapılandırmanın en kolay yoludur. Sihirbaza erişmek için aşağıdaki komutu çalıştırmanız yeterlidir:

`aspnet_regsql W`

Bu komutu çalıştırdıktan sonra, aşağıda gösterildiği gibi ASP.NET SQL Server Kurulum Sihirbazı ile sunulacaktır.

![](membership/_static/image1.jpg)

**Şekil 1**

ASP.NET SQL Server Kurulum Sihirbazı, sihirbazda belirttiğiniz durumda Web sitesini oluşturur. Ancak, ASP.NET veritabanınıza bağlanmak için machine.config dosyasındaki bağlantı dizesini kullanır. Varsayılan olarak, bu bağlantı dizesi bir SQL Server 2005 örneğini işaret eder, bu nedenle bir SQL Server 2000 veya SQL Server 7.0 örneği kullanıyorsanız, machine.config dosyasındaki bağlantı dizesini değiştirmeniz gerekir. Bu bağlantı dizesi burada bulunabilir:

[!code-xml[Main](membership/samples/sample1.xml)]

Ne yazık ki, bağlantı dizesini değiştirmezseniz, ASP.NET açıklayıcı bir hata vermez. Veritabanını oluşturmadığınızı söyleyerek şikayet etmeye devam edecektir. Yukarıdaki durumda, benim yerel SQL Server 2000 örnek işaret etmek için bağlantı dizesini değiştirdim.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Yapılandırmanın Belirtilmesi ve Kullanıcı ve Roller Inanın

Üyelik yapılandırmada bir sonraki adım, uygulamanın web.config dosyasına gerekli bilgileri eklemektir. 1.x ASP.NET, web.config dosyasını değiştirmek bazen alt CamelCase kullanımı ve Intellisense eksikliği nedeniyle zordu. Visual Studio .NET 2005 yapılandırma dosyaları için Intellisense ile görevi çok daha kolay hale getirir, ancak ASP.NET 2.0 yapılandırma dosyalarını düzenlemek için bir Web arabirimi sağlayarak bir adım daha ileri gider.

Aşağıda gösterildiği gibi Çözüm Gezgini araç çubuğundaki ASP.NET Yapılandırma düğmesini tıklatarak Web arabirimini başlatabilirsiniz. Giriş denetimleri eklendiğinde görüntülenen açılır pencereler aracılığıyla Web arabirimini de başlatabilirsiniz.

![](membership/_static/image2.jpg)

**Şekil 2**

Bu, aşağıda gösterilen ASP.NET Web Sitesi Yönetim Aracı'nı başlatıyor. ASP.NET Web Sitesi Yönetimi, uygulama ayarlarını yönetmeyi kolaylaştıran dört sekmeli bir arabirimdir. Aşağıdaki sekmeler kullanılabilir:

- **Giriş**
- **Güvenlik** Kullanıcıları, rolleri ve erişimi yapılandırın.
- **Başvuru** Uygulama ayarlarını yapılandırın.
- **Sağlayıcı** Uygulama üyelik sağlayıcınızı yapılandırın ve test edin.

Web Sitesi Yönetim Aracı, kolayca yeni kullanıcılar oluşturmanıza, yeni roller oluşturmanıza ve kullanıcıları ve rolleri yönetmenize olanak tanır. Bu yetenek Windows arabiriminde kullanılamaz. Windows arabirimi, yetkilendirme ayarlarını kolayca tanımlamanızı ve Web Sitesi Yönetim Aracı'nda olmayan sağlayıcıları, yetenekleri eklemenize, silmenize ve yönetmenize olanak tanır.

Windows arabirimini başlatmak için Internet Information Services snap-in'i açın, uygulamanıza sağ tıklayın ve Özellikler'i seçin. ASP.NET sekmesini tıklatın ve ardından Yapılandırmayı Edit düğmesini tıklatın. (Yapılandırmayı Edit düğmesinin etkinolabilmesi için uygulamanın ASP.NET 2.0 altında çalışıyor olması gerekir. ASP.NET iletişim kutusunda da ASP.NET sürümünü yapılandırabilirsiniz.) ASP.NET Yapılandırma Ayarları iletişim kutusu aşağıda gösterildiği gibi görüntülenir.

![](membership/_static/image3.jpg)

**Şekil 3**

Genel sekmesinde bağlantı dizeleri ve uygulama ayarları listelenir. Italik ayarlarbir üst yapılandırma dosyasında tanımlanır (machine.config veya daha yüksek bir düzeyde web.config) ve italik olmayan ayarlar uygulamalar yapılandırma dosyasındandır. Uygulama düzeyinde bir ayar eklenirse, kaldırılırsa veya düzenlenirse, ASP.NET, ayarı devralındığı yapılandırma dosyasından kaldırmak yerine uygulama düzeyleri web.config'deki ayarı ekler, kaldırır veya değiştirir.

Kimlik Doğrulama sekmesi aşağıda gösterilmiştir. Burası üyelik ayarlarınızı yapılandıracağınız yerdir. Formkimlik doğrulama ayarları, üyelik sağlayıcıları ve rol sağlayıcıları burada yapılandırılabilir.

![](membership/_static/image4.jpg)

**Şekil 4**

## <a name="implementing-membership-in-your-application"></a>Başvurunuza Üyelik Uygulama

Uygulamanızda 2,0 ASP.NET üyeliği uygulamanın en kolay yolu sağlanan Logon denetimlerini kullanmaktır. Bu yöntem, herhangi bir kod yazmadan ASP.NET 2.0 üyeliğinin temellerini uygulamanızı sağlar.

Aşağıdaki Logon denetimleri ASP.NET 2.0'da mevcuttur:

## <a name="login-control"></a>Giriş Kontrolü

Giriş denetimi, birinin üyelik sisteminize giriş yapabı için bir arayüz sağlar. Size bir kullanıcı adı ve şifre textbox ve bir giriş düğmesi sağlar. Henüz yapmamış kişiler için kayıt olmak için bir bağlantı, kullanıcının sonraki ziyaretlerde otomatik olarak oturum açmasına izin veren bir onay kutusu, parola hatırlatıcısı için bir bağlantı, vb. gibi diğer birçok yaygın özellik. Giriş denetiminin tüm özellikleri, denetimin özellikleri yle özelleştirilebilir.

1.x ASP.NET, geliştiriciler Formkimlik doğrulaması kullanırken bir arama yapmak için kod adil bir miktar yazmak zorunda kaldı. ASP.NET 2.0 üyeliği ile, hiç kod yazmadan kullanıcıları doğrulayabilirsiniz. ASP.NET otomatik olarak sizin için kullanıcının arama yapacaktır. (Giriş denetimini ASP.NET üyelik kullanmadan kullanıyorsanız, kullanıcıyı doğrulamak için **OnAuthenticate** yöntemini kullanabilirsiniz.)

## <a name="loginview-control"></a>GirişGörünümü Kontrolü

LoginView denetimi varsayılan olarak iki şablon sağlayan şablonlanmış bir denetimdir; AnonymousTemplate ve LoggedInTemplate. Görüntülenen şablon, kullanıcının üyelik sisteminize giriş yapıp yapmamaya göre belirlenir. Bu denetim genellikle, kullanıcı henüz oturum açmamışken bir Giriş denetimi ve kullanıcı oturum açtığında bir Giriş Durumu denetimi ve/veya diğer giriş denetimleri görüntülemek için kullanılır. ASP.NET uygulamanızda rol yönetimi kullanıyorsanız, LoginView denetimi kullanıcıların rolüne bağlı olarak belirli bir şablon görüntüleyebilir. (daha fazla ASP.NET rol yönetimi daha sonra ele alınacaktır.)

## <a name="passwordrecovery-control"></a>PasswordRecovery Denetimi

PasswordRecovery denetimi, kullanıcıların geçerli parolasını içeren bir e-posta almasını veya parolasını sıfırlamasını sağlar. Açık metin ve şifrelenmiş parolalar kurtarılabilir ve kullanıcılara e-posta yla gönderilebilir. Parola işlenebilirse kurtarılamaz. Bunun yerine kullanıcının parola sıfırlama gerçekleştirmesi gerekir.

## <a name="loginstatus-control"></a>Giriş Durum Kontrolü

Giriş Durumu denetimi, oturum açmamış kullanıcılara bir giriş göstergesi ve şu anda oturum açmış olan kullanıcılara bir giriş göstergesi görüntülemek için kullanılır. Request.IsAuthenticated özelliği, hangi göstergenin görüntülenilen belirlenecek lerini belirlemek için kullanılır. Giriş Durumu denetimi tarafından görüntülenen gösterge metin **(LoginText** ve **LogoutText** özellikleri üzerinden uygulanabilir) veya görüntüler **(LoginImageUrl** ve **LogoutImageUrl** özellikleri üzerinden uygulanır.)

Bir kullanıcı Giriş Durumu denetimi üzerinden oturum açtığında, **LogoutPageUrl** özelliği tarafından belirtilen URL'ye yönlendirilir. Bu özellik ayarlanmazsa, geçerli sayfa yenilenir. Site büyük olasılıkla Formlar kimlik doğrulaması tarafından korunduğundan, geçerli sayfanın yenilenmesi kullanıcıyı sitenin giriş sayfasına yönlendirir.

## <a name="loginname-control"></a>Giriş Adı Kontrolü

LoginName denetimi, siteye giriş yapmakta olan kullanıcının kullanıcı adını görüntüler.

## <a name="createuserwizard-control"></a>CreateUserWizard Denetimi

CreateUserWizard denetimi, kullanıcılara üyelik sisteminize kaydolmak için uygun bir yol sağlar. Aşağıda gösterilen arabirim aracılığıyla adımlar (WizardSteps koleksiyonu olarak uygulanır) ekleyebilirsiniz.

![](membership/_static/image5.jpg)

**Şekil 5**

CreateUserWizard, Sihirbaz sınıfından türetilen ve aşağıdaki şablonları sağlayan şablonlu bir denetimdir:

- **ÜstbilgiŞablon** Bu şablon, sihirbazın üstbilgigörünümünü denetler.
- **Kenar Çubuğu Şablonu** Bu şablon, sihirbazın kenar çubuğunun görünümünü denetler.
- **Başlangıç Navigasyon Şablonu** Bu şablon, gezintinin görünümünü denetler başlangıç adımında sihirbazVardır.
- **StepNavigationTemplate** Bu şablon, başlangıç veya bitiş adımında olmadığında gezinti alanının görünümünü denetler.
- **FinishNavigationTemplate** Bu şablon, bitiş adımında gezinti alanının görünümünü denetler.

Ayrıca, Sihirbaza eklediğiniz her adım için ASP.NET, bu adım için hem ContentTemplate hem de CustomNavigationTemplate içeren özel bir şablon oluşturur. CreateUserWizard'ı özelleştirme yle ilgili tüm ayrıntılar için 2005 VS.NET belgelerine bakın:

## <a name="changepassword-control"></a>Parola Denetimini Değiştir

ChangePassword denetimi, kullanıcıların parolasını değiştirmesine olanak tanır. DisplayUserName özelliği doğruysa (varsayılan olarak yanlıştır), kullanıcı oturum açmadığında parolasını değiştirebilir. Kullanıcı zaten oturum *açmışsa* ve DisplayUserName özelliği doğruysa, kullanıcı kullanıcının kullanıcı kimliğini bilmesi koşuluyla oturum açmamış başka bir kullanıcının parolasını değiştirebilir.

Kullanıcıların oturum açmalarına gerek kalmadan parolaları değiştirebilmelerini istiyorsanız, ChangePassword denetiminin görüntülendiği sayfanın anonim erişime izin verdiğinden emin olmanız gerektiğini unutmayın. Açıkçası, kullanıcıların şifrelerini değiştirmek için eski şifrelerini sağlamak zorunda kalacak.

## <a name="role-management"></a>Rol Yönetimi

Rol yönetimi, kullanıcıları belirli bir role atamanıza ve ardından bu role bağlı olarak belirli dosya veya klasörlere erişimi kısıtlamanıza olanak tanır. Rol yönetimi, birkişinin rolünü programlı olarak belirleyebilmeniz veya belirli bir roldeki tüm kullanıcıları belirleyebilmeniz ve buna göre yanıt verebilmeniz için bir API de sağlar.

Rol yönetimi ASP.NET üyeliğinde bir gereklilik olmadığı gibi, rol yönetimini kullanmak için de üyelik bir gereklilik değildir. Ancak, iki güzel birbirlerine ek ve geliştiriciler birbirleriyle birlikte bunları kullanacak muhtemeldir.

Uygulamanızda rol yönetimini etkinleştirmek için web.config dosyanızda aşağıdaki değişikliği yapın:

[!code-xml[Main](membership/samples/sample2.xml)]

**CacheRolesInCookie** özniteliği doğru ayarlandığında, ASP.NET istemcideki bir çerezde kullanıcıların rol üyeliğini önbelleğe alar. Bu, rol aramalarının RoleProvider'a çağrı lmadan gerçekleşmesini sağlar. Bu özniteliği kullanırken, **geliştiricilerin çerez Koruması** özniteliğinin Tümü'ne ayarlandığından emin olması önerilir. (Bu varsayılan ayardır.) Bu, çerez verilerinin şifrelenmesini sağlar ve tanımlama bilgilerinin değiştirilmediğinden emin olmaya yardımcı olur. Roller, Web Sitesi Yönetim Aracı kullanılarak eklenebilir. Rolleri kolayca tanımlamanızı, bu rollere göre sitenin bölümlerine erişimi yapılandırmanızı ve kullanıcıları rollere atamanızı sağlar.

![](membership/_static/image6.jpg)

**Şekil 6**

Yukarıda gösterildiği gibi, yalnızca rolün adını girerek ve sonra Rol Ekle'yi tıklatarak yeni roller eklenebilir. Varolan roller, varolan roller listesindeki uygun bağlantıyı tıklatarak yönetilebilir veya silinebilir.

Bir rolü yönetirken, aşağıda gösterildiği gibi kullanıcıları ekleyebilir veya kaldırabilirsiniz.

![](membership/_static/image7.jpg)

**Şekil 7**

Kullanıcı Rol'da dır onay kutusunu denetleyerek, kullanıcıyı belirli bir role kolayca ekleyebilirsiniz. ASP.NET, üyelik veritabanınızı uygun girişlerle otomatik olarak günceller. Ayrıca, uygulamanız için erişim kurallarını yapılandırmak isteyeceksiniz. ASP.NET 1.x geliştiricileri bunu web.config dosyasındaki &lt;yetkilendirme&gt; öğesi aracılığıyla yapmaya aşinadırlar ve bu seçenek 2.0 ASP.NET hala mevcuttur. Ancak, aşağıda gösterildiği gibi Web Sitesi Yönetim Aracı'nı kullanarak erişim kurallarını yönetmek daha kolaydır.

![](membership/_static/image8.jpg)

**Şekil 8**

Bu durumda, Yönetim klasörü vurgulanır (araç açık gri olarak vurgulandığı için görülmesi zor) ve Yöneticiler rolüne erişim izni verilmiştir. Diğer tüm kullanıcılar reddedilir. Bir kural seçmek için kafa simgesine tıklayabilir ve ardından kuralları düzenlemek için Yukarı ve Aşağı Taşı düğmelerini kullanabilirsiniz. ASP.NET &lt;yetkilendirme&gt; öğesinde olduğu gibi, kurallar göründükleri sırada işlenir. Başka bir deyişle, yukarıdaki çekimdeki kuralların sırası tersine çevrilseydi, hiç kimse Yönetim klasörüne erişemaz, çünkü ASP.NET karşılaşacağı ilk kural herkesi klasöre inleyen kural olacaktır.

ASP.NET 2.0, erişim kuralı belirttiğiniz klasöre bir web.config dosyası ekler. Erişim kuralları yapılandırma dosyası veya Web Sitesi Yönetim Aracı üzerinden düzenlenebilir. Başka bir deyişle, Web Sitesi Yönetim Aracı, yapılandırma dosyasının kullanıcı dostu bir ortamda düzenlenebileceği basit bir arabirimdir.

## <a name="using-roles-in-code"></a>Koddaki Rolleri Kullanma

Rol yönetimi için API sürüm 1.x'ten beri değişmedi. **IsInRole** yöntemi, bir kullanıcının belirli bir rolde olup olmadığını belirlemek için kullanılır.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET, geçerli bağlamın bir üyesi olarak roleprincipal örneğini de oluşturur. RolePrincipal nesnesi, kullanıcının ait olduğu tüm rolleri aşağıdaki gibi elde etmek için kullanılabilir:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>Giriş Görünümü Denetimi ile Rol Gruplarını Kullanma

Artık rol yönetimi ve üyelik konusunda bir anlayışa sahip olduğunuza göre, LoginView denetiminin bu yetenekten nasıl yararlandığını ASP.NET 2.0'da kısaca tartışalım. Daha önce de tartışıldığı gibi, LoginView denetimi varsayılan olarak iki şablon içeren şablonlu bir denetimdir; AnonymousTemplate ve LoggedInTemplate. LoginView Görevler iletişim kutusunda RoleGroups'ları görüntülemenize olanak tanıyan bir bağlantı (aşağıda gösterilmiştir) yer almaktadır.

![](membership/_static/image9.jpg)

**Şekil 9**

Her RoleGroup nesnesi, RoleGroup'un hangi rollere uygulandığını tanımlayan bir dizi dize içerir. LoginView denetimine yeni bir RoleGroup eklemek için RoleGroups'u Edit bağlantısını tıklatın. Yukarıdaki resimde, Yöneticiler için yeni bir RoleGroup eklediğimi görebilirsiniz. Görünümler açılır bölümünden rol grubunu (RoleGroup[0]) seçerek, yalnızca Yöneticiler rolünün üyelerine görüntülenecek bir şablon uyguluyorum. Aşağıdaki resimde, Satış rolü ve Dağıtım rolü üyeleri için geçerli olan yeni bir RoleGroup ekledik. Bu, LoginView Görevler iletişim kutusundaki Görünümler açılır listesine ikinci bir RoleGroup ekler ve bu şablona eklenen her şey Satış veya Dağıtım rolündeki herhangi bir kullanıcı tarafından görünür olur.

![](membership/_static/image10.jpg)

**Şekil 10**

## <a name="overriding-the-existing-membership-provider"></a>Varolan Üyelik Sağlayıcısının Geçersiz Kılınması

ASP.NET üyeliğin işlevselliğini genişletmenin birkaç yolu vardır. Her şeyden önce, sqlmembershipprovider sınıfının varolan işlevselliğini, ondan devralarak ve yöntemlerini geçersiz kılarak değiştirebilirsiniz. Örneğin, kullanıcılar oluşturulduğunda kendi işlevselliğinizi uygulamak istiyorsanız, SqlMembershipProvider'dan aşağıdaki gibi devralan kendi sınıfınızı oluşturabilirsiniz:

[!code-csharp[Main](membership/samples/sample5.cs)]

Diğer taraftan, kendi sağlayıcınızı oluşturmak istiyorsanız (örneğin, üyelik bilgilerinizi bir Access veritabanında depolamak için), kendi sağlayıcınızı oluşturabilirsiniz.

## <a name="creating-your-own-membership-provider"></a>Kendi Üyelik Sağlayıcınızı Oluşturma

Kendi üyelik sağlayıcınızı oluşturmak için öncelikle MembershipProvider sınıfından devralan bir sınıf oluşturmanız gerekir. VB.NET kullanıyorsanız, Visual Studio 2005 geçersiz kılmanız gereken tüm yöntemler için saplamalar ekleyecektir. C# kullanıyorsanız, saplamalar eklemek için size kalmış.

Aşağıdakileri geçersiz kılmanız gerekir:

- ApplicationName özelliği
- Parolayı Değiştir
- ChangePasswordQuestionAndAnswer fonksiyonu
- CreateUser fonksiyonu
- DeleteUser işlevi
- EnablePasswordReset özelliği
- ParolaRetrieval özelliğini etkinleştirme
- FindUsersByEmail fonksiyonu
- FindUsersByName fonksiyonu
- GetAllUsers fonksiyonu
- GetNumberOfUsersOnline fonksiyonu
- Parola'yı al işlevi
- GetUser işlevi
- GetUserNameByEmail fonksiyonu
- MaxInvalidPasswordGirişimleri özelliği
- MinRequiredNonAlphanumericCharacters özelliği
- MinRequiredPasswordLength özelliği
- PasswordAttemptWindow özelliği
- PasswordFormat özelliği
- PasswordStrengthRegularExpression özelliği
- RequiresQuestionAndAnswer özelliği
- RequiresUniqueEmail özelliği
- Parolayı sıfırlama işlevi
- Kullanıcı işlevinin kilidini açma
- UpdateUser fonksiyonu
- DoğrulamaKullanıcı işlevi

Bir C# geliştiricisi olarak uygulamak için oldukça iyi bir liste. Herhangi bir uygulama olmadan VB.NET sınıf oluşturmak ve daha sonra c # kodu dönüştürmek için .NET Reflektör veya benzer bir araç kullanabilirsiniz daha kolay bulabilirsiniz.

Bağlantı dizesi ve diğer özellikler, Initialize yönteminde varsayılanlarına ayarlanmalıdır. (Sağlayıcı çalışma zamanında yüklendiğinde Başlatma yöntemi çalıştırılır.) Initialize yönteminin ikinci parametresi System.Collections.Specialized.NameValueCollection türünden dir &lt;ve&gt; web.config dosyasındaki özel sağlayıcınızla ilişkili ekle öğesine bir başvurudur. Bu giriş aşağıdaki gibi görünür:

[!code-xml[Main](membership/samples/sample6.xml)]

Burada Initialize yönteminin bir örneğidir.

[!code-csharp[Main](membership/samples/sample7.cs)]

Kullanıcının giriş formunuzu gönderdiğinde doğrulayabilmek için ValidateUser yöntemini kullanmanız gerekir. Bu yöntem, kullanıcı Giriş denetiminde giriş düğmesini tıklattığında ateşler. Bu yöntemde kullanıcı arama yapar kodunuzu yerleştirecektir.

Gördüğünüz gibi, kendi üyelik sağlayıcınızı yazmak zor değildir ve 2.0'ASP.NET bu güçlü işlevselliğini genişletmenize olanak tanır.
