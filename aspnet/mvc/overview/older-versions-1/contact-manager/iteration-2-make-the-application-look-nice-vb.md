---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 'Yineleme #2 – Uygulamanın güzel görünmesini sağla (VB) | Microsoft Dokümanlar'
author: rick-anderson
description: Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a97958db442c48bd696f6414f7226127984bc34
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542436"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>2. Yineleme – Uygulamanın güzel görünmesini sağlama (VB)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (VB)

Öğreticiler bu dizi, biz baştan sona tüm Bir İletişim Yönetimi uygulaması oluşturmak. İletişim Yöneticisi uygulaması, kişi listesi için kişi bilgilerini (adlar, telefon numaraları ve e-posta adresleri) depolamanızı sağlar.

Uygulamayı birden çok yineleme üzerine oluşturuyoruz. Her yineleme ile, yavaş yavaş uygulama geliştirmek. Bu çoklu yineleme yaklaşımının amacı, her değişikliğin nedenini anlamanızı sağlamaktır.

- Yineleme #1 – Uygulamayı oluşturun. İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

- Yineleme #2 - Uygulama güzel görünmesini sağlamak. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

- Yineleme #3 – Form doğrulama ekle. Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

- Yineleme #4 – Uygulamayı gevşek bir şekilde biraraya getirin. Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

- Yineleme #5 – Birim testleri oluşturun. Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

- Yineleme #6 – Test odaklı geliştirmeyi kullanın. Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

- Yineleme #7 – Ajax işlevselliğini ekleyin. Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="this-iteration"></a>Bu Yineleme

Bu yinelemenin amacı, İletişim Yöneticisi uygulamasının görünümünü iyileştirmektir. Şu anda, Kişi Yöneticisi varsayılan ASP.NET MVC görünüm ana sayfası ve basamaklı stil sayfasını kullanır (Bkz. Şekil 1). Bu kötü görünmüyor, ama Contact Manager her ASP.NET MVC web sitesi gibi görünmesini istemiyorum. Bu dosyaları özel dosyalarla değiştirmek istiyorum.

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**Şekil 01**: ASP.NET bir MVC Uygulamasının varsayılan görünümü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image2.png))

Bu yinelemede, uygulamamızın görsel tasarımını geliştirmek için iki yaklaşımı tartışıyorum. İlk olarak, nasıl ücretsiz bir ASP.NET MVC tasarım şablonu indirmek için ASP.NET MVC Tasarım galerisi yararlanmak için gösterir. ASP.NET MVC Tasarım galerisi herhangi bir iş yapmadan profesyonel bir web uygulaması oluşturmanıza olanak sağlar.

İletişim Yöneticisi uygulaması için ASP.NET MVC Tasarım galerisinden bir şablon kullanmamaya karar verdim. Bunun yerine, profesyonel bir tasarım firması tarafından oluşturulan özel bir tasarım vardı. Bu öğreticinin ikinci bölümünde, ben nasıl profesyonel bir tasarım şirketi ile son ASP.NET MVC tasarım oluşturmak için çalıştı açıklar.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC Tasarım Galerisi

mvc tasarım galerisi ASP.NET, Microsoft tarafından sağlanan ücretsiz bir kaynaktır. mvc galerisi ASP.NET aşağıdaki adreste yer almaktadır:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC Tasarım Galerisi, ASP.NET bir MVC projesinde kullanılmak için özel olarak oluşturulmuş ücretsiz web sitesi tasarımlarından oluşan bir koleksiyona ev sahipliği yapmaktadır. Tasarımlar topluluk üyeleri tarafından yüklenir. Galeriyi ziyaret edenler en sevdikleri tasarımlara oy verebilirler (Bkz. Şekil 2).

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**Şekil 02**: mvc tasarım galerisi ASP.NET ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image4.png))

