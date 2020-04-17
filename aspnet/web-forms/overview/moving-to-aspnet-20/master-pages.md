---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Ana Sayfalar | Microsoft Dokümanlar
author: rick-anderson
description: Başarılı bir Web sitesinin temel bileşenlerinden biri tutarlı bir görünüm ve histir. 1.x ASP.NET, geliştiriciler ortak sayfa elem çoğaltmak için kullanıcı denetimleri kullanılır ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543190"
---
# <a name="master-pages"></a>Ana Sayfalar

[Microsoft](https://github.com/microsoft) tarafından

> Başarılı bir Web sitesinin temel bileşenlerinden biri tutarlı bir görünüm ve histir. 1.x'ASP.NET geliştiriciler, bir Web uygulamasında ortak sayfa öğelerini çoğaltmak için kullanıcı denetimlerini kullandı. Bu kesinlikle uygulanabilir bir çözüm olsa da, kullanıcı denetimleri kullanarak bazı dezavantajları var. Örneğin, kullanıcı denetiminin konumundaki bir değişiklik, bir sitedeki birden çok sayfada değişiklik gerektirir. Kullanıcı denetimleri, bir sayfaya yerleştirildikten sonra Tasarım görünümünde de işlenmez.

Başarılı bir Web sitesinin temel bileşenlerinden biri tutarlı bir görünüm ve histir. 1.x'ASP.NET geliştiriciler, bir Web uygulamasında ortak sayfa öğelerini çoğaltmak için kullanıcı denetimlerini kullandı. Bu kesinlikle uygulanabilir bir çözüm olsa da, kullanıcı denetimleri kullanarak bazı dezavantajları var. Örneğin, kullanıcı denetiminin konumundaki bir değişiklik, bir sitedeki birden çok sayfada değişiklik gerektirir. Kullanıcı denetimleri, bir sayfaya yerleştirildikten sonra Tasarım görünümünde de işlenmez.

ASP.NET 2.0, Master sayfalarını tutarlı bir görünüm ve his sağlamanın bir yolu olarak sunar ve yakında göreceğiniz gibi, Ana sayfalar kullanıcı denetimi yöntemine göre önemli bir gelişmeyi temsil eder.

## <a name="why-master-pages"></a>Neden Ana Sayfalar?

2.0'ASP.NET ana sayfalara neden ihtiyaç duyulduğunu merak ediyor olabilirsiniz. Sonuçta, Web sitesi geliştiricileri zaten ASP.NET 1.x'teki kullanıcı denetimlerini kullanarak içerik alanlarını sayfalar arasında paylaşıyor. Kullanıcı denetimlerinin ortak bir düzen oluşturmak için en uygun çözümden daha az olmasının aslında birkaç nedeni vardır.

Kullanıcı denetimleri aslında sayfa düzenini tanımlamaz. Bunun yerine, sayfanın bir bölümünün düzenini ve işlevselliğini tanımlarlar. Bu ikisi arasındaki ayrım önemlidir, çünkü kullanıcı denetim çözümünün yönetilebilirliğini çok daha zor hale getirir. Örneğin, sayfanızdaki bir kullanıcı denetiminin konumunu değiştirmek istediğinizde, kullanıcı denetiminin göründüğü gerçek sayfayı değiştirmeniz gerekir. Sadece birkaç sayfa varsa Thats ince, ama büyük sitelerde, hızlı bir site yönetimi kabus olur!

Ortak bir düzeni tanımlamak için kullanıcı denetimlerini kullanmanın bir diğer dezavantajı da ASP.NET mimarisine bağlıdır. Kullanıcı denetiminin ortak üyelerinden herhangi biri değiştirilirse, kullanıcı denetimini kullanan tüm sayfaları yeniden derlemeniz gerektirin. Buna karşılık, ASP.NET daha sonra ilk erişildiğinde sayfalarınızı yeniden JIT olacaktır. Bu, bir kez daha, ölçeklenebilir olmayan bir mimari ve daha büyük siteler için bir site yönetimi sorunu üretir.

Bu sorunların her ikisi de (ve daha birçok) güzel ASP.NET 2.0 ana sayfaları tarafından ele alınmıştır.

## <a name="how-master-pages-work"></a>Ana Sayfalar Nasıl Çalışır?

Ana sayfa, diğer sayfalar için bir şablona benzer. Diğer sayfalar arasında paylaşılması gereken sayfa öğeleri (örn. menüler, kenarlıklar, vb.) ana sayfaya eklenir. Siteye yeni sayfalar eklendiğinde, bunları bir ana sayfayla ilişkilendirebilirsiniz. Ana sayfayla ilişkili bir sayfaya **içerik sayfası**denir. Varsayılan olarak, bir içerik sayfası ana sayfadan görünüm alır. Ancak, bir ana sayfa oluşturduğunuzda, sayfanın içerik sayfasının kendi içeriğiyle değiştirebileceği bölümlerini tanımlayabilirsiniz. Bu bölümler, ASP.NET 2.0'da tanıtılan yeni bir denetim kullanılarak tanımlanır; **ContentPlaceHolder** kontrolü.

Ana sayfa herhangi bir sayıda ContentPlaceHolder denetimi içerebilir (veya hiç içermez.) İçerik sayfasında, ContentPlaceHolder denetimlerinden gelen içerik **İçerik** denetimlerinin içinde görünür ve ASP.NET 2.0'daki yeni bir denetim. Varsayılan olarak, kendi içeriğinizi sağlayabilmeniz için İçerik sayfaları İçerik denetimleri boştur. İçerik denetimlerinin içindeki ana sayfadaki içeriği kullanmak istiyorsanız, bu modülde daha sonra göreceğiniz gibi bunu yapabilirsiniz. İçerik denetimi, İçerik denetiminin ContentPlaceHolderID özelliği aracılığıyla ContentPlaceHoldercontrol denetimine eşlenir. Aşağıdaki kod, bir İçerik denetimini ana sayfada mainBody olarak adlandırılan ContentPlaceHolder denetimiyle eşler.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> İnsanların ana sayfaları diğer sayfalar için bir taban sınıf olarak tanımladığını sık sık duyarsınız. Bu aslında doğru değil. Ana sayfalar ve içerik sayfaları arasındaki ilişki kalıtım değildir.

**Şekil 1,** Visual Studio 2005'te göründükleri gibi bir ana sayfayı ve ilişkili bir içerik sayfasını gösterir. ContentPlaceHolder denetimini ana sayfada ve ilgili İçerik denetimini içerik sayfasında görebilirsiniz. İçerik Sahibinin dışındaki ana sayfaların içeriğinin görünür olmasına ancak içerik sayfasında gri renkte olduğuna dikkat edin. İçerik Alanı Tutucu'nun içindeki içerik, içerik sayfası tarafından yerine konabilir. Ana sayfadan gelen diğer tüm içerik ler değişmezdir.

![Ana sayfa ve ilişkili içerik sayfası](master-pages/_static/image1.jpg)

**Şekil 1**: Ana sayfa ve ilişkili içerik sayfası

## <a name="creating-a-master-page"></a>Ana Sayfa Oluşturma

Yeni bir ana sayfa oluşturmak için:

1. Visual Studio 2005'i açın ve yeni bir Web sitesi oluşturun.
2. Dosya, Yeni, Dosya'yı tıklatın.
3. **Şekil 2'de**gösterildiği gibi Yeni Öğe Ekle iletişim kutusundan Ana Dosya'yı seçin.
4. Ekle’ye tıklayın.

![Yeni Bir Ana Sayfa Oluşturma](master-pages/_static/image2.jpg)

**Şekil 2**: Yeni Bir Ana Sayfa Oluşturma

Ana sayfanın dosya uzantısı *.master*olduğuna dikkat edin. Bu, ana sayfanın sıradan bir sayfadan farklı olduğu yollardan biridir. Diğer birincil fark, bir @Page yönerge yerine, ana sayfanın bir @Master yönerge içermesidir. Oluşturduğunuz ana sayfa için Kaynak Görünümü'ne geçin ve kodu gözden geçirin.

Yeni bir ana sayfada varsayılan olarak bir ContentPlaceHolder denetimi olacaktır. Çoğu durumda, önce ortak sayfa öğelerini oluşturmak ve ardından özel içeriğin istendiği yerlerde ContentPlaceHolder denetimlerini eklemek daha mantıklıdır. Bu gibi durumlarda, geliştiriciler varsayılan ContentPlaceHolder denetimini silmek ve sayfa geliştirildikçe yenilerini eklemek isteyecektir. ContentPlaceHolder denetimleri, boyutlandırma tutamaçlarını görüntülemelerine rağmen yeniden boyutlandırılamaz. ContentPlaceHolder denetimi, bir istisna dışında içerdiği içeriğe göre otomatik olarak boyutlandır; Bir ContentPlaceHolder denetimini tablo hücresi gibi bir blok öğesinin içine yerletirseniz, öğenin boyutuna göre boyutlandırılır.

## <a name="lab-1-working-with-master-pages"></a>Laboratuvar 1 Ana Sayfalarla Çalışma

Bu laboratuvarda, yeni bir ana sayfa oluşturacak ve üç ContentPlaceHolder denetimi tanımlayacaktır. Daha sonra yeni bir İçerik sayfası oluşturur ve ContentPlaceHolder denetimlerinden en az birinin içeriğini değiştirirsiniz.

1. Bir ana sayfa oluşturun ve ContentPlaceHolder denetimlerini ekleyin. 

    1. Yukarıda açıklandığı gibi yeni bir ana sayfa oluşturun.
    2. Varsayılan ContentPlaceHolder denetimini silin.
    3. Denetimin gölgeli üst kenarlığı tıklayarak ContentPlaceHolder denetimini seçin ve ardından klavyenizdeki DEL tuşuna basarak ssilin.
    4. Şekil 3'te gösterildiği gibi *Üstbilgi ve yan* şablonu kullanarak yeni bir tablo ekleyin. Tüm tablonun tasarımcıda görülebilmesi için genişlik ve yüksekliği %90'a değiştirin.

![](master-pages/_static/image3.jpg)

**Şekil 3**

1. İmleci tablonun her hücresine yerleştirin ve *valign* özelliğini *en üste*ayarlayın.
2. Araç kutusundan, tablonun üst hücresine (üstbilgi hücresi) Bir ContentPlaceHolder denetimi ekleyin.
3. Bu ContentPlaceHolder denetimini eklediğinizde, satır yüksekliğinin şekil 4'te gösterildiği gibi sayfanın neredeyse tamamını kapladığını fark edeceksiniz. Bu noktada bu konuda endişelenmeyin.

![Boş alan ContentPlaceHolder ile aynı hücrede](master-pages/_static/image1.gif)

**Şekil 4**: Boş alan ContentPlaceHolder ile aynı hücrede

1. Diğer iki hücreye ContentPlaceHolder denetimi yerleştirin. Diğer ContentPlaceHolder denetimleri eklendikten sonra, tablo hücrelerinin boyutu beklediğiniz gibi olmalıdır. Sayfa şimdi **şekil 5'te**gösterilen sayfa gibi görünmelidir.

![Tüm ContentPlaceHolder kontrolleriyle Master. Üstbilgi hücresi için hücre yüksekliğinin artık olması gereken şey olduğuna dikkat edin](master-pages/_static/image2.gif)

**Şekil 5**: Tüm ContentPlaceHolder kontrolleriyle Master. Üstbilgi hücresi için hücre yüksekliğinin artık olması gereken şey olduğuna dikkat edin

1. Üç ContentPlaceHolder denetiminin her birine seçtiğiniz bazı metinleri girin.
2. Ana sayfayı exercise1.master olarak kaydedin.
3. Yeni bir Web Formu oluşturun ve exercise1.master master sayfasıyla ilişkilendirin.
4. Visual Studio 2005'te Dosya, Yeni, Dosya'yı seçin.
5. Yeni Öğe Ekle iletişim kutusunda **Web Formu'nu** seçin.
6. Ana sayfayı seç onay kutusunun şekil 6'da gösterildiği gibi işaretli olduğundan emin olun.

![Yeni İçerik Sayfası Ekleme](master-pages/_static/image3.gif)

**Şekil 6**: Yeni İçerik Sayfası Ekleme

1. Ekle’ye tıklayın.
2. Şekil 7'de gösterildiği gibi bir ana sayfa seçin iletişim kutusunda exercise1.master'ı seçin.
3. Yeni içerik sayfasını eklemek için Tamam'ı tıklatın.

Yeni içerik sayfası Visual Studio'da ana sayfada her ContentPlaceHolder denetimi için tek bir İçerik denetimiyle görünür. Varsayılan olarak, kendi içeriğinizi ekleyebilmeniz için İçerik denetimleri boştur. Ana sayfada ContentPlaceHolder denetimindeki içeriği kullanmalarını istiyorsanız, akıllı etiket simgesine (denetimin sağ üst köşesindeki küçük siyah ok) tıklamanız ve **şekil 8'de**gösterildiği gibi akıllı etiketten *Varsayılan Olarak Masters İçeriği'ni* seçmeniz yeterlidir. Bunu yaptığınızda, menü öğesi *Özel İçerik Oluştur'a*dönüşür. Bu noktada tıklatmak, içeriği ana sayfadan kaldırarak belirli İçerik denetimi için özel içerik tanımlamanıza olanak sağlar.

![İçerik Denetimini Ana Sayfalar İçeriğinde Varsayılan Olarak Ayarlama](master-pages/_static/image4.gif)

**Şekil 7**: İçerik Denetimini Ana Sayfalar İçeriğinde Varsayılan Olarak Ayarlama

## <a name="connecting-master-page-and-content-pages"></a>Ana Sayfa ve İçerik Sayfalarını Bağlama

Ana sayfa ile içerik sayfası arasındaki ilişki dört farklı şekilde yapılandırılabilir:

- Yönergenin @Page <strong>MasterPageFile</strong> özelliği
- **Page.MasterPageFile** özelliğini kodolarak ayarlama.
- Uygulamalar yapılandırma dosyasındaki ** &lt;sayfa&gt; ** öğesi (uygulamanın kök klasöründe web.config)
- Alt klasörler yapılandırma dosyasındaki ** &lt;sayfa&gt; ** öğesi (bir alt klasördeki web.config)

## <a name="masterpagefile-attribute"></a>MasterPageFile Özniteliği

MasterPageFile özelliği, ana sayfanın belirli bir ASP.NET sayfasına uygulanmasını kolaylaştırır. Ayrıca, Alıştırma 1'de yaptığınız gibi Ana **Sayfayı Seç** onay kutusunu işaretlediğinizde ana sayfayı uygulamak için kullanılan yöntemdir.

## <a name="setting-pagemasterpagefile-in-code"></a>Page.MasterPageFile'ı Kodda Ayarlama

MasterPageFile özelliğini koda ayarlayarak, belirli bir ana sayfayı çalışma zamanında içeriğinize uygulayabilirsiniz. Bu, kullanıcı rolüne veya diğer bazı ölçütlere dayalı olarak belirli bir ana sayfa uygulamanız gerekebileceği durumlarda yararlıdır. MasterPageFile özelliği PreInit yönteminde ayarlanmalıdır. PreInit yönteminden sonra ayarlanırsa, Bir GeçersizİşlemÖzel Durum atılır. Bu özelliğin ayarlandığı sayfada, sayfanın üst düzey denetimi olarak İçerik denetimi de olmalıdır. Aksi takdirde MasterPageFile özelliği ayarlandığında bir HttpException atılır.

## <a name="using-the-ltpagesgt-element"></a>Öğe &lt;sayfalarını&gt; kullanma

Web.config dosyasının &lt;sayfa&gt; öğesinde masterPageFile özniteliğini ayarlayarak sayfalarınız için bir ana sayfa yapılandırabilirsiniz. Bu yöntemi kullanırken, uygulama yapısında daha düşük web.config dosyalarının bu ayarı geçersiz kılabilir unutmayın. Bir yönergede ayarlanan @Page herhangi bir MasterPageFile özniteliği de bu ayarı geçersiz kılar. Sayfalar&gt; &lt;öğesini kullanmak, belirli klasörlerde veya dosyalarda gerekirse geçersiz kılınabilecek bir *ana* sayfa oluşturmayı kolaylaştırır.

## <a name="properties-in-master-pages"></a>Ana Sayfalardaki Özellikler

Ana sayfa, yalnızca bu özellikleri ana sayfa içinde herkese açık hale getirerek özellikleri ortaya çıkarabilir. Örneğin, aşağıdaki kod SomeProperty adlı bir özelliği tanımlar:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

İçerik sayfasından SomeProperty özelliğine erişmek için Ana özelliği aşağıdaki gibi kullanmanız gerekir:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>İç Içe Ana Sayfalar

Ana sayfalar, büyük bir Web uygulamasında ortak bir görünüm ve his sağlamak için mükemmel bir çözümdür. Ancak, diğer parçalar farklı bir arabirimi paylaşırken büyük bir sitenin belirli bölümlerinin ortak bir arabirimi paylaşması nadir değildir. Bu ihtiyacı gidermek için, birden çok ana sayfa mükemmel bir çözümdür. Ancak, yine de büyük bir uygulamanın tüm sayfalar ve yalnızca sitenin belirli bölümleri arasında paylaşılan diğer bileşenler arasında paylaşılan belirli bileşenlere (örneğin menü gibi) sahip olabileceği gerçeğini ele almaz. Bu tür bir durum için, iç içe ana sayfalar güzel ihtiyacı doldurun. Gördüğünüz gibi, normal bir ana sayfa bir ana sayfa ve içerik sayfasından oluşur. İç içe ana sayfa durumunda iki ana sayfa vardır; bir ebeveyn üst ve bir çocuk ustası. Alt ana sayfa aynı zamanda bir içerik sayfasıdır ve ana sayfası ana sayfadır.

Tipik bir ana sayfanın kodu aşağıdaverilmiştir:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

İç içe geçen bir ana senaryoda, bu ana ana öğretici olacaktır. Başka bir ana sayfa bu sayfayı ana sayfa olarak kullanır ve bu kod şu na benzer:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Bu senaryoda, alt asıl aynı zamanda üst yöneticisi için bir içerik sayfası olduğunu unutmayın. Alt üst öğenin tüm içeriği, içeriğini üst ebeveynin ContentPlaceHolder denetiminden alan bir İçerik denetiminin içinde görünür.

> [!NOTE]
> İç içe ana sayfalar için tasarımcı desteği kullanılamaz. İç içe geçme ustaları kullanarak geliştirme yaparken, kaynak görünümünü kullanmanız gerekir.

Bu video, iç içe geçen ana sayfaları kullanma nın bir çıkış ını gösterir.

![](master-pages/_static/image1.png)

[Tam Ekran Video Aç](master-pages/_static/nested1.wmv)

![Ana Sayfa Seçme](master-pages/_static/image4.jpg)

**Şekil 8**: Ana Sayfa Seçme
