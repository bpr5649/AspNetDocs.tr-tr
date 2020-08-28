---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045175"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Bir Denetleyiciden Modelinizin Verilerine Erişme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu bölümde, yeni bir `MoviesController` sınıf oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen bir kod yazacak.

Sonraki adıma geçmeden önce **uygulamayı derleyin** . Uygulamayı dermezseniz, denetleyici eklenirken bir hata alırsınız.

Çözüm Gezgini, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

**Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici**' ye tıklayın ve ardından **Ekle**' ye tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Model sınıfı için **filmi (MvcMovie. modeller)** seçin.
- Veri bağlamı sınıfı için **Moviedbcontext (MvcMovie. modeller)** öğesini seçin.
- Denetleyici adı için **MoviesController**girin.

  Aşağıdaki görüntüde tamamlanan iletişim kutusu gösterilmektedir.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**Ekle**'ye tıklayın. (Bir hata alırsanız, denetleyiciyi eklemeye başlamadan önce uygulamayı derlemeniz olasıdır.) Visual Studio aşağıdaki dosyaları ve klasörleri oluşturur:

- *Controllers* klasöründeki *bir MoviesController.cs* dosyası.
- *Views\filmler* klasörü.
- Yeni *Views\filmlerini* klasöründeki *. cshtml, delete. cshtml, details. cshtml, Edit. cshtml*ve *Index. cshtml* oluşturun.

