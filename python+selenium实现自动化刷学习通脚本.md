python+selenium实现自动化刷学习通脚本

依赖:

>python + selenium+Chrome驱动

selenium下载

>pip3 install selenium

文件组成：

>config.py  # 配置文件里面包含了usename，password，LoginType，Host
>
>dome_1.py # 脚本实现

config.py

```python
# 登录学习通的账号
username = "输入你的账号"
# 用户密码
password = "输入你的密码"
# 其中默认是1,手机号密码登陆;2位手机号验证码登陆;3位学号密码登陆,但是3加入的验证码,
loginType = "1"
# 学习通登录URL
Hsot = f'https://passport2.chaoxing.com/login?newversion=true&loginType={loginType}'
# 需要观看的课程名
curriculum_list = []
```

demo_1.py

```python
import xxt_demo.config
from selenium import webdriver
from selenium.webdriver.support.wait import WebDriverWait
from time import sleep
from selenium.webdriver import ActionChains


class AutoDemo(object):
    # 存放需要课程信息元素
    course_element = dict()
    # 存放需要是要到的页面句柄
    handles_dict = dict()

    # 初始化方法
    def __init__(self):
        # 创建谷歌驱动
        self.driver = webdriver.Chrome()
        # 打开登录窗口
        self.driver.get(url=xxt_demo.config.Hsot)
        # 最大化浏览器
        self.driver.maximize_window()
        # 初始化等待方法
        self.WebDriverWait = WebDriverWait
        # 初始化鼠标操作
        self.action = ActionChains(self.driver)

    # 登录方法
    def login_page(self):
        self.driver.find_element('css selector', "#phone").send_keys(xxt_demo.config.username)
        self.driver.find_element('css selector', "#pwd").send_keys(xxt_demo.config.password)
        self.driver.find_element('css selector', ".btn-big-blue").click()

    # 获取需要查看课程的元素信息
    def get_course_name(self):
        # 获取页面的句柄并存入到字典中
        self.handles_dict["课程页面"] = self.driver.window_handles[-1]
        # 点击课程进入课程二级标题
        self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
            lambda x: x.find_element('css selector', "#zne_kc_icon")).click()
        # 获取iframe元素
        iframe = self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
            lambda x: x.find_element('xpath', "//iframe"))
        # 切换至iframe页面中
        self.driver.switch_to.frame(iframe)
        # 获取所有课程名
        course = self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
            lambda x: x.find_elements('css selector', ".course-name"))
        # 将所有课程名及元素信息存入字典中
        for i in course:
            if i.text in xxt_demo.config.curriculum_list:
                self.course_element[i.text] = i

    def look_video(self):
        # 根据课程元素进行操作
        for i in self.course_element.values():
            print(f'现在看大课:{i.text}')
            # 点击课程
            i.click()
            # 将新窗口添加到窗口字典中
            self.handles_dict[i.text] = self.driver.window_handles[-1]
            # 切换窗口
            self.driver.switch_to.window(self.handles_dict[i.text])
            # 定位内置元素
            iframe = self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
                lambda x: x.find_element('xpath', "//iframe"))
            # 切换内置元素
            self.driver.switch_to.frame(iframe)
            # 获取课程节点元素列表
            mini_course = self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
                lambda x: x.find_elements('xpath', "//span[@class='catalog_points_yi']"))
            # 循环列表
            if len(mini_course) != 0:
                for i in mini_course:
                    num = len(mini_course)
                    print(f'现在小课还有:{num}')
                    # 点击课程
                    i.click()
                    iframe_0 = self.WebDriverWait(self.driver, timeout=10, poll_frequency=0.5).until(
                        lambda x: x.find_elements('css selector', "#iframe"))
                    # 定位视频课程元素
                    sp_btns = self.driver.find_elements('xpath', '//*[@title="视频"]')
                    # 查看是否有视频课程
                    if sp_btns is not None:
                        # 循环播放视频课程
                        for i in sp_btns:
                            # 点击查看的课程
                            i.click()
                            self.driver.switch_to.parent_frame()
                            js_down = "window.scrollTo(0,500)"
                            self.driver.execute_script(js_down)
                            iframe_1 = self.driver.find_element('xpath', "//div[@class='course_main']/iframe")
                            self.driver.switch_to.frame(iframe_1)
                            iframe_2 = self.driver.find_element('xpath', "//div[@class='ans-attach-ct']/iframe")
                            self.driver.switch_to.frame(iframe_2)
                            self.driver.find_element('partial link text', '知道').click()
                            self.driver.find_element('xpath', '//*[@title="播放视频"]').click()
                            self.driver.find_element('xpath', "//*[@title='静音']").click()
                            while True:
                                time_0 = self.driver.find_element('css selector', '.vjs-duration-display').text
                            	time_1 = self.driver.find_element('css selector', '.vjs-current-time-display').text
                            	time_1 = time_1.split(":")
                            	time_0 = time_0.split(":")
                            	time_1 = int(time_1[0]) * 60 + int(time_1[1])
                            	time_0 = int(time_0[0]) * 60 + int(time_0[1])
                            	wdw_time = time_0 - time_1
                            	print(wdw_time)
                                if time_1 == time_0:
                                    break
                                    print('该视频观看结束')
                                else:
                                    el = self.WebDriverWait(self.driver, timeout=time_0 - time_1,
                                                            poll_frequency=0.5).until(
                                        lambda x: x.find_elements('xpath', "//div[@class='vjs-control-bar']"))
                                    if len(el) == 0:
                                        print('定位不到播放盒子')
                                        continue
                                    else:
                                        el = self.driver.find_elements('xpath', "//*[@title='播放']")
                                        if len(el) == 0:
                                            continue
                                        else:
                                            el[0].click()
                            print('这个小节课程我已经看完了')
                            print(f'现在小课还有:{num - 1}')
                        # 切换会主页面
                        self.driver.switch_to.parent_frame()
                        # 返回上一个页面
                        self.driver.back()
                    else:
                        self.driver.back()
                self.driver.switch_to.window(self.handles_dict["课程页面"])
            else:
                print('你都看完了你还用脚本')
        print('结束啦！')

    def main(self):
        print('现在正在登录')
        self.login_page()
        print('登录完成')
        print('获取需要看的课程元素')
        self.get_course_name()
        print('课程元素获取完毕')
        print('准备去看咯')
        self.look_video()
        print('所有课程已经全部看完')


if __name__ == '__main__':
    ad = AutoDemo()
    ad.main()
```

