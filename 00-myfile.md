# 一、Pycharm

1. 写模板文件时用模板标签不能自动补全

解决：

![image-20191121203659520](C:\Users\RUAN\AppData\Roaming\Typora\typora-user-images\image-20191121203659520.png)

2. ![image-20191124001406090](C:\Users\RUAN\AppData\Roaming\Typora\typora-user-images\image-20191124001406090.png)

解决：重新配置解释器

3. /home/pyvip/.virtualenvs/py3env_django/bin/python3.6: can't open file '/home/pyvip/桌面/pytest/test2/home/pyvip/桌面/pytest/test1/manage.py': [Errno 2] No such file or directory

解决：

# 二、vscode

关于Visual studio code/power shell中无法使用virtualenv

解决：先以管理员身份运行window Poweroff，接着执行以下命令后输入Y同意即可

```shell
 Set-ExecutionPolicy RemoteSigned 
```

### 15款常用插件

| 插件名                | 作用                                        |
| :-------------------- | ------------------------------------------- |
| Chinese               | 英文转中文                                  |
| open in browser       | 浏览器打开                                  |
| guides                | 显示代码对齐辅助线                          |
| HTMLHint              | html代码检测，支持html5                     |
| vscode-icons          | 根据文件文件夹显示不同的图标                |
| JS-CSS-HTML Formatter | 每次保存，都会自动格式化js  css 和html 代码 |
| Import Cost           | 在行尾显示导入包的大小                      |
| Auto Rename Tag       | 自动重命名配对的HTML / XML标签              |
| CSS Peek              | 追踪至样式                                  |
| path Intellisense     | 路径提示                                    |
| Prettier              | 每次保存，都会自动格式化js  css 和html 代码 |
| Browser Preview       | 网页预览                                    |
| Live Server           | 开启本地服务器                              |
| Vetur                 | Vue文件语法高亮                             |
|                       |                                             |

# python

- 版本问题：django2.1不再支持mysql5.5，必须是mysql5.6以上

  - 解决：https://blog.csdn.net/devcloud/article/details/108059528?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~first_rank_v2~rank_v25-1-108059528.nonecase&utm_term=mysql%E5%92%8Cdjango%E7%9A%84%E7%89%88%E6%9C%AC

  - Django降级到2.0

    - 查看Django版本：

      ```python
      import django
      django.get_version()  # '2.1.4'
      # 或者
      django.VERSION  # (2, 1, 4, 'final', 0)
      ```

  - mysql升级5.5以上
    - 查看mysql版本：
      - 进入mysql会显示mysql版本，或进入mysql后执行select version()
      - mysql --version
    - 

- 获取当前python解释器路径

  - ```python
    # cmd进入python
    import sys
    sys.executable
    
    # 获取全局python解释器路径
    >where python
    ```

- 判断文件夹或文件是否存在

  ```python
  # 如果你要确定他是文件还是目录，从 Python 3.4 开始可以使用 pathlib 模块提供的面向对象的方法 (Python 2.7 为 pathlib2 模块):
  from pathlib import Path
  
  my_file = Path("/path/to/file")
  if my_file.is_file():
      # 指定的文件存在
  # 检测是否为一个目录：
  if my_file.is_dir():
      # 指定的目录存在
  ```


- python简单删除目录下文件以及文件夹
  ```python
  #Python简单删除目录下文件以及文件夹
  import os
  import shutil
  filelist=[]
  rootdir=r"D:\ALL\img"                       #选取删除文件夹的路径,最终结果删除img文件夹
  filelist=os.listdir(rootdir)                #列出该目录下的所有文件名
  for f in filelist:
      filepath = os.path.join( rootdir, f )   #将文件名映射成绝对路劲
      if os.path.isfile(filepath):            #判断该文件是否为文件或者文件夹
          os.remove(filepath)                 #若为文件，则直接删除
          print(str(filepath)+" removed!")
      elif os.path.isdir(filepath):
          shutil.rmtree(filepath,True)        #若为文件夹，则删除该文件夹及文件夹内所有文件
          print("dir "+str(filepath)+" removed!")
  shutil.rmtree(rootdir,True)                 #最后删除img总文件夹
  print("删除成功")
  ```

- python用时间戳生成不重复随机hash值函数
  ```python
  # 随机字符串
  def md5():
      m = hashlib.md5(str(time.time()).encode())
      return m.hexdigest()
  ```


## jupyter notebook

快捷键：

- 插入cell：a,b
- 删除cell：x
- 执行cell：shift+enter/ctrl+enter
- 切换cell模式：m,y
- cell执行后，在cell左侧双击就可以回到cell的可编辑模式
- 执行结果收回：在执行结果左侧双击即可
- 打开帮助文档：shift+tab
- tab：自动补全
- 撤销：z

## python爬虫

- 什么是爬虫：编写程序，模拟浏览器上网，在互联网爬取网站数据
  - 模拟：浏览器就是一个纯天然最原始的爬虫工具
  - 爬取：
    - 爬取一整张的源码数据
    - 爬取一整张页面中的局部数据

- 爬虫的分类：

  - 通用爬虫
    - 要求我们爬取一整张页面源码数据
  - 聚焦爬虫
    - 要求爬取一张页面中的局部的数据
      - 聚焦爬虫一定是建立在通用爬虫的基础之上
  - 增量式爬虫
    - 用来监测网站数据更新的情况，以便爬取到网站最新更新出来的数据。
  - 分布式爬虫
    - 提高爬取效率的终极武器。

