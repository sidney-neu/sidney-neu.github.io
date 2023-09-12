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

https://blog.51cto.com/u_15995006/6109244 (代码逻辑解析)