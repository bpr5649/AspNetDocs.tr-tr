---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API'de Yönlendirme | Microsoft Dokümanlar
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676134"
---
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API'sinde yönlendirme

Mike [Wasson](https://github.com/MikeWasson) tarafından

Bu makalede, web API ASP.NET http isteklerini denetleyicilere nasıl yönlendirir.

> [!NOTE]
> MVC ASP.NET aşinaysanız, Web API yönlendirmesi MVC yönlendirmesine çok benzer. Temel fark, Web API'nin eylemi seçmek için URI yolunu değil, HTTP fiilini kullanmasıdır. Web API'de MVC tarzı yönlendirmeyi de kullanabilirsiniz. Bu makalede, ASP.NET MVC herhangi bir bilgi kabul etmez.

## <a name="routing-tables"></a>Yönlendirme Tabloları

Web APIASP.NET denetleyici, HTTP isteklerini işleyen bir *sınıftır.* Denetleyicinin genel *yöntemlerine eylem yöntemleri* veya basitçe *eylemler*denir. Web API çerçevesi bir istek aldığında, isteği bir eyleme yönlendirir.

Hangi eylemi çağıracaklarını belirlemek için, çerçeve bir *yönlendirme tablosu*kullanır. Web API için Visual Studio proje şablonu varsayılan bir rota oluşturur:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Bu yol, *\_App Start* dizinine yerleştirilen *WebApiConfig.cs* dosyasında tanımlanır:

![](routing-in-aspnet-web-api/_static/image1.png)

`WebApiConfig` Sınıf hakkında daha fazla bilgi için, [Web APIASP.NET Yapılandırma'ya](../advanced/configuring-aspnet-web-api.md)bakın.

Web API'sini kendi kendine barındırıyorsanız, yönlendirme tablosunu `HttpSelfHostConfiguration` doğrudan nesnenin üzerine ayarlamanız gerekir. Daha fazla bilgi için, [Bir Web API Self-Host](../older-versions/self-host-a-web-api.md)bakın.

Yönlendirme tablosundaki her giriş bir *rota şablonu*içerir. Web API için varsayılan &quot;rota şablonu api/{controller}/{id}&quot;olur. Bu şablonda &quot;api&quot; gerçek bir yol kesimidir ve {controller} ve {id} yer tutucu değişkenlerdir.

Web API çerçevesi bir HTTP isteği aldığında, URI'yi yönlendirme tablosundaki rota şablonlarından biriyle eşleştirmeye çalışır. Rota eşleşmezse, istemci 404 hatası alır. Örneğin, aşağıdaki URI'ler varsayılan rotayla eşleşir:

- /api/kişiler
- /api/kişiler/1
- /api/ürünler/gizmo1

Ancak, &quot;api&quot; segmenti yoksun olduğundan, aşağıdaki URI eşleşmez:

- /kişiler/1

> [!NOTE]
> Rotada "api" kullanmanın nedeni, ASP.NET MVC yönlendirmesiyle çarpışmaları önlemektir. &quot;Bu şekilde, /kişileri&quot; bir MVC denetleyicisine, &quot;/api/kişiler&quot; bir Web API denetleyicisine gitmenizi sağlayabilirsiniz. Elbette, bu kuralı beğenmezseniz, varsayılan rota tablosunu değiştirebilirsiniz.

Eşleşen bir rota bulunduğunda, Web API denetleyiciyi ve eylemi seçer:

- Denetleyiciyi bulmak için Web &quot;API,&quot; *{controller}* değişkeninin değerine Denetleyici ekler.
- Eylemi bulmak için, Web API HTTP fiiline bakar ve sonra adı bu HTTP fiil adı ile başlayan bir eylem arar. Örneğin, GET isteğiyle, Web API Get &quot;ile önceden&quot;belirlenmiş &quot;bir&quot; eylem &quot;arar&quot;, Örneğin GetContact veya GetAllContacts. Bu sözleşme yalnızca GET, POST, PUT, DELETE, HEAD, OPTIONS ve PATCH fiilleri için geçerlidir. Denetleyicinizdeki öznitelikleri kullanarak diğer HTTP fiillerini etkinleştirebilirsiniz. Bunun bir örneğini daha sonra göreceğiz.
- Rota şablonundaki *{id}* gibi diğer yer tutucu değişkenler eylem parametrelerine eşlenir.

Şimdi örneği inceleyelim. Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Olası BAZı HTTP istekleri ve her biri için çağrılan eylem şunlardır:

| HTTP Fiil | URI Yolu | Eylem | Parametre |
| --- | --- | --- | --- |
| GET | api/ürünler | GetAllÜrünler | *(yok)* |
| GET | api/ürünler/4 | GetProductById | 4 |
| DELETE | api/ürünler/4 | Ürünü Silme | 4 |
| POST | api/ürünler | *(eşleşme yok)* |  |

Varsa URI'nin *{id}* kesiminin eylemin *kimlik* parametresine eşlenediğini unutmayın. Bu örnekte, denetleyici iki GET yöntemi, bir *id* parametresi ve bir parametre ile tanımlar.

Ayrıca, denetleyici bir &quot;Post tanımlamadığından POST isteğinin başarısız olacağını unutmayın... &quot; yöntemini belirtin.

## <a name="routing-variations"></a>Yönlendirme Varyasyonları

Önceki bölümde, ASP.NET Web API için temel yönlendirme mekanizması açıklanmıştır. Bu bölümde bazı varyasyonlar açıklanmaktadır.

### <a name="http-verbs"></a>HTTP fiiller

HTTP fiilleri için adlandırma kuralını kullanmak yerine, eylem yöntemini aşağıdaki özniteliklerden biriyle süsleyerek eylem için HTTP fiilini açıkça belirtebilirsiniz:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

Aşağıdaki örnekte, `FindProduct` yöntem GET istekleri eşlenir:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Bir eylem için birden çok HTTP fiiline izin vermek veya GET, PUT, POST, DELETE, HEAD, `[AcceptVerbs]` OPTIONS ve PATCH dışındaki HTTP fiillerine izin vermek için, HTTP fiillerinin listesini alan özniteliği kullanın.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Eylem Adına Göre Yönlendirme

Varsayılan yönlendirme şablonuyla, Web API eylemi seçmek için HTTP fiilini kullanır. Ancak, eylem adının URI'ye dahil edildiği bir rota da oluşturabilirsiniz:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

Bu yol şablonunda, *{action}* parametresi denetleyicideki eylem yöntemini adlandırır. Bu yönlendirme stiliyle, izin verilen HTTP fiillerini belirtmek için öznitelikleri kullanın. Örneğin, denetleyicinizin aşağıdaki yönteme sahip olduğunu varsayalım:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

Bu durumda, "api/products/details/1" için get isteği `Details` yöntemle eşlenecektir. Bu yönlendirme stili ASP.NET MVC'ye benzer ve RPC tarzı bir API için uygun olabilir.

Özniteliği kullanarak `[ActionName]` eylem adını geçersiz kılabilirsiniz. Aşağıdaki örnekte, api/products/thumbnail/ &quot;*id*ile eşleyen iki eylem vardır. Biri GET'i, diğeri post'u destekler:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Eylem Dışı

Bir yöntemin `[NonAction]` eylem olarak çağrılmasını önlemek için özniteliği kullanın. Bu, yönlendirme kurallarına uyacak olsa bile, yöntemin bir eylem olmadığını çerçeveye bildirir.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu konu yönlendirme nin üst düzey bir görünümünü sağladı. Daha fazla ayrıntı için, çerçevenin URI ile bir rotayla tam olarak nasıl eşleştiğini açıklayan, bir denetleyici seçen ve sonra çağırmak için eylemi seçen [Yönlendirme ve Eylem Seçimi'ne](routing-and-action-selection.md)bakın.
