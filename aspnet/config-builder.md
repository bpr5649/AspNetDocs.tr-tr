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
# <a name="configuration-builders-for-aspnet"></a>ASP.NET için yapılandırma oluşturucuları

, [Stephen Moldova](https://github.com/StephenMolloy) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Yapılandırma oluşturucuları, dış kaynaklardan yapılandırma değerlerini almak için ASP.NET uygulamalarına yönelik modern ve çevik bir mekanizma sağlar.

Yapılandırma oluşturucuları:

* .NET Framework 4.7.1 ve üzeri sürümlerde kullanılabilir.
* Yapılandırma değerlerini okumak için esnek bir mekanizma sağlar.
* Bir kapsayıcıya ve bulut odaklı ortama geçiş yaparken uygulamaların temel ihtiyaçlarını ele alırlar.
* , .NET yapılandırma sisteminde daha önce kullanılamayan (örneğin, Azure Key Vault ve ortam değişkenleri) kaynaklardan çizerek yapılandırma verilerinin korunmasını geliştirmek için kullanılabilir.

## <a name="keyvalue-configuration-builders"></a>Anahtar/değer yapılandırma oluşturucuları

Yapılandırma oluşturucuları tarafından işlenebilen yaygın bir senaryo, anahtar/değer düzenlerini izleyen yapılandırma bölümleri için temel bir anahtar/değer değiştirme mekanizması sağlamaktır. Configurationbuilder 'lar .NET Framework kavramı, belirli yapılandırma bölümleri veya desenlerle sınırlı değildir. Ancak, içindeki `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) yapılandırma oluşturucuların çoğu anahtar/değer düzeninde çalışır.

## <a name="keyvalue-configuration-builders-settings"></a>Anahtar/değer yapılandırma oluşturucuları ayarları

Aşağıdaki ayarlar, içindeki tüm anahtar/değer yapılandırma oluşturucuları için geçerlidir `Microsoft.Configuration.ConfigurationBuilders` .

### <a name="mode"></a>Mod

Yapılandırma oluşturucuları, yapılandırma sisteminin seçili anahtar/değer öğelerini doldurmak için anahtar/değer bilgilerinin dış kaynağını kullanır. Özellikle, `<appSettings/>` ve `<connectionStrings/>` bölümleri yapılandırma oluşturucularından özel bir işleme alır. Oluşturucular üç modda çalışır:

* `Strict`-Varsayılan mod. Bu modda, yapılandırma Oluşturucusu yalnızca iyi bilinen anahtar/değer merkezli yapılandırma bölümlerinde çalışır. `Strict`mod, bölümündeki her anahtarı numaralandırır. Dış kaynakta eşleşen bir anahtar bulunursa:

   * Yapılandırma oluşturucuları, elde edilen yapılandırma bölümündeki değeri dış kaynaktaki değerle değiştirir.
* `Greedy`-Bu mod mod ile yakından ilgilidir `Strict` . Özgün yapılandırmada zaten var olan anahtarlarla sınırlı olmamak yerine:

  * Yapılandırma oluşturucuları, dış kaynaktaki tüm anahtar/değer çiftlerini elde edilen yapılandırma bölümüne ekler.

* `Expand`-Bir yapılandırma bölümü nesnesine ayrıştırıldıktan önce ham XML üzerinde çalışır. Bir dizedeki belirteçleri genişletme olarak düşünülebilir. Ham XML dizesinin düzeniyle eşleşen herhangi bir bölümü, `${token}` belirteç genişletmesi için bir adaydır. Dış kaynakta karşılık gelen bir değer bulunamazsa, belirteç değiştirilmez. Bu moddaki oluşturucular `<appSettings/>` ve bölümleri ile sınırlı değildir `<connectionStrings/>` .

*web.config* ' den aşağıdaki biçimlendirme, [Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 'ı `Strict` modda sunar:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında ve gösterilen öğesini okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, şunları `ServiceID` içerir:

* Ortam değişkeni ayarlanmamışsa, "web.config ServiceId değeri" `ServiceID` .
* `ServiceID`Ayarlanırsa, ortam değişkeninin değeri.

Aşağıdaki görüntüde, `<appSettings/>` ortam düzenleyicisinde, önceki *web.config* Dosya kümesinden gelen anahtarlar/değerler gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/env.png)

