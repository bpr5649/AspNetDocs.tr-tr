---
uid: signalr/overview/security/introduction-to-security
title: SignalR Güvenliğine Giriş | Microsoft Dokümanlar
author: bradygaster
description: SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunlarını açıklar.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676197"
---
# <a name="introduction-to-signalr-security"></a>SignalR Güvenliğine Giriş

Patrick [Fletcher](https://github.com/pfletcher)tarafından , [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, bir SignalR uygulaması geliştirirken göz önünde bulundurmanız gereken güvenlik sorunları açıklanmaktadır.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Görsel Stüdyo 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.
>
> ## <a name="questions-and-comments"></a>Sorular ve yorumlar
>
> Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.

## <a name="overview"></a>Genel Bakış

Bu belgede aşağıdaki bölümler yer alır:

- [SignalR Güvenlik Kavramları](#concepts)

    - [Kimlik doğrulama ve yetkilendirme](#authentication)
    - [Bağlantı belirteci](#connectiontoken)
    - [Yeniden bağlanırken grupları yeniden birleştirme](#rejoingroup)
- [SignalR, SiteLer Arası İstek Sahtesini Nasıl Önler?](#csrf)
- [SignalR Güvenlik Önerileri](#recommendations)

    - [Güvenli Soket Katmanları (SSL) protokolü](#ssl)
    - [Grupları güvenlik mekanizması olarak kullanmayın](#groupsecurity)
    - [İstemcilerden gelen girdileri güvenli bir şekilde işleme](#input)
    - [Etkin bir bağlantı yla kullanıcı durumundaki değişikliği mutabakata varma](#reconcile)
    - [Otomatik olarak javascript proxy dosyaları oluşturuldu](#autogen)
    - [Özel Durumlar](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR Güvenlik Kavramları

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirme

SignalR, kullanıcıların kimliğini doğrulamak için herhangi bir özellik sağlamaz. Bunun yerine, SignalR özelliklerini bir uygulama için varolan kimlik doğrulama yapısına entegre eleştirirsiniz. Kullanıcıları, uygulamanızda normalde olduğu gibi doğrular sınız ve SignalR kodunuzdaki kimlik doğrulama sonuçlarıyla çalışırsınız. Örneğin, ASP.NET formkimlik doğrulaması yla kullanıcılarınızın kimliğini doğrulayabilirsiniz ve ardından hub'ınızda hangi kullanıcıların veya rollerin bir yöntemi çağırmayetkisine sahip olun. Hub'ınızda, kullanıcı adı veya kullanıcının bir role ait olup olmadığı gibi kimlik doğrulama bilgilerini istemciye de aktarabilirsiniz.

SignalR, hangi kullanıcıların bir hub'a veya yönteme erişimi olduğunu belirtmek için [Yetkilendirme](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) özniteliği sağlar. Yetkilendirme özniteliğini bir hub'a veya hub'daki belirli yöntemlere uygularsınız. Authorize özniteliği olmadan, hub'daki tüm ortak yöntemler hub'a bağlı bir istemci tarafından kullanılabilir. Hub'lar hakkında daha fazla bilgi için [Sinyal Hub'ları için Kimlik Doğrulama ve Yetkilendirme'ye](hub-authorization.md)bakın.

Öznitelik `Authorize` hub'lara uygularsınız, ancak kalıcı bağlantılara uygulayamazsınız. Bir yöntem kullanırken `PersistentConnection` yetkilendirme kurallarını zorlamak `AuthorizeRequest` için yöntemi geçersiz kılmanız gerekir. Kalıcı bağlantılar hakkında daha fazla bilgi [için SignalR Kalıcı Bağlantıları için Kimlik Doğrulama ve Yetkilendirme'ye](persistent-connection-authorization.md)bakın.

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Bağlantı belirteci

SignalR, gönderenin kimliğini doğrulayarak kötü amaçlı komutları yürütme riskini azaltır. Her istek için istemci ve sunucu, kimliği doğrulanmış kullanıcılar için bağlantı kimliği ve kullanıcı adını içeren bir bağlantı belirteci geçer. Bağlantı kimliği, bağlı her istemciyi benzersiz olarak tanımlar. Sunucu, yeni bir bağlantı oluşturulduğunda bağlantı kimliğini rasgele oluşturur ve bağlantı süresince bu kimliği devam eder. Web uygulaması için kimlik doğrulama mekanizması kullanıcı adını sağlar. SignalR, bağlantı belirteci korumak için şifreleme ve dijital imza kullanır.

![](introduction-to-security/_static/image2.png)

Her istek için sunucu, isteğin belirtilen kullanıcıdan geldiğinden emin olmak için belirteci içeriğini doğrular. Kullanıcı adı bağlantı kimliğine karşılık gelir. SignalR, hem bağlantı kimliğini hem de kullanıcı adını doğrulayarak kötü amaçlı bir kullanıcının başka bir kullanıcıyı kolayca taklit etmesini önler. Sunucu bağlantı belirteci doğrulayamıyorsa, istek başarısız olur.

![](introduction-to-security/_static/image4.png)

Bağlantı kimliği doğrulama işleminin bir parçası olduğundan, bir kullanıcının bağlantı kimliğini diğer kullanıcılarla göstermemeniz veya bir çerez gibi istemcide değeri saklamamalısınız.

#### <a name="connection-tokens-vs-other-token-types"></a>Bağlantı belirteçleri ve diğer belirteç türleri

Bağlantı belirteçleri, oturum belirteçleri veya kimlik doğrulama belirteçleri gibi göründükleri için zaman zaman güvenlik araçları tarafından işaretlenir ve bu da açığa çıktığında risk oluşturur.

SignalR'ın bağlantı belirteci kimlik doğrulama belirteci değildir. Bu isteği yapan kullanıcının bağlantıyı oluşturan kullanıcıyla aynı olduğunu doğrulamak için kullanılır. ASP.NET SignalR bağlantıların sunucular arasında taşınmasına izin verdiği için bağlantı belirteci gereklidir. Belirteç, bağlantıyı belirli bir kullanıcıyla ilişkilendirir, ancak isteği yapan kullanıcının kimliğini iddia etmez. SignalR isteğinin doğru şekilde doğrulanabilmesi için, kullanıcının kimliğini belirten çerez veya taşıyıcı belirteci gibi başka bir belirteci olması gerekir. Ancak, bağlantı belirteci kendisi isteği bu kullanıcı tarafından yapıldı hiçbir iddiada bulunmaz, yalnızca belirteç içinde bulunan bağlantı kimliği bu kullanıcı ile ilişkili olduğunu.

Bağlantı belirteci kendi kimlik doğrulama talebi sağlamadığından, "oturum" veya "kimlik doğrulama" belirteci olarak kabul edilir. Belirli bir kullanıcının bağlantı belirteci almak ve farklı bir kullanıcı (veya kimlik doğrulaması olmayan bir istek) olarak doğrulanmış bir istekte yeniden oynatmak başarısız olur, çünkü isteğin kullanıcı kimliği ve belirteçte depolanan kimlik eşleşmez.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Yeniden bağlanırken grupları yeniden birleştirme

Varsayılan olarak, SignalR uygulaması, bağlantı nın kesilmesi ve bağlantı zamanları bitmeden yeniden kurulması gibi geçici bir kesintiden yeniden bağlanırken kullanıcıyı otomatik olarak uygun gruplara yeniden atar. Yeniden bağlanırken, istemci bağlantı kimliğini ve atanan grupları içeren bir grup belirteci geçer. Grup belirteci dijital olarak imzalanır ve şifrelenir. İstemci yeniden bağlantıdan sonra aynı bağlantı kimliğini saklar; bu nedenle, yeniden bağlanan istemciden geçirilen bağlantı kimliği istemci tarafından kullanılan önceki bağlantı kimliğiyle eşleşmelidir. Bu doğrulama, kötü amaçlı bir kullanıcının yeniden bağlanırken yetkisiz gruplara katılmak için istekler geçirmesini önler.

Ancak, grup belirteci süresinin dolmadığını unutmayın. Bir kullanıcı geçmişte bir gruba aitse, ancak bu gruptan men edilmişse, bu kullanıcı yasaklı grubu içeren bir grup belirteci taklit edebilir. Hangi kullanıcıların hangi gruplara ait olduğunu güvenli bir şekilde yönetmeniz gerekiyorsa, bu verileri veritabanında olduğu gibi sunucuda depolamanız gerekir. Ardından, uygulamanıza, kullanıcının bir gruba ait olup olmadığını sunucuda doğrulayan mantık ekleyin. Grup üyeliğini doğrulama örneği [için](../guide-to-the-api/working-with-groups.md)bkz.

Gruplara otomatik olarak yeniden katılma yalnızca geçici bir kesintiden sonra bir bağlantı yeniden bağlandığında uygulanır. Bir kullanıcı uygulamadan uzaklaşarak bağlantısını keserse veya uygulama yeniden başlatılırsa, uygulamanızın bu kullanıcıyı doğru gruplara nasıl ekleyeceğini işlemesi gerekir. Daha fazla bilgi için [bkz.](../guide-to-the-api/working-with-groups.md)

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR, SiteLer Arası İstek Sahtesini Nasıl Önler?

Site Arası İstek Sahteciliği (CSRF), kötü amaçlı bir sitenin kullanıcının şu anda oturum açtığı savunmasız bir siteye istek gönderdiği bir saldırıdır. SignalR, kötü amaçlı bir sitenin SignalR uygulamanız için geçerli bir istek oluşturmasını son derece olası hale getirerek CSRF'yi önler.

### <a name="description-of-csrf-attack"></a>CSRF saldırısının açıklaması

Aşağıda bir CSRF saldırısı örneği verilmiştir:

1. Kullanıcı form kimlik doğrulamasını kullanarak www.example.com oturum açar.
2. Sunucu kullanıcının kimliğini doğrular. Sunucudan gelen yanıt bir kimlik doğrulama çerezi içerir.
3. Oturumu açmadan, kullanıcı kötü amaçlı bir web sitesini ziyaret eder. Bu kötü amaçlı site aşağıdaki HTML formunu içerir:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Form eyleminin kötü amaçlı siteye değil, savunmasız siteye gönderdiğine dikkat edin. Bu CSRF "çapraz site" parçasıdır.
4. Kullanıcı gönder düğmesini tıklatıyor. Tarayıcı, istekle birlikte kimlik doğrulama çerezini içerir.
5. İstek, kullanıcının kimlik doğrulama bağlamıyla example.com sunucusunda çalışır ve kimlik doğrulaması yapılan bir kullanıcının yapmasına izin verilen her şeyi yapabilir.

Bu örnek, kullanıcının form düğmesini tıklatmasını gerektirmesine rağmen, kötü amaçlı sayfa signalr uygulamanıza bir AJAX isteği gönderen bir komut dosyası gibi kolayca çalıştırılabilir. Ayrıca, kötü amaçlı site "https://" isteği gönderebileceğinden, SSL kullanmak Bir CSRF saldırısını engellemez.

Genellikle, tarayıcılar ilgili tüm çerezleri hedef web sitesine gönderdiğinden, kimlik doğrulama için tanımlama bilgilerini kullanan web sitelerine karşı CSRF saldırıları mümkündür. Ancak, CSRF saldırıları çerezleri istismar ile sınırlı değildir. Örneğin, Temel ve Özet kimlik doğrulaması da savunmasızdır. Bir kullanıcı Temel veya Özet kimlik doğrulaması ile oturum açtıktan sonra, tarayıcı oturum bitene kadar kimlik bilgilerini otomatik olarak gönderir.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR tarafından alınan CSRF azaltımları

SignalR, kötü amaçlı bir sitenin uygulamanız için geçerli istekler oluşturmasını önlemek için aşağıdaki adımları atar. SignalR varsayılan olarak bu adımları atar, kodunuzda herhangi bir işlem yapmanız gerekmez.

- **Çapraz etki alanı isteklerini devre dışı** SignalR, kullanıcıların harici bir etki alanından SignalR bitiş noktasını aramasını önlemek için etki alanı isteklerini devre dışı kılmaktadır. SignalR, harici bir etki alanından gelen herhangi bir talebigeçersiz kabul eder ve isteği engeller. Bu varsayılan davranışı korumanızı öneririz; aksi takdirde, kötü amaçlı bir site kullanıcıları sitenize komut göndermeleri için kandırabilir. Etki alanları arası istekleri kullanmanız gerekiyorsa, [etki alanları arası bağlantının nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) öğrenin.
- **Geçiş bağlantı belirteci sorgu dizesinde, çerez değil** SignalR, bağlantı belirteci yerine bir sorgu dize değeri olarak geçer. Tarayıcı kötü amaçlı kodla karşılaşıldığında yanlışlıkla bağlantı belirteci iletebilir, çünkü bir çerez bağlantı belirteci depolama kullanabilirsiniz güvenli değildir. Ayrıca, sorgu dizesinde bağlantı belirteci geçmek, bağlantı belirtecinin geçerli bağlantının ötesinde kalıcı olmasını engeller. Bu nedenle, kötü amaçlı bir kullanıcı başka bir kullanıcının kimlik doğrulama kimlik bilgileri altında istekte bulunamaz.
- **Bağlantı belirteci doğrula** [Bağlantı belirteci](#connectiontoken) bölümünde açıklandığı gibi, sunucu kimlik doğrulaması yapılan her kullanıcıyla hangi bağlantı kimliğinin ilişkili olduğunu bilir. Sunucu, kullanıcı adı ile eşleşmeyen bir bağlantı kimliğinden gelen herhangi bir isteği işlemez. Kötü niyetli kullanıcının kullanıcı adını ve rasgele oluşturulan geçerli bağlantı kimliğini bilmesi gerekeceği için kötü amaçlı bir kullanıcının geçerli bir isteği tahmin etmesi olası değildir. Bağlantı sona erdirilir sona ermez bu bağlantı kimliği geçersiz olur. Anonim kullanıcıların herhangi bir hassas bilgilere erişimi olmamalıdır.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR Güvenlik Önerileri

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Güvenli Soket Katmanları (SSL) protokolü

SSL protokolü, bir istemci ve sunucu arasında veri aktarımını güvence altına almak için şifreleme kullanır. SignalR uygulamanız istemci ve sunucu arasında hassas bilgiler iletiyorsa, aktarım için SSL'yi kullanın. SSL kurulumu hakkında daha fazla bilgi için [IIS 7'de SSL'yi nasıl ayarlayınız.](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Grupları güvenlik mekanizması olarak kullanmayın

Gruplar, ilgili kullanıcıları toplamanın kullanışlı bir yoludur, ancak hassas bilgilere erişimi sınırlamak için güvenli bir mekanizma değildir. Bu, özellikle kullanıcılar yeniden bağlanma sırasında gruplara otomatik olarak yeniden katılabiliyorsa geçerlidir. Bunun yerine, bir role ayrıcalıklı kullanıcılar eklemeyi ve hub yöntemine erişimi yalnızca bu rolün üyeleriyle sınırlamayı düşünün. Bir role dayalı erişimi kısıtlamak için [bkz.](hub-authorization.md) Yeniden bağlanırken gruplara kullanıcı erişimini denetleme örneği [için](../guide-to-the-api/working-with-groups.md)bkz.

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>İstemcilerden gelen girdileri güvenli bir şekilde işleme

Kötü amaçlı bir kullanıcının komut dosyasını diğer kullanıcılara göndermediğinden emin olmak için, istemcilerden diğer istemcilere yayın için tasarlanmış tüm girişleri kodlamanız gerekir. SignalR uygulamanızda çok farklı istemci türleri olabileceğinden, iletileri sunucu yerine alıcı istemcilere kodlamanız gerekir. Bu nedenle, HTML kodlama bir web istemcisi için çalışır, ancak istemcilerin diğer türleri için değil. Örneğin, bir sohbet iletisi görüntülemek için bir web istemcisi yöntemi `html()` işlevi arayarak kullanıcı adı ve iletigüvenli bir şekilde işleyebilir.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Etkin bir bağlantı yla kullanıcı durumundaki değişikliği mutabakata varma

Etkin bir bağlantı varken bir kullanıcının kimlik doğrulama durumu değişirse, kullanıcı "Etkin bir SignalR bağlantısı sırasında kullanıcı kimliği değiştirilemez" diyen bir hata alır. Bu durumda, bağlantı kimliğinin ve kullanıcı adının koordine olduğundan emin olmak için uygulamanızın sunucuya yeniden bağlanması gerekir. Örneğin, uygulamanız etkin bir bağlantı varken kullanıcının oturumu açmasına izin veriyorsa, bağlantının kullanıcı adı artık bir sonraki istek için geçirilen adla eşleşmez. Kullanıcı oturumu açmadan önce bağlantıyı durdurmak ve sonra yeniden başlatmak isteyeceksiniz.

Ancak, çoğu uygulamanın bağlantıyı el ile durdurması ve başlatması gerekmeyeceğini unutmayın. Uygulamanız oturumu açtıktan sonra kullanıcıları web formları uygulamasındaki varsayılan davranış veya oturumu açtıktan sonra geçerli sayfayı yenilerse, etkin bağlantı otomatik olarak kesilir ve ek bir işlem gerektirmez.

Aşağıdaki örnek, kullanıcı durumu değiştiğinde bir bağlantıyı nasıl durdurup başlatılacak gösterilmektedir.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Veya, siteniz Form kimlik doğrulamasıyla kaydırma son kullanma süresi kullanıyorsa ve kimlik doğrulama çerezini geçerli tutmak için etkinlik yoksa, kullanıcının kimlik doğrulama durumu değişebilir. Bu durumda, kullanıcı oturumu kapatılır ve kullanıcı adı artık bağlantı belirtecindeki kullanıcı adıyla eşleşmez. Kimlik doğrulama çerezini geçerli tutmak için web sunucusundaki bir kaynağı düzenli aralıklarla isteyen bazı komut dosyası ekleyerek bu sorunu giderebilirsiniz. Aşağıdaki örnek, her 30 dakikada bir kaynak isteğinin nasıl istendiğini gösterir.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Otomatik olarak javascript proxy dosyaları oluşturuldu

Her kullanıcı için JavaScript proxy dosyasına tüm hub'ları ve yöntemleri eklemek istemiyorsanız, dosyanın otomatik oluşturma devre dışı kullanabilirsiniz. Birden çok hub'ıniz ve yönteminiz varsa, ancak her kullanıcının tüm yöntemlerden haberdar olmasını istemiyorsanız, bu seçeneği seçebilirsiniz. **EnableJavaScriptProxies'i** **false'a**ayarlayarak otomatik üretimi devre dışı bıraktınız.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript proxy dosyaları hakkında daha fazla bilgi için, [oluşturulan proxy ve sizin için ne yaptığını](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)bakın. <a id="exceptions"></a>

### <a name="exceptions"></a>Özel Durumlar

Nesneler hassas bilgileri istemcilere gösterebileceğinden, özel durum nesnelerini istemcilere aktarmaktan kaçınmalısınız. Bunun yerine, ilgili hata iletisini görüntüleyen istemcide bir yöntem çağırın.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
