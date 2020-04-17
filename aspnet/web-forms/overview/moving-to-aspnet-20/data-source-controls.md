---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Veri Kaynağı Denetimleri | Microsoft Dokümanlar
author: rick-anderson
description: ASP.NET 1.x'teki DataGrid denetimi, Web uygulamalarında veri erişiminde büyük bir iyileşme ye işaret etti. Ancak, olması gibi kullanıcı dostu değildi ....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540226"
---
# <a name="data-source-controls"></a>Veri Kaynağı Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 1.x'teki DataGrid denetimi, Web uygulamalarında veri erişiminde büyük bir iyileşme ye işaret etti. Ancak, olması gibi kullanıcı dostu değildi. Yine de ondan çok yararlı işlevsellik elde etmek için kod önemli miktarda gerekli. 1.x'teki tüm veri erişim çabalarında model böyledir.

ASP.NET 1.x'teki DataGrid denetimi, Web uygulamalarında veri erişiminde büyük bir iyileşme ye işaret etti. Ancak, olması gibi kullanıcı dostu değildi. Yine de ondan çok yararlı işlevsellik elde etmek için kod önemli miktarda gerekli. 1.x'teki tüm veri erişim çabalarında model böyledir.

ASP.NET 2.0 bu adresleri kısmen veri kaynağı denetimleri ile. ASP.NET 2.0'daki veri kaynağı denetimleri, geliştiricilere verileri almak, verileri görüntülemek ve verileri düzenlemek için bildirimsel bir model sağlar. Veri kaynağı denetimlerinin amacı, bu verilerin kaynağından bağımsız olarak veriye bağlı denetimlere verilerin tutarlı bir temsilini sağlamaktır. 2.0 ASP.NET veri kaynağı denetimleri kalbinde DataSourceControl soyut sınıftır. DataSourceControl sınıfı, iDataSource arabiriminin ve IListSource arabiriminin temel uygulamasını sağlar ve ikincisi veri kaynağı denetimini veri kaynağı denetimi olarak atamanızı sağlar (daha sonra tartışılan yeni DataSourceId özelliği aracılığıyla) ve verileri liste olarak ortaya çıkarmanızı sağlar. Veri kaynağı denetiminden elde edilen her veri listesi DataSourceView nesnesi olarak ortaya çıkar. DataSourceView örneklerine erişim IDataSource arabirimi tarafından sağlanır. Örneğin, GetViewNames yöntemi, belirli bir veri kaynağı denetimiyle ilişkili DataSourceViews'u saymanızı sağlayan bir ICollection döndürür ve GetView yöntemi belirli bir DataSourceView örneğine ada göre erişmenizi sağlar.

Veri kaynağı denetimleri kullanıcı arabirimi yok. Bildirimsel sözdizimini destekleyebilmeleri ve istenirse sayfa durumuna erişebilmeleri için sunucu denetimleri olarak uygulanırlar. Veri kaynağı denetimleri istemciye herhangi bir HTML biçimlendirmesi oluşturmaz.

> [!NOTE]
> Daha sonra göreceğiniz gibi, veri kaynağı denetimleri kullanılarak elde edilen önbelleğe alma avantajları da vardır.

## <a name="storing-connection-strings"></a>Bağlantı Dizelerini Depolama

Veri kaynağı denetimlerinin nasıl yapılandırılabildiğini görmeden önce, bağlantı dizeleri ile ilgili ASP.NET 2.0'da yeni bir yeteneği kapsamalıyız. ASP.NET 2.0, yapılandırma dosyasında çalışma zamanında dinamik olarak okunabilen bağlantı dizelerini kolayca depolamanızı sağlayan yeni bir bölüm sunar. &lt;ConnectionStrings&gt; bölümü bağlantı dizelerini depolamayı kolaylaştırır.

Aşağıdaki parçacık yeni bir bağlantı dizesi ekler.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;Tıpkı&gt; appSettings bölümünde olduğu &lt;gibi,&gt; connectionStrings bölümü &lt;yapılandırma dosyasında system.web&gt; bölümünün dışında görünür.

Bu bağlantı dizesini kullanmak için, sunucu denetiminin ConnectionString özniteliğini ayarlarken aşağıdaki sözdizimini kullanabilirsiniz.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;ConnectionStrings&gt; bölümü, hassas bilgilerin açığa alınmaması için de şifrelenebilir. Bu yetenek daha sonraki bir modülde ele alınacaktır.