Note: ortam değişkenlerindeki değişiklikleri görmek için çıkmanız ve Visual Studio 'Yu yeniden başlatmanız gerekebilir.

### <a name="prefix-handling"></a>Önek işleme

Anahtar ön ekleri anahtarları ayarlamayı kolaylaştırabilir, çünkü:

* .NET Framework yapılandırması karmaşıktır ve iç içe geçmiş.
* Dış anahtar/değer kaynakları genellikle temel ve doğası gereği düz niteliktedir. Örneğin, ortam değişkenleri iç içe değildir.

`<appSettings/>`Ortam değişkenleri aracılığıyla hem hem de yapılandırmaya eklemek için aşağıdaki yaklaşımlardan herhangi birini kullanın `<connectionStrings/>` :

* İle `EnvironmentConfigBuilder` `Strict` yapılandırma dosyasında varsayılan modda ve uygun anahtar adlarıyla. Yukarıdaki kod ve biçimlendirme bu yaklaşımı alır. Bu yaklaşımı kullanarak hem hem de içinde **aynı şekilde adlandırılmış anahtarlara sahip olabilirsiniz** `<appSettings/>` `<connectionStrings/>` .
* `EnvironmentConfigBuilder` `Greedy` Farklı ön ekler ve ile iki adet kullanın `stripPrefix` . Bu yaklaşımda uygulama, `<appSettings/>` `<connectionStrings/>` yapılandırma dosyasını güncelleştirebilir ve güncelleştirmeye gerek kalmadan okuyabilir. Sonraki bölümde, [stripPrefix](#stripprefix), bunun nasıl yapılacağını gösterir.
* `EnvironmentConfigBuilder` `Greedy` Farklı öneklerle iki s modunda kullanın. Bu yaklaşımda, anahtar adları ön eke göre farklılık gösterdiğinden yinelenen anahtar adlarına sahip olabilirsiniz.  Örneğin:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

Yukarıdaki biçimlendirme ile, aynı düz anahtar/değer kaynağı iki farklı bölüm için yapılandırmayı doldurmak üzere kullanılabilir.

Aşağıdaki görüntüde, `<appSettings/>` `<connectionStrings/>` ortam Düzenleyicisi 'ndeki önceki *web.config* Dosya kümesinden ve anahtarları/değerleri gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/prefix.png)

Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında yer alan anahtarları/değerleri okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, önceki *web.config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:

|  Anahtar              | Değer |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | Env değişkenlerinden AppSetting_ServiceID|
|    AppSetting_default            | Env 'dan değer AppSetting_default |
|       ConnStr_default         | Env ConnStr_default Val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`: Boolean, varsayılan olarak `false` . 

Önceki XML biçimlendirmesi, uygulama ayarlarını bağlantı dizelerinden ayırır, ancak *web.config* dosyadaki tüm anahtarların belirtilen öneki kullanmasını gerektirir. Örneğin, önek `AppSetting` `ServiceID` anahtara eklenmelidir ("AppSetting_ServiceID"). İle `stripPrefix` , ön ek *web.config* dosyasında kullanılmaz. Ön ek, yapılandırma Oluşturucu kaynağında (örneğin, ortamında) gereklidir. Çoğu geliştiricilerin kullanacağı tahmin ederiz `stripPrefix` .

Uygulamalar genellikle ön eki devre dışı bırakır. Aşağıdaki *web.config* ön eki şeritleri:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

Yukarıdaki *web.config* dosyasında, anahtar hem hem de ' `default` de bulunur `<appSettings/>` `<connectionStrings/>` .

Aşağıdaki görüntüde, `<appSettings/>` `<connectionStrings/>` ortam Düzenleyicisi 'ndeki önceki *web.config* Dosya kümesinden ve anahtarları/değerleri gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/prefix.png)

Aşağıdaki kod, `<appSettings/>` `<connectionStrings/>` önceki *web.config* dosyasında yer alan anahtarları/değerleri okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *web.config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, önceki *web.config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:

|  Anahtar              | Değer |
| ----------------- | ------------ |
|     ServiceId           | Env değişkenlerinden AppSetting_ServiceID|
|    default            | Env 'dan değer AppSetting_default |
|    default         | Env ConnStr_default Val|

### <a name="tokenpattern"></a>Tokenmodel

`tokenPattern`: Dize, varsayılan olarak`@"\$\{(\w+)\}"`

`Expand`Oluşturucuların davranışı, gibi görünen belirteçler için ham xml arar `${token}` . Arama, varsayılan normal ifadeyle yapılır `@"\$\{(\w+)\}"` . Eşleşen karakter kümesi `\w` XML 'den daha sıkı ve birçok yapılandırma kaynağına izin verir. `tokenPattern`Belirteç adında gerekenden fazla karakter `@"\$\{(\w+)\}"` olması gerektiği zaman kullanın.

`tokenPattern`Dizisinde

* Geliştiricilerin belirteç eşleştirmesi için kullanılan Regex 'yi değiştirmesine izin verir.
* İyi biçimlendirilmiş, tehlikeli olmayan bir Regex olduğundan emin olmak için doğrulama yapılmaz.
* Bir yakalama grubu içermesi gerekir. Tüm Regex tüm belirteçle eşleşmelidir. İlk yakalama, yapılandırma kaynağında aranacak belirteç adı olmalıdır.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft.Configuration.ConfigUrationoluşturucular içindeki yapılandırma oluşturucular

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* Yapılandırma oluşturucuların en kolay olanıdır.
* Ortamdan değerleri okur.
* Ek yapılandırma seçeneklerine sahip değildir.
* `name`Öznitelik değeri rastgele.

**Note:** Bir Windows kapsayıcı ortamında, çalışma zamanında ayarlanan değişkenler yalnızca EntryPoint işlem ortamına eklenir. Hizmet olarak çalışan uygulamalar veya giriş noktası olmayan bir işlem, kapsayıcıda bir mekanizmaya eklenmediği sürece bu değişkenleri kullanmaz. [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.net](https://github.com/Microsoft/aspnet-docker)tabanlı kapsayıcılar için geçerli [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) sürümü bunu yalnızca *DefaultAppPool* içinde işler. Diğer Windows tabanlı kapsayıcı türevleri, giriş noktası olmayan işlemlere yönelik kendi ekleme mekanizmalarının geliştirilmesi gerekebilir.

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin. Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

Bu yapılandırma Oluşturucusu, [ASP.NET Core gizli bir yöneticiye](/aspnet/core/security/app-secrets)benzer bir özellik sağlar.

[Usersecretsconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) .NET Framework projelerinde kullanılabilir, ancak bir gizli dizi dosyası belirtilmelidir. Alternatif olarak, `UserSecretsId` özelliği proje dosyasında tanımlayabilir ve ham gizli dizileri dosyayı okumak için doğru konumda oluşturabilirsiniz. Dış bağımlılıkları projenizden tutmak için, gizli dosya XML olarak biçimlendirilir. XML biçimlendirmesi bir uygulama ayrıntısının yanı sıra biçim üzerinde güvenilmemelidir. .NET Core projeleriyle dosya *secrets.js* paylaşmanız gerekiyorsa, [Simplejsonconfigbuilder](#simplejsonconfigbuilder)' ı kullanmayı düşünün. `SimpleJsonConfigBuilder`.NET Core biçimi de bir uygulama ayrıntısı konusunun değiştirilmesini de kabul etmelidir.

Yapılandırma öznitelikleri `UserSecretsConfigBuilder` :

* `userSecretsId`-Bu, bir XML gizli dizi dosyasını tanımlamak için tercih edilen yöntemdir. `UserSecretsId`Bu tanımlayıcıyı depolamak için bir proje özelliği kullanan .NET Core ile benzerdir. Dize benzersiz olmalıdır, GUID olması gerekmez. Bu öznitelikle, `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` Bu tanımlayıcıya ait bir gizli dizi dosyası için iyi bilinen bir yerel konuma () bakın.
* `userSecretsFile`-Gizli dizileri içeren dosyayı belirten isteğe bağlı bir öznitelik. `~`Karakter, uygulama köküne başvurmak için başlangıçta kullanılabilir. Bu öznitelik ya da `userSecretsId` öznitelik gereklidir. Her ikisi de belirtilirse, `userSecretsFile` öncelik alır.
* `optional`: Boolean, varsayılan değer `true` -gizli dizi dosyası bulunamazsa özel durumu engeller. 
* `name`Öznitelik değeri rastgele.

Gizli dizileri dosyası aşağıdaki biçimdedir:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

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

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) [Azure Key Vault](/azure/key-vault/key-vault-whatis)depolanan değerleri okur.

`vaultName`gereklidir (kasanın adı ya da kasadaki bir URI). Diğer öznitelikler, hangi kasanın bağlanacağı konusunda denetime izin verir, ancak yalnızca uygulama ile birlikte çalışan bir ortamda çalışmıyorsa gereklidir `Microsoft.Azure.Services.AppAuthentication` . Azure Hizmetleri kimlik doğrulama kitaplığı, mümkünse yürütme ortamından bağlantı bilgilerini otomatik olarak almak için kullanılır. Bağlantı dizesi sağlayarak bağlantı bilgilerini otomatik olarak çekmeyi geçersiz kılabilirsiniz.

* `vaultName`-Sağlanmazsa gereklidir `uri` . Anahtar/değer çiftlerinin okunacağı Azure aboneliğinizdeki kasasının adını belirtir.
* `connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) tarafından kullanılabilen bir bağlantı dizesi
* `uri`-Belirtilen değere sahip diğer Key Vault sağlayıcılarına bağlanır `uri` . Belirtilmemişse, Azure ( `vaultName` ) kasa sağlayıcıdır.
* `version`-Azure Key Vault gizlilikler için bir sürüm oluşturma özelliği sağlar. `version`Belirtilmişse, Oluşturucu yalnızca bu sürümle eşleşen gizli dizileri alır.
* `preloadSecretNames`-Bu Oluşturucu, varsayılan olarak, başlatıldığında anahtar kasasındaki **Tüm** anahtar adlarını sorgular. Tüm anahtar değerlerini okumayı engellemek için, bu özniteliği olarak ayarlayın `false` . Bunu tek seferde `false` gizli dizileri okur şekilde ayarlama. Tek seferde gizli dizileri okumak, kasa "liste" erişimini "Al" erişimine izin veriyorsa "bir yandan" erişim sağlar. **Note:** Mode kullanılırken `Greedy` , `preloadSecretNames` `true` (varsayılan) olmalıdır.

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

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

