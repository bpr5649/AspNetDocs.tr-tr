---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Denetleyici ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: ae3258872df798f52d8e031dc8ebf01b4f0a7358
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045136"
---
# <a name="adding-a-controller"></a>Denetleyici Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

MVC, *Model-View-Controller*için temsil eder. MVC, iyi şekilde tasarlanmış ve bakımı kolay olan uygulamalar geliştirmeye yönelik bir modeldir. MVC tabanlı uygulamalar şunları içerir:

- **K** odels: uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.
- **V** ıews: uygulamanızın HTML yanıtlarını dinamik olarak oluşturmak Için kullandığı şablon dosyaları.
- **C** ontrolleyiciler: gelen tarayıcı isteklerini işleyen, model verilerini alan ve tarayıcıya yanıt döndüren şablonları görüntüleme gibi sınıflar.

Bu öğretici serisinde bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

Bir denetleyici sınıfı oluşturarak başlayalım. **Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.

![](adding-a-controller/_static/image1.png)

**Yapı Iskelesi Ekle** Iletişim kutusunda **MVC 5 denetleyici-boş**' ya tıklayın ve ardından **Ekle**' ye tıklayın.

![](adding-a-controller/_static/image2.png)  

Yeni denetleyicinizi "Merhaba Dünya denetleyicisi" olarak adlandırın ve **Ekle**' ye tıklayın.

![denetleyici Ekle](adding-a-controller/_static/image3.png)

**Çözüm Gezgini** , *HelloWorldController.cs* adlı yeni bir dosya ve *views\helloworld*adlı yeni bir klasör oluşturulduğunu fark edin. Denetleyici IDE 'de açıktır.

![](adding-a-controller/_static/image4.png)

Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Denetleyici yöntemleri bir örnek olarak HTML dizesi döndürür. Denetleyici adlandırılır `HelloWorldController` ve ilk yöntem adlandırılır `Index` . Bir tarayıcıdan çağıralım. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcıda, &quot; &quot; Adres çubuğundaki yola HelloWorld ekleyin. (Örneğin, aşağıdaki çizimde, `http://localhost:1234/HelloWorld.` ) Tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca birkaç HTML döndürdüyordu ve!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan URL yönlendirme mantığı, çağrılacak kodu belirlemek için aşağıdaki gibi bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

*Uygulama \_ Başlangıç/routeconfig. cs* dosyasında yönlendirme biçimini ayarlarsınız.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

Uygulamayı çalıştırdığınızda ve herhangi bir URL kesimini sağlamadığınızda, varsayılan olarak "giriş" denetleyicisi ve Yukarıdaki kodun varsayılanlar bölümünde belirtilen "Dizin" eylem yöntemi olur.

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle */HelloWorld* sınıfla eşlenir `HelloWorldController` . URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `Index` sınıfın yönteminin yürütülmesine neden olur `HelloWorldController` . Yalnızca */HelloWorld* öğesine göz atabildiğimiz ve `Index` yöntemin varsayılan olarak kullanıldığı konusunda dikkat edin. Bunun nedeni, bir yöntemi `Index` açıkça belirtilmediyse bir denetleyicide çağrılacak olan varsayılan yöntemdir. URL segmentinin () üçüncü bölümü `Parameters` Rota verileri içindir. Bu öğreticide daha sonra rota verilerini inceleyeceğiz.

`http://localhost:xxxx/HelloWorld/Welcome` adresine gidin. `Welcome`Yöntemi çalışır ve &quot; Bu karşılama eylemi yöntemi olan dizeyi döndürür... &quot; . Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]` . Bu URL için denetleyici, `HelloWorld` ve `Welcome` eylem yöntemidir. `[Parameters]`URL 'nin bir bölümünü henüz kullanmadınız.

![](adding-a-controller/_static/image6.png)

URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott &amp; numtimes = 4*). `Welcome`Yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Kodun, `numTimes` söz konusu parametreye hiçbir değer geçirilmezse parametrenin varsayılan olarak 1 ' i belirtmesi gerektiğini belirtmek Için C# isteğe bağlı parametresi özelliğini kullandığını unutmayın.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> Güvenlik notumu: Yukarıdaki kod, uygulamayı kötü amaçlı girişten korumak için [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) kullanır (yani JavaScript). Daha fazla bilgi için bkz. [nasıl yapılır: DIZELERE HTML kodlaması uygulayarak bir Web uygulamasındaki betiklere karşı koruma](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).

 Uygulamanızı çalıştırın ve örnek URL 'ye ( `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` ) gidin. URL 'de ve için farklı değerler `name` deneyebilirsiniz `numtimes` . [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image7.png)

Yukarıdaki örnekte, URL segmenti ( `Parameters` ) kullanılmaz, `name` ve `numTimes` parametreleri [sorgu dizeleri](http://en.wikipedia.org/wiki/Query_string)olarak geçirilir. ? işareti (soru işareti) Yukarıdaki URL 'de bir ayırıcıdır ve sorgu dizeleri aşağıdaki gibi olur. &amp;Karakter Sorgu dizelerini ayırır.

Welcome metodunu aşağıdaki kodla değiştirin:

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

Uygulamayı çalıştırın ve aşağıdaki URL 'YI girin: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

Bu kez, üçüncü URL segmenti, `ID.` `Welcome` `ID` yöntemi içindeki URL belirtimiyle eşleşen bir parametreyi () içeren yol parametresiyle eşleştirildiği zaman `RegisterRoutes` .

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC uygulamalarında, parametreleri sorgu dizeleri olarak geçirmeden, parametreleri yönlendirme verileri (yukarıda ID ile yaptığımız gibi) olarak geçirmek daha tipik bir yoldur. Ayrıca, `name` `numtimes` URL 'ye yönlendirme verileri olarak hem hem de parametrelerini geçirmek için bir yol ekleyebilirsiniz. *App \_ Start\routeconfig.cs* dosyasına "Merhaba" yolunu ekleyin:

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

Uygulamayı çalıştırın ve konumuna gidin `/localhost:XXX/HelloWorld/Welcome/Scott/3` .

![](adding-a-controller/_static/image9.png)

Birçok MVC uygulaması için, varsayılan yol sorunsuz şekilde çalışıyor. Bu öğreticide daha sonra model cildi kullanarak veri geçireceğini öğrenirsiniz ve bunun için varsayılan yolu değiştirmeniz gerekmez.

Bu örneklerde, denetleyici &quot; &quot; MVC 'nin VC bölümünü yapıyor — yani, görünüm ve denetleyici çalışır. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Şimdi bunu nasıl yapadığımızda bakalım.

> [!div class="step-by-step"]
> [Önceki](getting-started.md) 
>  [Sonraki](adding-a-view.md)
