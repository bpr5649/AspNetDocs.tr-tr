---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: Giriş ASP.NET Identity - ASP.NET 4.x
author: jongalloway
description: ASP.NET üyelik sistemini şekilde web uygulamaları typicall içinde birçok değişiklik yapıldı sonra ile ASP.NET 2.0 arka 2005 ve bu yana sunulmuştur...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 34a0d62d7afcaffa8fbac0bc774d9266efb6b165
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59413054"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity’ye Giriş


> Web uygulamaları genellikle kimlik doğrulaması ve yetkilendirme işleyecek şekilde birçok değişiklik yapıldı sonra ASP.NET üyelik sistemini ile ASP.NET 2.0 arka 2005'te ve sonrasında kullanıma sunulmuştur. ASP.NET, web, telefon veya tablet için modern uygulamalar oluştururken, üyelik sistemi olması gerekir, yeni bir görünüme kimliğidir.


## <a name="background-membership-in-aspnet"></a>Arka planı: ASP.NET üyelik

### <a name="aspnet-membership"></a>ASP.NET Üyeliği

[ASP.NET üyelik](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) form kimlik doğrulaması ve kullanıcı adları, parolalar ve profil verileri için bir SQL Server veritabanı 2005 ' te genel site üyeliği gereksinimlerini çözmek için tasarlanmıştır. Bugün bir çok daha geniş dizi web uygulamaları için veri depolama seçeneği yoktur ve çoğu geliştirici, sosyal kimlik sağlayıcıları için kimlik doğrulama ve yetkilendirme işlevselliği kullanmak sitelerini etkinleştirmek istiyor. Bu geçiş zorlaştıran ASP.NET üyelik'ın tasarım sınırlamaları:

- Veritabanı şemasını SQL Server için tasarlanmıştır ve bunu değiştiremezsiniz. Profil bilgilerini ekleyebilirsiniz, ancak ek veri erişimi dışında herhangi bir araçla profili sağlayıcısı API aracılığıyla zorlaştırır farklı bir tablo paketlenmiştir.
- Sağlayıcı sistemini yedekleme veri deposu değiştirmenize olanak tanır, ancak sistem varsayımlar ilişkisel bir veritabanı için uygun geçici olarak tasarlanmıştır. Azure depolama tabloları gibi bir ilişkisel olmayan depolama mekanizması üyelik bilgilerini depolamak için bir sağlayıcı yazabilirsiniz, ancak ilişkisel tasarım kadar kod ve çok sayıda yazarak çalışmak zorunda ardından `System.NotImplementedException` olmayan yöntemler için özel durumlar NoSQL veritabanları için geçerlidir.
- Form kimlik doğrulamasını log-günlük-çıkış işlevselliğini dayalı olduğundan, üyelik sistemini kullanamazsınız [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md). OWIN ara yazılımı bileşenleri (Microsoft Accounts, Facebook, Google, Twitter gibi) Dış kimlik sağlayıcısı kullanarak oturum açma desteği de dahil olmak üzere kimlik doğrulaması içerir ve oturum açma Kurumsal hesaplarını kullanarak şirket içi Active Directory veya Azure Active Directory. OWIN OAuth 2.0 JWT ve CORS desteği de içerir.

### <a name="aspnet-simple-membership"></a>ASP.NET basit üyelik

[Basit üyelik ASP.NET](../../../web-pages/overview/security/16-adding-security-and-membership.md) ASP.NET Web sayfaları için bir üyelik sistemi geliştirilmiştir. WebMatrix ve Visual Studio 2010 SP1 ile serbest bırakıldı. Basit üyelik amacı, üyelik işlevselliğini bir Web sayfalarını uygulamasına eklemek kolay hale getirmek için oluştu.

Basit üyelik daha kolay kullanıcı profili bilgilerini özelleştirmek yaptı, ancak yine de bir ASP.NET üyelik sorun paylaşır ve bazı sınırlamalara sahiptir:

- İlişkisel olmayan depolama üyelik sistemi verileri kalıcı hale getirmek zordu.
- OWIN ile kullanamazsınız.
- Mevcut ASP.NET üyelik sağlayıcıları ile iyi çalışmaz ve Genişletilebilir değildir.

