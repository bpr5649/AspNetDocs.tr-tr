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
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="07e2c-103">ASP.NET WebHooks alıcı bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="07e2c-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="07e2c-104">Microsoft ASP.NET WebHooks bağımlılık enjeksiyonu göz önünde bulundurularak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="07e2c-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="07e2c-105">Sistemdeki bağımlılıkların çoğu bağımlılık enjeksiyon motoru kullanılarak alternatif uygulamalarla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="07e2c-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="07e2c-106">Alıcı bağımlılıkları listesi için [DependencyScopeExtensions'a](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) bakın.</span><span class="sxs-lookup"><span data-stu-id="07e2c-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="07e2c-107">Bağımlılık kaydedilmemişse, varsayılan bir uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07e2c-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="07e2c-108">Varsayılan uygulamaların listesi için [ReceiverServices'e](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) bakın.</span><span class="sxs-lookup"><span data-stu-id="07e2c-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
