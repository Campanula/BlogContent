---
date: 2017-03-11T17:34:39+08:00
series: ["Java SE Tools Reference"]
tags: ["java"]
title: "Java SE 命令清单"
---

Java SE 命令工具可以用于处理一些开发任务，比如编译和运行程序；将源代码文件打包到 jar 文件中；给 jar 文件使用安全策略等。下面是 JDK 的全套命令，根据相关功能划分为一下几部分：

# 创建应用程序

`appletviewer` 在浏览器外运行 Applets
`extcheck` 检测目标 Java 归档（JAR）文件和当前安装的扩展 JAR 文件之间的版本冲突
`jar` 将多个文件合并为单个JAR文件
`java` 启动一个 Java 程序
`javac` 读取 Java 类和接口定义，并将它们编译成字节码和类文件
`javadoc` 从 Java 源文件中生成 API 文档的 HTML 页面
`javah` 从Java类生成C头文件和源文件
`javap` 分解（Disassembles）一个或多个 class 文件
`jdb` 查找并修复 java 程序中的 bug
`jdeps` Java 类依赖关系分析器

# 安全

`keytool` 管理一个存储密钥、X.509证书链和受信任证书的 keystore 数据库
`jarsigner` 签名或者验证 JAR 文件
`policytool` 根据用户在图形工具上的输入，读写一个纯文本的策略文件

# 国际化

`native2ascii` 将任何非 ASCII 字符集的字符转换为 ASCII 或者 Unicode 转义(\uxxxx)字符，反之亦然。

# 远程方法调用（RMI）

`rmic` 为使用Java远程方法协议（JRMP）或Internet Inter-Orb协议（IIOP）的远程对象生成存根，框架和绑定类。还生成对象管理组（OMG）接口定义语言（IDL）。
`rmiregistry` 在当前主机上的指定端口上启动远程对象注册表。
`rmid` 启动激活系统守护程序，该守护程序使对象能够在Java虚拟机（JVM）中注册和激活。
`serialver` 返回指定类的串行版本UID。

# Java IDL 和 RMI­IIOP

`tnameserv` 启动Java接口定义语言（IDL）名称服务器。
`idlj` 为给定的接口定义语言（IDL）文件生成Java绑定。
`orbd` 使客户端能够在CORBA环境中定位和调用服务器上的持久对象。
`servertool` 为应用程序员注册，注销，启动和关闭服务器提供一个易于使用的界面。

# 部署应用程序和 Applets

`pack200` 将JAR文件打包到用于Web部署的压缩pack200文件中。
`unpack200` 将由pack200（1）生成的打包文件转换为用于Web部署的JAR文件。

# Java Web Start

`javaws` 启动Java Web Start。

# 监控 Java 应用程序

`jconsole` 启动图形控制台，允许您监视和管理Java应用程序。
`jvisualvm` 对Java应用程序进行可视监视，故障排除和配置文件。

# 监控 JVM

`jps` 实验。列出目标系统上已检测的Java虚拟机（JVM）。
`jstat` 实验。监视JVM统计信息
`jstatd` 实验。监视JVM并启用远程监视工具以附加到JVM。
`jmc` 启动Java Mission Controla工具，用于监视和管理正在运行的Java应用程序和JVM。

# Web 服务

`schemagen` 为在Java类中引用的每个名称空间生成一个图式。
`wsgen` 读取Web服务端点实施（SEI）类，并生成Web服务部署和调用所需的所有工件。
`wsimport` 生成可以打包在Web应用程序归档（WAR）文件中的JAX-WS可移植工件，并提供Ant任务。
`xjc` 将一个 XML schema 文件编译到一个全注解的 Java classes 中

# 排查故障

`jcmd` 将诊断命令请求发送给运行中的 JVM
`jinfo` 实验性的，生成配置信息
`jhat` 实验性的，分析 java 堆
`jhat` 实验性的，打印一个进程、核心文件或者远程调试服务器的共享对象的内存映射或者堆内存细节
`jsadebugd` 实验性的，作为调试服务器绑定到一个 java 进程或者核心文件上
`jstack` 实验性的，打印一个进程、核心文件或者远程调试服务器的 Java 线程的堆栈跟踪

# 脚本

`jrunscript` 实验性的，运行一个支持交互式或者批量式的命令行脚本shell
`jss` 调用 Nashorn 引擎。您可以使用它来解释一个或多个脚本文件，或运行交互式shell