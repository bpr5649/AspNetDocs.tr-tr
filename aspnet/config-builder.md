---
uid: config-builder
title: ASP.NET için yapılandırma oluşturucuları
author: rick-anderson
description: Dış kaynaklardaki web.config değerden farklı kaynaklardan yapılandırma verileri almayı öğrenin.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424794"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="5a976-103">ASP.NET için yapılandırma oluşturucuları</span><span class="sxs-lookup"><span data-stu-id="5a976-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="5a976-104">, [Stephen Moldova](https://github.com/StephenMolloy) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="5a976-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="5a976-105">Yapılandırma oluşturucuları, dış kaynaklardan yapılandırma değerlerini almak için ASP.NET uygulamalarına yönelik modern ve çevik bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="5a976-106">Yapılandırma oluşturucuları:</span><span class="sxs-lookup"><span data-stu-id="5a976-106">Configuration builders:</span></span>

* <span data-ttu-id="5a976-107">.NET Framework 4.7.1 ve üzeri sürümlerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="5a976-108">Yapılandırma değerlerini okumak için esnek bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="5a976-109">Bir kapsayıcıya ve bulut odaklı ortama geçiş yaparken uygulamaların temel ihtiyaçlarını ele alırlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="5a976-110">, .NET yapılandırma sisteminde daha önce kullanılamayan (örneğin, Azure Key Vault ve ortam değişkenleri) kaynaklardan çizerek yapılandırma verilerinin korunmasını geliştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="5a976-111">Anahtar/değer yapılandırma oluşturucuları</span><span class="sxs-lookup"><span data-stu-id="5a976-111">Key/value configuration builders</span></span>

<span data-ttu-id="5a976-112">Yapılandırma oluşturucuları tarafından işlenebilen yaygın bir senaryo, anahtar/değer düzenlerini izleyen yapılandırma bölümleri için temel bir anahtar/değer değiştirme mekanizması sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5a976-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="5a976-113">Configurationbuilder 'lar .NET Framework kavramı, belirli yapılandırma bölümleri veya desenlerle sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="5a976-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="5a976-114">Ancak, içindeki `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) yapılandırma oluşturucuların çoğu anahtar/değer düzeninde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a976-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="5a976-115">Anahtar/değer yapılandırma oluşturucuları ayarları</span><span class="sxs-lookup"><span data-stu-id="5a976-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="5a976-116">Aşağıdaki ayarlar, içindeki tüm anahtar/değer yapılandırma oluşturucuları için geçerlidir `Microsoft.Configuration.ConfigurationBuilders` .</span><span class="sxs-lookup"><span data-stu-id="5a976-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="5a976-117">Mod</span><span class="sxs-lookup"><span data-stu-id="5a976-117">Mode</span></span>

<span data-ttu-id="5a976-118">Yapılandırma oluşturucuları, yapılandırma sisteminin seçili anahtar/değer öğelerini doldurmak için anahtar/değer bilgilerinin dış kaynağını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5a976-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="5a976-119">Özellikle, `<appSettings/>` ve `<connectionStrings/>` bölümleri yapılandırma oluşturucularından özel bir işleme alır.</span><span class="sxs-lookup"><span data-stu-id="5a976-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="5a976-120">Oluşturucular üç modda çalışır:</span><span class="sxs-lookup"><span data-stu-id="5a976-120">The builders work in three modes:</span></span>

* <span data-ttu-id="5a976-121">`Strict`-Varsayılan mod.</span><span class="sxs-lookup"><span data-stu-id="5a976-121">`Strict` - The default mode.</span></span> <span data-ttu-id="5a976-122">Bu modda, yapılandırma Oluşturucusu yalnızca iyi bilinen anahtar/değer merkezli yapılandırma bölümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a976-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="5a976-123">`Strict`mod, bölümündeki her anahtarı numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="5a976-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="5a976-124">Dış kaynakta eşleşen bir anahtar bulunursa:</span><span class="sxs-lookup"><span data-stu-id="5a976-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="5a976-125">Yapılandırma oluşturucuları, elde edilen yapılandırma bölümündeki değeri dış kaynaktaki değerle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5a976-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="5a976-126">`Greedy`-Bu mod mod ile yakından ilgilidir `Strict` .</span><span class="sxs-lookup"><span data-stu-id="5a976-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="5a976-127">Özgün yapılandırmada zaten var olan anahtarlarla sınırlı olmamak yerine:</span><span class="sxs-lookup"><span data-stu-id="5a976-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="5a976-128">Yapılandırma oluşturucuları, dış kaynaktaki tüm anahtar/değer çiftlerini elde edilen yapılandırma bölümüne ekler.</span><span class="sxs-lookup"><span data-stu-id="5a976-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="5a976-129">`Expand`-Bir yapılandırma bölümü nesnesine ayrıştırıldıktan önce ham XML üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a976-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="5a976-130">Bir dizedeki belirteçleri genişletme olarak düşünülebilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="5a976-131">Ham XML dizesinin düzeniyle eşleşen herhangi bir bölümü, `${token}` belirteç genişletmesi için bir adaydır.</span><span class="sxs-lookup"><span data-stu-id="5a976-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="5a976-132">Dış kaynakta karşılık gelen bir değer bulunamazsa, belirteç değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="5a976-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="5a976-133">Bu moddaki oluşturucular `<appSettings/>` ve bölümleri ile sınırlı değildir `<connectionStrings/>` .</span><span class="sxs-lookup"><span data-stu-id="5a976-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="5a976-134">*web.config* ' den aşağıdaki biçimlendirme, [Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 'ı `Strict` modda sunar:</span><span class="sxs-lookup"><span data-stu-id="5a976-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="5a976-135">Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında ve gösterilen öğesini okur:</span><span class="sxs-lookup"><span data-stu-id="5a976-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="5a976-136">Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5a976-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="5a976-137">Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.</span><span class="sxs-lookup"><span data-stu-id="5a976-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="5a976-138">Ayarlanırsa, ortam değişkeninin değerleri.</span><span class="sxs-lookup"><span data-stu-id="5a976-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="5a976-139">Örneğin, şunları `ServiceID` içerir:</span><span class="sxs-lookup"><span data-stu-id="5a976-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="5a976-140">Ortam değişkeni ayarlanmamışsa, "web.config ServiceId değeri" `ServiceID` .</span><span class="sxs-lookup"><span data-stu-id="5a976-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="5a976-141">`ServiceID`Ayarlanırsa, ortam değişkeninin değeri.</span><span class="sxs-lookup"><span data-stu-id="5a976-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="5a976-142">Aşağıdaki görüntüde, `<appSettings/>` ortam düzenleyicisinde, önceki *web.config* Dosya kümesinden gelen anahtarlar/değerler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5a976-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![ortam Düzenleyicisi](config-builder/static/env.png)

<span data-ttu-id="5a976-144">Note: ortam değişkenlerindeki değişiklikleri görmek için çıkmanız ve Visual Studio 'Yu yeniden başlatmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="5a976-145">Önek işleme</span><span class="sxs-lookup"><span data-stu-id="5a976-145">Prefix handling</span></span>

<span data-ttu-id="5a976-146">Anahtar ön ekleri anahtarları ayarlamayı kolaylaştırabilir, çünkü:</span><span class="sxs-lookup"><span data-stu-id="5a976-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="5a976-147">.NET Framework yapılandırması karmaşıktır ve iç içe geçmiş.</span><span class="sxs-lookup"><span data-stu-id="5a976-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="5a976-148">Dış anahtar/değer kaynakları genellikle temel ve doğası gereği düz niteliktedir.</span><span class="sxs-lookup"><span data-stu-id="5a976-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="5a976-149">Örneğin, ortam değişkenleri iç içe değildir.</span><span class="sxs-lookup"><span data-stu-id="5a976-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="5a976-150">`<appSettings/>`Ortam değişkenleri aracılığıyla hem hem de yapılandırmaya eklemek için aşağıdaki yaklaşımlardan herhangi birini kullanın `<connectionStrings/>` :</span><span class="sxs-lookup"><span data-stu-id="5a976-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="5a976-151">İle `EnvironmentConfigBuilder` `Strict` yapılandırma dosyasında varsayılan modda ve uygun anahtar adlarıyla.</span><span class="sxs-lookup"><span data-stu-id="5a976-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="5a976-152">Yukarıdaki kod ve biçimlendirme bu yaklaşımı alır.</span><span class="sxs-lookup"><span data-stu-id="5a976-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="5a976-153">Bu yaklaşımı kullanarak hem hem de içinde **aynı şekilde adlandırılmış anahtarlara sahip olabilirsiniz** `<appSettings/>` `<connectionStrings/>` .</span><span class="sxs-lookup"><span data-stu-id="5a976-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="5a976-154">`EnvironmentConfigBuilder` `Greedy` Farklı ön ekler ve ile iki adet kullanın `stripPrefix` .</span><span class="sxs-lookup"><span data-stu-id="5a976-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="5a976-155">Bu yaklaşımda uygulama, `<appSettings/>` `<connectionStrings/>` yapılandırma dosyasını güncelleştirebilir ve güncelleştirmeye gerek kalmadan okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="5a976-156">Sonraki bölümde, [stripPrefix](#stripprefix), bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a976-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="5a976-157">`EnvironmentConfigBuilder` `Greedy` Farklı öneklerle iki s modunda kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a976-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="5a976-158">Bu yaklaşımda, anahtar adları ön eke göre farklılık gösterdiğinden yinelenen anahtar adlarına sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a976-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="5a976-159">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5a976-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="5a976-160">Yukarıdaki biçimlendirme ile, aynı düz anahtar/değer kaynağı iki farklı bölüm için yapılandırmayı doldurmak üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="5a976-161">Aşağıdaki görüntüde, `<appSettings/>` `<connectionStrings/>` ortam Düzenleyicisi 'ndeki önceki *web.config* Dosya kümesinden ve anahtarları/değerleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5a976-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![ortam Düzenleyicisi](config-builder/static/prefix.png)

<span data-ttu-id="5a976-163">Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında yer alan anahtarları/değerleri okur:</span><span class="sxs-lookup"><span data-stu-id="5a976-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="5a976-164">Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5a976-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="5a976-165">Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.</span><span class="sxs-lookup"><span data-stu-id="5a976-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="5a976-166">Ayarlanırsa, ortam değişkeninin değerleri.</span><span class="sxs-lookup"><span data-stu-id="5a976-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="5a976-167">Örneğin, önceki *web.config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="5a976-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="5a976-168">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5a976-168">Key</span></span>              | <span data-ttu-id="5a976-169">Değer</span><span class="sxs-lookup"><span data-stu-id="5a976-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="5a976-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="5a976-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="5a976-171">Env değişkenlerinden AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="5a976-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="5a976-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="5a976-172">AppSetting_default</span></span>            | <span data-ttu-id="5a976-173">Env 'dan değer AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="5a976-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="5a976-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="5a976-174">ConnStr_default</span></span>         | <span data-ttu-id="5a976-175">Env ConnStr_default Val</span><span class="sxs-lookup"><span data-stu-id="5a976-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="5a976-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="5a976-176">stripPrefix</span></span>

<span data-ttu-id="5a976-177">`stripPrefix`: Boolean, varsayılan olarak `false` .</span><span class="sxs-lookup"><span data-stu-id="5a976-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="5a976-178">Önceki XML biçimlendirmesi, uygulama ayarlarını bağlantı dizelerinden ayırır, ancak *web.config* dosyadaki tüm anahtarların belirtilen öneki kullanmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5a976-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="5a976-179">Örneğin, önek `AppSetting` `ServiceID` anahtara eklenmelidir ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="5a976-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="5a976-180">İle `stripPrefix` , ön ek *web.config* dosyasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="5a976-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="5a976-181">Ön ek, yapılandırma Oluşturucu kaynağında (örneğin, ortamında) gereklidir. Çoğu geliştiricilerin kullanacağı tahmin ederiz `stripPrefix` .</span><span class="sxs-lookup"><span data-stu-id="5a976-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="5a976-182">Uygulamalar genellikle ön eki devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="5a976-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="5a976-183">Aşağıdaki *web.config* ön eki şeritleri:</span><span class="sxs-lookup"><span data-stu-id="5a976-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="5a976-184">Yukarıdaki *web.config* dosyasında, anahtar hem hem de ' `default` de bulunur `<appSettings/>` `<connectionStrings/>` .</span><span class="sxs-lookup"><span data-stu-id="5a976-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="5a976-185">Aşağıdaki görüntüde, `<appSettings/>` `<connectionStrings/>` ortam Düzenleyicisi 'ndeki önceki *web.config* Dosya kümesinden ve anahtarları/değerleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5a976-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![ortam Düzenleyicisi](config-builder/static/prefix.png)

<span data-ttu-id="5a976-187">Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında yer alan anahtarları/değerleri okur:</span><span class="sxs-lookup"><span data-stu-id="5a976-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="5a976-188">Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5a976-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="5a976-189">Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.</span><span class="sxs-lookup"><span data-stu-id="5a976-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="5a976-190">Ayarlanırsa, ortam değişkeninin değerleri.</span><span class="sxs-lookup"><span data-stu-id="5a976-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="5a976-191">Örneğin, önceki *web.config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="5a976-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="5a976-192">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5a976-192">Key</span></span>              | <span data-ttu-id="5a976-193">Değer</span><span class="sxs-lookup"><span data-stu-id="5a976-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="5a976-194">ServiceId</span><span class="sxs-lookup"><span data-stu-id="5a976-194">ServiceID</span></span>           | <span data-ttu-id="5a976-195">Env değişkenlerinden AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="5a976-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="5a976-196">default</span><span class="sxs-lookup"><span data-stu-id="5a976-196">default</span></span>            | <span data-ttu-id="5a976-197">Env 'dan değer AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="5a976-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="5a976-198">default</span><span class="sxs-lookup"><span data-stu-id="5a976-198">default</span></span>         | <span data-ttu-id="5a976-199">Env ConnStr_default Val</span><span class="sxs-lookup"><span data-stu-id="5a976-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="5a976-200">Tokenmodel</span><span class="sxs-lookup"><span data-stu-id="5a976-200">tokenPattern</span></span>

<span data-ttu-id="5a976-201">`tokenPattern`: Dize, varsayılan olarak`@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="5a976-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="5a976-202">`Expand`Oluşturucuların davranışı, gibi görünen belirteçler için ham xml arar `${token}` .</span><span class="sxs-lookup"><span data-stu-id="5a976-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="5a976-203">Arama, varsayılan normal ifadeyle yapılır `@"\$\{(\w+)\}"` .</span><span class="sxs-lookup"><span data-stu-id="5a976-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="5a976-204">Eşleşen karakter kümesi `\w` XML 'den daha sıkı ve birçok yapılandırma kaynağına izin verir.</span><span class="sxs-lookup"><span data-stu-id="5a976-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="5a976-205">`tokenPattern`Belirteç adında gerekenden fazla karakter `@"\$\{(\w+)\}"` olması gerektiği zaman kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a976-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="5a976-206">`tokenPattern`Dizisinde</span><span class="sxs-lookup"><span data-stu-id="5a976-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="5a976-207">Geliştiricilerin belirteç eşleştirmesi için kullanılan Regex 'yi değiştirmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="5a976-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="5a976-208">İyi biçimlendirilmiş, tehlikeli olmayan bir Regex olduğundan emin olmak için doğrulama yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="5a976-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="5a976-209">Bir yakalama grubu içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a976-209">It must contain a capture group.</span></span> <span data-ttu-id="5a976-210">Tüm Regex tüm belirteçle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5a976-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="5a976-211">İlk yakalama, yapılandırma kaynağında aranacak belirteç adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="5a976-212">Microsoft.Configuration.ConfigUrationoluşturucular içindeki yapılandırma oluşturucular</span><span class="sxs-lookup"><span data-stu-id="5a976-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="5a976-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="5a976-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="5a976-214">[Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="5a976-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="5a976-215">Yapılandırma oluşturucuların en kolay olanıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="5a976-216">Ortamdan değerleri okur.</span><span class="sxs-lookup"><span data-stu-id="5a976-216">Reads values from the environment.</span></span>
* <span data-ttu-id="5a976-217">Ek yapılandırma seçeneklerine sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="5a976-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="5a976-218">`name`Öznitelik değeri rastgele.</span><span class="sxs-lookup"><span data-stu-id="5a976-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="5a976-219">**Note:** Bir Windows kapsayıcı ortamında, çalışma zamanında ayarlanan değişkenler yalnızca EntryPoint işlem ortamına eklenir.</span><span class="sxs-lookup"><span data-stu-id="5a976-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="5a976-220">Hizmet olarak çalışan uygulamalar veya giriş noktası olmayan bir işlem, kapsayıcıda bir mekanizmaya eklenmediği sürece bu değişkenleri kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="5a976-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="5a976-221">[IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.net](https://github.com/Microsoft/aspnet-docker)tabanlı kapsayıcılar için geçerli [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) sürümü bunu yalnızca *DefaultAppPool* içinde işler.</span><span class="sxs-lookup"><span data-stu-id="5a976-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="5a976-222">Diğer Windows tabanlı kapsayıcı türevleri, giriş noktası olmayan işlemlere yönelik kendi ekleme mekanizmalarının geliştirilmesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="5a976-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="5a976-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="5a976-224">Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin.</span><span class="sxs-lookup"><span data-stu-id="5a976-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="5a976-225">Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="5a976-226">Bu yapılandırma Oluşturucusu, [ASP.NET Core gizli bir yöneticiye](/aspnet/core/security/app-secrets)benzer bir özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="5a976-227">[Usersecretsconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) .NET Framework projelerinde kullanılabilir, ancak bir gizli dizi dosyası belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5a976-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="5a976-228">Alternatif olarak, `UserSecretsId` özelliği proje dosyasında tanımlayabilir ve ham gizli dizileri dosyayı okumak için doğru konumda oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a976-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="5a976-229">Dış bağımlılıkları projenizden tutmak için, gizli dosya XML olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="5a976-230">XML biçimlendirmesi bir uygulama ayrıntısının yanı sıra biçim üzerinde güvenilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="5a976-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="5a976-231">.NET Core projeleriyle dosya *secrets.js* paylaşmanız gerekiyorsa, [Simplejsonconfigbuilder](#simplejsonconfigbuilder)' ı kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="5a976-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="5a976-232">`SimpleJsonConfigBuilder`.NET Core biçimi de bir uygulama ayrıntısı konusunun değiştirilmesini de kabul etmelidir.</span><span class="sxs-lookup"><span data-stu-id="5a976-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="5a976-233">Yapılandırma öznitelikleri `UserSecretsConfigBuilder` :</span><span class="sxs-lookup"><span data-stu-id="5a976-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="5a976-234">`userSecretsId`-Bu, bir XML gizli dizi dosyasını tanımlamak için tercih edilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="5a976-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="5a976-235">`UserSecretsId`Bu tanımlayıcıyı depolamak için bir proje özelliği kullanan .NET Core ile benzerdir.</span><span class="sxs-lookup"><span data-stu-id="5a976-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="5a976-236">Dize benzersiz olmalıdır, GUID olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5a976-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="5a976-237">Bu öznitelikle, `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` Bu tanımlayıcıya ait bir gizli dizi dosyası için iyi bilinen bir yerel konuma () bakın.</span><span class="sxs-lookup"><span data-stu-id="5a976-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="5a976-238">`userSecretsFile`-Gizli dizileri içeren dosyayı belirten isteğe bağlı bir öznitelik.</span><span class="sxs-lookup"><span data-stu-id="5a976-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="5a976-239">`~`Karakter, uygulama köküne başvurmak için başlangıçta kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="5a976-240">Bu öznitelik ya da `userSecretsId` öznitelik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5a976-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="5a976-241">Her ikisi de belirtilirse, `userSecretsFile` öncelik alır.</span><span class="sxs-lookup"><span data-stu-id="5a976-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="5a976-242">`optional`: Boolean, varsayılan değer `true` -gizli dizi dosyası bulunamazsa özel durumu engeller.</span><span class="sxs-lookup"><span data-stu-id="5a976-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="5a976-243">`name`Öznitelik değeri rastgele.</span><span class="sxs-lookup"><span data-stu-id="5a976-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="5a976-244">Gizli dizileri dosyası aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="5a976-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="5a976-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="5a976-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="5a976-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) [Azure Key Vault](/azure/key-vault/key-vault-whatis)depolanan değerleri okur.</span><span class="sxs-lookup"><span data-stu-id="5a976-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="5a976-247">`vaultName`gereklidir (kasanın adı ya da kasadaki bir URI).</span><span class="sxs-lookup"><span data-stu-id="5a976-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="5a976-248">Diğer öznitelikler, hangi kasanın bağlanacağı konusunda denetime izin verir, ancak yalnızca uygulama ile birlikte çalışan bir ortamda çalışmıyorsa gereklidir `Microsoft.Azure.Services.AppAuthentication` .</span><span class="sxs-lookup"><span data-stu-id="5a976-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="5a976-249">Azure Hizmetleri kimlik doğrulama kitaplığı, mümkünse yürütme ortamından bağlantı bilgilerini otomatik olarak almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5a976-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="5a976-250">Bağlantı dizesi sağlayarak bağlantı bilgilerini otomatik olarak çekmeyi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a976-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="5a976-251">`vaultName`-Sağlanmazsa gereklidir `uri` .</span><span class="sxs-lookup"><span data-stu-id="5a976-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="5a976-252">Anahtar/değer çiftlerinin okunacağı Azure aboneliğinizdeki kasasının adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a976-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="5a976-253">`connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) tarafından kullanılabilen bir bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="5a976-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="5a976-254">`uri`-Belirtilen değere sahip diğer Key Vault sağlayıcılarına bağlanır `uri` .</span><span class="sxs-lookup"><span data-stu-id="5a976-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="5a976-255">Belirtilmemişse, Azure ( `vaultName` ) kasa sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="5a976-256">`version`-Azure Key Vault gizlilikler için bir sürüm oluşturma özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="5a976-257">`version`Belirtilmişse, Oluşturucu yalnızca bu sürümle eşleşen gizli dizileri alır.</span><span class="sxs-lookup"><span data-stu-id="5a976-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="5a976-258">`preloadSecretNames`-Bu Oluşturucu, varsayılan olarak, başlatıldığında anahtar kasasındaki **Tüm** anahtar adlarını sorgular.</span><span class="sxs-lookup"><span data-stu-id="5a976-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="5a976-259">Tüm anahtar değerlerini okumayı engellemek için, bu özniteliği olarak ayarlayın `false` .</span><span class="sxs-lookup"><span data-stu-id="5a976-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="5a976-260">Bunu tek seferde `false` gizli dizileri okur şekilde ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5a976-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="5a976-261">Tek seferde gizli dizileri okumak, kasa "liste" erişimini "Al" erişimine izin veriyorsa "bir yandan" erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="5a976-262">**Note:** Mode kullanılırken `Greedy` , `preloadSecretNames` `true` (varsayılan) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="5a976-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="5a976-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="5a976-264">[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) , dizin dosyalarını değer kaynağı olarak kullanan temel bir yapılandırma kurucudır.</span><span class="sxs-lookup"><span data-stu-id="5a976-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="5a976-265">Dosyanın adı anahtardır ve içerik değerdir.</span><span class="sxs-lookup"><span data-stu-id="5a976-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="5a976-266">Bu yapılandırma Oluşturucusu, genişletilmiş bir kapsayıcı ortamında çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="5a976-267">Docker Sısınma ve Kubernetes gibi sistemler `secrets` , bu dosya başına bu anahtarla düzenlenmiş Windows kapsayıcılarına de olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="5a976-268">Öznitelik ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="5a976-268">Attribute details:</span></span>

