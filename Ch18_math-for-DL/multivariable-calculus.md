

<!--
 * @version:
 * @Author:  StevenJokes https://github.com/StevenJokes
 * @Date: 2020-07-08 19:12:24
 * @LastEditors:  StevenJokes https://github.com/StevenJokes
 * @LastEditTime: 2020-08-08 11:21:41
 * @Description:MT
 * @TODO::
 * @Reference:https://d2l.ai/chapter_appendix-mathematics-for-deep-learning/multivariable-calculus.html
-->

# 多元微积分

现在我们已经对单变量函数的导数有了相当深入的了解，让我们回到最初的问题，我们正在考虑一个可能有数十亿重量的损失函数。

## 高维微分

第18.3节告诉我们的是，如果我们改变这数十亿重量中的一个，而其他重量保持不变，我们就知道会发生什么！这只不过是一个单变量的函数，所以我们可以写

TODO:MATH

我们将一个变量中的导数称为*偏导数*，而另一个变量中的导数将被修正。在(18.4.1)中，我们将使用标记方法∂∂w1:

现在，让我们把 w 2改成 w 2 + 2:

我们再次使用了12这个概念，它是一个高阶项，我们可以像上一节中抛弃22一样抛弃它，还有我们在(18.4.1)中看到的。以这种方式继续下去，我们可以这样写

TODO:MATH

然后

我们将向量 w l something wL 称为 l的梯度。

方程式(18.4.5)值得思考一会儿。它的格式和我们在一维空间中遇到的格式完全一样，只是我们把所有的东西都转换成了矢量和点积。它允许我们近似地告诉我们，在任何对输入的扰动情况下，函数 l 将如何变化。正如我们将在下一节中看到的，这将为我们提供一个重要的工具，帮助我们以几何学的方式理解如何使用梯度中包含的信息来学习。

但是首先，让我们用一个例子来看看这个近似，假设我们在处理函数

TODO:MATH

如果我们观察一个点，比如(0，log (2))(0，log (2)) ，我们可以看到

因此，如果我们想近似 f 在(1，log (2) + 2)(1，log (2) + 2)处，我们看到我们应该有(18.4.5)的具体实例:

我们可以在代码中测试这一点，看看这个近似有多好。

TODO:CODE

## 梯度和梯度下降的几何

再考虑一下（18.4.5）：

（18.4.9）

L（w + ϵ）≈L（w）+ ϵ⋅∇wL（w）。

让我们假设我想用它来帮助减少损失LL。让我们从几何上理解第2.5节中首先介绍的梯度下降算法。我们将执行以下操作：

1. 从初始参数w的随机选择开始。
2. 找到使L在w下降最快的方向v。
3. 向该方向迈出一小步：w→w + ϵvw→w + ϵv。
4. 重复。

我们唯一不知道确切的操作方法是在第二步中计算向量v。我们将这种方向称为最陡下降方向。使用对18.1节中点积的几何理解，我们可以将（18.4.5）重写为（18.4.10）L（w + v）≈L（w）+v⋅∇wL（w）=∥∇  wL（w）∥cos（θ）。

请注意，为方便起见，我们将方向设为长度1，并将θ用于v与∇wL（w）之间的角度。如果我们想尽快找到使L减小的方向，则希望使它尽可能地为负。我们选择的方向进入此方程的唯一方法是通过cos（θ），因此我们希望使该余弦尽可能为负。现在，回顾余弦的形状，我们可以通过使cos（θ）=-1或等效地使梯度与我们选择的方向之间的角度为π弧度或等效地180度，使其尽可能为负。实现此目的的唯一方法是朝完全相反的方向前进：选择v以指向∇wL（w）的完全相反方向！

这将我们带入了机器学习中最重要的数学概念之一：最陡峭体点的方向为-∇wL（w）-∇wL（w）。因此，我们的非正式算法可以重写如下。

从初始参数ww的随机选择开始。

计算∇wL（w）∇wL（w）。

在与该方向相反的方向上走一小步：w→w−wL（w）w→w−wL（w）。

重复。

许多研究人员已经对该基本算法进行了多种修改和改编，但是其核心概念仍然相同。使用该梯度找到尽快降低损耗的方向，并更新参数以朝该方向迈出一步。

## 数学优化实现的注释

在本书中，由于深度学习设置中遇到的所有函数都过于复杂，无法明确地最小化，因此我们将重点放在数值优化技术上。

然而，考虑一下我们在上面获得的几何理解直接告诉我们如何优化函数是一个有用的练习。

假设我们希望找到使某个函数L(x)L(x)最小化的x0x0的值。我们假设有人给了我们一个值并且告诉我们这个值使LL最小化。我们是否可以检验他们的答案是否可信?

再次考虑（18.4.5）：（18.4.11）L（x0 + ϵ）≈L（x0）+ ϵ⋅∇xL（x0）。

如果梯度不为零，我们知道我们可以朝−ϵ∇xL（x0）方向迈出一步，以找到较小的L值。因此，如果我们真正处于最低限度，那就不可能如此！ 我们可以得出结论，如果x0为最小值，则∇xL（x0）= 0。我们称pointsxL（x0）= 0临界点。

这很好，因为在一些罕见的设置中，我们可以显式找到梯度为零的所有点，并找到具有最小值的一个点。
举一个具体的例子，考虑函数（18.4.12）f（x）= 3x4−4x3−12x2。

该函数的导数为（18.4.13）dfdx = 12x3-12x2-24x = 12x（x-2）（x + 1）。

