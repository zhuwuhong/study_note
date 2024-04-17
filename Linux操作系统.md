# Linux操作系统

### 1.LInux操作系统基础

#### 1.1什么是操作系统

>操作系统 Operating System 简称 OS，是软件的一部分，他是硬件基础上的第一层软件，是硬件和其他软件沟通的桥梁。
>
>操作系统会控制其他程序运行，管理系统资源，提供最基本的计算机功能，如管理及配置内存，决定系统资源供需的有限次序等，同时还提供一些基本的服务程序。

#### 1.2什么是Linux

```yacas
Linux系统内核与Linux发行套件的区别
	Linux系统内核指的是由linus Torcalds负责维护，提供硬件抽象层、硬盘及文件系统控制及多任务功能的系统核心程序。
	Linux发行套件系统是我们常说的Linux操作系统，也即是由Linux内核与各种常用软件的集合产品。
======================================================================================
总结 真正的Linux值得是系统内核，而我们常说的Linux指的是“发行版完整的包含一些基础软件的操作系统”。
```

### 2.Linux操作指令

#### 2.1命令格式

```yacas
command parameters (命令 参数)
==========长短参数(长参数前用--表示,短参数使用-表示)==================
单个参数: ls -a(a是英文all的缩写，表示“全部”)
多个参数: ls -al(全部文件 + 列表形式展示)
单个长参数: ls --all
多个长参数: ls --reverse --all
长短混合参数: ls --all -l

==========参数值================================================
短参数: command -p(参数) 10 (例如: ssh root@121.42.11.34 -p 22)
长参数: command --paramters=10(例如: ssh root@121.42.11.34 --port=22)
```

#### 2.2快捷方式

```yacas
1.通过上下方向按键↑↓来调取过往执行过的Linux命令;
2.命令或参数仅需要输入前几位就可以使用Tab键补全;
3.Ctrl + R: 用于查找使用过的命令(history 命令用于列出之前使用过的所有命令,然后输入！命令加上编号就可以直接调用执行该历史命令);
4.Ctrl + L: 清除屏幕所有内容;
5.Ctrl + C: 中止当前正在执行的命令;
6.Ctrl + U: 从光标位置剪切到首行;
7.Ctrl + K: 从光标位置剪切到行尾;
8.Ctrl + W: 剪切光标左侧的一个单词;
9.Ctrl + Y: 粘贴 Ctrl + U/K/W剪切的命令;
10.Ctrl + A: 光标跳到命令行开头;
11.Ctrl + E: 光标跳到命令行的行尾;
12.Ctrl + D: 关闭Shell会话;
```

#### 2.3操作指令

##### 2.3.1查看路径

```yacas
查看当前路径
pwd 显示当前所在目录的路径。
查看命令路径
which[which ls] 显示当前命令的可执行文件所在路径(在Linux中每一条命令其实都对应一个可执行程序)。
```

##### 2.3.2浏览和切换目录

```yacas
浏览目录
ls 列出当前所在路径下的文件和目录。
参数 [
    -a 显示所有文件和目录包括隐藏的。
    -l 显示详细列表
    -h 适合人类阅读的
    -t 按文件最近一次修改时间排序
    -i 显示文件的inode(inode是文件内容的标识)
]
切换目录
cd 表示切换目录。
参数[
    -h 适合人类阅读的;
    -a 同时列举出目录下文件的大小信息
    -s 只显示总计大小，不显示具体信息
]
```

##### 2.3.3文件的操作

