---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Sunucu Denetimleri | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET 2.0 birçok yönden sunucu denetimleri geliştirir. Bu modülde, 2.0 ve Visual Studio 200 ASP.NET şekilde bazı mimari değişiklikleri ele alacağız ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543749"
---
# <a name="server-controls"></a>Sunucu Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2.0 birçok yönden sunucu denetimleri geliştirir. Bu modülde, 2.0 ve Visual Studio 2005 ASP.NET sunucu denetimleri ile ilgili bazı mimari değişiklikleri ele alacağız.

ASP.NET 2.0 birçok yönden sunucu denetimleri geliştirir. Bu modülde, 2.0 ve Visual Studio 2005 ASP.NET sunucu denetimleri ile ilgili bazı mimari değişiklikleri ele alacağız.

## <a name="view-state"></a>Durumu görüntüle

ASP.NET 2.0'daki görünüm durumundaki birincil değişiklik, boyutunda belirgin bir azalmadır. Üzerinde yalnızca Takvim denetimi olan bir sayfa düşünün. Burada ASP.NET 1.1 görünüm durumudur.

[!code-css[Main](server-controls/samples/sample1.css)]

Şimdi burada ASP.NET 2.0 aynı sayfada görünüm durumu.

[!code-css[Main](server-controls/samples/sample2.css)]

Bu oldukça önemli bir değişiklik, ve bu görünüm durumu tel üzerinde ileri geri taşınır göz önüne alındığında, bu değişiklik geliştiriciler önemli bir performans artışı verebilir. Görünüm durumunun boyutundaki azalma büyük ölçüde onu dahili olarak ele verme biçimimizdir. Görünüm durumunun Base64 kodlanmış bir dize olduğunu unutmayın. ASP.NET 2.0'daki görünüm durumunu daha iyi anlamak için, yukarıdaki örneklerden çözülmüş değerlere bir göz atalım.

İşte 1.1 görünümü durumu deşifre edilir:

[!code-css[Main](server-controls/samples/sample3.css)]

Bu biraz anlamsız görünebilir, ama burada bir düzen var. 1.x ASP.NET veri türlerini tanımlamak ve &lt; &gt; karakterleri kullanarak değerleri sınırlandırmak için tek karakterler kullandık. Yukarıdaki görünüm durumu örneğindeki "t" bir Üçüz'u temsil eder. Üçüz bir çift ArrayLists içerir ("l" bir ArrayList'i temsil eder.) Bu ArrayLists biri 1 değeri ile bir Int32 ("i") içerir ve diğer başka bir Triplet içerir. Triplet ArrayLists, vb bir çift içerir. Unutulmaması gereken en önemli şey, çiftler içeren Triplets kullanmak, biz bir harf ile &lt; veri &gt; türleri tanımlamak, ve biz sınırlayıcıolarak ve karakterleri kullanın.

2.0 ASP.NET, kodlanmış görünüm durumu biraz farklı görünüyor.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Deşifre edilmiş görünüm durumunun görünümünde büyük bir değişiklik fark etmelisiniz. Bu değişikliğin birkaç mimari temeli vardır. ASP.NET 1.x'teki durumu görüntüle, verileri serileştirmek için LosFormatter'ı kullandı. 2.0'da yeni ObjectStateFormatter sınıfını kullanıyoruz. Bu sınıf, görünüm durumu ve denetim durumunun serileştirilmesine ve deserializasyonuna yardımcı olmak için özel olarak tasarlanmıştır. (Kontrol durumu sonraki bölümde ele alınacaktır.) Serileştirme ve deserialization'ın gerçekleşme yöntemini değiştirerek elde edilen birçok fayda vardır. En dramatik biri bir TextWriter kullanan LosFormatter aksine, ObjectStateFormatter bir BinaryWriter kullanır gerçektir. Bu, ASP.NET 2.0'ın görünüm durumunu dizeleri yerine bir dizi bayt depolamasına olanak tanır. Örneğin, bir karşıcıyı ele alalım. 1.1 ASP.NET bir tamsayı 4 bayt görüş durumuna ihtiyaç doldu. 2.0 ASP.NET, aynı tamsayı sadece 1 bayt gerektirir. Depolanan görünüm durumu miktarını azaltmak için diğer geliştirmeler yapıldı. Örneğin DateTime değerleri artık dize yerine TickCount kullanılarak depolanır.

