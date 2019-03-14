---
title: TypeScript ve Web ile ASP.NET Core SignalR kullanma
author: ssougnez
description: Bu öğreticide, Web, istemci, içinde TypeScript yazılmış bir ASP.NET Core SignalR web uygulaması derleme ve paket için yapılandırın.
ms.author: bradyg
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/signalr-typescript-webpack
ms.openlocfilehash: aaf9aa59928ed6b17bc0586d97dbdefc9e30362c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069411"
---
# <a name="use-aspnet-core-signalr-with-typescript-and-webpack"></a><span data-ttu-id="dff19-103">TypeScript ve Web ile ASP.NET Core SignalR kullanma</span><span class="sxs-lookup"><span data-stu-id="dff19-103">Use ASP.NET Core SignalR with TypeScript and Webpack</span></span>

<span data-ttu-id="dff19-104">Tarafından [Sébastien Sougnez](https://twitter.com/ssougnez) ve [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="dff19-104">By [Sébastien Sougnez](https://twitter.com/ssougnez) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="dff19-105">[Web](https://webpack.js.org/) geliştiricilerin paket ve derleme bir web uygulamasının istemci-tarafı kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="dff19-105">[Webpack](https://webpack.js.org/) enables developers to bundle and build the client-side resources of a web app.</span></span> <span data-ttu-id="dff19-106">Web istemcisi yazılmış bir ASP.NET Core SignalR web uygulaması kullanarak bu eğitimde [TypeScript](https://www.typescriptlang.org/).</span><span class="sxs-lookup"><span data-stu-id="dff19-106">This tutorial demonstrates using Webpack in an ASP.NET Core SignalR web app whose client is written in [TypeScript](https://www.typescriptlang.org/).</span></span>

<span data-ttu-id="dff19-107">Bu öğreticide şunların nasıl yapıladığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="dff19-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dff19-108">Bir başlangıç ASP.NET Core SignalR uygulaması iskelesini</span><span class="sxs-lookup"><span data-stu-id="dff19-108">Scaffold a starter ASP.NET Core SignalR app</span></span>
> * <span data-ttu-id="dff19-109">SignalR TypeScript istemciyi Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dff19-109">Configure the SignalR TypeScript client</span></span>
> * <span data-ttu-id="dff19-110">Web kullanarak bir derleme işlem hattı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dff19-110">Configure a build pipeline using Webpack</span></span>
> * <span data-ttu-id="dff19-111">SignalR sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dff19-111">Configure the SignalR server</span></span>
> * <span data-ttu-id="dff19-112">İstemci ve sunucu arasında iletişimi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dff19-112">Enable communication between client and server</span></span>

<span data-ttu-id="dff19-113">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr-typescript-webpack/sample) ([nasıl indirileceğini](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="dff19-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr-typescript-webpack/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-vs-vsc-2.2.md)]

## <a name="create-the-aspnet-core-web-app"></a><span data-ttu-id="dff19-114">ASP.NET Core web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dff19-114">Create the ASP.NET Core web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="dff19-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dff19-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="dff19-116">' Nde npm aramak için Visual Studio'yu yapılandırma *yolu* ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="dff19-116">Configure Visual Studio to look for npm in the *PATH* environment variable.</span></span> <span data-ttu-id="dff19-117">Varsayılan olarak, Visual Studio, yükleme dizininde bulunan npm sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="dff19-117">By default, Visual Studio uses the version of npm found in its installation directory.</span></span> <span data-ttu-id="dff19-118">Visual Studio'da bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="dff19-118">Follow these instructions in Visual Studio:</span></span>

1. <span data-ttu-id="dff19-119">Gidin **Araçları** > **seçenekleri** > **projeler ve çözümler** > **WebpaketYönetimi**  >  **Dış Web Araçları**.</span><span class="sxs-lookup"><span data-stu-id="dff19-119">Navigate to **Tools** > **Options** > **Projects and Solutions** > **Web Package Management** > **External Web Tools**.</span></span>
1. <span data-ttu-id="dff19-120">Seçin *$(PATH)* listeden girişi.</span><span class="sxs-lookup"><span data-stu-id="dff19-120">Select the *$(PATH)* entry from the list.</span></span> <span data-ttu-id="dff19-121">Giriş listede ikinci konuma taşımak için yukarı oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dff19-121">Click the up arrow to move the entry to the second position in the list.</span></span>

    ![Visual Studio yapılandırması](signalr-typescript-webpack/_static/signalr-configure-path-visual-studio.png)

<span data-ttu-id="dff19-123">Visual Studio yapılandırması tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="dff19-123">Visual Studio configuration is completed.</span></span> <span data-ttu-id="dff19-124">Projeyi oluşturmak için zaman var.</span><span class="sxs-lookup"><span data-stu-id="dff19-124">It's time to create the project.</span></span>

1. <span data-ttu-id="dff19-125">Kullanım **dosya** > **yeni** > **proje** menüsünde seçenek ve **ASP.NET Core Web uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="dff19-125">Use the **File** > **New** > **Project** menu option and choose the **ASP.NET Core Web Application** template.</span></span>
1. <span data-ttu-id="dff19-126">Projeyi adlandırın *SignalRWebPack*seçip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dff19-126">Name the project *SignalRWebPack*, and select **OK**.</span></span>
1. <span data-ttu-id="dff19-127">Seçin *.NET Core* açılır ve select hedef çerçeveden *ASP.NET Core 2.2* framework Seçici açılan menüsü'nden.</span><span class="sxs-lookup"><span data-stu-id="dff19-127">Select *.NET Core* from the target framework drop-down, and select *ASP.NET Core 2.2* from the framework selector drop-down.</span></span> <span data-ttu-id="dff19-128">Seçin **boş** şablonu ve select **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dff19-128">Select the **Empty** template, and select **OK**.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="dff19-129">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dff19-129">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="dff19-130">Aşağıdaki komutu çalıştırın **tümleşik Terminalini**:</span><span class="sxs-lookup"><span data-stu-id="dff19-130">Run the following command in the **Integrated Terminal**:</span></span>

```console
dotnet new web -o SignalRWebPack
```

<span data-ttu-id="dff19-131">Boş bir ASP.NET Core web uygulaması .NET Core'u hedefleyen oluşturulan bir *SignalRWebPack* dizin.</span><span class="sxs-lookup"><span data-stu-id="dff19-131">An empty ASP.NET Core web app, targeting .NET Core, is created in a *SignalRWebPack* directory.</span></span>

---

## <a name="configure-webpack-and-typescript"></a><span data-ttu-id="dff19-132">Web ve TypeScript yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dff19-132">Configure Webpack and TypeScript</span></span>

<span data-ttu-id="dff19-133">Aşağıdaki adımlar, JavaScript, TypeScript, dönüştürme ve istemci tarafı kaynaklarını paketleme yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dff19-133">The following steps configure the conversion of TypeScript to JavaScript and the bundling of client-side resources.</span></span>

1. <span data-ttu-id="dff19-134">Aşağıdaki komutu yürütün oluşturmak için proje kök dizininde bir *package.json* dosyası:</span><span class="sxs-lookup"><span data-stu-id="dff19-134">Execute the following command in the project root to create a *package.json* file:</span></span>

    ```console
    npm init -y
    ```

1. <span data-ttu-id="dff19-135">Vurgulanan özellik ekleyin *package.json* dosyası:</span><span class="sxs-lookup"><span data-stu-id="dff19-135">Add the highlighted property to the *package.json* file:</span></span>

    [!code-json[package.json](signalr-typescript-webpack/sample/snippets/package1.json?highlight=4)]

    <span data-ttu-id="dff19-136">Ayarı `private` özelliğini `true` sonraki adımda paket yükleme uyarıları engeller.</span><span class="sxs-lookup"><span data-stu-id="dff19-136">Setting the `private` property to `true` prevents package installation warnings in the next step.</span></span>

1. <span data-ttu-id="dff19-137">Gerekli npm paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="dff19-137">Install the required npm packages.</span></span> <span data-ttu-id="dff19-138">Proje kökünden aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="dff19-138">Execute the following command from the project root:</span></span>

    ```console
    npm install -D -E clean-webpack-plugin@1.0.1 css-loader@2.1.0 html-webpack-plugin@4.0.0-beta.5 mini-css-extract-plugin@0.5.0 ts-loader@5.3.3 typescript@3.3.3 webpack@4.29.3 webpack-cli@3.2.3
    ```

    <span data-ttu-id="dff19-139">Dikkat edilecek bazı komut ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="dff19-139">Some command details to note:</span></span>

    * <span data-ttu-id="dff19-140">Bir sürüm numarasından `@` her paket adı için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dff19-140">A version number follows the `@` sign for each package name.</span></span> <span data-ttu-id="dff19-141">npm, bu belirli bir paket sürümlerini yükler.</span><span class="sxs-lookup"><span data-stu-id="dff19-141">npm installs those specific package versions.</span></span>
    * <span data-ttu-id="dff19-142">`-E` Seçeneği, yazma npm'ın varsayılan davranışı devre dışı bırakır [semantic versioning](https://semver.org/) işleçler için aralığı *package.json*.</span><span class="sxs-lookup"><span data-stu-id="dff19-142">The `-E` option disables npm's default behavior of writing [semantic versioning](https://semver.org/) range operators to *package.json*.</span></span> <span data-ttu-id="dff19-143">Örneğin, `"webpack": "4.29.3"` yerine kullanılan `"webpack": "^4.29.3"`.</span><span class="sxs-lookup"><span data-stu-id="dff19-143">For example, `"webpack": "4.29.3"` is used instead of `"webpack": "^4.29.3"`.</span></span> <span data-ttu-id="dff19-144">Bu seçenek, istenmeyen yükseltmeleri için yeni bir paket sürümlerini önler.</span><span class="sxs-lookup"><span data-stu-id="dff19-144">This option prevents unintended upgrades to newer package versions.</span></span>

    <span data-ttu-id="dff19-145">Resmi görmek [npm yükleme](https://docs.npmjs.com/cli/install) daha fazla ayrıntı için belgeleri.</span><span class="sxs-lookup"><span data-stu-id="dff19-145">See the official [npm-install](https://docs.npmjs.com/cli/install) docs for more detail.</span></span>

1. <span data-ttu-id="dff19-146">Değiştirin `scripts` özelliği *package.json* aşağıdaki kod parçacığı dosyası:</span><span class="sxs-lookup"><span data-stu-id="dff19-146">Replace the `scripts` property of the *package.json* file with the following snippet:</span></span>

    ```json
    "scripts": {
      "build": "webpack --mode=development --watch",
      "release": "webpack --mode=production",
      "publish": "npm run release && dotnet publish -c Release"
    },
    ```

    <span data-ttu-id="dff19-147">Bazı komut dosyaları açıklaması:</span><span class="sxs-lookup"><span data-stu-id="dff19-147">Some explanation of the scripts:</span></span>

    * <span data-ttu-id="dff19-148">`build`: İstemci tarafı kaynaklarınızı geliştirme modunda oluşturur ve dosya değişikliklerini izler.</span><span class="sxs-lookup"><span data-stu-id="dff19-148">`build`: Bundles your client-side resources in development mode and watches for file changes.</span></span> <span data-ttu-id="dff19-149">Dosya İzleyici, paket her zaman bir proje dosya değişiklikleri yeniden neden olur.</span><span class="sxs-lookup"><span data-stu-id="dff19-149">The file watcher causes the bundle to regenerate each time a project file changes.</span></span> <span data-ttu-id="dff19-150">`mode` Seçeneği, ağaç sallayabilir ve küçültme gibi üretim iyileştirmeleri devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="dff19-150">The `mode` option disables production optimizations, such as tree shaking and minification.</span></span> <span data-ttu-id="dff19-151">Yalnızca `build` geliştirme.</span><span class="sxs-lookup"><span data-stu-id="dff19-151">Only use `build` in development.</span></span>
    * <span data-ttu-id="dff19-152">`release`: İstemci tarafı kaynaklarınızı üretim modunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dff19-152">`release`: Bundles your client-side resources in production mode.</span></span>
    * <span data-ttu-id="dff19-153">`publish`: Çalıştırmaları `release` üretim modunda istemci-tarafı kaynakları paket betiği.</span><span class="sxs-lookup"><span data-stu-id="dff19-153">`publish`: Runs the `release` script to bundle the client-side resources in production mode.</span></span> <span data-ttu-id="dff19-154">.NET Core CLI'ın çağırdığı [yayımlama](/dotnet/core/tools/dotnet-publish) uygulamayı yayımlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="dff19-154">It calls the .NET Core CLI's [publish](/dotnet/core/tools/dotnet-publish) command to publish the app.</span></span>

1. <span data-ttu-id="dff19-155">Adlı bir dosya oluşturun *webpack.config.js*, proje kökündeki aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="dff19-155">Create a file named *webpack.config.js*, in the project root, with the following content:</span></span>

    [!code-javascript[webpack.config.js](signalr-typescript-webpack/sample/webpack.config.js)]

    <span data-ttu-id="dff19-156">Önceki dosya Web Derleme yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="dff19-156">The preceding file configures the Webpack compilation.</span></span> <span data-ttu-id="dff19-157">Dikkat edilecek bazı yapılandırma ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="dff19-157">Some configuration details to note:</span></span>

    * <span data-ttu-id="dff19-158">`output` Özelliğini geçersiz kılar, varsayılan değerini *dist*.</span><span class="sxs-lookup"><span data-stu-id="dff19-158">The `output` property overrides the default value of *dist*.</span></span> <span data-ttu-id="dff19-159">Paket yerine yayıldığını *wwwroot* dizin.</span><span class="sxs-lookup"><span data-stu-id="dff19-159">The bundle is instead emitted in the *wwwroot* directory.</span></span>
    * <span data-ttu-id="dff19-160">`resolve.extensions` Dizi içeren *.js* SignalR istemci JavaScript içeri aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="dff19-160">The `resolve.extensions` array includes *.js* to import the SignalR client JavaScript.</span></span>

1. <span data-ttu-id="dff19-161">Yeni bir *src* proje kök dizini.</span><span class="sxs-lookup"><span data-stu-id="dff19-161">Create a new *src* directory in the project root.</span></span> <span data-ttu-id="dff19-162">Amacı, projenin istemci-tarafı varlıkları depolamaktır.</span><span class="sxs-lookup"><span data-stu-id="dff19-162">Its purpose is to store the project's client-side assets.</span></span>

1. <span data-ttu-id="dff19-163">Oluşturma *src/index.html* aşağıdaki içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="dff19-163">Create *src/index.html* with the following content.</span></span>

    [!code-html[index.html](signalr-typescript-webpack/sample/src/index.html)]

    <span data-ttu-id="dff19-164">Önceki HTML spotuna Demirbaş biçimlendirme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="dff19-164">The preceding HTML defines the homepage's boilerplate markup.</span></span>

1. <span data-ttu-id="dff19-165">Yeni bir *src/css* dizin.</span><span class="sxs-lookup"><span data-stu-id="dff19-165">Create a new *src/css* directory.</span></span> <span data-ttu-id="dff19-166">Amacı, projenin depolamaktır *.css* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="dff19-166">Its purpose is to store the project's *.css* files.</span></span>

1. <span data-ttu-id="dff19-167">Oluşturma *src/css/main.css* aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="dff19-167">Create *src/css/main.css* with the following content:</span></span>

    [!code-css[main.css](signalr-typescript-webpack/sample/src/css/main.css)]

    <span data-ttu-id="dff19-168">Önceki *main.css* dosya stiller uygulama.</span><span class="sxs-lookup"><span data-stu-id="dff19-168">The preceding *main.css* file styles the app.</span></span>

1. <span data-ttu-id="dff19-169">Oluşturma *src/tsconfig.json* aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="dff19-169">Create *src/tsconfig.json* with the following content:</span></span>

    [!code-json[tsconfig.json](signalr-typescript-webpack/sample/src/tsconfig.json)]

    <span data-ttu-id="dff19-170">Yukarıdaki kod üretmek için TypeScript derleyicisi yapılandırır [ECMAScript](https://wikipedia.org/wiki/ECMAScript) 5 ile uyumlu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dff19-170">The preceding code configures the TypeScript compiler to produce [ECMAScript](https://wikipedia.org/wiki/ECMAScript) 5-compatible JavaScript.</span></span>

1. <span data-ttu-id="dff19-171">Oluşturma *src/index.ts* aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="dff19-171">Create *src/index.ts* with the following content:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/snippets/index1.ts?name=snippet_IndexTsPhase1File)]

    <span data-ttu-id="dff19-172">Önceki TypeScript DOM öğeleri için başvuru alır ve iki olay işleyicisi ekler:</span><span class="sxs-lookup"><span data-stu-id="dff19-172">The preceding TypeScript retrieves references to DOM elements and attaches two event handlers:</span></span>

    * <span data-ttu-id="dff19-173">`keyup`: Kullanıcı bir şey olarak tanımlanmış metin kutusuna yazdığında, bu olay harekete `tbMessage`.</span><span class="sxs-lookup"><span data-stu-id="dff19-173">`keyup`: This event fires when the user types something in the textbox identified as `tbMessage`.</span></span> <span data-ttu-id="dff19-174">`send` İşlevi, kullanıcının bastığında çağrılır **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="dff19-174">The `send` function is called when the user presses the **Enter** key.</span></span>
    * <span data-ttu-id="dff19-175">`click`: Kullanıcı tıkladığında bu olay harekete **Gönder** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dff19-175">`click`: This event fires when the user clicks the **Send** button.</span></span> <span data-ttu-id="dff19-176">`send` İşlevi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="dff19-176">The `send` function is called.</span></span>

## <a name="configure-the-aspnet-core-app"></a><span data-ttu-id="dff19-177">ASP.NET Core uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dff19-177">Configure the ASP.NET Core app</span></span>

1. <span data-ttu-id="dff19-178">Sağlanan kod `Startup.Configure` yöntemi görüntüler *Merhaba Dünya!*.</span><span class="sxs-lookup"><span data-stu-id="dff19-178">The code provided in the `Startup.Configure` method displays *Hello World!*.</span></span> <span data-ttu-id="dff19-179">Değiştirin `app.Run` yöntem çağrısının çağrılarıyla [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) ve [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span><span class="sxs-lookup"><span data-stu-id="dff19-179">Replace the `app.Run` method call with calls to [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_UseStaticDefaultFiles)]

    <span data-ttu-id="dff19-180">Yukarıdaki kod bulun ve hizmet sunucuya sağlar *index.html* olmadığını tam URL'sini veya web uygulaması kök URL'sini kullanıcının girdiği dosya.</span><span class="sxs-lookup"><span data-stu-id="dff19-180">The preceding code allows the server to locate and serve the *index.html* file, whether the user enters its full URL or the root URL of the web app.</span></span>

1. <span data-ttu-id="dff19-181">Çağrı [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr#Microsoft_Extensions_DependencyInjection_SignalRDependencyInjectionExtensions_AddSignalR_Microsoft_Extensions_DependencyInjection_IServiceCollection_) içinde `Startup.ConfigureServices` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dff19-181">Call [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr#Microsoft_Extensions_DependencyInjection_SignalRDependencyInjectionExtensions_AddSignalR_Microsoft_Extensions_DependencyInjection_IServiceCollection_) in the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="dff19-182">SignalR Hizmetleri projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="dff19-182">It adds the SignalR services to your project.</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_AddSignalR)]

1. <span data-ttu-id="dff19-183">Harita bir */hub* yönlendirmek `ChatHub` hub.</span><span class="sxs-lookup"><span data-stu-id="dff19-183">Map a */hub* route to the `ChatHub` hub.</span></span> <span data-ttu-id="dff19-184">Sonunda aşağıdaki satırları ekleyin `Startup.Configure` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="dff19-184">Add the following lines at the end of the `Startup.Configure` method:</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_UseSignalR)]

1. <span data-ttu-id="dff19-185">Adlı yeni bir dizin oluşturma *Hubs*, proje kökündeki.</span><span class="sxs-lookup"><span data-stu-id="dff19-185">Create a new directory, called *Hubs*, in the project root.</span></span> <span data-ttu-id="dff19-186">Amacı sonraki adımda oluşturduğunuz SignalR hub depolamaktır.</span><span class="sxs-lookup"><span data-stu-id="dff19-186">Its purpose is to store the SignalR hub, which is created in the next step.</span></span>

1. <span data-ttu-id="dff19-187">Hub'ı oluşturma *Hubs/ChatHub.cs* aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="dff19-187">Create hub *Hubs/ChatHub.cs* with the following code:</span></span>

    [!code-csharp[ChatHub](signalr-typescript-webpack/sample/snippets/ChatHub.cs?name=snippet_ChatHubStubClass)]

1. <span data-ttu-id="dff19-188">Üstüne aşağıdaki kodu ekleyin *Startup.cs* çözümlemek için dosya `ChatHub` başvurusu:</span><span class="sxs-lookup"><span data-stu-id="dff19-188">Add the following code at the top of the *Startup.cs* file to resolve the `ChatHub` reference:</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_HubsNamespace)]

