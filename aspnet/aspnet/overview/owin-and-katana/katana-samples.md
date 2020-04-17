---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Örnekleri | Microsoft Dokümanlar
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540447"
---
# <a name="katana-samples"></a>Katana Örnekleri

[Microsoft](https://github.com/microsoft) tarafından

## <a name="katana-samples"></a>Katana Örnekleri

**ASP.NET Rotalar Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
Bazı uygulamalarda, owin olmayan bileşenlerle Asp.Net rota tablosundaki OWIN bileşenlerini yan yana bağlamak isteyebilirsiniz. Bu örnek, Microsoft.Owin.Host.SystemWeb tarafından sağlanan MapOwinPath ve MapOwinRoute Route Collection uzantı yöntemlerinin nasıl kullanılacağını gösterir.

**Dallanma Boru Hatları Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN istek işleme ardışık hatları doğrusal olması gerekmez, onlar farklı şekillerde istekleri işlemek için dallanmış olabilir. Bu örnek, istek yollarına veya üstbilgiler gibi diğer istek verilerine dayalı bir dallanma ardışık alanının nasıl inşa edilebildiğini gösterir. Bu bileşenler Microsoft.Owin.Mapping nuget paketinde kullanılabilir.

**Özel Sunucu Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
Kendi kendine barındırma OWIN zaman özel bir OWIN sunucusu nasıl kullanılacağını gösterir.

**Gömülü Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Bazı OWIN sunucuları kendi sürecinizin&quot;içinde çalıştırılabilir (kendi kendine barındırılan).&quot; Bu örnek, Microsoft.Owin.Hosting nuget paketi tarafından sağlanan araçları kullanarak bir OWIN uygulamasının nasıl başlatılabildiğini gösterir.

**HelloWorld Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN, çeşitli sunucularda uygulama taşınabilirliği sağlayan bir HTTP sunucusu API soyutlamasidir. Bu örnek nasıl ham OWIN soyutlama etrafında bazı **basit sarmalayıcıları** kullanarak bir Hello World uygulaması yazmak ve ASP.NET gibi bir web sunucusunda çalıştırmak gösterir.

**Merhaba Dünya Ham OWIN Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
Bu örnek nasıl **ham** OWIN soyutlama kullanarak bir Hello World uygulaması yazmak ve Asp.Net gibi bir web sunucusunda çalıştırmak gösterir.

**SignalR Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWIN / Katana kullanarak SignalR'ı nasıl barındırılabildiğini gösterir. Kendi kendine barındırma SignalR hakkında daha fazla bilgi için, [Eğitim bakın: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Statik Dosyalar Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWIN / Katana kullanarak statik dosyalar için HTTP isteklerini nasıl destekleyeceğini gösterir.

**Web API** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
Bu örnek, OWIN'i IIS'de nasıl barındırılabildiğini ve OWIN ardışık adına Web API'sinin nasıl ekleyeceğini gösterir.

**Web Soketi Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) sınıfını kullanarak OWIN'de Web Soketlerinin nasıl desteklenebildiğini gösterir.
