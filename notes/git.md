#### 撤销add的文件
*  git rm --cached [filename] // 不删除物理文件，仅将该文件从缓存中删除
*  git rm --f [filename] // 不仅将该文件从缓存中删除，还会将物理文件删除
*  git reset HEAD [filename]  //撤销文件，就是回到add步骤前(保留修改)

#### 撤销commit
* git reset --hard [commit] //回滚到某个commit，什么都不保留
* git reset --soft [commit] //将撤销放在缓存区，就是回到add步骤后
* git reset --mixed [commit] //撤销全部，就是回到add步骤前(保留修改)

#### 删除分支
1. git push origin :[branch] //先删除远程分支
2. git branch -d [branch] //再删除本地分支

#### 移动commit(master的commit移动到simsir)
1. git checkout simsir //先切换到simsir
2. git cherry-pick [commit] //[commit]是要移动的commit的哈希值，当执行完 cherry-pick 以后，将会生成一个新的提交；这个新的提交标识名一样，但哈希值和原来的不同(新的哈希值下面会用到)
3. // 如果顺利，就会正常提交到simsir分支，如果出现了冲突，
4. git add <冲突文件> // 解决冲突后add到缓存区
5. git commit -c [新的commit] // 新的commit指2生成的新的哈希值

### 某个分支回滚远程仓库某个版本
1. git reset --hard [commit] //本地先回滚到某个版本
2. git push origin [branch] -f //强制推送，覆盖掉远程仓库分支

### 拉取远程某个分支到本地
* git checkout -b 本地分支名 origin/远程分支名

### 拉取远程所有分支到本地
* git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done

### 查看两个分支的区别
* git diff [branch] [branch] --stat       //显示出所有有差异的文件列表
* git diff [branch] [branch] 文件名(带路径)   //显示指定文件的详细差异
* git diff [branch] [branch]                   //显示出所有有差异的文件的详细差异

### 查看某段代码是谁写的
* git blame <file-name>

### 修改远程仓库的url
* git remote set-url origin <URL>

### 打标签
* git tag 1.0.0    // 默认tag是打在最近的一次commit上
* git tag -a 1.0.0 -m "v1.0。0 发布描述" [commit]    // 指定commit打tag
* git push origin 1.0.0    // 推送标签到远程仓库

### 查看忽略的文件
* git ls-files --others -i --exclude-standard


> [commit] -- commit标识<br>
[branch] -- 分支名称
