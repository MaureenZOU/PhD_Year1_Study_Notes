# Video Object Segmentation Survey

### So Interesting !!!!
#### Spatial Transformer Network [\[Paper\]](https://papers.nips.cc/paper/5854-spatial-transformer-networks.pdf) [\[Code\]](https://pytorch.org/tutorials/intermediate/spatial_transformer_tutorial.html)

* Summary: This paper propose a generic network module to shift, rotate and rescale the image according to coordinate transformation.

![alt text](https://github.com/MaureenZOU/PhD_Year1_Study_Notes/blob/master/VOS_Survey/imgs/stn.png)

* Comment: It is the best kind of research, apply very light but mathematical things to deep learning and make it a differenciable module. Good performance. 

#### Sequential Clique Optimization for Video Object Segmentation [\[Paper\]](https://arxiv.org/pdf/1807.01452.pdf) [\[dataset\]](https://sites.google.com/view/ltnghia/research/sesiv?authuser=0)

* Summary: It use static image instance segmentation to get all the instance proposals for video object segmentation. Then, they use traditional graph theory to combine the static image mask to formulate a sequce.

* Comment: I like this paper, althought it is not an impact work. Because, it use some really clean tecnique (iamge instance segmentation and graph theory) to solve a really dirty problem.

### Reasonable Paper
#### Semantic Instance Meets Salient Object: Study on Video Semantic Salient Instance Segmentation [\[Paper\]](https://arxiv.org/pdf/1807.01452.pdf) [\[dataset\]](https://sites.google.com/view/ltnghia/research/sesiv?authuser=0)

* Summary: This paper propose a dataset with semantic salient instacne objects. They label several most obvious objects in DAVIS but not a full instance masks. Also, they propose a baseline for their tasks. 

* Comment: The dataset is useful somehow, but they didn't annotate all the instance, which is an obvious drawback.

#### Predicting Future Instance Segmentation by Forecasting Convolutional Features [\[Paper\]](https://arxiv.org/pdf/1803.11496.pdf) [\[Code\]](https://github.com/facebookresearch/instpred)

* Summary: This paper integrate the region proposal of frame T, T-1, T-k ... to predict the instance segmantation mask of next frame.
![alt text](https://github.com/MaureenZOU/PhD_Year1_Study_Notes/blob/master/VOS_Survey/imgs/2.png)

* Comment: Idea seems to be really interesting, but the paper written is bad bad bad. I can't fully understand by reading it twice.

#### Learning Video Object Segmentation with Visual Memory [\[Paper\]](https://lear.inrialpes.fr/people/alahari/papers/tokmakov17a.pdf)

* Summary: This paper integrate the information from optical flow and a pretrained semantic segmantation Network. And use a ConvGRU module to remember T-1 input.
![alt text](https://github.com/MaureenZOU/PhD_Year1_Study_Notes/blob/master/VOS_Survey/imgs/3.png)

* Comment: Somehow make sense. But not as explict as we want. 

#### Video Object Segmentation Without Temporal Information [\[Paper\]](https://arxiv.org/pdf/1709.06031.pdf)

* Summary: This paper use temporal information to select the correct instance from single image prediction.
* Comment: It works, but it didn't combine the advatance of image and video path.

#### Video Object Segmentation Without Temporal Information [\[Paper\]](https://arxiv.org/pdf/1709.06031.pdf)

* Summary: It only use static image to train the network and video to finetune. It take advantage of a large amount of static image without temporal information. It uses the "shaked" static image mask as input to predict the finegrained mask. During test time, we input mask t-1, and predict mask t. 

* Comment: This is a really interesting paper to learn. Even I can think out idea related to maskrcnn. 

### Anyway, they are boring papers to read

