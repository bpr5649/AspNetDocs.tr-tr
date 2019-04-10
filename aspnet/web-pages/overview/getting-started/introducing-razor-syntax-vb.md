---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: ASP.NET Web programlama Razor söz dizimini (Visual Basic) kullanarak giriş | Microsoft Docs
author: Rick-Anderson
description: Bu ekte Razor sözdizimini kullanarak Visual Basic'te, ASP.NET Web sayfaları ile programlamaya genel bir bakış sağlar.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: e6b63afb9492e810e19999c7c7ffe074ad510bda
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406775"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="1cf10-103">ASP.NET Web programlama Razor söz dizimini (Visual Basic) kullanarak giriş</span><span class="sxs-lookup"><span data-stu-id="1cf10-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="1cf10-104">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1cf10-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1cf10-105">Bu makalede Razor sözdizimi ve Visual Basic kullanarak ASP.NET Web sayfaları ile programlamaya genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="1cf10-106">ASP.NET dinamik web sayfaları web sunucuları üzerinde çalışan için Microsoft'un teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="1cf10-107">**Öğrenecekleriniz**:</span><span class="sxs-lookup"><span data-stu-id="1cf10-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="1cf10-108">Programlama ipuçları, Razor sözdizimini kullanan ASP.NET Web sayfaları programlama ile Başlarken üst 8.</span><span class="sxs-lookup"><span data-stu-id="1cf10-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="1cf10-109">Temel programlama kavramlarını ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="1cf10-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="1cf10-110">ASP.NET sunucusu kod ve Razor sözdizimi olan tüm hakkında.</span><span class="sxs-lookup"><span data-stu-id="1cf10-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="1cf10-111">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="1cf10-112">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1cf10-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1cf10-113">Bu öğreticide, ASP.NET Web Pages 2 ile de çalışır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="1cf10-114">Razor sözdizimi olan ASP.NET Web Pages kullanılarak çoğu örnekler C# kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="1cf10-115">Ancak, Razor sözdizimi Visual Basic de destekler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="1cf10-116">Program Visual Basic'te bir ASP.NET web sayfası için bir web sayfası oluşturun. bir *.vbhtml* dosya adı uzantısı ve Visual Basic kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="1cf10-117">Bu makalede, ASP.NET Web sayfaları oluşturmak için sözdizimi ve Visual Basic dili ile çalışmaya genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="1cf10-118">Microsoft WebMatrix için varsayılan Web sitesi şablonları (**Pastane**, **Fotoğraf Galerisi**, ve **başlangıç sitesi**, vb.) C# ve Visual Basic sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="1cf10-119">Visual Basic şablonları tarafından NuGet paketleri olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="1cf10-120">Adlı bir klasörde, sitenizin kök klasöründe yüklü Web sitesi şablonları *Microsoft Templates*.</span><span class="sxs-lookup"><span data-stu-id="1cf10-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="1cf10-121">Üst 8 programlama ipuçları</span><span class="sxs-lookup"><span data-stu-id="1cf10-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="1cf10-122">Bu bölümde kesinlikle Razor sözdizimini kullanan ASP.NET sunucusu kod yazmaya başladığınızda bilmeniz gereken birkaç ipucu listelenir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="1cf10-123">1. Kod kullanarak bir sayfa ekleyin @ karakteri</span><span class="sxs-lookup"><span data-stu-id="1cf10-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="1cf10-124">`@` Karakter satır içi ifadeler, tek deyim blokları ve birden fazla deyim blokları başlatır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="1cf10-125">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="1cf10-127">HTML kodlama</span><span class="sxs-lookup"><span data-stu-id="1cf10-127">HTML Encoding</span></span>**
> 
> <span data-ttu-id="1cf10-128">Kullanarak bir sayfanın içeriğini görüntülediğinizde `@` karakter, önceki örneklerde olduğu gibi çıkış ASP.NET HTML olarak kodlar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="1cf10-129">Bu ayrılmış HTML karakterlerini değiştirir (gibi `<` ve `>` ve `&`) karakterlerini HTML etiketleri veya varlıklar yorumlanmasını yerine bir web sayfasında karakter olarak görüntülenecek etkinleştirme kodları ile.</span><span class="sxs-lookup"><span data-stu-id="1cf10-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="1cf10-130">Sunucu kodunuz çıktısını HTML kodlaması olmadan düzgün görüntülenmeyebilir ve bir sayfa güvenlik risklerine maruz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="1cf10-131">Amacınız etiketlerini işler biçimlendirmesi olarak HTML biçimlendirmesi çıkış olup olmadığını (örneğin `<p></p>` paragrafı veya `<em></em>` metni vurgulamak için), bölümüne bakın [metin birleştirme, işaretleme ve kod blokları içinde kod](#BM_CombiningTextMarkupAndCode) bu makalenin ilerleyen bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="1cf10-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="1cf10-132">Daha fazla bilgi edinebilirsiniz, HTML kodlaması hakkında [ASP.NET Web sayfaları sitelerinde HTML formlarla çalışma](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="1cf10-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="1cf10-133">2. Kod ile kod blokları içine aldığınız... Bitiş kodu</span><span class="sxs-lookup"><span data-stu-id="1cf10-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="1cf10-134">Bir kod bloğu bir veya daha fazla kod deyimlerini içerir ve anahtar sözcüklerle içine `Code` ve `End Code`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="1cf10-135">Açılış yerleştirin `Code` anahtar sözcüğü hemen sonra `@` karakter &#8212; olamaz boşluk bunlar arasında.</span><span class="sxs-lookup"><span data-stu-id="1cf10-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="1cf10-136">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-136">The result displayed in a browser:</span></span>

![Razor Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="1cf10-138">3. Bir blok içinde her kod açıklaması satır sonu ile bitmelidir</span><span class="sxs-lookup"><span data-stu-id="1cf10-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="1cf10-139">Bir Visual Basic kod bloğu içinde her deyim bir satır sonu ile sona erer.</span><span class="sxs-lookup"><span data-stu-id="1cf10-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="1cf10-140">(Makalenin sonraki bölümlerinde gerekirse uzun kod deyimi birden fazla satır içine sarmak için bir yol görürsünüz.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="1cf10-141">4. Değerleri depolamak için değişkenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="1cf10-141">4. You use variables to store values</span></span>

<span data-ttu-id="1cf10-142">Değerleri depolayabilir bir *değişkeni*dizeler, sayılar ve tarihler, vb. dahil olmak üzere. Bir değişken kullanarak yeni oluşturduğunuz `Dim` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="1cf10-143">Değişken değerleri doğrudan bir sayfasını kullanarak içinde ekleyebilirsiniz `@`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="1cf10-144">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="1cf10-146">5. Değişmez değer dize değerleri çift tırnak içine alın</span><span class="sxs-lookup"><span data-stu-id="1cf10-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="1cf10-147">A *dize* metin olarak kabul edilir karakterden oluşan bir dizidir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="1cf10-148">Bir dizeyi belirtmek için çift tırnak içine alın:</span><span class="sxs-lookup"><span data-stu-id="1cf10-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="1cf10-149">Bir dize değeri çift tırnak işaretleri eklemek için iki çift tırnak işareti karakteri Ekle.</span><span class="sxs-lookup"><span data-stu-id="1cf10-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="1cf10-150">Çift tırnak karakteri sayfa çıktısında görünmesi istiyorsanız olarak girin `""` tırnak içindeki dize ve iki kez görünmesini istiyorsanız olarak girin `""""` alıntılanmış dize içinde.</span><span class="sxs-lookup"><span data-stu-id="1cf10-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="1cf10-151">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-151">The result displayed in a browser:</span></span>

![Razor Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="1cf10-153">6. Visual Basic kodunu büyük küçük harfe duyarlı değil</span><span class="sxs-lookup"><span data-stu-id="1cf10-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="1cf10-154">Visual Basic dili büyük/küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="1cf10-155">Programlama anahtar sözcükleri (gibi `Dim`, `If`, ve `True`) ve değişken adları (gibi `myString`, veya `subTotal`) her durumda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="1cf10-156">Aşağıdaki kod satırlarını değişkene bir değer atamak `lastname` bir küçük harf kullanarak adlandırın ve ardından değişken değeri için büyük bir adı kullanarak sayfayı çıktı.</span><span class="sxs-lookup"><span data-stu-id="1cf10-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="1cf10-157">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="1cf10-159">7. Nesneler ile çalışma kodlamanızı çoğunu içerir</span><span class="sxs-lookup"><span data-stu-id="1cf10-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="1cf10-160">Bir nesne ile programlayabileceğiniz bir şeyi temsil eder &#8212; bir sayfa, bir metin kutusu, bir dosya, görüntü, bir web isteği, bir e-posta iletisi, bir müşteri kaydı (veritabanı satır) vb. Nesnelerin özelliklerini tanımlayan özellikleri vardır &#8212; bir metin kutusu nesnesine sahip bir `Text` bir istek nesnesi özelliğine sahip bir `Url` özelliğine sahip bir e-posta iletisi bir `From` özelliği ve müşteri nesnesi olan bir `FirstName` özellik.</span><span class="sxs-lookup"><span data-stu-id="1cf10-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="1cf10-161">Nesneleri yöntemlerle de &quot;fiilleri&quot; yerine getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="1cf10-162">Örnekler, bir dosya nesnesinin `Save` yöntemi, bir görüntü nesnenin `Rotate` yöntemi ve bir e-posta nesnenin `Send` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="1cf10-163">Genellikle ile çalışacaksınız `Request` ne tür bir tarayıcı, sayfa, kullanıcı kimliği, vb. URL'sini istekte (metin kutuları, vb.) sayfasında alanları form değerleri gibi bilgileri sağlayan nesne. Bu örnek özelliklerine erişmek nasıl gösterir `Request` nesne ve nasıl çağrılacağını `MapPath` yöntemi `Request` sayfasının mutlak yolu sunucu üzerinde size nesnesi:</span><span class="sxs-lookup"><span data-stu-id="1cf10-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="1cf10-164">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="1cf10-166">8. Kararları kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="1cf10-167">Bir anahtar dinamik web sayfaları ne koşullara göre yapılacağını belirlemek özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="1cf10-168">Bunu yapmak için en yaygın yolu `If` deyimi (ve isteğe bağlı `Else` deyimi).</span><span class="sxs-lookup"><span data-stu-id="1cf10-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="1cf10-169">Deyim `If IsPost` yazma toplu yoludur `If IsPost = True`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="1cf10-170">İle birlikte `If` deyimleri, bir yineleme kod bloklarını koşulları test için çeşitli yollar vardır ve bu şekilde, bu makalenin sonraki bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="1cf10-171">Bir tarayıcıda görüntülenen sonuç (tıkladıktan sonra **Gönder**):</span><span class="sxs-lookup"><span data-stu-id="1cf10-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="1cf10-173">HTTP GET ve POST yöntemleri ve IsPost özelliği</span><span class="sxs-lookup"><span data-stu-id="1cf10-173">HTTP GET and POST Methods and the IsPost Property</span></span>**
> 
> <span data-ttu-id="1cf10-174">Çok sınırlı bir dizi yöntem (HTTP) Web sayfaları için kullanılan protokol destekler (&quot;fiilleri&quot;) sunucuya isteklerinde bulunmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="1cf10-175">İki en yaygın bir okumak için kullanılan GET ve POST, bir sayfa göndermek için kullanılan olanlardır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="1cf10-176">Genel olarak, ilk kez bir kullanıcı bir sayfa istediğinde, GET kullanarak sayfa istenmektedir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="1cf10-177">Kullanıcının bir formda doldurur daha sonra tıklatırsa **Gönder**, tarayıcı, sunucuya bir POST isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="1cf10-178">Web programlama, böylece sayfa işleme bildiğiniz bir sayfaya bir GET veya POST olarak istenen olup olmadığını bilmek yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="1cf10-179">ASP.NET Web sayfaları'nda kullanabileceğiniz `IsPost` bir GET veya POST isteği olup olmadığını görmek için özellik.</span><span class="sxs-lookup"><span data-stu-id="1cf10-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="1cf10-180">Bir POST isteğiyse `IsPost` özelliği true döndürür ve bir form üzerinde metin kutuları değerlerini okuma gibi şeyler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="1cf10-181">Birçok örnekler göreceksiniz sayfanın değerine bağlı olarak farklı şekilde işlemek nasıl Göster `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="1cf10-182">Basit bir kod örneğidir</span><span class="sxs-lookup"><span data-stu-id="1cf10-182">A Simple Code Example</span></span>

<span data-ttu-id="1cf10-183">Bu yordam, temel programlama tekniklerini gösteren bir sayfa oluşturma işlemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="1cf10-184">Örnekte, kullanıcılar bunları ekler ve sonucu görüntüler iki sayıyı girin sağlayan bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cf10-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="1cf10-185">Düzenleyicinizde, yeni bir dosya oluşturun ve adlandırın *AddNumbers.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="1cf10-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="1cf10-186">Aşağıdaki kodu ve biçimlendirmeyi sayfasındaki herhangi bir şey değiştirerek sayfasına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="1cf10-187">Not yapabileceğiniz bazı işlemler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1cf10-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="1cf10-188">`@` Karakter sayfasında ilk kod bloğunu başlar ve kendisinden `totalMessage` değişkeni altına katıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="1cf10-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="1cf10-189">Sayfanın üst kısmındaki blok içine `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="1cf10-190">Değişkenleri `total`, `num1`, `num2`, ve `totalMessage` birkaç sayı ve bir dize depolar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="1cf10-191">Atanan değişmez dize değeri `totalMessage` çift tırnak işareti bulunan bir değişkendir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="1cf10-192">Visual Basic kod zaman büyük/küçük harfe duyarlı olmadığı için `totalMessage` değişkeni sayfanın altına kullanılıyor, adı yalnızca sayfanın üstündeki değişken bildirimi yazımını ile eşleşmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="1cf10-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="1cf10-193">Büyük/küçük harf önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="1cf10-194">İfade `num1.AsInt()`  +  `num2.AsInt()` nesneleri ve yöntemleri ile çalışma hakkında bilgi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="1cf10-195">`AsInt` Yöntemi her bir değişken üzerinde eklenebilecek tamsayı (tamsayı) bir kullanıcı tarafından girilen bir dize dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="1cf10-196">`<form>` Etiket içeren bir `method="post"` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="1cf10-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="1cf10-197">Kullanıcı tıkladığında bu belirten **Ekle**, sayfanın HTTP POST yöntemini kullanarak sunucuya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="1cf10-198">Ne zaman sayfa gönderildiğinde, kodu `If IsPost` true ve koşullu değerlendirir kod çalıştırır, sayıları eklemenin sonucunu görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="1cf10-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="1cf10-199">Sayfayı kaydedin ve bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="1cf10-200">(Emin sayfanın içinde seçili **dosyaları** çalıştırmadan önce çalışma alanı.) İki tam sayılar girin ve ardından **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="1cf10-202">Visual Basic Dil ve sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1cf10-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="1cf10-203">Daha önce bir temel örnek, bir ASP.NET web sayfası oluşturmak nasıl ve sunucu kodunu HTML biçimlendirmesi nasıl ekleyebileceğinizi gördünüz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="1cf10-204">Burada, Razor sözdizimini kullanan ASP.NET sunucusu kod yazmak için Visual Basic kullanmanın temellerini öğreneceksiniz &#8212; diğer bir deyişle, programlama dili kuralları.</span><span class="sxs-lookup"><span data-stu-id="1cf10-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="1cf10-205">(Özellikle, C, C++, C#, Visual Basic veya JavaScript kullandıysanız) programlama deneyimli değilseniz ne burada okuma çoğunu tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="1cf10-206">Yalnızca nasıl WebMatrix kod biçimlendirme içinde eklenen ile kendinizi alıştırın gerekecektir *.vbhtml* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1cf10-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="1cf10-207">Metni İşaretleme ve kod blokları içinde kod birleştirme</span><span class="sxs-lookup"><span data-stu-id="1cf10-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="1cf10-208">Sunucu kod bloklarında genellikle metin ve biçimlendirme sayfasına çıkış isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="1cf10-209">Sunucusu kod bloğu kod değil ve, bunun yerine olarak işleneceğini metin içeriyorsa, ASP.NET koddan metni ayırt etmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="1cf10-210">Bunu yapmanın birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-210">There are several ways to do this.</span></span>

- <span data-ttu-id="1cf10-211">Bir HTML blok öğede gibi metin içine `<p></p>` veya `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="1cf10-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="1cf10-212">HTML öğesi, metin ve ek HTML öğelerinin sunucu kodu ifadeleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="1cf10-213">ASP.NET, HTML etiketi açılışı gördüğünde (örneğin, `<p>`), her şeyi öğesi işler ve içeriği olarak olan tarayıcı (ve çözümler sunucu kodu ifadeler).</span><span class="sxs-lookup"><span data-stu-id="1cf10-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="1cf10-214">Kullanım `@:` işleci veya `<text>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="1cf10-215">`@:` Tek satırlık bir düz metin veya HTML etiketleri eşleşmeyen; içeren içerik çıkarır `<text>` öğesi çıktısını almak için birden fazla satır alır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="1cf10-216">Bu seçenekler, çıkış bir parçası olarak bir HTML öğesini işlemek istemediğiniz zaman yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="1cf10-217">Aşağıdaki örnek, önceki örnekte yineler ancak tek bir çift kullanan `<text>` metin işlemek için etiketler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="1cf10-218">Aşağıdaki örnekte, `<text>` ve `</text>` etiketlerini bazı uncontained metin ve eşleşmeyen HTML etiketleri olması her biri üç satır içine (`<br />`), yanı sıra sunucu kodu ve eşleşen HTML etiketleri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="1cf10-219">Yine de her satırın tek tek önünde `@:` işleci; her iki şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="1cf10-220">Ne zaman, çıktı metin bu bölümde gösterildiği &#8212; bir HTML öğesini kullanarak `@:` işleci veya `<text>` öğesi &#8212; ASP.NET olmayan HTML olarak kodlanacak çıktı.</span><span class="sxs-lookup"><span data-stu-id="1cf10-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="1cf10-221">(Daha önce belirtildiği gibi ASP.NET sunucusu kod ifadeleri tarafından öncelenen sunucusu kod bloğu ve çıkış kodlama `@`, bu bölümde belirtilen özel durumlar hariç.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="1cf10-222">Boşluk</span><span class="sxs-lookup"><span data-stu-id="1cf10-222">Whitespace</span></span>

<span data-ttu-id="1cf10-223">Fazladan boşlukları deyimindeki (ve bir dize sabit değeri dışındaki) deyim etkilemez:</span><span class="sxs-lookup"><span data-stu-id="1cf10-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="1cf10-224">Uzun deyimlerin birkaç satıra yeni</span><span class="sxs-lookup"><span data-stu-id="1cf10-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="1cf10-225">Alt çizgi karakterini kullanarak uzun kod açıklaması birden fazla satıra bölebilir `_` (Visual Basic'te adlandırılan *devamı karakteri*) her kod satırının sonra.</span><span class="sxs-lookup"><span data-stu-id="1cf10-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="1cf10-226">Break sonraki satırdaki bir deyimi satırın sonunda boşluk ve devamı karakteri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="1cf10-227">İfade sonraki satırda devam edin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-227">Continue the statement on the next line.</span></span> <span data-ttu-id="1cf10-228">Deyimleri okunabilirliği artırmak gerektiği kadar satırlarına sarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="1cf10-229">Aşağıdaki deyimler aynıdır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="1cf10-230">Ancak, bir dize sabit değeri ortasında bir satır kaydırma olamaz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="1cf10-231">Aşağıdaki örnek çalışmaz:</span><span class="sxs-lookup"><span data-stu-id="1cf10-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="1cf10-232">Yukarıdaki kodu gibi çoklu satırlara sarar uzun bir dize birleştirmek için kullanmanız gerekecektir *birleştirme işlecini* (`&`), bu makalenin sonraki bölümlerinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="1cf10-233">Kod açıklamaları</span><span class="sxs-lookup"><span data-stu-id="1cf10-233">Code comments</span></span>

<span data-ttu-id="1cf10-234">Açıklama notları kendiniz veya başkaları için terk etmenize imkan.</span><span class="sxs-lookup"><span data-stu-id="1cf10-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="1cf10-235">Razor söz dizimi açıklamaları önekiyle `@*` ve ile sona erdi `*@`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="1cf10-236">Kod blokları içinde Razor söz dizimi açıklamaları kullanabilirsiniz ya da tek bir teklif olan normal Visual Basic açıklama karakter kullanabilirsiniz (`'`) her satır için önek.</span><span class="sxs-lookup"><span data-stu-id="1cf10-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="1cf10-237">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1cf10-237">Variables</span></span>

<span data-ttu-id="1cf10-238">Bir değişken verilerini depolamak için kullandığınız adlandırılmış bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="1cf10-239">Herhangi bir şey değişkenleri ad verebilirsiniz ancak adı, alfabetik bir karakter ile başlamalı ve boşluk ya da ayrılmış karakterler içeremez.</span><span class="sxs-lookup"><span data-stu-id="1cf10-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="1cf10-240">Visual Basic'te, daha önce gördüğünüz gibi büyük/küçük harf bir değişken adı önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="1cf10-241">Değişkenleri ve veri türleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-241">Variables and data types</span></span>

<span data-ttu-id="1cf10-242">Ne tür veriler bir değişkende depolandığını belirtir bir özel veri türü bir değişken olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="1cf10-243">Dize değerleri saklayan string değişkeni olabilir (gibi &quot;Merhaba Dünya&quot;), tam sayı değerleri (örneğin, 3 veya 79) depolayan tamsayı değişkenleri ve çeşitli biçimlerde (4/12/2012 veya 2009 yılı Mart gibi tarih değerlerini depolar tarih değişkenleri ).</span><span class="sxs-lookup"><span data-stu-id="1cf10-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="1cf10-244">Ve kullanabileceğiniz diğer birçok veri türleri vardır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="1cf10-245">Ancak, bir değişken için bir tür belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1cf10-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="1cf10-246">Çoğu durumda, ASP.NET, out değişkeni içinde verilerin nasıl kullanıldığı temel tür anlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="1cf10-247">(Bazen bir türünü belirtmeniz gerekir; bunun true olduğu örnekler göreceksiniz.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="1cf10-248">Bir tür belirtmeden bir değişken bildirmek için kullanın `Dim` ayrıca değişken adı (örneğin, `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="1cf10-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="1cf10-249">Bir türle bir değişken bildirmek için kullanın `Dim` değişken adından, artı `As` ve sonra tür adı (örneğin, `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="1cf10-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="1cf10-250">Aşağıdaki örnek, bir web sayfasında değişkenleri kullanan bazı satır içi ifadeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="1cf10-251">Bir tarayıcıda görüntülenen sonuç:</span><span class="sxs-lookup"><span data-stu-id="1cf10-251">The result displayed in a browser:</span></span>

![Razor Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="1cf10-253">Dönüştürme ve veri türleri test etme</span><span class="sxs-lookup"><span data-stu-id="1cf10-253">Converting and testing data types</span></span>

<span data-ttu-id="1cf10-254">ASP.NET genellikle bir veri türü otomatik olarak belirleyebilir, ancak bazen bunu dönüştürülemez.</span><span class="sxs-lookup"><span data-stu-id="1cf10-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="1cf10-255">Bu nedenle, ASP.NET açık bir dönüştürme gerçekleştirerek yardımcı olacak birçok gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="1cf10-256">Bazen türleri dönüştürmek yoksa bile, ne tür verilere, ile çalışabilir engellemediğini test etmek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="1cf10-257">En yaygın bir tamsayı veya tarih gibi bir dizeyi başka bir türe dönüştürmek sahip olduğu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="1cf10-258">Aşağıdaki örnek, bir sayıyı bir dize burada dönüştürmeniz gerekir tipik bir servis talebi gösterir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="1cf10-259">Bir kural olarak, kullanıcı girişini dize olarak size gelir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="1cf10-260">Bir sayı girin kullanıcıdan ve kullanıcı girişi gönderilir ve kodda okuma zaman bir basamak girdikten bile verileri dize biçiminde bile.</span><span class="sxs-lookup"><span data-stu-id="1cf10-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="1cf10-261">Bu nedenle, dizeyi sayıya dönüştürme gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="1cf10-262">Dönüştürmeden değerleri üzerinde aritmetik işlemleri denerseniz, iki dizeyi ASP.NET eklenemiyor çünkü örnekte, şu hata, sonuçları:</span><span class="sxs-lookup"><span data-stu-id="1cf10-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="1cf10-263">Tam sayılar değerlerini dönüştürmek için çağrı `AsInt` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="1cf10-264">Dönüştürme başarılı olursa, sayıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="1cf10-265">Aşağıdaki tablo bazı yaygın dönüştürme ve test yöntemleri değişkenleri listeler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-265">The following table lists some common conversion and test methods for variables.</span></span>


:::row:::
    :::column:::
        <strong>Method</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Example</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        Converts a string that represents a whole number (like &quot;593&quot;) to an integer.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number. (In ASP.NET, a decimal number is more precise than a floating-point number.)
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        Converts a string that represents a date and time value to the ASP.NET `DateTime` type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        Converts any other data type to a string.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::


## <a name="operators"></a><span data-ttu-id="1cf10-266">İşleçler</span><span class="sxs-lookup"><span data-stu-id="1cf10-266">Operators</span></span>

<span data-ttu-id="1cf10-267">Bir anahtar sözcük veya ne tür bir ifadede gerçekleştirilecek komut ASP karakter işlecidir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-267">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="1cf10-268">Visual Basic birçok işleçleri destekler, ancak yalnızca ASP.NET web sayfaları geliştirmeye başlamak için birkaç tanıması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-268">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="1cf10-269">En yaygın işleçleri aşağıdaki tabloda özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-269">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Examples</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        Math operators used in numerical expressions.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Assignment and equality. Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Inequality. Returns `True` if the values are not equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Less than, greater than, less than or equal, and greater than or equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Concatenation, which is used to join strings.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        The increment and decrement operators, which add and subtract 1 (respectively) from a variable.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        Dot. Used to distinguish objects and their properties and methods.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Parentheses. Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Not. Reverses a true value to false and vice versa. Typically used as a shorthand way to test for `False` (that is, for not `True`).
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Logical AND and OR, which are used to link conditions together.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="1cf10-270">Dosya ve klasör yollarında kod ile çalışma</span><span class="sxs-lookup"><span data-stu-id="1cf10-270">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="1cf10-271">Genellikle, kodunuzda dosya ve klasör yolları ile çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="1cf10-271">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="1cf10-272">Geliştirme bilgisayarınızda görünebilir gibi bir Web sitesi için fiziksel klasör yapısı örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-272">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="1cf10-273">URL'leri ve yolları hakkında bazı önemli ayrıntılar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1cf10-273">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="1cf10-274">Bir URL ile birlikte bir etki alanı adı başlar (`http://www.example.com`) veya bir sunucu adı (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="1cf10-274">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="1cf10-275">Bir URL bir ana bilgisayarın fiziksel yola karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-275">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="1cf10-276">Örneğin, `http://myserver` klasörüne karşılık gelebilir *C:\websites\mywebsite* sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="1cf10-276">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="1cf10-277">Sanal yol tam yolunu belirtmeniz gerek kalmadan kod yollarında temsil etmek için toplu özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-277">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="1cf10-278">Bu, etki alanı veya sunucu adı bir URL bölümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-278">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="1cf10-279">Sanal yol kullandığınızda, yolları güncelleştirmek zorunda kalmadan farklı bir etki alanı ya da sunucu kodunuzu taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-279">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="1cf10-280">Farklar anlamanıza yardımcı olması için bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1cf10-280">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="1cf10-281">Tam URL</span><span class="sxs-lookup"><span data-stu-id="1cf10-281">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="1cf10-282">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="1cf10-282">Server name</span></span> | *<span data-ttu-id="1cf10-283">mycompanyserver</span><span class="sxs-lookup"><span data-stu-id="1cf10-283">mycompanyserver</span></span>* |
| <span data-ttu-id="1cf10-284">Sanal yol</span><span class="sxs-lookup"><span data-stu-id="1cf10-284">Virtual path</span></span> | *<span data-ttu-id="1cf10-285">/HumanResources/CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="1cf10-285">/humanresources/CompanyPolicy.htm</span></span>* |
| <span data-ttu-id="1cf10-286">Fiziksel yol</span><span class="sxs-lookup"><span data-stu-id="1cf10-286">Physical path</span></span> | *<span data-ttu-id="1cf10-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="1cf10-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span></span>* |

<span data-ttu-id="1cf10-288">Sanal kök / yalnızca C: aynı kök gibi sürücüdür \.</span><span class="sxs-lookup"><span data-stu-id="1cf10-288">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="1cf10-289">(Sanal klasör yolları her zaman eğik çizgilerin kullanılması.) Sanal yolun bir klasörün, fiziksel klasör olarak aynı ada sahip gerekmez; Bu, bir diğer ad olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-289">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="1cf10-290">(Üretim sunucularında sanal yolu nadiren tam bir fiziksel yol ile eşleşir.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-290">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="1cf10-291">Bazen kod bulunan dosya ve klasörleri ile çalışırken, fiziksel yolunu ve bazen çalıştığınız hangi nesneleri bağlı olarak bir sanal yola başvurusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-291">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="1cf10-292">ASP.NET, size bu araçları dosya ve klasör yolları kod ile çalışmak için: `Server.MapPath` yöntemi ve `~` işleci ve `Href` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-292">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="1cf10-293">Sanal-fiziksel yolları dönüştürme: Server.MapPath yöntemi</span><span class="sxs-lookup"><span data-stu-id="1cf10-293">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="1cf10-294">`Server.MapPath` Yöntemi, bir sanal yol dönüştürür (gibi */default.cshtml*) mutlak bir fiziksel yola (gibi *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="1cf10-294">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="1cf10-295">Tam fiziksel yolunu ihtiyacınız dilediğiniz zaman bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-295">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="1cf10-296">Okunurken ya da bir metin dosyası veya web sunucusunda görüntü dosyası yazma tipik bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-296">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="1cf10-297">Genellikle sitenizi barındırma site sunucuda mutlak fiziksel yolu bilmiyorsanız, bu yöntem, yolun dönüştürebilirsiniz şekilde bildiğiniz — sanal yolu — sunucusu üzerinde karşılık gelen yolu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-297">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="1cf10-298">Sanal yol bir dosya veya klasöre yöntemine geçirmeniz ve fiziksel yolu döndürür:</span><span class="sxs-lookup"><span data-stu-id="1cf10-298">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="1cf10-299">Sanal kök başvuran: ~ işleci ve Href yöntemi</span><span class="sxs-lookup"><span data-stu-id="1cf10-299">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="1cf10-300">İçinde bir *.cshtml* veya *.vbhtml* dosyası, kök sanal yolu kullanarak başvurabilirsiniz `~` işleci.</span><span class="sxs-lookup"><span data-stu-id="1cf10-300">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="1cf10-301">Bu sayfaları bir siteye taşıyabilirsiniz ve içerdikleri diğer sayfalara giden bağlantıları kopmuş olmayacak çünkü çok kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-301">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="1cf10-302">Ayrıca, hiç olmadığı kadar Web sitenizi farklı bir konuma taşımanız durumunda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-302">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="1cf10-303">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-303">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="1cf10-304">Web sitesi ise `http://myserver/myapp`, işte sayfa çalıştığında ASP.NET bu yolların nasıl değerlendirir:</span><span class="sxs-lookup"><span data-stu-id="1cf10-304">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- `myImagesFolder`<span data-ttu-id="1cf10-305">:</span><span class="sxs-lookup"><span data-stu-id="1cf10-305">:</span></span> `http://myserver/myapp/images`
- `myStyleSheet` <span data-ttu-id="1cf10-306">:</span><span class="sxs-lookup"><span data-stu-id="1cf10-306">:</span></span> `http://myserver/myapp/styles/Stylesheet.css`

<span data-ttu-id="1cf10-307">(Bu yolları aslında değişken değerleri olarak göremezsiniz ancak alacağı ne oldukları olan ASP.NET yolları değerlendirir.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-307">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="1cf10-308">Kullanabileceğiniz `~` işleci hem de sunucu kodu (yukarıdaki gibi) bu gibi biçimlendirme içinde:</span><span class="sxs-lookup"><span data-stu-id="1cf10-308">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="1cf10-309">Biçimlendirme içinde kullandığınız `~` yollara görüntü dosyaları, diğer web sayfaları ve CSS dosyaları gibi kaynakları oluşturmak için işleç.</span><span class="sxs-lookup"><span data-stu-id="1cf10-309">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="1cf10-310">Sayfa çalıştığında, ASP.NET (kod ve biçimlendirme) sayfası görünür ve tüm çözümler `~` başvurularını uygun yolu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-310">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="1cf10-311">Koşullu mantık ve döngüler</span><span class="sxs-lookup"><span data-stu-id="1cf10-311">Conditional Logic and Loops</span></span>

<span data-ttu-id="1cf10-312">ASP.NET sunucusu kod koşullar ve bir döngünün çalışan diğer bir deyişle, belirli bir sayıda kod deyimlerini yineler yazma kod göre görevleri gerçekleştirmenize olanak tanıyan).</span><span class="sxs-lookup"><span data-stu-id="1cf10-312">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="1cf10-313">Test koşulları</span><span class="sxs-lookup"><span data-stu-id="1cf10-313">Testing conditions</span></span>

<span data-ttu-id="1cf10-314">Kullandığınız basit bir koşulunu test etmek için `If...Then` döndüren deyimi `True` veya `False` belirttiğiniz bir testi temel alan:</span><span class="sxs-lookup"><span data-stu-id="1cf10-314">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="1cf10-315">`If` Anahtar sözcüğü, bir blok başlatır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-315">The `If` keyword starts a block.</span></span> <span data-ttu-id="1cf10-316">Gerçek test (durum) izleyen `If` anahtar sözcüğü ve true veya false değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-316">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="1cf10-317">`If` Deyimi ile sona erer `Then`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-317">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="1cf10-318">Sınama true olduğunda çalıştırılacak deyimleri kapsadığı `If` ve `End If`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-318">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="1cf10-319">Bir `If` deyimi içerebilir bir `Else` koşul false ise çalıştırılacak deyimleri belirtir engelle:</span><span class="sxs-lookup"><span data-stu-id="1cf10-319">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="1cf10-320">Varsa bir `If` deyimi başlatan bir kod bloğu, normal kullanmak zorunda değilsiniz `Code...End Code` blokları içerecek şekilde deyimleri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-320">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="1cf10-321">Yalnızca ekleyebilirsiniz `@` bloğuna ve çalışır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-321">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="1cf10-322">Bu yaklaşım çalışır `If` diğer Visual Basic dahil olmak üzere kod blokları tarafından izlenen anahtar sözcükleri programlama yanı sıra `For`, `For Each`, `Do While`vb.</span><span class="sxs-lookup"><span data-stu-id="1cf10-322">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="1cf10-323">Bir veya daha fazla kullanarak birden çok koşul ekleyebilirsiniz `ElseIf` blokları:</span><span class="sxs-lookup"><span data-stu-id="1cf10-323">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="1cf10-324">Bu örnekte, ilk olarak koşulu, `If` blok true değil `ElseIf` koşul denetlenir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-324">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="1cf10-325">Bu koşul karşılanıyorsa deyimlerinde `ElseIf` bloğu yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-325">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="1cf10-326">Hiçbir koşul karşılanıyorsa deyimlerinde `Else` bloğu yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-326">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="1cf10-327">Herhangi bir sayıda ekleyebilirsiniz `ElseIf` engeller ve ile kapatın bir `Else` olarak block &quot;diğer her şey&quot; koşul.</span><span class="sxs-lookup"><span data-stu-id="1cf10-327">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="1cf10-328">Çok sayıda koşulları test etmek için bir `Select Case` engelle:</span><span class="sxs-lookup"><span data-stu-id="1cf10-328">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="1cf10-329">Test etmek için parantez (örneğin, hafta içi değişkeni içinde) değerdir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-329">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="1cf10-330">Her bir testi kullanan bir `Case` listeleyen bir değer ifadesi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-330">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="1cf10-331">Varsa değerini bir `Case` deyimi, kodu test değeri ile eşleşen `Case` bloğu yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-331">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="1cf10-332">Bir tarayıcıda görüntülenen son iki koşullu blokları sonucu:</span><span class="sxs-lookup"><span data-stu-id="1cf10-332">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="1cf10-334">Döngü kod</span><span class="sxs-lookup"><span data-stu-id="1cf10-334">Looping code</span></span>

<span data-ttu-id="1cf10-335">Genellikle aynı deyimleri tekrar tekrar çalıştırmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-335">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="1cf10-336">Bunun için döngü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-336">You do this by looping.</span></span> <span data-ttu-id="1cf10-337">Örneğin, genellikle her öğe için aynı deyimleri verilerinin bir koleksiyonunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-337">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="1cf10-338">Tam döngü istediğiniz kaç kez biliyorsanız, kullanabileceğiniz bir `For` döngü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-338">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="1cf10-339">Bu tür bir döngü sayımı veya sayım için kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-339">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="1cf10-340">Döngü ile başlayan `For` anahtar sözcüğü, üç öğeleri tarafından takip:</span><span class="sxs-lookup"><span data-stu-id="1cf10-340">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="1cf10-341">Hemen sonra `For` deyimi bir sayaç değişkeni bildirme (kullanmak zorunda değilsiniz `Dim`) ve ardından de aralık belirtmek `i = 10 to 20`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-341">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="1cf10-342">Değişkeni başka bir deyişle `i` 10'da sayımı Başlat ve 20 (sınırlar dahil) ulaşana kadar devam.</span><span class="sxs-lookup"><span data-stu-id="1cf10-342">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="1cf10-343">Arasında `For` ve `Next` deyimleri blok içeriği olan.</span><span class="sxs-lookup"><span data-stu-id="1cf10-343">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="1cf10-344">Bu, yürütülen bir veya daha fazla kod deyimlerini her döngü ile içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-344">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="1cf10-345">`Next i` Deyimi, döngü sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-345">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="1cf10-346">Bu sayaç artırılır ve döngünün sonraki yinelemesine başlatır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-346">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="1cf10-347">Arasında kod satırının `For` ve `Next` satırlarını döngünün her yinelemesinden için çalışan kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-347">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="1cf10-348">Yeni bir paragraf biçimlendirme oluşturur (`<p>` öğesi) her zaman ve çıktıyı görüntüleme değeri, bir satır ekler i (sayaç).</span><span class="sxs-lookup"><span data-stu-id="1cf10-348">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="1cf10-349">Bu sayfa çalıştırdığınızda, örnek çıktı, her satırda öğe sayısını gösteren bir metin ile görüntüleme 11 satırları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-349">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="1cf10-351">Bir koleksiyon veya dizi ile çalışıyorsanız, sık kullandığınız bir `For Each` döngü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-351">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="1cf10-352">Bir koleksiyon benzer nesnelerin grubudur ve `For Each` döngü, gerçekleştirdiğiniz koleksiyondaki her öğe üzerinde bir görev sağlar.</span><span class="sxs-lookup"><span data-stu-id="1cf10-352">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="1cf10-353">Bu tür bir döngü koleksiyonlar için uygundur çünkü aksine bir `For` döngü yazmanız gerekmez sayaç artırın veya bir sınır belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-353">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="1cf10-354">Bunun yerine, `For Each` döngü kodunun işlemi tamamlanana kadar toplulukta yalnızca geçer.</span><span class="sxs-lookup"><span data-stu-id="1cf10-354">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="1cf10-355">Bu örnekte öğeleri döndürür `Request.ServerVariables` (web sunucunuza hakkında bilgi içeren) koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-355">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="1cf10-356">Bunu kullanan bir `For Each` yeni bir oluşturarak her öğenin adını görüntülemek için döngü `<li>` HTML madde işaretli liste öğesinde.</span><span class="sxs-lookup"><span data-stu-id="1cf10-356">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="1cf10-357">`For Each` Anahtar sözcüğü koleksiyondaki tek bir öğeyi temsil eden bir değişken arkasından (örnekte `myItem`) ve ardından `In` döngü koleksiyonu ardından anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-357">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="1cf10-358">Gövdesinde `For Each` döngü, daha önce bildirilen değişken kullanarak geçerli öğeye erişebilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-358">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="1cf10-360">Daha genel amaçlı bir döngü oluşturmak için kullanın `Do While` deyimi:</span><span class="sxs-lookup"><span data-stu-id="1cf10-360">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="1cf10-361">Bu döngü ile başlayan `Do While` anahtar sözcüğü, bir koşul tarafından izlenen yinelemek için blok tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="1cf10-361">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="1cf10-362">Genellikle döngü Artır (Ekle) veya azaltma (Çıkart) bir değişken veya sayım için kullanılan nesne.</span><span class="sxs-lookup"><span data-stu-id="1cf10-362">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="1cf10-363">Örnekte, `+=` işleci döngü her çalıştığında bir değişken değerine 1 ekler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-363">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="1cf10-364">(Geriye doğru sayan bir döngü içinde bir değişken azaltma için azaltma işleci kullanırsınız `-=`.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-364">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="1cf10-365">Nesneler ve Koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="1cf10-365">Objects and Collections</span></span>

<span data-ttu-id="1cf10-366">ASP.NET Web sitesi içinde hemen her şeyi web sayfası dahil olmak üzere, bir nesne var.</span><span class="sxs-lookup"><span data-stu-id="1cf10-366">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="1cf10-367">Bu bölümde, ile sık kodunuzda çalışabilecek önemli bazı nesneler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-367">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="1cf10-368">Sayfa nesneleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-368">Page objects</span></span>

<span data-ttu-id="1cf10-369">En temel ASP.NET sayfası nesnedir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-369">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="1cf10-370">Herhangi bir hak kazanan nesnesi olmadan doğrudan sayfası nesnenin özelliklerine erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-370">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="1cf10-371">Aşağıdaki kod sayfanın dosya yolunu alır kullanarak `Request` sayfasının nesne:</span><span class="sxs-lookup"><span data-stu-id="1cf10-371">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="1cf10-372">Özelliklerini kullanabilirsiniz `Page` nesne gibi çok bilgi almak için:</span><span class="sxs-lookup"><span data-stu-id="1cf10-372">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- `Request`<span data-ttu-id="1cf10-373">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-373">.</span></span> <span data-ttu-id="1cf10-374">Bu önceden gördüğünüz gibi ne tür bir tarayıcı yapılan istek URL'sini sayfa, kullanıcı kimliği, vb. dahil olmak üzere, geçerli istek hakkındaki bilgiler koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-374">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- `Response`<span data-ttu-id="1cf10-375">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-375">.</span></span> <span data-ttu-id="1cf10-376">Sunucu kodu çalıştırma bittiğinde, tarayıcıya gönderilen yanıt (sayfa) hakkında bilgi koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-376">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="1cf10-377">Örneğin, yanıtınıza yazmak için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-377">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="1cf10-378">Koleksiyon nesnelerini (diziler ve sözlükleri)</span><span class="sxs-lookup"><span data-stu-id="1cf10-378">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="1cf10-379">Bir koleksiyonu, koleksiyonu gibi aynı türden nesneleri grubudur `Customer` veritabanı nesneleri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-379">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="1cf10-380">ASP.NET içeren pek çok yerleşik koleksiyonlar gibi `Request.Files` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-380">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="1cf10-381">Genellikle, koleksiyonları verilerle çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="1cf10-381">You'll often work with data in collections.</span></span> <span data-ttu-id="1cf10-382">İki ortak koleksiyon türü *dizi* ve *sözlük*.</span><span class="sxs-lookup"><span data-stu-id="1cf10-382">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="1cf10-383">Bir dizi benzer öğeleri koleksiyonu depolamak istediğiniz ancak her bir öğe tutmak için ayrı bir değişken oluşturmak istemeyen yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="1cf10-383">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="1cf10-384">Dizilerle, bir özel veri türü gibi bildirdiğiniz `String`, `Integer`, veya `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-384">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="1cf10-385">Bir dizi değişkeni içerebilir, Değişken bildiriminde parantez ekleyin belirtmek için (gibi `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="1cf10-385">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="1cf10-386">Öğeleri konumlarına (dizin) kullanarak bir diziye veya kullanarak erişebileceğiniz `For Each` deyimi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-386">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="1cf10-387">Dizi dizinleri sıfır tabanlı &#8212; diğer bir deyişle, birinci öğenin konumundaki konumlandırın 0, ikinci öğesi konum 1 ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-387">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="1cf10-388">Bir dizideki öğe sayısını alarak belirleyebilirsiniz, `Length` özelliği.</span><span class="sxs-lookup"><span data-stu-id="1cf10-388">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="1cf10-389">Dizideki belirli bir öğenin konumunu almak için (diğer bir deyişle, diziyi aramak için), kullanın `Array.IndexOf` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-389">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="1cf10-390">Bir dizinin içeriğini de ters gibi şeyler yapabilirsiniz ( `Array.Reverse` yöntemi) veya içeriği sıralama ( `Array.Sort` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="1cf10-390">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="1cf10-391">Bir tarayıcıda görüntülenen dize dizisi kodun çıktısı:</span><span class="sxs-lookup"><span data-stu-id="1cf10-391">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="1cf10-393">Bir anahtar/değer çifti koleksiyonunu ayarlayın veya karşılık gelen değeri almak için anahtar (veya ad) sağlarsınız sözlüktür:</span><span class="sxs-lookup"><span data-stu-id="1cf10-393">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="1cf10-394">Bir sözlüğü oluşturmak için kullandığınız `New` yeni oluşturuyorsanız göstermek için anahtar sözcüğü `Dictionary` nesne.</span><span class="sxs-lookup"><span data-stu-id="1cf10-394">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="1cf10-395">Bir değişken kullanarak bir sözlük atayabilirsiniz `Dim` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="1cf10-395">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="1cf10-396">Veri türleri parantez kullanılarak Sözlüğü'ndeki öğelerin kullanımını gösterir ( `( )` ).</span><span class="sxs-lookup"><span data-stu-id="1cf10-396">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="1cf10-397">Bildirimin sonunda, bu gerçekte yeni bir sözlük oluşturur bir yöntem olduğundan başka bir parantez çifti eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-397">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="1cf10-398">Öğeleri sözlüğüne eklenecek çağırabilirsiniz `Add` sözlük değişkeniyle yöntemi (`myScores` bu durumda) ve ardından bir anahtar ve değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-398">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="1cf10-399">Alternatif olarak, anahtarı belirtmek ve aşağıdaki örnekte olduğu gibi basit bir atama yapmak için parantez kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cf10-399">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="1cf10-400">Sözlükten bir değer almak için parantez içinde anahtarı belirtin:</span><span class="sxs-lookup"><span data-stu-id="1cf10-400">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="1cf10-401">Parametrelere sahip yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="1cf10-401">Calling Methods with Parameters</span></span>

<span data-ttu-id="1cf10-402">Bu makalenin önceki bölümlerinde anlatıldığı gibi ile program nesneleri yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-402">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="1cf10-403">Örneğin, bir `Database` nesne içerebilir bir `Database.Connect` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cf10-403">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="1cf10-404">Bir veya daha fazla parametre birçok yöntem de var.</span><span class="sxs-lookup"><span data-stu-id="1cf10-404">Many methods also have one or more parameters.</span></span> <span data-ttu-id="1cf10-405">A *parametresi* bir yöntem için geçirdiğiniz değerdir, görevini tamamlamak üzere yöntemi etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1cf10-405">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="1cf10-406">Örneğin, bakmak için bir bildirim `Request.MapPath` üç parametre almayan yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1cf10-406">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="1cf10-407">Bu yöntem, belirtilen sanal yolu sunucuda karşılık gelen fiziksel yolu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1cf10-407">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="1cf10-408">Yönteminin üç parametreler `virtualPath`, `baseVirtualDir`, ve `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="1cf10-408">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="1cf10-409">(Bildiriminde kabul verilerin veri türleriyle parametreleri listelendiğine dikkat edin.) Bu yöntemi çağırdığınızda, tüm üç parametrelerin değerlerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-409">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="1cf10-410">Razor sözdizimi olan Visual Basic kullanıyorsanız, bir yönteme parametreleri geçirmek için iki seçeneğiniz vardır: *konumsal parametreler* veya *adlandırılmış parametreleri*.</span><span class="sxs-lookup"><span data-stu-id="1cf10-410">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="1cf10-411">Konumsal parametreler kullanan bir yöntem çağırmak için yöntem bildiriminde belirtilen katı bir sırayla parametreleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-411">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="1cf10-412">(Genellikle bu sırada yöntemi için belgeleri okuyarak bilmeniz.) Sırayı izlemelidir ve herhangi bir parametre atlayamazsınız &#8212; gerekiyorsa, boş bir dize geçirirseniz (`""`) veya için bir değer yoksa, konumsal bir parametre için null.</span><span class="sxs-lookup"><span data-stu-id="1cf10-412">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="1cf10-413">Aşağıdaki örnekte adlı bir klasör olduğunu varsayar *betikleri* kullanarak Web sitenizde.</span><span class="sxs-lookup"><span data-stu-id="1cf10-413">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="1cf10-414">Kod çağrıları `Request.MapPath` doğru sırada üç parametre değerlerini yöntemi ve geçirir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-414">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="1cf10-415">Ardından, elde edilen eşlenen yolun görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-415">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="1cf10-416">Bir yöntem parametre fazla olduğunda, adlandırılmış parametreleri kullanarak daha temiz ve daha okunabilir kodunuzu tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-416">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="1cf10-417">Adlandırılmış parametreler kullanılarak bir yöntemi çağırmak için parametre adından belirtin `:=` ve sonra değerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-417">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="1cf10-418">Adlandırılmış parametreler bir avantajı, bunları istediğiniz herhangi bir sırada ekleyebilirsiniz sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-418">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="1cf10-419">(Bir dezavantajı yöntem çağrısında kompakt olmasıdır.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-419">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="1cf10-420">Aşağıdaki örnek, yukarıdakilerle aynı yöntemini çağırır, ancak adlı değerlerini sağlamak için parametreleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="1cf10-420">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="1cf10-421">Gördüğünüz gibi farklı parametreler geçirilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-421">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="1cf10-422">Ancak, önceki örnekte ve bu örneği çalıştırırsanız, aynı değeri döneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-422">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="1cf10-423">Hataları İşleme</span><span class="sxs-lookup"><span data-stu-id="1cf10-423">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="1cf10-424">Try-Catch deyimleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-424">Try-Catch statements</span></span>

<span data-ttu-id="1cf10-425">Denetiminiz dışındaki bir nedenle başarısız olabilir, kodunuzda genellikle deyimleri sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1cf10-425">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="1cf10-426">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1cf10-426">For example:</span></span>

- <span data-ttu-id="1cf10-427">Kodunuzu açmak, oluşturmak, okumak veya bir dosyaya yazmak çalışırsa, her türlü hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-427">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="1cf10-428">İstediğiniz dosyayı var olmayabilir, kilitli olabilir, kod değil izinlere sahip ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-428">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="1cf10-429">Benzer şekilde, veritabanındaki kayıtları güncelleştirmek kodunuzu çalışırsa, izin sorunları olabilir, veritabanı bağlantısını bırakılabilir, kaydetmek için verileri geçersiz vb. olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-429">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="1cf10-430">Programlama dilinde, bu gibi durumlarda çağrılır *özel durumları*.</span><span class="sxs-lookup"><span data-stu-id="1cf10-430">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="1cf10-431">Kodunuz bir özel durumla karşılaşırsa (oluşturur) oluşturur. bir hata iletisi diğer bir deyişle, en iyi kullanıcılara sinir bozucu.</span><span class="sxs-lookup"><span data-stu-id="1cf10-431">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="1cf10-433">Durumlarda burada kodunuzu çalıştırdığınızca özel durumlar ve hata iletileri bu tür önlemek için kullanabileceğiniz `Try/Catch` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-433">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="1cf10-434">İçinde `Try` deyimi, denetimi kodu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-434">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="1cf10-435">Bir veya daha fazla `Catch` deyimleri için özel konum (belirli tür özel durumlar) hatalar oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-435">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="1cf10-436">Kadar içerebilir `Catch` kapasitesinden hataları aramak ifadeleri yazarken gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-436">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="1cf10-437">Kullanmaktan kaçının öneririz `Response.Redirect` yönteminde `Try/Catch` deyimleri, bir özel durum sayfanızın neden olabileceği için.</span><span class="sxs-lookup"><span data-stu-id="1cf10-437">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="1cf10-438">Aşağıdaki örnek ilk isteğe bir metin dosyası oluşturur ve ardından kullanıcının dosyayı açma sağlayan bir düğme görüntüleyen bir sayfa görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-438">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="1cf10-439">Örnek kasıtlı olarak hatalı dosya adı kullanır, böylece bir özel durum neden olur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-439">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="1cf10-440">Kodu içerir `Catch` deyimleri için iki olası özel durumları: `FileNotFoundException`, dosya adı hatalı olması durumunda gerçekleşir ve `DirectoryNotFoundException`, ASP.NET bile klasörü bulamıyorsanız gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-440">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="1cf10-441">(, Örnek bir deyimde her şeyin düzgün çalıştığından, nasıl çalıştığını görmek için açıklama durumundan çıkarabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="1cf10-441">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="1cf10-442">Kodunuzu özel durumu işlemek istemediğiniz ederseniz, önceki ekran görüntüsündeki gibi bir hata sayfası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-442">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="1cf10-443">Ancak, `Try/Catch` bölüm, kullanıcı bu tür hataları görmemesi yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-443">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="1cf10-444">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1cf10-444">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="1cf10-445">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-445">Reference Documentation</span></span>

- [<span data-ttu-id="1cf10-446">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1cf10-446">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="1cf10-447">Visual Basic dili</span><span class="sxs-lookup"><span data-stu-id="1cf10-447">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
