# GPT-Academic Report
## # Title:



Neural Cognitive Diagnosis for Intelligent Education Systems

## # Abstract:



Cognitive diagnosis is a fundamental issue in intelligent education, which aims to discover the proficiency level of students on specific knowledge concepts. Existing approaches usually mine linear interactions of student exercising process by manual-designed function (e.g., logistic function), which is not sufficient for capturing complex relations between students and exercises. In this paper, we propose a general Neural Cognitive Diagnosis (NeuralCD) framework, which incorporates neural networks to learn the complex exercising interactions, for getting both accurate and interpretable diagnosis results. Specifically, we project students and exercises to factor vectors and leverage multi neural layers for modeling their interactions, where the monotonicity assumption is applied to ensure the interpretability of both factors. Furthermore, we propose two implementations of NeuralCD by specializing the required concepts of each exercise, i.e., the NeuralCDM with traditional Q-matrix and the improved NeuralCDM+ exploring the rich text content. Extensive experimental results on real-world datasets show the effectiveness of NeuralCD framework with both accuracy and interpretability.

## # Meta Translation

题目：用于智能教育系统的神经认知诊断

摘要：认知诊断是智能教育中的一个基本问题，旨在发现学生在特定知识概念上的熟练程度。现有的方法通常通过人为设计的函数（例如逻辑函数）来挖掘学生练习过程中的线性互动，这不足以捕捉学生与练习之间的复杂关系。在本文中，我们提出了一种通用的神经认知诊断（NeuralCD）框架，该框架结合神经网络来学习复杂的练习互动，以获得准确且可解释的诊断结果。具体来说，我们将学生和练习投射到因子向量，并利用多层神经网络来建模它们之间的互动，其中应用了单调性假设以确保因子解释的可行性。此外，我们提出了NeuralCD的两种实现方式，分别是传统Q矩阵的NeuralCDM及通过探索丰富文本内容的改进版NeuralCDM+。在真实数据集上的广泛实验结果表明，NeuralCD框架在准确性和可解释性方面的有效性。

## # Introduction

Cognitive diagnosis is a necessary and fundamental task in many real-world scenarios such as games (Chen and Joachims 2016), medical diagnosis (Guo et al. 2017), and education. Specifically, in intelligent education systems (Anderson et al. 2014;Burns et al. 2014), cognitive diagnosis aims to discover the states of students in the learning process, such as their proficiencies on specific knowledge concepts (Liu et al. 2018). Figure 1 shows a toy example of cognitive diagnosis. Generally, students usually first choose to practice a set of exercises (e.g., e 1 , • • • , e 4 ) and leave their responses (e.g., right or wrong). Then, our goal is to infer their actual knowledge states on the corresponding concepts (e.g., Trigonometric Function). In practice, these diagnostic reports are necessary as they are the basis of further services, such as exercise recommendation and targeted training (Kuh et al. 2011).
In the literature, massive efforts have been devoted for cognitive diagnosis, such as Deterministic Inputs, Noisy-And gate model (DINA) (De La Torre 2009), Item Response Theory (IRT) (Embretson and Reise 2013), Multidimensional IRT (MIRT) (Reckase 2009) and Matrix Factorization (MF) (Koren, Bell, and Volinsky 2009). Despite achieving some effectiveness, these works rely on handcrafted interaction functions that just combine the multiplication of student's and exercise's trait features linearly, such as logistic function (Embretson and Reise 2013) or inner product (Koren, Bell, and Volinsky 2009), which may not be sufficient for capturing the complex relationship between students and exercises (DiBello, Roussos, and Stout 2006). Besides, the design of specific interaction functions is also labor-intensive since it usually requires professional expertise. Therefore, it is urgent to find an automatic way to learn the complex interactions for cognitive diagnosis instead of manually designing them.
In this paper, we address this issue in a principled way of proposing a Neural Cognitive Diagnosis (NeuralCD) framework by incorporating neural networks to model complex non-linear interactions. Although the capability of neural networks to approximate continuous functions has been proved in many domains, such as natural language processing (Zhang et al. 2018) and recommender systems (Song et al. 2019), it is still highly nontrivial to adapt to cognitive diagnosis due to the following domain challenges. First, the black-box nature of neural networks makes them difficult to get explainable diagnosis results. That is to say, it is difficult to explicitly realize how much a student has mastered a certain knowledge concept (e.g., Equation). Second, traditional models are designed manually with non-neural functions, which makes it hard for them to leverage exercise text content. However, with neural network, it is worthy of finding ways to explore the rich information contained in exercise text content for cognitive diagnosis.
To address these challenges, we propose a NeuralCD framework to approximate interactions between students and exercises, yet preserving the explainability. We first project students and exercises to factor vectors and leverage multi-layers for modeling the complex interactions of student answering exercises. To ensure the interpretability Figure 1: A toy example of cognitive diagnosis. The student choose some exercises for practice and leave the response logs. With cognitive diagnosis methods, we get the diagnostic report containing the student's proficiency on each knowledge concept.
of both factors, we apply the monotonicity assumption taking from educational property (Reckase 2009) on the multilayers. Then, we propose two implementations on the basis of the general framework, i.e., NeuralCDM and Neural-CDM+. In NeuralCDM, we simply extract exercise factor vectors from traditional Q-matrix (an example is shown in Figure 6) and achieve the monotonicity property with positive full connection layers, which shows feasibility of the framework. While in NeuralCDM+, we demonstrate how information from exercise text can be explored with neural network to extend the framework. Particularly, our Neu-ralCD is a general framework since it can cover many traditional models such as MF, IRT and MIRT. Finally, we conduct extensive experiments on real-world datasets, and the results show the effectiveness of NeuralCD framework with both accuracy and interpretability guarantee.
Our code of NeuralCDM is available at https://github.com/bigdata-ustc/NeuralCD.

## 引言

认知诊断是许多现实世界场景中必要且基础的任务，例如游戏（Chen 和 Joachims 2016）、医疗诊断（Guo et al. 2017）和教育。具体来说，在智能教育系统中（Anderson et al. 2014；Burns et al. 2014），认知诊断旨在发现学生在学习过程中的状态，例如他们在特定知识概念上的熟练程度（Liu et al. 2018）。图1展示了一个认知诊断的简单示例。一般而言，学生通常会首先选择一组练习（例如，e1、...、e4）并留下他们的回答（例如，正确或错误）。然后，我们的目标是推断他们在对应概念（例如，三角函数）上的实际知识状态。在实践中，这些诊断报告是必要的，因为它们是进一步服务的基础，例如练习推荐和针对性训练（Kuh et al. 2011）。

在文献中，已为认知诊断付出了大量努力，例如确定性输入、噪声与门模型（DINA）（De La Torre 2009）、项目反应理论（IRT）（Embretson 和 Reise 2013）、多维项目反应理论（MIRT）（Reckase 2009）和矩阵分解（MF）（Koren、Bell 和 Volinsky 2009）。尽管取得了一定的效果，但这些工作依赖于手工设计的交互函数，这些函数仅能线性结合学生和练习的特征特征的乘法，例如逻辑函数（Embretson 和 Reise 2013）或内积（Koren、Bell 和 Volinsky 2009），这可能不足以捕捉学生和练习之间的复杂关系（DiBello、Roussos 和 Stout 2006）。此外，特定交互函数的设计也需要大量劳动力，因为这通常需要专业知识。因此，迫切需要找到一种自动学习复杂交互的方式，而不是手动设计它们。

在本文中，我们以原则性的方式解决这一问题，提出了一个神经认知诊断（NeuralCD）框架，将神经网络引入以建模复杂的非线性交互。尽管神经网络在许多领域（例如自然语言处理（Zhang et al. 2018）和推荐系统（Song et al. 2019））中证明了其逼近连续函数的能力，但由于以下领域挑战，适应认知诊断仍然是高度复杂的。首先，神经网络的黑箱特性使得它们难以获得可解释的诊断结果。也就是说，很难明确了解学生掌握某一知识概念（例如，方程）的程度。其次，传统模型使用非神经函数手动设计，这使它们难以利用练习文本内容。然而，使用神经网络的情况下，探索练习文本内容中包含的丰富信息对于认知诊断是值得的。

