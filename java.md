## map方法

map.containsKey(key)


**map只有key和value，没有order，每次的第一个item可能都不一样**
https://stackoverflow.com/questions/26230225/hashmap-getting-first-key-value

**Java HashMap replace()**

https://www.programiz.com/java-programming/library/hashmap/replace

map.replace(key,new value);

**How to iterate any Map in Java**

https://www.geeksforgeeks.org/iterate-map-java/

```java
for (Map.Entry<String,String> entry : gfg.entrySet()) 
    System.out.println("Key = " + entry.getKey() +
         ", Value = " + entry.getValue());

// using keySet() for iteration over keys
for (String name : gfg.keySet()) 
            System.out.println("key: " + name);
          
// using values() for iteration over values
for (String url : gfg.values()) 
            System.out.println("value: " + url);
```

**Print out all keys and values from a Map in Java**

https://www.techiedelight.com/print-all-keys-and-values-map-java/

https://stackoverflow.com/questions/5920135/printing-hashmap-in-java

```java
for (TypeKey name: example.keySet()) {
    String key = name.toString();
    String value = example.get(name).toString();
    System.out.println(key + " " + value);
}
```

## java 时间戳转换为日期格式 

https://blog.51cto.com/u_15077556/4083181

```java
Long timeLong = Long.parseLong(time);
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//要转换的时间格式
    Date date;
    try {
        date = sdf.parse(sdf.format(timeLong));
        return sdf.format(date);
    } catch (ParseException e) {
        e.printStackTrace();
        return null;
    }
```

https://www.jianshu.com/p/9ce60328e5ea

```java
public static String timeStamp2Date(String seconds,String format) {  
        if(seconds == null || seconds.isEmpty() || seconds.equals("null")){  
            return "";  
        }  
        if(format == null || format.isEmpty()){
            format = "yyyy-MM-dd HH:mm:ss";
        }   
        SimpleDateFormat sdf = new SimpleDateFormat(format);  
        return sdf.format(new Date(Long.valueOf(seconds+"000")));  
    }  
```

https://stackoverflow.com/questions/7492423/how-can-i-convert-a-timestamp-into-either-date-or-datetime-object

```java
public class DateTest {

    public static void main(String[] args) {
        Timestamp timestamp = new Timestamp(System.currentTimeMillis());
        Date date = new Date(timestamp.getTime());

        // S is the millisecond
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("MM/dd/yyyy' 'HH:mm:ss:S");

        System.out.println(simpleDateFormat.format(timestamp));
        System.out.println(simpleDateFormat.format(date));
    }
}
```



### Java Program to Convert TimeStamp to Date

https://www.geeksforgeeks.org/java-program-to-convert-timestamp-to-date/

```java
Timestamp ts
            = new Timestamp(System.currentTimeMillis());
 
        // Passing the long value in the Date class
        // constructor
        Date date = new Date(ts.getTime());
```

https://www.baeldung.com/java-datetimeformatter

```java
String timeColonPattern = "hh:mm:ss a";
DateTimeFormatter timeColonFormatter = DateTimeFormatter.ofPattern(timeColonPattern);
LocalTime colonTime = LocalTime.of(17, 35, 50);
System.out.println(timeColonFormatter.format(colonTime));
```

###  时间戳转换成时间

https://www.runoob.com/java/date-timestamp2date.html

```java
public class Main{
    public static void main(String[] args){
        Long timeStamp = System.currentTimeMillis();  //获取当前时间戳
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String sd = sdf.format(new Date(Long.parseLong(String.valueOf(timeStamp))));      // 时间戳转换成时间
        System.out.println("格式化结果：" + sd);
 
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy 年 MM 月 dd 日 HH 时 mm 分 ss 秒");
        String sd2 = sdf2.format(new Date(Long.parseLong(String.valueOf(timeStamp))));
        System.out.println("格式化结果：" + sd2);
   }
}
```

用的是这个方法

### Convert LocalDateTime to Timestamp & Vice Versa

https://www.javaprogramto.com/2021/11/java-8-convert-localdatetime-to.html

