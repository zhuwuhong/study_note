# selenium其他重要API

### 一、frame框架

- frame(iframe)标签作用是什么

  ```yacas
  在页面中加载另一个网页,可以在同一个页面中加载显示或使用另一个网页
  ```

- 为什么要处理frame（iframe）标签

  ```yacas
  焦点默认聚焦于主页面无法对frame标签中的页面进行控制
  ```

- 如何处理

  - 步骤：

    ```
    1.定位iframe元素
    2.切换iframe
    3.操作iframe标签中元素
    4.回到默认页面
    ```

  - 示例

    ```python
    from selenium import webdriver
    from time import sleep
    
    """
    对该网页中三个界面进行操作
    """
    driver = webdriver.Chrome()
    driver.get(url="file:///D:/web/Register.html")
    # 对首个页面进行输入操作
    driver.find_element('css selector', '#user').send_keys('admin')
    # 查找A页面
    A = driver.find_element('css selector', '#idframe1')
    # 将操作页面切换至A页面
    driver.switch_to.frame(A)
    # 对A页面进行操作
    driver.find_element('css selector', '#userA').send_keys('admin')
    # 切换回主页面
    driver.switch_to.default_content()
    # 对B页面进行定位
    B = driver.find_element('css selector', '#idframe2')
    # 切换至B页面
    driver.switch_to.frame(B)
    # 对B页面进行操作
    driver.find_element('css selector', '#userB').send_keys('admin')
    sleep(5)
    driver.quit()
    
    ```

### 二、多窗口操作

- 什么是多窗口

  ```yacas
  在网页操作中通过点击A标签后，浏览器打开了一个新的页面后，添加了一个新的窗口。
  ```

- 为什么要切换窗口

  ```yacas
  selenium库默认操作为首个窗口，如果要对新打开的窗口进行操作的话就要进行窗口切换否则会导致找不到元素/无法操作
  ```

- 怎么进行窗口切换

  ```yacas
  1.获取所有窗口句柄
  2.切换窗口句柄
  ```

  ```python
  示例：
  from time import sleep
  
  from selenium import webdriver
  from selenium.webdriver.support.wait import WebDriverWait
  """
  使用UI自动化实现4399登录功能
  """
  driver = webdriver.Chrome()
  driver.get(url="http://www.baidu.com")
  # 对百度输入框进行输入操作
  driver.find_element('css selector', '#kw').send_keys('4399小游戏')
  # 对百度搜索按钮进行操作
  driver.find_element('css selector', '#su').click()
  # 显示等待
  # 百度搜索后会导致找不到元素，因此等待搜索结果出现
  # 定位4399小游戏官网超链接
  el = WebDriverWait(driver, 5, 0.1).until(lambda x: x.find_element('css selector', "div[has-tts='false'] a"))
  # 点击标签
  el.click()
  # 获取窗口句柄
  print(f'当前网页窗口句柄有{driver.window_handles}')
  # 切换窗口
  driver.switch_to.window(driver.window_handles[1])
  # 对4399官网的登录按钮进行定位操作
  driver.find_element('css selector', '.ico_1').click()
  # 显示等待
  # 百度搜索后会导致找不到元素，因此等待搜索结果出现
  # 定位4399小游戏登录输入框
  dl_div = WebDriverWait(driver, 5, 0.5).until(lambda x: x.find_element('css selector', '#popup_login_frame'))
  # 切换iframe标签
  driver.switch_to.frame(dl_div)
  # 元素操作
  driver.find_element('css selector', '#username').send_keys('32644356')
  # 元素操作
  driver.find_element('css selector', '#j-password').send_keys('3913998')
  # 元素操作
  driver.find_element('css selector', '.ptlogin_btn').click()
  sleep(10)
  driver.quit()
  ```

- 多窗口切换工具

  ```python
  from time import sleep
  
  from selenium import webdriver
  
  """
      随心所欲的切换窗口
      思路：
          1.获取所有窗口句柄
          2.切换窗口
          3.判断当前所在窗口的title
          4.判断title是否为所需要的窗口
          5.执行代码
  """
  
  
  def switch_window(driver, title):
      handles = driver.window_handles
      for i in handles:
          driver.switch_to.window(i)
          print(f'期望title为:{title},当前title为:{driver.title}')
          if title == driver.title:
              return i
          else:
              continue
  
  
  if __name__ == '__main__':
      driver = webdriver.Chrome()
      driver.get(url="file:///D:/web/Register.html")
      el = driver.find_elements("css selector", 'a')
      for i in el:
          i.click()
      sleep(5)
      handle = switch_window(driver, '注册B')
      driver.switch_to.window(handle)
      driver.find_element('css selector', '#userB').send_keys('admin')
      sleep(5)
      driver.quit()
  ```

### 小结：

- 当你编写UI自动化脚本时无法定位元素怎么办

  >1.检查脚本代码是否编写正确
  >
  >2.是否是匹配唯一元素
  >
  >3.是否做了元素等待
  >
  >4.是否需要鼠标悬浮
  >
  >5.元素是否存在于新窗口
  >
  >6.元素是否存在与iframe标签中

### 三、报错截图

- 语法：driver.get_screenshot_as_file(文件名称及路径)

  示例：driver.get_screenshot_as_file("./Error/handles_Error{}.png".format(datetime.datetime.now().strftime("%Y年%m月%d日%H点%M分")))

- 作用：当脚本在运行时出现报错，单单通过日志无法知道错误地方，因此使用报错截图。

#### 四、验证码处理