为了解决这些挑战，我们提出了一个NeuralCD框架，以逼近学生和练习之间的交互，同时保持解释性。我们首先将学生和练习投影到因子向量，并利用多层来建模学生回答练习的复杂交互。为了确保两个因子的可解释性，我们在多层上应用从教育属性（Reckase 2009）中获得的单调性假设。然后，我们基于这个一般框架提出了两个实现，即NeuralCDM和NeuralCDM+。在NeuralCDM中，我们简单地从传统的Q-矩阵中提取练习因子向量（如图6所示），并使用正完全连接层实现单调性属性，这展示了框架的可行性。而在NeuralCDM+中，我们展示了如何利用神经网络探索练习文本中的信息以扩展框架。特别地，我们的NeuralCD是一个通用框架，因为它可以覆盖许多传统模型，如MF、IRT和MIRT。最后，我们在真实世界数据集上进行了广泛的实验，结果表明NeuralCD框架在准确性和可解释性保证方面的有效性。

我们NeuralCDM的代码可在以下网址获取：https://github.com/bigdata-ustc/NeuralCD。

## # Related Work

In this section, we briefly review the related works from the following three aspects. Cognitive Diagnosis. Existing works about student cognitive diagnosis mainly came from educational psychology area. DINA (De La Torre 2009;von Davier 2014) and IRT (Embretson and Reise 2013) were two of the most typical works, which model the result of a student answering an exercise as the interaction between the trait features of the student (θ) and the exercise (β). Specifically, in DINA, θ and β were binary, where β came directly from Q-matrix (a human labeled exercise-knowledge correlation matrix, an example is showed in Figure 6). Another two exercise factors, i.e. guessing and slipping (parameterized as g and s) are also taken into consideration. The probability of student i correctly answering exercise j was modeled as
P (r ij = 1|θ i ) = g 1-ηij j (1 -s j ) ηij , where η ij = k θ β jk ik .
On the other hand, in IRT, θ and β were unidimensional and continuous latent traits, indicating student ability and exercise difficulty respectively. The interaction between the trait features was modeled in a logistic way, e.g., a simple version is sigmoid(a(θ -β)), where a is the exercise discrimination parameter. Although extra parameters were added in IRT (Fischer 1995;Lord 2012) and latent trait was extended to multidimensional(MIRT) (Adams, Wilson, and Wang 1997;Reckase 2009), most of their item response functions were still logistic-like. These traditional models depended on manually designed functions, which was laborintensive and restricted their scope of applications. Matrix Factorization. Recently, some researches from data mining perspective have demonstrated the feasibility of MF for cognitive diagnosis. Student and exercise correspond to user and item in matrix factorization (MF). For instance, Toscher et al. (2010) improved SVD (Singular Value Decomposition) methods to factor the score matrix and get students and exercises' latent trait vectors. Thai-Nghe et al. ( 2010) applied some recommender system techniques including matrix factorization in the educational context, and compared it with traditional regression methods. Besides, Thai-Nghe et al. (2015) proposed a multi-relational factorization approach for student modeling in the intelligent tutoring systems. Despite their effectiveness in predicting students' scores on exercises, the latent trait vectors in MF is not interpretable for cognitive diagnosis, i.e. there is no clear correspondence between elements in trait vectors and specific knowledge concepts. Artificial Neural Network. Techniques using artificial neural network have reached state-of-the-art in many areas, e.g., speech recognition (Chan et al. 2016), text classification (Zhang, Zhao, and LeCun 2015) and image captioning (Wang, Chen, and Hu 2019). There are also some educational applications such as question difficulty prediction (Huang et al. 2017), code education (Wu et al. 2019), formula image transcribing (Yin et al. 2018) and student performance prediction (Huang et al. 2019). However, using neural network for cognitive diagnosis is nontrivial as it performs poorly in parameter interpretation due to its inherent traits. To the best of our knowledge, deep knowledge tracing (DKT) (Piech et al. 2015) was the first attempt to model student learning process using recurrent neural network. However, DKT aims to predict students' scores, and does not make a distinction between an exercise and the knowledge concepts it contains, thus it's unsuitable for cognitive diagnosis. Few works with neural network have high interpretability for student cognitive diagnosis. Towards this end, in this paper we propose a neural cognitive diagnosis (NeuralCD) framework which borrows concepts from educational psychology and combine them with interaction functions learned from data. NeuralCD could achieve both high accuracy and interpretation with neural network. Be-sides, the framework is general that can cover many tradition models, and at the same time easy for extension.

### 相关工作

在本节中，我们将从以下三个方面简要回顾相关工作。

#### 认知诊断

现有关于学生认知诊断的工作主要来自教育心理学领域。DINA（De La Torre 2009; von Davier 2014）和IRT（Embretson and Reise 2013）是其中最典型的两个模型，它们将学生回答练习的结果建模为学生特征（θ）和练习特征（β）之间的交互作用。具体来说，在DINA中，θ和β是二进制的，其中β直接来源于Q矩阵（一个人工标注的练习-知识点关联矩阵，示例如图6所示）。另外两个练习因素，即猜测和失误（参数化为g和s）也被考虑在内。模型中，学生i正确回答练习j的概率被建模为

\[P(r_{ij} = 1 | \theta_i) = g_j^{1-\eta_{ij}} (1 - s_j)^{\eta_{ij}},\]

其中，\(\eta_{ij} = \prod_{k} \theta_{ik} \beta_{jk}\)。

另一方面，在IRT中，θ和β是单维和连续的潜变量，分别表示学生能力和练习难度。特征之间的交互在逻辑上建模，例如一个简单版本是 sigmoid(a(θ - β))，其中a是练习的区分参数。尽管IRT中增加了额外的参数(Fischer 1995; Lord 2012)并且潜在特质扩展到了多维（MIRT）(Adams, Wilson, and Wang 1997; Reckase 2009)，大多数的作答函数仍然类似于逻辑函数。这些传统模型依赖于手工设计的函数，这既劳动密集又限制了它们的应用范围。

#### 矩阵分解

最近，从数据挖掘角度来看，一些研究证明了矩阵分解（MF）在认知诊断中的可行性。学生和练习在矩阵分解中分别对应用户和项目。例如，Toscher等人(2010)改进了SVD（奇异值分解）方法来分解得分矩阵，并得到了学生和练习的潜在特质向量。Thai-Nghe等人(2010)将一些推荐系统技术，包括矩阵分解，应用于教育背景，并与传统的回归方法进行了比较。另外，Thai-Nghe等人(2015)提出了一种多关系分解方法用于智能辅导系统中的学生建模。尽管这些方法在预测学生练习得分方面有效，但矩阵分解中的潜在特质向量对于认知诊断来说是不可解释的，即特质向量中的元素与具体的知识点之间没有明确的对应关系。

#### 人工神经网络

采用人工神经网络的技术已在许多领域达到最先进水平，如语音识别（Chan等人2016）、文本分类（Zhang, Zhao, 和LeCun 2015）和图像字幕生成（Wang, Chen, 和Hu 2019）。也有一些教育应用，如问题难度预测（Huang等人2017）、代码教育（Wu等人2019）、公式图像转换（Yin等人2018）和学生成绩预测（Huang等人2019）。然而，使用神经网络进行认知诊断并不简单，因为由于其固有的特性，它在参数解释方面表现不佳。据我们所知，深度知识追踪（DKT）（Piech等人2015）是第一次尝试使用递归神经网络建模学生学习过程。然而，DKT旨在预测学生的得分，并没有区分练习和其包含的知识点，因此不适用于认知诊断。很少有使用神经网络的工作在学生认知诊断方面具有高解释性。为此，本文提出了一个神经认知诊断（NeuralCD）框架，它借鉴了教育心理学的概念，并将其与从数据中学习的交互函数结合起来。NeuralCD可以通过神经网络实现高准确性和解释性。此外，该框架是通用的，可以涵盖许多传统模型，同时易于扩展。

## # Neural Cognitive Diagnosis

We first formally introduce cognitive diagnosis task. Then we describe the details of NeuralCD framework. After that, we design a specific diagnostic network NeuralCDM with traditional Q-matrix to show the feasibility of the framework, and an improved NeuralCDM+ by incorporating exercise text content for better performance. Finally, we demonstrate the generality of NeuralCD framework by showing its close relationship with some traditional models.

