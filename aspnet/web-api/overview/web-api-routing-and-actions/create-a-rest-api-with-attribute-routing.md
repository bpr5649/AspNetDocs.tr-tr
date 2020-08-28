---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045188"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma

, [Mike te son](https://github.com/MikeWasson)

Web API 2 ' de *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türü desteklenir. Öznitelik yönlendirmeye genel bir bakış için bkz. [Web API 2 ' de öznitelik yönlendirme](attribute-routing-in-web-api-2.md). Bu öğreticide, bir kitap koleksiyonu için REST API oluşturmak üzere öznitelik yönlendirmeyi kullanacaksınız. API aşağıdaki eylemleri destekler:

| Eylem | Örnek URI |
| --- | --- |
| Tüm kitapların bir listesini alın. | /api/Books |
| KIMLIĞE göre bir kitap alın. | /api/Books/1 |
| Bir kitabın ayrıntılarını alın. | /api/Books/1/details |
| Türe göre kitap listesini alın. | /api/Books/fantei |
| Yayın tarihine göre Kitaplar listesini alın. | /api/Books/Date/2013-02-16/api/Books/Date/2013/02/16 (alternatif form) |
| Belirli bir yazarın kitap listesini alın. | /api/Authors/1/Books |

Tüm yöntemler salt okunurdur (HTTP GET istekleri).

Veri katmanı için Entity Framework kullanacağız. Kitap kayıtları aşağıdaki alanlara sahip olacaktır:

- ID
- Başlık
- Tarzı
- Yayın tarihi
- Fiyat
- Açıklama
- AuthorId (bir yazarlar tablosuna yabancı anahtar)

Ancak, çoğu istek için, API bu verilerin bir alt kümesini döndürür (başlık, yazar ve tarz). Tüm kayıtları almak için istemci istekleri `/api/books/{id}/details` .

## <a name="prerequisites"></a>Önkoşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise Edition.

## <a name="create-the-visual-studio-project"></a>Visual Studio projesi oluşturma

Visual Studio 'Yu çalıştırarak başlayın. **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Yüklü**  >  **Visual C#** kategorisini genişletin. **Visual C#** altında **Web**' i seçin. Proje şablonları listesinde **ASP.NET Web uygulaması (.NET Framework)** öğesini seçin. Projeyi &quot; booksapı olarak adlandırın &quot; .

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

**Yeni ASP.NET Web uygulaması** Iletişim kutusunda **boş** şablonu seçin. "Klasör ve çekirdek başvuruları Ekle" altında **Web API** onay kutusunu seçin. **Tamam** düğmesine tıklayın.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

Bu, Web API işlevselliği için yapılandırılmış bir iskelet projesi oluşturur.

### <a name="domain-models"></a>Etki alanı modelleri

Daha sonra, etki alanı modelleri için sınıflar ekleyin. Çözüm Gezgini modeller klasörüne sağ tıklayın. **Ekle**' yi ve ardından **sınıf**' ı seçin. Sınıfı adlandırın `Author` .

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Author.cs içindeki kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

Şimdi adlı başka bir sınıf ekleyin `Book` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Web API denetleyicisi ekleme

Bu adımda, veri katmanı olarak Entity Framework kullanan bir Web API denetleyicisi ekleyeceğiz.

Projeyi oluşturmak için CTRL+SHIFT+B tuşlarına basın. Entity Framework, modellerin özelliklerini saptamak için yansıma kullanır, bu nedenle veritabanı şemasını oluşturmak için derlenmiş bir bütünleştirilmiş kod gerektirir.

Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle**' yi ve ardından **Denetleyici**' yi seçin.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

**Yapı Iskelesi Ekle** iletişim kutusunda, **ENTITY Framework kullanarak Web API 2 denetleyiciyi eylemlerle '** yi seçin.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

**Denetleyici Ekle** iletişim kutusunda, **Denetleyici adı**için, &quot; bookscontroller yazın &quot; . &quot;Zaman uyumsuz denetleyici eylemlerini kullan &quot; onay kutusunu seçin. **Model sınıfı**için kitap ' ı seçin &quot; &quot; . ( `Book` Açılan listede sınıfı görmüyorsanız, projeyi derlediğinizden emin olun.) Ardından "+" düğmesine tıklayın.

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

