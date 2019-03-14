---
title: ASP.NET core'da anahtar yönetimi
author: rick-anderson
description: ASP.NET Core veri koruma anahtar yönetimi API'leri uygulama ayrıntılarını öğrenin.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-management
ms.openlocfilehash: 431bdf2d3076c83279b78f327ddb647f69e6e584
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071412"
---
# <a name="key-management-in-aspnet-core"></a><span data-ttu-id="76bee-103">ASP.NET core'da anahtar yönetimi</span><span class="sxs-lookup"><span data-stu-id="76bee-103">Key management in ASP.NET Core</span></span>

<a name="data-protection-implementation-key-management"></a>

<span data-ttu-id="76bee-104">Veri koruma sisteminde ana korumak ve yüklerin korumasını kaldırma için kullanılan anahtarları ömrünü otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="76bee-104">The data protection system automatically manages the lifetime of master keys used to protect and unprotect payloads.</span></span> <span data-ttu-id="76bee-105">Her anahtar dört aşamasını biri mevcut olabilir:</span><span class="sxs-lookup"><span data-stu-id="76bee-105">Each key can exist in one of four stages:</span></span>

* <span data-ttu-id="76bee-106">Oluşturulan - anahtar, anahtar halka var ancak henüz etkinleştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="76bee-106">Created - the key exists in the key ring but has not yet been activated.</span></span> <span data-ttu-id="76bee-107">Yeterli süre kadar anahtarı bu anahtarı kademeyi kullanan tüm makinelere yaymak için bir fırsat oluşmuş anahtarı yeni koruma işlemleri için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="76bee-107">The key shouldn't be used for new Protect operations until sufficient time has elapsed that the key has had a chance to propagate to all machines that are consuming this key ring.</span></span>

* <span data-ttu-id="76bee-108">Etkin - anahtar, anahtar halka var ve tüm yeni koruma işlemleri için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="76bee-108">Active - the key exists in the key ring and should be used for all new Protect operations.</span></span>

* <span data-ttu-id="76bee-109">Kullanım süresi doldu - anahtar doğal ömrü çalıştırıldı ve artık yeni koruma işlemleri için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="76bee-109">Expired - the key has run its natural lifetime and should no longer be used for new Protect operations.</span></span>

* <span data-ttu-id="76bee-110">İptal edilen - anahtar tehlikeye ve yeni koruma işlemleri için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="76bee-110">Revoked - the key is compromised and must not be used for new Protect operations.</span></span>

<span data-ttu-id="76bee-111">Oluşturulan, etkin ve süresi dolan anahtarlar tüm gelen yüklerin korumasını kaldırma için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-111">Created, active, and expired keys may all be used to unprotect incoming payloads.</span></span> <span data-ttu-id="76bee-112">Varsayılan olarak, iptal edilen anahtarları yüklerin korumasını kaldırma için kullanılamaz, ancak uygulama geliştiricisi için [bu davranışı geçersiz kılma](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect) gerekirse.</span><span class="sxs-lookup"><span data-stu-id="76bee-112">Revoked keys by default may not be used to unprotect payloads, but the application developer can [override this behavior](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect) if necessary.</span></span>

>[!WARNING]
> <span data-ttu-id="76bee-113">Geliştirici (örneğin, karşılık gelen dosyayı dosya sisteminden silerek) anahtar halka dışında bir anahtarı silme fikri size cazip olabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-113">The developer might be tempted to delete a key from the key ring (e.g., by deleting the corresponding file from the file system).</span></span> <span data-ttu-id="76bee-114">Bu noktada, anahtar tarafından korunan tüm verileri kalıcı olarak undecipherable ve iptal edilen anahtarlarla gibi Acil Durum geçersiz kılma yoktur.</span><span class="sxs-lookup"><span data-stu-id="76bee-114">At that point, all data protected by the key is permanently undecipherable, and there's no emergency override like there's with revoked keys.</span></span> <span data-ttu-id="76bee-115">Bir anahtarı silme gerçekten yıkıcı davranıştır ve sonuç olarak bu işlemi gerçekleştirmek için veri koruma sisteminde birinci sınıf yok API sunar.</span><span class="sxs-lookup"><span data-stu-id="76bee-115">Deleting a key is truly destructive behavior, and consequently the data protection system exposes no first-class API for performing this operation.</span></span>

## <a name="default-key-selection"></a><span data-ttu-id="76bee-116">Varsayılan anahtar seçimi</span><span class="sxs-lookup"><span data-stu-id="76bee-116">Default key selection</span></span>