## <a name="caching-data-sources"></a>Veri Kaynaklarını Önbelleğe Alma

Her DataSourceControl önbelleğe alma yapılandırmak için dört özellik sağlar; EtkinleştirÖnme, ÖnbellekSüresi, Önbellek Politikası ve CacheKeyDependency.

## <a name="enablecaching"></a>EtkinleştirMeCaching

EnableCaching, veri kaynağı denetimi için önbelleğe alınıp alınmadığını belirleyen bir Boolean özelliğidir.

## <a name="cacheduration-property"></a>ÖnbellekSüresi Özelliği

CacheDuration özelliği, önbelleğin geçerli kaldığı saniye sayısını ayarlar. Bu özelliği **0** olarak ayarlamak önbelleğin açıkça geçersiz kılınana kadar geçerli kalmasına neden olur.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy Özelliği

CacheExpirationPolicy özelliği **Mutlak** veya **Sürgülü**olarak ayarlanabilir. Mutlak olarak ayarlanması, verilerin önbelleğe alınacağı maksimum sürenin Önbellek Süresi özelliği tarafından belirtilen saniye sayısı olduğu anlamına gelir. Sürgülü olarak ayarlayarak, her işlem yapıldığında son kullanma süresi sıfırlanır.

## <a name="cachekeydependency-property"></a>ÖnbellekBağımlılık Özelliği

CacheKeyDependency özelliği için bir dize değeri belirtilirse, ASP.NET bu dizeyi temel alan yeni bir önbellek bağımlılığı ayarlar. Bu, Önbelleği yalnızca değiştirerek veya kaldırarak önbelleği açıkça geçersiz kılmanızı sağlar.

**Önemli**: Kimliğe bürünme etkinleştirilirse ve veri kaynağına ve/veya veri içeriğine erişim istemci kimliğine dayanıyorsa, Etkinleştirme'yi False'a ayarlayarak önbelleğe almanın devre dışı bırakılması önerilir. Bu senaryoda önbelleğe alma etkinse ve verileri ilk isteyen kullanıcı dışında bir kullanıcı bir istek tesniye sinde bulunulmazsa, veri kaynağına yetkilendirme uygulanmaz. Veriler yalnızca önbellekten sunulacaktır.

## <a name="the-sqldatasource-control"></a>SqlDataSource Denetimi

SqlDataSource denetimi, bir geliştiricinin ADO.NET destekleyen herhangi bir ilişkisel veritabanında depolanan verilere erişmesine olanak tanır. Oracle'a erişmek için System.Data.SqlClient sağlayıcısını, System.Data.OleDb sağlayıcısına, System.Data.Odbc sağlayıcısına veya System.Data.OracleClient sağlayıcısına erişmek için kullanabilir. Bu nedenle, SqlDataSource kesinlikle sadece bir SQL Server veritabanında veri erişmek için kullanılan değildir.

SqlDataSource'u kullanmak için ConnectionString özelliği için bir değer sağlamanız ve bir SQL komutu veya depolanan yordam belirtmeniz yeterlidir. SqlDataSource denetimi, temel ADO.NET mimarisiyle çalışmayla ilgilenir. Bağlantıyı açar, veri kaynağını sorgular veya depolanan yordamı yürütür, verileri döndürür ve sonra bağlantıyı sizin için kapatır.

> [!NOTE]
> DataSourceControl sınıfı bağlantıyı sizin için otomatik olarak kapattığından, veritabanı bağlantılarını sızdırarak oluşturulan müşteri çağrılarının sayısını azaltmalıdır.

Aşağıdaki kod snippet yukarıda gösterildiği gibi yapılandırma dosyasında depolanan bağlantı dizesini kullanarak bir SqlDataSource denetimine DropDownList denetimi bağlar.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Yukarıda gösterildiği gibi, SqlDataSource'un DataSourceMode özelliği veri kaynağının modunu belirtir. Yukarıdaki örnekte, DataSourceMode DataReader olarak ayarlanır. Bu durumda, SqlDataSource yalnızca ileri ve salt okunur imleci kullanarak bir IDataReader nesnesini döndürecektir. Döndürülen belirtilen nesne türü, kullanılan sağlayıcı tarafından denetlenir. Bu durumda, system.data.sqlclient sağlayıcısını web.config &lt;dosyasının&gt; connectionStrings bölümünde belirtildiği şekilde kullanıyorum. Bu nedenle, döndürülen nesne SqlDataReader türünden olacaktır. DataSet'in DataSourceMode değeri belirterek, veriler sunucudaki bir DataSet'te depolanabilir. Bu mod sıralama, sayfalama, vb gibi özellikler eklemenize olanak sağlar. SqlDataSource'u GridView denetimine veri bağlamasaydım, DataSet modunu seçerdim. Ancak, Bir DropDownList durumunda, DataReader modu doğru seçimdir.

