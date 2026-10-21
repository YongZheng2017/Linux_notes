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
