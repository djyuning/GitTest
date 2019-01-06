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
$ git push -u origin -d dev

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
```