Tüm bunlar yeterli değilmiş gibi, 1.x'teki en büyük görüş tüketicilerinden birinin DataGrid ve benzeri kontroller olduğu gerçeğine özel önem verildi. Görünüm durumu söz konusu olduğunda DataGrid gibi denetimlerin önemli bir dezavantajı, genellikle büyük miktarda yinelenen bilgi içermesidir. 1.x ASP.NET, bu tekrarlanan bilgiler tekrar tekrar depolandı ve bu da şişirilmiş bir görünüm durumuna neden oldu. 2.0 ASP.NET, bu tür verileri depolamak için yeni IndexedString sınıfını kullanırız. Bir dize yinelerse, indexedString için belirteci ve dizin IndexedString nesnelerin çalışan bir tablo içinde saklarız.

## <a name="control-state"></a>Kontrol Durumu

Geliştiricilerin görünüm durumu yla ilgili en önemli sıkıntılarından biri, HTTP yüküne eklenen boyuttu. Daha önce de belirtildiği gibi, görünüm durumunun en büyük tüketicilerinden biri DataGrid denetimidir. Bir DataGrid tarafından oluşturulan büyük miktarda görünüm durumu önlemek için, birçok geliştirici yalnızca bu denetim için görünüm durumunu devre dışı bıraktı. Ne yazık ki, bu çözüm her zaman iyi bir değildi. 1.xASP.NETdeki durumu görüntüleme, yalnızca denetimin doğru işlevselliği için gerekli verileri içermez. Ayrıca, denetimin Kullanıcı Aracı'nın durumuyla ilgili bilgiler de içerir. Bu, Bir DataGrid'de duraklamaya izin vermek istiyorsanız, durumu görüntüleyen kullanıcı arabirimi bilgilerinin tümüne ihtiyacınız olmasa bile görünüm durumunu etkinleştirmeniz gerektiği anlamına gelir. Ya hep ya hiç senaryosu.

2.0ASP.NET, kontrol durumu bu sorunu kontrol durumunun devreye girmesiyle güzel cereyan eder. Denetim durumu, bir denetimin düzgün işlevselliği için kesinlikle gerekli olan verileri içerir. Görünüm durumundan farklı olarak denetim durumu devre dışı tutulamaz. Bu nedenle, denetim durumunda depolanan verilerin dikkatle denetlenir olması önemlidir.

> [!NOTE]
> Denetim durumu VIEWSTATE gizli form alanında \_görünüm durumu ile birlikte devam etti. \_

Bu video, görüntü durumu ve denetim durumu bir walkthrough olduğunu.

![](server-controls/_static/image1.png)

[Tam Ekran Video Aç](server-controls/_static/state1.wmv)

Bir sunucu denetiminin durumu kontrol etmek için okuma ve yazma için üç adım atmalısınız.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>Adım 1: RegisterRequiresControlState Yöntemini Arayın

RegisterRequiresControlState yöntemi, denetim durumunu n ASP.NET devam ettirmesi gerektiğini bildirir. Bu kayıtlı olan denetim türü Denetim bir bağımsız değişken alır.

Kayıt isteği istek ten devam etmediğini unutmayın. Bu nedenle, denetim denetim durumunu sürdürmek için bu yöntem her istek üzerinde çağrılmalıdır. Yöntemin OnInit'te çağrılması önerilir.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>Adım 2: KaydEtKontrolDurumunu Geçersiz Kılma

SaveControlState yöntemi, son gönderi den bu yana denetim durumu değişikliklerini denetim için kaydeder. Denetimin durumunu temsil eden bir nesne döndürür.

