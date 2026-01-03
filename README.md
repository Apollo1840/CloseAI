# CloseAI
This repository curates LLM (Large Language Model) research tailored for individual researchers. It focuses on high-impact work that does not require supercomputers, multi-GPU clusters, or massive data centers.

## Purpose
- **Discovery**: Catalog research that is accessible to independent developers.

- **Reproducibility**: Demonstrate how to run these models/methods on consumer-grade hardware or affordable cloud instances.

- **Inspiration**: Provide a starting point for individual researchers to implement and validate their own ideas with limited resources.

## Scope
What this repository is NOT:
- Computational-heavy tasks like designing new LLM architectures.
- Large-scale Pre-training or Full Parameter Fine-tuning (SFT).
- Fine-tuning models on massive private datasets.

What this repository FOCUSES on:
- Small Language Models (SLMs): High-performance models with low parameter counts. It may still be hard for individuals to even pretrain and finetune a SLM. However it become possible to test some ideas on SLM while it maybe too expensive to do it on LLM. 
- Compression: Model compression/quantification, long context compression etc.
- Parameter-Efficient Fine-Tuning (PEFT): Research into updating models without training all parameters. 
- Mechanistic Interpretability: The "neuroscience"/"Physics" of LLM.
  - Representation Engineering: Understanding and manipulating model internals without retraining.
- Prompt Engineering & Research: Maximizing model output through advanced prompting techniques.