<span data-ttu-id="76bee-117">Veri koruma sisteminde yedekleme deposundan anahtar halkası okuduğunda, bir "varsayılan" anahtar, anahtar halkası bulun dener.</span><span class="sxs-lookup"><span data-stu-id="76bee-117">When the data protection system reads the key ring from the backing repository, it will attempt to locate a "default" key from the key ring.</span></span> <span data-ttu-id="76bee-118">Varsayılan anahtar yeni koruma işlemleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="76bee-118">The default key is used for new Protect operations.</span></span>

<span data-ttu-id="76bee-119">Veri koruma sisteminde varsayılan anahtarı olarak en son etkinleştirme tarihi anahtarla seçtiği genel buluşsal yöntem olur.</span><span class="sxs-lookup"><span data-stu-id="76bee-119">The general heuristic is that the data protection system chooses the key with the most recent activation date as the default key.</span></span> <span data-ttu-id="76bee-120">(Küçük karamelli faktörü için sunucudan sunucuya saat eğriltme olanak yoktur.) Anahtarın süresi doldu veya iptal, anahtar oluşturma ve uygulama otomatik devre dışı ise durumunda yeni bir anahtar hemen etkinleştirme ile oluşturulan [anahtar süre sonu ve sıralı](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) aşağıdaki ilke.</span><span class="sxs-lookup"><span data-stu-id="76bee-120">(There's a small fudge factor to allow for server-to-server clock skew.) If the key is expired or revoked, and if the application has not disabled automatic key generation, then a new key will be generated with immediate activation per the [key expiration and rolling](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) policy below.</span></span>

<span data-ttu-id="76bee-121">Veri koruma sisteminde neden yeni bir anahtar hemen oluşturur yerine yeni anahtar oluşturma, yeni anahtar önce etkinleştirilen tüm anahtarların örtük bir sona erme olarak değerlendirilip olan farklı bir anahtara geri dönülüyor.</span><span class="sxs-lookup"><span data-stu-id="76bee-121">The reason the data protection system generates a new key immediately rather than falling back to a different key is that new key generation should be treated as an implicit expiration of all keys that were activated prior to the new key.</span></span> <span data-ttu-id="76bee-122">Genel yeni anahtarları farklı algoritmalar veya daha eski anahtarları bekleyen şifreleme mekanizmaları ile yapılandırılmış olabilir ve sistemin geçerli yapılandırmasını dönülüyor tercih etmelisiniz olur.</span><span class="sxs-lookup"><span data-stu-id="76bee-122">The general idea is that new keys may have been configured with different algorithms or encryption-at-rest mechanisms than old keys, and the system should prefer the current configuration over falling back.</span></span>

<span data-ttu-id="76bee-123">Bir özel durum söz konusudur.</span><span class="sxs-lookup"><span data-stu-id="76bee-123">There's an exception.</span></span> <span data-ttu-id="76bee-124">Uygulama geliştiricisi varsa [otomatik anahtar oluşturma devre dışı](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), sonra da veri koruma sisteminde bir varsayılan anahtar olarak seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76bee-124">If the application developer has [disabled automatic key generation](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), then the data protection system must choose something as the default key.</span></span> <span data-ttu-id="76bee-125">Geri dönüş Bu senaryoda, kümedeki diğer makinelere yaymak için bir süre beklendiğinden anahtarlarına öncelik ile en son etkinleştirme tarihi olmayan iptal anahtarla sistemi seçer.</span><span class="sxs-lookup"><span data-stu-id="76bee-125">In this fallback scenario, the system will choose the non-revoked key with the most recent activation date, with preference given to keys that have had time to propagate to other machines in the cluster.</span></span> <span data-ttu-id="76bee-126">Geri dönüş sistemi, süresi dolmuş varsayılan anahtar sonucunda seçme sonlandırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="76bee-126">The fallback system may end up choosing an expired default key as a result.</span></span> <span data-ttu-id="76bee-127">Geri dönüş sistemi hiçbir zaman iptal edilen bir anahtar varsayılan anahtarı olarak seçer ve ardından anahtar halkası boş ise veya her anahtarı iptal edilmiş sistem başlatma sırasında bir hata üretecektir.</span><span class="sxs-lookup"><span data-stu-id="76bee-127">The fallback system will never choose a revoked key as the default key, and if the key ring is empty or every key has been revoked then the system will produce an error upon initialization.</span></span>

<a name="data-protection-implementation-key-management-expiration"></a>

## <a name="key-expiration-and-rolling"></a><span data-ttu-id="76bee-128">Anahtarı süre sonu ve sıralı</span><span class="sxs-lookup"><span data-stu-id="76bee-128">Key expiration and rolling</span></span>

<span data-ttu-id="76bee-129">Bir anahtar oluşturulduğunda bir etkinleştirme tarihi {now + 2 gün} ve {now + 90 gün} bir sona erme tarihi otomatik olarak sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="76bee-129">When a key is created, it's automatically given an activation date of { now + 2 days } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="76bee-130">Etkinleştirme 2 gün gecikmeyle sistem üzerinden yaymak için anahtar zaman verir.</span><span class="sxs-lookup"><span data-stu-id="76bee-130">The 2-day delay before activation gives the key time to propagate through the system.</span></span> <span data-ttu-id="76bee-131">Diğer bir deyişle, anahtar, sonraki otomatik yenileme dönemi boyunca, böylece anahtar halka ettiğinde, yayılmadan olur mu etkin gerekebilecek tüm uygulamaları kullanın, büyük olasılıkla en üst düzeye gözlemlemek yedekleme mağazada işaret eden diğer uygulamaların izin verir.</span><span class="sxs-lookup"><span data-stu-id="76bee-131">That is, it allows other applications pointing at the backing store to observe the key at their next auto-refresh period, thus maximizing the chances that when the key ring does become active it has propagated to all applications that might need to use it.</span></span>

<span data-ttu-id="76bee-132">Varsayılan anahtar 2 gün içinde sona erecek ve anahtar halkası varsayılan anahtarı sona erdikten sonra etkin olan bir anahtar zaten yoksa, veri koruma sisteminde yeni bir anahtar halkası anahtarına otomatik olarak korunur.</span><span class="sxs-lookup"><span data-stu-id="76bee-132">If the default key will expire within 2 days and if the key ring doesn't already have a key that will be active upon expiration of the default key, then the data protection system will automatically persist a new key to the key ring.</span></span> <span data-ttu-id="76bee-133">Bu yeni anahtar bir etkinleştirme tarihi {varsayılan anahtarının sona erme tarihi} ve {now + 90 gün} bir sona erme tarihi vardır.</span><span class="sxs-lookup"><span data-stu-id="76bee-133">This new key has an activation date of { default key's expiration date } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="76bee-134">Bu anahtarlar düzenli olarak hizmet kesinti olmadan otomatik olarak geri almak sistem sağlar.</span><span class="sxs-lookup"><span data-stu-id="76bee-134">This allows the system to automatically roll keys on a regular basis with no interruption of service.</span></span>

