---
title: ASP.NET Core MVC ile çalışmaya başlama
author: rick-anderson
description: ASP.NET Core MVC ile çalışmaya başlama hakkında bilgi edinin.
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: c09c06f55c4179e9e2174f0063ab7387b7e4c31b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076437"
---
# <a name="get-started-with-aspnet-core-mvc"></a>ASP.NET Core MVC ile çalışmaya başlama

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu öğreticide bir ASP.NET Core MVC web uygulaması oluşturmaya ilişkin temel bilgileri size öğretir.

Uygulama bir veritabanı başlık yönetir. Aşağıdakilerin nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bir web uygulaması oluşturun.
> * Ekleme ve bir modeli iskelesini.
> * Bir veritabanı ile çalışır.
> * Arama ve doğrulama ekleyin.

Sonunda, yönetmek ve film verileri görüntüleyen bir uygulama vardır.

[!INCLUDE[](~/includes/mvc-intro/download.md)]

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a>Web uygulaması oluşturma

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Visual Studio'dan seçin **Dosya > Yeni > Proje**.

![Dosya > Yeni > Proje](start-mvc/_static/alt_new_project.png)

Tamamlamak **yeni proje** iletişim:

* Sol bölmede seçin **.NET Core**
* Orta bölmede seçin **ASP.NET Core Web uygulaması (.NET Core)**
* (Kod kopyaladığınızda, ad alanı eşleşecek şekilde "MvcMovie" proje adı önemlidir.) "MvcMovie" proje adı
* Seçin **Tamam**