- 10种反爬机制

  - 1.robots
    - 是一个纯文本的协议，协议中规定了该网站中哪些数据可以被哪些爬虫爬取，哪些数据不可以被爬取
  - 2.UA检测
    - 网站后台会检测请求对应的User-Agent，以判定当前请求是否为异常请求。
  - 3.动态加载数据的捕获
  - 4.图片懒加载
  - 5.cookie
    - 是存储在客户端的一组键值对
    - web中cookie的典型应用
      - 免密登录
    - cookie与爬虫的关联
      - 有时候，请求页面不携带cookie的话，那么无法请求到正确的页面数据，因此cookie是爬虫中一个非常典型常见的反爬机制
  - 6.高频访问时封ip

- 10种反反爬机制

  - 1.主观不遵从协议

  - 2.UA伪装

    - 从浏览器捕获User-Agent的值，将其伪装到字典中，作用到程序请求中

  - 3.抓包

  - 4.爬取src2缩略图

  - 5.cookie的处理方式

    - 方式1：手动处理
      - 将抓包工具中的cookie粘贴在headers中
      - 弊端：cookie如果过了有效时长则该方式失效

    - 方式2：自动处理
      - 基于Session对象实现自动处理。
      - 如何获取一个session对象：requests.Session()返回一个session对象。
      - session对象的作用
        - 该对象可以向requests一样调用get和post发起指定的请求。只不过如果在使用session发请求的过程中如果产生了cookie，则cookie会自动存储到该session对象中，那么就意味着下次再次使用session对象发起请求，则该次请求就是携带cookie进行的请求发送
      - 在爬虫中使用session的时候，session对象至少被使用几次？
        - 两次

  - 6.代理使用

    - 在爬虫中，所谓代理指定是什么？
      - 就是代理服务器
    - 代理服务器的作用是什么？
      - 就是用来转发请求和响应。
    - 在爬虫中为什么需要使用代理服务器
      - 如果我们使用爬虫短时间内对服务器发起高频请求，那么服务器就会检测到这样的一个异常的行为请求，就是将该请求对应设备的ip禁掉，这样client设备就无法对服务器再次发起请求(ip被禁掉了)
      - 如果ip被禁，我们就可以使用代理服务器进行请求转发，破解ip被禁的反爬机制。因此使用代理后，服务器端接收到的请求对应的ip地址就是代理服务器而不是我们真正客户端的。
    - 代理服务器分为不同的匿名度：
      - 透明代理：服务端知道你使用代理以及知道你的ip
      - 匿名代理：知道你使用代理，不知道你的ip
      - 高匿名代理：不知道你使用代理也不知道你的真实ip
    - 代理的类型
      - https：只能转发https请求
      - http：转发http请求
    - 代理服务器
      - 快代理
      - 西祠代理
      - goubanjia
      - 代理精灵(推荐) http://www.jinglingdaili.com/

- 思考：基于抓包工具进行全局搜索不一定可以每次都能定位到动态加载数据对应的数据包？

- 原因：如果数据动态加载的数据是经过加密的密文数据。

- ## 验证码的识别

  - 基于线上的打码平台识别验证码
  - 打码平台
    - 1.超级鹰(使用) http://www.chaojiying.com/
      - 注册【用户中心的身份】
      - 登录【用户中心的身份】
        - 1.查询余额，请充值
        - 2.创建一个软件ID（912054）
        - 3.下载示例代码
    - 2.云打码
    - 3.打码兔

### 1.requests

- 爬虫中一个基于网络请求的模块

- pip install requests

- 作用：模拟浏览器发起请求

- 编码流程：

  - 1.指定url
  - 2.发起请求
  - 3.获取响应数据（爬取到的页面源码数据）
  - 4.持久化存储

  ```python
  import requests
  url = 'www.baidu.com'
  headers = {
      'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Safari/537.36'
  }
  response = requests.get(url=url, headers=headers)
  page_text = response.text
  with open('baidu.html', 'w', encoding="utf-8") as fp:
      fp.write(page_text)
  
  ```

- 数据解析：

  - 1.正则

    - 单字符

      - `.`：除换行以外所有字符
      - `[]`：[aoe] [a-w]匹配集合中的任意一个字符
      - `\d`：数字[0-9]
      - `\D`：非数字
      - `\w`：数字、字母、下划线、中文
      - `\W`：非\w
      - `\s`：所有的空白字符包括空格、制表符、换行符等等[\f\n\r\t\v]
      - `\S`：非空白

    - 数量修饰

      - `*`：任意多次 >=0
      - `+`：至少一次 >=1
      - `?`：可有可无
      - `{m}`：固定多次
      - `{m,}`：至少m次
      - `{m,n}`：m-n次

    - 边界

      - `$`：以某某开头
      - `^`：以某某结束

    - 分组：(ab)

    - 贪婪模式：`.*`

    - 非贪婪模式：`.*?`

      ```python
      import re
      ex = '' # 正则表达式
      re.findall(ex, 匹配字符, 修饰符去除换行回车re.S) # 返回列表
      ```

      

  - bs4

    - 解析原理
      - 实例化一个BeautifulSoup的对象，且将待解析的页面源码加载到该对象中。
      - 调用BeautifulSoup对象中相关方法或者属性进行标签定位和文本数据的提取
    - 环境安装
      - pip install lxml # 解析器
      - pip install bs4
    - BeautifulSoup对象的实例化
      - BeautifulSoup(fp, 'lxml')：打开本地文件
      - BeautifulSoup(page_text, 'lxml')：互联网页面源码数据
    - 标签定位
      - soup.tagName：只可以定位到第一次匹配到的标签
      - soup.find('tagName', attrName='value')：属性定位
      - soup.findAll：跟find一样用作属性定位，只不过findAll返回的是列表
      - soup.select('选择器')：
        - 类选择器
        - id选择器
        - 层级选择器
          - `>`：一层
          - 空格：多层
    - 取数据
      - `.text`：返回该标签下所有的文本内容
      - `.string`：返回直属标签的文本内容
    - 取属性
      - tag['attrName']

  - xpath

    - 环境安装
      - pip install lxml
    - 解析原理：html标签是以树状的形式进行展示
      - 1.实例化一个etree的对象，且将待解析的页面源码数据加载到该对象中
      - 2.调用etree的xpath方法结合着不同的xpath表达式实现标签的定位和数据获取
    - 实例化etree对象
      - etree.parse('filename')：本地文件
      - etree.HTML(page_text)：网站页面源码
    - 标签定位
      - 最左侧的/：如果xpath表kait达式最左侧是以/开头则表示该xpath表达式一定要从根标签开始定位指定标签(忽略)
      - 非左侧的/：表示一个层级
      - 非左侧的//：表示多个层级
      - 最左侧的//：xpath表达式可以从任意位置进行标签定位
      - 属性定位：tagName[@class="value"]
      - 索引定位：tag[index]：索引是从1开始
      - 模糊匹配
        - //div[contains(@class,"ng")]
        - //div[starts-with(@class, "ta")]
    - 取文本
      - /text：直系文本内容
      - //text：所有文本内容
    - 取属性
      - /@attrName

  

  - 4.pyquery(自学)

