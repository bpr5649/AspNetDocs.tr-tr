---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 Sayfa Modeli | Microsoft Dokümanlar
author: rick-anderson
description: 1.x ASP.NET, geliştiricilerin satır içi kod modeli ile kod arkası kod modeli arasında bir seçim vardı. Kod arkası src attr kullanılarak uygulanabilir ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542865"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 Sayfa Modeli

[Microsoft](https://github.com/microsoft) tarafından

> 1.x ASP.NET, geliştiricilerin satır içi kod modeli ile kod arkası kod modeli arasında bir seçim vardı. Kod arkası, @Page yönergedeki Src özniteliği veya CodeBehind özniteliği kullanılarak uygulanabilir. ASP.NET 2.0'da, geliştiricilerin satır içi kod ve kod arkası arasında bir seçim vardır, ancak kod arkası modelinde önemli geliştirmeler yapılmıştır.

1.x ASP.NET, geliştiricilerin satır içi kod modeli ile kod arkası kod modeli arasında bir seçim vardı. Kod arkası, @Page yönergedeki Src özniteliği veya CodeBehind özniteliği kullanılarak uygulanabilir. ASP.NET 2.0'da, geliştiricilerin satır içi kod ve kod arkası arasında bir seçim vardır, ancak kod arkası modelinde önemli geliştirmeler yapılmıştır.

## <a name="improvements-in-the-code-behind-model"></a>Kod Arkası Modelindeki Geliştirmeler

ASP.NET 2.0'daki kod arkası modeldeki değişiklikleri tam olarak anlamak için, modeli 1.x'ASP.NET olduğu gibi hızlı bir şekilde gözden geçirmek en iyisidir.

## <a name="the-code-behind-model-in-aspnet-1x"></a>kod arkası modeli ASP.NET 1.x

1.x ASP.NET kod arkası modeli bir ASPX dosyası (Webform) ve programlama kodu içeren bir kod arkası dosyadan oluşuyordu. İki dosya ASPX @Page dosyasındaki yönerge kullanılarak bağlandı. ASPX sayfasındaki her denetimde, örnek değişken olarak kod arkası dosyasında karşılık gelen bir bildirim vardı. Kod arkası dosyası da olay bağlama için kod içeriyordu ve Visual Studio tasarımcısı için gerekli oluşturulan kod. Bu model oldukça iyi çalıştı, ancak ASPX sayfasındaki her ASP.NET öğesi kod arkasındaki dosyada karşılık gelen kod gerektirdiğinden, kod ve içeriğin gerçek bir ayrımı yoktu. Örneğin, bir tasarımcı Visual Studio IDE dışında bir ASPX dosyasına yeni bir sunucu denetimi eklediyse, kod arkasındaki dosyada bu denetim için bir bildirim olmaması nedeniyle uygulama bozulur.

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0'da Kod Arkası Modeli

ASP.NET 2.0 büyük ölçüde bu model üzerinde geliştirir. 2.0 ASP.NET, ASP.NET 2.0'da sağlanan yeni *kısmi sınıflar* kullanılarak kod arkası uygulanır. ASP.NET 2.0'daki kod arkası sınıfı, sınıf tanımının yalnızca bir bölümünü içerdiği anlamına gelen kısmi sınıf olarak tanımlanır. Sınıf tanımının kalan bölümü, çalışma zamanında veya Web sitesi önceden derlendiğinde ASPX sayfası kullanılarak 2.0 ASP.NET tarafından dinamik olarak oluşturulur. Kod arkası dosyası ile ASPX sayfası arasındaki bağlantı hala @ Page yönergesi kullanılarak kurulmuştur. Ancak, codebehind veya Src özniteliği yerine, ASP.NET 2.0 artık CodeFile özniteliğini kullanır. Devralan özniteliği, sayfanın sınıf adını belirtmek için de kullanılır.

Tipik bir @ Page yönergesi şu şekilde görünebilir:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 kod arkası dosyasındaki tipik bir sınıf tanımı aşağıdaki gibi görünebilir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# ve Visual Basic şu anda kısmi sınıfları destekleyen tek yönetilen dillerdir. Bu nedenle, J# kullanan geliştiriciler ASP.NET 2.0'da kod arkası modelini kullanamaz.

Geliştiriciler artık yalnızca oluşturdukları kodu içeren kod dosyalarına sahip olacaklarından, yeni model kod arkasındaki modeli geliştirir. Ayrıca kod ve içeriğin gerçek bir ayrımını sağlar, çünkü kod arkasındaki dosyada örnek değişken bildirimleri yoktur.

> [!NOTE]
> ASPX sayfasının kısmi sınıfı olay bağlamanın gerçekleştiği yer olduğundan, Visual Basic geliştiricileri olayları bağlamak için kod arkasında İşles anahtar sözcüklerini kullanarak hafif bir performans artışı gerçekleştirebilir. C# eşdeğer anahtar kelimesi yoktur.

## <a name="new--page-directive-attributes"></a>Yeni @ Sayfa Yönergesi Öznitelikleri

ASP.NET 2.0 @ Page yönergesine birçok yeni öznitelik ekler. Aşağıdaki öznitelikler 2.0 ASP.NET yenidir.

## <a name="async"></a>Zaman Uyumsuz

Async özniteliği, sayfayı eş senkronize olarak yürütülecek şekilde yapılandırmanızı sağlar. Peki bu modülde daha sonra asynchronous sayfaları kapağı.

## <a name="asynctimeout"></a>AsyncTimeout

Eşzamanlı sayfalar için zaman arasını belirtti. Varsayılan değer 45 saniyedir.

## <a name="codefile"></a>Codefile

CodeFile özniteliği Visual Studio 2002/2003 codebehind özniteliği için değiştirmedir.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

CodeFileBaseClass özniteliği, birden çok sayfanın tek bir taban sınıftan türebilmesini istediğiniz durumlarda kullanılır. Asp.NETs derleme altyapısı sayfadaki denetimlere göre otomatik olarak yeni üyeler oluşturacağı için, ASP.NET kısmi sınıfların uygulanması nedeniyle, bu öznitelik olmadan, bir ASPX sayfasında bildirilen denetimlere başvurmak için paylaşılan ortak alanları kullanan bir taban sınıf düzgün çalışmaz. Bu nedenle, ASP.NET'da iki veya daha fazla sayfa için ortak bir taban sınıf istiyorsanız, CodeFileBaseClass özniteliğinde taban sınıfınızı belirtmeyi tanımlamanız ve sonra her sayfa sınıfını bu taban sınıftan türemelisiniz. Bu öznitelik kullanıldığında CodeFile özniteliği de gereklidir.

## <a name="compilationmode"></a>Compilationmode

Bu öznitelik, ASPX sayfasının Derleme Modu özelliğini ayarlamanızı sağlar. DerlemeModu özelliği **Her zaman**, **Otomatik**ve **Asla**değerlerini içeren bir numaralandırmadır. Varsayılan her **zaman.** **Otomatik** ayar, ASP.NET mümkünse sayfayı dinamik olarak derlemesini engeller. Sayfaları dinamik derlemeden hariç tetmek performansı artırır. Ancak, dışlanan bir sayfa derlenmiş olması gereken kodu içeriyorsa, sayfaya göz atıldığında bir hata atılır.

## <a name="enableeventvalidation"></a>EtkinleştireventValidation

Bu öznitelik, postback ve geri arama olaylarının doğrulanıp doğrulanmadığını belirtir. Bu etkinleştirildiğinde, onları ilk işlenen sunucu denetiminden kaynaklandığından emin olmak için postback veya geri arama olayları bağımsız değişkenleri denetlenir.

## <a name="enabletheming"></a>Enabletheming

Bu öznitelik, ASP.NET temaların bir sayfada kullanılıp kullanılmadığını belirtir. Varsayılan **yanlıştır.** ASP.NET temaları [Modül 10'da](profiles-themes-and-web-parts.md)ele alınmıştır.

## <a name="linepragmas"></a>LinePragmas

Bu öznitelik, derleme sırasında satır pragmlarının eklenip eklenmeyeceğini belirtir. Satır pragmalar, hata ayıklayıcılar tarafından kodun belirli bölümlerini işaretlemek için kullanılan seçeneklerdir.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Bu özellik, postback'ler arasında kaydırma konumunu korumak için JavaScript'in sayfaya enjekte edilip edilemeyeceğini belirtir. Bu öznitelik varsayılan olarak **yanlıştır.**

Bu öznitelik **doğru**olduğunda, ASP.NET &lt;&gt; postback'e şuna benzeyen bir komut dosyası bloğu ekler:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Bu komut dosyası bloğu için src WebResource.axd olduğunu unutmayın. Bu kaynak fiziksel bir yol değildir. Bu komut dosyası istendiğinde, ASP.NET dinamik olarak komut dosyası oluşturur.

### <a name="masterpagefile"></a>Masterpagefile

Bu öznitelik, geçerli sayfanın ana sayfa dosyasını belirtir. Yol göreceli veya mutlak olabilir. Ana sayfalar [Modül 4'te](master-pages.md)yer almaktadır.

## <a name="stylesheettheme"></a>StyleSheetTheme

Bu öznitelik, ASP.NET 2.0 temasıyla tanımlanan kullanıcı arabirimi görünüm özelliklerini geçersiz kılmanızı sağlar. Temalar [Modül 10'da](profiles-themes-and-web-parts.md)ele alınmıştır.

## <a name="theme"></a>Tema

Sayfanın tesini belirtir. StyleSheetTheme özniteliği için bir değer belirtilmemişse, Tema özniteliği sayfadaki denetimlere uygulanan tüm stilleri geçersiz kılar.

## <a name="title"></a>Başlık

Sayfanın başlığını ayarlar. Burada belirtilen değer, işlenen &lt;&gt; sayfanın başlık öğesinde görünür.

### <a name="viewstateencryptionmode"></a>ViewStateŞifreleme Modu

ViewStateEncryptionMode numaralandırma değerini ayarlar. Kullanılabilir değerler **Her Zaman**, **Otomatik**ve **Asla**. Varsayılan değer **Otomatik'tir.** Bu öznitelik **Otomatik**bir değere ayarlandığında, viewstate şifrelenir bir denetim **RegisterRequiresViewStateEncryption** yöntemi ni arayarak istekleridir.

## <a name="setting-public-property-values-via-the--page-directive"></a>@ Sayfa Yönergesi ile Kamu Mülkiyeti Değerlerini Ayarlama

2.0'ASP.NET @ Page yönergesinin bir diğer yeni özelliği de bir taban sınıfın ortak özelliklerinin başlangıç değerini ayarlama yeteneğidir. Örneğin, taban sınıfınızda **SomeText** adında bir kamu mülkünüz olduğunu ve bir sayfa yüklendiğinde **bunun Hello** olarak başharfe çevrilmesini istediğinizi varsayalım. Bunu, @ Page yönergesindeki değeri şu şekilde ayarlayarak gerçekleştirebilirsiniz:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page yönergesinin **SomeText** özniteliği, taban sınıftaki SomeText özelliğinin başlangıç değerini *Hello olarak ayarlar!* Aşağıdaki video, @ Page yönergesini kullanarak bir taban sınıftaki bir kamu malının başlangıç değerini ayarlamanın bir bölümüdür.

![](the-asp-net-2-0-page-model/_static/image1.png)

[Tam Ekran Video Aç](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Sayfa Sınıfının Yeni Genel Özellikleri

Aşağıdaki kamu malları ASP.NET 2.0'da yenidir.

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

Uygulama göreli yolu sayfaya veya denetime döndürür. Örneğin, bulunan bir sayfa http://app/folder/page.aspxiçin , özellik ~/klasör/döndürür.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

Göreceli sanal dizin yolunu sayfaya veya denetime döndürür. Örneğin, bulunan bir sayfa http://app/folder/page.aspxiçin , özellik ~/folder/page.aspx döndürür.

## <a name="asynctimeout"></a>AsyncTimeout

Eşzamanlı sayfa işleme için kullanılan zaman aşımını alır veya ayarlar. (Asynchronous sayfaları daha sonra bu modülde ele alınacaktır.)

## <a name="clientquerystring"></a>ClientQueryString

İstenen URL'nin sorgu dize bölümünü döndüren salt okunur özelliği. Bu değer URL kodlanır. Şifreyi çözmek için HttpServerUtility sınıfının UrlDecode yöntemini kullanabilirsiniz.

## <a name="clientscript"></a>Müşteri Senaryosu

Bu özellik, istemci tarafı komut dosyasının ASP.NETs emisyonuna yönetmek için kullanılabilecek bir ClientScriptManager nesnesi döndürür. (ClientScriptManager sınıfı daha sonra bu modülde ele alınmıştır.)

## <a name="enableeventvalidation"></a>EtkinleştireventValidation

Bu özellik, olay doğrulamanın postback ve geri arama olayları için etkin olup olmadığını denetler. Etkinleştirildiğinde, postback veya geri arama olayları için bağımsız değişkenler, bunların başlangıçta işlenen sunucu denetiminden kaynaklandığından emin olmak için doğrulanır.

## <a name="enabletheming"></a>Enabletheming

Bu özellik, sayfaiçin ASP.NET 2.0 temasının uygulanıp uygulanmadığını belirten bir Boolean alır veya ayarlar.

## <a name="form"></a>Form

Bu özellik, ASPX sayfasındaki HTML formunu HtmlForm nesnesi olarak döndürür.

## <a name="header"></a>Üst bilgi

Bu özellik, sayfa üstbilgisini içeren bir HtmlHead nesnesine başvuru verir. Stil sayfalarını, Meta etiketlerini vb. almak/ayarlamak için döndürülen HtmlHead nesnesini kullanabilirsiniz.

## <a name="idseparator"></a>IdSeparator

Bu salt okunur özellik, ASP.NET bir sayfadaki denetimler için benzersiz bir kimlik oluşturuyorken denetim tanımlayıcılarını ayırmak için kullanılan karakteri alır. Doğrudan kodunuzdan kullanılmak üzere tasarlanmamıştır.

## <a name="isasync"></a>ısasync

Bu özellik, eşzamanlı sayfalara izin verir. Asynchronous sayfaları daha sonra bu modülde ele alınmıştır.

## <a name="iscallback"></a>IsCallback

Sayfa geri aramanın sonucuysa, bu salt okunur özellik **doğru** döndürür. Geri aramalar daha sonra bu modülde tartışılır.

## <a name="iscrosspagepostback"></a>IscrossPagePostBack

Sayfa sayfa çapraz gönderimin bir parçasıysa, bu salt okunur özellik **doğru** döndürür. Sayfa içi postback'ler daha sonra bu modülde ele alınmıştır.

## <a name="items"></a>Öğeler

Sayfalar bağlamında depolanan tüm nesneleri içeren bir IDictionary örneğine başvuru verir. Bu IDictionary nesnesine öğeler ekleyebilirsiniz ve bunlar bağlamın ömrü boyunca sizin için kullanılabilir olacaktır.

## <a name="maintainscrollpositiononpostback"></a>KorumaScrollPositionOnPostback

Bu özellik, ASP.NET bir postback oluştuktan sonra tarayıcıda sayfaların kaydırma konumunu koruyan JavaScript'i yayıp bırakmadığını denetler. (Bu özelliğin ayrıntıları daha önce bu modülde ele alınmıştır.)

## <a name="master"></a>Ana

Bu salt okunur özellik, ana sayfanın uygulandığı bir sayfa için MasterPage örneğine bir başvuru döndürür.

## <a name="masterpagefile"></a>Masterpagefile

Sayfanın ana sayfa dosya adını alır veya ayarlar. Bu özellik yalnızca PreInit yönteminde ayarlanabilir.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

Bu özellik, sayfaların baytlar halindeki durumunun en büyük uzunluğunu alır veya ayarlar. Özellik pozitif bir sayıya ayarlanırsa, sayfa görünümü durumu, belirtilen bayt sayısını aşmayacak şekilde birden çok gizli alana bölünecektir. Özellik negatif bir sayıysa, görünüm durumu parçalara bölünmez.

## <a name="pageadapter"></a>Pageadapter

İstenen tarayıcı için sayfayı değiştiren PageAdapter nesnesine bir başvuru verir.

## <a name="previouspage"></a>Previouspage

Server.Transfer veya çapraz sayfa postback durumlarında önceki sayfaya bir başvuru döndürür.

## <a name="skinid"></a>Skinıd

Sayfaya uygulamak için 2,0 ASP.NET cilt belirtir.

## <a name="stylesheettheme"></a>StyleSheetTheme

Bu özellik, bir sayfaya uygulanan stil sayfasını alır veya ayarlar.

## <a name="templatecontrol"></a>Şablon Denetimi

Sayfa için içeren denetime bir başvuru verir.

## <a name="theme"></a>Tema

Sayfaya uygulanan ASP.NET 2.0 temasının adını alır veya ayarlar. Bu değer PreInit yönteminden önce ayarlanmalıdır.

## <a name="title"></a>Başlık

Bu özellik, sayfa üstbilgisinden elde edilen sayfanın başlığını alır veya ayarlar.

## <a name="viewstateencryptionmode"></a>ViewStateŞifreleme Modu

Sayfanın ViewStateEncryptionMode'unu alır veya ayarlar. Bu özellik hakkında daha önce bu modülde ayrıntılı bir tartışmaya bakın.

## <a name="new-protected-properties-of-the-page-class"></a>Sayfa Sınıfının Yeni Korunan Özellikleri

Aşağıda, ASP.NET 2.0'daki Sayfa sınıfının yeni korumalı özellikleri verilmiştir.

## <a name="adapter"></a>Bağdaştırıcı

Sayfayı isteyen aygıtta işleyen ControlAdapter'a bir başvuru verir.

## <a name="asyncmode"></a>AsyncMode

Bu özellik, sayfanın eşzamanlı olarak işlenip işlenmediğini gösterir. Doğrudan kodda değil, çalışma zamanı tarafından kullanılmak üzere tasarlanmıştır.

## <a name="clientidseparator"></a>ClientIDSeparator

Bu özellik, denetimler için benzersiz istemci disleri oluştururken ayırıcı olarak kullanılan karakteri döndürür. Doğrudan kodda değil, çalışma zamanı tarafından kullanılmak üzere tasarlanmıştır.

## <a name="pagestatepersister"></a>Pagestatepersister

Bu özellik, sayfa için PageStatePersister nesnesini döndürür. Bu özellik öncelikle ASP.NET denetim geliştiricileri tarafından kullanılır.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

Bu özellik, önbelleğe alınan tarayıcılar için dosya yoluna eklenen benzersiz bir sonek döndürür. Varsayılan değer \_ \_ufps= ve 6 basamaklı bir sayıdır.

## <a name="new-public-methods-for-the-page-class"></a>Sayfa Sınıfı için Yeni Genel Yöntemler

Aşağıdaki genel yöntemler, 2.0 ASP.NET Sayfa sınıfına yenidir.

## <a name="addonprerendercompleteasync"></a>Addonprerendercompleteasync

Bu yöntem, asynchronous sayfa yürütme için olay işleyicisi temsilcileri kaydeder. Asynchronous sayfaları daha sonra bu modülde ele alınmıştır.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

Sayfa stili sayfasındaki özellikleri sayfaya uygular.

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncGörevleri

Bu yöntem, eşzamanlı bir görev dir.

### <a name="getvalidators"></a>GetValidators

Belirtilen doğrulama grubu veya varsayılan doğrulama grubu için bir doğrulama topluluğu verir.

## <a name="registerasynctask"></a>KayıtAsyncTask

Bu yöntem yeni bir async görevi kaydeder. Asynchronous sayfaları daha sonra bu modülde ele alınmıştır.

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

Bu yöntem, ASP.NET sayfaları n için denetim durumunun kalıcı olması gerektiğini söyler.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateŞifreleme

Bu yöntem, ASP.NET sayfaların görüntü durumunun şifreleme gerektirdiğini söyler.

## <a name="resolveclienturl"></a>Çözümistemci

İstemci istekleri için kullanılabilecek göreli bir URL verir.

## <a name="setfocus"></a>SetFocus

Bu yöntem, sayfa ilk yüklendiğinde belirtilen denetime odak ayarlar.

## <a name="unregisterrequirescontrolstate"></a>Kayıt DışıGerekKontrolState

Bu yöntem, artık denetim durumu kalıcılığı gerektiren olarak ona geçirilen denetim inregister unregister olacaktır.

## <a name="changes-to-the-page-lifecycle"></a>Sayfa Yaşam Döngüsünde Yapılan Değişiklikler

ASP.NET 2.0'daki sayfa yaşam döngüsü önemli ölçüde değişmedi, ancak farkında olmanız gereken bazı yeni yöntemler vardır. 2.0 sayfa yaşam döngüsünün ASP.NET aşağıda özetlenmiştir.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (Yeni ASP.NET 2.0)

PreInit olayı, bir geliştiricinin erişebileceği yaşam döngüsünün en erken aşamasıdır. Bu olayın eklenmesi, 2.0 temaları, ana sayfaları, ASP.NET 2.0 profili için erişim özelliklerini ASP.NET programlı olarak değiştirmeyi mümkün kılar. Bir postback durumundaysanız, Viewstate'in yaşam döngüsünün bu noktasındaki denetimlere henüz uygulanmadığını fark etmek önemlidir. Bu nedenle, bir geliştirici bu aşamada bir denetimin özelliğini değiştirirse, büyük olasılıkla daha sonra sayfaların yaşam döngüsünde üzerine yazılır.

## <a name="init"></a>Init

Init olayı ASP.NET 1.x'ten değişmedi. Sayfanızdaki denetimlerin özelliklerini okumak veya başlatmak istediğiniz yerburasıdır. Bu aşamada, ana sayfalar, temalar, vb zaten sayfaya uygulanır.

## <a name="initcomplete-new-in-20"></a>InitComplete (Yeni 2.0)

InitComplete olayı sayfaların başlangıç aşamasının sonunda çağrılır. Yaşam döngüsünün bu noktasında, sayfadaki denetimler erişebilirsiniz, ancak durumları henüz doldurulmadı.

## <a name="preload-new-in-20"></a>Ön Yükleme (Yeni 2.0)

Bu olay, tüm geri gönderme verileri uygulandıktan sonra\_ve Sayfa Yüklemesi'nden hemen önce çağrılır.

## <a name="load"></a>Yükleme

Yük olayı ASP.NET 1.x'ten değişmedi.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (Yeni 2.0)

LoadComplete olayı, sayfaların yükleme aşamasındaki son olaydır. Bu aşamada, tüm postback ve görünüm durumu verileri sayfaya uygulanmıştır.

## <a name="prerender"></a>Prerender

Sayfaya dinamik olarak eklenen denetimler için viewstate'in düzgün bir şekilde tutulmasını istiyorsanız, PreRender olayı bunları eklemek için son fırsattır.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (Yeni 2.0)

PreRenderComplete aşamasında, tüm denetimler sayfaya eklendi ve sayfa oluşturulmaya hazır. PreRenderComplete olayı, sayfa görünümü kaydedilmeden önce ortaya çıkan son olaydır.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (Yeni 2.0)

SaveStateComplete olayı, tüm sayfa görüntüleme durumu ve denetim durumu kaydedildikten hemen sonra çağrılır. Bu, sayfa tarayıcıya işlenmeden önceki son olaydır.

## <a name="render"></a>İşleme

Render yöntemi 1.x ASP.NET beri değişmedi. Burada HtmlTextWriter başlatılan ve sayfa tarayıcıya işlenir.

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0'da Çapraz Sayfa Postback

1.xASP.NETde, postback'lerin aynı sayfaya göndermeleri gerekiyordu. Çapraz sayfa postback'lerine izin verilmedi. ASP.NET 2.0, IButtonControl arabirimi aracılığıyla farklı bir sayfaya geri gönderme olanağı ekler. Yeni IButtonControl arabirimini (Düğme, LinkButton ve ImageButton) üçüncü taraf özel denetimlere ek olarak uygulayan tüm denetimler, PostBackUrl özniteliğini kullanarak bu yeni işlevsellinden yararlanabilir. Aşağıdaki kod, ikinci bir sayfaya geri gönderen bir Düğme denetimini gösterir.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Sayfa geri gönderildiğinde, postback'i başlatan Sayfaya ikinci sayfadaki PreviousPage özelliği üzerinden erişilebilir. Bu işlevsellik, bir denetim\_farklı bir sayfaya geri gönderdiğinde 2.0'ı ASP.NET yeni WebForm DoPostBackWithOptions istemci tarafı işlevi aracılığıyla uygulanır. Bu JavaScript işlevi, istemciye komut dosyası yayan yeni WebResource.axd işleyicisi tarafından sağlanır.

Aşağıdaki video, sayfa lar arası bir postback'in gözden geçirimidir.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Tam Ekran Video Aç](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Sayfa Sonrası Bilgiler Hakkında Daha Fazla Bilgi

### <a name="viewstate"></a>Viewstate

Sayfalar arası postback senaryosunda ilk sayfadan görüntü durumuna ne olduğunu kendinize zaten sormuş olabilirsiniz. Sonuçta, iPostBackDataHandler uygulamaz herhangi bir denetim viewstate üzerinden durumunu devam edecektir, bu nedenle bir çapraz sayfa postback ikinci sayfasında bu denetimin özelliklerine erişmek için, sayfa için görünüm durumuna erişimi olmalıdır. ASP.NET 2.0, PREVIOUSPAGE adlı \_ \_ikinci sayfada yeni bir gizli alan kullanarak bu senaryoyu hallediyor. PREVIOUSPAGE form alanı, \_ \_ikinci sayfadaki tüm denetimlerin özelliklerine erişebilmeniz için ilk sayfanın görünüm durumunu içerir.

### <a name="circumventing-findcontrol"></a>FindControl'i atlatmak

Bir çapraz sayfa postback video walkthrough, ben ilk sayfada TextBox denetimine bir başvuru almak için FindControl yöntemini kullandı. Bu yöntem bu amaç için iyi çalışır, ancak FindControl pahalıdır ve ek kod yazmayı gerektirir. Neyse ki, ASP.NET 2.0 birçok senaryoda çalışacak bu amaç için FindControl için bir alternatif sağlar. PreviousPageType yönergesi, TypeName veya VirtualPath özniteliğini kullanarak önceki sayfaya güçlü bir şekilde yazılan bir başvuruya sahip olsanız. TypeName özniteliği, VirtualPath özniteliği sanal bir yol kullanarak önceki sayfaya başvurmanızı sağlarken, önceki sayfanın türünü belirtmenize olanak tanır. PreviousPageType yönergesini ayarladıktan sonra, ortak özellikleri kullanarak erişime izin vermek istediğiniz denetimleri vb. ortaya çıkarmanız gerekir.

## <a name="lab-1-cross-page-postback"></a>Laboratuvar 1 Çapraz Sayfa Postback

Bu laboratuvarda, ASP.NET 2.0'ın yeni sayfa arası postback işlevini kullanan bir uygulama oluşturursunuz.

1. Visual Studio 2005'i açın ve yeni bir ASP.NET Web sitesi oluşturun.
2. page2.aspx adlı yeni bir Web formu ekleyin.
3. Tasarım görünümünde Varsayılan.aspx'i açın ve bir Düğme denetimi ve TextBox denetimi ekleyin. 

    1. Düğme denetimine Gönder **Düğmesi'nin** kimliğini ve TextBox denetimine **Kullanıcı Adı'nın**kimliğini verin.
    2. Düğmenin PostBackUrl özelliğini page2.aspx olarak ayarlayın.
4. Kaynak görünümünde page2.aspx'i açın.
5. Aşağıda gösterildiği gibi bir @ PreviousPageType yönergesi ekleyin:
6. Page2.aspx'In kod arkası Sayfa\_Yüküne aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Yapı menüsünde Oluştur'a tıklayarak projeyi oluşturun.
8. Default.aspx için kod arkasına aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Sayfa2.aspx'teki Sayfa\_Yükünü aşağıdaki yle değiştirin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Projeyi derleyin.
11. Projeyi çalıştırın.
12. TextBox'a adınızı girin ve düğmeyi tıklatın.
13. Sonuç nedir?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0'daki Eşsenkronize Sayfalar

ASP.NET'daki birçok çekişme sorunu dış aramaların gecikmesi (Web hizmeti veya veritabanı çağrıları gibi), dosya IO gecikmesi vb. neden olur. bir ASP.NET uygulamasına karşı bir istek yapıldığında, ASP.NET bu isteğe hizmet etmek için alt iş iş parçacığından birini kullanır. İstek tamamlanana ve yanıt gönderilene kadar bu istek iş parçacığına sahiptir. ASP.NET 2.0, sayfaları eşzamanlı olarak yürütme özelliğini ekleyerek bu tür sorunlarla ilgili gecikme sorunlarını gidermeye çalışıyor. Bu, bir alt iş parçacığının isteği başlatıp ek yürütmeyi başka bir iş parçacığına devrederek kullanılabilir iş parçacığı havuzuna hızla dönebileceği anlamına gelir. Dosya IO, veritabanı arama, vb tamamlandığında, yeni bir iş parçacığı istek bitirmek için iş parçacığı havuzundan elde edilir.

Bir sayfanın eş senkronize bir şekilde yürütülmesini sağlamanın ilk adımı, sayfa yönergesinin **Async** özniteliğini şu şekilde ayarlamaktır:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Bu öznitelik sayfa için IHttpAsyncHandler uygulamak için ASP.NET söyler.

Bir sonraki adım PreRender önce sayfanın yaşam döngüsü bir noktada AddOnPreRenderCompleteAsync yöntemi aramaktır. (Bu yöntem genellikle Sayfa\_Yükü olarak adlandırılır.) AddOnPreRenderCompleteAsync yöntemi iki parametre alır; bir BeginEventHandler ve bir EndEventHandler. BeginEventHandler, Daha sonra EndEventHandler'a parametre olarak geçirilen bir IAsyncResult döndürür.

Aşağıdaki video, bir eşzamanlı sayfa isteğinin bir gözden geçirimidir.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Tam Ekran Video Aç](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Bir async sayfası, EndEventHandler tamamlanana kadar tarayıcıya işlemez. Şüphesiz ama bazı geliştiriciler async istekleria async geri aramaları benzer olarak düşünecek. Öyle olmadıklarını fark etmek önemlidir. Eşkenar dörtbir isteklere yarar, ilk alt iş parçacığının yeni isteklere hizmet vermek üzere iş parçacığı havuzuna iade edilebilmeve böylece IO'ya bağlı olması nedeniyle çekişmeyi azaltmasın.

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0'da Komut Dosyası Geri Aramaları

Web geliştiricileri her zaman bir geri arama ile ilişkili titreme önlemek için yollar aradı. 1.x ASP.NET, SmartNavigation titreme önlemek için en yaygın yöntem oldu, ama SmartNavigation istemci üzerindeki uygulama karmaşıklığı nedeniyle bazı geliştiriciler için sorunlara neden oldu. ASP.NET 2.0 bu sorunu komut dosyası geri aramalarıyla giderer. Komut dosyası geri aramaları, JavaScript üzerinden Web sunucusuna karşı istekte bulunmak için XMLHttp'i kullanır. XMLHttp isteği, tarayıcının DOM'u aracılığıyla manipüle edilebilen XML verilerini döndürür. XMLHttp kodu yeni WebResource.axd işleyicisi tarafından kullanıcıdan gizlenir.

ASP.NET 2.0'da bir komut dosyası geri aramasını yapılandırmak için gereken birkaç adım vardır.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>Adım 1 : ICallbackEventHandler Arayüzünü Uygulayın

ASP.NET sayfanızı komut dosyası geri aramasına katıldığını kabul edebilmek için ICallbackEventHandler arabirimini uygulamanız gerekir. Bunu kod arkası dosyanızda şöyle yapabilirsiniz:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Bunu @ Uygular yönergesini kullanarak da yapabilirsiniz:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

Satır ASP.NET kodunu kullanırken genellikle @ Uygular yönergesini kullanırsınız.

## <a name="step-2--call-getcallbackeventreference"></a>Adım 2 : GetCallbackEventReference'ı arayın

Daha önce de belirtildiği gibi, XMLHttp arama WebResource.axd işleyicisi içinde kapsüllenir. Sayfanız işlendiğinde, ASP.NET WebResource.axd\_tarafından sağlanan bir istemci komut dosyası olan WebForm DoCallback'e bir çağrı ekler. WebForm\_DoCallback işlevi, \_ \_geri arama için doPostBack işlevinin yerini alır. DoPostBack'in \_ \_sayfadaki formu programlı bir şekilde gönderdiğini unutmayın. Bir geri arama senaryosunda, bir postback \_ \_önlemek istediğiniz, bu nedenle doPostBack yeterli olmayacaktır.

> [!NOTE]
> \_\_doPostBack hala bir istemci komut dosyası geri arama senaryosunda sayfaya işlenir. Ancak, geri arama için kullanılmaz.

WebForm\_DoCallback istemci tarafı işlevi için bağımsız değişkenler normalde Page\_Load olarak çağrılacak sunucu tarafı işlevi GetCallbackEventReference üzerinden sağlanır. GetCallbackEventReference için tipik bir arama şu şekilde görünebilir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> Bu durumda cm, ClientScriptManager'ın bir örneğidir. ClientScriptManager sınıfı daha sonra bu modülde ele alınacaktır.

GetCallbackEventReference'ın birkaç aşırı yüklü sürümü vardır. Bu durumda, bağımsız değişkenler aşağıdaki gibidir:

`this`

GetCallbackEventReference'ın çağrıldığı denetime başvuru. Bu durumda, sayfanın kendisidir.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

İstemci tarafı kodundan sunucu tarafındaki olaya geçirilecek bir dize bağımsız değişkeni. Bu durumda, Im ddlCompany adlı bir açılır bırakma değerini geçen.

`ShowCompanyName`

Sunucu tarafındaki geri arama olayından geri dönüş değerini (dize olarak) kabul edecek istemci tarafı işlevinin adı. Bu işlev yalnızca sunucu tarafındaki geri arama başarılı olduğunda çağrılır. Bu nedenle, sağlamlık uğruna, genellikle bir hata durumunda yürütmek için istemci tarafı işlevinin adını belirten ek bir dize bağımsız değişkeni alır GetCallbackEventReference aşırı yüklü sürümünü kullanılması önerilir.

`null`

Sunucuya geri çağırmadan önce başlattığı istemci tarafı işlevini temsil eden dize. Bu durumda, böyle bir komut dosyası yoktur, bu nedenle bağımsız değişken geçersizdir.

`true`

Bir Boolean, geri aramanın eş senkronize bir şekilde yapılıp yapılmayacağını belirtir.

İstemci üzerinde\_WebForm DoCallback için arama bu bağımsız değişkenleri geçirecektir. Bu nedenle, bu sayfa istemcide işlendiğinde, bu kod aşağıdaki gibi görünecektir:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

İstemci üzerindeki işlevin imzasının biraz farklı olduğuna dikkat edin. İstemci tarafı işlevi 5 dizeleri ve bir Boolean geçer. Ek dize (yukarıdaki örnekte null) sunucu tarafı geri arama herhangi bir hata işleyecek istemci tarafı işlevi içerir.

## <a name="step-3--hook-the-client-side-control-event"></a>Adım 3 : İstemci Tarafı Kontrol Olayını Kancaya Takma

Yukarıdaki GetCallbackEventReference'ın iade değerinin bir dize değişkenine atandığını unutmayın. Bu dize, geri aramayı başlatan denetim için istemci tarafı olayını bağlamak için kullanılır. Bu örnekte, geri arama sayfada bir açılır tarafından başlatılır, bu yüzden *OnChange* olay kanca istiyorum.

İstemci tarafı olayını bağlamak için istemci tarafı işaretlemesine aşağıdaki gibi bir işleyici eklemeniz yeterlidir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

*CbRef'ın* GetCallbackEventReference çağrısından gelen iade değeri olduğunu hatırlayın. Yukarıda gösterilen WebForm\_DoCallback aramasını içerir.

## <a name="step-4--register-the-client-side-script"></a>Adım 4 : İstemci Tarafı Komut Dosyasını Kaydedin

GetCallbackEventReference'a yapılan çağrıda, sunucu tarafındaki geri arama başarılı olduğunda **ShowCompanyName** adlı istemci tarafındaki bir komut dosyasının yürütüleceğini belirttiğini hatırlayın. Bu komut dosyasının bir ClientScriptManager örneği kullanılarak sayfaya eklenmesi gerekir. (ClientScriptManager sınıfı daha sonra bu modülde tartışılacaktır.) Böyle yapıyorsun:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>Adım 5 : ICallbackEventHandler Arayüzü Yöntemleri arayın

ICallbackEventHandler, kodunuzda uygulamanız gereken iki yöntem içerir. Onlar **RaiseCallbackEvent** ve **GetCallbackEvent**vardır.

**RaiseCallbackEvent** bir argüman olarak bir dize alır ve hiçbir şey döndürür. Dize bağımsız değişkeni istemci tarafındaki çağrıdan\_WebForm DoCallback'e geçirilir. Bu durumda, bu değer *value* ddlCompany adı verilen açılır bırakma değer özniteliğidir. Sunucu tarafındaki kodunuz RaiseCallbackEvent yöntemine yerleştirilmelidir. Örneğin, geri aramanız harici bir kaynağa karşı bir Web İsteği yapıyorsa, bu kod RaiseCallbackEvent'e yerleştirilmelidir.

**GetCallbackEvent,** geri aramanın istemciye geri dönüşünü işlemekten sorumludur. Hiçbir argüman alır ve bir dize döndürür. Döndürdeceği dize, bu durumda *ShowCompanyName*istemci tarafı işlevine bir bağımsız değişken olarak geçirilir.

Yukarıdaki adımları tamamladıktan sonra, 2.0 ASP.NET bir komut dosyası geri arama gerçekleştirmeye hazırsınız.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Tam Ekran Video Aç](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET'daki komut dosyası geri aramaları, XMLHttp aramaları yapmayı destekleyen herhangi bir tarayıcıda desteklenir. Bu, günümüzde kullanılan tüm modern tarayıcıları içerir. Internet Explorer XMLHttp ActiveX nesnesini kullanırken, diğer modern tarayıcılar (yaklaşan IE 7 dahil) içsel bir XMLHttp nesnesi kullanır. Bir tarayıcının geri aramaları destekleyip desteklemediğinizi programlı olarak belirlemek için **Request.Browser.SupportCallback** özelliğini kullanabilirsiniz. İstenen istemci komut dosyası geri aramalarını destekliyorsa, bu özellik **doğru** döndürecektir.

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2.0'da İstemci Komut Dosyası ile Çalışma

ASP.NET 2.0'daki istemci komut dosyaları ClientScriptManager sınıfının kullanımı yla yönetilir. ClientScriptManager sınıfı, bir tür ve ad kullanarak istemci komut dosyalarını izler. Bu, aynı komut dosyasının bir sayfaya birden fazla kez programlı olarak eklenmesini önler.

> [!NOTE]
> Bir komut dosyası bir sayfaya başarıyla kaydedildikten sonra, aynı komut dosyasını kaydetmeye yönelik sonraki herhangi bir girişim, komut dosyasının ikinci kez kaydolmamasıyla sonuçlanır. Yinelenen komut dosyaları eklenmez ve özel bir durum oluşmaz. Gereksiz hesaplamayı önlemek için, komut dosyasının zaten kaydedilip kaydedilemediğini belirlemek için kullanabileceğiniz yöntemler vardır, böylece komut dosyasını birden fazla kez kaydetmeye çalışmayın.

ClientScriptManager yöntemleri tüm mevcut ASP.NET geliştiriciler için tanıdık olmalıdır:

## <a name="registerclientscriptblock"></a>Registerclientscriptblock

Bu yöntem, işlenen sayfanın üst bölümüne bir komut dosyası ekler. Bu, istemcide açıkça çağrılacak işlevleri eklemek için yararlıdır.

Bu yöntemin iki aşırı yüklenen sürümü vardır. Dört bağımsız değişkenden üçü bunlar arasında yaygındır. Bunlar:

`type (string)`

***Tür*** bağımsız değişkeni komut dosyası için bir türü tanımlar. Genellikle sayfanın türünü kullanmak iyi bir fikirdir (bu. Türü için GetType())

`key (string)`

***Anahtar*** bağımsız değişken, komut dosyası için kullanıcı tanımlı bir anahtardır. Bu, her komut dosyası için benzersiz olmalıdır. Aynı anahtara ve zaten eklemiş bir komut dosyası türüne sahip bir komut dosyası eklemeye çalışırsanız, bu komut dosyası eklenmez.

`script (string)`

***Komut dosyası*** bağımsız değişkeni, eklenecek gerçek komut dosyasını içeren bir dizedir. Komut dosyasını oluşturmak için bir StringBuilder kullanmanız ve ardından ***komut dosyası*** bağımsız değişkenini atamak için StringBuilder'daki ToString() yöntemini kullanmanız önerilir.

Yalnızca üç bağımsız değişken alan aşırı yüklü RegisterClientScriptBlock'u kullanıyorsanız, &lt;komut&gt;dosyanıza komut dosyası öğelerini (komut&lt;dosyası&gt; ve /komut dosyası) eklemeniz gerekir.

Dördüncü bir bağımsız değişken gerektiren RegisterClientScriptBlock'un aşırı yükünü kullanmayı seçebilirsiniz. Dördüncü bağımsız değişken, ASP.NET sizin için komut dosyası öğeleri eklemesi gerekip gerekmediğini belirten bir Boolean'dır. Bu bağımsız değişken **doğruysa,** komut dosyanız komut dosyası öğelerini açıkça içermemelidir.

Bir komut dosyasının zaten kaydedilmiş olup olmadığını belirlemek için IsClientScriptBlockRegistered yöntemini kullanın. Bu, önceden kaydedilmiş bir komut dosyasını yeniden kaydetme girişimini önlemenizi sağlar.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (2.0'da Yeni)

RegisterClientScriptInclude etiketi, harici bir komut dosyası dosyası dosyasına bağlantı veren bir komut dosyası bloğu oluşturur. İki aşırı yüklemesi var. Bir anahtar ve bir URL alır. İkinci türü belirten üçüncü bir bağımsız değişken ekler.

Örneğin, aşağıdaki kod, uygulamanın komut dosyası klasörünün kökünde jsfunctions.js'ye bağlantı veren bir komut dosyası bloğu oluşturur:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Bu kod, işlenen sayfada aşağıdaki kodu üretir:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> Komut dosyası bloğu sayfanın alt kısmında işlenir.

Bir komut dosyasının zaten kaydedilmiş olup olmadığını belirlemek için IsClientScriptIncludeRegistered yöntemini kullanın. Bu, bir komut dosyasını yeniden kaydetme girişimini önlemenizi sağlar.

## <a name="registerstartupscript"></a>Registerstartupscript

RegisterStartupScript yöntemi, RegisterClientScriptBlock yöntemiyle aynı bağımsız değişkenleri alır. RegisterStartupScript'e kayıtlı bir komut dosyası, sayfa yüklendikten sonra ancak OnLoad istemci tarafındaki olaydan önce çalıştırır. 1.X'te RegisterStartupScript'e kayıtlı komut dosyaları &lt;kapanış&gt; /form etiketinden hemen önce yerleştirilirken, RegisterClientScriptBlock'a kayıtlı komut dosyaları açılış &lt;formu&gt; etiketinden hemen sonra yerleştirildi. 2.0 ASP.NET, her ikisi de &lt;kapanış&gt; /form etiketinden hemen önce yerleştirilir.

> [!NOTE]
> Bir işlevi RegisterStartupScript ile kaydederseniz, istemci tarafı kodunda açıkça aramadan bu işlev yürütülmez.

Bir komut dosyasının zaten kaydedilmiş olup olmadığını belirlemek ve bir komut dosyasını yeniden kaydetme girişimini önlemek için IsStartupScriptRegistered yöntemini kullanın.

## <a name="other-clientscriptmanager-methods"></a>Diğer ClientScriptManager Yöntemleri

ClientScriptManager sınıfının diğer yararlı yöntemlerinden bazıları aşağıda verilmiştir.

|  <strong>Getcallbackeventreference</strong>   |                                                 Bu modülde daha önceki komut dosyası geri aramalarına bakın.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                İstemci tarafındaki bir olaydan geri göndermek için kullanılabilecek bir JavaScript başvurusu (javascript:&lt;call)&gt;alır.                 |
|  <strong>Getpostbackeventreference</strong>   |                                   İstemciden bir gönderiyi başlatmak için kullanılabilecek bir dize alır.                                    |
|      <strong>GetWebResourceUrl</strong>       | URL'yi derlemeye katıştırılmış bir kaynağa döndürür. <strong>RegisterClientScriptResource</strong>ile birlikte kullanılmalıdır. |
| <strong>Registerclientscriptresource</strong> |     Sayfaya bir Web kaynağı kaydeder. Bunlar bir derlemeye katıştırılmış ve yeni WebResource.axd işleyicisi tarafından işlenen kaynaklardır.      |
|     <strong>Registerhiddenfield</strong>      |                                                 Sayfaya gizli bir form alanını kaydeder.                                                 |
|  <strong>RegisteronSubmitStatement</strong>   |                                  HTML formu gönderildiğinde çalıştıran istemci tarafı kodunu kaydeder.                                   |