![Yeni Proje iletişim kutusunda, sol bölmede, ASP.NET Core web'de .net core ](start-mvc/_static/new_project2-21.png)

Tamamlamak **yeni ASP.NET Core Web uygulaması (.NET Core) - MvcMovie** iletişim:

* Sürüm Seçici açılan kutusunda seçin **ASP.NET Core 2.2**
* Seçin **Web uygulaması (Model-View-Controller)**
* Seçin **Tamam**.

![Yeni Proje iletişim kutusunda, sol bölmede, ASP.NET Core web'de .net core ](start-mvc/_static/new_project22-21.png)

Visual Studio, yeni oluşturduğunuz MVC projesi için varsayılan bir şablon kullanılır. Çalışan bir uygulamayı şu anda bir proje adı girerek ve bazı Seçenekler'i seçerek sizde. Bu temel başlangıç projesini ve başlatmak için iyi bir yerdir.

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

Bu öğretici, VS Code ile familarity varsayar. Bkz: [VS Code ile çalışmaya başlama](https://code.visualstudio.com/docs) ve [Visual Studio Code Yardım](#visual-studio-code-help) daha fazla bilgi için.

* Açık [tümleşik Terminalini](https://code.visualstudio.com/docs/editor/integrated-terminal).
* Dizinleri (`cd`) proje içeren bir klasör.
* Şu komutu çalıştırın:

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * Bir iletişim kutusu görünür **gerekli varlıkları oluşturun ve hata ayıklama 'MvcMovie' eksik. Bunları eklensin mi?**  Seçin **Evet**

  * `dotnet new mvc -o MvcMovie`: yeni bir ASP.NET Core MVC projesindeki oluşturur *MvcMovie* klasör.
  * `code -r MvcMovie`: Yükleri *MvcMovie.csproj* proje dosyası Visual Studio code'da.

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Mac için Visual Studio](#tab/visual-studio-mac)

* Seçin **dosya** > **yeni çözüm**.

  ![Yeni çözüm macOS](~/tutorials/first-web-api-mac/_static/sln.png)

* Seçin **.NET Core uygulaması** > **ASP.NET Core** > **ASP.NET Core Web uygulaması (MVC)** > **sonraki**.

  ![macOS yeni proje iletişim kutusu](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* İçinde **, yeni ASP.NET Core Web API'sini yapılandırma** iletişim kutusunda varsayılan değerleri kabul **hedef Framework'ü** , **.NET Core 2.2*.

* Projeyi adlandırın **MvcMovie**ve ardından **Oluştur**.

---  
<!-- End of VS tabs -->

### <a name="run-the-app"></a>Uygulamayı çalıştırma

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Seçin **Ctrl-F5** uygulamayı olmayan hata ayıklama modunda çalıştırmak için.

[!INCLUDE[](~/includes/trustCertVS.md)]

* Visual Studio başlatır [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) ve uygulamayı çalıştırır. Adres çubuğuna gösteren uyarı `localhost:port#` gibi bir şey `example.com`. Çünkü `localhost` standart, yerel bilgisayar adıdır. Visual Studio, bir web projesi oluşturduğunda, web sunucusu için rastgele bir bağlantı noktası kullanılır.
* Ctrl + F5 (hata ayıklama olmayan mod) ile uygulamayı çalıştırdığınızda, kod değişiklikleri yapabilir, dosyayı kaydetmek, tarayıcıyı yenileyin ve kod değişikliklerini görebilirsiniz olanak tanır. Geliştiricilerin çoğu, hızlı bir şekilde uygulamayı başlatın ve değişiklikleri görmek için hata ayıklama olmayan modu kullanmayı tercih eder.
* Uygulamada hata ayıklama veya hata ayıklama olmayan moddan başlatabilirsiniz **hata ayıklama** menü öğesi:

  ![Menü hata ayıklama](start-mvc/_static/debug_menu.png)

* Seçerek uygulama hatalarını ayıklayabilir **IIS Express** düğmesi

  ![IIS Express](start-mvc/_static/iis_express.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code) 

Hata Ayıklayıcı olmadan çalıştırmak için CTRL + F5 tuşlarına basın.

[!INCLUDE[](~/includes/trustCertVSC.md)]

  Visual Studio Code başlatıldığında başlar [Kestrel](xref:fundamentals/servers/kestrel), bir tarayıcı başlatır ve gider `https://localhost:5001`. Adres çubuğu gösterir `localhost:port:5001` gibi bir şey `example.com`. Çünkü `localhost` standart yerel bilgisayar adıdır. Localhost yalnızca yerel bilgisayara gelen web isteklerini işlevi görür.

  Ctrl + F5 (hata ayıklama olmayan mod) ile uygulamayı çalıştırdığınızda, kod değişiklikleri yapabilir, dosyayı kaydetmek, tarayıcıyı yenileyin ve kod değişikliklerini görebilirsiniz olanak tanır. Geliştiricilerin çoğu, sayfayı yenileyin ve değişiklikleri görüntülemek için hata ayıklama olmayan modu kullanmayı tercih eder.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Mac için Visual Studio](#tab/visual-studio-mac)

Seçin **çalıştırma** > **hata ayıklama olmadan Başlat** uygulamayı başlatın. Başlatıldığında Mac için Visual Studio [Kestrel](xref:fundamentals/servers/index#kestrel) sunucusunda, bir tarayıcı başlatır ve gider `http://localhost:port`burada *bağlantı noktası* bir rastgele seçilen bağlantı noktası numarasıdır.

[!INCLUDE[](~/includes/trustCertMac.md)]

* Adres çubuğu gösterir `localhost:port#` gibi bir şey `example.com`. Çünkü `localhost` standart, yerel bilgisayar adıdır. Visual Studio, bir web projesi oluşturduğunda, web sunucusu için rastgele bir bağlantı noktası kullanılır. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası görürsünüz.
* Uygulamada hata ayıklama veya hata ayıklama olmayan moddan başlatabilirsiniz **çalıştırma** menüsü.

------

* Seçin **kabul** izleme için onay verme. Bu uygulama, kişisel bilgi izlemez. Oluşturulan şablon kodunun karşılamanıza yardımcı olmak üzere varlıkları içeren [genel veri koruma yönetmeliği (GDPR)](xref:security/gdpr).

  ![Giriş ya da dizin sayfası](start-mvc/_static/privacy.png)

  Aşağıdaki görüntüde, izleme kabul ettikten sonra uygulama gösterilir:

  ![Giriş ya da dizin sayfası](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

Bu öğreticinin sonraki bölümünde, MVC konusunda bilgi ve biraz kod yazmaya başlayın.

> [!div class="step-by-step"]
> [Next](adding-controller.md)  
