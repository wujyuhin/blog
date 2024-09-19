# 一、常用 GUI 库
常用 GUI 库为 Tkinter，适合小型 GUI 编写。当然以后会学习 wxPython，PyQT
# 二、Tkinter 入门

## 2.1学习资源
tkinter 官方文档 https://docs.python.org/3.7/library/tk.html\
## 2.2 核心步骤
### (1)创建应用程序主窗口对象
```python
from tkinter import *
root = Tk()
```
### (2)主窗口中，添加可视化组件
如按钮 Button，文本 Label 等
```python
btn1 = Button(root)
btn1['text'] = "点击我就送花"
```
### (3)通过几何布局管理大小位置
```python
btn1.pack()
```
### (4)事件处理
通过绑定事件处理程序，相应用户操作所触发的事件，单击、双击等
```python
# 此处的e是一个默认对象，记录了用户操作的信息
def songhua(e):
	messagebox.showinfo("Message","送你一朵玫瑰花，请你爱上我")
	print("送你99朵玫瑰花")

btn1.bind("<Button-1>",songhua)
```
## 2.3 主窗口设置
 ```python
 geometry('wxh±x±y')  # w为宽，h为高，+x表示距离屏幕左边距离，+y表示距离上边距离
 ```
## 2.4 GUI 编程整体描述
 ![[Pasted image 20240705170508.png]]
 上述都是继承结构，全都是对象。例如 Button 继承了 Widget 类
- Wm 做窗口之间的通信
	- 可以通过 root=Tk()创建一个窗口，而多个窗口之间的通信使用 Wm
- TopLevel 顶级窗口
	- 相当于手机中突然弹窗，需要处理弹窗后才能做其他操作
- Misc
- 布局管理器：Pack、Place、Grid, 其中组件都继承了这些管理器

![[Pasted image 20240705171014.png]]
## 2.5 常用组件使用
![[Pasted image 20240705171709.png]]
## 2.6 GUI 应用程序类经典写法
```python
from tkinter import Frame, Label, Entry, Button, StringVar, messagebox,Text, Tk  
  
class Application(Frame):  
    """一个经典的GUI程序的类的写法"""  
    def __init__(self, master=None):  
        super().__init__(master)  
        self.master = master  
        self.pack()  
        self.create_widgets()  
  
    def create_widgets(self):  
        self.bt1 = Button(self, text="打开目标与内容考察表文件", command=self.open_file1)  
        self.bt1.pack()  
        self.text1 = Text(self, width=50, height=5)  
        self.text1.pack()  
        self.bt2 = Button(self, text="打开学生成绩表文件", command=self.open_file2)  
        self.bt2.pack()  
        self.text2 = Text(self, width=50, height=5)  
        self.text2.pack()  
        self.bt3 = Button(self, text="计算并保存目标达成度", command=self.calculate_achieve)  
        self.bt3.pack()  
  
    def open_file1(self):  
        pass  
  
    def open_file2(self):  
        pass  
  
    def calculate_achieve(self):  
        pass  
  
if __name__ == "__main__":  
    root = Tk()  
    root.title("目标达成度计算器")  
    root.geometry("400x250+1000+500")  
    app = Application(master=root)  
    app.mainloop()
```
# 三、tkinter 简单组件
所有组件都是矩形，所以可以定义宽度和高度等，下面组件示例可以加到 2.6 经典写法中的 `create_widgets` 中
## label 组件
直接写法如下：
```python
	global photo  # 因为程序再不断循环，若非全局变量图片会一次性消失 
	photo = PhotoImage(file='data/logo.gif')
	label1 = Label(text='',width=8,height=4,
					font=('楷体',15,'bold'),
					image=photo,
					fg='gray',bg='lightblue',
					justify='left',
					borderwidth=5,
					relief='solid')
```
在类中写法如下：
```python
class ...
	...
	def create_widgets(self):
		global photo
		photo = PhotoImage(file='data/logo.gif') 
		self.label1 = Label(text='',width=8,height=4,
							font=('楷体',15,'bold'),
							image=photo,
							fg='gray',bg='lightblue',
							justify='left',
							borderwidth=5,
							relief='solid')
		self.label1.pack()
	...
```

