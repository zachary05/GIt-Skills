# Gits / Kills 
### LEARNGING PROCEDURE
#### [1.基本用法](id:basic)
#### [2.版本回退](id:back)

#####  [1.基本用法](#basic)
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
##### [2.版本回退](#back)

HEAD是当前版本，HEAD^是上个版本，HEAD~100上一白个版本

	git reset --hard HEAD^	 //
	git reset --hard 0e4f7bb // 退回到版本号
	git reflow // 可以查看所有历史记录和版本号
	cat README.md //可以查看文件内容
	
