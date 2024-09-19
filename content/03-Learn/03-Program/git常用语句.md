#常用语句 

# 常用语句

- 添加 `gitignore`  文件
	- 打开终端程序，用 `cd` 命令导航到包含项目的根文件夹，并输入 `touch .gitignore` 以下命令，为你的目录创建一个 `.gitignore` 文件
- 删除本地项目目录的缓存 `git rm -r --cached .`

# 创建

```python
mkdir learn-git # 创建文件夹
cd learn-git # 调整路径
git init  # 创建仓库
ls # 查看当前路径文件
ls -a # 查看当前路径所有文件
ls -altr # ?
cd .. # 退出
\rm -rf .git # 表示删除git仓库
git init my-repo # 指定生成git仓库名称
git clone 网址 # 从github上克隆
```

# 添加与提交

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

# 本地与 github 关联

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

如果远程建立仓库，本地也有仓库, 运行以下代码关联

```python
# git remote add <shortname><url>
git remote add origin git@github.com:wujyuhin/CDM.git 

# 指定分支为main分支，若我们显示main可忽略
git branch -M main  

# 将本地main分支与远程origin仓库main分支关联
git push -u origin main  
# 全称 git push -u origin main:main

# 如果已经进行关联过了，remote origin already exists，则
git remote rm origin
git remote add origin ssh名称
git push origin master
```

但是可能会有以下报错 Error: failed to push some refsto‘远程仓库地址’，成功解决办法：

```python
git pull --rebase origin main #保持本地目录干净
git push -u origin main
```
