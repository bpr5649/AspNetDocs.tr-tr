---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API ile OData v4 sürümünde açık türler | Microsoft Docs
author: microsoft
description: OData v4 sürümünde açık bir tür ek tür tanımında bildirilen herhangi bir özelliği olarak dinamik özellikleri içeren bir stuctured türüdür. Aç...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 77771d85532b8b622c2ad4ca219a38990e474c9c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071415"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="6fc70-104">ASP.NET Web API ile OData v4 sürümünde türleri açın</span><span class="sxs-lookup"><span data-stu-id="6fc70-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="6fc70-105">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6fc70-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6fc70-106">OData v4 sürümünde bir *açık tür* ek tür tanımında bildirilen herhangi bir özelliği olarak dinamik özellikleri içeren bir stuctured türüdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="6fc70-107">Açık türler, veri modelleri için esneklik eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fc70-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="6fc70-108">Bu öğreticide, ASP.NET Web API OData açık türler kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6fc70-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="6fc70-109">Bu öğreticide, ASP.NET Web API OData uç noktası oluşturma bildiğiniz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="6fc70-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="6fc70-110">Aksi takdirde, okuyarak başlamanız [bir OData v4 uç noktası oluşturma](create-an-odata-v4-endpoint.md) ilk.</span><span class="sxs-lookup"><span data-stu-id="6fc70-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6fc70-111">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="6fc70-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6fc70-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="6fc70-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="6fc70-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="6fc70-113">OData v4</span></span>


<span data-ttu-id="6fc70-114">İlk olarak, bazı OData terimler:</span><span class="sxs-lookup"><span data-stu-id="6fc70-114">First, some OData terminology:</span></span>

