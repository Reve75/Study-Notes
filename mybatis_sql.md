# JDBC（JavaDataBase Connectivity）就是Java数据库连接，说白了就是用Java语言来操作数据库。

mybatis是一个持久层ORM框架。它内部封装了jdbc，可以通过xml或注解完成ORM映射关系配置。使开发更简洁，更高效。使用Mybatis，可以让开发者只需要关注sql语句本身，简化JDBC操作，不需要在关注加载驱动、创建连接、处理SQL语句等繁杂的过程。下面来看一下通过Mybatis又是如何连接并操作数据库的。

## mybatis

http://lidol.top/frame/3359/

用户数据库的增改删查+测试

## dynamic select

https://stackoverflow.com/questions/19500425/dynamic-select-sql-statements-with-mybatis

https://mybatis.org/mybatis-3/dynamic-sql.html

https://mybatis.org/mybatis-3/sqlmap-xml.html

https://mybatis.org/mybatis-dynamic-sql/docs/insert.html

Good example of many sql statements

## mybatis config settings

https://mybatis.org/mybatis-3/configuration.html#settings

## insert null in db

https://stackoverflow.com/questions/16191296/insert-null-in-a-database

<settings>
        <setting name="jdbcTypeForNull" value="NULL" />
</settings>


## upsert
update insert statement

https://stackoverflow.com/questions/28993805/mybatis-do-a-fetch-and-based-on-return-value-do-an-update-insert-inside-the-xxxm


## mapper.xml根据时间筛选sql

https://blog.csdn.net/qq_22860341/article/details/82801585

```sql
<if test="beginTime != null and beginTime !='' ">
			<![CDATA[
				and	DATE_FORMAT(create_time, '%Y-%m-%d')>= DATE_FORMAT(#{beginTime}, '%Y-%m-%d')
			]]>
		</if>
		<if test="endTime != null and endTime !='' ">
			<![CDATA[
				and	DATE_FORMAT(create_time, '%Y-%m-%d')<= DATE_FORMAT(#{endTime}, '%Y-%m-%d')
			]]>
		</if>
```

https://www.bbsmax.com/A/E35pPbjL5v/

**这个非常全面，时间有关查询都有**

```sql
<if test="saleDateStart != null">
                and DATE_FORMAT(info.sale_date,'%Y-%m-%d') &gt;= DATE_FORMAT(#{saleDateStart},'%Y-%m-%d')
            </if>
            <if test="saleDateEnd != null">
                and DATE_FORMAT(info.sale_date,'%Y-%m-%d') &lt;= DATE_FORMAT(#{saleDateStart},'%Y-%m-%d')
            </if>
       
```

```sql
SELECT
    id,
    date_0
FROM
    worksheet_data_30
WHERE
    DATE_FORMAT( date_0, '%Y-%m-%d %H:%i:%S' ) = DATE_FORMAT( '2019-06-05 09:35:06', '%Y-%m-%d %H:%i:%S' )
```

**当天数据**
```xml
select * from security_code_config  where DATE_FORMAT(create_date,'%Y-%m-%d') = DATE_FORMAT(NOW(),'%Y-%m-%d')
```

**最近7天数据**
```sql
SELECT
    create_date,
    IFNULL(sum(security_code_total), 0) createSCNum,
    IFNULL(sum(print_num), 0) printNum
FROM
    security_code_config
WHERE
    tid = 'ten_pisen'
AND
    DATE_FORMAT(create_date,'%Y-%m-%d') <= DATE_FORMAT('2019-03-12','%Y-%m-%d')
AND
    DATE_FORMAT(create_date,'%Y-%m-%d') >= DATE_FORMAT('2019-03-01','%Y-%m-%d')
GROUP BY DATE_FORMAT(create_date,'%Y-%m-%d')
```

**最近6个月**

```sql
SELECT
    create_date,
    IFNULL(sum(security_code_total), 0) createSCNum,
    IFNULL(sum(print_num), 0) printNum
FROM
    security_code_config
WHERE
    tid = 'ten_pisen'
AND
    DATE_FORMAT(create_date,'%Y-%m-%d') <= DATE_FORMAT('2019-03-12','%Y-%m-%d')
AND
    DATE_FORMAT(create_date,'%Y-%m-%d') >= DATE_FORMAT('2018-10-01','%Y-%m-%d')
GROUP BY DATE_FORMAT(create_date,'%Y-%m')
```

