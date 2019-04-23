---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: Denetleyici (C#) oluşturma | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther bir denetleyici bir ASP.NET MVC uygulamasına nasıl ekleyebileceğinizi gösterir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: c92d7cdeb7b2d31d5eca810628e9f563840f7494
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400621"
---
# <a name="creating-a-controller-c"></a>Denetleyici Oluşturma (C#)

tarafından [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Stephen Walther bir denetleyici bir ASP.NET MVC uygulamasına nasıl ekleyebileceğinizi gösterir.


Bu öğreticinin amacı, yeni ASP.NET MVC denetleyicileri nasıl oluşturabileceğinizi açıklar sağlamaktır. Visual Studio denetleyici Ekle menü seçeneğini kullanarak hem bir sınıf dosyası el ile oluşturarak denetleyicileri oluşturmayı öğrenin.

### <a name="using-the-add-controller-menu-option"></a>Kullanarak denetleyici menü seçeneği ekleyin

Visual Studio Çözüm Gezgini penceresinde denetleyicileri klasörü sağ tıklatın ve seçin için yeni bir denetleyicisi oluşturmak için en kolay yolu olan **Ekle, denetleyici** menü seçeneği (bkz. Şekil 1). Bu menü seçeneğini belirleyerek açılır **denetleyici Ekle** iletişim (bkz: Şekil 2).


[![Yeni Proje iletişim kutusu](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**Şekil 01**: Yeni denetleyici ekleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image2.png))


[![Yeni Proje iletişim kutusu](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**Şekil 02**: Denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image4.png))


Denetleyici adının ilk bölümü vurgulanan bildirimi **denetleyici Ekle** iletişim. Her Denetleyici adı soneki ile sona ermelidir *denetleyicisi*. Örneğin, adında bir denetleyici oluşturabilirsiniz *ProductController* ancak adlı bir denetleyici *ürün*.


Eksik bir denetleyici oluşturursanız *denetleyicisi* denetleyici çağrılacak mümkün olmayacaktır sonra soneki. Bunu yapmayın--bu hata yaptıktan sonra doğduğum sayısız saatler boşa.


**1 - Controllers\ProductController.cs listeleme**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

Her zaman denetleyicileri klasöründe denetleyicileri oluşturmanız gerekir. Aksi takdirde, ASP.NET MVC kurallarını ihlal ve diğer geliştiriciler, uygulamanızın anlamak daha zor bir zaman alacaktır.

### <a name="scaffolding-action-methods"></a>Yapı iskelesi eylem yöntemleri

Bir denetleyici oluşturduğunuzda, oluşturma, güncelleştirme ve ayrıntıları eylem yöntemlerine otomatik olarak oluşturma seçeneğiniz vardır (bkz: Şekil 3). Ardından bu seçeneği belirlerseniz listeleme 2 controller sınıfında oluşturulur.


[![Eylem yöntemlerine otomatik olarak oluşturma](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**Şekil 03**: Eylem yöntemlerine otomatik olarak oluşturma ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image6.png))


**2 - Controllers\CustomerController.cs listeleme**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

Saptama yöntemleri bu oluşturulan yöntemlerdir. Oluşturma, güncelleştirme ve kendiniz için bir müşterinin ayrıntılarını gösteren fiili mantığı eklemeniz gerekir. Ancak, saptama yöntemleri ile güzel bir başlangıç noktası sağlar.

### <a name="creating-a-controller-class"></a>Denetleyici sınıfı oluşturma

ASP.NET MVC denetleyicisi, yalnızca bir sınıf değil. İsterseniz, uygun Visual Studio denetleyicisi iskele yoksaymak ve el ile bir denetleyici sınıfı oluşturun. Aşağıdaki adımları uygulayın:

1. Menü seçeneği denetleyicileri klasörüne sağ tıklayıp **Ekle, yeni öğe** seçip **sınıfı** şablonu (bkz: Şekil 4).
2. Yeni bir sınıf PersonController.cs adlandırın ve tıklatın **Ekle** düğmesi.
3. Temel System.Web.Mvc.Controller sınıfından (3 listeleme bakın) sınıfından devralan elde edilen sınıf dosyasını değiştirin.


[![Yeni bir sınıf oluşturma](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**Şekil 04**: Yeni bir sınıf oluşturursunuz ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image8.png))


**Listing 3 - Controllers\PersonController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

Denetleyici listeleme 3'te, "Hello World!" dizesini döndürür İNDİS() adlı bir eylem kullanıma sunar. Bu denetleyici eylemi, uygulamanızı çalıştıran ve aşağıdaki gibi bir URL isteyen çağırabilirsiniz:

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET Geliştirme Sunucusu bir rastgele bağlantı noktası numarası (örneğin, 40071) kullanır. Bir denetleyici çağırmak için bir URL girerken, doğru bağlantı noktası numarası girmeniz gerekir. ASP.NET Geliştirme Sunucusu (sağ alt ekranınızın) Windows bildirim alanındaki simgenin üzerine farenizi gelerek, bağlantı noktası numarasını belirleyebilirsiniz.
> 
> [!div class="step-by-step"]
> [Önceki](adding-dynamic-content-to-a-cached-page-cs.md)
> [İleri](creating-an-action-cs.md)
