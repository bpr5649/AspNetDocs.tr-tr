---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: Çıktı Önbelleğe Alma (VB) ile Performansı Artırma | Microsoft Dokümanlar
author: rick-anderson
description: Bu eğitimde, çıktı önbelleğe alma yararlanarak ASP.NET MVC web uygulamalarınızın performansını nasıl önemli ölçüde artırabileceğinizi öğrenirsiniz. Siz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: e18d4c5132d4dccc97f1465e7885c9c47a0edab1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542696"
---
# <a name="improving-performance-with-output-caching-vb"></a>Çıktı Önbelleğe Alma ile Performansı İyileştirme (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Bu eğitimde, çıktı önbelleğe alma yararlanarak ASP.NET MVC web uygulamalarınızın performansını nasıl önemli ölçüde artırabileceğinizi öğrenirsiniz. Aynı içeriğin her bir yeni kullanıcı eylemi çağırdığında oluşturulmasıgerekmemesi için bir denetleyici eyleminden döndürülen sonucu nasıl önbelleğe aldığınızı öğrenirsiniz.

Bu öğreticinin amacı, çıktı önbelleğinden yararlanarak ASP.NET bir MVC uygulamasının performansını nasıl önemli ölçüde artırabileceğinizi açıklamaktır. Çıktı önbelleği, denetleyici eylemi yle döndürülen içeriği önbelleğe almalarını sağlar. Bu şekilde, aynı denetleyici eylemi çağrıldığı her seferinde aynı içeriğin oluşturulması gerekmez.

Örneğin, ASP.NET MVC uygulamanızın Dizin adlı bir görünümde veritabanı kayıtlarının listesini görüntülediğini düşünün. Normalde, bir kullanıcı Dizin görünümünü döndüren denetleyici eylemini her kez çağırınca, veritabanı kayıtları kümesi veritabanı sorgusu gerçekleştirerek veritabanından alınmalıdır.

Diğer taraftan, çıktı önbelleğinden yararlanırsanız, herhangi bir kullanıcı aynı denetleyici eylemini her çağırdığında bir veritabanı sorgusuyürütmeyi önleyebilirsiniz. Görünüm denetleyici eyleminden yeniden oluşturulacak şekilde önbellekten alınabilir. Önbelleğe alma, sunucuda gereksiz çalışma yapmaktan kaçınmanızı sağlar.

#### <a name="enabling-output-caching"></a>Çıkış Önbelleğe Alma Etkinleştirme

Tek bir denetleyici eylemine &lt;veya&gt; tüm denetleyici sınıfına bir OutputCache özniteliği ekleyerek çıktı önbelleğe alma özelliğini etkinleştirin. Örneğin, Listeleme 1'deki denetleyici, Index() adlı bir eylemi ortaya çıkarır. Dizin() eyleminin çıktısı 10 saniye önbelleğe alınır.

**Listeleme 1 – Denetleyiciler\HomeController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

ASP.NET MVC'nin Beta sürümlerinde, çıktı önbelleğe [http://www.MySite.com/](http://www.mysite.com/)alma gibi bir URL için çalışmaz. Bunun yerine, gibi [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)bir URL girmeniz gerekir.

Listeleme 1'de, Dizin() eyleminin çıktısı 10 saniye önbelleğe alınır. İsterseniz, çok daha uzun bir önbellek süresi belirtebilirsiniz. Örneğin, bir denetleyici eyleminin çıktısını bir gün için önbelleğe almak isterseniz, önbellek süresi 86400 saniye \* (60 saniye 60 dakika \* 24 saat) belirtebilirsiniz.

İçeriğin belirttiğiniz süre boyunca önbelleğe alınacağının garantisi yoktur. Bellek kaynakları azaldığında, önbellek içeriği otomatik olarak tahliye etmeye başlar.

Listeleme 1'deki Ev denetleyicisi, Listeleme 2'deki Dizin görünümünü döndürür. Bu manzaranın özel bir özelliği yok. Dizin görünümü yalnızca geçerli zamanı görüntüler (Bkz. Şekil 1).

**Listeleme 2 – Görünümler\Ana Sayfa\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**Şekil 1 – Önbelleğe Alınmış Dizin görünümü**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

Tarayıcınızın adres çubuğuna URL /Home/Index'i girerek ve tarayıcınızdaki Yenile/Yeniden Yükle düğmesine tekrar tekrar basarak Index() eylemini birden çok kez çağırırsanız, Dizin görünümünde görüntülenen süre 10 saniye boyunca değişmez. Görünüm önbelleğe alındığından aynı süre görüntülenir.

Aynı görünümün uygulamanızı ziyaret eden herkes için önbelleğe alınmış olduğunu anlamak önemlidir. Index() eylemini çağıran herkes, Dizin görünümünün önbelleğe alınmış sürümünü alır. Bu, web sunucusunun Dizin görünümüne hizmet etmek için gerçekleştirmesi gereken çalışma miktarının önemli ölçüde azaldığı anlamına gelir.

