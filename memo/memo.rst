.. _memo:

个人备忘录
=====================================================================


Python
---------------------------------------------------------------
.. code-block:: python

   # python起文件服务器
   python3.4 -m http.server
   python -m SimpleHTTPServer    # python2

   # logging
   FATAL(50) > ERROR(40) > WARNING(30) > INFO(20) > DEBUG(10)


Mac
---------------------------------------------------------------
.. code-block:: python

   # 文件字符串批量替换
   find . -name \*.py -exec sed -i '' 's/old/new/g' {} \;
   # copy that data into the system’s paste buffer
   cat file.txt | pbcopy
   # The pbpaste command lets you take data from the system’s paste buffer and write it to standard out.
   pbcopy < birthday.txt
   pbpaste | ag name



Ubuntu相关
---------------------------------------------------------------

.. code-block:: python

    # virtual box虚拟机和windows主机共享目录方法：安装增强工具；win主机设置共享目录例如ubuntu_share；在ubuntu里建立/mnt/share后使用命令：

    sudo mount -t vboxsf ubuntu_share /mnt/share/

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


Git
-------------------------------------------------------------

.. code-block:: python

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


* `《Linux工具快速教程》 <https://linuxtools-rst.readthedocs.io/zh_CN/latest/>`_
