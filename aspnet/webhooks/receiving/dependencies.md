---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks alıcı bağımlılıkları | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET WebHooks'ta alıcı bağımlılıkları ve bağımlılık enjeksiyonu.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675207"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks alıcı bağımlılıkları

Microsoft ASP.NET WebHooks bağımlılık enjeksiyonu göz önünde bulundurularak tasarlanmıştır. Sistemdeki bağımlılıkların çoğu bağımlılık enjeksiyon motoru kullanılarak alternatif uygulamalarla değiştirilebilir.

Alıcı bağımlılıkları listesi için [DependencyScopeExtensions'a](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) bakın. Bağımlılık kaydedilmemişse, varsayılan bir uygulama kullanılır. Varsayılan uygulamaların listesi için [ReceiverServices'e](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) bakın.
