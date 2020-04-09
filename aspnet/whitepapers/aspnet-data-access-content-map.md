---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET Veri Erişimi - Önerilen Kaynaklar | Microsoft Dokümanlar
author: rick-anderson
description: Bu konu, öncelikle Entity Framework ve SQL Se kullanarak, ASP.NET web uygulamalarında verilere nasıl erişilenhakkında dokümantasyon kaynaklarına bağlantılar sağlar...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676169"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET Veri Erişimi - Önerilen Kaynaklar

> Bu konu, öncelikle Entity Framework ve SQL Server'ı kullanarak ASP.NET web uygulamalarındaki verilere nasıl erişilenle ilgili dokümantasyon kaynaklarına bağlantılar sağlar.
> 
> Eğer büyük bir blog yazısı, [stackoverflow](http://stackoverflow.com) iş parçacığı, ya da yararlı olacak başka bir bağlantı biliyorsanız, bize bağlantı ile [bir e-posta gönderin.](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)
> 
> Son güncelleme: 03.03.2014

Konu aşağıdaki bölümleri içerir:

- [ASP.NET'da Veri Erişimine Başlarken](#gettingstarted)
- [Varlık Çerçevesini Kullanma](#ef)

    - [Önce Varlık Çerçeve Kodunu Kullanma](#cf)
    - [Varlık Çerçeve Kodu İlk Geçişleri Kullanma](#efcfmigrations)
    - [Önce Varlık Çerçeve Veritabanını veya Önce Modeli Kullanma (EF Tasarımcısı)](#efdbf)
    - [Varlık Çerçevesinde İlgili Verilerin Yüklenmesi (Tembel Yükleme, Istekli Yükleme ve Açık Yükleme)](#efrelateddata)
    - [Varlık Çerçeve Performansını Optimize Etme](#optimizingef)
    - [Varlık Çerçeve Uygulamasında Eşzamanlılık İşleme](#efconcurrency)
    - [Varlık Çerçevesi ile ilgili kitaplar](#efbooks)
    - [Ek Varlık Çerçevesi kaynakları](#otherefresources)
- [ASP.NET Web Formlarında Veri Bağlama Uygulamaları](#wfdatabinding)

    - [Web Formları Model Bağlama kullanma](#wfmodelbinding)
    - [Web Formlarını Kullanma Veri Kaynağı Denetimleri](#wfdsc)
    - [Web Formlarını Veriye Bağlı Denetimleri ve Veri Bağlama İfadelerini Kullanma](#wfdbc)
- [SQL Server Veritabanları ile Çalışma](#sqlserver)

    - [SQL Server Express LocalDB Veritabanları ile Çalışma](#sslocaldb)
    - [SQL Server Express Veritabanları ile Çalışma](#sse)
    - [Windows Azure SQL Veritabanı ile çalışma](#ssdb)
    - [SQL Server ve Windows Azure SQL Veritabanı arasında seçim](#ssdbchoosing)
- [NoSQL Veritabanı Yönetim Sistemleri ile Çalışma](#nosql)
- [ASP.NET Uygulamalarında LINQ sorgularını kullanma](#linq)
- [Dinamik Veri İskelesi kullanma](#dd)
- [Veri Erişimini Güvence Altına Alma](#securing)
- [Veri Erişim Performansını Optimize Etme](#optimizingdataaccess)
- [Veritabanı dağıtma](#deploying)
- [Web Hizmeti Aracılığıyla Verilere Erişim](#webservice)
- [Ek Kaynaklar](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET'da Veri Erişimine Başlarken

- [Veri Depolama Seçenekleri (Windows Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Bulut için geliştirme hakkında bir e-kitap Bölüm. İlişkisel veritabanlarına aşina birçok geliştiricinin göz ardı etme eğiliminde olduğu bir alternatif olarak NoSQL veritabanlarını tanır. İlişkisel veya NoSQL seçerken veya belirli bir platformu seçerken nelere dikkat etmen gerektiğini zekler sunar.
- [ASP.NET Veri Erişim Seçenekleri](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). ASP.NET için ilişkisel veritabanları için veri erişim seçeneklerine giriş ve senaryonuziçin uygun olan platformların ve erişim yöntemlerinin nasıl seçilen hakkında rehberlik.
- [İlişkisel veritabanı](http://en.wikipedia.org/wiki/Relational_database). Vikipedi). İlişkisel veritabanlarıyla çalışmadıysanız, ilişkisel veritabanı terminolojisi ve kavramlarına giriş için bu sayfaya bakın. Özellikle SQL Server'a giriş için daha sonra bu konuda [SQL Server veritabanları ile çalışma](#sqlserver) bölümüne bakın.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Varlık Çerçevesini Kullanma

- [Varlık Çerçeve Geliştirme Yaklaşımları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Önce Önce Örnek Veya Kod İlk Veritabanı'nı nasıl seçeceğiniz hakkında kılavuz.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Önce Varlık Çerçeve Kodunu Kullanma

Aşağıdaki öğreticiler indirilebilir örnek uygulamalar sunuyoruz:

- [MVC 5 kullanarak EF 6 ile başlarken.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Geçişler ve bağlantı esnekliği, komut durdurma ve async gibi EF 6 özellikleri de dahil olmak üzere çok çeşitli Varlık Çerçeve Kodu İlk senaryoları kapsar. Bu [EF 5 / MVC 4 serisinin](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)güncelleştirilmiş bir sürümüdür. Önceki seri, yeni seride yer almayan depo ve çalışma birimi desenleri hakkında bir öğretici içerir.
- [MVC 5 ASP.NET Giriş](../mvc/overview/getting-started/introduction/getting-started.md). Varlık Çerçeve Kodu İlk senaryoları daha dar bir aralığı kapsar ama MVC özellikleri tanıtan daha kapsamlı bir iş yok.
- [Model Bağlama ve Web Formları](https://go.microsoft.com/fwlink/?LinkId=286117). Web Formları uygulamasında Önce Kod Kullanır.
- [4.5 Web Formlarını ASP.NET Başlarken](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Önce Kod'un bazı kapsama alanı olan Web Formlarına giriş. Model Bağlama kullanır.
- [MVC Müzik Mağazası](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Üyelik ve yetkilendirme yi de uygulayan bir e-ticaret MVC 3 uygulamasında Önce Kod Kullanır. Burada kullanılan MVC sürümü ve ASP.NET üyelik (kimlik doğrulama ve yetkilendirme) sistemi güncel liğini yitirir; ASP.NET üyeliği hakkında daha güncel bilgiler için [https://asp.net/identity](https://asp.net/identity)bkz.

Diğer kaynaklar:

- [Varlık Çerçevesi - Varolan Veritabanına Önce Kod](https://msdn.microsoft.com/data/jj200620). Msdn. Code First'in varolan bir veritabanıyla nasıl kullanılacağını gösteren video ve gözden geçirme.
- [Veri Geliştirici Merkezi - Entity Framework](https://msdn.microsoft.com/data/ef). Msdn. Varlık Çerçevesi ekibi tarafından oluşturulan ve tutulan Entity Framework belgeleri kılavuzu için [Başlat bağlantısını](https://msdn.microsoft.com/data/ee712907) görün.

Bu [konunun](#efbooks) ilerleyen saatlerinde Varlık Çerçevesi ve [Ek Varlık Çerçeve Kaynakları](#otherefresources) hakkında kitaplara da bakınız.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Varlık Çerçeve Kodu İlk Geçişleri Kullanma

Yukarıda listelenen Code First öğreticilerinin çoğu geçişleri kapsar. Ayrıca aşağıdaki kaynaklara bakın.

- [Visual Studio kullanarak web dağıtım ASP.NET.](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md) Bir veritabanı dağıtmak için Kod İlk Geçişler nasıl kullanılacağını gösteren 2 bölümlü öğretici serisi.
- [Üyelik, OAuth ve SQL Veritabanı ile Güvenli ASP.NET MVC 5 uygulamasını Windows Azure Web Sitesine dağıtın.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) Microsoft Azure). Üyelik ve uygulama verilerini Azure'a dağıtmak için geçişler nasıl kullanılır?
- [Görsel Stüdyo ve ASP.NET için Web DağıtımA Genel Bakış.](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) Kod İlk Geçişler Visual Studio web dağıtım özelliklerine nasıl entegre olduğunu açıklayan bir açıklama için **Visual Studio'da Veritabanı Dağıtımını Yapılandırma** bölümüne bakın.
- [Veri Geliştirici Merkezi - İlk Geçişleri Kodla](https://msdn.microsoft.com/data/jj591621) (MSDN). Varlık Çerçeve ekibinin Geçişbelgeleri.
- [Göçler Screencast Serisi](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF günlüğü). Kod İlk Geçişler gelişmiş konular hakkında üç video.
- [Kod Web Sayfaları Siteleri ASP.NET ile İlk Geçişler](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Mikesdotnetting blog). Veri bağlamını Visual Studio sınıf kitaplığı projesine koyarak kod ilk geçişleri ASP.NET bir Web Sayfaları sitesiyle nasıl kullanılacağını gösterir.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Önce Varlık Çerçeve Veritabanını veya Önce Modeli Kullanma (EF Tasarımcısı)

- [Varlık Framework 6 Veritabanı Ile Başlarken İlk MVC 5 kullanarak](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Veritabanı oluşturmak için Server Explorer'da bir komut dosyası çalıştırın ve ardından veri modelini oluşturmak için Entity Framework tasarımcısını kullanın. Basit CRUD web sayfalarının nasıl oluşturulabileceğini gösterir ve diğer veri işleme işlevleri için tüm EF iş akışları aynı DbContext API'yi kullandığından Önce Kod öğreticilerinden birini izleyebilirsiniz.

Aşağıdaki kaynaklar daha eskidir. Varlık Çerçevesi'nin sürüm 4.0'ını kullanmak istiyorsanız ve Bir Web Forms uygulamasında veri bağlama için veri kaynağı denetimi kullanmak istiyorsanız bunlar yararlıdır.

- [Varlık Çerçevesi 4.0 ile Başlarken](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). **EntityDataSource** denetiminin nasıl kullanılacağını gösterir.
- [Varlık Çerçevesi ile devam](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) **(ObjectDataSource** Denetiminin nasıl kullanılacağını gösterir. Eşzamanlılık işleme hakkında bir öğretici, EF performansı hakkında bir öğretici ve EF 4.0'daki yenilikler le ilgili bir öğretici içerir.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Varlık Çerçevesinde ilgili verilerin işlenmesi (Tembel Yükleme, Istekli Yükleme ve Açık Yükleme)

- [ASP.NET Bir MVC Uygulamasında Varlık Çerçevesi ile İlgili Verileri Okuma](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Kod İlk, MVC örnek uygulama. Gösterilen yöntemler, Web Forms modeli bağlama ve Veritabanı İlk iş akışı için de geçerlidir.
- [Veri Geliştirici Merkezi - İlgili Varlıkların Yüklenmesi](https://msdn.microsoft.com/data/jj574232) (MSDN). Varlık Çerçevesi ekibinin ilgili verilerin yüklenmesiyle ilgili belgeleri.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Varlık Çerçevesi performansını optimize etme

- [ASP.NET Uygulaması için Gelişmiş Varlık Çerçeve Senaryoları.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md) Kendi SQL deyimlerinizi nasıl çalıştıreceğiniz veya kendi depolanan yordamlarınızı nasıl çağırılacak, değişiklik algılamasını nasıl devre dışı kaltın ve değişiklikleri kaydederken doğrulamayı nasıl devre dışı kaltın gerektiğini gösterir.
- [Varlık Çerçevesi 5](https://msdn.microsoft.com/data/hh949853) (MSDN) için Performans Hususları.
- [Performans Değerlendirmeleri (Varlık Çerçevesi)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [ASP.NET Bir Web Uygulamasında Varlık Çerçevesi ile Performansı En Üst Düzeye Çıkarma](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md). Varlık Çerçevesi 4.0 için geçerlidir.
- Ayrıca bu konunun ilerleyen saatlerinde [ASP.NET veri erişimini en iyi duruma etme](#optimizingdataaccess) konusuna bakın.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Varlık Çerçeve Uygulamasında Eşzamanlılık İşleme

- [ASP.NET Bir MVC Uygulamasında Varlık Çerçevesi ile Eşzamanlılık Taşıma](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Kod İlk, DbContext API, bir MVC örnek uygulama kullanarak.
- [Veri Geliştirici Merkezi – İyimser Eşzamanlılık Desenleri](https://msdn.microsoft.com/data/jj592904) (MSDN). Varlık Çerçevesi ekibinin eşzamanlılık belgeleri.
- [ASP.NET Bir Web Uygulamasında Varlık Çerçevesi ile Eşzamanlılık Taşıma](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Varlık Çerçevesi 4.0 için geçerlidir. Veritabanı İlk, ObjectContext API, bir Web Forms örnek uygulama kullanarak.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Varlık Çerçevesi ile ilgili kitaplar

- Programlama Varlık Çerçeve: Julie Lerman ve Rowan Miller tarafından [DbContext.](http://shop.oreilly.com/product/0636920022237.do)
- [Programlama Varlık Çerçeve: Kod İlk](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman ve Rowan Miller tarafından.

Bu kitapların her ikisi de güncel önerilen teknikler ile güncel. Varlık Çerçevesi'ne, Internet'te bulunan her şeyden daha kapsamlı ama takip edilebilen bir giriş sağlarlar. Başka bir kitap, Julie Lerman tarafından [Programlama Varlık Çerçeve,](http://shop.oreilly.com/product/9780596807252.do) daha büyük ve daha kapsamlı ama daha eski ve kapsadığı tekniklerin çoğu artık Varlık Çerçeve kullanmak için önerilen yol vardır. Ayrıca, MsDN sitesindeki [Veri Geliştirici Merkezi - Kitaplar'da](https://msdn.microsoft.com/data/aa937716) Entity Framework ekibi tarafından önerilen kitapların listesine bakın.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Diğer Varlık Çerçeve Kaynakları

- [Varlık Çerçevesi (ADO.NET) takım blogu.](https://blogs.msdn.com/b/adonet/) En güncel bilgiler ve yeni geliştirmeduyuruları için en iyi kaynaklardan biri. DIĞER EF ile ilgili bloglar için, [Varlık Çerçevesi ile Başlayın'daki](https://msdn.microsoft.com/data/ee712907)Blogroll'a bakın.
- [MSDN Dergisi](https://msdn.microsoft.com/magazine/default.aspx). Varlık Çerçevesi ile ilgili konularla ilgili sık sık bulunan **Veri Noktaları** sütununa bakın.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web Formlarında Veri Bağlama Uygulamaları

- [ASP.NET Web Formlar Veri Erişim](https://msdn.microsoft.com/library/jj822927.aspx) <a id="wfmodelbinding"></a>Seçenekleri (MSDN) .

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Web Formları Model Bağlama kullanma

- [Model Bağlama ve Web Formları](https://go.microsoft.com/fwlink/?LinkId=286117). Önce EF Code'u kullanarak öğretici seriler.
- [Web Formları Model Bağlama Bölüm 1: Veri seçimi](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie günlüğü). Bu eski blog gönderilerinde, şu anda ItemType olarak adlandırılan özellik ModelType olarak adlandırılmıştır, ancak aksi takdirde içerdikleri bilgiler geçerlidir.
- [Web Formları Model Bağlama Bölüm 2: Veri Filtreleme](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthrie günlüğü).
- [Web Formları Model Bağlama Bölüm 3: Güncelleme ve Doğrulama](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie günlüğü).
- [ASP.NET 4.5 Web Formları Model Bağlama](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (video).
- [Model Bağlama Bölüm 1 - Veri Seçimi](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (video).
- [Model Bağlama Bölüm 2 - Filtreleme](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (video).
- [4.5 Web Formlarını ASP.NET başlarken - Veri Öğelerini ve Ayrıntılarını Görüntüleyin.](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Web Formlarını Kullanma Veri Kaynağı Denetimleri

- [Veri Kaynağı Web Sunucusu Denetimleri](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- Dinamik Veri sağlayıcısının ve EntityFramework 6 (Microsoft Web Development blogu) [için EntityDataSource denetiminin yayımlanmasından duyuruyorum.](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Web Formlarını Veriye Bağlı Denetimleri ve Veri Bağlama İfadelerini Kullanma

- [Model Bağlama ve Web Formları](https://go.microsoft.com/fwlink/?LinkId=286117). Önce EF Kodu kullanan öğretici seriler.
- [4.5 Web Formlarını ASP.NET başlarken - Veri Öğelerini ve Ayrıntılarını Görüntüleyin.](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)
- [Güçlü Daktiledilen Veri Denetimleri](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie günlüğü).
- [Güçlü Bir Şekilde Yazılan Veri Denetimleri](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [ASP.NET 4.5 Web Güçlü Daktil Ile Veri Denetimleri](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video) oluşturur.
- [Veriye Bağlı Web Sunucusu Denetimleri](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Veri Bağlayıcı İfadelere Genel Bakış](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Bu sayfa sadece **Eval** ve **Bind**kapsar; **item** ve **BindItem'i**içerecek şekilde güncelleştirilemedi.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server Veritabanları ile Çalışma

- [SQL Server Veritabanı Özellikleri](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Çok çeşitli SQL Server konularına genel bir giriş için, TOC'da bunun altındaki girişlere bakın.
- [SQL Server Editions](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Kullanılabilir SQL Server sürümlerinin bir özeti, her biri hakkında daha fazla bilgi bağlantılar.)
- ASP.NET Web Uygulamaları (MSDN) [için SQL Server Bağlantı Dizeleri.](https://msdn.microsoft.com/library/jj653752.aspx)
- ASP.NET Web Uygulamaları (MSDN) [için SQL Server Compact'ı kullanma.](https://msdn.microsoft.com/library/ms247257.aspx)
- [Microsoft SQL Server: Veritabanı Ürün Örnekleri](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Örnek AdventureWorks veritabanları.
- [Örnek Veritabanlarıyükleme.](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md) Burada gösterilen yöntemlere ek olarak, örnek .mdf dosyalarından birini\_bir web projesinin Uygulama Veri klasörüne indirebilir, veritabanını LocalDB'ye dönüştürebilir ve bir LocalDB bağlantı dizesi oluşturabilirsiniz. Bunun nasıl yapılacağını öğrenmek için [bkz.](https://msdn.microsoft.com/library/hh873188.aspx)

Ayrıca SQL Server Express ve LocalDB ile çalışma ve SQL Server ve SQL Veritabanı arasında seçim yapmak la ilgili aşağıdaki bölümlere bakın.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL Server Express LocalDB Veritabanları ile Çalışma

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). LocalDB'ye resmi MSDN girişi.
- ASP.NET Web Uygulamaları (MSDN) [için SQL Server Bağlantı Dizeleri.](https://msdn.microsoft.com/library/jj653752.aspx)
- [Nasıl?](https://msdn.microsoft.com/library/hh873188.aspx) Bir .mdf dosyasının SQL Server Express'in önceki bir sürümünden LocalDB'a nasıl geçirilir? [Ayrıca SQL Server 2012 örnek veritabanlarından](https://go.microsoft.com/fwlink/?linkid=117483)birini indirirseniz bu işlemden geçmeniz gerekir.
- Geliştirilmiş bir SQL Express (SQL Server Express blogu) [LocalDB](https://go.microsoft.com/fwlink/?LinkId=234375) ile karşınızdadır. LocalDB'nin neden oluşturulduğuna ilişkin msdn'ye dahil edilenden daha fazla arka plana sahiptir.
- [LocalDB: Veritabanım nerede?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express blog). LocalDB veritabanı dosyalarının nerede oluşturulduğu hakkında bilgi.
- [Tam IIS, Bölüm 1: Kullanıcı Profili](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express blog) ile LocalDB kullanma. LocalDB, IIS ile çalışmak üzere tasarlanmaz. Blog gönderileri Bu dizi sorunları ve bazı geçici geçici geçici işleri açıklar.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server Express Veritabanları ile Çalışma

- ASP.NET Web Uygulamaları (MSDN) [için SQL Server Bağlantı Dizeleri.](https://msdn.microsoft.com/library/jj653752.aspx) SQL Server Express ile AttachDBFileName bağlantı dize ayarını kullanıyorsanız, özellikle bu sayfanın Kullanıcı Örneği bölümüne bakın.
- [Yerel SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express blog) sahipliğini nasıl alır. SQL Server Express örneğinde yönetici olmadığınız için SQL Server Express veritabanlarıyla çalışamamak sık karşılaşılan bir sorundur. Varsayılan olarak, yalnızca SQL Server Express'i yükleyen kişi yöneticidir. Bu blog, bilgisayarda yöneticiyseniz kendinizi nasıl SQL Server Express yöneticisi yapacağınızı açıklar.
- [ASP.NET web uygulamam üretimde BIR SQL Server Express veritabanı kullanabilir mi?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL Veritabanı ile çalışma

- [Üyelik, OAuth ve SQL Veritabanı ile Güvenli ASP.NET MVC uygulamasını Windows Azure Web Sitesine](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure sitesi) dağıtın.
- [SQL Veritabanları](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure sitesi). Eğitimlere ve nasıl yapılacağınız kılavuzlarına başlarken.
- [Windows Azure SQL Veritabanı](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). MSDN'deki SQL Veritabanı için içerik tablosunun üst düzey düğümü.
- [Windows Azure SQL Veritabanı TechNet Wiki Makaleler Dizini](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft TechNet sitesi).
- [Geçici Arıza İşleme Uygulama Bloğu](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Azaltma sonucu geçici ağ hataları ve bağlantı hataları işlemek için olanak sağlayan bir çerçeve. NuGet paketinde mevcuttur: [Enterprise Library 5.0 - Geçici Arıza İşleme Uygulama Bloğu](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- SQL Veritabanı ve Varlık Çerçevesi (MSDN) [ile Başlarken.](https://msdn.microsoft.com/data/jj556244)
- [Windows Azure Eğitim Seti](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft Download Center). SQL Veritabanı için uygulamalı laboratuarlar içerir.
- [Windows Azure SQL Veritabanı Topluluk Forumu](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Windows Azure SQL Veritabanına](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN) taşıma. Microsoft Patterns and Practices ekibi tarafından kapsamlı bir uçtan uca senaryonun bir bölümü. Neden geçiş yapmak isteyebileceğinizi ve SQL Server'dan SQL Veritabanı'na nasıl geçirilenleri kapsar.
- [SQL Server Veritabanlarını Windows Azure SQL Veritabanına](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN) geçirme.
- [SQL Veritabanı Geçiş Sihirbazı](http://sqlazuremw.codeplex.com/). Veritabanlarını SQL Veritabanı'na ve SQL Veritabanı'na geçirmek için bir açık kaynak aracı.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server ve Windows Azure SQL Veritabanı arasında seçim

- [SQL Server'ı Windows Azure SQL Veritabanı](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet sitesi) ile karşılaştırın.
- [Windows Azure SQL Veritabanına Veri Geçişi: Araçlar ve Teknikler](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). SQL Server ile SQL Veritabanı'nı karşılaştıran ve SQL Server'dan SQL Veritabanı'na ne zaman geçiş yapmak gerektiğine ilişkin rehberlik sağlayan bölümler içerir.
- [Windows Azure SQL Veritabanı Teslim Kılavuzu](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet sitesi).
- [SQL Server Özellik Sınırlamaları (Windows Azure SQL Veritabanı)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure Tablo Depolama ve Windows Azure SQL Veritabanı - Karşılaştırıldığında ve Karşıt](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Windows Azure'a dağıttığınız bir uygulama için Windows Azure Table depolama alanı, Windows Azure SQL Veritabanı'na alternatif olabilir. Bu konu, bu alternatifler arasında karar vermenize yardımcı olur.
- [Windows Azure SQL Veritabanı](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Yönergeler ve Sınırlamalar (Windows Azure SQL Veritabanı)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL Veritabanı Yönetim Sistemleri ile Çalışma

- [Windows Azure Veri Hizmetleri](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure sitesi). Tablo [Hizmeti özellik kılavuzuna](https://docs.microsoft.com/azure/) ve sayfanın **Büyük Veri** bölümüne bakın.
- [Depolama Tabloları, Kuyruklar ve Blob'ları](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure sitesi) kullanarak çok katmanlı uygulama ASP.NET. Windows Azure depolama NoSQL tabloları kullanan indirilebilir örnek uygulama ile uça uça öğretici.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET Uygulamalarında LINQ Sorgularını Kullanma

- [ASP.NET Veri Erişim Seçenekleri](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). LINQ'ya giriş içerir.
- [LINQ Eğitim Videoları](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagner günlüğü).
- [Dinamik LINQ kaynaklarına bağlantılar ile ASP.NET Forum iş parçacığı](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Dinamik Veri İskelesi Kullanma

- [Dinamik Veri Projesi Şablonları](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Dinamik Veri projelerinin ne zaman kullanılacağına ilişkin yönerge.
- [ASP.NET Dinamik Veri](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Veri Erişimini Güvence Altına Alma

- [ASP.NET 'de Veri Erişimini Sağlama](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Güvenlik Hususları (Varlık Çerçevesi)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- Nasıl Kullanılır: Veri Kaynağı Denetimleri (MSDN) [kullanırken Bağlantı Dizeleri güvenli.](https://msdn.microsoft.com/library/ms178372.aspx)

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Veri Erişim Performansını Optimize Etme

- [ASP.NET Performansa Genel Bakış](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET Önbelleğe Alma](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [performansı (MSDN) geliştirme ASP.NET.](https://msdn.microsoft.com/library/ff647787) Bu sayfanın üst kısmında bir "Emekli İçerik" uyarısı vardır, ancak bilgilerin çoğu hala alakalıdır ve karşılaştırılabilir güncelleştirilmiş bir kaynak yoktur.
- [SQL Server Performansını](https://msdn.microsoft.com/library/ff647793) (MSDN) geliştirme. Önceki bağlantıyla aynı yorum.

Bu konuda varlık çerçevesi performansını daha önce [en iyi duruma getirilmesine](#optimizingef) de bakın.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Veritabanı dağıtma

- [ASP.NET Web Dağıtım - Önerilen Kaynaklar](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Web Hizmeti Aracılığıyla Verilere Erişim

- Web Hizmeti (MSDN) [aracılığıyla Verilere erişim.](https://msdn.microsoft.com/library/ms178359.aspx#webservice) WCF ile Web API'nin ne zaman kullanılacağı na ilişkin yönerge.
- [ASP.NET Web API ile başlarken.](../web-api/index.md)
- [WCF Veri Hizmetleri](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Veri Erişim SSS](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET Web Formları Öğreticiler - Veri](../web-forms/overview/data-access/index.md). Bu öğreticilerin çoğu nispeten eskidir; senaryonuz için uygun olmayan bir veri erişim yöntemine fazla yaklaşamamanız için önce [ASP.NET Veri Erişim Seçenekleri](https://msdn.microsoft.com/library/ms178359.aspx) ve Veri Depolama Seçenekleri [(Windows Azure ile Gerçek Dünya Bulut Uygulamaları Oluşturma)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) seçeneklerini okuduğunuzdan emin olun.
- [ASP.NET MVC İçerik Haritası](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [ASP.NET Web Sayfaları Öğreticiler - Veri](../web-pages/overview/data/index.md).
- [Visual Studio'da](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN) Verilere erişim. Bu içerik haritasına benzer ancak ASP.NET yerine Visual Studio'ya odaklanan bağlantıların bir listesini sağlar.
