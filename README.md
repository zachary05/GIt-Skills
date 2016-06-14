# Git / Skills 
### LEARNGING PROCEDURE
#### [1.基本用法](#chapter1)
#### [2.版本回退](#chapter2)
#### [3.撤销修改](#chapter3)
#### [4.远程仓库](#chapter4)
#### [5.分支管理](#chapter5)
#### [6.Bug分支](#chapter6)
#### [7.多人合作](#chapter7)
#### [8.标签管理](#chapter8)
#### [9.配置 Git](#chapter9)


####  [1.基本用法](id:chapter1)
	$ mkdir fileA //创建仓库(make dir) 
	
	$ cd fileA //进入当前文件夹
	
	$ pwd //查看当前文件路径
	

---
	$ git init //初始化git仓库
---
在文件夹里创建文件后(如README.md)：

执行下面命令会没有反应，没有消息是好消息。

	$ git add README.md //添加文件
	
	$ git add file1.md file2.md file3.md //git add可以一次提交多个文件

---
-m后是本次提交的说明：

	$ git commit -m 'write a readme.ad' //提交到仓库
	

---
	$ git status //查看当前状态
	
	$ git diff //查看修改内容
	
	$ git log //查看提交的历史记录,q退出
	
	$ git log --pretty=oneline //可以简单化历史记录


---
#### [2.版本回退](id:chapter2)

HEAD是当前版本，HEAD^是上个版本，HEAD~100上一白个版本

	$ git reset --hard HEAD^	 
	
	$ git reset --hard 0e4f7bb // 退回到版本号
	
	$ git reflog // 可以查看所有历史记录和版本号
	
	$ cat README.md //可以查看文件内容
	
#### [3.撤销修改](id:chapter3)
可以配合git reset --hard HEAD file 一起使用

	$ git checkout -- README.md //撤销到最近一次add或commit时的状态
	
	$ rm README.md //版本库里删除文件
	
	$ git checkout -- README.md // 一键还原删除文件，因为版本库里还有。
---
#### [4.远程仓库](id:chapter4)
 	1) 创建SSH key. 查看主目录.ssh是否有id_rsa,id_rsa.pub.
 	
 	2) If没有，创建SSH key:
 	
 		$ ssh-keygen -t rsa -C 'youremail@example.com'
 	
 	3) id_rsa是私钥不要泄露，id_rsa_pub是公钥可以暴露
 	
 	4) 登陆Github,进入settings,找到SSH keys,添加新SSH key,填上id_rsa_pub.
 	
 	5) Github需要知道是咱们自己提交的而不是别人所以需要SSH key.
 	
---

######>从远程仓库克隆

	1）登陆Github, 创建新仓库 For example: ohMyLove
	
	2）$ git clone git@github.com:xxx/ohMyLove.git
	
	3）Git原生的git协议比https协议更快
	
#### [5.分支管理](id:chapter5)
	创建分支：
	$ git checkout -b dev //创建并切换到dev分支
	
	>等同于：
	$ git branch dev //创建分支dev
	
	$ git checkout dev //切换分支dev
	
	查看分支：
	$ git branch //查看分支
	
	dev分支工作完成后：（切换主分支，进行合并）
	$ git checkout master //切换到主分支
	
	$ git merge dev // 把dev上工作内容合并到master上
	
	合并完成后删除分支dev分支：
	$ git branch -d dev // 删除dev分支
	
	$ git branch //可以查看分支情况
	
合并分支一般是Fast forward模式，删除分支后，会丢掉分支信息。

合并是加上 --no-ff参数可以变为普通合并模式。可以查看历史记录。

	$ git merge --no-ff -m 'merge with --no-ff' dev

因为此次合并Git会生成一个新的commit，所以加上-m.

---
如果要加入一个新的特征(feature)，最好新建一个分支，然后进行合并，再删除
	
#### [6.Bug分支](id:chapter6)
当接到BUG时，若要在master上创建issue-01分支进行修复，可是当前分支dev工作没有完成。

