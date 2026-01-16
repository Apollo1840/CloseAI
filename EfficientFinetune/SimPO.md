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
= -\mathbb{E}\Big[\log \sigma\big(\Delta\big)\Big]
$$

$$
\Delta = r'(x,y_{\text{win}})-r'(x,y_{\text{loss}})
$$

$$
r'(x,y)=\log \pi_\theta(y\mid x)-\log \pi_{\mathrm{ref}}(y\mid x)
$$

Where $\pi_{\mathrm{ref}}$ is the SFT model.