我们首先正式介绍认知诊断任务。然后，我们描述NeuralCD框架的细节。接下来，我们设计了一个具体的诊断网络NeuralCDM，使用传统的Q-矩阵，以展示该框架的可行性，并通过结合练习文本内容提出了改进的NeuralCDM+，以实现更好的性能。最后，我们通过展示NeuralCD框架与一些传统模型的紧密关系，证明其通用性。

## # Task Overview

Suppose there are N Students, M Exercises and K Knowledge concepts at a learning system, which can be represented as S = {s 1 , s 2 , . . . , s N }, E = {e 1 , e 2 , . . . , e M } and K n = {k 1 , k 2 , . . . , k K } respectively. Each student will choose some exercises for practice, and the response logs R are denoted as set of triplet (s, e, r) where s ∈ S, e ∈ E and r is the score (transferred to percentage) that student s got on exercise e. In addition, we have Q-matrix (usually labeled by experts)
Q = {Q ij } M ×K , where Q ij = 1 if exercise e i relates to knowledge concept k j and Q ij = 0 otherwise.
Problem Definition Given students' response logs R and the Q-matrix Q, the goal of our cognitive diagnosis task is to mine students' proficiency on knowledge concepts through the student performance prediction process.

## 任务概述

假设学习系统中有N名学生、M道练习题和K个知识概念，可以分别表示为 S = {s₁, s₂, …, sN}、E = {e₁, e₂, …, eM} 和 Kₙ = {k₁, k₂, …, kK}。每个学生会选择一些练习题进行练习，响应日志 R 表示为三元组集合 (s, e, r)，其中 s ∈ S，e ∈ E，r 是学生 s 在练习题 e 上获得的分数（转化为百分比）。此外，我们还有Q矩阵（通常由专家标记）

Q = {Qij} M×K，其中 Qij = 1 表示练习题 eᵢ 与知识概念 kⱼ 相关，Qij = 0 则表示不相关。

### 问题定义

给定学生的响应日志 R 和 Q 矩阵 Q，我们的认知诊断任务的目标是通过学生表现预测过程挖掘学生在知识概念上的熟练度。

## # Neural Cognitive Diagnosis Framework

Generally, for a cognitive diagnostic system, there are three elements need to be considered: student factors, exercise factors and the interaction function among them (DiBello, Roussos, and Stout 2006). In this paper, we propose a general NeuralCD framework to address them by using multilayer neural network modeling, which is shown in Figure 2. Specifically, for each response log, we use one-hot vectors of the corresponding student and exercise as input and obtain the diagnostic factors of the student and exercise. Then the interactive layers learn the interaction function among the factors and output the probability of correctly answering the exercise. After training, we get students' proficiency vectors as diagnostic results. Details are introduced as bellow.
Student Factors. Student factors characterize the traits of students, which would affect the students' response to exercises. As our goal is to mine students' proficiency on knowledge concepts, we do not use the latent trait vectors as in IRT and MIRT, which is not explainable enough to guide students' self-assessment. Instead, we design the student factors as explainable vectors similar to DINA, but has a major difference that they are continuous. Specifically, We use a vector F s to characterize a student, namely proficiency vector. Each entry of F s is continuous ([0,1]), which indicates the student's proficiency on a knowledge concept. For example, F s = [0.9, 0.2] indicates a high mastery on the first knowledge concept but low mastery on the second. F s is got through the parameter estimation process.  Exercise Factors. Exercise factors denote the factors that characterize the traits of exercises. We divide exercise factors into two categories. The first indicates the relationship between exercises and knowledge concepts, which is fundamental as we need it to make each entry of F s correspond to a specific knowledge concept for our diagnosis goal. We call it knowledge relevancy vector and denote it as F kn . F kn has the same dimension as F s , with the ith entry indicating the relevancy between the exercise and the knowledge concept k i . Each entry of F kn is non-negative. F kn is previously given (e.g., obtained from Q-matrix). Other factors are of the second type and are optional. Factors from IRT and DINA such as knowledge difficulty, exercise difficulty and discrimination can be incorporated if reasonable.
Interaction Function. We use artificial neural network to obtain the interaction function for the following reasons. First, the neural network has been proven to be capable of approximating any continuous function (Hornik, Stinchcombe, and White 1989). The strong fitting ability of neural network makes it competent for capturing relationships among student and exercise factors. Second, with neural network, the interaction function can be learned from data with few assumptions (that behind traditional models). This makes NeuralCD more general and can be applied in broad areas. Third, the framework can be highly extendable with neural network. For instance, extra information such as exercise texts can be integrated in with neural network (We will discuss its extendability in the following subsections.). Mathematically, we formulate the output of Neu-ralCD framework as:
y = ϕ n (. . . ϕ 1 (F s , F kn , F other , θ f )),(1)
where ϕ i denotes the mapping function of the ith MLP layer; F other denotes factors other than F s and F kn (e.g., difficulty); and θ f denotes model parameters of all the interactive layers. However, due to some intrinsic characteristics, neural networks usually have poor performance on interpretation (Samek et al. 2016). Fortunately, we find that the monotonicity assumption, which is used in some IRT and MIRT models (Reckase 2009), can be utilized to ensure the interpretation of student and exercise factors. Monotonicity assumption is general and reasonable in almost all circum-stance, thus it has little influence on the generality of Neu-ralCD framework. The assumption is defined as follows:
Monotonicity Assumption The probability of correct response to the exercise is monotonically increasing at any dimension of the student's knowledge proficiency.
This assumption should be converted as a property of the interaction function. Intuitively, we assume student s to answer exercise e correctly. During training, the optimization algorithm should increase the student's proficiency if the model output a wrong prediction (i.e., a value below 0.5). The increment of each knowledge proficiency is otherwise controlled by F kn .
After introducing the structure of NeuralCD framework, we will next show some specific implementations. We first design a diagnostic model based on NeuralCD with extra exercise factors (i.e., knowledge difficulty and exercise discrimination)( §3.3), and further show its extendability by incorporating text information ( §3.4) and generality by demonstrating how it covers traditional models ( §3.5).

# 神经认知诊断框架

一般来说，对于一个认知诊断系统，需要考虑三个要素：学生因素、习题因素以及它们之间的交互函数 (DiBello, Roussos, and Stout 2006)。在本文中，我们提出了一种通用的神经认知诊断（NeuralCD）框架来通过多层神经网络模型来解决这些问题，如图2所示。具体来说，对于每个响应日志，我们使用对应学生和习题的one-hot向量作为输入，并获得学生和习题的诊断因素。交互层学习这些因素之间的交互函数，并输出正确回答习题的概率。在训练之后，我们得到学生的熟练度向量作为诊断结果。详细内容如下所述。

### 学生因素

学生因素描述了学生的特质，这会影响学生对习题的响应。由于我们的目标是挖掘学生对知识概念的熟练程度，我们不使用IRT和MIRT中常见的潜在特质向量，因为它们不足以指导学生的自我评估。相反，我们设计了可以解释的学生向量，类似于DINA模型，但有一个主要区别在于它们是连续的。具体来说，我们使用向量 \(F_s\) 来描述一个学生，称之为熟练度向量。\(F_s\) 的每个条目都是连续的（[0,1]），表示学生在某个知识概念上的熟练度。例如，\(F_s = [0.9, 0.2]\) 表示在第一个知识概念上掌握较高，但在第二个知识概念上掌握较低。\(F_s\) 是通过参数估计过程获得的。

### 习题因素

习题因素表示描述习题特质的因素。我们将习题因素分为两类。第一类表示习题和知识概念之间的关系，这非常重要因为我们需要它来使熟练度向量 \(F_s\) 的每个条目对应于一个特定的知识概念以实现我们的诊断目标。我们称它为知识相关性向量，记为 \(F_{kn}\)。\(F_{kn}\) 与 \(F_s\) 具有相同的维度，第 \(i\) 个条目表示习题与知识概念 \(k_i\) 之间的相关性。每个条目都是非负的。\(F_{kn}\) 之前是给定的（例如从Q矩阵中获得）。其他因素属于第二类并且是可选的。来自IRT和DINA的因素如知识难度、习题难度和区分度可以根据需要被合并进来。

### 交互函数

