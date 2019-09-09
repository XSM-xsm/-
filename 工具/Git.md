# Git配置

ssh-keygen -t rsa -C "[71073534@qq.com](mailto:71073534@qq.com)"　生成SSH Key
id_rsa是私匙 id_rsa.pub是公匙（公匙和私匙的作用，属于密码学，百度！）
git config --global user.name "care526Lj"　配置user.name
git config --global user.email "[710783534@qq.com](mailto:710783534@qq.com)"　配置user.email

# 项目初始化

git init　　初始化版本库
配置需要版本控制的文件/目录和要忽略的文件/目录
在工作目录创建 .gitignore 文件
*.zip　 　 ＃忽略所有以 .zip 结尾的文件!lib.zip　 ＃lib.zip文件添加到版本控制build/　　 #忽略build目录下的所有文件doc/*.txt #忽略doc目录下的所有以 .txt 结尾的所有文件

# 远程仓库

git remote add origin [git@github.com](mailto:git@github.com):care526/learnGit.git　
为当前仓库添加远程仓库，后面的一长串是该远程仓库的地址
也可以用https的地址，如<https://github.com/care526/learnGit.git>
origin是远程库的默认name，也可以改成别的名字

# 克隆

git clone .git name 由某版本库克隆生成一个新的目录
git clone [git@github.com](mailto:git@github.com):care526/learnGit.git　克隆远程库到本地

# 版本提交／查看／回退／撤销

[![image](https://github.com/care526/blog/raw/master/%E8%BF%90%E7%BB%B4/clipboard.png)](https://github.com/care526/blog/blob/master/%E8%BF%90%E7%BB%B4/clipboard.png)
git add xxx　　添加某文件到暂存区，可使用多次添加多个文件
git add .　　添加所有文件
git commit -m "xxx"　　将添加到暂存区的文件更新同步到版本库
git push -u origin master　　将本地库的内容推送到远程库（第一次提交要加-u,之后可以省略）
git push -f XXXXXX 强制将本地代码覆盖远端的代码

git status　　查看当前的修改了那些文件
git diff filename　　查看具体修改了什么内容， filename是文件名

git log　　查看版本推送更迭历史记录
git log --pretty=oneline　　同上，简化输出
git log --graph --pretty=oneline --abbrev-commit　　同上，还可以看到分支的合并情况

git log --stat --summary　查看每一次版本的大致变动情况
git show dfb02e6e4f2f7b573337763e5c0013802e392818（版本号）　查看该版本的更新信息，也可以只写该版本的前几位dfb02e
git show HEAD^ # 查看 HEAD 的父版本更新细节
git show HEAD^^ # 查看 HEAD 的祖父版本更新细节
git show HEAD~4 # 查看 HEAD 的上四个版本更新细节
git tag v0.1 dfb02　对dfb02版本生成一个自定义的版本号，对未来发布有好处
git reflog　　查看每一次的记录

git reset --hard HEAD^　　回退到上个版本
git reset --hard HEAD^^　 回退到上上个版本（^的个数以此类推）
git reset --hard HEAD~10 回退到上10个版本（免得 ^ 写的太长）
git reset --hard commit_id 回退到指定版本，commit_id是某个版本号（版本号很长，可以只写前面几位）

git checkout -- a.txt　　将a.txt的修改撤销，a.txt会自动回到修改前的状态
两种情况，如果已经add了，那么将会回到暂存区里的文件内容，如果没有，将回到工作区修改前的状态，总之，就是回到最近的一次的git commit 或 git add的状态
git reset HEAD filename　　将某个文件从暂存区的修改回退到工作区（如果是上面的第二种情况，就先用这个命令回到暂存区的修改状态，再回到工作区的修改状态）
git rm filename　　删除某个文件，之后再commit就行了（如果用rm删除，要先git add . 再git commit）

# 分支

创建分支的目的是在不影响主分支的情况下进行开发，在分支完成的时候将分支的内容和主分支合并即可
git branch dev　　创建dev分支
git checkout dev　　切换到dev分支
git checkout filePath 还原未提交的该文件到上次提交
git checkout . 还原未提交的所有文件到上次提交
git checkout -b dev　　创建dev分支，并切换到该分支（等于上面两个命令之和）
git branch　　查看当前分支
git branch -a　　查看所有分支
git merge dev　　合并dev分支到当前分支
git merge --no-ff -m "XXX" dev　　将dev分支合并到当前分支（不采用Fast forward模式），并创建commit描述，提交一次，XXX是这次提交的修改内容
git push --set-upstream origin dev　　在远程库创建分支并推送
git push origin dev　　只是推送分支（如果之前已经创建了）
git branch -d dev　　删除dev分支（如果dev没有合并到当前分支，会有提示）
git branch -D dev　　强制删除dev分支，不管合没合并
git push origin --delete dev　　删除远程库上的dev分支
如果当前分支和主分支都提交的修改，但是修改的内容是不同的，我们在合并分支的时候就会发生冲突（相同文件的内容冲突），我们要手动修改两个分支为相同，然后才能合并分支，再删除

修改某个分支的bug的时候，先在当前分支分一个分支，在分好的分支上进行修改，修改完了合并分支，再删除分出来的分支。 开发新功能的时候，也是先分一个功能分支，开发实验结束后再合并，删除，流程同bug分支

git stash　　隐藏当前分支上工作区的修改
git stash list　　查看隐藏的内容
git stash apply　　恢复隐藏内容，不删除记录的隐藏内容
git stash drop　　删除恢复的隐藏内容
git stash pop　　恢复隐藏内容的同时将隐藏内容一并删掉
git remote　　查看远程库
git remote -v　　查看远程库详细信息（是否可提交 | 是否可拉取）
git push origin master　　推送主分支到远程库
git push origin dev　　推送dev分支到远程库
git checkout -b dev origin/dev　　拉取远程库的分支到本地并切换
git push origin dev　　推送分支到远程库
git pull　　抓取远程库的新提交
git branch --set-upstream dev origin/dev　　建立远程库分支与本地分支的关联
当其他人对你要用的分支做了提交，远程库的分支领先于你的本地分支，要先拉取远程库的分支与本地合并，再做开发。如果拉取的分支和当前有冲突，要先解决冲突。

合并分支的时候，发生冲突，解决完冲突后，已经合并，只需要commit一下就ok了