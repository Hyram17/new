1.安装python3及其他组件（如beautifulsoup、requests）并配置环境
在windows的控制面板\系统和安全\系统中，点击“高级系统设置”，然后点击“环境变量”，编辑“Path”变量。将Python相关目录添加到Path变量中。按win+R，输入cmd打开命令提示符，输入pip install beautifulsoup4安装beautifulsoup；输入pip install requests 安装 requests。
2.对于爬取回来的网页内容，可以通过re、beautifulsoup4等函数库来处理，其中最重要且最主流的两个函数库：requests 和beautifulsoup4，它们都是第三方库。requests 库是一个简洁且简单的处理HTTP请求的第三方库,建立在Python 语言的urllib3 库基础上。其最大优点是程序编写过程更接近正常URL 访问过程。Beautiful Soup提供一些简单的、python式的函数用来处理导航、搜索、修改分析树等功能。它是一个工具箱，通过解析文档为用户提供需要抓取的数据，因为简单，所以不需要多少代码就可以写出一个完整的应用程序。
爬虫调度端：用来启动、执行、停止爬虫，或者监视爬虫中的运行情况。
URL管理器：对将要爬取的URL和已经爬取过的URL这两个数据的管理。
网页下载器：将URL管理器里提供的一个URL对应的网页下载下来，存储为一个字符串，这个字符串会传送给网页解析器进行解析。
3.网页解析器：一方面会解析出有价值的数据，另一方面，由于每一个页面都有很多指向其它页面的网页，这些URL被解析出来之后，可以补充进URL管理器。
4.在注册GitHub之后创建新项目，即新建个repository来放项目，然后把repository克隆到本地，再把代码、代码说明文档、项目的发展状况、贡献者列表、历史演变、许可证条款等放在代码仓库里。