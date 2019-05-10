---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC yönlendirmesine genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, ASP.NET MVC çerçevesi tarayıcı istekleri denetleyici eylemleri için nasıl eşlendiğini Stephen Walther gösterir.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123640"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC Yönlendirmesine Genel Bakış (VB)

tarafından [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, ASP.NET MVC çerçevesi tarayıcı istekleri denetleyici eylemleri için nasıl eşlendiğini Stephen Walther gösterir.

Bu öğreticide, önemli bir özelliği olarak adlandırılan her bir ASP.NET MVC uygulaması için sunulan *ASP.NET yönlendirmesi*. ASP.NET yönlendirme modülü, belirli MVC denetleyici eylemleri için gelen tarayıcı istekleri eşlemek için sorumludur. Bu öğreticide sonuna kadar standart bir yol tablosu istekleri denetleyici eylemlerine eşlemelerini nasıl anlayacaksınız.

## <a name="using-the-default-route-table"></a>Varsayılan rota tablosu kullanma

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda uygulama ASP.NET yönlendirmesi kullanmak için zaten yapılandırıldı. ASP.NET yönlendirme iki yerde kurulur.

İlk olarak, ASP.NET yönlendirmesi, uygulamanızın Web yapılandırma dosyasında (Web.config dosyası) etkinleştirilir. Yapılandırma dosyasındaki Yönlendirmeyle ilgili dört bölüm vardır: system.web.httpModules bölümü, system.web.httpHandlers bölümü, system.webserver.modules bölümü ve system.webserver.handlers bölümü. Bu bölümler yönlendirme artık çalışmaz çünkü bu bölümleri silmemeye dikkat edin.

İkinci ve daha da önemlisi, uygulamanın Global.asax dosyasında bir yol tablosu oluşturulur. Global.asax dosyası, ASP.NET uygulama yaşam döngüsü olayları için olay işleyicileri içeren özel bir dosyadır. Rota tablosunu uygulama başlatma olayı sırasında oluşturulur.

1 listeleme dosyasında bir ASP.NET MVC uygulaması için varsayılan Global.asax dosyası içerir.

**Listing 1 - Global.asax.vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

Bir MVC uygulaması ilk kez başlatıldığında, uygulama\_Start() yöntemi çağrılır. Bu yöntem, buna karşılık RegisterRoutes() yöntemini çağırır. RegisterRoutes() metodu rota tablosu oluşturur.

Varsayılan rota tablosu (varsayılan olarak adlandırılır) tek bir yol içeriyor. Denetleyici adını, ikinci bir denetleyici eylemi için bir URL kesimini ve üçüncü kesim adlı bir parametre için bir URL ilk kesimi varsayılan rotayı eşler **kimliği**.

Imagine web tarayıcınızın adres çubuğuna aşağıdaki URL'yi girin:

/ Home/Index/3

Varsayılan yol bu URL'yi aşağıdaki parametrelerle eşlenir:

- Denetleyici giriş =

- Eylem dizini =

- Kimlik = 3

URL /Home/dizin/3 istediğinizde, aşağıdaki kod yürütülür:

HomeController.Index(3)

Varsayılan yol üç tüm parametreler için varsayılan değerleri içerir. Bir denetleyici sağlamazsanız, denetleyici parametre değerine varsayılanları **giriş**. Eylem parametresinin değeri varsayılan olarak, bu eylem sağlamazsanız, **dizin**. Son olarak, bir kimliği sağlamazsanız, ID parametresi boş dize olarak varsayar.

Varsayılan rota denetleyici eylemleri için URL'leri eşlemelerini nasıl bazı örnekler bakalım. Imagine tarayıcı adres çubuğuna aşağıdaki URL'yi girin:

/ Giriş

Varsayılan rota parametresi Varsayılanları nedeniyle, bu URL girilerek 2 çağrılacak listeleme HomeController sınıfının İNDİS() yöntemi neden olur.

**Listing 2 - HomeController.vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

Listeleme 2'de HomeController sınıfı kimliği adlı tek bir parametre kabul eden İNDİS() adlı bir yöntem içerir. URL /Home İNDİS() yöntemi değeriyle kimliği parametresinin değeri olarak bir şey çağrılmasına neden olur.

MVC çerçevesi denetleyici eylemleri çağırır şekli nedeniyle, URL /Home listeleme 3'te HomeController sınıfının İNDİS() yöntemi de eşleşir.

**3 - HomeController.vb (dizin eylem hiçbir parametre ile) listeleme**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

Listeleme 3'te İNDİS() yöntemi herhangi bir parametre kabul etmiyor. URL /Home bu İNDİS() yöntem çağrılacak neden olur. URL /Home/dizin/3 de (kimliği göz ardı edilir) bu yöntemi çağırır.

URL /Home listeleme 4'te HomeController sınıfının İNDİS() yöntemi de eşleşir.

**4 - HomeController.vb (boş değer atanabilen parametresi ile dizin eylem) listeleme**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

Listeleme 4'te İNDİS() yöntemi, bir tam sayı parametresi vardır. Parametresi (değeri hiçbir şey olabilir) bir boş değer atanabilen parametresi olduğundan, bir hata yükseltmeden İNDİS() çağrılabilir.

Son olarak, URL /Home ile listeleme 5'te İNDİS() metodu çağrılırken beri ID parametresine bir özel durum neden *değil* boş değer atanabilen parametresi. İNDİS() yöntemini çağırmak çalışırsanız, Şekil 1'de görüntülenen hata alırsınız.

**5 - HomeController.vb (dizin Eylem Kimliği parametresiyle) listeleme**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[![Bir parametre değerinin bir denetleyici eylemi çağırma](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**Şekil 01**: Bir parametre değerinin bir denetleyici Eylemi Çağırma ([tam boyutlu görüntüyü görmek için tıklatın](asp-net-mvc-routing-overview-vb/_static/image2.png))

URL /Home/dizin/3, diğer taraftan, yalnızca düzgün listeleme 5'te dizin denetleyici eylemi ile çalışır. İstek /Home/Index/3 İNDİS() yöntemi ile 3 değerine sahip bir ID parametresi çağrılmasına neden olur.

## <a name="summary"></a>Özet

ASP.NET yönlendirmesi için kısa bir giriş sağlamak için bu öğreticinin amacı oluştu. Biz, size yeni bir ASP.NET MVC uygulaması ile varsayılan rota tablosu incelenir. Varsayılan rota denetleyici eylemleri için URL'leri eşlemelerini nasıl yapılacağını öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](creating-an-action-cs.md)
> [İleri](understanding-action-filters-vb.md)
