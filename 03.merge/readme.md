## Merge Branch

1. git checkout -b <branch-name> (创建并切换分支)
2. 添加文件修改内容
3. git checkout dev
4. git merge --no-ff <branch-name> (--no-ff: without `fast-forward`)
5. 如果有 conflicts，就必须手动解决
6. 如果不想解决冲突，可以是使用 `git merge --abort` (abort: 中止)
