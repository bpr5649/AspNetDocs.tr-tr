---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'Yineleme #3 – Form doğrulama ekle (C#) | Microsoft Dokümanlar'
author: rick-anderson
description: Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Biz de emai doğrulamak ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: c8442574d4901045f044f53ea12cd8330e8eaaa3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542384"
---
# <a name="iteration-3--add-form-validation-c"></a>3. Yineleme – Form doğrulaması ekleme (C#)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (C#)

Öğreticiler bu dizi, biz baştan sona tüm Bir İletişim Yönetimi uygulaması oluşturmak. İletişim Yöneticisi uygulaması, kişi listesi için kişi bilgilerini (adlar, telefon numaraları ve e-posta adresleri) depolamanızı sağlar.

Uygulamayı birden çok yineleme üzerine oluşturuyoruz. Her yineleme ile, yavaş yavaş uygulama geliştirmek. Bu çoklu yineleme yaklaşımının amacı, her değişikliğin nedenini anlamanızı sağlamaktır.

- Yineleme #1 - Uygulamayı oluşturun. İlk yinelemede, İletişim Yöneticisi'ni mümkün olan en basit şekilde oluştururuz. Temel veritabanı işlemleri için destek ekliyoruz: Oluşturma, Okuma, Güncelleme ve Sil (CRUD).

- Yineleme #2 - Uygulama güzel görünmesini sağlamak. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfasını ve basamaklı stil sayfasını değiştirerek uygulamanın görünümünü iyileştiriyoruz.

- Yineleme #3 - Form doğrulama ekleyin. Üçüncü yinelemede, temel form doğrulamasını ekleriz. İnsanların gerekli form alanlarını tamamlamadan form göndermelerini engelliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğrularız.

- Yineleme #4 - Uygulamayı gevşek bir şekilde biraraya getirin. Bu dördüncü yinelemede, İletişim Yöneticisi uygulamasını korumayı ve değiştirmeyi kolaylaştırmak için çeşitli yazılım tasarım desenlerinden yararlanıyoruz. Örneğin, uygulamamızı Depo deseni ve Bağımlılık Enjeksiyonu modelini kullanmak üzere yeniden düzenlemeyiz.

- Yineleme #5 - Birim testleri oluşturun. Beşinci yinelemede, birim testleri ekleyerek uygulamamızın korunmasını ve değiştirilmesini kolaylaştırıyoruz. Veri modeli sınıflarımızla alay ediyoruz ve denetleyicilerimiz ve doğrulama mantığımız için birim testleri oluşturuyoruz.

- Yineleme #6 - Test odaklı geliştirme yi kullanın. Bu altıncı yinelemede, önce birim testleri yazarak ve birim testlerine karşı kod yazarak uygulamamıza yeni işlevler ekliyoruz. Bu yinelemeye kişi grupları ekliyoruz.

- Yineleme #7 - Ajax işlevselliği ekleyin. Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="this-iteration"></a>Bu Yineleme

İletişim Yöneticisi uygulamasının bu ikinci yinelemesinde temel form doğrulamasını ekliyoruz. İnsanların gerekli form alanları için değerler girmeden ilgili kişi göndermesini engelliyoruz. Telefon numaralarını ve e-posta adreslerini de doğrularız (Bkz. Şekil 1).

