---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Bağlantı dizesi oluşturma ve SQL Server LocalDB ile çalışma | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 4400cb8c6a5d57da60d164220f929d69d7f4d2f7
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044265"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma

`MovieDBContext`Oluşturduğunuz sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler. Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir. Gerçekten hangi veritabanını kullanacağınızı belirtmeniz gerekmez, Entity Framework varsayılan olarak [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)'yi kullanmaktır. Bu bölümde, uygulamanın *Web.config* dosyasına açıkça bir bağlantı dizesi ekleyeceğiz.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) , kullanıcı modunda isteğe bağlı ve çalışır durumda başlayan SQL Server Express veritabanı altyapısının hafif bir sürümüdür. LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modunda çalışır. Genellikle, LocalDB veritabanı dosyaları bir Web projesinin *uygulama \_ verileri* klasöründe tutulur.

SQL Server Express üretim Web uygulamalarında kullanılması önerilmez. LocalDB, IIS ile çalışmak üzere tasarlanmadığı için bir Web uygulamasıyla üretim için kullanılmamalıdır. Ancak, bir LocalDB veritabanı SQL Server veya SQL Azure kolayca geçirilebilir.

Visual Studio 2017 ' de, LocalDB, Visual Studio ile varsayılan olarak yüklenir.

Varsayılan olarak Entity Framework, nesne bağlamı sınıfıyla aynı adlı bir bağlantı dizesi arar ( `MovieDBContext` Bu proje için). Daha fazla bilgi için bkz. [ASP.NET Web uygulamaları Için bağlantı dizeleri SQL Server](https://msdn.microsoft.com/library/jj653752.aspx).

Aşağıda gösterilen uygulama kök *Web.config* dosyasını açın. ( *Görünümler* klasöründe *Web.config* dosyası değil.)

![](creating-a-connection-string/_static/image1.png)

Öğeyi bul `<connectionStrings>` :

![](creating-a-connection-string/_static/image2.png)

Aşağıdaki bağlantı dizesini `<connectionStrings>` *Web.config* dosyasındaki öğesine ekleyin.

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

Aşağıdaki örnek, yeni bağlantı dizesinin eklendiği *Web.config* dosyanın bir bölümünü gösterir:

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

İki bağlantı dizesi çok benzerdir. İlk bağlantı dizesi olarak adlandırılır `DefaultConnection` ve uygulamaya kimlerin erişebileceğini denetlemek üzere üyelik veritabanı için kullanılır. Eklediğiniz bağlantı dizesi, *uygulama \_ verileri* klasöründe bulunan *Movie. mdf* adlı bir LocalDB veritabanını belirtir. Bu öğreticide üyelik veritabanını kullanmayacağız, üyelik, kimlik doğrulama ve güvenlik hakkında daha fazla bilgi için bkz. öğreticimin [kimlik doğrulama ve SQL DB ile ASP.NET MVC uygulaması oluşturma ve Azure App Service için dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

Bağlantı dizesinin adı [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının adıyla eşleşmelidir.

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

Aslında `MovieDBContext` bağlantı dizesini eklemeniz gerekmez. Bir bağlantı dizesi belirtmezseniz, Entity Framework [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının tam adı ile Users dizininde bir LocalDB veritabanı oluşturur (Bu durumda `MvcMovie.Models.MovieDBContext` ). Veritabanına sahip olduğu sürece, istediğiniz herhangi bir şey için bir ad verebilirsiniz *. MDF* soneki. Örneğin, *MyFilms. mdf*veritabanına ad vereceğiz.

Daha sonra, `MoviesController` film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir sınıf oluşturacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-model.md) 
>  [Sonraki](accessing-your-models-data-from-a-controller.md)
