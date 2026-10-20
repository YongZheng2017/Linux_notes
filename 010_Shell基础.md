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

&nbsp;

撤销变量
unset 变量名    // 不要加$

```
test@123456789:~$ unset animal
test@123456789:~$ echo "There are some ${animal}s"
    There are some s
```

&nbsp;

只读变量（常量）
readonly VARNAME    // 不可撤销

```
test@123456789:~$ readonly animal="pig"
test@123456789:~$ echo "There are some ${animal}s"
    There are some pigs
test@123456789:~$ unset animal
-bash: unset: animal: cannot unset: readonly variable
```

&nbsp;

变量名：
只能包含数字、字母、下划线
环境变量都是大写
本地变量不建议用大写，且不要与环境变量同名

&nbsp;

变量赋值给变量
A=30
Age = "$A"

echo $Age    // 30

&nbsp;

若a有值，则赋值为a；若a无值，在赋值为40 （冒号可省略）

```
test@123456789:~$ age=${a:-40}
test@123456789:~$ echo $age
    40
```

&nbsp;

## 返回值

- 程序自身执行的返回值

- 程序执行状态返回值    
  0：成功
  1~255：失败 （1,2,127 系统留用）

&nbsp;

## 引号

单引号：强引用 直接替换 echo ‘$AGE’ // 显示 $AGE

双引号：弱引用 变量会替换 echo "$AGE" // 显示AGE变量的值

反引号：· 命令替换

&nbsp;

## 子shell

在一个shell进程中再打开一个shell

&nbsp;

## 命令替换

用命令的执行结果替换命令

1. 反引号

2. $()

```
test@123456789:~$ echo "today is `date +%F`"
    today is 2026-07-21
test@123456789:~$ echo "today is $(date +%F)"
    today is 2026-07-21

touch file_`date +%F-%H-%M-%S`
```

&nbsp;

## seq

生成序列数

Usage: seq [OPTION]... LAST

or: seq [OPTION]... FIRST LAST

or: seq [OPTION]... FIRST INCREMENT LAST

Print numbers from FIRST to LAST, in steps of INCREMENT.

seq 5 // 1,2,3,4,5

seq 5 10 // [5~10]

seq 10 2 100 // [10, 100]的偶数

&nbsp;

## shell脚本

命令的堆砌

开头 shebang： #!/bin/bash // 指定用bash执行，魔数，让linux识别文件类型

井号 xxx // 注释行，不会执行

&nbsp;

## 重定向

标准输入：0 stdin

标准输出：1 stdout

标准错误输出：2 stderr

&nbsp;

输出重定向

command > file 覆盖输出

command >> file 追加输出

&nbsp;

输入重定向

tr 'a-z' 'A-Z' < /etc/passwd // 从 /etc/passwd 读入， 小写字母变大写

command << "EOF" // 在脚本中用来生成文档，表示遇到 EOF 结束

```
test@123456789:~$ cat >> test.out << EOF
> The first line
> Thes second line
> The third line
> EOF

test@123456789:~$ cat test.out
The first line
The second line
The third line
test@123456789:~$
```

```
#!/bin/bash
cat << EOF
What do you want to eat?
1, Shaoji
2, Loongxia
3, Dazhaxie
EOF
```

&nbsp;

标准错误输出重定向

command 2> outfile

command 2>> outfile // 追加

&nbsp;

标准输出和错误输出一起重定向

command > outfile 2> &1

command &> outfile // 和上面等价

commande > outfile 2> errfile // 分开重定向

&nbsp;

/dev/null 丢弃的数据 date > /dev/null

/dev/zero 持续吐0的泡泡机

/dev/random 随机数生成器

/dev/urandom 随机数生成器

&nbsp;

set -c：禁止覆盖已存在的普通文件（通过重定向输出时，如 > 和 >>）

set +c：取消这个禁止覆盖的限制，允许重定向覆盖已存在的文件

command >| file // 强制覆盖

&nbsp;

## 管道

前一个命令的输出 当做 第二个命令的输入

只传递标准输出

command1 | command2 | command3

&nbsp;

有些场景不适用管道： file `ls /var/log`

file ls /var/log | cut -d: -f2 | tr -d ' ' // 用file取每个文件的文件类型； 按冒号分隔，取第2个字段； 删除空白字符

file `ls /var/log` | cut -d: -f2 | tr -d ' ' | sort | uniq // 再排序； 再去重

&nbsp;

## T命令

tee  一个输入，2个输出
command1 | tee file | command2      // 先输出到file, 再输出到command2
ls /etc | tee test1.out | tr 'a-z' 'A-Z'    // 先输出到 test1.out  再转换为大小并输出到屏幕
