---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Öğretici: SignalR 2 ile Sunucu yayını | Microsoft Dokümanlar'
author: tdykstra
description: Bu öğretici, sunucu yayını işlevselliğini sağlamak için ASP.NET SignalR 2 kullanan bir web uygulamasının nasıl oluşturulacağını gösterir.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676099"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="98c29-103">Öğretici: SignalR 2 ile sunucu yayını</span><span class="sxs-lookup"><span data-stu-id="98c29-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="98c29-104">Bu öğretici, sunucu yayını işlevselliğini sağlamak için ASP.NET SignalR 2 kullanan bir web uygulamasının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c29-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="98c29-105">Sunucu yayını, sunucunun istemcilere gönderilen iletişimi başlattığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="98c29-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="98c29-106">Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir hisse senedi işaretleyicisini simüle eder.</span><span class="sxs-lookup"><span data-stu-id="98c29-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="98c29-107">Düzenli olarak, sunucu hisse senedi fiyatlarını rasgele günceller ve güncelleştirmeleri bağlı tüm istemcilere yayınlar.</span><span class="sxs-lookup"><span data-stu-id="98c29-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="98c29-108">Tarayıcıda, **Değiştir** ve sütunlarda bulunan **%** sayılar ve semboller, sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="98c29-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="98c29-109">Aynı URL'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c29-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Web oluşturma](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="98c29-111">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="98c29-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98c29-112">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="98c29-112">Create the project</span></span>
> * <span data-ttu-id="98c29-113">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-113">Set up the server code</span></span>
> * <span data-ttu-id="98c29-114">Sunucu kodunu inceleme</span><span class="sxs-lookup"><span data-stu-id="98c29-114">Examine the server code</span></span>
> * <span data-ttu-id="98c29-115">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-115">Set up the client code</span></span>
> * <span data-ttu-id="98c29-116">İstemci kodunu inceleyin</span><span class="sxs-lookup"><span data-stu-id="98c29-116">Examine the client code</span></span>
> * <span data-ttu-id="98c29-117">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="98c29-117">Test the application</span></span>
> * <span data-ttu-id="98c29-118">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="98c29-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98c29-119">Uygulamayı oluşturma adımlarını gözden geçirmek istemiyorsanız, SignalR.Sample paketini yeni bir Boş ASP.NET Web Uygulaması projesine yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="98c29-120">NuGet paketini bu öğreticideki adımları gerçekleştirmeden yüklerseniz, *readme.txt* dosyasındaki yönergeleri izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="98c29-121">Paketi çalıştırmak için, yüklenen paketteki `ConfigureSignalR` yöntemi çağıran bir OWIN başlangıç sınıfı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="98c29-122">OWIN başlangıç sınıfını eklemezseniz bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="98c29-123">Bu [makalenin StockTicker örnek bölümüne yükleyin](#install-the-stockticker-sample) bakın.</span><span class="sxs-lookup"><span data-stu-id="98c29-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98c29-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="98c29-124">Prerequisites</span></span>

* <span data-ttu-id="98c29-125">**ASP.NET ve web geliştirme** iş yüküyle [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="98c29-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="98c29-126">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="98c29-126">Create the project</span></span>

<span data-ttu-id="98c29-127">Bu bölümde, boş bir ASP.NET Web Uygulaması oluşturmak için Visual Studio 2017'nin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98c29-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="98c29-128">Visual Studio'da bir ASP.NET Web Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98c29-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web oluşturma](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="98c29-130">Yeni **ASP.NET Web Uygulaması - SignalR.StockTicker** penceresinde, **Boş** seçili bırakın ve **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="98c29-131">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-131">Set up the server code</span></span>

<span data-ttu-id="98c29-132">Bu bölümde, sunucuda çalışan kodu ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="98c29-133">Stok sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="98c29-133">Create the Stock class</span></span>

<span data-ttu-id="98c29-134">Stok hakkındaki bilgileri depolamak ve iletmek için kullanacağınız *Stok* modeli sınıfını oluşturarak başlarsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="98c29-135">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Sınıf** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="98c29-136">Sınıf *Stok'u* adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98c29-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="98c29-137">*Stock.cs* dosyasındaki kodu bu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98c29-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="98c29-138">Hisse senetleri oluştururken ayarladığınız iki `Symbol` özellik (örneğin, Microsoft için `Price`MSFT) ve .</span><span class="sxs-lookup"><span data-stu-id="98c29-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="98c29-139">Diğer özellikler nasıl ve ne `Price`zaman ayarladığınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="98c29-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="98c29-140">İlk olarak ayarlağınızda, `Price`değer `DayOpen`' e yayılır.</span><span class="sxs-lookup"><span data-stu-id="98c29-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="98c29-141">Bundan sonra, ayarladığınızda, `Price`uygulama ve `Change` `PercentChange` arasındaki `Price` farka göre özellik `DayOpen`değerlerini hesaplar.</span><span class="sxs-lookup"><span data-stu-id="98c29-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="98c29-142">StockTickerHub ve StockTicker sınıflarını oluşturun</span><span class="sxs-lookup"><span data-stu-id="98c29-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="98c29-143">Sunucudan istemciye etkileşimi işlemek için SignalR Hub API'sını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="98c29-144">SignalR `StockTickerHub` `Hub` sınıfından türeyen bir sınıf, istemcilerden bağlantı ve yöntem çağrıları alma işlemlerini işler.</span><span class="sxs-lookup"><span data-stu-id="98c29-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="98c29-145">Ayrıca stok verilerini korumak ve `Timer` bir nesne çalıştırmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="98c29-146">Nesne, `Timer` istemci bağlantılarından bağımsız olarak düzenli olarak fiyat güncelleştirmelerini tetikler.</span><span class="sxs-lookup"><span data-stu-id="98c29-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="98c29-147">Hub'lar geçici olduğundan, `Hub` bu işlevleri bir sınıfa koyamazsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="98c29-148">Uygulama, istemciden `Hub` sunucuya bağlantılar ve aramalar gibi hub'daki her görev için bir sınıf örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98c29-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="98c29-149">Bu nedenle, stok verilerini tutan, fiyatları güncelleyen ve fiyat güncelleştirmelerini yayınlayan mekanizmanın ayrı bir sınıfta çalışması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="98c29-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="98c29-150">Sınıfa `StockTicker`isim vereceksin.</span><span class="sxs-lookup"><span data-stu-id="98c29-150">You'll name the class `StockTicker`.</span></span>

![StockTicker'dan Yayın](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="98c29-152">`StockTicker` Sınıfın yalnızca bir örneğinin sunucuda çalışmasını istiyorsunuz, bu nedenle her `StockTickerHub` örnekten singleton `StockTicker` örneğine bir başvuru ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="98c29-153">Sınıf, `StockTicker` stok verilerine sahip olduğundan ve güncelleştirmeleri tetiklediği `StockTicker` için istemcilere yayın yapmak zorundadır, ancak bir `Hub` sınıf değildir.</span><span class="sxs-lookup"><span data-stu-id="98c29-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="98c29-154">Sınıfın `StockTicker` SignalR Hub bağlantı bağlamı nesnesine bir başvuru alması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="98c29-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="98c29-155">Daha sonra istemcilere yayın için SignalR bağlantı bağlamı nesnesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="98c29-156">StockTickerHub.cs oluşturma</span><span class="sxs-lookup"><span data-stu-id="98c29-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="98c29-157">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Yeni Öğe** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="98c29-158">**Yeni Öğe Ekle - SignalR.StockTicker**, **Yüklü** > **Görsel C#** > **Web** > **SignalR'ı** seçin ve ardından **SignalR Hub Sınıfı'nı (v2)** seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="98c29-159">*StockTickerHub* sınıfının adını ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98c29-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="98c29-160">Bu adım, *StockTickerHub.cs* sınıf dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98c29-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="98c29-161">Aynı anda, projeye SignalR'ı destekleyen bir dizi komut dosyası dosyası ve derleme başvurusu ekler.</span><span class="sxs-lookup"><span data-stu-id="98c29-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="98c29-162">*StockTickerHub.cs* dosyasındaki kodu bu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98c29-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="98c29-163">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="98c29-163">Save the file.</span></span>

<span data-ttu-id="98c29-164">Uygulama, istemcilerin sunucuda çağırabileceği yöntemleri tanımlamak için [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="98c29-165">Bir yöntem tanımlıyorsunuz: `GetAllStocks()`.</span><span class="sxs-lookup"><span data-stu-id="98c29-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="98c29-166">Bir istemci başlangıçta sunucuya bağlandığında, geçerli fiyatları ile tüm hisse senetlerinin bir listesini almak için bu yöntemi arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="98c29-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="98c29-167">Yöntem eşzamanlı olarak çalıştırılabilir `IEnumerable<Stock>` ve bellekten veri döndürdeğinden döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="98c29-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="98c29-168">Yöntem, veritabanı araması veya web hizmeti çağrısı gibi beklemeyi gerektirecek bir şey yaparak verileri `Task<IEnumerable<Stock>>` almak zorunda kaldıysa, eşzamanlı işlemeyi etkinleştirmek için iade değeri olarak belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="98c29-169">Daha fazla bilgi için [SignalR Hub'ASP.NET API Kılavuzu - Sunucu - Ne zaman eşzamanlı olarak yürütülmesi gerektiğini](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)görün.</span><span class="sxs-lookup"><span data-stu-id="98c29-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="98c29-170">Öznitelik, `HubName` uygulamanın istemcideki JavaScript kodundaki Hub'a nasıl başvurulacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="98c29-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="98c29-171">Bu özniteliği kullanmazsanız istemcideki varsayılan ad, sınıf adının camelCase sürümüdür ve bu durumda `stockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="98c29-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="98c29-172">`StockTicker` Sınıfı oluşturduğunuzda daha sonra göreceğiniz gibi, uygulama statik `Instance` özelliğinde bu sınıfın tek tonluk bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98c29-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="98c29-173">Bu singleton `StockTicker` örneği, kaç istemci bağlanır veya bağlantıyı keserse bağlansın bellektedir.</span><span class="sxs-lookup"><span data-stu-id="98c29-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="98c29-174">Bu örnek, `GetAllStocks()` yöntemin geçerli stok bilgilerini döndürmek için kullandığı örnektir.</span><span class="sxs-lookup"><span data-stu-id="98c29-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="98c29-175">StockTicker.cs oluştur</span><span class="sxs-lookup"><span data-stu-id="98c29-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="98c29-176">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Sınıf** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="98c29-177">*StockTicker* sınıfının adını ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98c29-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="98c29-178">*StockTicker.cs* dosyasındaki kodu bu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98c29-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="98c29-179">Tüm iş parçacıkları StockTicker kodunun aynı örneğini çalıştıracağı için StockTicker sınıfının iş parçacığı açısından güvenli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="98c29-180">Sunucu kodunu inceleme</span><span class="sxs-lookup"><span data-stu-id="98c29-180">Examine the server code</span></span>

<span data-ttu-id="98c29-181">Sunucu kodunu incelerseniz, uygulamanın nasıl çalıştığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="98c29-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="98c29-182">Tekton örneğini statik bir alanda depolama</span><span class="sxs-lookup"><span data-stu-id="98c29-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="98c29-183">Kod, `Instance` özelliği destekleyen `_instance` statik alanı sınıfın bir örneğiyle birlikte baş harfe döndürer.</span><span class="sxs-lookup"><span data-stu-id="98c29-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="98c29-184">Oluşturucu özel olduğundan, uygulamanın oluşturabileceği tek örnektir.</span><span class="sxs-lookup"><span data-stu-id="98c29-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="98c29-185">Uygulama `_instance` alan için [Lazy başlatma](/dotnet/framework/performance/lazy-initialization) kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="98c29-186">Performans nedenlerinden dolayı değil.</span><span class="sxs-lookup"><span data-stu-id="98c29-186">It's not for performance reasons.</span></span> <span data-ttu-id="98c29-187">Örnek oluşturmanın iş parçacığı için güvenli olduğundan emin olmak içindir.</span><span class="sxs-lookup"><span data-stu-id="98c29-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="98c29-188">Bir istemci sunucuya her bağlandığında, ayrı bir iş parçacığıiçinde çalışan StockTickerHub sınıfının yeni bir `StockTicker.Instance` örneği, `StockTickerHub` daha önce sınıfta gördüğünüz gibi StockTicker singleton örneğini statik özellikten alır.</span><span class="sxs-lookup"><span data-stu-id="98c29-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="98c29-189">Stok verilerinin Eşzamanlı Sözlük'te saklanması</span><span class="sxs-lookup"><span data-stu-id="98c29-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="98c29-190">Oluşturucu, koleksiyonu bazı `_stocks` örnek stok verileriyle `GetAllStocks` başolarak alır ve stokları döndürür.</span><span class="sxs-lookup"><span data-stu-id="98c29-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="98c29-191">Daha önce de gördüğünüz gibi, bu `StockTickerHub.GetAllStocks`hisse senetleri koleksiyonu, `Hub` istemcilerin çağırabileceği sınıftaki bir sunucu yöntemi olan tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="98c29-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="98c29-192">Stoktoplama iş parçacığı güvenliği için [EşzamanlıSözlük](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="98c29-193">Alternatif olarak, [sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve sözlükte değişiklik yaptığınızda sözlüğü açıkça kilitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="98c29-194">Bu örnek uygulama için, uygulama verilerini bellekte depolamak ve uygulama `StockTicker` örneği attığında verileri kaybetmek sorun değil.</span><span class="sxs-lookup"><span data-stu-id="98c29-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="98c29-195">Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposu yla çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="98c29-196">Hisse senedi fiyatlarını periyodik olarak güncelleme</span><span class="sxs-lookup"><span data-stu-id="98c29-196">Periodically updating stock prices</span></span>

<span data-ttu-id="98c29-197">Oluşturucu, hisse `Timer` senedi fiyatlarını rasgele güncelleştiren yöntemleri düzenli olarak çağıran bir nesne başlatır.</span><span class="sxs-lookup"><span data-stu-id="98c29-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="98c29-198">`Timer`aramalar `UpdateStockPrices`, durum parametresi null geçer.</span><span class="sxs-lookup"><span data-stu-id="98c29-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="98c29-199">Fiyatları güncellemeden önce, uygulama nesneye `_updateStockPricesLock` kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="98c29-200">Kod, başka bir iş parçacığının fiyatları zaten `TryUpdateStockPrice` güncelleştirip güncellediğini denetler ve ardından listedeki her hisse senedini çağırır.</span><span class="sxs-lookup"><span data-stu-id="98c29-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="98c29-201">Yöntem, `TryUpdateStockPrice` hisse senedi fiyatını değiştirip değiştirmeyeceğine ve ne kadar değiştireceğinize karar verir.</span><span class="sxs-lookup"><span data-stu-id="98c29-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="98c29-202">Hisse senedi fiyatı değişirse, uygulama hisse senedi fiyat değişikliğini bağlı tüm istemcilere yayınlamayı çağırır. `BroadcastStockPrice`</span><span class="sxs-lookup"><span data-stu-id="98c29-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="98c29-203">İş `_updatingStockPrices` parçacığı güvenli olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak atanan bayrak.</span><span class="sxs-lookup"><span data-stu-id="98c29-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="98c29-204">Gerçek bir uygulamada, `TryUpdateStockPrice` yöntem fiyat aramak için bir web hizmeti çağırır.</span><span class="sxs-lookup"><span data-stu-id="98c29-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="98c29-205">Bu kodda, uygulama rasgele değişiklik yapmak için rasgele bir sayı üreteci kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="98c29-206">StockTicker sınıfının istemcilere yayın yapabilmesi için SignalR bağlamını alma</span><span class="sxs-lookup"><span data-stu-id="98c29-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="98c29-207">Fiyat değişiklikleri burada `StockTicker` nesne kaynaklı olduğundan, tüm bağlı istemcilerde bir `updateStockPrice` yöntem çağırmak için gereken nesnedir.</span><span class="sxs-lookup"><span data-stu-id="98c29-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="98c29-208">Bir `Hub` sınıfta, istemci yöntemlerini aramak için bir `StockTicker` API'niz vardır, ancak `Hub` sınıftan türeyen `Hub` ve herhangi bir nesneye başvurunuz yoktur.</span><span class="sxs-lookup"><span data-stu-id="98c29-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="98c29-209">Bağlı istemcilere yayın `StockTicker` yapmak için sınıfın sınıf için SignalR bağlam örneğini `StockTickerHub` alması ve istemcilere yönelik yöntemleri aramak için bunu kullanması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="98c29-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="98c29-210">Kod, tekton sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya `Clients` geçirir ve oluşturucu onu özelliğe koyar.</span><span class="sxs-lookup"><span data-stu-id="98c29-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="98c29-211">Bağlamı yalnızca bir kez almak istemenizin iki nedeni vardır: bağlamı almak pahalı bir görevdir ve bir kez almak, uygulamanın istemcilere gönderilen iletilerin amaçlanan sırasını koruduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="98c29-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="98c29-212">Bağlamın `Clients` özelliğini almak ve `StockTickerClient` özelliğine koymak, `Hub` bir sınıfta olduğu gibi görünen istemci yöntemlerini aramak için kod yazmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="98c29-213">Örneğin, tüm istemcilere yayın için `Clients.All.updateStockPrice(stock)`yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="98c29-214">Aradığınız `updateStockPrice` `BroadcastStockPrice` yöntem henüz yok.</span><span class="sxs-lookup"><span data-stu-id="98c29-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="98c29-215">İstemci üzerinde çalışan kod yazarken daha sonra eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="98c29-216">Dinamik `Clients.All` olduğu `updateStockPrice` için buraya başvurabilirsiniz, bu da uygulamanın çalışma zamanında ifadeyi değerlendireceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="98c29-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="98c29-217">Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve `updateStockPrice`istemcide adlı bir yöntem varsa, uygulama bu yöntemi çağırır ve parametre değerini ona geçirir.</span><span class="sxs-lookup"><span data-stu-id="98c29-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="98c29-218">`Clients.All`tüm istemcilere göndermek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="98c29-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="98c29-219">SignalR, hangi istemcilere veya istemci gruplarına gönderilecini belirtmeniz için başka seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="98c29-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="98c29-220">Daha fazla bilgi için [HubConnectionContext'a](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="98c29-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="98c29-221">SignalR rotasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="98c29-221">Register the SignalR route</span></span>

<span data-ttu-id="98c29-222">Sunucunun hangi URL'yi yakalayıp SignalR'a yönlendirecek olduğunu bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="98c29-223">Bunu yapmak için bir OWIN başlangıç sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="98c29-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="98c29-224">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve**Yeni Öğe** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="98c29-225">**Yeni Öğe Ekle - SignalR.StockTicker** **Yüklü** > **Visual C#** > **Web'i** seçin ve ardından **OWIN Başlangıç Sınıfı'nı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="98c29-226">*Sınıf Başlangıç* adını ve **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="98c29-227">*Startup.cs* dosyasındaki varsayılan kodu bu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98c29-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="98c29-228">Sunucu kodunu ayarlamayı tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="98c29-229">Bir sonraki bölümde istemciyi ayarla.</span><span class="sxs-lookup"><span data-stu-id="98c29-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="98c29-230">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-230">Set up the client code</span></span>

<span data-ttu-id="98c29-231">Bu bölümde, istemci üzerinde çalışan kodu ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="98c29-232">HTML sayfasını ve JavaScript dosyasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="98c29-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="98c29-233">HTML sayfası verileri görüntüler ve JavaScript dosyası verileri düzenler.</span><span class="sxs-lookup"><span data-stu-id="98c29-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="98c29-234">StockTicker.html oluştur</span><span class="sxs-lookup"><span data-stu-id="98c29-234">Create StockTicker.html</span></span>

<span data-ttu-id="98c29-235">İlk olarak, HTML istemcisini eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="98c29-236">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve**HTML Sayfası** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="98c29-237">*StockTicker* dosyasını adlandırın ve **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="98c29-238">*StockTicker.html* dosyasındaki varsayılan kodu bu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98c29-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="98c29-239">HTML, beş sütun, üstbilgi satırı ve beş sütunun tümine yayılan tek bir hücreye sahip bir veri satırı içeren bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98c29-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="98c29-240">Veri satırı "yükleme..." uygulama başladığında anlık olarak.</span><span class="sxs-lookup"><span data-stu-id="98c29-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="98c29-241">JavaScript kodu bu satırı kaldırır ve sunucudan alınan stok verileriyle yer satırları ekler.</span><span class="sxs-lookup"><span data-stu-id="98c29-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="98c29-242">Komut dosyası etiketleri şunları belirtir:</span><span class="sxs-lookup"><span data-stu-id="98c29-242">The script tags specify:</span></span>

    * <span data-ttu-id="98c29-243">jQuery komut dosyası dosyası.</span><span class="sxs-lookup"><span data-stu-id="98c29-243">The jQuery script file.</span></span>

    * <span data-ttu-id="98c29-244">SignalR çekirdek komut dosyası dosyası.</span><span class="sxs-lookup"><span data-stu-id="98c29-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="98c29-245">SignalR komut dosyası dosyasını vekiller.</span><span class="sxs-lookup"><span data-stu-id="98c29-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="98c29-246">Daha sonra oluşturacağınız StockTicker komut dosyası dosyası.</span><span class="sxs-lookup"><span data-stu-id="98c29-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="98c29-247">Uygulama dinamik olarak SignalR yakınlık komut dosyası dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98c29-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="98c29-248">"/signalr/hub" URL'sini belirtir ve Hub sınıfındaki yöntemler için `StockTickerHub.GetAllStocks`proxy yöntemleri tanımlar, bu durumda, için.</span><span class="sxs-lookup"><span data-stu-id="98c29-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="98c29-249">İsterseniz, [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)kullanarak bu JavaScript dosyayı el ile oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="98c29-250">Yöntem çağrısında dinamik dosya oluşturmayı `MapHubs` devre dışı etmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="98c29-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="98c29-251">**Çözüm Gezgini'nde,** **Komut Dosyalarını**genişletin.</span><span class="sxs-lookup"><span data-stu-id="98c29-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="98c29-252">JQuery ve SignalR için komut dosyası kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="98c29-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="98c29-253">Paket yöneticisi SignalR komut dosyalarının daha sonraki bir sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="98c29-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="98c29-254">Kod bloğundaki komut dosyası başvurularını projedeki komut dosyası dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="98c29-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="98c29-255">**Solution Explorer'da** *StockTicker.html'e*sağ tıklayın ve ardından **Başlangıç Sayfası olarak Ayarla'yı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="98c29-256">StockTicker.js oluştur</span><span class="sxs-lookup"><span data-stu-id="98c29-256">Create StockTicker.js</span></span>

<span data-ttu-id="98c29-257">Şimdi JavaScript dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98c29-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="98c29-258">**Solution Explorer'da**projeyi sağ tıklatın ve**JavaScript Dosyası** **Ekle'yi** > seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="98c29-259">*StockTicker* dosyasını adlandırın ve **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="98c29-260">Bu kodu *StockTicker.js* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="98c29-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="98c29-261">İstemci kodunu inceleyin</span><span class="sxs-lookup"><span data-stu-id="98c29-261">Examine the client code</span></span>

<span data-ttu-id="98c29-262">İstemci kodunu incelerseniz, uygulamanın çalışmasını sağlamak için istemci kodunun sunucu koduyla nasıl etkileşimde olduğunu öğrenmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="98c29-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="98c29-263">Bağlantıyı başlatma</span><span class="sxs-lookup"><span data-stu-id="98c29-263">Starting the connection</span></span>

<span data-ttu-id="98c29-264">`$.connection`SignalR yakınlıklarını ifade eder.</span><span class="sxs-lookup"><span data-stu-id="98c29-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="98c29-265">Kod `StockTickerHub` sınıf için proxy bir başvuru alır ve `ticker` değişken koyar.</span><span class="sxs-lookup"><span data-stu-id="98c29-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="98c29-266">Proxy adı öznitelik tarafından `HubName` ayarlanan addır:</span><span class="sxs-lookup"><span data-stu-id="98c29-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="98c29-267">Tüm değişkenleri ve işlevleri tanımladıktan sonra, dosyadaki son kod satırı SignalR `start` işlevini çağırarak SignalR bağlantısını açar.</span><span class="sxs-lookup"><span data-stu-id="98c29-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="98c29-268">İşlev `start` eşsenkronize yürütür ve [bir jQuery Ertelenmiş nesne](http://api.jquery.com/category/deferred-object/)döndürür.</span><span class="sxs-lookup"><span data-stu-id="98c29-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="98c29-269">Uygulama asynchronous eylemi bittiğinde aranacak işlevi belirtmek için yapılan işlevi arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="98c29-270">Tüm hisse senetlerialma</span><span class="sxs-lookup"><span data-stu-id="98c29-270">Getting all the stocks</span></span>

<span data-ttu-id="98c29-271">İşlev `init` sunucudaki `getAllStocks` işlevi çağırır ve stok tablosunu güncelleştirmek için sunucunun döndürdettiği bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="98c29-272">Varsayılan olarak, yöntem adı sunucuda pascal-cased olsa bile istemci üzerinde camelCasing kullanmanız gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="98c29-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="98c29-273">CamelCasing kuralı sadece yöntemler için geçerlidir, nesneler için değil.</span><span class="sxs-lookup"><span data-stu-id="98c29-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="98c29-274">Örneğin, başvurur `stock.Symbol` ve `stock.Price`, `stock.symbol` `stock.price`değil veya .</span><span class="sxs-lookup"><span data-stu-id="98c29-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="98c29-275">`init` `formatStock` Yöntemde, uygulama, `stock` nesnenin özelliklerini biçimlendirmek için arayarak sunucudan alınan her stok nesnesi `supplant` için bir tablo `rowTemplate` satırı için `stock` HTML oluşturur ve ardından değişkendeki yer tutucuları nesne özellik değerleriyle değiştirmek için çağrıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="98c29-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="98c29-276">Elde edilen HTML daha sonra stok tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="98c29-277">Asynchronous `init` `start` işlevi bittikten sonra çalıştırılabilen bir `callback` işlev olarak geçirerek çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="98c29-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="98c29-278">Aradıktan `init` sonra ayrı bir JavaScript `start`deyimi olarak adlandırılan , bağlantı kurmayı bitirmek için başlangıç işlevi beklemeden hemen çalışacak çünkü işlev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="98c29-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="98c29-279">Bu durumda, `init` işlev, uygulama bir `getAllStocks` sunucu bağlantısı kurmadan önce işlevi çağırmayı dener.</span><span class="sxs-lookup"><span data-stu-id="98c29-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="98c29-280">Güncellenmiş hisse senedi fiyatları alma</span><span class="sxs-lookup"><span data-stu-id="98c29-280">Getting updated stock prices</span></span>

<span data-ttu-id="98c29-281">Sunucu bir hisse senedinin fiyatını değiştirdiğinde, bağlı istemcileri `updateStockPrice` çağırır.</span><span class="sxs-lookup"><span data-stu-id="98c29-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="98c29-282">Uygulama, sunucudan gelen aramalariçin `stockTicker` kullanılabilir hale getirmek için proxy istemci özelliğine işlevi ekler.</span><span class="sxs-lookup"><span data-stu-id="98c29-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="98c29-283">İşlev, `updateStockPrice` sunucudan alınan stok nesnesini `init` işlevdeki yle aynı şekilde bir tablo satırına biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="98c29-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="98c29-284">Satırı tabloya eklemek yerine, tabloda stokun geçerli satırını bulur ve bu satırı yenisiyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="98c29-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="98c29-285">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="98c29-285">Test the application</span></span>

<span data-ttu-id="98c29-286">Çalıştığından emin olmak için uygulamayı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="98c29-287">Tüm tarayıcı pencerelerini hisse senedi fiyatları dalgalanan canlı stok tablogörüntülemek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="98c29-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="98c29-288">Araç çubuğunda, **Komut Dosyası Hata Ayıklama'yı** açın ve uygulamayı Hata Ayıklama modunda çalıştırmak için oynat düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Hata ayıklama modunu ve oynat'ı seçen kullanıcının ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="98c29-290">**Canlı Stok Tablosunu**gösteren bir tarayıcı penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="98c29-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="98c29-291">Stok tablosu başlangıçta "yükleme" gösterir. satır, daha sonra, kısa bir süre sonra, uygulama ilk hisse senedi verilerini gösterir ve sonra hisse senedi fiyatları değişmeye başlar.</span><span class="sxs-lookup"><span data-stu-id="98c29-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="98c29-292">URL'yi tarayıcıdan kopyalayın, diğer iki tarayıcıyı açın ve URL'leri adres çubuklarına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="98c29-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="98c29-293">İlk stok ekranı ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="98c29-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="98c29-294">Tüm tarayıcıları kapatın, yeni bir tarayıcı açın ve aynı URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="98c29-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="98c29-295">StockTicker singleton nesnesi sunucuda çalıştırmaya devam etti.</span><span class="sxs-lookup"><span data-stu-id="98c29-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="98c29-296">**Canlı Stok Tablosu** hisse senetlerinin değişmeye devam ettiğini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="98c29-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="98c29-297">İlk tabloyu sıfır değişiklik rakamlarıyla göremezsin.</span><span class="sxs-lookup"><span data-stu-id="98c29-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="98c29-298">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="98c29-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="98c29-299">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="98c29-299">Enable logging</span></span>

<span data-ttu-id="98c29-300">SignalR, istemcinin sorun gidermede yardımcı olmasını etkinleştirebileceğiniz yerleşik bir günlük işlevine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="98c29-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="98c29-301">Bu bölümde, signalr'in aşağıdaki aktarım yöntemlerinden hangisini kullandığını günlüklerin size nasıl söylediğini gösteren günlük günlüğe kaydetmeyi ve örnekleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="98c29-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="98c29-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="98c29-303">Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar.](http://en.wikipedia.org/wiki/Server-sent_events)</span><span class="sxs-lookup"><span data-stu-id="98c29-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="98c29-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="98c29-305">[Ajax uzun yoklama,](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)tüm tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="98c29-306">Herhangi bir bağlantı için SignalR, hem sunucunun hem de istemcinin desteklediği en iyi aktarım yöntemini seçer.</span><span class="sxs-lookup"><span data-stu-id="98c29-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="98c29-307">Açık *StockTicker.js*.</span><span class="sxs-lookup"><span data-stu-id="98c29-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="98c29-308">Dosyanın sonundaki bağlantıyı açan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bu vurgulanmış kod satırını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="98c29-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="98c29-309">Projeyi çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="98c29-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="98c29-310">Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için Konsol'u seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="98c29-311">SignalR'ın yeni bir bağlantı için aktarım yöntemini müzakere eden günlüklerini görmek için sayfayı yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="98c29-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="98c29-312">Windows 8'de (IIS 8) Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **WebSockets'tir.**</span><span class="sxs-lookup"><span data-stu-id="98c29-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="98c29-313">Windows 7'de (IIS 7.5) Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **iframe'dir.**</span><span class="sxs-lookup"><span data-stu-id="98c29-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="98c29-314">Windows 8'de Firefox 19 çalıştırıyorsanız (IIS 8), aktarım yöntemi **WebSockets'tir.**</span><span class="sxs-lookup"><span data-stu-id="98c29-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="98c29-315">Firefox'ta, Konsol penceresi almak için Firebug eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="98c29-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="98c29-316">Firefox 19'u Windows 7'de (IIS 7.5) çalıştırıyorsanız, aktarım yöntemi **sunucu tarafından gönderilen** olaylardır.</span><span class="sxs-lookup"><span data-stu-id="98c29-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="98c29-317">StockTicker örneğini yükleyin</span><span class="sxs-lookup"><span data-stu-id="98c29-317">Install the StockTicker sample</span></span>

<span data-ttu-id="98c29-318">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker uygulamasını yükler.</span><span class="sxs-lookup"><span data-stu-id="98c29-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="98c29-319">NuGet paketi, sıfırdan oluşturduğunuz basitleştirilmiş sürümden daha fazla özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="98c29-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="98c29-320">Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="98c29-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98c29-321">Paketi bu öğreticinin önceki adımlarını gerçekleştirmeden yüklerseniz, projenize bir OWIN başlangıç sınıfı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="98c29-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="98c29-322">NuGet paketi için bu readme.txt dosyası bu adımı açıklar.</span><span class="sxs-lookup"><span data-stu-id="98c29-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="98c29-323">SignalR.Sample NuGet paketini yükleyin</span><span class="sxs-lookup"><span data-stu-id="98c29-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="98c29-324">**Çözüm Gezgini'nde**projeyi sağ tıklatın ve **NuGet Paketlerini Yönet'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="98c29-325">**NuGet Paket yöneticisi: SignalR.StockTicker**, **Gözat**seçin .</span><span class="sxs-lookup"><span data-stu-id="98c29-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="98c29-326">**Paket kaynağından**, **nuget.org**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="98c29-327">Arama kutusuna *SignalR.Sample* girin ve **Microsoft.AspNet.SignalR.Sample** > **Install'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="98c29-328">**Solution Explorer'da** *SignalR.Sample* klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="98c29-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="98c29-329">SignalR.Sample paketinin yüklenmesi klasörü ve içeriğini oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="98c29-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="98c29-330">*SignalR.Sample* klasöründe *StockTicker.html'e*sağ tıklayın ve ardından **Başlangıç Sayfası Olarak Ayarla'yı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c29-331">SignalR.Sample NuGet paketinin *yüklenmesi, Komut Dosyaları* klasörünüzde bulunan jQuery sürümünü değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="98c29-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="98c29-332">Paketin *SignalR.Sample* klasörüne yükleştirdiği yeni *StockTicker.html* dosyası, paketin yükettiği jQuery sürümüyle senkronize olacaktır, ancak orijinal *StockTicker.html* dosyanızı yeniden çalıştırmak istiyorsanız, önce komut dosyası etiketindeki jQuery başvurularını güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="98c29-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="98c29-333">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="98c29-333">Run the application</span></span>

 <span data-ttu-id="98c29-334">İlk uygulamada gördüğünüz tabloyararlı özelliklere sahipti.</span><span class="sxs-lookup"><span data-stu-id="98c29-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="98c29-335">Tam stok işaretleyici uygulaması yeni özellikler gösterir: hisse senedi verilerini ve yükseldikçe ve düştükçe renk değiştiren hisse senetlerini gösteren yatay kaydırma penceresi.</span><span class="sxs-lookup"><span data-stu-id="98c29-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="98c29-336">Uygulamayı çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="98c29-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="98c29-337">Uygulamayı ilk kez çalıştırdığınızda, "pazar" "kapalı" dır ve kaydırma olmayan statik bir tablo ve işaretleyici penceresi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="98c29-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="98c29-338">**Açık Pazar'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-338">Select **Open Market**.</span></span>

    ![Canlı işaretleyicinin ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="98c29-340">**Canlı Stok Ticker** kutusu yatay olarak kaydırmaya başlar ve sunucu hisse senedi fiyat değişikliklerini düzenli olarak rasgele olarak yayınlamaya başlar.</span><span class="sxs-lookup"><span data-stu-id="98c29-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="98c29-341">Her zaman bir hisse senedi fiyatı değişir, uygulama hem **Live Stock Table** ve Live **Stock Ticker**günceller.</span><span class="sxs-lookup"><span data-stu-id="98c29-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="98c29-342">Bir hisse senedinin fiyat değişikliği pozitif olduğunda, uygulama yeşil arka plana sahip hisse senedini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c29-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="98c29-343">Değişiklik negatif olduğunda, uygulama kırmızı arka planlı hisse senedini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c29-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="98c29-344">**Pazarkapat'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="98c29-345">Tablo güncelleştirmeleri durur.</span><span class="sxs-lookup"><span data-stu-id="98c29-345">The table updates stop.</span></span>

    * <span data-ttu-id="98c29-346">İşaretleyici kaydırmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="98c29-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="98c29-347">**Sıfırla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="98c29-347">Select **Reset**.</span></span>

    * <span data-ttu-id="98c29-348">Tüm stok verileri sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-348">All stock data is reset.</span></span>

    * <span data-ttu-id="98c29-349">Uygulama, fiyat değişiklikleri başlamadan önce ilk durumu geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="98c29-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="98c29-350">URL'yi tarayıcıdan kopyalayın, diğer iki tarayıcıyı açın ve URL'leri adres çubuklarına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="98c29-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="98c29-351">Her tarayıcıda aynı anda dinamik olarak güncellenen aynı verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="98c29-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="98c29-352">Denetimlerden herhangi birini seçtiğinizde, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="98c29-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="98c29-353">Canlı Hayvan Ticker ekran</span><span class="sxs-lookup"><span data-stu-id="98c29-353">Live Stock Ticker display</span></span>

<span data-ttu-id="98c29-354">**Canlı Stok Ticker** ekranı, CSS `<div>` stilleri tarafından tek bir satıra biçimlendirilmiş bir öğedeki sıralanmamış bir listedir.</span><span class="sxs-lookup"><span data-stu-id="98c29-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="98c29-355">Uygulama, işaretleyiciyi tabloyla aynı şekilde başolarak algılar ve güncelleştirir: `<li>` bir şablon dizesinde yer tutucuları değiştirerek ve `<li>` öğeleri öğeye `<ul>` dinamik olarak ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="98c29-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="98c29-356">Uygulama içinde sıralanmamış listenin `animate` kenar boşluğu sol değiştirmek için jQuery işlevini `<div>`kullanarak kaydırma içerir.</span><span class="sxs-lookup"><span data-stu-id="98c29-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="98c29-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="98c29-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="98c29-358">Stok işaretleyici HTML kodu:</span><span class="sxs-lookup"><span data-stu-id="98c29-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="98c29-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="98c29-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="98c29-360">Stok işaretçisi CSS kodu:</span><span class="sxs-lookup"><span data-stu-id="98c29-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="98c29-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="98c29-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="98c29-362">Kaydırma yapan jQuery kodu:</span><span class="sxs-lookup"><span data-stu-id="98c29-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="98c29-363">İstemcinin çağırabileceği sunucudaki ek yöntemler</span><span class="sxs-lookup"><span data-stu-id="98c29-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="98c29-364">Uygulamaya esneklik eklemek için, uygulamanın çağırabileceği ek yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="98c29-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="98c29-365">SignalR.Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="98c29-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="98c29-366">Sınıf, `StockTickerHub` istemcinin çağırabileceği dört ek yöntem tanımlar:</span><span class="sxs-lookup"><span data-stu-id="98c29-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="98c29-367">Uygulama, `OpenMarket`sayfanın `Reset` üst kısmındaki düğmelere yanıt olarak ve çağırır. `CloseMarket`</span><span class="sxs-lookup"><span data-stu-id="98c29-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="98c29-368">Bunlar, bir istemcinin durumunda bir değişikliği tetikleyen deseni hemen tüm istemcilere yayılır şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c29-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="98c29-369">Bu yöntemlerin her `StockTicker` biri, sınıf içinde piyasa durumunun değişmesine neden olan bir yöntem çağırır ve ardından yeni durumu yayınlar.</span><span class="sxs-lookup"><span data-stu-id="98c29-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="98c29-370">SignalR.Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="98c29-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="98c29-371">`StockTicker` Uygulamada, uygulama `MarketState` enum değeri döndüren bir `MarketState` özellik ile piyasanın durumunu korur:</span><span class="sxs-lookup"><span data-stu-id="98c29-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="98c29-372">Sınıf iş parçacığı güvenli olması gerekir, çünkü `StockTicker` pazar durumunu değiştirmek yöntemlerin her biri bir kilit bloğu içinde bunu:</span><span class="sxs-lookup"><span data-stu-id="98c29-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="98c29-373">Bu kodun iş parçacığı için `_marketState` güvenli olduğundan emin `MarketState` olmak `volatile`için, atanan özelliği destekleyen alan:</span><span class="sxs-lookup"><span data-stu-id="98c29-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="98c29-374">İstemcide `BroadcastMarketStateChange` tanımlanan farklı yöntemleri çağırmaları dışında, yöntemler ve `BroadcastMarketReset` yöntemler, önceden gördüğünüz BroadcastStockPrice yöntemine benzer:</span><span class="sxs-lookup"><span data-stu-id="98c29-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="98c29-375">Sunucunun çağırabileceği istemcideki ek işlevler</span><span class="sxs-lookup"><span data-stu-id="98c29-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="98c29-376">İşlev `updateStockPrice` şimdi hem tabloyu hem de işaretçi `jQuery.Color` ekranını işler ve kırmızı ve yeşil renkleri yanıp sönmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="98c29-377">*SignalR.StockTicker.js'deki yeni işlevler,* piyasa durumuna göre düğmeleri etkinleştirebilir ve devre dışı eder.</span><span class="sxs-lookup"><span data-stu-id="98c29-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="98c29-378">Ayrıca Live Stock **Ticker** yatay kaydırma durdurmak veya başlatmak.</span><span class="sxs-lookup"><span data-stu-id="98c29-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="98c29-379">Birçok fonksiyon eklenmektedir `ticker.client`bu yana, uygulama bunları eklemek için [jQuery genişletmek işlevini](http://api.jquery.com/jQuery.extend/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="98c29-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="98c29-380">Bağlantıyı kurduktan sonra ek istemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="98c29-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="98c29-381">İstemci bağlantıyı kurduktan sonra, yapması gereken bazı ek işler vardır:</span><span class="sxs-lookup"><span data-stu-id="98c29-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="98c29-382">Uygun `marketOpened` veya `marketClosed` işlevi aramak için piyasanın açık mı kapalı mı yoksa kapalı mı olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="98c29-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="98c29-383">Sunucu yöntemi çağrılarını düğmelere takın.</span><span class="sxs-lookup"><span data-stu-id="98c29-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="98c29-384">Sunucu yöntemleri, uygulama bağlantıyı kurana kadar düğmelere bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="98c29-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="98c29-385">Bu, kodun kullanılabilir olmadan önce sunucu yöntemlerini arayamaabilmesi içindir.</span><span class="sxs-lookup"><span data-stu-id="98c29-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98c29-386">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="98c29-386">Additional resources</span></span>

<span data-ttu-id="98c29-387">Bu eğitimde, sunucudan tüm bağlı istemcilere ileti yayınlayan bir SignalR uygulamasını programlamayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="98c29-388">Artık iletileri periyodik olarak ve herhangi bir istemciden gelen bildirimlere yanıt olarak yayınlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="98c29-389">Çok oyunculu çevrimiçi oyun senaryolarında sunucu durumunu korumak için çok iş parçacığı singleton örneği kavramını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98c29-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="98c29-390">Örneğin, [SignalR tabanlı ShootR oyununa](https://github.com/NTaylorMullen/ShootR)bakın.</span><span class="sxs-lookup"><span data-stu-id="98c29-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="98c29-391">Eşler arası iletişim senaryolarını gösteren öğreticiler için [SignalR ile Başlarken](introduction-to-signalr.md) ve [SignalR ile Gerçek Zamanlı Güncelleme](tutorial-high-frequency-realtime-with-signalr.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="98c29-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="98c29-392">SignalR hakkında daha fazla şey için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="98c29-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="98c29-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="98c29-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="98c29-394">SignalR Projesi</span><span class="sxs-lookup"><span data-stu-id="98c29-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="98c29-395">Sinyalci GitHub ve Örnekler</span><span class="sxs-lookup"><span data-stu-id="98c29-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="98c29-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="98c29-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="98c29-397">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98c29-397">Next steps</span></span>

<span data-ttu-id="98c29-398">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="98c29-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98c29-399">Proje oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="98c29-399">Created the project</span></span>
> * <span data-ttu-id="98c29-400">Sunucu kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-400">Set up the server code</span></span>
> * <span data-ttu-id="98c29-401">Sunucu kodu incelendi</span><span class="sxs-lookup"><span data-stu-id="98c29-401">Examined the server code</span></span>
> * <span data-ttu-id="98c29-402">İstemci kodunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="98c29-402">Set up the client code</span></span>
> * <span data-ttu-id="98c29-403">İstemci kodu incelendi</span><span class="sxs-lookup"><span data-stu-id="98c29-403">Examined the client code</span></span>
> * <span data-ttu-id="98c29-404">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="98c29-404">Tested the application</span></span>
> * <span data-ttu-id="98c29-405">Etkin günlük</span><span class="sxs-lookup"><span data-stu-id="98c29-405">Enabled logging</span></span>

<span data-ttu-id="98c29-406">SignalR 2'yi ASP.NET kullanan gerçek zamanlı bir web uygulamasının nasıl oluşturulabildiğini öğrenmek için bir sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="98c29-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="98c29-407">SignalR ile gerçek zamanlı web uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="98c29-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
