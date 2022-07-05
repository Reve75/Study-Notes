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

### Java Program to Convert TimeStamp to Date

https://www.geeksforgeeks.org/java-program-to-convert-timestamp-to-date/

```java
Timestamp ts
            = new Timestamp(System.currentTimeMillis());
 
        // Passing the long value in the Date class
        // constructor
        Date date = new Date(ts.getTime());
```

