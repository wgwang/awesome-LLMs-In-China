# Falcon

摘要：TII开放出来的Falcon-180B大模型，进一步引发了开源开放大模型的激烈竞争。从已发布的信息看，Falcon-180B在各项指标上都超越了LLaMA-2。另外，Falcon-180B同时发布了基础模型和在基础模型之上进行有监督微调SFT和人类反馈的强化学习RLHF进行训练的Chat模型。


## 概述

Falcon-180B是一个拥有1800亿参数的因果解码器模型（自回归语言模型），由阿布扎比（Abu Dhabi）的技术创新研究院（TII）开发和训练，于2023年9月发布。它是继Falcon-40B之后，TII推出的第二个开源大语言模型（LLM），也是目前世界上最大的开源开放大模型。Falcon-180B的目标是为研究者和商业用户提供一个强大、高效、多语言和多领域的基础模型，可以用于各种自然语言处理（NLP）任务，如文本生成、摘要、问答、对话、机器翻译等。

Falcon 原始的意思是“猎鹰【A falcon is a bird of prey that can be trained to hunt other birds and animals. 】”。

Falcon 系列模型到目前发布了7B、40B 和180B 三个模型。Falcon-180B 模型是目前开源开放大模型中，参数规模最大的。所使用的训练词元（tokens）数量达3.5T，也是已发布的大模型中最多的。

Falcon-180B是一个基础模型，TII开放了两个版本，一个是纯无监督训练出来的基础模型Falcon-180B，另一个是在基础模型之上进行有监督微调SFT和人类反馈的强化学习RLHF进行训练的Chat模型Falcon-180B-chat。


## 基础信息


- 由TII开发和发布
- 发布于2023年9月6日，模型实际上传到 HuggingFace 的日期更早一些（8月29日）
- 数据集为RefinedWeb，压缩包约500GB，解压后2.8TB，用于训练 Falcon-180B 模型的词元数量为3.5T；
- Falcon是一种基于变换器网络（Transformer）架构的自回归语言模型/因果解码器模型。Falcon模型除了180B的之外，此前已经发布了1B、7B、40B参数的模型。
- 许可：允许商用，但如果要以托管形式（Hosting Use，大概是类似 OpenAI 的 API 或云服务商）商用的话，需要单独申请【不构成法律层面的建议，如果商用请自行判断或咨询专业的律师】
- 训练成本，约为 LLaMA-2-70B 的4倍，估计超过8000万美元（鉴于A800价格远超A100，且带宽被砍，国内的话估计要8亿人民币左右）
- Falcon-180B效果上表现很不错，在 MMLU 表现上超越了 LLaMA-2-70B、ChatGPT-3.5；在多个数据集【HellaSwag、LAMBADA、WebQuestions、Winogrande、PIQA、ARC、BoolQ、CB、COPA、RTE、WiC、WSC、ReCoRD 】上与谷歌的 PaLM 2-Large 不相上下
- 使用Falcon-180B的硬件要求非常高，Int8量化后的模型，需要320GB的显存（4块80G显存的A100/A800/H100/H800）
- 实际使用的话，还是使用LLaMA-2-70B吧，这是由于Falcon-180B 的效果仅略微超越了LLaMA-2-70B，但计算资源需要3倍以上，性价比不高，而且商业授权方面LLaMA-2更宽松
  

## 资料集合

