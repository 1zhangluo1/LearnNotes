# Git上传代码：

## 1.创建本地仓库

![image-20231127180747336](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231127180747336.png)

点击此处，能够直接打开文件夹，之后右键进入gitbush，输入git init就建好了本地仓库。

## 2.github上创建远程仓库

![image-20231127181301696](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231127181301696.png)

## 3.将要加的东西推到本地仓库

1.git add 此处为文件名（git add.是提交此文件夹全部文件的意思，就是add后面加一个点.）

2.git commit -m“提交描述”

## 4.上传本地仓库到github

该项目第一次上传时：

1.设置分支名字	git branch -M main

2.添加远程仓库地址	git remote add origin 此处为github上生成仓库时的地址

3.传到github上的远程仓库  git push -u origin main

如果不是第一次上传，直接push就行：

git push origin main

三部曲（add，commit，push）