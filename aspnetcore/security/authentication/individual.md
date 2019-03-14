---
title: Bireysel kullanıcı hesapları ile oluşturulan ASP.NET Core projeleri göre makaleler
author: rick-anderson
description: Bireysel kullanıcı hesapları ile oluşturulan ASP.NET Core projeleri göre makaleleri keşfedin.
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: c73365eafaf2c38ef02c3c83ccf5ced4264f7dc0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068772"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a><span data-ttu-id="ec231-103">Bireysel kullanıcı hesapları ile oluşturulan ASP.NET Core projeleri göre makaleler</span><span class="sxs-lookup"><span data-stu-id="ec231-103">Articles based on ASP.NET Core projects created with individual user accounts</span></span>

<span data-ttu-id="ec231-104">ASP.NET Core kimliği "Bireysel kullanıcı hesapları" seçeneği ile Visual Studio Proje şablonları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="ec231-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="ec231-105">.NET Core CLI ile kimlik doğrulaması şablonlar kullanılabilir `-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="ec231-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapp -au Individual
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new razor -au Individual
```

::: moniker-end

<span data-ttu-id="ec231-106">Bkz: [bu GitHub sorunu](https://github.com/aspnet/AspNetCore/issues/5833) web API'si kimlik doğrulama için.</span><span class="sxs-lookup"><span data-stu-id="ec231-106">See [this GitHub issue](https://github.com/aspnet/AspNetCore/issues/5833) for web API authentication.</span></span>

<a name="no"></a>
## <a name="no-authentication"></a><span data-ttu-id="ec231-107">Kimlik doğrulama yok</span><span class="sxs-lookup"><span data-stu-id="ec231-107">No Authentication</span></span>

<span data-ttu-id="ec231-108">Kimlik doğrulaması ile .NET Core CLI belirtilen `-au` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ec231-108">Authentication is specified in the .NET Core CLI with the `-au` option.</span></span> <span data-ttu-id="ec231-109">Visual Studio'da **kimlik doğrulamayı Değiştir** iletişim yeni web uygulamaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec231-109">In Visual Studio, the **Change Authentication** dialog is available for new web applications.</span></span> <span data-ttu-id="ec231-110">Visual Studio'da yeni web uygulamaları için varsayılan değer **kimlik doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="ec231-110">The default for new web apps in Visual Studio is **No Authentication**.</span></span>

<span data-ttu-id="ec231-111">Kimlik doğrulama olmadan oluşturulan projeleri:</span><span class="sxs-lookup"><span data-stu-id="ec231-111">Projects created with no authentication:</span></span>

* <span data-ttu-id="ec231-112">Web sayfaları ve oturum açın ve oturum kapatma UI içermez.</span><span class="sxs-lookup"><span data-stu-id="ec231-112">Don't contain web pages and UI to sign in and sign out.</span></span>
* <span data-ttu-id="ec231-113">Kimlik doğrulama kodu içermez.</span><span class="sxs-lookup"><span data-stu-id="ec231-113">Don't contain authentication code.</span></span>

<a name="win"></a>
## <a name="windows-authentication"></a><span data-ttu-id="ec231-114">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ec231-114">Windows Authentication</span></span>

<span data-ttu-id="ec231-115">Windows kimlik doğrulaması için yeni web apps ile .NET Core CLI belirtildiği `-au Windows` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ec231-115">Windows Authentication is specified for new web apps in the .NET Core CLI with the `-au Windows` option.</span></span> <span data-ttu-id="ec231-116">Visual Studio'da **kimlik doğrulamayı Değiştir** iletişim kutusu sunar **Windows kimlik doğrulaması** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="ec231-116">In Visual Studio, the **Change Authentication** dialog provides the **Windows Authentication** options.</span></span>

<span data-ttu-id="ec231-117">Windows kimlik doğrulamasını seçerseniz, uygulamayı kullanmak üzere yapılandırılmış [Windows kimlik doğrulaması IIS Modülü](xref:host-and-deploy/iis/modules).</span><span class="sxs-lookup"><span data-stu-id="ec231-117">If Windows Authentication is selected, the app is configured to use the [Windows Authentication IIS module](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="ec231-118">Windows kimlik doğrulaması, Intranet web siteleri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec231-118">Windows Authentication is intended for Intranet web sites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec231-119">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec231-119">Additional resources</span></span>

<span data-ttu-id="ec231-120">Aşağıdaki makaleler, bireysel kullanıcı hesapları kullanan ASP.NET Core şablonları oluşturulan kodu kullanmayı göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="ec231-120">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="ec231-121">SMS ile iki öğeli kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="ec231-121">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="ec231-122">Hesap onaylama ve parola kurtarma ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ec231-122">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="ec231-123">Kullanıcı verilerinin yetkilendirme tarafından korunduğu ile bir ASP.NET Core uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec231-123">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
