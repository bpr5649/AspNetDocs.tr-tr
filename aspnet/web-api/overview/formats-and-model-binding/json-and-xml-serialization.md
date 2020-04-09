---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API'de JSON ve XML Serileştirme - ASP.NET 4.x
author: MikeWasson
description: JSON ve XML formatters ASP.NET Web API için ASP.NET 4.x açıklar.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676225"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API'sinde JSON ve XML Serileştirme

Mike [Wasson](https://github.com/MikeWasson) tarafından

Bu makalede, ASP.NET Web API'sında JSON ve XML ön seçimlerini açıkçık

ASP.NET Web API'sinde, *medya türü formatter* şunları yapabilecek bir nesnedir:

- BIR HTTP ileti gövdesinden CLR nesnelerini okuma
- CLR nesnelerini http ileti gövdesine yazma

Web API hem JSON hem de XML için ortam tipi formatters sağlar. Çerçeve, varsayılan olarak bu formatters boru hattına ekler. İstemciler, HTTP isteğinin kabul üstbilgisinde JSON veya XML'i isteyebilir.

## <a name="contents"></a>İçindekiler

- [JSON Medya Tipi Formatter](#json_media_type_formatter)

    - [Salt Okunur Özellikler](#json_readonly)
    - [Tarih](#json_dates)
    - [Girintileme](#json_indenting)
    - [Deve Kılıfı](#json_camelcasing)
    - [Anonim ve Zayıf Yazılan Nesneler](#json_anon)
- [XML Medya Tipi Formatter](#xml_media_type_formatter)

    - [Salt Okunur Özellikler](#xml_readonly)
    - [Tarih](#xml_dates)
    - [Girintileme](#xml_indenting)
    - [XML Serializers Başına Ayar](#xml_pertype)
- [JSON veya XML Formatter kaldırma](#removing_the_json_or_xml_formatter)
- [Dairesel Nesne Başvurularının İşlemesi](#handling_circular_object_references)
- [Nesne Serileştirmeyi Test Etme](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Medya Tipi Formatter

JSON biçimlendirme **JsonMediaTypeFormatter** sınıfı tarafından sağlanmaktadır. Varsayılan olarak, **JsonMediaTypeFormatter** serileştirme gerçekleştirmek için [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) kitaplığını kullanır. Json.NET üçüncü taraf bir açık kaynak projesidir.

İsterseniz, **JsonMediaTypeFormatter** sınıfını Json.NET yerine **DataContractJsonSerializer'ı** kullanacak şekilde yapılandırabilirsiniz. Bunu yapmak için, **UseDataContractJsonSerializer** özelliğini **doğru**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON Seri Hale Getirme

Bu bölümde, varsayılan [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer kullanarak, JSON formatter bazı özel davranışları açıklanır. Bu, Json.NET kitaplığın kapsamlı bir belgelenmesi değildir; daha fazla bilgi için [Json.NET Belgeler'e](http://james.newtonking.com/projects/json/help/)bakın.

#### <a name="what-gets-serialized"></a>Ne Serialized alır?

Varsayılan olarak, tüm ortak özellikler ve alanlar serileştirilmiş JSON'a dahil edilir. Bir özelliği veya alanı atlamak için, **jsonIgnore** özniteliği ile süsleyin.

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

&quot;Bir kabul&quot; yaklaşımı tercih ederseniz, sınıfı **DataContract** özniteliğiyle süsleyin. Bu öznitelik varsa, **üyeler DataMember**yoksa yoksayılır. Özel üyeleri seri hale getirmek için **DataMember'ı** da kullanabilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Salt Okunur Özellikler

Salt okunur özellikler varsayılan olarak seri hale getirilir.

<a id="json_dates"></a>
### <a name="dates"></a>Dates

Varsayılan olarak, Json.NET [tarihleri ISO 8601](http://www.w3.org/TR/NOTE-datetime) biçiminde yazar. UTC'deki tarihler (Eşgüdümlü Evrensel Zaman) "Z" soneki ile yazılır. Yerel saatdeki tarihler arasında saat dilimi mahsulü içerir. Örneğin:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Varsayılan olarak, Json.NET saat dilimini korur. DateTimeZoneHandling özelliğini ayarlayarak bunu geçersiz kılabilirsiniz:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 yerine [Microsoft JSON tarih biçimini](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) kullanmayı tercih ederseniz, **DateFormatHandling** özelliğini serializer ayarlarında ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Girintileme

Girintilen JSON yazmak için **Biçimlendirme** ayarını **Biçimlendirme.Girini**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Deve Kılıfı

Deve kasalı JSON özellik adlarını yazmak için, veri modelinizi değiştirmeden **CamelCasePropertyNamesContractResolver'ı** serializer'a ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Anonim ve Zayıf Yazılan Nesneler

Eylem yöntemi anonim bir nesneyi döndürebilir ve JSON'a serileştirebilir. Örneğin:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Yanıt iletisi gövdesi aşağıdaki JSON'u içerir:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Web API'niz istemcilerden gevşek yapılandırılmış JSON nesneleri alıyorsa, istek gövdesini **Newtonsoft.Json.Linq.JObject** türüne dizileştirebilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

Ancak, genellikle güçlü dakti-si yazılan veri nesneleri kullanmak daha iyidir. Daha sonra verileri ayrıştırmanız gerekmez ve model doğrulamanın avantajlarından yararlanırsınız.

XML seri gösterici anonim türleri veya **JObject** örneklerini desteklemez. Bu özellikleri JSON verileriniz için kullanıyorsanız, bu makalede daha sonra açıklandığı gibi XML formatter'ı ardışık kaynaktan kaldırmanız gerekir.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML Medya Tipi Formatter

XML biçimlendirme **XmlMediaTypeFormatter** sınıfı tarafından sağlanır. Varsayılan olarak, **XmlMediaTypeFormatter** serileştirme gerçekleştirmek için **DataContractSerializer** sınıfını kullanır.

İsterseniz, **XmlMediaTypeFormatter'ı** **DataContractSerializer**yerine **XmlSerializer** kullanacak şekilde yapılandırabilirsiniz. Bunu yapmak için, **UseXmlSerializer** özelliğini **doğru**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer** sınıfı **DataContractSerializer'dan**daha dar bir tür kümesini destekler, ancak elde edilen XML üzerinde daha fazla denetim sağlar. Varolan bir XML şemasıyla eşleşmeniz gerekiyorsa **XmlSerializer** kullanmayı düşünün.

### <a name="xml-serialization"></a>XML seri hale getirme

Bu bölümde, varsayılan **DataContractSerializer**kullanarak XML formatter bazı özel davranışları açıklanır.

Varsayılan olarak, DataContractSerializer aşağıdaki gibi çalışır:

- Tüm ortak okuma/yazma özellikleri ve alanları seri hale getirilir. Bir özelliği veya alanı atlamak için, onu **IgnoreDataMember** özniteliğiyle süsleyin.
- Özel ve korunan üyeler serileştirilmeyecektir.
- Salt okunur özellikler seri hale getirilir. (Ancak, salt okunur toplama özelliğinin içeriği seri hale getirilmiştir.)
- Sınıf ve üye adları XML'de sınıf bildiriminde göründükleri gibi yazılır.
- Varsayılan bir XML ad alanı kullanılır.

Serileştirme üzerinde daha fazla denetime ihtiyacınız varsa, sınıfı **DataContract** özniteliğiyle dekore edebilirsiniz. Bu öznitelik mevcut olduğunda, sınıf aşağıdaki gibi serihale edilir:

- &quot;Yaklaşımı&quot; devre dışı bırakma: Özellikler ve alanlar varsayılan olarak serileştirilemez. Bir özelliği veya alanı seri hale getirmek için, **onu DataMember** özniteliğiyle süsleyin.
- Özel veya korumalı bir üyeyi seri hale getirmek için, **onu DataMember** özniteliğiyle süsleyin.
- Salt okunur özellikler seri hale getirilir.
- Sınıf adının XML'de nasıl göründüğünü değiştirmek için **DataContract** özniteliğindeki *Ad* parametresini ayarlayın.
- Bir üye adının XML'de nasıl görüneceğini değiştirmek **için, DataMember** özyüründeki *Ad* parametresini ayarlayın.
- XML ad alanını değiştirmek için **DataContract** *sınıfındaAd Alanı* parametresini ayarlayın.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Salt Okunur Özellikler

Salt okunur özellikler seri hale getirilir. Salt okunur bir özelliğin desteközel bir alanı varsa, özel alanı **DataMember** özniteliğiyle işaretleyebilirsiniz. Bu yaklaşım, **sınıftaki DataContract** özniteliğini gerektirir.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Dates

Tarihler ISO 8601 formatında yazılmıştır. Örneğin, &quot;2012-05-23T20:21:37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Girintileme

Girintilen XML yazmak için **Girintisi** **özelliğini doğru**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>XML Serializers Başına Ayar

Farklı CLR türleri için farklı XML serializers ayarlayabilirsiniz. Örneğin, geriye dönük uyumluluk için **XmlSerializer** gerektiren belirli bir veri nesneniz olabilir. Bu nesne için **XmlSerializer** kullanabilir ve diğer türler için **DataContractSerializer** kullanmaya devam edebilirsiniz.

Belirli bir tür için bir XML serializer ayarlamak **için, SetSerializer'ı**arayın.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Bir **XmlSerializer** veya **XmlObjectSerializer**türetilen herhangi bir nesne belirtebilirsiniz.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON veya XML Formatter kaldırma

Kullanmak istemiyorsanız, JSON formatter veya XML formatter formatters listesinden kaldırabilirsiniz. Bunu yapmak için ana nedenleri şunlardır:

- Web API yanıtlarınızı belirli bir ortam türüyle sınırlamak için. Örneğin, yalnızca JSON yanıtlarını desteklemeye ve XML formatter'ı kaldırmaya karar verebilirsiniz.
- Varsayılan formatter'ı özel bir formatter ile değiştirmek için. Örneğin, JSON formatter'ı kendi özel uygulamanızla değiştirebilirsiniz.

Aşağıdaki kod, varsayılan formatters kaldırmak için nasıl gösterir. Bunu Global.asax'ta tanımlanan **Uygulama\_Başlangıç** yönteminizden arayın.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Dairesel Nesne Başvurularının İşlemesi

Varsayılan olarak, JSON ve XML formatters değerleri olarak tüm nesneleri yazın. İki özellik aynı nesneye başvuruyorsa veya aynı nesne bir koleksiyonda iki kez görünüyorsa, madde nesneyi iki kez serileştirir. Nesne grafiğiniz döngüler içeriyorsa, bu belirli bir sorundur, çünkü serileştirici grafikte bir döngü algıladığında bir özel durum atar.

Aşağıdaki nesne modellerini ve denetleyiciyi düşünün.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Bu eylemi çağırmak, formatter'ın istemciye bir durum kodu 500 (İç Sunucu Hatası) yanıtı anlamına gelen bir özel durum atmasını sağlar.

JSON'daki nesne başvurularını korumak için Global.asax dosyasındaki **Uygulama\_Başlat** yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Şimdi denetleyici eylem bu gibi görünüyor JSON dönecektir:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Serileştiricinin her iki &quot;nesneye de $id&quot; özelliği eklediğine dikkat edin. Ayrıca, Employee.Department özelliğinin bir döngü oluşturduğunu algılar, bu nedenle değeri bir nesne&quot;&quot;başvurusuyla değiştirir: { $ref :&quot;1&quot;}.

> [!NOTE]
> Nesne başvuruları JSON'da standart değildir. Bu özelliği kullanmadan önce, müşterilerinizin sonuçları ayrıştırıp ayrıştıramayacağını düşünün. Grafiklerden döngüleri kaldırmak daha iyi olabilir. Örneğin, Çalışan'dan Departmana bağlantı bu örnekte gerçekten gerekli değildir.

XML'de nesne başvurularını korumak için iki seçeneğiniz vardır. Daha basit seçenek model `[DataContract(IsReference=true)]` sınıfınıza eklemektir. *IsReference* parametresi nesne başvuruları sağlar. **DataContract'ın** serileştirmeyi devre dışı bırakma özelliğine sahip olduğunu unutmayın, bu nedenle özelliklere **DataMember** öznitelikleri eklemeniz de gerekir:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Şimdi formatter aşağıdaki benzer XML üretecek:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Model sınıfınızdaki özniteliklerden kaçınmak istiyorsanız, başka bir seçenek daha vardır: Yeni bir türe özgü **DataContractSerializer** örneği oluşturun ve constructor'da **geçerli** olan *ObjectReferences'ı koruyun'* u ayarlayın. Daha sonra bu örneği XML ortam türü nde bir tür başına serileştirici olarak ayarlayın. Aşağıdaki kod, bunun nasıl yapılacağını gösterir:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Nesne Serileştirmeyi Test Etme

Web API'nizi tasarlarken, veri nesnelerinizin nasıl seri hale getirileceğini test etmek yararlıdır. Bunu bir denetleyici oluşturmadan veya bir denetleyici eylemi çağırmadan yapabilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
