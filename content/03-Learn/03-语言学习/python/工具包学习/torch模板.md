
1. 导入包以及设置随机种子
2. 以类的方式定义超参数
3. 定义自己的模型
```python
class modelNet(nn.Module):
    def __init__(self,**kwarg):
        super(modelNet,self).__init__()
        # 模型超参数设置
        # 网络需要使用的结构单元如线性层、激活函数tanh、sigmoid、dropout等
    def forward(self,data):
        # 搭建网络，网络结构中的运算与连接
        return pred
```
4. 定义早停类(此步骤可以省略)
5. 定义自己的数据集Dataset,DataLoader
```python
class MyDataset(torch.utils.data.Dataset):  
    def __init__(self, x_train, y_train):  
        self.x_train = x_train  
        self.y_train = y_train  
  
    def __getitem__(self, index):  
        return self.x_train[index], self.y_train[index]  
  
    def __len__(self):  
        return len(self.x_train)
```

DataLoader
参考：[pytorch中collate_fn函数的使用&如何向collate_fn函数传参_collate_fn=collater-CSDN博客](https://blog.csdn.net/dong_liuqi/article/details/114521240)
```python
# 传入的参数是train_data分成的一小块batch数据 
# 其中 x,y = batch[0]
# 输出是 x:torch.size(batch_size,dim),y:torch.size(batch_size)
def collate_fn(batch):  
    # batch是一个dataset类，里面包含了一个batch_size的数据: [(text1,label1),(text2,label2),...,(textn,labeln)]  
    x = []  
    y = []  
    for text,label in batch:  
        vec = []  
        # 如果句子为空，则用0向量代替，否则将句子中的词向量化，然后取平均值  
        if not text.split():  
            vec = [0] * 100  
        else:  
            for word in text.split():  
                try:  
                    vec.append(model.wv[word])  # 词向量化  
                except:  
                    pass  # 词不在词典中,跳过  
            x.append(sum(vec) / len(vec))  # 句子向量化,取平均值  注：sum(vec)将每个词的词向量相加  
        y.append(label)  
    return torch.tensor(x), torch.tensor(y)

train_data = MyDataset(x_train, y_trian)  
dataload = DataLoader(train_data, batch_size=64, shuffle=True, collate_fn=collate_fn)
```
6. 实例化模型，设置loss，优化器等
7. 开始训练以及调整lr
8. 绘图
9. 预测