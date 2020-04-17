---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Kimlik Doğrulama ve Yetkilendirme Kullanarak Güvenli Uygulamalar | Microsoft Dokümanlar
author: rick-anderson
description: Adım 9, NerdDinner uygulamamızı güvenli hale getirmek için kimlik doğrulama ve yetkilendirmenin nasıl ekleyeceğinigösterir, böylece kullanıcıların siteye kaydolması ve siteye giriş yapabilmesi gerekir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542579"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Kimlik Doğrulama ve Yetkilendirme Kullanarak Uygulamaların Güvenliğini Sağlama

[Microsoft](https://github.com/microsoft) tarafından

[PDF’yi İndir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu adım 9 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.
> 
> Adım 9, kullanıcıların yeni akşam yemekleri oluşturmak için siteye kaydolması ve siteye giriş yapması gerektiği ve yalnızca akşam yemeği ne zaman ev sahipliği yapan kullanıcının daha sonra düzenleyebileceği için, NerdDinner uygulamamızın güvenliğini sağlamak için kimlik doğrulama ve yetkilendirmenin nasıl ekleyeceğini gösterir.
> 
> MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner Adım 9: Kimlik doğrulama ve yetkilendirme

Şu anda NerdDinner uygulamamız siteyi ziyaret eden herkese herhangi bir akşam yemeğinin ayrıntılarını oluşturma ve düzeltme olanağı veriyor. Bunu, kullanıcıların yeni akşam yemekleri oluşturmak için siteye kaydolması ve siteye giriş yapması gerekeceği şekilde değiştirelim ve yalnızca akşam yemeğine ev sahipliği yapan kullanıcının daha sonra düzenleyebileceği bir kısıtlama ekleyelim.

Bunu etkinleştirmek için uygulamamızı güvence altına almak için kimlik doğrulama ve yetkilendirme kullanırız.

### <a name="understanding-authentication-and-authorization"></a>Kimlik Doğrulama ve Yetkilendirmeyi Anlama

*Kimlik doğrulaması,* bir uygulamaya erişen istemcinin kimliğini tanımlama ve doğrulama işlemidir. Daha basit bir ifadeyle, bir web sitesini ziyaret ettiklerinde son kullanıcının "kim" olduğunu belirlemekle ilgilidir. ASP.NET tarayıcı kullanıcılarının kimliğini doğrulamak için birden çok yolu destekler. Internet web uygulamaları için kullanılan en yaygın kimlik doğrulama yaklaşımı "Form kimlik doğrulaması" olarak adlandırılır. Form kimlik doğrulama, bir geliştiricinin uygulamaları içinde bir HTML giriş formu yazmasını ve ardından bir son kullanıcının veritabanıveya başka bir parola kimlik bilgisi deposuna karşı gönderdiği kullanıcı adını/parolasını doğrulamasını sağlar. Kullanıcı adı/parola birleşimi doğruysa, geliştirici ASP.NET gelecekteki istekler arasında kullanıcıyı tanımlamak için şifreli bir HTTP çerezi vermelerini isteyebilir. NerdDinner uygulamamızla form doğrulamasını kullanarak form doğrulamasını kullanacağız.

*Yetkilendirme,* kimlik doğrulaması yapılan bir kullanıcının belirli bir URL'ye/kaynağa erişme veya bazı eylemler gerçekleştirme iznine sahip olup olmadığını belirleme işlemidir. Örneğin, NerdDinner uygulamamızda yalnızca oturum açan kullanıcıların */Dinners/Create* URL'sine erişebileceğine ve yeni Akşam Yemekleri oluşturabilmesini yetkilendirmek isteriz. Ayrıca, yalnızca akşam yemeğine ev sahipliği yapan kullanıcının bunu düzenleyebilmeleri ve diğer tüm kullanıcılara erişimi reddedebilmeleri için yetkilendirme mantığı eklemek isteriz.

### <a name="forms-authentication-and-the-accountcontroller"></a>Formlar Kimlik Doğrulaması ve Hesap Kontrolörü

ASP.NET MVC için varsayılan Visual Studio proje şablonu, yeni ASP.NET MVC uygulamaları oluşturulduğunda formların otomatik olarak kimlik doğrulamasını sağlar. Ayrıca projeye önceden oluşturulmuş bir hesap giriş sayfası uygulaması da ekler ve bu da bir site içinde güvenliği entegre etmeyi gerçekten kolaylaştırır.

Varsayılan Site.master ana sayfası, siteye erişen kullanıcı kimlik doğrulaması olmadığında sitenin sağ üst kısmında bir "Oturum Aç" bağlantısı görüntüler:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

"Oturum Aç" bağlantısını tıklattığınızda bir kullanıcı */Account/LogOn* URL'sine geçer:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Kayıt yaptırmayan ziyaretçiler bunu */Account/Register* URL'sine götürecek ve hesap bilgilerini girmelerine olanak tanıyan "Kaydol" bağlantısını tıklayarak yapabilir:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"Kaydol" düğmesini tıklattığınızda, ASP.NET Üyelik sistemi içinde yeni bir kullanıcı oluşturulur ve form kimlik doğrulamasını kullanarak kullanıcının siteye doğruluğunu doğrular.

Bir kullanıcı oturum açıldığında, Site.master sayfanın sağ üst hakkını değiştirarak "Hoş geldiniz [kullanıcı adı]" çıktısı elde eder. iletir ve "Oturum Açma" bağlantısı yerine "Oturum Kapat" bağlantısı açar. "Oturumu Kapat" bağlantısını tıklattığınızda kullanıcı çıkış larını kaydeder:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

Yukarıdaki giriş, oturum açma ve kayıt işlevselliği, projeyi oluşturduğunda Visual Studio tarafından projemize eklenen AccountController sınıfı içinde uygulanmaktadır. Hesap Kontrolörü'nün Kullanıcı Arabirimi\Görünümler\Hesap dizini içindeki görünüm şablonları kullanılarak uygulanır:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController sınıfı, şifreli kimlik doğrulama tanımlama bilgilerini vermek için ASP.NET Forms Kimlik Doğrulama sistemini ve kullanıcı adlarını/parolaları depolamak ve doğrulamak için üyelik API'ASP.NET kullanır. üyelik API'ASP.NET genişletilebilir ve herhangi bir parola kimlik bilgisi deposunun kullanılmasını sağlar. kullanıcı adını/parolaları bir SQL veritabanında veya Active Directory içinde depolayan yerleşik üyelik sağlayıcısı uygulamalarına sahip ASP.NET.

NerdDinner uygulamamızın hangi üyelik sağlayıcısını kullanması gerektiğini projenin kökündeki "web.config" dosyasını açarak ve içinde &lt;üyelik&gt; bölümünü arayarak yapılandırabiliriz. Varsayılan web.config, proje oluşturulduğunda SQL üyelik sağlayıcısını kaydeder ve veritabanı konumunu belirtmek için "ApplicationServices" adlı bir bağlantı dizesi kullanacak şekilde yapılandırır.

Varsayılan "ApplicationServices" bağlantı dizesi (web.config dosyasının &lt;bağlantıStrings&gt; bölümünde belirtilir) SQL Express kullanmak üzere yapılandırılmıştır. "ASPNETDB" adlı bir SQL Express veritabanına işaret ediyor. MDF" uygulamasının "Uygulama\_Verileri" dizini altında. Bu veritabanı uygulama içinde üyelik API'si ilk kez kullanıldığında yoksa, ASP.NET otomatik olarak veritabanını oluşturacak ve içindeki uygun üyelik veritabanı şemasını sağlayacaktır:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express kullanmak yerine tam bir SQL Server örneğini (veya uzak bir veritabanına bağlanmak) kullanmak istiyorsak, tek yapmamız gereken web.config dosyasındaki "ApplicationServices" bağlantı dizesini güncelleştirmek ve işaret ettiği veritabanına uygun üyelik şemasının eklenmiş olduğundan emin olmaktır. \Windows\Microsoft.NET\Framework\v2.0.50727\ dizinindeki "aspnet\_regsql.exe" yardımcı programını çalıştırıp üyelik için uygun şemayı ve diğer ASP.NET uygulama hizmetlerini veritabanına ekleyebilirsiniz.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[Authorize] filtresini kullanarak /Dinners/Create URL'sini yetkilendirme

NerdDinner uygulaması için güvenli bir kimlik doğrulaması ve hesap yönetimi uygulaması sağlamak için herhangi bir kod yazmamız gerekmedi. Kullanıcılar uygulamamıza yeni hesaplar kaydedebilir ve siteye giriş/çıkış yapabilir.

Artık uygulamaya yetkilendirme mantığı ekleyebilir ve site içinde yapabileceklerini ve yapamayacaklarını kontrol etmek için ziyaretçilerin kimlik doğrulama durumunu ve kullanıcı adını kullanabiliriz. DinnersController sınıfımızın "Oluştur" eylem yöntemlerine yetkilendirme mantığı ekleyerek başlayalım. Özellikle, */Dinners/Create* URL'ye erişen kullanıcıların oturum açmalarını şart sayılacağız. Oturum açmazlarsa, oturum açabilmeleri için onları giriş sayfasına yönlendiririz.

Bu mantığı uygulamak oldukça kolaydır. Yapmamız gereken tek şey, gibi eylem oluştur yöntemlerimize bir [Authorize] filtresi özniteliği eklemektir:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC, eylem yöntemlerine bildirimsel olarak uygulanabilen yeniden kullanılabilir mantığı uygulamak için kullanılabilecek "eylem filtreleri" oluşturma yeteneğini destekler. [Authorize] filtresi, ASP.NET MVC tarafından sağlanan yerleşik eylem filtrelerinden biridir ve bir geliştiricinin eylem yöntemleri ve denetleyici sınıflarına yetkilendirme kurallarını bildirimsel olarak uygulamasına olanak tanır.

Herhangi bir parametre olmadan (yukarıdaki gibi) uygulandığında [Authorize] filtresi, eylem yöntemi isteğinde bulunan kullanıcının oturum açması gerektiğini ve yoksa tarayıcıyı otomatik olarak giriş URL'sine yönlendirir. Bunu yaparken ilk istenen URL sorgubağımsız değişkeni olarak geçirilir (örneğin: /Account/LogOn? ReturnUrl=%2fDinners%2fCreate). AccountController daha sonra kullanıcıyı giriş yaptıktan sonra ilk istenen URL'ye yönlendirir.

[Yetkilendirme] filtresi isteğe bağlı olarak, kullanıcının hem oturum açmış olmasını gerektirecek bir "Kullanıcılar" veya "Roller" özelliğini belirtebilme yeteneğini destekler, hem izin verilen kullanıcılar listesinde hem de izin verilen bir güvenlik rolünün üyesi. Örneğin, aşağıdaki kod yalnızca iki belirli kullanıcıya , "scottgu" ve "billg", /Dinners/Create URL'sine erişmesine izin verir:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Kod içinde belirli kullanıcı adlarını gömme oldukça un-maintainable olsa olma eğilimindedir. Daha iyi bir yaklaşım, kodun denetlenen üst düzey "rolleri" tanımlamak ve ardından kullanıcıları bir veritabanı veya etkin dizin sistemi kullanarak role eşlemektir (gerçek kullanıcı eşleme listesinin koddan harici olarak depolanmasına olanak sağlamak). ASP.NET, bu kullanıcı/rol eşleciliğini gerçekleştirmeye yardımcı olabilecek yerleşik bir rol yönetimi API'sının yanı sıra yerleşik bir rol sağlayıcıları (SQL ve Active Directory dahil) içerir. Daha sonra kodu yalnızca belirli bir "yönetici" rolündeki kullanıcıların /Dinners/Create URL'sine erişmesine izin verecek şekilde güncelleyebiliriz:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Akşam Yemeği Oluştururken User.Identity.Name özelliğini kullanma

Denetleyici taban sınıfında açığa çıkan User.Identity.Name özelliğini kullanarak, şu anda oturum açmış olan bir isteğin kullanıcı adını alabiliriz.

Daha önce Create() eylem yöntemimizin HTTP-POST sürümünü uyguladığımızda Akşam Yemeği'nin "HostedBy" özelliğini statik bir dize yle kodlamıştık. Artık bu kodu, User.Identity.Name özelliğini kullanacak şekilde güncelleyebilir ve akşam yemeğini oluşturan ana bilgisayar için otomatik olarak bir RSVP ekleyebiliriz:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create(] yöntemine bir [Yetkilendirme] özniteliği eklediğimiz için, ASP.NET MVC, eylem yönteminin yalnızca /Dinners/Create URL'yi ziyaret eden kullanıcı sitede oturum açtırDığı zaman yürütülmesini sağlar. Bu nedenle, User.Identity.Name özellik değeri her zaman geçerli bir kullanıcı adı içerir.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Akşam Yemeklerini Düzenlerken User.Identity.Name özelliğini kullanma

Şimdi, yalnızca kendilerinin barındırdığı akşam yemeklerinin özelliklerini düzenleyebilmeleri için kullanıcıları kısıtlayan bazı yetkilendirme mantığı ekleyelim.

Bu şekilde yardımcı olmak için, ilk olarak Akşam Yemeği nesnemize (daha önce oluşturduğumuz Dinner.cs kısmi sınıf içinde) bir "IsHostedBy(kullanıcı adı)" yardımcı yöntemi ekleyeceğiz. Bu yardımcı yöntemi, sağlanan bir kullanıcı adının Barındırılan Akşam Yemeği özelliğiyle eşleşip eşleşmediğine bağlı olarak doğru veya yanlış döndürür ve bunların karşılanmasına karşı duyarsız bir dize karşılaştırması gerçekleştirmek için gereken mantığı kapsüller:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Daha sonra DinnersController sınıfımızdaki Edit() eylem yöntemlerine bir [Authorize] özniteliği ekleyeceğiz. Bu, kullanıcıların */Dinners/Edit/[id] URL'si* istemek için oturum açmalarını sağlar.

Daha sonra, oturum açan kullanıcının Akşam Yemeği ana bilgisayarla eşleştiğini doğrulamak için Dinner.IsHostedBy(kullanıcı adı) yardımcı yöntemini kullanan Düzenleme yöntemlerimize kod ekleyebiliriz. Kullanıcı ana bilgisayar değilse, bir "Geçersiz Sahibi" görünümünü görüntüler ve isteği sonlandırırız. Bunu yapmak için kod aşağıdaki gibi görünür:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Daha sonra \Views\Dinners dizinine sağ tıklayıp yeni&gt;bir "Geçersiz Sahip" görünümü oluşturmak için Ekle-Görüntüle menüsü komutunu seçebiliriz. Biz aşağıdaki hata mesajı ile doldurmak olacak:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

Ve şimdi bir kullanıcı sahip olmadığı bir akşam yemeğini yapmaya çalıştığında, bir hata iletisi alır:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Denetleyicimizdeki Delete() eylem yöntemleriiçin akşam yemeklerini silme iznini de kilitlemek ve yalnızca akşam yemeğinin ana bilgisayarının silebilmesini sağlamak için aynı adımları yineleyebiliriz.

### <a name="showinghiding-edit-and-delete-links"></a>Düzenle ve Sil Bağlantıları Gösterme/Gizleme

DinnersController sınıfımızın Düzenle ve Sil eylem yöntemine Ayrıntılar URL'mizden bağlanıyoruz:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

Şu anda, ayrıntılar URL'nin ziyaretçisinin akşam yemeğinin ev sahibi olup olmadığına bakılmaksızın Düzenle ve Sil eylem bağlantılarını gösteriyoruz. Bunu, bağlantıların yalnızca akşam yemeğinin sahibi ziyaretçi kullanıcıysa görüntülenecek şekilde değiştirelim.

DinnersController'ımızdaki Ayrıntılar() eylem yöntemi bir Akşam Yemeği nesnesini alır ve ardından görünüm şablonumuza model nesnesi olarak geçirir:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Aşağıdaki gibi Dinner.IsHostedBy() yardımcı yöntemini kullanarak düzenleme ve silme bağlantılarını koşullu olarak göstermek/gizlemek için görünüm şablonumuzu güncelleyebiliriz:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Sonraki Adımlar

Şimdi, ajax kullanarak akşam yemekleri için rsvp kimlik doğrulaması kullanıcıların etkinleştirebilirsiniz nasıl bakalım.

> [!div class="step-by-step"]
> [Önceki](implement-efficient-data-paging.md)
> [Sonraki](use-ajax-to-deliver-dynamic-updates.md)
