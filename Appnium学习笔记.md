# Appnium学习笔记

## 一、adb命令

### ① 获取包名和启动名

- 包名： `一个安卓应用的唯一标识符，操作应用所需要依赖包名。`
- 启动名：`应用中界面标识符，允许重复。`

```
1. mac/linux：adb shell dumpsys window | grep usedApp
2. windows: adb shell dumpsys window | findstr usedApp
```

![image-20230215160246556](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230215160246556.png)

### ②上传本地文件到安卓手机上

- 上传本地文件：`adb push 本地文件路径 /sdcard`
- 下载手机文件：`adb pull 需要下载文件路径 存放本地路径`

### ③启动时间

- 命令：`adb shell am start -W 包名/启动名`

![image-20230215225844766](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230215225844766.png)

```yacas
注意：查看时间 一般要冷启动（应用程序没有启动）
冷启动：应用程序未在后台打开
热启动：应用程序在后台打开
```

### ④查看日志

- 命令：`adb locat > 日志存放本地路径`
-  提示：`对app操作时，要开启日志,用于记录APP的操作步骤与异常报错。`

### ⑤其他常用命令

1. 安装app到手机

   命令：`adb install app存放路径`

​	2.卸载手机上的app（需要指定的包名）

​		命令：`adb uninstall 包名`

 3. 获取当前电脑已经连接的设备以及对应的设备号

    命令：`adb devices`

​	4.进入到安卓手机内部的linux系统命令行中

​		命令：`adb shell`

 5. 启动adb服务端(出bug是使用可以重启服务器，先关闭再启动)

    命令：`adb start-server`

 6. 停止adb服务端(出bug是使用可以重启服务器，先关闭再启动)

    命令：`adb kill-server`

 7. 查看adb帮助，命令行记不清楚的时候有用

    命令：`adb --help`

 8. 连接手机/模拟器

    命令：`adb connect ip:端口`

## 二、元素定位工具

> 为什么要查看元素信息？
>
>说明：自动化测试就是查找元素操作元素，要查找元素，就需要根据元素的信息来进行 。

### ①启动工具

- 命令：`在终端中输入 UiAutomatorViewer`

```yacas
注意： 当UiAutomatorViewer无法进行截图或出现报错时多半是因为adb服务出现错误。
我们可以通过重新启动服务进行解决
adb kill-server
adb start-server
```

## 三、python中appium基础操作API

### 3.1 入门示例

>前置：必须启动appium服务、模拟器

```python
from appium import webdriver
# 定义字典变量
desired_caps = {}
# 字典追加启动参数
# platformName为操作系统
desired_caps["platformName"] = "Android"
# platformVersion操作系统版本
desired_caps["platformVersion"] = "7.1.2"
# 设备IP及端口号 andorid不检测，ios会对ip及其端口进行检测  
desired_caps["deviceName"] = "emulator:5554"
# 报名
desired_caps["appPackage"] = "com.android.settings"
# 启动名
desired_caps["appActivity"] = ".Settings"
# 设置中文
desired_caps["unicodeKeyboard"] = True
desired_caps["resetKeyboard"] = True
# 获取driver
driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
```

### 3.2基础API

##### ①跳转应用

- 语法：`driver.start_activity(启动名,包名)`
- 说明：appium支持跨应用，可以在操作应用中且坏到B应用

##### ②获取当前包名、启动名

- 获取包名语法：`driver.current_package`
- 获取当前启动名语法：`driver.current_activity`

练习：

```python
"""
    需求:
        1.启动设置后,暂停3秒,打开通讯录应用
        2.打印当前默认应用包名和启动名
"""
sleep(3)
# 启动通讯录
driver.start_activity('com.android.contacts', '.activities.PeopleActivity')
# 打印包名和启动名
print('当前包名为:' + driver.current_package)
print('当前启动名为:' + driver.current_activity)
```

##### ③关闭APP

- 语法：`driver,close_app()`

##### ④安装APP

- 语法：`driver.install_app(安装包路径)`

##### ⑤卸载APP

- 语法：`driver.remove_app(包名)`

##### ⑥判断APP是否安装

- 语法：`driver.is_app——install(包名)`
- 说明：return为True/False

##### ⑦置于后台

- 语法：`driver.background_app(seconds) seconds为放置时间`

##### ⑧关闭驱动

- 语法：`driver.quit()`

##### ⑨滑动位置

