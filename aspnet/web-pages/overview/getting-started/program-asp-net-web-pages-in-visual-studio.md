---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programlama ASP.NET Web Sayfaları (Razor) Visual Studio kullanma | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu ek, Web Sayfalarını Jilet sözdizimi yle program ASP.NETlamak için Visual Studio 2010 veya Visual Web Developer 2010 Express'i nasıl kullanabileceğinizi açıklar.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542904"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="315c8-103">Programlama ASP.NET Web Sayfaları (Razor) Visual Studio kullanma</span><span class="sxs-lookup"><span data-stu-id="315c8-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="315c8-104"> yazan: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="315c8-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="315c8-105">Bu makalede, Web Sayfaları (Razor) web sitelerini ASP.NET programlamak için Visual Studio veya Visual Web Developer Express'i nasıl kullanabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="315c8-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="315c8-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="315c8-106">What you'll learn</span></span>
>
> - <span data-ttu-id="315c8-107">Visual Studio sürümünüzdeki ASP.NET Web Sayfaları ile çalışmak için yüklemeniz gerekenler (varsa)</span><span class="sxs-lookup"><span data-stu-id="315c8-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="315c8-108">Visual Web Developer 2010 Express'e ASP.NET Web Sayfaları için destek nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="315c8-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="315c8-109">IntelliSense ve hata ayıklama dahil olmak üzere ASP.NET Razor sayfaları ile çalışmak için Visual Studio özellikleri nasıl kullanılır.</span><span class="sxs-lookup"><span data-stu-id="315c8-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="315c8-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="315c8-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="315c8-111">ASP.NET Web Sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="315c8-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="315c8-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="315c8-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="315c8-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="315c8-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="315c8-114">Bu öğretici ayrıca ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010 ve WebMatrix 2 ile birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="315c8-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="315c8-115">WebMatrix veya diğer birçok kod düzenleyicisini kullanarak Web sayfalarını Razor sözdizimi ile ASP.NET programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="315c8-116">Ayrıca, birçok uygulama türü (yalnızca web siteleri değil) oluşturmak için güçlü bir araç kümesi sağlayan tam özellikli tümleşik bir geliştirme ortamı (IDE) olan Microsoft Visual Studio'yu da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="315c8-117">ASP.NET Razor sayfaları ile çalışmak için [Visual Studio 2017'yi](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="315c8-118">Visual Studio'nun ASP.NET Razor web sayfaları yla programlama için sağladığı iki özellikle kullanışlı özellik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="315c8-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="315c8-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="315c8-119">*IntelliSense*.</span></span> <span data-ttu-id="315c8-120">Visual Studio'da yerleşik Olan IntelliSense özelliği, WebMatrix'teki IntelliSense'den daha kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="315c8-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="315c8-121">*Hata ayıklama.*</span><span class="sxs-lookup"><span data-stu-id="315c8-121">*Debugger*.</span></span> <span data-ttu-id="315c8-122">Hata ayıklayıcı, bir programı çalışırken durdurarak, değişkenleri inceleyerek ve kod satırına satır satır adım atarak kodunuzu sorun gidermenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="315c8-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="315c8-123">ASP.NET Web Sayfalarının Farklı Sürümleriyle Visual Studio'nun Kullanılması</span><span class="sxs-lookup"><span data-stu-id="315c8-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="315c8-124">Visual Studio 2017'de ASP.NET web uygulamaları geliştirmek için **ASP.NET ve web geliştirme** iş yükünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="315c8-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="315c8-125">Visual Studio 2012 ve Visual Studio 2013 ASP.NET Web Sayfaları desteğini içerir.</span><span class="sxs-lookup"><span data-stu-id="315c8-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="315c8-126">(Visual Studio'yu yüklediğinizde web sayfalarını ASP.NET desteklemek için gereken paketler yüklenir.)</span><span class="sxs-lookup"><span data-stu-id="315c8-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="315c8-127">Visual Studio 2010, web sayfalarını ASP.NET için varsayılan olarak destek içermez.</span><span class="sxs-lookup"><span data-stu-id="315c8-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="315c8-128">Visual Studio 2010 ile web sayfalarını ASP.NET kullanmak için ASP.NET MVC paketini yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="315c8-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="315c8-129">Web Sayfalarını 2ASP.NET almak için MVC 4 ASP.NET yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="315c8-130">Aşağıdaki tablo, Visual Studio'nun farklı sürümlerinde ASP.NET Web Sayfaları desteğini özetleyilmiştir.</span><span class="sxs-lookup"><span data-stu-id="315c8-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="315c8-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="315c8-131">Visual Studio 2010</span></span> | <span data-ttu-id="315c8-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="315c8-132">Visual Studio 2012</span></span> | <span data-ttu-id="315c8-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="315c8-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="315c8-134">**ASP.NET Web Sayfaları 2**</span><span class="sxs-lookup"><span data-stu-id="315c8-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="315c8-135">MVC 4 ASP.NET yükleyin</span><span class="sxs-lookup"><span data-stu-id="315c8-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="315c8-136">(Dahil)</span><span class="sxs-lookup"><span data-stu-id="315c8-136">(Included)</span></span> | <span data-ttu-id="315c8-137">(Dahil)</span><span class="sxs-lookup"><span data-stu-id="315c8-137">(Included)</span></span> |
| <span data-ttu-id="315c8-138">**ASP.NET Web Sayfaları 3**</span><span class="sxs-lookup"><span data-stu-id="315c8-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="315c8-139">NuGet ile Web Sayfalarını 3 ASP.NET güncelleme</span><span class="sxs-lookup"><span data-stu-id="315c8-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="315c8-140">(Dahil)</span><span class="sxs-lookup"><span data-stu-id="315c8-140">(Included)</span></span> |

