## Idea+springboot+mybatis+maven搭建web项目

https://blog.csdn.net/qq_39505065/article/details/81568056

## 跟着写完但是localhost 8080 返回404：

https://zhuanlan.zhihu.com/p/160901686

## @responsebody

在templates文件夹下新建index.html，然后通过以下controller定位到index，即可访问。【Controller的return字符串值，若直接返回，则为跳转的URL，若在返回值前加上***@ResponseBody***，则返回字符串】

## mybatis sql 语句

https://blog.csdn.net/linyiwwy/article/details/108688003

useGeneratedKeys 和 keyProperty 需要和insert语句一起用，不可以用在select里面

## Error: Missing URI template variable ” for method parameter of type String。使用@pathVariable

https://www.yawintutor.com/missing-uri-template-variable-for-method-parameter-of-type-string/

## 关于正确使用pathVariable和RequestParam

https://syntaxfix.com/question/12445/spring-mvc-missing-uri-template-variable

If the path variable name in the @RequestMapping annotation is different from the @PathVariable annotation, change the path variable name in the @RequestMapping annotation. The name in the @ReqeustMapping annotation should be the same as the name in the @PathVariable annotation.

@PathVariable is used to tell Spring that part of the URI path is a value you want passed to your method. Is this what you want, or are the variables supposed to be form data posted to the URI?

If you want form data, use @RequestParam instead of @PathVariable.

If you want @PathVariable, you need to specify placeholders in the @RequestMapping entry to tell Spring where the path variables fit in the URI. For example, if you want to extract a path variable called contentId, you would use:

@RequestMapping(value = "/whatever/{contentId}", method = RequestMethod.POST)

Edit: Additionally, if your path variable could contain a '.' and you want that part of the data, then you will need to tell Spring to grab everything, not just the stuff before the '.':

@RequestMapping(value = "/whatever/{contentId:.*}", method = RequestMethod.POST)

This is because the default behaviour of Spring is to treat that part of the URL as if it is a file extension, and excludes it from variable extraction.

## Spring MVC Missing URI template variable @pathVariable和@requestParam的差别

https://stackoverflow.com/questions/19803117/spring-mvc-missing-uri-template-variable

@PathVariable is used to tell Spring that part of the URI path is a value you want passed to your method. Is this what you want, or are the variables supposed to be form data posted to the URI?

If you want form data, use @RequestParam instead of @PathVariable.

If you want @PathVariable, you need to specify placeholders in the @RequestMapping entry to tell Spring where the path variables fit in the URI. For example, if you want to extract a path variable called contentId, you would use:

@RequestMapping(value = "/whatever/{contentId}", method = RequestMethod.POST)

## use Integer instead of int, Long instead of long

https://stackoverflow.com/questions/23977629/optional-long-parameter-is-present-but-cannot-be-translated-into-a-null-value

https://stackoverflow.com/questions/55861726/optional-int-parameter-is-present-but-cannot-be-translated-into-a-null-value

you can't declare a primitive to be null,
for example: private int myNumber = null; will not compile. So instead of using long use Long and you should be good to go.

通常是因为没有在arg里面用@RequestParam或者@pathVariable, 导致

## thymeleaf

https://developer.aliyun.com/article/769977

介绍

https://blog.51cto.com/u_9177933/3053625

配置

https://blog.csdn.net/qq_33790251/article/details/84108158

版本问题

https://www.programminghunter.com/article/75891177257/

路径

https://blog.csdn.net/qq_35869079/article/details/96244619

动态静态页面

http://www.4k8k.xyz/article/ITxiaofeixiang/107352880

配置路径

https://www.bbsmax.com/A/pRdBePeG5n/

配置

https://blog.51cto.com/u_15077556/3572123

配置



## springboot访问static 404

https://cloud.tencent.com/developer/article/1657234

## Unable to resolve table '表名'

https://blog.csdn.net/Eiji_g/article/details/90292312

用data sources 解决找不到数据库问题

