---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Yapılandırma ve Enstrümantasyon | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET 2.0'da yapılandırma ve enstrümantasyonda büyük değişiklikler vardır. Yeni ASP.NET yapılandırma API yapılandırma değişiklikleri pr yapılmasını sağlar ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543060"
---
# <a name="configuration-and-instrumentation"></a>Yapılandırma ve İzleme

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2.0'da yapılandırma ve enstrümantasyonda büyük değişiklikler vardır. Yeni ASP.NET yapılandırma API'si, yapılandırma değişikliklerinin programlı olarak yapılmasına olanak tanır. Buna ek olarak, birçok yeni yapılandırma ayarları yeni yapılandırmalar ve enstrümantasyon için izin var.

ASP.NET 2.0'da yapılandırma ve enstrümantasyonda büyük değişiklikler vardır. Yeni ASP.NET yapılandırma API'si, yapılandırma değişikliklerinin programlı olarak yapılmasına olanak tanır. Buna ek olarak, birçok yeni yapılandırma ayarları yeni yapılandırmalar ve enstrümantasyon için izin var.

Bu modülde, yapılandırma api'sinin ASP.NET, ASP.NET yapılandırma dosyalarına okuma ve yazma ile ilgili olduğu gibi, ASP.NET enstrümantasyonunu da ele alacağız. Ayrıca ASP.NET izleme mevcut yeni özellikleri ele alacaktır.

## <a name="aspnet-configuration-api"></a>ASP.NET Yapılandırma API'si

ASP.NET yapılandırma API'si, tek bir programlama arabirimi kullanarak uygulama yapılandırma verilerini geliştirmenize, dağıtmanıza ve yönetmenize olanak tanır. Yapılandırma dosyalarında XML'yi doğrudan düzenlemeden tam ASP.NET yapılandırmalarını programlamak üzere geliştirmek ve değiştirmek için yapılandırma API'sini kullanabilirsiniz. Ayrıca, konsol uygulamalarında ve geliştirdiğiniz komut dosyalarında, Web tabanlı yönetim araçlarında ve Microsoft Yönetim Konsolu 'nda (MMC) anlık uygulamalarda yapılandırma API'sini kullanabilirsiniz.

Aşağıdaki iki yapılandırma yönetimi aracı yapılandırma API'sini kullanır ve .NET Framework sürüm 2.0'a dahildir:

- Yönetim görevlerini basitleştirmek için yapılandırma API'sini kullanan ASP.NET MMC snap-in, yapılandırma hiyerarşisinin tüm düzeylerinden yerel yapılandırma verilerinin tümleşik görünümünü sağlar.
- Barındırılan siteler de dahil olmak üzere yerel ve uzak uygulamaların yapılandırma ayarlarını yönetmeniz için web sitesi yönetim aracı.

yapılandırma API'ASP.NET, Web sitelerini ve uygulamaları programlı olarak yapılandırmak için kullanabileceğiniz bir ASP.NET yönetim nesnesi kümesini içerir. Yönetim nesneleri .NET Framework sınıf kitaplığı olarak uygulanır. Yapılandırma API programlama modeli, derleme zamanında veri türlerini zorlayarak kod tutarlılığı ve güvenilirliğini sağlamaya yardımcı olur. Uygulama yapılandırmalarını yönetmeyi kolaylaştırmak için yapılandırma API'si, verileri farklı yapılandırma dosyalarından ayrı koleksiyonlar olarak görüntülemek yerine yapılandırma hiyerarşisindeki tüm noktalardan birleştirilen verileri tek bir koleksiyon olarak görüntülemenize olanak tanır. Ayrıca, yapılandırma API doğrudan yapılandırma dosyalarında XML düzenlemeden tüm uygulama yapılandırmaları işlemek için olanak sağlar. Son olarak, API, Web Sitesi Yönetim Aracı gibi yönetim araçlarını destekleyerek yapılandırma görevlerini basitleştirir. Yapılandırma API'si, bilgisayarda yapılandırma dosyaları oluşturulmasını destekleyerek ve yapılandırma komut dosyalarını birden çok bilgisayarda çalıştırarak dağıtımı kolaylaştırır.

> [!NOTE]
> Yapılandırma API'si IIS uygulamalarının oluşturulmasını desteklemez.

## <a name="working-with-local-and-remote-configuration-settings"></a>Yerel ve Uzak Yapılandırma Ayarları yla Çalışma

Yapılandırma nesnesi, bilgisayar gibi belirli bir fiziksel varlık veya uygulama veya Web sitesi gibi mantıksal bir varlık için uygulanan yapılandırma ayarlarının birleştirilmiş görünümünü temsil eder. Belirtilen mantıksal varlık yerel bilgisayarda veya uzak bir sunucuda bulunabilir. Belirli bir varlık için yapılandırma dosyası yoksa, Yapılandırma nesnesi Machine.config dosyası tarafından tanımlanan varsayılan yapılandırma ayarlarını temsil eder.

Aşağıdaki sınıflardan açık yapılandırma yöntemlerinden birini kullanarak yapılandırma nesnesi alabilirsiniz:

1. Kuruluşunuz bir istemci uygulamasıysa ConfigurationManager sınıfı.
2. Kuruluşunuz bir Web uygulamasıysa, WebConfigurationManager sınıfı.

Bu yöntemler, temel yapılandırma dosyalarını işlemek için gerekli yöntemleri ve özellikleri sağlayan bir Yapılandırma nesnesi döndürecektir. Okumak veya yazmak için bu dosyalara erişebilirsiniz.

### <a name="reading"></a>Okuma

Yapılandırma bilgilerini okumak için GetSection veya GetSectionGroup yöntemini kullanırsınız. Okuyan kullanıcı veya işlem, hiyerarşideki tüm yapılandırma dosyalarında Okuma İzinlerine sahip olmalıdır.

> [!NOTE]
> Yol parametresi alan statik bir GetSection yöntemi kullanıyorsanız, yol parametresi kodun çalıştırıldığı uygulamaya başvurmalıdır. Aksi takdirde, parametre yoksayılır ve şu anda çalışan uygulamanın yapılandırma bilgileri döndürülür.

### <a name="writing"></a>Yazma

Yapılandırma bilgilerini yazmak için Kaydet yöntemlerinden birini kullanırsınız. Yazan kullanıcı veya işlem, geçerli yapılandırma hiyerarşisi düzeyinde yapılandırma dosyası ve dizin üzerinde Yazma izinleri ve hiyerarşideki tüm yapılandırma dosyalarının okuma izinlerine sahip olmalıdır.

