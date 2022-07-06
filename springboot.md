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