[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) , dizin dosyalarını değer kaynağı olarak kullanan temel bir yapılandırma kurucudır. Dosyanın adı anahtardır ve içerik değerdir. Bu yapılandırma Oluşturucusu, genişletilmiş bir kapsayıcı ortamında çalışırken yararlı olabilir. Docker Sısınma ve Kubernetes gibi sistemler `secrets` , bu dosya başına bu anahtarla düzenlenmiş Windows kapsayıcılarına de olanak sağlar.

Öznitelik ayrıntıları:

* `directoryPath`İstenir. Değerlere bakmak için bir yol belirtir. Docker for Windows gizli dizileri *C:\programdata\docker\gizlilikler* dizininde varsayılan olarak depolanır.
* `ignorePrefix`-Bu önek ile başlayan dosyalar hariç tutulur. Varsayılan olarak "Yoksay" olarak belirlenmiştir.
* `keyDelimiter`-Varsayılan değer `null` . Belirtilmişse, yapılandırma Oluşturucusu dizinin birden çok düzeyine geçiş yaparken bu sınırlayıcıyla anahtar adları oluşturuyor. Bu değer ise, `null` yapılandırma Oluşturucusu yalnızca dizinin en üst düzeyine bakar.
* `optional`-Varsayılan değer `false` . Kaynak dizin yoksa yapılandırma oluşturucusunun hatalara neden olup olmayacağını belirtir.

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin. Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core projeleri genellikle yapılandırma için JSON dosyalarını kullanır. [Simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) oluşturucusu, .NET Framework .NET Core JSON dosyalarının kullanılmasına izin verir. Bu yapılandırma Oluşturucusu, düz bir anahtar/değer kaynağından .NET Framework yapılandırmanın belirli bir anahtar/değer alanına temel bir eşleme sağlar. Bu yapılandırma Oluşturucusu hiyerarşik **yapılandırmalar sağlamıyor.** JSON yedekleme dosyası karmaşık hiyerarşik bir nesne değil, bir sözlüğe benzerdir. Çok düzeyli hiyerarşik bir dosya kullanılabilir. Bu sağlayıcı `flatten` , her düzeyde özellik adını sınırlayıcı olarak kullanarak ekleyerek derinliği `:` .

