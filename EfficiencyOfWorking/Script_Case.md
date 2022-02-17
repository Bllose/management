# 文件处理  
## 整理项目所有接口
**背景**  
微服务A需要交接给其他项目组，但是微服务A与本项目多个微服务有交互，所以不能直接将微服务丢给其他项目。 又因为历史原因，各种需求文档、概要设计等均已经无法获得。所以只能从代码层面，
将数据结构、接口；从测试环境层面，将业务逻辑等 梳理出来，作为交接材料。   
当前针对“接口”进行描述。从技术层面，swagger已经足够方便，但是对于交接并不合适，况且还需要与流程图关联，所以需要生成一个额外的自定义格式的文档。    

**具体执行**  
1. 获取接口yaml文件
2. 通过python脚本直接读取该文件，并转译为yaml对象  

> 首先，直接读取yaml文件， 然后将其转化为 yaml对象。 对于python脚本而言， 分别都只是一行代码的事情。十分方便  

```
In[1]: import yaml
In[2]: target = open(r'C:\my\path\target-program-rest-interface.yaml', encoding = 'UTF-8')
In[3]: datas = yaml.load(target)
```    
```  
<ipython-input-4-22cbac360b27>:1: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  datas = yaml.load(target)
```  
> 工具：Jupyter 或者 PyCharm 都是不错的选择。 直接使用cmd 命令行也OK， 相对没那么方便。

> 从对象中，获取我们需要的内容，并组成自定义格式输出。 用比较方便的工具， 我们可以一边查看对象的接口， 一边写脚本， 一共也就是几行代码的事情， 最终将几百个接口信息瞬间组好格式并输出。
> 我仅仅需要复制粘贴，前后也就5分钟的事情
> 
```
In[8]:for cur in paths:
... :    value = paths.get(cur)
... :    if 'get' in value:
... :        summary = value.get('get').get('summary')
... :        print((cur + '\tget\t' + summary))
... :    elif 'post' in value:
... :        summary = value.get('post').get('summary')
... :        print((cur + '\tpost\t' + summary))
... :        
```  
