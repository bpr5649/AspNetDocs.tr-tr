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
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="a4a67-103">ASP.NET WebHooks alıcıları</span><span class="sxs-lookup"><span data-stu-id="a4a67-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="a4a67-104">WebHooks'u almak gönderenin kim olduğuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a4a67-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="a4a67-105">Bazen, abonenin gerçekten dinlediğini doğrulayan bir WebHook'u kaydeden ek adımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="a4a67-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="a4a67-106">Bazı WebHook'lar, HTTP POST isteğinin yalnızca bağımsız olarak alınacak olay bilgilerine bir başvuru içerdiği bir itme-çekme modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4a67-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="a4a67-107">Genellikle güvenlik modeli biraz değişir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="a4a67-108">Microsoft ASP.NET WebHooks'un amacı, WebHooks'un belirli bir varyantını nasıl işleyeceğinibulmak için çok fazla zaman harcamadan API'nizi kablolamayı hem daha basit hem de daha tutarlı hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="a4a67-109">WebHook alıcısı, belirli bir gönderenden Gelen WebHook'ları kabul etmekten ve doğrulamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="a4a67-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="a4a67-110">Bir WebHook alıcısı, her biri kendi yapılandırması olan herhangi bir sayıda WebHook'u destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="a4a67-111">Örneğin, GitHub WebHook alıcısı WebHooks'u herhangi bir sayıdaki GitHub deposundan kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="a4a67-112">WebHook Alıcı URIs</span><span class="sxs-lookup"><span data-stu-id="a4a67-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="a4a67-113">Microsoft ASP.NET WebHooks'u yükleyerek, açık uçlu sayıda hizmetten Gelen WebHook isteklerini kabul eden genel bir WebHook denetleyicisi elde elabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a67-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="a4a67-114">Bir istek geldiğinde, belirli bir WebHook göndereni işlemek için yüklediğiniz uygun alıcıyı seçer.</span><span class="sxs-lookup"><span data-stu-id="a4a67-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="a4a67-115">Bu denetleyicinin URI'si, hizmete kaydolduğunuz WebHook URI'dir ve formdadır:</span><span class="sxs-lookup"><span data-stu-id="a4a67-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="a4a67-116">Güvenlik nedenleriyle, birçok WebHook alıcısı URI'nin *bir https* URI olmasını gerektirir ve bazı durumlarda yalnızca amaçlanan tarafın yukarıdaki URI'ye WebHook'ları gönderebileceğini zorlamak için kullanılan ek bir sorgu parametresi de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="a4a67-117">Bileşen, `<receiver>` örneğin `github` alıcının adıdır veya. `slack`</span><span class="sxs-lookup"><span data-stu-id="a4a67-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="a4a67-118">*{id}* belirli bir WebHook alıcı yapılandırmasını tanımlamak için kullanılabilecek isteğe bağlı bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a4a67-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="a4a67-119">Bu, N WebHooks'u belirli bir alıcıyla kaydetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="a4a67-120">Örneğin, aşağıdaki üç URI üç bağımsız WebHooks için kayıt için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a4a67-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="a4a67-121">WebHook Alıcısı Yükleme</span><span class="sxs-lookup"><span data-stu-id="a4a67-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="a4a67-122">Microsoft ASP.NET WebHooks kullanarak WebHooks almak için, önce WebHook sağlayıcısı veya WebHooks almak istediğiniz sağlayıcılar için Nuget paketini yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a67-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="a4a67-123">Nuget paketleri, son bölümün desteklenen hizmeti gösterdiği [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a4a67-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="a4a67-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a4a67-124">For example</span></span>

<span data-ttu-id="a4a67-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub ve [Microsoft.AspNet.WebHooks.Receivers.Custom'dan](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) WebHook'lar almak için destek sağlar ASP.NET WebHooks tarafından oluşturulan WebHook'ları almak için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4a67-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="a4a67-126">Kutunun dışında Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello ve WordPress için destek bulabilirsiniz ama diğer sağlayıcıların herhangi bir sayı desteklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a4a67-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="a4a67-127">WebHook Alıcısı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4a67-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="a4a67-128">WebHook Alıcıları [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface üzerinden yapılandırılır ve bu arabirimin belirli uygulamaları herhangi bir bağımlılık enjeksiyon modeli kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="a4a67-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="a4a67-129">Varsayılan uygulama, Web.config dosyasında ayarlanabilen veya Azure Web Apps'ı kullanıyorsanız [Azure Portalı](https://portal.azure.com/)üzerinden ayarlanabilen Uygulama Ayarları'nı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4a67-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure Uygulama Ayarları](_static/AzureAppSettings.png)

<span data-ttu-id="a4a67-131">Uygulama Ayar anahtarlarının biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a4a67-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="a4a67-132">Değer, Örneğin WebHooks'un kaydedildiği *{id}* değerleriyle eşleşen virgülle ayrılmış değerler listesidir:</span><span class="sxs-lookup"><span data-stu-id="a4a67-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="a4a67-133">WebHook Alıcısı Başlatma</span><span class="sxs-lookup"><span data-stu-id="a4a67-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="a4a67-134">WebHook Alıcıları, genellikle *WebApiConfig* statik sınıfında, örneğin, bunları kaydederek başharfe çevrilir:</span><span class="sxs-lookup"><span data-stu-id="a4a67-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
