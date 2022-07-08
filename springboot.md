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

## SpringBoot @Scheduled

https://juejin.cn/post/6844904164284170247

这个链接有异步执行，@Conditional

cron表达式语法
[秒] [分] [小时] [日] [月] [周] [年]
每天23点执行一次：0 0 23 * * ?

**使用@ConditionalOnProperty**
@ConditionalOnProperty(prefix="scheduled",name = "enable", havingValue = "true")

配置文件application.properties
scheduled.enable=true

more on Conditional: 
https://stackoverflow.com/questions/18406713/how-to-conditionally-enable-or-disable-scheduled-jobs-in-spring

Did not study this part as I do not have to use Conditional for now.

## Springboot 在项目启动时将数据缓存到全局变量

https://blog.csdn.net/Alice_qixin/article/details/101547611

https://blog.wjup.top/2020/06/09/springboot%E8%AE%BE%E7%BD%AE%E5%85%A8%E5%B1%80%E5%8F%98%E9%87%8F/

```java
 
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
 
@Component
public class CodeCache {
    public static Map<String, TownNameDto> codeMap = new HashMap<String, TownNameDto>();
    public static Map<String, CompanyModel> companyMap = new HashMap<String, CompanyModel>();
 
    @Autowired
    private CityDao cityDao;
    @Autowired
    private CompanyDao companyDao;
 
 
    @PostConstruct
    public void init() {
        //系统启动中。。。加载codeMap
        List<TownNameDto> codeList = cityDao.selectCityNameAndCodeALL();
        for (TownNameDto code : codeList) {
            codeMap.put(code.getTownCode() + code.getValue(), code);
        }
        List<CompanyModel> companyModels = companyDao.selectCompanies();
        for (CompanyModel company : companyModels) {
            companyMap.put(company.getCode(), company);
        }
 
 
    }
 
    @PreDestroy
    public void destroy() {
        //系统运行结束
    }
 
    @Scheduled(cron = "0 0 0/2 * * ?")
    public void testOne() {
        //每2小时执行一次缓存
        init();
    }
 
}


```

### Springboot--设置全局常量使用 第2种方法

https://blog.csdn.net/weixin_43606226/article/details/105227007

**创建一个资源文件 properties。这里创建一个content.properties**

```xml
content.size=10
content.name=test
```
```java
//注册到Spring容器
@Component
//指定常量资源路径
@PropertySource("classpath:content.properties")
public class Content {
    //创建相应属性
	//直接使用注解获取常量值
	
    @Value("${content.size}")
    private Integer size;
    @Value("${content.name}")
    private String name;

    public Integer getSize() {
        return size;
    }

    public void setSize(Integer size) {
        this.size = size;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

## MySQL - java链接mysql8 并兼容链接mysql5 亲测可用

https://blog.csdn.net/ITzhangdaopin/article/details/116238636

```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.11</version>
</dependency>


```
链接URL修改:

jdbc.driverClassName=com.mysql.jdbc.Driver
database.url=jdbc:mysql://127.0.0.1:3306/demo?useSSL=false&allowMultiQueries=true&serverTimezone=Asia/Shanghai

mysql5.7 的驱动版本
https://www.cxyzjd.com/article/weixin_39559097/113218143



## How to create a JAR file with Maven in IntelliJ

https://www.tutorialworks.com/intellij-maven-create-jar/

https://www.cnblogs.com/acm-bingzi/p/6625303.html
jar打包

https://roytuts.com/create-both-war-and-jar-files-using-maven/

https://blog.csdn.net/sinat_35790812/article/details/90210387

https://www.jb51.net/article/212993.htm

https://blog.csdn.net/LXWalaz1s1s/article/details/107607607

https://blog.csdn.net/theKingOfCoding/article/details/114937857


## Getting "cannot find Symbol" in Java project in IntelliJ

https://stackoverflow.com/questions/12132003/getting-cannot-find-symbol-in-java-project-in-intellij

**Select Build->Rebuild Project will solve it**

## Spring NumberFormatException

https://stackoverflow.com/questions/32679451/spring-numberformatexception-failed-to-convert-value-of-type-java-lang-string

The number you are trying to convert to java.lang.Long is -26.2041028.

Your number contains a .(decimal). This is not allowed for Longs. You need to use java.lang.Double.

And also succeed your number with an L for Long or a D for Double for static initializations. Even though not required, it makes the code more readable.

Like, -26.2041028D for Double.

## SpringBoot 启动类 @SpringBootApplication 注解 以及执行流程

https://blog.csdn.net/qq_28289405/article/details/81302498

@ComponentScan这个注解在Spring中很重要，它对应XML配置中的元素，@ComponentScan的功能其实就是自动扫描并加载符合条件的组件（比如@Component和@Repository等）或者bean定义，最终将这些bean定义加载到IoC容器中。

@EnableAutoConfiguration 简单概括一下就是，借助@Import的支持，收集和注册特定场景相关的bean定义。

@EnableScheduling是通过@Import将Spring调度框架相关的bean定义都加载到IoC容器。
@EnableMBeanExport是通过@Import将JMX相关的bean定义加载到IoC容器。

@EnableAutoConfiguration自动配置的魔法骑士就变成了：从classpath中搜寻所有的META-INF/spring.factories配置文件，并将其中org.springframework.boot.autoconfigure.EnableutoConfiguration对应的配置项通过反射（Java Refletion）实例化为对应的标注了@Configuration的JavaConfig形式的IoC容器配置类，然后汇总为一个并加载到IoC容器。

## Adding headers when using httpClient.GetAsync

https://stackoverflow.com/questions/29801195/adding-headers-when-using-httpclient-getasync

没试过，没仔细看

## Spring request parameters

https://www.baeldung.com/spring-request-param

```java
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(@RequestParam(required = false) String id) { 
    return "ID: " + id;
}

