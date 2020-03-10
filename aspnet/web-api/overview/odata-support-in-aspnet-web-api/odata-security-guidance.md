---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData-ASP.NET 4. x için Güvenlik Kılavuzu
author: MikeWasson
description: ASP.NET 4. x üzerinde ASP.NET Web API 2 için OData aracılığıyla bir veri kümesini kullanıma alırken dikkate alınması gereken güvenlik sorunlarını açıklar.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556499"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="c0d54-103">ASP.NET Web API 2 OData için Güvenlik Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="c0d54-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="c0d54-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c0d54-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c0d54-105">Bu konuda, ASP.NET 4. x üzerinde ASP.NET Web API 2 için OData aracılığıyla bir veri kümesini kullanıma alırken göz önünde bulundurmanız gereken bazı güvenlik sorunları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="c0d54-106">EDM güvenliği</span><span class="sxs-lookup"><span data-stu-id="c0d54-106">EDM Security</span></span>

<span data-ttu-id="c0d54-107">Sorgu semantiği, temel alınan model türlerine değil, varlık veri modeli (EDM) tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="c0d54-108">EDM öğesinden bir özelliği hariç tutabilir ve sorgu görünür olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="c0d54-109">Örneğin, modelinize bir maaş özelliği olan bir çalışan türü içerdiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c0d54-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="c0d54-110">Bu özelliği, istemcilerinden gizlemek için EDM 'ten dışlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d54-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="c0d54-111">EDM 'ten bir özelliği dışmanın iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="c0d54-112">**[Ignoredatamember]** özniteliğini model sınıfındaki özellikte ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0d54-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="c0d54-113">Ayrıca, özelliği EDM aracılığıyla program aracılığıyla da kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0d54-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="c0d54-114">Sorgu güvenliği</span><span class="sxs-lookup"><span data-stu-id="c0d54-114">Query Security</span></span>

<span data-ttu-id="c0d54-115">Kötü amaçlı veya Naïve istemcisi, yürütülmesi çok uzun süren bir sorgu oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="c0d54-116">En kötü durumda, bu, hizmetinize erişimi kesintiye uğratabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="c0d54-117">**[Queryable]** özniteliği sorguyu ayrıştırır, doğrular ve uygular bir eylem filtresidir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="c0d54-118">Filtre, sorgu seçeneklerini bir LINQ ifadesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c0d54-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="c0d54-119">OData denetleyicisi bir **IQueryable** türü döndürdüğünde, **IQueryable** LINQ sağlayıcısı LINQ ifadesini bir sorguya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c0d54-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="c0d54-120">Bu nedenle, performans kullanılan LINQ sağlayıcısına ve ayrıca veri kümenizin veya veritabanı şemanızın belirli özelliklerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="c0d54-121">ASP.NET Web API 'sinde OData sorgu seçeneklerini kullanma hakkında daha fazla bilgi için bkz. [OData sorgu seçeneklerini destekleme](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="c0d54-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="c0d54-122">Tüm istemcilerin güvenilir olduğunu (örneğin, bir kurumsal ortamda) biliyorsanız veya veri kümeniz küçükse, sorgu performansı bir sorun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="c0d54-123">Aksi takdirde, aşağıdaki önerileri göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="c0d54-124">Farklı sorgularla hizmetinizi test edin ve DB 'yi profili yapın.</span><span class="sxs-lookup"><span data-stu-id="c0d54-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="c0d54-125">Tek bir sorguda büyük bir veri kümesi döndürmeyi önlemek için sunucu odaklı sayfalama özelliğini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0d54-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="c0d54-126">Daha fazla bilgi için bkz. [sunucu odaklı sayfalama](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="c0d54-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="c0d54-127">$Filter ve $orderby gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="c0d54-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="c0d54-128">Bazı uygulamalar $top ve $skip kullanarak istemci disk belleğine izin verebilir, ancak diğer sorgu seçeneklerini devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="c0d54-129">$Orderby kümelenmiş dizindeki özelliklerle kısıtlamayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c0d54-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="c0d54-130">Büyük verileri kümelenmiş dizin olmadan sıralama yavaş olur.</span><span class="sxs-lookup"><span data-stu-id="c0d54-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="c0d54-131">Maksimum düğüm sayısı: **[sorgulanabilir]** üzerindeki **MaxNodeCount** özelliği, $Filter sözdizimi ağacında izin verilen en fazla düğüm sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c0d54-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="c0d54-132">Varsayılan değer 100 ' dir, ancak daha düşük bir değer ayarlamak isteyebilirsiniz, çünkü çok sayıda düğüm derlemek için yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="c0d54-133">Bu, özellikle bir ara LINQ sağlayıcısı kullanmadan LINQ to Objects (örneğin, bellekte bir koleksiyonda LINQ sorguları) kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="c0d54-134">Herhangi bir () ve tüm () işlevlerini devre dışı bırakmayı düşünün, çünkü bunlar yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="c0d54-135">Herhangi bir dize özelliği örneğin, büyük&#8212;dizeler içeriyorsa, bir ürün açıklaması veya blog girdisi&#8212;dize işlevlerini devre dışı bırakmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c0d54-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="c0d54-136">Gezinti özelliklerinde filtrelemeye izin vermeme seçeneğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c0d54-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="c0d54-137">Gezinme özelliklerine filtre uygulamak, veritabanı şemanıza bağlı olarak yavaş olabilecek bir birleşime yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="c0d54-138">Aşağıdaki kod, gezinti özelliklerinin filtrelenmesini önleyen bir sorgu doğrulayıcısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="c0d54-139">Sorgu Doğrulayıcıları hakkında daha fazla bilgi için bkz. [sorgu doğrulaması](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="c0d54-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="c0d54-140">Veritabanınız için özelleştirilmiş bir doğrulayıcı yazarak $filter sorguları kısıtlamayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c0d54-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="c0d54-141">Örneğin, bu iki sorguyu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c0d54-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="c0d54-142">Son adı ' A ' ile başlayan aktörlere sahip tüm filmler.</span><span class="sxs-lookup"><span data-stu-id="c0d54-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="c0d54-143">1994 içinde yayınlanan tüm filmler.</span><span class="sxs-lookup"><span data-stu-id="c0d54-143">All movies released in 1994.</span></span>

    <span data-ttu-id="c0d54-144">Filmler aktörlere göre dizinlenmediği takdirde, ilk sorgu DB altyapısının tüm film listesini taramasını gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="c0d54-145">İkinci sorgu kabul edilebilir olabilir, ancak film yayın yılı tarafından dizine alınır.</span><span class="sxs-lookup"><span data-stu-id="c0d54-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="c0d54-146">Aşağıdaki kod, "ReleaseYear" ve "title" özelliklerinde filtrelemeye izin veren ancak başka hiçbir özellik bulunmayan bir doğrulayıcısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0d54-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="c0d54-147">Genel olarak, hangi $filter işlevleri gerektiğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c0d54-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="c0d54-148">İstemcileriniz $filter tam ifade etmek gerekmiyorsa, izin verilen işlevleri sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d54-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
