.. _codingstyle:

编码之前碎碎念
=====================================================================


代码风格
--------------------------------------
不一致的开发风格会给协作开发带来困难，同时也妨碍代码阅读，读代码的时间是多于写代码的，所以有必要统一编码规范。推荐使用pep8或者其子集作为代码规范，使用vim插件python-mode开启pep8和pylint对代码就行检测。如果使用其他编辑器或者IDE工具最好也使用相关插件使代码符合规范。工程上的代码应该尽可能保持清晰易懂，推荐看看requests等优秀的开源库学习下。强烈建议新手看看以下参考写出格式规范的代码，强烈建议打开pep8和pylint，pylint可以帮助你干掉很多低级错误。建议使用py的公司都指定好自己的代码规范并且严格遵守，同时做好code review，防止造成以后的维护噩梦。

* `《PEP8.org》 <http://pep8.org/>`_
* `《PEP 8 -- Style Guide for Python Code》 <https://www.python.org/dev/peps/pep-0008/>`_
* `《Google开源项目风格指南-Python风格指南》 <http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/>`_ google风格的docstring比较赞
* `《API_coding_style》 <http://deeplearning.net/software/pylearn/v2_planning/API_coding_style.html>`_
* `《code-example》 <https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html>`_
* `《编写优雅代码》 <http://www.kancloud.cn/kancloud/sina-boot-camp/64003>`_  新浪微博的培训课程，可以学习一下
* `《烂代码的那些事》 <http://blog.2baxb.me/archives/1343>`_  Axb的自我修养，大神的文章
* `《三种docstring示例》 <http://bwanamarko.alwaysdata.net/napoleon/format_exception.html>`_


一个简洁的代码规范：

- 格式请遵守pep8,务必开启编辑器的pylint和pep8检测。vim请试试python-mode插件。
- 模块、类和函数请使用docstring格式注释，除显而易见的代码，每个函数应该简洁地说明函数作用，函数参数说明和类型，返回值和类型。对于复杂的传入参数和返回值最好把示例附上。如有引用，可以把jira，github，stackoverflow，需求文档地址附上。 良好的文档和注释很考验人的判断（何时注释）和表达能力（注释什么）。
- 动态语言的变量命名尽量可以从名称就知道其类型，比如url_list, info_dict_list，降低阅读和理解的难度。(我的感觉就是动态语言易编写，写不好后期更难维护)
- 风格上衡量不了请参考知名开源项目的做法。以可读性和维护性作为标准。

* `《Python 工匠：善用变量来改善代码质量》 <http://www.zlovezl.cn/articles/python-using-variables-well/>`_ 动态语言命名尽量可以表达出类型，否则不好维护

编程范式
--------------------------------------
Python支持多重编程范式，过程式(Procedural)，面向对象(OOP)，简单函数式(Functional)编程。不同人，不同语言转过来的人，Python老鸟和菜鸟等写出来的代码风格迥异。笔者之前的同事有对OOP挖掘较深的，一般习惯写OOP风格的，但现在的项目却很少用类，之前的代码都是用一个个函数来实现各种功能。对个人风格喜好不予评判，但是个人感觉还是需要深挖一些Python的特性，虽然Python容易入门，但是有些语言特性还是需要一段时间才能了解深入的。使用各种风格的时候要酌情判断，比如一个过程需要维护大量的中间状态时，单纯的使用函数会写得很冗长，这时候可以用类和子函数的形式简化它。当你无法判断哪种方式比较好的时候，请在解释器里边 `import this` 看看。当可以实现一样的功能时，往往简单易懂的方式就是最好的。一些参考:

* `《requests》 <https://github.com/kennethreitz/requests>`_ requests库是接口设计的典范，可以参考参考。
* `《Python3 面向对象编程》 <https://book.douban.com/subject/26468916/>`_ 关于Python面向对象和一些设计模式。
* `《OOP vs Functional Programming vs Procedural》 <http://stackoverflow.com/questions/552336/oop-vs-functional-programming-vs-procedural>`_


何谓Pythonic?
--------------------------------------
Python的世界里你会听到这个词"Pythonic"，大概就是指代码符合Python的惯用法，使用的都是Python的语法糖。比如从其他语言转到Python
的写出来的代码很可能受到以前思维方式的影响，写出来的代码不够Pythonic:
比如:


.. code-block:: python

    # 不够Pythonic
    if a < b and a > c:
        pass

    # python里却可以这么写
    if c < a < b:
        pass

    # bad
    i = 0
    while i < mylist_length:
        do_something(mylist[i])
        i += 1

    # good
    for element in mylist:
       do_something(element)

    # bad, 不要使用默认可变对象作为默认参数
    def f(a, b=[])
        pass

    # good
    def f(a, b=None):
        if b is None:
            b = []



Python有一些语法上的坑，比如默认参数只计算一次，不要使用可变类型作为默认参数等，看多了写多了就知道了。尤其是可变类型作为函数参数传入后被改变的情况（函数尽量不要有副作用），尤其要注意。
一些参考帮助写出Pythonic的代码:


* `《Pythonic到底是什么玩意儿？》 <http://blog.csdn.net/gzlaiyonghao/article/details/2762251>`_ 赖勇浩的博客
* `《python-guide Code Style》 <http://docs.python-guide.org/en/latest/writing/style/>`_ python-guide关于代码风格的介绍
* `《Learning the Pythonic Way》 <https://www.cs.cmu.edu/~srini/15-441/F11/lectures/r04-python.pdf>`_ 一个cmu的课件
* `《Writing Idiomatic Python3》 <http://share.sm3.su/writing_idiomatic_python_3.pdf>`_ 一本免费小书
* `《编写高质量代码：改善Python程序的91个建议》 <https://book.douban.com/subject/25910544/>`_ 给国人的书捧捧场^_^
* `《好好写代码》 <好好写代码>`_ 豆瓣工程师董伟明的文章


敏捷与TDD
----------------------------
笔者非计算机科班出身，对于软件工程的东西也不是很懂，最近扫了一本《敏捷软件开发-原则、模式与实践》，感觉有些东西还是挺有启发的。在这里稍微提一下敏捷中的TDD(Test-driven development)吧。因为Python是动态类型语言，不像静态语言可以编译期检查，很多问题运行时暴露出来，而且动态语言语法灵活也容易刨坑。用TDD是可以提升代码质量的，虽然有时候完全用TDD可能有些死板，但是TDD的一些思想还是很值得借鉴：

* 测试最重要的是对架构和设计的影响，不是为了测试而测试。一般难以测试的代码往往是设计不好，耦合严重的代码。没有测试的代码同时也给重构带来压力和隐患。

编码的时候想着如何测试它，甚至都可以改善设计。对于动态语言，一直有『动态语言一时爽，代码重构火葬场』这种说法，说明动态语言如果没有良好的设计和测试，以后是会埋下不少隐患的。
当你发现debug的时间甚至比写代码长很多的时候，当你发现总是返工对代码修修补补的时候，或者可尝试下TDD。
你可以学习使用下python的unittest或者pytest等进行单元测试，以保证代码质量。个人工作经验也表明，难以测试的代码往往是设计不太好的代码。
update: 经验表明，TDD未必是必要的，但是单元测试是很必要的。如果是新项目建议为所有的复杂函数写单元测试，为项目质量保证。
下边是一些参考书籍:


* `《Tips for agile developers》 <http://web2.0coder.com/archives/92>`_
* `《pytest: helps you write better programs》 <http://pytest.org/latest/>`_
* `《代码整洁之道》 <https://book.douban.com/subject/5442024/>`_
* `《编写可读代码的艺术》 <https://book.douban.com/subject/10797189/>`_
* `《重构-改善既有代码设计》 <https://book.douban.com/subject/4262627/>`_
* `《软件调试修炼之道》 <https://book.douban.com/subject/6398127/>`_
  了解下调试和跟踪技术。


一些常见原则
----------------------------
对于什么是好代码，什么是坏代码我现在还没有太多经验，但是最近工作接手别人的代码感觉困难重重，还是too naive啊。每个人实力不同，风格不同，一起协作的时候确实会遇到很多问题和分歧。感觉code review啥的还是很有必要的，可以让菜鸟学习下老鸟的经验，也可以让老鸟指导下菜鸟的失误，同时避免过于个人化的糟糕风格（比如让人想立马离职的高达成百上千行的复杂函数，比如上来一堆不知道干啥的幻数，比如上来就 `form shit import *` 导致俺的编辑工具找不到定义，比如整个项目没有一行测试代码，比如不知道用logger，全用print+眼珠子瞅，一个bug找半天，比如没有pep8检测导致你的环境打开别人的代码彪了一堆警告......)。说好的规范呢，说好的设计模式呢，说好的高内聚低耦合呢？说好的KISS原则呢？说好的DYR原则呢？其实俺只是想多活几年，至少不要到三十岁头发掉光。啥设计模式的可以不用，能干活的代码就行，牢记几个原则，没事的时候对复杂的东西重构下，代码不能自解释的搞搞文档，不被队友坑同时不坑队友，俺就心满意足了。最后还是列举一下常用原则、思想和注意事项吧(最好import this看看python之禅，很多思想是通用的):