Listeleme 2 görünümü gerçekten basit bir şey yapıyor olur. Görünüm yalnızca geçerli saati görüntüler. Ancak, veritabanı kayıtları kümesini görüntüleyen bir görünümü kolayca önbelleğe alabilirsiniz. Bu durumda, veritabanı kayıtları kümesiveritabanından her ve görünümü döndüren denetleyici eylem çağrıldı her zaman alınması gerekmez. Önbelleğe alma, hem web sunucunuzun hem de veritabanı sunucunuzun gerçekleştirmesi gereken çalışma miktarını azaltabilir.

MVC görünümünde &lt;%@ OutputCache&gt; % yönergesini kullanmayın. Bu yönerge, Web Formlar dünyasından kanayan ve ASP.NET bir MVC uygulamasında kullanılmamalıdır. 

#### <a name="where-content-is-cached"></a>İçeriğin Önbelleğe Aldığı Yerler

Varsayılan olarak, OutputCache &lt;&gt; özniteliğini kullandığınızda, içerik üç konumda önbelleğe alınır: web sunucusu, tüm proxy sunucuları ve web tarayıcısı. &lt;OutputCache&gt; özniteliğinin Konum özelliğini değiştirerek içeriğin önbelleğe alınacağı yeri tam olarak denetleyebilirsiniz.

Konum özelliğini aşağıdaki değerlerden herhangi birine ayarlayabilirsiniz:

> · Herhangi bir
> 
> · Istemci
> 
> · Aşağı akım
> 
> · Sunucu
> 
> · Hiçbiri
> 
> · ServerAndClient

Varsayılan olarak, Konum özelliği Any değerine sahiptir. Ancak, yalnızca tarayıcıda veya yalnızca sunucuda önbellek yapmak isteyebileceğiniz durumlar vardır. Örneğin, her kullanıcı için kişiselleştirilmiş bilgileri önbelleğe alıyorsanız, sunucudaki bilgileri önbelleğe almamalısınız. Farklı kullanıcılara farklı bilgiler görüntülüyorsanız, bilgileri yalnızca istemci üzerinde önbelleğe almanız gerekir.

Örneğin, Listeleme 3'teki denetleyici, geçerli kullanıcı adını döndüren GetName() adlı bir eylemi ortaya çıkarır. Jack web sitesine giriş yaparsa ve GetName() eylemini çağırırsa, eylem "Merhaba Jack" dizesini döndürür. Eğer, daha sonra, Jill web sitesine giriş ve GetName () eylem çağırır o zaman o da dize "Hi Jack" alırsınız. Jak başlangıçta denetleyici eylemini çağırdıktan sonra dize tüm kullanıcılar için web sunucusunda önbelleğe alınır.

**Listeleme 3 – Denetleyiciler\BadUserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

Büyük olasılıkla, Listeleme 3'teki denetleyici istediğiniz şekilde çalışmaz. Jill'e "Merhaba Jack" mesajını göstermek istemezsin.

Sunucu önbelleğinde kişiselleştirilmiş içeriği asla önbelleğe almamalısınız. Ancak, performansı artırmak için tarayıcı önbelleğinde kişiselleştirilmiş içeriği önbelleğe almak isteyebilirsiniz. İçeriği tarayıcıda önbelleğe alırsanız ve bir kullanıcı aynı denetleyici eylemini birden çok kez çağırırsa, içerik sunucu yerine tarayıcı önbelleğinden alınabilir.

Listeleme 4'teki değiştirilmiş denetleyici GetName() eyleminin çıktısını önbelleğe alır. Ancak, içerik yalnızca tarayıcıda önbelleğe alınır ve sunucuda değil. Bu şekilde, birden çok kullanıcı GetName() yöntemini çağırdığında, her kişi başka bir kişinin kullanıcı adını değil, kendi kullanıcı adını alır.

**Listeleme 4 – Denetleyiciler\UserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

Listeleme &lt;4'teki&gt; OutputCache özniteliğinin OutputCacheLocation.Client değerine ayarlanmış bir Konum özelliği içerdiğine dikkat edin. &lt;OutputCache&gt; özniteliği de bir NoStore özelliği içerir. NoStore özelliği, proxy sunucularına ve tarayıcılara önbelleğe alınmış içeriğin kalıcı bir kopyasını saklamamaları gerektiğini bildirmek için kullanılır.

#### <a name="varying-the-output-cache"></a>Çıktı Önbelleğini Değiştirme

Bazı durumlarda, aynı içeriğin farklı önbelleğe alınmış sürümlerini isteyebilirsiniz. Örneğin, bir ana/ayrıntı sayfası oluşturduğunuzu düşünün. Ana sayfada film başlıklarının bir listesi görüntülenir. Bir başlığı tıklattığınızda, seçili filmin ayrıntılarını alırsınız.

Ayrıntılar sayfasını önbelleğe alırsak, hangi filme tıklarsanız tıklayın aynı filmin ayrıntıları görüntülenir. İlk kullanıcı tarafından seçilen ilk film gelecekteki tüm kullanıcılara görüntülenir.