### 2.selenium

- 概念：基于浏览器自动化的模块

- 自动化：可以通过代码指定一些列的行为动作，然后将其作用到浏览器中。

- pip install selemiun

- selemiun与爬虫之间的关联

  - 1.便捷的捕获任意形式动态的数据（可见即可得）
  - 2.实现模拟登录

- 谷歌驱动下载2.4以上：http://chromedriver.storage.googleapis.com/index.html

- 实例化一个浏览器对象

- 编写基于浏览器自动化的操作代码

  - 发起请求：get(url)
  - 标签定位：find系列方法
  - 标签交互：send_keys('xxx')
  - 执行js程序：excute_script('jscode')
  - 前进、后退：back()、forward()
  - js注入：execute_script(jscode)
  - 关闭浏览器

- selenium处理iframe

  - 如果通过find函数进行定位，元素在iframe下则会定位失败
  - 解决方案：使用switch_to.frame(id)即可
  - 动作链（拖动）：from selenium.webdriver import ActionChains
    - 实例化一个动作链对象：action = ActionChains(browser)
    - click_and_hold(div)：长按且点击操作
    - move_by_offset(x, y)：移动的距离
    - perform()：让动作立即执行
    - action.release()释放动作链对象

- selenium捕获动态数据

  - page_source

- selenium的弊端

  - 效率低

- #### 动作链ActionChains

  - 动作链：一系列连续的动作(滑动的动作)
  - 实现滑动：https://www.runoob.com/try/try.php?filename=jqueryui-api-droppable

- 如何让selenium规避检测？

  - 有的网站会检测请求是否为selenium发起，如果是的话则会让请求失败

  - 规避方法

    - selenium接管chrome浏览器

    - 实现步骤

      - 1.必须将你电脑安装的谷歌浏览器的驱动程序所在的目录找到，且将目录添加到环境变量中。
      - 2.打开cmd，在命令行输入：
        - chrome.exe --remote-debugging-port=9222 --user-data-dir="一个空文件夹"
      - 3.执行下列代码

      ```python
      from selenium import webdriver
      from selenium.webdriver.chrome.options import Options
      chrome_options = Options()
      chrome_options.add_experimental_option("debuggerAddress", "127.0.0.1:9222")
      # 本机装好谷歌的驱动程序路径
      chrome_driver = 'c:/'
      driver = webdriver.Chrome(executable_path=chrome_driver, chrome_options=chrome_options)
      print(driver.title)
      
      ```

- 无头浏览器

  - 谷歌无头浏览器(推荐)
  - phantomJs

  ```python
  from selenium import webdriver
  from selenium.webdriver.chrome.options import Options
  from time import sleep
  chrome_options = Options()
  chrome_options.add_argument('--headless')
  chrome_options.add_argument('--disable-gpu')
  browser = webdriver.Chrome(executable_path="./chromedriver", chrome_options=chrome_options)
  # 上网
  url = 'www.baidu.com'
  browser.get(url=url)
  sleep(3)
  browser.save_screenshot('baidu.png')
  browser.quit()
  
  ```

  

# MySQL

- 安装：
  - mysql 5.7 压缩包安装教程：https://www.cnblogs.com/misscai/p/11026987.html
  - mysql 5.7.24 安装包安装教程：https://blog.csdn.net/weixin_44051608/article/details/85163823
  
- 查看MySQL服务是否启动：
  - windows：
    - 键盘上按：win（就是那个旗帜图案的按键）+R，弹出框中输入：services.msc，会弹出服务窗口，在窗口中查找mysql项即可
  - linux： service mysqld status
  
- 启动MySQL服务(管理员方式启动)：
  
- mysql的bin目录下打开cmd，命令 net start mysql （对应的服务关闭命令为 net stop mysql） 
  
- 禁用MySQL服务：` sc delete mysql `

- 删除MySQL服务：`mysqld --remove`

- 安装MySQL服务：`mysqld --install`

- 初始化：`mysqld initialize`

- 设置密码(可以设置空密码)： mysql> set password for 用户名@localhost = password('123'); 

- 删除MySQL空用户登陆功能：

  ```mysql
  /*为了安全考虑，需要删除这个功能，可以登录进去mysql，删除掉*/
  
  mysql>use mysql;
  
  mysql>delete from user where user='';
  
  mysql>flush privileges; (必须的)
  ```

