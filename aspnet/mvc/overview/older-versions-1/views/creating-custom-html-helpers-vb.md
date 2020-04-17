---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Özel HTML Yardımcıları Oluşturma (VB) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Helper'dan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 52f16bf666edc9f1c95c01faf004e303fcb6a0b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542514"
---
# <a name="creating-custom-html-helpers-vb"></a>Özel HTML Yardımcıları Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.

Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.

Bu öğreticinin ilk bölümünde, bazı mevcut HTML Yardımcıları ASP.NET MVC çerçeve ile birlikte açıklar. Daha sonra, özel HTML Yardımcıları oluşturmanın iki yöntemini açıklıyorum: Paylaşılan bir yöntem oluşturarak ve bir uzantı yöntemi oluşturarak özel HTML Yardımcıları oluşturmanın nasıl yapılacağını açıklıyorum.

## <a name="understanding-html-helpers"></a>HTML Yardımcılarını Anlama

HTML Yardımcısı, dize döndüren bir yöntemdir. Dize istediğiniz herhangi bir içerik türünü temsil edebilir. Örneğin, HTML `<input>` ve `<img>` etiketler gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz. Sekme şeridi veya veritabanı verilerinin HTML tablosu gibi daha karmaşık içerik işlemek için HTML Yardımcıları'nı da kullanabilirsiniz.

ASP.NET MVC çerçevesi aşağıdaki standart HTML Yardımcıları kümesini içerir (bu tam bir liste değildir):

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

Örneğin, Listeleme 1'deki formu göz önünde bulundurun. Bu form, standart HTML Yardımcılarından ikisinin yardımıyla işlenir (Bkz. Şekil 1). Bu form `Html.BeginForm()` ve `Html.TextBox()` Yardımcı yöntemleri kullanır.

[![HTML Yardımcıları ile işlenen sayfa](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-vb/_static/image3.png))

**İlan 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()` Yardımcı yöntemi, HTML `<form>` etiketlerini açmak ve kapatmak için kullanılır. Yöntemin `Html.BeginForm()` bir using deyimi içinde çağrıldığına dikkat edin. Using deyimi, etiketin `<form>` kullanarak bloğun sonunda kapatılmasını sağlar.

İsterseniz, bir kullanarak blok oluşturmak yerine, etiketi kapatmak için Html.EndForm() `<form>` Yardımcı yöntemini arayabilirsiniz. Size en sezgisel görünen açılış `<form>` ve kapanış etiketini oluşturmak için hangi yaklaşımı kullanırsanız kullanın.

`Html.TextBox()` Yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için Listeleme 1'de kullanılır. Tarayıcınızda görünüm kaynağını seçerseniz, Listeleme 2'deki HTML kaynağını görürsünüz. Kaynağın standart HTML etiketleri içerdiğine dikkat edin.

> [!IMPORTANT]
> -HTML `Html.TextBox()`Yardımcısının `<%= %>` `<% %>` etiketler yerine etiketlerle işlendirilene dikkat edin. Eşit işareti eklemezseniz, tarayıcıya hiçbir şey işlenmez.

ASP.NET MVC çerçevesi küçük bir yardımcı kümesi içerir. Büyük olasılıkla, özel HTML Yardımcıları ile MVC çerçevesini genişletmeniz gerekir. Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrenirsiniz.

**Listeleme 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>Paylaşılan Yöntemlerle HTML Yardımcıları Oluşturma

Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren paylaşılan bir yöntem oluşturmaktır. Örneğin, html `<label>` etiketi işleyen yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün. Listeleme 2'deki sınıfı kullanarak `<label>`bir .

**Listeleme 2 –`Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

Listeleme 2'deki sınıfın özel bir özelliği yoktur. Yöntem `Label()` sadece bir dize döndürür.

Listeleme 3'teki değiştirilmiş `LabelHelper` Dizin `<label>` görünümü, HTML etiketlerini işlemek için kullanılır. Görünümün Application1.Helpers ad alanını içeri iten bir `<%@ imports %>` yönerge içerdiğine dikkat edin.

**Listeleme 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Uzantı Yöntemleriyle HTML Yardımcıları Oluşturma

ASP.NET MVC çerçevesine dahil edilen standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir. Uzantı yöntemleri, varolan bir sınıfa yeni yöntemler eklemenize olanak tanır. BIR HTML Yardımcısı yöntemi oluştururken, görünümün `HtmlHelper` Html özelliğiyle temsil edilen sınıfa yeni yöntemler eklersiniz.

Listeleme 3'teki Visual Basic `Label()` `HtmlHelper` modülü, sınıfa adlandırılmış bir uzantı yöntemi ekler. Bu modül hakkında dikkat etmelisiniz birkaç şey vardır. İlk olarak, modülün öznitelik `<Extension()>` ile dekore edilmiş olduğunu unutmayın. Bu özniteliği kullanmak `System.Runtime.CompilerServices` için, ad alanını almanız gerekir

İkinci olarak, yöntemin ilk `Label()` parametresinin `HtmlHelper` sınıfı temsil ettiğine dikkat edin. Uzantı yönteminin ilk parametresi, uzantı yönteminin genişletir sınıfını gösterir.

**İlan 3 –`Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

Bir uzantı yöntemi oluşturduktan ve uygulamanızı başarıyla oluşturduktan sonra, uzantı yöntemi visual studio intellisense'de sınıfın diğer tüm yöntemleri gibi görünür (Bkz. Şekil 2). Tek fark, uzantı yöntemlerinin yanlarında özel bir sembolle (aşağı doğru bir ok simgesi) görünmesidir.

[![Html.Label() uzantı yöntemini kullanma](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**Şekil 02**: Html.Label() uzantı yöntemini kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-vb/_static/image6.png))

Listeleme 4'teki değiştirilmiş Dizin görünümü, tüm etiket &lt;&gt; etiketlerini işlemek için Html.Label() uzantı yöntemini kullanır.

**İlan 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>Özet

Bu eğitimde, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrendiniz. İlk olarak, bir dize `Label()` döndüren paylaşılan bir yöntem oluşturarak özel bir HTML Yardımcısı oluşturmayı öğrendiniz. Ardından, sınıfta bir uzantı `Label()` yöntemi oluşturarak özel bir HTML `HtmlHelper` Yardımcı yöntemi oluşturmayı öğrendiniz.

Bu öğretici, ben son derece basit bir HTML Helper yöntemi bina üzerinde duruldu. Bir HTML Yardımcısının istediğiniz kadar karmaşık olabileceğini fark edin. Ağaç görünümleri, menüler veya veritabanı veri tabloları gibi zengin içerik oluşturan HTML Yardımcıları oluşturabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-views-overview-vb.md)
> [Sonraki](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