```yacas
浏览文件
cat 一次性显示文件所有内容,更适合查看小的文件。
[-n 显示行号]

less 分页显示文件内容，更适合查看大的文件。
快捷操作[
    空格键盘: 前进一页;
    b键: 后退一页;
    上下键: 回退或前进一行;
    d键: 前进半页;
    u键: 后退半页;
    q键: 停止读取文件,中止less命令
    =键: 显示当前页面内容是文件中的第几行到第几行以及一些其他关于本页内容的详细信息;
    /键: 进入搜索模式后,按n键跳到一个符合项目,按N键跳到上一个符合项目，同时也可以输入正则表达式进行匹配。
]

head 显示文件的开头几行(默认是10行)
[ -n 指定行数]

tail 显示文件的结尾几行(默认10行)
[
    -n 指定行数
    -f 会每过一秒检查文件是否由更新 也可以跟着-s参数指定时间间隔
]


创建文件或目录
touch 创建一个文件

mkdir 创建一个目录
[ -p 递归的创建目录结构]


文件的复制和移动
cp 拷贝文件和目录
[ -r 递归的拷贝,常用来拷贝一整个目录]、
[cp file file_copy --> file 是目标文件，file_copy 是拷贝出来的文件cp file one --> 把 file 文件拷贝到 one 目录下，并且文件名依然为 filecp file one/file_copy --> 把 file 文件拷贝到 one 目录下，文件名为file_copycp *.txt folder --> 把当前目录下所有 txt 文件拷贝到 folder 目录下复制代码]

mv 移动(重命名)文件或目录,与cp命令用法相似
[mv file one --> 将 file 文件移动到 one 目录下mv new_folder one --> 将 new_folder 文件夹移动到one目录下mv *.txt folder --> 把当前目录下所有 txt 文件移动到 folder 目录下mv file new_file --> file 文件重命名为 new_file复制代码]


删除文件
rm 删除文件和目录
[ 
    -i 向用户确认是否删除
    -f 文件强制删除
    -r 递归删除文件 著名的删除操作 rm -rf
]
[rm new_file  --> 删除 new_file 文件rm f1 f2 f3  --> 同时删除 f1 f2 f3 3个文件]


链接
软链接
ln -s [dir1] [dir2] [创建软链接]（软链接就是创建一个变量指向源文件）
a.软链接文件，无论对哪一个文件进行操作，都会影响另一个文件。
b.当源文件删除或移动或改名后，那么软链接文件会失效，链接文件会变成红色，如果将这个文件的文件名恢复或移动回原来的位置，那么链接就会恢复。
c.当创建软链接文件时，为了避免文件移动后链接失效，源文件要使用绝对链接指定
d.可以对目录做软链接


硬链接(是链接的两个文件共享同样的文件内容，因此inode是一样的，一旦文件1与文件2之间有了硬链接，那么修改任意一个文件，修改的都是同一块内容)
ln file1 file2
a.硬链接只能链接文件
b.硬链接不受路径影响
c.硬链接会保持数据同步
d.硬链接会改变文件属性信息中的连接属性
e.不允许对目录做硬连接
f.目录的文件信息中的连接数表示 当前目录下包含多少子目录
```

##### 2.3.4用户权限

>Linux是一个多用户的操作系统。在Linux中，理论上来说，我们可以创建无数个用户，但是这些用户是被划分到不同的群组里面，但是有一个用户名叫root，是一个十分特殊的用户，它是超级用户，拥有最高权限。

![](C:\Users\朱五红\Desktop\微信图片_20230310142027.jpg)

```yacas
以root身份运行命令
sudo [命令]
[sudo date  --> 当然查看日期是不需要sudo的这里只是演示，sudo 完之后一般还需要输入用户密码的]

添加新用户[需要root权限]
useradd [用户名]
[useradd lion --> 添加一个lion用户，添加完之后在 /home 路径下可以查看]

修改密码[需要root权限]
password [用户名]
[passwd lion --> 修改lion用户的密码]

删除用户[需要root权限]
userdel [用户名]
[userdel lion --> 只会删除用户名，不会从/home中删除对应文件夹
 userdel lion -r --> 会同时删除/home下的对应文件夹]

切换用户[需要root权限]
su [用户名]
[sudo su --> 切换为root用户（exit 命令或 CTRL + D 快捷键都可以使普通用户切换为 root 用户）
    su lion --> 切换为普通用户
    su - --> 切换为root用户]
```

##### 2.3.5群组的管理

>Linux中每个用户都属于一个特定的群组，如果不设置用户的群组，默认创建一个和她的用户名一样的群组，并且把用户划归到这个群组。

```yacas
创建群组(用法和useradd相似)
groupadd [群组名]
[groupadd friends --> 创建一个叫friends的群组]

删除群组
groupdel [群组名]
[groupdel foo --> 删除foo群组]

查找用户所在群组
groups [群组名]
[groups lion --> 查看lion用户所在的群组]

修改用户账户
usermod
[常用参数]
[
   -l 对用户重命名。需要注意的是 /home 中的用户家目录的名字不会改变，需要手动修改。
	-g 修改用户所在的群组，例如 usermod -g friends lion修改 lion 用户的群组为 friends 。
	-G 一次性让用户添加多个群组，例如 usermod -G friends,foo,bar lion 。
	-a -G 会让你离开原先的群组，如果你不想这样做的话，就得再添加 -a 参数，意味着append 追加的意思。
]

用于修改文件的群组
chgrp [群组名] [文件]
[chgrp bar file.text --> 将file.text文件的群组修改为bar]

改变文件的所有者[需要root权限]
chown [用户名]:[群组] [文件名]
[chown lion file.txt --> 把其它用户创建的file.txt转让给lion用户chown lion:bar file.txt --> 把file.txt的用户改为lion，群组改为bar]
[常用参数]
[-R 递归设置子目录和子文件， chown -R lion:lion /home/frank 把 frank 文件夹的用户和群组都改为 lion]
```

