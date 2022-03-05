# Attention is All You Need

> Source: NeurIPS-2017
>
> Tag: machine translation, attention
>
> 

## Abstract

1. 提出新的简单模型，仅使用了注意力机制，完全没有使用循环和卷积神经网络（Recurrence NN & Convolution NN ）
2. **机器翻译**任务中表现良好
3. 泛化到别的任务上也有良好的效果

## Conclusion (7)

1. 第一个仅使用注意力机制的序列转录模型，将循环层替换为multi-headed self-attention
2. 训练速度更快，效果更好
3. 应用范围不局限于文本，图片、音频、视频等都可以试试

## Introduction (1)

+ 当前（2017年），机器翻译常用循环语言模型和encoder-decoder模型
+ RNN的特点：从左到右，每一个当前的状态信息，由前一个状态和当前单词共同决定，来有效学习历史信息
  + 问题1：从左到右按时序完成，无法并行
  + 问题2：历史信息一步一步传递，隐藏层的历史信息无法全部保存（或造成大量历史开销）
+ 注意力机制以前和RNN一起使用，用于怎么将信息有效从encoder传递到decoder
+ Transformer使用纯attention机制做encoder-decoder

## Background (2)

+ CNN
  + 缺点：难以对长序列建模（一层一层向上卷积）
  + 优点：可以做多输出通道（因此，attention变为multi-head attention模拟多输出通道）
+ 自注意力机制

## Model Architecture

1. encoder-decoder模型介绍

   1. encoder：输入序列(x1, ..., xn)编码为序列表示(z1, ..., zn)（每个z都是一个向量）

      例如，如果输入的是一个句子(x1, x2, x3)，编码后的z1表示第一个单词的向量

   2. decoder：获得(z1, ..., z**n**)，生成(y1, ..., y**m**)

      编码器一般可以看完整个句子；解码器是一个一个生成的，每一步都是一个自回归（过去时刻的输出，也是当前的输入）

2. Transformer encoder

   每个层都有两个子层：multi-head attention和MLP（多层感知机）；子层都有残差连接；layer-norm

   每个层的向量表示都是固定的。

> 文章中提到的归一化方法：layer-norm和batch-norm
> + batch-norm
>   + 每一行是样本（batch），每一列是特征（feature）
>   + 使每一列（feature）均值为0、方差为1（减均值、除方差）
>   + 有参数λ和β，可以使这一列的均值和方差
> + layer-norm
>   + 使每一行（batch）均值为0、方差为1
>   + 在transformer中，因为每一个样本都是一个向量，因此输入就是二维（batch、seq），再算上特征，就是三维了。（想象一张纸，垂直放在）因为每个样本都是一个向量（上面提到的z），所以是3D的，分别为每个样本batch、样本中每个词对应的向量seq，还有每个词的特征feat

​			2.decoder

​				解码器的子层有3个，还有一个多头注意力机制；自回归；带掩码的多头注意力			机制（t时刻不会看到t之后的输入）



add：残差连接；norm：归一化

3. Attention

   不同的相似函数决定了不同的注意力的版本

   如果query与某个key更相似，最后用所有的value表示的输出中，那个和query更接近的key对应的value权重就会更大；而key-value-query本身并没有改变

### Others

sequence transduction model：seq2seq

recurrent/convolutional neural network：循环/卷积 神经网络

BLEU Score：语言模型打分

Background/Related Work：论文写作中，主要讲述相关论文、和它们联系是什么、区别是什么

### Reference

+ [李沐-Transformer论文逐段精读](https://www.bilibili.com/video/BV1pu411o7BE?from=search&seid=7927089393081921368&spm_id_from=333.337.0.0)

