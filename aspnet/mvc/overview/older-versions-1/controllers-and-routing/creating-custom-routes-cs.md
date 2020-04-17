---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Özel Rotalar Oluşturma (C#) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Bir MVC uygulamasına özel rotalar eklemeyi öğrenin. Bu eğitimde, Global.asax dosyasındaki varsayılan rota tablosunu nasıl değiştirdiğinizi öğrenirsiniz.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542761"
---
# <a name="creating-custom-routes-c"></a>Özel Rotalar Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET Bir MVC uygulamasına özel rotalar eklemeyi öğrenin. Bu eğitimde, Global.asax dosyasındaki varsayılan rota tablosunu nasıl değiştirdiğinizi öğrenirsiniz.

Bu öğreticide, ASP.NET bir MVC uygulamasına özel bir rota eklemeyi öğrenirsiniz. Global.asax dosyasındaki varsayılan rota tablosunu özel bir rotayla nasıl değiştirebilirsiniz öğrenin.

Birçok basit ASP.NET MVC uygulamaları için varsayılan rota tablosu gayet iyi çalışır. Ancak, özel yönlendirme gereksinimleriniz olduğunu keşfedebilirsiniz. Bu durumda, özel bir rota oluşturabilirsiniz.

Örneğin, bir blog uygulaması oluşturuyorolduğunuzu düşünün. Şuna benzeyen gelen istekleri işlemek isteyebilirsiniz:

/Arşiv/12-25-2009

Bir kullanıcı bu isteği girdiğinde, 25/12/2009 tarihine karşılık gelen blog girişini iade etmek istersiniz. Bu tür bir isteği işlemek için özel bir rota oluşturmanız gerekir.

Listeleme 1'deki Global.asax dosyası, /Arşiv/*giriş tarihine*benzeyen istekleri işleyen Blog adlı yeni bir özel rota içerir.

**Listeleme 1 - Global.asax (özel rota ile)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

Rota tablosuna eklediğiniz yolların sırası önemlidir. Yeni özel Blog rotamız, varolan Varsayılan rotadan önce eklenir. Siparişi tersine çevirdiyseniz, Varsayılan yol her zaman özel rota yerine çağrılır.

Özel Blog rotası / Arşiv/ ile başlayan herhangi bir istek eşleşir. Bu nedenle, aşağıdaki URL'lerin tümüyle eşleşir:

- /Arşiv/12-25-2009

- /Arşiv/10-6-2004

- /Arşiv/elma

Özel rota, gelen isteği Arşiv adlı bir denetleyiciyle eşler ve Giriş() eylemini çağırır. Giriş() yöntemi çağrıldığında, giriş tarihi entryDate adlı bir parametre olarak geçirilir.

Listeleme 2'deki denetleyiciile Blog özel rotasını kullanabilirsiniz.

**Listeleme 2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

Listeleme 2'deki Giriş() yönteminin DateTime türünden bir parametreyi kabul ettiğine dikkat edin. MVC çerçevesi, giriş tarihini URL'den otomatik olarak DateTime değerine dönüştürecek kadar akıllıdır. URL'den giriş tarihi parametresi DateTime'a dönüştürülemiyorsa, bir hata yükseltilir (Bkz. Şekil 1).

**Şekil 1 - Parametre dönüştürme hatası**

[![Yeni Proje iletişim kutusu](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**Şekil 01**: Parametredönüştürme hatası ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>Özet

Bu öğreticinin amacı, özel bir rotayı nasıl oluşturabileceğinizi göstermekti. Blog girişlerini temsil eden Global.asax dosyasındaki rota tablosuna özel bir rota eklemeyi öğrendiniz. Blog girişleri isteklerini ArchiveController adlı bir denetleyiciye ve Entry() adlı bir denetleyici eylemine nasıl eşlendirebileceğimizi tartıştık.

> [!div class="step-by-step"]
> [Önceki](aspnet-mvc-controllers-overview-cs.md)
> [Sonraki](creating-a-route-constraint-cs.md)
