---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio için ASP.NET ve Web Araçları 2013 Yayın Notları | Microsoft Dokümanlar
author: rick-anderson
description: Bu belge, Visual Studio 2013 için ASP.NET ve Web Araçları'nın yayımlanmasından açıklanmaktadır.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543502"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="7640c-103">Visual Studio 2013 için ASP.NET and Web Tools Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="7640c-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="7640c-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="7640c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7640c-105">Bu belge, Visual Studio 2013 için ASP.NET ve Web Araçları'nın yayımlanmasından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7640c-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="7640c-106">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="7640c-106">Contents</span></span>

- [<span data-ttu-id="7640c-107">Kurulum Notları</span><span class="sxs-lookup"><span data-stu-id="7640c-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="7640c-108">Belgeler</span><span class="sxs-lookup"><span data-stu-id="7640c-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="7640c-109">Yazılım Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="7640c-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="7640c-110">Visual Studio için ASP.NET ve Web Araçlarında Yeni Özellikler 2013</span><span class="sxs-lookup"><span data-stu-id="7640c-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="7640c-111">Bir ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7640c-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="7640c-112">Yeni Web Proje Deneyimi</span><span class="sxs-lookup"><span data-stu-id="7640c-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="7640c-113">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="7640c-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="7640c-114">Tarayıcı Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="7640c-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="7640c-115">Visual Studio Web Editörü Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7640c-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="7640c-116">Visual Studio'da Azure App Service Web Apps Desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="7640c-117">Web Yayımlama Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7640c-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="7640c-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="7640c-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="7640c-119">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="7640c-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="7640c-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="7640c-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="7640c-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="7640c-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="7640c-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="7640c-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="7640c-123">ASP.NET Kimlik</span><span class="sxs-lookup"><span data-stu-id="7640c-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="7640c-124">Microsoft OWIN Bileşenleri</span><span class="sxs-lookup"><span data-stu-id="7640c-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="7640c-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="7640c-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="7640c-126">ASP.NET Jilet 3</span><span class="sxs-lookup"><span data-stu-id="7640c-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="7640c-127">ASP.NET Uygulama Askıya Alma</span><span class="sxs-lookup"><span data-stu-id="7640c-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="7640c-128">Bilinen Sorunlar ve Son Dakika Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="7640c-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="7640c-129">Kurulum Notları</span><span class="sxs-lookup"><span data-stu-id="7640c-129">Installation Notes</span></span>

<span data-ttu-id="7640c-130">Visual Studio 2013 için ASP.NET ve Web Araçları ana yükleyici de paketlenmiş ve [buradan](https://www.asp.net/downloads)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="7640c-131">Belgeler</span><span class="sxs-lookup"><span data-stu-id="7640c-131">Documentation</span></span>

<span data-ttu-id="7640c-132">Eğitimler ve Visual Studio 2013 için ASP.NET ve Web Araçları hakkında diğer bilgiler [ASP.NET web sitesinden](https://www.asp.net/)edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="7640c-133">Yazılım Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="7640c-133">Software Requirements</span></span>

<span data-ttu-id="7640c-134">ASP.NET ve Web Araçları Visual Studio 2013 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="7640c-135">Visual Studio için ASP.NET ve Web Araçlarında Yeni Özellikler 2013</span><span class="sxs-lookup"><span data-stu-id="7640c-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="7640c-136">Aşağıdaki bölümlerde sürümde tanıtılan özellikler açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7640c-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="7640c-137">Bir ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7640c-137">One ASP.NET</span></span>

<span data-ttu-id="7640c-138">Visual Studio 2013'ün piyasaya sürülmesiyle, ASP.NET teknolojilerini kullanma deneyimini birleştirme yolunda bir adım attık, böylece istediğiniz teknolojileri kolayca karıştırıp eşleştirebilesiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="7640c-139">Örneğin, MVC kullanarak bir proje başlatabilir ve daha sonra projeye Web Formları sayfalarını kolayca ekleyebilir veya Web Formları projesinde Web API'lerini iskeleye alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="7640c-140">Bir ASP.NET, bir geliştirici olarak sevdiğiniz şeyleri ASP.NET daha kolay hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="7640c-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="7640c-141">Hangi teknolojiyi seçerseniz seçin, One ASP.NET'nin güvenilir temel çerçevesi üzerinde inşa ettiğinize güvenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="7640c-142">Yeni Web Proje Deneyimi</span><span class="sxs-lookup"><span data-stu-id="7640c-142">New Web Project Experience</span></span>

<span data-ttu-id="7640c-143">Visual Studio 2013'te yeni web projeleri oluşturma deneyimini artırdık.</span><span class="sxs-lookup"><span data-stu-id="7640c-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="7640c-144">Yeni **ASP.NET Web Projesi** iletişim kutusunda istediğiniz proje türünü seçebilir, herhangi bir teknoloji birleşimini (Web Forms, MVC, Web API) yapılandırabilir, kimlik doğrulama seçeneklerini yapılandırabilir ve birim test projesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![Yeni ASP.NET Projesi](release-notes/_static/image1.png)

<span data-ttu-id="7640c-146">Yeni iletişim kutusu, şablonların çoğu için varsayılan kimlik doğrulama seçeneklerini değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="7640c-147">Örneğin, bir ASP.NET Web Formları projesi oluşturduğunuzda aşağıdaki seçeneklerden birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7640c-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="7640c-148">Kimlik Doğrulaması Yok</span><span class="sxs-lookup"><span data-stu-id="7640c-148">No Authentication</span></span>
- <span data-ttu-id="7640c-149">Bireysel Kullanıcı Hesapları (ASP.NET üyelik veya sosyal sağlayıcı girişi)</span><span class="sxs-lookup"><span data-stu-id="7640c-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="7640c-150">Kurumsal Hesaplar (Bir internet uygulamasında Aktif Dizin)</span><span class="sxs-lookup"><span data-stu-id="7640c-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="7640c-151">Windows Kimlik Doğrulama (Intranet uygulamasında Etkin Dizin)</span><span class="sxs-lookup"><span data-stu-id="7640c-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![Kimlik doğrulaması seçenekleri](release-notes/_static/image2.png)

<span data-ttu-id="7640c-153">Web projeleri oluşturmak için yeni süreç hakkında daha fazla bilgi için Visual [Studio 2013'te ASP.NET Web Projeleri Oluşturma'ya](creating-web-projects-in-visual-studio.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="7640c-154">Yeni kimlik doğrulama seçenekleri hakkında daha fazla bilgi için, bu belgede daha sonra [ASP.NET Kimliği'ne](#TOC8) bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="7640c-155">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="7640c-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="7640c-156">ASP.NET İskele, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="7640c-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="7640c-157">Projenize bir veri modeliyle etkileşimde bulunarak ortak kod eklemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7640c-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="7640c-158">Visual Studio'nun önceki sürümlerinde, iskele ASP.NET MVC projeleri ile sınırlıydı.</span><span class="sxs-lookup"><span data-stu-id="7640c-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="7640c-159">Visual Studio 2013 ile artık Web Formlar da dahil olmak üzere herhangi bir ASP.NET projesi için iskele kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="7640c-160">Visual Studio 2013 şu anda bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Formları ile iskeleyi kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="7640c-161">Web Formları için sayfa oluşturma desteği gelecekteki bir güncelleştirmede eklenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="7640c-162">İskele kullanırken, gerekli tüm bağımlılıkların projeye yüklenmesini sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7640c-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="7640c-163">Örneğin, bir web formları projesi ASP.NETyle başlayıp web API Denetleyicisi eklemek için iskele kullanırsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="7640c-164">Bir Web Forms projesine MVC iskelesi eklemek için **Yeni İskele Öğesi** ekleyin ve iletişim penceresinde **MVC 5 Bağımlılıkları'nı** seçin.</span><span class="sxs-lookup"><span data-stu-id="7640c-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="7640c-165">İskele MVC için iki seçenek vardır; Minimal ve Tam.</span><span class="sxs-lookup"><span data-stu-id="7640c-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="7640c-166">Minimal'i seçerseniz, projenize yalnızca ASP.NET MVC için NuGet paketleri ve referansları eklenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="7640c-167">Tam seçeneği seçerseniz, Bir MVC projesi için gerekli içerik dosyalarının yanı sıra Minimal bağımlılıklar eklenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="7640c-168">İskele async denetleyicileri desteği, Entity Framework 6'nın yeni async özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="7640c-169">Daha fazla bilgi ve öğreticiler için, [ASP.NET İskele Genel bakınız.](aspnet-scaffolding-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7640c-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="7640c-170">Tarayıcı Bağlantısı – Tarayıcı ve Visual Studio arasındaki SignalR kanalı</span><span class="sxs-lookup"><span data-stu-id="7640c-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="7640c-171">Yeni [Tarayıcı Bağlantısı](using-browser-link.md) özelliği, birden fazla tarayıcıyı Visual Studio'ya bağlamanızı ve araç çubuğundaki bir düğmeyi tıklatarak hepsini yenilemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="7640c-172">Mobil emülatörler de dahil olmak üzere geliştirme sitenize birden fazla tarayıcı bağlayabilir ve tüm tarayıcıları aynı anda yenilemek için yenile'yi tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="7640c-173">Browser Link ayrıca geliştiricilerin Tarayıcı Bağlantısı uzantıları nı yazabilmeleri için bir API'yi de ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7640c-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="7640c-174">Geliştiricilerin Tarayıcı Bağlantısı API'si'nden yararlanmasını sağlayarak, Visual Studio ile bağlı herhangi bir tarayıcı arasındaki sınırları aşan çok gelişmiş senaryolar oluşturmak mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="7640c-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="7640c-175">Web Essentials, Visual Studio ve tarayıcının geliştirici araçları, mobil emülatörleri uzaktan kontrol etme ve çok daha fazlası arasında entegre bir deneyim oluşturmak için API'den yararlanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="7640c-176">Visual Studio Web Editörü Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7640c-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="7640c-177">Visual Studio 2013 web uygulamalarında Razor dosyaları ve HTML dosyaları için yeni bir HTML düzenleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="7640c-178">Yeni HTML düzenleyicisi HTML5 tabanlı tek bir birleşik şema sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="7640c-179">Otomatik ayraç tamamlama, jQuery UI ve AngularJS öznitelik IntelliSense, öznitelik IntelliSense Gruplama, KIMLIK ve sınıf adı Intellisense ve daha iyi performans, biçimlendirme ve SmartTags dahil olmak üzere diğer iyileştirmeler vardır.</span><span class="sxs-lookup"><span data-stu-id="7640c-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="7640c-180">Aşağıdaki ekran görüntüsü, HTML düzenleyicisinde Bootstrap özniteliği IntelliSense'in kullanılmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7640c-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![INtellisense IN HTML düzenleyicisi](release-notes/_static/image4.png)

<span data-ttu-id="7640c-182">Visual Studio 2013, hem CoffeeScript hem de DAHA AZ editörler dahili olarak da gelir.</span><span class="sxs-lookup"><span data-stu-id="7640c-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="7640c-183">LESS editörü CSS editörütüm serin özellikleri ile birlikte gelir ve @import zincirdeki tüm AZ belgeler arasında değişkenler ve mixins için özel Intellisense vardır.</span><span class="sxs-lookup"><span data-stu-id="7640c-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="7640c-184">Visual Studio'da Azure App Service Web Apps Desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="7640c-185">.NET 2.2 için Azure SDK ile Visual Studio 2013'te, uzak web uygulamalarınızla doğrudan etkileşim kurmak için **Server Explorer'ı** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="7640c-186">Azure hesabınızda oturum açabilir, yeni web uygulamaları oluşturabilir, uygulamaları yapılandırabilir, gerçek zamanlı günlükleri görüntüleyebilirsiniz ve daha fazlasını yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="7640c-187">SDK 2.2 yayımlandıktan kısa bir süre sonra Azure'da hata ayıklama modunda uzaktan çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="7640c-188">Azure App Service Web Apps'ın yeni özelliklerinin çoğu, .NET için Azure SDK'nın geçerli sürümüne yüklediğinizde Visual Studio 2012'de de çalışır.</span><span class="sxs-lookup"><span data-stu-id="7640c-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="7640c-189">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="7640c-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="7640c-190">Azure Uygulama Hizmeti'nde ASP.NET bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7640c-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="7640c-191">Visual Studio'yu kullanarak Azure Uygulama Hizmeti'ndeki bir web uygulamasını sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7640c-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="7640c-192">Web Yayımlama Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7640c-192">Web Publish Enhancements</span></span>

<span data-ttu-id="7640c-193">Visual Studio 2013 yeni ve gelişmiş Web Yayımlama özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="7640c-194">Bunlardan birkaçı şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7640c-194">Here are a few of them:</span></span>

- <span data-ttu-id="7640c-195">[Web.config dosya şifrelemeyi](https://go.microsoft.com/fwlink/?LinkId=325529)kolayca otomatikleştirin.</span><span class="sxs-lookup"><span data-stu-id="7640c-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="7640c-196">(Bu bağlantı ve 10/17 günün geç saatlerine kadar mevcut olmayabilir MSDN belgeleri için aşağıdaki iki nokta.)</span><span class="sxs-lookup"><span data-stu-id="7640c-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="7640c-197">Dağıtım sırasında uygulamayı çevrimdışı naalarak kolayca [otomatikleştirin.](https://go.microsoft.com/fwlink/?LinkId=325530)</span><span class="sxs-lookup"><span data-stu-id="7640c-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="7640c-198">Hangi dosyaların sunucuya kopyalanmasını gerektiğini belirlemek için [son değiştirilen tarih yerine dosya denetimi kullanmak](https://go.microsoft.com/fwlink/?LinkId=325531) üzere Web Dağıtımı'nı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7640c-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="7640c-199">FTP veya dosya sistemi yayımlama yöntemlerini kullanırken ve Web Dağıtımı'nda seçili dosyaları (Web.config dahil) hızla yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7640c-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="7640c-200">ASP.NET web dağıtımı hakkında daha fazla bilgi için [ASP.NET sitesine](https://go.microsoft.com/fwlink/?LinkId=322027)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="7640c-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="7640c-201">NuGet 2.7</span></span>

<span data-ttu-id="7640c-202">NuGet 2.7, [NuGet 2.7 Sürüm Notları'nda](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir yeni özellik kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="7640c-203">NuGet'in bu sürümü, Paketleri indirmek için NuGet'in paket geri yükleme özelliği için açık onay sağlama gereksinimini de ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7640c-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="7640c-204">NuGet'in kurulumu ile onay (ve NuGet'in tercihleri iletişim kutusundaki ilişkili onay kutusu) verilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="7640c-205">Şimdi paket geri yükleme sadece varsayılan olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="7640c-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="7640c-206">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="7640c-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="7640c-207">Bir ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7640c-207">One ASP.NET</span></span>

<span data-ttu-id="7640c-208">Web Formları proje şablonları, yeni One ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir.</span><span class="sxs-lookup"><span data-stu-id="7640c-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="7640c-209">Web Formları projenize MVC ve Web API desteği ekleyebilir ve One ASP.NET proje oluşturma sihirbazını kullanarak kimlik doğrulamasını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="7640c-210">Daha fazla bilgi için Visual [Studio 2013'te ASP.NET Web Projeleri Oluşturma'ya](creating-web-projects-in-visual-studio.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="7640c-211">ASP.NET Kimlik</span><span class="sxs-lookup"><span data-stu-id="7640c-211">ASP.NET Identity</span></span>

<span data-ttu-id="7640c-212">Web Formları proje şablonları yeni ASP.NET Kimlik çerçevesini destekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="7640c-213">Buna ek olarak, şablonlar artık bir Web Forms intranet projesinin oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="7640c-214">Daha fazla bilgi için Visual **Studio 2013'te ASP.NET Web Projeleri Oluşturmada** [Kimlik Doğrulama Yöntemleri'ne](creating-web-projects-in-visual-studio.md#auth) bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="7640c-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="7640c-215">Bootstrap</span></span>

<span data-ttu-id="7640c-216">Web Formları şablonları, şık ve duyarlı bir görünüm sağlamak ve kolayca özelleştirebileceğinizi hissetmek için [Bootstrap'ı](http://twitter.github.io/bootstrap/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="7640c-217">Daha fazla bilgi için [Visual Studio 2013 web proje şablonlarında Bootstrap'a](creating-web-projects-in-visual-studio.md#bootstrap)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="7640c-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="7640c-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="7640c-219">Bir ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7640c-219">One ASP.NET</span></span>

<span data-ttu-id="7640c-220">Web MVC proje şablonları, yeni One ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir.</span><span class="sxs-lookup"><span data-stu-id="7640c-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="7640c-221">One ASP.NET proje oluşturma sihirbazını kullanarak MVC projenizi özelleştirebilir ve kimlik doğrulamasını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="7640c-222">MVC 5'i ASP.NET için bir giriş eğitimi, [MVC 5'ASP.NET başlarken](../../../mvc/overview/getting-started/introduction/getting-started.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="7640c-223">MVC 4 projelerini MVC 5'e yükseltme hakkında bilgi için, [MVC 5 ve Web API 2'yi ASP.NET için ASP.NET MVC 4 ve Web API Projesi'ni nasıl yükseltilir'](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="7640c-224">ASP.NET Kimlik</span><span class="sxs-lookup"><span data-stu-id="7640c-224">ASP.NET Identity</span></span>

<span data-ttu-id="7640c-225">MVC proje şablonları kimlik doğrulama ve kimlik yönetimi için kimlik ASP.NET kullanmak üzere güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="7640c-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="7640c-226">Facebook ve Google kimlik doğrulama ve yeni üyelik API içeren bir öğretici [Facebook ve Google OAuth2 ve OpenID Oturum](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) açma ile ASP.NET bir MVC 5 App oluşturun ve [auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve Azure App Service dağıtmak](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="7640c-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="7640c-227">Bootstrap</span></span>

<span data-ttu-id="7640c-228">MVC proje şablonu, şık ve duyarlı bir görünüm sağlamak ve kolayca özelleştirebileceğinizi hissetmek için [Bootstrap'ı](http://getbootstrap.com/) kullanacak şekilde güncellendi.</span><span class="sxs-lookup"><span data-stu-id="7640c-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="7640c-229">Daha fazla bilgi için [Visual Studio 2013 web proje şablonlarında Bootstrap'a](creating-web-projects-in-visual-studio.md#bootstrap)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="7640c-230">Kimlik doğrulama filtreleri</span><span class="sxs-lookup"><span data-stu-id="7640c-230">Authentication filters</span></span>

<span data-ttu-id="7640c-231">Kimlik doğrulama filtreleri, ASP.NET MVC ardışık etki alanında yetkilendirme filtrelerinden önce çalışan ve tüm denetleyiciler için eylem başına, denetleyici başına veya genel olarak kimlik doğrulama mantığı belirtmenize olanak tanıyan ASP.NET MVC'deki yeni bir filtre türüdür.</span><span class="sxs-lookup"><span data-stu-id="7640c-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="7640c-232">Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve ilgili bir anapara sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="7640c-233">Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları da ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="7640c-234">Filtre geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="7640c-234">Filter overrides</span></span>

<span data-ttu-id="7640c-235">Artık bir geçersiz kılma filtresi belirterek, belirli bir eylem yöntemine veya denetleyicisine hangi filtrelerin uygulandığını geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="7640c-236">Geçersiz kılma filtreleri, belirli bir kapsam (eylem veya denetleyici) için çalıştırılmaması gereken bir filtre türü kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="7640c-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="7640c-237">Bu, genel olarak uygulanan filtreleri yapılandırmanıza, ancak daha sonra belirli genel filtrelerin belirli eylemlere veya denetleyicilere uygulanmasını hariç tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="7640c-238">Öznitelik yönlendirme</span><span class="sxs-lookup"><span data-stu-id="7640c-238">Attribute routing</span></span>

<span data-ttu-id="7640c-239">ASP.NET MVC şimdi öznitelik yönlendirme destekler, Tim McCall, yazarı [http://attributerouting.net](http://attributerouting.net)tarafından bir katkı sayesinde .</span><span class="sxs-lookup"><span data-stu-id="7640c-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="7640c-240">Öznitelik yönlendirmesi ile eylemlerinizi ve denetleyicilerinizi açıklamayaparak yollarınızı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="7640c-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="7640c-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="7640c-242">Öznitelik yönlendirme</span><span class="sxs-lookup"><span data-stu-id="7640c-242">Attribute routing</span></span>

<span data-ttu-id="7640c-243">ASP.NET Web API şimdi öznitelik yönlendirme destekler, Tim McCall, yazarı [http://attributerouting.net](http://attributerouting.net)tarafından bir katkı sayesinde .</span><span class="sxs-lookup"><span data-stu-id="7640c-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="7640c-244">Öznitelik yönlendirmesi ile eylemlerinizi ve denetleyicilerinizi şu şekilde ekleyerek Web API rotalarınızı belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7640c-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="7640c-245">Öznitelik yönlendirme, web API'nizdeki URI'ler üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="7640c-246">Örneğin, tek bir API denetleyicisi kullanarak bir kaynak hiyerarşisi kolayca tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7640c-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="7640c-247">Öznitelik yönlendirme, isteğe bağlı parametreleri, varsayılan değerleri ve rota kısıtlamalarını belirtmek için kullanışlı bir sözdizimi de sağlar:</span><span class="sxs-lookup"><span data-stu-id="7640c-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="7640c-248">Öznitelik yönlendirmesi hakkında daha fazla bilgi [için, Web API 2'de Öznitelik Yönlendirme'ye](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="7640c-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="7640c-249">OAuth 2.0</span></span>

<span data-ttu-id="7640c-250">Web API ve Tek Sayfa uygulaması proje şablonları artık OAuth 2.0 kullanarak yetkilendirmeyi destekliyor.</span><span class="sxs-lookup"><span data-stu-id="7640c-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="7640c-251">OAuth 2.0, istemcinin korunan kaynaklara erişimini yetkilendirmek için bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="7640c-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="7640c-252">Tarayıcılar ve mobil cihazlar da dahil olmak üzere çeşitli istemciler için çalışır.</span><span class="sxs-lookup"><span data-stu-id="7640c-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="7640c-253">OAuth 2.0 desteği, taşıyıcı kimlik doğrulaması ve yetkilendirme sunucusu rolünün uygulanması için Microsoft OWIN Bileşenleri tarafından sağlanan yeni güvenlik ara yazılımlarını temel almaktadır.</span><span class="sxs-lookup"><span data-stu-id="7640c-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="7640c-254">Alternatif olarak, istemciler Windows Server 2012 R2'de Azure Active Directory veya ADFS gibi bir kuruluş yetkilendirme sunucusu kullanılarak yetkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="7640c-255">OData Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7640c-255">OData Improvements</span></span>

<span data-ttu-id="7640c-256">**$select, $expand, $batch ve $value desteği**</span><span class="sxs-lookup"><span data-stu-id="7640c-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="7640c-257">ASP.NET Web API OData artık $select, $expand ve $value için tam desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7640c-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="7640c-258">Değişiklik kümelerinin istek toplu işlemesi ve işlenmesi için $batch da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="7640c-259">$select ve $expand seçenekleri, OData bitiş noktasından döndürülen verilerin şeklini değiştirmenize sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="7640c-260">Daha fazla bilgi için, [Web API OData'da $select ve $expand desteği tanıtma'ya](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="7640c-261">**Geliştirilmiş genişletilebilirlik**</span><span class="sxs-lookup"><span data-stu-id="7640c-261">**Improved extensibility**</span></span>

<span data-ttu-id="7640c-262">OData formatters artık genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="7640c-263">Atom girişi meta verilerini, adı geçen akışı ve medya bağlantısı girişlerini destekleyebilir, örnek ek açıklamalar ekleyebilir ve bağlantıların nasıl oluşturulduğunu özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="7640c-264">**Türüz destek**</span><span class="sxs-lookup"><span data-stu-id="7640c-264">**Type-less support**</span></span>

<span data-ttu-id="7640c-265">Artık varlık türleri için CLR türlerini tanımlamaya gerek kalmadan OData hizmetleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="7640c-266">Bunun yerine, OData denetleyicileriniz, OData'nın serihale/deserialize edilmesine neden olan **IEdmObject**örneklerini alabilir veya döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="7640c-267">**Varolan bir modeli yeniden kullanma**</span><span class="sxs-lookup"><span data-stu-id="7640c-267">**Reuse an existing model**</span></span>

<span data-ttu-id="7640c-268">Zaten varolan bir varlık veri modeli (EDM) varsa, artık yeni bir tane oluşturmak zorunda yerine doğrudan yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="7640c-269">Örneğin, Varlık Çerçevesi kullanıyorsanız, EF'nin sizin için oluşturduğu EDM'yi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="7640c-270">İstek Toplu İşlemi</span><span class="sxs-lookup"><span data-stu-id="7640c-270">Request Batching</span></span>

<span data-ttu-id="7640c-271">İstek toplu işlemi, ağ trafiğini azaltmak ve daha sorunsuz, daha az geveze bir kullanıcı arabirimi sağlamak için birden çok işlemi tek bir HTTP POST isteğinde birleştirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="7640c-272">ASP.NET Web API şimdi toplu talep için çeşitli stratejileri destekler:</span><span class="sxs-lookup"><span data-stu-id="7640c-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="7640c-273">Bir OData hizmetinin $batch bitiş noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7640c-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="7640c-274">Birden çok isteği tek bir MIME çok parçalı istekte paketle.</span><span class="sxs-lookup"><span data-stu-id="7640c-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="7640c-275">Özel bir toplu işlem biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="7640c-275">Use a custom batching format.</span></span>

<span data-ttu-id="7640c-276">İstek toplu çalışmasını etkinleştirmek için, Web API yapılandırmanıza toplu işleyiciiçeren bir rota eklemeniz yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="7640c-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="7640c-277">Ayrıca, isteklerin sırayla mı yoksa herhangi bir sırada mı yürütülmeyeceğini de denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="7640c-278">Taşınabilir ASP.NET Web API İstemci</span><span class="sxs-lookup"><span data-stu-id="7640c-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="7640c-279">Artık Windows Mağazası ve Windows Phone 8 uygulamalarınızda çalışan taşınabilir sınıf kitaplıkları oluşturmak için ASP.NET Web API İstemcisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="7640c-280">Ayrıca istemci ve sunucu arasında paylaşılabilir taşınabilir formatters oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="7640c-281">Geliştirilmiş Test Edilebilirlik</span><span class="sxs-lookup"><span data-stu-id="7640c-281">Improved Testability</span></span>

<span data-ttu-id="7640c-282">Web API 2, API denetleyicilerinizi birleştirmeyi çok daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="7640c-283">Api denetleyicinizi istek mesajınız ve yapılandırmanızla anında anında belirtin ve test etmek istediğiniz eylem yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="7640c-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="7640c-284">Bağlantı oluşturma gerçekleştiren eylem yöntemleri için **UrlHelper** sınıfıyla alay etmek de kolaydır.</span><span class="sxs-lookup"><span data-stu-id="7640c-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="7640c-285">ihttpactionresult</span><span class="sxs-lookup"><span data-stu-id="7640c-285">IHttpActionResult</span></span>

<span data-ttu-id="7640c-286">Artık Web API eylem yöntemlerinizin sonucunu kapsüllemek için IHttpActionResult uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="7640c-287">Bir Web API eylem yönteminden döndürülen bir IHttpActionResult, ortaya çıkan yanıt iletisini oluşturmak için ASP.NET Web API çalışma zamanı tarafından yürütülür.</span><span class="sxs-lookup"><span data-stu-id="7640c-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="7640c-288">Web API uygulamanızın birim testini basitleştirmek için herhangi bir Web API eyleminden bir IHttpActionResult döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="7640c-289">Kolaylık sağlamak için, belirli durum kodlarını, biçimlendirilmiş içeriği veya içerik leilgili yanıtları döndürmeye ilişkin sonuçlar da dahil olmak üzere kutunun dışında bir dizi IHttpActionResult uygulaması sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="7640c-290">httpRequestContext</span><span class="sxs-lookup"><span data-stu-id="7640c-290">HttpRequestContext</span></span>

<span data-ttu-id="7640c-291">Yeni **HttpRequestContext,** isteğe bağlı olan ancak istekten hemen kullanılamayan herhangi bir durumu izler.</span><span class="sxs-lookup"><span data-stu-id="7640c-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="7640c-292">Örneğin, rota verilerini, istekle ilişkili asıl kaynağı, istemci sertifikasını, **UrlHelper'ı** ve sanal yol kökünü almak için **HttpRequestContext'ı** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="7640c-293">Birim sınama amacıyla kolayca bir **HttpRequestContext** oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="7640c-294">İsteğin asıllığı **Thread.CurrentPrincipal'a**güvenmek yerine istekle birlikte aktığı ndan, asıl, web API ardışık ardışık ardışık ardışık olduğunda isteğin ömrü boyunca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="7640c-295">CORS</span><span class="sxs-lookup"><span data-stu-id="7640c-295">CORS</span></span>

<span data-ttu-id="7640c-296">Brock Allen başka bir büyük katkı sayesinde, ASP.NET şimdi tamamen Cross Origin İstek Paylaşımı (CORS) destekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="7640c-297">Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller.</span><span class="sxs-lookup"><span data-stu-id="7640c-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="7640c-298">[CORS,](http://www.w3.org/TR/cors/) bir sunucunun aynı orijin ilkesini gevşetmesine olanak tanıyan bir W3C standardıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="7640c-299">CORS'i kullanan sunucu, diğerlerini reddederken bazı kişiler arası isteklere açıkça izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="7640c-300">Web API 2 artık ön kontrol isteklerinin otomatik olarak işlenmesi de dahil olmak üzere CORS'u destekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="7640c-301">Daha fazla bilgi için bkz: [ASP.NET Web API'sinde Başlangıç Lar Arası İstekleri Etkinleştirme.](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="7640c-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="7640c-302">Kimlik Doğrulama Filtreleri</span><span class="sxs-lookup"><span data-stu-id="7640c-302">Authentication Filters</span></span>

<span data-ttu-id="7640c-303">Kimlik doğrulama filtreleri, ASP.NET Web API ardışık alt etki alanında yetkilendirme filtrelerinden önce çalışan ve tüm denetleyiciler için eylem başına, denetleyici başına veya genel olarak kimlik doğrulama mantığı belirtmenize olanak tanıyan ASP.NET Web API'sinde yeni bir tür filtredir.</span><span class="sxs-lookup"><span data-stu-id="7640c-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="7640c-304">Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve ilgili bir anapara sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="7640c-305">Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları da ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="7640c-306">Filtre Geçersiz Kılar</span><span class="sxs-lookup"><span data-stu-id="7640c-306">Filter Overrides</span></span>

<span data-ttu-id="7640c-307">Artık bir geçersiz kılma filtresi belirterek, belirli bir eylem yöntemine veya denetleyicisine hangi filtrelerin uygulandığını geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="7640c-308">Geçersiz kılma filtreleri, belirli bir kapsam (eylem veya denetleyici) için çalışmaması gereken bir filtre türü kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="7640c-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="7640c-309">Bu, genel filtreler eklemenize olanak tanır, ancak daha sonra bazılarını belirli eylemlerden veya denetleyicilerden hariç tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="7640c-310">OWIN Entegrasyonu</span><span class="sxs-lookup"><span data-stu-id="7640c-310">OWIN Integration</span></span>

<span data-ttu-id="7640c-311">ASP.NET Web API şimdi tam Olarak OWIN destekler ve herhangi bir OWIN yetenekli ana bilgisayarda çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="7640c-312">Ayrıca, OWIN kimlik doğrulama sistemiyle tümleştirme sağlayan bir **HostAuthenticationFiltresi** de dahildir.</span><span class="sxs-lookup"><span data-stu-id="7640c-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="7640c-313">OWIN tümleştirmesi ile, SignalR gibi diğer OWIN ara yazılımlarıyla birlikte kendi sürecinizde Web API'yi kendi ev sahipliğiyapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="7640c-314">Daha fazla bilgi için, [Web API'ASP.NET Self-Host için OWIN'i kullanın'](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)a bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="7640c-315">ASP.NET Sinyalci 2.0</span><span class="sxs-lookup"><span data-stu-id="7640c-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="7640c-316">Aşağıdaki bölümlerde SignalR 2.0'ın özellikleri açıklayınız.</span><span class="sxs-lookup"><span data-stu-id="7640c-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="7640c-317">OWIN üzerine inşa edilmiştir</span><span class="sxs-lookup"><span data-stu-id="7640c-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="7640c-318">MapHubs ve MapConnection artık MapSignalR vardır</span><span class="sxs-lookup"><span data-stu-id="7640c-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="7640c-319">Etki Alanı Arası Destek</span><span class="sxs-lookup"><span data-stu-id="7640c-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="7640c-320">MonoTouch ve MonoDroid ile iOS ve Android desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="7640c-321">Taşınabilir .NET İstemci</span><span class="sxs-lookup"><span data-stu-id="7640c-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="7640c-322">Yeni Self-Host Paketi</span><span class="sxs-lookup"><span data-stu-id="7640c-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="7640c-323">Geriye uyumlu sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="7640c-324">.NET 4.0 için kaldırılan sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="7640c-325">İstemci ve gruplar listesine ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="7640c-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="7640c-326">Belirli bir kullanıcıya ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="7640c-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="7640c-327">Daha iyi hata işleme desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="7640c-328">Hub'ların daha kolay birim testi</span><span class="sxs-lookup"><span data-stu-id="7640c-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="7640c-329">JavaScript hata işleme</span><span class="sxs-lookup"><span data-stu-id="7640c-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="7640c-330">Varolan bir 1.x projeyi SignalR 2.0'a yükseltme nin bir örneği için [bkz.](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)</span><span class="sxs-lookup"><span data-stu-id="7640c-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="7640c-331">OWIN üzerine inşa edilmiştir</span><span class="sxs-lookup"><span data-stu-id="7640c-331">Built on OWIN</span></span>

<span data-ttu-id="7640c-332">SignalR 2.0 tamamen [OWIN (.NET için Açık Web Arabirimi)](http://owin.org/)üzerine inşa edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7640c-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="7640c-333">Bu değişiklik, SignalR için kurulum işlemini web tarafından barındırılan ve kendi kendine barındırılan SignalR uygulamaları arasında çok daha tutarlı hale getirir, ancak bir dizi API değişikliği de gerektirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7640c-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="7640c-334">MapHubs ve MapConnection artık MapSignalR vardır</span><span class="sxs-lookup"><span data-stu-id="7640c-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="7640c-335">OWIN standartlarıyla uyumluluk için bu yöntemler in `MapSignalR`adı 'na yeniden verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7640c-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="7640c-336">`MapSignalR`parametrelerolmadan adlandırılan tüm hub'lar `MapHubs` (sürüm 1.x'te olduğu gibi) eşlenecektir; tek tek **PersistentConnection** nesnelerini eşlemek için, bağlantı türünü tür parametresi olarak ve bağlantının URL uzantısını ilk bağımsız değişken olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="7640c-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="7640c-337">Yöntem, `MapSignalR` Owin başlangıç sınıfında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7640c-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="7640c-338">Visual Studio 2013, Owin başlangıç sınıfı için yeni bir şablon içerir; bu şablonu kullanmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="7640c-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="7640c-339">Projeye sağ tıklayın</span><span class="sxs-lookup"><span data-stu-id="7640c-339">Right-click on the project</span></span>
2. <span data-ttu-id="7640c-340">**Ekle**, **Yeni Öğe'yi seçin...**</span><span class="sxs-lookup"><span data-stu-id="7640c-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="7640c-341">**Owin Başlangıç sınıf'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="7640c-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="7640c-342">Yeni sınıf **Startup.cs.**</span><span class="sxs-lookup"><span data-stu-id="7640c-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="7640c-343">Bir **Web uygulamasında,** `MapSignalR` yöntemi içeren Owin başlangıç sınıfı, aşağıda gösterildiği gibi Web.Config dosyasının uygulama ayarları düğümünde bir giriş kullanılarak Owin'in başlangıç sürecine eklenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="7640c-344">Kendi **kendine barındırılan**bir uygulamada, Başlangıç sınıfı `WebApp.Start` yöntemin tür parametresi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="7640c-345">**SignalR 1.x'teki hub'ları ve bağlantıları (bir web uygulamasındaki genel uygulama dosyasından):**</span><span class="sxs-lookup"><span data-stu-id="7640c-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="7640c-346">**SignalR 2.0'daki hub'ları ve bağlantıları eşleme (Owin Başlangıç sınıfı dosyasından):**</span><span class="sxs-lookup"><span data-stu-id="7640c-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="7640c-347">Kendi **kendine barındırılan**bir uygulamada, Başlangıç sınıfı aşağıda `WebApp.Start` gösterildiği gibi yöntemin tür parametresi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="7640c-348">Etki Alanı Arası Destek</span><span class="sxs-lookup"><span data-stu-id="7640c-348">Cross-Domain Support</span></span>

<span data-ttu-id="7640c-349">SignalR 1.x'te, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağı tarafından denetlendi.</span><span class="sxs-lookup"><span data-stu-id="7640c-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="7640c-350">Bu bayrak hem JSONP hem de CORS isteklerini denetler.</span><span class="sxs-lookup"><span data-stu-id="7640c-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="7640c-351">Daha fazla esneklik için, tüm CORS desteği SignalR'ın sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının bunu desteklediği algılanırsa hala KORS'u kullanır) ve bu senaryoları desteklemek için yeni OWIN ara yazılımları kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7640c-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="7640c-352">SignalR 2.0'da, istemcide JSONP gerekiyorsa (eski tarayıcılarda etki alanları arası isteklerini desteklemek için), `EnableJSONP` aşağıda `HubConfiguration` gösterildiği `true`gibi nesneüzerinde ayarlayarak açıkça etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7640c-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="7640c-353">JSONP, CORS'ten daha az güvenli olduğu için varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7640c-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="7640c-354">SignalR 2.0'a yeni CORS ara yazılımını eklemek `Microsoft.Owin.Cors` için, `UseCors` aşağıdaki bölümde gösterildiği gibi kitaplığı projenize ekleyin ve SignalR ara yazılımınızdan önce arayın.</span><span class="sxs-lookup"><span data-stu-id="7640c-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="7640c-355">**Projenize Microsoft.Owin.Cors ekleme**: Bu kitaplığı yüklemek için Paket Yöneticisi Konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7640c-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="7640c-356">Bu komut, paketin 2.0.0 sürümünü projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="7640c-357">**UseCors'u Arama**</span><span class="sxs-lookup"><span data-stu-id="7640c-357">**Calling UseCors**</span></span>

<span data-ttu-id="7640c-358">Aşağıdaki kod parçacıkları SignalR 1.x ve 2.0'da etki alanları arası bağlantıların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7640c-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="7640c-359">**SignalR 1.x'te (genel uygulama dosyasından) etki alanları arası isteklerin uygulanması**</span><span class="sxs-lookup"><span data-stu-id="7640c-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="7640c-360">**SignalR 2.0'da etki alanları arası isteklerin uygulanması (C# kod dosyasından)**</span><span class="sxs-lookup"><span data-stu-id="7640c-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="7640c-361">Aşağıdaki kod, SignalR 2.0 projesinde CORS veya JSONP'nin nasıl etkinleştirilen gösteriş olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7640c-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="7640c-362">Bu kod `Map` örneği, `RunSignalR` `MapSignalR`CORS ara yazılımının yalnızca CORS desteği gerektiren SignalR istekleri için (belirtilen `MapSignalR`yoldaki tüm trafikler yerine . `Map` tüm uygulama yerine belirli bir URL öneki için çalışması gereken diğer ara yazılımlar için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="7640c-363">MonoTouch ve MonoDroid ile iOS ve Android desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="7640c-364">[Xamarin kütüphanesinden](https://xamarin.com/)MonoTouch ve MonoDroid bileşenleri kullanan iOS ve Android istemcileri için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="7640c-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="7640c-365">Bunların nasıl kullanılacağı hakkında daha fazla bilgi için Bkz. [Xamarin Bileşenlerini Kullanma.](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)</span><span class="sxs-lookup"><span data-stu-id="7640c-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="7640c-366">SignalR RTW sürümü kullanılabilir olduğunda bu bileşenler [Xamarin Mağazası'nda](https://store.xamarin.com/) kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="7640c-367">### Taşınabilir .NET istemcisi</span><span class="sxs-lookup"><span data-stu-id="7640c-367">### Portable .NET client</span></span>

<span data-ttu-id="7640c-368">Platformlar arası geliştirmeyi daha iyi kolaylaştırmak için Silverlight, WinRT ve Windows Phone istemcileri aşağıdaki platformları destekleyen tek bir taşınabilir .NET istemcisiyle değiştirildi:</span><span class="sxs-lookup"><span data-stu-id="7640c-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="7640c-369">NET 4,5</span><span class="sxs-lookup"><span data-stu-id="7640c-369">NET 4.5</span></span>
- <span data-ttu-id="7640c-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="7640c-370">Silverlight 5</span></span>
- <span data-ttu-id="7640c-371">WinRT (Windows Mağazası Uygulamaları için.NET)</span><span class="sxs-lookup"><span data-stu-id="7640c-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="7640c-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="7640c-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="7640c-373">Yeni Self-Host Paketi</span><span class="sxs-lookup"><span data-stu-id="7640c-373">New Self-Host Package</span></span>

<span data-ttu-id="7640c-374">Artık SignalR Self-Host (bir web sunucusunda barındırılmak yerine bir işlem veya başka bir uygulamada barındırılan SignalR uygulamaları) ile başlamayı kolaylaştıran bir NuGet paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="7640c-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="7640c-375">SignalR 1.x ile oluşturulmuş bir kendi kendine barındıran projeyi yükseltmek için Microsoft.AspNet.SignalR.Owin paketini kaldırın ve Microsoft.AspNet.SignalR.SelfHost paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7640c-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="7640c-376">Self-host paketi ile başlamak hakkında daha fazla bilgi için, [Bkz. Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="7640c-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="7640c-377">Geriye uyumlu sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-377">Backward-compatible server support</span></span>

<span data-ttu-id="7640c-378">SignalR'ın önceki sürümlerinde, istemcide ve sunucuda kullanılan SignalR paketinin sürümlerinin aynı olması gerekiyordu.</span><span class="sxs-lookup"><span data-stu-id="7640c-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="7640c-379">Güncellemesi zor olan kalın istemci uygulamalarını desteklemek için SignalR 2.0 artık eski bir istemciye sahip daha yeni bir sunucu sürümünü kullanmayı destekliyor.</span><span class="sxs-lookup"><span data-stu-id="7640c-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="7640c-380">**Not: SignalR 2.0, eski sürümlerle oluşturulmuş sunucuları yeni istemcilerle desteklemez.**</span><span class="sxs-lookup"><span data-stu-id="7640c-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="7640c-381">.NET 4.0 için kaldırılan sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="7640c-382">SignalR 2.0,.NET 4.0 ile sunucu birlikte çalışabilirliği için destek düştü.</span><span class="sxs-lookup"><span data-stu-id="7640c-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="7640c-383">.NET 4.5 SignalR 2.0 sunucuları ile kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="7640c-384">SignalR 2.0 için bir .NET 4.0 istemcisi hala vardır.</span><span class="sxs-lookup"><span data-stu-id="7640c-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="7640c-385">İstemci ve gruplar listesine ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="7640c-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="7640c-386">SignalR 2.0'da, istemci ve grup dislerinin listesini kullanarak ileti göndermek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7640c-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="7640c-387">Aşağıdaki kod parçacıkları bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7640c-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="7640c-388">**PersistentConnection'ı kullanan istemciler ve gruplar listesine ileti gönderme**</span><span class="sxs-lookup"><span data-stu-id="7640c-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="7640c-389">**Hub'ları kullanan istemciler ve gruplar listesine ileti gönderme**</span><span class="sxs-lookup"><span data-stu-id="7640c-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="7640c-390">Belirli bir kullanıcıya ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="7640c-390">Sending a message to a specific user</span></span>

<span data-ttu-id="7640c-391">Bu özellik, kullanıcıların yeni bir arayüz iUserIdProvider üzerinden bir IRequest'e dayalı kullanıcı Kimliği'nin ne olduğunu belirtmelerine olanak tanır:</span><span class="sxs-lookup"><span data-stu-id="7640c-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="7640c-392">**IUserIdProvider arabirimi**</span><span class="sxs-lookup"><span data-stu-id="7640c-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="7640c-393">Varsayılan olarak, kullanıcı adı olarak kullanıcının IPrincipal.Identity.Name kullanan bir uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="7640c-394">Hub'larda, bu kullanıcılara yeni bir API aracılığıyla ileti gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7640c-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="7640c-395">**Clients.User API'yi kullanma**</span><span class="sxs-lookup"><span data-stu-id="7640c-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="7640c-396">Daha İyi Hata İşleme Desteği</span><span class="sxs-lookup"><span data-stu-id="7640c-396">Better Error Handling Support</span></span>

<span data-ttu-id="7640c-397">Kullanıcılar artık **hubexception'ı** herhangi bir hub çağırmasından atabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="7640c-398">**HubException'ın** oluşturucusu bir dize iletisi ve nesne ekstra hata verileri alabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="7640c-399">SignalR özel durumu otomatik olarak serihale getirir ve hub yöntemi çağırmasını reddetmek/başarısız yapmak için kullanılacağı istemciye gönderir.</span><span class="sxs-lookup"><span data-stu-id="7640c-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="7640c-400">**Ayrıntılı hub özel durumları ayarı,** **HubException'ın** istemciye geri gönderilmesi veya gönderilmemesi ile ilgili bir etkiye sahip değildir; her zaman gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="7640c-401">**İstemciye HubException göndermeyi gösteren sunucu tarafı kodu**</span><span class="sxs-lookup"><span data-stu-id="7640c-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="7640c-402">**JavaScript istemci kodu sunucudan gönderilen bir HubException yanıt gösteren**</span><span class="sxs-lookup"><span data-stu-id="7640c-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="7640c-403">**Sunucudan gönderilen HubException'a yanıt veren .NET istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="7640c-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="7640c-404">Hub'ların daha kolay birim testi</span><span class="sxs-lookup"><span data-stu-id="7640c-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="7640c-405">SignalR 2.0, Hub'larda sahte `IHubCallerConnectionContext` istemci tarafı çağrıları oluşturmayı kolaylaştıran bir arabirim içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="7640c-406">Aşağıdaki kod parçacıkları popüler test koşumları [xUnit.net](https://github.com/xunit/xunit) ve [moq](https://code.google.com/p/moq/)ile bu arayüzü kullanarak göstermek.</span><span class="sxs-lookup"><span data-stu-id="7640c-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="7640c-407">**xUnit.net ile Unit test SignalR**</span><span class="sxs-lookup"><span data-stu-id="7640c-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="7640c-408">**Birim test SignalR ile moq**</span><span class="sxs-lookup"><span data-stu-id="7640c-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="7640c-409">JavaScript hata işleme</span><span class="sxs-lookup"><span data-stu-id="7640c-409">JavaScript error handling</span></span>

<span data-ttu-id="7640c-410">SignalR 2.0'da, tüm JavaScript hata işleme geri aramaları ham dizeleri yerine JavaScript hata nesnelerini döndürer.</span><span class="sxs-lookup"><span data-stu-id="7640c-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="7640c-411">Bu, SignalR'ın hata işleyicilerinize daha zengin bilgiler akışını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="7640c-412">Hata özelliğinden `source` iç özel durum alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="7640c-413">**Başlat.Başarısız özel durumu işleyen JavaScript istemci kodu**</span><span class="sxs-lookup"><span data-stu-id="7640c-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="7640c-414">ASP.NET Kimlik</span><span class="sxs-lookup"><span data-stu-id="7640c-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="7640c-415">Yeni ASP.NET Üyelik Sistemi</span><span class="sxs-lookup"><span data-stu-id="7640c-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="7640c-416">ASP.NET Kimlik ASP.NET başvurular için yeni üyelik sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7640c-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="7640c-417">ASP.NET Kimlik, kullanıcıya özel profil verilerini uygulama verileriyle tümleştirmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7640c-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="7640c-418">ASP.NET Kimlik, uygulamanızdaki kullanıcı profilleri için kalıcılık modelini seçmenize de olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7640c-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="7640c-419">Verileri, Azure Depolama Tabloları gibi NoSQL veri depoları da dahil olmak üzere bir SQL Server veritabanında veya başka bir veri deposunda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="7640c-420">Daha fazla bilgi için **Visual Studio 2013'te ASP.NET Web Projeleri Oluştururken** [Bireysel Kullanıcı Hesapları'na](creating-web-projects-in-visual-studio.md#indauth) bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="7640c-421">Beyana dayalı kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="7640c-421">Claims-based authentication</span></span>

<span data-ttu-id="7640c-422">ASP.NET artık, kullanıcının kimliğinin güvenilir bir verenden gelen bir talep kümesi olarak temsil edildiği taleplere dayalı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="7640c-423">Kullanıcılar, bir uygulama veritabanında tutulan bir kullanıcı adı ve parola kullanılarak veya sosyal kimlik sağlayıcıları (örneğin: Microsoft Hesapları, Facebook, Google, Twitter) kullanılarak veya Azure Etkin Dizin veya Active Directory Federation Services (ADFS) aracılığıyla kuruluş hesaplarını kullanarak kimlik doğrulaması yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="7640c-424">Azure Active Directory ve Windows Server Active Directory ile Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="7640c-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="7640c-425">Artık kimlik doğrulaması için Azure Active Directory veya Windows Server Active Directory (AD) kullanan ASP.NET projeler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="7640c-426">Daha fazla bilgi için **Visual Studio 2013'te ASP.NET Web Projeleri Oluştururken** [Kuruluş Hesapları'na](creating-web-projects-in-visual-studio.md#orgauth) bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="7640c-427">OWIN Entegrasyonu</span><span class="sxs-lookup"><span data-stu-id="7640c-427">OWIN Integration</span></span>

<span data-ttu-id="7640c-428">ASP.NET kimlik doğrulaması artık herhangi bir OWIN tabanlı ana bilgisayarda kullanılabilen OWIN ara yazılımlarını temel alınr.</span><span class="sxs-lookup"><span data-stu-id="7640c-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="7640c-429">OWIN hakkında daha fazla bilgi için aşağıdaki [Microsoft OWIN Bileşenleri](#TOC7) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="7640c-430">Microsoft OWIN Bileşenleri</span><span class="sxs-lookup"><span data-stu-id="7640c-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="7640c-431">[.NET](http://owin.org/) için Açık Web Arabirimi (OWIN), .NET web sunucuları ve web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="7640c-432">OWIN web uygulamasını sunucudan ayırarak web uygulamalarını ana bilgisayar-agnostik hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="7640c-433">Örneğin, IIS'de OWIN tabanlı bir web uygulamasını barındırabilir veya özel bir işlemle kendi kendine barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="7640c-434">Microsoft OWIN bileşenlerinde (Katana projesi olarak da bilinir) tanıtılan değişiklikler, yeni sunucu ve ana bilgisayar bileşenlerini, yeni yardımcı kitaplıkları ve ara yazılımları ve yeni kimlik doğrulama ara yazılımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="7640c-435">OWIN ve Katana hakkında daha fazla bilgi için, [OWIN ve Katana yenilikleri](../../../aspnet/overview/owin-and-katana/index.md)hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="7640c-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="7640c-436">**Not: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamaları IIS klasik modunda çalıştırılamaz; entegre modda çalıştırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="7640c-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="7640c-437">**Not: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamaları tam güven içinde çalıştırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="7640c-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="7640c-438">Yeni Sunucular ve Ana Bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="7640c-438">New Servers and Hosts</span></span>

<span data-ttu-id="7640c-439">Bu sürümle, kendi kendine barındırış senaryolarını etkinleştirmek için yeni bileşenler eklendi.</span><span class="sxs-lookup"><span data-stu-id="7640c-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="7640c-440">Bu bileşenler aşağıdaki NuGet paketlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="7640c-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="7640c-441">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="7640c-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="7640c-442">HTTP isteklerini dinlemek ve bunları OWIN ardışık boru hattına yönlendirmek için **HttpListener'ı** kullanan bir OWIN sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="7640c-443">**Microsoft.Owin.Hosting,** konsol uygulaması veya Windows hizmeti gibi özel bir işlemle bir OWIN ardışık hattını kendi kendine barındırmak isteyen geliştiriciler için bir kitaplık sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="7640c-444">**OwinHost**.</span><span class="sxs-lookup"><span data-stu-id="7640c-444">**OwinHost**.</span></span> <span data-ttu-id="7640c-445">Özel bir ana bilgisayar uygulaması `Microsoft.Owin.Hosting` yazmak zorunda kalmadan bir OWIN ardışık hattını saran ve barındırmanızı sağlayan tek başına çalıştırılabilir bir yürütme sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="7640c-446">Buna ek `Microsoft.Owin.Host.SystemWeb` olarak, paket artık middleware **SystemWeb** sunucusuna ipuçları sağlamak için izin, middleware belirli bir ASP.NET boru hattı aşamasında çağrılması gerektiğini belirten sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="7640c-447">Bu özellik, özellikle ASP.NET ardışık çalışması gereken kimlik doğrulama ara ware için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="7640c-448">Yardımcı Kütüphaneler ve Middleware</span><span class="sxs-lookup"><span data-stu-id="7640c-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="7640c-449">OWIN belirtiminden yalnızca işlev ve tür tanımlarını kullanarak OWIN `Microsoft.Owin` bileşenleri yazabilirsiniz, ancak yeni paket daha kullanıcı dostu bir soyutlama kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="7640c-450">Bu paket, daha önceki birkaç paketi `Owin.Extensions`(örn. , , ) `Owin.Types`diğer OWIN bileşenleri tarafından kolayca kullanılabilen tek ve iyi yapılandırılmış bir nesne modelinde birleştirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="7640c-451">Aslında, Microsoft OWIN bileşenlerinin çoğu artık bu paketi kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7640c-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="7640c-452">[OWIN](http://www.owin.org) uygulamaları IIS klasik modunda çalıştırılamaz; entegre modda çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="7640c-453">[OWIN](http://www.owin.org) uygulamaları tam güven içinde çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="7640c-454">Bu sürüm, çalışan bir OWIN uygulamasını doğrulamak için ara yazılım ların yanı sıra hataları araştırmaya yardımcı olacak hata sayfası ara yazılımını da içeren Microsoft.Owin.Diagnostics paketini de içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="7640c-455">Kimlik Doğrulama Bileşenleri</span><span class="sxs-lookup"><span data-stu-id="7640c-455">Authentication Components</span></span>

<span data-ttu-id="7640c-456">Aşağıdaki kimlik doğrulama bileşenleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-456">The following authentication components are available.</span></span>

- <span data-ttu-id="7640c-457">**Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="7640c-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="7640c-458">Şirket içi veya bulut tabanlı dizin hizmetlerini kullanarak kimlik doğrulamayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7640c-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="7640c-459">**Microsoft.Owin.Security.Cookies** tanımlama bilgilerini kullanarak kimlik doğrulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="7640c-460">Bu paket daha `Microsoft.Owin.Security.Forms`önce seçildi.</span><span class="sxs-lookup"><span data-stu-id="7640c-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="7640c-461">**Microsoft.Owin.Security.Facebook,** Facebook'un OAuth tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştiri.</span><span class="sxs-lookup"><span data-stu-id="7640c-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="7640c-462">**Microsoft.Owin.Security.Google,** Google'ın OpenID tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="7640c-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="7640c-463">**Microsoft.Owin.Security.Jwt** JWT belirteçleri kullanarak kimlik doğrulamasağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="7640c-464">**Microsoft.Owin.Security.MicrosoftAccount** Microsoft hesaplarını kullanarak kimlik doğrulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="7640c-465">**Microsoft.Owin.Security.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="7640c-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="7640c-466">Taşıyıcı belirteçlerinin doğruluğunu doğrulamak için bir OAuth yetkilendirme sunucusunun yanı sıra ara yazılım sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="7640c-467">**Microsoft.Owin.Security.Twitter,** Twitter'ın OAuth tabanlı hizmetini kullanarak kimlik doğrulamayı etkinleştiri.</span><span class="sxs-lookup"><span data-stu-id="7640c-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="7640c-468">Bu sürüm, `Microsoft.Owin.Cors` çapraz kökenli HTTP isteklerini işlemek için ara yazılım içeren paketi de içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="7640c-469">Visual Studio 2013'ün son sürümünde JWT imza desteği kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="7640c-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="7640c-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="7640c-470">Entity Framework 6</span></span>

<span data-ttu-id="7640c-471">Varlık Çerçevesi 6'daki yeni özelliklerin ve diğer değişikliklerin listesi için Entity [Framework Version History](https://msdn.com/data/jj574253)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="7640c-472">ASP.NET Jilet 3</span><span class="sxs-lookup"><span data-stu-id="7640c-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="7640c-473">ASP.NET Razor 3 aşağıdaki yeni özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="7640c-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="7640c-474">Sekme düzenlemesi için destek.</span><span class="sxs-lookup"><span data-stu-id="7640c-474">Support for Tab editing.</span></span> <span data-ttu-id="7640c-475">Daha önce, Belgeyi **Biçimlendir** komutu, Visual Studio'da otomatik girintisi ve otomatik biçimlendirme **Sekmeleri Tut** seçeneğini kullanırken doğru çalışmadı.</span><span class="sxs-lookup"><span data-stu-id="7640c-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="7640c-476">Bu değişiklik, sekme biçimlendirmesi için Razor kodu için Visual Studio biçimlendirmesini düzeltir.</span><span class="sxs-lookup"><span data-stu-id="7640c-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="7640c-477">Bağlantılar oluştururken URL Yeniden Yazma kuralları için destek.</span><span class="sxs-lookup"><span data-stu-id="7640c-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="7640c-478">Güvenlik saydam özniteliği kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7640c-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="7640c-479">Bu bir kırılma değişikliğidir ve Razor 3'ün MVC4 ve daha öncekilerle uyumsuz olmasına neden olarak, Razor 2 MVC5 veya MVC5'e karşı derlenen derlemelerle uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="7640c-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="7640c-480">Visual Studio sabit Razor 3 sorunları 2013 ön sürüm [sürümleriburada](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)bulabilirsiniz .</span><span class="sxs-lookup"><span data-stu-id="7640c-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="7640c-481">ASP.NET Uygulama Askıya Alma</span><span class="sxs-lookup"><span data-stu-id="7640c-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="7640c-482">ASP.NET App Suspend, .NET Framework 4.5.1'de çok sayıda ASP.NET siteyi tek bir makinede barındırmak için kullanıcı deneyimini ve ekonomik modeli kökten değiştiren bir oyun değiştirme özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7640c-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="7640c-483">Daha fazla bilgi için, ASP.NET App Askıya Alma [– duyarlı paylaşılan .NET web barındırma](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="7640c-484">Bilinen Sorunlar ve Son Dakika Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="7640c-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="7640c-485">Bu bölümde, Visual Studio 2013 için ASP.NET ve Web Araçları'ndaki bilinen sorunlar ve kırılma değişiklikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7640c-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="7640c-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="7640c-486">NuGet</span></span>

- <span data-ttu-id="7640c-487">[Yeni paket geri yükleme SLN dosyayı kullanırken Mono çalışmıyor](https://nuget.codeplex.com/workitem/3596) - yaklaşan nuget.exe indirme ve [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleme sabit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="7640c-488">[Yeni paket geri yükleme Wix projeleri ile çalışmıyor](https://nuget.codeplex.com/workitem/3598) - yaklaşan nuget.exe indirme ve [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleme sabit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="7640c-489">[Otomatik Paket geri yüklemesi bir çözüm klasörü altındaki projelerde çalışmaz](https://nuget.codeplex.com/workitem/3625) – NuGet 2.8'de sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="7640c-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="7640c-490">ASP.NET Web API'si</span><span class="sxs-lookup"><span data-stu-id="7640c-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="7640c-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`biz destek `IQueryable<T>` `$select` ve ekledi her zaman `$expand`dönmez .</span><span class="sxs-lookup"><span data-stu-id="7640c-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="7640c-492">Bizim önceki `ODataQueryOptions<T>` örnekler için her zaman `ApplyTo` `IQueryable<T>`gelen dönüş değeri attı .</span><span class="sxs-lookup"><span data-stu-id="7640c-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="7640c-493">Daha önce desteklediğimiz sorgu seçenekleri (`$filter` `$orderby`, `$skip` `$top`, , ) sorgunun şeklini değiştirmediği için bu daha önce çalıştı.</span><span class="sxs-lookup"><span data-stu-id="7640c-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="7640c-494">Şimdi biz `$select` destek `$expand` ve geri `ApplyTo` dönüş `IQueryable<T>` değeri her zaman olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="7640c-495">Örnek kodu daha önce kullanıyorsanız, istemci göndermezse `$select` çalışmaya devam `$expand`eder ve .</span><span class="sxs-lookup"><span data-stu-id="7640c-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="7640c-496">Ancak, desteklemek `$select` istiyorsanız ve `$expand` bu kodu değiştirmek zorunda.</span><span class="sxs-lookup"><span data-stu-id="7640c-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="7640c-497">**Request.Url veya RequestContext.Url toplu iş isteği sırasında geçersizdir**</span><span class="sxs-lookup"><span data-stu-id="7640c-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="7640c-498">Bir toplu işlem senaryosunda, **UrlHelper** **Request.Url** veya **RequestContext.Url'den**erişildiğinde geçersizdir.</span><span class="sxs-lookup"><span data-stu-id="7640c-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="7640c-499">Bu sorun şu anda burada izlenir: [BatchRequestContext.Url toplu istek için null .](http://aspnetwebstack.codeplex.com/workitem/1301)</span><span class="sxs-lookup"><span data-stu-id="7640c-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="7640c-500">Bu sorun için geçici çözüm **UrlHelper**yeni bir örnek oluşturmaktır , aşağıdaki örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="7640c-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="7640c-501">**UrlHelper'ın yeni bir örneğini oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7640c-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="7640c-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="7640c-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="7640c-503">MVC5 ve OrgAuth kullanırken, AntiForgerToken doğrulama yapmak görünümlere sahipseniz, görünüme veri deftere naklettiğinizde aşağıdaki hata yla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7640c-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="7640c-504">**Hata**:</span><span class="sxs-lookup"><span data-stu-id="7640c-504">**Error**:</span></span>

    <span data-ttu-id="7640c-505">*'/' Uygulamasında Sunucu Hatası.*</span><span class="sxs-lookup"><span data-stu-id="7640c-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="7640c-506"><em>' ' veya<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' ' türü iddiası, sağlanan ClaimsIdentity'de mevcut değildi. Talep tabanlı kimlik doğrulamayla sahteciliğe karşı destek sağlamak için, lütfen yapılandırılan talep sağlayıcısının bu taleplerin her ikisini de oluşturduğu ClaimsIdentity örneklerinde sağladığını doğrulayın. Yapılandırılan talep sağlayıcısı bunun yerine benzersiz bir tanımlayıcı olarak farklı bir talep türü kullanıyorsa, statik özellik AntiForgeryConfig.UniqueClaimTypeIdentifier ayarlayarak yapılandırılabilir.</em></span><span class="sxs-lookup"><span data-stu-id="7640c-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="7640c-507">**Geçici Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="7640c-507">**Workaround**:</span></span>

    <span data-ttu-id="7640c-508">Düzeltmek için Global.asax'a aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7640c-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="7640c-509">Bu, bir sonraki sürüm için düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="7640c-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="7640c-510">Bir MVC4 uygulamasını MVC5'e yükselttikten sonra, çözümü oluşturun ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="7640c-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="7640c-511">Aşağıdaki hatayı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="7640c-511">You should see the following error:</span></span>

    <span data-ttu-id="7640c-512">[A] System.Web.WebPages.Razor.Configuration.HostSection [B]System.Web.WebPages.Razor.Configuration.HostSection için döküm olamaz.</span><span class="sxs-lookup"><span data-stu-id="7640c-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="7640c-513">A türü 'System.Web.WebPages.Razor' adresinden gelir, Sürüm=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' adresindeki 'Varsayılan'\_konumunda 'C:\windows\Microsoft.Net\assembly\GAC MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0\_\_31bf3856ad364e35\System..WebPages.d.d.</span><span class="sxs-lookup"><span data-stu-id="7640c-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="7640c-514">B türü 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' bağlamında 'Varsayılan' konumunda 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d 05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="7640c-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="7640c-515">Yukarıdaki hatayı düzeltmek için, projenizdeki *tüm* Web.config dosyalarını (Görünümler klasöründekiler dahil) açın ve aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="7640c-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="7640c-516">"System.Web.Mvc"in "4.0.0.0" sürümünün tüm oluşumlarını "5.0.0.0" olarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7640c-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="7640c-517">"System.Web.Helpers", &quot;System.Web.WebPages and&quot; &quot;System.WebPages.Razor&quot; sürümü "2.0.0.0" tüm oluşumları güncelleme "3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="7640c-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="7640c-518">Örneğin, yukarıdaki değişiklikleri yaptıktan sonra, derleme bağlamaları aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="7640c-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="7640c-519">MVC 4 projelerini MVC 5'e yükseltme hakkında bilgi için, [MVC 5 ve Web API 2'yi ASP.NET için ASP.NET MVC 4 ve Web API Projesi'ni nasıl yükseltilir'](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="7640c-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="7640c-520">jQuery Unobtrusive Doğrulama ile istemci tarafı doğrulama kullanırken, doğrulama iletisi bazen type='number' olan bir HTML giriş öğesi için yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="7640c-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="7640c-521">Geçersiz bir sayı girildiğinde, gerekli bir değer için doğrulama hatası ("Yaş alanı gereklidir") geçerli bir sayının gerekli olduğu doğru ileti yerine gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="7640c-522">Bu sorun genellikle Oluşturma ve Düzenley görünümleri üzerinde bir tamsayı özelliği olan bir model için iskele kodu ile bulunur.</span><span class="sxs-lookup"><span data-stu-id="7640c-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="7640c-523">Bu sorunu çözmek için düzenleyici yardımcıyı aşağıdakilerden değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7640c-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="7640c-524">Hedef:</span><span class="sxs-lookup"><span data-stu-id="7640c-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="7640c-525">ASP.NET MVC 5 artık kısmi güveni desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="7640c-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="7640c-526">MVC veya WebAPI ikililerine bağlanan projeler [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) özniteliğini ve [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) özniteliğini kaldırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7640c-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="7640c-527">Bu öznitelikleri kaldırmak aşağıdaki gibi derleyici hataları ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7640c-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="7640c-528">Not, bunun bir yan etkisi olarak aynı uygulamada 4.0 ve 5.0 derlemeleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="7640c-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="7640c-529">Hepsini 5.0 olarak güncellemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7640c-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="7640c-530">Facebook yetkilendirmeli SPA Şablonu, web sitesi intranet bölgesinde barındırılırken IE'de istikrarsızlığa neden olabilir</span><span class="sxs-lookup"><span data-stu-id="7640c-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="7640c-531">SPA şablonu Facebook ile harici oturum açma sağlar.</span><span class="sxs-lookup"><span data-stu-id="7640c-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="7640c-532">Şablonla oluşturulan proje yerel olarak çalışırken, oturum açma IE'nin çökmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7640c-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="7640c-533">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="7640c-533">Solution:</span></span>

1. <span data-ttu-id="7640c-534">Web sitesini internet bölgesinde barındırın; Veya</span><span class="sxs-lookup"><span data-stu-id="7640c-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="7640c-535">Senaryoyu IE dışındaki bir tarayıcıda test edin.</span><span class="sxs-lookup"><span data-stu-id="7640c-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="7640c-536">Web Formları İskele</span><span class="sxs-lookup"><span data-stu-id="7640c-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="7640c-537">Web Forms İskelesi VS2013'ten kaldırıldı ve Visual Studio için gelecekteki bir güncellemede kullanıma sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7640c-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="7640c-538">Ancak, MVC bağımlılıkları ekleyerek ve MVC için iskele oluşturarak bir Web Forms projesi içinde iskele kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7640c-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="7640c-539">Projeniz Web Formları ve MVC'nin bir birleşimini içerir.</span><span class="sxs-lookup"><span data-stu-id="7640c-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="7640c-540">Web Formları projenize MVC eklemek için yeni bir iskele öğesi ekleyin ve **MVC 5 Bağımlılıkları'nı**seçin.</span><span class="sxs-lookup"><span data-stu-id="7640c-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="7640c-541">Komut dosyaları gibi tüm içerik dosyalarına ihtiyacınız olup olmadığına bağlı olarak Minimal veya Tam'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7640c-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="7640c-542">Ardından, MVC için, projenizde görünümler ve denetleyici oluşturacak bir iskele öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7640c-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="7640c-543">MVC ve Web API İskele - HTTP 404, Bulunamadı hatası</span><span class="sxs-lookup"><span data-stu-id="7640c-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="7640c-544">Bir projeye iskeleye ayrılmış bir öğe eklerken bir hatayla karşılaşılırsa, projenizin tutarsız bir durumda kalması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7640c-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="7640c-545">İskele olarak yapılan değişikliklerin bazıları geri alınır, ancak yüklenen NuGet paketleri gibi diğer değişiklikler geri alınmaz.</span><span class="sxs-lookup"><span data-stu-id="7640c-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="7640c-546">Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar iskeledeki öğelerde gezinirken bir HTTP 404 hatası alır.</span><span class="sxs-lookup"><span data-stu-id="7640c-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="7640c-547">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="7640c-547">Workaround:</span></span>

- <span data-ttu-id="7640c-548">MVC için bu hatayı düzeltmek için yeni bir iskele öğesi ekleyin ve MVC 5 Bağımlılıkları 'nı (Minimal veya Tam) seçin.</span><span class="sxs-lookup"><span data-stu-id="7640c-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="7640c-549">Bu işlem, projenize gerekli tüm değişiklikleri ekler.</span><span class="sxs-lookup"><span data-stu-id="7640c-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="7640c-550">Web API için bu hatayı düzeltmek için:</span><span class="sxs-lookup"><span data-stu-id="7640c-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="7640c-551">WebApiConfig sınıfını projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7640c-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="7640c-552">Global.asax'ta Uygulama\_Başlangıç yönteminde WebApiConfig.Register'ı aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7640c-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
