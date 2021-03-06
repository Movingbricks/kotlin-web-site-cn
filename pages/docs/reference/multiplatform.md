---
type: doc
layout: reference
category: "Other"
title: "多平台程序设计"
---

# 多平台程序设计

> 多平台项目处于 [Alpha](evolution/components-stability.html) 版。语言特性与工具都可能在未来的 Kotlin 版本中发生变化。
{:.note}

Support for multiplatform programming is one of Kotlin’s key benefits. It reduces time spent writing and maintaining the
 same code for [different platforms](mpp-supported-platforms.html) while retaining the flexibility and benefits of native programming. 

This is how Kotlin Multiplatform works.

<img class="img-responsive" src="{{ url_for('asset', path='images/reference/mpp/kotlin-multiplatform.png' )}}" alt
="Kotlin Multiplatform" width="500" />

*   **Common Kotlin** includes the language, core libraries, and basic tools. Code written in common Kotlin works 
everywhere on all platforms.
*   With Kotlin Multiplatform libraries, you can reuse the multiplatform logic in common and platform-specific code. 
Common code can rely on a set of libraries that cover everyday tasks such as [HTTP](http://ktor.io/clients/http-client/multiplatform.html), [serialization](https://github.com/Kotlin/kotlinx.serialization), and [managing 
coroutines](https://github.com/Kotlin/kotlinx.coroutines).
*   To interop with platforms, use platform-specific versions of Kotlin. **Platform-specific versions of Kotlin** 
(Kotlin/JVM, Kotlin/JS, Kotlin/Native) include extensions to the Kotlin language, and platform-specific libraries and tools. 
*   Through these platforms you can access the **platform native code** (JVM, JS, and Native) and leverage all native
 capabilities.

With Kotlin Multiplatform, spend less time on writing and maintaining the same code for [different platforms](mpp-supported-platforms.html)
 – just share it using the mechanisms Kotlin provides:

*   [Share code among all platforms used in your project](mpp-share-on-platforms.html#share-code-on-all-platforms). Use it for sharing the common 
business logic that applies to all platforms. 
     
    ![Code shared for all platforms]({{ url_for('asset', path='images/reference/mpp/flat-structure.png') }})
    
*   [Share code among some platforms](mpp-share-on-platforms.html#share-code-on-similar-platforms) included in your project but not all. Do this 
when you can reuse much of the code in similar platforms.  
    
    ![Hierarchical structure]({{ url_for('asset', path='images/reference/mpp/hierarchical-structure.png') }})

If you need to access platform-specific APIs from the shared code, use the Kotlin mechanism of [expected and actual 
declarations](mpp-connect-to-apis.html).

With this mechanism, a common source set defines an *expected declaration*, and platform source sets must provide the 
*actual declaration* that corresponds to the expected declaration. This works for most Kotlin declarations, such as 
functions, classes, interfaces, enumerations, properties, and annotations.

![Expect and actual declarations]({{ url_for('asset', path='images/reference/mpp/expect-actual.png') }})

<div class="sample" markdown="1" theme="idea" data-highlight-only>

```kotlin
//Common
expect fun randomUUID(): String
```

</div>

<div class="sample" markdown="1" theme="idea" data-highlight-only>

```kotlin
//Android
import java.util.*
actual fun randomUUID() = UUID.randomUUID().toString()
```

</div>

<div class="sample" markdown="1" theme="idea" data-highlight-only>

```kotlin
//iOS
import platform.Foundation.NSUUID
actual fun randomUUID(): String = NSUUID().UUIDString()
```

</div>

## 使用场景

### Android——iOS

移动平台之间共享代码是 Kotlin 多平台的主要使用场景之一，现在<!--
-->可以通过在 Android 与 iOS 之间共享部分代码（如业务逻辑、连接等）
来构建移动应用。

See [Mobile Multiplatform features, case studies and examples](https://www.jetbrains.com/lp/mobilecrossplatform/)

### 客户端——服务端

代码共享可以带来收益的另一个场景是互联应用，其中的逻辑可以<!--
-->在服务器与运行在浏览器中的客户端中复用。Kotlin 多平台也覆盖了<!--
-->这个场景。

[Ktor 框架](https://ktor.kotlincn.net/)适用于在互联系统中构建异步的服务器与客户端。

## 接下来做什么？

New to Kotlin? Visit [Getting Started](/docs/reference/basic-syntax.html).

### 文档

* [Create a multiplatform project](mpp-create-lib.html)
* [Share code on multiple platforms](mpp-share-on-platforms.html)
* [Connect to platform-specific APIs](mpp-connect-to-apis.html)

### 教程

* [Creating a multiplatform Kotlin library](/docs/tutorials/mpp/multiplatform-library.html) teaches how to create a multiplatform 
library available for JVM, JS, and Native and which can be used from any other common code (for example, shared with 
Android and iOS). It also shows how to write tests which will be executed on all platforms and use an efficient implementation
 provided by a specific platform.
 
* [Building a Full Stack Web App with Kotlin Multiplatform](https://play.kotlinlang.org/hands-on/Full%20Stack%20Web%20App%20with%20Kotlin%20Multiplatform/01_Introduction) 
  teaches the concepts behind building an application that targets Kotlin/JVM and Kotlin/JS by building a client-server 
  application that makes use of shared code, serialization, and other multiplatform paradigms. It also provides a brief
  introduction to working with Ktor both as a server- and client-side framework.
  
## 样例项目

- [KotlinConf app](https://github.com/JetBrains/kotlinconf-app)
- [KotlinConf Spinner app](https://github.com/jetbrains/kotlinconf-spinner)