- 新装MySQL首次执行sql语句问题：` You must reset your password using ALTER USER statement before executing this statement.`

  - 解决方式如下：

    MySQL版本5.7.6版本以前用户可以使用如下命令：

    ```mysql
    mysql> SET PASSWORD = PASSWORD('Xiaoming250'); 
    ```

    MySQL版本5.7.6版本开始的用户可以使用如下命令：

    ```mysql
    mysql> ALTER USER USER() IDENTIFIED BY 'Xiaoming250';
    ```

### 编码问题

```csharp
1.查看数据库编码格式
show  create  database  <数据库名>;

2.查看数据表的编码格式
show  create  table  <表名>;

3.创建数据库时指定数据库的字符集
create  database  <数据库名>  character  set  utf8;

4.创建数据表时指定数据表的编码格式
create table tb_books(
    name  varchar(45) not  null,
    price  double  not  null,
    bookCount  int  not  null,
    author  varchar(45)  not  null) default  charset = utf8;

5.修改数据库的编码格式
alter  database  <数据库> character  set  utf8;

6.修改数据表格编码格式
alter  table  <表名> character  set  utf8;

7.修改字段编码格式
alter  table <表名>  change  <字段名>  <字段名>  <类型>  charset  set  utf8;
alter table tb_books change name name varchar(20) character  set  utf8 not null;
```

# Django

- 数据库表重建流程
  -  1.在数据库中删除对应的表 
  -  2.删除表django_migrations中要删除表所在项目的记录 
  -  3.删除表所在项目migrations目录下除init.py外的所有python文件 
  -  4.重新执行数据库迁移命令 

- 单张图片上传

  -  1.修改配置文件DjangoFileUpload/settings.py 

  ```python
  MEDIA_URL = '/media/'
  MEDIA_ROOT = os.path.join(BASE_DIR, 'media').replace('\\', '/')    # media即为图片上传的根路径
  
  ```

  - 2.添加表模型FileUpload/models.py 

  ```python
  from django.db import models
   
  class Img(models.Model):
      img_url = models.ImageField(upload_to='photos/',blank=True,null=True) #指定图片上传路径，即media/photos/
  
  ```

  -  3.数据迁移 
    - python manage.py makemigrations
    - python manage.py migrate
  - 4.增加图片上传的路由 DjangoFileUpload/urls.py 

  ```python
  from django.contrib import admin
  from django.urls import path
  from fileUpload import views
   
  urlpatterns = [
      path('admin/', admin.site.urls),
      path(r'uploadImg/',views.uploadImg,name='uploadImg'),
  ]
  ```

  - 5.增加图片上传的视图 views.py

  ```python
  from .models import Img
   
  #图片上传
  def uploadImg(request):
      if request.method == 'POST':
          img = Img(img_url=request.FILES.get('img'))
          img.save()
      return render(request, 'imgUpload.html')
  ```

  -  6.新增页面templates/imgUpload.html 

  ```python
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>图片上传</title>
  </head>
  <body>
      <form action="" method="post" enctype="multipart/form-data">
          {% csrf_token %}
          <input type="file" name="img" accept="image/*">
          <input type="submit" value="上传">
      </form>
  </body>
  </html>
  ```

- 多张图片上传

  -  修改imgUpload.html 

  ```python
  把<input type="file" name="img">
  改成<input type="file" name="img" multiple="" accept="image/*">，就这一处而已，其他都不动
  ```

  -  views.py 

  ```python
  from DjangoFileUpload.settings import BASE_DIR
  def uploadImg(request):
      files = request.FILES.getlist('img')
      for f in files:
          destination = open(BASE_DIR + '/media/photos/' + f.name,'wb+')      #上传的文件都放到/media/photos/文件夹里
          for chunk in f.chunks():
              destination.write(chunk)
              destination.close()
      return render(request, 'imgUpload.html')
  ```

- 生成csv文件函数
  ```python
  import csv
  from django.http import HttpResponse
  
  def csv_view(request):
      response = HttpResponse(content_type='text/csv')
      response['Content-Disposition'] = 'attachment; filename="somefilename.csv"'
  
      writer = csv.writer(response)
      writer.writerow(['username', 'age', 'height', 'weight'])
      writer.writerow(['zhiliao', '18', '180', '110'])
  	# writerow中数组的每个元素是csv文件的列
      return response
  ```

# JavaScript

- 随机获取数组中的一个元素

  ```javascript
  var items = ['1','2','4','5','6','7','8','9','10'];
  var item = items[Math.floor(Math.random()*items.length)];
  console.log(item)  // item为随机数组中的一个元素
  ```

- js为Array数组对象添加remove方法，可以删除指定元素

  ```javascript
  Array.prototype.indexOf = function(val) {
  for (var i = 0; i < this.length; i++) {
      if (this[i] == val) return i;
  }
      return -1;
  };
  Array.prototype.remove = function(val) {
      var index = this.indexOf(val);
      if (index > -1) {
      this.splice(index, 1);
      }
  };
  var items = ['1','2','4','5','6','7','8','9','10'];
  items.remove('1')
  console.log(items)  // [2','4','5','6','7','8','9','10'];
  ```

- 生成随机长度/固定长度的随机字符

  ```javascript
  /*
  ** randomWord 产生任意长度随机字母数字组合
  ** randomFlag-是否任意长度 min-任意长度最小位[固定位数] max-任意长度最大位
  ** xuanfeng 2014-08-28
  */
  function randomWord(randomFlag, min, max) {
      var str = "",
          range = min,
          arr = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
      // 随机产生
      if (randomFlag) {
          range = Math.round(Math.random() * (max - min)) + min;
      }
      for (var i = 0; i < range; i++) {
          pos = Math.round(Math.random() * (arr.length - 1));
          str += arr[pos];
      }
      return str;
  }
  // 生成3-32位随机串：randomWord(true, 3, 32)
  // 生成43位随机串：randomWord(false, 43)
  ```