## <a name="enable-client-and-server-communication"></a><span data-ttu-id="dff19-189">İstemci ve sunucu iletişimi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dff19-189">Enable client and server communication</span></span>

<span data-ttu-id="dff19-190">Uygulama şu anda ileti göndermek için basit bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dff19-190">The app currently displays a simple form to send messages.</span></span> <span data-ttu-id="dff19-191">Bunu yapmak denediğinizde hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="dff19-191">Nothing happens when you try to do so.</span></span> <span data-ttu-id="dff19-192">Sunucu, belirli bir yol dinleme ancak gönderilen iletilerle hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="dff19-192">The server is listening to a specific route but does nothing with sent messages.</span></span>

1. <span data-ttu-id="dff19-193">Proje kök dizinini aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="dff19-193">Execute the following command at the project root:</span></span>

    ```console
    npm install @aspnet/signalr
    ```

    <span data-ttu-id="dff19-194">Önceki komutta yükler [SignalR TypeScript istemci](https://www.npmjs.com/package/@aspnet/signalr), istemcinin sunucuya ileti göndermek izin verir.</span><span class="sxs-lookup"><span data-stu-id="dff19-194">The preceding command installs the [SignalR TypeScript client](https://www.npmjs.com/package/@aspnet/signalr), which allows the client to send messages to the server.</span></span>

1. <span data-ttu-id="dff19-195">Vurgulanmış kodu ekleyin *src/index.ts* dosyası:</span><span class="sxs-lookup"><span data-stu-id="dff19-195">Add the highlighted code to the *src/index.ts* file:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/snippets/index2.ts?name=snippet_IndexTsPhase2File&highlight=2,9-23)]

    <span data-ttu-id="dff19-196">Yukarıdaki kod, sunucudan iletileri alma destekler.</span><span class="sxs-lookup"><span data-stu-id="dff19-196">The preceding code supports receiving messages from the server.</span></span> <span data-ttu-id="dff19-197">`HubConnectionBuilder` Sınıf sunucu bağlantısı yapılandırmak için yeni bir oluşturucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dff19-197">The `HubConnectionBuilder` class creates a new builder for configuring the server connection.</span></span> <span data-ttu-id="dff19-198">`withUrl` İşlevi hub URL'sini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="dff19-198">The `withUrl` function configures the hub URL.</span></span>

    <span data-ttu-id="dff19-199">SignalR, bir istemci ve sunucu arasında ileti alışverişi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dff19-199">SignalR enables the exchange of messages between a client and a server.</span></span> <span data-ttu-id="dff19-200">Her ileti, belirli bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="dff19-200">Each message has a specific name.</span></span> <span data-ttu-id="dff19-201">Örneğin, iletileri adıyla olabilir `messageReceived` iletileri bölgede yeni bir ileti görüntülemek için sorumlu mantıksal yürütün.</span><span class="sxs-lookup"><span data-stu-id="dff19-201">For example, you can have messages with the name `messageReceived` that execute the logic responsible for displaying the new message in the messages zone.</span></span> <span data-ttu-id="dff19-202">Aracılığıyla belirli bir ileti için dinleme yapılabilir `on` işlevi.</span><span class="sxs-lookup"><span data-stu-id="dff19-202">Listening to a specific message can be done via the `on` function.</span></span> <span data-ttu-id="dff19-203">Herhangi bir sayıda ileti adları dinleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dff19-203">You can listen to any number of message names.</span></span> <span data-ttu-id="dff19-204">Yazarın adı ve alınan ileti içeriği gibi iletisi parametreleri geçirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="dff19-204">It's also possible to pass parameters to the message, such as the author's name and the content of the message received.</span></span> <span data-ttu-id="dff19-205">İstemci bir ileti aldıktan sonra yeni bir `div` öğesi oluşturulduğunda yazarın adı ve şu iletiyle içeriği kendi `innerHTML` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="dff19-205">Once the client receives a message, a new `div` element is created with the author's name and the message content in its `innerHTML` attribute.</span></span> <span data-ttu-id="dff19-206">Ana eklenir `div` iletileri görüntülemeyi öğesi.</span><span class="sxs-lookup"><span data-stu-id="dff19-206">It's added to the main `div` element displaying the messages.</span></span>

