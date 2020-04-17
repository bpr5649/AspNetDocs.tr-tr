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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="a50af-104">ASP.NET Web API ile OData v4'te Açık Türleri</span><span class="sxs-lookup"><span data-stu-id="a50af-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="a50af-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="a50af-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a50af-106">OData v4'te *açık tür,* tür tanımında bildirilen tüm özelliklere ek olarak dinamik özellikler içeren yapılandırılmış bir türdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="a50af-107">Açık türler, veri modellerinize esneklik eklemenize izin sağlar.</span><span class="sxs-lookup"><span data-stu-id="a50af-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="a50af-108">Bu öğretici, ASP.NET Web API OData'da açık türlerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a50af-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="a50af-109">Bu öğretici, ASP.NET Web API'sinde Bir OData bitiş noktası oluşturmayı zaten bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="a50af-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="a50af-110">Değilse, önce [Bir OData v4 Endpoint oluştur'u](create-an-odata-v4-endpoint.md) okuyarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="a50af-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a50af-111">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a50af-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a50af-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="a50af-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="a50af-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="a50af-113">OData v4</span></span>

<span data-ttu-id="a50af-114">İlk olarak, bazı OData terminolojisi:</span><span class="sxs-lookup"><span data-stu-id="a50af-114">First, some OData terminology:</span></span>

- <span data-ttu-id="a50af-115">Varlık türü: Anahtarlı yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="a50af-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="a50af-116">Karmaşık tür: Anahtarsız yapılandırılmış bir tür.</span><span class="sxs-lookup"><span data-stu-id="a50af-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="a50af-117">Açık tür: Dinamik özelliklere sahip bir tür.</span><span class="sxs-lookup"><span data-stu-id="a50af-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="a50af-118">Hem varlık türleri hem de karmaşık türler açık olabilir.</span><span class="sxs-lookup"><span data-stu-id="a50af-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="a50af-119">Dinamik bir özelliğin değeri ilkel bir tür, karmaşık tür veya numaralandırma türü olabilir; veya bu türlerden herhangi birinin bir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="a50af-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="a50af-120">Açık türleri hakkında daha fazla bilgi için [OData v4 belirtimine](http://www.odata.org/documentation/odata-version-4-0/)bakın.</span><span class="sxs-lookup"><span data-stu-id="a50af-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="a50af-121">Web OData Kitaplıklarını Yükleme</span><span class="sxs-lookup"><span data-stu-id="a50af-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="a50af-122">En son Web API OData kitaplıklarını yüklemek için NuGet Paket Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="a50af-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="a50af-123">Paket Yöneticisi Konsolu penceresinden:</span><span class="sxs-lookup"><span data-stu-id="a50af-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="a50af-124">CLR Türlerini Tanımla</span><span class="sxs-lookup"><span data-stu-id="a50af-124">Define the CLR Types</span></span>

<span data-ttu-id="a50af-125">EDM modellerini CLR türleri olarak tanımlayarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="a50af-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="a50af-126">Varlık Veri Modeli (EDM) oluşturulduğunda,</span><span class="sxs-lookup"><span data-stu-id="a50af-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="a50af-127">`Category`numaralandırma türüdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="a50af-128">`Address`karmaşık bir türüdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-128">`Address` is a complex type.</span></span> <span data-ttu-id="a50af-129">(Bir anahtarı yoktur, bu nedenle bir varlık türü değildir.)</span><span class="sxs-lookup"><span data-stu-id="a50af-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="a50af-130">`Customer`bir varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-130">`Customer` is an entity type.</span></span> <span data-ttu-id="a50af-131">(Bir anahtarı vardır.)</span><span class="sxs-lookup"><span data-stu-id="a50af-131">(It has a key.)</span></span>
- <span data-ttu-id="a50af-132">`Press`açık karmaşık bir türüdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="a50af-133">`Book`açık bir varlık türüdür.</span><span class="sxs-lookup"><span data-stu-id="a50af-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="a50af-134">Açık bir tür oluşturmak için CLR türüdinamik `IDictionary<string, object>`özellikleri tutan bir tür özelliğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a50af-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="a50af-135">EDM Modelini Oluşturun</span><span class="sxs-lookup"><span data-stu-id="a50af-135">Build the EDM Model</span></span>

<span data-ttu-id="a50af-136">EDM'yi oluşturmak için **ODataConventionModelBuilder** kullanıyorsanız `Press` ve `Book` bir `IDictionary<string, object>` özelliğin varlığına bağlı olarak otomatik olarak açık türler olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="a50af-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="a50af-137">Ayrıca açıkça EDM oluşturabilirsiniz, **ODataModelBuilder**kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a50af-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="a50af-138">OData Denetleyicisi Ekleme</span><span class="sxs-lookup"><span data-stu-id="a50af-138">Add an OData Controller</span></span>

<span data-ttu-id="a50af-139">Ardından, bir OData denetleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a50af-139">Next, add an OData controller.</span></span> <span data-ttu-id="a50af-140">Bu öğretici için, yalnızca GET ve POST isteklerini destekleyen ve varlıkları depolamak için bellek içi bir liste kullanan basitleştirilmiş bir denetleyici kullanırız.</span><span class="sxs-lookup"><span data-stu-id="a50af-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="a50af-141">İlk `Book` örneğin dinamik bir özelliği olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a50af-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="a50af-142">İkinci `Book` örnek aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a50af-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="a50af-143">"Yayınlandı": İlkel tip</span><span class="sxs-lookup"><span data-stu-id="a50af-143">"Published": Primitive type</span></span>
- <span data-ttu-id="a50af-144">"Yazarlar": Ilkel türlerin koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="a50af-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="a50af-145">"OtherCategories": Numaralandırma türlerinin toplanması.</span><span class="sxs-lookup"><span data-stu-id="a50af-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="a50af-146">Ayrıca, `Press` bu `Book` örneğin özelliği aşağıdaki dinamik özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a50af-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="a50af-147">"Blog": İlkel tip</span><span class="sxs-lookup"><span data-stu-id="a50af-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="a50af-148">"Adres": Karmaşık tür</span><span class="sxs-lookup"><span data-stu-id="a50af-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="a50af-149">Meta verileri sorgula</span><span class="sxs-lookup"><span data-stu-id="a50af-149">Query the Metadata</span></span>

<span data-ttu-id="a50af-150">OData meta veri belgesini almak için `~/$metadata`bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="a50af-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="a50af-151">Yanıt gövdesi buna benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a50af-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="a50af-152">Meta veri belgesinden şunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a50af-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="a50af-153">Ve türleri için özniteliğin `OpenType` değeri doğrudur. `Press` `Book`</span><span class="sxs-lookup"><span data-stu-id="a50af-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="a50af-154">`Customer` Ve `Address` türleri bu özniteliğe sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="a50af-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="a50af-155">Varlık `Book` türü, bildirilen üç özelluğa sahiptir: ISBN, Başlık ve Basın.</span><span class="sxs-lookup"><span data-stu-id="a50af-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="a50af-156">OData meta verileri CLR `Book.Properties` sınıfındaki özelliği içermez.</span><span class="sxs-lookup"><span data-stu-id="a50af-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="a50af-157">Benzer şekilde, `Press` karmaşık türü yalnızca iki bildirilen özellikleri vardır: Ad ve Kategori.</span><span class="sxs-lookup"><span data-stu-id="a50af-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="a50af-158">Meta veriler CLR `Press.DynamicProperties` sınıfındaki özelliği içermez.</span><span class="sxs-lookup"><span data-stu-id="a50af-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="a50af-159">Bir Varlığı Sorgula</span><span class="sxs-lookup"><span data-stu-id="a50af-159">Query an Entity</span></span>

<span data-ttu-id="a50af-160">"978-0-7356-7942-9" eeşit ISBN ile kitap almak için, `~/Books('978-0-7356-7942-9')`bir GET isteği gönderin .</span><span class="sxs-lookup"><span data-stu-id="a50af-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="a50af-161">Yanıt gövdesi aşağıdakine benzer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a50af-161">The response body should look similar to the following.</span></span> <span data-ttu-id="a50af-162">(Girindi daha okunabilir hale getirmek için.)</span><span class="sxs-lookup"><span data-stu-id="a50af-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="a50af-163">Dinamik özelliklerin bildirilen özelliklere satır satır da dahil olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a50af-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="a50af-164">Bir Varlık GÖNDER</span><span class="sxs-lookup"><span data-stu-id="a50af-164">POST an Entity</span></span>

<span data-ttu-id="a50af-165">Kitap varlığı eklemek için, `~/Books`bir POST isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="a50af-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="a50af-166">İstemci istek yükünde dinamik özellikler ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a50af-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="a50af-167">Aşağıda bir örnek istek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a50af-167">Here is an example request.</span></span> <span data-ttu-id="a50af-168">"Fiyat" ve "Yayınlanmış" özelliklerine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a50af-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="a50af-169">Denetleyici yönteminde bir kesme noktası ayarlarsanız, Web API'sinin bu `Properties` özellikleri ötmede ekladığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50af-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="a50af-170">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a50af-170">Additional Resources</span></span>

[<span data-ttu-id="a50af-171">OData Açık Tip Örneği</span><span class="sxs-lookup"><span data-stu-id="a50af-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