> [!NOTE]
> Bir SqlDataSource veya AccessDataSource önbelleğe alırken, DataSourceMode özelliği DataSet olarak ayarlanmalıdır. DataSourceMode of DataReader ile önbelleğe alma sağlarsanız bir özel durum oluşur.

## <a name="sqldatasource-properties"></a>SqlDataSource Özellikleri

SqlDataSource denetiminin özelliklerinden bazıları şunlardır.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Parametrelerden biri null ise seçme komutunun iptal edilip edilmeyeceğini belirten bir Boolean değeri. Varsayılan olarak doğrudur.

### <a name="conflictdetection"></a>Conflictdetection

Birden çok kullanıcının aynı anda bir veri kaynağını güncelleştirebileceği bir durumda, ConflictDetection özelliği SqlDataSource denetiminin davranışını belirler. Bu özellik, Çakışma Seçenekleri numaralandırma değerlerinden birine değerb.rö'ye göre değerlendirilir. Bu değerler **CompareAllValues** ve **OverwriteChanges**vardır. OverwriteChanges olarak ayarlanırsa, veri kaynağına veri yazan son kişi önceki değişikliklerin üzerine yazar. Ancak, ConflictDetection özelliği CompareAllValues olarak ayarlanırsa, SelectCommand tarafından döndürülen sütunlar için parametreler oluşturulur ve Bu sütunların her birinde özgün değerleri tutmak için parametreler oluşturulur ve SqlDataSource'un SelectCommand yürütüldükten sonra değerlerin değişip değişmediğini belirlemesine olanak tanıyan parametreler de oluşturulur.

### <a name="deletecommand"></a>Deletecommand

Satırları veritabanından silerken kullanılan SQL dizesini ayarlar veya alır. Bu bir SQL sorgusu veya depolanmış yordam adı olabilir.

### <a name="deletecommandtype"></a>Komut Türünü Silme

SQL sorgusu (Text) veya depolanmış yordam (StoredProcedure) komutunu ayarlar veya alır.

### <a name="deleteparameters"></a>Deleteparameters

SqlDataSource denetimi ile ilişkili SqlDataSourceView nesnesinin DeleteCommand tarafından kullanılan parametreleri döndürür.

### <a name="oldvaluesparameterformatstring"></a>Oldvaluesparameterformatstring

Bu özellik, Çakışma Algılama özelliğinin CompareAllValues olarak ayarlandığı durumlarda özgün değer parametrelerinin biçimini belirtmek için kullanılır. Varsayılan değer, {0} özgün değer parametrelerinin özgün parametreyle aynı adı alacağı anlamına gelir. Başka bir deyişle, alan adı EmployeeID ise, özgün @EmployeeIDdeğer parametresi .

### <a name="selectcommand"></a>Selectcommand

Veritabanından veri almak için kullanılan SQL dizesini ayarlar veya alır. Bu bir SQL sorgusu veya depolanmış yordam adı olabilir.

### <a name="selectcommandtype"></a>Komut Türünü Seçin

SQL sorgusu (Text) veya depolanmış yordam (StoredProcedure) select komutu türünü ayarlar veya alır.

### <a name="selectparameters"></a>Selectparameters

SqlDataSource denetimi ile ilişkili SqlDataSourceView nesnesinin SelectCommand tarafından kullanılan parametreleri döndürür.

### <a name="sortparametername"></a>SıralamaParameterName

Veri kaynağı denetimi tarafından alınan verileri sıralarken kullanılan depolanmış yordam parametresinin adını alır veya ayarlar. Yalnızca SelectCommandType StoredProcedure olarak ayarlandığında geçerlidir.

### <a name="sqlcachedependency"></a>Sqlcachedependency

SQL Server önbellek bağımlılığında kullanılan veritabanlarını ve tabloları belirten yarı nokta noktalı dize. (SQL önbellek bağımlılıkları daha sonraki bir modülde ele alınacaktır.)

### <a name="updatecommand"></a>Updatecommand

