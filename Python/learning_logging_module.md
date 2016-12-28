# Python logging 模块
参考
> [Python logging模块详解](http://blog.csdn.net/zyz511919766/article/details/25136485)


## 1. 简单使用：将日志打印到屏幕
```Python
import logging  
logging.debug('debug message')  
logging.info('info message')  
logging.warning('warning message')  
logging.error('error message')  
logging.critical('critical message')  
```
- 默认情况下Python的`logging`模块将日志打印到了标准输出中
- 只显示了大于等于WARNING级别的日志，这说明默认的日志级别设置为`WARNING`
- 日志级别等级：`CRITICAL > ERROR > WARNING > INFO > DEBUG > NOTSET`
- 默认的日志格式为日志级别：`Logger名称：用户输出消息`

## 2. 灵活配置日志级别，日志格式，输出位置
- 使用`logging.basicConfig()`函数

```python
import logging  
logging.basicConfig(level=logging.DEBUG,  
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',  
                    datefmt='%a, %d %b %Y %H:%M:%S',  
                    filename='/tmp/test.log',  
                    filemode='w')  

logging.debug('debug message')  
logging.info('info message')  
logging.warning('warning message')  
logging.error('error message')  
logging.critical('critical message')
```

### 可用参数
- filename：用指定的文件名创建FiledHandler（后边会具体讲解handler的概念），这样日志会被存储在指定的文件中。
- filemode：文件打开方式，在指定了filename时使用这个参数，默认值为“a”还可指定为“w”。
- format：指定handler使用的日志显示格式。
- datefmt：指定日期时间格式。
- level：设置rootlogger（后边会讲解具体概念）的日志级别
- stream：用指定的stream创建StreamHandler。可以指定输出到sys.stderr,sys.stdout或者文件，默认为sys.stderr。若同时列出了filename和stream两个参数，则stream参数会被忽略。

### 可用的格式化字符串
- %(name)s Logger的名字
- %(levelno)s 数字形式的日志级别
- %(levelname)s 文本形式的日志级别
- %(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
- %(filename)s 调用日志输出函数的模块的文件名
- %(module)s 调用日志输出函数的模块名
- %(funcName)s 调用日志输出函数的函数名
- %(lineno)d 调用日志输出函数的语句所在的代码行
- %(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
- %(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
- %(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
- %(thread)d 线程ID。可能没有
- %(threadName)s 线程名。可能没有
- %(process)d 进程ID。可能没有
- %(message)s用户输出的消息

## 3. 组件
logging库提供了多个组件：Logger、Handler、Filter、Formatter。
- Logger对象提供应用程序可直接使用的接口
- Handler发送日志到适当的目的地
- Filter提供了过滤日志信息的方法
- Formatter指定日志显示格式。

### Logger

- Logger是一个树形层级结构，输出信息之前都要获得一个Logger（如果没有显示的获取则自动创建并使用root Logger）
- logger = logging.getLogger()返回一个默认的Logger也即root Logger，并应用默认的日志级别、Handler和Formatter设置。
- 当然也可以通过Logger.setLevel(lel)指定最低的日志级别，可用的日志级别有logging.DEBUG、logging.INFO、logging.WARNING、logging.ERROR、logging.CRITICAL。
- Logger.debug()、Logger.info()、Logger.warning()、Logger.error()、Logger.critical()输出不同级别的日志，只有日志等级大于或等于设置的日志级别的日志才会被输出。
- name与Logger实例一一对应，只要logging.getLogger（name）中名称参数name相同则返回的Logger实例就是同一个

### Handler
- Handler对象负责发送相关的信息到指定目的地，有几个常用的Handler方法：
  - Handler.setLevel(lel):指定日志级别，低于lel级别的日志将被忽略
  - Handler.setFormatter()：给这个handler选择一个Formatter
  - Handler.addFilter(filt)、Handler.removeFilter(filt)：新增或删除一个filter对象

- 有多中可用的Handler，例如
```python
# 用于向一个文件输出日志信息
fh = logging.FileHandler('/tmp/test.log')
# 可以向类似与sys.stdout或者sys.stderr的任何文件对象(file object)输出信息
ch = logging.StreamHandler()
```

- 可以通过addHandler()方法为Logger添加多个Handler：
```python
logger.addHandler(fh)  
logger.addHandler(ch)
```

### Formatter
- Formatter对象设置日志信息最后的规则、结构和内容
- 默认的时间格式为`%Y-%m-%d %H:%M:%S`
```Python
# 定义Formatter  
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')  
# 为Handler添加Formatter  
fh.setFormatter(formatter)  
ch.setFormatter(formatter)
```
- 也可以直接给Logger加Filter。若为Handler加Filter则所有使用了该Handler的Logger都会受到影响。而为Logger添加Filter只会影响到自身。

## 配置文件
参考Python标准库文档
> [Configuration file format](https://docs.python.org/2/library/logging.config.html#configuration-file-format)

## 多模块使用logging
- logging模块保证在同一个python解释器内，多次调用logging.getLogger('log_name')都会返回同一个logger实例，即使是在多个模块的情况下。
- 典型的多模块场景下使用logging的方式是在main模块中配置logging，这个配置会作用于多个的子模块，然后在其他模块中直接通过getLogger获取Logger对象即可。
