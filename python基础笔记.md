# python基础笔记

```python
lambda 参数 ：参数的操作
```

## 1字符串常用方法

### 1.1 查找 替换 统计

```python
# 查找[参数 str(查找的字符串),start(开始查找的下标)，end(结束查找的下标)]
find() #查找不到规定的字符串时返回-1
rfind() #从右边开始查找，查找不到规定的字符串时返回-1
index() #查找不到规定的字符串时直接报错
rindex() #从右边开始查找，查找不到规定的字符串时直接报错
# 替换[参数 str_1(将被替换的字符串),str_2(将替换成的字符串),num(替换的次数)]
replace() #默认全部替换 
# 统计[str(需要统计出现次数的字符串)]
count() #统计特定字符串在字符串中出现的次数
```

### 1.2分割 连接

```python
# 分割[str(想要删除的字符串)]
split() # 输出的时一个列表[删除该字符串之前的字符串，之后的字符串]
partition() # 输出为元组格式为(删除该字符串之前的字符串，删除的字符串，删除后的字符串)
# 连接 [将想要添加的字符串添加到，被添加的字符串的每一个字符里]
join() # 将特定字符
```

### 1.3判断

```python
startswith() #判断是否以指定字符串开头 
endswith()   #判断是否以指定字符串结束 
isupper()	#判断是不是大写字符	
islower()	#判断是不是小写字符	
isdigit()	#判断是不是数字字符 
isalpha()	#判断是不是字母 
isalnum()	#判断是不是字母或数字字符 
isspace()	#判断是不是空白字符，包含空格，换行符\n，制表符\t (理解)注意''空字符串不是空白字符
```

### 1.4转换

```python
upper() # 转换成大写
lower() # 转换成小写
title() # 将每个单词首字符转换大写
capitalize() # 将第一个单词的首字符转换成大写
```

## 2.列表常用方法

### 2.1判断对象类型

```python
isinstance(obj,type)-->bool
# 如果obj的类型与type一致则返回 True 否则Fasle
```

### 2.2排序

```python
sort(reverse=False) #正序排序
reverse() #逆序排序
sort(key=fuction) #按照特定的要求进行排列
 #例如
    my_list = [{'id':'1','name':'tom','age':'3'},{'id':'2','name':'tom','age':'3'},{'id':'3','name':'tom','age':'3'}]
    my_list.sort(ke=lambda d:d['id'])
```

### 2.3增删改查

```python
# 增加
append() #该函数是在列表末尾添加元素括号内可以是字符串或者数字等
extend() #该函数用于在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表
insert() #该函数用于将制定对象插入列表的指定位置；语法为list.insert(index,obj) index——索引位置 obj——要插入列表中的对象
# 删除
del
1. del 目标  或  del(目标) # 删除列表
2. del 目标[index] # 删除数据
pop
1. 列表序列.pop() # 删除指定下标的数据，如果不指定下标，默认删除最后一个数据，无论是按照下标还是删除最后一个，pop函数都会返回这个被删除的数据
remove
1. 列表序列.remove(数据) # 移除列表中某个数据的第一个匹配项
clear
1. 列表序列.clear() # 清空列表内所有数据
# 修改 通过下标修改
list_1 = [1,2,3]
list_1[0] = 4
print(list_1) # [4,2,3]
# 查询
index() # 查询元素在列表中的下标如果不存在则报错
count() # 查询元素在列表中出现的次数
in # 判断元素是否存在于列表中 如果存在则返回True否则返回False
not in # 判断元素是否不存在于列表中，如果不存在则返回True否则返回Fales
```

## 3.高阶函数

### 3.1map()函数

```python
map() #会根据提供的函数对指定序列做映射
# 第一个参数function以参数序列中的每一个元素调用function函数，返回包含每次function函数返回值的新列表
# 例：（计算列表中 每一个数字的立方）
my_list = [1,2,3,4,5]
def f(num):
    return x**3

result = map(f,my_list)
print(type(result)) # <class 'map'>
print(result) # <map object at 0x0000019AED81BEE0>
print(list(result)) # [1, 8, 27, 64, 125]
```

### 3.2reduce()函数

