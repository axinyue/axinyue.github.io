# Overview
# core

# 注解
### jackson-annotations包中的注解：
```


JsonProperty #字段注解，修改序列化字段
JsonIgnoreProperties #类注解，忽略字段
JsonCreator #修改创建对象的默认方法，默认是无参构造
JsonTypeInfo #设置如何序列化对象
JsonSubTypes  # 
JsonAutoDetect  # 修改序列化字段自动搜索规则
```
### jackson-databind 中的注解：

```
JsonDeserialize #字段注解， 扩展类型
JsonSerialize #字段注解，扩展类型

```



* 参考： https://github.com/FasterXML/jackson-docs