* <span data-ttu-id="5a976-269">`directoryPath`İstenir.</span><span class="sxs-lookup"><span data-stu-id="5a976-269">`directoryPath` - Required.</span></span> <span data-ttu-id="5a976-270">Değerlere bakmak için bir yol belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a976-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="5a976-271">Docker for Windows gizli dizileri *C:\programdata\docker\gizlilikler* dizininde varsayılan olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5a976-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="5a976-272">`ignorePrefix`-Bu önek ile başlayan dosyalar hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="5a976-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="5a976-273">Varsayılan olarak "Yoksay" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a976-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="5a976-274">`keyDelimiter`-Varsayılan değer `null` .</span><span class="sxs-lookup"><span data-stu-id="5a976-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="5a976-275">Belirtilmişse, yapılandırma Oluşturucusu dizinin birden çok düzeyine geçiş yaparken bu sınırlayıcıyla anahtar adları oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="5a976-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="5a976-276">Bu değer ise, `null` yapılandırma Oluşturucusu yalnızca dizinin en üst düzeyine bakar.</span><span class="sxs-lookup"><span data-stu-id="5a976-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="5a976-277">`optional`-Varsayılan değer `false` .</span><span class="sxs-lookup"><span data-stu-id="5a976-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="5a976-278">Kaynak dizin yoksa yapılandırma oluşturucusunun hatalara neden olup olmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a976-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="5a976-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="5a976-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="5a976-280">Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin.</span><span class="sxs-lookup"><span data-stu-id="5a976-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="5a976-281">Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="5a976-282">.NET Core projeleri genellikle yapılandırma için JSON dosyalarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5a976-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="5a976-283">[Simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) oluşturucusu, .NET Framework .NET Core JSON dosyalarının kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="5a976-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="5a976-284">Bu yapılandırma Oluşturucusu, düz bir anahtar/değer kaynağından .NET Framework yapılandırmanın belirli bir anahtar/değer alanına temel bir eşleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="5a976-285">Bu yapılandırma Oluşturucusu hiyerarşik **yapılandırmalar sağlamıyor.**</span><span class="sxs-lookup"><span data-stu-id="5a976-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="5a976-286">JSON yedekleme dosyası karmaşık hiyerarşik bir nesne değil, bir sözlüğe benzerdir.</span><span class="sxs-lookup"><span data-stu-id="5a976-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="5a976-287">Çok düzeyli hiyerarşik bir dosya kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="5a976-288">Bu sağlayıcı `flatten` , her düzeyde özellik adını sınırlayıcı olarak kullanarak ekleyerek derinliği `:` .</span><span class="sxs-lookup"><span data-stu-id="5a976-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="5a976-289">Öznitelik ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="5a976-289">Attribute details:</span></span>

