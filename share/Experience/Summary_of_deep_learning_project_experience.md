---
layout: page
title: Summary of Deep Learning Project Experience
permalink: /share/Experience/231121_1/
---

<table><tr><td bgcolor=lightgray><strong>"The whole process of data modeling and analysis" </strong></td></tr></table>

<em>Data modeling can be divided into several steps:</em>

_1. **Define Objectives**: Clearly define the business problem and determine objectives._

_2. **Data Understanding and Acquisition**: Acquire and understand data, followed by descriptive analysis._

_3. **Data Cleaning and Preprocessing**: Handle missing values, outliers, and duplicates._

_4. **Data Restructuring**: Labeling, standardization, etc.; further cleaning based on actual situations._

_5. **Descriptive Statistics and Insights**: Draw insights from descriptive statistics, forming the initial report._

_6. **Feature Selection and Model Selection**: Select variables and algorithms._

_7. **Dataset Partitioning and Model Construction**: Split dataset, set parameters, load algorithms, and build the model._

_8. **Model Evaluation**: Evaluate the model's performance._

_9. **Model Tuning**: Fine-tune the model for better results._

_10. **Output Rules and Presentation**: Determine output rules, load the model, and present results._

_11. **Model Deployment**: Deploy the model for practical use._

<em>More information can be found in the following link: </em><br>
<em><a href="https://zhuanlan.zhihu.com/p/558520007" title="">数据建模分析的全流程</a> </em>




<table><tr><td bgcolor=lightgray><strong>"A complete Pytorch deep learning project code structure and project release guide" </strong></td></tr></table>

<em>A common project structure is as follows:</em>

--project_name/<br>
----data/：Data<br>
----checkpoints/：Saved trained models<br>
----logs/：Logs<br>
----model_hub/：Pre-trained model weights<br>
--------chinese-bert-wwm-ext/：<br>
----utils/：Utility modules, such as logging, evaluation metrics, etc.<br>
--------utils.py<br>
--------metrics.py<br>
----models/：Models<br>
--------model.py<br>
----configs/：Configuration files<br>
--------config.py<br>
----datasets/：Data loading<br>
--------data_loader.py<br>
----main.py：Main program containing training, validation, testing, and prediction logic<br>

<em>More information can be found in the following link: </em><br>
<em><a href="https://blog.csdn.net/ARPOSPF/article/details/129162213" title="">一个完整的Pytorch深度学习项目代码结构及项目发布指南</a> </em>


<table><tr><td bgcolor=lightgray><strong>"Neural Network Hyperparameter Tuning: Loss Issues Compilation" </strong></td></tr></table>

<em>The issues are listed as follows:</em>

1. Reasons for Model Non-Convergence<br>
   1.1. Setting a high learning rate may lead to divergence (sudden increase in loss).<br>
   1.2. Generally, having a too-small database might not cause non-convergence issues.<br>
   1.3. Prefer using smaller models.<br>
2. Model Loss Not Decreasing<br>
   2.1. Loss remains constant at 87.33.<br>
   2.2. Loss consistently stays around 0.69.<br>
3. Summary of Solutions<br>
   3.1. Data and labels<br>
   3.2. Improperly set learning rate<br>
   3.3. Inappropriate network architecture<br>
   3.4. Dataset label settings<br>
   3.5. Data normalization<br>
   3.6. Excessive regularization<br>
   3.7. Choosing the appropriate loss function<br>
   3.8. Inadequate training time<br>

<em>More information can be found in the following links: </em><br>
<em><a href="https://blog.csdn.net/ytusdc/article/details/107738749" title="">神经网络调参：loss 问题汇总（震荡/剧烈抖动，loss不收敛/不下降）</a> </em><br>
<em><a href="https://tsinghua-gongjing.github.io/posts/DL-tricks.html" title="">深度学习调参技巧</a> </em><br>
<em><a href="https://blog.csdn.net/qq_41554005/article/details/119767740" title="">Pytorch 模型 查看网络参数的梯度以及参数更新是否正确，优化器学习率设置固定的学习率，分层设置学习率</a> </em><br>



<table><tr><td bgcolor=lightgray><strong>"The considerations for using common evaluation metrics" </strong></td></tr></table>

<em>The issues are listed as follows:</em>

```python
# coding: utf-8

from math import sqrt
from sklearn.metrics import mean_squared_error
from sklearn.metrics import accuracy_score
from sklearn import metrics
import torch
import os
import numpy as np

def obtain_acc(actual, pred):
    return accuracy_score(actual, pred)

def obtain_rmse(actual, pred):
    return sqrt(mean_squared_error(actual, pred))

def obtain_auc(actual, pred):
    fpr, tpr, threshholds = metrics.roc_curve(actual, pred, pos_label=1)
    auc = metrics.auc(fpr, tpr)
    return auc

def obtain_f1(actual, pred):
    f1 = metrics.f1_score(actual, pred)
    return f1

def obtain_rec(actual, pred):
    recal = metrics.recall_score(actual, pred)
    return recal

def obtain_pre(actual, pred):
    precision = metrics.precision_score(actual, pred)
    return precision

def obtain_confusion_matrix(actual, pred):
    confusion_matrix = metrics.confusion_matrix(actual, pred)
    return confusion_matrix
```

_1. obtain_auc(actual, pred) -> actual is discrete (e.g. 0,1) and pred is continuous (e.g. 0.3,0.8). To plot the ROC curve, it's necessary to sort the probability values indicating each test sample's likelihood of belonging to the positive class in descending order._


<table><tr><td bgcolor=lightgray><strong>"Python json.loads shows ValueError: Extra data" </strong></td></tr></table>

<em>Getting the error like ValueError: Extra data: line 88 column 2 - line 50607 column 2 (char 3077 - 1868399)</em><br>
<em>Error can be solved by just iterating over the file and loading each line as JSON in the loop:</em><br>
```python
tweets = []
with open('tweets.json', 'r') as file:
    for line in file:
        tweets.append(json.loads(line))
```
<em>This avoids storing intermediate python objects. As long as you write one full tweet per append() call, this should work.</em>



