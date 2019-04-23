---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN başlangıç sınıfı algılama | Microsoft Docs
author: Praburaj
description: Bu öğreticide, hangi OWIN başlangıç sınıfı yüklenen yapılandırma işlemi gösterilmektedir. Bir genel bakış, Project Katana'ya OWIN hakkında daha fazla bilgi için bkz. Bu öğreticide oluştu...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e4d9424d691f92aacf078faed09689daa40a44fd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59418345"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="ca60d-105">OWIN Başlangıç Sınıfı Algılama</span><span class="sxs-lookup"><span data-stu-id="ca60d-105">OWIN Startup Class Detection</span></span>


> <span data-ttu-id="ca60d-106">Bu öğreticide, hangi OWIN başlangıç sınıfı yüklenen yapılandırma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ca60d-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="ca60d-107">OWIN hakkında daha fazla bilgi için bkz. [bir genel bakış, Project Katana'ya](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="ca60d-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="ca60d-108">Bu öğreticide, Rick Anderson tarafından yazılmış ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ), Praburaj Yöneticisi ve Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) ).</span><span class="sxs-lookup"><span data-stu-id="ca60d-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="ca60d-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ca60d-109">Prerequisites</span></span>
>
> [<span data-ttu-id="ca60d-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ca60d-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)


## <a name="owin-startup-class-detection"></a><span data-ttu-id="ca60d-111">OWIN Başlangıç Sınıfı Algılama</span><span class="sxs-lookup"><span data-stu-id="ca60d-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="ca60d-112">Her bir OWIN uygulaması bileşenleri uygulama ardışık düzeni için belirttiğiniz başlangıç sınıfı vardır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="ca60d-113">Çalışma zamanı ile başlangıç sınıfınıza bağlanabilir farklı yolu vardır, barındırma modeline bağlı olarak (OwinHost, IIS ve IIS Express) seçin.</span><span class="sxs-lookup"><span data-stu-id="ca60d-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="ca60d-114">Bu öğreticide gösterilen başlangıç sınıfı barındırma her uygulamada kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca60d-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="ca60d-115">Başlangıç sınıfı, barındırma çalışma zamanı bunlardan birini yaklaşıyor kullanarak bağlanın:</span><span class="sxs-lookup"><span data-stu-id="ca60d-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="ca60d-116">**Adlandırma kuralı**: Katana görünen adlı bir sınıf için `Startup` derleme adı veya genel ad eşleşen bir ad.</span><span class="sxs-lookup"><span data-stu-id="ca60d-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="ca60d-117">**OwinStartup özniteliği**: Bu, çoğu geliştirici, başlangıç sınıfı belirtmek için sürer yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="ca60d-118">Başlangıç sınıfı aşağıdaki öznitelik ayarlayacak `TestStartup` sınıfını `StartupDemo` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="ca60d-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="ca60d-119">`OwinStartup` Özniteliği adlandırma kuralını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ca60d-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="ca60d-120">Bu öznitelik ile kolay bir ad da belirtebilirsiniz, ancak bir kolay ad kullanmanızı da kullanmanızı gerekli hale getirmiş `appSetting` yapılandırma dosyasındaki öğesi.</span><span class="sxs-lookup"><span data-stu-id="ca60d-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="ca60d-121">**Yapılandırma dosyalarında appSetting öğesi**: `appSetting` Öğesini geçersiz kılar `OwinStartup` özniteliği ve adlandırma kuralları.</span><span class="sxs-lookup"><span data-stu-id="ca60d-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="ca60d-122">Birden çok başlangıç sınıfı olabilir (kullanarak her bir `OwinStartup` özniteliği) ve hangi başlangıç sınıfı kullanarak biçimlendirme aşağıdakine benzer bir yapılandırma dosyasında yüklenen yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="ca60d-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="ca60d-123">Derleme ve başlangıç sınıfı açıkça belirtir aşağıdaki anahtarı de kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ca60d-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="ca60d-124">Yapılandırma dosyasında aşağıdaki XML'i kolay başlangıç sınıf adını belirtir. `ProductionConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="ca60d-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="ca60d-125">Yukarıdaki biçimlendirme şunlarla birlikte kullanılmalıdır `OwinStartup` kolay bir ad belirtir ve neden özniteliği `ProductionStartup2` çalıştırmak için sınıf.</span><span class="sxs-lookup"><span data-stu-id="ca60d-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="ca60d-126">OWIN başlangıç bulma devre dışı bırakmak için ekleme `appSetting owin:AutomaticAppStartup` değeriyle `"false"` web.config dosyasında.</span><span class="sxs-lookup"><span data-stu-id="ca60d-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="ca60d-127">OWIN Başlangıç'ı kullanarak bir ASP.NET Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca60d-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="ca60d-128">Boş bir Asp.Net web uygulaması oluşturun ve adlandırın **StartupDemo**.</span><span class="sxs-lookup"><span data-stu-id="ca60d-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="ca60d-129">-Yükleme `Microsoft.Owin.Host.SystemWeb` NuGet Paket Yöneticisi'ni kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ca60d-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="ca60d-130">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="ca60d-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="ca60d-131">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="ca60d-132">OWIN başlangıç sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca60d-132">Add an OWIN startup class.</span></span> <span data-ttu-id="ca60d-133">Visual Studio 2017'de, projeye sağ tıklayıp seçin **sınıfı Ekle**. - **Yeni Öğe Ekle** iletişim kutusuna *OWIN* arama alanını ve için Startup.cs adını değiştirin ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ca60d-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="ca60d-134">Eklemek istediğiniz sonraki açışınızda bir *Owın başlangıç sınıfı*, bunu olacak kullanılabilir **Ekle** menüsü.</span><span class="sxs-lookup"><span data-stu-id="ca60d-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="ca60d-135">Alternatif olarak, projeye sağ tıklayıp seçin **Ekle**, ardından **yeni öğe**ve ardından **Owın başlangıç sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="ca60d-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="ca60d-136">Oluşturulan kod değiştirin *Startup.cs* aşağıdaki dosya:</span><span class="sxs-lookup"><span data-stu-id="ca60d-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="ca60d-137">`app.Use` Lambda ifadesi belirtilen bir ara yazılım bileşeni OWIN ardışık düzenine kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="ca60d-138">Bu durumda biz gelen isteği yanıtlamayı önce gelen isteklerin günlük ayarlıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ca60d-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="ca60d-139">`next` Parametresi, temsilci ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [görev](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) ardışık düzende sonraki bileşene.</span><span class="sxs-lookup"><span data-stu-id="ca60d-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="ca60d-140">`app.Run` Lambda ifadesi, gelen istekler için bir işlem hattı kancaları ve yanıt mekanizmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca60d-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="ca60d-141">Yukarıdaki kodda biz yorum `OwinStartup` özniteliği ve adlı sınıfını çalışan kuralına bağlı `Startup` .-basın ***F5*** uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca60d-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="ca60d-142">Yenileme birkaç kez basın.</span><span class="sxs-lookup"><span data-stu-id="ca60d-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="ca60d-143">![](owin-startup-class-detection/_static/image4.png) Not: Bu öğreticide görüntüde gösterilen sayıya gördüğünüz sayıyı eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="ca60d-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="ca60d-144">Milisaniyeden kısa dize, sayfayı yenileyin, yeni bir yanıt göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="ca60d-145">İzleme bilgileri gördüğünüz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ca60d-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="ca60d-146">Daha fazla başlangıç sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="ca60d-146">Add More Startup Classes</span></span>

<span data-ttu-id="ca60d-147">Bu bölümde başka bir başlangıç sınıfı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca60d-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="ca60d-148">Uygulamanızı birden çok OWIN başlangıç sınıfı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca60d-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="ca60d-149">Örneğin, geliştirme, test ve üretim için başlangıç sınıfları oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca60d-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="ca60d-150">Yeni bir OWIN başlangıç sınıfı oluşturun ve adlandırın `ProductionStartup`.</span><span class="sxs-lookup"><span data-stu-id="ca60d-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="ca60d-151">Oluşturulan kodu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="ca60d-152">Denetim uygulamayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ca60d-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="ca60d-153">`OwinStartup` Özniteliği belirtir üretim başlangıç sınıfı çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="ca60d-154">Başka bir OWIN başlangıç sınıfı oluşturun ve adlandırın `TestStartup`.</span><span class="sxs-lookup"><span data-stu-id="ca60d-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="ca60d-155">Oluşturulan kodu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="ca60d-156">`OwinStartup` Özniteliği aşırı yukarıdaki belirtir `TestingConfiguration` olarak *kolay* başlangıç sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="ca60d-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="ca60d-157">Açık *web.config* dosya ve başlangıç sınıfı kolay adını belirten OWIN uygulaması başlangıç anahtarı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="ca60d-158">Denetim uygulamayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ca60d-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="ca60d-159">Uygulama ayarları öğesi etkileyen ve test alır yapılandırma çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="ca60d-160">Kaldırma *kolay* ad alanından `OwinStartup` özniteliğini `TestStartup` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ca60d-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="ca60d-161">OWIN uygulaması başlangıç anahtarına değiştirin *web.config* aşağıdaki dosya:</span><span class="sxs-lookup"><span data-stu-id="ca60d-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="ca60d-162">Geri döndürme `OwinStartup` her sınıf için Visual Studio tarafından oluşturulan varsayılan öznitelik kodu özniteliği:</span><span class="sxs-lookup"><span data-stu-id="ca60d-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="ca60d-163">Her bir OWIN uygulaması başlangıç anahtarı aşağıdaki üretim sınıfı çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ca60d-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="ca60d-164">Son başlangıç anahtarı başlangıç yapılandırmasını yöntemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca60d-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="ca60d-165">Aşağıdaki OWIN uygulaması başlangıç anahtarı için yapılandırma sınıfı adını değiştirmenizi sağlar `MyConfiguration` .</span><span class="sxs-lookup"><span data-stu-id="ca60d-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="ca60d-166">Using Owinhost.exe</span><span class="sxs-lookup"><span data-stu-id="ca60d-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="ca60d-167">Web.config dosyasına aşağıdaki biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="ca60d-168">Son anahtar WINS, bu durumda bunu `TestStartup` belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ca60d-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="ca60d-169">Owinhost PMC'yi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="ca60d-170">Uygulama klasöre gidin (içeren klasörü *Web.config* dosyası) bir komut istemi ve türü:</span><span class="sxs-lookup"><span data-stu-id="ca60d-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="ca60d-171">Komut penceresinde gösterir:</span><span class="sxs-lookup"><span data-stu-id="ca60d-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="ca60d-172">URL ile bir tarayıcıyı başlatacak `http://localhost:5000/`.</span><span class="sxs-lookup"><span data-stu-id="ca60d-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="ca60d-173">OwinHost başlangıç kurallarına yukarıda listelenen dikkate alınır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="ca60d-174">Komut penceresinde OwinHost çıkmak için Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ca60d-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="ca60d-175">İçinde `ProductionStartup` sınıfı, kolay adını belirten şu OwinStartup özniteliği ekleyin *ProductionConfiguration*.</span><span class="sxs-lookup"><span data-stu-id="ca60d-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="ca60d-176">Komut istemi ve türü:</span><span class="sxs-lookup"><span data-stu-id="ca60d-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="ca60d-177">Üretim başlangıç sınıfı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ca60d-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="ca60d-178">Uygulamamızı birden çok başlangıç sınıfı vardır ve bu örnekte biz kadar çalışma zamanının hangi başlangıç sınıfı ertelenmiş yürütmeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ca60d-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="ca60d-179">Aşağıdaki çalışma zamanı başlatma seçenekleri test edin:</span><span class="sxs-lookup"><span data-stu-id="ca60d-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
