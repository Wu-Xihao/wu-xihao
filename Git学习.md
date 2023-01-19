# Git学习

## 常用命令
+ 操作文件与文件夹
  1. <font color=OrangeRed>cd</font> 改变目录，即切换到哪个目录下
  2. <font color=OrangeRed>cd ..</font> 回退到上一个目录，注意cd与..之间有空格
  3. <font color=OrangeRed>pwd</font> 打印工作目录，它会显示当前所在文件的目录路径
  4. <font color=OrangeRed>ls</font> 列出当前目录中所有文件
  5. <font color=OrangeRed>touch</font> 新建一个文件夹
  6. <font color=OrangeRed>rm</font> 删除一个文件
  7. <font color=OrangeRed>mkdir</font> 新建一个目录，即新建一个文件夹
  8. <font color=OrangeRed>rm -r</font> 删除一个文件夹
  9. <font color=OrangeRed>mv</font> 移动文件
  10. <font color=OrangeRed>reset</font> 清屏
+ 新建代码库
  1. <font color=OrangeRed>git init</font> 在当前目录新建一个git代码库
  2. <font color=OrangeRed>git init [文件名]</font> 新建一个目录，将其初始化为git代码库
  3. <font color=OrangeRed>git clone [项目地址]</font> 下载一个项目和它的整个代码历史
+ 配置
  1. <font color=OrangeRed>git config --list</font> 显示当前git配置
  2. <font color=OrangeRed>git config -e [--global]</font> 编辑git配置文件
  3. <font color=OrangeRed>git config [--global] user.name "[用户名]"</font> 设置git用户名
  4. <font color=OrangeRed>git config [--global] user.email "[用户邮箱]"</font> 设置git邮件地址
+ 增加/删除文件
  1. <font color=OrangeRed>git add [文件名1] [文件名2] ...</font> 添加指定文件到暂存区
  2. <font color=OrangeRed>git add [指定目录]</font> 添加指定目录到暂存区，包括子目录
  3. <font color=OrangeRed>git add .</font> 添加当前目录的所有文件到暂存区
  4. <font color=OrangeRed>git add -p</font> 添加每个变化前，都会要求确认，对于一个文件的多处变化，可实现分步提交
  5. <font color=OrangeRed>git rm [文件名1] [文件名2] ...</font> 删除工作区文件，并且将此次删除放入暂存区
  6. <font color=OrangeRed>git rm --cached [文件]</font> 停止追踪指定文件，但该文件会保留在工作区
  7. <font color=OrangeRed>git mv [原文件名] [新文件名]</font> 改文件名，并将这个改名放入暂存区
+ 代码提交
  1. <font color=OrangeRed>git commit -m [message]</font> 提交暂存区到仓库区
  2. <font color=OrangeRed>git commit [file1] [file2] ... -m [message]</font> 提交暂存区的指定文件到仓库区
  3. <font color=OrangeRed>git commit -a</font> 提交工作区自上次commit之后的变化，直接到仓库区
  4. <font color=OrangeRed>git commit -v</font> 提交时显示所有diff信息
  5. <font color=OrangeRed>git commit -am [message]</font> 将add和commit合为一步
  6. <font color=OrangeRed>git commit --amend -m [message]</font> 使用一次新的commit，替代上一次提交,如果代码没有任何新变化，则用来改写上一次commit的提交信息
  7. <font color=OrangeRed>git commit --amend [file1] [file2] ...</font> 重做上一次commit，并包括指定文件的新变化
