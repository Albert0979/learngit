Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.


git init 初始化仓库
git add  暂存修改
git commit -m ""  提交，消息
git status   当前状态
git log    提交历史
git log --pretty=oneline   简化显示
git reset --hard HEAD^  退回到上一个版本  HEAD^^ 上两个版本 HEAD~n  第前n个版本
git reset --hard <提交的版本号（不用全输）>   回到相应的版本
git reflog       记录你的每一次命令

#  git 工作区和暂存区

工作区(working directory)
就是电脑里能看到的目录

版本库(repository)
工作区有一个隐藏目录 .git , 这是git的版本库
版本库里有很多东西，有叫 stage(or index)的暂存区, git 自己帮你创建的第一个分支 master 以及指向
master 的一个指针 HEAD.

git add 指令实际上就是把文件加入到暂存区
git commit 就是把暂存区里的文件提交到当前分支

我们再创建Git版本库时git自动创建了一个也是唯一一个分支 master, git commit 就是往master 上提交更改

git restore <file>  撤销在工作区里的修改，如果stage里没文件，撤回到版本库里的状态，
                                         stage里有文件，就撤回到暂存区后的状态

git restore --staged <file>    从stage里取消文件
如果提交了，就退回到上一个版本   git reset --hard HEAD^


删除文件
手动删或 rm <file>
git rm <file>
git commit -m <message>
撤销删除
在commit删除 之前 git restore <file>
在commit删除 之后 版本回溯

创建公钥私钥
在用户界面 Git Bush 
输入 ssh-keygen -t rsa -C "youremail@example.com"
会有提示消息，点回车
（ok）
用 ls ~/.ssh 查看


添加远程库
先在GitHub上创建一个库，创建之后它会告诉你怎么关联本地库
第一次关联会有一个警告，可以对比一下，输入 yes 回车即可
之后就只要 git push origin <branch> 就可以把本地的branch分支推送到GitHub上