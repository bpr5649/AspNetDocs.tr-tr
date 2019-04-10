---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: İçerik anlaşması ASP.NET Web API'si - ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API HTTP İçerik anlaşması ASP.NET nasıl uyguladığını açıklar 4.x.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59380167"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="82d20-103">ASP.NET Web API'de içerik anlaşması</span><span class="sxs-lookup"><span data-stu-id="82d20-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="82d20-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="82d20-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="82d20-105">ASP.NET Web API ASP.NET için içerik anlaşması nasıl uyguladığını bu makalede 4.x.</span><span class="sxs-lookup"><span data-stu-id="82d20-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="82d20-106">HTTP belirtimini (RFC 2616) "kullanılabilir birden çok temsile olduğunda belirtilen bir yanıt için en iyi gösterimi seçme işleminin." olarak içerik anlaşmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="82d20-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="82d20-107">HTTP İçerik anlaşması için birincil mekanizma olan bu istek üst bilgileri:</span><span class="sxs-lookup"><span data-stu-id="82d20-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="82d20-108">**Kabul et:** Hangi medya türü "application/json" gibi bir yanıt için kabul edilebilir "application/xml" veya bir özel medya türü gibi &quot;application/vnd.example+xml&quot;</span><span class="sxs-lookup"><span data-stu-id="82d20-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="82d20-109">**Accept-Charset:** Hangi karakter kümelerini UTF-8 veya ISO 8859-1 gibi kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="82d20-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="82d20-110">**Kabul et-Encoding:** Hangi içerik kodlamaları, gzip gibi kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="82d20-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="82d20-111">**Kabul dili:** Tercih edilen doğal dili gibi "en-us".</span><span class="sxs-lookup"><span data-stu-id="82d20-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="82d20-112">Sunucu HTTP isteği diğer kısımlarını de bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82d20-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="82d20-113">İsteğin bir X-Requested-With üst bilgisi içeriyorsa, Accept üst bilgisi yok ise örneğin, bir AJAX isteği belirten JSON için varsayılan sunucu.</span><span class="sxs-lookup"><span data-stu-id="82d20-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="82d20-114">Bu makalede, Web API'si kabul et ve Accept-Charset üstbilgileri nasıl kullandığını adresindeki inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="82d20-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="82d20-115">(Şu anda yerleşik desteği yoktur Accept-Encoding veya Accept-Language.)</span><span class="sxs-lookup"><span data-stu-id="82d20-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="82d20-116">Serileştirme</span><span class="sxs-lookup"><span data-stu-id="82d20-116">Serialization</span></span>

