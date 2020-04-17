---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Yeni bir ASP.NET MVC Projesi Oluşturma | Microsoft Dokümanlar
author: rick-anderson
description: Adım 1, temel NerdDinner uygulama yapısını nasıl yerleştirdiğinizi gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541487"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="e80d5-103">Yeni ASP.NET MVC Projesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="e80d5-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="e80d5-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="e80d5-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e80d5-105">PDF’yi İndir</span><span class="sxs-lookup"><span data-stu-id="e80d5-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e80d5-106">Bu adım 1 ücretsiz bir ["NerdDinner" uygulama öğretici](introducing-the-nerddinner-tutorial.md) nasıl küçük, ama tam, web uygulaması ASP.NET MVC 1 kullanarak oluşturmak için yürüyüşler olduğunu.</span><span class="sxs-lookup"><span data-stu-id="e80d5-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e80d5-107">Adım 1, temel NerdDinner uygulama yapısını nasıl yerleştirdiğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="e80d5-108">MVC 3 ASP.NET kullanıyorsanız, [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) eğitimlerini takip edersiniz.</span><span class="sxs-lookup"><span data-stu-id="e80d5-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="e80d5-109">NerdDinner Adım 1:&gt;Dosya- Yeni Proje</span><span class="sxs-lookup"><span data-stu-id="e80d5-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="e80d5-110">Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express içindeki **Dosya-Yeni&gt;Proje** menü öğesini seçerek NerdDinner uygulamamıza başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="e80d5-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="e80d5-111">Bu "Yeni Proje" iletişim kutusunu gündeme getirecektir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="e80d5-112">Yeni bir ASP.NET MVC uygulaması oluşturmak için, iletişim kutusunun sol tarafındaki "Web" düğümünü ve ardından sağdaki "ASP.NET MVC Web Uygulaması" proje şablonu seçilir:</span><span class="sxs-lookup"><span data-stu-id="e80d5-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="e80d5-113">*Önemli: MVC ASP.NET indirdiğinizde ve yüklediğinizden emin olun , aksi takdirde Yeni Proje iletişim kutusunda gösterilmez. Henüz yüklemediyseniz [Microsoft Web Platform Installer'ın](https://www.microsoft.com/web/downloads/platform.aspx) V2'sini kullanabilirsiniz (ASP.NET MVC",&gt;"Web Platformu- Çerçeveler ve Çalışma Saatleri" bölümünde kullanılabilir).*</span><span class="sxs-lookup"><span data-stu-id="e80d5-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="e80d5-114">"NerdDinner" oluşturacağız ve oluşturmak için "ok" düğmesine tıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="e80d5-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="e80d5-115">"Ok" Visual Studio'yu tıklattığımızda, yeni uygulama için de isteğe bağlı olarak bir birim test projesi oluşturmamızı gerektiren ek bir iletişim formu gündeme gelecektir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="e80d5-116">Bu birim test projesi, uygulamamızın işlevselliğini ve davranışını doğrulayan otomatik testler oluşturmamıza olanak tanır (bu öğreticide daha sonra nasıl yapılacağını ele alacağız).</span><span class="sxs-lookup"><span data-stu-id="e80d5-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="e80d5-117">Yukarıdaki iletişim kutusundaki "Test çerçevesi" açılır bırakım, makineye yüklenen tüm kullanılabilir ASP.NET MVC birim test proje şablonlarıyla doldurulur.</span><span class="sxs-lookup"><span data-stu-id="e80d5-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="e80d5-118">Sürümler NUnit, MBUnit ve XUnit için indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="e80d5-119">Dahili Visual Studio Unit Test çerçevesi de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="e80d5-120">*Not: Visual Studio Unit Test Framework sadece Visual Studio 2008 Professional ve daha yüksek sürümlerle kullanılabilir. VS 2008 Standard Edition veya Visual Web Developer 2008 Express kullanıyorsanız, bu iletişim kutusunun gösterilebilmesi için ASP.NET MVC için NUnit, MBUnit veya XUnit uzantılarını indirmeniz ve yüklemeniz gerekir. Yüklü herhangi bir test çerçevesi yoksa iletişim kutusu görüntülenmez.*</span><span class="sxs-lookup"><span data-stu-id="e80d5-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="e80d5-121">Oluşturduğumuz test projesi için varsayılan "NerdDinner.Tests" adını ve "Visual Studio Unit Test" çerçeve seçeneğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e80d5-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="e80d5-122">"Ok" düğmesine tıkladığımızda Visual Studio bizim için iki proje ile bir çözüm yaratacak - bir web uygulaması ve birim testleri için bir:</span><span class="sxs-lookup"><span data-stu-id="e80d5-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="e80d5-123">NerdDinner dizin yapısının incelenmesi</span><span class="sxs-lookup"><span data-stu-id="e80d5-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="e80d5-124">Visual Studio ile yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, projeye otomatik olarak bir dizi dosya ve dizin ekler:</span><span class="sxs-lookup"><span data-stu-id="e80d5-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="e80d5-125">ASP.NET MVC projelerinin varsayılan olarak altı üst düzey dizini bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="e80d5-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="e80d5-126">**Dizin**</span><span class="sxs-lookup"><span data-stu-id="e80d5-126">**Directory**</span></span> | <span data-ttu-id="e80d5-127">**Amaç**</span><span class="sxs-lookup"><span data-stu-id="e80d5-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="e80d5-128">**/Denetleyiciler**</span><span class="sxs-lookup"><span data-stu-id="e80d5-128">**/Controllers**</span></span> | <span data-ttu-id="e80d5-129">URL isteklerini işleyen Denetleyici sınıflarını nereye koyduğunuz</span><span class="sxs-lookup"><span data-stu-id="e80d5-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="e80d5-130">**/Modeller**</span><span class="sxs-lookup"><span data-stu-id="e80d5-130">**/Models**</span></span> | <span data-ttu-id="e80d5-131">Verileri temsil eden ve işleyen sınıfları koyduğunuz yer</span><span class="sxs-lookup"><span data-stu-id="e80d5-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="e80d5-132">**/Görünümler**</span><span class="sxs-lookup"><span data-stu-id="e80d5-132">**/Views**</span></span> | <span data-ttu-id="e80d5-133">Çıktı oluşturmadan sorumlu UI şablon dosyalarını nereye koyduğunuz</span><span class="sxs-lookup"><span data-stu-id="e80d5-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="e80d5-134">**/Komut Dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e80d5-134">**/Scripts**</span></span> | <span data-ttu-id="e80d5-135">JavaScript kitaplık dosyalarını ve komut dosyalarını koyduğunuz yer (.js)</span><span class="sxs-lookup"><span data-stu-id="e80d5-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="e80d5-136">**/İçerik**</span><span class="sxs-lookup"><span data-stu-id="e80d5-136">**/Content**</span></span> | <span data-ttu-id="e80d5-137">CSS ve resim dosyalarını ve diğer dinamik olmayan/JavaScript olmayan içeriği koyduğunuz yer</span><span class="sxs-lookup"><span data-stu-id="e80d5-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="e80d5-138">**/Uygulama\_Verileri**</span><span class="sxs-lookup"><span data-stu-id="e80d5-138">**/App\_Data**</span></span> | <span data-ttu-id="e80d5-139">Okumak/yazmak istediğiniz veri dosyalarını depoladığınız yer.</span><span class="sxs-lookup"><span data-stu-id="e80d5-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="e80d5-140">ASP.NET MVC bu yapıyı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="e80d5-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="e80d5-141">Aslında, büyük uygulamalar üzerinde çalışan geliştiriciler genellikle uygulamayı daha yönetilebilir hale getirmek için genellikle birden çok projeye bölümlere ayırır (örneğin: veri modeli sınıfları genellikle web uygulamasından ayrı bir sınıf kitaplığı projesine gider).</span><span class="sxs-lookup"><span data-stu-id="e80d5-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="e80d5-142">Ancak varsayılan proje yapısı, uygulama sorunlarımızı temiz tutmak için kullanabileceğimiz hoş bir varsayılan dizin kuralı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e80d5-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="e80d5-143">/Controllers dizinini genişletdiğimizde Visual Studio'nun projeye varsayılan olarak iki denetleyici sınıfı -HomeController ve AccountController- eklediğini göreceğiz:</span><span class="sxs-lookup"><span data-stu-id="e80d5-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="e80d5-144">/Görünüm dizini genişlettiğinde, üç alt dizin (/Ana Sayfa, /Hesap ve /Paylaşılan) yanı sıra bunların içinde birkaç şablon dosyası da varsayılan olarak projeye eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="e80d5-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="e80d5-145">/İçerik ve /Scriptds dizinlerini genişletdiğimizde, sitedeki tüm HTML'leri stillemek için kullanılan bir Site.css dosyasının yanı sıra uygulama içinde ASP.NET AJAX ve jQuery desteğine olanak tanıyan JavaScript kitaplıklarını da buluruz:</span><span class="sxs-lookup"><span data-stu-id="e80d5-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="e80d5-146">NerdDinner.Tests projesini genişletirken denetleyici sınıflarımız için birim testleri içeren iki sınıf bulacağız:</span><span class="sxs-lookup"><span data-stu-id="e80d5-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="e80d5-147">Visual Studio tarafından eklenen bu varsayılan dosyalar bize çalışan bir uygulama için temel bir yapı sağlar - ana sayfa, sayfa hakkında, hesap giriş/giriş/kayıt sayfaları ve işlenmemiş bir hata sayfası (hepsi kablolu ve kutunun dışında çalışma) ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="e80d5-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="e80d5-148">NerdDinner Uygulamasını Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e80d5-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="e80d5-149">Hata **Ayıklama başlat veya&gt;Hata Ayıklama-** **&gt;Hata Ayıklama** menüsü öğelerini seçmeden projeyi çalıştırabiliriz:</span><span class="sxs-lookup"><span data-stu-id="e80d5-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="e80d5-150">Bu, Visual Studio ile birlikte gelen yerleşik ASP.NET Web sunucusunu başlatacak ve uygulamamızı çalıştıracaktır:</span><span class="sxs-lookup"><span data-stu-id="e80d5-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="e80d5-151">Yeni projemizin ana sayfası (URL: "/") çalıştığında:</span><span class="sxs-lookup"><span data-stu-id="e80d5-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="e80d5-152">"Hakkında" sekmesine tıkladığınızda bir sayfa görüntülenir (URL: "/Ana Sayfa/Hakkında"):</span><span class="sxs-lookup"><span data-stu-id="e80d5-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="e80d5-153">Sağ üstteki "Oturum Aç" bağlantısına tıkladığınızda giriş sayfası (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="e80d5-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="e80d5-154">Giriş hesabımız yoksa, aşağıdakileri oluşturmak için kayıt bağlantısını (URL: "/Account/Register") tıklayabiliriz:</span><span class="sxs-lookup"><span data-stu-id="e80d5-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="e80d5-155">Yeni projemizi oluşturduğumuzda, yukarıdaki ev, hakkında ve oturum açma/kayıt işlevini uygulamak için kod varsayılan olarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="e80d5-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="e80d5-156">Uygulamamızın başlangıç noktası olarak kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e80d5-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="e80d5-157">NerdDinner Uygulamasını Test Etme</span><span class="sxs-lookup"><span data-stu-id="e80d5-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="e80d5-158">Visual Studio 2008'in Professional Edition veya daha yüksek sürümünü kullanıyorsak, projeyi test etmek için Visual Studio'daki yerleşik birim test IDE desteğini kullanabiliriz:</span><span class="sxs-lookup"><span data-stu-id="e80d5-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="e80d5-159">Yukarıdaki seçeneklerden birini seçmek IDE içindeki "Test Sonuçları" bölmesini açacak ve yerleşik işlevselliği kapsayan yeni projemizde yer alan 27 birim testinde geçiş/başarısız durumu sağlayacaktır:</span><span class="sxs-lookup"><span data-stu-id="e80d5-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="e80d5-160">Bu öğreticinin ilerleyen saatlerinde otomatik sınama hakkında daha fazla konuşacağız ve uyguladığımız uygulama işlevselliğini kapsayan ek birim testleri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="e80d5-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="e80d5-161">Sonraki Adım</span><span class="sxs-lookup"><span data-stu-id="e80d5-161">Next Step</span></span>

<span data-ttu-id="e80d5-162">Şu anda temel bir uygulama yapısına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e80d5-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="e80d5-163">Şimdi uygulama [verilerimizi depolamak için bir veritabanı oluşturalım.](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="e80d5-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e80d5-164">[Önceki](introducing-the-nerddinner-tutorial.md)
> [Sonraki](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="e80d5-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