**format参数的格式有**

%a	缩写星期名
%b	缩写月名
%c	月，数值
%D	带有英文前缀的月中的天
%d	月的天，数值(00-31)
%e	月的天，数值(0-31)
%f	微秒
%H	小时 (00-23)
%h	小时 (01-12)
%I	小时 (01-12)
%i	分钟，数值(00-59)
%j	年的天 (001-366)
%k	小时 (0-23)
%l	小时 (1-12)
%M	月名
%m	月，数值(00-12)
%p	AM 或 PM
%r	时间，12-小时（hh:mm:ss AM 或 PM）
%S	秒(00-59)
%s	秒(00-59)
%T	时间, 24-小时 (hh:mm:ss)
%U	周 (00-53) 星期日是一周的第一天
%u	周 (00-53) 星期一是一周的第一天
%V	周 (01-53) 星期日是一周的第一天，与 %X 使用
%v	周 (01-53) 星期一是一周的第一天，与 %x 使用
%W	星期名
%w	周的天 （0=星期日, 6=星期六）
%X	年，其中的星期日是周的第一天，4 位，与 %V 使用
%x	年，其中的星期一是周的第一天，4 位，与 %v 使用
%Y	年，4 位
%y	年，2 位

### 按照日期查询
https://www.codeleading.com/article/94695492055/

```sql
select * from `order`
where orderDate >= date(now())
and orderDate < DATE_ADD(date(now()),INTERVAL 1 DAY)
```

xml不识别'<'
使用转义字符来表示（'<' = &lt;）

## Navicat 设置 varchar 无法输入中文解决办法

https://blog.csdn.net/runtu999/article/details/124510470

需要在navicat把varchar设置为utf8

## mybatis写当天 当月的数据 时间段数据

https://blog.csdn.net/Zhi_Sheng/article/details/78910082

**昨天的数据**

```sql
SELECT * FROM 表名 WHERE TO_DAYS( NOW( ) ) - TO_DAYS( 时间字段名) <= 1
```

**7天的数据**

```sql
SELECT * FROM 表名 where DATE_SUB(CURDATE(), INTERVAL 7 DAY) <= date(时间字段名)
```

**30天的数据**

```sql
SELECT * FROM 表名 where DATE_SUB(CURDATE(), INTERVAL 30 DAY) <= date(时间字段名)
```

**上个月**

```sql
SELECT * FROM 表名 WHERE PERIOD_DIFF( date_format( now( ) , '%Y%m' ) , date_format( 时间字段名, '%Y%m' ) ) =1
```

**本季度**

```sql
select * from `ht_invoice_information` where QUARTER(create_date)=QUARTER(now());
```

**上个季度**

```sql
select * from `ht_invoice_information` where QUARTER(create_date)=QUARTER(DATE_SUB(now(),interval 1 QUARTER));
```

**当前这周的数据**

```sql
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now());
```

**上周的数据**

```sql
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now())-1;
```

**距离当前现在6个月的数据**
```sql
select name,submittime from enterprise where submittime between date_sub(now(),interval 6 month) and now();
```

**数据查询**
```sql
<select id="方法名" parameterType="参数类型" resultType="返回类型">
       select *from jw_order where 1=1            
       <if test="tj_start!= null and tj_start!=''">
        AND submittime&gt;=#{tj_start}
       </if>
       <if test="tj_end!=null and tj_end!=''">
        AND submittime&lt;=#{tj_end}
       </if>
    </select>
```

**模糊查询sql**

```sql
 <select id="方法" parameterType="参数类型" resultType="返回类型">
 select *from 表名 where 1=1       
 AND 字段 LIKE CONCAT(CONCAT('%', #{参数}), '%')
</select>
```

**周一到周五每天的统计结果**

```sql
 SELECT COUNT(*),DAYNAME(CreateTime) FROM t_voipchannelrecord WHERE YEAR(CreateTime) = '2016' GROUP BY DAYNAME(CreateTime) 
```