# nvm(Node Version Manager)安装的Node

- 目前发现 8.11以上版本的node版本对应的npm都没法自动安装，
  需要自己到npm官网( https://npm.taobao.org/mirrors/npm/)
  下载手动安装对应的npm版本

  - 1、进入nvm下的指定的node版本目录发现目录下没有npm运行文件
  - 2、进入node_modules发现文件夹为空 
  - 3、自己下载node对应的npm版本
  - 4、解压后将文件夹重命名为npm并复制到node_modules目录下
  - 5、最后将npm中bin目录下的npm以及npm.cmd复制到与node_modules目录同级目录下 

  -  6、此时npm命令即可使用，如果不能使用需要使用 

    >  nvm use node版本号 

# Node.js

- Linux安装：
  
  - 1、下载：官网：http://nodejs.cn/download/ 
    
  - 通过  uname -a  命令查看到我的Linux系统位数是64位（备注：x86_64表示64位系统， i686 i386表示32位系统） 
  
  - 2、上传：下载下来的tar文件上传到服务器并且解压，然后通过建立软连接变为全局； 
  
    -  上传服务器可以是自己任意路径 
    -  解压上传（解压后的文件我这边将名字改为了nodejs，这个地方自己随意，只要在建立软连接的时候写正确就可以） 
  
  - 3、解压：  tar -xvf  node-v6.10.0-linux-x64.tar.xz   
  
  - 4、重命名： mv node-v6.10.0-linux-x64  nodejs  
  
  - 确认一下nodejs下bin目录是否有node 和npm文件，如果有执行软连接，如果没有重新下载执行上边 
  
  - 步骤：
  
    -  1)建立软连接，变为全局 
  
      -  ln -s /app/software/nodejs/bin/npm /usr/local/bin/  
      -  ln -s /app/software/nodejs/bin/node /usr/local/bin/ 
  
    -  2)修改配置文件，vim /etc/profile
  
      ```
      1、在文件末尾添加：
      export NODE_HOME=解压的nodejs文件路径
      export PATH=$NODE_HOME/bin:$PATH
      
      2、
      按ESC输入:wq，保存退出
      ```
      
    -  3)输入文件生效命令：source /etc/profile
  
    -  4)最后一步检验nodejs是否已变为全局 
  
    - 输入node、npm查看是否出版本号
  
    
  
     
  
- 创建简单服务器

  ```javascript
  var http = require('http');
  var server = http.createServer();
  
  server.listen(5000, function(){
      conlose.log('启动成功 http://127.0.0.1:5000')
  })
  server.on('request', function(req, res){
      // 发送中文
      res.setHeader('content-Type', 'text/plain;charset=utf-8;');
      res.end('哈喽 world!')
  })
  
  ```

- 获取post数据

  ```javascript
  req.on('data', function(dd){
      d+=dd;
  })
  req.on('end', function(){
      var postdata = require('querystring').parse(d);
      conlose.log(postdata);
  })
  ```

- 允许跨域请求设置

  ```javascript
  http.createServer((req,res)=>{
      //设置允许跨域的域名，*代表允许任意域名跨域
      res.setHeader("Access-Control-Allow-Origin","*");
      //跨域允许的header类型
      res.setHeader("Access-Control-Allow-Headers","Content-type,Content-Length,Authorization,Accept,X-Requested-Width");
      //跨域允许的请求方式
      res.setHeader("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
      //设置响应头信息
      res.setHeader("X-Powered-By",' 3.2.1')
      //让options请求快速返回
      if(req.method == "OPTIONS"){return res.end();}
      }
  }).listen(3000);
  ```


### express框架

```js
var express = require('express')
var bodyParser = require('body-parser');

var app = express()

//OPTIONS -- 若有跨域情况，浏览器会先发送试探请求
var allowCrossDomain = function(req, res, next) {
    res.setHeader('Access-Control-Allow-Origin', '*'); //允许请求的源头
    res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS, PUT, DELETE'); //允许任何方法
    res.setHeader('Access-Control-Allow-Headers', 'X-Requested-With,content-type,X-Session-Token'); //允许任何类型
    next(); //下一步
};
app.use(allowCrossDomain)

app.use(bodyParser.json()) // 创建 application/json 解析
app.use(bodyParser.urlencoded({ extended: true })) // 创建 application/x-www-form-urlencoded 解析

// 测试接口
app.get('/test', function(req, res) {
        res.send('test ok')
    })
    // 简单登录验证接口，
app.post('/login', function(req, res) {
    var user = 'admin',
        pwd = '123456';
    if (req.body) {
        var { username, password } = req.body
        if (user === username && pwd === password) {
            res.send({ message: "登录成功!", token: true })
        } else if (!username | !password) {
            res.send({ message: "账号或密码不能为空!", token: false })
        } else if (username.length > 20) {
            res.send({ message: "账号长度不能大于20!", token: false })
        } else if (password.length > 20) {
            console.log(123);
            res.send({ message: "密码长度不能大于20!", token: false })
        } else {
            res.send({ message: "账号或密码错误!", token: false })
        }
    }
})
app.listen(3000, function() { console.log("Server started on port 3000.") });
```

### koa

# Vue.js

1. 常用指令：v-for、v-if/v-show、v-bind、v-on、v-model、v-html/v-text、v-once
2. 修饰符：
   1. 事件修饰符：
      - `.stop`
      - `.prevent`
      - `.capture`
      - `.self`
      - `.once`
      - `.passive`
   2. 按键修饰符：
      - `.enter`
      - `.tab`
      - `.delete` (捕获“删除”和“退格”键)
      - `.esc`
      - `.space`
      - `.up`
      - `.down`
      - `.left`
      - `.right`
   3. v-model修饰符：.lazy、.number、.trim
