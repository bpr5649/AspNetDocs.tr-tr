---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 'Yineleme #4 – Uygulamayı gevşek bir şekilde birleştiğinde yapın (C#) | Microsoft Dokümanlar'
author: rick-anderson
description: Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Için...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542371"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>4. Yineleme – Uygulamanın gevşek bir şekilde bağlanmasını sağlama (C#)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

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

İletişim Yöneticisi uygulamasının bu dördüncü yinelemesinde, uygulamayı daha gevşek bir şekilde biraraya getirmek için uygulamayı yeniden bir araya getirebiliyoruz. Bir uygulama gevşek bir şekilde birleştiğinde, kodu uygulamanın diğer bölümlerinde değiştirmenize gerek kalmadan uygulamanın bir bölümünde değiştirebilirsiniz. Gevşek birleştirilmiş uygulamalar değiştirmek için daha esnektir.

Şu anda, Contact Manager uygulaması tarafından kullanılan tüm veri erişim ve doğrulama mantığı denetleyici sınıflarında bulunur. Bu kötü bir fikir. Uygulamanızın bir bölümünü değiştirmeniz gerektiğinde, uygulamanızın başka bir bölümüne hata girme riskine girersiniz. Örneğin, doğrulama mantığınızı değiştirirseniz, veri erişiminize veya denetleyici mantığınıza yeni hatalar girme riskine girersiniz.

> [!NOTE] 
> 
> (SRP), bir sınıfın değişmesi için hiçbir zaman birden fazla nedeni olmamalıdır. Karıştırma denetleyicisi, doğrulama ve veritabanı mantığı Tek Sorumluluk İlkesi büyük bir ihlalidir.

Uygulamanızı değiştirmeniz gerekebilecek çeşitli nedenler vardır. Uygulamanıza yeni bir özellik eklemeniz gerekebilir, uygulamanızdaki bir hatayı düzeltmeniz gerekebilir veya uygulamanızın bir özelliğinin nasıl uygulandığını değiştirmeniz gerekebilir. Uygulamalar nadiren statiktir. Zamanla büyüyüp mutasyona uğrarlar.

Örneğin, veri erişim katmanınızı uygulama şeklinizi değiştirmeye karar verdiğinizi düşünün. Şu anda, İletişim Yöneticisi uygulaması veritabanına erişmek için Microsoft Entity Framework'u kullanır. Ancak, ADO.NET veri hizmetleri veya NHibernate gibi yeni veya alternatif bir veri erişim teknolojisine geçiş yapmaya karar verebilirsiniz. Ancak, veri erişim kodu doğrulama ve denetleyici kodundan yalıtılmış olmadığından, doğrudan veri erişimiyle ilgili olmayan diğer kodu değiştirmeden uygulamanızdaki veri erişim kodunu değiştirmenin bir yolu yoktur.

Bir uygulama gevşek bir şekilde birleştiğinde, diğer taraftan, uygulamanın diğer bölümlerine dokunmadan uygulamanın bir bölümünde değişiklik yapabilirsiniz. Örneğin, doğrulama veya denetleyici mantığınızı değiştirmeden veri erişim teknolojilerinde geçiş yapabilirsiniz.

Bu yinelemede, İletişim Yöneticisi uygulamamızı daha gevşek bir şekilde birleştirilmiş bir uygulamaya dönüştürmemizi sağlayan çeşitli yazılım tasarım modellerinden yararlanıyoruz. Biz işimiz bittiğinde, İletişim Yöneticisi daha önce yapmadığı hiçbir şeyi yapmaz. Ancak, gelecekte uygulamayı daha kolay değiştirebileceğiz.

> [!NOTE] 
> 
> Yeniden düzenleme, bir uygulamayı varolan işlevselliği kaybetmeyecek şekilde yeniden yazma işlemidir.

## <a name="using-the-repository-software-design-pattern"></a>Depo Yazılımı Tasarım Deseni Kullanma

İlk değişikliğimiz, Depo deseni adı verilen bir yazılım tasarım deseninden yararlanmaktır. Veri erişim kodumuzu uygulamamızın geri kalanından izole etmek için Depo modelini kullanacağız.

