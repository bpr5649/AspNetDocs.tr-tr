---
title: MVC uygulamasına görünüm ekleme
author: Rick-Anderson
description: MVC uygulamasına görünüm ekleme
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045019"
---
# <a name="adding-a-view"></a>Görünüm Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu bölümde, `HelloWorldController` bir ISTEMCIYE HTML yanıtları oluşturma işlemini düzgün bir şekilde kapsüllemek için şablon dosyalarını görüntüle öğesini kullanmak için sınıfını değiştirirsiniz. 

[Razor görünüm altyapısını](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)kullanarak bir görünüm şablonu dosyası oluşturacaksınız. Razor tabanlı görünüm şablonlarının *. cshtml* dosya uzantısı vardır ve C# kullanarak HTML çıktısı oluşturmak için zarif bir yol sağlar. Razor, bir görünüm şablonu yazarken gereken karakter ve tuş vuruşlarının sayısını en aza indirir ve hızlı, akıcı bir kodlama iş akışını mümkün bir şekilde sunar.

Şu anda `Index` yöntemi, denetleyici sınıfında sabit kodlanmış bir ileti içeren bir dize döndürür. `Index`Aşağıdaki kodda gösterildiği gibi, yöntemi, Controllers [Görünüm](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) yöntemini çağırmak için değiştirin:

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

`Index`Yukarıdaki yöntem, TARAYıCıYA HTML yanıtı oluşturmak için bir görünüm şablonu kullanır. Yukarıdaki yöntem gibi denetleyici Yöntemleri ( [eylem yöntemleri](http://rachelappel.com/asp.net-mvc-actionresults-explained)olarak da bilinir), `Index` dize gibi basit türler değil, genellikle bir [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (veya [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)öğesinden türetilmiş bir sınıf) döndürür.

*Views\helloworld* klasörüne sağ tıklayın ve **Ekle**' ye ve ardından **MVC 5 görünüm sayfası düzen (Razor)** seçeneğine tıklayın.
  
![](adding-a-view/_static/image1.png)   
  
**Öğe Için ad belirtin** Iletişim kutusunda *Dizin*girin ve ardından **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image2.png)  
  
**Düzen sayfası seçin** iletişim kutusunda varsayılan ** \_ Layout. cshtml** dosyasını kabul edin ve **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image3.png)  
  
Yukarıdaki iletişim kutusunda, *Görünüm \ paylaşılan* klasörü sol bölmede seçilidir. Başka bir klasörde özel bir düzen dosyanız varsa, bunu seçebilirsiniz. Daha sonra öğreticide düzen dosyası hakkında konuşacağız

*Mvcmovie\views\helloworld\ındex.cshtml* dosyası oluşturulur.

![](adding-a-view/_static/image4.png)

Aşağıdaki Vurgulanan biçimlendirmeyi ekleyin.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

*Index. cshtml* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.

![PI](adding-a-view/_static/image5.png)

Ayrıca *Index. cshtml* dosyasına sağ tıklayıp **sayfa denetçisinde görüntüle** ' yi seçebilirsiniz. Daha fazla bilgi için bkz. [sayfa denetçisi öğreticisi](../../views/using-page-inspector-in-aspnet-mvc.md) .

Alternatif olarak, uygulamayı çalıştırın ve `HelloWorld` denetleyiciye ( `http://localhost:xxxx/HelloWorld` ) gidin. `Index`Denetleyicinizdeki yöntemi çok fazla iş gerçekleştirmedi; yalnızca metodunu çalıştırdığından `return View()` , metodun tarayıcıya yanıt işlemek için bir görünüm şablonu dosyası kullanması gerektiğini belirtti. Kullanılacak görünüm şablonu dosyasının adını açıkça belirtmediğinizden, ASP.NET MVC, *\Views\helloworld* klasöründeki *Index. cshtml* görünüm dosyasını kullanacak şekilde varsayılan olarak ' ı kullanır. Aşağıdaki görüntüde, Görünüm &quot; şablonumuza ait Merhaba! &quot; görünümde sabit kodlanmış dize gösterilmektedir.

