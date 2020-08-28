---
uid: mvc/overview/getting-started/introduction/adding-validation
title: Doğrulama ekleniyor | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044356"
---
# <a name="adding-validation"></a>Doğrulama Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu bölümde, modele doğrulama mantığı ekleyeceksiniz `Movie` ve bir kullanıcının uygulamayı kullanarak bir filmi oluşturma veya düzenleme girişiminde bulunduğu her seferinde doğrulama kurallarının uygulanmasını sağlayabilirsiniz.

## <a name="keeping-things-dry"></a>Işleri güncel tutma

ASP.NET MVC 'nin temel tasarımdan biri [kuru](http://en.wikipedia.org/wiki/Don't_repeat_yourself) ( &quot; kendini tekrarlama &quot; ). ASP.NET MVC, işlevselliği veya davranışı yalnızca bir kez belirtmenizi ve sonra bir uygulamada her yerde yansıtıldığını teşvik eder. Bu, yazmanız gereken kod miktarını azaltır ve daha az hata yazmanızı ve bakımını daha kolay hale getirir.

ASP.NET MVC ve Entity Framework Code First tarafından sağlanan doğrulama desteği, işlem içindeki kuru ilkeye yönelik harika bir örnektir. Doğrulama kurallarını tek bir yerde (model sınıfında) bildirimli olarak belirtebilir ve kurallar uygulamada her yerde zorlanır.

Film uygulamasındaki bu doğrulama desteğinden nasıl yararlanabilmenizi görelim.

## <a name="adding-validation-rules-to-the-movie-model"></a>Film modeline doğrulama kuralları ekleme

Sınıfa bazı doğrulama mantığı ekleyerek başlayacaksınız `Movie` .

*Movie.cs* dosyasını açın. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)Ad alanının içermediği fark `System.Web` . Dataaçıklamalarda, herhangi bir sınıfa veya özelliğe bildirimli olarak uygulayabileceğiniz yerleşik bir doğrulama öznitelikleri kümesi sağlar. (Ayrıca, biçimlendirme ile yardımcı olan ve herhangi bir doğrulama sağlamayan [veri türü](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) gibi biçimlendirme özniteliklerini de içerir.)

Şimdi `Movie` yerleşik [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) , [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)ve doğrulama özniteliklerinden yararlanmak için sınıfı güncelleştirin [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) . `Movie`Sınıfını aşağıdaki ile değiştirin:

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

