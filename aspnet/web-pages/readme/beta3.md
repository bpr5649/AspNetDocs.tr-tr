---
uid: web-pages/readme/beta3
title: Web Matrix ve ASP.NET Web sayfaları (Razor) Beta 3 yayını Benioku dosyası | Microsoft Docs
author: rick-anderson
description: WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124112"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="48a8a-103">WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası</span><span class="sxs-lookup"><span data-stu-id="48a8a-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="48a8a-104">WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası</span><span class="sxs-lookup"><span data-stu-id="48a8a-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="48a8a-105">9 Kasım 2010</span><span class="sxs-lookup"><span data-stu-id="48a8a-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="48a8a-106">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="48a8a-106">Contents</span></span>

- [<span data-ttu-id="48a8a-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="48a8a-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="48a8a-108">Yükleme</span><span class="sxs-lookup"><span data-stu-id="48a8a-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="48a8a-109">Yeni özellikleri, değişiklikler ve Beta 3 Yayını'te bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="48a8a-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="48a8a-110">WebMatrix yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="48a8a-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="48a8a-111">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="48a8a-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="48a8a-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="48a8a-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="48a8a-113">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="48a8a-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="48a8a-114">Uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="48a8a-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="48a8a-115">Diğer Sorunlar</span><span class="sxs-lookup"><span data-stu-id="48a8a-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="48a8a-116">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="48a8a-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="48a8a-117">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="48a8a-117">Overview</span></span>

> <span data-ttu-id="48a8a-118">Microsoft WebMatrix Beta dakikalar içinde yüklenen bir ücretsiz web geliştirme yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="48a8a-119">Veritabanını ve programlama çerçevelerini tek, tümleşik bir deneyim oluşturmak için bir web sunucusu tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="48a8a-120">DotNetNuke, Umbraco, WordPress ve Joomla gibi popüler açık kaynak uygulamalar kullanarak yeni bir Web sitesini başlatmak için WebMatrix Beta kullanabilirsiniz veya kod, test ve kendi ASP.NET veya PHP Web sitesi yayımlama yolu kolaylaştırmak için WebMatrix Beta kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="48a8a-121">WebMatrix Beta, aynı güçlü web sunucusu, veritabanı altyapısı ve Web sitenizi geliştirmeden üretime geçişinizin düzgün ve sorunsuz kılan Internet üzerinde çalışır ve çerçeveler ortamının kullanır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="48a8a-122">Yükleme</span><span class="sxs-lookup"><span data-stu-id="48a8a-122">Installation</span></span>

> <span data-ttu-id="48a8a-123">WebMatrix Beta 3'ü yüklemek için kullandığınız [Microsoft Web Platformu yükleyicisi 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="48a8a-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="48a8a-124">Web Platformu yükleyicisi yükledikten sonra WebMatrix Beta 3'ü yüklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="48a8a-125">Yükleme sırasında sorunlarla karşılaşırsanız, başvurmak [Microsoft Web Platformu Yükleyicisi ile sorunları giderme](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="48a8a-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="48a8a-126">Uygulamaları yayımlama yönergeleri</span><span class="sxs-lookup"><span data-stu-id="48a8a-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="48a8a-127">Bkz: [uygulamaları yayımlama hakkında adım adım yönergeler](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="48a8a-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="48a8a-128">Yeni özellikleri, değişiklikler, andKnown sorunları</span><span class="sxs-lookup"><span data-stu-id="48a8a-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="48a8a-129">WebMatrix Beta 3 yükleme</span><span class="sxs-lookup"><span data-stu-id="48a8a-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="48a8a-130">Sorun: WebMatrix Beta 3 yalnızca Microsoft .NET Framework 4'ü destekleyen platformlar üzerinde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="48a8a-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="48a8a-131">.NET Framework sürüm 4 WebMatrix Beta için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="48a8a-132">Bazı durumlarda, WebMatrix Beta yükleyici, desteklenen bir yapılandırma kümesinin parçası olmayan bir platformda yüklemeye olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="48a8a-133">Özellikle, Windows Vista SP1 Güncelleştirmesi olmadan, WebMatrix Beta yüklemesi başlamadan olanak tanır, ancak .NET Framework 4 bileşeni başarısız olur ve yüklemenizi engelleme.</span><span class="sxs-lookup"><span data-stu-id="48a8a-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="48a8a-134">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-134">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-135">İçeren desteklenen bir platform üzerinde yükleyin:</span><span class="sxs-lookup"><span data-stu-id="48a8a-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="48a8a-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="48a8a-136">Windows 7</span></span>
> - <span data-ttu-id="48a8a-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="48a8a-137">Windows Server 2008</span></span>
> - <span data-ttu-id="48a8a-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="48a8a-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="48a8a-139">Windows Vista SP1 veya sonraki sürümü</span><span class="sxs-lookup"><span data-stu-id="48a8a-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="48a8a-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="48a8a-140">Windows XP SP3</span></span>
> - <span data-ttu-id="48a8a-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="48a8a-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="48a8a-142">Sorun: Microsoft Visual Studio 2008 Microsoft Visual Studio 2008 SP1 yüklediyseniz, WebMatrix Beta 3'ü yükleyemezsiniz</span><span class="sxs-lookup"><span data-stu-id="48a8a-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="48a8a-143">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-143">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-144">Yükleme [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft İndirme Merkezi'nden.</span><span class="sxs-lookup"><span data-stu-id="48a8a-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="48a8a-145">Sorun: SQL Server Compact 4.0 için bazı derlemeler GAC yüklü değil</span><span class="sxs-lookup"><span data-stu-id="48a8a-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="48a8a-146">SQL Server Compact 4.0 için yönetilen derlemeleri genel derleme önbelleğinde (GAC), 64-bit bir bilgisayarda SQL Server Compact 4.0 yükledikten ve bilgisayarın yalnızca .NET Framework 3.5 SP1 istemci yüklü profili olduğunda yerleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="48a8a-147">GAC'de kurulu değil Yönetilen derlemeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="48a8a-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="48a8a-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span><span class="sxs-lookup"><span data-stu-id="48a8a-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="48a8a-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span><span class="sxs-lookup"><span data-stu-id="48a8a-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="48a8a-150">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-150">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-151">Kaldırma SQL Server Compact 4.0.</span><span class="sxs-lookup"><span data-stu-id="48a8a-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="48a8a-152">İndirin ve .NET Framework 3.5 SP1'in tam sürümünü şu konumdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="48a8a-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="48a8a-153">Microsoft .NET Framework 3.5 Service pack 1 (tam paket)</span><span class="sxs-lookup"><span data-stu-id="48a8a-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="48a8a-154">Ardından SQL Server Compact 4.0 yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="48a8a-155">Sorun: SQL Server için komut satırını kullanarak Compact kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="48a8a-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="48a8a-156">SQL Server komut satırı seçeneklerini kullanarak Compact kaldırılması, bu sürümde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="48a8a-157">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-157">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-158">Kullanım *programlar ve Özellikler* Microsoft SQL Server Compact 4.0 kaldırmak için Windows Denetim Masası'nda.</span><span class="sxs-lookup"><span data-stu-id="48a8a-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="48a8a-159">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="48a8a-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="48a8a-160">Belgenin bu bölümünde, yeni özellikleri, değişiklikler ve Razor sözdizimi olan ASP.NET Web sayfaları'nın Beta 3 sürüm ile ilgili bilinen sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="48a8a-161">Yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="48a8a-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="48a8a-162">Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="48a8a-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="48a8a-163">Sorunları</span><span class="sxs-lookup"><span data-stu-id="48a8a-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="48a8a-164">Beta 3 ASP.NET Web sayfaları için Razor sözdizimi olan yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="48a8a-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="48a8a-165">New: "Html.Raw" yöntemi, biçimlendirme kodlanmamış işler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="48a8a-166">Yeni `Html.Raw` kodlanmış çıkış işleme yerine biçimlendirmesi olarak HTML biçimlendirmesi oluşturmak yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48a8a-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="48a8a-167">(Varsayılan olarak, ASP.NET Razor dizeleri işlemeden önce kodlar.) Sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="48a8a-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="48a8a-168">Aşağıdaki örnek nasıl kullanılacağını gösterir `Html.Raw`:</span><span class="sxs-lookup"><span data-stu-id="48a8a-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="48a8a-169">Beta 3 ASP.NET Web sayfaları için Razor sözdizimi olan değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="48a8a-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="48a8a-170">Değiştir: Kaldırıldı "HrefAttribute" yöntemi</span><span class="sxs-lookup"><span data-stu-id="48a8a-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="48a8a-171">`HrefAttribute` Yöntemi `WebPage` sınıfı kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="48a8a-172">Bu yardımcı, URL'lerde güvenli olmayan karakterleri kodlamak için kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="48a8a-173">ASP.NET Razor otomatik olarak dizeyi kodlar için artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="48a8a-174">(Yeni `Html.Raw` kodlanmamış dizeleri işlemek için yöntemi.)</span><span class="sxs-lookup"><span data-stu-id="48a8a-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="48a8a-175">Değiştir: Söz dizimi için bildirime dayalı "@helper" Yardımcıları değiştirildi</span><span class="sxs-lookup"><span data-stu-id="48a8a-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="48a8a-176">Bunu nasıl kullanılarak oluşturulan Yardımcıları ayrıştırır ASP.NET Beta 3 sürümde değişiklikleri `@helper` söz dizimi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="48a8a-177">Esas olarak, `@helper` söz dizimi bir kod bloğu bir blok halinde kod içeren bir biçimlendirme olarak artık ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="48a8a-178">Bu nedenle, yardımcı içinde kod içinde içine alınması gerekmez `@{ }` engeller.</span><span class="sxs-lookup"><span data-stu-id="48a8a-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="48a8a-179">Buna karşılık, HTML öğeleri ya da ASP.NET Razor açıkça dahil edilmek üzere biçimlendirme içinde yardımcı olan `<text></text>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="48a8a-180">Örneğin, aşağıdaki `@helper` söz dizimi Beta 3 sürümündeki çalışır:</span><span class="sxs-lookup"><span data-stu-id="48a8a-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="48a8a-181">Beta 3 sürümde bu Yardımcısı aşağıdaki örneğe şekilde değiştirilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="48a8a-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="48a8a-182">Dikkat `@{ }` karakter çevresinde Yardımcısı ilk kod artık kullanılmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="48a8a-183">Bu durum, varsayılan olarak Yardımcıları içeriğini bir kod bloğu kabul edilir çünkü.</span><span class="sxs-lookup"><span data-stu-id="48a8a-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="48a8a-184">Yardımcı açılırken başlatan biçimlendirme işler `<a>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="48a8a-185">Yardımcı düz metin veya bir kapanış etiketi içermeyen etiketler oluşturma, (örneğin, `<meta>` etiketleri), işlenmek üzere içeriği olmalıdır `<text></text>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="48a8a-186">Değiştir: "WebPageContext.HttpContext" removed</span><span class="sxs-lookup"><span data-stu-id="48a8a-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="48a8a-187">`WebPageContext.HttpContext` Özelliği kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="48a8a-188">Bunun yerine `HttpContext.Current` kullanın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="48a8a-189">( `WebPageContext.HttpContext` Özelliği yalnızca sarmalanmış bu.)</span><span class="sxs-lookup"><span data-stu-id="48a8a-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="48a8a-190">Değiştir: Yeni paket için "Facebook" Yardımcısı taşındı</span><span class="sxs-lookup"><span data-stu-id="48a8a-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="48a8a-191">`Facebook` Yardımcısı taşındı *Facebook.Helper* içeren kitaplık `Facebook` Yardımcısı ve ek işlevler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="48a8a-192">Bu kitaplık ayrı bir paket halinde "Yükleme Yardımcıları ile Paket Yöneticisi'nde" açıklandığı öğreticide yüklemelisiniz [ASP.NET sayfaları ile çalışmaya başlama](https://go.microsoft.com/fwlink/?LinkId=202889).</span><span class="sxs-lookup"><span data-stu-id="48a8a-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="48a8a-193">Değiştir: Üyelik ve rol güvenlik türleri için yeni bir derleme taşır</span><span class="sxs-lookup"><span data-stu-id="48a8a-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="48a8a-194">Aşağıdaki türler için taşınan `WebMatrix.WebData` derleme:</span><span class="sxs-lookup"><span data-stu-id="48a8a-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="48a8a-195">Değiştir: "TagBuilder" sınıfı System.Web.WebPages.dll derlemeye taşındı</span><span class="sxs-lookup"><span data-stu-id="48a8a-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="48a8a-196">`TagBuilde` r sınıfı System.Web.WebPages.dll derlemeye taşındı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="48a8a-197">Daha önce ASP.NET MVC parçası olan bir derlemede oluştu.</span><span class="sxs-lookup"><span data-stu-id="48a8a-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="48a8a-198">Bu değişiklik kullanmak için ASP.NET MVC yüklemek gerekmez anlamına gelir. `TagBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="48a8a-199">Ancak, yine sınıftır `System.Web.Mvc` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="48a8a-200">Kullanmak için `TagBuilder` sınıfta (örneğin, bir özel ASP.NET Razor Yardımcısı), ad alanı başvurması gerekir (ekleyerek gibi `@using System.Web.Mvc` kodunuzda).</span><span class="sxs-lookup"><span data-stu-id="48a8a-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="48a8a-201">Değiştir: Değiştirilen doğrulama sözdizimi istemiş olursunuz; Kaldırıldı "Doğrulama" sınıfı</span><span class="sxs-lookup"><span data-stu-id="48a8a-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="48a8a-202">Beta 3 sürümde, her alan veya alanlar, bir dizi için doğrulama devre dışı bırakmak için çağırabilirsiniz `Validation.Exclude` yöntemi, ad veya doğrulamanın dışında tutulacak alanların adlarını geçirme.</span><span class="sxs-lookup"><span data-stu-id="48a8a-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="48a8a-203">Yeni bir söz dizimi doğrulama atlama için Beta 3 sürümü kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="48a8a-204">`Validation` Beta 3'te kullanılan yöntemi kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="48a8a-205">Kullanıcılar, HTML biçimlendirmesi (örneğin, zengin metin düzenleyicisi bir sayfada kullanarak) karşıya yüklemeye, istek doğrulamayı devre dışı bırakmayın, Web sitesi gibi bir hata rapor eder *potansiyel olarak tehlikeli olabilecek bir Request.Form değeristemcidenalgılandı*ve kullanıcı girişi kabul edilmez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="48a8a-206">İstek doğrulamanın devre dışı bırakırsanız, potansiyel olarak tehlikeli olabilecek biçimlendirme içeren veya desteklemez gibi kullanarak betik emin emin olmak için kullanıcı girişini el ile denetlemelisiniz [Microsoft virüsten arası Site komut dosyası kitaplığı V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span><span class="sxs-lookup"><span data-stu-id="48a8a-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="48a8a-207">Otomatik istek doğrulamayı devre dışı bırakmak için çağrı `Request.Unvalidated` yöntemi, alan veya ait istek doğrulamayı atlamak istediğiniz diğer posta nesne adını geçirerek.</span><span class="sxs-lookup"><span data-stu-id="48a8a-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="48a8a-208">Bu yöntem tüm öğeler için doğrulama atlama için kullanabileceğiniz `Form`, `QueryString`, `Cookies`, ve `ServerVariables` koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="48a8a-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="48a8a-209">Aşağıdaki örnekler nasıl kullanılacağını `Unvalidated` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="48a8a-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="48a8a-210">Razor sözdizimi olan ASP.NET Web sayfaları için bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="48a8a-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="48a8a-211">Sorun: Bir özel bir kullanıcı tablosu için üyeliği kullanılırken beklenmeyen davranışı</span><span class="sxs-lookup"><span data-stu-id="48a8a-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="48a8a-212">Bir ASP.NET Razor Web sitesi için üyelik sağlayıcıyı başlatmak için çağrı `WebSecurity.InitializeDatabaseConnection` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="48a8a-213">(Webmatrix'te, başlangıç sitesi şablonunda bu yönteme bir çağrı içerir.  *\_AppStart.cshtml* dosyası.) Varsa `autoCreateTables` bu yöntemin bir parametrenin ayarlanmış true (varsayılan olarak ayarlanır başlangıç sitesi şablonunda true), ve bir tanınmayan tablo adı (ikinci parametresi) yöntemine geçirilen, yöntem bir hata oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="48a8a-214">Bunun yerine, otomatik olarak bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="48a8a-215">Üyelik için bir özel bir kullanıcı tablosu kullanır ancak yanlış tablo adına geçirmek istiyorsanız, bu bir sorun olabilir `WebSecurity.InitializeDatabaseConnection` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="48a8a-216">Belirttiğiniz tablo mevcut değilse yöntemi varsayılan olarak bir hata oluşturmaz, çünkü ve bunun yerine yeni bir tablo oluşturur çünkü uygulama çalışıyor gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="48a8a-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="48a8a-217">Ancak, özel kullanıcı tablonuzda (ve bu alanlara) kullanan uygulama kodu sonunda beklenmeyen hatalarla başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="48a8a-218">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-218">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-219">İçinde geçirilen ad emin `InitializeDatabaseConnection` kullanıcı profili tablosunda üyelik veritabanında veya devre dışı olduğundan emin olun yöntemi eşleşme `autoCreateTables` parametresini false olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="48a8a-220">Sorun: "SQL Server'ın bir kullanıcı örneği oluşturulamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="48a8a-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="48a8a-221">Bir WebMatrix Web uygulaması, SQL Server Express kullanan ve IIS 7.5 Windows 7 veya Windows Server 2008 R2 çalıştıran, SQL Server çalışma zamanında kullanıcının yerel uygulama yolu alınamıyor belirten bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="48a8a-222">**Geçici çözüm** uygulama (genellikle altında ağ hizmeti) çalıştıran Windows hesabı gibi uygulamanın kök klasörler ve alt klasörleri için okuma/yazma izinlerine sahip olduğundan emin olun *uygulama\_veri*.</span><span class="sxs-lookup"><span data-stu-id="48a8a-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="48a8a-223">Bilgi Bankası makalesinde daha ayrıntılı bilgi kullanılabilir [sorunları kullanıcı SQL Server Express örneği oluşturmayı ve ASP.net Web uygulaması projelerinde](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="48a8a-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="48a8a-224">Sorun: Visual Studio'da ad alanları (DLL'ler) özel derlemeler için otomatik olarak alınmaz</span><span class="sxs-lookup"><span data-stu-id="48a8a-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="48a8a-225">Visual Studio projede özel derlemeler kullanırsanız, tasarım zamanında bu derlemeleri bildirilen ad alanları otomatik olarak alınmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="48a8a-226">Sonuç olarak, özel tür başvuruları tasarım zamanında tanınmayabilir ve (bir "dalgalı" kullanarak) içinde tanınan Visual Studio işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="48a8a-227">Visual Studio'da tasarım zamanında yalnızca bu sorun oluşur; Uygulama düzgün şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="48a8a-228">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-228">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-229">Dahil bir `using` deyimi (`imports` Visual Basic'te), tasarım zamanında tanınmıyor varlıkları başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="48a8a-230">Sorun: Visual Studio IntelliSense ve proje şablonları yalnızca ASP.NET MVC 3. sürüm kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="48a8a-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="48a8a-231">ASP.NET Web sayfaları yüklenmesi de araçları Visual Studio için ASP.NET Web Pages uygulamaları için IntelliSense ve proje şablonları gibi yüklemez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="48a8a-232">**Geçici çözüm** IntelliSense ve proje şablonları ASP.NET Web Pages uygulamaları Visual Studio'da kullanmak için ASP.NET MVC 3 RC Web Platformu yükleyicisi aracılığıyla yükleyin veya [tek başına yükleyici](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="48a8a-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="48a8a-233">Sorun: "&lt;Yardımcısı&gt; sınıfı bulunamıyor" hatası</span><span class="sxs-lookup"><span data-stu-id="48a8a-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="48a8a-234">Beta 3'e yükselttikten sonra bir hata görebilirsiniz, yardımcı bir sınıf (örneğin, `Facebook` sınıfı) bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="48a8a-235">Beta 2'de başlangıç ve devam etmeden Beta 3'te, açıkça yüklemeniz gereken paketleri Yardımcıları taşınmıştır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="48a8a-236">Bu paketleri dahil etmek için var olan siteler yükseltilmeden değil; Bu sitede içerir *\My Documents\IISExpress* veya *\My Documents\My Web siteleri* klasörleri.</span><span class="sxs-lookup"><span data-stu-id="48a8a-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="48a8a-237">Özellikle, varsayılan sitenin kullanıyorsanız bu hata iletisiyle karşılaşırsınız *Sitelerim* (Websitesi1), bir başvuru içeren `Twitter` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="48a8a-238">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-238">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-239">Açıklama satırı çalıştırın, sitedeki tüm yardımcıları çağrıları  *\_yönetici* sayfasında ve paket veya kullanmak istediğiniz Yardımcıları içeren paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="48a8a-240">Paketi yükledikten sonra Yardımcıları başvuran satırları açıklama durumundan çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="48a8a-241">Sorun: Bin klasörüne erişmeye Beta 3 ASP.NET Razor derlemeleri dağıtma siteleri barındırma sunucusunda çalışmıyor olabilir</span><span class="sxs-lookup"><span data-stu-id="48a8a-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="48a8a-242">Bir ASP.NET Web Pages Web sitesi barındırma bir siteye dağıtırsanız ve sitenin ASP.NET Razor Beta 3 derlemeleri dağıtırsanız *Bin* klasörü, hatalar, aşağıdakiler dahil olmak üzere karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48a8a-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="48a8a-243">Barındırma sağlayıcısı, sunucunun genel uygulama önbelleğine (GAC) ASP.NET Web sayfaları Beta 1 derlemeleri yüklediyse bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="48a8a-244">Derlemeler GAC içindeki yerel olarak yüklenen derlemeler üzerinde önceliği alma *Bin* klasör.</span><span class="sxs-lookup"><span data-stu-id="48a8a-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="48a8a-245">**Geçici çözüm** gördüğünüzü hataları sağlayıcının sürümleri arasında bir çakışma nedeniyle olduğunu onaylamak için barındırma sağlayıcınızla bağlantı kurun derlemelerin ve kullanacağınıza kendiniz karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="48a8a-246">Bu durumda, barındırma sağlayıcısı sunucunun GAC derlemelerde güncelleştirme isteği.</span><span class="sxs-lookup"><span data-stu-id="48a8a-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="48a8a-247">Sorun: Akışları okuma veya diğer dış veri bir ara sunucu aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="48a8a-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="48a8a-248">Site sunucusunu bir proxy sunucusu arkasında ise, Ara sunucu bilgileri yapılandırmanız gerekebilir *Web.config* dosyasını, site dışında geldiği bilgileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="48a8a-249">Örneğin, kullanırsanız `ReCaptcha` yardımcı, yardımcı reCAPTCHA hizmetiyle iletişim kurar, ancak proxy sunucunuz tarafından engelleniyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="48a8a-250">Benzer şekilde, Paket Yöneticisi tarafından kullanılan akış gibi ASP.NET Web sayfaları'nda kullanılan akışları proxy yapılandırma gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="48a8a-251">Bir dış hizmet çalışmaya veya akış paketi ile çalışırken sorunlarla karşılaşırsanız, aşağıdaki öğeleri, uygulamanızın kök ile put *Web.config* dosyası:</span><span class="sxs-lookup"><span data-stu-id="48a8a-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="48a8a-252">Bir proxy sunucusu yapılandırma hakkında daha fazla bilgi için bkz. [ &lt;proxy&gt; öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="48a8a-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="48a8a-253">Sorun: "Microsoft.Web.Infrastructure.dll yüklenemiyor" hatası</span><span class="sxs-lookup"><span data-stu-id="48a8a-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="48a8a-254">Daha önce Razor sözdizimi olan ASP.NET Web sayfaları, Beta 1 sürümü yüklü ve Beta 3 sürümünü yüklemeyi, tüm uygun derlemelere dışında GAC'deki yüklenir *Microsoft.Web.Infrastructure.dll*.</span><span class="sxs-lookup"><span data-stu-id="48a8a-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="48a8a-255">Sonuç olarak, ASP.NET Razor sayfaları çalıştırdığınızda bildiren bir hata görürsünüz *Microsoft.Web.Infrastructure.dll* yüklenemedi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="48a8a-256">Temiz bir bilgisayarda Beta 3 yayını yüklerse, bu sorun gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="48a8a-257">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-257">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-258">Denetim Masası'nda, ASP.NET Web Pages kaldırın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="48a8a-259">Ardından Beta 3 sürümünü yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="48a8a-260">Sorun: Razor sözdizimi olan ASP.NET Web Pages .NET Framework sürüm 4 kaldırma devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="48a8a-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="48a8a-261">.NET Framework sürüm 4 kaldırın ve daha sonra yeniden yüklerseniz, Razor sözdizimi olan ASP.NET Web sayfaları devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="48a8a-262">İle sayfaları *.cshtml* uzantısı düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="48a8a-263">ASP.NET Web sayfaları kaydeder derleme makinesi kök dizininde *Web.config* dosyasını ve .NET Framework kaldırarak bu dosyayı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="48a8a-264">.NET Framework yeniden yapılandırma dosyasının yeni bir sürümü yükler, ancak başvuru için ASP.NET Web Pages derleme eklemez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="48a8a-265">**Geçici çözüm** .NET Framework yeniden yükledikten sonra Razor sözdizimi olan ASP.NET Web sayfaları yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="48a8a-266">Bu şu öğeye ekler *Web.config* genellikle şu konumdadır makine kök dosyasında:</span><span class="sxs-lookup"><span data-stu-id="48a8a-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="48a8a-267">Sorun: Bin klasörü derlemelerde ASP.NET ile daha önce dağıttığınız uygulamaların trafiğinde yaşanan hataları</span><span class="sxs-lookup"><span data-stu-id="48a8a-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="48a8a-268">ASP.NET Web Pages derleme kopyaları, dağıtım sırasında (örneğin, *Microsoft.WebPages.dll*) için *Bin* Web sitesinin sunucusunda klasör.</span><span class="sxs-lookup"><span data-stu-id="48a8a-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="48a8a-269">(Bu otomatik olarak dağıtım sırasında durum meydana gelmiş veya Geliştirici derlemelerin açıkça kopyalanır.) Ancak, Beta 3 sürümü yüklendiğinde, hatalar oluşur, belirli türler bulunamadığı hataları gibi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="48a8a-270">Bu durum, bir ASP.NET Web Pages türlerinin sayısı Beta 3 sürümüyle farklı ad alanında taşınan kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="48a8a-271">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="48a8a-271">**Workaround** </span></span>  
> <span data-ttu-id="48a8a-272">NET *Bin* dağıtılan bir uygulama klasörü yeni derlemeleri klasöre kopyalayın (veya uygulama yeniden) ve ardından uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="48a8a-273">Sorun: Uzantısız URL'ler IIS 7 ya da IIS 7.5.cshtml/.vbhtml dosyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="48a8a-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="48a8a-274">IIS 7 veya IIS 7.5, aşağıdaki gibi bir URL isteklerle sahip sayfalar bulmak mümkün değildir *.cshtml* veya *.vbhtml* uzantısı:</span><span class="sxs-lookup"><span data-stu-id="48a8a-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="48a8a-275">URL yeniden yazma varsayılan olarak IIS 7 veya IIS 7.5 için etkin olmadığından, sorun ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="48a8a-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="48a8a-276">IIS Express kullanarak yerel olarak test ederken sorun görmüyorsanız, ancak Web sitenizi barındıran bir Web sitesine dağıttığınızda deneyimi, denetçilerinde bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="48a8a-277">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="48a8a-278">Sunucu bilgisayarı üzerinde denetime sahip olursunuz, sunucu bilgisayarda açıklanan güncelleştirmeyi yükleyin. [etkinleştirir işlemek için IIS 7.0 veya IIS 7.5 işleyicilerinin URL'leri istekleri belirli bir nokta ile bitmeyen bir güncelleştirme kullanılabilir](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="48a8a-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="48a8a-279">Sunucu bilgisayarı üzerinde denetim yoksa (örneğin, bir barındırma Web sitesine dağıtıyorsanız), Web sitenizin ekleyin *Web.config* dosyası:</span><span class="sxs-lookup"><span data-stu-id="48a8a-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="48a8a-280">Sorun: Web uygulaması projesi veya ASP.NET MVC ve ASP.NET Web sayfaları aynı uygulamada kullanma</span><span class="sxs-lookup"><span data-stu-id="48a8a-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="48a8a-281">ASP.NET Web sayfaları, bir Web uygulaması projesi ya da ASP.NET MVC uygulaması kullandıysanız, bir hata görebilirsiniz, *WebPageHttpApplication* bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="48a8a-282">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-282">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-283">Bu hata alırsanız, uygulama türetildiği temel sınıf değiştirin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="48a8a-284">İçinde *Global.asax* dosyasında, aşağıdaki satırı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="48a8a-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="48a8a-285">Şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="48a8a-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="48a8a-286">Bu uygulamada, sunulan bir değişiklik tersine çevirir Razor sözdizimi olan ASP.NET Web sayfaları, Beta 1 sürümü için.</span><span class="sxs-lookup"><span data-stu-id="48a8a-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="48a8a-287">Sorun: SQL Server yüklü Compact sahip olmayan bir bilgisayara uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="48a8a-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="48a8a-288">SQL Server Compact veritabanı içeren uygulamalar, SQL Server Compact değil yüklü olduğu bir bilgisayarda çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="48a8a-289">Microsoft WebMatrix Beta 3 otomatik olarak bu ikili dosyalar, kopyalar ve uygun gerçekleştirir *Web.config* dosya dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="48a8a-290">**Geçici çözüm** bu dosyaları kopyalayın ve gerekirse *Web.config* dosya değişikliklerini el ile şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="48a8a-291">Veritabanı altyapısı derlemeleri kopyalamak *Bin* uygulamanın hedef bilgisayardaki klasör (ve klasörleri):</span><span class="sxs-lookup"><span data-stu-id="48a8a-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="48a8a-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="48a8a-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="48a8a-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="48a8a-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="48a8a-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="48a8a-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="48a8a-295">Web sitesinin kök klasöründeki oluşturun veya açın bir *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="48a8a-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="48a8a-296">(WebMatrix Beta 3'te, bu dosya türü tıklarsanız kullanılabilir **tüm** içinde **bir dosya türünü seçin** iletişim kutusu.)</span><span class="sxs-lookup"><span data-stu-id="48a8a-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="48a8a-297">Bir alt öğesi olarak aşağıdaki öğeyi ekleyin **&lt;yapılandırma&gt;** öğesi (değilken **&lt;system.web&gt;** öğesi):</span><span class="sxs-lookup"><span data-stu-id="48a8a-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="48a8a-298">Sorun: Veritabanı ve WebGrid Yardımcıları Medium Trust Visual Basic içindeki mtm'de çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="48a8a-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="48a8a-299">Visual Basic kullanıyorsanız (oluşturma *.vbhtml* dosyaları), `Database` ve `WebGrid` uygulama Medium Trust kullanmak üzere ayarlanmışsa Yardımcıları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="48a8a-300">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-300">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-301">Tam güven kullanmak için uygulamayı geçici olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="48a8a-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="48a8a-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="48a8a-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="48a8a-303">Sorun: "Şifrele" özelliği tanınmıyor</span><span class="sxs-lookup"><span data-stu-id="48a8a-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="48a8a-304">SQL Server Compact 4.0 tanımıyor `Encrypt` özelliği `SqlCeConnection` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="48a8a-305">Veritabanı dosyaları şifrelemek için bu özelliği kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="48a8a-306">`Encrypt` Özelliği SQL Server Compact 3.5 sürümde kullanım dışı bırakıldı ve yalnızca geriye dönük uyumluluk için tutulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="48a8a-307">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-307">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-308">Kullanım `Encryption Mode` özelliği `SqlCeConnection` SQL Server Compact 4.0 veritabanı dosyaları şifrelemek için sınıf.</span><span class="sxs-lookup"><span data-stu-id="48a8a-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="48a8a-309">Aşağıdaki örnek, şifrelenmiş bir SQL Server Compact 4.0 veritabanını kullanarak oluşturma işlemi gösterilmektedir `Encryption Mode` özelliği:</span><span class="sxs-lookup"><span data-stu-id="48a8a-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="48a8a-310">Mevcut bir SQL Server Compact 4.0 veritabanı şifreleme modunu değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="48a8a-311">Şifrelenmemiş bir SQL Server Compact 4.0 veritabanı şifrelemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="48a8a-312">Sorun: Microsoft Visual C++ 2008 çalışma zamanı kitaplıkları gereklidir</span><span class="sxs-lookup"><span data-stu-id="48a8a-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="48a8a-313">Yerel DLL'leri, SQL Server Compact 4.0 Hizmet Paketi 1, Microsoft Visual C++ 2008 çalışma zamanı kitaplıkları (x 86, IA64 ve x 64) gerekir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="48a8a-314">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-314">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-315">.NET Framework 3.5 SP1 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="48a8a-316">Bu, Visual C++ 2008 çalışma zamanı kitaplıkları SP1'i de yükler.</span><span class="sxs-lookup"><span data-stu-id="48a8a-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="48a8a-317">Kitaplıklar şu konumdan indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48a8a-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="48a8a-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable paketi ATL güvenlik güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="48a8a-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="48a8a-319">Unutmayın, .NET Framework 2.0, 3.0, yükleme veya 4 mu *değil* Visual C++ 2008 çalışma zamanı kitaplıkları SP1'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="48a8a-320">Sorun: SQL Server Compact bilgisayarda .NET Framework yüklenmeden önce yüklü değilse, sağlayıcı değişmez adı .NET Framework machine.config dosyasında kayıtlı değil</span><span class="sxs-lookup"><span data-stu-id="48a8a-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="48a8a-321">SQL Server Compact, SQL Server Compact .NET framework gerektirdiği için .NET Framework yüklü olmayan bir makineye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="48a8a-322">SQL Server Compact yüklemeden önce .NET Framework sürüm 3.5 ve 4 ne yüklü ise SQL Server Compact Kurulumu sağlayıcı değişmez adını kaydetmez *machine.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="48a8a-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="48a8a-323">SQL Server Compact girişi dayanan herhangi bir uygulama *machine.config* dosyası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="48a8a-324">Değişmez adı kayıt girişi *machine.config* aşağıdaki örnek gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="48a8a-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="48a8a-325">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-325">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-326">SQL Server Compact 4.0 CTP1 kaldırın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="48a8a-327">İndirin ve tam .NET Framework sürümleri şu konumdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="48a8a-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="48a8a-328">Microsoft .NET Framework 3.5 Service pack 1 (tam paket)</span><span class="sxs-lookup"><span data-stu-id="48a8a-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="48a8a-329">Microsoft .NET Framework 4.0 sürümü (tüm paket)</span><span class="sxs-lookup"><span data-stu-id="48a8a-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="48a8a-330">Yeniden [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span><span class="sxs-lookup"><span data-stu-id="48a8a-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="48a8a-331">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="48a8a-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="48a8a-332">Sorun: Bir uygulamayı yüklemek kullanıcının Belgelerim klasöründeki bir ağ paylaşımına yönlendirilir, uzun bir zaman alabilir</span><span class="sxs-lookup"><span data-stu-id="48a8a-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="48a8a-333">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-333">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-334">Yok.</span><span class="sxs-lookup"><span data-stu-id="48a8a-334">None.</span></span> <span data-ttu-id="48a8a-335">Uygulama yüklemek için biraz sürebilir ancak düzgün yüklenecektir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="48a8a-336">Uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="48a8a-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="48a8a-337">Sorun: Site "Hedef URL'si" alanında http:// veya https:// ile eklenmedi, yayımladıktan sonra çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="48a8a-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="48a8a-338">İçinde **yayımlama ayarları** iletişim kutusunda, hedef URL ile başlamıyorsa `http://` veya `https://`, site dağıtımdan sonra çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="48a8a-339">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-339">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-340">Bir siteyi hedef URL yayımlamadan önce emin **yayımlama ayarları** iletişim kutusu ile başlayan `http://` veya `https://`.</span><span class="sxs-lookup"><span data-stu-id="48a8a-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="48a8a-341">Sorun: Bir MySQL veritabanı yayımlama "veritabanı yayımlanamadı. şu hata ile başarısız</span><span class="sxs-lookup"><span data-stu-id="48a8a-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="48a8a-342">Uzak veritabanı betiği çalıştırırsanız bu durum oluşabilir."</span><span class="sxs-lookup"><span data-stu-id="48a8a-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="48a8a-343">Hata, bir dizi nedenden ötürü ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="48a8a-344">Bu hatayı görebilirsiniz. bir veritabanı betik, tek tırnak karakterini (') içerir ve hedef MySQL veritabanının varsayılan karakter kümesini UTF-8'e değil nedenidir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="48a8a-345">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-345">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-346">Uzak bir MySQL veritabanı için UTF-8'e ayarlanmış varsayılan karakter kümesi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="48a8a-347">Diğer Sorunlar</span><span class="sxs-lookup"><span data-stu-id="48a8a-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="48a8a-348">Sorun: Arama/filtresi, Group By için raporlarda çalışmaz: Sorun türü</span><span class="sxs-lookup"><span data-stu-id="48a8a-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="48a8a-349">Çalıştırdığınızda, site için bir rapor metin girerseniz *URL'ye göre filtre* kutusuna ve tıklatın *arama*, hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="48a8a-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="48a8a-350">Bu denetim sırasında işlevsel değil olmasıdır *Group By* durumu raporu ayarlandığında *sorun türü*, varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="48a8a-351">**Geçici çözüm** içinde *Group By* sekmesi, Şerit tıklayın *URL* girişleri kendi kaynak URL'ye göre gruplandırmak için.</span><span class="sxs-lookup"><span data-stu-id="48a8a-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="48a8a-352">Bu durumda, metin kutusu ve düğme girişleri filtrelemenin işlevseldir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="48a8a-353">Sorun: IIS Express ile çalıştırmak WCF uygulamaları başarısız</span><span class="sxs-lookup"><span data-stu-id="48a8a-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="48a8a-354">Bir WCF uygulamaya göz atma aşağıdakine benzer bir hatayla sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="48a8a-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="48a8a-355">*Dosya veya derleme yüklenemedi ' Microsoft.Web.Administration, sürüm 7.0.0.0'dan, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri. Sistem belirtilen dosyayı bulamıyor.*</span><span class="sxs-lookup"><span data-stu-id="48a8a-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="48a8a-356">IIS Express Beta sürümü, varsayılan olarak WCF desteklemediğinden bu oluşur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="48a8a-357">**Geçici çözüm** aşağıdaki geçici çözümlerden birini kullanın (geçici çözüm #2 gerektiren Microsoft Windows Vista veya üzeri):</span><span class="sxs-lookup"><span data-stu-id="48a8a-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="48a8a-358">Kopyalama *Microsoft.Web.dll* ve *Microsoft.Web.Administration.dll* WebMatrix yükleme konumuna derlemelerden *bin* WCF dizin uygulama.</span><span class="sxs-lookup"><span data-stu-id="48a8a-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="48a8a-359">WebMatrix varsayılan olarak, yüklü *Microsoft WebMatrix* alt sistemin altında *Program dosyaları* klasör.</span><span class="sxs-lookup"><span data-stu-id="48a8a-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="48a8a-360">Microsoft Windows Vista veya sonraki derlemelerde için bir sembolik bağlantısını oluşturun *bin* aşağıdaki komutları kullanarak dizin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="48a8a-361">(Bu yaklaşım bir kopyasını derlemeleri oluşturmaz avantajına sahiptir.)</span><span class="sxs-lookup"><span data-stu-id="48a8a-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="48a8a-362">İki derlemenin GAC'de yükleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="48a8a-363">Yükseltilmiş bir isteminden aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="48a8a-364">Sorun: WebMatrix Beta 3 ayrıcalık gerektiren belirli görevleri gerçekleştirmek alamıyor</span><span class="sxs-lookup"><span data-stu-id="48a8a-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="48a8a-365">Aşağıdaki durumlarda ek bileşenler yükleme gibi yetki yükseltmesi gerektiren bazı görevleri gerçekleştirmek WebMatrix Beta 3'ü silemiyor:</span><span class="sxs-lookup"><span data-stu-id="48a8a-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="48a8a-366">Windows Vista veya Windows 7'de, yönetici ayrıcalıklarına sahip olmayan bir hesapla oturum günlüğe kaydedilir ve kullanıcı hesabı denetimi (UAC) devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="48a8a-367">Microsoft Windows XP veya Microsoft Windows Server 2003 kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="48a8a-368">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-368">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-369">Çoğu görevi WebMatrix Beta 3'te Yönetim iznini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="48a8a-370">Olmayanlar için yönetici olarak işlemi gerçekleştirebilir, veya bu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="48a8a-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="48a8a-371">UAC Windows Vista veya Windows 7'de etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="48a8a-372">Windows XP'de, kullanıcı Administrators güvenlik grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="48a8a-373">Sorun: "Web Galerisi sitesinden" devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="48a8a-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="48a8a-374">**Web Galerisi sitesinden** Web Platformu yükleyicisi 3.0 yüklü değilse seçeneği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="48a8a-375">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-375">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-376">Yükleme [Microsoft Web Platformu yükleyicisi 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="48a8a-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="48a8a-377">Sorun: Windows Server 2003'te, IIS Express için yönetici olmayan bir kullanıcısı başlamıyor</span><span class="sxs-lookup"><span data-stu-id="48a8a-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="48a8a-378">Bir sayfasını başlatmak veya IIS Express, Başlat, Windows Server 2003'te, IIS Express başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="48a8a-379">Web sayfaları için uygulama yönetici olmayan bir kullanıcı tarafından başlatılmış olduğunu belirten bir hata görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="48a8a-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="48a8a-380">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-380">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-381">Yönetici kullanıcı olarak WebMatrix Beta 3'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="48a8a-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="48a8a-382">Daha fazla bilgi için aşağıdaki Bilgi Bankası makalesine bakın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="48a8a-383">Yönetici olmayan bir kullanıcı tarafından başlatılan bir uygulama üzerinde uygulama Windows Vista, Windows Server 2003 veya Windows XP çalıştıran bilgisayarın HTTP trafiğini dinleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="48a8a-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="48a8a-384">Sorun: Google Chrome, bir çalıştırma seçeneği olarak kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="48a8a-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="48a8a-385">Google Chrome, tarayıcılar altında listesinde görüntülenmez **çalıştırma** üzerinde **giriş** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="48a8a-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="48a8a-386">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-386">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-387">Google Chrome'nün bazı sürümleri kendilerini doğru Windows varsayılan programlar özelliğiyle kaydetmeyin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="48a8a-388">Geçici bir çözüm olarak, Google Chrome Başlat'a tıklayın *özelleştirme ve denetim Google Chrome* menüsünde tıklatın *seçenekleri*ve ardından *yapma Google Chrome varsayılan tarayıcımda*.</span><span class="sxs-lookup"><span data-stu-id="48a8a-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="48a8a-389">Sorun: "Yabancı anahtarı" iletişim kutusu, birincil bir anahtar girilmesi izin vermez</span><span class="sxs-lookup"><span data-stu-id="48a8a-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="48a8a-390">**Yabancı anahtar** iletişim kutusu izin vermemektedir birincil anahtar tablosunda birincil anahtar adı girin.</span><span class="sxs-lookup"><span data-stu-id="48a8a-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="48a8a-391">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-391">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-392">Bu kasıtlıdır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-392">This is intentional.</span></span> <span data-ttu-id="48a8a-393">Birincil anahtar tablosundaki birincil anahtarın adını girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="48a8a-394">Sorun: "İlişkiler" düğmesini devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="48a8a-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="48a8a-395">**İlişkileri** düğmesini **tablo** sekmesinde **veritabanları** çalışma alanı, SQL Server Compact veritabanları için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="48a8a-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="48a8a-396">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-396">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-397">Yok.</span><span class="sxs-lookup"><span data-stu-id="48a8a-397">None.</span></span> <span data-ttu-id="48a8a-398">SQL Server Compact, tablolar arasında ilişki desteklemez.</span><span class="sxs-lookup"><span data-stu-id="48a8a-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="48a8a-399">Sorun: Parametrelenmiş SQL sorgularını, özel durumlar</span><span class="sxs-lookup"><span data-stu-id="48a8a-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="48a8a-400">SQL Server Compact bir veri türü gibi belirtmezseniz, 4.0, `SqlDbType` veya `DbType` sorgu çalıştırıldığında parametreli sorgular parametreleri için bir özel durum oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="48a8a-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="48a8a-401">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="48a8a-401">**Workaround**</span></span>  
> <span data-ttu-id="48a8a-402">Parametreler için veri türü gibi açıkça ayarlamak `SqlDbType` veya `DbType`.</span><span class="sxs-lookup"><span data-stu-id="48a8a-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="48a8a-403">Bu BLOB veri türleri söz konusu olduğunda önemlidir (`image` ve `ntext`).</span><span class="sxs-lookup"><span data-stu-id="48a8a-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="48a8a-404">Kod aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="48a8a-405">Daha Fazla Bilgi İçin</span><span class="sxs-lookup"><span data-stu-id="48a8a-405">For More Information</span></span>

<span data-ttu-id="48a8a-406">WebMatrix Beta 3 hakkında daha fazla bilgi için aşağıdaki Web sitelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="48a8a-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="48a8a-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="48a8a-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="48a8a-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="48a8a-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="48a8a-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="48a8a-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="48a8a-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="48a8a-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="48a8a-411">Tüm hakları saklıdır.</span><span class="sxs-lookup"><span data-stu-id="48a8a-411">All Rights Reserved.</span></span> <span data-ttu-id="48a8a-412">[Kullanım koşullarını](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="48a8a-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
