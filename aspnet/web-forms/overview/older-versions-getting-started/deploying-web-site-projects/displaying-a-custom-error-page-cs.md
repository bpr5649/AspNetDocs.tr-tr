---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: Özel hata sayfası görüntüleme (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET Web uygulamasında bir çalışma zamanı hatası oluştuğunda kullanıcı ne görür? Yanıt, Web sitesinin &lt; customErrors &gt; yapılandırmasına bağlıdır...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 777948732690443d63f1fb2afd6f72a33a496c44
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86211049"
---
# <a name="displaying-a-custom-error-page-c"></a>Özel Hata Sayfası Görüntüleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> ASP.NET Web uygulamasında bir çalışma zamanı hatası oluştuğunda kullanıcı ne görür? Yanıt, Web sitesinin &lt; customErrors &gt; yapılandırmasına bağlıdır. Varsayılan olarak, kullanıcılara bir çalışma zamanı hatası oluştuğunu gösteren unsightly sarı bir ekran görüntülenir. Bu öğreticide, sitenizin görünümü ile eşleşen bir aesthepepkiralama özel hata sayfasını göstermek üzere bu ayarların nasıl özelleştirileceği gösterilmektedir.

## <a name="introduction"></a>Giriş

Mükemmel bir dünyada, çalışma zamanı hataları olmayacaktır. Programcılar bir hata vererek ve güçlü Kullanıcı girişi doğrulaması ile kod yazar ve veritabanı sunucuları ile e-posta sunucuları gibi dış kaynaklar hiçbir şekilde çevrimdışı olmaz. Kuşkusuz, gerçeklik hataları ' nda kaçınılmaz. .NET Framework sınıflar bir özel durum oluşturarak hatayı işaret ediyor. Örneğin, bir SqlConnection nesnesinin Open metodunu çağırmak, bir bağlantı dizesi tarafından belirtilen veritabanına bir bağlantı oluşturur. Ancak, veritabanı kapalıysa veya bağlantı dizesindeki kimlik bilgileri geçersizse, Open yöntemi bir oluşturur `SqlException` . Özel durumlar blokların kullanımı tarafından işlenebilir `try/catch/finally` . Bir blok içindeki kod `try` bir özel durum oluşturursa, denetim, geliştiricinin hatadan kurtulmak için deneyebileceği uygun catch bloğuna aktarılır. Eşleşen bir catch bloğu yoksa veya özel durumu oluşturan kod bir try bloğunda değilse, özel durum blok aramasında çağrı yığınını uygular `try/catch/finally` .

Özel durum, işlenmeksizin ASP.NET çalışma zamanına kadar her şey için, [ `HttpApplication` sınıfın](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) [ `Error` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) tetiklenir ve yapılandırılan *hata sayfası* görüntülenir. Varsayılan olarak, ASP.NET, (ysod) [sarı ekranı](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) olarak adlandırılan affectionately bir hata sayfası görüntüler. Şu iki sürümü vardır: One özel durum ayrıntılarını, yığın izlemesini ve geliştiricilerin uygulamada hata ayıklamasına yardımcı olan diğer bilgileri gösterir (bkz. **Şekil 1**); diğeri de bir çalışma zamanı hatası olduğunu belirtir (bkz. **Şekil 2**).

Özel durum ayrıntıları, uygulamada hata ayıklamada geliştiriciler için oldukça yararlıdır, ancak son kullanıcıların da bir unsod 'yi göstermek çok daha fazla ve unuzman hale geldı. Bunun yerine, son kullanıcılar, durumu açıklayan daha kolay bir şekilde sitenin görünümünü tutan bir hata sayfasına alınmalıdır. İyi haber, böyle bir özel hata sayfasının oluşturulması oldukça kolaydır. Bu öğretici, ASP. NET ' in farklı hata sayfaları. Daha sonra, bir hata durumunda kullanıcılara özel hata sayfası göstermek için Web uygulamasının nasıl yapılandırılacağını gösterir.

### <a name="examining-the-three-types-of-error-pages"></a>Üç tür hata sayfasını İnceleme

Bir ASP.NET uygulamasında işlenmeyen bir özel durum ortaya çıkarsa, üç hata sayfası türünden biri görüntülenir:

- Özel durum ayrıntıları sarı ölüm hata sayfası
- Çalışma zamanı hatası sarı ölüm hata sayfası veya
- Özel hata sayfası

Hata sayfası geliştiricileri, en çok tanıdık özel durum ayrıntılardır. Bu sayfa, varsayılan olarak, yerel olarak ziyaret edilen kullanıcılara görüntülenir ve bu nedenle, siteyi geliştirme ortamında sınarken bir hata oluştuğunda gördüğünüz sayfasıdır. Adından da anlaşılacağı gibi, özel durum ayrıntıları, tür, ileti ve yığın izleme hakkında ayrıntılı bilgi sağlar. Daha fazlası, özel durum ASP.NET sayfanızın arka plan kod sınıfında kodu tarafından oluşturulmuşsa ve uygulama hata ayıklama için yapılandırıldıysa, özel durum ayrıntıları da bu kod satırını (ve üzerinde ve altında birkaç satır kod satırı) gösterir.

**Şekil 1** ' de özel durum ayrıntıları gösterilmektedir. Tarayıcının adres penceresindeki URL 'YI aklınızda edin: `http://localhost:62275/Genre.aspx?ID=foo` . `Genre.aspx`Sayfanın belirli bir tarz kitap incelemelerini listelediği hatırlayın. `GenreId`Değerin (a `uniqueidentifier` ) QueryString aracılığıyla geçirilmesini gerektirir; Örneğin, kurgu incelemelerini görüntülemek IÇIN uygun URL olur `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146` . Değer olmayan bir `uniqueidentifier` sorgu dizesi aracılığıyla ("foo" gibi) geçirilirse bir özel durum oluşturulur.

> [!NOTE]
> Bu hatayı indirmek üzere kullanılabilen demo Web uygulamasında yeniden oluşturmak için doğrudan ziyaret edebilir `Genre.aspx?ID=foo` veya ' de "çalışma zamanı hatası oluştur" bağlantısına tıklayabilirsiniz `Default.aspx` .

**Şekil 1**' de sunulan özel durum bilgilerini aklınızda edin. "Bir karakter dizesinden uniqueidentifier değerine dönüştürülürken dönüştürme başarısız oldu" özel durum iletisi sayfanın en üstünde bulunur. Özel durumun türü `System.Data.SqlClient.SqlException` de listelenir. Yığın izlemesi de vardır.

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**Şekil 1**: özel durum ayrıntıları YSOD özel durum hakkında bilgi içerir  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](displaying-a-custom-error-page-cs/_static/image3.png))

