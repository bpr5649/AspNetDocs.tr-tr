---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: Üyelik kullanıcı Store (VB) karşılaştırarak kullanıcı kimlik bilgilerini doğrulama | Microsoft Docs
author: rick-anderson
description: Bu öğreticide hem programlı anlamına gelir ve oturum açma denetimi kullanarak üyelik kullanıcı deposu ile karşılaştırarak kullanıcı kimlik bilgilerini doğrulamak nasıl inceleyeceğiz...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: 98869574adb8ac85a2b6dad8db2a583e013150fe
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393183"
---
# <a name="validating-user-credentials-against-the-membership-user-store-vb"></a>Üyelik Kullanıcı Deposu ile Karşılaştırarak Kullanıcı Kimlik Bilgilerini Doğrulama (VB)

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Kodu indir](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> Bu öğreticide hem programlı anlamına gelir ve oturum açma denetimi kullanarak üyelik kullanıcı deposu ile karşılaştırarak kullanıcı kimlik bilgilerini doğrulamak nasıl inceleyeceğiz. Biz de oturum açma denetimin görünümünü ve davranışını özelleştirmek konuları ele alınacaktır.


## <a name="introduction"></a>Giriş

İçinde <a id="Tutorial05"> </a> [önceki öğretici](creating-user-accounts-vb.md) yeni bir kullanıcı hesabı oluşturma üyelik framework inceledik. İlk program aracılığıyla aracılığıyla kullanıcı hesapları oluşturma sırasında incelemiştik `Membership` sınıfın `CreateUser` yöntemi ve ardından CreateUserWizard Web denetimi kullanarak incelenir. Ancak, oturum açma sayfasına şu anda sağlanan kimlik bilgilerinin sabit kodlanmış bir kullanıcı adı ve parola çiftleri listesi karşı doğrular. Üyelik framework'ün kullanıcı deposu ile karşılaştırarak kimlik bilgilerini doğrular oturum açma sayfanın mantığını güncelleştirmeye ihtiyacımız var.

Çok gibi kullanıcı hesapları oluşturma ile kimlik bilgilerini programlama yoluyla veya bildirimli olarak doğrulanabilir. Üyelik API'si programlı olarak kullanıcı deposu ile karşılaştırarak kullanıcı kimlik bilgilerini doğrulamak için bir yöntem içerir. Ve ASP.NET için kullanıcı adını ve parolayı ve oturum açmak için bir düğmeye metin kutularına bir kullanıcı arabirimiyle işler oturum açma Web denetimi ile birlikte gelir.

Bu öğreticide hem programlı anlamına gelir ve oturum açma denetimi kullanarak üyelik kullanıcı deposu ile karşılaştırarak kullanıcı kimlik bilgilerini doğrulamak nasıl inceleyeceğiz. Biz de oturum açma denetimin görünümünü ve davranışını özelleştirmek konuları ele alınacaktır. Haydi başlayalım!

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1. Adım: Üyelik kullanıcı Store karşı kimlik bilgileri doğrulanıyor

Forms kimlik doğrulaması kullanan Web siteleri için bir kullanıcı Web sitesine bir oturum açma sayfasını ziyaret ederek ve kimlik bilgilerini girmesini oturum açar. Bu kimlik bilgileri, sonra da kullanıcı deposunda karşı karşılaştırılır. Geçerliyse, kullanıcı kimliğini ve ziyaretçi güvenilirliğini gösteren bir güvenlik belirteci bir form kimlik doğrulama anahtarının izni verilir.

Kullanıcı üyeliğini framework karşı doğrulamak için kullanın `Membership` sınıfın [ `ValidateUser` yöntemi](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx). `ValidateUser` Yöntemi alır iki giriş parametresi - `username` ve `password` - ve kimlik bilgilerinin geçerli olup olmadığını gösteren bir Boole değeri döndürür. İle gibi `CreateUser` biz incelenir ve önceki öğreticide yöntemi `ValidateUser` yapılandırılmış üyelik sağlayıcısı için gerçek bir doğrulama yöntemi atar.

`SqlMembershipProvider` Sağlanan kimlik bilgilerinin belirtilen kullanıcının parolasını aracılığıyla elde ederek doğrular `aspnet_Membership_GetPasswordWithFormat` saklı yordamı. Bu geri çağırma `SqlMembershipProvider` üç biçimlerden birini kullanarak kullanıcıların parolalarını depolar: şifrelenmiş veya karma temizleyin. `aspnet_Membership_GetPasswordWithFormat` Saklı yordam, ham biçimde parolayı döndürür. Şifrelenmiş veya karma hale getirilen parola `SqlMembershipProvider` dönüştüren `password` yöntemlere geçirilen değer `ValidateUser` karşılığını yönteme şifrelenmiş veya durumu karma ve veritabanından iade edildiği ile karşılaştırır. Veritabanında depolanan parolanın kullanıcı tarafından girilen biçimlendirilmiş parola eşleşirse, kimlik bilgilerinin geçerli olduğundan.

Oturum açma sayfamızı güncelleştirelim (~ /`Login.aspx`) ve böylece sağlanan kimlik bilgilerinin framework üyelik kullanıcı deposu ile karşılaştırarak doğrular. Bu oturum açma sayfası oluşturduk geri <a id="Tutorial02"> </a> [ *form kimlik doğrulaması bir genel bakış* ](../introduction/an-overview-of-forms-authentication-vb.md) iki metin kutularına kullanıcı adı ve parola ile bir arabirim oluşturma Öğreticisi, bir Beni anımsa onay kutusunu ve oturum açma düğmesi (bkz. Şekil 1). Kod, sabit kodlanmış bir kullanıcı adı ve parola çifti (Scott/parola, Jisun/parola ve Sam/parola) listesiyle girilen kimlik bilgilerini doğrular. İçinde <a id="Tutorial03"> </a> [ *Forms kimlik doğrulaması yapılandırması ve Gelişmiş konular* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) formlarında ek bilgileri depolamak için oturum açma sayfasının kod güncelleştirdik Öğreticisi kimlik doğrulama anahtarı'nın `UserData` özelliği.


[![THe oturum açma sayfasının arabirimi içeren iki metin kutuları, bir CheckBoxList ve bir düğmeyi](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**Şekil 1**: Oturum açma sayfasının arabirimi içeren iki metin kutuları, bir CheckBoxList ve bir düğmeyi ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png))


Oturum açma sayfasının kullanıcı arabirimi değişmeden kalabilir, ancak oturum açma düğmenin değiştirilecek ihtiyacımız `Click` framework üyelik kullanıcı deposu ile karşılaştırarak kullanıcı doğrulama kodunu içeren olay işleyicisi. Olay işleyicisi güncelleştirin, böylece kendi kod aşağıdaki gibi görünür:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

Bu kod, son derece basit bir işlemdir. Çağırarak Başlat `Membership.ValidateUser` yöntemi, belirtilen kullanıcı adı ve parola geçirme. Bu yöntem, True döndürür sonra siteye kullanıcı oturumunu `FormsAuthentication` sınıfın RedirectFromLoginPage yöntemi. (Açıkladığımız gibi <a id="Tutorial02"> </a> [ *form kimlik doğrulaması bir genel bakış* ](../introduction/an-overview-of-forms-authentication-vb.md) öğreticide `FormsAuthentication.RedirectFromLoginPage` forms kimlik doğrulaması biletini oluşturur ve ardından kullanıcı yönlendirir uygun sayfaya.) Kimlik bilgileri ancak geçersiz olduğunda `InvalidCredentialsMessage` etiketi gösterilir, kullanıcı, kullanıcı adı veya parola yanlış olduğunu bildiren.

İşte bu kadar kolay!

Oturum açma sayfasına beklendiği gibi çalışıp çalışmadığını test etmek için önceki öğreticide oluşturduğunuz kullanıcı hesaplarından biri ile oturum açmayı deneyin. Hesabınız henüz oluşturmadıysanız, devam edin ve bir oluşturma `~/Membership/CreatingUserAccounts.aspx` sayfası.

> [!NOTE]
> Kullanıcı kendi kimlik bilgilerini girer ve oturum açma sayfası formunun gönderir, kendi parola içeren kimlik bilgileri web sunucusuna Internet üzerinden iletilir *düz metin*. Ağ trafiğini algılaması herhangi bir bilgisayar korsanı, kullanıcı adı ve parola görebilirsiniz anlamına gelir. Bunu önlemek için onu kullanarak ağ trafiğini şifrelemek için önemlidir [Güvenli Yuva Katmanı (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer). Bu kimlik bilgilerini (aynı zamanda tüm sayfanın HTML biçimlendirmeyi) web sunucusu tarafından alınana kadar kullanıcılar tarayıcı bırakın andan şifrelenir garanti eder.


### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Üyelik Framework geçersiz oturum açma girişimlerini nasıl işler?

Bir ziyaretçi oturum açma sayfasına ulaşır ve kimlik bilgilerini gönderir, kullanıcının tarayıcıyı oturum açma sayfasına bir HTTP isteği yapar. Kimlik bilgilerinin geçerli olduğundan, HTTP yanıtına bir tanımlama bilgisinde kimlik doğrulaması bileti içerir. Bu nedenle, bir bilgisayar korsanının sitenize kesilmeye çalışılıyor olsak da geçerli bir kullanıcı adı ve parola, bir tahmin ile oturum açma sayfasına HTTP istekleri gönderen bir program oluşturabilirsiniz. Parola tahmin doğru ise, oturum açma sayfasına kimlik doğrulaması bileti bir geçerli kullanıcı adı/parola çift stumbled hangi noktada programı bilir tanımlama bilgisi, döndürür. Özellikle parola zayıf yanılma böyle bir program bir kullanıcının parolasını stumble mümkün olabilir.

Bu deneme yanılma saldırıları önlemek için belirli bir sayıda belirli bir süre içinde başarısız oturum açma denemesi olduğunda bir kullanıcının oturumunu üyelik framework kilitler. Tam parametreleri aşağıdaki iki üyelik sağlayıcısı yapılandırma ayarları yapılandırılabilir:

- `maxInvalidPasswordAttempts` -kaç geçersiz parola denemesi için kullanıcı hesabı kilitlenmeden önce geçmesi gereken süre içinde verilir. Varsayılan değer 5'tir.
- `passwordAttemptWindow` -süre sırasında belirtilen geçersiz oturum açma girişimlerinin sayısını neden olacak hesabının kilitlenmesi dakika cinsinden belirtir. Varsayılan değer 10'dur.

Bir kullanıcı kilitlendi, o yönetici hesabını açana kadar oturum açamıyor. Bir kullanıcı kilitli zaman `ValidateUser` yöntemi olacak *her zaman* dönüş `False`geçerli kimlik bilgileri sağlanan bile. Bu davranış bir bilgisayar korsanının deneme yanılma yöntemleri sitenize keser olasılığını azaltır, ancak yalnızca kendi parolasını unutmuş veya yanlışlıkla Caps Lock sahip veya hatalı bir yazma gün yaşanmaktadır geçerli kullanıcının oturumunu kilitleme sona erdirebilirsiniz.

Ne yazık ki, bir kullanıcı hesabının kilidi kaldırma için yerleşik aracı yoktur. Bir hesap kilidini açmak için veritabanı değiştirebilirsiniz doğrudan - `IsLockedOut` alanındaki `aspnet_Membership` uygun kullanıcı hesabı için - tablo ya da kilitlerini seçeneklerle hesapları kilitli listeleyen bir web tabanlı bir arabirim oluşturma. Hesap ve rol ilgili yaygın kullanıcı görevlerini, bir sonraki öğreticide işlemi gerçekleştirmek için yönetim arabirimler oluşturma inceleyeceğiz.

> [!NOTE]
> Tek dezavantajı `ValidateUser` yöntemdir sağlanan kimlik bilgileri geçersiz olduğunda, bunu neden dair herhangi bir açıklama sağlamaz. Kimlik bilgileri, kullanıcı deposunda eşleşen hiçbir kullanıcı adı/parola çift olduğundan veya kullanıcı henüz onaylanmadığı için veya kullanıcı kilitlendi çünkü geçersiz olabilir. Adım 4'te, oturum açma denemesi başarısız olduğunda daha ayrıntılı bir ileti kullanıcıya göstermek nasıl göreceğiz.


## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>2. Adım: Oturum açma Web denetimi aracılığıyla topluyorsunuz kimlik bilgileri

[Oturum açma Web denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) varsayılan kullanıcı arabirimi çok benzeyen oluşturduğumuz geri işler <a id="Tutorial02"> </a> [ *form kimlik doğrulaması bir genel bakış* ](../introduction/an-overview-of-forms-authentication-vb.md) öğretici. Oturum açma denetimi kullanarak bize ziyaretçi kimlik bilgilerini toplamak için bir arabirim oluşturma işlemlerini kaydeder. Ayrıca, oturum açma denetimi otomatik olarak kullanıcının (gönderilen kimlik bilgilerinin geçerli olduğunu varsayarak), böylece bize kod yazmaya gerek kalmamasını imzalar.

Güncelleştirelim `Login.aspx`, el ile oluşturulan arabirimi değiştirme ve kodu ile bir oturum açma denetimi. Mevcut biçimlendirme kaldırarak başlayın ve kod `Login.aspx`. Yükseltebilir silin veya yalnızca yorum çıkarın. Bildirim temelli biçimlendirme yorum yapmak için ile çevreleyen `<%--` ve `--%>` sınırlayıcı. Bu sınırlayıcıları el ile girebilir veya Şekil 2 gösterildiği gibi açıklama satırı yapın ve ardından araç çubuğunda seçilen satırlar simgesi yorum metni seçebilirsiniz. Benzer şekilde, arka plan kod sınıfı seçili kod açıklama için yorum seçili satırları simgesi kullanabilirsiniz.


[![Cklama kullanıma mevcut bildirim temelli biçimlendirme ve kaynak kodunda Login.aspx](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**Şekil 2**: Açıklama çıkış mevcut bildirim temelli işaretleme ve Login.aspx kaynak kodunda ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png))


> [!NOTE]
> Seçili satırları simgesi yorum, bildirim temelli biçimlendirme Visual Studio 2005'te görüntülerken kullanılabilir değil. Visual Studio 2008 kullanmıyorsanız el ile eklemeniz gerekecektir `<%--` ve `--%>` sınırlayıcı.


Ardından, sayfayı açın araç kutusundan bir oturum açma denetimi sürükleyin ve ayarlayın, `ID` özelliğini `myLogin`. Bu noktada, ekran Şekil 3'e benzer görünmelidir. Oturum açma denetimin varsayılan arabirim için kullanıcı adı ve parola, bir Beni Hatırla sonraki açışınızda onay kutusu ve bir günlük düğmesine TextBox denetimi içerdiğini unutmayın. Ayrıca `RequiredFieldValidator` denetimler için iki metin kutuları.


[![Add sayfasına bir oturum açma denetimi](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**Şekil 3**: Sayfa için bir oturum açma denetimi ekleyin ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png))


Ve tamamlandı! Oturum açma denetimin oturum aç düğmesine tıklandığında, bir geri gönderme ortaya çıkar ve oturum açma denetimi çağıracak `Membership.ValidateUser` yöntemini, girilen kullanıcı adı ve parola. Kimlik bilgileri geçersiz olduğunda oturum açma denetimi gibi bildiren bir ileti görüntüler. Ancak, kimlik bilgilerinin geçerli olduğundan, oturum açma denetimi forms kimlik doğrulaması biletini oluşturur ve kullanıcı uygun sayfaya yeniden yönlendirir.

Oturum açma denetimi dört etkene başarılı bir oturum açma sırasında kullanıcıya yeniden yönlendirmek için uygun bir sayfayı belirlemek için kullanır:

- Oturum açma denetimi oturum açma sayfasında tanımlanan olup `loginUrl` forms kimlik doğrulaması yapılandırması; bu ayarın varsayılan değer: `Login.aspx`
- Varlığı bir `ReturnUrl` querystring parametresi
- Oturum açma denetimin değerini [ `DestinationUrl` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)
- `defaultUrl` Değeri belirtilen formlardaki kimlik doğrulaması yapılandırma ayarları; Default.aspx bu ayarın varsayılan değer:

Şekil 4'te nasıl gösterilmektedir, uygun sayfaya kararını ulaşması için bu dört parametre oturum açma denetimi kullanır.


[![Add sayfasına bir oturum açma denetimi](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**Şekil 4**: Sayfa için bir oturum açma denetimi ekleyin ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png))


Oturum açma denetimi tarayıcısından ziyaret ve üyelik Framework var olan bir kullanıcı olarak oturum açmayı test etmek için bir dakikamızı ayıralım.

Oturum açma denetimin işlenmiş arabirimi yüksek oranda yapılandırılabilir. Bir dizi görünümünü etkileyen özellikler vardır; Bunun da ötesinde, oturum açma denetimi düzeni üzerinde kesin denetim için bir şablona kullanıcı arabirimi öğeleri dönüştürülebilir. Bu adımı geri kalanı nasıl görünümünü ve düzeni özelleştirildiği inceler.

### <a name="customizing-the-login-controls-appearance"></a>Oturum açma denetimin görünümünü özelleştirme

Bir kullanıcı arabirimi bir başlık (günlük) ile oturum açma denetimin varsayılan özellik ayarları işlenemedi, kullanıcı adı ve parolası girişleri için bir Beni Hatırla metin kutusu ve etiket denetimleri yanındaki onay kutusunu ve oturum aç düğmesine zaman. Bu öğelerin görünüm çok sayıda oturum açma denetimin özellikleri aracılığıyla tüm yapılandırılabilir özelliktedir. Ayrıca, bir özellik ya da iki ayarlayarak - - yeni kullanıcı hesabı oluşturmak için bir sayfaya bağlantı gibi ek kullanıcı arabirimi öğeleri eklenebilir.

Şimdi oturum açma denetimimiz görünümünü oluşturan gussy için birkaç dakikanızı ayırın. Bu yana `Login.aspx` sayfa, oturum açma bildiren sayfanın üst kısmındaki metni zaten sahipse, oturum açma denetimin başlık gereksiz. Bu nedenle, temizleyin [ `TitleText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) oturum açma denetimin başlığı kaldırmak için değer.

Kullanıcı adı: ve parola: İki TextBox solundaki etiketleri aracılığıyla özelleştirilebilir [ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) ve [ `PasswordLabelText` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)sırasıyla. Kullanıcı adı olarak değiştirelim: Kullanıcı adı okunamıyor etiketi:. Etiket ve metin stilleri aracılığıyla yapılandırılabilir [ `LabelStyle` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) ve [ `TextBoxStyle` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)sırasıyla.

Sonraki zaman CheckBox'ın metin özelliği, oturum açma denetimin ayarlanabilir Beni Hatırla [ `RememberMeText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx), ve varsayılan durumu aracılığıyla yapılandırılabilir işaretli [ `RememberMeSet` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx)(hangi varsayılan olarak False). Devam etmek ve ayarlamak `RememberMeSet` özelliğini True Beni Hatırla sonraki saat onay kutusu, varsayılan olarak işaretli olacaktır.

Oturum açma denetimi, kullanıcı arabirimi denetimleri düzenini ayarlamak için iki özellik sunar. [ `TextLayout` Özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) belirtir olup olmadığını kullanıcı adı: ve parola: Kendi ilgili metin kutularına (varsayılan) ya da bunların yukarıda sol etiketleri görünür. [ `Orientation` Özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) kullanıcı adı ve parola girişleri dikey yer olup olmadığını gösterir (biri diğerinin) ya da yatay olarak. Bu iki özellik değerlerinde bırakın tıklıyorum, ancak bu iki özellik sonuçta elde edilen etkisini görmek için varsayılan olmayan değerlerine yapmayı deneyin geçmenizi öneriyoruz.

> [!NOTE]
> Sonraki bölümde, oturum açma denetimin düzenini yapılandırma biz şablonları Düzen denetimin kullanıcı arabirimi öğeleri kesin düzenini tanımlamak için kullanacaksınız.


Oturum açma denetimin özellik ayarlarını ayarlayarak kaydırma [ `CreateUserText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) ve [ `CreateUserUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) için henüz kayıtlı değil mi? Bir hesap oluşturun! ve `~/Membership/CreatingUserAccounts.aspx`sırasıyla. Bu sayfaya işaret eden bir oturum açma denetimin arabirimi oluşturduğumuz köprü ekler <a id="Tutorial05"> </a> [önceki öğretici](creating-user-accounts-vb.md). Oturum açma denetimin [ `HelpPageText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) ve [ `HelpPageUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) ve [ `PasswordRecoveryText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) ve [ `PasswordRecoveryUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) bağlantılar yardım sayfasına ve parola kurtarma sayfa işleme aynı şekilde çalışır.

Bu özellik değişiklikleri yaptıktan sonra oturum açma denetiminizin bildirim temelli işaretleme ve görünüm Şekil 5'te gösterilen şuna benzemelidir.


[![THe oturum açma denetimin özelliklerini değerleri dikte ait Görünüm](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**Şekil 5**: Oturum açma denetimin özelliklerini değerleri dikte ait Görünüm ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png))


### <a name="configuring-the-login-controls-layout"></a>Oturum açma denetimin düzenini yapılandırma

Oturum açma Web denetimin varsayılan kullanıcı arabirimi bir HTML arabiriminde kullanıma yerleştirir `<table>`. Ancak biz işlenen çıkışı üzerinde daha ince denetim ihtiyacım olursa ne? Belki de değiştirmek istiyoruz `<table>` bir dizi `<div>` etiketler. Veya uygulamamız ek kimlik bilgileri kimlik doğrulaması için ne gerekir? Birçok finansal Web siteleri, örneğin, yalnızca bir kullanıcı adı ve parola, ancak Ayrıca kişisel kimlik numarası (PIN) veya diğer kişisel bilgilerini sağlamak kullanıcıların gerektirir. İnovasyonunuz ne olursa olsun, nedenleri olabilir, oturum açma denetimi, biz açıkça arabirimin bildirim temelli biçimlendirme tanımlayabilirsiniz bir şablona dönüştürülecek mümkündür.

Ek kimlik bilgileri toplamak için oturum açma denetimi güncelleştirmek için iki işlem gerçekleştirmesi gerekir:

1. Ek kimlik bilgileri toplamak için Web denetim eklemek için oturum açma denetimin arabirimi güncelleştirin.
2. Oturum açma denetimin iç kimlik doğrulaması mantığı, böylece bir kullanıcının kullanıcı adı ve parola geçerli ise ve ek kimlik bilgilerini çok geçerli, yalnızca kimliği geçersiz kılar.

İlk görev gerçekleştirmek için oturum açma denetimi bir şablona dönüştürmeniz ve gerekli Web denetimleri eklemek ihtiyacımız var. İkinci görev olduğu gibi oturum açma denetimin kimlik doğrulaması mantığı denetim için bir olay işleyicisi oluşturarak yerini [ `Authenticate` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx).

Böylece kullanıcılar kendi kullanıcı adı, parola ve e-posta adresi ister ve yalnızca sağlanan e-posta adresine e-posta adresi dosya çubuğunda eşleşmesi durumunda kullanıcının kimliğini doğrular oturum açma denetimi güncelleştirelim. İlk oturum açma denetimin arabirimi bir şablona dönüştürülecek ihtiyacımız var. Oturum açma denetimin akıllı etiketten dönüştürme şablonu seçeneğini seçin.


[![Cbir şablon için oturum açma denetimi yayınına](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**Şekil 6**: Oturum açma denetimi bir şablona dönüştürün ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png))


> [!NOTE]
> Oturum açma denetimi, önceden template sürümüne geri almak için akıllı etiket denetimin sıfırlama bağlantısını tıklayın.


Oturum açma denetimi için bir şablonu dönüştürme ekler bir `LayoutTemplate` denetimin HTML öğelerinin ve kullanıcı arabirimi tanımlama Web denetimleri ile bildirim temelli biçimlendirme için. Şekil 7 gösterildiği gibi bir şablona denetimine dönüştürmeden çeşitli özellikleri Özellikler penceresinden gibi kaldırır `TitleText`, `CreateUserUrl`, vb., sonra bu özellik değerleri, bir şablon kullanırken göz ardı edilir.


[![Fvarlıkları özellikler kullanılabilir olduğunda oturum açma denetimi bir şablona dönüştürülür:](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**Şekil 7**: Kullanılabilir olduğunda oturum açma denetimi bir şablona dönüştürülür daha az özelliklerdir ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png))


HTML biçimlendirmeyi `LayoutTemplate` gerektiğinde değiştirilebilir. Benzer şekilde, tüm yeni Web denetimleri şablona eklemekten çekinmeyin. Ancak, bu oturum açma denetimin çekirdek Web denetimleri şablonda kalır ve atanmış tutmak önemlidir `ID` değerleri. Özellikle, yeniden adlandırmak veya kaldırmayın `UserName` veya `Password` metin kutuları, `RememberMe` onay kutusunu `LoginButton` düğmesi `FailureText` etiketi veya `RequiredFieldValidator` kontrol eder.

Ziyaretçi e-posta adresi toplamak için biz TextBox şablona eklemeniz gerekir. Aşağıdaki bildirim temelli biçimlendirmeyi tablo satırı arasındaki ekleyin (`<tr>`) içeren `Password` metin kutusu ve Beni Hatırla sonraki tutan bir tablo satırının onay kutusu süresi:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

Ekledikten sonra `Email` metin kutusu, bir tarayıcı aracılığıyla sayfasını ziyaret edin. Şekil 8 gösterildiği gibi oturum açma denetimin kullanıcı arabirimi artık üçüncü bir textbox içerir.


[![THe Login denetimi artık bir metin kutusu için kullanıcının e-posta adresini içerir](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**Şekil 8**: Oturum açma denetimi için kullanıcının e-posta adresi artık Textbox içerir ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png))


Bu noktada, oturum açma denetimi hala kullanarak `Membership.ValidateUser` sağlanan kimlik bilgilerini doğrulamak için yöntemi. Değer gelenlere, girilen `Email` metin kutusu kullanıcı oturum açabilir üzerinde hiçbir seçtiğiniz sahiptir. 3. adımda kimlik bilgilerini yalnızca kullanıcı adı ve parola geçerli olduğunu ve sağlanan e-posta adresi dosya çubuğunda e-posta adresiyle eşleşiyor, geçerli olarak kabul edilir, böylece oturum açma denetimin kimlik doğrulaması mantığı geçersiz kılma atacağız.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3. Adım: Oturum açma denetimin kimlik doğrulaması mantığı değiştirme

Her bir ziyaretçi sağlar, kimlik bilgileri ve oturum aç düğmesine, bir geri gönderme ensues tıklama ve oturum açma, kimlik doğrulama iş akışı durumuna ilerler denetler. İş akışı yükselterek başlar [ `LoggingIn` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx). Bu olay ile ilişkilendirilmiş herhangi bir olay işleyicilerinin işlem günlüğünde ayarlayarak iptal edebilirsiniz `e.Cancel` özelliğini `True`.

Oturum açma işlemi iptal edilmemiş, iş akışı yükselterek ilerledikçe [ `Authenticate` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx). Bir olay işleyicisi varsa `Authenticate` olay ve ardından, sağlanan kimlik bilgilerinin geçerli olup olmadığını belirlemekten sorumludur. Hiçbir olay işleyicisi belirtildiyse, oturum açma denetimi kullanır `Membership.ValidateUser` kimlik bilgilerinin geçerliliğini belirlemek için yöntemi.

Sağlanan kimlik bilgilerinin geçerli olduğundan sonra forms kimlik doğrulaması biletinin oluşturulduğu [ `LoggedIn` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) ortaya çıkar ve kullanıcı uygun sayfaya yönlendirilir. Ancak, kimlik bilgileri geçersiz, gerekirse, ardından [ `LoginError` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) oluşturulur ve kullanıcı kimlik bilgilerini geçersiz olduğunu bildiren bir ileti görüntülenir. Yalnızca denetim varsayılan olarak, oturum açma hatası ayarlar kendi `FailureText` (, oturum açma girişimi başarılı değildi. bir hata iletisi için denetimin metin özelliği etiketi Lütfen yeniden deneyin). Ancak, oturum açma denetimin [ `FailureAction` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) ayarlanır `RedirectToLoginPage`, ardından oturum açma denetimi sorunları bir `Response.Redirect` sorgu dizesi parametresini ekleyerek oturum açma sayfasına `loginfailure=1` (neden olan oturum açma hata iletisi görüntülemek için Denetim).

Şekil 9, kimlik doğrulama iş akışı bir akış çizelgesi sunar.


[![THe oturum açma denetimin kimlik doğrulama iş akışı](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**Şekil 9**: Oturum açma denetimin kimlik doğrulama iş akışı ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png))


> [!NOTE]
> Ne zaman kullanacağınız gerçekleştireceğini merak edenler varsa `FailureAction`'s `RedirectToLogin` seçeneği sayfasında, aşağıdaki senaryoyu göz önünde bulundurun. Şu anda bizim `Site.master` ana sayfa şu anda stranger anonim bir kullanıcı tarafından ziyaret edildiğinde sol sütunda görüntülenen metni, Hello var ancak Biz bu metni bir oturum açma denetimleri ile değiştirmek istediğinizi düşünelim. Bu sitede oturum açma sayfasına doğrudan gitmek gerek yerine herhangi bir sayfadan oturum açmak anonim kullanıcı çalıştırmasına olanak tanır. Bir kullanıcının ana sayfa tarafından işlenen oturum açma denetimi aracılığıyla oturum olduysa, ancak bu oturum açma sayfasına yeniden yönlendirmek mantıklı olabilir (`Login.aspx`) ek yönergeler, bağlantılar ve diğer Yardım - bağlantıları oluşturma gibi büyük olasılıkla bu sayfa içerdiği için bir Yeni hesap veya ana sayfaya eklenmedi kayıp parola - alın.


### <a name="creating-theauthenticateevent-handler"></a>Oluşturma`Authenticate`olay işleyicisi

Bizim Özel kimlik doğrulama mantığı eklenebilecek için oturum açma denetim için bir olay işleyicisi oluşturmak gerekiyor `Authenticate` olay. Bir olay işleyicisi oluşturma `Authenticate` olayı aşağıdaki olay işleyici tanımını oluşturur:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

Gördüğünüz gibi `Authenticate` olay işleyicisinin türü bir nesne geçirilen [ `AuthenticateEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) , ikinci bir giriş parametresi olarak. `AuthenticateEventArgs` Sınıfı içeren adlı bir Boolean özelliği `Authenticated` sağlanan kimlik bilgilerinin geçerli olup olmadığını belirtmek için kullanılır. Bizim görev, sağlanan kimlik bilgilerinin geçerli olup olmadığını belirler. kodu buraya yazın ve ayarlamak için ise `e.Authenticate` özelliği uygun şekilde.

### <a name="determining-and-validating-the-supplied-credentials"></a>Belirleme ve sağlanan kimlik bilgileri doğrulanıyor

Oturum açma denetimin kullanın [ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) ve [ `Password` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) kullanıcı tarafından girilen kullanıcı adı ve parola kimlik bilgilerini belirlemek için. Herhangi bir ek Web denetimlere girilen değerleri belirlemek için (gibi `Email` önceki adımda eklediğimiz metin kutusu), kullanın `LoginControlID.FindControl`("*`controlID`*") Web programlı bir başvuru almak için şablonda ayarlanmış denetim `ID` özelliğini eşittir *`controlID`*. Örneğin, bir başvuru almak için `Email` metin kutusuna aşağıdaki kodu kullanın:

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

Kullanıcının kimlik bilgilerini doğrulamak için şu iki şey yapmanız gerekir:

1. Sağlanan kullanıcı adı ve parola geçerli olduğundan emin olun
2. Girilen e-posta adresi dosya oturum açma girişiminde bulunan kullanıcı için e-posta adresi ile eşleştiğinden emin olun

Yalnızca kullanabileceğiniz ilk denetimi gerçekleştirmek için `Membership.ValidateUser` 1. adımda gördüğümüz gibi yöntemi. İkinci kontrol edin, böylece biz TextBox denetimine girilen e-posta adresine karşılaştırabilirsiniz kullanıcının e-posta adresini belirlemek ihtiyacımız var. Belirli bir kullanıcı hakkında bilgi almak için kullanın `Membership` sınıfın [ `GetUser` yöntemi](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx).

`GetUser` Yöntemi birkaç aşırı yüklemeleri vardır. Tüm parametreleri geçirme olmadan kullanılırsa, şu anda oturum açmış kullanıcı hakkındaki bilgileri döndürür. Belirli bir kullanıcı hakkında bilgi almak için arama `GetUser` kendi kullanıcı adını geçirerek. Her iki durumda da `GetUser` döndürür bir [ `MembershipUser` nesne](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), sahip olduğu gibi özellikleri `UserName`, `Email`, `IsApproved`, `IsOnline`ve benzeri.

Aşağıdaki kod, bu iki denetimler uygular. Her ikisi de, ardından geçirirseniz `e.Authenticate` ayarlanır `True`, aksi takdirde atanan `False`.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

Doğru kullanıcı adını, parolayı ve e-posta adresi girerek geçerli bir kullanıcı olarak oturum açmak Bu kod bir yerde çalışır. Yeniden deneyin, ancak bu kez kullanılamıyor.%n%nÇözüm yanlış e-posta adresi kullanın (bkz. Şekil 10). Son olarak, mevcut olmayan bir kullanıcı adı kullanarak bir üçüncü kez deneyin. İlk durumda, başarıyla siteye oturum açmış, ancak son iki durumda da oturum açma denetimin geçersiz kimlik bilgileri iletisini görmeniz gerekir.


[![Taslan e-posta adresi yanlış sağlanırken oturum açamıyorsanız](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**Şekil 10**: Tito olamaz günlük olarak, sağlama yanlış bir e-posta adresi ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png))


> [!NOTE]
> 1. adım, nasıl üyelik Framework işleme geçersiz oturum açma denemesi bölümünde açıklandığı gibi `Membership.ValidateUser` yöntemi çağrılır ve geçirilen geçersiz kimlik bilgileri, geçersiz oturum açma girişimi izler ve belirli bir aşarsanız, kullanıcının oturumunu kilitler Belirtilen bir zaman penceresi içinde geçersiz denemeleri eşiği. Bizim Özel kimlik doğrulama mantığı çağrıları beri `ValidateUser` yöntemi, geçerli bir kullanıcı adı için hatalı bir parolanın geçersiz oturum açma denemesi sayaç artış, ancak kullanıcı adı ve parola olduğu geçerli durumda bu sayaç artırılır değil ancak e-posta adresi doğru değil. Olasılığınız yüksektir, bir bilgisayar korsanının kullanıcı adı ve parolanızı biliyorsanız, ancak kullanıcının e-posta adresini belirlemek için tekniklerini yanılma kullanmak zorunda, olası olduğundan bu davranışı uygundur.


## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4. Adım: Oturum açma denetimin geçersiz kimlik bilgileri iletisi geliştirme

Geçersiz kimlik bilgileri ile oturum açmak bir kullanıcı çalıştığında, oturum açma denetimi oturum açma girişimi başarısız olduğunu açıklayan bir ileti görüntüler. Özellikle, denetim tarafından belirtilen iletiyi görüntüleyen kendi [ `FailureText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx), sahip olduğu bir varsayılan değeri, oturum açma denemesi başarılı olmadı. Lütfen yeniden deneyin.

Geri çağırma bir kullanıcının kimlik bilgileri geçersiz neden olabilecek birçok neden vardır:

- Kullanıcı adı yok
- Kullanıcı adı var, ancak parola geçersiz
- Kullanıcı adı ve parolanın geçerli olup, ancak kullanıcı henüz onaylanmamış
- Kullanıcı adı ve parolanın geçerli olup, ancak kullanıcının kilitlenip çıkış (bunlar belirtilen bir zaman çerçevesi içinde geçersiz oturum açma girişimlerinin sayısını aştığı için büyük olasılıkla)

Ve özel kimlik doğrulama mantığı kullanırken başka nedenler olabilir. Örneğin, kodla yazdığımız adım 3, kullanıcı adı ve parola geçerli olabilir, ancak e-posta adresi yanlış olabilir.

Neden kimlik bilgilerinin geçersiz olmasından bağımsız olarak, oturum açma denetimi aynı hata iletisini görüntüler. Bu geri besleme eksikliği bir kullanıcının hesabı henüz onaylanmadığı veya kimin kilitlendi kafa karıştırıcı olabilir. Biraz iş, yine de size daha uygun bir ileti görüntüler oturum açma denetimi olabilir.

Her bir kullanıcının çalıştığı oturum açma denetimi başlatır geçersiz kimlik bilgileri ile oturum açmak kendi `LoginError` olay. Devam edin ve bu olay için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

Yukarıdaki kod, oturum açma denetimin ayarlayarak başlatır `FailureText` özelliğini (, oturum açma girişimi başarılı değildi. varsayılan değer Lütfen yeniden deneyin). Ardından sağlanan kullanıcı adı var olan bir kullanıcı hesabına eşlenir, görmek için denetler. Bu nedenle, bu sonuç başvuruyorsa `MembershipUser` nesnenin `IsLockedOut` ve `IsApproved` hesap kilitlendi, veya henüz onaylanmadığı belirlemek için özellikleri. Her iki durumda da `FailureText` özelliği için karşılık gelen bir değer güncelleştirilir.

Bu kodu test etmek için var olan bir kullanıcı olarak oturum açın, ancak yanlış bir parola kullanmak kullanılamıyor.%n%nÇözüm deneyin. Bu beş satır içinde 10 dakikalık bir zaman çerçevesinde yapın ve hesap kilitlenir. Şekil 11 gösterir, sonraki oturum açma girişimleri her zaman başarısız (doğru parolayla bile) ancak şimdi daha açıklayıcı olarak hesabınızda çok fazla geçersiz oturum açma denemesi nedeniyle kilitlendi. Lütfen Hesap kilidi iletiniz için yöneticinize başvurun.


[![Taslan gerçekleştirilen çok fazla sayıda geçersiz oturum açma denemesi ve var olan kilitli Out](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**Şekil 11**: Tito gerçekleştirilen çok fazla sayıda geçersiz oturum açma denemesi ve var olan kilitli Out ([tam boyutlu görüntüyü görmek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png))


## <a name="summary"></a>Özet

Önceki öğreticide Bu, oturum açma sayfamızı sabit kodlanmış bir kullanıcı adı/parola çiftleri listesiyle sağlanan kimlik bilgilerinin doğrulanır. Bu öğreticide, üyelik framework karşı kimlik doğrulamak için sayfanın güncelleştirdik. 1. adımda kullanarak olan incelemiştik `Membership.ValidateUser` yöntemi programlı olarak. 2. adımda size sunduğumuz el ile oluşturulan kullanıcı arabirimi ve kod oturum açma denetimi ile değiştirildi.

Oturum açma denetimi bir standart oturum açma kullanıcı arabirimi oluşturur ve kullanıcının kimlik bilgilerini üyelik framework karşı otomatik olarak doğrular. Ayrıca, geçerli kimlik bilgilerini durumunda oturum açma denetimi form kimlik doğrulaması oturum açtığında. Kısacası, tam olarak işlevsel bir oturum açma kullanıcı deneyimi sayfa, hiçbir ek bildirim temelli işaretleme veya kod gerekli oturum açma denetimi yalnızca sürükleyerek kullanılabilir. Daha fazla nedir, oturum açma denetimi üst düzeyde bir işlenen kullanıcı arabirimi ve kimlik doğrulama mantığı denetime olanak yüksek düzeyde özelleştirilebilir niteliktedir.

Bu noktada Web sitemizi ziyaret edenlerin yeni kullanıcı hesabı ve günlük siteye oluşturabilirsiniz, ancak sayfa kimliği doğrulanmış kullanıcıya göre erişimi kısıtlama aramak henüz. Şu anda, herhangi bir kullanıcı kimliği doğrulanmış veya anonim, sitemizde herhangi bir sayfasında görüntüleyebilirsiniz. Bir kullanıcı tarafından temelinde bizim sitenin sayfalarına erişimi denetleme yanı sıra kullanıcı olan işlevselliği bağlıdır belirli sayfalar olabilir. Erişim ve oturum açmış kullanıcıya bağlı olarak sayfa içi işlevselliğini sınırlamak nasıl bir sonraki öğreticiye bakar.

Mutlu programlama!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kilitli ve onaylı olmayan kullanıcılar için özel iletilerini görüntüleme](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0'ın İnceleme üyelik, roller ve profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Nasıl yapılır: ASP.NET oturum açma sayfası oluşturma](https://msdn.microsoft.com/library/ms178331.aspx)
- [Oturum açma denetimi teknik belgeler](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Oturum açma denetimleri kullanma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Scott Mitchell, birden çok ASP/ASP.NET Books yazar ve poshbeauty.com sitesinin 4GuysFromRolla.com, Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan  *[Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott, konumunda ulaşılabilir [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) veya kendi blog'da aracılığıyla [ http://ScottOnWriting.NET ](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğretici için müşteri adayı gözden geçirenler Teresa Murphy ve Michael Olivero yoktu. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Önceki](creating-user-accounts-vb.md)
> [İleri](user-based-authorization-vb.md)
