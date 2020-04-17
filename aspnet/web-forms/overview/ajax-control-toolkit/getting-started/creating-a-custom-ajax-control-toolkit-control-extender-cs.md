---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: Özel AJAX Kontrol Araç Seti Kontrol Genişletici (C#) Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Özel Genişleticiler, yeni sınıflar oluşturmak zorunda kalmadan ASP.NET denetimlerinin özelliklerini özelleştirmenize ve genişletmenize olanak tanır.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543034"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>Özel AJAX Denetim Araç Seti Denetim Genişleticisi Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Özel Genişleticiler, yeni sınıflar oluşturmak zorunda kalmadan ASP.NET denetimlerinin özelliklerini özelleştirmenize ve genişletmenize olanak tanır.

Bu eğitimde, özel bir AJAX Control Toolkit kontrol genişletici oluşturmak için nasıl öğrenirler. TextBox'a metin yazarken düğmenin durumunu devre dışı bırakılandan etkine değiştiren basit, ancak kullanışlı, yeni bir genişletici oluştururuz. Bu öğretici okuduktan sonra, kendi kontrol genişleticiler ile ASP.NET AJAX Toolkit genişletmek mümkün olacak.

Visual Studio veya Visual Web Developer 'ı kullanarak özel denetim genişleticiler oluşturabilirsiniz (Visual Web Developer'ın en son sürümüne sahip olduğunuzdan emin olun).

## <a name="overview-of-the-disabledbutton-extender"></a>Engelli Düğme Genişletici'ye Genel Bakış

Yeni kontrol genişleticimiz DisabledButton genişletici olarak adlandırılmıştır. Bu genişleticinin üç özelliği olacaktır:

- TargetControlID - Denetimin genişletttiğin TextBox.
- TargetButtonIID - Devre dışı bırakılan veya etkin olan düğme.
- Engelli Metin - Başlangıçta Düğme'de görüntülenen metin. Yazmaya başladığınızda, Düğme Metin özelliğinin değerini görüntüler.

DisabledButton genişleticisini TextBox ve Button denetimine bağlarsınız. Herhangi bir metin yazmadan önce Düğme devre dışı bırakılır ve TextBox ve Düğme aşağıdaki gibi görünür:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([Tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))

Metin yazmaya başladıktan sonra Düğme etkinleştirilir ve TextBox ve Düğme aşağıdaki gibi görünür:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([Tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))

Denetim genişleticimizi oluşturmak için aşağıdaki üç dosyayı oluşturmamız gerekir:

- DisabledButtonExtender.cs - Bu dosya, genişleticinizi oluşturmayı yönetecek ve özellikleri tasarım zamanında ayarlamanızı sağlayan sunucu tarafı denetim sınıfıdır. Genişleticinizde ayarlanabilecek özellikleri de tanımlar. Bu özelliklere kod üzerinden ve tasarım zamanında erişilebilir ve DisableButtonBehavior.js dosyasında tanımlanan özellikleri eşler.
- DisabledButtonBehavior.js -- Bu dosya, tüm istemci komut dosyası mantığınızı ekleyeceğiniz yerdir.
- DisabledButtonDesigner.cs - Bu sınıf tasarım zamanı işlevselliği sağlar. Denetim genişleticinin Visual Studio/Visual Web Developer Designer ile doğru çalışmasını istiyorsanız bu sınıfa ihtiyacınız vardır.

Bu nedenle, denetim genişletici sunucu tarafı denetimi, istemci tarafı davranışı ve sunucu tarafı tasarımcı sınıfından oluşur. Aşağıdaki bölümlerde bu üç dosyanın nasıl oluşturulabileceğinizi öğrenirsiniz.

## <a name="creating-the-custom-extender-website-and-project"></a>Özel Genişletici Web Sitesi ve Projesi Oluşturma

İlk adım Visual Studio / Görsel Web Geliştirici bir sınıf kitaplık proje ve web sitesi oluşturmaktır. Sınıf kitaplığı projesinde özel genişletici oluşturacağız ve web sitesindeki özel genişleticitest edeceğiz.

