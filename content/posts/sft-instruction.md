---
title: "Supervised finetuning of instruction-following LLMs"
date: 2023-11-13
katex: true
markup: "mmark"
---

# Supervised finetuning of instruction-following Large Language Models (LLMs)

---

This blog post corresponds to the README from [here](https://github.com/daniel-furman/sft-demos).

---

This repo contains demos for supervised finetuning (sft) of large language models, like Meta's [llama-2](https://huggingface.co/meta-llama/Llama-2-7b-hf). In particular, we focus on tuning for short-form instruction following capabilities.

## Table of contents

1. [Background](https://github.com/daniel-furman/sft-demos#instruction-tuning-background)
2. [Finetuned models](https://github.com/daniel-furman/sft-demos#favorites-from-this-repo)
3. [Basic usage](https://github.com/daniel-furman/sft-demos#basic-usage)
4. [Base models and datasets](https://github.com/daniel-furman/sft-demos#base-models-and-datasets)


---

## Instruction-tuning background

The goal of instruction-tuning is to build LLMs that are capable of following natural language instructions to perform a wide range of tasks. The below was captured from the "[State of GPTs](https://www.youtube.com/watch?v=bZQun8Y4L2A)" talk by Andrej Karpathy. The key points illustrated for sft:

* Collect small but high-quality datasets in the form of prompt and ideal responses. 
* Do language modeling on this data, nothing changes algorithmically from pretraining. 
* After training we get an sft model which can be deployed as assistants (and it works to some extent).

![training_pipeline](https://raw.githubusercontent.com/daniel-furman/sft-demos/main/assets/assistant_training_pipeline.png)

For more background, see any number of excellent papers on the subject, including [Self-Instruct](https://arxiv.org/pdf/2212.10560.pdf) (2023), [Orca](https://arxiv.org/pdf/2306.02707.pdf) (2023), and [InstructGPT](https://arxiv.org/pdf/2203.02155.pdf) (2022). 

## Favorites from this repo

1. [dfurman/Llama-2-70B-Instruct-v0.1](https://huggingface.co/dfurman/Llama-2-70B-Instruct-v0.1)
    *  *Note*: This model was ranked 6th on 🤗's Open LLM Leaderboard in Aug 2023
2. [dfurman/Yi-6B-Instruct-v0.1](https://huggingface.co/dfurman/Yi-6B-Instruct-v0.1) 
3. [dfurman/Mistral-7B-Instruct-v0.1](https://huggingface.co/dfurman/Mistral-7B-Instruct-v0.1) 
4. [dfurman/Falcon-180B-Instruct-v0.1](https://huggingface.co/dfurman/Falcon-180B-Instruct-v0.1) 

## Basic usage

*Note*: Use the code below to get started with the sft models herein, as ran on 1x A100.  

**dfurman/Mistral-7B-Instruct-v0.1**

<details>

<summary>Setup</summary>

```python
!pip install -q -U transformers peft torch accelerate einops sentencepiece
```

```python
import torch
from peft import PeftModel, PeftConfig
from transformers import (
    AutoModelForCausalLM,
    AutoTokenizer,
)
```

```python
peft_model_id = "dfurman/Mistral-7B-Instruct-v0.1"
config = PeftConfig.from_pretrained(peft_model_id)

tokenizer = AutoTokenizer.from_pretrained(
    peft_model_id,
    use_fast=True,
    trust_remote_code=True,
)

model = AutoModelForCausalLM.from_pretrained(
    config.base_model_name_or_path,
    torch_dtype=torch.float16,
    device_map="auto",
    trust_remote_code=True,
)

model = PeftModel.from_pretrained(
    model, 
    peft_model_id
)
```

</details>


```python
messages = [
    {"role": "user", "content": "Tell me a recipe for a mai tai."},
]

print("\n\n*** Prompt:")
input_ids = tokenizer.apply_chat_template(
    messages,
    tokenize=True,
    return_tensors="pt",
)
print(tokenizer.decode(input_ids[0]))
```

<details>

<summary>Prompt</summary>

```python
"<s> [INST] Tell me a recipe for a mai tai. [/INST]"
```

</details>


```python
print("\n\n*** Generate:")
with torch.autocast("cuda", dtype=torch.bfloat16):
    output = model.generate(
        input_ids=input_ids.cuda(),
        max_new_tokens=1024,
        do_sample=True,
        temperature=0.7,
        return_dict_in_generate=True,
        eos_token_id=tokenizer.eos_token_id,
        pad_token_id=tokenizer.pad_token_id,
        repetition_penalty=1.2,
        no_repeat_ngram_size=5,
    )

response = tokenizer.decode(
    output["sequences"][0][len(input_ids[0]):], 
    skip_special_tokens=True
)
print(response)

```

<details>

<summary>Generation</summary>

```python
"""1 oz light rum
½ oz dark rum
¼ oz orange curaçao
2 oz pineapple juice
¾ oz lime juice
Dash of orgeat syrup (optional)
Splash of grenadine (for garnish, optional)
Lime wheel and cherry garnishes (optional)

Shake all ingredients except the splash of grenadine in a cocktail shaker over ice. Strain into an old-fashioned glass filled with fresh ice cubes. Gently pour the splash of grenadine down the side of the glass so that it sinks to the bottom. Add garnishes as desired."""
```

</details>

## Base models and datasets

We finetune off of the following base models in this repo:

* [yi](https://huggingface.co/01-ai)
* [mistral](https://huggingface.co/mistralai/Mistral-7B-v0.1)
* [llama-2](https://huggingface.co/meta-llama/Llama-2-70b-hf)
* [falcon](https://huggingface.co/tiiuae/falcon-180B)
* [mpt](https://huggingface.co/mosaicml/mpt-7b)

We use the following datasets in this repo:

* [ehartford/dolphin](https://huggingface.co/datasets/ehartford/dolphin)
* [jondurbin/airoboros-2.2.1](https://huggingface.co/datasets/jondurbin/airoboros-2.2.1)
* [garage-bAInd/Open-Platypus](https://huggingface.co/datasets/garage-bAInd/Open-Platypus)
* [timdettmers/openassistant-guanaco](https://huggingface.co/datasets/timdettmers/openassistant-guanaco)

---
