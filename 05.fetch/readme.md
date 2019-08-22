## Fetch

When you `git push`, you synchronize(同步) changes made to the Local Repository into the Remote Repository. To get changes made to the Remote into your Local Repository you use `git fetch`.

- git pull 和 git fetch 的区别

1.  git pull 会更新 remote repository 到本地并自动 merge
2.  git fetch 会更新 remote repository 到本地, 但是不会自动 merge

```
git fetch orgin master //将远程仓库的master分支下载到本地当前branch中

git log -p master  ..origin/master //比较本地的master分支和origin/master分支的差别

git merge origin/master //进行合并
```

![](https://res.cloudinary.com/practicaldev/image/fetch/s--LD07tDxG--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://raw.githubusercontent.com/UnseenWizzard/git_training/master/img/pull.png)

![](https://res.cloudinary.com/practicaldev/image/fetch/s--F6oFwBrc--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://raw.githubusercontent.com/UnseenWizzard/git_training/master/img/fetch.png)
