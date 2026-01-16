# Fast Inference from Transformers via Speculative Decoding

https://arxiv.org/pdf/2211.17192

**Speculative decoding** speeds up inference for large autoregressive Transformers.

It uses a smaller, efficient “draft” model to propose multiple next tokens, then runs the large model in parallel to verify them with an exact sampling procedure.