```python
reduce() #函数会对参数序列中的元素进行顺序导入规定函数中
# 函数将一个数据集合中的所有数据进行下列操作：
# 1.用出给reduce中的函数function(x1,x2)先对集合中的第一第二个元素进行操作
# 2.得到的结果在与第三个数据用function函数进行运算，直到到列表元素中的最后一个
import functools
my_list = [1,2,3,4,5]
def f(num_1,num_2):
    return num_1+num_2
result = functools.reduce(f,my_list)
print(result) # 15
```

### 3.3filter()函数

```python
filter() #函数用于过滤序列中不符合条件的元素，返回一个filter对象，如果要转换为列表可以使用list()进行转换。
# 该函数接收两个参数，第一个为函数，第二个为序列，序列的每一个元素作为参数传递给函数进行判断，如何返回True或False，最后将返回True的元素放到新列表中
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(list(filter(lambda x: x % 2 == 0, my_list))) #[2,4,6,8,10]
```

## 4文件处理

```yacas
4.1 文本形式分类：
	程序文件
		.txt
		.rtf
	二进制形式文件
		音频文件
		视频文件
		图片文件
4.2文件打开模式
	文本方式打开模式
		r -> rt -> read text 以文本方式打开文件读，文件存在即打开成功，文件不存在则打开失败。
		w -> wt -> write text 以文本方式打开文件写，不管文件是否存在都会创建一个新的文件。
		a -> at -> append text 以文本方式打开文件进行内容追加，文件不存在则创建文件，文件存在那么将在文件最后添加内容。
	以二进制形式打开文件模式
		rd 以二进制形式打开文件读取
		wd 以二进制形式打开文件写入
		ad 以二进制形式打开文件追加
```

```yacas
文件操作方法
1.读取方法
 read（） #一次性将整个文件内容读取出来，不适合大型文件读取
 read（size）# 读取指定字节数的文件内容 如果文件最后没有内容了，那么read的返回值就是空字符串
readline() # 每次读取一行文件内容
readlines() #一次性将整个文件内的内容以行的形式读取出来，放到一个列表中
```

```python
# 文件操作模块及其部分功能
import os
rename() # os模块中rename函数可以完成对文件的重命名操作,os.rename(filename,new_filename)
remove() # os模块中的remove函数可以完成对文件的删除操作,os.remove(filename)
mkdir() # os模块中mkdir函数可以创建一个文件夹，os.makdir(dirname)
getcwd() # os模块中getcwd函数可以获取当前的工作目录，os.getcwd()
chdir()  # os模块中chdir函数可以将当前的文件目录转移到指定路径上, os.chdir(newfile_path)
listdir() #os模块中listdir函数，默认获取当前目录下所有的文件，os.listdir(file_path)
rmdir() # os模块中的rmdir函数可以将规定路径下的目录进行删除
```

### 示例

```python
# 实现 在cmd中运行文件时可以精准实现复制
import sys

def copy_file(src, dst):
    file_r = open(src, 'rb')
    file_w = open(dst, 'wb')
    content = file_r.read()
    file_w.write(content)
    print('复制文件成功')


if __name__ == '__main__':
    src = sys.argv[1] #sys.argv实现获取终端输入的字符串内容 根据空格进行分割实现识别
    dst = sys.argv[2]
    copy_file(src=src, dst=dst)
    print(sys.argv)
```

## 5 init文件的作用

```yacas
1.在__init__.py文件中导入模块后，使用from xxx import 该模块后即可直接使用，
__init__.py文件在当前模块使用时自动运行一次，可以实现批量导入等功能
2.在__init__.py文件中可以使用__all___魔法函数，它会影响from - import * 这种导入方式的模块
在all中指定的模块或成员会被导入，没有指定的不会被导入
=======================================================================
举例 我在模块YY中创建了a.py文件 里面存在了一个输出 'Hello pycharm'
	我在模块UU中的__init__.py文件里对YY模块中的a.py实现导入
	那么我就可以在之后使用import导入UU模块实现对a.py里的方法实现调用
```

## 6.异常的处理

![image-20230307023224533](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230307023224533.png)

```yacas
用 class 错误名(Exception) 来自定义一个异常报错
然后使用try ... raise 来实现异常的抛出
		上图我定义了一个ZWHError错误
		当s字符串为'Hello World'时我会出现一个报错 内容为 我不允许你的字符串是Hello World
```

## 7.yield(类return)

```python
# yield类似于return，当在函数中遇到了yield那么将会返回出yield后的那个值，但是下一次调用时，会从yield的下一行开始运行而不是重新开始。
# yield= return+暂停+记住上一次运行的位置
def test():
    for i in range(5):
        yield i
print(test)
```