+ 分支
  1. <font color=OrangeRed>git branch</font> 列出所有本地分支
  2. <font color=OrangeRed>git branch -r</font> 列出所有远程分支
  3. <font color=OrangeRed>git branch -a</font> 列出所有本地分支和远程分支
  4. <font color=OrangeRed>git branch [branch-name]</font> 新建一个分支，但依然停留在当前分支
  5. <font color=OrangeRed>git checkout -b [branch]</font> 新建一个分支，并切换到该分支
  6. <font color=OrangeRed>git branch [branch] [commit]</font> 新建一个分支，指向指定commit
  7. <font color=OrangeRed>git branch --track [branch] [remote-branch]</font> 新建一个分支，与指定的远程分支建立追踪关系
  8. <font color=OrangeRed>git checkout [branch-name]</font> 切换到指定分支，并更新工作区
  9. <font color=OrangeRed>git checkout -</font> 切换到上一个分支
  10.<font color=OrangeRed>git branch --set-upstream [branch] [remote-branch]</font> 建立追踪关系，在现有分支与指定的远程分支之间
  11. <font color=OrangeRed>git merge [branch]</font> 合并指定分支到当前分支
  12. <font color=OrangeRed>git cherry-pick [commit]</font> 选择一个commit，合并进当前分支
  13. <font color=OrangeRed>git branch -d [branch-name]</font> 删除分支
  14. <font color=OrangeRed>git push origin --delete [branch-name]</font> 删除远程分支
  15. <font color=OrangeRed>git branch -dr [remote/branch]</font> 删除远程分支
  16. <font color=OrangeRed>git checkout v2.0</font> 检出版本v2.0
  17. <font color=OrangeRed> checkout -b devel origin/develop</font> 从远程分支develop创建新本地分支devel并检出
  18. <font color=OrangeRed> checkout -- README</font> 检出head版本的README文件（可用于修改错误回退）
+ 标签
  1. <font color=OrangeRed>git tag</font> 列出所有tag
  2. <font color=OrangeRed>git tag [tag]</font> 新建一个tag在当前commit
  3. <font color=OrangeRed>git tag [tag]</font> [commit] 新建一个tag在指定commit
  4. <font color=OrangeRed>git tag -d [tag]</font> 删除本地tag
  5. <font color=OrangeRed>git push origin :refs/tags/[tagName]</font> 删除远程tag
  6. <font color=OrangeRed>git show [tag]</font> 查看tag信息
  7. <font color=OrangeRed>git push [remote] [tag]</font> 提交指定tag
  8. <font color=OrangeRed>git push [remote] --tags</font> 提交所有tag
  9. <font color=OrangeRed>git checkout -b [branch] [tag]</font> 新建一个分支，指向某个tag
+ 查看信息
  1. <font color=OrangeRed>git status</font> 显示有变更的文件
  2. <font color=OrangeRed>git log</font> 显示当前分支的版本历史
  3. <font color=OrangeRed>git log --stat</font> 显示commit历史，以及每次commit发生变更的文件
  4. <font color=OrangeRed>git log -S [keyword]</font> 搜索提交历史，根据关键词
  5. <font color=OrangeRed>git log [tag] HEAD --pretty=format:%s</font> 显示某个commit之后的所有变动，每个commit占据一行
  6. <font color=OrangeRed>git log [tag] HEAD --grep feature</font> 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
  7. <font color=OrangeRed>git log --follow [file]</font> 显示某个文件的版本历史，包括文件改名
  8. <font color=OrangeRed>git whatchanged [file]</font> 显示某个文件的版本历史，包括文件改名
  9. <font color=OrangeRed>git log -p [file]</font> 显示指定文件相关的每一次diff
  10. <font color=OrangeRed>git log -5 --pretty --oneline</font> 显示过去5次提交
  11. <font color=OrangeRed>git shortlog -sn</font> 显示所有提交过的用户，按提交次数排序
  12. <font color=OrangeRed>git blame [file]</font> 显示指定文件是什么人在什么时间修改过
  13. <font color=OrangeRed>git diff</font> 显示暂存区和工作区的差异
  14. <font color=OrangeRed>git diff --cached [file]</font> 显示暂存区和上一个commit的差异
  15. <font color=OrangeRed>git diff HEAD</font> 显示工作区与当前分支最新commit之间的差异
  16. <font color=OrangeRed>git diff [first-branch]...[second-branch]</font> 显示两次提交之间的差异
  17. <font color=OrangeRed>git diff --shortstat "@{0 day ago}"</font> 显示今天你写了多少行代码
  18. <font color=OrangeRed>git show [commit]</font> 显示某次提交的元数据和内容变化
  19. <font color=OrangeRed>git show --name-only [commit]</font> 显示某次提交发生变化的文件
  20. <font color=OrangeRed>git show [commit]:[filename]</font> 显示某次提交时，某个文件的内容
  21. <font color=OrangeRed>git reflog</font> 显示当前分支的最近几次提交
