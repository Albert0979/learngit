Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
Creating a new branch is quick and easy.

nothing happens

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
关联之后第一次push加u参数 git push -u origin master,   这一Git会把本地master分支内容推送到新的master分支，还会把本地master分支和远程的master分支关联起来
第一次关联会有一个警告，可以对比一下，输入 yes 回车即可
之后就只要 git push origin <branch> 就可以把本地的branch分支推送到GitHub上


删除远程库
git remote rm <name>
使用前可以先用
git remote -v 查看远程库信息
这个删除只是解除了本地仓库和远程仓库的关系


从远程库克隆
先创建一个repository，用它教你的命令clone一个


Git 分支
git 中 HEAD指向的时分支，初始时是master，master再指向提交，创建分支其实
就是更改指向提交的指针，再把HEAD指向那个指针，你对工作区的更改、提交都是针对你目前所在的
分支而言的（也就是HEAD所指向的分支）

创建分支  git branch <branch name>
转到相应分支  git checkout(or switch) <branch name>
上面两个命令的合并  git checkout -b <branch name>    or    git switch -c <branch name>

分支的合并
比如你在dev上做完了一些工作，要把dev合并到master上，有以下方法：
1.直接将master指向dev的当前提交，合并后如果想删除分支用 git branch -d <branch name>
2.合并可能并不怎么简单，比如出现“冲突”,这个时候需要你自行修改，再提交，然后合并完成了
用  git log --graph 可以查看分支合并图

删除分支 git branch -d <name>


分支合并的时候，如果可以的话Git会优先使用 Fast forward 模式（就是直接把 master 指针切换到分支那里）
如果要禁用 Fast forward 模式合并分支，那 Git 在合并分支的时候会生成一个提交 commit, 
例如用 --no-ff 方式 git merge

git merge --no-ff -m "merge with no-ff" dev




Bug 分支
设想这样一个情况：你在某个分支上做事，但突然项目出了一个bug，自然你需要创建一个分支来修复这个bug，
但你不想或不能commit现在这个分支，你可以用
git stash save "message" 储藏这个分支并标记信息，没有信息可以直接用 git stash
修复好bug后想回到这个状态，你要先回到这个分支然后用
git stash pop 来回到暂存状态并清空储藏
git stash list  查看储藏的状态列表
git stash apply stash@{n}  回到指定状态并不删除储藏的状态
git stash pop stash@{n}    会删除

git cherry-pick <commit id>  复制一个特定的提交到当前分支



feature分支
创建一个新feature,最好新建一个分支
要丢弃一个没有合并的分支，用
git branch -D <name> 强制删除
