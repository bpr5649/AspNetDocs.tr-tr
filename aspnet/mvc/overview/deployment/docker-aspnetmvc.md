---
uid: mvc/overview/deployment/docker-aspnetmvc
title: ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme
description: Varolan bir ASP.NET MVC uygulamasını nasıl alıp Windows Docker Kapsayıcısı'nda çalıştırılamayı öğrenin
keywords: Windows Kapsayıcılar,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675189"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme

Varolan bir .NET Framework tabanlı uygulamayı bir Windows kapsayıcısında çalıştırmak için uygulamanızda herhangi bir değişiklik gerekmez. Uygulamanızı bir Windows kapsayıcısında çalıştırmak için uygulamanızı içeren bir Docker görüntüsü oluşturun ve kapsayıcıyı başlatın. Bu konu, varolan bir [ASP.NET MVC uygulamasının](http://www.asp.net/mvc) nasıl alınıp bir Windows kapsayıcısında dağıtılanın açıklanmaktadır.

Varolan bir ASP.NET MVC uygulamasıyla başlarsınız, ardından Visual Studio'yu kullanarak yayımlanmış varlıkları oluşturursunuz. Uygulamanızı içeren ve çalıştıran resmi oluşturmak için Docker'ı kullanırsınız. Windows kapsayıcısında çalışan siteye göz atar ve uygulamanın çalıştığını doğrularsınız.

Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar. [Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.

Bir kapta çalıştıracağınız uygulama, soruları rasgele yanıtlayan basit bir web sitesidir. Bu uygulama hiçbir kimlik doğrulama veya veritabanı depolama ile temel bir MVC uygulamasıdır; web katmanını bir kapsayıcıya taşımaya odaklanmanızı sağlar. Gelecekteki konular, kapsayıcı laştırılmış uygulamalarda kalıcı depolamanın nasıl taşınacağını ve yöneteceğini gösterir.

Uygulamanızı taşımak şu adımları içerir:

1. [Görüntü için varlıkları oluşturmak için bir yayımlama görevi oluşturma.](#publish-script)
1. [Uygulamanızı çalıştıracak bir Docker görüntüsü oluşturma.](#build-the-image)
1. [Resminizi çalıştıran bir Docker kapsayıcısı başlatma.](#start-a-container)
1. [Tarayıcınızı kullanarak uygulamayı doğrulama.](#verify-in-the-browser)

[Tamamlanan uygulama](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) GitHub'da.

## <a name="prerequisites"></a>Ön koşullar

Geliştirme makinesi aşağıdaki yazılıma sahip olmalıdır:

- [Windows 10 Yıldönümü Güncelleştirmesi](https://www.microsoft.com/software-download/windows10/) (veya üstü) veya [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (veya daha yüksek)
- [Docker for Windows](https://docs.docker.com/docker-for-windows/) - sürüm Kararlı 1.13.0 veya 1.12 Beta 26 (veya daha yeni sürümler)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Windows Server 2016 kullanıyorsanız, Kapsayıcı [Ana Bilgisayar Dağıtımı - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)yönergelerini izleyin.

Docker’ı yükleyip başlattıktan sonra tepsi simgesine sağ tıklayıp **Windows kapsayıcılarına geç** öğesini seçin. Bu işlem, Windows temelinde Docker görüntülerini çalıştırmak için gereklidir. Bu komutun yürütülmesi birkaç saniye sürer:

![Windows Kapsayıcı][windows-container]

## <a name="publish-script"></a>Komut dosyası yayımlama

Bir Docker görüntüsüne yüklemeniz gereken tüm varlıkları tek bir yerde toplayın. Uygulamanız için bir yayımlama profili oluşturmak için Visual Studio **Publish** komutunu kullanabilirsiniz. Bu profil, daha sonra bu öğreticide hedef resminize kopyaladığınız tüm varlıkları tek bir dizin ağacına koyar.

**Adımları Yayımla**

1. Visual Studio'daki web projesine sağ tıklayın ve **Yayımla'yı**seçin.
1. Özel **profil düğmesini**tıklatın ve ardından yöntem olarak **Dosya Sistemi'ni** seçin.
1. Dizini seçin. Kurallara göre, indirilen `bin\Release\PublishOutput`örnek kullanır.

![Bağlantı Yayımla][publish-connection]

**Ayarlar** sekmesinin **Dosya Yayımlama Seçenekleri** bölümünü açın. **Yayımlama sırasında Precompile'yi**seçin. Bu optimizasyon, Docker kapsayıcısında görünümleri derlettiğiniz, önceden derlenmiş görünümleri kopyaladığınız anlamına gelir.

![Ayarları Yayımla][publish-settings]

**Yayımla'yı**tıklatın ve Visual Studio gerekli tüm varlıkları hedef klasöre kopyalar.

## <a name="build-the-image"></a>Görüntü oluşturma

Docker resminizi tanımlamak için *Dockerfile* adında yeni bir dosya oluşturun. *Dockerfile* son görüntüyü oluşturmak için talimatlar içerir ve herhangi bir temel görüntü adları, gerekli bileşenleri, çalıştırmak istediğiniz uygulama ve diğer yapılandırma görüntüleri içerir. *Dockerfile* görüntüyü oluşturan `docker build` komuta giriştir.

Bu alıştırma için, Docker `microsoft/aspnet` [Hub'da](https://hub.docker.com/r/microsoft/aspnet/)bulunan görüntüye dayalı bir görüntü oluşturacaksınız.
Temel görüntü, `microsoft/aspnet`bir Windows Server görüntüsüdür. Windows Server Core, IIS ve 4.7.2 ASP.NET içerir. Bu resmi kapsayıcınızda çalıştırdığınızda, otomatik olarak IIS ve yüklü web siteleri başlatılır.

Resminizi oluşturan Dockerfile aşağıdaki gibi görünür:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

Bu Dockerfile içinde bir `ENTRYPOINT` komutu yoktur. Gerekli değildir. IIS ile Windows Server çalıştırırken, IIS işlemi aspnet temel görüntüde başlamak üzere yapılandırılan giriş noktasıdır.

ASP.NET uygulamanızı çalıştıran görüntüyü oluşturmak için Docker build komutunu çalıştırın. Bunu yapmak için, projenizin dizininde bir PowerShell penceresi açın ve çözüm dizinine aşağıdaki komutu yazın:

```console
docker build -t mvcrandomanswers .
```

Bu komut, Dockerfile'nizdeki yönergeleri kullanarak yeni görüntüyü oluşturur ve görüntüyü mvcrandomanswers olarak adlandır (-t etiketleme) verir. Bu, temel görüntüyü [Docker Hub'dan](http://hub.docker.com)çekmeyi ve uygulamanızı bu resme eklemeyi içerebilir.

Bu komut tamamlandıktan sonra, `docker images` yeni görüntü hakkındaki bilgileri görmek için komutu çalıştırabilirsiniz:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

GÖRÜNTÜ Kimliği makinenizde farklı olacaktır. Şimdi, uygulamayı çalıştıralım.

## <a name="start-a-container"></a>Bir kapsayıcı başlatma

Aşağıdaki `docker run` komutu çalıştırarak bir kapsayıcı başlatın:

```console
docker run -d --name randomanswers mvcrandomanswers
```

Bağımsız `-d` değişken, Docker'a görüntüyü müstakil modda başlatmasını söyler. Bu, Docker görüntüsünün geçerli kabuktan bağlantısının kesildiği anlamına gelir.

Birçok docker örneğinde, -p konteyner ve ana bağlantı noktaları harita görebilirsiniz. Varsayılan aspnet görüntüsü, konteyneri 80 bağlantı noktasında niçin dinleyecek ve ortaya çıkaracak şekilde yapılandırdı.

Çalışan `--name randomanswers` kapsayıcıya bir ad verir. Çoğu komutta kapsayıcı kimliği yerine bu adı kullanabilirsiniz.

Başletmek `mvcrandomanswers` için görüntünün adıdır.

## <a name="verify-in-the-browser"></a>Tarayıcıda doğrula

Kapsayıcı başladıktan sonra, gösterilen örnekte kullanarak `http://localhost` çalışan kapsayıcıya bağlanın. Bu URL'yi tarayıcınıza yazın ve çalışan siteyi görmeniz gerekir.

> [!NOTE]
> Bazı VPN veya proxy yazılımları sitenizde gezinmenizi engelleyebilir.
> Kapsayıcınızın çalıştığından emin olmak için geçici olarak devre dışı kullanabilirsiniz.

GitHub'daki örnek dizini, bu komutları sizin için yürüten bir [PowerShell komut dosyası](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) içerir. PowerShell penceresi açın, çözüm dizininizde dizin değiştirin ve yazın:

```console
./run.ps1
```

Yukarıdaki komut görüntüyü oluşturur, makinenizdeki görüntülerin listesini görüntüler ve bir kapsayıcı başlatır.

Kapsayıcınızı durdurmak için `docker stop` bir komut sorun:

```console
docker stop randomanswers
```

Kapsayıcıyı kaldırmak için `docker rm` bir komut düzenleyin:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows Kapsayıcısına Geçiş"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Dosya Sistemine Yayımla"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Ayarları Yayımla"
