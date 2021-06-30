---
marp: true
theme: firat-theme
class:
  - lead
  - invert



---
<!-- _footer: Fırat GÜRSOY - Senior Software Developer / May 2021--> 


# About
![w:300](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/logo.svg)

#
![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)

---
# The question is
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-why-java-slow.png)

---
# What we can do?
![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/frame-java-performance.png)

---
# So what is the solution?
![java](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic1.png)![4ever](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/comic2.png)

---
# What is GraalVM ?

`GraalVM` is a **high-performance** JDK distribution designed to **accelerate the execution of applications** written in `Java` and other JVM languages along with support for `JavaScript`, `Ruby`, `Python` and **_a number of other popular languages_**. `GraalVM`’s polyglot capabilities make it possible to mix multiple programming languages in a single application while **_eliminating foreign language call costs_**.
`GraalVM` created by ``Oracle``. The first production-ready version, ``GraalVM 19.0``, was released in ``May 2019``. There is no equivalent technology what GraalVM do.

---
# What can GraalVM give me?
* Mix multiple programming languages in a single application 
* Native executables
* ``Amazingly`` fast boot time
* Incredibly ``low RSS memory`` (not just heap size!)
* Instant (relatively) scale up and high density memory utilization in container orchestration platforms like ``Kubernetes``.

---

# GraalVM Architecture

![w:800](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/architecture.png)

---
# Native Image


![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/native-executable-process.png)

###### The ``native executable`` for our application will contain the ``application code``, ``required libraries``, ``Java APIs``, and ``a reduced version of a VM``. The smaller VM base improves the ``startup time`` of the application and produces a ``minimal disk footprint``.


---

# Truffle language implementation framework 

The Truffle language implementation framework (henceforth “Truffle”) is an open source library for building tools and programming languages implementations as interpreters for self-modifying Abstract Syntax Trees. Together with the open source GraalVM compiler, ``Truffle represents a significant step forward in programming language implementation technology in the current era of dynamic languages.``

---
# Supported Frameworks and Tech

* Spring Framework (Experimental)
* Quarkus
* Play Framework
* Camel
* Prometheus
* JavaFX
...

---
# Disadvantages

* The main downside of this approach is the platform-depended native code. 

That means you need to compile source code for linux/windows etc.

---
<!-- 
class:
  - uncover
  - invert
 -->

# Meanwhile ??

###### ``SystemAdmin01:`` server_api.so doesn't work on my server !
###### ``Customer$$$__:`` customer_api.exe doesn't work on my pc !
###### ``DevGuy42_____:`` api.jar works on my workstation !
###### ``Fırat________:`` In some cases, problems may arise from the libraries or build scripts used. In other words, it is necessary to pay attention to  **tests**.
###### ``SystemAdmin01:`` hımm, server_api.so doest work on my server !
###### ...........................................
###### ``DevGuy42 writing ...``

---

# Sample Application

Download and install GraalVM from oracle downloads. Create an ``Example.java`` file.

```java
public class Example {

    public static void main(String[] args) {
        System.out.println("Hello GraalVM");
    }
}
```

```shell
#Run following commands :
javac Example.java
native-image Example
```

---

<!-- 
class:
  - lead
  - invert
 -->

# Tests : Sure

```java
package org.acme.quickstart;


import io.quarkus.test.junit.NativeImageTest;

@NativeImageTest 
public class NativeGreetingResourceIT extends GreetingResourceTest { 
    // Run the same tests
}
```

---
# Performance

![w:1024](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/quarkus_test.png)
Quarkus Test

---
# Features Support

GraalVM technologies are distributed as production-ready and experimental.

Experimental features are being considered for future versions of GraalVM and are not meant to be used in production. The development team welcomes feedback on experimental features, but users should be aware that experimental features might never be included in a final version, or might change significantly before being considered production-ready.

---
After that knowage i tried to make a demo application for my individual requirement. 

Firstly i have prefer a desktop application with stylish UI.
(relatively:))

That means the application sadly use a lot of memory. So i need to use ``JavaFX`` also ``Gluon``(a native JavaFX solution) for improve to performance .


---
# What I did for graalvm integration?

For that integration i have only added a plugin to my maven pom. Surprisingly that is enough for the integration.

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

The main time spending problem is dedicating build and runtime classes also classes what used by Java's reflection. Also that lists depend on what libraries you used.

After several tries, the native image prepared successfully.

```shell
#creates native image
mvn gluonfx:build
```

After that, i created a distribution folder than copied the native image and all other executables what i need to run business logic.

---

# And finally

![w:1024](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/demoapp.png)

---
# Startup time metrics from my app


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

Lightning fast jvm startup time ! 

---
# OS memory usages by the app

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/cute_memory_usage.png)

![](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/cute_memory_usage_jar.png)


We have 200MB saving from memory usage ! 

---

<!-- _footer: Fırat GÜRSOY - Senior Software Developer / May 2021--> 
# Special thanks to

* Oracle, Quarkus, JavaFX / GluonHQ, Spring
* Google and Wiki
* ![w:360](https://raw.githubusercontent.com/firatgursoy/graalvm-presentation/main/images/adesso-logo.png)

You can reach the source code and windows builds via git.

https://github.com/firatgursoy/CuteOverlay