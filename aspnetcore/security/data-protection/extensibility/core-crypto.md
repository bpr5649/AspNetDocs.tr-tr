---
title: ASP.NET core'da çekirdek şifreleme genişletilebilirliği
author: rick-anderson
description: IAuthenticatedEncryptor, IAuthenticatedEncryptorDescriptor, IAuthenticatedEncryptorDescriptorDeserializer ve üst düzey factory hakkında bilgi edinin.
ms.author: riande
ms.date: 8/11/2017
uid: security/data-protection/extensibility/core-crypto
ms.openlocfilehash: 47432cfefe0a52c9f815d717f7269ec68fdb6af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069474"
---
# <a name="core-cryptography-extensibility-in-aspnet-core"></a><span data-ttu-id="9f6dc-103">ASP.NET core'da çekirdek şifreleme genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="9f6dc-103">Core cryptography extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-core-crypto"></a>

>[!WARNING]
> <span data-ttu-id="9f6dc-104">Aşağıdaki arabirimlerinden birini uygulayan türler, iş parçacığı açısından güvenli olmalıdır birden çok arayanlar için.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptor"></a>

## <a name="iauthenticatedencryptor"></a><span data-ttu-id="9f6dc-105">IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-105">IAuthenticatedEncryptor</span></span>

<span data-ttu-id="9f6dc-106">**IAuthenticatedEncryptor** şifreleme alt sistemi temel yapı bloğu arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-106">The **IAuthenticatedEncryptor** interface is the basic building block of the cryptographic subsystem.</span></span> <span data-ttu-id="9f6dc-107">Genellikle anahtar başına bir IAuthenticatedEncryptor yoktur ve tüm şifreleme anahtar malzemesi ve şifreleme işlemleri gerçekleştirmesi için gerekli olan algoritmik bilgileri IAuthenticatedEncryptor örneğine sarar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-107">There's generally one IAuthenticatedEncryptor per key, and the IAuthenticatedEncryptor instance wraps all cryptographic key material and algorithmic information necessary to perform cryptographic operations.</span></span>

<span data-ttu-id="9f6dc-108">Adından da anlaşılacağı gibi tür kimliği doğrulanmış şifreleme ve şifre çözme hizmetleri sağlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-108">As its name suggests, the type is responsible for providing authenticated encryption and decryption services.</span></span> <span data-ttu-id="9f6dc-109">Bunu, aşağıdaki iki API'lerini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-109">It exposes the following two APIs.</span></span>

* <span data-ttu-id="9f6dc-110">Şifre çözme (ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData): byte]</span><span class="sxs-lookup"><span data-stu-id="9f6dc-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

* <span data-ttu-id="9f6dc-111">Şifreleme (ArraySegment<byte> düz metin, ArraySegment<byte> additionalAuthenticatedData): byte]</span><span class="sxs-lookup"><span data-stu-id="9f6dc-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

<span data-ttu-id="9f6dc-112">Şifreleme yöntemi enciphered düz metin ve kimlik doğrulaması etiketi içeren bir blob döndürür.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-112">The Encrypt method returns a blob that includes the enciphered plaintext and an authentication tag.</span></span> <span data-ttu-id="9f6dc-113">AAD son yükten kurtarılabilir olması gerekmez ancak ek kimliği doğrulanmış veriler (AAD) kimlik doğrulaması etiketi kapsamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-113">The authentication tag must encompass the additional authenticated data (AAD), though the AAD itself need not be recoverable from the final payload.</span></span> <span data-ttu-id="9f6dc-114">Şifre çözme yöntemi, kimlik doğrulaması etiketi doğrular ve deciphered yükü döndürür.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-114">The Decrypt method validates the authentication tag and returns the deciphered payload.</span></span> <span data-ttu-id="9f6dc-115">Tüm hataları (ArgumentNullException dışında ve benzer) için CryptographicException homogenized.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-115">All failures (except ArgumentNullException and similar) should be homogenized to CryptographicException.</span></span>

