
 使用sbt构建scala项目
######


# 介绍：

sbt是一个代码编译工具，是scala界的mvn，可以编译scala,java等。

# sbt下载

地址：http://www.scala-sbt.org/download.html

# sbt安装

```C++
 1 ： tar zxvf sbt-0.13.9.tgz
```

```C++
 2 ：在./sbt目录下面新建文件名为sbt的文本文件 
 $ cd ./sbt
 $ vim sbt
 # 在sbt文本文件中添加如下信息：
   BT_OPTS="-Xms512M -Xmx1536M -Xss1M -XX:+CMSClassUnloadingEnabled -XX:MaxPermSize=256M"
   java $SBT_OPTS -jar /search/odin/ONLINE/Spark/sbt/bin/sbt-launch.jar "$@" 
   这里路径需要需改为你自己对应的文件路径，只要能够正确的定位到解压的sbt文件包中的sbt-launch.jar文件即可
 $ chmod u+x sbt 
 # 修改sbt文件权限
```
```C++
 3 ：配置PATH执行环境
 $ vim ~/.bashrc
 # 在文件尾部添加如下代码后，保存退出
 
 export PATH=/home/zhangchengfei/Tools/sbt/:$PATH
 $ source ~/.bashrc # 生效
```

```C++
 4 ：配置文件的目录在./sbt/conf/sbtconfig.txt
 # 设置网络代理，在配置中添加：
 
 -Dhttp.proxyHost=proxy.zte.com.cn
 -Dhttp.proxyPort=80
 
 # 安装完成后会在用户的根目录生成两个文件夹，sbt工作文件夹.sbt和lvy缓存目录.ivy2，修改默认路径，在配置中添加：
 -Dsbt.global.base=/search/odin/ONLINE/Spark/sbt/.sbt
 -Dsbt.ivy.home=/search/odin/ONLINE/Spark/sbt/.ivy2
 
 # 注意：上面这种方式修改路径我尝试过并没有成功，网上说需要重启系统才能生效。由于电脑当前状态信息太多（开的应用太多）
   重启后很难恢复，并且这并不影响实验结果，所以没有进一步测试验证。
```

```C++
  5 : 第一次执行时，会下载一些文件包，然后才能正常使用，要确保联网了，安装成功后显示如下
  $ sbt sbt-version
    [info] Set current project to sbt (in build file:/opt/scala/sbt/)
    [info] 0.13.9
```

 
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

libraryDependencies格式：

libraryDependencies += groupID % artifactID % revision

或用如下申明，其中configuration是一个字符串或者一个配置维度实例

libraryDependencies += groupID % artifactID % revision % configuration

例如：libraryDependencies += "org.apache.spark" %% "spark-core" % "1.6.2" % "provided"

libraryDependencies是指程序的库依赖，最后的provided的意思，spark内已经提供了这几个库，打包时，无需要考虑这几个。


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


# 参考：

    1：http://blog.csdn.net/zcf1002797280/article/details/49677881

    2：http://www.cnblogs.com/gaopeng527/p/4398225.html
     
    3: http://www.cnblogs.com/wrencai/p/3867460.html
