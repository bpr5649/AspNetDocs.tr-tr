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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="95a35-103">ASP.NET WebHooks işleyicileri</span><span class="sxs-lookup"><span data-stu-id="95a35-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="95a35-104">WebHooks istekleri bir WebHook alıcısı tarafından doğrulandıktan sonra, kullanıcı kodu yla işlenmeye hazırdır.</span><span class="sxs-lookup"><span data-stu-id="95a35-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="95a35-105">Burası *işleyicilerin* devreye girildiği yer.</span><span class="sxs-lookup"><span data-stu-id="95a35-105">This is where *handlers* come in.</span></span> <span data-ttu-id="95a35-106">İşleyiciler [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) arabiriminden türeyen ancak genellikle doğrudan arabirimden türeyen [webhookhandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="95a35-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="95a35-107">Bir WebHook isteği bir veya daha fazla işleyici tarafından işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="95a35-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="95a35-108">İşleyiciler, Sipariş'in basit bir tamsayı olduğu (1 ile 100 arasında olması önerilen) en düşükten en yükseğe giden kendi *Sipariş* özelliğine göre sırayla çağrılır:</span><span class="sxs-lookup"><span data-stu-id="95a35-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook İşleyici Sipariş Özellik Diyagramı](_static/Handlers.png)

<span data-ttu-id="95a35-110">İşleyici isteğe bağlı olarak WebHookHandlerContext'da *Yanıt* özelliğini ayarlayabilir ve bu özellik işlemenin durmasına ve yanıtın WebHook'a HTTP yanıtı olarak geri gönderilmesine yol açar.</span><span class="sxs-lookup"><span data-stu-id="95a35-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="95a35-111">Yukarıdaki durumda, B ve B'den daha yüksek bir sıraya sahip olduğu için İşleyici C çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="95a35-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="95a35-112">Yanıtı ayarlamak genellikle yalnızca yanıtın bilgileri kaynağı API'ye geri taşıyabileceği WebHook'lar için alakalıdır.</span><span class="sxs-lookup"><span data-stu-id="95a35-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="95a35-113">Bu, örneğin Yanıtın WebHook'un geldiği kanala geri nakledildiği Slack WebHooks'taki durumdur.</span><span class="sxs-lookup"><span data-stu-id="95a35-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="95a35-114">İşleyiciler, yalnızca belirli bir alıcıdan WebHooks almak istiyorlarsa Alıcı özelliğini ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="95a35-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="95a35-115">Alıcıyı ayarlamazlarsa hepsi için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="95a35-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="95a35-116">Yanıtın diğer yaygın kullanımlarından biri, WebHook'un artık etkin olmadığını ve başka istek gönderilmemesi gerektiğini belirtmek için *410 Gone* yanıtı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="95a35-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="95a35-117">Varsayılan olarak bir işleyici tüm WebHook alıcıları tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="95a35-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="95a35-118">Ancak, *Alıcı* özelliği işleyicinin adına ayarlanmışsa, bu işleyici yalnızca bu alıcıdan WebHook istekleri alır.</span><span class="sxs-lookup"><span data-stu-id="95a35-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="95a35-119">WebHook'u Işleme</span><span class="sxs-lookup"><span data-stu-id="95a35-119">Processing a WebHook</span></span>

<span data-ttu-id="95a35-120">Bir işleyici çağrıldığında, WebHook isteği hakkında bilgi içeren bir [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) alır.</span><span class="sxs-lookup"><span data-stu-id="95a35-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="95a35-121">Veriler, genellikle HTTP istek gövdesi, *Veri* özelliğinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="95a35-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="95a35-122">Verilerin türü genellikle JSON veya HTML form verileridir, ancak istenirse daha belirli bir türe döküm yapmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="95a35-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="95a35-123">Örneğin, ASP.NET WebHooks tarafından oluşturulan özel WebHooks aşağıdaki gibi [Tür CustomBildirimler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) döküm olabilir:</span><span class="sxs-lookup"><span data-stu-id="95a35-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="95a35-124">Sıralı İşlem</span><span class="sxs-lookup"><span data-stu-id="95a35-124">Queued Processing</span></span>

<span data-ttu-id="95a35-125">Yanıt birkaç saniye içinde oluşturulmazsa, çoğu WebHook gönderen kişi bir WebHook'u yeniden gönderir.</span><span class="sxs-lookup"><span data-stu-id="95a35-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="95a35-126">Bu, işleyicinizin yeniden çağrılmaması için işlemi bu zaman dilimi içinde tamamlaması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="95a35-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="95a35-127">İşlem daha uzun sürerse veya ayrı olarak daha iyi işlenirse, [WebHookQueueHandler WebHook](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) isteğini sıraya (örneğin [Azure Depolama Kuyruğu)](https://msdn.microsoft.com/library/azure/dd179353.aspx)göndermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="95a35-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="95a35-128">[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) uygulamasının anahattı burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="95a35-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