> [!NOTE]
> <span data-ttu-id="9f6dc-116">IAuthenticatedEncryptor örneği gerçekten anahtar malzemesi içermesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-116">The IAuthenticatedEncryptor instance itself doesn't actually need to contain the key material.</span></span> <span data-ttu-id="9f6dc-117">Örneğin, uygulama tüm işlemler için HSM temsilci seçebilecek.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-117">For example, the implementation could delegate to an HSM for all operations.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptorfactory"></a>
<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="how-to-create-an-iauthenticatedencryptor"></a><span data-ttu-id="9f6dc-118">Bir IAuthenticatedEncryptor oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f6dc-118">How to create an IAuthenticatedEncryptor</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9f6dc-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9f6dc-120">**IAuthenticatedEncryptorFactory** arabirimi oluşturmak bildiği bir türü temsil eder bir [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) örneği.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-120">The **IAuthenticatedEncryptorFactory** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="9f6dc-121">Kendi API aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-121">Its API is as follows.</span></span>

* <span data-ttu-id="9f6dc-122">CreateEncryptorInstance (IKey anahtarı): IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-122">CreateEncryptorInstance(IKey key) : IAuthenticatedEncryptor</span></span>

<span data-ttu-id="9f6dc-123">Verilen tüm IKey örneği için kendi CreateEncryptorInstance yöntemi tarafından oluşturulan tüm kimliği doğrulanmış encryptors eşdeğer olarak düşünülmesi gereken aşağıdaki kod örneği.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-123">For any given IKey instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorFactory instance and an IKey instance
IAuthenticatedEncryptorFactory factory = ...;
IKey key = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = factory.CreateEncryptorInstance(key);
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = factory.CreateEncryptorInstance(key);
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9f6dc-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9f6dc-125">**IAuthenticatedEncryptorDescriptor** arabirimi oluşturmak bildiği bir türü temsil eder bir [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) örneği.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-125">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="9f6dc-126">Kendi API aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-126">Its API is as follows.</span></span>

* <span data-ttu-id="9f6dc-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span></span>

* <span data-ttu-id="9f6dc-128">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="9f6dc-128">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

<span data-ttu-id="9f6dc-129">IAuthenticatedEncryptor gibi belirli bir anahtarı sarmalama IAuthenticatedEncryptorDescriptor örneğini varsayılır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-129">Like IAuthenticatedEncryptor, an instance of IAuthenticatedEncryptorDescriptor is assumed to wrap one specific key.</span></span> <span data-ttu-id="9f6dc-130">Bu tüm verilen IAuthenticatedEncryptorDescriptor örneği için kendi CreateEncryptorInstance yöntemi tarafından oluşturulan tüm kimliği doğrulanmış encryptors eşdeğer olarak değerlendirilmesi gerektiğini anlamına gelir. aşağıdaki kod örneği.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-130">This means that for any given IAuthenticatedEncryptorDescriptor instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorDescriptor instance
IAuthenticatedEncryptorDescriptor descriptor = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = descriptor.CreateEncryptorInstance();
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = descriptor.CreateEncryptorInstance();
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

---

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="iauthenticatedencryptordescriptor-aspnet-core-2x-only"></a><span data-ttu-id="9f6dc-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x yalnızca)</span><span class="sxs-lookup"><span data-stu-id="9f6dc-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x only)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9f6dc-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9f6dc-133">**IAuthenticatedEncryptorDescriptor** arabirimi kendisini XML biçimine dışa bildiği bir türü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-133">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to export itself to XML.</span></span> <span data-ttu-id="9f6dc-134">Kendi API aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-134">Its API is as follows.</span></span>

* <span data-ttu-id="9f6dc-135">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="9f6dc-135">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9f6dc-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

---

## <a name="xml-serialization"></a><span data-ttu-id="9f6dc-137">XML seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="9f6dc-137">XML Serialization</span></span>

