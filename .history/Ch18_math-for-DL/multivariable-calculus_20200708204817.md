

<!--
 * @version:
 * @Author:  StevenJokes https://github.com/StevenJokes
 * @Date: 2020-07-08 19:12:24
 * @LastEditors:  StevenJokes https://github.com/StevenJokes
 * @LastEditTime: 2020-07-08 20:48:17
 * @Description:translate
 * @TODO::
 * @Reference:https://d2l.ai/chapter_appendix-mathematics-for-deep-learning/multivariable-calculus.html
-->

# 多元微积分

现在我们已经对单变量函数的导数有了相当深入的了解，让我们回到最初的问题，我们正在考虑一个可能有数十亿重量的损失函数。

## 高维微分

第18.3节告诉我们的是，如果我们改变这数十亿重量中的一个，而其他重量保持不变，我们就知道会发生什么！这只不过是一个单变量的函数，所以我们可以写

TODO:MATH

我们将一个变量中的导数称为*偏导数*，而另一个变量中的导数将被修正。在(18.4.1)中，我们将使用标记方法∂∂w1:

现在，让我们把 w 2 w2改成 w 2 + 2 w2 + 2:

我们再次使用了1212这个概念，它是一个高阶项，我们可以像上一节中抛弃22一样抛弃它，还有我们在(18.4.1)中看到的。以这种方式继续下去，我们可以这样写

TODO:MATH

然后

我们将向量 w l something wL 称为 l l 的梯度。

方程式(18.4.5)值得思考一会儿。它的格式和我们在一维空间中遇到的格式完全一样，只是我们把所有的东西都转换成了矢量和点积。它允许我们近似地告诉我们，在任何对输入的扰动情况下，函数 l 将如何变化。正如我们将在下一节中看到的，这将为我们提供一个重要的工具，帮助我们以几何学的方式理解如何使用梯度中包含的信息来学习。

但是首先，让我们用一个例子来看看这个近似，假设我们在处理函数

TODO:MATH

如果我们观察一个点，比如(0，log (2))(0，log (2)) ，我们可以看到

因此，如果我们想近似 f 在(1，log (2) + 2)(1，log (2) + 2)处，我们看到我们应该有(18.4.5)的具体实例:

我们可以在代码中测试这一点，看看这个近似有多好。

TODO:CODE

## 梯度和梯度下降的几何

我们唯一不知道确切的操作方法是在第二步中计算向量v。 我们将这种方向称为最陡下降方向。 使用对18.1节中点积的几何理解，我们可以将（18.4.5）重写为（18.4.10）L（w + v）≈L（w）+v⋅∇wL（w）=∥∇  wL（w）∥cos（θ）。

请注意，为方便起见，我们将方向设为长度1，并将θ用于v与∇wL（w）之间的角度。 如果我们想尽快找到使L减小的方向，则希望使它尽可能地为负。 我们选择的方向进入此方程的唯一方法是通过cos（θ），因此我们希望使该余弦尽可能为负。 现在，回顾余弦的形状，我们可以通过使cos（θ）=-1或等效地使梯度与我们选择的方向之间的角度为π弧度或等效地180度，使其尽可能为负。 实现此目的的唯一方法是朝完全相反的方向前进：选择v以指向∇wL（w）的完全相反方向！

这将我们带入了机器学习中最重要的数学概念之一：最陡峭体点的方向为-∇wL（w）-∇wL（w）。 因此，我们的非正式算法可以重写如下。

从初始参数ww的随机选择开始。

计算∇wL（w）∇wL（w）。

在与该方向相反的方向上走一小步：w→w−wL（w）w→w−wL（w）。

重复。

许多研究人员已经对该基本算法进行了多种修改和改编，但是其核心概念仍然相同。 使用该梯度找到尽快降低损耗的方向，并更新参数以朝该方向迈出一步。

TODO:电脑装机搞了一天，烧的不行。

* 在更高的维度中，我们可以定义与一维导数具有相同目的的渐变。 这些使我们能够看到对输入进行任意小的更改时多变量函数的变化。
* 可以将反向传播算法看作是组织多变量链规则以允许有效计算许多偏导数的一种方法。
* 矩阵演算允许我们以简洁的方式编写矩阵表达式的导数。

## 练习

1. 给定行向量β，计算f（x）=βx和g（x）=x⊤β⊤的导数。 为什么会得到相同的答案？
1. 令v为n维向量。 什么是∥v∥v∥2？
1. 令L（x，y）= log（ex + ey）。 计算渐变。 梯度分量的总和是多少？
1. 令f（x，y）= x2y + xy2。 证明唯一的临界点是（0,0）。 通过考虑f（x，x），确定（0,0）是最大值，最小值还是两者都不是。
1. 假设我们将函数f（x）= g（x）+ h（x）最小化。 我们如何用g和h来几何解释∇f= 0的条件？