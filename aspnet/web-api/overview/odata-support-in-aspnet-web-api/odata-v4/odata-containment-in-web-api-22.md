---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2,2 kullanarak OData v4 'da kapsama | Microsoft Docs
author: rick-anderson
description: Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4 iki ek seçenek sunar, tek ve Con...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173010"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2,2 kullanarak OData v4 'de kapsama

Jinfu tan tarafından

> Geleneksel olarak, bir varlığa yalnızca bir varlık kümesi içinde kapsülleniyorsa erişilebilir. Ancak OData v4, her ikisi de hem WebAPI 2,2 ' nin desteklediği iki ek seçenek sunar.

Bu konuda, WebApi 2,2 ' de OData uç noktasında bir kapsama nasıl tanımlanacağı gösterilmektedir. Kapsama hakkında daha fazla bilgi için bkz. [içerme, OData v4 ile geliyor](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/). Web API 'de OData v4 uç noktası oluşturmak için, bkz. [ASP.NET Web apı 2,2 kullanarak OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md).

İlk olarak, bu veri modelini kullanarak OData hizmetinde bir kapsama alanı modeli oluşturacağız:

![Veri modeli](odata-containment-in-web-api-22/_static/image1.png)

Hesap birçok Paymentınstruments (PI) içerir, ancak bir PI için bir varlık kümesi tanımlamadık. Bunun yerine, PSIS 'ye yalnızca bir hesap üzerinden erişilebilir.

Bu konu başlığında kullanılan çözümü [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)adresinden indirebilirsiniz.

## <a name="defining-the-data-model"></a>Veri modeli tanımlama

1. CLR türlerini tanımlayın.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`Özniteliği, içerme gezintisi özellikleri için kullanılır.
2. CLR türlerini temel alan EDM modelini oluşturun.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder` `Contained` Özniteliği karşılık gelen gezinti özelliğine EKLENIRSE, EDM modelinin oluşturulmasını işleymeyecektir. Özellik bir koleksiyon türü ise, bir `GetCount(string NameContains)` işlev de oluşturulacaktır.

    Oluşturulan meta veriler aşağıdaki gibi görünür:

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`Özniteliği, Gezinti özelliğinin bir içerme olduğunu gösterir.

## <a name="define-the-containing-entity-set-controller"></a>İçerilen varlık kümesi denetleyicisini tanımlayın

Kapsanan varlıkların kendi denetleyicisi yok; eylem, kapsayan varlık kümesi denetleyicisinde tanımlanmıştır. Bu örnekte, bir AccountsController vardır ancak Paymentınstrumentscontroller yoktur.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData yolu 4 veya daha fazla `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` kesimdeyse, yukarıdaki denetleyicide olduğu gibi yalnızca öznitelik yönlendirme işe yarar. Aksi halde, özniteliği ve geleneksel yönlendirme işe yarar: Örneğin, `GetPayInPIs(int key)` eşleşir `GET ~/Accounts(1)/PayinPIs` .

*Bu makalenin özgün içeriği için yem hu için teşekkürler.*
