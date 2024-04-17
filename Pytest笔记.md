# Pytest学习笔记

## 1.安装pytest

```shell
pip install pytest
```

## 2.执行pytest代码

```shell
pytest 文件路径
```

```、
点击三角号进行运行
```

```shell
pytest 文件路径 #指定路径下的文件
pytest  #当前路径下的所有文件
```

## 3.配置文件

>在pytest中有一个配置文件可以直接配置pytest的运行
>
>​	pytest.ini文件

```ini
[pytest]
testpaths = ./ #指定当前路径下所有的文件
```

## 4.setup/teardown

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230529000831965.png" alt="image-20230529000831965" style="zoom:200%;" />

## 5.fixture的使用

> fixtue时pytest用于将测试前后进行预备或清理工作的代码处理机制
>
> fixture相对于setup和teardown来说更加灵活
>
> conftest.py配置里可以实现数据共享，不需要import就能自动找到一些配置

<img src="C:\Users\朱五红\AppData\Roaming\Typora\typora-user-images\image-20230529001509144.png" alt="image-20230529001509144" style="zoom:200%;" />

```python
#参数了解
scop #为作用域
autouse #为当前文件里的所有方法自动执行
```

## 6.yaml语法

```yaml
key:
	child-key:value
	child-key2:value2
#{'key':{'child-key':value,'child-key2':value2}}
key:
	-a
	-b
	-c
#{'key':[a,b,c]}
key:
	- child-key:value
	  child-key2:value2
# {'key':[{'child-key':'value','child-key2':'value2'}]}
-
  -
	-a
	-b
	-c
#[[a,b,c]]
```