### <a name="aspnet-universal-providers"></a>ASP.NET Evrensel Sağlayıcılar

[ASP.NET Evrensel sağlayıcıları](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) Microsoft Azure SQL veritabanı ve ayrıca çalışma SQL Server Compact ile üyelik bilgilerini kalıcı hale getirmek mümkün hale getirmek için geliştirilmiştir. Evrensel sağlayıcıları, Entity Framework Code Evrensel sağlayıcıları EF tarafından desteklenen herhangi bir deposundaki verileri kalıcı hale getirmek için kullanılabilir yani First üzerinde oluşturulmuştur. Evrensel sağlayıcıları ile veritabanı şeması tam anlamıyla bir çok temizlendi.

Bunlar yine de SqlMembership sağlayıcısı onunla aynı sınırlamalara yürütmek için evrensel sağlayıcıları ASP.NET üyeliği altyapısında yerleşik olarak bulunur. Diğer bir deyişle, bunlar ilişkisel veritabanları için tasarlanmıştır ve profili ve kullanıcı bilgilerini özelleştirmek zordur. Bu sağlayıcılar, form kimlik doğrulaması oturum açma ve oturum kapatma işlevsellik için yine de kullanın.

## <a name="aspnet-identity"></a>ASP.NET Kimlik

Üyelik hikayesi ASP.NET'te ASP.NET takımı geri bildirim müşterilerden gelen çok öğrendi yıllar içinde gelişmiştir.

Kullanıcıları bir kullanıcı adı ve kendi uygulamanıza isteneceği parola girerek oturum açacak varsayımıyla, artık geçerli değil. Web diğer sosyal haline gelmiştir. Kullanıcıların birbirleriyle gerçek zamanlı olarak Facebook, Twitter ve diğer sosyal web siteleri gibi sosyal kanallar aracılığıyla etkileşim. Geliştiriciler, kullanıcıların web sitelerinde zengin bir deneyim sağlayabilirsiniz sosyal kimliklerini oturum açmak istiyorsunuz. Modern üyelik sistemini yeniden yönlendirme tabanlı oturum açma işlemleri Facebook, Twitter ve diğerleri gibi kimlik doğrulama sağlayıcıları için etkinleştirmeniz gerekir.

Web geliştirme gelişerek gibi bu nedenle web geliştirme desenleri yaptım. Birim uygulama kodu test, uygulama geliştiricileri için bir temel sorun dönüştü. 2008'de, temel birim test edilebilir ASP.NET uygulamaları geliştirmek geliştiriciler kısmen yardımcı olmak için Model-View-Controller (MVC) deseni üzerinde yeni bir çerçeve ASP.NET eklendi. Ayrıca üyelik sistemi bunu yapabilmek için istiyordu, uygulama mantığını birimine istediği geliştiriciler test edin.

Web uygulaması geliştirme bu değişiklikleri göz önünde bulundurarak, ASP.NET Identity ile aşağıdaki hedeflere geliştirilmiştir:

- **Bir ASP.NET kimlik sistemi**

    - ASP.NET Identity, ASP.NET çerçevesini, ASP.NET MVC, Web Forms, Web sayfaları, Web API ve SignalR gibi tüm kullanılabilir.
    - Web, telefon, mağaza veya karma uygulamalar oluştururken, ASP.NET Identity kullanılabilir.
- **İlgili kullanıcı profili verileri takma kolaylığı**

    - Kullanıcı profili bilgilerini ve şema üzerinde denetiminiz vardır. Örneğin, uygulamanızda bir hesap kaydettiğinizde, kullanıcılar tarafından girilen Doğum tarihleri saklamak için sistem kolayca etkinleştirebilirsiniz.

- **Kalıcılık denetimi**

    - Varsayılan olarak, ASP.NET kimlik sistemi, tüm kullanıcı bilgilerini bir veritabanında depolar. ASP.NET Identity tüm Kalıcılık mekanizması uygulamak için Entity Framework Code First kullanır.
    - Denetim olduğundan veritabanı şemasını, tablo adlarının değiştirilmesi veya değiştirilmesi gibi genel görevleri yapmak birincil anahtar veri türü basittir.
    - Throw gerek kalmadan SharePoint, Azure depolama tablo hizmeti, NoSQL veritabanları, vs. gibi farklı depolama mekanizmaları takın kolaydır `System.NotImplementedExceptions` özel durumlar.
