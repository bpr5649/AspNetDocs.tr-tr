---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: MVC Yürütme Sürecinin ASP.NET Anlaşılması | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET MVC çerçevesinin tarayıcı isteğini adım adım nasıl işlediğini öğrenin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541032"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC Yürütme İşlemini Anlama

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET MVC çerçevesinin tarayıcı isteğini adım adım nasıl işlediğini öğrenin.

MVC tabanlı bir web uygulaması ASP.NETna yapılan istekler ilk olarak bir HTTP modülü olan **UrlRoutingModule** nesnesi üzerinden geçer. Bu modül isteği ayrışdırır ve rota seçimini gerçekleştirir. **UrlRoutingModule** nesnesi geçerli istekle eşleşen ilk rota nesnesini seçer. (Rota nesnesi, **RouteBase'i**uygulayan bir sınıftır ve genellikle **Rota** sınıfının bir örneğidir.) Hiçbir rota eşleşmiyorsa, **UrlRoutingModule** nesnesi hiçbir şey yapmaz ve isteğin normal ASP.NET veya IIS istek işlemesine geri dönmesini sağlar.

**UrlRoutingModule** nesnesi, seçili **Rota** nesnesinden, **Rota** nesnesiyle ilişkili **IRouteHandler** nesnesini alır. Genellikle, bir MVC uygulamasında, bu **MvcRouteHandler**bir örneği olacaktır. **IRouteHandler** örneği bir **IHttpHandler** nesnesi oluşturur ve **ihttpcontext** nesnesini geçirir. Varsayılan olarak, MVC için **IHttpHandler** örneği **MvcHandler** nesnesidir. **MvcHandler** nesnesi daha sonra isteği sonunda işleyecek denetleyiciyi seçer.

> [!NOTE]
> Bir ASP.NET MVC Web uygulaması IIS 7.0'da çalıştığında, MVC projeleri için dosya adı uzantısı gerekmez. Ancak, IIS 6.0'da işleyici, .mvc dosya adı uzantısını ASP.NET ISAPI DLL ile eşlenizi gerektirir.

Modül ve işleyici, ASP.NET MVC çerçevesinin giriş noktalarıdır. Aşağıdaki eylemleri gerçekleştirirler:

- Bir MVC Web uygulamasında uygun denetleyiciyi seçin.
- Belirli bir denetleyici örneği edinin.
- Denetleyicinin Yürüt **metodunu** arayın.

Aşağıda, bir MVC Web projesinin yürütme aşamaları listelenebilmiştir:

- Uygulama için ilk isteği alma 

    - Global.asax **dosyasında, Route** nesneleri **RouteTable** nesnesine eklenir.
- Yönlendirme yapma 

    - **UrlRoutingModule** modülü, **RouteTable** koleksiyonundaki ilk eşleşen **Route** nesnesini kullanır ve daha sonra **bir İstek Bağlamı** **(IHttpContext)** nesnesi oluşturmak için kullandığı **RouteData** nesnesini oluşturur.
- MVC istek işleyicisi oluşturma 

    - **MvcRouteHandler** nesnesi **MvcHandler** sınıfının bir örneğini oluşturur ve **RequestContext** örneğini geçirir.
- Denetleyici oluşturma 

    - **MvcHandler** nesnesi, **iControllerFactory** nesnesini (genellikle **DefaultControllerFactory** sınıfının bir örneği) tanımlamak için **İstek Bağlamı** örneğini kullanır.
- Yürütme denetleyicisi - **MvcHandler** örneği denetleyicinin **Execute** yöntemini çağırır. |
- Eylemi çağırma 

    - Denetleyicilerin çoğu **Denetleyici** taban sınıfından devralır. Bunu yapan denetleyiciler için, denetleyiciyle ilişkili **ControllerActionInvoker** nesnesi, denetleyici sınıfının hangi eylem yöntemini çağırarak çağıracaklarını belirler ve sonra bu yöntemi çağırır.
- Sonucu çalıştırma 

    - Tipik bir eylem yöntemi kullanıcı girişi alabilir, uygun yanıt verilerini hazırlayabilir ve sonuç türünü döndürerek sonucu çalıştırabilir. Yürütülebilir yerleşik sonuç türleri şunlardır: **ViewResult** (bir görünüm işler ve en sık kullanılan sonuç türüdür), **RedirectToRouteResult**, **ReDirectResult**, **ContentResult**, **JsonResult**, ve **EmptyResult**.
