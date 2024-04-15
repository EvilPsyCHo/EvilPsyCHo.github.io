---
title: Using-llamacpp-grammar-to-Constrain-LLMs-output-format
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

`Llamacpp grammar` is based on a specific set of syntax, but we don't need to learn it, there is a simple way to do this 😆.
1. Define the data structure with `TypeScript`
2. Goto [intrinsiclabs](https://grammar.intrinsiclabs.ai/) and translate `TypeScript` to `Llamacpp grammar`

![](../images/post_constrain_llms_output_format/translator.png)

For example, if our desired output format like this:
```json
{
  "game_state": string, # "game over" 或 "game on progress",
  "message": string,
  "active_player": string,
}
```

First, define data struction with `TypeScript`:

```typescript
interface DM {
  game_state: GameState;
  active_player: string;
  message: string;
}

enum GameState {
  GameOver = "game over",
  GameOnProgress = "game on progress",
}
```

Then, translate it to `llamacpp grammar`:

```grammar
root ::= DM
GameState ::= "\"game over\"" | "\"game on progress\""
DM ::= "{"   ws   "\"game_state\":"   ws   GameState   ","   ws   "\"active_player\":"   ws   string   ","   ws   "\"message\":"   ws   string   "}"
DMlist ::= "[]" | "["   ws   DM   (","   ws   DM)*   "]"
string ::= "\""   ([^"]*)   "\""
boolean ::= "true" | "false"
ws ::= [ \t\n]*
number ::= [0-9]+   "."?   [0-9]*
stringlist ::= "["   ws   "]" | "["   ws   string   (","   ws   string)*   ws   "]"
numberlist ::= "["   ws   "]" | "["   ws   string   (","   ws   number)*   ws   "]"

```

Finnally, we can use this 