![image-20230411003331903](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230411003331903.png)

```yacas
yield配合pytest.fixture使用类似于前置与后置条件（方法）；
```

## 8.线程与进程

>进程是最小的资源分配单位，线程是最小的资源调度单位。
>
>- 线程是Python程序中实现多任务的另外一种方式，线程的执行需要CPU的调度来完成。

### 8.1.1python中线程的使用

>注意点：
>
>1.线程之间的执行是无序的
>
>2.主线程会等到所有的子线程执行结束后再结束（可以设置守护线程，主线程结束后子线程不再进行执行，对线程的demon属性进行设置True表示开启
>
>）
>
>3.线程之间共享全局变量（在线程之间可以使用共同的全局变量，但是多线之间对全局变量的使用等操作可能会导致全局变量的错误，也就是在你操作保存前另一个线程就已经开始调用了全局变量）*例如1+1还没等于2的时候就被另一个线程调用了,但是再python3.10时已经解决了这个问题不会出现资源竞争
>
>使用步骤：
>
>1.导入模块 import threading
>
>2.实现多任务的功能函数 执行函数
>
>3.创建线程	threading.Thread(target=函数名，args=数组参数)
>
>4.启动线程 start()方法执行线程

### 8.1.2线程类Thread

Thread([group[,target[,name[,args[,kwagrs]]]]])

- group：线程组
- target：执行的目标任务名
- args：以元组的方式给执行任务传参
- kwargs：以字典的方式给执行任务传参
- name：线程名，一般不设置

实现：

```python
#############################################无传参，有序传参###################################################################
import threading
import time
from Pytest_Demo.Demo_test.loging import Login


# 无参数执行
def task1():
    for i in range(5):
        print(f'我在执行任务1，这是第{i + 1}次')
        time.sleep(1)


def task2():
    for i in range(5):
        print(f'我在执行任务2，这是第{i + 1}次')
        time.sleep(1)


# 有参数执行
def task3(*args):
    username, password = args
    for i in range(5):
        Login_def = Login()
        r = Login_def.login(username, password)
        print("这是任务3的登录结果：" + f"{r}")
        time.sleep(0.5)


def task4(*args):
    username, password = args
    for i in range(5):
        Login_def = Login()
        r = Login_def.login(username, password)
        print("这是任务4的登录结果：" + f"{r}")
        time.sleep(0.5)


if __name__ == '__main__':
    t1 = threading.Thread(target=task1)
    t2 = threading.Thread(target=task2)
    t3 = threading.Thread(target=task3, args=("admin", "123456"))
    t4 = threading.Thread(target=task4, args=("admin", "123456"))
    t1.start()
    t2.start()
    t3.start()
    t4.start()

```

### 8.1.3互斥锁、线程同步

>互斥锁指的是，多个线程去抢用一个公共的资源，先抢到的人先用，没有抢到的人需要等到先抢到的线程释放互斥锁后，其他线程才能再去抢用这个线程。
>
>线程同步值得是，当多个线程可能会多同一个资源进行使用时，对线程进行一个执行顺序的规定，使用 线程1.join()方法对主线程进行阻塞，当线程1执行完成后，才会让主线程继续往下执行。

```python
################################################################解决多线程对公共资源的竞争情况####################################
'''
使用线程互斥锁解决线程间共享全局变量时的资源竞争问题
'''
import threading

num = 0
# 创建锁对象
lock = threading.Lock()


def add_num():
    global num
    global lock
    # 上锁
    lock.acquire()
    for i in range(1000000):
        num += 1
    # 使用完资源后解锁
    lock.release()
    name = threading.current_thread().name
    print(f"{name}--{num}")


if __name__ == '__main__':
    t1 = threading.Thread(target=add_num)
    t2 = threading.Thread(target=add_num)
    t1.start()
    t2.start()
################################################################解决多线程对公共资源的竞争情况####################################
'''
使用线程互斥锁解决线程间共享全局变量时的资源竞争问题
'''
import threading

num = 0


def add_num():
    global num
    global lock
    for i in range(1000000):
        num += 1
    name = threading.current_thread().name
    print(f"{name}--{num}")


if __name__ == '__main__':
    t1 = threading.Thread(target=add_num)
    t2 = threading.Thread(target=add_num)
    t1.start()
    t1.join()
    t2.start()
```

