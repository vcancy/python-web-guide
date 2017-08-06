.. _codingtools:

开发和编程工具
=====================================================================


工欲善其事，必先利其器(装逼工具)
--------------------------------------------------

- Pycharm。专业的python IDE，功能很强大，特别喜欢它的代码merge工具，不想被编辑器折腾死的推荐直接使用，五星级推荐。(除了内存占用大点)
- vim。本人比较喜欢的编辑器，平常写代码、博客、文档等使用频繁，配上各种插件编辑效率很高。http://vimawesome.com/ 可以到这个上面安装排名靠前的那些插件，能够大大提高编辑效率，部分替代IDE(本人装了六七十个插件，满足各种变态的编辑需求)。其他优秀的编辑器sublime，atom，vscode，emacs等不熟，根据个人喜好来吧，不过vim等终端友好的编辑器方便在服务器上直接写代码，缺点就是补全和跳转支持不完善，也可以 Pycharm  和 vim插件配合。(在google搜索python awesome等可以在github上搜索到一些awesome项目，总结了该语言很多技术工具)。网上还有很多牛人开源了自己的 dotfiles，我们可以参考下别人的 vimrc 配置。
- meld/vimdiff: 文本比对工具。
- tmux。比screen好用，可以用来分屏，托管进程等，服务器端必备神器，ubuntu下基本就不用使用terminator之类的分屏工具了。最近看youtube视频还发现有人在服务器上使用tmux和vim结对编程，两个人同时attach到一个session里，基情四射。
- oh-my-zsh。替代原生的bash shell，提供了好多方便的特性和漂亮主题。linux/mac下vim+tmux+zsh简直是绝配，甚至可以直接在服务器上方便地撸代码，跟本地开发体验没区别。
- item2(mac)。替代原生的终端。
- brew(mac)。类似ubuntu下的apt-get，可以方便安转各种软件和工具。
- Alfred(mac): mac 下一款功能强大的工具，不过我一般只用它快速打开软件。
- Dash(mac): 强悍的文档查询工具。
- Karabiner-Elements(mac): 改键工具 https://github.com/tekezo/Karabiner-Elements
- autojump。方便在命令行里来回跳转目录。
- gitx(mac):方便查看代码提交历史，便于了解整个代码仓库是怎样一步步构建的。http://gitx.frim.nl/user_manual.html
- tig: text-mode interface for git. 喜欢命令行的可以尝试下。 https://github.com/jonas/tig
- tldr: 更好的man手册
- EditorConfig: http://editorconfig.org/ 用来统一编辑器配置

一定要有个趁手的开发工具(它甚至比你女朋友都重要)，不管是IDE还是编辑器，你程序员生涯的小半辈子都在和它打交道(提升编辑效率的秘诀在于多用键盘快捷键，少用鼠标，以及可以高度定制的编辑器)。甚至编程字体你都要谨慎选取，比如字体可以很好区分'1', 'l', 'I', '0', 'O', 'S', '5'等易混淆字符，给浏览代码带来便利。如果使用的是mac可以google下 "Mac OS X development environment setup"，有惊喜呦。最后注意你用编辑器的话一定要用 pylint，pep8 检测插件，否则不遵守规范可能会导致用 IDE 打开项目后一堆警告(别人会想问候你祖宗的)。

* `《使用vim+tmux+zsh+autojump高效工作》 <http://ningning.today/2016/11/09/tools/vim-tmux-zsh-autojump/>`_

代码辅助和检测工具
--------------------------------------
- pylint: 代码静态检测工具，请务必集成在你的编辑器或者IDE里（推荐）。能帮你少犯很多错误，动态语言写项目要十分谨慎，非常容易犯错。或者在CI加上 hook 每次 push 代码的时候检测。
- pep8: python代码风格检测工具(推荐)。懒人可以试试 autopep8 工具，自动格式化。所有人的代码都过一遍 pylint 和 autopep8(放宽行长度) 看起来就比较一致了。
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


我觉得对于动态语言使用好静态代码检测工具还是很有必要的，最好集成在你的开发工具里(比如使用vim的python-mode插件可以很容易整合这几个代码检测工具)，辅助你写出高质量代码，否则大型动态语言项目维护起来就是灾难。python会给你一种代码很好写的错觉，不严格要求经常会写出来难以维护的烂代码，甚至导致代码仓库失控。通过 pep8、pylint、mccae 检测过的代码如果警告和错误都消除以后，从代码风格来说基本是没有大问题的，笔者一开始用的时候也是各种警告，修正过很多代码警告以后，以后代码就越来越规范和整洁了。https://github.com/PyCQA

项目工具
--------------------------------------
- pigar: 找出项目使用到的依赖库
- buildout: 项目构建工具
- pyenv/virtualenv： 多版本管理

Api 工具
--------------------------------------
- checklist: http://python.apichecklist.com/

DSL
--------------------------------------
- PLY
- PyParsing
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
- google doc
- gitbook + markdown
- sphinx + readthedoc （代码即文档），python 项目很多在用这个生成文档
- swagger: 适合写 restful 文档
- jupyter notebook，可以做笔记或者代码演示或者ppt，支持rst，md等格式，搞数据科学的人用得比较多，配合 RISE (https://github.com/damianavila/RISE) 可以做代码交互式 slideshow，非常好的工具
- Confluence: 适合作为团队的项目文档工具，团队大了以后文档还是很重要的。

日志、异常收集工具
--------------------------------------

- Sentry
- Fluentd

管理及运维工具(devops很火)
--------------------------------------
- Supervisor.进程管理
- Fabric.应用部署
- docker.最近比较火的容器技术
- SaltStack和Ansible. 配置管理
- StatsD\Graphite等web监控

调试工具
--------------------------------------
- ipdb/pdb
- curl
- http
- postman

抓包工具
--------------------------------------
- mitmproxy: 用 python 实现的终端命令行抓包工具
- charles: 抓包软件(收费)

压测工具
--------------------------------------
- locust: python实现的压测工具。http://locust.io/
- ab

数据库工具
--------------------------------------
- mycli: mysql 命令行补全等。https://github.com/dbcli/mycli
- MysqlWorkbench/Sequel Pro: mysql 客户端工具。

效率工具
--------------------------------------
- 番茄工作法：人长期专注的时间是有限的，找到适合自己的最佳番茄钟，并且每个时间段都专注于一件事，每件事分清轻重缓急，要事优先。在休息时间处理喝水、上厕所等杂事，做几个深呼吸给脑瓜子充点氧。《精力管理》
- teambiation/trello: todo list 工具。今天做了什么；计划做什么；哪些困难导致工作被阻塞(实在搞不定的记下来及时向同事求助)；发现了什么问题；今天学到了什么。(类似于开发日志之类的玩意，每天都是真正做了事情的，并且最好每天都是学到了新东西的)
- 音乐：选择类似于《阿尔法波高效记忆音乐》《巴洛克学习音乐》等，能帮助你隔绝噪音。反正笔者听歌的时候会想歌词反而会打扰思路，一般就是听这种不怎么让你瞎想的音乐。
- 复盘。无论是写代码、做需求、改bug等，事后反思总结。分析并且记录耗时的地方和可以改进的地方(怎么让自己涨点记性)，对于一些错误或者坑也可以记录成文档当做团队的知识财富。
