---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[Bunu nasıl yaparım:]  Bir ASP.NET sayfasını HTTP üst bilgisinde dayalı önbellek | Microsoft Docs'
author: rick-anderson
description: Bu video Chris piksel ASP.NET çıktı önbelleğine sayfanın HTTP üst bilgisindeki bilgilere bağlı bir sayfaya nasıl gösterir. İlk olarak, olası HTTP üst...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: c90a3db1357df062909ad0e3b73fdeeb3dc16329
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069792"
---
<a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="522ba-104">[Bunu nasıl yaparım:]  Bir ASP.NET sayfasını HTTP üst bilgisindeki bilgilere bağlı olarak önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="522ba-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>
====================
<span data-ttu-id="522ba-105">tarafından [Chris piksel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="522ba-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="522ba-106">Bu video Chris piksel ASP.NET çıktı önbelleğine sayfanın HTTP üst bilgisindeki bilgilere bağlı bir sayfaya nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="522ba-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="522ba-107">İlk olarak, olası HTTP üstbilgi değerleri gözden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="522ba-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="522ba-108">Ardından, örnek bir sayfa oluşturulur ve ardından "kabul et-language", kullanıcının tarayıcısının dilini alan önbelleğe almayı denetlemek için bir HTTP üstbilgisi değeri içeren VaryByHeader özniteliğine sahip OutputCache yönergesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="522ba-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="522ba-109">IE'de İngilizce'ye ayarlanır ve ardından Fransızca kullanmak üzere ayarlanmış Firefox'ta örnek sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="522ba-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="522ba-110">Son olarak, web.config dosyasında bir CacheProfile önbellek tanımına gitme seçeneği ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="522ba-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="522ba-111">&#9654;(12 dakika) videosunu izleyin</span><span class="sxs-lookup"><span data-stu-id="522ba-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
