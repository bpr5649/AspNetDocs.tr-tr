---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Profiller, Temalar ve Web Bölümleri | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET 2.0'da yapılandırma ve enstrümantasyonda büyük değişiklikler vardır. Yeni ASP.NET yapılandırma API yapılandırma değişiklikleri pr yapılmasını sağlar ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: 4bc98cca226a0bd9bd766a21e88b0facf2a4b610
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543645"
---
# <a name="profiles-themes-and-web-parts"></a>Profiller, Temalar ve Web Bölümleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2.0'da yapılandırma ve enstrümantasyonda büyük değişiklikler vardır. Yeni ASP.NET yapılandırma API'si, yapılandırma değişikliklerinin programlı olarak yapılmasına olanak tanır. Buna ek olarak, birçok yeni yapılandırma ayarları yeni yapılandırmalar ve enstrümantasyon için izin var.

ASP.NET 2.0 kişiselleştirilmiş Web siteleri alanında önemli bir gelişme temsil eder. Daha önce ele aldığımız üyelik özelliklerine ek olarak, profiller, temalar ve Web bölümleri ASP.NET Web sitelerinde kişiselleştirilmişliği önemli ölçüde artırır.

## <a name="aspnet-profiles"></a>ASP.NET Profilleri

ASP.NET profilleri oturumlara benzer. Fark, bir profilin kalıcı olması, tarayıcı kapatıldığında ise oturumun kaybolmasıdır. Oturumlar ve profiller arasındaki bir diğer büyük fark, profillerin güçlü bir şekilde yazılmış olmasıdır, bu nedenle geliştirme sürecinde Size IntelliSense sağlar.

Bir profil, uygulama için makineler yapılandırma dosyasında veya web.config dosyasında tanımlanır. (Web.config dosyasının alt klasörlerinde profil tanımlayamazsınız.) Aşağıdaki kod, Web sitesi ziyaretçilerinin adını ve adını depolamak için bir profil tanımlar.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

Bir profil özelliği için varsayılan veri türü System.String'tir. Yukarıdaki örnekte, hiçbir veri türü belirtilmedi. Bu nedenle, Ad Ve Soyadı özellikleri string türündedir. Daha önce de belirtildiği gibi, profil özellikleri güçlü bir şekilde yazılır. Aşağıdaki kod, Int32 türünde yaş için yeni bir özellik ekler.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Profiller genellikle formlar kimlik doğrulaması ASP.NET kullanılır. Formkimlik doğrulaması ile birlikte kullanıldığında, her kullanıcının kullanıcı kimliğiyle ilişkili ayrı bir profili vardır. Ancak, aşağıda gösterildiği gibi **allowAnonymous** özniteliği ile birlikte &lt;yapılandırma&gt; dosyasındaki anonim Tanımlama öğesini kullanarak anonim bir uygulamada profillerin kullanımına izin vermek de mümkündür:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Anonim bir kullanıcı siteye göz attığında, ASP.NET kullanıcı için **ProfileCommon'ın** bir örneğini oluşturur. Bu profil, kullanıcıyı benzersiz bir ziyaretçi olarak tanımlamak için tarayıcıdaki çerezde depolanan benzersiz bir kimlik kullanır. Bu şekilde, anonim olarak göz atan kullanıcıların profil bilgilerini depolayabilirsiniz.

## <a name="profile-groups"></a>Profil Grupları

Profillerin özelliklerini gruplandırmak mümkündür. Özellikleri gruplandırma kılarak, belirli bir uygulama için birden çok profili simüle etmek mümkündür.

Aşağıdaki yapılandırma, iki grup için bir FirstName ve Soyadı özelliğini yapılandırır; Alıcılar ve Beklentiler.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Daha sonra özellikleri belirli bir grup üzerinde aşağıdaki gibi ayarlamak mümkündür:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Karmaşık Nesneleri Depolama

Şimdiye kadar, ele aldığımız örnekler bir profilde basit veri türlerini depoladı. **SeriizeAs** özniteliğini kullanarak serileştirme yöntemini belirterek karmaşık veri türlerini profilde depolamak da mümkündür:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

Bu durumda, türü PurchaseInvoice'dır. PurchaseInvoice sınıfının serileştirilebilir olarak işaretlemesi gerekir ve herhangi bir sayıda özellik içerebilir. Örneğin, **PurchaseInvoice'Da NumItemsPurchased**adında bir özellik varsa, bu özelliğe kod olarak aşağıdaki gibi başvurabilirsiniz:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Profil Devralma

Birden çok uygulamada kullanılmak üzere bir profil oluşturmak mümkündür. ProfileBase'den türetilen bir profil sınıfı oluşturarak, aşağıda gösterildiği gibi **devralan** özniteliğini kullanarak birkaç uygulamada bir profili yeniden kullanabilirsiniz:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

Bu durumda, sınıf **Satın AlmaProfili** de aşağıdaki gibi görünür:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Profil Sağlayıcıları

ASP.NET profilleri sağlayıcı modelini kullanır. Varsayılan sağlayıcı, bilgileri SqlProfileProvider sağlayıcısını kullanarak\_Web uygulamasının Uygulama Veri klasöründe bir SQL Server Express veritabanında depolar. Veritabanı yoksa, profil bilgi depolamaya çalıştığında ASP.NET otomatik olarak oluşturur.

Ancak, bazı durumlarda kendi profil sağlayıcınızı geliştirmek isteyebilirsiniz. ASP.NET profili özelliği, farklı sağlayıcıları kolayca kullanmanıza olanak tanır.

Şunları zaman özel bir profil sağlayıcısı oluşturursunuz:

- Profil bilgilerini FoxPro veritabanında veya Oracle veritabanında olduğu gibi .NET Framework'e dahil olan profil sağlayıcıları tarafından desteklenmeyen bir veri kaynağında depolamanız gerekir.
- .NET Framework'e dahil olan sağlayıcılar tarafından kullanılan veritabanı şemasından farklı bir veritabanı şeması kullanarak profil bilgilerini yönetmeniz gerekir. Yaygın bir örnek, profil bilgilerini varolan bir SQL Server veritabanında kullanıcı verileriyle tümleştirmek istediğinizdir.

### <a name="required-classes"></a>Gerekli Sınıflar

Bir profil sağlayıcısı uygulamak için System.Web.Profile.ProfileProvider özet sınıfını devralan bir sınıf oluşturursunuz. **ProfileProvider** özet sınıfı sırayla System.Configuration.SettingsProvider abstract class'ı devralır ve System.Configuration.Provider.ProviderBase özet sınıfını devralır. Bu devralma zinciri nedeniyle, **ProfileProvider** sınıfının gerekli üyelerine ek olarak, **Ayarlar Sağlayıcısı** ve **SağlayıcıBase** sınıflarının gerekli üyelerini uygulamanız gerekir.

Aşağıdaki **tablolar, SağlayıcıTabanı,** Ayarlar Sağlayıcısı ve **ProfileProvider**özet sınıflarından uygulamanız gereken özellikleri ve yöntemleri açıklar. **ProfileProvider**

### <a name="providerbase-members"></a>SağlayıcıBase Üyeleri

| **Üye** | **Açıklama** |
| --- | --- |
| Initialize yöntemi | Sağlayıcı örneğinin adını ve yapılandırma ayarlarının NameValueCollection'ını girer. Makine yapılandırmasında veya Web.config dosyasında belirtilen uygulamaya özgü değerler ve seçenekler de dahil olmak üzere sağlayıcı örneği için seçenekleri ve özellik değerlerini ayarlamak için kullanılır. |

### <a name="settingsprovider-members"></a>SettingsSağlayıcı Üyeler

