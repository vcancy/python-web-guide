.. _memo:

个人备忘录
=====================================================================


Python
---------------------------------------------------------------
.. code-block:: python

   # python起文件服务器
   python3.4 -m http.server
   python -m SimpleHTTPServer    # python2

   python -u script.py   # 刷新缓冲，执行脚本重定向结果到文件时候比较有用

   # logging
   FATAL(50) > ERROR(40) > WARNING(30) > INFO(20) > DEBUG(10)

   # 使用virtualenv制定python版本
   virtualenv -p /usr/bin/python2.7 ENV2.7

   # pyenv 安装多个版本的 python : https://github.com/pyenv/pyenv
   # pyenv-virtualenv https://github.com/pyenv/pyenv-virtualenv

   # 格式化 json
   cat some.json | python -m json.tool

   # brew install youtube-dl
   # https://askubuntu.com/questions/486297/how-to-select-video-quality-from-youtube-dl
   youtube-dl "http://www.youtube.com/watch?v=P9pzm5b6FFY"


Pip
---------------------------------------------------------------
.. code-block:: python

   # https://stackoverflow.com/questions/12332975/installing-python-module-within-code
   # pip install
   import pip

   def install(package):
       pip.main(['install', package])

   # Example
   if __name__ == '__main__':
       install('argh')


IPython
---------------------------------------------------------------
.. code-block:: python

   # -*- coding: utf-8 -*-

   # ~/.ipython/profile_default/startup/startup.py
   # Ned's .startup.py file    ipython 启动加载文件，用来导入一些自定义函数或者模块，方便调试
   # http://stackoverflow.com/questions/11124578/automatically-import-modules-when-entering-the-python-or-ipython-interpreter

   print("(.startup.py)")

   import datetime as dt
   import os
   import pprint
   import re
   import sys
   import time
   import json
   import requests as req

   try:
       import matplotlib.pyplot as plt
       import pandas as pd
       from pandas import Series, DataFrame
       import numpy as np
   except ImportError:
       pass

   print("(imported datetime, os, pprint, re, sys, time, json)")
   pp = pprint.pprint


   def repr_dict(d):
       """https://stackoverflow.com/questions/25118698/print-python-dictionary-with-utf8-values"""
       print '{%s}' % ',\n'.join("'%s': '%s'" % pair for pair in d.iteritems())

Ipdb
---------------------------------------------------------------
.. code-block:: python

   # ~/.pdbrc
   # https://github.com/gotcha/ipdb/issues/111

   import os
   alias kk os._exit(0)    # 如果不幸在循环里打了断点，可以用 os._exit(0) 跳出

   alias pd for k in sorted(%1.keys()): print "%s: %s" % (k, (%1[k]))

   # https://stackoverflow.com/questions/21123473/how-do-i-manipulate-a-variable-whose-name-conflicts-with-pdb-commands
   # 如果 pdb 里的内置命令和内置函数冲突了，可以加上 ! 使用内置函数
   !next(iter)

Mac
---------------------------------------------------------------
.. code-block:: python

   # 文件字符串批量替换，git项目里替换的时候注意指定文件类型，防止破坏git信息
   find . -name \*.py -exec sed -i '' 's/old/new/g' {} \;
   # copy that data into the system’s paste buffer
   cat file.txt | pbcopy
   # The pbpaste command lets you take data from the system’s paste buffer and write it to standard out.
   pbcopy < birthday.txt
   pbpaste | ag name
   pbpaste > filename

   # updatedb https://superuser.com/questions/109590/whats-the-equivalent-of-linuxs-updatedb-command-for-the-mac
   sudo /usr/libexec/locate.updatedb

   # homebrew 更换源, https://maomihz.com/2016/06/tutorial-6/
   cd /usr/local
   git remote set-url origin git://mirrors.ustc.edu.cn/brew.git

   cd /usr/local/Library/Taps/homebrew/homebrew-core
   git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git

   # 从终端查 wifi 密码, https://apple.stackexchange.com/questions/176119/how-to-access-the-wi-fi-password-through-terminal
   security find-generic-password -ga "ROUTERNAME" | grep "password:"


如何发送 mac 通知，可以用来做提示

.. code-block:: python

   # https://stackoverflow.com/questions/17651017/python-post-osx-notification

   import os

   def notify(title, text):
       os.system("""
                 osascript -e 'display notification "{}" with title "{}"'
                 """.format(text, title))

   notify("开会啦", "Go Go Go !!!")