* KISS原则，Keep It Simple, Stupid。能简单的绝对不要复杂，不要炫耀代码技巧，简单可读最重要，后人会感谢你的。
* DRY原则。就算咱不懂设计模式，只要代码复杂重复了就及时抽取出来，至少不会碰到大问题。
* YAGNI(You Aren't Gonna Need It)，不要猜测性编码。
* 快速失败，灵活使用断言。契约式编程(先验条件和后置条件)
* 及时清理技术债务，防止『破窗』。
* 一次只做一件事。尽量避免复杂度过高的逻辑，尽量做到代码简单，意图明确。
* 高内聚，低耦合。意义相近的东西应该放到同一个地方。写代码的时候想着怎么测试它就能避免过度复杂，耦合严重的代码。
* 代码应当易于理解。 《代码大全》、《编写可读代码的艺术》、《代码整洁之道》啥的都是告诉你代码最好自解释，好理解。记住代码首先是给人看的，其次才是让机器执行的，不要过度设计。
* 不要过早优化，最小可用原则。先测量，后优化。根据二八定律，大部分性能瓶颈只在20%的部分，这些才是真正需要优化的地方。
* 不要炫技，可读性最重要。合适的地方使用合适的技巧，不要过度炫耀语法糖导致维护和理解困难。
* Think about future, design with flexibility, but only implement for production. 尽量设计良好，避免繁杂和冗余。好的架构和设计都是不断演进的。
* 文档化。哪些东西该文档化，哪些该注释需要做好，以便新手可以尽快上手。尽量做到代码即文档，tornado的文档和代码就是典范。
* 不要直接吞掉任何错误和异常，一定要做好记录。血泪教训，使用Sentry或其他工具记录好异常发生的信息，为定位bug提供便利，web端的bug一般不好复现。
* ......还有的大家可以自己补充


还有OOP那一套:

* 开闭原则(Open-Closed Principle)
* 依赖倒置原则(Dependence Inversion Principle)
* 接口隔离原则(Interface Segregation Principle)
* 里氏代换原则(Liskov Substitution Principle)
* 迪米特原则(Law of Demeter)
* 合成复用原则(Composite/Aggregate Reuse Principle)
* 单一职责原则(Single-Responsibility Principle)


python代码坏味道(新手经常犯的错误)
--------------------------------------

- 不pythonic，写得很业余，真就信了半天学会python
- 上来就整一个不知道啥意思的magic number，大学老师没教你不要滥用幻数？
- 上来就from shit import *
- 复杂函数没有docstring，传入了一个嵌套字典都不注释，娘来
- 变量名乱起，看不出类型，加重理解负担。我在想是不是动态语言用匈牙利命名法要好一些
- 不遵守pep8，没有pylint检测，打开代码一堆语法警告，老子的编辑器满眼都是warnning，编辑器用不好就老老实实用pycharm，用编辑器就老老实实装好语法检测和pylint检测插件，没有插件请考虑换一个editor
- 没有单元测试，不知道怎么写测试（print大法好？）
- 超长函数，没有复用和拆分，我智商低，不能理解好几屏都翻不完的，见谅。这么长居然还tm能工作，牛逼
- 到处print，debug的时候加上，上线再删除（累不累亲？），logging模块很受冷落
- 上来就try/except了，把异常都捕获了，吞掉异常导致排错困难
- 没注意可变类型和非可变类型，传入可变类型并在函数里修改了参数，坑。。。
- 没有逻辑分块，没有美感（这个就算了），就算不限制一行超过80列，也不能写一行写几百列吧，左右转头脑瓜子疼

嗯，一开始就开启pep8和pylint检测能显著提升代码质量（各种错误警告逼着你写出高智力代码）。咱写不了诗一样的代码，也不能写shǐ 一样的代码。
可能很多东西对老鸟来说都是显而易见的，不过菜鸟和高级菜鸟们还是需要多多练习积累经验。慢慢摸索吧骚年。。。。。。


小白的踩坑记录
=====================================================================

文档化
--------------------------------------
很多程序员是懒得写文档的，仿佛牛逼的程序员不需要写。但是看人家真正牛逼的开源项目比如flask和tornado等，无论是代码还是文档都做得相当棒。对于一些项目，有些东西如部署步骤；常用命令等还是可以记录下来的，可以使用wiki或者readthedoc，gitbooks等文档工具记录一下，方便新人上手。如果不知道记录啥，就把你发现不止一次会用到的东西文档化。个人认为需求文档也应该有历史记录，方便接手的人可以快速了解业务和需求变更。数据库字段的含义也应该及时记录和更新。


注释
--------------------------------------
有经验的人都知道看别人的代码是一件很痛苦的事情，尤其是没有任何注释的代码。代码除了完成需求外，最重要的就是维护和协作，除非你觉得你做的项目活不过仨月(或你自己玩玩的项目随便你怎么艹)，否则就一定要重视代码质量，防止代码腐化(破窗)以至难以协作和维护。有时候比写注释更难的是知道何时写，写什么注释？python里有规范的docstring用来给类和函数进行注释，除了说明功能外，关于github,stackoverflow链接、复杂的传入传出参数（比如嵌套字典作为参数这种你都不注释就很不合适了)，类型说明、需求文档和bug的jira地址等都可以注释。凡是你回头看代码一眼看不出来干啥的，都应该有适当的注释，方便自己也方便别人。当然，最重要的是代码清晰易读，好的命名和编写风格的代码往往是自解释的，看代码大致就可以看出功能。建议就是给所有的模块、类和函数都加上注释，除非一眼能看出来这个东西干啥，否则都应该简洁注释下，让别人不用一行行看你的代码就大概知道你这个东西是干啥的。最后注意的就是一旦函数更改及时更新注释。qiniu的sdk写得就不错，可以去github看看。总之，"Explicit is better than implicit.", 代码里不要有隐晦的东西，一时偷懒将来可能会付出几倍的维护代价，请对将来的自己和他人负责。

