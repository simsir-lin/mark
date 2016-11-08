#### 撤销commit
* git reset --hard <commit> //回滚到某个commit，什么都不保留
* git reset --soft <commit> //将撤销放在缓存区，就是回到add步骤后
* git reset --mixed <commit> //撤销全部，就是回到add步骤前(保留修改)

#### 删除分支
1. git push origin :分支名称 //先删除远程分支
2. git branch -d 分支名称 //再删除本地分支

#### 移动commit(master的commit移动到simsir)
1. git checkout simsir //先切换到simsir
2. git cherry-pick <commit> //<commit>是要移动的commit的哈希值，当执行完 cherry-pick 以后，将会生成一个新的提交；这个新的提交标识名一样，但哈希值和原来的不同(新的哈希值下面会用到)
3. // 如果顺利，就会正常提交到simsir分支，如果出现了冲突，
4. git add <冲突文件> // 解决冲突后add到缓存区
5. git commit -c <新的commit> // 新的commit指2生成的新的哈希值