- 语法：`driver.swipe(stat_x,stat_y,end_x,end_y,duration)`

  ```python
  from time import sleep
  
  from appium import webdriver
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  desired_caps["platformName"] = "Android"
  desired_caps["platformVersion"] = "7.1.2"
  desired_caps["deviceName"] = "192.168.56.101:5555"
  desired_caps["appPackage"] = "com.netease.newsreader.activity"
  desired_caps["appActivity"] = "com.netease.nr.phone.main.MainActivity"
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  """
      需求：从屏幕100,1000位置滑动到100,400位置
  """
  sleep(5)
  print('暂停完成')
  i = 0
  while i <= 4:
      driver.swipe(800, 224, 100, 224)
      print(f'已经滑动{i + 1}次')
      i += 1
  print('开始暂停1秒')
  sleep(1)
  print('开始定位')
  el = driver.find_element_by_xpath('//*[@text="健康"]')
  print(f'定位找到')
  el.click()
  print('点击完成健康完成')
  driver.quit()
  
  ```

##### ⑩滚动、拖拽操作

- 滚动操作
  - 语法：`driver.scroll(exe,more)`
  - 将初始位置滚动到目标位置（不是特别准确）

- 拖拽操作

  - 语法：`driver.drag_and_drop(exe,more)`
  - 将初始位置拖拽到目标位置（较为准确）

  代码展示：

  ```python
  from time import sleep
  
  from appium import webdriver
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  desired_caps["platformName"] = "Android"
  desired_caps["platformVersion"] = "7.1.2"
  desired_caps["deviceName"] = "192.168.56.101:5555"
  desired_caps["appPackage"] = "com.android.settings"
  desired_caps["appActivity"] = ".Settings"
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  exe = driver.find_element_by_xpath('//*[@text="显示"]')
  more = driver.find_element_by_xpath('//*[@text="建议"]')
  # 滚动(直接滚动屏幕)
  # driver.scroll(exe,more)
  # 拖拽(点击元素进行拖拽较为准确)
  driver.drag_and_drop(exe,more)
  sleep(1)
  driver.quit()
  ```


## 四、appium中元素定位方法

##### ①id元素定位

- 语法：`driver.find_element('id','id信息语句')`
- id信息语句为：![image-20230217134315099](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230217134315099.png)

##### ②class元素定位

- 语法：`driver.find_element('class name','class信息语句')`
- class信息语句为：![image-20230217134433843](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230217134433843.png)

##### ③xpath元素定位

- 语法：`driver.find_element('xpath','//*[属性名=属性值]')`

##### ④name元素定位

- 语法：` `
- name信息语句为：![image-20230217134657013](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230217134657013.png)

##### 练习：

```python
from time import sleep

from appium import webdriver

# 定义字典变量
desired_caps = {}
# 字典追加启动参数
# platformName为操作系统
desired_caps["platformName"] = "Android"
# platformVersion操作系统版本
desired_caps["platformVersion"] = "7.1.2"
# 设备IP及端口号
desired_caps["deviceName"] = "emulator:5554"
# 报名
desired_caps["appPackage"] = "com.android.settings"
# 启动名
desired_caps["appActivity"] = ".Settings"
# 设置中文
desired_caps["unicodeKeyboard"] = True
desired_caps["resetKeyboard"] = True
# 获取driver
driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
"""
    需求:
        1.使用ID定位点击放大镜
        2.使用CLASS定位输入Hello
        3.使用XPATH定位点击返回
        4.使用NAME定位点击放大镜按钮
        5.等待3S关闭APP
"""
print('正在使用ID定位点击放大镜')
driver.find_element('id', 'com.android.settings:id/search').click()
sleep(1)
print('正在使用CLASS定位输入Hello')
driver.find_element('class name', 'android.widget.EditText').clear().send_keys('Hello')
sleep(1)
print('正在使用XPATH定位点击返回')
driver.find_element('xpath', '//*[@class="android.widget.ImageButton"]').click()
sleep(1)
print('正在使用NAME定位点击放大镜按钮')
driver.find_element('accessibility id', '搜索设置').click()
sleep(2)
print('正在关闭driver')
driver.quit()
```

## 五、元素获取信息

##### ①获取元素文本信息

- 语法：element.text

##### ②获取元素位置

- 语法：element.location

##### ③获取元素大小

- 语法：element.size

## 六、手势操作

##### ①轻点

- 语法：`TouchAction(driver/元素坐标(x,y)).tap(el).perform() `

- 示例：

  ```python
  el = driver.find_element_by_xpath("//*[@text='WLAN']")
  TouchAction(driver).tap(el).perform()
  sleep(2)
  driver.quit()
  ```

##### ②按下与释放

- 按下：`press(元素/坐标)`

- 释放：`release()`

