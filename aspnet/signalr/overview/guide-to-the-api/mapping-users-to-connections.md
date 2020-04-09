---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR Kullanıcılarını Bağlantılara Haritalama | Microsoft Dokümanlar
author: bradygaster
description: Bu konu, kullanıcılar ve bağlantıları hakkında nasıl bilgi saklarıkları gösterir. Patrick Fletcher bu konunun yazılmasına yardımcı oldu. Bu konuda kullanılan yazılım sürümleri...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676162"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="e340d-105">SignalR Kullanıcılarını Bağlantılarla Eşleme</span><span class="sxs-lookup"><span data-stu-id="e340d-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="e340d-106"> yazan: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e340d-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e340d-107">Bu konu, kullanıcılar ve bağlantıları hakkında nasıl bilgi saklarıkları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="e340d-108">Patrick Fletcher bu konunun yazılmasına yardımcı oldu.</span><span class="sxs-lookup"><span data-stu-id="e340d-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="e340d-109">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="e340d-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="e340d-110">Görsel Stüdyo 2013</span><span class="sxs-lookup"><span data-stu-id="e340d-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="e340d-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e340d-111">.NET 4.5</span></span>
> - <span data-ttu-id="e340d-112">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="e340d-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="e340d-113">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="e340d-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="e340d-114">SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e340d-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="e340d-115">Sorular ve yorumlar</span><span class="sxs-lookup"><span data-stu-id="e340d-115">Questions and comments</span></span>
>
> <span data-ttu-id="e340d-116">Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın.</span><span class="sxs-lookup"><span data-stu-id="e340d-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e340d-117">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e340d-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="e340d-118">Giriş</span><span class="sxs-lookup"><span data-stu-id="e340d-118">Introduction</span></span>

<span data-ttu-id="e340d-119">Bir hub'a bağlanan her istemci benzersiz bir bağlantı kimliği geçirir. Bu değeri hub bağlamının `Context.ConnectionId` özelliğinde alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e340d-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="e340d-120">Uygulamanızın bir kullanıcıyı bağlantı kimliğiyle eşlemesi ve bu eşlemayı devam etmesi gerekiyorsa, aşağıdakilerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e340d-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="e340d-121">Kullanıcı Kimliği Sağlayıcısı (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="e340d-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="e340d-122">Sözlük gibi [bellek içi depolama](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="e340d-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="e340d-123">Her kullanıcı için SignalR grubu</span><span class="sxs-lookup"><span data-stu-id="e340d-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="e340d-124">Veritabanı tablosu veya Azure tablo depolama gibi [kalıcı, harici depolama](#database)</span><span class="sxs-lookup"><span data-stu-id="e340d-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="e340d-125">Bu uygulamaların her biri bu konuda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="e340d-126">Kullanıcı bağlantı `OnConnected` `OnDisconnected`durumunu `OnReconnected` izlemek için `Hub` sınıfın , ve yöntemlerini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e340d-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="e340d-127">Uygulamanız için en iyi yaklaşım şuna bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="e340d-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="e340d-128">Uygulamanızı barındıran web sunucularının sayısı.</span><span class="sxs-lookup"><span data-stu-id="e340d-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="e340d-129">Şu anda bağlı olan kullanıcıların listesini almanız gerekip gerekmediği.</span><span class="sxs-lookup"><span data-stu-id="e340d-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="e340d-130">Uygulama veya sunucu yeniden başlatıldığında grup ve kullanıcı bilgilerini devam ettirebilmeniz gerekip gerekmediği.</span><span class="sxs-lookup"><span data-stu-id="e340d-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="e340d-131">Harici bir sunucuarama nın gecikmesinin bir sorun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="e340d-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="e340d-132">Aşağıdaki tabloda, bu hususlar için hangi yaklaşımın işe yaradığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e340d-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="e340d-133">Birden fazla sunucu</span><span class="sxs-lookup"><span data-stu-id="e340d-133">More than one server</span></span> | <span data-ttu-id="e340d-134">Şu anda bağlı olan kullanıcıların listesini alma</span><span class="sxs-lookup"><span data-stu-id="e340d-134">Get list of currently connected users</span></span> | <span data-ttu-id="e340d-135">Yeniden başlatıldıktan sonra bilgileri devam etti</span><span class="sxs-lookup"><span data-stu-id="e340d-135">Persist information after restarts</span></span> | <span data-ttu-id="e340d-136">Optimum performans</span><span class="sxs-lookup"><span data-stu-id="e340d-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e340d-137">UserID Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e340d-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="e340d-138">Bellek içi</span><span class="sxs-lookup"><span data-stu-id="e340d-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="e340d-139">Tek kullanıcılı gruplar</span><span class="sxs-lookup"><span data-stu-id="e340d-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="e340d-140">Kalıcı, dış</span><span class="sxs-lookup"><span data-stu-id="e340d-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="e340d-141">IUserID sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e340d-141">IUserID provider</span></span>

