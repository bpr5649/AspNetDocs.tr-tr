---
ms.openlocfilehash: e5c80c80380dadfce9cff5ec268535076258d980
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070974"
---
Kimlik iskele kurucu çalıştırın:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Gelen **Çözüm Gezgini**, projeye sağ tıklayın > **Ekle** > **yeni iskele kurulmuş öğe**.
* Sol bölmeden **İskele Ekle** iletişim kutusunda **kimlik** > **ekleme**.
* İçinde **ADD kimliğini** iletişim kutusunda, istediğiniz seçenekleri seçin.
  * Varolan bir düzen sayfası seçin veya hatalı biçimlendirme Düzen dosyanızın üzerine yazılacak. Örneğin `~/Pages/Shared/_Layout.cshtml` Razor sayfaları için `~/Views/Shared/_Layout.cshtml` MVC projeleri
  * Seçin **+** yeni bir düğme **veri bağlamı sınıfının**.
* Seçin **ekleme**.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

ASP.NET Core iskele kurucu daha önce yüklemediyseniz şimdi yükleyin:

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

Paket başvurusu ekleme [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) projesine (\*.csproj) dosyası. Proje dizininde aşağıdaki komutu çalıştırın:

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Kimlik destek seçeneklerini listelemek için aşağıdaki komutu çalıştırın:

```cli
dotnet aspnet-codegenerator identity -h
```

Proje klasöründe kimlik iskele kurucu istediğiniz seçeneği ile çalıştırın. Örneğin, varsayılan UI kimliği ve en az sayıda dosya Kurulumu için aşağıdaki komutu çalıştırın:

```cli
dotnet aspnet-codegenerator identity --useDefaultUI
```

-------------
