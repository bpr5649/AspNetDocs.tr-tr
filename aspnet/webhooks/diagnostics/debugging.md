---
uid: webhooks/diagnostics/debugging
title: ASP.NET hata ayıklama Web kancaları | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancaları hata ayıklamak nasıl.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077412"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="c9b49-103">ASP.NET hata ayıklama Web kancaları</span><span class="sxs-lookup"><span data-stu-id="c9b49-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="c9b49-104">Azure'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c9b49-104">Debugging in Azure</span></span>

<span data-ttu-id="c9b49-105">Web uygulamanızı Azure'da çalışırken hata ayıklama için öğreticiye bakın [Visual Studio kullanarak Azure App Service'te bir web uygulaması sorunlarını giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="c9b49-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="c9b49-106">Kaynak ve simgeler ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c9b49-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="c9b49-107">Kendi kod hata ayıklama ek olarak, Microsoft ASP.NET WebHooks doğrudan ve hatta hata ayıklamak mümkündür tüm .NET.</span><span class="sxs-lookup"><span data-stu-id="c9b49-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="c9b49-108">Bu, yerel olarak veya uzaktan hata ayıklama bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9b49-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="c9b49-109">İlk olarak, giderek kaynak ve simgeleri bulmak için Visual Studio yapılandırma **hata ayıklama** ardından **seçenekler ve ayarlar**.</span><span class="sxs-lookup"><span data-stu-id="c9b49-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="c9b49-110">Bu gibi seçenekleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c9b49-110">Set the options like this:</span></span>

![Seçenekler ve ayarlar](_static/SourceSymbols.png)

<span data-ttu-id="c9b49-112">Ardından bir bağlantı ekleyin [symbolsource.org](http://symbolsource.org) kaynak ve sembol karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="c9b49-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="c9b49-113">Git **sembolleri** sekmesinde menüsünden izleyebilirim ve bir simge konumu olarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c9b49-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="c9b49-114">Ayrıca, önbellek dizini kısa bir ad olduğundan emin olun; Aksi takdirde dosya adları değil yüklenecek semboller neden olacak uzun elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9b49-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="c9b49-115">Bir örnek yoludur:</span><span class="sxs-lookup"><span data-stu-id="c9b49-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="c9b49-116">Ayarları şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c9b49-116">The settings should look similar to this:</span></span>

![Seçenekleri sembol dosyası konumu örneği](_static/SymSource.png)