##### 2.3.6文件权限管理

>权限学习
>
>`drwxr-xr-x` 表示文件或目录的权限。让我们一起来解读它具体代表么？
>
>- `d` ：表示目录，就是说这是一个目录，普通文件是 `-` ，链接是 `l` 。
>- `r` ：`read` 表示文件可读。
>- `w` ：`write` 表示文件可写，一般有写的权限，就有删除的权限。
>- `x` ：`execute` 表示文件可执行。
>- `-` ：表示没有相应权限。
>
>权限的整体是按用户来划分的，如下图所示：
>
>![图片](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb12HhSLxYibr9w8y4GKAfhTDNHjwSKdibbHRmf7PrjuxDSSGmlJcw3TibY3dxFU9hm783e6bibg3jzpsw/640?wx_fmt=jpeg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)
>
>现在再来理解这句权限 `drwxr-xr-x` 的意思：
>
>- 它是一个文件夹；
>- 它的所有者具有：读、写、执行权限；
>- 它的群组用户具有：读、执行的权限，没有写的权限；
>- 它的其它用户具有：读、执行的权限，没有写的权限。
>
>现在理解了权限，我们使用 `chmod` 来尝试修改权限。`chmod` 它不需要是 `root` 用户才能运行的，只要你是此文件所有者，就可以用 `chmod` 来修改文件的访问权限。
>
>##### 数字分配权限
>
>| 权限 | 数字 |
>| :--- | :--- |
>| r    | 4    |
>| w    | 2    |
>| x    | 1    |

```yacas
修改访问权限
chmod [权限等级] [文件]
[常用参数]
[	R 可以递归地修改文件访问权限，例如 chmod -R 777 /home/lion
	u ：user 的缩写，用户的意思，表示所有者。
	g ：group 的缩写，群组的意思，表示群组用户。
	o ：other 的缩写，其它的意思，表示其它用户。
	a ：all 的缩写，所有的意思，表示所有用户。
	+ ：加号，表示添加权限。
	- ：减号，表示去除权限。
	= ：等于号，表示分配权限。]
[用法数字分配权限]
[chmod 640 hello.c # 分析6 = 4 + 2 + 0 表示所有者具有 rw 权限4 = 4 + 0 + 0 表示群组用户具有 r 权限0 = 0 + 0 + 0 表示其它用户没有权限对应文字权限为：rw- r-- ---]
[字母分配权限]
[
    chmod u+rx file -->file的所有者添加读与执行的权限
    chmod g+r file --> file的群组用户添加读的权限
    chmod o-r file --> 其他用户组去除读的权限
]
```

##### 2.3.7查找文件

