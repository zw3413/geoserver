.. _source:

源码
===========

GeoServer的源码位于https://github.com/geoserver/geoserver。

Clone源码git仓库::

  % git clone git://github.com/geoserver/geoserver.git geoserver

查看源码git仓库中的可用分支::

  % git branch
     2.1.x
     2.2.x
   * master

切换到稳定分支::

  % git checkout 2.2.x

Git
---

如果之前使用Subversion或者CSV版本管理工具，可能会觉得Git的使用并不太容易。
幸运的是关于Git的优秀文档非常的多。在开始开发前，应该先学习Git的使用。如下是一些关于Git使用的参考资料:

* `The Git Book <http://git-scm.com/book/>`_
* `A nice introduction <http://www.sbf5.com/~cduan/technical/git/>`_

Committing
----------

参照如下步骤来提交代码:

#. 为跨平台项目配置Git客户端。参考下面的 :ref:`notes <gitconfig>`。
#. 注册提交代码的权限。参考 :ref:`here <comitting>`。
#. Fork GeoServer的Git仓库到你自己的github账户。
#. Clone上一步Fork到的Git仓库到本地。
#. 为Clone到本地的Git仓库添加非只读的远程仓库URL (``git@github.com:geoserver/geoserver.git``)

.. note::

  下面会介绍项目的Git仓库的分布，和如何管理本地仓库的远程参考。


Repository distribution
-----------------------

Git是一个分布式的版本管理系统，它由一系列仓库构成，而没有中心仓库。GeoServer的仓库分布情况如下:

* 位于GitHub的 **canonical** 仓库作为官方权威的项目源码
* 位于GitHub的开发者 **fork** 到的代码仓库，包含了官方仓库的所有内容，包括所有的feature和开发者的开发分支
* 位于开发者自己电脑的 **本地** 代码仓库，用于开发者修改和添加代码

虽然Git是一个分布式的系统，各个代码仓库共享一个history，它们之间依然可以互相操作。这就是Git的神奇之处。
为了和GitHub上面的其他代码仓库互相操作，本地的代码仓库必须设置连接到它们的 *remote references* 。
典型的本地代码仓库会包含由如下的 remote references:
* 一个名字为 **origin** 的远程代码库,指向开发者 fork 到的github代码仓库。
* 一个名字为 **upstream** 的远程代码库，指向官方代码库。
* （可选）一些指向其他开发者 fork的gitbub代码库。

可以按照以下方式创建一个本地代码库:

#. Clone 你fork到的github自己账户的代码库(其中的bob替换为你的github账户名) ::

     % git clone git@github.com:bob/geoserver.git geoserver
     % cd geoserver

#. 创建 ``upstream``远程代码库链接，指向官方的代码库 ::

     % git remote add upstream git@github.com:geoserver/geoserver.git

  如果你的github账户没有往官方代码库push代码的权限的话，可以使用只读的url::

     % git remote add upstream git://github.com/geoserver/geoserver.git

#. 可选的，创建远程连接指向其他开发者fork的github代码库。这些远程连接一般都是只读的::

      % git remote add aaime git://github.com/aaime/geoserver.git
      % git remote add jdeolive git://github.com/jdeolive/geoserver.git


代码库结构
--------------------

一个git代码库会包含若干的分支。这些分支大概分为三种类型:

#. **Primary** 分支对应于软件的大版本
#. **Release** 分支用来管理primiary分支的发布
#. **Feature** 分支是开发分支

Primary 类型分支
^^^^^^^^^^^^^^^^

所有的代码库中都会有Primary类型的分支，其对应于项目的各个发布版本。Primary类型分支包含以下分支:

* **mater**分支是项目当前不稳定的开发版本
* **stable** 分支是项目当前稳定的开发版本
* 还有其他的之前的稳定版本分支

例如，现在GeoServer项目的Primary分支是:

* **master** - 2.3.x 发布流，包含了一些主要的新feature的不稳定分支
* **2.2.x** - 2.2.x 发布流，是一个主要修改bug和稳定feature的稳定分支
* **2.1.x** - 2.1.x 发布流，是一个即将结束开发的分支

Release 类型分支
^^^^^^^^^^^^^^^^

Release 类型分支用来管理稳定分支的发布。每一个稳定的primary分支都有一个相应的release分支。目前GeoServer项目的release类型分支有:

* **rel_2.2.x** - 稳定版本的发布分支
* **rel_2.1.x** - 前一个稳定版本的发布分支

Release类型分支只用于软件的版本化发布。任意指定时间的release分支都和最近一次发布时分支的状态完全一致。在发布过程中，这些分支会被标记(tagged).

所有的代码仓库中都有Release 类型分支。

Feature 类型分支
^^^^^^^^^^^^^^^^

Feature类型分支是开发者每天修改的分支。小到修复bug，大到添加新功能。Feature类型分支用作开发者工作的区域，在这些分支可以自由的提交代码而不影响primary类型分支。因此，feature类型分支一般只存在于开发者自己的本地代码仓库，也有可能存在于开发者fork到的github代码库。Feature类型分支永远都不会被推送到官方代码库。

