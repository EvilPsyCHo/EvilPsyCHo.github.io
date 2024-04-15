---
title: Using llamacpp grammar and pydantic to Constrain LLMs output format
layout: page
hide_header: true
---

Due to the limitation in training dataset and model parameter scale, most the open source LLMs suck as Llama2, Mistral, Baichuan2, etc., are unable to support features like `function call` or output specified format as effectively as GPT-4.

Based on the modifications to the sampling rules ultilizing token probability predicted by LLMs, we can solve this perfectly. For example, when numerical outputs are required, the sample probabilities of non-numerical are suppressed, achieving the desired output. This can be a transitional approach in response to the insufficient capabilities of open source LLMs. Here are some project related to this purpose:
- [llamacpp grammar](https://github.com/ggerganov/llama.cpp/blob/master/grammars/README.md)
- [guidance](https://github.com/guidance-ai/guidance)
- [localai](https://localai.io/features/openai-functions)
- [functionary](https://github.com/MeetKai/functionary)
- [https://github.com/1rgs/jsonformer](jsonformer)
- [lm-format-enforcer](https://github.com/noamgat/lm-format-enforcer)
- [outlines]()

## 🚀 Using llama.cpp grammar to enforce a specified format for LLMs output