| **Üye** | **Açıklama** |
| --- | --- |
| ApplicationName özelliği | Her profilde depolanan uygulama adı. Profil sağlayıcısı, her uygulama için profil bilgilerini ayrı ayrı depolamak için uygulama adını kullanır. Bu, birden çok ASP.NET uygulamanın, farklı uygulamalarda aynı kullanıcı adı oluşturulduğunda, çakışma olmadan aynı veri kaynağını kullanmasını sağlar. Alternatif olarak, birden çok ASP.NET uygulama aynı uygulama adını belirterek bir profil veri kaynağını paylaşabilir. |
| GetPropertyValues yöntemi | Bir SettingsContext ve SettingsPropertyCollection nesnesi olarak girer. **SettingsContext** kullanıcı hakkında bilgi sağlar. Bu bilgileri, kullanıcıiçin profil özelliği bilgilerini almak için birincil anahtar olarak kullanabilirsiniz. Kullanıcı adını ve kullanıcının kimlik doğrulaması veya anonim olup olmadığını almak için **SettingsContext** nesnesini kullanın. **SettingsPropertyCollection,** SettingsProperty nesnelerinin bir koleksiyonunu içerir. Her **SettingsProperty** nesnesi, özelliğin adını ve türünü ve özelliğin varsayılan değeri ve özelliğin salt okunup okunmadığı gibi ek bilgileri sağlar. GetPropertyValues yöntemi, giriş olarak sağlanan **SettingsProperty** nesnelerini temel alan SettingsPropertyValue nesneleri ile bir **SettingsPropertyValue** Collection'ı oluşturur. Belirtilen kullanıcının veri kaynağından gelen değerler her **SettingsPropertyValue** nesnesi için PropertyValue özelliklerine atanır ve tüm koleksiyon döndürülür. Çağrı yöntemi, belirtilen kullanıcı profili için LastActivityDate değerini geçerli tarih ve saate güncelleştirir. |
| SetPropertyValues yöntemi | Bir **SettingsContext** ve **SettingsPropertyValueCollection** nesnesi olarak girer. **SettingsContext** kullanıcı hakkında bilgi sağlar. Bu bilgileri, kullanıcıiçin profil özelliği bilgilerini almak için birincil anahtar olarak kullanabilirsiniz. Kullanıcı adını ve kullanıcının kimlik doğrulaması veya anonim olup olmadığını almak için **SettingsContext** nesnesini kullanın. **SettingsPropertyValueCollection,** **SettingsPropertyValue** nesnelerinin bir koleksiyonunu içerir. Her **SettingsPropertyValue** nesnesi, özelliğin adını, türünü ve değerinin yanı sıra özelliğin varsayılan değeri ve özelliğin salt okunup okunmadığı gibi ek bilgiler sağlar. **SetPropertyValues** yöntemi, belirtilen kullanıcının veri kaynağındaki profil özellik değerlerini güncelleştirir. Arama yöntemi, belirtilen kullanıcı profili için **LastActivityDate** ve LastUpdatedDate değerlerini geçerli tarih ve saate güncelleştirir. |

### <a name="profileprovider-members"></a>ProfileSağlayıcı Üyeleri

