---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: "ASP.NET Web API'de HTML Form verileri gönderme: Form-urlencoded verileri | Microsoft Docs"
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/15/2012
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 2d01212cc408f8bb66fa3103464c9a1f7a1e21c6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073458"
---
<a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="c682e-102">ASP.NET Web API'de HTML Form verileri gönderme: Form-urlencoded Verileri</span><span class="sxs-lookup"><span data-stu-id="c682e-102">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>
====================
<span data-ttu-id="c682e-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c682e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="c682e-104">Bölüm 1: Form-urlencoded Verileri</span><span class="sxs-lookup"><span data-stu-id="c682e-104">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="c682e-105">Bu makalede, bir Web API denetleyicisi için form-urlencoded verileri gönderileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c682e-105">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="c682e-106">HTML formu genel bakış</span><span class="sxs-lookup"><span data-stu-id="c682e-106">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="c682e-107">Karmaşık türler gönderme</span><span class="sxs-lookup"><span data-stu-id="c682e-107">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="c682e-108">AJAX üzerinden form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c682e-108">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="c682e-109">Gönderen basit türler</span><span class="sxs-lookup"><span data-stu-id="c682e-109">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="c682e-110">[Tamamlanmış projeyi indirmek](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="c682e-110">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="c682e-111">HTML formu genel bakış</span><span class="sxs-lookup"><span data-stu-id="c682e-111">Overview of HTML Forms</span></span>

<span data-ttu-id="c682e-112">HTML form kullanımı alın veya veri sunucuya göndermek için gönderin.</span><span class="sxs-lookup"><span data-stu-id="c682e-112">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="c682e-113">**Yöntemi** özniteliği **form** öğesi HTTP yöntemi sunar:</span><span class="sxs-lookup"><span data-stu-id="c682e-113">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="c682e-114">GET için varsayılan yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="c682e-114">The default method is GET.</span></span> <span data-ttu-id="c682e-115">Form kullanıyorsa, formun URI sorgu dizesi olarak kodlanmış verileri alın.</span><span class="sxs-lookup"><span data-stu-id="c682e-115">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="c682e-116">Form POST kullanıyorsa, form verilerini istek gövdesinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="c682e-116">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="c682e-117">Deftere nakledilen veri **Notenctype** özniteliği, istek gövdesi biçimini belirtir:</span><span class="sxs-lookup"><span data-stu-id="c682e-117">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="c682e-118">Notenctype</span><span class="sxs-lookup"><span data-stu-id="c682e-118">enctype</span></span> | <span data-ttu-id="c682e-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c682e-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c682e-120">Application/x-www-form-urlencoded işlemek</span><span class="sxs-lookup"><span data-stu-id="c682e-120">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="c682e-121">Ad/değer çiftleri, benzer bir URI sorgu dizesi olarak kodlanmış bir form verileri.</span><span class="sxs-lookup"><span data-stu-id="c682e-121">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="c682e-122">Bu GÖNDERİ için varsayılan biçimidir.</span><span class="sxs-lookup"><span data-stu-id="c682e-122">This is the default format for POST.</span></span> |
| <span data-ttu-id="c682e-123">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="c682e-123">multipart/form-data</span></span> | <span data-ttu-id="c682e-124">Form verileri çok parçalı MIME ileti olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="c682e-124">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="c682e-125">Bir dosya sunucusuna yüklüyorsanız bu biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c682e-125">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="c682e-126">Bu makalede, bölüm 1 x-www-form-urlencoded işlemek biçimi arar.</span><span class="sxs-lookup"><span data-stu-id="c682e-126">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="c682e-127">[2. bölüm](sending-html-form-data-part-2.md) çok parçalı MIME açıklar.</span><span class="sxs-lookup"><span data-stu-id="c682e-127">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="c682e-128">Karmaşık türler gönderme</span><span class="sxs-lookup"><span data-stu-id="c682e-128">Sending Complex Types</span></span>

<span data-ttu-id="c682e-129">Genellikle, birden çok form denetimlerini alınan değerleri oluşan karmaşık bir tür gönderir.</span><span class="sxs-lookup"><span data-stu-id="c682e-129">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="c682e-130">Durum güncelleştirmesi temsil eden şu model göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c682e-130">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="c682e-131">Kabul eden bir Web API denetleyicisi İşte bir `Update` POST aracılığıyla nesne.</span><span class="sxs-lookup"><span data-stu-id="c682e-131">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="c682e-132">Bu denetleyicisi kullanan [eylem tabanlı yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), rota şablonu, bu nedenle &quot;API / {denetleyici} / {eylem} / {id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="c682e-132">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="c682e-133">İstemci verileri post gerçekleştireceği &quot;/api/updates/complex&quot;.</span><span class="sxs-lookup"><span data-stu-id="c682e-133">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="c682e-134">Artık kullanıcıların durumu güncelleştirmeyi göndermek bir HTML formuna yazalım.</span><span class="sxs-lookup"><span data-stu-id="c682e-134">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="c682e-135">Dikkat **eylem** özniteliktir formdaki denetleyicisi eylemimiz URI'si.</span><span class="sxs-lookup"><span data-stu-id="c682e-135">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="c682e-136">Girilen bazı değerler formu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c682e-136">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="c682e-137">Kullanıcı gönderme tıkladığında tarayıcı bir HTTP isteği aşağıdakine benzer gönderir:</span><span class="sxs-lookup"><span data-stu-id="c682e-137">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="c682e-138">İstek gövdesini form verileri, ad/değer çiftleri biçimlendirilmiş içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c682e-138">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="c682e-139">Web API'si bir örneğine otomatik olarak ad/değer çiftleri dönüştürür `Update` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c682e-139">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="c682e-140">AJAX üzerinden form verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c682e-140">Sending Form Data via AJAX</span></span>

