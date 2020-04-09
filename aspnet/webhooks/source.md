---
uid: webhooks/source
title: ASP.NET WebHooks kaynak kodu ve NuGet paketleri | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET WebHooks kaynak kodu ve NuGet paketlerine bağlantılar
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675315"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="aa315-103">ASP.NET WebHooks kaynak kodu ve NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="aa315-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="aa315-104">Microsoft ASP.NET WebHooks, Microsoft ASP.NET modül ailesinin bir parçasıdır ve [GitHub'da Açık Kaynak Projesi](https://github.com/aspnet/WebHooks)olarak barındırılır.</span><span class="sxs-lookup"><span data-stu-id="aa315-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="aa315-105">Bu, katkıları kabul ettiğimiz anlamına gelir, ancak lütfen çekme isteği göndermeden önce [Katkı Yönergeleri'ne](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="aa315-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="aa315-106">Şu anda okuduğunuz bu çevrimiçi dokümantasyon aynı zamanda [GitHub'da Açık Kaynak](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) olarak barındırılır ve katkıları da kabul eder.</span><span class="sxs-lookup"><span data-stu-id="aa315-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="aa315-107">NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="aa315-107">NuGet packages</span></span>

<span data-ttu-id="aa315-108">[NuGet paketleri](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) üç bölüme ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="aa315-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="aa315-109">[Ortak](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Gönderenler ve alıcılar arasında paylaşılan ortak bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="aa315-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="aa315-110">[Gönderen](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Kendi WebHook'larınızı başkalarına göndermeyi destekleyen paketler kümesi.</span><span class="sxs-lookup"><span data-stu-id="aa315-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="aa315-111">WebHooks gönderme [işlevi, WebHooks Gönderme'de](sending/senders.md)daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="aa315-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="aa315-112">[Alıcılar](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Başkalarından WebHook almayı destekleyen paketler kümesi.</span><span class="sxs-lookup"><span data-stu-id="aa315-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="aa315-113">WebHooks alma işlevi [WebHooks alma](receiving/index.md)daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="aa315-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