+ 远程同步
  1. <font color=OrangeRed>git fetch [remote]</font> 下载远程仓库的所有变动
  2. <font color=OrangeRed>git remote -v</font> 显示所有远程仓库
  3. <font color=OrangeRed>git remote show [remote]</font> 显示某个远程仓库的信息
  4. <font color=OrangeRed>git remote add [shortname] [url]</font> 增加一个新的远程仓库，并命名
  5. <font color=OrangeRed>git pull [remote] [branch]</font> 取回远程仓库的变化，并与本地分支合并
  6. <font color=OrangeRed>git push [remote] [branch]</font> 上传本地指定分支到远程仓库
  7. <font color=OrangeRed>git push [remote] --force</font> 强行推送当前分支到远程仓库，即使有冲突
  8. <font color=OrangeRed>git push [remote] --all</font> 推送所有分支到远程仓库
+ 撤销
  1. <font color=OrangeRed>git checkout [file]</font> 恢复暂存区的指定文件到工作区
  2. <font color=OrangeRed>git checkout [commit] [file]</font> 恢复某个commit的指定文件到暂存区和工作区
  3. <font color=OrangeRed>git checkout .</font> 恢复暂存区的所有文件到工作区
  4. <font color=OrangeRed>git reset [file]</font> 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
  5. <font color=OrangeRed>git reset --hard</font> 重置暂存区与工作区，与上一次commit保持一致
  6. <font color=OrangeRed>git reset [commit]</font> 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
  7. <font color=OrangeRed>git reset --hard [commit]</font> 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
  8. <font color=OrangeRed>git reset --keep [commit]</font> 重置当前HEAD为指定commit，但保持暂存区和工作区不变
  9. <font color=OrangeRed>git revert [commit]</font> 新建一个commit，用来撤销指定commit，后者的所有变化都将被前者抵消，并且应用到当前分支
  10. <font color=OrangeRed>git stash</font> 暂时将未提交的变化移除，稍后再移入
  11. <font color=OrangeRed>git stash pop</font>
