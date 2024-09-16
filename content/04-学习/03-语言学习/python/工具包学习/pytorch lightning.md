
# 一、首先学习了基本框架
## 简单 mnist 数据图片识别
不写类的情况下，直接写框架使用 nn. Sequential ()
```python
import torch
import torch.nn as nn
import torch.optim as optim
from torchvision import datasets,transforms
from torch.utils.data import DataLoader,random_split

# dataset
train_data = dataset.MNIST('data',train=True,download=True,transform=transforms.ToTensor())
train,val = random_split(train_data,[50000,10000])
train_loader = DataLoader(train)
val_loader = DataLoader(val)

# model
model = nn.Sequential(
	nn.Linear(28*28,64),
	nn.ReLU(),
	nn.Linear(64,64),
	nn.ReLU(),
	nn.Linear(64,10))

# optimizer and loss
params = model.parameters()
optimizer = optim.SGD(params,lr=0.01)
loss = nn.CrossEntropyLoss()

# train and val
nb_epochs = 5
for epoch in range(nb_epochs):
	losses = list()
	for batch in train_loader:
		x,y = batch # x:[batchsize,1,28,28]
		b = x.size(0)
		x = x.view(b,-1) # x:[batchsize,784]
		# 1.forward
		l = model(x)
		# 2.cumpute the objective function
		J = loss(l,y)
		# 3.clean grad
		model.zero_grad() # params=0
		# 4.cumpute the grad with respect to params
		J.backward() # params.grad._sum(dJ/params)
		# 5.step in the opposite direction of gradient
		optimizer.step() # params = params - eta * params.grad
		losses.append(J.item())
	print(f"Epoch:{epoch+1},train loss:{torch.tensor(losses).mean():.2f}",end=',')
	losses = list()
	for batch in val_loader:
		x, y = batch  # x:[batchsize,1,28,28]  
		b = x.size(0)  
		x = x.view(b, -1)  # x:[batchsize,784]
		# 1.forward
		with torch.no_grad():
			l = model(x)
		# 2.cumpute the objective function
		J = loss(l,y)
		losses.append(J.item())
	print(f"Epoch:{epoch+1},val loss:{torch.tensor(losses).mean():.2f}")
```

## ResNet 框架
相比上面只需要更改模型部分，使用类 class 变得而更灵活
特别的不加残差连接操作，则以下模型与上述模型差不多
```python
import torch  
import torch.nn as nn  
import torch.optim as optim  
# download dataset  
from torchvision import datasets, transforms  
from torch.utils.data import DataLoader,random_split  
  
train_data = datasets.MNIST('data', train=True, download=True, transform=transforms.ToTensor())  
train,val = random_split(train_data, [50000, 10000])  
train_loader = DataLoader(train, batch_size=32)  
val_loader = DataLoader(val, batch_size=32)  
  
# define a more flexible model  
class ResNet(nn.Module):  
    def __init__(self):  
        super().__init__()  
        self.l1 = nn.Linear(28*28,64)  
        self.l2 = nn.Linear(64,64)  
        self.l3 = nn.Linear(64,10)  
        self.do = nn.Dropout(0.1)  
  
    def forward(self,x):  
        h1 = nn.functional.relu(self.l1(x))  
        h2 = nn.functional.relu(self.l2(h1))  
        do = self.do(h1+h2)  
        logits = self.l3(do)  
        return logits  
model = ResNet().cuda()  
  
  
  
# define the optimizer  
params = model.parameters()  
optimizer = optim.SGD(params, lr=1e-2)  
  
# define the loss function  
loss = nn.CrossEntropyLoss()  
  
# My training loops  
nb_epochs = 5 # number of epochs  
for epoch in range(nb_epochs):  
    losses = list()  
    for batch in train_loader:  
        x,y = batch  
  
        # x: [batch_size, 1, 28, 28]  
        b = x.size(0)  
        x = x.view(b, -1).cuda()  
  
        # 1 forward  
        l = model(x) # l: logit [batch_size, 10]  
  
        # 2 compute the objective function        J = loss(l, y.cuda())  
  
        # 3 cleaning the gradient  
        model.zero_grad() # params.grad = 0  
        # or optimizer.zero_grad()  # params.grad = 0  
        # 4 accumulate the partial derivatives of J with respect to params        J.backward() # params.grad._sum(dJ/dparams) 累加损失的导数  
  
        # 5 step in the opposite direction of the gradient 翻译 逆向梯度步进  
        optimizer.step()  # with torch.no_grad(): params = params - eta * params.grad  
  
        losses.append(J.item())  
  
    print(f'Epoch:{epoch+1},train loss:{torch.tensor(losses).mean():.2f}',end=',')  
  
  
    # validation 注意这里不需要计算梯度  
    losses = list()  
    accuracies = list()  
    for batch in train_loader:  
        x,y = batch # x: [batch_size, 1, 28, 28]  
        b = x.size(0)  
        x = x.view(b, -1).cuda()  
  
        # 1 forward  
        with torch.no_grad():  
            l = model(x) # l: logit [batch_size, 10]  
  
        # 2 compute the objective function        J = loss(l, y.cuda())  
  
        losses.append(J.item())  
        accuracies.append(y.eq(l.detach().argmax(dim=1).cpu()).float().mean())  
    print(f'Epoch:{epoch+1},val loss:{torch.tensor(losses).mean():.2f}',end=',')  
    print(f'validation accuracy:{torch.tensor(accuracies).mean():.2f}')
```

# 二、模型需要的调整
## 避免 overfitting with dropout
方法 1：模型拟合前的模型
方法 2：dropout
 interactive Neural Netword Debugging 如何调试网络防止过拟合
## 选择最佳 batch
# 三、使用 lightning
## 模块总结
1. Model
2. Optimizer
3. Data
4. Training loop
5. Validation loop
## 工具包安装
### 1 注意问题
pip 安装时注意版本问题, ，不可用以下代码!!！因为会删除已经下载的包
```cmd
pip install pytorch_lightning 错
pip install pytorch_lightning==2.2
```
![[Pasted image 20240410212055.png]]
### 2 查看版本对应
官方文档查看版本对应问题 https://lightning.ai/docs/pytorch/latest/versioning.html#pytorch-support
![[Pasted image 20240410212625.png]]
```
pip install pytorch_lightning=2.2
```


### 3.Lightning model
```python
 class MyModule(pytorch_lightning.LightningModule): 
    def __init__(self, ): 
        super().__init__() 
        self.model = Model() 
        #... 
    def forward(self, inputs): 
        return self.model(inputs) 
    def configure_optimizers(self): # -> optimizer 
        pass 
    def training_step(self, batch, batch_idx): # -> train loss 
        pass 
```

# 四、其他问题
### 验证集多行进度条问题解决
```python
class LitProgressBar(TQDMProgressBar):  
    """ 自定义进度条 : 使得验证集的进度条不显示"""  
    def init_validation_tqdm(self):  
        bar = super().init_validation_tqdm()  
        if not sys.stdout.isatty():  
            bar.disable = True  
model = Net()
trainer = pl.Trainer(max_epochs=100,callbacks=[LitProgressBar()])
trainer.fit(model,train_loader,val_loader)
```