**统计本周数据**

```sql
 SELECT COUNT(*) FROM t_voipchannelrecord WHERE MONTH(CreateTime) =
MONTH(CURDATE()) AND WEEK(CreateTime) = WEEK(CURDATE())
```
    
**按月统计**

```sql
SELECT COUNT(*),MONTH(CreateTime) FROM t_voipchannelrecord WHERE YEAR(CreateTime) = '2016' GROUP BY MONTH(CreateTime) 
```

**按季统计**

```sql
SELECT COUNT(*),QUARTER(CreateTime) FROM t_voipchannelrecord WHERE YEAR(CreateTime) = '2016' GROUP BY QUARTER(CreateTime) 
```


**按年统计**

```sql
SELECT COUNT(*),YEAR(CreateTime) FROM t_voipchannelrecord  GROUP BY YEAR(CreateTime) 
```

## java.lang.ClassNotFoundException: Cannot find class

https://www.cnblogs.com/biehongli/p/13416457.html

```xml
<resultMap id="userMap" type="com.bie.shiro.po.User">
 9         <id property="uid" column="uid"></id>
10         <result property="username" column="username"></result>
11         <result property="password" column="password"></result>
12         <collection property="roleSet" ofType="com.bie.shiro.po.Role">
13             <id property="rid" column="rid"></id>
14             <result property="rname" column="rname"></result>
15             <collection property="permissionSet" ofType="com.bie.shiro.po.Permission">
16                 <id property="pid" column="pid"></id>
17                 <result property="pname" column="pname"></result>
18                 <result property="url" column="url"></result>
19             </collection>
20         </collection>
21     </resultMap>

<select id="findByUsername" parameterType="string" resultMap="userMap">
30        SELECT
```

## Mybatis的java对象名和数据库表名不同

https://codeleading.com/article/61962794982/

```xml
<resultMap type="com.struts.entity.User" id="UserList">
	<!-- 主键 -->
	<id column="userid" jdbcType="VARCHAR" property="userid" />
	<result column="username" jdbcType="VARCHAR" property="username" />
	<result column="registDate" jdbcType="VARCHAR" property="registDate" />
	<result column="password" jdbcType="VARCHAR" property="password" />
</resultMap>
```
用resultMap进行映射

## 从object到mapper xml详细的解说

https://blog.51cto.com/u_15127575/4089599

很完整

## select,insert,update中用if

https://www.modb.pro/db/137958

不错。各种if的使用方法。

## MyBatis - Mapped Statements collection already contains value for

https://stackoverflow.com/questions/37085803/mybatis-mapped-statements-collection-already-contains-value-for

If you have the same method name, then mybatis throws the Mapped Statements collection already contains value error message. So the solution is to have different method names for different mapper statements even if the method signatures are different.

## More examples

https://www.alibabacloud.com/blog/mybatis-with-a-more-fluent-experience_598062

## inserting true/false - data type

https://stackoverflow.com/questions/3709507/storing-boolean-values-in-sql

Use the bit data type instead for your column.

## SQL selecting rows by most recent date with two unique columns

https://stackoverflow.com/questions/189213/sql-selecting-rows-by-most-recent-date-with-two-unique-columns

```sql
SELECT
  CHARGEID,
  CHARGETYPE,
  MAX(SERVICEMONTH) AS "MostRecentServiceMonth"
FROM INVOICE
GROUP BY CHARGEID, CHARGETYPE
```

## Slf4j获取日志对象(Logger)的实现分析

https://blog.csdn.net/Revivedsun/article/details/85208866

```java
 Logger logger = LoggerFactory.getLogger(Main.class);
```

## select with limit

https://www.w3schools.com/sql/sql_ref_select_top.asp

```sql
SELECT * FROM Customers
LIMIT 3;
```

## Inserting with trimming

https://programmer.group/the-default-value-of-mysql-field-inserted-by-mybatis-does-not-take-effect.html