3. 组件通信
   1. 父传子：父属性传，子props接收
   2. 子emit触发父方法传值给父
4. 路由($router、 route)、路由传参(params、query)
5. watch与computed
6. 生命周期4种状态8个钩子函数
7. 组件封装export default导出或暴露全局Vue.protype.xxx
8. vuex
   - commit同步更改
   - dispatch异步更改
9. 

- vue-cli：一个全局的命令行工具，他基于node开发的
  
  - vue-cli2:
  - 安装：npm install -g @vue/cli @vue/cli-init
  - 验证安装：vue -V
  - 使用：vue init webpack myapp(依赖webpack创建一个名为myapp的vue项目)
    - project name(项目名字)
    - project description(项目描述)
    - Author(作者)
    - Vue build(全部还是运行时的代码？)：全部
    - Install vue-router?(安装vue-router？)：
    - use ESlint to lint your code?(ESlint语法检测)
    - Set up unit tests ()：n
    - Setup e2e tests with Nightwatch? (Y/n)：n
    - Should we run `npm install` for you after the project has been created? (recommended) (Use arrow keys)：Yes,use NPM
    - 配置完成开始下载vue项目需要下载的所有东西
  - vue项目启动，进入项目文件夹：npm run dev
  
  
  
  - vue-cli3:
  - 创建项目：vue create projectname
    - please pick a preset:default(默认的)、手动的
    - Check the features needed for your project(检查项目所需特性):基本选择babel、Router两个
    - use history mode for router?：n(hash模式)
    - where do you prefer placing config for Babel,ESlint,etc.?：In dedicated config files
    - Save this as a perset for future projects?：n
    - 开始安装
    - 运行：npm run serve
  
- 组件之间传参

  - 父到子
    - 在父组件页面的子组件添加v-bind:msg="'msg'"
    - 子组件页面props:['msg']或props:{msg:String}
  - 子到父：
    - 接收消息：
      - 子组件$emit('自定义名字', '值')发射
      - 父组件接收v-on:自定义名字="函数"，在函数的参数中获取子路由传递的值
    - 子操作父方法
      - 父在mouted定义函数，用父传子的方法在子组件接收函数，接收到函数后，子组件$emit('自定义名',接收的函数)发射接收到的函数

# Element UI

- https://element.faas.ele.me/#/zh-CN

- 在vue项目文件夹命令安装： npm i element-ui -S 

- 引入Element

  - 在 main.js 中写入以下内容：

    ```javascript
    import Vue from 'vue';
    import ElementUI from 'element-ui';
    import 'element-ui/lib/theme-chalk/index.css';
    import App from './App.vue';
    
    Vue.use(ElementUI);
    
    new Vue({
      el: '#app',
      render: h => h(App)
    });
    ```

# Git分布式版本控制系统

 为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。 

下载后配置

- git config --global user.name "Ruan"

- git config --global user.email "947968945@qq.com"

- git init：创建一个repository仓库，创建的目录下的.git文件夹是用来跟踪管理版本库的

- ### 两步提交到本地仓库

  - 第一步：用命令告诉git，把文件添加到仓库暂存区stage，执行下面命令没有显示就是对了
    - git add readme.txt
  - 第二步：用命令git commit告诉git， 把暂存区的所有内容提交到当前分支master (-m 后加本次提交的说明)  ：
    - git commit -m "first commit"
    - git commit命令执行成功后会告诉你，1 file changed:1个文件被改动(我们新添加的readme.txt文件)；2 insertions：插入了两行内容(readme.txt有两行内容)

- `git status`：查看仓库状态(文件是否修改过)
- `git diff`： 可以查看修改内容。 
- `git log`：命令显示从最近到最远的提交日志 
  -  如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数
  -  你看到的一大串类似`1094adb...`的是`commit id`（版本号） 

- ### 版本回退`git reset`

  -  用`HEAD`表示当前版本，  上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。 

  -  回退到上一个版本`add distributed`，就可以使用`git reset`命令 ：

    ```
    git reset --hard HEAD~1
    HEAD is now at e475afc add distributed
    ```

- ### 版本前进`git reset --hard 1094a`

  -  版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。 
  - 获取`commit id`Git提供了一个命令`git reflog`用来记录你的每一次命令 



- #### 撤销修改`git checkout -- <file>` `git reset HEAD <file>`

  - 命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

     一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

    一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

  -  Git同样告诉我们，用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区： 

- ### 小结

  又到了小结时间。

  场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

  场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

  场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。

- #### 删除文件

-  现在你有两个选择

  - 一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`： 

    ```
    git rm test.txt
    git commit -m "remove test.txt"
    ```

    

  -  另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本： 

    ```
    git checkout -- test.txt
    ```

- #### 推送到远程库

  - SSH key(公钥与密钥)

  - 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

    ```
    $ ssh-keygen -t rsa -C "youremail@example.com"
    ```

  -  第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：添加ssh key

  - 在github新建仓库

  - 在本地创建的仓库提交

  - 关联远程库：`git remote add origin git@github.com:用户名/learngit.git`

  -  添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。 

  - 把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

    由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。
    
    查看远程地址：`git remote -v`
    
    ```
    git push -u origin master
    ```

- ### 克隆仓库`git clone`

  - `git clone git@github.com:woshisheine/hello-world.git`

  - 你也许还注意到，GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。

    使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。

- ### 分支管理

  - Git鼓励大量使用分支

  - 查看分支：`git branch`

    创建分支：`git branch `

    切换分支：`git checkout `或者`git switch `

    创建+切换分支：`git checkout -b `或者`git switch -c `

    合并某分支到当前分支：`git merge `

    删除分支：`git branch -d `

  - 新的switch

    -  创建并切换到新的`dev`分支，可以使用： 
    - `git switch -c dev`

  -  直接切换到已有的`master`分支，可以使用： 

    - `git switch master`

  - `git log --graph --pretty=oneline --abbrev-commit`查看分支合并情况图

  - 分支管理策略： 准备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`： 

    - `git merge --no-ff -m "merge with no-ff" dev`

