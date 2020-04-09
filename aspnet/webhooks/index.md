---
uid: webhooks/index
title: ASP.NET WebHooks Genel Bakış | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET WebHooks'a giriş.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675437"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="ea763-103">ASP.NET WebHooks genel bakış</span><span class="sxs-lookup"><span data-stu-id="ea763-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="ea763-104">WebHooks birlikte Web API'ler ve SaaS hizmetleri kablolama için basit bir pub / alt model sağlayan hafif bir HTTP desen.</span><span class="sxs-lookup"><span data-stu-id="ea763-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="ea763-105">Bir hizmette bir olay gerçekleştiğinde, kayıtlı abonelere HTTP POST isteği şeklinde bir bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="ea763-106">POST isteği, alıcının buna göre hareket etmesini mümkün kılan olay hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="ea763-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="ea763-107">Onların basitlik nedeniyle, WebHooks zaten [Dropbox](http://dropbox.com/)dahil hizmetlerin çok sayıda maruz , [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), ve daha birçok.</span><span class="sxs-lookup"><span data-stu-id="ea763-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="ea763-108">Örneğin, Bir WebHook [Dropbox'ta](http://dropbox.com/)bir dosyanın değiştiğini veya GitHub'da bir kod değişikliği nin işlendiğini veya [PayPal'da](http://www.paypal.com/)bir ödeme nin başlatıldığını veya [Trello'da](http://www.trello.com/)bir kart oluşturulduğunu gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="ea763-109">Olasılıklar sonsuzdur!</span><span class="sxs-lookup"><span data-stu-id="ea763-109">The possibilities are endless!</span></span>

<span data-ttu-id="ea763-110">Microsoft ASP.NET WebHooks, ASP.NET uygulamanızın bir parçası olarak WebHooks'u göndermenizi ve almayı kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="ea763-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="ea763-111">Alıcı tarafta, webhook sağlayıcılarının herhangi bir sayıda niçin WebHooks almak ve işlemek için ortak bir model sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea763-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="ea763-112">Bu [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Bolluk,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) ve [Zendesk](https://www.zendesk.com/) desteği ile kutusundan çıkar ama daha fazlası için destek eklemek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ea763-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="ea763-113">Gönderen tarafta, aboneliklerin yönetilmesi ve depolanmasının yanı sıra doğru abone kümesine olay bildirimleri gönderilmesi için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea763-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="ea763-114">Bu, abonelerin abone olabileceği kendi etkinlik kümenizi tanımlamanızı ve bir şeyler olduğunda bunları bildirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ea763-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="ea763-115">İki parça, senaryonuza bağlı olarak birlikte veya ayrı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="ea763-116">Yalnızca diğer hizmetlerden WebHook almanız gerekiyorsa, yalnızca alıcı kısmını kullanabilirsiniz; Yalnızca başkalarının tüketebileceği WebHooks'u ifşa etmek istiyorsanız, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea763-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="ea763-117">Kod, Web API 2 ve ASP.NET MVC 5 ASP.NET hedefler ve [GitHub'da OSS](https://github.com/aspnet/WebHooks)olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="ea763-118">WebHooks Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ea763-118">WebHooks Overview</span></span>

<span data-ttu-id="ea763-119">WebHooks, hizmetten hizmete nasıl kullanıldığını farklı olarak değişir, ancak temel fikir aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ea763-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="ea763-120">WebHooks'u, kullanıcının başka bir yerde gerçekleşen olaylara abone olabileceği basit bir pub/alt model olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea763-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="ea763-121">Olay bildirimleri, olayın kendisi hakkında bilgi içeren HTTP POST istekleri olarak yayılır.</span><span class="sxs-lookup"><span data-stu-id="ea763-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="ea763-122">Genellikle HTTP POST isteği, WebHook'un tetiklemesine neden olan olayla ilgili bilgileri içeren WebHook gönderentarafından belirlenen bir JSON nesnesi veya HTML form verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="ea763-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="ea763-123">Örneğin, [GitHub'dan](https://www.github.com/) bir WebHook POST istek gövdesi, belirli bir depoda açılan yeni bir sorunun sonucu olarak şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="ea763-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="ea763-124">WebHook'un gerçekten de amaçlanan gönderenden olduğundan emin olmak için, POST isteği bir şekilde güvence altına alındı ve alıcı tarafından doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="ea763-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="ea763-125">Örneğin, [GitHub WebHooks,](https://developer.github.com/webhooks/) alıcı uygulaması tarafından kontrol edilen istek gövdesinin karma sına sahip bir *X-Hub-Signature* HTTP üstbilgisini içerir, böylece bu konuda endişelenmenize gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="ea763-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="ea763-126">WebHook akışı genellikle böyle bir şey gider:</span><span class="sxs-lookup"><span data-stu-id="ea763-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="ea763-127">WebHook gönderen, istemcinin abone olabileceği olayları ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="ea763-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="ea763-128">Olaylar, sistemde gözlemlenebilir değişiklikleri, örneğin yeni bir veri öğesinin eklendiğini, bir işlemin tamamlandığını veya başka bir şeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="ea763-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="ea763-129">WebHook alıcısı dört şeyden oluşan bir WebHook kaydederek abone olur:</span><span class="sxs-lookup"><span data-stu-id="ea763-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="ea763-130">Olay bildiriminin HTTP POST isteği şeklinde yayınlanması gereken bir URI;</span><span class="sxs-lookup"><span data-stu-id="ea763-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="ea763-131">WebHook'un ateşlendiği belirli olayları açıklayan bir filtre kümesi;</span><span class="sxs-lookup"><span data-stu-id="ea763-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="ea763-132">HTTP POST isteğini imzalamak için kullanılan gizli bir anahtar;</span><span class="sxs-lookup"><span data-stu-id="ea763-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="ea763-133">HTTP POST isteğine eklenecek ek veriler.</span><span class="sxs-lookup"><span data-stu-id="ea763-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="ea763-134">Bu, örneğin HTTP POST istek gövdesine ek HTTP üstbilgi alanları veya özellikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="ea763-135">Bir olay gerçekleştiğinde, eşleşen WebHook kayıtları bulunur ve HTTP POST istekleri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ea763-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="ea763-136">Genellikle, alıcı yanıt vermiyorsa veya HTTP POST isteği bir hata yanıtı yla sonuçlanırsa, HTTP POST isteklerinin oluşumu birkaç kez yeniden denendi.</span><span class="sxs-lookup"><span data-stu-id="ea763-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="ea763-137">WebHooks İşleme Boru Hattı</span><span class="sxs-lookup"><span data-stu-id="ea763-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="ea763-138">Microsoft ASP.NET Gelen WebHooks için WebHooks işleme ardışık boru hattı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="ea763-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET WebHooks İşleme Boru Hattı](_static/WebHookReceivers.png)

<span data-ttu-id="ea763-140">Burada iki temel kavramlar *Alıcılar* ve *Handlers şunlardır:*</span><span class="sxs-lookup"><span data-stu-id="ea763-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="ea763-141">*Alıcılar,* belirli bir gönderenden Gelen WebHook'un belirli lezzetini işlemekten ve WebHook isteğinin gerçekten amaçlanan gönderenden olduğundan emin olmak için güvenlik denetimlerini zorlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="ea763-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="ea763-142">*İşleyiciler* genellikle kullanıcı kodunun belirli WebHook'u işleyerek çalıştığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="ea763-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="ea763-143">Aşağıdaki düğümlerde bu kavramlar daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ea763-143">In the following nodes these concepts are described in more details.</span></span>
