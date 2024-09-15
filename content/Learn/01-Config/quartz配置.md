#环境配置 

# 配置 quartz

## 步骤 0. 先决条件

* 在继续之前，您需要安装以下软件
	* NodeJS (v 20.16+)：https://nodejs.org/zh-cn/
	* Git：https://git-scm.com/
	* Obsidian：https://obsidian.md/

## 步骤 1：下载并安装 quartz

- 打开终端并运行以下命令
	- 输入 `cd 你的文件夹路径` 进入该文件夹
	- 输入 `git clone https://github.com/jackyzha0/quartz.git` 将 quartz 仓库克隆到本地
	- 输入 `cd: ...../quartz` 进入 quartz 文件夹
	- 输入 `npm config set registry https://registry.npmmirror.com` 添加国内镜像加速
	- 输入 `npm i`
		- 出现以下提示没关系，因为有些功能需要赞助，不用管
		- ![[Pasted image 20240914173404.png]]
	- 输入 `npx quartz create`创建新的 quartz 项目
[git对已经提交过的文件添加到.gitignore_git已经commit了怎么gitignore-CSDN博客](https://blog.csdn.net/hnjb5873/article/details/108774212)

## 步骤 2：设置 github 仓库

- 建立 github 仓库
	- ![[Pasted image 20240914220518.png]]
	- ![[Pasted image 20240914220647.png]]
	- ![[Pasted image 20240914220812.png]]

## 步骤 3 obsidian

- 新建新的笔记仓库 vaults
	- ![[Pasted image 20240914221101.png]]
	- ![[Pasted image 20240914221420.png]]



## 步骤 4 
![[Pasted image 20240914222445.png]]
![[Pasted image 20240822184529.png]]

# Quartz 使用技巧

## 修改页面的元素

![[Pasted image 20240823163040.png]]

![[Pasted image 20240823163102.png]] 标题则在此处修改

## 同步问题

### 目标

- 需要将某些笔记部署到 github page 上，完成 blog 更新

### 目前的更新方法

- 由于 blog 由 quartz 写
- quartz 的笔记内容使用 obsidian 管理，记为笔记仓库 1
- 但是我有笔记总仓库，我希望我只在总仓库中写笔记。
- 写完后如果将笔记上传到 blog，就只需要将笔记复制到仓库 2，图床也需要同步到仓库 2

步骤 1：笔记写在主仓库

步骤 2：将需要发表的笔记复制到仓库 2 (一直打开 airexplorer 即可, 随时手动同步)

步骤 3：图床需要同步（一直打开 airexplorer 即可，随时手动同步）

步骤 4：部署(一直打开 git ，路径为 `D:\Attachments\02-study\quartz\quartz`，输入 `npx quartz sync` 同步)

### 问题：修改后呢

如果想要修改笔记，只能手动再次复制笔记，如果这个笔记需要多次修改没问题

如果忘记了，那笔记一多就忘记哪些修改同步了，哪些修改没同步，出现管理问题

只有一个办法：记住每次修改都需要同步笔记、重新部署

## 如何加入 github 评论

直接看攻略网站 [Comments (jzhao.xyz)](https://quartz.jzhao.xyz/features/comments)

但是问题是我想取消怎么办，直接注释下面代码

![[Pasted image 20240825111352.png]]

## 如何加入近期笔记

加入以下代码即可，其中

- Title 是标题
- Limit 是显示最近 5 篇
- Showtags 是不显示笔记中的标签

![[Pasted image 20240825111552.png]]
