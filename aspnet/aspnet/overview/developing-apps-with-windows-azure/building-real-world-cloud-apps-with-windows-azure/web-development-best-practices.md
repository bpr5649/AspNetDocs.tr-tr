---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web Geliştirme En İyi Uygulamaları (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma) | Microsoft Dokümanlar
author: MikeWasson
description: Azure e-kitaplı Building Real World Cloud Apps, Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bu 13 desen ve uygulamaları açıklar ki o olabilir ...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676001"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web Geliştirme En İyi Uygulamaları (Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)

Mike [Wasson](https://github.com/MikeWasson)tarafından , [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya Download [E-kitap indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-kitaplı **Building Real World Cloud Apps,** Scott Guthrie tarafından geliştirilen bir sunuya dayanmaktadır. Bulut için web uygulamalarını geliştirmekte başarılı olmanıza yardımcı olabilecek 13 model ve uygulamayı açıklar. E-kitap hakkında bilgi için [ilk bölüme](introduction.md)bakın.

İlk üç model çevik bir gelişim süreci kurmakla ilgiliydi; geri kalanı mimari ve kod hakkında. Bu web geliştirme en iyi uygulamaları bir koleksiyon:

- Akıllı yük dengeleyiciarkasında [Stateless web sunucuları.](#stateless)
- [Oturum durumu kaçının](#sessionstate) (veya bunu önleyemiyorsanız, veritabanı yerine dağıtılmış önbellek kullanın).
- Statik dosya varlıklarını (resimler, komut dosyaları) kenar önbelleğe almak için [CDN kullanın.](#cdn)
- Aramaları engellememek için [.NET 4.5'in async desteğini kullanın.](#async)

Bu uygulamalar yalnızca bulut uygulamaları için değil, bulut uygulamaları için de tüm web geliştirmeleri için geçerlidir. Bulut ortamının sunduğu son derece esnek ölçeklemeden en iyi şekilde yararlanmanıza yardımcı olmak için birlikte çalışırlar. Bu uygulamaları izlemezseniz, uygulamanızı ölçeklendirmeye çalıştığınızda sınırlamalarla karşınıza elendi.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Akıllı yük dengeleyicinin arkasındaki stateless web katmanı

*Stateless web katmanı,* web sunucusu belleğinde veya dosya sisteminde herhangi bir uygulama verisi depolamadığınız anlamına gelir. Web katmanınızı benzersiz tutmak hem daha iyi bir müşteri deneyimi sağlamanızı hem de paradan tasarruf etmenizi sağlar:

- Web katmanı devletsizse ve bir yük dengeleyicisinin arkasında oturuyorsa, sunucuları dinamik olarak ekleyerek veya kaldırarak uygulama trafiğindeki değişikliklere hızla yanıt verebilirsiniz. Sunucu kaynaklarını gerçekten kullandığınız sürece yalnızca ödeme yaptığınız bulut ortamında, talepteki değişikliklere yanıt verme yeteneği büyük tasarruflara dönüşebilir.
- Bir stateless web katmanı mimari çok daha basit uygulama ölçekli. Bu da ölçekleme ihtiyaçlarına daha hızlı yanıt ve süreç içinde geliştirme ve test daha az para harcamak sağlar.
- Şirket içi sunucular gibi bulut sunucuların ara sıra yamalı ve yeniden başlatılması gerekir; ve web katmanı devletsizse, bir sunucu geçici olarak çöktüğinde trafiği yeniden yönlendirme, hatalara veya beklenmeyen davranışlara neden olmaz.

Çoğu gerçek dünya uygulamaları bir web oturumu için devlet depolamak gerekir; burada ana nokta web sunucusunda saklamak için değil. Bir önbellek sağlayıcısı kullanarak, istemcide tanımlama bilgilerinde veya işlem sunucusu nun dışında ASP.NET oturum durumunda olduğu gibi başka şekillerde durum depolayabilirsiniz. Dosyaları yerel dosya sistemi yerine [Windows Azure Blob depolama alanında](unstructured-blob-storage.md) depolayabilirsiniz.

Web katmanınız bağımsızsa Windows Azure Web Sitelerinde bir uygulamayı ölçeklendirmenin ne kadar kolay olduğuna örnek olarak, yönetim portalındaki Windows Azure Web Sitesi **Ölçek** sekmesine bakın:

![Ölçek sekmesi](web-development-best-practices/_static/image1.png)

Web sunucuları eklemek istiyorsanız, örnek sayısı kaydırıcısını sağa sürükleyebilirsiniz. 5'e ayarlayın ve **Kaydet'i**tıklatın ve saniyeler içinde Windows Azure'da web sitenizin trafiğini işleyen 5 web sunucunuz vardır.

![Beş örnek](web-development-best-practices/_static/image2.png)

Örnek sayısını 3'e kadar kolayca ayarlayabilir veya 1'e geri dönebilirsiniz. Küçültttüldüğünde, Windows Azure saat başına değil, dakika dakika ücretlendirdiği için hemen para biriktirmeye başlarsınız.

Ayrıca, Windows Azure'a CPU kullanımına bağlı olarak web sunucusu sayısını otomatik olarak artırmasını veya azaltmasını da söyleyebilirsiniz. Aşağıdaki örnekte, CPU kullanımı %60'ın altına düştüğünde, web sunucusu sayısı en az 2'ye düşer ve CPU kullanımı %80'in üzerine çıkarsa, web sunucusu sayısı en fazla 4'e çıkarılacaktır.

![CPU kullanımına göre ölçekle](web-development-best-practices/_static/image3.png)

Ya da sitenizin yalnızca çalışma saatleri içinde meşgul olacağını biliyorsanız? Windows Azure'a gündüz birden çok sunucu çalıştırmasını ve tek bir sunucu akşamı, gece ve hafta sonuna kadar azalmasını söyleyebilirsiniz. Aşağıdaki ekran görüntüleri serisi, web sitesinin çalışma saatleri dışında bir sunucuyu ve çalışma saatleri içinde 08:00-17:00 saatleri arasında 4 sunucuyu çalıştırmak üzere nasıl kurulacağı gösterilmektedir.

![Zamanlamaya göre ölçeklendir](web-development-best-practices/_static/image4.png)

![Zamanlama saatlerini ayarlama](web-development-best-practices/_static/image5.png)

![Gündüz programı](web-development-best-practices/_static/image6.png)

![Hafta içi programı](web-development-best-practices/_static/image7.png)

![Hafta sonu programı](web-development-best-practices/_static/image8.png)

Ve tabii ki tüm bu komut dosyaları yanı sıra portal yapılabilir.

Web katmanını devlet siz tutarak sunucu VM'lerini dinamik olarak eklemeveya kaldırma nın önündeki engelleri önlediğiniz sürece, uygulamanızın ölçeklendirme yeteneği Windows Azure'da neredeyse sınırsızdır.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Oturum durumundan kaçının

Bir kullanıcı oturumu için bir tür durum depolamaktan kaçınmak için gerçek dünya bulut uygulamasında genellikle pratik değildir, ancak bazı yaklaşımlar performansı ve ölçeklenebilirliği diğerlerinden daha fazla etkiler. Durumu depolamanız gerekiyorsa, en iyi çözüm durum miktarını küçük tutmak ve tanımlama bilgilerinde saklamaktır. Bu mümkün değilse, bir sonraki en iyi çözüm [dağıtılmış, bellek içi önbellek](distributed-caching.md#sessionstate)için bir sağlayıcı ile ASP.NET oturum durumu kullanmaktır. Performans ve ölçeklenebilirlik açısından en kötü çözüm veritabanı destekli oturum durum sağlayıcısı kullanmaktır.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Statik dosya varlıklarını önbelleğe almak için CDN kullanma

CDN, İçerik Dağıtım Ağı'nın kısaltmasıdır. Görüntüler ve komut dosyası dosyaları gibi statik dosya varlıklarını bir CDN sağlayıcısına sağlarsınız ve sağlayıcı bu dosyaları tüm dünyadaki veri merkezlerinde önbelleğe alır, böylece insanlar uygulamanıza eriştikleri her yerde önbelleğe alınan varlıklar için nispeten hızlı yanıt ve düşük gecikme süresi elde ederler. Bu, sitenin toplam yükleme süresini hızlandırZ ve web sunucularınızdaki yükü azaltır. Coğrafi olarak yaygın olarak dağıtılan bir hedef kitleye ulaşıyorsanız, CDN'ler özellikle önemlidir.

Windows Azure'da CDN vardır ve Diğer CDN'leri Windows Azure'da veya herhangi bir web barındırma ortamında çalışan bir uygulamada kullanabilirsiniz.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Aramaları engellemeyi önlemek için .NET 4.5'in async desteğini kullanın

.NET 4.5, görevleri eş senkronize olarak işlemeyi çok daha kolay hale getirmek için C# ve VB programlama dillerini geliştirdi. Eşzamanlı programlamanın yararı, aynı anda birden çok web hizmeti çağrısını başlatmak istediğinizde olduğu gibi paralel işleme durumları için değildir. Ayrıca, web sunucunuzun yüksek yük koşullarında daha verimli ve güvenilir bir performans göstermesini sağlar. Bir web sunucusunda yalnızca sınırlı sayıda iş parçacığı vardır ve tüm iş parçacıkları kullanımda olduğunda yüksek yük koşullarında, gelen istekler iş parçacıkları serbest bırakılana kadar beklemek zorundadır. Uygulama kodunuz veritabanı sorguları ve web hizmeti çağrıları gibi görevleri eşsenkronize olarak işlemiyorsa, sunucu G/Ç yanıtı beklerken birçok iş parçacığı gereksiz yere bağlanır. Bu, sunucunun yüksek yük koşullarında işleyebilir trafik miktarını sınırlar. Eşzamanlı programlama ile, verileri döndürmek için bir web hizmeti veya veritabanı bekleyen iş parçacıkları veri alınana kadar yeni isteklere hizmet kadar serbest bırakılır. Meşgul bir web sunucusunda, yüzlerce veya binlerce istek, aksi takdirde iş parçacıklarının serbest bırakılmasını bekleyen hemen işlenebilir.

Daha önce de gördüğünüz gibi, web sitenizi işleyen web sunucularının sayısını artırmak kadar azaltmak da kolaydır. Bu nedenle, bir sunucu daha fazla iş hacmi elde edebilirse, bunların çoğuna ihtiyacınız yoktur ve belirli bir trafik hacmi için aksi takdirde gerekenden daha az sunucuya ihtiyacınız olduğundan maliyetlerinizi düşürebilirsiniz.

.NET 4.5 eşzamanlı programlama modeli desteği, Web Forms, MVC ve Web API için ASP.NET 4.5'e dahildir; Entity Framework 6'da ve [Windows Azure Depolama API'sinde.](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4,5'te Async desteği

4.5 ASP.NET, eşzamanlı programlama desteği sadece dile değil, MVC, Web Formları ve Web API çerçevelerine de eklenmiştir. Örneğin, ASP.NET bir MVC denetleyici eylem yöntemi bir web isteğinden veri alır ve verileri bir görünüme aktarır ve daha sonra tarayıcıya gönderilmek üzere HTML oluşturur. Eylem yönteminin, bir web sayfasında görüntülemek veya bir web sayfasına girilen verileri kaydetmek için bir veritabanından veya web hizmetinden veri alması gerekir. Bu senaryolarda eylem yöntemini eşzamanlı hale getirmek kolaydır: *ActionResult* nesnesini döndürmek *yerine,&lt;Görev&gt; EylemSonucu'nu* döndürür ve yöntemi *async* anahtar sözcüğüyle işaretlersiniz. Yöntemin içinde, bir kod satırı bekleme süresini içeren bir işlemi başlattığında, onu bekleyen anahtar sözcüğüyle işaretlersiniz.

Veritabanı sorgusu için depo yöntemi çağıran basit bir eylem yöntemi aşağıda veda edin:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

Ve burada veritabanı asynchronously arama işleyen aynı yöntemdir:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

Kapakların altında derleyici uygun asynchronous kodu oluşturur. Uygulama aramayı yaptığında `FindTaskByIdAsync`, ASP.NET `FindTask` isteği yapar ve daha sonra alt iş parçacığı geri ve başka bir istek işlemek için kullanılabilir hale getirir. `FindTask` İstek yapıldığında, bu çağrıdan sonra gelen kodu işlemeye devam etmek için bir iş parçacığı yeniden başlatılır. `FindTask` İsteğin başlatıldığı zaman ile veriler döndürüldüğünde ara dönemde, yanıtı beklerken bağlanacak yararlı işler yapmak için kullanılabilir bir iş parçacığına sahipsiniz.

Eşzamanlı kod için bazı ek yükler vardır, ancak düşük yük koşullarında, genel ek yükü önemsizdir, yüksek yük koşullarında ise kullanılabilir iş parçacığı için bekletilen istekleri işleebilirsiniz.

1.1'ASP.NET beri bu tür bir eşzamanlı programlama yapmak mümkün olmuştur, ancak yazmak zordu, hataya açık ve hata ayıklama zor. 4.5 ASP.NET'da bunun için kodlamayı basitleştirdiğimize göre, artık bunu yapmamak için bir neden yok.

### <a name="async-support-in-entity-framework-6"></a>Varlık Çerçevesi 6'da Async desteği

4.5'teki async desteğinin bir parçası olarak web hizmeti aramaları, soketler ve dosya sistemi G/Ç için async desteği gönderdik, ancak web uygulamaları için en yaygın desen bir veritabanına çarpmaktır ve veri kitaplıklarımız async'i desteklemedi. Şimdi Entity Framework 6 veritabanı erişimi için async desteği ekler.

Varlık Çerçevesi 6'da, bir sorgunun veya komutun veritabanına gönderilmesine neden olan tüm yöntemlerin async sürümleri vardır. Buradaki örnek, *Bul* yönteminin async sürümünü gösterir.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

Ve bu async desteği sadece ekler, siler, güncelleştirmeler ve basit bulur için değil, aynı zamanda LINQ sorguları ile çalışır:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

Yöntemin `ToList` bir `Async` sürümü vardır, çünkü bu kodda sorgunun veritabanına gönderilmesine neden olan yöntem budur. Yöntem `Where` `OrderByDescending` sorguyu yürütürken ve `ToListAsync` yanıtı `result` değişkende depolarken, yöntem yalnızca sorguyu yapılandırMaktadır.

## <a name="summary"></a>Özet

Burada belirtilen web geliştirme en iyi uygulamalarını herhangi bir web programlama çerçevesi ve herhangi bir bulut ortamında uygulayabilirsiniz, ancak bunu kolaylaştırmak için ASP.NET ve Windows Azure'da araçlarımız vardır. Bu desenleri izlerseniz, web katmanınızı kolayca ölçeklendirebilirsiniz ve her sunucu daha fazla trafik işleyebildiği için harcamalarınızı en aza indirirsiniz.

Bir [sonraki bölümde](single-sign-on.md) bulutun tek oturum açma senaryolarını nasıl etkinleştirilediği bak.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın.

Devletsiz web sunucuları:

- [Microsoft Desenleri ve Uygulamaları - Kılavuzu otomatikleştirin.](https://msdn.microsoft.com/library/dn589774.aspx)
- [Windows Azure Web Sitelerinde ARR'ın Örnek Affinity'si devre dışı bırakılıyor.](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/) Erez Benari tarafından blog yazısı, Windows Azure Web Sitelerinde oturum yakınlık açıklar.

Cdn:

- [FailSafe: Ölçeklenebilir, Esnek Bulut Hizmetleri Oluşturma.](https://channel9.msdn.com/Series/FailSafe) Ulrich Homann, Marc Mercuri ve Mark Simms tarafından dokuz bölümlük video serisi. 1:34:00'ten itibaren 3.
- [Microsoft Desenler ve Uygulamalar Statik İçerik Barındırma deseni](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN Yorumlar](http://www.cdnreviews.com/). Birçok CDN'ye genel bakış.

Asynchronous programlama:

- [MVC 4 ASP.NET Asynchronous Yöntemleri kullanma](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Rick Anderson tarafından Öğretici.
- [Async ve Await (C# ve Visual Basic) ile Asynchronous Programlama.](https://msdn.microsoft.com/library/vstudio/hh191443.aspx) Asynchronous programlamanın mantığını, 4.5 ASP.NET nasıl çalıştığını ve uygulamak için kod yazmayı açıklayan MSDN teknik incelemesi.
- [Varlık Çerçevesi Async Sorgusu ve Kaydet](https://msdn.microsoft.com/data/jj819165)
- [Async kullanarak web uygulamaları ASP.NET nasıl inşa edilir.](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7) Rowan Miller tarafından video sunumu. Asynchronous programlamanın yüksek yük koşullarında web sunucusu verimesinde önemli artışları nasıl kolaylaştırabileceğini gösteren bir grafik gösteri içerir.
- [FailSafe: Ölçeklenebilir, Esnek Bulut Hizmetleri Oluşturma.](https://channel9.msdn.com/Series/FailSafe) Ulrich Homann, Marc Mercuri ve Mark Simms tarafından dokuz bölümlük video serisi. Eşzamanlı programlamanın ölçeklenebilirlik üzerindeki etkisi hakkında tartışmalar için bölüm 4 ve bölüm 8'e bakın.
- [ASP.NET 4.5 artı önemli bir gotcha Asynchronous Yöntemleri kullanmamagic](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Scott Hanselman tarafından Blog yazısı, öncelikle ASP.NET Web Formları uygulamalarında async kullanarak ilgili.

Ek web geliştirme en iyi uygulamaları için aşağıdaki kaynaklara bakın:

- [Fix It Örnek Uygulama - En İyi Uygulamalar](the-fix-it-sample-application.md#bestpractices). Bu e-kitabın eki, Fix It uygulamasında uygulanan en iyi uygulamaları listeler.
- [Web Geliştirici Kontrol Listesi](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Önceki](continuous-integration-and-continuous-delivery.md)
> [Sonraki](single-sign-on.md)
