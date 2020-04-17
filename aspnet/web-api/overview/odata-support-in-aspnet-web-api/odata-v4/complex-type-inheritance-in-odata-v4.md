---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API ile OData v4'te Karmaşık Tür Devralma | Microsoft Dokümanlar
author: rick-anderson
description: OData v4 belirtimine göre, karmaşık bir tür başka bir karmaşık türden devralınabilir. (Karmaşık bir tür, anahtarı olmayan yapılandırılmış bir türdür.) Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543606"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API ile OData v4'te Karmaşık Tür Devralma

[Microsoft](https://github.com/microsoft) tarafından

> OData v4 [belirtimine](http://www.odata.org/documentation/odata-version-4-0/)göre, karmaşık bir tür başka bir karmaşık türden devralınabilir. (Karmaşık *complex* bir tür, anahtarı olmayan yapılandırılmış bir türdür.) Web API OData 5.3 karmaşık tür devralma destekler.
> 
> Bu konu, karmaşık devralma türlerine sahip bir varlık veri modelinin (EDM) nasıl oluşturulabildiğini gösterir. Kaynak kodun tamamı için [Bkz. OData Complex Türü Devralma Örneği.](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>Model Hiyerarşisi

Karmaşık tür devralmagöstermek için aşağıdaki sınıf hiyerarşisini kullanacağız.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`soyut karmaşık bir türüdür. `Rectangle`, `Triangle`, `Circle` ve türetilen `Shape`karmaşık `RoundRectangle` türleri , `Rectangle`ve türetilmiştir . `Window`bir varlık türüdür ve `Shape` bir örnek içerir.

Bu türleri tanımlayan CLR sınıfları aşağıda verilmiştir.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM Modelini Oluşturun

EDM oluşturmak için, CLR türlerinden kalıtım ilişkileri çıkarımlar **ODataConventionModelBuilder**kullanabilirsiniz.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Ayrıca açıkça EDM oluşturabilirsiniz, **ODataModelBuilder**kullanarak. Bu daha fazla kod alır, ancak EDM üzerinde daha fazla kontrol sağlar.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Bu iki örnek aynı EDM şema oluşturmak.

## <a name="metadata-document"></a>Meta veri belgesi

Burada karmaşık tür devralma gösteren OData meta veri belgesi.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Meta veri belgesinden şunları görebilirsiniz:

- Karmaşık `Shape` türü soyuttur.
- , `Rectangle` `Triangle`ve `Circle` karmaşık türü taban `Shape`türüne sahiptir.
- Türü `RoundRectangle` taban türü `Rectangle`vardır.

## <a name="casting-complex-types"></a>Döküm Karmaşık Türleri

Karmaşık türleri döküm şimdi desteklenir. Örneğin, aşağıdaki sorgu a'dan `Shape` `Rectangle`bir'e

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Yanıt yükü aşağıda veda eder:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
