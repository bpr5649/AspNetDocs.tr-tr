---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: ASP.NET AJAX Web hizmetlerini anlama | Microsoft Docs
author: scottcate
description: Web Hizmetleri, dağıtılmış sistemler arasında veri alışverişi için platformlar arası bir çözüm sağlayan .NET Framework 'ün ayrılmaz bir parçasıdır. Web...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162841"
---
# <a name="understanding-aspnet-ajax-web-services"></a>ASP.NET AJAX Web Hizmetlerini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF’yi İndir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web Hizmetleri, dağıtılmış sistemler arasında veri alışverişi için platformlar arası bir çözüm sağlayan .NET Framework 'ün ayrılmaz bir parçasıdır. Web Hizmetleri, farklı işletim sistemleri, nesne modelleri ve programlama dillerinin veri göndermesini ve almasına izin vermek için normalde kullanılsa da, bir ASP.NET AJAX sayfasına dinamik olarak veri eklemek veya bir sayfadan arka uç sistemine veri göndermek için de kullanılabilir. Bunun hepsi geri gönderme işlemlerine yeniden bildirmeden yapılabilir.

## <a name="calling-web-services-with-aspnet-ajax"></a>Web hizmetlerini ASP.NET AJAX ile çağırma

Dan Wahlin

Web Hizmetleri, dağıtılmış sistemler arasında veri alışverişi için platformlar arası bir çözüm sağlayan .NET Framework 'ün ayrılmaz bir parçasıdır. Web Hizmetleri, farklı işletim sistemleri, nesne modelleri ve programlama dillerinin veri göndermesini ve almasına izin vermek için normalde kullanılsa da, bir ASP.NET AJAX sayfasına dinamik olarak veri eklemek veya bir sayfadan arka uç sistemine veri göndermek için de kullanılabilir. Bunun hepsi geri gönderme işlemlerine yeniden bildirmeden yapılabilir.

ASP.NET AJAX UpdatePanel denetimi, AJAX 'un herhangi bir ASP.NET sayfasına kolay bir yolunu sağladığından, bir UpdatePanel kullanmadan sunucudaki verilere dinamik olarak erişmeniz gereken zamanlar olabilir. Bu makalede, ASP.NET AJAX sayfaları içinde Web hizmetleri oluşturup tüketerek bunu nasıl gerçekleştirebileceğiniz göreceksiniz.

Bu makale, çekirdek ASP.NET AJAX uzantılarında sunulan işlevlere ve AutoCompleteExtender adlı ASP.NET AJAX araç setinde Web hizmeti etkinleştirilmiş bir denetime odaklanacaktır. Kapsanan konular, AJAX özellikli Web Hizmetleri tanımlamayı, istemci proxy 'leri oluşturmayı ve JavaScript ile Web hizmetlerini çağırmayı içerir. Ayrıca, Web hizmeti çağrılarının doğrudan ASP.NET sayfa yöntemlerine nasıl kullanılabileceğini de göreceksiniz.

## <a name="web-services-configuration"></a>Web Hizmetleri Yapılandırması

Visual Studio 2008 ile yeni bir Web sitesi projesi oluşturulduğunda, web.config dosyası, önceki Visual Studio sürümlerindeki kullanıcılara alışkın olabilecek bir dizi yeni eklemedir. Bu değişikliklerden bazıları, "ASP" önekini ASP.NET AJAX denetimlerine eşledikten sonra, diğerleri gerekli HttpHandlers ve HttpModules tanımladıkları sayfalarda kullanılabilirler. Listeleme 1, `<httpHandlers>` Web hizmeti çağrılarını etkileyen web.config öğesinde yapılan değişiklikleri gösterir. . Asmx çağrılarını işlemek için kullanılan varsayılan HttpHandler kaldırılır ve System.Web.Extensions.dll derlemesinde bulunan bir ScriptHandlerFactory sınıfıyla değiştirilmiştir. System.Web.Extensions.dll, ASP.NET AJAX tarafından kullanılan tüm çekirdek işlevleri içerir.

**Listeleme 1. ASP.NET AJAX Web hizmeti Işleyicisi yapılandırması**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

Bu HttpHandler değişikliği, ASP.NET AJAX sayfalarından bir JavaScript Web hizmeti proxy 'si kullanılarak .NET Web Hizmetleri 'ne JavaScript Nesne Gösterimi (JSON) çağrılarının yapılabilmesi için yapılır. ASP.NET AJAX, genellikle Web hizmetleriyle ilişkili olan standart basit nesne erişim Protokolü (SOAP) çağrılarını tersine Web Hizmetleri 'ne JSON iletileri gönderir. Bu, genel istek ve yanıt iletileri genelindeki sonuçlara neden olur. Ayrıca, ASP.NET AJAX JavaScript kitaplığı JSON nesneleriyle çalışacak şekilde iyileştirildiğinden, verilerin daha verimli istemci tarafı işlenmesini sağlar. Listeleme 2 ve Listeleme 3, Web hizmeti isteği ve JSON biçimine serileştirilmiş yanıt iletilerinin örneklerini gösterir. Kod 2 ' de gösterilen istek iletisi, "Belçika" değeriyle bir ülke parametresi geçirir, ancak Listeleme 3 ' teki yanıt iletisi bir müşteri nesneleri dizisi ve bunlarla ilişkili özellikler geçirir.