1. <span data-ttu-id="dff19-207">İstemci bir ileti alabilir, ileti göndermek için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dff19-207">Now that the client can receive a message, configure it to send messages.</span></span> <span data-ttu-id="dff19-208">Vurgulanmış kodu ekleyin *src/index.ts* dosyası:</span><span class="sxs-lookup"><span data-stu-id="dff19-208">Add the highlighted code to the *src/index.ts* file:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/src/index.ts?highlight=34-35)]

    <span data-ttu-id="dff19-209">WebSockets bağlantısı üzerinden ileti gönderme, arama gerektirir `send` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dff19-209">Sending a message through the WebSockets connection requires calling the `send` method.</span></span> <span data-ttu-id="dff19-210">Yöntemin ilk parametresi ileti adıdır.</span><span class="sxs-lookup"><span data-stu-id="dff19-210">The method's first parameter is the message name.</span></span> <span data-ttu-id="dff19-211">İleti verileri diğer parametreler inhabits.</span><span class="sxs-lookup"><span data-stu-id="dff19-211">The message data inhabits the other parameters.</span></span> <span data-ttu-id="dff19-212">Bu örnekte, bir ileti olarak tanımlanır. `newMessage` sunucuya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dff19-212">In this example, a message identified as `newMessage` is sent to the server.</span></span> <span data-ttu-id="dff19-213">Kullanıcı adı ve kullanıcı bir metin kutusunda girişi ileti oluşur.</span><span class="sxs-lookup"><span data-stu-id="dff19-213">The message consists of the username and the user input from a text box.</span></span> <span data-ttu-id="dff19-214">Gönderme çalışırsa, metin kutusunun değerini temizlenir.</span><span class="sxs-lookup"><span data-stu-id="dff19-214">If the send works, the text box value is cleared.</span></span>