我们使用人工神经网络来获得交互函数，原因如下。首先，神经网络已被证明能够逼近任何连续函数 (Hornik, Stinchcombe, and White 1989)。神经网络的强大拟合能力使其能够捕捉学生和习题因素之间的关系。其次，使用神经网络，交互函数可以在较少假设的情况下从数据中学习（传统模型通常有更多的假设）。这使得NeuralCD更加通用，可以应用于广泛的领域。第三，该框架通过神经网络可以高度扩展。例如，可以将习题文本等额外信息整合进来（我们将在后续的小节中讨论其扩展性）。在数学上，我们将NeuralCD框架的输出表述为：
\[ y = ϕ_n (\ldots ϕ_1 (F_s, F_{kn}, F_{other}, θ_f)) \]
其中，\(ϕ_i\) 指的是第 \(i\) 层多层感知器（MLP）的映射函数；\(F_{other}\) 表示除了 \(F_s\) 和 \(F_{kn}\) 之外的因素（例如难度）；\(θ_f\) 表示所有交互层的模型参数。然而，由于一些内在特性，神经网络通常在解释性能方面表现较差 (Samek et al. 2016)。幸运的是，我们发现用于一些IRT和MIRT模型中的单调性假设 (Reckase 2009) 可以用于确保学生和习题因素的解释性。单调性假设在几乎所有情况下都是通用且合理的，因此对NeuralCD框架的通用性影响很小。该假设定义如下：

**单调性假设**：正确响应习题的概率在任何一个维度上随着学生知识熟练度的增加而单调增加。

这个假设应该转化为交互函数的一个属性。直观地看，我们假设学生 \(s\) 正确回答习题 \(e\)。在训练过程中，如果模型输出错误预测（即值低于0.5），优化算法应提高学生的熟练度。每个知识熟练度的增加由 \(F_{kn}\) 控制。

在介绍NeuralCD框架的结构之后，我们将展示一些具体的实现。我们设计了基于NeuralCD的诊断模型，采用了额外的习题因素（例如知识难度和习题区分度）（第3.3节），并通过整合文本信息展示其扩展性（第3.4节），通过展示其如何涵盖传统模型展示其通用性（第3.5节）。

## # Neural Cognitive Diagnosis Model

Here we introduce a specific neural cognitive diagnosis model (NeuralCDM) under NeuralCD framework. Figure 3 illustrates the structure of NeuralCDM. Student Factors. In NeuralCDM, each student is represented with a knowledge proficiency vector. The student factor F s aforementioned is h s here, and h s is obtained by multiplying the student's one-hot representation vector x s with a trainable matrix A. That is,
h s = sigmoid(x s × A),(2)
in which h s ∈ (0, 1) 1×K , x s ∈ {0, 1} 1×N , A ∈ R N ×K .
Exercise Factors. As for each exercise, the aforementioned exercise factor F kn is Q e here, which directly comes from the pre-given Q-matrix:
Q e = x e × Q,(3)
where Q e ∈ {0, 1} 1×K , x e ∈ {0, 1} 1×M is the one-hot representation of the exercise. In order to make a more precise diagnosis, we adopt other two exercise factors: knowledge difficulty h dif f and exercise discrimination h disc . h dif f ∈ (0, 1) 1×K , indicates the difficulty of each knowledge concept examined by the exercise, which is extended from exercise difficulty used in IRT. h disc ∈ (0, 1), used in some IRT and MIRT models, indicates the capability of the exercise to differentiate between those students whose knowledge mastery is high from those with low knowledge mastery. They can be obtained by:
h dif f = sigmoid(x e × B), B ∈ R M ×K (4) h disc = sigmoid(x e × D), D ∈ R M ×1 (5)
where B and D are trainable matrices.
Interaction Function. The first layer of the interaction layers is inspired by MIRT models. We formulate it as:
x = Q e • (h s -h dif f ) × h disc , (6
)
where • is element-wise product. Following are two full connection layers and an output layer:
f 1 = φ(W 1 × x T + b 1 ), (7) f 2 = φ(W 2 × f 1 + b 2 ), (8) y = φ(W 3 × f 2 + b 3 ), (9
)
where φ is the activation function. Here we use Sigmoid.
Different methods can be used to satisfy the monotonicity assumption. We adopt a simple strategy: restrict each element of W 1 , W 2 , W 3 to be positive. It can be easily proved that ∂y ∂h s i is positive for each entry h s i in h s . Thus monotonicity assumption is always satisfied during training.
The loss function of NeuralCDM is cross entropy between output y and true label r:
loss CDM = - i (r i log y i + (1 -r i ) log(1 -y i )). (10)
After training, the value of h s is what we get as diagnosis result, which denotes the student's knowledge proficiency.

# Neural Cognitive Diagnosis Model

在这里，我们介绍了在NeuralCD框架下的一个具体的神经认知诊断模型（NeuralCDM）。图3展示了NeuralCDM的结构。

学生因素。在NeuralCDM中，每个学生通过一个知识熟悉度向量来表示。前面提到的学生因素 \( F_s \) 在这里是 \( h_s \)，而 \( h_s \) 是通过将学生的单热编码向量 \( x_s \) 与一个可训练矩阵 \( A \) 相乘获得的。即：
\[ h_s = \sigma(x_s \times A) \]
其中 \( h_s \in (0, 1)^{1 \times K} \), \( x_s \in \{0, 1\}^{1 \times N} \), \( A \in R^{N \times K} \)。

习题因素。对于每道习题，前述的习题因素 \( F_{kn} \) 在这里是 \( Q_e \)，它直接来源于预给定的Q矩阵：
\[ Q_e = x_e \times Q \]
其中 \( Q_e \in \{0, 1\}^{1 \times K} \), \( x_e \in \{0, 1\}^{1 \times M} \) 是习题的单热编码表示。为了做出更精确的诊断，我们采用了另外两个习题因素：知识难度 \( h_{\text{diff}} \) 和习题区分度 \( h_{\text{disc}} \)。 \( h_{\text{diff}} \in (0, 1)^{1 \times K} \)，表示习题所考察的每个知识概念的难度，这是对IRT中使用的习题难度的扩展。 \( h_{\text{disc}} \in (0, 1) \)，在一些IRT和MIRT模型中使用，表示习题区分知识掌握高低学生的能力。它们可以通过以下公式获得：
\[ h_{\text{diff}} = \sigma(x_e \times B), B \in R^{M \times K} \]
\[ h_{\text{disc}} = \sigma(x_e \times D), D \in R^{M \times 1} \]
其中 \( B \) 和 \( D \) 是可训练的矩阵。

交互函数。交互层的第一层受MIRT模型启发。我们将其公式化为：
\[ x = Q_e \cdot (h_s - h_{\text{diff}}) \times h_{\text{disc}} \]
其中 \(\cdot\) 是元素逐一相乘。接下来是两个全连接层和一个输出层：
\[ f_1 = \phi(W_1 \times x^T + b_1) \]
\[ f_2 = \phi(W_2 \times f_1 + b_2) \]
\[ y = \phi(W_3 \times f_2 + b_3) \]
其中 \(\phi\) 是激活函数。这里我们使用Sigmoid。

可以采用不同的方法来满足单调性假设。我们采用一个简单的策略：限制 \( W_1 \), \( W_2 \) 和 \( W_3 \) 的每个元素为正数。可以很容易地证明 \(\frac{\partial y}{\partial h_{s_i}}\) 对于 \( h_s \) 中的每个条目 \( h_{s_i} \) 是正的。因此，在训练过程中单调性假设始终满足。

NeuralCDM的损失函数是输出 \( y \) 与真实标签 \( r \) 之间的交叉熵：
\[ \text{loss}_{\text{CDM}} = - \sum_{i} (r_i \log y_i + (1 - r_i) \log(1 - y_i)) \]

训练结束后，\( h_s \) 的值就是我们得到的诊断结果，表示学生的知识熟悉度。

## # NeuralCD Extension with Text Information

