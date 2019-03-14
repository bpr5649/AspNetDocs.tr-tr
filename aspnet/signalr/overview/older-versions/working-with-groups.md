---
uid: signalr/overview/older-versions/working-with-groups
title: Signalr'da gruplarla çalışma 1.x | Microsoft Docs
author: bradygaster
description: Bu konu, grup üyeliği bilgileri Hub API'si ile kalıcı hale getirmek açıklar.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: e8ef7b34af4341fb97f54e2aab1d8971cce46af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066693"
---
<a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="7e9a6-103">SignalR 1.x Sürümünde Gruplarla Çalışma</span><span class="sxs-lookup"><span data-stu-id="7e9a6-103">Working with Groups in SignalR 1.x</span></span>
====================
<span data-ttu-id="7e9a6-104">tarafından [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7e9a6-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="7e9a6-105">Bu konuda, kullanıcı gruplarına ekleyin ve grup üyeliği bilgileri kalıcı açıklar.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-105">This topic describes how to add users to groups and persist group membership information.</span></span>


## <a name="overview"></a><span data-ttu-id="7e9a6-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7e9a6-106">Overview</span></span>

<span data-ttu-id="7e9a6-107">Signalr'da gruplarla, bağlı istemciler belirtilen alt kümelerine yayın iletileri için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="7e9a6-108">Bir grupta herhangi bir sayıda istemciler olabilir ve istemci grupları herhangi bir sayıda üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="7e9a6-109">Açıkça grupları oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="7e9a6-110">Aslında, bir grup otomatik olarak ilk kez bir çağrıda Groups.Add adını belirleyin oluşturulur ve bu üyelik son bağlantı kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="7e9a6-111">Grupları kullanarak bir giriş için bkz. [Hub sınıftan grup üyeliğini yönetme](index.md) Hubs API - Server Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="7e9a6-112">Bir grup üyeliği listesinin veya grupların listesini almak için hiçbir API yoktur.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="7e9a6-113">SignalR istemcisi ve yayımlama/abonelik modelini temel alan grubu iletileri gönderir ve sunucu grupları veya grup üyeliklerinin listesi korumaz.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="7e9a6-114">Bir web grubu için bir düğüm eklediğinizde, yeni bir düğüme dağıtılmasını SignalR tutar herhangi bir durum olduğundan bu ölçeklenebilirliği en üst düzeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="7e9a6-115">Kullanarak bir grup kullanıcı eklediğinizde `Groups.Add` yöntemi, kullanıcının geçerli bağlantının süresi boyunca bu gruba yönlendirilmiş iletileri alır, ancak kullanıcının üyelik o gruptaki geçerli bağlantı kalıcı değil.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="7e9a6-116">Gruplar ve grup üyeliği bilgileri kalıcı olarak tutmak istiyorsanız, bir veritabanı veya Azure tablo depolama gibi bir depoda bu verileri saklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="7e9a6-117">Ardından, bir kullanıcı uygulamanıza her bağlandığında, depodan kullanıcının ait olduğu grupları almak ve bu kullanıcı için bu grupları el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="7e9a6-118">Sonra geçici bir kesinti bağlanırken, kullanıcı otomatik olarak daha önce atanan gruplar yeniden birleştirir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="7e9a6-119">Otomatik olarak bir grup aşamalarını yalnızca yeniden bağlanma, yeni bir bağlantı kurmadan olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="7e9a6-120">Dijital olarak imzalanmış bir belirteç, daha önce atanan gruplar listesini içeren istemciden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="7e9a6-121">Kullanıcının istenen gruplara ait olup olmadığını doğrulamak istiyorsanız, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="7e9a6-122">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="7e9a6-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="7e9a6-123">Ekleme ve kullanıcıları kaldırma</span><span class="sxs-lookup"><span data-stu-id="7e9a6-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="7e9a6-124">Bir grubun üyeleri çağırma</span><span class="sxs-lookup"><span data-stu-id="7e9a6-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="7e9a6-125">Grup üyeliği veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="7e9a6-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="7e9a6-126">Azure tablo depolama grup üyeliği</span><span class="sxs-lookup"><span data-stu-id="7e9a6-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="7e9a6-127">Grup üyeliği bağlanırken doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="7e9a6-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="7e9a6-128">Ekleme ve kullanıcıları kaldırma</span><span class="sxs-lookup"><span data-stu-id="7e9a6-128">Adding and removing users</span></span>

<span data-ttu-id="7e9a6-129">Eklemek veya gruptan kullanıcılar kaldırmak için çağrı [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) veya [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemleri ve kullanıcının bağlantı kimliği ve grubun adını parametreler olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="7e9a6-130">El ile bağlantı sona erdiğinde bir kullanıcıyı bir gruptan kaldırmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="7e9a6-131">Aşağıdaki örnekte gösterildiği `Groups.Add` ve `Groups.Remove` Hub yöntemlerinde kullanılan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="7e9a6-132">`Groups.Add` Ve `Groups.Remove` zaman uyumsuz bir yöntem yürütülemez.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="7e9a6-133">Bir istemci bir gruba ekleyin ve hemen bir ileti grubunu kullanarak istemciye göndermek istiyorsanız, Groups.Add yöntemin ilk sonlandırdığından emin yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="7e9a6-134">Aşağıdaki kod örnekleri, .NET 4.5 ve .NET 4'te çalışan kod kullanarak bir tane çalışan kod kullanarak bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="7e9a6-135">Zaman uyumsuz .NET 4.5 örneği</span><span class="sxs-lookup"><span data-stu-id="7e9a6-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="7e9a6-136">Zaman uyumsuz .NET 4 örneği</span><span class="sxs-lookup"><span data-stu-id="7e9a6-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="7e9a6-137">Genel olarak, dahil `await` çağırırken `Groups.Remove` yöntemi kaldırmaya çalıştığınız bağlantı kimliği artık kullanılabilir olabileceğinden.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="7e9a6-138">Bu durumda, `TaskCanceledException` istek zaman aşımına sonra oluşturulur. Ekleyebileceğiniz uygulamanızı gruba bir ileti göndermeden önce kullanıcının gruptan kaldırıldığından emin olmanız gerekir, `await` Groups.Remove ve ardından catch önce `TaskCanceledException` oluşturulabilecek özel durum.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="7e9a6-139">Bir grubun üyeleri çağırma</span><span class="sxs-lookup"><span data-stu-id="7e9a6-139">Calling members of a group</span></span>

<span data-ttu-id="7e9a6-140">İleti tümünün bir grubun üyesi ya da yalnızca belirtilen grup üyeleri için aşağıdaki örneklerde gösterildiği gibi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="7e9a6-141">**Tüm** bağlı istemciler belirtilen grubunda.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="7e9a6-142">Bağlı olan tüm istemciler belirtilen gruptaki **dışındaki belirtilen istemcilerin**, belirtilen bağlantı kimliğine göre</span><span class="sxs-lookup"><span data-stu-id="7e9a6-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="7e9a6-143">Bağlı olan tüm istemciler belirtilen gruptaki **çağıran istemci dışındaki**.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="7e9a6-144">Grup üyeliği veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="7e9a6-144">Storing group membership in a database</span></span>

<span data-ttu-id="7e9a6-145">Aşağıdaki örnekler, Grup ve kullanıcı bilgileri bir veritabanında saklamanın gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="7e9a6-146">Tüm veri erişim teknolojisi kullanabilirsiniz; Ancak, aşağıdaki örnekte, Entity Framework kullanarak modelleri tanımlamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="7e9a6-147">Bu varlık modeli, veritabanı tabloları ve alanları karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="7e9a6-148">Data yapınız, uygulama gereksinimlerine bağlı olarak önemli ölçüde değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="7e9a6-149">Bu örnek adlı bir sınıf içerir `ConversationRoom` kullanıcıların spor veya bahçesi oluşturma gibi farklı konularla ilgili konuşmaları katılmasına sağlayan bir uygulama için benzersiz olacak.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="7e9a6-150">Bu örnek ayrıca bağlantılar için bir sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="7e9a6-151">Bağlantı sınıfı grup üyeliği izlemek için gerekli değildir, ancak kullanıcılar izleme için sağlam bir çözüm sık parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="7e9a6-152">Ardından, hub'ında grubu ve kullanıcı bilgilerini veritabanından ve el ile kullanıcı uygun gruplara ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="7e9a6-153">Örneğin, kullanıcı bağlantıları izlemek için kod içermez.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="7e9a6-154">Bu örnekte, `await` önce anahtar sözcüğü uygulanmaz `Groups.Add` çünkü bir ileti grubunun üyelerine hemen gönderilmez.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="7e9a6-155">Yeni üye hemen ekledikten sonra grubun tüm üyeleri için bir ileti göndermek istiyorsanız, uygulamak ister `await` zaman uyumsuz işlemi tamamlandı emin olmak için anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="7e9a6-156">Azure tablo depolama grup üyeliği</span><span class="sxs-lookup"><span data-stu-id="7e9a6-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="7e9a6-157">Grup ve kullanıcı bilgilerini depolamak için Azure tablo depolaması'nı kullanarak, bir veritabanı kullanmaya benzer.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="7e9a6-158">Aşağıdaki örnek, kullanıcı adı ve grup adı depolayan bir tablo varlığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="7e9a6-159">Hub'ında kullanıcı bağlandığında atanan grupları alır.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="7e9a6-160">Grup üyeliği bağlanırken doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="7e9a6-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="7e9a6-161">Varsayılan olarak, SignalR otomatik olarak bir kullanıcı uygun gruplara ne zaman bir bağlantı bırakılan ve bağlantı zaman aşımına uğramadan önce yeniden oluşturulan gibi geçici bir kesintisinden bağlanırken yeniden atar. Kullanıcı grubu bilgileri bağlanırken bir belirteç geçirilir ve bu belirteci, sunucu üzerinde doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="7e9a6-162">Kullanıcı gruplarına yeniden katılma için doğrulama işlemi hakkında daha fazla bilgi için bkz. [grupları bağlanırken aşamalarını](index.md).</span><span class="sxs-lookup"><span data-stu-id="7e9a6-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="7e9a6-163">Genel olarak, otomatik olarak gruplara yeniden aşamalarını varsayılan davranışını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="7e9a6-164">SignalR grupları hassas verilere erişimi kısıtlamak için bir güvenlik mekanizması olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="7e9a6-165">Ancak, uygulamanızın bir kullanıcının grup üyeliğine bağlanırken denetleyin, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="7e9a6-166">Bir kullanıcının grup üyeliğine her yeniden bağlantı yerine yalnızca kullanıcı bağlandığında alınması gerektiğinden varsayılan davranışını değiştirme veritabanınız için bir yük ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="7e9a6-167">Grup üyeliği doğrulamanız gerekir yeniden, aşağıda gösterildiği gibi atanan gruplarının bir listesini döndüren yeni bir hub işlem hattı modül oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="7e9a6-168">Ardından, bu modül aşağıda vurgulandığı gibi hub ardışık düzenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e9a6-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