+ 其他
  1. <font color=OrangeRed>git init</font>  初始化本地git仓库（创建新仓库）
  2. <font color=OrangeRed>git config --global user.name "xxx"</font>  配置用户名
  3. <font color=OrangeRed>git config --global user.email "xxx@xxx.com"</font>  配置邮件
  4. <font color=OrangeRed>git config --global color.ui true  git status</font>等命令自动着色
  5. <font color=OrangeRed>git config --global color.status auto</font>
  6. <font color=OrangeRed>git config --global color.diff auto</font>
  7. <font color=OrangeRed>git config --global color.branch auto</font>
  8. <font color=OrangeRed>git config --global color.interactive auto</font>
  9. <font color=OrangeRed>git config --global --unset http.proxy  remove  proxy configuration on git</font>
  10. <font color=OrangeRed>git clone git+ssh://git@192.168.53.168/VT.git</font>  clone远程仓库
  11. <font color=OrangeRed>git status</font>  查看当前版本状态（是否修改）
  12. <font color=OrangeRed>git add xyz</font>  添加xyz文件至index
  13. <font color=OrangeRed>git add .</font>  增加当前子目录下所有更改过的文件至index
  14. <font color=OrangeRed>git commit -m 'xxx'</font>  提交
  15. <font color=OrangeRed>git commit --amend -m 'xxx'</font>  合并上一次提交（用于反复修改）
  16. <font color=OrangeRed>git commit -am 'xxx'</font>  将add和commit合为一步
  17. <font color=OrangeRed>git rm xxx</font>  删除index中的文件
  18. <font color=OrangeRed>git rm -r *</font>  递归删除
  19. <font color=OrangeRed>git log</font>  显示提交日志
  20. <font color=OrangeRed>git log -1</font>  显示1行日志 -n为n行
  21. <font color=OrangeRed>git log -5</font>
  22. <font color=OrangeRed>git log --stat</font>  显示提交日志及相关变动文件
  23. <font color=OrangeRed>git log -p -m</font>
  24. <font color=OrangeRed>git show dfb02e6e4f2f7b573337763e5c0013802e392818</font>  显示某个提交的详细内容
  25. <font color=OrangeRed>git show dfb02</font>  可只用commit id的前几位
  26. <font color=OrangeRed>git show HEAD</font>  显示HEAD提交日志
  27. <font color=OrangeRed>git show HEAD^</font>  显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
  28. <font color=OrangeRed>git tag</font>  显示已存在的tag
  29. <font color=OrangeRed>git tag -a v2.0 -m 'xxx'</font>  增加v2.0的tag
  30. <font color=OrangeRed>git show v2.0</font>  显示v2.0的日志及详细内容
  31. <font color=OrangeRed>git log v2.0</font>  显示v2.0的日志
  32. <font color=OrangeRed>git diff</font>  显示所有未添加至index的变更
  33. <font color=OrangeRed>git diff --cached</font>  显示所有已添加index但还未commit的变更
  34. <font color=OrangeRed>git diff HEAD^</font>  比较与上一个版本的差异
  35. <font color=OrangeRed>git diff HEAD -- ./lib</font>  比较与HEAD版本lib目录的差异
  36. <font color=OrangeRed>git diff origin/master..master</font>  比较远程分支master上有本地分支master上没有的
  37. <font color=OrangeRed>git diff origin/master..master --stat</font>  只显示差异的文件，不显示具体内容
  38. <font color=OrangeRed>git remote add origin git+ssh://git@192.168.53.168/VT.git</font>  增加远程定义（用于push/pull/fetch）
  39. <font color=OrangeRed>git branch</font>  显示本地分支
  40. <font color=OrangeRed>git branch --contains 50089</font>  显示包含提交50089的分支
  41. <font color=OrangeRed>git branch -a</font>  显示所有分支
  42. <font color=OrangeRed>git branch -r</font>  显示所有原创分支
  43. <font color=OrangeRed>git branch --merged</font>  显示所有已合并到当前分支的分支
  44. <font color=OrangeRed>git branch --no-merged</font>  显示所有未合并到当前分支的分支
  45. <font color=OrangeRed>git branch -m master master_copy</font>  本地分支改名
  46. <font color=OrangeRed>git checkout -b master_copy</font>  从当前分支创建新分支master_copy并检出
  47. <font color=OrangeRed>git checkout -b master master_copy</font>  上面的完整版
  48. <font color=OrangeRed>git checkout features/performance</font>  检出已存在的features/performance分支
  49. <font color=OrangeRed>git checkout --track hotfixes/BJVEP933</font>  检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
  50. <font color=OrangeRed>git checkout v2.0</font>  检出版本v2.0
  51. <font color=OrangeRed>git checkout -b devel origin/develop</font>  从远程分支develop创建新本地分支devel并检出
  52. <font color=OrangeRed>git checkout -- README</font>  检出head版本的README文件（可用于修改错误回退）
  53. <font color=OrangeRed>git merge origin/master</font>  合并远程master分支至当前分支
  54. <font color=OrangeRed>git cherry-pick ff44785404a8e</font>  合并提交ff44785404a8e的修改
  55. <font color=OrangeRed>git push origin master</font>  将当前分支push到远程master分支
  56. <font color=OrangeRed>git push origin :hotfixes/BJVEP933</font>  删除远程仓库的hotfixes/BJVEP933分支
  57. <font color=OrangeRed>git push --tags</font>  把所有tag推送到远程仓库
  58. <font color=OrangeRed>git fetch</font>  获取所有远程分支（不更新本地分支，另需merge）
  59. <font color=OrangeRed>git fetch --prune</font>  获取所有原创分支并清除服务器上已删掉的分支
  60. <font color=OrangeRed>git pull origin master</font>  获取远程分支master并merge到当前分支
  61. <font color=OrangeRed>git mv README README2</font>  重命名文件README为README2
  62. <font color=OrangeRed>git reset --hard HEAD</font>  将当前版本重置为HEAD（通常用于merge失败回退）
  63. <font color=OrangeRed>git rebase</font>
  64. <font color=OrangeRed>git branch -d hotfixes/BJVEP933</font>  删除分支hotfixes/BJVEP933（本分支修改已合并到其他分支）
  65. <font color=OrangeRed>git branch -D hotfixes/BJVEP933</font>  强制删除分支hotfixes/BJVEP933
  66. <font color=OrangeRed>git ls-files</font>  列出git index包含的文件
  67. <font color=OrangeRed>git show-branch</font>  图示当前分支历史
  68. <font color=OrangeRed>git show-branch --all</font>  图示所有分支历史
  69. <font color=OrangeRed>git whatchanged</font>  显示提交历史对应的文件修改
  70. <font color=OrangeRed>git revert dfb02e6e4f2f7b573337763e5c0013802e392818</font>  撤销提交dfb02e6e4f2f7b573337763e5c0013802e392818
  71. <font color=OrangeRed>git ls-tree HEAD</font>  内部命令：显示某个git对象
  72. <font color=OrangeRed>git rev-parse v2.0</font>  内部命令：显示某个ref对于的SHA1 HASH
  73. <font color=OrangeRed>git reflog</font>  显示所有提交，包括孤立节点
  74. <font color=OrangeRed>git show HEAD@{5}</font>
  75. <font color=OrangeRed>git show master@{yesterday}</font>  显示master分支昨天的状态
  76. <font color=OrangeRed>git log --pretty=format:'%h %s' --graph</font>  图示提交日志
  77. <font color=OrangeRed>git show HEAD~3</font>
  78. <font color=OrangeRed>git show -s --pretty=raw 2be7fcb476</font>
  79. <font color=OrangeRed>git stash</font>  暂存当前修改，将所有至为HEAD状态
  80. <font color=OrangeRed>git stash list</font>  查看所有暂存
  81. <font color=OrangeRed>git stash show -p stash@{0}</font>  参考第一次暂存
  82. <font color=OrangeRed>git stash apply stash@{0}</font>  应用第一次暂存
  83. <font color=OrangeRed>git grep "delete from"</font>  文件中搜索文本“delete from”
  84. <font color=OrangeRed>git grep -e '#define' --and -e SORT_DIRENT</font>
  85. <font color=OrangeRed>git gc</font>
  86. <font color=OrangeRed>git fsck</font>
  87. <font color=OrangeRed>git archive</font>  生成一个可供发布的压缩包

