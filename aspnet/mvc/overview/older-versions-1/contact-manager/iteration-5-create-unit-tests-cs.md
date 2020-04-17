---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: 'Yineleme #5 – Birim testleri oluşturma (C#) | Microsoft Dokümanlar'
author: rick-anderson
description: Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: c005a8ffc3b09c126d796f2feb74d402cb784aa2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542358"
---
# <a name="iteration-5--create-unit-tests-c"></a>5. Yineleme – Birim testleri oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (C#)

Öğreticiler bu dizi, biz baştan sona tüm Bir İletişim Yönetimi uygulaması oluşturmak. İletişim Yöneticisi uygulaması, kişi listesi için kişi bilgilerini (adlar, telefon numaraları ve e-posta adresleri) depolamanızı sağlar.

Uygulamayı birden çok yineleme üzerine oluşturuyoruz. Her yineleme ile, yavaş yavaş uygulama geliştirmek. Bu çoklu yineleme yaklaşımının amacı, her değişikliğin nedenini anlamanızı sağlamaktır.

- Yineleme #1 - Uygulamayı oluşturun. İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

- Yineleme #2 - Uygulama güzel görünmesini sağlamak. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

- Yineleme #3 - Form doğrulama ekleyin. Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

- Yineleme #4 - Uygulamayı gevşek bir şekilde biraraya getirin. Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

- Yineleme #5 - Birim testleri oluşturun. Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

- Yineleme #6 - Test odaklı geliştirme yi kullanın. Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

- Yineleme #7 - Ajax işlevselliği ekleyin. Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="this-iteration"></a>Bu Yineleme

Contact Manager uygulamasının önceki yinelemesinde, uygulamayı daha gevşek bir şekilde birleştiğinde yeniden ele aldık. Uygulamayı farklı denetleyici, hizmet ve depo katmanlarına ayırdık. Her katman, arayüzler aracılığıyla altındaki katmanla etkileşime girer.

Uygulamanın bakımını ve değiştirilmesini kolaylaştırmak için uygulamayı yeniden düzenlemeyaptık. Örneğin, yeni bir veri erişim teknolojisi kullanmamız gerekirse, denetleyiciye veya hizmet katmanına dokunmadan depo katmanını değiştirebiliriz. İletişim Yöneticisi'ni gevşek bir şekilde biraraya getirerek, uygulamayı değiştirmek için daha esnek hale getirdik.

Ancak, İletişim Yöneticisi uygulamasına yeni bir özellik eklememiz gerektiğinde ne olur? Ya da bir hatayı düzelttediğimiz zaman ne olur? Bir üzücü, ama iyi kanıtlanmış, kod yazma gerçeği, kod dokunduğunuzda yeni hatalar tanıtma riski oluşturmak olduğunu.

Örneğin, iyi bir gün yöneticiniz Kişi Yöneticisi'ne yeni bir özellik eklemenizi isteyebilir. İletişim Grupları için destek eklemenizi istiyor. Kullanıcıların kişilerini Arkadaşlar, İş ve benzeri gruplar halinde düzenlemelerini sağlamanızı istiyor.

Bu yeni özelliği uygulamak için, İletişim Yöneticisi uygulamasının üç katmanını da değiştirmeniz gerekir. Denetleyicilere, hizmet katmanına ve depoya yeni işlevler eklemeniz gerekir. Kodu değiştirmeye başlar başlamaz, daha önce çalışan işlevselliği bozma riskine girersiniz.

Uygulamamızı, önceki yinelemede yaptığımız gibi ayrı katmanlara ayırmak iyi bir şeydi. Bu iyi bir şeydi çünkü uygulamanın geri kalanına dokunmadan tüm katmanlarda değişiklik yapmamızı sağlıyor. Ancak, bir katman içindeki kodu niçin korumayı ve değiştirmeyi kolaylaştırmak istiyorsanız, kod için birim testleri oluşturmanız gerekir.

Tek bir kod birimini test etmek için bir birim testi kullanırsınız. Bu kod birimleri tüm uygulama katmanlarından daha küçüktür. Genellikle, kodunuzda belirli bir yöntemin beklediğiniz şekilde çalışıp kullanmadığını doğrulamak için bir birim testi kullanırsınız. Örneğin, ContactManagerService sınıfı tarafından açığa çıkarılan CreateContact() yöntemi için bir birim testi oluşturursunuz.