### 小结

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick `命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D `强行删除。 



# cmder

https://www.cnblogs.com/feigao/p/8717520.html

### 简介： cmder是一个增强型命令行工具，不仅可以使用windows下的所有命令，更爽的是可以使用linux的命令,shell命令。 

### 下载： 官网地址：http://cmder.net/ 

下载的时候，会有两个版本，分别是mini与full版；唯一的差别在于有没有内建msysgit工具，这是Git for Windows的标准配备；全安装版 cmder 自带了 msysgit, 压缩包 23M, 除了 git 本身这个命令之外, 里面可以使用大量的 linux 命令；比如 grep, curl(没有 wget)； 像vim, grep, tar, unzip, ssh, ls, bash, perl 对于爱折腾的Coder更是痛点需求。

### 安装 

直接解压到某个目录就可以了，点击Cmder.exe运行。 

### 配置环境变量

在系统变量添加

- 变量名： *CMDER_HOME*
- 变量值： 安装绝对路径

 最后在Path添加一条*斜体文字*
*%CMDER_HOME%*



### 添加 cmder 到右键菜单

配置环境变量后，在**管理员权限**的终端输入以下语句。
Win8或者Win10可以直接 win+x 再按 a 键进入。

```
Cmder.exe /REGISTER ALL
```

### 解决中文乱码问题

 之前在网找了好多方法，可是都解决不了，很多人在在Environment里添加set LANG=zh_CN.UTF-8来解决中文乱码的问题，可是我用这个方法并没有成功，可能是环境的原因吧，我的系统是win10的。
