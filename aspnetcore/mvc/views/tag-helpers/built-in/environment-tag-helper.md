---
title: ASP.NET core'da ortam etiketi Yardımcısı
author: pkellner
description: Tüm özellikler dahil olmak üzere tanımlanan ASP.NET Core ortam etiketi Yardımcısı
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 379f58ed37329f047d53adf1dcfdfd2ad6a6ca4e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067203"
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="27893-103">ASP.NET core'da ortam etiketi Yardımcısı</span><span class="sxs-lookup"><span data-stu-id="27893-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="27893-104">Tarafından [Peter Kellner](http://peterkellner.net), [Hisham Bin Ateya](https://twitter.com/hishambinateya), ve [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="27893-104">By [Peter Kellner](http://peterkellner.net), [Hisham Bin Ateya](https://twitter.com/hishambinateya), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="27893-105">Ortam etiketi Yardımcısı koşullu olarak geçerli göre kapalı içeriğini işler [barındırma ortamı](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="27893-105">The Environment Tag Helper conditionally renders its enclosed content based on the current [hosting environment](xref:fundamentals/environments).</span></span> <span data-ttu-id="27893-106">Ortam etiketi Yardımcısı'nın tek öznitelik `names`, ortam adlarının virgülle ayrılmış listesidir.</span><span class="sxs-lookup"><span data-stu-id="27893-106">The Environment Tag Helper's single attribute, `names`, is a comma-separated list of environment names.</span></span> <span data-ttu-id="27893-107">Sağlanan ortam adları geçerli ortamı hiçbiriyle, ekteki içeriğin işlenir.</span><span class="sxs-lookup"><span data-stu-id="27893-107">If any of the provided environment names match the current environment, the enclosed content is rendered.</span></span>

<span data-ttu-id="27893-108">Etiket Yardımcıları genel bakış için bkz. <xref:mvc/views/tag-helpers/intro>.</span><span class="sxs-lookup"><span data-stu-id="27893-108">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="27893-109">Ortam etiketi Yardımcısı öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="27893-109">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="27893-110">adlar</span><span class="sxs-lookup"><span data-stu-id="27893-110">names</span></span>

<span data-ttu-id="27893-111">`names` Tek bir barındırma ortamı adı veya işleme ekteki içeriğin tetikleyen ortam adları barındırma virgülle ayrılmış listesini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="27893-111">`names` accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="27893-112">Tarafından döndürülen değeri, geçerli ortam değerlerini karşılaştırılır [IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*).</span><span class="sxs-lookup"><span data-stu-id="27893-112">Environment values are compared to the current value returned by [IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*).</span></span> <span data-ttu-id="27893-113">Karşılaştırma çalışması yoksayar.</span><span class="sxs-lookup"><span data-stu-id="27893-113">The comparison ignores case.</span></span>

<span data-ttu-id="27893-114">Aşağıdaki örnek, bir ortam etiketi Yardımcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="27893-114">The following example uses an Environment Tag Helper.</span></span> <span data-ttu-id="27893-115">Barındırma ortamı hazırlık veya üretim olması durumunda içeriğinin işlenip:</span><span class="sxs-lookup"><span data-stu-id="27893-115">The content is rendered if the hosting environment is Staging or Production:</span></span>

```cshtml
<environment names="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

::: moniker range=">= aspnetcore-2.0"

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="27893-116">dahil etme ve dışlama öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="27893-116">include and exclude attributes</span></span>

<span data-ttu-id="27893-117">`include` & `exclude` dahil veya hariç tutulan barındırma ortamı adlarını temel alarak ekteki içeriğin işleme öznitelikleri denetimi.</span><span class="sxs-lookup"><span data-stu-id="27893-117">`include` & `exclude` attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include"></a><span data-ttu-id="27893-118">include</span><span class="sxs-lookup"><span data-stu-id="27893-118">include</span></span>

<span data-ttu-id="27893-119">`include` Özelliği için benzer bir davranış gösteriyor `names` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="27893-119">The `include` property exhibits similar behavior to the `names` attribute.</span></span> <span data-ttu-id="27893-120">Listelenen bir ortam `include` öznitelik değeri, uygulamanın barındırma ortamına eşleşmelidir ([IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*)) içeriği işlemek için `<environment>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="27893-120">An environment listed in the `include` attribute value must match the app's hosting environment ([IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*)) to render the content of the `<environment>` tag.</span></span>

```cshtml
<environment include="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude"></a><span data-ttu-id="27893-121">exclude</span><span class="sxs-lookup"><span data-stu-id="27893-121">exclude</span></span>

<span data-ttu-id="27893-122">Tersine `include` özniteliği, içeriğini `<environment>` etiket listede bir ortam barındırma ortamı eşleşmediğinde işlenir `exclude` öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="27893-122">In contrast to the `include` attribute, the content of the `<environment>` tag is rendered when the hosting environment doesn't match an environment listed in the `exclude` attribute value.</span></span>

```cshtml
<environment exclude="Development">
    <strong>HostingEnvironment.EnvironmentName is not Development</strong>
</environment>
```

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="27893-123">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="27893-123">Additional resources</span></span>

* <xref:fundamentals/environments>
