新拉自己仓库本地分支：
```
git remote -v (查看远端仓库代号)
git fetch o(这是远端仓库的代号)
git checkout -b 本地分支名 远端仓库代号/远端分支
//例子: git checkout -b test o/innerAd
```

进行本地多次commit合并
```
每次操作之后进行 "git add ." "git commit -m 'xxxx'"
在push之前，进行rebase操作
执行步骤：
1. git log （查看本地comit记录）

2. git rebase -i
head~x/commit号(合并之前多少次记录或者合并至某个commit号)；

3. 执行完命令之后会弹出一个窗口，头几行如下：
    pick 3ca6ec3   '注释**********'

    pick 1b40566   '注释*********'

    pick 53f244a   '注释**********'
将pick改为squash或者s，pick为保留这次提交，squash为把本次提交和上一次提交合并（就是删掉这次提交）.

4. 改完保存之后会弹出一个窗，出现修改后的commit名字，可以对这次合并对commit名字进行修改。然后退出。

5. 然后执行"git add .","git rebase --continue",保存操作。

6. 如果想放弃这次压缩的化，可以执行以下命令："git rebase --abort"