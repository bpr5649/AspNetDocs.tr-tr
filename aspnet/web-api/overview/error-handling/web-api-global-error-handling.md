---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2'de Genel Hata İşleme - 4ASP.NET
author: davidmatson
description: ASP.NET 4.x için ASP.NET Web API 2'deki genel hata işleme genel bakışı.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675424"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2'de Genel Hata İşleme

David [Matson](https://github.com/davidmatson)tarafından , [Rick Anderson](https://twitter.com/RickAndMSFT)

Bu konu, ASP.NET 4.x için ASP.NET Web API 2'deki genel hata işleme genel görünümünü sağlar. Bugün Web API'sinde hataları genel olarak günlüğe kaydetmenin veya işlemenin kolay bir yolu yoktur. Bazı işlenmemiş özel durumlar [özel durum filtreleri](exception-handling.md)aracılığıyla işlenebilir, ancak özel durum filtrelerinin işleyebileceği birkaç özel durum vardır. Örneğin:

1. Denetleyici oluşturuculardan atılan özel durumlar.
2. İleti işleyicilerinden atılan özel durumlar.
3. Yönlendirme sırasında atılan özel durumlar.
4. Yanıt içeriği serileştirme sırasında atılan özel durumlar.

Bu özel durumları (mümkünse) günlüğe kaydetmek ve işlemek için basit ve tutarlı bir yol sağlamak istiyoruz. 

Özel durumları işlemek için iki önemli durum vardır, hata yanıtı gönderebildiğimiz ve tek yapabildiğimiz özel durumu günlüğe kaydetmek tir. İkinci durum için bir örnek, bir özel durum akış yanıt içeriğinin ortasına atıldığında; bu durumda durum kodu, üstbilgi ve kısmi içerik zaten tel üzerinden gitti, bu yüzden sadece bağlantı iptal beri yeni bir yanıt iletisi göndermek için çok geç. Özel durum yeni bir yanıt iletisi oluşturmak için ele alınamasa da, özel durumu günlüğe kaydetmeyi yine de destekliyoruz. Bir hata algılayabildiğimiz durumlarda, aşağıdakilerde gösterildiği gibi uygun bir hata yanıtı döndürebiliriz:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Varolan Seçenekler

[Özel durum filtrelerine](exception-handling.md)ek olarak, [ileti işleyicileri](../advanced/http-message-handlers.md) bugün 500 düzeyli yanıtların tümlerini gözlemlemek için kullanılabilir, ancak özgün hatayla ilgili bağlamları olmadığı için bu yanıtlara göre hareket etmek zordur. İleti işleyicileri de işleyebilir servis talepleri ile ilgili özel durum filtreleri olarak aynı sınırlamalar bazı vardır. Web API'de hata koşullarını yakalayan izleme altyapısı olsa da, izleme altyapısı tanılama amacıyladır ve üretim ortamlarında çalıştırmak için tasarlanmamıştır veya uygun değildir. Genel özel durum işleme ve günlüğe kaydetme, üretim sırasında çalıştırılabilen ve varolan izleme çözümlerine bağlanabilen hizmetler olmalıdır (örneğin, [ELMAH).](https://code.google.com/p/elmah/)

### <a name="solution-overview"></a>Çözüme Genel Bakış

 İşlenmemiş özel durumları günlüğe kaydetmek ve işlemek için iki yeni kullanıcı değiştirilebilir hizmet , [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) ve IExceptionHandler saiyoruz. Hizmetler çok benzer, iki ana farklılıklar ile:

1. Birden çok özel durum kaydedicisi, ancak yalnızca tek bir özel durum işleyicisi kaydetmeyi destekliyoruz.
2. İstisna kaydediciler her zaman çağrılır, bağlantıyı iptal etmek üzere olsak bile. Özel durum işleyicileri yalnızca hangi yanıt iletisini göndereceğimizi hala seçebildiğimizde çağrılır.

Her iki hizmet de, özel durum algılandığı noktadan ilgili bilgileri içeren bir özel durum bağlamına, özellikle [HttpRequestMessage,](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx) [HttpRequestContext,](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)atılan özel durum ve özel durum kaynağına (aşağıdaki ayrıntılar) erişim sağlar.

### <a name="design-principles"></a>Tasarım İlkeleri

1. **Son dakika değişikliği yok** Bu işlevsellik küçük bir sürümde eklendiğiniz için, çözümü etkileyen önemli bir kısıtlama, sözleşme yazmak veya davranış için herhangi bir kırılma değişiklik olmamasıdır. Bu kısıtlama, özel durumları 500 yanıta dönüştüren varolan catch blokları açısından yapmak istediğimiz bazı temizlemeleri ekarte etti. Bu ek temizleme biz bir sonraki büyük sürümü için düşünebilirsiniz bir şeydir. Bu sizin için önemli yse, lütfen [ASP.NET Web API kullanıcı sesi](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)nde oy verin.
2. **Web API yapıları ile tutarlılık sağlama** Web API'nin filtre boru hattı, eyleme özel, denetleyiciye özgü veya küresel kapsamda mantığı uygulama esnekliğiyle çapraz kesme yle başa çıkmanın harika bir yoludur. Özel durum filtreleri de dahil olmak üzere filtreler, genel kapsamda kaydedilmiş olsa lar bile her zaman eylem ve denetleyici bağlamlarına sahiptir. Bu sözleşme filtreler için anlamlıdır, ancak özel durum filtreleri, hatta genel olarak kapsamlı olanlar, hiçbir eylem veya denetleyici bağlam var ileti işleyicileri, özel durumlar gibi bazı özel durum işleme durumlarda için iyi bir uyum olmadığı anlamına gelir. Özel durum işleme için filtreler tarafından sağlanan esnek kapsam landırmayı kullanmak istiyorsak, yine de özel durum filtrelerine ihtiyacımız vardır. Ancak, denetleyici bağlamı dışında özel durumu ele almamız gerekirse, tam genel hata işleme için ayrı bir yapıya da ihtiyacımız vardır (denetleyici bağlamı ve eylem bağlamı kısıtlamaları olmayan bir şey).

### <a name="when-to-use"></a>Ne Zaman Kullanılır

- Özel durum kaydediciler, Web API tarafından yakalanan tüm işlenmemiş özel durum ları görmenin çözümüdür.
- Özel durum işleyicileri, Web API tarafından yakalanan işlenmemiş özel durumlara olası tüm yanıtları özelleştirmek için çözümdür.
- Özel durum filtreleri, belirli bir eylem veya denetleyiciyle ilgili işlenmemiş özel durumları işlemek için en kolay çözümdür.

### <a name="service-details"></a>Servis Detayları

 Özel durum kaydedici ve işleyici hizmet arabirimleri, ilgili bağlamları alarak basit async yöntemleridir: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Ayrıca, bu arabirimlerin her ikisi için de temel sınıflar salıyoruz. Çekirdek (eşitleme veya eşitleme) yöntemlerini geçersiz kılmak, önerilen zamanlarda günlüğe kaydetmek veya işlemek için gereken tek şeydir. Günlüğe kaydetme `ExceptionLogger` için, temel sınıf çekirdek günlüğe kaydetme yönteminin her özel durum için yalnızca bir kez çağrılmasını sağlar (daha sonra çağrı yığınını daha da yukarı yaysa ve tekrar yakalanırsa bile). `ExceptionHandler` Taban sınıf, eski iç içe geçme bloklarını yoksayarak yalnızca çağrı yığınının üst kısmındaki özel durumlar için çekirdek işleme yöntemini çağırır. (Bu temel sınıfların basitleştirilmiş sürümleri aşağıdaki ekte yer almaktadır.) Her `IExceptionLogger` `IExceptionHandler` ikisi de ve bir `ExceptionContext`üzerinden özel durum hakkında bilgi almak.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Çerçeve bir özel durum kaydedici veya özel durum işleyicisi çağırır, her zaman bir `Exception` ve bir `Request`. Birim testi dışında, aynı zamanda `RequestContext`her zaman bir sağlayacaktır . Nadiren bir `ControllerContext` ve `ActionContext` (yalnızca özel durum filtreleri için catch bloğundan ararken) sağlar. Çok nadiren bir `Response`(sadece bazı IIS durumlarda zaman yanıt yazmaya çalışırken ortasında) sağlayacaktır. Bu özelliklerden bazıları olabileceğinden, `null` özel durum sınıfının `null` üyelerine erişmeden önce denetlemenin tüketiciye bağlı olduğunu unutmayın.`CatchBlock` catch bloğunun özel durumu gördüğünü belirten bir dizedir. Catch block dizeleri aşağıdaki gibidir:

- HttpServer (SendAsync yöntemi)
- HttpControllerDispatcher (SendAsync yöntemi)
- HttpBatchHandler (SendAsync yöntemi)
- IExceptionFilter (ApiController'ın ExecuteAsync'deki özel durum filtresi denetim hattını işlemesi)
- OWIN ev sahibi:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (çıktı arabelleğe alma için)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (akış çıktısı için)
- Web barındırma:

    - httpControllerHandler.WriteBufferedResponseContentAsync (çıktı arabelleğe alma için)
    - httpControllerHandler.WriteStreamedResponseContentAsync (akış çıktısı için)
    - httpControllerHandler.WriteErrorResponseContentAsync (arabelleğe alma modu altında hata kurtarma hataları için)

Catch block dizeleri listesi statik salt özellikleri ile de kullanılabilir. (Çekirdek catch blok dizesi statik ExceptionCatchBlocks üzerindedir; geri kalanı OWIN ve web ana bilgisayar için her biri statik bir sınıfta görünür).`IsTopLevelCatchBlock` yalnızca çağrı yığınının üst kısmında ki özel durumları işleme nin önerilen deseni takip etmek için yararlıdır. İç içe geçme bloğu oluştuğu her yerde özel durumları 500 yanıta dönüştürmek yerine, özel durum işleyicisi, ana bilgisayar tarafından görülmek üzere olana kadar özel durumların yayılmasına izin verebilir.

Ek `ExceptionContext`olarak, bir logger tam `ExceptionLoggerContext`üzerinden bilgi bir parça daha alır:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

İkinci özellik, `CanBeHandled`bir logger işlenemez bir özel durum tanımlamak için izin verir. Bağlantı iptal etmek üzereyken ve yeni yanıt iletisi gönderilemiyorsa, kaydediciler çağrılacak, ancak işleyici ***çağrılmaz*** ve günbazı bu senaryoyu bu özellikten tanımlayabilir.

Ek `ExceptionContext`olarak, bir işleyici özel durum işlemek için `ExceptionHandlerContext` tam ayarlayabilirsiniz bir özellik daha alır:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Bir özel durum işleyicisi, `Result` özelliği bir eylem sonucuna ayarlayarak bir özel durum işlettiğini gösterir (örneğin, bir Özel Durum [Sonucu](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx), veya özel bir sonuç). `Result` Özellik null ise, özel durum işlenir ve özgün özel durum yeniden atılır.

Arama yığınının üst kısmındaki istisnalar için, yanıtın API arayanlar için uygun olduğundan emin olmak için fazladan bir adım attık. Özel durum ana bilgisayara yayılırsa, arayan normal bir şekilde HTML olan ve genellikle uygun bir API hata yanıtı olmayan yanıt veren sarı ölüm ekranını veya başka bir ana bilgisayarı görür. Bu gibi durumlarda, Sonuç null olmayan başlar ve yalnızca özel bir özel durum `null` işleyicisi açıkça geri ayarlar (işlenmemiş) özel durum ana bilgisayara yayılır. Bu gibi durumlarda ayar `Result` iki senaryo için yararlı olabilir: `null`

1. OWIN, Web API'sinden önce/dışında kayıtlı ara yazılımları işleyen özel istisnalarla Birlikte Web API'yi barındırıdadır.
2. Ölümün sarı ekranının aslında işlenmemiş bir özel durum için yararlı bir yanıt olduğu bir tarayıcı üzerinden yerel hata ayıklama.

Hem özel durum kaydediciler hem de özel durum işleyicileri için, logger veya işleyicinin kendisi bir özel durum atarsa kurtarmak için hiçbir şey yapmayız. (İstisnanın yayılmasına izin vermek dışında, daha iyi bir yaklaşımınız varsa bu sayfanın alt kısmında geri bildirim bırakın.) İstisna kaydediciler ve işleyicileri için sözleşme, istisnalar arayanlar kadar yaymak izin vermemek gerektiğini; aksi takdirde, özel durum genellikle bir HTML hatası (ASP gibi) sonuçlanan ana bilgisayara tüm yol, yayılır. NET'in sarı ekranı) istemciye geri gönderiliyor (genellikle JSON veya XML bekleyen API arayanlar için tercih edilen seçenek değildir).

## <a name="examples"></a>Örnekler

### <a name="tracing-exception-logger"></a>Özel Durum Kaydedici'nin İzini İzleme

Aşağıdaki özel durum kaydedicisi, yapılandırılmış İzleme kaynaklarına (Visual Studio'daki Hata Ayıklama çıkış penceresi dahil) özel durum verilerini gönderir.

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Özel Hata İletiSi Özel Durum Işleyicisi

Aşağıdaki özel durum işleyicisi, desteğe başvurmak için bir e-posta adresi de dahil olmak üzere istemcilere özel bir hata yanıtı üretir.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Özel Durum Filtrelerini Kaydetme

Projenizi oluşturmak için "ASP.NET MVC 4 Web Uygulaması" proje şablonunu kullanıyorsanız, `WebApiConfig` Web API yapılandırma kodunuzu sınıfın içine, *App_Start* klasörüne koyun:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Ek: Taban Sınıf Bilgileri

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
