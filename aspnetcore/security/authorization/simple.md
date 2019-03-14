---
title: ASP.NET core'da basit yetkilendirme
author: rick-anderson
description: Authorize özniteliği için ASP.NET Core denetleyicilere ve eylemlere erişimi kısıtlamak için kullanmayı öğrenin.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/simple
ms.openlocfilehash: 6409def0508b855d3d2a4a1f4d3a3d15bfe5dd32
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073848"
---
# <a name="simple-authorization-in-aspnet-core"></a><span data-ttu-id="15c29-103">ASP.NET core'da basit yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="15c29-103">Simple authorization in ASP.NET Core</span></span>

<a name="security-authorization-simple"></a>

<span data-ttu-id="15c29-104">Yetkilendirme mvc'de aracılığıyla denetlenebilir `AuthorizeAttribute` özniteliği ve çeşitli parametreleri.</span><span class="sxs-lookup"><span data-stu-id="15c29-104">Authorization in MVC is controlled through the `AuthorizeAttribute` attribute and its various parameters.</span></span> <span data-ttu-id="15c29-105">En basit şekliyle, uygulama `AuthorizeAttribute` denetleyici veya eylem erişimi denetleyiciye veya eylem kimliği doğrulanan kullanıcı için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="15c29-105">At its simplest, applying the `AuthorizeAttribute` attribute to a controller or action limits access to the controller or action to any authenticated user.</span></span>

<span data-ttu-id="15c29-106">Örneğin, aşağıdaki kod erişimi sınırlar `AccountController` herhangi bir kimliği doğrulanmış kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="15c29-106">For example, the following code limits access to the `AccountController` to any authenticated user.</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="15c29-107">Yetkilendirme denetleyicisi yerine bir eylemi uygulamak istiyorsanız, geçerli `AuthorizeAttribute` özniteliği eylem için:</span><span class="sxs-lookup"><span data-stu-id="15c29-107">If you want to apply authorization to an action rather than the controller, apply the `AuthorizeAttribute` attribute to the action itself:</span></span>

```csharp
public class AccountController : Controller
{
   public ActionResult Login()
   {
   }

   [Authorize]
   public ActionResult Logout()
   {
   }
}
```

<span data-ttu-id="15c29-108">Yalnızca kimliği doğrulanmış kullanıcıların artık `Logout` işlevi.</span><span class="sxs-lookup"><span data-stu-id="15c29-108">Now only authenticated users can access the `Logout` function.</span></span>

<span data-ttu-id="15c29-109">Ayrıca `AllowAnonymous` bireysel işlemlere doğrulanmamış kullanıcılar tarafından erişime izin vermek için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="15c29-109">You can also use the `AllowAnonymous` attribute to allow access by non-authenticated users to individual actions.</span></span> <span data-ttu-id="15c29-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="15c29-110">For example:</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    [AllowAnonymous]
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="15c29-111">Bu yalnızca kimliği doğrulanmış kullanıcılara izin `AccountController`, dışında `Login` kimliği doğrulanmış veya kimliği doğrulanmamış / anonim durumlarını bağımsız olarak herkes tarafından erişilebilir olan bir eylem.</span><span class="sxs-lookup"><span data-stu-id="15c29-111">This would allow only authenticated users to the `AccountController`, except for the `Login` action, which is accessible by everyone, regardless of their authenticated or unauthenticated / anonymous status.</span></span>

> [!WARNING]
> <span data-ttu-id="15c29-112">`[AllowAnonymous]` Tüm Yetkilendirme deyimleri atlar.</span><span class="sxs-lookup"><span data-stu-id="15c29-112">`[AllowAnonymous]` bypasses all authorization statements.</span></span> <span data-ttu-id="15c29-113">Birleştirirseniz `[AllowAnonymous]` ve tüm `[Authorize]` özniteliği `[Authorize]` öznitelikleri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="15c29-113">If you combine `[AllowAnonymous]` and any `[Authorize]` attribute, the `[Authorize]` attributes are ignored.</span></span> <span data-ttu-id="15c29-114">Örneğin, uygulamanızı `[AllowAnonymous]` denetleyici düzeyinde herhangi `[Authorize]` öznitelikleri aynı denetleyicisine (veya içindeki herhangi bir eylem) göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="15c29-114">For example if you apply `[AllowAnonymous]` at the controller level, any `[Authorize]` attributes on the same controller (or on any action within it) is ignored.</span></span>
