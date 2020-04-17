---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Jilet ve Göze batmaz JavaScript ile MVC 3 Uygulaması Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Kullanıcı Listesi örnek web uygulaması, Razor görünüm motorlarını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar basit olduğunu gösterir. Örnek uygulama s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542462"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor ve Unobtrusive JavaScript ile MVC 3 Uygulaması Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

> Kullanıcı Listesi örnek web uygulaması, Razor görünüm motorlarını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar basit olduğunu gösterir. Örnek uygulama, kullanıcıları oluşturma, görüntüleme, düzenleme ve silme gibi işlevleri içeren kurgusal bir Kullanıcı Listesi web sitesi oluşturmak için ASP.NET MVC sürüm 3 ve Visual Studio 2010 ile yeni Razor görünüm altyapısının nasıl kullanılacağını gösterir.
> 
> Bu öğretici, MVC 3 uygulaması ASP.NET Kullanıcı Listesi örneğini oluşturmak için atılan adımları açıklar. C# ve VB kaynak koduna sahip bir Visual Studio projesi bu konuya eşlik etmek için kullanılabilir: [İndir](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Bu öğretici hakkında sorularınız varsa, [MVC foruma](https://forums.asp.net/1146.aspx)gönderin.

## <a name="overview"></a>Genel Bakış

İnşa edeceğimiz uygulama basit bir kullanıcı listesi web sitesidir. Kullanıcılar kullanıcı bilgilerini girebilir, görüntüleyebilir ve güncelleyebilir.

