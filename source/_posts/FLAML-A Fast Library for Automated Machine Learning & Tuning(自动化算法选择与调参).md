---
title: FLAML-A Fast Library for Automated Machine Learning & Tuning(自动化算法选择与调参)
date: 2022-12-13 18:26:00
categories:
	-机器学习框架
---

# 1 AutoML综述

当我们需要训练一个机器学习模型时，算法选择以及参数调整是一个难以回避的问题，我该选用哪种机器学习算法？我的算法参数应该怎么调整呢？选择合适的模型并是一个需要高计算成本、时间和精力的过程。

基于这个问题就提出了AutoML(Automated machine learning)的概念，本篇文章我你们主要介绍由微软开发的高效轻量级自动化机器学习框架FLAML(A Fast Library for Automated Machine Learning & Tuning).

# 2 FLAML框架

## 2.1 FLAML框架特点

根据FLAML官网的描述，该框架主要有以下三个特点：

1.弹指间发现高质量模型，FLAML可以使用较少的计算资源为常规机器学习任务发现正确的模型，让使用者无需再为算法选择和参数调整发愁。

2.框架易于自定义或扩展，FLAML在设计时就考虑了框架的可拓展性，比如在框架内加入自定义的算法或者自定义衡量指标。

3.参数调整迅速，调到你满意为止，FLAML提供了一种高效的自动化调参工具，该工具使用了新的高性价比的调参方法，能有处理处理复杂的参数调优问题。

## 2.2 FLAML框架教程

教程细节见：

https://github.com/microsoft/FLAML/tree/tutorial/tutorial

https://microsoft.github.io/FLAML/docs/Getting-Started
