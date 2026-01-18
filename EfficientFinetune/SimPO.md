# SimPO
https://arxiv.org/pdf/2405.14734

【这项工作家用PC无法复现，但是包含很多小模型，所以推荐：https://github.com/princeton-nlp/SimPO
】

一种替代RLHF的方法，其中不使用RL，也不训练Reward Model。

## RLHF 传统方法
- a Reward Model(RM) is trained 
- and the RM  is used to further finetune the SFT through Proximal Policy Optimization (PPO).

## SimPO 方法
Create a loss to optimize, with the preference pairs data $\{(x, y_{win}, y_{lose})\}$

$$
\mathcal{L}_{\mathrm{DPO}}
= -\mathbb{E}\Big[\log \sigma\big(\Delta - \gamma \big)\Big]
$$

$$
\Delta = r'(x,y_{\text{win}})-r'(x,y_{\text{loss}})
$$

$$
r'_{\mathrm{simPO}}(x, y) \;=\;
\frac{\beta}{\lvert y \rvert}\,\log \pi_{\theta}(y \mid x)
$$



Where $\pi_{\mathrm{ref}}$ is the SFT model.


## SimPO 与 Direct Preference Optimization (DPO)

$$
r'_{\mathrm{DPO}}(x,y)=\log \pi_\theta(y\mid x)-\log \pi_{\mathrm{ref}}(y\mid x)
$$

从算法设计和理论逻辑上看，SimPO 与 DPO 之间主要有三个核心区别：

1. 移除了“参考模型”（Reference Model）
   
   这是 SimPO 在架构上最大的简化：DPO： 在计算 Loss 时，需要同时运行两个模型：一个是当前正在训练的模型，另一个是冻结的参考模型（SFT 模型）。DPO 通过比较这两个模型的概率比值来防止模型跑偏。SimPO： 完全不需要参考模型。它直接对当前模型生成的“好答案”和“坏答案”的对数概率进行对比。这直接节省了约 50% 的显存占用，同时也加快了训练速度。

2. 引入了“目标奖励边界”（Target Reward Margin, $\gamma$）
   
   这是 SimPO 提升效果的关键改进：DPO： 只要“好答案”的概率比“坏答案”高，Loss 就会降低。这可能导致模型学得“不求上进”，只要稍微好一点点就停止优化。SimPO： 引入了一个超参数 $\gamma$。它要求：好答案的对数概率 减去 坏答案的对数概率，必须大于 $\gamma$。这个“边界”强制模型必须显著地拉开好坏答案之间的差距，从而使模型在人类偏好上的表现更加鲁棒（Robust）。

3. 长度归一化（Length Normalization）的本质不同你提到的长度问题确实是核心，但我们可以从原理上深挖一下：
   
   DPO 的隐患： DPO 使用的是全句对数概率之和（Sum of log-probabilities）。由于每个 token 的对数概率通常是负数，长句子因为包含更多 token，其概率累加值在数学上更容易受到干扰，导致模型发现“增加长度”是骗取更高奖励的捷径（这就是所谓的“Verbosity Bias”）。SimPO 的解法： SimPO 使用的是平均对数概率（Average log-probabilities），即把总概率除以 token 数量。这样，模型评价的是“每一个 token 的平均质量”，而不是看谁的词儿多。