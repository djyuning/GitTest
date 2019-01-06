# 常用命令操作

> 常用 git 命令汇总

## 基础操作
```bash
# 初始化 git 仓库
# 如果不输入仓库名，则在当前命令执行的目录创建 .git
$ git init
# 如果指定了仓库，则创建指定的目录
$ git init projectName

# 克隆远程仓库到本地
# 远程仓库托管服务商如 github.com、coding.net 等
# 如果不指定项目名称，则使用远程仓库的默认名称
$ git clone https://github.com/djyuning/GitTest.git
# 如果指定了项目名称，则创建指定目录并把远程代码克隆到新建的目录
$ git clone projectName https://github.com/djyuning/GitTest.git

# 拉取远程代码
# git pull 等于 git fetch && git merge
$ git pull

# 添加文件
# . 可以添加所有更改，但可能也是不需要变动的更改
$ git add .
# 可以添加目录下的更改
$ git add ./design

# 提交更改
$ git commit -m "修改了文件，新增了文件"

# 提交所有更改到远程
$ git push -u origin
```

## 分支操作
```bash
# 查看现有分支
$ git branch

# 从当前分支创建新 dev 分支
# 新建的分支为本地分支，如果使用了远程仓库，远程是看不到新建的分支的
$ git branch dev

# 除了上面的直接新建分支，还可以从提交节点等创建分支
# 创建并切换到分支
$ git checkout -b master
# 3b92cd3 是当前分支的某个提交节点
$ git checkout -b 3b92cd3

# 从指定分支创建分支
# 首先切换到指定分支
$ git checkout dev
# 创建新分支
$ git checkout -b djyuning
# 上面就是从 dev 分支创建了一个 djyuning 分支

# 发布本地 dev 分支
# 发布成功后，远程仓库可以看到新发布的分支
# 当前分支做了修改，也可以使用该命令提交更新内容
$ git push origin dev

# 删除本地 dev 分支
# 如果删除的是当前工作分支，执行删除会报错
# 本地删除后，远程的分支仍然存在
$ git branch -d dev

# 删除远程分支
$ git push origin -d dev

# 把 dev 分支的更改合并到 master 分支
# 首先确保 dev 的所有更改已提交
# 切换到 master 分支
$ git checkout master
# 合并代码
$ git merge dev
# 合并后的代码如果存在冲突，需要手动解决冲突
# 查看合并后的内容
$ git log --oneline --graph
# 更新合并到的代码
$ git push -u origin master

# 变基
# 除了使用 merge 合并两个分支，还可以使用 rebase 变基
# 首先，切换到落后的分支
$ git chekout djyuning
# 执行变基命令
$ git rebase master
```

# 标签管理
```bash
# 查看现有标签
$ git tag

# 从当前分支创建标签
$ git tag -a v1.0.2
# 从指定版本号创建 tag
$ git tag -a v1.0.2 54e22ff -m "从指定版本号创建 tag"

# 删除指定标签
$ git tag -d v1.0.2

# 查看创建的版本信息
$ git show 1.0.2

# 推送本地标签到远程仓库
$ git push origin --tags

# 删除标签
# 这只是删除了本地的比钱
$ git tag -d 1.0.3
# 如果希望删除远程标签，可以使用下面的命令
$ git push origin :refs/tags/1.0.3
```

## commit 操作
```bash
# 提交代码
$ git add .
$ git commit -m "提交的描述信息"

# 撤销刚才的提交
$ git reset --hard HEAD~1

# 会退到某次提交
# 显示列出所有的提交记录
$ git log --oneline
# 回到指定的节点
$ git reset --hard 6922ba8

# 重新提交本地代码到远程
$ git push -f
```

## 合并多次 commit

> 为了美化 commit history 不择手段

有时候，本地修改的内容零零散散，为了简化 commit 的描述信息，我们可以合并多个 commit 然后进行提交。
需要注意的是，这里的合并 commit 是指在本地合并 commit，如果是合并到远程，我们可能需要使用其他方法实现。

**需要注意的是， `git rebase` 操作比较危险，如果我们不熟悉其命令参数，最好不要在正式的项目上尝试使用。**

```bash
# 首先列出所有提交记录
$ git log --oneline
# 输出
6922ba8 新增针对 rebase 的强调备注信息
bfd2d26 预添加代码
4081bf6 新增合并多次commit描述
····
# 合并最后的三条提交记录
$ git rebase -i HEAD~3
# 输出
pick 6922ba8	新增针对 rebase 的强调备注信息
pick bfd2d26	预添加代码
pick 4081bf6	新增合并多次commit描述
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
# ·······略

# 为了保留修改，我们需要把后面的合并到前面，按下 i 键，进入变基模式，修改上面的内容，如：
pick 6922ba8	新增针对 rebase 的强调备注信息
s bfd2d26	预添加代码
s 4081bf6	新增合并多次commit描述

# 按下 esc 退出编辑模式，如果有冲突，需要我们解决冲突，无冲突则显示：
# This is a combination of 4 commits.
# The first commit’s message is:
······略
```
