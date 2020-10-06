---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2 ' de OData sorgu seçeneklerini destekleme-ASP.NET 4. x
author: MikeWasson
description: Kod örneklerine genel bakış, ASP.NET 4. x için ASP.NET Web API 2 ' deki desteklenen OData sorgu seçeneklerini gösterir.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188649"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="bccd6-103">ASP.NET Web API 2 ' de OData sorgu seçeneklerini destekleme</span><span class="sxs-lookup"><span data-stu-id="bccd6-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="bccd6-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bccd6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bccd6-105">Kod örnekleri ile bu genel bakış, ASP.NET 4. x için ASP.NET Web API 2 ' deki desteklenen OData sorgu seçeneklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="bccd6-106">OData, bir OData sorgusunu değiştirmek için kullanılabilecek parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="bccd6-107">İstemci bu parametreleri istek URI 'sinin sorgu dizesinde gönderir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="bccd6-108">Örneğin, sonuçları sıralamak için bir istemci $orderby parametresini kullanır:</span><span class="sxs-lookup"><span data-stu-id="bccd6-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="bccd6-109">OData belirtimi Bu parametre *sorgu seçeneklerini*çağırır.</span><span class="sxs-lookup"><span data-stu-id="bccd6-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="bccd6-110">Projenizdeki herhangi bir Web API denetleyicisi için OData sorgu seçeneklerini etkinleştirebilir &#8212; denetleyicinin bir OData uç noktası olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bccd6-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="bccd6-111">Bu, herhangi bir Web API uygulamasına filtreleme ve sıralama gibi özellikleri eklemenin kolay bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="bccd6-112">Sorgu seçeneklerini etkinleştirmeden önce lütfen [OData Güvenlik Kılavuzu](odata-security-guidance.md)konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="bccd6-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="bccd6-113">OData sorgu seçeneklerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bccd6-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="bccd6-114">Örnek sorgular</span><span class="sxs-lookup"><span data-stu-id="bccd6-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="bccd6-115">Sunucu odaklı sayfalama</span><span class="sxs-lookup"><span data-stu-id="bccd6-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="bccd6-116">Sorgu seçeneklerini sınırlama</span><span class="sxs-lookup"><span data-stu-id="bccd6-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="bccd6-117">Sorgu seçenekleri doğrudan çağrılıyor</span><span class="sxs-lookup"><span data-stu-id="bccd6-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="bccd6-118">Sorgu doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bccd6-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="bccd6-119">OData sorgu seçeneklerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bccd6-119">Enabling OData Query Options</span></span>

