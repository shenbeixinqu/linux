## Linux

### 文件目录操作

#### ls

常用参数:

```shell
-l : 列出长数据串，包含文件的属性与权限数据等
-a : 列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）
```

实例:

```shell
ls -al /home
```

#### cd

实例:

```shell
cd /
cd /home/Code
```

#### pwd

显示当前路径

#### mkdir

实例:

```shell
# 创建一个空目录
mkdir test
# 递归创建多个目录
mkdir test/test1
# 创建权限为777的目录
mkdir -m 777 test2
# 创建目录显示信息
mkdir -v test3
```

#### rm

实例:

```shell
# 删除文件提示
rm test.txt
# 强制删除
rm -f test.txt
# 递归强制删除
rm -rf test
```

#### rmdir

删除一个或多个子目录项

常用参数:

```shell
-v 显示指令执行过程
-p 递归删除
```

实例:

```shell
# 删除空目录,非空目录无法删除
rmdir test1
# 当子目录被删除后使他成为空目录的话,则顺便一并删除
```

#### mv

移动文件或者将文件改名

常用参数

```shell
-b : 若需覆盖文件,覆盖文件前现行备份
-f : 强制,如果文件已经存在,不会询问直接覆盖
-i : 若目标文件已经存在时,询问是否覆盖
```

实例:

```shell
# 将test.txt重命名为test1.txt
mv test.txt test1.txt
# 移动文件test1.txt 到目录test2
mv test1.txt test2
# 将文件 test1.txt、test2.txt、test3.txt 移动到目录 test3。
mv test1.txt test2.txt test3.txt test3
```

#### cp

将源文件复制到目标文件,或将多个源文件复制到目标目录

常用参数:

```shell
-i 覆盖前询问
-n 不要覆盖已经存在的文件
```

实例:

```shell
# 复制文件 test1.txt 到 test1 目录
cp test1.txt test1 # 若文件存在，会提示是否覆盖。若不存在直接完成复制
# 复制 test1 整个目录到 test2
cp -a test1 test2
```

#### cat

显示文件内容,或者将几个文件连接起来显示,或者从标准输入读取内容并显示,常与重定向符号配合使用

常用参数:

```shell
-n 对输出的所有行进行编号
-E 在每行结束处显示$
-s 有连续两行以上的空白行,就代换为一行的空白行
```

实例:

```shell
cat -n test.log
```

#### nl

nl可以将行号做比较多的显示设计

常用参数:

```shell
-b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)
-b t ：如果有空行，空的那一行不要列出行号(默认值)
-n ln ：行号在萤幕的最左方显示
-n rn ：行号在自己栏位的最右方显示，且不加 0
-n rz ：行号在自己栏位的最右方显示，且加 0
```

实例:

```shell
# 用 nl 列出 test.log 的内容
nl test.log
# 用 nl 列出 test.log 的内容，空本行也加上行号。
nl -b a test.log
```

#### more

查看文件内容,并支持按页,跳行等功能

实例:

```shell
# 查看文件
more /var/log/dmesg
- 空格键  查看下一屏
- 回车键  往下滚动一行
- b键     往前查看一屏
- q键     退出
# 从指定行开始显示
more +50 /var/log/dmesg
# 限制每页显示的行数
more -10 /var/log/dmesg
# 显示操作提示信息
more -10 -d /var/log/dmesg
# 禁止滚动
more -10 -c /var/log/dmesg
## 如果我们一次显示 10 行，按一下空格键，它会往下继续显示 10 行
## 终端里一共显示了 20 行，也就是它会一直往下滚动
```

#### less

查看文件,也可以以分页的方式显示文件内容

```shell
# 查看文件
less /var/log/dmesg
# 显示行号
less -N /var/log/dmesg
命令操作
-  f 向后翻一页
-  b 向前翻一页
-  j 下一行
-  k 上一行
-  gg 调到文本最前面
-  G  调到文本末尾
-  空格键  滚动一页
-  回车键  滚动一行
# 搜索关键字
G 切换到文章的末尾
? (要搜索的字符串)

```

#### head

#### tail

### 文件查找

#### which

查找并显示给定命令的绝对路径

使用which命令,可以看到某个系统命令是否存在,以及执行的到底是哪一个位置的命令

常用参数:

```shell
-n: <文件名长度>：制定文件名长度，指定的长度必须大于或等于所有文件中最长的文件名；
-p: <文件名长度>：与-n参数相同，但此处的<文件名长度>包含了文件的路径；
-w： 指定输出时栏位的宽度；
-V： 显示版本信息。
```

实例:

```shell
which pwd
	/usr/bin/pwd
which adduser
	/usr/sbin/adduser
```

#### whereis

常用参数:

```shell
-b 定位可执行文件
-m 定位帮助文件
-s 定位源代码文件
-u 搜索默认路径下除可执行文件、源代码文件、帮助文件以外的其它文件
-B 指定搜索可执行文件的路径
-M 指定搜索帮助文件的路径
-S 指定搜索源代码文件的路径
```

实例:

```shell
# 将和 svn 文件相关的文件都查找出来。
whereis svn
# 只将二进制文件查找出来。
whereis -b svn
```

#### locate

可以快速搜索档案系统内是否有指定的档案

```shell
# 使用前先进行安装
yum install mlocate
# 更新库
updatedb
```

常用参数:

```shell
-e 将排除在寻找的范围之外
-1 如果 是 1．则启动安全模式。在安全模式下，使用者不会看到权限无法看到 的档案。这会始速度减慢，因为 locate 必须至实际的档案系统中取得档案的权限资料。
-f 将特定的档案系统排除在外，例如我们没有道理要把 proc 档案系统中的档案 放在资料库中。
-q 安静模式，不会显示任何错误讯息。
-n 至多显示 n个输出
-r 使用正规运算式 做寻找的条件。
-o 指定资料库存的名称。
-d 指定资料库的路径
-h  显示辅助讯息
```

实例

```shell
# 搜索etc目录下所有以sh开头的文件
locate /etc/sh
```









