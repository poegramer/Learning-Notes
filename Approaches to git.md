### 本地安装git
#### 1.安装git
* **sudo apt-get update**
* **sudo apt-get install git**

#### 2.配置SSH
##### 创建SSH Key
1. 在用户主目录下，看看有没有.ssh目录(/home/xxx/.ssh)：如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，创建SSH Key：
    * **ssh-keygen -t rsa -C "youremail@example.com"**
    * (你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。)
    * 如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”，你就应该看到已经添加的Key：

>* 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。  
>* 当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

##### 验证SSH链接是否成功
* **ssh -T git@github.com**
>成功结果为：Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.  
>第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告，输入yes回车即可。  
>&emsp;&emsp;　The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.  
>&emsp;&emsp;　RSA key fingerprint is xx.xx.xx.xx.xx.  
>&emsp;&emsp;　Are you sure you want to continue connecting (yes/no)?

#### 3.初始化目录
* **git init**
>这样就在本地建立了git仓库，可以直接操作git其他命令。  
>此命令执行后，在执行命令的目录下会出现.git文件夹，该文件夹默认为隐藏，可以使用ls -a命令或Ctrl+h查看。

### 建立本地仓库与github关联
#### 4.本地配置github
* **git config --global user.name "Your Name"**
* **git config --global user.email "youremail@domain.com"**
>查看配置信息:  
>    * **git config --list**

#### 5.本地库与github关联
* **git remote add origin https://github.com/你的github用户名/github仓库名.git**
>关联后可以在.git目录下的config文件中查看结果：  
>&emsp;&emsp; [remote "origin"]  
>&emsp;&emsp;    url = git@github.com:haoxr/-faceDetection.git  
>&emsp;&emsp;    fetch = +refs/heads/*:refs/remotes/origin/*  
>可能会出现 the repository exists. 提示，表示你重复关联了，如果需要重置，可以直接在以上文件中删掉，也可以命令：  
>    * **git remote rm origin**

### 克隆github已有仓库及提交到github（下载更新及上传）
#### 6.克隆github上已有的仓库（下载到本地）
* **git clone https://github.com/你的github用户名/github仓库名.git**

#### 7.提交更改内容到github
* **git add 更改文件名或者是文件夹名或者是点"."**
>添加更新的文件

* **git commit -m "commit内容标注"**
>提交到本地库

* **git push origin master**
>* 第一次推送master分支时，加上-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来(**git push -u origin master**);  
>* 在以后的推送或者拉取时就可以简化命令，只要本地作了提交，就可以通过命令把本地master分支的最新修改推送至GitHub;  
>* 提交的文件有大小限制，注意大文件的移除和备份.

#### 8.重命名文件
* **git mv "原文件名" "新文件名"**
>将文件重命名，可用以下命令查看重命名的文件：
>* **git status -s**
>* 命令执行结果：**R "原文件名"　->　“新文件名”**
>* Git在文件名之前显示R，表示文件已被重命名

* **git commit -a -m "commit内容标注"**
>提交文件，需要使用-a标志，这使git commit自动检测修改的文件

* **git push origin master**
>推送文件

#### 9.删除文件
* **git rm "文件"**
* **git rm -r "文件夹"**
>删除本地仓库的文件或文件夹  
>此处**-r**表示递归所有子目录，如果要删除的是空文件夹，则可以省略

* **git commit -m "commit内容标注"**
>提交代码

* **git push origin master**
>推送到远程仓库
















