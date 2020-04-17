---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: ComboBox Denetimini nasıl kullanırım? (VB) | Microsoft Dokümanlar
author: rick-anderson
description: ComboBox, TextBox'ın esnekliğini kullanıcıların seçebileceği seçenekler listesiyle birleştiren ASP.NET bir AJAX denetimidir.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 237e3ef864238c11fc1fb49239c3f6fa3f75537d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543073"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a>ComboBox Denetimini nasıl kullanırım? (VB)

[Microsoft](https://github.com/microsoft) tarafından

> ComboBox, TextBox'ın esnekliğini kullanıcıların seçebileceği seçenekler listesiyle birleştiren ASP.NET bir AJAX denetimidir.

Bu öğreticinin amacı AJAX Control Toolkit ComboBox denetimini açıklamaktır. ComboBox standart bir ASP.NET DropDownList denetimi ve TextBox denetimi arasında bir kombinasyon gibi çalışır. Önceden varolan bir öğe listesinden seçim yapabilir veya yeni bir öğe girebilirsiniz.

ComboBox Otomatik Tamamlama denetim genişleticibenzer, ancak denetimleri farklı senaryolarda kullanılır. Otomatik Tamamlama genişletici, eşleşen girişleri almak için bir web hizmetini sorgular. Buna karşılık ComboBox denetimi, bir dizi öğeyle baş harfe doğru başolarak ayarlanır. ComboBox denetimini kullanırken, büyük bir veri kümesiyle (milyonlarca araç parçası) çalışırken Otomatik Tamamlama genişleticisini kullanmak mantıklıdır (düzinelerce araç parçası).

## <a name="selecting-from-a-static-list-of-items"></a>Statik Öğe Listesinden seçme

ComboBox denetimini kullanarak basit bir örnek le başlayalım. Açılan listedeki öğelerin statik bir listesini görüntülemek istediğinizi düşünün. Ancak, listenin tamamlanmaması olasılığını açık bırakmak istiyorsunuz. Bir kullanıcının listeye özel bir değer girmesine izin vermek istiyorsunuz.

Yeni bir ASP.NET web formları sayfası oluşturacağız ve sayfadaki ComboBox denetimini kullanacağız. Projenize yeni ASP.NET sayfasını ekleyin ve Tasarım görünümüne geçin.

Sayfadaki ComboBox denetimini kullanmak istiyorsanız, sayfaya bir ScriptManager denetimi eklemeniz gerekir. ScriptManager denetimini AJAX Uzantıları sekmesinin altından Tasarımcı yüzeyine sürükleyin. Sayfanın üst kısmında ScriptManager denetim eklemeniz gerekir; sunucu tarafındaki &lt;form&gt; etiketinin hemen altına ekleyebilirsiniz.

Ardından, ComboBox denetimini sayfaya sürükleyin. Diğer AJAX Control Toolkit denetimleri ve kontrol genişleticiler ile Araç Kutusunda ComboBox denetimini bulabilirsiniz (bkz. şekil1).

[![Kartvizit oluşturmak için basit form](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

**Şekil 01**: Araç kutusundan ComboBox denetimini seçme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image2.png))

Statik bir seçenek listesini görüntülemek için ComboBox denetimini kullanacağız. Kullanıcı, gıdaları için belirli bir spiciness düzeyini üç seçenekarasından seçebilir: Hafif, Orta ve Sıcak (Bkz. Şekil 2).

[![Statik bir öğe listesinden seçme](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

**Şekil 02**: Statik bir öğe listesinden seçim yapmak([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image4.png))

Bu seçenekleri ComboBox denetimine eklemenin iki yolu vardır. İlk olarak, Tasarım görünümünde farenizi denetimin üzerine gezerken Seçenekleri Düzenleme görev seçeneğini seçin ve Öğe Düzenleyicisi'ni açın (Bkz. Şekil 3).

[![ComboBox öğelerini düzenleme](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

**Şekil 03**: ComboBox öğelerini düzenleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image6.png))

İkinci seçenek, Kaynak görünümünde asp:ComboBox &lt;&gt; etiketlerinin açılması ve kapatılması arasındaki öğelerin listesini eklemektir. Listeleme 1'deki sayfa, öğelerin listesini içeren güncelleştirilmiş ComboBox'ı içerir.

**Listeleme 1 - Static.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

Listeleme 1'de sayfayı açtığınızda, ComboBox'tan önceden varolan seçeneklerden birini seçebilirsiniz. Başka bir deyişle, ComboBox bir DropDownList denetimi gibi çalışır.

Ancak, varolan listede olmayan yeni bir seçenek (örneğin, Süper Baharatlı) girme seçeneğiniz de vardır. Yani, ComboBox da bir TextBox kontrolü gibi çalışır.

Önceden varolan bir öğeyi seçip seçmediğinize veya özel bir öğe girin, formu gönderdiğinizde seçiminiz etiket denetiminde görünür. Formu gönderdiğiniz zaman, btnGönder\_Click işleyicisi etiketi yürütür ve güncelleştirir (Bkz. Şekil 4).

[![Seçili öğeyi görüntüleme](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

**Şekil 04**: Seçili öğenin görüntülenmesi ([Tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image8.png))

ComboBox, bir form gönderildikten sonra seçili öğeyi almak için DropDownList denetimiyle aynı özellikleri destekler:

- SelectedItem.Text - Seçili öğenin Metin özelliğinin değerini görüntüler.
- SelectedItem.Value - Seçili öğenin Değer özelliğinin değerini görüntüler veya ComboBox'a yazılan metni görüntüler.
- SelectedValue - SelectedItem.Value ile aynıdır, ancak bu özellik varsayılan (ilk) seçili öğeyi belirtmenizi sağlar.

ComboBox'a özel bir seçim yazarsanız, özel seçim hem SelectedItem.Text hem de SelectedItem.Value özelliklerine atanır.

## <a name="selecting-the-list-of-items-from-the-database"></a>Veritabanından Öğeler Listesini Seçme

ComboBox'ın görüntülediğiniz öğelerin listesini bir veritabanından alabilirsiniz. Örneğin, ComboBox'ı Bir SqlDataSource denetimine, ObjectDataSource denetimine, bir LinqDataSource'a veya EntityDataSource'a bağlayabilirsiniz.

ComboBox'ta filmlerin listesini görüntülemek istediğinizi düşünün. Filmler veritabanı tablosundan film listesini almak istiyorsunuz. Şu adımları uygulayın:

1. Movies.aspx adlı sayfa oluşturma
2. Toolbox'taki AJAX Uzantıları sekmesinin altından ScriptManager'ı sayfaya sürükleyerek bir ScriptManager denetimi ekleyin.
3. ComboBox'ı sayfaya sürükleyerek sayfaya Bir ComboBox denetimi ekleyin.
4. Tasarım görünümünde, farenizi ComboBox denetiminin üzerine tarayın ve **Veri Kaynağı** seç görev seçeneğini seçin (Bkz. Şekil 5). Veri Kaynağı Yapılandırma Sihirbazı başlatıldı.
5. Veri **Kaynağı Seç** adımında Yeni &lt;veri&gt; kaynağı seçeneğini belirleyin.
6. Veri **Kaynağı Türü Seç** adımında Veritabanı'nı seçin.
7. Veri **Bağlantınızı Seçin** adımda veritabanınızı seçin (örneğin, MoviesDB.mdf).
8. Bağlantı **Dizesini Uygulama Yapılandırma Dosyası adımına kaydedin,** bağlantı dizenizi kaydetme seçeneğini seçin.
9. İfade **seç adımını Yapılandır'da** Filmler veritabanı tablosunu seçin ve tüm sütunları seçin.
10. Test **Sorgusu** adımında, Finish düğmesini tıklatın.
11. **Veri Kaynağı Seç** adımında, görüntülenecek alanın Başlık sütununa ve veri alanının Id sütununa (Bkz. Şekil' i) seçin.
12. Sihirbazı kapatmak için Tamam düğmesini tıklatın.

[![Veri kaynağı seçme](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

**Şekil 05**: Veri kaynağı nın seçilmesi ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image10.png))

[![Veri metni ve değer alanlarını seçme](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

**Şekil 06**: Veri metni ve değer alanlarını seçme[(Tam boyutlu görüntüyü görüntülemek için tıklayınız)](how-do-i-use-the-combobox-control-vb/_static/image12.png)

Yukarıdaki adımları tamamladıktan sonra, ComboBox Filmler veritabanı tablosundaki filmleri temsil eden bir SqlDataSource denetimine bağlıdır. Sayfanın kaynağı Listeleme 2 gibi görünüyor (ben biraz biçimlendirme temizledi).

**Listeleme 2 - Movies.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

ComboBox denetiminin SqlDataSource denetimini gösteren bir DataSourceID özelliğine sahip olduğuna dikkat edin. Sayfayı bir tarayıcıda açtığınızda, veritabanındaki filmlerin listesi görüntülenir (Bkz. Şekil 7). Listeden bir film seçebilir veya filmi ComboBox'a yazarak yeni bir film girebilirsiniz.

[![Filmlerin listesini görüntüleme](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

**Şekil 07**: Film listesini görüntüleme([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>DropDownStyle'ı ayarlama

ComboBox'ın davranışını değiştirmek için ComboBox DropDownStyle özelliğini kullanabilirsiniz. Bu özellik olası değerleri kabul eder:

- DropDown - (varsayılan değer) ComboBox oku tıklattığınızda bir açılır liste görüntüler ve özel bir değer girebilirsiniz.
- Basit - ComboBox açılır listeyi otomatik olarak görüntüler ve özel bir değer girebilirsiniz.
- DropDownList - ComboBox bir DropDownList kontrolü gibi çalışır.

DropDown ve Simple arasındaki fark, öğelerin listesinin görüntülenmesidir. Simple durumunda, odağı ComboBox'a taşıdığınızda liste hemen görüntülenir. DropDown durumunda, öğelerin listesini görmek için oku tıklatmanız gerekir.

DropDownList değeri, ComboBox denetiminin standart bir DropDownList denetimi gibi çalışmasına neden olur. Ancak, burada önemli bir fark vardır. Internet Explorer'ın eski sürümleri, sonsuz z dizinli bir DropDownList denetimi görüntüler, böylece denetim önüne yerleştirilen herhangi bir denetimin önünde görünür. ComboBox, &lt;HTML&gt; &lt;seç etiketi&gt; yerine HTML div etiketi işledığından, ComboBox z-siparişine doğru şekilde saygı duyar.

## <a name="setting-the-autocompletemode"></a>Otomatik Tamamlama Modu'nu ayarlama

Birisi ComboBox'a metin yazdığında ne olacağını belirtmek için ComboBox AutoCompleteMode özelliğini kullanırsınız. Bu özellik aşağıdaki olası değerleri kabul eder:

- Yok - (varsayılan değer) ComboBox herhangi bir otomatik tam davranış sağlamaz.
- Öner - ComboBox listeyi görüntüler ve listedeki eşleşen öğeyi vurgular (Bkz. Şekil 8).
- Ek - ComboBox listeyi görüntülemez ve listedeki eşleşen öğeyi yazdığınız öğeye ekler (Bkz. Şekil 9).
- SuggestAppend - ComboBox hem listeyi görüntüler hem de eşleşen öğeyi listeden yazdığınız öğeye ekler (Bkz. Şekil 10).

[![ComboBox bir öneride](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

**Şekil 08**: ComboBox bir öneride bulunmak ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image16.png))

[![ComboBox eşleşen metni ekler](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

**Şekil 09**: ComboBox eşleşen metni ekler([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image18.png))

[![ComboBox önerir ve ekler](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

**Şekil 10**: ComboBox önerir ve ekler ([Tam boyutlu görüntü görüntülemek için tıklayınız](how-do-i-use-the-combobox-control-vb/_static/image20.png))

## <a name="summary"></a>Özet

Bu eğitimde, sabit bir öğe kümesini görüntülemek için ComboBox denetimini nasıl kullanacağınızı öğrendiniz. ComboBox denetimini hem statik bir öğe kümesine hem de veritabanı tablosuna bağladık. Son olarak, DropDownStyle ve AutoCompleteMode özelliklerini ayarlayarak ComboBox'ın davranışını değiştirmeyi öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](how-do-i-use-the-combobox-control-cs.md)
