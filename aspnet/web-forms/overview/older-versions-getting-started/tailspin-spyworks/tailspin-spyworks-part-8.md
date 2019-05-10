---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 'Bölüm 8: Son sayfalar, özel durum işleme ve sonuç | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 8. Bölüm sayfası ve özel durum hakkında bir kişi sayfası ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130598"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>Bölüm 8: Son Sayfalar, Özel Durum İşleme ve Sonuç

tarafından [ALi Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir. Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.
> 
> Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 8. Bölüm sayfası ve özel durum işleme hakkında bir kişi sayfası ekler. Dizi sonuç budur.

## <a id="_Toc260221680"></a>  İlgili kişi sayfası (ASP.NET postadan gönderme)

ContactUs.aspx adlı yeni bir sayfa oluşturun

Tasarımcı kullanarak, aşağıdaki form ToolkitScriptManager ve AjaxControlToolkit Düzenleyicisi denetiminden dahil edilecek özel not alma oluşturun. biçimindeki telefon numarasıdır.

![](tailspin-spyworks-part-8/_static/image1.jpg)

Dosyanın arkasındaki kodda bir click olay işleyicisi oluşturmak ve kişi bilgilerini bir e-posta göndermek için bir yöntem uygulamak için "Gönder" düğmesine çift tıklayın.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

Bu kod, web.config dosyanız posta göndermek için kullanılacak SMTP sunucusu belirten yapılandırma bölümünde bir giriş içermesini gerektirir.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  Sayfa hakkında

AboutUs.aspx adlı bir sayfa oluşturun ve dilediğiniz ne olursa olsun içeriği ekleyin.

## <a id="_Toc260221682"></a>  Genel özel durum işleyicisi

Son olarak, uygulamanın tamamında size özel durumlar ve başka bir öngörülemeyen durumlarda bu soğuk de web uygulamamızı neden işlenmeyen özel durumları.

Hiçbir zaman web site ziyaretçilerini görüntülenecek işlenmeyen bir özel durum istiyoruz.

![](tailspin-spyworks-part-8/_static/image2.jpg)

İşlenmeyen özel durumları saltanatı kullanıcı deneyimi olan dışında bir güvenlik sorunu da olabilir.

Bu sorunu çözmek için bir genel özel durum işleyicisi uygular.

Bunu yapmak için Global.asax dosyası açın ve aşağıdaki önceden oluşturulan olay işleyicisini unutmayın.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

Uygulama için kod ekleyin\_hata işleyicisi aşağıdaki gibi.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

Ardından Error.aspx çözüme adlı bir sayfa ekleyin ve bu biçimlendirme kod parçacığı ekleyin.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

Artık sayfasındaki\_hata iletileri olay işleyicisi ayıklama istek nesnesinden yükleme.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  Sonuç

ASP.NET WebForms kolaylaştırır olduğunu gördük veritabanı erişimi, üyelik, AJAX, Gelişmiş bir Web sitesi oluşturmak için vs. oldukça hızlı bir şekilde.

Umarım Bu öğretici, kendi ASP.NET WebForms uygulamalar oluşturmaya başlamak için ihtiyacınız olan araçları verdiği!

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-7.md)
