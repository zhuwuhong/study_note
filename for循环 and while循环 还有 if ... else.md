# for循环 and while循环 还有 if ... else... 

>判断的真假
>
>真也就可以认为是满足条件及为真的意思
>
>假则是不满足条件就为假
>
>与或非（and or not）
>
>与（and）同时正确才为真
>
>或（or）只要有真及为真
>
>非（not）你真它就假你假它就真

## for循环

```python
在 Python 中，for 循环用于遍历一个序列（比如一个列表或者一个字符串）中的每个元素
```

```python
# 初始化一个存放颜色的列表
colors = ['red', 'green', 'blue']
# 使用for循环遍历这个存放了颜色的列表
for color in colors:
    print(color)

# 输出:
# red
# green
# blue
```

## while

```python
在 Python 中， while 循环则是在某个条件为真的情况下重复执行一段代码
```

```python
# 创建一个变量 i使其为1（i的作用:作为相加数存在）
i = 1
# 创建一个存放总和的变量初始化使为0（sum的作用:作为存放总数和的存在）
sum = 0
# while i <= 10的意思是当i小于或者等于10的时候则运行循环内部的语句
while i <= 10:
    # 如果满足条件则让sum加上那个相加数
    sum += i
    # 因为已经加过一次了那么第二次相加的话就要在i的原基础上再加上1
    i += 1

print(sum)  # 输出 55
```

## if...else...

```python
在 Python 中，if...else 语句用于根据条件判断执行不同的代码块
```

```python
if condition:
    # 在条件为真的情况下执行的代码
else:
    # 在条件为假的情况下执行的代码
```

```python
# 判断一个数是奇数还是假数
# num为想要判断的那个数字
num = 5
# 我们去判断这个数字是否被2整除
# %是求余数，如果num%2的结果等于0的话那么他就为偶数
if num % 2 == 0:
    # 当num%2等于0时执行
    print(num, '是偶数')
else:
    # 当num%2不等于0时执行
    print(num, '是奇数')

# 输出: 5 是奇数
```

```yacas
不过要注意的是
在 Python 中，if 和 else 后面的代码块都要缩进，表示它们是一个整体。
如果需要根据多个条件判断，可以使用 elif 语句，它的作用是在 if 语句的条件为假，而 elif 语句的条件为真的情况下执行代码块。
```

```python
# 判断一个数的正负性
# num为想要判断的那个数
num = 5
# 如果num>0的话就执行它缩进下的语句
if num > 0:
    # if num > 0为真时执行的语句
    print(num, '是正数')
# elif表示的为否则如果
# 否则如果 num<0的话执行它缩进下的话
elif num < 0:
    # 当elif num < 0 为真的时候执行的语句
    print(num, '是负数')
# 当if以及elif都为假的时候执行的语句，因此这个语句不需要判断
else:
    # 当执行到else时执行的语句
    print(num, '是 0')

# 输出: 5 是正数
```