Diğer YSOD türü, çalışma zamanı hatası yıldır ve **Şekil 2**' de gösterilir. Çalışma zamanı hatası, ziyaretçiye bir çalışma zamanı hatası oluştuğunu bildirir, ancak oluşturulan özel durumla ilgili herhangi bir bilgi içermez. (Ancak, bu, bu `Web.config` tür BIR YSOD görünümünü bir parçası olan dosyayı değiştirerek hata ayrıntılarının nasıl görünebileceği hakkında yönergeler sağlar.)

Varsayılan olarak, çalışma zamanı hatası YSOD, uzaktan ziyaret eden kullanıcılar için ( http://www.yoursite.com) **Şekil 2**' de TARAYıCıNıN adres çubuğundaki URL tarafından göz atma olarak) gösterilir: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo` . Geliştiriciler hata ayrıntılarını öğrenmekte olduğundan iki farklı YSOD ekranı mevcuttur, ancak bu tür bilgiler, sitenizi ziyaret eden herkese yönelik olası güvenlik açıklarını veya diğer hassas bilgileri açığa çıkarabileceğinden canlı bir sitede gösterilmemelidir.

> [!NOTE]
> ' İ de ve Web ana bilgisayarınız olarak DiscountASP.NET kullanıyorsanız, çalışma zamanı hatası ile canlı siteyi ziyaret ederken görüntülemediğine dikkat edebilirsiniz. Bunun nedeni, DiscountASP.NET 'in sunucularının varsayılan olarak özel durum ayrıntılarını gösterecek şekilde yapılandırılmalarından kaynaklanır. İyi haberler, dosyanıza bir bölüm ekleyerek bu varsayılan davranışı geçersiz kıkılabileceğiniz yerdir `<customErrors>` `Web.config` . "Hangi hata sayfasının görüntülendiğini yapılandırma" bölümü, `<customErrors>` bölümü ayrıntılı olarak inceler.

[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**Şekil 2**: çalışma zamanı hatası YSOD herhangi bir hata ayrıntısı içermiyor  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](displaying-a-custom-error-page-cs/_static/image6.png))

