---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071868"
---
## <a name="add-initial-migration-and-update-the-database"></a><span data-ttu-id="bde28-101">İlk geçiş ekleyin ve veritabanını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="bde28-101">Add initial migration and update the database</span></span>

* <span data-ttu-id="bde28-102">Bir komut istemi açın ve proje dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="bde28-102">Open a command prompt and navigate to the project directory.</span></span> <span data-ttu-id="bde28-103">(Dizinini içeren *Startup.cs* dosyası).</span><span class="sxs-lookup"><span data-stu-id="bde28-103">(The directory containing the *Startup.cs* file).</span></span>

* <span data-ttu-id="bde28-104">Komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bde28-104">Run the following commands in the command prompt:</span></span>

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  <span data-ttu-id="bde28-105">[.NET core](/dotnet/core/tools/index) bir çoklu platform .NET uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="bde28-105">[.NET Core](/dotnet/core/tools/index) is a cross-platform implementation of .NET.</span></span> <span data-ttu-id="bde28-106">Bu komutlar neler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bde28-106">Here is what these commands do:</span></span>

  * <span data-ttu-id="bde28-107">[DotNet restore](/dotnet/core/tools/dotnet-restore): Belirtilen NuGet paketlerini indirir *.csproj* dosya.</span><span class="sxs-lookup"><span data-stu-id="bde28-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): Downloads the NuGet packages specified in the *.csproj* file.</span></span>
  * <span data-ttu-id="bde28-108">`dotnet ef migrations add Initial` Entity Framework .NET Core CLI geçişleri komutu çalıştırır ve ilk geçiş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bde28-108">`dotnet ef migrations add Initial` Runs the Entity Framework .NET Core CLI migrations command and creates the initial migration.</span></span> <span data-ttu-id="bde28-109">"Ekle" sonra parametre geçişi atadığınız bir addır.</span><span class="sxs-lookup"><span data-stu-id="bde28-109">The parameter after "add" is a name that you assign to the migration.</span></span> <span data-ttu-id="bde28-110">Burada, ilk veritabanı geçiş olduğundan "Başlangıç" geçiş adlandırıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="bde28-110">Here you're naming the migration "Initial" because it's the initial database migration.</span></span> <span data-ttu-id="bde28-111">Bu işlem oluşturur *geçişlerini / /\<tarih-saat > _Initial.cs* eklemek için geçiş komutları içeren dosya *film* veritabanına tablo.</span><span class="sxs-lookup"><span data-stu-id="bde28-111">This operation creates the *Data/Migrations/\<date-time>_Initial.cs* file containing the migration commands to add the *Movie* table to the database.</span></span>
  * <span data-ttu-id="bde28-112">`dotnet ef database update`  Veritabanı, yeni oluşturduğumuz geçiş ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bde28-112">`dotnet ef database update`  Updates the database with the migration we just created.</span></span>

<span data-ttu-id="bde28-113">Sonraki öğreticide veritabanı ve bağlantı dizesini hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bde28-113">You'll learn about the database and connection string in the next tutorial.</span></span> <span data-ttu-id="bde28-114">Veri modeli değişikliklerini hakkında bilgi edineceksiniz [bir alan eklemek](xref:tutorials/first-mvc-app/new-field) öğretici.</span><span class="sxs-lookup"><span data-stu-id="bde28-114">You'll learn about data model changes in the [Add a field](xref:tutorials/first-mvc-app/new-field) tutorial.</span></span>
