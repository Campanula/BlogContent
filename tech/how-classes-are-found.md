---
date: 2017-03-06T00:19:52+08:00
tags: ["java","JVM"]
series: ["Java SE Tools Reference"]
title: "Java 如何查找 Classes"
---

JDK 提供了很多构建 java 程序的工具，比如 java、javac、javadoc、jdb 等。因为 eclipse 、IntelliJ IDEA 等 IDE 给我们提供了极大的便利，我们很少直接接触到这些基本的工具，但在实际的工作中，我们总会碰到与之相关的东西，比如 java 程序的部署和运行。了解这些知识可以让我们更加从容面对复杂的实际情形，Oracle 官方文档对这些话题提供了不错的参考，本系列文章是对[此处文档](http://docs.oracle.com/javase/8/docs/technotes/tools/windows/toc.html)的梳理和总结，后续若有机会的话，会对其中涉及的话题进一步的深入完善。

<!--more-->

`java` 命令被用于启动 java 程序，当被调用时，它会从用户的输入和环境中收集信息并引导 java 虚拟机（JVM），由 JVM 处理接下来的工作。

# Java 运行时如何查找 Class

JVM 会按照顺序依次查找并加载以下三种类：

**Bootstrap classes** 它们是构成 java 平台的类，比如位于`JDK/jre/lib/`中的 rt.jar 和 其他一些重要的 jar 文件。oracle 官网 tutorial 文档中[一处](http://docs.oracle.com/javase/tutorial/ext/basics/load.html)提到的 i18n.jar，[据了解](https://bugs.openjdk.java.net/browse/JDK-4412570)，已经被 charset.jar 取代，请各位了解准确信息的朋友斧正。

**Extension classes** 位于 `JDK/jre/lib/ext` 目录下的 jar 文件。

**User classes** 由开发者和第三方定义的 class 文件。通过 `-classpath` 命令行选项或者 `CLASSPATH` 环境变量指定位置。

用户一般只需指定 user classes 的位置，Bootstrap classes 和 Extension classes 会被自动处理。

# Java 运行时如何查找 Bootstrap classes

指明 Bootstrap classes 位置的信息存储在 `sun.boot.class.path` 系统属性中，它在方法 java.lang.System.initProperties 中被初始化，此方法是由 C++ 实现的 Native Method。Bootstrap classes 位置可以使用非标准选项 `-Xbootclasspath` 重新指定。

`JDK/lib/tools.jar` 并不属于 Bootstrap classes，但在调起 `java` 命令时，它会被自动拓展到 user class path 中，而 `javac` 和 `javadoc` 命令在处理源代码时，并不会这样。

# Java 运行时如何查找 Extension classes

位于 `JDK/jre/lib/ext` 的 class 文件必须包含在 jar 或者 zip 文件中，裸 class 文件不会被查找。如果存在多个 jar 文件，而且这些 jar 文件中包含有相同 class，则这种情况下这些 Class 的加载是未定义的行为。

```
smart­extension1_0.jar contains class smart.extension.Smart
smart­extension1_1.jar contains class smart.extension.Smart
```

# Java 运行时如何查找 User classes

user class path 是一系列包含有 Class 文件的目录、jar文件、zip文件。

如果 `com.mypackage.MyClass` 位于 `myclasses` 目录下，则这个目录必须被包含在 user class path 中，class 文件的全路径为 `/myclasses/com/mypackage/MyClass.class`。

如果 `com.mypackage.MyClass` 位于一个名为 `myclasses.jar` 的归档文件中，则这个归档文件必须被包含在 user class path 中，并且 class 文件在归档文件中必须存储为 `com/mypackage/MyClass.class`。

user class path 可以包含多个路径，在 windows 上，多个路径由分号（;）分割，在 linux 上则是冒号（：）。java 启动器将 user class path 中的字符串存储在 `java.class.path` 系统属性中，它的值按一下顺序决定：

1. 默认值，当前文件夹下的所有 class 文件。
2. CLASSPATH 环境变量中指定的值，覆盖上一设置。
3. 命令行选项 `-classpath`，`-cp` 指定的值，覆盖上一设置。
4. 如果通过 `-jar` 指定的 jar 文件中包含有指定了 `Class­-Path` 的 manifest 文件，所有 user class 文件都必须来自于指定的归档文件中。

# Java 运行时如何查找 JAR­-class-­path Classes

当 class 文件只来源于归档文件时，manifest 中可以定义一个 JAR class path, class 文件按一下顺序被访问：

1. class 文件被视为它所属的 jar 文件的一部分，jar 文件一般按 manifest 中的条目先后顺序搜索。
2. 已经被搜索过的 jar 不会被再次搜索，这样可以提升性能并且避免循环搜索。
3. 如果一个 jar 文件属于 extension，则其中定义的 JAR class path 会被忽略。所有被 extension 依赖的 class 都会被视为是 JDK 的一部分或者是已经被安装的 extension。

# javac 和 javadoc 命令如何查找 Classes

`javac` 和 `javadoc` 会在一下两方面使用到 class 文件：

1. 用于支持自身的运行。
2. 用于解析源代码中的引用。（被引用的类可以是 class 文件的形式或者源代码文件的形式）

`tools.jar` 仅被用于 `javac` 和 `javadoc` 的运行，若要用于源代码的解析，需要将其明确的包含在 user class path 中。

一个程序可以选择引用不同的 `java` 平台实现，`javac` 和 `javadoc` 通过 `-­bootclasspath` 和 `-­extdirs` 选项提供支持，但这些选项并不会改变这两个工具自身运行时所需要的一系列 class 文件。

对于 class 文件和源代码文件中的同一个类， `javadoc` 优先选择源代码文件。而 `javac` 优先选择 class 文件，但会自动从源代码文件重新编译那些已经过期的 class。

如果指定了 `­-sourcepath` 选项，则 `javac` 和 `javadoc` 会仅仅从指定的源代码路径搜索源代码文件，但依然会从 user class path 中搜索 class 文件。