## <a name="step-3-override-loadcontrolstate"></a>Adım 3: Yük Kontrol Durumunu Geçersiz Kılma

LoadControlState yöntemi kaydedilen durumu bir denetime yükler. Yöntem, denetim için kaydedilen durumu tutan nesne türünden bir bağımsız değişken alır.

## <a name="full-xhtml-compliance"></a>Tam XHTML Uyumluluğu

Herhangi bir Web geliştiricisi, Web uygulamalarında standartların önemini bilir. Standartlara dayalı bir geliştirme ortamı sağlamak için, ASP.NET 2.0 tamamen XHTML uyumludur. Bu nedenle, tüm etiketler, HTML 4.0 veya daha büyük destekleyen tarayıcılarda XHTML standartlarına göre işlenir.

1.1 ASP.NET DOCTYPE tanımı aşağıdaki gibidir:

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0'da varsayılan DOCTYPE tanımı aşağıdaki gibidir:

[!code-html[Main](server-controls/samples/sample7.html)]

İsterseniz, yapılandırma dosyasındaki xhtmlConformance düğümü aracılığıyla varsayılan XHTML uyumluluğunu değiştirebilirsiniz. Örneğin, web.config dosyasındaki aşağıdaki düğüm XHTML uyumluluğunu XHTML 1.0 Katı olarak değiştirir:

[!code-xml[Main](server-controls/samples/sample8.xml)]

İsterseniz, ASP.NET 1.x'te kullanılan eski yapılandırmayı aşağıdaki gibi kullanmak üzere ASP.NET da yapılandırabilirsiniz:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Adaptörleri Kullanarak Uyarlamalı Görüntüleme

1.x ASP.NET, yapılandırma dosyasında &lt;bir&gt; HttpBrowserYetenekleri nesnesi bulunan bir browserCaps bölümü bulunur. Bu nesne, bir geliştiricinin hangi aygıtın belirli bir istekte bulunduğunu belirlemesine ve kodu uygun şekilde işlemesine olanak tanır. ASP.NET 2.0'da model geliştirildi ve şimdi yeni ControlAdapter sınıfını kullanıyor. ControlAdapter sınıfı, denetimin yaşam döngüsündeki olayları geçersiz kılar ve kullanıcı aracısının özelliklerine göre denetimlerin işlenmesini denetler. Belirli bir kullanıcı aracısının yetenekleri c:\windows\microsoft.net\framework\v2.0'da depolanan bir tarayıcı tanım dosyası (.tarayıcı dosya uzantısı olan bir dosya) tarafından tanımlanır. \* \* \*\CONFIG\Tarayıcılar klasörü. \*

> [!NOTE]
> ControlAdapter sınıfı soyut bir sınıftır.

&lt;1.x'teki&gt; browserCaps bölümü gibi, tarayıcı tanım dosyası da isteyen tarayıcıyı tanımlamak için kullanıcı aracısı dizesini ayrıştırmak için Düzenli İfade kullanır. Bunlar, bu kullanıcı aracısı için belirli yetenekleri tanımlar. ControlAdapter, denetimi Render yöntemi yle işler. Bu nedenle, Render yöntemini geçersiz kılarsanız, temel sınıfta Render'ı aramamalısınız. Bunu yapmak, işlemenin iki kez, bağdaştırıcı için bir kez ve denetimin kendisi için bir kez oluşmasına neden olabilir.

## <a name="developing-a-custom-adapter"></a>Özel Bağdaştırıcı Geliştirme

ControlAdapter'dan devralarak kendi özel bağdaştırıcınızı geliştirebilirsiniz. Ayrıca, bir sayfa için bağdaştırıcının gerekli olduğu durumlarda, soyut sınıf PageAdapter'dan devralabilirsiniz. Denetimlerin özel bağdaştırıcınıza eşlenemi, tarayıcı tanım dosyasındaki &lt;controlAdapters&gt; öğesi üzerinden gerçekleştirilir. Örneğin, bir tarayıcı tanımı dosyasından aşağıdaki XML Menü denetimini MenuAdapter sınıfına eşler:

[!code-html[Main](server-controls/samples/sample10.html)]

Bu modeli kullanarak, bir kontrol geliştiricisinin belirli bir aygıtı veya tarayıcıyı hedeflemesi oldukça kolay laşır. Ayrıca, bir geliştiricinin sayfaların her cihazda nasıl işlendiği üzerinde tam kontrole sahip olması da oldukça basittir.

## <a name="per-device-rendering"></a>Cihaz Başına Görüntüleme

ASP.NET 2.0'daki sunucu denetim özellikleri tarayıcıya özgü bir öneki kullanılarak aygıt başına belirtilebilir. Örneğin, aşağıdaki kod, sayfaya göz atmak için hangi aygıtın kullanıldığına bağlı olarak etiket metnini değiştirir.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Bu etiketi içeren sayfaya Internet Explorer'dan göz atıldığında, etikette "Internet Explorer'dan geziniyorsunuz" yazan bir metin görüntülenir. Sayfafirefox'tan göz atıldığında, etiket "Firefox'tan geziniyorsunuz" metnini görüntüler. Sayfaya başka bir aygıttan göz atıldığında, "Bilinmeyen bir aygıttan geziniyorsunuz" görüntülenir. Herhangi bir özellik bu özel sözdizimi kullanılarak belirtilebilir.

## <a name="setting-focus"></a>Odak Ayarlama

ASP.NET 1.x geliştiricileri sık sık belirli bir denetim üzerinde ilk odak ayarlamak için nasıl sordu. Örneğin, bir giriş sayfasında, sayfa ilk yüklendiğinde Kullanıcı Kimliği textbox'ın odağı olması yararlıdır. 1.xASP.NETde, bunu yapmak bazı istemci tarafı komut dosyası yazmayı gerektiriyor. Böyle bir komut dosyası önemsiz bir görev olsa da, SetFocus yöntemi sayesinde ASP.NET 2.0'da artık gerekli değildir. SetFocus yöntemi, odak alması gereken denetimi gösteren bir bağımsız değişken alır. Bu bağımsız değişken, denetimin bir dize olarak istemci kimliği veya Denetim nesnesi olarak Sunucu denetiminin adı olabilir. Örneğin, sayfa ilk yüklendiğinde ilk netlemeyi txtUserID adı verilen bir TextBox\_denetimine ayarlamak için Sayfa Yükü'ne aşağıdaki kodu ekleyin:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-- veya

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0, odak noktasını ayarlayan istemci tarafı işlevini işlemek için Webresource.axd işleyicisini (daha önce tartışılan) kullanır. İstemci tarafı işlevinin adı\_burada gösterildiği gibi WebForm AutoFocus olduğunu:

[!code-html[Main](server-controls/samples/sample14.html)]

Alternatif olarak, ilk odağı bu denetime ayarlamak için denetim için Odak yöntemini kullanabilirsiniz. Odaklama yöntemi Denetim sınıfından türetilmiştir ve tüm ASP.NET 2.0 denetimleri için kullanılabilir. Doğrulama hatası oluştuğunda belirli bir denetime odak ayarlamak da mümkündür. Bu daha sonraki bir modülde ele alınacaktır.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0'da Yeni Sunucu Denetimleri

Aşağıda ASP.NET 2.0'daki yeni sunucu denetimleri veremistir. Daha sonraki modüllerde bazıları hakkında daha fazla detaya gireceğiz.

## <a name="imagemap-control"></a>ImageMap Kontrolü

