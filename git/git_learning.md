## Git Learning
#### Git 本地用户名和邮箱
1. 用户名和邮箱地址的作用: \
用户名和邮箱地址是本地git客户端的一个变量，不随git库而改变。
每次commit都会用用户名和邮箱纪录。
github的contributions统计就是按邮箱来统计的。
2. 查看用户名和邮箱地址:\
$ git config user.name \
$ git config user.email
3. 修改用户名和邮箱地址：\
$ git config --global user.name "username" \
$ git config --global user.email "email" \
(--global参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。)

#### Git仓库托管服务
- 第1步：创建SSH Key：\
$ ssh-keygen -t rsa -C "youremail@example.com" \
将在.ssh目录，里面创建id_rsa和id_rsa.pub两个文件，这两个是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。\
- 第2步：登陆GitHub/Gitee 、
“Add SSH Key” -> 填写id_rsa.pub里的内容，名字任意\
因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送；GitHub允许你添加多个Key。

#### 版本控制基本操作
版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。\

- 创建版本库、初始化 \
$ mkdir learngit \
$ cd learngit \
$ git init \
$ git add <file> \
$ git commit -m <message> \
$ git status \
(通过git init命令把这个目录变成Git可以管理的仓库,当前目录下多了一个.git的目录) \

$ git reset --hard HEAD \
(回退到上一次提交的版本；Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，HEAD^上一个版本，HEAD^上上一个版本)
$ git reset --hard commit_id \
(HEAD指向的版本就是当前版本) \
$ git log \
(查看提交历史，以便确定要回退到哪个版本) \
$ git reflog \
(查看命令历史，以便确定要回到未来的哪个版本)\


场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 \
$ git checkout -- file \

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 git reset HEAD <file>，就回到了场景1，第二步按场景1操作。 \

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。\

$git rm \
(用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。) \

#### 关联远程库 repository
- 要关联一个远程库，使用命令:\
$ git remote add origin git@server-name:path/repo-name.git \
(添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库)
- 关联后，使用命令: \
$ git push -u origin master \
第一次推送master分支的所有内容；
- 此后，每次本地提交后，只要有必要，就可以使用命令\
$ git push origin master \
推送最新修改；

####