Depo deseni uygulamak için aşağıdaki iki adımı tamamlamamız gerekmektedir:

1. Arayüz oluşturma
2. Arabirimi uygulayan somut bir sınıf oluşturma

İlk olarak, gerçekleştirmemiz gereken tüm veri erişim yöntemlerini açıklayan bir arabirim oluşturmamız gerekir. IContactManagerRepository arabirimi Listeleme 1'de bulunur. Bu arabirim beş yöntem açıklar: CreateContact(), DeleteContact(), EditContact(), GetContact ve ListContacts().

**Listeleme 1 - Modeller\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

Ardından, IContactManagerRepository arabirimini uygulayan somut bir sınıf oluşturmamız gerekir. Veritabanına erişmek için Microsoft Entity Framework'u kullandığımıziçin EntityContactManagerRepository adında yeni bir sınıf oluştururuz. Bu sınıf Listeleme 2'de yer almaktadır.

**Listeleme 2 - Modeller\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

EntityContactManagerRepository sınıfının IContactManagerRepository arabirimini uyguladığına dikkat edin. Sınıf, bu arabirim tarafından açıklanan yöntemlerin beşini de uygular.

Neden bir arayüzle uğraşmamız gerektiğini merak edebilirsiniz. Neden hem bir arabirim hem de onu uygulayan bir sınıf oluşturmamız gerekiyor?

Bir istisna dışında, uygulamamızın geri kalanı beton sınıf ile değil, arabirim ile etkileşime girecektir. EntityContactManagerRepository sınıfının maruz kaçtığı yöntemleri çağırmak yerine, IContactManagerRepository arabiriminin maruz kaçtığı yöntemleri çağıracağız.

Bu şekilde, uygulamamızın geri kalanını değiştirmenize gerek kalmadan arabirimi yeni bir sınıfla uygulayabiliriz. Örneğin, ileriki bir tarihte, IContactManagerRepository arabirimini uygulayan bir DataServicesContactManagerRepository sınıfını uygulamak isteyebiliriz. DataServicesContactManagerRepository sınıfı, Microsoft Entity Framework yerine bir veritabanına erişmek için ADO.NET Veri Hizmetleri'ni kullanabilir.

Uygulama kodumuz somut EntityContactManagerRepository sınıfı yerine IContactManagerRepository arabirimine karşı programlanmışsa, kodumuzun geri kalanından herhangi birini değiştirmeden beton sınıfları arasında geçiş yapabiliriz. Örneğin, veri erişim veya doğrulama mantığımızı değiştirmeden EntityContactManagerRepository sınıfından DataServicesContactManagerRepository sınıfına geçiş yapabiliriz.

Somut sınıflar yerine arayüzlere (soyutlamalara) karşı programlama uygulamamızı değiştirmek için daha esnek hale getirir.

> [!NOTE] 
> 
> Menü seçeneği Refactor, Extract Interface seçerek Visual Studio içinde bir beton sınıfından hızlı bir arayüz oluşturabilirsiniz. Örneğin, önce EntityContactManagerRepository sınıfını oluşturabilir ve ardından IContactManagerRepository arabirimini otomatik olarak oluşturmak için Extract Arabirimi'ni kullanabilirsiniz.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Bağımlılık Enjeksiyon Yazılımı Tasarım Deseni Kullanma

Veri erişim kodumuzu ayrı bir Depo sınıfına aktardığımıza göre, bu sınıfı kullanmak için İletişim denetleyicimizi değiştirmemiz gerekir. Denetleyicimizde Depo sınıfını kullanmak için Bağımlılık Enjeksiyonu adı verilen bir yazılım tasarım deseninden yararlanacağız.

Değiştirilmiş Kişi denetleyicisi Listeleme 3'te bulunur.

**Listeleme 3 - Denetleyiciler\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

Listeleme 3'teki Kişi denetleyicisinin iki oluşturucusu olduğuna dikkat edin. İlk oluşturucu, iContactManagerRepository arabiriminin somut bir örneğini ikinci oluşturucuya geçirir. Kontak denetleyici sınıfı *Yapıcı Bağımlılık Enjeksiyonu*kullanır.