* <span data-ttu-id="5a976-290">`jsonFile`İstenir.</span><span class="sxs-lookup"><span data-stu-id="5a976-290">`jsonFile` - Required.</span></span> <span data-ttu-id="5a976-291">Okunacak JSON dosyasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a976-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="5a976-292">`~`Karakter, uygulama köküne başvurmak için başlangıçta kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a976-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="5a976-293">`optional`-Boolean, varsayılan değer `true` .</span><span class="sxs-lookup"><span data-stu-id="5a976-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="5a976-294">JSON dosyası bulunamazsa özel durum üretilmesini önler.</span><span class="sxs-lookup"><span data-stu-id="5a976-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="5a976-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="5a976-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="5a976-296">`Flat` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="5a976-296">`Flat` is the default.</span></span> <span data-ttu-id="5a976-297">Ne zaman olduğunda `jsonMode` `Flat` , JSON dosyası tek bir düz anahtar/değer kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="5a976-298">`EnvironmentConfigBuilder` `AzureKeyVaultConfigBuilder` Ayrıca tek bir düz anahtar/değer kaynaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="5a976-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="5a976-299">, `SimpleJsonConfigBuilder` `Sectional` Modunda yapılandırıldığında:</span><span class="sxs-lookup"><span data-stu-id="5a976-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="5a976-300">JSON dosyası kavramsal olarak yalnızca en üst düzeyde birden fazla sözlüklere bölünmüştür.</span><span class="sxs-lookup"><span data-stu-id="5a976-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="5a976-301">Sözlüklerin her biri yalnızca, bunlara iliştirilmiş en üst düzey Özellik adıyla eşleşen yapılandırma bölümüne uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5a976-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="5a976-302">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5a976-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a><span data-ttu-id="5a976-303">Yapılandırma oluşturucuları sırası</span><span class="sxs-lookup"><span data-stu-id="5a976-303">Configuration builders order</span></span>

