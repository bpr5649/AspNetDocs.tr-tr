---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows Kimlik Doğrulama (VB) ile Kullanıcıların Kimlik Doğrulaması | Microsoft Dokümanlar
author: rick-anderson
description: Bir MVC uygulaması bağlamında Windows kimlik doğrulamasını nasıl kullanacağınızı öğrenin. Uygulamanızın web co içinde Windows kimlik doğrulaması etkinleştirmek için nasıl öğrenirler ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 446dcc338f61e1f76478c1085773e7ad089c73f4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540603"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>Windows Kimlik Doğrulaması ile Kullanıcıların Kimliğini Doğrulama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Bir MVC uygulaması bağlamında Windows kimlik doğrulamasını nasıl kullanacağınızı öğrenin. Uygulamanızın web yapılandırma dosyasında Windows kimlik doğrulamasını nasıl etkinleştirdiğinizi ve Kimlik doğrulamayı IIS ile nasıl yapılandırabileceğinizi öğrenirsiniz. Son olarak, denetleyici eylemlerine erişimi belirli Windows kullanıcıları veya gruplarıyla sınırlamak için [Yetkilendirme] özniteliğini nasıl kullanacağınızı öğrenirsiniz.

Bu öğreticinin amacı, MVC uygulamalarınızdaki görünümleri parolayla korumak için Internet Bilgi Hizmetleri'nde yerleşik güvenlik özelliklerinden nasıl yararlanabileceğinizi açıklamaktır. Denetleyici eylemlerinin yalnızca belirli Windows kullanıcıları veya belirli Windows gruplarının üyesi kullanıcılar tarafından çağrılmasını nasıl sağlayacağınızı öğrenirsiniz.

Windows kimlik doğrulamasını kullanmak, bir şirket içi web sitesi (intranet sitesi) oluşturuyorsanız ve kullanıcılarınızın web sitesine erişirken standart Windows kullanıcı adlarını ve parolalarını kullanabilmesini istediğinizde anlamlıdır. Dışa dönük bir web sitesi (Bir Internet web sitesi) oluşturuyorsanız, bunun yerine Formkimlik doğrulaması kullanmayı düşünün.

#### <a name="enabling-windows-authentication"></a>Windows Kimlik Doğrulamasını Etkinleştirme

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, Windows kimlik doğrulaması varsayılan olarak etkinleştirilir. Form kimlik doğrulaması, MVC uygulamaları için etkinleştirilmiş varsayılan kimlik doğrulama türüdür. MVC uygulamanızın web yapılandırmasını (web.config) dosyasını değiştirerek Windows kimlik doğrulamasını etkinleştirmelisiniz. &lt;Kimlik doğrulama&gt; bölümünü bulun ve Formlar kimlik doğrulaması yerine Windows'u kullanacak şekilde değiştirin:

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

Windows kimlik doğrulamasını etkinleştirdiğinizde, web sunucunuz kullanıcıların kimlik doğrulamasorumlusundan sorumlu olur. Genellikle, bir ASP.NET mvc uygulaması oluştururken ve dağıtırken kullandığınız iki farklı web sunucusu türü vardır.

İlk olarak, bir MVC uygulaması geliştirirken Visual Studio ile birlikte ASP.NET Geliştirme Web Sunucusu'nu kullanırsınız. Varsayılan olarak, ASP.NET Geliştirme Web Sunucusu tüm sayfaları geçerli Windows hesabı bağlamında yürütür (Windows'da oturum açmak için kullandığınız hesap ne olursa olsun).

ASP.NET Geliştirme Web Sunucusu da NTLM kimlik doğrulamasını destekler. Çözüm Gezgini penceresinde projenizin adını sağ tıklayarak ve Özellikler'i seçerek NTLM kimlik doğrulamasını etkinleştirebilirsiniz. Ardından, Web sekmesini seçin ve NTLM onay kutusunu işaretleyin (Bkz. Şekil 1).

**Şekil 1 – ASP.NET Geliştirme Web Sunucusu için NTLM kimlik doğrulamasını etkinleştirme**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

Bir üretim web uygulaması için, elde, web sunucusu olarak IIS kullanın. IIS, çeşitli kimlik doğrulama türlerini destekler:

- Temel Kimlik Doğrulama – HTTP 1.0 protokolünün bir parçası olarak tanımlanır. Internet üzerinden açık metin (Base64 kodlanmış) kullanıcı adları ve parolalar gönderir. - Digest Authentication - Internet üzerinden şifre kendisi yerine, bir şifre karma gönderir. - Entegre Windows (NTLM) Kimlik Doğrulaması – Pencereleri kullanarak intranet ortamlarında kullanılacak en iyi kimlik doğrulama türüdür. - Sertifika Kimlik Doğrulaması – İstemci tarafı sertifikası kullanarak kimlik doğrulamasını sağlar. Sertifika, bir Windows kullanıcı hesabına eşler.

