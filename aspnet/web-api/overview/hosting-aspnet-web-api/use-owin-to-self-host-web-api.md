---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Barındırılan ASP.NET Web API'si için OWIN kullanın | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, ASP.NET Web API OWIN barındırma Web API çerçevesini kullanarak bir konsol uygulamasında barındırmak gösterilir. .NET (OWIN) d için Web arabirimi Aç...
ms.author: riande
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 59ce24aa47ca590fbe9b617dbbe8bc6b3711849e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076335"
---
<a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="2e333-104">Barındırılan ASP.NET Web API'si için OWIN kullanın</span><span class="sxs-lookup"><span data-stu-id="2e333-104">Use OWIN to Self-Host ASP.NET Web API</span></span> 
====================

> <span data-ttu-id="2e333-105">Bu öğreticide, ASP.NET Web API OWIN barındırma Web API çerçevesini kullanarak bir konsol uygulamasında barındırmak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2e333-105">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="2e333-106">[.NET için açık Web arabirimi](http://owin.org) (OWIN) .NET web sunucuları ve web uygulaması arasında bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2e333-106">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="2e333-107">OWIN OWIN kendi işleminizde IIS dışında bir web uygulaması kendi kendine barındırma için ideal hale getirir sunucu web uygulamasından ayırır.</span><span class="sxs-lookup"><span data-stu-id="2e333-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2e333-108">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="2e333-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="2e333-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2e333-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="2e333-110">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="2e333-110">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="2e333-111">Bu öğreticinin için tam kaynak kodunu bulabilirsiniz [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="2e333-111">You can find the complete source code for this tutorial at [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="2e333-112">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e333-112">Create a console application</span></span>

<span data-ttu-id="2e333-113">Üzerinde **dosya** menüsünde **yeni**, ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="2e333-113">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="2e333-114">Gelen **yüklü**altında **Visual C#** seçin **Windows Masaüstü** seçip **konsol uygulaması (.Net Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2e333-114">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="2e333-115">"OwinSelfhostSample" Projeyi adlandırın ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2e333-115">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="2e333-116">Web API ve OWIN paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="2e333-116">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="2e333-117">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="2e333-117">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2e333-118">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="2e333-118">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="2e333-119">Bu Webapı OWIN selfhost paketi ve tüm gerekli OWIN paketlerini yükler.</span><span class="sxs-lookup"><span data-stu-id="2e333-119">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="2e333-120">Web API'sini yapılandırmak için barındırma</span><span class="sxs-lookup"><span data-stu-id="2e333-120">Configure Web API for self-host</span></span>

<span data-ttu-id="2e333-121">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle** / **sınıfı** yeni bir sınıf eklemek için.</span><span class="sxs-lookup"><span data-stu-id="2e333-121">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="2e333-122">Sınıf adını `Startup`.</span><span class="sxs-lookup"><span data-stu-id="2e333-122">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="2e333-123">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2e333-123">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="2e333-124">Bir Web API denetleyicisi Ekle</span><span class="sxs-lookup"><span data-stu-id="2e333-124">Add a Web API controller</span></span>

<span data-ttu-id="2e333-125">Ardından, bir Web API denetleyici sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2e333-125">Next, add a Web API controller class.</span></span> <span data-ttu-id="2e333-126">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle** / **sınıfı** yeni bir sınıf eklemek için.</span><span class="sxs-lookup"><span data-stu-id="2e333-126">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="2e333-127">Sınıf adını `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="2e333-127">Name the class `ValuesController`.</span></span>

<span data-ttu-id="2e333-128">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2e333-128">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="2e333-129">OWIN konak başlatın ve bir istekte içeren HttpClient</span><span class="sxs-lookup"><span data-stu-id="2e333-129">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="2e333-130">Tüm ortak kod Program.cs dosyasındaki aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2e333-130">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="2e333-131">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2e333-131">Run the application</span></span>

<span data-ttu-id="2e333-132">Uygulamayı çalıştırmak için Visual Studio'da F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2e333-132">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="2e333-133">Çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="2e333-133">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="2e333-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2e333-134">Additional resources</span></span>

[<span data-ttu-id="2e333-135">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2e333-135">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="2e333-136">Bir Azure çalışan rolünde ASP.NET Web API barındırma</span><span class="sxs-lookup"><span data-stu-id="2e333-136">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