<span data-ttu-id="76bee-135">Bir anahtar ile hemen etkinleştirme oluşturulacağı durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-135">There might be circumstances where a key will be created with immediate activation.</span></span> <span data-ttu-id="76bee-136">Bir örnek uygulama için bir saat boyunca çalışmamışsa ve tüm anahtar halkası anahtarlarında süresi dolmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-136">One example would be when the application hasn't run for a time and all keys in the key ring are expired.</span></span> <span data-ttu-id="76bee-137">Bu durumda, anahtar {şimdi} normal 2 günlük etkinleştirme gecikme olmadan bir etkinleştirme tarihi verilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-137">When this happens, the key is given an activation date of { now } without the normal 2-day activation delay.</span></span>

<span data-ttu-id="76bee-138">Varsayılan anahtar yaşam süresi 90 gün, aşağıdaki örnekte olduğu gibi yapılandırılabilir ancak.</span><span class="sxs-lookup"><span data-stu-id="76bee-138">The default key lifetime is 90 days, though this is configurable as in the following example.</span></span>

```csharp
services.AddDataProtection()
       // use 14-day lifetime instead of 90-day lifetime
       .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
```

<span data-ttu-id="76bee-139">Açık bir çağrı olsa yönetici aynı zamanda varsayılan sistem genelinde değiştirebilirsiniz `SetDefaultKeyLifetime` tüm sistem genelinde bir ilke geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="76bee-139">An administrator can also change the default system-wide, though an explicit call to `SetDefaultKeyLifetime` will override any system-wide policy.</span></span> <span data-ttu-id="76bee-140">Varsayılan anahtar yaşam süresi 7 günden daha kısa olamaz.</span><span class="sxs-lookup"><span data-stu-id="76bee-140">The default key lifetime cannot be shorter than 7 days.</span></span>

## <a name="automatic-key-ring-refresh"></a><span data-ttu-id="76bee-141">Otomatik anahtar halkası yenileme</span><span class="sxs-lookup"><span data-stu-id="76bee-141">Automatic key ring refresh</span></span>

