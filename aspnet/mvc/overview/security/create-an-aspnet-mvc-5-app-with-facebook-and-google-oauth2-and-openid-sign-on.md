---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma (C#) ile MVC 5 Uygulaması Oluşturun | Microsoft Dokümanlar
author: Rick-Anderson
description: Bu öğretici, kullanıcıların Harici bir authenti kimlik bilgileri ile OAuth 2.0 kullanarak oturum açmanızı sağlayan bir ASP.NET MVC 5 web uygulaması oluşturmak için nasıl gösterir ...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676323"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="a2dfc-103">Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma Özellikli Bir ASP.NET MVC 5 Uygulaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="a2dfc-104">tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="a2dfc-105">Bu öğretici, kullanıcıların Facebook, Twitter, LinkedIn, Microsoft veya Google gibi harici bir kimlik doğrulama sağlayıcısının kimlik bilgileriyle [OAuth 2.0](http://oauth.net/2/) kullanarak oturum açmalarını sağlayan bir ASP.NET MVC 5 web uygulaması oluşturmanızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="a2dfc-106">Basitlik için, bu öğretici Facebook ve Google'ın kimlik bilgileri ile çalışmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="a2dfc-107">Milyonlarca kullanıcının bu dış sağlayıcılarla zaten hesapları olduğundan, bu kimlik bilgilerini web sitelerinizde etkinleştirmek önemli bir avantaj sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="a2dfc-108">Bu kullanıcılar, yeni bir kimlik bilgileri kümesi oluşturmak ve hatırlamak zorunda değillerse sitenize kaydolmaya daha meyilli olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="a2dfc-109">Ayrıca [sms ve e-posta İki Faktörlü Kimlik Doğrulama ile MVC 5 uygulaması ASP.NET](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="a2dfc-110">Öğretici ayrıca kullanıcı için profil verilerinin nasıl ekleyeceğini ve rol eklemek için Üyelik API'sinin nasıl kullanılacağını da gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="a2dfc-111">Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır ( [@RickAndMSFT](https://twitter.com/RickAndMSFT) Twitter beni takip edin: ).</span><span class="sxs-lookup"><span data-stu-id="a2dfc-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="a2dfc-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="a2dfc-112">Getting Started</span></span>

<span data-ttu-id="a2dfc-113">Web veya [Visual Studio 2013 için Visual Studio Express 2013'u](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyerek ve çalıştırarak başlayın. [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="a2dfc-114">Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üzeri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="a2dfc-115">Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, ve daha fazlası ile ilgili yardım için bu [örnek projeye](https://github.com/matthewdunsdon/oauthforaspnet)bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="a2dfc-116">Google OAuth 2'yi kullanmak ve SSL uyarıları olmadan yerel hata ayıklamak için Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üzeri ni yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="a2dfc-117">**Başlat** sayfasından **Yeni Proje'yi** tıklatın veya menüyü kullanabilirsiniz ve **Dosya'yı**ve ardından **Yeni Proje'yi**seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="a2dfc-118">İlk Uygulamanızı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2dfc-118">Creating Your First Application</span></span>

<span data-ttu-id="a2dfc-119">**Yeni Proje'yi**tıklatın, ardından soldaki **Visual C#** seçeneğini, ardından **Web'i** ve ardından **ASP.NET Web Uygulamasını**seçin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="a2dfc-120">Projenizi "MvcAuth" olarak adlandırın ve **ardından Tamam'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="a2dfc-121">Yeni **ASP.NET Projesi** iletişim kutusunda **MVC'yi**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="a2dfc-122">Kimlik Doğrulama Bireysel **Kullanıcı Hesapları**değilse, **Kimlik Doğrulamayı Değiştir** düğmesini tıklatın ve Bireysel Kullanıcı **Hesapları'nı**seçin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="a2dfc-123">**Bulutta Host'u**kontrol ederek, uygulamayı Azure'da barındırmak çok kolay olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="a2dfc-124">**Bulutta Ana Bilgisayar'ı**seçtiyseniz, yapıla iletişim kutusunu tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="a2dfc-125">En son OWIN ara yazılımlarına güncellemek için NuGet'i kullanın</span><span class="sxs-lookup"><span data-stu-id="a2dfc-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="a2dfc-126">[OWIN ara yazılımını](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)güncellemek için NuGet paket yöneticisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="a2dfc-127">Sol menüde **Güncelleştirmeler'i** seçin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="a2dfc-128">**Tümlerini Güncelleştir** düğmesine tıklayabilir veya yalnızca OWIN paketlerini arayabilirsiniz (bir sonraki resimde gösterilmiştir):</span><span class="sxs-lookup"><span data-stu-id="a2dfc-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="a2dfc-129">Aşağıdaki resimde yalnızca OWIN paketleri gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="a2dfc-130">Paket Yöneticisi Konsolu'ndan (PMC) `Update-Package` tüm paketleri güncelleştiren komutu girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="a2dfc-131">Uygulamayı çalıştırmak için **F5** veya **Ctrl+F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="a2dfc-132">Aşağıdaki resimde bağlantı noktası numarası 1234'dür.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="a2dfc-133">Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="a2dfc-134">Tarayıcı pencerenizin boyutuna bağlı olarak, **Ana Sayfa** **,** **İletişim**, **Kayıt** ve **Giriş** bağlantılarını görmek için gezinti simgesini tıklatmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="a2dfc-135">Projede SSL Kurulumu</span><span class="sxs-lookup"><span data-stu-id="a2dfc-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="a2dfc-136">Google ve Facebook gibi kimlik doğrulama sağlayıcılarına bağlanmak için SSL'yi kullanmak üzere IIS-Express'i ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="a2dfc-137">Oturum açtıktan sonra SSL kullanmaya devam etmek ve HTTP'ye geri düşmemek önemlidir, giriş çereziniz de kullanıcı adınız ve şifreniz kadar gizlidir ve SSL kullanmadan tel boyunca açık metin olarak gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="a2dfc-138">Ayrıca, MVC ardışık hattı çalıştırılmadan önce el sıkışmayı gerçekleştirmek ve kanalı (HTTPS'yi HTTP'den daha yavaş yapan şeyin büyük bir kısmı dır) güvenli hale getirmek için zaman aldınız, bu nedenle oturum açtıktan sonra HTTP'ye yönlendirmek mevcut isteği veya gelecekteki istekleri çok daha hızlı yapmaz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="a2dfc-139">**Çözüm Gezgini'nde** **MvcAuth** projesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="a2dfc-140">Proje özelliklerini göstermek için F4 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="a2dfc-141">Alternatif olarak, **Görünüm** menüsünden **Özellikler Penceresi'ni**seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="a2dfc-142">**SSL Etkin'i** True'ya Değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="a2dfc-143">SSL URL'sini kopyalayın `https://localhost:44300/` (diğer SSL projeleri oluşturmadığınız sürece olacaktır).</span><span class="sxs-lookup"><span data-stu-id="a2dfc-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="a2dfc-144">**Çözüm Gezgini'nde,** **MvcAuth** projesine sağ tıklayın ve **Özellikler'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="a2dfc-145">**Web** sekmesini seçin ve ardından SSL URL'sini **Project Url** kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="a2dfc-146">Dosyayı kaydedin (Ctl+S).</span><span class="sxs-lookup"><span data-stu-id="a2dfc-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="a2dfc-147">Facebook ve Google kimlik doğrulama uygulamalarını yapılandırmak için bu URL'ye ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="a2dfc-148">Tüm [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) istekleri gerektiren `Home` denetleyiciye Zorunlu Https özniteliğini ekleyin HTTPS kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="a2dfc-149">Daha güvenli bir yaklaşım uygulamaya [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtresi eklemektir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="a2dfc-150">Eğitimimde &quot;Uygulamayı SSL ile koruyun ve&quot; Yetkilendirme Özniteliği ile koruyun bölümüne bakın [Auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve Azure Uygulama Hizmeti'ne dağıtın.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="a2dfc-151">Ev denetleyicisinin bir bölümü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="a2dfc-152">Uygulamayı çalıştırmak için CTRL+F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="a2dfc-153">Sertifikayı geçmişte yüklediyseniz, bu bölümün geri kalanını atlayabilir ve [OAuth 2 için bir Google uygulaması oluşturmaya ve uygulamayı projeye bağlayarak](#goog)atlayabilirsiniz , aksi takdirde, IIS Express'in oluşturduğu kendi imzalı sertifikaya güvenme yönergelerini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="a2dfc-154">Güvenlik **Uyarısı** iletişim kutusunu okuyun ve localhost'u temsil eden sertifikayı yüklemek istiyorsanız **Evet'i** tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="a2dfc-155">IE *Ana* sayfayı gösterir ve hiçbir SSL uyarıları vardır.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="a2dfc-156">Google Chrome da sertifikayı kabul eder ve bir uyarı olmadan HTTPS içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="a2dfc-157">Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="a2dfc-158">Uygulamamız için Riskleri **Anlıyorum'a**güvenle tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="a2dfc-159">OAuth 2 için bir Google uygulaması oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="a2dfc-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="a2dfc-160">Geçerli Google OAuth yönergeleri için, [ASP.NET Core'da Google kimlik doğrulamasını yapılandırmaya](/aspnet/core/security/authentication/social/google-logins)bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="a2dfc-161">[Google Geliştiriciler Konsolu'na](https://console.developers.google.com/)gidin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="a2dfc-162">Daha önce bir proje oluşturmadıysanız, sol sekmede **Kimlik Bilgileri'ni** seçin ve ardından **Oluştur'u**seçin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="a2dfc-163">Sol sekmesinde Kimlik **Bilgileri'ni**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="a2dfc-164">**Kimlik bilgileri oluştur'u** ve **Ardından OAuth istemci kimliğini**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="a2dfc-165">**İstemci Kimliği Oluştur** iletişim kutusunda, uygulama türü için varsayılan **Web uygulamasını** saklayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="a2dfc-166">Yetkili **JavaScript** menşelerini yukarıda kullandığınız SSL URL'sine ayarlama (başka`https://localhost:44300/` SSL projeleri oluşturmadığınız sürece)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="a2dfc-167">Yetkili **uri yönlendirmeyi** şu şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="a2dfc-168">OAuth Consent ekran menü öğesini tıklatın, ardından e-posta adresinizi ve ürün adınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="a2dfc-169">Formu tamamladığınızda **Kaydet'i**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="a2dfc-170">Kütüphane menü öğesini tıklatın, **Google+ API'yi**arayın, üzerine tıklayın ve etkinleştir'e basın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="a2dfc-171">Aşağıdaki resimde etkin API'ler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="a2dfc-172">Google API'ler API Yöneticisi'nden, **Müşteri Kimliğini**almak için **Kimlik Bilgileri** sekmesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="a2dfc-173">Uygulama sırları ile bir JSON dosyasını kaydetmek için indirin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="a2dfc-174">**ClientId** ve **ClientSecret'ı** App_Start `UseGoogleAuthentication` klasöründeki *Startup.Auth.cs* dosyasında *App_Start* bulunan yönteme kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="a2dfc-175">Aşağıda gösterilen **ClientId** ve **ClientSecret** değerleri örneklerdir ve çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="a2dfc-176">Güvenlik - Hassas verileri asla kaynak kodunuzda depolamayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="a2dfc-177">Örneği basit tutmak için yukarıdaki koda hesap ve kimlik bilgileri eklenir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="a2dfc-178">[Parolaları ve diğer hassas verileri ASP.NET ve Azure Uygulama Hizmetine dağıtmaya](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)yönelik en iyi uygulamalara bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="a2dfc-179">Uygulamayı oluşturmak ve çalıştırmak için **CTRL+F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="a2dfc-180">Giriş **Yap** bağlantısını tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="a2dfc-181">Oturum **açmak için başka bir hizmeti kullan**, **Google'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="a2dfc-182">Yukarıdaki adımlardan herhangi birini kaçırırsanız HTTP 401 hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="a2dfc-183">Yukarıdaki adımlarınızı yeniden kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-183">Recheck your steps above.</span></span> <span data-ttu-id="a2dfc-184">Gerekli ayarı (örneğin **ürün adı)** kaçırırsanız, eksik öğeyi ekleyin ve kaydedin; kimlik doğrulamanın çalışması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="a2dfc-185">Kimlik bilgilerinizi gireceğiniz Google sitesine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="a2dfc-186">Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz web uygulamasına izin vermeniz istenir:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="a2dfc-187">**Kabul et**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-187">Click **Accept**.</span></span> <span data-ttu-id="a2dfc-188">Artık Google hesabınızı kaydedebilirsiniz MvcAuth uygulamasının **Kayıt** sayfasına geri yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="a2dfc-189">Gmail hesabınız için kullanılan yerel e-posta kaydı adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta takma adını (diğer bir şekilde kimlik doğrulama için kullandığınız e-posta) tutmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="a2dfc-190">**Kaydol'u**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="a2dfc-191">Uygulamayı Facebook'ta oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="a2dfc-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="a2dfc-192">Geçerli Facebook OAuth2 kimlik doğrulama yönergeleri için Bkz. [Facebook kimlik doğrulamayı yapılandırma](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="a2dfc-193">Üyelik Verilerini İnceleyin</span><span class="sxs-lookup"><span data-stu-id="a2dfc-193">Examine the Membership Data</span></span>

<span data-ttu-id="a2dfc-194">**Görünüm** menüsünde **Sunucu Gezgini'ni**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="a2dfc-195">**Varsayılan Bağlantıyı Genişlet (MvcAuth)**, **Tabloları**genişlet, **AspNetUsers** sağ tıklatın ve **Tablo Verilerini Göster'i**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers tablo verileri](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="a2dfc-197">Kullanıcı Sınıfına Profil Verileri Ekleme</span><span class="sxs-lookup"><span data-stu-id="a2dfc-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="a2dfc-198">Bu bölümde, aşağıdaki resimde gösterildiği gibi, kayıt sırasında kullanıcı verilerine doğum tarihi ve memleket eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![ev şehir ve Bday ile reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="a2dfc-200">*Modeller\IdentityModels.cs* dosyasını açın ve doğum tarihi ve şehir özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="a2dfc-201">*Modelleri\AccountViewModels.cs* dosyasını ve ayarlanan doğum tarihini `ExternalLoginConfirmationViewModel`ve şehir merkezi özelliklerini .</span><span class="sxs-lookup"><span data-stu-id="a2dfc-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="a2dfc-202">*Denetleyiciler\AccountController.cs* dosyasını açın ve gösterildiği gibi `ExternalLoginConfirmation` eylem yönteminde doğum tarihi ve memleketi için kod ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="a2dfc-203">*Görünümler\Hesap\ExternalLoginConfirmation.cshtml* dosyasına doğum tarihi ve şehir ekle:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="a2dfc-204">Facebook hesabınızı tekrar başvurunuzla kaydedebilmeniz ve yeni doğum tarihi ve şehir merkezi profil bilgilerini ekleyebileceğinizdoğrulayabilirsiniz diye üyelik veritabanını silin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="a2dfc-205">**Çözüm Gezgini'nden**Tüm **Dosyaları Göster** simgesini tıklatın, ardından *Veriyi Ekle\aspnet-MvcAuth-\_&lt;dateStamp&gt;.mdf'yi* tıklatın ve **Sil'i**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="a2dfc-206">**Araçlar** menüsünden **NuGet Paket Yöneticisi'ni**tıklatın, ardından Paket **Yöneticisi Konsolu'nu** (PMC) tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="a2dfc-207">PMC'de aşağıdaki komutları girin.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="a2dfc-208">Geçişleri Etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a2dfc-208">Enable-Migrations</span></span>
2. <span data-ttu-id="a2dfc-209">Ekle-Geçiş Eklentisi</span><span class="sxs-lookup"><span data-stu-id="a2dfc-209">Add-Migration Init</span></span>
3. <span data-ttu-id="a2dfc-210">Güncelleme-Veritabanı</span><span class="sxs-lookup"><span data-stu-id="a2dfc-210">Update-Database</span></span>

<span data-ttu-id="a2dfc-211">Uygulamayı çalıştırın ve bazı kullanıcılara giriş yapmak ve kayıt yaptırmak için FaceBook ve Google'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="a2dfc-212">Üyelik Verilerini İnceleyin</span><span class="sxs-lookup"><span data-stu-id="a2dfc-212">Examine the Membership Data</span></span>

<span data-ttu-id="a2dfc-213">**Görünüm** menüsünde **Sunucu Gezgini'ni**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="a2dfc-214">**AspNetUsers'ı** sağ tıklatın ve **Tablo Verilerini Göster'i**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="a2dfc-215">Ve `HomeTown` `BirthDate` alanlar aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="a2dfc-216">Uygulamanızdan Oturum Açma ve Başka Bir Hesapla Giriş</span><span class="sxs-lookup"><span data-stu-id="a2dfc-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="a2dfc-217">Facebook ile uygulamanızda oturum açar ve oturumunuzu başka bir Facebook hesabıyla (aynı tarayıcıyı kullanarak) yeniden oturum açmaya çalışırsanız, kullandığınız önceki Facebook hesabına hemen giriş yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="a2dfc-218">Başka bir hesap kullanmak için Facebook'a gidip Facebook'ta oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="a2dfc-219">Aynı kural diğer üçüncü taraf kimlik doğrulama sağlayıcısı için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="a2dfc-220">Alternatif olarak, farklı bir tarayıcı kullanarak başka bir hesapla oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2dfc-221">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a2dfc-221">Next Steps</span></span>

<span data-ttu-id="a2dfc-222">Bkz. Yahoo ve LinkedIn talimatları için Jerrie Pelser tarafından OWIN için Yahoo ve [LinkedIn OAuth güvenlik sağlayıcıları tanıtımı.](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)</span><span class="sxs-lookup"><span data-stu-id="a2dfc-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="a2dfc-223">Sosyal giriş düğmelerini etkinleştirmek için ASP.NET MVC 5 için Jerrie'nin Pretty sosyal giriş düğmelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="a2dfc-224">Öğreticimi takip edin [Auth ve SQL DB ile ASP.NET bir MVC uygulaması oluşturun ve](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bu öğreticidevam eden ve aşağıdakileri gösteren Azure Uygulama Hizmeti'ne dağıtın:</span><span class="sxs-lookup"><span data-stu-id="a2dfc-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="a2dfc-225">Uygulamanızı Azure'a nasıl dağıtılayınız.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="a2dfc-226">Nasıl rolleri ile uygulama güvenli.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="a2dfc-227">[Zorunlu Https](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) ve [Yetkilendirme](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtreleri ile uygulamanızın güvenliğini sağlama.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="a2dfc-228">Kullanıcı ve roller eklemek için üyelik API'sinin nasıl kullanılacağı.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="a2dfc-229">Lütfen bu öğreticiyi nasıl beğendiğiniz ve neler geliştirebileceğimiz hakkında geri bildirimde bırakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="a2dfc-230">Ayrıca [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)adresinden yeni konular da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="a2dfc-231">Hatta ASP.NET eklenecek yeni özellikleri isteyebilir ve oylayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="a2dfc-232">Örneğin, [kullanıcıları ve rolleri oluşturmak ve yönetmek](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use) için bir araca oy verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="a2dfc-233">ASP.NET Dış Kimlik Doğrulama Hizmetlerinin nasıl çalıştığına ilişkin iyi bir açıklama için Robert McMurray'in [Dış Kimlik Doğrulama Hizmetleri](https://asp.net/web-api/overview/security/external-authentication-services)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="a2dfc-234">Robert'ın makalesi, Microsoft ve Twitter kimlik doğrulamasını etkinleştirmede de ayrıntılı olarak yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="a2dfc-235">Tom Dykstra'nın mükemmel [EF/MVC öğreticisi](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework ile nasıl çalışılabildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2dfc-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