Üçüncü hata türü sayfası, oluşturduğunuz bir Web sayfası olan özel hata sayfasıdır. Özel hata sayfasının avantajı, kullanıcının sayfanın görünümü ve hisde yanında görüntülenen bilgiler üzerinde tamamen denetim sahibi olmanız durumunda; özel hata sayfası, diğer sayfalarınız ile aynı ana sayfayı ve stilleri kullanabilir. "Özel hata sayfası kullanma" bölümünde özel bir hata sayfası oluşturma ve işlenmemiş bir özel durum durumunda görüntülenecek şekilde yapılandırma gösterilmektedir. **Şekil 3** ' te bu özel hata sayfasının gizli bir üst sürümü sunulmaktadır. Gördüğünüz gibi, hata sayfasının görünümü, Şekil 1 ve 2 ' de gösterilen sarı ekranlarından birinden çok daha profesyonel bir şekilde görünür.

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**Şekil 3**: özel bir hata sayfası daha uyarlanmış bir görünüm sağlar  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](displaying-a-custom-error-page-cs/_static/image9.png))

**Şekil 3**' te tarayıcının adres çubuğunu incelemek için bir dakikanızı ayırın. Adres çubuğunun özel hata sayfasının () URL 'sini gösterdiğini unutmayın `/ErrorPages/Oops.aspx` . Şekil 1 ve 2 ' de, ölüm 'nin sarı ekranları, hatanın kaynaklandığı sayfada ( `Genre.aspx` ) gösterilir. Özel hata sayfası, hata QueryString parametresi aracılığıyla Hatanın gerçekleştiği sayfanın URL 'sini geçti `aspxerrorpath` .

## <a name="configuring-which-error-page-is-displayed"></a>Hangi hata sayfasının görüntülendiğini yapılandırma

Olası üç hata sayfası görüntülendiğinde iki değişken temel alınarak belirlenir:

- Bölümündeki yapılandırma bilgileri `<customErrors>` ve
- Kullanıcının siteyi yerel olarak veya uzaktan ziyaret edip etmediğini belirtir.