&lt;OutputCache&gt; özniteliğinin VaryByParam özelliğinden yararlanarak bu sorunu çözebilirsiniz. Bu özellik, form parametresi veya sorgu dize parametresi değiştiğinde aynı içeriğin farklı önbelleğe alınmış sürümlerini oluşturmanıza olanak tanır.

Örneğin, Listeleme 5'teki denetleyici, Master() ve Details() adlı iki eylemi ortaya çıkarır. Master() eylemi film başlıklarının bir listesini döndürür ve Ayrıntılar() eylemi seçilen filmin ayrıntılarını döndürür.

**Listeleme 5 – Denetleyiciler\MoviesController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Master() eylemi "yok" değerine sahip bir VaryByParam özelliği içerir. Master() eylemi çağrıldığında, Master görünümünün aynı önbelleğe alınmış sürümü döndürülür. Form parametreleri veya sorgu dize parametreleri yoksayılır (Bkz. Şekil 2).

**Şekil 2 – /Filmler/Ana görünüm**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**Şekil 3 – /Filmler/Ayrıntılar görünümü**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Ayrıntılar() eylemi, "Id" değerine sahip bir VaryByParam özelliğini içerir. Id parametresinin farklı değerleri denetleyici eylemine aktarıldığında, Ayrıntılar görünümünün farklı önbelleğe alınmış sürümleri oluşturulur.

Bu VaryByParam özelliği kullanarak daha fazla önbelleğe alma ve daha az sonuçları anlamak önemlidir. Id parametresinin her farklı sürümü için Ayrıntılar görünümünün farklı bir önbelleğe alınmış sürümü oluşturulur.

VaryByParam özelliğini aşağıdaki değerlere ayarlayabilirsiniz:

> \*= Form veya sorgu dizesi parametresi değiştiğinde farklı önbelleğe alınmış bir sürüm oluşturun.
> 
> none = Asla farklı önbelleğe alınmış sürümler oluşturma
> 
> Parametrelerin semicolon listesi = Listedeki form veya sorgu dize parametrelerinden herhangi biri değiştiğinde farklı önbelleğe alınmış sürümler oluşturun

#### <a name="creating-a-cache-profile"></a>Önbellek Profili Oluşturma

OutputCache &lt;&gt; özniteliğinin özelliklerini değiştirerek çıktı önbelleği özelliklerini yapılandırmaya alternatif olarak, web yapılandırmasında (web.config) dosyada bir önbellek profili oluşturabilirsiniz. Web yapılandırma dosyasında önbellek profili oluşturmak birkaç önemli avantaj sunar.

İlk olarak, web yapılandırma dosyasında çıktı önbelleğe alma yapılandırarak, denetleyici eylemleri tek bir merkezi konumda içeriği nasıl önbelleğe denetleyebilirsiniz. Bir önbellek profili oluşturabilir ve profili birkaç denetleyiciye veya denetleyici eylemlere uygulayabilirsiniz.

İkinci olarak, uygulamanızı yeniden derlemeden web yapılandırma dosyasını değiştirebilirsiniz. Üretime zaten dağıtılmış bir uygulama için önbelleği devre dışı balmanız gerekiyorsa, web yapılandırma dosyasında tanımlanan önbellek profillerini değiştirebilirsiniz. Web yapılandırma dosyasındaki tüm değişiklikler otomatik olarak algılanır ve uygulanır.

Örneğin, Listeleme &lt;&gt; 6'daki önbelleğe alma web yapılandırması bölümü Cache1Hour adlı bir önbellek profili tanımlar. &lt;Önbelleğe&gt; alma bölümü, &lt;bir&gt; web yapılandırma dosyasının system.web bölümünde görünmelidir.

**Listeleme 6 – web.config için önbelleğe alma bölümü**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

Listeleme 7'deki denetleyici, Önbellek &lt;&gt; özelliğine sahip bir denetleyici eylemine Cache1Hour profilini nasıl uygulayabileceğinizi gösterir.

**Listeleme 7 – Denetleyiciler\ProfileController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

Listeleme 7'de denetleyici tarafından ortaya çıkarılan Index() eylemini çağırırsanız, aynı süre 1 saat boyunca döndürülür.

#### <a name="summary"></a>Özet

Çıkış önbelleğe alma, ASP.NET MVC uygulamalarınızın performansını önemli ölçüde artırmanın çok kolay bir yöntemini sağlar. Bu eğitimde, denetleyici &lt;eylemlerinçıktısını önbelleğe almak için OutputCache&gt; özniteliğini nasıl kullanacağınızı öğrendiniz. Ayrıca, içeriğin önbelleğe &lt;nasıl&gt; alındığını değiştirmek için Süre ve VaryByParam özellikleri gibi OutputCache özniteliğinin özelliklerini nasıl değiştireceğinizi de öğrendiniz. Son olarak, web yapılandırma dosyasındaki önbellek profillerini nasıl tanımlayabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](understanding-action-filters-vb.md)
> [Sonraki](adding-dynamic-content-to-a-cached-page-vb.md)
