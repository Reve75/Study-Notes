## Using Jackson to convert jsonstring to obj

https://www.baeldung.com/spring-mvc-send-json-parameters#:~:text=Send%20JSON%20Parameter%20in%20GET,parameter%20as%20a%20simple%20string.

The answer is pretty simple! The ObjectMapper class provided by the Jackson library offers a flexible way to convert JSON strings into Java objects.

Now, let's see how to send a JSON parameter via a GET request in Spring MVC. First, we'll need to create another handler method in our controller to handle GET requests:

```java
@GetMapping("/get")
@ResponseBody
public Product getProduct(@RequestParam String product) throws JsonMappingException, JsonProcessingException {
    Product prod = objectMapper.readValue(product, Product.class);
    return prod;
}
```
As shown above, the readValue() method allows deserializing the JSON parameter product directly into an instance of the Product class.

## Parse Json in java

https://stackoverflow.com/questions/2591098/how-to-parse-json-in-java

The org.json library is easy to use.

Just remember (while casting or using methods like getJSONObject and getJSONArray) that in JSON notation

[ … ] represents an array, so library will parse it to JSONArray
{ … } represents an object, so library will parse it to JSONObject
Example code below:

```java
import org.json.*;

String jsonString = ... ; //assign your JSON String here
JSONObject obj = new JSONObject(jsonString);
String pageName = obj.getJSONObject("pageInfo").getString("pageName");

JSONArray arr = obj.getJSONArray("posts"); // notice that `"posts": [...]`
for (int i = 0; i < arr.length(); i++)
{
    String post_id = arr.getJSONObject(i).getString("post_id");
    ......
}
```

This is a good reference.

## Extract data from json string with or without JSONObject

https://stackoverflow.com/questions/54699820/extract-data-from-json-string-with-or-without-jsonobject

```java
final JSONObject jsonObject = new JSONObject(str);
final JSONArray posts = jsonObject.getJSONArray("posts");
final Collection<String> values = new ArrayList<>(posts.length());

for (int i = 0; i < posts.length(); i++) {
    final JSONObject post = posts.getJSONObject(i);
    values.add(post.getString("value"));
}

```

## JSONObject ClassNotFoundException

https://stackoverflow.com/questions/15951032/jsonobject-classnotfoundexception

## convert String to JSON object in Java

https://www.java67.com/2016/10/3-ways-to-convert-string-to-json-object-in-java.html

String to JSON Object using Gson

```java
Gson g = new Gson();
Player p = g.fromJson(jsonString, Player.class)
```

## Returning JSON object as response in Spring Boot

https://stackoverflow.com/questions/44839753/returning-json-object-as-response-in-spring-boot

As you are using Spring Boot web, Jackson dependency is implicit and we do not have to define explicitly. You can check for Jackson dependency in your pom.xml in the dependency hierarchy tab if using eclipse.

And as you have annotated with @RestController there is no need to do explicit json conversion. Just return a POJO and jackson serializer will take care of converting to json. It is equivalent to using @ResponseBody when used with @Controller. Rather than placing @ResponseBody on every controller method we place @RestController instead of vanilla @Controller and @ResponseBody by default is applied on all resources in that controller.
Refer this link: https://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html#mvc-ann-responsebody

The problem you are facing is because the returned object(JSONObject) does not have getter for certain properties. And your intention is not to serialize this JSONObject but instead to serialize a POJO. So just return the POJO.
Refer this link: https://stackoverflow.com/a/35822500/5039001

If you want to return a json serialized string then just return the string. Spring will use StringHttpMessageConverter instead of JSON converter in this case.

## Gson – Parsing JSON Array to Java Array or List

https://howtodoinjava.com/gson/gson-parse-json-array/

```java
ArrayItem[] userArray = new Gson().fromJson(jsonSource, ArrayItem[].class); 
```

For converting such JSON array to a List, we need to use TypeToken class.

```java
Type listType = new TypeToken<ArrayList<ArrayItem>>(){}.getType();
 
ArrayList<ArrayItem> list = gson.fromJson(jsonSource, listType);  
```

**Converting JSON Array to Array of Objects**

