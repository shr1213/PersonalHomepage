# 一个导航页🗺

- 国内搜索引擎的信息流着实用不到，个人想关注的信息又过于分散，因此决定自己写一个导航页，整合自己所需要的信息和功能。

- 采用前后端分离的架构，前端使用Vue.js，后端使用Python，MariaDB+Redis提供数据存储。

- 前端框架使用Element UI，后端框架使用Flask，后端ORM使用Peewee。

- 🐞 如果有任何BUG/需求/建议，欢迎提Issues！

- ⭐ 欢迎star！尽量保证每天都有提交！

![screenshot](https://user-images.githubusercontent.com/27627484/92318185-361f9e80-f03b-11ea-9c33-b9759ccdbe80.png)

## 特性

- 简介优雅的展示方式：没有广告、没有信息流、只有你需要的功能和信息
- 灵活的组件配置：用不到某个组件？不满意默认的排序方式？使用组件编辑器轻松编辑个性化的主页组件！
- 组件内容随心定制：几乎所有的组件都可以自由修改内容，显示的天气、展示的书签、黄金价格提醒的阈值、想要关注的App Store应用...统统可以自由修改！
- 功能丰富的后端：当前类似的导航页项目大部分都仅有前端，或只有负责爬取数据的后端，本项目添加了可以在服务器上运行任意脚本的功能，With great backend comes great ability!

## 部署
  
  首先需要本地安装MySQL（测试时使用的是MariaDB）和Redis
  
  在具备环境后，使用python3运行根目录下的start.py并根据提示进行操作
  
  后端代码位于/backend，后端入口文件位于/backend/run.py，前端代码位于/frontend，前端编译的产物位于/dist，上传的文件保存在/upload
  
  **dev分支为开发中分支，运行可能会有问题，建议使用master分支进行部署测试**
  
## 开发进度

### Done：
- 多用户登录
- 搜索引擎（仅为入口，支持配置多搜索引擎）
- 灵活方便的异步脚本统一驱动和管理平台
- 接口层级的权限控制（用户、角色、权限的新增与关联）
- 网盘（支持生成链接分享）
- 易于操作的小组件编辑器
- 小组件-天气（未登录用户识别ip位置，登录后用户还可以添加自定义位置，支持天气异常时推送微信或发送邮件）
- 小组件-书签
- 小组件-AppStore价格监控（支持设置触发阈值后推送微信或发送邮件）
- 小组件-黄金价格（支持设置触发阈值后推送微信或发送邮件）
- 小组件-便签（支持定时发送便签内容到微信或邮箱）
- 小组件-翻译
- 小组件-必应壁纸
### Working on:
- 优化代码
### To Do
- 小组件-基金
- 小组件-股票
- 小组件-新闻
  
---------------------------------------------------------------------------------------------------------------------------------

## 介绍

### 搜索

入口：主页

功能：输入内容后跳转到搜索网址，进入页面焦点自动置于搜索框内，输入文字可以带出提示（使用的百度的接口）增加引擎的话是在数据库中增加数据(search_engines)

- 自动提示和切换搜索引擎

![image](https://user-images.githubusercontent.com/27627484/71998812-3f255980-327b-11ea-9e6d-7ad97cd5c18d.png)

### 控制台

入口：登陆后左上角hover用户名-控制台

功能：提供在console表中注册的前端组件入口，方便日后权限控制或进行排序等操作，如需增加前端模块，除了编写前端业务外，还需要在console表中增加一条记录

![image](https://user-images.githubusercontent.com/27627484/90091356-bf9fc180-dd58-11ea-85fb-9e2971dfb138.png)

### 控制台-脚本运行平台

入口：登陆后左上角hover用户名-控制台-脚本运行平台。

功能：用于后台程序的统一驱动。前端表单均由配置产生，无需接触前端代码，通过填写配置生成的表单来提交脚本至后端运行脚本，并展示运行结果，而且具有定时运行脚本、对以前运行的任务进行回放、记录运行耗时、记录运行日志、定制运行记录表格等人性化功能

注意：
1. 为了使作为html展示的运行结果正确展示空格数量，输出的所有空格都会被替换为"\&nbsp;"，如果需要在输出中真正输出空格，则脚本输出的空格必须使用"# "来代替空格，如：自己组装html标签并增加样式的时候，标签中就必须有空格，所以需要使用"\<table# border="1"\>"代替"\<table border="1"\>"
2. 定时任务需要配置"\backend\app\script\schedule_monitor.sh"为定时运行，因为系统默认可以配置的最短的定时运行间隔为五分钟，所以此定时任务的运行步长最好设置为五分钟

模块：
- 首页：左侧为脚本所属栏目，右侧为栏目下的脚本，一个脚本为一个tab，通过右上角的"+"可以增加所选栏目的脚本
![image](https://user-images.githubusercontent.com/27627484/72076975-6dfe0700-3331-11ea-9253-717766654a2d.png)
- 按钮区域：
  右上角的五个按钮依次为：回放我上一次运行的参数（回填到表单中）、展示我上一次运行的日志、展示最近50条运行记录、配置定时运行、编辑脚本和删除按钮（此系统中所有删除和更新操作都为逻辑删除）
![image](https://user-images.githubusercontent.com/27627484/72077181-ca612680-3331-11ea-9a88-37c6ead5e6f9.png)
- 编辑脚本：
  ![image](https://user-images.githubusercontent.com/27627484/72078174-95ee6a00-3333-11ea-9d24-be5e4ff41309.png)
  
  **初始选项：**
  - 脚本名称：展示在tab上
  - 起始文件夹：配置在此处的文件夹会使用cd命令打开
  - 起始脚本：配置在此处的脚本会作为初始命令
  - 组合方式：提供两种组合方式-"顺序"和"替换"："顺序"将起始脚本和参数顺序组合提交；"替换"则类似Jenkins的处理方式，如，当配置为"python3 %参数%"的时候，系统会将"%参数%"替换为"参数"组件内填写或选择的值，当"参数"填写为"Awesome.py"的时候，最终生成的命令将是"python3 Awesome.py"
  
   **组件选项：**
  - 组件名称：前端展示的label
  - 组件类型：提供四种类型-输入框、选择器、日期选择器和日期范围选择器，根据用户配置展示为相应的组件
  - 默认值：组件默认值
  - 是否只读：前端是否只读
  - 占位文字：前端展示的placeHolder
  - 备注：备注将以组件后一个icon的方式展现，鼠标悬浮即可展示
  - 是否有额外按钮：配置为是时，组件后方会展示一个按钮，运行按钮可以运行小型脚本，适用于动态提醒用户参数，如下方图片所示。有两种数据的展示模式，一种是脚本内直接使用`print()`来打印需要输出的文字；此外，通过一定的数据格式，可以选择器组件的选项进行初始化，见下方实例：
  ```python
  import json
  d = {
      'code': 200,                                # 状态码，非必填，无实际作用
      'data': {
          'msg': 'hello\nworld qwe\nqewqweewqwe', # 展示的文本，非必须，会被解析为html，使用"\n"换行
          'value': '123',                         # 非必须，当传递value时，会将组件内的值替换成传回的值
          'options': [                            # 非必须，当传递options时，会将选择器组件内的选项替换成传回的选项
              {
                  'label': '234',                 # 标签，用于选择器组件展示的值
                  'value': '234'                  # 值，用于选择器组件选择时实际代表和传递的值
              },
          ]
      }
  }
  print(json.dumps(d))
  ```
  ![image](https://user-images.githubusercontent.com/27627484/72077217-d947d900-3331-11ea-97ce-6a7cbda6e09d.png)
  - 是否在列表展示：配置为是时，在运行列表中会以单独一列的方式呈现运行时提交的参数，但是，如果将太多的组件都设置为"在列表展示"，会带来前端性能的影响，所以建议不要设置太多个
  - 是否显示：配置为否时前端不展示
  
- 运行列表：默认展示运行人、操作、运行开始时间、耗时、运行ID五列，其中操作列包含三个按钮：参数、日志和回放。"参数"按钮悬浮可以展示参数，"日志"按钮点击可以展示日志、"回放"按钮点击可以将所选运行记录的参数回填至当前表单上。运行列表可以通过配置组件的"是否在列表展示"选项来自定义列，但不建议设置过多。
![image](https://user-images.githubusercontent.com/27627484/72077227-df3dba00-3331-11ea-9e03-b82439f5cda8.png)
- 定时任务：最小颗粒度为五分钟，实际上更小也可以，但是没有试过，如果调小颗粒度，则需要减小定时任务扫库脚本的运行步长。定时任务驱动的脚本，在列表中会在运行人后方加上"(定时)"字样
![image](https://user-images.githubusercontent.com/27627484/72083322-90e1e880-333c-11ea-9995-774f0faeae73.png)

### 控制台-账户和权限

入口：登陆后左上角hover用户名-控制台-账户和权限

功能：使用"用户-角色-权限"模型编写的接口层级的权限控制系统，接口使用一个装饰器即可以对权限进行控制。默认用户请求接口时，请求IP必须与登录时使用的IP一致，这是一种较为严格的策略，在"/backend/app/privilege/privilege_control.py:20"可以关闭

模块：
- 用户设置：新增用户、禁用用户、删除用户、修改用户角色、修改用户密码

![image](https://user-images.githubusercontent.com/27627484/87305367-f5c70700-c548-11ea-89b4-5ce69d93dd9c.png)

- 角色对应权限设置：新增角色、禁用角色、删除角色、修改角色名称、修改角色对应权限

![image](https://user-images.githubusercontent.com/27627484/87307869-eea1f800-c54c-11ea-8862-ccc5503f333a.png)

- 权限设置：新增权限、禁用权限、删除权限、修改权限

![image](https://user-images.githubusercontent.com/27627484/87305485-2444e200-c549-11ea-91cb-612b3a4c9ca5.png)

### 控制台-小组件编辑器

入口：登陆后左上角hover用户名-控制台-修改主页组件

功能： 拖拽来修改主页显示的方式。组件的父级定义为"组件集"，当有且只有一个组件集的时候，页面不展示组件集标题，仅展示它所包含的组件，当有两个及两个以上的组件集时，展示组件集及其所包含的组件

按钮：使用左右拖拽的方式来编辑组件集的顺序，使用组件集右侧圆形加号按钮来添加组件集，使用每个组件集内部的编辑按钮来修改组件集的名称，使用每个组件集内部的删除按钮来删除组件集；组件集内的组件使用上下拖拽的方式来编辑顺序，使用每个组件集内的方形加号按钮来添加组件，使用组件右侧的删除按钮来删除组件。组件详情不支持修改，可以手动改库(widget)来对其进行修改

![image](https://user-images.githubusercontent.com/27627484/90026670-33ef4c00-dcea-11ea-8357-1420224b60a1.png)

![image](https://user-images.githubusercontent.com/27627484/90026706-3fdb0e00-dcea-11ea-8d3a-78db7d28bf62.png)

### 网盘&图床

入口：登陆后左上角hover用户名-网盘/图床

网盘：
  
  - 功能：一个简易的网盘功能，并支持通过下载链接分享，文件上传不限制大小，下载不限制速度，但是大文件上传时需要多等一会直到loading结束。文件存储于根目录的upload文件夹，并建立名称为日期的子文件夹。
  
  - 按钮：界面上方为上传文件按钮，可以点击并选择文件或者通过拖拽文件至浏览器来上传文件；下方文件列表的按钮有：1.下载按钮-点击会下载文件；2.分享按钮(未分享时出现)-点击后会生成分享链接，分享给其他人后，其他人粘贴至浏览器即可触发该文件的下载，分享链接经过加密和压缩，真实下载链接会被压缩为短链接，方便使用，且链接带有鉴权token，保证基本的安全性；3.复制分享链接按钮(分享后出现)-点击后复制分享链接至剪贴板；4.取消分享按钮(分享后出现)-将分享链接置为失效并取消分享；5.删除按钮-将文件逻辑删除

图床：
  - 功能：上传图片并生成链接
  - 按钮：预览&下载、复制图片链接、删除按钮

![image](https://user-images.githubusercontent.com/27627484/92317142-2189d900-f030-11ea-9f34-b4859b6c7a59.png)
![image](https://user-images.githubusercontent.com/27627484/92317155-38c8c680-f030-11ea-967c-f9c66431047d.png)


### 小组件-天气

入口：主页小组件

功能：如不登录则展示IP所在地的天气信息(受限于第三方API，IP位置为国外时，支持不好)，登录后可以进行自定义，展示范围为IP+自定义位置的信息

说明：当请求数据时，为了保障速度，首先会使用缓存，缓存数据有效期为3小时（在\backend\app\weather\weather_function.py:16修改），如果没有有效缓存，则会请求外部API以获取数据并存为缓存

按钮：新增-登录后新增城市；排序-可拖动对自定义的城市进行排序或删除

![image](https://user-images.githubusercontent.com/27627484/87287598-df12b700-c52c-11ea-9645-60418f048f45.png)

### 小组件-书签

入口：主页小组件

功能：登陆后可以自定义，不登录时展示的书签是在数据库中修改（bookmarks.user_id==0）

按钮：新增-登陆后新增书签；设置：登陆后拖动排序、删除或修改书签的图标

- 拖动修改展示顺序

![image](https://user-images.githubusercontent.com/27627484/87288831-72002100-c52e-11ea-9fe1-aca28bfabe73.png)
- 修改书签详情

![image](https://user-images.githubusercontent.com/27627484/87288878-8512f100-c52e-11ea-8a2a-4c771ff32143.png)
- 修改书签图标

![image](https://user-images.githubusercontent.com/27627484/93906905-5172f500-fd2f-11ea-9627-6c42936dc21e.png)

### 小组件-黄金价格

入口：主页小组件

功能描述：监控黄金价格，并且可以设定阈值，当价格超过阈值时发送提醒。需要在"脚本运行平台"中配置定时任务，爬虫在爬取数据的时候会跳过国内黄金不开盘的时间。

![image](https://user-images.githubusercontent.com/27627484/87305571-4b031880-c549-11ea-880a-115b891704db.png)

![image](https://user-images.githubusercontent.com/27627484/87305626-62da9c80-c549-11ea-8bac-f33695ac4d71.png)

### 小组件-App Store应用价格监控

入口：主页小组件

功能：监控苹果软件商店应用的价格，当小于设定的阈值时，提醒用户。需要填写AppStore应用链接，此链接可以百度'想要关注的app名字+" site:apps.apple.com"'来获取，如"gorogoa site:apps.apple.com"，然后打开中文商店的页面(这样价格爬取到的才是中文)，此时的页面链接即为AppStore应用链接，如"https://apps.apple.com/cn/app/id1269225754"。

![image](https://user-images.githubusercontent.com/27627484/87305689-7a198a00-c549-11ea-9925-d944bdb839e5.png)

![image](https://user-images.githubusercontent.com/27627484/88994520-2b2a6d80-d31b-11ea-9b3a-3f764f83b575.png)

### 小组件-便签

入口：主页小组件

功能：记录便签，并可以定时推送便签内容到微信/邮件。由于不想把功能做的太复杂，提交的推送是不允许撤销的，但可以多次设置，即：设置的推送可以随意加但不能减。此外，便签还可以通过"时间机器"回滚至之前的版本，适用于误删等情况。

按钮：鼠标hover省略号，可以弹出三个按钮：编辑和删除-对选中的便签进行编辑或删除，提交后将所有便签保存为一个新版本；提醒-点击后弹出编辑提醒对话框，可以通过微信/邮件的方式提醒便签内容，最小颗粒度为五分钟。下方的圆形按钮分别为新增按钮和时间机器按钮，功能不再赘述

![image](https://user-images.githubusercontent.com/27627484/90039924-e549ae00-dcf9-11ea-97c5-6c7b69b197ea.png)

![image](https://user-images.githubusercontent.com/27627484/89022948-69448300-d355-11ea-893d-2deb553072bc.png)

### 小组件-翻译

入口：主页小组件

功能：使用[translators](https://github.com/UlionTse/translators)实现，使用的是阿里的服务，当在左侧输入区输入文字后，一段间隔后，会根据上方选择的语言进行翻译。

![image](https://user-images.githubusercontent.com/27627484/92317176-9ceb8a80-f030-11ea-9e73-0e6656fcbe73.png)


### 小组件-必应每日壁纸

入口：主页小组件

功能：系统使用「脚本运行平台」驱动脚本来每天爬取一张必应壁纸，小组件上则滚动展示7天内的壁纸，点击图片可以下载原图。

![image](https://user-images.githubusercontent.com/27627484/94260304-8024e180-ff62-11ea-860a-2e27b7827d8c.png)

## License

[MPL-2.0](https://opensource.org/licenses/MPL-2.0)

