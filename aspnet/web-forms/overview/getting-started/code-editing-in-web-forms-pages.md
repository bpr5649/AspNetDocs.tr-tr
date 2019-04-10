---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013'te ASP.NET Web Forms kodunu düzenleme | Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 328dc6fb61ac562131b11b36b40f574ca5a53866
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59397376"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="04eee-102">Visual Studio 2013’te ASP.NET Web Forms Kodunu Düzenleme</span><span class="sxs-lookup"><span data-stu-id="04eee-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="04eee-103">tarafından [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="04eee-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="04eee-104">Çok sayıda ASP.NET Web formu sayfalarında, Visual Basic, C# veya başka bir dilde kod yazın.</span><span class="sxs-lookup"><span data-stu-id="04eee-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="04eee-105">Visual Studio Kod düzenleyicisinde hataları önlemeye yardımcı olurken hızla kod yazmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="04eee-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="04eee-106">Ayrıca, düzenleyici gerçekleştirmeniz gereken iş miktarını azaltmaya yardımcı olmak için yeniden kullanılabilir kod oluşturma yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="04eee-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="04eee-107">Bu izlenecek yol, Visual Studio Kod Düzenleyicisi'nin çeşitli özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="04eee-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="04eee-108">Bu kılavuz boyunca, öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="04eee-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="04eee-109">Satır içi kodlama hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="04eee-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="04eee-110">Yeniden düzenleme ve kod yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="04eee-110">Refactor and rename code.</span></span>
- <span data-ttu-id="04eee-111">Değişkenleri ve nesneleri yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="04eee-111">Rename variables and objects.</span></span>
- <span data-ttu-id="04eee-112">Kod parçacıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="04eee-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04eee-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="04eee-113">Prerequisites</span></span>


<span data-ttu-id="04eee-114">Bu izlenecek yolu tamamlamak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="04eee-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="04eee-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) veya [Web için Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="04eee-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="04eee-116">.NET Framework otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="04eee-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="04eee-117">Microsoft Visual Studio 2013 ve Web için Visual Studio Express 2013 Microsoft genellikle için Visual Studio Bu öğretici serisinin denir.</span><span class="sxs-lookup"><span data-stu-id="04eee-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="04eee-118">Visual Studio kullanıyorsanız, bu kılavuzda, seçtiğiniz varsayılır **Web geliştirme** ayarlar koleksiyonu, Visual Studio'yu ilk başlattığınızda.</span><span class="sxs-lookup"><span data-stu-id="04eee-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="04eee-119">Daha fazla bilgi için [nasıl yapılır: Web geliştirme ortam ayarlarını Seç](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="04eee-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="04eee-120">Bir Web uygulaması projesi ve bir sayfa oluşturma</span><span class="sxs-lookup"><span data-stu-id="04eee-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="04eee-121">Kılavuzun bu bölümünde, bir Web uygulaması projesi oluşturmak ve yeni bir sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="04eee-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="04eee-122">Bir Web uygulaması projesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="04eee-122">To create a Web application project</span></span>

1. <span data-ttu-id="04eee-123">Microsoft Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="04eee-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="04eee-124">Üzerinde **dosya** menüsünde **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="04eee-124">On the **File** menu, select **New Project**.</span></span>  
    ![Dosya menüsü](code-editing-in-web-forms-pages/_static/image1.png)

    <span data-ttu-id="04eee-126">**Yeni Proje** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="04eee-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="04eee-127">Seçin **şablonları**  - &gt; **Visual C#**  - &gt; **Web** soldaki şablonları grubu.</span><span class="sxs-lookup"><span data-stu-id="04eee-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="04eee-128">Seçin **ASP.NET Web uygulaması** Orta sütunda şablonu.</span><span class="sxs-lookup"><span data-stu-id="04eee-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="04eee-129">Projenizi adlandırın ***BasicWebApp*** tıklatıp **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="04eee-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
![Yeni Proje iletişim kutusu](code-editing-in-web-forms-pages/_static/image2.png)
6. <span data-ttu-id="04eee-131">Ardından, **Web Forms** şablonu ve tıklatın **Tamam** projeyi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="04eee-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
![Yeni ASP.NET projesi iletişim kutusu](code-editing-in-web-forms-pages/_static/image3.png)  

    <span data-ttu-id="04eee-133">Visual Studio Web Forms şablonu temel alan önceden oluşturulmuş işlevler içeren yeni bir proje oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04eee-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="04eee-134">Yeni bir ASP.NET Web Forms sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="04eee-134">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="04eee-135">Yeni Web Forms kullanarak bir uygulama oluşturduğunuzda **ASP.NET Web uygulaması** proje şablonu, Visual Studio ekler adlı bir ASP.NET sayfasına (Web Forms sayfası) *Default.aspx*, yanı sıra birkaç diğer dosya ve klasörler.</span><span class="sxs-lookup"><span data-stu-id="04eee-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="04eee-136">Kullanabileceğiniz *Default.aspx* sayfasında Web uygulamanız için giriş sayfası olarak.</span><span class="sxs-lookup"><span data-stu-id="04eee-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="04eee-137">Ancak, bu kılavuz için oluşturur ve yeni bir sayfa ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="04eee-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="04eee-138">Web uygulaması için bir sayfa eklemek için</span><span class="sxs-lookup"><span data-stu-id="04eee-138">To add a page to the Web application</span></span>


1. <span data-ttu-id="04eee-139">İçinde **Çözüm Gezgini**, Web uygulamasının adını sağ tıklayın (Bu öğreticide uygulama adı **BasicWebSite**) ve ardından **Ekle**  - &gt; **Yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="04eee-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="04eee-140">**Yeni Öğe Ekle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="04eee-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="04eee-141">Seçin **Visual C#**  - &gt; **Web** soldaki şablonları grubu.</span><span class="sxs-lookup"><span data-stu-id="04eee-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="04eee-142">Ardından, **Web formu** ortasından listesinde ve adlandırın *FirstWebPage.aspx*.</span><span class="sxs-lookup"><span data-stu-id="04eee-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    ![Yeni Öğe Ekle iletişim kutusu](code-editing-in-web-forms-pages/_static/image4.png)
3. <span data-ttu-id="04eee-144">Tıklayın **Ekle** Web Forms sayfası projenize eklenecek.</span><span class="sxs-lookup"><span data-stu-id="04eee-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="04eee-145">Visual Studio, yeni bir sayfa oluşturur ve açar.</span><span class="sxs-lookup"><span data-stu-id="04eee-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="04eee-146">Ardından, bu yeni sayfa varsayılan başlangıç sayfası olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="04eee-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="04eee-147">İçinde **Çözüm Gezgini**, adlı yeni bir sayfa sağ *FirstWebPage.aspx* seçip **başlangıç sayfası olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="04eee-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="04eee-148">İlerlememizin, test etmek için bu uygulamayı bir sonraki çalıştırmanızda otomatik olarak bu tarayıcıdaki yeni bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="04eee-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="04eee-149">Satır içi kodlama hataları düzeltme</span><span class="sxs-lookup"><span data-stu-id="04eee-149">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="04eee-150">Visual Studio Kod düzenleyicisinde kod yazma ve bir hata yaptıysanız, Kod Düzenleyicisi hatayı düzeltmek için yardımcı olan hataları önlemek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="04eee-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="04eee-151">Kılavuzun bu bölümünde bir Düzenleyicisi'nde hata düzeltme özellikleri gösteren bir kod satırı yazar.</span><span class="sxs-lookup"><span data-stu-id="04eee-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="04eee-152">Visual Studio'da basit kodlama hatalarını düzeltmek için</span><span class="sxs-lookup"><span data-stu-id="04eee-152">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="04eee-153">İçinde **tasarım** görünümünde, boş bir sayfa için bir işleyici oluşturmak için çift tıklatın **yük** sayfa için olay.</span><span class="sxs-lookup"><span data-stu-id="04eee-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="04eee-154">Olay işleyicisi yalnızca bir yer olarak bazı kodlar yazma için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="04eee-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="04eee-155">İşleyici içinde bir hata ve ENTER tuşuna içeren aşağıdaki satırdan **ENTER**:</span><span class="sxs-lookup"><span data-stu-id="04eee-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="04eee-156">Bastığınızda **ENTER**, Kod Düzenleyicisi, yeşil ve kırmızı alt çizgiler yerleştirir (sık çağrı &quot;dalgalı&quot; satırları) sorunları kod alanlarının altında.</span><span class="sxs-lookup"><span data-stu-id="04eee-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="04eee-157">Yeşil bir çizgi bir uyarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="04eee-157">A green underline indicates a warning.</span></span> <span data-ttu-id="04eee-158">Kırmızı alt çizgi, düzeltmeniz gerekir bir hata olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="04eee-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="04eee-159">Fare işaretçisini tutun `myStr` hakkında uyarı bildiren bir araç ipucu görmek için.</span><span class="sxs-lookup"><span data-stu-id="04eee-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="04eee-160">Ayrıca, fare işaretçisini hata iletisini görmek için kırmızı alt çizgi üzerinde tutun.</span><span class="sxs-lookup"><span data-stu-id="04eee-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="04eee-161">Aşağıdaki görüntüde, alt çizgi ile kod gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="04eee-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="04eee-162">![Hoş Geldiniz metni Tasarım görünümünde](code-editing-in-web-forms-pages/_static/image5.png "metin Tasarım görünümünde Hoş Geldiniz")</span><span class="sxs-lookup"><span data-stu-id="04eee-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="04eee-163">Noktalı virgül ekleyerek hatanın düzeltilmesi gereken `;` satırın sonuna.</span><span class="sxs-lookup"><span data-stu-id="04eee-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="04eee-164">Uyarı yeterlidir, kullanmadığınız alacağınızı `myStr` henüz değişkeni.</span><span class="sxs-lookup"><span data-stu-id="04eee-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="04eee-165">Visual Studio'da ayarlar seçerek biçimlendirme, geçerli kod görüntüleme **Araçları**  - &gt; **seçenekleri**  - &gt; **yazı tipleri ve Renkleri**.</span><span class="sxs-lookup"><span data-stu-id="04eee-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="04eee-166">Yeniden düzenleme ve yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="04eee-166">Refactoring and Renaming</span></span>

<span data-ttu-id="04eee-167">Yeniden düzenleme, kodunuzu anlamak ve işlevselliğini korurken korumak için daha kolay hale getirmek için yeniden yapılandırma içeren bir yazılım Metodoloji olur.</span><span class="sxs-lookup"><span data-stu-id="04eee-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="04eee-168">Basit bir örnek veritabanından veri almak için bir olay işleyicisine kod yazma olabilir.</span><span class="sxs-lookup"><span data-stu-id="04eee-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="04eee-169">Sayfanız geliştirirken, birkaç farklı işleyicilerindeki verilere erişmek gereken keşfedin.</span><span class="sxs-lookup"><span data-stu-id="04eee-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="04eee-170">Bu nedenle, bir veri erişim yöntemi sayfasında oluşturarak ve yöntemine yönelik çağrılar işleyicileri ekleme sayfanın kodun yeniden.</span><span class="sxs-lookup"><span data-stu-id="04eee-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="04eee-171">Kod Düzenleyicisi, yeniden düzenleme çeşitli görevleri gerçekleştirmenize yardımcı olacak araçlar içerir.</span><span class="sxs-lookup"><span data-stu-id="04eee-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="04eee-172">Bu kılavuzda, yeniden düzenleme iki teknikleri ile çalışır: değişkenleri yeniden adlandırma ve yöntemleri ayıklanıyor.</span><span class="sxs-lookup"><span data-stu-id="04eee-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="04eee-173">Diğer yeniden düzenleme seçeneklerini alanları Kapsüllenen, yöntem parametreleri yerel değişkenlere yükseltme ve yöntem parametreleri yönetme içerir.</span><span class="sxs-lookup"><span data-stu-id="04eee-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="04eee-174">Bu yeniden düzenleme seçeneklerini kullanılabilirliğini kodun konumuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="04eee-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="04eee-175">Kodu yeniden düzenleme</span><span class="sxs-lookup"><span data-stu-id="04eee-175">Refactoring Code</span></span>

<span data-ttu-id="04eee-176">Genel bir yeniden düzenleme senaryoyu (Ayıkla) oluşturmaktır bir yöntem içinde bir yöntemi gibi başka bir üye kodu.</span><span class="sxs-lookup"><span data-stu-id="04eee-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="04eee-177">Bu ilk üyenin boyutunu azaltır ve ayıklanan kod yeniden kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="04eee-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="04eee-178">Kılavuzun bu bölümünde bazı basit kod yazın ve ardından bir yöntem bundan ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="04eee-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="04eee-179">C# programlama dili kullanan bir sayfa oluşturacak şekilde yeniden düzenleme C# ' ta desteklenir.</span><span class="sxs-lookup"><span data-stu-id="04eee-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="04eee-180">Bir C# sayfasında bir yöntem ayıklamak için</span><span class="sxs-lookup"><span data-stu-id="04eee-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="04eee-181">Geçiş **tasarım** görünümü.</span><span class="sxs-lookup"><span data-stu-id="04eee-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="04eee-182">İçinde **araç kutusu**, gelen **standart** sekmesinde, sürükleyin bir [düğmesi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) sayfaya denetim.</span><span class="sxs-lookup"><span data-stu-id="04eee-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="04eee-183">Çift **düğmesi** denetim işleyicisi oluşturmak için kendi [tıklayın](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olay ve ardından aşağıdaki vurgulanmış kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="04eee-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="04eee-184">Kod oluşturur bir **ArrayList** nesnesi değerlerle yüklemek için bir döngü kullanır ve ardından içeriğini görüntülemek için başka bir döngü kullanır **ArrayList** nesne.</span><span class="sxs-lookup"><span data-stu-id="04eee-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="04eee-185">Tuşuna **CTRL + F5** sayfayı çalıştırın ve ardından **düğmesi** aşağıdaki çıktıyı gördüğünüzü emin olmak için:</span><span class="sxs-lookup"><span data-stu-id="04eee-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="04eee-186">Kod Düzenleyicisi'ne dönmek ve olay işleyicisi aşağıdaki satırları seçin.</span><span class="sxs-lookup"><span data-stu-id="04eee-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="04eee-187">Seçime sağ tıklayın, **yeniden düzenleme**ve ardından **yöntemi ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="04eee-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="04eee-188">**Yöntemi ayıklama** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="04eee-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="04eee-189">İçinde **yeni yöntem adı** kutusuna **DisplayArray**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="04eee-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="04eee-190">Kod Düzenleyicisi adlı yeni bir yöntem oluşturur `DisplayArray`ve yeni yönteme bir çağrı koyar **tıklayın** döngü nerede oluştuğunu başlangıçta işleyici.</span><span class="sxs-lookup"><span data-stu-id="04eee-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="04eee-191">Tuşuna **CTRL + F5** yeniden çalıştırırsanız ve **düğmesi**.</span><span class="sxs-lookup"><span data-stu-id="04eee-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="04eee-192">Önce yaptığınız gibi sayfa aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="04eee-192">The page functions the same as it did before.</span></span> <span data-ttu-id="04eee-193">`DisplayArray` Yöntemi çağrısı nerede olursanız olun artık olabilir sayfa sınıfında.</span><span class="sxs-lookup"><span data-stu-id="04eee-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="04eee-194">Değişkenleri yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="04eee-194">Renaming Variables</span></span>

<span data-ttu-id="04eee-195">Değişkenleri, yanı sıra nesneleri çalışırken, zaten kodunuzda başvurulan sonra bunları yeniden adlandırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04eee-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="04eee-196">Ancak, değişkenler ve nesneler yeniden adlandırma başvurulardan birini yeniden adlandırma kaçırmanıza kesmek için kodu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="04eee-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="04eee-197">Bu nedenle, yeniden adlandırma gerçekleştirmek için yeniden düzenleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04eee-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="04eee-198">Bir değişkeni yeniden adlandırmak için yeniden düzenleme kullanmak için</span><span class="sxs-lookup"><span data-stu-id="04eee-198">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="04eee-199">İçinde **tıklayın** olay işleyicisi, aşağıdaki satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="04eee-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="04eee-200">Değişken adına sağ tıklayın `alist`, seçin **yeniden düzenleme**ve ardından **Yeniden Adlandır**.</span><span class="sxs-lookup"><span data-stu-id="04eee-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="04eee-201">**Yeniden Adlandır** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="04eee-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="04eee-202">İçinde **yeni adı** kutusuna **ArrayList1** emin **başvuru değişikliklerini önizle** onay kutusunun seçili.</span><span class="sxs-lookup"><span data-stu-id="04eee-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="04eee-203">Sonra **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04eee-203">Then click **OK**.</span></span>

    <span data-ttu-id="04eee-204">**Değişiklikleri Önizle** iletişim kutusu görünür ve tüm başvuruları yeniden adlandırdığınız değişkeni içeren bir ağaç görüntüler.</span><span class="sxs-lookup"><span data-stu-id="04eee-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="04eee-205">Tıklayın **Uygula** kapatmak için **Değişiklikleri Önizle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="04eee-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="04eee-206">Özellikle, seçtiğiniz örneğine başvurma değişkenleri yeniden adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="04eee-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="04eee-207">Ancak, unutmayın, değişken `alist` aşağıdaki satırda yeniden adlandırılmaz.</span><span class="sxs-lookup"><span data-stu-id="04eee-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="04eee-208">Değişken `alist` değişkeni aynı değeri temsil etmediğinden bu satırda yeniden adlandırılmış değil `alist` adlandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="04eee-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="04eee-209">Değişken `alist` içinde `DisplayArray` bu yöntem için bir yerel değişken bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="04eee-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="04eee-210">Bu değişkenler yeniden adlandırmak için yeniden düzenleme kullanarak yalnızca düzenleyicide Bul ve Değiştir eylemini gerçekleştirmekten daha farklı olduğunu gösterir; yeniden düzenleme ile çalışma değişkeni semantiği bilgisi değişkenlerle yeniden adlandırır.</span><span class="sxs-lookup"><span data-stu-id="04eee-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="04eee-211">Kod parçacıkları ekleme</span><span class="sxs-lookup"><span data-stu-id="04eee-211">Inserting Snippets</span></span>

<span data-ttu-id="04eee-212">Web Forms geliştiriciler sık yapmanız gereken birçok kodlama görevleri olduğundan, Kod Düzenleyicisi kod parçacıkları veya önceden kod blokları bir kitaplık sağlar.</span><span class="sxs-lookup"><span data-stu-id="04eee-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="04eee-213">Bu kod parçacıklarının sayfanıza ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04eee-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="04eee-214">Visual Studio'da kullandığınız her bir dilin kod parçacıkları ekleme küçük farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="04eee-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="04eee-215">Kod parçacıkları ekleme hakkında daha fazla bilgi için bkz: [Visual Basic IntelliSense kodu parçacıkları](https://msdn.microsoft.com/library/18yz4be4.aspx).</span><span class="sxs-lookup"><span data-stu-id="04eee-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="04eee-216">Visual C# içinde kod parçacıkları ekleme hakkında daha fazla bilgi için bkz: [Visual C# kod parçacıkları](https://msdn.microsoft.com/library/z41h7fat.aspx).</span><span class="sxs-lookup"><span data-stu-id="04eee-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04eee-217">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="04eee-217">Next Steps</span></span>

<span data-ttu-id="04eee-218">Bu izlenecek kodunuzdaki hataları düzeltme, kodu yeniden düzenleme, yeniden adlandırma değişkenleri ve kodunuza kod parçacıkları ekleme için Visual Studio 2010 Kod Düzenleyicisi'ni temel özelliklerinde gösterilen.</span><span class="sxs-lookup"><span data-stu-id="04eee-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="04eee-219">Ek özellik Düzenleyicisi'nde uygulama geliştirme hızlı ve kolay hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04eee-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="04eee-220">Örneğin, aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04eee-220">For example, you might want to:</span></span>

- <span data-ttu-id="04eee-221">IntelliSense kod parçacıkları için çevrimiçi arama IntelliSense seçeneklerini değiştirme ve kod parçacıkları yönetme gibi özellikleri hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="04eee-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="04eee-222">Daha fazla bilgi için [IntelliSense kullanarak](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span><span class="sxs-lookup"><span data-stu-id="04eee-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="04eee-223">Kendi kod parçacıklarınızı oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="04eee-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="04eee-224">Daha fazla bilgi için [oluşturma ve IntelliSense kod parçacıkları kullanma](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="04eee-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="04eee-225">Visual Basic'e özel IntelliSense kod parçacıkları, kod parçacıkları özelleştirme ve sorun giderme gibi özellikleri hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="04eee-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="04eee-226">Daha fazla bilgi için [Visual Basic IntelliSense kod parçacıkları](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="04eee-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="04eee-227">C# hakkında daha fazla bilgi-IntelliSense, yeniden düzenleme ve kod parçacıkları gibi belirli özellikleri.</span><span class="sxs-lookup"><span data-stu-id="04eee-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="04eee-228">Daha fazla bilgi için [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span><span class="sxs-lookup"><span data-stu-id="04eee-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
