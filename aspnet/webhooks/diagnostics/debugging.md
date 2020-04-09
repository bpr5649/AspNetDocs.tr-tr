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
# <a name="aspnet-webhooks-debugging"></a>ASP.NET WebHooks hata ayıklama

## <a name="debugging-in-azure"></a>Azure'da hata ayıklama

Azure'da çalışırken Web Uygulamanızı hata ayıklamak için, [Visual Studio'yu kullanarak Azure Uygulama Hizmeti'ndeki bir web uygulamasının](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)sorun giderme uygulamasına bakın.

## <a name="debugging-with-source-and-symbols"></a>Kaynak ve Sembollerle Hata Ayıklama

Kendi kodunuzu hata ayıklamanın yanı sıra, webhooks'ASP.NET doğrudan Microsoft'a ve aslında tüm .NET'e hata ayıklamak mümkündür. Bu, yerel veya uzaktan hata ayıklama olup olmadığını ne olursa olsun çalışır. İlk olarak, **Hata Ayıklama** ve ardından Seçenekler ve **Ayarlar'a**giderek kaynağı ve simgeleri bulmak için Visual Studio'yu yapılandırın. Seçenekleri şu şekilde ayarlayın:

![Seçenekler ve Ayarlar](_static/SourceSymbols.png)

Ardından, kaynağı ve sembolleri indirmek için [symbolsource.org](http://symbolsource.org) bağlantı ekleyin. Yukarıdaki menünün **Semboller** sekmesine gidin ve sembol konumu olarak aşağıdakileri ekleyin:

```
http://srv.symbolsource.org/pdb/Public
```

Ayrıca, önbellek dizininin kısa bir adı olduğundan emin olun; aksi takdirde dosya adları çok uzun olabilir ve bu da sembollerin yüklenmemesi için neden olur. Örnek bir yol:

```
C:\SymCache
```

Ayarlar buna benzer olmalıdır:

![Seçenekler Sembolü Dosya Konumu Örneği](_static/SymSource.png)
