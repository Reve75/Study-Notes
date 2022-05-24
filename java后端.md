
## IDEA插件

https://zhuanlan.zhihu.com/p/439934300

https://www.cnblogs.com/luzhanshi/p/10592829.html

Springboot是一个idea插件，可以不用安装直接使用。

https://cloud.tencent.com/developer/article/1810741

https://www.jianshu.com/p/28e1aedb4819

https://blog.csdn.net/weixin_45897761/article/details/107893291

使用idea安装springboot框架
---

## 关于maven

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.


https://cloud.tencent.com/developer/article/1705945

Maven能够解决什么问题

在想Maven可以解决什么问题之前我们先来想想我们开发过程中经常遇到什么问题

 1、我们需要引用各种 jar 包，尤其是比较大的工程，引用的 jar 包往往有几十个乃至上百个， 每用到一种 jar 包，都需要手动引入工程目录，而且经常遇到各种让人抓狂的 jar 包冲突，版本冲突。

 2、我们辛辛苦苦写好了 Java 文件，可是只懂 0 和 1 的白痴电脑却完全读不懂，需要将它编译成二进制字节码。好歹现在这项工作可以由各种集成开发工具帮我们完成，Eclipse、IDEA 等都可以将代码即时编译。当然，如果你嫌生命漫长，何不铺张，也可以用记事本来敲代码，然后用 javac 命令一个个地去编译，逗电脑玩。

 3、世界上没有不存在 bug 的代码，计算机喜欢 bug 就和人们总是喜欢美女帅哥一样。为了追求美为了减少 bug，因此写完了代码，我们还要写一些单元测试，然后一个个的运行来检验代码质量。

 4、再优雅的代码也是要出来卖的。我们后面还需要把代码与各种配置文件、资源整合到一起，定型打包，如果是 web 项目，还需要将之发布到服务器，供人蹂躏。

 maven所帮助我们解决的问题

 以上的这些问题maven都把我们解决了，没错maven可以帮我们

 1构建工程，

 2管理jar，

 3.编译代码，

 4.自动运行单元测试，

 5.打包

 6.生成报表，

 7.部署项目，生成web站点。

 有没有孙悟空得到金箍棒的感觉

### maven 安装

https://developer.aliyun.com/article/706383

https://zhuanlan.zhihu.com/p/439934300

进入/usr/local:

https://discussions.apple.com/thread/1509209

### intellij maven 设置

https://www.jetbrains.com/help/idea/maven-support.html#maven_add_module

在idea里配置maven的入口。新版本要看这个，有改动。

https://zhuanlan.zhihu.com/p/122429605

更详细的配置

https://cloud.tencent.com/developer/article/1834702

有更多的设置，关于：

VM Options : -DarchetypeCatalog=internal： maven项目创建时，会联网下载模版文件，比较大， 使用-DarchetypeCatalog=internal，不用下载， 创建maven项目速度快。

## intellij 可以直接使用现有maven模板

https://cloud.tencent.com/developer/article/1705945

这个链接详细介绍了maven的作用以及如何使用idea里的maven模板

## vim使用

https://www.tutorialspoint.com/vim/vim_editing.htm

https://www.thegeekdiary.com/mac-terminal-vim-editor-commands/

https://blog.csdn.net/ma950924/article/details/103407871

vim文件尾部要以fi结尾
---


## MyBatis

https://blog.csdn.net/chaizepeng/article/details/119384531

mybatis是一款用于持久层的、轻量级的半自动化ORM框架，封装了所有jdbc操作以及设置查询参数和获取结果集的操作，支持自定义sql、存储过程和高级映射。

框架用于持久层，就是说这个框架是和数据库进行交互的，用于数据库中数据操作的框架。

轻量级框架的概念可以简单的理解为所用框架开发的程序启动时占用的资源少、对业务代码的侵入性不强、比较容易配置、使用和部署简单、独立部署即可使用无需依赖另外的框架，这种就是轻量级框架，相反的就是重量级。在互联网飞速发展和产品迭代更新速度如此之快的今天，轻量级的框架更容易被接受，这也是spring胜出，EJB退出的原因。

java中的数据类和数据库之间的类型系统不同，因此在使用java处理数据库时，需要进行对应的类型转化，而mybatis可以做这个事，可以将java中的类型一一映射到数据库的字段类型上，因此可以将其看作是一个ORM框架。那为什么又是半自动ORM框架呢？使用mybatis，需要手动配置pojo、sql和映射关系，用户可以自定义sql，这些sql是针对于处理数据库的，但是这些sql需要接受一些查询java类型的参数，或者是返回结果集封装到java类中，这些是需要配置的，因此mybatis是一个半自动ORM框架。说到底还是因为需要写sql，才能将数据库中的数据映射到java类中，而不是直接根据java类获取到对应数据库中数据。

高级映射是什么，这里可以类比数据表之间的映射关系，也就是一对一、一对多、多对多。

The MyBatis SQL mapper framework makes it easier to use a relational database with object-oriented applications.

### Latest version 3.5.9

https://github.com/mybatis/mybatis-3/releases

### Java connector: 最新8.0.29

https://dev.mysql.com/downloads/connector/j/

# maven mybatis 项目配置

安装配置完maven以后，在idea里面设置maven的路径。然后创建新的maven项目，在pom.xml里面加上mysql，junit，springboot，mybatis依赖包。注意我们并不需要创建一个springboot文件。然后编写实例文件(pojo/xxx), mapper文件(dao/mapper和dao/mapper.xml)，和util文件(util/util). 然后在resources里写BatisConfig.xml文件，含数据库名称密码，指向所有mapper文件。最后为了确保xml文件没有被遗漏，在pom里加上main和resources的文件读取。
然后在test里面编写unittest文件，run。

## pojo/xxx 里面需要注意的

记得写
- xxx(){} method
- xxx(name, pwd){this.name=name; this.pwd=pwd;} method
- toString() method (不然打印出来的是object)

## dao/mapper.xml
写的是sql语句

## 报错： mybatis：Error parsing SQL Mapper Configuration. Cause: java.io.IOException: Could not find resource

https://its201.com/article/BlackPlus28/108218098

## 参考网站

https://www.songbingjia.com/nginx/show-199590.html

有比较复杂的mapper

https://blog.csdn.net/weixin_51080803/article/details/118926604

mybatis mysql maven 项目

https://blog.csdn.net/qq_41962928/article/details/79854689

使用MyBatis+maven连接数据库

https://www.cnblogs.com/homejim/p/9613205.html

mybatis maven项目

https://blog.csdn.net/weixin_43823808/article/details/114142592

MyBatis——IDEA中使用Maven搭建MyBatis框架，让它跑起来

https://blog.csdn.net/weixin_45802810/article/details/118632039

完整配置+测试

https://blog.csdn.net/weixin_33770878/article/details/91633134

在web项目中应用Mybatis
---


https://blog.csdn.net/weixin_44739184/article/details/123312303

写alias
mapper sql解释
---


https://juejin.cn/post/6844903631548841991

详细的sql注释
---


https://medium.com/ryanjang-devnotes/spring-connect-spring-boot-to-db-with-mybatis-de6f82d12a26

 Connect Spring Boot to MySQL with MyBatis
---

https://codeantenna.com/a/7x7NFuYm4a

IDEA搭建mybatis框架的maven项目
---

https://www.superweb999.com/article/190132.html

maven mybatis 项目配置
---

## mybatis web项目

https://blog.csdn.net/brok1n/article/details/66973449

含有webapp文件夹，web-inf
---

# 非常详细的mybatis应用案例

https://zhuanlan.zhihu.com/p/351830443
---


