---
title: ASP.NET Core ile React-ile-Redux proje şablonu kullanın
author: SteveSandersonMS
description: React ile Redux ve oluşturma-react-uygulama için ASP.NET Core tek sayfa uygulama (SPA) proje şablonu ile çalışmaya başlama hakkında bilgi edinin.
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/13/2019
uid: spa/react-with-redux
ms.openlocfilehash: ed2e9aea449ddb09fef049a391f40f57452786a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067164"
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a><span data-ttu-id="e74ac-103">ASP.NET Core ile React-ile-Redux proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="e74ac-103">Use the React-with-Redux project template with ASP.NET Core</span></span>

<span data-ttu-id="e74ac-104">Güncelleştirilmiş Redux ile React proje şablonu kullanarak ASP.NET Core uygulamaları, React Redux, uygun bir başlama noktası sağlar ve [oluşturma-react-app](https://github.com/facebookincubator/create-react-app) (CRA) kuralları, istemci tarafı zengin kullanıcı arabirimi (UI) uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="e74ac-104">The updated React-with-Redux project template provides a convenient starting point for ASP.NET Core apps using React, Redux, and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="e74ac-105">Proje oluşturma komutuna dışında React-ile-Redux şablonu hakkındaki tüm bilgileri React şablonu ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="e74ac-105">With the exception of the project creation command, all information about the React-with-Redux template is the same as the React template.</span></span> <span data-ttu-id="e74ac-106">Bu proje türü oluşturmak için çalıştırılması `dotnet new reactredux` yerine `dotnet new react`.</span><span class="sxs-lookup"><span data-stu-id="e74ac-106">To create this project type, run `dotnet new reactredux` instead of `dotnet new react`.</span></span> <span data-ttu-id="e74ac-107">Her iki React tabanlı şablonlar için ortak olan işlevselliği hakkında daha fazla bilgi için bkz: [React şablon belgeleri](xref:spa/react).</span><span class="sxs-lookup"><span data-stu-id="e74ac-107">For more information about the functionality common to both React-based templates, see [React template documentation](xref:spa/react).</span></span>

<span data-ttu-id="e74ac-108">IIS React-ile-Redux bir alt uygulama yapılandırma hakkında daha fazla bilgi için bkz: [açarken kilitlenmesi şablon 2.1: IIS üzerinde SPA kullanılamıyor (aspnet/şablon &num;555)](https://github.com/aspnet/Templating/issues/555).</span><span class="sxs-lookup"><span data-stu-id="e74ac-108">For information on configuring a React-with-Redux sub-application in IIS, see [ReactRedux Template 2.1: Unable to use SPA on IIS (aspnet/Templating &num;555)](https://github.com/aspnet/Templating/issues/555).</span></span>
