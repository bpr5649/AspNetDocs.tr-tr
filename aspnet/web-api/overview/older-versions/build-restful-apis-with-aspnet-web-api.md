---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API - ASP.NET ile RESTful API'leri oluşturmak 4.x
author: rick-anderson
description: "Uygulamalı Laboratuvar: ASP.NET Web API'sini kullanan bir kişi manager uygulaması için basit bir REST API oluşturmak için 4.x."
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132260"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="deacd-103">ASP.NET Web API ile RESTful API'leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="deacd-104">Tarafından [Team Web Kampları](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="deacd-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="deacd-105">Uygulamalı Laboratuvar: ASP.NET Web API'sini kullanan bir kişi manager uygulaması için basit bir REST API oluşturmak için 4.x.</span><span class="sxs-lookup"><span data-stu-id="deacd-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="deacd-106">Ayrıca, API'yi kullanmak için bir istemci oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="deacd-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="deacd-107">Son yıllarda, HTML sayfaları yalnızca hizmet vermek için HTTP değil olduğu açıkça görülmektedir oldu.</span><span class="sxs-lookup"><span data-stu-id="deacd-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="deacd-108">Ayrıca birkaç fiiller (GET, POST vb.) gibi birkaç basit kavramları kullanarak Web API'leri oluşturmaya yönelik güçlü bir platform olan *URI'ler* ve *üstbilgileri*.</span><span class="sxs-lookup"><span data-stu-id="deacd-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="deacd-109">ASP.NET Web API HTTP programlamayı bileşenleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="deacd-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="deacd-110">ASP.NET MVC çalışma zamanı üzerine inşa edildiğinden, Web API HTTP alt düzey aktarım ayrıntılarını otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="deacd-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="deacd-111">Aynı zamanda, Web API'si, doğal olarak HTTP programlama modeli sunar.</span><span class="sxs-lookup"><span data-stu-id="deacd-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="deacd-112">Aslında, bir Web API'sinin olmaktır *değil* hemen HTTP gerçekte soyut.</span><span class="sxs-lookup"><span data-stu-id="deacd-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="deacd-113">Sonuç olarak, Web API'si genişletmek kolay ve esnek.</span><span class="sxs-lookup"><span data-stu-id="deacd-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="deacd-114">Bunu kesinlikle HTTP yalnızca geçerli bir yaklaşım olmasa da HTTP - yararlanmak için verimli bir yöntem olabilir REST mimari stili kanıtlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="deacd-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="deacd-115">Kişi Yöneticisi, listeleme, ekleme ve kaldırma kişiler, diğerlerinin yanı sıra RESTful açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="deacd-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="deacd-116">Bu Laboratuvar, HTTP, REST, temel bir anlayış gerektirir ve HTML, JavaScript ve jQuery temel bilgiye sahip olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="deacd-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="deacd-117">ASP.NET Web sitesinde ASP.NET Web API çerçevesi ayrılmış bir alan yok [ https://asp.net/web-api ](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="deacd-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="deacd-118">Bu site, en son haberler, örnekler ve Web API'si için ilgili Haberler şekilde kontrol edin, sık sağlamaya devam edecek içine neredeyse tüm cihaz veya geliştirme framework kullanılabilir özel Web API'leri oluşturmanın son teknoloji ürünü derin delve istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="deacd-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="deacd-119">ASP.NET Web API, ASP.NET MVC 4'e benzer birkaç kullanılabilir bağımlılık ekleme çerçevesini oldukça kolay kullanmanıza olanak sağlayan denetleyicilerinden Hizmet katmanını ayırarak açısından harika esnekliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="deacd-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="deacd-120">Olduğu iyi bir örnek için bağımlılık ekleme buradan indirebileceğiniz bir ASP.NET Web API projesinde Ninject kullanmayı gösterir MSDN [burada](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span><span class="sxs-lookup"><span data-stu-id="deacd-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="deacd-121">Web Kampları eğitim Seti, kullanılabilir tüm örnek kodu ve kod parçacıkları dahil [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="deacd-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="deacd-122">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="deacd-122">Objectives</span></span>

<span data-ttu-id="deacd-123">Bu uygulamalı laboratuvarda, öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="deacd-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="deacd-124">RESTful Web API'si uygulama</span><span class="sxs-lookup"><span data-stu-id="deacd-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="deacd-125">Bir HTML istemcisinde API çağırma</span><span class="sxs-lookup"><span data-stu-id="deacd-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="deacd-126">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="deacd-126">Prerequisites</span></span>

<span data-ttu-id="deacd-127">Aşağıda bu uygulamalı laboratuvarı tamamlamak için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="deacd-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="deacd-128">[Web için Visual Studio Express 2012 Microsoft](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) veya üst (okuma [ek B](#AppendixB) nasıl yükleneceği hakkında yönergeler için).</span><span class="sxs-lookup"><span data-stu-id="deacd-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="deacd-129">Kurulum</span><span class="sxs-lookup"><span data-stu-id="deacd-129">Setup</span></span>

<span data-ttu-id="deacd-130">**Kod parçacıkları yükleniyor**</span><span class="sxs-lookup"><span data-stu-id="deacd-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="deacd-131">Kolaylık olması için bu Laboratuvar yöneteceğiniz kodun çoğu Visual Studio kod parçacıkları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="deacd-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="deacd-132">Kod parçacıklarını çalıştırmak yüklenecek **.\Source\Setup\CodeSnippets.vsi** dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="deacd-133">Visual Studio kod parçacıkları ve bunları nasıl kullanacağınızı öğrenmek istediğiniz konusunda bilgi sahibi değilseniz, bu belge, ek başvurabilir &quot; [ek A: Kod parçacıkları](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="deacd-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="deacd-134">Alıştırmaları</span><span class="sxs-lookup"><span data-stu-id="deacd-134">Exercises</span></span>

<span data-ttu-id="deacd-135">Bu uygulamalı laboratuvarı aşağıdaki alıştırmada içerir:</span><span class="sxs-lookup"><span data-stu-id="deacd-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="deacd-136">Alıştırma 1: Salt okunur bir Web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="deacd-137">Alıştırma 2: Okuma/yazma Web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="deacd-138">Alıştırma 3: Bir HTML istemci Web API kullanma</span><span class="sxs-lookup"><span data-stu-id="deacd-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="deacd-139">Her bir alıştırma olarak sunulduğu bir **son** elde alıştırmalar tamamladıktan sonra ortaya çıkan çözüm içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="deacd-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="deacd-140">Çalışma alıştırmaları ek yardıma ihtiyacınız varsa, bu çözüm bir kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deacd-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="deacd-141">Bu laboratuvarı tamamlamak için tahmini süre: **60 dakika**.</span><span class="sxs-lookup"><span data-stu-id="deacd-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="deacd-142">Alıştırma 1: Salt okunur bir Web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="deacd-143">Bu alıştırmada kişi yöneticisi için salt okunur GET yöntemleri uygular.</span><span class="sxs-lookup"><span data-stu-id="deacd-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="deacd-144">Görev 1 - API projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="deacd-145">Bu görevde, bir Web API'si web uygulaması oluşturmak için yeni bir ASP.NET web projesi şablonları kullanır.</span><span class="sxs-lookup"><span data-stu-id="deacd-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="deacd-146">Çalıştırma **Visual Studio 2012 Express Web**, bu Git yapmak için **Başlat** ve türü **Web için VS Express** tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="deacd-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="deacd-147">Gelen **dosya** menüsünde **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="deacd-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="deacd-148">Seçin **Visual C# | Web** proje türü proje türü ağaç görünümünden ve ardından **ASP.NET MVC 4 Web uygulaması** proje türü.</span><span class="sxs-lookup"><span data-stu-id="deacd-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="deacd-149">Projenin ayarlamak **adı** için *ContactManager* ve **çözüm adı** için *başlamak*, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="deacd-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="deacd-150">![Yeni bir ASP.NET MVC 4.0 Web uygulaması projesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image1.png "yeni bir ASP.NET MVC 4.0 Web uygulaması projesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="deacd-151">*Yeni bir ASP.NET MVC 4.0 Web uygulaması projesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="deacd-152">ASP.NET MVC 4 Proje Türü Seç iletişim kutusu içinde **Web API** proje türü.</span><span class="sxs-lookup"><span data-stu-id="deacd-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="deacd-153">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="deacd-153">Click **OK**.</span></span>

    <span data-ttu-id="deacd-154">![Web API projesi türünü belirterek](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API projesi türünü belirtme")</span><span class="sxs-lookup"><span data-stu-id="deacd-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="deacd-155">*Web API projesi türünü belirtme*</span><span class="sxs-lookup"><span data-stu-id="deacd-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="deacd-156">Görev 2 - Kişi Yöneticisi APİ'si denetleyicilerinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="deacd-157">Bu görevde, API yöntemleri ikamet denetleyicisi sınıflar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="deacd-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="deacd-158">Adlı dosyayı silin **ValuesController.cs** içinde **denetleyicileri** proje klasöründen.</span><span class="sxs-lookup"><span data-stu-id="deacd-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="deacd-159">Sağ **denetleyicileri** seçin ve proje klasöründe **Ekle | Denetleyici** bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="deacd-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="deacd-160">![Yeni bir denetleyici projeye eklenirken](build-restful-apis-with-aspnet-web-api/_static/image3.png "projeye yeni bir denetleyici ekleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="deacd-161">*Projeye yeni bir denetleyici ekleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="deacd-162">İçinde **denetleyici Ekle** görüntülenirse, seçin iletişim **boş API denetleyicisi** şablon menüsünde.</span><span class="sxs-lookup"><span data-stu-id="deacd-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="deacd-163">Denetleyici sınıfı adı **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="deacd-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="deacd-164">' A tıklayarak **Ekle.**</span><span class="sxs-lookup"><span data-stu-id="deacd-164">Then, click **Add.**</span></span>

    <span data-ttu-id="deacd-165">![Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanarak](build-restful-apis-with-aspnet-web-api/_static/image4.png "yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma")</span><span class="sxs-lookup"><span data-stu-id="deacd-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="deacd-166">*Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma*</span><span class="sxs-lookup"><span data-stu-id="deacd-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="deacd-167">Aşağıdaki kodu ekleyin **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="deacd-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="deacd-168">(Kod parçacığını - *Web API Laboratuvar - Ex01 - API yöntem elde*)</span><span class="sxs-lookup"><span data-stu-id="deacd-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="deacd-169">Tuşuna **F5** uygulamada hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="deacd-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="deacd-170">Bir Web API projesi için varsayılan giriş sayfası görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="deacd-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="deacd-171">![Bir ASP.NET Web API uygulamasının varsayılan giriş sayfasını](build-restful-apis-with-aspnet-web-api/_static/image5.png "bir ASP.NET Web API uygulamasının varsayılan giriş sayfası")</span><span class="sxs-lookup"><span data-stu-id="deacd-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="deacd-172">*Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası*</span><span class="sxs-lookup"><span data-stu-id="deacd-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="deacd-173">Internet Explorer penceresinde tuşuna **F12** açmak için anahtar **Geliştirici Araçları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="deacd-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="deacd-174">Tıklayın **ağ** sekmesine ve ardından **Yakalamayı Başlat** penceresine ağ trafiğini yakalamaktan başlamak için düğme.</span><span class="sxs-lookup"><span data-stu-id="deacd-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="deacd-175">![Başlatma ve ağ sekmesini açıp Ağ Yakalama](build-restful-apis-with-aspnet-web-api/_static/image6.png "başlatan ve ağ sekmesini açıp ağ yakalama")</span><span class="sxs-lookup"><span data-stu-id="deacd-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="deacd-176">*Ağ sekmesini açıp ve ağ yakalama başlatılıyor*</span><span class="sxs-lookup"><span data-stu-id="deacd-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="deacd-177">İle tarayıcının adres çubuğuna URL'yi ekleme **/API/contact** ve enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="deacd-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="deacd-178">İletim ayrıntıları, Ağ Yakalama penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="deacd-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="deacd-179">Yanıtın MIME türü olduğunu unutmayın **application/json**.</span><span class="sxs-lookup"><span data-stu-id="deacd-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="deacd-180">Bu, varsayılan çıkış biçimini JSON nasıl olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="deacd-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="deacd-181">![Ağ Görünümü'nde Web API isteği çıkışını görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image7.png "ağ görünümü'nde Web API isteği çıkışını görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="deacd-182">*Ağ Görünümü'nde Web API isteği çıkışını görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-183">Internet Explorer 10'ın varsayılan davranışı, bu noktada kullanıcı kaydetmek veya Web API çağrısından kaynaklanan stream açmak isteyip istemediğini sormak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="deacd-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="deacd-184">Çıkış JSON Web API URL'si çağrı sonucunu içeren bir metin dosyasının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="deacd-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="deacd-185">Yanıtın içerik geliştiriciler araç penceresi aracılığıyla izlemek için iletişim kutusunu iptal etme.</span><span class="sxs-lookup"><span data-stu-id="deacd-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="deacd-186">Tıklayın **ayrıntılı görünümüne gidin** bu API çağrısının yanıtı hakkında daha fazla ayrıntı görmek için düğme.</span><span class="sxs-lookup"><span data-stu-id="deacd-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="deacd-187">![Geçiş için Ayrıntılı Görünüm](build-restful-apis-with-aspnet-web-api/_static/image8.png "ayrıntıları görünümüne geçin")</span><span class="sxs-lookup"><span data-stu-id="deacd-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="deacd-188">*Ayrıntılı görünümüne geç*</span><span class="sxs-lookup"><span data-stu-id="deacd-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="deacd-189">Tıklayın **yanıt gövdesi** gerçek JSON yanıt metni görüntülemek için sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="deacd-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="deacd-190">![Ağ İzleyicisi'nde metin çıktısını JSON görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image9.png "çıkış metnini Ağ İzleyicisi'nde JSON görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="deacd-191">*Ağ İzleyicisi'nde JSON çıkış metin görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="deacd-192">Görev 3 - kişi modelleri oluşturma ve ilgili kişi denetleyicisi büyütmek</span><span class="sxs-lookup"><span data-stu-id="deacd-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="deacd-193">Bu görevde, API yöntemleri ikamet denetleyicisi sınıflar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="deacd-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="deacd-194">Sağ **modelleri** klasörü ve select **Ekle | Sınıfı...**  bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="deacd-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="deacd-195">![Web uygulaması için yeni model ekleme](build-restful-apis-with-aspnet-web-api/_static/image10.png "yeni model web uygulamasına ekleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="deacd-196">*Yeni model web uygulamasına ekleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="deacd-197">İçinde **Yeni Öğe Ekle** iletişim kutusunda, yeni dosya adı **Contact.cs** tıklatıp **Ekle.**</span><span class="sxs-lookup"><span data-stu-id="deacd-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="deacd-198">![Yeni bir kişi sınıf dosyası oluşturma](build-restful-apis-with-aspnet-web-api/_static/image11.png "yeni kişi sınıf dosyası oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="deacd-199">*Yeni bir kişi sınıf dosyası oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="deacd-200">Aşağıdaki vurgulanmış kodu ekleyin **kişi** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="deacd-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="deacd-201">(Kod parçacığını - *Web API Laboratuvar - Ex01 - kişi sınıfı*)</span><span class="sxs-lookup"><span data-stu-id="deacd-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="deacd-202">İçinde **ContactController** sözcüğünü seçin, sınıf **dize** yöntemi tanımındaki **alma** yöntemi ve sözcük türü *kişi*.</span><span class="sxs-lookup"><span data-stu-id="deacd-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="deacd-203">Word yazılmış sonra bir göstergesi sözcüğün başında görünür **kişi**.</span><span class="sxs-lookup"><span data-stu-id="deacd-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="deacd-204">Ya da basılı **Ctrl** anahtar ve nokta (.) tuşuna basın veya otomatik olarak doldurmak için Kod Düzenleyicisi'nde Yardım iletişim kutusunu açmak için farenizi kullanarak simgesini **kullanarak** modellerine yönelik yönerge ad alanı.</span><span class="sxs-lookup"><span data-stu-id="deacd-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![Ad alanı bildirimi için IntelliSense Yardım'ı kullanarak](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="deacd-206">*Ad alanı bildirimi için IntelliSense Yardım'ı kullanarak*</span><span class="sxs-lookup"><span data-stu-id="deacd-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="deacd-207">Kodu değiştirmek **alma** olan kişi modeli örnekleri bir dizi döndürecek şekilde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="deacd-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="deacd-208">(Kod parçacığını - *Web API kişi listesi döndüren Laboratuvar - Ex01 -*)</span><span class="sxs-lookup"><span data-stu-id="deacd-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="deacd-209">Tuşuna **F5** tarayıcı web uygulamasında hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="deacd-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="deacd-210">API yanıt çıkışına yapılan değişiklikleri görmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="deacd-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="deacd-211">Tarayıcı açılır sonra basın **F12** geliştirici araçları henüz açık değilse.</span><span class="sxs-lookup"><span data-stu-id="deacd-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="deacd-212">Tıklayın **ağ** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="deacd-213">Tuşuna **Yakalamayı Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="deacd-214">URL soneki eklemek **/API/contact** tuşuna basın ve adres çubuğuna URL'ye **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="deacd-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="deacd-215">Tuşuna **ayrıntılı görünümüne gidin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="deacd-216">Seçin **yanıt gövdesi** sekmesi. İlgili kişi örnekleri bir dizi serileştirilmiş biçiminde temsil eden bir JSON dizesi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="deacd-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="deacd-217">![JSON serileştirilmiş bir karmaşık Web API yöntem çağrısının çıkış](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON seri hale getirilmiş bir karmaşık Web API yöntem çağrısının çıkış")</span><span class="sxs-lookup"><span data-stu-id="deacd-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="deacd-218">*Karmaşık bir Web API yöntem çağrısının çıkış JSON seri hale getirilmiş*</span><span class="sxs-lookup"><span data-stu-id="deacd-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="deacd-219">Görev 4 - bir hizmet katmanına ayıklanan işlevi</span><span class="sxs-lookup"><span data-stu-id="deacd-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="deacd-220">Bu görevi nasıl ayıklanacağını denetleyicisi katmandan, böylece çalışmalarında gerçekten kitaplıklarımızı hizmetleri sağlayan hizmet işlevleri ayırmak, geliştiriciler için kolaylaştıran bir hizmet katmanı işlevsellik gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="deacd-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="deacd-221">Çözüm kök dizininde yeni bir klasör oluşturun ve adlandırın **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="deacd-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="deacd-222">Bunu yapmak için sağ **ContactManager** proje, select **Ekle** | **yeni klasör**, adlandırın *Hizmetleri*.</span><span class="sxs-lookup"><span data-stu-id="deacd-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="deacd-223">![Oluşturma Hizmetleri klasörü](build-restful-apis-with-aspnet-web-api/_static/image14.png "oluşturma hizmetleri klasörü")</span><span class="sxs-lookup"><span data-stu-id="deacd-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="deacd-224">*Hizmetleri klasörü oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="deacd-225">Sağ **Hizmetleri** klasörü ve select **Ekle | Sınıfı...**  bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="deacd-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="deacd-226">![Yeni sınıf Hizmetleri klasörü ekleme](build-restful-apis-with-aspnet-web-api/_static/image15.png "Hizmetleri klasöre yeni sınıf ekleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="deacd-227">*Yeni sınıf Hizmetleri klasörü ekleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="deacd-228">Zaman **Yeni Öğe Ekle** iletişim kutusu açılır, yeni sınıfın adı **ContactRepository** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="deacd-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="deacd-229">![Kişi havuz hizmet katmanı için kod içeren bir sınıf dosyası oluşturma](build-restful-apis-with-aspnet-web-api/_static/image16.png "kişi havuz hizmet katmanı için kod içeren bir sınıf dosyası oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="deacd-230">*Kişi havuz hizmet katmanı için kod içeren bir sınıf dosyası oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="deacd-231">Kullanarak bir ekleme yönergesini **ContactRepository.cs** modelleri ad alanı içerecek şekilde dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="deacd-232">Aşağıdaki vurgulanmış kodu ekleyin **ContactRepository.cs** GetAllContacts yöntemi uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="deacd-233">(Kod parçacığını - *Web API Laboratuvar - Ex01 - kişi depo*)</span><span class="sxs-lookup"><span data-stu-id="deacd-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="deacd-234">Açık **ContactController.cs** zaten açık değilse, dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="deacd-235">Aşağıdaki dosya ad alanı bildirimi bölümünü using deyimi.</span><span class="sxs-lookup"><span data-stu-id="deacd-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="deacd-236">Aşağıdaki vurgulanmış kodu ekleyin **ContactController.cs** sınıfı üyeleri yapabilir sınıfın rest hizmeti uygulamasını kullanmak deponun örneği temsil eden bir özel alan eklemek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="deacd-237">(Kod parçacığını - *Web API Laboratuvar - Ex01 - kişi denetleyicisi*)</span><span class="sxs-lookup"><span data-stu-id="deacd-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="deacd-238">Değişiklik **alma** BT'nin yapsak yöntemi kişi depo hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="deacd-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="deacd-239">(Kod parçacığını - *Web API depo kişilerin listesini döndüren Laboratuvar - Ex01 -*)</span><span class="sxs-lookup"><span data-stu-id="deacd-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="deacd-240">Bir kesme noktasına yerleştirip **ContactController**'s **alma** yöntem tanımı.</span><span class="sxs-lookup"><span data-stu-id="deacd-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="deacd-241">![Kesme noktası için kişi denetleyicisi ekleme](build-restful-apis-with-aspnet-web-api/_static/image17.png "kişi denetleyiciye kesme noktası ekleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="deacd-242">*Kesme noktası için kişi denetleyicisi ekleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="deacd-243">Tuşuna **F5** uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="deacd-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="deacd-244">Tarayıcı açıldığında basın **F12** Geliştirici Araçları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="deacd-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="deacd-245">Tıklayın **ağ** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="deacd-246">Tıklayın **Yakalamayı Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="deacd-247">Sonekine sahip adres çubuğundaki URL Ekle **/API/contact** basın **Enter** API denetleyicisi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="deacd-248">Visual Studio 2012 sonu kez **alma** yöntemi yürütülmesine başlar.</span><span class="sxs-lookup"><span data-stu-id="deacd-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="deacd-249">![Get yöntemi içinde bozucu](build-restful-apis-with-aspnet-web-api/_static/image18.png "bozucu içinde Get yöntemi")</span><span class="sxs-lookup"><span data-stu-id="deacd-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="deacd-250">*Get yöntemi içinde kesme*</span><span class="sxs-lookup"><span data-stu-id="deacd-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="deacd-251">Tuşuna **F5** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="deacd-252">Odak yoksa Internet Explorer için geri dönün.</span><span class="sxs-lookup"><span data-stu-id="deacd-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="deacd-253">Ağ Yakalama aralığınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-253">Note the network capture window.</span></span>

    <span data-ttu-id="deacd-254">![Internet Explorer Web API çağrısının sonucunu gösteren görünümünde ağ](build-restful-apis-with-aspnet-web-api/_static/image19.png "ağ Internet Explorer'da Web API çağrısının sonucunu gösteren görünüm")</span><span class="sxs-lookup"><span data-stu-id="deacd-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="deacd-255">*Internet Explorer'da Web API çağrısının sonucunu gösteren ağ görünümü*</span><span class="sxs-lookup"><span data-stu-id="deacd-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="deacd-256">Tıklayın **ayrıntılı görünümüne gidin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="deacd-257">Tıklayın **yanıt gövdesi** sekmesi. JSON çıkışında API çağrısı ve hizmet katmanı tarafından alınan iki kişi nasıl temsil ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="deacd-258">![Web API'si JSON çıktısını Geliştirici Araçları penceresinde görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image20.png "JSON çıkışını Web API'si Geliştirici Araçları penceresinde görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="deacd-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="deacd-259">*Web API'si JSON çıktısını Geliştirici Araçları penceresinde görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="deacd-260">Alıştırma 2: Okuma/yazma Web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="deacd-261">Bu alıştırmada, POST uygular ve veri düzenleme özellikleri ile etkinleştirmek kişi yöneticisi için PUT yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="deacd-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="deacd-262">Görev 1 - Web API projesi açma</span><span class="sxs-lookup"><span data-stu-id="deacd-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="deacd-263">Bu görevde, böylece kullanıcı girişi kabul edebilir alıştırma 1'de oluşturduğunuz Web API projesi geliştirmek hazırlık yapacaksınız.</span><span class="sxs-lookup"><span data-stu-id="deacd-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="deacd-264">Çalıştırma **Visual Studio 2012 Express Web**, bu Git yapmak için **Başlat** ve türü **Web için VS Express** tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="deacd-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="deacd-265">Açık **başlamak** çözüm bulunan **kaynak/Ex02-ReadWriteWebAPI/başlangıç/** klasör.</span><span class="sxs-lookup"><span data-stu-id="deacd-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="deacd-266">Aksi takdirde kullanarak devam edebilir **son** çözüm elde edilen önceki egzersizini tamamlayarak.</span><span class="sxs-lookup"><span data-stu-id="deacd-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="deacd-267">Sağlanan açtıysanız **başlamak** çözümü ihtiyaç duyacağınız bazı eksik NuGet paketlerini yüklemek devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="deacd-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="deacd-268">Bunu yapmak için tıklatın **proje** menü ve select **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="deacd-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="deacd-269">İçinde **NuGet paketlerini Yönet** iletişim kutusunda, tıklayın **geri** eksik paketleri indirmek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="deacd-270">Son olarak, tıklayarak çözüm oluşturun **derleme** | **Çözümü Derle**.</span><span class="sxs-lookup"><span data-stu-id="deacd-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="deacd-271">NuGet kullanmanın yararlarından biri, projenizdeki tüm kitaplıkları göndermeye proje boyutunu küçültmeyi gerekmemesidir.</span><span class="sxs-lookup"><span data-stu-id="deacd-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="deacd-272">NuGet güç araçları ile paket sürümlerini Packages.config dosyasında belirterek, gerekli tüm kitaplıkların projeyi Çalıştır ilk kez yüklemeye mümkün olmayacak.</span><span class="sxs-lookup"><span data-stu-id="deacd-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="deacd-273">Bu laboratuvarda varolan bir çözümü açtıktan sonra aşağıdaki adımları çalıştırmanız gerekecek nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="deacd-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="deacd-274">Açık **Services/ContactRepository.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="deacd-275">Görev 2 - veri kalıcılığı özellik kişi depo uygulamaya ekleme</span><span class="sxs-lookup"><span data-stu-id="deacd-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="deacd-276">Bu görevde, böylece kalıcı hale getirmek ve kullanıcı girişi ve yeni kişi örnekleri kabul alıştırma 1'de oluşturduğunuz Web API projesi ContactRepository sınıfının genişletecektir.</span><span class="sxs-lookup"><span data-stu-id="deacd-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="deacd-277">Eklemek için aşağıdaki sabiti **ContactRepository** web sunucusu önbellek öğesi anahtar adı Bu alıştırmada daha sonra adını temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="deacd-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="deacd-278">Bir oluşturucuyu ekleyin **ContactRepository** aşağıdaki kodu içeren.</span><span class="sxs-lookup"><span data-stu-id="deacd-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="deacd-279">(Kod parçacığını - *Web API Laboratuvar - Ex02 - kişi depo Oluşturucusu*)</span><span class="sxs-lookup"><span data-stu-id="deacd-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="deacd-280">Kodu değiştirmek **GetAllContacts** aşağıda gösterildiği gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="deacd-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="deacd-281">(Kod parçacığını - *Web API Laboratuvar - Ex02 - tüm kişileri Al*)</span><span class="sxs-lookup"><span data-stu-id="deacd-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="deacd-282">Bu örnek, gösterim amaçlıdır ve değerleri aynı anda birden çok istemciler için kullanılabilir yerine böylece oturumu depolama mekanizmasını veya bir istek depolama ömrü web sunucusunun önbellek depolama ortamı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="deacd-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="deacd-283">Bir Entity Framework, XML depolama veya tüm diğer birçok web sunucusu önbelleği yerine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deacd-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="deacd-284">Adlı yeni bir yöntem **SaveContact** için **ContactRepository** kişi kaydetme işini yapması için sınıf.</span><span class="sxs-lookup"><span data-stu-id="deacd-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="deacd-285">**SaveContact** yöntemi, tek bir sürecektir **kişi** belirten başarı veya başarısızlık parametre ve dönüş bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="deacd-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="deacd-286">(Kod parçacığını - *API SaveContact yöntemi uygulama Laboratuvar - Ex02 - Web*)</span><span class="sxs-lookup"><span data-stu-id="deacd-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="deacd-287">Alıştırma 3: Bir HTML istemci Web API kullanma</span><span class="sxs-lookup"><span data-stu-id="deacd-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="deacd-288">Bu alıştırmada, Web API'sini çağırmak için bir HTML istemci oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="deacd-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="deacd-289">Bu istemci, JavaScript kullanarak Web API'si ile veri değişimi kolaylaştırmak ve sonuçları HTML biçimlendirmeyi kullanarak bir web tarayıcısında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="deacd-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="deacd-290">Görev 1 - kişiler görüntülemek için bir GUI sağlamak için dizini görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="deacd-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="deacd-291">Bu görevde, bir HTML tarayıcı içinde var olan bir kişi listesini görüntülemenin desteklemek için web uygulamasının varsayılan dizini görünümünü değiştirir.</span><span class="sxs-lookup"><span data-stu-id="deacd-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="deacd-292">Açık **Visual Studio 2012 Express Web** zaten açık değilse.</span><span class="sxs-lookup"><span data-stu-id="deacd-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="deacd-293">Açık **başlamak** çözüm bulunan **kaynak/Ex03-ConsumingWebAPI/başlangıç/** klasör.</span><span class="sxs-lookup"><span data-stu-id="deacd-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="deacd-294">Aksi takdirde kullanarak devam edebilir **son** çözüm elde edilen önceki egzersizini tamamlayarak.</span><span class="sxs-lookup"><span data-stu-id="deacd-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="deacd-295">Sağlanan açtıysanız **başlamak** çözümü ihtiyaç duyacağınız bazı eksik NuGet paketlerini yüklemek devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="deacd-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="deacd-296">Bunu yapmak için tıklatın **proje** menü ve select **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="deacd-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="deacd-297">İçinde **NuGet paketlerini Yönet** iletişim kutusunda, tıklayın **geri** eksik paketleri indirmek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="deacd-298">Son olarak, tıklayarak çözüm oluşturun **derleme** | **Çözümü Derle**.</span><span class="sxs-lookup"><span data-stu-id="deacd-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="deacd-299">NuGet kullanmanın yararlarından biri, projenizdeki tüm kitaplıkları göndermeye proje boyutunu küçültmeyi gerekmemesidir.</span><span class="sxs-lookup"><span data-stu-id="deacd-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="deacd-300">NuGet güç araçları ile paket sürümlerini Packages.config dosyasında belirterek, gerekli tüm kitaplıkların projeyi Çalıştır ilk kez yüklemeye mümkün olmayacak.</span><span class="sxs-lookup"><span data-stu-id="deacd-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="deacd-301">Bu laboratuvarda varolan bir çözümü açtıktan sonra aşağıdaki adımları çalıştırmanız gerekecek nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="deacd-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="deacd-302">Açık **Index.cshtml** konumundaki dosya **görünümler/giriş** klasör.</span><span class="sxs-lookup"><span data-stu-id="deacd-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="deacd-303">Div öğesinin içine HTML kodu kimliğiyle değiştirin **gövdesi** böylece şu kod gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="deacd-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="deacd-304">Web API'sine HTTP isteği gerçekleştirmek için dosyanın sonuna aşağıdaki Javascript kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="deacd-305">Açık **ContactController.cs** zaten açık değilse, dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="deacd-306">Bir kesme noktası yerleştirmek **alma** yöntemi **ContactController** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="deacd-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="deacd-307">![API denetleyicisi üzerinde Get yöntemi bir kesme noktası yerleştirerek](build-restful-apis-with-aspnet-web-api/_static/image21.png "bir kesme noktası yerleştirerek API denetleyicisi üzerinde Get yöntemi")</span><span class="sxs-lookup"><span data-stu-id="deacd-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="deacd-308">*Bir kesme noktası yerleştirerek API denetleyicisi üzerinde Get yöntemi*</span><span class="sxs-lookup"><span data-stu-id="deacd-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="deacd-309">Tuşuna **F5** projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="deacd-309">Press **F5** to run the project.</span></span> <span data-ttu-id="deacd-310">Tarayıcı HTML belgesi yükler.</span><span class="sxs-lookup"><span data-stu-id="deacd-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-311">Uygulama kök URL'sini tarama emin olun.</span><span class="sxs-lookup"><span data-stu-id="deacd-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="deacd-312">Sayfa yükler ve yürütür JavaScript sonra kesme noktasına isabet ve kod yürütme denetleyicide duraklatılır.</span><span class="sxs-lookup"><span data-stu-id="deacd-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="deacd-313">![Web için VS Express kullanarak Web API çağrısı ile hata ayıklama](build-restful-apis-with-aspnet-web-api/_static/image22.png "Web için VS Express kullanarak Web API çağrısı ile hata ayıklama")</span><span class="sxs-lookup"><span data-stu-id="deacd-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="deacd-314">*Web için Visual Studio Express 2012 kullanarak Web API çağrısı ile hata ayıklama*</span><span class="sxs-lookup"><span data-stu-id="deacd-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="deacd-315">Kesme noktası kaldırıp tuşuna **F5** veya hata ayıklama araç çubuğunun **devam** tarayıcıda görüntüle yüklemeye devam etmek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="deacd-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="deacd-316">Web API çağrısı tamamlandığında tarayıcıda listesi öğeleri olarak görüntülenen arama Web API'den döndürülen kişiler görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="deacd-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="deacd-317">![Liste öğeleri tarayıcıda görüntülenen API çağrısının sonucunu](build-restful-apis-with-aspnet-web-api/_static/image23.png "listesi öğeleri olarak tarayıcıda görüntülenen API çağrısının sonuçları")</span><span class="sxs-lookup"><span data-stu-id="deacd-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="deacd-318">*Liste öğeleri tarayıcıda görüntülenen API çağrısının sonuçları*</span><span class="sxs-lookup"><span data-stu-id="deacd-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="deacd-319">Hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="deacd-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="deacd-320">Görev 2 - kişiler oluşturmak için bir GUI sağlamak için dizini görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="deacd-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="deacd-321">Bu görevde, MVC uygulama dizini görünümünü değiştirmek devam eder.</span><span class="sxs-lookup"><span data-stu-id="deacd-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="deacd-322">Bir forma kullanıcı girişi yakalamak ve bunları yeni kişi oluşturmak için Web API'sine gönderir HTML sayfasına eklenen ve GUI tarihi toplamak için yeni bir Web API denetleyicisi yöntem oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="deacd-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="deacd-323">Açık **ContactController.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="deacd-324">Denetleyici sınıfına adlı yeni bir yöntem ekleyin **Post** aşağıdaki kodda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="deacd-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="deacd-325">(Kod parçacığını - *Web API Laboratuvar - Ex03 - Post yöntemini*)</span><span class="sxs-lookup"><span data-stu-id="deacd-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="deacd-326">Açık **Index.cshtml** zaten açık değilse Visual Studio'da dosya.</span><span class="sxs-lookup"><span data-stu-id="deacd-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="deacd-327">Aşağıdaki HTML kodu yalnızca önceki görevde eklediğiniz sırasız liste dosyaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="deacd-328">Belge alt kısmındaki betik öğesi içinde bir HTTP POST çağrısı kullanarak Web API'si için verileri post gerçekleştireceği düğme tıklama olayları işlemek için aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="deacd-329">İçinde **ContactController.cs**, bir kesme noktası yerleştirmek **Post** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="deacd-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="deacd-330">Tuşuna **F5** uygulamayı tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="deacd-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="deacd-331">Sayfanın tarayıcıda yüklendikten sonra yeni bir kişi adı ve kimliği ve tıklatın yazın **Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="deacd-332">![İstemci HTML belge yüklenirken tarayıcıda](build-restful-apis-with-aspnet-web-api/_static/image24.png "istemci HTML belgesi tarayıcıda yüklendi")</span><span class="sxs-lookup"><span data-stu-id="deacd-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="deacd-333">*Tarayıcıda yüklenen istemci HTML belgesi*</span><span class="sxs-lookup"><span data-stu-id="deacd-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="deacd-334">Hata ayıklayıcısı penceresinin zaman sonları **Post** yöntemi, özelliklerini atın **başvurun** parametresi.</span><span class="sxs-lookup"><span data-stu-id="deacd-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="deacd-335">Değerleri ve forma girdiniz verilerin eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="deacd-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="deacd-336">![Web API için istemci tarafından gönderilen kişi nesnesi](build-restful-apis-with-aspnet-web-api/_static/image25.png "istemcisinden Web API'ye gönderilen kişi nesnesi")</span><span class="sxs-lookup"><span data-stu-id="deacd-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="deacd-337">*Web API için istemci tarafından gönderilen kişi nesnesi*</span><span class="sxs-lookup"><span data-stu-id="deacd-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="deacd-338">Hata ayıklayıcı kadar yöntemi adımlayın **yanıt** değişken oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="deacd-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="deacd-339">İncelemesinin bağlı **Yereller** hata ayıklayıcı penceresinde tüm özellikler ayarlandıktan göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="deacd-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="deacd-340">![Hata ayıklayıcı oluşturulduktan yanıt](build-restful-apis-with-aspnet-web-api/_static/image26.png "hata ayıklayıcısı oluşturulduktan yanıt")</span><span class="sxs-lookup"><span data-stu-id="deacd-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="deacd-341">*Hata ayıklayıcı oluşturulduktan yanıt*</span><span class="sxs-lookup"><span data-stu-id="deacd-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="deacd-342">Basarsanız **F5** veya **devam** hata ayıklayıcıda istek tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="deacd-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="deacd-343">Tarayıcıya geçtikten sonra yeni kişi tarafından depolanan kişiler listesine eklendi **ContactRepository** uygulaması.</span><span class="sxs-lookup"><span data-stu-id="deacd-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="deacd-344">![Tarayıcı oluşturma başarılı yeni kişi örneğinin yansıtır](build-restful-apis-with-aspnet-web-api/_static/image27.png "tarayıcı yansıtan yeni kişi örneği başarıyla oluşturuldu")</span><span class="sxs-lookup"><span data-stu-id="deacd-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="deacd-345">*Tarayıcı yansıtan yeni kişi örneği başarıyla oluşturuldu*</span><span class="sxs-lookup"><span data-stu-id="deacd-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="deacd-346">Ayrıca, bu uygulama aşağıdaki Azure dağıtabilirsiniz [ek C: Bir ASP.NET MVC 4 Web dağıtımı kullanarak uygulama yayımlama](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="deacd-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="deacd-347">Özet</span><span class="sxs-lookup"><span data-stu-id="deacd-347">Summary</span></span>

<span data-ttu-id="deacd-348">Bu Laboratuvar, yeni ASP.NET Web API çerçevesi ve uygulaması çerçevesini kullanarak RESTful Web API'lerini kullanıma sundu.</span><span class="sxs-lookup"><span data-stu-id="deacd-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="deacd-349">Buradan, herhangi bir sayıda mekanizmalarını kullanarak veri kalıcılığı kolaylaştıran yeni bir havuz oluşturabilir ve yerine bu Laboratuvar içinde bir örnek olarak basit bir yedekleme, hizmet bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deacd-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="deacd-350">Web API'si, HTTP ve JSON veya XML destekleyen herhangi bir dilde yazılmış HTML olmayan istemcilerden gelen iletişimi etkinleştirme gibi ek özellikleri destekler.</span><span class="sxs-lookup"><span data-stu-id="deacd-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="deacd-351">Tipik bir web uygulaması dışında bir Web API'sini barındıran olanağı da mümkündür, aynı zamanda kendi serileştirme biçimleri oluşturma yeteneği.</span><span class="sxs-lookup"><span data-stu-id="deacd-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="deacd-352">ASP.NET Web sitesinde ASP.NET Web API çerçevesi ayrılmış bir alan yok [ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="deacd-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="deacd-353">Bu site, en son haberler, örnekler ve Web API'si için ilgili Haberler şekilde kontrol edin, sık sağlamaya devam edecek içine neredeyse tüm cihaz veya geliştirme framework kullanılabilir özel Web API'leri oluşturmanın son teknoloji ürünü derin delve istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="deacd-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="deacd-354">Ek A: Kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="deacd-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="deacd-355">Kod parçacıkları ile parmaklarınızın ucunda ihtiyacınız olan tüm kod vardır.</span><span class="sxs-lookup"><span data-stu-id="deacd-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="deacd-356">Laboratuvar belgenin tam olarak ne zaman, kullanabilmek için aşağıdaki şekilde gösterildiği gibi size bildirir.</span><span class="sxs-lookup"><span data-stu-id="deacd-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="deacd-357">![Kod projenize eklemek için Visual Studio kod parçacıkları](build-restful-apis-with-aspnet-web-api/_static/image28.png "kod projenize eklemek için Visual Studio kullanarak kod parçacıkları")</span><span class="sxs-lookup"><span data-stu-id="deacd-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="deacd-358">*Kod projenize eklemek için Visual Studio kod parçacıkları*</span><span class="sxs-lookup"><span data-stu-id="deacd-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="deacd-359">Klavye (yalnızca C#) kullanarak bir kod parçacığı eklemek için</span><span class="sxs-lookup"><span data-stu-id="deacd-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="deacd-360">Kod eklemesini istediğiniz imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="deacd-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="deacd-361">(Olmadan, boşluk veya tire) kod parçacığı adı yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="deacd-362">Kod parçacıkları adlarla eşleşen IntelliSense görüntüler izleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="deacd-363">Doğru kod parçacığını seçin (veya tüm parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="deacd-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="deacd-364">İki kez İmleç konumuna kod parçacığını eklemek için SEKME tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="deacd-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="deacd-365">![Kod parçacığı adını yazmaya başlayın](build-restful-apis-with-aspnet-web-api/_static/image29.png "kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="deacd-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="deacd-366">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="deacd-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="deacd-367">![Vurgulanan kod parçacığı seçmek için SEKME tuşuna basın](build-restful-apis-with-aspnet-web-api/_static/image30.png "vurgulanan kod parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="deacd-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="deacd-368">*Vurgulanan kod parçacığı seçmek için SEKME tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="deacd-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="deacd-369">![Yeniden Tab tuşuna basın ve kod parçacığı genişletir](build-restful-apis-with-aspnet-web-api/_static/image31.png "yeniden Tab tuşuna basın ve kod parçacığı genişletir")</span><span class="sxs-lookup"><span data-stu-id="deacd-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="deacd-370">*Yeniden Tab tuşuna basın ve kod parçacığı genişletir*</span><span class="sxs-lookup"><span data-stu-id="deacd-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="deacd-371">Fare (C#, Visual Basic ve XML) kullanarak bir kod parçacığı eklemek için</span><span class="sxs-lookup"><span data-stu-id="deacd-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="deacd-372">Kod parçacığını eklemek istediğiniz yeri sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="deacd-373">Seçin **parçacık Ekle** ardından **kod Parçacıklarım**.</span><span class="sxs-lookup"><span data-stu-id="deacd-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="deacd-374">Tıklayarak ilgili kod parçacığı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="deacd-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="deacd-375">![İstediğiniz kod parçacığını eklemek ve parçacık eklemek için sağ tıklama](build-restful-apis-with-aspnet-web-api/_static/image32.png "sağ tıklayın, istediğiniz kod parçacığını eklemek ve kod parçacığı Ekle")</span><span class="sxs-lookup"><span data-stu-id="deacd-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="deacd-376">*Kod parçacığını eklemek ve parçacık eklemek istediğiniz sağ tıklayın*</span><span class="sxs-lookup"><span data-stu-id="deacd-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="deacd-377">![Tıklayarak ilgili kod parçacığını listesinden çekme](build-restful-apis-with-aspnet-web-api/_static/image33.png "tıklayarak ilgili kod parçacığı listeden seçin")</span><span class="sxs-lookup"><span data-stu-id="deacd-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="deacd-378">*Tıklayarak ilgili kod parçacığı listeden seçin*</span><span class="sxs-lookup"><span data-stu-id="deacd-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="deacd-379">Ek B: Web için Express 2012 Visual Studio'yu yükleme</span><span class="sxs-lookup"><span data-stu-id="deacd-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="deacd-380">Yükleyebileceğiniz **Web için Visual Studio Express 2012 Microsoft** veya başka bir &quot;Express&quot; sürümüyle **[Microsoft Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="deacd-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="deacd-381">Aşağıdaki yönergeler, yüklemek için gereken adımlarda size kılavuzluk *Web için Visual studio Express 2012* kullanarak *Microsoft Web Platformu yükleyicisi*.</span><span class="sxs-lookup"><span data-stu-id="deacd-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="deacd-382">Git [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="deacd-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="deacd-383">Web Platformu Yükleyicisi'ı zaten yüklediyseniz, bunun yerine ve ürün için arama açabileceğiniz &quot; <em>Visual Studio Express 2012 için Azure SDK ile Web</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="deacd-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="deacd-384">Tıklayarak **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="deacd-384">Click on **Install Now**.</span></span> <span data-ttu-id="deacd-385">Yoksa **Web Platformu yükleyicisi** indirmek ve ilk yüklemek için yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deacd-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="deacd-386">Bir kez **Web Platformu yükleyicisi** açık tıklayın **yükleme** Kurulum'u başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="deacd-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="deacd-387">![Visual Studio Express yükleyin](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express'i yükle")</span><span class="sxs-lookup"><span data-stu-id="deacd-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="deacd-388">*Visual Studio Express yükleyin*</span><span class="sxs-lookup"><span data-stu-id="deacd-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="deacd-389">Tüm ürünlerin lisans ve koşulları okuyun ve tıklayın **kabul ediyorum** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="deacd-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="deacd-391">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="deacd-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="deacd-392">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-392">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="deacd-394">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="deacd-394">*Installation progress*</span></span>
6. <span data-ttu-id="deacd-395">Yükleme tamamlandığında, tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="deacd-395">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="deacd-397">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="deacd-397">*Installation completed*</span></span>
7. <span data-ttu-id="deacd-398">Tıklayın **çıkış** Web Platformu Yükleyicisi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="deacd-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="deacd-399">Web için Visual Studio Express'te açmak için Git **Başlat** ekranında ve yazmaya başlayabilirsiniz &quot; **VS Express**&quot;, ardından **Web için VS Express** bir kutucuk.</span><span class="sxs-lookup"><span data-stu-id="deacd-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web kutucuğu için VS Express](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="deacd-401">*Web kutucuğu için VS Express*</span><span class="sxs-lookup"><span data-stu-id="deacd-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="deacd-402">Ek C: Bir ASP.NET MVC 4 Web dağıtımı kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="deacd-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="deacd-403">Bu ekte, Azure portalında yeni bir web sitesi oluşturma ve Laboratuvar izleyerek Azure tarafından sağlanan Web dağıtımı Yayımlama özelliğini avantajlarını elde ettiğiniz uygulama yayımlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="deacd-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="deacd-404">Görev 1 - Azure portalında yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="deacd-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="deacd-405">Git [Azure Yönetim Portalı](https://manage.windowsazure.com/) aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="deacd-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-406">Azure'la 10 ASP.NET Web sitesini ücretsiz olarak barındırın ve ardından trafiğiniz büyüdükçe ölçeğinizi artırın.</span><span class="sxs-lookup"><span data-stu-id="deacd-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="deacd-407">Kaydolabilirsiniz [burada](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="deacd-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="deacd-408">![Windows Azure Portal'da oturum açın](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure Portal'da oturum açın")</span><span class="sxs-lookup"><span data-stu-id="deacd-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="deacd-409">*Portal'da oturum açın*</span><span class="sxs-lookup"><span data-stu-id="deacd-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="deacd-410">Tıklayın **yeni** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="deacd-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="deacd-411">![Yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image40.png "yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="deacd-412">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="deacd-413">Tıklayın **işlem** | **Web sitesi**.</span><span class="sxs-lookup"><span data-stu-id="deacd-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="deacd-414">Ardından **hızlı Oluştur** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="deacd-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="deacd-415">Yeni web sitesi için kullanılabilen bir URL girin ve tıklatın **Web sitesi oluştur**.</span><span class="sxs-lookup"><span data-stu-id="deacd-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-416">Azure, denetleyebileceğiniz ve yönetebileceğiniz bulutta çalışan bir web uygulaması için bir ana bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="deacd-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="deacd-417">Hızlı oluşturma seçeneği azure'a portalın dışında bir tamamlanmış web uygulaması dağıtmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="deacd-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="deacd-418">Bir veritabanını ayarlamak için adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="deacd-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="deacd-419">![Hızlı oluşturma yöntemini kullanarak yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image41.png "hızlı oluşturma yöntemini kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="deacd-420">*Hızlı oluşturma yöntemini kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="deacd-421">Yeni kadar bekleyin **Web sitesi** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="deacd-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="deacd-422">Web sitesi oluşturulduktan sonra altındaki bağlantıya tıklayın **URL** sütun.</span><span class="sxs-lookup"><span data-stu-id="deacd-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="deacd-423">Yeni Web sitesi çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="deacd-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="deacd-424">![Yeni web sitesi için gözatma](build-restful-apis-with-aspnet-web-api/_static/image42.png "yeni web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="deacd-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="deacd-425">*Yeni web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="deacd-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="deacd-426">![Web sitesi çalışan](build-restful-apis-with-aspnet-web-api/_static/image43.png "çalışan Web sitesi")</span><span class="sxs-lookup"><span data-stu-id="deacd-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="deacd-427">*Çalışan Web sitesi*</span><span class="sxs-lookup"><span data-stu-id="deacd-427">*Web site running*</span></span>
6. <span data-ttu-id="deacd-428">Portala geri dönün ve web sitesi altında adına **adı** yönetim sayfaları görüntülemek için sütun.</span><span class="sxs-lookup"><span data-stu-id="deacd-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="deacd-429">![Web sitesi Yönetim sayfalarının açma](build-restful-apis-with-aspnet-web-api/_static/image44.png "web sitesi Yönetim sayfalarının açma")</span><span class="sxs-lookup"><span data-stu-id="deacd-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="deacd-430">*Web Sitesi Yönetim sayfalarının açma*</span><span class="sxs-lookup"><span data-stu-id="deacd-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="deacd-431">İçinde **Pano** sayfasındaki **Hızlı Bakış** bölümünde **yayımlama profili indir** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="deacd-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-432">*Yayımlama profilini* bir her etkin yayımlama yöntemi için bir Azure web uygulamasına yayımlamak için gereken bilgilerin tümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="deacd-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="deacd-433">Yayımlama profili URL'leri, kullanıcı kimlik bilgileri ve her bir yayımlama yönteminin etkinleştirildiği uç noktalarına karşı kimlik doğrulaması yapmak ve bağlanmak için gereken veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="deacd-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="deacd-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express Web** ve **Microsoft Visual Studio 2012** okuma desteği yayımlama profillerini yapılandırma için bu programların otomatik hale getirmek için Azure Web uygulamaları yayımlama.</span><span class="sxs-lookup"><span data-stu-id="deacd-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="deacd-435">![Yayımlama profili web sitesi indiriliyor](build-restful-apis-with-aspnet-web-api/_static/image45.png "yayımlama profili web sitesi indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="deacd-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="deacd-436">*Yayımlama profili Web sitesi indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="deacd-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="deacd-437">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="deacd-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="deacd-438">Daha fazla Bu alıştırmada, bir Azure web uygulamasına Visual Studio'dan yayımlamak için bu dosyayı kullanmak nasıl görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="deacd-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="deacd-439">![Yayımlama profili dosyasını kaydetme](build-restful-apis-with-aspnet-web-api/_static/image46.png "yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="deacd-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="deacd-440">*Yayımlama profili dosyasını kaydetme*</span><span class="sxs-lookup"><span data-stu-id="deacd-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="deacd-441">Görev 2 - veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deacd-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="deacd-442">Uygulamanızı kullanan SQL Server'ın yaparsa veritabanlarını bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="deacd-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="deacd-443">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atla.</span><span class="sxs-lookup"><span data-stu-id="deacd-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="deacd-444">SQL veritabanı sunucusu, uygulama veritabanını depolamak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="deacd-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="deacd-445">Aboneliğinizde Azure Yönetim Portalı'nda SQL veritabanı sunucuları görüntüleyebilirsiniz **Sql veritabanları** | **sunucuları** | **sunucuPanosu**.</span><span class="sxs-lookup"><span data-stu-id="deacd-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="deacd-446">Oluşturulan server yoksa kullanarak bir tane oluşturabilirsiniz **Ekle** komut çubuğunda düğme.</span><span class="sxs-lookup"><span data-stu-id="deacd-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="deacd-447">Not **sunucu adı ve URL, yönetici oturum açma adı ve parola**, sonraki görevleri kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="deacd-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="deacd-448">Daha sonraki bir aşamasında oluşturulacak şekilde veritabanı henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="deacd-449">![SQL veritabanı sunucu Panosu](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL veritabanı sunucu Panosu")</span><span class="sxs-lookup"><span data-stu-id="deacd-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="deacd-450">*SQL veritabanı sunucu Panosu*</span><span class="sxs-lookup"><span data-stu-id="deacd-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="deacd-451">İşlemin sonraki görev ihtiyacınız sunucunun listesinde yerel IP adresinizi eklemek, bu nedenle Visual Studio'dan veritabanı bağlantısını test eder **izin verilen IP adresleri**.</span><span class="sxs-lookup"><span data-stu-id="deacd-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="deacd-452">Bunu yapmanın tıklatın **yapılandırma**, IP adresi seçin **geçerli istemci IP adresi** ve yapıştırın **başlangıç IP adresi** ve **bitiş IP adresi** metin kutuları ve tıklatın ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="deacd-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![İstemci IP adresi ekleme](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="deacd-454">*İstemci IP adresi ekleme*</span><span class="sxs-lookup"><span data-stu-id="deacd-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="deacd-455">Bir kez **istemci IP adresi** için izin verilen IP adreslerini eklenir listesinde, tıklayın **Kaydet** değişiklikleri onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="deacd-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri onaylayın](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="deacd-457">*Değişiklikleri onaylayın*</span><span class="sxs-lookup"><span data-stu-id="deacd-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="deacd-458">Görev 3 - bir ASP.NET MVC 4 Web dağıtımı kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="deacd-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="deacd-459">ASP.NET MVC 4 çözüme geri dönün.</span><span class="sxs-lookup"><span data-stu-id="deacd-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="deacd-460">İçinde **Çözüm Gezgini**, web sitesi projesini sağ tıklatın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="deacd-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="deacd-461">![Uygulama yayımlama](build-restful-apis-with-aspnet-web-api/_static/image51.png "uygulama yayımlama")</span><span class="sxs-lookup"><span data-stu-id="deacd-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="deacd-462">*Web sitesi yayımlama*</span><span class="sxs-lookup"><span data-stu-id="deacd-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="deacd-463">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="deacd-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="deacd-464">![Yayımlama profilini içeri aktarma](build-restful-apis-with-aspnet-web-api/_static/image52.png "yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="deacd-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="deacd-465">*Yayımlama profilini içeri aktarma*</span><span class="sxs-lookup"><span data-stu-id="deacd-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="deacd-466">Tıklayın **bağlantısını doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="deacd-466">Click **Validate Connection**.</span></span> <span data-ttu-id="deacd-467">Doğrulama tamamlandıktan sonra tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="deacd-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="deacd-468">Bağlantıyı doğrula düğmesi yanında görünür yeşil bir onay işareti gördükten sonra doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="deacd-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="deacd-469">![Bağlantı doğrulama](build-restful-apis-with-aspnet-web-api/_static/image53.png "bağlantısı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="deacd-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="deacd-470">*Bağlantı doğrulama*</span><span class="sxs-lookup"><span data-stu-id="deacd-470">*Validating connection*</span></span>
4. <span data-ttu-id="deacd-471">İçinde **ayarları** sayfasındaki **veritabanları** bölümünde, veritabanı bağlantının metin kutusunun yanındaki düğmeye tıklayın (yani **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="deacd-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="deacd-472">![Web dağıtımı yapılandırma](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web dağıtımı yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="deacd-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="deacd-473">*Web dağıtımı yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="deacd-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="deacd-474">Veritabanı bağlantısı aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="deacd-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="deacd-475">İçinde **sunucu adı** , SQL veritabanı sunucu URL'sini kullanarak yazın *tcp:* önek.</span><span class="sxs-lookup"><span data-stu-id="deacd-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="deacd-476">İçinde **kullanıcı adı** , Sunucu Yöneticisi oturum açma adı yazın.</span><span class="sxs-lookup"><span data-stu-id="deacd-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="deacd-477">İçinde **parola** Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="deacd-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="deacd-478">Örneğin, yeni bir veritabanı adı yazın: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="deacd-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="deacd-479">![Hedef bağlantı dizesi yapılandırma](build-restful-apis-with-aspnet-web-api/_static/image55.png "hedef bağlantı dizesini yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="deacd-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="deacd-480">*Hedef bağlantı dizesini yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="deacd-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="deacd-481">Sonra **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-481">Then click **OK**.</span></span> <span data-ttu-id="deacd-482">Veritabanı oluşturmak isteyip istemediğiniz sorulduğunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="deacd-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="deacd-483">![Veritabanı oluşturma](build-restful-apis-with-aspnet-web-api/_static/image56.png "veritabanı dizesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="deacd-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="deacd-484">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="deacd-484">*Creating the database*</span></span>
7. <span data-ttu-id="deacd-485">Windows Azure SQL veritabanına bağlanmak için kullanacağı bağlantı dizesini, varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="deacd-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="deacd-486">Sonra **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deacd-486">Then click **Next**.</span></span>

    <span data-ttu-id="deacd-487">![SQL veritabanı'na işaret eden bağlantı dizesi](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL veritabanına işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="deacd-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="deacd-488">*SQL veritabanı'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="deacd-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="deacd-489">İçinde **Önizleme** sayfasında **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="deacd-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="deacd-490">![Web uygulaması yayımlama](build-restful-apis-with-aspnet-web-api/_static/image58.png "web uygulaması yayımlama")</span><span class="sxs-lookup"><span data-stu-id="deacd-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="deacd-491">*Web uygulaması yayımlama*</span><span class="sxs-lookup"><span data-stu-id="deacd-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="deacd-492">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayımlanan web sitesi açılır.</span><span class="sxs-lookup"><span data-stu-id="deacd-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="deacd-493">![Uygulama Windows Azure'da yayımlanan](build-restful-apis-with-aspnet-web-api/_static/image59.png "uygulama yayımlanan Windows Azure'a")</span><span class="sxs-lookup"><span data-stu-id="deacd-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="deacd-494">*Azure'da yayımlanan uygulama*</span><span class="sxs-lookup"><span data-stu-id="deacd-494">*Application published to Azure*</span></span>
