---
uid: webhooks/receiving/dependencies
title: ASP.NET Web kancaları alıcı bağımlılıkları | Microsoft Docs
author: rick-anderson
description: Alıcı bağımlılıkları ve ASP.NET Web kancaları bağımlılık ekleme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: c44cfe3ed310aa728a989b108c410e8786e4f514
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073263"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Web kancaları alıcı bağımlılıkları

Microsoft ASP.NET WebHooks bağımlılık ekleme düşünülerek tasarlanmıştır. Çoğu bağımlılıkları sisteminde diğer uygulamaları ile bir bağımlılık ekleme altyapısı kullanılarak değiştirilebilir.

Lütfen [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) alıcı bağımlılıkları listesi. Hiçbir bağımlılık kayıtlı ise varsayılan bir uygulama kullanılır. Lütfen [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) varsayılan uygulamaları listesi.
