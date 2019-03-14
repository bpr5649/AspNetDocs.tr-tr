---
title: ASP.NET Core kimliği doğrulanmış şifreleme ayrıntıları
author: rick-anderson
description: ASP.NET Core veri koruma kimliği doğrulanmış şifreleme uygulama ayrıntıları öğrenin.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/authenticated-encryption-details
ms.openlocfilehash: ac650e5c32e7eacc4088225e63f56340f95e1913
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072960"
---
# <a name="authenticated-encryption-details-in-aspnet-core"></a><span data-ttu-id="498f2-103">ASP.NET Core kimliği doğrulanmış şifreleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="498f2-103">Authenticated encryption details in ASP.NET Core</span></span>

<a name="data-protection-implementation-authenticated-encryption-details"></a>

<span data-ttu-id="498f2-104">Kimliği doğrulanmış şifreleme IDataProtector.Protect çağrıları işlemlerdir.</span><span class="sxs-lookup"><span data-stu-id="498f2-104">Calls to IDataProtector.Protect are authenticated encryption operations.</span></span> <span data-ttu-id="498f2-105">Bu Idataprotector örnekte kendi kök IDataProtectionProvider türetmek için kullanılan amaçlı zinciri bağlıdır ve koruma yöntemi hem gizliliği ve kimlik doğrulama sunar.</span><span class="sxs-lookup"><span data-stu-id="498f2-105">The Protect method offers both confidentiality and authenticity, and it's tied to the purpose chain that was used to derive this particular IDataProtector instance from its root IDataProtectionProvider.</span></span>

