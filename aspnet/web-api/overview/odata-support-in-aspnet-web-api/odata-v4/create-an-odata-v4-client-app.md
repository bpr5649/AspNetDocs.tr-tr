---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 istemci uygulaması (C#) oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: 14d4b01a2ea8a4582294053416b626e7f1801b50
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59411520"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="b93a1-102">OData v4 İstemci Uygulaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="b93a1-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="b93a1-103">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b93a1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b93a1-104">Önceki öğreticide, temel CRUD işlemleri destekleyen bir OData hizmeti oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b93a1-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="b93a1-105">Artık bir istemci hizmeti için oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="b93a1-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="b93a1-106">Yeni bir Visual Studio örneği başlatın ve yeni bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b93a1-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="b93a1-107">İçinde **yeni proje** iletişim kutusunda **yüklü** &gt; **şablonları** &gt; **Visual C#** &gt; **Windows Masaüstü**seçip **konsol uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="b93a1-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="b93a1-108">Projeyi adlandırın &quot;ProductsApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="b93a1-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="b93a1-109">Ayrıca, OData hizmeti içeren aynı Visual Studio çözümünü konsol uygulaması ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b93a1-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>


## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="b93a1-110">OData istemci kodu oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="b93a1-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="b93a1-111">Gelen **Araçları** menüsünde **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="b93a1-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="b93a1-112">Seçin **çevrimiçi** &gt; **Visual Studio Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="b93a1-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="b93a1-113">Arama kutusuna arama &quot;OData istemci kodu Oluşturucu&quot;.</span><span class="sxs-lookup"><span data-stu-id="b93a1-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="b93a1-114">Tıklayın **indirme** VSIX'i yüklemek.</span><span class="sxs-lookup"><span data-stu-id="b93a1-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="b93a1-115">Visual Studio'yu yeniden başlatmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b93a1-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="b93a1-116">OData hizmeti yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b93a1-116">Run the OData Service Locally</span></span>

<span data-ttu-id="b93a1-117">Visual Studio'dan ProductService projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="b93a1-118">Varsayılan olarak, Visual Studio uygulama kökü için bir tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="b93a1-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="b93a1-119">URI dikkat edin. Bu sonraki adımda gerekir.</span><span class="sxs-lookup"><span data-stu-id="b93a1-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="b93a1-120">Uygulamasını çalışır durumda bırakın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="b93a1-121">Aynı çözüm içinde her iki proje yerleştirdiğinizde ProductService projeyi hata ayıklama olmadan çalıştırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="b93a1-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="b93a1-122">Sonraki adımda, konsol uygulama projesi değiştirme sırasında çalışan hizmeti tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b93a1-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>


## <a name="generate-the-service-proxy"></a><span data-ttu-id="b93a1-123">Hizmet proxy'si oluştur</span><span class="sxs-lookup"><span data-stu-id="b93a1-123">Generate the Service Proxy</span></span>

<span data-ttu-id="b93a1-124">Hizmet proxy'si OData hizmetine erişim yöntemleri tanımlayan bir .NET sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="b93a1-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="b93a1-125">Ara sunucu HTTP isteklerinin yöntemi çağrılarını çevirir.</span><span class="sxs-lookup"><span data-stu-id="b93a1-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="b93a1-126">Proxy sınıfı çalıştırarak oluşturacağınız bir [T4 şablonu](https://msdn.microsoft.com/library/bb126445.aspx).</span><span class="sxs-lookup"><span data-stu-id="b93a1-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="b93a1-127">Projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-127">Right-click the project.</span></span> <span data-ttu-id="b93a1-128">Seçin **ekleme** &gt; **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="b93a1-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="b93a1-129">İçinde **Yeni Öğe Ekle** iletişim kutusunda **Visual C# öğeleri** &gt; **kod** &gt; **OData istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="b93a1-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="b93a1-130">Şablon adı &quot;ProductClient.tt&quot;.</span><span class="sxs-lookup"><span data-stu-id="b93a1-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="b93a1-131">Tıklayın **Ekle** aracılığıyla güvenlik uyarısı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="b93a1-132">Bu noktada, siz görmezden gelmenizde bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b93a1-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="b93a1-133">Visual Studio, şablonu otomatik olarak çalışır, ancak bazı yapılandırma ayarları şablonun gerekir ilk.</span><span class="sxs-lookup"><span data-stu-id="b93a1-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="b93a1-134">ProductClient.odata.config dosyasını açın. İçinde `Parameter` öğesini ProductService projesi (önceki adımda) URI'SİNDEN yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="b93a1-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b93a1-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="b93a1-136">Şablonu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-136">Run the template again.</span></span> <span data-ttu-id="b93a1-137">Çözüm Gezgini'nde ProductClient.tt dosyasını sağ tıklatın ve seçin **özel aracı Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="b93a1-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="b93a1-138">Şablon proxy tanımlayan ProductClient.cs adlı bir kod dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b93a1-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="b93a1-139">OData uç noktasını değiştirirseniz, uygulamanızı geliştirirken, şablonun proxy güncelleştirmeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b93a1-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="b93a1-140">OData hizmeti çağırmak amacıyla hizmet proxy'si kullanın</span><span class="sxs-lookup"><span data-stu-id="b93a1-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="b93a1-141">Program.cs dosyasını açın ve ortak kod aşağıdakiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b93a1-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="b93a1-142">Değiştirin *serviceUri* hizmet URI'si ile daha önce.</span><span class="sxs-lookup"><span data-stu-id="b93a1-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="b93a1-143">Uygulamayı çalıştırdığınızda, aşağıdaki çıkışı oluşturmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b93a1-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
