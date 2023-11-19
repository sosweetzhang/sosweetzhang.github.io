---
layout: page
title: Some insights from using LSTM in KT
permalink: /share/Experience/231119_1/
---

<table><tr><td bgcolor=lightgray><strong>"The 'shift' operation in LSTM or other sequential model" </strong></td></tr></table>

<em>In LSTM or other sequential model applications, the 'shift' operation is often employed in creating input and target sequences.</em>

<em>The following is an example referring to the code from <a href="https://github.com/hcnoh/knowledge-tracing-collection-pytorch/blob/main/models/utils.py" title="">utils.py</a></em>

```python
q_seqs.append(FloatTensor(q_seq[:-1]))
r_seqs.append(FloatTensor(r_seq[:-1]))
qshft_seqs.append(FloatTensor(q_seq[1:]))
rshft_seqs.append(FloatTensor(r_seq[1:]))
```

<em>In the given code snippet:</em>

- `q_seqs.append(FloatTensor(q_seq[:-1]))`: This line creates the input sequence `q_seqs` from the question sequence. It consists of all elements from the beginning of the sequence up to the second-to-last element, excluding the last element. This sequence serves as the model's input. During training, the model attempts to predict the next element or next time step's content based on this input sequence.

- `r_seqs.append(FloatTensor(r_seq[:-1]))`: Similarly, this line creates the input sequence for the response sequence `r_seqs`. It excludes the last element of the response sequence, serving as the model's input.

- `qshft_seqs.append(FloatTensor(q_seq[1:]))` and `rshft_seqs.append(FloatTensor(r_seq[1:]))`: These lines create the target sequences for the question and response sequences. They start from the second element of the sequence up to the last element, which serves as the training target for the model. During training, the model attempts to predict the elements in the target sequences.

<em>In short, the purpose of doing the 'shift' operation is to ensure that the input information at the previous moment predicts the information at the next moment. If the 'shift' operation is not performed, then the current moment will be input to predict the current moment, resulting in untrustworthy model effects, or even AUC=1, ACC=1 occurs.</em>

