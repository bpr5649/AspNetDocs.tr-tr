---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SQL Server ile SignalR ölçeğini genişletme (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: eb0d6cd23563f72bb382b3a3304d03294f783ad8
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425853"
---
<a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="06931-102">SQL Server ile SignalR Ölçeğini Genişletme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="06931-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>
====================
<span data-ttu-id="06931-103">tarafından [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="06931-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="06931-104">Bu öğreticide, iki ayrı IIS ınstances'ta dağıtılabilen bir SignalR uygulama iletilerini dağıtmak üzere SQL Server'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="06931-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="06931-105">Bu öğreticide tek test makinesinde çalıştırabilirsiniz ancak tam etkisi almak için iki veya daha fazla sunucu SignalR uygulamayı dağıtmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="06931-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="06931-106">SQL Server sunuculardan biri üzerinde veya ayrılmış ayrı bir sunucuya yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06931-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="06931-107">Başka bir seçenek, Azure üzerinde sanal makineleri kullanarak öğreticiyi çalıştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="06931-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="06931-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="06931-108">Prerequisites</span></span>

<span data-ttu-id="06931-109">Microsoft SQL Server 2005 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="06931-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="06931-110">Devre kartına hem Masaüstü hem de sunucu SQL Server sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="06931-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="06931-111">SQL Server Compact Edition veya Azure SQL veritabanı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="06931-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="06931-112">(Uygulamanız Azure üzerinde barındırılıyorsa, bunun yerine Service Bus devre kartına düşünün.)</span><span class="sxs-lookup"><span data-stu-id="06931-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="06931-113">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="06931-113">Overview</span></span>

<span data-ttu-id="06931-114">Ayrıntılı Öğreticisine aldığımız önce ne yapacağını, hızlı bir genel bakış aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="06931-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="06931-115">Yeni bir boş veritabanı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="06931-115">Create a new empty database.</span></span> <span data-ttu-id="06931-116">Devre kartına gerekli tabloları bu veritabanında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06931-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="06931-117">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06931-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="06931-118">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="06931-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="06931-119">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="06931-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="06931-120">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06931-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="06931-121">Devre kartına yapılandırmak için Global.asax için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06931-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="06931-122">Veritabanını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="06931-122">Configure the Database</span></span>

<span data-ttu-id="06931-123">Uygulamayı Windows kimlik doğrulaması veya SQL Server kimlik doğrulaması veritabanına erişmek için kullanıp kullanmayacağını karar verin.</span><span class="sxs-lookup"><span data-stu-id="06931-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="06931-124">Ne olursa olsun, veritabanı kullanıcı oturum açmak için şema oluşturma ve tablo oluşturma izni olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="06931-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="06931-125">Devre kartına kullanmak için yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06931-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="06931-126">Veritabanı adı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06931-126">You can give the database any name.</span></span> <span data-ttu-id="06931-127">Veritabanında tablo oluşturmanız gerekmez; devre kartına gerekli tabloları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06931-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="06931-128">Hizmet Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="06931-128">Enable Service Broker</span></span>

<span data-ttu-id="06931-129">Devre kartına veritabanı için hizmet Aracısı etkinleştirme önerilir.</span><span class="sxs-lookup"><span data-stu-id="06931-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="06931-130">Hizmet Aracısı ileti ve daha verimli bir şekilde güncelleştirmelerini devre kartına sağlayan, SQL Server'da queuing için yerel destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="06931-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="06931-131">(Ancak devre kartına Ayrıca hizmet aracısı çalışır.)</span><span class="sxs-lookup"><span data-stu-id="06931-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="06931-132">Hizmet Aracısı etkin olup olmadığını denetlemek için sorgu **olduğu\_Aracısı\_etkin** sütununda **sys.databases** Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="06931-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="06931-133">Hizmet Aracısı'nı etkinleştirmek için aşağıdaki SQL sorgusunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="06931-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="06931-134">Bu sorgu görünürse emin olmak için kilitlenme DB'ye bağlı hiç uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="06931-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="06931-135">İzleme etkinleştirilirse, izlemeleri Ayrıca hizmet Aracısı etkin olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="06931-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="06931-136">Bir SignalR uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="06931-136">Create a SignalR Application</span></span>

<span data-ttu-id="06931-137">Bir SignalR uygulaması ya da bu öğreticileri izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="06931-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="06931-138">SignalR ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="06931-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="06931-139">SignalR ve MVC 4 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="06931-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="06931-140">Ardından, biz sohbet uygulaması, SQL Server ile ölçeğini genişletme destekleyecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="06931-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="06931-141">İlk olarak, SignalR.SqlServer NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06931-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="06931-142">Visual Studio'da gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="06931-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="06931-143">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="06931-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="06931-144">Ardından, Global.asax dosyası açın.</span><span class="sxs-lookup"><span data-stu-id="06931-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="06931-145">Aşağıdaki kodu ekleyin **uygulama\_Başlat** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="06931-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="06931-146">Dağıtma ve uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="06931-146">Deploy and Run the Application</span></span>

<span data-ttu-id="06931-147">SignalR uygulamayı dağıtmak için Windows Server örneklerinizin hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="06931-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="06931-148">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06931-148">Add the IIS role.</span></span> <span data-ttu-id="06931-149">WebSocket Protokolü dahil olmak üzere "Uygulama geliştirme" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="06931-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="06931-150">Yönetim Hizmeti ("Yönetim Araçları" altında listelenen) de içerir.</span><span class="sxs-lookup"><span data-stu-id="06931-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="06931-151">**Yükleme Web dağıtımı 3.0.**</span><span class="sxs-lookup"><span data-stu-id="06931-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="06931-152">IIS Yöneticisi'ni çalıştırın, Microsoft Web Platformu'nu yüklemenizi ister veya yapabilecekleriniz [yükleyiciyi indirin](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="06931-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="06931-153">Platform Yükleyicisi'nde, Web dağıtımı için arama ve Web dağıtımı 3.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="06931-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="06931-154">Web yönetimi hizmeti çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="06931-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="06931-155">Aksi durumda, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="06931-155">If not, start the service.</span></span> <span data-ttu-id="06931-156">(Web yönetimi hizmeti Windows Hizmetleri listede görmüyorsanız, IIS rolü eklendiğinde yönetim Hizmeti'nin yüklü emin olun.)</span><span class="sxs-lookup"><span data-stu-id="06931-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="06931-157">Son olarak, TCP bağlantı noktası 8172 açın.</span><span class="sxs-lookup"><span data-stu-id="06931-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="06931-158">Bu, Web dağıtımı Aracı'nı kullanan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="06931-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="06931-159">Geliştirme makinenizde Visual Studio projesinden sunucusuna dağıtmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="06931-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="06931-160">Çözüm Gezgini'nde çözüme sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="06931-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="06931-161">Belgeler web dağıtımı hakkında daha fazla ayrıntılı için bkz [Visual Studio ve ASP.NET için Web dağıtımı içerik haritası](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="06931-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="06931-162">İki sunucu için uygulama dağıtıyorsanız, her örnek bir ayrı bir tarayıcı penceresi açın ve her SignalR iletileri diğer aldığınız bakın.</span><span class="sxs-lookup"><span data-stu-id="06931-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="06931-163">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına sit.)</span><span class="sxs-lookup"><span data-stu-id="06931-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="06931-164">Uygulamayı çalıştırdıktan sonra bir veritabanında tabloları, SignalR otomatik olarak oluşturduğu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="06931-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="06931-165">SignalR tablolarını yönetir.</span><span class="sxs-lookup"><span data-stu-id="06931-165">SignalR manages the tables.</span></span> <span data-ttu-id="06931-166">Uygulamanızın dağıtıldığı sürece, yok satırları silmek, tabloyu değiştirebilir ve VS.</span><span class="sxs-lookup"><span data-stu-id="06931-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
