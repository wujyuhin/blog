#matplotlib #python
![[Pasted image 20240408145849.png]]

# Matpmatplotlib 概述
## 图标的常用设置
### 基本绘图主要函数
#### 主函数 plot
```python
matplotlib.pyplot.plot(x,y,format_string,**kwargs)
"""
参数说明
x：x轴数据
y：y轴数据
format_string：控制曲线格式的字符串（颜色、线条样式、标记样式）
**kwargs: 键值参数，相当于字典
- alpha=0.5 线条透明度
"""
```
#### 格式-颜色 color

```python
matplotlib.pyplot.plot(color='r') # color参数设置线条颜色
"""
b:蓝色
g:绿色
r:红色
c:蓝绿色
m:洋红色
y:黄色
k:黑色
w:白色
#FFFF00 黄色
0.5 灰度值字符串

"""
```
#### 格式-线条 linestyle
```python
matplotlib.pyplot.plot(linestyle='-.')
"""
实线'-'
双划线'--'
点划线'-.'
虚线':'
"""
```

#### 格式-标记 marker
```python
matplotlib.pyplot.plot(marker='>')
matplotlib.pyplot.plot(mfc='w') # markerfacecolor 散点实心颜色
matplotlib.pyplot.plot(mec='k') # markeredgecolor 散点外边颜色
matplotlib.pyplot.plot(mew='k') # markeredgewidth 折点线宽
matplotlib.pyplot.plot(ms='0.5') # markersize 散点大小

```
![[Pasted image 20240408151910.png]]


#### 演示代码 1
```python
# 折线图
import matplotlib.pyplot as plt
x = list(range(1,6,1))
y = [15,16,17,18,19]
plt.plot(x,y,linestyle='-.',marker='>')
y = [15,17,19,21,23]
plt.plot(x,y,color='r',linestyle=':',marker='1')
y = [15,18,21,24,27]
plt.plot(x,y,color='c',linestyle='--',marker='s')
plt.show()
```

![[Pasted image 20240408160708.png]]

#### 设置画布 figure
```python
matplotlib.pyplot.figure(num=None,figsize=None,dpi=None,facecolor=None,edgecolor=None,frameon=True)
"""
num:图像编号(数字)或名称(字符串)，通过该参数激活不同画布
figsize:指定画布宽高，单位英寸 输入元组(n,m)
dpi:指定绘图对象的分辨率，默认80.，分辨率越高画布越大
facecolor:背景颜色
edgecolor:边框颜色
frameon:是否显示边框，默认值为True
"""
```

#### 坐标轴
```python
坐标轴标题:plt.xlable('str')函数设置x轴标题、plt.ylabel('str')函数设置y轴标题
解决中文乱码问题:plt.rcParams['font.sans-serif']=['SimHei']
坐标轴范围:plt.xlim([a,b])设置x轴范围，plt.ylim([a,b])设置y轴范围
设置网格线:plt.grid(color='0.5',linestyle='--',linewidth='1',axis='x')
	axis='x'表示隐藏x轴网格线
设置坐标轴刻度:plt.xticks(range(1,6),['1月','2月','3月','4月','5月'])
```

#### 演示代码 2
```python
# 调整画布、设置标题、范围、网格线和中文乱码问题
import matplotlib.pyplot as plt
import random
plt.figure(figsize=(10,5),facecolor='c') # 画布
plt.rcParams['font.sans-serif']=['SimHei'] # 中文乱码问题
x = [i+random.random()*0.5 for i in range(1,11)]
y = [random.randint(1,10) for _ in range(10)]
plt.plot(x,y,color='b',linestyle='-.',marker='>')
plt.grid(color='0.5',linestyle='--',linewidth='0.7')            # 网格
plt.xlabel('超参数')  # x轴标题
plt.ylabel('修正率')  # y轴标题
plt.xlim([1,13])     # x轴范围
plt.ylim([0,12])     # y轴范围
# 设置刻度
month = [str(i)+'月' for i in range(1,11)]
plt.xticks(range(1,11),month)
plt.show()
```
![[Pasted image 20240408160613.png]]

注意：
- 范围设定 x 轴范围和 x 轴刻度是分开的
- x 轴刻度是和 x 数据是分开的

#### 添加文本标签 text
```python
matplotlib.pyplot.text(x,y,s,**kwargs)
"""
通用绘图参数
fontsize：字体大小
ha：水平对齐方式
va：垂直对齐方式
"""
```

#### 添加标题和图例
```python
matplotlib.pyplot.title()
matplotlib.pyplot.legend()
"""
通用绘图参数
fontsize：字体大小
ha：水平对齐方式
va：垂直对齐方式
"""
```

位置参数有
![[Pasted image 20240408161004.png]]





