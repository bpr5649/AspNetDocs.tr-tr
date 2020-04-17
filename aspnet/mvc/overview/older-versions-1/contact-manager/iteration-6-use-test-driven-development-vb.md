---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: 'Yineleme #6 – Test odaklı geliştirme (VB) kullanın | Microsoft Dokümanlar'
author: rick-anderson
description: Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemede,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 8464f4cdee673ef75d561e4cf89613fdca2c16af
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542813"
---
# <a name="iteration-6--use-test-driven-development-vb"></a>6. Yineleme – Test odaklı geliştirme kullanma (VB)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (VB)

Öğreticiler bu dizi, biz baştan sona tüm Bir İletişim Yönetimi uygulaması oluşturmak. İletişim Yöneticisi uygulaması, kişi listesi için kişi bilgilerini (adlar, telefon numaraları ve e-posta adresleri) depolamanızı sağlar.

Uygulamayı birden çok yineleme üzerine oluşturuyoruz. Her yineleme ile, yavaş yavaş uygulama geliştirmek. Bu çoklu yineleme yaklaşımının amacı, her değişikliğin nedenini anlamanızı sağlamaktır.

- Yineleme #1 - Uygulamayı oluşturun. İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

- Yineleme #2 - Uygulama güzel görünmesini sağlamak. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

- Yineleme #3 - Form doğrulama ekleyin. Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

- Yineleme #4 - Uygulamayı gevşek bir şekilde biraraya getirin. Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

- Yineleme #5 - Birim testleri oluşturun. Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

- Yineleme #6 - Test odaklı geliştirme yi kullanın. Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

- Yineleme #7 - Ajax işlevselliği ekleyin. Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="this-iteration"></a>Bu Yineleme

Contact Manager uygulamasının önceki yinelemesinde, kodumuz için bir güvenlik ağı sağlamak için birim testleri oluşturduk. Birim testleri oluşturmanın motivasyonu kodumuzu değiştirmeye karşı daha esnek hale getirmekti. Birim testleri devreye girince, kodumuzda herhangi bir değişiklik yapabilir ve mevcut işlevleri bozup bozmadığımızı hemen anlayabiliriz.

Bu yinelemede, birim testlerini tamamen farklı bir amaç için kullanırız. Bu yinelemede, birim testleri *test odaklı geliştirme*adı verilen bir uygulama tasarım felsefesinin bir parçası olarak kullanırız. Test odaklı geliştirme alıştırması yaptığınızda, önce testleri yazar, ardından testlere karşı kod yazarsınız.

Daha doğrusu, test odaklı geliştirme uygularken, kod oluştururken tamamladığınız üç adım vardır (Kırmızı/ Yeşil/Refactor):

1. Başarısız olan bir birim testi yazma (Kırmızı)
2. Birim testini geçen kod yazma (Yeşil)
3. Kodunuzu yeniden düzenleme (Refactor)

Önce birim testini yazarsın. Birim testi, kodunuzu nasıl beklediğinize yönelik niyetinizi ifade etmelidir. Birim testini ilk oluşturduğunuzda, birim testi başarısız olmalıdır. Testi karşılayan herhangi bir uygulama kodu henüz yazmadığınız için test başarısız olmalıdır.

Sonra, birim testinin geçmesi için yeterli kod yazarsınız. Amaç, kodu mümkün olan en tembel, en özensiz ve en hızlı şekilde yazmaktır. Uygulamanızın mimarisi ni düşünerek zaman kaybetmemelisiniz. Bunun yerine, birim testi tarafından ifade edilen niyeti karşılamak için gereken en az kod miktarını yazmaya odaklanmalısınız.

Son olarak, yeterli kod yazdıktan sonra geri adım atabilir ve uygulamanızın genel mimarisini göz önünde bulundurabilirsiniz. Bu adımda, kodunuzu daha iyi koruyabilmek için yazılım tasarım desenlerinden (depo deseni gibi) yararlanarak kodunuzu yeniden yazar (yeniden tasarlarsınız). Kodunuz birim testleri kapsamında olduğundan, bu adımda korkusuzca kodunuzu yeniden yazabilirsiniz.

