---
ms.openlocfilehash: 733a41a76e289f8aed6ec2d246ed720e44808fec
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57182767"
---
Çağrı [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity) varsayılan düzen ayarlarını yapılandırır. [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_) kümeleri aşırı [DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme) özelliği. [AddAuthentication (Eylem&lt;AuthenticationOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__) aşırı yükleme, farklı amaçlar için varsayılan kimlik doğrulama düzeni ' ayarlamak için kullanılan kimlik doğrulama seçeneklerini yapılandırma sağlar. Yapılan sonraki çağrılar `AddAuthentication` önceden yapılandırılmış bir geçersiz kılma [AuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions) özellikleri.

[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder) bir kimlik doğrulama işleyicisi kaydetme genişletme yöntemleri yalnızca çağrılabilir kez kimlik doğrulama düzeni. Aşırı yüklemeler yapılandırma düzeni özellikleri, Düzen adı verin ve görünen adı yok.
