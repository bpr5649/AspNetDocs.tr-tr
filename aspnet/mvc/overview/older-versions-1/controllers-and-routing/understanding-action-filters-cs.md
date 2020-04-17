---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Eylem Filtrelerini Anlama (C#) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı eylem filtrelerini açıklamaktır. Eylem filtresi, denetleyici eylemine (veya tüm denetleyiciye) uygulayabileceğiniz bir özniteliktir...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542189"
---
# <a name="understanding-action-filters-c"></a>Eylem Filtrelerini Anlama (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> Bu öğreticinin amacı eylem filtrelerini açıklamaktır. Eylem filtresi, bir denetleyici eylemine (veya tüm denetleyiciye) uygulayabileceğiniz ve eylemin yürütülme biçimini değiştiren bir özniteliktir.

## <a name="understanding-action-filters"></a>Eylem Filtrelerini Anlama

Bu öğreticinin amacı eylem filtrelerini açıklamaktır. Eylem filtresi, bir denetleyici eylemine (veya tüm denetleyiciye) uygulayabileceğiniz ve eylemin yürütülme biçimini değiştiren bir özniteliktir. ASP.NET MVC çerçevesi birkaç işlem filtresi içerir:

- OutputÖnbellek – Bu eylem filtresi, denetleyici eyleminin çıktısını belirli bir süre için önbelleğe alır.
- HandleError – Bu eylem filtresi, denetleyici eylemi yürütüldüğünde ortaya çıkan hataları işler.
- Authorize – Bu eylem filtresi, belirli bir kullanıcıya veya role erişimi kısıtlamanızı sağlar.

Ayrıca kendi özel eylem filtrelerinizi de oluşturabilirsiniz. Örneğin, özel bir kimlik doğrulama sistemi uygulamak için özel bir eylem filtresi oluşturmak isteyebilirsiniz. Veya, bir denetleyici eylemi tarafından döndürülen görünüm verilerini değiştiren bir eylem filtresi oluşturmak isteyebilirsiniz.

Bu öğreticide, sıfırdan bir eylem filtresi oluşturmayı öğrenirsiniz. Visual Studio Output penceresine bir eylemin işlenmesinin farklı aşamalarını kaydeden bir Günlük eylem filtresi oluştururuz.

### <a name="using-an-action-filter"></a>Eylem Filtresi Kullanma

Eylem filtresi bir özniteliktir. Çoğu eylem filtresini tek bir denetleyici eylemine veya tüm denetleyiciye uygulayabilirsiniz.

Örneğin, Listeleme 1'deki Veri denetleyicisi, geçerli zamanı döndüren bir `Index()` eylemi ortaya çıkarır. Bu eylem `OutputCache` eylem filtresi ile dekore edilmiştir. Bu filtre, eylem tarafından döndürülen değerin 10 saniye önbelleğe alınmasına neden olur.

**İlan 1 –`Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

URL/Veri/Dizin'i tarayıcınızın adres çubuğuna girerek ve Yenile düğmesine birden çok kez basarak `Index()` eylemi tekrar tekrar çağırırsanız, aynı zamanı 10 saniye boyunca görürsünüz. Eylemin çıktısı `Index()` 10 saniye önbelleğe alınır (Bkz. Şekil 1).

[![Önbelleğe alınmış zaman](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**Şekil 01**: Önbelleğe alınmış zaman ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](understanding-action-filters-cs/_static/image3.png))

Listeleme 1'de, `OutputCache` `Index()` tek bir eylem filtresi (eylem filtresi) yönteme uygulanır. İhtiyacınız varsa, aynı eyleme birden çok eylem filtresi uygulayabilirsiniz. Örneğin, hem eylem filtrelerini `OutputCache` hem `HandleError` de eylem filtrelerini aynı eyleme uygulamak isteyebilirsiniz.

Listeleme 1'de `OutputCache` eylem filtresi `Index()` eyleme uygulanır. Bu özniteliği `DataController` sınıfın kendisine de uygulayabilirsiniz. Bu durumda, denetleyici tarafından maruz kalan herhangi bir eylem tarafından döndürülen sonuç 10 saniye önbelleğe alınır.

### <a name="the-different-types-of-filters"></a>Farklı Filtre Türleri

ASP.NET MVC çerçevesi dört farklı filtre türünü destekler:

1. Yetkilendirme filtreleri – `IAuthorizationFilter` Özniteliği uygular.
2. Eylem filtreleri – `IActionFilter` Özniteliği uygular.
3. Sonuç filtreleri – `IResultFilter` Özniteliği uygular.
4. Özel durum filtreleri `IExceptionFilter` – Özniteliği uygular.

Filtreler yukarıda listelenen sırada yürütülür. Örneğin, yetkilendirme filtreleri her zaman işlem filtreleri ve özel durum filtreleri her zaman diğer filtre türsonra yürütülür önce yürütülür.

Yetkilendirme filtreleri, denetleyici eylemleri için kimlik doğrulama ve yetkilendirme uygulamak için kullanılır. Örneğin, Yetkilendirme filtresi Yetkilendirme filtresi bir Yetkilendirme filtresi örneğidir.

Eylem filtreleri, denetleyici eylemi yürütülmeden önce ve sonra yürütülen mantık içerir. Örneğin, denetleyici eyleminin döndürdettiği görünüm verilerini değiştirmek için bir eylem filtresi kullanabilirsiniz.

Sonuç filtreleri, görünüm sonucu yürütülmeden önce ve sonra yürütülen mantık içerir. Örneğin, görünüm tarayıcıya işlenmeden hemen önce bir görünüm sonucunu değiştirmek isteyebilirsiniz.

Özel durum filtreleri, çalıştırılabilmek için son filtre türüdür. Denetleyici eylemleriniz veya denetleyici eylem sonuçlarınız tarafından yükseltilen hataları işlemek için bir özel durum filtresi kullanabilirsiniz. Hataları günlüğe kaydetmek için özel durum filtrelerini de kullanabilirsiniz.

Her farklı filtre türü belirli bir sırada yürütülür. Aynı türdeki filtrelerin yürütüldürün sırasını denetlemek istiyorsanız, bir filtrenin Sipariş özelliğini ayarlayabilirsiniz.

Tüm eylem filtreleri için taban `System.Web.Mvc.FilterAttribute` sınıf sınıftır. Belirli bir filtre türünü uygulamak istiyorsanız, temel Filtre sınıfından devralan `IAuthorizationFilter`ve bir veya daha fazla , `IActionFilter`, `IResultFilter`veya `IExceptionFilter` arabirim uygulayan bir sınıf oluşturmanız gerekir.

### <a name="the-base-actionfilterattribute-class"></a>Temel ActionFilterAttribute Sınıf

Özel bir eylem filtresi uygulamanızı kolaylaştırmak için, mvc ASP.NET çerçevesi bir `ActionFilterAttribute` taban sınıf içerir. Bu sınıf hem `IActionFilter` arabirimleri uygular hem `IResultFilter` de `Filter` sınıftan devralır.

Buradaki terminoloji tam olarak tutarlı değil. Teknik olarak, ActionFilterAttribute sınıfından devralan bir sınıf hem bir eylem filtresi hem de sonuç filtresidir. Ancak, gevşek anlamda, eylem filtresi sözcüğü ASP.NET MVC çerçevesindeki herhangi bir filtre türünü ifade etmek için kullanılır.

Taban `ActionFilterAttribute` sınıf, geçersiz kılabileceğiniz aşağıdaki yöntemlere sahiptir:

- OnActionExecuting – Bu yöntem, denetleyici eylemi yürütülmeden önce çağrılır.
- OnActionExecuted – Bu yöntem, bir denetleyici eylemi yürütüldükten sonra çağrılır.
- OnResultExecuting – Bu yöntem, denetleyici eylem sonucu yürütülmeden önce çağrılır.
- OnResultExecuted – Bu yöntem, denetleyici eylem sonucu çalıştırılan sonra çağrılır.

Sonraki bölümde, bu farklı yöntemlerin her birini nasıl uygulayabileceğinizi göreceğiz.

### <a name="creating-a-log-action-filter"></a>Günlük Eylem Filtresi Oluşturma

Özel bir eylem filtresini nasıl oluşturabileceğinizi göstermek için, bir denetleyici eylemini Visual Studio Output penceresine işleme aşamalarını günlüğe kaydeden özel bir eylem filtresi oluştururuz. Bizim `LogActionFilter` Listeleme 2 yer almaktadır.

**Listeleme 2 –`ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

`OnActionExecuting()`Listeleme 2'de, `OnResultExecuting()`, `OnResultExecuted()` , `Log()` `OnActionExecuted()`ve yöntemlerin tümü yöntemi çağırır. Yöntemin adı ve geçerli rota verileri `Log()` yönteme aktarılır. Yöntem `Log()` Visual Studio Çıktı penceresine bir ileti yazar (Bkz. Şekil 2).

[![Visual Studio Çıkış penceresine yazma](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**Şekil 02**: Visual Studio Çıkış penceresine yazma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](understanding-action-filters-cs/_static/image6.png))

Listeleme 3'teki Ev denetleyicisi, Günlük eylem filtresini tüm denetleyici sınıfına nasıl uygulayabileceğinizi gösterir. Home denetleyicisi tarafından ortaya çıkarılan eylemlerden herhangi `Index()` biri çağrıldığı zaman –yöntem veya `About()` yöntem- eylemi işleme aşamaları Visual Studio Output penceresine kaydedilir.

**İlan 3 –`Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>Özet

Bu eğitimde, ASP.NET MVC eylem filtreleri tanıtıldı. Yetkilendirme filtreleri, eylem filtreleri, sonuç filtreleri ve özel durum filtreleri olmak üzere dört farklı filtre türünü öğrendiniz. Ayrıca taban `ActionFilterAttribute` sınıf hakkında öğrendim.

Son olarak, basit bir eylem filtresini nasıl uygulayacağınızı öğrendiniz. Visual Studio Output penceresine bir denetleyici eylemini işleme aşamalarını kaydeden bir Günlük eylem filtresi oluşturduk.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-routing-overview-cs.md)
> [Sonraki](improving-performance-with-output-caching-cs.md)
