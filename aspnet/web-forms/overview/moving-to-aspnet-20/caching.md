---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Önbelleğe Alma | Microsoft Dokümanlar
author: rick-anderson
description: Önbelleğe alma nın anlaşılması, iyi performans gösteren bir ASP.NET uygulaması için önemlidir. ASP.NET 1.x önbelleğe alma için üç farklı seçenek sundu; çıkış önbelleğe alma,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542943"
---
# <a name="caching"></a>Önbelleğe alma

[Microsoft](https://github.com/microsoft) tarafından

> Önbelleğe alma nın anlaşılması, iyi performans gösteren bir ASP.NET uygulaması için önemlidir. ASP.NET 1.x önbelleğe alma için üç farklı seçenek sundu; çıkış önbelleğe alma, parça önbelleğe alma ve önbellek API..

Önbelleğe alma nın anlaşılması, iyi performans gösteren bir ASP.NET uygulaması için önemlidir. ASP.NET 1.x önbelleğe alma için üç farklı seçenek sundu; çıkış önbelleğe alma, parça önbelleğe alma ve önbellek API.. ASP.NET 2.0 bu yöntemlerin üçünü de sunar, ancak bazı önemli ek özellikler ekler. Birkaç yeni önbellek bağımlılıkları vardır ve geliştiriciler artık özel önbellek bağımlılıkları oluşturma seçeneğine de sahiptir. Önbelleğe alma yapılandırması da 2.0 ASP.NET önemli ölçüde geliştirilmiştir.

## <a name="new-features"></a>Yeni Özellikler

## <a name="cache-profiles"></a>Önbellek Profilleri

Önbellek profilleri, geliştiricilerin daha sonra tek tek sayfalara uygulanabilecek belirli önbellek ayarlarını tanımlamasına olanak tanır. Örneğin, önbellekten 12 saat sonra süresi dolması gereken bazı sayfalarınız varsa, bu sayfalara uygulanabilecek bir önbellek profili kolayca oluşturabilirsiniz. Yeni bir önbellek profili eklemek &lt;için yapılandırma&gt; dosyasındaki önbellek ayarları bölümünü kullanın. Örneğin, aşağıda, önbellek süresini 12 saatlik yapılandıran *iki gün* olarak adlandırılan bir önbellek profilinin yapılandırması verilmiştir.

[!code-xml[Main](caching/samples/sample1.xml)]

Bu önbellek profilini belirli bir sayfaya uygulamak için, aşağıda gösterildiği gibi @ OutputCache yönergesinin Önbellek özniteliğini kullanın:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Özel Önbellek Bağımlılıkları

ASP.NET 1.x geliştiricileri özel önbellek bağımlılıkları için bağırdı. 1.x ASP.NET, CacheDependency sınıfı, geliştiricilerin kendi sınıflarını kendi sınıflarından türemesini engelleyen mühürlendi. 2.0 ASP.NET bu sınırlama kaldırılır ve geliştiriciler kendi özel önbellek bağımlılıklarını geliştirmekte özgürdür. CacheDependency sınıfı, dosyalara, dizinlere veya önbellek anahtarlarına dayalı özel bir önbellek bağımlılığı oluşturulmasına olanak tanır.

Örneğin, aşağıdaki kod, Web uygulamasının kökünde bulunan stuff.xml adlı dosyayı temel alan yeni bir özel önbellek bağımlılığı oluşturur:

[!code-csharp[Main](caching/samples/sample3.cs)]

Bu senaryoda, stuff.xml dosyası değiştiğinde önbelleğe alınmış öğe geçersiz kılınır.

Önbellek anahtarlarını kullanarak özel bir önbellek bağımlılığı oluşturmak da mümkündür. Bu yöntemi kullanarak, önbellek anahtarının kaldırılması önbelleğe alınan verileri geçersiz kılınır. Aşağıdaki örnekte bu gösterilmektedir:

[!code-csharp[Main](caching/samples/sample4.cs)]

Yukarıda eklenen öğeyi geçersiz kAklamak için önbellek anahtarı olarak hareket etmek için önbelleğe eklenen öğeyi kaldırmanız yeterlidir.

[!code-csharp[Main](caching/samples/sample5.cs)]

Önbellek anahtarı gibi davranan öğenin anahtarının önbellek anahtarları dizisine eklenen değerle aynı olması gerektiğini unutmayın.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Yoklama Tabanlı SQL Önbellek Bağımlılıkları (Tablo Tabanlı Bağımlılıklar olarak da adlandırılır)

SQL Server 7 ve 2000, SQL önbellek bağımlılıkları için yoklama tabanlı modeli kullanır. Yoklama tabanlı model, tablodaki veriler değiştiğinde tetiklenen bir veritabanı tablosunda tetikleyici kullanır. Bu tetikleyici, bildirim tablosunda ASP.NET düzenli aralıklarla denetlediği bir **changeId** alanını güncelleştirir. **ChangeId** alanı güncelleştirilmişse, ASP.NET verilerin değiştiğini bilir ve önbelleğe alınan verileri geçersiz kılır.

> [!NOTE]
> SQL Server 2005 yoklama tabanlı modeli de kullanabilir, ancak yoklama tabanlı model en verimli model olmadığından, SQL Server 2005 ile sorgu tabanlı bir model (daha sonra tartışılan) kullanılması tavsiye edilir.

Yoklama tabanlı modeli kullanan bir SQL önbellek bağımlılığının doğru çalışması için tabloların bildirimleri etkinleştirilmiş olması gerekir. Bu programlı SqlCacheDependencyAdmin sınıf kullanılarak veya aspnet\_regsql.exe yardımcı programı kullanılarak gerçekleştirilebilir.

Aşağıdaki komut satırı, SQL önbellek bağımlılığı için *dbase* adlı bir SQL Server örneğinde bulunan Northwind veritabanındaki Ürünler tablosunu kaydeder.

[!code-console[Main](caching/samples/sample6.cmd)]

Yukarıdaki komutta kullanılan komut satırı anahtarlarının açıklaması aşağıda veda edilebedilir:

| **Komut Hattı Anahtarı** | **Amaç** |
| --- | --- |
| -S *sunucusu* | Sunucu adını belirtir. |
| -ed | SQL önbellek bağımlılığı için veritabanının etkinleştirilmesi gerektiğini belirtir. |
| -d *\_veritabanı adı* | SQL önbellek bağımlılığı için etkinleştirilmesi gereken veritabanı adını belirtir. |
| -E | Aspnet\_regsql veritabanına bağlanırken Windows kimlik doğrulaması kullanmanız gerektiğini belirtir. |
| -et | SQL önbellek bağımlılığı için bir veritabanı tablosu etkinleştirdiğimizi belirtir. |
| -t *\_tablo adı* | SQL önbellek bağımlılığını etkinleştirmek için veritabanı tablosunun adını belirtir. |

> [!NOTE]
> Aspnet\_regsql.exe için başka anahtarlar da mevcuttur. Tam bir liste için,\_aspnet regsql.exe çalıştırın -? bir komut satırından.

Bu komut çalıştığında SQL Server veritabanında aşağıdaki değişiklikler yapılır:

- **AspNet\_SqlCacheTablesForChangeNotification** tablosu eklenir. Bu tablo, veritabanında bir SQL önbellek bağımlılığının etkinlendiği her tablo için bir satır içerir.
- Aşağıdaki depolanan yordamlar veritabanının içinde oluşturulur:

| AspNet\_SqlCachePollingStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification tablosunu sorgular ve SQL önbellek bağımlılığı ve her tablo için changeId değeri için etkinleştirilen tüm tabloları döndürür. Bu depolanan proc, verilerin değişip değişmediğini belirlemek için yoklama için kullanılır. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification tablosunu sorgulayarak SQL önbellek bağımlılığı için etkin olan tüm tabloları döndürür ve SQL önbellek bağımlılığı için etkin olan tüm tabloları döndürür. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | Bildirim tablosuna gerekli girişi ekleyerek SQL önbellek bağımlılığı için bir tablo kaydeder ve tetikleyiciyi ekler. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | Bildirim tablosundaki girişi kaldırarak SQL önbellek bağımlılığı için bir tabloyu kaldırır ve tetikleyiciyi kaldırır. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | Değiştirilen tablo için changeId'yi artımlayarak bildirim tablosunu güncelleştirir. ASP.NET, verilerin değişip değişmediğini belirlemek için bu değeri kullanır. Aşağıda belirtildiği gibi, tablo etkinleştirildiğinde oluşturulan tetikleyici tarafından bu depolanan proc yürütülür. |

- Tablo için ** _tablo\_adı_\_AspNet\_SqlCacheNotification\_Trigger** adlı bir SQL Server tetikleyicisi oluşturulur. Bu tetikleyici, tabloda\_bir INSERT, UPDATE veya DELETE yapıldığında AspNet SqlCacheUpdateChangeIdStoredProcedure'ı yürütür.
- **Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** adlı bir SQL Server rolü veritabanına eklenir.

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server rolü, AspNet\_SqlCachePollingStoredProcedure için EXEC izinlerine sahiptir. Yoklama modelinin doğru çalışması için işlem hesabınızı aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess rolüne eklemeniz gerekir. Aspnet\_regsql.exe aracı bunu sizin için yapmaz.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Yoklama Tabanlı SQL Önbellek Bağımlılıklarını Yapılandırma

Yoklama tabanlı SQL önbellek bağımlılıklarını yapılandırmak için gereken birkaç adım vardır. İlk adım veritabanı ve tablo yukarıda anlatıldığı gibi etkinleştirmektir. Bu adım tamamlandıktan sonra yapılandırmanın geri kalanı aşağıdaki gibidir:

- ASP.NET yapılandırma dosyasını yapılandırma.
- SqlCacheDependency yapılandırılması

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET Yapılandırma Dosyasını Yapılandırma

Önceki modülde belirtildiği gibi bir bağlantı dizesi eklemenin yanı &lt;sıra, aşağıda &lt;gösterildiği gibi&gt; bir sqlCacheDependency öğesi ile bir önbellek&gt; öğesi yapılandırmanız gerekir:

[!code-xml[Main](caching/samples/sample7.xml)]

Bu *yapılandırma, pubveritabanında* bir SQL önbellek bağımlılığı sağlar. sqlCacheDependency&gt; öğesindeki &lt;pollTime özniteliğinin varsayılan olarak 60000 milisaniye veya 1 dakika olduğunu unutmayın. (Bu değer 500 milisaniyeden az olamaz.) Bu örnekte, &lt;&gt; ekle öğesi yeni bir veritabanı ekler ve pollTime geçersiz kılar, 900000 milisaniye olarak ayar.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency yapılandırılması

Bir sonraki adım SqlCacheDependency yapılandırmaktır. Bunu başarmanın en kolay yolu @ Outcache yönergesinde SqlDependency özniteliğinin değerini aşağıdaki gibi belirtmektir:

[!code-aspx[Main](caching/samples/sample8.aspx)]

Yukarıdaki @ OutputCache yönergesinde, bir SQL önbellek bağımlılığı *pubs* veritabanında *yazarlar* tablosu için yapılandırılmıştır. Birden çok bağımlılık, bunları bir yarı-iki nokta nokta ile ayırarak yapılandırılabilir:

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency yapılandırma başka bir yöntem bunu programlı yapmaktır. Aşağıdaki kod, *pubveritabanındaki* *yazarlar* tablosunda yeni bir SQL önbelleği bağımlılığı oluşturur.

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL önbellek bağımlılığını programlı olarak tanımlamanın avantajlarından biri, oluşabilecek özel durumları işleyebileceğinizdir. Örneğin, bildirim için etkinleştirilmiş olmayan bir veritabanı için BIR SQL önbellek bağımlılığı tanımlamaya çalışırsanız, bir **DatabaseNotEnabledForNotificationException özel** durum atılır. Bu durumda, **SqlCacheDependencyAdmin.EnableNotifications** yöntemini arayarak ve veritabanı adını geçirerek bildirimler için veritabanını etkinleştirmeyi deneyebilirsiniz.

Aynı şekilde, bildirim için etkinleştirilmeyen bir tablo için bir SQL önbellek bağımlılığı tanımlamaya çalışırsanız, bir **TableNotEnabledForNotificationException** atılır. Daha sonra **SqlCacheDependencyAdmin.EnableTableForNotifications** yöntemi veritabanı adı ve tablo adı geçerek arayabilirsiniz.

Aşağıdaki kod örneği, SQL önbellek bağımlılığını yapılandırırken özel durum işlemenin nasıl doğru şekilde yapılandırılacağını göstermektedir.

[!code-csharp[Main](caching/samples/sample11.cs)]

Daha Fazla Bilgi:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Sorgu Tabanlı SQL Önbellek Bağımlılıkları (Yalnızca SQL Server 2005)

SQL önbellek bağımlılığı için SQL Server 2005 kullanırken, yoklama tabanlı model gerekli değildir. SQL Server 2005 ile kullanıldığında, SQL önbellek bağımlılıkları SQL Server örneğine SQL bağlantıları üzerinden doğrudan iletişim kurar (başka yapılandırma gerekmez) SQL Server 2005 sorgu bildirimlerini kullanarak.

Sorgu tabanlı bildirimi etkinleştirmenin en basit yolu, veri kaynağı nesnesinin **SqlCacheDependency** özniteliğini **CommandNotification'a** ayarlayarak ve **EnableCaching** özniteliğini **doğru**olarak ayarlayarak bunu bildirimsel olarak yapmaktır. Bu yöntemi kullanarak, hiçbir kod gereklidir. Veri kaynağına karşı yürütülen bir komutun sonucu değişirse, önbellek verilerini geçersiz klar.

Aşağıdaki örnek, SQL önbellek bağımlılığı için bir veri kaynağı denetimi yapılandırır:

[!code-aspx[Main](caching/samples/sample12.aspx)]

Bu durumda, **SelectCommand'da** belirtilen sorgu başlangıçtaolduğundan farklı bir sonuç döndürürse, önbelleğe alınmış sonuçlar geçersiz kılınur.

Ayrıca, **@ OutputCache** yönergesinin **SqlDependency** özniteliğini **CommandNotification'a**ayarlayarak tüm veri kaynaklarınızın SQL önbellek bağımlılıkları için etkinleştirilmesini de belirtebilirsiniz. Aşağıdaki örnekbunu göstermektedir.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005'teki sorgu bildirimleri hakkında daha fazla bilgi için SQL Server Books Online'a bakın.

Sorgu tabanlı SQL önbellek bağımlılığıyapılandırmanın başka bir yöntemi, bunu SqlCacheDependency sınıfını kullanarak programlı olarak yapmaktır. Aşağıdaki kod örneği bunun nasıl gerçekleştirilgösterdiğini göstermektedir.

[!code-csharp[Main](caching/samples/sample14.cs)]

Daha Fazla Bilgi:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Önbellek Sonrası Değiştirme

Bir sayfayı önbelleğe alma, bir Web uygulamasının performansını önemli ölçüde artırabilir. Ancak, bazı durumlarda önbelleğe alınması için sayfanın çoğunun ve sayfa içindeki bazı parçaların dinamik olması gerekir. Örneğin, belirli bir süre için tamamen durağan bir haber sayfası oluşturursanız, tüm sayfayı önbelleğe alınacak şekilde ayarlayabilirsiniz. Her sayfa isteğine değiştirilen dönen bir reklam başlığı eklemek istiyorsanız, sayfanın reklam içeren bölümünün dinamik olması gerekir. Bir sayfayı önbelleğe almak, ancak bazı içeriği dinamik olarak değiştirmek için önbellek sonrası ASP.NET kullanabilirsiniz. Önbellek sonrası ikame ile, tüm sayfa önbelleğe alma muaf olarak işaretlenmiş belirli parçalarla önbelleğe alınmış çıktıdır. Reklam afişleri örneğinde, AdRotator denetimi önbellek sonrası ikameden yararlanmanızı sağlar, böylece her kullanıcı ve her sayfa yenileme için dinamik olarak oluşturulan reklamlar oluşturulur.

Önbellek sonrası değiştirmeyi uygulamanın üç yolu vardır:

- Bildirimsel olarak, Ikame denetimini kullanarak.
- Programlı olarak, Değiştirme denetimi API'sini kullanarak.
- Dolaylı olarak, AdRotator denetimini kullanarak.

### <a name="substitution-control"></a>İkame Kontrolü

ASP.NET Değiştirme denetimi, önbelleğe alınmış bir sayfanın önbelleğe alınmış yerine dinamik olarak oluşturulan bir bölümünü belirtir. Dinamik içeriğin görünmesini istediğiniz sayfada konuma bir Değiştirme denetimi yersiniz. Çalışma zamanında, Değiştirme denetimi MethodName özelliğinde belirttiğiniz bir yöntemi çağırır. Yöntem, daha sonra Değiştirme denetiminin içeriğini değiştiren bir dize döndürmelidir. Yöntem, içeren Sayfa veya UserControl denetiminde statik bir yöntem olmalıdır. Değiştirme denetiminin kullanılması istemci tarafı önbelleğinin sunucu önbelleği olarak değiştirilmesine neden olur, böylece sayfa istemcide önbelleğe alınmaz. Bu, gelecekteki sayfa isteklerinin dinamik içerik oluşturmak için yöntemi yeniden aramasını sağlar.

### <a name="substitution-api"></a>İkame API

Önbelleğe alınmış bir sayfa için dinamik içerik oluşturmak için sayfa kodunuzdaki [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) yöntemini arayarak bir yöntemin adını parametre olarak geçirebilirsiniz. Dinamik içeriğin oluşturulmasını işleyen yöntem tek bir [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) parametresi alır ve bir dize döndürür. İade dizesi, verilen konumda değiştirilecek içeriktir. Yerine Alma denetimini bildirimle kullanmak yerine WriteSubstitution yöntemini çağırmanın bir avantajı, Sayfanın veya UserControl nesnesinin statik bir yöntemini aramak yerine herhangi bir rasgele nesnenin yöntemini arayabilirsiniz.

WriteSubstitution yöntemini çağırmak, istemci tarafı önbelleğinin sunucu önbelleği olarak değiştirilmesine neden olur, böylece sayfa istemcide önbelleğe alınmaz. Bu, gelecekteki sayfa isteklerinin dinamik içerik oluşturmak için yöntemi yeniden aramasını sağlar.

### <a name="adrotator-control"></a>AdRotator Kontrolü

AdRotator sunucu denetimi, önbellek sonrası değiştirme için dahili destek uygular. Sayfanıza bir AdRotator denetimi yerseniz, ana sayfanın önbelleğe alınmış olup olmadığına bakılmaksızın her istekte benzersiz reklamlar işler. Sonuç olarak, AdRotator denetimi içeren bir sayfa yalnızca sunucu tarafında önbelleğe alınır.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy Sınıfı

ControlCachePolicy sınıfı, kullanıcı denetimlerini kullanarak parça önbelleğe alma nın programlı denetimine olanak tanır. ASP.NET, kullanıcı denetimlerini [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) örneğine yerlebir eder. BasePartialCachingControl sınıfı, çıktı önbelleğe alma etkin olan bir kullanıcı denetimini temsil eder.

[Kısmi CachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) denetiminin [BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) özelliğine erişdiğinizde, her zaman geçerli bir ControlCachePolicy nesnesi alırsınız. Ancak, [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) denetiminin [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) özelliğine erişirseniz, yalnızca kullanıcı denetimi basePartialCachingControl denetimi tarafından zaten sarılmışsa geçerli bir ControlCachePolicy nesnesi alırsınız. Paketlenmemişse, özellik tarafından döndürülen ControlCachePolicy nesnesi, ilişkili bir BasePartialCachingControl'e sahip olmadığı için işlemeye çalıştığınızda özel durumlar oluşturur. UserControl örneğinin özel durumlar oluşturmadan önbelleğe alma özelliğini destekleyip desteklemediğini belirlemek [için, SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) özelliğini denetleyin.

ControlCachePolicy sınıfını kullanmak, çıktı önbelleğe almanızı etkinleştirmenin birkaç yollarından biridir. Aşağıdaki liste, çıktı önbelleğe etkinleştirmek için kullanabileceğiniz yöntemleri açıklar:

- Bildirimsenaryolarında çıktı önbelleğe alma sağlamak için [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) yönergesini kullanın.
- Bir kod arkası dosyasında kullanıcı denetimi için önbelleğe alma sağlamak için [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) özniteliğini kullanın.
- Önceki yöntemlerden birini kullanarak önbellek etkinleştirilmiş ve [System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) yöntemini kullanarak dinamik olarak yüklenen BasePartialCachingControl örnekleriyle çalıştığınız programlı senaryolarda önbellek ayarlarını belirtmek için ControlCachePolicy sınıfını kullanın.

ControlCachePolicy örneği, yalnızca denetim yaşam döngüsünün Init ve PreRender aşamaları arasında başarıyla değiştirilebilir. Bir ControlCachePolicy nesnesini PreRender aşamasından sonra değiştirirseniz, ASP.NET denetim yapıldıktan sonra yapılan değişiklikler önbellek ayarlarını gerçekten etkileyemediğinden (Render aşamasında bir denetim önbelleğe alınmış olduğundan) bir özel durum oluşturur. Son olarak, bir kullanıcı denetimi örneği (ve bu nedenle ControlCachePolicy nesnesi) yalnızca gerçekte işlendiğinde programlı işleme için kullanılabilir.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Önbelleğe Alma Yapılandırması'nda Değişiklikler - &lt;Önbelleğe Alma&gt; Öğesi

ASP.NET 2.0'da önbelleğe alma yapılandırmasında birkaç değişiklik vardır. &lt;Önbelleğe&gt; alma öğesi ASP.NET 2.0'da yenidir ve yapılandırma dosyasında önbelleğe alma yapılandırma değişiklikleri yapmanızı sağlar. Aşağıdaki öznitelikler kullanılabilir.

| **Öğe** | **Açıklama** |
| --- | --- |
| **Önbellek** | İsteğe bağlı öğe. Genel uygulama önbellek ayarlarını tanımlar. |
| **Outputcache** | İsteğe bağlı öğe. Uygulama genelinde çıktı önbellek ayarlarını belirtir. |
| **Outputcachesettings** | İsteğe bağlı öğe. Uygulamadaki sayfalara uygulanabilecek çıktı önbellek ayarlarını belirtir. |
| **Sqlcachedependency** | İsteğe bağlı öğe. ASP.NET bir uygulama için SQL önbellek bağımlılıklarını yapılandırır. |

### <a name="the-ltcachegt-element"></a>Önbellek &lt;&gt; Öğesi

Aşağıdaki öznitelikler önbellek &lt;&gt; öğesinde kullanılabilir:

| **Öznitelik** | **Açıklama** |
| --- | --- |
| **devre dışı, MemoryCollection** | İsteğe bağlı **Boolean** özniteliği. Makine bellek baskısı altındayken oluşan önbellek bellek koleksiyonunun devre dışı bırakıldığını belirten bir değer alır veya ayarlar. |
| **devre dışı son kullanma** | İsteğe bağlı **Boolean** özniteliği. Önbellek sona erdirme devre dışı bırakıldığını gösteren bir değer alır veya ayarlar. Devre dışı bırakıldığında, önbelleğe alınmış öğelerin süresi dolmaz ve süresi dolmuş önbellek öğelerinin arka plan atma işlemi gerçekleşmez. |
| **privateBytesLimit** | İsteğe bağlı **Int64** özniteliği. Önbellek süresi dolmuş öğeleri yıkamaya ve belleği geri almaya başlamadan önce bir uygulamanın özel baytlarının en büyük boyutunu gösteren bir değer alır veya ayarlar. Bu sınır, önbellek tarafından kullanılan bellek ve çalışan uygulamadan normal bellek ek yükü içerir. Sıfır ayarı, ASP.NET belleği geri almaya ne zaman başlayacağını belirlemek için kendi buluşsal larını kullanacağını gösterir. |
| **yüzdePhysicalMemoryUsedLimit** | İsteğe bağlı **Int32** özniteliği. Önbellek süresi dolmuş öğeleri yıkamaya başlamadan önce bir uygulama tarafından tüketilebilen bir makinenin fiziksel belleğinin maksimum yüzdesini gösteren bir değer alır veya ayarlar Bu bellek kullanımı hem önbellek tarafından kullanılan belleği hem de çalışan uygulamanın normal bellek kullanımını içerir. Sıfır ayarı, ASP.NET belleği geri almaya ne zaman başlayacağını belirlemek için kendi buluşsal larını kullanacağını gösterir. |
| **özelBytesPollTime** | İsteğe bağlı **TimeSpan** özniteliği. Uygulamanın özel bayt bellek kullanımı için yoklama arasındaki zaman aralığını gösteren bir değer alır veya ayarlar. |

### <a name="the-ltoutputcachegt-element"></a>&lt;OutputÖnbellek&gt; Öğesi

&lt;OutputCache&gt; öğesi için aşağıdaki öznitelikler kullanılabilir.

|       <strong>Öznitelik</strong>        |                                                                                                                                                                                                                                                       <strong>Açıklama</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>etkinleştirinOutputÖnbellek</strong>    |                                                                                                                                                          İsteğe bağlı <strong>Boolean</strong> özniteliği. Sayfa çıktı önbelleğini etkinleştirer/devre dışı bırakmaz. Devre dışı bırakılırsa, programatik veya bildirimsel ayarlardan bağımsız olarak hiçbir sayfa önbelleğe alınır. Varsayılan değer <strong>doğrudur.</strong>                                                                                                                                                           |
|  <strong>etkinleştirmeFragmentCache</strong>   |                                                İsteğe bağlı <strong>Boolean</strong> özniteliği. Uygulama parçası önbelleğini etkinleştirer/devre dışı katır. Devre dışı bırakılırsa, [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) yönergesi veya kullanılan önbelleğe alma profiline bakılmaksızın hiçbir sayfa önbelleğe alınır. Yukarı akışlı proxy sunucuları ve tarayıcı istemcilerinin sayfa çıktısını önbelleğe almaya çalışmaması gerektiğini belirten bir önbellek denetimi üstbilgisi içerir. Varsayılan değer <strong>yanlıştır.</strong>                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      İsteğe bağlı <strong>Boolean</strong> özniteliği. <strong>Önbellek denetimi:özel</strong> üstbilginin varsayılan olarak çıktı önbelleği modülü tarafından gönderilip gönderilmediğini belirten bir değer alır veya ayarlar. Varsayılan değer <strong>yanlıştır.</strong>                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | İsteğe bağlı <strong>Boolean</strong> özniteliği. Yanıtta bir Http "<strong>Vary: \</strong>" <em>üstbilgisini göndermeyi etkinleştirer/devre dışı kılabilir. Varsayılan false ayarı ile ,</em>bir \*" *Vary: <strong>" üstbilgi önbelleğe alınmış sayfalar için gönderilir. Vary üstbilgisi gönderildiğinde, Vary üstbilgisinde belirtilenlere göre farklı sürümlerin önbelleğe alınmasına olanak tanır. Örneğin, <em>Vary:User-Agents,</em> isteği veren kullanıcı aracısını temel alan bir sayfanın farklı sürümlerini saklar. Varsayılan değer **false'dur.</strong> |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;OutputCacheSettings&gt; Öğesi

&lt;OutputCacheSettings&gt; öğesi, daha önce açıklandığı gibi önbellek profillerioluşturulmasına olanak tanır. OutputCacheSettings &lt;&gt; öğesi için tek alt &lt;öğe önbellek&gt; profilleri yapılandırmak için outputCacheProfiles öğesidir.

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; Öğesi

&lt;SqlCacheDependency&gt; öğesi için aşağıdaki öznitelikler kullanılabilir.

| **Öznitelik** | **Açıklama** |
| --- | --- |
| **Etkin** | Gerekli **Boolean** özniteliği. Değişikliklerin yoklanıp yoklanmadığını gösterir. |
| **yokzaman** | İsteğe bağlı **Int32** özniteliği. SqlCacheDependency'nin veritabanı tablosunu değişiklikler için yoklama sıklığını ayarlar. Bu değer, ardışık yoklamalar arasındaki milisaniye sayısına karşılık gelir. 500 milisaniyeden az olarak ayarlanamaz. Varsayılan değer 1 dakikadır. |

### <a name="more-information"></a>Daha Fazla Bilgi

Önbellek yapılandırması ile ilgili olarak dikkat edilmesi gereken bazı ek bilgiler vardır.

- Alt işlem özel bayt sınırı ayarlanmazsa, önbellek aşağıdaki sınırlardan birini kullanır: 

    - x86 2GB: 800MB veya fiziksel RAM% 60, hangisi daha az
    - x86 3GB: 1800MB veya fiziksel RAM% 60, hangisi daha az
    - x64: 1 terabayt veya fiziksel RAM%60, hangisi daha az
- Hem alt işlem özel bayt &lt;sınırı ve önbellek privateBytesLimit/&gt; ayarlanırsa, önbellek iki en az kullanır.
- Tıpkı 1.x'te olduğu gibi, önbellek girişlerini bırakın ve GC'yi çağırıyoruz. İki nedenden dolayı toplayın: 

    - Özel bayt limitine çok yakınız.
    - Kullanılabilir bellek %10'a yakın veya daha az
- Önbellek yüzdesini Fiziksel MemoryUseLimit/ &lt;&gt; 100'e ayarlayarak, düşük kullanılabilir bellek koşulları için kırpma ve önbelleği etkin bir şekilde devre dışı kullanabilirsiniz.
- 1.x'in aksine, 2.0 kırpma askıya alacak ve son GC ise aramaları toplayacak. Collect, özel baytları veya yönetilen yığınların boyutunu (önbellek) bellek sınırının %1'inden fazla azaltmadı.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: Özel Önbellek Bağımlılıkları

1. Yeni bir Web sitesi oluşturun.
2. cache.xml adlı yeni bir XML dosyası ekleyin ve Web uygulamasının köküne kaydedin.
3. Default.aspx'in\_arkasındaki kodda Sayfa Yükü yöntemine aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Kaynak görünümünde default.aspx üst aşağıdakileri ekleyin: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Varsayılan.aspx'e göz atın. Zaman ne diyor?
6. Tarayıcıyı yenileyin. Zaman ne diyor?
7. cache.xml'i açın ve aşağıdaki kodu ekleyin: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. cache.xml kaydedin.
9. Tarayıcınızı yenileyin. Zaman ne diyor?
10. Önceden önbelleğe alınmış değerleri görüntülemek yerine neden güncelleştirilen zamanı açıklayın:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Laboratuvar 2: Yoklama Tabanlı Önbellek Bağımlılıklarını Kullanma

Bu laboratuvar, önceki modülde oluşturduğunuz projeyi kullanır ve GridView ve DetailsView denetimi aracılığıyla Northwind veritabanındaki verilerin düzenlenmesine olanak tanır.

1. Visual Studio 2005'te projeyi açın.
2. Veritabanı nı ve\_Ürünler tablosunu etkinleştirmek için aspnet regsql yardımcı programını Northwind veritabanına karşı çalıştırın. Visual Studio Komut İstemi'nden aşağıdaki komutu kullanın: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. web.config dosyanıza aşağıdakileri ekleyin: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. showdata.aspx adlı yeni bir web formu ekleyin.
5. Showdata.aspx sayfasına aşağıdaki @ outputcache yönergesini ekleyin: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. showdata.aspx'in Sayfa\_Yüküne aşağıdaki kodu ekleyin: 

    [!code-html[Main](caching/samples/sample21.html)]
7. Showdata.aspx için yeni bir SqlDataSource denetimi ekleyin ve Northwind veritabanı bağlantısını kullanacak şekilde yapılandırın. İleri'ye tıklayın.
8. Ürün Adı ve Ürün Kimliği onay kutularını seçin ve İleri'yi tıklatın.
9. Son'a tıklayın.
10. showdata.aspx sayfasına yeni bir GridView ekleyin.
11. Açılan açılır yerden SqlDataSource1'i seçin.
12. Showdata.aspx'i kaydedin ve göz atın. Görüntülenen zamana dikkat edin.