Zsh
---------------------------------------------------------------
.. code-block:: shell

   # Powerlevel9k 是一个强大的 zsh 主题
   # iTerm2 + Oh My Zsh + Solarized color scheme + Meslo powerline font + [Powerlevel9k] - (macOS)
   # https://gist.github.com/kevin-smets/8568070


Ubuntu相关
---------------------------------------------------------------

.. code-block:: python

    # 查看版本
    lsb_release -a

    # virtual box虚拟机和windows主机共享目录方法：安装增强工具；win主机设置共享目录例如ubuntu_share；在ubuntu里建立/mnt/share后使用命令：

    sudo mount -t vboxsf ubuntu_share /mnt/share/

    # 映射capslock 为　ctrl
    setxkbmap -layout us -option ctrl:nocaps

    # 文件字符串批量替换
    grep oldString -rl /path | xargs sed -i "s/oldString/newString/g"

    # 递归删除某一类型文件
    find . -name "*.bak" -type f -delete

    # 监控某一日志文件变化
    tail -f t.log

    # 类似mac pbcopy, apt-get install xsel
    cat README.TXT | xsel
    cat README.TXT | xsel -b # 如有问题可以试试-b选项
    xsel < README.TXT
    # 将readme.txt的文本放入剪贴板

    xsel -c
    # 清空剪贴板

    # 可以把代码文件贴到paste.ubuntu.com共享，此命令返回一个网址
    # sudo apt-get install pastebinit; sudo pip install configobj
    pastebinit -i [filename]


    # json格式化输出
    echo '{"foo": "lorem", "bar": "ipsum"}' | python -m json.tool
    python -m json.tool my_json.json
    # 或者apt-get intsall jq
    jq . <<< '{ "foo": "lorem", "bar": "ipsum"  }'


    # 进程相关
    dmesg | egrep -i -B100 'killed process'   # 查看被杀死进程信息

    # scp
    scp someuser@192.168.199.1:/home/someuser/file ./    # 远程机器拷贝到本机
    scp ./file someuser@192.168.199.1:/home/someuser/    # 拷贝到远程机器

    # tar
    tar zxvf FileName.tar.gz    # 解压
    tar zcvf FileName.tar.gz DirName    # 压缩

代码搜索用ag, 比ack快

.. code-block:: python

    sudo apt-get install silversearcher-ag    # ubuntu
    brew install ag
    ag string dir/    # search dir
    ag readme$    # regular expression
    ag -Q .rb    # Literal Expression Searches, search for the exact pattern
    ag string -l    # Listing Files (-l)
    ag string -i    # Case Insensitive Searches (-i)
    ag string -G py$    # 搜索应py结尾的文件
    ag readme -l --ignore-dir=railties/lib    # 忽略文件夹
    ag readme -l --ignore-dir="*.rb"    # 忽略特性类型文件
    .agignore    # 用来忽略一些vcs，git等文件。


crontab
-------------------------------------------------------------
分、时、日、月、周

.. code-block:: python

    # 记得bashrc里边
    EXPORT EDITOR=vim
    export PYTHONIOENCODING=UTF-8

    # crontab注意：绝对路径；环境变量；
    0 */5 * * * python -u /root/wechannel/crawler/sougou_wechat/sougou.py >> /root/wechannel/crawler/sougou_wechat/log 2>&1
    */5 * *  * * /root/pyhome/crawler/lagou/changeip.sh >> /root/pyhome/crawler/lagou/ip.log 2>&1


可以用如下方式执行依赖其他模块的python脚本，用run.sh执行run.py，记得chmod +x可执行权限，运行前执行下sh脚本测试能否成功

.. code-block:: python

    #!/usr/bin/env bash
    PREFIX=$(cd "$(dirname "$0")"; pwd)
    cd $PREFIX
    source ~/.bashrc

    python -u run.py    # -u 参数强制刷新输出
    date


对于python脚本，给main函数加上装饰器@single_process可以保证只有一个该脚本会执行, pip install single_process，比如下面这个run.py

.. code-block:: shell

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-

    import time
    from single_process import single_process    # pip install single_process


    @single_process    # 保证不会同时执行，原理请看single_process源码。新版本貌似改了用法，非装饰器
    def main():
        time.sleep(10)
        print(time.time())

    if __name__ == '__main__':
        main()


