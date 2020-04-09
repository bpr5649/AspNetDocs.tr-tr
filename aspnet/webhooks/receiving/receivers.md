---
uid: webhooks/receiving/receivers
title: ASP.NET WebHooks alıcıları | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET WebHooks alıcıları
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675161"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET WebHooks alıcıları

WebHooks'u almak gönderenin kim olduğuna bağlıdır. Bazen, abonenin gerçekten dinlediğini doğrulayan bir WebHook'u kaydeden ek adımlar vardır. Bazı WebHook'lar, HTTP POST isteğinin yalnızca bağımsız olarak alınacak olay bilgilerine bir başvuru içerdiği bir itme-çekme modeli sağlar. Genellikle güvenlik modeli biraz değişir.

Microsoft ASP.NET WebHooks'un amacı, WebHooks'un belirli bir varyantını nasıl işleyeceğinibulmak için çok fazla zaman harcamadan API'nizi kablolamayı hem daha basit hem de daha tutarlı hale getirmektir.

WebHook alıcısı, belirli bir gönderenden Gelen WebHook'ları kabul etmekten ve doğrulamaktan sorumludur. Bir WebHook alıcısı, her biri kendi yapılandırması olan herhangi bir sayıda WebHook'u destekleyebilir. Örneğin, GitHub WebHook alıcısı WebHooks'u herhangi bir sayıdaki GitHub deposundan kabul edebilir.

## <a name="webhook-receiver-uris"></a>WebHook Alıcı URIs

Microsoft ASP.NET WebHooks'u yükleyerek, açık uçlu sayıda hizmetten Gelen WebHook isteklerini kabul eden genel bir WebHook denetleyicisi elde elabilirsiniz. Bir istek geldiğinde, belirli bir WebHook göndereni işlemek için yüklediğiniz uygun alıcıyı seçer.

Bu denetleyicinin URI'si, hizmete kaydolduğunuz WebHook URI'dir ve formdadır:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Güvenlik nedenleriyle, birçok WebHook alıcısı URI'nin *bir https* URI olmasını gerektirir ve bazı durumlarda yalnızca amaçlanan tarafın yukarıdaki URI'ye WebHook'ları gönderebileceğini zorlamak için kullanılan ek bir sorgu parametresi de içermelidir.

Bileşen, `<receiver>` örneğin `github` alıcının adıdır veya. `slack`

*{id}* belirli bir WebHook alıcı yapılandırmasını tanımlamak için kullanılabilecek isteğe bağlı bir tanımlayıcıdır. Bu, N WebHooks'u belirli bir alıcıyla kaydetmek için kullanılabilir. Örneğin, aşağıdaki üç URI üç bağımsız WebHooks için kayıt için kullanılabilir:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>WebHook Alıcısı Yükleme

Microsoft ASP.NET WebHooks kullanarak WebHooks almak için, önce WebHook sağlayıcısı veya WebHooks almak istediğiniz sağlayıcılar için Nuget paketini yüklersiniz. Nuget paketleri, son bölümün desteklenen hizmeti gösterdiği [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) olarak adlandırılır. Örneğin:

[Microsoft.AspNet.WebHooks.Receivers.GitHub,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub ve [Microsoft.AspNet.WebHooks.Receivers.Custom'dan](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) WebHook'lar almak için destek sağlar ASP.NET WebHooks tarafından oluşturulan WebHook'ları almak için destek sağlar.

Kutunun dışında Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello ve WordPress için destek bulabilirsiniz ama diğer sağlayıcıların herhangi bir sayı desteklemek mümkündür.

## <a name="configuring-a-webhook-receiver"></a>WebHook Alıcısı Yapılandırma

WebHook Alıcıları [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface üzerinden yapılandırılır ve bu arabirimin belirli uygulamaları herhangi bir bağımlılık enjeksiyon modeli kullanılarak kaydedilebilir. Varsayılan uygulama, Web.config dosyasında ayarlanabilen veya Azure Web Apps'ı kullanıyorsanız [Azure Portalı](https://portal.azure.com/)üzerinden ayarlanabilen Uygulama Ayarları'nı kullanır.

![Azure Uygulama Ayarları](_static/AzureAppSettings.png)

Uygulama Ayar anahtarlarının biçimi aşağıdaki gibidir:

```
MS_WebHookReceiverSecret_<receiver>
```

Değer, Örneğin WebHooks'un kaydedildiği *{id}* değerleriyle eşleşen virgülle ayrılmış değerler listesidir:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>WebHook Alıcısı Başlatma

WebHook Alıcıları, genellikle *WebApiConfig* statik sınıfında, örneğin, bunları kaydederek başharfe çevrilir:

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