<span data-ttu-id="e340d-142">Bu özellik, kullanıcıların yeni bir arayüz iUserIdProvider üzerinden bir IRequest'e dayalı kullanıcı Kimliği'nin ne olduğunu belirtmelerine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e340d-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="e340d-143">**IUseridSağlayıcı**</span><span class="sxs-lookup"><span data-stu-id="e340d-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="e340d-144">Varsayılan olarak, kullanıcı adı olarak kullanıcının `IPrincipal.Identity.Name` kullanan bir uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e340d-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="e340d-145">Bunu değiştirmek için, uygulamanız başladığında uygulamanızı genel ana `IUserIdProvider` bilgisayara kaydedin:</span><span class="sxs-lookup"><span data-stu-id="e340d-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="e340d-146">Bir hub içinden, aşağıdaki API üzerinden bu kullanıcılara ileti gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e340d-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="e340d-147">**Belirli bir kullanıcıya ileti gönderme**</span><span class="sxs-lookup"><span data-stu-id="e340d-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="e340d-148">Bellek içi depolama</span><span class="sxs-lookup"><span data-stu-id="e340d-148">In-memory storage</span></span>

<span data-ttu-id="e340d-149">Aşağıdaki örnekler, bellekte depolanan bir sözlükte bağlantı ve kullanıcı bilgilerinin nasıl korunup korunacaklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="e340d-150">Sözlük, bağlantı `HashSet` kimliğini depolamak için a kullanır. Herhangi bir zamanda bir kullanıcı SinyalR uygulamasına birden fazla bağlantı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="e340d-151">Örneğin, birden çok aygıt veya birden fazla tarayıcı sekmesi aracılığıyla bağlanan bir kullanıcının birden fazla bağlantı kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="e340d-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="e340d-152">Uygulama kapanırsa, tüm bilgiler kaybolur, ancak kullanıcılar bağlantılarını yeniden kurdukça yeniden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="e340d-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="e340d-153">Ortamınızda birden fazla web sunucusu varsa bellek içi depolama çalışmaz, çünkü her sunucuda ayrı bir bağlantı koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="e340d-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="e340d-154">İlk örnek, kullanıcıların bağlantılarla eşleşmelerini yöneten bir sınıfı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="e340d-155">HashSet için anahtar kullanıcının adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e340d-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="e340d-156">Sonraki örnek, bir hub'dan bağlantı eşleme sınıfının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="e340d-157">Sınıfın örneği değişken bir adla `_connections`depolanır.</span><span class="sxs-lookup"><span data-stu-id="e340d-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="e340d-158">Tek kullanıcılı gruplar</span><span class="sxs-lookup"><span data-stu-id="e340d-158">Single-user groups</span></span>

