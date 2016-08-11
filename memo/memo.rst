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



Linux相关
---------------------------------------------------------------

virtual box虚拟机和windows主机共享目录方法：安装增强工具；win主机设置共享目录例如ubuntu_share；在ubuntu里建立/mnt/share后使用命令：

`sudo mount -t vboxsf ubuntu_share /mnt/share/`

文件字符串批量替换
`grep oldString -rl /path | xargs sed -i "s/oldString/newString/g"`

递归删除某一类型文件
`find . -name "*.bak" -type f -delete`


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


* `《Linux工具快速教程》 <https://linuxtools-rst.readthedocs.io/zh_CN/latest/>`_
