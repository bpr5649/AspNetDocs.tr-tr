---
title: Veri koruma makine geneli ilke içinde ASP.NET Core desteği
author: rick-anderson
description: Bir ASP.NET Core veri koruması kullanan tüm uygulamalar için varsayılan makine geneli ilke ayarlama desteği hakkında daha fazla bilgi edinin.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/configuration/machine-wide-policy
ms.openlocfilehash: 70aaca7afcd3df22cebb4466fbd9845a2277688c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075339"
---
# <a name="data-protection-machine-wide-policy-support-in-aspnet-core"></a><span data-ttu-id="5a703-103">Veri koruma makine geneli ilke içinde ASP.NET Core desteği</span><span class="sxs-lookup"><span data-stu-id="5a703-103">Data Protection machine-wide policy support in ASP.NET Core</span></span>

<span data-ttu-id="5a703-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5a703-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="5a703-105">Windows üzerinde çalışırken, veri koruma sisteminde bir ASP.NET Core veri koruması kullanan tüm uygulamalar için varsayılan makine geneli ilke ayarlamak için destek sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="5a703-105">When running on Windows, the Data Protection system has limited support for setting a default machine-wide policy for all apps that consume ASP.NET Core Data Protection.</span></span> <span data-ttu-id="5a703-106">Genel yönetici gibi kullanılan algoritmalar varsayılan ayarı veya anahtar kullanım süresi, her uygulama makinede el ile güncelleştirmek zorunda kalmadan değiştirmek isteyebileceğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="5a703-106">The general idea is that an administrator might wish to change a default setting, such as the algorithms used or key lifetime, without the need to manually update every app on the machine.</span></span>

> [!WARNING]
> <span data-ttu-id="5a703-107">Sistem Yöneticisi varsayılan ilkesi ayarlayabilirsiniz ancak onu zorla uygulayamaz.</span><span class="sxs-lookup"><span data-stu-id="5a703-107">The system administrator can set default policy, but they can't enforce it.</span></span> <span data-ttu-id="5a703-108">Uygulama geliştiricisi biriyle kendi seçerek herhangi bir değer her zaman geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a703-108">The app developer can always override any value with one of their own choosing.</span></span> <span data-ttu-id="5a703-109">Varsayılan ilke, yalnızca bir ayar için açık bir değer Geliştirici burada belirtilen edilmemiş uygulamalar etkiler.</span><span class="sxs-lookup"><span data-stu-id="5a703-109">The default policy only affects apps where the developer hasn't specified an explicit value for a setting.</span></span>

## <a name="setting-default-policy"></a><span data-ttu-id="5a703-110">Varsayılan ilke ayarını</span><span class="sxs-lookup"><span data-stu-id="5a703-110">Setting default policy</span></span>

<span data-ttu-id="5a703-111">Varsayılan ilkesini ayarlamak için yönetici bilinen değerler sistem kayıt defterinde aşağıdaki kayıt defteri anahtarı altında ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5a703-111">To set default policy, an administrator can set known values in the system registry under the following registry key:</span></span>

<span data-ttu-id="5a703-112">**HKLM\SOFTWARE\Microsoft\DotNetPackages\Microsoft.AspNetCore.DataProtection**</span><span class="sxs-lookup"><span data-stu-id="5a703-112">**HKLM\SOFTWARE\Microsoft\DotNetPackages\Microsoft.AspNetCore.DataProtection**</span></span>

<span data-ttu-id="5a703-113">Bir 64-bit işletim sisteminde yapıyorsanız ve 32-bit uygulamaları davranışını etkilemek istiyorsunuz, yukarıdaki anahtar Wow6432Node denk yapılandırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5a703-113">If you're on a 64-bit operating system and want to affect the behavior of 32-bit apps, remember to configure the Wow6432Node equivalent of the above key.</span></span>

<span data-ttu-id="5a703-114">Desteklenen değerler aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5a703-114">The supported values are shown below.</span></span>

