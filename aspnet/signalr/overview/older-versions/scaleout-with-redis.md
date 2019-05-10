---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redis ile SignalR ölçeğini genişletme (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117049"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="a8d24-102">Redis ile SignalR Ölçeğini Genişletme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="a8d24-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="a8d24-103">tarafından [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a8d24-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a8d24-104">Bu öğreticide kullanacağınız [Redis](http://redis.io/) iletileri iki ayrı IIS örneklerinde dağıtılan bir SignalR uygulamayı dağıtmak üzere.</span><span class="sxs-lookup"><span data-stu-id="a8d24-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="a8d24-105">Redis bellek içi anahtar-değer deposudur.</span><span class="sxs-lookup"><span data-stu-id="a8d24-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="a8d24-106">Ayrıca, bir Mesajlaşma sistemi ile bir yayımlama/abone olma modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="a8d24-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="a8d24-107">SignalR Redis devre kartına ileti başka bir sunucuya iletmek için pub/sub özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a8d24-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="a8d24-108">Bu öğretici için üç sunucu kullanır:</span><span class="sxs-lookup"><span data-stu-id="a8d24-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="a8d24-109">Bir SignalR uygulamayı dağıtmak için kullanacağınız Windows çalıştıran iki sunucu.</span><span class="sxs-lookup"><span data-stu-id="a8d24-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="a8d24-110">Redis çalışmaya kullanacağı Linux çalıştıran bir sunucu.</span><span class="sxs-lookup"><span data-stu-id="a8d24-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="a8d24-111">Bu öğreticideki ekran görüntüleri için Ubuntu 12.04 TLS kullandım.</span><span class="sxs-lookup"><span data-stu-id="a8d24-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="a8d24-112">Kullanmak için üç fiziksel sunucu yoksa, Hyper-V VM'ler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d24-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="a8d24-113">Azure'da VM'ler oluşturmanızı başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="a8d24-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="a8d24-114">Bu öğreticide resmi Redis uygulama kullansa da, de mevcuttur bir [, Windows bağlantı noktası Redis](https://github.com/MSOpenTech/redis) MSOpenTech öğesinden.</span><span class="sxs-lookup"><span data-stu-id="a8d24-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="a8d24-115">Kurulum ve yapılandırma farklıdır, ancak Aksi halde adımlar aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d24-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a8d24-116">Redis ile SignalR ölçeğini genişletme için Redis kümelerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a8d24-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="a8d24-117">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a8d24-117">Overview</span></span>

<span data-ttu-id="a8d24-118">Ayrıntılı Öğreticisine aldığımız önce ne yapacağını, hızlı bir genel bakış aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a8d24-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="a8d24-119">Redis yükleyin ve Redis sunucuyu başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="a8d24-120">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8d24-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="a8d24-121">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="a8d24-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="a8d24-122">Microsoft.AspNet.SignalR.Redis</span><span class="sxs-lookup"><span data-stu-id="a8d24-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="a8d24-123">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d24-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="a8d24-124">Devre kartına yapılandırmak için Global.asax için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8d24-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="a8d24-125">Ubuntu üzerinde Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a8d24-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="a8d24-126">Windows Hyper-V kullanarak, Windows Server üzerinde bir Ubuntu VM kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d24-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="a8d24-127">Ubuntu ISO'dan indirme [ http://www.ubuntu.com ](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="a8d24-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="a8d24-128">Hyper-V, yeni bir sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d24-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="a8d24-129">İçinde **Sanal Sabit Disk Bağla** adım, select **sanal sabit disk oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a8d24-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="a8d24-130">İçinde **yükleme seçenekleri** adım seçin **görüntü dosyası (.iso)**, tıklayın **Gözat**, Ubuntu yükleme ISO göz atın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="a8d24-131">Redis'i yükleme</span><span class="sxs-lookup"><span data-stu-id="a8d24-131">Install Redis</span></span>

<span data-ttu-id="a8d24-132">Bölümündeki adımları [ http://redis.io/download ](http://redis.io/download) indirip Redis oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d24-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="a8d24-133">Bu Redis ikili değerlerini oluşturur `src` dizin.</span><span class="sxs-lookup"><span data-stu-id="a8d24-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="a8d24-134">Varsayılan olarak, Redis, parola gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="a8d24-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="a8d24-135">Bir parola ayarlamak için Düzenle `redis.conf` kaynak kodunun kök dizininde bulunan dosya.</span><span class="sxs-lookup"><span data-stu-id="a8d24-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="a8d24-136">(Düzenlemeden önce dosyasının yedek bir kopyasını olun!) Eklemek için aşağıdaki yönerge `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="a8d24-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="a8d24-137">Redis Sunucu Şimdi Başlat:</span><span class="sxs-lookup"><span data-stu-id="a8d24-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="a8d24-138">Redis varsayılan bağlantı noktası olan açık 6379 bağlantı noktasının, üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="a8d24-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="a8d24-139">(Yapılandırma dosyasındaki bağlantı noktası numarasını değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="a8d24-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="a8d24-140">SignalR uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8d24-140">Create the SignalR Application</span></span>

<span data-ttu-id="a8d24-141">Bir SignalR uygulaması ya da bu öğreticileri izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a8d24-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="a8d24-142">SignalR ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a8d24-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="a8d24-143">SignalR ve MVC 4 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a8d24-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="a8d24-144">Ardından, biz sohbet uygulaması, Redis ile ölçeğini genişletme destekleyecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d24-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="a8d24-145">İlk olarak, SignalR.Redis NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d24-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="a8d24-146">Visual Studio'da gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="a8d24-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a8d24-147">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="a8d24-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="a8d24-148">Ardından, Global.asax dosyası açın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="a8d24-149">Aşağıdaki kodu ekleyin **uygulama\_Başlat** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a8d24-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="a8d24-150">"server" Redis'ı çalıştıran sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d24-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="a8d24-151">*bağlantı noktası* bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="a8d24-151">*port* is the port number</span></span>
- <span data-ttu-id="a8d24-152">"password" redis.conf dosyasında tanımlanan bir paroladır.</span><span class="sxs-lookup"><span data-stu-id="a8d24-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="a8d24-153">"AppName" herhangi bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="a8d24-153">"AppName" is any string.</span></span> <span data-ttu-id="a8d24-154">SignalR bu ada sahip bir Redis pub/sub kanalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8d24-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="a8d24-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a8d24-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="a8d24-156">Dağıtma ve uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a8d24-156">Deploy and Run the Application</span></span>

<span data-ttu-id="a8d24-157">SignalR uygulamayı dağıtmak için Windows Server örneklerinizin hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="a8d24-158">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d24-158">Add the IIS role.</span></span> <span data-ttu-id="a8d24-159">WebSocket Protokolü dahil olmak üzere "Uygulama geliştirme" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a8d24-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="a8d24-160">Yönetim Hizmeti ("Yönetim Araçları" altında listelenen) de içerir.</span><span class="sxs-lookup"><span data-stu-id="a8d24-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="a8d24-161">**Yükleme Web dağıtımı 3.0.**</span><span class="sxs-lookup"><span data-stu-id="a8d24-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="a8d24-162">IIS Yöneticisi'ni çalıştırın, Microsoft Web Platformu'nu yüklemenizi ister veya yapabilecekleriniz [yükleyiciyi indirin](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="a8d24-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="a8d24-163">Platform Yükleyicisi'nde, Web dağıtımı için arama ve Web dağıtımı 3.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="a8d24-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="a8d24-164">Web yönetimi hizmeti çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d24-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="a8d24-165">Aksi durumda, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-165">If not, start the service.</span></span> <span data-ttu-id="a8d24-166">(Web yönetimi hizmeti Windows Hizmetleri listede görmüyorsanız, IIS rolü eklendiğinde yönetim Hizmeti'nin yüklü emin olun.)</span><span class="sxs-lookup"><span data-stu-id="a8d24-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="a8d24-167">Varsayılan olarak, Web yönetimi hizmeti 8172 numaralı TCP bağlantı noktasını dinler.</span><span class="sxs-lookup"><span data-stu-id="a8d24-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="a8d24-168">Windows Güvenlik Duvarı'nda 8172 numaralı bağlantı noktasındaki TCP trafiğine izin veren yeni bir gelen kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d24-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="a8d24-169">Daha fazla bilgi için [güvenlik duvarı kurallarını yapılandırma](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d24-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="a8d24-170">(Azure Vm'lerinde barındırıyorsanız, doğrudan Azure Portalı'nda bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d24-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="a8d24-171">Bkz: [bir sanal makineye uç noktaları ayarlama](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="a8d24-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="a8d24-172">Geliştirme makinenizde Visual Studio projesinden sunucusuna dağıtmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a8d24-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="a8d24-173">Çözüm Gezgini'nde çözüme sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="a8d24-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="a8d24-174">Belgeler web dağıtımı hakkında daha fazla ayrıntılı için bkz [Visual Studio ve ASP.NET için Web dağıtımı içerik haritası](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="a8d24-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="a8d24-175">İki sunucu için uygulama dağıtıyorsanız, her örnek bir ayrı bir tarayıcı penceresi açın ve her SignalR iletileri diğer aldığınız bakın.</span><span class="sxs-lookup"><span data-stu-id="a8d24-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="a8d24-176">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına sit.)</span><span class="sxs-lookup"><span data-stu-id="a8d24-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="a8d24-177">Redis için kullanabileceğiniz gönderilen iletileri görmek merak ediyorsanız **redis-cli** istemcisi, Redis ile yükler.</span><span class="sxs-lookup"><span data-stu-id="a8d24-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
