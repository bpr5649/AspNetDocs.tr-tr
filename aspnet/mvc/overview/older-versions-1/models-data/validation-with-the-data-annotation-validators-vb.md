---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Veri Ek Açıklama Doğrulayıcıları (VB) ile doğrulama | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET bir MVC uygulaması içinde doğrulama gerçekleştirmek için Veri Açıklama Modeli Bağlayıcısı'ndan yararlanın. Farklı doğrulama türlerini nasıl kullanacağınızı öğrenin...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542644"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Veri Ek Açıklama Doğrulayıcıları ile Doğrulama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET bir MVC uygulaması içinde doğrulama gerçekleştirmek için Veri Açıklama Modeli Bağlayıcısı'ndan yararlanın. Microsoft Entity Framework'de farklı doğrulama özniteliklerini nasıl kullanacağınızı ve bunlarla nasıl çalışacağınızı öğrenin.

Bu eğitimde, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirmek için Veri Ek Açıklama doğrulayıcılarını nasıl kullanacağınızı öğrenirsiniz. Veri Ek Açıklama doğrulayıcılarını kullanmanın avantajı, bir sınıf özelliğine yalnızca bir veya daha fazla öznitelik (Gerekli veya StringLength özniteliği gibi) ekleyerek doğrulama gerçekleştirmenize olanak sağlamasıdır.

Veri Ek Açıklama doğrulayıcılarını kullanamadan önce Veri Ek Açıklamaları Model Bağlayıcısını indirmeniz gerekir. [CodePlex](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)web sitesinden Veri Ek Açıklamaları Model Bağlayıcı Örneğini buraya tıklayarak indirebilirsiniz.

Veri Ek Açıklamaları Modeli Bağlayıcısı'nın Microsoft ASP.NET MVC çerçevesinin resmi bir parçası olmadığını anlamak önemlidir. Veri Ek Açıklamaları Model Bağlayıcısı Microsoft ASP.NET MVC ekibi tarafından oluşturulmuş olsa da, Microsoft bu öğreticide açıklanan ve kullanılan Veri Ek Açıklamaları Modeli Bağlayıcısı için resmi ürün desteği sunmaz.

## <a name="using-the-data-annotation-model-binder"></a>Veri Açıklama Modeli Bağlayıcısını Kullanma

Veri Ek Açıklamaları Model Bağlayıcısı'nı ASP.NET bir MVC uygulamasında kullanmak için öncelikle Microsoft.Web.Mvc.DataAnnotations.dll derlemesine ve System.ComponentModel.DataAnnotations.dll derlemesine bir başvuru eklemeniz gerekir. Menü seçeneğini seçin **Proje, Referans Ekle**. Sonraki **gözat** sekmesini tıklatın ve Veri Ek Açıklamaları Model Bağlayıcı örnek indirilen (ve günülünü) indirdiğiniz konuma göz atın **(Bkz. Şekil 1).**

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Şekil 1**: Veri Ek Açıklamaları Model Bağlayıcısına başvuru ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](validation-with-the-data-annotation-validators-vb/_static/image3.png))

Hem Microsoft.Web.Mvc.DataAnnotations.dll derlemesini hem de System.ComponentModel.DataAnnotations.dll derlemesini seçin ve **Tamam** düğmesini tıklatın.

System.ComponentModel.DataAnnotations.dll derlemesi .NET Framework Service Pack 1 ile Birlikte Veri Ek Açıklamaları Model Bağlayıcısı ile kullanamazsınız. Data Ek Açıklamaları Model Bağlayıcı Örnek indir ile birlikte System.ComponentModel.DataAnnotations.dll derleme sürümünü kullanmanız gerekir.

Son olarak, Global.asax dosyasına DataAnnotations Model Bağlayıcısı'nı kaydetmeniz gerekir. Uygulama\_Başlat() yönteminin\_aşağıdaki gibi görünmesi için Uygulama Başlat() olay işleyicisine aşağıdaki kod satırını ekleyin:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Bu kod satırı, DataAnnotationsModelBinder'i tüm ASP.NET MVC uygulaması için varsayılan model bağlayıcısı olarak kaydeder.

