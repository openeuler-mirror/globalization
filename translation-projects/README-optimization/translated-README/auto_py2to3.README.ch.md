==========

auto_py2to3
==========

2020年1月1日，python 2代码库被冻结。从那天起，Python2就再也没有后台端口了，这实际上是让python2和它的运行时环境过时了。

核心开发人员Nick Coghlan在FAQ中解释道，结束了“核心开发团队已经使用Python 2和python3作为参考解释器长达大约13年之久”的历史。

目前，Python2的最终版本正处于测试和候选发布阶段，最终版本Python2.7.18预计将在2020年4月发布。

尽管python社区中的大多数人都赞同python需要彻底的更改，特别是因为急需并且早就应该提供Unicode支持。

但是，很多人都认为Python 2代码很好用，所以他们感到很遗憾。因此，我们必须进行代码迁移。我们的终极目标是，该仓库能自动地、快速地实现代码迁移，并且支持自动化测试。

虽然代码迁移过程中可能会有一些令人不满意的地方，但该库还将继续使用和维护。


特性
------------
* 使用unittest、python setup.py test、pytest来测试程序

* 用Click编写命令行


架构
------------

* 使用官方的2to3作为技术工具来封装可执行文件，供后续使用。

* 提供多种函数参数，通过命令行来处理项目代码。


版本支持
------------
* Python 2.x  to 3.x

* Linux: build/passing
* Windows: build/passing

功能
------------
主要的功能如下：

1. 能否将Python2代码自动转换为Python3
2. 决定是否保留Python2代码的备份
3. 决定是否打开转换代码的文本比较
4. 决定项目所依赖的仓库的版本是否与当前的Python环境相匹配


 用例
------------
.. 镜像:: https://gitee.com/weihaitong/auto_py2to3/raw/master/example/ticketGrabbingExample-commadTest%20processing.png

入门
------------
准备好贡献或者使用了吗？快来了解一下如何安装`auto_py2to3` 进行本地开发吧！

1. 在Gitee上 Fork `auto_py2to3` 存储库。
2. 在本地clone你的仓库: 

    $ git clone https://gitee.com/weihaitong/auto_py2to3.git

3. 这就是你如何使用这个工具:

    $ cd auto_py2to3/
    $ python setup.py install
    $ py2to3 --help

4. 如果你也想为这个项目做贡献，你可以创建一个用于本地开发的分支:

    $ git checkout -b name-of-your-bugfix-or-feature

   现在你可以在本地对代码进行更改了。

5. 提交你的更改，并将你的分支推送到Gitee::

    $ git add .
    $ git commit -m "你对更改的详细描述"
    $ git push origin name-of-your-bugfix-or-feature

6. 在Gitee上提交你的拉取请求（PR）。

 拉取请求指南
-----------------------

在提交拉取请求（PR）前，请检查是否符合以下准则：

1. 你提交的拉取请求应该包含相关的测试。

2. 如果你提交的拉取请求添加了新功能，请更新文档，并将新增的功能放入带有文档字符串的函数中，并将该功能添加到 README.rst 的列表中。
   
3. 你提交的拉取请求应该适用于 Python 3.x，并确保测试通过所有受支持的 Python版本。
   

