.. _codingtools:

开发和编程工具
=====================================================================

..

  Do one thing, and do it well. - A principle of Unix philosopy

工欲善其事，必先利其器(装逼工具)
--------------------------------------------------

- Pycharm。专业的python IDE，功能很强大，特别喜欢它的代码merge工具，不想被编辑器折腾死的推荐直接使用，五星级推荐。(除了内存占用大点)。如果你不喜欢折腾编辑器，请直接用 IDE，经常看见一些用裸编辑器写代码的，代码规范检测都没有。
- vim。本人比较喜欢的编辑器，平常写代码、博客、文档等使用频繁，配上各种插件编辑效率很高。http://vimawesome.com/ 可以到这个上面安装排名靠前的那些插件，能够大大提高编辑效率，部分替代IDE(本人装了六七十个插件，满足各种变态的编辑需求)。其他优秀的编辑器sublime，atom，vscode，emacs等根据个人喜好来吧，不过vim等终端友好的编辑器方便在服务器上直接写代码，和本地体验一样，缺点就是补全和跳转支持不完善，对新人不友好，也可以 Pycharm  和 vim插件配合。(在google搜索python awesome等可以在github上搜索到一些awesome项目，总结了该语言很多技术工具)。网上还有很多牛人开源了自己的 dotfiles，我们可以参考下别人的 vimrc 配置。
- neovim: 新时代的 vim，我在这个配置(https://github.com/PegasusWang/vim-config)上自定义了自己的配置，使用起来性能和反应速度上远超原生的老古董 vim，目前笔者已经全面迁移到 neovim，用着很爽。感兴趣可以关注笔者知乎专栏，我录了一些针对初学者的教学视频。
- oni: https://github.com/onivim/oni/ 构建在 neovim 上的 IDE。还有 VimR 等项目。
- keycastr: mac 按键回显到屏幕，最近录制 vim 视频教程的时候有用到。https://github.com/keycastr/keycastr
- meld/vimdiff: 文本比对工具。
- tmux/tmuxp。比screen好用，可以用来分屏，托管进程等，服务器端必备神器，ubuntu下基本就不用使用terminator之类的分屏工具了。最近看youtube视频还发现有人在服务器上使用tmux和vim结对编程，两个人同时attach到一个session里，基情四射。
- sshfs: 本地挂在服务器文件夹
- tmate: https://tmate.io 终端共享工具，结对编程。很多现代化编辑器 vscode, atom 提供结对编程的插件。
- asciinema: 终端会话记录工具。https://asciinema.org/
- oh-my-zsh。替代原生的bash shell，提供了好多方便的特性和漂亮主题。linux/mac下vim+tmux+zsh简直是绝配，甚至可以直接在服务器上方便地撸代码，跟本地开发体验没区别。
- item2(mac)。替代原生的终端。https://medium.com/@RyanDavidson/make-your-terminal-more-colourful-and-productive-with-iterm2-and-zsh-11b91607b98c
- brew(mac)。类似ubuntu下的apt-get，可以方便安转各种软件和工具。
- Alfred(mac): mac 下一款功能强大的工具，不过我一般只用它快速打开软件。可以用 python 编写一些自己的 workflow 提高效率(https://github.com/deanishe/alfred-workflow)，比如把时间戳转成日期等。 https://github.com/derimagia/awesome-alfred-workflows
- Dash(mac): 强悍的文档查询工具。
- devdocs.io: 文档查询工具
- Karabiner-Elements(mac): 改键工具 https://github.com/tekezo/Karabiner-Elements
- autojump。方便在命令行里来回跳转目录。
- gitx(mac):方便查看代码提交历史，便于了解整个代码仓库是怎样一步步构建的。http://gitx.frim.nl/user_manual.html
- tig: text-mode interface for git. 喜欢命令行的可以尝试下。 https://github.com/jonas/tig
- tldr: 更好的man手册
- EditorConfig: http://editorconfig.org/ 用来统一编辑器配置。如果成员用不同的操作系统和编辑器，建议使用。尤其是对于 python 这种使用缩进的语言
- mac-setup: https://github.com/sb2nov/mac-setup mac 下各种编程语言开发环境配置指引

一定要有个趁手的开发工具(它甚至比你女朋友都重要)，不管是IDE还是编辑器，你程序员生涯的小半辈子都在和它打交道(提升编辑效率的秘诀在于多用键盘快捷键，少用鼠标，以及可以高度定制、和扩展功能的编辑器)。甚至编程字体你都要谨慎选取，比如字体可以很好区分'1', 'l', 'I', '0', 'O', 'S', '5'等易混淆字符，给浏览代码带来便利。如果使用的是mac可以google下 "Mac OS X development environment setup"，有惊喜呦。最后注意你用编辑器的话一定要用 pylint，pep8 检测插件，否则不遵守规范可能会导致用 IDE 打开项目后一堆警告(别人会想问候你祖宗的)。
更多 mac 工具可以参考：https://github.com/jaywcjlove/awesome-mac 。搜 awesome-python 或者 awesome-flask 等有很多类似项目。
一些提升效率的建议：熟悉你的开发工具；学习一门脚本语言（编写自动化脚本）；熟悉 shell 命令；多用键盘快捷键少用鼠标；自动化（比如监听文件变动刷新浏览器、重启http服务等）；用好终端和命令行工具（我建议你用 mac 或者 linux 系统，因为 server 大多跑的 linux，熟悉命令行会给你调试和面试带来便利）

* `《使用vim+tmux+zsh+autojump高效工作》 <http://ningning.today/2016/11/09/tools/vim-tmux-zsh-autojump/>`_


打字速度练习
--------------------------------------
- https://typing.io/
- https://www.keybr.com/
- http://www.speedcoder.net/


Chrome 插件
--------------------------------------
- vimium: chrome 插件，可以用 vim 的方式操作浏览器，很方便，不用鼠标也能完成大部分操作。
- FE助手：前端插件，Json 格式化等很多有用的工具
- octotree: Chrome github 浏览插件

代码辅助和检测工具
--------------------------------------
- pylint: 代码静态检测工具，请务必集成在你的编辑器或者IDE里（推荐）。能帮你少犯很多错误，动态语言写项目要十分谨慎，非常容易犯错。或者在CI加上 hook 每次 push 代码的时候检测。pylintrc 参考：https://github.com/PegasusWang/linux_config/blob/master/pylintrc 这里我忽略了很多无关紧要的提示，默认的 pylint 配置对代码检查实在是太严格了，很多老鸟也过不了。我敢打赌大部分 python 项目用默认 pylint 检查都是不及格分。（pylint 会给代码算个分, 10分制）
- mypy: 类型检查工具
- pep8: python代码风格检测工具(推荐)。懒人可以试试 autopep8 工具，自动格式化。所有人的代码都过一遍 pylint 和 autopep8(放宽行长度) 看起来就比较一致了。甚至可以配置编辑器保存后自动执行 autopep8，类似 gofmt
- autopep8/yapf: python 代码自动格式化工具，懒人必备。都可以集成到 vim 里，比如使用  Plugin 'Chiel92/vim-autoformat'  工具一键格式化。不过注意有时会无法正确处理多重缩进，这个比较危险，代码逻辑都变了，还是自己写代码的时候注意下格式。
- prospector: 集成了众多python代码检测工具
- mccabe: 圈复杂度检测工具。McCabe 是一种度量程序复杂度的方法，如果单个子程序复杂度过高，或许就需要拆分逻辑提高程序的易读性。
- pyflakes
- bandit: 用于Python代码的安全性分析，openstack 的项目 https://github.com/openstack/bandit
- rope，可以用来重构等，功能强大。笔者经常用rope自动帮我重新整理导入的包顺序。
- python-mode: 一个vim插件，有很多 python 补全，语法检测等支持。并且集成了很多 python 工具(pylint,pep8等)，笔者正在用。
- jedi-vim: 一个 vim 插件，python 支持补全和重构。注意和 rope 的自动补全有冲突，不要同时启用。
- Pyreverse: 代码 UML 生成工具, 帮助我们理解继承关系 (https://pythonhosted.org/theape/documentation/developer/explorations/explore_graphs/explore_pyreverse.html)
- Epydoc: Automatic API Documentation Generation for Python
- 2to3/python-modernize: python2 转 python3 工具。目前 Instagram 已经全面迁移到 python3
- 编写2/3兼容代码：http://python-future.org/compatible_idioms.html

* `《[转] Instagram 在 PyCon 2017 的演讲摘要》 <https://zhuanlan.zhihu.com/p/27232791>`_

我觉得对于动态语言使用好静态代码检测工具还是很有必要的，最好集成在你的开发工具里(比如使用vim的python-mode插件可以很容易整合这几个代码检测工具)，辅助你写出高质量代码，否则大型动态语言项目维护起来就是灾难。python会给你一种代码很好写的错觉，不严格要求经常会写出来难以维护的烂代码，甚至导致代码仓库失控。通过 pep8、pylint、mccae 检测过的代码如果警告和错误都消除以后，从代码风格来说基本是没有大问题的，笔者一开始用的时候也是各种警告，修正过很多代码警告以后，以后代码就越来越规范和整洁了。https://github.com/PyCQA 。对于懒人的话直接用 autopep8 ，再也不用纠结格式问题了。目前笔者在公司的一些后端项目中就加入了 flake8 和 pylint 检测（自定义了 pylintrc 文件忽略一些无伤大雅的警告），代码写糙了 CI 都过不了。
我个人强烈建议，所有的人用 isort 整理包导入顺序，用 autopep8 格式化代码，用 pylint 静态检测，（笔者目前的小团队就是这么做的），这样提交的代码格式会非常一致，而且代码非常干净，大项目也不容易失控，动态语言写项目真的很容易出错。能用工具就尽量用工具帮我们解决格式等问题，多余的精力用来思考代码逻辑本身。

项目工具
--------------------------------------
- pigar: 找出项目使用到的依赖库
- buildout: 项目构建工具
- pyenv/virtualenv/pipenv：多版本管理


代码仓库托管
---------------------------------------
- gitlab: 公司用得多
- github: 著名的程序员同性交友网站
- bitbucket: 类似 github，好处是支持免费的私有仓库。当你不想共享代码的时候可以用


脚手架
--------------------------------------
- cookiecutter: 一系列项目模板生成工具，懒人必备。https://github.com/audreyr/cookiecutter。笔者之前内部项目就直接用 flask-cookiecutter 直接生成的。
- yeoman: http://yeoman.io/generators/ 前端项目模板生成工具
- ant-design: 后端管理后台项目解决方案 https://ant.design/docs/react/practical-projects-cn

持续集成
--------------------------------------
- gitlab
- Travis CI
- Jenkins

Api 工具
--------------------------------------
- checklist: http://python.apichecklist.com/

DSL
--------------------------------------
- PLY
- PyParsing: 用来实现 DSL 比较方便。
- Parsley


测试工具
--------------------------------------
- py.test
- nosetest
- unittest
- tox
- mock: mocking makes unit testing easier

文档工具
--------------------------------------
- google doc/石墨: 支持多人协作编辑
- gitbook + markdown: 可以写文档或电子书
- sphinx + readthedoc(或者 mkdocs，支持 markdown) （代码即文档），python 项目很多在用这个生成文档。这本小书就是这么写出来的。`编写《Redis 设计与实现》时用到的工具 <http://blog.huangz.me/diary/2013/tools-for-writing-redisbook.html>`_
- swagger: 适合写 restful 文档
- jupyter(ipython) notebook，可以做笔记或者代码演示或者ppt，支持rst，md等格式，搞数据科学的人用得比较多，配合 RISE (https://github.com/damianavila/RISE) 可以做代码交互式 slideshow，非常好的工具
- Confluence: 适合作为团队的项目文档工具，团队大了以后文档还是很重要的。
- vimwiki/emacs org-mode: 依赖于vim/emacs 编辑器，可以做个人笔记，不过笔者还是比较倾向于独立于编辑器的工具。
- Graphviz: 通过编写代码来生成图片 http://graphviz.org/

日志、异常收集工具
--------------------------------------

- Sentry: 用来记录异常非常好用，能看到完善的栈信息，方便排错。
- Fluentd

管理及运维工具(devops很火)
--------------------------------------
- Supervisor.进程管理
- Fabric.应用部署
- docker.最近比较火的容器技术。很多采用微服务架构的公司使用 docker 作为容器部署服务，或者构建一致的开发环境
- SaltStack和Ansible. 配置管理
- StatsD\Graphite等web监控

调试工具
--------------------------------------
- ipdb/pdb: ipdb 支持自动补全，比原生的 pdb 要好用一些。
- pdbpp: https://pypi.org/project/pdbpp/
- curl
- https://curl.trillworks.com/ 把 curl 命令参数转成 requests 代码。 https://github.com/NickCarneiro/curlconverter/
- httpie
- postman: 接口调试 gui 工具，其实相比gui 工具，笔者更喜欢命令行，比较自由。甚至经常用 requests 发请求来调试 http 接口，因为可以很方便地修改各种 header，请求参数等。
- httpbin.org
- curl/requests 互相转化: https://github.com/oeegor/curlify https://github.com/spulec/uncurl

抓包工具
--------------------------------------
- mitmproxy: 用 python 实现的终端命令行抓包工具，可以将请求直接导出成 python 代码，笔者经常用来抓包和调试。
- charles: 抓包软件(收费)

爬虫相关
--------------------------------------
- Scrapy: 知名的爬虫框架。生态比较丰富
- pyspider: 国人写的一个不错的爬虫框架
- requests: 一般小爬虫用 requests 绰绰有余。
- lxml/BeautifulSoup/pyquery: 解析 html，xml 等。
- tornado: 异步的 http client 可以写爬虫
- redis/celery: 实现队列、异步爬虫。异步方案也比较多
- phantomjs/puppeteer: 用来处理动态网站。puppeteer 基于 nodejs

RPC
--------------------------------------
- thrift: facebook 开源的 rpc 框架
- grpc: grpc是一个高性能、开源和通用的 RPC 框架，面向移动和 HTTP/2 设计。目前提供 C、Java 和 Go 语言版本，分别是：grpc, grpc-java, grpc-go. 其中 C 版本支持 C, C++, Node.js, Python, Ruby, Objective-C, PHP 和 C# 支持. https://github.com/grpc/grpc

Rest
--------------------------------------
- 随便搜吧，各种框架都有，一大把

数据处理
--------------------------------------
- pandas: 处理报表经常用，适合处理矩阵(DataFrame)、excel 等。配合一些前端可视化库可以弄报表啥的。
- matplotlib: python 绘图


压测工具
--------------------------------------
- locust: python实现的压测工具。http://locust.io/， 有 web 界面
- ab
- wrk


Profiler
--------------------------------------
- pyflame: https://github.com/uber/pyflame


数据库工具
--------------------------------------
- mycli: mysql 命令行补全等。https://github.com/dbcli/mycli
- MysqlWorkbench/Sequel Pro: mysql 客户端工具。
- Navicat Premium: 强大的数据库管理工具，收费
- Medis: redis client 工具
- MongoChef: Mongodb 客户端工具

绘图工具
--------------------------------------
- processon: http://processon.com/ 使用了下感觉还不错，基本能满足需求
- draw.io: https://www.draw.io/

量化投资
--------------------------------------
- tushare: https://github.com/waditu/tushare 有本小白参考书: https://wizardforcel.gitbooks.io/python-quant-uqer/

效率工具
--------------------------------------
- 番茄工作法：人长期专注的时间是有限的，找到适合自己的最佳番茄钟，并且每个时间段都专注于一件事，每件事分清轻重缓急，要事优先。在休息时间处理喝水、上厕所等杂事，做几个深呼吸给脑瓜子充点氧，或者活动下筋骨，眺望下远处。预防职业病（最近有看到工程师视网膜脱落的，要重视身体健康）。
- teambiation/trello: todo list 工具，管理任务。今天做了什么；计划做什么；哪些困难导致工作被阻塞(实在搞不定的记下来及时向同事求助)；发现了什么问题；今天学到了什么。(类似于开发日志之类的玩意，每天都是真正做了事情的，并且最好每天都是学到了新东西的)
- 音乐：选择类似于《阿尔法波高效记忆音乐》《巴洛克学习音乐》等，能帮助你隔绝噪音。反正笔者听歌的时候会想歌词反而会打扰思路，一般就是听这种不怎么让你瞎想的音乐。
- 复盘。无论是写代码、做需求、改bug等，事后反思总结。分析并且记录耗时的地方和可以改进的地方(怎么让自己涨点记性，整理 checklist)，对于一些错误或者坑也可以记录成文档当做团队的知识财富。
- zapier: https://zapier.com/ 一个连接 app 自动化工作流的工具，比如可以用来定期提醒发邮件等，非程序员也能实现定时任务啦