<span data-ttu-id="498f2-106">IDataProtector.Protect bayt [] düz metin parametre alır ve aşağıda açıklanan biçimde bir bayt [] korumalı yükü üretir.</span><span class="sxs-lookup"><span data-stu-id="498f2-106">IDataProtector.Protect takes a byte[] plaintext parameter and produces a byte[] protected payload, whose format is described below.</span></span> <span data-ttu-id="498f2-107">(Var. Ayrıca bir dize düz metin parametresi alan ve bir dize korumalı yükü döndüren bir genişletme yöntemi aşırı yüklemesi</span><span class="sxs-lookup"><span data-stu-id="498f2-107">(There's also an extension method overload which takes a string plaintext parameter and returns a string protected payload.</span></span> <span data-ttu-id="498f2-108">Bu API kullanılıyorsa, korumalı yükü biçimde hala olan yapısı, aşağıda ancak olur [base64url kodlu](https://tools.ietf.org/html/rfc4648#section-5).)</span><span class="sxs-lookup"><span data-stu-id="498f2-108">If this API is used the protected payload format will still have the below structure, but it will be [base64url-encoded](https://tools.ietf.org/html/rfc4648#section-5).)</span></span>

## <a name="protected-payload-format"></a><span data-ttu-id="498f2-109">Korumalı yük biçimi</span><span class="sxs-lookup"><span data-stu-id="498f2-109">Protected payload format</span></span>

<span data-ttu-id="498f2-110">Korumalı yük biçimi üç birincil bileşenden oluşur:</span><span class="sxs-lookup"><span data-stu-id="498f2-110">The protected payload format consists of three primary components:</span></span>

* <span data-ttu-id="498f2-111">Veri koruma sisteminde sürümünü tanımlayan bir 32-bit Sihirli üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="498f2-111">A 32-bit magic header that identifies the version of the data protection system.</span></span>

* <span data-ttu-id="498f2-112">Bu belirli yük korumak için kullanılan anahtarı tanımlar 128 bit anahtar kimliği.</span><span class="sxs-lookup"><span data-stu-id="498f2-112">A 128-bit key id that identifies the key used to protect this particular payload.</span></span>

* <span data-ttu-id="498f2-113">Korumalı yük kalan [bu anahtara göre kapsüllenmiş Şifreleyici özgü](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation).</span><span class="sxs-lookup"><span data-stu-id="498f2-113">The remainder of the protected payload is [specific to the encryptor encapsulated by this key](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation).</span></span> <span data-ttu-id="498f2-114">Aşağıdaki örnekte tuşunu temsil eder bir AES 256 CBC + HMACSHA256 Şifreleyici ve yükü daha ayrıntılı şekilde ayrılır: \* A 128 bit anahtar değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="498f2-114">In the example below the key represents an AES-256-CBC + HMACSHA256 encryptor, and the payload is further subdivided as follows: \* A 128-bit key modifier.</span></span> <span data-ttu-id="498f2-115">\* Bir 128-bit başlatma vektörü.</span><span class="sxs-lookup"><span data-stu-id="498f2-115">\* A 128-bit initialization vector.</span></span> <span data-ttu-id="498f2-116">\* AES 256 CBC çıkış 48 bayt.</span><span class="sxs-lookup"><span data-stu-id="498f2-116">\* 48 bytes of AES-256-CBC output.</span></span> <span data-ttu-id="498f2-117">\* Bir HMACSHA256 kimlik doğrulaması etiketi.</span><span class="sxs-lookup"><span data-stu-id="498f2-117">\* An HMACSHA256 authentication tag.</span></span>

<span data-ttu-id="498f2-118">Bir korumalı örnek yük aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="498f2-118">A sample protected payload is illustrated below.</span></span>

```
09 F0 C9 F0 80 9C 81 0C 19 66 19 40 95 36 53 F8
AA FF EE 57 57 2F 40 4C 3F 7F CC 9D CC D9 32 3E
84 17 99 16 EC BA 1F 4A A1 18 45 1F 2D 13 7A 28
79 6B 86 9C F8 B7 84 F9 26 31 FC B1 86 0A F1 56
61 CF 14 58 D3 51 6F CF 36 50 85 82 08 2D 3F 73
5F B0 AD 9E 1A B2 AE 13 57 90 C8 F5 7C 95 4E 6A
8A AA 06 EF 43 CA 19 62 84 7C 11 B2 C8 71 9D AA
52 19 2E 5B 4C 1E 54 F0 55 BE 88 92 12 C1 4B 5E
52 C9 74 A0
```

<span data-ttu-id="498f2-119">(09 F0 C9 F0) sürümünü tanımlayan Sihirli üstbilgi ilk 32 bit veya 4 bayt yukarıda yük biçimi arasındadır</span><span class="sxs-lookup"><span data-stu-id="498f2-119">From the payload format above the first 32 bits, or 4 bytes are the magic header identifying the version (09 F0 C9 F0)</span></span>

<span data-ttu-id="498f2-120">Sonraki 128 bit ya da 16 bayt olan anahtar tanımlayıcısı (80 9C 81 0C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span><span class="sxs-lookup"><span data-stu-id="498f2-120">The next 128 bits, or 16 bytes is the key identifier (80 9C 81 0C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span></span>

<span data-ttu-id="498f2-121">Kalan yükü içerir ve kullanılan biçimi özgüdür.</span><span class="sxs-lookup"><span data-stu-id="498f2-121">The remainder contains the payload and is specific to the format used.</span></span>

>[!WARNING]
> <span data-ttu-id="498f2-122">Belirli bir anahtarın için korunan tüm yükleri aynı 20 baytlık (Sihirli değeri, anahtar kimliği) üst bilgisi ile başlar.</span><span class="sxs-lookup"><span data-stu-id="498f2-122">All payloads protected to a given key will begin with the same 20-byte (magic value, key id) header.</span></span> <span data-ttu-id="498f2-123">Yöneticiler, bir yük oluşturulduğunda yaklaşık olarak belirlemenizi sağlayan bu olgu tanılama amacıyla kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="498f2-123">Administrators can use this fact for diagnostic purposes to approximate when a payload was generated.</span></span> <span data-ttu-id="498f2-124">Örneğin, yukarıdaki yükü {0c819c80-6619-4019-9536-53f8aaffee57} anahtarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="498f2-124">For example, the payload above corresponds to key {0c819c80-6619-4019-9536-53f8aaffee57}.</span></span> <span data-ttu-id="498f2-125">Anahtar deposu denetledikten sonra bu belirli bir anahtarın etkinleştirme tarihine gelindiğinden 2015-01-01 ve 2015-03-01, sona erme tarihine gelindiğinden sonra varsayımında şüphelenilebilir fark ederseniz yük (değiştirilmiş değil) sağlar, pencere içinde oluşturulan veya küçük olması Her iki tarafında karamelli faktörü.</span><span class="sxs-lookup"><span data-stu-id="498f2-125">If after checking the key repository you find that this specific key's activation date was 2015-01-01 and its expiration date was 2015-03-01, then it's reasonable to assume that the payload (if not tampered with) was generated within that window, give or take a small fudge factor on either side.</span></span>