**Listeleme 2. JSON 'a serileştirilmiş Web hizmeti Istek Iletisi**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]işlem adı Web HIZMETI URL 'sinin bir parçası olarak tanımlanır; Ayrıca, istek iletileri her zaman JSON aracılığıyla gönderilmez. Web Hizmetleri, UseHttpGet parametresi true olarak ayarlanan ScriptMethod özniteliğini kullanarak parametrelerin sorgu dizesi parametreleri aracılığıyla geçirilmesine neden olabilir.*

**Listeleme 3. JSON 'a serileştirilmiş Web hizmeti yanıt Iletisi**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

Sonraki bölümde, JSON istek iletilerini işleme ve hem basit hem de karmaşık türlerle yanıt veren Web Hizmetleri oluşturmayı öğreneceksiniz.

## <a name="creating-ajax-enabled-web-services"></a>AJAX etkin Web Hizmetleri oluşturma

ASP.NET AJAX Framework, Web hizmetlerini çağırmak için birkaç farklı yol sağlar. AutoCompleteExtender denetimini (ASP.NET AJAX araç seti 'nde kullanılabilir) veya JavaScript kullanabilirsiniz. Ancak, bir hizmeti çağırmadan önce, istemci betiği kodu tarafından çağrılabilmesi için AJAX 'u etkinleştirmeniz gerekir.

ASP.NET Web Hizmetleri için yeni bir hizmet olup olmadığınız gibi, hizmetleri oluşturmak ve AJAX etkinleştirmek için basit bulacaksınız. .NET Framework, 2002 ' deki ilk sürümü ve ASP.NET AJAX Uzantıları, .NET Framework 'ün varsayılan özellikler kümesini oluşturan ek AJAX işlevleri sunduğundan, ASP.NET Web Hizmetleri oluşturmayı destekliyordu. Visual Studio .NET 2008 Beta 2,. asmx Web hizmeti dosyaları oluşturmaya yönelik yerleşik desteğe sahiptir ve System. Web. Services. WebService sınıfından sınıfların yanına ilişkili kodu otomatik olarak türetiliyor. Sınıfına Yöntemler eklediğinizde, Web hizmeti tüketicileri tarafından çağrılabilmesi için WebMethod özniteliğini uygulamanız gerekir.

4. liste, WebMethod özniteliğini GetCustomersByCountry () adlı bir yönteme uygulamanın bir örneğini gösterir.

**4. liste. Web hizmetinde WebMethod özniteliğini kullanma**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry () yöntemi bir ülke parametresini kabul eder ve bir müşteri nesnesi dizisi döndürür. Yöntemine geçirilen ülke değeri, veritabanından veri almak için bir veri katmanı sınıfını çağıran bir iş katmanı sınıfına iletilir, müşteri nesnesi özelliklerini verilerle doldurup diziyi döndürün.

## <a name="using-the-scriptservice-attribute"></a>ScriptService özniteliğini kullanma

WebMethod özniteliği eklenirken, GetCustomersByCountry () yönteminin Web hizmetine standart SOAP iletileri gönderen istemciler tarafından çağrılmasına izin verilir. Bu, ASP.NET AJAX uygulamalarından gelen JSON çağrılarının kutudan çıkmasına izin vermez. JSON çağrılarının uygulanmasına izin vermek için, ASP.NET AJAX uzantısının `ScriptService` özniteliğini Web hizmeti sınıfına uygulamanız gerekir. Bu, bir Web hizmetinin JSON kullanarak biçimlendirilen yanıt iletilerini göndermesini ve istemci tarafı komut dosyasının JSON iletileri göndererek bir hizmeti çağırmasını sağlar.

5. liste, ScriptService özniteliğini CustomersService adlı bir Web hizmeti sınıfına uygulamanın bir örneğini gösterir.

**5. liste. Web hizmetini AJAX-etkinleştirmek için ScriptService özniteliğini kullanma**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService özniteliği, AJAX betik kodundan çağrılbileceğini belirten bir işaret görevi görür. Aslında, arka planda oluşan herhangi bir JSON serileştirmesi veya serisini kaldırma görevi işlemez. ScriptHandlerFactory (web.config ' de yapılandırılan) ve diğer ilgili sınıflar JSON işlemenin toplu işlemini gerçekleştiriyor.

## <a name="using-the-scriptmethod-attribute"></a>ScriptMethod özniteliğini kullanma

ScriptService özniteliği, ASP.NET AJAX sayfaları tarafından kullanılabilmesi için .NET Web hizmetinde tanımlanması gereken tek ASP.NET AJAX özniteliğidir. Ancak, ScriptMethod adlı başka bir öznitelik de bir hizmette Web yöntemlerine doğrudan uygulanabilir. ScriptMethod, ve dahil olmak üzere üç özelliği tanımlar `UseHttpGet` `ResponseFormat` `XmlSerializeString` . Bu özelliklerin değerlerini değiştirmek, bir Web yöntemi tarafından kabul edilen isteğin türünün al olarak değiştirilmesi gereken durumlarda veya bir Web yönteminin ham XML verilerini bir veya nesnesi biçiminde döndürmesi gerektiğinde `XmlDocument` `XmlElement` veya bir hizmetten döndürülen verilerin her zaman JSON yerine XML olarak serileştirilmesi gerektiğinde yararlı olabilir.

UseHttpGet özelliği, bir Web yönteminin POST isteklerini tersine kabul etmesi gerektiğinde kullanılabilir. İstekler, QueryString parametrelerine dönüştürülen Web yöntemi giriş parametrelerine sahip bir URL kullanılarak gönderilir. UseHttpGet özelliği false olarak ayarlanır ve yalnızca `true` işlemlerin güvenli olduğu bilindiğinde ve gizli verilerin bir Web hizmetine geçirilmediği durumlarda olarak ayarlanmalıdır. 6. liste, ScriptMethod özniteliğini UseHttpGet özelliği ile kullanmayla ilgili bir örnek gösterir.

**Liste 6. ScriptMethod özniteliğini UseHttpGet özelliğiyle kullanma.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

5. listede gösterilen HttpGetEcho Web yöntemi çağrıldığında gönderilen üstbilgilere bir örnek gösterilir:

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

Web yöntemlerinin HTTP GET isteklerini kabul etmesine izin vermenin yanı sıra, XML yanıtlarının JSON yerine bir hizmetten döndürülmesi gerektiğinde ScriptMethod özniteliği de kullanılabilir. Örneğin, bir Web hizmeti uzak bir siteden RSS akışı alabilir ve bunu XmlDocument veya XmlElement nesnesi olarak döndürebilir. XML verilerinin işlenmesi, daha sonra istemcisinde meydana gelebilir.

7. liste, XML verilerinin bir Web yönteminden döndürülüp döndürülmeyeceğini belirtmek için ResponseFormat özelliğinin kullanılmasına bir örnek gösterir.

**Listeleme 7. ScriptMethod özniteliğini ResponseFormat özelliği ile birlikte kullanma.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat özelliği de XmlSerializeString özelliği ile birlikte kullanılabilir. XmlSerializeString özelliğinin varsayılan değeri false değerine sahiptir; bu, bir Web yönteminden döndürülen dizeler hariç tüm dönüş türlerinin, özelliği olarak ayarlandığında XML olarak serileştirildiği anlamına gelir `ResponseFormat` `ResponseFormat.Xml` . , `XmlSerializeString` Olarak ayarlandığında `true` , bir Web yönteminden döndürülen tüm türler dize TÜRLERI dahil XML olarak serileştirilir. ResponseFormat özelliğinde XmlSerializeString özelliğinin bir değeri varsa, bu değer yok `ResponseFormat.Json` sayılır.

8. liste, dizelerin XML olarak serileştirilmesine zorlamak için XmlSerializeString özelliğinin kullanılmasına bir örnek gösterir.

**8. liste. ScriptMethod özniteliğini XmlSerializeString özelliği ile kullanma**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

{1 & gt; Liste 8 & lt; 1} bölümünde gösterilen GetXmlString Web yönteminin çağrılmasının döndürdüğü değer

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

Varsayılan JSON biçimi istek ve yanıt iletilerinin genel boyutunu en aza indirir ve ASP.NET AJAX istemcileri tarafından bir çapraz tarayıcıda daha kolay tüketibilse de, Internet Explorer 5 veya üzeri gibi istemci uygulamalar bir Web yönteminden XML verilerinin döndürülmesini beklediği zaman ResponseFormat ve XmlSerializeString özellikleri kullanılabilir.

## <a name="working-with-complex-types"></a>Karmaşık türlerle çalışma

Listeleme 5, bir Web hizmetinden müşteri adında karmaşık bir tür döndüren bir örnek gösterdi. Müşteri sınıfı, dahili olarak FirstName ve LastName gibi özellikler olarak birçok farklı basit türü tanımlar. Bir AJAX etkin Web yönteminde giriş parametresi veya dönüş türü olarak kullanılan karmaşık türler, istemci tarafına gönderilmeden önce otomatik olarak JSON olarak serileştirilir. Ancak, iç içe geçmiş karmaşık türler (başka bir tür içinde dahili olarak tanımlanmış olanlar), varsayılan olarak tek başına nesneler olarak istemci için kullanılamaz.

Bir Web hizmeti tarafından kullanılan iç içe geçmiş karmaşık türün aynı zamanda bir istemci sayfasında kullanılması gereken durumlarda, ASP.NET AJAX GenerateScriptType özniteliği Web hizmetine eklenebilir. Örneğin, liste 9 ' da gösterilen CustomerDetails sınıfı, ***iç içe geçmiş karmaşık türleri temsil eden*** Address ve cinsiyet özelliklerini içerir.

**9. liste. Burada gösterilen CustomerDetails sınıfı iki iç içe karmaşık tür içerir.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

Liste 9 ' da gösterilen CustomerDetails sınıfında tanımlanan Address ve cinsiyet nesneleri, iç içe türler olduklarından (adres bir sınıftır ve cinsiyet bir sabit listesi olduğundan), JavaScript aracılığıyla istemci tarafında kullanıma sunulmayacaktır. Bir Web hizmeti içinde kullanılan iç içe bir türün istemci tarafında kullanılabilir olması gereken durumlarda, daha önce bahsedilen GenerateScriptType özniteliği kullanılabilir (bkz. listeleme 10). Bu öznitelik, bir hizmetten farklı iç içe geçmiş karmaşık türlerin döndürüldüğü durumlarda birden çok kez eklenebilir. Doğrudan Web hizmeti sınıfına veya belirli Web yöntemlerine uygulanabilir.

**10 dökümünü yapın. İstemci tarafından kullanılabilir olması gereken iç içe türler tanımlamak için GenerateScriptService özniteliğini kullanma.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

`GenerateScriptType`Özniteliği Web hizmetine uygulayarak, adres ve cinsiyet türleri otomatik olarak istemci tarafı ASP.NET Ajax JavaScript kodu tarafından kullanılabilir hale getirilir. Bir Web hizmetine GenerateScriptType özniteliği eklenerek otomatik olarak oluşturulan ve istemciye gönderilen JavaScript örneği, liste 11 ' de gösterilir. Makalenin devamındaki iç içe geçmiş karmaşık türleri nasıl kullanacağınızı göreceksiniz.

**11. liste. İç içe geçmiş karmaşık türler, bir ASP.NET AJAX sayfasında kullanılabilir hale getirilir.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

Artık Web Hizmetleri oluşturma ve bunları ASP.NET AJAX sayfaları için erişilebilir hale getirme hakkında daha fazla göründüğünüze göre, verilerin alınabilmesi veya Web Hizmetleri 'ne gönderilmesi için JavaScript proxy 'leri oluşturma ve kullanma konusuna göz atalım.

## <a name="creating-javascript-proxies"></a>JavaScript proxy 'Leri oluşturma

Standart bir Web hizmetinin (.NET veya başka bir platformun) çağrılması genellikle SOAP isteği ve yanıt iletilerinin gönderilmesinin karmaşıklıklarından kalkan eden bir proxy nesnesi oluşturulmasını içerir. ASP.NET AJAX Web hizmeti çağrılarında, JavaScript proxy 'leri oluşturulabilir ve JSON iletilerinin serileştirilmesi ve serisini kaldırma hakkında endişelenmeden hizmetleri kolayca çağırmak için kullanılabilir. JavaScript proxy 'leri, ASP.NET AJAX ScriptManager denetimi kullanılarak otomatik olarak oluşturulabilir.

Web Hizmetleri 'ni çağırasağlayan bir JavaScript proxy oluşturma işlemi, ScriptManager 'ın Services özelliği kullanılarak gerçekleştirilir. Bu özellik, bir ASP.NET AJAX sayfasının geri gönderme işlemlerine gerek kalmadan veri göndermek veya almak için zaman uyumsuz olarak çağırabilmesi için bir veya daha fazla hizmet tanımlamanızı sağlar. ASP.NET AJAX `ServiceReference` denetimini kullanarak ve denetimin özelliğine Web hizmeti URL 'si atayarak bir hizmet tanımlarsınız `Path` . 12. liste, CustomersService. asmx adlı bir hizmete başvurmak için bir örnek gösterir.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**12. liste. Bir ASP.NET AJAX sayfasında kullanılan bir Web hizmeti tanımlama.**

ScriptManager denetimi aracılığıyla CustomersService. asmx başvurusu eklemek, JavaScript proxy 'sinin sayfa tarafından dinamik olarak oluşturulup başvurulmasına neden olur. Proxy, &lt; komut dosyası etiketi kullanılarak katıştırılır &gt; ve CustomersService. asmx dosyası çağırarak ve/js Bunun sonuna eklenerek dinamik olarak yüklenir. Aşağıdaki örnek, web.config hata ayıklama devre dışı bırakıldığında JavaScript proxy 'sinin sayfaya nasıl katıştırıldığını gösterir:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]Oluşturulan gerçek JavaScript proxy kodunu görmek isterseniz, istenen .NET Web hizmetinin URL 'Sini Internet Explorer 'ın Adres kutusuna yazabilir ve/js ' nin sonuna ekleyebilirsiniz.*

web.config 'de hata ayıklama etkinse, JavaScript proxy 'sinin hata ayıklama sürümü, sonraki gösterildiği gibi sayfada gömülecektir:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager tarafından oluşturulan JavaScript proxy 'si, &lt; komut dosyası etiketinin src özniteliği kullanılarak başvurulmak yerine doğrudan sayfaya gömülebilir &gt; . Bu işlem, ServiceReference denetiminin InlineScript özelliği true olarak ayarlanarak yapılabilir (varsayılan değer false 'dur). Bu, bir ara sunucu birden çok sayfada paylaşılmıyorsa ve sunucuya yapılan ağ çağrılarının sayısını azaltmak istediğinizde yararlı olabilir. InlineScript değeri true olarak ayarlandığında proxy betiği tarayıcı tarafından önbelleğe alınmaz. bu nedenle, proxy 'nin bir ASP.NET AJAX uygulamasında birden çok sayfa tarafından kullanıldığı durumlarda varsayılan değer false değeri önerilir. InlineScript özelliğinin kullanılmasına bir örnek aşağıda gösterilmiştir:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>JavaScript proxy 'Leri kullanma