1. <span data-ttu-id="dff19-215">Vurgulanan yöntemine ekleyin `ChatHub` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="dff19-215">Add the highlighted method to the `ChatHub` class:</span></span>

    [!code-csharp[ChatHub](signalr-typescript-webpack/sample/Hubs/ChatHub.cs?highlight=8-11)]

    <span data-ttu-id="dff19-216">Sunucu bunları aldıktan sonra önceki kod bağlı tüm kullanıcılar için alınan iletiler yayımlar.</span><span class="sxs-lookup"><span data-stu-id="dff19-216">The preceding code broadcasts received messages to all connected users once the server receives them.</span></span> <span data-ttu-id="dff19-217">Genel gereksizdir `on` tüm iletileri almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dff19-217">It's unnecessary to have a generic `on` method to receive all the messages.</span></span> <span data-ttu-id="dff19-218">İleti adı eklerini sonra adlı bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="dff19-218">A method named after the message name suffices.</span></span>

    <span data-ttu-id="dff19-219">Bu örnekte, TypeScript istemci olarak tanımlanan bir ileti gönderir. `newMessage`.</span><span class="sxs-lookup"><span data-stu-id="dff19-219">In this example, the TypeScript client sends a message identified as `newMessage`.</span></span> <span data-ttu-id="dff19-220">C# `NewMessage` yöntemi istemci tarafından gönderilen verilerin bekliyor.</span><span class="sxs-lookup"><span data-stu-id="dff19-220">The C# `NewMessage` method expects the data sent by the client.</span></span> <span data-ttu-id="dff19-221">İçin bir çağrı yapılır [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) metodunda [Clients.All](/dotnet/api/microsoft.aspnetcore.signalr.ihubclients-1.all).</span><span class="sxs-lookup"><span data-stu-id="dff19-221">A call is made to the [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) method on [Clients.All](/dotnet/api/microsoft.aspnetcore.signalr.ihubclients-1.all).</span></span> <span data-ttu-id="dff19-222">Alınan iletiler, hub'ına bağlı tüm istemcilere gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dff19-222">The received messages are sent to all clients connected to the hub.</span></span>

