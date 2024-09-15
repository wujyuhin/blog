1. Embedding 层
	是对所有词指定长度向量 (10,3)，表示 10 个词都映射到 3 维向量
	Embedding = nn.Embedding (10,3)
	输入两句话分别为 123，243，维度是 2*3，embedding 后则得到 2*3*3 的两句话
	Embedding ([1,2,3],[2,4,3])  
```python
Loss.item() # 去除梯度提取数值
```

# Bug 1
## 输入的的 X 和 y 的要求
- X，y 均需要 tensor 格式！
- 并且如果与模型保持一致的设备，如同时cpu，或者同时 gpu
- y 标签需要进行 y.squeeze，将 (128,1)转成 (128,)才能避免一下报错，因为交叉熵需要这种格式
	- RuntimeError: 0D or 1D target tensor expected, multi-target not supported&& 神经网络中 label 出现的错误


```python
Creating a tensor from a list of numpy.ndarrays is extremely slow. Please consider converting the list to a single numpy.ndarray with numpy.array() before converting to a tensor
```