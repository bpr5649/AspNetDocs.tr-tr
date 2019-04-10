---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: Denetleyici (C#) oluşturma | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther bir denetleyici bir ASP.NET MVC uygulamasına nasıl ekleyebileceğinizi gösterir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: c92d7cdeb7b2d31d5eca810628e9f563840f7494
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400621"
---
# <a name="creating-a-controller-c"></a><span data-ttu-id="be9d2-103">Denetleyici Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="be9d2-103">Creating a Controller (C#)</span></span>

<span data-ttu-id="be9d2-104">tarafından [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="be9d2-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="be9d2-105">Bu öğreticide, Stephen Walther bir denetleyici bir ASP.NET MVC uygulamasına nasıl ekleyebileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="be9d2-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>


<span data-ttu-id="be9d2-106">Bu öğreticinin amacı, yeni ASP.NET MVC denetleyicileri nasıl oluşturabileceğinizi açıklar sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="be9d2-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="be9d2-107">Visual Studio denetleyici Ekle menü seçeneğini kullanarak hem bir sınıf dosyası el ile oluşturarak denetleyicileri oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="be9d2-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="be9d2-108">Kullanarak denetleyici menü seçeneği ekleyin</span><span class="sxs-lookup"><span data-stu-id="be9d2-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="be9d2-109">Visual Studio Çözüm Gezgini penceresinde denetleyicileri klasörü sağ tıklatın ve seçin için yeni bir denetleyicisi oluşturmak için en kolay yolu olan **Ekle, denetleyici** menü seçeneği (bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="be9d2-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="be9d2-110">Bu menü seçeneğini belirleyerek açılır **denetleyici Ekle** iletişim (bkz: Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="be9d2-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>


[![T<span data-ttu-id="be9d2-111">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="be9d2-111">he New Project dialog box]</span></span>(creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

<span data-ttu-id="be9d2-112">**Şekil 01**: Yeni denetleyici ekleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="be9d2-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>


[![T<span data-ttu-id="be9d2-113">Yeni Proje iletişim kutusu he]</span><span class="sxs-lookup"><span data-stu-id="be9d2-113">he New Project dialog box]</span></span>(creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

<span data-ttu-id="be9d2-114">**Şekil 02**: Denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="be9d2-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>


<span data-ttu-id="be9d2-115">Denetleyici adının ilk bölümü vurgulanan bildirimi **denetleyici Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be9d2-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="be9d2-116">Her Denetleyici adı soneki ile sona ermelidir *denetleyicisi*.</span><span class="sxs-lookup"><span data-stu-id="be9d2-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="be9d2-117">Örneğin, adında bir denetleyici oluşturabilirsiniz *ProductController* ancak adlı bir denetleyici *ürün*.</span><span class="sxs-lookup"><span data-stu-id="be9d2-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>


<span data-ttu-id="be9d2-118">Eksik bir denetleyici oluşturursanız *denetleyicisi* denetleyici çağrılacak mümkün olmayacaktır sonra soneki.</span><span class="sxs-lookup"><span data-stu-id="be9d2-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="be9d2-119">Bunu yapmayın--bu hata yaptıktan sonra doğduğum sayısız saatler boşa.</span><span class="sxs-lookup"><span data-stu-id="be9d2-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>


**<span data-ttu-id="be9d2-120">Listing 1 - Controllers\ProductController.cs</span><span class="sxs-lookup"><span data-stu-id="be9d2-120">Listing 1 - Controllers\ProductController.cs</span></span>**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="be9d2-121">Her zaman denetleyicileri klasöründe denetleyicileri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be9d2-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="be9d2-122">Aksi takdirde, ASP.NET MVC kurallarını ihlal ve diğer geliştiriciler, uygulamanızın anlamak daha zor bir zaman alacaktır.</span><span class="sxs-lookup"><span data-stu-id="be9d2-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="be9d2-123">Yapı iskelesi eylem yöntemleri</span><span class="sxs-lookup"><span data-stu-id="be9d2-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="be9d2-124">Bir denetleyici oluşturduğunuzda, oluşturma, güncelleştirme ve ayrıntıları eylem yöntemlerine otomatik olarak oluşturma seçeneğiniz vardır (bkz: Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="be9d2-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="be9d2-125">Ardından bu seçeneği belirlerseniz listeleme 2 controller sınıfında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be9d2-125">If you select this option then the controller class in Listing 2 is generated.</span></span>


[![C<span data-ttu-id="be9d2-126">reating eylem yöntemlerine otomatik olarak]</span><span class="sxs-lookup"><span data-stu-id="be9d2-126">reating action methods automatically]</span></span>(creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

<span data-ttu-id="be9d2-127">**Şekil 03**: Eylem yöntemlerine otomatik olarak oluşturma ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="be9d2-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>


**<span data-ttu-id="be9d2-128">2 - Controllers\CustomerController.cs listeleme</span><span class="sxs-lookup"><span data-stu-id="be9d2-128">Listing 2 - Controllers\CustomerController.cs</span></span>**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="be9d2-129">Saptama yöntemleri bu oluşturulan yöntemlerdir.</span><span class="sxs-lookup"><span data-stu-id="be9d2-129">These generated methods are stub methods.</span></span> <span data-ttu-id="be9d2-130">Oluşturma, güncelleştirme ve kendiniz için bir müşterinin ayrıntılarını gösteren fiili mantığı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be9d2-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="be9d2-131">Ancak, saptama yöntemleri ile güzel bir başlangıç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="be9d2-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="be9d2-132">Denetleyici sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be9d2-132">Creating a Controller Class</span></span>

<span data-ttu-id="be9d2-133">ASP.NET MVC denetleyicisi, yalnızca bir sınıf değil.</span><span class="sxs-lookup"><span data-stu-id="be9d2-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="be9d2-134">İsterseniz, uygun Visual Studio denetleyicisi iskele yoksaymak ve el ile bir denetleyici sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be9d2-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="be9d2-135">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="be9d2-135">Follow these steps:</span></span>

1. <span data-ttu-id="be9d2-136">Menü seçeneği denetleyicileri klasörüne sağ tıklayıp **Ekle, yeni öğe** seçip **sınıfı** şablonu (bkz: Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="be9d2-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="be9d2-137">Yeni bir sınıf PersonController.cs adlandırın ve tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be9d2-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="be9d2-138">Temel System.Web.Mvc.Controller sınıfından (3 listeleme bakın) sınıfından devralan elde edilen sınıf dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="be9d2-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>


[![C<span data-ttu-id="be9d2-139">Yeni bir sınıf reating]</span><span class="sxs-lookup"><span data-stu-id="be9d2-139">reating a new class]</span></span>(creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

<span data-ttu-id="be9d2-140">**Şekil 04**: Yeni bir sınıf oluşturursunuz ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-controller-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="be9d2-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>


**<span data-ttu-id="be9d2-141">Listing 3 - Controllers\PersonController.cs</span><span class="sxs-lookup"><span data-stu-id="be9d2-141">Listing 3 - Controllers\PersonController.cs</span></span>**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="be9d2-142">Denetleyici listeleme 3'te, "Hello World!" dizesini döndürür İNDİS() adlı bir eylem kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="be9d2-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="be9d2-143">Bu denetleyici eylemi, uygulamanızı çalıştıran ve aşağıdaki gibi bir URL isteyen çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be9d2-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="be9d2-144">ASP.NET Geliştirme Sunucusu bir rastgele bağlantı noktası numarası (örneğin, 40071) kullanır.</span><span class="sxs-lookup"><span data-stu-id="be9d2-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="be9d2-145">Bir denetleyici çağırmak için bir URL girerken, doğru bağlantı noktası numarası girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be9d2-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="be9d2-146">ASP.NET Geliştirme Sunucusu (sağ alt ekranınızın) Windows bildirim alanındaki simgenin üzerine farenizi gelerek, bağlantı noktası numarasını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be9d2-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="be9d2-147">[Önceki](adding-dynamic-content-to-a-cached-page-cs.md)
> [İleri](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="be9d2-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
