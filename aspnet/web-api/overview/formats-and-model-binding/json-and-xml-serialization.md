---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API'de JSON ve XML Serileştirme - ASP.NET 4.x
author: MikeWasson
description: JSON ve XML formatters ASP.NET Web API için ASP.NET 4.x açıklar.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676225"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="40c91-103">ASP.NET Web API'sinde JSON ve XML Serileştirme</span><span class="sxs-lookup"><span data-stu-id="40c91-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="40c91-104">Mike [Wasson](https://github.com/MikeWasson) tarafından</span><span class="sxs-lookup"><span data-stu-id="40c91-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="40c91-105">Bu makalede, ASP.NET Web API'sında JSON ve XML ön seçimlerini açıkçık</span><span class="sxs-lookup"><span data-stu-id="40c91-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="40c91-106">ASP.NET Web API'sinde, *medya türü formatter* şunları yapabilecek bir nesnedir:</span><span class="sxs-lookup"><span data-stu-id="40c91-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="40c91-107">BIR HTTP ileti gövdesinden CLR nesnelerini okuma</span><span class="sxs-lookup"><span data-stu-id="40c91-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="40c91-108">CLR nesnelerini http ileti gövdesine yazma</span><span class="sxs-lookup"><span data-stu-id="40c91-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="40c91-109">Web API hem JSON hem de XML için ortam tipi formatters sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c91-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="40c91-110">Çerçeve, varsayılan olarak bu formatters boru hattına ekler.</span><span class="sxs-lookup"><span data-stu-id="40c91-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="40c91-111">İstemciler, HTTP isteğinin kabul üstbilgisinde JSON veya XML'i isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="40c91-112">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="40c91-112">Contents</span></span>

- [<span data-ttu-id="40c91-113">JSON Medya Tipi Formatter</span><span class="sxs-lookup"><span data-stu-id="40c91-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="40c91-114">Salt Okunur Özellikler</span><span class="sxs-lookup"><span data-stu-id="40c91-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="40c91-115">Tarih</span><span class="sxs-lookup"><span data-stu-id="40c91-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="40c91-116">Girintileme</span><span class="sxs-lookup"><span data-stu-id="40c91-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="40c91-117">Deve Kılıfı</span><span class="sxs-lookup"><span data-stu-id="40c91-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="40c91-118">Anonim ve Zayıf Yazılan Nesneler</span><span class="sxs-lookup"><span data-stu-id="40c91-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="40c91-119">XML Medya Tipi Formatter</span><span class="sxs-lookup"><span data-stu-id="40c91-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="40c91-120">Salt Okunur Özellikler</span><span class="sxs-lookup"><span data-stu-id="40c91-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="40c91-121">Tarih</span><span class="sxs-lookup"><span data-stu-id="40c91-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="40c91-122">Girintileme</span><span class="sxs-lookup"><span data-stu-id="40c91-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="40c91-123">XML Serializers Başına Ayar</span><span class="sxs-lookup"><span data-stu-id="40c91-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="40c91-124">JSON veya XML Formatter kaldırma</span><span class="sxs-lookup"><span data-stu-id="40c91-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="40c91-125">Dairesel Nesne Başvurularının İşlemesi</span><span class="sxs-lookup"><span data-stu-id="40c91-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="40c91-126">Nesne Serileştirmeyi Test Etme</span><span class="sxs-lookup"><span data-stu-id="40c91-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="40c91-127">JSON Medya Tipi Formatter</span><span class="sxs-lookup"><span data-stu-id="40c91-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="40c91-128">JSON biçimlendirme **JsonMediaTypeFormatter** sınıfı tarafından sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="40c91-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="40c91-129">Varsayılan olarak, **JsonMediaTypeFormatter** serileştirme gerçekleştirmek için [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c91-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="40c91-130">Json.NET üçüncü taraf bir açık kaynak projesidir.</span><span class="sxs-lookup"><span data-stu-id="40c91-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="40c91-131">İsterseniz, **JsonMediaTypeFormatter** sınıfını Json.NET yerine **DataContractJsonSerializer'ı** kullanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="40c91-132">Bunu yapmak için, **UseDataContractJsonSerializer** özelliğini **doğru**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="40c91-133">JSON Seri Hale Getirme</span><span class="sxs-lookup"><span data-stu-id="40c91-133">JSON Serialization</span></span>

<span data-ttu-id="40c91-134">Bu bölümde, varsayılan [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer kullanarak, JSON formatter bazı özel davranışları açıklanır.</span><span class="sxs-lookup"><span data-stu-id="40c91-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="40c91-135">Bu, Json.NET kitaplığın kapsamlı bir belgelenmesi değildir; daha fazla bilgi için [Json.NET Belgeler'e](http://james.newtonking.com/projects/json/help/)bakın.</span><span class="sxs-lookup"><span data-stu-id="40c91-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="40c91-136">Ne Serialized alır?</span><span class="sxs-lookup"><span data-stu-id="40c91-136">What Gets Serialized?</span></span>

<span data-ttu-id="40c91-137">Varsayılan olarak, tüm ortak özellikler ve alanlar serileştirilmiş JSON'a dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="40c91-138">Bir özelliği veya alanı atlamak için, **jsonIgnore** özniteliği ile süsleyin.</span><span class="sxs-lookup"><span data-stu-id="40c91-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="40c91-139">&quot;Bir kabul&quot; yaklaşımı tercih ederseniz, sınıfı **DataContract** özniteliğiyle süsleyin.</span><span class="sxs-lookup"><span data-stu-id="40c91-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="40c91-140">Bu öznitelik varsa, **üyeler DataMember**yoksa yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="40c91-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="40c91-141">Özel üyeleri seri hale getirmek için **DataMember'ı** da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="40c91-142">Salt Okunur Özellikler</span><span class="sxs-lookup"><span data-stu-id="40c91-142">Read-Only Properties</span></span>

<span data-ttu-id="40c91-143">Salt okunur özellikler varsayılan olarak seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="40c91-144">Dates</span><span class="sxs-lookup"><span data-stu-id="40c91-144">Dates</span></span>

<span data-ttu-id="40c91-145">Varsayılan olarak, Json.NET [tarihleri ISO 8601](http://www.w3.org/TR/NOTE-datetime) biçiminde yazar.</span><span class="sxs-lookup"><span data-stu-id="40c91-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="40c91-146">UTC'deki tarihler (Eşgüdümlü Evrensel Zaman) "Z" soneki ile yazılır.</span><span class="sxs-lookup"><span data-stu-id="40c91-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="40c91-147">Yerel saatdeki tarihler arasında saat dilimi mahsulü içerir.</span><span class="sxs-lookup"><span data-stu-id="40c91-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="40c91-148">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="40c91-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="40c91-149">Varsayılan olarak, Json.NET saat dilimini korur.</span><span class="sxs-lookup"><span data-stu-id="40c91-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="40c91-150">DateTimeZoneHandling özelliğini ayarlayarak bunu geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40c91-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="40c91-151">ISO 8601 yerine [Microsoft JSON tarih biçimini](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) kullanmayı tercih ederseniz, **DateFormatHandling** özelliğini serializer ayarlarında ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="40c91-152">Girintileme</span><span class="sxs-lookup"><span data-stu-id="40c91-152">Indenting</span></span>

<span data-ttu-id="40c91-153">Girintilen JSON yazmak için **Biçimlendirme** ayarını **Biçimlendirme.Girini**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="40c91-154">Deve Kılıfı</span><span class="sxs-lookup"><span data-stu-id="40c91-154">Camel Casing</span></span>

<span data-ttu-id="40c91-155">Deve kasalı JSON özellik adlarını yazmak için, veri modelinizi değiştirmeden **CamelCasePropertyNamesContractResolver'ı** serializer'a ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="40c91-156">Anonim ve Zayıf Yazılan Nesneler</span><span class="sxs-lookup"><span data-stu-id="40c91-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="40c91-157">Eylem yöntemi anonim bir nesneyi döndürebilir ve JSON'a serileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="40c91-158">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="40c91-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="40c91-159">Yanıt iletisi gövdesi aşağıdaki JSON'u içerir:</span><span class="sxs-lookup"><span data-stu-id="40c91-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="40c91-160">Web API'niz istemcilerden gevşek yapılandırılmış JSON nesneleri alıyorsa, istek gövdesini **Newtonsoft.Json.Linq.JObject** türüne dizileştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="40c91-161">Ancak, genellikle güçlü dakti-si yazılan veri nesneleri kullanmak daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="40c91-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="40c91-162">Daha sonra verileri ayrıştırmanız gerekmez ve model doğrulamanın avantajlarından yararlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="40c91-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="40c91-163">XML seri gösterici anonim türleri veya **JObject** örneklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="40c91-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="40c91-164">Bu özellikleri JSON verileriniz için kullanıyorsanız, bu makalede daha sonra açıklandığı gibi XML formatter'ı ardışık kaynaktan kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c91-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="40c91-165">XML Medya Tipi Formatter</span><span class="sxs-lookup"><span data-stu-id="40c91-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="40c91-166">XML biçimlendirme **XmlMediaTypeFormatter** sınıfı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="40c91-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="40c91-167">Varsayılan olarak, **XmlMediaTypeFormatter** serileştirme gerçekleştirmek için **DataContractSerializer** sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c91-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="40c91-168">İsterseniz, **XmlMediaTypeFormatter'ı** **DataContractSerializer**yerine **XmlSerializer** kullanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="40c91-169">Bunu yapmak için, **UseXmlSerializer** özelliğini **doğru**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="40c91-170">**XmlSerializer** sınıfı **DataContractSerializer'dan**daha dar bir tür kümesini destekler, ancak elde edilen XML üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c91-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="40c91-171">Varolan bir XML şemasıyla eşleşmeniz gerekiyorsa **XmlSerializer** kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="40c91-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="40c91-172">XML seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="40c91-172">XML Serialization</span></span>

<span data-ttu-id="40c91-173">Bu bölümde, varsayılan **DataContractSerializer**kullanarak XML formatter bazı özel davranışları açıklanır.</span><span class="sxs-lookup"><span data-stu-id="40c91-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="40c91-174">Varsayılan olarak, DataContractSerializer aşağıdaki gibi çalışır:</span><span class="sxs-lookup"><span data-stu-id="40c91-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="40c91-175">Tüm ortak okuma/yazma özellikleri ve alanları seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="40c91-176">Bir özelliği veya alanı atlamak için, onu **IgnoreDataMember** özniteliğiyle süsleyin.</span><span class="sxs-lookup"><span data-stu-id="40c91-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="40c91-177">Özel ve korunan üyeler serileştirilmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="40c91-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="40c91-178">Salt okunur özellikler seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="40c91-179">(Ancak, salt okunur toplama özelliğinin içeriği seri hale getirilmiştir.)</span><span class="sxs-lookup"><span data-stu-id="40c91-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="40c91-180">Sınıf ve üye adları XML'de sınıf bildiriminde göründükleri gibi yazılır.</span><span class="sxs-lookup"><span data-stu-id="40c91-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="40c91-181">Varsayılan bir XML ad alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="40c91-181">A default XML namespace is used.</span></span>

<span data-ttu-id="40c91-182">Serileştirme üzerinde daha fazla denetime ihtiyacınız varsa, sınıfı **DataContract** özniteliğiyle dekore edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="40c91-183">Bu öznitelik mevcut olduğunda, sınıf aşağıdaki gibi serihale edilir:</span><span class="sxs-lookup"><span data-stu-id="40c91-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="40c91-184">&quot;Yaklaşımı&quot; devre dışı bırakma: Özellikler ve alanlar varsayılan olarak serileştirilemez.</span><span class="sxs-lookup"><span data-stu-id="40c91-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="40c91-185">Bir özelliği veya alanı seri hale getirmek için, **onu DataMember** özniteliğiyle süsleyin.</span><span class="sxs-lookup"><span data-stu-id="40c91-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="40c91-186">Özel veya korumalı bir üyeyi seri hale getirmek için, **onu DataMember** özniteliğiyle süsleyin.</span><span class="sxs-lookup"><span data-stu-id="40c91-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="40c91-187">Salt okunur özellikler seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="40c91-188">Sınıf adının XML'de nasıl göründüğünü değiştirmek için **DataContract** özniteliğindeki *Ad* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="40c91-189">Bir üye adının XML'de nasıl görüneceğini değiştirmek **için, DataMember** özyüründeki *Ad* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="40c91-190">XML ad alanını değiştirmek için **DataContract** *sınıfındaAd Alanı* parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="40c91-191">Salt Okunur Özellikler</span><span class="sxs-lookup"><span data-stu-id="40c91-191">Read-Only Properties</span></span>

<span data-ttu-id="40c91-192">Salt okunur özellikler seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="40c91-193">Salt okunur bir özelliğin desteközel bir alanı varsa, özel alanı **DataMember** özniteliğiyle işaretleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="40c91-194">Bu yaklaşım, **sınıftaki DataContract** özniteliğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="40c91-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="40c91-195">Dates</span><span class="sxs-lookup"><span data-stu-id="40c91-195">Dates</span></span>

<span data-ttu-id="40c91-196">Tarihler ISO 8601 formatında yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="40c91-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="40c91-197">Örneğin, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="40c91-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="40c91-198">Girintileme</span><span class="sxs-lookup"><span data-stu-id="40c91-198">Indenting</span></span>

<span data-ttu-id="40c91-199">Girintilen XML yazmak için **Girintisi** **özelliğini doğru**olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40c91-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="40c91-200">XML Serializers Başına Ayar</span><span class="sxs-lookup"><span data-stu-id="40c91-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="40c91-201">Farklı CLR türleri için farklı XML serializers ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="40c91-202">Örneğin, geriye dönük uyumluluk için **XmlSerializer** gerektiren belirli bir veri nesneniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="40c91-203">Bu nesne için **XmlSerializer** kullanabilir ve diğer türler için **DataContractSerializer** kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="40c91-204">Belirli bir tür için bir XML serializer ayarlamak **için, SetSerializer'ı**arayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="40c91-205">Bir **XmlSerializer** veya **XmlObjectSerializer**türetilen herhangi bir nesne belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="40c91-206">JSON veya XML Formatter kaldırma</span><span class="sxs-lookup"><span data-stu-id="40c91-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="40c91-207">Kullanmak istemiyorsanız, JSON formatter veya XML formatter formatters listesinden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="40c91-208">Bunu yapmak için ana nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="40c91-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="40c91-209">Web API yanıtlarınızı belirli bir ortam türüyle sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="40c91-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="40c91-210">Örneğin, yalnızca JSON yanıtlarını desteklemeye ve XML formatter'ı kaldırmaya karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="40c91-211">Varsayılan formatter'ı özel bir formatter ile değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="40c91-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="40c91-212">Örneğin, JSON formatter'ı kendi özel uygulamanızla değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="40c91-213">Aşağıdaki kod, varsayılan formatters kaldırmak için nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="40c91-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="40c91-214">Bunu Global.asax'ta tanımlanan **Uygulama\_Başlangıç** yönteminizden arayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="40c91-215">Dairesel Nesne Başvurularının İşlemesi</span><span class="sxs-lookup"><span data-stu-id="40c91-215">Handling Circular Object References</span></span>

<span data-ttu-id="40c91-216">Varsayılan olarak, JSON ve XML formatters değerleri olarak tüm nesneleri yazın.</span><span class="sxs-lookup"><span data-stu-id="40c91-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="40c91-217">İki özellik aynı nesneye başvuruyorsa veya aynı nesne bir koleksiyonda iki kez görünüyorsa, madde nesneyi iki kez serileştirir.</span><span class="sxs-lookup"><span data-stu-id="40c91-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="40c91-218">Nesne grafiğiniz döngüler içeriyorsa, bu belirli bir sorundur, çünkü serileştirici grafikte bir döngü algıladığında bir özel durum atar.</span><span class="sxs-lookup"><span data-stu-id="40c91-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="40c91-219">Aşağıdaki nesne modellerini ve denetleyiciyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="40c91-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="40c91-220">Bu eylemi çağırmak, formatter'ın istemciye bir durum kodu 500 (İç Sunucu Hatası) yanıtı anlamına gelen bir özel durum atmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c91-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="40c91-221">JSON'daki nesne başvurularını korumak için Global.asax dosyasındaki **Uygulama\_Başlat** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40c91-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="40c91-222">Şimdi denetleyici eylem bu gibi görünüyor JSON dönecektir:</span><span class="sxs-lookup"><span data-stu-id="40c91-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="40c91-223">Serileştiricinin her iki &quot;nesneye de $id&quot; özelliği eklediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="40c91-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="40c91-224">Ayrıca, Employee.Department özelliğinin bir döngü oluşturduğunu algılar, bu nedenle değeri bir nesne&quot;&quot;başvurusuyla değiştirir: { $ref :&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="40c91-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="40c91-225">Nesne başvuruları JSON'da standart değildir.</span><span class="sxs-lookup"><span data-stu-id="40c91-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="40c91-226">Bu özelliği kullanmadan önce, müşterilerinizin sonuçları ayrıştırıp ayrıştıramayacağını düşünün.</span><span class="sxs-lookup"><span data-stu-id="40c91-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="40c91-227">Grafiklerden döngüleri kaldırmak daha iyi olabilir.</span><span class="sxs-lookup"><span data-stu-id="40c91-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="40c91-228">Örneğin, Çalışan'dan Departmana bağlantı bu örnekte gerçekten gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="40c91-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="40c91-229">XML'de nesne başvurularını korumak için iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="40c91-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="40c91-230">Daha basit seçenek model `[DataContract(IsReference=true)]` sınıfınıza eklemektir.</span><span class="sxs-lookup"><span data-stu-id="40c91-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="40c91-231">*IsReference* parametresi nesne başvuruları sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c91-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="40c91-232">**DataContract'ın** serileştirmeyi devre dışı bırakma özelliğine sahip olduğunu unutmayın, bu nedenle özelliklere **DataMember** öznitelikleri eklemeniz de gerekir:</span><span class="sxs-lookup"><span data-stu-id="40c91-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="40c91-233">Şimdi formatter aşağıdaki benzer XML üretecek:</span><span class="sxs-lookup"><span data-stu-id="40c91-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="40c91-234">Model sınıfınızdaki özniteliklerden kaçınmak istiyorsanız, başka bir seçenek daha vardır: Yeni bir türe özgü **DataContractSerializer** örneği oluşturun ve constructor'da **geçerli** olan *ObjectReferences'ı koruyun'* u ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="40c91-235">Daha sonra bu örneği XML ortam türü nde bir tür başına serileştirici olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40c91-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="40c91-236">Aşağıdaki kod, bunun nasıl yapılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="40c91-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="40c91-237">Nesne Serileştirmeyi Test Etme</span><span class="sxs-lookup"><span data-stu-id="40c91-237">Testing Object Serialization</span></span>

<span data-ttu-id="40c91-238">Web API'nizi tasarlarken, veri nesnelerinizin nasıl seri hale getirileceğini test etmek yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="40c91-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="40c91-239">Bunu bir denetleyici oluşturmadan veya bir denetleyici eylemi çağırmadan yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c91-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
