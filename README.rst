===================
Python Web 入坑指南
===================

.. code-block:: text

     ____        _   _                  __        __   _          ____       _     _
    |  _ \ _   _| |_| |__   ___  _ __   \ \      / /__| |__      / ___|_   _(_) __| | ___
    | |_) | | | | __| '_ \ / _ \| '_ \   \ \ /\ / / _ \ '_ \    | |  _| | | | |/ _` |/ _ \
    |  __/| |_| | |_| | | | (_) | | | |   \ V  V /  __/ |_) |   | |_| | |_| | | (_| |  __/
    |_|    \__, |\__|_| |_|\___/|_| |_|    \_/\_/ \___|_.__/     \____|\__,_|_|\__,_|\___|
           |___/


本指南根据作者的自学和工作经历提供(吐槽)一下python
web的学习路线，主要包括概念介绍，参考书籍，开发工具和开发流程等，希望可以帮助非科班人士通过自学入门python
网站开发，弥补学校教育和公司需求之间的鸿沟(也作为自己的学习笔记和面试参考手册)，同时也希望可以作为公司菜鸟实习生的培训手册，帮助公司快速培训新人上手开发，减轻招聘压力。
笔者目前能力有限，希望有经验的python圈人士可以一起协作。
本小书灵感来自于requests库作者的 `python-guide <https://github.com/kennethreitz/python-guide>`_ 。
你可以使用强大的电子书阅读软件 `calibre <https://calibre-ebook.com/>`_ 下载epub格式阅读。


.. image:: https://readthedocs.org/projects/z42/badge/?version=latest

.. code-block:: python

    git clone https://github.com/PegasusWang/python-web-guide.git    # 协作请fork一份你自己的地址
    pip install -r requeirements.txt
    make html
    python3.4 -m http.server
    or
    python -m SimpleHTTPServer    # open _build/html

文档采用rst格式书写，用 `readthedocs <https://readthedocs.org/>`_ 托管。一个快速的rst语法demo `教程 <http://azuwis.github.io/sphinx_demo/demo.html>`_。 如果使用vim编写可以使用rst插件 `riv.vim <https://github.com/Rykka/riv.vim>`_ 配合 `InstantRst <https://github.com/Rykka/InstantRst>`_ 本地预览，定期pull一下拉取更新。
欢迎你fork一份然后添加自己的章节，本书主要面对经验尚浅的同学作为自学的指导手册，并非速成指南，内容来自笔者工作经验总结。
本电子版书集合了同事的智慧结晶，感谢你们带我入坑。
本指南同时会有一些不负责任的吐槽。学到东西的请狂点 star，让笔者有动力更新更多业界实战干货，更多技术分享请关注作者知乎帐号 `pegasuswang <https://www.zhihu.com/people/pegasus-wang/activities>`_ ，知乎专栏 `Python 学习之路 <https://zhuanlan.zhihu.com/c_85234576>`_ ，`个人博客 <http://ningning.today/>`_ 。
笔者还维护了一个 vim 视频教程专栏，感兴趣可以访问 `玩转vim <https://zhuanlan.zhihu.com/vim-video>`_

TODO:
=================================================================
您的打赏就是我写作的最大动力，呵呵哒！

- 面试题指南（包括python、数据结构与算法、http、Linux、数据库、web 框架、系统设计等常考点）

.. raw:: html

   <center>
    <img src="http://7ktuty.com1.z0.glb.clouddn.com/weixin_dashang.png" alt="微信打赏" width=260 height=300>
   </center>
