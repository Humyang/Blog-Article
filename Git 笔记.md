将已忽略的文件重新添加到监听中。

`git add -f [filepath]`

分支来回切换

`git checkout -`

## 合并指定分支

`git cherry-pick [commit]`

想充分享受这个命令带来的好处的话，就不要再用 `git add .` 一股脑的把所有文件变更放在一个 commit 里面了。

例如用 git 作为博客系统，不同分支分别代表草稿箱，校验箱，已发布，通过这个命令可以充分隔离不同的分支。