<span data-ttu-id="5a976-304">[ASPNET/Microsoftconfigurationbuilder](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub deposunda, bkz. [Configurationoluşturucular yürütme sırası](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) .</span><span class="sxs-lookup"><span data-stu-id="5a976-304">See [ConfigurationBuilders Order of Execution](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) in the [aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub repository.</span></span>

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="5a976-305">Özel anahtar/değer yapılandırma Oluşturucusu uygulama</span><span class="sxs-lookup"><span data-stu-id="5a976-305">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="5a976-306">Yapılandırma oluşturucular gereksinimlerinizi karşılamıyorsa, özel bir tane yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a976-306">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="5a976-307">`KeyValueConfigBuilder`Temel sınıf değiştirme modlarını ve çoğu önek kaygılarını işler.</span><span class="sxs-lookup"><span data-stu-id="5a976-307">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="5a976-308">Yalnızca uygulama gerektiren bir proje gereklidir:</span><span class="sxs-lookup"><span data-stu-id="5a976-308">An implementing project need only:</span></span>

* <span data-ttu-id="5a976-309">Temel sınıftan devralınır ve ile temel bir anahtar/değer çiftleri kaynağı uygulayın `GetValue` `GetAllValues` :</span><span class="sxs-lookup"><span data-stu-id="5a976-309">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="5a976-310">[Microsoft.Configuration.ConfigUrationoluşturucular. Base öğesini](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a976-310">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="5a976-311">`KeyValueConfigBuilder`Temel sınıf, anahtar/değer yapılandırma oluşturucuları arasında çalışmanın ve tutarlı davranışların çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a976-311">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a976-312">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5a976-312">Additional resources</span></span>

* [<span data-ttu-id="5a976-313">Yapılandırma oluşturucular GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="5a976-313">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="5a976-314">.NET kullanarak Azure Key Vault için hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5a976-314">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