- 示例

  ```python
  el = driver.find_element_by_xpath("//*[@text='WLAN']")
  lco = el.location
  TouchAction(driver).press(x=lco.get("x"),y=lco.get("y")).release().perform()
  sleep(2)
  driver.quit()
  ```

##### ③长按

- 长按：`long_press`(元素/坐标)

- 示例

  ```python
  el = driver.find_element_by_xpath("//*[@text='yuyu']")
  lco = el.location
  TouchAction(driver).long_press(x=lco.get("x"),y=lco.get("y")).perform()
  driver.quit()
  ```

##### ④移动

- 移动：`.move_to(x,y)`

- 示例：

  ```python
  ===================================设置九宫格密码========================================================
  from time import sleep
  
  from appium import webdriver
  from appium.webdriver.common.touch_action import TouchAction
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  # platformName为操作系统
  desired_caps["platformName"] = "Android"
  # platformVersion操作系统版本
  desired_caps["platformVersion"] = "7.1.2"
  # 设备IP及端口号
  desired_caps["deviceName"] = "emulator:5554"
  # 报名
  desired_caps["appPackage"] = "com.android.settings"
  # 启动名
  desired_caps["appActivity"] = ".Settings"
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  start = driver.find_element_by_xpath("//*[@text='显示']")
  end = driver.find_element_by_xpath("//*[@text='使用指纹']")
  driver.drag_and_drop(start, end)
  sleep(2)
  start = driver.find_element_by_xpath("//*[@text='存储']")
  end = driver.find_element_by_xpath("//*[@text='显示']")
  driver.drag_and_drop(start, end)
  sleep(2)
  el = driver.find_element_by_xpath("//*[@text='安全']")
  el.click()
  el = driver.find_element_by_xpath("//*[@text='屏幕锁定']")
  el.click()
  sleep(1)
  driver.find_element_by_xpath("//*[@text='图案']").click()
  sleep(2)
  """
  1.  235,993  548,993  845,993
  2.           544,1276
  3.  235,1577 544,1577 845,1577
  """
  # 开始绘制九宫格密码
  TouchAction(driver).press(x=235, y=993).wait(100).move_to(x=548, y=993).move_to(x=845, y=993).wait(100).move_to(x=544, y=1276).move_to(
      x=233, y=1577).wait(100).move_to(x=544, y=1577).move_to(x=845,y=1577).release().perform()
  sleep(5)
  driver.quit()
  
  ```

##### ⑤获取网络模式、设置网络模式、获取分辨率、截图

- 获取网络模式：`driver.network_connection`

- 设置网络模式：`driver.set_network_connection(网络模式(数字))`

  - 注释：0为无，1为飞行模式，2为wifi，4为数据网络，6为wifi和数据网络共用

- 获取分辨率：`driver.get_window_size()`

- 截图：`driver,get_screenshot_as_file(截图保存路径)`

- 示例

  ```python
  from time import sleep
  
  from appium import webdriver
  from appium.webdriver.common.touch_action import TouchAction
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  # platformName为操作系统
  desired_caps["platformName"] = "Android"
  # platformVersion操作系统版本
  desired_caps["platformVersion"] = "7.1.2"
  # 设备IP及端口号
  desired_caps["deviceName"] = "emulator:5554"
  # 报名
  desired_caps["appPackage"] = "com.android.settings"
  # 启动名
  desired_caps["appActivity"] = ".Settings"
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  """
  需求：
      1.获取网络模式
      2. 设置网络模式为飞行模式
      3. 获取分辨率
      4. 截图
  """
  network = driver.network_connection
  match network:
      case 0: print('当前网络模式为：无')
      case 1: print('当前网络模式为：飞行模式')
      case 2: print('当前网络模式为：WIFI')
      case 4: print('当前网络模式为：数据网络')
      case 6: print('当前网络模式为：WIFI 和 数据网络共用')
  driver.set_network_connection(6)
  print('飞行模式设置成功')
  print(f'当前手机分辨率为:{driver.get_window_size()}')
  driver.get_screenshot_as_file('./screen.png')
  print('截图成功已保存')
  ```

##### ⑥模拟手机按键

- 语法：`driver.press_keycode(keycode)`

- 注意：keycode表示的设备的默认按键

- keycode：

  ![image-20230222184731188](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230222184731188.png)

##### ⑦打开通知栏

- 语法：`driver.open_notifications()`
- 应用场景：查看服务器发送的定时通知

