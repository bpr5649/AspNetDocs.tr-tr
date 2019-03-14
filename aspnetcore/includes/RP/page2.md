---
ms.openlocfilehash: 7d84624165abd0cf61d3b94f82f3d25f78dbc630
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073956"
---
<span data-ttu-id="a1143-101">`<form method="post">` Öğesi bir [Form etiketi Yardımcısı](xref:mvc/views/working-with-forms#the-form-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="a1143-101">The `<form method="post">` element is a [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="a1143-102">Form etiketi Yardımcısı otomatik olarak içeren bir [antiforgery belirteci](xref:security/anti-request-forgery).</span><span class="sxs-lookup"><span data-stu-id="a1143-102">The Form Tag Helper automatically includes an [antiforgery token](xref:security/anti-request-forgery).</span></span>

<span data-ttu-id="a1143-103">Yapı iskelesi altyapısı Razor işaretlemesi için her bir alan (ID dışında) modelinde aşağıdakine benzer oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a1143-103">The scaffolding engine creates Razor markup for each field in the model (except the ID) similar to the following:</span></span>

[!code-cshtml[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=15-20)]

<span data-ttu-id="a1143-104">[Doğrulama etiket Yardımcıları](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` ve ` <span asp-validation-for`) doğrulama hataları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a1143-104">The [Validation Tag Helpers](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` and ` <span asp-validation-for`) display validation errors.</span></span> <span data-ttu-id="a1143-105">Doğrulama Bu seriyi ilerleyen bölümlerinde daha ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="a1143-105">Validation is covered in more detail later in this series.</span></span>

<span data-ttu-id="a1143-106">[Etiket etiketi Yardımcısı](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) etiketi başlığını oluşturur ve `for` özniteliğini `Title` özelliği.</span><span class="sxs-lookup"><span data-stu-id="a1143-106">The [Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) generates the label caption and `for` attribute for the `Title` property.</span></span>

<span data-ttu-id="a1143-107">[Giriş etiketi Yardımcısı](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) kullanan [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) öznitelikleri ve jQuery doğrulaması istemci tarafında gereken HTML öznitelikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1143-107">The [Input Tag Helper](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) uses the [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span>
