---
uid: webhooks/diagnostics/logging
title: ASP.NET WebHooks günlüğü | Microsoft Dokümanlar
author: rick-anderson
description: WebHooks'ASP.NET oturum açma nasıl yapılacağını.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675352"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET WebHooks günlüğü

Microsoft ASP.NET WebHooks, günlüğe kaydetmeyi sorunları ve sorunları raporlamanın bir yolu olarak kullanır. Varsayılan günlükleri [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) kullanılarak yazılır nerede başka bir günlük akışı gibi [Trace Dinleyici](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) kullanılarak manged olabilir.

Web Uygulamanızı Azure Web Uygulaması olarak dağıtırken, günlükler otomatik olarak alınır ve diğer [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) günlüğüyle birlikte yönetilebilir. Ayrıntılar için lütfen [Azure Uygulama Hizmeti'ndeki web uygulamaları için tanılama günlüğe kaydetme](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Buna ek olarak, günlükleri Visual Studio kullanarak [Azure App Service bir web uygulaması Troubleshoot](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)açıklandığı gibi Visual Studio içinden düz elde edilebilir.

## <a name="redirecting-logs"></a>Günlükleri Yönlendirme

[System.Diagnostics.Trace'e](https://msdn.microsoft.com/library/system.diagnostics.trace)günlük yazmak yerine, [Log4Net](http://logging.apache.org/log4net/) ve NLog gibi bir günlük yöneticisine doğrudan oturum açabilen alternatif bir günlük uygulaması sağlamak [mümkündür.](http://nlog-project.org/) Sadece [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) bir uygulama sağlamak ve seçtiğiniz bir bağımlılık enjeksiyon motoru ile kayıt ve Microsoft ASP.NET WebHooks tarafından alınan alacak. Ayrıntılar için lütfen [ASP.NET Web API 2'de Bağımlılık Enjeksiyonu'na](https://www.asp.net/web-api/overview/advanced/dependency-injection) bakın.
