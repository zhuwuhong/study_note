# Python的容器

### python中文文档:

- 官方文档：https://docs.python.org/zh-cn/3/
- Python 官方网站：https://www.python.org/
- 博客文章：https://www.cnblogs.com/python/
- 教程：[https://www.runo](https://www.runo/)

### 一、字符串str

##### 1.1字符串的定义

```yacas
定义：（使用单引号，双引号，三引号）引起来的内容，就是字符串
例：
1.使用单引号：str='Hello Word'
2.使用双引号：str="Hello Word"
3.使用三引号：str="""Hello Word"""/'''Hello Word'''、
4.1.定义字符串中本身包含单引号，定义的时候不能使用单引号：
str="I'm 小明"
4.2定义字符串中本身包含双引号，定义的时候不能使用双引号：
str='这是"的用法'
5.转义字符：
\n(换行)		\t(制表符，相当于一个TAB键)		\"(输出一个")		\'(输出一个')
6.原生字符串在字符串前加上r"",字符串中的\就不会进行转义
str=r"I\"小明"
print(str) #I\"小明
```

##### 1.2字符串的下标（索引）

```yacas
1.下标（索引），是数据在容器（字符串，列表，元组）中的位置，编号
2.一般来说，使用的是正数下标，且从0开始
3.可以使用索引（下标）来获取具体位置的数据（可以是单个，也可以是多个位置的数据）
4.python中支持复数下标，-1表示的是最后一个数据
str="abcdefg"
下图为字符串的下标（索引）图
```

![OMVEW}RB7LT@6@U7YYZNZMD](C:\Users\朱五红\Desktop\OMVEW}RB7LT@6@U7YYZNZMD.png)

```yacas
1.打印str中字符"a":
    print(str[0])
    print(str[-7])
2.打印出str中最后一个字符:
    print(str[-1])
    print(str[6])
3.打印出str中下标为3的字符:
    print(str[3])
```

##### 1.3切片

```yacas
1.使用切片操作，可以一次性获取容器中的多个数据（多个数据之间存在一定的规律，数据下标是等差数列）
2.语法 容器[start:end:step]
	2.1 start 表示开始的位置
	2.2 end 表示结束的位置下标,但end所对应的下标位置的数据是取不到的
	2.3 step 表示步长，就是相邻两个坐标的差值
start,start+step,start+2*step,.....,end(取不到)

实现：
my_str="abcdefg"    #定义一个容器装下"abcdefg"
#需求：打印出字符串中abc字符
print(my_str[0:3:1])  #abc
#需求:打印出字符串中efg字符
print(my_str[-3::1])
#如果取到最后一个值end可以不写,但是：不可以少
print(my_str[4:])
#需求：打印出aceg,start:0,end:（最后一个可以不写），step:2
print(my_str[0::2])
#反向打印字符串,从末尾开始到开头
print(my_str[::-1])
print(my_str[6:-1:-1])
```

##### 1.4字符串中查找方法find（）

```yacas
1.字符串.find(str)#字符串中是否存在str这样的字符串
返回值（这个代买执行的结果）
	1.如果存在str，返回第一次出现str位置的下标数
	2.如果不存在str，则返回-1

实现：
my_str="我是Ikun"
str="Ikun"
xb=my_str.find(str)
if xb !=-1:
    print(f"{str}存在{my_str}中，下标为{xb}")
else:
    print(f"{str}不存在{my_str}中")
```

##### 1.5字符串的替换replace()

```yacas
字符串.replace(old,new,count)#将字符串中的old替换为new
-old 元字符中想要替换的字符
-new 替换原字符串中的字符
-count 为替换元字符的次数，如果不写则全部替换
-返回 会返回一个替换后的完整字符串
-注意 原字符串不会改变

实现:
    my_str="我是小聪明,小聪明，小聪明"
print(my_str)
#将小聪明改为小黑子
my_str.replace("小聪明","小黑子")
print(my_str.replace("小聪明","小黑子"))
#将第一个小聪明改为小黑子
my_str.replace("小聪明","小黑子")
print(my_str.replace("小聪明","小黑子",1))
#将最后一个小聪明改为小黑子
d=my_str.replace("小聪明","小黑子")
d=d.replace("小黑子","小聪明",2)
print(d)
#将第二个小聪明改为小黑子
d=my_str.replace("小聪明","小黑子",2)
d=d.replace("小黑子","小聪明",1)
print(d)
```

1.6字符串拆分split()

```yacas
字符串.split(sep)#将字符串按照指定的字符sep进行分隔
-sep 按照sep分隔,可以不写，默认按照空白字符（空格、\t、\n）分割
返回: 返回列表，列表中的每个数据就是分隔后的字符串


实现:
    str="hello Python\tand itcast and\nitheima"
print(str)
#默认按照空白符进行分隔
list=str.split()
print(list)
#按照空格进行分隔
list=str.split(" ")
print(list)
#按照and进行分隔
list=str.split("and")
print(list)
```

##### 1.7字符串的连接join

