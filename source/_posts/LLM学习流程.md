---
title: LLM学习流程
date: 2022-03-12 23:57:00
categories:
	-LLM
---

# 大语言模型有价值的博客

随着chatgpt的火爆，大语言模型(Large Language Models)成为了AI之光，AI也逐渐从解决某一个垂直领域问题的打工仔，向解决通用问题的百科管家的通用模型更进一步。

如果想更多的了解大语言模型以及更多AI专业知识可以关注以下博客：

1.[AHEAD OF AI(By Sebastian Raschka, PhD)](https://magazine.sebastianraschka.com/)

2.the [Illustrated Transformer](http://jalammar.github.io/illustrated-transformer/) by Jay Alammar

3.a [more technical blog article](https://lilianweng.github.io/posts/2020-04-07-the-transformer-family/) by Lilian Weng

4.[a catalog and family tree](https://amatriain.net/blog/transformer-models-an-introduction-and-catalog-2d1e9039f376/) of all major transformers to date by Xavier Amatriain

5.[a minimal code implementation](https://github.com/karpathy/nanoGPT) of a generative language model for educational purposes by Andrej Karpathy

6.[a lecture series](https://sebastianraschka.com/blog/2021/dl-course.html#l19-self-attention-and-transformer-networks) and [book chapter](https://github.com/rasbt/machine-learning-book/tree/main/ch16) by yours truly

其中6是Sebastian Raschka的书籍对应的视频和书籍资料。

# 理解大语言模型的主要架构和任务

## Neural Machine Translation by Jointly Learning to Align and Translate

论文介绍了一种注意力机制，用于改进循环神经网络的长序列建模能力。这使得RNN能够准确翻译更长的句子，这也是后来开发Transformer架构的动机。

原始论文：

https://arxiv.org/abs/1409.0473

平替博客：

https://zhuanlan.zhihu.com/p/37212011 (论文解读)

https://blog.51cto.com/u_15995006/6109244 (逻辑解析)

## Attention Is All You Need

这一篇是引用最为广泛的经典论文，介绍了最初的Transformer架构，包括后来成为单独模块的编码器和解码器部分。此外，还介绍了缩放点积注意力机制、多头注意力块和位置输入编码等概念，这些概念仍然是现代Transformer的基础。

原始论文：

https://arxiv.org/abs/1706.03762

平替博客：

https://zhuanlan.zhihu.com/p/350739760 （论文解读）

https://zhuanlan.zhihu.com/p/62397974 （逻辑解析）

https://zhuanlan.zhihu.com/p/44731789 （逻辑解析）

## BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

沿用原始的Transformer架构，大型语言模型研究开始分为两个方向：编码器风格的Transformer用于预测建模任务，如文本分类，解码器风格的Transformer用于生成建模任务，如翻译，摘要和其他形式的文本创作。而这一篇介绍了BERT掩码语言建模的原始概念，而下一个句子的预测仍然是一种有影响力的解码器风格架构。可以继续关注RoBERTa，它通过删除下一个句子的预测任务简化了预训练目标。

原始论文：

https://arxiv.org/abs/1810.04805

Code：

https://github.com/codertimo/BERT-pytorch

平替博客：



# 参考文献

[系统学习大模型的20篇论文](https://blog.csdn.net/wireless_com/article/details/130798925)









