# LLaMA-2

摘要：Meta开放出来的LLaMA-2引起了人工智能领域的极大震撼！本文从全局角度概览LLaMA-2，包括基础模型和在基础模型之上进行有监督微调SFT和人类反馈的强化学习RLHF进行训练的模型，每类皆包含7B、13B和70B三个版本。


Llama 原始的意思是“美洲驼【A llama is a South American animal with thick hair, which looks like a small camel without a hump.】”，也因此，许多基于 LLaMA的模型都以动物名称来命名。

Meta 开发并“开放”的LLaMA-2大模型，是其此前发布的大模型LLaMA的升级迭代版本，是一个巨大进步的版本。

LLaMA-2是一个基础模型，Meta开放了两个版本，一个是纯无监督训练出来的基础模型，另一个是在基础模型之上进行有监督微调SFT和人类反馈的强化学习RLHF进行训练的Chat模型。所发布的两个版本中，都提供了7B、13B 和70B的三个参数规模的模型。


## 基础信息

- 由Meta AI的GenAI团队开发
- 发布于2023年7月18日
- LLaMA-2无监督训练数据截至2022年9月；有监督微调的数据截至2023年7月；
- LLaMA是一种基于变换器网络（Transformer）架构的自回归语言模型。该模型有不同的参数规模：7B、13B、70B参数
- 许可：允许商用，非常的宽松，但如果使用方及其关联公司所提供的产品或服务的月活跃用户超过7亿的话，需要向Meta请求许可，而Meta可以自行决定是否授权。【 If, on the Llama 2 version release date, the monthly active users of the products or services made available by or for Licensee, or Licensee’s affiliates, is greater than 700 million monthly active users in the preceding calendar month, you must request a license from Meta, which Meta may grant to you in its sole discretion, and you are not authorized to exercise any of the rights under this Agreement unless or until Meta otherwise expressly grants you such rights.】
- 训练成本，估计超过2000万美元（鉴于A800价格远超A100，且带宽被砍，国内的话估计要2亿人民币左右）
  


## 资料集合

[代码仓库](https://github.com/facebookresearch/llama)
[论文](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/)
[模型](https://huggingface.co/meta-llama)

## 参数

|名称|LLaMA2-70B|LLaMA-34B|LLaMA-13B|LLaMA-7B|
|:-|:-|:-|:-|:-|
|参数规模params|70B|34B|13B|7B|
|隐变量维度dimension|8192|6656|5120|4096|
|自注意力头的个数n heads|64|52|40|32|
|层数n layers|80|60|40|32|
|词表大小Vocab size|32000|32000|32000|32000|
|输入序列长度sequence length|4096|4096|4096|4096|
|数据规模词元数量n tokens|2.0T|2.0T|2.0T|2.0T|
|训练时长Training GPU-hours(A100)|1720320|1038336|368640|184320|

## 训练模型的算力设施

- Meta’s Research Super Cluster，
- 70B LLaMA 模型
- 处理速度：320 tokens/sec/GPU
- 2000个A100-80GB
- 训练时间：从2023年1月到2023年7月

## 模型下载
- 官方下载： [HuggingFace](https://huggingface.co/meta-llama)，需提交授权申请，基本都会批准的。
- 非官方： [HuggingFace](https://huggingface.co/TheBloke) 

### 官方

|参数规模|LLaMA-2|LLaMA-2-hf|LLaMA-2-Chat|LLaMA-2-Chat-hf|
|:-|:-|:-|:-|:-|
|7B|[下载链接](https://huggingface.co/llamaste/Llama-2-7b)|[下载链接](https://huggingface.co/llamaste/Llama-2-7b-hf)|[下载链接](https://huggingface.co/llamaste/Llama-2-7b-chat)|[下载链接](https://huggingface.co/llamaste/Llama-2-7b-chat-hf)|
|13B|[下载链接](https://huggingface.co/llamaste/Llama-2-13b)|[下载链接](https://huggingface.co/llamaste/Llama-2-13b-hf)|[下载链接](https://huggingface.co/llamaste/Llama-2-13b-chat)|[下载链接](https://huggingface.co/llamaste/Llama-2-13b-chat-hf)|
|70B|[下载链接](https://huggingface.co/llamaste/Llama-2-70b)|[下载链接](https://huggingface.co/llamaste/Llama-2-70b-hf)|[下载链接](https://huggingface.co/llamaste/Llama-2-70b-chat)|[下载链接](https://huggingface.co/llamaste/Llama-2-70b-chat-hf)|

### 其他

70B的模型下载，有几种不同的变种，支持不同的框架载入：
- [LLaMA-2-70B-GGML](https://huggingface.co/TheBloke/Llama-2-70B-GGML)
- [LLaMA-2-70B-Chat-GGML](https://huggingface.co/TheBloke/Llama-2-70B-Chat-GGML)
- [LLaMA-2-70B-GPTQ](https://huggingface.co/TheBloke/Llama-2-70B-GPTQ)
- [LLaMA-2-70B-chat-GPTQ](https://huggingface.co/TheBloke/Llama-2-70B-chat-GPTQ)


## 效果方面

Meta在论文中表示，LLaMA 70B的模型在许多方面都超越了 ChatGPT-3.5的水平。在一些第三方的评测中【[HuggingFace LeaderBoard](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard)】不错。
- AI2 Reasoning Challenge (25-shot) - a set of grade-school science questions.
  - Llama 1 (llama-65b): 57.6
  - LLama 2 (llama-2-70b-chat-hf): 64.6
  - GPT-3.5: 85.2
  - GPT-4: 96.3

- HellaSwag (10-shot) - a test of commonsense inference, which is easy for humans (~95%) but challenging for SOTA models.
  - Llama 1: 84.3
  - LLama 2: 85.9
  - GPT-3.5: 85.3
  - GPT-4: 95.3

- MMLU (5-shot) - a test to measure a text model’s multitask accuracy. The test covers 57 tasks including elementary mathematics, US history, computer science, law, and more.
  - Llama 1: 63.4
  - LLama 2: 63.9
  - GPT-3.5: 70.0
  - GPT-4: 86.4

- TruthfulQA (0-shot) - a test to measure a model’s propensity to reproduce falsehoods commonly found online. Note: TruthfulQA in the Harness is actually a minima a 6-shots task, as it is prepended by 6 examples systematically, even when launched using 0 for the number of few-shot examples.
  - Llama 1: 43.0
  - LLama 2: 52.8
  - GPT-3.5: 47.0
  - GPT-4: 59.0

## 训练数据

指2T Tokens的公开数据，未详细披露数据情况。

在RLHF训练中，Meta 使用了141万条对比数据加上公开能够获取的数据集一起来训练奖励模型。

LLaMA-2无监督训练数据截至2022年9月；有监督微调的数据截至2023年7月；



## 模型架构

与LLaMA类似，但做了些许修改。LLaMA 的模型架构参阅[LLaMA](llama.md)

- Context Length从2048增加到4096
- 在多头注意力中使用了[GQA](https://arxiv.org/pdf/2305.13245.pdf)
  
  

