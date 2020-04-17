---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Ana Sayfaları Görüntüle ile Sayfa Düzenleri Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticide, ana sayfaları görüntüleyerek uygulamanızdaki birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğrenirsiniz. Bir kullanabilirsiniz ...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542501"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>Görünüm Ana Sayfalarıyla Sayfa Düzenleri Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> Bu öğreticide, ana sayfaları görüntüleyerek uygulamanızdaki birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğrenirsiniz. Örneğin, iki sütunlu bir sayfa düzenini tanımlamak ve web uygulamanızdaki tüm sayfalar için iki sütunlu düzeni kullanmak için bir görünüm ana sayfası kullanabilirsiniz.

## <a name="creating-page-layouts-with-view-master-pages"></a>Ana Sayfaları Görüntüle ile Sayfa Düzenleri Oluşturma

Bu öğreticide, ana sayfaları görüntüleyerek uygulamanızdaki birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğrenirsiniz. Örneğin, iki sütunlu bir sayfa düzenini tanımlamak ve web uygulamanızdaki tüm sayfalar için iki sütunlu düzeni kullanmak için bir görünüm ana sayfası kullanabilirsiniz.

Ayrıca, uygulamanızdaki birden çok sayfada ortak içeriği paylaşmak için ana sayfaları görüntüleme avantajından da yararlanabilirsiniz. Örneğin, web sitenizin logosunu, gezinme bağlantılarını ve banner reklamlarınızı bir görünüm ana sayfasına yerleştirebilirsiniz. Bu şekilde, uygulamanızdaki her sayfa bu içeriği otomatik olarak görüntüler.

Bu öğreticide, yeni bir görünüm ana sayfası oluşturmayı ve ana sayfayı temel alan yeni bir görünüm içeriği sayfası oluşturmayı öğrenirsiniz.

### <a name="creating-a-view-master-page"></a>Görünüm Ana Sayfası Oluşturma

İki sütunlu düzeni tanımlayan bir görünüm ana sayfası oluşturarak başlayalım. Görünümler\Paylaşılan klasörüne sağ tıklayarak, **Ekle, Yeni Öğe**ve MVC Görünüm Ana Sayfa şablonu seçeneğini seçerek MVC projesine yeni bir görünüm ana sayfası eklersiniz (Bkz. Şekil 1).

