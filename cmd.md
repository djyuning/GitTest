# 常用命令操作

> 常用 git 命令汇总

## 分支操作

```bash
# 查看现有分支
$ git branch

# 从当前分支创建新 dev 分支
# 新建的分支为本地分支，如果使用了远程仓库，远程是看不到新建的分支的
$ git branch dev

# 发布本地 dev 分支
# 发布成功后，远程仓库可以看到新发布的分支
$ git push origin dev

# 删除本地 dev 分支
# 如果删除的是当前工作分支，执行删除会报错
# 本地删除后，远程的分支仍然存在
$ git branch -d dev

# 删除远程分支
$ git branch -d origin/dev
```
