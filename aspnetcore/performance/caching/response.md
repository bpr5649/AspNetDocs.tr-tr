---
title: ASP.NET Core yanıt önbelleğe alma
author: rick-anderson
description: Önbelleğe alma daha düşük bant genişliği gereksinimlerine yanıt kullanmayı öğrenin ve ASP.NET Core uygulamaları performansını artırın.
ms.author: riande
ms.date: 01/07/2018
uid: performance/caching/response
ms.openlocfilehash: 5fbcaddff6e53d01a19ba8a7455c719feb614326
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077877"
---
# <a name="response-caching-in-aspnet-core"></a>ASP.NET Core yanıt önbelleğe alma

Tarafından [John Luo](https://github.com/JunTaoLuo), [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), ve [Luke Latham](https://github.com/guardrex)

> [!NOTE]
> Razor sayfaları yanıt önbelleğe alma, ASP.NET Core 2.1 veya üstü.

[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/samples) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))

Yanıt önbelleğe alma, bir istemci ya da proxy web sunucusunda yapar istek sayısını azaltır. Yanıtları önbelleğe alma de azaltır çalışmanın bir yanıtı oluşturmak için web sunucusu gerçekleştirir. Yanıt önbelleğe alma, istemci proxy ve önbellek yanıtları Ara yazılımıyla nasıl istediğinizi belirtmek üstbilgileri tarafından denetlenir.