Bir Web hizmetine ScriptManager denetimi kullanılarak bir ASP.NET AJAX sayfası tarafından başvurulduktan sonra, Web hizmetine bir çağrı yapılabilir ve döndürülen veriler geri çağırma işlevleri kullanılarak işlenebilir. Web hizmeti, ad alanına (varsa) başvurarak çağrılır, sınıf adı ve Web yöntemi adı. Web hizmetine geçirilen parametreler, döndürülen verileri işleyen bir geri çağırma işleviyle birlikte tanımlanabilir.

GetCustomersByCountry () adlı bir Web yöntemini çağırmak için JavaScript proxy kullanma örneği, 13. listede gösterilmektedir. GetCustomersByCountry () işlevi, son kullanıcı sayfadaki bir düğmeye tıkladığında çağrılır.

**13. liste. Bir Web hizmetini JavaScript proxy ile çağırma.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

Bu çağrı, hizmette tanımlanmış olan ınterfacetsınvinamespace, CustomersService Class ve GetCustomersByCountry Web metoduna başvurur. Bir metin kutusundan alınan bir ülke değerini ve zaman uyumsuz Web hizmeti çağrısı döndürüldüğünde çağrılması gereken Onwsrequesttamamlanmıştır adlı bir geri çağırma işlevini geçirir. Onwsrequesttamamlanmıştır, hizmetten döndürülen müşteri nesnelerinin dizisini işler ve bunları sayfada görüntülenen bir tabloya dönüştürür. Çağrıdan oluşturulan çıkış şekil 1 ' de gösterilmiştir.

