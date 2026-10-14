## Bash

编译型语言（编译）：c, c++, 有变量类型
    变量：字符、整数、浮点数（单精度、双精度）
脚本型语言（动态）：解释执行，依赖于解释器（bash）
    变量：弱类型，默认识别为字符型，参与运算时自动进行类型转换
    bash, python

&nbsp;

## bash变量

变量类型
a.本地变量（局部变量）
    i.作用范围仅限于当前源程序文件
    ii.仅对当前shell进程有效（子shell中无效）
    iii.不需要声明，直接使用   age=23
b.环境变量
    i.作用范围：当前shell及其子shell
    ii.export VARNAME   若VARNAME是本地变量，则转换为环境变量
    iii.export VARNAME=value    导出环境变量 
    iv.撤销也用 unset
    v.查看所有环境变量  
        1.env
        2.printenv
        3.export
    c.特殊变量

        $?  引用前一个命令的执行状态返回值
    d.位置变量

&nbsp;

声明变量： 
declare  变量名
-i  声明为整型
-a  声明为数组
-r  声明变量为只读变量
-x  声明为环境变量
declare -i age=23 

&nbsp;

引用变量值
${VARNAME}    // 花括号可省略

```
test@123456789:~$ unset animal
test@123456789:~$ echo "There are some ${animal}s"
    There are some s
```