Test odaklı geliştirme uygulama sonucu birçok faydası vardır. İlk olarak, test odaklı geliştirme sizi gerçekten yazılması gereken koda odaklanmaya zorlar. Sürekli olarak belirli bir testi geçmek için yeterli kod yazmaya odaklandığınız için, asla kullanamayacağınız büyük miktarda kod yazmak için izniniçine girmeniz ve yazmanız engellenir.

İkinci olarak, "önce test edin" tasarım metodolojisi sizi kodunuzu nasıl kullanılacağı açısından kod yazmaya zorlar. Başka bir deyişle, test odaklı geliştirme uygularken, testlerinizi sürekli olarak kullanıcı açısından yazarsınız. Bu nedenle, test odaklı geliştirme daha temiz ve daha anlaşılır API'ler neden olabilir.

Son olarak, test odaklı geliştirme, bir uygulama yazma normal sürecinin bir parçası olarak birim testleri yazmaya zorlar. Bir proje son tarih yaklaştıkça, sınama genellikle pencereden dışarı gider ilk şeydir. Diğer taraftan, test odaklı geliştirme yi uygularken birim testleri yazma konusunda erdemli olma olasılığınız daha yüksektir, çünkü test odaklı geliştirme birim testlerini bir uygulama oluşturma sürecinin merkezinde yapar.

> [!NOTE] 
> 
> Test odaklı geliştirme hakkında daha fazla bilgi edinmek için, Michael Feathers'ın **Legacy Code ile Etkili Bir Şekilde Çalışma**kitabını okumanızı öneririm.

Bu yinelemede, İletişim Yöneticisi uygulamamıza yeni bir özellik ekliyoruz. İletişim Grupları için destek ekliyoruz. Kişi Grupları'nı, kişilerinizi İş ve Arkadaş grupları gibi kategorilerhalinde düzenlemek için kullanabilirsiniz.

Bu yeni işlevselliği, test odaklı bir geliştirme sürecini izleyerek uygulamamıza ekleyeceğiz. Önce birim testlerimizi yazacağız ve tüm kodlarımızı bu testlere karşı yazacağız.

## <a name="what-gets-tested"></a>Ne Test Gets

Önceki yinelemede de belirttiğimiz gibi, genellikle veri erişim mantığı veya görünüm mantığı için birim testleri yazmayın. Veritabanına erişmek nispeten yavaş bir işlem olduğundan, veri erişim mantığı için birim testleri yazmazsınız. Görünüm mantığı için birim testleri yazmazsınız, çünkü bir görünüme erişmek nispeten yavaş bir işlem olan bir web sunucusunu döndürmeyi gerektirir. Test tekrar tekrar çok hızlı yürütülmedikçe bir birim testi yazmamalısınız

Test odaklı geliştirme birim testleri tarafından yürütüldüğünden, başlangıçta denetleyici ve işman manılığına odaklanılır. Veritabanına veya görünüme dokunmaktan kaçınıyoruz. Bu eğitimin sonuna kadar veritabanını değiştirmeyecek veya görünümlerimizi oluşturmayacağız. Test edilebilenlerle başlıyoruz.

## <a name="creating-user-stories"></a>Kullanıcı Hikayeleri Oluşturma