- width、height 为宽度和高度 (注：汉字占 2 个宽度，1 个高度)
- Font 是字体格式
- Image 是 label 上的图像  (注：加图像需要` global`！)
- fg、bg 是 foreground、前景色，background、背景色
- justify 是文字对齐方式，可选 `left` 、`center` 和`right`
- borderwdth 是边界线的粗细
- relief 是边界线的呈现模式
## Button 组件及其 options 选项
在类中的写法如下：
```python
class Application(Frame):
	...
	def create_widgets(self):
		self.bt1 = Button(text='打开文件',fg='red',bg='blue')
		self.bt1.pack()
```
已知可以通过 option 设置组件 Label 的属性，还有哪些方法可以修改设置？
- 1. 创建对象时，使用命名参数 `fred = Button(self,fg='red',bg='blue')`
- 2. 创建对象后，使用字典索引 `fred['fg'] = 'red'`
- 3. 创建对象后，使用 fonfig () `fred.config(fg='red',bg='blue')`
Button 中的文字位置
- `anchor=` 可为 N, NE, E, SE, S, SW, W, NW, center

## Enter
```python
class Application(Frame):
	...
	def create_widgets(self):
		# StringVar变量绑定到entry组件
		# 此时，stringvar变化，组件内容也变化
		# 组件内容变化，stringvar也变化
		v1 = StringVar()
		self.entry1 = Entry(self,textvariable=v1)
		self.entry1.pack()
```


# N、GUI 打包成 exe
## 1. Tkinter
### 1.1打包成 exe 前的准备
导入需要的库，注意**第一个坑**，tkinter 的子模块需要显式导入，例如正确如下
```python
import tkinter.messagebox
# 或者
from tkinter import messagebox
```
错误如下
```python
import tkinter
```
### 1.2 完整样例
```python
from tkinter import Frame, Label, Entry, Button, StringVar, messagebox, Text, Tk  
  
  
class Application(Frame):  
    """一个经典的GUI程序的类的写法"""  
  
    def __init__(self, master=None):  
        super().__init__(master)  
        self.master = master  
        self.pack()  
        self.create_widgets()  
  
    def create_widgets(self):  
        Label(self, text="\n学科目标达成度计算器", font=("楷体", 20)).grid(row=0, column=0)  
        Label(self, text="", font=("楷体", 5)).grid(row=1, column=0)  
        # 创建一个灰色的frame  
        container_frame = Frame(self.master, bg="lightgray", padx=30, pady=35)  
        container_frame.pack(padx=20, pady=20)  # 为容器Frame设置外边距  
        # 打开文件按钮  
        Button(container_frame, text="打开目标与内容考察表文件", font=("楷体", 15),  
               width=30, height=1, command=self.open_file1).grid(row=2, column=0)  
        Label(container_frame, text="", bg="lightgray", font=("楷体", 5)).grid(row=3, column=0)  
        # 文本框  
        self.text1 = Text(container_frame, width=45, height=3)  
        self.text1.grid(row=4, column=0)  
        Label(container_frame, text="", bg="lightgray", font=("楷体", 5)).grid(row=5, column=0)  
        # 打开文件按钮  
        Button(container_frame, text="打开学生成绩表文件", font=("楷体", 15),  
               width=30, height=1, command=self.open_file2).grid(row=6, column=0)  
        Label(container_frame, text="", bg="lightgray", font=("楷体", 5)).grid(row=7, column=0)  
        # 文本框  
        self.text2 = Text(container_frame, width=45, height=3)  
        self.text2.grid(row=8, column=0)  
        # Label(container_frame, text="",bg="gray", font=("楷体", 5)).grid(row=9, column=0)  
        container_frame2 = Frame(self.master, bg="lightgray", padx=30, pady=35)  
        container_frame2.pack(padx=20, pady=20)  # 为容器Frame设置外边距  
        # 计算按钮  
        Button(container_frame2, text="计算并各目标平均达成度", font=("楷体", 15),  
               width=30, height=1, command=self.calculate_achieve).grid(row=10, column=0)  
        # 显示结果按钮  
        Label(container_frame2, text="", bg="lightgray", font=("楷体", 5)).grid(row=11, column=0)  
        Label(container_frame2, text="计算结果:", bg='lightgray', font=("楷体", 15, 'bold'), justify='left').grid(  
            row=12,  
            column=0,  
            sticky='W')  
        self.label_result = Label(container_frame2, bg="lightgray", font=("楷体", 15))  
        self.label_result.grid(row=13, column=0)  
        # 退出按钮  
        container_frame3 = Frame(root, bg="white", padx=0, pady=0)  
        container_frame3.pack(padx=0, pady=0)  # 为容器Frame设置外边距  
        bt = (Button(container_frame3, text="关闭窗口", font=("楷体", 15), command=self.close_window))  
        bt.grid(row=14, column=0)
  
    def open_file1(self):  
        pass  
  
    def open_file2(self):  
        pass  
  
    def calculate_achieve(self):  
        pass  

	def close_window(self):  
	    self.master.quit()
  
  
if __name__ == "__main__":  
    root = Tk()  
    root.title("目标达成度计算器")  
    root.geometry("600x300+300+100")  
    app = Application(master=root)  
    app.mainloop()
```
比较简陋
![[Pasted image 20240708212154.png]]

