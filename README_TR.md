---
marp: true
theme: firat-theme
class:
  - lead
  - invert



---
<!-- _footer: Fırat GÜRSOY - Kıdemli Yazılım Geliştirici / Mayıs 2021--> 


# Konumuz
![w:300](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/logo.svg)

#
![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)

---
# Soru ve problem neydi?
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-why-java-slow.png)

---
# Ne yapabiliriz?
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-java-performance.png)

---
# Peki çözüm nedir?
![java](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic1.png)![4ever](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic2.png)

---
# GraalVM nedir?

'GraalVM', 'Java' ve diğer JVM dillerinde yazılmış **uygulamaların yürütülmesini hızlandırmak** için tasarlanmış **yüksek performanslı** bir JDK dağıtımıdır ve 'JavaScript', 'Ruby', 'Python' ve **_bir dizi başka popüler dil_**. `GraalVM`nin çok dilli yetenekleri, **_yabancı dil arama maliyetlerini ortadan kaldırırken_** birden çok programlama dilini tek bir uygulamada karıştırmayı mümkün kılar.
`Oracle` tarafından oluşturulan `GraalVM`. Üretime hazır ilk sürüm olan ``GraalVM 19.0``, ``Mayıs 2019``da yayınlandı. GraalVM'nin yaptığına eşdeğer bir başka teknoloji yoktur.

---
# GraalVM bana ne verebilir?
* Tek bir uygulamada birden fazla programlama dilini karıştırmak
* Yerel yürütülebilir dosyalar
* ``İnanılmaz`` hızlı önyükleme süresi
* İnanılmaz derecede ``düşük RSS belleği`` (yalnızca yığın boyutu değil!)
* ``Kubernetes`` gibi kapsayıcı düzenleme platformlarında anında (nispeten) ölçek büyütme ve yüksek yoğunluklu bellek kullanımı.
---

# GraalVM Mimarisi

![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/architecture.png)

---
# Yerel yürütülebilir dosyalar

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/native-executable-process.png)

###### Uygulamamız için ``yerel yürütülebilir dosya``, ``uygulama kodu``, ``gerekli kütüphaneler``, ``Java API'leri`` ve ``bir sanal makinenin küçültülmüş sürümü``nü içerecektir. `. Daha küçük VM tabanı, uygulamanın ``başlangıç zamanını`` iyileştirir ve ``minimum disk ayak izi`` üretir.

---

# Truffle dil uygulama çatısı

Truffle dil uygulama çatısı kendi kendini değiştiren Soyut Sözdizimi Ağaçları için yorumlayıcılar olarak araçlar ve programlama dilleri uygulamaları oluşturmaya yönelik açık kaynaklı bir kitaplıktır. Açık kaynak GraalVM derleyicisi ile birlikte, ``Truffle, mevcut dinamik diller çağında programlama dili uygulama teknolojisinde önemli bir adımı temsil ediyor.``

---
# Desteklenen çatılar ve teknolojiler

* Spring Framework (Deneyimsel)
* Quarkus
* Play Framework
* Camel
* Prometheus
* JavaFX
...

---
# Dezavantajlar

* Bu yaklaşımın ana dezavantajı, platforma bağlı yerel koddur.

Bu, linux/windows vb. için kaynak kodunu derlemeniz gerektiği anlamına gelir.

---
<!-- 
class:
  - uncover
  - invert
 -->

# O esnada 

###### ``SystemAdmin01:`` server_api.so sunucumda çalışmıyor !
###### ``Müşteri$$$__:`` customer_api.exe bilgisayarımda çalışmıyor!
###### ``DevGuy42_____:`` api.jar iş istasyonumda çalışıyor!
###### ``Fırat________:`` Bazı durumlarda kullanılan kitaplıklardan veya derleme komut dosyalarından sorunlar çıkabilir. Yani **testlere** dikkat etmek gerekiyor.
###### ``SystemAdmin01:`` hımm, server_api.so benim sunucumda çalışmıyor !
###### ................................................................
###### ``DevGuy42 yazıyor ...``

---

# Örnek Uygulama : İlk adım

Oracle indirmelerinden GraalVM'yi indirin ve kurun. Bir ``Example.java`` dosyası oluşturun.

```java
public class Example {

    public static void main(String[] args) {
        System.out.println("Hello GraalVM");
    }
}
```

