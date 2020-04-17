---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 'Yineleme #7 – Ekle Ajax işlevselliği (VB) | Microsoft Dokümanlar'
author: rick-anderson
description: Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: 04eaaa129a56b765c090e64118ed528c65987b50
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542306"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>7. Yineleme – Ajax işlevselliği ekleme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[İndirme Kodu](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> Yedinci yinelemede, Ajax'a destek ekleyerek uygulamamızın duyarlılığını ve performansını artırıyoruz.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC Uygulaması ASP.NET İletişim Yönetimi Oluşturma (VB)

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

İletişim Yöneticisi uygulamasının bu yinelemesinde, Ajax'tan yararlanmak için uygulamamızı yeniden düzenlemeyi yapıyoruz. Ajax'tan yararlanarak uygulamamızı daha duyarlı hale getiriyoruz. Bir sayfada yalnızca belirli bir bölgeyi güncelleştirmemiz gerektiğinde tüm sayfayı işlemekten kaçınabiliriz.

Birisi yeni bir kişi grubu seçtiğinde tüm sayfayı yeniden görüntülememize gerek kalmaması için Dizin görünümümüzü yeniden belirleriz. Bunun yerine, birisi bir kişi grubunu tıklattığında, kişilerin listesini güncelleştireceğiz ve sayfanın geri kalanını rahat bırakacağız.

Silme bağlantımızın çalışma şeklini de değiştireceğiz. Ayrı bir onay sayfası görüntülemek yerine, bir JavaScript onay iletişim kutusu görüntüleriz. Bir ilgili kişi silmek istediğinizi onaylarsanız, kişi kaydını veritabanından silmek için sunucuya karşı bir HTTP DELETE işlemi gerçekleştirilir.

Ayrıca, dizin görünümüne animasyon efektleri eklemek için jQuery'den yararlanacağız. Sunucudan yeni kişi listesi alınırken bir animasyon görüntüleriz.

Son olarak, tarayıcı geçmişini yönetmek için ASP.NET AJAX çerçeve desteğinden yararlanacağız. Kişi listesini güncellemek için bir Ajax çağrısı yaptığımızda tarih puanları oluştururuz. Bu şekilde, tarayıcı geriye ve ileri düğmeleri çalışacaktır.

## <a name="why-use-ajax"></a>Neden Ajax kullanıyorsun?

Ajax kullanmanın birçok faydası vardır. İlk olarak, bir uygulamaya Ajax işlevselliği eklemek daha iyi bir kullanıcı deneyimi sağlar. Normal bir web uygulamasında, bir kullanıcı her eylem gerçekleştirse tüm sayfanın sunucuya geri gönderilmesi gerekir. Bir eylem gerçekleştirdiğiniz zaman, tarayıcı kilitlenir ve kullanıcı sayfanın tamamı getirilip yeniden görüntülenene kadar beklemelidir.

Bu, bir masaüstü uygulaması durumunda kabul edilemez bir deneyim olacaktır. Ama, geleneksel olarak, biz daha iyi yapabileceğini bilmiyordum çünkü bir web uygulaması durumunda bu kötü kullanıcı deneyimi ile yaşadı. Biz, aslında, bizim hayal sadece bir sınırlama olduğu zaman web uygulamaları bir sınırlama olduğunu düşündüm.

Bir Ajax uygulamasında, yalnızca bir sayfayı güncellemek için kullanıcı deneyimini durdurmanız gerekmez. Bunun yerine, sayfayı güncelleştirmek için arka planda eşzamanlı bir istek gerçekleştirebilirsiniz. Sayfanın bir bölümü güncellenirken kullanıcıyı beklemeye zorlayamazsınız.

Ajax'tan yararlanarak uygulamanızın performansını da artırabilirsiniz. İletişim Yöneticisi uygulamasının Ajax işlevi olmadan şu anda nasıl çalıştığını göz önünde bulundurun. Bir kişi grubunu tıklattığınızda, tüm Dizin görünümü yeniden görüntülenmelidir. Kişiler listesi ve kişi grupları listesi veritabanı sunucusundan alınmalıdır. Tüm bu veriler web sunucusundan web tarayıcısına kablo üzerinden geçirilmelidir.

