# Multi-Modal Attention Network Learning for Semantic Source Code Retrieval

> Source: ASE-2019
>
> Tag: multi-modal, attention, code retrieval

## Abstract

1. 现有研究缺陷：只表示浅层特征、缺乏可解释性

2. 提出方法

   2.1 使用多模态表示：token序列、AST和CFG

    	a) token序列：LSTM
    	
    	b) AST：Tree-LSTM（体现程序层次语法结构）

   ​	 c) CFG：GGNN（体现程序计算和控制流）

   2.2 attention融合层：每个模态的不同部分赋予不同权重

   ​	不同部分指token、AST和CFG的node，以推断哪一部分对最终结果贡献更大

## Ⅰ Introduction

1. 代码检索的挑战：源代码深层语义理解、跨模态检测相似性

2. 现有工作问题：第一个应用深度网络作代码检索工作的问题有浅层次特征、缺乏可解释性等

3. 本论文解决方案和贡献

   ① 多模态表示方法，用融合层集成

   ② 首次用attention网络对同一模态的不同部分赋权，并获得可解释性

## Ⅱ Related Work

+ 包括Deep Code Representation、Multi-Modal Learning、Attention Mechanism等

+ 对于文本的attention机制：关注输入和输出的”对齐“【？】

## Ⅲ Preliminaries

1. 问题的数学表达

+ 代码片段（token、AST、CFG表示）和对应描述

+ 模型同时学习代码片段和描述的中间语义空间表示

2. 多模态学习：joint / coordinated【？】

3. 注意力机制【？】

+ 给定query、key，得到attetion value

+ 最终attention得分是对内存中值累加

## Ⅳ Multi-modal attention network

1. 概述：Online和Offline两部分

2. 多模态代码表示

   2.1 词法层面：token，LSTM

   2.2 语法层面：AST，Tree-LSTM（previous的那元只有一个forget门【？】）

   2.3 语法层面：CFG，GGNN

3. 多模态attention混合【？】

   3.1 token、AST、CFG的attention weight计算方法

   3.2 fusion：连接 + 网络处理

4. 描述表示：vallina LSTM【？】

5. 模型学习：期望预测与正确描述的高相似性（这里的图3对应的是论文1的哪个？）

6. 代码检索：余弦相似度

## Ⅴ Experiments and analysis

+ 是否提高了检索性能：Yes

+ 每个modal的有效性和贡献：互补

+ 改变代码长度、AST结点数后的性能：...

+ 定性分析和可视化

还有数据集、评估标准、其他细节等。

## Ⅵ Discussion

作用、有效性和局限性等

## Ⅶ Conclusion and future work

1. 使用了顺序特征token和结构化数据AST和CFG
2. 使用了基于attention机制的融合层
3. 模型同时学习代码表示和自然语言查询