In NeuralCDM and some traditional methods (e.g., DINA), Q-matrix is the source of information about the exercise knowledge concept. However, manually-labeled Q-matrix may be deficient because of inevitable errors and subjective bias (Liu, Xu, and Ying 2012;DiBello, Roussos, and Stout 2006). On the other hand, exercise texts have been proved to be highly related to some exercise features (e.g., difficulty, relevant knowledge concepts) (Su et al. 2018;Huang et al. 2017), thus it can be leveraged to refine the Qmatrix. For example, in Q-matrix, maybe only 'Equation' is labeled for an equation solving exercise. However, we may discover that 'Division' is also required due to the existence of '÷' in the text. Traditional cognitive models didn't leverage text content due to the limitation of their handcraft nonneural interaction functions. However, with neural network, we are able to incorporate text information into our framework. We denote the extended model as NeuralCDM+, and present its structure in Figure 4.
Specifically, we first pre-train a CNN (convolutional neural network) to predict knowledge concepts related to the input exercise. CNN has advantage of extracting local information in text processing, thus it's able to capture important words from texts (e.g., words that are highly relative to certain knowledge concepts). The network takes concatenated word2vec embedding of words in texts as input, and output the relevancy of each predefined knowledge concept (that has occurred in data) to the exercise. Humanlabeled Q-matrix is used as label for training. We define
V k i = {V ij1 , V ij2 , . . . , V ij k }
as the set of top-k knowledge concepts of exercise e i outputted by the CNN.
Then we combine V k i with Q-matrix. Although there are defects in human-labeled Q-matrix, it still has high confidence. Thus we consider knowledge concepts labeled by Q-matrix are more relative than concepts in {k j |k j ∈ V k i and Q ij = 0}. To achieve this, we adopt a pairwise Bayesian method as follows. For convenience, we define partial order > + i as:
a > + i b, if Q ia = 1 and Q ib = 0 and b ∈ V k i , (11
)
and define the partial order relationship set as
D V = {(i, a, b)|a > + i b, i = 1, 2, . . . , M}.
Following traditional Bayesian treatment, we assume Q follows a zero mean Gaussian prior with standard deviation σ of each dimension. To give Q-matrix labels higher confidence, we define p(a > + i b| Qi ) with a pairwise logistic-like function:
p(a > + i b| Qi ) = 1 1 + e -λ( Qia-Qib ) . (12
)
The parameter λ controls the discrimination of relevance values between labeled and unlabeled knowledge concepts. The log posterior distribution over D V on Q is finally formulated as:
ln p( Q|D V ) = ln (i,a,b)∈DV p(a > + i b| Qi )p( Qi ) = M i=1 K a=1 K b=1 I(a > + i b) ln 1 1 + e -λ( Qia-Qib) + C - M i=1 K j=1 Q2 ij 2σ 2 , (13
)
where C is a constant that can be ignored during optimization. Before using Q in NeuralCDM, we need to restrict its elements to the range (0, 1), and set elements of concepts unlabeled or not predicted to 0. Thus, Sigmoid( Q)•M is used to replace Q in NeuralCDM, where M ∈ {0, 1} M ×K is a mask matrix, and
M ij = 1 if j ∈ V k i or Q ij = 1; M ij = 0 otherwise.
Q is trained together with the cognitive diagnostic model, thus the loss function is:
loss = -ln p( Q|D V ) + loss CDM .
(14)

### NeuralCD加上文本信息的扩展

在NeuralCDM和一些传统方法（如DINA）中，Q矩阵是关于练习知识概念的信息来源。然而，由于不可避免的错误和主观偏见，手动标注的Q矩阵可能存在缺陷（Liu, Xu, and Ying 2012; DiBello, Roussos, and Stout 2006）。另一方面，练习文本已被证明与一些练习特征（如难度、相关知识概念）高度相关（Su et al. 2018; Huang et al. 2017），因此可以利用其来改进Q矩阵。例如，在Q矩阵中，可能仅为一个方程求解练习标记了“方程”。然而，由于文本中存在“÷”，我们可能会发现“除法”也是必需的。传统的认知模型由于其手工设计的非神经交互函数的限制，未能利用文本内容。但是，借助神经网络，我们能够将文本信息整合到我们的框架中。我们将扩展模型记为NeuralCDM+，并在图4中展示其结构。

具体来说，我们首先预训练一个CNN（卷积神经网络）来预测与输入练习相关的知识概念。CNN在文本处理中具有提取局部信息的优势，因此能够从文本中捕捉重要的词汇（例如，与某些知识概念高度相关的词语）。该网络以文本中单词的word2vec嵌入的拼接作为输入，并输出每个预定义知识概念（在数据中出现的）与练习的相关性。人工标注的Q矩阵用作训练的标签。我们定义

\[ V_k^i = \{ V_{ij1}, V_{ij2}, \dots, V_{ij^k} \} \]

为由CNN输出的练习\(e_i\)的前k个知识概念的集合。

然后我们将\(V_k^i\)与Q矩阵结合。尽管人工标注的Q矩阵存在缺陷，但其仍然具有很高的可信度。因此我们认为Q矩阵标注的知识概念比集合 \(\{ k_j | k_j \in V_k^i 且 Q_{ij} = 0 \} \)中的概念更相关。为实现这一点，我们采用如下的成对贝叶斯方法。为了方便起见，我们定义偏序关系 >^+_i为：

\[ a >^+_i b, 如果 Q_{ia} = 1 且 Q_{ib} = 0 且 b \in V_k^i, \]

并定义偏序关系集为

\[ D_V = \{ (i, a, b) | a >^+_i b, i = 1, 2, \dots, M \}。\]

按照传统贝叶斯处理方法，我们假设Q服从标准差为σ的零均值高斯先验分布。为了赋予Q矩阵标签更高的可信度，我们用成对对数似然函数定义

\[ p(a >^+_i b|Q_i) = \frac{1}{1 + e^{-\lambda(Q_{ia} - Q_{ib})}}. \]

参数λ控制标注和未标注知识概念之间相关性值的辨别。最终，对Q的对数后验分布在\(D_V\)上的公式化如下：

\[ \ln p(Q|D_V) = \ln \prod_{(i,a,b) \in D_V} p(a >^+_i b|Q_i)p(Q_i) = \sum_{i=1}^M \sum_{a=1}^K \sum_{b=1}^K I(a >^+_i b) \ln \frac{1}{1 + e^{-\lambda(Q_{ia} - Q_{ib})}} + C - \sum_{i=1}^M \sum_{j=1}^K \frac{Q_{ij}^2}{2\sigma^2}, \]

其中C是优化过程中可以忽略的常数。在NeuralCDM中使用Q之前，我们需要将其元素限制在(0, 1)范围，并将未标注或未预测的概念元素设为0。因此，我们在NeuralCDM中用 \(Sigmoid(Q) \cdot M\) 替换Q，其中 \(M \in \{0, 1\}^{M \times K}\) 是掩码矩阵，并且

\[ M_{ij} = 1 \text{ 如果 } j \in V_k^i \text{ 或 } Q_{ij} = 1; M_{ij} = 0 \text{ 否则。} \]

Q与认知诊断模型一起训练，因此损失函数为：

\[ \text{损失} = -\ln p(Q|D_V) + \text{损失} _{CDM}。 \]

## # Generality of NeuralCD

In this subsection we show that NeuralCD is a general framework which can cover many traditional cognitive diagnostic models. Using Eq. ( 6) as the first layer, we now Top-k QId h s h diff k1 k2 k3 k4 k5 e1 0 1 0 0 0 e2 1 0 1 0 0 e3 0 0 0 1 0 e4 0 0 1 1 0 show the close relationship between NeuralCD and traditional models, including MF, IRT and MIRT. MF. Q e and h s can be seen as exercise and student latent trait vectors respectively in MF. By setting h dif f ≡ 0 and h disc ≡ 1, the output of the first layer is x = Q e • h s . Then in order to work like MF (i.e., y = Q e • h s ), all the rest of layers need to do is to sum up the values of each entry in x, which is easy to achieve. Monotonicity assumption is not applied in MF approaches. IRT. Take the typical formation of IRT y = Sigmoid((h sh dif f ) × h disc ) as example. Set Q e ≡ 1, and let h s and h dif f be unidimensional, the output of the first layer is x = (h sh dif f ) × h disc , followed by a Sigmoid activation function. Monotonicity assumption is achieved by limiting h disc to be positive. Other variations of IRT (e.g., y = C + (1 -C)y where C is guessing parameter) can be realized with a few changes. MIRT. One direct extension from IRT to MIRT is to use multidimensional latent trait vectors of exercises and student. Here we take the typical formation proposed in (Adams, Wilson, and Wang 1997) as example:
y = e Qe•h s -de 1 + e Qe•h s -de . (15
)
Let h disc ≡ 1, the output of the first layer given by Eq. ( 6) is
x = Q e • (h s -h dif f ). By Setting W 1 = [1 1 • • • 1]
, b 1 = 0 and φ(x) = x in Eq. ( 7), we have
f 1 = Q e • h s -d e (where d e = Q e • h dif f ).
All the rest of the layers need to do is to approximate the function g(f 1 ) = 1-Sigmoid(f 1 ), which can be easily achieved with two more layers. Monotonicity assumption can be realized if each entry of Q e is restricted to be positive.

