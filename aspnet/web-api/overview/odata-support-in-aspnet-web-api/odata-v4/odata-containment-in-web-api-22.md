---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: OData v4 sürümünde kapsama kullanarak Web API 2.2 | Microsoft Docs
author: rick-anderson
description: Geleneksel olarak, bir varlık kümesi içinde kapsüllenmiş, bir varlığın yalnızca erişilemedi. Ancak, OData v4 tekil ve Con olmak üzere iki ek seçenekler sağlar...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: aca263a04df25ca241bc0b9798b3a0b588d4cae8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074919"
---
<a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="814a5-104">OData v4 sürümünde kapsama Web API 2.2 kullanma</span><span class="sxs-lookup"><span data-stu-id="814a5-104">Containment in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="814a5-105">by Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="814a5-105">by Jinfu Tan</span></span>

> <span data-ttu-id="814a5-106">Geleneksel olarak, bir varlık kümesi içinde kapsüllenmiş, bir varlığın yalnızca erişilemedi.</span><span class="sxs-lookup"><span data-stu-id="814a5-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="814a5-107">Ancak, OData v4 tekil ve kapsama, ikisi için de Webapı 2.2 destekleyen iki ek seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="814a5-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="814a5-108">Bu konuda, bir kapsama Webapı 2.2 içinde OData uç noktası tanımlamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="814a5-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="814a5-109">Kapsama hakkında daha fazla bilgi için bkz: [kapsama ile OData v4 yakında](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span><span class="sxs-lookup"><span data-stu-id="814a5-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="814a5-110">Web API'de OData V4 uç nokta oluşturmak için bkz [OData v4 uç noktası kullanarak ASP.NET Web API 2.2 oluşturma](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="814a5-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="814a5-111">İlk olarak, bir kapsama etki alanı modeli OData hizmeti kullanarak bu veri modeli oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="814a5-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![Veri modeli](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="814a5-113">Birçok PaymentInstruments (PI) bir hesap içeriyor, ancak bir varlık kümesini PI sayısı için tanımlarız yok.</span><span class="sxs-lookup"><span data-stu-id="814a5-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="814a5-114">Bunun yerine, yönergelerinin yalnızca bir hesap erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="814a5-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="814a5-115">Bu konu başlığı altında kullanılan çözüm indirebileceğiniz [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span><span class="sxs-lookup"><span data-stu-id="814a5-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="814a5-116">Veri modelini tanımlama</span><span class="sxs-lookup"><span data-stu-id="814a5-116">Defining the data model</span></span>

1. <span data-ttu-id="814a5-117">CLR Türleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="814a5-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="814a5-118">`Contained` Özniteliği kapsama Gezinti özellikleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="814a5-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="814a5-119">CLR türlerine göre EDM modelini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="814a5-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="814a5-120">`ODataConventionModelBuilder` EDM modelini derlenerek işleyecek `Contained` özniteliği için karşılık gelen gezinme özelliğini eklenir.</span><span class="sxs-lookup"><span data-stu-id="814a5-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="814a5-121">Koleksiyon türü, özellik ise bir `GetCount(string NameContains)` işlevi de oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="814a5-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="814a5-122">Oluşturulan meta veriler aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="814a5-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="814a5-123">`ContainsTarget` Özniteliği gezinme özelliğinin bir kapsama olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="814a5-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="814a5-124">İçeren varlık kümesi denetleyicisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="814a5-124">Define the containing entity set controller</span></span>

<span data-ttu-id="814a5-125">Kapsanan varlıkları kendi denetleyici gerekmez; eylemi içeren varlık kümesi denetleyicide tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="814a5-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="814a5-126">Bu örnekte, bir AccountsController, ancak hiçbir PaymentInstrumentsController yoktur.</span><span class="sxs-lookup"><span data-stu-id="814a5-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="814a5-127">OData yolu kesimleri 4 veya daha fazla ise, yalnızca yönlendirmenin çalıştığını gibi öznitelik `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` yukarıdaki denetleyicisindeki.</span><span class="sxs-lookup"><span data-stu-id="814a5-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="814a5-128">Aksi takdirde, hem öznitelik hem de Geleneksel yönlendirme çalışır: Örneğin, `GetPayInPIs(int key)` eşleşen `GET ~/Accounts(1)/PayinPIs`.</span><span class="sxs-lookup"><span data-stu-id="814a5-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="814a5-129">*Bu makalede, özgün içerik sayesinde Hu satılmıştır.*</span><span class="sxs-lookup"><span data-stu-id="814a5-129">*Thanks to Leo Hu for the original content of this article.*</span></span>