- 示例

  ```python
  from time import sleep
  
  from appium import webdriver
  from appium.webdriver.common.touch_action import TouchAction
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  # platformName为操作系统
  desired_caps["platformName"] = "Android"
  # platformVersion操作系统版本
  desired_caps["platformVersion"] = "7.1.2"
  # 设备IP及端口号
  desired_caps["deviceName"] = "emulator:5554"
  # 报名
  desired_caps["appPackage"] = "com.android.settings"
  # 启动名
  desired_caps["appActivity"] = ".Settings"
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  """
  需求：
      1.打开通知栏
      2.全部清除通知栏
  """
  driver.open_notifications()
  sleep(2)
  driver.find_element_by_xpath('//*[@text="全部清除"]').click()
  sleep(2)
  driver.quit()
  ```

##### ⑧toast消息获取

实现：

> 使用语句 pip install uiautomator2下载
>
> 下载失败时可以使用 pip --default-timeout=100 install gevent
>
> 后使用 pip install --upgrade --pre uiautomator2 下载

步骤：

>1. 安装依赖库
>2. 配置driver启动参数
>3. 3.编写代码获取文本值

应用场景：

> 场景：在出现某些定时弹窗时获取弹窗上的文本内容
>
> 目的：可以使用获取到的文本内容进行断言

- 语法：在创建desired_caps字典中添加`desired_caps['automationName'] = 'Uiautomator2'`字段

- 示例：获取作业帮微信登录时弹出的定时弹窗

  ```python
  from time import sleep
  
  from appium import webdriver
  from appium.webdriver.common.touch_action import TouchAction
  
  # 定义字典变量
  desired_caps = {}
  # 字典追加启动参数
  # platformName为操作系统
  desired_caps["platformName"] = "Android"
  # platformVersion操作系统版本
  desired_caps["platformVersion"] = "7.1.2"
  # 设备IP及端口号
  desired_caps["deviceName"] = "emulator:5554"
  # 报名
  desired_caps["appPackage"] = "com.baidu.homework"
  # 启动名
  desired_caps["appActivity"] = ".activity.user.passport.ChoiceLoginModeActivity"
  # 获取toast
  desired_caps['automationName'] = 'Uiautomator2'
  # 设置中文
  desired_caps["unicodeKeyboard"] = True
  desired_caps["resetKeyboard"] = True
  # 获取driver
  driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", desired_caps)
  """
      需求：
      1. 作业帮微信登录获取toast
  """
  sleep(1)
  driver.find_element_by_xpath('//*[@text="微信"]').click()
  msg = driver.find_element_by_xpath("//*[contains(@text,'请先安装')]").text
  print("toast消息为：",msg)
  sleep(3)
  driver.quit()
  ```
  

⑨切换环境(webView)

- 为什么要钱还？

  ```yacas
  app中嵌套web信息，如果不切换的话就无法定位操作元素
  ```

- 如何切换

  ```yacas
  1.获取当前环境 ---> driver.contexts
  2.切换环境 ---> driver.switch_to.context('环境')
  ```

- 示例

  ```python
  # 1.定位url栏
  el = driver.find_element_by_xpath('//*[@text="https://www.ldmnq.com/app/"]')
  # 2，点击
  el.click()
  # 3.清空
  el.clear()
  # 4.输入百度的网址
  el.send_keys('https://m.baidu.com')
  # 5.模拟回车按键
  driver.press_keycode(66)
  # 点击拒绝共享信息
  el = driver.find_element_by_xpath('//*[@text="拒绝"]').click()
  # 获取当前页面中的环境
  print(driver.contexts)
  # 切换环境
  driver.switch_to.context('WEBVIEW_com.android.browser')
  # 定位输入框并输入it黑马
  driver.find_element_by_xpath('//*[@id="index-kw"]').send_keys('it黑马')
  # 定位搜索按钮并点击
  driver.find_element_by_xpath('//*[@id="index-bn"]').click()
  sleep(5)
  driver.quit()
  ```


## 七、Monkey

- 什么是monkey？

  ```
  Android系统中自带的一种测试压力的小工具，主要测试系统或应用稳定性。
  ```

- monkey测试时什么？

  ```
  测试是否崩溃、闪退、死机
  ```

- 执行命令是什么？

  ```yacas
  adb shell monke -p com.yuanmall.lc -v -v 10000 > xxx.loh
  ```

  - -p:包名

  - -v-v:日志等级

  - 10000:乱抓的次数

  - -s：设置随机种子数（两次执行随机种子数一样，执行的事件也是一样的）

  - 其他参数

    ![image-20230226101513626](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230226101513626.png)

- 日志查看什么？

  ```
  搜索：“ANR”、ERROR、null、相关错误
  ```
