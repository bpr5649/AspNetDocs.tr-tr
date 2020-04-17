---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: Ana Sayfaları Görüntülemek Için Veri Aktarma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı, verileri bir denetleyiciden görünüm ana sayfasına nasıl geçirebileceğinizi açıklamaktır. Biz bir görünüm m veri aktarmak için iki strateji incelemek ...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: ef65541a5f2297414f923e2f8108a14de67531e5
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542475"
---
# <a name="passing-data-to-view-master-pages-vb"></a>Görünüm Ana sayfalarına Veri Geçirme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> Bu öğreticinin amacı, verileri bir denetleyiciden görünüm ana sayfasına nasıl geçirebileceğinizi açıklamaktır. Verileri bir görünüm ana sayfasına aktarmak için iki stratejiyi inceleriz. İlk olarak, bakımı zor bir uygulama ile sonuçlanan kolay bir çözüm tartışmak. Daha sonra, biraz daha ilk çalışma gerektiren ama çok daha bakımlı bir uygulama ile sonuçlanan çok daha iyi bir çözüm incelemek.

## <a name="passing-data-to-view-master-pages"></a>Ana Sayfaları Görüntülemek Için Veri Aktarma

Bu öğreticinin amacı, verileri bir denetleyiciden görünüm ana sayfasına nasıl geçirebileceğinizi açıklamaktır. Verileri bir görünüm ana sayfasına aktarmak için iki stratejiyi inceleriz. İlk olarak, bakımı zor bir uygulama ile sonuçlanan kolay bir çözüm tartışmak. Daha sonra, biraz daha ilk çalışma gerektiren ama çok daha bakımlı bir uygulama ile sonuçlanan çok daha iyi bir çözüm incelemek.

### <a name="the-problem"></a>Sorun

Bir film veritabanı uygulaması yaptığınızı ve uygulamanızdaki her sayfada film kategorisi listesini görüntülemek istediğinizi düşünün (Bkz. Şekil 1). Ayrıca, film kategorileri listesinin bir veritabanı tablosunda depoladığını düşünün. Bu durumda, kategorileri veritabanından almak ve bir görünüm ana sayfasındaki film kategorileri listesini oluşturmak mantıklı olacaktır.

[![Film kategorilerini görünüm ana sayfasında görüntüleme](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**Şekil 01**: Film kategorilerini görünüm ana sayfasında görüntüleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](passing-data-to-view-master-pages-vb/_static/image3.png))

Sorun şu. Ana sayfadaki film kategorileri listesini nasıl alabilirsiniz? Model sınıflarınızın yöntemlerini ana sayfada doğrudan aramak caziptir. Başka bir deyişle, veritabanından verileri almak için kodu ana sayfanıza eklemek caziptir. Ancak, veritabanına erişmek için MVC denetleyicilerinizi atlayarak, bir MVC uygulaması oluşturmanın birincil avantajlarından biri olan endişelerin temiz bir şekilde ayrılmasını ihlal eder.

Bir MVC uygulamasında, MVC görünümleriniz ile MVC modeliniz arasındaki tüm etkileşimin MVC denetleyicileriniz tarafından ele alınmasını istersiniz. Endişelerin bu ayrımı daha sayılabilir, uyarlanabilir ve test edilebilir bir uygulamayla sonuçlanır.

Bir MVC uygulamasında, görünüm ana sayfası da dahil olmak üzere bir görünüme aktarılan tüm veriler denetleyici eylemi tarafından görünüme geçirilmelidir. Ayrıca, veri görünüm verileri yararlanılarak geçirilmelidir. Bu öğreticinin geri kalanında, görünüm verilerini bir görünüm ana sayfasına aktarmanın iki yöntemini inceliyorum.

### <a name="the-simple-solution"></a>Basit Çözüm

Görünüm verilerini bir denetleyiciden görünüm ana sayfasına aktarmak için en basit çözümle başlayalım. En basit çözüm, her denetleyici eyleminde ana sayfanın görünüm verilerini aktarmaktır.

Listeleme 1'deki denetleyiciyi göz önünde bulundurun. Bu adlı `Index()` iki eylemi `Details()`ortaya çıkarır ve . Eylem `Index()` yöntemi, Filmler veritabanı tablosundaki her filmi döndürür. Eylem `Details()` yöntemi, belirli bir film kategorisindeki her filmi döndürür.

**İlan 1 –`Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

Hem eylemlerin `Index()` hem `Details()` de eylemlerin verileri görüntülemek için iki öğe eklediğini unutmayın. Eylem `Index()` iki anahtar ekler: kategoriler ve filmler. Kategoriler anahtarı, görünüm ana sayfası tarafından görüntülenen film kategorileri listesini temsil eder. Film anahtarı, Dizin görünümü sayfası tarafından görüntülenen filmlerin listesini temsil eder.

Eylem `Details()` ayrıca kategoriler ve filmler adlı iki anahtar ekler. Kategoriler anahtarı, bir kez daha, görünüm ana sayfası tarafından görüntülenen film kategorileri listesini temsil eder. Film anahtarı, Ayrıntılar görünüm sayfasında görüntülenen belirli bir kategorideki filmlerin listesini temsil eder (Bkz. Şekil 2).

[![Ayrıntılar görünümü](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**Şekil 02**: Ayrıntılar görünümü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](passing-data-to-view-master-pages-vb/_static/image6.png))

Dizin görünümü Listeleme 2'de bulunur. Sadece görünüm verilerinde film öğesi tarafından temsil edilen filmlerin listesi üzerinden yinelenir.

**Listeleme 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

Görünüm ana sayfası Listeleme 3'te yer almaktadır. Görünüm ana sayfası, görünüm verilerinden kategoriler öğe tarafından temsil edilen tüm film kategorilerini yineler ve işler.

**İlan 3 –`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