## 通用性

在本小节中，我们展示了 NeuralCD 是一个通用框架，可以涵盖许多传统的认知诊断模型。利用公式（6）作为第一层，我们现在展示 NeuralCD 与传统模型（包括 MF、IRT 和 MIRT）之间的密切关系。

**MF**。在 MF 中，Qe 和 hs 可以分别视为练习和学生的潜在特征向量。通过设置 h_diff ≡ 0 和 h_disc ≡ 1，第一层的输出为 x = Qe • hs。为了使其类似于 MF（即 y = Qe • hs），其余层所需做的只是对 x 中每个条目的值求和，这很容易实现。MF 方法未应用单调性假设。

**IRT**。以 IRT 的典型形成 y = Sigmoid((h_s • h_diff) × h_disc) 为例。设 Qe ≡ 1，且让 hs 和 h_diff 为一维，第一层的输出为 x = (h_s • h_diff) × h_disc，然后通过 Sigmoid 激活函数进行处理。通过将 h_disc 限制为正值，实现了单调性假设。IRT 的其他变种（例如 y = C + (1 - C)y，其中 C 是猜测参数）也可以通过少量更改来实现。

**MIRT**。从 IRT 到 MIRT 的一个直接扩展是使用多维的练习和学生潜在特征向量。这里我们以 (Adams, Wilson, and Wang 1997) 提出的典型形成为例：
y = e^(Qe•hs - de) / (1 + e^(Qe•hs - de)。

设 h_disc ≡ 1，依据公式（6）给出的第一层输出为：
x = Qe • (hs - h_diff)。通过设置 W1 = [1 1 • • • 1]，b1 = 0 和 φ(x) = x 在公式（7）中，我们有：
f1 = Qe • hs - de（其中 de = Qe • h_diff）。

其余层所需做的只是逼近函数 g(f1) = 1 - Sigmoid(f1)，这可以通过再添加两层轻松实现。如果将 Qe 的每个条目限制为正值，则可实现单调性假设。

## # Discussion

We have introduced the details of NeuralCD framework and showed special cases of it. It's necessary to point out that the student's proficiency vector F s and exercise's knowledge relevancy vector F kn are basic factors needed in NeuralCD framework. Additional factors such as exercise discrimination can be integrated into if reasonable. The formation of the first interactive layer is not limited, but it's better to contain the term F s • F kn to ensure that each dimension of F s corresponds to a specific knowledge concept. The positive full connection is only one of the strategies that implement monotonicity assumption. More sophisticated network structures can be designed as the interaction layers. For example, recurrent neural network may be used to capture the time characteristics of the student's learning process.

我们介绍了NeuralCD框架的详细信息，并展示了其特殊案例。需要指出的是，学生的熟练度向量 \(F_s\) 和练习的知识相关性向量 \(F_{kn}\) 是NeuralCD框架中所需的基本因素。额外的因素，如练习的区分度，可以在合理的情况下整合进来。第一个交互层的形成并不局限，但最好包含项 \(F_s \cdot F_{kn}\)，以确保 \(F_s\) 的每个维度对应于特定的知识概念。正向全连接只是实现单调性假设的一种策略。可以设计更复杂的网络结构作为交互层。例如，可以使用递归神经网络来捕捉学生学习过程的时间特征。

## # Experiments

We first compare our NeuralCD models with some baselines on the student performance prediction task. Then we make some interpretation assessments of the models.

我们首先在学生表现预测任务上将我们的NeuralCD模型与一些基准模型进行比较。然后，我们对模型进行一些解释性评估。

## # Dataset Description

We use two real-world datasets in the experiments, i.e., Math and ASSIST. Math dataset supplied by iFLYTEK Co., Ltd. is collected from the widely-used online learning system Zhixue1 , which contains mathematical exercises and logs of high school examinations. ASSIST (ASSISTments 2009-2010 "skill builder"
) is an open dataset collected by the AS-SISTments online tutoring systems (Feng, Heffernan, and Koedinger 2009), which only provides student response logs and knowledge concepts2 . We choose the public corrected version that eliminates the duplicated data issue proposed by previous work (Xiong et al. 2016). Table 1 summarizes basic statistics of the datasets. We filter out students with less than 30 and 15 response logs for Math and ASSIST respectively to guarantee that each student has enough data for diagnosis. Therefore for dataset Math, we got 2,507 exercises with 497 knowledge concepts for diagnostic network, and the remaining exercises with knowledge concepts not appearing in logs are used for the Q-matrix refining part of NeuralCDM+. We perform a 80%/20% train/test split of each student's response log. As for ASSIST, we divide the response logs in the same way with Math, but NeuralCDM+ is not evaluated on this dataset as exercise text is not provided. All models are evaluated with 5-fold cross validation.
Students' knowledge proficiencies are stable in Math as the dataset is composed of logs from examinations. However, a student's proficiency on a knowledge concept may change as he will be continually given exercises of that concept until meeting certain criterion (e.g., answering 3 relevant exercises correctly in a row). To analyze whether static models (e.g., NeuralCD models and static traditional models) are suitable to apply on ASSIST, we compare two metrics between Math and ASSIST. The first metric is the average amount of logs that each student toke for each knowledge concept:
AVG #log = N i K j Log(i, j) N i K j I(Log(i, j) > 0) , (16
)
where Log(i, j) is the amount of exercises student s i answered that related to knowledge concept k j . Further, another metric is the mean standard deviation of scores r ij that Log(i, j) > 1 as:
STD #log>1 = mean si∈S ( mean kj ∈Kn, Log(i,j)>1 (std ij )),(17)
where std ij is the standard deviation of scores that student s i got for exercises related to knowledge concept k j . As the results showed in Table 1, although ASSIST has a much larger AVG #log than Math, their STD #log>1 are close. Therefore, it is reasonable to assume that the knowledge states of students in ASSIST are also stable, and our static NeuralCD models and baselines are applicable for both dataset. There will be more discussions in Model Interpretation.

## 数据集描述

我们在实验中使用了两个真实世界的数据集，即数学数据集和ASSIST数据集。数学数据集由科大讯飞有限公司提供，来源于广泛使用的在线学习系统Zhixue，该数据集包含数学练习题和高中考试的日志。ASSIST数据集（ASSISTments 2009-2010 “技能构建器”）是由ASSISTments在线辅导系统（Feng, Heffernan, 和 Koedinger 2009）收集的开放数据集，仅提供学生响应日志和知识概念。我们选择了经过公共修正的版本，以消除之前研究中提出的重复数据问题（Xiong et al. 2016）。表1总结了数据集的基本统计信息。为了确保每个学生有足够的数据进行诊断，我们筛选了响应日志少于30和15条的学生，分别对应数学数据集和ASSIST数据集。因此，数学数据集中，我们获得了2507个练习题和497个知识概念用于诊断网络，其余包含不在日志中的知识概念的练习题则用于NeuralCDM+的Q矩阵精炼部分。我们对每个学生的响应日志进行了80%/20%的训练/测试拆分。对于ASSIST，我们以与数学数据集相同的方式划分响应日志，但由于不提供练习文本，因此不对NeuralCDM+进行评估。所有模型均采用5折交叉验证评估。