* `《python docstring》 <http://bwanamarko.alwaysdata.net/napoleon/format_exception.html>`_

Code Review
--------------------------------------
笔者认为code review是一件非常重要的事情，可以有效防止代码腐化，同时方便同事了解业务。可以在公司搭建Phabricator（facebook在用）类似工具进行代码review。


日志与异常记录
--------------------------------------
一定要有良好的日志记录习惯。良好的日志对于记录问题至关重要。python有方便的日志模块帮助我们记录，日志输出的代价是比较小的，python的日志模块尽量做到对函数功能没有性能影响，可以在线上和开发环境设置不同的log等级，方便开发调试。注意别再日志语句里引入了bug或异常。
对于异常，一定『不要吞掉任何异常』，常有新手上来就try/except，也不区分非退出异常，也没有日志记录(坑啊......)。请先阅读python文档的异常机制，可以使用Sentry等工具记录异常。同时发生异常时候的时间，调用点，栈调用信息，locals()变量等要注意记录，给排查错误带来便利。有些错误的复现是比较困难的，这时候日志和异常的作用就凸显出来了。

* `《每个 Python 程序员都要知道的日志实践》 <http://mp.weixin.qq.com/s?__biz=MzA4MjEyNTA5Mw==&mid=2652564362&idx=1&sn=f33910af004f276bbef7ae52e0757bcb&chksm=8464c3c0b3134ad617bcffd865894344367fdd2995a0d5ff9c4da30e0c158b3d02b3d616f615&mpshare=1&scene=23&srcid=1124K7Ht1FP2A1Fnvi3HTBE5#rd>`_

调试
--------------------------------------
调试也是个很重要的问题，不可能保证代码没bug，要命的是有时候写代码完成功能的时间还没调试的时间多。注意复现是排错的第一步，之后通过各种方式确定原因（访问日志、邮件报的异常记录）等，通过走查代码、断点调试（二分法等）确定错误位置，确定好错误原因了就好改了。修复后最好反思下问题的原因、类型等，哪些地方可以改进，争取下次不犯一样的错。

* `《调试九法》 <http://www.wklken.me/posts/2015/11/29/debugging-9-rules.html>`_

尽量写出对自己也对其他人负责的代码，上边费了牛劲都是在阐述这个显而易见但是没多少人严格遵守的东西。用动态语言写大型项目维护起来要稍麻烦，
很多新手写代码不注重可维护性，甚至自己写的代码回头自己看都一脸懵逼，问了一句这代码TM是干啥的？
一开始的负责会为以后协作和维护带来极大便利（当然你想干两天就走让其他人擦屁股就当我没说）。
最后，很多东西我也在摸索，上面的玩意你就当小白的踩坑记录，随着理解和经验的加深我会不定期更新本篇内容。
