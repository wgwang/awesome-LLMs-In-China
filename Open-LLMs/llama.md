# LLaMA

Llama 原始的意思是“美洲驼【A llama is a South American animal with thick hair, which looks like a small camel without a hump.】”，也因此，许多基于 LLaMA的模型都以动物名称来命名。

Meta 开发并“开放”的LLaMA大模型，是ChatGPT 出现之后第一个真正意义上的大语言模型，与此前的OPT、GALACTICA、BLOOM等大语言模型有了较大进步。

LLaMA是一个基础模型，可以针对各种任务进行微调，如文本生成、问答、摘要等。也是在 LLaMA 发布之后，开源大语言模型才有了长足的进展，各种 SFT、RLHF 以及基于 LLaMA 的LoRA 等大量出现。也正是基于LLaMA，才有了一大批农场中的动物系列模型出现。

Meta在论文中表示，LLaMA 13B在大多数基准测试中都优于OpenAI流行的GPT-3模型，而LLaMA 65B与DeepMind的Chinchilla70B和谷歌的PaLM 540B等最好的模型有的一比。这其实得益于 Meta 用了比之前那些模型更多的语料来训练LLaMA。


## 基础信息

- 由Meta AI的FAIR团队开发
- LLaMA是在2022年12月份到2023年2月份之间训练的
- LLaMA是一种基于变换器网络（Transformer）架构的自回归语言模型。该模型有不同的参数规模：7B、13B、33B(通常称30B) 和 65B 参数
- 许可：非商业定制许可证
  - 代码许可：GPL v3（GNU General Public License v3.0）允许使用、修改和分发代码，但必须开源；允许收维护费，但不允许收授权费等。
  - 模型许可：[LLaMA LICENSE AGREEMENT](https://docs.google.com/forms/d/e/1FAIpQLSfqNECQnMkycAp2jP4Z9TFX0cGR4uf7b_fBxjY_OjhJILlKGA/viewform) 其中明确说明不允许商业目的使用。




## 资料集合
[代码仓库](https://github.com/facebookresearch/llama)
[论文](https://arxiv.org/pdf/2302.13971.pdf)

## 参数
|params|dimension|n heads|n layers| learning rate| batch size| n tokens|Training GPU-hours|
|:-|:-|:-|:-|:-|:-|:-|:-|
|6.7B |4096| 32|32|3.0e−4|4M|1.0T|82,432|
|13.0B|5120| 40|40|3.0e−4|4M|1.0T|135,168|
|32.5B|6656| 52|60|1.5e−4|4M|1.4T|530,432|
|65.2B|8192| 64|80|1.5e−4|4M|1.4T|1,022,362|



|名称|LLaMA-65B|LLaMA-33B|LLaMA-13B|LLaMA-7B|
|:-|:-|:-|:-|:-|
|参数规模params|65.2B|32.5B|13.0B|6.7B|
|隐变量维度dimension|8192|6656|5120|4096|
|自注意力头的个数n heads|64|52|40|32|
|层数n layers|80|60|40|32|
|词表大小Vocab size|32000|32000|32000|32000|
|输入序列长度sequence length|2048|2048|2048|2048|
|数据规模词元数量n tokens|1.4T|1.4T|1.0T|1.0T|
|训练时长Training GPU-hours|1,022,362（A100）|530,432|135,168|82,432|

## 训练模型的算力设施

- 65B LLaMA 模型
- 处理速度：380 tokens/sec/GPU
- 2048个A100-80GB
- 训练时长：20.8天

## 模型下载

 - 官方下载：填写[表单](https://docs.google.com/forms/d/e/1FAIpQLSfqNECQnMkycAp2jP4Z9TFX0cGR4uf7b_fBxjY_OjhJILlKGA/viewform)提交申请

- 非官方下载
  - P2P 下载：[magnet:?xt=urn:btih:ZXXDAUWYLRUXXBHUYEMS6Q5CE5WA3LVA&dn=LLaMA](magnet:?xt=urn:btih:ZXXDAUWYLRUXXBHUYEMS6Q5CE5WA3LVA&dn=LLaMA)
  - Hugging Face [LLaMA-65B](https://huggingface.co/datasets/nyanko7/LLaMA-65B) [LLaMA-65B](https://huggingface.co/huggyllama/llama-65b) [LLaMA-30B](https://huggingface.co/huggyllama/llama-30b) [LLaMA-13B](https://huggingface.co/huggyllama/llama-13b) [LLaMA-7B](https://huggingface.co/huggyllama/llama-7b)


## 训练数据

指1.4T Tokens的版本

|Dataset|Sampling prop.|Epochs|Disk size|
|:-|:-|:-|:-|
|CommonCrawl   |67.0% |1.10| 3.3| TB|
|C4            |15.0% |1.06| 783| GB|
|Github        |4.5%  |0.64| 328| GB|
|Wikipedia     |4.5%  |2.45| 83 | GB|
|Books         |4.5%  |2.23| 85 | GB|
|ArXiv         |2.5%  |1.06| 92 | GB|
|StackExchange |2.0%  |1.03| 78 | GB|


## 模型架构



- LayerNorm使用了[RMSNorm](https://arxiv.org/pdf/1910.07467.pdf)，并且通过对每个transformer子层的输入进行归一化，而不是对输出进行归一化。

- 激活函数使用了[SwiGLU](https://arxiv.org/pdf/2002.05202.pdf)代替ReLU，这点和PaLM模型一样

- 位置编码使用了[rotary嵌入RoPE【RoFormer: Enhanced transformer with rotary position embedding】](https://arxiv.org/pdf/2104.09864.pdf)，这点和GPTNeo一样

- 在自注意力机制的实现上，由于自回归语言模型的特性，使用了causal multi-head attention，并使用了[xformers](https://github.com/facebookresearch/xformers)的实现方法。这个自注意力机制的理论来自于两篇论文[SELF-ATTENTION DOES NOT NEED $O(n^2)$ MEMORY](https://arxiv.org/pdf/2205.14135.pdf)和[FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness](https://arxiv.org/pdf/2205.14135.pdf)。