| <span data-ttu-id="5a703-115">Değer</span><span class="sxs-lookup"><span data-stu-id="5a703-115">Value</span></span>              | <span data-ttu-id="5a703-116">Tür</span><span class="sxs-lookup"><span data-stu-id="5a703-116">Type</span></span>   | <span data-ttu-id="5a703-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a703-117">Description</span></span> |
| ------------------ | :----: | ----------- |
| <span data-ttu-id="5a703-118">EncryptionType</span><span class="sxs-lookup"><span data-stu-id="5a703-118">EncryptionType</span></span>     | <span data-ttu-id="5a703-119">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-119">string</span></span> | <span data-ttu-id="5a703-120">Hangi algoritmaları veri koruma için kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a703-120">Specifies which algorithms should be used for data protection.</span></span> <span data-ttu-id="5a703-121">Değer, CNG CBC, CNG GCM veya yönetilen olmalıdır ve aşağıda daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5a703-121">The value must be CNG-CBC, CNG-GCM, or Managed and is described in more detail below.</span></span> |
| <span data-ttu-id="5a703-122">DefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="5a703-122">DefaultKeyLifetime</span></span> | <span data-ttu-id="5a703-123">DWORD</span><span class="sxs-lookup"><span data-stu-id="5a703-123">DWORD</span></span>  | <span data-ttu-id="5a703-124">Yeni oluşturulan anahtarları için yaşam süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a703-124">Specifies the lifetime for newly-generated keys.</span></span> <span data-ttu-id="5a703-125">Değer, gün içinde belirtilen ve olmalıdır > = 7.</span><span class="sxs-lookup"><span data-stu-id="5a703-125">The value is specified in days and must be >= 7.</span></span> |
| <span data-ttu-id="5a703-126">KeyEscrowSinks</span><span class="sxs-lookup"><span data-stu-id="5a703-126">KeyEscrowSinks</span></span>     | <span data-ttu-id="5a703-127">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-127">string</span></span> | <span data-ttu-id="5a703-128">Anahtar emanet için kullanılan türlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a703-128">Specifies the types that are used for key escrow.</span></span> <span data-ttu-id="5a703-129">Listedeki her öğe uygulayan bir tür bütünleştirilmiş kodla nitelenen adı olduğu anahtar emanet havuzlarını noktalı virgülle ayrılmış listesini değerdir [IKeyEscrowSink](/dotnet/api/microsoft.aspnetcore.dataprotection.keymanagement.ikeyescrowsink).</span><span class="sxs-lookup"><span data-stu-id="5a703-129">The value is a semicolon-delimited list of key escrow sinks, where each element in the list is the assembly-qualified name of a type that implements [IKeyEscrowSink](/dotnet/api/microsoft.aspnetcore.dataprotection.keymanagement.ikeyescrowsink).</span></span> |

## <a name="encryption-types"></a><span data-ttu-id="5a703-130">Şifreleme türleri</span><span class="sxs-lookup"><span data-stu-id="5a703-130">Encryption types</span></span>

<span data-ttu-id="5a703-131">CNG CBC EncryptionType ise sistem CBC modunda simetrik blok şifreleme gizliliği ve HMAC için kimlik doğrulaması için Windows CNG tarafından sağlanan hizmetleri ile kullanmak üzere yapılandırılmış (bkz [özel Windows CNG algoritmaları belirtme](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) için Daha fazla ayrıntı).</span><span class="sxs-lookup"><span data-stu-id="5a703-131">If EncryptionType is CNG-CBC, the system is configured to use a CBC-mode symmetric block cipher for confidentiality and HMAC for authenticity with services provided by Windows CNG (see [Specifying custom Windows CNG algorithms](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) for more details).</span></span> <span data-ttu-id="5a703-132">Aşağıdaki ek değerler desteklenir, her biri CngCbcAuthenticatedEncryptionSettings türünde bir özelliğe karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5a703-132">The following additional values are supported, each of which corresponds to a property on the CngCbcAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="5a703-133">Değer</span><span class="sxs-lookup"><span data-stu-id="5a703-133">Value</span></span>                       | <span data-ttu-id="5a703-134">Tür</span><span class="sxs-lookup"><span data-stu-id="5a703-134">Type</span></span>   | <span data-ttu-id="5a703-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a703-135">Description</span></span> |
| --------------------------- | :----: | ----------- |
| <span data-ttu-id="5a703-136">EncryptionAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5a703-136">EncryptionAlgorithm</span></span>         | <span data-ttu-id="5a703-137">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-137">string</span></span> | <span data-ttu-id="5a703-138">CNG tarafından anlaşılan bir simetrik blok şifreleme algoritması adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-138">The name of a symmetric block cipher algorithm understood by CNG.</span></span> <span data-ttu-id="5a703-139">Bu algoritma CBC modunda açılır.</span><span class="sxs-lookup"><span data-stu-id="5a703-139">This algorithm is opened in CBC mode.</span></span> |
| <span data-ttu-id="5a703-140">EncryptionAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="5a703-140">EncryptionAlgorithmProvider</span></span> | <span data-ttu-id="5a703-141">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-141">string</span></span> | <span data-ttu-id="5a703-142">Algoritma EncryptionAlgorithm üretebilir CNG sağlayıcıyı uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-142">The name of the CNG provider implementation that can produce the algorithm EncryptionAlgorithm.</span></span> |
| <span data-ttu-id="5a703-143">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="5a703-143">EncryptionAlgorithmKeySize</span></span>  | <span data-ttu-id="5a703-144">DWORD</span><span class="sxs-lookup"><span data-stu-id="5a703-144">DWORD</span></span>  | <span data-ttu-id="5a703-145">Blok simetrik şifreleme algoritması türetmek için anahtar uzunluğu (bit cinsinden).</span><span class="sxs-lookup"><span data-stu-id="5a703-145">The length (in bits) of the key to derive for the symmetric block cipher algorithm.</span></span> |
| <span data-ttu-id="5a703-146">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5a703-146">HashAlgorithm</span></span>               | <span data-ttu-id="5a703-147">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-147">string</span></span> | <span data-ttu-id="5a703-148">CNG tarafından anlaşılan bir karma algoritması adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-148">The name of a hash algorithm understood by CNG.</span></span> <span data-ttu-id="5a703-149">Bu algoritma HMAC modunda açılır.</span><span class="sxs-lookup"><span data-stu-id="5a703-149">This algorithm is opened in HMAC mode.</span></span> |
| <span data-ttu-id="5a703-150">HashAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="5a703-150">HashAlgorithmProvider</span></span>       | <span data-ttu-id="5a703-151">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-151">string</span></span> | <span data-ttu-id="5a703-152">Algoritma HashAlgorithm üretebilir CNG sağlayıcıyı uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-152">The name of the CNG provider implementation that can produce the algorithm HashAlgorithm.</span></span> |

