+++
title = "llm"
author = ["PENG Kevin"]
draft = false
+++

## 环境搭建 {#环境搭建}

python 安装

```python
pip3 install transformers
pip3 install pytorch
pip3 install accelerate
```

model 下载
个人 PC 上暂时跑不了太大的模型

chat
: <https://huggingface.co/Qwen/Qwen2-0.5B-Instruct>


## 运行 {#运行}

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
device = "cuda" # the device to load the model onto

model = AutoModelForCausalLM.from_pretrained(
    "Qwen2-0.5B-Instruct",
    torch_dtype="auto",
    device_map="auto"
)
tokenizer = AutoTokenizer.from_pretrained("Qwen2-0.5B-Instruct")

prompt = "用 C 语言写一个冒泡排序的算法"
messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": prompt}
]
text = tokenizer.apply_chat_template(
    messages,
    tokenize=False,
    add_generation_prompt=True
)
model_inputs = tokenizer([text], return_tensors="pt").to(device)

generated_ids = model.generate(
    model_inputs.input_ids,
    max_new_tokens=512
)
generated_ids = [
    output_ids[len(input_ids):] for input_ids, output_ids in zip(model_inputs.input_ids, generated_ids)
]

response = tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]

print(str(response))

```
