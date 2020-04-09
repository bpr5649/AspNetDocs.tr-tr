---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 ve Visual Studio 2012 Yenilikler | Microsoft Dokümanlar
author: rick-anderson
description: Bu belge, ASP.NET 4.5'te tanıtılan yeni özellikleri ve geliştirmeleri açıklar. Ayrıca web geliştirme için yapılan iyileştirmeler açıklar ...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676288"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 ve Visual Studio 2012’deki Yenilikler

> Bu belge, ASP.NET 4.5'te tanıtılan yeni özellikleri ve geliştirmeleri açıklar. Ayrıca Visual Studio 2012'de web geliştirme için yapılan iyileştirmeleri de açıklar. Bu belge ilk olarak 29 Şubat 2012 tarihinde yayımlanmış.

- [ASP.NET Çekirdek Çalışma Süresi ve Çerçevesi](#_Toc318097372)

    - [Http İstek leri ve Yanıtları Eş senkronize Okuma ve Yazma](#_Toc318097373)
    - [HttpRequest işleme için iyileştirmeler](#_Toc318097374)
    - [Bir yanıtı eş senkronize olarak yıkama](#_Toc318097375)
    - [*Bekleme* ve *Görev*Tabanlı Asenkron Modüller ve İşleyiciler için destek](#_Toc318097376)
    - [Asynchronous HTTP modülleri](#_Toc318097377)
    - [Asynchronous HTTP işleyicileri](#_Toc318097378)
    - [Yeni ASP.NET İstek Doğrulama Özellikleri](#_Toc318097379)
    - [Ertelenmiş ("tembel") istek doğrulama](#_Toc318097380)
    - [Geçersiz kılınmamış istekler için destek](#_Toc318097381)
    - [AntiXSS Kütüphanesi](#_Toc318097382)
    - [WebSockets Protokolü desteği](#_Toc318097383)
    - [Paketleme ve Küçültme](#_Toc318097384)
    - [Web Hosting için Performans Geliştirmeleri](#_Toc_perf)

        - [Temel Performans Faktörleri](#_Toc_perf_1)
        - [Yeni Performans Özellikleri Için Gereksinimler](#_Toc_perf_2)
        - [Ortak Derlemeleri Paylaşma](#_Toc_perf_3)
        - [Daha hızlı başlatma için çok Çekirdekli JIT derlemesi kullanma](#_Toc_perf_4)
        - [Bellek için en iyi duruma getirmek için çöp toplama yı](#_Toc_perf_5)
        - [Web uygulamaları için ön alma](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [Kesin Türü Belirtilmiş Veri Denetimleri](#_Toc318097386)
    - [Model Bağlama](#_Toc318097387)

        - [Veri seçme](#_Toc318097388)
        - [Değer sağlayıcılar](#_Toc318097389)
        - [Denetimden gelen değerlere göre filtreleme](#_Toc318097390)
    - [HTML Kodlanmış Veri Bağlama İfadeleri](#_Toc318097391)
    - [Göze çarpmadan doğrulama](#_Toc318097392)
    - [HTML5 Güncellemeleri](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web Sayfaları 2](#_Toc318097395)
- [Visual Studio 2012 Yayın Adayı](#_Toc318097396)

    - [Visual Studio 2010 ve Visual Studio 2012 Sürüm Adayı Arasında Proje Paylaşımı (Proje Uyumluluğu)](#project-compatibility)
    - [ASP.NET 4.5 Web Sitesi Şablonlarında Yapılandırma Değişiklikleri](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [ASP.NET Yönlendirme için IIS 7'de Yerel Destek](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML Düzenleyicisi](#_Toc318097397)

        - [Akıllı Görevler](#_Toc318097398)
        - [WAI-ARIA desteği](#_Toc318097399)
        - [Yeni HTML5 parçacıkları](#_Toc318097400)
        - [Kullanıcı denetimine ayıklama](#_Toc318097401)
        - [Öznitelikleri kod külçeleri için IntelliSense](#_Toc318097402)
        - [Açılış veya kapanış etiketini yeniden adlandırdığınızda eşleşen etiketin otomatik olarak yeniden adlandırılması](#_Toc318097403)
        - [Olay işleyicisi oluşturma](#_Toc318097404)
        - [Akıllı girintin](#_Toc318097405)
        - [İfade tamamlamayı otomatik küçültme](#_Toc318097406)
    - [JavaScript Düzenleyicisi](#_Toc318097407)

        - [Kod anahat](#_Toc318097408)
        - [Ayraç eşleştirme](#_Toc318097409)
        - [Tanıma Git](#_Toc318097410)
        - [ECMAScript5 desteği](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC imzası aşırı yükler](#_Toc318097413)
        - [Örtük referanslar](#_Toc318097414)
    - [CSS Editörü](#_Toc318097415)

        - [İfade tamamlamayı otomatik küçültme](#_Toc318097416)
        - [Hiyerarşik girintisi.](#_Toc318097417)
        - [CSS kesmek desteği](#_Toc318097418)
        - [Satıcıya özgü şemalar (-moz-,-webkit)](#_Toc318097419)
        - [Yorumlama ve yorumsuz destek](#_Toc318097420)
        - [Renk seçici](#_Toc318097421)
        - [Kod Parçacıkları](#_Toc318097422)
        - [Özel bölgeler](#_Toc318097423)
    - [Sayfa Denetçisi](#_Toc318097424)
    - [Yayımlama](#_Toc318097425)

        - [Yayımlama profilleri](#_Toc318097426)
        - [ASP.NET derleme ve birleştirme](#_Toc318097427)
- [IIS Ekspresi](#_Toc318097428)
- [Disclaimer](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Çekirdek Çalışma Süresi ve Çerçevesi

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>Http İstek leri ve Yanıtları Eş senkronize Okuma ve Yazma

ASP.NET *4, HttpRequest.GetBufferlessInputStream* yöntemini kullanarak bir HTTP istek varlığını akış olarak okuma olanağını tanıttı. Bu yöntem, istek varlığına akış erişimi sağladı. Ancak, bir istek süresi için bir iş parçacığı bağlı eşzamanlı olarak yürütülür.

ASP.NET 4.5, bir HTTP istek varlığında akışları eşit olarak okuma ve eşzamanlı olarak floş yapma yeteneğini destekler. ASP.NET 4.5 ayrıca ,aspx sayfa işleyicileri ve ASP.NET MVC denetleyicileri gibi downstream HTTP işleyicileri ile daha kolay entegrasyon sağlayan bir HTTP istek varlığını çift arabelleğe alma olanağı sağlar.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest işleme için iyileştirmeler

*HttpRequest.GetBufferlessInputStream'den* 4,5 ASP.NET döndürülen Akış başvurusu hem senkron hem de eşzamanlı okuma yöntemlerini destekler. *GetBufferlessInputStream'den* döndürülen *Akış* nesnesi artık Hem BeginRead hem de EndRead yöntemlerini uygular. Eşzamanlı *Akış* yöntemleri, istek varlığını parçalar halinde eşit olarak okumanızı sağlarken, ASP.NET asynchronous okuma döngüsünün her yinelemesi arasındaki geçerli iş parçacığı serbest bırakır.

ASP.NET 4.5 ayrıca arabelleğe getirilmiş bir şekilde istek varlığını okumak için bir eşlik eden yöntem ekledi: *HttpRequest.GetBufferedInputStream*. Bu yeni aşırı yükleme *GetBufferlessInputStream*gibi çalışır , hem senkron ve asynchronous destekleyen okur. Ancak, okuduğu gibi, *GetBufferedInputStream* ayrıca alt akış modülleri ve işleyicileri hala istek varlık erişebilirsiniz böylece ASP.NET iç arabellekleri içine varlık bayt kopyalar. Örneğin, ardışık düzendeki bazı akış yukarı kodlar *GetBufferedInputStream*kullanarak istek varlığını zaten okuduysa, Yine de *HttpRequest.Form* veya *HttpRequest.Files'ı*kullanabilirsiniz. Bu, bir istek üzerinde eşzamanlı işlem gerçekleştirmenize (örneğin, büyük bir dosya yüklemesini veritabanına aktarma), ancak daha sonra .aspx sayfaları ve MVC ASP.NET denetleyicilerini çalıştırmanıza olanak tanır.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Bir yanıtı eş senkronize olarak yıkama

Bir HTTP istemcisine yanıt göndermek, istemci uzaktayken veya düşük bant genişliğine sahipolduğunda önemli ölçüde zaman alabilir. Normalde ASP.NET, yanıt baytlarını bir uygulama tarafından oluşturulduğu için arabellekte aralar. ASP.NET sonra, istek işlemeişleminin sonunda tahakkuk eden arabelleklerin tek bir gönderme işlemini gerçekleştirir.

Arabelleğe alan yanıt büyükse (örneğin, büyük bir dosyayı istemciye aktarmak), arabelleğe alan çıktıyı istemciye göndermek ve bellek kullanımını kontrol altında tutmak için düzenli olarak *HttpResponse.Flush'ı* aramanız gerekir. Ancak, *Flush* eşzamanlı bir çağrı olduğundan, yinelemeli olarak *Flush* arama hala potansiyel olarak uzun süren istekleri süresince bir iş parçacığı tüketir.

ASP.NET 4.5, *HttpResponse* sınıfının *BeginFlush* ve *EndFlush* yöntemlerini kullanarak floşları eşit bir şekilde gerçekleştirmek için destek ekler. Bu yöntemleri kullanarak, işletim sistemi iş parçacıklarını bağlamadan istemciye artımlı olarak veri gönderen eşzamanlı modüller ve eş zamanlı işleyiciler oluşturabilirsiniz. *BeginFlush* ve *EndFlush* aramaları arasında, ASP.NET geçerli iş parçacığı bültenleri. Bu, uzun süreli HTTP indirmelerini desteklemek için gereken toplam etkin iş parçacığı sayısını önemli ölçüde azaltır.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*Bekleme* ve *Görev* Desteği - Tabanlı Asynchronous Modülleri ve İşleyicileri

.NET Framework *4, görev*olarak adlandırılan eşzamanlı programlama kavramını tanıttı. Görevler, *System.Threading.Tasks* ad alanında *Görev* türü ve ilgili türleri ile temsil edilir. .NET Framework 4.5, *Görev* nesneleriyle çalışmayı basit hale getiren derleyici geliştirmeleriyle bunun üzerine inşa eder. .NET Framework 4.5'te derleyiciler iki yeni anahtar kelimeyi destekler: *bekleme* ve *async.* *Bekleyen* anahtar sözcük, bir kod parçasının eşzamanlı olarak başka bir kod parçasıüzerinde beklemesi gerektiğini belirtmek için sözdizimsel kısaltmadır. *Async* anahtar sözcüğü, yöntemleri görev tabanlı eşzamanlı yöntemler olarak işaretlemek için kullanabileceğiniz bir ipucunu temsil eder.

*Bekleme*, *async*ve *Görev* nesnesinin birleşimi .NET 4.5'e eşzamanlı kod yazmanızı çok daha kolay hale getirir. ASP.NET 4.5, yeni derleyici geliştirmelerini kullanarak eşzamanlı HTTP modülleri ve eşzamanlı HTTP işleyicileri yazmanıza izin veren yeni API'lerle bu basitleştirmeleri destekler.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Asynchronous HTTP modülleri

*Görev* nesnesini döndüren bir yöntem içinde eşenkron çalışma gerçekleştirmek istediğinizi varsayalım. Aşağıdaki kod örneği, Microsoft ana sayfasını indirmek için eşzamanlı arama yapan bir eşzamanlı yöntem tanımlar. Yöntem imzasında *async* anahtar kelimesinin kullanımına dikkat edin ve *DownloadStringTaskAsync*için *bekleyen* arama .

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

Yazmanız gereken tek şey bu - .NET Framework, indirmenin tamamlanmasını beklerken arama yığınını otomatik olarak gevşetmeyi ve indirme işlemi tamamlandıktan sonra arama yığınını otomatik olarak geri yüklemeyi ele alacaktır.

Şimdi bu eşzamanlı yöntemi bir asynchronous ASP.NET HTTP modülünde kullanmak istediğinizi varsayalım. ASP.NET 4.5, ASP.NET HTTP ardışık alt üst hattı tarafından açığa çıkarılan eski asynchronous programlama modeliyle görev tabanlı eşzamanlı yöntemleri tümleştirmek için kullanabileceğiniz bir yardımcı yöntem *(EventHandlerSyncHelper)* ve yeni bir temsilci türü *(TaskEventHandler)* içerir. Bu örnek, şunları gösterir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Asynchronous HTTP işleyicileri

ASP.NET asynchronous işleyicileri yazma geleneksel yaklaşım *IHttpAsyncHandler* arabirimini uygulamaktır. ASP.NET 4.5, elde edebilirsiniz *HttpTaskAsyncHandler* asynchronous baz türü tanıttı, hangi çok daha kolay asynchronous işleyicileri yazmak için yapar.

*HttpTaskAsyncHandler* türü soyuttur ve *ProcessRequestAsync* yöntemini geçersiz kılmanızı gerektirir. Dahili olarak ASP.NET, *ProcessRequestAsync'in* ASP.NET ardışık ardışık ardışık tarafından kullanılan eski eşzamanlı programlama modeliyle iade imzasını *(Görev* nesnesi) tümleştirmeyi halleder.

Aşağıdaki örnek, *Görev'i* nasıl kullanabileceğinizi ve eşzamanlı bir HTTP işleyicisinin uygulanmasının bir parçası olarak *nasıl bekleyeceğinizi* gösterir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Yeni ASP.NET İstek Doğrulama Özellikleri

Varsayılan olarak, ASP.NET istek doğrulamagerçekleştirir - bu alanlarda işaretleme veya komut dosyası aramak için istekleri inceler, üstbilgi, çerezleri, ve benzeri. Varsa, ASP.NET bir özel durum atar. Bu, olası site ler arası komut dosyası saldırılarına karşı ilk savunma hattı görevi görür.

ASP.NET 4.5, geçersiz istek verilerini seçikolarak okumayı kolaylaştırır. ASP.NET 4.5 aynı zamanda eskiden harici bir kütüphane olan popüler AntiXSS kütüphanesini de entegre eder.

Geliştiriciler sık sık uygulamaları için istek doğrulamasını seçikez kapatma olanağı nı istediler. Örneğin, uygulamanız forum yazılımıysa, kullanıcıların HTML biçimli forum gönderilerini ve yorumlarını göndermesine izin vermek, ancak yine de istek doğrulamanın diğer her şeyi kontrol ettiğinden emin olmak isteyebilirsiniz.

ASP.NET 4.5, geçersiz kılınmamış girişle seçici olarak çalışmanızı kolaylaştıran iki özellik sunar: ertelenmiş ("tembel") istek doğrulama ve geçersiz istek verilerine erişim.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Ertelenmiş ("tembel") istek doğrulama

4,5 ASP.NET, varsayılan olarak tüm istek verileri istek doğrulamasına tabidir. Ancak, isteği verilerine gerçekten erişene kadar isteği doğrulamayı ertelemek için uygulamayı yapılandırabilirsiniz. (Bu bazen belirli veri senaryoları için tembel yükleme gibi terimlere dayalı tembel istek doğrulama olarak adlandırılır.) Aşağıdaki örnekte olduğu gibi, *httpRUntime* öğesinde *requestValidationMode* özniteliğini 4,5 olarak ayarlayarak uygulamayı Web.config dosyasında ertelenmiş doğrulama kullanacak şekilde yapılandırabilirsiniz:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

İstek doğrulama modu 4,5 olarak ayarlandığında, istek doğrulaması yalnızca belirli bir istek değeri için ve yalnızca kodunuz bu değere eriştiğinde tetiklenir. Örneğin, kodunuz Request.Form["forum\_post"]değerini alırsa, yalnızca form koleksiyonundaki öğe için istek doğrulaması çağrılır. *Form* koleksiyonundaki diğer öğelerin hiçbiri doğrulanmadı. ASP.NET önceki sürümlerinde, koleksiyondaki herhangi bir öğeye erişildiğinde tüm istek koleksiyonu için istek doğrulaması tetiklendi. Yeni davranış, farklı uygulama bileşenlerinin diğer parçalarda istek doğrulaması tetiklemeden farklı istek verilerine bakmasını kolaylaştırır.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Geçersiz kılınmamış istekler için destek

Ertelenmiş istek doğrulaması tek başına istek doğrulamasını seçerek atlama sorununu çözmez. Request.Form["forum\_post"] çağrısı yine de belirli bir istek değeri için istek doğrulamasını tetikler. Ancak, bu alanda biçimlendirmeye izin vermek istediğiniziçin doğrulamayı tetiklemeden bu alana erişmek isteyebilirsiniz.

Buna izin vermek için, ASP.NET 4,5 artık istenen verilere doğrulanmamış erişimi destekler. ASP.NET 4.5, *HttpRequest* sınıfında *geçersiz kılınmamış* yeni bir koleksiyon özelliği içerir. Bu koleksiyon, *Form,* *QueryString,* *Çerezler*ve *Url*gibi istek verilerinin tüm ortak değerlerine erişim sağlar.

Geçersiz kılınmamış istek verilerini okuyabilmek için forum örneğini kullanarak, öncelikle uygulamayı yeni istek doğrulama modunu kullanacak şekilde yapılandırmanız gerekir:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Daha sonra geçersiz biçim değerini okumak için *HttpRequest.Unvalidated* özelliğini kullanabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Güvenlik - *Onaylanmamış istek verilerini dikkatli kullanın!* ASP.NET 4.5, çok özel geçersiz istek verilerine erişmenizi kolaylaştırmak için geçersiz kılınmamış istek özelliklerini ve koleksiyonlarını ekledi. Ancak, tehlikeli metnin kullanıcılara görüntülenmediğinden emin olmak için ham istek verilerinde özel doğrulama gerçekleştirmeniz gerekir.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS Kütüphanesi

Microsoft AntiXSS Kitaplığı'nın popülaritesi nedeniyle, 4.5 ASP.NET artık bu kitaplığın sürüm 4.0'ından temel kodlama yordamlarını içermektedir.

Kodlama yordamları yeni *System.Web.Security.AntiXss* namespace *AntiXssEncoder* türü tarafından uygulanır. *AntiXssEncoder* türünü, türde uygulanan statik kodlama yöntemlerinden herhangi birini çağırarak doğrudan kullanabilirsiniz. Ancak, yeni anti-XSS yordamları kullanmak için en kolay yaklaşım varsayılan olarak *AntiXssEncoder* sınıfını kullanmak için ASP.NET bir uygulama yapılandırmaktır. Bunu yapmak için, Web.config dosyasına aşağıdaki özniteliği ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*KodlayıcıType* özniteliği *AntiXssEncoder* türünü kullanacak şekilde ayarlandığında, ASP.NET'daki tüm çıktı kodlaması yeni kodlama yordamlarını otomatik olarak kullanır.

Bunlar, harici AntiXSS kitaplığı ASP.NET 4,5'e dahil edilmiş bölümleridir:

- *HtmlEncode*, *HtmlFormUrlEncode*, ve *HtmlAttributeEncode*
- *XmlAttributeEncode* ve *XmlEncode*
- *UrlEncode* ve *UrlPathEncode* (yeni)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>WebSockets Protokolü desteği

WebSockets protokolü, http üzerinden bir istemci ve sunucu arasında güvenli, gerçek zamanlı çift yönlü iletişimin nasıl kurulabildiğini tanımlayan standartlara dayalı bir ağ protokolüdür. Microsoft, protokolün tanımlanmasına yardımcı olmak için hem IETF hem de W3C standartları kuruluşlarıyla birlikte çalışmıştır. WebSockets protokolü, Microsoft'un hem istemci hem de mobil işletim sistemlerinde WebSockets protokolünü destekleyen önemli kaynaklara yatırım yaptığı herhangi bir istemci (yalnızca tarayıcılar) tarafından desteklenir.

WebSockets protokolü, istemci ve sunucu arasında uzun süreli veri aktarımları oluşturmayı çok daha kolay hale getirir. Örneğin, bir istemci ve sunucu arasında gerçek bir uzun soluklu bağlantı kurabilirsiniz, çünkü bir sohbet uygulaması yazma çok daha kolaydır. Bir soketin davranışını simüle etmek için periyodik yoklama veya HTTP uzun yoklama gibi geçici çözüme başvurmanız gerekmez.

4.5 ve IIS 8 ASP.NET düşük düzeyli WebSockets desteği içerir ve ASP.NET geliştiricilerin yönetilen API'leri websockets nesnesi üzerinde hem dize hem de ikili verileri eşzamanlı olarak okumave yazma için kullanmalarını sağlar. 4.5ASP.NET için, WebSockets protokolü ile çalışmak için türleri içeren yeni bir *System.Web.WebSockets* ad alanı vardır.

Tarayıcı istemcisi, aşağıdaki örnekte olduğu gibi, ASP.NET bir uygulamada BIR URL'yi işaret eden bir DOM *WebSocket* nesnesi oluşturarak bir WebSockets bağlantısı kurar:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Herhangi bir modül veya işleyici kullanarak ASP.NET WebSockets uç noktaları oluşturabilirsiniz. Önceki örnekte, .ashx dosyaları işleyici oluşturmak için hızlı bir yol olduğundan, bir .ashx dosyası kullanılmıştır.

WebSockets protokolüne göre, bir ASP.NET uygulaması, isteğin BIR HTTP GET isteğinden WebSockets isteğine yükseltilmesi gerektiğini belirterek istemcinin WebSockets isteğini kabul eder. Bir örneği aşağıda verilmiştir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest* yöntemi, ASP.NET geçerli HTTP isteğini geri aldığı ve ardından denetimi işlev temsilcisine aktardığı için bir işlev temsilcisi kabul eder. Kavramsal olarak bu yaklaşım, arka plan çalışmasının gerçekleştirildiği bir iş parçacığı başlatma temsilcisi tanımladığınız *System.Threading.Thread'i*nasıl kullandığınıza benzer.

ASP.NET ve istemci websockets el sıkışmasını başarıyla tamamladıktan sonra, ASP.NET temsilcinizi arar ve WebSockets uygulaması çalışmaya başlar. Aşağıdaki kod örneği, ASP.NET yerleşik WebSockets desteğini kullanan basit bir yankı uygulamasını gösterir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

.NET 4.5'teki *destek, bekleme* anahtar sözcüğü ve eşzamanlı görev tabanlı işlemler için WebSockets uygulamaları yazmak için doğal bir uyum sağlar. Kod örneği, Bir WebSockets isteğinin ASP.NET içinde tamamen eş senkronize olarak çalıştığını gösterir. Uygulama, bekleme soketi'ni arayarak istemciden bir iletinin gönderilmesini eşzamanlı olarak *bekler. ReceiveAsync*. Benzer şekilde, bekleme soketi'ni arayarak istemciye eşzamanlı bir ileti *gönderebilirsiniz. SendAsync*.

Tarayıcıda, bir uygulama *bir onmessage* işlevi aracılığıyla WebSockets iletileri alır. Bir tarayıcıdan ileti göndermek için, bu örnekte gösterildiği gibi *WebSocket* DOM türünün *gönderme* yöntemini çağırırsınız:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

Gelecekte, WebSockets uygulamaları için bu sürümde gerekli olan düşük düzeyli kodlamanın bazılarını özetleyen bu işlevsellik güncelleştirmeleri yayımlayabiliyoruz.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Paketleme ve Küçültme

Bundling, tek bir JavaScript ve CSS dosyalarını tek bir dosya gibi ele alınabilecek bir pakette birleştirmenizi sağlar. Minification, gerekli olmayan boşluk ve diğer karakterleri kaldırarak JavaScript ve CSS dosyalarını yoğunlaştırır. Bu özellikler Web Formları, ASP.NET MVC ve Web Sayfaları ile çalışır.

Paketler, Bundle sınıfı veya alt sınıfları, ScriptBundle ve StyleBundle kullanılarak oluşturulur. Paketin bir örneğini yapılandırıldıktan sonra, paket yalnızca global bir BundleCollection örneğine ekleyerek gelen isteklere açık hale getirilir. Varsayılan şablonlarda paket yapılandırması bir BundleConfig dosyasında gerçekleştirilir. Bu varsayılan yapılandırma, şablonlar tarafından kullanılan tüm temel komut dosyaları ve css dosyaları için paketler oluşturur.

Paketler, birkaç olası yardımcı yöntemden biri kullanılarak görünümler içinden başvurulur. Hata ayıklama ve sürüm modundayken bir paket için farklı biçimlendirme oluşturmayı desteklemek için, ScriptBundle ve StyleBundle sınıflarında yardımcı yöntem, Render vardır. Hata ayıklama modundayken, Render paketteki her kaynak için biçimlendirme oluşturur. Sürüm modundayken, Render tüm paket için tek bir biçimlendirme öğesi oluşturur. Hata ayıklama ve sürüm modu arasında gezinme, aşağıda gösterildiği gibi web.config'deki derleme öğesinin hata ayıklama özniteliğini değiştirerek gerçekleştirilebilir:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Ayrıca, optimizasyonun etkinleştirilmesi veya devre dışı bırakılması doğrudan BundleTable.EnableOptimizations özelliği üzerinden ayarlanabilir.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Dosyalar paketlendiğinde, önce alfabetik olarak sıralanırlar **(Çözüm Gezgini'nde**görüntülenme şekilleri). Daha sonra bilinen kitaplıklar ve özel uzantıları (jQuery, MooTools ve Dojo gibi) ilk yüklenir böylece düzenlenir. Örneğin, yukarıda gösterildiği gibi Komut Dosyaları klasörünün birbirilmesi için son sıra:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS dosyaları da alfabetik olarak sıralanır ve sonra sıfırlama.css ve normalize.css başka bir dosya önce gelmek böylece yeniden düzenlenir. Yukarıda gösterilen Stiller klasörünün birleştirme son sıralama sı aşağıdaki olacaktır:

1. Reset.css
2. content.css
3. forms.css
4. globals.css
5. menü.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web Hosting için Performans Geliştirmeleri

.NET Framework 4.5 ve Windows 8, web sunucusu iş yükleri için önemli bir performans artışı elde yardımcı olabilecek özellikler sunar. Buna bir azalma (%35'e kadar) dahildir hem başlangıç zamanında hem de ASP.NET kullanan web barındırma sitelerinin bellek ayak izinde.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Temel performans faktörleri

İdeal olarak, tüm web siteleri etkin olmalı ve bir sonraki isteğe hızlı yanıt sağlamak için bellekte olmalıdır, ne zaman gelirse. Site yanıt verme yeteneğini etkileyebilecek etkenler şunlardır:

- Bir uygulama havuzu geri dönüşümden sonra bir sitenin yeniden başlatılması için gereken süre. Bu, site derlemeleri artık bellekte değilken site için bir web sunucusu işlemi başlatmak için gereken süredir. (Diğer siteler tarafından kullanıldığından platform derlemeleri hala bellektedir.) Bu durum "soğuk site, sıcak çerçeve başlangıç" veya sadece "soğuk site başlangıç" olarak adlandırılır.
- Sitenin ne kadar bellek kaplar. Bunun için terimler "site başına bellek tüketimi" veya "paylaşılmayan çalışma kümesi" dir.

Yeni performans iyileştirmeleri bu faktörlerin her ikisine de odaklanır.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Yeni Performans Özellikleri Için Gereksinimler

Yeni özellikler için gereksinimler şu kategorilere ayrılabilir:

- .NET Framework 4'te çalışan geliştirmeler.
- .NET Framework 4.5 gerektiren ancak Windows'un herhangi bir sürümünde çalıştırılabilen geliştirmeler.
- Yalnızca Windows 8'de çalışan .NET Framework 4.5 ile kullanılabilen geliştirmeler.

Etkinleştirebildiğiniz her iyileştirme düzeyiyle performans artar.

.NET Framework 4.5 geliştirmelerinden bazıları, diğer senaryolar için de geçerli olan daha geniş performans özelliklerinden yararlanır.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Ortak Derlemeleri Paylaşma

**Gereksinim**: .NET Framework 4 ve Visual Studio 11 Geliştirici Önizleme SDK

Sunucudaki farklı siteler genellikle aynı yardımcı derlemeleri kullanır (örneğin, başlangıç kitinden veya örnek uygulamadan derlemeler). Her sitenin Bin dizininde bu derlemelerin kendi kopyası vardır. Derlemeler için nesne kodu aynı olsa da, bunlar fiziksel olarak ayrı derlemelerdir, bu nedenle her derleme nin soğuk site başlatma sırasında ayrı ayrı okunması ve ayrı olarak bellekte tutulması gerekir.

Yeni dahiletme işlevi bu verimsizliği çözer ve hem RAM gereksinimlerini hem de yükleme süresini azaltır. Staj, Windows'un her derlemenin tek bir kopyasını dosya sisteminde tutmasına olanak tanır ve site Bin klasörleri klasörleri deki tek derlemeler tek kopyaya sembolik bağlantılarla değiştirilir. Tek bir sitenin derlemenin farklı bir sürümüne ihtiyacı varsa, sembolik bağlantı derlemenin yeni sürümüyle değiştirilir ve yalnızca bu site etkilenir.

Derlemeleri sembolik bağlantılar kullanarak paylaşmak, interned\_derlemeleri deposuoluşturmanıza ve yönetmenize olanak tanıyan aspnet intern.exe adlı yeni bir araç gerektirir. Visual Studio 11 Developer Preview SDK'nın bir parçası olarak sağlanmaktadır. (Ancak, en son [güncelleştirmeyi](https://support.microsoft.com/kb/2468871)yüklediğinizi varsayarak yalnızca .NET Framework 4 yüklü olan bir sistem üzerinde çalışacaktır.)

Tüm uygun derlemelerin staj alabilmesini sağlamak için\_aspnet intern.exe'yi periyodik olarak çalıştırın (örneğin, haftada bir kez planlanmış bir görev olarak). Tipik bir kullanım aşağıdaki gibidir:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Tüm seçenekleri görmek için aracı bağımsız değişken olmadan çalıştırın.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Daha hızlı başlatma için çok Çekirdekli JIT derlemesi kullanma

**Gereksinim**: .NET Framework 4.5

Soğuk bir site başlatma için, sadece derlemeler diskten okunması gerekir, ancak site JIT-derlenmiş olmalıdır. Karmaşık bir site için bu önemli gecikmeler ekleyebilirsiniz. .NET Framework 4.5'teki yeni bir genel amaçlı teknik, JIT derlemesini kullanılabilir işlemci çekirdeklerine yayarak bu gecikmeleri azaltır. Bu kadar çok ve mümkün olduğunca erken sitenin önceki lansmanları sırasında toplanan bilgileri kullanarak yapar. [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) yöntemi ile bu işlevsellik uygulanmaktadır.

Birden çok çekirdek kullanarak JIT derleme varsayılan olarak ASP.NET, bu nedenle bu özellikyararlanmak için bir şey yapmanız gerekmez. Bu özelliği devre dışı kılmış olmak istiyorsanız, Web.config dosyasında aşağıdaki ayarı yapın:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Bellek için en iyi duruma getirmek için çöp toplama yı

**Gereksinim**: .NET Framework 4.5

Bir site çalıştırdıktan sonra, çöp toplayıcı (GC) yığınının kullanımı bellek tüketiminde önemli bir faktör olabilir. Herhangi bir çöp toplayıcısı gibi,.NET Framework GC de CPU zamanı (koleksiyonların sıklığı ve önemi) ile bellek tüketimi (yeni, serbest bırakılan veya serbest nesneler için kullanılan ekstra alan) arasında dengeler yapar. Önceki sürümler için, doğru dengeyi sağlamak için GC'nin nasıl yapılandırılacaklarına ilişkin kılavuzlar sağladık (örneğin, bkz ASP.NET [2.0/3.5 Paylaşılan Barındırma Yapılandırması).](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)

.NET Framework 4.5 için, birden çok bağımsız ayar yerine, daha önce önerilen GC ayarlarının tümünün yanı sıra site başına çalışma kümesi için ek performans sağlayan yeni ayarlamaları sağlayan iş yükü tanımlı bir yapılandırma ayarı kullanılabilir.

GC bellek ayarlamasını etkinleştirmek için Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(aspnet.config'deki değişiklikler için önceki kılavuza aşinaysanız, bu ayarın eski ayarların yerini alsa lar — örneğin gcServer, gcConcurrent, vb. ayarlamaya gerek olmadığını unutmayın. Eski ayarları kaldırmanız gerekmez.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Web uygulamaları için ön alma

**Gereksinim**: .NET Framework 4.5 Windows 8'de çalışıyor

Birkaç sürüm için Windows, uygulama başlatmanın disk okuma maliyetini azaltan [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) olarak bilinen bir teknoloji eklemiştir. Soğuk başlatma ağırlıklı olarak istemci uygulamaları için bir sorun olduğundan, bu teknoloji yalnızca bir sunucu için gerekli olan bileşenleri içeren Windows Server'a dahil edilmemiştir. Prefetching artık Windows Server'ın en son sürümünde kullanılabilir ve burada tek tek web sitelerinin başlatılmasını en iyi duruma getirebilir.

Windows Server için prefetcher varsayılan olarak etkinleştirilmez. Yüksek yoğunluklu web barındırma için prefetcher'ı etkinleştirmek ve yapılandırmak için komut satırında aşağıdaki komut kümesini çalıştırın:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Daha sonra, prefetcher ASP.NET uygulamaları ile tümleştirmek için, Web.config dosyasına aşağıdakileri ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Kesin Türü Belirtilmiş Veri Denetimleri

4.5 ASP.NET, Web Formları verilerle çalışmak için bazı geliştirmeler içerir. İlk geliştirme güçlü bir şekilde yazılan veri denetimleridir. ASP.NET önceki sürümlerindeki Web Formları denetimleri için, *Eval* ve veri bağlayıcı ifade kullanarak veriye bağlı bir değer görüntülersiniz:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

Çift yönlü veri bağlama için *Bind*kullanın:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

Çalışma zamanında, bu çağrılar belirtilen üyenin değerini okumak ve sonra işaretleme sonucu görüntülemek için yansıma kullanın. Bu yaklaşım, verilerin rasgele, şekillenmemiş verilere karşı bağlanmasını kolaylaştırır.

Ancak, bu gibi veri bağlayıcı ifadeler üye adları için IntelliSense, navigasyon (Tanıma Git gibi) veya bu adlar için derleme zamanı denetimi gibi özellikleri desteklemez.

Bu sorunu gidermek için, ASP.NET 4,5, denetimin bağlı olduğu verilerin veri türünü bildirme olanağı nı ekler. Bunu yeni *ItemType* özelliğini kullanarak yaparsınız. Bu özelliği ayarladığınızda, veri bağlama ifadeleri kapsamında iki yeni daktino değişken kullanılabilir: *Öğe* ve *BindItem.* Değişkenler güçlü bir şekilde yazıldığı için Visual Studio geliştirme deneyiminin tüm avantajlarından yararlanırsınız.

Çift yönlü veri bağlama ifadeleri için *BindItem* değişkenini kullanın:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web Formlar çerçevesinde veri bağlamayı destekleyen çoğu denetim *ItemType* özelliğini desteklemek üzere güncelleştirildi.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Model Bağlama

Model bağlama, kod odaklı veri erişimiyle çalışmak için ASP.NET Web Forms denetimlerinde veri bağlamayı genişletir. *ObjectDataSource* denetiminden ve ASP.NET MVC'de model bağlama kavramları içerir.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Veri seçme

Verileri seçmek için model bağlamayı kullanacak bir veri denetimini yapılandırmak için, denetimin *SelectMethod* özelliğini sayfanın kodundaki bir yöntemin adına ayarlarsınız. Veri denetimi, yöntemi sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. *DataBind* yöntemini açıkça aramanız gerekmez.

Aşağıdaki örnekte, *GridView* denetimi *GetCategories*adlı bir yöntem kullanacak şekilde yapılandırılır:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

Sayfanın kodunda *GetCategories* yöntemini oluşturursunuz. Basit bir seçim işlemi için yöntemin parametreye ihtiyacı yoktur ve Tanımlanabilir veya *Sorgulanabilen* bir nesne döndürmelidir. *IQueryable* Yeni *ItemType* özelliği ayarlanmışsa (daha önce Güçlü Olarak [Yazılan Veri Denetimleri](#_Toc318097386) altında açıklandığı gibi güçlü bir şekilde yazılan veri bağlama ifadelerini etkinleştiren), bu arabirimlerin genel sürümleri *, ItemType* özelliğinin türüyle eşleşen *T* parametresi ile (örneğin, *IQueryable&lt;Category)&gt;* ile birlikte ( Tanımlanabilir *&lt;T&gt; * veya *IQueryable&lt;T&gt;*) döndürülmelidir.

Aşağıdaki örnek, *GetCategories* yönteminin kodunu gösterir. Bu örnek, Northwind örnek veritabanıile Varlık Çerçeve Kodu İlk modelini kullanır. Kod, sorgunun Her kategori için ilgili ürünlerin ayrıntılarını *Ekle* yöntemi yle döndürmesini sağlar. (Bu, biçimlendirmedeki *TemplateField* öğesinin [n+1 seçmegerektirmeden](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)her kategorideki ürün sayısını görüntülemesini sağlar.)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Sayfa çalıştığında, *GridView* denetimi *GetCategories* yöntemini otomatik olarak çağırır ve döndürülen verileri yapılandırılan alanları kullanarak işler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Select yöntemi Bir *IQueryable* nesnesi döndürür, *GridView* denetimi yürütmeden önce sorguyu daha fazla işleyebilir. Örneğin, *GridView* denetimi, yürütülmeden önce döndürülen *IQueryable* nesnesine sıralama ve sayfalama için sorgu ifadeleri ekleyebilir, böylece bu işlemler altta yatan LINQ sağlayıcısı tarafından gerçekleştirilir. Bu durumda, Entity Framework bu işlemlerin veritabanında gerçekleştirilmesini sağlayacaktır.

Aşağıdaki örnekte *GridView* denetimi sıralama ve sayfalama izin vermek için değiştirildi gösterir:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Şimdi sayfa çalıştığında, denetim yalnızca geçerli veri sayfasının görüntülendiğinden ve seçili sütun tarafından sıralandığından emin olabilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Döndürülen verileri filtrelemek için parametrelerin select yöntemine eklenmesi gerekir. Bu parametreler çalışma zamanında bağlama modeli tarafından doldurulur ve verileri döndürmeden önce sorguyu değiştirmek için bunları kullanabilirsiniz.

Örneğin, sorgu dizesinde bir anahtar kelime girerek kullanıcıların ürünleri filtrelemasına izin vermek istediğinizi varsayalım. Yönteme bir parametre ekleyebilir ve parametre değerini kullanmak için kodu güncelleştirebilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Bu kod, *anahtar kelime* için bir değer sağlanmışsa ve sorgu sonuçlarını döndürürse *Nerede* ifadesini içerir.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Değer sağlayıcılar

Önceki örnek, *anahtar kelime* parametresi değerinin nereden geldiği konusunda özel değildi. Bu bilgileri belirtmek için bir parametre özniteliği kullanabilirsiniz. Bu örnekiçin, *System.Web.ModelBinding* ad alanında bulunan *QueryStringAttribute* sınıfını kullanabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

Bu, sorgu dizesinden anahtar *kelime* parametresine çalışma zamanında bir değer bağlamayı denemek için model bağlamatalimatı verir. (Bu durumda olmasa da, bu tür dönüştürme gerçekleştirme içerebilir.) Bir değer sağlanamazsa ve tür nullable değilse, bir özel durum atılır.

Bu yöntemlerin değer kaynakları değer sağlayıcılar olarak adlandırılır ve hangi değer sağlayıcısının kullanılacağını gösteren parametre öznitelikleri ne ad verilir. Web Formları, sorgu dizesi, tanımlama bilgileri, form değerleri, denetimler, görünüm durumu, oturum durumu ve profil özellikleri gibi bir Web Forms uygulamasındaki tüm tipik kullanıcı girişi kaynakları için değer sağlayıcılar ve ilgili öznitelikler içerir. Özel değer sağlayıcılar da yazabilirsiniz.

Varsayılan olarak, parametre adı değer sağlayıcı koleksiyonunda bir değer bulmak için anahtar olarak kullanılır. Örnekte, kod anahtar kelime (örneğin, ~/default.aspx?keyword=chef) adlı bir sorgu dize değeri arar. Parametre özniteliğine bağımsız değişken olarak geçirerek özel bir anahtar belirtebilirsiniz. Örneğin, q adlı sorgu dize değişkeninin değerini kullanmak için şunları yapabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Bu yöntem sayfanın kodunda ysa, kullanıcılar sorgu dizesini kullanarak bir anahtar kelime geçirerek sonuçları filtreleyebilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

Model bağlama, aksi takdirde elle kodlamanız gereken birçok görevi gerçekleştirir: değeri okuma, null değeri denetleme, uygun türe dönüştürmeye çalışma, dönüştürmenin başarılı olup olmadığını denetleme ve son olarak sorgudaki değeri kullanma. Model bağlama, çok daha az kod ve uygulamanız boyunca işlevselliği yeniden kullanma olanağıyla sonuçlanır.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Denetimden gelen değerlere göre filtreleme

Kullanıcının açılan listeden bir filtre değeri seçmesine izin vermek için örneği genişletmek istediğinizi varsayalım. Aşağıdaki açılır listeyi işaretlemeye ekleyin ve *SelectMethod* özelliğini kullanarak verilerini başka bir yöntemden alacak şekilde yapılandırın:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

Genellikle *GridView* denetimine bir *EmptyDataTemplate* öğesi de eklersiniz, böylece eşleşen ürünler bulunmazsa denetim bir ileti görüntüler:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

Sayfa kodunda, açılan liste için yeni seç yöntemini ekleyin:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Son olarak, açılan listeden seçili kategorinin kimliğini içeren yeni bir parametre almak için *GetProducts* seç yöntemini güncelleştirin:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Şimdi sayfa çalıştığında, kullanıcılar açılır listeden bir kategori seçebilir ve *GridView* denetimi filtrelenmiş verileri göstermek için otomatik olarak yeniden bağlanır. Bu, model bağlamanın belirli yöntemler için parametrelerin değerlerini izlediği ve bir postback'ten sonra herhangi bir parametre değerinin değişip değişmediğini algıladığı için mümkündür. Bu durumda, model bağlama ilişkili veri denetimini verilere yeniden bağlamaya zorlar.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML Kodlanmış Veri Bağlama İfadeleri

Artık veri bağlama ifadelerinin sonucunu HTML kodlayabilirsiniz. Bir kolon ekleme (:) veri bağlayıcı ifadeyi işaretleyen &lt;%# önekinin sonuna kadar:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Göze çarpmadan doğrulama

Artık istemci tarafı doğrulama mantığı için göze batmaz JavaScript kullanacak yerleşik doğrulayıcı denetimlerini yapılandırabilirsiniz. Bu, sayfa işaretlemede satır satır alalı olarak işlenen JavaScript miktarını önemli ölçüde azaltır ve genel sayfa boyutunu azaltır. Bu yollardan herhangi birinde geçerlilik denetimleri için göze batmaz JavaScript yapılandırabilirsiniz:

- Web.config dosyasındaki * &lt;appSettings&gt; * öğesine aşağıdaki ayarı ekleyerek genel olarak: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Global olarak statik *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* özelliğini *UnobtrusiveValidationMode.WebForms* 'a ayarlayarak (genellikle Global.asax dosyasındaki *\_Uygulama Başlangıç* yönteminde).
- *Sayfa* sınıfının yeni *UnobtrusiveValidationMode* özelliğini *UnobtrusiveValidationMode.WebForms'a*ayarlayarak bir sayfa için ayrı ayrı.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 Güncellemeleri

HTML5'in yeni özelliklerinden yararlanmak için Web Forms sunucu denetimlerinde bazı iyileştirmeler yapılmıştır:

- *TextBox* denetiminin *TextMode* *özelliği, e-posta,* *datetime*ve benzeri yeni HTML5 giriş türlerini desteklemek için güncelleştirildi.
- *FileUpload* denetimi artık bu HTML5 özelliğini destekleyen tarayıcılardan birden fazla dosya yüklemesini destekler.
- Validator denetimleri artık HTML5 giriş öğelerini doğrulamayı destekler.
- BIR URL'yi temsil eden özniteliklere sahip yeni HTML5 öğeleri artık runat="server"ı destekler. Sonuç olarak, uygulama kökünü temsil etmek için ~ işleci gibi URL yollarında &lt;ASP.NET kuralları kullanabilirsiniz (örneğin, video runat="sunucu"&gt;src="~/myVideo.wmv" / ).
- *UpdatePanel* denetimi, HTML5 giriş alanlarının deftere naklini destekleyecek şekilde düzeltildi.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta şimdi Visual Studio 11 Beta ile birlikte. ASP.NET MVC, Model-View-Controller (MVC) deseninden yararlanarak yüksek oranda test edilebilir ve korunabilir Web uygulamaları geliştirmek için bir çerçevedir. ASP.NET MVC 4, mobil Web için uygulama oluşturmayı kolaylaştırır ve herhangi bir cihaza ulaşabilen HTTP hizmetleri oluşturmanıza yardımcı olan ASP.NET Web API'sini içerir. Daha fazla bilgi için [MVC 4 Sürüm Notları ASP.NET](mvc4-release-notes.md)bakın.

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web Sayfaları 2

Yeni özellikler şunlardır:

- Yeni ve güncelleştirilmiş site şablonları.
- *Doğrulama* yardımcısını kullanarak sunucu tarafı ve istemci tarafı doğrulama ekleme.
- Varlıklar yöneticisini kullanarak komut dosyalarını kaydetme yeteneği.
- OAuth ve OpenID kullanarak Facebook ve diğer sitelerden giriş leri etkinleştirme.
- *Haritalar* yardımcısını kullanarak haritalar ekleme.
- Web Sayfaları uygulamalarını yan yana çalıştırmak.
- Mobil cihazlar için sayfaları oluşturma.

Bu özellikler ve tam sayfa kod örnekleri hakkında daha fazla bilgi [için, Web Sayfaları 2 Beta'daki En İyi Özellikler sayfasına](https://go.microsoft.com/fwlink/?LinkID=227824)bakın.

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Görsel Web Geliştirici 11 Beta

Bu bölümde Visual Web Developer 11 Beta ve Visual Studio 2012 Yayın Adayı web geliştirme geliştirmeleri hakkında bilgi sağlar.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 ve Visual Studio 2012 Sürüm Adayı Arasında Proje Paylaşımı (Proje Uyumluluğu)

Kadar Visual Studio 2012 Sürüm Aday, Visual Studio yeni bir sürümünde mevcut bir proje açılış Dönüşüm Sihirbazı başlattı. Bu, bir projenin içeriğinin (varlıklarının) ve çözümün geriye dönük uyumlu olmayan yeni biçimlere yükseltilmeye zorlanmasına neden oldu. Bu nedenle, dönüşümden sonra Visual Studio'nun eski sürümünde projeyi açamadınız.

Birçok müşteri bu doğru bir yaklaşım olmadığını söyledi. Visual Studio 11 Beta'da visual studio 2010 SP1 ile proje ve çözümleri paylaşmayı destekliyoruz. Bu, Visual Studio 2012 Sürüm Adayı'nda 2010 projesini açarsanız, projeyi Visual Studio 2010 SP1'de açabileceğiniz anlamına gelir.

> [!NOTE]
> Visual Studio 2010 SP1 ve Visual Studio 2012 Yayın Adayı arasında birkaç tür proje paylaşılamaz. Bunlar arasında bazı eski projeler (ASP.NET MVC 2 projeleri gibi) veya özel amaçlı projeler (Kurulum projeleri gibi) yer almaktadır.

Visual Studio 11 Beta'da ilk kez bir Visual Studio 2010 SP1 Web projesini açtığınızda, proje dosyasına aşağıdaki özellikler eklenir:

- FileUpgradeFlags
- YükseltmeBackupLocation
- OldToolsVersion
- Visualstudioversion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation ve OldToolsVersion proje dosyasını yükselten işlem tarafından kullanılır. Visual Studio 2010'da proje ile birlikte çalışma konusunda hiçbir etkileri yoktur.

VisualStudioVersion, MSBuild 4.5 tarafından kullanılan ve visual studio'nun geçerli proje sürümünü gösteren yeni bir özelliktir. Bu özellik MSBuild 4.0'da (Visual Studio 2010 SP1'in kullandığı MSBuild sürümünde) bulunmadığından, proje dosyasına varsayılan bir değer enjekte ediyoruz.

VSToolsPath özelliği, MSBuildExtensionsPath32 ayarı tarafından temsil edilen yoldan içe aktarılan doğru .targets dosyasını belirlemek için kullanılır.

Alma öğeleriyle ilgili bazı değişiklikler de vardır. Bu değişiklikler Visual Studio'nun her iki sürümü arasındaki uyumluluğu desteklemek için gereklidir.

> [!NOTE]
> Visual Studio 2010 SP1 ve Visual Studio 11 Beta arasında iki farklı bilgisayarda bir proje paylaşılıyorsa ve proje App\_Data klasöründe yerel bir veritabanı içeriyorsa, veritabanı tarafından kullanılan SQL Server sürümünün her iki bilgisayara da yüklendiğinden emin olmalısınız.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 Web Sitesi Şablonlarında Yapılandırma Değişiklikleri

Visual Studio 2012 Sürüm Adayı'nda web sitesi şablonları kullanılarak oluşturulan site için varsayılan *Web.config* dosyasında aşağıdaki değişiklikler yapılmıştır:

- Öğede, `<httpRuntime>` `encoderType` öznitelik artık varsayılan olarak ASP.NET eklenen AntiXSS türlerini kullanmak üzere ayarlanır. Ayrıntılar için [AntiXSS Kitaplığı'na](#_Toc318097382)bakın.
- Ayrıca `<httpRuntime>` öğede, `requestValidationMode` öznitelik "4,5" olarak ayarlanır. Bu, varsayılan olarak, istek doğrulama ertelenmiş ("tembel") doğrulama kullanmak için yapılandırılmış olduğu anlamına gelir. Ayrıntılar için [Yeni ASP.NET İstek Doğrulama Özellikleri'ne](#_Toc318097379)bakın.
- `<system.webServer>` Bölümün `<modules>` öğesi bir `runAllManagedModulesForAllRequests` öznitelik içermez. (Varsayılan değeri yanlıştır.) Bu, IIS 7'nin SP1'e güncelleştirilen bir sürümünü kullanıyorsanız, yeni bir sitede yönlendirme yle ilgili sorunlar olabileceğiniz anlamına gelir. Daha fazla bilgi için, [ASP.NET Yönlendirme için IIS 7'deki Yerel Destek'e](#Native_Support_In_IIS7_For_ASPNET_Routine)bakın.

Bu değişiklikler varolan uygulamaları etkilemez. Ancak, yeni şablonları kullanarak ASP.NET 4,5 için oluşturduğunuz mevcut web siteleri ve yeni web siteleri arasında davranış farkı temsil edebilir.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>ASP.NET Yönlendirme için IIS 7'de Yerel Destek

Bu, ASP.NET için bir değişiklik değil, SP1 güncelleştirmesini uygulamamış iIS 7 sürümüüzerinde çalışıyorsanız sizi etkileyebilecek yeni web sitesi projeleri için şablonlarda bir değişikliktir.

ASP.NET, yönlendirmeyi desteklemek için uygulamalara aşağıdaki yapılandırma ayarını ekleyebilirsiniz:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**RunAllManagedModulesForAllRequests** doğru olduğunda, URL'de `http://mysite/myapp/home` *.aspx*, *.mvc*veya benzer bir uzantı olmamasına rağmen, ASP.NET gibi bir URL gider.

IIS 7'ye yapılan bir **güncelleştirme, runAllManagedModulesForAllRequests** ayarını gereksiz kılar ve yerel olarak yönlendirmeASP.NET destekler. (Güncelleştirme hakkında bilgi için, belirli [IIS 7.0 veya IIS 7.5 işleyicilerinin URL'leri bir dönemle bitmeyen istekleri işlemesini sağlayan](https://support.microsoft.com/kb/980368)microsoft destek makalesine bakın.)

Web siteniz IIS 7'de çalışıyorsa ve IIS güncelleştirilmişse, **runAllManagedModulesForAllRequests'leri** doğru yapmanıza gerek yoktur. Aslında, bunu doğru ayarlamak önerilmez, çünkü istemek için gereksiz işlem yükü ekler. Bu ayar doğru olduğunda, *.htm*, *.jpg*ve diğer statik dosyalar da dahil olmak üzere tüm istekler, ASP.NET istek ardışık bölümünden geçer.

Visual Studio 2012 RC'de sağlanan şablonları kullanarak yeni bir ASP.NET 4.5 web sitesi oluşturursanız, web sitesinin yapılandırması **runAllManagedModulesForAllRequests** ayarını içermez. Bu, varsayılan olarak ayarın yanlış olduğu anlamına gelir.

Daha sonra SP1 yüklü olmadan Windows 7 web sitesini çalıştırırsanız, IIS 7 gerekli güncelleştirmeyi içermez. Sonuç olarak, yönlendirme çalışmaz ve hataları görürsünüz. Yönlendirmenin işe yaramadığını bir sorununuzun varsa, aşağıdakilerden birini yapabilirsiniz:

- Güncelleştirmeyi IIS 7'ye ekleyecek olan Windows 7'yi SP1'e güncelleyin.
- Daha önce listelenen Microsoft Destek makalesinde açıklanan güncelleştirmeyi yükleyin.
- **RunAllManagedModulesForAllRequests'i** bu web sitesinin Web.config dosyasında doğru şekilde ayarlayın. Bunun isteklere bazı ek ek yükü ekleyeceğini unutmayın.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML Düzenleyicisi

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Akıllı Görevler

Tasarım görünümünde, sunucu denetimlerinin karmaşık özellikleri genellikle iletişim kutuları ve sihirbazları kolay ayarlamak için ilişkili var. Örneğin, *Yinelenen* denetime veri kaynağı eklemek veya *GridView* denetimine sütun eklemek için özel bir iletişim kutusu kullanabilirsiniz.

Ancak, karmaşık özellikler için bu tür UI yardımı Kaynak görünümünde kullanılamıyor. Bu nedenle, Visual Studio 11 Kaynak görünümü için Akıllı Görevler tanıttı. Akıllı Görevler, C# ve Visual Basic düzenleyicilerinde sık kullanılan özellikler için bağlam duyarlı kısayollardır.

web formlarının ASP.NET için, ekleme noktası öğenin içinde olduğunda Akıllı Görevler sunucu etiketlerinde küçük bir glifler olarak görünür:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

Akıllı Görev, gph'yi tıklattığınızda veya CTRL+'ya bastığınızda genişler. (nokta), kod editörleri gibi. Daha sonra Tasarım görünümünde Akıllı Görevler'e benzer kısayollar görüntüler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Örneğin, önceki çizimdeki Akıllı Görev GridView Görevleri seçeneklerini gösterir. Sütunları Edit'i seçerseniz, aşağıdaki iletişim kutusu görüntülenir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

İletişim kutusunu doldurmak, Tasarım görünümünde ayarlaabileceğiniz özellikleri ayarlar. Tamam'ı tıklattığınızda, denetimin biçimlendirmesi yeni ayarlarla güncelleştirilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA desteği

Erişilebilir web siteleri yazma giderek daha önemli hale gelmektedir. [WAI-ARIA erişilebilirlik standardı, geliştiricilerin](http://www.w3.org/WAI/intro/aria) erişilebilir web sitelerini nasıl yazmaları gerektiğini tanımlar. Bu standart artık Visual Studio'da tam olarak desteklenmiştir.

Örneğin, *rol* özniteliği şimdi tam IntelliSense vardır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA standardı, html5 belgesine anlamsal eklemenize izin veren *arya* ile önceden belirlenmiş öznitelikleri de ekler. Visual Studio da tam olarak bu *arya* öznitelikleri destekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Yeni HTML5 parçacıkları

Daha hızlı ve daha kolay yaygın olarak kullanılan HTML5 işaretleme yazmak için, Visual Studio parçacıkları bir dizi içerir. Bir örnek video snippet olduğunu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Parçacığı çağırmak için, IntelliSense'de öğe seçildiğinde Sekme'ye iki kez basın:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Bu, özelleştirebileceğiniz bir parçacık üretir.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Kullanıcı denetimine ayıklama

Büyük web sayfalarında, tek tek parçaları kullanıcı denetimlerine taşımak iyi bir fikir olabilir. Bu yeniden düzenleme biçimi sayfanın okunabilirliğini artırmaya yardımcı olabilir ve sayfa yapısını basitleştirebilir.

Bunu kolaylaştırmak için, Kaynak görünümünde Web Formları sayfalarını güncellediğinizde, artık bir sayfadaki metni seçebilir, sağ tıklayabilir ve ardından Kullanıcı Denetimine Ayıkla'yı seçebilirsiniz:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>Öznitelikleri kod külçeleri için IntelliSense

Visual Studio her zaman herhangi bir sayfa veya kontrol sunucu tarafı kod nuggets için IntelliSense sağlamıştır. Şimdi Visual Studio html öznitelikleri kod nuggets için de IntelliSense içerir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

Bu, veri bağlayıcı ifadeler oluşturmayı kolaylaştırır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Açılış veya kapanış etiketini yeniden adlandırdığınızda eşleşen etiketin otomatik olarak yeniden adlandırılması

Bir HTML öğesini yeniden adlarsanız (örneğin, *div* etiketini *üstbilgi* etiketi olarak değiştirirseniz), karşılık gelen açılış veya kapanış etiketi de gerçek zamanlı olarak değişir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

Bu, kapanış etiketini değiştirmeyi veya yanlış etiketini değiştirmeyi unuttuğun hatayı önlemeye yardımcı olur.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Olay işleyicisi oluşturma

Visual Studio artık olay işleyicileri yazmanıza ve bunları el ile bağlamanıza yardımcı olmak için Kaynak görünümünde özellikler içerir. Kaynak görünümünde bir olay adını düzenliyorsanız, IntelliSense&gt;sayfanın kodunda doğru imzaya sahip bir olay işleyicisi oluşturacak Yeni Olay Oluştur'u görüntüler: &lt;

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Varsayılan olarak, olay işleyicisi olay işleme yönteminin adı için denetimin kimliğini kullanır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

Ortaya çıkan olay işleyicisi (bu durumda, C#) gibi görünecektir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Akıllı girintin

Boş bir HTML öğesinin içindeyken Enter tuşuna bastığınızda, düzenleyici ekleme noktasını doğru yere koyar:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Bu konumda Enter tuşuna baslarsanız, kapanış etiketi aşağı taşınır ve açılış etiketiyle eşleşecek şekilde girinir. Ekleme noktası da girintisi:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>İfade tamamlamayı otomatik küçültme

Visual Studio'daki IntelliSense listesi artık yazdıklarına göre yalnızca alakalı seçenekleri görüntülenebilmek için filtreleme yapmaktadır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense ayrıca IntelliSense listesindeki tek tek sözcüklerin başlık durumuna göre filtreler. Örneğin, "dl" yazarsanız, hem dl hem de asp:DataList görüntülenir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Bu özellik, bilinen öğeler için ekstre tamamlama almak için daha hızlı yapar.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript Düzenleyicisi

Visual Studio JavaScript editörü 2012 Sürüm Adayı tamamen yeni ve büyük ölçüde Visual Studio JavaScript ile çalışma deneyimini geliştirir.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Kod anahat

Anahat bölgeleri artık tüm işlevler için otomatik olarak oluşturulur ve dosyanın geçerli odağınızla ilgili olmayan kısımlarını daraltmanıza olanak sağlar.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Ayraç eşleştirme

Ekleme noktasını bir açma veya kapatma ayracına koyduğunuzda, düzenleyici eşleşeni vurgular.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Tanıma Git

Tanıma Git komutu, bir işlev veya değişken için kaynağa atlamanızı sağlar.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 desteği

Düzenleyici, JavaScript dilini açıklayan standardın en son sürümü olan ECMAScript5'teki yeni sözdizimini ve API'leri destekler.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

INtelliSense FOR DOM API'leri, *querySelector,* DOM Depolama, çapraz belge mesajlaşma ve *tuval*dahil olmak üzere birçok yeni HTML5 API'si desteği ile geliştirilmiştir. DOM IntelliSense artık yerel bir tür kitaplık tanımı yerine tek bir basit JavaScript dosyası tarafından yönlendirilir. Bu, genişletmeyi veya değiştirmeyi kolaylaştırır.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC imzası aşırı yükler

Ayrıntılı IntelliSense yorumları şimdi bu örnekte gösterildiği gibi, yeni * &lt;&gt; imza* öğesi kullanılarak JavaScript işlevlerinin ayrı overloads için ilan edilebilir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Örtük referanslar

Artık JavaScript dosyalarını, herhangi bir JavaScript dosyasının veya blok başvurularının bulunduğu dosyalar listesine dolaylı olarak dahil edilecek merkezi bir listeye ekleyebilirsiniz, yani içeriği için IntelliSense alırsınız. Örneğin, dosyaların merkezi listesine jQuery dosyaları ekleyebilirsiniz ve dosyanın herhangi bir JavaScript bloğunda jQuery işlevleri için IntelliSense alırsınız, açık &lt;bir&gt;şekilde başvuruda bulunup bulunmadığınız (lütfen başvuruyu kullanarak / ) veya değil.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS Editörü

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>İfade tamamlamayı otomatik küçültme

CSS için IntelliSense listesi artık seçilen şema tarafından desteklenen CSS özelliklerini ve değerlerini temel alarak filtreler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense ayrıca başlık durum aramalarını da destekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Hiyerarşik girintisi

CSS düzenleyicisi hiyerarşik kuralları görüntülemek için girintiyi kullanır ve bu da basamaklama kurallarının mantıksal olarak nasıl düzenlendiğine genel bir bakış sağlar. Aşağıdaki örnekte, seçici #list listenin basamaklı bir alt çocuğudur ve bu nedenle girintilenir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

Aşağıdaki örnekte daha karmaşık kalıtım gösterilmektedir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

Bir kuralın girintisi, ana kurallarıyla belirlenir. Hiyerarşik girintisi varsayılan olarak etkinleştirilir, ancak Seçenekler iletişim kutusunu devre dışı kullanabilirsiniz (Araçlar, Menü çubuğundan Seçenekler):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS kesmek desteği

Gerçek dünya CSS dosyalarıyüzlerce Analizi CSS kesmek çok yaygın olduğunu gösterir, ve şimdi Visual Studio en yaygın olarak kullanılan olanları destekler. Bu destek IntelliSense ve yıldız doğrulama\*içerir (\_) ve altını çizin ( ) özellik kesmek:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

Tipik seçici kesmek de hiyerarşik girintisi uygulandığında bile korunur böylece desteklenir. Internet Explorer 7'yi hedeflemek için kullanılan tipik bir seçici kesmek, bir seçiciyi * \*:first-child + html*ile prepend etmektir. Bu kuralın kullanılması hiyerarşik girintiyi korur:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Satıcıya özgü şemalar (-moz-, -webkit)

CSS3 farklı zamanlarda farklı tarayıcılar tarafından uygulanan birçok özellikleri tanıtır. Bu daha önce geliştiricileri satıcıya özgü sözdizimini kullanarak belirli tarayıcılar için kod lar kullanmaya zorlanır. Bu tarayıcıya özel özellikler artık IntelliSense'de yer alıyor.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Yorumlama ve yorumsuz destek

Artık kod düzenleyicisinde kullandığınız aynı kısayolları kullanarak CSS kurallarını yorumlayabilir ve yorumdışı kullanabilirsiniz (Ctrl+K,C yorum yapmak için ve Ctrl+K, yorum yapmayı bırakın).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Renk seçici

Visual Studio'nun önceki sürümlerinde, renkle ilgili öznitelikler için IntelliSense, adlandırılmış renk değerlerinin açılır listesinden oluşuyordu. Bu liste tam özellikli bir renk seçici tarafından değiştirildi.

Renk değeri girdiğinizde, renk seçici otomatik olarak görüntülenir ve daha önce kullanılan renklerin bir listesini ve ardından varsayılan renk paletini sunar. Fareyi veya klavyeyi kullanarak bir renk seçebilirsiniz.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

Liste tam bir renk seçici içine genişletilebilir. Seçici, opaklık kaydırıcısını hareket ettirdiğinizde herhangi bir rengi otomatik olarak RGBA'ya dönüştürerek alfa kanalını kontrol etmenizi sağlar:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Kod Parçacıkları

CSS düzenleyicisindeki parçacıklar tarayıcılar arası stilleri oluşturmayı daha kolay ve hızlı hale getirir. Tarayıcıya özel ayarlar gerektiren birçok CSS3 özelliği artık parçacıklara ayrılmıştır.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS parçacıkları, IntelliSense listesini gösteren at-symbol'u (@) yazarak gelişmiş senaryoları (CSS3 medya sorguları gibi) destekler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

Değer'i @media seçip Tab tuşuna bastığınızda, CSS düzenleyicisi aşağıdaki snippet'i ekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Kod parçacıklarında olduğu gibi, kendi CSS parçacıklarınızı oluşturabilirsiniz.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Özel bölgeler

Kod düzenleyicisinde zaten mevcut olan adlandırılmış kod bölgeleri artık CSS düzenlemesi için kullanılabilir. Bu, ilgili stil bloklarını kolayca gruplandırmanızı sağlar.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Bir bölge daraltıldığında, bölgenin adını görüntüler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Sayfa Denetçisi

Sayfa Denetçisi, Visual Studio IDE'de bir web sayfasını (HTML, Web Formları, ASP.NET MVC veya Web Sayfaları) işleyen ve hem kaynak kodu hem de ortaya çıkan çıktıyı incelemenize olanak tanıyan bir araçtır. Sayfa ASP.NET için Sayfa Denetçisi, tarayıcıya işlenen HTML biçimlendirmesini hangi sunucu tarafı kodunun ürettiğini belirlemenize olanak tanır.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Sayfa Denetçisi hakkında daha fazla bilgi için lütfen aşağıdaki eğitimlere bakın:

- [ASP.NET MVC'de](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md) Sayfa Denetçisi Kullanma
- sayfa denetçiyi [ASP.NET Web Formlarında](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md) Kullanma

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Yayımlama

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Yayımlama profilleri

Visual Studio 2010'da, Web uygulama projeleri için yayımlama bilgileri sürüm denetiminde depolanmaz ve başkalarıyla paylaşmak için tasarlanmaz. Visual Studio 2012 Sürüm Adayı'nda yayın profilinin biçimi değiştirildi. Bir takım artifakı yapıldı ve artık MSBuild'e dayalı yapılardan yararlanmak çok kolay. Yapı yapılandırma bilgileri Yayımlama iletişim kutusunda dır, böylece yayımlamadan önce yapı yapılandırmalarında kolayca geçiş yapabilirsiniz.

Yayımlama profilleri PublishProfiles klasöründe depolanır. Klasörün konumu, hangi programlama dilini kullandığınıza bağlıdır:

- C#: Özellikler\YayınProfilleri
- Visual Basic: Projem\YayınProfilleri

Her profil bir MSBuild dosyasıdır. Yayımlama sırasında, bu dosya projenin MSBuild dosyasına aktarılır. Visual Studio 2010'da, yayımlama veya paket işleminde değişiklik yapmak istiyorsanız, özelleştirmelerinizi **ProjectName**.wpp.targets adlı bir dosyaya koymanız gerekir. Bu hala desteklenir, ancak artık özelleştirmelerinizi yayımlama profilinin kendisine koyabilirsiniz. Bu şekilde, özelleştirmeler yalnızca bu profil için kullanılır.

Artık MSBuild'in yayın profillerinden de yararlanabilirsiniz. Bunu yapmak için, projeyi oluştururken aşağıdaki komutu kullanın:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Project.csproj değeri projenin yoludur ve ProfileName yayımlanacak profilin adıdır. Alternatif olarak, *PublishProfile* özelliğinin profil adını geçmek yerine, yayımlama profiline tam yoldan geçebilirsiniz.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET derleme ve birleştirme

Web uygulama projeleri için Visual Studio 2012 Sürüm Adayı, Paketi yayımladığınızda veya paketlediğinizde sitenizin içeriğini önceden derlemenize ve birleştirmenize olanak tanıyan Paket/Web özellikleri sayfasına bir seçenek ekler. Bu seçenekleri görmek için Solution Explorer'da projeyi sağ tıklatın, Özellikler'i seçin ve ardından Paket/Web özelliği sayfasını seçin. Aşağıdaki resimde yayımlama seçeneği önce Precompile bu uygulamayı gösterir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Bu seçenek seçildiğinde, Visual Studio web uygulamasını her yayımladığınızda veya paketlediğinizde uygulamayı önceden derler. Sitenin nasıl önceden derlenmiş olduğunu veya derlemelerin nasıl birleştiriliyi denetlemek istiyorsanız, bu seçenekleri yapılandırmak için Gelişmiş düğmesini tıklatın.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Ekspresi

Visual Studio'daki web projelerini test etmek için varsayılan web sunucusu artık IIS Express'tir. Visual Studio Development Server geliştirme sırasında yerel web sunucusu için hala bir seçenektir, ancak IIS Express artık önerilen sunucudur. Visual Studio 11 Beta'da IIS Express'i kullanma deneyimi Visual Studio 2010 SP1'de kullanmaya çok benzer.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Disclaimer

Bu bir ön belgedir ve burada açıklanan yazılımın nihai ticari sürümünden önce önemli ölçüde değiştirilebilir.

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Microsoft değişen pazar koşullarına yanıt vermesi gerektiğinden, bu durum Microsoft adına bir taahhüt olarak yorumlanmamalıdır ve Microsoft yayımtarihinden sonra sunulan bilgilerin doğruluğunu garanti edemez.

Bu Teknik İnceleme yalnızca bilgilendirme amaçlıdır. MICROSOFT, BU BELGEDEKI BILGILERLE ILGILI OLARAK AÇıK, ZıMNI VEYA YASAL HIÇBIR GARANTI VERMEZ.

Yürürlükteki tüm telif hakkı yasalarına uymak kullanıcının sorumluluğundadır. Telif hakkı kapsamındaki haklar sınırlandırılmadan, bu belgenin hiçbir bölümü, Microsoft Corporation'ın açık yazılı izni olmaksızın çoğaltılamaz, depolanamaz veya bir geri alma sistemine dahil edilemez veya herhangi bir biçimde veya herhangi bir şekilde (elektronik, mekanik, fotokopi, kayıt veya başka bir şekilde) iletilebilir.

Microsoft'un bu belgede konuyla ilgili patentleri, patent başvuruları, ticari markaları, telif hakları veya diğer fikri mülkiyet hakları olabilir. Microsoft'un herhangi bir yazılı lisans sözleşmesinde açıkça belirtilmesi dışında, bu belgenin döşenmesi size bu patentler, ticari markalar, telif hakları veya diğer fikri mülkiyet ler için herhangi bir lisans vermez.

Aksi belirtilmedikçe, örnek şirketler, kuruluşlar, ürünler, alan adları, e-posta adresleri, logolar, kişiler, yerler ve burada gösterilen olaylar hayalidir ve herhangi bir gerçek şirket, kuruluş, ürün, alan adı, e-posta adresi, logo, kişi, yer veya olay ile hiçbir ilişki amaçlanmıştır veya çıkarılmalıdır.

© 2012 Microsoft Corporation. Tüm hakları saklıdır.

Microsoft ve Windows, Microsoft Corporation'ın ABD ve/veya diğer ülkelerdeki tescilli ticari markaları veya ticari markalarıdır.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.
