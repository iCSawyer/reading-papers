# On Multi-Modal Learning of Editing Source Code

> Source: ASE-2021
>
> Tag: multi-modal, neural machine learning, code editing

### Abstract

+ Neural Machine Translator用于编辑代码表现很好，其输入是要更改的代码，输出是补丁列表

+ 本文使用的三种模态：编辑位置、编辑代码上下文、提交信息

+ 开发者的hint可以缩小补丁搜索空间

### Ⅰ Introduction

+ 提出了一种基于三种信息模式的多模态代码编辑引擎：需要编辑的代码片段、自然语言表示的开发者意图和显式的编辑上下文
+ 以前的工作往往将上下文和编辑位置统一作为代码元素，而不是两种单独的模态

+ 使用基于transformer的已经训练过的模型PLBART来初始化参数
+ 开发者的guidance可以缩小change pattern的搜索空间
+ 用一个encoder编码所有modal，比每个modal用单独的encoder编码学习效果好

+ 论文的总结贡献

  ① 提出多模态自动代码编辑工具MODIT，通过context和guidence

  ② 关于modal的作用、encoder/decoder的变化给了一些经验教训

### Ⅱ Background

1. 神经机器翻译：encoder-decoder，将句子从一种语言翻译到另一种语言

2. 用Transformer进行序列处理

   2.1 不同于传统RNN模型token顺序处理，Transformer假定序列中的每一对token有soft-dependency【？】

   2.2 dependency权重通过attention机制进行学习

3. 源代码的迁移学习

   3.1 迁移学习：学习源代码不可知表示并重用

   3.2 目标：通过大量源代码预先训练，期望理解或生成代码

### Ⅲ MODIT

（尽管edit location属于context，但仍然作为不同模式处理）

1. 预处理

   token-subtoken【？】

2. Encoder-Decoder模型【？】

   2.1 编码器：多模态统一编码和表示

   2.2 解码器：self-attention和cross-attention【？】

3. 输出生成

### Ⅳ Experiment Design

数据集、数据准备（模式如何提取的...）、训练、评价标准（top-1 accuracy）

### Ⅴ Empirical Results

1. MODIT准确度如何

   1.1 guidance缩小pattern搜索空间，context缩小token搜索空间

   1.2 Transformer无需监督也可学习；用预训练模型初始化参数效果明显更好

2. 不同模态的作用

   2.1 每个模态都有用，缺失任何一个都会导致性能下降（尽管待编辑代码属于上下文的一个部分）

   2.2 显式的上下文可以让模型选择合适的标识符

   2.3 隔离有缺陷的代码后性能更好

3. encoder和decoder不同带来的改变

   3.1 单一encoder学习所有modal效果更好

   3.2 通过基于attention的跨模态推理，代码表示更鲁棒

### Ⅵ Discussion

1. 编辑位置

+ 假设：不知道编辑位置，将整个函数输入，期待MODIT输出整个函数

+ 结果：有开发者的guidance仍然可以提高性能

2. 源代码的tokenization：本文用subword（其他各种分词法【？】）

### Ⅸ Conclusion

1. 多模态很有用：location、context、guidance

2. 给了一些关于模态、encoder/decoder改变等带来的影响
