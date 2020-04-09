---
uid: mvc/overview/deployment/docker-aspnetmvc
title: ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme
description: Varolan bir ASP.NET MVC uygulamasını nasıl alıp Windows Docker Kapsayıcısı'nda çalıştırılamayı öğrenin
keywords: Windows Kapsayıcılar,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675189"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="136d6-104">ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme</span><span class="sxs-lookup"><span data-stu-id="136d6-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="136d6-105">Varolan bir .NET Framework tabanlı uygulamayı bir Windows kapsayıcısında çalıştırmak için uygulamanızda herhangi bir değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="136d6-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="136d6-106">Uygulamanızı bir Windows kapsayıcısında çalıştırmak için uygulamanızı içeren bir Docker görüntüsü oluşturun ve kapsayıcıyı başlatın.</span><span class="sxs-lookup"><span data-stu-id="136d6-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="136d6-107">Bu konu, varolan bir [ASP.NET MVC uygulamasının](http://www.asp.net/mvc) nasıl alınıp bir Windows kapsayıcısında dağıtılanın açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="136d6-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="136d6-108">Varolan bir ASP.NET MVC uygulamasıyla başlarsınız, ardından Visual Studio'yu kullanarak yayımlanmış varlıkları oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="136d6-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="136d6-109">Uygulamanızı içeren ve çalıştıran resmi oluşturmak için Docker'ı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="136d6-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="136d6-110">Windows kapsayıcısında çalışan siteye göz atar ve uygulamanın çalıştığını doğrularsınız.</span><span class="sxs-lookup"><span data-stu-id="136d6-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="136d6-111">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="136d6-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="136d6-112">[Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="136d6-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="136d6-113">Bir kapta çalıştıracağınız uygulama, soruları rasgele yanıtlayan basit bir web sitesidir.</span><span class="sxs-lookup"><span data-stu-id="136d6-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="136d6-114">Bu uygulama hiçbir kimlik doğrulama veya veritabanı depolama ile temel bir MVC uygulamasıdır; web katmanını bir kapsayıcıya taşımaya odaklanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="136d6-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="136d6-115">Gelecekteki konular, kapsayıcı laştırılmış uygulamalarda kalıcı depolamanın nasıl taşınacağını ve yöneteceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="136d6-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="136d6-116">Uygulamanızı taşımak şu adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="136d6-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="136d6-117">Görüntü için varlıkları oluşturmak için bir yayımlama görevi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="136d6-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="136d6-118">Uygulamanızı çalıştıracak bir Docker görüntüsü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="136d6-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="136d6-119">Resminizi çalıştıran bir Docker kapsayıcısı başlatma.</span><span class="sxs-lookup"><span data-stu-id="136d6-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="136d6-120">Tarayıcınızı kullanarak uygulamayı doğrulama.</span><span class="sxs-lookup"><span data-stu-id="136d6-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="136d6-121">[Tamamlanan uygulama](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) GitHub'da.</span><span class="sxs-lookup"><span data-stu-id="136d6-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="136d6-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="136d6-122">Prerequisites</span></span>

<span data-ttu-id="136d6-123">Geliştirme makinesi aşağıdaki yazılıma sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="136d6-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="136d6-124">[Windows 10 Yıldönümü Güncelleştirmesi](https://www.microsoft.com/software-download/windows10/) (veya üstü) veya [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (veya daha yüksek)</span><span class="sxs-lookup"><span data-stu-id="136d6-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="136d6-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - sürüm Kararlı 1.13.0 veya 1.12 Beta 26 (veya daha yeni sürümler)</span><span class="sxs-lookup"><span data-stu-id="136d6-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="136d6-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="136d6-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="136d6-127">Windows Server 2016 kullanıyorsanız, Kapsayıcı [Ana Bilgisayar Dağıtımı - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="136d6-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="136d6-128">Docker’ı yükleyip başlattıktan sonra tepsi simgesine sağ tıklayıp **Windows kapsayıcılarına geç** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="136d6-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="136d6-129">Bu işlem, Windows temelinde Docker görüntülerini çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="136d6-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="136d6-130">Bu komutun yürütülmesi birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="136d6-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="136d6-131">![Windows Kapsayıcı][windows-container]</span><span class="sxs-lookup"><span data-stu-id="136d6-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="136d6-132">Komut dosyası yayımlama</span><span class="sxs-lookup"><span data-stu-id="136d6-132">Publish script</span></span>

<span data-ttu-id="136d6-133">Bir Docker görüntüsüne yüklemeniz gereken tüm varlıkları tek bir yerde toplayın.</span><span class="sxs-lookup"><span data-stu-id="136d6-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="136d6-134">Uygulamanız için bir yayımlama profili oluşturmak için Visual Studio **Publish** komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="136d6-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="136d6-135">Bu profil, daha sonra bu öğreticide hedef resminize kopyaladığınız tüm varlıkları tek bir dizin ağacına koyar.</span><span class="sxs-lookup"><span data-stu-id="136d6-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="136d6-136">**Adımları Yayımla**</span><span class="sxs-lookup"><span data-stu-id="136d6-136">**Publish Steps**</span></span>

1. <span data-ttu-id="136d6-137">Visual Studio'daki web projesine sağ tıklayın ve **Yayımla'yı**seçin.</span><span class="sxs-lookup"><span data-stu-id="136d6-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="136d6-138">Özel **profil düğmesini**tıklatın ve ardından yöntem olarak **Dosya Sistemi'ni** seçin.</span><span class="sxs-lookup"><span data-stu-id="136d6-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="136d6-139">Dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="136d6-139">Choose the directory.</span></span> <span data-ttu-id="136d6-140">Kurallara göre, indirilen `bin\Release\PublishOutput`örnek kullanır.</span><span class="sxs-lookup"><span data-stu-id="136d6-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="136d6-141">![Bağlantı Yayımla][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="136d6-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="136d6-142">**Ayarlar** sekmesinin **Dosya Yayımlama Seçenekleri** bölümünü açın. **Yayımlama sırasında Precompile'yi**seçin.</span><span class="sxs-lookup"><span data-stu-id="136d6-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="136d6-143">Bu optimizasyon, Docker kapsayıcısında görünümleri derlettiğiniz, önceden derlenmiş görünümleri kopyaladığınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="136d6-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="136d6-144">![Ayarları Yayımla][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="136d6-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="136d6-145">**Yayımla'yı**tıklatın ve Visual Studio gerekli tüm varlıkları hedef klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="136d6-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="136d6-146">Görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="136d6-146">Build the image</span></span>

<span data-ttu-id="136d6-147">Docker resminizi tanımlamak için *Dockerfile* adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="136d6-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="136d6-148">*Dockerfile* son görüntüyü oluşturmak için talimatlar içerir ve herhangi bir temel görüntü adları, gerekli bileşenleri, çalıştırmak istediğiniz uygulama ve diğer yapılandırma görüntüleri içerir.</span><span class="sxs-lookup"><span data-stu-id="136d6-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="136d6-149">*Dockerfile* görüntüyü oluşturan `docker build` komuta giriştir.</span><span class="sxs-lookup"><span data-stu-id="136d6-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="136d6-150">Bu alıştırma için, Docker `microsoft/aspnet` [Hub'da](https://hub.docker.com/r/microsoft/aspnet/)bulunan görüntüye dayalı bir görüntü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="136d6-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="136d6-151">Temel görüntü, `microsoft/aspnet`bir Windows Server görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="136d6-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="136d6-152">Windows Server Core, IIS ve 4.7.2 ASP.NET içerir.</span><span class="sxs-lookup"><span data-stu-id="136d6-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="136d6-153">Bu resmi kapsayıcınızda çalıştırdığınızda, otomatik olarak IIS ve yüklü web siteleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="136d6-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="136d6-154">Resminizi oluşturan Dockerfile aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="136d6-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="136d6-155">Bu Dockerfile içinde bir `ENTRYPOINT` komutu yoktur.</span><span class="sxs-lookup"><span data-stu-id="136d6-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="136d6-156">Gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="136d6-156">You don't need one.</span></span> <span data-ttu-id="136d6-157">IIS ile Windows Server çalıştırırken, IIS işlemi aspnet temel görüntüde başlamak üzere yapılandırılan giriş noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="136d6-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="136d6-158">ASP.NET uygulamanızı çalıştıran görüntüyü oluşturmak için Docker build komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="136d6-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="136d6-159">Bunu yapmak için, projenizin dizininde bir PowerShell penceresi açın ve çözüm dizinine aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="136d6-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="136d6-160">Bu komut, Dockerfile'nizdeki yönergeleri kullanarak yeni görüntüyü oluşturur ve görüntüyü mvcrandomanswers olarak adlandır (-t etiketleme) verir.</span><span class="sxs-lookup"><span data-stu-id="136d6-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="136d6-161">Bu, temel görüntüyü [Docker Hub'dan](http://hub.docker.com)çekmeyi ve uygulamanızı bu resme eklemeyi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="136d6-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="136d6-162">Bu komut tamamlandıktan sonra, `docker images` yeni görüntü hakkındaki bilgileri görmek için komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="136d6-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="136d6-163">GÖRÜNTÜ Kimliği makinenizde farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="136d6-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="136d6-164">Şimdi, uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="136d6-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="136d6-165">Bir kapsayıcı başlatma</span><span class="sxs-lookup"><span data-stu-id="136d6-165">Start a container</span></span>

<span data-ttu-id="136d6-166">Aşağıdaki `docker run` komutu çalıştırarak bir kapsayıcı başlatın:</span><span class="sxs-lookup"><span data-stu-id="136d6-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="136d6-167">Bağımsız `-d` değişken, Docker'a görüntüyü müstakil modda başlatmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="136d6-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="136d6-168">Bu, Docker görüntüsünün geçerli kabuktan bağlantısının kesildiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="136d6-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="136d6-169">Birçok docker örneğinde, -p konteyner ve ana bağlantı noktaları harita görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="136d6-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="136d6-170">Varsayılan aspnet görüntüsü, konteyneri 80 bağlantı noktasında niçin dinleyecek ve ortaya çıkaracak şekilde yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="136d6-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="136d6-171">Çalışan `--name randomanswers` kapsayıcıya bir ad verir.</span><span class="sxs-lookup"><span data-stu-id="136d6-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="136d6-172">Çoğu komutta kapsayıcı kimliği yerine bu adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="136d6-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="136d6-173">Başletmek `mvcrandomanswers` için görüntünün adıdır.</span><span class="sxs-lookup"><span data-stu-id="136d6-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="136d6-174">Tarayıcıda doğrula</span><span class="sxs-lookup"><span data-stu-id="136d6-174">Verify in the browser</span></span>

<span data-ttu-id="136d6-175">Kapsayıcı başladıktan sonra, gösterilen örnekte kullanarak `http://localhost` çalışan kapsayıcıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="136d6-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="136d6-176">Bu URL'yi tarayıcınıza yazın ve çalışan siteyi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="136d6-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="136d6-177">Bazı VPN veya proxy yazılımları sitenizde gezinmenizi engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="136d6-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="136d6-178">Kapsayıcınızın çalıştığından emin olmak için geçici olarak devre dışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="136d6-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="136d6-179">GitHub'daki örnek dizini, bu komutları sizin için yürüten bir [PowerShell komut dosyası](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) içerir.</span><span class="sxs-lookup"><span data-stu-id="136d6-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="136d6-180">PowerShell penceresi açın, çözüm dizininizde dizin değiştirin ve yazın:</span><span class="sxs-lookup"><span data-stu-id="136d6-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="136d6-181">Yukarıdaki komut görüntüyü oluşturur, makinenizdeki görüntülerin listesini görüntüler ve bir kapsayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="136d6-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="136d6-182">Kapsayıcınızı durdurmak için `docker stop` bir komut sorun:</span><span class="sxs-lookup"><span data-stu-id="136d6-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="136d6-183">Kapsayıcıyı kaldırmak için `docker rm` bir komut düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="136d6-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows Kapsayıcısına Geçiş"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Dosya Sistemine Yayımla"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Ayarları Yayımla"