使用git stash将当前工作现场dev储藏起来。
	
	$ git stash // 储藏
	
然后切换到master支上创建并切换到issue-01分支上：

	$ git checkout master
	
	$ git checkout -b issue-01

issue-01修改结束后，切换到master进行合并，并删除issue-01:

	$ git checkout master
	
	$ git merge --no-ff -m 'fix issue-01' issus-01 
	
	$ git branch -d issue-01 //删除issue-01分支
	
现在完成的修复Bug任务，可以回到dev上工作：

	$ git checkout dev
	
	$ git stash list //查看储藏的内容
	
	$ git pop // 恢复之前的工作
	
#### [7.多人合作](id:chapter7)

当从远端仓库克隆时，实际上是将本地master分支和远端master分支对应起来。远端仓库的默认名称是origin,可以查看：

	$ git remote // origin
	
	$ git remote -v // 查看详细信息
	
	origin	git@github.com:zachary05/gitskills.git (fetch)
	
	origin	git@github.com:zachary05/gitskills.git (push)
	
上面显示了可以推送和抓取的origin的地址，如果没有推送权限则没有push的地址。

---
**推送分支**

	$ git push origin master
	
推送时要指定本地分支，这样本地分支可以推送到远端仓库对应的分支。

---
**抓取分支**

* 多人合作时，大家会各自推送到master和dev分支上。

* 当从别人远端仓库克隆仓库时。一般只会有master分支。

* 但是如果要在dev分支上工作，必须创建远程origin的dev到本地。

---

	$ git checkout -b dev origin/dev
	
	$ git push origin dev //推送dev分支到远端
	
	
本地dev与远程dev建立联系：
	
	$  git branch --set-upstream dev origin/dev
	
如果和别人对同一文件的修改存在冲突，则先抓取下来进行修改，再提交。

	$ git pull //抓取分支
	
#### [8.标签管理](id:chapter8)
创建标签:


	$ git tag <name>//eg: $ git tag v.01
	
	$ git tag <name> <commit:id> //在对应commit上打标签。
	
	$ git tag -a v.01 -m 'version v.01 released' 8678979 //创建带有说明的标签。

查看标签:

	$ git tag

查看标签信息：

	$ git show <tagname>

删除标签：

	$ git tag -d v.01 //删除v.01标签
	
推送标签到远程：

	$ git push origin v.01 
	
	$ git push --tags //一次性推送未推送的标签。
	
如果要删除远程标签： (先删除本地标签，在删除远程标签)

	$ git tag -d v.01 //本地删除 v.01
	
	$ git push origin :refs/tags/v.01 // 远程删除 v.01
#### [9.配置Git](id:chapter9)

显示颜色：

	$ git config --global color.ui true

快捷方式的配置：

	$ git config --global alias.st status // git st 显示状态
	
	$ git config --global alias.ck checkout // git ck 切换分支
	
	$ git config --global alias.co commit // git co 提交
	
	$ git config --global alias.br branch // git br 分支
	
	$ git config --global alias.unstage 'reset HEAD' // git unstage 撤销暂存区的修改
	
	$ git config --global alias.last 'log -1' // 显示最后一次提交
	
	$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit" // git lg显示（我承认这个很无敌）记录
	
配置文件

配置git时，加上--global是对全局起作用，如果不加，只对当前文件夹起作用。

每个仓库的git配置都放在了.git/config里面

如果要删除直接把[alias]对应的删掉。

---

全局配置的git文件在用户主目录的.gitconfig文件中

---
	
* 忽略特殊文件：（如一些数据库密码）

* 必须把这些文件放在工作目录中，但是不能提交他们，但每次git st时都会显示Untracked file...

* 这个时候在文件夹中创建'.gitignore'，把这些要忽略的文件名填写进去就OK了。

* Github为我们准备了各种配置文件：https://github.com/github/gitignore

---
#### Useful Git-Related Websites：

1.[Git官网](http://git-scm.com)

2.[Git Cheat Sheet](http://pan.baidu.com/s/1jGxjQL4#path=%252Fpub%252Fgit)