---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'Bölüm 3: Düzen ve kategori menüsü | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 3. Bölüm ekleyerek düzen ve kategori menüsü kapsar.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: f55b29a271dbdb72d3e2249ed74517b77d78cf5e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069075"
---
<a name="part-3-layout-and-category-menu"></a>Bölüm 3: Düzen ve Kategori Menüsü
====================
tarafından [ALi Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir. Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.
> 
> Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 3. Bölüm ekleyerek düzen ve kategori menüsü kapsar.


## <a id="_Toc260221669"></a>  Bazı düzen ve kategori menüsü ekleme

Bizim ürün kategori menüsü içerecek sol tarafındaki sütunun bir div bizim site ana sayfa ekleyeceğiz.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

Bizim Style.css dosyasına ekledik CSS sınıfı tarafından istenen hizalama ve diğer biçimlendirme sağlanacağını unutmayın.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

Ürün kategorisi menüsünden mevcut ürün kategorilerini ve menü öğeleri oluşturma ve karşılık gelen bağlantıları için ticaret veritabanını sorgulayarak çalışma zamanında dinamik olarak oluşturulur.

Bunu gerçekleştirmek için'de iki ASP kullanacağız. NET güçlü veri denetimleri. "Varlık veri kaynağı" ve "ListView" denetimi.

![](tailspin-spyworks-part-3/_static/image1.jpg)

Şimdi "Tasarım görünümüne" ve Yardımcıları bizim denetimlerini yapılandırmak için kullanın.

![](tailspin-spyworks-part-3/_static/image2.jpg)

EntityDataSource ID özelliği için EDS ayarlayalım\_kategori\_menüsüne ve ardından "Veri kaynağı yapılandırma".

![](tailspin-spyworks-part-3/_static/image3.jpg)

Ticaret veritabanımızdaki varlık veri kaynağı modeli oluşturduk, bizim için oluşturulmuş CommerceEntities bağlantıyı seçin ve "İleri" ye tıklayın.

![](tailspin-spyworks-part-3/_static/image4.jpg)

"Kategoriler" varlık kümesinin adını seçin ve diğer seçenekleri varsayılan olarak bırakın. "Son" düğmesini tıklatın.

Şimdi biz sayfamıza ListView yerleştirilen ListView denetimi örneği ID özelliği ayarlayalım\_ProductsMenu ve kendi Yardımcısı'nı etkinleştirin.

![](tailspin-spyworks-part-3/_static/image5.jpg)

Ancak Denetim seçenekleri veri öğesi görünen biçimlendirmek için kullanabiliriz ve biz Kaynak Görünümü'nde kod gireceksiniz biçimlendirme, bizim menü oluşturma yalnızca basit biçimlendirme gerektirir.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

"Eval satırını" deyimi lütfen unutmayın: &lt;% # Eval("CategoryName") %&gt;

ASP.NET sözdizimini &lt;% # %&gt; ne içerdiği ve sonuçları "satır" çıkış yürütmek için çalışma zamanı yönlendiren bir toplu kuralıdır.

Bildirir Eval("CategoryName") deyim veri öğelerinin ilişkili koleksiyon geçerli girişi için "CatagoryName" varlık modeli öğe adları değerini getirir. Bu çok güçlü bir özellik kısa sözdizimi aşağıdaki gibidir.

Şimdi uygulamayı çalıştıralım.

![](tailspin-spyworks-part-3/_static/image6.jpg)

Bizim ürün kategori menüsü artık görüntülenir ve ProductsList.aspx adlı zaman biz biz menü öğesi bağlantı noktalarına henüz uygulamak için sahip olduğumuz bir sayfa görebilirsiniz kategori menü öğelerinden birinin üzerine gelin ve dinamik sorgu dizesi bağımsız değişkeni, derledik olduğunu içerdiğini unutmayın  Kategori Kimliği.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-2.md)
> [İleri](tailspin-spyworks-part-4.md)
