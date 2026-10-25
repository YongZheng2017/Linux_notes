## bash算术运算

+， -， *， /， %

++，--

&nbsp;

## 算术运算表达式

declare -i sum=2+3

&nbsp;

let 表达式

let sum=2+3

&nbsp;

expr 表达式

sum=`expr 2 + 3` // +两边要有空格

echo "The sum of 2+3 is `expr 2 + 3`"

$[expression] 算术运算表达式

$((expression))

```
test@123456789:~$ a=4
test@123456789:~$ let a++
test@123456789:~$ echo $a
    5
```

```
test@123456789:~$ c=$[3+4]
test@123456789:~$ echo $c
    7
```

```
test@123456789:~$ d=$((4+5))
test@123456789:~$ echo $d
    9
```

&nbsp;

bash只支持整数运算，会取整（省略小数）

&nbsp;

浮点运算：

bc

bc - An arbitrary precision calculator language

scale=需要精确到的小数位数

echo 'scale=3;3/2' | bc

```
test@123456789:~$ echo 'scale=3;3/2' | bc
    1.500
```

计算当前时间到1970.1.1的天数：

```
test@123456789:~$ days=$[$(date +%s)/24/60/60]
test@123456789:~$ echo $days
    20657

test@123456789:~$ echo "scale=2;$(date +%s)/24/60/60" | bc
    20657.37
```

&nbsp;

## 赋值

=

a++

a--

sum+=1 // +=, -=, *=, /=, %=

&nbsp;

## 逻辑运算

按位逻辑运算

a&b

逻辑关系运算（短路计算，当从第一个参数就能判断结果时，就不计算第2个参数了）

&& 与

|| 或

！ 取反

&nbsp;

## 比较运算

整数比较

-eq 等于

-ne 不等于

-gt >

-lt <

-ge >=

-le <=

&nbsp;

测试表达式

test expression

[ expression ]

[[ expression ]]

test 2 -eq 3

&nbsp;

字符串比较

== 等于

!=, <> 不等于

\> 大于， 其他一样，前面需要用反斜杠

-n "$A" 测试是否存在字符

-z "$A" 测试是否不存在任何字符（为空）

string1 == string2

test "abc" == "abc"

&nbsp;

文件测试

test -e path // 测试文件是否存在

test -f path // 是否一个普通文件

test -d path // 是否一个目录

test -l path // 是否一个链接

test r/w/x path // 是否有读/写/执行权限