Ben bu öğretici yazmak gibi, galeride en popüler tasarım David Hauser tarafından Ekim adlı bir tasarımdır. Aşağıdaki adımları tamamlayarak bu tasarımı ASP.NET bir MVC projesi için kullanabilirsiniz:

1. October.zip dosyasını bilgisayarınıza indirmek için **İndir** düğmesini tıklatın.
2. İndirilen October.zip dosyasına sağ tıklayın ve **Engeli Kaldır** düğmesini tıklatın (Bkz. Şekil 3).
3. Dosyayı Ekim adlı bir klasöre açın.
4. Ekim klasöründe bulunan DesignTemplate klasöründeki tüm dosyaları seçin, dosyalara sağ tıklayın ve menü **seçeneğini**kopyala seçeneğini seçin.
5. Visual Studio Solution Explorer penceresindeki ContactManager proje düğümüne sağ tıklayın ve menü seçeneği **Yapıştır'ı** seçin (Bkz. Şekil 4).
6. Visual Studio menü seçeneğini **seçin, Bul ve Değiştir, Hızlı Değiştir** ve *[MyProjectName]* ile *ContactManager* ile değiştirin (Bkz. Şekil 5).

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**Şekil 03**: Web'den indirilen bir dosyanın engelini kaldırma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image6.png))

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**Şekil 04**: Çözüm Gezgini'nde dosyaların üzerine yazma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image8.png))

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**Şekil 05**: ContactManager ile [ProjectName] değiştirme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image10.png))

Bu adımları tamamladıktan sonra, web uygulamanız yeni tasarımı kullanır. Şekil 6'daki sayfa, Ekim tasarımıyla Birlikte İletişim Yöneticisi uygulamasının görünümünü göstermektedir.

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**Şekil 06**: Ekim şablonu ile ContactManager ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>MVC Tasarımına Özel ASP.NET Oluşturma

ASP.NET MVC Tasarım Galerisi farklı tasarım stilleri iyi bir seçim vardır. Galeri, ASP.NET MVC uygulamalarınızın görünümünü özelleştirmek için size ağrısız bir yol sunar. Ve, tabii ki, Galeri tamamen özgür olmanın büyük bir avantaja sahiptir.

Ancak, web siteniz için tamamen benzersiz bir tasarım oluşturmanız gerekebilir. Bu durumda, bir web sitesi tasarım şirketi ile çalışmak mantıklı. İletişim Yöneticisi uygulaması için tasarım için bu yaklaşımı almaya karar verdim.

Yineleme #1'ndeki İletişim Yöneticisi'ni sıkıştırdım ve projeyi tasarım şirketine gönderdim. Onlar Visual Studio (onlara utanç!) kendi değildi, ama bir sorun mevcut değildi. Microsoft Visual Web Developer'ı [https://www.asp.net](https://www.asp.net) web sitesinden ücretsiz olarak indirebildiler ve Visual Web Developer'da İletişim Yöneticisi uygulamasını açtılar. Birkaç gün içinde, şekil 7'deki tasarımı ürettiler.

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**Şekil 07**: MVC İletişim Yöneticisi Tasarımı ASP.NET ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-2-make-the-application-look-nice-vb/_static/image14.png))

Yeni tasarım iki ana dosyadan oluşuyordu: yeni bir basamaklı stil sayfası dosyası ve yeni bir görünüm ana sayfa dosyası. Görünüm ana sayfası, ASP.NET bir MVC uygulamasında görünümlerin düzenini ve paylaşılan içeriğini içerir. Örneğin, görünüm ana sayfası Şekil 7'de görünen üstbilgi, gezinti sekmeleri ve altbilgi içerir. Tasarım şirketinden yeni Site.Master dosyası ile Görünümler\Paylaşılan klasöründeki mevcut Site.Master görünüm ana sayfasını yazdım,

Tasarım şirketi ayrıca yeni bir basamaklı stil sayfası ve görüntü kümesi oluşturdu. Bu yeni dosyaları İçerik klasörüne yerleştirdim ve varolan Site.css dosyasını yazdım. Tüm statik içeriği İçerik klasörüne yerleştirmelisiniz.

