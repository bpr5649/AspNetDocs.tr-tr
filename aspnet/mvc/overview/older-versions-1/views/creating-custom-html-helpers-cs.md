---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Özel HTML Yardımcıları Oluşturma (C#) | Microsoft Dokümanlar
author: rick-anderson
description: Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Helper'dan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542566"
---
# <a name="creating-custom-html-helpers-c"></a>Özel HTML Yardımcıları Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.

Bu öğreticinin amacı, MVC görünümleriniz içinde kullanabileceğiniz özel HTML Yardımcıları'nı nasıl oluşturabileceğinizi göstermektir. HTML Yardımcıları'ndan yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken sıkıcı HTML etiketleri yazma miktarını azaltabilirsiniz.

Bu öğreticinin ilk bölümünde, bazı mevcut HTML Yardımcıları ASP.NET MVC çerçeve ile birlikte açıklar. Daha sonra, özel HTML Yardımcıları oluşturmanın iki yöntemini açıklıyorum: Statik bir yöntem oluşturarak ve bir uzantı yöntemi oluşturarak özel HTML Yardımcıları oluşturmanın nasıl yapılacağını açıklıyorum.

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

Örneğin, Listeleme 1'deki formu göz önünde bulundurun. Bu form, standart HTML Yardımcılarından ikisinin yardımıyla işlenir (Bkz. Şekil 1). Bu form, `Html.BeginForm()` `Html.TextBox()` basit bir HTML formu oluşturmak için Yardımcı ve Yardımcı yöntemlerini kullanır.

[![HTML Yardımcıları ile işlenen sayfa](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-cs/_static/image3.png))

**İlan 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

HTML.BeginForm() Yardımcı yöntemi, HTML `<form>` etiketlerini açmak ve kapatmak için kullanılır. Yöntemin `Html.BeginForm()` bir using deyimi içinde çağrıldığına dikkat edin. Using deyimi, etiketin `<form>` kullanarak bloğun sonunda kapatılmasını sağlar.

İsterseniz, bir kullanarak blok oluşturmak yerine, etiketi kapatmak için Html.EndForm() `<form>` Yardımcı yöntemini arayabilirsiniz. Size en sezgisel görünen açılış `<form>` ve kapanış etiketini oluşturmak için hangi yaklaşımı kullanırsanız kullanın.

`Html.TextBox()` Yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için Listeleme 1'de kullanılır. Tarayıcınızda görünüm kaynağını seçerseniz, Listeleme 2'deki HTML kaynağını görürsünüz. Kaynağın standart HTML etiketleri içerdiğine dikkat edin.

> [!IMPORTANT]
> -HTML `Html.TextBox()`Yardımcısının `<%= %>` `<% %>` etiketler yerine etiketlerle işlendirilene dikkat edin. Eşit işareti eklemezseniz, tarayıcıya hiçbir şey işlenmez.

ASP.NET MVC çerçevesi küçük bir yardımcı kümesi içerir. Büyük olasılıkla, özel HTML Yardımcıları ile MVC çerçevesini genişletmeniz gerekir. Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrenirsiniz.

**Listeleme 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Statik Yöntemlerle HTML Yardımcıları Oluşturma

Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, dize döndüren statik bir yöntem oluşturmaktır. Örneğin, html `<label>` etiketi işleyen yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün. Listeleme 2'deki sınıfı kullanarak `<label>` bir .

**Listeleme 2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

Listeleme 2'deki sınıfın özel bir özelliği yoktur. Yöntem `Label()` sadece bir dize döndürür.

Listeleme 3'teki değiştirilmiş `LabelHelper` Dizin `<label>` görünümü, HTML etiketlerini işlemek için kullanılır. Görünümün ad alanını `<%@ imports %>` içeri iten bir yönerge içerdiğine dikkat edin. `Application1.Helpers`

**Listeleme 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Uzantı Yöntemleriyle HTML Yardımcıları Oluşturma

ASP.NET MVC çerçevesine dahil edilen standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir. Uzantı yöntemleri, varolan bir sınıfa yeni yöntemler eklemenize olanak tanır. BIR HTML Yardımcı yöntemi oluştururken, görünümün Html özelliğiyle temsil edilen HtmlHelper sınıfına yeni yöntemler eklersiniz.

Listeleme 3'teki sınıf, adlı `HtmlHelper` `Label()`sınıfa bir uzantı yöntemi ekler. Bu sınıf hakkında dikkat etmelisiniz birkaç şey vardır. İlk olarak, sınıfın statik bir sınıf olduğuna dikkat edin. Statik bir sınıfa sahip bir uzantı yöntemi tanımlamanız gerekir.

İkinci olarak, yöntemin `Label()` ilk parametreanahtar kelimesi `this`önce olduğunu unutmayın. Uzantı yönteminin ilk parametresi, uzantı yönteminin genişletir sınıfını gösterir.

**İlan 3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Bir uzantı yöntemi oluşturduktan ve uygulamanızı başarıyla oluşturduktan sonra, uzantı yöntemi visual studio intellisense'de sınıfın diğer tüm yöntemleri gibi görünür (Bkz. Şekil 2). Tek fark, uzantı yöntemlerinin yanlarında özel bir sembolle (aşağı doğru bir ok simgesi) görünmesidir.

[![Html.Label() uzantı yöntemini kullanma](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Şekil 02**: Html.Label() uzantı yöntemini kullanma ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-custom-html-helpers-cs/_static/image6.png))

Listeleme 4'teki değiştirilmiş Dizin görünümü, tüm etiketlerini işlemek `<label>` için Html.Label() uzantı yöntemini kullanır.

**İlan 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Özet

Bu eğitimde, özel HTML Yardımcıları oluşturmanın iki yöntemini öğrendiniz. İlk olarak, bir dize `Label()` döndüren statik bir yöntem oluşturarak özel bir HTML Yardımcısı oluşturmayı öğrendiniz. Ardından, sınıfta bir uzantı `Label()` yöntemi oluşturarak özel bir HTML `HtmlHelper` Yardımcı yöntemi oluşturmayı öğrendiniz.

Bu öğretici, ben son derece basit bir HTML Helper yöntemi bina üzerinde duruldu. Bir HTML Yardımcısının istediğiniz kadar karmaşık olabileceğini fark edin. Ağaç görünümleri, menüler veya veritabanı veri tabloları gibi zengin içerik oluşturan HTML Yardımcıları oluşturabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-views-overview-cs.md)
> [Sonraki](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