## <a name="using-the-data-annotation-validator-attributes"></a>Veri Ek Açıklama Doğrulaması Doğrulaması Özniteliklerini Kullanma

Veri Ek Açıklamaları Model Bağlayıcısı'nı kullandığınızda, doğrulama gerçekleştirmek için doğrulayıcı öznitelikleri ni kullanırsınız. System.ComponentModel.DataAnnotations ad alanı aşağıdaki doğrulayıcı öznitelikleri içerir:

- Aralık – Bir özelliğin değerinin belirli bir değer aralığı arasında düşüp düşmediğini doğrulamanızı sağlar.
- RegularExpression – Bir özelliğin değerinin belirli bir normal ifade deseniyle eşleşip eşleşmediğini doğrulamanızı sağlar.
- Gerekli – Bir özelliği gerektiği gibi işaretlemenizi sağlar.
- StringLength – Bir dize özelliği için maksimum uzunluk belirtmenizi sağlar.
- Doğrulama – Tüm doğrulayıcı öznitelikleri için taban sınıf.

> [!NOTE] 
> 
> Doğrulama gereksinimleriniz standart doğrulayıcılardan herhangi biri tarafından karşılanmadıysa, temel Doğrulama özniteliğinden yeni bir doğrulayıcı özniteliği devralarak her zaman özel bir doğrulayıcı özniteliği oluşturma seçeneğiniz vardır.

**Listeleme 1'deki** Ürün sınıfı, bu geçerliniteliklerin nasıl kullanılacağını gösterir. Ad, Açıklama ve UnitPrice özellikleri gerektiği gibi işaretlenir. Ad özelliği, 10 karakterden az bir dize uzunluğuna sahip olmalıdır. Son olarak, UnitPrice özelliği, para birimi tutarını temsil eden normal bir ifade deseniyle eşleşmelidir.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**İlan 1**: Modeller\Product.vb

Ürün sınıfı, ek bir öznitelik olan DisplayName özniteliğinin nasıl kullanılacağını gösterir. DisplayName özniteliği, özellik bir hata iletisinde görüntülendiğinde özelliğin adını değiştirmenize olanak tanır. "UnitPrice alanı gereklidir" hata iletisini görüntülemek yerine hata iletisini görüntüleyebilirsiniz "Fiyat alanı gereklidir".

> [!NOTE] 
> 
> Bir doğrulayıcı tarafından görüntülenen hata iletisini tamamen özelleştirmek istiyorsanız, geçerlinin ErrorMessage özelliğine şu şekilde özel bir hata iletisi atayabilirsiniz:`<Required(ErrorMessage:="This field needs a value!")>`

**Listeleme 1'de** Ürün sınıfını, **Listeleme 2'deki**Create() denetleyici eylemiyle kullanabilirsiniz. Bu denetleyici eylem, model durumu herhangi bir hata içerdiğinde Oluştur görünümünü yeniden görüntüler.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Listeleme 2**: Denetleyiciler\ProductController.vb

Son olarak, Create() eylemine sağ tıklayarak ve menü seçeneğini seçerek **Görünüm Ekle**seçeneğini seçerek **Listeleme 3'te** görünüm oluşturabilirsiniz. Model sınıfı olarak Ürün sınıfıyla güçlü bir şekilde yazılan bir görünüm oluşturun. Görünüm içeriği açılır listesinden **Oluştur'u** seçin **(Bkz. Şekil 2).**

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Şekil 2**: Create View ekleme

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Listeleme 3**: Görünümler\Ürün\Create.aspx

> [!NOTE] 
> 
> **Görünüm Ekle** seçeneği tarafından oluşturulan Oluştur formundan Id alanını kaldırın. Kimlik alanı bir Kimlik sütununa karşılık geldiği için, kullanıcıların bu alan için bir değer girmesine izin vermek istemezsiniz.

Bir Ürün oluşturma formunu gönderirseniz ve gerekli alanlar için değerler girmezseniz, Şekil **3'teki** doğrulama hatası iletileri görüntülenir.

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Şekil 3**: Eksik gerekli alanlar

