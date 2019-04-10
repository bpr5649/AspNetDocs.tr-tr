---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2'de izleme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API'de izlemenin nasıl etkinleştirileceği gösterilmektedir.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59405904"
---
# <a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2'de izleme

tarafından [Mike Wasson](https://github.com/MikeWasson)

> Web tabanlı bir uygulamanın hatalarını ayıklama çalışırken izleme günlüklerini iyi bir dizi için geçerli olur. Bu öğreticide, ASP.NET Web API'de izlemenin nasıl etkinleştirileceği gösterilmektedir. Bu özellik, Web API çerçevesi önce ve sonra denetleyiciyi çağıran yaptığı izlemek için kullanabilirsiniz. Kendi kodunuzu izlemek için de kullanabilirsiniz.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Bu öğreticide kullanılan yazılım sürümleri
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (Visual Studio 2015 ile de çalışır)
> - Web API 2
> - [Microsoft.AspNet.WebApi.Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>Web API'si izleme System.Diagnostics etkinleştir

İlk olarak, yeni bir ASP.NET Web uygulaması projesi oluşturacağız. Visual Studio'da gelen **dosya** menüsünde **yeni** > **proje**. Altında **şablonları**, **Web**seçin **ASP.NET Web uygulaması**.

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

Web API proje şablonunu seçin.

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **paket yönetme Konsolu**.

Paket Yöneticisi konsolu penceresinde, aşağıdaki komutları yazın.

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

İlk komut, en son Web API'sini izleme paketini yükler. Ayrıca, core Web API'si paketleri güncelleştirir. İkinci komut, en son sürüme WebApi.WebHost paketini güncelleştirir.

> [!NOTE]
> Belirli bir Web API sürümünü hedeflemek istiyorsanız, kullanma izleme paketi yüklediğinizde sürüm bayrağı.

Uygulamada WebApiConfig.cs dosya açma\_başlangıç klasörü. Aşağıdaki kodu ekleyin **kaydetme** yöntemi.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

Bu kod ekler [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) Web API ardışık düzeni için sınıf. **SystemDiagnosticsTraceWriter** sınıfı Yazar izlemelere [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).

İzlemelerini görmek için hata ayıklayıcıda uygulamayı çalıştırın. Tarayıcıda gidin `/api/values`.

![](tracing-in-aspnet-web-api/_static/image5.png)

İzleme Deyimleri Visual Studio çıktı penceresinde yazılır. (Gelen **görünümü** menüsünde **çıkış**).

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

Çünkü **SystemDiagnosticsTraceWriter** izlemeleri için Yazar **System.Diagnostics.Trace**, ek izleme dinleyicileri kaydedebilirsiniz; Örneğin, yazma için izler bir günlük dosyasına. İzleme yazıcılar hakkında daha fazla bilgi için bkz. [izleme dinleyicilerine](https://msdn.microsoft.com/library/4y5y10s7.aspx) MSDN'de konu.

### <a name="configuring-systemdiagnosticstracewriter"></a>SystemDiagnosticsTraceWriter yapılandırma

Aşağıdaki kod, izleme yazıcısı yapılandırma işlemi gösterilmektedir.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

Denetleyebileceğiniz iki ayarı vardır:

- IsVerbose: False ise, her izleme en düşük miktarda bilgiyi içerir. TRUE ise izlemeleri daha fazla bilgi içerir.
- MinimumLevel: Minimum izleme düzeyini ayarlar. İzleme düzeylerini, sırasıyla, hata ayıklama, bilgi, uyarı, hata ve önemli olan.

## <a name="adding-traces-to-your-web-api-application"></a>Web API uygulamanızı izlemeleri ekleme

Bir izleme yazıcısı ekleme Web API ardışık düzeni tarafından oluşturulan izlemeleri anında erişim sağlar. Kendi kodunuzu izlemek için izleme yazıcısı de kullanabilirsiniz:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

İzleme yazıcısı almak için arama **HttpConfiguration.Services.GetTraceWriter**. Bu yöntem bir denetleyiciden üzerinden erişilebilir **ApiController.Configuration** özelliği.

Bir izleme yazmak için çağırabilirsiniz **ITraceWriter.Trace** yöntemi doğrudan, ancak [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) sınıfı daha kolay olan bazı genişletme yöntemleri tanımlar. Örneğin, **bilgisi** yukarıda gösterilen yöntemi oluşturur bir izleme ile izleme düzeyini **bilgisi**.

## <a name="web-api-tracing-infrastructure"></a>Web API izleme altyapısı

Bu bölümde, bir Web API'si için özel izleme yazıcısı yazma açıklar.

Web API'de daha genel bir izleme altyapısının en üstünde Microsoft.AspNet.WebApi.Tracing paket oluşturulur. Microsoft.AspNet.WebApi.Tracing kullanmak yerine, ayrıca bazı diğer izleme/günlüğünü Kitaplığı'nda, aşağıdaki gibi takabilirsiniz [NLog](http://nlog-project.org/) veya [log4net](http://logging.apache.org/log4net/).

İzlemeleri toplamak için uygulama **ITraceWriter** arabirimi. Basit bir örnek aşağıda verilmiştir:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter.Trace** yöntemi, bir izleme oluşturur. Arayan bir kategori ve izleme düzeyini belirtir. Kategori herhangi bir kullanıcı tanımlı dize olabilir. Uygulamanıza **izleme** aşağıdakileri yapmalıdır:

1. Yeni bir **TraceRecord**. Bu istek, kategori ve izleme düzeyi ile gösterildiği gibi başlatın. Bu değerler, çağıran tarafından sağlanır.
2. Çağırma *traceAction* temsilci. Bu temsilci içinde çağırana geri kalanında doldurması beklenir **TraceRecord**.
3. Yazma **TraceRecord**, istediğiniz herhangi bir günlük teknik kullanarak. İçine burada gösterilen örnek yalnızca yapılan çağrılar **System.Diagnostics.Trace**.

## <a name="setting-the-trace-writer"></a>İzleme yazıcısı ayarlama

İzlemeyi etkinleştirmek için Web API'ı kullanmak için yapılandırmanız gerekir, **ITraceWriter** uygulaması. Bunu aracılığıyla **HttpConfiguration** nesne, aşağıdaki kodda gösterildiği gibi:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

Yalnızca bir izleme yazıcısı etkin olabilir. Varsayılan olarak, Web API kümelerini bir &quot;İşlemsiz&quot; hiçbir şey yapmaz İzleyici. ( &quot;İşlemsiz&quot; İzleyici mevcut izleme yazıcısı olup olmadığını denetlemek izleme kodu yok böylece **null** izleme yazmadan önce.)

## <a name="how-web-api-tracing-works"></a>Nasıl çalıştığını izleme API Web

Web API izleme kullanan bir *cephe* Desen: İzleme etkin olduğunda, Web API'sini izleme çağrıları gerçekleştirmek sınıflarla istek ardışık düzenini çeşitli bölümlerini sarmalar.

Örneğin, bir denetleyici seçerken, işlem hattı kullanır **IHttpControllerSelector** arabirimi. Etkin izleme ile işlem hattı uygulayan bir sınıf ekler **IHttpControllerSelector** ancak çağrıları üzerinden gerçek uygulama:

![Web API izlemesi cephe deseni kullanır.](tracing-in-aspnet-web-api/_static/image8.png)

Bu tasarım avantajları şunlardır:

- İzleme yazıcısı eklemezseniz izleme bileşenleri değil örneği oluşturulur ve performansını etkilemez.
- Varsayılan hizmetler gibi değiştirirseniz **IHttpControllerSelector** izleme sarmalayıcısı nesne tarafından yapıldığı için kendi özel uygulamasıyla izleme etkilenmez.

Varsayılan değiştirerek kendi özel framework ile tüm Web API izleme çerçevesini değiştirebilirsiniz **ITraceManager** hizmeti:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

Uygulama **ITraceManager.Initialize** izleme sisteminizi başlatılamadı. Bu değiştirir unutmayın *tüm* tüm Web API'sine yerleşik izleme kodu da dahil olmak üzere, izleme framework.