- 处理方式

  ```yacas
  1.去除验证码
  2.使用万能验证码
  3.使用图片识别技术
  4.使用cookie实现登录
  ```

​	5.1 cookie

- 说明：由服务器生成，储存在客户端的登录凭证

- 使用：

  ```yacas
  1.获取cookie # 获取所有的cookie driver.get_cookies()
  2.添加cookie # driver.add_cookie(data)
  ```

- 示例

  ```python
  # 1.获取cookie信息
  from time import sleep
  
  from selenium import webdriver
  from selenium.webdriver.support.wait import WebDriverWait
  
  """
  使用UI自动化实现4399登录功能
  """
  driver = webdriver.Chrome()
  driver.get(url="http://www.baidu.com")
  driver.find_element('css selector', '#kw').send_keys('4399小游戏')
  driver.find_element('css selector', '#su').click()
  el = WebDriverWait(driver, 5, 0.1).until(lambda x: x.find_element('css selector', "div[has-tts='false'] a"))
  el.click()
  print(f'当前网页窗口句柄有{driver.window_handles}')
  driver.switch_to.window(driver.window_handles[1])
  driver.find_element('css selector', '.ico_1').click()
  dl_div = WebDriverWait(driver, 5, 0.5).until(lambda x: x.find_element('css selector', '#popup_login_frame'))
  driver.switch_to.frame(dl_div)
  driver.find_element('css selector', '#username').send_keys('32644356')
  driver.find_element('css selector', '#j-password').send_keys('3913998')
  driver.find_element('css selector', '.ptlogin_btn').click()
  sleep(10)
  print(driver.get_cookies())
  driver.quit()
  ```

  ```python
  # 2.使用获得的cookie信息进行添加
  from time import sleep
  
  from selenium import webdriver
  from selenium.webdriver.support.wait import WebDriverWait
  
  driver = webdriver.Chrome()
  cookies = [
      {'domain': '.4399.com', 'expiry': 1709969873, 'httpOnly': False, 'name': 'Pnick', 'path': '/', 'secure': False,
       'value': '%E5%85%BB%E5%BE%B7%E8%BE%89'},
      {'domain': '.4399.com', 'expiry': 1709969873, 'httpOnly': False, 'name': 'ptusertype', 'path': '/', 'secure': False,
       'value': 'www_home.4399_login'},
      {'domain': '.4399.com', 'expiry': 1676705873, 'httpOnly': False, 'name': 'Xauth', 'path': '/', 'secure': False,
       'value': 'fd5549829d780606d3973a879abf1d9c'},
      {'domain': '.4399.com', 'httpOnly': False, 'name': 'Hm_lpvt_334aca66d28b3b338a76075366b2b9e8', 'path': '/',
       'secure': False, 'value': '1675409872'},
      {'domain': '.4399.com', 'expiry': 1676705873, 'httpOnly': False, 'name': 'Uauth', 'path': '/', 'secure': False,
       'value': '4399|1|202323|www_home.|1675409869896|70f053829a23e9cac865a1d6595c09fd'},
      {'domain': '.4399.com', 'expiry': 1709969873, 'httpOnly': False, 'name': 'Puser', 'path': '/', 'secure': False,
       'value': '32644356'},
      {'domain': '.4399.com', 'expiry': 1676705872, 'httpOnly': False, 'name': 'phlogact', 'path': '/', 'secure': False,
       'value': 'l127469'}, {'domain': '.4399.com', 'httpOnly': False, 'name': 'USESSIONID', 'path': '/', 'secure': False,
                             'value': 'e2fb58f5-3866-4451-8fcf-c198e2c59eed'},
      {'domain': '.4399.com', 'httpOnly': False, 'name': 'ck_accname', 'path': '/', 'secure': False, 'value': '32644356'},
      {'domain': '.4399.com', 'expiry': 1709969873, 'httpOnly': False, 'name': 'Qnick', 'path': '/', 'secure': False,
       'value': ''},
      {'domain': '.4399.com', 'expiry': 1706945871, 'httpOnly': False, 'name': 'Hm_lvt_334aca66d28b3b338a76075366b2b9e8',
       'path': '/', 'secure': False, 'value': '1675409872'},
      {'domain': '.4399.com', 'expiry': 1691134671, 'httpOnly': False, 'name': 'UM_distinctid', 'path': '/',
       'secure': False, 'value': '1861635d24a107b-04f7ec567ee0f3-26021051-144000-1861635d24b1012'},
      {'domain': '.4399.com', 'expiry': 1676705873, 'httpOnly': False, 'name': 'Pauth', 'path': '/', 'secure': False,
       'value': '225661322|32644356|t3ce7n190598a505e967e6a34c72eb2e|1675409869|10002|dea1e64a3cdf98ab2a991b52baf9b4f2|2'},
      {'domain': '.4399.com', 'expiry': 1675841870, 'httpOnly': False, 'name': 'home4399', 'path': '/', 'secure': False,
       'value': 'yes'}]
  driver.get(url='http://www.4399.com')
  sleep(5)
  for cookie in cookies:
      # 根据获得的cooki信息进行添加格式
      cookie_dict = {
          "domain": ".4399.com",
          'name': cookie.get("name"),
          # 'expiry': cookie.get('expiry'),
          'httpOnly': False,
          'path': '/',
          'secure': False,
          'value': cookie.get('value')
      }
      driver.add_cookie(cookie_dict)
  driver.refresh()
  sleep(5)
  driver.quit()
  
  ```

  