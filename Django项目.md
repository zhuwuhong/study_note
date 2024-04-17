# Django项目

## 1.下载Django

```shell
pip3 install Django == 2.0
```

## 2.创建项目

```shell
#1.cd /d 项目存放路径
2. django-admin startproject <project_name> #创建项目
3. django-admin startapp <app_name> #子应用名称
```

## 3.打开项目且配置编译器

使用pycharm打开项目且配置python解释器

![image-20230522214828561](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230522214828561.png)

点击Add Interpreter(添加解释器)选择本地添加解释器

![image-20230522214703183](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230522214703183.png)

## 4.设置数据库

1. 下载依赖

   ```shell
   pip3 install pymysql
   ```

2. 将PyMySQL导入到项目中

   ```python
   #打开Django的工程中同名的目录中的__init__.py文件中添加以下语句
   import pymysql
   pymysql.install_as_MySQLdb()
   ```

3. 在setting.py文件中找到`DATABASES`变量

   ```python
   DATABASES = {
       'default':{
           'ENGINE':'django.db.backends.mysql',
           'HSOT':'本地计算机IP',
           'PROT':3306,
           'USER':'root',
           'PASSWORD':'123456',
           'NAME':'表名'
       }
   }
   ```

4. 注册子应用，在setting.py文件中找到INSTALLED_APPS

   ```python
   '子应用名.apps.类名'
   ```

## 5.生成数据迁移文件并迁移并配置路由

1. 在子应用models文件中创建数据表类

   ```python
   # 创建书本类
   class BookInfo(models.Model):
       # 属性名 = 属性选项名
       # 书名
       name = models.CharField(max_length=10, unique=True, verbose_name='书名')
       # 发布时间
       pub_date = models.DateField(null=True, verbose_name='发布日期')
       # 阅读量
       readcount = models.IntegerField(default=0, verbose_name='阅读量')
       # 评论量
       commentcount = models.IntegerField(default=0, verbose_name='评论量')
       # 是否删除(逻辑删除)
       is_delete = models.BooleanField(default=False, verbose_name='是否删除')
   
       class Meta:
           db_table = 'bookinfo'
   
       def __str__(self):
           return self.name
   
   # 创建人物类，书本类的id为它的外键
   class PeopleInfo(models.Model):
       class Meta:
   
           db_table = 'peopleinfo'
   
       GENDER_CHOICES = [
           (0, 'MAN'),
           (1, 'WOMAN'),
       ]
       """
       default:用于设置默认值
       choices:设置枚举列表
       on_delete:指明主表删除数据时，对于外键引用表数据如何处理，在django.db.models中包含了可选常量：
           CASCADE级联，删除主表数据时连通一起删除外键表中数据
           PROTECT保护，通过抛出ProtectedError异常，来阻止删除主表中被外键应用的数据
           SET_NULL设置为NULL，仅在该字段null=True允许为null时可用
           SET_DEFAULT设置为默认值，仅在该字段设置了默认值时可用
           SET()设置为特定值或者调用特定方法
           DO_NOTHING不做任何操作，如果数据库前置指明级联性，此选项会抛出IntegrityError异常
       """
       #  姓名
       name = models.CharField(max_length=10, verbose_name='姓名')
       #  性别
       gender = models.SmallIntegerField(choices=GENDER_CHOICES, default=0, verbose_name='性别')
       #  人物描述
       description = models.TextField(default='', verbose_name='描述', null=True)
       #  人物出处
       book = models.ForeignKey(BookInfo, on_delete=models.CASCADE, verbose_name='书籍')
       #  是否被删除
       is_delete = models.BooleanField(default=False, verbose_name='是否删除')
   
       def __str__(self):
           return self.name
   ```

2. 生成数据迁移文件，并完成迁移

   ```shell
   # 生成迁移文件
   python .\manage.py makemigrations
   # 完成迁移
   python .\manage.py migrate
   ```