```yacas
字符串.jonin(容器)#容器一般为列表，将字符串插入列表相邻的两个数据之间，组成新的字符串
注意点:列表中的数据必须都为字符串才可以
实现:
str="Hello"
str1="Word"
srr=str1.join(str)
print(srr)#字符串连接字符串，是将字符串的每个字母看作一个单元进行插入 HWordeWordlWordlWordo
list=['hello','Python','and','itcast','and','itheima']
str=" ".join(list)
print(str)#利用空个将list中的数据组成新的字符串 hello Python and itcast and itheima
str="，".join(list)
print(str)##使用逗号与list进行一个连接  hello，Python，and，itcast，and，itheima
```

### 二、列表list

```yacas
1.列表，list使用[]
2.列表可以存放多个数据
3.列表可以存放多个类型的数据
4.列表中数据之间使用逗号隔开

实现：
#方式一 使用类实例化的方式
#1.1 定义空列表 变量 = list()
lis=list()
print(type(lis),lis)#<class 'list'> []
#1.2 定义非空列表，也成为类型转换list(可迭代类型),本办法覅有是固体部分for循环遍历的就是课迭代类型(例如容器)
#将容器中的每个数据都作为列表中的一个数据进行保存
list1=list("abcd")
print(list1)#['a', 'b', 'c', 'd']

#方式二 直接使用[]进行定义（使用次数较多）
#2.1定义空列表
list2=[]
print(list2)#[]
#2.2定义非空列表
list3=[3.14,'hello',False]
print(list3)#[3.14, 'hello', False]
```

##### 2.1列表的下标（索引）和切片

```yacas
列表的切片 得到的是新的列表
字符串中的切片 的到的是新的字符串 				
							--如果下标不存在则会报错
实现：
list1=[1,3.14,'hello',True]
print(list1)#[1, 3.14, 'hello', True]
#获取列表中的第一个数据
print(list1[0])#1
#获取最后一个数据
print(list1[-1])#True
#获取中间的两个数据
print(list1[1:3])#[3.14, 'hello']
```

##### 2.2列表查询 index()方法

```yacas
index()这个方法的作用和字符串中的find()的作用是一样的
列表中是没有find方法的，只有index()方法
字符串中同时存在find()和index()方法

index()
1.找到返回下标  2.不存在的话直接报错
实现:
list1=[1,3.14,'hello',True]
s=list1.index("str")
print(s)#报错 列表中不存在‘str’ 'str' is not in list
s=list1.index(3.14)
print(s)#返回列表中3.14的下标  1 
```

##### 2.3count()方法

```yacas
列表.count(数据) #统计指定数据在列表中出现的次数
实现:
list=['hello',2,3,4,5]
num=list.count(2)#查询出列表中5出现的次数
print(num)#列表中5出现了1次
num=list.count(20)#查询出列表中20出现的次数
print(num)#列表中20出现了0次
拓展:
#找出list1中2出现的次数已经下标
list1=[1,2,3,2,4,2,6,2,8]
c=list1.count(2)
print(c)
list2=[]
p=0
while True:
    b = list1.index(2)
    list2.append(b)
    list1[b]=" "
    p+=1
    if p < c:
        pass
    else:
        break
print(list2)
for i in list2:
    list1[i]=2
print(list1)
```

##### 2.4添加数据append()

```yacas
列表.append(数据) #向列表的尾部添加数据
#返回None ，所以不用使用变量=列表.append（）
直接向原列表中添加数据，不会残生新的列表，如果想要差看添加后的数据，直接print()打印原来的i二标就好了


实现:
    #向list1列表中添加五个数据
list1=[]
for i in range(5):
    list1.append(i)
print(list1)
```

##### 2.5删除数据pop()

```yacas
列表.pop(index())#根据下标来删除列表中的数据
-index 下标可以不写默认删除列表中最后一个数据
-返回 返回删除后的数据


实现:
#向list1列表中添加五个数据
list1=[]
for i in range(5):
    list1.append(i)
print(list1)#[0,1,2,3,4]
#删除列表中小于2的数据
list2=[]#定义一个空容器存放满足数据的下标
for i in list1:
    if list1[i] < 2:
        list2.append(i)
list2.reverse()#将需要删除的下标进行反转则不会干扰原列表的排序
for i in list2:
    list1.pop(i)
print(list2)#[0,1]
print(list1)#[2,3,4]
```

##### 2.6修改数据

```yacas
想要修改列表中的数据直接使用其下标进行修改即可
列表[下标]=新数据

实现:
#需求更改列表中的2为3
list1=[1,2]
b=list1.index(2)
list1[b]=3
print(list1)
```

##### 2.7列表的反转reverse()

```yacas
字符串反转  字符串[::-1]
列表反转:
1.列表[::-1] 	   得到一个新的列表
2.列表.reverse() 直接对原列表进行修改


实现:
list1=[]
for i in range(10):
    list1.append(i)
print(list1)
b=list1[::-1]
print(b)
list1.reverse()
print(list1)
```

##### 2.8列表排序sort()