ImageMap denetimi, bir gönderiyi geri başlatabilen veya URL'ye gidebilecek bir resme etkin noktalar eklemenize olanak tanır. Üç tür etkin nokta vardır; CircleHotSpot, DikdörtgenHotSpot ve PolygonHotSpot. Etkin noktalar Visual Studio'daki bir koleksiyon düzenleyicisi aracılığıyla veya programlı olarak kod olarak eklenir. Görüntüüzerinde etkin noktalar çizmek için kullanılabilir kullanıcı arabirimi yoktur. Etkin noktanın koordinatları ve boyutu veya yarıçapı bildirimsel olarak belirtilmelidir. Ayrıca tasarımcı bir hotspot görsel temsili yoktur. Bir etkin nokta bir URL'ye gidecek şekilde yapılandırılırsa, URL etkin noktanın Gezinme Url özelliği üzerinden belirtilir. Bir gönderi geri hotspot durumunda, PostBackValue özelliği sunucu tarafı kodunda alınabilir sonrası geri bir dize geçmek için izin verir.

![HotSpot Collection Editörü - Visual Studio](server-controls/_static/image1.jpg)

**Şekil 1**: Visual Studio'da HotSpot Koleksiyon Editörü

## <a name="bulletedlist-control"></a>Madde İşaretli Liste Kontrolü

Madde İşareti Listesi denetimi, veriye kolayca bağlanabilen bir madde işaretli listedir. Liste, BulletStyle özelliği üzerinden sipariş edilebilir (numaralandırılabilir) veya sırasız olabilir. Listedeki her öğe bir ListItem nesnesi tarafından temsil edilir.

