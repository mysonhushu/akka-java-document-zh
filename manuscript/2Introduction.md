# 2 Akka简介
## 2.1 Akka 是什么？
《弹性可伸缩的分布式实时传输处理程序》
我们认为编写正确的分布式，并发，容错和可伸缩的应用程序太难了。 大部分时间都是因为我们使用了错误的工具和错误的抽象级别。 Akka 在这里改变了这一点。 使用Actor模型，我们提高了抽象级别，并提供了一个更好的平台来构建可伸缩，有弹性和高响应的应用程序 - 请参阅 [Reactive Manifesto](http://reactivemanifesto.org/) 以获取更多详细信息。 为了容错，我们采用了 “let it crash” 的模式，电信行业已经非常成功地使用该模型来构建自我修复的应用程序和永不停止的系统。 Actor还提供透明分发的抽象，以及真正可伸缩和容错应用程序的基础。

Akka是开源的，可在Apache 2许可下使用。

从 http://akka.io/downloads 下载。

请注意，所有代码示例都是编译的，因此如果您想直接访问源代码，请查看github上的Akka Docs子项目：[Java](http://github.com/akka/akka/tree/v2.4.20/akka-docs/rst/java/code/docs) 和[Scala](http://github.com/akka/akka/tree/v2.4.20/akka-docs/rst/scala/code/docs)。

### 2.1.1 Akka实现了独特的混合动力(hybrid)

**Actors**

Actors 为你提供了：
- 用于分发(distribution)，并发(concurrency)和并行(parallelism)的简单和高级抽象。
- 异步(Asynchronous)，非阻塞(non-blocking)和高性能的(highly performant)消息驱动编程模型(message-driven programming model)。
- 非常轻量级的事件驱动进程（每GB堆内存数百万个actor）。

**容错能力**
- 具有“let-it-crash”语义的监听层次结构。
- Actor系统可以跨越多个JVM，以提供真正的容错系统。
- 非常适合编写自我修复且永不停止的高容错系统。

**位置透明**
Akka中的所有内容都设计为在分布式环境中工作：所有actor的交互都使用纯消息传递，一切都是异步的。

**持久化**
当actor被启动或重新启动时，可以选择持久化并重放actor所经历的状态变化。 即使在JVM崩溃或迁移到另一个节点之后，这也允许actor恢复其状态。

### 2.1.2 Scala 和 Java APIs
Akka既有scala-api，也有Java文档。

### 2.1.3 Akka可以以不同的方式使用
Akka是一个工具包，而不是一个框架：您可以像任何其他库一样将它集成到您的构建中，而无需遵循特定的源代码布局。 当您将系统表示为协作Actors时，您可能会觉得更倾向于正确封装内部状态，您可能会发现业务逻辑和组件间通信之间存在自然分离。

Akka应用程序通常部署如下：
- 作为库：在类路径或Web应用程序中用作常规JAR。
- 与[sbt-native-packager](https://github.com/sbt/sbt-native-packager)打包在一起。
- 使用[Lightbend ConductR](http://www.lightbend.com/products/conductr)打包和部署。

### 2.1.4 商业支持
Akka可从Lightbend Inc.获得，商业许可包括开发或生产支持，请在[此处](http://www.lightbend.com/how/subscription)阅读更多内容。

## 2.2 为什么选择Akka？
### 2.2.1 在竞争中，Akka平台可以提供哪些功能？
Akka提供可扩展的实时事务处理。

Akka是一个统一的运行时和编程模型，用于：
- 向上扩展（并发）
- 横向扩展（Remoting）
- 容错

学习和管理的一件事，具有高凝聚力和连贯的语义。

Akka是一个非常可扩展的软件，不仅在性能方面，而且在其有用的应用程序大小方面。 Akka的核心，akka-actor，非常小，当你需要异步和无锁并发时，很容易被放入现有的项目中，而不会太麻烦。

您可以选择仅在您的应用程序中包含您需要的Akka部分。 随着CPU在每个周期内越来越多的内核，即使您只在一台机器上运行它，Akka也能提供出色的性能。 Akka还提供各种并发范例，允许用户为工作选择合适的工具。

### 2.2.2  Akka 有好的应用案例吗？
我们看到Akka被许多行业的许多大型组织采用：
- 投资和商业银行
- 零售
- 社交媒体
- 模拟
- 游戏和投注
- 汽车和交通系统
- 健康呵护
- 数据分析

以及更多。 任何需要高吞吐量和低延迟的系统都是使用的良好候选者Akka。
Actors允许您管理服务故障（主管Supervisors），负载管理（退避策略，超时和处理隔离），以及水平和垂直可扩展性（添加更多内核和/或添加更多计算机）。

以下是一些Akka用户对如何使用Akka的看法：
http://stackoverflow.com/questions/4493001/good-use-case-for-akka
所有这些都在ApacheV2许可的开源项目中。

## 2.3 开始搭建环境
### 2.3.1 先决条件
Akka要求您在计算机上安装[Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)或更高版本。

[Lightbend Inc.](http://www.lightbend.com)提供商业版本的Akka和相关项目，如Scala或Play，作为[Lightbend Reactive Platform](http://www.lightbend.com/platform)的一部分，如果您的项目尚未升级到Java 8，则可用于Java 6。 它还包括其他商业功能或库。

### 2.3.2 入门指南和模板项目
开始学习Akka的最佳方式是下载 [Lightbend Activator](http://www.lightbend.com/platform/getstarted) 并试用Akka Template Projects之一。

### 2.3.3 下载
有几种方法可以下载Akka。 您可以将其作为Lightbend平台的一部分下载（如上所述）。 您可以下载完整的发行版，其中包括所有模块。 或者您可以使用Maven或SBT等构建工具从Akka Maven存储库下载依赖项。

### 2.3.4 模块
Akka非常模块化，由几个包含不同功能的JAR组成。
- akka-actor - 经典 Acptors，类型 Acptors，IO Acptors等
- akka-agent - 代理(Agents)，与Scala STM集成
- akka-camel - Apache Camel 集成
- akka-cluster - 集群成员管理，弹性路由器。
- akka-osgi - 在OSGi容器中使用Akka的实用程序
- akka-remote - 远端 Actors
- akka-slf4j - SLF4J Logger(event bus listener 事件总线侦听)
- akka-stream - 反应流处理
- akka-testkit - 用于测试Actor系统的工具包

除了这些稳定的模块之外，还有几个正在进入稳定核心的路上，但此时仍然标记为“实验性”。 这并不意味着它们不能按预期运行，它主要意味着它们的API还没有足够的固化才能被视为冻结。 您可以通过在我们的邮件列表上提供有关这些模块的反馈来帮助加快此过程。
- akka-contrlib - 可能会或可能不会转移到核心模块的各种贡献，有关详细信息，请参阅外部贡献(External Contributions)。

### 2.3.5 使用已经发布的分发包
从 http://akka.io/downloads 下载所需的版本并解压缩。

### 2.3.6 使用 snapshot 版本
Akka每夜快照发布到　http://repo.akka.io/snapshots/　，并且版本都带有SNAPSHOT和时间戳。 您可以选择要使用的带时间戳的版本，并可以决定何时更新到更新的版本。
> 注意: 除非你知道你在做什么，否则不鼓励使用Akka SNAPSHOT，nightlies和里程碑版本。

### 2.3.7 使用一个构建工具
Akka可以与支持Maven存储库的构建工具一起使用。

### 2.3.8 Maven 仓库
对于Akka 2.1-M2版及以后版本：
[Maven Central](https://repo1.maven.org/maven2/)
对于之前的Akka版本:
[Akka Repo](http://repo.akka.io/releases/)

### 2.3.9 使用 Maven 构建 Akka
开始使用Akka和Maven的最简单方法是查看名为Akka的[Lightbend Activator](http://www.lightbend.com/platform/getstarted)教程
[Akka Main in Java](http://www.lightbend.com/activator/template/akka-sample-main-java)。

由于Akka发布到Maven Central（对于自2.1-M2以来的版本），因此将Akka依赖项添加到POM就足够了。 例如，这是akka-actor的依赖项：

```xml
<dependency>
    <groupId>com.typesafe.akka</groupId>
    <artifactId>akka-actor_2.11</artifactId>
    <version>2.4.20</version>
</dependency>
```
 对于快照版本，还需要添加快照存储库：

```xml
<repositories>
    <repository>
        <id>akka-snapshots</id>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        <url>http://repo.akka.io/snapshots/</url>
    </repository>
</repositories>
```
**备注**: 对于快照版本，将发布SNAPSHOT和带时间戳的版本。

### 2.3.10 使用SBT构建Akka
开始使用Akka和SBT的最简单方法是将Lightbend Activator与其中一个SBT模板一起使用。使用Akka和SBT的基本部分概述：

SBT安装说明: http://www.scala-sbt.org/release/tutorial/Setup.html

build.sbt 文件:
```
name := "My Project"
version := "1.0"
scalaVersion := "2.11.11"
libraryDependencies +=
"com.typesafe.akka" %% "akka-actor" % "2.4.20"
```
**注意**： 上面的libraryDependencies设置特定于SBT v0.12.x及更高版本。 如果您使用的是较旧版本的SBT，则libraryDependencies应如下所示：
```
libraryDependencies +=
"com.typesafe.akka" % "akka-actor_2.11" % "2.4.20"
```

对于快照版本，还需要添加快照存储库：
```
resolvers += "Akka Snapshot Repository" at "http://repo.akka.io/snapshots/"
```

### 2.3.11 使用Gradle构建Akka
至少需要 [Gradle](https://gradle.org) 1.4 以上的版本，还要使用 [Scala 插件](http://www.gradle.org/docs/current/userguide/scala_plugin.html)

```gradle
apply plugin: ’scala’
repositories {
    mavenCentral()
}
dependencies {
    compile ’org.scala-lang:scala-library:2.11.11’
}
tasks.withType(ScalaCompile) {
    scalaCompileOptions.useAnt = false
}
dependencies {
    compile group: ’com.typesafe.akka’, name: ’akka-actor_2.11’, version: ’2.4.20’
    compile group: ’org.scala-lang’, name: ’scala-library’, version: ’2.11.11’
}
```

对于快照版本，还需要添加快照存储库：
```gradle
repositories {
    mavenCentral()
    maven {
        url "http://repo.akka.io/snapshots/"
    }
}
```

### 2.3.12 用Eclipse开发工具搭建Akka项目
设置SBT项目，然后使用[sbteclipse](https://github.com/typesafehub/sbteclipse)生成Eclipse项目。

### 2.3.13 使用IntelliJ IDEA 开发工具搭建Akka项目
设置SBT项目，然后使用[sbt-idea](https://github.com/mpeltonen/sbt-idea)生成IntelliJ IDEA项目。

### 2.3.14 使用NetBeans 开发工具搭建Akka项目
设置SBT项目，然后使用 [nbsbt](https://github.com/dcaoyuan/nbsbt) 生成NetBeans项目。
您还应该在IDE中使用 [nbscala](https://github.com/dcaoyuan/nbscala) 进行常规scala支持。

### 2.3.15  不要使用 -optimize Scala编译器标志
>警告： Akka尚未使用-optimize Scala编译器标志进行编译或测试。 已经尝试过的用户已经报告了奇怪的行为。

### 2.3.16 基于源码构建
Akka使用Git并在[Github](https://github.com)上托管。
- Akka: 从 https://github.com/akka/akka 克隆 Akka仓库代码
详细的步骤请参考后面的构建Akka章节。

### 2.3.17 需要帮助？
如果你遇到问题，可以从[Akka邮件列表](https://groups.google.com/group/akka-user)中得到帮助。
你还可以寻求[商业支持](https://www.lightbend.com)。
感谢您成为Akka社区的一员。

## 2.4 Hello World 入门
基于 actor 的版本的一个问题是向控制台打印一个众所周知的问候语. [Lightbend Activator](http://www.lightbend.com/platform/getstarted)教程中命名为[ Akka Main in Java](http://www.lightbend.com/activator/template/akka-sample-main-java)。

本教程说明了通用启动程序类 akka.Main，它只需要一个命令行参数：应用程序 main actor的类名。 然后，这个主要方法将创建运行actors 所需的基础结构，启动给定的 main actor，并在 main actor 终止后安排整个应用程序关闭。

在同一问题域中还有另一个名为[Hello Akka！](http://www.lightbend.com/activator/template/hello-akka)的[Lightbend Activator](http://www.lightbend.com/platform/getstarted)教程。 它更深入地描述了Akka的基础知识。