```shell
#Aşağıdaki komutları çalıştırın:
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
Quarkus Testi

---
# Şuan Kullanılabilir mi?

GraalVM teknolojileri, üretime hazır ve deneysel olarak dağıtılır.

GraalVM'nin gelecekteki sürümleri için deneysel özellikler değerlendirilmektedir ve üretimde kullanılması amaçlanmamıştır. Geliştirme ekibi, deneysel özelliklerle ilgili geri bildirimleri memnuniyetle karşılar, ancak kullanıcılar, deneysel özelliklerin hiçbir zaman son sürüme dahil edilmeyebileceğini veya üretime hazır kabul edilmeden önce önemli ölçüde değişebileceğini bilmelidir.

---
Bu bilgiden sonra bireysel ihtiyacım için bir demo uygulaması yapmaya çalıştım.

Öncelikle şık kullanıcı arayüzüne sahip bir masaüstü uygulamasını tercih ettim.
(Nispeten:))

Bu, uygulamanın ne yazık ki çok fazla bellek kullandığı anlamına gelir. Bu yüzden performansı artırmak için ``JavaFX`` ve ayrıca ``Gluon`` (yerel bir JavaFX çözümü) kullanmam gerekiyor.


---
# Graalvm entegrasyonu için ne yaptım?

Bu entegrasyon için sadece maven pom'uma bir eklenti ekledim. Şaşırtıcı bir şekilde, entegrasyon için bu yeterlidir.

---

```xml
<plugin>
	<groupId>com.gluonhq</groupId>
	<artifactId>gluonfx-maven-plugin</artifactId>
	<version>1.0.2</version>
	<configuration>
		<target>host</target>
		<mainClass>com.gnosis.cuteoverlay.Application</mainClass>
		<reflectionList>
			<list>com.gnosis.cuteoverlay.Application</list>
			<list>com.gnosis.cuteoverlay.DataToSend</list>
			<list>com.gnosis.cuteoverlay.DataToSendContainer</list>
		</reflectionList>
		<graalvmHome>C:\dev\tools\graalvm-svm-windows-gluon-21.2.0-dev</graalvmHome>
		<nativeImageArgs>
			<imageArg>-Dio.netty.noUnsafe=true</imageArg>
			<imageArg>--report-unsupported-elements-at-runtime</imageArg>
			<imageArg>--allow-incomplete-classpath --enable-all-security-services</imageArg>
			<imageArg>--enable-url-protocols=https -H:EnableURLProtocols=http</imageArg>
			<imageArg>-H:TraceClassInitialization=true</imageArg>
			<imageArg>--initialize-at-build-time=${buildtime-classes}</imageArg>
			<imageArg>--initialize-at-run-time=${runtime-classes}</imageArg>
		</nativeImageArgs>
	</configuration>
</plugin>
```
---

Ana zaman harcama sorunu, derleme ve çalışma zamanı sınıflarını ayrıca Java'nın Reflection ı tarafından kullanılanları sınıflara ayırmaktır. Ayrıca bu listeler hangi kütüphaneleri kullandığınıza bağlıdır.

Birkaç denemeden sonra exe başarıyla hazırlandı.

```shell
#yerel çalıştıralabilir dosyayı hazırlar
mvn gluonfx:build
```

Bundan sonra, exeyi ve iş mantığını çalıştırmak için ihtiyaç duyduğum diğer tüm yürütülebilir dosyaları kopyaladığım bir dağıtım klasörü oluşturdum.

---

# ve sonunda

![w:1024](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/demoapp.png)

---
# Uygulamadan başlangıç zamanı metrikleri


```shell
# Jar Log
Uptime:781ms
StartTime:Wed Jun 30 02:02:09 EET 2021
Max heap memory is 4086 MBytes
Used non-heap memory is 32 MBytes
```

```shell
# Native Image(exe) Log
Uptime:1ms
StartTime:Wed Jun 30 02:06:14 TRT 2021
Max heap memory is 0 MBytes
Used non-heap memory is 0 MBytes
```

Yıldırım hızında jvm başlangıç zamanı!

---
# İşletim sisteminde gözüken bellek kullanımları

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/cute_memory_usage.png)

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/cute_memory_usage_jar.png)


Bellek kullanımından 200MB tasarruf sağladık!

---

<!-- _footer: Fırat GÜRSOY - Kıdemli Yazılım Geliştirici / Mayıs 2021--> 
# Özellikle Teşekkürler !

* Oracle, Quarkus, JavaFX / GluonHQ, Spring
* Google and Wiki
* ![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)

Kaynak koduna ve windows buildlerine git üzerinden ulaşabilirsiniz.

https://github.com/firatgursoy/CuteOverlay