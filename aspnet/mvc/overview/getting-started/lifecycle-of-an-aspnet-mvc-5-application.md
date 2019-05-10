---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: Bir ASP.NET MVC 5 uygulamasının yaşam döngüsü | Microsoft Docs
author: cephalin
description: Bir ASP.NET MVC 5 uygulamasının yaşam döngüsü grafikleri bir PDF belgesini indirin. Bu yaşam döngüsü belge MVC yaşam döngüsü üst düzey bir görünümünü sağlar bir...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124091"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>Bir ASP.NET MVC 5 Uygulamasının Yaşam Döngüsü

tarafından [Cephas Bağla](https://github.com/cephalin)

[PDF belgesini indirin](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

Burada HTTP almasını her ASP.NET MVC 5 uygulamasının yaşam döngüsü İstek HTTP yanıtı göndermeyi grafikleri istemciye bir PDF belgesini indirebilirsiniz. ASP.NET MVC Acemi olanlar için eğitim bir aracı hem de de olarak bir başvuru uygulaması belirli yönlerini detaya gitmek için ihtiyacınız olanlar için tasarlanmıştır. PDF belgesinin aşağıdaki özelliklere sahiptir:

- İlgili [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) MVC tümleştirir burada anlamanıza yardımcı olması için aşamaları [ASP.NET uygulama yaşam döngüsü](https://msdn.microsoft.com/library/bb470252.aspx).
- Burada isteği işleme işlem hattı, her bir MVC uygulaması geçtiği ana aşamaları anlayabilmeniz MVC uygulama yaşam döngüsünün üst düzey bir görünüm.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- İstek işleme Ardışık düzenin ayrıntılara inmesi aşağı gösteren ayrıntılı görünüm. Üst düzey Görünüm ve çeşitli aşamaları yaşam döngüleri ayrıntılarını nasıl toplanır görmek için ayrıntılı görünüm karşılaştırabilirsiniz. [PDF'yi indirin](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) daha büyük bir görmek için.
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- Yerleştirme ve tüm geçersiz kılınabilir yöntemleri üzerinde bir amacı [denetleyicisi](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) istek işleme ardışık düzeninde nesne. Olabilir veya herhangi bir yöntemi geçersiz kılmak için gerek olmayabilir, ancak uygulama yaşam döngüsü içindeki rollerine için istediğinize etkisi uygun yaşam döngüsü aşamasında kod yazmaya başlayabilmeniz için önceden anlamak önemlidir.
- Akıl yukarı diyagramları gösteren nasıl her filtre türü (kimlik doğrulaması, yetkilendirme, eylem ve sonuç) çağrılır.
- Ayrıntılar görünümünde her ilgi çekici bir kullanışlı bir makale veya blog bağlantı.

## <a name="next-steps"></a>Sonraki Adımlar

Bu belge, gereksinimi karşılar mı? Görüşleriniz bizim için önemlidir. Uygulamanızda, ASP.NET MVC yaşam döngüsü üzerinde herhangi bir sorunuz varsa [Stackoverflow](http://stackoverflow.com/help) ve [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx) istemek için mükemmel yerlerdir. İzleyin [bana](https://twitter.com/Cephas_MSFT) my en yeni öğreticiler güncelleştirmeleri alabilmeniz için Twitter'da.
