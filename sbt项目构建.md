
## 使用sbt构建scala项目

#介绍：
    
    
    sbt是一个代码编译工具，是scala界的mvn，可以编译scala,java等。


#sbt项目环境构建：

 
    sbt编译需要固定的目录格式，并且需要联网，sbt会将依赖的jar包下载到用户home的.ivy2下面，目录结构如下：
  
```c++
|--build.sbt
    |--lib
    |--project
    |--src
    |   |--main
    |   |    |--scala
    |   |--test
    |         |--scala
    |--sbt
    |--target
```
