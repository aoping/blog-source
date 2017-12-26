---
title: git
date: 2017-12-25 15:35:28
tags:
categories:
---


## git命令

### git push 远程仓库别名 推送分支
推送本地分支到远程仓库，这2个参数缺省分别就是 origin 、 当前分支（一般为master）
```
git push origin master
可以简写成
git push
```

#### options
-u 设置本地分支去跟踪远程对应的分支


### rebase
rebase操作过程是把本地提交一次一个地迁移到更新了的中央仓库master分支之上
```
git pull --rebase
```
如果有冲突，用git status查看，解决冲突后
```
git add <some-file> 
git rebase --continue
```
取消rebase
```
git rebase --abort
```

### git patch
git diff生成patch文件
或者pull request生成的patch文件（在连接上加上.patch即可知道链接）
vscode安装git patch插件可以生成文件





## git流程