[![Görünüm ana sayfası ekleme](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**Şekil 01**: Görünüm ana sayfası ekleme ([Tam boyutlu resmi görüntülemek için tıklayınız](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))

Bir uygulamada birden fazla görünüm ana sayfası oluşturabilirsiniz. Her görünüm ana sayfası farklı bir sayfa düzeni tanımlayabilir. Örneğin, belirli sayfaların iki sütunlu düzeni ve diğer sayfaların üç sütunlu düzeni olmasını isteyebilirsiniz.

Görünüm ana sayfası standart ASP.NET MVC görünümüne çok benzer. Ancak, normal görünümün aksine, görünüm ana `<asp:ContentPlaceHolder>` sayfası bir veya daha fazla etiket içerir. Etiketler, `<contentplaceholder>` ana sayfanın tek bir içerik sayfasında geçersiz kılınabilecek alanlarını işaretlemek için kullanılır.

Örneğin, Listeleme 1'deki görünüm ana sayfası iki sütunlu düzeni tanımlar. İki `<contentplaceholder>` etiket içeriyor. Her `<ContentPlaceHolder>` sütun için bir tane.

**İlan 1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

Listeleme 1'deki görünüm ana sayfasının gövdesi, iki sütuna karşılık gelen iki `<div>` etiket içerir. Basamaklı Stil Sayfası sütun sınıfı her `<div>` iki etikete de uygulanır. Bu sınıf, ana sayfanın üst kısmında bildirilen stil sayfasında tanımlanır. Tasarım görünümüne geçerek görünüm ana sayfasının nasıl oluşturulacağını önizleyebilirsiniz. Kaynak kod düzenleyicisinin sol alt kısmındaki Tasarım sekmesini tıklatın (Bkz. Şekil 2).

[![Tasarımcıda ana sayfaönizleme](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**Şekil 02**: Tasarımcıda bir ana sayfanın önizlemesi ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))

### <a name="creating-a-view-content-page"></a>Görünüm İçerik Sayfası Oluşturma

Bir görünüm ana sayfası oluşturduktan sonra, görünüm ana sayfasına göre bir veya daha fazla görünüm içerik sayfası oluşturabilirsiniz. Örneğin, Görünümler\Ana klasörüne sağ tıklayarak, **Ekle, Yeni Öğe,** **MVC Görünüm İçerik Sayfası** şablonu seçeneğini seçerek, Index.aspx adını girerek ve Ekle düğmesini tıklatarak Ana Sayfa denetleyicisi için Bir Dizin görünümü içerik sayfası oluşturabilirsiniz (Bkz. Şekil 3).

[![Görünüm içeriği sayfası ekleme](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**Şekil 03**: Görünüm içerik sayfası ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))

Ekle düğmesini tıklattıktan sonra, görünüm içeriği sayfasıyla ilişkilendirmek için bir görünüm ana sayfası seçmenize olanak tanıyan yeni bir iletişim kutusu görüntülenir (Bkz. Şekil 4). Bir önceki bölümde oluşturduğumuz Site.master görünüm ana sayfasına gidebilirsiniz.

[![Ana sayfa seçme](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**Şekil 04**: Ana sayfa seçme ([Tam boyutlu resmi görüntülemek için tıklayınız](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))

Site.master ana sayfasına dayalı yeni bir görünüm içerik sayfası oluşturduktan sonra, dosyayı Listeleme 2'de alırsınız.

**Listeleme 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

Bu görünümün, `<asp:Content>` görünüm ana sayfasındaki `<asp:ContentPlaceHolder>` etiketlerin her birine karşılık gelen bir etiket içerdiğine dikkat edin. Her `<asp:Content>` etiket, geçersiz kıladığı özelliğe `<asp:ContentPlaceHolder>` işaret eden bir ContentPlaceHolderID özniteliği içerir.

Ayrıca, Listeleme 2'deki içerik görüntüleme sayfasının normal açılış ve kapanış HTML etiketlerinden hiçbirini içermediğine dikkat edin. Örneğin, açma ve kapatma `<html>` veya `<head>` etiketleri içermez. Normal açılış ve kapanış etiketlerinin tümü görünüm ana sayfasında bulunur.

Görünüm içerik sayfasında görüntülemek istediğiniz tüm içerikler etiketin `<asp:Content>` içine yerleştirilmelidir. Bu etiketlerin dışına herhangi bir HTML veya başka içerik yerseniz, sayfayı görüntülemeye çalıştığınızda bir hata alırsınız.

İçerik görüntüleme sayfasındaki ana `<asp:ContentPlaceHolder>` sayfadaki her etiketi geçersiz kılmanız gerekmez. Etiketi yalnızca belirli içerikle değiştirmek istediğinizde bir `<asp:ContentPlaceHolder>` etiketi geçersiz kılmanız gerekir.

Örneğin, Listeleme 3'teki değiştirilmiş Dizin görünümü yalnızca iki `<asp:Content>` etiket içerir. Etiketlerin `<asp:Content>` her biri bazı metin içerir.

**İlan 3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

Listeleme 3'teki görünüm istendiğinde, sayfayı Şekil 5'te işler. Görünümün iki sütunlu bir sayfa yı işlettiğine dikkat edin. Ayrıca, görünüm içeriği sayfasındaki içeriğin görünüm ana sayfasındaki içerikle birleştirilen içeriğe dikkat edin.

[![Dizin görünümü içerik sayfası](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**Şekil 05**: Dizin görünümü içerik sayfası ([Tam boyutlu resmi görüntülemek için tıklayınız](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>Ana Sayfa İçeriğini Görüntüle

Görünüm ana sayfalarıyla çalışırken hemen karşılaştığınız bir sorun, farklı görünüm içerik sayfaları istendiğinde ana sayfa içeriğini görüntüleme sorunudur. Örneğin, web uygulamanızdaki her sayfanın benzersiz bir başlığa sahip olmasını istiyorsunuz. Ancak, başlık görünüm içeriği sayfasında değil, görünüm ana sayfasında bildirilir. Peki, her görünüm içeriği sayfası için sayfa başlığını nasıl özelleştirebilirsiniz?

Görünüm içeriği sayfası tarafından görüntülenen başlığı değiştirmenin iki yolu vardır. İlk olarak, bir görünüm içeriği sayfasının üst `<%@ page %>` kısmında bildirilen yönergenin başlık özniteliğine bir sayfa başlığı atayabilirsiniz. Örneğin, "Süper Harika Web Sitesi" sayfabaşlığını Dizin görünümüne atamak istiyorsanız, Dizin görünümünün üst bölümüne aşağıdaki yönergeyi ekleyebilirsiniz:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

Dizin görünümü tarayıcıya işlendiğinde, istenen başlık tarayıcı başlık çubuğunda görünür:

[![Tarayıcı başlık çubuğu](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

Başlık özniteliğinin çalışabilmesi için ana görünüm sayfasının karşılaması gereken önemli bir gereksinim vardır. Görünüm ana sayfası üstbilgi için `<head runat="server">` normal `<head>` bir etiket yerine bir etiket içermelidir. `<head>` Etiket runat="server" özniteliğini içermiyorsa, başlık görünmez. Varsayılan görünüm ana sayfası `<head runat="server">` gerekli etiketi içerir.

Ana sayfa içeriğini tek bir görünüm içeriği sayfasından değiştirmek için alternatif bir yaklaşım, `<asp:ContentPlaceHolder>` değiştirmek istediğiniz bölgeyi bir etikette kaydırmaktır. Örneğin, yalnızca başlığı değil, aynı zamanda ana görünüm sayfası tarafından işlenen meta etiketlerini de değiştirmek istediğinizi düşünün. Listeleme 4'teki ana `<asp:ContentPlaceHolder>` görünüm sayfası `<head>` etiketinde bir etiket içerir.

**İlan 4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

Listeleme `<asp:ContentPlaceHolder>` 4'teki etiketin varsayılan içeriği içerdiğine dikkat edin: varsayılan başlık ve varsayılan meta etiketleri. Bu `<asp:ContentPlaceHolder>` etiketi tek bir görüntüleme içeriği sayfasında geçersiz kılmazsanız, varsayılan içerik görüntülenir.

Listeleme 5'teki içerik görüntüleme `<asp:ContentPlaceHolder>` sayfası, özel bir başlık ve özel meta etiketleri görüntülemek için etiketi geçersiz kılar.

**İlan 5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>Özet

Bu öğretici, ana sayfaları görüntülemek ve içerik sayfalarını görüntülemek için temel bir giriş sağlar. Yeni görünüm ana sayfaları oluşturmayı ve bunlara dayalı görünüm içerik sayfaları oluşturmayı öğrendiniz. Ayrıca, belirli bir görünüm içeriği sayfasından bir görünüm ana sayfasının içeriğini nasıl değiştirebileceğinizi de inceledik.

> [!div class="step-by-step"]
> [Önceki](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [Sonraki](passing-data-to-view-master-pages-vb.md)