[![Yeni Proje iletişim kutusu](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**Şekil 01**: Doğrulamalı bir form ([Tam boyutlu resmi görüntülemek için tıklayınız](iteration-3-add-form-validation-cs/_static/image2.png))

Bu yinelemede, doğrulama mantığını doğrudan denetleyici eylemlere ekleriz. Genel olarak, bu ASP.NET Bir MVC uygulamasına doğrulama eklemek için önerilen yol değildir. Daha iyi bir yaklaşım, bir uygulama doğrulama mantığını ayrı bir [hizmet katmanına](http://martinfowler.com/eaaCatalog/serviceLayer.html)yerleştirmektir. Bir sonraki yinelemede, uygulamayı daha koruyabilir hale getirmek için İletişim Yöneticisi uygulamasını yeniden eleştirmekteyiz.

Bu yinelemede, her şeyi basit tutmak için, tüm doğrulama kodunu elle yazarız. Doğrulama kodunu kendimiz yazmak yerine, doğrulama çerçevesinden yararlanabiliriz. Örneğin, ASP.NET MVC uygulamanız için doğrulama mantığını uygulamak için Microsoft Enterprise Library Library Doğrulama Uygulama Bloğu'nu (VAB) kullanabilirsiniz. Doğrulama Uygulama Bloğu hakkında daha fazla bilgi edinmek için bkz:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Oluşturma Görünümüne Doğrulama Ekleme

Oluştur görünümüne doğrulama mantığı ekleyerek başlayalım. Neyse ki, Visual Studio ile Create görünümünü oluşturduğumuz için, Create görünümü doğrulama iletilerini görüntülemek için gerekli tüm kullanıcı arabirimi mantığını zaten içerir. Oluştur görünümü Listeleme 1'de bulunur.

**Listeleme 1 - \Görünümler\İletişim\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

HTML formunun hemen üzerinde görünen Html.ValidationSummary() yardımcı yöntemine yapılan çağrıya dikkat edin. Doğrulama hatası iletileri varsa, bu yöntem madde işaretli listede doğrulama iletileri görüntüler.

Ayrıca, her form alanının yanında görünen Html.ValidationMessage() çağrılarına da dikkat edin. Doğrulama İletisi() yardımcısı tek bir doğrulama hatası iletisi görüntüler. Listeleme 1 durumunda, bir doğrulama hatası olduğunda bir yıldız görüntülenir.

Son olarak, Html.TextBox() yardımcısı, yardımcı tarafından görüntülenen özellik ile ilişkili bir doğrulama hatası olduğunda, otomatik olarak Basamaklı Stil Sayfası sınıfını işler. Html.TextBox() yardımcı girişi **doğrulama-hata**adlı bir sınıf işler.

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, İçerik klasöründe otomatik olarak Site.css adında bir stil sayfası oluşturulur. Bu stil sayfası, doğrulama hatası iletilerinin görünümüyle ilgili CSS sınıfları için aşağıdaki tanımları içerir:

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

Alan doğrulama-hata sınıfı, Html.ValidationMessage() yardımcısı tarafından işlenen çıktıyı stillendirmek için kullanılır. Giriş doğrulama-hata sınıfı, Html.TextBox() yardımcısı tarafından işlenen textbox'ı (giriş) stillendirmek için kullanılır. Doğrulama-özet-hatalar sınıfı, Html.ValidationSummary() yardımcısı tarafından işlenen sıralanmamış listeyi stillendirmek için kullanılır.

> [!NOTE] 
> 
> Doğrulama hatası iletilerinin görünümünü özelleştirmek için bu bölümde açıklanan stil sayfası sınıflarını değiştirebilirsiniz.

## <a name="adding-validation-logic-to-the-create-action"></a>Oluşturma Eylemine Doğrulama Mantığı Ekleme

Şu anda, herhangi bir ileti oluşturma mantığını yazmadığımız için Oluşturma görünümü hiçbir zaman doğrulama hatası iletilerini görüntülemez. Doğrulama hata iletilerini görüntülemek için hata iletilerini ModelState'e eklemeniz gerekir.

> [!NOTE] 
> 
> UpdateModel() yöntemi, bir form alanının değerini bir özelliğe atama hatası olduğunda, modeldurumuna otomatik olarak hata iletileri ekler. Örneğin, DateTime değerlerini kabul eden bir BirthDate özelliğine "apple" dizesini atamaya çalışırsanız, UpdateModel() yöntemi ModelState'e bir hata ekler.

Listeleme 2'deki değiştirilmiş Oluştur() yöntemi, yeni kişi veritabanına eklenmeden önce İlgili Kişi sınıfının özelliklerini doğrulayan yeni bir bölüm içerir.

**Listeleme 2 - Denetleyiciler\ContactController.cs (Doğrulama ile oluştur)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

Doğrulama bölümü dört farklı doğrulama kuralı uygular:

- FirstName özelliğinin uzunluğu sıfırdan büyük olmalıdır (ve yalnızca boşluklardan oluşamaz)
- Soyadı özelliğinin uzunluğu sıfırdan büyük olmalıdır (ve yalnızca boşluklardan oluşamaz)
- Telefon özelliğinin bir değeri varsa (uzunluğu 0'dan büyükse) Telefon özelliği normal bir ifadeyle eşleşmelidir.
- E-posta özelliğinin bir değeri varsa (uzunluğu 0'dan büyükse) E-posta özelliği normal bir ifadeyle eşleşmelidir.

Doğrulama kuralı ihlali olduğunda, AddModelError() yöntemi yardımıyla ModelState'e bir hata iletisi eklenir. ModelState'e bir ileti eklediğinizde, bir özelliğin adını ve doğrulama hatası iletisinin metnini sağlarsınız. Bu hata iletisi görünümde Html.ValidationSummary() ve Html.ValidationMessage() yardımcı yöntemleri tarafından görüntülenir.

Doğrulama kuralları yürütüldükten sonra, ModelState'in Geçerli özelliği denetlenir. ModelState'e herhangi bir doğrulama hatası iletisi eklendiğinde, Geçerli özellik yanlış döndürür. Doğrulama başarısız olursa, Oluştur formu hata iletileriyle birlikte yeniden görüntülenir.

> [!NOTE] 
> 
> Telefon numarasını ve e-posta adresini normal ifade deposundan doğrulamak için düzenli ifadeler aldım.[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>İşleme Doğrulama Mantığı Ekleme

Edit() eylemi bir Kişi'yi güncelleştirir. Edit() eyleminin Create() eylemiyle tam olarak aynı doğrulamayı gerçekleştirmesi gerekir. Aynı doğrulama kodunu çoğaltmak yerine, Kişi Denetleyicisini hem Oluştur() hem de Edit() eylemlerinin aynı doğrulama yöntemini aramasını sağlayacak şekilde yeniden düzenlememiz gerekir.

Değiştirilmiş Kişi Denetleyicisi sınıfı Listeleme 3'te bulunur. Bu sınıfın hem Create() hem de Edit() eylemleri içinde çağrılan yeni bir ValidateContact() yöntemi vardır.

**Listeleme 3 - Denetleyiciler\ContactController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>Özet

Bu yinelemede, İletişim Yöneticisi uygulamamıza temel form doğrulamayı ekledik. Doğrulama mantığımız, kullanıcıların First Name ve LastName özellikleri için değerler sağlamadan yeni bir kişi göndermesini veya varolan bir ilgili kişi yi düzenlemesini engeller. Ayrıca, kullanıcıların geçerli telefon numaraları ve e-posta adresleri sağlaması gerekir.

Bu yinelemede, Doğrulama mantığını İletişim Yöneticisi uygulamamıza mümkün olan en kolay şekilde ekledik. Ancak doğrulama mantığımızı denetleyici mantığımıza karıştırmak uzun vadede bizim için sorun yaratacaktır. Uygulamamızı korumak ve değiştirmek zaman içinde daha zor olacaktır.

Bir sonraki yinelemede, doğrulama mantığımızı ve veritabanı erişim mantığımızı denetleyicilerimizden yeniden çıkaracağız. Daha gevşek ve daha bakımlı bir uygulama oluşturmamızı sağlamak için çeşitli yazılım tasarım ilkelerinden yararlanacağız.

> [!div class="step-by-step"]
> [Önceki](iteration-2-make-the-application-look-nice-cs.md)
> [Sonraki](iteration-4-make-the-application-loosely-coupled-cs.md)