Web sitesi ile başlayalım. Web sitesini oluşturmak için aşağıdaki adımları izleyin:

1. Menü seçeneği **Dosya, Yeni Web Sitesi**seçin.
2. ASP.NET **Web Sitesi** şablonunu seçin.
3. Yeni web sitesi *Website1*adı .
4. **Tamam** düğmesini tıklatın.

Ardından, denetim genişleticinin kodunu içeren sınıf kitaplığı projesini oluşturmamız gerekir:

1. Menü seçeneği **Dosya, Ekle, Yeni Proje'yi**seçin.
2. Sınıf **Kitaplığı** şablonu'nu seçin.
3. **CustomExtenders**adı ile yeni sınıf kitaplığı adı.
4. **Tamam** düğmesini tıklatın.

Bu adımları tamamladıktan sonra Çözüm Gezgini pencereniz Şekil 1 gibi görünmelidir.

[![Web sitesi ve sınıf kitaplığı projesi ile çözüm](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**Şekil 01**: Web sitesi ve sınıf kitaplığı projesi ile çözüm ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))

Ardından, sınıf kitaplığı projesine gerekli tüm derleme başvurularını eklemeniz gerekir:

1. CustomExtenders projesine sağ tıklayın ve **Menü**seçeneğini seçin Referans Ekle seçeneğini belirleyin.
2. .NET sekmesini seçin.
3. Aşağıdaki derlemelere başvurular ekleyin:

    1. Sistem.Web.dll
    2. System.Web.Extensions.dll
    3. Sistem.Design.dll
    4. System.Web.Extensions.Design.dll
4. Gözat sekmesini seçin.
5. AjaxControlToolkit.dll montaj bir referans ekleyin. Bu derleme, AJAX Control Toolkit'i indirdiğiniz klasörde bulunur.

Bu adımları tamamladıktan sonra, sınıf kitaplığı proje Başvuruları klasörünüz Şekil 2 gibi görünmelidir.