Belirli bir varlığın devralınan yapılandırma ayarlarını temsil eden bir yapılandırma dosyası oluşturmak için aşağıdaki kaydet yapılandırma yöntemlerinden birini kullanın:

1. Yeni bir yapılandırma dosyası oluşturmak için Kaydet yöntemi.
2. Başka bir konumda yeni bir yapılandırma dosyası oluşturmak için SaveAs yöntemi.

## <a name="configuration-classes-and-namespaces"></a>Yapılandırma Sınıfları ve İsim Alanları

Birçok yapılandırma sınıfları ve yöntemleri birbirine benzer. Aşağıdaki tabloda en sık kullanılan yapılandırma sınıfları ve ad alanları açıklanmaktadır.

| **Yapılandırma sınıfı veya ad alanı** | **Açıklama** |
| --- | --- |
| [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) ad alanı | Tüm .NET Framework uygulamaları için ana yapılandırma sınıflarını içerir. Bölüm işleyicisınıfları, GetSection ve GetSectionGroup gibi yöntemlerden bir bölümün yapılandırma verilerini elde etmek için kullanılır. Bu iki yöntem statik değildir. |
| System.Configuration.Configuration sınıfı | Bilgisayar, uygulama, Web dizini veya başka bir kaynak için yapılandırma verileri kümesini temsil eder. Bu sınıf, yapılandırma ayarlarını güncelleştirmek ve bölümlere ve bölüm gruplarına başvurular almak için GetSection ve GetSectionGroup gibi yararlı yöntemler içerir. Bu sınıf, WebConfigurationManager ve ConfigurationManager sınıflarının yöntemleri gibi tasarım zamanı yapılandırma verilerini elde eden yöntemler için bir iade türü olarak kullanılır. |
| System.Web.Configuration ad alanı | [ASP.NET Yapılandırma Ayarları'nda](https://msdn.microsoft.com/library/b5ysx397.aspx)tanımlanan ASP.NET yapılandırma bölümleri için bölüm işleyicisınıflarını içerir. Bölüm işleyicisınıfları, GetSection ve GetSectionGroup gibi yöntemlerden bir bölümün yapılandırma verilerini elde etmek için kullanılır. |
| System.Web.Configuration.WebConfigurationManager sınıfı | Çalışma zamanı ve tasarım zamanı yapılandırma ayarlarına başvurular almak için yararlı yöntemler sağlar. Bu yöntemler, return türü olarak System.Configuration.Configuration sınıfını kullanır. Bu sınıfın statik GetSection yöntemini veya System.Configuration.ConfigurationManager sınıfının statik olmayan GetSection yöntemini birbirinin yerine kullanabilirsiniz. Web uygulama yapılandırmaları için System.Configuration.ConfigurationManager sınıfı, System.Configuration.ConfigurationManager sınıfı yerine önerilir. |
| [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) ad alanı | Yapılandırma sağlayıcısını özelleştirmek ve genişletmek için bir yol sağlar. Bu, yapılandırma sistemindeki tüm sağlayıcı sınıfları için taban sınıftır. |
| [System.Web.Management](https://msdn.microsoft.com/library/system.web.management.aspx) ad alanı | Web uygulamalarının sistem durumunu yönetmek ve izlemek için sınıflar ve arabirimler içerir. Açıkçası, bu ad alanı yapılandırma API'sinin bir parçası olarak kabul edilmez. Örneğin, izleme ve olay ateş bu ad alanındaki sınıflar tarafından gerçekleştirilir. |
| [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) isim alanı | Uygulamaların, windows yönetim araçları (WMI) aracılığıyla yönetim bilgilerini ve olaylarını potansiyel tüketicilere ifşa etmesi için gerekli sınıfları sağlar. ASP.NET sağlık izleme olayları sunmak için WMI kullanır. Açıkçası, bu ad alanı yapılandırma API'sinin bir parçası olarak kabul edilmez. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET Yapılandırma Dosyalarından Okuma

WebConfigurationManager sınıfı, yapılandırma dosyalarını ASP.NET okumanın temel sınıfıdır. Yapılandırma dosyalarını okumak için temelde üç adım vardır ASP.NET:

1. OpenWebConfiguration yöntemini kullanarak bir Yapılandırma nesnesi alın.
2. Yapılandırma dosyasında istenilen bölüme başvuru alın.
3. Yapılandırma dosyasından istenen bilgileri okuyun.

Yapılandırma nesnesinin temsili belirli bir yapılandırma dosyasını temsil etmez. Bunun yerine, bir bilgisayarın, uygulamanın veya Web sitesinin yapılandırmasının birleştirilmiş görünümünü temsil eder. Aşağıdaki kod örneği, *ProductInfo*adlı bir Web uygulamasının yapılandırmasını temsil eden bir Yapılandırma nesnesini anında bir araya sağlar.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> /ProductInfo yolu yoksa, yukarıdaki kodun machine.config dosyasında belirtildiği gibi varsayılan yapılandırmayı döndüreceğini unutmayın.

Yapılandırma nesnesine sahip olduktan sonra, yapılandırma ayarlarını delmek için GetSection veya GetSectionGroup yöntemini kullanabilirsiniz. Aşağıdaki örnek, yukarıdaki ProductInfo uygulaması için kimliğe bürünme ayarlarına bir başvuru alır:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET Yapılandırma Dosyalarına Yazma

Yapılandırma dosyalarından okumada olduğu gibi, WebConfigurationManager sınıfı yapılandırma dosyalarına yazmanın Asp.NET için temeldir. Yapılandırma dosyalarına yazmanın üç adımı da vardır ASP.NET.

1. OpenWebConfiguration yöntemini kullanarak bir Yapılandırma nesnesi alın.
2. Yapılandırma dosyasında istenilen bölüme başvuru alın.
3. Kaydet veya Kaydet yöntemini kullanarak yapılandırma dosyasından istenen bilgileri yazın.

Aşağıdaki kod, derleme&gt; öğesinin hata &lt; **ayıklama** özniteliğini false olarak değiştirir:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Bu kod yürütüldüğünde,&gt; derleme öğesinin &lt;hata **ayıklama** özniteliği *webApp* uygulamasının web.config dosyası için false olarak ayarlanır.

## <a name="systemwebmanagement-namespace"></a>System.Web.Management İsim Alanı

System.Web.Management ad alanı, ASP.NET uygulamalarının durumunu yönetmek ve izlemek için sınıflar ve arayüzler sağlar.

Günlüğe kaydetme, olayları bir sağlayıcıyla ilişkilendiren bir kural tanımlayarak gerçekleştirilir. Kural, sağlayıcıya gönderilen olayların türünü tanımlar. Aşağıdaki temel olaylar oturum açmanız için kullanılabilir:

| **WebBaseEvent** | Tüm etkinlikler için taban olay sınıfı. Olay kodu, olay ayrıntı kodu, olayın yükseltildiği tarih ve saat, sıra numarası, olay iletisi ve olay ayrıntıları gibi tüm olaylar için gerekli özellikleri içerir. |
| --- | --- |
| **Webmanagementevent** | Uygulama ömrü, istek, hata ve denetim olayları gibi yönetim olayları için temel olay sınıfı. |
| **WebHeartbeatEvent** | Yararlı çalışma zamanı durum bilgilerini yakalamak için uygulama tarafından düzenli aralıklarla oluşturulan olay. |
| **Webauditevent** | Yetkilendirme hatası, şifre çözme hatası vb. durumları işaretlemek için kullanılan güvenlik denetim olayları için taban *sınıf.* |
| **WebRequestEvent** | Tüm bilgilendirme isteği etkinlikleri için taban sınıf. |
| **Webbaseerrorevent** | Hata koşullarını gösteren tüm olaylar için taban sınıf. |

Kullanılabilir sağlayıcı türleri olay çıktısını Event Viewer, SQL Server, Windows Management Instrumentation (WMI) ve e-postaadresine göndermenize olanak tanır. Önceden yapılandırılmış sağlayıcılar ve olay eşlemeleri, olay çıktısının günlüğe kaydedilmesi için gereken çalışma miktarını azaltır.

ASP.NET 2.0, etkinlik giriş ve durdurma etkinliklerini günlüğe kaydetmek ve işlenmemiş özel durumları günlüğe kaydetmek için Olay Günlüğü sağlayıcısını kutunun dışında kullanır. Bu, bazı temel senaryoları kapsamanıza yardımcı olur. Örneğin, uygulamanızın bir özel durum attığını, ancak kullanıcının hatayı kaydetmediğini ve yeniden oluşturamayacağınızı varsayalım. Varsayılan Olay Günlüğü kuralıyla, ne tür bir hata oluştuğu hakkında daha iyi bir fikir edinmek için özel durum ve yığın bilgilerini toplayabilirsiniz. Uygulamanız oturum durumunu kaybediyorsa, başka bir örnek de geçerlidir. Bu durumda, uygulama etki alanının geri dönüşüm olup olmadığını ve uygulama etki alanının neden durdurulduğunu belirlemek için Olay Günlüğü'ne bakabilirsiniz.

Ayrıca, sağlık izleme sistemi genişletilebilir. Örneğin, özel Web olayları tanımlayabilir, bunları uygulamanızda ateşleyebilir ve ardından olay bilgilerini e-posta nız gibi bir sağlayıcıya göndermek için bir kural tanımlayabilirsiniz. Bu, enstrümantasyonunuzu sağlık izleme sağlayıcılarına kolayca bağlamanızı sağlar. Başka bir örnek olarak, bir sipariş her işlenir ve her olay SQL Server veritabanına gönderen bir kural kurmak bir olay yangın olabilir. Ayrıca, bir kullanıcı art arda birden çok kez oturum açamayınca ve olayı e-posta tabanlı sağlayıcıları kullanacak şekilde ayarladığında da bir olayı ateşleyebilirsiniz.

Varsayılan sağlayıcılar ve olaylar için yapılandırma, genel Web.config dosyasında depolanır. Global Web.config dosyası, Machine.config dosyasında depolanan tüm Web tabanlı ayarları ASP.NET 1x olarak depolar. Global Web.config dosyası aşağıdaki dizinde bulunur:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

Genel &lt;Web.config dosyasının healthMonitoring&gt; bölümü varsayılan yapılandırma ayarları sağlar. Bu ayarı geçersiz kılabilir veya uygulamanız için &lt;Web.config dosyasındaki sağlık Denetimi&gt; bölümünü uygulayarak kendi ayarlarınızı yapılandırabilirsiniz.

Genel &lt;Web.config dosyasının healthMonitoring&gt; bölümü aşağıdaki öğeleri içerir:

| **Sağlayıcı** | Olay Görüntüleyicisi, WMI ve SQL Server için ayarlanan sağlayıcıları içerir. |
| --- | --- |
| **Eventmappings** | Çeşitli WebBase sınıfları için eşlemeler içerir. Kendi etkinlik sınıfınızı oluşturursanız bu listeyi genişletebilirsiniz. Kendi etkinlik sınıfınızı oluşturmak, bilgi gönderdiğiniz sağlayıcılar üzerinde daha ayrıntılı bilgi sağlar. Örneğin, kendi özel etkinliklerinizi e-postaya gönderirken, işlenmemiş özel durumları SQL Server'a gönderilmek üzere yapılandırabilirsiniz. |
| **Kural -ları** | Olay Haritalama'yı sağlayıcıya bağlar. |
| **Tamponlama** | Olayları sağlayıcıya ne sıklıkta temize çıkarılabildiğini belirlemek için SQL Server ve e-posta sağlayıcılarıyla birlikte kullanılır. |

Aşağıda global Web.config dosyasından bir kod örneği verilmiştir.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>Etkinlikleri Olay Görüntüleyicisi'nde depolama

Daha önce de belirtildiği gibi, Olay Görüntüleyicisi'ndeki olayları günlüğe kaydetme sağlayıcısı, global Web.config dosyasında sizin için yapılandırılır. Varsayılan olarak, **WebBaseErrorEvent** ve **WebFailureAuditEvent'e** dayalı tüm olaylar günlüğe kaydedilir. Olay Günlüğü'ne ek bilgileri günlüğe kaydetmek için ek kurallar ekleyebilirsiniz. Örneğin, tüm olayları *(yani* **WebBaseEvent'e**dayalı her olay) günlüğe kaydetmek istiyorsanız, Web.config dosyanıza aşağıdaki kuralı ekleyebilirsiniz:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Bu kural, **Tüm Olaylar** olay haritasını Olay Günlüğü sağlayıcısına bağlar. Hem olayMapping hem de sağlayıcı global Web.config dosyasına dahildir.

## <a name="how-to-store-events-to-sql-server"></a>Olayları SQL Server'da depolama

Bu yöntem, Aspnet\_regsql.exe aracı tarafından oluşturulan **ASPNETDB** veritabanını kullanır. Varsayılan sağlayıcı, Uygulama\_veri klasöründe dosya tabanlı bir veritabanı veya SQL Server'ın yerel SQLExpress örneğini kullanan LocalSqlServer bağlantı dizesini kullanır. Hem LocalSqlServer bağlantı dizesi hem de SqlProvider global Web.config dosyasında yapılandırılır.

Global Web.config dosyasındaki LocalSqlServer bağlantı dizesi aşağıdaki gibi görünür:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Başka bir SQL Server örneği kullanmak istiyorsanız, %windir%\Microsoft.Net\Framework\v2.0'da bulunan Aspnet\_regsql.exe aracını kullanmanız gerekir. \* klasörü. SQL Server örneğinde özel bir\_ **ASPNETDB** veritabanı oluşturmak için Aspnet regsql.exe aracını kullanın, ardından uygulama yapılandırma dosyanıza bağlantı dizesi ekleyin ve ardından yeni bağlantı dizesini kullanarak bir sağlayıcı ekleyin. **ASPNETDB** veritabanını oluşturduktan sonra, bir eventMapping'i sqlProvider'a bağlamak için bir kural belirlemeniz gerekir.

Varsayılan SqlProvider'ı kullanın veya kendi sağlayıcınızı yapılandırın, sağlayıcıyı bir olay haritasına bağlayan bir kural eklemeniz gerekir. Aşağıdaki kural, yukarıda oluşturduğunuz yeni sağlayıcıyı **Tüm Etkinlikler** etkinlik haritasına bağlar. Bu kural, Tüm olayları **WebBaseEvent'e** göre kaydeder ve MYASPNETDB bağlantı dizesini kullanacak MySqlWebEventProvider'a gönderir. Aşağıdaki kod, sağlayıcıyı bir olay haritasına bağlamak için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Yalnızca SQL Server'a hata göndermek istiyorsanız, aşağıdaki kuralı ekleyebilirsiniz:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Olayları WMI'ye iletme

Ayrıca olayları WMI'ye iletebilirsiniz. WMI sağlayıcısı varsayılan olarak global Web.config dosyasında sizin için yapılandırılır.

Aşağıdaki kod örneği, olayları WMI'ye iletmek için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Sağlayıcıya bir olayMapping ilişkilendirmek için bir kural eklemek gerekir, ve aynı zamanda olayları dinlemek için bir WMI dinleyici uygulaması. Aşağıdaki kod örneği, WMI sağlayıcısını Tüm **Etkinlikler** olay haritasına bağlamak için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>Olayları e-postaya iletme

Ayrıca olayları e-postaya da iletebilirsiniz. İstemeden kendinize SQL Server veya Olay Günlüğü için daha uygun olabilecek birçok bilgi gönderebileceğinizden, hangi etkinlik kurallarını e-posta sağlayıcınıza eşlediğiniz konusunda dikkatli olun. İki e-posta sağlayıcısı vardır; SimpleMailWebEventProvider ve TemplatedMailWebEventProvider. Her biri, her ikisi de yalnızca TemplatedMailWebEventProvider'da bulunan "şablon" ve "ayrıntılı TemplateErrors" öznitelikleri dışında aynı yapılandırma özniteliklerine sahiptir.

> [!NOTE]
> Bu e-posta sağlayıcılarının hiçbiri sizin için yapılandırılmamıştır. Bunları Web.config dosyanıza eklemeniz gerekir.

Bu iki e-posta sağlayıcısı arasındaki temel fark, SimpleMailWebEventProvider değiştirilemez genel bir şablon içinde e-postalar gönderir. Örnek Web.config dosyası, aşağıdaki kuralı kullanarak bu e-posta sağlayıcısını yapılandırılan sağlayıcılar listesine ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

E-posta sağlayıcısını **Tüm Etkinlikler** etkinlik haritasına bağlamak için aşağıdaki kural da eklenir:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 İzleme

ASP.NET 2.0'da izlemenin üç önemli geliştirmesi vardır.

1. Tümleşik izleme işlevi
2. İzleme iletilerine programlı erişim
3. Geliştirilmiş uygulama düzeyi izleme

## <a name="integrated-tracing-functionality"></a>Entegre İzleme İşlevselliği

Artık System.Diagnostics.Trace sınıfı tarafından yayılan iletileri, çıktıyı izleme ASP.NET yönlendirebilir ve ASP.NET izleme yle yayılan iletileri System.Diagnostics.Trace'e yönlendirebilirsiniz. Ayrıca ASP.NET enstrümantasyon olaylarını System.Diagnostics.Trace'e iletebilirsiniz. Bu &lt;işlevsellik, izleme&gt; öğesinin yeni **writeToDiagnosticsTrace** özniteliği tarafından sağlanır. Bu Boolean değeri doğru olduğunda, ASP.NET İzleme iletileri Trace iletilerini görüntülemek için kayıtlı olan tüm dinleyiciler tarafından kullanılmak üzere altyapı izleme altyapısısystem.Diagnostics izleme için iletilir.

## <a name="programmatic-access-to-trace-messages"></a>İz Mesajlarına Programlı Erişim

ASP.NET 2.0, **TraceContextRecord** sınıfı ve **TraceRecords** koleksiyonu aracılığıyla tüm izleme iletilerine programlı erişim sağlar. İzleme iletilerine erişmenin en etkili yolu, yeni **TraceFinished** olayını işlemek için bir **TraceContextEventHandler** temsilcisini (ASP.NET 2,0'da da yeni) kaydetmektir. Daha sonra izleme iletilerini istediğiniz gibi iletebilirsiniz.

Aşağıdaki kod örneği bunu göstermektedir:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

Yukarıdaki örnekte, TraceRecords koleksiyonunu döngüye sokup her iletiyi Yanıt akışına yazıyorum.

## <a name="improved-application-level-tracing"></a>Geliştirilmiş Uygulama Düzeyi İzleme

Uygulama düzeyi &lt;izleme, izleme&gt; öğesinin yeni en **Son** özniteliğinin getirilmesiyle geliştirilir. Bu öznitelik, en son uygulama düzeyinde izleme çıktısının görüntülenip görüntülenmediğini ve requestLimit tarafından belirtilen sınırların ötesindeki eski izleme verilerinin atılıp atılmadığını belirtir. Yanlışsa, istekLimit özniteliğine ulaşılıncaya kadar istekler için izleme verileri görüntülenir.

## <a name="aspnet-command-line-tools"></a>ASP.NET Komut Satırı Araçları

ASP.NET yapılandırmasına yardımcı olmak için çeşitli komut satırı araçları vardır. ASP.NET geliştiriciler aspnet\_regiis.exe aracı aşina olmalıdır. ASP.NET 2.0 yapılandırmaya yardımcı olmak için diğer üç komut satırı araçları sağlar.

Aşağıdaki komut satırı araçları kullanılabilir:

| **Araç** | **Kullanma** |
| --- | --- |
| **aspnet\_regiis.exe** | iIS ile ASP.NET kaydı için izin verir. Bu araçların 2,0 ASP.NET ile, biri 32 bit sistemler (Framework klasöründe) ve diğeri 64 bit sistemler (Framework64 klasöründe) ile birlikte iki sürümü vardır. 64 bit sürüm 32 bit işletim sistemi üzerinde yüklenmez. |
| **aspnet\_regsql.exe** | ASP.NET SQL Server Registration aracı, ASP.NET'daki SQL Server sağlayıcıları tarafından kullanılmak üzere bir Microsoft SQL Server veritabanı oluşturmak veya varolan bir veritabanından seçenek eklemek veya kaldırmak için kullanılır. Aspnet\_regsql.exe dosyası Web sunucunuzdaki [drive:]\WINDOWS\Microsoft.NET\Framework\versionNumber klasöründe bulunur. |
| **aspnet\_regbrowsers.exe** | tarayıcı kaydı ASP.NET aracı, sistem genelindeki tüm tarayıcı tanımlarını bir derlemeye ayrıştırır ve derler ve derlemeyi genel derleme önbelleğine yükler. Araç tarayıcı tanımı dosyalarını kullanır (. BROWSER dosyaları) .NET Framework Browsers alt dizininden. Araç %SystemRoot%\Microsoft.NET\Framework\version\ dizininde bulunabilir. |
| **aspnet\_derleyici.exe** | ASP.NET Derleme aracı, bir ASP.NET Web uygulamasını yerinde veya üretim sunucusu gibi bir hedef konuma dağıtım için derlemenize olanak tanır. Uygulama derlenirken son kullanıcılar uygulamaya ilk istekte bir gecikmeyle karşılaşmadığından, yerinde derleme uygulama performansına yardımcı olur. |

Aspnet\_regiis.exe aracı 2.0 ASP.NET yeni olmadığından, burada tartışmayacağız.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server Kayıt Aracı\_- aspnet regsql.exe

SQL Server Registration aracını kullanarak ASP.NET seçenek türünü ayarlayabilirsiniz. Bir SQL bağlantısı belirtebilir, bilgileri yönetmek için hangi ASP.NET uygulama hizmetlerinin SQL Server'ı kullandığını belirtebilir, SQL önbellek bağımlılığı için hangi veritabanının veya tablonun kullanıldığını belirtebilir ve yordamları ve oturum durumunu depolamak için SQL Server'ı kullanmak için destek ekleyebilir veya kaldırabilirsiniz.

Birkaç ASP.NET uygulama hizmeti, verileri bir veri kaynağından depolamayı ve almayı yönetmek için bir sağlayıcıya güvenir. Her sağlayıcı veri kaynağına özgüdür. ASP.NET aşağıdaki ASP.NET özellikleri için bir SQL Server sağlayıcısı içerir:

- Üyelik [(SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) sınıfı).
- Rol Yönetimi [(SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) sınıfı).
- Profil [(SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) sınıfı).
- Web Parçaları Kişiselleştirme [(SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) sınıfı).
- Web Olayları [(SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) sınıfı).

ASP.NET yüklediğinizde, sunucunuz için Machine.config dosyası, sağlayıcıya dayanan ASP.NET özelliklerin her biri için SQL Server sağlayıcılarını belirten yapılandırma öğeleri içerir. Bu sağlayıcılar varsayılan olarak SQL Server Express 2005'in yerel bir kullanıcı örneğine bağlanmak üzere yapılandırılır. Sağlayıcılar tarafından kullanılan varsayılan bağlantı dizesini değiştirirseniz, makine yapılandırmasında yapılandırılan ASP.NET özelliklerden herhangi birini kullanamadan önce, Aspnet\_regsql.exe'yi kullanarak seçtiğiniz özellik için SQL Server veritabanını ve veritabanı öğelerini yüklemeniz gerekir. SQL kayıt aracıyla belirttiğiniz veritabanı zaten yoksa (komut satırında belirtilmemişse aspnetdb varsayılan veritabanı olacaktır), geçerli kullanıcının SQL Server'da veritabanları oluşturma ve veritabanı içinde şema öğeleri oluşturma hakkına sahip olması gerekir.

### <a name="sql-cache-dependency"></a>SQL Önbellek Bağımlılığı

ASP.NET çıktı önbelleği gelişmiş bir özelliği SQL önbellek bağımlılığıdır. SQL önbellek bağımlılığı iki farklı işlem modlarını destekler: biri tablo yoklama ASP.NET uygulamasını ve SQL Server 2005'in sorgu bildirim özelliklerini kullanan ikinci bir mod. SQL kayıt aracı, tablo yoklama işlemini yapılandırmak için kullanılabilir.

### <a name="session-state"></a>Oturum Durumu

Varsayılan olarak, oturum durum değerleri ve bilgileri ASP.NET işlemi içinde bellekte depolanır. Alternatif olarak, oturum verilerini birden çok Web sunucusu tarafından paylaşılabilen bir SQL Server veritabanında depolayabilirsiniz. SQL kayıt aracıyla oturum durumu için belirttiğiniz veritabanı zaten yoksa, geçerli kullanıcının SQL Server'da veritabanları oluşturma nın yanı sıra veritabanı içinde şema öğeleri oluşturma hakkına sahip olması gerekir. Veritabanı varsa, geçerli kullanıcı varolan veritabanında şema öğeleri oluşturmak için haklara sahip olmalıdır.

Oturum durum veritabanını SQL Server'a yüklemek\_için Aspnet regsql.exe aracını çalıştırın ve aşağıdaki bilgileri komutla birlikte veriniz:

- **-S** seçeneğini kullanarak SQL Server örneğinin adı.
- SQL Server çalıştıran bir bilgisayarda veritabanı oluşturma izni olan bir hesabın oturum açma kimlik bilgileri. Şu anda oturum açmış olan kullanıcıyı kullanmak için **-E** seçeneğini kullanın veya parola belirtmek için **-P** seçeneğiyle birlikte bir kullanıcı kimliği belirtmek için **-U** seçeneğini kullanın.
- Oturum durum veritabanını eklemek için **-ssadd** komut satırı seçeneği.

Varsayılan olarak, SQL Server 2005 Express Edition çalıştıran bir bilgisayara oturum durum veritabanını yüklemek için Aspnet\_regsql.exe aracını kullanamazsınız.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET Tarayıcı Kayıt Aracı -\_aspnet regbrowsers.exe

ASP.NET sürüm 1.1'de, Machine.config dosyası &lt;browserCaps&gt;adında bir bölüm içeriyordu. Bu bölümde, normal bir ifadeye dayalı olarak çeşitli tarayıcılar için yapılandırmaları tanımlayan bir dizi XML girişi yer almaktadır. ASP.NET sürüm 2.0 için, yeni bir . BROWSER dosyası, XML girişlerini kullanarak belirli bir tarayıcının parametrelerini tanımlar. Yeni bir tarayıcı ekleyerek yeni bir tarayıcı hakkında bilgi eklersiniz. Browser dosyası sisteminizde %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers adresinde bulunan klasöre.

Bir uygulama tarayıcı bilgileri gerektirdiği her zaman bir .config dosyaokuma olmadığından, yeni bir . BROWSER dosya ve montaj\_için gerekli değişiklikleri eklemek için Aspnet regbrowsers.exe çalıştırın. Bu, sunucunun yeni tarayıcı bilgilerine hemen erişmesine olanak tanır, böylece bilgileri almak için uygulamalarınızın hiçbirini kapatmanız gerekmez. Bir uygulama, tarayıcı özelliklerine geçerli HttpRequest'in Tarayıcı özelliği üzerinden erişebilir.

Aspnet\_regbrowser.exe çalışırken aşağıdaki seçenekler mevcuttur:

| **Seçeneği** | **Açıklama** |
| --- | --- |
| **-?** | Komut penceresinde Aspnet\_regbbrowsers.exe Yardım metnini görüntüler. |
| **-i** | Çalışma zamanı tarayıcı özelliklerini derlemeyi oluşturur ve genel derleme önbelleğine yükler. |
| **-u** | Genel derleme önbelleğinden çalışma zamanı tarayıcı özellikleri derlemesini kaldırır. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>derleme ASP.NET - aspnet\_compiler.exe

ASP.NET Derleme aracı iki genel şekilde kullanılabilir: hedef çıktı dizininin belirtildiği dağıtım için yerinde derleme ve derleme için.

### <a name="compiling-an-application-in-place"></a>[Uygulamayı Yerinde Derleme](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET Derleme aracı bir uygulamayı yerinde derleyebilir, yani uygulamaya birden fazla istekte bulunma davranışını taklit eder ve böylece düzenli derlemeye neden olur. Önceden derlenmiş bir sitenin kullanıcıları, sayfanın ilk istek üzerine derlenmesine bağlı bir gecikme yaşamayacaktır.

Bir siteyi yerinde derlediğinizde, aşağıdaki öğeler geçerlidir:

- Site, dosyalarını ve dizin yapısını korur.
- Sunucuda site tarafından kullanılan tüm programlama dilleri için derleyiciler olmalıdır.
- Herhangi bir dosya derlemede başarısız olursa, tüm site derlemede başarısız olur.

Ayrıca, yeni kaynak dosyaları ekledikten sonra uygulamayı yerinde yeniden derleyebilirsiniz. Araç, **-c** seçeneğini eklemediğiniz sürece yalnızca yeni veya değiştirilmiş dosyaları derler.

> [!NOTE]
> İç içe geçmiş bir uygulama içeren bir uygulamanın derlemesi iç içe geçmiş uygulamayı derlemez. İç içe geçmiş uygulama ayrı olarak derlenmelidir.

### <a name="compiling-an-application-for-deployment"></a>[Dağıtım için Bir Uygulama Derleme](https://msdn.microsoft.com/library/ms229863.aspx)

HedefDir parametresini belirterek dağıtım için bir uygulama (hedef konuma derleme) derlersiniz. HedefDir Web uygulaması için son konum olabilir veya derlenen uygulama daha da dağıtılabilir. **-u** seçeneğini kullanmak, uygulamayı derlenen uygulamadaki belirli dosyalarda yeniden derlemeden değişiklik yapabilecek şekilde derler. Aspnet\_compiler.exe statik ve dinamik dosya türleri arasında bir ayrım yapar ve ortaya çıkan uygulamayı oluştururken bunları farklı işler.

- Statik dosya türleri, .css, .gif, .htm, .html, .jpg, .js gibi uzantıları olan dosyalar gibi ilişkili bir derleyicisi veya yapı sağlayıcısı olmayan lardır. Bu dosyalar yalnızca hedef konuma kopyalanır ve dizin yapısındaki göreli yerleri korunur.
- Dinamik dosya türleri, .asax, .ascx, .ashx, .aspx, .browser, .master gibi ASP.NET özel dosya adı uzantılarına sahip dosyalar da dahil olmak üzere ilişkili bir derleyiciye veya yapı sağlayıcısına sahip olanlardır. ASP.NET Derleme aracı bu dosyalardan derlemeler oluşturur. **-u** seçeneği atlanırsa, araç dosya adı uzantısı ile de dosyalar oluşturur. Özgün kaynak dosyaları kendi derlemesine eşleyen DERLENDİ. Uygulama kaynağının dizin yapısının korunduğundan emin olmak için, araç hedef uygulamada ilgili konumlarda yer tutucu dosyaları oluşturur.

Derlenen uygulamanın içeriğinin değiştirilebilenbir şey olduğunu belirtmek için **-u** seçeneğini kullanmanız gerekir. Aksi takdirde, sonraki değişiklikler yoksayılmak veya çalışma zamanı hatalarına neden olur.

Aşağıdaki tabloda, **-u** seçeneği eklendiğinde ASP.NET Derleme aracının farklı dosya türlerini nasıl işlediği açıklanmaktadır.

| **Dosya türü** | **Derleyici eylemi** |
| --- | --- |
| .ascx, .aspx, .master | Bu dosyalar biçimlendirme ve kaynak koduna ayrılır, bu kod arkası dosyaları ve &lt;komut dosyası runat="sunucu"&gt; öğelerine dahil olan tüm kodları içerir. Kaynak kodu, karma algoritmasından türetilen adlarla derlemeler halinde derlenir ve derlemeler Bin dizinine yerleştirilir. Herhangi bir satır kodu, yani, kod ** &lt; ** ** % ** ve parantez arasında kapalı, biçimlendirme ile birlikte ve derlenmez. Kaynak dosyalarıyla aynı ada sahip yeni dosyalar biçimlendirmeyi içerecek şekilde oluşturulur ve ilgili çıktı dizinlerine yerleştirilir. |
| .ashx, .asmx | Bu dosyalar derlenmez ve derlenmemiş çıktı dizinlerine taşınır. İşleyici kodunun derlenmiş olmasını istiyorsanız, kodu Uygulama\_Kodu dizinindeki kaynak kod dosyalarına yerleştirin. |
| .cs, .vb, .jsl, .cpp (daha önce listelenen dosya türleri için kod arkası dosyaları dahil değildir) | Bu dosyalar derlenir ve bunlara başvuran derlemelerde kaynak olarak eklenmiştir. Kaynak dosyaları çıktı dizinine kopyalanmaz. Bir kod dosyası başvurulmuyorsa, derlenmez. |
| Özel dosya türleri | Bu dosyalar derlenmez. Bu dosyalar ilgili çıktı dizinlerine kopyalanır. |
| Uygulama\_Kodu alt dizinindeki kaynak kod dosyaları | Bu dosyalar derlemeler halinde derlenir ve Bin dizinine yerleştirilir. |
| .resx ve .kaynak dosyaları\_App GlobalResources alt dizini | Bu dosyalar derlemeler halinde derlenir ve Bin dizinine yerleştirilir. Ana\_çıktı dizini altında App GlobalResources alt dizini oluşturulmaz ve kaynak dizinde bulunan .resx veya .resources dosyaları çıktı dizinlerine kopyalanır. |
| .resx ve .kaynak dosyaları\_App LocalResources alt dizininde | Bu dosyalar derlenmez ve ilgili çıktı dizinlerine kopyalanır. |
| .Uygulama\_Temaları alt dizinindeki cilt dosyaları | .skin dosyaları ve statik tema dosyaları derlenmez ve ilgili çıktı dizinlerine kopyalanır. |
| .browser Web.config Statik dosya türleri Derlemeler zaten Bin dizini mevcut | Bu dosyalar çıktı dizinlerine olduğu gibi kopyalanır. |

Aşağıdaki tabloda, **-u** seçeneği atlandığında ASP.NET Derleme aracının farklı dosya türlerini nasıl işlediği açıklanmaktadır.

| **Dosya türü** | **Derleyici eylemi** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Bu dosyalar biçimlendirme ve kaynak koduna ayrılır, bu kod arkası dosyaları ve &lt;komut dosyası runat="sunucu"&gt; öğelerine dahil olan tüm kodları içerir. Kaynak kodu, karma algoritmasından türetilen adlarla derlemeler halinde derlenir. Elde edilen derlemeler Bin dizinine yerleştirilir. Herhangi bir satır kodu, yani, kod ** &lt; ** ** % ** ve parantez arasında kapalı, biçimlendirme ile birlikte ve derlenmez. Derleyici, kaynak dosyalarla aynı ada sahip biçimlendirmeyi içerecek yeni dosyalar oluşturur. Bu ortaya çıkan dosyalar Bin dizinine yerleştirilir. Derleyici ayrıca kaynak dosyaları yla aynı ada sahip ancak uzantılı dosyalar oluşturur. Eşleme bilgileri içeren DERLENDİ. Şey. DERLENEN dosyalar, kaynak dosyaların özgün konumuna karşılık gelen çıktı dizinlerine yerleştirilir. |
| Ascx | Bu dosyalar biçimlendirme ve kaynak koduna ayrılır. Kaynak kodu derlemeler halinde derlenir ve karma algoritmasından türetilen adlarla Bin dizinine yerleştirilir. Biçimlendirme dosyaları oluşturulmama. |
| .cs, .vb, .jsl, .cpp (daha önce listelenen dosya türleri için kod arkası dosyaları dahil değildir) | .ascx, .ashx veya .aspx dosyalarından oluşturulan derlemeler tarafından başvurulan kaynak kodu derlemeler halinde derlenir ve Bin dizinine yerleştirilir. Kaynak dosyaları kopyalanır. |
| Özel dosya türleri | Bu dosyalar dinamik dosyalar gibi derlenir. Bağımlı oldukları dosyatürüne bağlı olarak, derleyici çıktı dizinlerine eşleme dosyaları yerleyebilir. |
| Uygulama\_Kodu alt dizinindeki dosyalar | Bu alt dizindeki kaynak kod dosyaları derlemeler halinde derlenir ve Bin dizinine yerleştirilir. |
| App\_GlobalResources alt dizinindeki dosyalar | Bu dosyalar derlemeler halinde derlenir ve Bin dizinine yerleştirilir. Ana\_çıktı dizini altında App GlobalResources alt dizini oluşturulmaz. Yapılandırma dosyasında To="Tümü" yazıyorsa, .resx ve .resources dosyaları çıktı dizinlerine kopyalanır. [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)tarafından başvurulmuyorsa kopyalanmaz. |
| .resx ve .kaynak dosyaları\_App LocalResources alt dizininde | Bu dosyalar benzersiz adlara sahip derlemeler halinde derlenir ve Bin dizinine yerleştirilir. Hiçbir .resx veya .kaynak dosyaları çıktı dizinlerine kopyalanır. |
| .Uygulama\_Temaları alt dizinindeki cilt dosyaları | Temalar derlemeler halinde derlenir ve Bin dizinine yerleştirilir. Saplama dosyaları .skin dosyaları için oluşturulur ve ilgili çıktı dizinine yerleştirilir. Statik dosyalar (.css gibi) çıktı dizinlerine kopyalanır. |
| .browser Web.config Statik dosya türleri Derlemeler zaten Bin dizini mevcut | Bu dosyalar çıktı dizinine olduğu gibi kopyalanır. |

### <a name="fixed-assembly-names"></a>[Sabit Montaj Adları](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Yükleyici'yi kullanarak bir Web uygulamasını dağıtma gibi bazı senaryolar, güncelleştirmeler için derlemeleri veya yapılandırma ayarlarını tanımlamak için tutarlı dosya adları ve içeriklerinin yanı sıra tutarlı dizin yapıları kullanımını gerektirir. Bu gibi durumlarda, ASP.NET Derleme aracının birden çok sayfanın derlemeler halinde derlendiği yeri kullanmak yerine her kaynak dosya için bir derleme derlemesi gerektiğini belirtmek için **-sabit adlar** seçeneğini kullanabilirsiniz. Bu çok sayıda derlemeye yol açabilir, bu nedenle ölçeklenebilirlikle ilgileniyorsanız bu seçeneği dikkatli kullanmalısınız.

### <a name="strong-name-compilation"></a>[Güçlü İsim Derlemesi](https://msdn.microsoft.com/library/ms229863.aspx##)

**-aptca**, **-delaysign**, **-keycontainer** ve **-keyfile** seçenekleri, Güçlü\_Ad [Aracı (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) ayrı ayrı kullanmadan güçlü adlandırılmış derlemeler oluşturmak için Aspnet compiler.exe kullanabilirsiniz sağlanır. Bu seçenekler, sırasıyla, **AllowPartiallyTrustedCallersAttribute**, **AssemblyDelaySignAttribute**, **AssemblyKeyNameAttribute**ve **AssemblyKeyFileAttribute**karşılık gelir.

Bu özniteliklerin tartışılması bu dersin kapsamı dışındadır.

## <a name="labs"></a>Labs

Aşağıdaki laboratuvarların her biri önceki laboratuvarlar üzerinde inşa edin. Sırayla yapmanız gerekir.

## <a name="lab-1-using-the-configuration-api"></a>Laboratuvar 1: Yapılandırma API'sini kullanma

1. *Mod9lab*adında yeni bir Web sitesi oluşturun.
2. Siteye yeni bir Web Yapılandırma Dosyası ekleyin.
3. web.config dosyasına aşağıdakileri ekleyin:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Bu, web.config dosyasındaki değişiklikleri kaydetme iznine sahip olmasını sağlar.

1. Default.aspx'e yeni bir Etiket denetimi ekleyin ve kimliği **lblDebugStatus**olarak değiştirin.
2. Varsayılan.aspx'e yeni bir Düğme denetimi ekleyin.
3. Düğme denetiminin kimliğini **btnToggleDebug** ve Metin hata **ayıklama durumunu geçişyapmak**için değiştirin.
4. Default.aspx'in kod arkası dosyası için Kod Görünümü'nu açın ve **System.Web.Configuration** için aşağıdaki gibi **bir kullanma** deyimi ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Sınıfa iki özel değişken ve\_aşağıda gösterildiği gibi bir Sayfa Init yöntemi ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Sayfa\_Yükü'ne aşağıdaki kodu ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Varsayılan.aspx'i kaydedin ve göz atın. Etiket denetiminin geçerli hata ayıklama durumunu gösterdiğine dikkat edin.
2. Tasarımcıdaki Düğme denetimine çift tıklayın ve Düğme denetimi için Click etkinliğine aşağıdaki kodu ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Varsayılan.aspx'i kaydedin ve göz atın ve düğmeye tıklayın.
2. Her düğmeyi tıklattıktan sonra web.config dosyasını açın &lt;ve&gt; derleme bölümünde **hata ayıklama** özniteliğini gözlemleyin.

## <a name="lab-2-logging-application-restarts"></a>Laboratuvar 2: Günlük Uygulaması Yeniden Başlatılır

Bu laboratuvarda, Olay Görüntüleyicisi'nde uygulama kapatmalarının, başlangıçların ve yeniden derlemelerin günlüğe kaydedilmesini sağlayan kod oluşturursunuz.

1. Default.aspx'e bir DropDownList ekleyin ve kimliği ddlLogAppEvents olarak değiştirin.
2. DropDownList için **AutoPostBack** özelliğini **doğru**olarak ayarlayın.
3. DropDownList için Öğeler koleksiyonuna üç öğe ekleyin. İlk öğe için **Metin** *Seç Değeri* ve -1 değerini yapın. İkinci öğenin **Metnini** ve **Değerini** **Doğru,** üçüncü öğenin **Metin** ve **Değerini** **Yanlış**yapın.
4. Default.aspx'e yeni bir Etiket ekleyin. Kimliği **lblLogAppEvents olarak değiştirin.**
5. Default.aspx için kod arkası görünümünü açın ve aşağıda gösterildiği gibi HealthMonitoringSection türünden bir değişken için yeni bir bildirim ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Sayfa\_Init'teki varolan koda aşağıdaki kodu ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList'e çift tıklayın ve SelectedIndexChanged etkinliğine aşağıdaki kodu ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default.aspx'e göz atın.
2. Açılır düşüşü **False**olarak ayarlayın.
3. Olay Görüntüleyici'ndeki Uygulama günlüğünü temizleyin.
4. Uygulama için Hata Ayıklama özniteliğini değiştirmek için düğmeyi tıklatın.
5. Olay Görüntüleyicisi'ndeki Uygulama günlüğünü yenileyin. 

    1. Herhangi bir olay kaydedildi mi?
    2. Neden ya da neden olmasın?
6. Okulu **True'ya ayarlayın.**
7. Uygulama için Hata Ayıklama özniteliğini geçiş yapmak için düğmeyi tıklatın.
8. Etkinlik Görüntüleyicisi'nde Uygulama oturumaçını yenileyin. 

    1. Herhangi bir olay kaydedildi mi?
    2. Uygulamanın kapanmasının nedeni neydi?
9. Günlüğü açıp kapatmayı deneyin ve web.config dosyasında yapılan değişikliklere bakın.

## <a name="more-information"></a>Daha Fazla Bilgi:

ASP.NET 2.0'ın Sağlayıcı modeli, yalnızca uygulama enstrümantasyonu için değil, Üyelik, Profiller, vb. gibi diğer birçok kullanım için de kendi sağlayıcılarınızı oluşturmanıza olanak tanır. Uygulama olaylarını bir metin dosyasına günlüğe kaydetmek için özel bir sağlayıcı yazma hakkında ayrıntılı bilgi için bu bağlantıyı ziyaret [edin.](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)
