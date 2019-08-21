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

1. 场景：假设你正在 dev 分支上进行开发，突然来了一个 bug，但是你现在改动了很多内容，你应该如何立即去解决 bug 呢?

答：git 提供了一个 `stash` 的功能，把当前工作内容 " 存储 " 起来，等 bug 修复了再继续回到之前的工作中 .

2. 用法如下

```
	git stash (存储当前工作区的内容)

	git stash list (查看存储的内容)

	git stash pop (弹出存储的内容)

	git stash pop (弹出存储的内容同时删除 stash 中的内容)

	git stash apply (弹出stash 中的内容，但是并不删除 stash 中的内容)

	git stash drop (可以删除 stash 中的内容)

```

3. 假设我们在 master 分支上切出了一个 bug 分支，开发完了才知道，这个 bug 原本是要在 dev 上进行开发的，该怎么办呢 ?

- 假设你已经开发完了，那么就 commit 这个 bug 分支的内容
- 通过 git log 拿到刚刚 commit 的 commit_id
- git checkout dev
- git cherry-pick <commit-id> (此时，刚才开发的 bug 分支的内容就迁移到了 dev 分支上了)
- git branch -d <bug-branch>
- 但是，如果没有合并的 bug 分支，你是无法删除的，必须使用 `-D` 来进行强制删除

如果没有进行合并的分支，你使用 `git branch -d branch-name` 的话，控制台就会提示出如下信息:

```
	error: The branch 'issue-002' is not fully merged.
	If you are sure you want to delete it, run 'git branch -D issue-002'.
```

## 多人协作

1. 首先，可以试图用 git push origin <branch-name>推送自己的修改；

2. 如果推送失败，则因为远程分支比你的本地更新，需要先用 git pull 试图合并；

3. 如果 git pull 提示 no tracking information，则说明本地分支和远程分支的链接关系没有创建，设置 dev 和 origin/dev 的链接, 用命令 git branch --set-upstream-to=origin/<branch-name> <branch-name>

4. 如果合并有冲突，则解决冲突，并在本地提交；

5. 没有冲突或者解决掉冲突后，再用 git push origin <branch-name>推送就能成功！

## Rebase

多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后 push 的童鞋不得不先 pull，在本地合并，然后才能 push 成功。每次合并再 push 后, 总之看上去很乱 !

- #### 为什么 Git 的提交历史不能是一条干净的直线？
      	- 当然可以! Git 有一种 rebase 的操作，有人将其称为 "变基"
      	- git rebase
      	- 原理:
      	- Git 将我们本地的提交 "挪动" 了位置,整个放在远程(origin/master)之后了
      	- 最终结果就是 commit 提交线就是一条直线了