Bir uygulama için birim testleri tıpkı bir güvenlik ağı gibi çalışır. Bir uygulamada kodu değiştirdiğinizde, değişikliğin varolan işlevselliği bozup bozmadığını denetlemek için bir dizi birim testi çalıştırabilirsiniz. Birim testleri, kodunuzu değiştirmek için güvenli hale getirin. Birim testleri, uygulamanızdaki tüm kodun değiştirilmesine karşı daha esnek olmasını sağlar.

Bu yinelemede, İletişim Yöneticisi uygulamamıza birim testleri ekliyoruz. Bu şekilde, bir sonraki yinelemede, varolan işlevleri bozma endişesi duymadan Uygulamamıza Kişi Grupları ekleyebiliriz.

> [!NOTE] 
> 
> NUnit, xUnit.net ve MbUnit dahil olmak üzere çeşitli birim test çerçeveleri vardır. Bu eğitimde Visual Studio ile birlikte birim test çerçevesini kullanıyoruz. Ancak, bu alternatif çerçevelerden birini kolayca kullanabilirsiniz.

## <a name="what-gets-tested"></a>Ne Test Gets

Mükemmel dünyada, tüm kodunuzu birim testleri kapsamında olacaktır. Mükemmel dünyada, mükemmel bir güvenlik ağına sahip olurdunuz. Uygulamanızdaki herhangi bir kod satırını değiştirebilir ve birim testlerinizi gerçekleştirerek, değişikliğin varolan işlevselliği bozup kırmadığını anında anlayın.

Ancak, mükemmel bir dünyada yaşamıyoruz. Uygulamada, birim testleri yazarken, iş mantığınız için testler yazmaya odaklanırsınız (örneğin, doğrulama mantığı). Özellikle, veri erişim mantığınız veya görünüm mantığınız için birim testleri *yazmazsınız.*

Yararlı olmak için birim testleri çok hızlı bir şekilde yürütülmelidir. Bir uygulama için yüzlerce (hatta binlerce) birim testi kolayca biriktirebilirsiniz. Birim testlerinin çalıştırılması uzun sürerse, bunları yürütmekten kaçınırsınız. Başka bir deyişle, uzun süren birim testleri günlük kodlama amaçlı işe yaramaz.

Bu nedenle, genellikle bir veritabanı ile etkileşim kodu için birim testleri yazmayın. Canlı bir veritabanına karşı yüzlerce birim testi çalıştırmak çok yavaş olur. Bunun yerine, veritabanınızla alay eder ve sahte veritabanıyla etkileşimedebilen kod yazarsınız (aşağıdaki veritabanıyla alay etme konusunu tartışıyoruz).

Benzer bir nedenle, genellikle görünümler için birim testleri yazmayın. Görünümü sınamak için bir web sunucusu döndürmeniz gerekir. Bir web sunucusu oluşturmak nispeten yavaş bir işlem olduğundan, görüşleriniz için birim testleri oluşturma nız önerilmez.

Görünümünüz karmaşık mantık içeriyorsa, mantığı Yardımcı yöntemlere taşımayı düşünmelisiniz. Bir web sunucusu döndürmeden çalıştırılabilen Yardımcı yöntemleri için birim testleri yazabilirsiniz.

> [!NOTE] 
> 
> Birim testleri yazarken veri erişim mantığı veya görünüm mantığı için testler yazmak iyi bir fikir olmasa da, işlevsel veya tümleştirme testleri yaparken bu testler çok değerli olabilir.

> [!NOTE] 
> 
> ASP.NET MVC Web Formları Görünüm Motorudur. Web Formlarını Görüntüle Altyapısı bir web sunucusuna bağımlı olsa da, diğer görünüm motorları olmayabilir.

## <a name="using-a-mock-object-framework"></a>Sahte Nesne Çerçevesi Kullanma

Birim testleri yaparken, hemen hemen her zaman sahte nesne çerçevesinden yararlanmanız gerekir. Mock Object çerçevesi, uygulamanızdaki sınıflar için alaylar ve saplamalar oluşturmanıza olanak tanır.