* `《crontab快速参考》 <http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/crontab.html>`_


Iterm2
-------------------------------------------------------------

.. code-block:: sh

   # https://stackoverflow.com/questions/11913990/iterm2-keyboard-shortcut-for-moving-tabs-around
   # Preferences/Keys 自定义配置使用 Cmd +jk 来在 Iterm2 tab 前后移动，模仿 vim 键位


Tmux
-------------------------------------------------------------

.. code-block:: sh

   tmux rename -t oriname newname
   tmux att -t name -d               # -d 不同窗口全屏
   # 如果手贱在本机tmux里又ssh到服务器又进入服务器的tmux怎么办
   c-b c-b d

   # Vim style pane selection
   bind -n C-h select-pane -L
   bind -n C-j select-pane -D
   bind -n C-k select-pane -U
   bind -n C-l select-pane -R

SSH
-------------------------------------------------------------

.. code-block:: python

   # https://superuser.com/questions/98562/way-to-avoid-ssh-connection-timeout-freezing-of-gnome-terminal/98565#98565
   Press Enter, ~, . one after the other to disconnect from a frozen session.

Git
-------------------------------------------------------------

.. code-block:: python

    # .gitconfig配置用如下配置可以使用pycharm的diff和merge工具（已经安装pycharm）
    [diff]
        tool = pycharm
    [difftool "pycharm"]
        cmd = /usr/local/bin/charm diff "$LOCAL" "$REMOTE" && echo "Press enter to continue..." && read
    [merge]
        tool = pycharm
        keepBackup = false
    [mergetool "pycharm"]
        cmd = /usr/local/bin/charm merge "$LOCAL" "$REMOTE" "$BASE" "$MERGED"

    # https://stackoverflow.com/questions/34549040/git-not-displaying-unicode-file-names
    # git 显示中文文件名
    git config --global core.quotePath false

    # 用来review：
    git log --since=1.days --committer=PegasusWang --author=PegasusWang
    git diff commit1 commit2

    # 冲突以后使用远端的版本：
    git checkout --theirs templates/efmp/campaign.mako

    # 防止http协议每次都要输入密码：
    git config --global credential.helper 'cache --timeout=36000000'      #秒数

    # 暂存和恢复
    git stash
    git stash apply
    git stash apply stash@{1}
    git stash pop # 重新应用储藏并且从堆栈中移走

    # 删除远程分之
    git push origin --delete {the_remote_branch}

    # 手残 add 完以后输入错了 commit 信息
    git commit --amend

    # 撤销 add （暂存）
    git reset -- file

    # 撤销修改
    git checkout -- file

    # 手残pull错了分支就
    git reset --hard HEAD~

    # How to revert Git repository to a previous commit?, https://stackoverflow.com/questions/4114095/how-to-revert-git-repository-to-a-previous-commit
    git reset --hard 0d1d7fc32

    # 手残直接在master分之改了并且add了
    git reset --soft HEAD^
    git branch new_branch # 切到一个新分支去 commit
    git checkout new_branch
    git commit -a -m "..."
    # 或者
    git reset --soft HEAD^
    git stash
    git checkout new_branch
    git stash pop

    # 如果改了master但是没有add比较简单，三步走
    git stash
    git checkout -b new_branch
    git stash pop

    # rename branch
    git branch -m <oldname> <newname>
    git branch -m <newname> # rename the current branch

    # 指定文件类型diff
    git diff master -- '*.c' '*.h'
    # 带有上下文的diff
    git diff master --no-prefix -U999

    # undo add
    git reset <file>
    git reset    # undo all

    # 查看add后的diff
    git diff --staged

    # http://weizhifeng.net/git-rebase.html
    # rebase改变历史, 永远不要用在master分之，别人有可能使用你的分之时也不要用
    # only change history for commits that have not yet been pushed
    # master has changed since I stared my feature branch, and I want bo bring my branch up to date with master. - Dont't merge. rebase
    # rebase: finds the merge base; cherry-picks all commits; reassigns the branch pointer.
    # then git push -f
    # git rebase --abort

    # 全局 ignore, 对于不同编辑器协作的人比较有用，或者用来单独忽略一些自己建立的测试文件等
    git config --global core.excludesfile ~/.gitignore_global

    # 拉取别人远程分支，在 .git/config 里配置好
    git fetch somebody somebranch
    git checkout -b somebranch origin/somebranch


