---
uid: webhooks/source
title: ASP.NET Web kancaları kaynak kodu ve NuGet paketleri | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancaları kaynak kodu ve NuGet paketlerinin bağlantıları
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633065"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="c2b12-103">ASP.NET Web kancaları kaynak kodu ve NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="c2b12-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="c2b12-104">Microsoft ASP.NET Web kancaları Microsoft ASP.NET modül ailesinin bir parçasıdır ve [GitHub üzerinde açık kaynak proje](https://github.com/aspnet/WebHooks)olarak barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c2b12-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="c2b12-105">Bu, katkıların kabul ettiğimiz anlamına gelir ancak çekme isteği göndermeden önce lütfen [katkı yönergelerine](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="c2b12-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="c2b12-106">Artık okuduğunuz bu çevrimiçi belgeler ayrıca [GitHub 'Da açık kaynak](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) olarak barındırılır ve ayrıca katkıları kabul eder.</span><span class="sxs-lookup"><span data-stu-id="c2b12-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="c2b12-107">NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="c2b12-107">NuGet packages</span></span>

<span data-ttu-id="c2b12-108">[NuGet paketleri](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) üç parçaya ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="c2b12-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="c2b12-109">[Ortak](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Gönderenler ve alıcılar arasında paylaşılan ortak bir paket.</span><span class="sxs-lookup"><span data-stu-id="c2b12-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="c2b12-110">[Gönderici](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): başkalarına kendi web kancaları göndermeyi destekleyen bir paket kümesi.</span><span class="sxs-lookup"><span data-stu-id="c2b12-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="c2b12-111">Web kancaları gönderme işlevselliği, [Web kancaları gönderme](sending/senders.md)konusunda daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c2b12-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="c2b12-112">[Alıcılar](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): başkalarından Web kancalarını almayı destekleyen bir paket kümesi.</span><span class="sxs-lookup"><span data-stu-id="c2b12-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="c2b12-113">Web kancalarını alma işlevselliği, [Web kancalarını alma](receiving/index.md)konusunda daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c2b12-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