Ancak uygulamamıza Ajax işlevselliğini ekledikten sonra, bir kullanıcı bir kişi grubunu tıklattığında tüm sayfanın yeniden görüntülenmesini önleyebiliriz. Artık veritabanındaki kişi gruplarını almamıza gerek yok. Ayrıca tüm Index görünümünü kablonun ötesine itmemiz gerekmez. Ajax'tan yararlanarak, veritabanı sunucumuzun gerçekleştirmesi gereken iş miktarını azaltıyoruz ve uygulamamızın gerektirdiği ağ trafiği miktarını azaltıyoruz.

## <a name="don-t-be-afraid-of-ajax"></a>Ajax korkmayın

Bazı geliştiriciler, alt düzey tarayıcılar hakkında endişe çünkü Ajax kullanmaktan kaçının. JavaScript'i desteklemeyen bir tarayıcı tarafından erişildiğinde web uygulamalarının çalışmaya devam ettiğinden emin olmak isterler. Ajax JavaScript bağlıdır çünkü, bazı geliştiriciler Ajax kullanmaktan kaçının.

Ancak, Ajax'ı nasıl uyguladığınız konusunda dikkatli olursanız, hem üst düzey hem de alt düzey tarayıcılarla çalışan uygulamalar oluşturabilirsiniz. İletişim Yöneticisi uygulamamız JavaScript'i destekleyen tarayıcılarla ve desteklemeyen tarayıcılarla çalışır.

JavaScript destekleyen bir tarayıcı ile Contact Manager uygulamasını kullanırsanız daha iyi bir kullanıcı deneyimi olacak. Örneğin, bir kişi grubunu tıklattığınızda, yalnızca kişileri görüntüleyen sayfanın bölgesi güncelleştirilir.

Öte yandan, JavaScript'i desteklemeyen (veya JavaScript devre dışı bırakılmış olan) bir tarayıcıyla İletişim Yöneticisi uygulamasını kullanırsanız, daha az arzu edilen bir kullanıcı deneyiminiz olacaktır. Örneğin, bir kişi grubunu tıklattığınızda, eşleşen kişiler listesini görüntülemek için tüm Dizin görünümünün tarayıcıya yeniden nakledilmesi gerekir.

## <a name="adding-the-required-javascript-files"></a>Gerekli JavaScript Dosyalarını Ekleme

Uygulamamıza Ajax işlevselliği eklemek için üç JavaScript dosyası kullanmamız gerekir. Bu dosyaların üçü de yeni bir ASP.NET MVC uygulamasının Scriptler klasöründe yer alıyor.

Ajax'ı uygulamanızda birden fazla sayfada kullanmayı planlıyorsanız, gerekli JavaScript dosyalarını uygulamanızın görünüm ana sayfasına eklemeniz mantıklıdır. Bu şekilde, JavaScript dosyaları uygulamanızdaki tüm sayfalara otomatik olarak dahil edilir.

Görünüm ana sayfanızın baş &lt;&gt; etiketinin içinde yer alan aşağıdaki JavaScript'i ekleyin:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Ajax'ı kullanmak için Dizin Görünümünü Yeniden Düzenleme

Dizin görünümümüzü değiştirerek başlayalım, böylece bir kişi grubunu tıklatarak yalnızca kişileri görüntüleyen görünümün bölgesini güncelleştirir. Şekil 1'deki kırmızı kutu, güncelleştirmek istediğimiz bölgeyi içerir.

