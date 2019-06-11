# 1 安全公告

## 1.1 接收安全建议
接收任何和所有安全公告的最佳方式是订阅Akka安全列表。[邮件列表](https://groups.google.com/forum/#!forum/akka-security) (https://groups.google.com/forum/#!forum/akka-security)的流量非常低，只有在核心团队管理安全报告并且修复程序公开可用后才会收到通知。

## 1.2 报告漏洞
我们强烈建议人们首先将这些问题反馈给我们的私人安全邮件列表，然后再在公共论坛中披露。按照最佳做法，我们强烈建议任何人在发送邮件列表或Github问题等公共论坛之前向security@akka.io报告潜在的安全漏洞。此电子邮件地址的报告将由我们的安全团队处理，他们将与您一起确保可以立即提供修复。

## 1.3 安全相关的文档
* disable-java-serializer-scala
* remote-deployment-whitelist-scala
* remote-security-scala

## 1.4 已修复了的安全漏洞

### 1.4.1 Java序列化，已在 Akka 2.4.17 中修复

**日期**
2017 年 10 月

**漏洞描述**
攻击者可以通过TCP经由公开的ActorSystem连接到Akka远端。在运行ActorSystem的JVM进程的上下文中获得远程代码执行功能，如果：
- JavaSerializer 是启用的(这是　Akka　２.4.x 的默认配置)
- TLS 是禁用的，或者 TLS 是通过配置 akka.remote.netty.ssl.security.require-mutual-authenticatic = false　启用的(这是　Akka　２.4.x 的默认配置)
- 或者如果通过相互身份验证启用了TLS并且允许连接的主机的身份验证密钥已被泄露，则攻击者可以访问有效证书（例如，通过破坏
具有由相同内部PKI树颁发的证书的节点，以获取证书的访问权限）
- 无论是否启用不受信任模式

[众所周知](https://community.hpe.com/t5/Security-Research/The-perils-of-Java-deserialization/ba-p/6838995)，Java反序列化在攻击者可以提供任意类型时容易受到攻击。

Akka Remoting使用Java serialiser作为默认配置，使其以默认形式容易受到攻击。 有关如何禁用Java序列化程序的文档未完成。 缺少如何启用相互身份验证的文档（仅在reference.conf中描述）。

为防止此类攻击，系统应更新为Akka 2.4.17或更高版本，并配置为禁用的Java序列化程序。 通过启用相互身份验证的TLS，可以在不受信任的网络中运行时实现额外的保护。

请订阅[akka-security邮件列表](https://groups.google.com/forum/#!forum/akka-security)，以便及时通知未来的安全问题。

**严重性**
该漏洞的 [CVSS](https://en.wikipedia.org/wiki/CVSS) 评分为6.8（中等），基于矢量[AV:A/AC:M/Au:N/C:C/I:C/A:C/E:F/RL:TF/RC:C](https://nvd.nist.gov/cvss.cfm?calculator&version=2&vector=(AV:A/AC:M/Au:N/C:C/I:C/A:C/E:F/RL:TF/RC:C))。

得分的基本原理：
- AV:A - 最佳做法是只能从相邻网络访问Akka远程节点，因此在良好的设置中，这将是相邻的。
- AC:M - 相邻网络中的任何一个都可以使用非特殊访问权限启动攻击。
- C:C,I:C,A:C - 远程代码执行漏洞根据定义 CIA:C。

**影响的版本**
- Akka 2.4.16 和更早的版本
- Akka 2.5-M1(一个分支版本，并没有纳入主分支产品版本)

**修复后的版本**
我们已为受影响的版本准备了补丁，并已发布以下版本来解决问题
问题：
- Akka 2.4.17(Scala 2.11, 2.12)

已修补版本已维护二进制和源兼容性，因此升级过程与更改库依赖关系一样简单。 它也将固定在2.5-M2或2.5.0-RC1中。

**致谢**
我们要感谢Hewlett Packard Enterprise Security的Alvaro Munoz和Workday的Adrian Bravo进行彻底的调查并将此问题提请我们注意。

### 1.4.2 Camel依赖，在Akka 2.4.20中修复

**日期**
2017年9月

**漏洞描述**
Apache Camel的验证组件通过远程DTD和XXE容易受到SSRF攻击，如[CVE-2017-5643](https://nvd.nist.gov/vuln/detail/CVE-2017-5643)中所述

为防止此类攻击，系统应更新为Akka 2.4.20,2.5.4或更高版本。 Camel库的依赖关系应更新到2.7.17版。

**严重性**
根据[CVE-2017-5643](https://nvd.nist.gov/vuln/detail/CVE-2017-5643)，此漏洞的[CVSS](https://en.wikipedia.org/wiki/CVSS)评分为7.4（高）。

**受影响的版本**
- Akka 2.4.19 和之前的版本
- Akka 2.5.3 和之前的版本

**修复后的版本**
我们已为受影响的版本准备了补丁程序，并已发布以下版本以解决此问题：
- Akka 2.4.20(Scale 2.11,2.12)
- Akka 2.5.4 (Scale 2.11, 2.12)

**致谢**
我们要感谢Thomas Szymanski将此问题提给我们，才引起我们的注意。
