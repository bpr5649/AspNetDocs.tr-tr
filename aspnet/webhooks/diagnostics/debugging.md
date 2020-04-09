---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks hata ayıklama | Microsoft Dokümanlar
author: rick-anderson
description: WebHooksASP.NET hata ayıklama.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675375"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="d9c79-103">ASP.NET WebHooks hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="d9c79-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="d9c79-104">Azure'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="d9c79-104">Debugging in Azure</span></span>

<span data-ttu-id="d9c79-105">Azure'da çalışırken Web Uygulamanızı hata ayıklamak için, [Visual Studio'yu kullanarak Azure Uygulama Hizmeti'ndeki bir web uygulamasının](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)sorun giderme uygulamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="d9c79-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="d9c79-106">Kaynak ve Sembollerle Hata Ayıklama</span><span class="sxs-lookup"><span data-stu-id="d9c79-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="d9c79-107">Kendi kodunuzu hata ayıklamanın yanı sıra, webhooks'ASP.NET doğrudan Microsoft'a ve aslında tüm .NET'e hata ayıklamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d9c79-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="d9c79-108">Bu, yerel veya uzaktan hata ayıklama olup olmadığını ne olursa olsun çalışır.</span><span class="sxs-lookup"><span data-stu-id="d9c79-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="d9c79-109">İlk olarak, **Hata Ayıklama** ve ardından Seçenekler ve **Ayarlar'a**giderek kaynağı ve simgeleri bulmak için Visual Studio'yu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d9c79-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="d9c79-110">Seçenekleri şu şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d9c79-110">Set the options like this:</span></span>

![Seçenekler ve Ayarlar](_static/SourceSymbols.png)

<span data-ttu-id="d9c79-112">Ardından, kaynağı ve sembolleri indirmek için [symbolsource.org](http://symbolsource.org) bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9c79-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="d9c79-113">Yukarıdaki menünün **Semboller** sekmesine gidin ve sembol konumu olarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d9c79-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="d9c79-114">Ayrıca, önbellek dizininin kısa bir adı olduğundan emin olun; aksi takdirde dosya adları çok uzun olabilir ve bu da sembollerin yüklenmemesi için neden olur.</span><span class="sxs-lookup"><span data-stu-id="d9c79-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="d9c79-115">Örnek bir yol:</span><span class="sxs-lookup"><span data-stu-id="d9c79-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="d9c79-116">Ayarlar buna benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d9c79-116">The settings should look similar to this:</span></span>

![Seçenekler Sembolü Dosya Konumu Örneği](_static/SymSource.png)
