# 利用训练好的 word 2 vec 模型完成下游任务 (lstm_classifier.py)
主要是利用了 ELMO 框架训练下游任务，词嵌入还是使用 word 2 vec
## 一、思路
- 1. 导入训练 word 2 vec 前输入的文本数据
- 2. 将文本数据根据 word 2 vec 网络转成向量
- 3. 划分训练集、测试集、验证集
- 4. 建立 dataset、创建 dataloader
- 5. 编写下游任务分类器 ELMO.py
- 6. 训练模型
## 二、dataset
```python
class HotelDataset(Dataset):  
    def __init__(self, x_train, y_train):  
        self.x_train = x_train  
        self.y_train = y_train  
  
    def __getitem__(self, index):  
        return self.x_train[index], self.y_train[index]  
  
    def __len__(self):  
        return len(self.x_train)
```
## 三、collate
```
```