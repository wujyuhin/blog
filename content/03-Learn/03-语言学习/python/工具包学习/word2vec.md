```python
import gensim.models import Word2Vec
gensim.models.word2vec.Word2Vec(sentences=None, corpus_file=None, size=100, alpha=0.025, window=5, min_count=5,
              max_vocab_size=None, sample=0.001, seed=1, workers=3, min_alpha=0.0001, sg=0, hs=0, negative=5,
              ns_exponent=0.75, cbow_mean=1, hashfxn=<built-in function hash>, iter=5, null_word=0, trim_rule=None, 
              sorted_vocab=1, batch_words=10000, compute_loss=False, callbacks=(), max_final_vocab=None)

'''def __init__(  
        self, sentences=None, corpus_file=None, vector_size=100, alpha=0.025, window=5, min_count=5,  
        max_vocab_size=None, sample=1e-3, seed=1, workers=3, min_alpha=0.0001,  
        sg=0, hs=0, negative=5, ns_exponent=0.75, cbow_mean=1, hashfxn=hash, epochs=5, null_word=0,  
        trim_rule=None, sorted_vocab=1, batch_words=MAX_WORDS_IN_BATCH, compute_loss=False, callbacks=(),  
        comment=None, max_final_vocab=None, shrink_windows=True,  
    ):'''

```

Sentences (iterable of iterables, optional)：供训练的句子，可以使用简单的列表。
- [['你','我','他'],[...],[...]...]
Corpus_file (str, optional)：LineSentence 格式的语料库文件路径。
- 未用
Size (int, optional)：word 向量的维度。
Window (int, optional)： 一个句子中当前单词和被预测单词的最大距离。
Min_count (int, optional) ： 忽略词频小于此值的单词。
Workers (int, optional)： 训练模型时使用的线程数。
Sg ({0, 1}, optional)： 模型的训练算法: 1: skip-gram; 0: CBOW.
Hs ({0, 1}, optional)： 1: 采用 hierarchical softmax 训练模型; 0: 使用负采样。
Negative (int, optional)： 0: 使用负采样，设置多个负采样 (通常在 5-20 之间)。
Ns_exponent (float, optional)： 负采样分布指数。1.0 样本值与频率成正比，0.0 样本所有单词均等，负值更多地采样低频词。
Cbow_mean ({0, 1}, optional)： 0: 使用上下文单词向量的总和; 1: 使用均值，适用于使用 CBOW。
Alpha (float, optional)： 初始学习率。
Min_alpha (float, optional)： 随着训练的进行，学习率线性下降到 min_alpha。
Seed (int, optional)： 随机数发生器种子。
Max_vocab_size (int, optional)： 词汇构建期间 RAM 的限制; 如果有更多的独特单词，则修剪不常见的单词。每 1000 万个类型的字需要大约 1 GB 的 RAM。
Max_final_vocab (int, optional)： 自动选择匹配的 min_count 将词汇限制为目标词汇大小。
Sample (float, optional)：高频词随机下采样的配置阈值，范围是 (0,1 e-5)。
Hashfxn (function, optional)： 哈希函数用于随机初始化权重，以提高训练的可重复性。
Iter (int, optional)： 迭代次数。
Trim_rule (function, optional)： 词汇修剪规则，指定某些词语是否应保留在词汇表中，修剪掉或使用默认值处理。
Sorted_vocab ({0, 1}, optional)：如果为 1，则在分配单词索引前按降序对词汇表进行排序。
Batch_words (int, optional)： 每一个 batch 传递给线程单词的数量。
Compute_loss (bool, optional)：如果为 True，则计算并存储可使用 get_latest_training_loss ()检索的损失值。
Callbacks (iterable of CallbackAny 2 Vec, optional)： 在训练中特定阶段执行回调序列。
————————————————
