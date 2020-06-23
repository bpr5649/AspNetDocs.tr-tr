---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure Web rolünde SignalR performans sayaçlarını kullanma | Microsoft Docs
author: guardrex
description: Azure Web rolünde SignalR performans sayaçlarını yüklemek ve kullanmak.
keywords: ASP. NET, SignalR, performans sayacı, Azure Web rolü
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240647"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Azure Web rolünde SignalR performans sayaçlarını kullanma

[Luke Latham](https://github.com/guardrex) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR performans sayaçları, uygulamanızın performansını bir Azure Web rolünde izlemek için kullanılır. Sayaçlar Microsoft Azure Tanılama tarafından yakalanır. Azure 'da SignalR performans sayaçlarını, tek başına veya şirket içi uygulamalar için kullanılan aynı aracı *signalr.exe*ile birlikte yüklersiniz. Azure rolleri geçici olduğundan, bir uygulamayı başlangıçtan sonra SignalR performans sayaçlarını yükleyecek ve kaydedecek şekilde yapılandırırsınız.

## <a name="prerequisites"></a>Ön koşullar

* Visual Studio 2015 veya [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [Visual Studio için MICROSOFT Azure SDK](https://azure.microsoft.com/downloads/) 'sı **: SDK 'yı yükledikten sonra makinenizi yeniden başlatın.**
* Microsoft Azure abonelik: ücretsiz bir Azure deneme hesabına kaydolmak Için bkz. [Azure Ücretsiz deneme](https://azure.microsoft.com/free/dotnet/).

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>SignalR performans sayaçlarını kullanıma sunan bir Azure Web rolü uygulaması oluşturma

1. Visual Studio'yu açın.

2. Visual Studio 'da **Dosya**  >  **Yeni**  >  **Proje**' yi seçin.

3. **Yeni proje** iletişim kutusunda, sol taraftaki **Visual C#**  >  **bulut** kategorisini seçin ve ardından **Azure bulut hizmeti** şablonunu seçin. Uygulamayı **Signalrperfcounters** olarak adlandırın ve **Tamam**' ı seçin.

   ![Yeni bulut uygulaması](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > **Bulut** şablonu kategorisini veya **Azure bulut hizmeti** şablonunu görmüyorsanız, Visual Studio 2017 için **Azure geliştirme** iş yükünü yüklemeniz gerekir. Visual Studio Yükleyicisi açmak için **Yeni proje** iletişim kutusunun sol alt tarafındaki **Visual Studio yükleyicisi aç** bağlantısını seçin. **Azure geliştirme** iş yükünü seçin ve sonra iş yükünü yüklemeye başlamak için **Değiştir** ' i seçin.
   >
   > ![Visual Studio Yükleyicisi Azure geliştirme iş yükü](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. **Yeni Microsoft Azure bulut hizmeti** iletişim kutusunda **ASP.NET Web rolü** ' nü seçin ve rolü projeye eklemek için > düğmesini seçin. **Tamam**’ı seçin.

   ![ASP.NET Web rolü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. **Yeni ASP.NET Web uygulaması-WebRole1** Iletişim kutusunda **MVC** şablonunu seçin ve ardından **Tamam**' ı seçin.

   ![MVC ve Web API 'SI ekleme](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. **Çözüm Gezgini**' de, **WebRole1**altında *Diagnostics. wadcfgx* dosyasını açın.

   ![Çözüm Gezgini Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. Dosyanın içeriğini aşağıdaki yapılandırmayla değiştirin ve dosyayı kaydedin:

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. **Araçlar**NuGet Paket Yöneticisi ' nden **Paket Yöneticisi konsolunu** açın  >  **NuGet Package Manager**. SignalR 'nin en son sürümünü ve SignalR yardımcı programları paketini yüklemek için aşağıdaki komutları girin:

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. Uygulamayı başlatıldığında veya geri dönüştürüldüğünde, SignalR performans sayaçlarını rol örneğine yükleyecek şekilde yapılandırın. **Çözüm Gezgini**, **WebRole1** projesine sağ tıklayın ve **Add**  >  **Yeni klasör**Ekle ' yi seçin. Yeni klasör *başlangıcını*adlandırın.

   ![Başlangıç klasörü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. *signalr.exe* dosyasını ( **Microsoft. Aspnet. SignalR. utils** paketiyle eklenen) \<project folder> /SignalRPerfCounters/Packages/Microsoft.Aspnet.SignalR.utils. \<version> adresinden kopyalayın /Tools önceki adımda oluşturduğunuz *Başlangıç* klasörüne gidin.

11. **Çözüm Gezgini**, *Başlangıç* klasörüne sağ tıklayın ve **Add**  >  **Varolan öğe**Ekle ' yi seçin. Görüntülenen iletişim kutusunda *signalr.exe* ' ı seçin ve **Ekle**' yi seçin.

    ![Projeye signalr.exe Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. Oluşturduğunuz *Başlangıç* klasörüne sağ tıklayın. **Add**  >  **Yeni öğe**Ekle ' yi seçin. **Genel** düğümünü seçin, **metin dosyası**' nı seçin ve yeni öğe *signalrperfcounterınstall. cmd*olarak adlandırın. Bu komut dosyası, SignalR performans sayaçlarını Web rolüne yükler.

    ![SignalR performans sayacı yüklemesi toplu iş dosyası oluşturma](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Visual Studio, *Signalrperfcounterınstall. cmd* dosyasını oluşturduğunda ana pencerede otomatik olarak açılır. Dosyanın içeriğini aşağıdaki komut dosyasıyla değiştirin, sonra dosyayı kaydedip kapatın. Bu betik, SignalR performans sayaçlarını rol örneğine ekleyen *signalr.exe*yürütülür.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. **Çözüm Gezgini** *signalr.exe* dosyasını seçin. Dosyanın **özelliklerinde**, **her zaman kopyalamak**için **Çıkış Dizinine Kopyala** ' yı ayarlayın.

    ![Her zaman kopyalamak için çıkış dizinine Kopyala ayarla](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. *Signalrperfcounterınstall. cmd* dosyası için önceki adımı tekrarlayın.

16. *Signalrperfcounterınstall. cmd* dosyasına sağ tıklayın ve **birlikte Aç**' ı seçin. Görüntülenen iletişim kutusunda **Ikili düzenleyici** ' yi seçin ve **Tamam**' ı seçin.

    ![Ikili düzenleyiciyle aç](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. İkili düzenleyicide, dosyadaki önde gelen baytları seçin ve silin. Dosyayı kaydedin ve kapatın.

    ![Baştaki baytları Sil](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. *ServiceDefinition. csdef* ' i açın ve hizmet başlatıldığında *Signalrperfcounterınstall. cmd* dosyasını yürüten bir başlangıç görevi ekleyin:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. `Views/Shared/_Layout.cshtml`Dosya sonundan jQuery paket betiğini açın ve kaldırın.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. Sunucuda yöntemi sürekli çağıran bir JavaScript istemcisi ekleyin `increment` . `Views/Home/Index.cshtml`İçeriğini açın ve şu kodla değiştirin:

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. **WebRole1** projesinde *hub 'lar*adlı yeni bir klasör oluşturun. **Çözüm Gezgini** *hub* klasörüne sağ tıklayın ve **Add**  >  **Yeni öğe**Ekle ' yi seçin. **Yeni öğe Ekle** iletişim kutusunda, **Web**  >  **SignalR** kategorisini seçin ve ardından **SignalR hub sınıfı (v2)** öğe şablonunu seçin. Yeni hub *MyHub.cs* ' ı adlandırın ve **Ekle**' yi seçin.

    ![SignalR hub sınıfı yeni öğe Ekle iletişim kutusunda hub klasörüne ekleniyor](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs* , ana pencerede otomatik olarak açılır. İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* , SignalR kod temeli ile birlikte sunulan bir bağlantı yoğunluğu test aracıdır. Crank kalıcı bir bağlantı gerektirdiğinden, test ederken kullanmak için sitenize bir tane ekleyin. **WebRole1** projesine *Persistentconnections*adlı yeni bir klasör ekleyin. Bu klasöre sağ tıklayın ve sınıf **Ekle**' yi seçin  >  **Class**. Yeni sınıf dosyasını *MyPersistentConnections.cs* olarak adlandırın ve **Ekle**' yi seçin.

24. Visual Studio, *MyPersistentConnections.cs* dosyasını ana pencerede açar. İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. Sınıfını kullanarak `Startup` , OWıN başlatıldığında SignalR nesneleri başlatılır. *Startup.cs* açın veya oluşturun ve içeriğini şu kodla değiştirin:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    Yukarıdaki kodda `OwinStartup` özniteliği, OWıN 'u başlatmak için bu sınıfı işaretler. `Configuration`Yöntemi SignalR 'yi başlatır.

26. **F5**tuşuna basarak Microsoft Azure öykünücüsü uygulamanızı test edin.

    > [!NOTE]
    > **Mapsignalr**'de bir **fileloadexception** ile karşılaşırsanız *web.config* bağlama yeniden yönlendirmelerini aşağıdaki şekilde değiştirin:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. Bir dakika bekleyin. Visual Studio 'da Cloud Explorer araç penceresini açın (**View**  >  **bulut Gezginini**görüntüleyin) ve yolu genişletin `(Local)/Storage Accounts/(Development)/Tables` . **WADPerformanceCountersTable**çift tıklayın. Tablo verilerinde SignalR sayaçlarını görmeniz gerekir. Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir. Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.

    ![Visual Studio Cloud Explorer 'da WAD performans sayaçları tablosunu seçme](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD performans sayaçları tablosunda toplanan sayaçları gösterme](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. Uygulamanızı bulutta test etmek için, **ServiceConfiguration. Cloud. cscfg** dosyasını güncelleştirin ve öğesini `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` geçerli bir Azure depolama hesabı bağlantı dizesi olarak ayarlayın.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Uygulamayı Azure aboneliğinize dağıtın. Bir uygulamayı Azure 'a dağıtma hakkında ayrıntılı bilgi için bkz. [bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).

30. Birkaç dakika bekleyin. **Cloud Explorer**'da, yukarıda yapılandırdığınız depolama hesabını bulun ve `WADPerformanceCountersTable` içindeki tabloyu bulun. Tablo verilerinde SignalR sayaçlarını görmeniz gerekir. Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir. Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.

Bu öğreticide kullanılan özgün içerik için özel [Marrichard](https://social.msdn.microsoft.com/profile/Martin+Richard) 'e teşekkür ederiz.