[![Bir Web hizmetine zaman uyumsuz bir AJAX çağrısı yaparak edinilen verileri bağlama.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**Şekil 1**: bir Web hizmetine zaman uyumsuz bir AJAX çağrısı yaparak alınan verileri bağlama.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-web-services/_static/image3.png))

JavaScript proxy 'leri, Web yönteminin çağrılması gereken ancak proxy 'nin bir Yanıt beklemesi beklenmemesi durumunda Web Hizmetleri için tek yönlü çağrılar da yapabilir. Örneğin, iş akışı gibi bir işlemi başlatmak için bir Web hizmetini çağırmak, ancak hizmetten bir dönüş değeri beklemeleri beklenmez. Bir hizmete tek yönlü çağrının yapılması gereken durumlarda, 13. listede gösterilen geri çağırma işlevi yalnızca atlanabilir. Hiçbir geri arama işlevi tanımlanmadığı için, proxy nesnesi Web hizmetinin veri döndürmesini beklemez.

## <a name="handling-errors"></a>Hataları İşleme

Web hizmetlerine yönelik zaman uyumsuz geri çağrılar, ağ çalışmıyor, Web hizmeti kullanılamayan veya döndürülmekte olan bir özel durum gibi farklı türde hatalarla karşılaşabilir. Neyse ki, ScriptManager tarafından oluşturulan JavaScript proxy nesneleri, daha önce gösterilen başarı geri çağırmaya ek olarak hataları ve hataları işlemek için birden çok geri aramanın tanımlanmasına izin verir. Hata geri çağırma işlevi, 14. listede gösterildiği gibi Web metoduna yapılan çağrıda standart geri çağırma işlevinden hemen sonra tanımlanabilir.

