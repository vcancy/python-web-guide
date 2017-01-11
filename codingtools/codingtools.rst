.. _codingtools:

开发和编程工具
=====================================================================


开发工具（很多只列举个名字，具体使用请自行google）
--------------------------------------------------

- Pycharm。专业的python ide，功能很强大，特别喜欢它的代码merge工具，不想被编辑器折腾死的推荐直接使用。
- vim。本人比较喜欢，配上各种插件编辑效率很高。http://vimawesome.com/ 可以到这个上面安装排名靠前的那些插件，能够大大提高编辑效率，替代IDE。其他编辑器sublime，atom，vscode，emacs等不熟，根据个人喜好来吧。(在google搜索python awesome等可以在github上搜索到一些awesome项目，总结了该语言很多技术工具)
- tmux。比screen好用，可以用来分屏等，ubuntu下基本就不用使用terminator之类的分屏工具了
- zsh。替代原生的bash shell，提供了好多方便的特性。linux/mac下vim+tmux+zsh简直是绝配，甚至可以直接在服务器上方便地撸代码。
- item2(mac)。替代原生的终端。
- brew(mac)。类似ubuntu下的apt-get，可以方便安转各种软件和工具。
- autojump。方便在命令行里来回跳转。

一定要有个趁手的开发工具，不管是IDE还是编辑器，你程序员生涯的小半辈子都在和它打交道。甚至编程字体你都要谨慎选取，比如字体可以很好区分'1','l','0','O'等，给浏览代码带来便利。

* `《使用vim+tmux+zsh+autojump高效工作》 <http://ningning.today/2016/11/09/tools/vim-tmux-zsh-autojump/>`_

代码检测工具
--------------------------------------
- pylint
- pyflake

我觉得对于动态语言使用好静态代码检测工具还是很有必要的，最好集成在你的开发工具里(比如使用vim的python-mode插件可以很容易整合这几个代码检测工具)，辅助你写出高质量代码。python会给你一种代码很好写的错觉，不严格要求经常会写出来难以维护的烂代码。


日志收集工具
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
