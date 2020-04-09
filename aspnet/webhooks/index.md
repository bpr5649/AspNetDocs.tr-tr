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
# <a name="aspnet-webhooks-overview"></a>ASP.NET WebHooks genel bakış

WebHooks birlikte Web API'ler ve SaaS hizmetleri kablolama için basit bir pub / alt model sağlayan hafif bir HTTP desen. Bir hizmette bir olay gerçekleştiğinde, kayıtlı abonelere HTTP POST isteği şeklinde bir bildirim gönderilir. POST isteği, alıcının buna göre hareket etmesini mümkün kılan olay hakkında bilgi içerir.

Onların basitlik nedeniyle, WebHooks zaten [Dropbox](http://dropbox.com/)dahil hizmetlerin çok sayıda maruz , [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), ve daha birçok. Örneğin, Bir WebHook [Dropbox'ta](http://dropbox.com/)bir dosyanın değiştiğini veya GitHub'da bir kod değişikliği nin işlendiğini veya [PayPal'da](http://www.paypal.com/)bir ödeme nin başlatıldığını veya [Trello'da](http://www.trello.com/)bir kart oluşturulduğunu gösterebilir. Olasılıklar sonsuzdur!

Microsoft ASP.NET WebHooks, ASP.NET uygulamanızın bir parçası olarak WebHooks'u göndermenizi ve almayı kolaylaştırır:

* Alıcı tarafta, webhook sağlayıcılarının herhangi bir sayıda niçin WebHooks almak ve işlemek için ortak bir model sağlar. Bu [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Bolluk,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) ve [Zendesk](https://www.zendesk.com/) desteği ile kutusundan çıkar ama daha fazlası için destek eklemek kolaydır.

* Gönderen tarafta, aboneliklerin yönetilmesi ve depolanmasının yanı sıra doğru abone kümesine olay bildirimleri gönderilmesi için destek sağlar. Bu, abonelerin abone olabileceği kendi etkinlik kümenizi tanımlamanızı ve bir şeyler olduğunda bunları bildirmenize olanak tanır.

İki parça, senaryonuza bağlı olarak birlikte veya ayrı olarak kullanılabilir. Yalnızca diğer hizmetlerden WebHook almanız gerekiyorsa, yalnızca alıcı kısmını kullanabilirsiniz; Yalnızca başkalarının tüketebileceği WebHooks'u ifşa etmek istiyorsanız, bunu yapabilirsiniz.

Kod, Web API 2 ve ASP.NET MVC 5 ASP.NET hedefler ve [GitHub'da OSS](https://github.com/aspnet/WebHooks)olarak kullanılabilir.

## <a name="webhooks-overview"></a>WebHooks Genel Bakış

WebHooks, hizmetten hizmete nasıl kullanıldığını farklı olarak değişir, ancak temel fikir aynıdır. WebHooks'u, kullanıcının başka bir yerde gerçekleşen olaylara abone olabileceği basit bir pub/alt model olarak düşünebilirsiniz. Olay bildirimleri, olayın kendisi hakkında bilgi içeren HTTP POST istekleri olarak yayılır.

Genellikle HTTP POST isteği, WebHook'un tetiklemesine neden olan olayla ilgili bilgileri içeren WebHook gönderentarafından belirlenen bir JSON nesnesi veya HTML form verileri içerir. Örneğin, [GitHub'dan](https://www.github.com/) bir WebHook POST istek gövdesi, belirli bir depoda açılan yeni bir sorunun sonucu olarak şuna benzer:

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

WebHook'un gerçekten de amaçlanan gönderenden olduğundan emin olmak için, POST isteği bir şekilde güvence altına alındı ve alıcı tarafından doğrulandı. Örneğin, [GitHub WebHooks,](https://developer.github.com/webhooks/) alıcı uygulaması tarafından kontrol edilen istek gövdesinin karma sına sahip bir *X-Hub-Signature* HTTP üstbilgisini içerir, böylece bu konuda endişelenmenize gerek kalmaz.

WebHook akışı genellikle böyle bir şey gider:

* WebHook gönderen, istemcinin abone olabileceği olayları ortaya çıkarır. Olaylar, sistemde gözlemlenebilir değişiklikleri, örneğin yeni bir veri öğesinin eklendiğini, bir işlemin tamamlandığını veya başka bir şeyi açıklar.

* WebHook alıcısı dört şeyden oluşan bir WebHook kaydederek abone olur:

     1. Olay bildiriminin HTTP POST isteği şeklinde yayınlanması gereken bir URI;

     2. WebHook'un ateşlendiği belirli olayları açıklayan bir filtre kümesi;

     3. HTTP POST isteğini imzalamak için kullanılan gizli bir anahtar;

     4. HTTP POST isteğine eklenecek ek veriler. Bu, örneğin HTTP POST istek gövdesine ek HTTP üstbilgi alanları veya özellikleri olabilir.

* Bir olay gerçekleştiğinde, eşleşen WebHook kayıtları bulunur ve HTTP POST istekleri gönderilir. Genellikle, alıcı yanıt vermiyorsa veya HTTP POST isteği bir hata yanıtı yla sonuçlanırsa, HTTP POST isteklerinin oluşumu birkaç kez yeniden denendi.

## <a name="webhooks-processing-pipeline"></a>WebHooks İşleme Boru Hattı

Microsoft ASP.NET Gelen WebHooks için WebHooks işleme ardışık boru hattı aşağıdaki gibi görünür:

![ASP.NET WebHooks İşleme Boru Hattı](_static/WebHookReceivers.png)

Burada iki temel kavramlar *Alıcılar* ve *Handlers şunlardır:*

* *Alıcılar,* belirli bir gönderenden Gelen WebHook'un belirli lezzetini işlemekten ve WebHook isteğinin gerçekten amaçlanan gönderenden olduğundan emin olmak için güvenlik denetimlerini zorlamaktan sorumludur.

* *İşleyiciler* genellikle kullanıcı kodunun belirli WebHook'u işleyerek çalıştığı yerdir.

Aşağıdaki düğümlerde bu kavramlar daha ayrıntılı olarak açıklanmıştır.
