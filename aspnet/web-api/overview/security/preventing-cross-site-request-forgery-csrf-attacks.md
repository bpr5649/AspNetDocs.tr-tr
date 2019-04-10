---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET mvc'de siteler arası istek sahteciliği (CSRF) saldırılarını önleme
author: MikeWasson
description: Siteler arası istek sahteciliği (CSRF) saldırı ve ASP.NET Web MVC'de kötü CSRF önlemlerini açıklar.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392033"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>ASP.NET MVC uygulamasındaki siteler arası istek sahteciliği (CSRF) saldırılarını önleme

tarafından [Mike Wasson](https://github.com/MikeWasson)

Burada bir kötü niyetli site burada kullanıcı şu anda oturum savunmasız sitesine bir istek gönderir, siteler arası istek sahteciliği (CSRF) bir saldırı olma

CSRF saldırılarının bir örnek aşağıda verilmiştir:

1. Bir kullanıcının oturum açtığı `www.example.com` forms kimlik doğrulaması kullanma.
2. Sunucusu kullanıcının kimliğini doğrular. Sunucu yanıtı bir kimlik doğrulama tanımlama bilgisi içerir.
3. Kullanıcı oturumu kapatmak olmadan kötü amaçlı web sitesini ziyaret eder. Bu kötü niyetli site aşağıdaki HTML formu içerir: 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Form eylemi kötü niyetli site için güvenlik açığı siteye gönderir dikkat edin. CSRF "siteler arası" parçasıdır.
4. Kullanıcının gönder düğmesine tıklar. Tarayıcı, kimlik doğrulama tanımlama bilgisi ile istek içerir.
5. İstek, kullanıcının kimlik doğrulaması bağlamı sunucunuz üzerinde çalışan ve kimliği doğrulanmış bir kullanıcıyı yapmak için izin verilen herhangi bir şey yapabilirsiniz.

Bu örnekte form düğmesini tıklatarak kullanıcı gerektirse de, kötü amaçlı sayfası kolayca otomatik olarak formu gönderdiği bir betik çalıştırma gibi olabilir. Ayrıca, SSL kullanarak, bunlar "https://" istek kötü niyetli site gönderebileceğinden bile, CSRF saldırısını engellemez.

Genellikle, tarayıcılar ilgili tüm tanımlama bilgilerini hedef web sitesine göndermek için CSRF saldırılarına karşı kimlik doğrulaması için tanımlama bilgileri kullanan web siteleri mümkün olabilir. Ancak, CSRF saldırıları tanımlama bilgilerinin kötüye için sınırlı değildir. Örneğin, temel ve Özet kimlik doğrulaması ayrıca savunmasız. Sonra bir kullanıcı oturum temel veya Özet kimlik doğrulamasını açın. oturum sonlandırılana kadar tarayıcı kimlik bilgilerini otomatik olarak gönderir.

## <a name="anti-forgery-tokens"></a>Sahteciliğe karşı koruma belirteçleri

ASP.NET MVC CSRF saldırılarını önlemeye yardımcı olmak için olarak da bilinir, sahteciliğe karşı koruma belirteçleri kullanır *doğrulama belirteci istemek*.

1. İstemci, bir form içeren bir HTML sayfası ister.
2. Sunucunun yanıtta iki belirteçleri içerir. Bir simge bir tanımlama bilgisi gönderilir. Diğer bir gizli form alanına yerleştirilir. Böylece bir saldırganın değerleri tahmin edilemez belirteçleri rastgele oluşturulur.
3. İstemci formu gönderdiğinde, bu sunucuya geri hem belirteçleri göndermeniz gerekir. Bir tanımlama bilgisi tanımlama bilgisi belirteci istemciye gönderir ve formu içinde form belirteç gönderir. (Kullanıcı formu gönderdiğinde tarayıcı istemci otomatik olarak bunu yapar.)
4. Bir isteği her iki simge içermiyorsa, sunucu istek izin vermiyor.

Bir HTML formuna gizli form belirteci ile bir örneği aşağıda verilmiştir:

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

Sahteciliğe karşı koruma belirteçleri çalışır, çünkü kötü amaçlı sayfası aynı çıkış noktası ilkeleri nedeniyle kullanıcının belirteçleri okunamıyor. ([Aynı çıkış noktası ilkeleri](http://www.w3.org/Security/wiki/Same_Origin_Policy) birbirlerinin içeriğe erişmesini iki farklı sitelerde barındırılan belge engelle. Bu nedenle önceki örnekte, kötü amaçlı sayfası istekleri example.com gönderebilir, ancak yanıt okunamıyor.)

Kullanıcı oturum açtığında sonra CSRF saldırıların önlenmesine, tarayıcı sessizce göndereceği yeri sahteciliğe karşı koruma belirteçleri ile herhangi bir kimlik doğrulama protokolünü kullanmak için kimlik bilgileri. Bu tanımlama bilgisi tabanlı kimlik doğrulama protokolleri, forms kimlik doğrulaması gibi içerir hem de temel ve Özet kimlik doğrulaması gibi protokoller.

Sahteciliğe karşı koruma belirteçleri için tüm nonsafe yöntemleri (POST, PUT, DELETE) istemeniz gerekir. Ayrıca güvenli yöntemleri (GET, HEAD) yan etkileri sahip olmadığından emin olun. CORS veya JSONP, gibi etki alanları arası destek etkinleştirirseniz, ayrıca, sonra da güvenli GET gibi hassas olabilecek verileri okumak, saldırganın CSRF saldırılarına karşı savunmasız yöntemlerdir.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET mvc'de sahteciliğe karşı koruma belirteçleri

Sahteciliğe karşı koruma belirteçleri için bir Razor sayfası eklemek için **HtmlHelper.AntiForgeryToken** yardımcı yöntemi:

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

Bu yöntem, gizli form alanının ekler ve ayrıca tanımlama bilgisi belirteci ayarlar.

## <a name="anti-csrf-and-ajax"></a>Anti-CSRF ve AJAX

Form simgesi HTML form verileri JSON verilerini bir AJAX isteği gönderebilir AJAX istekleri için bir sorun olabilir. Tek bir çözüm, özel bir HTTP üst bilgisinde belirteçleri göndermektir. Aşağıdaki kod, belirteçleri oluşturmak için Razor sözdizimini kullanır ve ardından belirteçleri için bir AJAX isteği ekler. Çağırarak sunucuda oluşturulan belirteçleri **AntiForgery.GetTokens**.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

İsteği işlerken, istek üstbilgisi belirteçleri ayıklayın. Ardından çağırın **AntiForgery.Validate** belirteçleri doğrulamak için yöntemi. **Doğrulama** yöntemi belirteçleri geçerli değilse bir özel durum oluşturur.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
