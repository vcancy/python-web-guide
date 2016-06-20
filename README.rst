===================
python web 入坑指南
===================

本指南提供一个python
web的学习路线，主要包括一些概念介绍和参考书籍，希望可以帮助非专业人士入门python
web相关开发，同时也可以作为公司实习生的指导手册。希望热心的python圈人士可以一起协作。
本小书灵感来自于requests库作者的 `python-guide <http://example.com>`_ 。


.. image:: https://readthedocs.org/projects/z42/badge/?version=latest

.. code-block:: python

    git clone https://github.com/PegasusWang/python-web-guide.git
    pip install -r requeirements.txt
    make html
    python3.4 -m http.server
    or
    python -m SimpleHTTPServer    # open _build/html

文档采用rst格式书写，用 `readthedocs <https://readthedocs.org/>`_ 托管。一个快速的rst语法demo `教程 <http://azuwis.github.io/sphinx_demo/demo.html>`_。 如果使用vim编写可以使用rst插件 `riv.vim <https://github.com/Rykka/riv.vim>`_ 配合 `InstantRst <https://github.com/Rykka/InstantRst>`_ 本地预览。
