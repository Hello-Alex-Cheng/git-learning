## 创建与合并分支

1. git checkout -b <branch-name>
2. add file and append content.
3. git checkout master
4. git merge <branch-name>
5. git branch -d <branch-name>

description:

- git checkout -b 是 git branch 和 git checkout 的缩写
- git merge 是指将指定的分支合并到当前分支

注意: Fast-forward 信息，Git 告诉我们，这次合并是“快进模式”，也就是直接把 master 指向 dev 的当前提交，所以合并速度非常快

## git log --graph

> git log --graph 命令可以看到分支合并图

## 分支策略管理

使用这个命令查看详细的用户操作流程

> git log --graph --pretty=oneline --abbrev-commit

在使用 git merge 时， 使用 --no-ff 参数表示禁用 fast-forward:
`git merge --no-ff -m "merge with no-ff" dev`