<span data-ttu-id="82d20-117">Bir Web API denetleyicisi, bir kaynak olarak CLR türü döndürürse, işlem hattı dönüş değeri serileştirir ve HTTP yanıt gövdesi yazar.</span><span class="sxs-lookup"><span data-stu-id="82d20-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="82d20-118">Örneğin, aşağıdaki denetleyici eylemi göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="82d20-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="82d20-119">Bir istemci, bu HTTP isteği gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="82d20-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="82d20-120">Yanıt olarak, sunucunun gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="82d20-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="82d20-121">Bu örnekte, JSON, Javascript veya "şey" istemci istenen (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="82d20-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="82d20-122">Sunucu yanıtı bir JSON temsili `Product` nesne.</span><span class="sxs-lookup"><span data-stu-id="82d20-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="82d20-123">Yanıttaki Content-Type üstbilgisi ayarlandığına dikkat edin &quot;application/json&quot;.</span><span class="sxs-lookup"><span data-stu-id="82d20-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="82d20-124">Bir denetleyici de döndürebilir bir **HttpResponseMessage** nesne.</span><span class="sxs-lookup"><span data-stu-id="82d20-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="82d20-125">Yanıt gövdesi için bir CLR nesnesi belirtmek için çağrı **CreateResponse** genişletme yöntemi:</span><span class="sxs-lookup"><span data-stu-id="82d20-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="82d20-126">Bu seçenek hakkında daha fazla denetime yanıt ayrıntılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="82d20-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="82d20-127">Durum kodu ayarlamak, HTTP üst bilgileri ekleyin ve VS.</span><span class="sxs-lookup"><span data-stu-id="82d20-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="82d20-128">Kaynak serileştiren nesnesi olarak adlandırılan bir *medya biçimlendiricisi*.</span><span class="sxs-lookup"><span data-stu-id="82d20-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="82d20-129">Medya biçimlendiricileri türetilen **MediaTypeFormatter** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="82d20-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="82d20-130">Web API'si, XML ve JSON için medya biçimlendiricileri sağlar ve diğer medya türleri desteklemek için özel biçimlendiriciler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82d20-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="82d20-131">Özel bir Biçimlendiricinin yazma hakkında daha fazla bilgi için bkz: [medya Biçimlendiricileri](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="82d20-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="82d20-132">Nasıl içerik anlaşması çalışır</span><span class="sxs-lookup"><span data-stu-id="82d20-132">How Content Negotiation Works</span></span>

<span data-ttu-id="82d20-133">İlk olarak, işlem hattı alır **IContentNegotiator** hizmetinde **HttpConfiguration** nesne.</span><span class="sxs-lookup"><span data-stu-id="82d20-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="82d20-134">Ayrıca medya biçimlendiricileri listesi alır **HttpConfiguration.Formatters** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="82d20-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="82d20-135">Ardından, işlem hattını çağıran **IContentNegotiator.Negotiate**, içinde geçen:</span><span class="sxs-lookup"><span data-stu-id="82d20-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="82d20-136">Serileştirilecek nesnenin türü</span><span class="sxs-lookup"><span data-stu-id="82d20-136">The type of object to serialize</span></span>
- <span data-ttu-id="82d20-137">Medya biçimlendiricileri koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="82d20-137">The collection of media formatters</span></span>
- <span data-ttu-id="82d20-138">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="82d20-138">The HTTP request</span></span>

<span data-ttu-id="82d20-139">**Anlaş** yöntemi iki bilgi parçasını döndürür:</span><span class="sxs-lookup"><span data-stu-id="82d20-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="82d20-140">Kullanmak için hangi biçimlendirici</span><span class="sxs-lookup"><span data-stu-id="82d20-140">Which formatter to use</span></span>
- <span data-ttu-id="82d20-141">Yanıt medya türü</span><span class="sxs-lookup"><span data-stu-id="82d20-141">The media type for the response</span></span>

<span data-ttu-id="82d20-142">Biçimlendirici bulunamazsa **anlaş** yöntemi döndürür **null**, ve istemci 406 (kabul edilemez) HTTP hatası alır.</span><span class="sxs-lookup"><span data-stu-id="82d20-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="82d20-143">Aşağıdaki kod nasıl bir denetleyici içerik anlaşması doğrudan çağırabilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="82d20-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="82d20-144">Bu kod eşdeğerdir için işlem hattı otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="82d20-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="82d20-145">Varsayılan içerik Uzlaştırıcı</span><span class="sxs-lookup"><span data-stu-id="82d20-145">Default Content Negotiator</span></span>

<span data-ttu-id="82d20-146">**DefaultContentNegotiator** sınıf varsayılan uygulamasını sağlar **IContentNegotiator**.</span><span class="sxs-lookup"><span data-stu-id="82d20-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="82d20-147">Bir biçimlendirici seçmek için birden çok ölçüt kullanır.</span><span class="sxs-lookup"><span data-stu-id="82d20-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="82d20-148">İlk olarak, biçimlendirici türü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82d20-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="82d20-149">Bu çağrı yaparak doğrulanır **MediaTypeFormatter.CanWriteType**.</span><span class="sxs-lookup"><span data-stu-id="82d20-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="82d20-150">Ardından, içerik uzlaştırıcı her bir Biçimlendiricinin arar ve onu HTTP isteğiyle ne kadar iyi eşleştiğini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="82d20-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="82d20-151">Eşleşme değerlendirilecek içerik uzlaştırıcı iki şeyi biçimlendirici üzerinde görünür:</span><span class="sxs-lookup"><span data-stu-id="82d20-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="82d20-152">**SupportedMediaTypes** desteklenen medya türlerinin bir listesini içeren bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="82d20-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="82d20-153">İçerik uzlaştırıcı Accept üst bilgisi isteğe karşı bu listesi ile eşleşecek şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="82d20-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="82d20-154">Accept üst bilgisi aralıkları dahil edebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82d20-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="82d20-155">Örneğin, "text/plain" metin için bir eşleşme olduğundan /\* veya \* / \*.</span><span class="sxs-lookup"><span data-stu-id="82d20-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="82d20-156">**MediaTypeMappings** listesini içeren bir koleksiyon **MediaTypeMapping** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="82d20-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="82d20-157">**MediaTypeMapping** sınıfı HTTP isteklerini medya türleriyle eşleşmesi için genel bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="82d20-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="82d20-158">Örneğin, özel bir HTTP üstbilgisi belirli bir ortama eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82d20-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="82d20-159">Varsa birden çok yüksek kalite faktörü WINS eşleşmeyi eşleşir.</span><span class="sxs-lookup"><span data-stu-id="82d20-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="82d20-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="82d20-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="82d20-161">Bu örnekte, uygulama/json 1.0, bir örtük kalite faktörü bulunduğundan application/xml ' tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="82d20-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="82d20-162">Herhangi bir eşleşme bulunursa, içerik uzlaştırıcı istek gövdesinin medya türü üzerinden varsa çalışır.</span><span class="sxs-lookup"><span data-stu-id="82d20-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="82d20-163">Örneğin, istek JSON veri içeriyorsa, içerik uzlaştırıcı JSON biçimlendirici için görünür.</span><span class="sxs-lookup"><span data-stu-id="82d20-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="82d20-164">Yine de herhangi bir eşleşme varsa, içerik uzlaştırıcı yalnızca türü serileştirebilen ilk biçimlendiriciyi alır.</span><span class="sxs-lookup"><span data-stu-id="82d20-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="82d20-165">Bir karakter kodlaması seçme</span><span class="sxs-lookup"><span data-stu-id="82d20-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="82d20-166">Biçimlendiriciyi seçtikten sonra içerik uzlaştırıcı en iyi karakter bakarak kodlamasını seçer **SupportedEncodings** biçimlendirici ve bu istek üstbilgisinde Accept-Charset (varsa) eşleştirme özelliği.</span><span class="sxs-lookup"><span data-stu-id="82d20-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
