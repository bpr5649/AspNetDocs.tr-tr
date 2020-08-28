---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC görünümlerine genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC görünümü nedir ve bir HTML sayfasından farklılık gösterir? Bu öğreticide, Stephen Walther size görünümleri ve nasıl yapılacağını gösterir...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044675"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC Görünümlerine Genel Bakış (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC görünümü nedir ve bir HTML sayfasından farklılık gösterir? Bu öğreticide, Stephen Walther bir görünüm içinde verileri ve HTML yardımcılarını görüntülemeyi nasıl kullanabileceğinizi gösterir.

Bu öğreticinin amacı, ASP.NET MVC görünümleri, verileri görüntülemek ve HTML Yardımcıları hakkında kısa bir giriş sunmaktır. Bu öğreticinin sonunda, yeni görünümler oluşturmayı, bir denetleyiciden bir görünüme veri geçişi ve bir görünümde içerik oluşturmak için HTML Yardımcıları kullanmayı anlamalısınız.

## <a name="understanding-views"></a>Görünümleri anlama

ASP.NET veya Active Server sayfalarından farklı olarak, ASP.NET MVC doğrudan bir sayfaya karşılık gelen herhangi bir şeyi içermez. Bir ASP.NET MVC uygulamasında, bir diskte, tarayıcınızın adres çubuğuna yazdığınız URL 'deki yola karşılık gelen bir sayfa yoktur. ASP.NET MVC uygulamasındaki bir sayfaya en yakın şey, *Görünüm*olarak adlandırılan bir şeydir.

ASP.NET MVC uygulamasında, gelen tarayıcı istekleri denetleyici eylemlerine eşlenir. Bir denetleyici eylemi bir görünüm döndürebilir. Ancak, bir denetleyici eylemi sizi başka bir denetleyici eylemine yönlendirme gibi başka bir eylem türü gerçekleştirebilir.

Listeleme 1, HomeController adlı basit bir denetleyici içerir. HomeController, Index () ve details () adlı iki denetleyici eylemini kullanıma sunar.

**Listeleme 1-HomeController. vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

Tarayıcı adres çubuğuna aşağıdaki URL 'YI yazarak dizin () eylemini ilk eylemi çağırabilirsiniz:

/Home/Index

Bu adresi tarayıcınıza yazarak, ayrıntılar () eylemini ikinci eylemi çağırabilirsiniz:

/Home/Details

Index () eylemi bir görünüm döndürür. Oluşturduğunuz çoğu eylem, görünümleri döndürür. Ancak, bir eylem diğer eylem sonuçları türlerini döndürebilir. Örneğin, Details () eylemi, gelen isteği dizin () eylemine yönlendiren bir RedirectToActionResult döndürür.

Index () eylemi aşağıdaki tek kod satırını içerir:

Görüntüleme ()

Bu kod satırı, Web sunucunuzdaki aşağıdaki yolda bulunması gereken bir görünüm döndürür:

\Views\home\ındex.aspx

Görünümün yolu, denetleyicinin adından ve denetleyici eyleminin adıyla algılanır.

İsterseniz, görünüm hakkında açık olabilirsiniz. Aşağıdaki kod satırı, Fred adlı bir görünüm döndürür:

Görünüm (Fred)

Bu kod satırı yürütüldüğünde, aşağıdaki yoldan bir görünüm döndürülür:

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC uygulamanız için birim testleri oluşturmayı planlıyorsanız, görünüm adları hakkında açık olması iyi bir fikirdir. Bu şekilde, beklenen görünümün bir denetleyici eylemi tarafından döndürüldüğünü doğrulamak için bir birim testi oluşturabilirsiniz.

## <a name="adding-content-to-a-view"></a>Görünüme Içerik ekleme

Görünüm, komut dosyaları içerebilen standart (X) HTML belgesidir. Bir görünüme dinamik içerik eklemek için betikleri kullanın.

Örneğin, liste 2 ' deki görünüm geçerli tarih ve saati gösterir.

**Listeleme 2-\Views\home\ındex.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

Liste 2 ' deki HTML sayfasının gövdesi aşağıdaki betiği içerir:

&lt;% Response. Write (DateTime. Now)%&gt;

&lt; &gt; Bir betiğin başlangıcını ve sonunu işaretlemek için% ve% komut dosyası sınırlayıcılarını kullanın. Bu betik, Visual Basic 'te yazılmıştır. İçeriği tarayıcıya işlemek için Response. Write () yöntemini çağırarak geçerli tarih ve saati görüntüler. &lt;% Ve% komut dosyası sınırlayıcıları &gt; bir veya daha fazla deyimi yürütmek için kullanılabilir.

Genellikle Response. Write () çağrısı yaptığından, Microsoft size Response. Write () metodunu çağırma için bir kısayol sağlar. Listeleme 3 ' teki görünüm, &lt; &gt; Response. Write () çağrısı için bir kısayol olarak% = ve% sınırlayıcılarını kullanır.

**Listeleme 3-Views\home\ındex2,aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

Bir görünümde dinamik içerik oluşturmak için herhangi bir .NET dili kullanabilirsiniz. Normalde, denetleyicilerinizi ve görünümlerinizi yazmak Için Visual Basic .NET veya C# kullanın.

## <a name="using-html-helpers-to-generate-view-content"></a>Görünüm Içeriği oluşturmak için HTML Yardımcıları kullanma

Bir görünüme içerik eklemenizi kolaylaştırmak için, *HTML Yardımcısı*adlı bir şeyin avantajlarından yararlanabilirsiniz. Genellikle bir HTML Yardımcısı, bir dize üreten bir yöntemdir. HTML Yardımcıları, metin kutuları, bağlantılar, açılan listeler ve liste kutuları gibi standart HTML öğeleri oluşturmak için kullanabilirsiniz.

