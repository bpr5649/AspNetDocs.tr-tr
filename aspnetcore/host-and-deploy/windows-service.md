---
title: ASP.NET Core bir Windows hizmetinde barındırma
author: guardrex
description: ASP.NET Core uygulaması bir Windows hizmetinde barındırmayı öğrenin.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: 081a631c9c3e74c01e15f4b0b272d650c162bd20
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068001"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>ASP.NET Core bir Windows hizmetinde barındırma

Tarafından [Luke Latham](https://github.com/guardrex) ve [Tom Dykstra](https://github.com/tdykstra)

ASP.NET Core uygulaması Windows barındırılabilen bir [Windows hizmeti](/dotnet/framework/windows-services/introduction-to-windows-service-applications) IIS kullanmadan. Bir Windows hizmeti olarak barındırıldığında, uygulama yeniden başlatma sonrasında otomatik olarak başlar.

[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))

## <a name="deployment-type"></a>Dağıtım türü

Her iki framework bağımlı veya kendi içinde Windows hizmet dağıtımı oluşturabilirsiniz. Bilgi ve dağıtım senaryoları hakkında daha fazla öneri için bkz. [.NET Core uygulama dağıtımı](/dotnet/core/deploying/).

### <a name="framework-dependent-deployment"></a>Framework bağımlı dağıtım

.NET Core hedef sistemdeki bir paylaşılan sistem genelinde sürüm varlığını Framework bağımlı dağıtım (FDD) kullanır. FDD senaryo ile bir ASP.NET Core Windows hizmeti uygulaması kullanıldığında, SDK'sı bir çalıştırılabilir dosyası oluşturur (*\*.exe*) adlı bir *framework bağımlı yürütülebilir*.

### <a name="self-contained-deployment"></a>Kendi içinde dağıtım

Hedef sistemdeki paylaşılan Bileşenler'in müstakil dağıtım (SCD) içermez. Çalışma zamanı ve uygulamanın bağımlılıklarını, barındıran sistemde uygulamaya ile dağıtılır.

## <a name="convert-a-project-into-a-windows-service"></a>Bir Windows hizmetinde bir projeyi dönüştürmeye

Uygulamayı bir hizmet olarak çalıştırmak için mevcut bir ASP.NET Core projesi için aşağıdaki değişiklikleri yapın:

### <a name="project-file-updates"></a>Proje dosyası güncelleştirmeleri

