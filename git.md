# Git 学习笔记

[Git-Book](https://git-scm.com/book/en/v2)

## 下载现有仓库

``` shell
git clone https://some/git/repo.git
# OR SSH clone
git clone git@github.com:someone/some_repo.git

git pull  # 更新
```

## 创建新的项目

``` shell
git init
git add .
git commit -m "first commit" # -n 用于不做 pylint/cpplint check 强制提交，在需要合入主分支的提交中不建议

git push --set-upstream https://some/git/repo.git master
# OR
git remote add origin https://some/git/repo.git

git push -u origin master
```

## 添加分支

```shell
git branch -a # 查看分支状态
# git branch xxx # 创建新分支
# git checkout xxx # 切换到新分支
git checkout -b xxx # 直接替代上面两行
git status # 查看本地代码状态
git add file # 提交 file 到缓存，一般使用 . 代表当前目录下所有改动
git commit -m "commit info"
git push origin xxx # 将本地代码提交到 origin 远端的 xxx 分支
```

## 回退版本

```shell
git reset [commit number] # 退回到上一个 commit [或指定 commit]，但保留新修改的代码。默认使用 --mixed 模式，撤销 "git add ." 的操作
git reset --soft # 退回到上一个 commit，保留新修改的代码，不撤销 "git add ."。使用 HEAD^ 来操作本地
git reset --hard # 退回到上一个 commit，不保留新修改的代码
git commit --amend # 修改 commit 信息，使用默认编辑器
```

## 本地 rebase/merge

```shell
git pull # 拉取最新版本
git rebase origin master # origin 是指的远程链接的名称，master 是指需要 rebase 的分支
# 如果有冲突，会在冲突文件里写入 >>>>>>/<<<<<<，需要解决冲突才能完成 rebase/merge
```
