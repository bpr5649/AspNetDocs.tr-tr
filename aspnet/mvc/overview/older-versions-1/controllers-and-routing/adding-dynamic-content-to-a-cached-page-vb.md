---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Önbelleğe Alınmış Sayfaya Dinamik İçerik Ekleme (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Dinamik ve önbelleğe alınmış içeriği aynı sayfada nasıl karıştırırabilirsiniz öğrenin. Önbellek sonrası ikame, banner reklamları gibi dinamik içerik görüntülemenizi sağlar...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542267"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>Önbelleğe Alınmış Bir Sayfaya Dinamik İçerik Ekleme (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Dinamik ve önbelleğe alınmış içeriği aynı sayfada nasıl karıştırırabilirsiniz öğrenin. Önbellek sonrası değiştirme, önbelleğe alınmış bir sayfa içinde banner reklamları veya haber öğeleri gibi dinamik içerik görüntülemenize olanak tanır.

Çıktı önbelleğe alınmasından yararlanarak, bir ASP.NET MVC uygulamasının performansını önemli ölçüde artırabilirsiniz. Sayfa her seferinde bir sayfayı yeniden oluşturmak yerine, sayfa bir kez oluşturulabilir ve birden çok kullanıcı için bellekte önbelleğe alınabilir.

Ama bir sorun var. Sayfada dinamik içerik görüntülemeniz gerekiyorsa ne olur? Örneğin, sayfada bir banner reklamı görüntülemek istediğinizi düşünün. Her kullanıcıaynı reklamı görebilecek şekilde banner reklamının önbelleğe alınmasını istemezsinüz. Bu şekilde para kazanamazsın!

Neyse ki, kolay bir çözüm var. Önbellek *sonrası ikame*adı verilen ASP.NET çerçevesinin bir özelliğinden yararlanabilirsiniz. Önbellek sonrası değiştirme, bellekte önbelleğe alınmış bir sayfadaki dinamik içeriği değiştirmenize olanak tanır.

Normalde, &lt;OutputCache&gt; özniteliğini kullanarak bir sayfayı önbelleğe aldığınızda, sayfa hem sunucuda hem de istemcide (web tarayıcısı) önbelleğe alınır. Önbellek sonrası değiştirme kullandığınızda, bir sayfa yalnızca sunucuda önbelleğe alınır.

#### <a name="using-post-cache-substitution"></a>Önbellek Sonrası Değiştirme Kullanma

Önbellek sonrası ikame kullanmak iki adım gerektirir. İlk olarak, önbelleğe alınmış sayfada görüntülemek istediğiniz dinamik içeriği temsil eden bir dize döndüren bir yöntem tanımlamanız gerekir. Ardından, dinamik içeriği sayfaya enjekte etmek için HttpResponse.WriteSubstitution() yöntemini ararsınız.

Örneğin, önbelleğe alınmış bir sayfada farklı haber öğelerini rasgele görüntülemek istediğinizi düşünün. Listeleme 1'deki sınıf, üç haber öğesi listesinden rastgele bir haber öğesi döndüren RenderNews() adlı tek bir yöntemi ortaya çıkarır.

**Listeleme 1 – Modeller\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Önbellek sonrası ikameden yararlanmak için HttpResponse.WriteSubstitution() yöntemini ararsınız. WriteSubstitution() yöntemi, önbelleğe alınmış sayfanın bir bölgesini dinamik içerikle değiştirmek için kodu ayarlar. WriteSubstitution() yöntemi, Listeleme 2'deki görünümde rastgele haber öğesini görüntülemek için kullanılır.

**Listeleme 2 – Görünümler\Ana Sayfa\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

RenderNews yöntemi WriteSubstitution() yöntemine aktarılır. RenderNews yönteminin çağrılmadığını unutmayın. Bunun yerine yönteme bir başvuru AddressOf işleci yardımıyla WriteSubstitution() geçirilir.

Dizin görünümü önbelleğe alındı. Görünüm, Listeleme 3'teki denetleyici tarafından döndürülür. Dizin() eyleminin, Dizin &lt;görünümünün&gt; 60 saniye önbelleğe alınmasına neden olan bir OutputCache özniteliğiyle süslenmiş olduğuna dikkat edin.

**Listeleme 3 – Denetleyiciler\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

Dizin görünümü önbelleğe alınmış olsa da, Dizin sayfasını istediğinizde farklı rasgele haber öğeleri görüntülenir. Dizin sayfasını istediğinizde, sayfa tarafından görüntülenen süre 60 saniye boyunca değişmez (Bkz. Şekil 1). Zamanın değişmemesi, sayfanın önbelleğe alınmış olduğunu kanıtlıyor. Ancak, WriteSubstitution() yöntemi tarafından enjekte edilen içerik - rastgele haber öğesi – her istekle birlikte değişir.

**Şekil 1 - Önbelleğe alınmış bir sayfaya dinamik haber öğeleri enjekte etme**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Yardımcı Yöntemlerde Önbellek Sonrası Değiştirme Kullanma

Önbellek sonrası ikameden yararlanmanın daha kolay bir yolu, özel bir yardımcı yöntemi yle WriteSubstitution() yöntemine yapılan çağrıyı özetlemektir. Bu yaklaşım, Listeleme 4'teki yardımcı yöntemle gösterilmiştir.

**Listeleme 4 – Yardımcılar\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

Listeleme 4 iki yöntem ortaya bir Visual Basic modülü içerir: RenderBanner() ve RenderBannerInternal(). RenderBanner() yöntemi gerçek yardımcı yöntemini temsil eder. Bu yöntem, diğer yardımcı yöntem gibi html.RenderBanner() numaralı telefonu arayabilmeniz için standart ASP.NET MVC HtmlHelper sınıfını genişletir.

RenderBanner() yöntemi, HttpResponse.WriteSubstitution() yöntemini RenderBannerInternal() yöntemini WriteSubstitution() yöntemine geçirerek çağırır.

RenderBannerInternal() yöntemi özel bir yöntemdir. Bu yöntem yardımcı yöntem olarak açıklanamaz. RenderBannerInternal() yöntemi rasgele üç afiş reklam görüntüleri bir listeden bir afiş reklam görüntü döndürür.

Listeleme 5'teki değiştirilmiş Dizin görünümü, RenderBanner yardımcı yöntemini nasıl kullanabileceğinizi gösterir. MvcApplication1.Helpers ad alanını almak için görünümün en üstünde ek &lt;bir %@ Alma %&gt; yönergesinin ek olarak yer aldığına dikkat edin. Bu ad alanını almamayı ihmal ederseniz, RenderBanner() yöntemi Html özelliğinde bir yöntem olarak görünmez.

**Listeleme 5 – Görünümler\Home\Index.aspx (RenderBanner() yöntemi ile)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Listeleme 5'teki görünümtarafından işlenen sayfayı istediğinizde, her istekle birlikte farklı bir banner reklamı görüntülenir (Bkz. Şekil 2). Sayfa önbelleğe alınmış, ancak banner reklam RenderBanner() yardımcı yöntemi tarafından dinamik olarak enjekte edilir.

**Şekil 2 – Rasgele bir banner reklamı gösteren Dizin görünümü**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Özet

Bu öğretici, önbelleğe alınmış bir sayfadaki içeriği dinamik olarak nasıl güncelleştirebileceğinizi açıklamıştır. Önbelleğe alınmış bir sayfaya dinamik içeriğin enjekte edilmesini sağlamak için HttpResponse.WriteSubstitution() yöntemini kullanmayı öğrendiniz. Ayrıca, bir HTML yardımcı yöntemi içinde WriteSubstitution() yöntemine çağrıyı nasıl kapsüllediğinizi de öğrendiniz.

Mümkün olduğunda önbelleğe alma avantajından yararlanın – web uygulamalarınızın performansı üzerinde dramatik bir etkisi olabilir. Bu öğreticide açıklandığı gibi, sayfalarınızda dinamik içerik görüntülemeniz gerektiğinde bile önbelleğe alma avantajından yararlanabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](improving-performance-with-output-caching-vb.md)
> [Sonraki](creating-a-controller-vb.md)