```yacas
#前提列表中的数据类型一致
列表.sort() #升序 从小到大的排序，直接对原列表进行排序
列表.sort(reverse=True) #降序，从大到小，直接对原列表进行排序

实现:
#升序
list1=[2,3,5,6,7,8,1,9]
list1.sort()
print(list1)#[1, 2, 3, 5, 6, 7, 8, 9]
#降序
list1.sort(reverse=True)
print(list1)#[9, 8, 7, 6, 5, 3, 2, 1]
```

2.9列表的嵌套

```yacas
列表的嵌套就是值列表中的数据是列表

实现:
list1=[['张三',18,181],['小红',20,171]]
#给每个数据添加性别
for i in list1:
    print(i)
    if i[0] == "张三":
        i.append("男")
    else:
        i.append("女")
print(list1)
#删除每个数据中的性别
for i in list1:
    i.pop()
print(list1)
#输出每个数据中的年龄
for i in list1:
    print(i[1])
```

### 三、元组tuple

```yacas
1.元组typle,使用的是()
2.元组与列表非常相似，都可以存储多个数据且都可以存储任意的数据类型
3.区别是元组中的数据不能修改没列表中的数据可以修改
4.因为元组中的数据不能修改，所以只能使用查询方法，如index()、count()，支持下标与切片
5.元组，主要用于传参与返回值


实现:
#定义空元组(一般不用)
tuple1=tuple()
print(type(tuple1),tuple1)#<class 'tuple'> ()
#类型转换
tuple2=tuple([1,2,3,5])
print(type(tuple2),tuple2)#<class 'tuple'> (1, 2, 3, 5)

#直接使用()创建元组
#创建空元组
tuple3=()
print(tuple3)
#创建非空元组
tuple4=(1,2,3,"Ikun")
print(tuple4)
print(tuple4[-1])
#定义只含有一个元素的元组后一定要在后面加一个逗号
tuple5=(1,)
print(tuple5)
```

##### 3.1应用--交换两个变量的值

```yacas
1.在定义元组的时候，小括号可以不写
2.组包（pack）,将多个数据值组成元组的过程a=1,2 #a=(1,2)
3.拆包（unpack）,将容器中的多个数据分别给到多个变量，需要保证容器中的元素的个数与变量的元素个数保持一致

实现:
a=10
b=20
c=a,b #组包
print(c) #(10,20)

a,b=b,a
print(a,b) # 20,10

x,y,z='abc'
print(y)#b
```

### 四、字典dict



```yacas
1.字典dict,使用{}进行定义
2.字典是由键(key)值(value)对的形式来组成的 key:value
3.一个键值对是一个数据，多个键值对之间使用逗号隔开
4.一个字典中，字典里的见键是不能重复的
5.字典中的键主要是使用字符串类型的，也可以是数字
6.字典中是没有下标的

实现:
#1类实例化
my_dict=dict()
print(type(my_dict),my_dict)#<class 'dict'> {}
#2.1直接使用{}进行定义
my_dict={}
print(type(my_dict),my_dict)#<class 'dict'> {}
#2.2 定义非空字典
my_dict={'name':"小红","age":18,"isMan":True}
print(type(my_dict),my_dict)#<class 'dict'> {'name': '小红', 'age': 18, 'isMan': True}
```

##### 4.1字典的添加与修改

```yacas
字典["键"]=值 (1.键存在修改 2.键不存在则添加)

实现：
my_dict={'name':"小红","age":18,"isMan":True}
#更改字典中的name为王明，年龄为20，
my_dict['name']="王明"
my_dict['age']=20
#在字典里添加一个身高为177
my_dict['height']=177
```

##### 4.2删除字典里的数据

```yacas
1.字典的删除时根据字典的键删除键值对
2.字典.pop('键')

实现:
my_dict={'name':"小红","age":18,"isMan":True}
#删除字典中'isMan'的键值对
my_dict.pop('isMan')
```

##### 4.3字典的查询

```yacas
根据字典里的键获取对应的值
方法1 字典['key'] #不存在则会报错
方法2 字典.get('key') #不存在则返回None

实现:
my_dict={"name":"小明","age":18}
#存在时
print(my_dict["name"])#小明
print(my_dict.get('name'))#小明
#不存在时
print(my_dict["height"])#报错
print(my_dict.get('height'))#返回None
```

##### 4.4字典的遍历

```yacas
字典存在键(key)和值(value),且遍历分为三种情况


1.#遍历字典中的键
my_dict={"name":"小明","age":18}
for i in my_dict/my_dict.keys():
    print(i)
2.#遍历字典中的值
for i in my_dict.values():
    print(i)
3.#遍历字典中的值和键
for i,c in my_dict.items():
    print(i,c)
```

### 5.集合set

```yacas
集合 set{数据,数据,......}
1.集合中数据时不能重复的，即没有重复的数据
2.应用对列表进行去重的操作

实现:
my_list=[1,2,2,2,5,6,9,8,7,10,4]
#方式一(去重排序)
list1=list(set(my_list))
print(list1)
#方式二(去重不排序)
list2=list(set(my_list))
list2.sort(key=my_list.index)
print(list2)
```













































































































