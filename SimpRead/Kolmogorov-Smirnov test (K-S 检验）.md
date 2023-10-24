做为一个数据科学家，在工作中时常会做一些统计假设检验，来检测数据是不是满足一定的统计分布。Kolmogorov-Smirnov test 是一个有用的非参数（nonparmetric）假设检验，主要是用来检验一组样本是否来自于某个概率分布（one-sample K-S test），或者比较两组样本的分布是否相同（two-sample K-S test）。

先介绍一下 one-sample K-S test，two-sample K-S test 类似。假设我们有观测值 X1， X2，。。。，Xn，我们认为这些值来自某个分布 P。K-S test 用来检验

H0: 样本来自于 P

H1: 样本不来自于 P

随机变量 X 的 cumulative distribution function F(x) 为 $F(x)=P(X\leq x)$ 。Cumulative distribution function 唯一地描述了一个概率分布。对于观测值 X1， X2，。。。，Xn，它们的经验分布函数（empirical distribution function）

$F_{obs}(x) = \frac{nums\space of\space observations\space below\space x}{observations}$

如果我们把所有的 observation 排个序，得到 y1， y2，。。。，yn，那么

$F_{obs}(y_{i})=\frac{i}{n}$

接下来需要做的是，把得到的 empirical distribution function 和 null hypothesis 中的 cumulative distribution function（记做 $F_{exp}$ ) 进行比较。

K-S statistic（检验统计量）是 $D_{n}=max|F_{exp}(x)-F_{obs}|$

举一个例子来说明。我们有 10 个数据点：

108， 112， 117， 130， 111， 131， 113， 113， 105， 128。我们想知道，这些点是否来自平均值是 120，标准差是 10 的正态分布？

首先进行排序。

105， 108，111，112， 113， 113， 117， 128， 130， 131。

计算 $F_{obs}$ 和 $F_{exp}$ 。

![](https://pic3.zhimg.com/v2-598fd6953d1ffddc8cde98f968e0c05a_b.jpg)

其中 $F_{exp}(y_{1})=P(X\leq105) = p(Z\leq\frac{105-120}{10}=P(Z\leq-1.5)=0.0668$

从上面的表个中可以看到， $D_{n}$ 的最大值是 0.358。 从表格（见附录）中可以查出，在 $\alpha$ =0.10 的时，critical value 是 0.37。因为 0.358 小于 0.37， 所以我们不拒绝 null hypothesis。

**Two-sample KS test**

接下来介绍一下 two-sample KS test。Two-sample KS test 回答这个问题：给定两组样本，检测是否他们的分布是否一样？

H0：两组样本的分布一样

H1：两组样本的分布不一样

仍然举例来说明。假设我们有以下两组样本：

X：1.2， 1.4， 1.9， 3.7， 4.4，4.8，9.7，17.3，21.1，28.4

Y：5.6，6.5，6.6，6.9，9.2，10.4，10.6，19.3

先把两组样本合在一块，进行排序，再计算 culumative emperical cdf。

![](https://pic3.zhimg.com/v2-860b83498b6f3b4017e18e67ab9d22d2_r.jpg)

K-S statistic（检验统计量）仍然是 $D_{n}=max|F_{exp}(x)-F_{obs}|$

这里 $D_{n}=0.6$

对于两样本，95% 的 critical value 的计算公式为：

$D_{crit,0.05}=1.36\sqrt{\frac{1}{n_{x}}+\frac{1}{n_{y}}}$ =0.645

因为 0.6<0.645，所以我们不拒绝原假设。

附录：

![](https://pic3.zhimg.com/v2-a831d74d745ccaf7ceb57110850bce5e_r.jpg)

Reference:

1) [Lesson 22: Kolmogorov-Smirnov Goodness-of-Fit Test](https://online.stat.psu.edu/stat415/book/export/html/838)

2) [Real Statistics Using Excel](https://www.real-statistics.com/statistics-tables/kolmogorov-smirnov-table/)

3) [http://www.stats.ox.ac.uk/~massa/Lecture%2013.pdf](http://www.stats.ox.ac.uk/~massa/Lecture%2013.pdf)