- **Birim Test Edilebilirlik**

    - ASP.NET Identity web uygulaması daha fazla birim test edilebilir hale getirir. Birim testleri için ASP.NET Identity kullanan uygulamanızın parçalarını yazabilirsiniz.
- **Rol sağlayıcısı**

    - Erişim için uygulamanızın parçalarını rolleri tarafından kısıtlamanıza olanak sağlayan bir rol sağlayıcısı yok. Kolayca "Admin" gibi roller oluşturabilir ve rollerine kullanıcı ekleme.
- **Talep tabanlı**

    - Burada kullanıcının kimliğini talepler kümesi temsil edilen talep tabanlı kimlik doğrulaması, ASP.NET Identity destekler. Talepler, geliştiricilerin rolleri izin verdiğinden, bir kullanıcının kimliğini tanımlamak için çok daha etkileyici olmasını sağlar. Rol üyeliği yalnızca bir Boole değeri (üye veya üye olmayan) iken, bir talep kullanıcının kimlik ve üyelik hakkında zengin bilgiler içerebilir.
- **Sosyal oturum açma sağlayıcıları**

    - Kolayca uygulamanıza Microsoft Account, Facebook, Twitter, Google ve diğerleri gibi sosyal oturum açma işlemleri ekleyin ve uygulamanızda kullanıcıya özgü verileri depolamak.

- **OWIN tümleştirme**

    - ASP.NET kimlik doğrulaması, artık tüm OWIN tabanlı ana bilgisayarda kullanılan OWIN ara yazılımı dayanır. ASP.NET Identity System.Web üzerinde herhangi bir bağımlılığı yok. Bu tam olarak uyumlu bir OWIN çerçeve ve herhangi bir OWIN barındırılan uygulamasında kullanılabilir.
    - ASP.NET Identity log-günlük-çıkış web sitesinde kullanıcı için OWIN kimlik doğrulaması kullanır. Bu, tanımlama bilgisi oluşturmak için FormsAuthentication kullanmak yerine, uygulamanın OWIN CookieAuthentication Bunu yapmak için kullandığı anlamına gelir.
- **NuGet paketi**

    - Visual Studio 2017'yle birlikte gelen ASP.NET MVC, Web Forms ve Web API şablonlarında yüklü bir NuGet paketi olarak ASP.NET Identity dağıtılır. Bu NuGet paketi NuGet gallery'den indirebilirsiniz.
    - ASP.NET Identity bir NuGet olarak bırakarak paket ASP.NET ekibinin yeni özellikler ve hata düzeltmeleri üzerinde yineleme yapmak ve bunları geliştiricilere Çevik bir şekilde teslim kolaylaştırır.

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity ile çalışmaya başlama

ASP.NET Identity Visual Studio 2017 proje şablonları, ASP.NET MVC, Web Forms, Web API ve SPA için kullanılır. Bu kılavuzda, biz nasıl kaydolun, oturum açın ve bir kullanıcının oturumunu kapatmaz işlevselliği eklemek için ASP.NET Identity proje şablonlarını kullanma gösterilmektedir.

Aşağıdaki yordamı kullanarak ASP.NET Identity uygulanır. Bu makalenin amacı, ASP.NET Identity üst düzey bir genel bakış, vermektir; adım adım izleyin veya yalnızca ayrıntıları okuyun. ASP.NET kimliği kullanıcıları, rolleri ve profil bilgilerini eklemek için yeni API kullanımı dahil olmak üzere, kullanarak uygulamaları oluşturma hakkında daha ayrıntılı yönergeler için bu makalenin sonunda sonraki adımlar bölümüne bakın.

