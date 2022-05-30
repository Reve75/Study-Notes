https://www.baeldung.com/spring-mvc-send-json-parameters#:~:text=Send%20JSON%20Parameter%20in%20GET,parameter%20as%20a%20simple%20string.

The answer is pretty simple! The ObjectMapper class provided by the Jackson library offers a flexible way to convert JSON strings into Java objects.

Now, let's see how to send a JSON parameter via a GET request in Spring MVC. First, we'll need to create another handler method in our controller to handle GET requests:

@GetMapping("/get")
@ResponseBody
public Product getProduct(@RequestParam String product) throws JsonMappingException, JsonProcessingException {
    Product prod = objectMapper.readValue(product, Product.class);
    return prod;
}
As shown above, the readValue() method allows deserializing the JSON parameter product directly into an instance of the Product class.