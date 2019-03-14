---
title: ASP.NET Core karma parolalar
author: rick-anderson
description: ASP.NET Core veri koruma API'lerini kullanarak parolaları karma öğrenin.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: 70301ffffbaaf3c5ff0642b19b80e40be83aa438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070518"
---
# <a name="hash-passwords-in-aspnet-core"></a>ASP.NET Core karma parolalar

Veri koruma kod tabanı içeren bir paket *Microsoft.AspNetCore.Cryptography.KeyDerivation* şifreleme anahtar türetme işlevleri içerir. Bu paket, bir tek başına bileşeni ve veri koruma sistemin geri kalanı üzerinde bağımlılık yok. Tamamen bağımsız olarak kullanılabilir. Veri koruma kod kolaylık tabanı yanı sıra kaynağı yok.

Paket şu anda bir yöntem sunar `KeyDerivation.Pbkdf2` sağlayan kullanarak bir parolayı karma [PBKDF2 algoritması](https://tools.ietf.org/html/rfc2898#section-5.2). Bu API .NET Framework'ün varolan çok benzer [Rfc2898DeriveBytes türü](/dotnet/api/system.security.cryptography.rfc2898derivebytes), ancak üç önemli farklılıklar vardır:

1. `KeyDerivation.Pbkdf2` Yöntem, birden çok PRFs tüketen destekler (şu anda `HMACSHA1`, `HMACSHA256`, ve `HMACSHA512`) bilgileriyse `Rfc2898DeriveBytes` destekler yazın `HMACSHA1`.

2. `KeyDerivation.Pbkdf2` Yöntemi geçerli işletim sistemini algılar ve bazı durumlarda çok daha iyi performans sağlayan yordamının en iyileştirilmiş uygulamayı seçme dener. (İsteğe bağlı olarak Windows 8'de yaklaşık 10 aktarım hızı x sunar `Rfc2898DeriveBytes`.)

3. `KeyDerivation.Pbkdf2` Yöntemi çağıran tüm parametreleri belirtmek gerektirir (salt, PRF ve yineleme sayısı). `Rfc2898DeriveBytes` Türü için varsayılan değerleri sağlar.

[!code-csharp[](password-hashing/samples/passwordhasher.cs)]

Bkz: [kaynak kodu](https://github.com/aspnet/Identity/blob/master/src/Core/PasswordHasher.cs) için ASP.NET Core kimliğin `PasswordHasher` gerçek dünya için tür kullanım örneği.
