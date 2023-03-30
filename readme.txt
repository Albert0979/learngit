Git is a distributed version control system.
Git is free software distributed under the GPL.

git init 初始化仓库
git add  暂存修改
git commit -m ""  提交，消息
git status   当前状态
git log    提交历史
git log --pretty=oneline   简化显示
git reset --hard HEAD^  退回到上一个版本  HEAD^^ 上两个版本 HEAD~n  第前n个版本
git reset --hard <提交的版本号（不用全输）>   回到相应的版本
git reflog       记录你的每一次命令