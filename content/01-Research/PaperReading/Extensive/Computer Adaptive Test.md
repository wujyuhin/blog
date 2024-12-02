#文献笔记 

期刊：[Studies in Educational Evaluation](https://www.sciencedirect.com/journal/studies-in-educational-evaluation)

Cat 关键词只有两篇

# 1.2009 Psychometric aspects of pupil monitoring systems 

# 1.Data for developing computerized adaptive testing of problematic mobile phone use

关键词  #CAT 

旨在问题性手机使用的测量使用 CAT 来做，为大规模、异质性样本的心理评估问题提供优化方案。该文章提供了数据

之前的工作：结构方程、回归分析、机器学习模型、项目反应模型

学生监测系统的心理测量方面

贡献：加权的方法提高初始估计的精度

# 2.Multistage Adaptive Testing for a Large-Scale Classification Test: Design, Heuristic Assembly, and Comparison with Other Testing Modes. 2012

检索平台：EBSCO

数据库：ERIC

# 2.Multidimensional adaptive testing in educational and psychological measurement: Current state and future challenges (2009 ) 

教育和心理测量中的多维适应性测试：现状和未来挑战

一篇综述，说明未来做多维的难点。

CDM 关键词只有 5 篇

- 中国高中英语阅读能力的诊断
	- 重点是具体的知识点的分析和语言素养的论证，模型次要
- 在伊朗 EAP 背景下用通用认知诊断模型改造雅思阅读部分
- 使用认知诊断模型规避国际评估中与结构无关的差异：一种对课程敏感的措施
- 开发用于认知诊断评估的阅读理解测试：RUM 分析
- 评估幼稚园儿童的数学问题解决能力：认知诊断测试的开发

> [!tldr] 2024 A Bounded Ability Estimation for Computerized Adaptive Testing.
> 
> **问题与动机:**
> 虽然 CAT 有效提升了测试效率并减少了所需试题数量，但传统方法往往侧重于最大化信息量或最小化信
> 息不确定性，而不是明确地追求准确的能力估计。由于缺乏受试者真实能力的标准，现有的方法在保证最终估计结果准确性方面存在局限性。
> 
> **方法:**
> 为解决上述问题，文章提出了一种名为"Bounded Ability Estimation for Computerized Adaptive Testing" (BECAT) 的框架。BECAT 旨在优化能力估计的准确性，通过分析估计的统计特性，找到了一个理论上的最佳近似一基于全题库的完整响应估计。框架采用数据提取的方法，选取与全响应梯度高度匹配的问题子集，以实现这一目标。具体来说，文章设计了一个基于预期梯度差异的近似法，进而开发了简单的贪婪选择算法来实现问题的动态选择，同时提供了能力估计的严格理论保证及误差上界。
> 
> **效果:**
> 实验结果显示，使用 BECAT 框架的 CAT 方法相较于传统方法，可以在减少约 15%的试题使用量的情况下达到相同的估计精度，显著降低了测试时长，提升了测试效率和实用性。
> 
> **有待解决的问题:** 尽管 BECAT 框架展示了改进能力估计的潜力，但它仍面临一些挑战。
> 
> - 首先，如何在保持测试的高效率与准确性之间找到更好的平衡点，尤其是在面对多样性和复杂性的测试内容时。
> - 其次，如何进一步优化算法性能，特别是在处理大规模题库和高维能力空间的情况下的效率和精确度。
> - 最后，未来研究可能需要探索将 BECAT 与其他先进的 AI 和机器学习技术结合，以进一步提升能力估计的精度和适应性。

^290308

>[!tldr] 2020 Deep reinforcement learning for adaptive learning systems
>期刊：[Psychometrika](https://link.springer.com/journal/11336)
> 
>**问题与动机**：先提出个性化教育的意义、然后是目前教师进行个性化的局限性、引出自适应测试、引出其中的潜在能力如何表征，提出现在工作是集中在学习路径建模、加速学习记忆、序列推荐、知识追踪和无模型算法。感觉引言没有很好的引出为什么要用强化学习MDP，就在说强化学习理论本身就是对自适应测试的最大动机一样，可看作是 RL 应用于 CAT 的开山之作
>
>**方法贡献**：
>- 将自适应学习问题建模成 MDP 问题，状态=潜在特征，动作=考生的学习题目，
>- 实际应用中状态转移模型未知，因此无法传统算法(值迭代)计算 MDP ，本文用的 free model 的深度强化学习
>-  free model DRL 需要大量状态转移的数据，在实际应用中不易获取，本文开发了转移模型估计（神经网络模拟考生学习过程），该转移模型使用历史数据拟合出来的
>
>**结论**：
>没有 baseline 比较，是 RL 内部用不同的策略优化比较，如 DQN、启发式、随机这三种策略计算 episode reward，DQN 最优
>
>**有待解决的问题**：
>- 第一、系统应该用于实际的考生，评价方法的有效性
>- 第二、CAT 由测量模型和策略学习模型（在 [[2024 Survey of CAT]] 中称为问题选择模型）组成，一些文献提出的系统认为某些题目会直接影响考生考试反应，因此不采纳。（？）
>- 第三、每个考生用同质的MDP 模型，可以进一步研究，在用 CAT 之前对考生进行分组，便于小组找到最优策略（理解：一个学习速度不同的学生，状态都是 0.9 的情况下，推荐同一道题目似乎不够好）
>- 第四、面向推荐系统的机器学习算法、协同过滤等于 RL 结合
>- 第五、进一步考虑在不同情景和约束条件下，DQN 学习策略比随机启发式策略好多少（？）
>- 第六、将 CAT 问题建模为 POMDP 问题，
>
>**应该精读**，MDP 用于 CAT 的初始文献

# 


数据库 [SAGE期刊（易阅通平台）](http://libdb-zju-edu-cn-s.webvpn.zju.edu.cn:8001/s/lib/libtb/show/555)

其中的期刊 Applied Psychological Measurement  [Applied Psychological Measurement](https://journals.sagepub.com/home/APM)
