---
tags:
  - "#文献笔记"
parent: "A Survey of Models for Cognitive Diagnosis: New Developments and Future Directions"
collections:
  - 认知诊断
---
认知诊断模型研究综述：新进展与未来方向

# 1.Introduction

> [!info]
> 为什么需要认知诊断，引入认知诊断，给出认知诊断的本质

## Definition

**Cognitive diagnosis (CD)** ：Psychology was suggested to be combined with psychometrics in order to model the micro knowledge structure and cognitive processing of persons during the assessments so that the diagnostic results can be more instructional.  
将心理学与心理测量学相结合，对评估过程中人的微观知识结构和认知加工过程进行建模，使诊断结果更具有指导性。术语认知诊断模型 (CDM)
![](Pasted%20image%2020241210173707.png)
* left: 
	* same student, different score:  
* right: complete CD procedure
	* test construction: Q
	* response data collection: R
	* cognitive diagnosis model: IRT, DINA, NCDM...
	* psychological factor estimation:  model base on R
	* diagnosis feedback: different, depend on CDMs , eg:
		* over all ability(3.1)
		* mastered certain attributes(3.2)
		* proficiency of certain attributes (4.2)

## CDM

**CDM essence**：infer the unobservable ability levels from observable

$$
Rr(response) = f(\theta,\beta,\Omega)
$$

