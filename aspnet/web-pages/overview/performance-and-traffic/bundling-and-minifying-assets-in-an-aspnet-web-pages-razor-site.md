---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET Web Sayfaları (Jilet) Sitesinde Varlıkları Birleştirme ve Minifying | Microsoft Dokümanlar
author: rick-anderson
description: Bundling ve minification sitenizi daha hızlı hale getirmenin yollarıdır. Bundling birden fazla JavaScript ( .js ) dosyaları veya birden çok basamaklı stil sayfası (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539937"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="78b84-104">ASP.NET Web Sayfaları (Razor) Sitesinde Varlıkları Paketleme ve Küçültme</span><span class="sxs-lookup"><span data-stu-id="78b84-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="78b84-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="78b84-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="78b84-106">Bundling ve minification sitenizi daha hızlı hale getirmenin yollarıdır.</span><span class="sxs-lookup"><span data-stu-id="78b84-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="78b84-107">Bundling, birden çok JavaScript (*.js*) dosyasını veya birden çok basamaklı stil sayfasını *(.css)* birleştirerek birbirim olarak indirilebilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="78b84-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="78b84-108">Minification beyaz boşluğu sıkıştırır ve indirilen dosyaları mümkün olduğunca küçük hale getirmek için diğer sıkıştırma türlerini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="78b84-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="78b84-109">Web Sayfalarını 2 ASP.NET RC sürümü, gerekli öğeleri içeren paket henüz Microsoft WebMatrix'te kullanılamadığından birleştirme ve çıkarma yı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="78b84-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="78b84-110">Bu rahatsızlıktan dolayı özür dileriz.</span><span class="sxs-lookup"><span data-stu-id="78b84-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="78b84-111">Paketin ASP.NET Web Sayfaları 2 ve WebMatrix 2'nin son sürümünde bulunması beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="78b84-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
