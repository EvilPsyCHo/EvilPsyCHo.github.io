---
title: Using llamacpp grammar and pydantic to Constrain LLMs output format
layout: post
hide_header: true
---

Due to the limitation in training dataset and model parameter scale, most the open source LLMs suck as Llama2, Mistral, Baichuan2, etc., are unable to support features like `function call` or output specified format as effectively as GPT-4.

Based on the modifications to the sampling rules ultilizing token probability predicted by LLMs, we can solve this perfectly. For example, when numerical outputs are required, the sample probabilities of non-numerical are suppressed, achieving the desired output. This can be a transitional approach in response to the insufficient capabilities of open source LLMs. Here are some project related to this purpose:
- [llamacpp grammar](https://github.com/ggerganov/llama.cpp/blob/master/grammars/README.md)，灵活度中等，劣势是只支持llamacpp后端 
- [guidance](https://github.com/guidance-ai/guidance)更加灵活，支持llamacpp/hf transformers后端，缺点是不稳定
- [localai](https://localai.io/features/openai-functions)是对llamacpp grammar 的封装
- [functionary](https://github.com/MeetKai/functionary)只支持很少的模型
- [https://github.com/1rgs/jsonformer](jsonformer)
- [lm-format-enforcer](https://github.com/noamgat/lm-format-enforcer)，活跃项目，支持vllm/llamacpp 
- [outlines]()