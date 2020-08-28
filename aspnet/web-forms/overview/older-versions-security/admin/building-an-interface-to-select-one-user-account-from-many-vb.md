---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: Birden çok kullanıcı hesabını seçmek için arabirim oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, sayfalandırılmış, filtrelenebilir bir kılavuza sahip bir kullanıcı arabirimi oluşturacağız. Özellikle Kullanıcı arabirimimiz, için bir dizi bağlantı düğmesinden oluşur...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044590"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>Çok Sayıda Kullanıcı Hesabından Birinin Seçilmesi için Bir Arabirim Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> Bu öğreticide, sayfalandırılmış, filtrelenebilir bir kılavuza sahip bir kullanıcı arabirimi oluşturacağız. Özellikle Kullanıcı arabirimimiz, Kullanıcı arabiriminin başlangıç harfine ve eşleşen kullanıcıları göstermek için bir GridView denetimine göre sonuçlara filtre uygulamak için bir dizi bağlantı düğmesinden oluşur. Bir GridView içindeki tüm Kullanıcı hesaplarını listeleyerek başlayacağız. Daha sonra 3. adımda filtre LinkButtons ' ı ekleyeceğiz. 4. adım filtrelenmiş sonuçları sayfalama konusunda arar. 2 ila 4. adımlarda oluşturulan arabirim, sonraki öğreticilerde belirli bir kullanıcı hesabı için yönetim görevlerini gerçekleştirmek üzere kullanılacaktır.

## <a name="introduction"></a>Giriş

<a id="_msoanchor_1"></a> [*Kullanıcılara roller atama*](../roles/assigning-roles-to-users-vb.md) öğreticisinde, bir yöneticinin Kullanıcı seçmesini ve rollerini yönetmesi için bir ilkel arabirimi oluşturduk. Özellikle, arabirim yöneticiye tüm kullanıcıların bir açılan listesini sundu. Bu tür bir arabirim, bir düzine veya So Kullanıcı hesabı olduğunda ve yüzlerce ya da binlerce hesabı olan siteler için çok uygun olduğunda uygundur. Sayfalandırılmış, filtrelenebilir bir ızgara, büyük Kullanıcı temellerine sahip Web siteleri için daha uygun bir kullanıcı arabirimidir.

Bu öğreticide, böyle bir kullanıcı arabirimi oluşturacağız. Özellikle Kullanıcı arabirimimiz, Kullanıcı arabiriminin başlangıç harfine ve eşleşen kullanıcıları göstermek için bir GridView denetimine göre sonuçlara filtre uygulamak için bir dizi bağlantı düğmesinden oluşur. Bir GridView içindeki tüm Kullanıcı hesaplarını listeleyerek başlayacağız. Daha sonra 3. adımda filtre LinkButtons ' ı ekleyeceğiz. 4. adım filtrelenmiş sonuçları sayfalama konusunda arar. 2 ila 4. adımlarda oluşturulan arabirim, sonraki öğreticilerde belirli bir kullanıcı hesabı için yönetim görevlerini gerçekleştirmek üzere kullanılacaktır.

Haydi başlayalım!

## <a name="step-1-adding-new-aspnet-pages"></a>1. Adım: yeni ASP.NET sayfaları ekleme

Bu öğreticide ve sonraki iki adım, yönetimle ilgili çeşitli işlevler ve yetenekler inceliyoruz. Bu öğreticiler genelinde incelenen konuları uygulamak için bir dizi ASP.NET sayfasına ihtiyacımız olacak. Bu sayfaları oluşturalım ve site haritasını güncelleştirlim.

Adlı projede yeni bir klasör oluşturarak başlayın `Administration` . Sonra, klasöre iki yeni ASP.NET sayfası ekleyerek her bir sayfayı `Site.master` ana sayfayla bağlantılandırın. Sayfaları adlandırın:

- `ManageUsers.aspx`
- `UserInformation.aspx`

