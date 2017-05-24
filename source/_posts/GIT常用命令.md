---
title: GIT常用命令
date: 2017-05-23 16:20:30
tag: GIT
category: 工具
---

# 安装
## 从源代码安装
Git 的工作需要调用 curl，zlib，openssl，expat，libiconv 等库的代码，所以需要先安装这些依赖工具。在有 yum 的系统上（比如 Fedora）或者有 apt-get 的系统上（比如 Debian 体系），可以用下面的命令安装：
```
$ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
```
之后，从下面的 Git 官方站点下载最新版本源代码：
```
http://git-scm.com/download
```
然后编译并安装：
```
$ tar -zxf git-1.7.2.2.tar.gz
$ cd git-1.7.2.2
$ make prefix=/usr/local all
$ sudo make prefix=/usr/local install
```
## 在 Linux 上安装
如果要在 Linux 上安装预编译好的 Git 二进制安装包，可以直接用系统提供的包管理工具。在 Fedora 上用 yum 安装：
```
$ yum install git-core
```
在 Ubuntu 这类 Debian 体系的系统上，可以用 apt-get 安装：
```
$ apt-get install git
```
## 在 Mac 上安装
在 Mac 上安装 Git 有两种方式。最容易的当属使用图形化的 Git 安装工具,下载地址在：
[http://sourceforge.net/projects/git-osx-installer/](http://sourceforge.net/projects/git-osx-installer/)
另一种是通过 MacPorts (http://www.macports.org) 安装。如果已经装好了 MacPorts，用下面的命令安装 Git：
```
$ sudo port install git-core +svn +doc +bash_completion +gitweb
```
## 在 Windows 上安装
在 Windows 上安装 Git 同样轻松，有个叫做 msysGit 的项目提供了安装包，可以到 GitHub 的页面上下载 exe 安装文件并运行：
[http://msysgit.github.com/](http://msysgit.github.com/
完成安装之后，就可以使用命令行的 git 工具（已经自带了 ssh 客户端）了，另外还有一个图形界面的 Git 项目管理工具。)
## 初次运行 Git 前的配置
## 用户信息
第一个要配置的是你个人的用户名称和电子邮件地址。这两条配置很重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录：
```
$ git config --global user.name "Steven Wang"
$ git config --global user.email stevenjxw@gmail.com
```
## 文本编辑器
接下来要设置的是默认使用的文本编辑器。Git 需要你输入一些额外消息的时候，会自动调用一个外部文本编辑器给你用。默认会使用操作系统指定的默认编辑器，一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Emacs 的话，可以重新设置：
```
$ git config --global core.editor emacs
```
## 差异分析工具
还有一个比较常用的是，在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话：
```
$ git config --global merge.tool vimdiff
```
## 查看配置信息
要检查已有的配置信息，可以使用 git config --list 命令：
```
$ git config --list
```
## 获取帮助
想了解 Git 的各式工具该怎么用，可以阅读它们的使用帮助，方法有三：
```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```
比如，要学习 config 命令可以怎么用，运行：
```
$ git help config
```
# 常用命令
## 在工作目录中初始化新仓库
要对现有的某个项目开始用 Git 管理，只需到此项目所在的目录，执行：
```
$ git init
```
初始化后，在当前目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。
如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：
```
$ git add *.c
$ git add README
$ git commit -m 'initial project version'
```
## 从现有仓库克隆
克隆仓库的命令格式为 git clone [url]。比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：
```
$ git clone git://github.com/schacon/grit.git
```
如果希望在克隆的时候，自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：
```
$ git clone git://github.com/schacon/grit.git mygrit
```
## 检查当前文件状态
要确定哪些文件当前处于什么状态，可以用 git status 命令。如果在克隆仓库之后立即执行此命令，会看到类似这样的输出：
```
$ git status
On branch master
nothing to commit, working directory clean
```
## 跟踪新文件
使用命令 git add 开始跟踪一个新文件。所以，要跟踪 README 文件，运行：

```
$ git add README
```
## 忽略某些文件
```
$ cat .gitignore
*.[oa]
*~
```
文件 .gitignore 的格式规范如下：
>所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
>可以使用标准的 glob 模式匹配。
>匹配模式最后跟反斜杠（/）说明要忽略的是目录。
>要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
## 查看已暂存和未暂存的更新
实际上 git status 的显示比较简单，仅仅是列出了修改过的文件，如果要查看具体修改了什么地方，可以用 git diff 命令。
```
$ git status
$ git diff
```
若要看已经暂存起来的文件和上次提交时的快照之间的差异，可以用 git diff --cached 命令。
```
$ git diff --cached
```
## 提交更新
现在的暂存区域已经准备妥当可以提交了。在此之前，请一定要确认还有什么修改过的或新建的文件还没有 git add 过，否则提交的时候不会记录这些还没暂存起来的变化。所以，每次准备提交前，先用 git status 看下，是不是都已暂存起来了，然后再运行提交命令 git commit：
```
$ git commit
```
编辑器会显示类似下面的文本信息（本例选用 Vim 的屏显方式展示）：
```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#       new file:   README
#       modified:   benchmarks.rb
#
~
~
~
".git/COMMIT_EDITMSG" 10L, 283C
```
另外也可以用 -m 参数后跟提交说明的方式，在一行命令中提交更新：
```
$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed
 2 files changed, 3 insertions(+)
 create mode 100644 README
```
## 跳过使用暂存区域
尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。Git 提供了一个跳过使用暂存区域的方式，只要在提交的时候，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：
## 移除文件
要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。可以用 git rm 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。
```
$ git rm readme.txt
```
另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。换句话说，仅是从跟踪清单中删除。比如一些大型日志文件或者一堆 .a 编译文件，不小心纳入仓库后，要移除跟踪但不删除文件，以便稍后在 .gitignore 文件中补上，用 --cached 选项即可：
```
$ git rm --cached readme.txt
```
后面可以列出文件或者目录的名字，也可以使用 glob 模式。比方说：
```
$ git rm log/\*.log
```
## 移动文件
不像其他的 VCS 系统，Git 并不跟踪文件移动操作。如果在 Git 中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。不过 Git 非常聪明，它会推断出究竟发生了什么，至于具体是如何做到的，我们稍后再谈。
```
$ git mv file_from file_to
```
其实，运行 git mv 就相当于运行了下面三条命令：
```
$ mv README.txt README
$ git rm README.txt
$ git add README
```
## 查看提交历史
在提交了若干更新之后，又或者克隆了某个项目，想回顾下提交历史，可以使用 git log 命令查看。
```
$ git log
```
我们常用 -p 选项展开显示每次提交的内容差异，用 -2 则仅显示最近的两次更新：
```
$ git log -p -2
```
某些时候，单词层面的对比，比行层面的对比，更加容易观察。Git 提供了 --word-diff 选项。我们可以将其添加到 git log -p 命令的后面，从而获取单词层面上的对比。
```
$ git log -U1 --word-diff
```
另外, git log 还提供了许多摘要选项可以用，比如 --stat，仅显示简要的增改行数统计：
```
$ git log --stat
```
## 修改最后一次提交
```
$ git commit --amend
```
## 取消已经暂存的文件
可以使用 git reset HEAD <file>... 的方式取消暂存。
```
$ git reset HEAD benchmarks.rb
```
## 取消对文件的修改
```
$ git checkout -- benchmarks.rb
```
## 查看当前的远程库
要查看当前配置有哪些远程仓库，可以用 git remote 命令，它会列出每个远程库的简短名字。
```
$ git remote
origin
```
也可以加上 -v 选项（译注：此为 --verbose 的简写，取首字母），显示对应的克隆地址：
```
$ git remote -v
```
## 添加远程仓库
要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用，运行 git remote add [shortname] [url]：
```
$ git remote
origin
$ git remote add pb git://github.com/paulboone/ticgit.git
$ git remote -v
origin  git://github.com/schacon/ticgit.git
pb  git://github.com/paulboone/ticgit.git
```
现在可以用字符串 pb 指代对应的仓库地址了。比如说，要抓取所有 Paul 有的，但本地仓库没有的信息，可以运行 git fetch pb：
```
$ git fetch pb
```
## 从远程仓库抓取数据
```
$ git fetch [remote-name]
```
## 推送数据到远程仓库
项目进行到一个阶段，要同别人分享目前的成果，可以将本地仓库中的数据推送到远程仓库。实现这个任务的命令很简单： git push [remote-name] [branch-name]。如果要把本地的 master 分支推送到 origin 服务器上（再次说明下，克隆操作会自动使用默认的 master 和 origin 名字），可以运行下面的命令：
```
$ git push origin master
```
## 查看远程仓库信息
我们可以通过命令 git remote show [remote-name] 查看某个远程仓库的详细信息，比如要看所克隆的 origin 仓库，可以运行：
```
$ git remote show origin
```
## 远程仓库的删除和重命名
在新版 Git 中可以用 git remote rename 命令修改某个远程仓库在本地的简称，比如想把 pb 改成 paul，可以这么运行：
```
$ git remote rename pb paul
$ git remote
origin
paul
```
碰到远端仓库服务器迁移，或者原来的克隆镜像不再使用，又或者某个参与者不再贡献代码，那么需要移除对应的远端仓库，可以运行 git remote rm 命令：
```
$ git remote rm paul
$ git remote
origin
```
## 列显已有的标签
列出现有标签的命令非常简单，直接运行 git tag 即可：
```
$ git tag
v0.1
v1.3
```
我们可以用特定的搜索模式列出符合条件的标签。在 Git 自身项目仓库中，有着超过 240 个标签，如果你只对 1.4.2 系列的版本感兴趣，可以运行下面的命令：
```
$ git tag -l 'v1.4.2.*'
v1.4.2.1
v1.4.2.2
v1.4.2.3
v1.4.2.4
```
## 新建含附注的标签
创建一个含附注类型的标签非常简单，用 -a （译注：取 annotated 的首字母）指定标签名字即可：
```
$ git tag -a v1.4 -m 'my version 1.4'
$ git tag
v0.1
v1.3
v1.4
```
## 新建签署标签
如果你有自己的私钥，还可以用 GPG 来签署标签，只需要把之前的 -a 改为 -s （译注： 取 signed 的首字母）即可：
```
$ git tag -s v1.5 -m 'my signed 1.5 tag'
```
现在再运行 git show 会看到对应的 GPG 签名也附在其内：
```
$ git show v1.5
```
## 新建轻量级标签
轻量级标签实际上就是一个保存着对应提交对象的校验和信息的文件。要创建这样的标签，一个 -a，-s 或 -m 选项都不用，直接给出标签名字即可
```
$ git tag v1.4-lw
$ git tag
v0.1
v1.3
v1.4
v1.4-lw
v1.5
```
## 验证标签
可以使用 git tag -v [tag-name] （译注：取 verify 的首字母）的方式验证已经签署的标签。此命令会调用 GPG 来验证签名，所以你需要有签署者的公钥，存放在 keyring 中，才能验证：
```
$ git tag -v v1.4.2.1
```
## 后期加注标签
```
$ git log --pretty=oneline
```
我们忘了在提交 “updated rakefile” 后为此项目打上版本号 v1.2，没关系，现在也能做。只要在打标签的时候跟上对应提交对象的校验和（或前几位字符）即可：
```
$ git tag -a v1.2 9fceb02
```
## 分享标签
默认情况下，git push 并不会把标签传送到远端服务器上，只有通过显式命令才能分享标签到远端仓库。其命令格式如同推送分支，运行 git push origin [tagname] 即可：
```
$ git push origin v1.5
```
如果要一次推送所有本地新增的标签上去，可以使用 --tags 选项：
```
$ git push origin --tags
```
## Git 命令别名
Git 并不会推断你输入的几个字符将会是哪条命令，不过如果想偷懒，少敲几个命令的字符，可以用 git config 为命令设置别名。来看看下面的例子：
```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```
# Git 分支
## 分支的新建与切换
要新建并切换到该分支，运行 git checkout 并加上 -b 参数：
```
$ git checkout -b iss53
```
这相当于执行下面这两条命令：
```
$ git branch iss53
$ git checkout iss53
```
用 git merge 命令来进行合并：
```
$ git checkout master
$ git merge hotfix
```
由于当前 hotfix 分支和 master 都指向相同的提交对象，所以 hotfix 已经完成了历史使命，可以删掉了。使用 git branch 的 -d 选项执行删除操作：
```
$ git branch -d hotfix
```
## 分支的合并
在问题相关的工作完成之后，可以合并回 master 分支。实际操作同前面合并 hotfix 分支差不多，只需回到 master 分支，运行 git merge 命令指定要合并进来的分支：
```
$ git checkout master
$ git merge iss53
```
之前的工作成果已经合并到 master 了，那么 iss53 也就没用了。你可以就此删除它，并在问题追踪系统里关闭该问题。
```
$ git branch -d iss53
```
## 遇到冲突时的分支合并
Git 作了合并，但没有提交，它会停下来等你解决冲突。要看看哪些文件在合并时发生冲突，可以用 git status 查阅
任何包含未解决冲突的文件都会以未合并（unmerged）的状态列出。Git 会在有冲突的文件里加入标准的冲突解决标记，可以通过它们来手工定位并解决这些冲突。可以看到此文件包含类似下面这样的部分：
```
<<<<<<< HEAD
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
  please contact us at support@github.com
</div>
>>>>>>> iss53
```
运行 git mergetool，它会调用一个可视化的合并工具并引导你解决所有冲突：
```
$ git mergetool
```
## 分支的管理
git branch 命令不仅仅能创建和删除分支，如果不加任何参数，它会给出当前所有分支的清单：
```
$ git branch
  iss53
* master
  testing
```
要从该清单中筛选出你已经（或尚未）与当前分支合并的分支，可以用 --merged 和 --no-merged 选项（Git 1.5.6 以上版本）。比如用 git branch --merged 查看哪些分支已被并入当前分支（译注：也就是说哪些分支是当前分支的直接上游。）：
```
$ git branch -v
```
另外可以用 git branch --no-merged 查看尚未合并的工作：
```
$ git branch --no-merged
```
## 推送本地分支
如果你有个叫 serverfix 的分支需要和他人一起开发，可以运行 git push (远程仓库名) (分支名)：
```
$ git push origin serverfix
```
当你的协作者再次从服务器上获取数据时，他们将得到一个新的远程分支 origin/serverfix，并指向服务器上 serverfix 所指向的版本：
```
$ git fetch origin
```
如果要把该远程分支的内容合并到当前分支，可以运行 git merge origin/serverfix。如果想要一份自己的 serverfix 来开发，可以在远程分支的基础上分化出一个新的分支来：
```
$ git checkout -b serverfix origin/serverfix
```
## 跟踪远程分支
从远程分支 checkout 出来的本地分支，称为 跟踪分支 (tracking branch)。跟踪分支是一种和某个远程分支有直接联系的本地分支。在跟踪分支里输入 git push，Git 会自行推断应该向哪个服务器的哪个分支推送数据。同样，在这些分支里运行 git pull 会获取所有远程索引，并把它们的数据都合并到本地分支中来。
```
$ git checkout --track origin/serverfix
```
要为本地分支设定不同于远程分支的名字，只需在第一个版本的命令里换个名字：
```
$ git checkout -b sf origin/serverfix
```
## 删除远程分支
如果不再需要某个远程分支了，比如搞定了某个特性并把它合并进了远程的 master 分支（或任何其他存放稳定代码的分支），可以用这个非常无厘头的语法来删除它：git push [远程名] :[分支名]。如果想在服务器上删除 serverfix 分支，运行下面的命令：
```
$ git push origin :serverfix
```



























