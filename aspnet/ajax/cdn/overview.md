---
uid: ajax/cdn/overview
title: Microsoft Ajax İçerik Dağıtım Ağı | Microsoft Dokümanlar
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540213"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="b3516-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="b3516-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="b3516-103">Üretim uygulamaları CDN varlıklarına sıkı bir bağımlılık almamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3516-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="b3516-104">Uygulamalar başvurulan CDN varlığı için test etmeli ve CDN kullanılamadığında bir geri dönüş varlığı kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3516-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="b3516-105">Microsoft Ajax CDN'de Azure CDN kullanmanın üzerinde ve ötesinde SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="b3516-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="b3516-106">Microsoft Ajax CDN ile ilgili sorunları bildirmek için [bu GitHub sorununu](https://github.com/dotnet/AspNetDocs/issues/116) kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3516-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="b3516-107">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="b3516-107">Table of Contents</span></span>

<span data-ttu-id="b3516-108">**[ajax.microsoft.com ajax.aspnetcdn.com olarak değiştirildi](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="b3516-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="b3516-109">**[Visual Studio .vsdoc Desteği](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="b3516-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="b3516-110">**[CDN'den ASP.NET Ajax'ı kullanma](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="b3516-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="b3516-111">**[CDN'den jQuery kullanma](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="b3516-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="b3516-112">**[CDN'den jQuery UI kullanma](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="b3516-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="b3516-113">**[CDN'deki Üçüncü Taraf Dosyaları](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="b3516-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="b3516-114">cdn üzerinde jQuery Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="b3516-115">jQuery CDN'de Serbest Geçiş</span><span class="sxs-lookup"><span data-stu-id="b3516-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="b3516-116">jQuery UI CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="b3516-117">cdn üzerinde jQuery Doğrulama Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="b3516-118">CDN üzerinde jQuery Mobil Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="b3516-119">jQuery Şablonlar CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="b3516-120">cdn üzerinde jQuery Döngüsü Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="b3516-121">jQuery DataTables CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="b3516-122">CDN'de Modernizr Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="b3516-123">CDN'de JSHint Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="b3516-124">CDN'de Nakavt Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="b3516-125">CDN'de Yayınları Küreselleştir</span><span class="sxs-lookup"><span data-stu-id="b3516-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="b3516-126">CDN'deki Yanıt Ları</span><span class="sxs-lookup"><span data-stu-id="b3516-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="b3516-127">CDN'de Bootstrap Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="b3516-128">Bootstrap TouchCarousel CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="b3516-129">CDN üzerinde Hammer.js Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="b3516-130">ASP.NET Web Formları ve Ajax Bültenleri CDN üzerinde</span><span class="sxs-lookup"><span data-stu-id="b3516-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="b3516-131">CDN'de ASP.NET MVC Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="b3516-132">CDN'de ASP.NET SignalR Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="b3516-133">Microsoft Ajax İçerik Dağıtım Ağı (CDN), jQuery gibi popüler üçüncü taraf JavaScript kitaplıklarını barındırAr ve bunları Web uygulamalarınıza kolayca eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b3516-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="b3516-134">Örneğin, sayfanıza yalnızca ajax.aspnetcdn.com işaret eden bir &lt;komut dosyası&gt; etiketi ekleyerek bu CDN'de barındırılan jQuery'yi kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3516-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="b3516-135">CDN'den yararlanarak Ajax uygulamalarınızın performansını önemli ölçüde artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3516-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="b3516-136">CDN'nin içeriği, dünyanın dört bir yanında bulunan sunucularda önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="b3516-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="b3516-137">Buna ek olarak, CDN tarayıcıların farklı etki alanlarında bulunan web siteleri için önbelleğe alınmış üçüncü taraf JavaScript dosyalarını yeniden kullanmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b3516-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="b3516-138">CDN, Güvenli Soketler Katmanı'nı kullanarak bir web sayfasına hizmet vermeniz gerektiğinde SSL'yi (HTTPS) destekler.</span><span class="sxs-lookup"><span data-stu-id="b3516-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="b3516-139">CDN, bu kitaplıkların sahipleri tarafından yüklenen ve size lisanslanan aşağıdaki üçüncü taraf komut dosyası kitaplıklarını barındırmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b3516-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="b3516-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b3516-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="b3516-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="b3516-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="b3516-142">jQuery Mobil (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="b3516-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="b3516-143">jQuery Doğrulama (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="b3516-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="b3516-144">jQuery Döngüsü (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="b3516-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="b3516-145">jQuery Veri Tabloları (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="b3516-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="b3516-146">Microsoft Ajax CDN ayrıca Microsoft tarafından yüklenen aşağıdaki kitaplıkları içerir:</span><span class="sxs-lookup"><span data-stu-id="b3516-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="b3516-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="b3516-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="b3516-148">ASP.NET MVC JavaScript Dosyaları</span><span class="sxs-lookup"><span data-stu-id="b3516-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="b3516-149">ASP.NET SignalR JavaScript Dosyaları</span><span class="sxs-lookup"><span data-stu-id="b3516-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="b3516-150">Microsoft, bu CDN'de barındırılan üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="b3516-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b3516-151">Kütüphanelerin telif hakkı sahipleri bu kütüphaneleri size lisanslıyor.</span><span class="sxs-lookup"><span data-stu-id="b3516-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b3516-152">Bu tür kitaplıkları indirmek ve kullanmak zorunda kaldığınız tüm haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="b3516-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b3516-153">Bunlar Microsoft kitaplıkları olmadığından, Microsoft bu CDN'de barındırılan üçüncü taraf kitaplıkları için hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları hakları dahil) sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="b3516-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="b3516-154">JavaScript kitaplığınızı göndermek istiyorsanız ve kitaplığınız en iyi JavaScript http://trends.builtwith.com) kitaplıklarından biridir ((a) popüler olan bu kitaplıklarda listelenen veya uzantıları/eklentileri; veya (b) ASP.NET kullanım için yararlı dır, lütfen iletişime geçin. AjaxCDNSubmission@Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b3516-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="b3516-155">ajax.microsoft.com ajax.aspnetcdn.com olarak değiştirildi</span><span class="sxs-lookup"><span data-stu-id="b3516-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="b3516-156">CDN microsoft.com etki alanı adını kullanmak için kullanılan ve aspnetcdn.com etki alanı adını kullanmak için değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="b3516-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="b3516-157">Bu değişiklik performansı artırmak için yapıldı, çünkü bir tarayıcı microsoft.com etki alanına atıfta bulunduğunda, her istekle birlikte bu etki alanından herhangi bir tanımlama bilgisi gönderirdi.</span><span class="sxs-lookup"><span data-stu-id="b3516-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="b3516-158">microsoft.com dışındaki bir etki alanı adına yeniden ad vererek performans %25'e kadar artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b3516-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="b3516-159">Not ajax.microsoft.com çalışmaya devam edecektir, ancak ajax.aspnetcdn.com önerilir.</span><span class="sxs-lookup"><span data-stu-id="b3516-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="b3516-160">Eski Biçim:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b3516-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="b3516-161">Yeni Biçim:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b3516-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="b3516-162">Visual Studio .vsdoc Desteği</span><span class="sxs-lookup"><span data-stu-id="b3516-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="b3516-163">.vsdoc dosyalarını Visual Studio 2008 ile düzgün kullanmak için VS 2008 SP1 yüklü olduğundan ve vsdoc dosyalarının düzeltmesinin yüklü olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3516-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="b3516-164">Bunları buradan alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b3516-164">You can get these from here:</span></span>

- [<span data-ttu-id="b3516-165">Karşıdan yükleme Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="b3516-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Karşıdan yükleme Visual Studio 2008 SP1")
- [<span data-ttu-id="b3516-166">Karşıdan yükleme .vsdoc hotfix visual studio 2008 SP1 için</span><span class="sxs-lookup"><span data-stu-id="b3516-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Karşıdan yükleme .vsdoc hotfix visual studio 2008 SP1 için")

<span data-ttu-id="b3516-167">Visual Studio 2010 herhangi bir ek yamalar olmadan .vsdoc dosyaları destekler.</span><span class="sxs-lookup"><span data-stu-id="b3516-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="b3516-168">CDN'den ASP.NET Ajax'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="b3516-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="b3516-169">ASP.NET 4'ASP.NET kullanırken, ASP.NET çerçeve komut dosyaları yla ilgili tüm istekleri CDN'ye yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3516-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="b3516-170">Yerel web sunucunuz yerine CDN'den komut dosyaları almak, genel ASP.NET web sitelerinin performansını önemli ölçüde artırabilir.</span><span class="sxs-lookup"><span data-stu-id="b3516-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="b3516-171">Tüm ASP.NET framework komut dosyası isteklerini Microsoft Ajax CDN'e yönlendirmek için ScriptManager EnableCDN özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="b3516-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="b3516-172">CDN'den jQuery kullanma</span><span class="sxs-lookup"><span data-stu-id="b3516-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="b3516-173">Web uygulamanızda CDN'de barındırılan jQuery komut dosyalarını bir sayfaya aşağıdaki komut dosyası öğesini ekleyerek kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b3516-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="b3516-174">CDN ayrıca aşağıdaki öğeyi kullanarak alabilirsiniz jQuery komut dosyası, minified sürümünü içerir:</span><span class="sxs-lookup"><span data-stu-id="b3516-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="b3516-175">CDN kullanılamıyorsa, sayfanızın kendi web sitenizdeki yerel bir yoldan jQuery yüklemesine geri dönmesine izin vermek için, CDN'ye başvuran öğeden hemen sonra aşağıdaki öğeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3516-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="b3516-176">Aşağıdaki örnek sayfa, bir düğme tıklatıldığında div öğesinin içeriğini görüntülemek için jQuery kitaplığın CDN sürümünü (yerel bir kopyaya geri dönüşle) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3516-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="b3516-177">JQuery web sitesini ziyaret ederek jQuery hakkında daha [jQuery](http://jquery.com/) fazla bilgi edinebilir ve jQuery'nin yerel bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3516-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="b3516-178">CDN'den jQuery UI kullanma</span><span class="sxs-lookup"><span data-stu-id="b3516-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="b3516-179">CDN ayrıca jQuery UI kitaplığını da barındırır.</span><span class="sxs-lookup"><span data-stu-id="b3516-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="b3516-180">jQuery Kullanıcı Bira Kitaplığı, ASP.NET uygulamalarınızda kullanabileceğiniz zengin bir widget ve efekt kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="b3516-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="b3516-181">Örneğin, aşağıdaki sayfa, açılır bir takvimi görüntülemek için ASP.NET Web Formları uygulaması bağlamında jQuery UI Datepicker'ı nasıl kullanabileceğinizi gösterir:</span><span class="sxs-lookup"><span data-stu-id="b3516-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="b3516-182">Klavyenizi kullanarak textbox'a odaklandığınızda bir takvim görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="b3516-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Datepicker ile oluşturulan pop-up takvimi](overview/_static/image1.png)

<span data-ttu-id="b3516-184">Yukarıdaki koda CDN'den üç dosya eklemeniz gerektiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b3516-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="b3516-185">jQuery kitaplığı &mdash; jQuery UI kitaplığı jQuery kitaplığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b3516-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="b3516-186">jQuery UI kitaplığını eklemeden önce sayfanıza jQuery kitaplığını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3516-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="b3516-187">jQuery UI &mdash; kitaplığı jQuery UI kitaplığı yukarıdaki sayfada kullanılan Datepicker widget gibi jQuery UI efektleri ve widget'ların tümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b3516-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="b3516-188">Bir jQuery UI &mdash; tema jQuery UI farklı temalar destekler.</span><span class="sxs-lookup"><span data-stu-id="b3516-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="b3516-189">Yukarıdaki sayfa, Redmond temasını almak için bir CSS dosyasına bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="b3516-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="b3516-190">Standart jQuery UI temalarının tümü CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="b3516-191">Her tema için küçük resimleri görüntülemek için [bu sayfayı ziyaret edin.](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10")</span><span class="sxs-lookup"><span data-stu-id="b3516-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="b3516-192">jQuery UI kitaplığı hakkında daha fazla bilgi edinmek için resmi [jQuery UI web sitesini](http://jQueryUI.com "jQuery UI web sitesi")ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="b3516-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="b3516-193">CDN'deki Üçüncü Taraf Dosyaları</span><span class="sxs-lookup"><span data-stu-id="b3516-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="b3516-194">CDN, en popüler üçüncü taraf JavaScript kitaplıklarından bazılarını barındıran bir kitapdır.</span><span class="sxs-lookup"><span data-stu-id="b3516-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="b3516-195">Microsoft, bu CDN'de barındırılan üçüncü taraf kitaplıklarının sahipliğini talep etmez.</span><span class="sxs-lookup"><span data-stu-id="b3516-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b3516-196">Kütüphanelerin telif hakkı sahipleri bu kütüphaneleri size lisanslıyor.</span><span class="sxs-lookup"><span data-stu-id="b3516-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b3516-197">Bu tür kitaplıkları indirmek ve kullanmak zorunda kaldığınız tüm haklar yalnızca ilgili telif hakkı sahipleri tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="b3516-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b3516-198">Bunlar Microsoft kitaplıkları olmadığından, Microsoft bu CDN'de barındırılan üçüncü taraf kitaplıkları için hiçbir garanti veya fikri mülkiyet hakları lisansı (zımni patent hakları hakları dahil) sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="b3516-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="b3516-199">cdn üzerinde jQuery Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="b3516-200">jQuery aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="b3516-201">jQuery sürüm 3.5.0</span><span class="sxs-lookup"><span data-stu-id="b3516-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="b3516-202">jQuery sürüm 3.4.1</span><span class="sxs-lookup"><span data-stu-id="b3516-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="b3516-203">jQuery sürüm 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b3516-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="b3516-204">jQuery sürüm 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b3516-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="b3516-205">jQuery sürüm 3.2.1</span><span class="sxs-lookup"><span data-stu-id="b3516-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="b3516-206">jQuery sürüm 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="b3516-207">jQuery sürüm 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="b3516-208">jQuery sürüm 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="b3516-209">jQuery sürüm 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="b3516-210">jQuery sürüm 2.2.4</span><span class="sxs-lookup"><span data-stu-id="b3516-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="b3516-211">jQuery sürüm 2.2.3</span><span class="sxs-lookup"><span data-stu-id="b3516-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="b3516-212">jQuery sürüm 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b3516-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="b3516-213">jQuery sürüm 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b3516-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="b3516-214">jQuery sürüm 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="b3516-215">jQuery sürüm 2.1.4</span><span class="sxs-lookup"><span data-stu-id="b3516-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="b3516-216">jQuery sürüm 2.1.3</span><span class="sxs-lookup"><span data-stu-id="b3516-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="b3516-217">jQuery sürüm 2.1.2</span><span class="sxs-lookup"><span data-stu-id="b3516-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="b3516-218">jQuery sürüm 2.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="b3516-219">jQuery sürüm 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="b3516-220">jQuery sürüm 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b3516-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="b3516-221">jQuery sürüm 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b3516-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="b3516-222">jQuery sürüm 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b3516-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="b3516-223">jQuery sürüm 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="b3516-224">jQuery sürüm 1.12.4</span><span class="sxs-lookup"><span data-stu-id="b3516-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="b3516-225">jQuery sürüm 1.12.3</span><span class="sxs-lookup"><span data-stu-id="b3516-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="b3516-226">jQuery sürüm 1.12.2</span><span class="sxs-lookup"><span data-stu-id="b3516-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="b3516-227">jQuery sürüm 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b3516-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="b3516-228">jQuery sürüm 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3516-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="b3516-229">jQuery sürüm 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b3516-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="b3516-230">jQuery sürüm 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b3516-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="b3516-231">jQuery sürüm 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3516-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="b3516-232">jQuery sürüm 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3516-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="b3516-233">jQuery sürüm 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b3516-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="b3516-234">jQuery sürüm 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b3516-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="b3516-235">jQuery sürüm 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3516-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="b3516-236">jQuery sürüm 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3516-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="b3516-237">jQuery sürüm 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b3516-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="b3516-238">jQuery sürüm 1.8.3</span><span class="sxs-lookup"><span data-stu-id="b3516-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="b3516-239">jQuery sürüm 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b3516-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="b3516-240">jQuery sürüm 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b3516-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="b3516-241">jQuery sürüm 1.8.0</span><span class="sxs-lookup"><span data-stu-id="b3516-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="b3516-242">jQuery sürüm 1.7.2</span><span class="sxs-lookup"><span data-stu-id="b3516-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="b3516-243">jQuery sürüm 1.7.1</span><span class="sxs-lookup"><span data-stu-id="b3516-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="b3516-244">jQuery sürüm 1.7</span><span class="sxs-lookup"><span data-stu-id="b3516-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="b3516-245">jQuery sürüm 1.6.4</span><span class="sxs-lookup"><span data-stu-id="b3516-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="b3516-246">jQuery sürüm 1.6.3</span><span class="sxs-lookup"><span data-stu-id="b3516-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="b3516-247">jQuery sürüm 1.6.2</span><span class="sxs-lookup"><span data-stu-id="b3516-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="b3516-248">jQuery sürüm 1.6.1</span><span class="sxs-lookup"><span data-stu-id="b3516-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="b3516-249">jQuery sürüm 1.6</span><span class="sxs-lookup"><span data-stu-id="b3516-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="b3516-250">jQuery sürüm 1.5.2</span><span class="sxs-lookup"><span data-stu-id="b3516-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="b3516-251">jQuery sürüm 1.5.1</span><span class="sxs-lookup"><span data-stu-id="b3516-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="b3516-252">jQuery sürüm 1.5</span><span class="sxs-lookup"><span data-stu-id="b3516-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="b3516-253">jQuery sürüm 1.4.4</span><span class="sxs-lookup"><span data-stu-id="b3516-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="b3516-254">jQuery sürüm 1.4.3</span><span class="sxs-lookup"><span data-stu-id="b3516-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="b3516-255">jQuery sürüm 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b3516-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="b3516-256">jQuery sürüm 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b3516-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="b3516-257">jQuery sürüm 1.4</span><span class="sxs-lookup"><span data-stu-id="b3516-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="b3516-258">jQuery sürüm 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b3516-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="b3516-259">jQuery CDN'de Serbest Geçiş</span><span class="sxs-lookup"><span data-stu-id="b3516-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="b3516-260">jQuery Geçir'in aşağıdaki sürümleri CDN'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="b3516-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="b3516-261">jQuery Geçiş sürümü 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="b3516-262">jQuery Geçiş sürümü 1.2.1</span><span class="sxs-lookup"><span data-stu-id="b3516-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="b3516-263">jQuery Geçiş sürümü 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="b3516-264">jQuery Geçiş sürümü 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="b3516-265">jQuery Geçiş sürümü 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="b3516-266">jQuery Geçiş sürümü 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="b3516-267">jQuery UI CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="b3516-268">jQuery UI kitaplığın aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="b3516-269">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-270">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b3516-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.1")
- [<span data-ttu-id="b3516-271">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3516-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.12.0")
- [<span data-ttu-id="b3516-272">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="b3516-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.4")
- [<span data-ttu-id="b3516-273">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b3516-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.3")
- [<span data-ttu-id="b3516-274">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b3516-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.2")
- [<span data-ttu-id="b3516-275">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3516-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.1")
- [<span data-ttu-id="b3516-276">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3516-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.11.0")
- [<span data-ttu-id="b3516-277">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b3516-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.4")
- [<span data-ttu-id="b3516-278">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="b3516-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.3")
- [<span data-ttu-id="b3516-279">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b3516-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.2")
- [<span data-ttu-id="b3516-280">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b3516-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.1")
- [<span data-ttu-id="b3516-281">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3516-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.10.0")
- [<span data-ttu-id="b3516-282">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b3516-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.2")
- [<span data-ttu-id="b3516-283">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3516-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.1")
- [<span data-ttu-id="b3516-284">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b3516-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.9.0")
- [<span data-ttu-id="b3516-285">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="b3516-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.24")
- [<span data-ttu-id="b3516-286">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="b3516-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.23")
- [<span data-ttu-id="b3516-287">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="b3516-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.22")
- [<span data-ttu-id="b3516-288">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="b3516-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.21")
- [<span data-ttu-id="b3516-289">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="b3516-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.20")
- [<span data-ttu-id="b3516-290">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="b3516-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.19")
- [<span data-ttu-id="b3516-291">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="b3516-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.18")
- [<span data-ttu-id="b3516-292">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="b3516-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.17")
- [<span data-ttu-id="b3516-293">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="b3516-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.16")
- [<span data-ttu-id="b3516-294">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="b3516-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.15")
- [<span data-ttu-id="b3516-295">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="b3516-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.14")
- [<span data-ttu-id="b3516-296">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="b3516-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.13")
- [<span data-ttu-id="b3516-297">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="b3516-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.12")
- [<span data-ttu-id="b3516-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="b3516-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.11")
- [<span data-ttu-id="b3516-299">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="b3516-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.10")
- [<span data-ttu-id="b3516-300">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="b3516-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.9")
- [<span data-ttu-id="b3516-301">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="b3516-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.8")
- [<span data-ttu-id="b3516-302">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="b3516-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.7")
- [<span data-ttu-id="b3516-303">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b3516-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN üzerinde jQuery Kullanıcı Arabirimi 1.8.6")
- [<span data-ttu-id="b3516-304">jQuery Kullanıcı Arabirimi 1.8.5</span><span class="sxs-lookup"><span data-stu-id="b3516-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery Kullanıcı Arabirimi 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="b3516-305">cdn üzerinde jQuery Doğrulama Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="b3516-306">[jQuery Doğrulama](https://jqueryvalidation.org/ "jQuery Doğrulama Eklentisi") eklentisinin aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3516-307">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-308">jQuery Doğrulama 1.19.1</span><span class="sxs-lookup"><span data-stu-id="b3516-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery Doğrulama 1.19.1")
- [<span data-ttu-id="b3516-309">jQuery Onayla 1.19.0</span><span class="sxs-lookup"><span data-stu-id="b3516-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery Doğrulama 1.19.0")
- [<span data-ttu-id="b3516-310">jQuery Doğrulama 1.17.0</span><span class="sxs-lookup"><span data-stu-id="b3516-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery Doğrulama 1.17.0")
- [<span data-ttu-id="b3516-311">jQuery Doğrulama 1.16.0</span><span class="sxs-lookup"><span data-stu-id="b3516-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Doğrulaması 1.16.0")
- [<span data-ttu-id="b3516-312">jQuery Doğrulama 1.15.1</span><span class="sxs-lookup"><span data-stu-id="b3516-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Doğrulaması 1.15.1")
- [<span data-ttu-id="b3516-313">jQuery Doğrulama 1.15.0</span><span class="sxs-lookup"><span data-stu-id="b3516-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Doğrulaması 1.15.0")
- [<span data-ttu-id="b3516-314">jQuery Doğrulama 1.14.0</span><span class="sxs-lookup"><span data-stu-id="b3516-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Doğrulaması 1.14.0")
- [<span data-ttu-id="b3516-315">jQuery Doğrulama 1.13.1</span><span class="sxs-lookup"><span data-stu-id="b3516-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Doğrulaması 1.13.1")
- [<span data-ttu-id="b3516-316">jQuery Doğrulama 1.13.0</span><span class="sxs-lookup"><span data-stu-id="b3516-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Doğrulaması 1.13.0")
- [<span data-ttu-id="b3516-317">jQuery Doğrulama 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3516-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Doğrulaması 1.12.0")
- [<span data-ttu-id="b3516-318">jQuery Doğrulama 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3516-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Doğrulaması 1.11.1")
- [<span data-ttu-id="b3516-319">jQuery Doğrulama 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3516-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Doğrulaması 1.11.0")
- [<span data-ttu-id="b3516-320">jQuery Doğrulama 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3516-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Doğrulaması 1.10.0")
- [<span data-ttu-id="b3516-321">jQuery Doğrulama 1.9</span><span class="sxs-lookup"><span data-stu-id="b3516-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate sürümü 1.9")
- [<span data-ttu-id="b3516-322">jQuery Doğrulama 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b3516-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate sürümü 1.8.1")
- [<span data-ttu-id="b3516-323">jQuery Doğrulama 1.8</span><span class="sxs-lookup"><span data-stu-id="b3516-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate sürümü 1.8")
- [<span data-ttu-id="b3516-324">jQuery Doğrulama 1.7</span><span class="sxs-lookup"><span data-stu-id="b3516-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate sürümü 1.7")
- [<span data-ttu-id="b3516-325">jQuery Doğrulama 1.6</span><span class="sxs-lookup"><span data-stu-id="b3516-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Doğrulama 1.6")
- [<span data-ttu-id="b3516-326">jQuery Doğrulama 1.5.5</span><span class="sxs-lookup"><span data-stu-id="b3516-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Doğrulama 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="b3516-327">CDN üzerinde jQuery Mobil Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="b3516-328">jQuery Mobile kitaplığın aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="b3516-329">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-330">jQuery Mobil 1.4.5</span><span class="sxs-lookup"><span data-stu-id="b3516-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.5")
- [<span data-ttu-id="b3516-331">jQuery Mobil 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b3516-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.2")
- [<span data-ttu-id="b3516-332">jQuery Mobil 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b3516-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.1")
- [<span data-ttu-id="b3516-333">jQuery Mobil 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b3516-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.4.0")
- [<span data-ttu-id="b3516-334">jQuery Mobil 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b3516-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.2")
- [<span data-ttu-id="b3516-335">jQuery Mobil 1.3.1</span><span class="sxs-lookup"><span data-stu-id="b3516-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.1")
- [<span data-ttu-id="b3516-336">jQuery Mobil 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b3516-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.3.0")
- [<span data-ttu-id="b3516-337">jQuery Mobil 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.2.0")
- [<span data-ttu-id="b3516-338">jQuery Mobil 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b3516-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.2")
- [<span data-ttu-id="b3516-339">jQuery Mobil 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.1")
- [<span data-ttu-id="b3516-340">jQuery Mobil 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0")
- [<span data-ttu-id="b3516-341">jQuery Mobil 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b3516-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="b3516-342">jQuery Mobil 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b3516-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0.1")
- [<span data-ttu-id="b3516-343">jQuery Mobil 1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0")
- [<span data-ttu-id="b3516-344">jQuery Mobil 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b3516-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="b3516-345">jQuery Mobil 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="b3516-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="b3516-346">jQuery Mobil 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="b3516-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN üzerinde jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="b3516-347">jQuery Şablonlar CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="b3516-348">jQuery Şablonları eklentisinin aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3516-349">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-350">jQuery Şablonları Beta 1</span><span class="sxs-lookup"><span data-stu-id="b3516-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Şablonları Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="b3516-351">cdn üzerinde jQuery Döngüsü Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="b3516-352">jQuery Döngüsü eklentisinin aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3516-353">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-354">jQuery Döngüsü 2.99</span><span class="sxs-lookup"><span data-stu-id="b3516-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Döngüsü 2.99")
- [<span data-ttu-id="b3516-355">jQuery Döngüsü 2.94</span><span class="sxs-lookup"><span data-stu-id="b3516-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Döngüsü 2.94")
- [<span data-ttu-id="b3516-356">jQuery Döngüsü 2.88</span><span class="sxs-lookup"><span data-stu-id="b3516-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Döngüsü 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="b3516-357">jQuery DataTables CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="b3516-358">jQuery DataTables eklentisinin aşağıdaki sürümleri bu CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3516-359">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="b3516-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="b3516-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b3516-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="b3516-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="b3516-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="b3516-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="b3516-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="b3516-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b3516-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="b3516-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3516-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="b3516-366">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b3516-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="b3516-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b3516-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="b3516-368">CDN'de Modernizr Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="b3516-369">[Modernizr](http://www.modernizr.com "Modernizr") aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="b3516-370">CDN'de JSHint Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="b3516-371">[JSHint](http://www.jshint.com "JSHint") aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="b3516-372">CDN'de Nakavt Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="b3516-373">[Knockout](http://www.knockoutjs.com "Nakavt") aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="b3516-374">CDN'de Yayınları Küreselleştir</span><span class="sxs-lookup"><span data-stu-id="b3516-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="b3516-375">[Globalize'ın](https://github.com/jquery/globalize "Küreselleşin") aşağıdaki sürümleri CDN'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="b3516-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="b3516-376">Sürüm 1.0.0'ı küreselleştir</span><span class="sxs-lookup"><span data-stu-id="b3516-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="b3516-377">Sürüm 0.1.1'i küreselleştir</span><span class="sxs-lookup"><span data-stu-id="b3516-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="b3516-378">tüm kültürler</span><span class="sxs-lookup"><span data-stu-id="b3516-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="b3516-379">"{culture-code}"u istediğiniz kültür koduyla değiştirin, örneğin globalize.culture.en-GB.js== CDN'deki Microsoft Dosyaları ==Bu kitaplıklar Microsoft tarafından yüklendi.</span><span class="sxs-lookup"><span data-stu-id="b3516-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="b3516-380">CDN'deki Yanıt Ları</span><span class="sxs-lookup"><span data-stu-id="b3516-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="b3516-381">Yanıtla'nın [Respond](https://github.com/scottjehl/Respond "Yanıtlama") aşağıdaki sürümleri CDN'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="b3516-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="b3516-382">Sürüm 1.4.2'yi yanıtla</span><span class="sxs-lookup"><span data-stu-id="b3516-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="b3516-383">Sürüm 1.4.1'i yanıtla</span><span class="sxs-lookup"><span data-stu-id="b3516-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="b3516-384">Sürüm 1.4.0'ı yanıtla</span><span class="sxs-lookup"><span data-stu-id="b3516-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="b3516-385">Sürüm 1.3.0'ı yanıtla</span><span class="sxs-lookup"><span data-stu-id="b3516-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="b3516-386">Sürüm 1.2.0'ı yanıtla</span><span class="sxs-lookup"><span data-stu-id="b3516-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="b3516-387">CDN'de Bootstrap Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="b3516-388">[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="b3516-389">Bootstrap sürüm 4.4.1</span><span class="sxs-lookup"><span data-stu-id="b3516-389">Bootstrap version 4.4.1</span></span>

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

#### <a name="bootstrap-version-431"></a><span data-ttu-id="b3516-390">Bootstrap sürüm 4.3.1</span><span class="sxs-lookup"><span data-stu-id="b3516-390">Bootstrap version 4.3.1</span></span>

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

#### <a name="bootstrap-version-421"></a><span data-ttu-id="b3516-391">Bootstrap sürüm 4.2.1</span><span class="sxs-lookup"><span data-stu-id="b3516-391">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="b3516-392">Bootstrap sürüm 4.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-392">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="b3516-393">Bootstrap sürüm 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-393">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-341"></a><span data-ttu-id="b3516-394">Bootstrap sürüm 3.4.1</span><span class="sxs-lookup"><span data-stu-id="b3516-394">Bootstrap version 3.4.1</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="b3516-395">Bootstrap sürüm 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b3516-395">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="b3516-396">Bootstrap sürüm 3.3.7</span><span class="sxs-lookup"><span data-stu-id="b3516-396">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="b3516-397">Bootstrap sürüm 3.3.6</span><span class="sxs-lookup"><span data-stu-id="b3516-397">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="b3516-398">Bootstrap sürüm 3.3.5</span><span class="sxs-lookup"><span data-stu-id="b3516-398">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="b3516-399">Bootstrap sürüm 3.3.4</span><span class="sxs-lookup"><span data-stu-id="b3516-399">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="b3516-400">Bootstrap sürüm 3.3.2</span><span class="sxs-lookup"><span data-stu-id="b3516-400">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="b3516-401">Bootstrap sürüm 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b3516-401">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="b3516-402">Bootstrap sürüm 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b3516-402">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="b3516-403">Bootstrap sürüm 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-403">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="b3516-404">Bootstrap sürüm 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-404">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="b3516-405">Bootstrap sürüm 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-405">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="b3516-406">Bootstrap sürüm 3.0.3</span><span class="sxs-lookup"><span data-stu-id="b3516-406">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="b3516-407">Bootstrap sürüm 3.0.2</span><span class="sxs-lookup"><span data-stu-id="b3516-407">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="b3516-408">Bootstrap sürüm 3.0.1</span><span class="sxs-lookup"><span data-stu-id="b3516-408">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="b3516-409">Bootstrap sürüm 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-409">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="b3516-410">Bootstrap sürüm 2.3.2</span><span class="sxs-lookup"><span data-stu-id="b3516-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="b3516-411">Bootstrap sürüm 2.3.1</span><span class="sxs-lookup"><span data-stu-id="b3516-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="b3516-412">Bootstrap TouchCarousel CDN üzerinde Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="b3516-413">[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel sürümleri aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="b3516-414">Bootstrap TouchCarousel sürüm 0.8.0</span><span class="sxs-lookup"><span data-stu-id="b3516-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="b3516-415">CDN üzerinde Hammer.js Bültenleri</span><span class="sxs-lookup"><span data-stu-id="b3516-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="b3516-416">[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js bültenleri aşağıdaki sürümleri CDN barındırılan:</span><span class="sxs-lookup"><span data-stu-id="b3516-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="b3516-417">Hammer.js sürüm 2.0.4</span><span class="sxs-lookup"><span data-stu-id="b3516-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="b3516-418">ASP.NET Web Formları ve Ajax Bültenleri CDN üzerinde</span><span class="sxs-lookup"><span data-stu-id="b3516-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="b3516-419">ASP.NET Ajax Kütüphanesi'nin aşağıdaki sürümleri CDN'de barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b3516-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="b3516-420">Gerçek dosya listesini görmek için her bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3516-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3516-421">ASP.NET Web Formları ve Ajax sürüm 4.5.2</span><span class="sxs-lookup"><span data-stu-id="b3516-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms ve Ajax 4.5.2")
- [<span data-ttu-id="b3516-422">ASP.NET Web Formları ve Ajax sürüm 4</span><span class="sxs-lookup"><span data-stu-id="b3516-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms ve Ajax 4")
- [<span data-ttu-id="b3516-423">ASP.NET Ajax sürüm 3.5</span><span class="sxs-lookup"><span data-stu-id="b3516-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="b3516-424">CDN'de ASP.NET MVC Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="b3516-425">Aşağıdaki ASP.NET MVC JavaScript dosyaları bu CDN'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="b3516-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="b3516-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="b3516-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="b3516-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="b3516-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="b3516-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="b3516-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="b3516-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="b3516-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="b3516-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="b3516-430">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="b3516-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="b3516-432">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="b3516-433">CDN'de ASP.NET SignalR Yayınları</span><span class="sxs-lookup"><span data-stu-id="b3516-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="b3516-434">Aşağıdaki ASP.NET SignalR JavaScript dosyaları bu CDN'de barındırılır:</span><span class="sxs-lookup"><span data-stu-id="b3516-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="b3516-435">ASP.NET Sinyalci 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b3516-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="b3516-436">ASP.NET Sinyalci 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b3516-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="b3516-437">ASP.NET Sinyalci 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b3516-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="b3516-438">ASP.NET Sinyalci 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="b3516-439">ASP.NET Sinyalci 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b3516-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="b3516-440">ASP.NET Sinyalci 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b3516-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="b3516-441">ASP.NET Sinyalci 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b3516-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="b3516-442">ASP.NET Sinyalci 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3516-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="b3516-443">ASP.NET Sinyalci 1.1.3</span><span class="sxs-lookup"><span data-stu-id="b3516-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="b3516-444">ASP.NET Sinyalci 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b3516-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="b3516-445">ASP.NET Sinyalci 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3516-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="b3516-446">ASP.NET Sinyalci 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3516-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="b3516-447">ASP.NET Sinyalci 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b3516-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="b3516-448">CDN kullanım koşulları hakkında daha fazla bilgi için [Microsoft Ajax CDN Kullanım Koşulları'na](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Kullanım Koşulları")bakın.</span><span class="sxs-lookup"><span data-stu-id="b3516-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
