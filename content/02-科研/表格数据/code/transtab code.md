测试了简单模型发现没问题
但是测试其他文件发现有问题
![[Pasted image 20240308215201.png]]
问题应该是在数据端上：
![[Pasted image 20240308215229.png]]
![[Pasted image 20240308215222.png]]
少了 credit-approval 参数就出现下面这个 bug
free variable 'bin_cols' referenced before assignment in enclosing scope

# 模型部分
将表格数据 dataframe 转成 input
```python
# TransTabClassifier的前馈
inputs = self.input_encoder.feature_extractor(x)
# 其中input_encoder是
self.input_encoder = TransTabInputEncoder(  
    feature_extractor=feature_extractor,  
    feature_processor=feature_processor,  
    device=device,  
    )
# 其中feature_extractor是
if feature_extractor is None:  
    feature_extractor = TransTabFeatureExtractor(  
        categorical_columns=self.categorical_columns,  
        numerical_columns=self.numerical_columns,  
        binary_columns=self.binary_columns,  
        **kwargs,  
    )
# 其中feature_processor
feature_processor = TransTabFeatureProcessor(  
    vocab_size=feature_extractor.vocab_size,  
    pad_token_id=feature_extractor.pad_token_id,  
    hidden_dim=hidden_dim,  
    hidden_dropout_prob=hidden_dropout_prob,  
    device=device,  
    )
```



```python
----------------------   transtab  ---------------------------------------
def build_classifier()->TransTabClassifier:
	model = TransTabClassifier() #来自modeling_transtab的TransTabClassifier()
	if checkpoint is not None:    # 	如果有训练好的模型就直接load，没有就
	    model.load(checkpoint)
	return model
	

def build_extractor()
	feature_extractor = TransTabFeatureExtractor # 来自modeling_transtab
	有训练好的就load训练好的
	return feature_extractor

def build_encoder()————构建输入表格映射到embedding的encoder
	如果没设定层数就直接建立TransTabFeatureExtractor、TransTabFeatureProcessor，组成TransTabInputEncoder
	如果有设定encoder的层数，则使用TransTabModel建立即可，里面是多层的结构逻辑

def train(model,trainset,valset,*args,**kwargs)


def build_contrastive_learner()
	建立一个基于transtab的对比学习器进行预训练

def train() - 来自trainer
	所有基于transtabmodel的模型共享训练函数 
	
------------------- modeling_transtab   -------------------------------
class TransTabWordEmbedding(nn.Module) 输入词id输出嵌入
class TransTabNumEmbedding(nn.Module) 输入num输出embedding
class TransTabFeatureExtractor(nn.Module)  特征提取器
	def __init__(): 导入本地的bert-base-uncased文件
	def __call__():
class TransTabFeatureProcessor(nn.Module)————返回all_feat_embedding,attention_mask
class TransTabTransformerLayer(nn.Module)————多头注意力机制层
class TransTabInputEncoder(nn.Module)
	将输入表格映射到embedding
	初始化要输入feature_extractor,  feature_processor,
	def load
class TransTabEncoder(nn.Module)————使用TransTabInputEncoder形成完成的encoding层
class TransTabLinearClassifier(nn.Module)————未知
class TransTabProjectionHead(nn.Module)————未知
class TransTabCLSToken(nn.Module)
	在每一个序列中增加一个可学习cls嵌入
class TransTabModel(nn.Module):  
	是基础模型，其他模型基于该模型重写forward实现，用于下游任务的基本transtab模型
	def __init__()
		feature_extractor = TransTabFeatureExtractor
		feature_processor = TransTabFeatureProcessor
		self.input_encoder = TransTabInputEncoder
		self.encoder = TransTabEncoder
		self.cls_token = TransTabCLSToken(hidden_dim=hidden_dim)
class TransTabClassifier(TransTabModel)————分类器学习模型-继承transtab
class TransTabForCL(TransTabModel)—————————对比学习模型-继承transtab

--------------------  trianer  ----------------------------------------
class Trainer():
	def train
	def evaluate
	def save_model
	def create_optimizer
	def create_scheduler
	......


```


代码结构



为什么会 eraly stop
![[Pasted image 20240315105123.png]]

![[Pasted image 20240315105139.png]]

![[Pasted image 20240315105211.png]]