3. 插入数据

   ```sql
   
   insert into bookinfo(name, pub_date, readcount,commentcount, is_delete) values
   ('射雕英雄传', '1980-5-1', 12, 34, 0),
   ('天龙八部', '1986-7-24', 36, 40, 0),
   ('笑傲江湖', '1995-12-24', 20, 80, 0),
   ('雪山飞狐', '1987-11-11', 58, 24, 0);
   
   insert into peopleinfo(name, gender, book_id, description, is_delete)  values
       ('郭靖', 1, 1, '降龙十八掌', 0),
       ('黄蓉', 0, 1, '打狗棍法', 0),
       ('黄药师', 1, 1, '弹指神通', 0),
       ('欧阳锋', 1, 1, '蛤蟆功', 0),
       ('梅超风', 0, 1, '九阴白骨爪', 0),
       ('乔峰', 1, 2, '降龙十八掌', 0),
       ('段誉', 1, 2, '六脉神剑', 0),
       ('虚竹', 1, 2, '天山六阳掌', 0),
       ('王语嫣', 0, 2, '神仙姐姐', 0),
       ('令狐冲', 1, 3, '独孤九剑', 0),
       ('任盈盈', 0, 3, '弹琴', 0),
       ('岳不群', 1, 3, '华山剑法', 0),
       ('东方不败', 0, 3, '葵花宝典', 0),
       ('胡斐', 1, 4, '胡家刀法', 0),
       ('苗若兰', 0, 4, '黄衣', 0),
       ('程灵素', 0, 4, '医术', 0),
       ('袁紫衣', 0, 4, '六合拳', 0);
   ```

4. 添加视图

   ```python
   # 创建视图方法 在子应用中views文件中创建
   def index(request):
       return HttpResponse("Hello, world. You're at the index page.")
   # 添加子应用路由，在子应用路径下创建一共urls.py文件
   from django.urls import re_path
   from book.views import index
   
   urlpatterns = [
       re_path(r'^index/$', index),
   ]
   # 在主应用路径下创建访问子应用的路由
   from django.contrib import admin
   from django.urls import path, re_path, include
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       re_path(r'^book/', include('book.urls')),
   ]
   ################reverse动态获取路由地址
   # 在子应用中的路由设置name属性
   urlpatterns = [
       re_path(r'^index/', index, name='index'),
   ]
   # 这样就可以在views中使用serverse方法获取路由地址
   def index(request):
       print(reverse('index')) #/book/index/
       return HttpResponse('Hello, world. You\'re in the index page.')
   ###############为了防止多子应用之间都有同一个页面因此可以在子应用的urls文件中设置app_name这样就可以防止出现这个问题
   app_name = 'book'
   urlpatterns = [
       re_path(r'^index/', index, name='index'),
   ]
   def index(request):
       print(reverse('book:index')) #/book/index/
       return HttpResponse('Hello, world. You\'re in the index page.')
   # 但是需要注意的是如果还使用index去获取路由的话会出现报错噢!
   ```

5. 路由访问效果

![image-20230522225107690](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230522225107690.png)

## 6.HttpRequest对象

1. 获取URL路径参数

   - 如果想从URL中获取值，则需要在正则中提取数据

   - 获取值的两种方式

     - 位置参数

       - 此参数的位置不能错

         ```python
         # 应用中urls
         re_path(r'^(\d+)/(\d+)/$'),views.index)
         # 视图中函数，参数的位置不能错
         def index(request,value1,value2):
             context={'v1':value1,'v2':value2}
             # 按照路径传递参数
             reverse('book:index',args=(value1,value2))
             return render(request,'Book/index.html',context)
         ```

         

     - 关键字参数

       - 参数位置可变，组名与关键字保持一致

         ```python
         # 应用中urls
         re_path(r'^(?P<value1>\d+)/(?P<value2>\d+)/$', views.index),
         # 视图中函数，参数的位置可以改变
         def index(request, value2, value1):
               context = {'v1':value1, 'v2':value2}
                 # 按照路径传递参数
             reverse('book:index',args=(value1,value2))
               return render(request, 'Book/index.html', context)
         ```

