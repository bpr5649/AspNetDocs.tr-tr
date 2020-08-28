---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Model ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045123"
---
# <a name="adding-a-model"></a>Model Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](~/includes/razor.md)]

Bu bölümde, bir veritabanında film yönetmeye yönelik bazı sınıflar ekleyeceksiniz. Bu sınıflar, &quot; &quot; ASP.NET MVC uygulamasının model parçası olacaktır.

Bu model sınıflarını tanımlamak ve bunlarla çalışmak için [Entity Framework](https://docs.microsoft.com/ef/) olarak bilinen .NET Framework veri erişim teknolojisini kullanacaksınız. Entity Framework (genellikle EF olarak adlandırılır) *Code First*adlı bir geliştirme paradigmasını destekler. Code First basit sınıflar yazarak model nesneleri oluşturmanızı sağlar. (Bunlar ayrıca, düz eski CLR nesnelerinden POCO sınıfları olarak da bilinir &quot; . &quot; ) Daha sonra veritabanı, çok temiz ve hızlı bir geliştirme iş akışını sağlayan sınıflarınızda anında oluşturulmuş olabilir. Önce veritabanını oluşturmanız gerekiyorsa, MVC ve EF uygulama geliştirme hakkında bilgi edinmek için bu öğreticiyi izleyebilirsiniz. Daha sonra veritabanı ilk yaklaşımını kapsayan Tom Fizmakens [ASP.net Scafkatlama](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) öğreticisini izleyebilirsiniz.

## <a name="adding-model-classes"></a>Model sınıfları ekleme

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![](adding-a-model/_static/image1.png)

Film *sınıfı* adını girin &quot; &quot; .

Sınıfına aşağıdaki beş özelliği ekleyin `Movie` :

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

`Movie`Bir veritabanındaki filmleri göstermek için sınıfını kullanacağız. Bir nesnenin her örneği `Movie` , bir veritabanı tablosundaki bir satıra karşılık gelir ve sınıfın her özelliği `Movie` tablodaki bir sütunla eşlenir.

Note: System. Data. Entity ve ilgili sınıfı kullanabilmek için [Entity Framework NuGet paketini](https://www.nuget.org/packages/EntityFramework/)yüklemeniz gerekir. Daha fazla yönerge için bağlantıyı izleyin.

Aynı dosyada, aşağıdaki `MovieDBContext` sınıfı ekleyin:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`Sınıfı, `Movie` bir veritabanında sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework film veritabanı bağlamını temsil eder. , `MovieDBContext` `DbContext` Entity Framework tarafından belirtilen temel sınıftan türetilir.

Ve ' nin başvurabilebilmesi için `DbContext` `DbSet` `using` dosyanın en üstüne aşağıdaki ifadeyi eklemeniz gerekir:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Bunu, using ifadesini el ile ekleyerek yapabilir veya kırmızı dalgalı çizgilerin üzerine geldiğinizde `Show potential fixes` , ' ye tıklayıp `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Note: birkaç kullanılmamış `using` deyim kaldırılmıştır. Visual Studio, kullanılmayan bağımlılıkları gri olarak gösterecektir. Kullanılmayan bağımlılıkları gri bağımlılıkların üzerine gelerek kaldırabilirsiniz ve kullanılmayan kullanımları Kaldır ' a tıklayın `Show potential fixes` **.**

![](adding-a-model/_static/image3.png)

Son olarak bir model ekledik (MVC 'de d). Sonraki bölümde, veritabanı bağlantı dizesiyle çalışacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-view.md) 
>  [Sonraki](creating-a-connection-string.md)
