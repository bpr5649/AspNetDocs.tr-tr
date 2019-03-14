---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: Signalr'da gruplarla çalışma | Microsoft Docs
author: bradygaster
description: Bu konu, grup üyeliği bilgileri Hub API'si ile kalıcı hale getirmek açıklar.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 384b7e5f07fa46ea3cc32e5c18c3c2327b7aedd3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066207"
---
<a name="working-with-groups-in-signalr"></a>SignalR’da Gruplarla Çalışma
====================
tarafından [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konuda, kullanıcı gruplarına ekleyin ve grup üyeliği bilgileri kalıcı açıklar.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konu başlığında kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR eski sürümleri hakkında daha fazla bilgi için bkz: [SignalR eski sürümleri](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Sorularınız ve yorumlarınız
>
> Lütfen bu öğreticide sevmediğinizi nasıl ve ne sayfanın alt kısmındaki açıklamalarda geliştirebileceğimiz hakkında geri bildirim bırakın. Öğretici için doğrudan ilgili olmayan sorularınız varsa, bunları gönderebilir [ASP.NET SignalR Forumu](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Genel Bakış

Signalr'da gruplarla, bağlı istemciler belirtilen alt kümelerine yayın iletileri için bir yöntem sağlar. Bir grupta herhangi bir sayıda istemciler olabilir ve istemci grupları herhangi bir sayıda üyesi olabilir. Açıkça grupları oluşturmanız gerekmez. Aslında, bir grup otomatik olarak ilk kez bir çağrıda Groups.Add adını belirleyin oluşturulur ve bu üyelik son bağlantı kaldırdığınızda silinir. Grupları kullanarak bir giriş için bkz. [Hub sınıftan grup üyeliğini yönetme](hubs-api-guide-server.md#groupsfromhub) Hubs API - Server Kılavuzu.

Bir grup üyeliği listesinin veya grupların listesini almak için hiçbir API yoktur. SignalR istemcisi ve yayımlama/abonelik modelini temel alan grubu iletileri gönderir ve sunucu grupları veya grup üyeliklerinin listesi korumaz. Bir web grubu için bir düğüm eklediğinizde, yeni bir düğüme dağıtılmasını SignalR tutar herhangi bir durum olduğundan bu ölçeklenebilirliği en üst düzeye yardımcı olur.

Kullanarak bir grup kullanıcı eklediğinizde `Groups.Add` yöntemi, kullanıcının geçerli bağlantının süresi boyunca bu gruba yönlendirilmiş iletileri alır, ancak kullanıcının üyelik o gruptaki geçerli bağlantı kalıcı değil. Gruplar ve grup üyeliği bilgileri kalıcı olarak tutmak istiyorsanız, bir veritabanı veya Azure tablo depolama gibi bir depoda bu verileri saklamanız gerekir. Ardından, bir kullanıcı uygulamanıza her bağlandığında, depodan kullanıcının ait olduğu grupları almak ve bu kullanıcı için bu grupları el ile ekleyin.

Sonra geçici bir kesinti bağlanırken, kullanıcı otomatik olarak daha önce atanan gruplar yeniden birleştirir. Otomatik olarak bir grup aşamalarını yalnızca yeniden bağlanma, yeni bir bağlantı kurmadan olduğunda geçerlidir. Dijital olarak imzalanmış bir belirteç, daha önce atanan gruplar listesini içeren istemciden geçirilir. Kullanıcının istenen gruplara ait olup olmadığını doğrulamak istiyorsanız, varsayılan davranışı geçersiz kılabilirsiniz.

Bu konu aşağıdaki bölümleri içermektedir:

- [Ekleme ve kullanıcıları kaldırma](#add)
- [Bir grubun üyeleri çağırma](#call)
- [Grup üyeliği veritabanında depolama](#storedatabase)
- [Azure tablo depolama grup üyeliği](#storeazuretable)
- [Grup üyeliği bağlanırken doğrulanıyor](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Ekleme ve kullanıcıları kaldırma

Eklemek veya gruptan kullanıcılar kaldırmak için çağrı [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) veya [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemleri ve kullanıcının bağlantı kimliği ve grubun adını parametreler olarak geçirin. El ile bağlantı sona erdiğinde bir kullanıcıyı bir gruptan kaldırmak gerekmez.

Aşağıdaki örnekte gösterildiği `Groups.Add` ve `Groups.Remove` Hub yöntemlerinde kullanılan yöntemleri.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` Ve `Groups.Remove` zaman uyumsuz bir yöntem yürütülemez.

Bir istemci bir gruba ekleyin ve hemen bir ileti grubunu kullanarak istemciye göndermek istiyorsanız, Groups.Add yöntemin ilk sonlandırdığından emin yapmanız gerekir. Aşağıdaki kod örnekleri bunun nasıl yapılacağını gösterir.

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

Genel olarak, dahil `await` çağırırken `Groups.Remove` yöntemi kaldırmaya çalıştığınız bağlantı kimliği artık kullanılabilir olabileceğinden. Bu durumda, `TaskCanceledException` istek zaman aşımına sonra oluşturulur. Ekleyebileceğiniz uygulamanızı gruba bir ileti göndermeden önce kullanıcının gruptan kaldırıldığından emin olmanız gerekir, `await` önce `Groups.Remove`ve ardından catch `TaskCanceledException` oluşturulabilecek özel durum.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Bir grubun üyeleri çağırma

İleti tümünün bir grubun üyesi ya da yalnızca belirtilen grup üyeleri için aşağıdaki örneklerde gösterildiği gibi gönderebilirsiniz.

- **Tüm** bağlı istemciler belirtilen grubunda.

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- Bağlı olan tüm istemciler belirtilen gruptaki **dışındaki belirtilen istemcilerin**, belirtilen bağlantı kimliğine göre

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- Bağlı olan tüm istemciler belirtilen gruptaki **çağıran istemci dışındaki**.

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Grup üyeliği veritabanında depolama

Aşağıdaki örnekler, Grup ve kullanıcı bilgileri bir veritabanında saklamanın gösterilmektedir. Tüm veri erişim teknolojisi kullanabilirsiniz; Ancak, aşağıdaki örnekte, Entity Framework kullanarak modelleri tanımlamak nasıl gösterir. Bu varlık modeli, veritabanı tabloları ve alanları karşılık gelir. Data yapınız, uygulama gereksinimlerine bağlı olarak önemli ölçüde değişiklik gösterebilir. Bu örnek adlı bir sınıf içerir `ConversationRoom` kullanıcıların spor veya bahçesi oluşturma gibi farklı konularla ilgili konuşmaları katılmasına sağlayan bir uygulama için benzersiz olacak. Bu örnek ayrıca bağlantılar için bir sınıf içerir. Bağlantı sınıfı grup üyeliği izlemek için gerekli değildir, ancak kullanıcılar izleme için sağlam bir çözüm sık parçasıdır.

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

Ardından, hub'ında grubu ve kullanıcı bilgilerini veritabanından ve el ile kullanıcı uygun gruplara ekleyin. Örneğin, kullanıcı bağlantıları izlemek için kod içermez. Bu örnekte, `await` önce anahtar sözcüğü uygulanmaz `Groups.Add` çünkü bir ileti grubunun üyelerine hemen gönderilmez. Yeni üye hemen ekledikten sonra grubun tüm üyeleri için bir ileti göndermek istiyorsanız, uygulamak ister `await` zaman uyumsuz işlemi tamamlandı emin olmak için anahtar sözcüğü.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Azure tablo depolama grup üyeliği

Grup ve kullanıcı bilgilerini depolamak için Azure tablo depolaması'nı kullanarak, bir veritabanı kullanmaya benzer. Aşağıdaki örnek, kullanıcı adı ve grup adı depolayan bir tablo varlığı gösterir.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

Hub'ında kullanıcı bağlandığında atanan grupları alır.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Grup üyeliği bağlanırken doğrulanıyor

Varsayılan olarak, SignalR otomatik olarak bir kullanıcı uygun gruplara ne zaman bir bağlantı bırakılan ve bağlantı zaman aşımına uğramadan önce yeniden oluşturulan gibi geçici bir kesintisinden bağlanırken yeniden atar. Kullanıcı grubu bilgileri bağlanırken bir belirteç geçirilir ve bu belirteci, sunucu üzerinde doğrulanır. Kullanıcı gruplarına yeniden katılma için doğrulama işlemi hakkında daha fazla bilgi için bkz. [grupları bağlanırken aşamalarını](../security/introduction-to-security.md#rejoingroup).

Genel olarak, otomatik olarak gruplara yeniden aşamalarını varsayılan davranışını kullanmanız gerekir. SignalR grupları hassas verilere erişimi kısıtlamak için bir güvenlik mekanizması olarak tasarlanmamıştır. Ancak, uygulamanızın bir kullanıcının grup üyeliğine bağlanırken denetleyin, varsayılan davranışı geçersiz kılabilirsiniz. Bir kullanıcının grup üyeliğine her yeniden bağlantı yerine yalnızca kullanıcı bağlandığında alınması gerektiğinden varsayılan davranışını değiştirme veritabanınız için bir yük ekleyebilirsiniz.

Grup üyeliği doğrulamanız gerekir yeniden, aşağıda gösterildiği gibi atanan gruplarının bir listesini döndüren yeni bir hub işlem hattı modül oluşturun.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

Ardından, bu modül aşağıda vurgulandığı gibi hub ardışık düzenine ekleyin.

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
