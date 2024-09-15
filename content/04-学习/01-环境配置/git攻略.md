#git
# 常用语句

加入 git ignore
打开终端程序（如 macOS 上的 Terminal.app）。然后，用 `cd` 命令导航到包含项目的根文件夹，并输入以下命令，为你的目录创建一个 `.gitignore` 文件：
```python
touch .gitignore
```


# 快速攻略
1. 下载
	1）官网 [git-scm.Com](https://git-scm.Com)
	2）Download for Windows
	3）64-bit Git for Windows Setup	
2. 安装
	1）下载完后一路回车法即可
3. 配置
	1）桌面右键点击 open git bash here
	2）打开界面后配置用户名
		Git config --global user. Name wujyuhin
	3）配置邮箱
		git config --global user. Email wujyuhin@haha.com
4. 代码管理
	1）从仓库 clone 到本地（链接为 github 项目的 code 底下的 https 链接）
		git clone https://github.com/JiaoyangXu-hub/CSnotes.git
	
	2）本地代码管理
		【初始化】
		git init  //初始化创建.git 文件夹 
		【提交所有代码】
		git add .   // 把当前文件夹的所有文件设置为准备提交状态
		git commit -m "功能1已完成"  // 提交准备状态的所有文件，备注一定要写，版本管理的作用
		【提交部分代码】
		git add main.py  // 把main.py设置为准备提交状态
		git commit -m "功能2已完成"   // 此时提交的文件是main.py
		【恢复代码】
		git checkout HEAD test.py  // 恢复之前保存的版本




# 问题
【问题 1】无法 clone 项目
如果出现
fatal: unable to access 'https://github.com/xxx/autowrite.git/': 
OpenSSL SSL_read: Connection was reset, errno 10054
或者
fatal: unable to access 'https://github.com/xxx/autowrite.git/':
Failed to connect to github. Com port 443: Timed out
	【问题 1 解决 1】
	Git config --global --unset http. Proxy  //取消 http 代理
	Git config --global --unset https. Proxy  //取消 https 代理 
	【问题 1 解决 2】
	科学上网，查看端口，本机端口为 7890
	git config --global http. Proxy http://127.0.0.1:7890




# 代码仓库管理的课程笔记

## 1.新建仓库
```python
mkdir learn-git
cd learn-git
git init
# =====创建完成
ls # 查看当前路径文件
ls -a # 查看当前路径所有文件
ls -altr # ?
cd .. # 退出
\rm -rf .git # 表示删除git仓库

git init my-repo # 指定生成git仓库名称
git clone 网址 # 从github上克隆
```

## 2.工作区等概念
工作区：实际操作的. Git 目录
暂存区：临时存放即将提交的修改内容
本地仓库：git 存储代码和版本信息主要位置
![[Pasted image 20240318155752.png]]

git add 将修改文件放到暂存区
git commit 是将暂存区所有文件一次性运送所有仓库

![[Pasted image 20240318160126.png]]



## 3.添加与提交文件

```python
git status # 查看git当前状态
echo "这是第一个文件">file1.txt
ls # 发现多了一个文件
cat file1.txt # 查看文件内容
git status # 查看状态
# 发现是untrack，未跟踪状态
git add file1.txt # 
git status # 发现是changes to be committed 已经在暂存区
# 命令行中多了一个加号，这是有修改但未提交的文件
git rm --cached file1.txt # 从暂存区拿回来
git commit # 只会提交暂存区文件
git commit -m "第一次提交"  # 对本次提交进行备注
# 可利用通配符add多个文件
git add *.txt
git add . # add所有文件
git commit # 提交后进入vim模式，i进入输入模式，esc推出输入模式，输入:wq保存退出：
git log # 提交记录
git log --oneline
```
![[Pasted image 20240318170539.png]]


## 4.回退版本

```python
git reset
git ls-files  # 查看暂存区内容
ls # 查看文件区
git reset --soft 回退的编号 
git reset --harf
git reset --mixed
```

![[Pasted image 20240318170654.png]]

	git reset --soft
	不改变现有文件，也不改变暂存区文件，只回退，
	注：回退了提交记录
	注：识别了后面添加的新文件

手动复制三个 my-repo 文件
然后分别进入使用回退功能
```python
git reset --hard HEAD^ # 表示回退到上一个版本
git reset --log中的编号
git ls-files # 查看暂存区文件
git reset HEAD^ # 相当于mixed

git reflog # 查看所有的记录，找到误操作之前的版本号进行回退
```

## 5.查看差异
![[Pasted image 20240318205306.png]]
```python
git diff # 默认比较工作区和暂存区的不同
```


## 6.删除
```python
法1
ls -ltr
rm file1.txt
# 如果暂存文件也有file1，那就需要git add .
法2
git rm file2.txt
# 不需要git add . 了
直接提交
git commit -m "delete file2.txt"


```

![[Pasted image 20240318212048.png]]

## 7.本地与 github 关联
如果本地没有仓库
```python
echo "# remote-repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:wujyuhin/LPKT.git
git push -u origin main
```

如果本地有仓库
```python
git remote add origin git@github.com:wujyuhin/LPKT.git
git branch -M main
git push -u origin main
# 如果已经进行关联过了，remote origin already exists，则
git remote rm origin
git remote add origin ssh名称
git push origin master
```

## 8.使用 shh 方法配置

配置密钥
```python
cd # 退回根目录
cd .ssh
ssh-keygen -t rsa -b 4096 # 指定协议指定大小
# 然后输入文件名后回车
# 然后输入密码回车
# 然后在输入密码回车 wujyuhin
ls -ltr # 查看发现多了id_rsa -d_rsa.pub
vi id_rsa.pub # 查看公钥文件
复制到github上配置ssh
```
Id_rsa 是私钥文件
Id_rsa.pub 是公钥文件

```python
如果上面没输入名称直接回车就不需要看了
如果上面是重新输入文件名的话，需要在git上输入以下五行
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/test
```

## 9.本地仓库与远程仓库的同步

如果远程建立仓库，本地也有仓库, 运行以下代码关联
```python
git remote add origin git@github.com:wujyuhin/CDM.git # git remote add <shortname><url>
git branch -M main  # 指定分支为main分支，若我们显示main可忽略
git push -u origin main  # 将本地main分支与远程origin仓库main分支关联
# 全称 git push -u origin main:main
```
但是可能会有以下报错
error: failed to push some refsto‘远程仓库地址’
成功解决办法：
```python
git pull --rebase origin main #保持本地目录干净
git push -u origin main
```
本地文件同步到远程
```python
git add .
git commit -m "第一次提交"
git push
```
远程同步到本地
```python
# github修改
git pull origin main # 表示将远程仓库别名origin拉到本地的mian
git pull # 如果不指定分支，默认是origin拉去到main分支
```
查看远程别名
```python
# 先查看我本地仓库所对应的远程仓库别名叫origin，以及对应的远程仓库
git remote -v
```
![[Pasted image 20240320103526.png]]


![[Pasted image 20240318221046.png]]
![[Pasted image 20240320110248.png]]

## 10.vscode 中使用 git
在命令行中输入
```python
code . # 打开python
```
在 vscode 中下载 git graph扩展
```python
ctrl shift p # 查询功能
ctrl shift ` # 打开终端 
```
源码管理器左侧第三个图标
在修改了代码之后点 commit、然后点 sync change 同步改变是和 git 上操作一样的!
![[Pasted image 20240320112953.png]]


## 分支

![[Pasted image 20240320152508.png]]
```python
echo main1>main1.txt
git add .
git commit -m "main:1"
-------------------------
echo main2>main2.txt
git add .
echo commit -m "main:2"
------------------------
echo main3>main3.txt
git add .
echo commit -m "main:3"
-----------------------
git branch  # 查看当前分支
git branch dev  # 创建一个名为dev分支
git cherkout dev  # 切换到dev分支，可到哪个分支的状态，但如果有文件同名则不能切换文件修改前的状态？这里不太懂
git switch dev  #  只会切换分支（可不用cherkout）
------------- dev -------------
echo dev1>dev1.txt
git add .
git commit -m "dev:1"
-------------------------------
echo dev2>dev2.txt
git add .
git commit -m "dev:2"
------------- main --------------
git switch main
echo main4>main4.txt
git add .
git commit -m "main:4"
--------------------------------
echo main5>main5.txt
git add .
git commit -m "main:5"
-------------------------------
# 经过上述操作已经两个分支已经分叉
# 如果需要将dev分支并入main分支中
git merge dev  # 分支不成功，输入信息之后再commit 
git branch -d dev  # 需要呗合并的分支才能删除
git branch -D dev  # 强制删除
git rebase
```

![[Pasted image 20240320170824.png]]


## 文件冲突管理

```python
vi main1.txt #修改main1文件
此处如何退出？
点i可以输入，点esc可以退出编辑
点大写的Z两次能退出为原本的命令行
git commit -a -m "feat:1"
```

![[Pasted image 20240320181803.png]]
# Rebase
 ```python
 git checkout -b dev 244d35# 切换为git,如果没看到后面编号就右键点选sha
让dev分支合并到main的最新commit后
git switch dev
git rebase main
 ```
![[Pasted image 20240321110120.png]]


### trick 起别名
```python
git log --oneline --graph --decorate --all  # 在命令行中显示分支结构
alias graph="git log --oneline --graph --decorate --all" # 直接使用graph就可以查看分支结构
```

### checkout 与 reset 区别
版本回退后，reset 让整个工作流程回退
![[Pasted image 20240321110120.png]]
![[Pasted image 20240321110129.png]]

checkout 切换分支，但所有工作流程还在，随时切换


# question
## 大于 100 M 的传输方法
