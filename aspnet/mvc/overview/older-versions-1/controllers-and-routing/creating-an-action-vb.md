---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Eylem Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin. Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542254"
---
# <a name="creating-an-action-vb"></a>Eylem Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET Bir MVC denetleyicisine nasıl yeni bir eylem ekleyeceğinizi öğrenin. Bir yöntemin eylem olması için gerekenler hakkında bilgi edinin.

Bu öğreticinin amacı, yeni bir denetleyici eylemi nasıl oluşturabileceğinizi açıklamaktır. Bir eylem yönteminin gereksinimleri hakkında bilgi edinebilirsiniz. Ayrıca, bir yöntemin bir eylem olarak açığa çıkarMasını nasıl önleyeceğinizi de öğrenirsiniz.

## <a name="adding-an-action-to-a-controller"></a>Denetleyiciye Eylem Ekleme

Denetleyiciye yeni bir yöntem ekleyerek denetleyiciye yeni bir eylem eklersiniz. Örneğin, Listeleme 1'deki denetleyici, Index() adlı bir eylem ve SayHello() adlı bir eylem içerir. Her iki yöntem de eylem olarak ortaya çıkar.

**Listeleme 1 - Denetleyiciler\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

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

Denetleyici sınıfında ortak bir yöntem oluşturmanız gerekiyorsa ve yöntemi denetleyici eylemi olarak ortaya çıkarmak istemiyorsanız, yöntemin &lt;Eylem&gt; Dışı özniteliğini kullanarak çağrılmasını engelleyebilirsiniz. Örneğin, Listeleme 2'deki denetleyici, Eylem &lt;&gt; Dışı özniteliğiyle dekore edilmiş CompanySecrets() adlı genel bir yöntem içerir.

**Listeleme 2 - Denetleyiciler\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

/Work/CompanySecrets yazıp /İş/ŞirketSırları'nı tarayıcınızın adres çubuğuna yazarak CompanySecrets() denetleyici eylemini çağırmaya çalışırsanız, hata iletisini Şekil 1'de alırsınız.

[![Eylemsizlik yöntemini çağırmak](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Şekil 01**: Eylemsizlik yöntemini çağırmak([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Önceki](creating-a-controller-vb.md)
> [Sonraki](aspnet-mvc-controllers-overview-cs.md)
