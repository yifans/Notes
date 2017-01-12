# Git教程
学习[廖雪峰Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137586810169600f39e17409a4358b1ac0d3621356287000)，记录笔记。
## Git简介
## 安装Git
- Linux 使用包管理器安装
- Mac OS X 安装XCode
- Windows 上安装msysgit

安装好之后，进行设置

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 创建版本库
- 初始化一个Git仓库，使用`git init`命令。
- 添加文件到Git仓库，分两步：
	- 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
	- 第二步，使用命令`git commit`，完成。

## 时光机穿梭
- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

### 版本回退
- `HEAD`指向的版本就是当前版本
- 因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

### 工作区和暂存区
- 暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。
- `工作区（Working Directory）`: 就是你在电脑里能看到的目录.
- `版本库（Repository）`: 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
- 其中最重要的就是称为`stage（或者叫index）的暂存区`，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。
- 我们把文件往Git版本库里添加的时候，是分两步执行的：
	- 第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
	- 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

### 管理修改
- 每次修改，如果不add到暂存区，那就不会加入到commit中。

### 撤销修改
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`
	- `git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令.
- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。
- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
- 总结：退回也是要分两步，一个是从master退回到stage，然后再从stage退回到工作目录。
	- 对于还没有提交到stage的，可以从stage用checkout命令退回，这一步会取stage中的文件状态，覆盖掉工作目录中文件的状态，跟master完全没关系。
	- 对于已经到达stage的，想把state中的文件状态用master中的覆盖掉，就用reset命令，这样就把stage中修改用master的状态覆盖掉了，完全跟工作目录没关系

### 删除文件
- 命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
- 使用`rm`删除文件后，有两个选择
	- 一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`
	- 二是删错了，所以可以很轻松地把误删的文件恢复到最新版本：`git checkout -- test.txt`

## 远程仓库
- 设置SSH Key
	- 创建SSH Key：`ssh-keygen -t rsa -C "youremail@example.com"`
	- 如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。
	- 将`id_rsa.pub`加在GitHub设置中

### 添加远程库
- 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`
- 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

### 从远程库克隆
- 要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
- Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

## 分支管理
### 创建与合并分支
Git鼓励大量使用分支：
- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`
- 创建+切换分支：`git checkout -b <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

### 解决冲突
- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
- 用`git log --graph`命令可以看到分支合并图。

### 分支管理策略
- Git分支十分强大，在团队开发中应该充分应用。
- 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
- 在实际开发中，我们应该按照几个基本原则进行分支管理：
	- 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	- 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	- 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

### Bug分支
- 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
- 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

### Feature分支
- 开发一个新feature，最好新建一个分支；
- 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

### 多人协作
- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。
- 因此，多人协作的工作模式通常是这样：
	- 首先，可以试图用`git push origin branch-name`推送自己的修改；
	- 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
	- 如果合并有冲突，则解决冲突，并在本地提交；
	- 没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
	- 如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。

## 标签管理
tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起
### 创建标签
- 命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；
- `git show <tagname>`查看标签信息
- `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- `git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；
- 命令`git tag`可以查看所有标签。

### 操作标签
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

## 使用GitHub
- 在GitHub上，可以任意Fork开源仓库；
- 自己拥有Fork后的仓库的读写权限；
- 可以推送pull request给官方仓库来贡献代码。

## 自定义Git
### 忽略特殊文件
- 忽略某些文件时，需要编写`.gitignore`；
- `.gitignore`文件本身要放到版本库里，并且可以对`.gitignore`做版本管理！
- 不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore
- 需要找出来到底哪个规则写错了，可以用`git check-ignore`命令检查：`$ git check-ignore -v App.class`

### 配置别名
- ` git config --global alias.st status`
- 配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
- 每个仓库的Git配置文件都放在`.git/config`文件中：

### 搭建Git服务器



