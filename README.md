# Git / Skills 
### LEARNGING PROCEDURE
#### [1.基本用法](#chapter1)
#### [2.版本回退](#chapter2)
#### [3.撤销修改](#chapter3)
#### [4.远程仓库](#chapter4)
#### [5.分支管理](#chapter5)

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

	$ git reset --hard HEAD^	 //
	$ git reset --hard 0e4f7bb // 退回到版本号
	$ git reflow // 可以查看所有历史记录和版本号
	$ cat README.md //可以查看文件内容
	
#### [3.撤销修改](id:chapter3)
可以配合git reset --hard HEAD file 一起使用

	$ git checkout -- README.md //撤销到最近一次add或commit时的状态
	---
	$ rm README.md //版本库里删除文件
	$ git checkout -- README.md // 一键还原删除文件，因为版本库里还有。
---
#### [4.远程仓库](id:chapter4)
 	1) 创建SSH key. 查看主目录.ssh是否有id_rsa,id_rsa.pub.
 	2) 如果没有，创建SSH key:
 	---
 	$ ssh-keygen -t rsa -C 'youremail@example.com'
 	---
 	3) id_rsa是私钥不要泄露，id_rsa_pub是公钥可以暴露
 	4) 登陆Github,进入settings,找到SSH keys,添加新SSH key,填上id_rsa_pub.
 	5) Github需要知道是咱们自己提交的而不是别人所以需要SSH key.
 	
---

######>从远程仓库克隆

	1）登陆Github, 创建新仓库 For example: ohMyLove
	2）$ git clone git@github.com:xxx/ohMyLove.git
	3）Git原生的git协议比https协议更快
	
#### [5.分支管理](id:chapter5)
	$ git checkout -b dev //创建并切换到dev分支
	
	>等同于：
	$ git branch dev //创建分支dev
	$ git checkout dev //切换分支dev
	
	查看分支：
	$ git branch //查看分支
	
	dev分支工作完成后：
	$ git checkout master //切换到主分支
	$ git merge dev // 把dev上工作内容合并到master上
	//git merge 用于合并指定分支到当前分支
	
	合并完成后删除分支dev分支
	$ git branch -d dev // 删除dev分支
	$ git branch //可以查看分支情况
	
合并分支一般是Fast forward模式，删除分支后，会丢掉分支信息。

合并是加上 --no-ff参数可以变为普通合并模式。可以查看历史记录。

	$ git merge --no-ff -m 'merge with --no-ff' dev

因为此次合并Git会生成一个新的commit，所以加上-m.
	