Tüm veriler görünüm verileri aracılığıyla görünüme ve görünüm ana sayfasına aktarılır. Bu, ana sayfaya veri aktarmanın doğru yoludur.

Peki, bu çözümün nesi var? Sorun şu ki, bu çözüm DRY (Kendinizi Tekrar etmeyin) ilkesini ihlal ediyor. Her denetleyici eylemi, verileri görüntülemek için aynı film kategorileri listesini eklemelidir. Uygulamanızda yinelenen kod olması, uygulamanızın korunmasını, uyarlamasını ve değiştirilmesini çok daha zor hale getirir.

### <a name="the-good-solution"></a>İyi Çözüm

Bu bölümde, bir denetleyici eyleminden görünüm ana sayfasına veri aktarmak için alternatif ve daha iyi bir çözümü inceliyoruz. Her denetleyici eyleminde ana sayfanın film kategorilerini eklemek yerine, film kategorilerini görünüm verilerine yalnızca bir kez ekleriz. Görünüm ana sayfası tarafından kullanılan tüm görünüm verileri bir Uygulama denetleyicisi eklenir.

ApplicationController sınıfı Listeleme 4'te yer almaktadır.

ApplicationController sınıfı Listeleme 4'te yer almaktadır.

**İlan 4 –`Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

Listeleme 4'teki Uygulama denetleyicisi hakkında dikkat etmelisiniz üç şey vardır. İlk olarak, sınıfın base System.Web.Mvc.Controller sınıfından devraldığına dikkat edin. Uygulama denetleyicisi bir denetleyici sınıfıdır.

İkinci olarak, Uygulama denetleyici sınıfının mustinherit sınıfı olduğuna dikkat edin. MustInherit sınıfı, somut bir sınıf tarafından uygulanması gereken bir sınıftır. Uygulama denetleyicisi bir MustInherit sınıfı olduğundan, sınıfta tanımlanan yöntemleri doğrudan çağıramazsınız. Uygulama sınıfını doğrudan çağırmaya çalışırsanız, Kaynak Bulunamadı hata iletisi alırsınız.

Üçüncü olarak, Uygulama denetleyicisinin verileri görüntülemek için film kategorileri listesini ekleyen bir oluşturucu içerdiğine dikkat edin. Uygulama denetleyicisinden devralan her denetleyici sınıfı, Uygulama denetleyicisinin oluşturucusu otomatik olarak çağırır. Uygulama denetleyicisinden devralınan herhangi bir denetleyici üzerinde herhangi bir eylem dediğinizde, film kategorileri görüntüleme verilerine otomatik olarak dahil edilir.

Listeleme 5'teki Filmler denetleyicisi Uygulama denetleyicisinden devralır.

**İlan 5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

Filmler denetleyicisi, tıpkı önceki bölümde tartışılan Ev denetleyicisi gibi, adlı `Index()` iki eylem yöntemini ortaya çıkarır ve `Details()`. Görünüm ana sayfası tarafından görüntülenen film kategorileri listesinin verileri `Index()` `Details()` görüntülemek için eklenmediğini unutmayın. Filmler denetleyicisi Uygulama denetleyicisinden devraldığı için, verileri otomatik olarak görüntülemek için film kategorileri listesi eklenir.

Bir görünüm ana sayfası için görünüm verileri eklemeye yönelik bu çözümün DRY (Kendinizi Tekrar Etmeyin) ilkesini ihlal etmediğine dikkat edin. Verileri görüntülemek için film kategorileri listesini ekleme kodu yalnızca bir konumda bulunur: Uygulama denetleyicisinin oluşturucusu.

### <a name="summary"></a>Özet

Bu öğreticide, görünüm verilerini bir denetleyiciden görünüm ana sayfasına geçirmek için iki yaklaşımı tartıştık. İlk olarak, basit ama yaklaşımı korumak zor bir inceleme yaptık. İlk bölümde, uygulamanızdaki her denetleyici eyleminde bir görünüm ana sayfası için görünüm verilerini nasıl ekleyebileceğiniz tartışıldı. Bunun kötü bir yaklaşım olduğu sonucuna vardık çünkü DRY (Kendini Tekrar Etme) ilkesini ihlal ediyor.

Daha sonra, verileri görüntülemek için bir görünüm ana sayfası tarafından gerekli verileri eklemek için çok daha iyi bir strateji inceledik. Her denetleyici eyleminde görünüm verilerini eklemek yerine, görünüm verilerini bir Uygulama denetleyicisi içinde yalnızca bir kez ekledik. Bu şekilde, ASP.NET bir MVC uygulamasında bir görünüm ana sayfasına veri aktarırken yinelenen kodlardan kaçınabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](creating-page-layouts-with-view-master-pages-vb.md)
