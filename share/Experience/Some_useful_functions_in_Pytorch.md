---
layout: page
title: Some useful functions in Pytorch
permalink: /share/Experience/231118_1/
---


<table><tr><td bgcolor=lightgray><strong>Torch Functions for Matrix Operations</strong></td></tr></table>

- `torch.mul()`: _Performs element-wise multiplication (same as the multiplication symbol). Requires matrices to have the same dimensions. Broadcasting is allowed if the first dimension differs._
- `torch.mm()`: _Performs simple 2D matrix multiplication. Extensions include functions like `matmul()` and `bmm()`._
- `torch.matmul()`: _Performs matrix multiplication. When the inputs are two 2D matrices, it behaves similar to `torch.mm()`. If the inputs are a 3D and a 2D matrix, it considers the first dimension of the 3D tensor as batch size and performs matrix multiplication on the last two dimensions, resulting in a 3D tensor with unchanged batch size. When both inputs are 3D, it broadcasts the first dimension to match and then performs matrix multiplication on the last two dimensions._
- `np.dot()`: _If two vectors of the same size are passed, it performs a dot product and returns a scalar. If two matrices are passed, it performs matrix multiplication._



<table><tr><td bgcolor=lightgray><strong>"torch.nn.BatchNorm1d()" </strong></td></tr></table>

<em>torch.nn.BatchNorm1d(num_features, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)</em>

<em>The other parameters here are not important, just look at num_features. num_features is the dimension you need to normalize.
nn.BatchNorm1d itself is not a function that outputs the normalized result given an input matrix. Instead, it defines a method and then uses this method to perform normalization.
Below is an example:</em>

```python
BN = nn.BatchNorm1d(100)
input = torch.randn(20, 100)
output = m(input)
```

<em>We first define a normalized function BN, the dimension to be normalized is 100, and other parameters are default. Then randomly initialize a 20×100 matrix input, and then use BN to normalize this matrix.
The input of the function can be two-dimensional or three-dimensional. When the input dimension is (N, C), BN will normalize the C dimension; when the input dimension is (N, C, L), the normalized dimension is also the C dimension.</em>

<em>reference: <a href="https://blog.csdn.net/qsmx666/article/details/109527726" title="">pytorch：nn.BatchNorm1d()用法介绍</a> </em>



<table><tr><td bgcolor=lightgray><strong>"torch.nn.Dropout()" </strong></td></tr></table>

<em>Dropout is a trick proposed by Mr. Hinton for training. In pytorch, in addition to the original usage, there is also the usage of data enhancement (mentioned later).
The first thing to know is that dropout is specifically used for training. During the inference phase, dropout needs to be turned off, and model.eval() will do this.</em>

<em>The usual explanation of dropout is: in the forward propagation of the training process, each neuron is in an inactive state with a certain probability p. To achieve the effect of reducing overfitting.</em>

<em>If dropout is added to the input tensor, then, This operation means that there is a certain probability that the elements at each position of x will return to 0, in order to simulate the data loss of certain channels in real life and achieve the purpose of data augmentation.</em>

```python
x = torch.randn(20, 16)
dropout = nn.Dropout(p=0.2)
x_drop = dropout(x)
```
<em>More information can be found in the following link: </em>

<em><a href="https://blog.csdn.net/leviopku/article/details/120786990" title="">pytorch中nn.Dropout的使用技巧</a> </em>



<table><tr><td bgcolor=lightgray><strong>"torch.gather()" </strong></td></tr></table>

<em>The torch.gather function in PyTorch is used to gather values along a specified axis of a tensor according to specified indices. It allows you to select specific elements or sub-tensors from the input tensor based on the provided index tensor.</em>

```python
A = torch.randn(32, 49, 10)
B = torch.randint(0, 10, (32, 49))

# Extracts the value of the third dimension in A using the value in B as an index and adjusts the shape of A
A_new = torch.gather(A, 2, B.unsqueeze(-1))
A_new = A_new.squeeze(-1)
```

<em>More information can be found in the following link: </em>

<em><a href="https://blog.csdn.net/iteapoy/article/details/106203954" title="">图解torch.gather()的用法</a> </em>


<table><tr><td bgcolor=lightgray><strong>"torch.topk()" </strong></td></tr></table>

<em>torch.topk(input, k, dim=None, largest=True, sorted=True, out=None) -> (Tensor, LongTensor)</em>

<em>Find the top k largest or top k smallest values ​​of a certain dim in tensor and the corresponding index.</em>

<em>More information can be found in the following link: </em>

<em><a href="https://blog.csdn.net/qq_34914551/article/details/103738160" title="">PyTorch中的topk函数详解</a> </em>