### 8.1.4死锁

>死锁指的是，当多个线程中的某一个线程对公共资源进行互斥锁上锁后，未按照需求进行解锁导致后续线程无法进行的情况。
>
>一般情况有：①上锁后调用出现异常弹出未解锁 ②多个资源多个锁，多个线程需要集齐所有资源进行运作，在运行是可能若干个程序都拿到了一部分的资源，导致资源等待造成死锁的情况
### 8.2.1python中进程的使用

>使用步骤：
>
>1.导入模块 import multiprocessing
>
>2.实现多任务的功能函数 执行函数
>
>3.创建进程 multiprocessing.Process(target=执行函数名)
>
>4.启动进程 start()方法执行进程
>
>注意事项：
>
>1.进程之间不共享全局变量
>
>2.主线程会等所有的子进程执行结束后再结束 

```python
“”“
多进程的使用
”“”
import multiprocessing
import time


def take_1():
    for i in range(100):
        print(f"take1 {i}")
        time.sleep(0.5)

def take_2():
    for i in range(100):
        print(f"take2 {i}")
        time.sleep(0.5)

if __name__ == '__main__':
    m1 = multiprocessing.Process(target=take_1)
    m2 = multiprocessing.Process(target=take_2)
    m1.start()
    m2.start()
```

### 8.2.2获取进程ID

```yacas
os.getpid()获取当前进程的ID
os.getPPid()获取当前进程的父进程ID
也可以在进程运行时打印进程也可以获得进程的ID以及对应父进程ID
```

### 8.3 线程池、进程池

>线程池的基类是 concurrent.futures 模块中的 Executor，Executor 提供了两个子类，即 ThreadPoolExecutor 和 ProcessPoolExecutor，其中 ThreadPoolExecutor 用于创建线程池，而 ProcessPoolExecutor 用于创建进程池。
>
>如果使用线程池/进程池来管理并发编程，那么只要将相应的 task 函数提交给线程池/进程池，剩下的事情就由线程池/进程池来搞定。
>
>Exectuor 提供了如下常用方法：
>
>- submit(fn, *args, **kwargs)：将 fn 函数提交给线程池。*args 代表传给 fn 函数的参数，*kwargs 代表以关键字参数的形式为 fn 函数传入参数。
>- map(func, *iterables, timeout=None, chunksize=1)：该函数类似于全局函数 map(func, *iterables)，只是该函数将会启动多个线程，以异步方式立即对 iterables 执行 map 处理。
>- shutdown(wait=True)：关闭线程池。
>
>程序将 task 函数提交（submit）给线程池后，submit 方法会返回一个 Future 对象，Future 类主要用于获取线程任务函数的返回值。由于线程任务会在新线程中以异步方式执行，因此，线程执行的函数相当于一个“将来完成”的任务，所以 Python 使用 Future 来代表。
>
>Future 提供了如下方法：
>
>- cancel()：取消该 Future 代表的线程任务。如果该任务正在执行，不可取消，则该方法返回 False；否则，程序会取消该任务，并返回 True。
>- cancelled()：返回 Future 代表的线程任务是否被成功取消。
>- running()：如果该 Future 代表的线程任务正在执行、不可被取消，该方法返回 True。
>- done()：如果该 Funture 代表的线程任务被成功取消或执行完成，则该方法返回 True。
>- result(timeout=None)：获取该 Future 代表的线程任务最后返回的结果。如果 Future 代表的线程任务还未完成，该方法将会阻塞当前线程，其中 timeout 参数指定最多阻塞多少秒。
>- exception(timeout=None)：获取该 Future 代表的线程任务所引发的异常。如果该任务成功完成，没有异常，则该方法返回 None。
>- add_done_callback(fn)：为该 Future 代表的线程任务注册一个“回调函数”，当该任务成功完成时，程序会自动触发该 fn 函数。
>
>
>在用完一个线程池后，应该调用该线程池的 shutdown() 方法，该方法将启动线程池的关闭序列。调用 shutdown() 方法后的线程池不再接收新任务，但会将以前所有的已提交任务执行完成。当线程池中的所有任务都执行完成后，该线程池中的所有线程都会死亡。
>
>使用线程池来执行线程任务的步骤如下：
>
>1. 调用 ThreadPoolExecutor 类的构造器创建一个线程池。
>2. 定义一个普通函数作为线程任务。
>3. 调用 ThreadPoolExecutor 对象的 submit() 方法来提交线程任务。
>4. 当不想提交任何任务时，调用 ThreadPoolExecutor 对象的 shutdown() 方法来关闭线程池。