2. 获取请求方法携带的参数

   - get方法

   - 使用request.GET方法获取数据

     - 返回的是一一个QueryDict类型数据

     - 当想获取一键一值的时候使用字典获取数据方法即可，但是当某个数据为多值则默认获取最后一个数据

     - 当想获取一键多值的时候则使用getlist方法获取数据，获取到的则是一个列表数据

       ```python
       #请求数据 http://127.0.0.1:8000/book/index/oo/?username=admin&password=123
       request.GET # <QueryDict: {'username': ['admin'], 'password': ['123']}>
       request.GET["username"],request.GET["password"] #'admin', '123'
       #请求数据 http://127.0.0.1:8000/book/index/oo/?username=admin&password=123&username='root'
       request.GET # <QueryDict: {'username': ['admin', "'root'"], 'password': ['123']}>
       request.GET["username"],request.GET["password"] # ("'root'", '123')
       request.GET.getlist('username') #['admin', 'root']
       ```

   - post方法
   
   - 使用request.POST获取数据
   
     - 返回的是一一个QueryDict类型数据
   
     - 当想获取一键一值的时候使用字典获取数据方法即可，但是当某个数据为多值则默认获取最后一个数据
   
     - 当想获取一键多值的时候则使用getlist方法获取数据，获取到的则是一个列表数据
   
       与get使用方法几乎一致(传递的为表单格式)
   
       非表单格式需要从使用request.body方法获取传输信息

## 7.HttpResponse对象

1. HttpResponse

   - 可以使用django.http.HttpResponse来构造响应对象

     ```python
     HttpResponse(content=响应体, content_type=响应体数据类型, status=状态码)
     ```

   - 响应头可以直接将HttpResponse对象当作字典进行响应头键值对的设置：

     ```python
     response = HttpResponse()
     response['username'] = 'admin' # 自定义响应头username，值为admin
     ```

2. HttpResponse子类

   - Django提供了一系列HttpResponse的子类，可以快速设置状态码
     - HttpResponseRedirect 301
     - HttpResponsePermanentRedirect 302
     - HttpResponseNotModified 304
     - HttpResponseBadRequest 400
     - HttpResponseNotFound 404
     - HttpResponseForbidden 403
     - HttpResponseNotAllowed 405
     - HttpResponseGone 410
     - HttpResponseServerError 500

3. JsonResponse

   - 若要返回json数据，可以使用JsonResponse来构造响应对象帮助我们将数据转换为json字符串，并且将响应头设置为`Content-Type`为`application/json`

     ```python
     from django.http import JsonResponse
     
     def response_data(request):
     	return JsonResponse({'city':'beijing'})
     ```

4. redirect重定向

   - redirect可以将次页面重定向到指定路径页面

     ```python
     from django.shortcuts import redirect
     # 将访问此页面中的请求重定向到另一个页面
     def response_data(request):
         return redirect(reverse('book:index'))
     ```

## 8状态保持

1. Cookie

   - Cookie以键值对的格式进行信息存储。
   - Cookie基于域名安全，不同的域名的Cookie是不能相互访问的
   - 当浏览器请求某网址时，会将浏览器存储的与网站相关的所有Cookie信息提交给网站服务器

   - 设置Cookie，通过HttpResponse对象中的`set_cookie`方法来设置cookie。

     ```python
     # max_age单位为秒，默认为None。如果时零时的cookie，可将max_age设置为None
     def SetCookie(request):
         response = HttpResponse('ok')
         response.set_cookie('username','admin') # 零时cookie
         response.set_ccokie('username1','root',max_age=3600)# 有效期一小时
         return response
     ```

   - 获取Cookie，可以通过**HttpResponse**对象的**COOKIES**属性来读取本次请求携带的cookie值。**request.COOKIES为字典类型**。

     ```python
     def cookie(request):
         cookie1 = request.COOKIES.get('itcast1')
         print(cookie1)
         return HttpResponse('OK')
     ```

   - 删除Cookie，可以通过HttpResponse对象中的delete.cookie方法来删除

     ```python
     # 将响应中的cookie名为'username1'的cookie删除
     response.deletc.cookie('username1')
     ```

2. Session

   - Session原理
   - 1.客户端发送带有用户信息的post请求发送给服务器，服务器验证信息
   - 2.将用户对象放入到session存放到session的内存中，生成一个sessionid对应session
   - 3.将sessionid存放在cookie中
   - 4.客户端后续的请求中的cookie携带着sessionid，发送给服务器
   - 5.服务器根据sessionid从内存中获取用户的信息
   - 6.返回请求响应信息

   1. ![image-20230526000120807](C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230526000120807.png)