[![Gerekli başvuruları içeren başvurular klasörü](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**Şekil 02**: Gerekli referansları içeren başvurular klasörü ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>Özel Denetim Genişletici Oluşturma

Artık sınıf kütüphanemiz olduğuna göre genişletici kontrolümüzü oluşturmaya başlayabiliriz. Özel bir genişletici kontrol sınıfının çıplak kemikleri ile başlayalım (Bkz. Listeleme 1).

**İlan 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

Listeleme 1'deki denetim genişletici sınıfı hakkında fark ettiğiniz birkaç şey vardır. İlk olarak, sınıfın temel ExtenderControlBase sınıfından devraldığına dikkat edin. Tüm AJAX Control Toolkit genişletici denetimleri bu taban sınıftan türetilmiştir. Örneğin, taban sınıf, her denetim genişleticinin gerekli özelliği olan TargetID özelliğini içerir.

Ardından, sınıfın istemci komut dosyasıyla ilgili aşağıdaki iki öznitelikleri içerdiğine dikkat edin:

- WebKaynak - Dosyanın derlemeye katıştırılmış kaynak olarak eklenmesine neden olur.
- ClientScriptResource - Bir derlemeden alınacak komut dosyası kaynağına neden olur.

WebResource özniteliği, özel genişletici derlendiğinde MyControlBehavior.js JavaScript dosyasını derlemeye yerleştirmek için kullanılır. ClientScriptResource özniteliği, özel genişletici bir web sayfasında kullanıldığında Derleme'den MyControlBehavior.js komut dosyasını almak için kullanılır.

WebResource ve ClientScriptResource özniteliklerinin çalışması için, JavaScript dosyasını katıştırılmış bir kaynak olarak derlemeniz gerekir. Solution Explorer penceresindedosyayı seçin, özellik sayfasını açın ve *Katıştırılmış Kaynak* değerini **Yapı Eylemi** özelliğine atayın.

Denetim genişleticinin targetControlType özniteliği de içerdiğine dikkat edin. Bu öznitelik, denetim genişletici tarafından uzatılan denetim türünü belirtmek için kullanılır. Listeleme 1 durumunda, denetim genişletici textbox genişletmek için kullanılır.

Son olarak, özel genişletici MyProperty adlı bir özellik içerdiğini unutmayın. Özellik ExtenderControlProperty özniteliği ile işaretlenir. GetPropertyValue() ve SetPropertyValue() yöntemleri, özellik değerini sunucu tarafındaki denetim genişleticisinden istemci tarafındaki davranışa geçirmek için kullanılır.

Devam edelim ve Engelli Düğme genişleticimiz için kodu uygulayalım. Bu genişleticinin kodu Listeleme 2'de bulunabilir.

**Listeleme 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

Listeleme 2'deki Engelli Düğme genişleticinin TargetButtonID ve DisabledText adlı iki özelliği vardır. TargetButtonID özelliğine uygulanan IDReferenceÖzelliği, bu özelliğe Düğme denetimikimliği dışında herhangi bir şey atamanızı engeller.

WebResource ve ClientScriptResource öznitelikleri, DisabledButtonBehavior.js adlı bir dosyada bulunan istemci tarafı davranışını bu genişleticiyle ilişkilendirir. Bu JavaScript dosyasını bir sonraki bölümde tartışıyoruz.

## <a name="creating-the-custom-extender-behavior"></a>Özel Genişletici Davranışı Oluşturma

Denetim genişleticinin istemci tarafı bileşenine davranış denir. Düğmeyi devre dışı bırakma ve etkinleştirme için gerçek mantık Engelli Düğmesi davranışında bulunur. Davranışın JavaScript kodu Listeleme 3'e dahildir.

**Listeleme 3 - DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

Listeleme 3'teki JavaScript dosyası, DisabledButtonBehavior adlı istemci tarafı sınıfını içerir. Bu sınıf, sunucu tarafındaki ikizi gibi TargetButtonID ve DisabledText adlı iki\_özellik içerir,\_TargetButtonID'yi al/TargetButtonID'i ayarlayabilir ve\_DisabledText/set\_DisabledText'i kullanarak erişebilirsiniz.

Initialize() yöntemi, bir keyup olay işleyicisini davranış için hedef öğeyle ilişkilendirer. Bu davranışla ilişkili TextBox'a her mektup yazdığınızda, anahtar teslimi işleyici sisini yürütür. Anahtar teslimi işleyici, davranışla ilişkili TextBox'ın herhangi bir metin içerip içermediğine bağlı olarak Düğmeyi etkinleştirer veya devre dışı eder.

Listeleme 3'teki JavaScript dosyasını gömülü bir kaynak olarak derlemeniz gerektiğini unutmayın. Solution Explorer penceresindedosyayı seçin, özellik sayfasını açın ve *Katıştırılmış Kaynak* değerini **Yapı Eylemi** özelliğine atayın (Bkz. Şekil 3). Bu seçenek hem Visual Studio hem de Visual Web Developer'da kullanılabilir.

[![Gömülü kaynak olarak JavaScript dosyası ekleme](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**Şekil 03**: Gömülü kaynak olarak JavaScript dosyası ekleme ([Tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>Özel Genişletici Tasarımcısı oluşturma

Genişleticimizi tamamlamak için oluşturmamız gereken son bir sınıf daha var. Listeleme 4'te tasarımcı sınıfını oluşturmamız gerekiyor. Bu sınıf, genişleticinin Visual Studio/Visual Web Developer Designer ile doğru şekilde şekilde görünmesini sağlamak için gereklidir.

**İlan 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

Listeleme 4'teki tasarımcıyı DisabledButton genişleticisiyle Tasarımcı özniteliğiyle ilişkilendirirsiniz. Designer özniteliğini DisabledButtonExtender sınıfına şu şekilde uygulamanız gerekir:

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>Özel Genişletici'yi Kullanma

Şimdi Biz DisabledButton kontrol genişletici oluşturma bitmiş, bizim ASP.NET web sitesinde kullanmak zamanı. İlk olarak, özel genişletici araç kutusuna eklemeniz gerekir. Şu adımları uygulayın:

1. Çözüm Gezgini penceresindeki sayfayı çift tıklatarak bir ASP.NET sayfası açın.
2. Araç kutusuna sağ tıklayın ve Menü seçeneğini seçin **Öğeleri Seçin.**
3. Araç Kutusu Öğelerini Seç iletişim kutusunda CustomExtenders.dll derlemesine göz atın.
4. İletişim kutusunu kapatmak için **Tamam** düğmesini tıklatın.

Bu adımları tamamladıktan sonra, Engelli Düğmesi denetim genişletici araç kutusunda görünmelidir (Bkz. Şekil 4).

[![Engelli Düğmesi araç kutusunda](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**Şekil 04**: Özürlü Düğme araç kutusunda ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))

Sonra, yeni bir ASP.NET sayfası oluşturmamız gerekir. Şu adımları uygulayın:

1. ShowDisabledButton.aspx adlı yeni bir ASP.NET sayfası oluşturun.
2. Bir ScriptManager'ı sayfaya sürükleyin.
3. TextBox denetimini sayfaya sürükleyin.
4. Düğme denetimini sayfaya sürükleyin.
5. Özellikler penceresinde, Düğme Kimliği özelliğini <em>btnKayd değerine</em> ve Metin özelliğini *Kaydet\** değerine değiştirin.

TextBox ve Button denetimi ASP.NET standart bir sayfa oluşturduk.

Ardından, DisabledButton genişletici ile TextBox denetimini genişletmemiz gerekir:

1. Genişletici Sihirbazı iletişim kutusunu açmak için **Genişletici Ekle** görev seçeneğini seçin (Bkz. Şekil 5). İletişim kutusunun özel Engelli Düğme genişleticimizi içerdiğine dikkat edin.
2. Engelli Düğmesi genişleticisini seçin ve **Tamam** düğmesini tıklatın.

[![Genişletici Sihirbazı iletişim kutusu](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**Şekil 05**: Genişletici Sihirbazı iletişim kutusu([Tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))

Son olarak, DisabledButton genişleticinin özelliklerini ayarlayabiliriz. TextBox denetiminin özelliklerini değiştirerek Engelli Düğmesi genişleticinin özelliklerini değiştirebilirsiniz:

1. Designer'daki TextBox'ı seçin.
2. Özellikler penceresinde, Genişleticiler düğümünü genişletin (Bkz. Şekil 6).
3. DisabledText özelliğine *kaydet* değerini ve *btnDeğerini* TargetButtonID özelliğine kaydet'i atayın.

[![Genişletici özelliklerini ayarlama](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**Şekil 06**: Genişletici özelliklerini ayarlama([Tam boyutlu görüntüyü görüntülemek için tıklayınız](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))

Sayfayı çalıştırdığınızda (F5 tuşuna basarak), Düğme denetimi başlangıçta devre dışı bırakılır. TextBox'a metin girmeye başladığınız anda Düğme denetimi etkinleştirilir (Bkz. Şekil 7).

[![Engelli Düğmesi genişletici iş başında](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**Şekil 07**: Engelli Düğme genişletici[(Tam boyutlu görüntüyü görüntülemek için tıklayınız)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)

## <a name="summary"></a>Özet

Bu öğreticinin amacı, AJAX Control Toolkit'i özel genişletici denetimleriyle nasıl genişletebileceğinizi açıklamaktı. Bu eğitimde, basit bir DisabledButton kontrol genişletici oluşturduk. Bu genişleticiyi DisabledButtonExtender sınıfı, DisabledButtonBehavior JavaScript davranışı ve DisabledButtonDesigner sınıfı oluşturarak uyguladık. Özel bir denetim genişletici oluşturduğunuzda benzer bir adım kümesi izlersiniz.

> [!div class="step-by-step"]
> [Önceki](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [Sonraki](get-started-with-the-ajax-control-toolkit-vb.md)
