#科研 #文献笔记 #认知诊断


Leveraging Transferable Knowledge Concept Graph Embedding for Cold-Start Cognitive Diagnosis
利用可转移知识概念图嵌入进行冷启动认知诊断
### 0.abstract
认知诊断(Cognitive diagnosis, CD)旨在揭示学生对特定知识概念的熟练程度和试题的特征(如难度)。然而，近年来认知诊断的发展主要集中在提高诊断结果的准确性上，而往往忽视了领域级零射击认知诊断(DZCD)这一重要而实用的任务。DZCD的主要挑战是由于缺乏学生练习，导致目标域的学生行为数据不足用于培训目的的锻炼记录相互作用或不可用。为了解决冷启动问题，我们提出了一个两阶段的解决方案，名为TechCD(可转移知识概念图嵌入框架的认知诊断)。基本概念包括利用教学知识概念图(KCG)作为连接不同领域的中介，允许学生的认知信号从已建立的领域传输到零射冷启动领域。具体来说，首先在KCG上使用一种具有底层丢弃操作的朴素但有效的图卷积网络(GCN)来学习可转移的学生认知状态和特定领域的练习特征。此外，我们还根据典型的认知诊断解决方案给出了通用TechCD框架的三种实现。最后，在现实数据集上的大量实验不仅证明了Tech可以有效地进行零射击诊断，而且还给出了一些流行的应用，如运动推荐
### 1.introduction
**概述**：为了解决冷启动问题，提出了一个两阶段的解决方案TechCD：可转移知识概念图嵌入框架的认知诊断
**思路**：学生认知从已建立的领域传输到零射冷启动领域（教学知识概念图(KCG)作为中介）
**技术**：KCG（教学知识概念图）+图卷积网络(GCN) =学习可转移的学生认知状态和特定领域的练习特征
**结果**：典型的认知诊断解决方案给出了通用TechCD框架的三种实现
**问题**：domain-level zero-shot cognitive-exercise(DZCD)领域级zeroshot认知诊断是一个新的领域中无学生练习交互数据。
KCG涵盖每个领域的只是概念和相关练习，就能够链接不同领域
**例子**：数学(源领域)和编程(目标领域)，它们的每个练习都至少关联一个知识概念。

**定义一些属性**：适合CD的KCG模型应该具有四个基本属性
(1)面向诊断:该模型可以在DZCD设置中执行CD任务
(2)学生状态传播:KCG模型应该为学生嵌入提取通用和可转移的信息，使学生认知信号能够跨领域共享
(3)领域自适应:对于任何需要诊断的冷启动领域，期望模型具有领域自适应能力。
(4)应用:诊断结果可有效支持进一步的智能化服务
### 2.related work
### 3.preliminaries
#### 3.1认知诊断模型
分为数学建模参数估计方法、神经网络非线性的方法
#### 3.2知识概念图
全称为 Knowledge Concept Graph Embedding
定义：$\mathcal{G}=\{\mathcal{E,R,P}\}$
$\mathcal{E}$：实体集合（包括知识概念集$\mathcal{C}$与相关练习）
$\mathcal{R}$：关系集合（包括教育依赖关系（如先决条件、相似性），或者概念关联关系）
$\mathcal{P}$：实体-关系-实体三元组集合$\mathcal{P}=\{(h,r,t)|h,t\in\mathcal{E},r\in\mathcal{R}$}，
	例如（立方体概念，相似度，概念锥），（练习1，关联，函数概念）
#### 3.3问题定义
##### 符号定义
$\mathcal{S}$：成熟可用的source domain
$\mathcal{T}$：冷启动或者zero-shot的target domain
$\mathcal{U_S}$：为在source domain中的学生集
$\mathcal{V_S}$：为在source domain中的练习集
$\mathcal{U_T}$：为在target domain中的学生集
$\mathcal{V_T}$：为在target domain中的练习集
	其中有特别关系：
	目标域学生集合$\subset$源域学生集合内
	目标域题目和源域题目没有相同题目
$L_{\mathcal{S}}=\{(u_i,v_j,y_{ij})\}$，源域学生带标签的练习表现（表示源域的第$i$个学生，第$j$题，和是否做对）
$L_{\mathcal{T}}=\{(u_i,v_j)\}$，目标域学生练习无标签交互（表示目标域的第$i$个学生，第$j$题）
##### TechCD问题定义：
给定$L_\mathcal{S}$，$\mathcal{G}$，目标是通过充分利用$L_\mathcal{S}$，和学生成绩预测，对目标域$\mathcal{T}$中的学生进行诊断

### 4.the techCD framework

模型：general Transferable knowledgE Concept grapH framework to perform the domain-level zero-shot Cognitive Diagnosis (abbreviated as
TechCD)
![[Pasted image 20231226214148.png]]
4.1框架概述
#### 4.2知识概念图嵌入
**作用**：识别source domain的学生状态，通过定制KCG转移到zero-shot domain
**嵌入过程：**
每个实体嵌入，需要通过单独融合每种关系的相邻信息来区分不同的关系
实体$e_i$是可学习嵌入，作为GCN的输入，初始图的实体状态$z_i^{(0)}=e_i$，
（以下公式应该是[[GCN]]的特征提取过程：此处表示与练习$i$具有关系$r$的所有习题$j$进行遍历，每个实体乘以关系$r$对应的权重$W_r$）
![[Pasted image 20231226205007.png]]
$z_i^{(l)}$为GCN$l$次提取特征，$z_i^{(0)}=e_i$，初始值输入为每一个练习实体

$\mathcal{R}_i$为实体$e_i$的关系类型组成的$\mathcal{R}$的子集

$\mathcal{P}_i$：$\mathcal{P}$的子集，包含与$e_i$有关系$r$的所有三元组$(e_j,r,e_i)$

对于每一种关系，都具有一个学习矩阵$W_r$将练习概念实体特征变换到相同的嵌入空间。

【公式理解】若

![[Pasted image 20231226204956.png]]


![[Pasted image 20231226195537.png]]
$h_u$为学生转移认知状态

$H_u^S$为习题集（学生$u$与source domain$S$交互的习题集）

$z_v^\#$为学生状态（在底层的时候捕捉了实体特定的信息）







其他模型如neuralCDM






图神经网络参考帖子

[何时能懂你的心——图卷积神经网络（GCN） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/71200936)