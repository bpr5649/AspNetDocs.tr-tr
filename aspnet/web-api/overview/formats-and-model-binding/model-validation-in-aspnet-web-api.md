---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Model doğrulama ASP.NET Web API'si - ASP.NET 4.x
author: MikeWasson
description: Genel Bakış ASP.NET Web API'de model doğrulama ASP.NET 4.x.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: d4e792f8cc2f79c2ab82c5a74fd50f49475fac4f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404578"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="0adb9-103">ASP.NET Web API'de model doğrulama</span><span class="sxs-lookup"><span data-stu-id="0adb9-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="0adb9-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0adb9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0adb9-105">Bu makalede, web API'NİZİN doğrulama hataları işlemek modellerinize eklemek ve veri doğrulama için ek açıklamalarını kullanma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0adb9-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="0adb9-106">İstemci web API'nize veri gönderdiğinde, genellikle herhangi bir işlem gerçekleştirmeden önce verileri doğrulamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="0adb9-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="0adb9-107">Veri ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="0adb9-107">Data Annotations</span></span>

<span data-ttu-id="0adb9-108">ASP.NET Web API'de öznitelikleri kullanabilirsiniz [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) modelinize göre özellikler için doğrulama kurallarını ayarlamak için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="0adb9-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="0adb9-109">Şu model göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="0adb9-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="0adb9-110">ASP.NET MVC'de model doğrulama kullandıysanız, bu tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="0adb9-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="0adb9-111">**Gerekli** öznitelik yazan `Name` özelliği null olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0adb9-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="0adb9-112">**Aralığı** öznitelik yazan `Weight` sıfır ile 999 arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0adb9-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="0adb9-113">Bir istemci aşağıdaki JSON gösterimine sahip bir POST isteği gönderir varsayalım:</span><span class="sxs-lookup"><span data-stu-id="0adb9-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="0adb9-114">İstemci içermediği gördüğünüz `Name` olarak işaretlenmiş özelliği gerekli.</span><span class="sxs-lookup"><span data-stu-id="0adb9-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="0adb9-115">Web API dönüştürür JSON'a ne zaman bir `Product` örneği, nasıl doğruladığı `Product` karşı doğrulama öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="0adb9-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="0adb9-116">Denetleyici eyleminizi model geçerli olup olmadığını kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0adb9-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="0adb9-117">Model doğrulaması istemci verilerini güvenli olduğu garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="0adb9-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="0adb9-118">Ek doğrulama diğer uygulama katmanında gerekli.</span><span class="sxs-lookup"><span data-stu-id="0adb9-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="0adb9-119">(Örneğin, veri katmanı yabancı anahtar kısıtlamalarını zorlayabilir.) Öğreticiyi [Entity Framework ile Web API kullanarak](../data/using-web-api-with-entity-framework/part-1.md) bu sorunlardan bazıları keşfediyor.</span><span class="sxs-lookup"><span data-stu-id="0adb9-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="0adb9-120">**"Eksik posta"**: Eksik posta istemcisi bazı özellikleri dışına çıktığında gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="0adb9-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="0adb9-121">Örneğin, aşağıdaki istemcinin gönderdiği varsayalım:</span><span class="sxs-lookup"><span data-stu-id="0adb9-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="0adb9-122">Burada, istemci için değerleri belirtmediniz `Price` veya `Weight`.</span><span class="sxs-lookup"><span data-stu-id="0adb9-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="0adb9-123">JSON biçimlendirici sıfır eksik özellikleri için varsayılan değeri atar.</span><span class="sxs-lookup"><span data-stu-id="0adb9-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="0adb9-124">Bu özellikler için geçerli bir değer sıfır olduğundan model durumu geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="0adb9-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="0adb9-125">Bu bir sorun olup olmadığını, senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0adb9-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="0adb9-126">Örneğin, bir update işleminde "sıfır" ve "ayarlı değil." ayırt etmek isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0adb9-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="0adb9-127">Bir değer ayarlamak için istemcileri zorlamak için özelliği boş değer atanabilir ve ayarlanmış olun **gerekli** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="0adb9-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="0adb9-128">**"Aşırı gönderme"**: Bir istemci de gönderebilirsiniz *daha fazla* beklediğinizden daha veri.</span><span class="sxs-lookup"><span data-stu-id="0adb9-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="0adb9-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0adb9-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="0adb9-130">Burada, JSON yok ("rengi") bir özellik içeren `Product` modeli.</span><span class="sxs-lookup"><span data-stu-id="0adb9-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="0adb9-131">Bu durumda, JSON biçimlendirici, yalnızca bu değeri yoksayar.</span><span class="sxs-lookup"><span data-stu-id="0adb9-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="0adb9-132">(Aynı XML biçimlendiricisi desteklemez.) Model salt okunur olmasını istediğiniz özellikler varsa fazla posta sorunlara neden olur.</span><span class="sxs-lookup"><span data-stu-id="0adb9-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="0adb9-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0adb9-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="0adb9-134">Güncelleştirilecek kullanıcı istemediğiniz `IsAdmin` özelliği ve kendileri için yöneticileri Yükselt!</span><span class="sxs-lookup"><span data-stu-id="0adb9-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="0adb9-135">Güvenli stratejisi, istemcinin göndermek için izin verilenden tam olarak eşleşen bir model sınıfı kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="0adb9-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="0adb9-136">Brad Wilson'ın blog gönderisi "[giriş doğrulaması vs. Model doğrulama ASP.NET mvc'de](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"eksik posta ve fazla posta iyi bir tartışma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0adb9-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="0adb9-137">ASP.NET MVC 2 hakkında posta olsa da, sorunları Web API'sine yine de ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="0adb9-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="0adb9-138">Doğrulama hataları işleme</span><span class="sxs-lookup"><span data-stu-id="0adb9-138">Handling Validation Errors</span></span>

<span data-ttu-id="0adb9-139">Doğrulama başarısız olduğunda web API'si otomatik olarak bir hata istemciye döndürmez.</span><span class="sxs-lookup"><span data-stu-id="0adb9-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="0adb9-140">Model durumu denetlemek ve uygun şekilde yanıtlanması için en fazla denetleyici eylemi var.</span><span class="sxs-lookup"><span data-stu-id="0adb9-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="0adb9-141">Denetleyici eylemini çağrılmadan önce model durumunu denetlemek için bir eyleme eylem filtresi de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0adb9-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="0adb9-142">Aşağıdaki kodda bir örnek gösterilir:</span><span class="sxs-lookup"><span data-stu-id="0adb9-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="0adb9-143">Bu filtre, model doğrulama başarısız olursa doğrulama hatalarını içeren bir HTTP yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="0adb9-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="0adb9-144">Bu durumda, denetleyici eylem çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="0adb9-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="0adb9-145">Tüm Web APİ'si denetleyicilerinin için bu filtre uygulamak için filtre bir örneğini ekleme **HttpConfiguration.Filters** yapılandırma sırasında koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="0adb9-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="0adb9-146">Filtre bir özniteliği olarak tek tek denetleyicileri veya denetleyici eylemlerini ayarlamak başka bir seçenektir:</span><span class="sxs-lookup"><span data-stu-id="0adb9-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