<span data-ttu-id="e340d-159">Her kullanıcı için bir grup oluşturabilir ve yalnızca o kullanıcıya ulaşmak istediğinizde bu gruba bir ileti gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e340d-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="e340d-160">Her grubun adı kullanıcının adıdır.</span><span class="sxs-lookup"><span data-stu-id="e340d-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="e340d-161">Bir kullanıcının birden fazla bağlantısı varsa, her bağlantı kimliği kullanıcının grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="e340d-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="e340d-162">Kullanıcı bağlantınızı kestiğinde kullanıcıyı gruptan el ile kaldırmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="e340d-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="e340d-163">Bu eylem SignalR çerçevesi tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="e340d-164">Aşağıdaki örnek, tek kullanıcılı grupların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="e340d-165">Kalıcı, harici depolama</span><span class="sxs-lookup"><span data-stu-id="e340d-165">Permanent, external storage</span></span>

<span data-ttu-id="e340d-166">Bu konu, bağlantı bilgilerini depolamak için veritabanı nın veya Azure tablo depolama alanının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="e340d-167">Her web sunucusu aynı veri deposuyla etkileşimkurabileceğinden, birden çok web sunucunuz olduğunda bu yaklaşım çalışır.</span><span class="sxs-lookup"><span data-stu-id="e340d-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="e340d-168">Web sunucularınız çalışmayı durdurursa veya `OnDisconnected` uygulama yeniden başlatılırsa, yöntem çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="e340d-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="e340d-169">Bu nedenle, veri deponuzun artık geçerli olmayan bağlantı kimlikleri için kayıtları olması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e340d-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="e340d-170">Bu yetim kayıtları temizlemek için, uygulamanızla ilgili bir zaman dilimi dışında oluşturulan tüm bağlantıları geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="e340d-171">Bu bölümdeki örnekler, bağlantı oluşturulduğunda izleme değeri içerir, ancak arka plan işlemi olarak bunu yapmak isteyebilirsiniz, çünkü eski kayıtları temizlemek için nasıl göstermez.</span><span class="sxs-lookup"><span data-stu-id="e340d-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="e340d-172">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="e340d-172">Database</span></span>

<span data-ttu-id="e340d-173">Aşağıdaki örnekler, bağlantı ve kullanıcı bilgilerinin bir veritabanında nasıl korunup korunur'u gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="e340d-174">Herhangi bir veri erişim teknolojisini kullanabilirsiniz; ancak, aşağıdaki örnek, Varlık Çerçevesi'ni kullanarak modellerin nasıl tanımlanacağından gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e340d-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="e340d-175">Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="e340d-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="e340d-176">Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="e340d-177">İlk örnek, birçok bağlantı varlığıyla ilişkilendirilebilen bir kullanıcı varlığının nasıl tanımlanabileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e340d-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="e340d-178">Daha sonra, hub'dan, aşağıda gösterilen kodla her bağlantının durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e340d-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="e340d-179">Azure tablo depolama</span><span class="sxs-lookup"><span data-stu-id="e340d-179">Azure table storage</span></span>

<span data-ttu-id="e340d-180">Aşağıdaki Azure tablo depolama örneği veritabanı örneğine benzer.</span><span class="sxs-lookup"><span data-stu-id="e340d-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="e340d-181">Azure Tablo Depolama Hizmeti'ni başlatmanız gereken tüm bilgileri içermez.</span><span class="sxs-lookup"><span data-stu-id="e340d-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="e340d-182">Bilgi için [.NET'ten Tablo depolamasını nasıl kullanacağına](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)bakın.</span><span class="sxs-lookup"><span data-stu-id="e340d-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="e340d-183">Aşağıdaki örnekte, bağlantı bilgilerini depolamak için bir tablo varlığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e340d-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="e340d-184">Verileri kullanıcı adına göre bölümlere ayırır ve her varlığı bağlantı kimliğiyle tanımlar, böylece kullanıcı herhangi bir zamanda birden çok bağlantıya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e340d-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="e340d-185">Hub'da, her kullanıcının bağlantısının durumunu izlersiniz.</span><span class="sxs-lookup"><span data-stu-id="e340d-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