**Yeni veri bağlamı** Iletişim kutusunda **Ekle** ' ye tıklayın.

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

**Denetleyici Ekle** Iletişim kutusunda **Ekle** ' ye tıklayın. Scafkatlama, API denetleyicisini tanımlayan adlı bir sınıf ekler `BooksController` . Ayrıca `BooksAPIContext` , Entity Framework için veri bağlamını tanımlayan modeller klasörüne adlı bir sınıfı ekler.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>Veritabanının Çekirdeğini Oluşturma

Araçlar menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' nu seçin.

Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

Bu komut bir geçişler klasörü oluşturur ve Configuration.cs adlı yeni bir kod dosyası ekler. Bu dosyayı açın ve yöntemine aşağıdaki kodu ekleyin `Configuration.Seed` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

Paket Yöneticisi konsolu penceresinde aşağıdaki komutları yazın.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

Bu komutlar yerel bir veritabanı oluşturur ve veritabanını doldurmak için çekirdek yöntemini çağırır.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>DTO sınıfları ekleme

Uygulamayı şimdi çalıştırırsanız ve/api/Books/1 öğesine bir GET isteği gönderirseniz, yanıt aşağıdakine benzer şekilde görünür. (Okunabilirlik için girinti ekledim.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

Bunun yerine, bu isteğin, alanların bir alt kümesini döndürmesini istiyorum. Ayrıca, yazar KIMLIĞI yerine yazarın adını döndürmesini istiyorum. Bunu gerçekleştirmek için, denetleyici yöntemlerini EF modeli yerine bir *veri aktarımı nesnesi* (DTO) döndürecek şekilde değiştireceksiniz. Bir DTO yalnızca verileri taşımak için tasarlanan bir nesnedir.

Çözüm Gezgini, projeye sağ tıklayın ve **Add**  |  **Yeni klasör**Ekle ' yi seçin. &quot;DTOS klasörünü adlandırın &quot; . `BookDto`Aşağıdaki tanıma sahip DTOs klasörüne adlı bir sınıf ekleyin:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

Adlı başka bir sınıf ekleyin `BookDetailDto` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

Sonra, `BooksController` örnekleri döndürecek şekilde sınıfı güncelleştirin `BookDto` . Örneklere örnek olarak proje örnekleri eklemek için [sorgulanabilir. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) yöntemini kullanacağız `Book` `BookDto` . Controller sınıfının güncelleştirilmiş kodu aşağıda verilmiştir.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> `PutBook`, `PostBook` Ve yöntemlerini sildim, `DeleteBook` çünkü bu öğretici için gerekli değildir.

Şimdi uygulamayı çalıştırırsanız ve/api/Books/1 isteğinde bulunursa yanıt gövdesi şöyle görünmelidir:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>Rota öznitelikleri Ekle

Ardından, denetleyiciyi öznitelik yönlendirmeyi kullanacak şekilde dönüştürüyoruz. İlk olarak, denetleyiciye bir **Routeprefix** özniteliği ekleyin. Bu öznitelik, bu denetleyicideki tüm yöntemler için ilk URI segmentlerini tanımlar.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

Ardından aşağıdaki gibi, denetleyici eylemlerine **[Route]** öznitelikleri ekleyin:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

Her bir Controller yöntemi için yol şablonu, önek artı **yol** özniteliğinde belirtilen dizedir. Yöntemi için `GetBook` yol şablonu, &quot; &quot; URI segmentinin bir tamsayı değer içermesi durumunda eşleşen parametre parametreli {ID: int} dizesini içerir.

| Yöntem | Rota şablonu | Örnek URI |
| --- | --- | --- |
| `GetBooks` | "API/Kitaplar" | `http://localhost/api/books` |
| `GetBook` | "API/kitaplar/{id: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>Kitap ayrıntılarını al

Kitap ayrıntılarını almak için, istemci öğesine bir GET isteği gönderir `/api/books/{id}/details` ; burada *{id}* , kitabın kimliğidir.

Sınıfına aşağıdaki yöntemi ekleyin `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

İstek yaptıysanız `/api/books/1/details` Yanıt şöyle görünür:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>Türe göre kitap al

Belirli bir tarz kitap listesini almak için, istemci öğesine bir GET isteği gönderir `/api/books/genre` , burada *tarz* tarz adıdır. (Örneğin, `/api/books/fantasy` .)

Aşağıdaki yöntemi öğesine ekleyin `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

Burada URI şablonunda bir {tarzı} parametresi içeren bir yol tanımlanıyoruz. Web API 'sinin bu iki URI 'yi ayırt edebildiğine ve bunları farklı yöntemlere yönlendirdiğine dikkat edin:

`/api/books/1`

`/api/books/fantasy`

Bunun nedeni, `GetBook` yöntemi "ID" segmentinin bir tamsayı değeri olması gereken bir kısıtlama içerir:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

/Api/Books/FI isteğinde karşılaşırsanız, yanıt şöyle görünür:

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>Yazara göre kitaplar alın

Belirli bir yazarın kitaplarının listesini almak için, istemci öğesine bir GET isteği gönderir `/api/authors/id/books` ; burada *KIMLIK* yazarın kimliğidir.

Aşağıdaki yöntemi öğesine ekleyin `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

Bu örnek, &quot; kitaplar &quot; yazarların bir alt kaynağını kabul ettiğinden ilgi çekici bir örnektir &quot; &quot; . Bu model, yeniden gerçekleştirilen API 'lerde oldukça yaygındır.

Yol şablonundaki tilde (~), **routeprefix** özniteliğinde rota önekini geçersiz kılar.

## <a name="get-books-by-publication-date"></a>Yayın tarihine göre kitap al

Yayın tarihine göre Kitaplar listesini almak için, istemci öğesine bir GET isteği gönderir `/api/books/date/yyyy-mm-dd` ; burada *yyyy-aa-gg* tarih olur.

Bunu yapmanın bir yolu aşağıda verilmiştir:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`Parametresi bir **Tarih saat** değeriyle eşleşecek şekilde kısıtlanıyor. Bu işe yarar, ancak beğenmekten daha fazla izin veriyoruz. Örneğin, bu URI 'Ler rotayla de eşleşir:

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

Bu URI 'Lere izin veren bir sorun yok. Ancak, yol şablonuna normal ifade kısıtlaması ekleyerek yolu belirli bir biçimle kısıtlayabilirsiniz:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

Şimdi yalnızca &quot; YYYY-AA-GG biçiminde olan tarihler &quot; eşleşir. Gerçek bir tarih olduğunu doğrulamak için Regex kullandığımıza dikkat edin. Web API 'SI, URI segmentini bir **DateTime** örneğine dönüştürmeye çalıştığında işlenir. ' 2012-47-99 ' gibi geçersiz bir tarih dönüştürülemeyecek ve istemci 404 hatası alacak.

Ayrıca, `/api/books/date/yyyy/mm/dd` farklı bir Regex ile başka bir **[Route]** özniteliği ekleyerek eğik çizgi ayırıcısını () de destekleyebilirsiniz.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

Burada hafif ancak önemli bir ayrıntı vardır. İkinci yol şablonunda \* {pubdate} parametresinin başlangıcında bir joker karakter () vardır:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

Bu, yönlendirme altyapısına {pubdate} uygulamasının URI 'nin geri kalanı ile eşleştiğinden emin olduğunu söyler. Varsayılan olarak, bir şablon parametresi tek bir URI segmentiyle eşleşir. Bu durumda, {pubdate} ' nin birkaç URI kesimini yaymasına istiyoruz:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>Denetleyici kodu

BooksController sınıfının tüm kodu aşağıda verilmiştir.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>Özet

Öznitelik yönlendirme API 'niz için URI 'Leri tasarlarken daha fazla denetim ve daha fazla esneklik sağlar.
