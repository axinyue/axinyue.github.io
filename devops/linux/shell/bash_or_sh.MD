# bash or sh
bash会向下兼容sh,但是两者语法还是有些差异的.
1. bash 声明
```
#!/bin/bash
```
2. sh
```
#!/bin/sh
```

# basic
```
# define variables

NAME="ax"
AGE=18

# use variables
echo "$NAME"
echo $AGE
echo "$NAME-$AGE"

# arguments 
$0, current scripts
$1, first arguments
...
$n

# use arguments in command line.
hello.sh [arg1] [arg2] [arg..]

# use argements in shell
NAME=$1
AGE=$2
echo "$NAME-$AGE"

# Decision Making

if [ condition ];then
    command...
fi

# if e.g.
if [ "$NAME"="ax" ];then
    echo "good boy"
elif [ $"NAME"="someone" ];then
    echo "$NAME good boy"
else
    echo "$NAME good boy"
fi

# if compare number
-lt <
-gt >
-le <=
-ge >=
-eq =
-ne !=

# if compare string
"$a" = "b", equal 
"$a" == "b", equal
"$a" != "$b"
-z "$a", $a is empty

# if compare number e.g.
if [ $AGE -lt 18 ];then
    echo "young man"
else
    echo "grown-man"
fi




```

see more: 
* https://www.learnshell.org/