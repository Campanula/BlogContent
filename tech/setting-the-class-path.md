---
date: 2017-03-10T22:15:38+08:00
tags: ["java","class","jre","jar"]
title: "设置 Class Path"
---

`Class Path` 是 java 运行时环境（JRE）搜索 classes 文件和其他资源文件的路径。

# 概要

class path 可以通过 `-classpath` 选项或者 `CLASSPATH` 环境变量来设定。前者是更好的方式，每一个程序都可以单独设置而避免对其他程序产生影响。对于新版的 JDK，`CLASSPATH` 环境变量不是必须配置的。

下面等号两边没有空格，等号后可以没有内容，多个路径需使用分隔符，在 windows 系统中使用分号(;) linux 系统中使用冒号(:)分割。路径按指定的顺序优先搜索。
```
sdkTool -­classpath classpath1:classpath2...
set CLASSPATH=classpath1;classpath2...
```

`sdkTool` 一个命令行工具，比如 `java`,`javac`,`javadoc` 或者 `apt` 等，请参见此处的[列表](http://docs.oracle.com/javase/8/docs/technotes/tools/index.html)

`classpath1:classpath2` 指向 `JAR`、`zip`、`class` 文件的路径。路径需要以文件名或者文件夹结尾：

1. `JAR/zip 文件` 路径以 JAR 或者 zip 文件名结尾（包括后缀名）
2. `没有被命名包名的 class 文件` 路径以包含这些 class 文件的目录结尾
3. `包下的 class 文件` 路径结尾为包含根包的文件夹。

默认路径为当前文件夹，指定 class path 后会覆盖默认值，如果要包含当前路径，需要将一个点(.)包含在 class path 中。不以`目录`、`JAR/zip文件`、和星号(*)通配符结尾的路径会被忽略。

注意：一些早期的JDK版本中，默认的 class path 包含了 `<jdk­dir>/classes` ，这个目录仅仅被 JDK 工具使用，用户应用程序需要的 classes 应该单独放到 JDK 目录层次外，这样当需要重新安装 JDK 时不需要重新布置应用程序。

# Class Path 通配符

Class Path 中可以包含通配符(*)以匹配一系列的`jar`文件，比如 `mydir/*` 会匹配 mydir 目录下的所有 jar 文件。这样并不能匹配 class 文件，如果需要同时匹配 jar 和 class 文件，可以使用`mydir:mydir/*` 或者 `mydir/*:mydir`，书写的先后顺序决定载入的顺序。

子文件夹不会被递归搜索，比如 `mydir/*` 不会搜索 `mydir/subdir1` 下的 jar 文件。如果一个文件夹下有多个 jar 文件，这些 jar 文件的载入顺序是不明确的，可能会跟随系统平台而变，结构良好的程序不应该依赖于确定的载入顺序。如果需要明确载入顺序，可以将 jar 文件在 class path 中逐一明确列出。

通配符会在调用程序主方法前被展开，并被设置为系统属性`java.class.path`的值。通配符对`CLASSPATH`环境变量和`-classpath`选项都有效，但在 jar-manifest 文件的 Class-Path 条目中无效。

# Class Path 和包名

Java 类的包路径与文件系统的目录层次相对应，但是在指定包名时，需要完整的包路径而不是路径的一部分。`java.awt.Button` 的包名需要明确指定为 `java.awt`。比如一个名为 `Cool.class` 的 class 文件，位于 `utility.myapp` 包下，位于 `C:\java\MyClasses\utility\myapp` 路径之下，你可以使用以下命令运行这个类：

```
java ­-classpath C:\java\MyClasses utility.myapp.Cool
```

而以下命令无效：

```
java ­-classpath C:\java\MyClasses\utility myapp.Cool
```

包名是 class 的一部分，除非重新编译，否则不能被修改。一个包下的多个 class 可以分布在不同文件夹下。

对于归档文件中的 class 可以使用以下命令运行：

```
java -­classpath C:\java\MyClasses\myclasses.jar utility.myapp.Cool
```