Öznitelik ayrıntıları:

* `jsonFile`İstenir. Okunacak JSON dosyasını belirtir. `~`Karakter, uygulama köküne başvurmak için başlangıçta kullanılabilir.
* `optional`-Boolean, varsayılan değer `true` . JSON dosyası bulunamazsa özel durum üretilmesini önler.
* `jsonMode` - `[Flat|Sectional]`. `Flat` varsayılan değerdir. Ne zaman olduğunda `jsonMode` `Flat` , JSON dosyası tek bir düz anahtar/değer kaynağıdır. `EnvironmentConfigBuilder` `AzureKeyVaultConfigBuilder` Ayrıca tek bir düz anahtar/değer kaynaklarıdır. , `SimpleJsonConfigBuilder` `Sectional` Modunda yapılandırıldığında:

  * JSON dosyası kavramsal olarak yalnızca en üst düzeyde birden fazla sözlüklere bölünmüştür.
  * Sözlüklerin her biri yalnızca, bunlara iliştirilmiş en üst düzey Özellik adıyla eşleşen yapılandırma bölümüne uygulanır. Örneğin:

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

## <a name="configuration-builders-order"></a>Yapılandırma oluşturucuları sırası

[ASPNET/Microsoftconfigurationbuilder](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub deposunda, bkz. [Configurationoluşturucular yürütme sırası](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) .

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>Özel anahtar/değer yapılandırma Oluşturucusu uygulama

Yapılandırma oluşturucular gereksinimlerinizi karşılamıyorsa, özel bir tane yazabilirsiniz. `KeyValueConfigBuilder`Temel sınıf değiştirme modlarını ve çoğu önek kaygılarını işler. Yalnızca uygulama gerektiren bir proje gereklidir:

* Temel sınıftan devralınır ve ile temel bir anahtar/değer çiftleri kaynağı uygulayın `GetValue` `GetAllValues` :
* [Microsoft.Configuration.ConfigUrationoluşturucular. Base öğesini](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) projeye ekleyin.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`Temel sınıf, anahtar/değer yapılandırma oluşturucuları arasında çalışmanın ve tutarlı davranışların çoğunu sağlar.

## <a name="additional-resources"></a>Ek kaynaklar

* [Yapılandırma oluşturucular GitHub deposu](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [.NET kullanarak Azure Key Vault için hizmetten hizmete kimlik doğrulaması](/azure/key-vault/service-to-service-authentication#connection-string-support)
