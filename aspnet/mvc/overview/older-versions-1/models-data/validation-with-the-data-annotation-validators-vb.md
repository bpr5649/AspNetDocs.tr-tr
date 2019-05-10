---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: (VB) veri ek açıklama doğrulayıcıları ile doğrulama | Microsoft Docs
author: microsoft
description: Bir ASP.NET MVC uygulaması içindeki doğrulama gerçekleştirmek için veri ek açıklama Model bağlayıcı yararlanın. Doğrulayıcı farklı türleri kullanmayı öğrenin...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117571"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Veri Ek Açıklama Doğrulayıcıları ile Doğrulama (VB)

tarafından [Microsoft](https://github.com/microsoft)

> Bir ASP.NET MVC uygulaması içindeki doğrulama gerçekleştirmek için veri ek açıklama Model bağlayıcı yararlanın. Doğrulayıcı öznitelikleri farklı türde ve bunlarla çalışan Microsoft varlık Çerçevesi'nde nasıl kullanılacağını öğrenin.

Bu öğreticide bir ASP.NET MVC uygulamasındaki doğrulamayı gerçekleştirmek için veri ek açıklama doğrulayıcıları kullanmayı öğrenin. Veri ek açıklama doğrulayıcıları kullanmanın avantajı, bunlar, yalnızca ekleyerek – gerekli gibi bir veya daha fazla öznitelikleri veya StringLength öznitelik – bir sınıf özelliği için doğrulama gerçekleştirmek etkinleştirmenizi ' dir.

Veri ek açıklama doğrulayıcıları kullanabilmeniz için veri ek açıklamaları Model bağlayıcısını yüklemeniz gerekir. Veri ek açıklamaları Model bağlayıcı örneği tıklayarak CodePlex Web sitesinden indirebilirsiniz [burada](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).

Veri ek açıklamaları Model bağlayıcı Microsoft ASP.NET MVC çerçevesi resmi bir parçası olmadığını anlamak önemlidir. Veri ek açıklamaları Model bağlayıcı Microsoft ASP.NET MVC ekibi tarafından oluşturulmuş olsa da, Microsoft resmi ürün desteği için veri ek açıklamaları Model bağlayıcı açıklanmış ve Bu öğreticide kullanılan sunmaz.

## <a name="using-the-data-annotation-model-binder"></a>Veri ek açıklama Model Bağlayıcısı kullanma

Bir ASP.NET MVC uygulamasındaki veri ek açıklamaları Model bağlayıcısını kullanmak için öncelikle Microsoft.Web.Mvc.DataAnnotations.dll derleme ve System.ComponentModel.DataAnnotations.dll derlemeye bir başvuru eklemeniz gerekir. Menü seçeneğini **proje, Başvuru Ekle**. İleri'yi **Gözat** sekmesini ve indirdiğiniz (ve sıkıştırması açılan) veri ek açıklamaları Model bağlayıcı örneği konumuna göz atın (bkz **Şekil 1**).

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Şekil 1**: Veri ek açıklamaları Model bağlayıcı için bir başvuru eklemeyi ([tam boyutlu görüntüyü görmek için tıklatın](validation-with-the-data-annotation-validators-vb/_static/image3.png))

Hem Microsoft.Web.Mvc.DataAnnotations.dll derleme hem de System.ComponentModel.DataAnnotations.dll derlemeyi seçin ve tıklayın **Tamam** düğmesi.

.NET Framework Service Pack 1 veri ek açıklamaları Model Bağlayıcısı ile birlikte System.ComponentModel.DataAnnotations.dll derleme kullanamazsınız. Veri ek açıklamaları Model bağlayıcı örneği indirmeye dahil System.ComponentModel.DataAnnotations.dll derleme sürümünü kullanmanız gerekir.

Son olarak, Global.asax dosyasında DataAnnotations Model bağlayıcı kaydetmeniz gerekir. Uygulamaya aşağıdaki kod satırını ekleyin\_Start() olay işleyicisi böylece uygulamanın\_Start() yöntemini aşağıdaki gibi görünür:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Bu kod satırı DataAnnotationsModelBinder tüm ASP.NET MVC uygulaması için varsayılan model bağlayıcısını olarak kaydeder.

## <a name="using-the-data-annotation-validator-attributes"></a>Veri ek açıklama Doğrulayıcı öznitelikleri kullanma

Veri ek açıklamaları Model bağlayıcısını kullandığınızda, doğrulama gerçekleştirmek için doğrulama öznitelikleri kullanın. System.ComponentModel.DataAnnotations ad alanı, aşağıdaki doğrulama öznitelikleri içerir:

- Aralığı – belirtilen bir aralıktaki değerleri arasında bir özelliğin değerini denk olup olmadığını doğrulamak sağlar.
- Yanıtta normal ifade – bir özelliğin değerini belirtilen normal ifade deseni ile eşleşip eşleşmediğini doğrulamanıza olanak sağlar.
- Gerekli: bir özelliği gerekli olarak işaretlemek sağlar.
- StringLength – bir dize özelliği için en fazla uzunluk belirtmenize imkan tanır.
- Doğrulama – tüm Doğrulayıcı öznitelikleri için temel sınıfı.

> [!NOTE] 
> 
> Ardından, doğrulama gereksinimlerinizi standart doğrulayıcıları biriyle tatmin edici değil her zaman yeni bir doğrulayıcı öznitelik temel doğrulama özniteliği devralarak özel Doğrulayıcı sağlayıcısı öznitelik oluşturma seçeneğiniz vardır.

Ürün sınıfında **listeleme 1** bu Doğrulayıcı özniteliklerinin nasıl kullanılacağı gösterilmektedir. Ad, açıklama ve UnitPrice özellikler işaretlendi gerektiğinde. Name özelliği, bir dize uzunluğu 10 karakter olmalıdır. Son olarak, UnitPrice özelliği bir para birimi tutarını gösteren bir normal ifade deseni eşleşmesi gerekir.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**1 listeleme**: Models\Product.vb

Ürün sınıfı bir ek özellik nasıl kullanıldığı gösterilmektedir: DisplayName özniteliğini. DisplayName özniteliğini özelliği bir hata iletisi görüntülendiğinde, özelliğin adını değiştirmenizi sağlar. Hata iletisi "UnitPrice alanını gerekiyor" yerine "Fiyat alanının gerekiyor" hata iletisini görüntüleyebilirsiniz.

> [!NOTE] 
> 
> Tamamen Doğrulayıcısı tarafından görüntülenen hata iletisini özelleştirmek istiyorsanız Doğrulayıcısı'nın ErrorMessage özelliğine benzer bir özel hata iletisi atayabilirsiniz: `<Required(ErrorMessage:="This field needs a value!")>`

Ürün sınıfında kullanabileceğiniz **listeleme 1** Create() denetleyici eylemi ile **listeleme 2**. Model durumu hataları içerdiğinde Bu denetleyici Eylem oluştur görünümünün görüntüler.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Kod 2**: Controllers\ProductController.vb

Son olarak, görünümde oluşturabilirsiniz **listeleme 3** Create() eylem sağ tıklayıp menü seçeneğini belirleyerek **Görünüm Ekle**. Kesin türü belirtilmiş görünüm ürün sınıfıyla model sınıfı oluşturun. Seçin **Oluştur** görünümü içerik açılır listede (bkz **Şekil 2**).

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Şekil 2**: Oluşturma görünümü ekleme

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Kod 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> Tarafından oluşturulan form oluştur Kimliği alanı kaldırma **Görünüm Ekle** menü seçeneği. Kimliği alanı bir kimlik sütununa karşılık olmadığından, bu alan için bir değer girin izin vermek istemezsiniz.

Bir ürün oluşturmak için form gönderme ve gerekli alanlar için değerler girin değil durumunda doğrulama hatası iletilerini **Şekil 3** görüntülenir.

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Şekil 3**: Gerekli alanlar eksik

Geçersiz bir para birimi tutarı ve hata iletisinde girerseniz **Şekil 4** görüntülenir.

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Şekil 4**: Geçersiz bir para birimi tutarı

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Veri ek açıklama doğrulayıcıları ile Entity Framework kullanma

Microsoft Entity Framework veri modeli sınıfları oluşturmak için kullanıyorsanız, doğrudan sınıflarınızı Doğrulayıcı öznitelikleri uygulanamıyor. Entity Framework Designer model sınıfları oluşturur, çünkü tasarımcıda herhangi bir değişiklik bir sonraki açışınızda model sınıflarına yaptığınız tüm değişiklikler yazılır.

Entity Framework tarafından oluşturulan sınıflar doğrulayıcıları kullanmak istiyorsanız, meta veri sınıfları oluşturmak gerekir. Doğrulayıcıları doğrulayıcıları gerçek sınıf için uygulama yerine meta veri sınıfı için geçerlidir.

Örneğin, Entity Framework kullanarak bir film sınıf oluşturduğunuz düşünün (bkz **Şekil 5**). Ayrıca, film adı ve Direktörü özellikleri gerekli özellikleri yapmak istediğinizi düşünün. Bu durumda, kısmi sınıf ve meta veri sınıfında oluşturabilirsiniz **listeleme 4**.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Şekil 5**: Entity Framework tarafından oluşturulan film sınıfı

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**4 listeleme**: Models\Movie.vb

Dosyada **listeleme 4** film ve MovieMetaData adlı iki sınıf içerir. Kısmi bir sınıf film sınıftır. DataModel.Designer.vb dosyasında yer alan Entity Framework tarafından üretilen kısmi sınıf karşılık gelir.

Şu anda, .NET framework kısmi özellikleri desteklemez. Bu nedenle, Doğrulayıcı öznitelikleri dosyasında tanımlanan film sınıf özelliklerini Doğrulayıcı öznitelikleri uygulayarak DataModel.Designer.vb dosyasında tanımlanan film sınıf özelliklerini uygulanacak bir yolu yoktur **4listeleme**.

Film kısmi sınıf'ın MovieMetaData sınıfa işaret eden MetadataType özniteliğiyle donatılmış dikkat edin. MovieMetaData sınıfı proxy özellikleri film sınıf özelliklerini içerir.

Doğrulayıcı öznitelikleri MovieMetaData sınıfının özelliklerine uygulanır. Başlık, Müdür ve DateReleased özellikleri tüm gerekli özellikleri olarak işaretlenir. 5'ten daha az karakter içeren bir dize Yöneticisi özelliği atanması gerekir. Son olarak, DisplayName özniteliğini "tarih Serbest alan gereklidir."gibi bir hata iletisi görüntülemek için DateReleased özelliğine uygulanır hata yerine "DateReleased alan gereklidir."

> [!NOTE] 
> 
> Proxy özellikleri MovieMetaData sınıfında aynı türlerine karşılık gelen özelliklerinde film sınıfı temsil eden gerekmez dikkat edin. Örneğin, Müdür film sınıfındaki bir dize özelliğini ve bir nesne özelliği MovieMetaData sınıfında özelliğidir.

Sayfanın **Şekil 6** film özelliklerini geçersiz değerler girdiğinizde, döndürülen hata iletilerini gösterir.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Şekil 6**: Entity Framework ile doğrulayıcıları kullanma ([tam boyutlu görüntüyü görmek için tıklatın](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>Özet

Bu öğreticide bir ASP.NET MVC uygulaması içindeki doğrulama gerçekleştirmek için veri ek açıklama Model bağlayıcı yararlanmak öğrendiniz. Farklı türde gerekli gibi Doğrulayıcı öznitelikleri ve StringLength öznitelikleri kullanmayı öğrendiniz. Ayrıca Microsoft Entity Framework ile çalışırken bu öznitelikler kullanmayı öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](validating-with-a-service-layer-vb.md)
