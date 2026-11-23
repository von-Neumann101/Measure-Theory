# 基本定义
（概率）测度空间是一个三元组 $(\Omega,\mathcal F,\mathbf P)$：
- 样本空间 $\Omega$ 是任意非空集合
- $\sigma$-代数（或 $\sigma$-域）$\mathcal F$ 是样本空间 $\Omega$ **的若干子集**的集合，包含 $\emptyset,\Omega$，并且对于**取补集**、**可列并**和**可列交**运算封闭
- 概率测度是一个映射：$\mathbf P:\mathcal F\mapsto [0,1]$，满足 $\mathbf P(\varnothing)=0,\mathbf P(\Omega)=1$ 以及**可列可加性**。概率空间和测度空间的区别是 $\Omega$ 测度为 1

值得补充的是：$\sigma$-代数 $\mathcal F$ 是所有事件或者**可测集**的集合，这些 $\Omega$ 的子集 $A$ 满足 $\mathbf P(A)$ 是良定义的

![[Pasted image 20261118234336.png|700]]
证明都不难，都是构造不交并
# 构建概率三元组
考虑泊松分布 $\pi(5)$
- 样本空间 $\Omega=\mathbb N$
- $\sigma$ 代数 $\mathcal F$ 包含 $\Omega$ 的全部子集
- 概率测度 $\forall A\in\mathcal F,\mathbf P(A)=\sum_{k\in A}e^{-5}5^k/k!$

记 $\mathcal J=\{[0,1]\text{ 中的所有区间}\}$，显然有 $\mathcal J\subset\mathcal F$，$\mathcal J$ 是 $\Omega$ 子集的**半代数(semialgebra)**，即满足：
- 包含 $\emptyset,\Omega$
- 对于有限次交封闭
- 任何元素的补集等于其元素的有限不交并

注意到半代数 $\mathcal J$ 并不能生成 $\sigma$-代数，因为他**不对有限次并封闭**，进而**不对补集封闭**
所以我们考虑集合代数（域） $\mathcal B_0=\{\mathcal J\text{ 中所有元素的有限并}\}$，但是我们只要求“有限”，而**没有要求可列性**，比如：
$$
A_n=\big\{\frac1n\big\}\in\mathcal J,\quad n=1,2,...
$$
但是: 
$$
\bigcup_{n=1}^{\infty}A_n = \left\{1,\frac12,\frac13,\ldots\right\}\notin\mathcal B_0
$$
故集合代数不满足可列xx性（其实无限可数集都可以作为反例），所以不是 $\sigma$-代数
自然地，我们考虑扩张到可列并—— $\mathcal B_1$，但是这并不是 $\sigma$-代数（后面证明）
# 扩张定理
**The Extension Theorem**：
设 $\mathcal J$ 是 $\Omega$ 的子集构成的一个半代数，设 $\mathbf P:\mathcal J\to[0,1]$
- 满足 $\mathbf P(\varnothing)=0, \mathbf P(\Omega)=1$
- 满足**有限超可加性**：(其实是可列可加性+单调性推出来的)
  $$\mathbf P\left(\bigcup_{i=1}^{k}A_i\right)\geq\sum_{i=1}^{k}\mathbf P(A_i),\tag{2.3.2}$$
  其中 $A_1,\ldots,A_k\in\mathcal J$，$\bigcup_{i=1}^{k}A_i\in\mathcal J$，且 $\{A_i\}$ 中的集合两两不相交。
- 满足**可列单调性**：（重复计算+覆盖多出来的部分）
  $$\mathbf P(A)\leq\sum_{n=1}^{\infty}\mathbf P(A_n),\tag{2.3.3}$$
  其中 $A,A_1,A_2,\ldots\in\mathcal J$，且$A\subseteq\bigcup_{n=1}^{\infty}A_n.$

*实际上，有限超可加性+可列单调性可以推出可列可加性，$\mathbf P$ 实际上叫做**预测度**，也就是在半代数上的“概率测度”*
那么，存在一个 $\sigma$-代数：
$$
\mathcal M\supseteq\mathcal J,
$$
以及定义在其上的**概率测度**
$$
\mathbf P^*:\mathcal M\to[0,1],
$$
使得
$$
\boxed{
\mathbf P^*(A)=\mathbf P(A),
\qquad \forall A\in\mathcal J.
}
$$
也就是说，$(\Omega,\mathcal M,\mathbf P^*)$ 是一个合法的**概率空间**，并且在 $\mathcal J$ 上与原先定义的概率一致