## 学习内容
+ 初始化一个Git仓库时，使用git init命令；
+ 添加文件到Git仓库分为两步：
  1. 使用命令git add [file],注意可反复多次使用，添加多个文件；
  2. 使用命令git commit -m "message",完成提交；
+ 注：用vi [file]来编辑文件，进入后按“i”键进入编辑状态（出现--INSERT--），编辑完后按esc键后输入:wq退出；
+ 要随时掌握工作区状态，使用git status命令；
+ 如果git status告诉你文件被修改过，可以用git diff查看修改内容；
+ 想要查看文件内容时，可以使用命令cat [file]
+ 穿梭历史版本
  + HEAD指向的版本就是当前版本，Git允许我们在版本历史之间穿梭
  + 使用命令git reset --hard commit_id ,（上个版本是HEAD^,上上个版本是HEAD^^,往上100个版本是HEAD~100）
  + 穿梭前，可以使用git log查看提交历史，以便确定要回退到哪个版本
  + 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本
+ 问题：编辑完文件后使用git add [file]时出现：warning:LF will be replaced by CRLF the next time Git touches it.
  + 原因：在文本处理中，CR（CarriageReturn），LF（LineFeed），CR/LF是不同操作系统上使用的换行符
  + Dos和Windows平台： 使用回车（CR）和换行（LF）两个字符来结束一行，回车+换行(CR+LF)，即“\r\n”
  + Mac 和 Linux平台：只使用换行（LF）一个字符来结束一行，即“\n”
+ 问题：为什么Git添加文件需要add与commit两步
  + 因为commit可以一次提交很多文件，所以可以多次add不同文件，然后一并提交到仓库
+ 理解工作区与版本库（含暂存区）
  + 工作区：即在电脑里能所看到的目录
  + 版本库：作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库，Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD
+ 将文件添加到Git版本库时
  1. git add 实际上是把文件修改添加到暂存区
  2. git commit 实际上是把暂存区的所有内容提交到当前分支，就是向当前分支上提交更改
+ 撤销修改
  + git checkout --file 可以丢弃工作区的修改，将文件在工作区的修改全部撤销，分为两种情况：
    1. 文件自修改后还没有被放到暂存区，撤销修改就回到和版本库一模一样的状态
    2. 文件已经添加到暂存区后，又作了修改，撤销修改就回到添加到暂存区后的状态
  + 使用命令git reset HEAD [file]可以把暂存区的修改撤销掉（unstage），重新放回工作区
  + 已经提交了不合适的修改到版本库时，想要撤销本次提交，可以进行版本回退，前提是没有推送到远程库