![](adding-a-view/_static/image6.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlık çubuğunda "Index-My ASP.NET Application" ifadesinin görüntülendiğine ve sayfanın en üstündeki büyük bağlantının "uygulama adı" olduğunu fark edeceksiniz. Tarayıcı pencerenizi ne kadar küçük olduğunuza bağlı olarak, **giriş**, **hakkında**, **Iletişim**, **kayıt** ve **oturum açma bağlantılarında oturum** açmak için sağ üst köşedeki üç çubuğu tıklamanızı gerekebilir.

## <a name="changing-views-and-layout-pages"></a>Görünümleri ve düzen sayfalarını değiştirme

İlk olarak, &quot; &quot; sayfanın en üstündeki uygulama adı bağlantısını değiştirmek istersiniz. Bu metin her sayfada ortaktır. Aslında uygulamada her sayfada görünse de, projede yalnızca bir yerde uygulanır. **Çözüm Gezgini** */views/Shared* klasörüne gidin ve * \_ Layout. cshtml* dosyasını açın. Bu dosyaya bir *Düzen sayfası* denir ve diğer tüm sayfaların kullandığı paylaşılan klasörde bulunur.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Düzen şablonları, sitenizin HTML kapsayıcı yerleşimini tek bir yerde belirtmenize ve sonra sitenizdeki birden çok sayfaya uygulamanıza olanak tanır. Satırı bulun `@RenderBody()` . `RenderBody` , oluşturduğunuz tüm görünüme özgü sayfaların, &quot; Düzen sayfasında kaydırılan bir yer tutucudur &quot; . Örneğin, **hakkında** bağlantısını seçerseniz, *Views\home\about.exe* görünümü yöntemin içinde işlenir `RenderBody` .

Title öğesinin içeriğini değiştirin. Düzen şablonundaki [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) , &quot; uygulama adından &quot; &quot; MVC filmi &quot; ve denetleyiciyi ' dan `Home` `Movies` ' e kadar olan ActionLink değiştirin. Tüm düzen dosyası aşağıda gösterilmiştir:

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

Uygulamayı çalıştırın ve şimdi MVC filmi belirten bir uyarı görürsünüz &quot; &quot; . **Hakkında** ' ya tıklayın ve bu sayfanın &quot; MVC filmi de göster ' i nasıl göstertiğine bakabilirsiniz &quot; . Düzen şablonunda değişikliği bir kez yapabildik ve sitedeki tüm sayfalar yeni başlığı yansıtmaktadır.

![](adding-a-view/_static/image8.png)

İlk olarak *Views\helloworld\ındex.cshtml* dosyasını oluşturduğumuz zaman aşağıdaki kodu içerir:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Yukarıdaki Razor kodu, düzen sayfasını açıkça ayarlıyor. *Görünümler \\ _ViewStart. cshtml* dosyasını inceleyin, tam olarak aynı Razor işaretlemesini içerir. *[Görünümler \\ _ViewStart. cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* dosyası, tüm görünümlerin kullanacağı ortak düzeni tanımlar, bu nedenle söz konusu kodu *Views\helloworld\ındex.cshtml* dosyasından açıklama ekleyebilir veya kaldırabilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

`Layout`Özelliğini kullanarak farklı bir düzen görünümü ayarlayabilir veya bir `null` Düzen dosyası kullanılmayacak şekilde ayarlayabilirsiniz.

Şimdi Dizin görünümünün başlığını değiştirelim.

*Mvcmovie\views\helloworld\ındex.cshtml*dosyasını açın. Değişiklik yapmak için iki yer vardır: ilk olarak, tarayıcının başlığında görünen metin ve ardından ikincil üst bilgi ( `<h2>` öğe). Uygulamanın parçası olan hangi kod bitini değiştireceğiz için bunları biraz farklı hale getirebilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

Görüntülenecek HTML başlığını göstermek için, yukarıdaki kod `Title` nesnesinin bir özelliğini ayarlar `ViewBag` ( *Index. cshtml* görünüm şablonunda bulunan). Düzen şablonunun ( *Views\shared \\ _Layout. cshtml* ) bu değeri, `<title>` `<head>` daha önce değiştirildiğimiz HTML bölümünün bir parçası olarak öğesini kullandığını unutmayın.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

Bu `ViewBag` yaklaşımı kullanarak, görünüm şablonunuz ve düzen dosyanız arasında kolayca başka parametreler geçirebilirsiniz.

Uygulamayı çalıştırın. Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. (Tarayıcıda değişiklik görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz. Sunucudan gelen yanıtı zorlamak için tarayıcınızda CTRL + F5 tuşlarına basın.) Tarayıcı başlığı `ViewBag.Title` *Index. cshtml* görünüm şablonunda ve &quot; Düzen dosyasına eklenen ek film uygulamasına ayarlanmış olan ile oluşturulur &quot; .

Ayrıca *Index. cshtml* görünüm şablonundaki içeriğin * \_ Layout. cshtml* görünüm şablonuyla nasıl birleştirildiğini ve tarayıcıya tek bir HTML yanıtı gönderildiğini de unutmayın. Düzen şablonları, uygulamanızdaki tüm sayfalara uygulanan değişiklikler yapmayı gerçekten kolaylaştırır.

![](adding-a-view/_static/image9.png)

Çok az &quot; veri &quot; (Bu durumda, &quot; görüntüleme şablonumuzdaki Merhaba! &quot; iletisi) sabit kodlanmış, ancak. MVC uygulamasının bir &quot; V &quot; (görünüm) ve bir C (Controller) var &quot; &quot; , ancak &quot; &quot; henüz M (model) yok. Kısa süre içinde, bir veritabanının nasıl oluşturulduğunu ve model verilerinin nasıl alınacağını adım adım inceleyeceğiz.

## <a name="passing-data-from-the-controller-to-the-view"></a>Denetleyiciden görünüme veri geçirme

Bir veritabanına gitmekten ve modeller hakkında konuşmadan önce, ilk olarak denetleyiciden bir görünüme bilgi geçirme konusunda konuşalım. Denetleyici sınıfları gelen bir URL isteğine yanıt olarak çağrılır. Bir denetleyici sınıfı, gelen tarayıcı isteklerini işleyen, veritabanından veri alan ve son olarak tarayıcıya ne tür bir yanıt gönderileceğini karar veren kodu yazdığınız yerdir. Daha sonra Görünüm şablonları, tarayıcıya HTML yanıtı oluşturmak ve biçimlendirmek için bir denetleyiciden kullanılabilir.

Bir görünüm şablonunun tarayıcıya yanıt oluşturması için gereken verilerin veya nesnelerin sağlanmasından denetleyiciler sorumludur. En iyi yöntem: **bir görünüm şablonu asla iş mantığı gerçekleştirmemelidir veya doğrudan bir veritabanıyla etkileşime sahip olmalıdır**. Bunun yerine, bir görünüm şablonu yalnızca denetleyici tarafından sunulan verilerle birlikte çalışmalıdır. Bu sorunların &quot; ayrılmasını sürdürmek &quot; , kodunuzun temiz, test edilebilir ve daha sürdürülebilir olmasını sağlar.

Şu anda, `Welcome` sınıfındaki Action yöntemi `HelloWorldController` bir `name` ve `numTimes` parametresini alır ve sonra değerleri doğrudan tarayıcıya çıkarır. Denetleyicinin bu yanıtı bir dize olarak işlemesini sağlamak yerine, denetleyiciyi bir görünüm şablonu kullanacak şekilde değiştirelim. Görünüm şablonu dinamik bir yanıt oluşturur, bu, yanıtı oluşturmak için denetleyiciden uygun veri bitlerini görünüme geçirmeniz gerektiği anlamına gelir. Bu, denetleyicinin, görünüm şablonunun erişebileceği bir nesne için gerektirdiği dinamik verileri (parametreler) yerleştirerek bunu yapabilirsiniz `ViewBag` .

*HelloWorldController.cs* dosyasına dönün ve `Welcome` nesnesine bir ve değeri eklemek için yöntemini değiştirin `Message` `NumTimes` `ViewBag` . `ViewBag` dinamik bir nesnedir, bu, içinde istediğiniz her şeyi koyabileceğiniz anlamına gelir; `ViewBag` nesnenin içine bir öğe yerleştirene kadar tanımlanmış özellikleri yok. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri ( `name` ve `numTimes` ) adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler. Tüm *HelloWorldController.cs* dosyası şuna benzer:

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

Artık `ViewBag` nesne görünüme otomatik olarak geçirilecek verileri içerir. Daha sonra bir hoş geldiniz görünüm şablonunuz olması gerekir! Projenin derlendiğinden **Build** emin olmak için Build **(veya** Ctrl + Shift + B) öğesini seçin. *Views\helloworld* klasörüne sağ tıklayın ve **Ekle**' ye ve ardından **MVC 5 görünüm sayfası düzen (Razor)** seçeneğine tıklayın.
  
![](adding-a-view/_static/image10.png)   
  
**Öğe Için ad belirtin** Iletişim kutusunda *hoş geldiniz*yazın ve ardından **Tamam**' a tıklayın.   
  
**Düzen sayfası seçin** iletişim kutusunda varsayılan ** \_ Layout. cshtml** dosyasını kabul edin ve **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image11.png)   

*Mvcmovie\views\helloworld\welcome.cshtml* dosyası oluşturulur.

*Welcome. cshtml* dosyasındaki biçimlendirmeyi değiştirin. &quot;Kullanıcı tarafından söylenecek kadar Merhaba bir döngü oluşturacaksınız &quot; . Tüm *Welcome. cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

Uygulamayı çalıştırın ve aşağıdaki URL 'ye gidin:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Artık veriler URL 'den alınır ve [model cildi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)kullanılarak denetleyiciye geçirilir. Denetleyici, verileri bir `ViewBag` nesnesine paketler ve bu nesneyi görünüme geçirir. Daha sonra Görünüm, verileri kullanıcıya HTML olarak görüntüler.

![](adding-a-view/_static/image12.png)

Yukarıdaki örnekte, `ViewBag` denetleyicideki verileri bir görünüme geçirmek için bir nesne kullandık. Öğreticide daha sonra, bir denetleyicideki verileri bir görünüme geçirmek için bir görünüm modeli kullanacağız. Veri geçirme yaklaşımını görüntüleme yaklaşımı, görünüm paketi yaklaşımına göre genellikle çok tercih edilir. Daha fazla bilgi için bkz. blog girdisi [dinamik türü kesin belirlenmiş görünümler](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) . 

Bu, &quot; model için bir d türüdür &quot; , ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](adding-a-controller.md) 
>  [Sonraki](adding-a-model.md)
