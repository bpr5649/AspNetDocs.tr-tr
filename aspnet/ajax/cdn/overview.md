---
uid: ajax/cdn/overview
title: Microsoft Ajax Content Delivery Network | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 9eebe0e52af2a0fca967a51afb58c7db174d9fdb
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702926"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="371e8-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="371e8-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="371e8-103">Üretim uygulamaları, CDN varlıklarına sabit bir bağımlılık alamaz.</span><span class="sxs-lookup"><span data-stu-id="371e8-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="371e8-104">Uygulamalar başvurulan CDN varlığını test etmelidir ve CDN kullanılabilir olmadığında bir geri dönüş varlığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="371e8-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="371e8-105">Microsoft Ajax CDN 'nin, bir Azure CDN kullanarak yukarıdaki ve sonraki bir SLA 'sı yoktur.</span><span class="sxs-lookup"><span data-stu-id="371e8-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="371e8-106">Microsoft Ajax CDN ile ilgili sorunları bildirmek için [Bu GitHub sorununu](https://github.com/dotnet/AspNetDocs/issues/116) kullanın.</span><span class="sxs-lookup"><span data-stu-id="371e8-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="371e8-107">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="371e8-107">Table of Contents</span></span>

<span data-ttu-id="371e8-108">**[ajax.microsoft.com, ajax.aspnetcdn.com olarak yeniden adlandırıldı](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="371e8-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="371e8-109">**[Visual Studio. vsdoc desteği](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="371e8-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="371e8-110">**[CDN 'den ASP.NET AJAX kullanma](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="371e8-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="371e8-111">**[CDN 'den jQuery kullanma](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="371e8-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="371e8-112">**[CDN 'den jQuery kullanıcı arabirimini kullanma](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="371e8-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="371e8-113">**[CDN 'deki üçüncü taraf dosyaları](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="371e8-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="371e8-114">CDN üzerinde jQuery yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="371e8-115">CDN üzerinde jQuery geçişi sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="371e8-116">CDN üzerinde jQuery kullanıcı arabirimi yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="371e8-117">CDN üzerinde jQuery doğrulama yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="371e8-118">CDN üzerinde jQuery Mobile yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="371e8-119">CDN üzerinde jQuery şablonları yayınlar</span><span class="sxs-lookup"><span data-stu-id="371e8-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="371e8-120">CDN üzerinde jQuery Cycle yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="371e8-121">CDN üzerinde jQuery DataTable yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="371e8-122">CDN 'de Modernizr yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="371e8-123">CDN 'de Jshınt yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="371e8-124">CDN 'deki sürümleri altını gizleme</span><span class="sxs-lookup"><span data-stu-id="371e8-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="371e8-125">CDN 'de globalize sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="371e8-126">CDN 'deki yanıt verme yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="371e8-127">CDN 'de önyükleme yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="371e8-128">CDN 'de önyükleme TouchCarousel sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="371e8-129"> CDN üzerinde yayınlarHammer.js</span><span class="sxs-lookup"><span data-stu-id="371e8-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="371e8-130">CDN 'de ASP.NET Web Forms ve Ajax sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="371e8-131">CDN 'de ASP.NET MVC yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="371e8-132">CDN üzerinde ASP.NET SignalR yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="371e8-133">Microsoft Ajax Content Delivery Network (CDN), jQuery gibi popüler üçüncü taraf JavaScript kitaplıklarını barındırır ve bunları Web uygulamalarınıza kolayca eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="371e8-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="371e8-134">Örneğin, &lt; &gt; sayfanıza Ajax.aspnetcdn.com işaret eden bir betik etiketi ekleyerek bu CDN üzerinde barındırılan jQuery kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="371e8-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="371e8-135">CDN 'den yararlanarak, Ajax uygulamalarınızın performansını önemli ölçüde artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="371e8-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="371e8-136">CDN içeriği dünyanın dört bir yanındaki sunucularda önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="371e8-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="371e8-137">Ayrıca, CDN, tarayıcıların farklı etki alanlarında bulunan Web siteleri için önbelleğe alınmış üçüncü taraf JavaScript dosyalarını yeniden kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="371e8-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="371e8-138">CDN, Güvenli Yuva Katmanı kullanarak bir Web sayfasına ihtiyacınız olması durumunda SSL 'yi (HTTPS) destekler.</span><span class="sxs-lookup"><span data-stu-id="371e8-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="371e8-139">CDN, karşıya yüklenen ve size lisanslanan aşağıdaki üçüncü taraf komut dosyası kitaplıklarını bu kitaplıkların sahiplerine barındırır:</span><span class="sxs-lookup"><span data-stu-id="371e8-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="371e8-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="371e8-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="371e8-141">jQuery kullanıcı arabirimi (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="371e8-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="371e8-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="371e8-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="371e8-143">jQuery doğrulaması (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="371e8-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="371e8-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="371e8-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="371e8-145">jQuery DataTable (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="371e8-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="371e8-146">Microsoft Ajax CDN, Microsoft tarafından karşıya yüklenen aşağıdaki kitaplıkları da içerir:</span><span class="sxs-lookup"><span data-stu-id="371e8-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="371e8-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="371e8-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="371e8-148">ASP.NET MVC JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="371e8-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="371e8-149">ASP.NET SignalR JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="371e8-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="371e8-150">Microsoft, bu CDN 'de barındırılan herhangi bir üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="371e8-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="371e8-151">Kitaplıkların telif hakkı sahipleri bu kitaplıkları sizin için lisanslardır.</span><span class="sxs-lookup"><span data-stu-id="371e8-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="371e8-152">Bu tür kitaplıkları indirmeniz ve kullanmanız gereken haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="371e8-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="371e8-153">Bunlar Microsoft kitaplıkları olmadığından, bu CDN 'de barındırılan üçüncü taraf kitaplıkları için Microsoft hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları dahil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="371e8-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="371e8-154">JavaScript kitaplığınızı göndermek isterseniz ve kitaplığınız en üst JavaScript kitaplıklarından biridir ( http://trends.builtwith.com) (a) popüler olan bu kitaplıkların ya da uzantılar/eklentilerden listelendiği gibi) veya (b) ASP.net üzerinde kullanım için yararlı olarak, lütfen iletişim kurun AjaxCDNSubmission@Microsoft.com .</span><span class="sxs-lookup"><span data-stu-id="371e8-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="371e8-155">ajax.microsoft.com, ajax.aspnetcdn.com olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="371e8-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="371e8-156">Microsoft.com etki alanı adını kullanmak için kullanılan CDN, aspnetcdn.com etki alanı adını kullanacak şekilde değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="371e8-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="371e8-157">Bu değişiklik performansı artırmak için yapılmıştır çünkü bir tarayıcı microsoft.com etki alanına başvurduğu zaman, her istekle birlikte bu etki alanındaki herhangi bir tanımlama bilgisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="371e8-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="371e8-158">Microsoft.com performansının dışındaki bir etki alanı adına yeniden adlandırarak, %25 ' e kadar artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="371e8-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="371e8-159">Note ajax.microsoft.com çalışmaya devam edecektir ancak ajax.aspnetcdn.com önerilir.</span><span class="sxs-lookup"><span data-stu-id="371e8-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="371e8-160">Eski biçim: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="371e8-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="371e8-161">Yeni biçim: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="371e8-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="371e8-162">Visual Studio. vsdoc desteği</span><span class="sxs-lookup"><span data-stu-id="371e8-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="371e8-163">. Vsdoc dosyalarını Visual Studio 2008 ile düzgün şekilde kullanmak için, VS 2008 SP1 'in yüklü olduğundan ve vsdoc dosyalarının düzeltmesinin yüklü olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="371e8-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="371e8-164">Bunları buradan öğrenebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="371e8-164">You can get these from here:</span></span>

- [<span data-ttu-id="371e8-165">Visual Studio 2008 SP1 'i indirin</span><span class="sxs-lookup"><span data-stu-id="371e8-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 SP1 'i indirin")
- [<span data-ttu-id="371e8-166">Visual Studio 2008 SP1 için. vsdoc düzeltmesini indirin</span><span class="sxs-lookup"><span data-stu-id="371e8-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 SP1 için. vsdoc düzeltmesini indirin")

<span data-ttu-id="371e8-167">Visual Studio 2010, ek düzeltme ekleri olmadan. vsdoc dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="371e8-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="371e8-168">CDN 'den ASP.NET AJAX kullanma</span><span class="sxs-lookup"><span data-stu-id="371e8-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="371e8-169">ASP.NET 4 kullanırken, tüm ASP.NET Framework betikleri isteklerini CDN 'ye yeniden yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="371e8-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="371e8-170">Yerel Web sunucunuz yerine CDN 'den betikler alma, genel ASP.NET Web sitelerinin performansını önemli ölçüde iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="371e8-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="371e8-171">Tüm ASP.NET Framework betik isteklerini Microsoft Ajax CDN 'ye yönlendirmek için ScriptManager EnableCDN özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="371e8-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="371e8-172">CDN 'den jQuery kullanma</span><span class="sxs-lookup"><span data-stu-id="371e8-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="371e8-173">Aşağıdaki betik öğesini bir sayfaya ekleyerek, Web uygulamanızda CDN üzerinde barındırılan jQuery betiklerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="371e8-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="371e8-174">CDN, jQuery betiğinin mini kullanılan sürümünü de içerir ve bu, aşağıdaki öğeyi kullanarak edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="371e8-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="371e8-175">Sayfanızın, CDN 'nin kullanılamaz olması durumunda kendi web sitenizde yerel bir yoldan jQuery yüklemeye geri dönüşü sağlamak için, CDN 'e başvuran öğeden hemen sonra aşağıdaki öğeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="371e8-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="371e8-176">Aşağıdaki örnek sayfa, bir düğmeye tıklandığında bir div öğesinin içeriğini göstermek için jQuery kitaplığının CDN sürümünü (yerel bir kopyaya geri dönüş ile) kullanır.</span><span class="sxs-lookup"><span data-stu-id="371e8-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="371e8-177">JQuery hakkında daha fazla bilgi alabilir ve [jQuery Web sitesini](http://jquery.com/) ziyaret ederek jQuery 'in yerel bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="371e8-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="371e8-178">CDN 'den jQuery kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="371e8-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="371e8-179">CDN, jQuery kullanıcı arabirimi kitaplığını da barındırır.</span><span class="sxs-lookup"><span data-stu-id="371e8-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="371e8-180">JQuery kullanıcı arabirimi kitaplığı, ASP.NET uygulamalarınızda kullanabileceğiniz zengin bir pencere öğesi ve efekt kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="371e8-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="371e8-181">Örneğin, aşağıdaki sayfada bir ASP.NET Web Forms uygulaması bağlamında bir açılır takvimi göstermek için jQuery UI DatePicker nasıl kullanabileceğiniz gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="371e8-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="371e8-182">Klavyenizi kullanarak metin kutusuna odağı taşıdığınızda bir takvim görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="371e8-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![DatePicker ile oluşturulan açılan takvim](overview/_static/image1.png)

<span data-ttu-id="371e8-184">Yukarıdaki kodda CDN 'den üç dosya eklemeniz gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="371e8-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="371e8-185">JQuery kitaplığı jQuery &mdash; Kullanıcı arabirimi kitaplığı jQuery kitaplığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="371e8-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="371e8-186">JQuery kullanıcı arabirimi kitaplığını eklemeden önce jQuery kitaplığını sayfanıza eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="371e8-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="371e8-187">JQuery kullanıcı arabirimi kitaplığı jQuery kullanıcı arabirimi, &mdash; Yukarıdaki sayfada kullanılan tüm jQuery kullanıcı arabirimi efektlerini ve DatePicker pencere öğesi gibi pencere öğelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="371e8-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="371e8-188">JQuery kullanıcı arabirimi teması &mdash; , jQuery kullanıcı arabirimi farklı temaları destekler.</span><span class="sxs-lookup"><span data-stu-id="371e8-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="371e8-189">Yukarıdaki sayfa, Redmond temasını içeri aktarmak için CSS dosyasının bir bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="371e8-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="371e8-190">Tüm standart jQuery UI temaları CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="371e8-191">Her temanın küçük resimlerini görüntülemek için [Bu sayfayı ziyaret edin](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10") .</span><span class="sxs-lookup"><span data-stu-id="371e8-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="371e8-192">JQuery kullanıcı arabirimi kitaplığı hakkında daha fazla bilgi edinmek için resmi [jQuery kullanıcı arabirimi Web sitesini](http://jQueryUI.com "jQuery kullanıcı arabirimi Web sitesi")ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="371e8-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="371e8-193">CDN 'deki üçüncü taraf dosyaları</span><span class="sxs-lookup"><span data-stu-id="371e8-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="371e8-194">CDN, en popüler üçüncü taraf JavaScript kitaplıklarından bazılarını barındırır.</span><span class="sxs-lookup"><span data-stu-id="371e8-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="371e8-195">Microsoft, bu CDN 'de barındırılan herhangi bir üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="371e8-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="371e8-196">Kitaplıkların telif hakkı sahipleri bu kitaplıkları sizin için lisanslardır.</span><span class="sxs-lookup"><span data-stu-id="371e8-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="371e8-197">Bu tür kitaplıkları indirmeniz ve kullanmanız gereken haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="371e8-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="371e8-198">Bunlar Microsoft kitaplıkları olmadığından, bu CDN 'de barındırılan üçüncü taraf kitaplıkları için Microsoft hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları dahil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="371e8-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="371e8-199">CDN üzerinde jQuery yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="371e8-200">JQuery 'in aşağıdaki sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-351"></a><span data-ttu-id="371e8-201">jQuery sürüm 3.5.1</span><span class="sxs-lookup"><span data-stu-id="371e8-201">jQuery version 3.5.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.map

#### <a name="jquery-version-350"></a><span data-ttu-id="371e8-202">jQuery sürümü 3.5.0</span><span class="sxs-lookup"><span data-stu-id="371e8-202">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="371e8-203">jQuery sürümü 3.4.1</span><span class="sxs-lookup"><span data-stu-id="371e8-203">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="371e8-204">jQuery sürümü 3.4.0</span><span class="sxs-lookup"><span data-stu-id="371e8-204">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="371e8-205">jQuery sürümü 3.3.1</span><span class="sxs-lookup"><span data-stu-id="371e8-205">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="371e8-206">jQuery sürümü 3.2.1</span><span class="sxs-lookup"><span data-stu-id="371e8-206">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="371e8-207">jQuery sürümü 3.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-207">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="371e8-208">jQuery sürümü 3.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-208">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="371e8-209">jQuery sürümü 3.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-209">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="371e8-210">jQuery sürümü 3.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-210">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="371e8-211">jQuery sürümü 2.2.4</span><span class="sxs-lookup"><span data-stu-id="371e8-211">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="371e8-212">jQuery sürümü 2.2.3</span><span class="sxs-lookup"><span data-stu-id="371e8-212">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="371e8-213">jQuery sürümü 2.2.2</span><span class="sxs-lookup"><span data-stu-id="371e8-213">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="371e8-214">jQuery sürümü 2.2.1</span><span class="sxs-lookup"><span data-stu-id="371e8-214">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="371e8-215">jQuery sürümü 2.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-215">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="371e8-216">jQuery sürümü 2.1.4</span><span class="sxs-lookup"><span data-stu-id="371e8-216">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="371e8-217">jQuery sürümü 2.1.3</span><span class="sxs-lookup"><span data-stu-id="371e8-217">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="371e8-218">jQuery sürümü 2.1.2 'yi</span><span class="sxs-lookup"><span data-stu-id="371e8-218">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="371e8-219">jQuery sürümü 2.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-219">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="371e8-220">jQuery sürümü 2.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-220">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="371e8-221">jQuery sürümü 2.0.3</span><span class="sxs-lookup"><span data-stu-id="371e8-221">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="371e8-222">jQuery sürümü 2.0.2</span><span class="sxs-lookup"><span data-stu-id="371e8-222">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="371e8-223">jQuery sürüm 2.0.1</span><span class="sxs-lookup"><span data-stu-id="371e8-223">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="371e8-224">jQuery sürümü 2.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-224">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="371e8-225">jQuery sürümü 1.12.4</span><span class="sxs-lookup"><span data-stu-id="371e8-225">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="371e8-226">jQuery sürümü 1.12.3</span><span class="sxs-lookup"><span data-stu-id="371e8-226">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="371e8-227">jQuery sürümü 1.12.2</span><span class="sxs-lookup"><span data-stu-id="371e8-227">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="371e8-228">jQuery sürümü 1.12.1</span><span class="sxs-lookup"><span data-stu-id="371e8-228">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="371e8-229">jQuery sürümü 1.12.0</span><span class="sxs-lookup"><span data-stu-id="371e8-229">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="371e8-230">jQuery sürümü 1.11.3</span><span class="sxs-lookup"><span data-stu-id="371e8-230">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="371e8-231">jQuery sürümü 1.11.2</span><span class="sxs-lookup"><span data-stu-id="371e8-231">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="371e8-232">jQuery sürümü 1.11.1</span><span class="sxs-lookup"><span data-stu-id="371e8-232">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="371e8-233">jQuery sürümü 1.11.0</span><span class="sxs-lookup"><span data-stu-id="371e8-233">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="371e8-234">jQuery sürümü 1.10.2</span><span class="sxs-lookup"><span data-stu-id="371e8-234">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="371e8-235">jQuery sürümü 1.10.1</span><span class="sxs-lookup"><span data-stu-id="371e8-235">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="371e8-236">jQuery sürümü 1.10.0</span><span class="sxs-lookup"><span data-stu-id="371e8-236">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="371e8-237">jQuery sürümü 1.9.1</span><span class="sxs-lookup"><span data-stu-id="371e8-237">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="371e8-238">jQuery sürümü 1.9.0</span><span class="sxs-lookup"><span data-stu-id="371e8-238">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="371e8-239">jQuery sürümü 1.8.3 birden fazla</span><span class="sxs-lookup"><span data-stu-id="371e8-239">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="371e8-240">jQuery sürümü 1.8.2</span><span class="sxs-lookup"><span data-stu-id="371e8-240">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="371e8-241">jQuery sürümü 1.8.1</span><span class="sxs-lookup"><span data-stu-id="371e8-241">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="371e8-242">jQuery sürümü 1.8.0</span><span class="sxs-lookup"><span data-stu-id="371e8-242">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="371e8-243">jQuery sürümü 1.7.2</span><span class="sxs-lookup"><span data-stu-id="371e8-243">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="371e8-244">jQuery sürümü 1.7.1</span><span class="sxs-lookup"><span data-stu-id="371e8-244">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="371e8-245">jQuery sürüm 1,7</span><span class="sxs-lookup"><span data-stu-id="371e8-245">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="371e8-246">jQuery sürümü 1.6.4</span><span class="sxs-lookup"><span data-stu-id="371e8-246">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="371e8-247">jQuery sürümü 1.6.3</span><span class="sxs-lookup"><span data-stu-id="371e8-247">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="371e8-248">jQuery sürümü 1.6.2</span><span class="sxs-lookup"><span data-stu-id="371e8-248">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="371e8-249">jQuery sürümü 1.6.1</span><span class="sxs-lookup"><span data-stu-id="371e8-249">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="371e8-250">jQuery sürüm 1,6</span><span class="sxs-lookup"><span data-stu-id="371e8-250">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="371e8-251">jQuery sürümü 1.5.2 planlama</span><span class="sxs-lookup"><span data-stu-id="371e8-251">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="371e8-252">jQuery sürümü 1.5.1</span><span class="sxs-lookup"><span data-stu-id="371e8-252">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="371e8-253">jQuery sürüm 1,5</span><span class="sxs-lookup"><span data-stu-id="371e8-253">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="371e8-254">jQuery sürümü 1.4.4</span><span class="sxs-lookup"><span data-stu-id="371e8-254">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="371e8-255">jQuery sürümü 1.4.3</span><span class="sxs-lookup"><span data-stu-id="371e8-255">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="371e8-256">jQuery sürümü 1.4.2</span><span class="sxs-lookup"><span data-stu-id="371e8-256">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="371e8-257">jQuery sürümü 1.4.1</span><span class="sxs-lookup"><span data-stu-id="371e8-257">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="371e8-258">jQuery sürüm 1,4</span><span class="sxs-lookup"><span data-stu-id="371e8-258">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="371e8-259">jQuery sürümü 1.3.2</span><span class="sxs-lookup"><span data-stu-id="371e8-259">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="371e8-260">CDN üzerinde jQuery geçişi sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-260">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="371e8-261">JQuery geçişi 'nin aşağıdaki sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-261">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="371e8-262">jQuery geçişi sürüm 3.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-262">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="371e8-263">jQuery geçişi sürüm 1.2.1</span><span class="sxs-lookup"><span data-stu-id="371e8-263">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="371e8-264">jQuery geçişi sürüm 1.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-264">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="371e8-265">jQuery geçişi sürüm 1.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-265">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="371e8-266">jQuery geçişi sürüm 1.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-266">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="371e8-267">jQuery geçişi sürüm 1.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-267">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="371e8-268">CDN üzerinde jQuery kullanıcı arabirimi yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-268">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="371e8-269">JQuery kullanıcı arabirimi kitaplığı 'nın aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-269">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="371e8-270">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-270">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-271">jQuery kullanıcı arabirimi 1.12.1</span><span class="sxs-lookup"><span data-stu-id="371e8-271">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.1")
- [<span data-ttu-id="371e8-272">jQuery kullanıcı arabirimi 1.12.0</span><span class="sxs-lookup"><span data-stu-id="371e8-272">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.0")
- [<span data-ttu-id="371e8-273">jQuery kullanıcı arabirimi 1.11.4</span><span class="sxs-lookup"><span data-stu-id="371e8-273">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.4")
- [<span data-ttu-id="371e8-274">jQuery kullanıcı arabirimi 1.11.3</span><span class="sxs-lookup"><span data-stu-id="371e8-274">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.3")
- [<span data-ttu-id="371e8-275">jQuery kullanıcı arabirimi 1.11.2</span><span class="sxs-lookup"><span data-stu-id="371e8-275">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.2")
- [<span data-ttu-id="371e8-276">jQuery kullanıcı arabirimi 1.11.1</span><span class="sxs-lookup"><span data-stu-id="371e8-276">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.1")
- [<span data-ttu-id="371e8-277">jQuery kullanıcı arabirimi 1.11.0</span><span class="sxs-lookup"><span data-stu-id="371e8-277">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.0")
- [<span data-ttu-id="371e8-278">jQuery kullanıcı arabirimi 1.10.4</span><span class="sxs-lookup"><span data-stu-id="371e8-278">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.4")
- [<span data-ttu-id="371e8-279">jQuery kullanıcı arabirimi 1.10.3</span><span class="sxs-lookup"><span data-stu-id="371e8-279">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.3")
- [<span data-ttu-id="371e8-280">jQuery kullanıcı arabirimi 1.10.2</span><span class="sxs-lookup"><span data-stu-id="371e8-280">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.2")
- [<span data-ttu-id="371e8-281">jQuery kullanıcı arabirimi 1.10.1</span><span class="sxs-lookup"><span data-stu-id="371e8-281">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.1")
- [<span data-ttu-id="371e8-282">jQuery kullanıcı arabirimi 1.10.0</span><span class="sxs-lookup"><span data-stu-id="371e8-282">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.0")
- [<span data-ttu-id="371e8-283">jQuery kullanıcı arabirimi 1.9.2</span><span class="sxs-lookup"><span data-stu-id="371e8-283">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.2")
- [<span data-ttu-id="371e8-284">jQuery kullanıcı arabirimi 1.9.1</span><span class="sxs-lookup"><span data-stu-id="371e8-284">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.1")
- [<span data-ttu-id="371e8-285">jQuery kullanıcı arabirimi 1.9.0</span><span class="sxs-lookup"><span data-stu-id="371e8-285">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.0")
- [<span data-ttu-id="371e8-286">jQuery kullanıcı arabirimi 1.8.24</span><span class="sxs-lookup"><span data-stu-id="371e8-286">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.24")
- [<span data-ttu-id="371e8-287">jQuery kullanıcı arabirimi 1.8.23</span><span class="sxs-lookup"><span data-stu-id="371e8-287">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.23")
- [<span data-ttu-id="371e8-288">jQuery kullanıcı arabirimi 1.8.22</span><span class="sxs-lookup"><span data-stu-id="371e8-288">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.22")
- [<span data-ttu-id="371e8-289">jQuery kullanıcı arabirimi 1.8.21</span><span class="sxs-lookup"><span data-stu-id="371e8-289">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.21")
- [<span data-ttu-id="371e8-290">jQuery kullanıcı arabirimi 1.8.20</span><span class="sxs-lookup"><span data-stu-id="371e8-290">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.20")
- [<span data-ttu-id="371e8-291">jQuery kullanıcı arabirimi 1.8.19</span><span class="sxs-lookup"><span data-stu-id="371e8-291">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.19")
- [<span data-ttu-id="371e8-292">jQuery kullanıcı arabirimi 1.8.18</span><span class="sxs-lookup"><span data-stu-id="371e8-292">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.18")
- [<span data-ttu-id="371e8-293">jQuery kullanıcı arabirimi 1.8.17</span><span class="sxs-lookup"><span data-stu-id="371e8-293">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.17")
- [<span data-ttu-id="371e8-294">jQuery kullanıcı arabirimi 1.8.16</span><span class="sxs-lookup"><span data-stu-id="371e8-294">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.16")
- [<span data-ttu-id="371e8-295">jQuery kullanıcı arabirimi 1.8.15</span><span class="sxs-lookup"><span data-stu-id="371e8-295">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.15")
- [<span data-ttu-id="371e8-296">jQuery kullanıcı arabirimi 1.8.14</span><span class="sxs-lookup"><span data-stu-id="371e8-296">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.14")
- [<span data-ttu-id="371e8-297">jQuery kullanıcı arabirimi 1.8.13</span><span class="sxs-lookup"><span data-stu-id="371e8-297">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.13")
- [<span data-ttu-id="371e8-298">jQuery kullanıcı arabirimi 1.8.12</span><span class="sxs-lookup"><span data-stu-id="371e8-298">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.12")
- [<span data-ttu-id="371e8-299">jQuery kullanıcı arabirimi 1.8.11</span><span class="sxs-lookup"><span data-stu-id="371e8-299">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.11")
- [<span data-ttu-id="371e8-300">jQuery kullanıcı arabirimi 1.8.10</span><span class="sxs-lookup"><span data-stu-id="371e8-300">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10")
- [<span data-ttu-id="371e8-301">jQuery kullanıcı arabirimi 1.8.9</span><span class="sxs-lookup"><span data-stu-id="371e8-301">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.9")
- [<span data-ttu-id="371e8-302">jQuery kullanıcı arabirimi 1.8.8</span><span class="sxs-lookup"><span data-stu-id="371e8-302">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.8")
- [<span data-ttu-id="371e8-303">jQuery kullanıcı arabirimi 1.8.7</span><span class="sxs-lookup"><span data-stu-id="371e8-303">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.7")
- [<span data-ttu-id="371e8-304">jQuery kullanıcı arabirimi 1.8.6</span><span class="sxs-lookup"><span data-stu-id="371e8-304">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.6")
- [<span data-ttu-id="371e8-305">jQuery Kullanıcı Arabirimi 1.8.5</span><span class="sxs-lookup"><span data-stu-id="371e8-305">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery Kullanıcı Arabirimi 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="371e8-306">CDN üzerinde jQuery doğrulama yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-306">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="371e8-307">[JQuery doğrulama](https://jqueryvalidation.org/ "jQuery doğrulama eklentisi") eklentisinin aşağıdaki SÜRÜMLERI bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-307">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="371e8-308">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-308">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-309">jQuery Validate 1.19.2</span><span class="sxs-lookup"><span data-stu-id="371e8-309">jQuery Validate 1.19.2</span></span>](jquery-validate/cdnjqueryvalidate1192.md "jQuery doğrulama 1.19.2")
- [<span data-ttu-id="371e8-310">jQuery Validate 1.19.1</span><span class="sxs-lookup"><span data-stu-id="371e8-310">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery doğrulama 1.19.1")
- [<span data-ttu-id="371e8-311">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="371e8-311">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery doğrulama 1.19.0")
- [<span data-ttu-id="371e8-312">jQuery Validate 1.17.0</span><span class="sxs-lookup"><span data-stu-id="371e8-312">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery doğrulama 1.17.0")
- [<span data-ttu-id="371e8-313">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="371e8-313">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Doğrulaması 1.16.0")
- [<span data-ttu-id="371e8-314">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="371e8-314">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Doğrulaması 1.15.1")
- [<span data-ttu-id="371e8-315">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="371e8-315">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Doğrulaması 1.15.0")
- [<span data-ttu-id="371e8-316">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="371e8-316">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Doğrulaması 1.14.0")
- [<span data-ttu-id="371e8-317">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="371e8-317">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Doğrulaması 1.13.1")
- [<span data-ttu-id="371e8-318">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="371e8-318">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Doğrulaması 1.13.0")
- [<span data-ttu-id="371e8-319">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="371e8-319">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Doğrulaması 1.12.0")
- [<span data-ttu-id="371e8-320">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="371e8-320">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Doğrulaması 1.11.1")
- [<span data-ttu-id="371e8-321">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="371e8-321">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Doğrulaması 1.11.0")
- [<span data-ttu-id="371e8-322">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="371e8-322">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Doğrulaması 1.10.0")
- [<span data-ttu-id="371e8-323">jQuery doğrulaması 1,9</span><span class="sxs-lookup"><span data-stu-id="371e8-323">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate sürümü 1.9")
- [<span data-ttu-id="371e8-324">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="371e8-324">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate sürümü 1.8.1")
- [<span data-ttu-id="371e8-325">jQuery doğrulaması 1,8</span><span class="sxs-lookup"><span data-stu-id="371e8-325">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate sürümü 1.8")
- [<span data-ttu-id="371e8-326">jQuery doğrulaması 1,7</span><span class="sxs-lookup"><span data-stu-id="371e8-326">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate sürümü 1.7")
- [<span data-ttu-id="371e8-327">jQuery Doğrulama 1.6</span><span class="sxs-lookup"><span data-stu-id="371e8-327">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Doğrulama 1.6")
- [<span data-ttu-id="371e8-328">jQuery Doğrulama 1.5.5</span><span class="sxs-lookup"><span data-stu-id="371e8-328">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Doğrulama 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="371e8-329">CDN üzerinde jQuery Mobile yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-329">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="371e8-330">JQuery mobile Library 'in aşağıdaki sürümleri bu CDN 'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-330">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="371e8-331">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-331">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-332">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="371e8-332">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.5")
- [<span data-ttu-id="371e8-333">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="371e8-333">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.2")
- [<span data-ttu-id="371e8-334">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="371e8-334">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.1")
- [<span data-ttu-id="371e8-335">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="371e8-335">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.0")
- [<span data-ttu-id="371e8-336">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="371e8-336">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.2")
- [<span data-ttu-id="371e8-337">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="371e8-337">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.1")
- [<span data-ttu-id="371e8-338">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="371e8-338">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.0")
- [<span data-ttu-id="371e8-339">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-339">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.2.0")
- [<span data-ttu-id="371e8-340">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="371e8-340">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.2")
- [<span data-ttu-id="371e8-341">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-341">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.1")
- [<span data-ttu-id="371e8-342">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-342">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0")
- [<span data-ttu-id="371e8-343">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="371e8-343">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="371e8-344">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="371e8-344">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0.1")
- [<span data-ttu-id="371e8-345">jQuery Mobile 1,0</span><span class="sxs-lookup"><span data-stu-id="371e8-345">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0")
- [<span data-ttu-id="371e8-346">jQuery Mobile 1,0 RC 2</span><span class="sxs-lookup"><span data-stu-id="371e8-346">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="371e8-347">jQuery Mobile 1,0 RC 1</span><span class="sxs-lookup"><span data-stu-id="371e8-347">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="371e8-348">jQuery Mobile 1,0 Beta 3</span><span class="sxs-lookup"><span data-stu-id="371e8-348">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="371e8-349">CDN üzerinde jQuery şablonları yayınlar</span><span class="sxs-lookup"><span data-stu-id="371e8-349">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="371e8-350">JQuery şablonları eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-350">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="371e8-351">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-351">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-352">jQuery Şablonları Beta 1</span><span class="sxs-lookup"><span data-stu-id="371e8-352">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Şablonları Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="371e8-353">CDN üzerinde jQuery Cycle yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-353">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="371e8-354">JQuery Cycle eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-354">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="371e8-355">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-355">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-356">jQuery Döngüsü 2.99</span><span class="sxs-lookup"><span data-stu-id="371e8-356">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Döngüsü 2.99")
- [<span data-ttu-id="371e8-357">jQuery Döngüsü 2.94</span><span class="sxs-lookup"><span data-stu-id="371e8-357">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Döngüsü 2.94")
- [<span data-ttu-id="371e8-358">jQuery Döngüsü 2.88</span><span class="sxs-lookup"><span data-stu-id="371e8-358">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Döngüsü 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="371e8-359">CDN üzerinde jQuery DataTable yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-359">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="371e8-360">JQuery DataTable eklentisinin aşağıdaki sürümleri bu CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-360">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="371e8-361">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-361">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-362">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="371e8-362">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="371e8-363">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="371e8-363">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="371e8-364">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="371e8-364">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="371e8-365">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="371e8-365">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="371e8-366">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="371e8-366">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="371e8-367">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="371e8-367">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="371e8-368">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="371e8-368">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="371e8-369">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="371e8-369">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="371e8-370">CDN 'de Modernizr yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-370">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="371e8-371">Aşağıdaki [Modernizr](http://www.modernizr.com "Modernize") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-371">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="371e8-372">CDN 'de Jshınt yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-372">JSHint Releases on the CDN</span></span>

<span data-ttu-id="371e8-373">Aşağıdaki [Jshınt](http://www.jshint.com "JSHint") sürümleri CDN 'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-373">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="371e8-374">CDN 'deki sürümleri altını gizleme</span><span class="sxs-lookup"><span data-stu-id="371e8-374">Knockout Releases on the CDN</span></span>

<span data-ttu-id="371e8-375">Aşağıdaki [altını gizleme](http://www.knockoutjs.com "Renkleri") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-375">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="371e8-376">CDN 'de globalize sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-376">Globalize Releases on the CDN</span></span>

<span data-ttu-id="371e8-377">Aşağıdaki [globalize](https://github.com/jquery/globalize "Globalize") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-377">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="371e8-378">Globalize sürümü 1.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-378">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="371e8-379">Globalize sürümü 0.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-379">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="371e8-380">tüm kültürler</span><span class="sxs-lookup"><span data-stu-id="371e8-380">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="371e8-381">"{Culture-Code}" öğesini istenen kültür koduyla değiştirin; globalize.culture.en-GB.jsÖrneğin, CDN = = Microsoft dosyaları, Microsoft tarafından karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="371e8-381">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="371e8-382">CDN 'deki yanıt verme yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-382">Respond Releases on the CDN</span></span>

<span data-ttu-id="371e8-383">Aşağıdaki [yanıt verme](https://github.com/scottjehl/Respond "Yanıtlama") sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-383">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="371e8-384">Yanıt 1.4.2 sürümü</span><span class="sxs-lookup"><span data-stu-id="371e8-384">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="371e8-385">Yanıt 1.4.1 sürümü</span><span class="sxs-lookup"><span data-stu-id="371e8-385">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="371e8-386">Yanıt 1.4.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="371e8-386">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="371e8-387">Yanıt 1.3.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="371e8-387">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="371e8-388">Yanıt 1.2.0 sürümü</span><span class="sxs-lookup"><span data-stu-id="371e8-388">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="371e8-389">CDN 'de önyükleme yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-389">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="371e8-390">Aşağıdaki [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") Bootstrap sürümleri CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-390">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-452"></a><span data-ttu-id="371e8-391">Önyükleme sürümü 4.5.2</span><span class="sxs-lookup"><span data-stu-id="371e8-391">Bootstrap version 4.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-450"></a><span data-ttu-id="371e8-392">Önyükleme sürümü 4.5.0</span><span class="sxs-lookup"><span data-stu-id="371e8-392">Bootstrap version 4.5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-441"></a><span data-ttu-id="371e8-393">Önyükleme sürümü 4.4.1</span><span class="sxs-lookup"><span data-stu-id="371e8-393">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="371e8-394">Önyükleme sürümü 4.3.1</span><span class="sxs-lookup"><span data-stu-id="371e8-394">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="371e8-395">Önyükleme sürümü 4.2.1</span><span class="sxs-lookup"><span data-stu-id="371e8-395">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="371e8-396">Önyükleme sürümü 4.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-396">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="371e8-397">Önyükleme sürümü 4.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-397">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="371e8-398">Önyükleme sürümü 3.4.1</span><span class="sxs-lookup"><span data-stu-id="371e8-398">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="371e8-399">Önyükleme sürümü 3.4.0</span><span class="sxs-lookup"><span data-stu-id="371e8-399">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="371e8-400">Önyükleme sürümü 3.3.7</span><span class="sxs-lookup"><span data-stu-id="371e8-400">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="371e8-401">Önyükleme sürümü 3.3.6</span><span class="sxs-lookup"><span data-stu-id="371e8-401">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="371e8-402">Önyükleme sürümü 3.3.5</span><span class="sxs-lookup"><span data-stu-id="371e8-402">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="371e8-403">Önyükleme sürümü 3.3.4</span><span class="sxs-lookup"><span data-stu-id="371e8-403">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="371e8-404">Önyükleme sürümü 3.3.2</span><span class="sxs-lookup"><span data-stu-id="371e8-404">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="371e8-405">Önyükleme sürümü 3.3.1</span><span class="sxs-lookup"><span data-stu-id="371e8-405">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="371e8-406">Önyükleme sürümü 3.3.0</span><span class="sxs-lookup"><span data-stu-id="371e8-406">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="371e8-407">Önyükleme sürümü 3.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-407">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="371e8-408">Önyükleme sürümü 3.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-408">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="371e8-409">Önyükleme sürümü 3.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-409">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="371e8-410">Önyükleme sürümü 3.0.3</span><span class="sxs-lookup"><span data-stu-id="371e8-410">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="371e8-411">Önyükleme sürümü 3.0.2</span><span class="sxs-lookup"><span data-stu-id="371e8-411">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="371e8-412">Önyükleme sürümü 3.0.1</span><span class="sxs-lookup"><span data-stu-id="371e8-412">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="371e8-413">Önyükleme sürümü 3.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-413">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="371e8-414">Önyükleme sürümü 2.3.2</span><span class="sxs-lookup"><span data-stu-id="371e8-414">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="371e8-415">Önyükleme sürümü 2.3.1</span><span class="sxs-lookup"><span data-stu-id="371e8-415">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="371e8-416">CDN 'de önyükleme TouchCarousel sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-416">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="371e8-417">Aşağıdaki [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") önyükleme TouchCarousel sürümleri SÜRÜMLERI CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-417">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="371e8-418">Bootstrap TouchCarousel sürümü 0.8.0</span><span class="sxs-lookup"><span data-stu-id="371e8-418">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="371e8-419">CDN üzerinde yayınlar Hammer.js</span><span class="sxs-lookup"><span data-stu-id="371e8-419">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="371e8-420">Hammer.js sürümlerinin aşağıdaki sürümleri [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-420">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="371e8-421">Hammer.js Version 2.0.4</span><span class="sxs-lookup"><span data-stu-id="371e8-421">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="371e8-422">CDN 'de ASP.NET Web Forms ve Ajax sürümleri</span><span class="sxs-lookup"><span data-stu-id="371e8-422">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="371e8-423">ASP.NET Ajax Kitaplığı 'nın aşağıdaki sürümleri CDN üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="371e8-423">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="371e8-424">Dosyaların gerçek listesini görmek için her bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="371e8-424">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="371e8-425">ASP.NET Web Forms ve Ajax sürümü 4.5.2</span><span class="sxs-lookup"><span data-stu-id="371e8-425">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms ve Ajax 4.5.2")
- [<span data-ttu-id="371e8-426">ASP.NET Web Forms ve Ajax sürüm 4</span><span class="sxs-lookup"><span data-stu-id="371e8-426">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms ve Ajax 4")
- [<span data-ttu-id="371e8-427">ASP.NET AJAX sürüm 3,5</span><span class="sxs-lookup"><span data-stu-id="371e8-427">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="371e8-428">CDN 'de ASP.NET MVC yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-428">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="371e8-429">Aşağıdaki ASP.NET MVC JavaScript dosyaları bu CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-429">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="371e8-430">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="371e8-430">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="371e8-431">ASP.NET MVC 5,1</span><span class="sxs-lookup"><span data-stu-id="371e8-431">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="371e8-432">ASP.NET MVC 5,0</span><span class="sxs-lookup"><span data-stu-id="371e8-432">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="371e8-433">ASP.NET MVC 4,0</span><span class="sxs-lookup"><span data-stu-id="371e8-433">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="371e8-434">ASP.NET MVC 3,0</span><span class="sxs-lookup"><span data-stu-id="371e8-434">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="371e8-435">ASP.NET MVC 2,0</span><span class="sxs-lookup"><span data-stu-id="371e8-435">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="371e8-436">ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="371e8-436">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="371e8-437">CDN üzerinde ASP.NET SignalR yayınları</span><span class="sxs-lookup"><span data-stu-id="371e8-437">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="371e8-438">Aşağıdaki ASP.NET SignalR JavaScript dosyaları bu CDN üzerinde barındırılır:</span><span class="sxs-lookup"><span data-stu-id="371e8-438">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="371e8-439">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="371e8-439">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="371e8-440">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="371e8-440">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="371e8-441">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="371e8-441">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="371e8-442">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-442">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="371e8-443">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="371e8-443">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="371e8-444">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="371e8-444">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="371e8-445">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="371e8-445">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="371e8-446">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="371e8-446">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="371e8-447">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="371e8-447">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="371e8-448">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="371e8-448">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="371e8-449">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="371e8-449">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="371e8-450">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="371e8-450">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="371e8-451">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="371e8-451">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="371e8-452">CDN için kullanım koşulları hakkında daha fazla bilgi için bkz. [Microsoft Ajax CDN kullanım koşulları](https://www.asp.net/terms-of-use "Microsoft Ajax CDN kullanım koşulları").</span><span class="sxs-lookup"><span data-stu-id="371e8-452">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