![Visual Studio'da BulletedList Kontrolü](server-controls/_static/image1.gif)

**Şekil 2**: Visual Studio'da BulletedList Control

## <a name="hiddenfield-control"></a>HiddenField Kontrolü

HiddenField denetimi, sayfanıza değeri sunucu tarafı kodunda bulunan gizli bir form alanı ekler. Gizli form alanının değerinin genellikle posta arkaları arasında değişmeden kalması beklenir. Ancak, kötü amaçlı bir kullanıcının geri göndermeden önce değeri değiştirmesi mümkündür. Bu durumda, HiddenField denetimi ValueChanged olayını yükseltir. HiddenField denetiminde hassas bilgiler varsa ve değişmediğinden emin olmak istiyorsanız, kodunuzda Değer Değiştiren olayını işlemeniz gerekir.

## <a name="fileupload-control"></a>FileUpload Denetimi

ASP.NET 2.0'daki FileUpload denetimi, ASP.NET bir sayfa üzerinden bir Web sunucusuna dosya yüklemeyi mümkün kılar. Bu denetim birkaç istisna dışında ASP.NET 1.x HtmlInputFile sınıfına oldukça benzer. 1.x ASP.NET, iyi bir dosyanız olup olmadığını belirlemek için PostedFile özelliğinin null olup olmadığının kontrol edilmesi önerilir. ASP.NET 2.0'daki FileUpload denetimi, aynı amaç için kullanabileceğiniz yeni bir HasFile özelliği ekler ve biraz daha verimlidir.

PostedFile özelliği hala bir HttpPostedFile nesnesine erişmek için kullanılabilir, ancak HttpPostedFile bazı işlevsellik şimdi dosya yükleme denetimi ile özünde kullanılabilir. Örneğin, yüklenen bir dosyayı ASP.NET 1.x olarak kaydetmek için HttpPostedFile nesnesinde SaveAs yöntemini çağırırsınız. 2.0 ASP.NET'daki FileUpload denetimini kullanarak, FileUpload denetiminde SaveAs yöntemini çağırırsınız.

2.0 davranışındaki (ve büyük olasılıkla en önemli değişiklik) bir diğer önemli değişiklik de, yüklenen dosyanın tamamını kaydetmeden önce belleğe yüklemenin artık gerekli olmamasıdır. 1.x'te, yüklenen herhangi bir dosya diske yazılmadan önce tamamen belleğe kaydedilir. Bu mimari, büyük dosyaların yüklenmesini engeller.

ASP.NET 2.0'da, httpRuntime öğesinin requestLengthDiskThreshold özelliği, diske yazılmadan önce bellekte kaç Kilobayt tutulduğunu yapılandırmanızı sağlar.

**ÖNEMLİ**: MSDN belgeleri (ve başka yerlerdeki belgeler) bu değerin bayt (Kilobayt değil) olduğunu ve varsayılan değerin 256 olduğunu belirtir. Değer aslında Kilobytes belirtilir ve varsayılan değeri 80'dir. Varsayılan değeri 80K olan, arabellek büyük nesne yığını üzerinde sona ermez emin olun.

## <a name="wizard-control"></a>Sihirbaz Denetimi

Panelleri kullanarak veya sayfadan sayfaya aktararak bir dizi "sayfa" içinde bilgi toplamaya çalışan ASP.NET geliştiricilerle karşılaşmak oldukça yaygındır. Çoğu zaman, çaba sinir bozucu bir ve zaman alıcı. Yeni Sihirbaz denetimi, kullanıcıların aşina olduğu bir sihirbaz arabiriminde doğrusal ve doğrusal olmayan adımlara izin vererek sorunları çözer. Sihirbaz denetimi, giriş formlarını bir dizi adımda sunar. Her adım, denetimin StepType özelliği tarafından belirtilen belirli bir türdedir. Kullanılabilir adım türleri aşağıdaki gibidir:

| **Adım Türü** | **Açıklama** |
| --- | --- |
| Otomatik | Sihirbaz, adım hiyerarşisi içindeki konumuna göre adım türünü otomatik olarak belirler. |
| Başlat | İlk adım, genellikle bir giriş deyimi sunmak için kullanılır. |
| Adım | Normal bir adım. |
| Son | Son adım, genellikle sihirbazı bitirmek için bir düğme sunmak için kullanılır. |
| Complete | Başarı veya başarısızlık iletisi sunar. |

> [!NOTE]
> Sihirbaz denetimi, ASP.NET denetim durumunu kullanarak durumunu izler. Bu nedenle, EnableViewState özelliği herhangi bir zarar olmadan false olarak ayarlanabilir.

Bu video Sihirbaz denetiminin bir bölümüdür.

![](server-controls/_static/image2.png)

[Tam Ekran Video Aç](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Denetimi Yerelleştir

Yerelleştirme denetimi, Literal denetime benzer. Ancak, Yerelleştirme denetimi, ona eklenen biçimlendirmenin nasıl işlenmediğini denetleyen bir **Mode** özelliğine sahiptir. Mod özelliği aşağıdaki değerleri destekler:

| **Mod** | **Açıklama** |
| --- | --- |
| Dönüşüm | Biçimlendirme, isteği yapan tarayıcının protokolüne göre dönüştürülür. |
| Geçiş | Biçimlendirme olduğu gibi işlenir. |
| Kodlama | Denetime eklenen biçimlendirme HtmlEncode kullanılarak kodlanır. |

## <a name="multiview-and-view-controls"></a>MultiView ve View Denetimleri

MultiView denetimi Görünüm denetimleri için bir kapsayıcı gibi davranır ve Görünüm denetimi diğer denetimler için bir kapsayıcı (panel denetimi gibi) olarak hareket eder. MultiView denetimindeki her görünüm tek bir Görünüm denetimiyle temsil edilir. MultiView'deki ilk Görünüm denetimi görünüm 0, ikincisi görünüm 1, vb. MultiView denetiminin ActiveViewIndex'ini belirterek görünümler arasında geçiş yapabilirsiniz.

## <a name="substitution-control"></a>İkame Kontrolü

İkame denetimi ASP.NET önbelleğe alma ile birlikte kullanılır. Önbelleğe alma işleminden yararlanmak istediğiniz, ancak her istekte güncellenmesi gereken bir sayfanın bölümlerine sahip olduğunuz durumlarda (diğer bir deyişle, önbelleğe alınan bir sayfanın bölümleri), Değiştirme bileşeni harika bir çözüm sağlar. Denetim aslında kendi başına herhangi bir çıktı render değildir. Bunun yerine, sunucu tarafı kodunda bir yönteme bağlıdır. Sayfa istendiğinde, yöntem çağrılır ve döndürülen biçimlendirme ikame denetimi yerine işlenir.

Değiştirme denetiminin bağlı olduğu yöntem **MethodName** özelliği ile belirtilir. Bu yöntem aşağıdaki ölçütleri karşılamalıdır:

- Statik (VB'de paylaşılan) bir yöntem olmalıdır.
- Bir parametreyi kabul eder HttpContext türü.
- Sayfadaki denetimi değiştirmesi gereken biçimlendirmeyi temsil eden bir dize döndürür.

Değiştirme denetimi, sayfadaki başka bir denetimi değiştirme yeteneğine sahip değildir, ancak parametresi üzerinden geçerli HttpContext'a erişebilir.

## <a name="gridview-control"></a>GridView Denetimi

GridView denetimi, DataGrid denetiminin yerini aldı. Bu denetim daha sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="detailsview-control"></a>DetailsView Denetimi

DetailsView denetimi, bir veri kaynağından tek bir kaydı görüntülemenize ve bunu düzenlemenize veya silmenize olanak tanır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="formview-control"></a>FormView Denetimi

FormView denetimi, bir veri kaynağından gelen tek bir kaydı yapılandırılabilir bir arabirimde görüntülemek için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="accessdatasource-control"></a>AccessDataSource Denetimi

AccessDataSource denetimi, access veritabanını veri ye bağlamak için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="objectdatasource-control"></a>ObjectDataSource Denetimi

ObjectDataSource denetimi, denetimlerin doğrudan veri kaynağına bağlı olduğu iki katmanlı bir modelin aksine, denetimlerin orta katmanlı bir iş nesnesine veri ye bağlı olabilmesi için üç katmanlı bir mimariyi desteklemek için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="xmldatasource-control"></a>XmlDataSource Kontrolü

XmlDataSource denetimi, bir XML veri kaynağına veri bağlamak için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource Kontrolü

SiteMapDataSource denetimi, site haritasını temel alan site gezinti denetimleri için veri bağlama sağlar. Daha sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="sitemappath-control"></a>SiteMapPath Kontrolü

SiteMapPath denetimi, genellikle ekmek kırıntıları olarak adlandırılan bir dizi gezinme bağlantısını görüntüler. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="menu-control"></a>Menü Kontrolü

Menü denetimi DHTML kullanarak dinamik menüleri görüntüler. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="treeview-control"></a>TreeView Denetimi

TreeView denetimi, verilerin hiyerarşik ağaç görünümünü görüntülemek için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="login-control"></a>Giriş Kontrolü

Giriş denetimi, bir Web sitesine giriş yapmak için bir mekanizma sağlar. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="loginview-control"></a>GirişGörünümü Kontrolü

LoginView denetimi, kullanıcının giriş durumuna bağlı olarak farklı şablonların görüntülenmesine olanak tanır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="passwordrecovery-control"></a>PasswordRecovery Denetimi

ParolaKurtarma denetimi, ASP.NET bir uygulamanın kullanıcıları tarafından unutulan parolaları almak için kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="loginstatus"></a>Loginstatus

Giriş Durumu denetimi, kullanıcının giriş durumunu görüntüler. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="loginname"></a>Loginname

LoginName denetimi, bir ASP.NET uygulamasına giriş yaptıktan sonra kullanıcının kullanıcı adını görüntüler. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard, kullanıcılara ASP.NET bir uygulamada kullanılmak üzere ASP.NET üyelik hesabı oluşturma olanağı sağlayan yapılandırılabilir bir sihirbazdır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="changepassword"></a>Changepassword

ChangePassword denetimi, kullanıcıların ASP.NET bir uygulama için parolalarını değiştirmelerine olanak tanır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınmıştır.

## <a name="various-webparts"></a>Çeşitli Web Parçaları

ASP.NET çeşitli Web Parçaları ile 2.0 gemi. Bunlar daha sonraki bir modülde ayrıntılı olarak ele alınacaktır.
