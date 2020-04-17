---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API ile OData v4'te Açık Türleri | Microsoft Dokümanlar
author: rick-anderson
description: OData v4'te açık tür, tür tanımında bildirilen tüm özelliklere ek olarak dinamik özellikler içeren yapılandırılmış bir türdür. Aç...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543736"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API ile OData v4'te Açık Türleri

[Microsoft](https://github.com/microsoft) tarafından

> OData v4'te *açık tür,* tür tanımında bildirilen tüm özelliklere ek olarak dinamik özellikler içeren yapılandırılmış bir türdür. Açık türler, veri modellerinize esneklik eklemenize izin sağlar. Bu öğretici, ASP.NET Web API OData'da açık türlerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici, ASP.NET Web API'sinde Bir OData bitiş noktası oluşturmayı zaten bildiğinizi varsayar. Değilse, önce [Bir OData v4 Endpoint oluştur'u](create-an-odata-v4-endpoint.md) okuyarak başlayın.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API OData 5.3
> - OData v4

İlk olarak, bazı OData terminolojisi:

- Varlık türü: Anahtarlı yapılandırılmış bir tür.
- Karmaşık tür: Anahtarsız yapılandırılmış bir tür.
- Açık tür: Dinamik özelliklere sahip bir tür. Hem varlık türleri hem de karmaşık türler açık olabilir.

Dinamik bir özelliğin değeri ilkel bir tür, karmaşık tür veya numaralandırma türü olabilir; veya bu türlerden herhangi birinin bir koleksiyonu. Açık türleri hakkında daha fazla bilgi için [OData v4 belirtimine](http://www.odata.org/documentation/odata-version-4-0/)bakın.

## <a name="install-the-web-odata-libraries"></a>Web OData Kitaplıklarını Yükleme

En son Web API OData kitaplıklarını yüklemek için NuGet Paket Yöneticisi'ni kullanın. Paket Yöneticisi Konsolu penceresinden:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR Türlerini Tanımla

EDM modellerini CLR türleri olarak tanımlayarak başlayın.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Varlık Veri Modeli (EDM) oluşturulduğunda,

- `Category`numaralandırma türüdür.
- `Address`karmaşık bir türüdür. (Bir anahtarı yoktur, bu nedenle bir varlık türü değildir.)
- `Customer`bir varlık türüdür. (Bir anahtarı vardır.)
- `Press`açık karmaşık bir türüdür.
- `Book`açık bir varlık türüdür.

Açık bir tür oluşturmak için CLR türüdinamik `IDictionary<string, object>`özellikleri tutan bir tür özelliğine sahip olmalıdır.

## <a name="build-the-edm-model"></a>EDM Modelini Oluşturun

EDM'yi oluşturmak için **ODataConventionModelBuilder** kullanıyorsanız `Press` ve `Book` bir `IDictionary<string, object>` özelliğin varlığına bağlı olarak otomatik olarak açık türler olarak eklenir.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Ayrıca açıkça EDM oluşturabilirsiniz, **ODataModelBuilder**kullanarak.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData Denetleyicisi Ekleme

Ardından, bir OData denetleyicisi ekleyin. Bu öğretici için, yalnızca GET ve POST isteklerini destekleyen ve varlıkları depolamak için bellek içi bir liste kullanan basitleştirilmiş bir denetleyici kullanırız.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

İlk `Book` örneğin dinamik bir özelliği olmadığına dikkat edin. İkinci `Book` örnek aşağıdaki dinamik özelliklere sahiptir:

- "Yayınlandı": İlkel tip
- "Yazarlar": Ilkel türlerin koleksiyonu
- "OtherCategories": Numaralandırma türlerinin toplanması.

Ayrıca, `Press` bu `Book` örneğin özelliği aşağıdaki dinamik özelliklere sahiptir:

- "Blog": İlkel tip
- "Adres": Karmaşık tür

## <a name="query-the-metadata"></a>Meta verileri sorgula

OData meta veri belgesini almak için `~/$metadata`bir GET isteği gönderin. Yanıt gövdesi buna benzer olmalıdır:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Meta veri belgesinden şunları görebilirsiniz:

- Ve türleri için özniteliğin `OpenType` değeri doğrudur. `Press` `Book` `Customer` Ve `Address` türleri bu özniteliğe sahip değildir.
- Varlık `Book` türü, bildirilen üç özelluğa sahiptir: ISBN, Başlık ve Basın. OData meta verileri CLR `Book.Properties` sınıfındaki özelliği içermez.
- Benzer şekilde, `Press` karmaşık türü yalnızca iki bildirilen özellikleri vardır: Ad ve Kategori. Meta veriler CLR `Press.DynamicProperties` sınıfındaki özelliği içermez.

## <a name="query-an-entity"></a>Bir Varlığı Sorgula

"978-0-7356-7942-9" eeşit ISBN ile kitap almak için, `~/Books('978-0-7356-7942-9')`bir GET isteği gönderin . Yanıt gövdesi aşağıdakine benzer olmalıdır. (Girindi daha okunabilir hale getirmek için.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Dinamik özelliklerin bildirilen özelliklere satır satır da dahil olduğuna dikkat edin.

## <a name="post-an-entity"></a>Bir Varlık GÖNDER

Kitap varlığı eklemek için, `~/Books`bir POST isteği gönderin. İstemci istek yükünde dinamik özellikler ayarlayabilir.

Aşağıda bir örnek istek verilmiştir. "Fiyat" ve "Yayınlanmış" özelliklerine dikkat edin.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Denetleyici yönteminde bir kesme noktası ayarlarsanız, Web API'sinin bu `Properties` özellikleri ötmede ekladığını görebilirsiniz.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Ek Kaynaklar

[OData Açık Tip Örneği](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
