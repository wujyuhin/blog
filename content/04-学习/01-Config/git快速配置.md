#环境配置 

# 快速攻略

1. 下载
	1）官网 [git-scm.Com](https://git-scm.Com)
	2）Download for Windows
	3）64-bit Git for Windows Setup	
2. 安装
	1）下载完后一路回车法即可
3. 配置
	1）桌面右键点击 open git bash here
	2）打开界面后配置用户名 `Git config --global user. Name wujyuhin`
	3）配置邮箱 `git config --global user. Email wujyuhin@haha.com`
4. 代码管理
	1. 从仓库 clone 到本地（链接为 github 项目的 code 底下的 https 链接）
		1. `git clone https://github.com/JiaoyangXu-hub/CSnotes.git`
	2. 本地代码管理
		1. 【初始化】 `git init`  //初始化创建. Git 文件夹 
		2. 【提交所有代码】
			1. `git add .`   // 把当前文件夹的所有文件设置为准备提交状态
			2. `git commit -m "功能 1 已完成"`  // 提交准备状态的所有文件，备注一定要写，版本管理的作用
		3. 【提交部分代码】
			1. `git add main. Py`  // 把 main. Py 设置为准备提交状态
			2. `git commit -m "功能 2 已完成"`   // 此时提交的文件是 main. Py
		4. 【恢复代码】
			1. `Git checkout HEAD test.py`  // 恢复之前保存的版本

# 添加 git ignore

# 常用语句

删除本地项目目录的缓存 `git rm -r -cached .`