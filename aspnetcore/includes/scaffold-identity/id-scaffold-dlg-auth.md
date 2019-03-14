---
ms.openlocfilehash: cb9041a466309a400b19cdecd76f653499c6ac4b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074847"
---
Kimlik iskele kurucu çalıştırın:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Gelen **Çözüm Gezgini**, projeye sağ tıklayın > **Ekle** > **yeni iskele kurulmuş öğe**.
* Sol bölmeden **İskele Ekle** iletişim kutusunda **kimlik** > **ekleme**.
* İçinde **ADD kimliğini** iletişim kutusunda, istediğiniz seçenekleri seçin.
  * Varolan bir düzen sayfası seçin veya hatalı biçimlendirme Düzen dosyanızın üzerine yazılacak. Var olan bir zaman  *\_Layout.cshtml* dosya seçildiğinde, **değil** üzerine.

 Örneğin `~/Pages/Shared/_Layout.cshtml` Razor sayfaları için `~/Views/Shared/_Layout.cshtml` MVC projeleri
* Mevcut veri Bağlamınızı kullanmak için geçersiz kılmak için en az bir dosya seçin. Veri Bağlamınızı eklemek için en az bir dosya seçmelisiniz.
  * Veri bağlamı sınıfı seçin.
  * Seçin **ekleme**.
* Yeni bir kullanıcı bağlam oluşturur ve muhtemelen kimlik için bir özel kullanıcı sınıfı oluşturmak için:
  * Seçin **+** yeni bir düğme **veri bağlamı sınıfının**.
  * Seçin **ekleme**.

Not: Yeni bir kullanıcı bağlamı oluşturuyorsanız, geçersiz kılmak için bir dosya seçmek gerekmez.

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

Proje klasöründe kimlik iskele kurucu istediğiniz seçeneği ile çalıştırın. Örneğin, kimliği ' % s'varsayılan kullanıcı Arabirimi ile ve en az sayıda dosya kurmak için aşağıdaki komutu çalıştırın. DB Bağlamınızı doğru tam adını kullanın:

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

PowerShell komut ayırıcı olarak virgül kullanır. PowerShell kullanarak, dosya listesinde noktalı kaçış veya dosya listesi çift tırnak işaretleri içine alın. Örneğin:

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"
```

Kimlik iskele kurucu belirtmeden çalıştırırsanız `--files` bayrağı veya `--useDefaultUI` bayrak, tüm kullanılabilir kimlik UI sayfaları projenizde oluşturulur.

-------------