<span data-ttu-id="76bee-142">Veri koruma sisteminde başlatır, temel alınan depodan anahtar halkası okur ve bellekte önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="76bee-142">When the data protection system initializes, it reads the key ring from the underlying repository and caches it in memory.</span></span> <span data-ttu-id="76bee-143">Bu önbellek yedekleme deposu ulaşmaktan olmadan devam etmek, koruma ve Unprotect işlemlere izin verir.</span><span class="sxs-lookup"><span data-stu-id="76bee-143">This cache allows Protect and Unprotect operations to proceed without hitting the backing store.</span></span> <span data-ttu-id="76bee-144">Sistem otomatik olarak yaklaşık 24 saatte veya geçerli varsayılan anahtar süresi dolduğunda, hangisinin önce geldiğine bağlı değişiklikleri yedekleme deposu kontrol edecektir.</span><span class="sxs-lookup"><span data-stu-id="76bee-144">The system will automatically check the backing store for changes approximately every 24 hours or when the current default key expires, whichever comes first.</span></span>

>[!WARNING]
> <span data-ttu-id="76bee-145">Geliştiriciler gereken çok nadir (Şimdiye kadar değilse) anahtar yönetimi API'lerini doğrudan kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="76bee-145">Developers should very rarely (if ever) need to use the key management APIs directly.</span></span> <span data-ttu-id="76bee-146">Veri koruma sistemi otomatik anahtar yönetimi, yukarıda açıklanan şekilde gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="76bee-146">The data protection system will perform automatic key management as described above.</span></span>

<span data-ttu-id="76bee-147">Veri koruma sisteminde bir arabirimi kullanıma sunan `IKeyManager` incelemek için anahtar halkası değişiklikler yapmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-147">The data protection system exposes an interface `IKeyManager` that can be used to inspect and make changes to the key ring.</span></span> <span data-ttu-id="76bee-148">Örneğini sağlanan DI sistem `IDataProtectionProvider` örneği de sağlayabilirsiniz `IKeyManager` tüketiminiz için.</span><span class="sxs-lookup"><span data-stu-id="76bee-148">The DI system that provided the instance of `IDataProtectionProvider` can also provide an instance of `IKeyManager` for your consumption.</span></span> <span data-ttu-id="76bee-149">Alternatif olarak, çekme `IKeyManager` doğrudan gelen `IServiceProvider` aşağıdaki örnekte olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="76bee-149">Alternatively, you can pull the `IKeyManager` straight from the `IServiceProvider` as in the example below.</span></span>

<span data-ttu-id="76bee-150">Anahtar (yeni bir anahtar açıkça oluşturma veya iptali gerçekleştirme) halkası değiştirir, herhangi bir işlem, bellek içi önbellek geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="76bee-150">Any operation which modifies the key ring (creating a new key explicitly or performing a revocation) will invalidate the in-memory cache.</span></span> <span data-ttu-id="76bee-151">Sonraki çağrı `Protect` veya `Unprotect` anahtar halkası yeniden okuyun ve önbelleği yeniden oluşturmak veri koruma sisteminde neden olur.</span><span class="sxs-lookup"><span data-stu-id="76bee-151">The next call to `Protect` or `Unprotect` will cause the data protection system to reread the key ring and recreate the cache.</span></span>

<span data-ttu-id="76bee-152">Aşağıdaki örneği kullanarak gösterir `IKeyManager` inceleyin ve belirtece anahtarları mevcut ve yeni bir anahtarı el ile oluşturma da dahil olmak üzere anahtar halkası işlemek için arabirim.</span><span class="sxs-lookup"><span data-stu-id="76bee-152">The sample below demonstrates using the `IKeyManager` interface to inspect and manipulate the key ring, including revoking existing keys and generating a new key manually.</span></span>

[!code-csharp[](key-management/samples/key-management.cs)]

## <a name="key-storage"></a><span data-ttu-id="76bee-153">Anahtar depolama</span><span class="sxs-lookup"><span data-stu-id="76bee-153">Key storage</span></span>

<span data-ttu-id="76bee-154">Veri koruma sisteminde verebileceğiniz bir uygun anahtar depolama konumu ve bekleyen şifreleme mekanizması otomatik olarak çıkarmaya çalışır bir buluşsal yönteme sahip.</span><span class="sxs-lookup"><span data-stu-id="76bee-154">The data protection system has a heuristic whereby it attempts to deduce an appropriate key storage location and encryption-at-rest mechanism automatically.</span></span> <span data-ttu-id="76bee-155">Anahtar kalıcılığı mekanizmasının Ayrıca uygulama geliştiricisi tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="76bee-155">The key persistence mechanism is also configurable by the app developer.</span></span> <span data-ttu-id="76bee-156">Aşağıdaki belgeler, bu mekanizmaların yerleşik uygulamalar açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="76bee-156">The following documents discuss the in-box implementations of these mechanisms:</span></span>

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>