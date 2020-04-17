---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Eylem Oluşturma (C#) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin. Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542280"
---
# <a name="creating-an-action-c"></a>Eylem Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin. Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.

Bu öğreticinin amacı, yeni bir denetleyici eylemi nasıl oluşturabileceğinizi açıklamaktır. Bir eylem yönteminin gereksinimleri hakkında bilgi edinebilirsiniz. Ayrıca, bir yöntemin bir eylem olarak açığa çıkarMasını nasıl önleyeceğinizi de öğrenirsiniz.

## <a name="adding-an-action-to-a-controller"></a>Denetleyiciye Eylem Ekleme

Denetleyiciye yeni bir yöntem ekleyerek denetleyiciye yeni bir eylem eklersiniz. Örneğin, Listeleme 1'deki denetleyici, Index() adlı bir eylem ve SayHello() adlı bir eylem içerir. Her iki yöntem de eylem olarak ortaya çıkar.

**Listeleme 1 - Denetleyiciler\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

Bir eylem olarak evrene maruz kalmak için, bir yöntem belirli gereksinimleri karşılamak gerekir:

- Yöntem herkese açık olmalıdır.
- Yöntem statik bir yöntem olamaz.
- Yöntem bir uzantı yöntemi olamaz.
- Yöntem bir oluşturucu, getter veya ayarlayıcı olamaz.
- Yöntem, açık genel türleri olamaz.
- Yöntem denetleyici taban sınıfının bir yöntemi değildir.
- Yöntem **ref** veya **çıkış** parametreleri içeremez.

Denetleyici eyleminin dönüş türünde herhangi bir kısıtlama bulunmadığına dikkat edin. Denetleyici eylem bir dize, DateTime, Rasgele sınıfın bir örneği veya geçersiz döndürebilir. ASP.NET MVC çerçevesi, eylem sonucu olmayan herhangi bir iade türünü bir dize ye dönüştürür ve dizeyi tarayıcıya dönüştürür.

Denetleyiciye bu gereksinimleri ihlal etmeyen herhangi bir yöntem eklediğinizde, yöntem denetleyici eylemi olarak ortaya çıkarır. Burada dikkatli ol. Denetleyici eylemi, Internet'e bağlı herkes tarafından çağrılabilir. Örneğin, bir DeleteMyWebsite() denetleyici eylemi oluşturmayın.

## <a name="preventing-a-public-method-from-being-invoked"></a>Genel Yöntemin Çağrılmasını Önleme

Denetleyici sınıfında ortak bir yöntem oluşturmanız gerekiyorsa ve yöntemi denetleyici eylemi olarak ortaya çıkarmak istemiyorsanız, [Eylem Dışı] özniteliğini kullanarak yöntemin çağrılmasını engelleyebilirsiniz. Örneğin, Listeleme 2'deki denetleyici, [Eylem Dışı] özniteliğiyle dekore edilmiş CompanySecrets() adlı genel bir yöntem içerir.

**Listeleme 2 - Denetleyiciler\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

/Work/CompanySecrets yazıp /İş/ŞirketSırları'nı tarayıcınızın adres çubuğuna yazarak CompanySecrets() denetleyici eylemini çağırmaya çalışırsanız, hata iletisini Şekil 1'de alırsınız.

[![Eylemsizlik yöntemini çağırmak](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**Şekil 01**: Eylemsizlik yöntemini çağırmak([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-an-action-cs/_static/image2.png))

> [!div class="step-by-step"]
> [Önceki](creating-a-controller-cs.md)
> [Sonraki](asp-net-mvc-routing-overview-vb.md)
