---
layout: page
title: Summary of Deep Learning Project Experience
permalink: /share/Experience/231121_1/
---

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
<em><a href="https://blog.csdn.net/ytusdc/article/details/107738749" title="">神经网络调参：loss 问题汇总（震荡/剧烈抖动，loss不收敛/不下降）</a> </em>
<em><a href="https://blog.csdn.net/qq_41554005/article/details/119767740" title="">Pytorch 模型 查看网络参数的梯度以及参数更新是否正确，优化器学习率设置固定的学习率，分层设置学习率</a> </em>