+ 删除文件
  + 一般情况下，你通常直接在文件管理器中把没用的文件删除，或者用rm命令删除，此时的工作区和版本库就不一致了
  + 确定要从版本库中删除文件，那就用命令git rm删掉，并且git commit
  + 误删时，由于版本库里还有，可以把误删的文件恢复到最新版本，使用命令git chechout -- file,(只会丢失最近一次的修改)
    + git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”
    + 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的
+ 远程仓库
  + 创建GitHub账户：注册username,password,email
  + SSH加密：本地Git仓库和GitHub仓库之间的传输是通过SSH加密的
    1. 创建SSH Key：ssh-keygen -t rsa -C "youremail@example.com" ，一直回车，使用默认值即可
    2. 之后可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以告诉别人
    3. 登录GitHub->settings->SSH and GPG keys->填写title->在key文本框中粘贴id_rsa.pub内容->add key
  + 创建一个仓库
    + 在头像处找到“+”->new repository->填写Repository name->creat repository
  + 关联一个远程库，命令：git remote add origin git@server-name:path/repo-name.git
    + 关联一个远程库时必须给远程库指定一个名字，origin是默认习惯命名
    + 关联后，使用命令git push -u origin master第一次推送master分支的所有内容
    + 此后，本地提交后，可以使用命令git push origin master推送最新修改
  + 删除远程仓库
    + 使用git remote rm [name]命令
    + 使用前，可以先用git remote -v查看远程库信息
    + 此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库
  + 克隆远程仓库
    + git clone git@server-name:path/repo-name.git
    + Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议
+ 分支
  + 创建分支并切换至该分支（例如分支dev）：git checkout -b dev
  + git checkout命令加上-b参数表示创建并切换，相当于两条命令：git branch dev与git checkout dev
  + 用git branch命令查看当前分支，git branch命令会列出所有分支，当前分支前面会标一个*号
  + git merge命令用于合并指定分支到当前分支
  + 创建并切换到新的dev分支：git switch -c dev
  + 直接切换到已有的master分支：git switch master
+ 解决冲突
  + 当不同分支各自都有新的提交时，Git无法快速合并，只能试图将各自的修改合并起来，但这种合并可能会有冲突
  + git status命令会告诉我们冲突的文件
  + 用cat [file]查看文件时，Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
  + 冲突后我们要手动修改解决冲突后保存提交
  + 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交
  + 用git log --graph命令可以看到分支合并图
  + git log --graph --pretty=oneline --abbrev-commit 分支合并图较简洁
+ 分支管理
  + 通常合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息
  + 如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息
  + 当有另一个分支dev时，且该分支上有提交时，要使其与master主分支上进行合并，且禁用Fast forward模式时，要注意 --no-ff 参数
    + git merge --no-ff -m "..." dev
    + 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去
+ Bug分支
  + 软件开发中，经常需要修复bug，每个bug都可以新建临时分支来修复，修复后合并分支
  + 使用git stash命令，可以将当前工作区隐藏起来，等之后恢复后继续工作
  + 修复完bug后，切换到原来分支，工作区是干净的，只是因为Git把stash内容存在某个地方了，需要恢复一下，有两个办法：
    1. 用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除
    2. 用git stash pop，恢复的同时把stash内容也删了
  + 可以多次使用stash，恢复的时候，先用git stash list查看，然后恢复指定的stash
    + 命令：git stash apply stash@{0}
  + 当修复了一个分支上的bug后，其它分支上仍有相同bug时
    + 可以用git cherry-pick [commit]命令，把bug提交的修改“复制”到当前分支，避免重复修改文件
+ Feature分支
  + 在为软件添加一个新功能时，可以新建一个feature分支，在上面开发，最后合并到主分支再删除临时分支
  + 若要丢弃一个没有被合并过的分支，可以通过git branch -D [name]强行删除
+ 多人协作
  + 本地新建的分支如果不推送到远程，对其他人就是不可见的
  + 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交
  + 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致
  + 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name
  + 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突
+ git rebase操作可以把本地未push的分叉提交历史整理成直线