> [!NOTE] 
> 
> Bu farklı kimlik doğrulama türlerinin daha ayrıntılı [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)bir özeti için bkz.

Belirli bir kimlik doğrulama türünü etkinleştirmek için Internet Information Services Manager'ı kullanabilirsiniz. Her işletim sisteminde her türlü kimlik doğrulamanın kullanılmadığını unutmayın. Ayrıca, Windows Vista ile IIS 7.0 kullanıyorsanız, Internet Bilgi Hizmetleri Yöneticisi'nde görünmeden önce farklı Windows kimlik doğrulama türlerini etkinleştirmeniz gerekir. **Denetim Masası, Programlar, Programlar ve Özellikler açık, Windows özelliklerini açıp kapatın**ve Internet Bilgi Hizmetleri düğümünü genişletin (Bkz. Şekil 2).

**Şekil 2 – Windows IIS özelliklerini etkinleştirme**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

Internet Bilgi Hizmetleri'ni kullanarak farklı kimlik doğrulama türlerini etkinleştirebilir veya devre dışı kullanabilirsiniz. Örneğin, Şekil 3 anonim kimlik doğrulamasını devre dışı bırakmayı ve IIS 7.0 kullanırken Tümleşik Windows (NTLM) kimlik doğrulamasını etkinleştirmeyi göstermektedir.

**Şekil 3 – Tümleşik Windows Kimlik Doğrulamasını Etkinleştirme**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows Kullanıcılarını ve Gruplarını Yetkilendirme

Windows kimlik doğrulamasını etkinleştirdikten sonra, denetleyicilere veya denetleyici eylemlerine erişimi denetlemek için &lt;Yetkilendirme&gt; özniteliğini kullanabilirsiniz. Bu öznitelik, tüm MVC denetleyicisine veya belirli bir denetleyici eylemine uygulanabilir.

Örneğin, Listeleme 1'deki Ev denetleyicisi Index(), CompanySecrets() ve StephenSecrets() adlı üç eylemi ortaya çıkarır. Herkes Index() eylemini çağırabilir. Ancak, yalnızca Windows yerel Yöneticileri grubunun üyeleri CompanySecrets() eylemini çağırabilir. Son olarak, yalnızca Stephen adlı Windows etki alanı kullanıcısı (Redmond etki alanında) StephenSecrets() eylemini başlatabilir.

**Listeleme 1 – Denetleyiciler\HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> Windows Kullanıcı Hesabı Denetimi (UAC) nedeniyle, Windows Vista veya Windows Server 2008 ile çalışırken, yerel Yöneticiler grubu diğer gruplardan farklı davranacaktır. Bilgisayarınızın &lt;&gt; UAC ayarlarını değiştirmediğiniz sürece Yetkilendirme özniteliği yerel Yöneticiler grubunun bir üyesini doğru şekilde tanımaz.

Doğru izinler olmadan bir denetleyici eylemi çağırmaya çalıştığınızda tam olarak ne olur, kimlik doğrulamanın etkinleştirilen türüne bağlıdır. Varsayılan olarak, ASP.NET Geliştirme Sunucusu'nu kullanırken boş bir sayfa elde edersiniz. Sayfa **401 Yetkili değil** HTTP Yanıt Durumu ile servis edilir.

Diğer taraftan, Anonim kimlik doğrulama devre dışı bırakılmış ve Temel kimlik doğrulama etkini ile IIS kullanıyorsanız, korumalı sayfayı her istediğinizde bir giriş iletişim istemi almaya devam emzebilirsiniz (Bkz. Şekil 4).

**Şekil 4 – Temel kimlik doğrulama giriş iletişim kutusu**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>Özet

Bu öğretici, windows kimlik doğrulamasını ASP.NET bir MVC uygulaması bağlamında nasıl kullanabileceğinizi açıklamıştır. Uygulamanızın web yapılandırma dosyasında Windows kimlik doğrulamasını etkinleştirmeyi ve Kimlik Doğrulamayı IIS ile nasıl yapılandırabileceğinizi öğrendiniz. Son olarak, denetleyici eylemlerine erişimi belirli Windows kullanıcıları veya gruplarıyla sınırlamak için &lt;Yetkilendirme&gt; özniteliğini nasıl kullanacağınızı öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](authenticating-users-with-forms-authentication-vb.md)
> [Sonraki](preventing-javascript-injection-attacks-vb.md)