### 8.3.1通过线程池实现爬虫

```python
import re
import requests
import threading


def a_get_movie_link(page_num):
    movie_link = list()
    for i in range(1, page_num + 1):
        respon = requests.get(url=HOST + page_index.format(f'{i}'))
        respon.encoding = 'gbk'
        # print(respon.text)
        movie_link += re.findall(r'<a href="(.*)" class="ulink">(.*)</a>', respon.text)
    print(f'共加载{len(movie_link)}部电影')
    movie_link_dict = {key: value for value, key in movie_link}
    movie_number = 1
    for movie_name, url in movie_link_dict.items():
        respon = requests.get(url=HOST + url)
        respon.encoding = 'gbk'
        xz_url = re.search(r'<a href="(.*)" target="_blank"  title="qBittorrent">点击下载</a>', respon.text).group(1)
        movie_link_dict[movie_name] = xz_url
        print(f'{movie_name} - 电影下载路径为:{xz_url}')
        movie_number += 1
    return movie_link_dict


def get_movie_link(page_num):
    movie_link = list()
    for i in range(1, page_num + 1):
        respon = requests.get(url=HOST + page_index.format(f'{i}'))
        respon.encoding = 'gbk'
        movie_link += re.findall(r'<a href="(.*)" class="ulink">(.*)</a>', respon.text)
    print(f'共加载{len(movie_link)}部电影')
    return movie_link


def get_movie_xz_link(movie_xx):
    # movie_xx = get_movie_link(page_nuber)
    # lock.acquire()
    respon = requests.get(url=HOST + movie_xx[0])
    respon.encoding = 'gbk'
    try:
        xz_url = re.search(r'<a href="(.*)" target="_blank"  title="qBittorrent">点击下载</a>', respon.text).group(
            1)
    except Exception as e:
        xz_url = '未找到'
    # movie_link_dict[movie_xx[1]] = xz_url
    # lock.release()
    name = threading.current_thread().name
    # print(f'{movie_xx[1]} - 电影下载路径为:{xz_url} ---[{name}--{num}]')
    return movie_xx[1], xz_url


# 回调函数
def print_xx(t):
    name, host = t.result()
    global movie_xz_xx
    movie_xz_xx = f'《{name}》 电影下载的路径为:{host}'
    print(movie_xz_xx)


if __name__ == '__main__':
    from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor
    import math
    import time

    # 主页
    HOST = 'https://www.ygdy8.net'
    page_index = '/html/gndy/dyzz/list_23_{}.html'
    movie_xx = get_movie_link(1)
    start = time.time()
    # t.time 6 p.time 5
    #  submit方法
    with ProcessPoolExecutor(max_workers=5) as excutor:
        result_list = [excutor.submit(get_movie_xz_link, i) for i in movie_xx]
        print(type(result_list[0]))
        # # for f in result_list:
        # #     f.add_done_callback(print_xx)
        # movie_link_dict = {i.result()[0]: i.result()[1] for i in result_list}
        # # print(movie_link_dict)
        # number = 1
        # for name, host in movie_link_dict.items():
        #     print(f'{number} - 《{name}》 电影下载的路径为:{host}')
        #     number += 1
        # end = time.time()
        # print(end - start)

    # map方法
    # t.time 4s p.time 5
    # with ThreadPoolExecutor() as e:
    #     movie = e.map(get_movie_xz_link, movie_xx)
    #     print("*" * 20)
    #     movie_link_dict = {key: value for key, value in movie}
    #     number = 1
    #     for name, host in movie_link_dict.items():
    #         print(f'{number} - 《{re.findall(r"《(.*?)》", name)[0]}》 电影下载的路径为:{host}')
    #         number += 1
    #     end = time.time()
    #     print(end - start)

```



### 小结

>- 进程和线程都是完成多任务的一种方式
>- 多进程要比多线程消耗的资源多，但是多进程开发比单进程开发稳定性要强，某个进程挂掉不会影响其他进程。
>- 多进程可以使用cpu的多核运行，多线程可以共享全局变量（"但是要使用互斥锁"）
>- 线程不能单独执行必须依附在进程里 

