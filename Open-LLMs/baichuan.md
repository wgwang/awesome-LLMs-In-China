# baichuan

baichuan，应该是“百川”的拼音，目前开放的是7B 的模型baichuan-7B。

baichuan-7B 是由百川智能开发的一个开源非商用的大规模预训练语言模型，如果商用需要联系获得单独的许可。

baichuan-7B基于 Transformer 结构，在大约1.2万亿 tokens 上训练的70亿参数模型，支持中英双语，上下文窗口长度为4096。

在多个数据集的评估中，在7B（6B）规模的模型中，baichuan-7B成绩排在第一。比如，在高考数据集中.


## 基础信息

- 由百川智能开发和发布
- baichuan-7B发布于2023年6月15日
- baichuan-7B是基于变换器网络（Transformer）架构，7B参数
- 许可：非商业定制许可证
  - 代码许可：Apache License 2.0，允许商用，相比GPL更宽松。
  - 模型许可：[baichuan-7B模型许可协议](https://huggingface.co/baichuan-inc/baichuan-7B/resolve/main/baichuan-7B%20%E6%A8%A1%E5%9E%8B%E8%AE%B8%E5%8F%AF%E5%8D%8F%E8%AE%AE.pdf) 非商业用途可直接使用，商用的话需联系邮箱“opensource@baichuan-inc.com”以获得授权。
  - 模型许可协议目前仅提供中文版本。



## 资料集合
[代码仓库：Github](https://github.com/baichuan-inc/baichuan-7B)
[模型仓库：HuggingFace](https://huggingface.co/baichuan-inc/baichuan-7B)
[模型仓库：modelscope](https://modelscope.cn/models/baichuan-inc/baichuan-7B/)



## 参数
|params|dimension|n heads|n layers| n tokens|
|:-|:-|:-|:-|:-|
|7B |4096| 32|32|1.2T|


|名称|baichuan-7B|
|:-|:-|
|参数规模params| 7B|
|隐变量维度dimension|4096|
|自注意力头的个数n heads|32|
|层数n layers|32|
|词表大小Vocab size|64,000|
|输入序列长度sequence length|4096|
|数据规模词元数量n tokens|1.2T|
|训练时长Training GPU-hours||


## 模型下载

[模型仓库：HuggingFace](https://huggingface.co/baichuan-inc/baichuan-7B)
[模型仓库：modelscope](https://modelscope.cn/models/baichuan-inc/baichuan-7B/)



## 训练数据

1.2T Tokens，没有其他明确的数据分布情况说明。

原始数据包括开源的中英文数据和自行抓取的中文互联网数据，以及部分高质量知识性数据。


以下是收集的非官方信息：

有网友实验了模型，提到可能用了百度知道的数据
