---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Güvenlik Kılavuzu ASP.NET Web API 2 OData - ASP.NET 4.x
author: MikeWasson
description: ASP.NET'te ASP.NET Web API 2 OData aracılığıyla bir veri kümesi gösterme yaparken dikkate alınması gereken güvenlik konularını açıklar 4.x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393515"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>Güvenlik Kılavuzu ASP.NET Web API 2 OData

tarafından [Mike Wasson](https://github.com/MikeWasson)

Bu konuda bazı ASP.NET'te ASP.NET Web API 2 OData aracılığıyla bir veri kümesi gösterme, dikkate almanız gereken güvenlik konuları açıklanmaktadır 4.x.

## <a name="edm-security"></a>EDM güvenlik

Sorgu semantiği, varlık veri Modeli'ni temel (EDM), temel alınan model türleri değil temel alır. EDM bir özellik hariç tutabilir ve sorgu için görünür olmaz. Örneğin, bir çalışan türü maaş özelliğine sahip modelinizi içerdiğini varsayın. Bu özellik istemcilerden gizlemek için EDM dışlanacak isteyebilirsiniz.

EDM bir özelliği dışarıda iki yolu vardır. Ayarlayabileceğiniz **[IgnoreDataMember]** model sınıfı özelliğinde özniteliği:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

Ayrıca özelliği EDM programlı bir şekilde kaldırabilirsiniz:

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>Sorgu güvenliği

Kötü amaçlı veya naïve istemci yürütmek için çok uzun zaman alan bir sorgu oluşturmak mümkün olabilir. En kötü durumda bu, hizmete erişimi kesintiye uğratabilir.

**[Queryable]** özniteliktir ayrıştırır, doğrular ve sorgu geçerli bir eylem filtresi. Filtre sorgu seçeneklerini bir LINQ ifadesini dönüştürür. OData denetleyicisi döndürdüğünde bir **Iqueryable** türü **Iqueryable** LINQ sağlayıcısı bir sorguda LINQ ifadesi dönüştürür. Bu nedenle, performansı, kullanılan LINQ sağlayıcısı ve aynı zamanda veri kümesi veya veritabanı şemanızı belirli özelliklerine bağlıdır.

ASP.NET Web API OData sorgu seçenekleri kullanma hakkında daha fazla bilgi için bkz. [OData sorgu seçeneklerini destekleme](supporting-odata-query-options.md).

Tüm istemciler (örneğin, bir kuruluş ortamında) güvenilir biliyorsanız ya da veri kümeniz küçükse, sorgu performansı sorunu olmayabilir. Aksi takdirde, aşağıdaki önerileri göz önünde bulundurmalısınız.

- Çeşitli sorgularla hizmetinizi test etme ve DB profil.
- Büyük bir veri kümesi döndüren bir sorgu önlemek sunucu tabanlı disk belleği, etkinleştirin. Daha fazla bilgi için [Server-Driven sayfalama](supporting-odata-query-options.md#server-paging). 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter ve $orderby gerekiyor mu? Bazı uygulamalar disk belleği, $top ve $skip kullanarak istemci izin ver, ancak başka sorgu seçenekleriyle devre dışı. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- Kümelenmiş bir dizin özelliklerinde $orderby kısıtlama göz önünde bulundurun. Kümelenmiş bir dizin olmadan büyük veri sıralama yavaştır. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- En yüksek düğüm sayısı: **MaxNodeCount** özelliği **[Queryable]** izin $filter sözdizimi ağacı maksimum düğüm sayısına ayarlar. Varsayılan değer 100'dür, ancak çok sayıda düğümü derlemek yavaş olabilir çünkü daha düşük bir değere ayarlamak isteyebilirsiniz. LINQ to Objects'in (yani, bir koleksiyonda Ara bir LINQ sağlayıcısı kullanmadan bellekte LINQ sorguları) kullanıyorsanız, bu özellikle doğrudur. 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Bunlar yavaş olması gibi any() ve all() işlevler devre dışı bırakmayı düşünün. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- Herhangi bir dize özelliği büyük dizelerin içeriyorsa&#8212;ürün açıklaması veya blog girişi&#8212;dize işlevleri devre dışı bırakmayı düşünün. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- Gezinti özellikleri filtreleme engelleyerek göz önünde bulundurun. Gezinti özellikleri filtreleme bağlı olarak, veritabanı şemasını yavaş olabilir bir birleştirme neden olabilir. Aşağıdaki kod, gezinti özellikleri filtreleme engelleyen bir sorgu Doğrulayıcı gösterir. Sorgu doğrulayıcıları hakkında daha fazla bilgi için bkz: [sorgu doğrulama](supporting-odata-query-options.md#query-validation). 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- $Filter sorgu veritabanınız için özelleştirilmiş bir doğrulayıcı yazarak kısıtlamayı göz önünde bulundurun. Örneğin, bu iki sorguları göz önünde bulundurun: 

  - Aktörler son adı 'A' ile başlayan tüm filmlerle.
  - Tüm filmlere 1994'te yayımlanan.

    İlk sorgu, filmler aktörler tarafından dizinlenen sürece filmler listesinin tümünü taramak üzere veritabanı altyapısı gerektirebilir. İkinci sorgu kabul edilebilir ise varsayılıyor filmler yayın yıla göre dizine eklenir.

    Aşağıdaki kod, "ReleaseYear" ve "Title" özellikleri ancak başka hiçbir özellik filtrelemeye olanak tanır, Doğrulayıcıyı gösterir.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- Genel olarak, gereksinim duyduğunuz $filter işlev göz önünde bulundurun. $Filter, tam anlamlılık istemcilerinize ihtiyacınız yoksa, izin verilen işlevler sınırlayabilirsiniz.
