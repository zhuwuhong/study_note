# selenium学习笔记①元素

```yacas
元素操作方法:
	1.输入方法：send_keys('输入值')
	2.点击方法：click()
	3.清除方法：clear()
```

## 一、准备

- 学习所需环境：python解释器+pycharm+selenium+浏览器+浏览器驱动

- selenium

  ```
  pip install selenium
  ```

- 浏览器驱动

  - chrome：http://npm.taobao.org/mirrors/chromedriver/

    ```
    提示:浏览器驱动大版本必须和浏览器版本一致
    ```

  - 使用:

    ```
    windows:
    	1、解压下载的驱动，获取到chromdriver.exe
    	2、将chromdriver.exe复制到python.exe所在目录即可
    mac:
    	1、解压下载的驱动，获取到chromdriver
    	2、将chromdriver复制到/usr/local/bin目录即可
    ```

## 二、元素定位

- 什么是元素定位

  ```
  通过代码调用的方法查找元素
  ```

- 元素定位方法

  ```
  1、 id
  2、 name
  3、 class
  4、 tag_name
  5、 link_text
  6、 partial_link_text
  7、 xpath
  8、 css
  ```

- 使用步骤

  ```
  1、打开⾕歌浏览器
  2、输⼊url
  3、找元素及操作
  4、关闭浏览器
  ```

  ```python
  from time import sleep
  from selenium import webdriver
  # 1、打开⾕歌浏览器(实例化浏览器对象)
  driver = webdriver.Chrome()
  # 2、输⼊url
  driver.get("http://tpshop-test.itheima.net/Home/user/login.html")
  # 3、找元素及操作
  # 4、关闭浏览器
  sleep(3)
  driver.quit()
  ```

### 2.1 id定位

>定位格式：
>
>​		通过webdriver对象的find_element("属性名","属性值")
>
>例:(定位该网页中name属性为userA的位置) 
>
>​		driver.find_element("name", "userA")

- 方法: driver.find_element(value='id值')

- 前置: 标签必须又id属性

- 输入方法: send_keys('输入内容')

- 示例: 

  ```python
  from selenium import webdriver
  from time import sleep
  
  # 1.获取浏览器驱动
  driver = webdriver.Chrome()
  # 2.打开浏览器
  driver.get(
      url='file:///D:/web/%E6%B3%A8%E5%86%8CA.html')
  # 3.查找元素且进行操作
  #   3.1通过find_element方法查找ID为userA的输入框，输入admin
  driver.find_element(value='userA').send_keys('admin')
  #   3.1通过find_element方法查找ID为passwordA的输入框，输入123456
  driver.find_element(value='passwordA').send_keys('123456')
  # 4.关闭浏览器
  #   4.1停留3秒时间
  sleep(3)
  #   4.2利用浏览器驱动关闭浏览器
  driver.quit()
  ```

### 2.2 name定位

- 方法： driver.find_element('name', 'name属性值')。
- 前置：标签必须含有name属性。
- 特点：当前页面可以有重复的name属性值。
- 提示：由于name属性可以重复，所以使用时需要查看是否为唯一。

### 2.3 class_name定位

- 方法： driver.find_element('class name', 'class属性值')。
- 前置：标签必须含有class属性。
- 特点：class属性值可以有很多个。
- 提示：在定位class属性值时当该属性有多个class属性时，只需要定位其中一个即可。
### 2.4 tag_name定位

- 说明：根据标签名进行定位

- 方法：driver.find_element('tag name', '标签名称')
- 提示：如果页面存在多个相同的标签默认返回第一个。

### 2.5 link_text定位

- 说明：根据连接文本（a标签）定位
- 方法：driver.find_element('link text', "连接文本")
- 特点：传入的连接文本，必须全部匹配，不能模糊查询。
### 2.6 partial_link_text定位

- 说明：根据连接文本（a标签）定位
- 方法：driver.find_element('partial link text', "连接文本")
- 特点：传入的连接文，支持模糊查询。

### 2.6 扩展查找一组元素

- 说明：返回列表格式， 要使用需要添加下标或遍历
- 方法： driver.find_elements(xxxx,属性)
- 提示：八大元素定位方法，都可以使用一组元素定位，如果没有搜索到符合标签，则返回空列表。
### 2.7 xpath、css定位

  为什么学xpath、css

  ```
  1.如果没有（id/name/css）3个属性，也不是链接标签，只能使用tag_name定位，比较麻烦。
  2.方便工作中查找元素，使用xpath和css比较方便（支持任意属性、层级）来找元素。
  ```