EntityContactManagerRepository sınıfının kullanıldığı tek yer ilk oluşturucudur. Sınıfın geri kalanı, somut EntityContactManagerRepository sınıfı yerine IContactManagerRepository arabirimini kullanır.

Bu, gelecekte IContactManagerRepository sınıfının uygulamalarını değiştirmeyi kolaylaştırır. EntityContactManagerRepository sınıfı yerine DataServicesContactRepository sınıfını kullanmak istiyorsanız, ilk oluşturucuyu değiştirmeniz.

Constructor Bağımlılık enjeksiyonu da Contact denetleyici sınıf Çok test edilebilir hale getirir. Birim testlerinizde, IContactManagerRepozitory sınıfının sahte bir uygulamasını geçerek Contact denetleyicisini anında atabilirsiniz. Bağımlılık Enjeksiyonunun bu özelliği, Contact Manager uygulaması için birim testleri oluşturduğumuz da bir sonraki yinelemede bizim için çok önemli olacaktır.

> [!NOTE] 
> 
> İletişim denetleyicisi sınıfını IContactManagerRepository arabiriminin belirli bir uygulamasından tamamen ayırmak istiyorsanız, StructureMap veya Microsoft Entity Framework (MEF) gibi Bağımlılık Enjeksiyonu'nu destekleyen bir çerçeveden yararlanabilirsiniz. Bağımlılık Enjeksiyonu çerçevesinden yararlanarak, kodunuzda somut bir sınıfa başvurmanız gerekmez.

## <a name="creating-a-service-layer"></a>Hizmet Katmanı Oluşturma

Doğrulama mantığımızın, Listeleme 3'teki değiştirilmiş denetleyici sınıfındadenetleyici mantığımızla hala karışık olduğunu fark etmişsinizdir. Veri erişim mantığımızı yalıtmanın iyi bir fikir olmasıyla aynı nedenle, doğrulama mantığımızı yalıtmak iyi bir fikirdir.

