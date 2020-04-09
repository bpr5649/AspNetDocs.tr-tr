---
uid: webhooks/receiving/handlers
title: ASP.NET WebHooks işleyicileri | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET WebHooks'taki istekler nasıl işleyeceğini.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675212"
---
# <a name="aspnet-webhooks-handlers"></a>ASP.NET WebHooks işleyicileri

WebHooks istekleri bir WebHook alıcısı tarafından doğrulandıktan sonra, kullanıcı kodu yla işlenmeye hazırdır. Burası *işleyicilerin* devreye girildiği yer. İşleyiciler [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) arabiriminden türeyen ancak genellikle doğrudan arabirimden türeyen [webhookhandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) sınıfını kullanır.

Bir WebHook isteği bir veya daha fazla işleyici tarafından işlenebilir. İşleyiciler, Sipariş'in basit bir tamsayı olduğu (1 ile 100 arasında olması önerilen) en düşükten en yükseğe giden kendi *Sipariş* özelliğine göre sırayla çağrılır:

![WebHook İşleyici Sipariş Özellik Diyagramı](_static/Handlers.png)

İşleyici isteğe bağlı olarak WebHookHandlerContext'da *Yanıt* özelliğini ayarlayabilir ve bu özellik işlemenin durmasına ve yanıtın WebHook'a HTTP yanıtı olarak geri gönderilmesine yol açar. Yukarıdaki durumda, B ve B'den daha yüksek bir sıraya sahip olduğu için İşleyici C çağrılmaz.

Yanıtı ayarlamak genellikle yalnızca yanıtın bilgileri kaynağı API'ye geri taşıyabileceği WebHook'lar için alakalıdır. Bu, örneğin Yanıtın WebHook'un geldiği kanala geri nakledildiği Slack WebHooks'taki durumdur. İşleyiciler, yalnızca belirli bir alıcıdan WebHooks almak istiyorlarsa Alıcı özelliğini ayarlayabilir. Alıcıyı ayarlamazlarsa hepsi için çağrılır.

Yanıtın diğer yaygın kullanımlarından biri, WebHook'un artık etkin olmadığını ve başka istek gönderilmemesi gerektiğini belirtmek için *410 Gone* yanıtı kullanmaktır.

Varsayılan olarak bir işleyici tüm WebHook alıcıları tarafından çağrılır. Ancak, *Alıcı* özelliği işleyicinin adına ayarlanmışsa, bu işleyici yalnızca bu alıcıdan WebHook istekleri alır.

## <a name="processing-a-webhook"></a>WebHook'u Işleme

Bir işleyici çağrıldığında, WebHook isteği hakkında bilgi içeren bir [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) alır. Veriler, genellikle HTTP istek gövdesi, *Veri* özelliğinden kullanılabilir.

Verilerin türü genellikle JSON veya HTML form verileridir, ancak istenirse daha belirli bir türe döküm yapmak mümkündür. Örneğin, ASP.NET WebHooks tarafından oluşturulan özel WebHooks aşağıdaki gibi [Tür CustomBildirimler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) döküm olabilir:

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>Sıralı İşlem

Yanıt birkaç saniye içinde oluşturulmazsa, çoğu WebHook gönderen kişi bir WebHook'u yeniden gönderir. Bu, işleyicinizin yeniden çağrılmaması için işlemi bu zaman dilimi içinde tamamlaması gerektiği anlamına gelir.

İşlem daha uzun sürerse veya ayrı olarak daha iyi işlenirse, [WebHookQueueHandler WebHook](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) isteğini sıraya (örneğin [Azure Depolama Kuyruğu)](https://msdn.microsoft.com/library/azure/dd179353.aspx)göndermek için kullanılabilir.

[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) uygulamasının anahattı burada verilmiştir:

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
