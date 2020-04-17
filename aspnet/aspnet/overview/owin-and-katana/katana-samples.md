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
# <a name="katana-samples"></a><span data-ttu-id="4fdb8-102">Katana Örnekleri</span><span class="sxs-lookup"><span data-stu-id="4fdb8-102">Katana Samples</span></span>

<span data-ttu-id="4fdb8-103">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="4fdb8-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="4fdb8-104">Katana Örnekleri</span><span class="sxs-lookup"><span data-stu-id="4fdb8-104">Katana Samples</span></span>

<span data-ttu-id="4fdb8-105">**ASP.NET Rotalar Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="4fdb8-106">Bazı uygulamalarda, owin olmayan bileşenlerle Asp.Net rota tablosundaki OWIN bileşenlerini yan yana bağlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="4fdb8-107">Bu örnek, Microsoft.Owin.Host.SystemWeb tarafından sağlanan MapOwinPath ve MapOwinRoute Route Collection uzantı yöntemlerinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="4fdb8-108">**Dallanma Boru Hatları Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="4fdb8-109">OWIN istek işleme ardışık hatları doğrusal olması gerekmez, onlar farklı şekillerde istekleri işlemek için dallanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="4fdb8-110">Bu örnek, istek yollarına veya üstbilgiler gibi diğer istek verilerine dayalı bir dallanma ardışık alanının nasıl inşa edilebildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="4fdb8-111">Bu bileşenler Microsoft.Owin.Mapping nuget paketinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="4fdb8-112">**Özel Sunucu Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="4fdb8-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="4fdb8-113">Kendi kendine barındırma OWIN zaman özel bir OWIN sunucusu nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="4fdb8-114">**Gömülü Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="4fdb8-115">Bazı OWIN sunucuları kendi sürecinizin&quot;içinde çalıştırılabilir (kendi kendine barındırılan).&quot;</span><span class="sxs-lookup"><span data-stu-id="4fdb8-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="4fdb8-116">Bu örnek, Microsoft.Owin.Hosting nuget paketi tarafından sağlanan araçları kullanarak bir OWIN uygulamasının nasıl başlatılabildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="4fdb8-117">**HelloWorld Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="4fdb8-118">OWIN, çeşitli sunucularda uygulama taşınabilirliği sağlayan bir HTTP sunucusu API soyutlamasidir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="4fdb8-119">Bu örnek nasıl ham OWIN soyutlama etrafında bazı **basit sarmalayıcıları** kullanarak bir Hello World uygulaması yazmak ve ASP.NET gibi bir web sunucusunda çalıştırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="4fdb8-120">**Merhaba Dünya Ham OWIN Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="4fdb8-121">Bu örnek nasıl **ham** OWIN soyutlama kullanarak bir Hello World uygulaması yazmak ve Asp.Net gibi bir web sunucusunda çalıştırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="4fdb8-122">**SignalR Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="4fdb8-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="4fdb8-123">OWIN / Katana kullanarak SignalR'ı nasıl barındırılabildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="4fdb8-124">Kendi kendine barındırma SignalR hakkında daha fazla bilgi için, [Eğitim bakın: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="4fdb8-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="4fdb8-125">**Statik Dosyalar Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="4fdb8-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="4fdb8-126">OWIN / Katana kullanarak statik dosyalar için HTTP isteklerini nasıl destekleyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="4fdb8-127">**Web API** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="4fdb8-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="4fdb8-128">Bu örnek, OWIN'i IIS'de nasıl barındırılabildiğini ve OWIN ardışık adına Web API'sinin nasıl ekleyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="4fdb8-129">**Web Soketi Örnek** | [Kaynak Kodu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="4fdb8-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="4fdb8-130">[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) sınıfını kullanarak OWIN'de Web Soketlerinin nasıl desteklenebildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fdb8-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
