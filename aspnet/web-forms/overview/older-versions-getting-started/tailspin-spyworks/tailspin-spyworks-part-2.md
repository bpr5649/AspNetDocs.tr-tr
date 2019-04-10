---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Bölüm 2: Veri erişim katmanı | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 2. bölüm, veri erişim katmanı ekleyerek kapsar.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378399"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="61eec-104">Bölüm 2: Veri Erişim Katmanı</span><span class="sxs-lookup"><span data-stu-id="61eec-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="61eec-105">tarafından [ALi Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="61eec-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="61eec-106">Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="61eec-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="61eec-107">Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="61eec-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="61eec-108">Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="61eec-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="61eec-109">2. bölüm, veri erişim katmanı ekleyerek kapsar.</span><span class="sxs-lookup"><span data-stu-id="61eec-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="61eec-110">Veri erişim katmanı ekleme</span><span class="sxs-lookup"><span data-stu-id="61eec-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="61eec-111">E-ticaret uygulamamız iki veritabanlarında bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="61eec-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="61eec-112">Standart ASP.NET üyelik veritabanı müşteri bilgileri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="61eec-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="61eec-113">Alışveriş sepeti ve ürün kataloğu için size bir SQL Express veritabanı gibi uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="61eec-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="61eec-114">' % S'veritabanı (Commerce.mdf) uygulamanın uygulamada oluşturduğunuza\_biz devam edebilirsiniz, veri erişim katmanı .NET Entity Framework kullanarak oluşturmak için veri klasörü.</span><span class="sxs-lookup"><span data-stu-id="61eec-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="61eec-115">Adlı bir klasör oluşturacağız "veri\_erişim" ve bunları bu klasörü sağ tıklatın ve "Yeni Öğe Ekle"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="61eec-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="61eec-116">"Yüklü şablonlarında" öğesini ve ardından "ADO.NET varlık veri modeli" EDM girin\_Commerce.edmx adı olarak "Ekle" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61eec-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="61eec-117">"Veritabanından oluştur" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="61eec-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="61eec-118">Kaydet ve derleyin.</span><span class="sxs-lookup"><span data-stu-id="61eec-118">Save and build.</span></span>

<span data-ttu-id="61eec-119">Artık ilk özelliğimiz – bir ürün kategorisini menü eklemek hazırız.</span><span class="sxs-lookup"><span data-stu-id="61eec-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="61eec-120">[Önceki](tailspin-spyworks-part-1.md)
> [İleri](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="61eec-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
