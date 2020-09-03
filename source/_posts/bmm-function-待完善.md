---
title: bmm function(待完善)
date: 2020-08-24 11:32:41
tags: Pytorch
categories: Pytorch function
mathjax: true
---
[官方文档: torch.bmm(), version=1.2.0](https://pytorch.org/docs/1.2.0/torch.html?highlight=bmm#torch.bmm)

`torch.bmm()`用于实现矩阵的乘法，其引用方式为：

```python
torch.bmm(input, mat2, deterministic = False, out = None)
# 参数：
# ！！！input和mat2的都需要是3-D tensor，即维度等于3
# input(Tensor): 第一个用于矩阵乘法的batch
# mat2(Tensor): 第二个用于矩阵乘法的batch
# out(Tensor, optional): 输出结果
```

除了需要满足`input`和`mat2`的维度一致，相似于线性代数的矩阵相乘，`bmm()`的矩阵乘法也约束了当`input`的维度为$(b\times n\times m)$，`mat2`的维度应为$(b\times m\times p)$，相乘结果`out`维度为$(b\times n\times p)$。

```python
# example
import torch
# optional
out1 = torch.empty(0)
input = torch.randn(3,4,5)
mat2 = torch.randn(3,5,6)
# method 1
torch.bmm(input, mat2, out = out1)
# method 2
torch.bmm(input, mat2, out = mat2)
# method 3
out2 = torch.bmm(input, mat2)
```


