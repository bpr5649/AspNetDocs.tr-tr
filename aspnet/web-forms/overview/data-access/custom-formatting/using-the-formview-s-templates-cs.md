---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
title: FormView şablonları (C#) kullanarak | Microsoft Docs
author: rick-anderson
description: DetailsView FormView alanlarının oluşur değil. Bunun yerine, FormView şablonları kullanılarak işlenir. Bu öğreticide F. kullanarak inceleyeceğiz...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d3f062af-88cf-426d-af44-e41f32c41672
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
msc.type: authoredcontent
ms.openlocfilehash: d275e3b154ca3397294d6cd0924cb6a50bbcef9a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395543"
---
# <a name="using-the-formviews-templates-c"></a>FormView şablonları (C#) kullanma

tarafından [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Örnek uygulamayı indirin](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_14_CS.exe) veya [PDF olarak indirin](using-the-formview-s-templates-cs/_static/datatutorial14cs1.pdf)

> DetailsView FormView alanlarının oluşur değil. Bunun yerine, FormView şablonları kullanılarak işlenir. FormView kullanarak inceleyeceğiz Bu öğreticide, verileri daha az katı bir görünümünü sunmak için denetler.


## <a name="introduction"></a>Giriş

Son iki öğreticilerde TemplateField kullanma GridView ve DetailsView denetimlerini çıkışları özelleştirme gördük. TemplateField içeriği için yüksek oranda özelleştirilmiş için belirli bir alan için izin ver, ancak sonunda GridView ve DetailsView yerine boxy, kılavuz benzeri bir görünüm vardır. Böyle bir kılavuz benzeri düzeni birçok senaryo için ideal olan, ancak bazen daha akıcı, daha az katı bir görüntü gereklidir. Tek bir kaydını görüntülerken, akıcı bir düzen FormView denetimini kullanarak mümkündür.

DetailsView FormView alanlarının oluşur değil. Bir FormView'da için BoundField veya TemplateField ekleyemezsiniz. Bunun yerine, FormView şablonları kullanılarak işlenir. FormView tek bir TemplateField içeren bir DetailsView denetimi olarak düşünün. FormView şablonları aşağıdaki destekler:

- `ItemTemplate` bir FormView'da görüntülenen belirli bir kayıtla işlemek için kullanılan
- `HeaderTemplate` bir isteğe bağlı üst bilgi satırı belirtmek için kullanılır
- `FooterTemplate` İsteğe bağlı alt satır belirtmek için kullanılır
- `EmptyDataTemplate` zaman FormView `DataSource` herhangi bir kayıt eksik `EmptyDataTemplate` yerine kullanılan `ItemTemplate` denetimin biçimlendirme işlemek için
- `PagerTemplate` disk belleği etkin olan FormViews için disk belleği arabirimini özelleştirmek için kullanılabilir
- `EditItemTemplate` / `InsertItemTemplate` ekleme arabirimi ve düzenleme arabirimi bu tür işlevselliği destekleyen FormViews için özelleştirmek için kullanılan

Bu öğreticide inceleyeceğiz FormView denetim ürünleri daha az katı bir görünümünü sunmak için kullanma. Ad, kategori, tedarikçi ve vb. FormView ait alanları yerine `ItemTemplate` header öğesi bir birleşimini kullanarak bu değerleri gösterir ve `<table>` (bkz. Şekil 1).


[![FormView kesilmeler DetailsView içinde görülen kılavuz benzeri düzeni](using-the-formview-s-templates-cs/_static/image2.png)](using-the-formview-s-templates-cs/_static/image1.png)

**Şekil 1**: FormView keser Grid-Like Düzen görülen yetersiz içinde DetailsView ([tam boyutlu görüntüyü görmek için tıklatın](using-the-formview-s-templates-cs/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-formview"></a>1. Adım: FormView için veri bağlama

Açık `FormView.aspx` sayfa ve bir FormView'da tasarımcı araç kutusundan sürükleyin. FormView eklenmediği bize söyleyen bir gri kutu olarak görünür, bir `ItemTemplate` gereklidir.


[![Tasarımcıda bir ItemTemplate sağlanmadıkça FormView işlenemiyor](using-the-formview-s-templates-cs/_static/image5.png)](using-the-formview-s-templates-cs/_static/image4.png)

**Şekil 2**: FormView olamaz işlenecek Tasarımcısı kadar içinde bir `ItemTemplate` sağlanır ([tam boyutlu görüntüyü görmek için tıklatın](using-the-formview-s-templates-cs/_static/image6.png))


`ItemTemplate` FormView Tasarımcısı aracılığıyla veri kaynak denetimi bağlama tarafından otomatik olarak oluşturulmuş veya (bildirim temelli söz dizimi aracılığıyla) el ile oluşturulabilir. Bu otomatik olarak oluşturulan `ItemTemplate` içeren liste her bir alan ve bir etiket adı ayarlanmış denetim HTML `Text` özellik alan değerine bağlı. Bu yaklaşım ayrıca otomatik oluşturur-bir `InsertItemTemplate` ve `EditItemTemplate`, veri kaynak denetimi tarafından döndürülen veri alanlarının her ikisi de giriş denetimleri ile doldurulur.

Otomatik-şablon oluşturmak istiyorsanız, FormView akıllı etiketten çağıran yeni ObjectDataSource denetim ekleme `ProductsBLL` sınıfın `GetProducts()` yöntemi. Bu bir FormView ile oluşturacak bir `ItemTemplate`, `InsertItemTemplate`, ve `EditItemTemplate`. Kaynak görünümden Kaldır `InsertItemTemplate` ve `EditItemTemplate` ilginizi değiliz bu yana bir FormView'da henüz ekleme veya düzenleme destekleyen oluşturma. Sonraki içinde Biçimlendirmeyi Temizle `ItemTemplate` böylece çalışabilmesi için temiz bir maskeleme görüntüsü sunuyoruz.

Bunun yerine temponuzda, `ItemTemplate` el ile ekleyin ve araç kutusundan tasarımcıya sürükleyerek ObjectDataSource yapılandırın. Ancak, FormView veri kaynağı Tasarımcısı'ndan ayarlamanız gerekmez. Bunun yerine, kaynak görünümüne gidin ve FormView el ile ayarlamanız `DataSourceID` özelliğini `ID` ObjectDataSource değeri. Ardından, el ile eklemeniz `ItemTemplate`.

Hangi yaklaşımın bağımsız olarak yararlanmak, bu noktada, FormView bildirim temelli biçimlendirme gibi görünür verdi:


[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample1.aspx)]

FormView akıllı etiketinde etkinleştirme sayfalama onay için bir dakikanızı ayırın; Bu ekler `AllowPaging="True"` FormView bildirim temelli söz dizimi özniteliği. Ayrıca, `EnableViewState` özelliğini False.

## <a name="step-2-defining-theitemtemplates-markup"></a>2. Adım: Tanımlama`ItemTemplate`'s biçimlendirme

Disk belleği desteklemek için yapılandırılmış ve ObjectDataSource denetimine bağlı FormView ile içeriğini belirtmek hazırız `ItemTemplate`. Bu öğreticide, github'dan görüntülenen ürünün ada sahip bir `<h3>` başlığı. HTML kullanalım `<table>` burada ilk ve üçüncü sütun özellik adlarını listelemek ve dördüncü ve saniye değerlerini listesinde bir dört sütunlu tabloda kalan ürün özelliklerini görüntülemek için.

Bu işaretleme Tasarımcısı'nda FormView şablon düzenleme arabirimi aracılığıyla girilen veya bildirim temelli söz dizimi aracılığıyla elle girilebilir. Şablonları ile çalışırken, genellikle, daha hızlı doğrudan bildirim temelli söz dizimi ile çalışma, ancak herhangi bir teknik en rahat araştırmalarında buluyorum.

FormView bildirim temelli biçimlendirme sonra aşağıdaki biçimlendirme gösterir `ItemTemplate`'s yapısı tamamlandı:


[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample2.aspx)]

Dikkat veri bağlama söz dizimi - `<%# Eval("ProductName") %>`için örnek doğrudan şablonun çıkışını yerleştirilebilir. Diğer bir deyişle, bir etiket denetimin atanamaz `Text` özelliği. Örneğin, sahibiz `ProductName` görüntülenen değeri bir `<h3>` öğesini kullanarak `<h3><%# Eval("ProductName") %></h3>`, Chai olarak işlenir, ürünün `<h3>Chai</h3>`.

`ProductPropertyLabel` Ve `ProductPropertyValue` CSS sınıfları ürün özellik adlarını ve değerlerini stilini belirtmek için kullanılan `<table>`. Bu CSS sınıfları tanımlanan `Styles.css` ve özellik adları kalın ve sağa hizalı olmasını ve özellik değerlerine doldurma hakkı eklemek neden olabilir.

Olduğundan hiçbir CheckBoxFields FormView ile kullanılabilir göstermek için `Discontinued` değeri bir onay kutusu biz kendi onay kutusu denetimi eklemeniz gerekir. `Enabled` Özelliği ayarlanmışsa False, salt okunur yapma ve CheckBox'ın `Checked` özelliğinin değerine bağlı `Discontinued` veri alanı.

İle `ItemTemplate` tam, ürün bilgilerini daha akıcı bir şekilde da görüntülenir. Bu öğreticide (Şekil 4) FormView tarafından oluşturulan çıktı DetailsView çıkış son öğreticiden (Şekil 3) karşılaştırın.


[![Katı DetailsView çıkış](using-the-formview-s-templates-cs/_static/image8.png)](using-the-formview-s-templates-cs/_static/image7.png)

**Şekil 3**: Katı DetailsView çıkış ([tam boyutlu görüntüyü görmek için tıklatın](using-the-formview-s-templates-cs/_static/image9.png))


[![Akıcı FormView çıkış](using-the-formview-s-templates-cs/_static/image11.png)](using-the-formview-s-templates-cs/_static/image10.png)

**Şekil 4**: Sıvı FormView çıkış ([tam boyutlu görüntüyü görmek için tıklatın](using-the-formview-s-templates-cs/_static/image12.png))


## <a name="summary"></a>Özet

GridView ve DetailsView denetimlerini kullanma özelleştirilmiş çıktılarını varken hem hala verilerine bir kılavuz benzeri, boxy biçimde sunar. Tek bir kaydı gerektiğinde gösterilecek destekleyebilirsiniz daha az katı bir düzen kullanarak FormView ideal bir seçimdir. DetailsView gibi tek bir kayıttan FormView işler kendi `DataSource`, ancak DetailsView aksine yalnızca şablonları oluşur ve alanlarını desteklemez.

Bu öğreticide gördüğümüz gibi tek bir kaydı görüntülenirken FormView için daha esnek bir düzen sağlar. İleride hangi düzeyde esneklik FormsView olarak sağlar, ancak (örneğin, GridView) birden çok kayıt görüntüleyemiyoruz DataList ve Repeater denetimleri inceleyeceğiz öğreticiler.

Mutlu programlama!

## <a name="about-the-author"></a>Yazar hakkında

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yazar yedi ASP/ASP.NET kitaplardan ve poshbeauty.com sitesinin [4GuysFromRolla.com](http://www.4guysfromrolla.com), Microsoft Web teknolojileriyle beri 1998'de çalışmaktadır. Scott, bağımsız Danışman, Eğitimci ve yazıcı çalışır. En son nitelemiştir olan [ *Unleashed'i öğretin kendiniz ASP.NET 2.0 24 saat içindeki*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). He adresinden ulaşılabilir [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) veya kendi blog hangi bulunabilir [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Özel teşekkürler

Bu öğretici serisinde, birçok yararlı Gözden Geçiren tarafından gözden geçirildi. Bu öğreticide E.R. için Gözden Geçiren sağlama Gilmore. Yaklaşan My MSDN makaleleri gözden geçirme ilgileniyor musunuz? Bu durumda, bir satır bana bırak [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](using-templatefields-in-the-detailsview-control-cs.md)
> [İleri](displaying-summary-information-in-the-gridview-s-footer-cs.md)