## <a name="test-the-app"></a><span data-ttu-id="dff19-223">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="dff19-223">Test the app</span></span>

<span data-ttu-id="dff19-224">Uygulama aşağıdaki adımlarla çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="dff19-224">Confirm that the app works with the following steps.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="dff19-225">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dff19-225">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="dff19-226">Web Çalıştır *yayın* modu.</span><span class="sxs-lookup"><span data-stu-id="dff19-226">Run Webpack in *release* mode.</span></span> <span data-ttu-id="dff19-227">Kullanarak **Paket Yöneticisi Konsolu** penceresinde proje kök dizininde aşağıdaki komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="dff19-227">Using the **Package Manager Console** window, execute the following command in the project root.</span></span> <span data-ttu-id="dff19-228">Proje kök dizininde değilse girin `cd SignalRWebPack` komutu ulaşmadan önce.</span><span class="sxs-lookup"><span data-stu-id="dff19-228">If you are not in the project root, enter `cd SignalRWebPack` before entering the command.</span></span>

    [!INCLUDE [npm-run-release](../includes/signalr-typescript-webpack/npm-run-release.md)]

1. <span data-ttu-id="dff19-229">Seçin **hata ayıklama** > **ayıklamadan Başlat** Haya ayıklayıcı eklemeden uygulamayı bir tarayıcıda başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="dff19-229">Select **Debug** > **Start without debugging** to launch the app in a browser without attaching the debugger.</span></span> <span data-ttu-id="dff19-230">*Wwwroot/index.html* dosya hizmet `http://localhost:<port_number>`.</span><span class="sxs-lookup"><span data-stu-id="dff19-230">The *wwwroot/index.html* file is served at `http://localhost:<port_number>`.</span></span>