<span data-ttu-id="bccd6-120">Web API 'SI aşağıdaki OData sorgu seçeneklerini destekler:</span><span class="sxs-lookup"><span data-stu-id="bccd6-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="bccd6-121">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bccd6-121">Option</span></span> | <span data-ttu-id="bccd6-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bccd6-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bccd6-123">$expand</span><span class="sxs-lookup"><span data-stu-id="bccd6-123">$expand</span></span> | <span data-ttu-id="bccd6-124">İlgili varlıkları satır içi genişletir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="bccd6-125">$filter</span><span class="sxs-lookup"><span data-stu-id="bccd6-125">$filter</span></span> | <span data-ttu-id="bccd6-126">Sonuçları Boole koşuluna göre filtreler.</span><span class="sxs-lookup"><span data-stu-id="bccd6-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="bccd6-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="bccd6-127">$inlinecount</span></span> | <span data-ttu-id="bccd6-128">Sunucuya, yanıttaki eşleşen varlıkların toplam sayısını içermesini söyler.</span><span class="sxs-lookup"><span data-stu-id="bccd6-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="bccd6-129">(Sunucu tarafı sayfalama için kullanışlıdır.)</span><span class="sxs-lookup"><span data-stu-id="bccd6-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="bccd6-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="bccd6-130">$orderby</span></span> | <span data-ttu-id="bccd6-131">Sonuçları sıralar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-131">Sorts the results.</span></span> |
| <span data-ttu-id="bccd6-132">$select</span><span class="sxs-lookup"><span data-stu-id="bccd6-132">$select</span></span> | <span data-ttu-id="bccd6-133">Yanıta hangi özelliklerin ekleneceğini seçer.</span><span class="sxs-lookup"><span data-stu-id="bccd6-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="bccd6-134">$skip</span><span class="sxs-lookup"><span data-stu-id="bccd6-134">$skip</span></span> | <span data-ttu-id="bccd6-135">İlk n sonucu atlar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-135">Skips the first n results.</span></span> |
| <span data-ttu-id="bccd6-136">$top</span><span class="sxs-lookup"><span data-stu-id="bccd6-136">$top</span></span> | <span data-ttu-id="bccd6-137">Sonuçları yalnızca ilk n sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="bccd6-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="bccd6-138">OData sorgu seçeneklerini kullanmak için bunları açıkça etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="bccd6-139">Uygulamayı tüm uygulama için küresel olarak etkinleştirebilir veya belirli denetleyiciler veya belirli eylemler için etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="bccd6-140">OData sorgu seçeneklerini küresel olarak etkinleştirmek için, başlangıç sırasında **HttpConfiguration** sınıfında **EnableQuerySupport** ' u çağırın:</span><span class="sxs-lookup"><span data-stu-id="bccd6-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="bccd6-141">**EnableQuerySupport** yöntemi bir **IQueryable** türü döndüren herhangi bir denetleyici eylemi için genel olarak sorgu seçeneklerini sunar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="bccd6-142">Sorgu seçeneklerinin tüm uygulama için etkinleştirilmesini istemiyorsanız, eylem yöntemine **[Queryable]** özniteliğini ekleyerek belirli denetleyici eylemleri için bunları etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="bccd6-143">Örnek Sorgular</span><span class="sxs-lookup"><span data-stu-id="bccd6-143">Example Queries</span></span>