- <span data-ttu-id="6fc70-115">Varlık türü: Bir anahtar ile yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="6fc70-116">Karmaşık tür: Bir anahtar olmadan yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="6fc70-117">Açık tür: Dinamik özelliklere sahip bir tür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="6fc70-118">Hem varlık türlerinde ve karmaşık türler, açık olabilir.</span><span class="sxs-lookup"><span data-stu-id="6fc70-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="6fc70-119">Dinamik özelliğinin değeri, bir basit tür, karmaşık tür veya numaralandırma türü olabilir; veya bu türlerinden herhangi birinin bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="6fc70-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="6fc70-120">Açık türler hakkında daha fazla bilgi için bkz: [OData v4 belirtimi](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="6fc70-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="6fc70-121">Web OData kitaplıklarını yükleme</span><span class="sxs-lookup"><span data-stu-id="6fc70-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="6fc70-122">NuGet paketi en son Web API OData kitaplıklarını yüklemek için Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fc70-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="6fc70-123">Paket Yöneticisi konsol penceresinden:</span><span class="sxs-lookup"><span data-stu-id="6fc70-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="6fc70-124">CLR türlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6fc70-124">Define the CLR Types</span></span>

<span data-ttu-id="6fc70-125">EDM modeli CLR türleri olarak tanımlayarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="6fc70-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="6fc70-126">Varlık veri modeli (EDM) oluşturulduğunda</span><span class="sxs-lookup"><span data-stu-id="6fc70-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="6fc70-127">`Category` bir sabit listesi türüdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="6fc70-128">`Address` karmaşık bir türdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-128">`Address` is a complex type.</span></span> <span data-ttu-id="6fc70-129">(Bir varlık türü, yani, bir anahtar yok.)</span><span class="sxs-lookup"><span data-stu-id="6fc70-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="6fc70-130">`Customer` bir varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-130">`Customer` is an entity type.</span></span> <span data-ttu-id="6fc70-131">(Bir anahtarı yok.)</span><span class="sxs-lookup"><span data-stu-id="6fc70-131">(It has a key.)</span></span>
- <span data-ttu-id="6fc70-132">`Press` bir açık karmaşık bir türdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="6fc70-133">`Book` bir açık varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="6fc70-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="6fc70-134">Açık bir tür oluşturmak için CLR türü türünün bir özelliği olmalıdır `IDictionary<string, object>`, dinamik özelliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="6fc70-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="6fc70-135">EDM modeli oluşturun</span><span class="sxs-lookup"><span data-stu-id="6fc70-135">Build the EDM Model</span></span>

<span data-ttu-id="6fc70-136">Kullanırsanız **ODataConventionModelBuilder** EDM oluşturmak için `Press` ve `Book` varlığını temel alarak açık türler olarak otomatik olarak eklenen bir `IDictionary<string, object>` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6fc70-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="6fc70-137">Ayrıca EDM açıkça kullanarak oluşturabilirsiniz **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="6fc70-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="6fc70-138">Bir OData denetleyicisi Ekle</span><span class="sxs-lookup"><span data-stu-id="6fc70-138">Add an OData Controller</span></span>

<span data-ttu-id="6fc70-139">Ardından, bir OData denetleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6fc70-139">Next, add an OData controller.</span></span> <span data-ttu-id="6fc70-140">Bu öğretici için yalnızca destekler alma POST istekleri ve varlıkları depolamak için bir bellek içi listesini kullanır, Basitleştirilmiş bir denetleyici kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="6fc70-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="6fc70-141">Dikkat ilk `Book` örneğinin dinamik özellik vardır.</span><span class="sxs-lookup"><span data-stu-id="6fc70-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="6fc70-142">İkinci `Book` örneği aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6fc70-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="6fc70-143">"Yayımlanmış": temel tür</span><span class="sxs-lookup"><span data-stu-id="6fc70-143">"Published": Primitive type</span></span>
- <span data-ttu-id="6fc70-144">"Yazar": İlkel türler koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="6fc70-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="6fc70-145">"OtherCategories": Numaralandırma türleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="6fc70-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="6fc70-146">Ayrıca, `Press` , söz konusu özellik `Book` örneği aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6fc70-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="6fc70-147">"Blog": temel tür</span><span class="sxs-lookup"><span data-stu-id="6fc70-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="6fc70-148">"Address": Karmaşık tür</span><span class="sxs-lookup"><span data-stu-id="6fc70-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="6fc70-149">Meta verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="6fc70-149">Query the Metadata</span></span>

<span data-ttu-id="6fc70-150">OData meta veri belgesi almak için GET isteğini göndermek `~/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="6fc70-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="6fc70-151">Yanıt gövdesi, şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6fc70-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="6fc70-152">Meta veri belgeden görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6fc70-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="6fc70-153">İçin `Book` ve `Press` türleri, değerini `OpenType` öznitelik değeri true.</span><span class="sxs-lookup"><span data-stu-id="6fc70-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="6fc70-154">`Customer` Ve `Address` türleri bu özniteliği yok.</span><span class="sxs-lookup"><span data-stu-id="6fc70-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="6fc70-155">`Book` Varlık türünde üç bildirilmiş özellikleri: ISBN, başlık ve tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="6fc70-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="6fc70-156">OData meta veri içermemesi `Book.Properties` CLR sınıftaki özellik.</span><span class="sxs-lookup"><span data-stu-id="6fc70-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="6fc70-157">Benzer şekilde, `Press` karmaşık tür yalnızca iki bildirilen özelliklere sahiptir: Adı ve kategori.</span><span class="sxs-lookup"><span data-stu-id="6fc70-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="6fc70-158">Meta veriler içermemesi `Press.DynamicProperties` CLR sınıftaki özellik.</span><span class="sxs-lookup"><span data-stu-id="6fc70-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="6fc70-159">Sorgu bir varlık</span><span class="sxs-lookup"><span data-stu-id="6fc70-159">Query an Entity</span></span>

<span data-ttu-id="6fc70-160">ISBN defteriyle "978-0-7356-7942-9" eşit almak için GET isteğini göndermek `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="6fc70-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="6fc70-161">Yanıt gövdesi, aşağıdakine benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="6fc70-161">The response body should look similar to the following.</span></span> <span data-ttu-id="6fc70-162">(Daha okunabilir yapmak için girintili.)</span><span class="sxs-lookup"><span data-stu-id="6fc70-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="6fc70-163">Dinamik özellikler satır içi bildirilen özelliklere sahip olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6fc70-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="6fc70-164">Bir varlık gönderin</span><span class="sxs-lookup"><span data-stu-id="6fc70-164">POST an Entity</span></span>

<span data-ttu-id="6fc70-165">Bir kitap varlığı eklemek için bir POST isteği gönderin `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="6fc70-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="6fc70-166">İstemci istek yükünde dinamik özellikleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fc70-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="6fc70-167">İşte bir örnek istek.</span><span class="sxs-lookup"><span data-stu-id="6fc70-167">Here is an example request.</span></span> <span data-ttu-id="6fc70-168">"Price" ve "Yayımlanmış" özellikleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6fc70-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="6fc70-169">Denetleyici yöntemde bir kesme noktası ayarlarsanız, Web API'si için bu özellikleri eklendi görebilirsiniz `Properties` sözlüğü.</span><span class="sxs-lookup"><span data-stu-id="6fc70-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="6fc70-170">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6fc70-170">Additional Resources</span></span>

[<span data-ttu-id="6fc70-171">OData açık tür örneği</span><span class="sxs-lookup"><span data-stu-id="6fc70-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