@PostMapping("/api/foos")
@ResponseBody
public String addFoo(@RequestParam(name = "id") String fooId, @RequestParam String name) { 
    return "ID: " + fooId + " Name: " + name;
}
```

## Differences between @RequestParam and @PathVariable annotations in Spring MVC

https://javarevisited.blogspot.com/2017/10/differences-between-requestparam-and-pathvariable-annotations-spring-mvc.html#axzz7UmKDSftk

For example, if the incoming HTTP request to retrieve a book on topic "Java" is http://localhost:8080/shop/order/1001/receipts?date=12-05-2017, then you can use the @RequestParam annotation to retrieve the query parameter date and you can use @PathVariable to extract the orderId i.e. "1001" as shown below:

```java
@RequestMapping(value="/order/{orderId}/receipts", method = RequestMethod.GET)
public List listUsersInvoices( @PathVariable("orderId") int order,
 @RequestParam(value = "date", required = false) Date dateOrNull) {
...
}
```

Read more: https://javarevisited.blogspot.com/2017/10/differences-between-requestparam-and-pathvariable-annotations-spring-mvc.html#ixzz7YEySxKVj

### Spring @RequestParam vs @PathVariable Annotations

https://www.baeldung.com/spring-requestparam-vs-pathvariable

https://www.baeldung.com/spring-request-param

https://stackoverflow.com/questions/12296642/is-it-possible-to-have-empty-requestparam-values-use-the-defaultvalue


## JSON Parameters with Spring MVC

https://www.baeldung.com/spring-mvc-send-json-parameters#:~:text=Send%20JSON%20Parameter%20in%20GET,parameter%20as%20a%20simple%20string.

```java
@GetMapping("/get")
@ResponseBody
public Product getProduct(@RequestParam String product) throws JsonMappingException, JsonProcessingException {
    Product prod = objectMapper.readValue(product, Product.class);
    return prod;
}
```

## Content type 'application/x-www-form-urlencoded;charset=UTF-8' not supported for @RequestBody MultiValueMap

https://stackoverflow.com/questions/33796218/content-type-application-x-www-form-urlencodedcharset-utf-8-not-supported-for

The problem is that when we use application/x-www-form-urlencoded, Spring doesn't understand it as a RequestBody. So, if we want to use this we must remove the @RequestBody annotation.

```java
@RequestMapping(value = "/{email}/authenticate", method = RequestMethod.POST,
        consumes = MediaType.APPLICATION_FORM_URLENCODED_VALUE, 
        produces = {MediaType.APPLICATION_ATOM_XML_VALUE, MediaType.APPLICATION_JSON_VALUE})
public @ResponseBody  Representation authenticate(@PathVariable("email") String anEmailAddress, MultiValueMap paramMap) throws Exception {
   if(paramMap == null && paramMap.get("password") == null) {
        throw new IllegalArgumentException("Password not provided");
    }
    return null;
}