<span data-ttu-id="9f6dc-138">IAuthenticatedEncryptor IAuthenticatedEncryptorDescriptor arasındaki birincil fark tanımlayıcı Şifreleyici oluşturma ve geçerli bağımsız değişkenlerle tedarik bilir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-138">The primary difference between IAuthenticatedEncryptor and IAuthenticatedEncryptorDescriptor is that the descriptor knows how to create the encryptor and supply it with valid arguments.</span></span> <span data-ttu-id="9f6dc-139">Uygulaması SymmetricAlgorithm ve KeyedHashAlgorithm kullanır bir IAuthenticatedEncryptor göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-139">Consider an IAuthenticatedEncryptor whose implementation relies on SymmetricAlgorithm and KeyedHashAlgorithm.</span></span> <span data-ttu-id="9f6dc-140">Bu tür tüketmeye Şifreleyici'nın iş, ancak uygulama yeniden başlatılırsa kendisi yeniden oluşturmak nasıl uygun açıklamasını gerçekten yazamaz şekilde, mutlaka, bu tür bir nereden geldiğini bilmez.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-140">The encryptor's job is to consume these types, but it doesn't necessarily know where these types came from, so it can't really write out a proper description of how to recreate itself if the application restarts.</span></span> <span data-ttu-id="9f6dc-141">Tanımlayıcı, bu üzerinde daha yüksek bir düzeye olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-141">The descriptor acts as a higher level on top of this.</span></span> <span data-ttu-id="9f6dc-142">Tanımlayıcı Şifreleyici örneği oluşturmak nasıl bilir olduğundan (örneğin, gerekli algoritmalar oluşturma Giden), böylece uygulama sıfırladıktan sonra Şifreleyici örneği yeniden oluşturulabilir, Bilgi Bankası XML formundaki serileştirebiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-142">Since the descriptor knows how to create the encryptor instance (e.g., it knows how to create the required algorithms), it can serialize that knowledge in XML form so that the encryptor instance can be recreated after an application reset.</span></span>

<a name="data-protection-extensibility-core-crypto-exporttoxml"></a>

<span data-ttu-id="9f6dc-143">Tanımlayıcı, ExportToXml yordamı seri hale getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-143">The descriptor can be serialized via its ExportToXml routine.</span></span> <span data-ttu-id="9f6dc-144">Bu yordam, iki özellik içeren bir XmlSerializedDescriptorInfo döndürür: tanımlayıcı ve temsil eden tür XElement temsili bir [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) olabilir. karşılık gelen XElement verilen bu tanımlayıcıyı resurrect için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-144">This routine returns an XmlSerializedDescriptorInfo which contains two properties: the XElement representation of the descriptor and the Type which represents an [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) which can be used to resurrect this descriptor given the corresponding XElement.</span></span>

<span data-ttu-id="9f6dc-145">Seri hale getirilmiş tanımlayıcı şifreleme anahtar malzemesi gibi hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-145">The serialized descriptor may contain sensitive information such as cryptographic key material.</span></span> <span data-ttu-id="9f6dc-146">Veri koruma sisteminde kalıcı depolama için önce bilgi şifreleme için yerleşik destek sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-146">The data protection system has built-in support for encrypting information before it's persisted to storage.</span></span> <span data-ttu-id="9f6dc-147">Bu yararlanmak için tanımlayıcı öznitelik adı "boşluğu requiresEncryption" ile hassas bilgiler içeren öğe işaretlemeniz gerekir (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), değeri "true".</span><span class="sxs-lookup"><span data-stu-id="9f6dc-147">To take advantage of this, the descriptor should mark the element which contains sensitive information with the attribute name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), value "true".</span></span>

>[!TIP]
> <span data-ttu-id="9f6dc-148">Bu öznitelik ayarlamak için bir yardımcı API yoktur.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-148">There's a helper API for setting this attribute.</span></span> <span data-ttu-id="9f6dc-149">XElement.MarkAsRequiresEncryption() Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel ad alanında bulunan uzantı yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-149">Call the extension method XElement.MarkAsRequiresEncryption() located in namespace Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span></span>