>​		线程与进程的差别及优缺点
>
>- 进程之间不可以共享全局变量
>- 线程之间共享全局变量，但是要注意资源竞争的问题，互斥锁或者线程同步
>- 创建进程的资源开销比创建线程的资源开销大
>- 进程是对操作系统资源分配的基本单位，线程是CPU调度的基本单位
>- 线程不能够独立执行，必须依存在进程中
>- 多进程开发比单进程开发稳定性强
>
> 优缺点：
>- 进程优缺点：
>- 优点：可以用多核
>- 缺点：资源开销大
>- 线程优缺点
>- 优点：资源开销小
>- 缺点：不能使用多核【GIL锁，Python多线程中，在同一时刻只能有一个线程被执行】
>

## 9.闭包和装饰器

### 9.1闭包的介绍

>在函数嵌套的前提下，内部函数使用了外部函数的变量，并且外部函数返回了内部函数的引用，我们把这个使用外部函数变量的内部函数成为闭包
>
>**构成条件**
>
>- 在函数嵌套(函数里面在定义函数)的前提下
>- 内部函数使用了外部函数的变量(还包括外部函数的参数)
>- 外部函数返回了内部函数的引用

**示例**

```python
# 定义一个外部函数
def func_out(num1):
    # 定义一个内部函数
    def func_inner(num2):
        # 内部函数使用了外部函数的变量(num1)
        result = num1+num2
        print(f"结果是:{result}")
    return func_inner
# 将num1 = 1保存在f中
f = func_out(1)
f(2) # 3
f(3)# 4
```

### 9.2闭包的作用

- 闭包可以保存外部函数内的变量，不会随着外部函数调用完而销毁。

注意点:

- 由于闭包引用了外部函数的变量，则外部函数的变量没有及时释放，导致小号内存

### 9.3闭包的使用

案例

>需求:根据配置信息使用闭包实现不同人的对话信息,例如:
>
>张三:到北京了吗?
>
>李四:已经到了，放心吧!

实现

```python
# 类实现
# 优点：拥有更完善的继承关系
# 缺点：继承耗费资源
class WhoSay(object):
    def __init__(self, name):
        self.name = name
    def say(self,say):
        print(f"{self.name}:{say}")

tom = WhoSay('tom')
tom.say('到哪了老表')
jack = WhoSay('jack')
jack.say('到北京了')

# 闭包实现
# 优点：更加轻量化
# 缺点：继承不够完善
def who(name):
    def say(sqy_str):
        print(f"{name}:{sqy_str}")
    return say
tom = who('tom')
tom('到哪了?')
jack = who('jack')
jack('到北京了啦!')
```

### 9.4闭包内修改外部函数的变量

```python
# 修改外部函数变量
def out():
    n = 2
    def inner():
        nonlocal n
        n = n+10
        print(n)
    print(n) # 2
    return inner

f = out()
f() # 12
f() # 22

# 修改全局变量
n = 1
def out(name):
    def inner():
        global n
        n = n+10
        print(f'name{n}')
    print(f'name{n}')
    return inner

f = out('jack')
f()
f()
```

>LEGB: local enclosure golbal Buindin
>
>在嵌套函数中调用变量现在local(本地函数)中查找>enclosure(外部函数)查找>golbal(全局变量查找)>Buindin(外键环境)查找

### 9.5装饰器

定义

>给已有函数增加额外功能的函数,他本质上就是一个闭包函数

装饰器的功能特点:

>- 不修改已有的函数的源代码
>- 不修改已有的函数的调用方式
>- 给已有函数增加额外的功能

### 9.6装饰器的语法糖写法

>如果有多个函数都需要添加登录验证的功能，每次都需要编写 func=check(func)这样代码对已有函数进行装饰，这种做法还是比较麻烦的。
>
>Python给提供了一个装饰函数更加简单的写法,那就是语法糖，语法糖的书写格式是:@装饰器名字，通过语法糖的方式也可以完成对已有函数的装饰。

**示例**

```python
import time


def count_time(fun):
    def inner():
        start = time.time()
        fun()
        end = time.time()
        print(f'一共用时:{end - start}秒')

    return inner

@count_time
def show():
    n = 0
    for i in range(10000000):
        n += i
    print(f'Show - {n}')

show()
"""
@count_time
show()
-> show(变量) = count_time(show(函数))=将show(函数)的地址传递给count_time函数中并赋值给show变量
-> show(变量) = 可以调用show(函数)的inner方法
因为是闭包的原因,所以inner函数可以调用父函数的参数。
"""
```

