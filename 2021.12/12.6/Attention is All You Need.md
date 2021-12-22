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

## Conclusion（7）

1. 第一个仅使用注意力机制的序列转录模型，将循环层替换为multi-headed self-attention
2. 训练速度更快，效果更好
3. 应用范围不局限于文本，图片、音频、视频等都可以试试

## Introduction（1）

+ 当前（2017年），机器翻译常用循环语言模型和encoder-decoder模型
+ RNN的特点：从左到右，每一个当前的状态信息，由前一个状态和当前单词共同决定，来有效学习历史信息
  + 问题1：从左到右按时序完成，无法并行
  + 问题2：历史信息一步一步传递，隐藏层的历史信息无法全部保存（或造成大量历史开销）
+ 注意力机制以前和RNN一起使用，用于怎么讲信息有效从encoder传递到decoder
+ Transformer使用纯attention机制

## Background（2）

+ CNN：难以对长序列建模；可以做多输出通道（因此attention变为multi-head attention）
+ 自注意力机制

### Model Architecture

1. 传统encoder-decoder模型

   1. encoder：从输入序列(x1, ..., xn)，到序列表示(z1, ..., zn)（每个z都是一个向量）
   2. decoder：生成(y1, ..., y**m**)；解码器是一个一个y生成的，每一步都是一个自回归（输入又是你的输出）

2. Encoder and Decoder Stacks

   1. encoder

      6个完全一样的层堆叠而成，每个层都有两个子层，第一个是multi-head attention，第二个是MLP【？】，每个子层都有残差【？】连接；每一层的维度固定。

> 文章中提到的layer-norm和batch-norm
> + batch-norm：令每一列的feature，均值为0、方差为1（全局）
> + layer-norm：每一行（每个样本），均值为0、方差为1（每个样本）
> 因为每个样本都是一个向量（上面提到的z），所以是3D的，分别为每个样本batch、样本中每个词对应的向量seq，还有每个词的特征feat

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