<span data-ttu-id="9f6dc-150">Servis taleplerini seri hale getirilmiş tanımlayıcı hassas bilgileri burada içermiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-150">There can also be cases where the serialized descriptor doesn't contain sensitive information.</span></span> <span data-ttu-id="9f6dc-151">Tekrar bir şifreleme anahtarının bir HSM'de depolanan bir durum düşünün.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-151">Consider again the case of a cryptographic key stored in an HSM.</span></span> <span data-ttu-id="9f6dc-152">Tanımlayıcı, HSM malzeme düz metin biçiminde göstermek olmaz bu yana kendisine serileştirilirken anahtar malzemesi yazılamıyor.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-152">The descriptor cannot write out the key material when serializing itself since the HSM won't expose the material in plaintext form.</span></span> <span data-ttu-id="9f6dc-153">Bunun yerine, tanımlayıcı (HSM bu biçimde dışa aktarma izin verirse), anahtar veya anahtar HSM'ın kendi benzersiz tanımlayıcısını anahtar sarmalanmış sürümünü kullanıma yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-153">Instead, the descriptor might write out the key-wrapped version of the key (if the HSM allows export in this fashion) or the HSM's own unique identifier for the key.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer"></a>

## <a name="iauthenticatedencryptordescriptordeserializer"></a><span data-ttu-id="9f6dc-154">IAuthenticatedEncryptorDescriptorDeserializer</span><span class="sxs-lookup"><span data-stu-id="9f6dc-154">IAuthenticatedEncryptorDescriptorDeserializer</span></span>

<span data-ttu-id="9f6dc-155">**IAuthenticatedEncryptorDescriptorDeserializer** arabirimi bir XElement IAuthenticatedEncryptorDescriptor örneğinden seri durumdan çıkarılacak bildiği bir türü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-155">The **IAuthenticatedEncryptorDescriptorDeserializer** interface represents a type that knows how to deserialize an IAuthenticatedEncryptorDescriptor instance from an XElement.</span></span> <span data-ttu-id="9f6dc-156">Bu, tek bir yöntemi gösterir:</span><span class="sxs-lookup"><span data-stu-id="9f6dc-156">It exposes a single method:</span></span>

* <span data-ttu-id="9f6dc-157">ImportFromXml (XElement öğesi): IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-157">ImportFromXml(XElement element) : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="9f6dc-158">ImportFromXml yöntem tarafından döndürülen XElement alır [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) ve özgün IAuthenticatedEncryptorDescriptor eşdeğer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-158">The ImportFromXml method takes the XElement that was returned by [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) and creates an equivalent of the original IAuthenticatedEncryptorDescriptor.</span></span>

<span data-ttu-id="9f6dc-159">IAuthenticatedEncryptorDescriptorDeserializer uygulayan türleri, aşağıdaki iki genel oluşturucular biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="9f6dc-159">Types which implement IAuthenticatedEncryptorDescriptorDeserializer should have one of the following two public constructors:</span></span>

* <span data-ttu-id="9f6dc-160">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="9f6dc-160">.ctor(IServiceProvider)</span></span>

* <span data-ttu-id="9f6dc-161">.ctor()</span><span class="sxs-lookup"><span data-stu-id="9f6dc-161">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="9f6dc-162">Oluşturucuya geçirilen IServiceProvider null olabilir.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-162">The IServiceProvider passed to the constructor may be null.</span></span>

## <a name="the-top-level-factory"></a><span data-ttu-id="9f6dc-163">Üst düzey Fabrika</span><span class="sxs-lookup"><span data-stu-id="9f6dc-163">The top-level factory</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9f6dc-164">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-164">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9f6dc-165">**AlgorithmConfiguration** sınıfı oluşturmak bildiği bir türü temsil eder [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) örnekleri.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-165">The **AlgorithmConfiguration** class represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="9f6dc-166">Bu, tek bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-166">It exposes a single API.</span></span>

