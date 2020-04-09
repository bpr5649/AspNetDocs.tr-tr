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
# <a name="mapping-signalr-users-to-connections"></a>SignalR Kullanıcılarını Bağlantılarla Eşleme

 yazan: [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konu, kullanıcılar ve bağlantıları hakkında nasıl bilgi saklarıkları gösterir.
>
> Patrick Fletcher bu konunun yazılmasına yardımcı oldu.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Görsel Stüdyo 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR'ın önceki sürümleri hakkında daha fazla bilgi için [SignalR Eski Sürümleri'ne](../older-versions/index.md)bakın.
>
> ## <a name="questions-and-comments"></a>Sorular ve yorumlar
>
> Lütfen bu öğreticiyi nasıl beğendiğiniz ve sayfanın altındaki yorumlarda neler geliştirebileceğimiz hakkında geri bildirim de bırakın. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları ASP.NET [SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)gönderebilirsiniz.

## <a name="introduction"></a>Giriş

Bir hub'a bağlanan her istemci benzersiz bir bağlantı kimliği geçirir. Bu değeri hub bağlamının `Context.ConnectionId` özelliğinde alabilirsiniz. Uygulamanızın bir kullanıcıyı bağlantı kimliğiyle eşlemesi ve bu eşlemayı devam etmesi gerekiyorsa, aşağıdakilerden birini kullanabilirsiniz:

