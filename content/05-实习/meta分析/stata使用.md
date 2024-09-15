
# 数据导入
准备好处理清理完后的 excel 或 csv 数据
![[Pasted image 20240419214024.png]]
点击数据载入框
![[Pasted image 20240402193430.png]]

![[Pasted image 20240421083252.png]]

![[Pasted image 20240421083240.png]]

可以从 excel 直接复制数据到 stata 中，如下
![[Pasted image 20240402210225.png]]

# 输入代码进行诊断性 meta 分析
## 导入分析包

![[Pasted image 20240421083818.png]]
```python
ssc install midas
ssc install mylabels
```

## 汇总总的敏感性特异性等
```python
midas tp fp fn tn, res(all)
```
得出的结果可用
ROC Area, AUROC = 0.91 [0.88 - 0.93]
Parameter                   Estimate          95% CI
Sensitivity                     0.84 [    0.78,    0.88]
Specificity                     0.86 [    0.80,    0.90]
Positive Likelihood Ratio        5.9 [     4.0,     8.7]
Negative Likelihood Ratio       0.19 [    0.13,    0.27]
Diagnostic Odds Ratio             31 [      16,      59]
这是数据总体上的特征
## 森林图（分别计算敏感性特异性的异质性）

![[Pasted image 20240421084716.png]]
![[Pasted image 20240422155202.png]]
```python 
midas tp fp fn tn, id (author year) bforest (dss) text (0.4) ford fors
```
![[Pasted image 20240421145027.png]]
命令中的 ms(0.75)是设定森林图中黑点大小的，可以自己换做其他数值。
text(0.4)是设定字体大小
从森林图中可以看出，
灵敏度的 Q 检验 P<0.01，说明纳入研究间的异质性有统计学意义
I2统计量为79.76%，说明异质性占比较大（I2超过50%即认为异质性较为明显）。
同样特异度的 Q 检验 P=0.01，说明纳入研究间的异质性有统计学意义，
而 I2统计量为 84.96%，说明有轻度的异质性。

（注：Q检验用来从统计学角度说明异质性是否存在，而I2统计量用来衡量异质性的大小，一般Q检验的P值越小，I2统计量越大。）除了运用统计学方法对异质性进行描述外，作者还可以直接通过森林图各数值的排列整齐情况进行定性的判断，该方法相对主观，可以与统计学方法相结合。
## 绘制 sroc 曲线
```python
midas tp fp fn tn, plot sroc(both)
```
![[Pasted image 20240402212059.png]]
SROC 曲线如果从理论将其还挺繁琐的，就是理解为综合 ROC 曲线
在一般的预测模型下，会有一个阈值，大于 0.5 就..

## 检验异质性
```python
midas tp fp fn tn, galb(tpr)
```
![[Pasted image 20240419215425.png]]

标准化效应测量，计算穿过原点的回归线，和 95%的边界
偏离群体太远的点都是异质性很高的点，可以使用留一计算异质性
留一计算的意思是，把一篇剔除，然后重新做 meta 分析计算异质性，如果降幅较大，则说明删除的那一篇产生很高的异质性，需要查看这篇文章的特征
而途中的偏离的点对应的文献都是产生了较大的异质性。
## 漏斗图
```python
midas tp fp fn tn, pubbias
```

![[Pasted image 20240402211156.png]]
无统计学差异，表明不存在发表偏倚，也基本分布在两侧

如果漏斗图比较平衡，说明

![[Pasted image 20240419220537.png]]
