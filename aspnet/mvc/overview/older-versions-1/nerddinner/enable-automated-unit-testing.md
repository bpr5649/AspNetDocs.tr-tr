---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Otomatik Birim Testini Etkinleştir | Microsoft Dokümanlar
author: rick-anderson
description: Adım 12, NerdDinner işlevselliğimizi doğrulayan ve bize değişiklik yapma güvenini kazandıracak bir dizi otomatik birim testinin nasıl geliştirilebildiğini gösterir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541474"
---
# <a name="enable-automated-unit-testing"></a>Otomatik Birim Testini Etkinleştirme

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 12 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 12, NerdDinner işlevselliğimizi doğrulayan ve gelecekte uygulamada değişiklik ve iyileştirmeler yapma konusunda bize güven verecek bir dizi otomatik birim testinin nasıl geliştirilebildiğini gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner Adım 12: Ünite Testi

NerdDinner işlevselliğimizi doğrulayan ve gelecekte uygulamada değişiklik ve iyileştirmeler yapmamız için bize güven verecek bir dizi otomatik birim testi geliştirelim.

### <a name="why-unit-test"></a>Neden Ünite Testi?

Bir sabah işe giderken üzerinde çalıştığınız bir uygulama hakkında ani bir ilham ışığı var. Uygulamayı önemli ölçüde daha iyi hale getirecek bir değişiklik olduğunu fark. Kodu temizleyen, yeni bir özellik ekleyen veya bir hatayı düzelten bir yeniden düzenleme olabilir.

Bilgisayarınıza vardığınızda karşınıza çıkan soru şudur: "Bu gelişmeyi yapmak ne kadar güvenli?" Değişiklik yapmanın yan etkileri varsa veya bir şey kırarsa ne olur? Değişiklik basit olabilir ve uygulanması yalnızca birkaç dakika sürebilir, ancak tüm uygulama senaryolarının el ile test edilmesi saatler sürerse ne olur? Ya bir senaryoyu örtbas etmeyi unutursanız ve bozuk bir uygulama üretime geçerse? Bu gelişmegerçekten tüm çaba değer mi?

Otomatik birim testleri, uygulamalarınızı sürekli olarak geliştirmenizi ve üzerinde çalıştığınız koddan korkmanızı sağlayan bir güvenlik ağı sağlayabilir. İşlevselliği hızla doğrulayan otomatik testlere sahip olmak, güvenle kod yapmanızı sağlar ve aksi takdirde bunu yaparken kendini rahat hissetmemiş olabileceğiniz iyileştirmeler yapmanızı sağlar. Ayrıca daha bakımlı ve daha uzun bir ömür esahip çözümler oluşturmaya yardımcı olur - bu da yatırımın çok daha yüksek bir getirisine yol açar.

MVC Framework ASP.NET, uygulama işlevselliğini birleştirmeyi kolay ve doğal hale getirir. Ayrıca, test tabanlı geliştirmeyi sağlayan bir Test Tabanlı Geliştirme (TDD) iş akışı sağlar.

### <a name="nerddinnertests-project"></a>NerdDinner.Tests Projesi

Bu eğitimin başında NerdDinner uygulamamızı oluşturduğumuzda, uygulama projesiyle birlikte bir birim test projesi oluşturmak isteyip istemediğimizi soran bir iletişim kutusu yla istendi:

![](enable-automated-unit-testing/_static/image1.png)

"Evet, bir birim test projesi oluştur" radyo düğmesini seçtik – bu da çözümümüze bir "NerdDinner.Tests" projesinin eklenmesiyle sonuçlandı:

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Tests projesi, NerdDinner uygulama proje derlemesine başvurur ve uygulama işlevselliğini doğrulayan otomatik testler eklememizi sağlar.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Yemek Modeli Sınıfımız İçin Ünite Testleri Oluşturma

Model katmanımızı oluşturduğumuzda oluşturduğumuz Akşam Yemeği sınıfını doğrulayan NerdDinner.Tests projemize bazı testler ekleyelim.

Modelle ilgili testlerimizi yerleştireceğimiz "Modeller" adlı test projemizde yeni bir klasör oluşturarak başlayacağız. Daha sonra klasöre sağ tıklayıp **&gt;Yeni Test Ekle** menüsü komutunu seçeceğiz. Bu, "Yeni Test Ekle" iletişim kutusunu gündeme getirir.