[`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)Özniteliği, dizenin uzunluk üst sınırını ayarlar ve bu sınırlamayı veritabanında belirler, bu nedenle veritabanı şeması değişir. **Sunucu Gezgini** 'nde **filmler** tablosuna sağ tıklayın ve **tablo tanımını aç**' a tıklayın:

![](adding-validation/_static/image1.png)

Yukarıdaki görüntüde, tüm dize alanlarının [nvarchar (max)](https://technet.microsoft.com/library/ms186939.aspx)olarak ayarlandığını görebilirsiniz. Şemayı güncelleştirmek için geçişleri kullanacağız. Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutları girin:

[!code-console[Main](adding-validation/samples/sample2.cmd)]

Bu komut tamamlandığında, Visual Studio, `DbMigration` belirtilen ada sahip yeni türetilmiş sınıfı tanımlayan sınıf dosyasını ( `DataAnnotations` ) açar ve `Up` yönteminde şema kısıtlamalarını güncelleştiren kodu görebilirsiniz:

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

`Genre`Alan artık null yapılabilir değil (yani bir değer girmeniz gerekir). `Rating`Alan en fazla 5 uzunluğuna sahiptir ve `Title` en fazla 60 uzunluğuna sahiptir. En az 3 uzunluğu `Title` ve üzerindeki Aralık `Price` şema değişikliği oluşturmadı.

Film şemasını inceleyin:

![](adding-validation/_static/image2.png)

Dize alanları yeni uzunluk sınırlarını gösterir ve `Genre` artık null yapılabilir olarak işaretlenmiyor.

Doğrulama öznitelikleri, uygulanan model özellikleri üzerinde zorlamak istediğiniz davranışı belirtir. `Required`Ve `MinimumLength` öznitelikleri bir özelliğin bir değere sahip olması gerektiğini belirtir; ancak hiçbir şey, bir kullanıcının bu doğrulamayı karşılamak için boşluk girmesini engeller. [Cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliği, hangi karakterlerin giriş yapabileceğini sınırlamak için kullanılır. Yukarıdaki kodda `Genre` ve `Rating` yalnızca harfler kullanılmalıdır (boşluk, sayı ve özel karakterlere izin verilmez). [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)Özniteliği bir değeri belirtilen bir Aralık içinde kısıtlar. `StringLength`Özniteliği, bir dize özelliğinin en büyük uzunluğunu ve isteğe bağlı olarak en düşük uzunluğunu ayarlamanıza olanak sağlar. Değer türleri (gibi `decimal, int, float, DateTime` ), doğal olarak gereklidir ve özniteliğe gerek kalmaz `Required` .

Code First, bir model sınıfında belirttiğiniz doğrulama kurallarının, uygulama değişiklikleri veritabanına kaydedilmeden önce uygulanmasını sağlar. Örneğin, aşağıdaki kod, yöntemi çağrıldığında bir [Dbentityvalidationexception](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) özel durumu oluşturur `SaveChanges` , çünkü gerekli bazı `Movie` özellik değerleri eksik.

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

Yukarıdaki kod aşağıdaki özel durumu oluşturur:

*Bir veya daha fazla varlık için doğrulama başarısız oldu. Daha fazla ayrıntı için bkz. ' EntityValidationErrors ' özelliği.*

Doğrulama kurallarının .NET Framework tarafından otomatik olarak uygulanmasını sağlamak, uygulamanızın daha sağlam olmasına yardımcı olur. Ayrıca, bir şeyi doğrulamayı unutmanızı ve veritabanına yanlışlıkla veri vermemesini de sağlar.

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 'de doğrulama hatası Kullanıcı arabirimi

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin.

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Formu, bazı geçersiz değerlerle doldurun. JQuery istemci tarafı doğrulaması hatayı algıladıktan hemen sonra bir hata iletisi görüntüler.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> ondalık bir nokta için virgül (",") kullanan Ingilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için, bu öğreticide daha önce açıklandığı gibi NuGet globalize dahil etmeniz gerekir.

Formun, geçersiz veriler içeren metin kutularını vurgulamak için otomatik olarak kırmızı kenarlık rengini nasıl kullandığını ve her birinin yanında uygun bir doğrulama hata iletisi oluşturmuş olduğunu unutmayın. Hatalar hem istemci tarafında (JavaScript ve jQuery kullanılarak) hem de sunucu tarafında (kullanıcının JavaScript devre dışı bırakılmış olması durumunda) zorlanır.

Gerçek bir avantaj, `MoviesController` Bu doğrulama kullanıcı arabirimini etkinleştirmek için sınıfında veya *Create. cshtml* görünümündeki tek bir kod satırını değiştirmeniz gerekmez. Bu öğreticide daha önce oluşturduğunuz denetleyici ve görünümler, model sınıfının özelliklerinde doğrulama özniteliklerini kullanarak belirttiğiniz doğrulama kurallarını otomatik olarak çekti `Movie` . Eylem yöntemini kullanarak test doğrulama `Edit` ve aynı doğrulama uygulandı.

Form verileri, istemci tarafı doğrulama hatası kalmayana kadar sunucuya gönderilmez. Bunu, [Fiddler aracını](http://fiddler2.com/fiddler2/)veya IE [F12 GELIŞTIRICI araçlarını](https://msdn.microsoft.com/ie/aa740478)kullanarak http post yöntemine bir kesme noktası koyarak doğrulayabilirsiniz.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Oluşturma görüntüleme ve eylem oluşturma yönteminde doğrulama nasıl gerçekleşir

Doğrulama Kullanıcı arabiriminin denetleyici veya görünümlerde kodda herhangi bir güncelleştirme yapmadan nasıl oluşturulduğunu merak edebilirsiniz. Sonraki liste, `Create` sınıftaki yöntemlerin nasıl `MovieController` göründüğünü gösterir. Bunlar, bu öğreticide daha önce oluşturduğunuz şekilde değiştirilmez.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

İlk (HTTP GET) `Create` eylem yöntemi Ilk oluşturma formunu görüntüler. İkinci ( `[HttpPost]` ) sürüm, form gönderisini işler. İkinci `Create` Yöntem ( `HttpPost` sürüm), `ModelState.IsValid` filmin herhangi bir doğrulama hatası olup olmadığını denetler. Bu özelliğin alınması, nesnesine uygulanmış olan tüm doğrulama özniteliklerini değerlendirir. Nesne doğrulama hatalarıyla karşılaşırsanız, `Create` yöntemi formu yeniden görüntüler. Hata yoksa, yöntemi yeni filmi veritabanına kaydeder. Film örneğimizde, **istemci tarafında algılanan doğrulama hataları olduğunda form sunucuya nakledilmez; ikinci** `Create` **Yöntem hiçbir zaman çağrılmaz**. Tarayıcınızda JavaScript 'i devre dışı bırakırsanız, istemci doğrulaması devre dışıdır ve HTTP POST `Create` yöntemi, `ModelState.IsValid` filmin herhangi bir doğrulama hatası olup olmadığını kontrol etmek için alır.

Yönteminde bir kesme noktası ayarlayabilir `HttpPost Create` ve yöntemin hiçbir zaman çağrılmadığını doğrulayabilirsiniz, doğrulama hataları algılandığında istemci tarafı doğrulaması form verilerini göndermez. Tarayıcınızda JavaScript 'i devre dışı bırakır, ardından formu hatalarla gönderirseniz, kesme noktası isabet eder. JavaScript olmadan tam doğrulama almaya devam edersiniz. Aşağıdaki görüntüde, Internet Explorer 'da JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

Aşağıdaki görüntüde, FireFox tarayıcısında JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation/_static/image7.png)

Aşağıdaki görüntüde, Chrome tarayıcısında JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation/_static/image8.png)

Öğreticide daha önce iskele aldığınız *Create. cshtml* görünüm şablonu aşağıda verilmiştir. İlk formu görüntülemek ve bir hata durumunda onu yeniden görüntülemek için yukarıda gösterilen eylem yöntemleri tarafından kullanılır.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

Kodun `Html.EditorFor` `<input>` her bir özellik için öğesini çıkarmak üzere bir yardımcı kullanma şeklini görürsünüz `Movie` . Bu yardımcının yanında yardımcı yöntemine yapılan bir çağrıdır `Html.ValidationMessageFor` . Bu iki yardımcı yöntem, denetleyici tarafından görünüme geçirilen model nesnesiyle (Bu durumda bir `Movie` nesne) çalışır. Model üzerinde belirtilen doğrulama özniteliklerini otomatik olarak arar ve hata iletilerini uygun şekilde görüntüler.

Bu yaklaşım ne kadar iyi bir şeydir, denetleyicinin ne de `Create` Görünüm şablonu zorlanmakta olan gerçek doğrulama kuralları veya görüntülenen belirli hata iletileri hakkında herhangi bir şeyi bilmez. Doğrulama kuralları ve hata dizeleri yalnızca `Movie` sınıfında belirtilmiştir. Bu aynı doğrulama kuralları, bir `Edit` görünüme ve modelinizi düzenleyebilecek oluşturabileceğiniz diğer tüm görünümler şablonlarına otomatik olarak uygulanır.

Daha sonra doğrulama mantığını değiştirmek istiyorsanız, modele doğrulama öznitelikleri ekleyerek tam olarak bir yerde bunu yapabilirsiniz (Bu örnekte, `movie` sınıfı). Kuralların nasıl zorlandığından, uygulamanın farklı bölümlerinin tutarsız olması konusunda endişelenmeniz gerekmez; tüm doğrulama mantığı tek bir yerde tanımlanır ve her yerde kullanılır. Bu, kodun temiz kalmasını sağlar ve bakımını ve gelişmesini kolaylaştırır. Ayrıca, *kurulama* ilkesini tam olarak sunabileceksiniz anlamına gelir.

## <a name="using-datatype-attributes"></a>DataType özniteliklerini kullanma

*Movie.cs* dosyasını açın ve `Movie` sınıfını inceleyin. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)Ad alanı, yerleşik doğrulama öznitelikleri kümesine ek olarak biçimlendirme öznitelikleri sağlar. [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)Yayın tarihine ve fiyat alanlarına bir numaralandırma değeri zaten uyguladık. Aşağıdaki kod, `ReleaseDate` `Price` uygun özniteliğiyle ve özelliklerini gösterir [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) .

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri yalnızca görünüm altyapısının verileri biçimlendirmek için ipuçları sağlar (ve `<a>` URL 'ler ve `<a href="mailto:EmailAddress.com">` e-posta için gibi öznitelikleri sağlayın. Verilerin biçimini doğrulamak için [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliğini kullanabilirsiniz. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, veritabanı iç türünden daha özel bir veri türü belirtmek için kullanılır, bunlar doğrulama öznitelikleri ***değildir*** . Bu durumda, tarihi ve saati değil yalnızca tarihi izlemek istiyoruz. Veri [türü numaralandırması](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , *Tarih, saat, PhoneNumber, para birimi, emaadresi* ve daha fazlası gibi birçok veri türü sağlar. `DataType`Özniteliği Ayrıca uygulamanın türe özgü özellikleri otomatik olarak sağlamasını da sağlayabilir. Örneğin, `mailto:` [DataType. emaadresi](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)için bir bağlantı oluşturulabilir ve [HTML5](http://html5.org/)'ı destekleyen tarayıcılarda [DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) için bir tarih seçici sağlanmış olabilir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri HTML 5 tarayıcısının ANLAYABILMESI için HTML 5 [veri](http://ejohn.org/blog/html-5-data-attributes/) (bir *veri Dash*) öznitelikleri yayar. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri herhangi bir doğrulama sağlamaz.

`DataType.Date` görüntülenen tarihin biçimini belirtmez. Varsayılan olarak, veri alanı sunucunun [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)öğesine göre varsayılan biçimlere göre görüntülenir.

`DisplayFormat`Öznitelik, tarih biçimini açıkça belirtmek için kullanılır:

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

`ApplyFormatInEditMode`Ayar, bir metin kutusunda değer görüntülenmek üzere görüntülendiğinde belirtilen biçimlendirmenin de uygulanacağını belirtir. (Örneğin, para birimi değerleri için, metin kutusundaki para birimi sembolünü, düzenlenebilir bir şekilde istemeyebilirsiniz.)

[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini kendisi kullanabilirsiniz, ancak aynı zamanda [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliğini de kullanmak iyi bir fikir olabilir. `DataType`Özniteliği, bir ekranda nasıl işlenirim aksine, verilerin *semantiğini* sunar ve aşağıdaki avantajları sağlar `DisplayFormat` :

- Tarayıcı HTML5 özelliklerini etkinleştirebilir (örneğin, bir Takvim denetimini, yerel ayara uygun para birimi sembolünü, e-posta bağlantılarını vb. göstermek için).
- Varsayılan olarak tarayıcı, verileri [yerel ayarınızı](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)temel alarak doğru biçimi kullanarak işleyebilir.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, verileri işlemek için doğru alan şablonunu seçmek üzere MVC 'yi etkinleştirebilir (kendisi tarafından kullanılıyorsa [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , dize şablonunu kullanır). Daha fazla bilgi için bkz. atacan Solson 'ın [ASP.NET MVC 2 şablonları](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (MVC 2 için yazılmış olsa da, bu makale hala ASP.NET MVC 'nin geçerli sürümü için geçerlidir.)

`DataType`Özniteliğini bir tarih alanı ile birlikte kullanıyorsanız, `DisplayFormat` alanın Chrome tarayıcılarında doğru şekilde işlediğinden emin olmak için özniteliği de belirtmeniz gerekir. Daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)bakın.

> [!NOTE]
> jQuery doğrulaması, [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) özniteliği ve [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)ile birlikte çalışmaz. Örneğin, aşağıdaki kod, tarih belirtilen aralıkta olduğunda bile her zaman bir istemci tarafı doğrulama hatası görüntüler:
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> [Aralık](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) özniteliğini [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)ile kullanmak için jQuery Tarih doğrulamasını devre dışı bırakmanız gerekir. Modellerinizde sabit tarihleri derlemek genellikle iyi bir uygulamadır, bu yüzden [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) özniteliği ve [Tarih saat](https://msdn.microsoft.com/library/system.datetime.aspx) kullanılması önerilmez.

Aşağıdaki kod, öznitelikleri tek bir satırda birleştirmeyi gösterir:

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

Serinin bir sonraki bölümünde, uygulamayı gözden geçireceğiz ve otomatik olarak oluşturulan `Details` ve metotlarda bazı geliştirmeler yaparsınız `Delete` .

> [!div class="step-by-step"]
> [Önceki](adding-a-new-field.md) 
>  [Sonraki](examining-the-details-and-delete-methods.md)