İçindeki [ `<customErrors>` bölümünde](https://msdn.microsoft.com/library/h0hfz6fc.aspx) , `Web.config` hangi hata sayfasının gösterildiğini etkileyen iki özniteliği vardır: `defaultRedirect` ve `mode` . `defaultRedirect`Özniteliği isteğe bağlıdır. Sağlanmışsa, özel hata sayfasının URL 'sini belirtir ve çalışma zamanı hatası olarak özel hata sayfasının gösterilip gösterilmeyeceğini belirtir. `mode`Özniteliği zorunludur ve üç değerden birini kabul eder: `On` , `Off` , veya `RemoteOnly` . Bu değerler aşağıdaki davranışa sahiptir:

- `On`-özel hata sayfası veya çalışma zamanı hatası, yerel veya uzak olmalarından bağımsız olarak tüm ziyaretçilere gösterildiğini gösterir.
- `Off`-Özel durum ayrıntılarının, yerel veya uzak olup olmadığına bakılmaksızın tüm ziyaretçilere görüntülendiğini belirtir.
- `RemoteOnly`-özel hata sayfası veya çalışma zamanı hatası YSOD 'nin uzak ziyaretçilere gösterildiğini, ancak özel durum ayrıntıları, yerel ziyaretçilere gösterildiğini gösterir.

Aksi belirtilmedikçe, ASP.NET mode özniteliğini ayarlamış `RemoteOnly` ve bir değer belirtmediğiniz gibi davranır `defaultRedirect` . Diğer bir deyişle, varsayılan davranış, özel durum ayrıntılarının, uzak ziyaretçilere çalışma zamanı hatası gösterilirken yerel ziyaretçilere görüntülenmelerdir. Web uygulamanıza bir bölüm ekleyerek bu varsayılan davranışı geçersiz kılabilirsiniz `<customErrors>``Web.config file.`

## <a name="using-a-custom-error-page"></a>Özel hata sayfası kullanma

Her Web uygulamasının özel bir hata sayfası olmalıdır. Çalışma zamanı hatasına daha profesyonel bir alternatif sağlar, daha kolay bir şekilde oluşturulabilir ve uygulamanın özel hata sayfasını kullanmak üzere yapılandırılması, yalnızca birkaç dakika sürer. İlk adım özel hata sayfasını oluşturuyor. Adlı kitap Incelemeleri uygulamasına yeni bir klasör ekledim `ErrorPages` ve adlı yeni bir ASP.NET sayfasına ekledi `Oops.aspx` . Sayfanın, sitenizdeki geri kalan sayfalarla aynı ana sayfayı kullanmasını sağlamak için, aynı görünümü otomatik olarak devramını sağlayabilirsiniz.

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**Şekil 4**: özel hata sayfası oluşturma

Sonra, hata sayfası için içerik oluşturma birkaç dakika harcaın. Beklenmeyen bir hata olduğunu ve sitenin giriş sayfasına geri bir bağlantı olduğunu belirten bir ileti içeren basit bir özel hata sayfası oluşturduğdum.

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**Şekil 5**: özel hata sayfanızı tasarlama  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](displaying-a-custom-error-page-cs/_static/image14.png))

Hata sayfası tamamlandığında, Web uygulamasını özel hata sayfasını kullanmak için çalışma zamanı hatası ' nın yerine kullanın. Bu, bölümün özniteliğinde hata sayfasının URL 'SI belirtilerek gerçekleştirilir `<customErrors>` `defaultRedirect` . Aşağıdaki biçimlendirmeyi uygulamanızın `Web.config` dosyasına ekleyin:

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

