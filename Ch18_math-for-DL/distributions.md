

<!--
 * @version:
 * @Author:  StevenJokes https://github.com/StevenJokes
 * @Date: 2020-07-25 14:04:21
 * @LastEditors:  StevenJokes https://github.com/StevenJokes
 * @LastEditTime: 2020-07-25 14:10:30
 * @Description:translate by machine half
 * @TODO::
 * @Reference:http://preview.d2l.ai/d2l-en/master/chapter_appendix-mathematics-for-deep-learning/distributions.html
-->

# 分布

既然我们已经学习了如何在离散和连续设置中以概率进行工作，那么让我们了解遇到的一些常见分布。根据机器学习领域的不同，我们可能需要熟悉其中更多的内容，或者对于某些深度学习领域可能根本不熟悉。但是，这是一个很好的基本清单。让我们首先导入一些常见的库。





## 指数族

上面列出的所有分布的一个共同性质是它们都属于所谓的指数族。指数族是一组分布，其密度可以用以下形式表示:

TODO:CODE

由于这个定义可能有点微妙，让我们仔细检查一下。

首先，h(x)被称为基础测度。这可以看作是我们用指数权值来修改的测量的原始选择。

其次，我们有向量boys =(boys 1, boys 2，…，boys l)∈Rl boys =(boys 1, boys 2，…，boys l)∈Rl，称为自然参数或规范参数。这些定义了如何修改基本度量。进入新措施的自然参数对一些采取这些参数的点积函数T (⋅) T (⋅) (x) = (x1, x2,…, xn)∈Rnx = (x1, x2,…, xn)∈Rn和取幂。T (x) = (T1 (x) T2 (x)…, Tl (x)) T (x) = (T1 (x) T2 (x)…, Tl (x))被称为ηη足够的统计数字。之所以使用这个名称，是因为T(x)T(x)表示的信息足以计算概率密度，不需要来自样本xx的其他信息。

第三，我们有A(恳请)A(恳请)，它被称为累积函数，它确保上述分布(18.8.20)积分为1，即，

TODO:MATH

具体来说，让我们考虑高斯分布。假设xx是一个单变量，我们看到它的密度是

TODO:MATH

这符合指数族的定义:

* 基本测度:h(x)=12√h(x)=12，
* 自然参数:η=[η1η2]=[μσ212σ2]η=[η1η2]=[μσ212σ2],
* 充分统计:T(x)=[x−x2]T(x)=[x−x2]，且
* 累积量功能:(η)= 12σ2μ2 +日志(σ)=η214η2−12日志(2η2)(η)= 12σ2μ2 +日志⁡(σ)=η124η2−12日志⁡(2η2)。

值得注意的是，对上述每一项的准确选择有些武断。事实上，重要的特征是分布可以用这种形式来表示，而不是精确的形式本身。

正如我们在3.4.5.2节中提到的，一种广泛使用的技术是假设最终输出yy服从指数族分布。指数族是机器学习中经常遇到的一种常见而强大的分布族。

## 小结

* 伯努利随机变量可用于对结果为是/否的事件进行建模。
* 离散均匀分布模型从一组有限的可能性中进行选择。
* 从间隔中选择连续的均匀分布。
* 二项分布为一系列伯努利随机变量建模，并计算成功次数。
* 泊松随机变量为稀有事件的到来建模。
* 高斯随机变量模拟将大量独立随机变量加在一起的结果。
* 以上所有分布均属于指数族。


## 练习

两个独立的二项式随机变量X,Y ~二项式(16,1/2)X,Y ~二项式(16,1/2)X的差值X - YX - Y的标准差是多少?

如果我们取一个泊松随机变量X ~泊松(流场)X ~泊松(流场)，并把(X−流场)/流场- -√(流场-流场)/流场看作是流场趋近于∞趋近于∞，我们可以发现这近似于高斯分布。为什么会这样呢?

nn元素上两个离散均匀随机变量之和的概率质量函数是什么?
