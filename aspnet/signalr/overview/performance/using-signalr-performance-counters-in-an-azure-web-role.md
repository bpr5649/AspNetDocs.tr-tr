---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure Web rolünde SignalR performans sayaçlarını kullanma | Microsoft Docs
author: guardrex
description: Azure Web rolünde SignalR performans sayaçlarını yüklemek ve kullanmak.
keywords: ASP. NET, SignalR, performans sayacı, Azure Web rolü
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240647"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="09ea0-104">Azure Web rolünde SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="09ea0-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="09ea0-105">[Luke Latham](https://github.com/guardrex) tarafından</span><span class="sxs-lookup"><span data-stu-id="09ea0-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="09ea0-106">SignalR performans sayaçları, uygulamanızın performansını bir Azure Web rolünde izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="09ea0-107">Sayaçlar Microsoft Azure Tanılama tarafından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="09ea0-108">Azure 'da SignalR performans sayaçlarını, tek başına veya şirket içi uygulamalar için kullanılan aynı aracı *signalr.exe*ile birlikte yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="09ea0-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="09ea0-109">Azure rolleri geçici olduğundan, bir uygulamayı başlangıçtan sonra SignalR performans sayaçlarını yükleyecek ve kaydedecek şekilde yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="09ea0-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09ea0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09ea0-110">Prerequisites</span></span>

* <span data-ttu-id="09ea0-111">Visual Studio 2015 veya [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="09ea0-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="09ea0-112">[Visual Studio için MICROSOFT Azure SDK](https://azure.microsoft.com/downloads/) 'sı **: SDK 'yı yükledikten sonra makinenizi yeniden başlatın.**</span><span class="sxs-lookup"><span data-stu-id="09ea0-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="09ea0-113">Microsoft Azure abonelik: ücretsiz bir Azure deneme hesabına kaydolmak Için bkz. [Azure Ücretsiz deneme](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="09ea0-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="09ea0-114">SignalR performans sayaçlarını kullanıma sunan bir Azure Web rolü uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="09ea0-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="09ea0-115">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="09ea0-116">Visual Studio 'da **Dosya**  >  **Yeni**  >  **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="09ea0-117">**Yeni proje** iletişim kutusunda, sol taraftaki **Visual C#**  >  **bulut** kategorisini seçin ve ardından **Azure bulut hizmeti** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="09ea0-118">Uygulamayı **Signalrperfcounters** olarak adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![Yeni bulut uygulaması](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="09ea0-120">**Bulut** şablonu kategorisini veya **Azure bulut hizmeti** şablonunu görmüyorsanız, Visual Studio 2017 için **Azure geliştirme** iş yükünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="09ea0-121">Visual Studio Yükleyicisi açmak için **Yeni proje** iletişim kutusunun sol alt tarafındaki **Visual Studio yükleyicisi aç** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="09ea0-122">**Azure geliştirme** iş yükünü seçin ve sonra iş yükünü yüklemeye başlamak için **Değiştir** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio Yükleyicisi Azure geliştirme iş yükü](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="09ea0-124">**Yeni Microsoft Azure bulut hizmeti** iletişim kutusunda **ASP.NET Web rolü** ' nü seçin ve rolü projeye eklemek için > düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="09ea0-125">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-125">Select **OK**.</span></span>

   ![ASP.NET Web rolü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="09ea0-127">**Yeni ASP.NET Web uygulaması-WebRole1** Iletişim kutusunda **MVC** şablonunu seçin ve ardından **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC ve Web API 'SI ekleme](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="09ea0-129">**Çözüm Gezgini**' de, **WebRole1**altında *Diagnostics. wadcfgx* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![Çözüm Gezgini Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="09ea0-131">Dosyanın içeriğini aşağıdaki yapılandırmayla değiştirin ve dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="09ea0-132">**Araçlar**NuGet Paket Yöneticisi ' nden **Paket Yöneticisi konsolunu** açın  >  **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="09ea0-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="09ea0-133">SignalR 'nin en son sürümünü ve SignalR yardımcı programları paketini yüklemek için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="09ea0-134">Uygulamayı başlatıldığında veya geri dönüştürüldüğünde, SignalR performans sayaçlarını rol örneğine yükleyecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="09ea0-135">**Çözüm Gezgini**, **WebRole1** projesine sağ tıklayın ve **Add**  >  **Yeni klasör**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="09ea0-136">Yeni klasör *başlangıcını*adlandırın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-136">Name the new folder *Startup*.</span></span>

   ![Başlangıç klasörü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="09ea0-138">*signalr.exe* dosyasını ( **Microsoft. Aspnet. SignalR. utils** paketiyle eklenen) \<project folder> /SignalRPerfCounters/Packages/Microsoft.Aspnet.SignalR.utils. \<version> adresinden kopyalayın /Tools önceki adımda oluşturduğunuz *Başlangıç* klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="09ea0-139">**Çözüm Gezgini**, *Başlangıç* klasörüne sağ tıklayın ve **Add**  >  **Varolan öğe**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="09ea0-140">Görüntülenen iletişim kutusunda *signalr.exe* ' ı seçin ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Projeye signalr.exe Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="09ea0-142">Oluşturduğunuz *Başlangıç* klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="09ea0-143">**Add**  >  **Yeni öğe**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="09ea0-144">**Genel** düğümünü seçin, **metin dosyası**' nı seçin ve yeni öğe *signalrperfcounterınstall. cmd*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="09ea0-145">Bu komut dosyası, SignalR performans sayaçlarını Web rolüne yükler.</span><span class="sxs-lookup"><span data-stu-id="09ea0-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR performans sayacı yüklemesi toplu iş dosyası oluşturma](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="09ea0-147">Visual Studio, *Signalrperfcounterınstall. cmd* dosyasını oluşturduğunda ana pencerede otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="09ea0-148">Dosyanın içeriğini aşağıdaki komut dosyasıyla değiştirin, sonra dosyayı kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="09ea0-149">Bu betik, SignalR performans sayaçlarını rol örneğine ekleyen *signalr.exe*yürütülür.</span><span class="sxs-lookup"><span data-stu-id="09ea0-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="09ea0-150">**Çözüm Gezgini** *signalr.exe* dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="09ea0-151">Dosyanın **özelliklerinde**, **her zaman kopyalamak**için **Çıkış Dizinine Kopyala** ' yı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![Her zaman kopyalamak için çıkış dizinine Kopyala ayarla](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="09ea0-153">*Signalrperfcounterınstall. cmd* dosyası için önceki adımı tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="09ea0-154">*Signalrperfcounterınstall. cmd* dosyasına sağ tıklayın ve **birlikte Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="09ea0-155">Görüntülenen iletişim kutusunda **Ikili düzenleyici** ' yi seçin ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![Ikili düzenleyiciyle aç](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="09ea0-157">İkili düzenleyicide, dosyadaki önde gelen baytları seçin ve silin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="09ea0-158">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-158">Save and close the file.</span></span>

    ![Baştaki baytları Sil](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="09ea0-160">*ServiceDefinition. csdef* ' i açın ve hizmet başlatıldığında *Signalrperfcounterınstall. cmd* dosyasını yürüten bir başlangıç görevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="09ea0-161">`Views/Shared/_Layout.cshtml`Dosya sonundan jQuery paket betiğini açın ve kaldırın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="09ea0-162">Sunucuda yöntemi sürekli çağıran bir JavaScript istemcisi ekleyin `increment` .</span><span class="sxs-lookup"><span data-stu-id="09ea0-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="09ea0-163">`Views/Home/Index.cshtml`İçeriğini açın ve şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="09ea0-164">**WebRole1** projesinde *hub 'lar*adlı yeni bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09ea0-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="09ea0-165">**Çözüm Gezgini** *hub* klasörüne sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="09ea0-166">**Yeni öğe Ekle** iletişim kutusunda, **Web**  >  **SignalR** kategorisini seçin ve ardından **SignalR hub sınıfı (v2)** öğe şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="09ea0-167">Yeni hub *MyHub.cs* ' ı adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![SignalR hub sınıfı yeni öğe Ekle iletişim kutusunda hub klasörüne ekleniyor](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="09ea0-169">*MyHub.cs* , ana pencerede otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="09ea0-170">İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:</span><span class="sxs-lookup"><span data-stu-id="09ea0-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="09ea0-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* , SignalR kod temeli ile birlikte sunulan bir bağlantı yoğunluğu test aracıdır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="09ea0-172">Crank kalıcı bir bağlantı gerektirdiğinden, test ederken kullanmak için sitenize bir tane ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="09ea0-173">**WebRole1** projesine *Persistentconnections*adlı yeni bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="09ea0-174">Bu klasöre sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**.</span><span class="sxs-lookup"><span data-stu-id="09ea0-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="09ea0-175">Yeni sınıf dosyasını *MyPersistentConnections.cs* olarak adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="09ea0-176">Visual Studio, *MyPersistentConnections.cs* dosyasını ana pencerede açar.</span><span class="sxs-lookup"><span data-stu-id="09ea0-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="09ea0-177">İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:</span><span class="sxs-lookup"><span data-stu-id="09ea0-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="09ea0-178">Sınıfını kullanarak `Startup` , OWıN başlatıldığında SignalR nesneleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="09ea0-179">*Startup.cs* açın veya oluşturun ve içeriğini şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="09ea0-180">Yukarıdaki kodda `OwinStartup` özniteliği, OWıN 'u başlatmak için bu sınıfı işaretler.</span><span class="sxs-lookup"><span data-stu-id="09ea0-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="09ea0-181">`Configuration`Yöntemi SignalR 'yi başlatır.</span><span class="sxs-lookup"><span data-stu-id="09ea0-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="09ea0-182">**F5**tuşuna basarak Microsoft Azure öykünücüsü uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="09ea0-183">**Mapsignalr**'de bir **fileloadexception** ile karşılaşırsanız *web.config* bağlama yeniden yönlendirmelerini aşağıdaki şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="09ea0-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="09ea0-184">Bir dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-184">Wait about one minute.</span></span> <span data-ttu-id="09ea0-185">Visual Studio 'da Cloud Explorer araç penceresini açın (**View**  >  **bulut Gezginini**görüntüleyin) ve yolu genişletin `(Local)/Storage Accounts/(Development)/Tables` .</span><span class="sxs-lookup"><span data-stu-id="09ea0-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="09ea0-186">**WADPerformanceCountersTable**çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="09ea0-187">Tablo verilerinde SignalR sayaçlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="09ea0-188">Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="09ea0-189">Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio Cloud Explorer 'da WAD performans sayaçları tablosunu seçme](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD performans sayaçları tablosunda toplanan sayaçları gösterme](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="09ea0-192">Uygulamanızı bulutta test etmek için, **ServiceConfiguration. Cloud. cscfg** dosyasını güncelleştirin ve öğesini `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` geçerli bir Azure depolama hesabı bağlantı dizesi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="09ea0-193">Uygulamayı Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="09ea0-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="09ea0-194">Bir uygulamayı Azure 'a dağıtma hakkında ayrıntılı bilgi için bkz. [bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="09ea0-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="09ea0-195">Birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="09ea0-195">Wait a few minutes.</span></span> <span data-ttu-id="09ea0-196">**Cloud Explorer**'da, yukarıda yapılandırdığınız depolama hesabını bulun ve `WADPerformanceCountersTable` içindeki tabloyu bulun.</span><span class="sxs-lookup"><span data-stu-id="09ea0-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="09ea0-197">Tablo verilerinde SignalR sayaçlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="09ea0-198">Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="09ea0-199">Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="09ea0-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="09ea0-200">Bu öğreticide kullanılan özgün içerik için özel [Marrichard](https://social.msdn.microsoft.com/profile/Martin+Richard) 'e teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="09ea0-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
