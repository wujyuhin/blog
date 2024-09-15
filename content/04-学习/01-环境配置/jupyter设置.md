#jupyter
Jupyter 使用 (python 3.7)
1. 更改 python 环境
	1)在 cmd 中切换环境 conda activate 你的环境
	2)导入相关包 
		Pip install jupyter
		Pip install ipykernel
	3)在环境中安装 ipykernel
		Python -m ipykernel install --user --name 环境名 --display-name "jupyter 显示的环境名"
	4)查看 jupyter 的所有环境（这个不行）
		Jupyter kernelspec list
	5)输入 jupyter notebook, 在选项卡 kernel-Change kernel 中可以选择切换环境
	6）删除环境
		Jupyter kernelspec list  查看环境
		Jupyter kernelspec uninstall 环境名

2. 更改 jupyter 默认路径
	1）生成配置文件
		打开 Anaconda Prompt 输入 jupyter notebook --generate-config
	2）查找配置文件
		路径在 C:\Users\Administrator. Jupyter
	3）修改配置文件
		以 txt 文件打开文件，查找c.NotebookApp. Notebook_dir
		取消注释，并修改为c.NotebookApp. Notebook_dir=“自己的路径”

3. 设置多个 jupyter notebook 路径（不同项目需求）
	1)新建 txt 文件
	2)输入
		Start cmd /k "cd 自己想要的文件路径 && 路径的盘符 && jupyter notebook"
	3)改后缀为 bat
	4)例子
		想要以本地 attachments 文件夹内为根目录：
		Start cmd /k "cd F:\onedrive-wujyuhin\OneDrive - mails. Ccnu. Edu. Cn\Attachments && F: && jupyter notebook"



基本操作
1. 启动：在 cmd 输入 jupyter notebook
2. 模型切换
	Esc：command mode (命令模式)
	Enter: edit mode (编辑模式)
3. 代码运行
	Ctrl + enter ：运行后不增加块
	Shift + enter ： 运行后增加 cell
4. 帮助查询
	在函数后：shift + tab
5. 增删 cell
	Command 模式下创建：
		A：创建后在上方新增 cell
		B：创建后在下方新增 cell
	Command 模式下删除：两次 d 或者  x
6. 保存
	Command 模式下：s
7. 魔法函数
	%who ： 查看所有变量

8. Command 模式
	1，2，3，4 等对应标题大小
9. Commad 模式下
	M ： markdown 模式
	Y ： 代码格式