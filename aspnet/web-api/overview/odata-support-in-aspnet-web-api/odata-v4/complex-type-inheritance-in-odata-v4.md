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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="8c344-104">ASP.NET Web API ile OData v4'te Karmaşık Tür Devralma</span><span class="sxs-lookup"><span data-stu-id="8c344-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="8c344-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="8c344-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8c344-106">OData v4 [belirtimine](http://www.odata.org/documentation/odata-version-4-0/)göre, karmaşık bir tür başka bir karmaşık türden devralınabilir.</span><span class="sxs-lookup"><span data-stu-id="8c344-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="8c344-107">(Karmaşık *complex* bir tür, anahtarı olmayan yapılandırılmış bir türdür.) Web API OData 5.3 karmaşık tür devralma destekler.</span><span class="sxs-lookup"><span data-stu-id="8c344-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="8c344-108">Bu konu, karmaşık devralma türlerine sahip bir varlık veri modelinin (EDM) nasıl oluşturulabildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8c344-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="8c344-109">Kaynak kodun tamamı için [Bkz. OData Complex Türü Devralma Örneği.](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="8c344-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8c344-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="8c344-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8c344-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="8c344-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="8c344-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="8c344-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="8c344-113">Model Hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="8c344-113">Model Hierarchy</span></span>

<span data-ttu-id="8c344-114">Karmaşık tür devralmagöstermek için aşağıdaki sınıf hiyerarşisini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8c344-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="8c344-115">`Shape`soyut karmaşık bir türüdür.</span><span class="sxs-lookup"><span data-stu-id="8c344-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="8c344-116">`Rectangle`, `Triangle`, `Circle` ve türetilen `Shape`karmaşık `RoundRectangle` türleri , `Rectangle`ve türetilmiştir .</span><span class="sxs-lookup"><span data-stu-id="8c344-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="8c344-117">`Window`bir varlık türüdür ve `Shape` bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="8c344-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="8c344-118">Bu türleri tanımlayan CLR sınıfları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8c344-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="8c344-119">EDM Modelini Oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c344-119">Build the EDM Model</span></span>

<span data-ttu-id="8c344-120">EDM oluşturmak için, CLR türlerinden kalıtım ilişkileri çıkarımlar **ODataConventionModelBuilder**kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c344-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="8c344-121">Ayrıca açıkça EDM oluşturabilirsiniz, **ODataModelBuilder**kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8c344-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="8c344-122">Bu daha fazla kod alır, ancak EDM üzerinde daha fazla kontrol sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c344-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="8c344-123">Bu iki örnek aynı EDM şema oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="8c344-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="8c344-124">Meta veri belgesi</span><span class="sxs-lookup"><span data-stu-id="8c344-124">Metadata Document</span></span>

<span data-ttu-id="8c344-125">Burada karmaşık tür devralma gösteren OData meta veri belgesi.</span><span class="sxs-lookup"><span data-stu-id="8c344-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="8c344-126">Meta veri belgesinden şunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8c344-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="8c344-127">Karmaşık `Shape` türü soyuttur.</span><span class="sxs-lookup"><span data-stu-id="8c344-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="8c344-128">, `Rectangle` `Triangle`ve `Circle` karmaşık türü taban `Shape`türüne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8c344-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="8c344-129">Türü `RoundRectangle` taban türü `Rectangle`vardır.</span><span class="sxs-lookup"><span data-stu-id="8c344-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="8c344-130">Döküm Karmaşık Türleri</span><span class="sxs-lookup"><span data-stu-id="8c344-130">Casting Complex Types</span></span>

<span data-ttu-id="8c344-131">Karmaşık türleri döküm şimdi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8c344-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="8c344-132">Örneğin, aşağıdaki sorgu a'dan `Shape` `Rectangle`bir'e</span><span class="sxs-lookup"><span data-stu-id="8c344-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="8c344-133">Yanıt yükü aşağıda veda eder:</span><span class="sxs-lookup"><span data-stu-id="8c344-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
