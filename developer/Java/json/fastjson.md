# 简述
一个简单易用的json包：alibaba fastjson。

# core class
```
JSON, 通过toJSONString,parseObject序列化和反序列化。

JSON的子类： JSONArray,JSONObject 对一组对象进行序列化。

注解：JSONField 控制序列化字段，是否序列化。

需要注意的是： 
1. 序列化是通过get，set方法赋值的，所以序列化字段必须要提供该方法。
2. 序列化对象必须有无参构造方法。
```