执行顺序:

![image-20230508231404134](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230508231404134.png)

### 9.7通用装饰器

```python
def outer(fun):
    def inner(*args,**kwargs):
        print('装饰器语句1')
        rt = fun()
        print('装饰器语句2')
        return rt
    return inner
```

### 9.8多装饰器

>执行顺序:从上至下
>
>装饰顺序:从下至上

示例:

```python
def wrapper_div(fun):
    def inner(*args, **kwargs):
        return f'<div> {fun(*args, **kwargs)} </div>'
    return inner


def wrapper_p(fun):
    def inner(*args, **kwargs):
        return f'<p> {fun(*args, **kwargs)} </p>'
    return inner


@wrapper_div
@wrapper_p
def show():
    return 'Short Life I use Python'


print(show()) # "<div> <p> Short Life I use Python </p> </div>"
"""
@wrapper_div
@wrapper_p
def show()
->
@wrapper_div
show = wrapper_p(show) 
show()
->
show = wrapper_div(wrapper_p(show))
show()
多装饰器从上往下囊括，从下往上进行操作
---------------------执行顺序
->先执行wrapper_div中在fun之前的语句
->再执行fun方法语句 <div>
->然后执行wrapper_p中所有的语句[因为wrapper_p是最后一个装饰器]<div> <p> Short Life I use Python </p>
->再执行wrapper_div中再fun之后的语句 <div> <p> Short Life I use Python </p> </div>
"""
```

### 9.9类装饰器

>装饰器还有一种特殊的用法就是类装饰器，就是通过定义一个类来装饰函数。

```python
class Wrapper():
    def __init__(self,fun):
        self.fun = fun

    def __call__(self, *args, **kwargs):
        print('装饰器内容1...')
        ret = self.fun(*args,**kwargs)
        print('装饰器内容2...')
        return ret
"""
如果使用的是一个类装饰器，那么该装饰器执行完之后，被装饰函数指向的就是该类的实例化对象
如果能让装饰器函数正常执行，那么在该实例化对象的类中实现__call__方法，就相当于闭包格式中的内函数
一旦被装饰函数执行调用，那么就会去执行实例对象中的__call__方法
"""
@Wrapper # Wrapper(show)
def show():
    print('show run ...')
show()
```

### 9.10装饰器传参

>使用带有参数的装饰器，其实就是在装饰器外又报过来一个函数，使用该函数接收参数，返回是展示区，因为@符号需要配合装饰器使用

示例:

```python
def set_args(mes):
    def set_func(func):
        print('装饰器语句1')
        def inner():
            print('装饰器语句2'+ mes)
            func()
        return inner
    return set_func

@set_args('你好呀')
def show():
    print('show run ...')

show()
```

类装饰器传参示例:

```python
class MyDecorator:
    def __init__(self, arg1, arg2):
        self.arg1 = arg1
        self.arg2 = arg2

    def __call__(self, func):
        def wrapper(*args, **kwargs):
            print("Decorator arguments:", self.arg1, self.arg2)
            return func(*args, **kwargs)
        return wrapper
    
@MyDecorator("Hello", "World")
def my_function():
    print("Inside my_function") 
# Decorator arguments: Hello World
# Inside my_function
```

拓展在实现页面的时候同时存入字典:

```python
title_dict = {}


def set_dict(fun):
    def inner():
        title_dict[f'{fun.__name__}.html'] = fun
        fun()

    return inner


@set_dict
def index():
    print('首页')


@set_dict
def my_page():
    print('个人中心')


index()
my_page()
def request_url(url):
    title_dict[url]()
```

### 9.11property

>property在类中定义了一个类属性，这时可以通过这个类属性间接操作 类中的对象属性，可以实现细节德隐藏和简化操作。

类方法实现：

```python
class PropertyTest(object):
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    def get_name(self):
        return self.__name

    def get_age(self):
        return self.__age

    def set_name(self, name):
        if isinstance(name, str):
            self.__name = name

    def set_age(self, age):
        if isinstance(age, int):
            self.__age += age

    username = property(get_name, set_name)
    userage = property(get_age, set_age)


if __name__ == '__main__':
    xm = PropertyTest('小明', 12)
    print(xm.get_name())
    xm.set_name('小红')
    print(xm.get_name())
    print(xm.get_age())
    xm.set_age(12)
    print(xm.get_age())
    xh = PropertyTest('小红', 10)
    print(xh.username)
    xh.username = str('小明')
    print(xh.username)
    print(xh.userage)
    xh.userage = 14
    print(xh.userage)
```