```sql
<sql id="blogColumns">  
    <trim suffixOverrides=",">  
        <if test="title != null">title,</if>  
        <if test="author != null">author,</if>  
        <if test="content != null">content</if>  
    </trim>  
</sql>  
  
<sql id="blogValues">  
    <trim suffixOverrides=",">  
        <if test="title != null">#{title},</if>  
        <if test="author != null">#{author},</if>  
        <if test="content != null">#{content}</if>  
    </trim>  
</sql>  
  
<insert id="addOneBlog" parameterType="Blog">  
    insert into blog(<include refid="blogColumns"/>)  
    values (<include refid="blogValues"/>)  
</insert>  
```

## if-statement in mybatis insert query

https://stackoverflow.com/questions/51519368/if-statement-in-mybatis-insert-query

```sql
INSERT INTO table (
      ... other columns ...,
      <if test="i9TB1000_CODRIC != null">
          I9TB1000_CODRIC,
      </if>
      <if test="i9TB1000_PROGRIC != null">
      I9TB1000_PROGRIC,
      </if>
      ... other columns ...
) VALUES (
     ... values ...
)
```

## insert with trim

https://programmer.group/the-default-value-of-mysql-field-inserted-by-mybatis-does-not-take-effect.html

```sql
<sql id="blogColumns">  
    <trim suffixOverrides=",">  
        <if test="title != null">title,</if>  
        <if test="author != null">author,</if>  
        <if test="content != null">content</if>  
    </trim>  
</sql>  
  
<sql id="blogValues">  
    <trim suffixOverrides=",">  
        <if test="title != null">#{title},</if>  
        <if test="author != null">#{author},</if>  
        <if test="content != null">#{content}</if>  
    </trim>  
</sql>  
  
<insert id="addOneBlog" parameterType="Blog">  
    insert into blog(<include refid="blogColumns"/>)  
    values (<include refid="blogValues"/>)  
</insert>  
```

## adding null test

https://stackoverflow.com/questions/55861001/mybatis-update-if-a-field-in-the-source-object-is-not-null

```sql
<if test='description != null'>
```

## Insert null in a database

https://stackoverflow.com/questions/16191296/insert-null-in-a-database

```xml
<settings>
        <setting name="jdbcTypeForNull" value="NULL" />
</settings>
```

## Updating multiple database rows in Spring - Mybatis

https://stackoverflow.com/questions/35480461/updating-multiple-database-rows-in-spring-mybatis

```xml
<!--mapper xml-->
<update id="updateEmployeeTrips" parameterType="java.util.List">
    <foreach collection="list" item="employeeTrips" index="index" separator=";">
        update employee_trips set pickup_drop_time = #{employeeTrips.pickupTime} where id = #{employeeTrips.id}
    </foreach>
</update>

```

```java
// mapper java
updateEmployeeTrips(List<employeeTrip> employeeTripList)
```

## sql sample

https://github.com/mybatis/mybatis-3/wiki/FAQ#what-is-the-difference-between--and-

very comprehensive.
covers wildcard, String/Integer parameter type, retrieving value of autogenerated key, batch insert. There is no need to use $. Only # needed.

## MySQLSyntaxErrorException: Mybatis :Bulk update query using foreach

https://stackoverflow.com/questions/28673237/mysqlsyntaxerrorexception-mybatis-bulk-update-query-using-foreach

Solution: 
**enable the multiple update in the jdbc url. You should append the parameter allowMultiQueries=true into the url of jdbc**

### Alternatively

https://developpaper.com/mybatis-batch-updates-in-three-ways/

```xml
<update id="updateBatch"  parameterType="java.util.List">  
    <foreach collection="list" item="item" index="index" open="" close="" separator=";">
        update tableName
        <set>
            name=${item.name},
            name2=${item.name2}
        </set>
        where id = ${item.id}
    </foreach>      
</update>
```

**But by default, SQL statements in Mybatis mapping files do not support execution of multiple SQL statements ending with “;”. So you need to add & allow MultiQueries = true to the URL that connects Mysql to execute.**

### JDBC URL setting Allowmultiqueries to True and false when the underlying processing mechanism is studied

https://topic.alibabacloud.com/a/jdbc-url-setting-allowmultiqueries-to-true-and-false-when-the-underlying-processing-mechanism-is-studied_8_8_30095746.html