极小值的唯一可能位置是x = −1,0,2，其中函数分别取值−5,0，−32，因此我们可以 结论是，当x = 2时，我们将函数最小化。快速绘图确认了这一点。

TODO:CODE

这突出了一个重要的事实，无论是从理论上还是从数值上进行工作，都应了解：我们可以最小化（或最大化）函数的唯一可能点的梯度将等于零，但是，并非每个梯度为零的点都是真实的全局最小值（或 最大值）。

## 一个小小的矩阵演算

涉及矩阵的函数的导数是非常好的。这一节可能会变得很繁琐，所以可能会在第一次阅读时被跳过，但是了解涉及公共矩阵运算的函数的导数如何比人们最初预期的更清晰是很有用的，特别是考虑到深度学习应用的中心矩阵运算。

让我们从一个例子开始。假设我们有一些固定的列向量ββ,我们想把产品函数f (x) =β⊤x,和理解当我们改变x时的点积变化。

在ML中处理矩阵导数时，有一个有用的符号叫做分母布局矩阵导数，在这里，我们将偏导数组合成任何向量、矩阵或张量的形状，在微分的分母中。在这种情况下，我们会写

TODO:MATH

我们匹配了列向量x的形状。

如果我们把函数写成分量的形式

TODO:MATH

如果我们现在相对于说β1取偏导数，请注意，一切都为零，而第一项只是x1乘以β1，因此我们得到

TODO:MATH

或更普遍地，

TODO:MATH

现在我们可以将其重组为矩阵以查看

TODO:MATH

这说明了关于矩阵演算的一些因素，我们在本节中将经常对此加以反驳：

1. 首先，计算将变得相当复杂。
1. 其次，最终结果比中间过程要干净得多，并且看起来总是类似于单变量情况。 在这种情况下，请注意ddx（bx）= b和ddx（β⊤x）=β相似。
1. 第三，转座似乎常常无处出现。 这样做的核心原因是我们习惯匹配分母的形状，因此当我们乘以矩阵时，我们将需要转置以匹配原始项的形状。

为了保持直觉，让我们尝试一些更难的计算。 假设我们有一个列向量x和一个方阵A，我们想计算

TODO:MATH

为了使符号更容易操作，让我们用爱因斯坦符号来考虑这个问题。在这种情况下，我们可以把函数写成

TODO:MATH

为了计算导数，我们需要了解每一个k的值

TODO:MATH

根据乘法法则，这是

TODO:MATH

对于像dxidxk这样的术语，不难发现当i = k时为1，否则为0。 这意味着i和k不同的每个项都将从该和中消失，因此保留在该第一个和中的唯一项是i = k的那些项。 对于第二项，我们需要j = k时，也具有相同的推理。 这给

TODO:MATH

现在，爱因斯坦符号中的指标名称是任意的——事实上，i和j的不同在这一点上对这个计算来说是无关紧要的，所以我们可以重新索引，以便它们都使用i来看到这一点

TODO:MATH

现在，这里是我们开始需要一些实践以进一步发展的地方。 让我们尝试根据矩阵运算来确定此结果。 aki + ai是A +A⊤的k，ik，i -th分量。 这使得

TODO:MATH

这里一个重要的微妙之处是k=a的要求并不出现在内部和中因为k是一个哑变量我们在内部项中求和。对于一个更简洁的示例，请考虑为什么

TODO:MATH

从这一点开始，我们可以确定和式的组成部分。首先,

TODO:MATH

所以这个和里面的整个表达式是

TODO:MATH

这意味着我们可以把导数写成

TODO:MATH

我们希望这个看起来像矩阵的a,b元素，所以我们可以使用前面例子中的技术来得到一个矩阵表达式，这意味着我们需要交换uiauia上指标的顺序。如果我们注意到uia = [U⊤]aiuia = U⊤ai,我们可以写

TODO:MATH

因此我们可以将解决方案写到（18.4.49）

TODO:MATH

这是一个矩阵乘积，因此我们可以得出以下结论：

TODO:MATH

这和我们上面猜测的解决方案是一致的!

在这一点上，我们有理由问:“为什么我不把我学过的所有微积分规则都写下来呢?”很明显，这仍然是机械的。我们为什么不赶快结束呢!确实存在这样的规则， [Petersen et al., 2008] 提供了一个很好的总结。但是，由于矩阵运算的组合方式与单值运算相比过多，因此存在着比单变量求导规则更多的矩阵求导规则。通常情况下，最好是使用索引，或者在适当的时候让它自动微分。

## 小结

* 在更高的维度中，我们可以定义与一维导数具有相同目的的渐变。这些使我们能够看到对输入进行任意小的更改时多变量函数的变化。
* 可以将反向传播算法看作是组织多变量链规则以允许有效计算许多偏导数的一种方法。
* 矩阵演算允许我们以简洁的方式编写矩阵表达式的导数。

## 练习

1. 给定行向量β，计算f（x）=βx和g（x）=x⊤β⊤的导数。为什么会得到相同的答案？
1. 令v为n维向量。什么是∥v∥v∥2？
1. 令L（x，y）= log（ex + ey）。计算渐变。梯度分量的总和是多少？
1. 令f（x，y）= x2y + xy2。证明唯一的临界点是（0,0）。通过考虑f（x，x），确定（0,0）是最大值，最小值还是两者都不是。
1. 假设我们将函数f（x）= g（x）+ h（x）最小化。我们如何用g和h来几何解释∇f= 0的条件？