```yacas
查找文件(文件数据库中查找)
locate [搜索包含关键字的所有文件和目录。后接需要查找的文件名，也可以使用正则表达式。] 
[安装locate]
[yum -y install mlocate --> 安装包updatedb --> 更新数据库
    locate file.txtlocate fil*.txt]
*locate 命令会去文件数据库中查找命令，而不是全磁盘查找，因此刚创建的文件并不会更新到数据库中，所以无法被查找到，可以执行 updatedb 命令去更新数据库。*

find (实际硬盘进行查找)
[find <何处> <何物> <做什么>复制代码]
[
    何处：指定在哪个目录查找，此目录的所有子目录也会被查找。
	何物：查找什么，可以根据文件的名字来查找，也可以根据其大小来查找，还可以根据其最近访问时间来查找。
	做什么：找到文件后，可以进行后续处理，如果不指定这个参数， find 命令只会显示找到的文件。
]
例
根据文件名查找
[
find -name "file.txt" --> 当前目录以及子目录下通过名称查找文件
find . -name "syslog" --> 当前目录以及子目录下通过名称查找文件
find / -name "syslog" --> 整个硬盘下查找syslog
find /var/log -name "syslog" --> 在指定的目录/var/log下查找syslog文件
find /var/log -name "syslog*" --> 查找syslog1、syslog2 ... 等文件，通配符表示所有
find /var/log -name "*syslog*" --> 查找包含syslog的文件
]
根据文件大小查找
[
find /var -size +10M --> /var 目录下查找文件大小超过 10M 的文件
find /var -size -50k --> /var 目录下查找文件大小小于 50k 的文件
find /var -size +1G --> /var 目录下查找文件大小超过过 1G 的文件
find /var -size 1M --> /var 目录下查找文件大小等于 1M
]
根据文件最近访问时间查找
[
find -name "*.txt" -atime -7  --> 近 7天内访问过的.txt结尾的文件复制代码
]
仅查找目录或文件
[
find . -name "file" -type f  --> 只查找当前目录下的file文件
find . -name "file" -type d  --> 只查找当前目录下的file目录
]
操作查找结果
[
find -name "*.txt" -printf "%p - %u\n" --> 找出所有后缀为txt的文件，并按照 %p - %u\n 格式打印，其中%p=文件名，%u=文件所有者
find -name "*.jpg" -delete --> 删除当前目录以及子目录下所有.jpg为后缀的文件，不会有删除提示，因此要慎用
find -name "*.c" -exec chmod 600 {} \; --> 对每个.c结尾的文件，都进行 -exec 参数指定的操作，{} 会被查找到的文件替代，\; 是必须的结尾
find -name "*.c" -ok chmod 600 {} \; --> 和上面的功能一直，会多一个确认提示
]
```

##### 2.3.8软件仓库

>`Linux` 下软件是以包的形式存在，一个软件包其实就是软件的所有文件的压缩包，是二进制的形式，包含了安装软件的所有指令。`Red Hat` 家族的软件包后缀名一般为 `.rpm` ，`Debian` 家族的软件包后缀是 `.deb` 。
>
>`Linux` 的包都存在一个仓库，叫做软件仓库，它可以使用 `yum` 来管理软件包， `yum` 是 `CentOS` 中默认的包管理工具，适用于 `Red Hat` 一族。可以理解成 `Node.js` 的 `npm` 。

```yacas
yum常用命令
yum update | yum upgrade 更新软件包
yum search xxx 搜索相应的软件包
yum install xxx 安装软件包
yum remove xxx 删除软件包
```

##### 2.3.9文本操作

```yacas
文件内容查找
grep(在文件中查找关键字，并显示关键字所在行。)
[常用参数]
[
-i 忽略大小写， grep -i path /etc/profile
-n 显示行号，grep -n path /etc/profile
-v 只显示搜索文本不在的那些行，grep -v path /etc/profile
-r 递归查找， grep -r hello /etc ，Linux 中还有一个 rgrep 命令，作用相当于 grep -r
]
例[grep -in  path /etc/profile --> 完全匹配path grep -in ^path /etc/profile --> 匹配path开头的字符串grep -in [Pp]ath /etc/profile --> 匹配path或Path复制代码]

文件内容统计
wc(它可以统计单词数目、行数、字符数，字节数等。)
例[wc name.txt # 统计name.txt]
[常用参数]
[-l 只统计行数， wc -l name.txt ；
-w 只统计单词数， wc -w name.txt ；
-c 只统计字节数， wc -c name.txt ；
-m 只统计字符数， wc -m name.txt 。]

文件内容操作
unip(删除文件中的重复内容)
例[uniq name.txt # 去除name.txt重复的行数，并打印到屏幕上uniq name.txt uniq_name.txt # 把去除重复后的文件保存为 uniq_name.txt]
```

#####  2.3.10压缩和打包

```yacas
tar 命令可以将多个文件进行打包或解包
注意：打包时是不会进行压缩文件的
	使用选项是：f 选项一定是在所有选项的最右侧，后面跟的是包名
为了在打包时可以进行压测，tar集成了两个选项，z和j，用来在打包的同时对文件进压缩
z->gzip工具，压缩格式为.gz
j->bzip2工具，压缩格式为.bz2

固定格式：
tar -zcvf xxx.tar.gz 被压缩文件
tar -zxvf xxx.tar.gz -C 指定解压路径

tar -jcvf xxx.tar.bz2 被压缩文件
tar -jxvf xxx.tar.bz2 -C 指定解压路径
```

![image-20230330231825511](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230330231825511.png)
