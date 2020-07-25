

<!--
 * @version:
 * @Author:  StevenJokes https://github.com/StevenJokes
 * @Date: 2020-07-25 13:20:41
 * @LastEditors:  StevenJokes https://github.com/StevenJokes
 * @LastEditTime: 2020-07-25 13:29:39
 * @Description:translate by machine
 * @TODO::
 * @Reference:http://preview.d2l.ai/d2l-en/master/chapter_appendix-mathematics-for-deep-learning/information-theory.html
-->


# 信息理论

宇宙充满了信息。 信息提供了跨学科裂痕的通用语言：从莎士比亚的十四行诗到研究人员在康奈尔·阿克斯的论文，从梵高的印刷《星夜》到贝多芬的《第五音乐交响曲》，从第一门编程语言普兰卡克尔到最先进的机器 学习算法。 无论采用何种格式，一切都必须遵循信息论的规则。 利用信息论，我们可以测量和比较不同信号中存在多少信息。 在本节中，我们将研究信息理论的基本概念以及信息理论在机器学习中的应用。

在开始之前，让我们概述一下机器学习和信息理论之间的关系。 机器学习旨在从数据中提取有趣的信号并做出重要的预测。 另一方面，信息理论研究信息的编码，解码，传输和操纵。 结果，信息理论为讨论机器学习系统中的信息处理提供了基础语言。 例如，许多机器学习应用程序使用第3.4节中所述的交叉熵损失。 这种损失可以直接从信息理论的考虑中得出。

## 信息

让我们从信息理论的“灵魂”开始：信息。 信息可以用一种或多种编码格式的特定序列以任何形式编码。 假设我们要努力定义信息概念。 可能是什么起点？

考虑以下思想实验。 我们有一个朋友，一副扑克牌。 他们会洗牌，翻一些牌，并告诉我们有关牌的说明。 我们将尝试评估每个声明的信息内容。

首先，他们将卡片翻过来并告诉我们，“我看到卡片了。” 这根本没有提供任何信息。 我们已经确定情况确实如此，因此我们希望信息应该为零。

接下来，他们翻转卡片，然后说：“我看到一颗心。” 这为我们提供了一些信息，但实际上只有44种不同的诉讼是可能的，每种诉讼的可能性均等，因此我们对这一结果并不感到惊讶。 我们希望无论采取何种信息措施，此事件的信息含量都应较低。

接下来，他们翻转卡片，然后说：“这是33张黑桃。” 这是更多信息。 确实有5252个可能的结果可能，而我们的朋友告诉我们是哪一个。 这应该是中等数量的信息。

让我们将此推向逻辑极限。 假设最后他们翻过来了牌组中的每张牌，并读出了洗牌后的牌组的整个序列。 有52！52！ 甲板上有不同的订单，同样都有可能，因此我们需要大量信息来知道它是哪一个。

我们开发的任何信息概念都必须符合这种直觉。 确实，在下一节中，我们将学习如何计算这些事件分别具有0位0位，2位2位，5.7位5.7位和225.6位225.6位信息的信息。

如果我们阅读了这些思想实验，就会发现一个自然的想法。 作为出发点，我们可能会以信息为代表的意外程度或事件的抽象可能性，而不是关心知识。 例如，如果我们想描述一个不寻常的事件，我们需要很多信息。 对于常见事件，我们可能不需要太多信息。

1948年，克劳德·e·香农发表了《通信数学理论》[香农，1948]，建立了信息理论。在他的书中，香农第一次引入了信息熵的概念。我们将从这里开始我们的旅程。

## 自我信息

由于信息体现了事件的抽象可能性，因此我们如何将可能性映射到位数？ Shannon引入了术语位作为信息单位，它最初是由John Tukey创建的。 那么什么是“位”，为什么我们要用它来衡量信息呢？ 从历史上看，古董发射机只能发送或接收两种类型的代码：00和11。 实际上，二进制编码仍然在所有现代数字计算机上普遍使用。 这样，任何信息都由一系列的00和11编码。 因此，一系列长度为nn的二进制数字包含nn位信息。

现在，假设对于任何系列的代码，每个00或11发生的可能性为1212。 因此，具有一系列长度为nn的代码的事件XX发生的概率为12n12n。 同时，如前所述，该系列包含nn位信息。 那么，我们可以概括为一个数学函数，该函数可以将概率pp转换为位数吗？ 香农通过定义自我信息给出了答案

TODO:MATH

作为我们收到的有关此事件XX的信息。 请注意，本节将始终使用以2为底的对数。 为了简单起见，本节的其余部分将省略对数表示法中的下标2，即log（。）log⁡（。）始终引用log2（。）log2⁡（。）。 例如，代码“ 0010”具有自我信息



由于在最大似然估计中，我们通过使πj=pθ（yij∣xi）最大化目标函数l（θ）l（θ）。 因此，对于任何多类分类，最大化上述对数似然函数l（θ）l（θ）等效于最小化CE损失CE（y，y ^）CE（y，y ^）。

为了测试以上证明，让我们应用内置的度量NegativeLogLikelihood。 使用与前面的示例相同的标签和前缀，我们将得到与前面的示例相同的数值损失，直到小数点后5位。

TODO:CODE

## 小结

* 信息论是研究信息编码、解码、传输和操纵的学科。
* 熵是衡量有多少信息以不同的信号呈现的单位。
* KL散度也可以测量两个分布之间的散度。
* 交叉熵可以看作是多类分类的目标函数。交叉熵损失的最小化等价于对数似然函数的最大化。

## 练习

1. 验证从第一部分的卡例子确实有声称的熵。
1. 结果表明，对于所有分布pp和qq, KL散度D(p∥q)是非负的。提示:使用Jensen不等式，即。,使用计算lnx−−日志⁡x是一个凸函数。
1. 让我们从以下几个数据源计算熵:
    * 假设你正在观察一只猴子在打字机前产生的输出。猴子随机地按下打字机的4444个键中的任何一个(可以假定它还没有发现任何特殊键或shift键)。你观察到每个角色有多少位的随机性?
    * 由于对猴子不满，你用一个喝醉的排字工人代替了它。它能够产生词汇，尽管不是连贯的。相反，它从2000 2000个单词中随机抽取一个单词。再假设英语单词的平均长度为4.54.5个字母。你现在观察到多少位随机?
    * 仍然对结果不满意，您将排字机替换为高质量的语言模型。目前，每个角色的困惑度可以低至1515分。perplexity定义为长度归一化概率，即
        PPL (x) = [p (x)] 1 /长度(x)。
        你现在观察到多少位随机?
1. 直观地解释为什么我(X, Y) = H (X)−H (X | Y)我(X, Y) = H (X)−H (X | Y)。然后，通过将两边都表示为关于联合分布的期望来证明这是真的。
1. 两个高斯分布N(大气压强1，大气压强21)N(大气压强1，大气压强12)和N(大气压强2，大气压强22)N(大气压强2，大气压强22)之间的KL散度是多少?