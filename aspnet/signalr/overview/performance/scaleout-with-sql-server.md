---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server ile SignalR ölçeğini genişletme | Microsoft Docs
author: bradygaster
description: Yazılım sürümleri, sürüm 2 önceki sürümleri bu konunun önceki sürümleri hakkında bilgi için bu konu Visual Studio 2013 .NET 4.5 SignalR kullanılan...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: c0c214ea32ad13b3a63be9ef84bcb4b8bc7311aa
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393587"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="68727-103">SQL Server ile SignalR Ölçeğini Genişletme</span><span class="sxs-lookup"><span data-stu-id="68727-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="68727-104">tarafından [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="68727-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="68727-105">Bu konu başlığında kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="68727-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="68727-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="68727-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="68727-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="68727-107">.NET 4.5</span></span>
> - <span data-ttu-id="68727-108">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="68727-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="68727-109">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="68727-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="68727-110">SignalR eski sürümleri hakkında daha fazla bilgi için bkz: [SignalR eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="68727-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="68727-111">Sorularınız ve yorumlarınız</span><span class="sxs-lookup"><span data-stu-id="68727-111">Questions and comments</span></span>
>
> <span data-ttu-id="68727-112">Lütfen bu öğreticide sevmediğinizi nasıl ve ne sayfanın alt kısmındaki açıklamalarda geliştirebileceğimiz hakkında geri bildirim bırakın.</span><span class="sxs-lookup"><span data-stu-id="68727-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="68727-113">Öğretici için doğrudan ilgili olmayan sorularınız varsa, bunları gönderebilir [ASP.NET SignalR Forumu](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="68727-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="68727-114">Bu öğreticide, iki ayrı IIS ınstances'ta dağıtılabilen bir SignalR uygulama iletilerini dağıtmak üzere SQL Server'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="68727-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="68727-115">Bu öğreticide tek test makinesinde çalıştırabilirsiniz ancak tam etkisi almak için iki veya daha fazla sunucu SignalR uygulamayı dağıtmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="68727-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="68727-116">SQL Server sunuculardan biri üzerinde veya ayrılmış ayrı bir sunucuya yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68727-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="68727-117">Başka bir seçenek, Azure üzerinde sanal makineleri kullanarak öğreticiyi çalıştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="68727-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="68727-118">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="68727-118">Prerequisites</span></span>

<span data-ttu-id="68727-119">Microsoft SQL Server 2005 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="68727-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="68727-120">Devre kartına hem Masaüstü hem de sunucu SQL Server sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="68727-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="68727-121">SQL Server Compact Edition veya Azure SQL veritabanı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="68727-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="68727-122">(Uygulamanız Azure üzerinde barındırılıyorsa, bunun yerine Service Bus devre kartına düşünün.)</span><span class="sxs-lookup"><span data-stu-id="68727-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="68727-123">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="68727-123">Overview</span></span>

<span data-ttu-id="68727-124">Ayrıntılı Öğreticisine aldığımız önce ne yapacağını, hızlı bir genel bakış aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="68727-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="68727-125">Yeni bir boş veritabanı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="68727-125">Create a new empty database.</span></span> <span data-ttu-id="68727-126">Devre kartına gerekli tabloları bu veritabanında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="68727-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="68727-127">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="68727-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="68727-128">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="68727-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="68727-129">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="68727-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="68727-130">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68727-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="68727-131">Devre kartına yapılandırmak için Startup.cs için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="68727-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="68727-132">Bu kod için varsayılan değerlerle devre kartına yapılandırır [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) ve [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span><span class="sxs-lookup"><span data-stu-id="68727-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="68727-133">Bu değerleri değiştirme hakkında daha fazla bilgi için bkz: [SignalR performansı: Genişletme ölçümleri](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="68727-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="68727-134">Veritabanını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="68727-134">Configure the Database</span></span>

<span data-ttu-id="68727-135">Uygulamayı Windows kimlik doğrulaması veya SQL Server kimlik doğrulaması veritabanına erişmek için kullanıp kullanmayacağını karar verin.</span><span class="sxs-lookup"><span data-stu-id="68727-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="68727-136">Ne olursa olsun, veritabanı kullanıcı oturum açmak için şema oluşturma ve tablo oluşturma izni olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="68727-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="68727-137">Devre kartına kullanmak için yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68727-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="68727-138">Veritabanı adı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68727-138">You can give the database any name.</span></span> <span data-ttu-id="68727-139">Veritabanında tablo oluşturmanız gerekmez; devre kartına gerekli tabloları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="68727-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="68727-140">Hizmet Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="68727-140">Enable Service Broker</span></span>

<span data-ttu-id="68727-141">Devre kartına veritabanı için hizmet Aracısı etkinleştirme önerilir.</span><span class="sxs-lookup"><span data-stu-id="68727-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="68727-142">Hizmet Aracısı ileti ve daha verimli bir şekilde güncelleştirmelerini devre kartına sağlayan, SQL Server'da queuing için yerel destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="68727-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="68727-143">(Ancak devre kartına Ayrıca hizmet aracısı çalışır.)</span><span class="sxs-lookup"><span data-stu-id="68727-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="68727-144">Hizmet Aracısı etkin olup olmadığını denetlemek için sorgu **olduğu\_Aracısı\_etkin** sütununda **sys.databases** Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="68727-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="68727-145">Hizmet Aracısı'nı etkinleştirmek için aşağıdaki SQL sorgusunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="68727-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="68727-146">Bu sorgu görünürse emin olmak için kilitlenme DB'ye bağlı hiç uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="68727-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>


<span data-ttu-id="68727-147">İzleme etkinleştirilirse, izlemeleri Ayrıca hizmet Aracısı etkin olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="68727-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="68727-148">Bir SignalR uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="68727-148">Create a SignalR Application</span></span>

<span data-ttu-id="68727-149">Bir SignalR uygulaması ya da bu öğreticileri izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="68727-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="68727-150">SignalR 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="68727-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="68727-151">SignalR 2.0 ve MVC 5 kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="68727-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="68727-152">Ardından, biz sohbet uygulaması, SQL Server ile ölçeğini genişletme destekleyecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68727-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="68727-153">İlk olarak, SignalR.SqlServer NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="68727-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="68727-154">Visual Studio'da gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="68727-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="68727-155">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="68727-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="68727-156">Ardından, Startup.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="68727-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="68727-157">Aşağıdaki kodu ekleyin **yapılandırma** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="68727-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="68727-158">Dağıtma ve uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="68727-158">Deploy and Run the Application</span></span>

<span data-ttu-id="68727-159">SignalR uygulamayı dağıtmak için Windows Server örneklerinizin hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="68727-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="68727-160">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="68727-160">Add the IIS role.</span></span> <span data-ttu-id="68727-161">WebSocket Protokolü dahil olmak üzere "Uygulama geliştirme" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="68727-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="68727-162">Yönetim Hizmeti ("Yönetim Araçları" altında listelenen) de içerir.</span><span class="sxs-lookup"><span data-stu-id="68727-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="68727-163">**Yükleme Web dağıtımı 3.0.**</span><span class="sxs-lookup"><span data-stu-id="68727-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="68727-164">IIS Yöneticisi'ni çalıştırın, Microsoft Web Platformu'nu yüklemenizi ister veya yapabilecekleriniz [yükleyiciyi indirin](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="68727-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="68727-165">Platform Yükleyicisi'nde, Web dağıtımı için arama ve Web dağıtımı 3.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="68727-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="68727-166">Web yönetimi hizmeti çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68727-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="68727-167">Aksi durumda, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="68727-167">If not, start the service.</span></span> <span data-ttu-id="68727-168">(Web yönetimi hizmeti Windows Hizmetleri listede görmüyorsanız, IIS rolü eklendiğinde yönetim Hizmeti'nin yüklü emin olun.)</span><span class="sxs-lookup"><span data-stu-id="68727-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="68727-169">Son olarak, TCP bağlantı noktası 8172 açın.</span><span class="sxs-lookup"><span data-stu-id="68727-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="68727-170">Bu, Web dağıtımı Aracı'nı kullanan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="68727-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="68727-171">Geliştirme makinenizde Visual Studio projesinden sunucusuna dağıtmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="68727-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="68727-172">Çözüm Gezgini'nde çözüme sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="68727-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="68727-173">Belgeler web dağıtımı hakkında daha fazla ayrıntılı için bkz [Visual Studio ve ASP.NET için Web dağıtımı içerik haritası](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="68727-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="68727-174">İki sunucu için uygulama dağıtıyorsanız, her örnek bir ayrı bir tarayıcı penceresi açın ve her SignalR iletileri diğer aldığınız bakın.</span><span class="sxs-lookup"><span data-stu-id="68727-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="68727-175">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına sit.)</span><span class="sxs-lookup"><span data-stu-id="68727-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="68727-176">Uygulamayı çalıştırdıktan sonra bir veritabanında tabloları, SignalR otomatik olarak oluşturduğu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="68727-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="68727-177">SignalR tablolarını yönetir.</span><span class="sxs-lookup"><span data-stu-id="68727-177">SignalR manages the tables.</span></span> <span data-ttu-id="68727-178">Uygulamanızın dağıtıldığı sürece, yok satırları silmek, tabloyu değiştirebilir ve VS.</span><span class="sxs-lookup"><span data-stu-id="68727-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
