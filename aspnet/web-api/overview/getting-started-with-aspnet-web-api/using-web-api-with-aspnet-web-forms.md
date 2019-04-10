---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms ile - ASP.NET Web API kullanma 4.x
author: MikeWasson
description: Kodla Web API'si için bir ASP.NET Forms uygulaması için ASP.NET eklemek için adım adım öğretici 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422583"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET Web Forms ile Web API Kullanma

tarafından [Mike Wasson](https://github.com/MikeWasson)

Bu öğreticide, geleneksel bir ASP.NET Web Forms uygulaması ASP.NET Web API eklemek için adım adım anlatılmaktadır 4.x. 

## <a name="overview"></a>Genel Bakış

ASP.NET Web API, ASP.NET MVC ile paketlenmiştir olsa da, Web API'si için geleneksel bir ASP.NET Web Forms uygulaması eklemek kolay bir işlemdir.

Bir Web Forms uygulaması'nda Web API'sini kullanmak için iki ana adım vardır:

- Türetilen bir Web API denetleyicisi ekleme **ApiController** sınıfı.
- Bir rota tablosuna ekleme **uygulama\_Başlat** yöntemi.

## <a name="create-a-web-forms-project"></a>Web Forms projesi oluşturun

Visual Studio'yu başlatın ve seçin **yeni proje** gelen **Başlat** sayfası. Veya **dosya** menüsünde **yeni** ardından **proje**.

İçinde **şablonları** bölmesinde **yüklü şablonlar** genişletin **Visual C#** düğümü. Altında **Visual C#** seçin **Web**. Proje şablonları listesinde seçin **ASP.NET Web Forms uygulaması**. Proje için bir ad girin ve tıklayın **Tamam**.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>Model ve denetleyici oluşturma

Bu öğreticide aynı model ve denetleyici sınıflar olarak [Başlarken](tutorial-your-first-web-api.md) öğretici.

İlk olarak, bir model sınıfı ekleyin. İçinde **Çözüm Gezgini**, projeye sağ tıklayıp seçin **sınıfı Ekle**. ' % S'sınıfı ürün adı ve aşağıdaki uygulama ekleyin:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

Ardından, bir Web API denetleyicisi proje, A ekleyin. *denetleyicisi* Web API'si için HTTP isteklerini işleyen nesne.

İçinde **Çözüm Gezgini**, projeye sağ tıklayın. Seçin **Add New Item**.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

Altında **yüklü şablonlar**, genişletme **Visual C#** seçip **Web**. Şablonlar listesinden seçip **Web API denetleyici sınıfı**. Denetleyici "ProductsController" adını verin ve tıklayın **Ekle**.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**Yeni Öğe Ekle** Sihirbazı ProductsController.cs adlı bir dosya oluşturur. Sihirbaz dahil yöntemleri silin ve aşağıdaki yöntemleri ekleyin:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlarken](tutorial-your-first-web-api.md) öğretici.

## <a name="add-routing-information"></a>Yönlendirme bilgileri

Ardından, URI yolu şekilde ekleyeceğiz, bir URI'leri formun &quot;/API'si/ürünler/&quot; denetleyiciye yönlendirilir.

İçinde **Çözüm Gezgini**, Global.asax Global.asax.cs arka plan kod dosyasını açmak için çift tıklayın. Aşağıdaki **kullanarak** deyimi.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

Ardından aşağıdaki kodu ekleyin **uygulama\_Başlat** yöntemi:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

Yönlendirme tabloları hakkında daha fazla bilgi için bkz. [ASP.NET Web API'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="add-client-side-ajax"></a>İstemci tarafı AJAX ekleme

Tüm web istemcilerin erişebileceği bir API oluşturmak için gereken budur. Şimdi, API'yi çağırmak için jQuery kullanan bir HTML sayfası ekleyelim.

Ana sayfanıza emin olun (örneğin, *Site.Master*) içeren bir `ContentPlaceHolder` ile `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default.aspx dosyasını açın. Ana içerik bölümü Demirbaş metni gösterildiği gibi değiştirin:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

Ardından, jQuery kaynak dosyasına bir başvuru ekleyin `HeaderContent` bölümü:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

Not: Dosyadan sürükleyip bırakarak betik başvurusu kolayca ekleyebilirsiniz **Çözüm Gezgini** içine kod düzenleyicisi penceresi.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

Aşağıdaki komut dosyası bloğu jQuery komut dosyası etiketi ekleyin:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

Belge yüklendiğinde bu betik bir AJAX isteğinde bulunur. &quot;API/ürünleri&quot;. İstek, JSON biçiminde ürünlerin listesini döndürür. Betik, ürün bilgisi HTML tablosuna ekler.

Uygulamayı çalıştırdığınızda, şu şekilde görünmelidir:

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