简洁一点说，**扩张定理可以把半代数上的预测度 $\mathbf P$ 在保留原有映射规则的情况下，将其扩张为 $\sigma$-代数上的概率测度 $\mathbf P^*$**
## 证明
首先需要考虑的问题，怎么对非 $\mathcal J$ 的 $\sigma$-代数中的元素定义新的概率测度？我们需要引入**外测度 $\mathbf P^*$** 
$$
\mathbf P^*(A) = \inf_{\substack{A_1,A_2,\ldots\in\mathcal J\\ A\subseteq\bigcup_i A_i}} \sum_i \mathbf P(A_i), \qquad A\subseteq\Omega
$$
通过从半代数 $\mathcal J$ 中选取可数个集合 $A_i$ 覆盖 $\Omega$ 任意子集，最后取所有可能覆盖的下确界

**引理**：$P^*$ 是 $P$ 的扩张，即 $\forall A\in\mathcal J,P^*(A)=P(A)$
**证明**：先取 $A_1=A,A_i...=\emptyset$，那么 $A\subset\bigcup_iA_i$ $P^*(A)\le\sum_iP(A_i)=P(A)$，我们**找到了一个覆盖**使得 $P^*(A)\le P(A)$，意味着，下确界最多不会超过 $P(A)$
可列单调性描述了被覆盖的上界：$P(A)\le \sum_{n=1}^\infty P(A_n)$，也就是说，**任意的覆盖和**，都 $\ge P(A)$，那么覆盖和的下确界也 $\ge P(A)$，于是得到 $P(A)=P^*(A)$

**引理**：对于任意的子集 $A_i\subset\Omega$，外测度都满足**可列次可加性(countably subadditive)**：
$$
\mathbf P^*\!\left(\bigcup_{n=1}^\infty A_n\right) \le \sum_{n=1}^\infty \mathbf P^*(A_n),\quad A_n\subset\Omega
$$
**证明**：由于下确界可被任意逼近，那么对于任意 $A_n$，可以从 $\mathcal J$ 中选择一组集合 $\{C_{nk}|C_{nk}\in\mathcal J\}_{k=1}^\infty$，对于任意的误差 $\delta$，这里取 $\delta=\varepsilon 2^{-n}$，这里 $\varepsilon>0$ 是任意的，有：
$$
A_n\subseteq\bigcup_{k=1}^{\infty} C_{nk}, \qquad \sum_{k=1}^{\infty}\mathbf P(C_{nk}) \le \mathbf P^*(A_n)+\varepsilon 2^{-n}
$$
整个覆盖叠在一起 $\{C_{nk}\}_{n,k=1}^\infty$ 就覆盖了 $\bigcup_{n=1}^\infty A_n$，于是有：
$$
\mathbf P^*\!\left(\bigcup_{n=1}^{\infty}A_n\right) \le \sum_{n,k}\mathbf P(C_{nk}) \le \sum_n\mathbf P^*(A_n)+\varepsilon
$$
得证
这里的重点使用一个性质很好的区域（半代数）的集合来逼近（这里的误差无穷小）一个性质不好的区域（全部子集）的集合
> [!NOTE] 下确界可被任意逼近
> $\forall \delta>0,\exists s\in S$ 使得 $\inf S\le s<\inf S+\delta$

定义：
$$
\mathcal M = \left\{A\subseteq\Omega\ \middle|\ \mathbf P^*(A\cap E)+\mathbf P^*(A^C\cap E)=\mathbf P^*(E) \quad\forall E\subseteq\Omega \right\}
$$
用 $A$ 和其补集把任意子集划分为两部分，这两部分的外测度之和等于该子集的外测度
由次可加性，我们得到更常用的等价形式：
$$
\mathcal M = \left\{A\subseteq\Omega\ \middle|\ \mathbf P^*(A\cap E)+\mathbf P^*(A^C\cap E)\le\mathbf P^*(E) \quad\forall E\subseteq\Omega \right\}
$$

