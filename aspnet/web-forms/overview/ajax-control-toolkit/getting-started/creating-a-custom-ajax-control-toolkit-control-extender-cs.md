---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: Oluşturma özel AJAX Denetim Araç Seti denetim Genişleticisi (C#) | Microsoft Docs
author: microsoft
description: Özel Genişleticileri özelleştirmek ve yeni sınıflar oluşturmak zorunda kalmadan ASP.NET denetimleri yeteneklerini genişletmek etkinleştirin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: b9a3b9a8d5c86cc7aac6aeb8b4bac48af2e2edc7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066690"
---
<a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a><span data-ttu-id="257bb-103">Özel AJAX Denetim Araç Seti Denetim Genişleticisi Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="257bb-103">Creating a Custom AJAX Control Toolkit Control Extender (C#)</span></span>
====================
<span data-ttu-id="257bb-104">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="257bb-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="257bb-105">Özel Genişleticileri özelleştirmek ve yeni sınıflar oluşturmak zorunda kalmadan ASP.NET denetimleri yeteneklerini genişletmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="257bb-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>


<span data-ttu-id="257bb-106">Bu öğreticide, bir özel AJAX Denetim Araç Seti denetim Genişleticisi oluşturma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="257bb-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="257bb-107">Basit, ancak bir metin kutusuna bir metin yazın, etkin için devre dışı bir düğmenin durumu değişir kullanışlı, yeni genişletici oluştururuz.</span><span class="sxs-lookup"><span data-stu-id="257bb-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="257bb-108">Bu öğreticide okuduktan sonra ASP.NET AJAX araç seti ile kendi denetim genişleticilerini genişletmek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="257bb-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="257bb-109">Visual Studio veya Visual Web Developer kullanarak bir özel denetim genişleticilerini oluşturabilirsiniz (Visual Web Developer en son sürümüne sahip olduğunuzdan emin olun).</span><span class="sxs-lookup"><span data-stu-id="257bb-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="257bb-110">DisabledButton genişletici genel bakış</span><span class="sxs-lookup"><span data-stu-id="257bb-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="257bb-111">Sunduğumuz yeni denetim genişletici DisabledButton genişletici adı verilir.</span><span class="sxs-lookup"><span data-stu-id="257bb-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="257bb-112">Bu genişletici üç özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="257bb-112">This extender will have three properties:</span></span>

- <span data-ttu-id="257bb-113">TargetControlID - metin kutusu denetimini genişletir.</span><span class="sxs-lookup"><span data-stu-id="257bb-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="257bb-114">TargetButtonIID - etkin veya devre dışı düğme.</span><span class="sxs-lookup"><span data-stu-id="257bb-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="257bb-115">DisabledText - başlangıçta düğmede görüntülenen metni.</span><span class="sxs-lookup"><span data-stu-id="257bb-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="257bb-116">Yazmaya başladığınızda, düğmenin düğme metin özelliğini değerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="257bb-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="257bb-117">Bir metin kutusu ve düğme denetimine DisabledButton genişletici bağlayın.</span><span class="sxs-lookup"><span data-stu-id="257bb-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="257bb-118">Herhangi bir metin yazın önce düğmesi devre dışıdır ve metin kutusu ve düğme şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="257bb-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

<span data-ttu-id="257bb-119">([Tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span></span>


<span data-ttu-id="257bb-120">Yazılan metin başlattıktan sonra düğmesi etkinleştirilir ve metin kutusu ve düğme şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="257bb-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

<span data-ttu-id="257bb-121">([Tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span></span>


<span data-ttu-id="257bb-122">Bizim denetim Genişleticisi oluşturmak için size aşağıdaki üç dosyayı oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="257bb-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="257bb-123">DisabledButtonExtender.cs - Bu dosya, Genişleticisi oluşturma, yönetme ve tasarım zamanında özelliklerini ayarlamanıza olanak sağlar sunucu tarafı denetim sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="257bb-123">DisabledButtonExtender.cs - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="257bb-124">Ayrıca extender'ayarlanabilir özellikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="257bb-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="257bb-125">Bu özellikler aracılığıyla kod ve tasarım zamanında erişebilir ve DisableButtonBehavior.js dosyasında tanımlanan özellikler eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="257bb-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="257bb-126">DisabledButtonBehavior.js--, Tüm istemci kod mantığınızı nereye ekleyeceksiniz bu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="257bb-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="257bb-127">Bu sınıf, DisabledButtonDesigner.cs - tasarım zamanı işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="257bb-127">DisabledButtonDesigner.cs - This class enables design-time functionality.</span></span> <span data-ttu-id="257bb-128">Bu sınıf, Visual Studio/Visual Web Developer Tasarımcısı ile düzgün çalışması için Denetim genişletici istiyorsanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="257bb-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="257bb-129">Bu nedenle bir denetim genişletici sunucu tarafı denetimlerdir, bir istemci-tarafı davranışı ve sunucu tarafı Tasarımcı sınıfını içerir.</span><span class="sxs-lookup"><span data-stu-id="257bb-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="257bb-130">Aşağıdaki bölümlerde bu dosyaların üç oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="257bb-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="257bb-131">Özel genişletici Web sitesi ve proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="257bb-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="257bb-132">İlk adım bir sınıf kitaplığı projesi ve Web sitesi Visual Studio/Visual Web Developer oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="257bb-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="257bb-133">Biz ll özel genişletici sınıf kitaplığı projesi oluşturun ve Web sitesi özel genişletici sınayın.</span><span class="sxs-lookup"><span data-stu-id="257bb-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="257bb-134">Web sitesiyle başlama s olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="257bb-134">Let�s start with the website.</span></span> <span data-ttu-id="257bb-135">Web sitesi oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="257bb-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="257bb-136">Menü seçeneğini **dosya, yeni Web sitesi**.</span><span class="sxs-lookup"><span data-stu-id="257bb-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="257bb-137">Seçin **ASP.NET Web sitesi** şablonu.</span><span class="sxs-lookup"><span data-stu-id="257bb-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="257bb-138">Yeni Web sitesi adı *websitesi1*.</span><span class="sxs-lookup"><span data-stu-id="257bb-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="257bb-139">Tıklayın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="257bb-139">Click the **OK** button.</span></span>

<span data-ttu-id="257bb-140">Ardından, biz denetim genişletici için kod içeren sınıf kitaplığı projesi oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="257bb-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="257bb-141">Menü seçeneğini **dosya, Ekle, yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="257bb-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="257bb-142">Seçin **sınıf kitaplığı** şablonu.</span><span class="sxs-lookup"><span data-stu-id="257bb-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="257bb-143">Yeni sınıf kitaplığı adı ile **CustomExtenders**.</span><span class="sxs-lookup"><span data-stu-id="257bb-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="257bb-144">Tıklayın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="257bb-144">Click the **OK** button.</span></span>

<span data-ttu-id="257bb-145">Bu adımları tamamladıktan sonra Çözüm Gezgini penceresinde Şekil 1 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="257bb-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>


<span data-ttu-id="257bb-146">[![Web sitesi ve sınıf kitaplığı projesi ile çözüm](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="257bb-147">**Şekil 01**: Web sitesi ve sınıf kitaplığı projesi olan çözüm ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span></span>


<span data-ttu-id="257bb-148">Ardından, tüm gerekli derleme başvurularını sınıf kitaplığı projesine eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="257bb-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="257bb-149">Menü seçeneği CustomExtenders projeye sağ tıklayıp **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="257bb-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="257bb-150">.NET sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="257bb-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="257bb-151">Aşağıdaki derlemelere başvurular ekleyin:</span><span class="sxs-lookup"><span data-stu-id="257bb-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="257bb-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="257bb-152">System.Web.dll</span></span>
    2. <span data-ttu-id="257bb-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="257bb-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="257bb-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="257bb-154">System.Design.dll</span></span>
    4. <span data-ttu-id="257bb-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="257bb-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="257bb-156">Gözat sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="257bb-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="257bb-157">AjaxControlToolkit.dll derlemesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="257bb-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="257bb-158">Başvuruluyor AJAX Denetim Araç Seti indirdiğiniz klasörde bulunur.</span><span class="sxs-lookup"><span data-stu-id="257bb-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="257bb-159">Bu adımları tamamladıktan sonra sınıf kitaplığı proje başvuruları klasörü Şekil 2'gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="257bb-159">After you complete these steps, your class library project References folder should look like Figure 2.</span></span>


<span data-ttu-id="257bb-160">[![Gerekli başvuruları olan başvuruları klasörü](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span></span>

<span data-ttu-id="257bb-161">**Şekil 02**: Gerekli başvuruları olan başvuruları klasörü ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span></span>


## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="257bb-162">Özel denetim Genişleticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="257bb-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="257bb-163">Sınıf kitaplığımızı sahibiz, biz bizim genişletici denetimi oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257bb-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="257bb-164">Bir özel genişletici denetimi sınıfın (1 listeleme bakın) ile tam kemikleri Başlat s olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="257bb-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="257bb-165">**1 - MyCustomExtender.cs listeleme**</span><span class="sxs-lookup"><span data-stu-id="257bb-165">**Listing 1 - MyCustomExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

<span data-ttu-id="257bb-166">Listeleme 1'deki denetim genişletici sınıfı hakkında dikkat edin birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="257bb-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="257bb-167">İlk olarak, sınıfın temel ExtenderControlBase sınıfından devralan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="257bb-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="257bb-168">Tüm AJAX Denetim Araç Seti genişletici denetimleri, bu temel sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="257bb-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="257bb-169">Örneğin, temel sınıfın her denetim genişletici gerekli bir özelliktir TargetID özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="257bb-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="257bb-170">Ardından, sınıfın istemci komut dosyası için ilgili aşağıdaki iki öznitelik eklediğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="257bb-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="257bb-171">Bir derlemede gömülü olan bir kaynak olarak eklenmek üzere bir dosya WebResource - neden olur.</span><span class="sxs-lookup"><span data-stu-id="257bb-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="257bb-172">ClientScriptResource - bir derlemeden alınacak bir betik kaynak neden olur.</span><span class="sxs-lookup"><span data-stu-id="257bb-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="257bb-173">WebResource özniteliği özel genişletici derlendiğinde MyControlBehavior.js JavaScript dosyasını derlemesine gömmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="257bb-174">ClientScriptResource öznitelik, bir web sayfasında özel genişletici kullanıldığında derlemeden MyControlBehavior.js betiği almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>


<span data-ttu-id="257bb-175">Sırayla çalışması Web kaynağı ve ClientScriptResource öznitelikler için JavaScript dosyası katıştırılmış bir kaynağı derlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="257bb-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="257bb-176">Çözüm Gezgini penceresinde dosyayı seçin, özellik sayfasını açın ve değer atamak *gömülü kaynak* için **derleme eylemi** özelliği.</span><span class="sxs-lookup"><span data-stu-id="257bb-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>


<span data-ttu-id="257bb-177">Denetim genişletici TargetControlType özniteliği eklediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="257bb-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="257bb-178">Bu öznitelik tarafından denetim genişletici genişletilmiş denetim türünü belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="257bb-179">Listeleme 1 olması durumunda, Denetim genişletici TextBox genişletmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="257bb-180">Son olarak, özel genişletici MyProperty adlı bir özellik eklediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="257bb-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="257bb-181">Özellik ExtenderControlProperty özniteliği ile işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="257bb-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="257bb-182">GetPropertyValue() ve SetPropertyValue() yöntemleri, özellik değeri, istemci tarafı davranışı için sunucu taraflı denetim genişletici geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="257bb-183">Devam edip bizim DisabledButton genişletici kodunu uygulamak s olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="257bb-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="257bb-184">Bu genişletici için kod listeleme 2'de bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="257bb-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="257bb-185">**2 - DisabledButtonExtender.cs listeleme**</span><span class="sxs-lookup"><span data-stu-id="257bb-185">**Listing 2 - DisabledButtonExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

<span data-ttu-id="257bb-186">Listeleme 2 DisabledButton genişletici TargetButtonID ve DisabledText adlı iki özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="257bb-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="257bb-187">TargetButtonID özelliğine uygulanan IDReferenceProperty düğme denetiminin kimliği dışında her şey bu özelliğine atama engeller.</span><span class="sxs-lookup"><span data-stu-id="257bb-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="257bb-188">WebResource ve ClientScriptResource öznitelikleri ile bu genişletici DisabledButtonBehavior.js adlı bir dosyada bulunan bir istemci-tarafı davranışı ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="257bb-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="257bb-189">Bu JavaScript dosyası sonraki bölümde ele alır.</span><span class="sxs-lookup"><span data-stu-id="257bb-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="257bb-190">Özel genişletici davranışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="257bb-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="257bb-191">Bir denetim genişletici istemci-tarafı bileşeninin bir davranış olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="257bb-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="257bb-192">Devre dışı bırakıp düğmeyi etkinleştirerek fiili mantığı DisabledButton davranışı yer alır.</span><span class="sxs-lookup"><span data-stu-id="257bb-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="257bb-193">JavaScript kod davranışı için listeleme 3'te eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="257bb-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="257bb-194">**3 - DisabledButton.js listeleme**</span><span class="sxs-lookup"><span data-stu-id="257bb-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

<span data-ttu-id="257bb-195">Listeleme 3 JavaScript dosyasında DisabledButtonBehavior adlı bir istemci-tarafı sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="257bb-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="257bb-196">Sunucu tarafı ikizi gibi bu sınıf TargetButtonID adlı iki özellik içerir ve kullanarak erişebileceğiniz DisabledText alma\_TargetButtonID/set\_TargetButtonID ve\_DisabledText/set\_ DisabledText.</span><span class="sxs-lookup"><span data-stu-id="257bb-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="257bb-197">Initialize() yöntemi olay işleyici keyup davranışı için hedef öğe ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="257bb-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="257bb-198">Her zaman bir harf bu davranışı ile ilişkili metin kutusuna yazdığınız işleyici keyup yürütür.</span><span class="sxs-lookup"><span data-stu-id="257bb-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="257bb-199">İşleyici keyup etkinleştirir veya davranışla ilişkili metin herhangi bir metin içerip içermediğini bağlı olarak düğmesini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="257bb-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="257bb-200">JavaScript dosyası katıştırılmış bir kaynağı olarak listeleme 3'te derlemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="257bb-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="257bb-201">Çözüm Gezgini penceresinde dosyayı seçin, özellik sayfasını açın ve değer atamak *gömülü kaynak* için **derleme eylemi** özelliği (bkz: Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="257bb-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="257bb-202">Bu seçenek, hem Visual Studio ve Visual Web Developer kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="257bb-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>


<span data-ttu-id="257bb-203">[![Bir JavaScript dosyası katıştırılmış bir kaynağı ekleme](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span></span>

<span data-ttu-id="257bb-204">**Şekil 03**: Bir JavaScript dosyası katıştırılmış bir kaynağı ekleme ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span></span>


## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="257bb-205">Özel genişletici Tasarımcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="257bb-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="257bb-206">Bizim genişletici tamamlanması oluşturmak için gereken son bir sınıf yoktur.</span><span class="sxs-lookup"><span data-stu-id="257bb-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="257bb-207">Biz listeleme 4'te Tasarımcı sınıfını oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="257bb-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="257bb-208">Bu sınıf, Visual Studio/Visual Web Developer Tasarımcısı ile doğru şekilde davranmaz genişletici yapmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="257bb-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="257bb-209">**4 - DisabledButtonDesigner.cs listeleme**</span><span class="sxs-lookup"><span data-stu-id="257bb-209">**Listing 4 - DisabledButtonDesigner.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

<span data-ttu-id="257bb-210">Listeleme 4 tasarımcıda Tasarımcısı özniteliğine sahip DisabledButton genişletici ile ilişkilendirin. Bu DisabledButtonExtender Sınıf Tasarımcısı özniteliği uygulamak yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="257bb-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="257bb-211">Özel genişletici kullanma</span><span class="sxs-lookup"><span data-stu-id="257bb-211">Using the Custom Extender</span></span>

<span data-ttu-id="257bb-212">Biz DisabledButton denetim Genişleticisi oluşturma tamamladınız, ASP.NET sitemizin kullanılacak zaman var.</span><span class="sxs-lookup"><span data-stu-id="257bb-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="257bb-213">İlk olarak biz özel genişletici araç kutusuna eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="257bb-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="257bb-214">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="257bb-214">Follow these steps:</span></span>

1. <span data-ttu-id="257bb-215">Çözüm Gezgini penceresinde sayfanın çift tıklayarak bir ASP.NET sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="257bb-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="257bb-216">Araç kutusunu sağ tıklatın ve menü seçeneğini **öğelerini Seç**.</span><span class="sxs-lookup"><span data-stu-id="257bb-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="257bb-217">Araç kutusu öğelerini Seç iletişim kutusunda CustomExtenders.dll derlemeye göz atın.</span><span class="sxs-lookup"><span data-stu-id="257bb-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="257bb-218">Tıklayın **Tamam** iletişim kutusunu kapatmak için düğme.</span><span class="sxs-lookup"><span data-stu-id="257bb-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="257bb-219">Bu adımları tamamladıktan sonra DisabledButton denetim genişletici araç kutusunda görünmesi gerekir (bkz: Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="257bb-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>


<span data-ttu-id="257bb-220">[![Araç kutusunda DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span></span>

<span data-ttu-id="257bb-221">**Şekil 04**: Araç kutusunda DisabledButton ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span></span>


<span data-ttu-id="257bb-222">Ardından, size yeni bir ASP.NET sayfası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="257bb-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="257bb-223">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="257bb-223">Follow these steps:</span></span>

1. <span data-ttu-id="257bb-224">ShowDisabledButton.aspx adlı yeni bir ASP.NET sayfası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="257bb-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="257bb-225">Bir ScriptManager sayfaya sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="257bb-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="257bb-226">TextBox denetimi sayfaya sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="257bb-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="257bb-227">Bir düğme denetimi sayfaya sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="257bb-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="257bb-228">Özellikler penceresinde düğmesi ID özelliği değere değiştirin <em>btnSave</em> ve metin özelliğini değerini *Kaydet\**.</span><span class="sxs-lookup"><span data-stu-id="257bb-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>
  

<span data-ttu-id="257bb-229">Bir standart ASP.NET metin kutusu ve düğme denetimi ile bir sayfa oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="257bb-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="257bb-230">Ardından, biz TextBox denetimi DisabledButton genişletici ile genişletin gerekir:</span><span class="sxs-lookup"><span data-stu-id="257bb-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="257bb-231">Seçin **ekleme genişletici** görev seçeneği genişletici Sihirbazı iletişim kutusu açmak için (bkz: Şekil 5).</span><span class="sxs-lookup"><span data-stu-id="257bb-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="257bb-232">İletişim kutusu özel bizim DisabledButton genişletici içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="257bb-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="257bb-233">DisabledButton genişletici seçip tıklayın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="257bb-233">Select the DisabledButton extender and click the **OK** button.</span></span>


<span data-ttu-id="257bb-234">[![Genişletici Sihirbazı iletişim kutusu](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span></span>

<span data-ttu-id="257bb-235">**Şekil 05**: Genişletici Sihirbazı iletişim kutusu ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span></span>


<span data-ttu-id="257bb-236">Son olarak, biz DisabledButton genişletici özelliklerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257bb-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="257bb-237">TextBox denetimi özelliklerini değiştirerek DisabledButton genişletici özelliklerini değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="257bb-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="257bb-238">Tasarımcıda seçin.</span><span class="sxs-lookup"><span data-stu-id="257bb-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="257bb-239">Özellikler penceresinde Genişleticileri düğümünü genişletin (bkz. Şekil 6).</span><span class="sxs-lookup"><span data-stu-id="257bb-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="257bb-240">Değer atamak *Kaydet* DisabledText özelliği ve değerini *btnSave* TargetButtonID özelliğine.</span><span class="sxs-lookup"><span data-stu-id="257bb-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>


<span data-ttu-id="257bb-241">[![Genişletici özelliklerini ayarlama](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span></span>

<span data-ttu-id="257bb-242">**Şekil 06**: Genişletici özellikleri ayarlama ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span></span>


<span data-ttu-id="257bb-243">Sayfa çalıştırdığınızda (F5 tuşlarına basarak) düğme denetimini başlangıçta devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="257bb-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="257bb-244">Aşağıdaki metin kutusuna metin girerek başlamadan hemen sonra (bkz. Şekil 7) denetim düğmesi etkin.</span><span class="sxs-lookup"><span data-stu-id="257bb-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>


<span data-ttu-id="257bb-245">[![Uygulamada DisabledButton genişletici](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="257bb-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span></span>

<span data-ttu-id="257bb-246">**Şekil 07**: DisabledButton extender uygulamada ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="257bb-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="257bb-247">Özet</span><span class="sxs-lookup"><span data-stu-id="257bb-247">Summary</span></span>

<span data-ttu-id="257bb-248">AJAX Denetim Araç Seti ile özel genişletici denetimleri nasıl genişletebileceğiniz açıklamak için bu öğreticinin amacı oluştu.</span><span class="sxs-lookup"><span data-stu-id="257bb-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="257bb-249">Bu öğreticide, bir basit DisabledButton denetim genişletici oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="257bb-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="257bb-250">DisabledButtonExtender sınıfı DisabledButtonBehavior JavaScript davranışları ve DisabledButtonDesigner sınıfı oluşturarak bu genişletici uyguladık.</span><span class="sxs-lookup"><span data-stu-id="257bb-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="257bb-251">Bir özel denetim genişletici oluşturduğunuzda bir dizi benzer adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="257bb-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="257bb-252">[Önceki](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [İleri](get-started-with-the-ajax-control-toolkit-vb.md)</span><span class="sxs-lookup"><span data-stu-id="257bb-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
[Next](get-started-with-the-ajax-control-toolkit-vb.md)</span></span>