1. <span data-ttu-id="dff19-231">Başka bir tarayıcı örneğinde (herhangi bir tarayıcıda) açın.</span><span class="sxs-lookup"><span data-stu-id="dff19-231">Open another browser instance (any browser).</span></span> <span data-ttu-id="dff19-232">Adres çubuğuna URL'yi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="dff19-232">Paste the URL in the address bar.</span></span>

1. <span data-ttu-id="dff19-233">Ya da tarayıcı seçin, bir **ileti** metin kutusu seçeneğine tıklayıp **Gönder** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dff19-233">Choose either browser, type something in the **Message** text box, and click the **Send** button.</span></span> <span data-ttu-id="dff19-234">Benzersiz kullanıcı adı ve ileti iki sayfalarında anında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dff19-234">The unique user name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="dff19-235">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dff19-235">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="dff19-236">Web Çalıştır *yayın* proje kök dizininde aşağıdaki komutu yürüterek modu:</span><span class="sxs-lookup"><span data-stu-id="dff19-236">Run Webpack in *release* mode by executing the following command in the project root:</span></span>

    [!INCLUDE [npm-run-release](../includes/signalr-typescript-webpack/npm-run-release.md)]

1. <span data-ttu-id="dff19-237">Yapı ve proje kök dizininde aşağıdaki komutu çalıştırarak uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dff19-237">Build and run the app by executing the following command in the project root:</span></span>

    ```console
    dotnet run
    ```

    <span data-ttu-id="dff19-238">Web sunucusu uygulama başlar ve komut localhost üzerinde kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="dff19-238">The web server starts the app and makes it available on localhost.</span></span>