**引理**：若 $A_1$ 和 $A_2$ 不相交，且 $A_1\in\mathcal M$，则 $\mathbf P^*\!\left(\bigcup_n A_n\right)=\sum_n\mathbf P^*(A_n)$（扩张在 $\mathcal M$ 上可列可加）
**证明**：对于有限个，使用归纳法易证。下证对可列个成立。
考虑可数个两两不交的集合 $A_i\in\mathcal M$，对于任意 $m\in\mathbb N$，利用**单调性**：
$$
\sum_{n\le m}\mathbf P^*(A_n) =\mathbf P^*\!\left(\bigcup_{n\le m} A_n\right) \le \mathbf P^*\!\left(\bigcup_n A_n\right)
$$
这种手法叫**有限截断**，遇到无穷多个对象时，先设置一个 $n$ 的上界，以便于使用有限个时的情况，然后再放缩让这个上界消失，再把这个上界拉到无穷，得到无穷的证明
接下来使用可列次可加性的反向不等式得到等式成立

我们得到了 $P$ 的扩张 $P^*$ 是 $\mathcal M$ 上的概率测度，以及半代数上 $P=P^*$，接下来我们只需要证明 $\mathcal M$ 是 $\sigma$-代数即可（这是一条长路）

**引理**：$\mathcal M$ 是一个代数
**证明**：显然 $\mathcal M$ 对补集封闭，下证对有限次交封闭
$$
\begin{aligned}
&\mathbf P^*(A\cap B\cap E)+\mathbf P^*((A\cap B)^c\cap E)\\
&=\mathbf P^*(A\cap B\cap E)
  +\mathbf P^*((A^c\cap B\cap E)\cup(B^c\cap E))\\
&\le \mathbf P^*(A\cap B\cap E)
  +\mathbf P^*(A^c\cap B\cap E)+\mathbf P^*(B^c\cap E)\\
&=\mathbf P^*(B\cap E)+\mathbf P^*(B^c\cap E)
  &&(A\in\mathcal M)\\
&=\mathbf P^*(E) &&(B\in\mathcal M).
\end{aligned}
$$
易证对有限次交也是封闭的

**引理**：令 $A_1,A_2,...\in\mathcal M$ 是不交集，那么 $\bigcup_nA_n\in\mathcal M$
**证明**：我们已经证明了 $\mathcal M$ 是一个代数了，接下来尝试使用有限截断（由于 $\mathcal M$ 的等价形式，这非常有益于我们放缩）：
$B_m=\bigcup_{n\le m}A_n,m\in\mathbb N$，那么 $\forall m\in\mathbb N,E\subset\Omega$，有：
$$
\begin{aligned}
\mathbf P^*(E)
&= \mathbf P^*(E\cap B_m)+\mathbf P^*(E\cap B_m^C)\\
&= \sum_{n\le m}\mathbf P^*(E\cap A_n)+\mathbf P^*(E\cap B_m^C)\\
&\ge \sum_{n\le m}\mathbf P^*(E\cap A_n)
  +\mathbf P^*\!\left(E\cap\left(\bigcup_n A_n\right)^C\right)\\
&\ge \sum_n\mathbf P^*(E\cap A_n)
  +\mathbf P^*\!\left(E\cap\left(\bigcup_n A_n\right)^C\right)\\
&\ge \mathbf P^*\!\left(E\cap\bigcup_n A_n\right)
  +\mathbf P^*\!\left(E\cap\left(\bigcup_n A_n\right)^C\right).
\end{aligned}
$$
注意到这是我们之前写的 $\mathcal M$ 的等价形式，所以 $\bigcup_n A_n$ 是 $\mathcal M$ 中的元素

这里我们实际上用了一个**引理**：$P^*(E\cap B_m)=\sum_{n\le m}P^*(E\cap A_n)$，由于这是有限次的，我们使用归纳法：
对于 $m=1$，这是显然的
现在假设 $P^*(E\cap B_m)=\sum_{n\le m}P^*(E\cap A_n)$ 成立，证明 $P^*(E\cap B_{m+1})=\sum_{n\le m+1}P^*(E\cap A_n)$
$$
\begin{align}
P^*(E\cap B_{m+1})&=P^*(B_m\cap E\cap B_{m+1})+P^*(B_m^C\cap E\cap B_{m+1})\\
&=P^*(E\cap B_{m+1})+P^*(A_{m+1}\cap E)
\end{align}
$$
利用归纳假设即证（注意第二个式子需要不交集才成立）

