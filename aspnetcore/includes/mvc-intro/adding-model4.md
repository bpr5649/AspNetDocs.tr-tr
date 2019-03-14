---
ms.openlocfilehash: cf30f952c08d9801eead9574d4fc5073e80ceb71
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066981"
---
Gösterildiği eklenmesini film veritabanı bağlamı vurgulanan kod [bağımlılık ekleme](xref:fundamentals/dependency-injection) kapsayıcı (içinde *Startup.cs* dosyası). `services.AddDbContext<MvcMovieContext>(options =>` Veritabanı ve bağlantı dizesini belirtir. `=>` olan bir [lambda işleci](/dotnet/articles/csharp/language-reference/operators/lambda-operator).

Açık *Controllers/MoviesController.cs* dosya ve oluşturucu inceleyin:

<!-- l.. Make copy of Movies controller because we comment out the initial index method and update it later  -->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_1)] 

Oluşturucu kullanan [bağımlılık ekleme](xref:fundamentals/dependency-injection) veritabanı bağlamı eklemesine (`MvcMovieContext `) içine denetleyici. Her bir veritabanı bağlamı kullanılan [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) denetleyici yöntemleri.

<a name="strongly-typed-models-keyword-label"></a>
<a name="strongly-typed-models-and-the--keyword"></a>

## <a name="strongly-typed-models-and-the-model-keyword"></a>Kesin olarak modelleri ve @model anahtar sözcüğü

Bu öğreticide daha önce nasıl bir denetleyici veri veya nesneleri kullanarak bir görünüm geçirebilirsiniz gördüğünüz `ViewData` sözlüğü. `ViewData` Sözlüktür bilgi bir görünüme iletmek için kullanışlı bir geç bağlanan yol sağlayan bir dinamik Nesne.

MVC, model nesneleri bir görünüme kesin geçirme özelliği yazılan de sağlar. Bu yaklaşım etkinleştirir daha iyi derleme, kodu denetleme zamanı kesin. (Bu, türü kesin belirlenmiş bir model geçirdiğini) Bu yaklaşımı kullanılan yapı iskelesi mekanizması `MoviesController` sınıfı ve metotları ve görünümleri oluştururken görünümleri.

Oluşturulan inceleyin `Details` yönteminde *Controllers/MoviesController.cs* dosyası:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_details)]

`id` Parametre rota verileri genel olarak geçirilir. Örneğin `http://localhost:5000/movies/details/1` ayarlar:

* Denetleyiciye `movies` denetleyici (ilk URL kesimini).
* Eyleme `details` (ikinci URL kesimini).
* 1 (son URL kesimini) kimliği.

Ayrıca, geçirebilirsiniz `id` ile bir sorgu dizesi şu şekilde:

`http://localhost:1234/movies/details?id=1`

`id` Parametresi olarak tanımlanmış olan bir [boş değer atanabilir tür](/dotnet/csharp/programming-guide/nullable-types/index) (`int?`) durumda bir kimlik değeri sağlanmadı.

A [lambda ifadesi](/dotnet/articles/csharp/programming-guide/statements-expressions-operators/lambda-expressions) için geçirilen `FirstOrDefaultAsync` rota verileri veya sorgu dizesi değeriyle eşleşen film varlıkları seçin.

```csharp
var movie = await _context.Movie
    .FirstOrDefaultAsync(m => m.Id == id);
```

Bir filmi bulunursa örneği `Movie` modeline geçirilir `Details` görüntüle:

```csharp
return View(movie);
   ```

İçeriğini incelemek *Views/Movies/Details.cshtml* dosyası:

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/DetailsOriginal.cshtml)]

Ekleyerek bir `@model` deyimi görünüm dosyası üst kısmındaki görünümü bekliyor nesne türünü belirtebilirsiniz. Aşağıdaki film denetleyicisi oluşturduğunuzda `@model` deyimi otomatik olarak dahil edilen en üstündeki *Details.cshtml* dosyası:

```HTML
@model MvcMovie.Models.Movie
   ```

Bu `@model` yönergesi kullanarak denetleyici görünüm tarafından geçirilen film erişmenize olanak sağlayan bir `Model` türü kesin belirlenmiş bir nesne. Örneğin, *Details.cshtml* görünümü, kod, her filmin alanına geçirir `DisplayNameFor` ve `DisplayFor` HTML Yardımcıları ile kesin olarak belirlenmiş `Model` nesne. `Create` Ve `Edit` metotları ve görünümleri de başarılı bir `Movie` model nesnesi.

İnceleme *Index.cshtml* görünümü ve `Index` denetleyici filmler yöntemi. Kodun nasıl oluşturduğunu fark bir `List` nesne çağırdığında `View` yöntemi. Bu kod geçirir `Movies` gelen listesinde `Index` eylem yöntemine görünümü:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_index)]

Denetleyici filmler oluşturduğunuzda otomatik olarak iskele kurma özelliği aşağıdaki dahil `@model` en üstündeki deyimi *Index.cshtml* dosyası:

<!-- Copy Index.cshtml to IndexOriginal.cshtml -->

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?range=1)]

`@model` Yönergesi kullanarak görünüm tarafından geçirilen denetleyici filmler listesini erişmenize olanak sağlayan bir `Model` türü kesin belirlenmiş bir nesne. Örneğin, *Index.cshtml* görüntülemek, filmlerle kodunu döner bir `foreach` deyimi kesin olarak belirlenmiş üzerinden `Model` nesnesi:

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?highlight=1,31,34,37,40,43,46-48)]

Çünkü `Model` nesne türü kesin belirlenmiş (olarak bir `IEnumerable<Movie>` nesne), Döngüdeki her bir öğe olarak yazılan `Movie`. Diğer avantajlar arasında bu derleme zamanı elde anlamına gelir kodunu denetleniyor:
