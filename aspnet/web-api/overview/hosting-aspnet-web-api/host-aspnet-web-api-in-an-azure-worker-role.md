---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Ana bilgisayar ASP.NET Web API 2 Azure çalışan rolünde - ASP.NET 4.x
author: MikeWasson
description: "Öğretici: OWIN barındırma Web API çerçevesini kullanarak bir Azure çalışan rolünde ASP.NET Web API'si barındırın."
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: bfb23aafb814010e8651965dad91ca20a37fd786
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404630"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="93725-103">ASP.NET Web API 2 Azure çalışan rolünde barındırın</span><span class="sxs-lookup"><span data-stu-id="93725-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="93725-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="93725-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="93725-105">Bu öğreticide bir Azure çalışan rolünde ASP.NET Web API'yi barındırmak nasıl OWIN barındırma Web API çerçevesi kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="93725-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="93725-106">[.NET için açık Web arabirimi](http://owin.org/) (OWIN) .NET web sunucuları ve web uygulaması arasında bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="93725-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="93725-107">OWIN ayırır OWIN kendi işleminizde IIS dışında bir web uygulaması kendi kendine barındırma için ideal hale getirir sunucu web uygulamasından – Örneğin, bir Azure çalışan rolü içinde.</span><span class="sxs-lookup"><span data-stu-id="93725-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="93725-108">Bu öğreticide, Microsoft.Owin.Host.HttpListener paket kullanacağınız, bir HTTP sunucusu sağlayan Self OWIN uygulamalarını barındırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="93725-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="93725-109">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="93725-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="93725-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="93725-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="93725-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="93725-111">Web API 2</span></span>
> - [<span data-ttu-id="93725-112">.NET 2.3 için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="93725-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="93725-113">Microsoft Azure projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="93725-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="93725-114">Visual Studio'yu yönetici ayrıcalıklarıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="93725-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="93725-115">Azure işlem öykünücüsü kullanarak uygulamayı yerel olarak hata ayıklama için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="93725-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="93725-116">Üzerinde **dosya** menüsünde tıklayın **yeni**, ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="93725-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="93725-117">Gelen **yüklü şablonlar**, Visual C# altında tıklayın **bulut** ve ardından **Windows Azure bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="93725-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="93725-118">"AzureApp" Projeyi adlandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="93725-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="93725-119">İçinde **yeni Windows Azure bulut hizmeti** iletişim kutusunda, çift **çalışan rolü**.</span><span class="sxs-lookup"><span data-stu-id="93725-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="93725-120">("WorkerRole1") varsayılan adı bırakın.</span><span class="sxs-lookup"><span data-stu-id="93725-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="93725-121">Bu adım, bir çalışan rolü çözüme ekler.</span><span class="sxs-lookup"><span data-stu-id="93725-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="93725-122">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="93725-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="93725-123">Oluşturulan Visual Studio çözümünü iki proje içerir:</span><span class="sxs-lookup"><span data-stu-id="93725-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="93725-124">&quot;AzureApp&quot; Azure uygulaması için yapılandırma ve rolleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="93725-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="93725-125">&quot;WorkerRole1&quot; çalışan rolü kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="93725-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="93725-126">Genel olarak, bu öğreticide tek bir rol olsa da Azure uygulaması birden çok rol içerebilir.</span><span class="sxs-lookup"><span data-stu-id="93725-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="93725-127">Web API ve OWIN paketleri Ekle</span><span class="sxs-lookup"><span data-stu-id="93725-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="93725-128">Gelen **Araçları** menüsünde tıklayın **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="93725-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="93725-129">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="93725-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="93725-130">Bir HTTP uç noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="93725-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="93725-131">Çözüm Gezgini'nde AzureApp projeyi genişletin.</span><span class="sxs-lookup"><span data-stu-id="93725-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="93725-132">Rolleri düğümünü genişletin, WorkerRole1 sağ tıklatın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="93725-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="93725-133">Tıklayın **uç noktaları**ve ardından **uç nokta Ekle**.</span><span class="sxs-lookup"><span data-stu-id="93725-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="93725-134">İçinde **Protokolü** açılan listeyi seçin "http".</span><span class="sxs-lookup"><span data-stu-id="93725-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="93725-135">İçinde **genel bağlantı noktası** ve **özel bağlantı noktası**, 80 yazın.</span><span class="sxs-lookup"><span data-stu-id="93725-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="93725-136">Bu bağlantı noktası numaraları farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="93725-136">These port numbers can be different.</span></span> <span data-ttu-id="93725-137">Role bir isteği gönderdiğinizde istemciler kullandıklarınız genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="93725-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="93725-138">Web API'si için yapılandırma barındırma</span><span class="sxs-lookup"><span data-stu-id="93725-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="93725-139">Çözüm Gezgini'nde WorkerRole1 projeyi sağ tıklatın ve seçin **Ekle** / **sınıfı** yeni bir sınıf eklemek için.</span><span class="sxs-lookup"><span data-stu-id="93725-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="93725-140">Sınıf adını `Startup`.</span><span class="sxs-lookup"><span data-stu-id="93725-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="93725-141">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="93725-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="93725-142">Web API denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="93725-142">Add a Web API Controller</span></span>

<span data-ttu-id="93725-143">Ardından, bir Web API denetleyici sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="93725-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="93725-144">WorkerRole1 projeye sağ tıklayıp **Ekle** / **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="93725-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="93725-145">TestController sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="93725-145">Name the class TestController.</span></span> <span data-ttu-id="93725-146">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="93725-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="93725-147">Kolaylık olması için bu denetleyici yalnızca düz metin döndürür iki GET yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="93725-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="93725-148">OWIN konağını Başlat</span><span class="sxs-lookup"><span data-stu-id="93725-148">Start the OWIN Host</span></span>

<span data-ttu-id="93725-149">WorkerRole.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="93725-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="93725-150">Bu sınıf, çalışan rolü başlatıldığında ve durdurulduğunda çalışan kodu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="93725-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="93725-151">Aşağıdaki using deyimi:</span><span class="sxs-lookup"><span data-stu-id="93725-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="93725-152">Ekleme bir **IDisposable** üyesine `WorkerRole` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="93725-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="93725-153">İçinde `OnStart` yöntemi, ana bilgisayarı başlatmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="93725-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="93725-154">**WebApp.Start** yöntemi OWIN ana bilgisayarı başlatır.</span><span class="sxs-lookup"><span data-stu-id="93725-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="93725-155">Adını `Startup` yöntem bir tür parametresine bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="93725-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="93725-156">Kural gereği, konak çağıracak `Configure` bu sınıfın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="93725-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="93725-157">Geçersiz kılma `OnStop` elden çıkarmak  *\_uygulama* örneği:</span><span class="sxs-lookup"><span data-stu-id="93725-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="93725-158">WorkerRole.cs için tam kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="93725-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="93725-159">Çözümü derleyin ve uygulamayı Azure işlem öykünücüsü'nde yerel olarak çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="93725-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="93725-160">Güvenlik duvarı ayarlarınıza bağlı olarak, güvenlik duvarı üzerinden öykünücü izin gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="93725-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="93725-161">Lütfen aşağıdaki gibi bir özel durum alırsanız bkz [bu blog gönderisini](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) geçici bir çözüm için.</span><span class="sxs-lookup"><span data-stu-id="93725-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="93725-162">"Dosyası veya bütünleştirilmiş kod yüklenemedi ' Microsoft.Owin, sürüm 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri.</span><span class="sxs-lookup"><span data-stu-id="93725-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="93725-163">Bildirim tanımı bulunduğu derlemenin, derleme başvurusunu eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="93725-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="93725-164">(HRESULT özel durum döndürdü: 0x80131040)"</span><span class="sxs-lookup"><span data-stu-id="93725-164">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="93725-165">İşlem öykünücüsü, uç nokta için bir yerel IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="93725-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="93725-166">IP adresi, işlem öykünücüsü kullanıcı Arabiriminde görüntüleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93725-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="93725-167">Görev çubuğu bildirim alanında bulunan öykünücü simgesine sağ tıklayın ve seçin **Göster işlem öykünücüsü kullanıcı Arabiriminde**.</span><span class="sxs-lookup"><span data-stu-id="93725-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="93725-168">IP adresi hizmet dağıtımları, dağıtım [ID] hizmet ayrıntıları altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93725-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="93725-169">Bir web tarayıcısı açın ve http:// gidin<em>adresi</em>/test/1, burada <em>adresi</em> ; işlem öykünücüsü tarafından atanan IP adresi gibi `http://127.0.0.1:80/test/1`.</span><span class="sxs-lookup"><span data-stu-id="93725-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="93725-170">Web API denetleyicisi yanıtı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="93725-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="93725-171">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="93725-171">Deploy to Azure</span></span>

<span data-ttu-id="93725-172">Bu adım için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="93725-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="93725-173">Zaten yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93725-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="93725-174">Ayrıntılar için bkz [Microsoft Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="93725-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="93725-175">Çözüm Gezgini'nde AzureApp projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93725-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="93725-176">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="93725-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="93725-177">Azure hesabınızda oturum açmadınız tıklatmak **oturum**.</span><span class="sxs-lookup"><span data-stu-id="93725-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="93725-178">Oturum açtıktan sonra bir abonelik seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="93725-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="93725-179">Bulut hizmeti için bir ad girin ve bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="93725-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="93725-180">**Oluştur**'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="93725-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="93725-181">Tıklayın **yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="93725-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="93725-182">Azure Etkinlik Günlüğü penceresini dağıtımın ilerleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="93725-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="93725-183">Uygulama dağıtıldığında, Gözat http://appname.cloudapp.net/test/1.</span><span class="sxs-lookup"><span data-stu-id="93725-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="93725-184">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="93725-184">Additional Resources</span></span>

- [<span data-ttu-id="93725-185">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="93725-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="93725-186">Github'da Katana proje</span><span class="sxs-lookup"><span data-stu-id="93725-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
