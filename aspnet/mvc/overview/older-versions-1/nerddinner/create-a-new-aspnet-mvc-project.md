---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Yeni bir ASP.NET MVC projesi oluştur | Microsoft Docs
author: microsoft
description: 1\. adım temel Nerdakşam yemeği uygulama yapısını yerinde nasıl koyabileceğiniz gösterilmektedir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580936"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="7df50-103">Yeni ASP.NET MVC Projesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="7df50-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="7df50-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="7df50-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7df50-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="7df50-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7df50-106">Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 1. adımından oluşur.</span><span class="sxs-lookup"><span data-stu-id="7df50-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="7df50-107">1\. adım temel Nerdakşam yemeği uygulama yapısını yerinde nasıl koyabileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7df50-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="7df50-108">ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="7df50-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="7df50-109">Nerdakşam yemeği adım 1: dosya-&gt;yeni proje</span><span class="sxs-lookup"><span data-stu-id="7df50-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="7df50-110">Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express içinde **dosya&gt;yeni proje** menü öğesini seçerek Nerdakşam yemeği uygulamamıza başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="7df50-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="7df50-111">Bu, "yeni proje" iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="7df50-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="7df50-112">Yeni bir ASP.NET MVC uygulaması oluşturmak için, iletişim kutusunun sol tarafındaki "Web" düğümünü seçip sağdaki "ASP.NET MVC web uygulaması" proje şablonunu seçeceğiz:</span><span class="sxs-lookup"><span data-stu-id="7df50-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="7df50-113">*Önemli: ASP.NET MVC 'yi indirdiğinizden ve yüklediğinizden emin olun; Aksi takdirde yeni proje iletişim kutusunda gösterilmez. Henüz yüklemediyseniz [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) v2 'yi kullanabilirsiniz (ASP.NET MVC, "Web platformu-&gt;çerçeveleri ve çalışma zamanları" bölümünde bulunur).*</span><span class="sxs-lookup"><span data-stu-id="7df50-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="7df50-114">"Nerdakşam yemeği" oluşturacağımız yeni projeyi adlandırın ve ardından oluşturmak için "Tamam" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7df50-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="7df50-115">"Tamam" seçeneğine tıkladığımızda, Visual Studio, isteğe bağlı olarak yeni uygulama için bir birim testi projesi oluşturmamızı isteyen ek bir iletişim kutusu getirir.</span><span class="sxs-lookup"><span data-stu-id="7df50-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="7df50-116">Bu birim testi projesi, uygulamamızın işlevlerini ve davranışını doğrulayan otomatikleştirilmiş testler oluşturmamızı sağlar (Bu öğreticide daha sonra yapılacak nasıl yapılacağını ele alacağız).</span><span class="sxs-lookup"><span data-stu-id="7df50-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="7df50-117">Yukarıdaki iletişim kutusundaki "test çerçevesi" açılan menüsü, makinede yüklü olan tüm ASP.NET MVC birim test projesi şablonları ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="7df50-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="7df50-118">Sürümler NUnit, MBUnit ve XUnit için indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7df50-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="7df50-119">Yerleşik Visual Studio birim test çerçevesi de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7df50-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="7df50-120">*Note: Visual Studio birim testi çerçevesi yalnızca Visual Studio 2008 Professional ve daha yeni sürümlerde kullanılabilir. VS 2008 Standard Edition veya Visual Web Developer 2008 Express kullanıyorsanız, bu iletişim kutusunun gösterilmesi için NUnit, MBUnit veya XUnit uzantıları ASP.NET MVC için indirmeniz ve yüklemeniz gerekir. Yüklü herhangi bir test çerçevesi yoksa iletişim kutusu görüntülenmez.*</span><span class="sxs-lookup"><span data-stu-id="7df50-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="7df50-121">Oluşturduğumuz test projesi için varsayılan "Nerdakşam yemeği. Tests" adını kullanacağız ve "Visual Studio birim testi" çerçeve seçeneğini kullanırız.</span><span class="sxs-lookup"><span data-stu-id="7df50-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="7df50-122">"Tamam" düğmesine tıkladığımızda, Visual Studio, web uygulamamız ve birim testlerimiz için bir tane olmak üzere iki proje ile bizim için bir çözüm oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="7df50-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="7df50-123">Nerdakşam yemeği dizin yapısını İnceleme</span><span class="sxs-lookup"><span data-stu-id="7df50-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="7df50-124">Visual Studio ile yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, projeye otomatik olarak bir dizi dosya ve dizin ekler:</span><span class="sxs-lookup"><span data-stu-id="7df50-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="7df50-125">ASP.NET MVC projeleri varsayılan olarak altı üst düzey dizine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7df50-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="7df50-126">**Dizinden**</span><span class="sxs-lookup"><span data-stu-id="7df50-126">**Directory**</span></span> | <span data-ttu-id="7df50-127">**Amaç**</span><span class="sxs-lookup"><span data-stu-id="7df50-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="7df50-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="7df50-128">**/Controllers**</span></span> | <span data-ttu-id="7df50-129">URL isteklerini işleyen denetleyici sınıflarını yerleştirdiğiniz yer</span><span class="sxs-lookup"><span data-stu-id="7df50-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="7df50-130">**/Modeller**</span><span class="sxs-lookup"><span data-stu-id="7df50-130">**/Models**</span></span> | <span data-ttu-id="7df50-131">Verileri temsil eden ve işleyen sınıfları yerleştirdiğiniz yer</span><span class="sxs-lookup"><span data-stu-id="7df50-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="7df50-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="7df50-132">**/Views**</span></span> | <span data-ttu-id="7df50-133">Çıktı işlemeden sorumlu Kullanıcı Arabirimi şablon dosyalarını yerleştirdiğiniz yerdir</span><span class="sxs-lookup"><span data-stu-id="7df50-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="7df50-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="7df50-134">**/Scripts**</span></span> | <span data-ttu-id="7df50-135">JavaScript kitaplığı dosyalarını ve komut dosyalarını (. js) yerleştirdiğiniz yer</span><span class="sxs-lookup"><span data-stu-id="7df50-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="7df50-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="7df50-136">**/Content**</span></span> | <span data-ttu-id="7df50-137">CSS ve resim dosyalarını ve dinamik olmayan/JavaScript olmayan diğer içeriği yerleştirdiğiniz yer</span><span class="sxs-lookup"><span data-stu-id="7df50-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="7df50-138">**/App\_verileri**</span><span class="sxs-lookup"><span data-stu-id="7df50-138">**/App\_Data**</span></span> | <span data-ttu-id="7df50-139">Okumak/yazmak istediğiniz veri dosyalarını depoladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="7df50-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="7df50-140">ASP.NET MVC bu yapıyı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="7df50-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="7df50-141">Aslında, büyük uygulamalar üzerinde çalışan geliştiriciler genellikle uygulamayı daha yönetilebilir hale getirmek için birden fazla proje genelinde bölümleyebilir (örneğin: veri modeli sınıfları, genellikle Web uygulamasından ayrı bir sınıf kitaplığı projesine gider).</span><span class="sxs-lookup"><span data-stu-id="7df50-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="7df50-142">Bununla birlikte, varsayılan proje yapısı, uygulama kaygılarını temiz tutmak için kullanabilmemiz için iyi bir varsayılan dizin kuralı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7df50-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="7df50-143">/Controllers dizinini genişlettiğimiz zaman, Visual Studio 'Nun iki denetleyici sınıfı (varsayılan olarak, giriş denetleyicisi ve AccountController) eklediğini bulacağız:</span><span class="sxs-lookup"><span data-stu-id="7df50-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="7df50-144">/Views dizinini genişlettiğimiz sırada üç alt dizin bulunur:/Home,/Account ve/Shared – Ayrıca, içindeki çeşitli şablon dosyaları da projeye varsayılan olarak eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="7df50-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="7df50-145">/Content ve/Scripts dizinlerini genişlettiğimiz zaman, sitedeki tüm HTML 'yi (Ayrıca, uygulamada ASP.NET AJAX ve jQuery desteğini etkinleştirebileceği JavaScript kitaplıklarını) bir site. css dosyası bulacağız:</span><span class="sxs-lookup"><span data-stu-id="7df50-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="7df50-146">Nerdakşam yemeği. Tests projesini genişlettiğimiz zaman denetleyici sınıflarımız için birim testlerini içeren iki sınıf bulacaksınız:</span><span class="sxs-lookup"><span data-stu-id="7df50-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="7df50-147">Visual Studio tarafından eklenen bu varsayılan dosyalar bize, çalışan bir uygulama için temel bir yapı ve giriş sayfası, sayfa, hesap oturumu açma/kayıt sayfaları ve işlenmemiş bir hata sayfası (tüm kablolu ve kutudan çıkar) sağlar.</span><span class="sxs-lookup"><span data-stu-id="7df50-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="7df50-148">Nerdakşam yemeği uygulamasını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7df50-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="7df50-149">Hata **Ayıkla-&gt;Başlat** veya **hata ayıkla-&gt;** hata ayıklama menü öğelerinden birini seçerek projeyi çalıştırabiliriz:</span><span class="sxs-lookup"><span data-stu-id="7df50-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="7df50-150">Bu işlem, Visual Studio ile birlikte gelen yerleşik ASP.NET Web sunucusunu başlatır ve uygulamamızı çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="7df50-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="7df50-151">Yeni Projemiz için giriş sayfası (URL: "/") çalışırken aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7df50-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="7df50-152">"Hakkında" sekmesine tıklanması hakkında bir sayfa (URL: "/Home/About") görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="7df50-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="7df50-153">Sağ üst taraftaki "oturum aç" bağlantısına tıkladığınızda bir oturum açma sayfası (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="7df50-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="7df50-154">Bir oturum açma hesabınız yoksa, oluşturmak için kayıt bağlantısına tıklayeceğiz (URL: "/Account/Register"):</span><span class="sxs-lookup"><span data-stu-id="7df50-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="7df50-155">Yeni projemizi oluşturduğumuzda, yukarıdaki giriş, hakkında ve oturum kapatma/kaydetme işlevlerini uygulamak için kod varsayılan olarak eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="7df50-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="7df50-156">Bunu uygulamamız başlangıç noktası olarak kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7df50-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="7df50-157">Nerdakşam yemeği uygulamasını test etme</span><span class="sxs-lookup"><span data-stu-id="7df50-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="7df50-158">Visual Studio 2008 ' nin Professional sürümünü veya daha yüksek bir sürümünü kullandığımızda, Visual Studio içinde yerleşik birim testi IDE desteğini kullanarak projeyi test edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7df50-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="7df50-159">Yukarıdaki seçeneklerden birini seçmek, IDE 'nin içindeki "Test Sonuçları" bölmesini açar ve yeni projemizdeki yerleşik işlevselliği kapsayan 27 birim testlerinde Pass/Fail durumu sağlar:</span><span class="sxs-lookup"><span data-stu-id="7df50-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="7df50-160">Bu öğreticide daha sonra otomatikleştirilmiş test hakkında daha fazla konuşacak ve uyguladığımız uygulama işlevselliğini kapsayan ek birim testleri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="7df50-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="7df50-161">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="7df50-161">Next Step</span></span>

<span data-ttu-id="7df50-162">Artık temel bir uygulama yapısı sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="7df50-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="7df50-163">Şimdi [uygulama Verilerimizi depolamak için bir veritabanı oluşturalım](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="7df50-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7df50-164">[Önceki](introducing-the-nerddinner-tutorial.md)
> [İleri](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="7df50-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
