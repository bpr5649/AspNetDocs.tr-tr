---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC'ye giriş | Microsoft Docs
author: shanselman
description: ASP.NET MVC ile ilgili temel bilgileri tanıtan bir başlangıç Öğreticisi budur. Okuyan ve yazan bir veritabanından basit bir web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: dcc2e703829cfa0b77575870feff451fd0738f56
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416499"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="11e30-104">ASP.NET MVC’ye Giriş</span><span class="sxs-lookup"><span data-stu-id="11e30-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="11e30-105">tarafından [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="11e30-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="11e30-106">Bu öğreticide kullanılabiliyorsa, güncelleştirilmiş bir sürümünü [burada](../../getting-started/introduction/getting-started.md) kullanarak [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span><span class="sxs-lookup"><span data-stu-id="11e30-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="11e30-107">Bu öğretici birçok iyileştirme sağlayan ASP.NET MVC 5 yeni öğretici kullanır.</span><span class="sxs-lookup"><span data-stu-id="11e30-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="11e30-108">ASP.NET MVC ile ilgili temel bilgileri tanıtan bir başlangıç Öğreticisi budur.</span><span class="sxs-lookup"><span data-stu-id="11e30-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="11e30-109">Okuyan ve yazan bir veritabanından basit bir web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="11e30-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="11e30-110">Ziyaret [ASP.NET MVC eğitim Merkezi](../../../index.md) diğer ASP.NET MVC, öğreticilerimiz ve örneklerimizden bulunacak.</span><span class="sxs-lookup"><span data-stu-id="11e30-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="11e30-111">Bizim ilk ASP.NET MVC Web uygulaması kullanarak olalım [Visual Web Developer 2010 Express'i](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="11e30-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="11e30-112">Bize oluşturun ve filmler listesinde biraz film listesi uygulaması oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="11e30-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="11e30-113">Ne oluşturacaksınız</span><span class="sxs-lookup"><span data-stu-id="11e30-113">What You'll Build</span></span>

<span data-ttu-id="11e30-114">Aşağıda oluşturacağınız uygulama iki ekran görüntüleri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="11e30-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="11e30-115">Film çeşitli sütunları içeren basit bir tablo gerekir.</span><span class="sxs-lookup"><span data-stu-id="11e30-115">You will have a simple table of movies with various columns.</span></span>

[![M<span data-ttu-id="11e30-116">ovie liste - Windows Internet Explorer (12)]</span><span class="sxs-lookup"><span data-stu-id="11e30-116">ovie List - Windows Internet Explorer (12)]</span></span>(getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

<span data-ttu-id="11e30-117">Ve filmler listesine ekleyebilirsiniz oluşturma Form sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="11e30-117">And you'll have a Create Form so we can add movies to the list.</span></span>

[![C<span data-ttu-id="11e30-118">Windows Internet Explorer (2) bir filmi - Oluştur]</span><span class="sxs-lookup"><span data-stu-id="11e30-118">reate a Movie - Windows Internet Explorer (2)]</span></span>(getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="11e30-119">Beceriler hakkında bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="11e30-119">Skills You'll Learn</span></span>

<span data-ttu-id="11e30-120">Bu öğreticide Visual Studio kullanarak bir ASP.NET MVC Web uygulaması oluşturmaya yönelik temel bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="11e30-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="11e30-121">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="11e30-121">You'll learn:</span></span>

- <span data-ttu-id="11e30-122">Yeni bir ASP.NET MVC projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="11e30-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="11e30-123">SQL Server ile yeni bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="11e30-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="11e30-124">ASP.NET MVC denetleyicileri ve görünümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="11e30-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="11e30-125">Nasıl alınacağını ve verileri görüntüle</span><span class="sxs-lookup"><span data-stu-id="11e30-125">How to retrieve and display data</span></span>
- <span data-ttu-id="11e30-126">Verileri düzenleme ve veri doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="11e30-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="11e30-127">Veritabanı şemasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="11e30-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="11e30-128">Başlarken</span><span class="sxs-lookup"><span data-stu-id="11e30-128">Get Started</span></span>

<span data-ttu-id="11e30-129">Visual Web Developer 2010 (ben bunu "VWD" andan itibaren ararız) Express ve yeni bir proje seçin, başlangıç ekranından çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="11e30-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="11e30-130">Visual Web Developer, bir IDE veya tümleşik Geliştirici Ortamı ' dir.</span><span class="sxs-lookup"><span data-stu-id="11e30-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="11e30-131">Belgeler yazmak için Microsoft Word kullanma gibi bir IDE uygulamalar oluşturmak için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="11e30-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="11e30-132">Araç, hem de de kullanmış dosyasına seçin menü için çeşitli seçenekler kullanılabilir gösteren üstünde yok | Yeni bir proje.</span><span class="sxs-lookup"><span data-stu-id="11e30-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

[![M<span data-ttu-id="11e30-133">icrosoft Visual Web Developer 2010 Express'i]</span><span class="sxs-lookup"><span data-stu-id="11e30-133">icrosoft Visual Web Developer 2010 Express]</span></span>(getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="11e30-134">İlk uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="11e30-134">Creating Your First Application</span></span>

<span data-ttu-id="11e30-135">Visual Basic veya Visual C# kullanarak uygulamalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11e30-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="11e30-136">Şimdilik seçin Visual C# solda, ardından "ASP.NET MVC 2 Web uygulaması." seçin</span><span class="sxs-lookup"><span data-stu-id="11e30-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="11e30-137">"Film" projenizi adlandırın ve Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="11e30-137">Name your project "Movies" and click OK.</span></span>

[![N<span data-ttu-id="11e30-138">Yeni Proje]</span><span class="sxs-lookup"><span data-stu-id="11e30-138">ew Project]</span></span>(getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

<span data-ttu-id="11e30-139">Sağ tarafta tüm dosya ve klasörlerin uygulamanızda gösteren Çözüm Gezgini ' dir.</span><span class="sxs-lookup"><span data-stu-id="11e30-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="11e30-140">Büyük ortada, kodunuzu düzenleyin ve zamanınızın çoğunu harcama penceredir.</span><span class="sxs-lookup"><span data-stu-id="11e30-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="11e30-141">Çalışan bir uygulama şu anda hiçbir şey yapmadan sahip olduğunuz visual Studio ASP.NET MVC projesi için az önce oluşturduğunuz varsayılan bir şablon kullanılan!</span><span class="sxs-lookup"><span data-stu-id="11e30-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="11e30-142">Bu, bir basit "Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="11e30-142">This is a simple "Hello World!</span></span> <span data-ttu-id="11e30-143">Proje ve uygulamamız için başlatmak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="11e30-143">project, and it is a good place to start for our application.</span></span>

[![M<span data-ttu-id="11e30-144">icrosoft Visual Web Developer 2010 Express'i]</span><span class="sxs-lookup"><span data-stu-id="11e30-144">icrosoft Visual Web Developer 2010 Express]</span></span>(getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

<span data-ttu-id="11e30-145">Araç çubuğu "yürütme" düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="11e30-145">Select the "play" button to the toolbar.</span></span>

![Hata Ayıklamayı Başlat](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="11e30-147">Bu, programı derleyin ve uygulamanızı bir web tarayıcısında başlatın sağ işaret eden yeşil bir ok olur.</span><span class="sxs-lookup"><span data-stu-id="11e30-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

*<span data-ttu-id="11e30-148">NOT: Bunun yerine, klavyenizde F5 tuşuna basın veya hata ayıklama - seçin&gt;hata ayıklamaya Başla "Debug" menüsünden.</span><span class="sxs-lookup"><span data-stu-id="11e30-148">NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.</span></span>*

<span data-ttu-id="11e30-149">Bu, bir geliştirme web sunucusunu başlatmak ve web uygulamamıza (yapılandırma veya yoktur bunu etkinleştirmek için gerekli adımları el ile) çalıştırmak Visual Web Developer neden olur.</span><span class="sxs-lookup"><span data-stu-id="11e30-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="11e30-150">Ardından bir tarayıcıyı başlatın ve uygulamanın giriş sayfası göz atmak için yapılandırmanız.</span><span class="sxs-lookup"><span data-stu-id="11e30-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="11e30-151">Aşağıda tarayıcının adres çubuğuna "localhost" ve example.com şöyle diyor dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="11e30-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="11e30-152">Bu durumda yalnızca oluşturulan uygulama çalıştıran kendi yerel bilgisayar için - her zaman localhost işaret eder olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="11e30-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

[![H<span data-ttu-id="11e30-153">Sayfa v]</span><span class="sxs-lookup"><span data-stu-id="11e30-153">ome Page]</span></span>(getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

<span data-ttu-id="11e30-154">Kullanıma hazır, bu varsayılan şablonu ziyaret etmek için iki sayfa ve bir temel oturum açma sayfası sunar.</span><span class="sxs-lookup"><span data-stu-id="11e30-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="11e30-155">Şimdi bu uygulamayı nasıl çalıştığını değiştirmek ve biraz işlemde ASP.NET MVC hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="11e30-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="11e30-156">Tarayıcınızı kapatın ve bazı kod değiştirme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="11e30-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="11e30-157">Next</span><span class="sxs-lookup"><span data-stu-id="11e30-157">Next</span></span>](getting-started-with-mvc-part2.md)
