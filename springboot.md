## 关于springboot

Java Spring Boot (Spring Boot) is a tool that makes developing web application and microservices with Spring Framework faster and easier through three core capabilities: Autoconfiguration. An opinionated approach to configuration. The ability to create standalone applications.

## springboot介绍

https://www.cnblogs.com/luzhanshi/p/10592209.html

## 用springboot插件在idea创建项目

- 社区版idea用spring initialzr插件创建springboot项目

https://blog.csdn.net/chy555chy/article/details/84970042

## MissingServletRequestParameterException

Required parameter not found. This issue arose because the java object has this parameter but is of the wrong type. i.e., mysql has updateTime in Datetime but java object has updateTime in String.

## 时区差别
### 检查服务器时区： date -R
https://my.oschina.net/u/2474820/blog/521184

### 检查jdbc driver
&useTimezone=true&serverTimezone=GMT%2B8
https://help.fanruan.com/finereport/doc-view-3891.html

### 检查mysql 时区
mysql -u root -p
select now();
https://www.shuzhiduo.com/A/RnJW3owwJq/

### check springboot 时区
TimeZone.setDefault(TimeZone.getTimeZone("Asia/Shanghai"))；
https://blog.csdn.net/XiaoWenJava123/article/details/99431805
TimeZone.setDefault(TimeZone.getTimeZone("GMT+8"));
https://blog.csdn.net/zhongzk69/article/details/98601125
这两种都没用，最后解决方式在application.yml里面写:
spring:
    jackson:
        time-zone: GMT+8
参考链接： 
https://blog.csdn.net/a823007573/article/details/89489323


## 求两个时间的差

https://www.geeksforgeeks.org/find-the-duration-of-difference-between-two-dates-in-java/#:~:text=Parse%20both%20start_date%20and%20end_date,getTime().

```java
// Calucalte time difference
            // in milliseconds
            long difference_In_Time
                = d2.getTime() - d1.getTime();

                long difference_In_Minutes
                = (difference_In_Time
                   / (1000 * 60))
                  % 60;
```


