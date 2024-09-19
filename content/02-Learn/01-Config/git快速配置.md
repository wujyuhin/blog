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
			2. `git commit -m "功能 2 已完成"`   // 此时提交的文件是 `main.py`
		4. 【恢复代码】
			1. `Git checkout HEAD test.py`  // 恢复之前保存的版本

# 常出的 bug

**问题 1：无法 clone 项目**

```
报错一下错误：
fatal: unable to access 'https://github.com/xxx/autowrite.git/': 
OpenSSL SSL_read: Connection was reset, errno 10054
或者
fatal: unable to access 'https://github.com/xxx/autowrite.git/':
Failed to connect to github. Com port 443: Timed out
```

- 方法一：取消 git代理，然后进行克隆
	- `git config --global --unset http. Proxy  //取消 http 代理`
	- `git config --global --unset https. Proxy  //取消 https 代理 `
- 方法二：设置相同端口的代理，然后进行克隆
	- 科学上网>查看本地代理端口>打开本机端口为 7890
	- `git config --global http. Proxy http://127.0.0.1:7890`