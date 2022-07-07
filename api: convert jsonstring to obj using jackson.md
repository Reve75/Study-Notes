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

## 

