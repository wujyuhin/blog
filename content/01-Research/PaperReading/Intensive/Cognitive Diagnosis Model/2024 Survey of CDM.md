---
tags:
  - "#文献笔记"
parent: "A Survey of Models for Cognitive Diagnosis: New Developments and Future Directions"
collections:
  - 认知诊断
---
认知诊断模型研究综述：新进展与未来方向

# Introduction

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

![[Pasted image 20241210174212.png#pic_center|500]] 
- Base on psychometrics
	- Item response theory (IRT)
		- Measure macro ability of individuals
	- AHM, DINA, NIDA
		- The proposal and usage Q-matrix was a  significant milestone
- Base on machine learning
	- Filtering, matrix factorization, Neural network-based (协同过滤、矩阵分解、神经网络)
	- Deep learning-based: Neural CD (In order to better fitting ability of sophisticated cognitive process and promising interpretability.)（想要更好的拟合认知过程和可解释性，需要结合心理测量学的理论和假设）
![[Pasted image 20241211104950.png#pic_center]]

## CDM mathematization

- **Suppose Data**
	- Examinees $\mathcal{S}=\{S_1,...,S_I\}$
	- Items $\mathcal{E}=\{E_1,...,E_J\}$
	- Responeses $R=\{(S_i,E_j,r_{ij}),S_i\in\mathcal{S},E_j\in\mathcal{E},i=1,...,I\}$
	- Q-matrix $Q=\{q_{ij}^{J\times K}\},q_{jk}=1(or$ $0)$
	- Extra multifaceted information: $X$
- Problem Definition
	- Input: $R,Q,X$
	- Output (Goal of Cognitive diagnosis): examinees' ability levels $\theta_i(i=1,...,I)$ 
- Basic assumptions
	- Assumption 1 constant ability
		- Cognitive status remains unchanged during the process of answering the test items
		- 假设一个人的能力水平在短时间内不发生变化 (例如, 在标准测试期间) 是合理的，在此期间可以根据对测试项目的反应来测量该人的能力水平。认知诊断与知识追踪的重要区别在于，后者近年来也引起了广泛关注。知识追踪侧重于对在线学习者知识状态 (要么可解释, 要么不可解释) 的变化模式进行建模，高度依赖隐马尔可夫链和循环神经网络等时序建模方法。在知识追踪模型中，认知过程通常被忽视，而预测学习者的未来表现是最常用的任务。相比之下，认知诊断旨在测量学习者在一定时间内的能力水平。它挖掘学习者的反应数据，对回答项目的认知过程进行建模，并在一定的度量空间内提供学习者的能力水平值。
	- Assumption 2 constant item charateristics
		- The characteristics of a test item remain constant over all of the testing situations where it is used
		- 题目的一些统计量如正确率会受到考生的影响。然而，试题的难度、区分度、相关知识概念等特征反映了试题的本质特征，不应改变。这种稳定性有助于所有考生对测验项目的公平性，并表明测验项目可以用反映这些特征的固定参数值来表示。
	- Assumption 3 monotonicity
		- The probability of a correct response to the test item increases, or at least does not decrease, as the locations of examinees increase on any of the coordinate dimensions
		- 大多数认知诊断模型采用单调性假设对认知过程进行建模，尤其是基于 IRT 和 MIRT 的模型。该假设表明
		- 大多数认知诊断模型采用单调性假设对认知过程进行建模，尤其是基于 IRT 和 MIRT 的模型。该假设表明