* <span data-ttu-id="9f6dc-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="9f6dc-168">Üst düzey Fabrika olarak AlgorithmConfiguration düşünün.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-168">Think of AlgorithmConfiguration as the top-level factory.</span></span> <span data-ttu-id="9f6dc-169">Yapılandırma şablon olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-169">The configuration serves as a template.</span></span> <span data-ttu-id="9f6dc-170">Algoritmik bilgi sarmalar (örneğin, bu yapılandırma bir AES-128-GCM ana anahtar ile tanımlayıcıları üretir), ancak henüz belirli bir anahtar ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-170">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="9f6dc-171">CreateNewDescriptor çağrılır, yeni anahtar malzemesi bu çağrı için yalnızca oluşturulduğunda ve yeni IAuthenticatedEncryptorDescriptor üretilir, bu anahtar malzemesi ve malzeme kullanmak için gereken bilgilerin algoritmik sarmalar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-171">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="9f6dc-172">Anahtar malzemesi yazılımda oluşturulabilir (ve bellekte tutulan), bunu oluşturulabilir ve bir HSM ve benzeri tutulan.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-172">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="9f6dc-173">İki çağrıları CreateNewDescriptor eşdeğer IAuthenticatedEncryptorDescriptor örnekleri hiçbir zaman oluşturmalısınız önemli noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-173">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="9f6dc-174">Gibi AlgorithmConfiguration türü anahtarı oluşturma rutinleri için giriş noktası olarak hizmet [çalışırken otomatik anahtar](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span><span class="sxs-lookup"><span data-stu-id="9f6dc-174">The AlgorithmConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="9f6dc-175">Gelecekteki tüm anahtarların uygulamasını değiştirmek için KeyManagementOptions AuthenticatedEncryptorConfiguration özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-175">To change the implementation for all future keys, set the AuthenticatedEncryptorConfiguration property in KeyManagementOptions.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9f6dc-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9f6dc-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9f6dc-177">**IAuthenticatedEncryptorConfiguration** arabirimi oluşturmak bildiği bir türü temsil eder [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) örnekleri.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-177">The **IAuthenticatedEncryptorConfiguration** interface represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="9f6dc-178">Bu, tek bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-178">It exposes a single API.</span></span>

* <span data-ttu-id="9f6dc-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="9f6dc-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="9f6dc-180">Üst düzey Fabrika olarak IAuthenticatedEncryptorConfiguration düşünün.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-180">Think of IAuthenticatedEncryptorConfiguration as the top-level factory.</span></span> <span data-ttu-id="9f6dc-181">Yapılandırma şablon olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-181">The configuration serves as a template.</span></span> <span data-ttu-id="9f6dc-182">Algoritmik bilgi sarmalar (örneğin, bu yapılandırma bir AES-128-GCM ana anahtar ile tanımlayıcıları üretir), ancak henüz belirli bir anahtar ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-182">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="9f6dc-183">CreateNewDescriptor çağrılır, yeni anahtar malzemesi bu çağrı için yalnızca oluşturulduğunda ve yeni IAuthenticatedEncryptorDescriptor üretilir, bu anahtar malzemesi ve malzeme kullanmak için gereken bilgilerin algoritmik sarmalar.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-183">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="9f6dc-184">Anahtar malzemesi yazılımda oluşturulabilir (ve bellekte tutulan), bunu oluşturulabilir ve bir HSM ve benzeri tutulan.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-184">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="9f6dc-185">İki çağrıları CreateNewDescriptor eşdeğer IAuthenticatedEncryptorDescriptor örnekleri hiçbir zaman oluşturmalısınız önemli noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-185">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="9f6dc-186">Gibi IAuthenticatedEncryptorConfiguration türü anahtarı oluşturma rutinleri için giriş noktası olarak hizmet [çalışırken otomatik anahtar](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span><span class="sxs-lookup"><span data-stu-id="9f6dc-186">The IAuthenticatedEncryptorConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="9f6dc-187">Gelecekteki tüm anahtarların uygulamasını değiştirmek için hizmet kapsayıcısında IAuthenticatedEncryptorConfiguration tek kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9f6dc-187">To change the implementation for all future keys, register a singleton IAuthenticatedEncryptorConfiguration in the service container.</span></span>

---