<span data-ttu-id="c682e-141">Kullanıcı formu gönderdiğinde, tarayıcı Geçerli sayfadan ayrılmak gider ve yanıt iletisinin gövdesini işler.</span><span class="sxs-lookup"><span data-stu-id="c682e-141">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="c682e-142">Yanıtı HTML sayfası Tamam andır.</span><span class="sxs-lookup"><span data-stu-id="c682e-142">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="c682e-143">Bir web API ile ancak yanıt gövdesinin genellikle geçerli boş veya JSON gibi yapılandırılmış verilerin içerir.</span><span class="sxs-lookup"><span data-stu-id="c682e-143">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="c682e-144">Bu durumda, bu istek bir AJAX kullanarak form verilerini, sayfanın yanıt işleyebilmesi göndermek için daha anlamlı olur.</span><span class="sxs-lookup"><span data-stu-id="c682e-144">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="c682e-145">Aşağıdaki kod, jQuery kullanarak form verileri gönderileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c682e-145">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="c682e-146">JQuery **gönderme** işlevi, form eylemi yeni bir işlev ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c682e-146">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="c682e-147">Bu, Gönder düğmesinin varsayılan davranışı geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="c682e-147">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="c682e-148">**Serileştirmek** işlevi ad/değer çiftlerine form verilerini serileştirir.</span><span class="sxs-lookup"><span data-stu-id="c682e-148">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="c682e-149">Form verileri sunucuya göndermek için arama `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="c682e-149">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="c682e-150">İstek tamamlandıktan sonra `.success()` veya `.error()` işleyicisi, kullanıcı için uygun bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c682e-150">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="c682e-151">Gönderen basit türler</span><span class="sxs-lookup"><span data-stu-id="c682e-151">Sending Simple Types</span></span>

<span data-ttu-id="c682e-152">Önceki bölümlerde, Web API'si için bir model sınıfının bir örneği seri durumdan bir karmaşık tür gönderdik.</span><span class="sxs-lookup"><span data-stu-id="c682e-152">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="c682e-153">Ayrıca, bir dize gibi basit türler de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c682e-153">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="c682e-154">Basit bir tür göndermeden önce değerin bir karmaşık türü yerine sarmalama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c682e-154">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="c682e-155">Bu, sunucu tarafında model doğrulama avantajlarını sağlar ve gerekirse modelinizi genişletmek daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c682e-155">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="c682e-156">Basit bir tür göndermek için temel adımlar aynıdır, ancak iki küçük farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="c682e-156">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="c682e-157">İlk olarak, denetleyicisi, parametre adı ile tasarlamanız gerekir **FromBody** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c682e-157">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="c682e-158">Varsayılan olarak, Web API'si basit türler istek URI'SİNDEN almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c682e-158">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="c682e-159">**FromBody** öznitelik değeri gövdeden okunacak Web API söyler.</span><span class="sxs-lookup"><span data-stu-id="c682e-159">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="c682e-160">Web API yanıt gövdesinin en fazla bir kez, bu nedenle yalnızca tek bir eylem parametresinin gövdeden gelebilir okur.</span><span class="sxs-lookup"><span data-stu-id="c682e-160">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="c682e-161">Gövdeden birden çok değer almanız gerekirse, bir karmaşık tür tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c682e-161">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="c682e-162">İkinci olarak, istemci aşağıdaki biçimde değeri göndermesi gerekiyor:</span><span class="sxs-lookup"><span data-stu-id="c682e-162">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="c682e-163">Özellikle, ad/değer çiftinin ad bölümünü basit bir tür için boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c682e-163">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="c682e-164">Tüm tarayıcılar bu için HTML formları desteklemez, ancak, bu biçim şu şekilde oluştur:</span><span class="sxs-lookup"><span data-stu-id="c682e-164">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="c682e-165">Bir örnek formu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c682e-165">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="c682e-166">Ve form değer göndermek için komut dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="c682e-166">And here is the script to submit the form value.</span></span> <span data-ttu-id="c682e-167">Tek fark önceki komut dosyası içine geçirilen bağımsız değişken, **sonrası** işlevi.</span><span class="sxs-lookup"><span data-stu-id="c682e-167">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="c682e-168">Basit bir tür dizisi göndermek için aynı yaklaşımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c682e-168">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="c682e-169">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c682e-169">Additional Resources</span></span>

[<span data-ttu-id="c682e-170">Bölüm 2: Karşıya dosya yükleme ve çok parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="c682e-170">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