```sql
Allowmultiqueriesallow the use of '; ' to delimit multiple queries during one statement (True/false), defaults to ' false ', And does not affect the Addbatch () and ExecuteBatch () methods, which instead rely on RewriteBatchStatements.Default:false Since version:3.1.1
```

### Alternatively

https://blog.karatos.in/a?ID=01800-f2db2faf-a5bb-4625-9430-3d68cfd96186

similar to above links.

```xml
<update id="xxxx" parameterType="java.util.List">
        <foreach collection="list" item="user" separator=";">
            update t_xxx_user set is_default = #{user.isDefault}
            where id = #{user.id}
        </foreach>
    </update>
```

```yml
jdbc:mysql://xxxx:3306/hc_insurance_center?useUnicode=true&characterEncoding=utf-8&useSSL=false&allowMultiQueries=true
```

## ExecutorException: Error getting generated key or setting result to parameter object

https://blog.csdn.net/weixin_44299027/article/details/105528727

useGeneratedKeys = true （使用生成的主键） 这个表示插入数据之后返回一个自增的主键id给你对应实体类中的主键属性。通过这个设置可以解决在主键自增的情况下通过实体的getter方法获取主键（当然还需要keyproperty指明数据库中返回的主键id给实体类中的哪个属性）。
keyproperty = 主键，这样就可以解决在主键自增的情况下获取主键。


## Spring Boot整合MyBatis

http://c.biancheng.net/spring_boot/mybatis.html

不错

## SpringBoot集成Mybatis

https://zhuanlan.zhihu.com/p/160901686

不错

## Spring Boot中使用MyBatis详解

https://blog.csdn.net/m0_46696320/article/details/105472191

不错

## mybatis 和 jdbc两种方法操作数据库

http://lidol.top/frame/3359/

不错

## pass multiple parameters and use them

https://stackoverflow.com/questions/24968088/how-can-i-pass-multiple-parameters-and-use-them

Do not specify parameterType but use @Param annotation on parameters in mapper:

```java
@Mapper
public interface MyMapper {

    void update(@Param("a") A a, @Param("b") B b);

    ...
}
```

```xml
<update id="update" > 
   UPDATE SOME WHERE x=#{a.x} AND y=#{b.y}
</update>
```

e.g.

```java
void mapCategoryAndPage(@Param("categoryLocalId") Long categoryLocalId, @Param("pageLocalId") Long localId);

```

```xml
<insert id="mapCategoryAndPage" parameterType="map">
    INSERT INTO
        category_page_mapping (
            page_local_id,
            category_local_id)
    VALUES
        (#{pageLocalId},
         #{categoryLocalId});
</insert>
```

## Add seconds to current date using Calendar.add() method in Java

https://www.tutorialspoint.com/add-seconds-to-current-date-using-calendar-add-method-in-java

```java
Calendar calendar = Calendar.getInstance();
      System.out.println("Current Date = " + calendar.getTime());
      
      
      calendar.add(Calendar.SECOND, 15);
```

## How to get the current date/time in Java

https://stackoverflow.com/questions/5175728/how-to-get-the-current-date-time-in-java#:~:text=on%20this%20post.-,Use%3A,getInstance().

```java
String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss").format(Calendar.getInstance().getTime());
```

```java
DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
Calendar cal = Calendar.getInstance();
System.out.println(dateFormat.format(cal.getTime()));
```

https://www.tutorialspoint.com/add-seconds-to-current-date-using-calendar-add-method-in-java

```java
Calendar calendar = Calendar.getInstance();

calendar.add(Calendar.SECOND, 15);
```

## retrieve values from hashmap inside a hashmap

https://stackoverflow.com/questions/49925837/to-retrieve-values-from-hashmap-inside-a-hashmap

```java

Map<String, Object> innerMap = outerMap.get("marks");

for (String key : innerMap.keySet()) {
    Object value = innerMap.get(key);
    
    
}
```

## Field 'Id' doesn't have a default value解决方法

https://blog.csdn.net/qq_38974634/article/details/81039660

设置为auto-increment