Test odaklı geliştirme pratiği yaparken, her zaman bir test yazarak başlarsınız. Bu hemen şu soruyu gündeme getiriyor: İlk olarak hangi testi yazacağına nasıl karar verebilirsiniz? Bu soruyu yanıtlamak için, bir dizi [*kullanıcı hikayesi*](http://en.wikipedia.org/wiki/User_stories)yazmanız gerekir.

Kullanıcı hikayesi, yazılım gereksiniminin çok kısa (genellikle tek cümle) açıklamasıdır. Kullanıcı açısından yazılmış bir gereksinimin teknik olmayan bir açıklaması olmalıdır.

Burada, yeni Kişi Grubu işlevinin gerektirdiği özellikleri açıklayan kullanıcı öyküleri kümesi verilmiştir:

1. Kullanıcı kişi gruplarının listesini görüntüleyebilir.
2. Kullanıcı yeni bir kişi grubu oluşturabilir.
3. Kullanıcı varolan bir kişi grubunu silebilir.
4. Kullanıcı, yeni bir kişi oluştururken bir kişi grubu seçebilir.
5. Kullanıcı, varolan bir kişi düzenlerken bir kişi grubu seçebilir.
6. Dizin görünümünde kişi gruplarının listesi görüntülenir.
7. Bir kullanıcı bir kişi grubunu tıklattığında, eşleşen kişilerin listesi görüntülenir.

Bu kullanıcı hikayeleri listesinin bir müşteri tarafından tamamen anlaşılabilir olduğuna dikkat edin. Teknik uygulama detaylarından söz edilememektedir.

Uygulamanızı oluşturma sürecinde yken, kullanıcı öyküleri kümesi daha rafine hale gelebilir. Bir kullanıcı hikayesini birden çok öyküye (gereksinimlere) kırabilirsiniz. Örneğin, yeni bir kişi grubu oluşturmanın doğrulama içermesi gerektiğine karar verebilirsiniz. Adsız bir kişi grubu göndermek bir doğrulama hatası döndürmelidir.

Kullanıcı öykülerinin bir listesini oluşturduktan sonra, ilk birim testinizi yazmaya hazırsınız. Kişi gruplarının listesini görüntülemek için bir birim testi oluşturarak başlayacağız.

## <a name="listing-contact-groups"></a>Kişi Gruplarını Listeleme

İlk kullanıcı hikayemiz, bir kullanıcının kişi gruplarının listesini görebilmeleridir. Bu hikayeyi bir testle ifade etmeliyiz.

ContactManager.Tests projesinde Denetleyiciler klasörüne sağ tıklayarak, **Ekle, Yeni Test'i**seçerek ve **Birim Testi** şablonuna bakarak yeni bir birim testi oluşturun (Bkz. Şekil 1). Yeni birim test GroupControllerTest.vb adını ve **Tamam** düğmesini tıklatın.

[![GroupControllerTest birim testi ekleme](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**Şekil 01**: GroupControllerTest birim testinin eklenmesi([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image2.png))

İlk ünite testimiz Listeleme 1'de yer almaktadır. Bu test, Grup denetleyicisinin Dizin() yönteminin bir grup kümesini döndürür olduğunu doğrular. Test, görünüm verilerinde gruplar koleksiyonunun döndürüldettiğini doğrular.

**Listeleme 1 - Denetleyiciler\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

Visual Studio'da Liste 1'e kodu ilk yazdığınızda, çok sayıda kırmızı kıvrımlı çizgi alırsınız. GroupController veya Grup sınıflarını oluşturmadık.

Bu noktada, uygulamamızı bile oluşturamıyorduk, bu yüzden ilk birim testimizi uygulayabiliyoruz. Bu iyi. Bu başarısız bir test sayılır. Bu nedenle, artık uygulama kodu yazmaya başlamak için iznimiz vardır. Testimizi uygulamak için yeterli kod yazmamız gerekiyor.

Listeleme 2'deki Grup denetleyici sınıfı, birim testini geçmek için gereken minimum kodu içerir. Index() eylemi, statik olarak kodlanmış gruplar listesini döndürür (Grup sınıfı Listeleme 3'te tanımlanır).

**Listeleme 2 - Denetleyiciler\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**Listeleme 3 - Modeller\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

GroupController ve Grup sınıflarını projemize ekledikten sonra, ilk ünite testimiz başarıyla tamamlar (Bkz. Şekil 2). Testi geçmek için gereken minimum işi yaptık. Kutlama zamanı.

[![Başarı!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**Şekil 02**: Başarı! ([Tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-vb/_static/image4.png))

## <a name="creating-contact-groups"></a>Kişi Grupları Oluşturma

Şimdi ikinci kullanıcı hikayesine geçebiliriz. Yeni kişi grupları oluşturabilmelidir. Bu niyeti bir testle ifade etmeliyiz.

Listeleme 4'teki test, Yeni Bir Grupla Oluştur() yöntemini aramanın Grubu Dizin() yöntemiyle döndürülen Gruplar listesine eklediği doğrular. Başka bir deyişle, yeni bir grup oluşturursam, yeni Grubu Index() yöntemiyle döndürülen Gruplar listesinden geri alabiliyorum.

**Listeleme 4 - Denetleyiciler\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

Listeleme 4'teki test, Grup denetleyicisi Oluşturma() yöntemini yeni bir kişi Grubu ile çağırır. Daha sonra, test Grup denetleyicisi Index() yöntemini aramanın görünüm verilerinde yeni Grubu döndürür doğrular.

Listeleme 5'teki değiştirilmiş Grup denetleyicisi, yeni testi geçmek için gereken en az değişikliği içerir.

**Listeleme 5 - Denetleyiciler\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>Listeleme 5'teki Grup denetleyicisinin yeni bir Oluşturma() eylemi vardır. Bu eylem, Gruplar koleksiyonuna bir Grup ekler. Gruplar koleksiyonunun içeriğini döndürmek için Index() eyleminin değiştirildiğini unutmayın.

Bir kez daha, birim testini geçmek için gereken minimum iş miktarını gerçekleştirdik. Grup denetleyicisi için bu değişiklikleri yaptıktan sonra, tüm birim testlerimiz geçer.

## <a name="adding-validation"></a>Doğrulama Ekleme

Bu gereksinim kullanıcı hikayesinde açıkça belirtilmemiştir. Ancak, bir Grubun bir adı olmasını istemek makuldür. Aksi takdirde, kişileri Gruplar halinde düzenlemek çok yararlı olmaz.

Listeleme 6 bu niyeti ifade eden yeni bir test içerir. Bu sınama, ad sağlamadan bir Grup oluşturmaya çalışırken model durumunda bir doğrulama hatası iletisi ile sonuçladığını doğrular.

**Listeleme 6 - Denetleyiciler\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

Bu testi karşılamak için, Grup sınıfımıza bir Ad özelliği eklememiz gerekir (bkz. Ayrıca, Grup denetleyicimiz Create() eylemine biraz doğrulama mantığı eklememiz gerekir (bkz.

**Listeleme 7 - Modeller\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**Listeleme 8 - Denetleyiciler\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

Grup denetleyicisi Create() eyleminin artık hem doğrulama hem de veritabanı mantığı içerdiğine dikkat edin. Şu anda, Grup denetleyicisi tarafından kullanılan veritabanı bellek içi bir koleksiyondan başka bir şey oluşturmaz.

## <a name="time-to-refactor"></a>Refactor Zamanı

Kırmızı / Yeşil / Refactor üçüncü adım Refactor parçasıdır. Bu noktada, kodumuzdan geri adım atmalıyız ve tasarımını geliştirmek için uygulamamızı nasıl yeniden değerlendirebileceğimizi düşünmeliyiz. Refactor aşaması, yazılım tasarım ilke ve desenlerini uygulamanın en iyi yolu hakkında çok düşündüğümüz aşamadır.

Kodumuzu, kodun tasarımını geliştirmek için seçtiğimiz herhangi bir şekilde değiştirmekte özgüruz. Mevcut işlevleri kırmamızı engelleyen bir güvenlik birimi testağına sahibiz.

Şu anda, Bizim Grup denetleyiciiyi yazılım tasarımı açısından bir karmaşa olduğunu. Grup denetleyicisi doğrulama ve veri erişim kodu karışık bir karmaşa içerir. Tek Sorumluluk İlkesi'ni ihlal etmekten kaçınmak için, bu endişeleri farklı sınıflara ayırmamız gerekir.

Refactored Grup denetleyici sınıfımız Listeleme 9'da yer almaktadır. Denetleyici, ContactManager hizmet katmanını kullanacak şekilde değiştirildi. Bu, İletişim denetleyicisi ile kullandığımız hizmet katmanıdır.

Liste 10, doğrulamayı, listelemeyi ve grupları oluşturmak için ContactManager hizmet katmanına eklenen yeni yöntemleri içerir. IContactManagerService arabirimi yeni yöntemleri içerecek şekilde güncelleştirildi.

Listeleme 11, IContactManagerRepository arabirimini uygulayan yeni bir FakeContactManagerRepository sınıfı içerir. Ayrıca IContactManagerRepository arabirimini uygulayan EntityContactManagerRepository sınıfının aksine, yeni FakeContactManagerRepository sınıfımız veritabanı ile iletişim kurmaz. FakeContactManagerRepository sınıf veritabanı için bir proxy olarak bellek koleksiyonu kullanır. Bu sınıfı birim testlerimizde sahte depo katmanı olarak kullanacağız.

**Listeleme 9 - Denetleyiciler\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**Listeleme 10 - Denetleyiciler\ContactManagerService.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**Listeleme 11 - Denetleyiciler\FakeContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

IContactManagerRepository arabiriminin değiştirilmesi, EntityContactManagerRepository sınıfında CreateGroup() ve ListGroups() yöntemlerini uygulamak için kullanım gerektirir. Bunu yapmanın en tembel ve en hızlı yolu şuna benzeyen saplama yöntemleri eklemektir:

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

Son olarak, uygulamamızın tasarımında yapılan bu değişiklikler, birim testlerimizde bazı değişiklikler yapmamızı gerektirmektedir. Şimdi birim testleri yaparken FakeContactManagerRepository kullanmanız gerekir. Güncelleştirilmiş GroupControllerTest sınıfı Listeleme 12'de bulunur.

**Listeleme 12 - Denetleyiciler\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

Tüm bu değişiklikleri yaptıktan sonra, bir kez daha, tüm birim testlerimiz geçer. Kırmızı/Yeşil/Refactor döngüsünün tamamını tamamladık. İlk iki kullanıcı öykülerini uyguladık. Artık kullanıcı hikayelerinde ifade edilen gereksinimler için destekleyici birim testlerine sahibiz. Kullanıcı öykülerinin geri kalanının uygulanması, aynı Kırmızı/Yeşil/Refactor döngüsünü yinelemeyi içerir.

## <a name="modifying-our-database"></a>Veritabanımızı Değiştirme

Ne yazık ki, birim testlerimizin ifade ettiği tüm gereklilikleri yerine getirmiş olsak da, çalışmalarımız bitmedi. Hala veritabanımızı değiştirmemiz gerekiyor.

Yeni bir Grup veritabanı tablosu oluşturmamız gerekiyor. Şu adımları uygulayın:

1. Server Explorer penceresinde, Tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**seçeneğini seçin.
2. Tablo Tasarımcısı'nda aşağıda açıklanan iki sütunu girin.
3. Kimlik sütununu birincil anahtar ve Kimlik sütunu olarak işaretleyin.
4. Disket simgesini tıklatarak ad Grupları ile yeni tablokaydedin.

<a id="0.12_table01"></a>

| **Sütun Adı** | **Veri Türü** | **Nulls'a İzin Ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Adı | nvarchar(50) | False |

Ardından, Kişiler tablosundaki tüm verileri silmemiz gerekir (aksi takdirde Kişiler ve Gruplar tabloları arasında bir ilişki oluşturamayız). Şu adımları uygulayın:

1. Kişiler tablosuna sağ tıklayın ve **Tablo Verilerini Göster**menüsü seçeneğini seçin.
2. Tüm satırları silin.

Ardından, Gruplar veritabanı tablosu ile varolan Kişiler veritabanı tablosu arasında bir ilişki tanımlamamız gerekir. Şu adımları uygulayın:

1. Tablo Tasarımcısı'nı açmak için Sunucu Gezgini penceresindeki Kişiler tablosunu çift tıklatın.
2. Kişiler tablosuna GroupId adlı yeni bir tamsayı sütunu ekleyin.
3. Yabancı Anahtar İlişkileri iletişim kutusunu açmak için İlişki düğmesini tıklatın (Bkz. Şekil 3).
4. Ekle düğmesini tıklatın.
5. Tablo ve Sütunlar Belirtimi düğmesinin yanında görünen elips düğmesini tıklatın.
6. Tablolar ve Sütunlar iletişim kutusunda, birincil anahtar tablosu olarak Gruplar'ı ve birincil anahtar sütun olarak Id'yi seçin. Kişiler'i yabancı anahtar tablosu olarak seçin ve groupid yabancı anahtar sütunu olarak (Bkz. Şekil 4). Tamam düğmesine tıklayın.
7. **INSERT ve UPDATE Belirtimi**altında, **Silme Kuralı**için **Basamaklı** değeri seçin.
8. Yabancı Anahtar İlişkileri iletişim kutusunu kapatmak için Kapat düğmesini tıklatın.
9. Kişiler tablosundaki değişiklikleri kaydetmek için Kaydet düğmesini tıklatın.

[![Veritabanı tablo ilişkisi oluşturma](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**Şekil 03**: Veritabanı tablosu ilişkisi oluşturma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image6.png))

[![Tablo ilişkilerini belirtme](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**Şekil 04**: Tablo ilişkilerini belirtme([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image8.png))

### <a name="updating-our-data-model"></a>Veri Modelimizi Güncelleme

Ardından, yeni veritabanı tablosunu temsil etmek için veri modelimizi güncelleştirmemiz gerekir. Şu adımları uygulayın:

1. Entity Designer'ı açmak için Modeller klasöründeki ContactManagerModel.edmx dosyasını çift tıklatın.
2. Designer yüzeyine sağ tıklayın ve Veritabanından Menü seçeneği **Güncelleştirme Modelini**seçin.
3. Güncelleştirme Sihirbazı'nda Gruplar tablosunu seçin ve Bitiş düğmesini tıklatın (Bkz. Şekil 5).
4. Gruplar varlığına sağ tıklayın ve menü seçeneğini yeniden **adlandır'ı**seçin. *Gruplar* varlığının adını *Grup* (tekil) olarak değiştirin.
5. İlgili Kişi varlığının alt kısmında görünen Gruplar gezinti özelliğini sağ tıklatın. *Gruplar* gezinti özelliğinin adını *Grup* (tekil) olarak değiştirin.

[![Varlık Çerçevesi modelini veritabanından güncelleştirme](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**Şekil 05**: Varlık Çerçevesi modelini veritabanından güncelleştirme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image10.png))

Bu adımları tamamladıktan sonra, veri modeliniz hem Kişiler hem de Gruplar tablolarını temsil edecektir. Varlık Tasarımcısı her iki varlığı da göstermelidir (bkz. Şekil 6).

[![Grup ve İlgili Kişi Görüntüleme Entity Designer](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**Şekil 06**: Grup ve İletişim'i görüntüleyen Varlık Tasarımcısı([Tam boyutlu görüntüyü görüntülemek için tıklayınız)](iteration-6-use-test-driven-development-vb/_static/image12.png)

### <a name="creating-our-repository-classes"></a>Depo Sınıflarımızı Oluşturma

Sonra, depo sınıfımızı uygulamamız gerekiyor. Bu yineleme boyunca, birim testlerimizi karşılamak için kod yazarken IContactManagerRepository arabirimine birkaç yeni yöntem ekledik. iContactManagerRepository arabiriminin son sürümü Listeleme 14'te bulunur.

**Listeleme 14 - Modeller\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

Biz aslında bizim gerçek EntityContactManagerRepository sınıfında temas grupları ile çalışma ile ilgili yöntemlerin hiçbirini uygulamadık. Şu anda EntityContactManagerRepository sınıfı, IContactManagerRepository arabiriminde listelenen kişi grubu yöntemlerinin her biri için saplama yöntemlerine sahiptir. Örneğin, ListGroups() yöntemi şu anda şu şekilde görünür:

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

Saplama yöntemleri uygulamamızı derlememizi ve birim testlerini geçmemizi sağladı. Ancak, şimdi aslında bu yöntemleri uygulamak için zamanı. EntityContactManagerRepository sınıfının son sürümü Listeleme 13'te yer almaktadır.

**Listeleme 13 - Modeller\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>Görünümleri Oluşturma

Varsayılan ASP.NET görünüm altyapısını kullandığınızda MVC uygulamasını ASP.NET. Bu nedenle, belirli bir birim testine yanıt olarak görünüm oluşturmazsınız. Ancak, bir uygulama görünümler olmadan yararsız olacağından, İletişim Yöneticisi uygulamasında bulunan görünümleri oluşturmadan ve değiştirmeden bu yinelemeyi tamamlayamayız.

Kişi gruplarını yönetmek için aşağıdaki yeni görünümleri oluşturmamız gerekir (Bkz. Şekil 7):

- Görünümler\Group\Index.aspx - Kişi gruplarının listesini görüntüler
- Görünümler\Grup\Delete.aspx - Kişi grubunu silmek için onay formunu görüntüler

[![Grup Dizini görünümü](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**Şekil 07**: Grup Dizini görünümü([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image14.png))

Aşağıdaki varolan görünümleri, kişi gruplarını içerecek şekilde değiştirmemiz gerekir:

- Görünümler\Ana Sayfa\Create.aspx
- Görünümler\Ana Sayfa\Edit.aspx
- Görünümler\Ana Sayfa\Index.aspx

Bu öğreticiye eşlik eden Visual Studio uygulamasına bakarak değiştirilmiş görünümleri görebilirsiniz. Örneğin, Şekil 8 Kişi Dizini görünümünü göstermektedir.

[![Kişi Dizini görünümü](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**Şekil 08**: İletişim Dizini görünümü([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-6-use-test-driven-development-vb/_static/image16.png))

## <a name="summary"></a>Özet

Bu yinelemede, test odaklı geliştirme uygulama tasarım metodolojisini izleyerek Contact Manager uygulamamıza yeni işlevler ekledik. Bir dizi kullanıcı hikayesi oluşturarak başladık. Kullanıcı hikayeleri tarafından ifade edilen gereksinimlere karşılık gelen bir birim testleri kümesi oluşturduk. Son olarak, birim testleri tarafından ifade edilen gereksinimleri karşılamak için yeterli kod yazdı.

Birim testleri tarafından ifade edilen gereksinimleri karşılayacak kadar kod yazmayı bitirdikten sonra, veritabanımızı ve görünümlerimizi güncelledik. Veritabanımıza yeni bir Gruplar tablosu ekledik ve Varlık Çerçeve Veri Modelimizi güncelledik. Ayrıca bir dizi görünüm oluşturduk ve değiştirdik.

Bir sonraki yinelemede -- son yinelemede -- Ajax'tan yararlanmak için başvurumuzu yeniden yazıyoruz. Ajax'tan yararlanarak, Contact Manager uygulamasının yanıt verme yeteneğini ve performansını artıracağız.

> [!div class="step-by-step"]
> [Önceki](iteration-5-create-unit-tests-vb.md)
> [Sonraki](iteration-7-add-ajax-functionality-vb.md)