Tercih ettiğiniz tabanlı [dağıtım türü](#deployment-type), proje dosyasını güncelleştirin:

#### <a name="framework-dependent-deployment-fdd"></a>Framework bağımlı dağıtım (FDD)

Bir Windows ekleme [çalışma zamanı tanımlayıcı (RID)](/dotnet/core/rid-catalog) için `<PropertyGroup>` , hedef Framework'ü içerir. Aşağıdaki örnekte, RID kümesine `win7-x64`. Ekleme `<SelfContained>` özelliğini `false`. Bu özellikler, yürütülebilir bir dosya oluşturmak için SDK'sı isteyin (*.exe*) için Windows dosyası.

A *web.config* normalde bir ASP.NET Core uygulaması yayımlama sırasında oluşturulur, dosya, bir Windows hizmet uygulaması için gereksiz. Oluşturulmasını devre dışı bırakmak için *web.config* ekleyin `<IsTransformWebConfigDisabled>` özelliğini `true`.

::: moniker range=">= aspnetcore-2.2"

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

Ekleme `<UseAppHost>` özelliğini `true`. Bu özellik etkinleştirme yolu hizmetiyle sağlar (bir yürütülebilir dosya *.exe*) bir FDD için.

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.1</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <UseAppHost>true</UseAppHost>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

#### <a name="self-contained-deployment-scd"></a>Kendi başına dağıtım (SCD)

Bir Windows varlığını onaylamak [çalışma zamanı tanımlayıcı (RID)](/dotnet/core/rid-catalog) veya eklemek için bir RID `<PropertyGroup>` , hedef Framework'ü içerir. Oluşturulmasını devre dışı bir *web.config* ekleyerek dosya `<IsTransformWebConfigDisabled>` özelliğini `true`.

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

İçin birden fazla RID yayımlamak için:

* RID noktalı virgülle ayrılmış bir liste sağlar.
* Özellik adını kullanan `<RuntimeIdentifiers>` (çoğul).

  Daha fazla bilgi için [.NET Core RID Kataloğu](/dotnet/core/rid-catalog).

İçin bir paket başvurusu ekleme [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).

Windows olay günlüğü günlük kaydını etkinleştirmek için paket başvurusu ekleyin [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog).

Daha fazla bilgi için [başlatılması ve durdurulması olaylarını işlemek](#handle-starting-and-stopping-events) bölümü.

### <a name="programmain-updates"></a>Program.Main güncelleştirmeleri

Aşağıdaki değişiklikleri yapın `Program.Main`:

* Test ve hizmet dışında çalışırken hata ayıklama için uygulamayı bir hizmet veya bir konsol uygulaması olarak çalışıp çalışmadığını belirlemek için kod ekleyin. Hata ayıklayıcıyı eklediyseniz veya inceleyin `--console` komut satırı bağımsız değişkeni varsa.

  İki koşuldan birinin (uygulamayı değil çalıştırma hizmet olarak) true ise, çağrı <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> Web ana bilgisayarı üzerinde.

  Koşullar (uygulama, hizmet olarak çalıştırıldığında) false olduğunda:

  * Çağrı <xref:System.IO.Directory.SetCurrentDirectory*> ve uygulamanın yayımlanmış konumuna bir yol kullanın. Remove() çağırmayın <xref:System.IO.Directory.GetCurrentDirectory*> bir Windows hizmeti uygulaması döndürüldüğünden yolunu almak için *C:\\WINDOWS\\system32* klasör zaman <xref:System.IO.Directory.GetCurrentDirectory*> çağrılır. Daha fazla bilgi için [geçerli dizin ve içerik kök](#current-directory-and-content-root) bölümü.
  * Çağrı <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> uygulamasını bir hizmet olarak çalıştırmak için.

  Çünkü [komut satırı yapılandırma sağlayıcısı](xref:fundamentals/configuration/index#command-line-configuration-provider) komut satırı bağımsız değişkenleri için ad-değer çiftleri gerektirir `--console` anahtarı bağımsız değişkenlerden önce kaldırılır <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> bunları alır.

* Windows olay günlüğüne yazmak için olay günlüğü Sağlayıcısı Ekle <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>. İle günlük tutma düzeyini ayarlamaya `Logging:LogLevel:Default` anahtarını *appsettings. Production.JSON* dosya. Tanıtım ve test amacıyla örnek uygulamanın üretim ayarları dosyası günlüğe kaydetme düzeyini ayarlar `Information`. Üretim ortamında genellikle değerine `Error`. Daha fazla bilgi için bkz. <xref:fundamentals/logging/index#windows-eventlog-provider>.

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

### <a name="publish-the-app"></a>Uygulamayı yayımlama

Kullanarak uygulama yayımlamayı [dotnet yayımlama](/dotnet/articles/core/tools/dotnet-publish), [Visual Studio yayımlama profilini](xref:host-and-deploy/visual-studio-publish-profiles), veya Visual Studio Code. Visual Studio kullanırken **FolderProfile** ve yapılandırma **hedef konum** seçmeden önce **Yayımla** düğmesi.

Komut satırı arabirimi (CLI) araçlarını kullanarak örnek uygulamayı yayımlamak için çalıştırma [dotnet yayımlama](/dotnet/core/tools/dotnet-publish) geçirilen bir sürüm yapılandırması ile proje klasöründeki bir komut isteminde komutunu [- c |--yapılandırma](/dotnet/core/tools/dotnet-publish#options)seçeneği. Kullanım [-o |--çıktı](/dotnet/core/tools/dotnet-publish#options) uygulama dışında bir klasöre yayımlamak için bir yol ile seçeneği.

#### <a name="publish-a-framework-dependent-deployment-fdd"></a>Framework bağımlı dağıtım (FDD) yayımlama

Aşağıdaki örnekte, uygulama için yayımlanan *c:\\svc* klasörü:

```console
dotnet publish --configuration Release --output c:\svc
```

#### <a name="publish-a-self-contained-deployment-scd"></a>Kendi içinde bir dağıtım (SCD) yayımlama

RID belirtilmelidir `<RuntimeIdenfifier>` (veya `<RuntimeIdentifiers>`) özelliği proje dosyasının. Çalışma zamanı kaynağı [- r |--çalışma zamanı](/dotnet/core/tools/dotnet-publish#options) seçeneği `dotnet publish` komutu.

Aşağıdaki örnekte, uygulama için yayımlanan `win7-x64` çalışma zamanına *c:\\svc* klasörü:

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

### <a name="create-a-user-account"></a>Bir kullanıcı hesabı oluşturun

Hizmet kullanımı için bir kullanıcı hesabı oluşturma `net user` bir yönetici komut kabuğu komutunu:

```console
net user {USER ACCOUNT} {PASSWORD} /add
```

Varsayılan parola süre sonu altı hafta olur.

Örnek uygulama için bir kullanıcı hesabı adı ile oluşturun. `ServiceUser` ve parola. Aşağıdaki komutta `{PASSWORD}` ile bir [güçlü parola](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).

```console
net user ServiceUser {PASSWORD} /add
```

Bir gruba kullanıcı eklemeniz gerekiyorsa, kullanın `net localgroup` komutu, burada `{GROUP}` grubunun adıdır:

```console
net localgroup {GROUP} {USER ACCOUNT} /add
```

Daha fazla bilgi için [hizmeti kullanıcı hesaplarını](/windows/desktop/services/service-user-accounts).

Active Directory kullanarak kullanıcıları yönetme için alternatif bir yaklaşım, yönetilen hizmet hesaplarını kullanmaktır. Daha fazla bilgi için [Grup yönetilen hizmet hesaplarına genel bakış](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

### <a name="set-permissions"></a>İzinleri ayarlama

#### <a name="access-to-the-app-folder"></a>Uygulama klasör erişimi

Uygulamanın klasörüne yazma/okuma/yürütme erişimi vermek kullanarak [icacls](/windows-server/administration/windows-commands/icacls) bir yönetici komut kabuğu komutunu:

```console
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* `{PATH}` &ndash; Uygulamanın klasörün yolu.
* `{USER ACCOUNT}` &ndash; Kullanıcı hesabı (SID).
* `(OI)` &ndash; Nesne devral bayrağı dosyaları alt izinleri yayar.
* `(CI)` &ndash; Kapsayıcı devral bayrağı, alt klasörler için izinleri yayar.
* `{PERMISSION FLAGS}` &ndash; Uygulamanın erişim izinlerini ayarlar.
  * Yazma (`W`)
  * Okuma (`R`)
  * Yürütme (`X`)
  * Tam (`F`)
  * Değiştir (`M`)
* `/t` &ndash; Yinelemeli olarak mevcut alt klasörler ve dosyalar için geçerlidir.

Örnek uygulamayı yayımlanan *c:\\svc* klasörü ve `ServiceUser` hesap yazma/okuma/Yürütme izinleri, aşağıdaki komutu kullanın:

```console
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

Daha fazla bilgi için [icacls](/windows-server/administration/windows-commands/icacls).

#### <a name="log-on-as-a-service"></a>Bir hizmet olarak oturum aç

Vermek [hizmet oturum açma](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) ayrıcalıklı kullanıcı hesabı için:

1. Bulun **kullanıcı hakları ataması** Yerel Güvenlik İlkesi konsolunu veya yerel Grup İlkesi Düzenleyicisi Konsolu ilkeleri. Yönergeler için, bkz: [Güvenlik İlkesi ayarlarını yapılandırma](/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).
1. Bulun `Log on as a service` ilkesi. Açmak için ilkeye çift tıklayın.
1. Seçin **kullanıcı veya grup ekleme**.
1. Seçin **Gelişmiş** seçip **Şimdi Bul**.
1. Oluşturulan kullanıcı hesabını seçin [bir kullanıcı hesabı oluşturma](#create-a-user-account) bölümüne. Seçin **Tamam** Seçimi kabul etmek için.
1. Seçin **Tamam** nesne adının doğru olduğunu onayladıktan sonra.
1. **Uygula**’yı seçin. Seçin **Tamam** İlkesi penceresini kapatın.

## <a name="manage-the-service"></a>Hizmeti yönetme

### <a name="create-the-service"></a>Hizmet oluşturma

Kullanım [sc.exe](https://technet.microsoft.com/library/bb490995) bir yönetim komut kabuğu'ndan bir hizmet oluşturmak için komut satırı aracı. `binPath` Değerdir yürütülebilir dosya adını içeren uygulamanın yürütülebilir dosyanın yolu. **Eşittir işareti ve tırnak karakteri her bir parametre ve değer arasında gerekli bir alandır.**

```console
sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
```

* `{SERVICE NAME}` &ndash; Hizmete atanacak ad [Hizmet Denetimi Yöneticisi](/windows/desktop/services/service-control-manager).
* `{PATH}` &ndash; Hizmet yürütülebilir dosya yolu.
* `{DOMAIN}` &ndash; Etki alanına katılmış bir makine etki alanı. Makine etki alanına katılmış değilse, yerel makine adını kullanın.
* `{USER ACCOUNT}` &ndash; Hizmetinin çalıştığı kullanıcı hesabı.
* `{PASSWORD}` &ndash; Kullanıcı hesabı parolası.

> [!WARNING]
> Yapmak **değil** atlamak `obj` parametresi. İçin varsayılan değer `obj` olduğu [LocalSystem hesabı](/windows/desktop/services/localsystem-account) hesabı. Altında bir hizmeti çalıştıran `LocalSystem` hesabı önemli bir güvenlik riski sunar. Her zaman bir servis ayrıcalıkları sınırlı sahip bir kullanıcı hesabı ile çalıştırın.

Aşağıdaki örnekte örnek uygulama için:

* Adlı hizmetin **MyService**.
* Yayınlanan hizmet bulunan *c:\\svc* klasör. Uygulama yürütülebilir dosyası adlı *SampleApp.exe*. İçine `binPath` çift tırnak (") değeri.
* Altında çalışacağı `ServiceUser` hesabı. Değiştirin `{DOMAIN}` kullanıcı hesabının etki alanı veya yerel makine adı. İçine `obj` çift tırnak (") değeri. Örnek: Barındıran sistemde adlı bir yerel makineye ise `MairaPC`ayarlayın `obj` için `"MairaPC\ServiceUser"`.
* Değiştirin `{PASSWORD}` ile kullanıcı hesabının parolası. İçine `password` çift tırnak (") değeri.

```console
sc create MyService binPath= "c:\svc\sampleapp.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
```

> [!IMPORTANT]
> Parametreleri eşittir işareti ve parametrelerin değerleri arasında boşluk bulunmadığından emin olun.

### <a name="start-the-service"></a>Hizmeti Başlat

Hizmetle başlar `sc start {SERVICE NAME}` komutu.

Örnek uygulama hizmeti başlatmak için aşağıdaki komutu kullanın:

```console
sc start MyService
```

Komut hizmeti başlatmak için birkaç saniye sürer.

### <a name="determine-the-service-status"></a>Hizmet durumunu belirleme

Hizmet durumunu denetlemek için kullanmak `sc query {SERVICE NAME}` komutu. Durumu aşağıdaki değerlerden biri olarak bildirilir:

* `START_PENDING`
* `RUNNING`
* `STOP_PENDING`
* `STOPPED`

Örnek uygulama hizmeti durumunu denetlemek için aşağıdaki komutu kullanın:

```console
sc query MyService
```

### <a name="browse-a-web-app-service"></a>Bir web app service Gözat

Hizmet olduğunda `RUNNING` durum ve hizmeti bir web uygulaması ise, uygulama, bir yola göz atın (varsayılan olarak, `http://localhost:5000`, hangi yönlendiren `https://localhost:5001` kullanırken [HTTPS yeniden yönlendirmesi ara yazılım](xref:security/enforcing-ssl)).

Örnek app service için uygulamaya Gözat `http://localhost:5000`.

### <a name="stop-the-service"></a>Hizmeti Durdur

Hizmetle Durdur `sc stop {SERVICE NAME}` komutu.

Aşağıdaki komut örnek uygulama hizmetini durdurur:

```console
sc stop MyService
```

### <a name="delete-the-service"></a>Hizmeti Sil

Hizmeti ile bir hizmeti durdurmak için bir kısa bir gecikmeyle kaldırmanız `sc delete {SERVICE NAME}` komutu.

Örnek uygulama hizmeti durumunu kontrol edin:

```console
sc query MyService
```

Örnek uygulama hizmeti olduğunda `STOPPED` durum, örnek uygulama hizmeti kaldırmak için aşağıdaki komutu kullanın:

```console
sc delete MyService
```

## <a name="handle-starting-and-stopping-events"></a>Başlatma ve durdurma olayları işleme

İşlenecek <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*>, ve <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> olayları, aşağıdaki ek değişiklikleri gerçekleştirin:

1. Türetilen bir sınıf oluşturmanız <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService> ile `OnStarting`, `OnStarted`, ve `OnStopping` yöntemleri:

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. Bir genişletme yöntemi için oluşturma <xref:Microsoft.AspNetCore.Hosting.IWebHost> Geçiren `CustomWebHostService` için <xref:System.ServiceProcess.ServiceBase.Run*>:

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. İçinde `Program.Main`, çağrı `RunAsCustomService` genişletme yöntemi yerine <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>:

   ```csharp
   host.RunAsCustomService();
   ```

   Konumu görmek için <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> içinde `Program.Main`, gösterilen kod örneği başvurmak [bir Windows hizmetinde bir projeyi dönüştürmeye](#convert-a-project-into-a-windows-service) bölümü.

## <a name="proxy-server-and-load-balancer-scenarios"></a>Ara sunucu ve yük dengeleyici senaryoları

Internet'ten veya kurumsal ağ istekleri etkileşim ve bir proxy'nin arkasındaysa veya yük dengeleyici Hizmetleri ek yapılandırma gerektirebilir. Daha fazla bilgi için bkz. <xref:host-and-deploy/proxy-load-balancer>.

## <a name="configure-https"></a>HTTPS yapılandırma

Hizmet güvenli bir uç nokta ile yapılandırmak için:

1. Barındırma system, platformun sertifika edinme ve dağıtım mekanizmalarını kullanarak bir X.509 sertifikası oluşturun.

1. Belirtin bir [Kestrel sunucu HTTPS uç noktası yapılandırması](xref:fundamentals/servers/kestrel#endpoint-configuration) sertifikayı kullanmak için.

Hizmet uç noktası güvenli hale getirmek için ASP.NET Core HTTPS geliştirme sertifikası kullanılması desteklenmiyor.

## <a name="current-directory-and-content-root"></a>Geçerli dizin ve içerik kök

Geçerli çalışma dizini çağırarak döndürülen <xref:System.IO.Directory.GetCurrentDirectory*> bir Windows hizmeti için *C:\\WINDOWS\\system32* klasör. *System32* klasör değil bir hizmetin dosyaları (örneğin, ayarları) depolamak için uygun bir konum. Korumak ve bir hizmetin varlıklar ve ayar dosyaları erişmek için aşağıdaki yaklaşımlardan birini kullanın.

### <a name="set-the-content-root-path-to-the-apps-folder"></a>Uygulamanın klasör için içerik kök yolu ayarlayın

<xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> Sağlanan aynı yol `binPath` hizmeti oluşturulduğunda bağımsız değişken. Çağırmak yerine `GetCurrentDirectory` ayarları dosyalara olan yolları oluşturmak için arama <xref:System.IO.Directory.SetCurrentDirectory*> ile içerik uygulamanın kök yolu.

İçinde `Program.Main`, hizmetin yürütülebilir dosya klasörü yolunu belirlemek ve uygulamanın içerik kök'kurmak için yolunu kullanın:

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a>Disk üzerinde uygun bir konumda hizmetin dosyaları Store

Mutlak bir yol belirtin <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> kullanırken bir <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> dosyaları içeren klasör.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kestrel'i uç nokta Yapılandırması](xref:fundamentals/servers/kestrel#endpoint-configuration) (HTTPS yapılandırma ve SNI desteği içerir)
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>
