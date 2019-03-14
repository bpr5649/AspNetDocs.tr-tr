---
title: ASP.NET Core’a Giriş
author: rick-anderson
description: 'Modern, bulut tabanlı, İnternet bağlantılı uygulamalar oluşturmaya yönelik platformlar arası, yüksek performanslı, açık kaynak bir çerçeve olan ASP.NET Core’a giriş yapın.'
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: index
---
# <a name="introduction-to-aspnet-core"></a>ASP.NET Core’a Giriş

[Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) ve [Shaun Luttin](https://twitter.com/dicshaunary) tarafından hazırlanmıştır

ASP.NET Core, modern, bulut tabanlı, İnternet bağlantılı uygulamalar oluşturmaya yönelik platformlar arası, yüksek performanslı, [açık kaynak](https://github.com/aspnet/home) bir çerçevedir. ASP.NET Core ile şunları yapabilirsiniz:

* Web uygulamaları ve hizmetleri, [IoT](https://www.microsoft.com/internet-of-things/) uygulamaları ve mobil arka uçlar oluşturun.
* Windows, macOS ve Linux üzerinde tercih ettiğiniz geliştirme araçlarını kullanın.
* Buluta veya şirket içine dağıtın.
* [.NET Core veya .NET Framework](/dotnet/articles/standard/choosing-core-framework-server) üzerinde çalıştırın.

## <a name="why-use-aspnet-core"></a>Neden ASP.NET Core kullanılmalı?

Milyonlarca geliştirici, web uygulamaları oluşturmak için [ASP.NET 4.x](/aspnet/overview) kullandı (ve kullanmaya devam ediyor). ASP.NET Core, ASP.NET 4.x sürümünün daha yalın, daha modüler bir çerçeve elde edilmesini sağlayan mimari değişikliklerle yeniden tasarlanmış halidir.

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a>ASP.NET Core MVC kullanarak web API'leri ve web kullanıcı arabirimi oluşturma

ASP.NET Core MVC, [web API’leri](xref:tutorials/first-web-api) ve [web uygulamaları](xref:tutorials/razor-pages/index) oluşturmaya yönelik özellikler sağlar:

* [Model-Görünüm-Denetleyici (MVC) deseni](xref:mvc/overview), web API'lerinin ve web uygulamalarının sınanabilir olmasını sağlamanıza yardımcı olur.
* [Razor Pages](xref:razor-pages/index), web kullanıcı arabirimi oluşturmayı daha kolay ve üretken bir hale getiren, sayfa tabanlı bir programlama modelidir.
* [Razor işaretlemesi](xref:mvc/views/razor), [Razor Sayfaları](xref:razor-pages/index) ve [MVC görünümleri](xref:mvc/views/overview) için üretken bir söz dizimi sağlar.
* [Etiket Yardımcıları](xref:mvc/views/tag-helpers/intro), Razor dosyalarında HTML öğelerinin oluşturulmasına ve işlenmesine sunucu tarafı kodun katılmasını etkinleştir.
* [Birden çok veri biçimi ve içerik anlaşması](xref:web-api/advanced/formatting) için sunulan yerleşik destek, web API'lerinizin tarayıcılar ve mobil cihazlar dahil olmak üzere birçok çeşit istemciye ulaşmasına imkan tanır.
* [Model bağlama](xref:mvc/models/model-binding), HTTP isteklerinden alınan verileri otomatik olarak eylem metodu parametreleriyle eşleştirir.
* [Model doğrulama](xref:mvc/models/validation), otomatik olarak istemci ve sunucu tarafı doğrulama gerçekleştirir.

## <a name="client-side-development"></a>İstemci tarafı geliştirme

ASP.NET Core, aralarında [Razor Components](xref:razor-components/index), [Angular](xref:spa/angular), [React](xref:spa/react) ve [Bootstrap](https://getbootstrap.com/)’in bulunduğu popüler istemci tarafı çerçeve ve kitaplıklarla sorunsuz bir şekilde tümleştirilir. Daha fazla bilgi için [Razor Components](xref:razor-components/index) ve *İstemci tarafı geliştirme* altındaki ilgili konulara bakın.

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a>.NET Framework'ü hedefleyen ASP.NET Core

ASP.NET Core 2.x, .NET Core'u veya .NET Framework'ü hedefleyebilir. .NET Framework'ü hedefleyen ASP.NET Core uygulamaları platformlar arası çalışmaz; bunlar yalnızca Windows üzerinde çalışır. Genel olarak, ASP.NET Core 2.x [.NET Standard](/dotnet/standard/net-standard) kitaplıklarından oluşturulmuştur. .NET Standard 2.0 ile yazılmış uygulamalar .NET Standard 2.0'ın desteklendiği her yerde çalıştırılır.

ASP.NET Core 2.x, .NET Standard 2.0 ile uyumlu .NET Framework sürümlerinde desteklenir:

* .NET Framework 4.7.1 ve üzeri önemle tavsiye edilir.
* .NET Framework 4.6.1 ve üzeri.

ASP.NET Core 3.0 ve üzeri yalnızca .NET Core’da çalışır. Bu değişiklik hakkında daha fazla bilgi için bkz. [ASP.NET Core 3.0’daki değişikliklere ilk bakış](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/).

.NET Core hedeflemesinin çeşitli avantajları vardır ve bu avantajlar her yeni sürümle birlikte artmaktadır. .NET Framework'e göre .NET Core'un bazı avantajları şunlardır:

* Platformlar arası. macOS, Linux ve Windows üzerinde çalışır.
* Geliştirilmiş performans
* Yan yana sürüm oluşturma
* Yeni API'ler
* Açık kaynak

.NET Framework ile .NET Core arasındaki API açığını kapatmak için çok çalışıyoruz. [Windows Uyumluluk Paketi](/dotnet/core/porting/windows-compat-pack), .NET Core'da yalnızca Windows'a yönelik binlerce API'yi kullanıma sunmaktadır. Bu API'ler .NET Core 1.x'te sağlanmamıştı.

## <a name="recommended-learning-path"></a>Önerilen öğrenme yolu

ASP.NET Core uygulamaları geliştirmeye başlamak için şu öğreticileri ve makaleleri takip etmenizi öneririz:

1. Geliştirmek veya yönetmek istediğiniz uygulama türüne yönelik bir öğreticiyi takip edin:

   |Uygulama türü  |Senaryo  |Eğitmen  |
   |----------|----------|----------|
   |Web uygulaması       | Yeni proje geliştirmek için        |[Razor Sayfaları kullanmaya başlama](xref:tutorials/razor-pages/razor-pages-start) |
   |Web uygulaması       | MVC uygulaması yönetmek için |[MVC ile çalışmaya başlama](xref:tutorials/first-mvc-app/start-mvc)|
   |Web API       |                            |[Web API’si oluşturma](xref:tutorials/first-web-api)\*  |
   |Gerçek zamanlı uygulama |                            |[SignalR ile çalışmaya başlama](xref:tutorials/signalr) |

1. Temel veri erişiminin nasıl yapıldığını gösteren bir öğreticiyi takip edin:

   |Senaryo  |Eğitmen  |
   |----------|----------|
   | Yeni proje geliştirmek için        |[Entity Framework Core ile Razor Pages](xref:data/ef-rp/intro) |
   | MVC uygulaması yönetmek için |[Entity Framework Core ile MVC](xref:data/ef-mvc/intro)

1. Tüm uygulama türleri için geçerli olan ASP.NET Core özelliklerine yönelik genel bakışı okuyun:

   * [Temeller](xref:fundamentals/index)

1. İlgilendiğiniz diğer konular için İçindekiler Tablosu’na göz atın.

Tarayıcıda tamamını takip ettiğiniz ve yerel IDE yüklemesi gerektirmeyen \* yeni bir [web API’si öğreticisi var](https://docs.microsoft.com/learn/modules/build-web-api-net-core).  Kod [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/)’de çalışır, [curl](https://curl.haxx.se/) ise test için kullanılır.

## <a name="how-to-download-a-sample"></a>Örnek indirme

Çoğu makale ve öğretici örnek koda bağlantılar içerir.

1. [ASP.NET depo zip dosyasını indirin](https://codeload.github.com/aspnet/Docs/zip/master).
1. *Docs-master.zip* dosyasının sıkıştırmasını açın.
1. Örnek dizinde gezinmek için örnek bağlantıdaki URL’yi kullanın.

### <a name="preprocessor-directives-in-sample-code"></a>Örnek kodda ön işlemci yönergeleri

Örnek uygulamalar birden çok senaryoyu göstermek amacıyla aynı koda ait farklı bölümleri seçmeli olarak derleyip çalıştırmak için `#define` ve `#if-#else/#elif-#endif` C# deyimlerini kullanır. Bu yaklaşımdan yararlanan örneklerde C# dosyalarının üst kısmındaki `#define` deyimini, çalıştırmak istediğiniz senaryoyla ilişkili olan simgeye ayarlayın. Bazı örnekler senaryoyu çalıştırmak için birden çok dosyanın üst kısmındaki simgenin ayarlanmasını gerektirebilir.

Örneğin, aşağıdaki simge listesi `#define` dört senaryonun kullanılabilir olduğunu gösterir (her simge için bir senaryo). Geçerli örnek yapılandırması `TemplateCode` senaryosunu çalıştırır:

```csharp
#define TemplateCode // or LogFromMain or ExpandDefault or FilterInCode
```

Örneği `ExpandDefault` senaryosunu çalıştıracak şekilde değiştirmek için `ExpandDefault` simgesini tanımlayın ve kalan simgeleri açıklama satırı yapılmış şekilde bırakın:

```csharp
#define ExpandDefault // TemplateCode or LogFromMain or FilterInCode
```

Kod bölümlerini seçmeli olarak derlemek üzere [C# ön işlemci yönergelerini](/dotnet/csharp/language-reference/preprocessor-directives/) kullanma hakkında daha fazla bilgi için bkz. [#define (C# Başvurusu)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define) ve [#if (C# Başvurusu)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if).

### <a name="regions-in-sample-code"></a>Örnek kodda bölgeler

Bazı örnek uygulamalar, [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) ve [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) C# deyimleri içine yerleştirilmiş kod bölümleri içerir. Belge derleme sistemi bu bölgeleri işlenmiş belge konularının içine ekler.  

Bölge adları çoğunlukla şu sözcüğü içerir: "snippet." Aşağıdaki örnekte `snippet_FilterInCode` adlı bir bölge gösterilir:

```csharp
#region snippet_FilterInCode
WebHost.CreateDefaultBuilder(args)
    .UseStartup<Startup>()
    .ConfigureLogging(logging =>
        logging.AddFilter("System", LogLevel.Debug)
            .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Trace))
            .Build();
#endregion
```

Önündeki C# kod parçacığına, konunun markdown dosyasında aşağıdaki satırla başvurulur:

```
[!code-csharp[](sample/SampleApp/Program.cs?name=snippet_FilterInCode)]
```

Kodu çevreleyen `#region` ve `#endregion` deyimlerini rahatça yoksayabilirsiniz (veya kaldırabilirsiniz). Konuda açıklanan örnek senaryoları çalıştırmayı planlıyorsanız, bu deyimlerin anasındaki kodu değiştirmeyin. Başka senaryolarla denemeler yaparken kodu rahatça değiştirebilirsiniz.

Daha fazla bilgi için bkz. [ASP.NET belgelerine katkıda bulunma: Kod parçacıkları](https://github.com/aspnet/Docs/blob/master/CONTRIBUTING.md#code-snippets).

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

* <xref:getting-started>
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [ASP.NET Core temelleri](xref:fundamentals/index)
* [Haftalık ASP.NET topluluğu toplantısında](https://live.asp.net/), takımın ilerleme durumu ve planları ele alınır. Yeni bloglara ve üçüncü taraf yazılıma yer verilir.
