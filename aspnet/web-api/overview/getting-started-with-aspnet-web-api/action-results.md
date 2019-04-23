---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Eylem sonuçlarını Web API 2 - ASP.NET 4.x
author: MikeWasson
description: Nasıl ASP.NET Web API dönüş değeri bir denetleyici eylemi bir HTTP yanıt iletisine ASP.NET'te dönüştürür açıklar 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400899"
---
# <a name="action-results-in-web-api-2"></a>Web API 2’de Eylem Sonuçları

tarafından [Mike Wasson](https://github.com/MikeWasson)

Bu konuda, nasıl ASP.NET Web API dönüş değeri bir denetleyici eylemi bir HTTP yanıt iletisine dönüştürür açıklanmaktadır.

Bir Web API denetleyici eylemi aşağıdakilerden herhangi birini geri dönebilirsiniz:

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. Başka bir türü

Bu bağlı olarak getirilen, Web API'si, HTTP yanıtı oluşturmak için farklı bir mekanizma kullanır.

| Dönüş türü | Web API'si yanıtı nasıl oluşturur? |
| --- | --- |
| void | Boş dönüş 204 (içerik yok) |
| **HttpResponseMessage** | Bir HTTP yanıt iletisi doğrudan dönüştürün. |
| **IHttpActionResult** | Çağrı **ExecuteAsync** oluşturmak için bir **HttpResponseMessage**, ardından bir HTTP yanıt iletisi dönüştürün. |
| Diğer tür | Yanıt gövdesine seri hale getirilmiş dönüş değeri yazabilirsiniz. 200 (Tamam) döndürür. |

Bu konunun geri kalanında her bir seçenek daha ayrıntılı açıklanmaktadır.

## <a name="void"></a>void

Dönüş türü ise `void`, Web API'sini yalnızca boş bir HTTP yanıtının durum kodu 204 (içerik yok) döndürür.

Örnek denetleyicisi:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP yanıtı:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

Eylem döndürürse bir [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API'si dönüştürür dönüş değeri doğrudan bir HTTP yanıt iletisine, özelliklerini kullanarak **HttpResponseMessage** doldurmak için nesne yanıt.

Bu seçenek birçok yanıt iletisi üzerinde denetim sağlar. Örneğin, aşağıdaki denetleyici eylemi Cache-Control üst bilgisi ayarlar.

[!code-csharp[Main](action-results/samples/sample3.cs)]

Yanıt:

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

Bir etki alanı modeline geçirirseniz **CreateResponse** yöntemi, Web API'sini kullanan bir [medya biçimlendiricisi](../formats-and-model-binding/media-formatters.md) serileştirilmiş modeli yanıt gövdesine yazılacak.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API'si, biçimlendirici seçmek için istekte Accept üst bilgisi kullanır. Daha fazla bilgi için [içerik anlaşması](../formats-and-model-binding/content-negotiation.md).

## <a name="ihttpactionresult"></a>IHttpActionResult

**Ihttpactionresult** arabirimi, Web API 2'de tanıtılmıştır. Esas olarak tanımlayan bir **HttpResponseMessage** üreteci. Kullanmanın bazı avantajları şunlardır **Ihttpactionresult** arabirimi:

- Basitleştirir [birim testi](../testing-and-debugging/unit-testing-controllers-in-web-api.md) denetleyicilerinizi.
- HTTP yanıt ayrı sınıflara oluşturmak için sık kullanılan mantıksal taşır.
- Yanıt oluşturmak, alt düzey ayrıntıları gizleyerek amacı, NET, denetleyici eylemi sağlar.

**Ihttpactionresult** içeren tek bir yöntem **ExecuteAsync**, zaman uyumsuz olarak oluşturan bir **HttpResponseMessage** örneği.

[!code-csharp[Main](action-results/samples/sample6.cs)]

Bir denetleyici eylemi döndürürse bir **Ihttpactionresult**, Web API'si çağıran **ExecuteAsync** yöntemi oluşturmak için bir **HttpResponseMessage**. Bunu dönüştürür **HttpResponseMessage** içine bir HTTP yanıt iletisi.

İşte basit bir uygulaması **Ihttpactionresult** düz metin yanıtı oluşturur:

[!code-csharp[Main](action-results/samples/sample7.cs)]

Örnek denetleyici eylem:

[!code-csharp[Main](action-results/samples/sample8.cs)]

Yanıt:

[!code-console[Main](action-results/samples/sample9.cmd)]

Daha sık kullanacağınız **Ihttpactionresult** tanımlanan uygulamaları **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** ad alanı. **ApiController** sınıfı, bu yerleşik eylem sonuçları döndüren yardımcı yöntemler tanımlar.

Aşağıdaki örnekte, istek var olan bir ürün kimliği eşleşmiyorsa denetleyicisi çağıran [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 404 (bulunamadı) yanıt oluşturmak için. Aksi takdirde, denetleyiciyi çağıran [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), ürün, 200 (Tamam) bir yanıt oluşturan içerir.

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>Diğer dönüş türleri

Diğer tüm dönüş türleri için Web API'si kullanan bir [medya biçimlendiricisi](../formats-and-model-binding/media-formatters.md) dönüş değeri serileştirmek için. Web API'si, yanıt gövdesine seri hale getirilmiş değer yazar. Yanıt durum kodu 200 (Tamam) ' dir.

[!code-csharp[Main](action-results/samples/sample11.cs)]

Bu yaklaşımın bir dezavantajı, 404 gibi bir hata kodu doğrudan döndüremez ' dir. Ancak, oluşturabilecek bir **HttpResponseException** hata kodları. Daha fazla bilgi için [ASP.NET Web API'de özel durum işleme](../error-handling/exception-handling.md).

Web API'si, biçimlendirici seçmek için istekte Accept üst bilgisi kullanır. Daha fazla bilgi için [içerik anlaşması](../formats-and-model-binding/content-negotiation.md).

Örnek istek

[!code-console[Main](action-results/samples/sample12.cmd)]

Örnek yanıt:

[!code-console[Main](action-results/samples/sample13.cmd)]
