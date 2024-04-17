# 【pymysq】python之pymysql学习笔记

### 一、简介与安装

##### 1.1 简介：

```
		PyMySQL是在 Python3.x 版本中用于连接 MySQL 服务器的一个库，用来对mysql数据库进行操作。
```

##### 1.2 安装：使用pip方式进行安装，输入以下命令

```
pip3 install pymysql
```

### 二、使用mysql进行增、删、改、查

##### 2.1 对mysql进行增、删、改操作

需求如下，增加第5条记录，修改第三条记录，删除第四条记录，如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200503111832750.png)

```python
import pymysql
def mysql_action():
    # 创建连接
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='123456', db='dbtest1', charset='utf8')
    # 创建游标
    cursor = conn.cursor()

    # 新增新的记录
    add_sql="insert into knlg_baseinfo \
            (knlg_id,knlg_title,knlg_desc,knlg_content,knlg_category,create_time,update_time) \
            values ('5', '理财标题', '理财摘要', '理财内容', 'financial', now(),now());"
    #修改记录
    update_sql="update knlg_baseinfo set knlg_title='如何理财3' where knlg_id='%s'" % ('3',)

    #删除记录
    delete_sql="delete from knlg_baseinfo where knlg_id='%s' and knlg_category='%s';" % ('4','financial')


    effect_row = cursor.execute(add_sql)
    effect_row = cursor.execute(update_sql)
    effect_row = cursor.execute(delete_sql)

    # 提交，不然无法保存新建或者修改的数据
    conn.commit()

    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()

mysql_action()
```

##### 2.2 基本查询操作，

获取查询结果的第一行数据 ： row_1 = cursor.fetchone()
获取剩余结果前n行数据： row_2 = cursor.fetchmany(2)
获取所有记录： row_3 = cursor.fetchall()
带参数查询 ： query_sql2=“select * from knlg_baseinfo where knlg_id=’%s’ and knlg_category=’%s’;”%(‘6’,‘financial’)
默认查询结果返回的是元祖类型：如下
(‘6’, ‘理财标题’, ‘理财摘要’, ‘理财内容’, ‘financial’, datetime.datetime(2020, 5, 3, 11, 27, 39), datetime.datetime(2020, 5, 3, 11, 27, 39))
具体代码如下：

```python
import pymysql

def query():
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='123456', db='dbtest1', charset='utf8')
    cursor = conn.cursor()
    query_sql1="select * from knlg_baseinfo;"
    query_sql2="select * from knlg_baseinfo where knlg_id='%s' and knlg_category='%s';"%('6','financial')
    cursor.execute(query_sql2)

    # 获取查询结果的第一行数据
    row_1 = cursor.fetchone()
    print(row_1)

    # 获取剩余结果前n行数据
    # row_2 = cursor.fetchmany(3)

    # 获取剩余结果所有数据
    # row_3 = cursor.fetchall()

    conn.commit()
    cursor.close()
    conn.close()

query()
```

##### 2.3 查询结果以字典形式返回：

步骤：将游标设置为字典类型即可 cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050314233816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTU4OTcxMw==,size_16,color_FFFFFF,t_70)

{‘knlg_id’: ‘6’, ‘knlg_title’: ‘理财标题’, ‘knlg_desc’: ‘理财摘要’, ‘knlg_content’: ‘理财内容’, ‘knlg_category’: ‘financial’, ‘create_time’: datetime.datetime(2020, 5, 3, 11, 27, 39), ‘update_time’: datetime.datetime(2020, 5, 3, 11, 27, 39)}

```python
import pymysql
def query():
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='123456', db='dbtest1', charset='utf8')
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    query_sql1="select * from knlg_baseinfo;"
    query_sql2="select * from knlg_baseinfo where knlg_id='%s' and knlg_category='%s';"%('6','financial')
    query_sql3="select knlg_id,knlg_title,knlg_desc,knlg_content,knlg_category, \
                cast(create_time as char) as create_time,cast(update_time as char) as update_time from knlg_baseinfo where knlg_id='%s' and knlg_category='%s';"%('6','financial')
    cursor.execute(query_sql3)

    # 获取查询结果的第一行数据
    row_1 = cursor.fetchone()
    '''
    {'knlg_id': '6', 'knlg_title': '理财标题', 'knlg_desc': '理财摘要',
     'knlg_content': '理财内容', 'knlg_category': 'financial',
      'create_time': '2020-05-03 11:27:39', 'update_time': '2020-05-03 11:27:39'}

    '''
    print(row_1)

    # 获取剩余结果前n行数据
    # row_2 = cursor.fetchmany(3)

    # 获取剩余结果所有数据
    #row_3 = cursor.fetchall()
    #print(row_3)

    conn.commit()
    cursor.close()
    conn.close()

query()
```

### 三、关于pymysql防注入 （参考： [明天OoO你好 ](https://www.cnblogs.com/wt11/p/6141225.html)）

##### 3.1 字符串拼接查询，造成注入

正常语句:

```
user="u1"
passwd="u1pass"
#正常构造语句的情况
sql="select user,pass from tb7 where user='%s' and pass='%s'" % (user,passwd)
#sql=select user,pass from tb7 where user='u1' and pass='u1pass'
row_count=cursor.execute(sql) row_1 = cursor.fetchone()
```

构造注入语句:

```
user="u1' or '1'-- "
passwd="u1pass"
sql="select user,pass from tb7 where user='%s' and pass='%s'" % (user,passwd)
 
#拼接语句被构造成下面这样，永真条件，此时就注入成功了。因此要避免这种情况需使用pymysql提供的参数化查询。
#select user,pass from tb7 where user='u1' or '1'-- ' and pass='u1pass'
 
row_count=cursor.execute(sql)
row_1 = cursor.fetchone()
```

##### 3.2 避免注入，使用pymysql提供的参数化语句

正常参数化查询:

```
user="u1"
passwd="u1pass"
#执行参数化查询
row_count=cursor.execute("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
row_1 = cursor.fetchone()
```

构造注入，参数化查询注入失败:

```
user="u1' or '1'-- "
passwd="u1pass"
#执行参数化查询
row_count=cursor.execute("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
#内部执行参数化生成的SQL语句，对特殊字符进行了加\转义，避免注入语句生成。
# sql=cursor.mogrify("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
# print sql
#select user,pass from tb7 where user='u1\' or \'1\'-- ' and pass='u1pass'被转义的语句。
 
row_1 = cursor.fetchone()
```

##### 结论：excute执行SQL语句的时候，必须使用参数化的方式，否则必然产生SQL注入漏洞。

### 四、使用with简化连接过程

每次都连接关闭很麻烦，使用上下文管理，简化连接过程

```python
import pymysql
import contextlib

#定义上下文管理器，连接后自动关闭连接
@contextlib.contextmanager
def contomysql(host='127.0.0.1', port=3306, user='root', passwd='123456', db='dbtest1',charset='utf8'):
    conn = pymysql.connect(host=host, port=port, user=user, passwd=passwd, db=db, charset=charset)
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    try:
        # 先把yield看做 return，然后看做是生成器（generator）
        yield cursor
    finally:
        conn.commit()
        cursor.close()
        conn.close()

# 执行sql
with contomysql() as cursor:
  print(cursor)
  row_count = cursor.execute("select * from knlg_baseinfo;")
  row_1 = cursor.fetchone()
  print(row_count)
  print(row_1)
```

以上是我参考资料做的一个学习笔记，希望对大家学习或使用python有一定的帮助，也欢迎大家在评论区给出建议！