| **Üye** | **Açıklama** |
| --- | --- |
| Profilleri Silme yöntemi | Kullanıcı adlarından oluşan bir dizi girin ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği belirtilen adlar için tüm profil bilgilerini ve özellik değerlerini veri kaynağından siler. Veri kaynağınız hareketleri destekliyorsa, bir hareketteki tüm silme işlemlerini eklemeniz ve herhangi bir silme işlemi başarısız olursa hareketi geri alıp özel bir durum atmanız önerilir. |
| Profilleri Silme yöntemi | ProfilInfo nesnelerinin bir koleksiyonunu girer ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği her profil için tüm profil bilgilerini ve özellik değerlerini veri kaynağından siler. Veri kaynağınız hareketleri destekliyorsa, bir hareketteki tüm silme işlemlerini eklemeniz ve herhangi bir silme işlemi başarısız olursa hareketi geri almanız ve bir özel durum atmanız önerilir. |
| DeleteInactiveProfiles yöntemi | Bir ProfileAuthenticationOption değerini ve DateTime nesnesini girdi olarak alır ve son etkinlik tarihinin belirtilen tarih ve saatten daha az olduğu veya bu tarihe eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği tüm profil bilgilerini ve özellik değerlerini veri kaynağından siler. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin silinip silinmeyeceğini belirtir. Veri kaynağınız hareketleri destekliyorsa, bir hareketteki tüm silme işlemlerini eklemeniz ve herhangi bir silme işlemi başarısız olursa hareketi geri almanız ve bir özel durum atmanız önerilir. |
| GetAllProfiles yöntemi | **Bir ProfilAuthenticationOption** değeri, sayfa dizini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve profillerin toplam sayısına ayarlanacak bir tamsayı için bir başvuru olarak alır. Uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller için **ProfileInfo** nesneleri içeren bir ProfileInfoCollection döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin mi döndürüleceğini belirtir. **GetAllProfiles** yöntemi yle döndürülen sonuçlar, sayfa dizini ve sayfa boyutu değerleri yle sınırlandırılmıştır. Sayfa boyutu **değeri, ProfileInfoCollection'da**döndürülecek maksimum **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri, 1'in ilk sayfayı tanımladığı sonuç sayfasının hangi sayfayı döndüreceklerini belirtir. Toplam kayıtlar için parametre, toplam profil sayısına ayarlanmış bir çıkış parametresi (Visual Basic'te **ByRef'i** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizin değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** onuncu profiller aracılığıyla altıncı profili içerir. Yöntem döndüğünde toplam kayıt değeri 13 olarak ayarlanır. |
| GetAllInactiveProfiles yöntemi | Bir **ProfilAuthenticationOption** değeri, **DateTime** nesnesi, sayfa dizinini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve toplam profil sayısına ayarlanacak bir tamsayıya başvuru olarak alır. Son etkinlik tarihinin belirtilen **DateTime'dan** daha az veya eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller için **ProfileInfo** nesneleri içeren bir **ProfileInfoKoleksiyonu** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin mi döndürüleceğini belirtir. **GetAllInactiveProfiles** yöntemi yle döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri ile sınırlandırılmıştır. Sayfa boyutu **değeri, ProfileInfoCollection'da**döndürülecek maksimum **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri, 1'in ilk sayfayı tanımladığı sonuç sayfasının hangi sayfayı döndüreceklerini belirtir. Toplam kayıtlar için parametre, toplam profil sayısına ayarlanmış bir çıkış parametresi (Visual Basic'te **ByRef'i** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizin değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** onuncu profiller aracılığıyla altıncı profili içerir. Yöntem döndüğünde toplam kayıt değeri 13 olarak ayarlanır. |
| FindProfilesByUserName yöntemi | **Bir ProfilAuthenticationOption** değeri, bir kullanıcı adı içeren bir dize, sayfa dizini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve profillerin toplam sayısına ayarlanacak bir tamsayı için bir başvuru olarak alır. Kullanıcı adının belirtilen kullanıcı adıyla eşleştiği ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller için **ProfileInfo** nesneleri içeren bir **ProfileInfoCollection** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin mi döndürüleceğini belirtir. Veri kaynağınız joker karakter gibi ek arama özelliklerini destekliyorsa, kullanıcı adları için daha kapsamlı arama özellikleri sağlayabilirsiniz. **FindProfilesByUserName** yöntemi yle döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri ile sınırlandırılmıştır. Sayfa boyutu **değeri, ProfileInfoCollection'da**döndürülecek maksimum **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri, 1'in ilk sayfayı tanımladığı sonuç sayfasının hangi sayfayı döndüreceklerini belirtir. Toplam kayıtlar için parametre, toplam profil sayısına ayarlanmış bir çıkış parametresi (Visual Basic'te **ByRef'i** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizin değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** onuncu profiller aracılığıyla altıncı profili içerir. Yöntem döndüğünde toplam kayıt değeri 13 olarak ayarlanır. |
| FindInactiveProfilesByUserName yöntemi | **Bir ProfilAuthenticationOption** değeri, bir kullanıcı adı, **datetime** nesnesi, sayfa dizini belirten bir tamsayı içeren bir dize, sayfa boyutunu belirten bir tamsayı ve profillerin toplam sayısına ayarlanacak bir tamsayı için bir başvuru olarak alır. Kullanıcı adının belirtilen kullanıcı adıyla eşleştiği, son etkinlik tarihinin belirtilen **DateTime'dan**daha az veya eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller için **ProfileInfo** nesneleri içeren bir **ProfileInfoCollection** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin mi döndürüleceğini belirtir. Veri kaynağınız joker karakter gibi ek arama özelliklerini destekliyorsa, kullanıcı adları için daha kapsamlı arama özellikleri sağlayabilirsiniz. **FindInactiveProfilesByUserName** yöntemi yle döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri ile sınırlandırılmıştır. Sayfa boyutu **değeri, ProfileInfoCollection'da**döndürülecek maksimum **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri, 1'in ilk sayfayı tanımladığı sonuç sayfasının hangi sayfayı döndüreceklerini belirtir. Toplam kayıtlar için parametre, toplam profil sayısına ayarlanmış bir çıkış parametresi (Visual Basic'te **ByRef'i** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizin değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** onuncu profiller aracılığıyla altıncı profili içerir. Yöntem döndüğünde toplam kayıt değeri 13 olarak ayarlanır. |
| GetNumberOfInActiveProfiles yöntemi | **Bir ProfileAuthenticationOption** değerini ve **DateTime** nesnesini girer ve son etkinlik tarihinin belirtilen **DateTime'dan** daha az veya eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profillerin sayısını döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimlik doğrulaması yapılan profillerin mi yoksa tüm profillerin mi sayılamayacağını belirtir. |

### <a name="applicationname"></a>ApplicationName

Profil sağlayıcıları her uygulama için profil bilgilerini ayrı ayrı depoladığından, veri şemanızın uygulama adını içerdiğinden ve sorguların ve güncelleştirmelerin de uygulama adını içerdiğinden emin olmalısınız. Örneğin, aşağıdaki komut, kullanıcı adına ve profilin anonim olup olmadığını temel alan bir veritabanından özellik değeri almak için kullanılır ve **ApplicationName** değerinin sorguya dahil edilmesini sağlar.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET Temalar

## <a name="what-are-aspnet-20-themes"></a>2.0 ASP.NET Temalar nelerdir?

Bir Web uygulamasının en önemli yönlerinden biri tutarlı bir görünüm ve site genelinde hissediyorum. ASP.NET 1.x geliştiricilergenellikle tutarlı bir görünüm ve his uygulamak için Basamaklı Stil Sayfaları (CSS) kullanın. ASP.NET 2.0 temaları, ASP.NET geliştiriciye ASP.NET sunucu denetimlerinin yanı sıra HTML öğelerinin görünümünü tanımlama olanağı verdiği için CSS'de önemli ölçüde gelişir. ASP.NET temalar tek tek denetimlere, belirli bir Web sayfasına veya tüm Web uygulamasına uygulanabilir. Temalar, css dosyalarının bir birleşimini, isteğe bağlı bir cilt dosyanı ve görüntüler gerektiğinde isteğe bağlı Görüntüler dizinini kullanır. Cilt dosyası, ASP.NET sunucu denetimlerinin görsel görünümünü denetler.

## <a name="where-are-themes-stored"></a>Temalar Nerede Saklanır?

Temaların depolandığı konum, kapsamına göre farklılık gösterir. Herhangi bir uygulamaya uygulanabilecek temalar aşağıdaki klasörde depolanır:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Belirli bir uygulamaya özgü bir tema, Web `App\_Themes\<Theme\_Name>` sitesinin kökündeki bir dizinde depolanır.

> [!NOTE]
> Cilt dosyası yalnızca görünümü etkileyen sunucu denetim özelliklerini değiştirmelidir.

Genel tema, Web sunucusunda çalışan herhangi bir uygulamaya veya Web sitesine uygulanabilen bir temadır. Bu temalar, v2.x.xxxxx dizininin içindeki ASP.NETClientfiles\Themes dizininde varsayılan olarak depolanır. Alternatif olarak, tema dosyalarını Web sitenizin\_kökündeki\_aspnet istemci/sistem web/[sürüm]/Temalar/[tema\_adı] klasörüne taşıyabilirsiniz.

Uygulamaya özgü temalar yalnızca dosyaların bulunduğu uygulamaya uygulanabilir. Bu dosyalar Web sitesinin `App\_Themes/<theme\_name>` kökündeki dizinde depolanır.

## <a name="the-components-of-a-theme"></a>Bir Temanın Bileşenleri

Tema, bir veya daha fazla CSS dosyasından, isteğe bağlı cilt dosyasından ve isteğe bağlı Görüntüler klasöründen oluşur. CSS dosyaları istediğiniz herhangi bir ad olabilir (yani default.css veya theme.css, vb) ve temalar klasörünün kökünde olmalıdır. CSS dosyaları, belirli seçiciler için sıradan CSS sınıfları ve öznitelikleritanımlamak için kullanılır. CSS sınıflarından birini bir sayfa öğesine uygulamak için **CSSClass** özelliği kullanılır.

Cilt dosyası, sunucu denetimleri ASP.NET için özellik tanımları içeren bir XML dosyasıdır. Aşağıda listelenen kod örnek bir cilt dosyasıdır.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**Aşağıdaki Şekil 1,** tema uygulanmadan gezinilen küçük bir ASP.NET sayfası gösterir. **Şekil 2,** uygulanan bir tema ile aynı dosyayı gösterir. Arka plan rengi ve metin rengi bir CSS dosyası aracılığıyla yapılandırılır. Düğmenin ve textbox'ın görünümü, yukarıda listelenen cilt dosyası kullanılarak yapılandırılır.

![Tema Yok](profiles-themes-and-web-parts/_static/image1.gif)

**Şekil 1**: Tema Yok

![Tema Uygulamalı](profiles-themes-and-web-parts/_static/image2.gif)

**Şekil 2**: Uygulanan Tema

Yukarıda listelenen cilt dosyası, tüm TextBox denetimleri ve Düğme denetimleri için varsayılan bir görünüm tanımlar. Bu, bir sayfaya eklenen her TextBox denetiminin ve Düğme denetiminin bu görünüme sahip olacağı anlamına gelir. Denetimin **SkinID** özelliğini kullanarak bu denetimlerin belirli örneklerine uygulanabilen bir cilt de tanımlayabilirsiniz.

Aşağıdaki kod, Düğme kontrolü için bir deriyi tanımlar. **GoButton'un** **SkinID** özelliğine sahip yalnızca Button kontrolleri cildin görünümünü alır.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Sunucu denetim türü başına yalnızca bir varsayılan görünüme sahip olabilirsiniz. Ek kaplamalara ihtiyacınız varsa, SkinID özelliğini kullanmalısınız.

## <a name="applying-themes-to-pages"></a>Sayfalara Tema Uygulama

Bir tema aşağıdaki yöntemlerden herhangi biri kullanılarak uygulanabilir:

- &lt;web.config dosyasının sayfa&gt; öğesi
- Bir @Page sayfanın yönergesinde
- Programlı olarak

## <a name="applying-a-theme-in-the-configuration-file"></a>Yapılandırma Dosyasına Tema Uygulama

Uygulamalar yapılandırma dosyasında bir tema uygulamak için aşağıdaki sözdizimini kullanın:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

Burada belirtilen tema adı temalar klasörünün adı ile eşleşmelidir. Bu klasör, bu kursta daha önce bahsedilen konumlardan herhangi birinde bulunabilir. Var olmayan bir tema uygulamaya çalışırsanız, bir yapılandırma hatası oluşur.

## <a name="applying-a-theme-in-the-page-directive"></a>Sayfa Yönergesinde Tema Uygulama

Ayrıca @ Page yönergesinde bir tema uygulayabilirsiniz. Bu yöntem, belirli bir sayfa için bir tema kullanmanıza olanak sağlar.

@Page Yönergede bir tema uygulamak için aşağıdaki sözdizimini kullanın:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Bir kez daha, burada belirtilen tema daha önce belirtildiği gibi tema klasörü eşleşmelidir. Var olmayan bir tema uygulamaya çalışırsanız, bir yapı hatası oluşur. Visual Studio da özniteliği vurgulamak ve böyle bir tema var olduğunu bildirir.

## <a name="applying-a-theme-programmatically"></a>Programlı Bir Tema Uygulama

Bir tema programlı olarak uygulamak için, **Sayfa\_PreInit** yönteminde sayfanın **Tema** özelliğini belirtmeniz gerekir.

Bir tema programlı uygulamak için aşağıdaki sözdizimini kullanın:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

Sayfa yaşam döngüsü nedeniyle preinit yönteminde temanın uygulanması gerekmektedir. Bu noktadan sonra uygularsanız, sayfa teması çalışma süresine göre zaten uygulanmış olur ve bu noktadaki bir değişiklik yaşam döngüsünde çok geç olur. Var olmayan bir tema uygularsanız, bir **HttpException** oluşur. Bir tema programlı olarak uygulandığında, herhangi bir sunucu denetimiskinID özelliği belirtilirse bir yapı uyarısı oluşur. Bu uyarı, hiçbir temanın bildirimsel olarak uygulanmadığını ve yoksayılabildiği konusunda sizi bilgilendirmek için tasarlanmıştır.

## <a name="exercise-1--applying-a-theme"></a>Egzersiz 1 : Tema Uygulama

Bu alıştırmada, bir Web sitesine ASP.NET teması uygularsınız.

> [!IMPORTANT]
> Bilgileri bir cilt dosyasına girmek için Microsoft Word kullanıyorsanız, normal tırnak bilgilerini akıllı tırnaklarla değiştirmediğinizden emin olun. Akıllı tırnak cilt dosyaları ile ilgili sorunlara neden olur.

1. Yeni bir ASP.NET Web sitesi oluşturun.
2. Solution Explorer'da projeye sağ tıklayın ve Yeni Öğe Ekle'yi seçin.
3. Dosyalar listesinden Web Yapılandırma Dosyası'nı seçin ve Ekle'yi tıklatın.
4. Solution Explorer'da projeye sağ tıklayın ve Yeni Öğe Ekle'yi seçin.
5. Cilt Dosyası'nı seçin ve Ekle'yi tıklatın.
6. Dosyayı Uygulama\_Temaları klasörünün içine yerleştirmek isteyip istindiğiniz sorulduğunda Evet'i tıklatın.
7. Solution Explorer'daki Uygulama\_Temaları klasörünün içindeki SkinFile klasörüne sağ tıklayın ve Yeni Öğe Ekle'yi seçin.
8. Dosyalar listesinden Stil Sayfası'nı seçin ve Ekle'yi tıklatın. Artık yeni temanızı uygulamak için gerekli tüm dosyalara sahipsiniz. Ancak Visual Studio, temalar klasörünüzü SkinFile olarak adlandırmıştır. Bu klasöre sağ tıklayın ve CoolTheme adını değiştirin.
9. SkinFile.skin dosyasını açın ve dosyanın sonuna aşağıdaki kodu ekleyin: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. SkinFile.skin dosyasını kaydedin.
11. StyleSheet.css'yi açın.
12. Metindeki tüm metni aşağıdakilerle değiştirin: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. StyleSheet.css dosyasını kaydedin.
14. Varsayılan.aspx sayfasını açın.
15. TextBox denetimi ve Düğme denetimi ekleyin.
16. Sayfayı kaydedin. Şimdi Varsayılan.aspx sayfasına göz atın. Normal bir Web formu olarak görüntülenmelidir.
17. web.config dosyasını açın.
18. Açılış `<system.web>` etiketinin altına aşağıdakileri ekleyin: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. web.config dosyasını kaydedin. Şimdi Varsayılan.aspx sayfasına göz atın. Uygulanan tema ile görüntülenmelidir.
20. Zaten açık değilse Visual Studio'da Default.aspx sayfasını açın.
21. Düğmeyi seçin.
22. **SkinID** özelliğini goButton olarak değiştirin. Visual Studio'nun Düğme kontrolü için geçerli SkinID değerleriyle açılır bir şekilde açılır bir şekilde izin verdiğine dikkat edin.
23. Sayfayı kaydedin. Şimdi tarayıcınızdaki sayfayı yeniden önizleyin. Düğme şimdi "git" demeli ve görünüm olarak daha geniş olmalıdır.

**SkinID** özelliğini kullanarak, belirli bir sunucu denetimitinin farklı örnekleri için farklı görünümleri kolayca yapılandırabilirsiniz.

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme Özellik

Şimdiye kadar, biz temalar temaları kullanarak uygulama hakkında konuştuk. Tema özelliğini kullanırken, cilt dosyası sunucu denetimleri için bildirimsel ayarları geçersiz kılar. Örneğin, alıştırma 1'de Düğme denetimi için "goButton" skinid'ini belirttiniz ve bu da Düğme'nin metnini "git" olarak değiştirdi. Tasarımcıdaki Düğme'nin Metin özelliğinin "Düğme" olarak ayarlandığını fark etmiş olabilirsiniz, ancak tema bunu geçersiz kılmıştır. Tema her zaman tasarımcıherhangi bir özellik ayarlarını geçersiz kılar.

Temanın cilt dosyasında tanımlanan özellikleri tasarımcıda belirtilen özelliklere sahip geçersiz kılmak istiyorsanız, Tema özelliği yerine **StyleSheetTheme** özelliğini kullanabilirsiniz. StyleSheetTheme özelliği, Tema özelliği gibi tüm açık özellik ayarlarını geçersiz kılmaması dışında Tema özelliğiyle aynıdır.

Bunu iş başında görmek için, 1 alıştırmasında projeden web.config dosyasını açın ve öğeyi aşağıdakiyle değiştirin: `<pages>`

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Şimdi Varsayılan.aspx sayfasına göz atın ve Düğme denetiminin yine "Düğme" metin özelliğine sahip olduğunu göreceksiniz. Bunun nedeni, tasarımcıdaki açık özellik ayarı goButton SkinID tarafından ayarlanan Metin özelliğini geçersiz kılmıştır.

## <a name="overriding-themes"></a>Geçersiz Kılma Temaları

Genel bir tema, uygulamanın Uygulama\_Temaları klasörüne aynı ada göre bir tema uygulanarak geçersiz kılınabilir. Ancak, tema gerçek bir geçersiz kılma senaryosunda uygulanmaz. Çalışma zamanı Uygulama\_Temaları klasöründe tema dosyalarıyla karşılaşırsa, bu dosyaları kullanarak teonu uygular ve genel teonu yok sayacaktır.

StyleSheetTheme özelliği geçersiz kılınabilir ve aşağıdaki gibi kod geçersiz kılınabilir:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Web Bölümleri

ASP.NET Web Parçaları, son kullanıcıların Web sayfalarının içeriğini, görünümünü ve davranışını doğrudan bir tarayıcıdan değiştirmesini sağlayan Web siteleri oluşturmak için tümleşik bir denetim kümesidir. Değişiklikler sitedeki tüm kullanıcılara veya tek tek kullanıcılara uygulanabilir. Kullanıcılar sayfaları ve denetimleri değiştirdiğinde, ayarlar kullanıcının kişisel tercihlerini gelecekteki tarayıcı oturumları boyunca korumak için kaydedilebilir, bu özellik kişiselleştirme olarak adlandırılır. Bu Web Parçaları özellikleri, geliştiricilerin son kullanıcıları geliştirici veya yönetici müdahalesi olmadan bir Web uygulamasını dinamik olarak kişiselleştirmeleri için güçlendirebileceği anlamına gelir.

Web Parçaları denetim kümesini kullanarak, geliştirici olarak son kullanıcıların aşağıdakileri yapmalarını sağlayabilirsiniz:

- Sayfa içeriğini kişiselleştirin. Kullanıcılar bir sayfaya yeni Web Parçaları denetimleri ekleyebilir, bunları kaldırabilir, gizleyebilir veya sıradan pencereler gibi en aza indirebilir.
- Sayfa düzenini kişiselleştirin. Kullanıcılar Web Parçaları denetimini sayfadaki farklı bir bölgeye sürükleyebilir veya görünümünü, özelliklerini ve davranışını değiştirebilir.
- Dışa aktarma ve alma denetimleri. Kullanıcılar, diğer sayfalarda veya sitelerde kullanılmak üzere Web Parçaları denetim ayarlarını içe aktarabilir veya dışa aktarabilir, özellikleri, görünümü ve hatta denetimdeki verileri koruyabilir. Bu, son kullanıcılardaki veri girişini ve yapılandırma taleplerini azaltır.
- Bağlantılar oluşturun. Kullanıcılar denetimler arasında bağlantılar kurabilir, böylece, örneğin, bir grafik denetimi stok işaretçisi denetimindeki veriler için bir grafik görüntüleyebilir. Kullanıcılar yalnızca bağlantının kendisini değil, grafik denetiminin verileri nasıl görüntülediğinin görünümünü ve ayrıntılarını da kişiselleştirebilir.
- Site düzeyindeki ayarları yönetin ve kişiselleştirin. Yetkili kullanıcılar site düzeyindeki ayarları yapılandırabilir, bir siteye veya sayfaya kimlerin erişebileceğini belirleyebilir, denetimlere rol tabanlı erişim ayarlayabilir ve benzeri. Örneğin, yönetimrolündeki bir kullanıcı, bir Web Parçaları denetimini tüm kullanıcılar tarafından paylaşılacak şekilde ayarlayabilir ve yönetici olmayan kullanıcıların paylaşılan denetimi kişiselleştirmesini engelleyebilir.

Web Bölümleri ile genellikle üç şekilde çalışırsınız: Web Parçaları denetimlerini kullanan sayfalar oluşturmak, tek tek Web Parçaları denetimleri oluşturmak veya portal gibi tam, kişiselleştirilebilir Web uygulamaları oluşturmak.

## <a name="page-development"></a>Sayfa Geliştirme

Sayfa geliştiricileri, Web Parçaları kullanan sayfalar oluşturmak için Microsoft Visual Studio 2005 gibi görsel tasarım araçlarını kullanabilir. Visual Studio gibi bir aracı kullanmanın bir avantajı, Web Parçaları denetim kümesinin görsel bir tasarımcıda Sürükle ve bırak denetimi ve Web Parçaları denetimlerinin yapılandırması için özellikler sağlamasıdır. Örneğin, tasarımcıyı bir Web Parts bölgesini veya Web Parçaları düzenleyicidenetimini tasarım yüzeyine sürüklemek için kullanabilir ve ardından Web Parçaları denetim kümesi tarafından sağlanan Web Parçaları denetim kümesi tarafından sağlanan Web Parçaları denetim kümesi tarafından sağlanan Web Parçaları denetim kümesi tarafından sağlanan Web Parçaları denetim kümesini kullanarak tasarımcıdaki denetimi doğru şekilde yapılandırabilirsiniz. Bu, Web Parçaları uygulamalarının geliştirilmesini hızlandırabilir ve yazmanız gereken kod miktarını azaltabilir.

## <a name="control-development"></a>Kontrol Geliştirme

Standart Web sunucusu denetimleri, özel sunucu denetimleri ve kullanıcı denetimleri de dahil olmak üzere, varolan tüm ASP.NET denetimini Web Parçaları denetimi olarak kullanabilirsiniz. Ortamınızın maksimum programlı denetimi için, WebPart sınıfından türeyen özel Web Parçaları denetimleri de oluşturabilirsiniz. Tek tek Web Parçaları denetimi geliştirmesi için, genellikle bir kullanıcı denetimi oluşturur ve web parçaları denetimi olarak kullanır veya özel bir Web Parçaları denetimi geliştirirsiniz.

Özel bir Web Parçaları denetimi geliştirmeye örnek olarak, diğer ASP.NET sunucu denetimleri tarafından sağlanan ve kişiselleştirilebilir bir Web Parçaları denetimi olarak paketlenebilir özelliklerden herhangi birini sağlamak için bir denetim oluşturabilirsiniz: takvimler, listeler, finansal bilgiler, haberler, hesap makineleri, içeriği güncelleştirmek için zengin metin denetimleri, veritabanlarına bağlanan editable ızgaralar, ekranlarını dinamik olarak güncelleştiren grafikler , veya hava ve seyahat bilgileri. Denetiminizi kullanarak görsel bir tasarımcı sağlarsanız, Visual Studio'u kullanan herhangi bir sayfa geliştiricisi denetiminizi bir Web Bölgesine sürükleyebilir ve ek kod yazmak zorunda kalmadan tasarım zamanında yapılandırabilir.

Kişiselleştirme, Web Parçaları özelliğinin temelidir. Kullanıcıların bir sayfadaki Web Parçaları denetimlerinin düzenini, görünümünü ve davranışını değiştirmelerine veya kişiselleştirmelerine olanak tanır. Kişiselleştirilmiş ayarlar uzun ömürlüdür: yalnızca geçerli tarayıcı oturumu sırasında (görünüm durumunda olduğu gibi) değil, aynı zamanda uzun süreli depolama da devam eder, böylece kullanıcının ayarları da gelecekteki tarayıcı oturumları için kaydedilir. Web Bölümleri sayfaları için varsayılan olarak kişiselleştirme etkinleştirilir.

UI yapısal bileşenleri kişiselleştirmeye dayanır ve tüm Web Parçaları denetimleri için gereken temel yapı yı ve hizmetleri sağlar. Her Web Parçaları sayfasında gerekli bir UI yapısal bileşeni WebPartManager denetimidir. Hiçbir zaman görünmese de, bu denetim, bir sayfadaki tüm Web Parçaları denetimlerini koordine etme gibi kritik bir görevi vardır. Örneğin, tüm tek tek Web Parçaları denetimlerini izler. Web Parçaları bölgelerini (sayfada Web Parçaları denetimleri içeren bölgeler) ve hangi denetimlerin hangi bölgelerde olduğunu yönetir. Ayrıca, göz atma, bağlanma, değiştirme veya katalog modu gibi bir sayfanın olabileceği farklı ekran modlarını ve kişiselleştirme değişikliklerinin tüm kullanıcılar için mi yoksa tek tek kullanıcılar için mi geçerli olduğunu izler ve denetler. Son olarak, Web Parçaları denetimleri arasındaki bağlantıları ve iletişimi başlatır ve izler.

İkinci tür ui yapısal bileşeni bölgedir. Bölgeler, Web Bölümleri sayfasında düzen yöneticileri olarak hareket eder. Bölüm sınıfından (parça denetimleri) türeyen denetimler içerir ve düzenler ve yatay veya dikey yönlendirmede modüler sayfa düzeni yapma olanağı sağlar. Bölgeler ayrıca içerdikleri her denetim için ortak ve tutarlı u-u bilgi aracı öğeleri (üstbilgi ve altbilgi stili, başlık, kenarlık stili, eylem düğmeleri vb.) sunar; bu ortak öğeler bir denetimin krom olarak bilinir. Farklı görüntü modlarında ve çeşitli denetimlerde çeşitli özel bölge türleri kullanılır. Farklı bölge türleri aşağıdaki Web Parçaları Temel Denetimleri bölümünde açıklanmıştır.

Tümü **Bölüm** sınıfından türetilen Web Parçaları Web Parçaları Web Parçaları Web Parçaları denetimleri, Web Bölümleri sayfasındaki birincil Web Arama Ayını'nı oluşturur. Web Parçaları kontrol kümesi esnektir ve parça denetimleri oluşturmak için size verdiği seçeneklere dahildir. Kendi özel Web Parçaları denetimlerinizi oluşturmanın yanı sıra, Web Parçaları denetimleri olarak varolan sunucu denetimleri, kullanıcı denetimleri veya özel sunucu denetimleri ASP.NET de kullanabilirsiniz. Web Parçaları sayfalarını oluşturmak için en sık kullanılan temel denetimler sonraki bölümde açıklanmıştır.

## <a name="web-parts-essential-controls"></a>Web Parçaları Temel Kontroller

Web Parçaları denetim kümesi kapsamlıdır, ancak Web Bölümlerinin çalışması için gerekli olduklarından veya Web Parçaları sayfalarında en sık kullanılan denetimler olduklarından bazı denetimler gereklidir. Web Bölümleri'ni kullanmaya ve temel Web Parçaları sayfalarını oluşturmaya başladığınızda, aşağıdaki tabloda açıklanan temel Web Parçaları denetimlerine aşina olmak yararlıdır.

| **Web Parçaları kontrolü** | **Açıklama** |
| --- | --- |
| Webpartmanager | Bir sayfadaki tüm Web Parçaları denetimlerini yönetir. Her Web Bölümü sayfası için bir (ve yalnızca bir) **WebPartManager** denetimi gereklidir. |
| Catalogzone | CatalogPart denetimleri içerir. Kullanıcıların sayfaya eklemek için denetimleri seçebileceği Web Parçaları denetimleri kataloğunu oluşturmak için bu bölgeyi kullanın. |
| Editorzone | EditorPart denetimlerini içerir. Kullanıcıların web parçaları denetimlerini bir sayfadaki olarak ve kişiselleştirmelerini sağlamak için bu bölgeyi kullanın. |
| Webpartzone | Bir sayfanın ana Kullanıcı Arabirimi'ni oluşturan WebPart denetimleri için genel düzeni içerir ve sağlar. Web Parçaları denetimleri içeren sayfalar oluşturduğunuzda bu bölgeyi kullanın. Sayfalar bir veya daha fazla bölge içerebilir. |
| Connectionszone | WebPartConnection denetimleri içerir ve bağlantıları yönetmek için bir kullanıcı arabirimi sağlar. |
| Web Part (GenericWebPart) | Birincil UI'yi işler; çoğu Web Parçaları Web Parts UI denetimi bu kategoriye girer. Maksimum programlı denetim için, temel **WebPart** denetiminden türeyen özel Web Parçaları denetimleri oluşturabilirsiniz. Web Parçaları denetimleri olarak varolan sunucu denetimlerini, kullanıcı denetimlerini veya özel denetimleri de kullanabilirsiniz. Bu denetimlerden herhangi biri bir bölgeye yerleştirildiğinde, **WebPartManager** denetimi bunları otomatik olarak çalışma zamanında **GenericWebPart** denetimleriyle sarar, böylece Bunları Web Parçaları işlevselliğiyle kullanabilirsiniz. |
| Catalogpart | Kullanıcıların sayfaya ekleyebileceği kullanılabilir Web Parçaları denetimlerinin listesini içerir. |
| Webpartconnection | Bir sayfadaki iki Web Parçası denetimi arasında bağlantı oluşturur. Bağlantı, Web Parçaları denetimlerinden birini sağlayıcı (veri) ve diğerini tüketici olarak tanımlar. |
| Editorpart | Özel düzenleyici denetimleri için taban sınıf olarak hizmet vermektedir. |
| EditorPart denetimleri (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart ve PropertyGridEditorPart) | Kullanıcıların bir sayfadaki Web Parçaları Kullanıcı Arama Hizmeti denetimlerinin çeşitli yönlerini kişiselleştirmesine izin verme |

## <a name="lab-create-a-web-part-page"></a>Laboratuvar: Web Bölümü Sayfası Oluşturma

Bu laboratuvarda, ASP.NET profilleri aracılığıyla bilgileri kalıcı olarak devam edecek bir Web bölümü sayfası oluşturursunuz.

### <a name="creating-a-simple-page-with-web-parts"></a>Web Parçalarıyla Basit Bir Sayfa Oluşturma

Gözden geçirmenin bu bölümünde, statik içeriği göstermek için Web Parçaları denetimlerini kullanan bir sayfa oluşturursunuz. Web Parçaları ile çalışmanın ilk adımı, iki gerekli yapısal öğeye sahip bir sayfa oluşturmaktır. İlk olarak, Web bölümleri sayfasının tüm Web Parçaları denetimlerini izlemek ve koordine etmek için bir WebPartManager denetimine ihtiyacı vardır. İkinci olarak, Bir Web Parçaları sayfası, WebPart veya diğer sunucu denetimleri içeren ve sayfanın belirli bir bölgesini işgal eden bileşik denetimler olan bir veya daha fazla bölgeye ihtiyaç duyar.

> [!NOTE]
> Web Parçaları kişiselleştirmesağlamak için bir şey yapmanız gerekmez; Web Parçaları denetim kümesi için varsayılan olarak etkinleştirilir. Bir sitede ilk kez bir Web Parts sayfasını çalıştırdığınızda, ASP.NET kullanıcı kişiselleştirme ayarlarını depolamak için varsayılan bir kişiselleştirme sağlayıcısı ayarlar. Kişiselleştirme hakkında daha fazla bilgi için Web Bölümleri Kişiselleştirme Genel Bakış bölümüne bakın.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>Web Parçaları denetimleri içeren bir sayfa oluşturmak için

1. Varsayılan sayfayı kapatın ve WebPartsDemo.aspx adlı siteye yeni bir sayfa ekleyin.
2. **Tasarım** görünümüne geçin.
3. **Görünüm** menüsünden, **Görsel Olmayan Denetimler** ve **Ayrıntılar** seçeneklerinin seçildiğinden emin olun, böylece arama aysayısı olmayan düzen etiketlerini ve denetimlerini görebilirsiniz.
4. Ekleme noktasını etiketlerin `<div>` önüne tasarım yüzeyine yerleştirin ve yeni bir satır eklemek için ENTER tuşuna basın. Ekleme noktasını yeni satır karakterinden önce konumlandırın, menüdeki **Biçim** açılır liste denetimini engelle'yi tıklatın ve **Başlık 1** seçeneğini seçin. Başlıkta, metin **Web Parçaları Tanıtım Sayfası**ekleyin.
5. Araç Kutusunun **Web Parts** sekmesinden, bir **WebPartManager** denetimini sayfaya sürükleyin ve yeni `<div>`satır karakterinden hemen sonra ve etiketlerden önce konumlandırın.   
  
   **WebPartManager** denetimi herhangi bir çıktı oluşturmaz, bu nedenle tasarımcı yüzeyinde gri bir kutu olarak görünür.
6. Ekleme noktasını etiketlerin `<div>` içine yerleştirin.
7. **Düzen** menüsünde **Tablo Ekle'yi**tıklatın ve bir satır ve üç sütuniçeren yeni bir tablo oluşturun. Hücre **Özellikleri** düğmesini tıklatın, **Dikey hizalama** açılır listesinden **üstünü** seçin, **Tamam'ı**tıklatın ve tabloyu oluşturmak için yeniden **Tamam'ı** tıklatın.
8. WebPartZone denetimini sol tablo sütununa sürükleyin. **WebPartZone** denetimine sağ tıklayın, **Özellikler'i**seçin ve aşağıdaki özellikleri ayarlayın:   
  
   ID: Kenar ÇubuğuBölgesi   
  
   Üstbilgi Metni: Kenar Çubuğu
9. İkinci bir **WebPartZone** denetimini orta tablo sütununa sürükleyin ve aşağıdaki özellikleri ayarlayın:   
  
   ID: MainZone   
  
   BaşlıkMetni: Ana
10. Dosyayı kaydedin.

Sayfanızın artık ayrı olarak denetleyebileceğiniz iki ayrı bölgesi vardır. Ancak, her iki bölgenin de içeriği yoktur, bu nedenle içerik oluşturmak bir sonraki adımdır. Bu gözden geçirme için, yalnızca statik içeriği görüntüleyen Web Parçaları denetimleriyle çalışırsınız.

Web Parçaları bölgesinin düzeni, &lt;bölge şablonu&gt; öğesi tarafından belirtilir. Bölge şablonuna, ister özel Web Parçaları denetimi, ister kullanıcı denetimi veya varolan bir sunucu denetimi olsun, herhangi bir ASP.NET denetimi ekleyebilirsiniz. Burada Etiket denetimini kullandığınıza ve yalnızca statik metin eklediğinize dikkat edin. **Bir WebPartZone** bölgesine normal bir sunucu denetimi yerleştirdiğinizde, ASP.NET denetimi çalışma zamanında Web Parçaları denetimi olarak ele verir ve bu da web parçaları özelliklerinin denetimde olmasını sağlar.

**Ana bölge için içerik oluşturmak için**

1. **Tasarım** görünümünde, Bir **Etiket** denetimini Araç Kutusu'nun **Standart** sekmesinden, **kimliği** MainZone olarak ayarlanmış bölgenin içindekiler alanına sürükleyin.
2. **Kaynak** görünümüne geçin. **Etiket** denetimini&gt; MainZone'da sarmak için bir &lt;zonetemplate öğesi eklendi.
3. asp:label &lt;&gt; öğesine **başlık** adlı bir öznitelik ekleyin ve değerini İçerik olarak ayarlayın. Asp:label &lt;&gt; öğesinden Text="Label" özniteliğini kaldırın. &lt;asp:label&gt; öğesinin açılış ve kapanış etiketleri arasında, &lt;bir çift h2&gt; öğesi etiketi içinde Ana **Sayfama Hoş Geldiniz** gibi bazı metinler ekleyin. Kodunuz aşağıdaki gibi görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Dosyayı kaydedin.

Ardından, sayfaya Web Parçaları denetimi olarak da eklenebilecek bir kullanıcı denetimi oluşturun.

### <a name="to-create-a-user-control"></a>Kullanıcı denetimi oluşturmak için

1. Arama denetimi olarak hizmet vermek için sitenize yeni bir Web kullanıcı denetimi ekleyin. **Kaynak kodunu ayrı bir dosyaya yerleştirme**seçeneğini seçin. WebPartsDemo.aspx sayfasıyla aynı dizine ekleyin ve SearchUserControl.ascx adını.   
  
    > [!NOTE]
    > Bu gözden geçirme için kullanıcı denetimi gerçek arama işlevini uygulamaz; yalnızca Web Parçaları özelliklerini göstermek için kullanılır.
2. **Tasarım** görünümüne geçin. Araç Kutusu'nun **Standart** sekmesinden, textbox denetimini sayfaya sürükleyin.
3. Ekleme noktasını az önce eklediğiniz metin kutusundan sonra yerleştirin ve yeni bir satır eklemek için ENTER tuşuna basın.
4. Az önce eklediğiniz metin kutusunun altındaki yeni satırdaki sayfaya düğme denetimini sürükleyin.
5. **Kaynak** görünümüne geçin. Kullanıcı denetimi için kaynak kodunun aşağıdaki örnek gibi göründüğünden emin olun. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Dosyayı kaydedin ve kapatın.

Artık Kenar Çubuğu bölgesine Web Parçaları denetimleri ekleyebilirsiniz. Kenar Çubuğu bölgesine biri bağlantı listesini ve diğeri de önceki yordamda oluşturduğunuz kullanıcı denetimi içeren iki denetim ekliyorsunuz. Bağlantılar, Ana bölge için statik metni oluşturma şeklinize benzer standart bir **Etiket** sunucusu denetimi olarak eklenir. Ancak, kullanıcı denetiminde bulunan tek tek sunucu denetimleri doğrudan bölgede (etiket denetimi gibi) bulunabilir, ancak bu durumda değildir. Bunun yerine, bunlar önceki yordamda oluşturduğunuz kullanıcı denetiminin bir parçasıdır. Bu, kullanıcı denetiminde istediğiniz denetimleri ve ekstra işlevselliği paketlemenin ve ardından bu denetime Web Parçaları denetimi olarak başvurmanın yaygın bir yolunu gösterir.

Çalışma zamanında, Web Parçaları denetim kümesi genericWebPart denetimleri ile her iki denetimi de sarar. **GenericWebPart** denetimi bir Web sunucusu denetimini sararsa, genel parça denetimi üst denetimdir ve sunucu denetimine üst denetimin ChildControl özelliği üzerinden erişebilirsiniz. Genel parça denetimlerinin bu kullanımı, standart Web sunucusu denetimlerinin **WebPart** sınıfından türeyen Web Parçaları denetimleri ile aynı temel davranış ve özniteliklere sahip olmasını sağlar.

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>Kenar çubuğu bölgesine Web Parçaları denetimleri eklemek için

1. WebPartsDemo.aspx sayfasını açın.
2. **Tasarım** görünümüne geçin.
3. Oluşturduğunuz kullanıcı denetim sayfası SearchUserControl.ascx'i **Solution Explorer'dan** **kimlik** özelliği SidebarZone olarak ayarlanmış bölgeye sürükleyin ve oraya bırakın.
4. WebPartsDemo.aspx sayfasını kaydedin.
5. **Kaynak** görünümüne geçin.
6. SidebarZone için &lt;asp:webpartzone&gt; öğesiiçinde, kullanıcı denetiminize yapılan başvurunun &lt;hemen üzerinde, aşağıdaki örnekte gösterildiği gibi, içerdiği bağlantıları içeren bir asp:etiket&gt; öğesi ekleyin. Ayrıca, gösterildiği gibi **Arama**değeriile kullanıcı denetim etiketine bir **Başlık** özniteliği ekleyin. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Dosyayı kaydedin ve kapatın.

Artık sayfanızı tarayıcınızda tutarak test edebilirsiniz. Sayfa iki bölge görüntüler. Aşağıdaki ekran görüntüsü sayfayı gösterir.

**İki bölgeli Web Parçaları Demo sayfası**

![Web Parçaları VS Walkthrough 1 Ekran Görüntüsü](profiles-themes-and-web-parts/_static/image3.gif)

**Şekil 3**: Web Parçaları VS Walkthrough 1 Ekran Görüntüsü

Her denetimin başlık çubuğunda, denetimde gerçekleştirebileceğiniz kullanılabilir eylemlerden oluşan fiiller menüsüne erişim sağlayan aşağı doğru bir ok bulunur. Denetimlerden biri için fiiller menüsünü tıklatın, ardından **Simge durumuna küçült'ü** tıklatın ve denetimin en aza indirilmiş olduğunu unutmayın. Fiiller menüsünden **Geri Yükle'yi**tıklatın ve denetim normal boyutuna döner.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Kullanıcıların Sayfaları Düzenlemesini ve Düzeni Değiştirmesini Etkinleştirme

Web Parçaları, kullanıcıların web parçaları denetimlerinin düzenini bir bölgeden diğerine sürükleyerek değiştirme olanağı sağlar. Kullanıcıların **WebPart** denetimlerini bir bölgeden diğerine taşımasına izin vermenin yanı sıra, kullanıcıların görünümleri, düzenleri ve davranışları da dahil olmak üzere denetimlerin çeşitli özelliklerini ayarlamalarına izin verebilirsiniz. Web Parçaları denetim kümesi, **WebPart** denetimleri için temel düzenleme işlevselliği sağlar. Bu izlenecek yolda bunu yapmasanız da, kullanıcıların **WebPart** denetimlerinin özelliklerini yeniden oluşturmasına olanak tanıyan özel düzenleyici denetimleri de oluşturabilirsiniz. **WebPart** denetiminin konumunu değiştirmede olduğu gibi, denetimin özelliklerini düzenlemek, kullanıcıların yaptığı değişiklikleri kaydetmek için ASP.NET kişiselleştirmeye dayanır.

Bu bölümün bu bölümünde, kullanıcıların sayfadaki herhangi bir **WebPart** denetiminin temel özelliklerini de Bu özellikleri etkinleştirmek için, sayfaya bir asp:editorzone &lt;&gt; öğesi ve iki düzenleme denetimiyle birlikte başka bir özel kullanıcı denetimi eklersiniz.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>Sayfa düzenini değiştirmeyi sağlayan bir kullanıcı denetimi oluşturmak için

1. Visual Studio'da Dosya **menüsünde** **Yeni** alt menüsünü seçin ve **Dosya** seçeneğini tıklatın.
2. Yeni **Öğe Ekle** iletişim kutusunda **Web Kullanıcı Denetimi'ni**seçin. Yeni dosyadisplayModeMenu.ascx adını verin. **Kaynak kodunu ayrı bir dosyaya yerleştirme**seçeneğini seçin.
3. Yeni denetim oluşturmak için Ekle'yi tıklatın.
4. **Kaynak** görünümüne geçin.
5. Yeni dosyadaki varolan tüm kodu kaldırın ve aşağıdaki koda yapıştırın. Bu kullanıcı denetim kodu, bir sayfanın görünümünü veya görüntü modunu değiştirmesini sağlayan Web Parçaları denetim kümesinin özelliklerini kullanır ve belirli görüntü modlarındayken sayfanın fiziksel görünümünü ve düzenini değiştirmenizi sağlar. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Araç çubuğundaki kaydet simgesine tıklayarak veya **Dosya** menüsünde Kaydet'i seçerek dosyayı **kaydedin.**

### <a name="to-enable-users-to-change-the-layout"></a>Kullanıcıların düzeni değiştirmesini sağlamak için

1. WebPartsDemo.aspx sayfasını açın ve **Tasarım** görünümüne geçin.
2. Ekleme **noktasını,** daha önce eklediğiniz **WebPartManager** denetiminden hemen sonra Tasarım görünümüne yerleştirin. **WebPartManager** denetiminden sonra boş bir satır olması için metinden sonra sabit bir geri dönüş ekleyin. Ekleme noktasını boş satıra yerleştirin.
3. Oluşturduğunuz kullanıcı denetimini (dosya DisplayModeMenu.ascx olarak adlandırılır) WebPartsDemo.aspx sayfasına sürükleyin ve boş satıra bırakın.
4. Bir EditorZone denetimini Araç Kutusu'nun **WebParts** bölümünden WebPartsDemo.aspx sayfasında kalan açık tablo hücresine sürükleyin.
5. Toolbox'ın **WebParts** bölümünden AppearanceEditorPart denetimini ve LayoutEditorPart denetimini **EditorZone** denetimine sürükleyin.
6. **Kaynak** görünümüne geçin. Tablo hücresinde ortaya çıkan kod aşağıdaki koda benzer görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. WebPartsDemo.aspx dosyasını kaydedin. Görüntü modlarını ve sayfa düzenini değiştirmenize olanak tanıyan bir kullanıcı denetimi oluşturdunuz ve birincil Web sayfasındaki denetime başvurulmuşsunuz.

Artık sayfaları düzene ve düzeni değiştirme özelliğini sınayabilirsiniz.

### <a name="to-test-layout-changes"></a>Düzen değişikliklerini sınamak için

1. Sayfayı tarayıcıya yükleyin.
2. **Görüntümodu** açılır menüsüne tıklayın ve **Edit'i**seçin. Bölge başlıkları görüntülenir.
3. **Bağlantılarım** denetimini kenar çubuğu bölgesinden Ana bölgenin altına kadar başlık çubuğuna göre sürükleyin. Sayfanız aşağıdaki ekran görüntüsüne benzemelidir.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Bağlantılarım denetimi ile Web Bölümleri Demo sayfası taşındı

![Web Parçaları VS Walkthrough 2 Ekran Görüntüsü](profiles-themes-and-web-parts/_static/image4.gif)

**Şekil 4**: Web Parçaları VS Walkthrough 2 Ekran Görüntüsü

1. **Görüntümodu** açılır menüsüne tıklayın ve **Gözat'ı**seçin. Sayfa yenilenir, bölge adları kaybolur ve **Bağlantılarım** denetimi konumunuz da burada kalır.
2. Kişiselleştirmenin çalıştığını göstermek için tarayıcıyı kapatın ve sayfayı yeniden yükleyin. Yaptığınız değişiklikler gelecekteki tarayıcı oturumları için kaydedilir.
3. Ekran **Modu** menüsünden **Edit'i**seçin.   
  
   Sayfadaki her denetim artık başlık çubuğunda, açılan fiilleri içeren bir aşağı okla görüntülenir.
4. **Linklerimle** düğmesindeki fiiller menüsünü görüntülemek için oku tıklatın. **Edit** fiilini tıklatın.   
  
   **EditorZone** denetimi görüntülenir ve eklediğiniz EditorPart denetimlerini görüntüler.
5. Denetimin **Görünüm** bölümünde, **Başlığı** Sık Kullanılanlarım olarak değiştirin, **Yalnızca Başlık'ı**seçmek için **Chrome Türü** açılır listesini kullanın ve sonra **Uygula'yı**tıklatın. Aşağıdaki ekran görüntüsü sayfayı edit modunda gösterir.

### <a name="web-parts-demo-page-in-edit-mode"></a>Web Parçaları Demo sayfasını Edit modunda

![Web Parçaları VS Walkthrough 3 Ekran Görüntüsü](profiles-themes-and-web-parts/_static/image5.gif)

**Şekil 5**: Web Parçaları VS Walkthrough 3 Ekran Görüntüsü

1. Görüntü **modu** menüsüne tıklayın ve gözatma moduna dönmek için **Gözat'ı** seçin.
2. Denetim şimdi güncelleştirilmiş bir başlık ve aşağıdaki ekran görüntüsünde gösterildiği gibi kenarlık vardır.

### <a name="edited-web-parts-demo-page"></a>Düzenlenen Web Bölümleri Demo sayfası

![Web Parçaları VS Walkthrough 4 Ekran Görüntüsü](profiles-themes-and-web-parts/_static/image6.gif)

**Şekil 4**: Web Parçaları VS Walkthrough 4 Ekran Görüntüsü

### <a name="adding-web-parts-at-run-time"></a>Çalışma Zamanında Web Parçaları Ekleme

Ayrıca, kullanıcıların çalışma zamanında sayfalarına Web Parçaları denetimleri eklemelerine de izin verebilirsiniz. Bunu yapmak için, sayfayı, kullanıcıların kullanımına açmak istediğiniz Web Parçaları denetimlerinin listesini içeren bir Web Parçaları kataloğuyla yapılandırın.

**Kullanıcıların çalışma zamanında Web Parçaları eklemesine izin vermek için**

1. WebPartsDemo.aspx sayfasını açın ve **Tasarım** görünümüne geçin.
2. Toolbox'ın **Web Parts** sekmesinden, CatalogZone denetimini **EditorZone** denetiminin altındaki tablonun sağ sütununa sürükleyin.   
  
   Aynı anda görüntülenmeyecekleri için her iki denetim de aynı tablo hücresinde olabilir.
3. Özellikler bölmesinde, Web Parçaları **Ekle** dizesini **CatalogZone** denetiminin HeaderText özelliğine atayın.
4. Toolbox'ın **WebParts** bölümünden, DeclarativeCatalogPart denetimini **CatalogZone** denetiminin içerik alanına sürükleyin.
5. Görevler menüsünü ortaya çıkarmak için **DeclarativeCatalogPart** denetiminin sağ üst köşesindeki oku tıklatın ve ardından **Şablonları Edit'i**seçin.
6. Araç Kutusunun **Standart** bölümünden, Bir **FileUpload** denetimini ve **Takvim** denetimini **DeclarativeCatalogPart** denetiminin **WebPartsTemplate** bölümüne sürükleyin.
7. **Kaynak** görünümüne geçin. asp:catalogzone&gt; &lt;öğesinin kaynak kodunu inceleyin. **DeclarativeCatalogCatalogPart** denetiminde, &lt;kataloğuzdan&gt; sayfanıza ekleyebileceğiniz iki kapalı sunucu denetimiyle birlikte bir web partstemplate öğesi bulunduğuna dikkat edin.
8. Aşağıdaki kod örneğinde her başlık için gösterilen dize değerini kullanarak, kataloğa eklediğiniz denetimlerin her birine bir **Başlık** özelliği ekleyin. Başlık normalde bu iki sunucu denetiminde tasarım zamanında ayarlaabileceğiniz bir özellik olmasa da, bir kullanıcı bu denetimleri çalışma zamanında katalogdan **bir WebPartZone** bölgesine eklediğinde, her biri **GenericWebPart** denetimiyle sarılır. Bu, web parçaları denetimleri olarak hareket etmelerini sağlar, böylece başlıkları görüntüleyebilirler.   
  
   **DeclarativeCatalogPart** denetiminde yer alan iki denetimin kodu aşağıdaki gibi görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Sayfayı kaydedin.

Artık kataloğu test edebilirsiniz.

### <a name="to-test-the-web-parts-catalog"></a>Web Parçaları kataloğunu test etmek için

1. Sayfayı tarayıcıya yükleyin.
2. Görüntü **modu** açılır menüsüne tıklayın ve **Katalog'u**seçin.   
  
   **Web Parçaları Ekle** başlıklı katalog görüntülenir.
3. **Favorilerim** denetimini Ana bölgeden Kenar Çubuğu bölgesinin en üstüne sürükleyin ve oraya bırakın.
4. Web **Parçaları Ekle** kataloğunda, her iki onay kutusunu seçin ve ardından kullanılabilir bölgeleri içeren açılır listeden **Main'i** seçin.
5. Katalogda **Ekle'yi** tıklatın. Denetimler Ana bölgeye eklenir. İsterseniz, kataloğunuza birden çok denetim örneği ekleyebilirsiniz.   
  
   Aşağıdaki ekran görüntüsü, dosya yükleme denetiminin olduğu sayfayı ve Ana bölgedeki takvimi gösterir. 

![Katalogdan Ana bölgeye eklenen denetimler](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. **Görüntümodu** açılır menüsüne tıklayın ve **Gözat'ı**seçin. Katalog kaybolur ve sayfa yenilenir.
7. Tarayıcıyı kapatın. Sayfayı yeniden yükleyin. Yaptığınız değişiklikler devam ediyor.
