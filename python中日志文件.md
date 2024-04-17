# 		python中日志文件

### 日志

- 日志的作用

  ```yacas
  记录程序运行的步骤与错误。
  ```

- 日志的使用场景

  ```yacas
  1、调试bug
  2、查看程序运行的轨迹
  ```

- 日志的基本应用

  ```yacas
  1、导报
  import logging
  2、设置日志信息输出
  logging.日志等级("出错啦,错误原因{}".format(e))
  ```

- 日志底层组成

  ```yacas
  说明:logging库底层有4大组件(日志器、处理器、格式器、过滤器)
  1、日志器:接受日志信息、设置日志显示级别
  2、处理器:控制日志显示位置或文件
  3、格式器:控制日志输出的显示样式
  关系:
  	格式器必须关联处理器
  	处理器必须关联日志器
  ```

- 日志功能封装

  ```python
  import logging.handlers
  import logging
  
  
  def init_log_config(filename=None, when='midnight', interval=1, backup_count=7):
      """
      功能：初始化日志配置函数
      :param filename: 日志文件名
      :param when: 设定日志切分的间隔时间单位
      :param interval: 间隔时间单位的个数，指等待多少个 when 后继续进行日志记录
      :param backup_count: 保留日志文件的个数
      :return:
      """
      # 1. 创建日志器对象
      logger = logging.getLogger()
  
      # 2. 设置日志打印级别
      logger.setLevel(logging.DEBUG)
      # logging.DEBUG 调试级别
      # logging.INFO 信息级别
      # logging.WARNING 警告级别
      # logging.ERROR 错误级别
      # logging.CRITICAL 严重错误级别
  
      # 3. 创建处理器对象
      # 控制台对象
      st = logging.StreamHandler()
      # 日志文件对象
      fh = logging.handlers.TimedRotatingFileHandler(filename,
                                                     when=when,
                                                     interval=interval,
                                                     backupCount=backup_count,
                                                     encoding='utf-8')
  
      # 4. 日志信息格式
      fmt = "%(asctime)s %(levelname)s [%(filename)s(%(funcName)s:%(lineno)d)] - %(message)s"
      formatter = logging.Formatter(fmt)
  
      # 5. 给处理器设置日志信息格式
      st.setFormatter(formatter)
      fh.setFormatter(formatter)
  
      # 6. 给日志器添加处理器
      logger.addHandler(st)
      logger.addHandler(fh)
  ```

  
