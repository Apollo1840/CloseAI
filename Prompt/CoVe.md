# CoVe
https://arxiv.org/pdf/2309.11495

## Introduction
Like Zero-CoT, it is a way of prompting. And it is mainly for reduce hallucination. 

eg. 
```python
你将使用 Chain-of-Verification 来降低幻觉。严格按下面 4 个阶段输出，并使用指定标题。

用户问题：
{USER_QUESTION}

阶段1【草稿答案】
- 尽力回答，但允许不确定
- 不要编造来源/数据/论文结论
- 不确定点用“[不确定]”标记

阶段2【核查问题】
- 基于草稿生成 3-6 个可验证/可证伪的核查问题
- 覆盖最关键、最可能出错的断言
- 用编号列表输出

阶段3【逐条核查】
- 对阶段2的每个问题逐条回答
- 回答每个问题时：不要依赖草稿（假装草稿不可见）
- 若信息不足，写“无法验证”并说明缺什么证据

阶段4【最终答案】
- 结合核查结果修正草稿
- 保留无法验证点并解释原因
- 追加一个“已核查要点”列表，标注确定/不确定

```

上述是One-Prompt方法，效果不如分步式。因为验证问题时最好是独立QA。但是都比Baseline好。