## 3 ways Spring Boot implements timed tasks

https://programmer.ink/think/four-ways-spring-boot-implements-timed-tasks.html

1. use timer
2. Scheduled ExecutorService
3. Spring Task


## Running Scheduled Jobs in Spring Boot

https://reflectoring.io/spring-scheduler/

comprehensive.

## timer、scheduledexecutorservice、spring task、quartz

https://icode.best/i/45460247936784

不错

## Timer存在一些缺陷，因此你应该考虑使用ScheduledThreadPoolExecutor作为代替品

https://blog.51cto.com/u_15478573/4912039

## 不同方法实现定时任务

http://soiiy.com/java/14759.html

https://www.cainiaojc.com/note/qagyck.html

单机和distributed不同的实现方式

https://segmentfault.com/a/1190000041698515

## ScheduledExecutorService

https://www.javaguides.net/2018/09/scheduledexecutorservice-interface-in-java.html

https://mkyong.com/java/java-scheduledexecutorservice-examples/

https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/TaskScheduler.html

https://mkyong.com/java/java-scheduledexecutorservice-examples/

https://blog.csdn.net/lzl9421na/article/details/87881960

### How to execute a callable in the executor service

https://www.educative.io/answers/how-to-execute-a-callable-in-the-executor-service

### ScheduledExecutorService写runnable

https://blog.csdn.net/qq_35246620/article/details/78254527

非常不错，完全参考的这个写的runnable method。

### 深入理解Java线程池

https://segmentfault.com/a/1190000011443715

比较深入，没仔细看

### callable举例

https://howtodoinjava.com/java/multi-threading/scheduledexecutorservice/

不错，参考callable写法

### callable的写法

https://developer.aliyun.com/article/365026

不错，参考了callable写法

### java callable 传参数

https://blog.csdn.net/weixin_32803887/article/details/114155365

没仔细看

### 带参数的 Java 8 Runnable Lambda 和 callable lambda 写法

https://www.twle.cn/t/372

### ScheduledExecutorService和ExecutorService

https://www.cnblogs.com/yyy-blog/p/10283837.html

### ScheduledExecutorService异常处理

https://www.itranslater.com/qa/details/2582544325515150336

要写try catch

### ExecutorService的shutdown方法和awaitTermination方法

https://blog.csdn.net/Milogenius/article/details/79677922

没仔细看，用的shutdown()

### ScheduledExecutorService的停止有shutdown和shutdownNow

https://blog.csdn.net/winter_jay/article/details/89669527

不错

### Runnable写法（非单独写）

https://zhuanlan.zhihu.com/p/399724001

### Runnable 写法 （单独写）

https://www.baeldung.com/spring-task-scheduler

### 通过改变配置，使 Spring 采用多线程执行定时任务。

https://blog.51cto.com/u_10448399/2517866



## @Scheduled

https://www.tutorialspoint.com/spring_boot/spring_boot_scheduling.htm

https://developer.51cto.com/article/635616.html

https://www.jianshu.com/p/b8e8882336fd

https://blog.csdn.net/qq_35067322/article/details/103982304

https://blog.csdn.net/yzh_1346983557/article/details/86244486

加async

https://cloud.tencent.com/developer/article/1582434

@scheduled

https://www.liaoxuefeng.com/wiki/1252599548343744/1282385878450210

https://blog.csdn.net/AlbenXie/article/details/100021983

https://stackoverflow.com/questions/29388540/spring-schedule-a-task-which-takes-a-parameter

**Notice that the methods to be scheduled must have void returns and must not expect any arguments.**

### official docs

https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/scheduling.html

official docs

## Quartz

### 为spring-quartz动态设置参数

https://xcj01010203.github.io/2017/09/27/2017-09-27-%E4%B8%BAspring-quartz%E5%8A%A8%E6%80%81%E8%AE%BE%E7%BD%AE%E5%8F%82%E6%95%B0/

### springboot集成quartz实现定时任务调度

https://blog.csdn.net/Alice_qixin/article/details/113802030

### 整合Quartz作为调度中心完整实用例子

https://www.cnblogs.com/ealenxie/p/9134602.html

## Elastic job

https://juejin.cn/post/6902689757395386376

