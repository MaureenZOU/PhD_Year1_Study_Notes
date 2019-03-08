# Video Object Segmentation Survey

### So Interesting !!!!
#### Spatial Transformer Network [\[Paper\]](https://papers.nips.cc/paper/5854-spatial-transformer-networks.pdf) [\[Code\]](https://pytorch.org/tutorials/intermediate/spatial_transformer_tutorial.html)

* Summary: This paper propose a generic network module to shift, rotate and rescale the image according to coordinate transformation.

![alt text](https://github.com/MaureenZOU/PhD_Year1_Study_Notes/blob/master/VOS_Survey/imgs/stn.png)

* Comment: It is the best kind of research, apply very light but mathematical things to deep learning and make it a differenciable module. Good performance. 

### Reasonable Paper
#### Semantic Instance Meets Salient Object: Study on Video Semantic Salient Instance Segmentation [\[Paper\]](https://arxiv.org/pdf/1807.01452.pdf) [\[dataset\]](https://sites.google.com/view/ltnghia/research/sesiv?authuser=0)

* Summary: This paper propose a dataset with semantic salient instacne objects. They label several most obvious objects in DAVIS but not a full instance masks. Also, they propose a baseline for their tasks. 

* Comment: The dataset is useful somehow, but they didn't annotate all the instance, which is an obvious drawback.

#### Predicting Future Instance Segmentation by Forecasting Convolutional Features [\[Paper\]](https://arxiv.org/pdf/1803.11496.pdf) [\[Code\]](https://github.com/facebookresearch/instpred)

* Summary: This paper integrate the region proposal of fram T, T-1, T-k ... to predict the instance segmantation mask of next frame.

* Comment: Idea seems to be really interesting, but the paper written is bad bad bad. I can't fully understand by reading it twice. 

### Anyway, they are boring papers to read