```

## 微信小程序开发【前端+后端（java）】

https://blog.csdn.net/zwb19940216/article/details/81023191

@RestController与@Controller注解的区别@RestController相当于两个注解，它能实现将后端得到的数据在前端页面（网页）中以json串的形式传递。而微信小程序与后台之间的数据传递就是以json报文的形式传递。所以这就是选择springboot框架开发小程序后端的主要原因之一。

比较全面的springboot小程序开发

### SpringBoot+mysql搭建微信小程序后台（2）连接数据库和后端代码

https://blog.csdn.net/m0_48878393/article/details/119083346

这两个链接很不错，参考了不少

### 小程序的简单后台搭建（基于SpringBoot+Mybatis）

http://t.csdn.cn/ckNRd

https://blog.csdn.net/qq_21537671/article/details/98847630?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-8-98847630-blog-113735330.pc_relevant_antiscanv2&spm=1001.2101.3001.4242.5&utm_relevant_index=11

挺详细，不错

## springboot+mybatis整合

https://blog.csdn.net/huangwei18351/article/details/85235500

不错

## idea使用maven搭建mybatis项目连接mysql完整版

https://blog.csdn.net/weixin_44835979/article/details/107521273

**非常详细的解释，参考了很多次**

### 在idea中创建maven工程，搭建mybatis框架，完成单表增删改查操作

https://blog.csdn.net/weixin_46136820/article/details/120313464

也很不错，参考了很多

### IDEA创建并配置Spring boot+Mybatis+Maven项目

https://blog.csdn.net/cty_com/article/details/96104078

不错，参考了不少

## SpringBoot项目Mybatis连接MySQL以及前端访问文件配置

https://blog.csdn.net/qq_26012495/article/details/81260120

不错，讲了postman测试


## eclipse里面springboot项目和maven module创立

https://juejin.cn/post/6844903910755270670

没有用到

### 也是eclipse

http://www.360doc.com/content/20/1113/20/65840031_945697074.shtml

不少mybatis部分，也不错，有个踩坑总结点不错

### Eclipse SpringBoot+mybatis搭建小程序

https://blog.csdn.net/Adonis_D_Gogh/article/details/79419975


## 小程序上基于Springboot+mybatis+mysql实现登陆、注册功能

https://blog.csdn.net/qq_42487559/article/details/104070164

完整注册功能，但是是简单用户名密码


## 利用spring自动注入list,map性质

https://blog.51cto.com/u_15257216/2862672

### 例子

https://blog.csdn.net/weixin_39769767/article/details/114134642

### 全面的官方map operations

https://docs.oracle.com/javase/8/docs/api/java/util/Map.html

https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html

## springboot中使用requestBody注解接收json串

https://blog.csdn.net/taiguolaotu/article/details/105390113

```java

@RequestMapping(path = "/addOrgposNoparametercheck", method = RequestMethod.POST, produces ="application/json;charset=UTF-8" )
    public int addOrgposNoparametercheck(@RequestBody SysOrgpos sysOrgpos)  {
        return sysOrgposService.addOrgposNoparametercheck(sysOrgpos);
    }
```

**@RequestBody SysOrgpos sysOrgpos 这种形式会将JSON字符串中的值赋予SysOrgpos 中对应的属性上,需要注意的是，JSON字符串中的key必须对应user中的属性名，否则是请求不过去的。**

## 为什么main方法启动类SpringApplication需要在项目根目录，以及标注的意义

https://cloud.tencent.com/developer/article/1639231#:~:text=%E5%90%AF%E5%8A%A8%E7%B1%BB%E8%87%AA%E8%BA%AB%E6%98%AF%E4%B8%80%E4%B8%AA,%E4%BD%BF%E7%94%A8%E8%BF%99%E4%B8%89%E4%B8%AA%E6%B3%A8%E8%A7%A3%E3%80%82

@SpringBootConfiguration，@ComonentScan，@EnableAutoConfiguration

## Springboot整合微信小程序实现登录与增删改查

https://blog.51cto.com/u_15466961/4837849

非常完整的例子，很不错

### SpringBoot+MyBatis搭建迷你小程序

https://codeantenna.com/a/yn0nFtRVug

不错

## 微信小程序的springboot后端写法，包括发送订阅消息

https://tuojinhui.github.io/wechat/ma/MiniApp.html#%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E8%8E%B7%E5%8F%96phonenumber-openid-nickname-avatarurl

不错

## 跨域问题和options

https://blog.csdn.net/socct_yj/article/details/107233627

SpringBoot里也好办，在application.yml里配置

```xml
# 允许预检请求
spring:
  mvc:
    dispatch-options-request: true
```

