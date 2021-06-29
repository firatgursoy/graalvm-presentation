---
marp: true
theme: firat-theme
class:
  - lead
  - invert



---
<!-- _footer: Fırat GÜRSOY - Kıdemli Yazılım Geliştirici / May 2021--> 


# Hakkında
![w:300](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/logo.svg)

#
![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)

---
# Soru şuydu
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-why-java-slow.png)

---
# Ne yapabiliriz ?
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-java-performance.png)

---
# Çözüm Nedir?
![java](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic1.png)![4ever](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic2.png)

---
# GraalVM Nedir ?
`GraalVM`, `Java` ve diğer JVM dillerinde yazılmış **uygulamaların yürütülmesini hızlandırmak** için tasarlanmış **yüksek performanslı** bir JDK dağıtımıdır ve `JavaScript`, `Ruby`, `Python` ve **_bir dizi başka popüler dil_**. `GraalVM`in çok dilli yetenekleri, **_yabancı dil arama maliyetlerini ortadan kaldırırken_** birden çok programlama dilini tek bir uygulamada karıştırmayı mümkün kılar.

---
# GraalVM bana ne verir ?
* Tek bir uygulamada birden fazla programlama dilini karıştırın
* Yerel yürütülebilir dosyalar
* ``İnanılmaz`` hızlı önyükleme süresi
* İnanılmaz derecede ``düşük RSS belleği`` (yalnızca yığın boyutu değil!)
* ``Kubernetes`` gibi kapsayıcı düzenleme platformlarında anında (nispeten) ölçek büyütme ve yüksek yoğunluklu bellek kullanımı.

---

# GraalVM Mimarisi

![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/architecture.png)

---
# Yerel Yürütülebilir Dosyalar

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/native-executable-process.png)

###### Uygulamamız için ``yerel yürütülebilir dosya``; ``uygulama kodu``, ``gerekli kitaplıklar``, ``Java API'ları`` ve ``bir sanal makinenin küçültülmüş sürümü``nü içerecektir. Daha küçük VM tabanı, uygulamanın ``başlangıç zamanını`` iyileştirir ve ``minimum disk ayak izi`` üretir.

---

# Truffle dil uygulama çerçevesi

Truffle dili uygulama çerçevesi (bundan böyle "Truffle"), kendi kendini değiştiren Soyut Sözdizimi Ağaçları için yorumlayıcılar olarak araçlar ve programlama dilleri uygulamaları oluşturmak için açık kaynaklı bir kitaplıktır. Açık kaynak GraalVM derleyicisi ile birlikte, ``Truffle, mevcut dinamik diller çağında programlama dili uygulama teknolojisinde önemli bir adımı temsil ediyor.``

---
# Desteklenen Çerçeveler ve Teknoloji

* Spring Framework (Experimental)
* Quarkus
* Play Framework
* Camel
* Prometheus
* JavaFX
...

---
# Dezavantajları

* Bu yaklaşımın ana dezavantajı, platforma bağlı yerel koddur.

Bu, linux/windows vb. için kaynak kodunu derlemeniz gerektiği anlamına gelir.

---
<!-- 
class:
  - uncover
  - invert
 -->

# Yani ??

###### ``SystemAdmin01:`` server_api.so sunucumda çalışmıyor !
###### ``Customer$$$__:`` customer_api.exe bilgisayarımda çalışmıyor!
###### ``DevGuy42_____:`` api.jar iş istasyonumda çalışıyor!
###### ``Fırat________:`` Bazı durumlarda kullanılan kitaplıklardan veya derleme komut dosyalarından sorunlar çıkabilir. Yani **testlere** dikkat etmek gerekiyor.
###### ``SystemAdmin01:`` hımm, server_api.so benim sunucumda çalışmıyor !
###### ................................................................
###### ``DevGuy42 yazıyor ...``

---

# Örnek Uygulama

Oracle indirmelerinden GraalVM'i indirin ve kurun. Bir ``Example.java`` dosyası oluşturun.

```java
public class Example {

    public static void main(String[] args) {
        System.out.println("Merhaba GraalVM");
    }
}
```

```shell
#Bu komutları çağırın :
javac Example.java
native-image Example
```

---

<!-- 
class:
  - lead
  - invert
 -->

# Testler : Tabiki

```java
package org.acme.quickstart;


import io.quarkus.test.junit.NativeImageTest;

@NativeImageTest 
public class NativeGreetingResourceIT extends GreetingResourceTest { 
    // Run the same tests
}
```

---
# Performans

![w:1024](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/quarkus_test.png)
Quarkus Testleri

---
Bu deneyimden sonra ihtiyacım için bir demo uygulaması yaptım. Başlangıç ve bellek ayak izini gerçekten önemli ölçüde azaltıyor. :)

![w:1024](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/demoapp.png)

---

# Destek

GraalVM teknolojileri, üretime hazır ve deneysel olarak dağıtılır.

GraalVM'nin gelecekteki sürümleri için deneysel özellikler değerlendirilmektedir ve üretimde kullanılması amaçlanmamıştır. Geliştirme ekibi, deneysel özelliklerle ilgili geri bildirimleri memnuniyetle karşılar, ancak kullanıcılar, deneysel özelliklerin hiçbir zaman son sürüme dahil edilmeyebileceğini veya üretime hazır kabul edilmeden önce önemli ölçüde değişebileceğini bilmelidir.

---
<!-- _footer: Fırat GÜRSOY - Senior Software Developer / May 2021--> 
# Teşekkürler

* Oracle
* Quarkus
* Spring
* JavaFX / GluonHQ
* Google and Wiki
* ![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)
