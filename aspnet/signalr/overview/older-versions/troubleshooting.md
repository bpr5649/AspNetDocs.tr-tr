---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR Sorun Giderme (SignalR 1.x) | Microsoft Dokümanlar
author: bradygaster
description: Bu makalede, SignalR uygulamaları geliştirme ile ilgili yaygın sorunlar açıklanmaktadır.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543099"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR Sorunlarını Giderme (SignalR 1.x)

tarafından [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belge, SignalR ile sık karşılaşılan sorun giderme sorunlarını açıklar.

Bu belge aşağıdaki bölümleri içerir.

- [İstemci ve sunucu arasındaki arama yöntemleri sessizce başarısız olur](#connection)
- [Diğer bağlantı sorunları](#other)
- [Derleme ve sunucu tarafı hataları](#server)
- [Visual Studio sorunları](#vs)
- [İnternet Bilgi Hizmetleri sorunları](#iis)
- [Azure sorunları](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>İstemci ve sunucu arasındaki arama yöntemleri sessizce başarısız olur

Bu bölümde, istemci ve sunucu arasındaki yöntem çağrısının anlamlı bir hata iletisi olmadan başarısız olmasının olası nedenleri açıklanmaktadır. SignalR uygulamasında, sunucunun istemcinin uyguladığı yöntemler hakkında hiçbir bilgisi yoktur; sunucu bir istemci yöntemi çağırdığında, yöntem adı ve parametre verileri istemciye gönderilir ve yöntem yalnızca sunucunun belirttiği biçimde varsa yürütülür. İstemcide eşleşen bir yöntem bulunmazsa, hiçbir şey olmaz ve sunucuda hata iletisi yükseltilmez.

İstemci yöntemlerinin çağrılmadığını daha fazla araştırmak için, sunucudan hangi çağrıların geldiğini görmek için hub'daki başlangıç yöntemini aramadan önce günlüğe kaydetmeyi açabilirsiniz. JavaScript uygulamasında günlüğe kaydetmeyi etkinleştirmek [için istemci tarafı günlüğe kaydetmeyi (JavaScript istemci sürümü) nasıl etkinleştirin.](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging) .NET istemci uygulamasında günlüğe kaydetmeyi etkinleştirmek [için istemci tarafı günlüğe kaydetmeyi (.NET İstemci sürümü) nasıl etkinleştirin.](../guide-to-the-api/hubs-api-guide-net-client.md#logging)

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Yanlış yazılmış yöntem, yanlış yöntem imzası veya yanlış hub adı

Çağrılan bir yöntemin adı veya imzası istemcide uygun bir yöntemle tam olarak eşleşmiyorsa, arama başarısız olur. Sunucu tarafından çağrılan yöntem adının istemcideki yöntemin adıyla eşleştiğini doğrulayın. Ayrıca, SignalR JavaScript uygun olarak deve kasalı yöntemleri kullanarak hub proxy `SendMessage` oluşturur, bu nedenle `sendMessage` sunucuda çağrılan bir yöntem istemci proxy çağrılır. Sunucu tarafındaki `HubName` kodunuzda özniteliği kullanırsanız, kullanılan adın istemcide hub'ı oluşturmak için kullanılan adla eşleştiğini doğrulayın. Özniteliği kullanmıyorsanız, `HubName` JavaScript istemcisindeki hub'ın adının ChatHub yerine chatHub gibi deve kasası olduğunu doğrulayın.

### <a name="duplicate-method-name-on-client"></a>İstemciüzerinde yinelenen yöntem adı

İstemcide yalnızca duruma göre farklılık gösteren bir yinelenen yönteminiz olmadığını doğrulayın. İstemci uygulamanızda adı `sendMessage`verilen bir yöntem varsa, aynı `SendMessage` zamanda çağrılan bir yöntem de olmadığını doğrulayın.

### <a name="missing-json-parser-on-the-client"></a>Müşteri üzerinde Eksik JSON parser

SignalR, sunucu ve istemci arasındaki aramaları seri hale getirmek için bir JSON araleyicisinin bulunmasını gerektirir. İstemcinizin yerleşik bir JSON parer'i yoksa (Internet Explorer 7 gibi), uygulamanıza bir tane eklemeniz gerekir. [Burada](http://nuget.org/packages/json2)JSON parser indirebilirsiniz.

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Karıştırma Hub ve PersistentConnection sözdizimi

SignalR iki iletişim modeli kullanır: Hub'lar ve Kalıcı Bağlantılar. Bu iki iletişim modelini arama sözdizimi istemci kodunda farklıdır. Sunucu kodunuza bir hub eklediyseniz, istemci kodunun tamamının uygun hub sözdizimini kullandığını doğrulayın.

**JavaScript istemcisinde Kalıcı Bağlantı oluşturan JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Javascript istemcisinde Hub Proxy oluşturan JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**Bir rotayı PersistentConnection'a eşleyen C# sunucu kodu**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**Birden çok uygulamanız varsa, bir hub'a veya birden çok hub'a rota lar oluşturan C# sunucu kodu**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>Abonelikler eklenmeden önce bağlantı başlatıldı

Sunucudan çağrılabilen yöntemler proxy'ye eklenmeden Hub bağlantısı başlatılırsa, iletiler alınmaz. Aşağıdaki JavaScript kodu hub'ı düzgün bir şekilde başlatmaz:

**Hubs iletilerinin alınmasına izin vermeyecek yanlış JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Bunun yerine, Başlat'ı aramadan önce yöntem aboneliklerini ekleyin:

**Bir hub'a abonelikleri doğru bir şekilde ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Hub proxy'de eksik yöntem adı

Sunucuda tanımlanan yöntemin istemcide abone olduğunu doğrulayın. Sunucu yöntemi tanımlasa da, yine de istemci proxy'ye eklenmesi gerekir. Yöntemler istemci proxy'ye aşağıdaki yollarla eklenebilir (Yöntemin doğrudan `client` hub'a değil, hub üyesine eklandığını unutmayın):

**Hub proxy'ye yöntem ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Genel olarak bildirilmemiş hub veya hub yöntemleri

İstemci üzerinde görünür olması için hub uygulaması `public`ve yöntemleri .

### <a name="accessing-hub-from-a-different-application"></a>Hub'a farklı bir uygulamadan erişim

SignalR Hub'larına yalnızca SignalR istemcilerini uygulayan uygulamalar aracılığıyla erişilebilir. SignalR diğer iletişim kitaplıklarıyla (SOAP veya WCF web hizmetleri gibi) birlikte çalışamaz. Hedef platformunuz için kullanılabilir sinyalr istemcisi yoksa, sunucunun bitiş noktasına doğrudan erişemezsiniz.

### <a name="manually-serializing-data"></a>Verileri el ile serileştirme

SignalR, yöntem parametrelerinizi seri hale getirmek için Otomatik olarak JSON'u kullanır- bunu kendiniz yapmanıza gerek yoktur.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Uzaktan Hub yöntemi OnDisconnected işlevinde istemcide yürütülmedi

Bu davranış tasarım gereğidir. Çağrıldığında, `OnDisconnected` hub zaten `Disconnected` daha fazla hub yöntemlerinin çağrılmasını izin vermez duruma girmiştir.

**OnDisconnected olayında kodu doğru şekilde yürüten C# sunucu kodu**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>Bağlantı sınırına ulaşıldı

IIS'nin tam sürümünü Windows 7 gibi bir istemci işletim sisteminde kullanırken, 10 bağlantı sınırı uygulanır. İstemci işletim sistemi kullanırken, bu sınırdan kaçınmak için Bunun yerine IIS Express'i kullanın.

### <a name="cross-domain-connection-not-set-up-properly"></a>Etki alanı bağlantısı düzgün ayarlanmamıştır

Bir etki alanı bağlantısı (SignalR URL'sinin barındırma sayfasıyla aynı etki alanında olmadığı bir bağlantı) doğru şekilde ayarlanmazsa, bağlantı hata iletisi olmadan başarısız olabilir. Etki alanları arası iletişimi etkinleştirme hakkında bilgi için, [etki alanları arası bağlantının nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)öğrenin.

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>.NET istemcisinde çalışmayan NTLM (Active Directory) kullanarak bağlantı

Bağlantı düzgün yapılandırılmamışsa, Etki Alanı güvenliğini kullanan bir .NET istemci uygulamasındaki bağlantı başarısız olabilir. SignalR'i etki alanı ortamında kullanmak için gerekli bağlantı özelliğini aşağıdaki gibi ayarlayın:

**Bağlantı kimlik bilgilerini uygulayan C# istemci kodu**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>Diğer bağlantı sorunları

Bu bölümde, bağlantı sırasında oluşan belirli belirtiler veya hata iletileri için nedenler ve çözümler açıklanmaktadır.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"Veriler gönderilmeden önce Başlat çağrılmalı" hatası

Bu hata genellikle bağlantı başlatılmadan önce signalr nesnelerine başvuruyorsa görülür. Bağlantı tamamlandıktan sonra sunucuda tanımlanan yöntemleri çağıracak işleyiciler ve benzeri için wireup eklenmelidir. Çağrının eşzamanlı `Start` olduğunu unutmayın, bu nedenle arama tamamlandıktan sonra kod yürütülebilir. Bağlantı tamamen başladıktan sonra işleyicileri eklemenin en iyi yolu, bunları başlangıç yöntemine parametre olarak geçirilen bir geri arama işlevine koymaktır:

**SignalR nesnelerine başvuran olay işleyicilerini doğru bir şekilde ekleyen JavaScript istemci kodu**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

SignalR nesneleri hala başvurulmaktayken bir bağlantı durursa bu hata da görülür.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 Kalıcı Olarak Taşınmış" veya "302 Geçici Olarak Taşınmış" hatası

Proje, otomatik olarak oluşturulan proxy'yi engelleyecek SignalR adlı bir klasör içeriyorsa bu hata görülebilir. Bu hatayı önlemek için, uygulamanızda `SignalR` adı geçen bir klasör kullanmayın veya otomatik proxy oluşturmayı kapatın. [Oluşturulan Proxy'ye ve](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) daha fazla ayrıntı için sizin için neler yaptığını görün.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET veya Silverlight istemcisinde "403 Yasak" hatası

Bu hata, etki alanları arası iletişimin düzgün şekilde etkinleştirilen olmadığı etki alanları arası ortamlarda oluşabilir. Etki alanları arası iletişimi etkinleştirme hakkında bilgi için, [etki alanları arası bağlantının nasıl kurulabildiğini](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)öğrenin. Silverlight istemcisinde etki alanı bağlantısı kurmak için [Silverlight istemcilerinden çapraz etki alanı bağlantılarına](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)bakın.

### <a name="404-not-found-error"></a>"404 Bulunamadı" hatası

Bu sorunun çeşitli nedenleri vardır. Aşağıdakilerin tümlerini doğrulayın:

- **Hub proxy adresi başvurusu doğru biçimlendirilmemiş:** Oluşturulan hub proxy adresine başvuru doğru biçimlendirme değilse, bu hata genellikle görülür. Hub adresine yapılan başvurunun doğru yapıldığından doğrulayın. Ayrıntılar için [dinamik olarak oluşturulan proxy'ye nasıl başvurulsağlayacağına](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) bakın.
- **Hub rotasını eklemeden önce uygulamaya yol ekleme:** Uygulamanız başka yollar kullanıyorsa, `MapHubs`eklenen ilk rotanın .

### <a name="500-internal-server-error"></a>"500 Dahili Sunucu Hatası"

Bu nedenleri geniş bir yelpazede olabilir çok genel bir hatadır. Hatanın ayrıntıları sunucunun olay günlüğünde görünmelidir veya sunucunun hata ayıklama yoluyla bulunabilir. Sunucudaki ayrıntılı hataları açarak daha ayrıntılı hata bilgileri elde edilebilir. Daha fazla bilgi için [Hub sınıfındaki hataları nasıl işlersin.](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; tanımsız" hatası

Arama düzgün yapılmazsa `MapHubs` bu hata ortaya çıkacaktır. [SinyalR rotasını nasıl kaydedin ve](../guide-to-the-api/hubs-api-guide-server.md#route) daha fazla bilgi için SignalR seçeneklerini yapılandırmaya bakın.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException kullanıcı kodu tarafından işlenmemiş oldu

Yöntemlerinize gönderdiğiniz parametrelerin seri olarak izlenebilir olmayan türleri (dosya tutamaçları veya veritabanı bağlantıları gibi) içermediğini doğrulayın. İstemciye gönderilmek istemediğiniz sunucu tarafındaki bir nesnede (güvenlik için veya serileştirme nedeniyle) üye kullanmanız `JSONIgnore` gerekiyorsa, özniteliği kullanın.

### <a name="protocol-error-unknown-transport-error"></a>"Protokol hatası: Bilinmeyen aktarım" hatası

İstemci SignalR'ın kullandığı aktarımları desteklemiyorsa bu hata oluşabilir. SignalR ile hangi tarayıcıların kullanılabileceğini bilgi için [Transports ve Fallbacks'e](../getting-started/introduction-to-signalr.md#transports) bakın.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript Hub proxy oluşturma devre dışı bırakıldı."

Dinamik olarak oluşturulan `DisableJavaScriptProxies` proxy'ye bir başvuru da dahil edilirken `signalr/hubs`ayarlanırsa bu hata oluşur. Proxy'yi el ile oluşturma hakkında daha fazla bilgi için [oluşturulan proxy'ye ve sizin için neler yaptığına](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)bakın.

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"Bağlantı kimliği yanlış biçimde" veya "Etkin bir SinyalR bağlantısı sırasında kullanıcı kimliği değiştirilemez" hatası

Kimlik doğrulaması kullanılıyorsa ve bağlantı durdurulmadan önce istemci oturumu kapatılırsa bu hata görülebilir. Çözüm, istemciyi oturumu açmadan önce SignalR bağlantısını durdurmaktır.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Yakalanmayan Hata: SignalR: jQuery bulunamadı. Lütfen SignalR.js dosyasından önce jQuery'ye başvuruldığından emin olun" hatası

SignalR JavaScript istemcisi jQuery'nin çalışmasını gerektirir. jQuery başvurunuzun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery'ye yapılan başvurunun SignalR'a başvurudan önce olduğunu doğrulayın.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"Caught TypeError: Tanımlanmamış&lt;özellik&gt;' özelliği ' okuyamıyorum" hatası

Bu hata, jQuery veya hub proxy düzgün başvurulan olmaması ndan kaynaklanır. jQuery ve hub proxy'ye başvurunuzun doğru olduğunu, kullanılan yolun geçerli olduğunu ve jQuery'ye yapılan başvurunun hub proxy'ye başvurudan önce olduğunu doğrulayın. Hub'lar proxy varsayılan başvuru aşağıdaki gibi görünmelidir:

**Hubs proxy'ye doğru başvuran HTML istemci tarafı kodu**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException kullanıcı kodu tarafından işlenmemiş oldu" hatası

Yanlış aşırı yükleme `Hub.On` kullanıldığında bu hata oluşabilir. Yöntemin iade değeri varsa, iade türü genel bir tür parametresi olarak belirtilmelidir:

**İstemci üzerinde tanımlanan yöntem (oluşturulan proxy olmadan)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>Bağlantı kimliği tutarsız veya sayfa yükleri arasında bağlantı sonu

Bu davranış tasarım gereğidir. Hub nesnesi sayfa nesnesinde barındırıldığından, sayfa yenilendiğinde hub yok edilir. Çok sayfalı bir uygulama, sayfa yükleri arasında tutarlı olacak şekilde kullanıcılar ve bağlantı disleri arasındaki ilişkiyi korumak gerekir. Bağlantı adları sunucuda bir `ConcurrentDictionary` nesne de veya veritabanında depolanabilir.

### <a name="value-cannot-be-null-error"></a>"Değer null olamaz" hatası

İsteğe bağlı parametrelere sahip sunucu tarafı yöntemleri şu anda desteklenmez; isteğe bağlı parametre atlanırsa, yöntem başarısız olur. Daha fazla bilgi için [Isteğe Bağlı Parametreler'e](https://github.com/SignalR/SignalR/issues/324)bakın.

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>Firebug hata "Firefox &lt;adresinde&gt;sunucuya bir bağlantı kuramaz "

WebSocket aktarımının anlaşması başarısız olursa ve bunun yerine başka bir aktarım kullanılırsa, bu hata iletisi Firebug'da görülebilir. Bu davranış tasarım gereğidir.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET istemci uygulamasında "Uzak sertifika doğrulama prosedürüne göre geçersizdir" hatası

Sunucunuz özel istemci sertifikaları gerektiriyorsa, istek yapılmadan önce bağlantıya x509sertifikası ekleyebilirsiniz. Kullanarak bağlantıya sertifika `Connection.AddClientCertificate`ekleyin.

### <a name="connection-drops-after-authentication-times-out"></a>Kimlik doğrulama süreleri bittikten sonra bağlantı düşer

Bu davranış tasarım gereğidir. Bağlantı etkinken kimlik doğrulama kimlik bilgileri değiştirilemez; kimlik bilgilerini yenilemek için bağlantının durdurulması ve yeniden başlatılması gerekir.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected jQuery Mobile kullanırken iki kez çağrılır

jQuery Mobile'ın `initializePage` işlevi, her sayfadaki komut dosyalarını yeniden yürütülmesi için zorlayarak ikinci bir bağlantı oluşturur. Bu soruna yönelik çözümler şunlardır:

- JavaScript dosyanızdan önce jQuery Mobile'a başvuruyu ekleyin.
- İşlevayarlayarak `initializePage` `$.mobile.autoInitializePage = false`işlevi devre dışı
- Bağlantıyı başlatmadan önce sayfanın başlatmayı bitirmesini bekleyin.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Sunucu Gönderilen Etkinlikler kullanılarak Silverlight uygulamalarında iletiler geciktirilir

Silverlight'ta sunucu nun gönderdiği olaylar kullanılarak iletiler gecikiyor. Bunun yerine uzun yoklamanın kullanılmasını zorlamak için bağlantıyı kurarken aşağıdakileri kullanın:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>Forever Frame protokolünü kullanarak "İzin Reddedildi"

Bu bilinen bir konudur, [burada](https://github.com/SignalR/SignalR/issues/1963)açıklanan. Bu belirti en son JQuery kitaplığı kullanılarak görülebilir; geçici çözüm JQuery 1.8.2 için uygulamanızı düşürmek için.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Derleme ve sunucu tarafı hataları

 Aşağıdaki bölümde derleyici ve sunucu tarafı çalışma zamanı hataları için olası çözümler içerir. 

### <a name="reference-to-hub-instance-is-null"></a>Hub örneğine başvuru null

Her bağlantı için bir hub örneği oluşturulduğundan, kodunuzda kendiniz hub örneği oluşturamazsınız. Hub'ın dışından bir hub'da yöntemleri çağırmak için, hub bağlamına başvuru almak için [hub sınıfının dışından gelen grupları nasıl arayacağınızı ve grupları](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) nasıl yöneteceklerini görün.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session geçersizdir

Bu davranış tasarım gereğidir. SignalR, oturum durumunu etkinleştirme çift yönlü iletiyi kıracağı için ASP.NET oturum durumunu desteklemez.

### <a name="no-suitable-method-to-override"></a>Geçersiz kılmak için uygun bir yöntem yok

Eski belgelerden veya bloglardan kod kullanıyorsanız bu hatayı görebilirsiniz. Değiştirilen veya amortismana alınmış yöntemlerin adlarını (örneğin) `OnConnectedAsync`başvurmadığınızı doğrulayın.

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions.WebSocketServerUrl null

Bu davranış tasarım gereğidir. Bu üye amortismana sokulmalıdır ve kullanılmamalıdır.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"'signalr.hub' adlı bir rota zaten rota koleksiyonunda" hatası

Uygulamanız tarafından iki `MapHubs` kez çağrılırsa bu hata görülecektir. Bazı örnek uygulamalar `MapHubs` doğrudan genel uygulama dosyasında arama; diğerleri bir sarmalayıcı sınıfında arama yapmak. Uygulamanızın her ikisini de yapmadığından emin olun.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio sorunları

Bu bölümde Visual Studio'da karşılaşılan sorunlar açıklanmaktadır.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Komut Dosyası Belgeleri düğümü Çözüm Gezgini'nde görünmüyor

Bazı öğreticilerimiz hata ayıklama sırasında sizi Solution Explorer'daki "Komut Dosyası Belgeleri" düğümüne yönlendirir. Bu düğüm JavaScript hata ayıklama tarafından üretilir ve yalnızca Internet Explorer'da tarayıcı istemcilerini hata ayıklarken görünür; Chrome veya Firefox kullanılırsa düğüm görünmez. Silverlight hata ayıklama gibi başka bir istemci hata ayıklama çalışıyorsa JavaScript hata ayıklama da çalışmaz.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR Visual Studio 2008 veya daha önce çalışmıyor

Bu davranış tasarım gereğidir. SignalR gerektirir .NET Framework 4 veya daha sonra; bu, SignalR uygulamalarının Visual Studio 2010 veya sonraki yıllarda geliştirilmesini gerektirir.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS sorunları

Bu bölümde Internet Bilgi Hizmetleri ile ilgili sorunlar içerir.

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs çağrısından sonra web sitesi çöküyor

Bu sorun SignalR'ın en son sürümünde giderilmiştir. Yüklemenizi NuGet kullanarak güncelleyerek SignalR'ın en son sürümünden kullandığınızı doğrulayın.

<a id="azure"></a>

## <a name="azure-issues"></a>Azure sorunları

Bu bölümde Microsoft Azure ile ilgili sorunlar bulunmaktadır.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Konu adlarını değiştirdikten sonra Iletiler Azure arka düzlemi üzerinden alınmaz

Azure arka düzlemi tarafından kullanılan konular kullanıcı tarafından yapılandırılabilir olarak tasarlanmamıştır.