- [Kullanıcı Kimliği Sağlayıcısı (SignalR 2)](#IUserIdProvider)
- Sözlük gibi [bellek içi depolama](#inmemory)
- [Her kullanıcı için SignalR grubu](#groups)
- Veritabanı tablosu veya Azure tablo depolama gibi [kalıcı, harici depolama](#database)

Bu uygulamaların her biri bu konuda gösterilir. Kullanıcı bağlantı `OnConnected` `OnDisconnected`durumunu `OnReconnected` izlemek için `Hub` sınıfın , ve yöntemlerini kullanırsınız.

Uygulamanız için en iyi yaklaşım şuna bağlıdır:

- Uygulamanızı barındıran web sunucularının sayısı.
- Şu anda bağlı olan kullanıcıların listesini almanız gerekip gerekmediği.
- Uygulama veya sunucu yeniden başlatıldığında grup ve kullanıcı bilgilerini devam ettirebilmeniz gerekip gerekmediği.
- Harici bir sunucuarama nın gecikmesinin bir sorun olup olmadığı.

Aşağıdaki tabloda, bu hususlar için hangi yaklaşımın işe yaradığı gösterilmektedir.

|  | Birden fazla sunucu | Şu anda bağlı olan kullanıcıların listesini alma | Yeniden başlatıldıktan sonra bilgileri devam etti | Optimum performans |
| --- | --- | --- | --- | --- |
| UserID Sağlayıcısı | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| Bellek içi |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Tek kullanıcılı gruplar | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Kalıcı, dış | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID sağlayıcısı

Bu özellik, kullanıcıların yeni bir arayüz iUserIdProvider üzerinden bir IRequest'e dayalı kullanıcı Kimliği'nin ne olduğunu belirtmelerine olanak tanır.

**IUseridSağlayıcı**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Varsayılan olarak, kullanıcı adı olarak kullanıcının `IPrincipal.Identity.Name` kullanan bir uygulama olacaktır. Bunu değiştirmek için, uygulamanız başladığında uygulamanızı genel ana `IUserIdProvider` bilgisayara kaydedin:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

Bir hub içinden, aşağıdaki API üzerinden bu kullanıcılara ileti gönderebilirsiniz:

**Belirli bir kullanıcıya ileti gönderme**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Bellek içi depolama

Aşağıdaki örnekler, bellekte depolanan bir sözlükte bağlantı ve kullanıcı bilgilerinin nasıl korunup korunacaklarını gösterir. Sözlük, bağlantı `HashSet` kimliğini depolamak için a kullanır. Herhangi bir zamanda bir kullanıcı SinyalR uygulamasına birden fazla bağlantı olabilir. Örneğin, birden çok aygıt veya birden fazla tarayıcı sekmesi aracılığıyla bağlanan bir kullanıcının birden fazla bağlantı kimliği vardır.

Uygulama kapanırsa, tüm bilgiler kaybolur, ancak kullanıcılar bağlantılarını yeniden kurdukça yeniden doldurulur. Ortamınızda birden fazla web sunucusu varsa bellek içi depolama çalışmaz, çünkü her sunucuda ayrı bir bağlantı koleksiyonu vardır.

İlk örnek, kullanıcıların bağlantılarla eşleşmelerini yöneten bir sınıfı gösterir. HashSet için anahtar kullanıcının adı olacaktır.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Sonraki örnek, bir hub'dan bağlantı eşleme sınıfının nasıl kullanılacağını gösterir. Sınıfın örneği değişken bir adla `_connections`depolanır.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Tek kullanıcılı gruplar

Her kullanıcı için bir grup oluşturabilir ve yalnızca o kullanıcıya ulaşmak istediğinizde bu gruba bir ileti gönderebilirsiniz. Her grubun adı kullanıcının adıdır. Bir kullanıcının birden fazla bağlantısı varsa, her bağlantı kimliği kullanıcının grubuna eklenir.

Kullanıcı bağlantınızı kestiğinde kullanıcıyı gruptan el ile kaldırmamalısınız. Bu eylem SignalR çerçevesi tarafından otomatik olarak gerçekleştirilir.

Aşağıdaki örnek, tek kullanıcılı grupların nasıl uygulanacağını gösterir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Kalıcı, harici depolama

Bu konu, bağlantı bilgilerini depolamak için veritabanı nın veya Azure tablo depolama alanının nasıl kullanılacağını gösterir. Her web sunucusu aynı veri deposuyla etkileşimkurabileceğinden, birden çok web sunucunuz olduğunda bu yaklaşım çalışır. Web sunucularınız çalışmayı durdurursa veya `OnDisconnected` uygulama yeniden başlatılırsa, yöntem çağrılmaz. Bu nedenle, veri deponuzun artık geçerli olmayan bağlantı kimlikleri için kayıtları olması mümkündür. Bu yetim kayıtları temizlemek için, uygulamanızla ilgili bir zaman dilimi dışında oluşturulan tüm bağlantıları geçersiz kılabilir. Bu bölümdeki örnekler, bağlantı oluşturulduğunda izleme değeri içerir, ancak arka plan işlemi olarak bunu yapmak isteyebilirsiniz, çünkü eski kayıtları temizlemek için nasıl göstermez.

### <a name="database"></a>Veritabanı

Aşağıdaki örnekler, bağlantı ve kullanıcı bilgilerinin bir veritabanında nasıl korunup korunur'u gösterir. Herhangi bir veri erişim teknolojisini kullanabilirsiniz; ancak, aşağıdaki örnek, Varlık Çerçevesi'ni kullanarak modellerin nasıl tanımlanacağından gösterilmektedir. Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir. Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde değişebilir.

İlk örnek, birçok bağlantı varlığıyla ilişkilendirilebilen bir kullanıcı varlığının nasıl tanımlanabileceğini gösterir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Daha sonra, hub'dan, aşağıda gösterilen kodla her bağlantının durumunu izleyebilirsiniz.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure tablo depolama

Aşağıdaki Azure tablo depolama örneği veritabanı örneğine benzer. Azure Tablo Depolama Hizmeti'ni başlatmanız gereken tüm bilgileri içermez. Bilgi için [.NET'ten Tablo depolamasını nasıl kullanacağına](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)bakın.

Aşağıdaki örnekte, bağlantı bilgilerini depolamak için bir tablo varlığı gösterilmektedir. Verileri kullanıcı adına göre bölümlere ayırır ve her varlığı bağlantı kimliğiyle tanımlar, böylece kullanıcı herhangi bir zamanda birden çok bağlantıya sahip olabilir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

Hub'da, her kullanıcının bağlantısının durumunu izlersiniz.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