装饰器实现：

```python
class PropertyTest(object):
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, name):
        if isinstance(name, str):
            self.__name = name

    @property
    def age(self):
        return self.__age

    @age.setter
    def age(self, age):
        if isinstance(age, int):
            self.__age += age

    # username = property(get_name, set_name)
    # userage = property(get_age, set_age)


if __name__ == '__main__':
    xm = PropertyTest('小明', 12)
    print(xm.name)
    xm.name = '小红'
    print(xm.name)
    print(xm.age)
    xm.age = (12)
    print(xm.age)
    xh = PropertyTest('小红', 10)
    print(xh.name)
    xh.name = '小明'
    print(xh.name)
    print(xh.age)
    xh.age = 14
    print(xh.age)

```

## 10.with语句和上下文管理器

>__  enter __ 表示上文方法，需要返回一个操作文件对象
>
>__ exit __ 表示下文方法，with语句执行完成会自动执行，即使出现异常也会执行改方法。

```python
import pymysql


class MySQLTest(object):
    def __init__(self, host='localhost', password='123456', database='miniweb', prot=3307, user='root', charset='utf8'):
        self.host = host
        self.password = password
        self.database = database
        self.port = prot
        self.user = user
        self.charset = charset

    def __enter__(self):
        """
        初始化方法
        :return: 实例化对象本身
        """
        self.conn = pymysql.connect(host=self.host, password=self.password, database=self.database, port=self.port,
                                    user=self.user, charset=self.charset)
        self.cursor = self.conn.cursor()
        return self

    def cursor_sql(self, sql):
        self.cursor.execute(sql)
        data_info = self.cursor.fetchall()
        return data_info

    def __exit__(self, exc_type, exc_val, exc_tb):
        """
        :param exc_type: 错误类型
        :param exc_val: 错误内容
        :param exc_tb: 错误来源
        """
        self.cursor.close()
        print('游标关闭')
        self.conn.close()
        print('数据库连接关闭')
        if exc_type:
            print('数据库操作出现了错误噢！')


if __name__ == '__main__':
    """
    利用with实现前置后置方法
    """
    with MySQLTest() as mysql:
        print(mysql.cursor_sql("""select * from info"""))
```

## 11.深拷贝与浅拷贝

>__浅拷贝__
>
>浅拷贝（Shallow Copy）指的是创建一个新对象，新对象中只有一个引用指向原对象，而原对象的内容会被复制到新对象中。
>
>__深拷贝__
>
>深拷贝（Deep Copy）指的是创建一个新对象，新对象中有两个引用指向原对象，确保了对象中所有数据都会被复制。

深浅拷贝对不同类型对象拷贝的区别

>对不可变对象，无论深浅拷贝，都相当于是引用的赋值。

__深浅拷贝对可变对象中保存不可变数据的拷贝原理图__

![image-20230514204652100](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514204652100.png)

__深浅拷贝对可变对象中保存可变数据的拷贝原理图__

- 浅

![image-20230514213227472](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514213227472.png)

- __深__

![image-20230514213329107](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514213329107.png)

## 12.正则表达式

>在实际开发过程中经常会有查找符合某些复杂规则的字符串的需求，比如：邮箱、图片地址、手机号码等，这时想匹配或者查找符合某些规则的字符串就可以使用正则表达式。

### 12.1在python中使用正则

- re模块的介绍

在python中需要通过正则表达式对字符串进行匹配的时候，可以使用一个re模块

```python
import re
# 使用match方法来进行匹配操作
# match 模块只能从头匹配
result = re.match('正则表达式，需要匹配的字符串')

result.group() # 如果上一步提取到数据则使用group来提取数据
```

匹配单个字符

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514215543648.png" alt="image-20230514215543648" style="zoom:200%;" />

匹配多个字符

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514215816741.png" alt="image-20230514215816741" style="zoom:200%;" />

为分组设置名

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514231427795.png" alt="image-20230514231427795" style="zoom:200%;" />

  正则的高级函数

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230514233115709.png" alt="image-20230514233115709" style="zoom:200%;" />
