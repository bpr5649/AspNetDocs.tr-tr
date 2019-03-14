---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: (C#) veritabanı ile CascadingDropDown kullanma | Microsoft Docs
author: wenz
description: Bir DropDownList yükleri değişiklikleri anoth değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: ed5057ee942ce57503b038cbd856fefaa3d287ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071409"
---
<a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="72605-103">Veritabanı ile CascadingDropDown Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="72605-103">Using CascadingDropDown with a Database (C#)</span></span>
====================
<span data-ttu-id="72605-104">tarafından [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="72605-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="72605-105">[Kodu indir](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) veya [PDF olarak indirin](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="72605-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="72605-106">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="72605-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="72605-107">Bunun çalışması sırada bir özel web hizmeti oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72605-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="72605-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="72605-108">Overview</span></span>

<span data-ttu-id="72605-109">Bir DropDownList yükleri değişiklikleri başka bir DropDownList değerleri ilişkili böylece AJAX Denetim Araç Seti CascadingDropDown denetiminde bir DropDownList denetimi genişletir.</span><span class="sxs-lookup"><span data-stu-id="72605-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="72605-110">(Örneği için BİZE durumları listesini bir liste sağlar ve sonraki listesi, bu durumda bulunan büyük şehirlerin ile doldurulur.) Bunun çalışması sırada bir özel web hizmeti oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72605-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="72605-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="72605-111">Steps</span></span>

<span data-ttu-id="72605-112">İlk olarak bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="72605-112">First of all, a data source is required.</span></span> <span data-ttu-id="72605-113">Bu örnekte, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="72605-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="72605-114">Veritabanı (express sürüm dahil) bir Visual Studio yüklemesi isteğe bağlı bir parçasıdır ve ayrıca altında ayrı bir indirme olarak kullanılabilir [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="72605-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="72605-115">AdventureWorks veritabanı SQL Server 2005 örnekleri ve örnek veritabanları parçasıdır (adresinden [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="72605-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="72605-116">En kolay yolu, veritabanını ayarlamak için Microsoft SQL Server Management Studio Express kullanmaktır ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = tr](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) ve ekleme `AdventureWorks.mdf` veritabanı dosyası.</span><span class="sxs-lookup"><span data-stu-id="72605-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="72605-117">Bu örnek için SQL Server 2005 Express Edition örneğini çağrıldığından emin olan varsayıyoruz `SQLEXPRESS` ve web sunucusu; ile aynı makinede bulunan varsayılan kurulumu da budur.</span><span class="sxs-lookup"><span data-stu-id="72605-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="72605-118">Kurulumunuzu farklıysa, veritabanı için bağlantı bilgilerini uymak zorunda.</span><span class="sxs-lookup"><span data-stu-id="72605-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="72605-119">ASP.NET AJAX Denetim Araç Seti ve işlevlerini etkinleştirmek için `ScriptManager` denetim gerekir yerleştirmek herhangi bir sayfada (ancak içinde &lt; `form` &gt; öğesi):</span><span class="sxs-lookup"><span data-stu-id="72605-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="72605-120">Sonraki adımda, iki DropDownList denetimi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="72605-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="72605-121">Bu örnekte, AdventureWorks satıcı ve ilgili kişi bilgileri kullanırız, bu nedenle bir liste kullanılabilir satıcılar, biri kullanılabilir kişi oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="72605-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="72605-122">Ardından, iki CascadingDropDown Genişleticileri sayfaya eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="72605-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="72605-123">Bir ilk (Satıcılar) listesini doldurur ve diğeri ikinci (kişi) listesi girer.</span><span class="sxs-lookup"><span data-stu-id="72605-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="72605-124">Aşağıdaki öznitelikler ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="72605-124">The following attributes must be set:</span></span>

- <span data-ttu-id="72605-125">`ServicePath`: Liste girişlerini sunan bir web hizmeti URL'si</span><span class="sxs-lookup"><span data-stu-id="72605-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="72605-126">`ServiceMethod`: Liste girişlerini sunan web yöntemi</span><span class="sxs-lookup"><span data-stu-id="72605-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="72605-127">`TargetControlID`: Aşağı açılan liste kimliği</span><span class="sxs-lookup"><span data-stu-id="72605-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="72605-128">`Category`: Web yöntemi çağrıldığında gönderilen kategori bilgileri</span><span class="sxs-lookup"><span data-stu-id="72605-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="72605-129">`PromptText`: Zaman uyumsuz olarak sunucudan liste verilerini yüklerken görüntülenecek metin</span><span class="sxs-lookup"><span data-stu-id="72605-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="72605-130">`ParentControlID`: (isteğe bağlı) üst açılır listede, şu anki listenin Tetikleyicileri yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="72605-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="72605-131">Kullanılan programlama diline bağlı olarak söz konusu web hizmeti adını değiştirir, ancak diğer öznitelik değerleri aynıdır.</span><span class="sxs-lookup"><span data-stu-id="72605-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="72605-132">CascadingDropDown öğe için ilk açılan listede aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="72605-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="72605-133">İkinci liste için Denetim genişleticilerini gerekir `ParentControlID` yükleniyor satıcıları listesi Tetikleyicileri girişi seçerek ilişkili kişiler listesi öğeleri, öznitelik.</span><span class="sxs-lookup"><span data-stu-id="72605-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="72605-134">Asıl işi, ardından aşağıdaki ayarlamaları yapın web hizmetinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="72605-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="72605-135">Unutmayın `[ScriptService]` özniteliği kullanılır, aksi takdirde, ASP.NET AJAX istemci tarafı komut dosyası kodunu web yöntemlere erişmek için JavaScript proxy'si oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="72605-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="72605-136">CascadingDropDown tarafından çağrılan web yöntemler imzası aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="72605-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="72605-137">Dönüş değeri bir dizi türünde olmalıdır, böylece `CascadingDropDownNameValue` Denetim Araç Seti tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="72605-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="72605-138">`GetVendors()` Yöntemi uygulamak oldukça kolaydır: Kod, AdventureWorks veritabanına bağlanır ve ilk 25 satıcıları sorgular.</span><span class="sxs-lookup"><span data-stu-id="72605-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="72605-139">İlk parametre `CascadingDropDownNameValue` Oluşturucusu değerini başlıktır ikinci bir liste girdisi (öznitelik HTML'nin &lt; `option` &gt; öğesi).</span><span class="sxs-lookup"><span data-stu-id="72605-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="72605-140">Kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="72605-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="72605-141">İlişkili kişiler için satıcı alma (yöntem adı: `GetContactsForVendor()`) biraz zor olduğu.</span><span class="sxs-lookup"><span data-stu-id="72605-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="72605-142">İlk olarak, ilk açılan listede seçili satıcı belirlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="72605-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="72605-143">Denetim Araç Seti, bu görev için bir yardımcı yöntem tanımlar: `ParseKnownCategoryValuesString()` Yöntemi döndürür bir `StringDictionary` açılan verilerle öğesi:</span><span class="sxs-lookup"><span data-stu-id="72605-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="72605-144">Güvenlik nedeniyle, bu verileri önce doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72605-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="72605-145">Bir satıcı girişi varsa bunu (çünkü `Category` özelliği ilk CascadingDropDown öğenin `"Vendor"`), seçili satıcı kimliği alınabilir:</span><span class="sxs-lookup"><span data-stu-id="72605-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="72605-146">Yöntemin geri kalanını oldukça rahatça, ise.</span><span class="sxs-lookup"><span data-stu-id="72605-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="72605-147">Satıcı Kimliği bir parametre olarak, tüm ilişkili kişiler için satıcıya alır bir SQL sorgusu için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="72605-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="72605-148">Bir kez daha, yöntem türünde bir dizi döndürür `CascadingDropDownNameValue`.</span><span class="sxs-lookup"><span data-stu-id="72605-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="72605-149">ASP.NET sayfasını yüklemek ve kısa bir süre sonra satıcı listesini 25 girişleri ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="72605-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="72605-150">Bir girişi seçin ve açılır listeden ikinci veri ile doldurulan nasıl dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="72605-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="72605-151">[![İlk liste otomatik olarak doldurulur.](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="72605-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="72605-152">İlk liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görmek için tıklatın](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="72605-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


<span data-ttu-id="72605-153">[![İkinci liste ilk listede seçime göre doldurulur.](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="72605-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="72605-154">İkinci liste ilk listede seçime göre doldurulur ([tam boyutlu görüntüyü görmek için tıklatın](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="72605-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="72605-155">[Önceki](filling-a-list-using-cascadingdropdown-cs.md)
> [İleri](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="72605-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
