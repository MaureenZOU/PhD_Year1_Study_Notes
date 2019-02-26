# Computer-Vision---An-Implementation-Survey

Explore Top Researchers' work, get the fowllowing information:
* An experiment base Problem Setting (Input, Output)
* Model Structure
* Network Structure
* Dataset Scale
* Data Augmentation
* Initialization and Optimization



## Kaiming He
### [Deep Residual Learning for Image Recognition](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf)
- ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) `Classification and Object Detection`

#### Problem Setting
* ImageNet/Cifar 10 Classification
* Object Detection on PASCAL and MS COCO

#### Model Structure
A general Encoder structure

#### Network Structure
![alt text](https://github.com/MaureenZOU/What-could-Deep-Learning-do/blob/master/imgs/resnet.png)

![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `why the channel size first increase and decrease like 256 - 1024 - 512`

#### Dataset Scale
1.28 million train, 50k validation, 100k test images (ImageNet), 1000 class
50k train, 10k test, 10 class


#### Data Augmentation
* Scale Augmentation \[256, 480\] [ref](https://arxiv.org/pdf/1409.1556.pdf)
* Flipping (left and right flip)
* Random Crop (224)
* Mean subtraction (per pixel)
* Standard color augmentation [ref](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)
- ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) `First, I think this method has the similar effect with ColorJitter in PyTorch code. However as the below repo points out that, this modification may have offset with batchnorm. We could just think, we shift the data around to make the network easy to train. But if we make the data harder, then there is an offset effect for batch-norm.`
[repo](https://github.com/koshian2/PCAColorAugmentation)
* Batch Normalization after each convolution before activation

#### Initialization and Optimization
* Kaiming Initialization
* SGD  lr = 0.1, divided by 10 when the error plateaus, weight decay of 0.0001, a momentum of 0.9
* 60 × 10^4 iterations (This number is their max training iterations)
![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `This should be high lighted. For myself I usually go through lots of epochs (It seems wrong now), but according to He's paper, they even not go through all the training data in ImageNet. (Which is actually strange)`
* batch_size = 128/256

## Saining Xie

### [Aggregated Residual Transformations for Deep Neural Networks](https://arxiv.org/pdf/1611.05431.pdf)
- ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) `Classification and Object Detection`

#### Problem Setting
* ImageNet/Cifar 10 classification
* Object Detection

#### Model Structure
A general Encoder structure

#### Network Structure


