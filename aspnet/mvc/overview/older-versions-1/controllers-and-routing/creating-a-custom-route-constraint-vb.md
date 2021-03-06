---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: Özel yol kısıtlaması oluşturma (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther nasıl özel bir yol kısıtlaması oluşturacağınızı gösterir. Bir yolun w ile eşleştirilmesini engelleyen basit bir özel kısıtlama uyguladık...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601411"
---
# <a name="creating-a-custom-route-constraint-vb"></a>Özel Rota Kısıtlaması Oluşturma (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther nasıl özel bir yol kısıtlaması oluşturacağınızı gösterir. Uzak bir bilgisayardan bir tarayıcı isteği yapıldığında bir yolun eşleştirilmesini engelleyen basit bir özel kısıtlama uyguladık.

Bu öğreticinin amacı, özel bir yol kısıtlaması oluşturmayı gösterir. Özel bir yol kısıtlaması, bir özel koşul eşleştirilmediği takdirde bir yolun eşleştirilmesini engellemenizi sağlar.

Bu öğreticide, bir localhost yol kısıtlaması oluşturacağız. Localhost yol kısıtlaması yalnızca yerel bilgisayardan yapılan isteklerle eşleşir. Internet üzerinden gelen uzak istekler eşleşmiyor.

IRouteConstraint arabirimini uygulayarak özel bir yol kısıtlaması uygulayabilirsiniz. Bu, tek bir yöntemi açıklayan son derece basit bir arabirimdir:

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

Yöntemi bir Boole değeri döndürür. False değerini döndürmediyseniz, kısıtlama ile ilişkili yol tarayıcı isteğiyle eşleşmez.

Localhost kısıtlaması, liste 1 ' de bulunur.

**Listeleme 1-LocalhostConstraint. vb**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

Listeleme 1 ' deki kısıtlama, HttpRequest sınıfı tarafından kullanıma sunulan IsLocal özelliğinden yararlanır. Bu özellik, isteğin IP adresi 127.0.0.1 olduğunda ya da isteğin IP 'si sunucunun IP adresiyle aynı olduğunda true değerini döndürür.

Global. asax dosyasında tanımlanan bir yol içinde özel bir kısıtlama kullanırsınız. Liste 2 ' deki Global. asax dosyası, yerel sunucudan istekte bulunmadıkları takdirde herkesin Yönetici sayfası istemesini engellemek için localhost kısıtlamasını kullanır. Örneğin, uzak bir sunucudan yapıldığında/Admin/DeleteAll için bir istek başarısız olur.

**Listeleme 2-Global. asax**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

Localhost kısıtlaması, yönetici yolunun tanımında kullanılır. Bu yol, uzak bir tarayıcı isteğiyle eşleşmeyecek. Bununla birlikte, Global. asax dosyasında tanımlanan diğer yolların de aynı istekle eşleşeceğini fark edebilirsiniz. Bir kısıtlamanın, belirli bir yolun, Global. asax dosyasında tanımlı tüm yolların değil, bir istekle eşleşmesini önlediği anlaşılması önemlidir.

Varsayılan yolun, liste 2 ' deki Global. asax dosyasından yorumdığına dikkat edin. Varsayılan yolu eklerseniz, varsayılan yol, yönetici denetleyicisi istekleriyle eşleşir. Bu durumda, uzak kullanıcılar, istekleri yönetici rotayla eşleşmese de yönetici denetleyicisinin eylemlerini çağırmaya devam edebilir.

> [!div class="step-by-step"]
> [Öncekini](creating-a-route-constraint-vb.md)
