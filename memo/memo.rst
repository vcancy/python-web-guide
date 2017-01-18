.. _memo:

个人备忘录
=====================================================================


Python
---------------------------------------------------------------
.. code-block:: python

   # python起文件服务器
   python3.4 -m http.server
   python -m SimpleHTTPServer    # python2

   python -u    # 刷新缓冲，执行脚本重定向结果到文件时候比较有用

   # logging
   FATAL(50) > ERROR(40) > WARNING(30) > INFO(20) > DEBUG(10)

   # 使用virtualenv制定python版本
   virtualenv -p /usr/bin/python2.7 ENV2.7


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

    # 可以把代码文件贴到paste.ubuntu.com共享，此命令返回一个网址sudo apt-get install pastebinit
    pastebinit -i [filename]


    # json格式化输出
    echo '{"foo": "lorem", "bar": "ipsum"}' | python -m json.tool
    python -m json.tool my_json.json
    # 或者apt-get intsall jq
    jq . <<< '{ "foo": "lorem", "bar": "ipsum"  }'


    # 进程相关
    dmesg | egrep -i -B100 'killed process'   # 查看被杀死进程信息

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


    @single_process    # 保证不会同时执行，原理请看single_process源码
    def main():
        time.sleep(10)
        print(time.time())

    if __name__ == '__main__':
        main()


* `《crontab快速参考》 <http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/crontab.html>`_

Tmux
-------------------------------------------------------------

.. code-block:: python

   tmux rename -t oriname newname
   tmux att -t name -d               # -d 不同窗口全屏
   # 如果手贱在本机tmux里又ssh到服务器又进入服务器的tmux怎么办
   c-b c-b d


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

    # 手残pull错了分支就
    git reset --hard HEAD~
    # 手残add错了就
    git reset file # git reset 撤销所有add

    # 指定文件类型diff
    git diff master -- '*.c' '*.h'
    # 带有上下文的diff
    git diff master --no-prefix -U999

    # undo add
    git reset <file>
    git reset    # undo all

    # 查看add后的diff
    git diff --staged

    # rebase改变历史, 永远不要用在master分之，别人有可能使用你的分之时也不要用
    # only change history for commits that have not yet been pushed
    # master has changed since I stared my feature branch, and I want bo bring my branch up to date with master. - Dont't merge. rebase
    # rebase: finds the merge base; cherry-picks all commits; reassigns the branch pointer.
    # then git push -f
    # git rebase --abort


Git工作流
------------

.. code-block:: shell

   git checkout master    # 切到master
   git pull origin master     # 拉取更新
   git checkout -b newbranch    # 新建分之，名称最好起个有意义的，比如jira号等

   # 开发中。。。
   git fetch origin master    # fetch master
   git rebase origin/master    #

   # 开发完成等待合并到master
   git rebase -i origin/master
   git checkout master
   git merge newbranch
   git push origin master


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


* `《Linux工具快速教程》 <https://linuxtools-rst.readthedocs.io/zh_CN/latest/>`_
* `《slide show》 <http://slideshow-s9.github.io/>`_
* `《markdown sheet》 <http://commonmark.org/help/>`_
* `《CONQUERING THE COMMAND LINE》 <http://conqueringthecommandline.com/book/>`_