Örneğin, kod 4 ' teki görünüm üç HTML yardımcıdan faydalanır: BeginForm (), TextBox () ve Password () yardımcıları--oturum açma formu oluşturmak için (bkz. Şekil 1).

**Listeleme 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![Yeni Proje iletişim kutusu](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**Şekil 01**: standart bir oturum açma formu ([tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-views-overview-vb/_static/image2.png))

HTML yardımcılarının tümü, görünümün HTML özelliğinde çağrılır. Örneğin, HTML. TextBox () yöntemini çağırarak bir metin kutusunu işleyebilirsiniz.

&lt; &gt; Hem HTML. TextBox () hem de HTML. Password () yardımcıları çağrılırken% = ve% komut dosyası sınırlayıcılarını kullanacağınızı unutmayın. Bu yardımcılar yalnızca bir dize döndürür. Dizeyi tarayıcıya işlemek için Response. Write () çağrısı yapmanız gerekir.

HTML Yardımcısı yöntemlerini kullanmak isteğe bağlıdır. Yazmanız gereken HTML ve betiğin miktarını azaltarak yaşamınızı daha kolay hale getirir. Listeleme 5 ' teki görünüm, HTML Yardımcıları kullanmadan liste 4 ' teki görünümle tam olarak aynı formu işler.

**Listeleme 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

Kendi HTML Yardımcıları oluşturma seçeneğiniz de vardır. Örneğin, bir HTML tablosunda otomatik olarak bir veritabanı kaydı kümesi görüntüleyen bir GridView () yardımcı yöntemi oluşturabilirsiniz. Bu konu, **özel HTML Yardımcıları oluşturma**öğreticisinde araştırıyoruz.

## <a name="using-view-data-to-pass-data-to-a-view"></a>Verileri görünüme geçirmek için Görünüm verilerini kullanma

Bir denetleyiciden bir görünüme veri geçirmek için verileri görüntüle 'yi kullanırsınız. Verileri posta aracılığıyla göndereceğiniz bir paket gibi görüntülemeyi düşünün. Bir denetleyiciden bir görünüme geçirilen tüm verilerin bu paket kullanılarak gönderilmesi gerekir. Örneğin, liste 6 ' daki denetleyici verileri görüntülemek için bir ileti ekler.

**6-ProductController. vb dosyasını listeleme**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

Controller ViewData özelliği bir ad ve değer çiftleri koleksiyonunu temsil eder. Liste 6 ' da, Index () yöntemi, Merhaba Dünya! değerine sahip ileti adlı görünüm verileri koleksiyonuna bir öğe ekler. Görünüm, Index () yöntemiyle döndürüldüğünde görünüm verileri otomatik olarak görünüme geçirilir.

Liste 7 ' deki görünüm, verileri görünüm verilerinden alır ve iletiyi tarayıcıya işler.

**Listeleme 7--\Views\product\ındex.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

Görünümün, iletiyi işlerken HTML. Encode () HTML yardımcı yönteminden yararlandığına dikkat edin. HTML. Encode () HTML Yardımcısı, ve gibi özel karakterleri, &lt; &gt; bir Web sayfasında görüntülenmek üzere güvenli karakterler olarak kodlar. Bir kullanıcının bir Web sitesine gönderdiği içeriği her oluşturduğunuzda, JavaScript ekleme saldırılarını engellemek için içeriği kodlamanız gerekir.

(Kendimize iletisini ProductController 'da oluşturduğumuz için gerçekten iletiyi kodlayamıyoruz. Ancak, görünümün içindeki verilerden alınan içeriği görüntülerken, her zaman HTML. Encode () yöntemini çağırmak iyi bir alışkanlıktır.)

Liste 7 ' de, bir denetleyiciden bir görünüme basit bir dize iletisi geçirmek için verileri görüntüle ' den faydalanır. Ayrıca, veritabanı kayıtlarının bir koleksiyonu gibi diğer veri türlerini bir denetleyiciden bir görünüme geçirmek için verileri görüntüle ' yi de kullanabilirsiniz. Örneğin, Products veritabanı tablosunun içeriğini bir görünümde görüntülemek istiyorsanız, veritabanı kayıtlarının koleksiyonunu görünüm verilerinde geçitirsiniz.

Bir denetleyiciden bir görünüme kesin olarak belirlenmiş görünüm verisi geçirme seçeneğiniz de vardır. Bu konuyu, **kesin türü belirtilmiş Görünüm verilerini ve görünümlerini anlama**öğreticisinde araştırıyoruz.

## <a name="summary"></a>Özet

Bu öğreticide, ASP.NET MVC görünümleri, verileri görüntüleme ve HTML Yardımcıları hakkında kısa bir giriş sunulmaktadır. İlk bölümde, projenize yeni görünümler eklemeyi öğrendiniz. Belirli bir denetleyiciden çağırmak için doğru klasöre bir görünüm eklemeniz gerektiğini öğrendiniz. Daha sonra, HTML yardımcılarını ele aldık. HTML yardımcıların standart HTML içeriğini kolayca oluşturmanıza nasıl imkan sağladığını öğrendiniz. Son olarak, bir denetleyiciden bir görünüme veri geçirmek için verileri görüntüleme özelliğinden nasıl yararlanırsınız hakkında öğrenirsiniz.

> [!div class="step-by-step"]
> [Önceki](passing-data-to-view-master-pages-cs.md) 
>  [Sonraki](creating-custom-html-helpers-vb.md)