Veritabanındaki verileri güncellerken kullanılan SQL dizesini ayarlar veya alır. Bu bir SQL sorgusu veya depolanmış yordam adı olabilir.

### <a name="updatecommandtype"></a>GüncellemeKomut Türü

SQL sorgusu (Text) veya depolanmış yordam (StoredProcedure) yordamını ayarlar veya alır.

### <a name="updateparameters"></a>Updateparameters

SqlDataSource denetimi ile ilişkili SqlDataSourceView nesnesinin UpdateCommand tarafından kullanılan parametreleri döndürür.

## <a name="the-accessdatasource-control"></a>AccessDataSource Denetimi

AccessDataSource denetimi SqlDataSource sınıfından türetilmiştir ve microsoft access veritabanına veri bağlamak için kullanılır. AccessDataSource denetimi için ConnectionString özelliği salt okunur bir özelliktir. DataFile özelliği, ConnectionString özelliğini kullanmak yerine, aşağıda gösterildiği gibi Access Veritabanı'nı işaret etmek için kullanılır.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource her zaman System.Data.OleDb için temel SqlDataSource Sağlayıcı Adı ayarlar ve Microsoft.Jet.OLEDB.4.0 OLE DB sağlayıcısı kullanarak veritabanına bağlanır. Parola korumalı access veritabanına bağlanmak için AccessDataSource denetimini kullanamazsınız. Parola korumalı bir veritabanına bağlanmanız gerekiyorsa, SqlDataSource denetimini kullanmanız gerekir.

> [!NOTE]
> Web sitesinde depolanan erişim veritabanları Uygulama\_Veri dizini yerleştirilmelidir. ASP.NET bu dizindeki dosyaların göz atılmasına izin vermez. Access veritabanlarını kullanırken işlem hesabı Okuma ve\_Yazma izinlerini Uygulama Veri dizinine vermeniz gerekir.

## <a name="the-xmldatasource-control"></a>XmlDataSource Kontrolü

XmlDataSource, XML verilerini veriye bağlı denetimlere bağlamak için kullanılır. DataFile özelliğini kullanarak bir XML dosyasına bağlayabilirsiniz veya Veri özelliğini kullanarak bir XML dizesine bağlanabilirsiniz. XmlDataSource, XML özniteliklerini bağlanabilir alanlar olarak ortaya çıkarır. Öznitelik olarak temsil edilmeyen değerlere bağlamanız gereken durumlarda, XSL dönüşümü kullanmanız gerekir. XML verilerini filtrelemek için XPath ifadelerini de kullanabilirsiniz.

Aşağıdaki XML dosyasını göz önünde bulundurun:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource'un yalnızca Kişi&gt; düğümlerine filtre uygulayabilmek için *Kişi/Kişi'nin* XPath özelliğini kullandığına dikkat edin. &lt; DropDownList sonra DataTextField özelliğini kullanarak Soyadı özniteliğine veri bağlar.

XmlDataSource denetimi öncelikle yalnızca okunan XML verilerine veri bağlamak için kullanılırken, XML veri dosyasını da yeniden yapmak mümkündür. Bu gibi durumlarda, XML dosyasındaki bilgilerin otomatik olarak eklenmesi, güncellenmesi ve silinmesi, diğer veri kaynağı denetimlerinde olduğu gibi otomatik olarak gerçekleşmez. Bunun yerine, XmlDataSource denetiminin aşağıdaki yöntemlerini kullanarak verileri el ile yeniden disetetmek için kod yazmanız gerekir.

### <a name="getxmldocument"></a>GetXmlBelgesi

XmlDataSource tarafından alınan XML kodunu içeren bir XmlDocument nesnesini alır.

### <a name="save"></a>Kaydet

Bellek teki XmlDocument'ı veri kaynağına geri kaydeder.

Kaydet yönteminin yalnızca aşağıdaki iki koşul yerine getirildiğinde çalışacağını fark etmek önemlidir:

1. XmlDataSource, Bellekteki XML verilerine bağlamak için Veri özelliği yerine bir XML dosyasına bağlamak için DataFile özelliğini kullanır.
2. Transform veya TransformFile özelliği aracılığıyla hiçbir dönüşüm belirtilmemiştir.

Kaydet yönteminin aynı anda birden çok kullanıcı tarafından çağrıldığında beklenmeyen sonuçlar doğurabileceğini de unutmayın.

## <a name="the-objectdatasource-control"></a>ObjectDataSource Denetimi

