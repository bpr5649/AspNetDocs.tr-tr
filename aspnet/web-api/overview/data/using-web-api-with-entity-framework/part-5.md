---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Veri aktarımı nesneleri (Dto) oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 1af29955e8040c34840d4c77fc2006f59d2324dd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395283"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="47d53-102">Veri Aktarımı Nesneleri (DTO) Oluşturma</span><span class="sxs-lookup"><span data-stu-id="47d53-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="47d53-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="47d53-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="47d53-104">Projeyi yükle</span><span class="sxs-lookup"><span data-stu-id="47d53-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="47d53-105">Sağ istemciye veritabanı varlıklarını şimdi web API kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="47d53-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="47d53-106">İstemci, doğrudan veritabanı tablolarına eşleyen veri alır.</span><span class="sxs-lookup"><span data-stu-id="47d53-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="47d53-107">Ancak, her zaman iyi bir fikir değildir.</span><span class="sxs-lookup"><span data-stu-id="47d53-107">However, that's not always a good idea.</span></span> <span data-ttu-id="47d53-108">Bazen istemciye göndermek veri şeklini değiştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="47d53-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="47d53-109">Örneğin, aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47d53-109">For example, you might want to:</span></span>

- <span data-ttu-id="47d53-110">Döngüsel başvurular (önceki bölüme bakın) kaldırın.</span><span class="sxs-lookup"><span data-stu-id="47d53-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="47d53-111">İstemciler görüntülemek için görmemesi belirli özellikleri gizleyin.</span><span class="sxs-lookup"><span data-stu-id="47d53-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="47d53-112">Yükü boyutunu azaltmak için bazı özellikler atlayın.</span><span class="sxs-lookup"><span data-stu-id="47d53-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="47d53-113">İstemciler için daha kullanışlı hale getirmek için iç içe geçmiş nesneleri içeren nesne grafiklerini düzleştirin.</span><span class="sxs-lookup"><span data-stu-id="47d53-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="47d53-114">"Güvenlik açıklarını aşırı gönderme" kaçının.</span><span class="sxs-lookup"><span data-stu-id="47d53-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="47d53-115">(Bkz [Model doğrulama](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) fazla posta hakkında ayrıntılı bilgi için.)</span><span class="sxs-lookup"><span data-stu-id="47d53-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="47d53-116">Veritabanı katmanı, hizmet katmanından ayırırsınız.</span><span class="sxs-lookup"><span data-stu-id="47d53-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="47d53-117">Bunu gerçekleştirmek için tanımlayabileceğiniz bir *veri aktarımı nesnesi* (DTO).</span><span class="sxs-lookup"><span data-stu-id="47d53-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="47d53-118">Bir DTO verileri ağ üzerinden nasıl gönderilir tanımlayan bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="47d53-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="47d53-119">Kitap varlığı ile nasıl çalıştığına bakalım.</span><span class="sxs-lookup"><span data-stu-id="47d53-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="47d53-120">Modeller klasörü içinde iki DTO sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="47d53-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="47d53-121">`BookDetailDTO` Sınıfı içeren kitap modelinden hariç tüm özellikler `AuthorName` yazar adını tutacak bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="47d53-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="47d53-122">`BookDTO` Sınıfı içeren bir alt kümesini özelliklerinden `BookDetailDTO`.</span><span class="sxs-lookup"><span data-stu-id="47d53-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="47d53-123">Ardından, iki GET yöntemleri yerine `BooksController` sınıfı sürümleriyle Dto döndürür.</span><span class="sxs-lookup"><span data-stu-id="47d53-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="47d53-124">LINQ kullanacağız **seçin** Dto'lar kitap varlıklardan dönüştürülecek ifade.</span><span class="sxs-lookup"><span data-stu-id="47d53-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="47d53-125">Yeni oluşturulan SQL işte `GetBooks` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="47d53-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="47d53-126">EF LINQ çevirir gördüğünüz **seçin** içine bir SQL SELECT deyimi.</span><span class="sxs-lookup"><span data-stu-id="47d53-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="47d53-127">Son olarak, değişiklik `PostBook` yöntemi bir DTO döndürür.</span><span class="sxs-lookup"><span data-stu-id="47d53-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="47d53-128">Bu öğreticide, biz Dto'lar için el ile kod dönüştürüyoruz.</span><span class="sxs-lookup"><span data-stu-id="47d53-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="47d53-129">Gibi bir kitaplık kullanmak üzere başka bir seçenektir [AutoMapper](http://automapper.org/) dönüştürme otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="47d53-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="47d53-130">[Önceki](part-4.md)
> [İleri](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="47d53-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