**14. liste. Hata geri çağırma işlevini tanımlama ve hataları görüntüleme.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

Web hizmeti çağrıldığında oluşan tüm hatalar, hatayı bir parametre olarak temsil eden bir nesneyi kabul eden OnWSRequestFailed () geri çağırma işlevini tetikler. Hata nesnesi, hatanın nedenini ve çağrının zaman aşımına uğramadığını öğrenmek için birkaç farklı işlev sunar. 14. liste, farklı hata işlevlerini kullanmanın bir örneğini gösterir ve Şekil 2 işlevler tarafından oluşturulan çıktının bir örneğini gösterir.

[![ASP.NET AJAX hata işlevleri çağrılırken oluşturulan çıkış.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**Şekil 2**: ASP.NET AJAX hata işlevleri çağrılırken oluşturulan çıkış.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-web-services/_static/image6.png))

## <a name="handling-xml-data-returned-from-a-web-service"></a>Bir Web hizmetinden döndürülen XML verilerini işleme

Daha önce, bir Web yönteminin, ' ın ResponseFormat özelliği ile birlikte ScriptMethod özniteliğini kullanarak ham XML verilerini nasıl döndürediğinin gördük. ResponseFormat ResponseFormat.Xml olarak ayarlandığında, Web hizmetinden döndürülen veriler JSON yerine XML olarak serileştirilir. Bu, XML verilerinin JavaScript veya XSLT kullanılarak işlenmek üzere istemciye doğrudan geçirilmesi gerektiğinde yararlı olabilir. Geçerli zamanda, Internet Explorer 5 veya üzeri, MSXML için yerleşik desteği nedeniyle XML verilerini ayrıştırmak ve filtrelemek için en iyi istemci tarafı nesne modelini sağlar.