![[Pasted image 20241210174212.png#pic_center]] 
- Base on psychometrics
	- Item response theory (IRT)
		- Measure macro ability of individuals
	- AHM, DINA, NIDA
		- The proposal and usage Q-matrix was a  significant milestone
- Base on machine learning
	- Filtering, matrix factorization, Neural network-based (协同过滤、矩阵分解、神经网络)
	- Deep learning-based: Neural CD (In order to better fitting ability of sophisticated cognitive process and promising interpretability.)（想要更好的拟合认知过程和可解释性，需要结合心理测量学的理论和假设）
![[Pasted image 20241211104950.png#pic_center]]

# 2. Overview CDM

## 2.1 CDM mathematization

- **Suppose Data**
	- Examinees $S=\{s_1,...,s_I\}$
	- Items $E=\{e_1,...,e_J\}$
	- Responeses $R=\{(s_i,e_j,r_{ij}),s_i\in S,e_j\in E,r_{ij}\in\{0,1\}\}$
		- $i=1,...,I,j=1,...,J$
	- Q-matrix $Q=\{q_{ij}^{J\times K}\},q_{jk}=1(or$ $0)$
	- Extra multifaceted information: $X$
- **Problem Definition**
	- Input: $R,Q,X$
	- Output (Goal of Cognitive diagnosis): examinees' ability levels $\theta_i(i=1,...,I)$ 
- **Basic assumptions**
	- Assumption 1 constant ability
		- Cognitive status remains unchanged during the process of answering the test items
		- 假设一个人的能力水平在短时间内不发生变化 (例如, 在标准测试期间) 是合理的，在此期间可以根据对测试项目的反应来测量该人的能力水平。认知诊断与知识追踪的重要区别在于，后者近年来也引起了广泛关注。知识追踪侧重于对在线学习者知识状态 (要么可解释, 要么不可解释) 的变化模式进行建模，高度依赖隐马尔可夫链和循环神经网络等时序建模方法。在知识追踪模型中，认知过程通常被忽视，而预测学习者的未来表现是最常用的任务。相比之下，认知诊断旨在测量学习者在一定时间内的能力水平。它挖掘学习者的反应数据，对回答项目的认知过程进行建模，并在一定的度量空间内提供学习者的能力水平值。
	- Assumption 2 constant item charateristics
		- The characteristics of a test item remain constant over all of the testing situations where it is used
		- 题目的一些统计量如正确率会受到考生的影响。然而，试题的难度、区分度、相关知识概念等特征反映了试题的本质特征，不应改变。这种稳定性有助于所有考生对测验项目的公平性，并表明测验项目可以用反映这些特征的固定参数值来表示。
	- Assumption 3 monotonicity
		- The probability of a correct response to the test item increases, or at least does not decrease, as the locations of examinees increase on any of the coordinate dimensions
		- $\theta \uparrow \Longrightarrow P(r=1)\uparrow$
		- 任意一个维度上的能力提升，在作答正确的可能性应该增加，或者至少不降。
		- 大多数认知诊断模型采用单调性假设对认知过程进行建模，尤其是基于 IRT 和 MIRT 的模型。该假设表明，更好的表现应该来自于更高的能力水平，这与通常的直觉或经验是一致的。

## 2.2 A Brief Review of Cognitive Diagnosis Model Development

![[Pasted image 20241211154402.png]]

Without cognitive diagnosis, the most widely adopted method to evaluate a learner’s ability is through their scores obtained in tests. Eg. Classical Test Theory (CTT)
在没有认知诊断的情况下，最广泛使用的评估学习者能力的方法是通过他们在测试中获得的分数
消除分数中存在的错误而提出，但分数是受到问题属性和其他心理特征等因素影响观察到的能力，这是隐藏的，因此通过几十年的发展，从数据特征和模型结构总结：

- **The development of model structures**  模型结构
	- Psychometrics-based models
		- IRT, MIRT: unidimensional or multidimensional latent vectors to represent examinees'overall ability levels (一维或者多维潜在向量表示学生的整体水平)
		- RSM, DINA, GDM, G-DINA(proposal of Q)（随着测量细粒度能力的需求，对知识概念的掌握，逐渐提出了认知水平范式）
	- Machine learning-based models
		- Clustering algorithms 聚类算法
		- Support vector machine 支持向量机
		- Matrix factorization 矩阵分解
		- Fuzzy set 模糊集
		- Artificial neural networks 人工神经网络
		- Deep-learning based NCDM （随之跟进大量的数据驱动的深度学习方法）
		- Encoder-decoder-like CDM （重点研究诊断，是从框架上突破了以 NCDM 为基础的众多模型的题目和学生 id embedding问题）
- **The changes of exploited data**
	- Only numerical data: correct, incorrect, scores
		- IRT, MIRT
	- Q matrix or hierarchical structures 层次结构
		- AHM, DINA
	- Diverse data types
		- Test item contents 题目内容
		- examinees' background information 测试者背景
		- sophisticated graph-structured data 复杂图结构
		- Behavioral data 行为数据

# 3. Psychometrics-based cognitive diagnosis models

![[Pasted image 20241213150945.png#pic_center]]

## 3.1 ability levels paradigm

- Item Response Theory (IRT)
	- ==Model==: IRT (most classical latent trait methods for  measuring human cognitive status)
	- ==Assumption==: relation between **examinees' responese** and **their ability levels** can be modeledby a continuous mathematical function. $Pr(r_{ij}=1)=f(\theta_i,\beta_j)$
	- ==1 PL-IRT==: 

$$Pr(r_{ij}=1|\theta_i,b_j)=\sigma(\theta_i-b_j)=\frac{1}{1+e^{-(\theta_i-b_j)}}$$

	- ==2 PL-IRT==: 

$$
Pr(r_{ij}=1|\theta_i,a_j,b_j)=\frac{1}{1+e^{-a_j(\theta_i-b_j)}}
$$

	- ==3 PL-IRT==: 

$$
Pr(r_{ij}=1|\theta_i,a_j,b_j,c_j)=c_j+(1-c_j)\frac{1}{1+e^{-a_j(\theta_i-b_j)}}
$$

	- ==MIRT==: $\theta_i=(\theta_{i1},...,\theta_{im})$

$$
Pr(r_{ij}=1|\theta_i,a_i,b_j) = \frac{1}{1+e^{-{a_j^T(\theta_i-b_j)}}}=\frac{1}{1+e^{-\Sigma_k{a_j(\theta_{ik}-b_j)}}}=\frac{1}{1+e^{-{a_j(\Sigma_k\theta_{ik}-mb_j)}}}
$$

![[Pasted image 20241213152701.png]]

## 3 .2 cognitive level paradigm

在认知范式中，研究者关注的是对学生细粒度的认知状态的估计，例如一道题目考了知识点加法、减法、分数通分和约分，需要从题目中诊断学生对这些知识点的掌握程度
在认知水平范式中的 CDMs，诊断的过程就看作把学生分类成理想的熟练程度模式，
- ==what？==： estimation of the fine-grained cognitive states of students
- ==How？==： classifying students to an “ideal” proficiency pattern
- ==So==： traditional cognitive level paradigm-based CDMs are also named as Diagnostic Classification Model (DCM)
RSM And Its Variations
- ==RSM==： Rule Space Method. 规则空间方法
	- 侧重表示个体对测试项目做出的反应的认知过程，识别个体在回答测试项目时采用的特定规则。缺点在于它把只是概念看作独立的实体，忽略知识点之间的关系
- ==AHM==： Attribute Hierarchy Method 属性层次方法
	- Add a adjacent Matrix to Limit RSM
DINA and relevant CDMs
- ==DINA==：Deterministic Input, Noisy “And” Gate
	- Assumption: konwledge concepts is non-compensatory
	- $Pr(r_{ij}=1|\theta_i,q_j,s_j,g_j)=(1-s_j)^{\eta_{ij}}g_j^{1-\eta_{ij}}$, where $\eta_{ij}=\prod^K_{k=1}\theta_{ik}^{q_{jk}}$
	- $s_j$ and $g_j$ is slip and guess
		- About $\eta_{ij},e.g.$
		- $q_j=(0,0,1,1)$，$\theta_i=(0,1,1,1)\longrightarrow \eta_{ij}=1$
		- $q_j=(0,0,1,1)$，$\theta_i=(0,0,1,0)\longrightarrow \eta_{ij}=0$
![[Pasted image 20241218100546.png]]

```
$$\begin{aligned} P(r_{ij}=1|\theta_i, q_j) &= (1-s_j)\eta_{ij} + g_j(1-\eta_{ij}) \\
&=\left\{\begin{aligned}1-s_j,\eta_{ij}=1 \\ g_j,\eta_{ij}=0  \end{aligned}\right.
\quad where \quad\eta_{ij} = \prod_{k=1}^{K} \theta_{ik}^{q_{jk}}
\end{aligned}$$
```

- ==**DINO**==：The Deterministic Input, Noisy “Or” Gate
	- Assumption: knowledge concepts is compensatory
	- Shortcomings：over-estimation of students' ability levels
	- About $\eta_{ij},e.g.$
	- $q_j=(0,0,1,1)$，$\theta_i=(0,0,1,0)\longrightarrow \eta_{ij}=1$
	- $q_j=(0,0,1,1)$，$\theta_i=(0,0,1,1)\longrightarrow \eta_{ij}=1$
	- $q_j=(0,0,1,1)$，$\theta_i=(0,1,1,1)\longrightarrow \eta_{ij}=1$

![[Pasted image 20241218100610.png]]

```
$$ \begin{aligned}
P(R_{ij}=1|\theta_i, q_j) &= (1 - s_j)\eta_{ij} + g_j(1-\eta_{ij}) \\
&=\left\{\begin{aligned}1-s_j,\eta_{ij}=1 \\ g_j,\eta_{ij}=0  \end{aligned}\right. \quad where \quad \eta_{ij}=\left(1 - \prod_{k=1}^{K} (1-\theta_{ik})^{q_{jk}}\right)
\end{aligned}$$
```

# 4. 基于深度学习的模型

![[Pasted image 20241217092051.png]]
掌握模式分类器、认知交互模拟器、及编码器-解码器架构

## 4.1 非深度学习模型

- 聚类算法：将学生分为不同的簇，每个簇表示知识掌握模式
	- K-means 结合层次聚类分析、谱聚类、支持向量机 (SVM)、矩阵分解等协同过滤方法.
	- 上述机器学习模型侧重于预测学生表现，而不是诊断学生的知识水平.
	- FuzzyCDF 继承了模糊集处理主客观题目，用于 IRT 的变分贝叶斯推断算法，处理大规模数据集更准确.

## 4.2 深度学习模型

### 4.2.1 深度学习框架

融合深度学习方法已成为认知诊断的新趋势。根据模型架构及其出现时间，基于深度学习的 CDM 一般可以分为掌握模式分类器、认知交互模拟器和基于编码器-解码器的架构。
![[Pasted image 20241217092929.png]]
- 掌握模式分类器 (a)
	- 一种基于神经网络的反向模型结构: 它以考生的反应模式作为输入，直接输出考生的属性模式.
	- 问题：输出是考生属性模式，无法获取真实能力的作答数据 (采用 AHM 等方法生成模拟数据)，模型性能受限于生成训练数据的 CMDs
	- 优点: 新考生能够通过模型推断进行评估
$\theta=g_{NN}(Response,\Omega)$
- 认知交互模拟器 (b)
	- 传统心理测量基于专家设计交互函数 $f$, 有较高的可解释性，但导致较弱的拟合和泛化能力。
$Response=f_{NN}(\theta,\beta,\Omega)$
	- $\theta$ 表示考生能力水平 (多维连续向量)
	- $\beta$ 为题目特征如知识难度、项目区分度等

	- 深度神经网络 (DNN) 
		- 为了单调性假设、可推广和可解释性，Neural CD 具有很强的启发性.
		- $P(r_{ij}=1)=f_{DNN}(q_j(\circ(\theta_i-b_j)*a_j))$
	- 神经结构搜索 (Neural architecture search, NAS)
	- 图神经网络 (Graph neural network, GNN)

- Encoder-Decoder-based 框架 (c)
- (a) 看作编码器，(b) 看作解码器，那么组合的新框架可看作是编码器-解码器
- 克服了掌握模式分类器(a) 没有真实标签数据的问题
- 克服了认知交互模拟器 (b) 无法对训练数据中没出现过的学生进行诊断
$Response=f_{NN_{dec}}(\theta,\beta,\Omega_{dec}|\theta,\beta\leftarrow f_{NN_{enc}}(Response,\Omega_{enc}))$
- IC-CDF（中科大）考虑单调性、可识别性的自编码器
- ICDM（华东师大）构造了以学生为中心的图，增加了图信息的自编码器
- DCD（合工大）把学生能力和题目特征用分布形式表示，用变分自编码器做交互函数
- ICD () 提出一种数据增强的方式，使得每个学习者得作答被区分开

### 4.2.2 多方面的信息整合

尽管认知诊断交互函数技术取得了重大进展，但认知诊断的瓶颈来自初始化仅根据诊断因子的 ID 值得出诊断因子 (学习者特征和测试项目特征)。因此，研究人员开始探索如何利用多方面信息 (包括边信息和领域先验) 来增强诊断因子的表达能力，旨在进一步提高诊断模型的可解释性和性能

$$

Reponse=f_{NN}(\theta,\beta,\Omega|\theta\leftarrow f_{NN_{user}}(X,\Omega_{user}),\beta\leftarrow f_{NN_{user}}(X,\Omega_{item}))

$$

- 学生方面的信息 (Learner-side information)
- 题目方面信息 (Item-side information)
- 基于关系图的信息 (Relational graph-based information)

### 4.2.3认知诊断与知识追踪结合 

(Combination of cognitive diagnosis and knowledge tracing)

### 4.2.4其他问题

- 认知诊断中的冷启动问题
	- E.g.在线学习导致不同考生有选择性的接触其擅长的题目，或是不定期练习，产生"稀疏问题"，使得诊断结果有偏差.
- 认知诊断中的公平性
	- CDMs 对学生诊断是会容易受到地区或者社会背景影响，e.g.用河北高考学生数据训练的CDMs 诊断河北与福建学生.
- 群体诊断
	- 真实教学场景存在分组教学，因此需要小组的水平诊断。
- 对抗场景的认知诊断
	- 例如个体对抗 (棋类等)或者团队对抗(MOBA)，对反应过程进行能力诊断
- 诊断效率
	- 学生一直在做题，有新学生、题库有新题等情况，模型重新训练成本大
- 认知诊断中的数据隐私
	- 学习者在学习平台上的行为数据可能是学习者或平台管理员不允许共享的私有数据。

![[Pasted image 20241217130820.png]]