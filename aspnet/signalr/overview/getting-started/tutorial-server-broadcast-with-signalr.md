---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Öğretici: SignalR 2 ile sunucu yayını | Microsoft Docs'
author: tdykstra
description: Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345603"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="b1329-103">Öğretici: SignalR 2 ile sunucu yayını</span><span class="sxs-lookup"><span data-stu-id="b1329-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b1329-104">Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1329-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="b1329-105">Sunucu yayını, sunucunun istemcilere gönderilen iletişimleri başlattığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b1329-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="b1329-106">Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir stok Ticker benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="b1329-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="b1329-107">Düzenli aralıklarla, sunucu stok fiyatlarını rastgele güncelleştirir ve güncelleştirmeleri tüm bağlı istemcilere yayınlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="b1329-108">Tarayıcıda, **değişiklik** ve sütunlardaki sayılar ve semboller, **%** sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="b1329-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="b1329-109">Aynı URL 'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="b1329-111">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="b1329-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1329-112">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-112">Create the project</span></span>
> * <span data-ttu-id="b1329-113">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-113">Set up the server code</span></span>
> * <span data-ttu-id="b1329-114">Sunucu kodunu inceleyin</span><span class="sxs-lookup"><span data-stu-id="b1329-114">Examine the server code</span></span>
> * <span data-ttu-id="b1329-115">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-115">Set up the client code</span></span>
> * <span data-ttu-id="b1329-116">İstemci kodunu inceleme</span><span class="sxs-lookup"><span data-stu-id="b1329-116">Examine the client code</span></span>
> * <span data-ttu-id="b1329-117">Uygulamayı test edin</span><span class="sxs-lookup"><span data-stu-id="b1329-117">Test the application</span></span>
> * <span data-ttu-id="b1329-118">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b1329-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1329-119">Uygulamayı oluşturma adımları boyunca çalışmak istemiyorsanız, SignalR. Sample paketini yeni bir boş ASP.NET Web uygulaması projesine yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="b1329-120">NuGet paketini bu öğreticideki adımları uygulamadan yüklerseniz, *readme.txt* dosyadaki yönergeleri izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="b1329-121">Paketi çalıştırmak için, yüklü paketteki yöntemi çağıran bir OWıN başlangıç sınıfı eklemeniz gerekir `ConfigureSignalR` .</span><span class="sxs-lookup"><span data-stu-id="b1329-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="b1329-122">OWıN başlangıç sınıfını eklememanız durumunda bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="b1329-123">Bu makalenin [StockTicker örneğini Install](#install-the-stockticker-sample) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b1329-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1329-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1329-124">Prerequisites</span></span>

* <span data-ttu-id="b1329-125">**ASP.NET ve web geliştirme** iş yüküyle [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b1329-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="b1329-126">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-126">Create the project</span></span>

<span data-ttu-id="b1329-127">Bu bölümde, Visual Studio 2017 ' ın boş bir ASP.NET Web uygulaması oluşturmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1329-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="b1329-128">Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1329-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="b1329-130">**Yeni ASP.NET Web uygulaması-SignalR. StockTicker** penceresinde **boş** bırakın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="b1329-131">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-131">Set up the server code</span></span>

<span data-ttu-id="b1329-132">Bu bölümde, sunucuda çalışan kodu ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="b1329-133">Hisse senedi sınıfını oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-133">Create the Stock class</span></span>

<span data-ttu-id="b1329-134">Bir hisse senedi hakkındaki bilgileri depolamak ve aktarmak için kullanacağınız *Stok* modeli sınıfını oluşturarak başlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="b1329-135">**Çözüm Gezgini**, projeye sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**.</span><span class="sxs-lookup"><span data-stu-id="b1329-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b1329-136">Sınıfı *stoğa* adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1329-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="b1329-137">*Stock.cs* dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b1329-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="b1329-138">Hisse senetleri oluştururken ayarlayacağımız iki özellik `Symbol` (örneğin, Microsoft IÇIN MSFT) ve `Price` .</span><span class="sxs-lookup"><span data-stu-id="b1329-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="b1329-139">Diğer özellikler, nasıl ve ne zaman ayarlandığınıza bağlıdır `Price` .</span><span class="sxs-lookup"><span data-stu-id="b1329-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="b1329-140">İlk kez ayarlandığında `Price` değer değerine yayılır `DayOpen` .</span><span class="sxs-lookup"><span data-stu-id="b1329-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="b1329-141">Bundan sonra uygulama, ve `Price` `Change` `PercentChange` özellik değerlerini ve arasındaki farka göre hesaplar `Price` `DayOpen` .</span><span class="sxs-lookup"><span data-stu-id="b1329-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="b1329-142">StockTickerHub ve StockTicker sınıfları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="b1329-143">Sunucudan istemciye etkileşimi işlemek için SignalR hub API 'sini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="b1329-144">`StockTickerHub`SignalR sınıfından türetilen bir sınıf, `Hub` istemcilerden gelen bağlantıları ve Yöntem çağrılarını almayı işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="b1329-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="b1329-145">Ayrıca, stok verilerini korumanız ve bir nesnesi çalıştırmanız gerekir `Timer` .</span><span class="sxs-lookup"><span data-stu-id="b1329-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="b1329-146">`Timer`Nesne, istemci bağlantılarından bağımsız olarak fiyat güncelleştirmelerini tetikleyecektir.</span><span class="sxs-lookup"><span data-stu-id="b1329-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="b1329-147">`Hub`Hub 'lar geçici olduğundan bu işlevleri bir sınıfa koyamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="b1329-148">Uygulama, `Hub` hub üzerindeki her görev için, istemcilerden sunucuya bağlantılar ve çağrılar gibi bir sınıf örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1329-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="b1329-149">Bu nedenle, stok verilerini tutan, fiyatları güncelleştiren ve fiyat güncelleştirmelerinin yayınlarından oluşan mekanizmanın ayrı bir sınıfta çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="b1329-150">Sınıfını adlandırın `StockTicker` .</span><span class="sxs-lookup"><span data-stu-id="b1329-150">You'll name the class `StockTicker`.</span></span>

![StockTicker 'den yayımlama](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="b1329-152">Yalnızca bir sınıfın bir örneğinin `StockTicker` sunucuda çalıştırılmasını istiyorsunuz, bu nedenle her örnekten tek örneğe bir başvuru ayarlamanız gerekir `StockTickerHub` `StockTicker` .</span><span class="sxs-lookup"><span data-stu-id="b1329-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="b1329-153">`StockTicker`Hisse senedi verileri olduğundan ve güncelleştirmeleri tetiklediği, ancak `StockTicker` bir sınıf olmadığı için, sınıfı istemcilere yayınlayacak `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b1329-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="b1329-154">`StockTicker`Sınıfı, SignalR hub bağlantı bağlamı nesnesine bir başvuru almak için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b1329-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="b1329-155">Daha sonra, istemcilere yayımlamak için SignalR bağlantı bağlamı nesnesini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b1329-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="b1329-156">StockTickerHub.cs oluştur</span><span class="sxs-lookup"><span data-stu-id="b1329-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="b1329-157">**Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b1329-158">**Add New Item-SignalR. StockTicker**' da, **yüklü**  >  **Visual C#**  >  **Web**  >  **SignalR** ' yi seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="b1329-159">Sınıfı *StockTickerHub* olarak adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1329-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="b1329-160">Bu adım *StockTickerHub.cs* sınıf dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1329-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="b1329-161">Aynı anda, bir dizi betik dosyası ve proje için SignalR 'yi destekleyen derleme başvuruları ekler.</span><span class="sxs-lookup"><span data-stu-id="b1329-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="b1329-162">*StockTickerHub.cs* dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b1329-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="b1329-163">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b1329-163">Save the file.</span></span>

<span data-ttu-id="b1329-164">Uygulama, istemcilerin sunucuda çağırabilmesine yönelik yöntemleri tanımlamak için [hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="b1329-165">Bir yöntem tanımlanıyor: `GetAllStocks()` .</span><span class="sxs-lookup"><span data-stu-id="b1329-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="b1329-166">Bir istemci sunucuya ilk kez bağlandığında, geçerli fiyatlarına sahip tüm hisse senetleri listesini almak için bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="b1329-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="b1329-167">Yöntemi zaman uyumlu olarak çalışabilir ve bellekten veri döndürdüğü için döndürebilir `IEnumerable<Stock>` .</span><span class="sxs-lookup"><span data-stu-id="b1329-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="b1329-168">Bir veritabanı araması veya bir Web hizmeti çağrısı gibi beklenmek üzere, yöntemin verileri alması gerekiyorsa, `Task<IEnumerable<Stock>>` zaman uyumsuz işlemeyi etkinleştirmek için dönüş değeri olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="b1329-169">Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-zaman uyumsuz olarak yürütülecektir](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="b1329-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="b1329-170">`HubName`Özniteliği, uygulamanın, Istemcideki JavaScript kodunda hub 'a nasıl başvurulacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b1329-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="b1329-171">İstemci üzerindeki varsayılan ad bu özniteliği kullanmıyorsanız, sınıf adının bir camelCase sürümüdür ve bu durumda olacaktır `stockTickerHub` .</span><span class="sxs-lookup"><span data-stu-id="b1329-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="b1329-172">Daha sonra `StockTicker` sınıfı oluşturduğunuzda, uygulama statik özelliğinde bu sınıfın tek bir örneğini oluşturur `Instance` .</span><span class="sxs-lookup"><span data-stu-id="b1329-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="b1329-173">Bu tek örneği `StockTicker` , kaç istemcinin bağlanıp bağlantısı kesildiğine bakılmaksızın bellekte bulunur.</span><span class="sxs-lookup"><span data-stu-id="b1329-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="b1329-174">Bu örnek, `GetAllStocks()` yöntemin geçerli stok bilgilerini döndürmek için kullandığı şeydir.</span><span class="sxs-lookup"><span data-stu-id="b1329-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="b1329-175">StockTicker.cs oluştur</span><span class="sxs-lookup"><span data-stu-id="b1329-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="b1329-176">**Çözüm Gezgini**, projeye sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**.</span><span class="sxs-lookup"><span data-stu-id="b1329-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b1329-177">Sınıfı *StockTicker* olarak adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1329-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="b1329-178">*StockTicker.cs* dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b1329-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="b1329-179">Tüm iş parçacıkları StockTicker Code 'un aynı örneğini çalıştırdığından, StockTicker sınıfının iş parçacığı açısından güvenli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="b1329-180">Sunucu kodunu inceleyin</span><span class="sxs-lookup"><span data-stu-id="b1329-180">Examine the server code</span></span>

<span data-ttu-id="b1329-181">Sunucu kodunu incelerseniz, uygulamanın nasıl çalıştığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b1329-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="b1329-182">Tek örneği statik bir alanda depolama</span><span class="sxs-lookup"><span data-stu-id="b1329-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="b1329-183">Kod, `_instance` `Instance` özelliği sınıfın bir örneğiyle yedekleyen statik alanı başlatır.</span><span class="sxs-lookup"><span data-stu-id="b1329-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="b1329-184">Oluşturucu özel olduğundan, sınıfın, uygulamanın oluşturabileceğinden tek örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b1329-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="b1329-185">Uygulama, alan için [yavaş başlatma](/dotnet/framework/performance/lazy-initialization) kullanır `_instance` .</span><span class="sxs-lookup"><span data-stu-id="b1329-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="b1329-186">Performans nedenleriyle bu değildir.</span><span class="sxs-lookup"><span data-stu-id="b1329-186">It's not for performance reasons.</span></span> <span data-ttu-id="b1329-187">Örnek oluşturmanın iş parçacığı açısından güvenli olduğundan emin olmak.</span><span class="sxs-lookup"><span data-stu-id="b1329-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="b1329-188">İstemci sunucuya her bağlanışında, ayrı bir iş parçacığında çalışan StockTickerHub sınıfının yeni bir örneği, `StockTicker.Instance` sınıfında daha önce gördüğünüz gibi, static özelliğinden StockTicker Singleton örneğini alır `StockTickerHub` .</span><span class="sxs-lookup"><span data-stu-id="b1329-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="b1329-189">Bir ConcurrentDictionary içinde hisse senedi verilerini depolama</span><span class="sxs-lookup"><span data-stu-id="b1329-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="b1329-190">Oluşturucu, `_stocks` koleksiyonu bazı örnek hisse senedi verileri ile başlatır ve `GetAllStocks` hisse senetleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="b1329-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="b1329-191">Daha önce gördüğünüz gibi, bu hisse senedi koleksiyonu tarafından `StockTickerHub.GetAllStocks` , `Hub` istemcilerin çağırabileceği sınıfta bir sunucu yöntemi olan tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b1329-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="b1329-192">Hisse senetleri koleksiyonu, iş parçacığı güvenliği için bir [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="b1329-193">Alternatif olarak, bir [Sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve üzerinde değişiklik yaptığınızda sözlüğü açıkça kilitleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="b1329-194">Bu örnek uygulama için uygulama verilerini bellekte depolamak ve uygulama örneği olmadığında verileri kaybetmek için Tamam  `StockTicker` .</span><span class="sxs-lookup"><span data-stu-id="b1329-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="b1329-195">Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposuyla çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="b1329-196">Stok fiyatlarını düzenli olarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b1329-196">Periodically updating stock prices</span></span>

<span data-ttu-id="b1329-197">Oluşturucu, `Timer` stok fiyatlarını rastgele olarak güncelleştiren yöntemleri düzenli aralıklarla çağıran bir nesne başlatır.</span><span class="sxs-lookup"><span data-stu-id="b1329-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="b1329-198">`Timer``UpdateStockPrices`durum parametresinde null değeri geçen çağrılar.</span><span class="sxs-lookup"><span data-stu-id="b1329-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="b1329-199">Fiyatlar güncelleştirilmeden önce uygulama, nesne üzerinde bir kilit alır `_updateStockPricesLock` .</span><span class="sxs-lookup"><span data-stu-id="b1329-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="b1329-200">Kod, başka bir iş parçacığının fiyatları güncelleştirme olup olmadığını denetler ve ardından `TryUpdateStockPrice` listedeki her bir stoğa çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="b1329-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="b1329-201">`TryUpdateStockPrice`Yöntemi, stok fiyatının değiştirilip değişmeyeceğine ve ne kadarının değiştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="b1329-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="b1329-202">Stok fiyatı değişirse, uygulama `BroadcastStockPrice` Stok fiyatı değişikliğini tüm bağlı istemcilere yayınlamak için çağırır.</span><span class="sxs-lookup"><span data-stu-id="b1329-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="b1329-203">`_updatingStockPrices`Bu bayrak, iş parçacığı açısından güvenli olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak belirlenmiş.</span><span class="sxs-lookup"><span data-stu-id="b1329-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="b1329-204">Gerçek bir uygulamada, `TryUpdateStockPrice` yöntemi fiyatı aramak için bir Web hizmeti çağırır.</span><span class="sxs-lookup"><span data-stu-id="b1329-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="b1329-205">Bu kodda, uygulama, değişiklikleri rastgele yapmak için rastgele bir sayı Oluşturucu kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="b1329-206">StockTicker sınıfının istemcilere yayınlanabilmesi için SignalR bağlamı alma</span><span class="sxs-lookup"><span data-stu-id="b1329-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="b1329-207">Fiyat değişiklikleri nesnede yer aldığı için `StockTicker` , bu, `updateStockPrice` tüm bağlı istemcilerde bir yöntemi çağırması gereken nesnedir.</span><span class="sxs-lookup"><span data-stu-id="b1329-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="b1329-208">Bir `Hub` sınıfında, istemci yöntemlerini çağırmak için BIR API 'si vardır, ancak `StockTicker` sınıfından türemez `Hub` ve herhangi bir nesneye başvuruya sahip olmaz `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b1329-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="b1329-209">Bağlı istemcilere yayımlamak için, sınıfın, `StockTicker` sınıfa yönelik SignalR bağlam örneğini alması `StockTickerHub` ve istemcileri üzerinde yöntemleri çağırmak için kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="b1329-210">Kod, tek sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya geçirir ve Oluşturucu onu `Clients` özelliğine koyar.</span><span class="sxs-lookup"><span data-stu-id="b1329-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="b1329-211">Bağlamı yalnızca bir kez almak istediğiniz iki neden vardır: bağlamı almak pahalı bir görevdir ve bir kez alınması, uygulamanın istemcilere gönderilen iletilerin amaçlanan sırasını koruyabilmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="b1329-212">`Clients`Bağlam özelliğinin alınması ve özelliğe yerleştirilmesi, `StockTickerClient` bir sınıfta olduğu gibi görünen istemci yöntemlerini çağırmak için kod yazmanıza olanak tanır `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b1329-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="b1329-213">Örneğin, yazabileceğiniz tüm istemcilere yayımlamak için `Clients.All.updateStockPrice(stock)` .</span><span class="sxs-lookup"><span data-stu-id="b1329-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="b1329-214">`updateStockPrice`İçinde aradığınız Yöntem `BroadcastStockPrice` henüz yok.</span><span class="sxs-lookup"><span data-stu-id="b1329-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="b1329-215">Daha sonra, istemcide çalışan bir kod yazdığınızda eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="b1329-216">`updateStockPrice` `Clients.All` Dinamik olduğundan, uygulamanın, çalışma zamanında ifadeyi değerlendileceğini gösterdiği için buraya başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="b1329-217">Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve istemcinin adlı bir yöntemi varsa `updateStockPrice` , uygulama bu yöntemi çağırır ve parametre değerini bu yönteme iletir.</span><span class="sxs-lookup"><span data-stu-id="b1329-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="b1329-218">`Clients.All` tüm istemcilere gönderme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b1329-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="b1329-219">SignalR, hangi istemcileri veya istemci gruplarını gönderileceğini belirtmek için size diğer seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="b1329-220">Daha fazla bilgi için bkz. [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="b1329-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="b1329-221">SignalR rotasını kaydetme</span><span class="sxs-lookup"><span data-stu-id="b1329-221">Register the SignalR route</span></span>

<span data-ttu-id="b1329-222">Sunucunun hangi URL 'yi ele geçirip SignalR 'ye yönlendireceğimizi bilmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="b1329-223">Bunu yapmak için bir OWıN başlangıç sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b1329-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="b1329-224">**Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b1329-225">**Yeni öğe Ekle-SignalR. StockTicker** **yüklü**  >  **Visual C#**  >  **Web** ' i seçin ve ardından **owın başlangıç sınıfı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="b1329-226">Sınıfın *başlangıcını* adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="b1329-227">*Startup.cs* dosyasındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b1329-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="b1329-228">Artık sunucu kodunu ayarlamayı tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="b1329-229">Sonraki bölümde, istemcisini ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="b1329-230">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-230">Set up the client code</span></span>

<span data-ttu-id="b1329-231">Bu bölümde, istemcisinde çalışan kodu ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b1329-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="b1329-232">HTML sayfası ve JavaScript dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="b1329-233">HTML sayfasında veriler görüntülenir ve JavaScript dosyası verileri düzenler.</span><span class="sxs-lookup"><span data-stu-id="b1329-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="b1329-234">StockTicker.html oluştur</span><span class="sxs-lookup"><span data-stu-id="b1329-234">Create StockTicker.html</span></span>

<span data-ttu-id="b1329-235">İlk olarak, HTML istemcisini eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="b1329-236">**Çözüm Gezgini**' de projeye sağ tıklayın ve **Add**  >  **HTML sayfası**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="b1329-237">Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b1329-238">*StockTicker.html* dosyasındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b1329-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="b1329-239">HTML, beş sütun, üst bilgi satırı ve beş sütuna yayılan tek bir hücre içeren bir veri satırı içeren bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1329-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="b1329-240">Veri satırında "yükleniyor..." görüntülenir uygulama başladığında anlık olarak.</span><span class="sxs-lookup"><span data-stu-id="b1329-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="b1329-241">JavaScript kodu, bu satırı kaldırır ve kendi yerleştirme satırlarına sunucudan alınan stok verilerini ekler.</span><span class="sxs-lookup"><span data-stu-id="b1329-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="b1329-242">Komut dosyası etiketleri şunları belirtir:</span><span class="sxs-lookup"><span data-stu-id="b1329-242">The script tags specify:</span></span>

    * <span data-ttu-id="b1329-243">JQuery betik dosyası.</span><span class="sxs-lookup"><span data-stu-id="b1329-243">The jQuery script file.</span></span>

    * <span data-ttu-id="b1329-244">SignalR çekirdek betik dosyası.</span><span class="sxs-lookup"><span data-stu-id="b1329-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="b1329-245">SignalR proxy 'leri betik dosyası.</span><span class="sxs-lookup"><span data-stu-id="b1329-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="b1329-246">Daha sonra oluşturacağınız bir StockTicker betik dosyası.</span><span class="sxs-lookup"><span data-stu-id="b1329-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="b1329-247">Uygulama, SignalR proxy 'leri betik dosyasını dinamik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1329-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="b1329-248">"/SignalR/hub 'ları" URL 'sini belirtir ve bu örnekte, için hub sınıfındaki yöntemler için proxy yöntemlerini tanımlar `StockTickerHub.GetAllStocks` .</span><span class="sxs-lookup"><span data-stu-id="b1329-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="b1329-249">İsterseniz, [SignalR yardımcı programlarını](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)kullanarak bu JavaScript dosyasını el ile oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="b1329-250">Yöntem çağrısında dinamik dosya oluşturmayı devre dışı bırakmayı unutmayın `MapHubs` .</span><span class="sxs-lookup"><span data-stu-id="b1329-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="b1329-251">**Çözüm Gezgini**' de **betikler**' ı genişletin.</span><span class="sxs-lookup"><span data-stu-id="b1329-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="b1329-252">JQuery ve SignalR için betik kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b1329-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b1329-253">Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="b1329-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="b1329-254">Kod bloğundaki betik başvurularını projedeki betik dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b1329-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="b1329-255">**Çözüm Gezgini**' de, *StockTicker.html*öğesine sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="b1329-256">StockTicker.js oluştur</span><span class="sxs-lookup"><span data-stu-id="b1329-256">Create StockTicker.js</span></span>

<span data-ttu-id="b1329-257">Şimdi JavaScript dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1329-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="b1329-258">**Çözüm Gezgini**, projeye sağ tıklayın ve **Add**  >  **JavaScript dosyası**Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="b1329-259">Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b1329-260">Bu kodu *StockTicker.js* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b1329-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="b1329-261">İstemci kodunu inceleme</span><span class="sxs-lookup"><span data-stu-id="b1329-261">Examine the client code</span></span>

<span data-ttu-id="b1329-262">İstemci kodunu incelerseniz, istemci kodunun, uygulamayı çalışır hale getirmek için sunucu koduyla nasıl etkileşime gireceğini öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="b1329-263">Bağlantı başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="b1329-263">Starting the connection</span></span>

<span data-ttu-id="b1329-264">`$.connection` SignalR proxy 'leri anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b1329-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="b1329-265">Kod, sınıf için proxy 'ye bir başvuru alır `StockTickerHub` ve `ticker` değişkenine koyar.</span><span class="sxs-lookup"><span data-stu-id="b1329-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="b1329-266">Proxy adı, öznitelik tarafından ayarlanan addır `HubName` :</span><span class="sxs-lookup"><span data-stu-id="b1329-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="b1329-267">Tüm değişkenleri ve işlevleri tanımladıktan sonra, dosyadaki kodun son satırı, SignalR işlevini çağırarak SignalR bağlantısını başlatır `start` .</span><span class="sxs-lookup"><span data-stu-id="b1329-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="b1329-268">`start`İşlev zaman uyumsuz olarak yürütülür ve [jQuery ertelenmiş nesnesini](http://api.jquery.com/category/deferred-object/)döndürür.</span><span class="sxs-lookup"><span data-stu-id="b1329-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="b1329-269">Uygulama zaman uyumsuz eylemi bitirdiğinde çağrılacak işlevi belirtmek için bitti işlevini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="b1329-270">Tüm stokları alma</span><span class="sxs-lookup"><span data-stu-id="b1329-270">Getting all the stocks</span></span>

<span data-ttu-id="b1329-271">`init`İşlevi, `getAllStocks` sunucuda işlevini çağırır ve sunucunun stok tablosunu güncelleştirmek için döndürdüğü bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="b1329-272">Varsayılan olarak, yöntem adı sunucuda Pascal-cased olsa da, istemci üzerinde Camelbüyük harfleri kullanmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b1329-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="b1329-273">Camelphı kuralı yalnızca yöntemlere uygulanır, nesneleri değil.</span><span class="sxs-lookup"><span data-stu-id="b1329-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="b1329-274">Örneğin, `stock.Symbol` ve ' a başvurursunuz `stock.Price` `stock.symbol` `stock.price` .</span><span class="sxs-lookup"><span data-stu-id="b1329-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="b1329-275">`init`Yönteminde, uygulama, `formatStock` nesnenin özelliklerini biçimlendirme ' ye çağırarak `stock` ve sonra `supplant` `rowTemplate` değişkendeki yer tutucuları nesne özelliği değerleriyle değiştirmek için çağırarak, `stock` sunucudan alınan her bir stok NESNESI için bir tablo satırı için HTML oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1329-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="b1329-276">Elde edilen HTML daha sonra hisse senedi tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="b1329-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="b1329-277">Öğesini `init` `callback` zaman uyumsuz işlev bittikten sonra yürüten bir işlev olarak geçirerek çağırın `start` .</span><span class="sxs-lookup"><span data-stu-id="b1329-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="b1329-278">Çağrıldıktan `init` sonra ayrı bir JavaScript açıklaması olarak çağrılırsa `start` , başlangıç işlevinin bağlantıyı kurmayı bitirmesini beklemeden hemen çalıştırılacağından işlev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b1329-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="b1329-279">Bu durumda, işlev, `init` `getAllStocks` uygulama bir sunucu bağlantısı oluşturmadan önce işlevi çağırmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b1329-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="b1329-280">Güncelleştirilmiş Stok fiyatları alma</span><span class="sxs-lookup"><span data-stu-id="b1329-280">Getting updated stock prices</span></span>

<span data-ttu-id="b1329-281">Sunucu bir hisse senedi fiyatını değiştirdiğinde, `updateStockPrice` bağlı istemcileri çağırır.</span><span class="sxs-lookup"><span data-stu-id="b1329-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="b1329-282">Uygulama, `stockTicker` sunucudan çağrılarla kullanılabilir hale getirmek için, işlevini proxy 'nin istemci özelliğine ekler.</span><span class="sxs-lookup"><span data-stu-id="b1329-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="b1329-283">`updateStockPrice`İşlevi, sunucudan alınan bir stok nesnesini, işlevle aynı şekilde bir tablo satırına biçimlendirir `init` .</span><span class="sxs-lookup"><span data-stu-id="b1329-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="b1329-284">Satırı tabloya eklemek yerine, stoktaki geçerli satırını bulur ve bu satırı yeni bir satır ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b1329-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="b1329-285">Uygulamayı test edin</span><span class="sxs-lookup"><span data-stu-id="b1329-285">Test the application</span></span>

<span data-ttu-id="b1329-286">Çalıştığından emin olmak için uygulamayı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="b1329-287">Tüm tarayıcı pencerelerinin, hisse senedi fiyatları dalgalanarak canlı hisse senedi tablosunu görüntülemesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b1329-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="b1329-288">Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından uygulamayı hata ayıklama modunda çalıştırmak için Yürüt düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Kullanıcı hata ayıklama modunu açıp oynat 'ı seçen kullanıcının ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="b1329-290">**Canlı hisse senedi tablosunu**görüntüleyen bir tarayıcı penceresi açılacaktır.</span><span class="sxs-lookup"><span data-stu-id="b1329-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="b1329-291">Hisse senedi tablosu başlangıçta "yükleniyor..." ardından, kısa bir süre sonra, uygulama ilk stok verilerini gösterir ve stok fiyatları değişme başlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="b1329-292">Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b1329-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="b1329-293">İlk stok görüntüsü ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="b1329-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="b1329-294">Tüm tarayıcıları kapatın, yeni bir tarayıcı açın ve aynı URL 'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="b1329-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="b1329-295">StockTicker Singleton nesnesi sunucuda çalışmaya devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="b1329-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="b1329-296">**Canlı hisse senedi tablosu** , hisse senedinin değişmeye devam etseyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="b1329-297">Sıfır değişiklik rakamlarını içeren ilk tabloyu görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="b1329-298">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="b1329-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="b1329-299">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b1329-299">Enable logging</span></span>

<span data-ttu-id="b1329-300">SignalR 'de, sorun gidermeye yardımcı olmak için istemcisinde etkinleştirebilmeniz gereken yerleşik bir günlüğe kaydetme işlevi vardır.</span><span class="sxs-lookup"><span data-stu-id="b1329-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="b1329-301">Bu bölümde, günlüğe kaydetmeyi etkinleştirir ve günlüklerin, SignalR aşağıdaki taşıma yöntemlerinden hangisini kullandığını nasıl söyletiğini gösteren örneklere bakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1329-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="b1329-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b1329-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="b1329-303">Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar](http://en.wikipedia.org/wiki/Server-sent_events).</span><span class="sxs-lookup"><span data-stu-id="b1329-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="b1329-304">Internet Explorer tarafından desteklenen [süresiz çerçeve](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe).</span><span class="sxs-lookup"><span data-stu-id="b1329-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="b1329-305">Tüm tarayıcılar tarafından desteklenen [Ajax uzun yoklama](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).</span><span class="sxs-lookup"><span data-stu-id="b1329-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="b1329-306">Verilen herhangi bir bağlantı için, SignalR hem sunucu hem de istemci tarafından desteklenen en iyi taşıma yöntemini seçer.</span><span class="sxs-lookup"><span data-stu-id="b1329-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="b1329-307">*StockTicker.js*açın.</span><span class="sxs-lookup"><span data-stu-id="b1329-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="b1329-308">Dosyanın sonunda bağlantıyı başlatan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bu vurgulanmış kod satırını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b1329-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="b1329-309">Projeyi çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b1329-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="b1329-310">Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için konsolu seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="b1329-311">Yeni bir bağlantı için taşıma yöntemiyle ilgili olarak, SignalR 'nin işlem için anlaşmasının günlüklerini görmek üzere sayfayı yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b1329-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="b1329-312">Windows 8 (IIS 8) üzerinde Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.</span><span class="sxs-lookup"><span data-stu-id="b1329-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="b1329-313">Windows 7 ' de (IIS 7,5) Internet Explorer 10 çalıştırıyorsanız, taşıma yöntemi **iframe**'dir.</span><span class="sxs-lookup"><span data-stu-id="b1329-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="b1329-314">Windows 8 (IIS 8) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.</span><span class="sxs-lookup"><span data-stu-id="b1329-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="b1329-315">Firefox 'ta, bir konsol penceresi almak için Firebug eklentisini yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="b1329-316">Windows 7 (IIS 7,5) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **sunucu tarafından gönderilen** olaylardır.</span><span class="sxs-lookup"><span data-stu-id="b1329-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="b1329-317">StockTicker örneğini yükler</span><span class="sxs-lookup"><span data-stu-id="b1329-317">Install the StockTicker sample</span></span>

<span data-ttu-id="b1329-318">[Microsoft. Aspnet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) , StockTicker uygulamasını yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="b1329-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="b1329-319">NuGet paketi sıfırdan oluşturduğunuz Basitleştirilmiş sürümden daha fazla özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="b1329-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="b1329-320">Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b1329-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1329-321">Bu öğreticinin önceki adımlarını gerçekleştirmeden paketi yüklerseniz, projenize bir OWıN başlangıç sınıfı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1329-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="b1329-322">NuGet paketi için bu readme.txt dosyası bu adımı açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1329-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="b1329-323">SignalR. Sample NuGet paketini yükler</span><span class="sxs-lookup"><span data-stu-id="b1329-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="b1329-324">**Çözüm Gezgini**, projeye sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="b1329-325">**NuGet Paket Yöneticisi: SignalR. StockTicker**' de, **Araştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="b1329-326">**Paket kaynağından** **NuGet.org**öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="b1329-327">Arama kutusuna *SignalR. Sample* girin ve **Microsoft. Aspnet. SignalR. Sample**  >  **Install**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="b1329-328">**Çözüm Gezgini**, *SignalR. Sample* klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="b1329-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="b1329-329">SignalR. Sample paketini yükleme, klasörü ve içeriğini oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="b1329-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="b1329-330">*SignalR. Sample* klasöründe, *StockTicker.html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1329-331">SignalR. Sample NuGet paketini yükleme, *Scripts* klasörünüzdeki jQuery sürümünü değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="b1329-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="b1329-332">Paketin *SignalR. Sample* klasörüne yüklediği yeni *StockTicker.html* dosyası, paketin yüklediği jQuery sürümüyle eşitlenmiş olacaktır, ancak özgün *StockTicker.html* dosyanızı yeniden çalıştırmak Istiyorsanız, önce komut dosyası etiketinde jQuery başvurusunu güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b1329-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b1329-333">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b1329-333">Run the application</span></span>

 <span data-ttu-id="b1329-334">İlk uygulamada gördüğünüz tablo yararlı özelliklere sahipti.</span><span class="sxs-lookup"><span data-stu-id="b1329-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="b1329-335">Tam hisse senedi oluşturma uygulaması yeni özellikleri gösterir: bir yatay kaydırma penceresi, renkleri arttığında ve düşecek şekilde değişen hisse senedi verilerini ve stokları gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="b1329-336">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b1329-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="b1329-337">Uygulamayı ilk kez çalıştırdığınızda, "Pazar" "kapalı" olur ve kaydırılmayan bir statik tablo ve bir Ticker penceresi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b1329-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="b1329-338">**Açık Pazar**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-338">Select **Open Market**.</span></span>

    ![Canlı Ticker 'ın ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="b1329-340">**Canlı hisse senedi bandı** , yatay olarak kaydırmaya başlar ve sunucu düzenli olarak stok fiyatı değişikliklerini rastgele bir şekilde yayınlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="b1329-341">Bir stok fiyatı her değiştiğinde uygulama hem **canlı hisse senedi tablosunu** hem de **canlı hisse senedi bandı**' ni güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b1329-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="b1329-342">Bir hisse senedinin fiyat değişikliği pozitif olduğunda, uygulama stoku yeşil bir arka plana gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="b1329-343">Değişiklik negatifse, uygulama, stoku kırmızı bir arka plana gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="b1329-344">**Pazara kapat**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="b1329-345">Tablo güncelleştirmeleri durdu.</span><span class="sxs-lookup"><span data-stu-id="b1329-345">The table updates stop.</span></span>

    * <span data-ttu-id="b1329-346">Ticker, kaydırmayı durduruyor.</span><span class="sxs-lookup"><span data-stu-id="b1329-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="b1329-347">**Sıfırla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1329-347">Select **Reset**.</span></span>

    * <span data-ttu-id="b1329-348">Tüm hisse senedi verileri sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-348">All stock data is reset.</span></span>

    * <span data-ttu-id="b1329-349">Uygulama, Fiyat değişikliklerinin başlatılmasından önce ilk durumu geri yükler.</span><span class="sxs-lookup"><span data-stu-id="b1329-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="b1329-350">Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b1329-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="b1329-351">Aynı verileri her bir tarayıcıda dinamik olarak güncelleştirilmiş şekilde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b1329-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="b1329-352">Denetimlerden herhangi birini seçtiğinizde, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b1329-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="b1329-353">Canlı hisse şeridi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b1329-353">Live Stock Ticker display</span></span>

<span data-ttu-id="b1329-354">**Canlı hisse senedi bandı** EKRANı, `<div>` CSS stilleriyle tek bir satıra biçimlendirilen bir öğe içinde sıralanmamış bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="b1329-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="b1329-355">Uygulama başlatılır ve Ticker 'ı tabloyla aynı şekilde güncelleştirir: bir şablon dizesindeki yer tutucuları değiştirerek `<li>` ve öğeleri dinamik olarak `<li>` öğesine ekler `<ul>` .</span><span class="sxs-lookup"><span data-stu-id="b1329-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="b1329-356">Uygulama `animate` , içindeki sıralanmamış listenin sol kenar boşluğunu değiştirmek Için jQuery işlevini kullanarak kaydırma içerir `<div>` .</span><span class="sxs-lookup"><span data-stu-id="b1329-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="b1329-357">SignalR. örnek StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="b1329-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="b1329-358">Stock Ticker HTML kodu:</span><span class="sxs-lookup"><span data-stu-id="b1329-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="b1329-359">SignalR. Sample StockTicker. css</span><span class="sxs-lookup"><span data-stu-id="b1329-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="b1329-360">Hisse senedi bandı CSS kodu:</span><span class="sxs-lookup"><span data-stu-id="b1329-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="b1329-361">SignalR. Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="b1329-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="b1329-362">Kaydırma yapan jQuery kodu:</span><span class="sxs-lookup"><span data-stu-id="b1329-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="b1329-363">Sunucuda istemcinin çağıra, ek Yöntemler</span><span class="sxs-lookup"><span data-stu-id="b1329-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="b1329-364">Uygulamaya esneklik eklemek için, uygulamanın çağırabilmesine ek yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="b1329-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="b1329-365">SignalR. Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="b1329-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="b1329-366">`StockTickerHub`Sınıfı, istemcinin çağırabileceğini dört ek yöntem tanımlar:</span><span class="sxs-lookup"><span data-stu-id="b1329-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="b1329-367">Uygulama, `OpenMarket` `CloseMarket` , ve `Reset` sayfanın en üstündeki düğmelere yanıt olarak çağırır.</span><span class="sxs-lookup"><span data-stu-id="b1329-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="b1329-368">Tüm istemcilere anında yayılmış durumdaki bir değişikliği tetikleyen bir istemcinin modelini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1329-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="b1329-369">Bu yöntemlerin her biri, bir `StockTicker` sınıf içinde piyasa durumu değişikliğine neden olan bir yöntemi çağırır ve sonra yeni durumu yayınlar.</span><span class="sxs-lookup"><span data-stu-id="b1329-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="b1329-370">SignalR. Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="b1329-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="b1329-371">`StockTicker`Sınıfında, uygulama `MarketState` bir sabit listesi değeri döndüren bir özellik ile Pazar durumunu korur `MarketState` :</span><span class="sxs-lookup"><span data-stu-id="b1329-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="b1329-372">Pazar durumunu değiştiren yöntemlerin her biri, `StockTicker` sınıfın iş parçacığı açısından güvenli olması gerektiğinden bir kilit bloğunun içinde olur:</span><span class="sxs-lookup"><span data-stu-id="b1329-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="b1329-373">Bu kodun iş parçacığı açısından güvenli olduğundan emin olmak için, `_marketState` belirtilen özelliği yedekleyen alan `MarketState` `volatile` :</span><span class="sxs-lookup"><span data-stu-id="b1329-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="b1329-374">`BroadcastMarketStateChange`Ve `BroadcastMarketReset` yöntemleri, zaten gördüğünüz BroadcastStockPrice yöntemine benzerdir, ancak istemcide tanımlı farklı Yöntemler çağırır:</span><span class="sxs-lookup"><span data-stu-id="b1329-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="b1329-375">İstemcinin çağıra, istemci üzerinde ek işlevler</span><span class="sxs-lookup"><span data-stu-id="b1329-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="b1329-376">`updateStockPrice`İşlev artık hem tabloyu hem de Ticker görüntüsünü işler ve `jQuery.Color` kırmızı ve yeşil renkleri Flash için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="b1329-377">*SignalR.StockTicker.js* yeni işlevler, Pazar durumuna göre düğmeleri etkinleştirir ve devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="b1329-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="b1329-378">Ayrıca **canlı hisse senedi bandı** yatay kaydırmayı da durdurur veya başlatır.</span><span class="sxs-lookup"><span data-stu-id="b1329-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="b1329-379">Uygulamasına birçok işlev eklendiğinden `ticker.client` , uygulama bunları eklemek Için [jQuery genişletme işlevini](http://api.jquery.com/jQuery.extend/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1329-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="b1329-380">Bağlantı kurulduktan sonra ek istemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="b1329-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="b1329-381">İstemci bağlantıyı belirledikten sonra, yapılacak bazı ek işler de vardır:</span><span class="sxs-lookup"><span data-stu-id="b1329-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="b1329-382">Uygun veya işlevi çağırmak için pazar açık veya kapalı olduğunu öğrenin `marketOpened` `marketClosed` .</span><span class="sxs-lookup"><span data-stu-id="b1329-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="b1329-383">Düğmelerine sunucu yöntemi çağrılarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1329-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="b1329-384">Sunucu yöntemleri, uygulama bağlantıyı yapana kadar düğmelere bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="b1329-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="b1329-385">Bu, kodun kullanılabilir hale gelmeden önce sunucu yöntemlerine çağrı yapamıyor.</span><span class="sxs-lookup"><span data-stu-id="b1329-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1329-386">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b1329-386">Additional resources</span></span>

<span data-ttu-id="b1329-387">Bu öğreticide, sunucudan bağlı olan tüm istemcilere ileti veren bir SignalR uygulamasını nasıl programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="b1329-388">Artık iletileri düzenli aralıklarla ve herhangi bir istemciden gelen bildirimlere yanıt olarak yayınlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="b1329-389">Çoklu iş parçacıklı tekil örnek kavramını kullanarak, çok oyunculu çevrimiçi oyun senaryolarında sunucu durumunu koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1329-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="b1329-390">Bir örnek için bkz. [SignalR tabanlı ShootR oyunu](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="b1329-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="b1329-391">Eşler arası iletişim senaryolarını gösteren öğreticiler için bkz. [SignalR Ile çalışmaya](introduction-to-signalr.md) başlama ve [SignalR Ile gerçek zamanlı güncelleştirme](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="b1329-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="b1329-392">SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="b1329-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="b1329-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="b1329-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="b1329-394">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="b1329-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="b1329-395">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="b1329-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="b1329-396">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="b1329-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="b1329-397">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1329-397">Next steps</span></span>

<span data-ttu-id="b1329-398">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="b1329-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1329-399">Proje oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b1329-399">Created the project</span></span>
> * <span data-ttu-id="b1329-400">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-400">Set up the server code</span></span>
> * <span data-ttu-id="b1329-401">Sunucu kodu incelendi</span><span class="sxs-lookup"><span data-stu-id="b1329-401">Examined the server code</span></span>
> * <span data-ttu-id="b1329-402">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1329-402">Set up the client code</span></span>
> * <span data-ttu-id="b1329-403">İstemci kodu incelendi</span><span class="sxs-lookup"><span data-stu-id="b1329-403">Examined the client code</span></span>
> * <span data-ttu-id="b1329-404">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="b1329-404">Tested the application</span></span>
> * <span data-ttu-id="b1329-405">Etkin günlük kaydı</span><span class="sxs-lookup"><span data-stu-id="b1329-405">Enabled logging</span></span>

<span data-ttu-id="b1329-406">ASP.NET SignalR 2 kullanan gerçek zamanlı bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="b1329-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b1329-407">SignalR ile gerçek zamanlı web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1329-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
