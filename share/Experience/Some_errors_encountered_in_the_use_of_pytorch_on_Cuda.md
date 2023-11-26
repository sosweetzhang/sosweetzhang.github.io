---
layout: page
title: Some errors encountered in the use of PyTorch on Cuda
permalink: /share/Experience/231106_1/
---

<table><tr><td bgcolor=lightgray><strong>"CUDA error: CUBLAS_STATUS_NOT_INITIALIZED when calling cublasCreate(handle)" </strong></td></tr></table>

<em>This error might be raised, if you are running out of memory and cublas fails to create the handle, so try to reduce the memory usage e.g. via a smaller batch size.</em>



<table><tr><td bgcolor=lightgray><strong>"{RuntimeError}Expected a 'cuda' device type for generator but found 'cpu'" </strong></td></tr></table>

<em>This is an error encountered in the use of "torch.utils.data.random_split". And it is solved by adding the "generator=torch.Generator(device=device)" as follows:</em>

```python
train_dataset, validate_dataset = torch.utils.data.random_split(dataset, [train_size, validate_size]) # incorrect
train_dataset, validate_dataset = torch.utils.data.random_split(dataset, [train_size, validate_size], generator=torch.Generator(device=device)) # correct
```

<em> More information can be found in the following links: </em>

<em><a href="https://blog.csdn.net/weixin_45809449/article/details/123635839" title="">Expected a ‘cuda‘ device type for generator but found ‘cpu‘的解决方法</a> </em>

<em><a href="https://discuss.pytorch.org/t/runtimeerror-expected-a-cuda-device-type-for-generator-but-found-cpu/161463" title="">RuntimeError: Expected a ‘cuda’ device type for generator but found ‘CPU’</a> </em>


<table><tr><td bgcolor=lightgray><strong>"RuntimeError: Boolean value of Tensor with more than one value is ambiguous" </strong></td></tr></table>

<em>The general meaning is that the tensor contains multiple (more than 1 but not 1) boolean values, which is unclear, that is, it cannot be compared. The reason for the error may be that the loss function is declared without parentheses or the callable object is used without parentheses.</em>

```python
loss_function=nn.MSELoss   # correct
loss_function=nn.MSELoss() # incorrect
```

<em> More information can be found in the following link: </em>

<em><a href="https://blog.csdn.net/weixin_43818631/article/details/122255929" title="">RuntimeError: Boolean value of Tensor with more than one value is ambiguous</a> </em>



<table><tr><td bgcolor=lightgray><strong>"ValueError: multilabel-indicator format is not supported" </strong></td></tr></table>

<em>This is an error encountered in running "fpr, tpr, thresholds = metrics.roc_curve(actual, pred, pos_label=1)". At first, the shape of actual and pred are (batch_size, seq) which meets this error. Then I reshape the shape to 1 dimension and the problem is solved.</em>

<em>This function expects inputs in a certain format, usually either a 1D array for binary classification or a 2D array for multi-class classification. Adjusting the shape of your input arrays to match these expectations can help resolve this issue. By using .ravel() or another method to reshape your actual and pred arrays to the desired format, you can avoid the error related to the shape mismatch when using metrics.roc_curve(). </em>

<em>In addition, there is a useful function torch.masked_select(x, mask) which can mask the noise in x according to the boolean in the mask. Note that the value in mask is boolean not 0 or 1. More information can be found in the following link: </em>

<em><a href="https://zhuanlan.zhihu.com/p/348035584" title="">PyTorch中的masked_select选择函数</a> </em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: Expected all tensors to be on the same device, but found at least two devices, cuda:1 and cpu! (when checking argument for argument index in method wrapper_gather)</strong></td></tr></table>

<em>Here are some useful links to convert data and code from the CPU to the GPU：</em>

<em><a href="https://blog.csdn.net/mxh3600/article/details/124460988" title="">Pytorch中实现CPU和GPU之间的切换</a> </em>

<em><a href="https://xiaosongshine.blog.csdn.net/article/details/89401522?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-89401522-blog-124233475.235%5Ev38%5Epc_relevant_anti_t3_base&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-89401522-blog-124233475.235%5Ev38%5Epc_relevant_anti_t3_base&utm_relevant_index=5" title="">PyTorch如何使用GPU加速（CPU与GPU数据的相互转换）</a></em>

<em><a href="https://www.cnblogs.com/picassooo/p/13736843.html" title="">PyTorch查看模型和数据是否在GPU上</a></em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: CUDA error: device-side assert triggered CUDA kernel errors might be asynchronously reported at some other API call, so the stacktrace below might be incorrect. For debugging consider passing CUDA_LAUNCH_BLOCKING=1</strong></td></tr></table>

<em>While I tried your code, and it did not give me an error, I can say that usually the best practice to debug CUDA Runtime Errors: device-side assert like yours is to turn collab to CPU and recreate the error. It will give you a more useful traceback error.</em>

<em>Most of the time CUDA Runtime Errors can be the cause of <font color=Blue>some index mismatching</font> so like you tried to train a network with 10 output nodes on a dataset with 15 labels. And the thing with this CUDA error is once you get this error, you will receive it for every operation you do with torch.tensors. This forces you to restart your notebook.</em>

<em>I suggest you restart your notebook, get a more accurate traceback by <font color=Blue>moving to CPU</font>, and check the rest of your code especially if you train a model on the set of targets somewhere.</em>


<table><tr><td bgcolor=lightgray><strong>RuntimeError: Expected tensor for argument #1 'indices' to have scalar type Long; but got CUDAType instead (while checking arguments for embedding)</strong></td></tr></table>

<em>I would suggest you check the input type I had the same issue which was solved by <font color=Blue>converting the input type from int32 to int64</font>.(running on win10) ex: x = torch.tensor(train).to(torch.int64)</em>


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

<em>Now you can also set the roc_auc_score to be zero if there is only one class present. However, I wouldn't do this. I guess your test data is highly unbalanced. I would suggest using a stratified K-fold instead so that you at least have both classes present.</em>


<table><tr><td bgcolor=lightgray><strong>Import "cv2" could not be resolved. ModuleNotFoundError: No module named 'cv2'</strong></td></tr></table>

<em>It just happened to me and I solved it by installing both opencv-python and opencv-python-headless with pip and reloading the Visual Studio Code window right after it.</em>

<em>To install the needed packages, just run this command in the terminal:</em>

```python
$ pip install opencv-python opencv-python-headless
```
