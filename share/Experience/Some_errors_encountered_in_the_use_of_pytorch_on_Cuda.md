---
layout: page
title: Some errors encountered in the use of pytorch on Cuda
permalink: /share/Experience/231106_1/
---

<table><tr><td bgcolor=lightgray><strong>RuntimeError: Expected all tensors to be on the same device, but found at least two devices, cuda:1 and cpu! (when checking argument for argument index in method wrapper_gather)</strong></td></tr></table>

<em>Here are some useful links to convert data and code from the CPU to the GPU：</em>

<em><a href="https://blog.csdn.net/mxh3600/article/details/124460988" title="">Pytorch中实现CPU和GPU之间的切换</a> </em>

<em><a href="https://xiaosongshine.blog.csdn.net/article/details/89401522?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-89401522-blog-124233475.235%5Ev38%5Epc_relevant_anti_t3_base&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-89401522-blog-124233475.235%5Ev38%5Epc_relevant_anti_t3_base&utm_relevant_index=5" title="">PyTorch如何使用GPU加速（CPU与GPU数据的相互转换）</a></em>

<em><a href="https://www.cnblogs.com/picassooo/p/13736843.html" title="">PyTorch查看模型和数据是否在GPU上</a></em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: CUDA error: device-side assert triggered CUDA kernel errors might be asynchronously reported at some other API call,so the stacktrace below might be incorrect. For debugging consider passing CUDA_LAUNCH_BLOCKING=1</strong></td></tr></table>

<em>While I tried your code, and it did not give me an error, I can say that usually the best practice to debug CUDA Runtime Errors: device-side assert like yours is to turn collab to CPU and recreate the error. It will give you a more useful traceback error.</em>

<em>Most of the time CUDA Runtime Errors can be the cause of <font color=Blue>some index mismatching</font> so like you tried to train a network with 10 output nodes on a dataset with 15 labels. And the thing with this CUDA error is once you get this error once, you will recieve it for every operation you do with torch.tensors. This forces you to restart your notebook.</em>

<em>I suggest you restart your notebook, get a more accuracate traceback by <font color=Blue>moving to CPU</font>, and check the rest of your code especially if you train a model on set of targets somewhere.</em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: Expected tensor for argument #1 'indices' to have scalar type Long; but got CUDAType instead (while checking arguments for embedding)</strong></td></tr></table>

<em>I would suggest you to check the input type I had the same issue which solved by <font color=Blue>converting the input type from int32 to int64</font>.(running on win10) ex: x = torch.tensor(train).to(torch.int64)</em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: expected scalar type Double but found Float</strong></td></tr></table>

<em>You can use <font color=Blue>model.double()</font> to convert all the model parameters into double type. This should give a compatible model given your input data is double. Keep in mind though that double type is usually slower than single due to its higher precision nature. You can also use <font color=Blue>model.float()</font> to convert all the model parameters into float type.</em>


<table><tr><td bgcolor=lightgray><strong>roc_auc_score - Only one class present in y_true</strong></td></tr></table>

<em>You could use try-except to prevent the error:</em>

```python
import numpy as np
from sklearn.metrics import roc_auc_score
y_true = np.array([0, 0, 0, 0])
y_scores = np.array([1, 0, 0, 0])
try:
    roc_auc_score(y_true, y_scores)
except ValueError:
    pass
```

<em>Now you can also set the roc_auc_score to be zero if there is only one class present. However, I wouldn't do this. I guess your test data is highly unbalanced. I would suggest to use stratified K-fold instead so that you at least have both classes present.</em>

