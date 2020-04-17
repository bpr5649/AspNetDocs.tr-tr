---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET ve Web Araçları için Yayın Notları 2013.1 Visual Studio 2012 | Microsoft Dokümanlar
author: rick-anderson
description: Bu belge, Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1 sürümü açıklanmaktadır.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543580"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="31c44-103">Visual Studio 2012 için ASP.NET and Web Tools 2013.1 Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="31c44-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="31c44-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="31c44-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="31c44-105">Bu belge, Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1 sürümü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="31c44-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="31c44-106">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="31c44-106">Contents</span></span>

- [<span data-ttu-id="31c44-107">Kurulum Notları</span><span class="sxs-lookup"><span data-stu-id="31c44-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="31c44-108">Yazılım Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="31c44-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="31c44-109">Visual Studio 2012 için ASP.NET ve Web Araçlarında Yeni Özellikler 2013.1</span><span class="sxs-lookup"><span data-stu-id="31c44-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="31c44-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="31c44-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="31c44-111">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="31c44-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="31c44-112">ASP.NET MVC 5 şablonu</span><span class="sxs-lookup"><span data-stu-id="31c44-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="31c44-113">ASP.NET Web API 2 şablonu</span><span class="sxs-lookup"><span data-stu-id="31c44-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="31c44-114">Öğe Şablonları</span><span class="sxs-lookup"><span data-stu-id="31c44-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="31c44-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="31c44-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="31c44-116">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="31c44-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="31c44-117">Razor Editörü</span><span class="sxs-lookup"><span data-stu-id="31c44-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="31c44-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="31c44-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="31c44-119">Bilinen Sorunlar ve Son Dakika Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31c44-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="31c44-120">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="31c44-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="31c44-121">MVC ve Web API İskele - HTTP 404, Bulunamadı hatası</span><span class="sxs-lookup"><span data-stu-id="31c44-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="31c44-122">Web için Visual Studio Express 2012, iskeleye bağlı bir öğe ekledikten sonra çalışmayı durdurur</span><span class="sxs-lookup"><span data-stu-id="31c44-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="31c44-123">ASP.NET Jilet 3</span><span class="sxs-lookup"><span data-stu-id="31c44-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="31c44-124">Cshtml dosyasInI Gözat veya F5 ile görüntülemek sunucu hatasına neden olur</span><span class="sxs-lookup"><span data-stu-id="31c44-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="31c44-125">Url Yeniden Yazma ve Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="31c44-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="31c44-126">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="31c44-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="31c44-127">Kurulum Notları</span><span class="sxs-lookup"><span data-stu-id="31c44-127">Installation Notes</span></span>

<span data-ttu-id="31c44-128">[Yükle](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012 için ASP.NET ve Web Araçları 2013.1.</span><span class="sxs-lookup"><span data-stu-id="31c44-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="31c44-129">Yazılım Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="31c44-129">Software Requirements</span></span>

<span data-ttu-id="31c44-130">Web için Visual Studio 2012 veya Visual Studio Express 2012'ye sahip olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="31c44-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="31c44-131">Visual Studio 2012 için ASP.NET ve Web Araçlarında Yeni Özellikler 2013.1</span><span class="sxs-lookup"><span data-stu-id="31c44-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="31c44-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="31c44-132">Bootstrap</span></span>

<span data-ttu-id="31c44-133">MVC 5 denetleyicilerini ve görünümlerini iskeleye aldığınızda, görünümlerin biçimlendirmesi [Bootstrap'ı](http://getbootstrap.com/)kullanır.</span><span class="sxs-lookup"><span data-stu-id="31c44-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="31c44-134">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="31c44-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="31c44-135">ASP.NET MVC 5 şablonu</span><span class="sxs-lookup"><span data-stu-id="31c44-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="31c44-136">Yeni bir MVC 5 şablonu ekledik.</span><span class="sxs-lookup"><span data-stu-id="31c44-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="31c44-137">En son MVC 5 NuGet paketlerine atıfta bulunur ve denetleyiciler ve görünümler eklemek için iskeleyi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="31c44-138">ASP.NET Web API 2 şablonu</span><span class="sxs-lookup"><span data-stu-id="31c44-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="31c44-139">Yeni bir Web API 2 şablonu ekledik.</span><span class="sxs-lookup"><span data-stu-id="31c44-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="31c44-140">En son Web API 2 NuGet paketlerine başvurur ve denetleyiciler ve görünümler eklemek için iskeleyi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="31c44-141">Öğe Şablonları</span><span class="sxs-lookup"><span data-stu-id="31c44-141">Item Templates</span></span>

<span data-ttu-id="31c44-142">MVC 5 görünümleri, Web Sayfaları (Razor 3) ve Web API 2 denetleyicileri için yeni öğe şablonları ekledik.</span><span class="sxs-lookup"><span data-stu-id="31c44-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="31c44-143">Yeni öğeler eklerken ilgili NuGet paketlerini projeye yüklerler.</span><span class="sxs-lookup"><span data-stu-id="31c44-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="31c44-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="31c44-144">Entity Framework 6</span></span>

<span data-ttu-id="31c44-145">Varlık Çerçevesi'ni kullanarak bir MVC veya Web API denetleyicisi satın aldığınızda, Framework 6'yı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="31c44-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="31c44-146">Varlık Çerçevesi hakkında daha fazla bilgi için [Entity Framework Version History'ye](https://msdn.com/data/jj574253)bakın.</span><span class="sxs-lookup"><span data-stu-id="31c44-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="31c44-147">Ayrıca Visual Studio 2012 için Entity Framework 6 Tools'u indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="31c44-148">Varlık [Çerçevesini Al'a](https://msdn.com/data/ee712906#tooling)bakın.</span><span class="sxs-lookup"><span data-stu-id="31c44-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="31c44-149">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="31c44-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="31c44-150">ASP.NET İskele, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="31c44-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="31c44-151">Projenize bir veri modeliyle etkileşimde bulunarak ortak kod eklemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="31c44-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="31c44-152">Visual Studio'nun önceki sürümlerinde, iskele ASP.NET MVC projeleri ile sınırlıydı.</span><span class="sxs-lookup"><span data-stu-id="31c44-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="31c44-153">Bu güncelleştirmeyle, artık Web Formlar da dahil olmak üzere herhangi bir ASP.NET projesi için iskele kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="31c44-154">Bu güncelleştirme, bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Formları ile iskeleyi kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="31c44-155">Web Formları için sayfa oluşturma desteği gelecekteki bir güncelleştirmede eklenir.</span><span class="sxs-lookup"><span data-stu-id="31c44-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="31c44-156">İskele kullanırken, gerekli tüm bağımlılıkların projeye yüklenmesini sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="31c44-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="31c44-157">Örneğin, bir web formları projesi ASP.NETyle başlayıp web API Denetleyicisi eklemek için iskele kullanırsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="31c44-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="31c44-158">Bir Web Forms projesine MVC iskelesi eklemek için **Yeni İskele Öğesi** ekleyin ve iletişim penceresinde **MVC 5 Bağımlılıkları'nı** seçin.</span><span class="sxs-lookup"><span data-stu-id="31c44-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="31c44-159">İskele MVC için iki seçenek vardır; Minimal ve Tam.</span><span class="sxs-lookup"><span data-stu-id="31c44-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="31c44-160">Minimal'i seçerseniz, projenize yalnızca ASP.NET MVC için NuGet paketleri ve referansları eklenir.</span><span class="sxs-lookup"><span data-stu-id="31c44-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="31c44-161">Tam seçeneği seçerseniz, Bir MVC projesi için gerekli içerik dosyalarının yanı sıra Minimal bağımlılıklar eklenir.</span><span class="sxs-lookup"><span data-stu-id="31c44-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="31c44-162">İskele async denetleyicileri desteği, Entity Framework 6'nın yeni async özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="31c44-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="31c44-163">Daha fazla bilgi ve öğreticiler için, [ASP.NET İskele Genel bakınız.](../2013/aspnet-scaffolding-overview.md)</span><span class="sxs-lookup"><span data-stu-id="31c44-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="31c44-164">Bu öğreticiler Visual Studio 2013 ile iskele göstermek, ama aynı zamanda Visual Studio 2012 için ASP.NET ve Web Tools 2013.1 için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="31c44-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="31c44-165">Razor Editörü</span><span class="sxs-lookup"><span data-stu-id="31c44-165">Razor Editor</span></span>

<span data-ttu-id="31c44-166">Bu güncelleme ile Visual Studio 2012 artık Razor 3 araç/düzenlemeyi destekliyor.</span><span class="sxs-lookup"><span data-stu-id="31c44-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="31c44-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="31c44-167">NuGet 2.7</span></span>

<span data-ttu-id="31c44-168">NuGet 2.7, [NuGet 2.7 Sürüm Notları'nda](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir yeni özellik kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="31c44-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="31c44-169">NuGet'in bu sürümü, kullanıcıların NuGet'in eksik paketleri geri yüklemesine açıkça izin verme gereğini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="31c44-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="31c44-170">NuGet 2.7'yi yüklerken, kullanıcılar eksik paketleri otomatik olarak geri yüklemeyi dolaylı olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="31c44-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="31c44-171">Kullanıcılar Visual Studio'daki NuGet ayarları aracılığıyla paket geri yüklemesini açıkça devre dışı edebilirler.</span><span class="sxs-lookup"><span data-stu-id="31c44-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="31c44-172">Bu değişiklik, paket geri yüklemenin nasıl çalıştığını basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="31c44-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="31c44-173">Bilinen Sorunlar ve Son Dakika Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31c44-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="31c44-174">ASP.NET İskele</span><span class="sxs-lookup"><span data-stu-id="31c44-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="31c44-175">MVC ve Web API İskele - HTTP 404, Bulunamadı hatası</span><span class="sxs-lookup"><span data-stu-id="31c44-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="31c44-176">Bir projeye iskeleye ayrılmış bir öğe eklerken bir hatayla karşılaşırsanız, projenizin tutarsız bir durumda kalması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="31c44-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="31c44-177">İskele olarak yapılan değişikliklerin bazıları geri alınır, ancak yüklenen NuGet paketleri gibi diğer değişiklikler geri alınmaz.</span><span class="sxs-lookup"><span data-stu-id="31c44-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="31c44-178">Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar iskeledeki öğelerde gezinirken bir HTTP 404 hatası alır.</span><span class="sxs-lookup"><span data-stu-id="31c44-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="31c44-179">MVC için bu hatayı düzeltmek için yeni bir iskele öğesi ekleyin ve MVC 5 Bağımlılıkları 'nı (Minimal veya Tam) seçin.</span><span class="sxs-lookup"><span data-stu-id="31c44-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="31c44-180">Bu işlem, projenize gerekli tüm değişiklikleri ekler.</span><span class="sxs-lookup"><span data-stu-id="31c44-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="31c44-181">Web API için bu hatayı düzeltmek için:</span><span class="sxs-lookup"><span data-stu-id="31c44-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="31c44-182">Projenize aşağıdaki WebApiConfig sınıfını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31c44-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="31c44-183">Global.asax'ta Uygulama\_Başlangıç yönteminde WebApiConfig.Register'ı aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="31c44-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="31c44-184">Web için Visual Studio Express 2012, iskeleye bağlı bir öğe ekledikten sonra çalışmayı durdurur</span><span class="sxs-lookup"><span data-stu-id="31c44-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="31c44-185">Web için Visual Studio Express 2012, Entity Framework ile (Entity Framework kullanarak web API 2 Controller gibi) İskeleli öğe ekledikten sonra çalışmayı durdurursa, Visual Studio Express'in System.Web.Extensions'a bağlı bir derlemenin yerel görüntüsünü yüklememesi mümkündür.</span><span class="sxs-lookup"><span data-stu-id="31c44-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="31c44-186">Bu sorunu gidermek için Visual Studio Express'i System.Web.Extensions'ın MSIL görüntüsüyle çalışacak şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="31c44-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="31c44-187">Yönetici modunda Komut İstem'i açın.</span><span class="sxs-lookup"><span data-stu-id="31c44-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="31c44-188">%ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE veya %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (64 bit Windows için) gidin.</span><span class="sxs-lookup"><span data-stu-id="31c44-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="31c44-189">Bir metin editöründe VWDExpress.exe.config'i açın.</span><span class="sxs-lookup"><span data-stu-id="31c44-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="31c44-190">Yapılandırma&lt;&gt; &lt;&gt;/çalışma zamanı öğesinin altına aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="31c44-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="31c44-191">Web için Visual Studio Express 2012'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="31c44-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="31c44-192">ASP.NET Jilet 3</span><span class="sxs-lookup"><span data-stu-id="31c44-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="31c44-193">Cshtml dosyasInI Gözat veya F5 ile görüntülemek sunucu hatasına neden olur</span><span class="sxs-lookup"><span data-stu-id="31c44-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="31c44-194">Visual Studio 2012'de bir MVC 5 projesi oluşturduğunuzda (veya Visual Studio 2012'de açılan bir MVC 5 projesi 2013'te oluşturulduğunda) ve Gözat ile veya F5 kullanarak bir cshtml dosyasını görüntülemeye çalıştığınızda, bir hata alırsınız - **Sunucu Hatası '/' Uygulamasında**.</span><span class="sxs-lookup"><span data-stu-id="31c44-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="31c44-195">Sunucu gezinmek için çalışır`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="31c44-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="31c44-196">Bu sorunu gidermek için, projenizdeki **Başlangıç Eylemi** ayarını **Belirli Sayfa**olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="31c44-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="31c44-197">Sayfa için bir değer sağlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="31c44-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="31c44-198">Bu değişikliği yaptıktan sonra, F5'i seçerek uygulamanızın köküne doğru iletin (`http://localhost:XXXX`).</span><span class="sxs-lookup"><span data-stu-id="31c44-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="31c44-199">Bu davranış, **Geçerli Sayfa** ayarının açık sayfayı başlattığı Visual Studio 2013'teki MVC 5 projelerinin davranışıyla aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="31c44-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="31c44-200">Url Yeniden Yazma ve Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="31c44-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="31c44-201">ASP.NET Razor 3 veya ASP.NET MVC 5'e yükselttikten sonra, URL yeniden yazmalarını kullanıyorsanız tilde(~) gösterimi artık doğru çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="31c44-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="31c44-202">URL &lt;yeniden yazma, A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;gibi HTML öğelerindeki tilde(~) gösterimini etkiler ve sonuç olarak tilde artık kök diziniyle eşlenmez.</span><span class="sxs-lookup"><span data-stu-id="31c44-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="31c44-203">Örneğin, **asp.net** **için asp.net/content** isteklerini yeniden yazarsanız, A &lt;href="~/content/"/&gt; adresindeki href özniteliği **/**/ **içerik/içerik/** yerine giderir.</span><span class="sxs-lookup"><span data-stu-id="31c44-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="31c44-204">Bu değişikliği bastırmak için, **IIS\_WasUrlRewritten** bağlamını her Web Sayfasında veya Global.asax'taki **Application\_BeginRequest'de** false olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="31c44-205">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="31c44-205">Templates</span></span>

<span data-ttu-id="31c44-206">Visual Studio 2012 ile Windows 8.1 veya Windows Server 2012 R2'de ASP.NET MVC projeleri oluşturduğunuzda, Visual Studio "ASP.NET 4,5 için Web [url]'yi yapılandırma" belirten bir hata iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="31c44-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![yapılandırma hatası](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="31c44-208">Visual Studio 2012, Windows'un bu sürümlerine yüklendiğinde ASP.NET 4.5 özelliğini etkinleştirmediği için bu hatayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="31c44-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="31c44-209">4,5 ASP.NET etkinleştirmek için Windows özelliklerini aç veya kapat'ta açıklanan adımları [gerçekleştirin.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)</span><span class="sxs-lookup"><span data-stu-id="31c44-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows özelliklerini açma veya kapatma](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="31c44-211">Alternatif olarak, komut satırı üzerinden 4,5 ASP.NET etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c44-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="31c44-212">Yönetici modunda Komut İstem'i açın.</span><span class="sxs-lookup"><span data-stu-id="31c44-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="31c44-213">4,5 ASP.NET sağlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="31c44-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
