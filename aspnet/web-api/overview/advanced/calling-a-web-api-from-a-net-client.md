---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET Istemcisinden bir Web API 'SI çağırma (C#)-ASP.NET 4. x
author: MikeWasson
description: Bu öğreticide, bir .NET 4. x uygulamasından bir Web API 'sinin nasıl çağrılacağını gösterilmektedir.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172945"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>.NET Istemcisinden Web API 'SI çağırma (C#)

, [Mike, son](https://github.com/MikeWasson) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[Tamamlanmış projeyi indirin](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample). [Yönergeleri indirin](/aspnet/core/tutorials/#how-to-download-a-sample). 

Bu öğreticide, [System .net. http. HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) kullanılarak .NET uygulamasından BIR Web API 'sinin nasıl çağrılacağını gösterir.

Bu öğreticide, aşağıdaki Web API 'sini tüketen bir istemci uygulaması yazılmıştır:

| Eylem | HTTP yöntemi | Göreli URI |
| --- | --- | --- |
| KIMLIĞE göre ürün al | GET | /api/Products/*ID* |
| Yeni ürün oluştur | POST | /api/Products |
| Bir ürünü güncelleştirme | PUT | /api/Products/*ID* |
| Bir ürünü silme | DELETE | /api/Products/*ID* |

Bu API 'yi ASP.NET Web API 'SI ile nasıl uygulayacağınızı öğrenmek için bkz. [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).

Kolaylık olması için, bu öğreticideki istemci uygulaması bir Windows konsol uygulamasıdır. **HttpClient** , Windows Phone ve Windows Mağazası uygulamaları için de desteklenir. Daha fazla bilgi için bkz. [Taşınabilir kitaplıkları kullanarak birden çok platform Için Web API Istemci kodu yazma](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)

**Note:** Temel URL 'Leri ve göreli URI 'Leri sabit kodlanmış değerler olarak geçirirseniz, API 'yi kullanmak için kuralların en az olması gerekir `HttpClient` . `HttpClient.BaseAddress`Özelliği sondaki eğik çizgi () içeren bir adrese ayarlanmalıdır `/` . Örneğin, sabit kodlanmış kaynak URI 'Lerini `HttpClient.GetAsync` yönteme geçirirken önünde eğik çizgi eklemeyin. `Product`Kimliğe göre almak için:

1. Kurmak`client.BaseAddress = new Uri("https://localhost:5001/");`
1. İstek a `Product` . Örneğin, `client.GetAsync<Product>("api/products/4");`.

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>Konsol uygulaması oluşturma

Visual Studio 'da **Httpclientsample** adlı yeni bir Windows konsol uygulaması oluşturun ve aşağıdaki kodu yapıştırın:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

Yukarıdaki kod, tüm istemci uygulamasıdır.

`RunAsync`çalışır ve tamamlanana kadar engeller. Ağ g/ç gerçekleştirdiklerinden, çoğu **HttpClient** yöntemi zaman uyumsuz. Tüm zaman uyumsuz görevler içinde yapılır `RunAsync` . Normalde bir uygulama ana iş parçacığını engellemez, ancak bu uygulama hiçbir etkileşime izin vermez.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>Web API Istemci kitaplıklarını yükler

Web API Istemci kitaplıkları paketini yüklemek için NuGet Paket Yöneticisi 'Ni kullanın.

**Araçlar** menüsünde **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu yazın:

`Install-Package Microsoft.AspNet.WebApi.Client`

Yukarıdaki komut, projeye aşağıdaki NuGet paketlerini ekler:

* Microsoft. AspNet. WebApi. Client
* Newtonsoft.Json

Netmerak Soft. JSON (Json.NET olarak da bilinir), .NET için popüler bir yüksek performanslı JSON çerçevesidir.

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>Model sınıfı ekleme

Sınıfı inceleyin `Product` :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

Bu sınıf, Web API 'SI tarafından kullanılan veri modeliyle eşleşir. Bir uygulama, HTTP yanıtından bir örnek okumak için **HttpClient** kullanabilir `Product` . Uygulamanın seri durumdan çıkarma kodu yazmak zorunda değildir.

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>HttpClient oluşturma ve başlatma

Statik **HttpClient** özelliğini inceleyin:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient** uygulamasının bir kez oluşturulması ve bir uygulamanın ömrü boyunca yeniden kullanılması amaçlanmıştır. Aşağıdaki koşullar, **SocketException** hatalarına neden olabilir:

* İstek başına yeni bir **HttpClient** örneği oluşturuluyor.
* Sunucu ağır yük altında.

Her istek için yeni bir **HttpClient** örneği oluşturulması, kullanılabilir yuvaları tüketebilir.

Aşağıdaki kod, **HttpClient** örneğini başlatır:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

Yukarıdaki kod:

* HTTP istekleri için temel URI 'yi ayarlar. Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin. Sunucu uygulaması için bağlantı noktası kullanılmadığı takdirde uygulama çalışmaz.
* Accept üst bilgisini "Application/JSON" olarak ayarlar. Bu üst bilgiyi ayarlamak, sunucuya verileri JSON biçiminde göndermesini söyler.

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>Kaynak almak için GET isteği gönderme

Aşağıdaki kod, bir ürün için GET isteği gönderir:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**GetAsync** YÖNTEMI http get isteğini gönderir. Yöntem tamamlandığında, HTTP yanıtını içeren bir **HttpResponseMessage** döndürür. Yanıttaki durum kodu bir başarı kodu ise, yanıt gövdesi bir ürünün JSON gösterimini içerir. JSON yükünün bir örneğe serisini kaldırmak için **Readasasync** çağrısı yapın `Product` . Yanıt gövdesi çok büyük olabileceğinden **Readasasync** yöntemi zaman uyumsuzdur.

HTTP yanıtı bir hata kodu içerdiğinde **HttpClient** bir özel durum oluşturmaz. Bunun yerine, durum bir hata kodu ise **IsSuccessStatusCode** özelliği **false 'tur** . HTTP hata kodlarını özel durumlar olarak kabul etmek isterseniz, yanıt nesnesinde [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) öğesini çağırın. `EnsureSuccessStatusCode`durum kodu 200 299 aralığının dışında kalırsa bir özel durum oluşturur &ndash; . **HttpClient** &mdash; , istek zaman aşımına uğrarsa diğer nedenlerle özel durumlar oluşturabilir.

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>Seri durumdan çıkarılacak medya türü Formatlayıcıları

**Readasasync** parametresi olmadan çağrıldığında, yanıt gövdesini okumak için varsayılan *medya formatlayıcıları* kümesini kullanır. Varsayılan biçim JSON, XML ve form-URL kodlamalı verileri destekler.

Varsayılan biçimleri kullanmak yerine, **Readasasync** yöntemine bir formatınters listesi sağlayabilirsiniz.  Özel bir medya türü biçimlendirici varsa, bir biçim listesinin kullanılması yararlı olur:

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

Daha fazla bilgi için bkz. [ASP.NET Web API 2 ' de medya biçimleri](../formats-and-model-binding/media-formatters.md)

## <a name="sending-a-post-request-to-create-a-resource"></a>Kaynak oluşturmak için POST Isteği gönderme

Aşağıdaki kod, JSON biçiminde bir örnek içeren bir POST isteği gönderir `Product` :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**Postasjsonasync** yöntemi:

* Bir nesneyi JSON 'a dizleştirir.
* JSON yükünü bir POST isteğinde gönderir.

İstek başarılı olursa:

* Bu, 201 (oluşturulan) yanıtı döndürmelidir.
* Yanıt, konum üstbilgisindeki oluşturulan kaynakların URL 'sini içermelidir.

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>Bir kaynağı güncelleştirmek için PUT Isteği gönderme

Aşağıdaki kod bir ürünü güncelleştirmek için bir PUT isteği gönderir:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**Putasjsonasync** yöntemi, post yerıne bir PUT isteği göndermesi dışında, **postasjsonasync**yöntemi gibi çalışmaktadır.

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>Bir kaynağı silmek için SILME Isteği gönderme

Aşağıdaki kod, bir ürünü silmek için bir SILME isteği gönderir:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

GET gibi, bir DELETE isteğinin bir istek gövdesi yoktur. DELETE ile JSON veya XML biçimi belirtmeniz gerekmez.

## <a name="test-the-sample"></a>Örneği test etme

İstemci uygulamasını test etmek için:

1. Sunucu uygulamasını [indirip](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) çalıştırın. [Yönergeleri indirin](/aspnet/core/#how-to-download-a-sample). Sunucu uygulamasının çalıştığını doğrulayın. Örneğin, `http://localhost:64195/api/products` ürünlerin bir listesini döndürmelidir.
2. HTTP istekleri için temel URI 'yi ayarlayın. Bağlantı noktası numarasını sunucu uygulamasında kullanılan bağlantı noktasıyla değiştirin.
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. İstemci uygulamasını çalıştırın. Aşağıdaki çıktı üretilir:

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
