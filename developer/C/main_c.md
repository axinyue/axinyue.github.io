# 使用VsCode开发C/C++
### 一.初始化环境:
通过RemoteSSH连接服务器并安装C++ Extension Pack插件.
1. 指定编译的输出文件添加后缀. 为了使用git管理代码同时忽略编译后的输入,需要指定编译输出路径或输出文件的后缀, 可以修改.vscode目录中的tasks.json和lunch.json. 
- tasks.json 的 -o参数指定后缀或者添加目录
- lunch.json 的program 指定为taskjson中输出路径的同样的路径
- ps.关于g++命令,可以参考g++ --help命令查看相应参数.
```
// tasks.json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: g++ build active file",
            "command": "/usr/bin/g++",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}.o"
            ]
---------


// lunch.json

{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++ - Build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}.o",

----
```
