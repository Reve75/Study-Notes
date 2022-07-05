## dynamic select

https://stackoverflow.com/questions/19500425/dynamic-select-sql-statements-with-mybatis

https://mybatis.org/mybatis-3/dynamic-sql.html

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