Yukarıdaki biçimlendirme, uygulamayı yerel olarak ziyaret eden kullanıcılar için özel hata sayfasını kullanırken, uzaktan ziyaret eden kullanıcılar için özel hata sayfası olan özel durum ayrıntılarını göstermek üzere uygulamayı yapılandırır. Bunu işlem içinde görmek için Web sitenizi üretim ortamına dağıtın ve ardından canlı sitedeki tarz. aspx sayfasını geçersiz bir QueryString değeri ile ziyaret edin. Özel hata sayfasını görmeniz gerekir (bkz. **Şekil 3**' e geri bakın).

Özel hata sayfasının yalnızca uzak kullanıcılara gösterildiğini doğrulamak için, `Genre.aspx` geliştirme ortamından geçersiz bir QueryString içeren sayfayı ziyaret edin. Hala özel durum ayrıntılarını görmeniz gerekir (bkz. **Şekil 1**' e geri başvurabilirsiniz). `RemoteOnly`Bu ayar, üretim ortamındaki siteyi ziyaret eden kullanıcıların özel hata sayfasını görmesini sağlarken geliştiriciler yerel olarak çalışır ve özel durum ayrıntılarını görmeye devam eder.

## <a name="notifying-developers-and-logging-error-details"></a>Geliştiricilere ve günlüğe kaydetme hata ayrıntılarına bildirme

Geliştirme ortamında oluşan hatalar, geliştiricinin bilgisayarında oturmuş olması nedeniyle oluşur. Özel durum ayrıntılarında özel durumun bilgileri gösterilir ve hata oluştuğunda hangi adımların gerçekleştiğini bilir. Ancak üretimde bir hata oluştuğunda, siteyi ziyaret eden Son Kullanıcı hatayı raporlamak için zaman alacağından, geliştirici bir hata meydana geldi bilgisine sahip değildir. Ayrıca, Kullanıcı geliştirme ekibine bir hata oluştuğunu uyarma, özel durum türü, ileti ve yığın izlemesini bilmeden hatanın nedenini tanılamak zor olabilir ve tek başına düzelme olanağı sağlar.

Bu nedenlerden dolayı, üretim ortamındaki herhangi bir hata, kalıcı bir depoya (örneğin, bir veritabanı) kaydedilir ve geliştiricilerin bu hata ile ilgili uyarı almış olması halinde işlenir. Özel hata sayfası, bu günlüğe kaydetme ve bildirim yapmak için iyi bir yer olabilir. Ne yazık ki özel hata sayfasının hata ayrıntılarına erişimi yok ve bu nedenle bu bilgileri günlüğe kaydetmek için kullanılamaz. İyi haber, hata ayrıntılarını kesmeye ve bunları günlüğe girmeye yönelik çeşitli yollar ve sonraki üç öğreticinin bu konuyu daha ayrıntılı bir şekilde araştırmasına olanak sağlar.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>Farklı HTTP hata durumları için farklı özel hata sayfaları kullanma

Bir ASP.NET sayfası tarafından bir özel durum oluşturulduğunda ve işlenmezse, özel durum, yapılandırılan hata sayfasını görüntüleyen ASP.NET çalışma zamanına kadar çalışır. Bir istek ASP.NET altyapısına gelirse ancak bazı nedenlerle işlenemezse, istenen dosya bulunamadı veya dosya için okuma izinleri devre dışı bırakılmış olabilir; ASP.NET altyapısı bir oluşturur `HttpException` . Bu özel durum, ASP.NET sayfalarından çıkarılan özel durumlar, çalışma zamanına kadar kabarcıklar ve uygun hata sayfasının görüntülenmesine neden olur.

Bu, üretimde Web uygulaması için ne anlama geldiğini, kullanıcının bulunamayan bir sayfayı istemesi durumunda özel hata sayfasını görebileceklerini belirtir. **Şekil 6** ' da böyle bir örnek gösterilmektedir. İstek var olmayan bir sayfa () için olduğundan `NoSuchPage.aspx` , bir oluşturulur `HttpException` ve özel hata sayfası görüntülenir (QueryString parametresindeki başvuruya göz atılır `NoSuchPage.aspx` `aspxerrorpath` ).

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**Şekil 6**: ASP.NET çalışma zamanı, geçersiz bir Isteğe yanıt olarak yapılandırılmış hata sayfasını görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-custom-error-page-cs/_static/image17.png))

Varsayılan olarak, tüm hata türleri aynı özel hata sayfasının görüntülenmesine neden olur. Ancak, bölümünde alt öğeleri kullanarak belirli bir HTTP durum kodu için farklı bir özel hata sayfası belirtebilirsiniz `<error>` `<customErrors>` . Örneğin, 404 HTTP durum koduna sahip olan sayfa bulunamadı hatası durumunda farklı bir hata sayfası görüntülenmesi için, `<customErrors>` Bu bölümü aşağıdaki biçimlendirmeyi içerecek şekilde güncelleştirin:

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

Bu değişiklik varken, her ziyaret eden bir Kullanıcı, var olmayan bir ASP.NET kaynağını istediğinde, `404.aspx` yerine özel hata sayfasına yönlendirilir `Oops.aspx` . **Şekil 7** ' de gösterildiği gibi, `404.aspx` sayfa genel özel hata sayfasından daha belirli bir ileti içerebilir.

> [!NOTE]
> 404 hata sayfasına göz atın ve etkili 404 hata sayfaları oluşturma konusunda yönergeler için [bir kez daha](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) .

[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)

