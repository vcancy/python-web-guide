.. _codingtools:

开发和编程工具
=====================================================================


工欲善其事，必先利其器
--------------------------------------------------

- Pycharm。专业的python IDE，功能很强大，特别喜欢它的代码merge工具，不想被编辑器折腾死的推荐直接使用。
- vim。本人比较喜欢的编辑器，平常写代码、博客、文档等使用频繁，配上各种插件编辑效率很高。http://vimawesome.com/ 可以到这个上面安装排名靠前的那些插件，能够大大提高编辑效率，部分替代IDE。其他优秀的编辑器sublime，atom，vscode，emacs等不熟，根据个人喜好来吧。(在google搜索python awesome等可以在github上搜索到一些awesome项目，总结了该语言很多技术工具)
- tmux。比screen好用，可以用来分屏，托管进程等，ubuntu下基本就不用使用terminator之类的分屏工具了。最近看youtube视频还发现有人在服务器上使用tmux和vim结对编程，两个人同时attach到一个session里，基情四射。
- zsh。替代原生的bash shell，提供了好多方便的特性和漂亮主题。linux/mac下vim+tmux+zsh简直是绝配，甚至可以直接在服务器上方便地撸代码，跟本地开发体验没区别。
- item2(mac)。替代原生的终端。
- brew(mac)。类似ubuntu下的apt-get，可以方便安转各种软件和工具。
- autojump。方便在命令行里来回跳转目录。
- gitx(mac):方便查看代码提交历史，便于了解整个代码仓库是怎样一步步构建的。http://gitx.frim.nl/user_manual.html
- tldr: 更好的man手册

一定要有个趁手的开发工具，不管是IDE还是编辑器，你程序员生涯的小半辈子都在和它打交道。甚至编程字体你都要谨慎选取，比如字体可以很好区分'1','l','0','O'等易混淆字符，给浏览代码带来便利。如果使用的是mac可以google下 "Mac OS X development environment setup"，有惊喜呦。

* `《使用vim+tmux+zsh+autojump高效工作》 <http://ningning.today/2016/11/09/tools/vim-tmux-zsh-autojump/>`_

代码辅助和检测工具
--------------------------------------
- prospector: 集成了众多python代码检测工具
- pylint: 最好集成在你的编辑器或者IDE里
- pyflake
- bandit: 用于Python代码的安全性分析，openstack 的项目 https://github.com/openstack/bandit
- rope，可以用来重构等，功能强大。笔者经常用rope自动帮我重新整理导入的包顺序。

我觉得对于动态语言使用好静态代码检测工具还是很有必要的，最好集成在你的开发工具里(比如使用vim的python-mode插件可以很容易整合这几个代码检测工具)，辅助你写出高质量代码，否则大型动态语言项目维护起来就是灾难。python会给你一种代码很好写的错觉，不严格要求经常会写出来难以维护的烂代码，甚至导致代码仓库失控。


日志、异常收集工具
--------------------------------------

- Sentry.
- Fluentd


管理及运维工具
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