1. Bir ASP.NET MVC uygulaması ile tek tek hesapları oluşturun. ASP.NET MVC, Web Forms, Web API ve SignalR vb. ASP.NET Identity kullanabilirsiniz. Bu makalede bir ASP.NET MVC uygulaması ile başlayacağız.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. Oluşturulan proje ASP.NET kimliği için aşağıdaki üç paketleri içerir.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   Bu paket, ASP.NET Identity veri ve şema SQL Server için açık kalır ASP.NET Identity için Entity Framework uygulamasını sahiptir.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   Bu paket, ASP.NET kimliği için temel arabirimler vardır. Bu paket, hedefleri farklı Kalıcılık, veritabanları vb. Azure tablo depolama, NoSQL gibi depolar, ASP.NET kimliği için bir uygulama yazmak için kullanılabilir.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   Bu paket, OWIN kimlik doğrulaması, ASP.NET uygulamalarındaki ASP.NET Identity ile bağlamak için kullanılan işlevselliği içerir. Oturum tanımlama bilgisi oluşturmak için çağrı OWIN tanımlama bilgisi kimlik doğrulaması ara yazılımı ve uygulama işlevselliği eklediğinizde, bu kullanılır.
3. Kullanıcı oluşturma.  
   Uygulamayı başlatın ve ardından **kaydetme** bir kullanıcı oluşturmak için bağlantı. Aşağıdaki görüntüde, kullanıcı adı ve parola toplar kayıt sayfası gösterilmektedir.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   Kullanıcı seçtiğinde **kaydetme** düğme `Register` eylem hesabı denetleyicinin aşağıda vurgulanan ASP.NET Identity API'sini çağırarak kullanıcı oluşturur:

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. Oturum Aç.  
   Kullanıcı başarıyla oluşturulduysa, kendisi tarafından oturum `SignInAsync` yöntemi.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]


   `SignInManager.SignInAsync` Yöntemi oluşturur bir [Claimsıdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx). ASP.NET Identity ve OWIN tanımlama bilgisi kimlik doğrulaması talep tabanlı bir sistemi olduğundan, framework kullanıcı için bir Claimsıdentity oluşturulacak uygulamayı gerektirir. Claimsıdentity hangi rolleri bir kullanıcının ait olduğu gibi kullanıcı için tüm talepleri ilgili bilgiler bulunur.   
 
5. Oturumunuzu kapatın.  
   Seçin **oturumunu** kapatma eylemi hesabı denetleyicisi çağırma için bağlantı. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   OWIN kod gösterir vurgulanan `AuthenticationManager.SignOut` yöntemi. Bunun için benzer [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) yöntemi tarafından kullanılan [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) Web formlarındaki modülü.

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity bileşenleri

ASP.NET kimlik sistemi bileşenlerini Aşağıdaki diyagramda gösterilmektedir (select deyiminde [bu](introduction-to-aspnet-identity/_static/image3.png) ya da büyütmek için diyagram üzerinde). Yeşil paketleri ASP.NET kimlik sistemi olun. Diğer tüm paketleri, ASP.NET kimlik sistemi ASP.NET uygulamaları kullanmak için gerekli bağımlılıklardır.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

Daha önce bahsedilen değil NuGet paketlerini kısa bir açıklaması verilmiştir:

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 Tanımlama bilgisi kullanmak bir uygulama sağlayan bir ara yazılım tabanlı kimlik doğrulaması, ASP benzer. NET form kimlik doğrulaması.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Varlık, ilişkisel veritabanları için Microsoft'un önerilen veri erişim teknolojisi çerçevedir.

## <a name="migrating-from-membership-to-aspnet-identity"></a>Üyeliğinden ASP.NET Identity'ye geçirme

Kısa süre içinde veya basit üyelik ASP.NET üyelik için yeni ASP.NET kimlik sistemi kullanan mevcut uygulamalarınızı geçirme hakkında yönergeler sağlamak üzere umuyoruz.

## <a name="next-steps"></a>Sonraki Adımlar

- [Facebook ve Google OAuth2 ve Openıd oturum açma ile bir ASP.NET MVC 5 uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 Öğreticide ASP.NET Identity API kullanıcı veritabanına profil bilgileri ve Google ve Facebook ile kimlik doğrulaması yapmayı eklemek için kullanılır.
- [Kimlik doğrulaması ve SQL DB ile bir ASP.NET MVC uygulaması oluşturma ve Azure App Service'e dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 Bu öğreticide, kullanıcıları ve rolleri eklemek için kimlik API kullanmayı gösterir.
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 Temel rol ve kullanıcı desteği eklemeyi ve rol ve kullanıcı yönetimi nasıl gösteren örnek uygulama.
