---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072870"
---
<span data-ttu-id="4557a-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Aşağıdaki özellikleri `Movie` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4557a-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="4557a-102">`Movie` Sınıfı içerir:</span><span class="sxs-lookup"><span data-stu-id="4557a-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="4557a-103">`ID` Alan veritabanı için birincil anahtar tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4557a-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="4557a-104">`[DataType(DataType.Date)]`:  [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) özniteliği (tarih) veri türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="4557a-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="4557a-105">Bu öznitelik ile:</span><span class="sxs-lookup"><span data-stu-id="4557a-105">With this attribute:</span></span>

  * <span data-ttu-id="4557a-106">Kullanıcının tarih alanı saat bilgilerini girmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4557a-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="4557a-107">Yalnızca tarih görüntülenen, olmayan zaman bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="4557a-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="4557a-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) bir sonraki öğreticide ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4557a-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>