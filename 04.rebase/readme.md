## Rebase

多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后 push 的童鞋不得不先 pull，在本地合并，然后才能 push 成功。每次合并再 push 后, 总之看上去很乱 !

- #### 为什么 Git 的提交历史不能是一条干净的直线？
      	- 当然可以! Git 有一种 rebase 的操作，有人将其称为 "变基"
      	- git rebase
      	- 原理:
      	- Git 将我们本地的提交 "挪动" 了位置,整个放在远程(origin/master)之后了
      				- 最终结果就是 commit 提交线就是一条直线了

场景:

1. 假设现在有两个分支 master and dev, 他们当前都指向最新的 commit (取名为: common ancestor)
2. 现在在 master 分支上修改 readme.md 文件内容, 然后 commit
3. checkout 到 dev 分支上修改 readme.md 文件内容,然后 commit
4. 回到 master 分支上: `git merge --no-ff -m "..." dev`
5. 手动解决 conflicts, 然后 commit
6. 查看日志: `git log --graph --pretty=oneline --abbrev-commit`
7. 你会发现,log 中的记录分叉了,而且有好多的 commit message, 非常乱 !
8. 它长这样:

```
*   9e8d57f (HEAD -> master) Merge conflicts
|\
| * e87da4f (dev) Changed content on Dev branch
* | 243317b Changed file on Master branch
|/
* 45932f3 common ancestor
    ...
    (更老的commit)
```

使用 git rebase:

1. 现在我们的 git log 看起来非常的不舒服.
2. 使用 git rebase
3. 此时 HEAD 回到 common ancestor 分支上, 然后将 dev 上的 commit 接在其后
4. 最后手动解决 conflicts, 然后提交, 将这次 commit 接在 dev 的 commit 后
5. 最后 git log 看起来就是这样的:

```
* ca97cfe (HEAD) Merge dev branch
* 031d2bd Changed file on dev branch.
* 35ae0e9 common ancestor
    ...
    (更老的commit)

```
