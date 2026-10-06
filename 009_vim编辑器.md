# Vim

## 打开文件

打开单个文件：vim filename.txt

&nbsp;

打开多个文件：

- 水平分屏：vim -o file1 file2
- 垂直分屏：vim -O file1 file2
- 普通多文件：vim file1 file2（依次打开，默认只显示第一个）

&nbsp;

打开文件并跳转到指定行：

- vim filename.txt +10      # 打开并光标定位到第 10 行
- vim filename.txt +         # 打开并定位到最后一行
- vim filename.txt +/keyword # 打开并定位到第一个匹配 keyword 的行

&nbsp;

以只读方式打开：

- vim -R filename.txt       # 只读模式，防止误改
- view filename.txt         # 同上，view 是 vim -R 的别名

&nbsp;

恢复崩溃时的文件：

- vim -r filename.txt       # 恢复因崩溃未保存的文件