Git工作流
------------

.. code-block:: shell

   git checkout master    # 切到master
   git pull origin master     # 拉取更新
   git checkout -b newbranch    # 新建分之，名称最好起个有意义的，比如jira号等

   # 开发中。。。
   git fetch origin master    # fetch master
   git rebase origin/master    #

   # 开发完成等待合并到master，推荐使用 rebase 保持线性的提交历史，但是记住不要在公众分之搞，如果有无意义的提交也可以用 rebase -i 压缩提交
   git rebase -i origin/master
   git checkout master
   git merge newbranch
   git push origin master

   # 压缩提交
   git rebase -i HEAD~~    # 最近两次提交


Git hook
------------
比如我们要在每次 commit 之前运行下单测，进入项目的 .git/hooks 目录， "cp pre-commit.sample pre-commit" 修改内容如下:

.. code-block:: bash

    #!/bin/sh

    if git rev-parse --verify HEAD >/dev/null 2>&1
    then
        against=HEAD
    else
        # Initial commit: diff against an empty tree object
        against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
    fi

    # Redirect output to stderr.
    exec 1>&2

    if /your/path/bin/test:    # 这里添加需要运行的测试脚本
    then
        exit 0
    else
        exit 1
    fi

    # If there are whitespace errors, print the offending file names and fail.
    exec git diff-index --check --cached $against --


vim
----

.. code-block:: vim

    " http://stackoverflow.com/questions/9104706/how-can-i-convert-spaces-to-tabs-in-vim-or-linux
   :set tabstop=2      " To match the sample file
   :set noexpandtab    " Use tabs, not spaces
   :%retab!            " Retabulate the whole file，替换tab为空格
   map <F4> :%retab! <CR> :w <CR> " 映射一个命令

   "https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjF6JzH8aTRAhXiqVQKHUQBDcIQFggcMAA&url=http%3A%2F%2Fstackoverflow.com%2Fquestions%2F71323%2Fhow-to-replace-a-character-by-a-newline-in-vim&usg=AFQjCNGer9onNl_RExCUdE75ctTvVx8WGA&sig2=WrcRh9RFNvN6bUZoHpJvDg
   "vim替换成换行符使用\r不是\n
   " 多行加上引号 http://stackoverflow.com/questions/9055998/vim-add-tag-to-multiple-lines-with-surround-vim"
   :1,3norm yss"

   # Git 插件
   Plugin 'tpope/vim-fugitive' # 在 vim 里执行 :Gblame 可以看到当前文件每行代码的提交人和日期，找人背锅或者咨询的神器

   # 直接在 vim 里 diff 文件，比如打开了两个文件
   :windo diffthis
   :diffoff!

* `《vim cheet sheet》 <https://vim.rtorr.com/lang/zh_cn/>`_

用markdown文件制作html ppt
-------------------------------------------------------------

.. code-block:: python

   apt-add-repository ppa:brightbox/ruby-ng
   apt-get update
   apt-get install ruby2.2
   gem install slideshow
   slideshow install deck.js
   sudo  pip install https://github.com/joh/when-changed/archive/master.zip
   when-changed rest.md slideshow  build rest.md -t deck.js

   # mac: brew install fswatch, http://stackoverflow.com/questions/1515730/is-there-a-command-like-watch-or-inotifywait-on-the-mac
   jfswatch -o ~/path/to/watch | xargs -n1 ~/script/to/run/when/files/change.sh
   fswatch -o ./*.py  | xargs -n1  ./runtest.sh    # 比如写单元测试的时候修改后就让测试执行

   # 也可以使用下边的工具用 Jupyter 做 slideshow，最大的特点是直接在浏览器里敲代码交互演示
   # Reveal.js - Jupyter/IPython Slideshow Extension, also known as live_reveal
   # https://github.com/damianavila/RISE

Benchmark
-------------------------------------------------------------

.. code-block:: shell

    sudo apt-get install apache2-utils
    ab -c 并发数量 -n 总数量 url

* `《Linux工具快速教程》 <https://linuxtools-rst.readthedocs.io/zh_CN/latest/>`_
* `《slide show》 <http://slideshow-s9.github.io/>`_
* `《markdown sheet》 <http://commonmark.org/help/>`_
* `《CONQUERING THE COMMAND LINE》 <http://conqueringthecommandline.com/book/>`_
