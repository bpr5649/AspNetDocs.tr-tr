---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2 ' de OData sorgu seçeneklerini destekleme-ASP.NET 4. x
author: MikeWasson
description: Kod örneklerine genel bakış, ASP.NET 4. x için ASP.NET Web API 2 ' deki desteklenen OData sorgu seçeneklerini gösterir.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188649"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de OData sorgu seçeneklerini destekleme

, [Mike te son](https://github.com/MikeWasson)

Kod örnekleri ile bu genel bakış, ASP.NET 4. x için ASP.NET Web API 2 ' deki desteklenen OData sorgu seçeneklerini gösterir. 

OData, bir OData sorgusunu değiştirmek için kullanılabilecek parametreleri tanımlar. İstemci bu parametreleri istek URI 'sinin sorgu dizesinde gönderir. Örneğin, sonuçları sıralamak için bir istemci $orderby parametresini kullanır:

`http://localhost/Products?$orderby=Name`

OData belirtimi Bu parametre *sorgu seçeneklerini*çağırır. Projenizdeki herhangi bir Web API denetleyicisi için OData sorgu seçeneklerini etkinleştirebilir &#8212; denetleyicinin bir OData uç noktası olması gerekmez. Bu, herhangi bir Web API uygulamasına filtreleme ve sıralama gibi özellikleri eklemenin kolay bir yolunu sunar.

Sorgu seçeneklerini etkinleştirmeden önce lütfen [OData Güvenlik Kılavuzu](odata-security-guidance.md)konusunu okuyun.

- [OData sorgu seçeneklerini etkinleştirme](#enable)
- [Örnek sorgular](#examples)
- [Sunucu odaklı sayfalama](#server-paging)
- [Sorgu seçeneklerini sınırlama](#limiting_query_options)
- [Sorgu seçenekleri doğrudan çağrılıyor](#ODataQueryOptions)
- [Sorgu doğrulaması](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>OData sorgu seçeneklerini etkinleştirme

Web API 'SI aşağıdaki OData sorgu seçeneklerini destekler:

| Seçenek | Açıklama |
| --- | --- |
| $expand | İlgili varlıkları satır içi genişletir. |
| $filter | Sonuçları Boole koşuluna göre filtreler. |
| $inlinecount | Sunucuya, yanıttaki eşleşen varlıkların toplam sayısını içermesini söyler. (Sunucu tarafı sayfalama için kullanışlıdır.) |
| $orderby | Sonuçları sıralar. |
| $select | Yanıta hangi özelliklerin ekleneceğini seçer. |
| $skip | İlk n sonucu atlar. |
| $top | Sonuçları yalnızca ilk n sonucunu döndürür. |

OData sorgu seçeneklerini kullanmak için bunları açıkça etkinleştirmeniz gerekir. Uygulamayı tüm uygulama için küresel olarak etkinleştirebilir veya belirli denetleyiciler veya belirli eylemler için etkinleştirebilirsiniz.

OData sorgu seçeneklerini küresel olarak etkinleştirmek için, başlangıç sırasında **HttpConfiguration** sınıfında **EnableQuerySupport** ' u çağırın:

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**EnableQuerySupport** yöntemi bir **IQueryable** türü döndüren herhangi bir denetleyici eylemi için genel olarak sorgu seçeneklerini sunar. Sorgu seçeneklerinin tüm uygulama için etkinleştirilmesini istemiyorsanız, eylem yöntemine **[Queryable]** özniteliğini ekleyerek belirli denetleyici eylemleri için bunları etkinleştirebilirsiniz.

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>Örnek Sorgular

Bu bölümde, OData sorgu seçenekleri kullanılarak mümkün olan sorgu türleri gösterilmektedir. Sorgu seçenekleri hakkında ayrıntılı bilgi için [www.OData.org](http://www.odata.org/)adresindeki OData belgelerine bakın.

$Expand ve $select hakkında daha fazla bilgi için bkz. [ASP.NET Web API OData içinde $SELECT, $expand ve $value kullanma](using-select-expand-and-value.md).

**İstemci odaklı disk belleği**

Büyük varlık kümelerinde istemci, sonuçların sayısını sınırlamak isteyebilir. Örneğin, bir istemci bir sonraki sonuç sayfasını almak için "ileri" bağlantıları ile her seferinde 10 giriş gösterebilir. Bunu yapmak için, istemci $top ve $skip seçeneklerini kullanır.

`http://localhost/Products?$top=10&$skip=20`

$Top seçeneği döndürülecek en fazla girdi sayısını verir ve $skip seçeneği, atlanacak girdi sayısını verir. Önceki örnek, girdileri 21 ile 30 arasında getirir.

**Filtreleme**

$Filter seçeneği, bir istemcinin Boole ifadesi uygulayarak sonuçları filtrelemesine olanak sağlar. Filtre ifadeleri oldukça güçlüdür; mantıksal ve aritmetik işleçler, dize işlevleri ve Tarih işlevleri içerirler.

| Kategori "Toys" değerine eşit olan tüm ürünleri döndürür. | `http://localhost/Products?$filter=Category` EQ ' Toys ' |
| --- | --- |
| Fiyatı 10 ' dan küçük olan tüm ürünleri döndürün. | `http://localhost/Products?$filter=Price` lt 10 |
| Mantıksal işleçler: Price >= 5 ve Price <= 15 olan tüm ürünleri döndürün. | `http://localhost/Products?$filter=Price` GE 5 ve fiyat Le 15 |
| Dize işlevleri: adında "ZZ" olan tüm ürünleri döndürün. | `http://localhost/Products?$filter=substringof('zz',Name)` |
| Tarih işlevleri: 2005 sonrasında ReleaseDate ile tüm ürünleri döndürün. | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**Sıralama**

Sonuçları sıralamak için $orderby filtresini kullanın.

| Fiyata göre sıralayın. | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| Fiyata göre azalan sırada sıralayın (en yüksek-en düşük). | `http://localhost/Products?$orderby=Price desc` |
| Kategoriye göre sıralayın ve ardından kategoriler içinde azalan sırada fiyata göre sıralayın. | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>Sunucu odaklı sayfalama

Veritabanınız milyonlarca kayıt içeriyorsa, bunların tümünü tek bir yükte göndermek istemezsiniz. Bunu engellemek için sunucu tek bir yanıtta gönderdiği giriş sayısını sınırlayabilir. Sunucu Sayfalamayı etkinleştirmek için, **sorgulanabilir** özniteliğinde **PageSize** özelliğini ayarlayın. Değer döndürülecek en fazla girdi sayısıdır.

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

Denetleyiciniz OData biçimi döndürürse, yanıt gövdesi sonraki veri sayfasına bir bağlantı içerir:

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

İstemci bu bağlantıyı bir sonraki sayfayı getirmek için kullanabilir. Sonuç kümesindeki toplam giriş sayısını öğrenmek için, istemci $inlinecount sorgu seçeneğini "AllPages" değeriyle ayarlayabilir.

`http://localhost/Products?$inlinecount=allpages`

"AllPages" değeri, sunucuya yanıttaki toplam sayıyı dahil etmek için şunu söyler:

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> Sonraki sayfa bağlantıları ve satır içi sayısı her ikisi de OData biçimi gerektirir. Bunun nedeni, OData 'in bağlantıyı ve saymayı tutmak için yanıt gövdesinde özel alanlar tanımlamasının nedenidir.

OData olmayan biçimler için, sorgu sonuçlarını bir **PageResult &lt; &gt; ** nesnesine sarmalayarak, sonraki sayfa bağlantılarını ve satır içi sayıyı desteklemek yine de mümkündür. Ancak, biraz daha fazla kod gerektirir. Aşağıda bir örnek verilmiştir:

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

Örnek bir JSON yanıtı aşağıda verilmiştir:

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>Sorgu seçeneklerini sınırlama

Sorgu seçenekleri istemciye sunucusunda çalıştırılan sorgu üzerinde çok fazla denetim sağlar. Bazı durumlarda, güvenlik veya performans nedenleriyle kullanılabilir seçenekleri sınırlamak isteyebilirsiniz. **[Queryable]** özniteliğinde bunun için bazı yerleşik özellikler vardır. Aşağıda bazı örnekler verilmiştir.

Yalnızca $skip ve $top, sayfalamayı desteklemeye ve başka hiçbir şey yapmasına izin ver:

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

Veritabanında dizinlenmemiş özelliklerde sıralamayı engellemek için yalnızca belirli özelliklere göre sıralamaya izin ver:

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

"EQ" mantıksal işlevine izin verin, ancak başka mantıksal işlevler yoktur:

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

Aritmetik işleçlere izin vermeyin:

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

Bir **QueryableAttribute** örneği oluşturarak ve bunu **EnableQuerySupport** işlevine geçirerek, seçenekleri küresel olarak kısıtlayabilirsiniz:

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>Sorgu seçenekleri doğrudan çağrılıyor

**[Sorgulanabilir]** özniteliğini kullanmak yerine, doğrudan denetleyicinizde sorgu seçeneklerini çağırabilirsiniz. Bunu yapmak için, Controller yöntemine bir **ODataQueryOptions** parametresi ekleyin. Bu durumda, **[Queryable]** özniteliğine ihtiyacınız yoktur.

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Web API 'si, **ODataQueryOptions** 'ı URI sorgu dizesinden doldurur. Sorguyu uygulamak için **ApplyTo** yöntemine bir **IQueryable** geçirin. Yöntemi başka bir **IQueryable**döndürür.

Gelişmiş senaryolar için, bir **IQueryable** sorgu sağlayıcınız yoksa, **ODataQueryOptions** öğesini inceleyebilir ve sorgu seçeneklerini başka bir forma çevirebilirsiniz. (Örneğin, bkz. ıghurhar Naazaltı 'ın Web günlüğü gönderisi, [OData sorgularını HQL 'ye çevirerek](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)bir [örnek](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)de içerir.)

<a id="query-validation"></a>
## <a name="query-validation"></a>Sorgu doğrulaması

**[Queryable]** özniteliği yürütmeden önce sorguyu doğrular. Doğrulama adımı **QueryableAttribute. ValidateQuery** yönteminde gerçekleştirilir. Doğrulama işlemini de özelleştirebilirsiniz.

Ayrıca bkz. [OData Güvenlik Kılavuzu](odata-security-guidance.md).

İlk olarak, **Web. http. OData. Query. doğrulayıcılar** ad alanında tanımlanan Doğrulayıcı sınıflarından birini geçersiz kılın. Örneğin, aşağıdaki Doğrulayıcı sınıfı $orderby seçeneği için ' DESC ' seçeneğini devre dışı bırakır.

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

**Validatequery** yöntemini geçersiz kılmak Için **[Queryable]** özniteliğini alt sınıf yapın.

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

Ardından özel öznitelerinizi genel olarak veya denetleyiciden göre ayarlayın:

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

**ODataQueryOptions** ' ı doğrudan kullanıyorsanız, seçenekler üzerinde doğrulayıcısı ayarlayın:

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
