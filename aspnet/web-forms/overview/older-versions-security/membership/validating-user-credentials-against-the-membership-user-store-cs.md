---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: Kullanıcı kimlik bilgilerini üyelik kullanıcı deposunda doğrulama (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: fd50f4e63c75cf77eb21629d0c11a859da6b357d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045240"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>Üyelik Kullanıcı Deposu ile Karşılaştırarak Kullanıcı Kimlik Bilgilerini Doğrulama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır. Ayrıca, oturum açma denetiminin görünümünü ve davranışını özelleştirmeye de bakacağız.

## <a name="introduction"></a>Giriş

<a id="Tutorial05"></a> [Önceki öğreticide](creating-user-accounts-cs.md) , üyelik çerçevesinde yeni bir kullanıcı hesabı oluşturmayı inceledik. İlk olarak, sınıfın yöntemi aracılığıyla Kullanıcı hesapları oluşturmaya `Membership` `CreateUser` ve ardından CreateUserWizard Web denetimi kullanılarak incelenmiştik. Ancak, oturum açma sayfası şu anda belirtilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı ve parola çiftleri listesine göre doğrular. Oturum açma sayfasının mantığını, üyelik çerçevesinin Kullanıcı deposunda kimlik bilgilerini doğrulayacak şekilde güncelleştirmemiz gerekiyor.

Kullanıcı hesapları oluşturma konusunda çok benzer şekilde, kimlik bilgileri programlı bir şekilde veya bildirimli olarak doğrulanabilir. Üyelik API 'SI, kullanıcının kimlik bilgilerini Kullanıcı deposuna göre doğrulamaya yönelik bir yöntem içerir. Ve ASP.NET, oturum açma Web denetimiyle birlikte gönderilir. Bu, Kullanıcı arabirimini Kullanıcı arabirimi, Kullanıcı adı ve parola için metin kutularına ve oturum açmak için bir düğmeye sahiptir.

Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır. Ayrıca, oturum açma denetiminin görünümünü ve davranışını özelleştirmeye de bakacağız. Haydi başlayalım!

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1. Adım: üyelik kullanıcı deposunda kimlik bilgilerini doğrulama

Form kimlik doğrulaması kullanan Web siteleri için, bir Kullanıcı oturum açma sayfasını ziyaret ederek ve kimlik bilgilerini girerek Web sitesinde oturum açar. Bu kimlik bilgileri daha sonra kullanıcı deposu ile karşılaştırılır. Bunlar geçerliyse, kullanıcıya ziyaretçinin kimliğini ve gerçekliğini gösteren bir güvenlik belirteci olan bir form kimlik doğrulama bileti verilir.

Bir kullanıcıyı üyelik çerçevesine karşı doğrulamak için, `Membership` sınıfının [ `ValidateUser` metodunu](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)kullanın. `ValidateUser`Yöntemi iki giriş parametresi alır- *`username`* ve *`password`* -kimlik bilgilerinin geçerli olup olmadığını gösteren bir Boole değeri döndürür. `CreateUser`Önceki öğreticide incelenen yöntemi beğendiniz, `ValidateUser` yöntemi, yapılandırılmış üyelik sağlayıcısına gerçek doğrulamayı devreder.

, `SqlMembershipProvider` Belirtilen kullanıcı parolasını saklı yordam aracılığıyla alarak sağlanan kimlik bilgilerini doğrular `aspnet_Membership_GetPasswordWithFormat` . `SqlMembershipProvider`Kullanıcıların parolalarını üç biçimden birini kullanarak depoladığını hatırlayın: şifresiz, şifrelenmiş veya karma hale getirilmiş. `aspnet_Membership_GetPasswordWithFormat`Saklı yordam, parolayı ham biçiminde döndürür. Şifrelenmiş ya da karma parolalar için, `SqlMembershipProvider` *`password`* metoduna geçirilen değeri `ValidateUser` eşdeğer şifreli veya karma durumuna dönüştürür ve ardından veritabanından döndürülmüş şekilde karşılaştırır. Veritabanında depolanan parola, Kullanıcı tarafından girilen biçimli parolayla eşleşiyorsa, kimlik bilgileri geçerlidir.

Oturum açma sayfamızı (~/ `Login.aspx` ), üyelik çerçevesi kullanıcı deposunda sağlanan kimlik bilgilerini doğrulamak için güncelleştirelim. Bu oturum açma sayfasını <a id="Tutorial02"></a> [*form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) bölümünde, Kullanıcı adı ve parola, beni anımsa onay kutusu ve oturum açma düğmesi için iki metin kutusuna sahip bir arabirim oluşturma (bkz. Şekil 1). Kod, girilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı ve parola çiftleri (Scott/Password, Jisun/Password ve Sam/Password) listesiyle karşılaştırarak doğrular. <a id="Tutorial03"></a> [*Forms kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) öğreticisinde, form kimlik doğrulama biletinin özelliğindeki ek bilgileri depolamak için oturum açma sayfasının kodunu güncelleştirdik `UserData` .

[![Oturum açma sayfasının arabirimi Iki metin kutuları, bir CheckBoxList ve bir düğme Içerir](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**Şekil 1**: oturum açma sayfasının arabirimi Iki metin kutuları, bir CheckBoxList ve bir düğme içerir ([tam boyutlu görüntüyü görüntülemek için tıklatın](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png))

Oturum açma sayfasının Kullanıcı arabirimi değişmeden kalabilir, ancak oturum açma düğmesinin `Click` olay işleyicisini, kullanıcıyı üyelik çerçevesi Kullanıcı deposuna göre doğrulayan kodla değiştirmemiz gerekiyor. Olay işleyicisini kodun aşağıdaki gibi görünmesi için güncelleştirin:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

Bu kod daha basit bir işlemdir. `Membership.ValidateUser`Yöntemi çağırarak, sağlanan kullanıcı adını ve parolayı geçirerek başladık. Bu yöntem true değerini döndürürse, Kullanıcı, `FormsAuthentication` sınıfın RedirectFromLoginPage yöntemi aracılığıyla sitede oturum açmış olur. <a id="Tutorial2"></a>( [*Forms kimlik doğrulama öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) , `FormsAuthentication.RedirectFromLoginPage` Forms kimlik doğrulama bileti oluşturur ve ardından kullanıcıyı uygun sayfaya yönlendirir.) Kimlik bilgileri geçersiz ise, `InvalidCredentialsMessage` kullanıcıya Kullanıcı adının veya parolasının yanlış olduğunu bildiren etiket görüntülenir.

İşte bu kadar!

Oturum açma sayfasının beklendiği gibi çalışıp çalışmadığını sınamak için, önceki öğreticide oluşturduğunuz kullanıcı hesaplarından biriyle oturum açmayı deneyin. Ya da henüz bir hesap oluşturmadıysanız sayfadan bir tane oluşturun `~/Membership/CreatingUserAccounts.aspx` .

> [!NOTE]
> Kullanıcı kimlik bilgilerini girdiğinde ve oturum açma sayfası formunu gönderdiğinde, parola da dahil olmak üzere kimlik bilgileri Internet üzerinden *düz metin*olarak iletilir. Bu, tüm korsanlarının ağ trafiğinin Kullanıcı adını ve parolayı göremeyeceğini gösterir. Bunu engellemek için [Güvenli Yuva katmanları (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)kullanarak ağ trafiğini şifrelemek gereklidir. Bu, kimlik bilgilerinin (Ayrıca tüm sayfanın HTML işaretlemesi) Web sunucusu tarafından alınana kadar tarayıcıdan ayrıldıklarından emin olur.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Üyelik çerçevesi geçersiz oturum açma girişimlerini nasıl Işler?

Bir ziyaretçi oturum açma sayfasına ulaştığında ve kimlik bilgilerini gönderdiğinde, tarayıcıları oturum açma sayfasına bir HTTP isteği oluşturur. Kimlik bilgileri geçerliyse, HTTP yanıtı bir tanımlama bilgisinde kimlik doğrulama biletini içerir. Bu nedenle, sitenize kesintiye uğramaya çalışan bir korsan, oturum açma sayfasına geçerli bir Kullanıcı adı ve parola tahminiyle, her zaman çalışan bir program oluşturabilir. Parola tahmini doğruysa, oturum açma sayfası, kimlik doğrulama anahtarı tanımlama bilgisini döndürür. bu noktada, programın geçerli bir Kullanıcı adı/parola çiftinin üzerinde olduğunu bildiğinde haberdar olur. Bu tür bir program, deneme yanılma aracılığıyla bir kullanıcının parolasıyla, özellikle de parolanın zayıfına göre anlaşılabilir.

Bu tür deneme yanılma saldırılarını engellemek için, belirli bir süre içinde belirli sayıda başarısız oturum açma girişimi varsa üyelik çerçevesi bir kullanıcıyı kilitler. Tam parametreler aşağıdaki iki üyelik sağlayıcısı yapılandırma ayarları aracılığıyla yapılandırılabilir:

- `maxInvalidPasswordAttempts` -hesap kilitlenmeden önceki süre içinde Kullanıcı için kaç geçersiz parola denemesine izin verileceğini belirtir. Varsayılan değer 5 ' tir.
- `passwordAttemptWindow` -belirtilen geçersiz oturum açma girişimi sayısının, hesabın kilitlenmesine neden olacağı dakika cinsinden süreyi belirtir. Varsayılan değer 10 ' dur.

Bir Kullanıcı kilitlendiyse, yönetici hesabının kilidini açana kadar oturum açamaz. Bir Kullanıcı kilitlendiğinde, `ValidateUser` *always* `false` geçerli kimlik bilgileri sağlanmış olsa bile Yöntem her zaman döndürülür. Bu davranış, bir korsanın, deneme yanılma yöntemleri aracılığıyla sitenize bölünmesinin olasılığını azaltır, ancak parolasını unutduktan veya yanlışlıkla Caps Lock 'ta veya hatalı yazma gününe sahip olan geçerli bir kullanıcının kilitlenmesini sonlandırabilir.

Ne yazık ki, bir kullanıcı hesabının kilidini açmak için yerleşik bir araç yoktur. Bir hesabın kilidini açmak için, veritabanını doğrudan değiştirebilir ve `IsLockedOut` `aspnet_Membership` ilgili Kullanıcı hesabı için tablodaki alanı değiştirebilir veya kilidi açma seçeneklerini içeren kilitli hesapları listeleyen bir Web tabanlı arabirim oluşturabilirsiniz. Gelecekteki bir öğreticide, ortak kullanıcı hesabı ve rolle ilgili görevleri yerine getirmeye yönelik yönetim arabirimleri oluşturmayı inceleyeceğiz.

> [!NOTE]
> Metodun bir alt tarafı, `ValidateUser` sağlanan kimlik bilgileri geçersiz olduğunda, neden bir açıklama sağlamaz. Kullanıcı deposunda eşleşen bir Kullanıcı adı/parola çifti olmadığından veya Kullanıcı henüz onaylanmadığından veya Kullanıcı kilitlenmiş olduğundan kimlik bilgileri geçersiz olabilir. Adım 4 ' te, oturum açma girişimi başarısız olduğunda kullanıcıya daha ayrıntılı bir ileti göstermeyi öğreneceğiz.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>2. Adım: oturum açma Web denetimi aracılığıyla kimlik bilgileri toplama

[Oturum açma Web denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) , <a id="SKM5"></a> [*form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) konusunda daha sonra oluşturduğumuz bir varsayılan kullanıcı arabirimini çok benzer şekilde işler. Oturum açma denetiminin kullanılması, ziyaretçi kimlik bilgilerini toplamak için arabirim oluşturmak üzere sahip olma zorunluluğunu kaydeder. Üstelik, oturum açma denetimi kullanıcı oturumunu otomatik olarak imzalar (gönderilen kimlik bilgilerinin geçerli olduğu varsayıldığında) ve bu sayede herhangi bir kod yazmak zorunda kalmaktan tasarruf edin.

`Login.aspx`El ile oluşturulan arabirimi ve kodu bir oturum açma denetimiyle değiştirerek güncellim. ' De varolan biçimlendirmeyi ve kodu kaldırarak başlayın `Login.aspx` . Doğru bir şekilde silebilirsiniz ya da yalnızca bir açıklama olarak görebilirsiniz. Bildirim temelli biçimlendirmeyi açıklama olarak eklemek için `<%--` ve `--%>` sınırlayıcılarıyla çevreleyin. Bu sınırlayıcıları el ile girebilir veya şekil 2 ' de gösterildiği gibi, açıklama eklemek için metni seçip araç çubuğunda Seçili çizgiler simgesine tıklayabilirsiniz. Benzer şekilde, arka plan kod sınıfında seçili kodu açıklama olarak eklemek için seçili çizgiler simgesini açıklama olarak kullanabilirsiniz.

[![Login. aspx dosyasındaki mevcut bildirime dayalı biçimlendirmeyi ve kaynak kodu açıklama](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**Şekil 2**: Içindeki mevcut bildirime dayalı biçimlendirmeyi ve kaynak kodu açıklama `Login.aspx` ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png))

> [!NOTE]
> Visual Studio 2005 ' de bildirim temelli biçimlendirme görüntülenirken Seçili satırlar simgesinin açıklaması kullanılamaz. Visual Studio 2008 kullanmıyorsanız, `<%--` ve sınırlayıcılarını el ile eklemeniz gerekir `--%>` .

Sonra, bir oturum açma denetimini sayfada bulunan araç kutusundan sürükleyin ve `ID` özelliğini olarak ayarlayın `myLogin` . Bu noktada, ekranınızda şekil 3 ' e benzer görünmelidir. Oturum açma denetiminin varsayılan arabiriminin Kullanıcı adı ve parola, bir sonraki zaman beni anımsa onay kutusu ve oturum açma düğmesi için TextBox denetimleri içerdiğini unutmayın. Ayrıca `RequiredFieldValidator` Iki metin kutuları için denetimler de vardır.

[![Sayfaya bir oturum açma denetimi ekleyin](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**Şekil 3**: sayfaya bir oturum açma denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png))

Tebrikler! Oturum açma denetiminin oturum açma düğmesine tıklandığında, bir geri gönderme gerçekleşir ve oturum açma denetimi `Membership.ValidateUser` yöntemi, girilen Kullanıcı adı ve parolayı geçirerek çağırır. Kimlik bilgileri geçersizse, oturum açma denetimi şöyle bir ileti görüntüler. Ancak, kimlik bilgileri geçerliyse, oturum açma denetimi Forms kimlik doğrulama bileti oluşturur ve kullanıcıyı uygun sayfaya yönlendirir.

Oturum açma denetimi, kullanıcıyı başarılı bir oturum açma üzerine yönlendiren uygun sayfayı belirlemekte kullanılacak dört faktörü kullanır:

- Oturum açma denetiminin, form kimlik doğrulama yapılandırmasında ayarıyla tanımlanan oturum açma sayfasında olup olmadığı `loginUrl` . bu ayarın varsayılan değeri `Login.aspx`
- `ReturnUrl`QueryString parametresinin varlığı
- Oturum açma denetiminin [ `DestinationUrl` özelliğinin](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) değeri
- `defaultUrl`Forms kimlik doğrulaması yapılandırma ayarlarında belirtilen değer; bu ayarın varsayılan değeri`Default.aspx`

Şekil 4 ' te, oturum açma denetiminin ilgili sayfa kararına ulaşmak için bu dört parametreyi nasıl kullandığı gösterilmektedir.

[![Sayfaya bir oturum açma denetimi ekleyin](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**Şekil 4**: sayfaya bir oturum açma denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png))

Bir tarayıcı aracılığıyla siteyi ziyaret ederek ve üyelik çerçevesinde var olan bir kullanıcı olarak oturum açarak, oturum açma denetimini test etmek için bir dakikanızı ayırın.

Oturum açma denetiminin işlenmiş arabirimi yüksek oranda yapılandırılabilir. Görünümünü etkileyen bazı özellikler vardır; Artık, oturum açma denetimi, Kullanıcı arabirimi öğelerinin düzeni üzerinde kesin denetim için bir şablona dönüştürülebilir. Bu adımın geri kalanında görünümün ve düzenin nasıl özelleştirileceği incelenir.

### <a name="customizing-the-login-controls-appearance"></a>Oturum açma denetiminin görünümünü özelleştirme

Oturum açma denetiminin varsayılan özellik ayarları, Kullanıcı arabirimini bir başlık (oturum açma), TextBox ve etiket denetimleri Kullanıcı adı ve parola girişleri, bir sonraki zaman anımsa onay kutusu ve oturum açma düğmesi ile birlikte işler. Bu öğelerin görünümleri, oturum açma denetiminin çok sayıda özelliği aracılığıyla yapılandırılabilir. Ayrıca, Yeni Kullanıcı hesabı oluşturmak için bir sayfanın bağlantısı gibi ek kullanıcı arabirimi öğeleri, bir özellik veya ikisi ayarlanarak eklenebilir.

Oturum açma denetimizin görünümünü en az bir dakika sonra harcayalım. `Login.aspx`Sayfanın üst kısmında, oturum açma belirten bir metin zaten olduğundan, oturum açma denetiminin başlığı gereksiz. Bu nedenle, oturum açma denetiminin başlığını kaldırmak için [ `TitleText` özellik](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) değerini temizleyin.

Kullanıcı adı: ve parola: iki metin kutusu denetiminin solundaki Etiketler [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) sırasıyla ve [ `PasswordLabelText` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)aracılığıyla özelleştirilebilir. Kullanıcı adını değiştirelim: etiketle Kullanıcı adı:. Etiket ve metin kutusu stilleri [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) sırasıyla ve [ `TextBoxStyle` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)aracılığıyla yapılandırılabilir.

Beni anımsa bir sonraki zaman onay kutusunun metin özelliği oturum açma denetimi tarafından ayarlanabilir [`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx) ve varsayılan olarak denetlenen durumu (varsayılan olarak false ' dur) ile yapılandırılabilir [`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) . `RememberMeSet`Şimdi beni anımsa onay kutusunun varsayılan olarak denetleneceğini sağlamak için özelliği doğru olarak ayarlayın.

Oturum açma denetimi, Kullanıcı arabirimi denetimlerinin yerleşimini ayarlamak için iki özellik sunar. , [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) Kullanıcı adı: ve Password: etiketlerin Ilgili metin kutularının solunda (varsayılan) veya üstünde görünür olup olmadığını gösterir. , [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) Kullanıcı adı ve parola girişlerinin dikey mi (diğeri üzerinde) yoksa yatay mi olduğunu gösterir. Bu iki özelliği varsayılan ayarlarına ayarlıyorum, ancak sonuçta ortaya çıkan etkiyi görmek için bu iki özelliği varsayılan olmayan değerlerine ayarlamayı deneyin.

> [!NOTE]
> Sonraki bölümde, oturum açma denetiminin yerleşimini yapılandırırken, düzen denetiminin Kullanıcı arabirimi öğelerinin kesin yerleşimini tanımlamak için şablonları kullanma bölümüne bakacağız.

[`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx)Ve [ `CreateUserUrl` özelliklerini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) henüz kaydedilmemiş olarak ayarlayıp, oturum açma denetiminin özellik ayarlarını kaydırın. Hesap oluşturun! ve `~/Membership/CreatingUserAccounts.aspx` sırasıyla. Bu, <a id="SKM6"></a> [önceki öğreticide](creating-user-accounts-cs.md)oluşturduğumuz sayfaya Işaret eden, oturum açma denetiminin arabirimine bir köprü ekler. Oturum açma denetimi [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) ve [ `HelpPageUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) ve [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) [ `PasswordRecoveryUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) aynı şekilde çalışarak, bağlantıları bir yardım sayfası ve parola kurtarma sayfası ile işleme.

Bu özellik değiştirildikten sonra, oturum açma denetiminizin bildirim temelli biçimlendirme ve görünüşü Şekil 5 ' te gösterilenle benzer şekilde görünmelidir.

[![Oturum açma denetiminin özelliklerinin değerleri görünümü dikte](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**Şekil 5**: oturum açma denetiminin özelliklerinin değerleri görünümü dikte ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png))

### <a name="configuring-the-login-controls-layout"></a>Oturum açma denetiminin yerleşimini yapılandırma

Oturum açma Web denetiminin varsayılan kullanıcı arabirimi, arabirimi bir HTML içinde yerleştirir `<table>` . Ancak işlenmiş çıktı üzerinde daha ayrıntılı denetime ihtiyacım varsa ne olacak? Belki de `<table>` etiketini bir dizi etiketle değiştirmek istiyoruz `<div>` . Veya uygulamamız kimlik doğrulaması için ek kimlik bilgileri gerektiriyorsa ne olacak? Örneğin, çok sayıda Finans Web sitesi, kullanıcıların yalnızca bir Kullanıcı adı ve parola sağlamalarına, ayrıca bir kişisel kimlik numarası (PIN) veya diğer tanımlama bilgilerine sahip olmasını gerektirir. Nedenler ne olursa olsun, oturum açma denetimini bir şablona dönüştürmek mümkündür ve bu, arabirimin bildirim temelli işaretlemesini açıkça tanımlayabiliriz.

Oturum açma denetimini ek kimlik bilgileri toplayacak şekilde güncelleştirmek için iki şey yapmanız gerekir:

1. Ek kimlik bilgilerini toplamak için, oturum açma denetiminin arabirimini Web denetimleri içerecek şekilde güncelleştirin.
2. Kullanıcının Kullanıcı adı ve parolası geçerliyse ve bunların ek kimlik bilgileri geçerli olduğunda kimlik doğrulaması yapmak için oturum açma denetiminin iç kimlik doğrulama mantığını geçersiz kılın.

İlk görevi gerçekleştirmek için, oturum açma denetimini bir şablona dönüştürmemiz ve gerekli Web denetimlerini eklemesi gerekir. İkinci görevde olduğu gibi, Denetim [ `Authenticate` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)için bir olay Işleyicisi oluşturularak, oturum açma denetiminin kimlik doğrulama mantığının yerini alabilirsiniz.

Oturum açma denetimini, Kullanıcı adı, parola ve e-posta adresi için sorar ve yalnızca belirtilen e-posta adresi dosyadaki e-posta adresiyle eşleşiyorsa kullanıcının kimliğini doğrular. Önce, oturum açma denetiminin arabirimini bir şablona dönüştürmeniz gerekir. Oturum açma denetiminin akıllı etiketinden şablona Dönüştür seçeneğini belirleyin.

[![Oturum açma denetimini bir şablona Dönüştür](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**Şekil 6**: oturum açma denetimini bir şablona Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png))

> [!NOTE]
> Oturum açma denetimini şablon öncesi sürümüne geri döndürmek için denetimin akıllı etiketindeki Sıfırla bağlantısına tıklayın.

Oturum açma denetimini bir şablona dönüştürmek, `LayoutTemplate` denetimin bildirim temelli IŞARETLEMESINI HTML öğeleriyle ve Kullanıcı arabirimini tanımlayan Web denetimleriyle bir ekler. Şekil 7 ' de gösterildiği gibi, denetimi bir şablona dönüştürmek, bir `TitleText` `CreateUserUrl` şablon kullanılırken bu özellik değerleri dikkate alındıklarından, ve gibi Özellikler penceresi birçok özelliği kaldırır.

[![Oturum açma denetimi bir şablona dönüştürüldüğünde daha az özellik mevcuttur](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**Şekil 7**: oturum açma denetimi bir şablona dönüştürüldüğünde daha az özellik kullanılabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png))

İçindeki HTML işaretlemesi `LayoutTemplate` gerektiği şekilde değiştirilebilir. Benzer şekilde, şablona yeni Web denetimleri eklemeyi de ücretsiz olarak hissetmekten çekinmeyin. Ancak, oturum açma denetiminin çekirdek Web denetimlerinin şablonda kalması ve atanan değerlerinin tutulması önemlidir `ID` . Özellikle, `UserName` veya `Password` metin kutuları, `RememberMe` onay kutusu, `LoginButton` düğme, `FailureText` etiket veya `RequiredFieldValidator` denetimleri kaldırmayın veya yeniden adlandırmayın.

Ziyaretçi e-posta adresini toplamak için, şablona bir metin kutusu eklememiz gerekiyor. `<tr>`Metin kutusunu içeren tablo satırı () `Password` ve bir sonraki beni anımsa onay kutusunun bulunduğu tablo satırı arasına aşağıdaki bildirim temelli biçimlendirmeyi ekleyin:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

`Email`Metin kutusunu ekledikten sonra tarayıcı aracılığıyla sayfayı ziyaret edin. Şekil 8 ' de gösterildiği gibi, oturum açma denetiminin Kullanıcı arabirimi artık üçüncü bir TextBox içerir.

[![Oturum açma denetimi artık kullanıcının e-posta adresi için bir metin kutusu Içeriyor](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**Şekil 8**: oturum açma denetimi artık kullanıcının e-posta adresi Için bir metin kutusu içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png))

Bu noktada, oturum açma denetimi, `Membership.ValidateUser` sağlanan kimlik bilgilerini doğrulamak için yöntemini kullanmaya devam eder. Karşılık `Email` gelen metin kutusuna girilen değerin, kullanıcının oturum açabilip oturum açıp kullanamayacağını yok. 3. adımda, kimlik bilgilerinin yalnızca Kullanıcı adı ve parola geçerli olduğunda ve sağlanan e-posta adresi dosyadaki e-posta adresiyle eşleşiyorsa, kimlik bilgilerinin geçerli kabul edilmesi için oturum açma denetiminin kimlik doğrulama mantığını geçersiz kılma bölümüne bakacağız.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3. Adım: oturum açma denetiminin kimlik doğrulama mantığını değiştirme

Bir ziyaretçi kimlik bilgilerini ne zaman sağlar ve oturum aç düğmesine tıkladığında, bir geri gönderme ve oturum açma denetimi kimlik doğrulama iş akışı üzerinden ilerler. İş akışı, [ `LoggingIn` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)yükselterek başlar. Bu olayla ilişkili herhangi bir olay işleyicisi özelliği olarak ayarlanarak oturum açma işlemini iptal edebilir `e.Cancel` `true` .

Oturum açma işlemi iptal edilmediğinden, iş akışı, [ `Authenticate` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)yükselterek ilerler. Olay için bir olay işleyici varsa `Authenticate` , sağlanan kimlik bilgilerinin geçerli olup olmadığını belirlemekten sorumludur. Hiçbir olay işleyicisi belirtilmemişse, oturum açma denetimi `Membership.ValidateUser` kimlik bilgilerinin geçerliliğini belirlemede yöntemini kullanır.

Sağlanan kimlik bilgileri geçerliyse, Forms kimlik doğrulama bileti oluşturulur, [ `LoggedIn` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) tetiklenir ve Kullanıcı uygun sayfaya yönlendirilir. Ancak, kimlik bilgileri geçersiz kabul edildiği takdirde [ `LoginError` olay](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) tetiklenir ve kullanıcıya kimlik bilgilerinin geçersiz olduğunu bildiren bir ileti görüntülenir. Varsayılan olarak, hata durumunda oturum açma denetimi, `FailureText` etiket denetiminin Text özelliğini bir hata iletisine ayarlar (oturum açma denemeniz başarılı olmadı. Lütfen yeniden deneyin). Ancak, oturum açma denetiminin [ `FailureAction` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) olarak ayarlandıysa `RedirectToLoginPage` , oturum açma denetimi bir oturum açma `Response.Redirect` sayfasında QueryString parametresini `loginfailure=1` (oturum açma denetiminin hata iletisini görüntülemesine neden olur) bir öğesine yayınlar.

Şekil 9, kimlik doğrulama iş akışının Akış grafiğini sunar.

[![Oturum açma denetiminin kimlik doğrulama Iş akışı](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**Şekil 9**: oturum açma denetiminin kimlik doğrulama iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png))

> [!NOTE]
> Sayfa seçeneğini ne zaman kullanacağınızı merak ediyorsanız `FailureAction` `RedirectToLogin` , aşağıdaki senaryoyu göz önünde bulundurun. Şu `Site.master` anda ana sayfamızda, anonim bir kullanıcı tarafından ziyaret edildiğinde sol sütunda görüntülenen, Hello, Stranger metni bulunur, ancak bu metni bir oturum açma denetimiyle değiştirmek istediğimizi düşünün. Bu, anonim bir kullanıcının oturum açma sayfasını doğrudan ziyaret etmesini gerektirmek yerine sitedeki herhangi bir sayfadan oturum açmasına olanak tanır. Ancak, bir Kullanıcı Ana sayfa tarafından işlenen oturum açma denetimi aracılığıyla oturum açmıyorsa, `Login.aspx` Bu sayfada büyük olasılıkla ek yönergeler, bağlantılar ve yeni bir hesap oluşturmak veya kayıp bir parola almak için ana sayfaya eklenmemiş bağlantılar gibi diğer yardım bilgileri de dahil olmak üzere, bunları oturum açma sayfasına () yönlendirmek mantıklı olabilir.

### <a name="creating-theauthenticateevent-handler"></a>`Authenticate`Olay işleyicisi oluşturma

Özel kimlik doğrulama mantığımızı bağlamak için, oturum açma denetiminin olayı için bir olay işleyicisi oluşturmamız gerekir `Authenticate` . Olay için olay işleyicisi oluşturmak `Authenticate` aşağıdaki olay işleyici tanımını oluşturur:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

Görebileceğiniz gibi, `Authenticate` olay işleyicisine [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) ikinci giriş parametresi olarak türünde bir nesne geçirilir. `AuthenticateEventArgs`Sınıfı, `Authenticated` sağlanan kimlik bilgilerinin geçerli olup olmadığını belirtmek için kullanılan adlı bir Boole özelliği içerir. Bundan sonra, sağlanan kimlik bilgilerinin geçerli olup olmadığını ve özelliği uygun şekilde ayarlamayı belirleyen kodu buraya yazalım `e.Authenticate` .

### <a name="determining-and-validating-the-supplied-credentials"></a>Sağlanan kimlik bilgilerini belirleme ve doğrulama

[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx)Kullanıcı tarafından girilen Kullanıcı adı ve parola kimlik bilgilerini öğrenmek Için oturum açma denetiminin ve [ `Password` özelliklerini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) kullanın. Ek Web denetimlerine ( `Email` önceki adımda eklediğimiz metin kutusu gibi) girilen değerleri belirleyebilmek için, *`LoginControlID`* `.FindControl` *`controlID`* özelliği eşit olan şablonda Web denetimine programlı bir başvuru almak için ("") kullanın `ID` *`controlID`* . Örneğin, metin kutusuna bir başvuru almak için `Email` aşağıdaki kodu kullanın:

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

Kullanıcının kimlik bilgilerini doğrulamak için iki şey olması gerekir:

1. Belirtilen kullanıcı adının ve parolanın geçerli olduğundan emin olun
2. Girilen e-posta adresinin, oturum açmaya çalışan kullanıcının dosyadaki e-posta adresiyle eşleştiğinden emin olun

İlk denetimi gerçekleştirmek için, `Membership.ValidateUser` 1. adımda gördüğdiğimiz yöntemi tek bir şekilde kullanabiliriz. İkinci denetim için kullanıcının e-posta adresini belirlememiz gerekir, böylece metin kutusu denetimine girdiğiniz e-posta adresiyle karşılaştırılmaktadır. Belirli bir kullanıcı hakkında bilgi almak için `Membership` sınıfın [ `GetUser` yöntemini](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)kullanın.

`GetUser`Yönteminde çok sayıda aşırı yükleme vardır. Herhangi bir parametreye geçirilmeden kullanılırsa, o anda oturum açmış olan kullanıcı hakkında bilgi döndürür. Belirli bir kullanıcı hakkında bilgi almak için, `GetUser` Kullanıcı adında geçiş yapın. Her iki durumda da,,,, vb `GetUser` . gibi özelliklere sahip bir [ `MembershipUser` nesnesi](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)döndürür `UserName` `Email` `IsApproved` `IsOnline` .

Aşağıdaki kod bu iki denetimi uygular. Her iki geçiş de olarak `e.Authenticate` ayarlanırsa `true` , aksi takdirde atanır `false` .

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

Bu kod yerine, doğru Kullanıcı adını, parolayı ve e-posta adresini girerek geçerli bir kullanıcı olarak oturum açmaya çalışın. Yeniden deneyin, ancak bu zaman, bu kez doğru bir e-posta adresi kullanır (bkz. Şekil 10). Son olarak, var olmayan bir Kullanıcı adı kullanarak bunu üçüncü kez deneyin. İlk durumda, sitede başarıyla oturum açmanız gerekir, ancak son iki durumda oturum açma denetiminin geçersiz kimlik bilgileri iletisini görmeniz gerekir.

[![Yanlış bir e-posta adresi sağlarken Tito oturum açılamıyor](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**Şekil 10**: Hatalı bir e-posta adresi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)) sağlanırken oturum açılamıyor

> [!NOTE]
> Üyelik çerçevesinin adım 1 ' de geçersiz oturum açma girişimlerini nasıl Işleyeceği konusunda anlatıldığı gibi, `Membership.ValidateUser` Yöntem çağrıldığında ve geçersiz kimlik bilgileri geçirildiğinde, geçersiz oturum açma girişimini izler ve belirtilen zaman penceresinde belirli bir eşik eşiğini aşarsa kullanıcıyı kilitler. Özel kimlik doğrulama mantığımız yöntemi çağırdığı `ValidateUser` için geçerli bir Kullanıcı adı için hatalı bir parola geçersiz oturum açma denemesi sayacını artırır, ancak Kullanıcı adı ve parolanın geçerli olduğu, ancak e-posta adresinin yanlış olması durumunda bu sayaç artmaz. Bu davranış, bir korsanın Kullanıcı adı ve parolayı bilmesi, ancak kullanıcının e-posta adresini belirlemesi için deneme yanılma tekniklerini kullanması gereken bir olasılıktır.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4. Adım: oturum açma denetiminin geçersiz kimlik bilgileri Iletisini geliştirme

Kullanıcı geçersiz kimlik bilgileriyle oturum açmaya çalıştığında, oturum açma denetimi, oturum açma girişiminin başarısız olduğunu belirten bir ileti görüntüler. Özellikle denetim, kendi [ `FailureText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)tarafından belirtilen iletiyi görüntüler, bu, oturum açma girişiminizin varsayılan bir değeri olan başarılı olmadı. Lütfen tekrar deneyin.

Kullanıcının kimlik bilgilerinin geçersiz olmasının birçok nedeni olduğunu unutmayın:

- Kullanıcı adı mevcut olmayabilir
- Kullanıcı adı var, ancak parola geçersiz
- Kullanıcı adı ve parola geçerli, ancak kullanıcı henüz onaylanmamış
- Kullanıcı adı ve parola geçerli, ancak kullanıcı kilitli (büyük olasılıkla belirtilen zaman çerçevesinde geçersiz oturum açma girişimi sayısını aştıkları için)

Ve özel kimlik doğrulama mantığı kullanılırken başka nedenler de olabilir. Örneğin, adım 3 ' te yazdığımız kodla, Kullanıcı adı ve parola geçerli olabilir, ancak e-posta adresi hatalı olabilir.

Kimlik bilgilerinin neden geçersiz olmasından bağımsız olarak, oturum açma denetimi aynı hata iletisini görüntüler. Bu geri bildirim olmaması, hesabı henüz onaylanmamış veya kilitlenen bir kullanıcı için kafa karıştırıcı olabilir. Çok az iş sayesinde, oturum açma denetiminin daha uygun bir ileti görüntülemesini de sağlayabilirsiniz.

Kullanıcı geçersiz kimlik bilgileriyle oturum açmaya çalıştığında, oturum açma denetimi `LoginError` olayını başlatır. Devam edin ve bu olay için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

Yukarıdaki kod, oturum açma denetiminin `FailureText` özelliğini varsayılan değere ayarlayarak başlar (oturum açma denemeniz başarılı olmadı. Lütfen yeniden deneyin). Daha sonra sağlanan kullanıcı adının mevcut bir kullanıcı hesabına eşlendiğini kontrol eder. Bu durumda, `MembershipUser` `IsLockedOut` `IsApproved` hesabın kilitlenip kilitlenmediğini veya henüz onaylanmadığını belirleme, sonuçta elde edilen nesnenin ve özelliklerinin yaptığı bir yol açar. Her iki durumda da, `FailureText` Özelliği karşılık gelen bir değere güncelleştirilir.

Bu kodu test etmek için,, mevcut bir kullanıcı olarak oturum açmaya çalışır, ancak yanlış bir parola kullanın. 10 dakikalık bir zaman çerçevesinde bu beş kez bir satırda bunu yapın ve hesap kilitlenir. Şekil 11 ' de gösterildiği gibi, sonraki oturum açma girişimleri her zaman başarısız olur (doğru parolayla bile), ancak artık çok fazla geçersiz oturum açma denemesi nedeniyle hesabınız daha açıklayıcı bir şekilde görüntülenir. Hesabınızın kilidi açık olması için lütfen yöneticiye başvurun.

[![Tito geçersiz oturum açma denemesi gerçekleştirdi ve kilitlendi](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**Şekil 11**: Tito geçersiz oturum açma girişimi gerçekleştirdi ve kilitlendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png))

## <a name="summary"></a>Özet

Bu öğreticide, oturum açma sayfamız belirtilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı/parola çiftleri listesine göre doğruladı. Bu öğreticide, üyelik çerçevesinde kimlik bilgilerini doğrulamak için sayfayı güncelleştirdik. Adım 1 ' de yöntemi programlı olarak kullanma hakkında baktık `Membership.ValidateUser` . 2. adımda, el ile oluşturulan kullanıcı arabirimimizi ve kodumuzu oturum açma denetimiyle değiştirdik.

Oturum açma denetimi standart bir oturum açma kullanıcı arabirimini işler ve Kullanıcı kimlik bilgilerini üyelik çerçevesine göre otomatik olarak doğrular. Ayrıca, geçerli kimlik bilgileri durumunda oturum açma denetimi, Kullanıcı tarafından form kimlik doğrulaması aracılığıyla oturum açar. Kısacası, tam işlevli bir oturum açma kullanıcı deneyimi yalnızca oturum açma denetimini bir sayfaya sürükleyerek, ek bildirime dayalı biçimlendirme veya kod gerekli olmadan kullanılabilir. Artık, oturum açma denetimi, hem işlenmiş Kullanıcı arabirimi hem de kimlik doğrulama mantığı üzerinde ince bir denetim sağlayan yüksek düzeyde özelleştirilebilir.

Bu noktada, Web sitemizden ziyaretçi yeni bir kullanıcı hesabı oluşturabilir ve sitede oturum açabilir, ancak kimliği doğrulanmış kullanıcıya göre sayfaların erişimini kısıtlama konusunda bakmamız gerekir. Şu anda, tüm kullanıcılar, kimliği doğrulanmış veya anonim, sitemizdeki herhangi bir sayfayı görüntüleyebilir. Sitemizdeki sayfalara erişimi denetim altına alarak, işlevselliği kullanıcıya bağlı olan belirli sayfaları da olabilir. Sonraki öğreticide, oturum açmış kullanıcıya göre erişimin ve sayfa içi işlevlerin nasıl sınırlandırılır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kilitli ve onaylanmamış kullanıcılara özel Iletiler görüntüleme](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Nasıl yapılır: ASP.NET oturum açma sayfası oluşturma](https://msdn.microsoft.com/library/ms178331.aspx)
- [Oturum açma denetimi teknik belgeleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Oturum açma denetimlerini kullanma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott, [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) konumundaki blogundan veya üzerinden erişilebilir [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Michael Kayvero. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, bana bir satır bırakın [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [Önceki](creating-user-accounts-cs.md) 
>  [Sonraki](user-based-authorization-cs.md)