İlgili Kişi Yöneticisi'nin yeni tasarımının kişileri düzenlemek ve silen görüntüler içerdiğine dikkat edin. Kişilerin HTML tablosundaki her ilgili nin yanında bir Düzenle ve Sil görüntüsü görünür.

Başlangıçta, HTML ile işlenen bu bağlantılar. ActionLink() aşağıdaki gibi yardımcı:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() yöntemi görüntüleri desteklemez (HTML yöntemi güvenlik nedenleriyle bağlantı metnini kodlar). Bu nedenle, Html.ActionLink() çağrıları url.action() çağrıları ile değiştirdim:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink() yöntemi tüm HTML köprülerini işler. Url.Action() yöntemi ise etiketi olmayan &lt;&gt; sadece URL'yi işler.

Ayrıca, yeni tasarımın hem seçili hem de seçilmemiş sekmeleri içerdiğine dikkat edin. Örneğin, Şekil 8'de **Yeni İlgili Kişi Oluştur** sekmesi seçilir ve **Kişilerim** sekmesi seçilmez.

[![Yeni Proje iletişim kutusu](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**Şekil 08**: Seçili ve seçilmemiş sekmeler([Tam boyutlu görüntüyü görüntülemek için tıklayınız)](iteration-2-make-the-application-look-nice-vb/_static/image16.png)

Seçili ve seçilmemiş sekmeleri oluşturmayı desteklemek için MenuItemHelper adında özel bir HTML yardımcısı oluşturdum. Bu yardımcı yöntem, geçerli &lt;&gt; denetleyici ve &lt;eylemin yardımcıya&gt; geçirilen denetleyici ve eylem adına karşılık gelip gelmediğine bağlı olarak li etiketi veya li sınıfı="seçilmiş" etiketini işler. MenuItemHelper'ın kodu Listeleme 1'de bulunur.

**Listeleme 1 – Yardımcılar\MenuItemHelper.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper, li&gt; HTML etiketini oluşturmak &lt;için dahili olarak TagBuilder sınıfını kullanır. TagBuilder sınıfı, yeni bir HTML etiketi oluşturmanız gerektiğinde kullanabileceğiniz çok kullanışlı bir yardımcı program sınıfıdır. Öznitelikleri ekleme, CSS sınıfları ekleme, Kimlik oluşturma ve etiketin iç HTML'sini değiştirme yöntemlerini içerir.

## <a name="summary"></a>Özet

Bu yinelemede, ASP.NET MVC uygulamamızın görsel tasarımını geliştirdik. İlk olarak, ASP.NET MVC Tasarım Galerisi tanıtıldı. ASP.NET MVC uygulamalarınızda kullanabileceğiniz ASP.NET MVC Tasarım Galerisi'nden ücretsiz tasarım şablonlarını nasıl indirebileceğinizi öğrendiniz.

Ardından, varsayılan basamaklı stil sayfası dosyasını ve ana görünüm sayfa dosyasını değiştirerek özel bir tasarımı nasıl oluşturabileceğinizi tartıştık. Yeni tasarımı desteklemek için, İletişim Yöneticisi uygulamamızda bazı küçük değişiklikler yapmak zorunda kaldık. Örneğin, seçili ve seçilmemiş sekmeleri görüntüleyen MenuItemHelper adında yeni bir HTML yardımcısı ekledik.

Bir sonraki yinelemede, çok önemli doğrulama konusunu ele alacağız. Uygulamamıza doğrulama kodu ekleriz, böylece kullanıcı kişinin adı ve soyadı gibi gerekli değerleri sağlamadan yeni bir kişi oluşturamaz.

> [!div class="step-by-step"]
> [Önceki](iteration-1-create-the-application-vb.md)
> [Sonraki](iteration-3-add-form-validation-vb.md)