1. <span data-ttu-id="dff19-239">Bir tarayıcıda `http://localhost:<port_number>`.</span><span class="sxs-lookup"><span data-stu-id="dff19-239">Open a browser to `http://localhost:<port_number>`.</span></span> <span data-ttu-id="dff19-240">*Wwwroot/index.html* dosya hizmet.</span><span class="sxs-lookup"><span data-stu-id="dff19-240">The *wwwroot/index.html* file is served.</span></span> <span data-ttu-id="dff19-241">Adres çubuğundan URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dff19-241">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="dff19-242">Başka bir tarayıcı örneğinde (herhangi bir tarayıcıda) açın.</span><span class="sxs-lookup"><span data-stu-id="dff19-242">Open another browser instance (any browser).</span></span> <span data-ttu-id="dff19-243">Adres çubuğuna URL'yi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="dff19-243">Paste the URL in the address bar.</span></span>

1. <span data-ttu-id="dff19-244">Ya da tarayıcı seçin, bir **ileti** metin kutusu seçeneğine tıklayıp **Gönder** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dff19-244">Choose either browser, type something in the **Message** text box, and click the **Send** button.</span></span> <span data-ttu-id="dff19-245">Benzersiz kullanıcı adı ve ileti iki sayfalarında anında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dff19-245">The unique user name and message are displayed on both pages instantly.</span></span>

---

![Her iki Tarayıcı pencerelerinde görüntülenen ileti](signalr-typescript-webpack/_static/browsers-message-broadcast.png)

## <a name="additional-resources"></a><span data-ttu-id="dff19-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dff19-247">Additional resources</span></span>

* <xref:signalr/javascript-client>
* <xref:signalr/hubs>