Örneğin, depo sınıfınızın sahte sürümünü oluşturmak için Sahte Nesne çerçevesini kullanabilirsiniz. Bu şekilde, birim testlerinizde gerçek depo sınıfı yerine sahte depo sınıfını kullanabilirsiniz. Sahte depoyu kullanmak, birim testini yürürken veritabanı kodunu yürütmekten kaçınmanızı sağlar.

Visual Studio sahte nesne çerçevesi içermez. Ancak, .NET çerçevesi için birkaç ticari ve açık kaynak Sahte Nesne çerçevesi vardır:

1. Moq - Bu çerçeve açık kaynak BSD lisansı altında mevcuttur. Sen Moq indirebilirsiniz [https://code.google.com/p/moq/](https://code.google.com/p/moq/).
2. Rhino Mocks - Bu çerçeve açık kaynak BSD lisansı altında mevcuttur. Rhino Mocks'ı [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)buradan indirebilirsiniz.
3. Typemock Isolator - Bu ticari bir çerçevedir. Bir deneme sürümünü ' [http://www.typemock.com/](http://www.typemock.com/)den indirebilirsiniz.

Bu öğreticide, Ben Moq kullanmaya karar verdi. Ancak, Temas Yöneticisi uygulaması için Mock nesneleri oluşturmak için Rhino Mocks veya Typemock Isolator'u kolayca kullanabilirsiniz.

Moq'u kullanmadan önce aşağıdaki adımları tamamlamanız gerekir:

1. .
2. İndirme işleminin üst ünü açmadan önce, dosyayı sağ tıklattığınızdan ve **Engeli Kaldır** etiketli düğmeyi tıklattığınızdan emin olun (Bkz. Şekil 1).
3. İndirme işleminin zip'ini aç.
4. ContactManager.Tests projesindeki Başvurular klasörüne sağ tıklayarak ve **Referans Ekle'yi**seçerek Moq derlemesine bir başvuru ekleyin. Gözat sekmesinin altında, Moq'un fermuarını açtığınızda klasöre göz atın ve Moq.dll derlemesini seçin. **Tamam** düğmesini tıklatın.
5. Bu adımları tamamladıktan sonra, Referanslar klasörünüz Şekil 2 gibi görünmelidir.

[![Engellemeyi Kaldırma Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**Şekil 01**: Engellemeyi Kaldırma Moq ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-5-create-unit-tests-cs/_static/image2.png))

[![Moq ekledikten sonra referanslar](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**Şekil 02**: Moq'u ekledikten sonra referanslar ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-5-create-unit-tests-cs/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>Hizmet Katmanı için Birim Testleri Oluşturma

İletişim Yöneticisi uygulamamızın hizmet katmanı için bir dizi birim testi oluşturarak başlayalım. Doğrulama mantığımızı doğrulamak için bu testleri kullanacağız.

ContactManager.Tests projesinde Modeller adlı yeni bir klasör oluşturun. Ardından, Modeller klasörüne sağ tıklayın ve **Ekle, Yeni Test'i**seçin. Şekil 3'te gösterilen **Yeni Test Ekle** iletişim kutusu görüntülenir. Birim **Testi** şablonunu seçin ve yeni test ContactManagerServiceTest.cs. Yeni testinizi Test Projenize eklemek için **Tamam** düğmesini tıklatın.

> [!NOTE] 
> 
> Genel olarak, Test Projenizin klasör yapısının ASP.NET MVC projenizin klasör yapısıyla eşleşmesini istiyorsunuz. Örneğin, denetleyici testlerini denetleyiciler klasörüne, model testlerini modeller klasörüne ve benzeri bir yere yerlikirsiniz.

[![Modeller\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**Şekil 03**: Modeller\ContactManagerServiceTest.cs([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-5-create-unit-tests-cs/_static/image6.png))

Başlangıçta, ContactManagerService sınıfı tarafından açığa çıkarılan CreateContact() yöntemini test etmek istiyoruz. Aşağıdaki beş testi oluşturacağız:

- CreateContact() - CreateContact() için geçerli bir Kişi yönteme geçirildiğinde doğru değeri döndüren testler.
- CreateContactGerekliFirstName() - Eksik bir ilk adı olan bir Kişi CreateContact() yöntemine geçirildiğinde model durumuna bir hata iletisinin ekildiğini sınar.
- CreateContactRequiredLastName() - Eksik soyadı olan bir Kişi CreateContact() yöntemine geçirildiğinde model durumuna bir hata iletisinin ekildiğini sınar.
- CreateContactInvalidPhone() - Geçersiz bir telefon numarasına sahip bir Kişi CreateContact() yöntemine geçirildiğinde model durumuna bir hata iletisinin ekildiğini test eder.
- CreateContactInvalidEmail() - Geçersiz bir e-posta adresi olan bir Kişi CreateContact() yöntemine geçirildiğinde model durumuna bir hata iletisinin ekildiğini sınar...

İlk sınama, geçerli bir Kişi doğrulama hatası oluşturmadığını doğrular. Kalan testler doğrulama kurallarının her birini denetler.

Bu testlerin kodu Listeleme 1'de bulunur.

**Listeleme 1 - Modeller\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

Listeleme 1'de Kişi sınıfını kullandığımız için, Test projemize Microsoft Varlık Çerçevesi'ne bir başvuru eklememiz gerekir. System.Data.Entity derlemesine bir başvuru ekleyin.

Listeleme 1, [TestInitialize] özniteliği ile dekore edilmiş Initialize() adlı bir yöntem içerir. Bu yöntem, birim testlerinin her biri çalıştırılmadan önce otomatik olarak çağrılır (birim testlerinin her biri sağdan önce 5 kez çağrılır). Initialize() yöntemi, aşağıdaki kod satırıyla sahte bir depo oluşturur:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

Bu kod satırı, IContactManagerRepository arabiriminden sahte bir depo oluşturmak için Moq çerçevesini kullanır. Sahte depo, her birim testi çalıştırıldığında veritabanına erişmemek için gerçek EntityContactManagerRepository yerine kullanılır. Sahte depo IContactManagerRepository arabiriminin yöntemlerini uygular, ancak yöntemler aslında hiçbir şey yapmaz.

> [!NOTE] 
> 
> Moq çerçevesini kullanırken mockRepository ve \_ \_mockRepository.Object arasında bir ayrım vardır. Eski mock depo&lt;nasıl olacağını belirtmek için&gt; yöntemler içeren Mock IContactManagerRepository sınıf anlamına gelir. İkincisi, IContactManagerRepository arabirimini uygulayan gerçek sahte depoyu ifade eder.

Mock deposu, ContactManagerService sınıfının bir örneğini oluştururken Initialize() yönteminde kullanılır. Tüm tek tek birim testleri ContactManagerService sınıfının bu örneğini kullanır.

Listeleme 1, birim testlerinin her birine karşılık gelen beş yöntem içerir. Bu yöntemlerin her biri [TestMethod] özniteliği ile dekore edilmiştir. Birim testlerini çalıştırdığınızda, bu özniteliği olan tüm yöntemler çağrılır. Başka bir deyişle, [TestMethod] özniteliği ile dekore edilmiş herhangi bir yöntem bir birim testidir.

CreateContact() adlı ilk birim testi, Kişi sınıfının geçerli bir örneği yönteme geçirildiğinde CreateContact() aramasının değeri doğru döndürür doğrular. Test, Kişi sınıfının bir örneğini oluşturur, CreateContact() yöntemini çağırır ve CreateContact() değerini doğru döndürür doğrular.

Kalan testler, CreateContact() yöntemi geçersiz bir Kişi ile çağrıldığında yöntemin yanlış döndürür ve beklenen doğrulama hatası iletisinin model durumuna eklendiğinde doğrulanır. Örneğin, CreateContactRequiredFirstName() testi, FirstName özelliği için boş bir dize içeren Kişi sınıfının bir örneğini oluşturur. Ardından, CreateContact() yöntemi geçersiz Kişi ile çağrılır. Son olarak, test CreateContact() yanlış döndürür ve bu model durumu beklenen doğrulama hatası iletisi "İlk ad gereklidir" içerir doğrular.

Menü seçeneği **Test, Çalıştır, Tüm Testler in Solution (CTRL+R, A)** seçeneğini seçerek Listeleme 1'deki birim testlerini çalıştırabilirsiniz. Testlerin sonuçları Test Sonuçları penceresinde görüntülenir (bkz. Şekil 4).

[![Test Sonuçları](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**Şekil 04**: Test Sonuçları ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-5-create-unit-tests-cs/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>Denetleyiciler için Birim Testleri Oluşturma

ASP.NETMVC uygulaması kullanıcı etkileşiminin akışını kontrol edin. Bir denetleyiciyi sınarken, denetleyicinin doğru eylem sonucunu döndürüp döndürmediğini ve verileri görüntüleyip görüntülemediğini test etmek istersiniz. Denetleyicinin model sınıflarıyla beklenen şekilde etkileşimde bulunup bulunmayacağını da test etmek isteyebilirsiniz.

Örneğin, Listeleme 2, İletişim denetleyicisi Oluşturma() yöntemi için iki birim testi içerir. İlk birim testi, geçerli bir Kişi Create() yöntemine geçildiğinde Create() yönteminin Dizin eylemine yönlendirildiğini doğrular. Başka bir deyişle, geçerli bir Kişi geçtiğinde, Create() yöntemi Dizin eylemini temsil eden bir ReDirectToRouteResult döndürmelidir.

Denetleyici katmanını test ederken ContactManager hizmet katmanını test etmek istemiyoruz. Bu nedenle, Initialize yönteminde aşağıdaki kodile hizmet katmanı alay:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

CreateValidContact() birim testinde, hizmet katmanı createcontact() yöntemini aşağıdaki kod satırıyla arama davranışıyla alay ediyoruz:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

Bu kod satırı, CreateContact() yöntemi çağrıldığında sahte ContactManager hizmetinin doğru değeri döndürmesine neden olur. Hizmet katmanıyla alay ederek, hizmet katmanında herhangi bir kod yürütmeye gerek kalmadan denetleyicimizin davranışını sınayabiliriz.

İkinci birim testi, geçersiz bir kişi yönteme geçtiğinde Create() eyleminin Create görünümünü döndürür doğrular. Hizmet katmanı CreateContact() yönteminin aşağıdaki kod satırıyla yanlış değeri döndürmesine neden oluruz:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Create() yöntemi beklediğimiz gibi olursa, hizmet katmanı değeri false döndürdüğünde Create görünümünü döndürmelidir. Bu şekilde, denetleyici Create görünümünde doğrulama hatası iletilerini görüntüleyebilir ve kullanıcının geçersiz Kişi özelliklerini düzeltme şansı vardır.

Denetleyicileriniz için birim testleri oluşturmayı planlıyorsanız, denetleyici eylemlerinizden açık görünüm adlarını döndürmeniz gerekir. Örneğin, şu şekilde bir görünüm döndürmeyin:

return View();

Bunun yerine, görünümü şu şekilde döndürün:

return View("Create");

Bir görünümü döndürürken açık değilseniz, ViewResult.ViewName özelliği boş bir dize döndürür.

**Listeleme 2 - Denetleyiciler\ContactControllerTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>Özet

Bu yinelemede, İletişim Yöneticisi uygulamamız için birim testleri oluşturduk. Uygulamamızın hala beklediğimiz şekilde davrandığını doğrulamak için bu birim testlerini istediğimiz zaman çalıştırabiliriz. Birim testleri, uygulamamızı gelecekte güvenli bir şekilde değiştirmemizi sağlayan bir güvenlik ağı görevi göremez.

İki birim testi oluşturduk. İlk olarak, hizmet katmanımız için birim testleri oluşturarak doğrulama mantığımızı test ettik. Daha sonra, denetleyici katmanımız için birim testleri oluşturarak akış kontrol mantığımızı test ettik. Hizmet katmanımızı test ederken, depo katmanımızla alay ederek hizmet katmanımız için testlerimizi depo katmanımızdan izole ettik. Denetleyici katmanını test ederken, servis katmanıyla alay ederek kontrolör katmanımız için testlerimizi izole ettik.

Bir sonraki yinelemede, Kişi Yöneticisi uygulamasını Kişi Grupları'nı destekleyebilecek şekilde değiştiririz. Bu yeni işlevselliği, test odaklı geliştirme adı verilen bir yazılım tasarım işlemi kullanarak uygulamamıza ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](iteration-4-make-the-application-loosely-coupled-cs.md)
> [Sonraki](iteration-6-use-test-driven-development-cs.md)
