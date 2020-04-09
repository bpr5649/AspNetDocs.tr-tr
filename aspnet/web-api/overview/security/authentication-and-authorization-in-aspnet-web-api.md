---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API'sinde kimlik doğrulama ve yetkilendirme | Microsoft Dokümanlar
author: MikeWasson
description: ASP.NET Web API'sinde kimlik doğrulama ve yetkilendirme hakkında genel bir genel bakış sağlar.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676260"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API'sinde kimlik doğrulama ve yetkilendirme

Mike [Wasson](https://github.com/MikeWasson) tarafından

Bir web API'sı oluşturdunuz, ancak şimdi web'e erişimi denetlemek istiyorsunuz. Bu makale serisinde, yetkisiz kullanıcılardan bir web API'sini güvence altına almak için bazı seçeneklere bakacağız. Bu seri hem kimlik doğrulamayı hem de yetkilendirmeyi kapsayacaktır.

- *Kimlik doğrulama,* kullanıcının kimliğini bilmektir. Örneğin, Alice kullanıcı adı ve parolasıyla oturum açar ve sunucu Alice'in kimliğini doğrulamak için parolayı kullanır.
- *Yetkilendirme,* bir kullanıcının bir eylem gerçekleştirmesine izin verilip verilmeyeceğine karar vermektir. Örneğin, Gamze'nin kaynak almak için izni vardır, ancak kaynak oluşturmaz.

Serinin ilk makalesi, web API'ASP.NET kimlik doğrulama ve yetkilendirmeye genel bir genel bakış sağlar. Diğer konular, Web API'si için yaygın kimlik doğrulama senaryolarını açıklar.

> [!NOTE]
> Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken: Bu dizi gözden ve değerli geribildirim sağlanan insanlar sayesinde.

## <a name="authentication"></a>Kimlik Doğrulaması

Web API kimlik doğrulamasının ana bilgisayarda gerçekleştiğini varsayar. Web barındırma için, ana bilgisayar kimlik doğrulaması için HTTP modülleri kullanan IIS'dir. Projenizi, IIS veya ASP.NET yerleşik kimlik doğrulama modüllerinden herhangi birini kullanacak şekilde yapılandırabilir veya özel kimlik doğrulaması gerçekleştirmek için kendi HTTP modülünüzü yazabilirsiniz.

Ana bilgisayar kullanıcının kimliğini doğruladığında, kodun çalıştırıldığı güvenlik bağlamını temsil eden bir [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) nesnesi olan bir *anapara*oluşturur. Ana **bilgisayar, Thread.CurrentPrincipal'ı**ayarlayarak asıl başlığı geçerli iş parçacığına bağlar. Asıl, kullanıcı hakkında bilgi içeren ilişkili bir **Kimlik** nesnesi içerir. Kullanıcının kimliği doğrulanmışsa, **Identity.IsAuthenticated** özelliği **doğru**döndürür. Anonim istekler **için, IsAuthenticated** **yanlış**döndürür. Müdürler hakkında daha fazla bilgi için [Bkz. Rol Tabanlı Güvenlik.](https://msdn.microsoft.com/library/shz8h065.aspx)

### <a name="http-message-handlers-for-authentication"></a>Kimlik Doğrulama için HTTP İleti Işleyicileri

Kimlik doğrulaması için ana bilgisayarı kullanmak yerine, kimlik doğrulama mantığını bir [HTTP ileti işleyicisine](../advanced/http-message-handlers.md)koyabilirsiniz. Bu durumda, ileti işleyicisi HTTP isteğini inceler ve asıllığı ayarlar.

Kimlik doğrulaması için ileti işleyicilerini ne zaman kullanmalısınız? İşte bazı tradeoffs şunlardır:

- Bir HTTP modülü, ASP.NET ardışık alandan geçen tüm istekleri görür. İleti işleyicisi yalnızca Web API'sine yönlendirilen istekleri görür.
- Belirli bir rotaya kimlik doğrulama düzeni uygulamanıza olanak tanıyan rota başına ileti işleyicileri ayarlayabilirsiniz.
- HTTP modülleri IIS'e özgüdür. İleti işleyicileri ana bilgisayar anostiktir, bu nedenle hem web barındırma hem de kendi kendine barındırma ile kullanılabilirler.
- HTTP modülleri IIS günlüğü, denetimi ve benzeri çalışmalara katılır.
- HTTP modülleri boru hattında daha erken çalışır. İleti işleyicisinde kimlik doğrulaması işlerseniz, işleyici çalışana kadar asıl ayaralmaz. Ayrıca, yanıt ileti işleyicisi ayrıldığında asıl önceki ana müdüre geri döner.

Genellikle, kendi kendine barındırma desteklemek gerekmez, bir HTTP modülü daha iyi bir seçenektir. Kendi kendine barındırmayı desteklemeniz gerekiyorsa, bir ileti işleyicisi düşünün.

### <a name="setting-the-principal"></a>Müdürü ayarlama

Uygulamanız herhangi bir özel kimlik doğrulama mantığı gerçekleştiriyorsa, asıllığı iki yere ayarlamanız gerekir:

- **Konu.CurrentPrincipal**. Bu özellik, iş parçacığının anasını .NET'te ayarlamanın standart yoludur.
- **httpContext.Current.User**. Bu özellik ASP.NET özgüdür.

Aşağıdaki kod, asılın nasıl ayarlanır olduğunu gösterir:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Web barındırma için, her iki yerde de ana lığı belirlemeniz gerekir; aksi takdirde güvenlik bağlamı tutarsız hale gelebilir. Kendi kendine barındırma için, ancak, **HttpContext.Current** null. Kodunuzu ana bilgisayar-agnostik olduğundan emin olmak için, bu nedenle, gösterildiği gibi **HttpContext.Current'a**atamadan önce null olup olmadığını denetleyin.

## <a name="authorization"></a>Yetkilendirme

Yetkilendirme daha sonra boru hattında, denetleyiciye daha yakın olur. Bu, kaynaklara erişim izni verirken daha ayrıntılı seçimler yapmanızı sağlar.

- *Yetkilendirme filtreleri* denetleyici eyleminden önce çalışır. İstek yetkilendirilemezse, filtre bir hata yanıtı döndürür ve eylem çağrılmaz.
- Denetleyici eylemi içinde, geçerli anaparayı **ApiController.User** özelliğinden alabilirsiniz. Örneğin, yalnızca bu kullanıcıya ait kaynakları döndürerek kullanıcı adını temel alan bir kaynak listesini filtreleyebilirsiniz.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[Authorize] Özniteliğini Kullanma

Web API yerleşik yetkilendirme filtresi sağlar, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Bu filtre, kullanıcının kimliğinin doğrulanıp doğrulanmadığını denetler. Değilse, eylemi devreye girmeden HTTP durum kodu 401 (Yetkisiz) döndürür.

Filtreyi genel olarak, denetleyici düzeyinde veya tek tek eylemler düzeyinde uygulayabilirsiniz.

**Genel Olarak**: Her Web API denetleyicisi için erişimi kısıtlamak **için, yetkilendirme** özniteliği filtresini genel filtre listesine ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Denetleyici**: Belirli bir denetleyicinin erişimini kısıtlamak için, filtreyi denetleyiciye öznitelik olarak ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Eylem**: Belirli eylemlere erişimi kısıtlamak için, özniteliği eylem yöntemine ekleyin:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Alternatif olarak, denetleyiciyi kısıtlayabilir ve özniteliği kullanarak `[AllowAnonymous]` belirli eylemlere anonim erişime izin verebilirsiniz. Aşağıdaki örnekte, `Post` yöntem sınırlıdır, ancak `Get` yöntem anonim erişimsağlar.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

Önceki örneklerde, filtre kimlik doğrulaması yapılan herhangi bir kullanıcının kısıtlı yöntemlere erişmesine izin verir; yalnızca anonim kullanıcılar dışarıda tutulur. Erişimi belirli kullanıcılara veya belirli rollerdeki kullanıcılarla da sınırlandırabilirsiniz:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API denetleyicileri için **YetkilendirmeÖze filtresi** **System.Web.Http** ad alanında bulunur. **System.Web.Mvc** ad alanında, Web API denetleyicileriyle uyumlu olmayan MVC denetleyicileri için benzer bir filtre vardır.

### <a name="custom-authorization-filters"></a>Özel Yetkilendirme Filtreleri

Özel yetkilendirme filtresi yazmak için aşağıdaki türlerden birini türetin:

- **AuthorizeAttribute**. Geçerli kullanıcıyı ve kullanıcının rollerini temel alan yetkilendirme mantığını gerçekleştirmek için bu sınıfı genişletin.
- **YetkilendirmeFilterAttribute**. Geçerli kullanıcıya veya role dayalı olmayan eşzamanlı yetkilendirme mantığını gerçekleştirmek için bu sınıfı genişletin.
- **IAuthorizationFiltresi**. Eşzamanlı yetkilendirme mantığı gerçekleştirmek için bu arabirimi uygulayın; örneğin, yetkilendirme mantığınız eşzamanlı G/Ç veya ağ aramaları yapıyorsa. (Yetkilendirme mantığınız CPU'ya bağlıysa, **AuthorizationFilterAttribute'tan**türetmek daha kolaydır, çünkü o zaman bir eşzamanlı yöntem yazmanız gerekmez.)

Aşağıdaki diyagram, **AuthorizeAttribute** sınıfının sınıf hiyerarşisini gösterir.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Denetleyici Eylem İçinde Yetkilendirme

Bazı durumlarda, isteğin devam etmesine izin verebilirsiniz, ancak davranışı anaparaya göre değiştirebilirsiniz. Örneğin, döndürüleceğiniz bilgiler kullanıcının rolüne bağlı olarak değişebilir. Denetleyici yöntemi nde geçerli anaparayı **ApiController.User** özelliğinden alabilirsiniz.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