Bu noktaya kadar örtbas ettiğimiz veri kaynağı denetimleri, veri kaynağı denetiminin doğrudan veri deposuna iletildiği iki katmanlı uygulamalar için mükemmel seçeneklerdir. Ancak, birçok gerçek dünya uygulamaları, veri kaynağı denetiminin veri katmanıyla iletişim kuranabilecek bir iş nesnesiyle iletişim kurması gerekebileceği çok katmanlı uygulamalardır. Bu gibi durumlarda, ObjectDataSource faturayı güzelce doldurur. ObjectDataSource bir kaynak nesneile birlikte çalışır. ObjectDataSource denetimi kaynak nesnenin bir örneğini oluşturur, belirtilen yöntemi çağırır ve nesne örneğini statik yöntemler yerine örnek yöntemleri varsa tek bir istek kapsamında imha eder (Visual Basic'te paylaşılır). Bu nedenle, nesneniz instateless olmalıdır. Diğer bir süre, nesneniz tek bir istek aralığında gerekli tüm kaynakları edinmeli ve serbest bırakmalıdır. ObjectDataSource denetiminin ObjectCreating olayını işleyerek kaynak nesnenin nasıl oluşturulduğunu denetleyebilirsiniz. Kaynak nesnenin bir örneğini oluşturabilir ve objectdataSourceEventArgs sınıfının ObjectInstance özelliğini bu örneğin olarak ayarlayabilirsiniz. ObjectDataSource denetimi, kendi başına bir örnek oluşturmak yerine ObjectCreating olayında oluşturulan örneği kullanır.

ObjectDataSource denetiminin kaynak nesnesi, verileri almak ve değiştirmek için çağrılabilen ortak statik yöntemleri (Visual Basic'te Paylaşılan) ortaya çıkarırsa, ObjectDataSource denetimi bu yöntemleri doğrudan çağırır. Bir ObjectDataSource denetimi yöntem aramaları yapmak için kaynak nesnenin bir örneğini oluşturması gerekiyorsa, nesne hiçbir parametre almayan bir ortak oluşturucu içermelidir. ObjectDataSource denetimi, kaynak nesnenin yeni bir örneğini oluşturduğunda bu oluşturucuyu çağırır.

Kaynak nesne parametreleri olmayan bir ortak oluşturucu içermiyorsa, ObjectDataSource denetimi tarafından ObjectCreate olayında kullanılacak kaynak nesnenin bir örneğini oluşturabilirsiniz.

## <a name="specifying-object-methods"></a>Nesne Yöntemlerini Belirtme

ObjectDataSource denetiminin kaynak nesnesi, verileri seçmek, eklemek, güncelleştirmek veya silmek için kullanılan herhangi bir sayıda yöntem içerebilir. Bu yöntemler, ObjectDataSource denetiminin SelectMethod, InsertMethod, UpdateMethod veya DeleteMethod özelliği kullanılarak tanımlanan yöntemin adına dayalı ObjectDataSource denetimi tarafından çağrılır. Kaynak nesne, veri kaynağındaki toplam nesne sayısının sayısını döndüren SelectCountMethod özelliğini kullanarak ObjectDataSource denetimi tarafından tanımlanan isteğe bağlı bir SelectCount yöntemi de içerebilir. ObjectDataSource denetimi, çağrı yaparken kullanılmak üzere veri kaynağındaki toplam kayıt sayısını almak için bir Select yöntemi çağrıldıktan sonra SelectCount yöntemini çağırır.

## <a name="lab-using-data-source-controls"></a>Veri Kaynağı Denetimlerini Kullanan Laboratuvar

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Alıştırma 1 - SqlDataSource Denetimi ile Veri Görüntüleme

Aşağıdaki alıştırma, Northwind veritabanına bağlanmak için SqlDataSource denetimini kullanır. Bir SQL Server 2000 örneğinde Northwind veritabanına erişiminiz olduğunu varsayar.

1. Yeni bir ASP.NET Web sitesi oluşturun.
2. Yeni bir web.config dosyası ekleyin.

    1. Solution Explorer'da projeye sağ tıklayın ve Yeni Öğe Ekle'yi tıklatın.
    2. Şablonlar listesinden Web Yapılandırma Dosyası'nı seçin ve Ekle'yi tıklatın.
3. Bağlantıları aşağıdaki &lt;gibi&gt; edinStrings bölümünü: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Kod görünümüne geçin ve asp:SqlDataSource &lt;&gt; denetimine connectionString özniteliği ve SelectCommand özniteliği ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Tasarım görünümünden yeni bir GridView denetimi ekleyin.
6. GridView Görevler menüsündeki Veri Kaynağı açılır menüsünden SqlDataSource1'i seçin.
7. Varsayılan.aspx'e sağ tıklayın ve menüden Tarayıcıda Görüntüle'yi seçin. Kaydedilmesi istendiğinde Evet'i tıklatın.
8. GridView Ürünler tablosundaki verileri görüntüler.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Alıştırma 2 - SqlDataSource Denetimi ile Veri Düzenleme

Aşağıdaki alıştırma, bildirimsel sözdizimini kullanarak bir DropDownList denetiminin nasıl bağlanılsüreceğini gösterir ve DropDownList denetiminde sunulan verileri düzenliletmenizi sağlar.

1. Tasarım görünümünde, GridView denetimini Varsayılan.aspx'ten silin. 

    **Önemli**: SqlDataSource denetimini sayfada bırakın.
2. Varsayılan.aspx'e DropDownList denetimi ekleyin.
3. Kaynak görünümüne geçin.
4. Asp:DropDownList &lt;&gt; denetimine aşağıdaki gibi bir DataSourceId, DataTextField ve DataValueField özniteliği ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Varsayılan.aspx'i kaydedin ve tarayıcıda görüntüleyin. DropDownList'in Northwind veritabanındaki tüm ürünleri içerdiğini unutmayın.
6. Tarayıcıyı kapatın.
7. Varsayılan.aspx'in Kaynak görünümünde, DropDownList denetiminin altına yeni bir TextBox denetimi ekleyin. TextBox'ın kimlik özelliğini txtProductName olarak değiştirin.
8. TextBox denetimi altında yeni bir Düğme denetimi ekleyin. Düğmenin kimlik özelliğini btnUpdate ve Metin **özelliğini Ürün Adını Güncelleştirmek**için değiştirin.
9. Default.aspx'in Kaynak görünümünde, SqlDataSource etiketine aşağıdaki gibi bir UpdateCommand özelliği ve iki yeni UpdateParameters ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Bu koda iki güncelleştirme parametresi (ProductName ve ProductID) eklendi. Bu parametreler txtProductName TextBox'ın Metin özelliğine ve ddlProducts DropDownList'in SelectedValue özelliğine eşlenir.
10. Tasarım görünümüne geçin ve olay işleyicisi eklemek için Düğme denetimine çift tıklayın.
11. btnUpdate\_Click koduna aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx'e sağ tıklayın ve tarayıcıda görüntülemeyi seçin. Tüm değişiklikleri kaydetmek için istendiğinde Evet'i tıklatın.
13. ASP.NET 2.0 kısmi sınıflar çalışma zamanında derlemeye izin verir. Kod değişikliklerinin etkili olduğunu görmek için bir uygulama oluşturmana gerek yoktur.
14. DropDownList'ten bir ürün seçin.
15. TextBox'a seçili ürünün yeni bir adını girin ve ardından Güncelleştir düğmesini tıklatın.
16. Ürün adı veritabanında güncelleştirilir.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Egzersiz 3 ObjectDataSource Denetimini Kullanma

Bu alıştırma, ObjectDataSource denetiminin ve northwind veritabanıyla etkileşimde bulunacak bir kaynak nesnenin nasıl kullanılacağını gösterecektir.

1. Solution Explorer'da projeye sağ tıklayın ve Yeni Öğe Ekle'ye tıklayın.
2. Şablonlar listesinde Web Formu'nu seçin. Object.aspx adını değiştirin ve Ekle'yi tıklatın.
3. Solution Explorer'da projeye sağ tıklayın ve Yeni Öğe Ekle'ye tıklayın.
4. Şablonlar listesinde Sınıf'ı seçin. Sınıfın adını NorthwindData.cs olarak değiştirin ve Ekle'yi tıklatın.
5. Sınıfı Uygulama\_Kodu klasörüne eklemek istendiğinde Evet'i tıklatın.
6. NorthwindData.cs dosyasına aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. object.aspx'in Kaynak görünümüne aşağıdaki kodu ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Tüm dosyaları kaydedin ve object.aspx'e göz atın.
9. Ayrıntıları görüntüleyerek, çalışanları düzenleyerek, çalışan ekleyerek ve çalışanları silerek arayüzle etkileşimkurun.