[ResponseCache özniteliği](#responsecache-attribute) yanıt üst bilgileri, hangi istemcilerin yanıtları önbelleğe alırken dikkate, önbelleğe alma ayarını katılır. [Yanıtları önbelleğe alma ara yazılımı](xref:performance/caching/middleware) sunucusunda önbellek yanıtları için kullanılabilir. Ara yazılım kullanabilirsiniz `ResponseCache` özniteliği sunucu tarafı önbelleğe alma davranışını etkilemek için özellikleri.

## <a name="http-based-response-caching"></a>HTTP tabanlı yanıt önbelleğe alma

[HTTP 1.1 önbelleğe alma belirtimi](https://tools.ietf.org/html/rfc7234) Internet önbelleklerini nasıl hareket etmesi gerektiğini açıklar. Önbelleğe alma işlemi için kullanılan birincil HTTP üst bilgisi [Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2), önbellek belirtmek için kullanılan *yönergeleri*. Yönergeleri aşamalarından istemcilerden sunucularına isteklerde ve yanıtı sunucudan istemcilere geri aşamalarından yaptıkça önbelleğe alma davranışını denetleme. İsteklerin ve yanıtların proxy sunucular taşıyın ve proxy sunucuları HTTP 1.1 önbelleğe alma belirtime uygun de gerekir.

Ortak `Cache-Control` yönergeleri, aşağıdaki tabloda gösterilmiştir.

| Yönergesi                                                       | Eylem |
| --------------------------------------------------------------- | ------ |
| [public](https://tools.ietf.org/html/rfc7234#section-5.2.2.5)   | Bir önbellek yanıt depolayabilir. |
| [private](https://tools.ietf.org/html/rfc7234#section-5.2.2.6)  | Yanıt tarafından paylaşılan bir önbellek depolanması gerekir. Özel bir önbellek depolayın ve yanıt yeniden kullanın. |
| [Maksimum yaş](https://tools.ietf.org/html/rfc7234#section-5.2.1.1)  | İstemci, yaş, belirtilen sayıda saniye büyük bir yanıtı kabul edilmeyecektir. Örnekler: `max-age=60` (60 saniye) `max-age=2592000` (1 ay) |
| [önbellek yok](https://tools.ietf.org/html/rfc7234#section-5.2.1.4) | **İsteklerinde**: Bir önbellekte depolanmış bir yanıt isteği karşılamak için kullanmamalıdır. Not: İçin istemci yanıt kaynak sunucuya yeniden oluşturur ve ara yazılım önbelleğinde depolanan yanıtta güncelleştirir.<br><br>**Yanıtlar üzerinde**: Kaynak sunucu doğrulaması olmadan bir sonraki istek için yanıt kullanılmamalıdır. |
| [No-store](https://tools.ietf.org/html/rfc7234#section-5.2.1.5) | **İsteklerinde**: Bir önbellek isteği depolamamayı gerekir.<br><br>**Yanıtlar üzerinde**: Bir önbellek yanıt herhangi bir bölümünü depolamamayı gerekir. |

Önbelleğe alma bir rol oynar diğer önbellek üst bilgileri aşağıdaki tabloda gösterilmektedir.

| Üstbilgi                                                     | İşlev |
| ---------------------------------------------------------- | -------- |
| [Geçerlilik süresi](https://tools.ietf.org/html/rfc7234#section-5.1)     | Yanıt beri geçen saniye sayısı süre miktarı tahmin oluşturulan veya kaynak sunucuda başarıyla doğrulandı. |
| [Süre sonu](https://tools.ietf.org/html/rfc7234#section-5.3) | Sonra yanıt eski olarak değerlendirmeden tarih. |
| [Pragma](https://tools.ietf.org/html/rfc7234#section-5.4)  | HTTP/1.0 ile uyumluluk ayarı için geriye doğru önbellekleri için mevcut `no-cache` davranışı. Varsa `Cache-Control` üstbilgisi mevcutsa, `Pragma` üstbilgi göz ardı edilir. |
| [değişiklik](https://tools.ietf.org/html/rfc7231#section-7.1.4)  | Önbelleğe alınan yanıt sürece tüm gönderilmemesini gerekir belirtir, `Vary` önbelleğe alınan yanıtın özgün istek ve yeni istek üst bilgi alanları eşleştir. |

## <a name="http-based-caching-respects-request-cache-control-directives"></a>HTTP tabanlı önbelleğe alma gizliliğinize Cache-Control yönergeleri istek

[Cache-Control üst bilgisi için HTTP 1.1 önbelleğe alma belirtimi](https://tools.ietf.org/html/rfc7234#section-5.2) geçerli kabul etmenin bir önbellek gerektirir `Cache-Control` istemci tarafından gönderilen başlığı. Bir istemci isteği ile yapabilen bir `no-cache` üstbilgi değeri ve zorla her istek için yeni bir yanıt oluşturmak için sunucu.

Her zaman istemci uygularken `Cache-Control` HTTP önbelleğe alma amacı gerçekleştiriliyorsa, istek üst bilgilerini mantıklı. Altında bir resmi belirtimi, önbelleğe alma, istemcileri ve proxy sunucuları, ağ üzerinden isteklerini karşılamak gecikme süresi ve ağ yükünü azaltmak için tasarlanmıştır. Mutlaka, kaynak sunucu üzerindeki yükü denetlemek için bir yol değil.

Kullanırken bu önbelleğe alma davranışı üzerinde Geliştirici denetimi olan [yanıt önbelleğe alma ara yazılımı](xref:performance/caching/middleware) çünkü resmi belirtimi önbelleğe alma ara yazılımı uyar. [Ara yazılım geliştirmeler planlı](https://github.com/aspnet/AspNetCore/issues/2612) bir isteğin yoksaymak için bir ara yazılım yapılandırmak için bir fırsat `Cache-Control` önbelleğe alınan yanıt hizmet verirken başlığı. Planlanan geliştirmeleri daha iyi denetim sunucu iş yükü için bir fırsat sağlar.

## <a name="other-caching-technology-in-aspnet-core"></a>ASP.NET core'da diğer önbelleğe alma teknolojisini

### <a name="in-memory-caching"></a>Bellek içi önbelleğe alma

Bellek içi caching, önbelleğe alınmış verileri depolamak için sunucu belleği kullanır. Bu tür bir önbelleğe alma, tek veya birden fazla sunucu kullanmak için uygundur *Yapışkan oturumlar*. Yapışkan oturumlar, istemciden gelen isteklere her zaman aynı sunucuya işleme yönlendirildiğinden anlamına gelir.

Daha fazla bilgi için [bellek içi önbelleğe alma](xref:performance/caching/memory).

### <a name="distributed-cache"></a>Dağıtılmış Önbellek

Uygulamayı bir bulut veya sunucu grubunda barındırıldığında bellek verilerini depolamak için Dağıtılmış bir önbellek kullanın. Önbelleği istekleri işleyen sunucular arasında paylaşılır. Bir istemci, istemci için önbelleğe alınan verileri kullanılabilir ise gruptaki hiçbir sunucu tarafından işlenen bir istek gönderebilirsiniz. ASP.NET Core, SQL Server ve dağıtılmış Redis önbellekleri sunar.

Daha fazla bilgi için bkz. <xref:performance/caching/distributed>.

### <a name="cache-tag-helper"></a>Önbellek etiketi Yardımcısı

Önbellek etiketi Yardımcısı ile bir MVC görünümü ya da bir Razor sayfası içeriği önbelleğe alabilir. Önbellek etiketi Yardımcısı, verileri depolamak için bellek içi önbelleğe alma kullanır.

Daha fazla bilgi için [önbellek etiketi Yardımcısı, ASP.NET Core MVC](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).

### <a name="distributed-cache-tag-helper"></a>Dağıtılmış önbellek etiketi Yardımcısı

Dağıtılmış önbellek etiketi Yardımcısı ile bir MVC görünümü ya da dağıtılmış bir bulut ya da web grubu senaryoları Razor sayfası içeriği önbelleğe alabilir. Dağıtılmış önbellek etiketi Yardımcısı, verileri depolamak için SQL Server veya Redis kullanır.

Daha fazla bilgi için [dağıtılmış önbellek etiketi Yardımcısı](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper).

## <a name="responsecache-attribute"></a>ResponseCache özniteliği

[ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute) yanıt önbelleğe alma uygun üstbilgileri ayarlamak için gerekli parametreleri belirtir.

> [!WARNING]
> Kimlik doğrulamasından geçen istemcilerin bilgilerini içeren içerik için önbelleğe alma devre dışı bırakın. Önbelleğe alma yalnızca bir kullanıcının kimlik veya bir kullanıcının oturum açtığı göre değişmeyen içerik için etkinleştirilmiş olmalıdır.

[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys) saklı yanıt sorgu anahtarları ait belirtilen liste değerleriyle göre değişir. Tek bir değeri `*` ara yazılım değişir, yanıtların tümü tarafından istek sorgu dizesi parametreleri sağlanır. `VaryByQueryKeys` ASP.NET Core 1.1 veya sonraki bir sürümü gerektirir.

[Yanıtları önbelleğe alma ara yazılımı](xref:performance/caching/middleware) ayarlamak için etkinleştirilmelidir `VaryByQueryKeys` özelliği; Aksi takdirde, çalışma zamanı özel durum oluşturulur. Karşılık gelen bir HTTP üst bilgisi için hiç `VaryByQueryKeys` özelliği. Özelliği, yanıt önbelleğe alma ara yazılımı tarafından işlenen bir HTTP özelliğidir. Önbelleğe alınan yanıt verecek ara yazılımı için sorgu dizesi ve sorgu dizesi değerini, önceki bir istek eşleşmelidir. Örneğin, istekler ve sonuçları aşağıdaki tabloda gösterilen bir dizi göz önünde bulundurun.

| İstek                          | Sonuç                   |
| -------------------------------- | ------------------------ |
| `http://example.com?key1=value1` | Sunucudan döndürülen     |
| `http://example.com?key1=value1` | Ara yazılım döndürülen |
| `http://example.com?key1=value2` | Sunucudan döndürülen     |

İlk istek sunucu tarafından döndürülen ve Ara yazılımında önbelleğe alınır. Önceki istek sorgu dizesini eşleştiği için ikinci isteği ara yazılımı tarafından döndürülür. Sorgu dizesi değerini, önceki bir istek eşleşmediği için üçüncü isteği ara yazılım önbellekte değil. 

`ResponseCacheAttribute` Yapılandırmak ve oluşturmak için kullanılır (aracılığıyla `IFilterFactory`) bir [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter). `ResponseCacheFilter` Uygun HTTP üst bilgilerini ve yanıt özellikleri güncelleştirme işlemlerini gerçekleştirir. Filtresi:

* Mevcut üst bilgileri için kaldırır `Vary`, `Cache-Control`, ve `Pragma`. 
* Kullanıma uygun üstbilgileri kümesinde özelliklerine göre Yazar `ResponseCacheAttribute`. 
* HTTP özelliği, önbelleğe alma yanıt güncelleştirmeleri `VaryByQueryKeys` ayarlanır.

### <a name="vary"></a>değişiklik

Bu üst bilginin ne zaman yalnızca yazılır `VaryByHeader` özelliği ayarlanmış. Ayarlanmış `Vary` özelliğinin değeri. Aşağıdaki örnek kullanımları `VaryByHeader` özelliği:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

Yanıt Üstbilgileri tarayıcınızın ağ araçları ile görüntüleyebilirsiniz. Aşağıdaki resimde gösterilmektedir Edge üzerinde çıkışını F12 **ağ** sekmesinde `About2` eylem yöntemine yenilenir:

![About2 eylem yöntemi çağrıldığında F12 çıkış Ağ sekmesinde kenar](response/_static/vary.png)

### <a name="nostore-and-locationnone"></a>NoStore ve Location.None

`NoStore` diğer özelliklerin çoğu geçersiz kılar. Bu özelliği ayarlandığında `true`, `Cache-Control` üstbilgi ayarlandığında `no-store`. Varsa `Location` ayarlanır `None`:

* `Cache-Control` ayarlanır `no-store,no-cache`.
* `Pragma` ayarlanır `no-cache`.

Varsa `NoStore` olduğu `false` ve `Location` olduğu `None`, `Cache-Control` ve `Pragma` ayarlandığından `no-cache`.

Genellikle ayarlanabilir `NoStore` için `true` hata sayfalarında. Örneğin:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

Bu, şu olur:

```
Cache-Control: no-store,no-cache
Pragma: no-cache
```

### <a name="location-and-duration"></a>Konum ve süresi

Önbelleğe alma, etkinleştirme `Duration` pozitif bir değere ayarlanması gerekir ve `Location` olmalıdır `Any` (varsayılan) veya `Client`. Bu durumda, `Cache-Control` üstbilgi arkasından konum değeri ayarlandığında `max-age` yanıtın.

> [!NOTE]
> `Location`ın seçenekleri `Any` ve `Client` küçültmesini `Cache-Control` üstbilgi değerlerini `public` ve `private`sırasıyla. Daha önce belirtildiği gibi ayarı `Location` için `None` hem de ayarlar `Cache-Control` ve `Pragma` üstbilgileri `no-cache`.

Ayarlayarak üstbilgileri gösteren bir örnek aşağıda üretilir `Duration` varsayılan bırakarak `Location` değeri:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

Bu, aşağıdaki üst bilgi oluşturur:

```
Cache-Control: public,max-age=60
```

### <a name="cache-profiles"></a>Önbellek profilleri

Çoğaltma yerine `ResponseCache` birçok denetleyici eylem özniteliklerinin, önbellek profilleri ayarları MVC'de ayarlarken seçeneği olarak yapılandırılabilir `ConfigureServices` yönteminde `Startup`. Başvurulan önbellek profilinde bulunan değerleri tarafından varsayılan olarak kullanılır `ResponseCache` öznitelik ve öznitelik üzerinde belirtilen herhangi bir özelliği tarafından geçersiz kılınır.

Önbellek profili ayarlama:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

Önbellek profili başvuruyor:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

`ResponseCache` Özniteliği, hem Eylemler (yöntem) ve denetleyicilerine (sınıflar) uygulanabilir. Yöntem düzeyindeki öznitelikler, sınıf düzeyi özniteliklerinde belirtilen ayarları geçersiz kılar.

60 saniye olarak belirlendi süre önbellek profili yöntemi düzeyinde bir öznitelik başvuruyor ancak yukarıdaki örnekte, 30 saniye süre sınıf düzeyinde bir öznitelik belirtir.

Sonuçta elde edilen üst bilgi:

```
Cache-Control: public,max-age=60
```

## <a name="additional-resources"></a>Ek kaynaklar

* [Yanıtları depolama önbelleklerinde](https://tools.ietf.org/html/rfc7234#section-3)
* [Önbellek denetimi](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* <xref:performance/caching/memory>
* <xref:performance/caching/distributed>
* <xref:fundamentals/change-tokens>
* <xref:performance/caching/middleware>
* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper>