<span data-ttu-id="5a703-153">CNG GCM EncryptionType ise sistem Galois/sayacı modu simetrik blok şifreleme gizlilik ve kimlik doğrulama için Windows CNG tarafından sağlanan hizmetleri ile kullanmak üzere yapılandırılmış (bkz [özel Windows CNG algoritmaları belirtme](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) Daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="5a703-153">If EncryptionType is CNG-GCM, the system is configured to use a Galois/Counter Mode symmetric block cipher for confidentiality and authenticity with services provided by Windows CNG (see [Specifying custom Windows CNG algorithms](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) for more details).</span></span> <span data-ttu-id="5a703-154">Aşağıdaki ek değerler desteklenir, her biri CngGcmAuthenticatedEncryptionSettings türünde bir özelliğe karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5a703-154">The following additional values are supported, each of which corresponds to a property on the CngGcmAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="5a703-155">Değer</span><span class="sxs-lookup"><span data-stu-id="5a703-155">Value</span></span>                       | <span data-ttu-id="5a703-156">Tür</span><span class="sxs-lookup"><span data-stu-id="5a703-156">Type</span></span>   | <span data-ttu-id="5a703-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a703-157">Description</span></span> |
| --------------------------- | :----: | ----------- |
| <span data-ttu-id="5a703-158">EncryptionAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5a703-158">EncryptionAlgorithm</span></span>         | <span data-ttu-id="5a703-159">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-159">string</span></span> | <span data-ttu-id="5a703-160">CNG tarafından anlaşılan bir simetrik blok şifreleme algoritması adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-160">The name of a symmetric block cipher algorithm understood by CNG.</span></span> <span data-ttu-id="5a703-161">Bu algoritma Galois/sayacı modunda açılır.</span><span class="sxs-lookup"><span data-stu-id="5a703-161">This algorithm is opened in Galois/Counter Mode.</span></span> |
| <span data-ttu-id="5a703-162">EncryptionAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="5a703-162">EncryptionAlgorithmProvider</span></span> | <span data-ttu-id="5a703-163">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-163">string</span></span> | <span data-ttu-id="5a703-164">Algoritma EncryptionAlgorithm üretebilir CNG sağlayıcıyı uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-164">The name of the CNG provider implementation that can produce the algorithm EncryptionAlgorithm.</span></span> |
| <span data-ttu-id="5a703-165">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="5a703-165">EncryptionAlgorithmKeySize</span></span>  | <span data-ttu-id="5a703-166">DWORD</span><span class="sxs-lookup"><span data-stu-id="5a703-166">DWORD</span></span>  | <span data-ttu-id="5a703-167">Blok simetrik şifreleme algoritması türetmek için anahtar uzunluğu (bit cinsinden).</span><span class="sxs-lookup"><span data-stu-id="5a703-167">The length (in bits) of the key to derive for the symmetric block cipher algorithm.</span></span> |

<span data-ttu-id="5a703-168">EncryptionType yönetiliyorsa, sistemin bir yönetilen SymmetricAlgorithm gizliliği ve KeyedHashAlgorithm için kimlik doğrulaması için kullanmak üzere yapılandırılmış (bkz [belirtme özel yönetilen algoritmaları](xref:security/data-protection/configuration/overview#specifying-custom-managed-algorithms) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="5a703-168">If EncryptionType is Managed, the system is configured to use a managed SymmetricAlgorithm for confidentiality and KeyedHashAlgorithm for authenticity (see [Specifying custom managed algorithms](xref:security/data-protection/configuration/overview#specifying-custom-managed-algorithms) for more details).</span></span> <span data-ttu-id="5a703-169">Aşağıdaki ek değerler desteklenir, her biri ManagedAuthenticatedEncryptionSettings türünde bir özelliğe karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5a703-169">The following additional values are supported, each of which corresponds to a property on the ManagedAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="5a703-170">Değer</span><span class="sxs-lookup"><span data-stu-id="5a703-170">Value</span></span>                      | <span data-ttu-id="5a703-171">Tür</span><span class="sxs-lookup"><span data-stu-id="5a703-171">Type</span></span>   | <span data-ttu-id="5a703-172">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a703-172">Description</span></span> |
| -------------------------- | :----: | ----------- |
| <span data-ttu-id="5a703-173">EncryptionAlgorithmType</span><span class="sxs-lookup"><span data-stu-id="5a703-173">EncryptionAlgorithmType</span></span>    | <span data-ttu-id="5a703-174">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-174">string</span></span> | <span data-ttu-id="5a703-175">SymmetricAlgorithm uygulayan bir tür bütünleştirilmiş kodla nitelenen adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-175">The assembly-qualified name of a type that implements SymmetricAlgorithm.</span></span> |
| <span data-ttu-id="5a703-176">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="5a703-176">EncryptionAlgorithmKeySize</span></span> | <span data-ttu-id="5a703-177">DWORD</span><span class="sxs-lookup"><span data-stu-id="5a703-177">DWORD</span></span>  | <span data-ttu-id="5a703-178">Simetrik şifreleme algoritması için türetmek için anahtar uzunluğu (bit cinsinden).</span><span class="sxs-lookup"><span data-stu-id="5a703-178">The length (in bits) of the key to derive for the symmetric encryption algorithm.</span></span> |
| <span data-ttu-id="5a703-179">ValidationAlgorithmType</span><span class="sxs-lookup"><span data-stu-id="5a703-179">ValidationAlgorithmType</span></span>    | <span data-ttu-id="5a703-180">dize</span><span class="sxs-lookup"><span data-stu-id="5a703-180">string</span></span> | <span data-ttu-id="5a703-181">KeyedHashAlgorithm uygulayan bir tür bütünleştirilmiş kodla nitelenen adı.</span><span class="sxs-lookup"><span data-stu-id="5a703-181">The assembly-qualified name of a type that implements KeyedHashAlgorithm.</span></span> |

<span data-ttu-id="5a703-182">EncryptionType başka bir değer null dışında ya da boş varsa, veri koruma sisteminde başlatma sırasında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a703-182">If EncryptionType has any other value other than null or empty, the Data Protection system throws an exception at startup.</span></span>

> [!WARNING]
> <span data-ttu-id="5a703-183">Tür adları (EncryptionAlgorithmType, ValidationAlgorithmType, KeyEscrowSinks) içeren bir varsayılan ilke ayarını yapılandırırken türleri uygulamaya kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a703-183">When configuring a default policy setting that involves type names (EncryptionAlgorithmType, ValidationAlgorithmType, KeyEscrowSinks), the types must be available to the app.</span></span> <span data-ttu-id="5a703-184">Başka bir deyişle, Masaüstü CLR'sini üzerinde çalışan uygulamalar için bu türleri içeren derlemeler Genel Derleme Önbelleği'ne (GAC) mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a703-184">This means that for apps running on Desktop CLR, the assemblies that contain these types should be present in the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="5a703-185">.NET Core üzerinde çalışan ASP.NET Core uygulamaları için bu türleri içeren paketleri yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a703-185">For ASP.NET Core apps running on .NET Core, the packages that contain these types should be installed.</span></span>