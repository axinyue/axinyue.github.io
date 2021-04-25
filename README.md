# Tips
https://axinyue.github.io 将会始终停留在旧版本，原因是使用了ruby语法导致jekyll无法解析。优先md文档

# Bugs
1. jekyll 中会解析 code block.导致无法显示部分代码块，
给出的解决方法是添加 {% raw %} 包裹ruby语法避免解析。 但是会影响直接查阅md的浏览体验，TODO 可通过修改jekyll自己上传web到github并提供html入口。修改jekyll不解析 code block, 如需使用code block需要使用特定标签包裹。
```
# error e.g.  
# i wang to print source code: {{ a }}, but ruby will parse to a varible.
{{ a }}

# fix to 
{% parse_ruby %}
# some need parse ruby block.
{{ end_parse_ruby }}

```