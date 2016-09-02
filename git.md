#git常用命令
>工作区有一个隐藏目录.git，是Git的版本库。里面有git的配置文件。

####本地命令
1. `git help`    *git帮助命令*
2. `git config` *git配置命令*
3. `git init` *初始化一个repository，或者在一个已存在的版本库中重新初始化。*
4. `git add <file1> <file2> ...` *把文件加入到索引区index*
5. `git add .` *把当前工作区变动的所有文件添加到index*
6. `git commit -m '提交的信息'` *提交index到版本库*
7. `git commit -a -m "commit content"` *假如嫌git add麻烦，可以直接这样提交*
8. `git commit` *会强制弹出vim编辑器来编辑‘提交信息’，必须。*
9. `git log` *查看commit提交历史* 
10. `git reflog` *重返未来，查看commit历史* 
11. `git reset --hard commit_id` *版本回退。HEAD表示当前版本，Reset current HEAD to the specified state*
12. `git rm <filename>` *用于删除一个文件，Remove files from the working tree and from the index*
13. `git rm --cached <filename>` *从版本库删除，但是在本地保留。.gitignore*
14. `git mv filefrom fileto` *修改文件名字或路经，Move or rename a file, a directory, or a symlink*
15. `git diff` *查看工作区和版本库里面最新版本的区别*
16. `git checkout -- <filename>` *可以丢弃工作区的修改,总之，就是让这个文件回到最近一次git commit或git add时的状态。* 
17. `git reset HEAD <filename>` *把暂存区的修改撤销掉（unstage），重新放回工作区*
18. `git revert` *是生成一个新的提交来撤销某次提交，此次提交之前的commit都会被保留* 
19. `git reset` *是回到某次提交，提交及之前的commit都会被保留，但是此次之后的修改都会被退回到暂存区*

-----------
####远程命令
1. `git clone git@github.com:<username>/<repositoryName>.git` *克隆远程版本库(所有人都可以克隆github-free)*
2. `git remote add origin git@github.com:<username>/<repositoryName>.git` *把本地版本库的当前分支关联到远程服务器的origin分支（有权限才可以关联，sshkey，github-free）*
3. `git push -u origin master` *第一次推送版本到远程分支*
4. `git push origin master` *推送*
5. `git pull origin master` *从远程抓取分支，如果有冲突，要先处理冲突*