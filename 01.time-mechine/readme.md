## Description

- Git is a distributed(分布式的) version control system.

- Git is a free software distributed under the GPL.

## git log

> "git log --pretty=oneline"

You can use command "git log" to look the history you had commit.

## Verson Fallback

> git reset --hard HEAD^

"HEAD^" 表示上一个版本，上上个版本就是 "HEAD^^"，同时我们可以使用 "HEAD~2" 代表上上个版本 .

通过 `git reset` 命令，其实就是移动版本库(.git)中的分支上的`HEAD`指针

> git reflog

`git reflog`用来记录你的每一次命令，在这里你可以看到 commit_id, 还有你提交的 message.

## 工作区

`工作区`就是我们编写代码的地方

## 版本库

`.git`就是 Git 的版本库，里面存了很多东西，最重要的就是`stage (index)`叫做暂存区，还有 Git 为我们自动创建的第一个分支 master, 以及指向 master 的一个指针`HEAD`.

## 管理修改

> 注意：只有在还没有使用 git add 的时候，修改了文件，才能使用 git diff 查看区别 (diff ---> difference)

1. 修改文件
2. git add <file>
3. 修改文件 again.
4. git commit -m "..."

很抱歉，你第二次修改的文件内容，不会被提交到版本库中！原因就在于，git commit 只会提交暂存区(stage)中的内容，也就是你使用 `git add <file>`命令

## 撤销修改

> git checkout -- <file>

将 `file` 文件在工作区中的修改全部撤销，这里有两种情况:

1. <file> 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
2. <file> 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次 git commit 或 git add 时的状态。

> git reset HEAD <file>

当你使用 `git add <file>` 将修改的文件添加到了 stage 中(还没有 commit), 就可以使用 git reset HEAD <file> 将暂存区中的文件撤销至工作区中(状态将改为：unstage)

## 删除文件

git rm <file>

如果你删错了怎么办? 可以使用 `git checkout -- <file>`
