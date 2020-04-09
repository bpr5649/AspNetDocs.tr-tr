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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET WebHooks kaynak kodu ve NuGet paketleri

Microsoft ASP.NET WebHooks, Microsoft ASP.NET modül ailesinin bir parçasıdır ve [GitHub'da Açık Kaynak Projesi](https://github.com/aspnet/WebHooks)olarak barındırılır. Bu, katkıları kabul ettiğimiz anlamına gelir, ancak lütfen çekme isteği göndermeden önce [Katkı Yönergeleri'ne](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) bakın.

Şu anda okuduğunuz bu çevrimiçi dokümantasyon aynı zamanda [GitHub'da Açık Kaynak](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) olarak barındırılır ve katkıları da kabul eder.

## <a name="nuget-packages"></a>NuGet paketleri

[NuGet paketleri](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) üç bölüme ayrılmıştır:

* [Ortak](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Gönderenler ve alıcılar arasında paylaşılan ortak bir pakettir.

* [Gönderen](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Kendi WebHook'larınızı başkalarına göndermeyi destekleyen paketler kümesi. WebHooks gönderme [işlevi, WebHooks Gönderme'de](sending/senders.md)daha ayrıntılı olarak açıklanmıştır.

* [Alıcılar](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Başkalarından WebHook almayı destekleyen paketler kümesi. WebHooks alma işlevi [WebHooks alma](receiving/index.md)daha ayrıntılı olarak açıklanmıştır.
