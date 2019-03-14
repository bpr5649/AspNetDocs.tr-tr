---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1 sürümünde BSON desteği | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 709fb0266c0725176358a1bd0d08b3e07fa6e2a6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077190"
---
<a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="2180d-102">ASP.NET Web API 2.1 sürümünde BSON desteği</span><span class="sxs-lookup"><span data-stu-id="2180d-102">BSON Support in ASP.NET Web API 2.1</span></span>
====================
<span data-ttu-id="2180d-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2180d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2180d-104">Web API 2.1 BSON desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="2180d-104">Web API 2.1 introduces support for BSON.</span></span> <span data-ttu-id="2180d-105">Bu konuda, Web API denetleyicinizde (sunucu tarafı) ve bir .NET istemci uygulamasında BSON kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2180d-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span>

## <a name="what-is-bson"></a><span data-ttu-id="2180d-106">BSON nedir?</span><span class="sxs-lookup"><span data-stu-id="2180d-106">What is BSON?</span></span>

<span data-ttu-id="2180d-107">[BSON](http://bsonspec.org/) bir ikili serileştirme biçimidir.</span><span class="sxs-lookup"><span data-stu-id="2180d-107">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="2180d-108">"BSON", "İçin ikili JSON" anlamına gelir, ancak BSON ve JSON çok farklı serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="2180d-108">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="2180d-109">BSON olan "JSON benzeri", çünkü nesneleri ad-değer çiftleri, JSON ile benzer olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="2180d-109">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="2180d-110">JSON, sayısal veri türleri değil dizeleri bayt depolanır</span><span class="sxs-lookup"><span data-stu-id="2180d-110">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="2180d-111">BSON, basit, kolay taranabilir ve hızlı kodlama/kod çözme için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2180d-111">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="2180d-112">BSON, JSON'a boyutu karşılaştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2180d-112">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="2180d-113">Verilere bağlı olarak bir BSON yükü daha küçük veya büyük bir JSON yükü olabilir.</span><span class="sxs-lookup"><span data-stu-id="2180d-113">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="2180d-114">İkili verileri base64 kodlu olmadığı için bir görüntü dosyası gibi ikili verileri seri hale getirme için BSON JSON küçüktür.</span><span class="sxs-lookup"><span data-stu-id="2180d-114">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="2180d-115">Bir Ayrıştırıcı kod çözme olmadan öğeleri atlayabilirsiniz öğeleri bir uzunluğu alanıyla önünde taramak BSON belgeleri kolaydır.</span><span class="sxs-lookup"><span data-stu-id="2180d-115">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="2180d-116">Sayısal veri türleri olmayan dizeler numaraları olarak depolandığından kodlama ve kodunu çözme ve verimlidir.</span><span class="sxs-lookup"><span data-stu-id="2180d-116">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="2180d-117">.NET istemci uygulamaları gibi yerel istemci JSON veya XML gibi metin tabanlı biçimler yerine BSON kullanımından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2180d-117">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="2180d-118">JavaScript JSON yükü doğrudan dönüştürebilirsiniz çünkü tarayıcı istemcileri için büyük olasılıkla JSON ile takılıyor isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2180d-118">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="2180d-119">Neyse ki, Web API'si kullanan [içerik anlaşması](content-negotiation.md), API'nizi hem biçimleri için destek ve seçin istemci olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2180d-119">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="2180d-120">BSON sunucu üzerindeki etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2180d-120">Enabling BSON on the Server</span></span>

<span data-ttu-id="2180d-121">Web API yapılandırmanızda ekleme **BsonMediaTypeFormatter** biçimlendiricileri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="2180d-121">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="2180d-122">Artık Web API'sini istemci "application/bson" isterse, BSON biçimlendirici kullanır.</span><span class="sxs-lookup"><span data-stu-id="2180d-122">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="2180d-123">BSON diğer medya türleri ile ilişkilendirilecek SupportedMediaTypes koleksiyona ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2180d-123">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="2180d-124">Aşağıdaki kod, desteklenen medya türleri için "application/vnd.contoso" ekler:</span><span class="sxs-lookup"><span data-stu-id="2180d-124">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="2180d-125">Örnek HTTP oturumu</span><span class="sxs-lookup"><span data-stu-id="2180d-125">Example HTTP Session</span></span>

<span data-ttu-id="2180d-126">Bu örnekte, aşağıdaki model sınıfı artı basit bir Web API denetleyicisi kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="2180d-126">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="2180d-127">Bir istemci, aşağıdaki HTTP isteği gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="2180d-127">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="2180d-128">Yanıt şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="2180d-128">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="2180d-129">Ben ikili verileri burada yerine &quot;.&quot; karakter.</span><span class="sxs-lookup"><span data-stu-id="2180d-129">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="2180d-130">Aşağıdaki ekranda Fiddler programlarla ham onaltılık değerleri görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="2180d-130">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="2180d-131">BSON HttpClient kullanma</span><span class="sxs-lookup"><span data-stu-id="2180d-131">Using BSON with HttpClient</span></span>

<span data-ttu-id="2180d-132">.NET istemci uygulamaları, BSON biçimlendirici ile kullanabileceğiniz **HttpClient**.</span><span class="sxs-lookup"><span data-stu-id="2180d-132">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="2180d-133">Hakkında daha fazla bilgi için **HttpClient**, bkz: [bir Web API'si bir .NET istemcinin çağırma](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="2180d-133">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="2180d-134">Aşağıdaki kod, BSON kabul eder ve yanıt BSON yükü seri durumdan çıkarır bir GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="2180d-134">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="2180d-135">BSON sunucudan istek için Accept üst bilgisi için "application/bson" ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2180d-135">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="2180d-136">Yanıt gövdesi seri durumdan çıkarılacak kullanın **BsonMediaTypeFormatter**.</span><span class="sxs-lookup"><span data-stu-id="2180d-136">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="2180d-137">Yanıt gövdesi okunurken, bunu belirtmeniz gerekmez, bu Biçimlendiricinin varsayılan biçimlendiricileri koleksiyonunda değildir:</span><span class="sxs-lookup"><span data-stu-id="2180d-137">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="2180d-138">Sonraki örnek, BSON içeren bir POST isteği göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="2180d-138">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="2180d-139">Bu kod çoğunu önceki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2180d-139">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="2180d-140">Ancak **PostAsync** yöntemini belirtin **BsonMediaTypeFormatter** biçimlendirici olarak:</span><span class="sxs-lookup"><span data-stu-id="2180d-140">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="2180d-141">Üst düzey ilkel türler seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="2180d-141">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="2180d-142">Her BSON belge, anahtar/değer çifti listesidir. BSON belirtimi, bir tamsayı veya dize gibi tek bir ham değerini serileştirmeye yönelik bir söz dizimi tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="2180d-142">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="2180d-143">Bu sınırlara yakın çalışmak için **BsonMediaTypeFormatter** ilkel türler, özel bir durum olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="2180d-143">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="2180d-144">Seri hale getirme önce değeri bir anahtar/değer çifti "Value" anahtarı ile dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="2180d-144">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="2180d-145">Örneğin, bir API denetleyicisi bir tamsayı döndürür varsayalım:</span><span class="sxs-lookup"><span data-stu-id="2180d-145">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="2180d-146">Seri hale getirme önce BSON biçimlendirici bu aşağıdaki anahtar/değer çifti dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="2180d-146">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="2180d-147">Seri durumdan, biçimlendirici verileri özgün değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="2180d-147">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="2180d-148">Ancak, web API'NİZİN ham değer döndürürse bu durumu işlemek farklı bir BSON Ayrıştırıcıyı kullanarak istemcileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2180d-148">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="2180d-149">Genel olarak, ham değerler yerine, yapılandırılmış veriler döndüren düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2180d-149">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2180d-150">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2180d-150">Additional Resources</span></span>

[<span data-ttu-id="2180d-151">Web API BSON örneği</span><span class="sxs-lookup"><span data-stu-id="2180d-151">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="2180d-152">Medya Biçimlendiricileri</span><span class="sxs-lookup"><span data-stu-id="2180d-152">Media Formatters</span></span>](media-formatters.md)