Visual Studio [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini sizin için otomatik olarak oluşturdu (CRUD eylem yöntemlerinin ve görünümlerinin otomatik olarak oluşturulması, yapı iskelesi olarak bilinir). Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.

Uygulamayı çalıştırın ve **MVC film** bağlantısına tıklayın (veya `Movies` TARAYıCıNıN adres çubuğundaki URL 'ye */filmler* ekleyerek denetleyiciye gidin). Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *App \_ Start\routeconfig.cs* dosyasında tanımlanan), tarayıcı isteği `http://localhost:xxxxx/Movies` `Index` denetleyicinin varsayılan eylem yöntemine yönlendirilir `Movies` . Diğer bir deyişle, tarayıcı isteği `http://localhost:xxxxx/Movies` tarayıcı isteğiyle aynı şekilde aynıdır `http://localhost:xxxxx/Movies/Index` . Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Film oluşturma

**Yeni oluştur** bağlantısını seçin. Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Fiyat alanına ondalık nokta veya virgül giremeyebilirsiniz. &quot;Ondalık bir nokta ve ABD İngilizcesi olmayan tarih biçimleri için virgül (,) kullanan İngilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için &quot; , *globalize.js* ve belirli *kültürleri/globalize.cultures.js* dosyanızı (Kimden [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve kullanılacak JavaScript 'i dahil etmeniz gerekir `Globalize.parseFloat` . Bunu bir sonraki öğreticide nasıl yapacağım. Şimdilik, yalnızca 10 gibi tüm sayıları girmeniz yeterlidir.

**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar. Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Birkaç film girişi oluşturun. Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.

## <a name="examining-the-generated-code"></a>Oluşturulan kodu İnceleme

*Controllers\MoviesController.cs* dosyasını açın ve oluşturulan `Index` yöntemi inceleyin. Aşağıdaki yöntemi içeren film denetleyicisinin bir bölümü `Index` aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Denetleyiciye yönelik bir istek `Movies` tablodaki tüm girişleri döndürür `Movies` ve sonra sonuçları `Index` görünüme geçirir. Sınıfından aşağıdaki satır `MoviesController` , daha önce açıklandığı gibi bir film veritabanı bağlamı oluşturur. Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü

Bu öğreticide daha önce, bir denetleyicinin nesneyi kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz `ViewBag` . , `ViewBag` Bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.

MVC Ayrıca, *türü kesin* belirlenmiş nesneleri bir görünüm şablonuna geçirebilme olanağı da sağlar. Bu kesin türü belirtilmiş yaklaşım, Visual Studio düzenleyicisinde kodunuzun ve daha zengin [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 'in derleme zamanı denetimini daha iyi bir şekilde sunar. Visual Studio 'daki scafkatlama mekanizması, bu yaklaşımı (yani, *türü kesin* belirlenmiş bir model geçirerek), `MoviesController` Yöntem ve görünümleri oluştururken sınıfla ve görüntüleme şablonlarına kullandı.

*Controllers\MoviesController.cs* dosyasında, oluşturulan `Details` yöntemi inceleyin. `Details`Yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`Parametre genellikle rota verileri olarak geçirilir. Örneğin, `http://localhost:1234/movies/details/1` denetleyiciyi film denetleyicisine, eylemini öğesine ve ile 1 ' e ayarlar `details` `id` . Ayrıca kimliği bir sorgu dizesi ile aşağıdaki gibi geçirebilirsiniz:

`http://localhost:1234/movies/details?id=1`

Bir `Movie` bulunursa, modelin bir örneği `Movie` `Details` görünüme geçirilir:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

*Views\Movies\Details.cshtml* dosyasının içeriğini inceleyin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

`@model`Görünüm şablonu dosyasının üst kısmına bir ifade ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz. Film denetleyicisini oluştururken, Visual Studio `@model` *details. cshtml* dosyasının en üstüne aşağıdaki ifadeyi otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Bu `@model` yönerge, kesin olarak belirlenmiş bir nesne kullanarak denetleyicinin görünüme geçirildiği filme erişmenizi sağlar `Model` . Örneğin, *details. cshtml* şablonunda, kod her bir film alanını, `DisplayNameFor` türü kesin belirlenmiş nesne olan HTML Yardımcıları [için ve displayto](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) öğesine geçirir `Model` . `Create`Ve `Edit` yöntemleri ve Görünüm şablonları da bir film modeli nesnesi iletir.

*Index. cshtml* görünüm şablonunu ve `Index` *MoviesController.cs* dosyasındaki yöntemi inceleyin. [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` Eylem yönteminde yardımcı yöntemini çağırdığında kodun bir nesne nasıl oluşturduğunu fark edin `Index` . Kod daha sonra bu `Movies` listeyi `Index` eylem yönteminden görünüme geçirir:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

Film denetleyicisini oluştururken, Visual Studio `@model` *Index. cshtml* dosyasının en üstüne aşağıdaki ifadeyi otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Bu `@model` yönerge, kesin olarak belirlenmiş bir nesne kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar `Model` . Örneğin, *Index. cshtml* şablonunda, kod, `foreach` türü kesin belirlenmiş nesne üzerinde bir ekstre yaparak filmlerle döngü yapılır `Model` :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model`Nesne türü kesin belirlenmiş olduğundan (bir nesne olarak `IEnumerable<Movie>` ), `item` döngüdeki her bir nesne olarak yazılır `Movie` . Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server Yerel Veritabanı ile çalışma

Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin `Movies` henüz mevcut olmayan bir veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First. *Uygulamanın \_ veri* klasörüne bakarak oluşturulduğunu doğrulayabilirsiniz. *Filmler. mdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama \_ verileri* klasörünü genişletin.

![](accessing-your-models-data-from-a-controller/_static/image9.png)

*Film. mdf* ' ye çift TıKLAYARAK **Sunucu Gezgini**'Ni açın ve ardından Filmler tablosunu görmek için **Tablolar** klasörünü genişletin. ID ' ın yanındaki anahtar simgesine göz önünde. Varsayılan olarak, EF, birincil anahtar adlı bir özellik oluşturacak. EF ve MVC hakkında daha fazla bilgi için, bkz. Tom Dykstra 'ın [MVC ve EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)hakkında harika bir öğreticisi.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Tabloya sağ tıklayıp `Movies` **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Tabloya sağ tıklayıp tablo `Movies` **tanımını aç** ' ı seçerek Entity Framework Code First sizin için oluşturduğu tablo yapısını görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Tablo şemasının, `Movies` `Movie` daha önce oluşturduğunuz sınıfa nasıl eşlendiğini unutmayın. Entity Framework Code First, bu şemayı sınıfınıza göre sizin için otomatik olarak oluşturdu `Movie` .

İşiniz bittiğinde, *Moviedbcontext* ' i sağ tıklatıp **Bağlantıyı kapat**' ı seçerek bağlantıyı kapatın. (Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Artık veri görüntüleme, düzenleme, güncelleştirme ve silme için bir veritabanınız ve sayfalarınız vardır. Sonraki öğreticide, yapı iskelesi kodunun geri kalanını inceleyeceğiz ve `SearchIndex` `SearchIndex` Bu veritabanında film aramanıza olanak tanıyan bir yöntem ve bir görünüm ekleyeceğiz. MVC ile Entity Framework kullanma hakkında daha fazla bilgi için, bkz. [ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Önceki](creating-a-connection-string.md) 
>  [Sonraki](examining-the-edit-methods-and-edit-view.md)