**引理**：$\mathcal M$ 是一个 $\sigma$-代数
**证明**：由之前的引理可以得到 $\mathcal M$ 对于可列不交并封闭，接下来利用这个引理推导对于可列并封闭
实际上，只要构造 $D_i=A_i\cap A_1^C\cap...\cap A_{i-1}^C$ 即可，这是一系列两两不交集合，且 $\bigcup_i D_i=\bigcup_i A_i$

我们还差一个证明，也就是 $\mathcal M$ 要包含原来的半代数 $\mathcal J$
**引理**：$\mathcal J\subset \mathcal M$
**证明**：令 $A\in\mathcal J$，那么存在有限不交区间 $J_1,J_2,...,J_k$ 使得 $A^C=J_1\dot{\cup}...\dot{\cup}J_k$，我们考虑使用 $A_1,A_2,...$ 能覆盖 $\Omega$ 中的全部子集 $E$，即 $E\subset\bigcup_n A_n$
$$
\begin{align}
&P^*(E\cap A)+P^*(E\cap A^C)\\
&\le P^*((\bigcup_n A_n)\cap A)+P^*((\bigcup_n A_n)\cap A^C)\\
&=P^*((\bigcup_n A_n)\cap A)+P^*(\bigcup_n\bigcup_{i=1}^k(A_n\cap J_i))\\
&\le \sum_n [P(A_n\cap A)+\sum_{i=1}^k P(A_n\cap J_i)]\\
&= \sum_nP\big((A_n\cap A)\cup(A_n\cap J_1)\cup...\cup(A_n\cup J_k)\big)\\
&\le\sum_nP(A_n)
\end{align}
$$
接下来，由下确界可被无限逼近：
$$
\forall \varepsilon>0,\sum_nP(A_n)\le P^*(E)+\varepsilon
$$
由极限定义，得证！

**至此，扩张定理得证**

**命题**：扩张 $(\Omega,\mathcal M,\mathbf P^*)$ 必须是*完备的*，即如果 $A\in\mathcal M,\mathbf P^*(A)=0$，那么 $A$ 的任意子集 $B$ 都属于 $\mathcal M$
**证明**：$P^*(B)\le P^*(A)\Longrightarrow P^*(B)=0$，所以：
$$
P^*(E\cap B)+P^*(E\cap B^C)=P^*(E\cap B^C)\le P^*(E)
$$
这是等价形式，得证！
# 构建 $[0,1]$ 上的均匀分布
依旧是考虑所有区间的集合 $\mathcal J$，之前证明过这是一个半代数。对于 $I\in\mathcal J$ 令 $\mathbf P(I)$ 为区间 $I$ 的长度，现在需要证明 $P$ 满足扩张的条件

**命题**：$P$ 在 $\mathcal J$ 上满足有限超可加性的对应等式
**证明**：由于区间不交，所以可以直接让所有区间首尾相连，易证等式成立

**引理**：$I_1,I_2,...$ 是任意可数的区间集合，满足 $I\subset\bigcup_{j=1}^{\infty}I_j$ 的任意区间 $I$，都有：
$$
\sum_{j=1}^{\infty}P(I_j)\ge P(I)
$$
**证明**：我们可以尝试给区间设定开闭——把区间缩小都可以变成闭区间，把区间扩大都可以变成开区间，而只要控制放缩的大小就能使得最终的误差任意小（需要实数的完备性）：
将 $I$ 的左右各向内收缩 $\varepsilon/4$ 为闭区间（希望利用有界闭区间的[[补充#紧致性|紧致性]]），将 $I_n$ 的左右各向外扩张 $\varepsilon 2^{-n}/4$ 为开区间（紧致性需要开区间）：
$$
|I|\le\sum_n|I_n|+\varepsilon
$$
由于 $\varepsilon$ 任意小，所以不等式得证

**定理**：存在一个概率三元组 $(\Omega,\mathcal M,\mathbf P^*)$ 使得 $\Omega=[0,1]$，$\mathcal M$ 包含 $[0,1]$ 的所有区间，对于任意区间 $I\subset[0,1]$，$\mathbf P^*(I)$ 是 $I$ 的长度
这个概率三元组叫做 $[0,1]$ 上的均匀分布，或者是 $[0,1]$ 上的勒贝格(Lebesgue)测度