```java
String userJson = "[{'name': 'Alex','id': 1}, "
				+ "{'name': 'Brian','id':2}, "
				+ "{'name': 'Charles','id': 3}]";

Gson gson = new Gson(); 

User[] userArray = gson.fromJson(userJson, User[].class);  

for(User user : userArray) {
	System.out.println(user);
}
```

**Converting JSON Array to List of Objects**

```java
String userJson = "[{'name': 'Alex','id': 1}, "
        + "{'name': 'Brian','id':2}, "
        + "{'name': 'Charles','id': 3}]";
     
Gson gson = new Gson(); 
 
Type userListType = new TypeToken<ArrayList<User>>(){}.getType();
 
ArrayList<User> userArray = gson.fromJson(userJson, userListType);  
 
for(User user : userArray) {
  System.out.println(user);
}
```

### Gson — Mapping of Arrays and Lists of Objects

https://futurestud.io/tutorials/gson-mapping-of-arrays-and-lists-of-objects

Comprehensive. includes lists and lists of lists and getting type of lists.

## Convert JSON object to Java object using Gson library in Jav

https://www.tutorialspoint.com/convert-json-object-to-java-object-using-gson-library-in-java#:~:text=A%20Gson%20is%20a%20json,JSON%20object%20to%20Java%20Object.

## Gson – How to convert Java object to / from JSON

https://mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/

comprehensive

## HTTP POST using JSON in Java

https://stackoverflow.com/questions/7181534/http-post-using-json-in-java

不错的httpclient例子

## JAVA中实现API对接时POST请求

https://bbs.huaweicloud.com/blogs/320456

## Gson: Directly convert String to JsonObject (no POJO)

https://stackoverflow.com/questions/4110664/gson-directly-convert-string-to-jsonobject-no-pojo

好像是用的另一个stackoverflow答案的方法

## 使用Gson将Java对象转换为JSON

https://blog.csdn.net/wuseyukui/article/details/13775449

https://vinxikk.github.io/2017/10/02/java/gson-1/#Gson%E4%BD%BF%E7%94%A8

不错

### Gson – How to convert Java object to / from JSON

https://mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/

### Gson：直接将String转换为JsonObject（无POJO）

https://java-askforanswer-com.translate.goog/gsonzhijiejiangstringzhuanhuanweijsonobjectwupojo.html?_x_tr_sch=http&_x_tr_sl=zh-CN&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=sc

### Convert JSON to a Map Using Gson

https://www.baeldung.com/gson-json-to-map

https://stackoverflow.com/questions/2779251/how-can-i-convert-json-to-a-hashmap-using-gson

```java
import java.lang.reflect.Type;
import com.google.gson.reflect.TypeToken;

Type type = new TypeToken<Map<String, String>>(){}.getType();
Map<String, String> myMap = gson.fromJson("{'k1':'apple','k2':'orange'}", type);

```

```java
Gson gson = new Gson(); 
String json = "{\"k1\":\"v1\",\"k2\":\"v2\"}";
Map<String,Object> map = new HashMap<String,Object>();
map = (Map<String,Object>) gson.fromJson(json, map.getClass());
```

## HttpClient 的 PoolingHttpClientConnectionManager

https://blog.51cto.com/u_1472521/5117888

## Java HttpClient Post多层json格式参数

https://blog.csdn.net/liubo1991_java/article/details/51360361

## Http框架封装

https://jxiaow.gitee.io/posts/84a009ed/

没仔细看

## gson无法正常将时间戳转化成date

https://blog.csdn.net/Booleaning/article/details/88343464

参考了这个链接,按照以下方法写的

```java
		@Test
    public void fun1(){

        GsonBuilder builder = new GsonBuilder();

        // Register an adapter to manage the date types as long values
        builder.registerTypeAdapter(Date.class, new JsonDeserializer<Date>() {
            public Date deserialize(JsonElement json, Type typeOfT, JsonDeserializationContext context) throws JsonParseException {
                return new Date(json.getAsJsonPrimitive().getAsLong());
            }
        });

        Gson gson = builder.create();


        String str = "{\"name\":\"yjt\",\"date\":\"1552012460277\"}";
        Person person = gson.fromJson(str,Person.class);
        log.info("{}", person);
    }

```