Bu sorunu gidermek için ayrı bir [*hizmet katmanı*](http://martinfowler.com/eaaCatalog/serviceLayer.html)oluşturabiliriz. Hizmet katmanı, denetleyicimiz ve depo sınıflarımız arasına ekleyebileceğimiz ayrı bir katmandır. Hizmet katmanı, tüm doğrulama mantığımızı da içeren iş mantığımızı içerir.

ContactManagerService Listeleme 4'te yer almaktadır. İletişim denetleyicisi sınıfından doğrulama mantığını içerir.

**Listeleme 4 - Modeller\ContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

ContactManagerService'in oluşturucusu için doğrulama sözlüğü gerektirdiğine dikkat edin. Hizmet katmanı, bu Doğrulama Sözlüğü aracılığıyla denetleyici katmanı ile iletişim kurar. Dekoratör deseni tartışırken Doğrulama Sözlüğü'nu aşağıdaki bölümde ayrıntılı olarak tartışıyoruz.

Ayrıca, ContactManagerService'in IContactManagerService arabirimini uyguladığına dikkat edin. Her zaman somut sınıflar yerine arayüzlere karşı programlamak için çaba göstermelisiniz. İletişim Yöneticisi uygulamasındaki diğer sınıflar ContactManagerService sınıfıyla doğrudan etkileşime geçmez. Bunun yerine, bir istisna dışında, Contact Manager uygulamasının geri kalanı IContactManagerService arabirimine göre programlanır.

IContactManagerService arabirimi Listeleme 5'te bulunur.

**Listeleme 5 - Modeller\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

Değiştirilmiş Kişi Denetleyicisi sınıfı Listeleme 6'da bulunur. İletişim denetleyicisinin Artık ContactManager deposuyla etkileşimde bulunmadığına dikkat edin. Bunun yerine, İletişim denetleyicisi ContactManager hizmeti ile etkileşime geçer. Her katman mümkün olduğunca diğer katmanlardan izole edilmiştir.

**Listeleme 6 - Denetleyiciler\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

Uygulamamız artık Tek Sorumluluk İlkesi (SRP) afoul çalışır. Listeleme 6'daki İletişim denetleyicisi, uygulama yürütme akışını denetlemek dışında her türlü sorumluluktan mahrum bırakılmıştı. Tüm doğrulama mantığı Contact denetleyicisinden kaldırıldı ve hizmet katmanına itildi. Tüm veritabanı mantığı depo katmanına itildi.

## <a name="using-the-decorator-pattern"></a>Dekoratör Deseni Kullanma

Hizmet katmanımızı kontrol örneğımızdan tamamen ayırmak istiyoruz. Prensip olarak, Hizmet katmanımızı, MVC uygulamamıza bir referans eklemeye gerek kalmadan, denetleyici katmanımızdan ayrı bir derleme yapabilmemiz gerekir.

Ancak, hizmet katmanımızın doğrulama hatası iletilerini denetleyici katmanına geri geçirebilmesi gerekir. Denetleyici ve hizmet katmanını bağlamadan hizmet katmanının doğrulama hatası iletilerini iletmesini nasıl sağlayabiliriz? Dekoratör deseni adında bir yazılım tasarım [deseni](http://en.wikipedia.org/wiki/Decorator_pattern)yararlanabilir.

Denetleyici, doğrulama hatalarını temsil etmek için ModelState Dictionary adlı bir ModelStateDictionary kullanır. Bu nedenle, Denetleyici katmanından hizmet katmanına ModelState geçmek için cazip olabilir. Ancak, hizmet katmanında ModelState'i kullanmak, hizmet katmanınızı ASP.NET MVC çerçevesinin bir özelliğine bağımlı hale getirecek. Bu kötü olabilir, çünkü bir gün, ASP.NET bir MVC uygulaması yerine WPF uygulaması ile hizmet katmanı nı kullanmak isteyebilirsiniz. Bu durumda, ModelStateDictionary sınıfını kullanmak için ASP.NET MVC çerçevesine başvurmak istemezsinüz.

Dekoratör deseni, arabirimi uygulamak için varolan bir sınıfı yeni bir sınıfta kaydırmanızı sağlar. İletişim Yöneticisi projemiz, Listeleme 7'de yer alan ModelStateWrapper sınıfını içerir. ModelStateWrapper sınıfı Listeleme 8'deki arabirimi uygular.

**Listeleme 7 - Modeller\Doğrulama\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Listeleme 8 - Modeller\Doğrulama\IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

Listeleme 5'e yakından bakarsanız, ContactManager hizmet katmanının yalnızca IValidationDictionary arabirimini kullandığını görürsünüz. ContactManager hizmeti ModelStateDictionary sınıfına bağlı değildir. Contact controller ContactManager hizmetini oluşturduğunda, denetleyici ModelDurumunu şu şekilde sarar:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>Özet

Bu yinelemede, İletişim Yöneticisi uygulamasına yeni bir işlev eklemedik. Bu yinelemenin amacı, kişi yöneticisi uygulamasını yeniden düzenlemekti, böylece bakımı ve değiştirilmesi daha kolay.

İlk olarak, Depo yazılım tasarım modelini uyguladık. Tüm veri erişim kodunu ayrı bir ContactManager deposu sınıfına geçtik.

Doğrulama mantığımızı denetleyici mantığımızdan da izole ettik. Tüm doğrulama kodumuzu içeren ayrı bir hizmet katmanı oluşturduk. Denetleyici katmanı hizmet katmanıyla etkileşime giriyor ve servis katmanı depo katmanıyla etkileşime giriyor.

Hizmet katmanını oluşturduğumuzda, ModelState'i hizmet katmanımızdan ayırmak için Dekoratör deseninden yararlandık. Hizmet katmanımızda ModelState yerine IValidationDictionary arabirimine göre programlandık.

Son olarak, Bağımlılık Enjeksiyon deseni adlı bir yazılım tasarım deseni yararlandı. Bu desen, somut sınıflar yerine arabirimlere (soyutlamalar) karşı programlamamızı sağlar. Bağımlılık Enjeksiyonu tasarım deseni uygulamak da kodumuzu daha test edilebilir hale getirir. Bir sonraki yinelemede, projemize birim testleri ekliyoruz.

> [!div class="step-by-step"]
> [Önceki](iteration-3-add-form-validation-cs.md)
> [Sonraki](iteration-5-create-unit-tests-cs.md)
