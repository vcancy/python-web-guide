.. _codingstyle:

编码之前碎碎念
=====================================================================


代码风格
--------------------------------------
不一致的开发风格会给协作开发带来困难，同时也妨碍代码阅读，读代码的时间是多于写代码的，所以有必要统一编码规范。推荐使用pep8或者其子集作为代码规范，使用vim插件python-mode开启pep8和pylint对代码静态检测。如果使用其他编辑器或者IDE工具最好也使用相关插件使代码符合规范。工程上的代码应该尽可能保持清晰易懂，推荐看看requests等优秀的开源库学习下。强烈建议新手看看以下参考写出格式规范的代码，强烈建议打开pep8和pylint，pylint可以帮助你干掉很多低级错误。建议使用py的公司都指定好自己的代码规范并且严格遵守，同时做好code review，防止造成以后的维护噩梦。

* `《PEP8.org》 <http://pep8.org/>`_
* `《PEP 8 -- Style Guide for Python Code》 <https://www.python.org/dev/peps/pep-0008/>`_
* `《Google开源项目风格指南-Python风格指南》 <http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/>`_ google风格的docstring比较赞
* `《API_coding_style》 <http://deeplearning.net/software/pylearn/v2_planning/API_coding_style.html>`_
* `《code-example》 <https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html>`_
* `《编写优雅代码》 <http://www.kancloud.cn/kancloud/sina-boot-camp/64003>`_  新浪微博的培训课程，可以学习一下
* `《烂代码的那些事》 <http://blog.2baxb.me/archives/1343>`_  Axb的自我修养，大神的文章
* `《三种docstring示例》 <http://bwanamarko.alwaysdata.net/napoleon/format_exception.html>`_
* `《Simple python style guide》 <http://liyangliang.me/posts/2015/08/simple-python-style-guide/>`_


一个简洁的代码规范：

- 格式请遵守pep8,务必开启编辑器的pylint和pep8检测。vim请试试python-mode插件。
- 模块、类和函数请使用docstring格式注释，除显而易见的代码，每个函数应该简洁地说明函数作用，函数参数说明和类型，返回值和类型。对于复杂的传入参数和返回值最好把示例附上。如有引用，可以把jira，github，stackoverflow，需求文档地址附上。 良好的文档和注释很考验人的判断（何时注释）和表达能力（注释什么）。
- 动态语言的变量命名尽量可以从名称就知道其类型，比如url_list, info_dict_list，降低阅读和理解的难度。(我的感觉就是动态语言易编写，写不好后期更难维护)
- 风格上衡量不了请参考知名开源项目的做法。以可读性和维护性作为标准。(比如知名网站reddit的python代码已经开源了，可以作为参考)
- 阿里最近开源了一个规范《阿里巴巴Java开发手册》，网上可以很容易搜到，写得比较细，建议新手下载来看看，有不少实战干货，很多思想是通用的，其实python的unittest等模块很多都是直接借鉴了java。

* `《Python 工匠：善用变量来改善代码质量》 <http://www.zlovezl.cn/articles/python-using-variables-well/>`_ 动态语言命名尽量可以表达出类型，否则不好维护

编程范式
--------------------------------------
Python支持多重编程范式，过程式(Procedural)，面向对象(OOP)，简单函数式(Functional)编程。不同人，不同语言转过来的人，Python老鸟和菜鸟等写出来的代码风格迥异。笔者之前的同事有对OOP挖掘较深的，一般习惯写OOP风格的，但现在的项目却很少用类，之前的代码都是用一个个函数来实现各种功能。对个人风格喜好不予评判，但是个人感觉还是需要深挖一些Python的特性，虽然Python容易入门，但是有些语言特性还是需要一段时间才能了解深入的。使用各种风格的时候要酌情判断，比如多个过程需要共享中间状态时，单纯的使用函数会写得很冗长，这时候就应当使用类。通常能用函数完成功能的就使用函数。当你无法判断哪种方式比较好的时候，请在解释器里边 `import this` 看看。当可以实现一样的功能时，往往简单易懂的方式就是最好的。一些参考:

* `《requests》 <https://github.com/kennethreitz/requests>`_ requests库是接口设计的典范，可以参考参考。
* `《Python3 面向对象编程》 <https://book.douban.com/subject/26468916/>`_ 关于Python面向对象和一些设计模式。
* `《OOP vs Functional Programming vs Procedural》 <http://stackoverflow.com/questions/552336/oop-vs-functional-programming-vs-procedural>`_


何谓Pythonic?
--------------------------------------
Python的世界里你会听到这个词"Pythonic"，大概就是指代码符合Python的惯用法，使用的都是Python的语法糖(我觉得可以翻译为『地道』)。比如从其他语言转到Python
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
* `《Code Like a Pythonista: Idiomatic Python》 <http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html>`_  我强烈推荐新手看看这个教程


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
* `《软件调试修炼之道》 <https://book.douban.com/subject/6398127/>`_ 了解下调试和跟踪技术。


一些常见原则
----------------------------
对于什么是好代码，什么是坏代码我现在还没有太多经验，但是最近工作接手别人的代码感觉困难重重，还是too naive啊。每个人实力不同，风格不同，一起协作的时候确实会遇到很多问题和分歧。感觉code review啥的还是很有必要的，可以让菜鸟学习下老鸟的经验，也可以让老鸟指导下菜鸟的失误，同时避免过于个人化的糟糕风格（比如让人想立马离职的高达成百上千行的复杂函数，比如上来一堆不知道干啥的幻数，比如上来就 `form shit import *` 导致俺的编辑工具找不到定义，比如整个项目没有一行测试代码，比如不知道用logger，全用print+眼珠子瞅，一个bug找半天，比如没有pep8检测导致你的环境打开别人的代码彪了一堆警告......)。说好的规范呢，说好的设计模式呢，说好的高内聚低耦合呢？说好的KISS原则呢？说好的DYR原则呢？其实俺只是想多活几年，至少不要到三十岁头发掉光。啥设计模式的可以不用，能干活的代码就行，牢记几个原则，没事的时候对复杂的东西重构下，代码不能自解释的搞搞文档，不被队友坑同时不坑队友，俺就心满意足了 ，遇到坑队友就等着加班和折寿吧:(。最后还是列举一下常用原则、思想和注意事项吧(最好import this看看python之禅，很多思想是通用的):

* KISS原则，Keep It Simple, Stupid。能简单的绝对不要复杂，不要炫耀代码技巧，简单可读最重要，后人会感谢你的。
* DRY原则。就算咱不懂设计模式，只要代码复杂重复了就及时抽取出来，至少不会碰到大问题。当然不要矫枉过正，过度追求设计和通用可能导致难以维护和理解。
* YAGNI(You Aren't Gonna Need It)，不要猜测性编码，不用的及时删除，估计以后也不太可能会用到。
* 快速失败，灵活使用断言。契约式编程(先验条件和后置条件)，越早失败，越容易排查错误。
* 及时清理技术债务，防止『破窗』。
* 隐藏复杂性。如果复杂性避免不了，应该尽让内部复杂，接口要保持简单易用，而不要因为业务逻辑复杂就堆砌一堆shit.
* 一次只做一件事。尽量避免复杂度过高的逻辑，尽量做到代码简单，意图明确。
* 高内聚，低耦合。意义相近的东西应该放到同一个地方。写代码的时候想着怎么测试它就能避免过度复杂，耦合严重的代码。
* 代码应当易于理解。 《代码大全》、《编写可读代码的艺术》、《代码整洁之道》啥的都是告诉你代码最好自解释，好理解。记住代码首先是给人看的，其次才是让机器执行的，不要过度设计。
* 不要过早优化，最小可用原则。先测量，后优化。根据二八定律，大部分性能瓶颈只在20%的部分，这些才是真正需要优化的地方。
* 不要炫技，可读性最重要。合适的地方使用合适的技巧，不要过度炫耀语法糖导致维护和理解困难。大部分人不是造轮子的，你用不着太多奇淫技巧。
* 不要重复发明轮子。遇到问题首选稳定可靠的解决方案。比如处理excel报表等直接用pandas提供的函数非常方便，我经常看见还是有人自己写一堆恶心的处理函数而不用pandas。
* 自动化。重复执行的任务应该使之自动化，你用的python是写自动化脚本最合适的语言。
* Think about future, design with flexibility, but only implement for production. 尽量设计良好，避免繁杂和冗余。好的架构和设计都是不断演进的。
* 文档化。哪些东西该文档化，哪些该注释需要做好，以便新手可以尽快上手。尽量做到代码即文档，tornado的文档和代码就是典范。
* 不要直接吞掉任何非预知错误和异常，一定要做好记录。血泪教训，使用Sentry或其他工具记录好异常发生的信息，为定位bug提供便利，web端的bug一般不好复现。
* ......还有的大家可以自己补充。我建议新手可以看看《代码大全》或者《编程匠艺》之中的任何一本，带你快速入门。当然有些东西只是建议，编程中往往没有绝对正确，只有相对更优，No Silver Bullet，大家在实践中摸索吧。


还有OOP那一套，当你设计一个类的时候需要有所注意:

* 单一职责原则(Single-Responsibility Principle)
* 开闭原则(Open-Closed Principle): 对修改关闭，对扩展开放。
* 里氏代换原则(Liskov Substitution Principle): 所有使用基类的地方都可以使用子类替换。
* 接口隔离原则(Interface Segregation Principle): 不要强制客户端使用他们不需要的接口。
* 依赖倒置原则(Dependence Inversion Principle): 高层模块不应该依赖于底层模块，他们都应该依赖于抽象。
* 迪米特原则(Law of Demeter):
* 合成复用原则(Composite/Aggregate Reuse Principle):


python代码坏味道(新手经常犯的错误)
--------------------------------------
下边是笔者学习和维护代码的过程中总结的一些经验和发现的一些问题，可能有些地方会有分歧，仅供参考：

风格相关:

- 不pythonic，写得很业余(随意)，真就信了半天学会python
- 上来就整一个不知道啥意思的magic number，大学老师没教你不要滥用幻数？
- 上来就 `from shit import *,` 为了偷懒有可能会导致同名覆盖问题，还会让开发工具找不到定义，工程上不要这么用。
- 包导入顺序混乱，没有按照pep8要求，实际上rope等工具能自动帮你整理顺序，我现在就是偷懒随意写，直接让rope给我整理
- 变量名乱起，表意不明，推断不出类型，加重理解负担。我在想是不是动态语言用匈牙利命名法要好一些，命名尽量要可以看出类型，比如复数表示容器类型，nums，cnts等后缀表示数值
- 不遵守pep8，没有pylint检测，打开代码一堆语法警告，老子的编辑器满眼都是warnning，编辑器用不好就老老实实用pycharm，用编辑器就老老实实装好语法检测(pep8)和pylint检测插件，没有插件请考虑换一个editor。我个人的感觉就是python代码很容易写得难以维护，请务必加上pylint检测，帮助提高代码质量。
- 没有逻辑分块，一点都不重视排版，没有美感（这个就算了），就算不限制一行超过80列，也不能写一行写几百列吧，左右转头脑瓜子疼(请不要用tab，全用空格)。使用良好的分行，空格使代码更美观，逻辑更清晰。


异常相关：

- 到处print，debug的时候加上，上线再删除（累不累亲？），logging模块很受冷落
- 上来就try/except了，把异常都捕获了，吞掉异常导致排错困难。就在我写这段的时候又因为使用了他人未经测试的代码排错许久，就是因为吞了异常没打出来异常信息。
- 捕获的异常应该尽量类型精确，范围清晰。不要上来就try一整个代码块，可以继承内置异常类定义自己的更为精确的异常类。
- 使用sentry等工具记录异常，有利于排查问题(能保存堆栈和现场信息)。切记不要轻易吞掉非预知异常，一旦出现问题不好排查，笔者之前维护的项目曾踩过坑，后来笔者引入了sentry排查问题方便很多。
- 捕获异常是为了处理它，确定要怎么处理异常，记录待修复？流程控制？交给上一层重新抛出(raise)？预知异常直接pass？
- 了解你所使用的类库函数会抛出哪些异常，需不需要捕获异常？自定义函数抛出的异常最好在docstring里写出来。


函数相关:

- 复杂函数没有docstring，接口易用性极差，传入了一个嵌套字典都不注释，娘来。python没有类型声明真是维护代码的一个大坑。
- 保持函数参数尽量使简单数据类型，你传入dict不写docstring我知道字典有哪些字段？
- 函数要么修改传入的可变参数，要么返回一个值。请不要两者同时做。注意python默认参数只计算一次，如果默认参数不是immutable对象，最好使用None作为占位符。
- 超长函数，没有复用和拆分，抱歉我智商低，不能理解好几屏都翻不完的，见谅。这么长居然还tm能工作，牛逼(我发现越是新手写的代码越难理解,我实习那会总被说代码写得像面条)
- 函数圈复杂度太高，一堆嵌套逻辑判断，导致测试难以覆盖到所有分之，单元测试几乎就没法写，恩，你压根不写单元测试就当我没说。
- 没注意可变类型和非可变类型，传入可变类型并在函数里修改了参数(无意的修改)，坑。。。
- 滥用 `(*args, **kwargs)` 导致函数接口模糊，有类似接口应该明确用docstring写明参数，"Explicity is better than implicity"，不要为了偷懒把代码写得隐晦。
- 返回多个值可以使用namedtuple封装，比用下标更直观

测试相关:

- 没有单元测试，不知道怎么写测试（print大法好？）。没有一点专业精神，或许和python大部分都是自学的业余选手有关，哈哈当然我也是
- 不专业，写了几句代码print下结果就觉得正确了，单元测试呢？docstring呢？代码易用性和可维护性极差，未经测试的代码是不值得信任的。不要太相信自己，人人都会犯错，但不能反复犯一样的错。

日志相关:

- 哪些地方需要打印日志？debug参数？记录用户行为？排查问题？记录哪些信息？
- 注意日志等级，使用debug/info/warnning/error要斟酌好。

ORM相关：

- 优先使用ORM，相比sql语句更加容易维护，同时避免了sql注入。
- 获取对象的时候尽量传入需要的字段(数据表列)，减少数据传输同时还能避免拼对象的时间消耗，python构建对象比较耗时。
- 注意不要在循环里使用查询语句，合并查询语句。比如不要在for循环中使用一个对象的relation查询(懒加载的时候，每次调用都会查询数据库)

嗯，一开始就开启pep8和pylint检测能显著提升代码质量（各种错误警告逼着你写出规范的代码）。咱写不了诗一样的代码，也不能写shǐ 一样的代码，维护一个ugly的代码仓库能有效减少你的寿命。可能很多东西对老鸟来说都是显而易见的，不过菜鸟和高级菜鸟们还是需要多多练习积累经验。慢慢摸索吧骚年。。。。。。如果能主动读一读《代码大全》《编程匠艺》《clean code》之类的书更好(或者flask等优秀的开源项目代码)，别人会更乐意和你一起合作编程，不然你总会心想『天呐，千万别让我改那个家伙的代码，我宁愿离职！！！』

难以维护的Python代码
--------------------------------------

::

	# python
    def isRankingBetter(self, customer,topranking):
        testranking = getRanking(customer)
        return testranking > topranking

    // java
    public boolean isRankingBetter(Customer customer, int topranking) {
        int testranking = getRanking(customer);
        return testranking > topranking;
    }

上面是一段java和python的对比，用来说明为什么python难以维护。java版本一眼就能看出来传入参数的类型和返回值，但是遗憾的是python看不出来，在python中基本只有通过docstring你才能知道传入参数的类型。当项目大了以后，维护一份没有文档和注释的python项目基本就是灾难。笔者曾很喜欢python语言，认为python是“伪代码”语言，但是有了维护python旧代码的经验后，我开始怀疑python是不是适合构建大型项目。当然很多知名应用是python构建的，我觉得老外们软件工程做得还是不错的，把控好代码质量和单元测试（比如Quora创始人曾经解释过他们为什么选择了python）。但是我经历的一些使用python的项目工程方面却比较糟糕，代码维护起来非常吃力，开始让我对python产生严重怀疑。java虽然写起来繁琐，但是不容易出错，动态语言写起来爽，但是维护和重构起来吃力，并且容易出错。我个人感觉就是使用动态语言要严格把控代码质量和文档，用好pylint对代码静态检测，否则项目大了难以维护。

重视细节
--------------------------------------

版式
--------------------------------------

良好的代码排版可以让人理解代码更容易，一点经验:

- 尽量遵守pep8，除了行长度可以适当放宽，比如django使用120列。
- 合理使用换行使代码更易理解，同时更美观
- 合理使用空行对代码块逻辑进行分隔，使层次清晰。
- 不要使用太长的行(别超出120列)，否则分屏查看或合并代码的时候很不方便 ，你得来回移动编辑器指针，对笔者这种喜欢分屏的简直就是灾难。

::

    # 分行之前，我见过最长的得俩屏幕连起来才能看完
    daily_report_data = db.session.query(Data.event_date, func.sum(Data.revenue).label('revenue'), func.sum(Data.payout).label('payout')).filter(Data.tag != Data.TagEnum.arbitrage).filter(Data.event_date < self._next_month_date).filter(Data.event_date >= self._this_month_date).filter(Data.finance_type == Data.TypeEnum.normal).group_by(Data.event_date).all()

    # 分行之后
    daily_report_data = db.session.query(
        Data.event_date,
        func.sum(Data.revenue).label('revenue'),
        func.sum(Data.payout).label('payout')
    ).filter(
        Data.tag != Data.TagEnum.arbitrage
    ).filter(
        Data.event_date < self._next_month_date
    ).filter(
        Data.event_date >= self._this_month_date
    ).filter(
        Data.finance_type == Data.TypeEnum.normal
    ).group_by(
        Data.event_date
    ).all()


你看看大概各需要几秒才能分别理解上边的代码，分行之后能在三秒之内大致理解代码是干啥的，但是太长行你光移动编辑器指针就要花几秒。所以有时候排版还是很重要的，为了快速理解代码你要用上各种手段，尽量让代码更直观。当然有时候你拿不定注意怎么样选择的时候，就以一种最容易理解的方式写，下边是笔者常用的一些分行方式，有利于写出遵守pep8的代码:

::

    from some_module import (
        a_long_variable_name, b_long_variable_name, c_long_variable_name,
        d_long_variable_name
    )

    if a_long_variable_name and b_long_variable_name and c_variable_name \
            and d_variable:
        # 我更倾向于用括号而不是反斜线来分行
        pass


    if (a_long_variable_name and b_long_variable_name
        and c_long_variable_name and d_long_variable_name):

        pass


    a_long_list_comprehension = [person.name
                                 for person in db.session.query(Person.name)]


    a_long_dict_comprehension = {
        person.id: person.name
        for person in db.session.query(Person.name, Person.id)
    }


    employee_id_list = [
        ins.id for ins in Employee.get_role_team_members(
            role_int, team_int, ['id']
        )
    ]


    def long_variable_function_name_and_function_params(a_long_variable_name,
                                                        b_long_variable_name,
                                                        c_long_variable_name,
                                                        d_long_variable_name):
        pass



    def long_variable_function_name_and_function_params(
        a_long_variable_name,
        b_long_variable_name,
        c_long_variable_name,
        d_long_variable_name
    ):
        pass


    return {
        'code': ErrorCode.OPERATOR_FAILED_NEED_TOKEN,
        'msg': ErrorCode.OPERATOR_FAILED_NEED_TOKEN_MSG,
        'data': {}
    }, status_codes.unauthorized


    new_employee = Employee.get_by_id(new_employee_id)
    (
        changed_advertiser_ids,
        changed_account_ids
    ) = assign_employee_advertiser_and_account(employee, new_employee)


    result = a_very_very_very_very_very_very_very_very_long_function_name(
        a_long_variable_name, b_long_variable_name,
        c_long_variable_name, d_long_variable_name
    )


命名
--------------------------------------

首先你要遵守pep8的规定，使用惯用法来命名。或者根据你们公司的python编码规范（如果你们公司有的话）

- joined_lower for functions, methods, attributes
- ALL_CAPS for constants
- StudlyCaps for classes

另外注意动态语言因为没有类型声明，所以在阅读源代码的时候，如果名称起的不好，很难推测出代码中间变量的数据结构，给阅读代码带来障碍。比如一个字典列表，或者嵌套字典等，笔者维护过python代码，深感其中坑太多。我个人的经验就是适度在命名中加入一些类型提示，比如使用nums, cnts等作为后缀很容易知道是数值类型，复数单词或者some_list等很容易知道是序列，some_mapper或者some_dict, some_set等基本从命名就知道什么数据类型了。当然这只是我的经验，有些人会反对这种命名方式，老实说如果代码写得是自解释的，可以不用这么来，但是我个人感觉这种方式虽然冗余，但是确实给我维护和阅读代码带来了便利。python3中加入了type hint特性，所以我觉得类型声明对于维护代码来说还是非常便利的。但是注意，动态语言有鸭子类型的概念，所以有时候名称中的类型提示并不代表就是该类型，很可能造成歧义，这也是很多人反对在python中使用类似匈牙利命名法的原因。老实说我不怎么使用鸭子类型，我感觉鸭子类型是很多错误的来源，如果它真的很有用，python3也不用加上类型注解了，甚至mypy都加上类型检测了（python3中的注解只是为IDE工具提供便利，并没有真正的类型检查）。我觉得对于软件工程重视不够的团队最好不要使用动态语言开发后台。

- 注意词性。比如函数用动词，数据变量使用名词，布尔数据经常使用is等作为前缀。
- 适当使用"匈牙利"命名法。比如一个变量明显是字典或者集合，加上后缀可能会更易理解。（个人经验，有争议，不过我确实感觉这种代码更容易阅读理解）
- 含义精确。不要使用诸如data，info等概念太广泛的词汇给变量命名。

注释与docstring
--------------------------------------

.. code-block:: python

    def function_with_types_in_docstring(param1, param2):
    """Example function with types documented in the docstring.

    `PEP 484`_ type annotations are supported. If attribute, parameter, and
    return types are annotated according to `PEP 484`_, they do not need to be
    included in the docstring:

    Args:
        param1 (int): The first parameter.
        param2 (str): The second parameter.

    Returns:
        bool: The return value. True for success, False otherwise.

    .. _PEP 484:
        https://www.python.org/dev/peps/pep-0484/

    """

这个是google的docstring示例,是我比较推崇的一种格式。还是那个问题，动态语言没有类型声明，所以复杂函数要在docstring里写清楚传入参数和返回值的描述和类型。良好的docstring能让维护代码的人一眼就看明白这个函数是怎么使用的，即使内部很复杂，也尽量保持接口简单，容易使用。经常有人传出个嵌套字典（dict的key是主键，每个key对应的value里还有字典），这种相对复杂的数据结构还不注释，每次看这种函数都要打断点看返回结构。这种就是典型的接口易用性差，只在意实现功能，完全不管别人使用，合作起来比较心累。

- Docstrings = How to use code。代码约定
- Comments = Why & how code works

Docstring应该包括什么?接口易用性

- 意图(目的)。解释为什么需要它？有些对你来说很明显的东西对其他人来说不一定很明显。
- 描述参数，返回值和会抛出的异常。我举个简单的例子， `def f(date): pass` ，仅仅看date这个参数你不知道传入str还是datetime.date，如果传入字符串又有很多格式的字符串，需要哪种格式？所以这个时候一个简单的描述 `date (str): 'YYYY-MM-DD'` 就能让使用函数的人一下子明白了。当然如果有单元测试实际上测试代码也是很好的文档，我们通过单元测试就知道怎么传值。另外使用了 `**kwargs` 如果都不说明就太不厚道了
- 使用注意事项。复杂的使用可以有demo示例说明。
- 需求文档或者github, stackoverflow等链接。比如有个很trick的实现是你查阅 stackoverflow解决的，可以附上地址帮助阅读代码的人找到出处。

注释怎么写?

- 当然，好代码 > 差代码+好注释，自解释的代码最好。
- 适当注释，仔细衡量，不要隐晦也不要多余。
- 及时更新。
- 注释代码中一些tricky的技巧或者特殊的业务逻辑。

很多东西都需要自己斟酌，不要矫枉过正，比如说需要注释你就写一堆没必要的冗余的注释，说遵守pep8尽量不超过80列你连url都要拆成两行，我。。。。。。如果有些规范相冲突，你就以代码的可读性为标准，所有标准都是为了良好的代码设计的。我最怕和随意的程序员一起干活，随意就是写个函数print下就觉得正确了，没有docstring和注释，写的接口让别人难以使用。公司项目毕竟不是自己过家家，我现在就是自己的小项目也会注重规范（自己维护起来也方便，不要相信你的记忆力）。很多用python的小公司就是很不规范，维护起来真心累。也希望所有看到这里的python学习者可以把规范重视起来(很多知名开源项目文档都相当不错)，这也是一个职业程序员应该具备的素养。毕竟大部分人不是造轮子的人，能把业务逻辑实现地简单优雅易维护也是一种能力。


* `《google docstring示例》 <http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html>`_

* `《注重细节:代码排版，命名与注释》 <http://ningning.today/2017/01/22/python/python-coding-details/>`_

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
笔者认为code review是一件非常重要的事情，可以有效防止代码腐化，同时方便同事了解业务。可以在公司搭建Phabricator（facebook在用）类似工具进行代码review。可惜小公司流程不严格，codereview总是坚持不下去，要不就是被同事吐槽总是给他挑刺。实际上如果是新手能够从code review当中快速学到很多东西，比如编程惯用法，摆脱不良编码习惯，不良设计和难以维护的代码等。review的时候对事不对人，代码如果有明显缺陷快速记录个TODO等待review后修正，以一种开放和学习的心态看待review，慢慢整个团队的实力和代码质量就会提高。review就是个互相学习进步的过程，正规的团队都应该严格遵守，而不只是走走流程。

日志与异常记录
--------------------------------------
一定要有良好的日志记录习惯。良好的日志对于记录问题至关重要。python有方便的日志模块帮助我们记录，日志输出的代价是比较小的，python的日志模块尽量做到对函数功能没有性能影响，可以在线上和开发环境设置不同的log等级，方便开发调试。注意别再日志语句里引入了bug或异常。有时候需要判断什么时候需要日志，记录哪些东西方便我们排查问题，分析数据。
对于异常，一定『不要吞掉任何异常』，常有新手上来就try/except，也不区分非退出异常，也没有日志记录(坑啊......)。请先阅读python文档的异常机制，可以使用Sentry等工具记录异常。同时发生异常时候的时间，调用点，栈调用信息，locals()变量等要注意记录，给排查错误带来便利。有些错误的复现是比较困难的，这时候日志和异常的作用就凸显出来了。

* `《每个 Python 程序员都要知道的日志实践》 <http://mp.weixin.qq.com/s?__biz=MzA4MjEyNTA5Mw==&mid=2652564362&idx=1&sn=f33910af004f276bbef7ae52e0757bcb&chksm=8464c3c0b3134ad617bcffd865894344367fdd2995a0d5ff9c4da30e0c158b3d02b3d616f615&mpshare=1&scene=23&srcid=1124K7Ht1FP2A1Fnvi3HTBE5#rd>`_

调试
--------------------------------------
调试也是个很重要的问题，不可能保证代码没bug，要命的是有时候写代码完成功能的时间还没调试的时间多。注意复现是排错的第一步，之后通过各种方式确定原因（访问日志、邮件报的异常记录）等，通过走查代码、断点调试（二分法等）确定错误位置，确定好错误原因了就好改了。修复后最好反思下问题的原因、类型等，哪些地方可以改进，争取下次不犯一样的错，慢慢减少错误才能越来越高效。

* `《调试九法》 <http://www.wklken.me/posts/2015/11/29/debugging-9-rules.html>`_

尽量写出对自己也对其他人负责的代码，上边费了牛劲都是在阐述这个显而易见但是没多少人严格遵守的东西。用动态语言写大型项目维护起来要稍麻烦，
很多新手写代码不注重可维护性，甚至自己写的代码回头自己看都一脸懵逼，问了一句这代码TM是干啥的？
一开始的负责会为以后协作和维护带来极大便利（当然你想干两天就走让其他人擦屁股就当我没说）。
最后，很多东西我也在摸索，上面的玩意你就当小白的踩坑记录，随着理解和经验的加深我会不定期更新本篇内容。另外我发现网上大部分是教程性的东西，对于python相关的工程性的东西很少，我很疑惑难道大部分公司的python项目都写得相当规范？没人吐槽？反正我是踩过坑，希望看到过本章的人能把python代码质量重视起来。


最后来，跟我一起大声朗读《The Zen of Python》

::

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!
