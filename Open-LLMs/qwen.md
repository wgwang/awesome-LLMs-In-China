# 千问

摘要：阿里云开放出来的通义千问大模型，技术报告很长，但除了宣称模型很牛之外，没啥有价值的信息！目前已开放7B 和14B两个版本的模型，分别由2.4T词元和3.0T词元训练出来的大语言模型。

## 基础信息

- 由阿里云团队开发
- 14B模型发布于2023年9月25日, 7B模型发布于2023年8月3日
- 许可：允许商用，页面介绍说商用需申请，但在 LICENSE 中，仅要求超过1亿用户的机构才需要申请【If you are commercially using the Materials, and your product or service has more than 100 million monthly active users, You shall request a license from Us. You cannot exercise your rights under this Agreement without our express authorization.】。同时，LICENSE没有中文版本，这很神奇！【注：本条内容不构成法律建议】
- 7B和14B 两种参数规模的自回归语言模型
- 7B用了2.4T词元训练，14B用了3.0T词元训练


## 资料集合

[代码仓库](https://github.com/QwenLM/Qwen)
[技术报告](https://qianwen-res.oss-cn-beijing.aliyuncs.com/QWEN_TECHNICAL_REPORT.pdf)
[modelscope仓库](https://modelscope.cn/organization/qwen) 和 [HuggingFace仓库](https://huggingface.co/Qwen)


关于技术报告，再吐槽一下，真的很长但没啥价值，除了宣称自己很牛之外，关键内容一概没有！


## 参数

|名称|Qwen-14B|QWen-7B|
|:-|:-|:-|
|隐变量维度dimension|5120|4096|
|自注意力头的个数n heads|40|32|
|层数n layers|40|32|
|词表大小Vocab size|152000|152000|
|输入序列长度sequence length|2048|2048|
|数据规模词元数量n tokens|3.0T|2.4T|
|训练时长Training GPU-hours(A100)|||

## 训练模型的算力设施

无披露

## 模型下载


|参数规模|Qwen-Chat |Qwen-Chat (Int4)| Qwen|
|----|:---:|:------:|:-----:|
| 7B |  <a href="https://modelscope.cn/models/qwen/Qwen-7B-Chat/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-7B-Chat">HuggingFace</a>  |  <a href="https://modelscope.cn/models/qwen/Qwen-7B-Chat-Int4/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-7B-Chat-Int4">HuggingFace</a>  |  <a href="https://modelscope.cn/models/qwen/Qwen-7B/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-7B">HuggingFace</a>  |
| 14B | <a href="https://modelscope.cn/models/qwen/Qwen-14B-Chat/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-14B-Chat">HuggingFace</a> | <a href="https://modelscope.cn/models/qwen/Qwen-14B-Chat-Int4/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-14B-Chat-Int4">HuggingFace</a> | <a href="https://modelscope.cn/models/qwen/Qwen-14B/summary">ModelScope <a>  <a href="https://huggingface.co/Qwen/Qwen-14B">HuggingFace</a> |


## 效果方面

很多，整个技术报告就这部分内容最丰富了，有兴趣的自行阅读技术报告


## 训练数据

7B 的用了2.4T 词元的数据；14B 的用了3.0T词元的数据。没有披露其他信息。


## 模型架构
- 使用了RoPE
- 使用了RMSNorm
- 激活函数使用了SwiGLU
- FFN的维度降低了【Reduced the dimension of the feed-forward network (FFN) from 4 times the hidden size to 8/3 of the hidden size.】

  