XML verilerinin bir Web hizmetinden alınması, diğer veri türlerini almaktan farklı değildir. Uygun işlevi çağırmak ve bir geri çağırma işlevi tanımlamak için JavaScript proxy 'sini çağırarak başlayın. Çağrı geri döndüğünde, geri çağırma işlevindeki verileri işleyebilirsiniz.

15 numaralı listede, bir XmlElement nesnesi döndüren GetRssFeed () adlı bir Web yöntemi çağırma örneği gösterilmektedir. GetRssFeed () alınacak RSS akışı URL 'sini temsil eden tek bir parametre kabul eder.

**15. liste. Bir Web hizmetinden döndürülen XML verileriyle çalışma.**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

Bu örnek, bir RSS akışına bir URL geçirir ve döndürülen XML verilerini Onwsrequesttamamlana () işlevinde işler. Onwsrequesttamamlanmıştır () önce tarayıcının, MSXML ayrıştırıcısının kullanılabilir olup olmadığını anlamak için Internet Explorer olup olmadığını kontrol eder. Eğer ise, &lt; RSS akışı içindeki tüm öğe etiketlerini bulmak için bir XPath deyimleri kullanılır &gt; . Her öğe daha sonra üzerinden yinelenir ve ilgili &lt; başlık &gt; ve &lt; bağlantı etiketleri, &gt; her öğenin verilerini görüntüleyecek şekilde bulunur ve işlenir. Şekil 3 ' te, GetRssFeed () Web metoduna bir JavaScript proxy üzerinden ASP.NET AJAX çağrısı yapmaktan oluşturulan çıktının bir örneği gösterilmektedir.

## <a name="handling-complex-types"></a>Karmaşık türleri işleme

Bir Web hizmeti tarafından kabul edilen veya döndürülen karmaşık türler otomatik olarak bir JavaScript proxy 'si aracılığıyla sunulur. Ancak, daha önce anlatıldığı gibi, GenerateScriptType özniteliği hizmete uygulanmamışsa, iç içe karmaşık türler doğrudan istemci tarafında erişilebilir değildir. Neden istemci tarafında iç içe geçmiş karmaşık bir tür kullanmak istiyorsunuz?

Bu soruyu yanıtlamak için, bir ASP.NET AJAX sayfasının müşteri verilerini görüntülediğini ve son kullanıcıların bir müşterinin adresini güncelleştirmesine izin verdiğini varsayın. Web hizmeti, adres türünün (bir CustomerDetails sınıfı içinde tanımlanan karmaşık bir tür) istemciye gönderilemeyeceğini belirtirse, daha iyi kod yeniden kullanımı için güncelleştirme işlemi ayrı işlevlere ayrılabilir.

[![RSS verileri döndüren bir Web hizmetini çağırmadan çıkış oluşturma.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**Şekil 3**: RSS verileri döndüren bir Web hizmetini çağırarak çıkış oluşturma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-web-services/_static/image9.png))

16 listesi, model ad alanında tanımlanan bir adres nesnesini çağıran istemci tarafı kodu örneğini gösterir, bunu güncelleştirilmiş verilerle doldurur ve bir CustomerDetails nesnesinin Address özelliğine atar. CustomerDetails nesnesi daha sonra işlenmek üzere Web hizmetine geçirilir.

**16 dökümünü yapın. İç içe karmaşık türleri kullanma**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>Sayfa yöntemleri oluşturma ve kullanma

Web Hizmetleri, ASP.NET AJAX sayfaları dahil olmak üzere çeşitli istemcilere yeniden sunulan hizmetleri kullanıma sunmak için harika bir yol sağlar. Ancak, bir sayfanın başka sayfalar tarafından kullanılmayan veya paylaşılmayan verileri alması gereken durumlar olabilir. Bu durumda, hizmetin yalnızca tek bir sayfa tarafından kullanıldığından, sayfanın verilere erişmesine izin vermek için bir. asmx dosyasının yapılması çok fazla kalabilir.