数学数据集中的学生知识水平是稳定的，因为它由考试日志组成。然而，学生在某个知识概念上的熟练程度可能会变化，因为他会不断接收到该概念的练习题，直到达到某个标准（例如，连续正确回答3个相关练习题）。为了分析静态模型（例如NeuralCD模型和静态传统模型）是否适合用于ASSIST，我们比较了数学与ASSIST之间的两个指标。第一个指标是每个学生在每个知识概念上花费的平均日志数量：
\[ \text{AVG #log} = \frac{N_i K_j \text{Log}(i, j)}{N_i K_j I(\text{Log}(i, j) > 0)} \]
其中，\(\text{Log}(i, j)\)是学生\(s_i\)回答与知识概念\(k_j\)相关的练习题的数量。进一步，另一个指标是响应日志数量大于1的得分\(r_{ij}\)的平均标准差：
\[ \text{STD #log>1} = \text{mean}_{s_i \in S} \left( \text{mean}_{k_j \in K_n, \text{Log}(i,j) > 1} (\text{std}_{ij}) \right) \]
其中，\(\text{std}_{ij}\)是学生\(s_i\)在与知识概念\(k_j\)相关的练习题上获得的分数的标准差。正如表1中的结果所示，尽管ASSIST的AVG #log远大于数学数据集，但它们的STD #log>1接近。因此，可以合理地假设ASSIST中学生的知识状态也是稳定的，我们的静态NeuralCD模型和基线适用于这两个数据集。关于模型解释将有更多讨论。

## # Experimental Setup

The dimensions of the full connection layers (Eq. ( 7) ∼ (9)) are 512, 256, 1 respectively, and Sigmoid is used as activation function for all of the layers. We set hyperparameters λ = 0.1 (Eq. ( 12)) and σ = 1 ( Eq. ( 13)). For k in top-k knowledge concepts selecting, we use the value that make the predicting network reach 0.85 recall. That is, in our experiment, k = 20. We initialize the parameters with Xavier initialization (Glorot and Bengio 2010), which fill the weights with random values sampled from N (0, std 2 ),
where std = 2 nin+nout . n in is the number of neurons feeding into the weights, and n out is the number of neurons the results is fed to.
The CNN architecture we use in NeuralCDM+ contains 3 convolutional layers followed by a full connection output layer. MaxPooling are used after 1st and 3rd convolutional layers. The channels of convolutional layers are 400, 200, 100, and kernel sizes are set to 3, 4, 5 respectively. We adopt ReLu activation function for convolution layers and Sigmoid for the output layer. Multi-label binary cross entropy is used as loss function for training the CNN.
To evaluate the performance of our NeuralCD models, we compare them with previous approaches, i.e., DINA, IRT, MIRT and PMF. All models are implemented by PyTorch using Python, and all experiments are run on a Linux server with four 2.0GHz Intel Xeon E5-2620 CPUs and a Tesla K20m GPU.

### 实验设置

全连接层的维度（公式 (7) ∼ (9)）分别为 512、256 和 1，所有层均采用 Sigmoid 作为激活函数。我们设置超参数 λ = 0.1（公式 (12)）和 σ = 1（公式 (13)）。在选择前 k 个知识概念时，我们使用使预测网络达到 0.85 召回率的值。也就是说，在我们的实验中，k = 20。我们使用 Xavier 初始化（Glorot 和 Bengio 2010）来初始化参数，该方法将权重填充为从 N(0, std²) 中抽样的随机值，其中 std = 2 / (n_in + n_out)，n_in 是输入到权重的神经元数量，n_out 是结果输出到的神经元数量。

我们在 NeuralCDM+ 中使用的 CNN 架构包含 3 个卷积层，后接一个全连接输出层。在第一和第三个卷积层之后使用了最大池化。卷积层的通道数分别为 400、200 和 100，卷积核的大小设置为 3、4 和 5。我们在卷积层中采用 ReLu 激活函数，而在输出层中使用 Sigmoid。多标签二元交叉熵被用作训练 CNN 的损失函数。

为了评估我们 NeuralCD 模型的性能，我们将其与之前的方法进行了比较，即 DINA、IRT、MIRT 和 PMF。所有模型均通过 PyTorch 使用 Python 实现，所有实验在配备四个 2.0GHz Intel Xeon E5-2620 CPU 和一块 Tesla K20m GPU 的 Linux 服务器上运行。

## # Experimental Results Part-1

Student Performance Prediction The performance of a cognitive diagnosis model is difficult to evaluate as we can't  obtain the true knowledge proficiency of students. As diagnostic result is usually acquired through predicting students' performance in most works, performance on these prediction tasks can indirectly evaluate the model from one aspect (Liu et al. 2018). Considering that all the exercises we used in our data are objective exercises, we use evaluation metrics from both classification aspect and regression aspect, including accuracy, RMSE (root mean square error) (Pei et al. 2018) and AUC (area under the curve) (Bradley 1997).
Table 2 shows the experimental results of all models on student performance prediction task. The error bars after '±' is the standard deviations of 5 evaluation runs for each model. From the table, we can observe that NeuralCD models outperform almost all the other baselines on both datasets, indicating the effectiveness of our framework. In addition, the better performance of NeuralCDM+ over Neu-ralCDM proves that the Q-matrix refining method is effective, and also demonstrates the importance of fine estimated knowledge relevancy vectors for cognitive diagnosis.
Model Interpretation To assess the interpretability of NeuralCD framework (i.e., whether the diagnostic result is reasonable), we further conduct several experiments. Intuitively, if student a has a better mastery on knowledge concept k than student b, then a is more likely to answer exercises related to k correctly than b (Chen et al. 2017). We adopt Degree of Agreement (DOA) (Pirotte et al. 2007) as the evaluation metric of this kind of ranking performance. For knowledge concept k, DOA(k) is formulated as:

### 学生表现预测

认知诊断模型的性能难以评估，因为我们无法获得学生的真实知识水平。由于大多数研究通过预测学生的表现来获取诊断结果，因此在这些预测任务上的表现可以间接评估模型的一个方面（刘等，2018）。考虑到我们数据中使用的所有练习都是客观练习，我们从分类和回归两个方面使用评估指标，包括准确率、RMSE（均方根误差）（裴等，2018）和AUC（曲线下面积）（布拉德利，1997）。

表2展示了所有模型在学生表现预测任务上的实验结果。'±'后面的误差条是每个模型的5次评估运行的标准差。从表中可以看出，NeuralCD模型在这两个数据集上的表现几乎优于所有其他基准模型，表明我们框架的有效性。此外，NeuralCDM+相较于NeuralCDM的优异表现证实了Q矩阵精炼方法的有效性，也展示了对认知诊断而言，精确估计知识相关性向量的重要性。

### 模型解释

为了评估NeuralCD框架的可解释性（即，诊断结果是否合理），我们进一步进行了若干实验。直观地说，如果学生a对知识概念k的掌握优于学生b，那么a在回答与k相关的练习时，更有可能比b答对（陈等，2017）。我们采用一致性程度（Degree of Agreement, DOA）（皮罗特等，2007）作为这种排序性能的评估指标。对于知识概念k，DOA(k)的公式为：

## # Experimental Results Part-2

DOA(k) = 1 Z N a=1 N b=1 δ(F s ak , F s bk ) M j=1 I jk J(j, a, b) ∧ δ(r aj , r bj ) J(j, a, b) ,(18)
where Z = N a=1 N b=1 δ(F s ak , F s bk ). F s ak is the proficiency of student a on knowledge concept k. δ(x, y) = 1 if x > y and δ(x, y) = 0 otherwise. I jk = 1 if exercise j contains knowledge concept k and I jk = 0 otherwise. J(j, a, b) = 1 if both student a and b did exercise j and J(j, a, b) = 0 otherwise. We average DOA(k) on all knowledge concepts to evaluate the quality of diagnostic result (i.e., knowledge proficiency acquired by models).

实验结果部分-2

DOA(k) = \(\frac{1}{Z} \sum_{a=1}^{N} \sum_{b=1}^{N} \delta(F^s_{ak}, F^s_{bk}) \sum_{j=1}^{M} I_{jk} J(j, a, b) \land \delta(r_{aj}, r_{bj})}{J(j, a, b)} \), (18)

其中 \(Z = \sum_{a=1}^{N} \sum_{b=1}^{N} \delta(F^s_{ak}, F^s_{bk})\)。\(F^s_{ak}\) 是学生 \(a\) 在知识概念 \(k\) 上的熟练程度。δ(x, y) = 1 当 \(x > y\) 时，δ(x, y) = 0 否则。\(I_{jk} = 1\) 当练习 \(j\) 包含知识概念 \(k\) 时，\(I_{jk} = 0\) 否则。\(J(j, a, b) = 1\) 当学生 \(a\) 和学生 \(b\) 都完成了练习 \(j\) 时，\(J(j, a, b) = 0\) 否则。我们对所有知识概念的DOA(k)进行平均，以评估诊断结果的质量（即模型获得的知识熟练程度）。

## # Experimental Results Part-3

Among traditional models, we only compare with DINA, since for IRT, MIRT and PMF, there are no clear correspondence between their latent features and knowledge concepts. Besides, we conduct experiments on two reduced NeuralCDM models. In the first reduced model (denoted as NeuralCDM-Qmatrix), knowledge relevancy vectors are estimated during unsupervised training instead of getting from Q-matrix. While in another reduced model (denoted as NeuralCDM-Monotonocity), monotonicity assumption is removed by eliminating the positive restriction on the full connection layers. These two reduced models are used to demonstrate the importance of fine-estimated knowledge relevancy vector and monotonicity assumption respectively. Furthermore, we conduct an extra experiment in which students' knowledge proficiencies are randomly estimated, and compute the DOA for comparison.

在传统模型中，我们仅与DINA进行比较，因为对于IRT、MIRT和PMF，它们的潜在特征与知识概念之间没有明确的对应关系。此外，我们在两个简化的NeuralCDM模型上进行了实验。在第一个简化模型（记作NeuralCDM-Qmatrix）中，知识相关向量是在无监督训练期间估计的，而不是从Q矩阵获取的。另一方面，在另一个简化模型（记作NeuralCDM-Monotonocity）中，通过消除全连接层的正向限制，去除了单调性假设。这两个简化模型分别用于展示精确估计的知识相关向量和单调性假设的重要性。此外，我们还进行了一个额外实验，在该实验中，学生的知识熟练度是随机估计的，并计算了用于比较的DOA。

## # Experimental Results Part-4

Figure 5 presents the experimental results. From the figure we can observe that DOAs of NeuralCDM and Neural-CDM+ are significantly higher than baselines, which proves that knowledge proficiencies diagnosed by them are reasonable. The DOAs of NeuralCDM-Qmatrix and NeuralCDM-Monotonicity are much lower than NeuralCDM, which indicates that both information from Q-matrix and monotonicity assumption are important for getting interpretable diagnosis results (knowledge proficiency vectors). DOA of DINA is slightly higher than Random due to the use of Q-matrix. Besides, NeuralCDM performs much better on Math than on ASSIST. This is mainly due to the contradictions in logs, i.e., a student may answer some exercises containing knowledge concept k j correctly while others containing k j wrong (reasons may be the change of knowledge proficiency, or other knowledge concepts contained by the exercises). As showed in Table 1, ASSIST has much larger AVG #log and slightly higher STD #log>1 than Math dataset, which makes more contradictions in logs. Longer logs with more contradictions would decrease DOA.
Case Study. Here we present an example of a student's diagnostic result of NeuralCDM on dataset ASSIST in Figure 6. The upper part of Figure 6 shows the Q-matrix of three exercises on five knowledge concepts and the response of a student to the exercises. The bars in the underneath subfigure represent the student's proficiency on each knowledge concept. The lines with different colors and markers represent the knowledge difficulties of the three exercises (for clarity, we only present difficulties of relevant knowledge concepts for each exercise). We can observe from the figure that the student is more likely to response correctly when his proficiency satisfies the requirement of the exercise. For example, exercise 3 requires the mastery of 'Ordering Fraction' and corresponding difficulty is 0.35. The student's proficiency on 'Ordering Fraction' is 0.60, which is higher than required, thus he answered it correctly. Both knowledge difficulty (h dif f ) and knowledge proficiency (h s ) in Neural-CDM are explainable as expected.

实验结果部分-4

图5展示了实验结果。从图中可以观察到，NeuralCDM和NeuralCDM+的DOA（诊断准确度）明显高于基准模型，这证明了它们诊断出的知识掌握程度是合理的。NeuralCDM-Qmatrix和NeuralCDM-Monotonicity的DOA明显低于NeuralCDM，这表明Q矩阵和单调性假设的信息对于获取可解释的诊断结果（知识掌握向量）非常重要。DINA的DOA略高于随机模型，这归因于使用了Q矩阵。此外，NeuralCDM在数学数据集上的表现明显优于在ASSIST数据集上的表现。这主要是由于日志中的矛盾，即一个学生可能在包含知识概念k j的某些练习中回答正确，而在其他包含k j的练习中回答错误（原因可能是知识掌握程度的变化，或练习中包含的其他知识概念）。如表1所示，ASSIST的数据集的平均日志数量（AVG #log）远大于数学数据集，并且标准差（STD #log>1）也稍高，这使得日志中存在更多矛盾。更长的日志和更多的矛盾会降低DOA。

案例研究。在这里，我们展示了NeuralCDM在ASSIST数据集上对一个学生的诊断结果，如图6所示。图6的上半部分显示了三个练习在五个知识概念上的Q矩阵，以及学生对这些练习的响应。下方子图中的条形图表示学生在每个知识概念上的掌握程度。不同颜色和标记的线条表示三个练习的知识难度（为清晰起见，我们仅展示了每个练习相关知识概念的难度）。从图中可以观察到，当学生的掌握程度满足练习要求时，回答正确的可能性更大。例如，练习3要求掌握“排序分数”，对应的难度为0.35。学生在“排序分数”上的掌握程度为0.60，超过了要求，因此他正确回答了这个练习。在NeuralCDM中，知识难度（h dif f）和知识掌握程度（h s）都是可以解释的，符合预期。

## # Discussion.

From the above experiments, we can observe that NeuralCD models provide both accurate and interpretable results for cognitive diagnosis.
There still some directions for future studies. First, we may make our effort to design a more efficient model for knowledge concept prediction, which would promote the performance of NeuralCDM+. Second, the positive restriction on neural network weights may limit the approximate ability, thus we would like to explore more flexible methods to satisfy the monotonicity assumption. Third, since students' knowledge statuses change in many online selflearning circumstances, we would like to extend NeuralCD for dynamic cognitive diagnosis.

从上述实验中，我们可以观察到，NeuralCD 模型在认知诊断方面提供了准确且可解释的结果。未来的研究仍有一些方向。首先，我们可能会努力设计一个更高效的知识概念预测模型，这将提高 NeuralCDM+ 的性能。其次，对神经网络权重的正向限制可能会限制近似能力，因此我们希望探索更灵活的方法来满足单调性假设。第三，由于在许多在线自学环境中，学生的知识状态会发生变化，我们希望扩展 NeuralCD 以实现动态认知诊断。

## # Conclusion

In this paper, we proposed a neural cognitive diagnostic framework, NeuralCD framework, for students' cognitive diagnosis. Specifically, we first discussed fundamental student and exercise factors in the framework, and placed a monotonicity assumption on the framework to ensure its interpretability. Then, we implemented a specific model Neu-ralCDM under the framework to show its feasibility, and further extended NeuralCDM by incorporating exercise text to refine Q-matrix. Extended experimental results on realworld datasets showed the effectiveness of our models with both accuracy and interpretability. We also showed that Neu-ralCD could be seen as the generalization of some traditional cognitive diagnostic models (e.g., MIRT). The structure of the diagnostic network in our work is designed intuitively. However, with the high flexibility and potential of neural network, we hope this work could lead to further studies.

在本文中，我们提出了一种神经认知诊断框架NeuralCD框架，用于学生的认知诊断。具体而言，我们首先讨论了框架中的基本学生和练习因素，并对框架施加了单调性假设，以确保其可解释性。然后，我们在框架下实施了一个具体模型NeuralCDM，以展示其可行性，并通过结合练习文本来细化Q矩阵，进一步扩展了NeuralCDM。基于真实世界数据集的扩展实验结果显示了我们模型的有效性，兼具准确性和可解释性。我们还表明，NeuralCD可以被视为一些传统认知诊断模型（例如，MIRT）的推广。我们工作的诊断网络结构设计直观。然而，鉴于神经网络的高度灵活性和潜力，我们希望这项工作能够引领进一步的研究。

