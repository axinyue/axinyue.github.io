## Heap dump
查询java pid,注意不同于linux PID
jmap 命令用于堆分析

```
# 获取java pid
jps -l

#dump一个堆文件
jmap -dump:format=b,file=dump_file.bin 
```

## 使用visualVM分析dump file
```
1. 打开VisualVM
2. 选择File->Load 加载dump_file 
```

## 在visualVM中使用OQL分析
通过OQL脚本进行查询，过滤分析。

```
#在OQL Console窗口编写一个简单的脚本，获取String的实例
select s from java.lang.String s

# 指定instanceof 关键字可以获取子类
select s from instanceof java.lang.String s

# 获取filed,显示String中的属性
select s.value from java.lang.String s

# where
select s.size from java.util.HashMap s where s.size>0

# 获取多个value
select {name: s, size: s.size} from java.util.HashMap s where s.size>0

# 使用内置函数
select count(s) from java.lang.String s


select count(unique(map(heap.objects('java.lang.String'), 'it.value')))

```

* [monitoring tools](https://docs.oracle.com/javase/9/tools/monitoring-tools-and-commands.htm#JSWOR732)
* [trouble-shooting tools](https://docs.oracle.com/javase/9/tools/troubleshooting-tools-and-commands.htm#JSWOR742)

*[VisualVM OQL](https://htmlpreview.github.io/?https://raw.githubusercontent.com/visualvm/visualvm.java.net.backup/master/www/oqlhelp.html)