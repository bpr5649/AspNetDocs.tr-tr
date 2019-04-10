---
uid: signalr/overview/older-versions/hub-authorization
title: Kimlik doğrulama ve SignalR hub'ları için yetkilendirme (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: Bu konuda, belirli kullanıcılar ya da rolleri hub yöntemlerini erişebileceği kısıtlaması açıklar.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: af97ff2488841b2d65e50122691736603be2a686
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401419"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="3ec43-103">SignalR Hub’ları için Kimlik Doğrulaması ve Yetkilendirme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="3ec43-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="3ec43-104">tarafından [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ec43-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3ec43-105">Bu konuda, belirli kullanıcılar ya da rolleri hub yöntemlerini erişebileceği kısıtlaması açıklar.</span><span class="sxs-lookup"><span data-stu-id="3ec43-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>


## <a name="overview"></a><span data-ttu-id="3ec43-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3ec43-106">Overview</span></span>

<span data-ttu-id="3ec43-107">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="3ec43-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="3ec43-108">Öznitelik Yetkilendir</span><span class="sxs-lookup"><span data-stu-id="3ec43-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="3ec43-109">Tüm hub'ları için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="3ec43-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="3ec43-110">Özel yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="3ec43-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="3ec43-111">İstemciler için kimlik doğrulama bilgilerini geçirin</span><span class="sxs-lookup"><span data-stu-id="3ec43-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="3ec43-112">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="3ec43-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="3ec43-113">Forms kimlik doğrulaması ile tanımlama</span><span class="sxs-lookup"><span data-stu-id="3ec43-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="3ec43-114">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3ec43-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="3ec43-115">Bağlantı üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="3ec43-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="3ec43-116">Sertifika</span><span class="sxs-lookup"><span data-stu-id="3ec43-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="3ec43-117">Öznitelik Yetkilendir</span><span class="sxs-lookup"><span data-stu-id="3ec43-117">Authorize attribute</span></span>

<span data-ttu-id="3ec43-118">SignalR sağlar [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) belirli kullanıcılar ya da rolleri bir hub veya yöntem için erişimi belirtmek için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="3ec43-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="3ec43-119">Bu öznitelik bulunan `Microsoft.AspNet.SignalR` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="3ec43-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="3ec43-120">Uyguladığınız `Authorize` özniteliği bir hub'ı ya da belirli bir hub yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="3ec43-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="3ec43-121">Uyguladığınızda `Authorize` özniteliği için belirtilen kimlik doğrulama gereksinimini bir hub sınıfı, tüm hub yöntemleri için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3ec43-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="3ec43-122">Farklı türde uygulayabileceğiniz yetkilendirme gereksinimleri aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="3ec43-123">Olmadan `Authorize` özniteliği, hub'ında tüm genel yöntemleri hub'ına bağlı bir istemci için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="3ec43-124">Web uygulamanızda "Yönetici" adlı bir rol tanımladıysanız, o roldeki yalnızca kullanıcılar hub'ı aşağıdaki kod ile erişebilmesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="3ec43-125">Ya da bir hub'ı tüm kullanıcılar için kullanılabilir olan bir yöntem ve aşağıda gösterildiği gibi yalnızca kimliği doğrulanmış kullanıcılar için kullanılabilir olan ikinci bir yöntem içerdiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="3ec43-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="3ec43-126">Aşağıdaki örnekler, farklı yetkilendirme senaryosu:</span><span class="sxs-lookup"><span data-stu-id="3ec43-126">The following examples address different authorization scenarios:</span></span>

- `[Authorize]` <span data-ttu-id="3ec43-127">– yalnızca kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="3ec43-127">– only authenticated users</span></span>
- `[Authorize(Roles = "Admin,Manager")]` <span data-ttu-id="3ec43-128">– yalnızca belirtilen rollerdeki kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3ec43-128">– only authenticated users in the specified roles</span></span>
- `[Authorize(Users = "user1,user2")]` <span data-ttu-id="3ec43-129">– Belirtilen kullanıcı adları ile kullanıcıların kimlik doğrulaması yalnızca</span><span class="sxs-lookup"><span data-stu-id="3ec43-129">– only authenticated users with the specified user names</span></span>
- `[Authorize(RequireOutgoing=false)]` <span data-ttu-id="3ec43-130">– yalnızca kimliği doğrulanmış kullanıcılar hub çağırma, ancak sunucu çağrılarından istemcilerine sınırı yoktur yetkilendirme tarafından gibi diğer tüm ileti alabilir ancak yalnızca belirli kullanıcılara ileti gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-130">– only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="3ec43-131">RequireOutgoing özelliği, yalnızca kişilere yöntemleri hub'ının içinden değil, tüm hub'ına uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="3ec43-132">RequireOutgoing false olarak ayarlı değil, yalnızca kimlik doğrulama gereksinimini karşılayan kullanıcılar sunucudan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3ec43-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="3ec43-133">Tüm hub'ları için kimlik doğrulaması gerektir</span><span class="sxs-lookup"><span data-stu-id="3ec43-133">Require authentication for all hubs</span></span>

<span data-ttu-id="3ec43-134">Kimlik doğrulaması tüm hub'lara ve hub yöntemleri için uygulamanızda çağırarak gerektirebilir [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) uygulama başlatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3ec43-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="3ec43-135">Birden çok hub'ları vardır ve hepsi için bir kimlik doğrulama gereksinimini zorlamak istediğinizde bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="3ec43-136">Bu yöntemde, rol, kullanıcı veya giden yetkilendirme belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="3ec43-137">Yalnızca kimliği doğrulanmış kullanıcılara hub yöntemleri için erişim kısıtlıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="3ec43-138">Ancak, ancak yine de Authorize özniteliği hubs veya ek gereksinimleri belirtmek için yöntemleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="3ec43-139">Öznitelikleri belirttiğiniz herhangi bir gereksinim temel kimlik doğrulaması gereksinimi ek olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3ec43-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="3ec43-140">Aşağıdaki örnek, kimliği doğrulanmış kullanıcılara tüm hub yöntemleri kısıtlayan bir Global.asax dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="3ec43-141">Eğer `RequireAuthentication()` SignalR bir SignalR isteğini işlendikten sonra yöntemi oluşturur bir `InvalidOperationException` özel durum.</span><span class="sxs-lookup"><span data-stu-id="3ec43-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="3ec43-142">İşlem hattı çağrıldıktan sonra bir modül için HubPipeline eklenemiyor çünkü bu özel durum oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3ec43-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="3ec43-143">Önceki örnek arama gösterir `RequireAuthentication` yönteminde `Application_Start` yönteminin, ilk isteği işleme önce bir kez yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3ec43-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="3ec43-144">Özel yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="3ec43-144">Customized authorization</span></span>

<span data-ttu-id="3ec43-145">Yetkilendirme nasıl belirlendiğini özelleştirmek ihtiyacınız varsa, türetilen bir sınıf oluşturabilirsiniz `AuthorizeAttribute` ve geçersiz kılma [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3ec43-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="3ec43-146">Bu yöntem, kullanıcı isteği tamamlamak için yetki verilip verilmediğini belirlemek üzere her istek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3ec43-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="3ec43-147">Geçersiz kılınan yönteminde yetkilendirme senaryonuz için gerekli mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ec43-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="3ec43-148">Aşağıdaki örnek, yetkilendirme aracılığıyla beyana dayalı kimlik uygulamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="3ec43-149">İstemciler için kimlik doğrulama bilgilerini geçirin</span><span class="sxs-lookup"><span data-stu-id="3ec43-149">Pass authentication information to clients</span></span>

<span data-ttu-id="3ec43-150">İstemcide çalışan kod, kimlik doğrulama bilgilerini kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="3ec43-151">Gerekli bilgileri, istemcide yöntemleri çağrılırken geçirin.</span><span class="sxs-lookup"><span data-stu-id="3ec43-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="3ec43-152">Örneğin, bir sohbet uygulaması yöntem parametre olarak bir ileti gönderen kişinin kullanıcı adı aşağıda gösterildiği gibi geçirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="3ec43-153">Veya, aşağıda gösterildiği gibi kimlik doğrulama bilgilerini temsil eder ve o nesnenin bir parametre olarak geçirmek için bir nesne oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="3ec43-154">Kötü niyetli bir kullanıcı bu istemciden gelen istek taklit etmek için kullanabilir gibi diğer istemcilere hiçbir zaman bir istemcinin bağlantı kimliği göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="3ec43-155">.NET istemcileri için kimlik doğrulama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="3ec43-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="3ec43-156">Kimliği doğrulanmış kullanıcılara sınırlı bir hub ile etkileşime giren, bir konsol uygulaması gibi bir .NET istemcisi olduğunda, kimlik doğrulama bilgileri bir tanımlama bilgisi, bağlantı üst bilgi veya bir sertifika geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="3ec43-157">Bu bölümdeki örneklerde, bir kullanıcı kimlik doğrulaması için bu farklı yöntemleri kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="3ec43-158">SignalR tam işlevsel uygulamaları değiller.</span><span class="sxs-lookup"><span data-stu-id="3ec43-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="3ec43-159">SignalR ile .NET istemcileri hakkında daha fazla bilgi için bkz: [Hubs API Kılavuzu - .NET istemcisi](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="3ec43-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="3ec43-160">Tanımlama bilgisi</span><span class="sxs-lookup"><span data-stu-id="3ec43-160">Cookie</span></span>

<span data-ttu-id="3ec43-161">.NET istemci ASP.NET formları kimlik doğrulamasını kullanan bir hub ile etkileşim kurduğunda, kimlik doğrulama tanımlama bağlantıda el ile ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="3ec43-162">Tanımlama bilgisinin eklediğiniz `CookieContainer` özelliği [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) nesne.</span><span class="sxs-lookup"><span data-stu-id="3ec43-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="3ec43-163">Aşağıdaki örnek, bir web sayfasından bir kimlik doğrulama tanımlama bilgisi alır ve bağlantı konusu tanımlama bilgisine ekler bir konsol uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="3ec43-164">URL `https://www.contoso.com/RemoteLogin` örnek işaret oluşturmak için gereken bir web sayfası.</span><span class="sxs-lookup"><span data-stu-id="3ec43-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="3ec43-165">Sayfa gönderilen kullanıcı adını ve parolasını almak ve kullanıcı kimlik bilgileriyle oturum dener.</span><span class="sxs-lookup"><span data-stu-id="3ec43-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="3ec43-166">Konsol uygulaması için kimlik bilgilerini, aşağıdaki arka plan kod dosyasını içeren boş bir sayfa başvurabileceğiniz www.contoso.com/RemoteLogin gönderir.</span><span class="sxs-lookup"><span data-stu-id="3ec43-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="3ec43-167">Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3ec43-167">Windows authentication</span></span>

<span data-ttu-id="3ec43-168">Windows kimlik doğrulaması kullanırken, geçerli kullanıcının kimlik bilgilerini kullanarak geçirebilirsiniz [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="3ec43-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="3ec43-169">Bağlantı için kimlik bilgilerini DefaultCredentials değerine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3ec43-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="3ec43-170">Bağlantı üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="3ec43-170">Connection header</span></span>

<span data-ttu-id="3ec43-171">Uygulamanızı tanımlama bilgilerini kullanmıyorsa, kullanıcı bilgilerini bağlantı üstbilgisinde geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="3ec43-172">Örneğin, bir belirteç bağlantı üstbilgisinde geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="3ec43-173">Ardından, hub'ında kullanıcı belirteci doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="3ec43-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="3ec43-174">Sertifika</span><span class="sxs-lookup"><span data-stu-id="3ec43-174">Certificate</span></span>

<span data-ttu-id="3ec43-175">Kullanıcıyı doğrulamak için bir istemci sertifikası geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ec43-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="3ec43-176">Sertifika, bağlantı oluştururken ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3ec43-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="3ec43-177">Aşağıdaki örnek, bir istemci sertifikası bağlantısı eklemek yalnızca nasıl gösterir; tam bir konsol uygulaması göstermez.</span><span class="sxs-lookup"><span data-stu-id="3ec43-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="3ec43-178">Kullandığı [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) sertifikayı oluşturmak için çeşitli yollar sağlar sınıfını.</span><span class="sxs-lookup"><span data-stu-id="3ec43-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