[![Yalnızca kişileri güncelleştirme](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**Şekil 01**: Yalnızca kişileri güncelleme ([Tam boyutlu görüntüyü görüntülemek için tıklayınız](iteration-7-add-ajax-functionality-vb/_static/image2.png))

İlk adım, görünümün eşit olarak güncelleştirmek istediğimiz kısmını ayrı bir kısmi (görünüm kullanıcı denetimi) olarak ayırmaktır. Dizin görünümünün kişiler tablosunu görüntüleyen bölümü Listeleme 1'de kısmi olarak taşındı.

**Listeleme 1 - Görünümler\İletişim\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

Listeleme 1'deki kısmi modelin Dizin görünümünden farklı bir modele sahip olduğuna dikkat edin. %@ Sayfa %&gt; &lt;yönergesinde *devralınan* öznitelik, kısmi mirasın&lt;ViewUserControl&gt; Group sınıfından devraldığı belirtilir.

Güncelleştirilmiş Dizin görünümü Listeleme 2'de bulunur.

**Listeleme 2 - Görünümler\İletişim\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

Listeleme 2'deki güncelleştirilmiş görünüm hakkında dikkat etmelisiniz iki şey vardır. İlk olarak, kısmi olarak taşınan içeriğin tamamının Html.RenderPartial() çağrısıyla değiştirilmeye dikkat edin. İlk kişi kümesini görüntülemek için Dizin görünümü ilk istendiğinde Html.RenderPartial() yöntemi çağrılır.

İkinci olarak, kişi gruplarını görüntülemek için kullanılan Html.ActionLink() yerine bir Ajax.ActionLink() ile değiştirildiğini unutmayın. Ajax.ActionLink() aşağıdaki parametrelerle çağrılır:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

İlk parametre bağlantı için görüntülenecek metni, ikinci parametre rota değerlerini, üçüncü parametre ise Ajax seçeneklerini temsil eder. Bu durumda, Ajax isteği tamamlandıktan sonra güncelleştirmek &lt;istediğimiz&gt; HTML div etiketini belirtmek için UpdateTargetId Ajax seçeneğini kullanırız. Div &lt;&gt; etiketini yeni kişi listesiyle güncelleştirmek istiyoruz.

İlgili Kişi denetleyicisinin güncelleştirilmiş Index() yöntemi Listeleme 3'te bulunur.

**Listeleme 3 - Denetleyiciler\ContactController.vb (Dizin yöntemi)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

Güncelleştirilmiş Index() eylemi koşullu olarak iki şeyden birini döndürür. Index() eylemi bir Ajax isteği tarafından çağrılırsa, denetleyici kısmi olarak döndürür. Aksi takdirde, Index() eylemi tüm görünümü döndürür.

Bir Ajax isteği tarafından çağrıldığınızda Index() eyleminin bu kadar çok veri döndürmesine gerek olmadığını unutmayın. Normal bir istek bağlamında, Dizin eylemi tüm kişi gruplarının ve seçili kişi grubunun listesini döndürür. Bir Ajax isteği bağlamında, Index() eylemi yalnızca seçilen grubu döndürür. Ajax veritabanı sunucunuzda daha az çalışma anlamına gelir.

Modifiye Dizin görünümümüz hem üst düzey hem de alt düzey tarayıcılarda çalışır. Bir kişi grubunu tıklatırsanız ve tarayıcınız JavaScript'i destekliyorsa, yalnızca kişi listesini içeren görünüm bölgesi güncelleştirilir. Diğer taraftan, tarayıcınız JavaScript'i desteklemiyorsa, tüm görünüm güncelleştirilir.

Güncelleştirilmiş Dizin görünümümüzün bir sorunu var. Bir kişi grubunu tıklattığınızda, seçili grup vurgulanmaz. Grup listesi, Bir Ajax isteği sırasında güncelleştirilen bölgenin dışında görüntülendiğinden, doğru grup vurgulanmaz. Bu sorunu bir sonraki bölümde gidereceğiz.

## <a name="adding-jquery-animation-effects"></a>jQuery Animasyon Efektleri Ekleme

Normalde, bir web sayfasındaki bir bağlantıyı tıklattığınızda, tarayıcının güncelleştirilmiş içeriği etkin olarak alıp almadığını algılamak için tarayıcı ilerleme çubuğunu kullanabilirsiniz. Bir Ajax isteği gerçekleştirirken, diğer taraftan, tarayıcı ilerleme çubuğu herhangi bir ilerleme göstermez. Bu, kullanıcıları tedirgin edebilir. Tarayıcının donup donmadığını nasıl anlarsınız?

Bir Kullanıcıya, Bir Ajax isteği gerçekleştirirken çalışmanın gerçekleştirildiğini gösterebileceğiniz birkaç yol vardır. Bir yaklaşım basit bir animasyon görüntülemektir. Örneğin, bir Ajax isteği başladığında bir bölge solabilir ve istek tamamlandığında bölgede solmaya.

Animasyon efektleri oluşturmak için Microsoft ASP.NET MVC çerçevesine dahil olan jQuery kitaplığını kullanacağız. Güncelleştirilmiş Dizin görünümü Listeleme 4'te bulunur.

**Listeleme 4 - Görünümler\İletişim\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

Güncelleştirilmiş Dizin görünümünde üç yeni JavaScript işlevi bulunduğuna dikkat edin. İlk iki işlev, yeni bir kişi grubunu tıklattığınızda kişi listesinde solup gitmek için jQuery'yi kullanır. Üçüncü işlev, Bir Ajax isteği bir hatayla sonuçlandığında (örneğin, ağ zaman sonu) bir hata iletisi görüntüler.

İlk işlev, seçili grubu vurgulamayı da önemser. Bir sınıf= seçili öznitelik tıklanan öğenin üst öğe (LI öğesi) eklenir. Yine, jQuery kolay doğru öğeyi seçmek ve CSS sınıfı eklemek yapar.

Bu komut dosyaları Ajax.ActionLink() AjaxOptions parametresi yardımıyla grup bağlantılarına bağlıdır. Güncelleştirilmiş Ajax.ActionLink() yöntem çağrısı aşağıdaki gibi görünür:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Tarayıcı Geçmişi Desteği Ekleme

Normalde, bir sayfayı güncelleştirmek için bir bağlantıyı tıklattığınızda, tarayıcı geçmişiniz güncelleştirilir. Bu şekilde, sayfanın önceki durumuna zamanda geri dönmek için tarayıcı geri düğmesini tıklatabilirsiniz. Örneğin, Arkadaşlar kişi grubunu tıklatıp İş kişi grubunu tıklatırsanız, Arkadaşlar kişi grubu seçildiğinde sayfanın durumuna geri dönmek için tarayıcıyı Geri Al düğmesini tıklatabilirsiniz.

Ne yazık ki, Bir Ajax isteği gerçekleştirmek tarayıcı geçmişini otomatik olarak güncelleştirmez. Bir kişi grubunu tıklatırsanız ve eşleşen kişilerin listesi Bir Ajax isteğiyle birlikte alınırsa, tarayıcı geçmişi güncelleştirilmeyecektir. Yeni bir kişi grubu seçtikten sonra bir kişi grubuna geri dönmek için tarayıcı Yı kullanabilirsiniz.

Kullanıcıların Ajax isteklerini yerine getirttikten sonra tarayıcı geri düğmesini kullanabilmelerini istiyorsanız, o zaman biraz daha çalışmanız gerekir. ASP.NET AJAX Framework'de yerleşik tarayıcı geçmişi yönetimi işlevinden yararlanmanız gerekir.

ASP.NET AJAX tarayıcı geçmişi, üç şey yapmanız gerekir:

1. EnableBrowserHistory özelliğini doğru ayarlayarak Tarayıcı Geçmişini etkinleştirin.
2. View'ın durumu addHistoryPoint() yöntemini arayarak görünüm durumu değiştiğinde geçmiş noktalarını kaydedin.
3. Gezinme olayı yükseltildiğinde görünümün durumunu yeniden oluştur.

Güncelleştirilmiş Dizin görünümü Listeleme 5'te bulunur.

**Listeleme 5 - Görünümler\İletişim\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

Listeleme 5'te Tarayıcı Geçmişi pageInit() işlevinde etkinleştirilir. PageInit() işlevi, gezinme olayı için olay işleyicisini ayarlamak için de kullanılır. Tarayıcı İleri veya Geri düğmesi sayfanın durumunun değişmesine neden olduğunda gezinme olayı yükseltilir.

Bir kişi grubunu tıklattığınızda beginContactList() yöntemi çağrılır. Bu yöntem, addHistoryPoint() yöntemini çağırarak yeni bir geçmiş noktası oluşturur. Tıklanan kişi grubunun kimliği geçmişe eklenir.

Grup kimliği, kişi grubu bağlantısındaki bir expando özniteliğinden alınır. Bağlantı, Ajax.ActionLink() için aşağıdaki çağrı ile işlenir.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

Ajax.ActionLink() geçirilen son parametre bağlantıya groupid adlı bir expando özniteliği ekler (XHTML uyumluluğu için küçük harf).

Bir kullanıcı tarayıcıyı Geri veya İleri düğmesine bastığında, gezinme olayı yükseltilir ve gezinme() yöntemi çağrılır. Bu yöntem, gezinme yöntemine geçirilen tarayıcı geçmişi noktasına karşılık gelen sayfanın durumuyla eşleşecek şekilde sayfada görüntülenen kişileri güncelleştirir.

## <a name="performing-ajax-deletes"></a>Performans Ajax Siler

Şu anda, bir kişi silmek için Sil bağlantısını tıklatıp silme onay sayfasında görüntülenen Sil düğmesini tıklatmanız gerekir (Bkz. Şekil 2). Bu, veritabanı kaydını silerken gibi basit bir şey yapmak için çok fazla sayfa isteği gibi görünüyor.

[![Silme onay sayfası](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**Şekil 02**: Sil onay sayfası([Tam boyutlu resmi görüntülemek için tıklayınız](iteration-7-add-ajax-functionality-vb/_static/image4.png))

Silme onay sayfasını atlamak ve bir ilgili kişi doğrudan Index görünümünden silmek caziptir. Bu uygulamayı alarak güvenlik deliklerine uygulamanızı açar, çünkü bu ayartma kaçınmalısınız. Genel olarak, web uygulamanızın durumunu değiştiren bir eylem çağırırken BIR HTTP GET işlemi gerçekleştirmek istemezsiniz. Silme işlemi gerçekleştirirken, bir HTTP POST veya daha iyisi bir HTTP DELETE işlemi gerçekleştirmek istiyorsunuz.

Sil bağlantısı, Kişi Listesi'nde kısmi olarak yer almaktadır. List kısmi'in güncelleştirilmiş bir sürümü List 6'da bulunur.

**Listeleme 6 - Görünümler\İletişim\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

Sil bağlantısı, Ajax.ImageActionLink() yöntemine aşağıdaki çağrı ile işlenir:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink() ASP.NET MVC çerçevesinin standart bir parçası değildir. Ajax.ImageActionLink() İletişim Yöneticisi projesinde yer alan özel bir yardımcı yöntemidir.

AjaxOptions parametresi iki özellime sahiptir. İlk olarak, Bir açılır JavaScript onay iletişim kutusunu görüntülemek için Onay özelliği kullanılır. İkinci olarak, HttpMethod özelliği bir HTTP DELETE işlemi gerçekleştirmek için kullanılır.

Listeleme 7, İletişim denetleyicisine eklenen yeni bir AjaxDelete() eylemi içerir.

**Listeleme 7 - Denetleyiciler\ContactController.vb (AjaxDelete)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete() eylemi AcceptVerbs özelliği ile dekore edilmiştir. Bu öznitelik, http delete işlemi dışında herhangi bir HTTP işlemi dışında eylemin çağrılmasını önler. Özellikle, bir HTTP GET ile bu eylemi başlatamazsınız.

Veritabanı kaydını sildikten sonra, silinen kaydı içermeyen kişilerin güncelleştirilmiş listesini görüntülemeniz gerekir. AjaxDelete() yöntemi, Kişiler Listesi'ni ve güncelleştirilmiş kişi listesini verir.

## <a name="summary"></a>Özet

Bu yinelemede, İletişim Yöneticisi uygulamamıza Ajax işlevselliğini ekledik. Uygulamamızın duyarlılığını ve performansını artırmak için Ajax'ı kullandık.

İlk olarak, bir kişi grubunu tıklatmanın tüm görünümü güncelleştirmemesi için Dizin görünümünü yeniden düzenlemedik. Bunun yerine, bir kişi grubunu tıklattığınızda yalnızca kişiler listesini güncelleştirir.

Daha sonra, kişiler listesinde solmaya ve solmaya jQuery animasyon efektleri kullandı. Bir Ajax uygulamasına animasyon eklemek, uygulama kullanıcılarına tarayıcı ilerleme çubuğuna eşdeğer bir çubuk sağlamak için kullanılabilir.

Ayrıca Ajax uygulamamıza tarayıcı geçmişi desteği ekledik. Kullanıcıların Dizin görünümünün durumunu değiştirmek için tarayıcıyı İleri ve İleri düğmelerini tıklatmalarını sağladık.

Son olarak, HTTP DELETE işlemlerini destekleyen bir silme bağlantısı oluşturduk. Ajax silmeleri gerçekleştirerek, kullanıcıların kullanıcının ek bir silme onay sayfası istemesine gerek kalmadan veritabanı kayıtlarını silmelerini sağlarız.

> [!div class="step-by-step"]
> [Önceki](iteration-6-use-test-driven-development-vb.md)
