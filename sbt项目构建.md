
## 使用sbt构建scala项目

# 介绍：

sbt是一个代码编译工具，是scala界的mvn，可以编译scala,java等。

# sbt项目环境构建：
 
sbt编译需要固定的目录格式，并且需要联网，sbt会将依赖的jar包下载到用户home的.ivy2下面，目录结构如下：
  
```c++
|--build.sbt
    |--lib
    |--project
    |--src
    |   |--main
    |   |    |--scala
    |   |    |--java
    |   |    |--resources
    |   |--test
    |         |--scala
    |         |--java
    |         |--resources
    |--sbt
    |--target
```
* src/main/java目录存放Java源代码文件
* src/main/resources目录存放相应的资源文件
* src/main/scala目录存放Scala源代码文件
* src/test/java目录存放Java语言书写的测试代码文件
* src/test/resources目录存放测试起见使用到的资源文件
* src/test/scala目录存放scala语言书写的测试代码文件

# build.sbt详解

```C++

name := "SimpleProject"    // 项目名称

version := "1.0.0"         // 版本号

scalaVersion := "2.9.3"    // 使用的Scala版本号

libraryDependencies += "ch.qos.logback" % "logback-core" % "1.0.0"  
或
libraryDependencies += "ch.qos.logback" % "logback-classic" % "1.0.0"  // 添加源代码编译或者运行期间使用的依赖 
或
libraryDependencies ++= Seq(     "ch.qos.logback" % "logback-core" % "1.0.0",             
                                 "ch.qos.logback" % "logback-classic" % "1.0.0",                      
                                 ... )
```

# 编译&打包&运行

进入当前目录

```C++
   1:sbt compile
   2:sbt package
   3:sbt run
```

```C++
   先输入sbt命令，在输入run，就会运行scala项目，如果scala项目中有多个main方法，会询问执行那个
```
编译过程，sbt需要上网下载依赖工具包，jna,scala等。编译完成后可以在target/scala-2.9.3/目录下找到打好的jar包。
