# selenium学习笔记②浏览器

### 1.浏览器操作

#### 	1.1最大化浏览器页面
- 语法：driver.maximize_window()
- 作用：将浏览器页面最大化。
#### 	1.2设置页面大小
- 语法： driver.set_window_size(x,y) x代表x轴，y表示y轴
- 作用：将浏览器页面设置为一定的大小。
#### 	1.3设置页面所在位置
- 语法：driver.set_window_position(width,height)
- 作用：将浏览器拖动到一定的位置。
#### 	1.4返回上一个页面
- 语法：driver.back()
- 作用：将浏览器页面返回到之前的页面。
#### 	1.5前往浏览器前置页面（也就是回退前的页面）
- 语法：driver.forward()
- 作用：奖励领取返回到会退钱的页面。
#### 	1.6刷新页面
- 语法：driver.refresh()
- 作用：刷新浏览器当前网页。
#### 综合练习
![image-20230121204652825](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230121204652825.png)

### 2.网页信息操作

#### 2.1获取网页标题

- 语法：driver.title
- 作用：获取锁定窗口的标题
#### 2.2获取网页url

- 语法： driver.driver.current_url
- 作用：获取锁定窗口的URL

#### 2.3关闭窗口

- 语法：driver.close()
- 作用：将锁定的浏览器窗口关闭

#### 综合练习

![image-20230129180028965](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230129180028965.png)

### 3.特殊操作

#### 3.1下拉框操作

- 语法：select_by_index()
- 作用：根据下标对下拉框进行选择。
- 语法：select_by_value('xx')
- 作用：根据下拉框选项的value值进行选择。
- 语法：select_by_visible_text('x')
- 作用：根据下拉框选项的文本内容进行选择。

#### 综合练习

![image-20230130150251003](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230130150251003.png)

#### 3.2弹窗处理

1、为什么要处理弹窗？

```yacas
如果页面操作过程中，有弹窗出现，不处理，无法继续对页面进行操作。
```

2、弹窗类型？

```yacas
1.js原生弹窗(警告框、提示框、输入框)必须处理
2.开发使用标签自定义弹窗效果(不用处理，正常操作即可。)
```

3、如何处理？

```yacas
步骤：
	1.获取弹窗对象
	2.点击确认/取消
```

示例：
```python
from selenium import webdriver
from time import sleep

# 实例化webdriver对象操作谷歌浏览器
driver = webdriver.Chrome()
# 通过get方法对网址进行打开
driver.get(url="file:///D:/web/%E6%B3%A8%E5%86%8CA.html")
# 对对应弹窗进行操作
driver.find_element('css selector', '#alerta').click()
sleep(2)
# 获取弹窗对象
el = driver.switch_to.alert
# 获取弹窗文本
print('弹窗文本为：' + el.text)
# 点击确认
el.accept()
# 对对应弹窗进行操作
driver.find_element('css selector', '#confirma').click()
# 获取弹窗对象
el = driver.switch_to.alert
# 获取弹窗文本
print('弹窗文本为：' + el.text)
# 点击取消
el.dismiss()
# 对对应弹窗进行操作
driver.find_element('css selector', '#prompta').click()
# 获取弹窗文本
print('弹窗文本为：' + el.text)
# 点击取消
el.dismiss()
sleep(2)
# 关闭浏览器
driver.quit()
```

#### 3.3滚动条操作

1、为什么要操作滚动条

```yacas
有些页面场景需要将滚动条拉到最低下才能进行某种操作
如：注册用户时，需要阅读完用户须知后才能点击确定
```

2、步骤

```yacas
1.定义js语句
2.调用方法执行js语句
```

3、示例

```python
from time import sleep

from selenium import webdriver

# 1、获取浏览器
from selenium.webdriver.common.by import By
from selenium.webdriver.support.select import Select

driver = webdriver.Chrome()
# 2、打开url
driver.get("file:///Users/lgy/Documents/fodder/web/%E6%B3%A8%E5%86%8CA.html")
# 设置窗口大小
driver.set_window_size(100,100)
sleep(2)
# js -> 向下
# js_down = "window.scrollTo(0,10000)"
# 动态执行滑倒底部 document.body.scrollHeight
js_down = "window.scrollTo(0,document.body.scrollHeight)"

# 执行js方法
driver.execute_script(js_down)
sleep(2)
# js—> 向上
js_top = "window.scrollTo(0,0)"
driver.execute_script(js_top)
===================================================================================
# ui 与li 标签进行操作
# 定位要点击的元素
el_t = WebDriverWait(driver=driver, timeout=10, poll_frequency=0.5).until(
    lambda x: x.find_elements('xpath', "//div[@class='ant-time-picker-panel-select']/ul/li"))
# 使用arguments[0]对页面元素去进行定位点击
driver.execute_script('arguments[0].click()', el_t[23]);
```