[发布文章](https://huggingface.co/blog/zh/falcon-180b)
[基础模型](https://hf.co/tiiuae/falcon-180B)
[Chat模型](https://hf.co/tiiuae/falcon-180B-chat)

## 参数

|名称|Falcon-180B|Falcon-40B|Falcon-7B|
|:-|:-|:-|:-|
|参数规模params|180B|40B|7B|
|隐变量维度dimension|14848|8192|4544|
|自注意力头的个数n heads|64|64|64|
|层数n layers|80|60|32|
|词表大小Vocab size|65024|65024|65024|
|输入序列长度sequence length|2048|2048|2048|
|数据规模词元数量n tokens|3.5T|1.0T|1.5T|
|训练时长Training GPU-hours(A100)|7000000|552960|129024|

## 训练模型的算力设施

### falcon-180B
- AWS SageMaker
- 180B Falcon 模型
- 处理速度： tokens/sec/GPU
- 4096个A100-80GB，P4d instances
- 训练时间：从2023年初开始至今
- 自定义的分布式训练库Gigatron，使用了3D parallelism approach，DeepSpeed ZeRO和Triton(FlashAttention等)

### falcon-40B
- 384 A100 40GB GPUs
- 3D parallelism strategy (TP=8, PP=4, DP=12) combined with ZeRO
- 2022年12月开始训练，费时2个月，约552960小时GPU（384x60x24）

### falcon-7B
- 384 A100 40GB GPUs
- 2D parallelism strategy (PP=2, DP=192) combined with ZeRO
- 2023年3月初开始，费时两周，约129024小时GPU（384x14x24）



## 模型下载
- [Falcon-180B](https://huggingface.co/tiiuae/falcon-180B)
- [Falcon-180B-chat](https://huggingface.co/tiiuae/falcon-180B-chat)
- [Falcon-40B](https://huggingface.co/tiiuae/falcon-40b)
- [Falcon-40B-Instruct](https://huggingface.co/tiiuae/falcon-40b-instruct)
- [Falcon-7B](https://huggingface.co/tiiuae/falcon-7b)
- [Falcon-7B-Instruct](https://huggingface.co/tiiuae/falcon-7b-instruct)


### 授权

- Falcon-180B 可商用，但如用于 Hosting Use（托管使用）xu 单独申请授权。听起来主要避免以服务的形势商用，但如果把模型和应用打包出售，模型本身不收费，那是可以的。[使用协议](https://huggingface.co/spaces/tiiuae/falcon-180b-license/blob/main/LICENSE.txt)
- Falcon-40B和Falcon-7B使用了Apache 2.0 license授权模式，可商用。
- 不构成法律建议


## 效果方面

Falcon-180B效果上表现很不错，在 MMLU 表现上超越了 LLaMA-2-70B、ChatGPT-3.5；在多个数据集【HellaSwag、LAMBADA、WebQuestions、Winogrande、PIQA、ARC、BoolQ、CB、COPA、RTE、WiC、WSC、ReCoRD 】上与谷歌的 PaLM 2-Large 不相上下。

技术报告或论文尚未发布，详细内容后续更新

## 训练数据

- 使用TII 发布的[RefinedWeb](https://huggingface.co/datasets/tiiuae/falcon-refinedweb)数据集


下面数据分布来自huggingface 仓库说明，但数据总量并不是3.5T。代技术报告或论文出来后再更新。

|数据集|比例|词元数量|来源|
|:-|:-|:-|:-|
|[RefinedWeb-English](https://huggingface.co/datasets/tiiuae/falcon-refinedweb)|75%|750B|	massive web crawl|
|RefinedWeb-Europe|7%|70B|European massive web crawl|
|Books|6%|60B||
|Conversations|5%|50B|Reddit, StackOverflow, HackerNews|
|Code|5%|50B||
|Technical|2%|20B|arXiv, PubMed, USPTO, etc.|

RefinedWeb-Europe的语言分布如下：

|语言|比例|	词元数量|
|:-|:-|:-|
|German|26%|18B|
|Spanish|24%|17B|
|French|23%|16B|
|Italian|7%|5B|
|Portuguese|4%|3B|
|Polish|4%|3B|
|Dutch|4%|3B|
|Romanian|3%|2B|
|Czech|3%|2B|
|Swedish|2%|1B|


## 模型架构

- 自回归语言模型，也称因果语言模型（causal decoder-only model）
- 基于[GPT-3](https://arxiv.org/abs/2005.14165)
- 使用了[RoPE: Rotary Positionnal embeddings](https://arxiv.org/abs/2104.09864)
- 使用了[Multi-Query Attention](https://arxiv.org/abs/1911.02150) 和 [FlashAttention](https://arxiv.org/abs/2205.14135)


