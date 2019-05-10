---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter ile ASP.NET Web sayfaları Yardımcısı | Microsoft Docs
author: Rick-Anderson
description: Bu konu başlığında ve uygulama bir Twitter Yardımcısı, WebMatrix 3'ü projenize ekleme işlemini göstermektedir. Twitter Yardımcısı kodunu içerir ve yardımcı çağırma gösterilmektedir...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132764"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET Web Sayfaları ile Twitter Yardımcısı

tarafından [Tom FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Twitter Yardımcıları kullanım dışıdır. Twitter'ın en son engagement araçları için Web siteleri için bkz: [Twitter için Web siteleri genel bakış](https://developer.twitter.com/en/docs/twitter-for-websites/overview).

> Bu konu başlığında ve uygulama bir Twitter Yardımcısı, WebMatrix 3'ü projenize ekleme işlemini göstermektedir. Twitter Yardımcısı kodunu içerir ve yardımcı yöntemleri çağırma gösterilmektedir.
> 
> Twitter.cshtml dosyası için bu kodu tarafından geliştirilmiştir **Tian Pan** Microsoft.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Bu öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğreticide, ASP.NET Web Pages 2 ile de çalışır.

## <a name="introduction"></a>Giriş

Bu konuda, bir Twitter Yardımcısı uygulamanıza ekleyin ve yardımcı yöntemlerini çağırmak için Razor sözdizimini kullanan gösterilmektedir. Twitter Yardımcısı, Twitter düğmeler ve uygulamanızdaki pencere öğeleri bir araya kolaylaştırır. Bir kullanıcının zaman çizelgesinde veya diyez etiketi için arama sonuçları gibi bir Twitter pencere öğesini kullanmak için öncelikle oluşturmanız gerekir [pencere öğesi Twitter'da](https://twitter.com/settings/widgets). Pencere öğenizi oluşturduktan sonra bir pencere öğesi kimliği alırsınız. Pencere öğesi Göster yardımcı yöntemler ararken Bu pencere öğesi kimliği bir parametre olarak geçiriyoruz.

Bu konu başlığında, Twitter API'si 1.1 sürümü alınmaktadır. Projenize doğrudan Twitter Yardımcısı kod ekleyerek, Twitter API'si değişirse yardımcı kod güncelleştirebilirsiniz.

Webmatrix'i yükleme hakkında daha fazla bilgi için bkz: [Karşınızda ASP.NET Web sayfaları Başlarken 2 -](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).

## <a name="add-twitter-helper-to-your-project"></a>Twitter Yardımcısı projenize ekleyin.

Twitter Yardımcısı eklemek için ilk olarak, adlı bir klasör ekleyin **uygulama\_kod** projenize. Adlı bir dosya oluşturup **Twitter.cshtml**.

![App_Code klasörü](twitter-helper/_static/image1.png)

Twitter.cshtml varsayılan kodu aşağıdaki kodla değiştirin.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>Web sayfalarınızdan twitter yöntemlerini çağırın

Aşağıdaki örnek, projenizde sayfasından Twitter yardımcı yöntemler kullanmayı gösterir. Projenizde, ihtiyaçlarınıza uygun olan değerleri içeren parametre değerlerini değiştirmek istersiniz. Yöntemleri nasıl keşfetmek için sağlanan pencere öğesi kimlikleri kullanabilirsiniz, ancak projeniz için kendi pencere öğelerinizi oluşturmak isteyeceksiniz.

Aşağıda gösterilen parametrelerin tümü gereklidir. İsteğe bağlı parametreler, bir düğme veya pencere öğesi nasıl görüntüleneceğini özelleştirmek için kullanılır. Örneğin, İzle düğmesine izlemek için kullanıcı adı yalnızca gerektiriyor, ancak örnek takipçi sayısı eklemek nasıl düğmesi ve dilin boyutunu belirlemek nasıl gösterir.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>Sonuçları göster

Yukarıdaki kod, aşağıdaki düğmeler ve pencere öğeleri oluşturur. Bu düğmeler ve pencere öğeleri tam işlevsel, ekran görüntüleri değil. Dili için parametre olarak ayarlanmış olduğu için İspanyolca izleyin düğmesi görüntülenir **es**.

### <a name="follow-button"></a>Düğme izleyin

[İzleyin @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>Tweet düğmesi

[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>Kullanıcı zaman çizelgesini (Profil)

[Seçtiği tweet'ler: @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>Sık Kullanılanlar

[Sık kullanılan seçtiği Tweet'ler: @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>List

[Gelen bir tweet @Microsoft/MS \_tüketici\_bantları](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>Ara

[İlgili bir tweet &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
