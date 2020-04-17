---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML Düzenleyici Denetimini nasıl kullanırım? (VB) | Microsoft Dokümanlar
author: rick-anderson
description: HTMLEditor, bir araç çubuğundaki düğmeler aracılığıyla HTML içeriğini kolayca oluşturmanıza ve düzenlemenize olanak tanıyan ASP.NET bir AJAX Control'dür.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542839"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>HTML Düzenleyici Denetimini nasıl kullanırım? (VB)

[Microsoft](https://github.com/microsoft) tarafından

> HTMLEditor, bir araç çubuğundaki düğmeler aracılığıyla HTML içeriğini kolayca oluşturmanıza ve düzenlemenize olanak tanıyan ASP.NET bir AJAX Control'dür.

Bu öğreticinin amacı, AJAX Control Toolkit ile birlikte verilen HTML Düzenleyici denetimine genel bir bakış sağlamaktır. HTML Düzenleyicisi yazı tipi boyutunu değiştirme, yazı tipi seçme, arka plan rengini değiştirme, ön plan rengini değiştirme, bağlantılar ekleme, resim ekleme, metin hizalamasını değiştirme ve kesme, kopyalama ve yapıştırma işlemlerini gerçekleştirme seçeneklerini içerir (Bkz. Şekil 1).

[![HTML Düzenleyicisi](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**Şekil 01**: HTML Düzenleyicisi([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-html-editor-control-vb/_static/image2.png))

HTML düzenleyicisi bir tasarım modu kullanarak içerik girmenizi sağlar veya doğrudan HTML girebilirsiniz. Ayrıca HTML içeriğinizi önizleme seçeneği de size verilir (Bkz. Şekil 2).

[![Tasarım, HTML ve Önizleme düğmeleri](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**Şekil 02**: Tasarım, HTML ve Önizleme düğmeleri([Tam boyutlu görüntüyü görüntülemek için tıklayınız)](how-do-i-use-the-html-editor-control-vb/_static/image4.png)

Bu eğitimde, HTML Düzenleyicisi'ni nasıl görüntüleyesiniz, HTML Düzenleyicisi'nde görünen araç çubuğu düğmelerini nasıl özelleştirdiğinizi ve Siteler Arası Komut Dosyası Saldırılarından nasıl kaçınabileceğinizi öğrenirsiniz.

## <a name="displaying-the-html-editor"></a>HTML Düzenleyicisini Görüntüleme

HTML Düzenleyicisini ASP.NET bir sayfada kullanabilmek için önce sayfaya bir ScriptManager denetimi eklemeniz gerekir. ScriptManager denetimi, Visual Studio/Visual Web Developer Express araç kutusundaki AJAX Uzantıları sekmesinin altında yer alır.

Sayfadaki diğer denetimlerden önce ScriptManager denetimini sayfanın en üstüne yerleştirmelisiniz. Örneğin, bunu sunucu tarafındaki &lt;açılış form&gt; etiketinin hemen altına yerleştirebilirsiniz.

HTML Düzenleyici denetimi, AJAX Control Toolkit denetimlerinin geri kalanıyla birlikte araç kutusunda bulunur. Editör denetimi olarak adlandırılır (bkz. Şekil 3).

[![HTML Düzenleyici denetimi](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**Şekil 03**: HTML Düzenleyici kontrolü([Tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-html-editor-control-vb/_static/image6.png))

HTML Düzenleyicisini bir sayfaya sürükledikten sonra, özelliklerini özellik sayfasında ayarlayabilirsiniz. Örneğin, normalde Genişlik ve Yükseklik özelliklerini ayarlamak istiyorsunuz. Listeleme 1, HTML düzenleyicisi içeren bir ASP.NET sayfasının kaynağını içerir.

**Listeleme 1 - SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

Listeleme 1'deki sayfa bir HTML Düzenleyici denetimi, düğme denetimi ve Bir Literal denetim içerir. Düğmeyi tıklattığınızda, HTML Düzenleyicisi'nin içeriği Literal denetiminde görünür (Bkz. Şekil 4).

[![HTML Düzenleyicisi ile form gönderme](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**Şekil 04**: HTML Düzenleyicisi ile form gönderme ([tam boyutlu görüntüyü görüntülemek için tıklayınız](how-do-i-use-the-html-editor-control-vb/_static/image8.png))

HTML Düzenleyici İçeriği özelliği, HTML Düzenleyicisi'ne girilen HTML içeriğini almak için kullanılır. Bu HTML içeriğinin JavaScript içerebileceğini unutmayın. Sonraki bölümde, JavaScript Enjeksiyon Saldırılarını nasıl önleyebileceğinizi tartışıyoruz.

## <a name="customizing-the-html-editor-toolbar"></a>HTML Düzenleyici araç çubuğunu özelleştirme

Editörde tam olarak hangi düğmelerin görünebileceğini özelleştirebilirsiniz. Örneğin, kullanıcıların HTML Düzenleyicisi'ni HTML moduna dönüştürmesini önlemek için HTML sekmesini kaldırmak isteyebilirsiniz. Veya, kullanıcıların bir forum ileti gönderisinde aşırı büyük metin oluşturmalarını önlemek için yazı tipi boyutu açılır listesini kaldırmak isteyebilirsiniz (Bkz. Şekil 5).

[![Özelleştirilmiş BIR HTML Düzenleyicisi](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**Şekil 05**: Özelleştirilmiş bir HTML Düzenleyicisi([Tam boyutlu görüntüyü görüntülemek için tıklayınız)](how-do-i-use-the-html-editor-control-vb/_static/image10.png)

Temel Düzenleyici sınıfından yeni bir HTML Düzenleyicisi türeterek araç çubuğu düğmelerini özelleştirebilirsiniz. Örneğin, Listeleme 2'deki özel düzenleyici yalnızca kalın ve italik için araç çubuğu düğmeleri içerir. Diğer tüm araç çubuğu düğmeleri kaldırıldı. Ayrıca, HTML sekmesi editörün alt kısmından kaldırıldı (ancak Tasarım ve Önizleme sekmeleri hala orada).

**Listeleme 2\_- Uygulama Kodu\CustomEditor.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

Sınıfın otomatik olarak derlenmesi için\_Listeleme 2'deki sınıfı Uygulama Kodu klasörünüze eklemeniz gerekir. Uygulama\_Kodu klasörü web sitenizde yoksa, klasörü ekleyebilirsiniz.

Özel bir düzenleyici oluşturduktan sonra, normal HTML Düzenleyicisini eklediğiniz gibi ASP.NET bir sayfaya ekleyebilirsiniz (bkz.

**Listeleme 3 - ShowCustomEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Siteler Arası Komut Dosyası (XSS) Saldırılarından Kaçınma

Bir kullanıcının girdisini kabul ettiğinizde ve web sitenizdeki bu girişi yeniden görüntülediğinizde, web sitenizi Siteler Arası Komut Dosyası (XSS) Saldırılarına açma potansiyeliniz. Teorik olarak, kötü niyetli bir bilgisayar korsanı giriş yeniden görüntülendiğinde çalıştırılan JavaScript kodu gönderebilir. JavaScript kullanıcı parolalarını veya diğer hassas bilgileri çalmak için kullanılabilir.

Normalde, xss saldırılarını, bir web sayfasında görüntülemeden önce bir kullanıcıdan aldığınız girişi kodlayarak HTML kodlayarak yenebilirsiniz. Ancak, HTML Düzenleyicisi çıktıkodlama HTML sadece &lt;komut&gt; dosyası etiketleri kodlamak olmaz, aynı zamanda tüm HTML etiketleri kodlamak istiyorsunuz. Başka bir deyişle, yazı tipi türü, yazı tipi boyutu ve arka plan rengi gibi biçimlendirmenin tümlerini kaybedersiniz.

Parolalar, kredi kartı numaraları ve sosyal güvenlik numaraları gibi kullanıcılarınızdan hassas bilgiler topluyorsanız, HTML Düzenleyicisi olan bir kullanıcıdan aldığınız kodlanmamış içeriği görüntülememelisiniz. HTML Düzenleyicisini yalnızca HTML içeriğini yeniden görüntülemediğiniz veya HTML içeriğinin güvenilir bir taraf tarafından web sitenize gönderildiği durumlarda kullanmalısınız.

Örneğin, bir blog uygulaması oluşturduğunuzu düşünün. Bu durumda, blog gönderileri oluştururken HTML Düzenleyicisi'ni kullanmak mantıklıdır. Bir blog yazısı gönderen tek kişi sizsiniz ve muhtemelen kötü amaçlı JavaScript göndermemek için kendinize güvenebilirsiniz. Ancak, anonim kullanıcıların yorum yayınlamasına izin verirken HTML Düzenleyicisi'ni kullanmak mantıklı değildir. Özellikle kullanıcıların parolalar gibi hassas bilgileri gönderdiği durumlarda dikkatli olmalısınız. Kötü amaçlı bir kullanıcı, parola çalmak için doğru JavaScript'i içeren bir yorum yayınlayabilir.

## <a name="summary"></a>Özet

Bu eğitimde, AJAX Control Toolkit'te yer alan HTML Düzenleyici denetimine kısa bir genel bakış sunulmuştur. HTML Düzenleyicisi'ni kullanarak bir kullanıcıdan zengin içeriği kabul etmeyi ve içeriği sunucuya göndermeyi öğrendiniz. Ayrıca HTML Düzenleyicisi tarafından görüntülenen araç çubuğu düğmelerini nasıl özelleştirebileceğinizi de tartıştık. Son olarak, olası kötü amaçlı girişi kabul etmek için HTML Düzenleyicisi'ni kullanırken Siteler Arası Komut Dosyası Saldırılarından kaçınmayı öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](how-do-i-use-the-html-editor-control-cs.md)
