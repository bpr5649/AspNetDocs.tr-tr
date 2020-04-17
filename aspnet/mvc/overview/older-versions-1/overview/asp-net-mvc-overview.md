---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC Genel Bakış | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET MVC uygulaması ile ASP.NET Web Formları uygulamaları arasındaki farklar hakkında bilgi edinin. ASP.NET MVC uygulamasını ne zaman oluşturacağına nasıl karar verebilirsiniz öğrenin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541019"
---
# <a name="aspnet-mvc-overview"></a>ASP.NET MVC’ye Genel Bakış

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET MVC uygulaması ile ASP.NET Web Formları uygulamaları arasındaki farklar hakkında bilgi edinin. ASP.NET MVC uygulamasını ne zaman oluşturacağına nasıl karar verebilirsiniz öğrenin.

Model Görünümü Denetleyicisi (MVC) mimari deseni bir uygulamayı üç ana bileşene ayırır: model, görünüm ve denetleyici. ASP.NET MVC çerçevesi, MVC tabanlı Web uygulamaları oluşturmak için ASP.NET Web Forms desenine bir alternatif sağlar. ASP.NET MVC çerçevesi, (Web Formları tabanlı uygulamalarda olduğu gibi) ana sayfalar ve üyelik tabanlı kimlik doğrulama gibi mevcut ASP.NET özellikleriyle entegre edilmiş hafif ve son derece test edilebilir bir sunu çerçevesidir. MVC çerçevesi **System.Web.Mvc** ad alanında tanımlanır ve **System.Web** ad alanının temel, desteklenen bir parçasıdır.   
  
MVC, birçok geliştiricinin aşina olduğu standart bir tasarım desenidir. Bazı Web uygulamaları MVC çerçevesinden yararlanacaktır. Diğerleri Web Formları ve postbacks dayalı geleneksel ASP.NET uygulama deseni kullanmaya devam edecektir. Diğer Web uygulama türleri iki yaklaşımı birleştirir; ne yaklaşım diğer hariç.   
  
MVC çerçevesi aşağıdaki bileşenleri içerir:

[![Parametre değeri bekleyen bir denetleyici eylemi çağırmak](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Şekil 01**: Parametre değeri bekleyen bir denetleyici eylemi çağırmak ([Tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-overview/_static/image2.png))

- **Modeller**. Model nesneleri, uygulamanın veri etki alanı için mantığı uygulayan bölümleridir. Genellikle, model nesneleri bir veritabanında model durumunu alır ve depolar. Örneğin, bir Ürün nesnesi bir veritabanından bilgi alabilir, üzerinde çalışabilir ve güncelleştirilmiş bilgileri SQL Server'daki Ürünler tablosuna geri yazabilir.

Küçük uygulamalarda, model genellikle fiziksel bir yerine kavramsal bir ayrımdır. Örneğin, uygulama yalnızca bir veri kümesini okur ve görünüme gönderirse, uygulamanın fiziksel bir model katmanı ve ilişkili sınıfları yoktur. Bu durumda, veri kümesi bir model nesnesinin rolünü alır.

- **Görünümler**. Görünümler, uygulamanın kullanıcı arabirimini (UI) görüntüleyen bileşenlerdir. Genellikle, bu ui model verilerinden oluşturulur. Bir örnek, Ürünler nesnesinin geçerli durumuna göre metin kutularını, açılır listeleri ve onay kutularını görüntüleyen Ürünler tablosunun bir edit görünümü olacaktır.

- **Denetleyiciler**. Denetleyiciler, kullanıcı etkileşimini işleyen, modelle çalışan ve sonuçta Kullanıcı Aracı'nı görüntüleyen bir görünüm seçen bileşenlerdir. Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici, kullanıcı girişini ve etkileşimini işler ve yanıtlar. Örneğin, denetleyici sorgu dize değerlerini işler ve bu değerleri modele geçirir ve bu değerleri kullanarak veritabanını sorgular.

MVC deseni, bu öğeler arasında gevşek bir bağlantı sağlarken uygulamanın farklı yönlerini (giriş mantığı, iş mantığı ve Kullanıcı Arabirimi mantığı) ayıran uygulamalar oluşturmanıza yardımcı olur. Desen, uygulamada her tür mantığın nerede bulunması gerektiğini belirtir. UI mantığı görünüme aittir. Giriş mantığı denetleyiciye aittir. İş mantığı modele aittir. Bu ayrım, bir uygulama oluştururken karmaşıklığı yönetmenize yardımcı olur, çünkü aynı anda uygulamanın bir boyutuna odaklanmanızı sağlar. Örneğin, iş mantığına bağlı olmadan görünüme odaklanabilirsiniz.   
  
Karmaşıklığı yönetmeye ek olarak, MVC deseni uygulamaları test etmeyi Web Formları tabanlı bir Web uygulaması ASP.NET test etmekten daha kolaylaştırır. Örneğin, Web Formları tabanlı bir ASP.NET Web uygulamasında, hem çıktıgörüntülemek hem de kullanıcı girişine yanıt vermek için tek bir sınıf kullanılır. Web Formları tabanlı ASP.NET uygulamaları için otomatik testler yazmak karmaşık olabilir, çünkü tek bir sayfayı test etmek için sayfa sınıfını, tüm alt denetimlerini ve uygulamadaki ek bağımlı sınıfları anında anlamanız gerekir. Sayfayı çalıştırmak için çok fazla sınıf anında olduğundan, yalnızca uygulamanın tek tek bölümlerine odaklanan testler yazmak zor olabilir. Bu nedenle, Web Formları tabanlı ASP.NET uygulamaları için testlerin uygulanması, Bir MVC uygulamasındaki testlerden daha zor olabilir. Ayrıca, Web Formları tabanlı bir ASP.NET uygulamasında yapılan testler bir Web sunucusu gerektirir. MVC çerçevesi bileşenleri ayırır ve arabirimleri yoğun olarak kullanır, bu da tek tek bileşenleri çerçevenin geri kalanından izole olarak test etmeyi mümkün kılar.   
  
Bir MVC uygulamasının üç ana bileşeni arasındaki gevşek bağlantı da paralel gelişimi teşvik eder. Örneğin, bir geliştirici görünüm üzerinde çalışabilir, ikinci bir geliştirici denetleyici mantığı üzerinde çalışabilir ve üçüncü bir geliştirici modeldeki iş mantığına odaklanabilir.

## <a name="deciding-when-to-create-an-mvc-application"></a>MVC UygulamasıNe Ne Zaman Oluşturulacağına Karar Verme

ASP.NET MVC çerçevesini veya ASP.NET Web Forms modelini kullanarak bir Web uygulamasını uygulayıp uygulamayacağınız konusunda dikkatlice düşünmelisiniz. MVC çerçevesi Web Formları modelinin yerini almaz; web uygulamaları için her iki çerçeveyi de kullanabilirsiniz. (Web Formları tabanlı varsa, bunlar her zaman olduğu gibi çalışmaya devam eder.)   
  
Belirli bir Web sitesi için MVC çerçevesini veya Web Formları modelini kullanmaya karar vermeden önce, her yaklaşımın avantajlarını tartın.

### <a name="advantages-of-an-mvc-based-web-application"></a>MVC Tabanlı Web Uygulamasının Avantajları

ASP.NET MVC çerçevesi aşağıdaki avantajları sunar:

- Bir uygulamayı modele, görünüme ve denetleyiciye bölerek karmaşıklığı yönetmeyi kolaylaştırır.
- Görünüm durumu veya sunucu tabanlı formlar kullanmaz. Bu, MVC çerçevesini bir uygulamanın davranışı üzerinde tam denetim isteyen geliştiriciler için ideal hale getirir.
- Web uygulama isteklerini tek bir denetleyici aracılığıyla işleyen bir Ön Denetleyici deseni kullanır. Bu, zengin bir yönlendirme altyapısını destekleyen bir uygulama tasarlamanızı sağlar. Daha fazla bilgi için MSDN Web sitesindeki [Ön Denetleyici'ye](https://go.microsoft.com/fwlink/?LinkId=106357 "Ön Kumanda") bakın.
- Test odaklı geliştirme (TDD) için daha iyi destek sağlar.
- Uygulama davranışı üzerinde yüksek derecede denetime ihtiyaç duyan büyük geliştirici ve Web tasarımcıları ekipleri tarafından desteklenen Web uygulamaları için iyi çalışır.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web Formları Tabanlı Web Uygulamasının Avantajları

Web Formları tabanlı çerçeve aşağıdaki avantajları sunar:

- Http üzerinden durumu koruyan ve iş hattı Web uygulaması geliştirmeden yararlanan bir olay modelini destekler. Web Formları tabanlı uygulama, yüzlerce sunucu denetiminde desteklenen düzinelerce olay sağlar.
- Tek tek sayfalara işlevsellik katan bir Sayfa Denetleyicisi deseni kullanır. Daha fazla bilgi için MSDN Web sitesindeki [Sayfa Denetleyicisi](https://go.microsoft.com/fwlink/?LinkId=106359 "Sayfa Denetleyici") sayfasına bakın.
- Durum bilgilerini yönetmeyi kolaylaştıran görünüm durumu veya sunucu tabanlı formlar kullanır.
- Hızlı uygulama geliştirme için kullanılabilir bileşenlerin çok sayıda yararlanmak isteyen Web geliştiricileri ve tasarımcıları küçük ekipler için iyi çalışır.
- Bileşenler **(Sayfa** sınıfı, denetimler vb.) sıkıca tümleştirilmeden ve genellikle MVC modelinden daha az kod gerektirdiğinden, genel olarak uygulama geliştirme için daha az karmaşıktır.

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC Çerçevesinin Özellikleri

ASP.NET MVC çerçevesi aşağıdaki özellikleri sağlar:

- Uygulama görevlerinin (giriş mantığı, iş mantığı ve Kullanıcı Arası TümevarMantığı), sınanabilirlik ve test tabanlı geliştirme (TDD) varsayılan olarak ayrılması. MVC çerçevesindeki tüm temel sözleşmeler arayüz tabanlıdır ve uygulamadaki gerçek nesnelerin davranışını taklit eden simüle edilmiş nesneler olan sahte nesneler kullanılarak sınanabilir. Ünite testini hızlı ve esnek hale getiren ASP.NET bir işlemde denetleyicileri çalıştırmak zorunda kalmadan uygulamayı birim test edebilirsiniz. .NET Framework ile uyumlu herhangi bir birim test çerçevesi kullanabilirsiniz.
- Genişletilebilir ve takılabilir bir çerçeve. ASP.NET MVC çerçevesinin bileşenleri kolayca değiştirilebilmeleri veya özelleştirilebilmeleri için tasarlanmıştır. Kendi görünüm altyapınızı, URL yönlendirme ilkenizi, eylem yöntemi parametre serileştirmenizi ve diğer bileşenleri takabilirsiniz. ASP.NET MVC çerçevesi bağımlılık enjeksiyonu (DI) ve Inversion of Control (IOC) konteyner modellerinin kullanımını da destekler. DI, nesnenin kendisini oluşturmak için sınıfa güvenmek yerine nesneleri bir sınıfa enjekte etmenizi sağlar. IOC, bir nesne başka bir nesne gerektiriyorsa, ilk nesnelerin ikinci nesneyi yapılandırma dosyası gibi bir dış kaynaktan alması gerektiğini belirtir. Bu, testi kolaylaştırır.
- Anlaşılır ve aranabilir URL'lere sahip uygulamalar oluşturmanıza olanak tanıyan güçlü bir URL eşleme bileşeni. URL'ler dosya adı uzantıları içermemelidir ve arama motoru optimizasyonu (SEO) ve temsili durum aktarımı (REST) adresleme için iyi çalışan URL adlandırma desenleri desteklemek üzere tasarlanmıştır.
- Varolan ASP.NET sayfasında (.aspx dosyaları), kullanıcı denetiminde (.ascx dosyaları) ve ana sayfa (.asıl dosyalar) biçimlendirme dosyalarında görünüm şablonları olarak biçimlendirme desteği. İç içe geçmiş ana sayfalar, satır içi ifadeler (&lt;%= %&gt;), bildirimsel sunucu denetimleri, şablonlar, veri bağlama, yerelleştirme vb. gibi ASP.NET MVC çerçevesi ile varolan ASP.NET özelliklerini kullanabilirsiniz.
- Varolan ASP.NET özellikleri için destek. ASP.NET MVC form kimlik doğrulama ve Windows kimlik doğrulama, URL yetkilendirme, üyelik ve roller, çıktı ve veri önbelleğe alma, oturum ve profil durumu yönetimi, sistem durumu izleme, yapılandırma sistemi ve sağlayıcı mimarisi gibi özellikleri kullanmanıza olanak sağlar.
