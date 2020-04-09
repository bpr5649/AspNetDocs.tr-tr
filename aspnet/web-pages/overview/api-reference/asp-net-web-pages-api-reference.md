---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Sayfaları (Razor) API Hızlı Başvuru | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu sayfa, Web Sayfalarını Jilet sözdizimi ile ASP.NET programlamak için en sık kullanılan nesnelerin, özelliklerin ve yöntemlerin kısa örneklerini içeren bir liste içerir.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676246"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="3bda2-103">ASP.NET Web Sayfaları (Razor) API Hızlı Başvuru</span><span class="sxs-lookup"><span data-stu-id="3bda2-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="3bda2-104"> yazan: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3bda2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3bda2-105">Bu sayfa, Web Sayfalarını Jilet sözdizimi ile ASP.NET programlamak için en sık kullanılan nesnelerin, özelliklerin ve yöntemlerin kısa örneklerini içeren bir liste içerir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="3bda2-106">"(v2)" ile işaretlenmiş açıklamalar ASP.NET Web Sayfaları sürüm 2'de tanıtıldı.</span><span class="sxs-lookup"><span data-stu-id="3bda2-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="3bda2-107">API başvuru belgeleri için, MSDN'deki [Web Sayfaları Başvuru Belgeleri ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) bakın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="3bda2-108">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="3bda2-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="3bda2-109">ASP.NET Web Sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3bda2-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3bda2-110">Bu öğretici ayrıca ASP.NET Web Sayfaları 2 ve ASP.NET Web Sayfaları 1.0 ile de çalışır (v2 işaretli özellikler hariç).</span><span class="sxs-lookup"><span data-stu-id="3bda2-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="3bda2-111">Bu sayfa aşağıdakiler için referans bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="3bda2-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="3bda2-112">Sınıflar</span><span class="sxs-lookup"><span data-stu-id="3bda2-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="3bda2-113">Veri</span><span class="sxs-lookup"><span data-stu-id="3bda2-113">Data</span></span>](#Data)
- [<span data-ttu-id="3bda2-114">Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="3bda2-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="3bda2-115">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="3bda2-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="3bda2-116">Sınıflar</span><span class="sxs-lookup"><span data-stu-id="3bda2-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="3bda2-117">Uygulamadaki herhangi bir sayfa tarafından paylaşılabilen verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="3bda2-118">Aşağıdaki örnekte `App` olduğu gibi, aynı verilere erişmek için dinamik özelliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bda2-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="3bda2-119">Dize değerini Boolean değerine (true/false) dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="3bda2-120">Dize doğru/yanlışı temsil etmiyorsa false veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="3bda2-121">Dize değerini tarihe/saate dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-121">Converts a string value to date/time.</span></span> <span data-ttu-id="3bda2-122">Dize bir tarihi/saati temsil etmiyorsa, verir `DateTime.MinValue` veya belirtilen değeri verir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="3bda2-123">Dize değerini ondalık değere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="3bda2-124">Dize ondalık değeri temsil etmiyorsa 0,0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="3bda2-125">Dize değerini float'a dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-125">Converts a string value to a float.</span></span> <span data-ttu-id="3bda2-126">Dize ondalık değeri temsil etmiyorsa 0,0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="3bda2-127">Dize değerini bir tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-127">Converts a string value to an integer.</span></span> <span data-ttu-id="3bda2-128">Dize bir karşıcıyı temsil etmiyorsa 0 veya belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="3bda2-129">İsteğe bağlı ek yol parçalarıyla yerel bir dosya yolundan tarayıcı uyumlu bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bda2-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="3bda2-130">*Değeri* HTML kodlanmış çıktı olarak işlemek yerine HTML biçimlendirmesi olarak işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="3bda2-131">Değer bir dizeden belirtilen türe dönüştürülebiliyorsa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="3bda2-132">Nesne veya değişkenin değeri yoksa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="3bda2-133">İstek bir POST ise doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="3bda2-134">(İlk istekler genellikle GET'dir.)</span><span class="sxs-lookup"><span data-stu-id="3bda2-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="3bda2-135">Bu sayfaya uygulanacak bir düzen sayfasının yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="3bda2-136">Geçerli istekteki sayfa, düzen sayfaları ve kısmi sayfalar arasında paylaşılan verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="3bda2-137">Aşağıdaki örnekte `Page` olduğu gibi, aynı verilere erişmek için dinamik özelliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bda2-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="3bda2-138">(Düzen sayfaları) Herhangi bir adlandırılmış bölümde olmayan bir içerik sayfasının içeriğini işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="3bda2-139">Belirtilen yolu ve isteğe bağlı ek verileri kullanarak bir içerik sayfasını işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="3bda2-140">Ekstra parametrelerin değerlerini konuma göre `PageData` (örnek 1) veya anahtardan (örnek 2) alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bda2-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="3bda2-141">(Düzen sayfaları) Adı olan bir içerik bölümü işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="3bda2-142">Bir bölümü isteğe bağlı hale getirmek için yanlış olması *için gerekli* ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="3bda2-143">Bir HTTP çerezinin değerini alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="3bda2-144">Geçerli istekte yüklenen dosyaları alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="3bda2-145">Bir formda (dizeleri olarak) deftere nakledilen verileri alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="3bda2-146">`Request[key]`hem koleksiyonları `Request.Form` hem `Request.QueryString` de koleksiyonları denetler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="3bda2-147">URL sorgu dizesinde belirtilen verileri alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="3bda2-148">`Request[key]`hem koleksiyonları `Request.Form` hem `Request.QueryString` de koleksiyonları denetler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="3bda2-149">Bir form öğesi, sorgu dize değeri, çerez veya üstbilgi değeri için istek doğrulamayı seçici olarak devre dışı kılabilir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="3bda2-150">İstek doğrulaması varsayılan olarak etkinleştirilir ve kullanıcıların biçimlendirme veya diğer tehlikeli olabilecek içerikleri deftere nakletmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="3bda2-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="3bda2-151">Yanıta bir HTTP sunucu üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="3bda2-152">Sayfa çıktısını belirli bir süre için önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="3bda2-153">İsteğe bağlı olarak her sayfa erişiminde zaman alabildiği zaman asımı sıfırlamak için *kaydırMa* ayarlayın ve sayfa isteğindeki her farklı sorgu dizesi için sayfanın farklı sürümlerini önbelleğe almak için *ByParams'ı değiştirin.*</span><span class="sxs-lookup"><span data-stu-id="3bda2-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="3bda2-154">Tarayıcı isteğini yeni bir konuma yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="3bda2-155">Tarayıcıya gönderilen HTTP durum kodunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="3bda2-156">*Verilerin* içeriğini isteğe bağlı MIME türüyle yanıta yazar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="3bda2-157">Yanıta bir dosyanın içeriğini yazar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="3bda2-158">(Düzen sayfaları) Adı olan bir içerik bölümü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="3bda2-159">HTML kodlanmış bir dize çözme.</span><span class="sxs-lookup"><span data-stu-id="3bda2-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="3bda2-160">HTML biçimlendirmesinde işleme için bir dize kodlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="3bda2-161">Belirtilen sanal yol için sunucu fiziksel yolunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="3bda2-162">URL'deki metni deşifre eder.</span><span class="sxs-lookup"><span data-stu-id="3bda2-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="3bda2-163">URL'ye koymak için metni kodlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="3bda2-164">Kullanıcı tarayıcıyı kapatana kadar var olan bir değeri alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="3bda2-165">Nesnenin değerinin dize gösterimini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="3bda2-166">URL'den ek veri alır (örneğin, */MyPage/ExtraData).*</span><span class="sxs-lookup"><span data-stu-id="3bda2-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="3bda2-167">Belirtilen kullanıcının parolasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="3bda2-168">Hesap onay belirteci kullanarak bir hesabı onaylar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="3bda2-169">Belirtilen kullanıcı adı ve parolaile yeni bir kullanıcı hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bda2-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="3bda2-170">Bir onay belirteci gerektirmek için, *gerekliConfirmationToken* için doğru geçmek.</span><span class="sxs-lookup"><span data-stu-id="3bda2-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="3bda2-171">Şu anda oturum açmış kullanıcıiçin sonda tanımlayıcısını alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="3bda2-172">Şu anda oturum açmış olan kullanıcının adını alır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="3bda2-173">Kullanıcının parolayı sıfırlayabilmesi için kullanıcıya e-posta yla gönderilebilen parola sıfırlama belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bda2-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="3bda2-174">Kullanıcı adından kullanıcı kimliğini verir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="3bda2-175">Geçerli kullanıcı oturum açmışsa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="3bda2-176">Kullanıcı onaylandıysa (örneğin, bir onay e-postası aracılığıyla) doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="3bda2-177">Geçerli kullanıcının adı belirtilen kullanıcı adıyla eşleşiyorsa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="3bda2-178">Çerezde kimlik doğrulama belirteci ayarlayarak kullanıcıyı oturum açar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="3bda2-179">Kimlik doğrulama belirteci çerezini kaldırarak kullanıcıyı dışarı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3bda2-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="3bda2-180">Kullanıcı nın kimliği doğrulanmazsa, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="3bda2-181">Geçerli kullanıcı belirtilen rollerden birinin üyesi değilse, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="3bda2-182">Geçerli kullanıcı *kullanıcı adı*ile belirtilen kullanıcı değilse, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="3bda2-183">Parola sıfırlama belirteci geçerliyse, kullanıcının parolasını yeni parolayla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="3bda2-184">Veriler</span><span class="sxs-lookup"><span data-stu-id="3bda2-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="3bda2-185">INSERT, DELETE veya UPDATE gibi *SQLstatement* 'ı (isteğe bağlı parametrelerle) yürütür ve etkilenen kayıtların sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="3bda2-186">En son eklenen satırdaki kimlik sütununa döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="3bda2-187">Belirtilen veritabanı dosyasını veya *Web.config* dosyasından adlandırılmış bir bağlantı dizesini kullanarak belirtilen veritabanını açar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="3bda2-188">Bağlantı dizesini kullanarak bir veritabanı açar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-188">Opens a database using the connection string.</span></span> <span data-ttu-id="3bda2-189">`Database.Open`(Bu, bağlantı dizesi adı kullanan ile tezat.)</span><span class="sxs-lookup"><span data-stu-id="3bda2-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="3bda2-190">*SQLstatement* kullanarak veritabanını sorgular (isteğe bağlı parametreleri geçen) ve sonuçları bir koleksiyon olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="3bda2-191">*SQLdeyimi* (isteğe bağlı parametrelerle) yürütür ve tek bir kayıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="3bda2-192">*SQLdeyimi* (isteğe bağlı parametrelerle) yürütür ve tek bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="3bda2-193">Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="3bda2-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="3bda2-194">Belirtilen kimlik için Google Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="3bda2-195">Belirtilen proje için StatCounter Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="3bda2-196">Belirtilen hesap için Yahoo Analytics JavaScript kodunu işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="3bda2-197">Aramayı Bing'e aktarın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-197">Passes a search to Bing.</span></span> <span data-ttu-id="3bda2-198">Aranacak siteyi ve arama kutusunun başlığını belirtmek için, bu siteyi `Bing.SiteUrl` ve `Bing.SiteTitle` özelliklerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bda2-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="3bda2-199">Normalde bu özellikleri \* \_AppStart\* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3bda2-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="3bda2-200">Bir grafiği n için başharfe ait hale.</span><span class="sxs-lookup"><span data-stu-id="3bda2-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="3bda2-201">Grafiğe bir gösterge ekler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="3bda2-202">Grafiğe bir dizi değer ekler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="3bda2-203">Belirtilen veriler için karma döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="3bda2-204">Varsayılan algoritma `sha256`.</span><span class="sxs-lookup"><span data-stu-id="3bda2-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="3bda2-205">Facebook kullanıcılarının sayfalara bağlantı kurmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="3bda2-206">Dosya yüklemek için Genel BirA'yı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="3bda2-207">Belirtilen Xbox oyuncu etiketini işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="3bda2-208">Belirtilen e-posta adresi için Gravatar görüntüsünü işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="3bda2-209">Bir veri nesnesini JavaScript Nesne Gösterimi (JSON) biçiminde bir dize dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="3bda2-210">JSON kodlu giriş dizesini, üzerinde kopyalayabildiğiniz veya veritabanına ekleyebildiğiniz bir veri nesnesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="3bda2-211">Belirtilen başlığı ve isteğe bağlı URL'yi kullanarak sosyal ağ bağlantılarını işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="3bda2-212">Hata iletisi form alanıyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="3bda2-212">Associates an error message with a form field.</span></span> <span data-ttu-id="3bda2-213">Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="3bda2-214">Hata iletisi ile form ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-214">Associates an error message with a form.</span></span> <span data-ttu-id="3bda2-215">Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="3bda2-216">Doğrulama hatası yoksa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="3bda2-217">Bu `ModelState` üyeye erişmek için yardımcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bda2-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="3bda2-218">Bir nesnenin ve alt nesnelerin özelliklerini ve değerlerini işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="3bda2-219">ReCAPTCHA doğrulama testini işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="3bda2-220">ReCAPTCHA hizmeti için ortak ve özel anahtarları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="3bda2-221">Normalde bu özellikleri \* \_AppStart\* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3bda2-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="3bda2-222">ReCAPTCHA testinin sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="3bda2-223">ASP.NET Web Sayfaları hakkındaki durum bilgilerini işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="3bda2-224">Belirtilen kullanıcı için bir Twitter akışı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="3bda2-225">Belirtilen arama metni için bir Twitter akışı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="3bda2-226">Belirtilen dosya için isteğe bağlı genişlik ve yüksekliğe sahip bir Flash video oynatıcı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="3bda2-227">Belirtilen dosya için isteğe bağlı genişlik ve yüksekliğe sahip bir Windows Media oynatıcısı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="3bda2-228">Belirtilen *.xap* dosyası için gerekli genişlik ve yüksekliğe sahip bir Silverlight oynatıcı sıcağa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="3bda2-229">*Anahtarla*belirtilen nesneyi döndürür veya nesne bulunmazsa null' u verir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="3bda2-230">*Anahtarla* belirtilen nesneyi önbellekten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3bda2-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="3bda2-231">*Anahtarla*belirtilen ad altında önbelleğe *değer* koyar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="3bda2-232">Sorgudaki verileri `WebGrid` kullanarak yeni bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bda2-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="3bda2-233">Verileri HTML tablosunda görüntülemek için biçimlendirme yi işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="3bda2-234">Nesne için bir çağrı `WebGrid` cihazı işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="3bda2-235">Görüntüyü belirtilen yoldan yükler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="3bda2-236">Belirtilen görüntüyü filigran olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="3bda2-237">Belirtilen metni resme ekler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="3bda2-238">Görüntüyü yatay veya dikey olarak çevirir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="3bda2-239">Dosya yüklemesi sırasında bir sayfaya görüntü gönderildiğinde görüntü yükler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="3bda2-240">Görüntüyü yeniden boyutlandırıyor.</span><span class="sxs-lookup"><span data-stu-id="3bda2-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="3bda2-241">Görüntüyü sola veya sağa döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="3bda2-242">Görüntüyü belirtilen yola kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3bda2-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="3bda2-243">SMTP sunucusunun parolasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="3bda2-244">Normalde bu özelliği \* \_AppStart\* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3bda2-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="3bda2-245">Bir e-posta iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="3bda2-246">SMTP sunucu adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-246">Sets the SMTP server name.</span></span> <span data-ttu-id="3bda2-247">Normalde bu özelliği \* \_AppStart\* sayfasında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3bda2-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="3bda2-248">SMTP sunucusunun kullanıcı adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="3bda2-249">Normalde bu özelliği \* \_AppStart\* sayfasında ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="3bda2-250">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="3bda2-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="3bda2-251">(v2) Belirtilen alan için bir doğrulama hatası iletisi işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="3bda2-252">(v2) Tüm doğrulama hatalarının listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="3bda2-253">(v2) Belirtilen doğrulama türü için bir kullanıcı giriş öğesi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3bda2-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="3bda2-254">(v2) Doğrulama hata iletilerini biçimlendirebilmeniz için istemci tarafı doğrulaması için CSS sınıf özniteliklerini dinamik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="3bda2-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="3bda2-255">(Uygun istemci komut dosyası kitaplıklarına başvurmanızı ve CSS sınıflarını tanımlamanızı gerektirir.)</span><span class="sxs-lookup"><span data-stu-id="3bda2-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="3bda2-256">(v2) Kullanıcı giriş alanı için istemci tarafı doğrulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3bda2-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="3bda2-257">(Uygun istemci komut dosyası kitaplıkları başvuru gerektirir.)</span><span class="sxs-lookup"><span data-stu-id="3bda2-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="3bda2-258">(v2) Doğrulama için kayıt yaptırılan tüm kullanıcı giriş öğeleri geçerli değerler içeriyorsa doğru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bda2-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="3bda2-259">(v2) Kullanıcıların kullanıcı giriş öğesi için bir değer sağlaması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="3bda2-260">(v2) Kullanıcıların her kullanıcı giriş öğesi için değerler sağlaması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="3bda2-261">Bu yöntem, özel bir hata iletisi belirtmenize izin vermez.</span><span class="sxs-lookup"><span data-stu-id="3bda2-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="3bda2-262">(v2) `Validation.Add` Yöntemi kullandığınızda bir doğrulama testi belirtir.</span><span class="sxs-lookup"><span data-stu-id="3bda2-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
