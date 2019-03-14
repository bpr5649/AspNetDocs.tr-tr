---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077478"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="95b29-101">ASP.NET Core yanıt önbelleğe alma örneği</span><span class="sxs-lookup"><span data-stu-id="95b29-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="95b29-102">Bu örnek ASP.NET Core kullanımını [yanıt önbelleğe alma ara yazılımı](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="95b29-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="95b29-103">Uygulama, dizin sayfasıyla yanıt dahil olmak üzere bir `Cache-Control` önbelleğe alma davranışını yapılandırmak için üst bilgi.</span><span class="sxs-lookup"><span data-stu-id="95b29-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="95b29-104">Uygulama ayrıca ayarlar `Vary` yanıt yalnızca şu durumlarda hizmet önbelleğini yapılandırmak için üst bilgi `Accept-Encoding` sonraki istekleri üstbilgisinin özgün istekteki eşleşen.</span><span class="sxs-lookup"><span data-stu-id="95b29-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="95b29-105">Örnek çalışırken, dizin sayfası depolandığında ve 10 saniye boyunca önbelleğe önbelleğinden sunulur.</span><span class="sxs-lookup"><span data-stu-id="95b29-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