**Şekil 7**: özel 404 hata sayfasında daha fazla hedefli bir ileti görüntülenir`Oops.aspx`  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](displaying-a-custom-error-page-cs/_static/image20.png)) 

`404.aspx`Yalnızca Kullanıcı, bulunamayan bir sayfa için istek yaptığında sayfaya ulaşılmadığını bildiğiniz için, bu özel hata sayfasını, kullanıcının bu özel hata türünü ele almanıza yardımcı olacak işlevselliği içerecek şekilde geliştirebilirsiniz. Örneğin, bilinen hatalı URL 'Leri iyi URL 'Ler ile eşleyen bir veritabanı tablosu oluşturabilir ve ardından `404.aspx` özel hata sayfasının bu tabloda bir sorgu çalıştırmasını ve kullanıcının ulaşmaya çalıştığı sayfaları önermesini sağlayabilirsiniz.

> [!NOTE]
> Özel hata sayfası yalnızca, ASP.NET altyapısı tarafından işlenen bir kaynağa bir istek yapıldığında görüntülenir. [IIS ile ASP.NET geliştirme sunucusu öğreticisi arasındaki temel farklılıklar](core-differences-between-iis-and-the-asp-net-development-server-cs.md) konusunda anlatıldığı gibi, Web sunucusu belirli isteklerin kendisini işleyebilir. Varsayılan olarak, IIS Web sunucusu, ASP.NET altyapısını çağırmadan görüntüler ve HTML dosyaları gibi statik içerik isteklerini işler. Sonuç olarak, Kullanıcı var olmayan bir görüntü dosyası isterse ASP yerine IIS 'nin varsayılan 404 hata iletisini geri alır. AĞ tarafından yapılandırılan hata sayfası.

## <a name="summary"></a>Özet

Bir ASP.NET uygulamasında işlenmeyen bir özel durum oluştuğunda, Kullanıcı üç hata sayfasında gösterilir: özel durum ayrıntıları sarı ekran ölüm ekranı; Çalışma zamanı hatası sarı ekran ölüm ekranı; veya özel bir hata sayfası. Hangi hata sayfası görüntülendiği, uygulamanın `<customErrors>` yapılandırmasına ve kullanıcının yerel olarak veya uzaktan ziyaret edilip edilmeyeceğini bağlıdır. Varsayılan davranış, yerel ziyaretçilere özel durum ayrıntıları ve uzak ziyaretçilere çalışma zamanı hatası gösterir.

Çalışma zamanı hatası YSOD, siteyi ziyaret eden kullanıcının potansiyel olarak gizli hata bilgilerini gizlediğini de, sitenizin görünüm ve kullanım alanını keser ve uygulamanızın hata halinde görünmesini sağlar. Özel hata sayfasının oluşturulmasını ve tasarlanmasını ve bölümün özniteliğinde URL 'sini belirtmesini gerektiren özel bir hata sayfası kullanmak daha iyi bir yaklaşımdır `<customErrors>` `defaultRedirect` . Farklı HTTP hata durumları için birden çok özel hata sayfasına da sahip olabilirsiniz.

Özel hata sayfası, üretimde bir Web sitesi için kapsamlı bir hata işleme stratejisindeki ilk adımdır. Hatanın geliştiricisini uyarma ve ayrıntılarını günlüğe kaydetme de önemli adımlardır. Sonraki üç öğretici hata bildirimi ve günlüğe kaydetme tekniklerini keşfedebilir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Hata sayfaları, bir kez daha](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [Özel Durumlar için Tasarım Yönergeleri](https://msdn.microsoft.com/library/ms229014.aspx)
- [Kullanıcı dostu hata sayfaları](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Özel durumları işleme ve atma](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [ASP.NET 'de özel hata sayfalarını kullanarak düzgün şekilde](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)
- [ASP.NET İzlemeye Genel Bakış](/previous-versions/aspnet/bb386420(v%3Dvs.100))

> [!div class="step-by-step"]
> [Önceki](strategies-for-database-development-and-deployment-cs.md) 
>  [Sonraki](processing-unhandled-exceptions-cs.md)