### 4.鼠标操作

#### 4.1普通操作

- 方法一：悬停
  - 语法：action.move_to_element(element)
  - 作用：将鼠标悬停在元素对象上。

- 方法二：右击
  - 语法：action.context_click(element)
  - 作用：鼠标对元素对象进行右击操作。

- 方法三：双击
  - 语法：action.double_click(element)
  - 作用：鼠标对元素对象进行双击操作。

- 使用方法：

  ```
  鼠标操作
  1.实例化鼠标操作对象
  2.调用鼠标操作方法（传入鼠标操作的元素对象）且使用perform对象进行操作
  ```

#### 综合练习

```python
from selenium import webdriver
from time import sleep
from selenium.webdriver import ActionChains

"""
鼠标操作
1.实例化鼠标操作对象
2.调用鼠标操作方法（传入鼠标操作的元素对象）且使用perform对象进行操作
"""
driver = webdriver.Chrome()
driver.get(url="file:///D:/web/%E6%B3%A8%E5%86%8CA.html")
"练习一 鼠标悬停注册按钮"
# 实例化鼠标操作对象
action = ActionChains(driver)
# 确认鼠标操作元素对象
el = driver.find_element('css selector', '[value="注册A"]')
# 执行悬停操作
action.move_to_element(el).perform()
sleep(3)
# 确认鼠标操作元素对象
"练习二 鼠标邮寄用户输入框"
el = driver.find_element('css selector', '#userA')
# 执行右击操作
action.context_click(el).perform()
sleep(3)
"练习三 对用户输入框输入admin后双击用户输入框"
el.send_keys('admin')
action.double_click(el).perform()
sleep(5)
driver.quit()
```

#### 4.2鼠标拖动操作

- 语法：drag_and_drop(拖动的元素, 拖动至的元素位置)
- 作用：将某个元素拖动到某一个元素的位置。

#### 综合练习

```python
from selenium import webdriver
from selenium.webdriver import ActionChains
from time import sleep

driver = webdriver.Chrome()
driver.get(url="file:///D:/web/drop.html")
action = ActionChains(driver)
div1 = driver.find_element('css selector', '#div1')
div2 = driver.find_element('css selector', '#div2')
action.drag_and_drop(div1, div2).perform()
sleep(5)
driver.quit()
```

### 5.等待操作

- 什么是等待

```yacas
代码执行中，第一次未找到元素，先不抛出异常，激活等待时间，在等待过程中如果自己安排搭配元素就执行
```

- 为什么要等待

```yacas
由于网络或配置原因，导致元素未加载出来，而代码执行，会触发异常。
```

- 元素等待类型

```yacas
1.隐式等待
2.显示等待
3.强制等待 ----> time.sleep(秒)
```

#### 5.1隐式元素等待

- 说明：`针对全部元素生效`

- 方法：`driver.implicitly_wait(秒)`

- 作用：隐式等待是全局的是针对所有元素，设置等待时间如10秒，如果10
  秒内出现，则继续向下，否则抛异常。可以理解为在10秒以内，不
  停刷新看元素是否加载出来

- 提示：在项目中，如果未封装自动化框架时，推荐使用。

- 示例：

  ```python
  from selenium import webdriver
  from time import sleep
  
  driver = webdriver.Chrome()
  driver.get(url='http://www.baidu.com')
  driver.find_element('css selector', '#kw').send_keys('4399小游戏')
  driver.find_element('css selector', '#su').click()
  # 隐式等待
  driver.implicitly_wait(3)
  driver.find_element('css selector', 'h3>a').click()
  sleep(5)
  driver.quit()
  
  ```

#### 5.2显示等待

- 说明：`针对某个特定的元素生效`

- 方法：WebDriverwait(driver,timeout,poll_frequency).until(lambda x: x.find_element('css selector', '表达式')) #其中timeout指的是等待的时间，poll_frequency指的是间隔时间

- 作用：显示等待是单独针对某个元素，设置一个等待时间如5秒，每隔0.5
  秒检查一次是否出现，如果在5秒之前任何时候出现，则继续向下，
  超过5秒尚未出现则抛异常。

- 示例：

  ```python
  from selenium import webdriver
  from selenium.webdriver.support.wait import WebDriverWait
  from time import sleep
  
  driver = webdriver.Chrome()
  driver.get(url='http://www.baidu.com')
  driver.find_element('css selector', '#kw').send_keys('4399小游戏')
  driver.find_element('css selector', '#su').click()
  # 显示等待
  """ 2指的是等待时间 0.5指的是每次查询的间隔时间"""
  el = WebDriverWait(driver, 5, 0.5).until(lambda x: x.find_element('css selector', '#userAA'))
  el.click()
  sleep(5)
  driver.quit()
  ```

#### 5.3强制等待

- 说明：无论是否找到该元素都要强制等待。
- 方法：sleep(秒)