ASP.NET AJAX, tek başına. asmx dosyaları oluşturmadan Web hizmeti benzeri çağrılar yapmak için başka bir mekanizma sağlar. Bu, "sayfa yöntemleri" olarak adlandırılan bir teknik kullanılarak yapılır. Sayfa yöntemleri, doğrudan bir sayfada veya bir kod yanına eklenmiş olan ve bu dosyalara uygulanan WebMethod özniteliği uygulanmış olan, statik (VB.NET ' de paylaşılan) yöntemlerdir. WebMethod özniteliğini uygulayarak, çalışma zamanında dinamik olarak oluşturulan PageMethods adlı özel bir JavaScript nesnesi kullanılarak çağrılabilir. PageMethods nesnesi, JSON serileştirme/serisini kaldırma işleminden kalkan eden bir proxy görevi görür. PageMethods nesnesini kullanmak için ScriptManager 'ın EnablePageMethods özelliğini true olarak ayarlamanız gerektiğini unutmayın.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

17 listesi, ASP.NET Code-yanýndaki sınıfında iki sayfa yöntemi tanımlamayı gösteren bir örnek gösterir. Bu yöntemler \_ , Web sitesinin uygulama kodu klasöründe bulunan bir iş katmanı sınıfından veri alır.

**17. liste. Sayfa yöntemlerini tanımlama.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

ScriptManager sayfada Web yöntemlerinin varlığını algıladığında, daha önce bahsedilen PageMethods nesnesine dinamik bir başvuru oluşturur. Bir Web yöntemi çağırmak, PageMethods sınıfına ve ardından yönteminin adı ve geçirilmesi gereken tüm gerekli parametre verileri ile başvurularak gerçekleştirilir. 18 listesi, daha önce gösterilen iki sayfa yöntemini çağırma örneklerini gösterir.

**16 dökümünü yapın. Sayfa yöntemleri PageMethods JavaScript nesnesiyle çağrılıyor.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

PageMethods nesnesinin kullanılması, JavaScript proxy nesnesi kullanılmasına çok benzer. Önce sayfa yöntemine geçirilmesi gereken tüm parametre verilerini belirttikten sonra zaman uyumsuz çağrı döndürüldüğünde çağrılması gereken geri çağırma işlevini tanımlamanız gerekir. Hata geri çağırma de belirtilebilir (hata işleme örneği için 14. listeye bakın).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender ve ASP.NET AJAX araç seti

ASP.NET AJAX Toolkit (içinden kullanılabilir [http://ajax.asp.net](http://ajax.asp.net) ), Web hizmetlerine erişmek için kullanılabilecek çeşitli denetimler sunar. Özellikle araç seti, `AutoCompleteExtender` Web hizmetlerini çağırmak ve verileri sayfalarda hiçbir JavaScript kodu yazmadan göstermek için kullanılabilen adlı faydalı bir denetim içerir.

AutoCompleteExtender denetimi, bir TextBox 'ın varolan işlevselliğini genişletmek ve kullanıcıların aradığınız verileri daha kolay bulmalarına yardımcı olmak için kullanılabilir. Bir metin kutusuna yazdıkları için denetim bir Web hizmetini sorgulamak için kullanılabilir ve metin kutusunun altındaki sonuçları dinamik olarak gösterir. Şekil 4 ' te, bir destek uygulamasının Müşteri kimliklerini göstermek için AutoCompleteExtender denetimini kullanma örneği gösterilmektedir. Kullanıcı TextBox içine farklı karakterler yazdığında, bu, girişleri temel alınarak aşağıda gösterildiği gibi farklı öğeler görüntülenecektir. Kullanıcılar, istenen müşteri kimliğini seçebilir.

Bir ASP.NET AJAX sayfasında AutoCompleteExtender kullanmak, AjaxControlToolkit.dll derlemesinin Web sitesinin bin klasörüne eklenmesini gerektirir. Araç seti derlemesi eklendikten sonra, içerdiği denetimlerin bir uygulamadaki tüm sayfalar için kullanılabilir olması için web.config içinde başvurmak isteyeceksiniz. Bu, web.config Controls etiketinin içine aşağıdaki etiketi ekleyerek yapılabilir &lt; &gt; :

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

Yalnızca belirli bir sayfada denetimi kullanmanız gereken durumlarda, web.config güncelleştirmek yerine bir sayfanın en üstüne başvuru yönergesini ekleyerek başvurbaşvurabilirsiniz:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![AutoCompleteExtender denetimini kullanma.](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**Şekil 4**: AutoCompleteExtender denetimini kullanma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-web-services/_static/image12.png))

Web sitesi ASP.NET AJAX araç setini kullanacak şekilde yapılandırıldıktan sonra, bir AutoCompleteExtender denetimi sayfaya, normal bir ASP.NET sunucu denetimi eklediğinize benzer şekilde eklenebilir. Listeleme 19, bir Web hizmetini çağırmak için denetimin kullanılmasına ilişkin bir örnek gösterir.

**Listeleme 19. ASP.NET AJAX Toolkit AutoCompleteExtender denetimini kullanma.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender, sunucu denetimlerinde bulunan standart KIMLIK ve runat özellikleri de dahil olmak üzere birkaç farklı özelliğe sahiptir. Bunlara ek olarak, Web hizmeti veri sorgulanmadan önce son kullanıcının ne kadar karakter kullandığını tanımlamanızı sağlar. 19. listede gösterilen en düşük öncelik Refixlength özelliği, metin kutusuna bir karakter yazıldığında hizmetin çağrılmasına neden olur. Kullanıcı, metin kutusundaki karakterlerle eşleşen değerleri aramak için Web hizmeti her bir karakter yazdığında, bu değeri ayarlama konusunda dikkatli olmak isteyeceksiniz. Çağrılacak Web hizmeti ve hedef Web yöntemi sırasıyla ServicePath ve ServiceMethod özellikleri kullanılarak tanımlanır. Son olarak, TargetControlID özelliği, AutoCompleteExtender denetiminin hangi metin kutusuna bağlanacağını tanımlar.

Çağrılan Web hizmeti, daha önce anlatıldığı gibi ScriptService özniteliğinin uygulanmış olması ve hedef Web yönteminin prefixText ve Count adlı iki parametreyi kabul etmesi gerekir. PrefixText parametresi, son kullanıcı tarafından yazılan karakterleri temsil eder ve count parametresi döndürülecek öğe sayısını temsil eder (varsayılan değer 10 ' dur). 20 ' nin listelenmesi, AutoCompleteExtender denetimi tarafından çağrılan Getcustomerıds Web yönteminin bir örneğini göstermektedir. Web yöntemi, verileri filtrelemeyi ve eşleşen sonuçları döndürmeyi işleyen bir veri katmanı yöntemini çağıran bir iş katmanı yöntemi çağırır. Veri katmanı yöntemi için kod 21. listede gösterilmektedir.

**20 dökümünü yapın. AutoCompleteExtender denetiminden gönderilen verileri filtreleme.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**Listeleme 21. Son Kullanıcı girişine göre sonuçları filtreleme.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>Sonuç

ASP.NET AJAX, istek ve yanıt iletilerini işlemek için çok sayıda özel JavaScript kodu yazmadan Web hizmetlerini çağırmak için mükemmel destek sağlar. Bu makalede, .NET Web Hizmetleri 'nin JSON iletilerini işlemesini ve ScriptManager denetimini kullanarak JavaScript proxy 'leri nasıl tanımlanacağını belirlemek için AJAX 'ı nasıl etkinleştireceğinizi gördünüz. JavaScript proxy 'lerinin Web hizmetlerini çağırmak, basit ve karmaşık türleri işlemek ve hatalarla başa çıkmak için nasıl kullanılabileceğini de gördünüz. Son olarak, Web hizmeti çağrıları oluşturma ve kurma sürecini ve AutoCompleteExtender denetiminin, yazdıkları sürece son kullanıcılara nasıl yardım sağlayabileceğini basitleştirmek için sayfa yöntemlerinin nasıl kullanılabileceğini gördünüz. ASP.NET AJAX 'ta kullanılabilir olan UpdatePanel, basitliği nedeniyle birçok AJAX programcısı için tercih edilen denetim olacak olsa da, JavaScript proxy 'leri aracılığıyla Web hizmetlerinin nasıl çağrılacağını bilmek birçok uygulamada yararlı olabilir.

## <a name="bio"></a>Biyografisi

Dan Wahlin (ASP.NET ve XML Web Hizmetleri için Microsoft en değerli profesyonel), arabirim teknik eğitimi () adresindeki bir .NET geliştirme eğitmeni ve mimari danışmanıdır [http://www.interfacett.com](http://www.interfacett.com) . , ASP.NET geliştiricileri Web sitesi ([www.XMLforASP.net](http://www.XMLforASP.NET)) için XML, bir konuşmacı bürosuna ve birçok konferansda konuşuyor. Dan co-yazılan profesyonel Windows DNA (SaaS x), ASP.NET: Ipuçları, öğreticiler ve kod (Sams), ASP.NET 1,1 Insider Solutions, Professional ASP.NET 2,0 AJAX (SaaS x), ASP.NET 2,0 MVP Hacks ve yazılan XML for ASP.NET Developers (Sams). Kod, makale veya kitap yazmadığınızda, bol ve çocukları kullanarak müzik yazma ve kaydetme ve Golf ve basketbol topu oynatma.

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden bağlantı kurulabilirler

> [!div class="step-by-step"]
> [Önceki](understanding-asp-net-ajax-localization.md) 
>  [Sonraki](understanding-asp-net-ajax-debugging-capabilities.md)