![Örnek site](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

VB ve C# tamamlanan projeyi [buradan](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)indirebilirsiniz.

## <a name="creating-the-web-application"></a>Web Uygulamasını Oluşturma

Öğreticiyi başlatmak için Visual Studio 2010'u açın ve *mvc 3 Web Uygulaması* şablonu ASP.NET kullanarak yeni bir proje oluşturun. Uygulama &quot;Mvc3Razor&quot;adı .

[![Yeni MVC 3 projesi](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

Yeni **ASP.NET MVC 3 Project** iletişim kutusunda, **Internet Application'ı**seçin, Razor görünüm altyapısını seçin ve ardından **Tamam'ı**tıklatın.

![Yeni ASP.NET MVC 3 Proje iletişim kutusu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

Bu eğitimde ASP.NET üyelik sağlayıcısını kullanmaydığınız için oturum açma ve üyelikle ilişkili tüm dosyaları silebilirsiniz. **Çözüm Gezgini'nde,** aşağıdaki dosyaları ve dizinleri kaldırın:

- *Denetleyiciler\Hesap Kontrolörü*
- *Modeller\Hesap Modelleri*
- *Görünümler\Paylaşılan\\_LogOnPartial*
- *Görünümler\Hesap* (ve bu dizindeki tüm dosyalar)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em> \_Layout.cshtml</em> dosyasını düzenle ve giriş `<div>` devre `logindisplay` dışı&quot;bırakılan <em>&quot;</em>ileti ile adlandırılmış öğenin içindeki biçimlendirmeyi değiştirin. Aşağıdaki örnekte yeni biçimlendirme gösterilmektedir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Model Ekleme

**Çözüm Gezgini'nde,** *Modeller* klasörüne sağ tıklayın, **Ekle'yi**seçin ve ardından **Sınıf'ı**tıklatın.

![Yeni Kullanıcı Mdl sınıfı](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Sınıfı `UserModel`adlandırın. *UserModel* dosyasının içeriğini aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Sınıf `UserModel` kullanıcıları temsil eder. Sınıfın her [üyesi, DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanından [Gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelik ile açıklamalı. [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki öznitelikler, web uygulamaları için otomatik istemci ve sunucu tarafı doğrulaması sağlar.

Sınıfı `HomeController` açın ve `using` sınıflara `UserModel` erişebilmeniz `Users` için bir yönerge ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Bildirimden `HomeController` hemen sonra, aşağıdaki yorumu ve `Users` bir sınıfa başvuru ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Sınıf, `Users` bu öğreticide kullanacağınız basitleştirilmiş, bellek içi veri deposudur. Gerçek bir uygulamada, kullanıcı bilgilerini depolamak için bir veritabanı kullanırsınız. Dosyanın `HomeController` ilk birkaç satırı aşağıdaki örnekte gösterilir:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Uygulamayı, kullanıcı modelinin bir sonraki adımda iskele sihirbazı tarafından kullanılabileceğini oluşturun.

## <a name="creating-the-default-view"></a>Varsayılan Görünümü Oluşturma

Bir sonraki adım, kullanıcıları görüntülemek için bir eylem yöntemi ve görünüm eklemektir.

Varolan *Görünümler\Ana Sayfa\Dizin* dosyasını silin. Kullanıcıları görüntülemek için yeni bir *Dizin* dosyası oluşturursunuz.

`HomeController` Sınıfta, `Index` yöntemin içeriğini aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Yöntemin `Index` içine sağ tıklayın ve ardından **Görünüm Ekle'yi**tıklatın.

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Güçlü **bir şekilde yazılmış görünüm** oluştur seçeneğini seçin. **Veri sınıfı görüntüle**için **Mvc3Razor.Models.UserModel'i**seçin. (Veri **sınıfı görünümü** kutusunda **Mvc3Razor.Models.UserModel'i** görmüyorsanız, projeyi oluşturmanız gerekir.) Görünüm motorunun **Razor**olarak ayarlandıklarına emin olun. İçeriği **Listeye** **Göre'ye** Ayarla ve Ardından **Ekle'yi**tıklatın.

![Dizin Görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Yeni görünüm, `Index` görünüme geçirilen kullanıcı verilerini otomatik olarak kalıba biçer. Yeni oluşturulan *Görünümler\Ana Sayfa\Dizin* dosyasını inceleyin. **Yeni Oluştur**, **Düzenle,** **Ayrıntıları**düzenle ve **sil** bağlantıları çalışmıyor, ancak sayfanın geri kalanı işlevsel. Sayfayı çalıştırın. Kullanıcıların listesini görürsünüz.

![Dizin Sayfası](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

*Index.cshtml* dosyasını açın `ActionLink` ve **Düzenle**, **Ayrıntılar**ve **Sil** için biçimlendirmeyi aşağıdaki kodla değiştirin:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Kullanıcı adı, **Düzenle**, **Ayrıntılar**ve **Sil** bağlantılarında seçili kaydı bulmak için kimlik olarak kullanılır.

## <a name="creating-the-details-view"></a>Ayrıntıları Görüntüleme

Bir sonraki adım, `Details` kullanıcı ayrıntılarını görüntülemek için bir eylem yöntemi ve görünüm eklemektir.

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Ev denetleyicisine aşağıdaki `Details` yöntemi ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Yöntemin `Details` içine sağ tıklayın ve ardından <strong>Görünüm Ekle'yi</strong>seçin. <strong>Veri sınıfı görüntükutusunun</strong> <strong>Mvc3Razor.Models.UserModel</strong>içerdiğini<em>doğrulayın.</em> İçeriği <strong>Ayrıntılara</strong> <strong>Göre Ayarla</strong> ve <strong>Ardından Ekle'yi</strong>tıklatın.

![Ayrıntıları görünüm ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Uygulamayı çalıştırın ve ayrıntılar bağlantısını seçin. Otomatik iskele modeldeki her özelliği gösterir.

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Görünüm Edit Oluşturma

Ev denetleyicisine aşağıdaki `Edit` yöntemi ekleyin.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Önceki adımlardaki gibi bir görünüm ekleyin, ancak **Görünümü** **Edit'e**ayarlayın.

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Uygulamayı çalıştırın ve kullanıcılardan birinin adını ve soyadını edin. Sınıfa uygulanan `DataAnnotation` kısıtlamaları ihlal ederseniz, formu gönderdiğiniz zaman sunucu kodu tarafından üretilen doğrulama hatalarını görürsünüz. `UserModel` Örneğin, formu gönderdiğiniz zaman &quot;ilk&quot; &quot;ad&quot;Ann'i A ile değiştirirseniz, formda aşağıdaki hata görüntülenir:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

Bu öğreticide, kullanıcı adını birincil anahtar olarak ele alıyoruz. Bu nedenle, kullanıcı adı özelliği değiştirilemez. *Edit.cshtml* dosyasında, deyimden `Html.BeginForm` hemen sonra, kullanıcı adını gizli bir alan olarak ayarlayın. Bu, özelliğin modelde geçirilmesine neden olur. Aşağıdaki kod parçası deyimin `Hidden` yerleşimini gösterir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Kullanıcı `TextBoxFor` adı `ValidationMessageFor` için işaretleme ve işaretlemeyi bir `DisplayFor` çağrıyla değiştirin. Yöntem, `DisplayFor` özelliği salt okunur öğe olarak görüntüler. Aşağıdaki örnek, tamamlanan biçimlendirmeyi gösterir. Orijinal `TextBoxFor` ve `ValidationMessageFor` aramalar Razor başlangıç-yorum ve son yorum karakterleri`@* *@`ile yorumlanır ( )

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>İstemci Tarafı Doğrulamayı Etkinleştirme

mvc 3 ASP.NET'te istemci tarafı doğrulamayı etkinleştirmek için iki bayrak ayarlamanız ve üç JavaScript dosyası eklemeniz gerekir.

Uygulamanın *Web.config* dosyasını açın. `that ClientValidationEnabled` Doğrulayın `UnobtrusiveJavaScriptEnabled` ve uygulama ayarlarında doğru ayarlanır. Root *Web.config* dosyasından aşağıdaki parça doğru ayarları gösterir:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Doğru `UnobtrusiveJavaScriptEnabled` ayar, göze batmaz Ajax ve göze batmaz istemci doğrulaması sağlar. Göze çarpmadan doğrulama kullandığınızda, doğrulama kuralları HTML5 özniteliklerine dönüştürülr. HTML5 öznitelik adları yalnızca küçük harflerden, sayılardan ve tirelerden oluşabilir.

Doğru `ClientValidationEnabled` ayar istemci tarafı doğrulamasağlar. Bu anahtarları uygulama *Web.config* dosyasında ayarlayarak, tüm uygulama için istemci doğrulamasını ve göze batmaz JavaScript'i etkinleştirmiş olursunuz. Ayrıca, aşağıdaki kodu kullanarak bu ayarları tek tek görünümlerde veya denetleyici yöntemlerinde etkinleştirebilir veya devre dışı kullanabilirsiniz:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Ayrıca, işlenen görünüme birkaç JavaScript dosyası eklemeniz gerekir. JavaScript'i tüm görünümlere eklemenin kolay bir yolu, bunları *Görünümler\Paylaşılan\\_Layout.cshtml* dosyasına eklemektir. Layout.cshtml dosyasının `<head>` öğesini aşağıdaki kodla değiştirin: * \_*

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

İlk iki jQuery komut dosyası Microsoft Ajax İçerik Dağıtım Ağı (CDN) tarafından barındırılır. Microsoft Ajax CDN'den yararlanarak, uygulamalarınızın ilk hit performansını önemli ölçüde artırabilirsiniz.

Uygulamayı çalıştırın ve bir edit bağlantısını tıklatın. Sayfanın kaynağını tarayıcıda görüntüleyin. Tarayıcı kaynağı formun `data-val` birçok özniteliklerini gösterir (veri doğrulama için). İstemci doğrulama ve göze batmayan JavaScript etkinleştirildiğinde, istemci doğrulama kuralına `data-val="true"` sahip giriş alanları, göze batmayan istemci doğrulaması tetiklemek için öznitelik içerir. Örneğin, modeldeki `City` alan [Gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelik ile dekore edilmiştir ve bu da aşağıdaki örnekte gösterilen HTML ile sonuçlanır:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Her istemci doğrulama kuralı için, formu `data-val-rulename="message"`olan bir öznitelik eklenir. Daha `City` önce gösterilen alan örneğini kullanarak, gerekli istemci `data-val-required` doğrulama kuralı &quot;özniteliği oluşturur&quot;ve Şehir alanının gerekli olduğu ileti. Uygulamayı çalıştırın, kullanıcılardan birini edin `City` ve alanı temizleyin. Alanın dışına çıktığınızda, istemci tarafı doğrulama hatası iletisi görürsünüz.

![Şehir gerekli](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Benzer şekilde, istemci doğrulama kuralındaki her parametre için, formu `data-val-rulename-paramname=paramvalue`olan bir öznitelik eklenir. Örneğin, `FirstName` özellik [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliği ile açıklamalı ve en az 3 uzunluk ve 8 maksimum uzunluk belirtir. Adlı `length` veri doğrulama kuralı parametre `max` adı ve parametre değeri 8 vardır. Aşağıdaki, kullanıcılardan birini yaptığınızda `FirstName` alan için oluşturulan HTML'yi gösterir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Göze batmaz istemci doğrulaması hakkında daha fazla bilgi için, Brad Wilson'ın blogunda [ASP.NET MVC 3'teki Unobtrusive Müşteri Doğrulama](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) girişine bakın.

> [!NOTE]
> MVC 3 BetaASP.NET bazen istemci tarafı doğrulamayı başlatmak için formu göndermeniz gerekir. Bu son sürüm için değiştirilebilir.

## <a name="creating-the-create-view"></a>Görünüm Oluştur

Bir sonraki adım, `Create` kullanıcının yeni bir kullanıcı oluşturmasını sağlamak için bir eylem yöntemi ve görünüm eklemektir. Ev denetleyicisine aşağıdaki `Create` yöntemi ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Önceki adımlardaki gibi bir görünüm ekleyin, ancak **Görünümü** **Oluştur'a**ayarlayın.

![Görünüm Oluşturma](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Uygulamayı çalıştırın, **Oluştur** bağlantısını seçin ve yeni bir kullanıcı ekleyin. Yöntem `Create` otomatik olarak istemci tarafı ve sunucu tarafı doğrulama yararlanır. Ben X &quot;&quot;gibi beyaz alan içeren bir kullanıcı adı girmeyi deneyin. Kullanıcı adı alanının dışına çıktığınızda, istemci tarafı doğrulama`White space is not allowed`hatası ( ) görüntülenir.

## <a name="add-the-delete-method"></a>Sil yöntemini ekle

Öğreticiyi tamamlamak için ev `Delete` denetleyicisine aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Önceki `Delete` adımlardaki gibi bir görünüm ekleyin, **Içeriği** **Sil'e**ayarlayın.

![Görünümü Sil](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Şimdi doğrulama ile basit ama tamamen işlevsel ASP.NET MVC 3 uygulama var.