## 2. 虚拟环境与 pyinstaller 打包
### 2.1 为何需要虚拟环境？有哪些虚拟环境？
**为什么**
- 因为平常使用的环境有太多无关的工具包和配置，打包的时候会变得很大！因此需要一个纯净的环境，仅包含程序使用到的工具包。作用在于减少打包时长、优化 exe 文件体积、加快 exe 运行速度
**有哪些**
- **virtualenv** 最流行的
- **venv** 操作与前者类似
- **pipenv** 本文采用该方案，能管理多个环境和第三方包。优点有
	- 集成 pip、virtualenv 并优化
	- virtualenv 管理 requirements.txt 会出问题，pipenv 查看包的依赖关系方便？
- **anaconda** 该方法会有大量自动下载的冗余包
- 前三种方法更多了解参考 https://blog.csdn.net/weixin_40922744/article/details/103721870

### 2.2 pipenv 使用
**pipenv 基本命令**
```python
pipenv install #创建虚拟环境
pipenv shell  #进入虚拟环境，若不存在则创建并进入
pipenv install flask  # 安装
pipenv uninstall flask
pipenv graph  # 查看模块之间的依赖关系
pip list  # 查看所有包
exit()  # 退出
pip freeze > requirments.txt
pip install -r requirements.txt
```

**正式操作**
**1. 安装**
进入 cmd 输入
```python
pip install pipenv
```
**2. 创建并进入虚拟环境**
```python
pipenv install
pipenv shell
```
问题如何管理多个虚拟环境，在 cmd 中想进入哪个就进入哪个？
**3. 在虚拟环境中安装所需的包**
```python
# 第2坑:如果下载速度很慢，pip install pandas -i https://pypi.douban.com/simple
pip install pandas  
pip install pyinstaller
pip install xlrd  # 第3坑:最好安装xlrd包到最新版本，否则可能无法处理xlsx格式
pip install ...
```
**4. 使用 pyinstall 打包 exe**
```python
pyinstaller -F -w D:\Attachments\model.py --distpath=D:\Attachments\ -i \Attachments\icon.ico
pyinstaller -F -w -i favicon.ico --name=达成度.exe tkinterModel.py
```
其中
`-F` 是打包成独立的 exe 文件
`-w`  是去掉黑色的控制台（**第 4 坑**：建议输出一个控制台的 exe，在调试完各种 bug 之后再使用 `-w` 去掉控制台）
`D:\Attachments\model.py` 是需要打包的 py 文件路径
`D:\Attachments\` 是需要保存 exe 的目标路径
`D:\Attachments\icon.ico` 是 exe 图标的 ico 文件路径
### 2.3 打包效果
使用 anaconda 虚拟环境打包有 60 M 大小，使用 pipenv 打包大小仅有 6 M

### 2 .4 与 pycharm 的交互
打开 pycharm 这个中的 file->setting
![[Pasted image 20240708210406.png]]
由于在 cmd 中已经使用 pipenv 创建了虚拟环境，因此能在此处找到选择即可
![[Pasted image 20240708210413.png]]