Bir "Birim Testi" oluşturmayı ve adını "DinnerTest.cs" olarak adlandıracağız:

![](enable-automated-unit-testing/_static/image3.png)

"Ok" düğmesini tıklattığımızda Visual Studio projeye bir DinnerTest.cs dosyası ekler (ve açar:

![](enable-automated-unit-testing/_static/image4.png)

Varsayılan Visual Studio birim test şablonu içinde biraz dağınık bulmak kazan plakakodu bir demet vardır. Aşağıdaki kodu içerecek şekilde temizleyelim:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

Yukarıdaki DinnerTest sınıfındaki [TestClass] özniteliği, bunu testleri içeren bir sınıf olarak tanımlar, ayrıca isteğe bağlı test başlatma ve yıkma kodu. Üzerinde [TestMethod] özniteliği olan genel yöntemler ekleyerek içindeki testleri tanımlayabiliriz.

Aşağıda bizim Akşam Yemeği sınıf egzersiz ekleyeceğiz iki testin ilki dir. İlk test, tüm özellikler doğru ayarlanmadan yeni bir Akşam Yemeği oluşturulursa Akşam Yemeğimizin geçersiz olduğunu doğrular. İkinci test, Akşam Yemeğimiz geçerli değerlerle ayarlanmış tüm özelliklere sahip olduğunda geçerli olduğunu doğrular:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Yukarıda test adlarımızın çok açık (ve biraz ayrıntılı) olduğunu fark edeceksiniz. Bunu yapıyoruz çünkü yüzlerce veya binlerce küçük test oluşturabiliriz ve her birinin niyetini ve davranışını hızlı bir şekilde belirlemeyi kolaylaştırmak istiyoruz (özellikle de bir test koşucusundaki başarısızlıklistesine bakarken). Test adları, test ettikleri işlevsellikten sonra adlandırılmalıdır. Yukarıda "İsim\_Fiil Olmalı"\_adlandırma deseni kullanıyoruz.

Testleri "Düzenle, Harekete, İddia" anlamına gelen "AAA" test modelini kullanarak yapılandırıyoruz:

- Düzenleme: Test edilen üniteyi ayarlama
- Yasa: Üniteyi test altında çalıştırın ve sonuçları yakalayın
- Assert: Davranışı doğrulayın

Testleri yazarken bireysel testlerin çok fazla yapmasından kaçınmak isteriz. Bunun yerine her test yalnızca tek bir kavramı doğrulamalıdır (bu da hataların nedenini saptamayı çok daha kolay hale getirir). İyi bir kılavuz denemek ve sadece her test için tek bir assert deyimi var. Bir test yönteminde birden fazla assert deyiminiz varsa, bunların hepsinin aynı kavramı test etmek için kullanıldığından emin olun. Şüpheye düştüğünüzde, başka bir test yapın.

### <a name="running-tests"></a>Testleri Çalıştırma

Visual Studio 2008 Professional (ve daha yüksek sürümler), IDE içinde Visual Studio Unit Test projelerini çalıştırmak için kullanılabilecek yerleşik bir test koşucusu içerir. Tüm birim testlerimizi çalıştırmak için Çözüm menüsündeki **&gt;&gt;Tüm Testleri** (veya Ctrl R, A yazın) seçebiliriz. Ya da alternatif olarak imlecimizi belirli bir test sınıfı veya test yöntemi içinde konumlandırabilir ve birim testlerinin bir alt kümesini çalıştırmak için **Geçerli Bağlam menüsünde Test-Çalıştır&gt;&gt;** testlerini (veya Ctrl R, T yazın) kullanabiliriz.

İmlecimizi DinnerTest sınıfına yerleştirelim ve az önce tanımladığımız iki testi çalıştırmak için "Ctrl R, T" yazalım. Bunu yaptığımızda Visual Studio'da bir "Test Sonuçları" penceresi görünecek ve test çalışmamızın sonuçlarını bu pencerede listelenmiş olarak göreceğiz:

![](enable-automated-unit-testing/_static/image5.png)

*Not: VS test sonuçları penceresi varsayılan olarak Sınıf Adı sütununu göstermez. Bunu, Test Sonuçları penceresinde sağ tıklayarak ve Sütunekle/Kaldır menüsü komutunu kullanarak ekleyebilirsiniz.*

Bizim iki test çalıştırmak için saniyenin sadece bir kısmını aldı - ve gördüğünüz gibi her ikisi de geçti. Artık, Dinner sınıfına eklediğimiz isUserHost() ve IsUserRegistered() gibi iki yardımcı yöntemi kapsayan ve belirli kural doğrulamalarını doğrulayan ek testler oluşturarak bunları genişletebiliriz. Akşam Yemeği sınıfı için tüm bu testlerin yerinde olması, gelecekte buna yeni iş kuralları ve doğrulamalar eklemeyi çok daha kolay ve güvenli hale getirecektir. Yeni kural mantığımızı Akşam Yemeği'ne ekleyebiliriz ve saniyeler içinde önceki mantık işlevselliğimizin hiçbirini kırmadığını doğrulayabiliriz.

Açıklayıcı bir test adı kullanmanın, her testin neyi doğruladığıyla hızlı bir şekilde anlamayı nasıl kolaylaştırdığını fark edin. **Araçlar-&gt;Seçenekler** menüsü komutunu kullanmanızı, Test&gt;Araçları- Test Yürütme yapılandırma ekranını açmanızı ve "Başarısız veya sonuçsuz birim test sonucunu çift tıklatma test kutusunda ki hata noktasını görüntüler" onay kutusunu kontrol etmenizi öneririm. Bu, test sonuçları penceresindeki bir başarısızlığa çift tıklamanızı ve hemen ileri hatasına atlamanızı sağlar.

### <a name="creating-dinnerscontroller-unit-tests"></a>DinnersController Birim Testleri Oluşturma

Şimdi DinnersController işlevselliğimizi doğrulayan bazı birim testleri oluşturalım. Test projemizdeki "Denetleyiciler" klasörüne sağ tıklayarak başlayacağız ve ardından **Ekle-Yeni&gt;Test** menüsü komutunu seçeceğiz. Bir "Birim Testi" oluşturacağız ve adını "DinnersControllerTest.cs" koyacağız.

DinnersController'daki Ayrıntılar() eylem yöntemini doğrulayan iki test yöntemi oluşturacağız. İlki, varolan bir Akşam Yemeği istendiğinde Görünümün döndürüldettiğini doğrular. İkinci, var olmayan bir Akşam Yemeği istendiğinde "Bulunduyama" görünümünün döndürüldeceğini doğrular:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

Yukarıdaki kod temiz derlenir. Testleri çalıştırdığımızda, ikisi de başarısız oluyor:

![](enable-automated-unit-testing/_static/image6.png)

Hata iletilerine bakacak olursak, testlerin başarısız olmasının nedeninin DinnersRepository sınıfımızın bir veritabanına bağlanamaması olduğunu görürsünüz. NerdDinner uygulamamız, NerdDinner uygulama projesinin \App\_Data dizininin altında yaşayan yerel bir SQL Server Express dosyasına bağlantı dizesini kullanıyor. NerdDinner.Tests projemiz farklı bir dizinde çalıştığından ve uygulama projesinden sonra çalıştığından, bağlantı dizimizin göreli yol konumu yanlıştır.

Bunu, SQL Express veritabanı dosyasını test projemize kopyalayarak düzeltebilir ve test projemizin App.config'ine uygun bir test bağlantısı dizesi *ekleyebiliriz.* Bu, yukarıdaki testlerin engelini kaldırıp çalıştırılabırdı.

Gerçek bir veritabanı kullanarak birim test kodu olsa da, beraberinde bir dizi zorluk getirir. Daha ayrıntılı şekilde belirtmek gerekirse:

- Birim testlerinin yürütme süresini önemli ölçüde yavaşlatıyor. Testleri çalıştırmak ne kadar uzun sürerse, bunları sık sık yürütme olasılığınız da o kadar azalır. İdeal olarak, birim testlerinizin saniyeler içinde çalıştırılabilmesini ve projeyi derlemek kadar doğal bir şey olmasını istersiniz.
- Testler deki kurulum ve temizleme mantığını karmaşıklaştırır. Her birim testinin izole edilmiş ve diğerlerinden bağımsız olmasını istiyorsunuz (hiçbir yan etkisi veya bağımlılığı olmadan). Gerçek bir veritabanına karşı çalışırken duruma dikkat etmek ve testler arasında sıfırlamak zorunda.

Bu sorunları aşmamıza ve testlerimizle gerçek bir veritabanı kullanma gereksinimini önlememize yardımcı olabilecek "bağımlılık enjeksiyonu" adı verilen bir tasarım desenine bakalım.

### <a name="dependency-injection"></a>Bağımlılık Ekleme

Şu anda DinnersController sıkıca DinnerRepository sınıfa "birleştiğinde" olduğunu. "Bağlantı", bir sınıfın çalışmak için açıkça başka bir sınıfa dayandığı durumu ifade eder:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository sınıfı bir veritabanına erişim gerektirdiğinden, DinnersController sınıfının DinnerRepository'deki sıkı bir şekilde birleştirilmiş bağımlılığı, DinnersController eylem yöntemlerinin test edilebilmesi için bir veritabanına sahip olmamızı gerektirir.

Bunu, bağımlılıkların (veri erişimi sağlayan depo sınıfları gibi) artık bunları kullanan sınıflar içinde dolaylı olarak oluşturulmayan bir yaklaşım olan "bağımlılık enjeksiyonu" adı verilen bir tasarım deseni kullanarak atabiliriz. Bunun yerine, bağımlılıklar açıkça bunları kullanan sınıfa constructor bağımsız değişkenleri kullanılarak geçirilebilir. Bağımlılıklar arabirimler kullanılarak tanımlanırsa, birim test senaryoları için "sahte" bağımlılık uygulamalarında geçme esnekliğine sahibiz. Bu, veritabanına gerçekten erişim gerektirmeyen sınamaya özgü bağımlılık uygulamaları oluşturmamızı sağlar.

Bunu iş başında görmek için DinnersController ile bağımlılık enjeksiyonu uygulayalım.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository arabirimi ayıklama

İlk adımımız, denetleyicilerimizin Akşam Yemeklerini almak ve güncellemek için ihtiyaç duydukları depo sözleşmesini özetleyen yeni bir IDinnerRepository arabirimi oluşturmak olacaktır.

Bu arabirim sözleşmesini \Models klasörüne sağ tıklayarak ve sonra **Ekle-&gt;Yeni Öğe** menüsü komutunu seçerek ve IDinnerRepository.cs adlı yeni bir arabirim oluşturarak el ile tanımlayabiliriz.

Alternatif olarak, visual studio professional'da yerleşik refactoring araçlarını (ve daha yüksek sürümler) kullanarak mevcut DinnerRepository sınıfımızdan bizim için otomatik olarak bir arayüz oluşturabiliriz. VS kullanarak bu arabirimi ayıklamak için imleci DinnerRepository sınıfındaki metin düzenleyicisine konumlandırmanız ve ardından sağ tıklayıp **Refactor-Extract&gt;Interface** menü komutunu seçmemiz yeterlidir:

![](enable-automated-unit-testing/_static/image7.png)

Bu "Extract Interface" iletişim başlatacak ve oluşturmak için arabirimin adı için bize ister. IDinnerRepository varsayılan ve otomatik olarak arayüzeklemek için mevcut DinnerRepository sınıfında tüm ortak yöntemleri seçin:

![](enable-automated-unit-testing/_static/image8.png)

"Ok" düğmesini tıklattığımızda Visual Studio uygulamamıza yeni bir IDinnerRepository arabirimi ekleyecek:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

Ve mevcut DinnerRepository sınıf arayüzü uygular böylece güncellenecektir:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>Yapıcı enjeksiyonu desteklemek için DinnersController'ı güncelleme

Şimdi yeni arayüzü kullanmak için DinnersController sınıfını güncelleceğiz.

Şu anda DinnersController onun "dinnerRepository" alanı her zaman bir DinnerRepository sınıf olduğunu gibi sabit kodlu:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Biz böylece "dinnerRepository" alan tip IDinnerRepository yerine DinnerRepository olduğunu değiştireceğiz. Daha sonra iki public DinnersController yapıcısı ekleyeceğiz. Yapıcılardan biri bir IDinnerRepository bir argüman olarak geçirilmesini sağlar. Diğer bizim mevcut DinnerRepository uygulamasını kullanan varsayılan bir yapıcı:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

Varsayılan olarak ASP.NET MVC varsayılan oluşturucuları kullanarak denetleyici sınıfları oluşturduğundan, çalışma zamanındaki DinnersController'ımız veri erişimi gerçekleştirmek için DinnerRepository sınıfını kullanmaya devam edecektir.

Şimdi parametre oluşturucu kullanarak bir "sahte" akşam yemeği deposu uygulama geçmek için, ancak, bizim birim testleri güncelleyebilirsiniz. Bu "sahte" akşam yemeği deposu gerçek bir veritabanına erişim gerektirmez ve bunun yerine bellek içi örnek verileri kullanır.

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository sınıf oluşturma

FakeDinnerRepository sınıf oluşturalım.

NerdDinner.Tests projemizde bir "Fakes" dizini oluşturarak başlayacağız ve sonra yeni bir FakeDinnerRepository sınıfı ekleyeceğiz (klasöre sağ tıklayın ve **Ekle-&gt;Yeni Sınıf'ı**seçin):

![](enable-automated-unit-testing/_static/image9.png)

FakeDinnerRepository sınıfının IDinnerRepository arabirimini uygulayacak şekilde kodu güncelleştireceğiz. Daha sonra üzerine sağ tıklayıp "Arayüz IDinnerRepository Uygula" bağlam menüsü komutunu seçebiliriz:

![](enable-automated-unit-testing/_static/image10.png)

Bu, Visual Studio'nun varsayılan "saplama" uygulamalarıyla FakeDinnerRepository sınıfımıza tüm IDinnerRepository arayüz üyelerini otomatik olarak eklemesine neden olur:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Daha sonra bir in-memory List&lt;Dinner&gt; koleksiyonu kapalı çalışmak için FakeDinnerRepository uygulamasını güncelleyebilirsiniz bir yapıcı bağımsız değişken olarak geçti:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Şimdi bir veritabanı gerektirmeyen bir sahte IDinnerRepository uygulama var, ve bunun yerine Akşam yemeği nesnelerin bir in-bellek listesi kapalı çalışabilir.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Ünite Testleri ile FakeDinnerRepository kullanma

Veritabanı kullanılamadığı için daha önce başarısız olan DinnersController birim testlerine dönelim. Aşağıdaki kodu kullanarak DinnersController'a örnek bellek temalı Akşam Yemeği verileriyle doldurulan bir FakeDinnerRepository kullanmak için test yöntemlerini güncelleyebiliriz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

Ve şimdi bu testleri yaptığımızda ikisi de geçiyor:

![](enable-automated-unit-testing/_static/image11.png)

Hepsinden iyisi, onlar çalıştırmak için saniyenin sadece bir kısmını almak ve herhangi bir karmaşık kurulum / temizleme mantığı gerekmez. Artık gerçek bir veritabanına bağlanmaya gerek kalmadan tüm DinnersController eylem yöntemi kodumuzu (listeleme, sayfalama, ayrıntılar, oluşturma, güncelleme ve silme dahil) birim olarak test edebiliriz.

| **Yan Konu: Bağımlılık Enjeksiyon Çerçeveleri** |
| --- |
| Manuel bağımlılık enjeksiyonu gerçekleştirmek (yukarıda gibi) iyi çalışır, ancak bir uygulamadaki bağımlılık ların ve bileşenlerin sayısı arttıkça bakımı zorlaşır. .NET için daha fazla bağımlılık yönetimi esnekliği sağlamaya yardımcı olabilecek çeşitli bağımlılık enjeksiyon çerçeveleri vardır. Bazen "Denetimin Ters Çevrilmesi" (IoC) kapsayıcıları olarak da adlandırılan bu çerçeveler, çalışma zamanında (çoğunlukla yapıcı enjeksiyon kullanarak) nesnelere bağımlılıkları belirtmek ve aktarmak için ek bir yapılandırma desteği düzeyi sağlayan mekanizmalar sağlar. .NET'teki daha popüler OSS Bağımlılık Enjeksiyonu / IOC çerçevelerinden bazıları şunlardır: AutoFac, Ninject, Spring.NET, StructureMap ve Windsor. ASP.NET MVC, geliştiricilerin denetleyicilerin çözümüne ve anında alınmasına katılmalarını sağlayan ve Bağımlılık Enjeksiyonu / IoC çerçevelerinin bu süreç içinde temiz bir şekilde entegre edilmesini sağlayan genişletilebilirlik API'lerini ortaya çıkarır. DI/IOC çerçevesi kullanmak aynı zamanda varsayılan oluşturucuyu DinnersController'ımızdan çıkarmamıza olanak sağlayacaktır – bu da dinnerrepository ile arasındaki bağlantıyı tamamen ortadan kaldırır. NerdDinner uygulamamızla bağımlılık enjeksiyonu / IOC çerçevesi kullanmayacağız. Ama NerdDinner kod tabanı ve yetenekleri büyüdü eğer biz gelecek için düşünebilirsiniz bir şeydir. |

### <a name="creating-edit-action-unit-tests"></a>Eylem Birimi Testleri Yap Oluşturma

Şimdi DinnersController'ın Edit işlevini doğrulayan bazı birim testleri oluşturalım. Düzenleme eylemimizin HTTP-GET sürümünü test ederek başlayacağız:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Geçerli bir akşam yemeği istendiğinde DinnerFormViewModel nesnesi tarafından desteklenen bir Görünümün geri görüntülendiğini doğrulayan bir test oluşturacağız:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Ancak testi çalıştırdığımızda, Düzenleme yöntemi Dinner.IsHostedBy() denetimini gerçekleştirmek için User.Identity.Name özelliğine eriştiğinde geçersiz bir başvuru özel durumu atıldığı için başarısız olduğunu göreceğiz.

Denetleyici taban sınıfındaki Kullanıcı nesnesi, oturum açmış kullanıcı yla ilgili ayrıntıları kapsüller ve çalışma zamanında denetleyiciyi oluşturduğunda ASP.NET MVC tarafından doldurulur. DinnersController'ı bir web sunucusu ortamı dışında test ettiğimizden, Kullanıcı nesnesi ayarlı değildir (dolayısıyla null reference exception).

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Name mülküyle alay etmek

Alaycı çerçeveler, testlerimizi destekleyen bağımlı nesnelerin sahte sürümlerini dinamik olarak oluşturmamızı sağlayarak testi kolaylaştırır. Örneğin, Edit eylem testimizde, DinnersController'ımızın simüle edilmiş bir kullanıcı adını aramak için kullanabileceği bir Kullanıcı nesnesi oluşturmak için alaycı bir çerçeve kullanabiliriz. Bu, testimizi çalıştırdığımızda boş bir başvurunun atılmasını önleyecektir.

mvc ASP.NET ile kullanılabilecek birçok .NET alay çerçeveleri vardır (burada bunların bir [http://www.mockframeworks.com/](http://www.mockframeworks.com/)listesini görebilirsiniz: ). NerdDinner uygulamamızı test etmek için "Moq" adı verilen ve ücretsiz olarak indirilebilen [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)açık kaynak alaycı bir çerçeve kullanacağız.

İndirdikten sonra, Moq.dll derlemesine NerdDinner.Tests projemize bir referans ekleyeceğiz:

![](enable-automated-unit-testing/_static/image12.png)

Daha sonra bir kullanıcı adını parametre olarak alan ve daha sonra DinnersController örneğinde User.Identity.Name özelliğini "alay eden" test sınıfımıza bir "CreateDinnersControllerAs(username)" yardımcı yöntemi ekleriz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Yukarıda, Bir ControllerContext nesnesini taklit eden bir Mock nesnesi oluşturmak için Moq kullanıyoruz (ASP.NET MVC'nin Kullanıcı, İstek, Yanıt ve Oturum gibi çalışma zamanı nesnelerini ortaya çıkarmak için Controller sınıflarına geçirdiği şeydir). DenetleyiciBağlam'daki HttpContext.User.Identity.Name özelliğinin yardımcı yönteme aktardığımız kullanıcı adı dizesini döndürmesi gerektiğini belirtmek için Mock'da "SetupGet" yöntemini çağırıyoruz.

Herhangi bir sayıda ControllerContext özelliği ve yöntemiyle alay edebiliriz. Bunu göstermek için request.IsAuthenticated özelliği için bir SetupGet() çağrısı ekledim (aşağıdaki testler için aslında gerekli değildir – ancak İstek özellikleriyle nasıl alay edebileceğinizi göstermeye yardımcı olur). Bittiğinde, DinnersController'a ControllerContext ile ilgili bir örneğini yardımcı yöntemimiz döndürür.

Artık farklı kullanıcıları içeren senaryoları yeniden delemek için bu yardımcı yöntemini kullanan birim testleri yazabiliriz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

Ve şimdi testleri yaptığımızda geçiyorlar:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>UpdateModel() senaryolarını test etme

Edit eyleminin HTTP-GET sürümünü kapsayan testler oluşturduk. Şimdi Edit eyleminin HTTP-POST sürümünü doğrulayan bazı testler oluşturalım:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

Bu eylem yöntemiyle desteklememiz gereken ilginç yeni test senaryosu, Denetleyici taban sınıfındaki UpdateModel() yardımcı yönteminin kullanımıdır. Form sonrası değerlerini Akşam Yemeği nesnesi örneğimize bağlamak için bu yardımcı yöntemi kullanıyoruz.

Aşağıda, UpdateModel() yardımcı yöntemi için form deftere nakledilen değerleri nasıl sağlayabileceğimizi gösteren iki test verilmiştir. Bunu bir FormCollection nesnesi oluşturup doldurarak yapacağız ve ardından Denetleyici'deki "ValueProvider" özelliğine atayacağız.

İlk test, başarılı bir kaydede tarayıcının ayrıntılar eylemine yönlendirilmiş olduğunu doğrular. İkinci sınama, geçersiz giriş deftere nakledildiğinde eylemin bir hata iletisiyle yeniden edit görünümünü yeniden görüntülediğini doğrular.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Test Tamamlama

Ünite test kontrolör sınıflarında yer alan temel kavramları ele aldık. Uygulamamızın davranışını doğrulayan yüzlerce basit test oluşturmak için bu teknikleri kullanabiliriz.

Denetleyici ve model testlerimiz gerçek bir veritabanı gerektirmediği için, son derece hızlı ve çalıştırılabildiği kolaydır. Yüzlerce otomatik testi saniyeler içinde gerçekleştirebileceğiz ve yaptığımız bir değişikliğin bir şeyi bozup kırmadığı konusunda hemen geri bildirim alabiliriz. Bu, uygulamamızı sürekli olarak geliştirmemiz, yeniden düzenlememiz ve iyileştirmemiz için bize güven sağlayacaktır.

Biz bu bölümde son konu olarak test kaplı - ama test bir geliştirme sürecinin sonunda yapmanız gereken bir şey olduğu için değil! Tam tersine, geliştirme sürecinizde mümkün olduğunca erken otomatik testler yazmalısınız. Bunu yapmak, geliştikçe anında geri bildirim almanızı sağlar, uygulamanızın kullanım durumu senaryoları hakkında düşünceli düşünmenize yardımcı olur ve uygulamanızı temiz katmanlama ve bağlantı göz önünde bulundurarak tasarlamanız için size yol verir.

Kitabın daha sonraki bir bölümünde Test Odaklı Geliştirme (TDD) ve nasıl ASP.NET MVC ile kullanmak tartışılacaktır. TDD, ortaya çıkan kodun tatmin edeceği testleri ilk olarak yazdığınız yinelemeli bir kodlama uygulamasıdır. TDD ile uygulamak üzere olduğunuz işlevselliği doğrulayan bir test oluşturarak her özelliğe başlarsınız. Birim testini ilk olarak yazmak, özelliği ve nasıl çalışması gerektiğini net bir şekilde anlamanıza yardımcı olur. Yalnızca test yazıldıktan sonra (ve başarısız olduğunu doğruladınız) daha sonra testin doğruladığının gerçek işlevselliğini uygularsınız. Özelliğin nasıl çalışması gerektiğine dair kullanım durumunu düşünmek için zaman harcadığınız için, gereksinimleri ve bunları en iyi nasıl uygulayacağınızı daha iyi anlayabilirsiniz. Uygulama ile yaptığınızda testi yeniden çalıştırabilir ve özelliğin doğru çalışıp çalışmadığına ilişkin anında geri bildirim alabilirsiniz. Bölüm 10'da TDD'yi daha çok ele alacağız.

### <a name="next-step"></a>Sonraki Adım

Bazı son yorum sarın.

> [!div class="step-by-step"]
> [Önceki](use-ajax-to-implement-mapping-scenarios.md)
> [Sonraki](nerddinner-wrap-up.md)