当开发者认为一个功能已经开发完毕，那么这个feature分支会被合并到一个primary分支中，通常是  ``master`` 分支。如果在feature分支完成的工作，适用于stable分支，那么修改内容也可以合并到stable分支。 :ref:`source_workflow` 部分对此进行了详细介绍。


代码结构
------------------

每个分支都有如下的文件结构::

     build/
     doc/
     src/
     data/


* ``build`` - 发布 和 持续集成脚本
* ``doc`` - 用户和开发者指导手册的源码
* ``src`` - GeoServer的java源代码
* ``data`` - 多种GeoServer数据或者配置文件夹

.. _gitconfig:

Git客户端的配置
------------------------

如果一个代码库需要在不同平台上面工作，那么对于文件行结尾的处理就成为了一个问题。Git是一个比较好的工具在不需要显式配置的情况下可以很好的处理这个问题。安全起见，开发者可以将 ``core.autocrlf`` 设置为 "input"::

    % git config --global core.autocrlf input

"input"告诉git要识别和接受代码库中任意类型的行结尾。

.. note::

   对于windows用户，可以将 ``core.safecrlf`` 设置为"true"::

      % git config --global core.safecrlf true

   如此设置可以阻止对于文件行结尾的修改。

其他相关资料:

* http://www.kernel.org/pub/software/scm/git/docs/git-config.html
* https://help.github.com/articles/dealing-with-line-endings
* http://stackoverflow.com/questions/170961/whats-the-best-crlf-handling-strategy-with-git

.. _source_workflow:

开发工作流程
--------------------

本节描述了一个日常开发的典型流程示例。
首先需要理解git工作流中对于代码修改的处理方式。一个修改的生命周期如下:

#. 开发者在本地代码库中执行了一项代码修改。
#. 修改内容被 **staged**，用于commit。
#. 提交已经被stage的修改内容。
#. 提交的修改内容被**push**到一个远程代码库

这个基本的流程中，也有着许多不同的情况。
例如，经常会多次提交后，再一下push到远程代码库。
另外，可以将多个内容较少的提交 **squash** 到一个 commit中进行提交。

从官方代码库中更新内容
^^^^^^^^^^^^^^^^^^^^^^^

一般情况下，开发人员总是在最新版本的官方源码上面工作。如下的示例演示了怎么将官方代码库的最新修改更新到自己的代码库中::

  % git checkout master
  % git pull upstream master

更新稳定分支的方法类似::

  % git checkout 2.2.x
  % git pull upstream 2.2.x

在本地修改代码
^^^^^^^^^^^^^^^^^^^^

如上所述，git的在本地修改代码分为两个阶段，第一是stage，第二是commit。例如，要修改、stage、commit一个文件::

  % git checkout master
  # do some work on file x
  % git add x
  % git commit -m "commit message" x

同样的，本地修改代码也有多种不同的情况。通常情况下，通过``git add``来stage修改或者新增的文件，通过``git rm``来stage被删除的文件。通过``git mv``用来移动文件并stage此修改。

任何时候都可以运行 ``git status`` 来检查工作区中的哪些文件被修改，哪些被stage，哪些被commit了。它同时也显示当前的分支，如果频繁切换分支的话这个非常有用。

将本地修改push到官方库
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

当一个开发者在本地代码库修改了内容，并且希望将修改内容push到远程代码库。对于primary分支的修改都应该push到官方代码库。如果因为某些原因不能直接push到官方库，就不能在primary分支上面修改，而是应该在一个feature分支上开发。

例如，要往官方版本库的 ``master`` 分支推送一个本地修改bug的commit::

  % git checkout master
  # make a change
  % git add/rm/mv ...
  % git commit -m "making change x"
  % git pull upstream master
  % git push upstream master

本示例演示了在push一个commit到远程代码库之前，应该先执行以下pull。开发者应该总是如此执行。实际上，如果远程官方代码库中有新的commit未被pull到本地时，默认情况下git是不允许你push任何修改的，你必须将远程代码库中新的commit（别人push的）先pull到本地，才可以继续执行push操作。

.. note::

   在一个分支和另外一个分支合并，并且不是"fase-forward"合并时，会产生**merge commit**。当本地commit新的修改内容，但是目标分支已经被改动时，就会出现这种非"fast-forward"的合并。Fast-forward具体参阅 `reading about <http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging>`_ .

   一种简单的避免合并不同commit的方法是在pull的时候，执行一个“rebase”操作::

     % git pull --rebase upstream master

   rebase使本地的修改在pull之后显示在git history中。这样就能使下面的commit合并变为fast-forward合并。但是这并不是必须的操作，因为执行非fast-forward的commit合并并不会有任何的损害，但是应该尽量的减少非fast-forward的commit合并，因为它会使commit history和git log变得难以阅读。

在feature类型分支上面开发
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