最后找到解决办法：
Settings->Startup->Environment 在最后添加
set LANG=zh_CN.UTF-8
set LC_ALL=zh_CN.utf8 

 ![img](https://images2018.cnblogs.com/blog/763945/201804/763945-20180404153700272-1516801389.png) 

### 更改背景

setting->Main->Background->选择图片->选择背景透明度->背景展示方式->save settings

 ![img](https://images2018.cnblogs.com/blog/763945/201804/763945-20180404153813574-2036831489.png) 

### 更换主题

settings->Features->Colors

 ![img](https://images2018.cnblogs.com/blog/763945/201804/763945-20180404153852546-1032635388.png) 







# webpack

webpack基于node，不推荐全局安装

##### 安装：`npm install webpack webpack-cli`

##### 卸载：`npm uninstall webpack webpack-cli`

版本坑cli版本过高Error: Cannot find module 'webpack-cli/bin/config-yargs'(复制npm install)能运行：

```js
"webpack": "^4.17.1",
"webpack-cli": "^3.3.9",  // cli版本过高
"webpack-dev-server": "^3.8.2"

"webpack-hot-middleware": "^2.22.0",
"webpack-merge": "^4.1.1"

```

以下使用版本

webpack 4.43.0

webpack-cli 3.3.12

webpack-dev-server 3.11.0

基本配置

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const TerserJSPlugin = require('terser-webpack-plugin')
const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')
const CleanWebpackPlugin = require('clean-webpack-plugin')

module.exports = {
    mode: 'production', // 换development为开发模式打包
    // 入口
    entry: './src/main.js',
    // 出口
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    optimization:{
        minimizer:[new TerserJSPlugin({}),new OptimizeCssAssetsWebpackPlugin({})]
    },
    // loader装载器
    module: {
        rules: [
            { test: /\.css$/, use: [MiniCssExtractPlugin.loader, {
                loader:"css-loader",
                options:{
                    importLoaders: 2  // 用后面几个加载器来解析
                }
            },"postcss-loader", "less-loader"] 
            },
            { test:/\.less$/, use:[MiniCssExtractPlugin.loader,'css-loader','less-loader']}
            {
            	test:/\.(jpg|jpeg|gif)$/,
            	use:{
            		loader:'url-loader',
            		options:{
            			limlt:10*1024,
            			outputPath: 'img', // 输出到img文件夹
                	}
            	}
            },
            {
                test:/\.js$/,
                use:{
                    loader: 'babel-loader',
                    options:{ // 或在配置文件.babelrc写
                        presets: ["@babel/preset-env"],
                        plugins: []
                    }
                }
            }
        ]
    },
    // plugin插件
    plugins: [
        new CleanWebpackPlugin()
        new HtmlWebpackPlugin({
            template: path.join(__dirname, './src/index.html'),
            filename: 'index.html'
        }),
        new MiniCssExtractPlugin({
            filename:'index.css'
        })
        
    ]
}
```

.babelrc

```js
{
    "presets":[
        // @babel/core  babel的核心模块
        // @babel-preset-env  主要是把es6转换成es5 插件的集合
        ["@babel-preset-env",{
            "useBuiltIns": "usage", //按需加载
            "corejs":3  // babel/poliyfill
        }]
    ],
    "plugins":[
        // @babel/runtime减少冗余代码，需@babel/plugin-transform-runtime调用
        "@babel/plugin-transform-runtime",
        // 装饰器
        ["@babel/plugin-proposal-decorators",{
            "legacy":true
        }],
        // 类语法
        ["@babel/plugin-proposal-class-properties",{
            "loose":true
        }]
    ]
}
```

### 加载器loader

##### 动态加载(在入口文件引入)图片:file-loader、url-loader(小图片生成base64)

```js
module:{
    rules:[
        {
            test:/\.(jpg|jpeg|gif)$/,
            use:{
                loader:'url-loader',
                options:{
                    limlt:10*1024,
                    outputPath: 'img', // 输出到img文件夹
                }
            }
        }
    ]
}
```

##### 图片:html-withimg-loader(第三方)

```js
module:{
    rules:[
        {
            test:/\.html$/,
            use:'html-withimg-loader'
        }
    ]
}
```

兼容其他浏览器：postcss-loader

```js
module.exports = {
    plugins:[
        
    ]
}
```



自动加私有前缀：autoprefixer

### 插件plugin总结归类

#### 功能类

##### html-webpack-plugin

> 自动生成html，基本语法：

```js
new HtmlWebpackPlugin({
    template: path.join(__dirname, './src/index.html'),
    filename: 'index.html'
})
```

##### clean-webpack-plugin

>在编译之前清理指定目录指定内容。基本用法：

```js
// 清理目录
const pathsToClean = [
  'dist',
  'build'
]
 
// 清理参数
const cleanOptions = {
  exclude:  ['shared.js'], // 跳过文件
}
module.exports = {
  // ...
  plugins: [
    new CleanWebpackPlugin(pathsToClean, cleanOptions)
  ]
}
```

压缩js：terser-webpack-plugin

压缩css：optimize-css-assets-webpack-plugin

##### copy-webpack-plugin

> 拷贝资源插件，基本用法：

```js
new CopyWebpackPlugin([
    {
        from: path.join(process.cwd(), './vebdir/'),
        to: path.join(process.cwd(), './dist/'),
        ignore: ['*.json']
    }
])
```

##### webpack-manifest-plugin && assets-webpack-plugin

> 俩个插件效果一致，都是生成编译结果的资源单，只是资源单的数据结构不一致而已。

webpack-manifest-plugin 基本用法：

```js
module.exports = {
  plugins: [
    new ManifestPlugin()
  ]
}
```

 assets-webpack-plugin 基本用法： 

```js
module.exports = {
  plugins: [
    new AssetsPlugin()
  ]
}
```

#### 全局变量(jquery、)

1. cdn

2. ProvidePluhgin 第三方模块不打包

   ```js
   const webpack = require('webpack')
   module.exports = {
       externals:{
           "jquery":"$"  // 
       }
       plugins:[
       	new webpack.ProvidePluhgin({
       	"$": "jquery" // $变量是jquery导出的
   })
       ]
   }
   ```

3. 暴露的方式 expose-loader

   ```js
   module:{
       rules:[
           {
               test:require.resolve('juery'),
               use:{
                   loader:"expose-loader",
                   options:"$"
               }
           }
       ]
   }
   ```

#### 代码排查(soure-map)

开发环境推荐：cheap-module-eval-source-map

生产环境推荐：cheap-module-source-map

```js
module.exports = {
    devtool:"cheap-module-eval-source-map"
}
```

#### 图片压缩：image-webpack-loader

```js
rules: [{
  test: /\.(gif|png|jpe?g|svg)$/i,
  use: [
    'file-loader',
    {
      loader: 'image-webpack-loader',
      options: {
        mozjpeg: {
          progressive: true,
        },
        // optipng.enabled: false will disable optipng
        optipng: {
          enabled: false,
        },
        pngquant: {
          quality: [0.65, 0.90],
          speed: 4
        },
        gifsicle: {
          interlaced: false,
        },
        // the webp option will enable WEBP
        webp: {
          quality: 75
        }
      }
    },
  ],
}]
```

### 热更新：host:true 功能是在style里的(style-loader)

局部更新插件：

```js
plugins:[
    new webpack.HotModuleReplacementPlugin(),
]
```

### 懒加载：



### 打包文件分析工具：webpack-bundle-analyzer插件

```js
const {BludleAnalyzerPlugin} = require('webpack-bundle-analyzer')
plugins:[
    new BludleAnalyzerPlugin()
]
```

### 多入口多出口

```js
entry:{
    index:'./src/index.js',
    other:'./src/other.js'
}
output:{
    filename:'[name].js'
    path:path.resolve(__dirname, 'dist'})
}
plugins:[
    new HtmlWebpackPlugin({
        template: path.join(__dirname, './src/index.html'),
        filename: 'index.html',
        chunks:["index", "other"]
    }),
]
```

### 第三方模块抽离：splitChunks

```js
module.exports = {
  //...
  optimization: {
    splitChunks: {
      chunks: 'async',  // 异步代码
      minSize: 20000,  // 至少30kb才去抽离
      minRemainingSize: 0,
      maxSize: 0,
      minChunks: 1,  //至少引用模块一次
      maxAsyncRequests: 30,  // 请求最多不超过30次
      maxInitialRequests: 30,  // 首屏请求次数不超过30次
      automaticNameDelimiter: '~',  // 抽离模块名称的连接符
      enforceSizeThreshold: 50000,
      cacheGroups: {  // 自己设定一些规则
        defaultVendors: {
          test: /[\\/]node_modules[\\/](jquery)/,
          priority: -10,
          reuseExistingChunk: true
        },
        default: {
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true
        }
      }
    }
  }
};
```

### 分离生产开发环境文件(webpack-merge):

```js
const merge = require('webpack-merge')
module.exports = (env)=>{
    let base = {} // 公共配置
    if(env.development){
        return merge(base, dev);
    }else{
        return merge(base, prod);
    }
}
```



清楚浮动：

```
.clearfix::after{
    content:"";
    display:block;
    visibility:hidden;
    clear:both;
    }
```