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

1. 通常，合并分支时，如果可能，Git 会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

2. 如果要强制禁用`Fast forward`模式，Git 就会在 merge 时生成一个新的 commit，这样，从分支历史上就可以看出分支信息。

3. 在使用 `git merge` 时， 使用 --no-ff 参数表示禁用 fast-forward:

4. 然后就能看到分支合并的信息了

总结: 合并分支时，加上 --no-ff 参数后就可以使用`普通模式`合并，合并后的历史有分支，能看出来曾经做过合并，而使用`fast-forward`模式合并就看不出来曾经做过合并

`git merge --no-ff -m "merge with no-ff" dev`

## Bug 分支

每个 bug 都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
