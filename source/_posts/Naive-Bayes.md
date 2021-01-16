---
title: Naive Bayes
date: 2021-01-16 21:53:17
categories: [MACHINE_LEARNING, NAIVE_BAYES]
tags: [machine learn, bayes, classification]
mathjax: true
---

## 基本方法

**输入**：
    * 设输入空间$\chi\subseteq \mathbf{R}^n$为$n$维向量的集合，输出空间为类标记集合$\gamma=\{c_1,c_2\cdots,c_K\}$。
    * 输入为特征向量$x\in\chi$，输出为类标记$y\in\gamma$。
    * $X$是定义在输入空间$\chi$上的随机向量，$Y$是定义在输出空间$\gamma$上的随机变量。
    * $P(X,Y)$是$X$和$Y$的联合概率分布。训练数据集$T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}$由$P(X,Y)$独立同分布产生。其中$x_i=(x_i^{(1)},x_i^{(2)},\cdots,x_i^{(n)})^T$，$x_i^{(j)}$是第$i$个样本的第$j$个特征，$x_i^{(j)}\in \{a_{j1}, a_{j2}, \cdots, a_{jS_j}\}$，$a_{jl}$是第$j$个特征可能的第$l$个值

**朴素贝叶斯假设**（条件独立性）：$P(X=x|Y=c_k)=P(X^{(1)}=x^{(1)},\cdots, X^{(n)}=x^{(n)}|Y=c_k)=\Pi^{n}_{j=1}P(X^{(j)}=x^{(j)}|Y=c_k)$

**学习与分类算法**：

1. 极大似然估计：$P_{\lambda}(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^{N}I(x_i^{(j)}=a_{jl},y_i=c_k)}{\sum_{i=1}^{N}I(y=c_k)},\lambda\geq0$
   1. 计算先验概率：$P(Y=c_k)=\frac{\sum^N_{i=1}I(y_i=c_k)}{N}$
   2. 计算条件概率：$P(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^{N}I(x_i^{(j)}=a_{jl},y_i=c_k)}{\sum_{i=1}^NI(y_i=c_k)}$
   3. 对于$x=(x^{(x)}, x^{(2)},\cdots,x^{(n)})^T$，计算$P(Y=c_k)\Pi^{n}_{j=1}P(X^{(j)}=x^{(j)}|Y=c_k)$
   4. 确定实例$x$的类，$y=\mathrm{argmax}P(Y=c_k)\Pi^{n}_{j=1}P(X^{(j)}=x^{(j)}|Y=c_k)$
2. 贝叶斯估计：$P_{\lambda}(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^{N}I(x_i^{(j)}=a_{jl},y_i=c_k)+\lambda}{\sum_{i=1}^{N}I(y=c_k)+S_j\lambda}, \lambda\geq0$

