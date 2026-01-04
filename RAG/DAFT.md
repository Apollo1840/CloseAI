# RAFT
https://arxiv.org/pdf/2403.10131

## Introduction

A RAG system:
- Retriever (find top-k relevant document)
- Answer

RAG termiology:



## Method


3 key methods:
- **Retrieval Augment**: append unrelated referenced document to the finetuning dataset.
- **Anti-collapsing**: have pure unrelated referencing finetuning samples.
- **CoT-Style**: change the (answer) label to CoT with verbatim citing style. 

### Retrieval augment

How to determine Related/Unrelated(`Golden/Distractor` in the paper)?

### Anti-collapsing

Propotion?

### CoT-Style

Use larger LLM.