<span data-ttu-id="315c8-141">Visual Studio 2010 ile çalışmak için Visual [Studio 2010'da ASP.NET Web Sayfaları için Destek Yükleme'ye](#vs2010support)bakın.</span><span class="sxs-lookup"><span data-stu-id="315c8-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="315c8-142">WebMatrix'ten Visual Studio'nun başlatılması</span><span class="sxs-lookup"><span data-stu-id="315c8-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="315c8-143">WebMatrix'te bir proje başlattıysanız ve Visual Studio'ya geçmek istiyorsanız, WebMatrix projeyi Visual Studio'da kolayca açmak için bir düğme sağlar.</span><span class="sxs-lookup"><span data-stu-id="315c8-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="315c8-144">Bu düğmenin etkin olabilmesi için bilgisayarınızda Visual Studio yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="315c8-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="315c8-145">Aşağıdaki resimde WebMatrix'teki düğme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="315c8-145">The following image shows the button in WebMatrix.</span></span>

![Görsel Stüdyo'da başlat](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="315c8-147">Düğmeyi tıklattığınızda, proje Visual Studio'da açılır.</span><span class="sxs-lookup"><span data-stu-id="315c8-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="315c8-148">WebMatrix ve Visual Studio arasında herhangi bir sorun olmadan geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="315c8-149">Diğer ortamda herhangi bir dosya değiştiyse ve en son değişiklikleri almak için yeniden yüklenmesi gerekiyorsa size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="315c8-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="315c8-150">Visual Studio'da ASP.NET Jilet Sitesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="315c8-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="315c8-151">Visual Studio'da ASP.NET bir Razor web sitesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="315c8-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="315c8-152">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="315c8-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="315c8-153">**Dosya** menüsünde **Yeni Web Sitesi'ni**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-153">In the **File** menu, click **New Web Site**.</span></span>

    ![yeni web sitesi oluşturmak](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="315c8-155">Yeni **Web Sitesi** iletişim kutusunda kullanılacak dili (Visual C# veya Visual Basic) seçin.</span><span class="sxs-lookup"><span data-stu-id="315c8-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="315c8-156">web **sitesi (Razor)** şablonu ASP.NET seçin.</span><span class="sxs-lookup"><span data-stu-id="315c8-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![jilet sitesi](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="315c8-158">**Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="315c8-158">Click **OK**.</span></span>

<span data-ttu-id="315c8-159">Yeni projeniz var ve başlamanıza yardımcı olacak bazı varsayılan web sayfalarıyla doldurulur.</span><span class="sxs-lookup"><span data-stu-id="315c8-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="315c8-160">IntelliSense Kullanma</span><span class="sxs-lookup"><span data-stu-id="315c8-160">Using IntelliSense</span></span>

<span data-ttu-id="315c8-161">Artık bir site oluşturduğunuza göre, IntelliSense'in Visual Studio'da nasıl çalıştığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="315c8-162">Oluşturduğunuz web sitesinde *Varsayılan.cshtml* sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="315c8-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="315c8-163">Sayfadaki `<h3>` etiketlerden sonra `@ServerInfo.` ,(nokta dahil) yazın.</span><span class="sxs-lookup"><span data-stu-id="315c8-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="315c8-164">IntelliSense'in, `ServerInfo` yardımcıiçin kullanılabilir yöntemleri açılır listede nasıl görüntülenebildiğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="315c8-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![ıntellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="315c8-166">Listeden `GetHtml` yöntemi seçin ve sonra Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="315c8-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="315c8-167">IntelliSense yöntemi otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="315c8-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="315c8-168">(C#'daki herhangi bir yöntemde `()` olduğu gibi, yöntemden sonra karakter eklemeniz gerekir.) `GetHtml` Yöntem için tamamlanan kod aşağıdaki örnek gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="315c8-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="315c8-169">Sayfayı çalıştırmak için Ctrl+F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="315c8-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="315c8-170">Bir tarayıcıda görüntülendiğinde sayfa aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="315c8-170">This is what the page looks like when displayed in a browser:</span></span>

    ![tarayıcıda varsayılan sayfa](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="315c8-172">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="315c8-173">Hata Ayıklama'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="315c8-173">Using the Debugger</span></span>

1. <span data-ttu-id="315c8-174">*Default.cshtml* sayfasının üst kısmında, ile başlayan `Page.Title`satırdan sonra, aşağıdaki kod satırını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="315c8-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="315c8-175">Kodun solundaki düzenleyicinin gri kenar boşluğunda, *bir kesme noktası*eklemek için bu yeni satırın yanındaki niyazda bulunun.</span><span class="sxs-lookup"><span data-stu-id="315c8-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="315c8-176">Kesme noktası, hata ayıklayana programı o noktada çalıştırmayı durdurmasını söyleyen bir işaretçidir, böylece neler olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![kesme noktasını ayarlama](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="315c8-178">Aramayı yönteme `ServerInfo.GetHtml` kaldırın ve yerine `@myTime` değişkene bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="315c8-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="315c8-179">Bu çağrı, yeni kod satırı tarafından döndürülen geçerli saat değerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="315c8-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="315c8-180">Sayfayı hata ayıklamada çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="315c8-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="315c8-181">Sayfa ayarladığınız kesme noktasında durur.</span><span class="sxs-lookup"><span data-stu-id="315c8-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="315c8-182">Aşağıdaki resim, sayfanın yazıcıda kesme noktası (sarı renkte) ile nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="315c8-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![hata ayıklama kesme noktası](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="315c8-184">Hata Ayıklama araç çubuğunda, bir sonraki kod satırını çalıştırmak için **Adım adım** düğmesini (veya F11 tuşuna basın) tıklatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="315c8-185">Bu düğmeyi her tıklattığınızda, yürütmeyi bir sonraki kod satırına ilerletin.</span><span class="sxs-lookup"><span data-stu-id="315c8-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Düğmeye bas](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="315c8-187">Fare işaretçinizi `myTime` üzerinde tutarak veya **Yerel Halk** ve **Çağrı Yığını** pencerelerinde görüntülenen değerleri inceleyerek değişkenin değerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="315c8-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="315c8-188">Visual Studio değişkenin değerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="315c8-188">Visual Studio display the value of the variable.</span></span>

    ![zaman değerini göster](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="315c8-190">Değişkeni incelemeyi ve kodu aşmayı bitirdiğinizde, her satırda durmadan sayfayı çalıştırmaya devam etmek için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="315c8-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="315c8-191">Tüm kodu niçin tamamlamayı tamamladığınızda, tarayıcı sayfayı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="315c8-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="315c8-192">Hata ayıklama ve Visual Studio'da kod ayıklama hakkında daha fazla bilgi edinmek [için, Visual Web Developer'da Web Sayfalarını](https://msdn.microsoft.com/library/z9e7w6cs.aspx)Hata Ayıklama bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="315c8-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="315c8-193">Visual Studio ile ASP.NET MVC projelerinde Razor kullanma</span><span class="sxs-lookup"><span data-stu-id="315c8-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="315c8-194">Razor sözdizimi de ASP.NET MVC projelerinde yaygın olarak kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="315c8-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="315c8-195">MVC, dinamik web siteleri oluşturmanın güçlü, desen tabanlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="315c8-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="315c8-196">ASP.NET Web Sayfaları sitenizin bakımı zorlaşırsa, siteyi ASP.NET bir MVC uygulamasına dönüştürmeyi düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="315c8-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="315c8-197">Bir MVC uygulaması oluşturma örneği için, [ASP.NET MVC 5 ile Başlarken'e](../../../mvc/overview/getting-started/introduction/getting-started.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="315c8-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="315c8-198">Visual Studio 2010'da ASP.NET Web Sayfaları için Destek Yükleme</span><span class="sxs-lookup"><span data-stu-id="315c8-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="315c8-199">Bu bölümde Visual Web Developer Express 2010 ve Visual Studio için ASP.NET Web Sayfaları Araçları nasıl yüklenir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="315c8-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="315c8-200">Web Platformu Yükleyici'niz zaten yoksa, aşağıdaki URL'den indirin:</span><span class="sxs-lookup"><span data-stu-id="315c8-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="315c8-201">Web Platform Yükleyicisini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="315c8-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="315c8-202">**Ürünler** sekmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-202">Click the **Products** tab.</span></span>

    ![WebPI Ürünleri sekmesi](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="315c8-204">**MVC 4 ASP.NET** arayın (ASP.NET Web Sayfaları 2 için) ve sonra **Ekle'yi**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="315c8-205">Bu ürünler ASP.NET Razor web siteleri oluşturmak için Visual Studio araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="315c8-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi yükleme seçenekleri](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="315c8-207">Yüklemeyi tamamlamak için **Yükle'yi** tıklatın.</span><span class="sxs-lookup"><span data-stu-id="315c8-207">Click **Install** to complete the installation.</span></span>
