python+Selenium自动化测试架构
## 环境

- Python 3
- selenium 2.53
- PyYaml
- xlrd
- requests
- JMESPath
- Faker
需要的环境

    浏览器（Firefox/Chrome/IE…）
    Python
    Selenium
    Selenium IDE（如果用Firefox）
    FireBug、FirePath（如果用Firefox）
    chromedriver、IEDriverServer、phantomjs.exe
    IDE（Pycharm/Sublime/Eclipse…）

1、浏览器建议用Firefox或Chrome，千万不要用最新版本，要用早两到三个版本的。
2、Python不要使用python2，而使用python3。
3、Selenium安装使用命令pip install selenium
4、Selenium IDE可以录制回放，只能应用与Firefox浏览器。作为Firefox插件插件而存在。
5、如果要使用Firefox，必备的插件就是FireBug和FirePath，这俩都可以在附加组件管理器中搜到。
6、果需要使用Chrome浏览器或者IE浏览器，则需要对应的驱动，下载链接如下：
chromedriver，chromedriver没有64位版本，32即可驱动：
http://chromedriver.storage.googleapis.com/index.html

IEDriverServer，下面链接能够下载所有版本的selenium以及IEDriverServer，IEDriverServer区分32位/64位：
http://selenium-release.storage.googleapis.com/index.html

选择合适的版本并下载即可。

找个容易找到的文件夹放起来，在启动chrome浏览器以及IE时需要用到。

注意：chromedriver、IEDriverServer等浏览器测试驱动都是调用系统的谷歌浏览器和IE浏览器，所以驱动和浏览器客户端必须相互匹配（而最新的测试驱动往往比最新的浏览器差了好几个版本）。所以在下载驱动时尽量下载最新的，在下载浏览器时要尽量使用旧一点的版本。
Selenium Webdriver下载链接
模块名称 	模块描述 	Selenium Webdriver下载链接
Selenium Standalone Server 3.0 	这是Selenium Webdriver的最新稳定版本。你要执行remote Selenium Webdriver时需要它。同时，注意Selenium 3.0+不再支持RC API。你应该用一个备用接口来启动那些旧的东西 	Selenium Webdriver 3.0下载（稳定版本）
Selenium Java 包（3.0.1）、Selenium Python 包（3.0.0） 	这些包包括了一系列的扩展Selenium功能的库 	Selenium Java 包 3.0.1（稳定版本）、Selenium Python 包 3.0.0（稳定版本）
IE Server Driver（2.53.1） 	如果你想要启动IE来做网页测试，你必须有这两个驱动之一。根据你的系统架构来选择。 	32-位 IE Server Driver（稳定版本）、64-位 IE Server Driver（稳定版本）
GECKO Driver（最新版） 	这个驱动是用来支持新版本的Firefox浏览器，从这里下载最新版 	Mozilla GECKO Driver（稳定版本）
Google Chrome Driver（最新版） 	从这里下载最新版本的Google Chrome驱动 	Google Chrome Driver（稳定版本）
Selenium安装链接(谷歌浏览器)

https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd/related
YAML文件语法

YAML 是专门用来写配置文件的语言，非常简洁和强大，远比 JSON 格式方便。它的语法规则可以参考：http://blog.csdn.net/luanpeng825485697/article/details/79478338
GIitHub托管

自动化测试的架构代码托管在github上，读者可以自行下载
https://github.com/626626cdllp/Test/tree/master/Test_framework
自动化测试框架

这里写图片描述

在这个自动化测试框架中。

    在config目录中存放的是测试配置相关的文件，配置文件可以使用ini、xml、yml等文件类型。例如，要测试的网址、调试日志的文件名、日志的输出格式等

    在data目录中存放的是需要测试的数据。可以使用xmls、xml等文件类型。例如，测试网址中要提交的各种各样的内容。

    在drivers目录中存放的是测试需要用到的浏览器驱动。主要为chromedriver.exe、IEDriverServer.exe、phantomjs.exe

    在log目录下存放输出日志.log文件。

    在report目录下存放测试报告文件html类的文件。

    在test目录下存放所有测试相关的文件。

– 在test/case目录下，用于存放测试用例。

– 在test/common目录下，用于存放跟项目、页面无关的封装。

– 在test/interface目录下，用于存放以前台角色测试后台接口的测试用例。

– 在test/page目录下，用于存放具体页面测试时的重复性过程。

– 在test/suite目录下，用于存放测试套件，用来组织用例。

    在utils目录下存放公共方法。

– utils/assertion.py文件用于添加各种自定义的断言（测试结果和目标结果是否一致的判断），断言失败抛出AssertionError就OK。

– utils/client.py文件用于测试web后台接口的前端client，对于HTTP接口添加HTTPClient，发送http请求。还可以封装TCPClient，用来进行tcp链接，测试socket接口等等。

– utils/config.py文件用于项目公共内容配置，以及读取配置文件中的配置。这里配置文件用的yaml，也可用其他如XML,INI等，需在file_reader中添加相应的Reader进行处理。

– utils/extractor.py文件用于抽取器，从响应结果中抽取部分数据，这里实现的是json返回数据的抽取，可以自己添加XML格式、普通字符串格式、Header的抽取器

– utils/file_reader.py文件用于文件的读取,包含配置文件和数据文件的读取函数.根据文件地址，返回文件中包含的内容

– utils/generator.py文件用于一些生成器方法，生成随机数，手机号，以及连续数字等，以便使用这些数据进行测试

– utils/HTMLTestRunner.py是一个第三方模块，用于生成html的测试报告。读者可以不改动它。

– utils/log.py文件通过读取配置文件，定义日志级别、日志文件名、日志格式等。

– utils/mail.py文件用来给指定用户发送邮件。可指定多个收件人，可带附件。

– utils/support.py文件用来编写一些支持方法，比如签名、加密等
相关提示：

pycharm中如果无法引入自定义模块，要先在pycharm中右键点击项目根目录->标记目录为Resource Root，然后再右键点击项目根目录->根源。这样就能引用项目根目录下的所有自定义模块了。
————————————————
版权声明：本文为CSDN博主「数据架构师」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/luanpeng825485697/java/article/details/79457867