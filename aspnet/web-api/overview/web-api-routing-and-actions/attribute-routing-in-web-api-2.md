---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 Öznitelik Yönlendirme | Microsoft Dokümanlar
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675380"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2'de Öznitelik Yönlendirme

Mike [Wasson](https://github.com/MikeWasson) tarafından

*Yönlendirme,* Web API'nin bir EYLEMle URI ile eşleştiğinin şeklidir. Web API 2, *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türünü destekler. Adından da anlaşılacağı gibi, öznitelik yönlendirme yolları tanımlamak için öznitelikleri kullanır. Öznitelik yönlendirme, web API'nizdeki URI'ler üzerinde daha fazla denetim sağlar. Örneğin, kaynak hiyerarşilerini açıklayan UR'leri kolayca oluşturabilirsiniz.

Kongre tabanlı yönlendirme olarak adlandırılan daha önceki yönlendirme stili hala tam olarak desteklenir. Aslında, aynı projede her iki tekniği birleştirebilirsiniz.

Bu konu öznitelik yönlendirmesini nasıl etkinleştireceklerini gösterir ve öznitelik yönlendirmesi için çeşitli seçenekleri açıklar. Öznitelik yönlendirmesini kullanan uçtan uca bir öğretici için [bkz.](create-a-rest-api-with-attribute-routing.md)

## <a name="prerequisites"></a>Ön koşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Topluluk, Profesyonel veya Kurumsal sürüm

Alternatif olarak, gerekli paketleri yüklemek için NuGet Package Manager'ı kullanın. Visual Studio'daki **Araçlar** menüsünden **NuGet Package Manager'ı**seçin, ardından **Paket Yöneticisi Konsolu'nu**seçin. Paket Yöneticisi Konsolu penceresine aşağıdaki komutu girin:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Neden Öznitelik Yönlendirme?

Web API'nin ilk *sürümünde kural tabanlı* yönlendirme kullanılmıştır. Bu yönlendirme türünde, temelde parametrelendirilmiş dizeleri olan bir veya daha fazla rota şablonu tanımlarsınız. Çerçeve bir istek aldığında, uri ile rota şablonuyla eşleşir. Kongre tabanlı yönlendirme hakkında daha fazla bilgi için, [ASP.NET Web API'de Yönlendirme'ye](routing-in-aspnet-web-api.md)bakın.

Kural tabanlı yönlendirmenin bir avantajı, şablonların tek bir yerde tanımlanması ve yönlendirme kurallarının tüm denetleyicilere tutarlı bir şekilde uygulanmasıdır. Ne yazık ki, kongre tabanlı yönlendirme zor RESTful API'larda yaygın olan bazı URI desenleri desteklemek için yapar. Örneğin, kaynaklar genellikle alt kaynaklar içerir: Müşterilerin siparişleri vardır, filmlerin aktörleri vardır, kitapların yazarları vardır, vb. Bu ilişkileri yansıtan URI'ler oluşturmak doğaldır:

`/customers/1/orders`

Uri Bu tür kural tabanlı yönlendirme kullanarak oluşturmak zordur. Yapılsa da, çok sayıda denetleyiciniz veya kaynak türünüz varsa sonuçlar iyi ölçeklendirilmez.

Öznitelik yönlendirmesi ile, bu URI için bir rota tanımlamak için önemsiz. Denetleyici eylemine bir öznitelik eklemeniz yeterlidir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Yönlendirmenin kolaylaştırdığı diğer desenler şunlardır.

**API sürüm**

Bu örnekte, "/api/v1/products" "/api/v2/products" daha farklı bir denetleyiciye yönlendirildirilebilir.

`/api/v1/products`
`/api/v2/products`

**Aşırı yüklenmiş URI segmentleri**

Bu örnekte, "1" bir sipariş numarasıdır, ancak bir koleksiyona "beklemede" eşler.

`/orders/1`
`/orders/pending`

**Birden çok parametre türü**

Bu örnekte, "1" bir sipariş numarasıdır, ancak "2013/06/16" bir tarih belirtir.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Öznitelik Yönlendirmesini Etkinleştirme

Öznitelik yönlendirmesini etkinleştirmek için yapılandırma sırasında **MapHttpAttributeRoutes'u** arayın. Bu uzantı yöntemi **System.Web.Http.HttpConfigurationExtensions** sınıfında tanımlanır.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Öznitelik [yönlendirme, kural tabanlı](routing-in-aspnet-web-api.md) yönlendirme ile birleştirilebilir. Kongre tabanlı rotalar tanımlamak için **MapHttpRoute** yöntemini arayın.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API'yi yapılandırma hakkında daha fazla bilgi için bkz. [ASP.NET Yapılandırma Web API 2.](../advanced/configuring-aspnet-web-api.md)

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Not: Web API'sinden Geçiş 1

Web API 2'den önce, Web API proje şablonları aşağıdaki gibi kod lar oluşturmaktadır:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Öznitelik yönlendirmesi etkinleştirilmişse, bu kod bir özel durum oluşturur. Öznitelik yönlendirmesini kullanmak üzere varolan bir Web API projesini yükseltirseniz, bu yapılandırma kodunu aşağıdakilere güncelleştirmeyi unutmayın:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Daha fazla bilgi için, [web API'yi ASP.NET Barındırma ile Yapılandırma'ya](../advanced/configuring-aspnet-web-api.md#webhost)bakın.

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Rota Öznitelikleri Ekleme

Burada bir öznitelik kullanılarak tanımlanan bir rota örneği verilmiştir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

String &quot;customers/{customerId}/orders,&quot; rota için URI şablonudur. Web API, istek URI'yi şablonla eşleştirmeye çalışır. Bu örnekte, "müşteriler" ve "siparişler" gerçek segmentlerdir ve "{customerId}" değişken bir parametredir. Aşağıdaki URI'ler bu şablonla eşleşir:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Bu konuda daha sonra açıklanan [kısıtlamaları](#constraints)kullanarak eşleştirmeyi kısıtlayabilirsiniz.

Rota şablonundaki &quot;{customerId}&quot; parametresinin yöntemdeki *customerId* parametresinin adıyla eşleştiğini unutmayın. Web API denetleyici eylemini çağırdığında, rota parametrelerini bağlamaya çalışır. Örneğin, URI ise, `http://example.com/customers/1/orders`Web API eylemi *customerId* parametre "1" değerini bağlamaya çalışır.

URI şablonunda çeşitli parametreler olabilir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Rota özniteliği olmayan tüm denetleyici yöntemleri kural tabanlı yönlendirme kullanır. Bu şekilde, aynı projede her iki yönlendirme türünü birleştirebilirsiniz.

## <a name="http-methods"></a>HTTP Yöntemleri

Web API ayrıca isteğin HTTP yöntemine (GET, POST, vb) dayalı eylemleri seçer. Varsayılan olarak, Web API denetleyici yöntemi adının başlangıcı ile bir büyük/küçük harf duyarsız eşleşme arar. Örneğin, adlı `PutCustomers` bir denetleyici yöntemi bir HTTP PUT isteğiyle eşleşir.

Yöntemi aşağıdaki özniteliklerle süsleyerek bu kuralı geçersiz kılabilirsiniz:

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[Seçenekler]**
- **[HttpPatch]**
- **[Posta]**
- **[HttpPut]**

Aşağıdaki örnek, CreateBook yöntemini HTTP POST istekleriyle eşler.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Standart olmayan yöntemler de dahil olmak üzere diğer tüm HTTP yöntemleri için, HTTP yöntemlerinin bir listesini alan **AcceptVerbs** özniteliğini kullanın.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Rota Önekleri

Genellikle, denetleyicideki yolların tümü aynı önek ile başlar. Örneğin:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[RoutePrefix]** özniteliğini kullanarak tüm denetleyici için ortak bir önek ayarlayabilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Rota önekini geçersiz kılmak için yöntem özniteliğiüzerinde bir tilde (~) kullanın:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Rota öneki parametreleri içerebilir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Rota Kısıtlamaları

Rota kısıtlamaları, rota şablonundaki parametrelerin nasıl eşleşip eşleşip eşleştirildiğini kısıtlamanıza izin sağlar. Genel sözdizimi &quot;{parametre:constraint}&quot;'dur. Örneğin:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Burada, ilk rota yalnızca &quot;URI'nin&quot; kimlik bölümü bir sondaysa seçilecektir. Aksi takdirde, ikinci rota seçilir.

Aşağıdaki tabloda desteklenen kısıtlamaları listeler.

| Kısıtlama | Açıklama | Örnek |
| --- | --- | --- |
| alfa | Büyük veya küçük Latin alfabesi karakterleri (a-z, A-Z) eşleşir | {x:alfa} |
| bool | Boolean değeriyle eşleşir. | {x:bool} |
| datetime | **DateTime** değeriyle eşleşir. | {x:datetime} |
| decimal | Ondalık değerle eşleşir. | {x:ondalık} |
| double | 64 bit kayan nokta değeriyle eşleşir. | {x:çift} |
| float | 32 bit kayan nokta değeriyle eşleşir. | {x:float} |
| Guıd | GUID değeriyle eşleşir. | {x:guid} |
| int | 32 bit tamsayı değeriyle eşleşir. | {x:int} |
| length | Bir dize belirtilen uzunlukta veya belirli bir uzunluk aralığında eşleşir. | {x:uzunluk(6)} {x:uzunluk(1,20)} |
| long | 64 bit tamsayı değeriyle eşleşir. | {x:uzun} |
| max | En yüksek değere sahip bir tamsayıyla eşleşir. | {x:max(10)} |
| Maxlength | Bir dize maksimum uzunlukta eşleşir. | {x:maxlength(10)} |
| min | En az değere sahip bir tamsayıyla eşleşir. | {x:min(10)} |
| Minlength | En az uzunlukta bir dize eşleşir. | {x:minlength(10)} |
| aralık | Bir tamsede, çeşitli değerler içinde eşleşir. | {x:aralığı(10,50)} |
| Regex | Normal bir ifadeyle eşleşir. | {x:regex(^\d{3}-\d{3}-\d{4}$)} |

Min &quot;&quot;gibi bazı kısıtlamaların parantez içinde bağımsız değişkenler aldığına dikkat edin. Bir üst nokta ile ayrılmış bir parametreye birden çok kısıtlama uygulayabilirsiniz.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Özel Rota Kısıtlamaları

**IHttpRouteConstraint** arabirimini uygulayarak özel rota kısıtlamaları oluşturabilirsiniz. Örneğin, aşağıdaki kısıtlama bir parametreyi sıfır olmayan bir tamsayı değeriyle sınırlandırmaz.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Aşağıdaki kod kısıtlamanın nasıl kaydedilen gösteriş olduğunu gösterir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Artık kısıtlamaları rotalarınızda uygulayabilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

**Ayrıca IInlineConstraintResolver** arabirimini uygulayarak tüm **DefaultInlineConstraintResolver** sınıfını değiştirebilirsiniz. Bunu yapmak, **IInlineConstraintResolver** uygulamanız özellikle bunları eklmediği sürece, yerleşik kısıtlamaların tümünün yerini alacaktır.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>İsteğe Bağlı URI Parametreleri ve Varsayılan Değerler

Rota parametresine soru işareti ekleyerek URI parametresini isteğe bağlı hale getirebilirsiniz. Bir rota parametresi isteğe bağlıysa, yöntem parametresi için varsayılan değer tanımlamanız gerekir.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

Bu örnekte `/api/books/locale/1033` `/api/books/locale` ve aynı kaynağı döndürün.

Alternatif olarak, rota şablonu içinde aşağıdaki gibi varsayılan bir değer belirtebilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

Bu, önceki örnekle hemen hemen aynıdır, ancak varsayılan değer uygulandığında hafif bir davranış farkı vardır.

- İlk örnekte ("{lcid:int?}"), 1033 varsayılan değeri doğrudan yöntem parametresine atanır, böylece parametre tam olarak bu değere sahip olur.
- İkinci örnekte ("{lcid:int=1033}"), "1033"ün varsayılan değeri model bağlama işleminden geçer. Varsayılan model bağlayıcısı "1033"ü sayısal değer 1033'e dönüştürür. Ancak, farklı bir şey yapabilir özel bir model bağlayıcı, takabilirsiniz.

(Çoğu durumda, ardışık ardışık nızda özel model bağlayıcıları yoksa, iki form eşdeğer olacaktır.)

<a id="route-names"></a>
## <a name="route-names"></a>Rota Adları

Web API'sinde her rotanın bir adı vardır. Rota adları, http yanıtına bir bağlantı ekleyebilmeniz için bağlantı oluşturmak için yararlıdır.

Rota adını belirtmek için, öznitelik üzerinde **Ad** özelliğini ayarlayın. Aşağıdaki örnek, rota adının nasıl ayarlanır ve bağlantı oluştururken rota adının nasıl kullanılacağını gösterir.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Rota Siparişi

Çerçeve bir URI'yi bir rotayla eşleştirmeye çalıştığında, yolları belirli bir sırada değerlendirir. Siparişi belirtmek için, rota özniteliği üzerinde **Sipariş** özelliğini ayarlayın. Önce daha düşük değerler değerlendirilir. Varsayılan sipariş değeri sıfırdır.

Toplam sıralama nın nasıl belirlendiği aşağıda açıklanmıştır:

1. Rota özniteliğinin **Sipariş** özelliğini karşılaştırın.
2. Rota şablonundaki her URI bölümüne bakın. Her kesim için aşağıdaki gibi sipariş:

    1. Gerçek bölümler.
    2. Kısıtlarla rota parametreleri.
    3. Kısıtlama olmadan rota parametreleri.
    4. Joker karakter parametresi kısıtlamaları içeren segmentler.
    5. Joker karakter parametresi kısıtlama olmadan segmentler.
3. Bir kravat durumunda, rotalar rota şablonunun duyarsız bir ordinal dize karşılaştırması[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)tarafından sıralanır.

Aşağıda bir örnek vardır. Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Bu güzergahlar aşağıdaki gibi sıralanır.

1. siparişler/ayrıntılar
2. siparişler/{id}
3. siparişler/{customerName}
4. siparişler/{\*tarih}
5. siparişler/beklemede

"Ayrıntılar"ın gerçek bir kesim olduğuna ve "{id}" harfinin önünde göründüğüne, ancak **Sipariş** özelliği 1 olduğundan "beklemede" olarak en son göründüğüne dikkat edin. (Bu örnek, "ayrıntılar" veya "beklemede" adlı müşteri olmadığını varsayar. Genel olarak, belirsiz yolları önlemek için deneyin. Bu örnekte, daha iyi `GetByCustomer` bir rota şablonu için "customers/{customerName}" (