Ayrıca, Web sitesinin kök dizinine iki sayfa ekleyin: `ChangePassword.aspx` ve `RecoverPassword.aspx` .

Bu dört sayfa, her ana sayfanın Contenttutucuları için bir tane olmak üzere iki Içerik denetimine sahip olmalıdır: `MainContent` ve `LoginContent` .

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

Bu sayfaların ContentPlaceHolder için ana sayfanın varsayılan işaretlemesini göstermek istiyoruz `LoginContent` . Bu nedenle, içerik denetimi için bildirim temelli biçimlendirmeyi kaldırın `Content2` . Bunu yaptıktan sonra, sayfaların biçimlendirmesi yalnızca bir Içerik denetimi içermelidir.

Klasöründeki ASP.NET sayfaları `Administration` yalnızca yönetim kullanıcılarına yöneliktir. <a id="_msoanchor_2"></a> [*Rol oluşturma ve yönetme*](../roles/creating-and-managing-roles-vb.md) öğreticisinde sisteme bir Yöneticiler rolü ekledik, bu iki sayfaya erişimi bu rolle kısıtlayın. Bunu gerçekleştirmek için, klasöre bir `Web.config` dosya ekleyin `Administration` ve kendi `<authorization>` öğesini Yöneticiler rolündeki kullanıcıları kabul olarak yapılandırın ve diğerlerini reddedin.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

Bu noktada, projenizin Çözüm Gezgini Şekil 1 ' de gösterilen ekran görüntüsüne benzer olması gerekir.

[![Web sitesine dört yeni sayfa ve bir Web.config dosyası eklenmiştir](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**Şekil 1**: Web sitesine dört yeni sayfa ve bir `Web.config` dosya eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))

Son olarak, site haritasını ( `Web.sitemap` ) sayfaya bir giriş içerecek şekilde güncelleştirin `ManageUsers.aspx` . `<siteMapNode>`Rol öğreticileri için eklendiğimiz sonra AŞAĞıDAKI XML 'i ekleyin.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

Site Haritası güncelleştirildikten sonra, siteyi bir tarayıcı aracılığıyla ziyaret edin. Şekil 2 ' de gösterildiği gibi, sol taraftaki Gezinti artık yönetim öğreticilerinin öğelerini içerir.