像之前所述，相较于直接在primary类型分支上面工作，在一个feature分支上面进行代码开发和修改时更好的方式。开发人员使用版本管理系统的一直以来的一个痛点是，当在一个本地开发某个功能并进行了大量修改时，突然需要切换到另外一个场景进行一个更加紧急的bug修改工作。开发人员必须在进行一半的代码中去修改另外一个地方的代码，这是传统版本管理系统难以解决的一个场景。在git中使用feature类型分支就可以很好的解决这个问题。

基于master分支创建一个新的分支::

  % git checkout -b my_feature master
  % # make some changes
  % git add/rm, etc...
  % git commit -m "first part of my_feature"

冲、洗，不断重复。使用feature分支的好处是可以在不同的上下文环境中很简单的切换，来进行不同的工作。只需要 ``git checkout``一个你需要的分支就可以在其上进行开发，结束后再返回前一个feature分支。


.. note::

   When a branch is checked out, all the files in the working area are modified to reflect
   the current state of the branch.  When using development tools which cache the state of the
   project (such as Eclipse) it may be necessary to refresh their state to match the file system.
   If the branch is very different it may even be necessary to perform a rebuild so that
   build artifacts match the modified source code.


Merging feature branches
^^^^^^^^^^^^^^^^^^^^^^^^

Once a developer is done with a feature branch it must be merged into one of the primary branches and pushed up
to the canonical repository. The way to do this is with the ``git merge`` command::

  % git checkout master
  % git merge my_feature

It's as easy as that. After the feature branch has been merged into the primary branch push it up as described before::

  % git pull --rebase upstream master
  % git push upstream master


Porting changes between primary branches
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Often a single change (such as a bug fix) has to be committed to multiple branches. Unfortunately primary
branches **cannot** be merged with the ``git merge`` command. Instead we use ``git cherry-pick``.

As an example consider making a change to master::

  % git checkout master
  % # make the change
  % git add/rm/etc...
  % git commit -m "fixing bug GEOS-XYZ"
  % git pull --rebase upstream master
  % git push upstream master

We want to backport the bug fix to the stable branch as well. To do so we have to note the commit
id of the change we just made on master. The ``git log`` command will provide this. Let's assume the commit
id is "123". Backporting to the stable branch then becomes::

  % git checkout 2.2.x
  % git cherry-pick 123
  % git pull --rebase upstream 2.2.x
  % git push upstream 2.2.x

Cleaning up feature branches
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Consider the following situation. A developer has been working on a feature branch and has gone back
and forth to and from it making commits here and there. The result is that the feature branch has accumulated
a number of commits on it. But all the commits are related, and what we want is really just one commit.

This is easy with git and you have two options:

#. Do an **interactive rebase** on the feature branch
#. Do a **merge with squash**

Interactive rebase
~~~~~~~~~~~~~~~~~~

Rebasing allows us to rewrite the commits on a branch, deleting commits we don't want, or merging commits that should
really be done. You can read more about interactive rebasing `here <http://git-scm.com/book/en/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages>`_.

.. warning::

   Much care should be taken with rebasing. You should **never** rebase commits that are public (that is, commits that have
   been copied outside your local repository). Rebasing public commits changes branch history and results in the inability to merge
   with other repositories.


The following example shows an interactive rebase on a feature branch::

  % git checkout my_feature
  % git log

The git log shows the current commit on the branch is commit "123".
We make some changes and commit the result::

  % git commit "fixing bug x" # results in commit 456

We realize we forgot to stage a change before committing, so we add the file and commit::

  % git commit -m "oops, forgot to commit that file" # results in commit 678

Then we notice a small mistake, so we fix and commit again::

  % git commit -m "darn, made a typo" # results in commit #910

At this point we have three commits when what we really want is one. So we rebase,
specifying the revision immediately prior to the first commit::

  % git rebase -i 123

This invokes an editor that allows indicating which commits should be combined.
Git then *squashes* the commits into an equivalent single commit.
After this we can merge the cleaned-up feature branch into master as usual::

  % git checkout master
  % git merge my_feature

Again, be sure to read up on this feature before attempting to use it. And again, **never rebase a public commit**.

Merge with squash
~~~~~~~~~~~~~~~~~

The ``git merge`` command takes an option ``--squash`` that performs the merge
against the working area but does not commit the result to the target branch.
This squashes all the commits from the feature branch into a single changeset that
is staged and ready to be committed::

  % git checkout master
  % git merge --squash my_feature
  % git commit -m "implemented feature x"


More useful reading
-------------------

The content in this section is not intended to be a comprehensive introduction to git. There are many things not covered
that are invaluable to day-to-day work with git. Some more useful info:

* `10 useful git commands <http://webdeveloperplus.com/general/10-useful-advanced-git-commands/>`_
* `Git stashing <http://git-scm.com/book/en/Git-Tools-Stashing>`_
* `GeoTools git primer <http://docs.geotools.org/latest/developer/procedures/git.html>`_
