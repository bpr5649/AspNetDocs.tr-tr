---
title: ASP.NET Core Grunt kullanma
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2016
uid: client-side/using-grunt
ms.openlocfilehash: 21fa565c930563bbc819c2a02ea71655193513d0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073590"
---
# <a name="use-grunt-in-aspnet-core"></a>ASP.NET Core Grunt kullanma

Tarafından [Noel pirinç](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)

Grunt betik küçültme, TypeScript derleme, kod kalitesini "lint" araçları, CSS ön işlemci ve neredeyse tüm istemci geliştirme desteği için yapmanız gereken yinelenen işi otomatikleştiren bir JavaScript görev Çalıştırıcı ' dir. ASP.NET proje şablonları, varsayılan olarak Gulp kullanır ancak grunt Visual Studio'da tam olarak desteklenir (bkz [kullanın Gulp](using-gulp.md)).

Bu örnek, boş bir ASP.NET Core projesi sıfırdan istemci derleme işlemini otomatik hale getirmek nasıl göstermek için başlangıç noktası olarak kullanır.

Tamamlanan örnek hedef dağıtım dizinine temizler, JavaScript dosyaları birleştirir, kod kalitesini denetler, JavaScript dosya içeriği toplar ve web uygulamanızın kök dizinine dağıtır. Aşağıdaki paketler kullanacağız:

* **grunt**: Grunt görev Çalıştırıcı paket.

* **grunt contrib temiz**: Dosyaları veya dizinleri kaldıran bir eklenti.

* **grunt-contrib-jshint**: JavaScript kod kalitesini gözden geçirmeleri bir eklenti.

* **grunt contrib concat**: Bir eklenti dosyalarını tek bir dosya halinde birleştirir.

* **grunt contrib uglify**: Bir eklenti boyutunu azaltmak için JavaScript küçültür.

* **grunt contrib watch**: Dosya etkinliği izleyen bir eklenti.

## <a name="preparing-the-application"></a>Uygulama hazırlama

Başlamak için yeni bir boş web uygulaması oluşturma ve TypeScript örnek dosyaları ekleyin. TypeScript dosyalarını otomatik olarak varsayılan Visual Studio ayarları kullanarak JavaScript ile derlenen ve Grunt kullanarak işlemek için sunduğumuz ham madde olacaktır.

1.  Visual Studio'da yeni bir oluşturma `ASP.NET Web Application`.

2.  İçinde **yeni ASP.NET projesi** iletişim kutusunda, ASP.NET Core seçin **boş** şablon ve Tamam düğmesine tıklayın.

3.  Çözüm Gezgini'nde proje yapısını inceleyin. `\src` Klasörünü de içeren boş `wwwroot` ve `Dependencies` düğümleri.

    ![boş web çözümü](using-grunt/_static/grunt-solution-explorer.png)

4.  Adlı yeni bir klasör eklemek `TypeScript` proje dizininiz için.

5.  Tüm dosyalar eklemeden önce Visual Studio seçeneği bulunduğundan emin ' derleme kaydederken ' işaretli TypeScript dosyaları için. Gidin **Araçları** > **seçenekleri** > **metin düzenleyici** > **Typescript**  >  **Proje**:

    ![TypeScript dosyalarının otomatik compliation ayarlama seçenekleri](using-grunt/_static/typescript-options.png)

6.  Sağ `TypeScript` dizin ve select **Ekle > Yeni öğe** bağlam menüsünden. Seçin **JavaScript dosyası** öğe ve dosya adı *Tastes.ts* (Not \*.ts uzantısı). TypeScript kod satırının dosyaya kopyalayın (kaydettiğinizde, yeni bir *Tastes.js* dosya ile JavaScript kaynak görünür).
    
    ```typescript
    enum Tastes { Sweet, Sour, Salty, Bitter }
    ```

7.  İkinci bir dosya ekleyin **TypeScript** dizin ve adlandırın `Food.ts`. Dosyaya aşağıdaki kodu kopyalayın.

    ```typescript
    class Food {
      constructor(name: string, calories: number) {
        this._name = name;
        this._calories = calories;
      }
    
      private _name: string;
      get Name() {
        return this._name;
      }
    
      private _calories: number;
      get Calories() {
        return this._calories;
      }
    
      private _taste: Tastes;
      get Taste(): Tastes { return this._taste }
      set Taste(value: Tastes) {
        this._taste = value;
      }
    }
    ```

## <a name="configuring-npm"></a>NPM yapılandırma

Ardından, NPM, grunt ve grunt görevlerini indirmek için yapılandırın.

1. Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle > Yeni öğe** bağlam menüsünden. Seçin **NPM yapılandırma dosyası** öğesi, varsayılan adı bırakın *package.json*, tıklatıp **Ekle** düğmesi.

2. İçinde *package.json* içinde dosya `devDependencies` nesne küme ayraçları, "grunt" girin. Seçin `grunt` IntelliSense'de listesinde ve Enter tuşuna basın. Visual Studio teklifi grunt paket adı ve bir iki nokta üst üste ekleyin. İki nokta üst üste sağında, IntelliSense listesini üst kısmından paketin en son kararlı sürümünü seçin (basın `Ctrl-Space` IntelliSense görünmüyorsa).

    ![grun IntelliSense](using-grunt/_static/devdependencies-grunt.png)
    
    > [!NOTE]
    > NPM kullanan [semantic versioning](http://semver.org/) bağımlılıkları düzenlemek için. SemVer olarak da bilinen semantik sürüm oluşturma, numaralandırma düzeni ile paketleri tanımlayan <major>.<minor>. <patch>. IntelliSense, yalnızca birkaç genel seçenek göstererek semantic versioning basitleştirir. Üst öğeyi IntelliSense listesinde (yukarıdaki örnekte 0.4.5) paketin en son kararlı sürüm olarak kabul edilir. Şapka (^) simgesi en son sürümle eşleşen ve son ikincil sürümle tilde (~) ile eşleşir. Bkz: [NPM semver sürümü çözümleyici başvurusu](https://www.npmjs.com/package/semver) SemVer sağlayan tam expressivity kılavuzu olarak.

3. Yüklemek için daha fazla bağımlılıkları grunt Ekle-contrib -\* için paketler *temiz*, *jshint*, *concat*, *uglify*ve *watch* aşağıdaki örnekte gösterildiği gibi. Sürümleri örnekle eşleşmesi gerekmez.

    ```json
    "devDependencies": {
      "grunt": "0.4.5",
      "grunt-contrib-clean": "0.6.0",
      "grunt-contrib-jshint": "0.11.0",
      "grunt-contrib-concat": "0.5.1",
      "grunt-contrib-uglify": "0.8.0",
      "grunt-contrib-watch": "0.6.1"
    }
    ```

4. Kaydet *package.json* dosya.

Her paket için gerekli tüm dosyaları ile birlikte her devDependencies öğesi paketleri indirir. Paket dosyaları bulabilirsiniz `node_modules` etkinleştirerek dizin **tüm dosyaları göster** Çözüm Gezgini'nde düğmesi.

![grunt node_modules](using-grunt/_static/node-modules.png)

> [!NOTE]
> Gerek duyarsanız, el ile bağımlılıkları Çözüm Gezgini'nde sağ tıklayarak geri yükleyebilirsiniz `Dependencies\NPM` seçerek **paketleri geri** menü seçeneği.

![Paketleri geri yükle](using-grunt/_static/restore-packages.png)

## <a name="configuring-grunt"></a>Grunt yapılandırma

Grunt adlı bir bildiri kullanarak yapılandırılmış *Gruntfile.js* tanımlar, yükler ve el ile çalıştırmak veya Visual Studio'da olaylara göre otomatik olarak çalıştırılmak için yapılandırılan görevleri kaydeder.

1. Projeye sağ tıklayıp **Ekle > Yeni öğe**. Seçin **Grunt yapılandırma dosyası** seçeneği, varsayılan adı bırakın *Gruntfile.js*, tıklatıp **Ekle** düğmesi.

   Başlangıç kodunu bir modül tanımı içerir ve `grunt.initConfig()` yöntemi. `initConfig()` Her paket için seçenekleri ayarlamak için kullanılır ve modül geri kalanında yüklemek ve görevleri kaydedin.
    
   ```javascript
   module.exports = function (grunt) {
     grunt.initConfig({
     });
   };
   ```

2. İçinde `initConfig()` yöntemi eklemek için Seçenekler `clean` örnekte gösterildiği gibi görev *Gruntfile.js* aşağıda. Temizleme görevini, bir dizi dizin dizeleri kabul eder. Bu görev dosyaları wwwroot/lib ve tamamını/temp dizini kaldırır.

    ```javascript
    module.exports = function (grunt) {
      grunt.initConfig({
        clean: ["wwwroot/lib/*", "temp/"],
      });
    };
    ```

3. İnitConfig() yöntemi bir çağrı ekleyin `grunt.loadNpmTasks()`. Bu görev çalıştırılabilir Visual Studio'dan yapar.

    ```javascript
    grunt.loadNpmTasks("grunt-contrib-clean");
    ```

4. Kaydet *Gruntfile.js*. Dosya aşağıdaki ekran gibi görünmelidir.

    ![ilk gruntfile](using-grunt/_static/gruntfile-js-initial.png)

5. Sağ *Gruntfile.js* seçip **görev Çalıştırıcı Gezgini** bağlam menüsünden. Görev Çalıştırıcı Gezgini penceresi açılır.

    ![Görev Çalıştırıcı Gezgini menüsü](using-grunt/_static/task-runner-explorer-menu.png)

6. Doğrulayın `clean` altında gösterir **görevleri** görev Çalıştırıcı Gezgini içinde.

    ![Görev Çalıştırıcı Gezgini görev listesi](using-grunt/_static/task-runner-explorer-tasks.png)

7. Temizleme görevini sağ tıklayıp **çalıştırma** bağlam menüsünden. Bir komut penceresi, görevin ilerleme durumunu görüntüler.

    ![Görev Çalıştırıcı Gezgini çalıştırma temizleme görevini](using-grunt/_static/task-runner-explorer-run-clean.png)
    
    > [!NOTE]
    > Dosyaları veya dizinleri henüz temizlemek için yoktur. İsterseniz, bunları Çözüm Gezgini'nde el ile oluşturmanız ve ardından bir test olarak temizleme görevini çalıştırın.
    
8. İnitConfig() yöntemi eklemek için bir giriş `concat` aşağıdaki kodu kullanarak.

    `src` Özellik dizisi, bunlar birleştirilmelidir, sırayla birleştirmek için dosyaları listeler. `dest` Özelliği üretilen birleşik bir dosyaya yol atar.

    ```javascript
    concat: {
      all: {
        src: ['TypeScript/Tastes.js', 'TypeScript/Food.js'],
        dest: 'temp/combined.js'
      }
    },
    ```
    
    > [!NOTE]
    > `all` Yukarıdaki kod özelliğinde bir hedef adıdır. Hedefleri, bazı Grunt görevleri birden çok yapı ortamları izin vermek için kullanılır. IntelliSense kullanarak yerleşik hedefleri görüntüle veya kendi atayın.
    
9. Ekleme `jshint` aşağıdaki kodu kullanarak görev.

    Geçici dizinde bulunan her bir JavaScript dosyası karşı jshint kod kalitesini yardımcı programını çalıştırın.
    
    ```javascript
    jshint: {
      files: ['temp/*.js'],
      options: {
        '-W069': false,
      }
    },
    ```

    > [!NOTE]
    > Seçenek "-W069" JavaScript kullanır, yani noktalı gösterim yerine bir özellik atamak için söz dizimi köşeli ayraç olduğunda bir hata jshint tarafından üretilen `Tastes["Sweet"]` yerine `Tastes.Sweet`. Seçeneği, rest işleminin devam etmesine izin vermek için uyarı devre dışı bırakır.

10. Ekleme `uglify` aşağıdaki kodu kullanarak görev.

    Görev küçültür *combined.js* dosya geçici dizinde bulunan ve wwwroot / standart bir adlandırma kuralının LIB sonuç dosyası oluşturur  *\<dosya adı\>. min.js*.
    
    ```javascript
    uglify: {
     all: {
       src: ['temp/combined.js'],
       dest: 'wwwroot/lib/combined.min.js'
     }
    },
    ```

11. Grunt contrib temiz yükleyen çağrı grunt.loadNpmTasks() altında aşağıdaki kodu kullanarak uglify ve jshint, concat aynı çağrısı içerir.
    
    ```javascript
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-concat');
    grunt.loadNpmTasks('grunt-contrib-uglify');
    ```

12. Kaydet *Gruntfile.js*. Dosya aşağıdaki örnek gibi görünmelidir.

    ![tam grunt dosyası örneği](using-grunt/_static/gruntfile-js-complete.png)

13. Görev Çalıştırıcı Gezgini Görevler listesini içeren bir bildirim `clean`, `concat`, `jshint` ve `uglify` görevleri. Her görev sıraya göre çalıştırın ve Çözüm Gezgini'nde sonuçlarını gözlemleyin. Her görev hatasız çalışmalıdır.
    
    ![Görev Çalıştırıcı Gezgini her görevi çalıştır](using-grunt/_static/task-runner-explorer-run-each-task.png)
    
    Concat görev yeni bir oluşturur *combined.js* dosya ve geçici dizine yerleştirir. Jshint görevi yalnızca çalışır ve çıktı oluşturmuyor. Yeni bir uglify görev oluşturur *combined.min.js* dosya ve wwwroot/lib yerleştirir. Tamamlandığında, çözüm aşağıdaki ekran görüntüsüne benzer görünmelidir:
    
    ![Çözüm Gezgini tüm görevler](using-grunt/_static/solution-explorer-after-all-tasks.png)
    
    > [!NOTE]
    > Her bir paket için seçenekleri hakkında daha fazla bilgi için ziyaret [ https://www.npmjs.com/ ](https://www.npmjs.com/) ve arama ana sayfada arama kutusuna paket adı. Örneğin, tüm parametrelerinin açıklayan bir belge bağlantısını almak için grunt contrib temiz paketi bakabilirsiniz.

### <a name="all-together-now"></a>Özet

Grunt kullanma `registerTask()` belirli bir sırayla bir dizi görevi çalıştırmak için yöntemi. Örneğin, yukarıdaki adımları sırayla temiz -> örneği çalıştırmak için concat -> jshint -> uglify, modüle aşağıdaki kodu ekleyin. Kod initConfig dışında loadNpmTasks() çağrıları ile aynı düzeyde eklenmesi gerekir.

```javascript
grunt.registerTask("all", ['clean', 'concat', 'jshint', 'uglify']);
```

Yeni görevin görev Çalıştırıcı Gezgini diğer ad görevleri altında görünür. Sağ tıklayın ve diğer görevler gibi çalıştırın. `all` Görevin çalışacağını `clean`, `concat`, `jshint` ve `uglify`, sırasıyla.

![diğer ad grunt görevleri](using-grunt/_static/alias-tasks.png)

## <a name="watching-for-changes"></a>Değişiklikleri izleniyor

A `watch` dosyaları ve dizinleri görev tutar. Değişiklik algılarsa izleme görevleri otomatik olarak tetikler. İnitConfig değişiklikleri izlemek için aşağıdaki kodu ekleyin \*TypeScript dizinde .js dosyası. Bir JavaScript dosyası değiştirilirse, `watch` çalışacak `all` görev.

```javascript
watch: {
  files: ["TypeScript/*.js"],
  tasks: ["all"]
}
```

Bir çağrı ekleyin `loadNpmTasks()` gösterilecek `watch` görev Çalıştırıcı Gezgini görevi.

```javascript
grunt.loadNpmTasks('grunt-contrib-watch');
```

Görev Çalıştırıcı Gezgini izleme görevi sağ tıklayın ve bağlam menüsünden Çalıştır'ı seçin. İzleme görev çalıştırma gösteren komut penceresinde bir "bekleniyor..." görüntülenir İleti. TypeScript dosyaları birini açın, bir alan ekleyin ve ardından dosyayı kaydedin. Bu izleme tetikleyici ve sırayla çalışması diğer görevlerini tetikleyin. Aşağıdaki ekran görüntüsünde, bir örnek çalıştırmayı gösterir.

![çalışan görevleri çıkış](using-grunt/_static/watch-running.png)

## <a name="binding-to-visual-studio-events"></a>Visual Studio olaylara bağlama

Visual Studio'daki çalışmalar her zaman el ile görevlerinizi başlatmak istediğiniz sürece, görevler bağlayabilirsiniz **önce yapı**, **sonra yapı**, **temiz**, ve  **Proje Aç** olayları.

Şimdi bağlama `watch` böylece Visual Studio her açtığında çalıştırır. Görev Çalıştırıcı Gezgini, izleme görev sağ tıklatın ve seçin **bağlamaları > Proje Aç** bağlam menüsünden.

![bir görev için proje açma bağlama](using-grunt/_static/bindings-project-open.png)

Kaldırın ve projeyi yeniden yükleyin. Projeyi yeniden yüklediğinde, izleme görev otomatik olarak çalıştırarak başlayın.

## <a name="summary"></a>Özet

Grunt, çoğu istemci derleme görevleri otomatik hale getirmek için kullanılan bir güçlü görev Çalıştırıcı ' dir. Grunt, NPM, paketleri ve araçları Visual Studio ile tümleştirme özelliklerini sunmak için yararlanır. Görev Çalıştırıcı Gezgini Visual Studio'nun, yapılandırma dosyalarındaki değişiklikleri algılar ve görevleri çalıştırmak, çalışmakta olan görevlerin görüntüleyin ve görevler için Visual Studio olaylar bağlamak için kullanışlı bir arabirim sağlar.

## <a name="additional-resources"></a>Ek kaynaklar

   * [Gulp kullanma](using-gulp.md)