[![Site Haritası Kullanıcı Yönetimi başlıklı bir düğüm Içerir](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**Şekil 2**: site haritası Kullanıcı Yönetimi başlıklı bir düğüm içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>2. Adım: GridView 'da tüm Kullanıcı hesaplarını listeleme

Bu öğreticide Son hedefiniz, yöneticinin yönetmek üzere bir kullanıcı hesabı seçebileceği, sayfalandırılmış, filtrelenebilir bir kılavuz oluşturmaktır. Bir GridView içindeki *Tüm* kullanıcıları listeleyerek başlayalım. Bu işlem tamamlandıktan sonra filtreleme ve sayfalama arabirimlerini ve işlevselliğini ekleyeceğiz.

`ManageUsers.aspx` `Administration` Klasörü klasörde açın ve bir GridView ekleyin ve bir GridView ekleyin, bu `ID` , `UserAccounts` sınıfının metodunu kullanarak Kullanıcı hesapları kümesini GridView 'a bağlamak için kod yazacağız `Membership` `GetAllUsers` . Önceki öğreticilerde anlatıldığı gibi, `GetAllUsers` yöntemi nesne `MembershipUserCollection` koleksiyonu olan bir nesnesi döndürür `MembershipUser` . Koleksiyondaki her biri,,, vb `MembershipUser` . gibi özellikleri içerir `UserName` `Email` `IsApproved` .

GridView 'da istenen kullanıcı hesabı bilgilerini göstermek için, GridView 'un özelliğini false olarak ayarlayın ve,, ve özellikleri için,, `AutoGenerateColumns` `UserName` `Email` ve `Comment` özellikleri ve Checkboxfields için `IsApproved` `IsLockedOut` boundfields alanları ekleyin `IsOnline` . Bu yapılandırma, denetimin bildirim temelli biçimlendirmesi veya alanlar iletişim kutusu aracılığıyla uygulanabilir. Şekil 3 ' te alanları otomatik oluştur onay kutusunun işaretlendiğine ve BoundFields ve CheckBoxFields eklendikten ve yapılandırıldıktan sonra Fields iletişim kutusunun ekran görüntüsü gösterilir.

[![GridView 'a üç BoundFields ve üç CheckBoxFields ekleyin](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**Şekil 3**: GridView 'A üç boundfields ve üç CheckBoxField ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))

GridView 'nizi yapılandırdıktan sonra, bildirim temelli biçimlendirmesinin aşağıdakine benzer olduğundan emin olun:

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

Sonra, Kullanıcı hesaplarını GridView 'a bağlayan bir kod yazmamız gerekir. `BindUserAccounts`Bu görevi gerçekleştirmek için adlı bir yöntem oluşturun ve ardından `Page_Load` ilk sayfada ziyaret eden olay işleyicisinden onu çağırın.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

Sayfayı bir tarayıcı ile test etmek için bir dakikanızı ayırın. Şekil 4 ' ün gösterdiği gibi, `UserAccounts` GridView, sistemdeki tüm kullanıcılar için Kullanıcı adını, e-posta adresini ve diğer ilgili hesap bilgilerini listeler.

[![Kullanıcı hesapları GridView 'da listelenir](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**Şekil 4**: Kullanıcı hesapları GridView 'da listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>3. Adım: sonuçları Kullanıcı adının Ilk harfine göre filtreleme

Şu anda `UserAccounts` GridView *Tüm* Kullanıcı hesaplarını gösterir. Yüzlerce veya binlerce kullanıcı hesabına sahip Web siteleri için, kullanıcının görüntülenen hesapları hızla çözebilmesi zorunludur. Bu, sayfaya filtreleme bağlantı düğmeleri eklenerek gerçekleştirilebilir. Sayfaya 27 LinkButton ekleyelim: her bir alfabede her bir harf için tek bir LinkButton ile birlikte başlıklı bir. Ziyaretçi tüm LinkButton düğmesine tıkladığında, GridView tüm kullanıcıları gösterir. Belirli bir harfe tıkladıklarında, yalnızca Kullanıcı adı seçili harfle başlayan kullanıcılar görüntülenir.

İlk göreviniz, 27 LinkButton denetimlerini eklemektir. Tek bir seçenek, her seferinde bir tane olmak üzere 27 LinkButtons 'ı bildirimli olarak oluşturmaktır. Daha esnek bir yaklaşım, bir `ItemTemplate` bağlantı düğmesini işleyen ve sonra filtreleme seçeneklerini bir dizi olarak yineleyicisi 'ne bağlayan bir yineleyici denetimi kullanmaktır `String` .

GridView 'un üzerindeki sayfaya bir yineleyici denetimi ekleyerek başlayın `UserAccounts` . Yineleyicisi 'nin `ID` `FilteringUI` şablonunu, `ItemTemplate` `Text` ve `CommandName` özellikleri geçerli dizi öğesine bağlanan bir LinkButton öğesi olacak şekilde yapılandırmak için, Repeater 'ın özelliğini ayarlayın. <a id="_msoanchor_3"></a> [*Kullanıcılara roller atama*](../roles/assigning-roles-to-users-vb.md) öğreticisinde gördüğünüz gibi, bu, `Container.DataItem` veri bağlama söz dizimi kullanılarak gerçekleştirilebilir. `SeparatorTemplate`Her bağlantı arasında dikey bir çizgi göstermek Için Yineleyici ' i kullanın.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

Bu yineleyicisi istenen filtreleme seçenekleriyle doldurmak için adlı bir yöntem oluşturun `BindFilteringUI` . İlk sayfa yükünde olay işleyicisinden bu yöntemi çağırdığınızdan emin olun `Page_Load` .

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

Bu yöntem, filtre seçeneklerini `String` `filterOptions` dizideki her öğe için dizideki öğeler olarak belirtir, Repeater, `Text` ve `CommandName` özellikleri dizi öğesinin değerine atanmış bir LinkButton öğesini işleyecek.

Şekil 5 ' te `ManageUsers.aspx` bir tarayıcıdan görüntülendiklerinde sayfa gösterilir.

[![Yineleyici, 27 filtreleme bağlantı düğmelerini listeler](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**Şekil 5**: Yineleyici, 27 filtreleme bağlantı düğmelerini listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))

> [!NOTE]
> Kullanıcı adları, sayılar ve noktalama işaretleri de dahil olmak üzere herhangi bir karakterle başlayabilir. Bu hesapları görüntülemek için, yöneticinin tüm LinkButton seçeneğini kullanması gerekir. Alternatif olarak, bir sayıyla başlayan tüm Kullanıcı hesaplarını döndürmek için bir LinkButton ekleyebilirsiniz. Bunu okuyucu için bir alıştırma olarak bırakıyorum.

Filtreleme bağlantı düğmelerinden herhangi birine tıkladığınızda geri göndermeye neden olur ve yineleyicisi 'nin `ItemCommand` olayı yükseltilir, ancak sonuçları filtrelemek için herhangi bir kod yazdığımızda kılavuzda değişiklik yapılmaz. Sınıfı, Kullanıcı `Membership` adı belirtilen arama düzeniyle eşleşen bu kullanıcı hesaplarını döndüren bir [ `FindUsersByName` yöntemi](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) içerir. Kullanıcı adları, `CommandName` tıklanan filtrelenmiş LinkButton tarafından belirtilen harfle başlayan yalnızca Kullanıcı hesaplarını almak için bu yöntemi kullanabiliriz.

`ManageUser.aspx`Bu özellik adlı bir özellik içermesi adına sayfanın arka plan kod sınıfını güncelleştirerek başlayın `UsernameToMatch` :

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch`Özelliği, `ViewState` ' usernameToMatch ' anahtarı kullanılarak koleksiyona atanan değerini depolar. Bu özelliğin değeri okundu ise, koleksiyonda bir değer olup olmadığını kontrol eder `ViewState` ; Aksi takdirde, varsayılan değeri boş bir dize döndürür. Özelliği `UsernameToMatch` ortak bir model sergiler, yani özellikte yapılan herhangi bir değişiklik geri göndermeler arasında kalıcı hale gelecek şekilde durumu görüntülemek için bir değeri kalıcı hale getiren. Bu düzenle ilgili daha fazla bilgi için, [ASP.net görünüm durumunu anlama](https://msdn.microsoftn-us/library/ms972976.aspx)konusunu okuyun.

Daha sonra, `BindUserAccounts` yöntemini çağırmak yerine, `Membership.GetAllUsers` `Membership.FindUsersByName` `UsernameToMatch` SQL joker karakteri% olan bir özellik değerini çağırarak çağrı yapmak yerine,

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

Yalnızca Kullanıcı adı A harfiyle başlayan kullanıcıları görüntülemek için, `UsernameToMatch` özelliğini bir olarak ayarlayın ve sonra `BindUserAccounts` Bu `Membership.FindUsersByName("A%")` , Kullanıcı adı ile başlayan tüm kullanıcıları döndürecek bir çağrısına yol açar. benzer şekilde, *Tüm* kullanıcıları döndürmek için, `UsernameToMatch` metodun, `BindUserAccounts` tüm Kullanıcı hesaplarını döndürecek şekilde özelliğe boş bir dize atayın `Membership.FindUsersByName("%")` .

Yineleyici olayı için bir olay işleyicisi oluşturun `ItemCommand` . Bu olay, filtre bağlantı düğmelerinden birine tıklandığında tetiklenir; nesne aracılığıyla tıklanmış LinkButton değeri geçirilir `CommandName` `RepeaterCommandEventArgs` . Özelliğe uygun değeri atamız `UsernameToMatch` ve sonra yöntemini çağırmanız gerekir `BindUserAccounts` . Tümü ise `CommandName` , `UsernameToMatch` tüm Kullanıcı hesaplarının görüntülenmesi için boş bir dize atayın. Aksi takdirde, `CommandName` değeri ata `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

Bu kod yerine, filtreleme işlevini test edin. Sayfa ilk kez ziyaret edildiğinde, tüm Kullanıcı hesapları görüntülenir (bkz. Şekil 5 ' e geri bakın). LinkButton öğesine tıkladığınızda geri göndermeye neden olur ve sonuçları filtreleyerek yalnızca ile başlayan Kullanıcı hesapları görüntüleniyor.

[![Kullanıcı adı belirli bir harfle başlayan kullanıcıları görüntülemek için filtreleme bağlantı düğmelerini kullanın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**Şekil 6**: Kullanıcı adı belirli bir harfle başlayan kullanıcıları görüntülemek Için filtreleme bağlantı düğmelerini kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))

## <a name="step-4-updating-the-gridview-to-use-paging"></a>4. Adım: GridView 'ı sayfalama kullanacak şekilde güncelleştirme

Şekil 5 ve 6 ' da gösterilen GridView, yöntemden döndürülen tüm kayıtları listeler `FindUsersByName` . Yüzlerce veya binlerce kullanıcı hesabı varsa, bu, tüm hesapların (tüm bağlantı düğmesine tıklanması veya ilk kez ziyaret edildiğinde olduğu gibi) görüntülenirken bilgi yüküne yol açabilir. Kullanıcı hesaplarını daha yönetilebilir parçalara sunma konusunda yardımcı olmak için GridView 'u aynı anda 10 Kullanıcı hesabı görüntüleyecek şekilde yapılandıralim.

GridView denetimi iki tür sayfalama sunar:

- **Varsayılan disk belleği** kullanımı kolay, ancak verimsiz. Bir Nutshell 'de, varsayılan sayfalama ile GridView, veri kaynağından *Tüm* kayıtları bekler. Daha sonra yalnızca uygun kayıt sayfasını görüntüler.
- **Özel disk belleği** -uygulamak için daha fazla iş gerektirir, ancak özel sayfalama ile veri kaynağı, görüntülenecek yalnızca kesin kayıt kümesini iade ettiğinden varsayılan sayfalama daha etkilidir.

Varsayılan ve özel sayfalama arasındaki performans farkı, binlerce kayıt üzerinde sayfalama yaparken oldukça önemli olabilir. Yüzlerce veya binlerce kullanıcı hesabı olabileceğini varsayarak bu arabirimi oluşturduğumuz için özel sayfalama kullanalım.

> [!NOTE]
> Varsayılan ve özel sayfalama arasındaki farklar hakkında daha kapsamlı bir tartışma ve özel sayfalama uygulama Ile ilgili güçlükler için, [büyük miktarlarda veri aracılığıyla verimli sayfalama](https://asp.net/learn/data-access/tutorial-25-vb.aspx)bölümüne bakın. Varsayılan ve özel sayfalama arasındaki performans farkının bazı analizine ilişkin bazı analizler için, bkz. [ASP.net 'de özel sayfalama SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx).

Özel sayfalama uygulamak için öncelikle GridView tarafından görüntülenmekte olan kayıtların kesin alt kümesini almak için bazı mekanizmaya ihtiyacımız vardır. İyi haber, `Membership` sınıfın `FindUsersByName` yönteminin, sayfa dizinini ve sayfa boyutunu belirtmemizi ve yalnızca bu kayıt aralığı içinde yer alan Kullanıcı hesaplarını döndürmemize olanak sağlar.

Özellikle, bu aşırı yükleme aşağıdaki imzaya sahiptir: [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) .

*PageIndex* parametresi döndürülecek Kullanıcı hesaplarının sayfasını belirtir; *PageSize* , sayfa başına görüntülenecek kayıt sayısını belirtir. *TotalRecords* parametresi, `ByRef` Kullanıcı deposundaki Toplam Kullanıcı hesabı sayısını döndüren bir parametredir.

> [!NOTE]
> Tarafından döndürülen veriler `FindUsersByName` Kullanıcı adına göre sıralanır; sıralama ölçütü özelleştirilemez.

GridView, yalnızca bir ObjectDataSource denetimine bağlandığında özel sayfalama kullanacak şekilde yapılandırılabilir. ObjectDataSource denetiminin özel sayfalama uygulaması için iki yöntem gerekir: bir başlangıç satırı dizini ve görüntülenecek en fazla kayıt sayısı ve bu yayılma dahilinde kalan kayıtların kesin alt kümesini döndürür. ve üzerinde disk belleğine alınan toplam kayıt sayısını döndüren bir yöntem. `FindUsersByName`Aşırı yükleme bir sayfa dizinini ve sayfa boyutunu kabul eder ve bir parametre üzerinden toplam kayıt sayısını döndürür `ByRef` . Burada bir arabirim uyumsuzluğu var.

Bir seçenek, ObjectDataSource 'un beklediği arabirimi kullanıma sunan bir proxy sınıfı oluşturmak ve sonra yöntemi dahili olarak çağırıyorsa `FindUsersByName` . Diğer bir seçenek ve bu makale için kullanacağımız şey, kendi sayfalama arabirimimizi oluşturmak ve GridView 'ın yerleşik sayfalama arabirimi yerine bunu kullanmaktır.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>Birinci, önceki, sonraki, son sayfalama arabirimi oluşturma

Ilk, önceki, sonraki ve son LinkButtons ile bir sayfalama arabirimi oluşturalım. Ilk LinkButton tıklandığında, Kullanıcı ilk veri sayfasına götürür, ancak önceki sayfaya geri dönecektir. Benzer şekilde, Ileri ve son, kullanıcıyı sırasıyla sonraki ve son sayfaya taşıyacaktır. GridView 'un altına dört LinkButton denetimini ekleyin `UserAccounts` .

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

Ardından, LinkButton 'ın olaylarının her biri için bir olay işleyicisi oluşturun `Click` .

Şekil 7 ' de, Visual Web Developer Tasarım görünümü ile görüntülendiğinde dört LinkButton gösterilmektedir.

[![GridView 'un altına Ilk, önceki, Next ve son LinkButtons ekleyin](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**Şekil 7**: GridView 'un altına Ilk, önceki, Next ve son linkbuttons ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))

### <a name="keeping-track-of-the-current-page-index"></a>Geçerli sayfa dizinini takip tutma

Bir Kullanıcı sayfayı ilk kez ziyaret ettiğinde `ManageUsers.aspx` veya filtre düğmelerinden birine tıkladığında, GridView 'daki ilk veri sayfasını göstermek istiyoruz. Ancak Kullanıcı, gezinti bağlantı düğmelerinden birine tıkladığında sayfa dizinini güncelleştirmemiz gerekir. Sayfa dizinini ve sayfa başına görüntülenecek kayıt sayısını korumak için, sayfanın arka plan kod sınıfına aşağıdaki iki özelliği ekleyin:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

Özelliği gibi `UsernameToMatch` , özelliği de `PageIndex` durumunu görüntülemek için değerini sürdürür. Salt okunurdur `PageSize` özelliği, sabit kodlanmış bir değer olan 10 ' u döndürür. İlgili okuyucuyu, bu özelliği aynı kalıbı kullanacak şekilde güncelleştirmek için davet ediyorum ve sayfayı, sayfayı `PageIndex` `ManageUsers.aspx` ziyaret eden kişinin sayfa başına kaç Kullanıcı hesabı görüntülemesi gerektiğini belirtebilir.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>Yalnızca geçerli sayfanın kayıtlarını alma, sayfa dizinini güncelleştirme ve sayfalama arabirimi LinkButtons 'ı etkinleştirme ve devre dışı bırakma

Sayfalama arabirimi yerinde ve `PageIndex` ve `PageSize` özellikleri eklendiğinde, `BindUserAccounts` yöntemi uygun aşırı yüklemeyi kullanacak şekilde güncelleştirmeye hazırız `FindUsersByName` . Ayrıca, hangi sayfanın görüntülendiğine bağlı olarak, bu yöntemin sayfalama arabirimini etkinleştirmesi veya devre dışı bırakmakta olmaları gerekir. Verilerin ilk sayfasını görüntülerken, Ilk ve önceki bağlantıların devre dışı bırakılması gerekir; Son sayfa görüntülenirken sonraki ve sonuncu devre dışı bırakılmalıdır.

`BindUserAccounts`Yöntemi aşağıdaki kodla güncelleştirin:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

Disk belleğine alınan toplam kayıt sayısının, metodun son parametresine göre belirlendiğini unutmayın `FindUsersByName` . Belirtilen kullanıcı hesapları sayfası döndürüldüğünde, verilerin ilk veya son sayfasının görüntülenip görüntülenmediğine bağlı olarak dört bağlantı düğmesi etkinleştirilir veya devre dışı bırakılır.

Son adım dört LinkButtons olay işleyicisi için kod yazmaktır `Click` . Bu olay işleyicilerinin, `PageIndex` özelliği güncelleştirmesi ve ardından `BindUserAccounts` Ilk, önceki ve sonraki olay işleyicilerinin bir çağrı yoluyla verileri GridView 'da yeniden bağlamasını gerekir. Son `Click` LinkButton için olay işleyicisi, son sayfa dizinini belirleyebilmek için kaç kayıt görüntülendiğini belirlememiz gerektiğinden biraz daha karmaşıktır.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

Şekil 8 ve 9 işlem içinde özel sayfalama arabirimini gösterir. Şekil 8 ' de `ManageUsers.aspx` tüm Kullanıcı hesapları için ilk veri sayfası görüntülenirken sayfa görüntülenir. 13 hesabın yalnızca 10 ' un görüntülendiğini unutmayın. Ileri veya son bağlantıya tıkladığınızda geri göndermeye neden olur, `PageIndex` 1 olarak güncelleştirilir ve Kullanıcı hesaplarının ikinci sayfasını kılavuza bağlar (bkz. Şekil 9).

[![Ilk 10 Kullanıcı hesabı görüntülenir](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**Şekil 8**: Ilk 10 Kullanıcı hesabı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))

[![Sonraki bağlantıya tıkladığınızda Kullanıcı hesaplarının Ikinci sayfası görüntülenir](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**Şekil 9**: sonraki bağlantıya tıklandığında Kullanıcı hesaplarının Ikinci sayfası görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))

## <a name="summary"></a>Özet

Yöneticilerin genellikle hesaplar listesinden bir Kullanıcı seçmesini gerekir. Önceki öğreticilerde, kullanıcılarla doldurulmuş bir açılan listeyi kullanmaya baktık, ancak bu yaklaşım iyi ölçeklenmez. Bu öğreticide, daha iyi bir alternatif inceliyoruz: sonuçları Sayfalanmış bir GridView 'da görüntülenen filtrelenebilir bir arabirim. Bu Kullanıcı arabirimiyle Yöneticiler, binlerce arasında bir kullanıcı hesabını hızla ve etkili bir şekilde bulabilir ve seçebilir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [SQL Server 2005 ile ASP.NET 'de özel sayfalama](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [Büyük miktarlarda veri aracılığıyla verimli sayfalama](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [Kendi web sitesi yönetim aracınızı toplama](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott, [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) konumundaki blogundan veya üzerinden erişilebilir [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Alicja Maziarz. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Bu durumda, şu adreste bir satır bırakın:

> [!div class="step-by-step"]
> [Önceki](unlocking-and-approving-user-accounts-cs.md) 
>  [Sonraki](recovering-and-changing-passwords-vb.md)
