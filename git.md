#git基础

#### 基础概念

#### 参考资料
1. [廖雪峰Git教程][1]


#### 本地命令
1. `git help`    *git帮助命令*
2. `git config` *git配置命令*
3. `git init` *初始化一个repository，或者在一个已存在的版本库中重新初始化。*
4. `git status` *显示状态*
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

#### 远程命令
1. `git clone git@github.com:<username>/<repositoryName>.git` *克隆远程版本库(所有人都可以克隆github-free)*
2. `git remote add origin git@github.com:<username>/<repositoryName>.git` *把本地版本库的当前分支关联到远程服务器的origin分支（有权限才可以关联，sshkey，github-free）*
3. `git push -u origin master` *第一次推送版本到远程分支*
4. `git push origin master` *推送*
5. `git pull origin master` *从远程抓取分支，如果有冲突，要先处理冲突*
6. `git remote` *查看远程库的信息*
7. `git remote -v`*查看远程库的详细信息*
8. `git checkout -b branch-name origin/branch-name`*在本地创建和远程分支对应的分支*
9. `git branch --set-upstream branch-name origin/branch-name` *建立本地分支和远程分支的关联*

#### 分支
1. `git branch` *查看版本库的分支列表*
2. `git branch <branchname>` *创建新分支*
3. `git branch -d <branchname>` *删除分支*
4. `git checkout <branchname>` *切换到分支*
5. `git checkout -b <branchname>`*创建并切换分支*
6. `git merge <branchname>`*合并指定分支到当前分支   有2种情况1⃣️fast_forward方式2⃣️conflict方式。第一种方式直接合并，第二种方式先手动解决冲突，再git add,git commit.*

#### 标签
1. `git tag <name>` *创建新标签 eg:git tag v1.0。默认标签是打在最新提交的commit上的*
2. `git tag`*查看所有标签*
3. `git tag v0.9 <commit-id>`*在某次commit上打标签*
4. `git tag -a v1.0 -m "version 1.0 released" <commit-id>`*创建带有说明的标签，用-a指定标签名，-m指定说明文字*
5. `git show <tagname>`*查看标签信息*
6. `git tag -d <tagname>`*可以删除一个本地标签*

#### .gitignore文件
1. .gitignore *忽略文件*
2. `git check-ignore -v <path/filename>`*检查.gitignore文件配置文件规则*


#### **git配置**`git config` 
1. `git config --list` *查看git的配置*
1. `git config --global user.name "Your Name"`
2. `git config --global user.email "email@example.com"`
3. `git config --global color.ui true`*显示颜色*
4. `git config --global alias.st status`*配置git命令的别名`git st`代表`git status`*

#### git安装
1. MacOS
2. Windows
3. Linux

#### git服务器安装



[1]:http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/