<span data-ttu-id="bccd6-144">Bu bölümde, OData sorgu seçenekleri kullanılarak mümkün olan sorgu türleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="bccd6-145">Sorgu seçenekleri hakkında ayrıntılı bilgi için [www.OData.org](http://www.odata.org/)adresindeki OData belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="bccd6-146">$Expand ve $select hakkında daha fazla bilgi için bkz. [ASP.NET Web API OData içinde $SELECT, $expand ve $value kullanma](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="bccd6-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="bccd6-147">**İstemci odaklı disk belleği**</span><span class="sxs-lookup"><span data-stu-id="bccd6-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="bccd6-148">Büyük varlık kümelerinde istemci, sonuçların sayısını sınırlamak isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="bccd6-149">Örneğin, bir istemci bir sonraki sonuç sayfasını almak için "ileri" bağlantıları ile her seferinde 10 giriş gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="bccd6-150">Bunu yapmak için, istemci $top ve $skip seçeneklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="bccd6-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="bccd6-151">$Top seçeneği döndürülecek en fazla girdi sayısını verir ve $skip seçeneği, atlanacak girdi sayısını verir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="bccd6-152">Önceki örnek, girdileri 21 ile 30 arasında getirir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="bccd6-153">**Filtreleme**</span><span class="sxs-lookup"><span data-stu-id="bccd6-153">**Filtering**</span></span>

<span data-ttu-id="bccd6-154">$Filter seçeneği, bir istemcinin Boole ifadesi uygulayarak sonuçları filtrelemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="bccd6-155">Filtre ifadeleri oldukça güçlüdür; mantıksal ve aritmetik işleçler, dize işlevleri ve Tarih işlevleri içerirler.</span><span class="sxs-lookup"><span data-stu-id="bccd6-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="bccd6-156">Kategori "Toys" değerine eşit olan tüm ürünleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bccd6-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="bccd6-157">`http://localhost/Products?$filter=Category` EQ ' Toys '</span><span class="sxs-lookup"><span data-stu-id="bccd6-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="bccd6-158">Fiyatı 10 ' dan küçük olan tüm ürünleri döndürün.</span><span class="sxs-lookup"><span data-stu-id="bccd6-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="bccd6-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="bccd6-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="bccd6-160">Mantıksal işleçler: Price >= 5 ve Price <= 15 olan tüm ürünleri döndürün.</span><span class="sxs-lookup"><span data-stu-id="bccd6-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="bccd6-161">`http://localhost/Products?$filter=Price` GE 5 ve fiyat Le 15</span><span class="sxs-lookup"><span data-stu-id="bccd6-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="bccd6-162">Dize işlevleri: adında "ZZ" olan tüm ürünleri döndürün.</span><span class="sxs-lookup"><span data-stu-id="bccd6-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="bccd6-163">Tarih işlevleri: 2005 sonrasında ReleaseDate ile tüm ürünleri döndürün.</span><span class="sxs-lookup"><span data-stu-id="bccd6-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="bccd6-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="bccd6-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="bccd6-165">**Sıralama**</span><span class="sxs-lookup"><span data-stu-id="bccd6-165">**Sorting**</span></span>

<span data-ttu-id="bccd6-166">Sonuçları sıralamak için $orderby filtresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="bccd6-167">Fiyata göre sıralayın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="bccd6-168">Fiyata göre azalan sırada sıralayın (en yüksek-en düşük).</span><span class="sxs-lookup"><span data-stu-id="bccd6-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="bccd6-169">Kategoriye göre sıralayın ve ardından kategoriler içinde azalan sırada fiyata göre sıralayın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="bccd6-170">Sunucu odaklı sayfalama</span><span class="sxs-lookup"><span data-stu-id="bccd6-170">Server-Driven Paging</span></span>

<span data-ttu-id="bccd6-171">Veritabanınız milyonlarca kayıt içeriyorsa, bunların tümünü tek bir yükte göndermek istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="bccd6-172">Bunu engellemek için sunucu tek bir yanıtta gönderdiği giriş sayısını sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="bccd6-173">Sunucu Sayfalamayı etkinleştirmek için, **sorgulanabilir** özniteliğinde **PageSize** özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="bccd6-174">Değer döndürülecek en fazla girdi sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="bccd6-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="bccd6-175">Denetleyiciniz OData biçimi döndürürse, yanıt gövdesi sonraki veri sayfasına bir bağlantı içerir:</span><span class="sxs-lookup"><span data-stu-id="bccd6-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="bccd6-176">İstemci bu bağlantıyı bir sonraki sayfayı getirmek için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="bccd6-177">Sonuç kümesindeki toplam giriş sayısını öğrenmek için, istemci $inlinecount sorgu seçeneğini "AllPages" değeriyle ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="bccd6-178">"AllPages" değeri, sunucuya yanıttaki toplam sayıyı dahil etmek için şunu söyler:</span><span class="sxs-lookup"><span data-stu-id="bccd6-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="bccd6-179">Sonraki sayfa bağlantıları ve satır içi sayısı her ikisi de OData biçimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="bccd6-180">Bunun nedeni, OData 'in bağlantıyı ve saymayı tutmak için yanıt gövdesinde özel alanlar tanımlamasının nedenidir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="bccd6-181">OData olmayan biçimler için, sorgu sonuçlarını bir \*\*PageResult &lt; &gt; \*\* nesnesine sarmalayarak, sonraki sayfa bağlantılarını ve satır içi sayıyı desteklemek yine de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="bccd6-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="bccd6-182">Ancak, biraz daha fazla kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-182">However, it requires a bit more code.</span></span> <span data-ttu-id="bccd6-183">Aşağıda bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bccd6-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="bccd6-184">Örnek bir JSON yanıtı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bccd6-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="bccd6-185">Sorgu seçeneklerini sınırlama</span><span class="sxs-lookup"><span data-stu-id="bccd6-185">Limiting the Query Options</span></span>

<span data-ttu-id="bccd6-186">Sorgu seçenekleri istemciye sunucusunda çalıştırılan sorgu üzerinde çok fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bccd6-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="bccd6-187">Bazı durumlarda, güvenlik veya performans nedenleriyle kullanılabilir seçenekleri sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="bccd6-188">**[Queryable]** özniteliğinde bunun için bazı yerleşik özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="bccd6-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="bccd6-189">Aşağıda bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-189">Here are some examples.</span></span>

<span data-ttu-id="bccd6-190">Yalnızca $skip ve $top, sayfalamayı desteklemeye ve başka hiçbir şey yapmasına izin ver:</span><span class="sxs-lookup"><span data-stu-id="bccd6-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="bccd6-191">Veritabanında dizinlenmemiş özelliklerde sıralamayı engellemek için yalnızca belirli özelliklere göre sıralamaya izin ver:</span><span class="sxs-lookup"><span data-stu-id="bccd6-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="bccd6-192">"EQ" mantıksal işlevine izin verin, ancak başka mantıksal işlevler yoktur:</span><span class="sxs-lookup"><span data-stu-id="bccd6-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="bccd6-193">Aritmetik işleçlere izin vermeyin:</span><span class="sxs-lookup"><span data-stu-id="bccd6-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="bccd6-194">Bir **QueryableAttribute** örneği oluşturarak ve bunu **EnableQuerySupport** işlevine geçirerek, seçenekleri küresel olarak kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bccd6-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="bccd6-195">Sorgu seçenekleri doğrudan çağrılıyor</span><span class="sxs-lookup"><span data-stu-id="bccd6-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="bccd6-196">**[Sorgulanabilir]** özniteliğini kullanmak yerine, doğrudan denetleyicinizde sorgu seçeneklerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="bccd6-197">Bunu yapmak için, Controller yöntemine bir **ODataQueryOptions** parametresi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bccd6-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="bccd6-198">Bu durumda, **[Queryable]** özniteliğine ihtiyacınız yoktur.</span><span class="sxs-lookup"><span data-stu-id="bccd6-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="bccd6-199">Web API 'si, **ODataQueryOptions** 'ı URI sorgu dizesinden doldurur.</span><span class="sxs-lookup"><span data-stu-id="bccd6-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="bccd6-200">Sorguyu uygulamak için **ApplyTo** yöntemine bir **IQueryable** geçirin.</span><span class="sxs-lookup"><span data-stu-id="bccd6-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="bccd6-201">Yöntemi başka bir **IQueryable**döndürür.</span><span class="sxs-lookup"><span data-stu-id="bccd6-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="bccd6-202">Gelişmiş senaryolar için, bir **IQueryable** sorgu sağlayıcınız yoksa, **ODataQueryOptions** öğesini inceleyebilir ve sorgu seçeneklerini başka bir forma çevirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="bccd6-203">(Örneğin, bkz. ıghurhar Naazaltı 'ın Web günlüğü gönderisi, [OData sorgularını HQL 'ye çevirerek](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)bir [örnek](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)de içerir.)</span><span class="sxs-lookup"><span data-stu-id="bccd6-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="bccd6-204">Sorgu doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bccd6-204">Query Validation</span></span>

<span data-ttu-id="bccd6-205">**[Queryable]** özniteliği yürütmeden önce sorguyu doğrular.</span><span class="sxs-lookup"><span data-stu-id="bccd6-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="bccd6-206">Doğrulama adımı **QueryableAttribute. ValidateQuery** yönteminde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bccd6-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="bccd6-207">Doğrulama işlemini de özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bccd6-207">You can also customize the validation process.</span></span>

<span data-ttu-id="bccd6-208">Ayrıca bkz. [OData Güvenlik Kılavuzu](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="bccd6-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="bccd6-209">İlk olarak, **Web. http. OData. Query. doğrulayıcılar** ad alanında tanımlanan Doğrulayıcı sınıflarından birini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="bccd6-210">Örneğin, aşağıdaki Doğrulayıcı sınıfı $orderby seçeneği için ' DESC ' seçeneğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="bccd6-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="bccd6-211">**Validatequery** yöntemini geçersiz kılmak Için **[Queryable]** özniteliğini alt sınıf yapın.</span><span class="sxs-lookup"><span data-stu-id="bccd6-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="bccd6-212">Ardından özel öznitelerinizi genel olarak veya denetleyiciden göre ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="bccd6-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="bccd6-213">**ODataQueryOptions** ' ı doğrudan kullanıyorsanız, seçenekler üzerinde doğrulayıcısı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="bccd6-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