```java
LocalDate localDate = LocalDate.now();
		
Timestamp timestamp = Timestamp.valueOf(localDate.atStartOfDay());
```

## How to round a number to n decimal places in Java

https://stackoverflow.com/questions/153724/how-to-round-a-number-to-n-decimal-places-in-java

```java
(double)Math.round(value * 100000d) / 100000d
```
https://mkyong.com/java/how-to-round-double-float-value-to-2-decimal-points-in-java/#mathround

```java
double salary = Math.round(input * 100.0) / 100.0;
```

## compare whether 1 date is after the other

https://www.geeksforgeeks.org/date-after-method-in-java/

```dateObject.after(Date specifiedDate)```

## Iterating through list

https://www.geeksforgeeks.org/iterate-through-list-in-java/#:~:text=ListIterator%20is%20an%20iterator%20is,a%20list%20using%20while%20loop.

good reference

可以用while, for, Iterator, forEach, for String: myList

List operations:
https://docs.oracle.com/javase/8/docs/api/java/util/List.html

https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html

## Integer vs int

https://stackoverflow.com/questions/22777568/why-int-cant-be-compared-to-null-but-integer-can-be-compared-to-null


## Java实例类嵌套List的例子

https://blog.csdn.net/mws666/article/details/104028381

嵌套类已经掌握。

https://blog.csdn.net/qq_36098284/article/details/79936335

一次性传递多个list。

查看test4：list<list<String>>的初始化

## Java switch statement

https://www.geeksforgeeks.org/switch-statement-in-java/

## double to int

int x = (int) 4.97542;

https://stackoverflow.com/questions/10280520/convert-double-to-int-rounded-down

## String Comparison returning false while they have same value

https://stackoverflow.com/questions/56352667/string-comparison-returning-false-while-they-have-same-value

```java
s1.equals(s2)
```

## Java 8 date add n seconds to current date example program

http://www.instanceofjava.com/2018/02/java-8-date-add-seconds-example.html

Java 8 providing java.time.LocalDateTime class.
By using plusSeconds() method of  LocalDateTime we can add seconds to date.
By Using minusSeconds() method we can substract  seconds from java date.

```java
public class addSecondsToDate {

 public static void main(String[] args) {
  
  //create data using java 8 LocalDateTime 
  LocalDateTime datetime= LocalDateTime.now();
  
  System.out.println("Before: "+datetime);
  //add seconds by using plusSeconds(seconds) method
  datetime=datetime.plusSeconds(12);
  System.out.println("After: "+datetime);
 }
```

### another method

https://stackoverflow.com/questions/1655357/how-do-i-say-5-seconds-from-now-in-java

```java
now.setTime(now.getTime() + 5000);

DateTime later = DateTime.now().plusSeconds( 5 );

new Date( System.currentTimeMillis() + 5000L)
```


## convert date to string

https://stackoverflow.com/questions/2942857/how-to-convert-current-date-into-string-in-java

```java
String date = new SimpleDateFormat("dd-MM-yyyy").format(new Date());

Calendar cal = Calendar.getInstance();
SimpleDateFormat sdf = new SimpleDateFormat(DATE_FORMAT_NOW);
return sdf.format(cal.getTime());
```

## Arraylist operations

https://www.geeksforgeeks.org/arraylist-in-java/

## Iterating through a map

https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/

### Storing and Retrieving ArrayList values from hashmap

https://stackoverflow.com/questions/19541582/storing-and-retrieving-arraylist-values-from-hashmap

Map<ArrayList<>>

### Store Duplicate Keys in a Map in Java

https://www.baeldung.com/java-map-duplicate-keys

## convert a Timestamp into either Date or DateTime object

https://stackoverflow.com/questions/7492423/how-can-i-convert-a-timestamp-into-either-date-or-datetime-object

## declare HashMap in global and add values into it only for the first time

https://stackoverflow.com/questions/33775273/how-to-declare-hashmap-in-global-and-add-values-into-it-only-for-the-first-time

```java
static final Map<String, String> PRODUCT_LIST;
```