#### 2.7.1xpath

- 说明：xpath是xml path的简称，使用标签路径来定位
  - 绝对路径：/html/body/form/div/fieldset/center/p[1]/input
  - 相对路径：//fieldset/center/p[1]/input

- 策略（方法）：

  ```
  1.路径
  2.属性
  3.属性与逻辑（多个属性）
  4.属性与层级（路径）
  ```

- 路径方法：driver.finde_element('xpath','xpath表达式')

- 实现：![image-20230112170230127](C:\Users\朱五红\Desktop\总结文件\image_data\image-20230112170230127.png)

- 属性与逻辑：

  - 单属性：

    find_element('xpath', '//*[@属性名="属性值"]')
    
  - 多属性：
  
    find_element('xpath', '//*[@属性名="属性值" and @属性名="属性值"]')

- 实现：

  ![image-20230112165650599](C:\Users\朱五红\Desktop\总结文件\image_data\image-20230112165650599.png)

- 属性与层级：

  - 说明：如果元素现有的属性不难唯一匹配，需要结合层级使用。
  
  - 语法：
    - //父标签/子标签       必须为直属子级
    - //父标签[@属性='值']//后代标签      父和后代之间可以跨越元素
  
  - 实现：
  
    ![image-20230112174124655](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230112174124655.png)
  
- 扩展1（xpath中属性包含某个关键字）：

  - 说明：当标签内某个元素中属性值包含某个关键字时使用。
  - 语法：
    - driver.find_element('xpath', '//input[contains(@placeholder,"账号")]')

- 扩展2（文本一致）:
  - 说明：如果元素中的文本标签与关键字一致的时候可以使用。
  - 语法：
    - driver.find_element('xpath', '//a[text()="访问 新浪 网站" ]')

- 扩展实现：

  ![屏幕截图_20230112_173002](C:\Users\朱五红\Pictures\Screenshots\屏幕截图_20230112_173002.png)

- xpath综合训练：

  - 需求：使用xpath方法对tpshop2.0商城进行登录操作

  - 实现：

    ![image-20230113141647893](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230113141647893.png)

#### 2.7.2css选择器

- 说明：css选择器是html查找元素的⼯具

- 策略：

  ```
  1、id选择器
  2、类选择器
  3、标签选择器
  4、属性选择器
  5、层级选择器
  ```

- id选择器
  - 语法：#id属性值
  - 前置：标签必须含有id属性

- 类选择器
  - 语法：.class属性值
  - 前置：标签必须含有class属性

- 标签选择器
  - 语法：标签名
  - 提示：注意标签是否在页面唯一，否则返回单个或所有

- 属性选择器
  - 语法：[属性名="属性值"]
  - 说明：标签任意属性都可以

- 层级选择器

  - 语法：

    ⽗⼦关系： 选择器>选择器 如： #p1>input

    后代关系： 选择器 选择器 如： #p1 input

  - 提示：选择器使⽤任何⼀种css选择器（id选择器、类选择器、属性选择器、标签选

    择器）都可以

- 综合案例：
  ![image-20230113154321460](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230113154321460.png)
  
  实现：
  
  ![image-20230113154427983](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230113154427983.png)

- 扩展：

  - 语法：^：以什么开头
    	       $：以什么结尾
               *：匹配所有

    ​		 例：标签名[属性名*='部分属性值']（含有）

  - 说明：当属性值过多或者不确定时使用。

## 三、获取元素信息

```yacas
⽅法:
获取⼤⼩： 元素.size
获取⽂本： 元素.text
获取属性： 元素.get_attribute('属性名')
元素是否可⻅： 元素.is_displayed()
元素是否可⽤： 元素.is_enabled()
元素是否选中： 元素.is_selected()
```

## 四、总结

![image-20230113154549921](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230113154549921.png)

```
结论：
 1、⾸推css定位，原因执⾏速度快。
 ①如果有ID属性，使⽤#id
 ②没有id属性，使⽤其他有的属性（能代表唯⼀的属性）
 ③如果属性都带不了唯⼀，使⽤层级
 2、如果css解决不了，使⽤xpath。
```