Geçersiz bir para birimi tutarı girerseniz, **Şekil 4'teki** hata iletisi görüntülenir.

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Şekil 4**: Geçersiz para birimi tutarı

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Varlık Çerçevesi ile Veri EkAçıklama Doğrulayıcıları Kullanma

Veri modeli sınıflarınızı oluşturmak için Microsoft Entity Framework'ü kullanıyorsanız, geçerlilik özniteliklerini doğrudan sınıflarınıza uygulayamazsınız. Varlık Çerçeve Tasarımcısı model sınıflarını oluşturduğundan, model sınıflarında yaptığınız değişiklikler, Tasarımcı'da bir sonraki değişiklik yaptığınızda üzerine yazılır.

Varlık Çerçevesi tarafından oluşturulan sınıfları ile doğrulayıcıları kullanmak istiyorsanız, meta veri sınıfları oluşturmanız gerekir. Doğrulayıcıları gerçek sınıfa uygulamak yerine meta veri sınıfına uygularsınız.

Örneğin, Varlık Çerçevesi'ni kullanarak bir Film sınıfı oluşturduğunuzu düşünün **(Bkz. Şekil 5).** Ayrıca, Film Başlığı ve Yönetmen özellikleri gerekli özellikleri yapmak istediğinizi düşünün. Bu durumda, **Listeleme 4'te**kısmi sınıf ve meta veri sınıfı oluşturabilirsiniz.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Şekil 5**: Entity Framework tarafından oluşturulan film sınıfı

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**İlan 4**: Modeller\Movie.vb

**Listeleme 4'teki** dosya, Film ve MovieMetaData adlı iki sınıf içerir. Film sınıfı kısmi bir sınıftır. DataModel.Designer.vb dosyasında yer alan Entity Framework tarafından oluşturulan kısmi sınıfa karşılık gelir.

Şu anda,.NET çerçevesi kısmi özellikleri desteklemez. Bu nedenle, **Listeleme 4'teki**dosyada tanımlanan Film sınıfının özelliklerine doğrulayıcı öznitelikleri ni uygulayarak DataModel.Designer.vb dosyasında tanımlanan Film sınıfının özelliklerine doğrulayıcı özniteliklerini uygulamanın bir yolu yoktur.

Film kısmi sınıfının MovieMetaData sınıfına işaret eden bir MetadataType özniteliği ile dekore edildiğine dikkat edin. MovieMetaData sınıfı, Film sınıfının özellikleri için proxy özellikleri içerir.

Doğrulayıcı öznitelikleri MovieMetaData sınıfının özelliklerine uygulanır. Başlık, Müdür ve DateReleased özelliklerinin tümü gerekli özellikler olarak işaretlenir. Yönetmen özelliğine 5 karakterden az karakter içeren bir dize atanmalıdır. Son olarak, DisplayName özniteliği DateReleased özelliğine "Çıkış Tarihi alanı gereklidir" gibi bir hata iletisi görüntülemek için uygulanır. hata yerine "DateReleased alanı gereklidir."

> [!NOTE] 
> 
> MovieMetaData sınıfındaki proxy özelliklerinin Film sınıfındaki ilgili özelliklerle aynı türleri temsil etmesi gerekmediğini unutmayın. Örneğin, Yönetmen özelliği Film sınıfında bir dize özelliği ve MovieMetaData sınıfında bir nesne özelliğidir.

**Şekil 6'daki** sayfa, Film özellikleri için geçersiz değerler girdiğinizde döndürülen hata iletilerini gösterir.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Şekil 6**: Varlık Çerçevesi ile doğrulayıcılar kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>Özet

Bu eğitimde, ASP.NET bir MVC uygulaması içinde doğrulama gerçekleştirmek için Veri Ek Açıklama Modeli Bağlayıcısı'ndan nasıl yararlanabileceğinizi öğrendiniz. Gerekli ve StringLength öznitelikleri gibi farklı doğrulama özniteliklerini kullanmayı öğrendiniz. Microsoft Entity Framework ile çalışırken bu öznitelikleri nasıl kullanacağınızı da öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](validating-with-a-service-layer-vb.md)
