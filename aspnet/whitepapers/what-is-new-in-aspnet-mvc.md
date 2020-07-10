---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2 ' deki yenilikler | Microsoft Docs
author: rick-anderson
description: Bu belge, ASP.NET MVC 2 ' de tanıtılan yeni özellikleri ve geliştirmeleri açıklamaktadır. Bu belge indirileceği için de kullanılabilir.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: 1a0a29241d8afecd295b11013b27621b21c9ed52
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162727"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2 Sürümündeki Yenilikler

> Bu belge, ASP.NET MVC 2 ' de tanıtılan yeni özellikleri ve geliştirmeleri açıklamaktadır. Bu belge [Indirileceği](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf) için de kullanılabilir

[Giriş](#_TOC1)   
[ASP.NET MVC 1,0 projesini ASP.NET MVC 2 ' ye yükseltme](#_TOC2)   
[Yeni özellikler](#_TOC3)   
[Şablonlu yardımcılar](#_TOC3_1)   
[Alanları](#_TOC3_2)   
[Zaman uyumsuz denetleyiciler için destek](#_TOC3_3)   
[Işlem yöntemi parametrelerinde DefaultValueAttribute desteği](#_TOC3_4)   
[Model ciltleri ile Ikili verileri bağlama desteği](#_TOC3_5)   
[ModelMetadata ve ModelMetadataProvider sınıfları](#_TOC3_6)   
[Dataek açıklama öznitelikleri için destek](#_TOC3_7)   
[Model doğrulayıcı sağlayıcıları](#_TOC3_8)   
[İstemci tarafı doğrulaması](#_TOC3_9)   
[Visual Studio 2010 için yeni kod parçacıkları](#_TOC3_10)   
[Yeni RequireHttpsAttribute eylem filtresi](#_TOC3_11)   
[HTTP yöntemi fiilini geçersiz kılma](#_TOC3_12)   
[Şablonlu Yardımcılar için yeni HiddenInputAttribute sınıfı](#_TOC3_13)   
[HTML. ValidationSummary yardımcı yöntemi model düzeyi hataları gösterebilir](#_TOC3_14)   
[Visual Studio 'Daki T4 şablonları .NET Framework](#_TOC3_15)[API 'si geliştirmelerinden](#_TOC4) oluşan hedef sürüme özel kod oluşturur  
[Hataya Neden Olan Değişiklikler](#_TOC5)  
[Disclaimer](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>Giriş

ASP.NET MVC 2 ASP.NET MVC 1,0 üzerinde yapılar ve üretkenliği arttırmaya odaklanan büyük bir geliştirme ve özellik kümesi sunar. Bu sürüm, ASP.NET MVC 1,0 ile uyumludur; Bu nedenle ASP.NET MVC 1,0 için tüm bilgi, beceriler, kodunuz ve uzantılar uygulanmaya devam eder.

ASP.NET MVC hakkında daha fazla bilgi için aşağıdaki kaynakları ziyaret edin:

- [MSDN 'de ASP.NET MVC belgeleri](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC web sitesi](https://asp.net/mvc/)
- [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>ASP.NET MVC 1,0 projesini ASP.NET MVC 2 ' ye yükseltme

ASP.NET MVC 2 aynı sunucuda ASP.NET MVC 1,0 ile yan yana yüklenebilir. Bu, uygulama geliştiricilerinin bir ASP.NET MVC 1,0 uygulamasının ASP.NET MVC 2 ' ye ne zaman yükseltileceğini seçme esnekliği sağlar. Yükseltme hakkında daha fazla bilgi için, [ASP.net mvc 1,0 uygulamasını ASP.NET MVC 2 ' ye yükseltme](https://go.microsoft.com/fwlink/?LinkID=185459)belgesine bakın.

## <a name="new-features"></a><a id="_TOC3"></a>Yeni özellikler

Bu bölümde, MVC 2 sürümünde tanıtılan özellikler açıklanmaktadır.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>Şablonlu yardımcılar

Şablonlu yardımcılar, veri türleriyle düzenleme ve görüntüleme için HTML öğelerini otomatik olarak ilişkilendirmenize olanak tanır. Örneğin, System. DateTime türündeki veriler bir görünümde görüntülenirken, tarih seçici UI öğesi otomatik olarak işlenebilir. Bu, alan şablonlarının ASP.NET dinamik verilerinde çalışmasına benzer. Daha fazla bilgi için bkz. verileri MSDN Web sitesinde [görüntülemek Için şablonlu yardımcıları kullanma](https://go.microsoft.com/fwlink/?LinkId=159062) .

### <a name="areas"></a><a id="_TOC3_2"></a>Alanları

Alan, büyük bir projeyi daha küçük bir Web uygulamasının karmaşıklığını yönetmek için birden çok daha küçük bölüme düzenlemenizi sağlar. Her bölüm ("Area") genellikle büyük bir Web sitesinin ayrı bir bölümünü temsil eder ve ilgili denetleyici ve görünüm kümelerini gruplandırmak için kullanılır. Daha fazla bilgi için bkz. [Izlenecek yol: msdn Web sitesindeki alanlara göre ASP.NET MVC uygulamasını düzenleme](https://go.microsoft.com/fwlink/?LinkId=158978) .

Yeni bir alan oluşturmak için, Çözüm Gezgini ' de projeye sağ tıklayın, Ekle ' ye tıklayın ve ardından alan ' a tıklayın. Bu, alan adı için size istemde bulunan bir iletişim kutusu görüntüler. Alan adını girdikten sonra, Visual Studio projeye yeni bir alan ekler.

Aşağıdaki şekilde iki alan, yönetici ve blogların bulunduğu bir proje için örnek düzen gösterilmektedir.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

Bir alan oluşturduğunuzda, Visual Studio AreaRegistration öğesinden her bir alana türeten bir sınıf ekler. Bu sınıf, aşağıdaki örnekte gösterildiği gibi, alanı ve yollarını kaydetmek için gereklidir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2 için varsayılan proje şablonu, Global. asax dosyası kodunda RegisterAllAreas yöntemine bir çağrı içerir. Bu yöntem, AreaRegistration sınıfından türetilen tüm türleri arayarak, türün bir örneğini örnekleyerek ve sonra örnek üzerinde RegisterArea metodunu çağırarak, projedeki her alanı kaydeder. Aşağıdaki örnek bunun nasıl yapıldığını göstermektedir.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Bağlamı çağırarak RegisterArea yönteminde ad alanı belirtmeyin. Namespaces. Add yöntemi, kayıt sınıfının ad alanı varsayılan olarak kullanılır.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>Zaman uyumsuz denetleyiciler için destek

ASP.NET MVC 2 artık denetleyicilerin istekleri zaman uyumsuz olarak işlemesini sağlar. Bu, genellikle engelleme işlemlerini çağırma (ağ istekleri gibi) sunucuların, engellenmeyen karşılıkların çağırmasına izin vererek performans kazanmasına yol açabilir. Daha fazla bilgi için MSDN 'de [ASP.NET MVC 'de zaman uyumsuz denetleyici kullanma](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) konusuna bakın.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>Işlem yöntemi parametrelerinde DefaultValueAttribute desteği

System. ComponentModel. DefaultValueAttribute sınıfı, bağımsız değişken parametresi için bir eylem yöntemine varsayılan bir değer verilmesini sağlar. Örneğin, aşağıdaki varsayılan yolun tanımlandığını varsayalım:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

Ayrıca, aşağıdaki denetleyicinin ve eylem yönteminin tanımlandığını de varsayın:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Aşağıdaki istek URL 'Lerinden herhangi biri, önceki örnekte tanımlanan görüntüleme eylemi yöntemini çağırır.

- /Article/View/123
- /Article/View/123? sayfa = 1 (önceki istekle aynı şekilde)
- /Article/View/123? sayfa = 2

DefaultValueAttribute özniteliği olmadan, yukarıdaki listenin ilk URL 'SI çalışmaz, çünkü sayfa bağımsız değişkeni değeri sağlanmamış bir null değer türüdür.

Kodunuz Visual Basic 2010 veya Visual C# 2010 ' de yazılmışsa, aşağıdaki örnekte gösterildiği gibi DefaultValueAttribute özniteliği yerine isteğe bağlı parametreleri kullanabilirsiniz:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>Model ciltleri ile Ikili verileri bağlama desteği

İkili değerleri Base-64 kodlu dizeler olarak kodlayan HTML. Hidden Yardımcısı 'nın iki yeni aşırı yüklemesi vardır:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Tipik bir kullanım, görünümdeki bir nesne için zaman damgası katıştırmanız olur. Örneğin, uygulamanız aşağıdaki ürün nesnesini içerebilir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Bir düzenleme formu, aşağıdaki örnekte gösterildiği gibi formundaki TimeStamp özelliğini işleyebilir:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Bu biçimlendirme, aşağıdaki örneğe benzer bir Base-64 kodlu dize olarak zaman damgası değeri olan bir gizli giriş öğesini işler:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Bu form, aşağıdaki örnekte gösterildiği gibi ürün türünde bir bağımsız değişkeni olan bir eylem yöntemine gönderilebilir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

Action yönteminde, postalanan Base-64 kodlu dize bir bayt dizisine dönüştürüldüğü için TimeStamp özelliği doğru doldurulur.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>ModelMetadata ve ModelMetadataProvider sınıfları

ModelMetadataProvider sınıfı, bir görünüm içindeki model için meta verileri almak üzere bir soyutlama sağlar. MVC 2, System. ComponentModel. Dataaçıklamalarda ad alanındaki öznitelikler tarafından açığa çıkarılan meta verileri kullanılabilir hale getiren bir varsayılan sağlayıcı içerir. Veritabanları veya XML dosyaları gibi diğer veri depolarından meta veriler sağlayan meta veri sağlayıcıları oluşturmak mümkündür.

ViewDataDictionary sınıfı, ModelMetadataProvider sınıfı tarafından modelden ayıklanan meta verileri içeren bir ModelMetadata nesnesi gösterir. Bu, şablonlu yardımcıların bu meta verileri kullanmasını ve çıktılarını bunlara göre ayarlamasını sağlar.

Daha fazla bilgi için bkz. [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) ve [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) sınıfları için belgeler.

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>Dataek açıklama öznitelikleri için destek

ASP.NET MVC 2, giriş doğrulaması sağlamak üzere bir modele bağladığınızda RangeAttribute, RequiredAttribute, StringLengthAttribute ve RegexAttribute doğrulama özniteliklerinin (System. ComponentModel. Dataaçıklamalarda tanımlanmıştır) kullanılmasını destekler.

Daha fazla bilgi için bkz. [nasıl yapılır: msdn Web sitesindeki Dataaçıklamaların özniteliklerini kullanarak model verilerini doğrulama](https://go.microsoft.com/fwlink/?LinkId=159063) . Bu özniteliklerin kullanımını gösteren örnek bir proje ' de indirilebilir [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>Model doğrulayıcı sağlayıcıları

Model doğrulama sağlayıcısı sınıfı, model için doğrulama mantığı sağlayan bir soyutlamayı temsil eder. ASP.NET MVC, System. ComponentModel. Dataaçıklamalarda ad alanına dahil olan doğrulama özniteliklerini temel alan bir varsayılan sağlayıcı içerir. Ayrıca, özel doğrulama kurallarını tanımlayan kendi doğrulama sağlayıcılarınızı ve bu modele doğrulama kurallarının özel eşlemelerini de oluşturabilirsiniz. Daha fazla bilgi için bkz. [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) sınıfı için belgeler.

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>İstemci tarafı doğrulaması

Model-doğrulayıcı sağlayıcısı sınıfı, bir istemci tarafı doğrulama kitaplığı tarafından tüketilen JSON seri hale getirilmiş veriler biçiminde tarayıcıya doğrulama meta verilerini gösterir. ASP.NET MVC 2, daha önce belirtilen Dataaçıklamalarda ad alanı doğrulama özniteliklerini destekleyen bir istemci doğrulama kitaplığı ve bağdaştırıcısı içerir. Sağlayıcı sınıfı, JSON verilerini işleyen bir bağdaştırıcı yazarak diğer istemci doğrulama kitaplıklarını ve alternatif kitaplığa çağrıları kullanmanıza da olanak sağlar.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>Visual Studio 2010 için yeni kod parçacıkları

ASP.NET MVC 2 için bir dizi HTML kod parçacığı, Visual Studio 2010 ile birlikte yüklenir. Bu kod parçacıklarının bir listesini görüntülemek için, Araçlar menüsünde kod parçacıkları Yöneticisi ' ni seçin. Dil için HTML ' i seçin ve konum için ASP.NET MVC 2 ' yi seçin. Kod parçacıklarını kullanma hakkında daha fazla bilgi için bkz. Visual Studio belgeleri.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>Yeni RequireHttpsAttribute eylem filtresi

ASP.NET MVC 2, eylem yöntemlerine ve denetleyicilerine uygulanabilen yeni bir RequireHttpsAttribute sınıfı içerir. Varsayılan olarak filtre, SSL olmayan (HTTP) isteği SSL etkin (HTTPS) eşdeğerine yeniden yönlendirir.

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>HTTP yöntemi fiilini geçersiz kılma

REST mimari stilini kullanarak bir Web sitesi oluşturduğunuzda, bir kaynak için hangi eylemin gerçekleştirileceğini belirleyen HTTP fiilleri kullanılır. REST, uygulamaların al, koy, POST ve DELETE dahil olmak üzere ortak HTTP fiillerinin tam aralığını desteklemesini gerektirir.

ASP.NET MVC 2, eylem yöntemlerine uygulayabileceğiniz yeni öznitelikleri ve bu özellik Compact söz dizimini içerir. Bu öznitelikler, ASP.NET MVC 'nin HTTP fiilini temel alan bir eylem yöntemi seçmesini sağlar. Aşağıdaki örnekte, bir POST isteği ilk eylem yöntemini çağırır ve bir PUT isteği ikinci eylem yöntemini çağıracaktır.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

ASP.NET MVC 'nin önceki sürümlerinde, bu eylem yöntemleri aşağıdaki örnekte gösterildiği gibi daha ayrıntılı sözdizimi gerektirir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Tarayıcılar yalnızca GET ve POST HTTP fiillerini desteklediğinden, farklı bir fiil gerektiren bir eyleme gönderi yapılamaz. Bu nedenle, tüm yeniden yapılan istekleri yerel olarak desteklemek mümkün değildir.

Ancak, POST işlemleri sırasında yeniden yapılan istekleri desteklemek için, ASP.NET MVC 2 yeni bir Httpyöntemverride HTML yardımcı yöntemi sunar. Bu yöntem, formun herhangi bir HTTP yöntemine etkin bir şekilde öykünmesine neden olan gizli bir giriş öğesi oluşturur. Örneğin, Httpyöntemverride HTML yardımcı yöntemini kullanarak form gönderiminizin bir PUT veya DELETE isteği olarak görünmesini sağlayabilirsiniz. Httpmetodoverride 'ın davranışı aşağıdaki öznitelikleri etkiler:

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

Gizli giriş öğesinin adı X-HTTP-Method-override ve değeri benzetimi yapılacak HTTP fiili olarak ayarlanmıştır. Geçersiz kılma değeri bir HTTP üst bilgisinde veya bir sorgu dizesi değerinde ad/değer çifti olarak belirtilebilir.

Geçersiz kılma yalnızca gerçek istek bir POST isteği olduğunda kullanılabilir. Herhangi bir HTTP fiilini kullanan isteklerde geçersiz kılma değeri yok sayılır.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>Şablonlu Yardımcılar için yeni HiddenInputAttribute sınıfı

Model bir düzenleyici şablonunda görüntülenirken bir gizli giriş öğesinin işlenip işlenmeyeceğini göstermek için yeni HiddenInputAttribute özniteliğini bir model özelliğine uygulayabilirsiniz. (Öznitelik, Hiddenınput öğesinin örtük Uııınt değerini ayarlar). Özniteliğin DisplayValue özelliği, değerin düzenleyici ve görüntüleme modlarında görüntülenip görüntülenmeyeceğini belirtmenize olanak tanır. DisplayValue değeri false olarak ayarlandığında, normalde bir alanı çevreleyecek HTML biçimlendirmesi olmasa da hiçbir şey görüntülenmez. DisplayValue için varsayılan değer true 'dur.

Aşağıdaki senaryolarda HiddenInputAttribute özniteliğini kullanabilirsiniz:

- Bir görünüm, kullanıcıların bir nesnenin KIMLIĞINI düzenlemesine izin verir ve bu değerin, denetleyiciye geri geçirilebilmesi için eski KIMLIĞI içeren gizli bir giriş öğesi sağlaması gerekir.
- Bir görünüm, kullanıcıların zaman damgası özelliği gibi hiçbir zaman gösterilmemesi gereken bir ikili özelliği düzenlemesine izin verir. Bu durumda, değer ve çevreleyen HTML biçimlendirmesi (örneğin, etiket ve değer) görüntülenmez.

Aşağıdaki örnek, HiddenInputAttribute sınıfının nasıl kullanılacağını göstermektedir.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Özniteliği true olarak ayarlandığında (veya hiçbir parametre belirtilmemişse), aşağıdakiler gerçekleşir:

- Görüntüleme şablonlarında, bir etiket işlenir ve değer kullanıcıya gösterilir.
- Düzenleyici şablonlarında, bir etiket işlenir ve değer gizli bir giriş öğesinde işlenir.

Özniteliği false olarak ayarlandığında aşağıdakiler gerçekleşir:

- Görüntüleme şablonlarında, bu alan için hiçbir şey işlenmez.
- Düzenleyici şablonlarında, hiçbir etiket işlenmez ve değer gizli bir giriş öğesinde işlenir.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>HTML. ValidationSummary yardımcı yöntemi model düzeyi hataları gösterebilir

Tüm doğrulama hatalarını her zaman görüntülemek yerine, HTML. ValidationSummary yardımcı yönteminin yalnızca model düzeyi hataları görüntülemek için yeni bir seçeneği vardır. Bu, her alanın yanında görüntülenmek üzere doğrulama özetinde ve alana özgü hatalarda model düzeyi hataların görüntülenmesini sağlar.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>Visual Studio 'daki T4 şablonları .NET Framework hedef sürümüne özel kod oluşturur

ASP.NET MVC T4 ana bilgisayardan, uygulama tarafından kullanılan .NET Framework sürümünü belirten yeni bir özellik kullanılabilir. Bu, T4 şablonlarının .NET Framework bir sürümüne özgü kod ve biçimlendirme oluşturmasına olanak sağlar. Visual Studio 2008 ' de, değer her zaman .NET 3,5 ' dir. Visual Studio 2010 ' de, değer .NET 3,5 veya .NET 4 ' dir.

## <a name="api-improvements"></a><a id="_TOC4"></a>API geliştirmeleri

Bu bölümde, var olan ASP.NET MVC türleri ve üyelerinde yapılan değişiklikler açıklanmaktadır.

- Denetleyici sınıfına korumalı bir sanal CreateActionInvoker yöntemi eklendi. Bu yöntem, denetleyicinin ActionInvoker özelliği tarafından çağrılır ve zaten bir başlatıcı ayarlanmamışsa, başlatıcının yavaş örneklenmesini sağlar.
- AuthorizeAttribute sınıfına korumalı bir sanal HandleUnauthorizedRequest yöntemi eklendi. Bu, yetkilendirmenin başarısız olduğu bir davranışı denetlemek için AuthorizeAttribute 'tan türetilmiş filtrelerin kullanılmasını sağlar.
- ValueProviderDictionary sınıfına bir Add (dize anahtarı, nesne değeri) yöntemi eklendi. Bu, aşağıdaki örnekte olduğu gibi ValueProviderDictionary için sözlük başlatıcısı sözdizimini kullanmanıza olanak sağlar:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- \_Sys. Mvc. AjaxContext sınıfında nesne Al yöntemi eklendi. Bu, Get Data yöntemine benzer bir JavaScript yöntemidir \_ , ancak yanıtın içerik türü uygulama/JSON ise, \_ nesne al JSON nesnesini döndürür.
- AuthorizationContext sınıfına bir ActionDescriptor özelliği eklendi.
- Bir URL parametresi eklendi. bir ID özelliği içeren bir modele bağlama yaparken sorunları geçici olarak çözmek için kullanılabilen, özellik form gönderisini olmadığında bu belirteç. Daha fazla ayrıntı için bkz. PHIL Haack 'in blogu üzerinde [ASP.NET MVC 2 Isteğe bağlı URL parametreleri](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) .

## <a name="breaking-changes"></a><a id="_TOC5"></a>Son değişiklikler

Aşağıdaki değişiklikler, var olan ASP.NET MVC 1,0 uygulamalarında hatalara neden olabilir.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>IDataErrorInfo uygulayan sınıflar için özellik doğrulama davranışında değişiklik

Doğrulama gerçekleştirmek için IDataErrorInfo kullanan model nesneleri için, yeni bir değerin ayarlanmış olup olmamasına bakılmaksızın her özellik onaylanır. ASP.NET MVC 1,0 ' de, yalnızca yeni değerler ayarlanmış olan özellikler doğrulandıktan sonra. ASP.NET MVC 2 ' de, IDataErrorInfo hata özelliği yalnızca tüm özellik Doğrulayıcıları başarılı olursa çağrılır.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>IIS betik eşleme betiği artık yükleyicide kullanılamıyor

IIS betik eşleme betiği, IIS 6 ve IIS 7 için betik eşlemelerini Klasik modda yapılandırmak için kullanılan bir komut satırı betiğdir. Visual Studio geliştirme sunucusunu kullanıyorsanız veya tümleşik modda IIS 7 kullanıyorsanız, betik eşleme betiği gerekli değildir. Betikler, [ASP.net WebStack](https://github.com/aspnet/AspNetWebStack)üzerinde ayrı bir desteklenmeyen indirme olarak kullanılabilir.

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>MVC Futures içindeki HTML. değiştirme Yardımcısı yöntemi artık kullanılamıyor

MVC görünüm altyapısının işleme davranışında yapılan değişiklikler nedeniyle, HTML. değiştirme Yardımcısı yöntemi çalışmaz ve kaldırılmıştır.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider arabirimi IDictionary 'nin tüm kullanımlarını değiştirir

MVC 1,0 içinde IDictionary kabul eden her özellik veya yöntem bağımsız değişkeni artık IValueProvider kabul eder. Bu değişiklik yalnızca özel değer sağlayıcıları veya özel model ciltleri içeren uygulamaları etkiler. Bu değişiklikten etkilenen özellik ve yöntemlere örnek olarak şunlar verilebilir:

- ControllerBase ve ModelBindingContext sınıflarının ValueProvider özelliği.
- Controller sınıfının TryUpdateModel yöntemleri.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Yeni CSS sınıfları site. css dosyasına eklendi

ASP.NET MVC proje şablonlarındaki site. css dosyası, doğrulama işlevi tarafından kullanılan yeni stilleri ve şablonlu yardımcıları içerecek şekilde güncelleştirilmiştir.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Yardımcılar şimdi bir MvcHtmlString nesnesi döndürüyor

ASP.NET 4 ' teki yeni HTML kodlama ifadesi sözdiziminin avantajlarından yararlanabilmek için, HTML Yardımcıları için dönüş türü artık bir dize yerine MvcHtmlString olur. ASP.NET MVC 2 ve ASP.NET 3,5 ' deki yeni yardımcılar ' ı kullanırsanız, HTML kodlaması sözdiziminden yararlanabilemeyeceksiniz; Yeni sözdizimi yalnızca ASP.NET 4 üzerinde ASP.NET MVC 2 ' i çalıştırdığınızda kullanılabilir.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult artık yalnızca HTTP POST isteklerine yanıt veriyor

Bilgilerin açığa çıkması potansiyeli olan JSON ele geçirme saldırılarını azaltmak için, varsayılan olarak, JsonResult sınıfı yalnızca HTTP POST isteklerine yanıt verir. Bir JsonResult nesnesi döndüren eylem yöntemlerine yönelik Ajax GET çağrısı, POST kullanılacak şekilde değiştirilmelidir. Gerekirse, JsonResult 'ın yeni JsonRequestBehavior özelliğini ayarlayarak bu davranışı geçersiz kılabilirsiniz. Olası faydalanma hakkında daha fazla bilgi için bkz. PHIL Haack 'in bloguna yönelik [JSON](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 'a yönelik blog gönderisi.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>ModelBindingContext üzerinde model ve ModelType özellik ayarlayıcıları artık kullanılmıyor

ModelBindingContext sınıfına yeni bir ayarlanabilir ModelMetadata özelliği eklenmiştir. Yeni özellik hem modeli hem de ModelType özelliklerini kapsar. Model ve ModelType özellikleri artık kullanılmıyor olsa da, geriye dönük uyumluluk için, özellik alıcıları hala çalışır; Bu, değeri almak için ModelMetadata özelliğine temsilciliğini sağlar.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>DefaultControllerFactory sınıfında türetilen özel denetleyici fabrikaları üzerinde yapılan değişiklikler

DefaultControllerFactory sınıfı, RequestContext Özelliği kaldırılarak düzeltildi. Bu özelliğin yerine, istek bağlamı örneği korumalı sanal GetControllerInstance ve GetControllerType yöntemlerine geçirilir. Bu değişiklik, DefaultControllerFactory 'den türetilen özel denetleyici fabrikalarını etkiler.

Özel denetleyici fabrikaları, genellikle ASP.NET MVC uygulamalarına yönelik bağımlılık ekleme sağlamak için kullanılır. Özel denetleyici fabrikalarını ASP.NET MVC 2 ' yi destekleyecek şekilde güncelleştirmek için, yöntem imzasını veya imzaları yeni imzalarla eşleşecek şekilde değiştirin ve özellik yerine istek bağlamı parametresini kullanın.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Area" artık ayrılmış bir rota-değer anahtarıdır

Yol değerlerindeki "Area" dizesinin "Controller" ve "Action" ile aynı şekilde ASP.NET MVC 'de özel anlamları vardır. Tek bir sorun, "alan" içeren bir rota-değer sözlüğü ile HTML Yardımcıları sağlandıysa, yardımcılar artık sorgu dizesinde "alan" eklememesi olur.

Alanlar özelliğini kullanıyorsanız, rota URL 'nizin bir parçası olarak {Area} ' ı kullandığınızdan emin olun.

## <a name="disclaimer"></a><a id="_TOC6"></a>Sorumluluk reddi

Bu bir ön belgedir ve burada açıklanan yazılımın son ticari sürümünden önce önemli ölçüde değiştirilebilir.

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Microsoft 'un değişen piyasa koşullarını yanıtlaması gerektiğinden, Microsoft 'un kapsamında bir taahhüt olarak yorumlanmamalıdır ve Microsoft 'un, yayın tarihinden sonra sunulan bilgilerin doğruluğunu garanti edemez.

Bu teknik Inceleme yalnızca bilgilendirme amaçlıdır. MICROSOFT, BU BELGEDEKI BILGILERE GÖRE HIÇBIR GARANTI VERMEZ, ÖRTÜLÜ VEYA YASAL DEĞILDIR.

Tüm geçerli telif hakkı yasaları ile uyumlu olması, kullanıcının sorumluluğundadır. Telif hakkı kapsamındaki hakları sınırlandırmadan, bu belgenin hiçbir bölümü çoğaltılamaz, bir alma sisteminde depolanabilir veya bir alma sisteminde bulunabilir ya da herhangi bir biçimde ya da herhangi bir amaçla (elektronik, mekanik, Fotokopi, kayıt veya diğer yollarla) ya da herhangi bir amaçla (Microsoft Corporation 'ın Express yazılı izni olmadan) veya herhangi bir amaçla iletilebilir.

Microsoft 'un bu belgede ilgili konuyu kapsayan patentler, patent uygulamaları, ticari markalar, telif hakları veya diğer fikri mülkiyet hakları olabilir. Microsoft 'un herhangi bir yazılı lisans sözleşmesinde açık bir şekilde sağlanmasının dışında, bu belgenin bu patentinin bir lisansını, ticari markalara, telif haklarına veya diğer fikri mülkiyet için herhangi bir lisansa vermez.

Aksi belirtilmedikçe, burada adı geçen örnek şirketler, kuruluşlar, ürünler, etki alanı adları, e-posta adresleri, logolar, kişiler, konumlar ve olaylar kurgusaldır ve gerçek şirket, kuruluş, ürün, etki alanı adı, e-posta adresi, logo, kişi, yer veya olayla hiçbir ilişki amaçlanmamıştır.

© 2010 Microsoft Corporation. Tüm hakları saklıdır.

Microsoft ve Windows, Microsoft Corporation 'ın Birleşik Devletler ve/veya diğer ülkelerde kayıtlı ticari markaları veya ticari markalarıdır.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.
