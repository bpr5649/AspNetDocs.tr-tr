---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 'Bölüm 4: Ürünleri listeleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 4. Bölüm GridView Sözl ile ürünleri listeleme kapsayan...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131013"
---
# <a name="part-4-listing-products"></a>Bölüm 4: Ürünleri Listeleme

tarafından [ALi Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir. Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.
> 
> Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 4. Bölüm GridView denetimi ile ürünleri listeleme kapsar.

## <a id="_Toc260221670"></a>  GridView denetimi ile ürünleri listeleme

"Sağ tıklayarak" ProductsList.aspx sayfamızı uygulama Çözümümüzü ve "Ekle" ve "Yeni öğe" seçerek başlayalım.

![](tailspin-spyworks-part-4/_static/image1.jpg)

"Web formu kullanarak ana sayfa" öğesini seçin ve ProductsList.aspx sayfa adını".

"Ekle" ye tıklayın.

![](tailspin-spyworks-part-4/_static/image2.jpg)

Sonraki biz Site.Master sayfanın nereye yerleştirileceğini "Stilleri" klasörü seçin ve "Klasörünün içeriğini" penceresinden seçin.

![](tailspin-spyworks-part-4/_static/image3.jpg)

Sayfayı oluşturmak için "Tamam"'a tıklayın.

Veritabanımızdaki aşağıda görüldüğü gibi ürün verilerle doldurulur.

![](tailspin-spyworks-part-4/_static/image4.jpg)

Sayfamızı oluşturulduktan sonra yeniden bir varlık veri kaynağı bu ürün verilere erişmek için kullanacağız ancak bu örnekte ürün varlıkları seçmeliyiz ve yalnızca seçilen kategori için döndürülen öğeleri sınırlamak gerekiyor.

Bunu gerçekleştirmek için otomatik oluşturmak için EntityDataSource WHERE yan tümcesi anlatılır ve biz WhereParameter belirtirsiniz.

Bizim "ürün kategorisi menüde" menü öğelerini oluşturduğumuz zaman dinamik olarak bağlantı CategoryID her bağlantı için sorgu dizesini ekleyerek oluşturduk, Hatırlayacağınız. Biz bu QueryString parametresi nerede parametresi türetmek için varlık veri kaynağını bildirir.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

Ardından, ürünlerin listesini görüntülemek için ListView denetimi yapılandıracağız. En iyi bir alışveriş deneyimi oluşturmak için sizi birkaç kısa özellik bizim ListVew içinde gösterilen her bir ürün düzenlenecek.

- Ürün adı, ürün ayrıntılı görünüm bağlantısı olacaktır.
- Ürünün fiyatını görüntülenir.
- Ürün görüntüsü görüntülenir ve dinamik olarak görüntüyü bir katalog görüntüleri dizinden uygulamamız içinde seçeneğini belirleyeceğiz.
- Biz, hemen ürününün alışveriş sepetine eklemek için bir bağlantı bulunur.

Bizim ListView denetimi örneği için biçimlendirme şöyledir.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

Biz, dinamik olarak görüntülenen her ürün için çeşitli bağlantılar oluşturuyorsunuz.

Ayrıca, kendi yeni sayfa test ederiz önce ürün için dizin yapısına şu şekilde Kataloğu görüntüleri oluşturmak gerekir.

![](tailspin-spyworks-part-4/_static/image1.png)

Ürün görüntülerimizi erişilebilir olduğunda, ürün listesi sayfamızı sınayabiliriz.

![](tailspin-spyworks-part-4/_static/image5.jpg)

Sitenin giriş sayfasından, kategori listesi bağlantılardan birine tıklayın.

![](tailspin-spyworks-part-4/_static/image6.jpg)

Artık ProductDetails.aspx sayfası ve AddToCart işlevselliği uygulamak ihtiyacımız var.

Dosya - kullanma&gt;yeni bir sayfa adı daha önce yaptığımız gibi sitenin ana sayfasını kullanarak ProductDetails.aspx oluşturmak için.

Biz yeniden EntityDataSource denetimi veritabanında belirli bir ürün kaydı erişmek için kullanacağı ve ASP.NET FormView denetimi gibi ürün verilerini görüntülemek için kullanacağız.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

Biçimlendirme bir bit size komik olmadıysa endişelenmeyin. Ekran düzenini odada birkaç biz daha sonra uygulayacaksınız özellikleri için yukarıdaki biçimlendirme bırakır.

Alışveriş sepeti uygulamamızı daha karmaşık mantık temsil eder. Başlamak için dosya - kullanma&gt;MyShoppingCart.aspx adlı bir sayfa oluşturmak için yeni.

Biz ShoppingCart.aspx adı almadığınızdan unutmayın.

Veritabanımızdaki "ShoppingCart" adında bir tablo içeriyor. Biz oluşturulan bir varlık veri modeli, veritabanındaki her tablo için bir sınıf oluşturuldu. Bu nedenle, varlık veri modeli "ShoppingCart" adında bir varlık sınıfı oluşturulur. Modeli böylece biz alışveriş sepeti kararlılığımızın için bu adı kullanın veya ilişkin genişletmek ancak biz yalnızca çakışma kaçınır bir ad seçmek için bunun yerine benimseyeceksiniz düzenlemek.

Ayrıca biz basit bir alışveriş sepeti oluşturacağınız belirterek ve alışveriş sepeti mantığı ile alışveriş sepetini görüntüleme katıştırma değer olur. Biz de tamamen ayrı bir iş katmanında alışveriş sepetimizi uygulamak seçebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-3.md)
> [İleri](tailspin-spyworks-part-5.md)
